---
title: Certifikáty CMG
titleSuffix: Configuration Manager
description: Přečtěte si o různých digitálních certifikátech, které se mají používat s bránou pro správu cloudu.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.openlocfilehash: 33e4ecbac965206ec4043f5adf91d2dbfb9602d8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714077"
---
# <a name="certificates-for-the-cloud-management-gateway"></a>Certifikáty pro bránu pro správu cloudu

*Platí pro: Configuration Manager (Current Branch)*

V závislosti na scénáři, který používáte ke správě klientů na internetu s bránou pro správu cloudu (CMG), budete potřebovat jeden nebo více z následujících digitálních certifikátů:  

- [Ověřovací certifikát serveru CMG](#bkmk_serverauth)  
  - [CMG důvěryhodný kořenový certifikát pro klienty](#bkmk_cmgroot)  
  - [Certifikát ověřování serveru vydaný veřejným poskytovatelem](#bkmk_serverauthpublic)  
  - [Certifikát ověřování serveru vydaný z podnikové infrastruktury veřejných klíčů](#bkmk_serverauthpki)  

- [Certifikát pro ověřování klientů](#bkmk_clientauth)  
  - [Důvěryhodný kořenový certifikát klienta pro CMG](#bkmk_clientroot)  

- [Povolit bod správy pro protokol HTTPS](#bkmk_mphttps)  

- [Certifikát pro správu Azure](#bkmk_azuremgmt)  

Další informace o různých scénářích najdete v tématu [Plánování brány pro správu cloudu](plan-cloud-management-gateway.md).

## <a name="general-information"></a>Obecné informace

<!--SCCMDocs issue #779-->
Certifikáty pro bránu pro správu cloudu podporují následující konfigurace:  

- 2048-bitová nebo 4096 délka klíče

- Zprostředkovatelé úložiště klíčů pro privátní klíče certifikátu Další informace najdete v tématu [Přehled certifikátů CNG](../../../plan-design/network/cng-certificates-overview.md).  

- Při konfiguraci systému Windows pomocí následujících zásad: **Kryptografie systému: pro šifrování, algoritmus hash a podepisování použijte algoritmy kompatibilní se standardem FIPS.**  

- **TLS 1,2**. Další informace najdete v tématu [Jak povolit TLS 1,2](../../../plan-design/security/enable-tls-1-2.md).  

## <a name="cmg-server-authentication-certificate"></a><a name="bkmk_serverauth"></a>Ověřovací certifikát serveru CMG

*Tento certifikát je vyžadován ve všech scénářích.*

Tento certifikát zadáte při vytváření CMG v konzole Configuration Manager.

CMG vytvoří službu HTTPS, ke které se připojují internetoví klienti. Server vyžaduje k sestavení zabezpečeného kanálu certifikát ověřování serveru. Získejte certifikát pro tento účel od veřejného poskytovatele nebo ho vydejte od infrastruktury veřejných klíčů (PKI). Další informace najdete v tématu [CMG důvěryhodný kořenový certifikát pro klienty](#bkmk_cmgroot).

> [!NOTE]
> Ověřovací certifikát serveru CMG podporuje zástupné znaky. Některé certifikační autority vystavují certifikáty pomocí zástupného znaku pro název hostitele. Například, `*.contoso.com`. Některé organizace používají certifikáty se zástupnými znaky ke zjednodušení infrastruktury veřejných klíčů a snížení nákladů na údržbu.<!--491233-->  
>
> Další informace o tom, jak používat certifikát se zástupnými znaky s CMG, najdete v tématu [Nastavení CMG](setup-cloud-management-gateway.md#set-up-a-cmg).<!--SCCMDocs issue #565-->  

Tento certifikát vyžaduje globálně jedinečný název, který identifikuje službu v Azure. Než si vyžádáte certifikát, potvrďte, že název domény Azure, který chcete, je jedinečný. Například *GraniteFalls.CloudApp.NET*.

1. Přihlaste se k webu [Azure Portal](https://portal.azure.com).
1. Vyberte **všechny prostředky**a pak vyberte **Přidat**.
1. Vyhledejte **cloudovou službu**. Vyberte **Vytvořit**.
1. Do pole **název DNS** zadejte požadovanou předponu, například *GraniteFalls*. Rozhraní odráží, zda je název domény k dispozici nebo již používá jiná služba.

    > [!Important]  
    > Nevytvářejte službu na portálu, stačí pomocí tohoto procesu ověřit dostupnost názvu.

Pokud povolíte také CMG pro obsah, zkontrolujte, že název služby CMG je také jedinečný název účtu úložiště Azure. Pokud je název cloudové služby CMG jedinečný, ale název účtu úložiště není, Configuration Manager se nepovede zřídit službu v Azure. Opakujte výše uvedený proces v Azure Portal a proveďte následující změny:

- Vyhledat **účet úložiště**
- Otestujte své jméno v poli **název účtu úložiště** .

Předpona názvu DNS, například *GraniteFalls*, by měla být 3 až 24 znaků dlouhá a používejte jenom alfanumerické znaky. Nepoužívejte speciální znaky, například pomlčku (`-`).<!-- SCCMDocs#1080 -->

### <a name="cmg-trusted-root-certificate-to-clients"></a><a name="bkmk_cmgroot"></a>CMG důvěryhodný kořenový certifikát pro klienty

Klienti musí důvěřovat ověřovacímu certifikátu serveru CMG. Existují dvě metody, jak tento vztah důvěryhodnosti provést:

- Použijte certifikát od poskytovatele veřejného a globálně důvěryhodného certifikátu. Například mimo jiné, DigiCert, Thawte nebo VeriSign. Mezi tyto poskytovatele patří mezi klienty Windows důvěryhodné kořenové certifikační autority (CA). Když použijete certifikát pro ověření serveru vydaný jedním z těchto poskytovatelů, vaši klienti ho automaticky důvěřují.  

- Použijte certifikát vydaný certifikační autoritou organizace ze své infrastruktury veřejných klíčů (PKI). Většina podnikových implementací infrastruktury veřejných klíčů přidávají klientům Windows důvěryhodné kořenové certifikační autority. Například používání služby Active Directory Certificate Services se zásadami skupiny. Pokud vydáte ověřovací certifikát serveru CMG z certifikační autority, které nedůvěřují vašim klientům, přidejte důvěryhodný kořenový certifikát certifikační autority do internetových klientů.  

  - K zřizování certifikátů na klientech můžete také použít Configuration Manager profily certifikátů. Další informace najdete v tématu [Úvod do profilů certifikátů](../../../../protect/deploy-use/introduction-to-certificate-profiles.md).

  - Pokud plánujete [instalaci klienta Configuration Manager z Intune](../../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client), můžete k zřizování certifikátů na klientech použít taky profily certifikátů Intune. Další informace najdete v tématu [Konfigurace profilu certifikátu](https://docs.microsoft.com/intune/certificates-configure).

### <a name="server-authentication-certificate-issued-by-public-provider"></a><a name="bkmk_serverauthpublic"></a>Certifikát ověřování serveru vydaný veřejným poskytovatelem

Poskytovatel certifikátů třetích stran nemůže vytvořit certifikát pro CloudApp.net, protože tuto doménu vlastní Microsoft. Můžete získat pouze certifikát vydaný pro doménu, kterou vlastníte. Hlavním důvodem pro získání certifikátu od poskytovatele třetí strany je to, že vaši klienti již důvěřují kořenovému certifikátu tohoto poskytovatele.

K vytvoření aliasu DNS použijte následující postup:

1. Vytvořte záznam kanonického názvu (CNAME) ve veřejném DNS vaší organizace. Tento záznam vytvoří alias pro CMG s popisným názvem, který používáte ve veřejném certifikátu.

    Například contoso pojmenuje své CMG **GraniteFalls**. Tento název se v Azure bude **GraniteFalls.CloudApp.NET** . Ve veřejném oboru názvů DNS contoso.com společnosti Contoso vytvoří Správce DNS nový záznam CNAME pro **GraniteFalls.contoso.com** pro skutečný název hostitele **GraniteFalls.CloudApp.NET**.  

2. Vyžádejte certifikát ověřování serveru od veřejného poskytovatele pomocí obecného názvu (CN) aliasu CNAME.
Například contoso používá **GraniteFalls.contoso.com** pro CN certifikátu.  

3. Vytvořte CMG pomocí tohoto certifikátu v konzole Configuration Manager. Na stránce **Nastavení** v Průvodci vytvořením brána pro správu cloudu:  

    - Když přidáte certifikát serveru pro tuto cloudovou službu (ze **souboru certifikátu**), průvodce extrahuje název hostitele z CN certifikátu jako název služby.  

    - Pak tento název hostitele připojí k **cloudapp.NET**nebo **usgovcloudapp.NET** pro státní správu Azure USA, jako plně kvalifikovaný název domény služby pro vytvoření služby v Azure.  

    - Například když contoso vytvoří CMG, Configuration Manager extrahuje název hostitele **GraniteFalls** z CN certifikátu. Azure vytvoří skutečnou službu jako **GraniteFalls.CloudApp.NET**.  

Při vytváření instance CMG v Configuration Manager, zatímco certifikát má GraniteFalls.Contoso.com, Configuration Manager extrahuje pouze název hostitele, například: GraniteFalls. Připojí tento název hostitele k CloudApp.net, které Azure vyžaduje při vytváření cloudové služby. Alias CNAME v oboru názvů DNS pro vaši doménu (Contoso.com) mapuje tyto dva plně kvalifikované názvy domény společně. Configuration Manager poskytuje klientům zásadu pro přístup k tomuto CMG, mapování DNS se tak spojí, aby mohl bezpečně přistupovat ke službě v Azure.<!--SCCMDocs issue #565-->  

### <a name="server-authentication-certificate-issued-from-enterprise-pki"></a><a name="bkmk_serverauthpki"></a>Certifikát ověřování serveru vydaný z podnikové infrastruktury veřejných klíčů

Vytvořte si vlastní certifikát SSL pro CMG stejně jako u cloudového distribučního bodu. Postupujte podle pokynů pro [Nasazení certifikátu služby pro cloudové distribuční body](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012) , ale proveďte následující akce:

- Při vyžádání vlastního certifikátu webového serveru zadejte plně kvalifikovaný název domény pro běžný název certifikátu. Může to být název veřejné domény, který vlastníte, nebo můžete použít doménu cloudapp.net. Pokud používáte vlastní veřejnou doménu, přečtěte si výše uvedený postup a vytvořte alias DNS ve veřejném DNS vaší organizace.  

- Při použití veřejné domény cloudapp.net pro certifikát webového serveru CMG:  

  - Ve veřejném cloudu Azure použijte název, který končí na **cloudapp.NET** .  

  - Použijte název, který končí v **usgovcloudapp.NET** pro státní správu Azure USA.  

## <a name="client-authentication-certificate"></a><a name="bkmk_clientauth"></a>Certifikát pro ověřování klientů

*Tento certifikát je vyžadován pro internetové klienty se systémem Windows 8.1 a zařízení s Windows 10 nepřipojená k Azure Active Directory (Azure AD). Je také vyžadováno v bodu připojení CMG. Nevyžaduje se pro klienty Windows 10 připojené ke službě Azure AD.*

Klienti používají tento certifikát k ověřování pomocí CMG. Zařízení s Windows 10, která jsou hybridní nebo cloudová doména, tento certifikát nevyžadují, protože k ověřování používají službu Azure AD.

Tento certifikát zřiďte mimo kontext Configuration Manager. K vystavování certifikátů ověřování klientů můžete například použít službu AD CS (Active Directory Certificate Services) a zásady skupiny. Další informace najdete v tématu [nasazení klientského certifikátu pro počítače se systémem Windows](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).

Pro bezpečné přeposílání požadavků klienta vyžaduje spojovací bod CMG certifikát ověřování klienta, který odpovídá ověřovacímu certifikátu serveru v bodu správy HTTPS. Pokud klienti používají ověřování Azure AD nebo nakonfigurujete bod správy pro rozšířený protokol HTTP, tento certifikát se nevyžaduje. Další informace najdete v tématu [Povolení bodu správy pro protokol HTTPS](#bkmk_mphttps).

> [!NOTE]
> Microsoft doporučuje připojit zařízení k Azure AD. Internetová zařízení můžou pomocí Azure AD ověřit pomocí Configuration Manager. Také umožňuje scénářům zařízení i uživatele, zda je zařízení na internetu nebo připojeno k interní síti. Další informace najdete v tématu [instalace a registrace klienta pomocí Azure AD identity](../../deploy/deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).
>
> Počínaje verzí 2002,<!--5686290--> Configuration Manager rozšiřuje podporu internetových zařízení, která se často nepřipojují k interní síti, nelze se připojit k Azure Active Directory (Azure AD) a nemusíte mít k dispozici metodu pro instalaci certifikátu vystaveného infrastrukturou veřejných klíčů. Další informace najdete v tématu [ověřování založené na tokenech pro CMG](../../deploy/deploy-clients-cmg-token.md).

### <a name="client-trusted-root-certificate-to-cmg"></a><a name="bkmk_clientroot"></a>Důvěryhodný kořenový certifikát klienta pro CMG

*Tento certifikát je vyžadován při použití certifikátů ověřování klienta. Když všichni klienti používají Azure AD k ověřování, tento certifikát se nevyžaduje.*

Tento certifikát zadáte při vytváření CMG v konzole Configuration Manager.

CMG musí důvěřovat certifikátům pro ověřování klientů. Chcete-li dosáhnout tohoto vztahu důvěryhodnosti, zadejte důvěryhodný kořenový řetěz certifikátů. Nezapomeňte přidat všechny certifikáty v řetězu důvěryhodnosti. Pokud je třeba certifikát pro ověřování klientů vydaný zprostředkující certifikační autoritou, přidejte jak certifikáty zprostředkující, tak i kořenových certifikačních autorit.

> [!Note]  
> Při vytváření CMG už nebudete muset poskytovat důvěryhodný kořenový certifikát na stránce nastavení. Tento certifikát se nevyžaduje při použití Azure Active Directory (Azure AD) pro ověřování klientů, ale používá se v průvodci. Pokud používáte certifikáty pro ověřování klientů PKI, musíte do CMG Přidat důvěryhodný kořenový certifikát.<!--SCCMDocs-pr issue #2872 SCCMDocs issue #1319-->
>
> Ve verzi 1902 a starší můžete přidat pouze dva důvěryhodné kořenové certifikační autority a čtyři zprostředkující (podřízené) certifikační autority.

#### <a name="export-the-client-certificates-trusted-root"></a>Exportovat důvěryhodný kořenový certifikát klientského certifikátu

Po vydání ověřovacího certifikátu klienta k počítači pomocí tohoto postupu exportujte důvěryhodný kořenový adresář.

1. Otevřete nabídku Start. Zadáním příkazu Run (spustit) otevřete okno spuštění. Otevřete `mmc`.  

2. V nabídce soubor klikněte na příkaz **Přidat nebo odebrat modul snap-in...**.  

3. V dialogovém okně Přidat nebo odebrat moduly snap-in vyberte **certifikáty**a pak vyberte **Přidat**.  

    1. V dialogovém okně modul snap-in certifikáty vyberte možnost **účet počítače**a pak vyberte možnost **Další**.  

    1. V dialogovém okně Vybrat počítač vyberte možnost **místní počítač**a pak vyberte **Dokončit**.  

    1. V dialogovém okně Přidat nebo odebrat moduly snap-in vyberte **OK**.  

4. Rozbalte položku **certifikáty**, rozbalte položku **osobní**a vyberte položku **certifikáty**.  

5. Vyberte certifikát, jehož cílem je **ověření klienta**.  

    1. V nabídce Akce vyberte **otevřít**.  

    1. Přejít na kartu **cesta k certifikátu** .  

    1. Vyberte další certifikát v rámci řetězce a vyberte **Zobrazit certifikát**.  

6. V tomto dialogovém okně Nový certifikát přejdete na kartu **Podrobnosti** . Vyberte **Kopírovat do souboru...**.  

7. Dokončete Průvodce exportem certifikátu s použitím výchozího formátu certifikátu a **binární soubor kódování der X. 509 (. CER)**. Poznamenejte si název a umístění exportovaného certifikátu.  

8. Exportujte všechny certifikáty v cestě k certifikátu původního certifikátu ověřování klienta. Poznamenejte si, které exportované certifikáty jsou zprostředkující certifikační autority a které jsou důvěryhodné kořenové certifikační autority.  

## <a name="enable-management-point-for-https"></a><a name="bkmk_mphttps"></a>Povolit bod správy pro protokol HTTPS

Tento certifikát zřiďte mimo kontext Configuration Manager. K vydání certifikátu webového serveru můžete například použít službu AD CS (Active Directory Certificate Services) a zásady skupiny. Další informace najdete v tématu [požadavky na certifikát PKI](../../../plan-design/network/pki-certificate-requirements.md) a [Nasazení certifikátu webového serveru pro systémy lokality, které spouští službu IIS](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).

Při použití možnosti web k **použití Configuration Manager generovaných certifikátů pro systémy lokality http**může být bod správy http. Další informace najdete v tématu [Rozšířená http](../../../plan-design/hierarchy/enhanced-http.md).

> [!Tip]  
> Pokud nepoužíváte rozšířené požadavky HTTP a vaše prostředí má více bodů správy, nemusíte je povolit pro CMG. Nakonfigurujte body správy s povoleným CMG jako **pouze Internet**. Místní klienti je pak nezkusí použít.<!-- SCCMDocs#1676 -->

### <a name="enhanced-http-certificate-for-management-points"></a>Rozšířený certifikát HTTP pro body správy

Pokud povolíte rozšířené protokolu HTTP, server lokality vygeneruje certifikát podepsaný svým držitelem s názvem **certifikát SSL role SMS**vydaný kořenovým certifikátem vydávající služby SMS. Bod správy přidá tento certifikát do výchozího webu služby IIS vázaného na port 443.

### <a name="management-point-client-connection-mode-summary"></a>Souhrn režimu připojení klienta bodu správy

Tyto tabulky shrnují, jestli bod správy vyžaduje protokol HTTP nebo HTTPS, v závislosti na typu klienta a verze lokality.

#### <a name="for-internet-based-clients-communicating-with-the-cloud-management-gateway"></a>Pro internetové klienty komunikující s bránou pro správu cloudu

Nakonfigurujte místní bod správy, aby povoloval připojení z CMG s následujícím režimem připojení klienta:

| Typ klienta   | Bod správy |
|------------------|------------------|
| Pracovní skupina        | E-HTTP<sup>[Poznámka 1](#bkmk_note1)</sup>, https |
| Připojeno k doméně AD | E-HTTP<sup>[Poznámka 1](#bkmk_note1)</sup>, https |
| Připojeno k Azure AD  | E-HTTP, HTTPS |
| Hybrid – připojeno    | E-HTTP, HTTPS |

<a name="bkmk_note1"></a>

> [!Note]  
> **Poznámka 1**: Tato konfigurace vyžaduje, aby klient měl [certifikát pro ověřování klientů](#bkmk_clientauth), a podporuje jenom scénáře zaměřené na zařízení.  

#### <a name="for-on-premises-clients-communicating-with-the-on-premises-management-point"></a>U místních klientů, kteří komunikují s místním bodem správy

Nakonfigurujte místní bod správy pomocí následujícího režimu připojení klienta:

| Typ klienta   | Bod správy |
|------------------|------------------|
| Pracovní skupina        | HTTP, HTTPS |
| Připojeno k doméně AD | HTTP, HTTPS |
| Připojeno k Azure AD  | HTTPS       |
| Hybrid – připojeno    | HTTP, HTTPS |

> [!NOTE]  
> Klienti připojení k doméně služby AD podporují scénáře zaměřené na zařízení i uživatele na komunikaci s bodem správy HTTP nebo HTTPS.  
>
> Klienti připojení k Azure AD a hybridní připojení můžou komunikovat přes protokol HTTP pro scénáře zaměřené na zařízení, ale potřebují E-HTTP nebo HTTPS, aby mohli scénáře zaměřené na uživatele. V opačném případě se chovají stejně jako klienti pracovní skupiny.  

#### <a name="legend-of-terms"></a>Legenda podmínek

- *Pracovní skupina*: zařízení není připojené k doméně nebo službě Azure AD, ale má [certifikát pro ověřování klientů](#bkmk_clientauth) .  
- *Připojeno k doméně služby*Active Directory: připojení zařízení k místní doméně služby Active Directory  
- *Služba Azure AD – připojeno*: taky se označuje jako cloudová doména připojená, připojíte zařízení k tenantovi Azure Active Directory.  
- *Hybridní*připojení: Připojte zařízení k doméně služby Active Directory i k Tenantovi služby Azure AD.  
- *Http*: ve vlastnostech bodu správy nastavíte připojení klienta na **http** .  
- *Https*: ve vlastnostech bodu správy nastavíte připojení klienta k **https** .  
- *E-http*: na kartě Vlastnosti lokality, **komunikace s klientským počítačem** nastavíte nastavení systému lokality na **https nebo http**a povolíte možnost **používat Configuration Manager certifikáty generované pro systémy lokality http**. Nakonfigurujete bod správy pro protokol HTTP, bod správy protokolu HTTP je připravený pro komunikaci HTTP i HTTPS (scénáře ověřování tokenů).  
    > [!Note]
    > Počínaje verzí 1906 se tato karta nazývá **zabezpečení komunikace**.<!-- SCCMDocs#1645 -->  

## <a name="azure-management-certificate"></a><a name="bkmk_azuremgmt"></a>Certifikát pro správu Azure

*Tento certifikát je nutný pro nasazení v klasickém provozu. Pro Azure Resource Manager nasazení se nevyžaduje.*

> [!Important]  
> Od verze 1810 jsou nasazení klasických služeb v Azure v Configuration Manager zastaralá. Začněte používat nasazení Azure Resource Manager pro bránu pro správu cloudu. Další informace najdete v tématu [plánování pro CMG](plan-cloud-management-gateway.md#azure-resource-manager).
>
> Počínaje verzí 1902 Configuration Manager Azure Resource Manager je jediným mechanismem nasazení pro nové instance brány pro správu cloudu. Tento certifikát se nevyžaduje v Configuration Manager verze 1902 nebo novější.<!-- 3605704 -->

Tento certifikát zadáte do Azure Portal a při vytváření CMG v konzole Configuration Manager.

Pokud chcete vytvořit CMG v Azure, musí se bod připojení služby Configuration Manager nejdřív ověřit u vašeho předplatného Azure. Při použití klasického nasazení služby používá certifikát pro správu Azure pro toto ověřování. Správce Azure tento certifikát nahraje do vašeho předplatného. Po vytvoření CMG v konzole Configuration Manager zadejte tento certifikát.

Další informace a pokyny, jak nahrát certifikát pro správu, najdete v následujících článcích v dokumentaci k Azure:

- [Cloud Services a certifikáty pro správu](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)  

- [Nahrajte certifikát pro správu služeb Azure.](https://docs.microsoft.com/azure/azure-api-management-certs)  

> [!IMPORTANT]
> Nezapomeňte zkopírovat ID předplatného přidruženého k certifikátu pro správu. Použijete ho k vytvoření CMG v konzole Configuration Manager.

## <a name="next-steps"></a>Další kroky

- [Instalace brány pro správu cloudu](setup-cloud-management-gateway.md)  

- [Nejčastější dotazy týkající se brány pro správu cloudu](cloud-management-gateway-faq.md)  

- [Zabezpečení a ochrana brány pro správu cloudu](security-and-privacy-for-cloud-management-gateway.md)  
