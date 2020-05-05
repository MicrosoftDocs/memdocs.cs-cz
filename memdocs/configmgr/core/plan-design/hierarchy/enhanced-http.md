---
title: Vylepšený protokol HTTP
titleSuffix: Configuration Manager
description: Pomocí moderního ověřování Zabezpečte komunikaci s klienty bez nutnosti certifikátů PKI.
ms.date: 03/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4deac022-e397-4f1f-bc0a-cea6c6c6368d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bb14830e99600da1b71c516a44d51a0090cdc673
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720174"
---
# <a name="enhanced-http"></a>Vylepšený protokol HTTP

*Platí pro: Configuration Manager (Current Branch)*

<!--1356889,1358460-->

> [!Tip]  
> Tato funkce byla poprvé představena ve verzi 1806 jako [funkce předběžné verze](../../servers/manage/pre-release-features.md). Počínaje verzí 1810 Tato funkce už není součástí předběžné verze.  

Microsoft doporučuje používat komunikaci přes protokol HTTPS pro všechny Configuration Manager komunikačních cest, ale u některých zákazníků je nenáročné, protože se řídí nároky na správu certifikátů PKI.

Configuration Manager verze 1806 obsahuje vylepšení způsobu, jakým klienti komunikují se systémy lokality. Existují dva primární cíle těchto vylepšení:  

- Můžete zabezpečit citlivou komunikaci klienta bez nutnosti ověřování certifikátů serverů PKI.  

- Klienti mohou bezpečně přistupovat k obsahu z distribučních bodů bez nutnosti použít účet přístupu k síti, klientský certifikát PKI a ověřování systému Windows.  

Veškerá ostatní komunikace klienta je přes protokol HTTP. Rozšířený protokol HTTP není stejný jako povolování protokolu HTTPS pro komunikaci klientů nebo systém lokality.<!-- SCCMDocs issue #1212 -->

> [!Note]  
> Certifikáty PKI jsou stále platnou možností pro zákazníky s následujícími požadavky:  
>
> - Veškerá komunikace klienta je přes protokol HTTPS.  
> - Rozšířené řízení podpisové infrastruktury
>
> I když už používáte PKI, použije se certifikát PKI vázaný ve službě IIS i v případě, že je zapnutý rozšířený protokol HTTP.



## <a name="scenarios"></a><a name="bkmk_scenario"></a>Řešení

Následující scénáře mají výhodu z těchto vylepšení:  

### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_scenario1"></a>Scénář 1: klient do bodu správy

<!--1356889-->
[Zařízení připojená k Azure Active Directory (Azure AD)](/azure/active-directory/devices/concept-azure-ad-join) můžou komunikovat s bodem správy nakonfigurovaným pro protokol HTTP. Webový server vygeneruje certifikát pro bod správy, který umožňuje komunikaci přes zabezpečený kanál.

> [!Note]  
> Toto chování se mění z Configuration Manager aktuální větve verze 1802, která vyžaduje bod správy s povoleným protokolem HTTPS pro klienty připojené k Azure AD, kteří komunikují přes bránu pro správu cloudu. Další informace najdete v tématu [Povolení bodu správy pro protokol HTTPS](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_scenario2"></a>Scénář 2: klient s distribučním bodem

<!--1358228-->
Pracovní skupina nebo klient připojený k Azure AD může ověřit a stáhnout obsah přes zabezpečený kanál z distribučního bodu nakonfigurovaného pro protokol HTTP. Tyto typy zařízení také mohou ověřovat a stahovat obsah z distribučního bodu nakonfigurovaného pro protokol HTTPS bez vyžadování certifikátu PKI v klientovi. Přidání certifikátu pro ověřování klientů do pracovní skupiny nebo klienta připojeného k Azure AD je náročné.

Toto chování zahrnuje scénáře nasazení operačního systému s pořadím úkolů spuštěným ze spouštěcího média, PXE nebo centra softwaru. Další informace najdete v tématu [účet pro přístup k síti](accounts.md#network-access-account).<!--1358278-->

### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_scenario3"></a>Scénář 3: identita zařízení Azure AD

<!--1358460-->
Zařízení Azure AD, které je připojené k Azure AD nebo [hybridní](/azure/active-directory/devices/concept-azure-ad-join-hybrid) , bez přihlášení uživatele Azure AD, může bezpečně komunikovat s přiřazenou lokalitou. Cloudová identita zařízení je nyní dostačující pro ověřování s CMG a bodem správy pro scénáře zaměřené na zařízení. (Pro scénáře zaměřené na uživatele se stále vyžaduje token uživatele.)  


## <a name="features"></a>Funkce

Následující funkce Configuration Manager podporují nebo vyžadují rozšířené HTTP:

- [Brána pro správu cloudu](../../clients/manage/cmg/plan-cloud-management-gateway.md)
- [Nasazení operačního systému bez účtu přístupu k síti](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#enhanced-http)
- [Povolit spolusprávu pro nová zařízení s Windows 10 na internetu](../../../comanage/tutorial-co-manage-new-devices.md)
- [Schválení aplikací prostřednictvím e-mailu](../../../apps/deploy-use/app-approval.md#bkmk_email-approve)
- [Služba správy](../../../develop/adminservice/overview.md)
- [Zobrazit nedávno připojené konzoly](../../servers/manage/admin-console.md#bkmk_viewconnected)

> [!Note]  
> Bod aktualizace softwaru a související scénáře vždy podporují zabezpečený provoz HTTP s klienty i bránou pro správu cloudu. Používá mechanismus s bodem správy, který se liší od ověřování založeného na certifikátech nebo na základě tokenů.<!-- SCCMDocs issue #1148 -->


## <a name="prerequisites"></a>Požadavky  

- Bod správy nakonfigurovaný pro připojení klienta pomocí protokolu HTTP. Tuto možnost nastavte na kartě **Obecné** ve vlastnostech role bodu správy.  

- Distribuční bod konfigurovaný pro připojení klienta pomocí protokolu HTTP. Tuto možnost nastavte na kartě **komunikace** vlastností role distribučního bodu. Nepovolujte možnost **Povolit anonymní připojení klientů**.  

- Připojte lokalitu k Azure AD pro správu cloudu.  

    - Pokud jste už tento požadavek splnili pro vaši lokalitu, musíte aktualizovat aplikaci Azure AD. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte možnost **Azure Active Directory klienti**. Vyberte tenanta Azure AD, vyberte webovou aplikaci v podokně **aplikace** a pak na pásu karet vyberte **aktualizovat nastavení aplikace** .  

- *Jenom pro [scénáře 3](#bkmk_scenario3) *: klient se systémem Windows 10 verze 1803 nebo novější a připojený k Azure AD. Klient vyžaduje tuto konfiguraci pro ověřování zařízení Azure AD.<!-- SCCMDocs issue 1126 -->


## <a name="configure-the-site"></a>Konfigurace lokality

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** . Vyberte lokalitu a na pásu karet zvolte **vlastnosti** .  

2. Přepněte na kartu **komunikace s klientským počítačem** .

    > [!Note]
    > Počínaje verzí 1906 se tato karta nazývá **zabezpečení komunikace**.<!-- SCCMDocs#1645 -->  

    Vyberte možnost **protokolu HTTPS nebo http**. Pak povolte možnost **použití Configuration Manager generovaných certifikátů pro systémy lokality http**.

> [!Tip]
> Počkejte až 30 minut, než bod správy přijme a nakonfiguruje nový certifikát z lokality.

<!--3798957-->
Počínaje verzí 1902 můžete také povolit rozšířený protokol HTTP pro lokalitu centrální správy. Použijte stejný postup a otevřete vlastnosti centrální lokality pro správu. Tato akce aktivuje pouze rozšířený protokol HTTP pro role poskytovatele služby SMS v lokalitě centrální správy. Nejedná se o globální nastavení, které platí pro všechny lokality v hierarchii.

Tyto certifikáty můžete zobrazit v konzole Configuration Manager. Otevřete pracovní prostor **Správa** , rozbalte položku **zabezpečení**a vyberte uzel **certifikáty** . Vyhledejte kořenový certifikát **vydávající zprávu SMS** a certifikáty rolí serveru lokality vydané kořenem vydávající zprávy SMS.

Další informace o tom, jak klient komunikuje s bodem správy a distribučním bodem s touto konfigurací, najdete v tématu [komunikace mezi klienty a systémy lokality a služby](communications-between-endpoints.md#Planning_Client_to_Site_System).


## <a name="see-also"></a>Viz také

- [Plánování zabezpečení](../security/plan-for-security.md)  

- [Zabezpečení a ochrana osobních údajů pro klienty Configuration Manager](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Konfigurace zabezpečení](../security/configure-security.md)  

- [Komunikace mezi koncovými body](communications-between-endpoints.md)  
