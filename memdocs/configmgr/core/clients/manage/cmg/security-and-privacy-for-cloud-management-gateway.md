---
title: Zabezpečení a ochrana osobních údajů v CMG
titleSuffix: Configuration Manager
description: Přečtěte si o pokynech a doporučeních pro zabezpečení a ochranu osobních údajů s bránou pro správu cloudu.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/26/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7304730b-b517-4c76-aadd-4cbd157dc971
ms.openlocfilehash: 93427cb34b2216bf16f713818481e69573a4b0de
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712887"
---
# <a name="security-and-privacy-for-the-cloud-management-gateway"></a>Zabezpečení a ochrana osobních údajů pro bránu pro správu cloudu

*Platí pro: Configuration Manager (Current Branch)*

Tento článek obsahuje informace o zabezpečení a ochraně osobních údajů pro Configuration Manager bránu pro správu cloudu (CMG). Další informace najdete v tématu [Plánování brány pro správu cloudu](plan-cloud-management-gateway.md).

## <a name="cmg-security-details"></a>Podrobnosti o zabezpečení CMG

- CMG přijímá a spravuje připojení z přípojných bodů CMG. Používá vzájemné ověřování SSL pomocí certifikátů a ID připojení.
- CMG přijímá a předávají požadavky klientů pomocí následujících metod:
    - Předem ověřuje připojení pomocí vzájemného protokolu SSL s certifikátem ověřování klientů na základě infrastruktury veřejných klíčů nebo Azure AD.
      - Služba IIS na instancích virtuálních počítačů CMG ověřuje cestu k certifikátu na základě důvěryhodných kořenových certifikátů odeslaných do CMG.
      - Služba IIS na instanci virtuálního počítače také ověřuje odvolání klientského certifikátu, pokud je povoleno. Další informace najdete v tématu [publikování seznamu odvolaných certifikátů](#bkmk_crl).
    - Seznam důvěryhodných certifikátů kontroluje kořen certifikátu pro ověřování klientů. Provádí také stejné ověření jako bod správy pro klienta. Další informace najdete v tématu [Kontrola záznamů v seznamu důvěryhodných certifikátů pro daný web](#bkmk_ctl).
    - Ověřuje a filtruje požadavky klienta (adresy URL), aby zkontroloval, jestli kterýkoli bod připojení CMG může požadavek obsluhovat.  
    - Kontroluje délku obsahu pro každý koncový bod publikování.
    - K vyrovnávání zatížení CMG přípojných bodů ve stejné lokalitě používá chování kruhového dotazování.
- Bod připojení CMG používá následující metody:
    - Vytvoří konzistentní připojení HTTPS/TCP ke všem instancím virtuálních počítačů CMG. Každou minutu kontroluje a udržuje tato připojení.
    - Používá vzájemné ověřování SSL s CMG pomocí certifikátů.
    - Přepošle požadavky klienta na základě mapování adres URL.
    - Oznamuje stav připojení k zobrazení stavu služby v konzole nástroje.
    - Oznamuje provoz na koncový bod každých pět minut.

### <a name="configuration-manager-client-facing-roles"></a>Configuration Manager rolí klienta

Body správy a koncové body hostitele bodu aktualizace softwaru ve službě IIS pro požadavky klientů na službu. CMG nevystavuje všechny vnitřní koncové body. Každý koncový bod publikovaný na CMG má mapování adresy URL.

- Externí adresa URL je ta, kterou klient používá ke komunikaci s CMG.
- Interní adresa URL je bod připojení CMG, který se používá k přeposílání požadavků na interní server.

#### <a name="url-mapping-example"></a>Příklad mapování adres URL

Pokud povolíte CMG provoz v bodu správy, vytvoří Configuration Manager interní sadu mapování adres URL pro každý server bodu správy. Například: ccm_system, ccm_incoming a sms_mp. Externí adresa URL bodu správy ccm_system koncový bod může vypadat takto:  
`https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System`  
Adresa URL je jedinečná pro každý bod správy. Klient Configuration Manager pak vloží název bodu správy s povoleným CMG do seznamu bodů správy sítě Internet. Tento název vypadá takto:  
`<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>`  
Lokalita automaticky nahraje všechny publikované externí adresy URL do CMG. Toto chování umožňuje CMG filtrování adres URL. Všechna mapování adres URL se replikují do spojovacího bodu CMG. Pak předá komunikaci interním serverům podle externí adresy URL z žádosti klienta.


## <a name="security-guidance-for-cmg"></a>Doprovodné materiály k zabezpečení pro CMG

<a name="bkmk_crl"></a>

### <a name="publish-the-certificate-revocation-list"></a>Publikování seznamu odvolaných certifikátů

Publikování seznamu odvolaných certifikátů PKI (CRL) pro internetové klienty pro přístup. Při nasazování CMG pomocí PKI nakonfigurujte službu tak, aby **ověřila odvolání klientského certifikátu** na kartě nastavení. Toto nastavení nakonfiguruje službu tak, aby používala publikovaný seznam odvolaných certifikátů (CRL). Další informace najdete v tématu [Plánování odvolání certifikátu PKI](../../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

Tato možnost CMG ověřuje certifikát pro ověřování klientů.

- Pokud klient používá ověřování Azure AD, nezáleží na seznamu CRL.
- Pokud používáte PKI a externě publikujete seznam odvolaných certifikátů, pak tuto možnost povolte (doporučeno).
- Pokud používáte infrastrukturu veřejných klíčů (PKI), nepublikujte seznam CRL a pak tuto možnost vypněte.
- Pokud tuto možnost nenakonfigurujete, může to způsobit další provoz od klientů až po CMG. Tento další provoz může zvýšit objem dat Azure pro výstup, což může zvýšit náklady na Azure.<!-- SCCMDocs#1434 -->

<a name="bkmk_ctl"></a>

### <a name="review-entries-in-the-sites-certificate-trust-list"></a>Zkontrolujte položky v seznamu důvěryhodných certifikátů pro daný web.

<!--503739-->
Každá Configuration Manager lokalita obsahuje seznam důvěryhodných kořenových certifikačních autorit, seznam důvěryhodných certifikátů (CTL). Seznam můžete zobrazit a upravit tak, že v pracovním prostoru Správa rozbalte nabídku Konfigurace lokality a vyberete možnost lokality. Vyberte lokalitu a na pásu karet klikněte na vlastnosti. Přepněte na kartu **komunikace s klientským počítačem** a pak klikněte na **nastavit** v části Důvěryhodné kořenové certifikační autority.

> [!Note]
> Počínaje verzí 1906 se tato karta nazývá **zabezpečení komunikace**.<!-- SCCMDocs#1645 -->  

Pro lokalitu s CMG pomocí ověřování klientů PKI použijte více omezující seznam CTL. V opačném případě budou klienti s ověřovacími certifikáty klientů vydanými jakýmkoli důvěryhodným kořenovým adresářem, který již existuje v bodu správy, automaticky přijati pro registraci klienta.

Tato podmnožina poskytuje správcům větší kontrolu nad zabezpečením. Seznam CTL omezí server tak, aby přijímal jenom klientské certifikáty vydané certifikačními autoritami v seznamu CTL. Například Windows se dodává s řadou známých certifikátů certifikační autority (CA) třetích stran, jako jsou VeriSign a Thawte. Ve výchozím nastavení počítač, ve kterém je služba IIS, důvěřuje certifikátům, které jsou zřetězené na tyto dobře známé certifikační autority. Bez konfigurace služby IIS se seznamem CTL je každý počítač, který má klientský certifikát vydaný z těchto certifikačních autorit, přijatý jako platný klient Configuration Manager. Pokud službu IIS nakonfigurujete se seznamem CTL, který nezahrnuje tyto certifikační autority, připojení klientů se odmítne, pokud se certifikát řetězí k těmto certifikačním autoritám.

### <a name="enforce-tls-12"></a><a name="bkmk_tls"></a>Vynutilit TLS 1,2

<!-- SCCMDocs-pr#4021 -->

Počínaje verzí 1906 použijte nastavení CMG k **vymáhání TLS 1,2**. Vztahuje se jenom na virtuální počítač Azure Cloud Service. Nevztahuje se na žádné místní Configuration Manager servery lokality nebo klienty. Další informace o TLS 1,2 najdete v článku [Jak povolit tls 1,2](../../../plan-design/security/enable-tls-1-2.md).


<!--486209-->


<!-- ## Privacy information for CMG -->


## <a name="next-steps"></a>Další kroky

- [Plánování brány pro správu cloudu](plan-cloud-management-gateway.md)
- [Instalace brány pro správu cloudu](setup-cloud-management-gateway.md)
- [Nejčastější dotazy týkající se brány pro správu cloudu](cloud-management-gateway-faq.md)
- [Certifikáty brány pro správu cloudu](certificates-for-cloud-management-gateway.md)
