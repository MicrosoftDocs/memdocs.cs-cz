---
title: Plánování správy aplikací
titleSuffix: Configuration Manager
description: Implementujte a nakonfigurujte nezbytné závislosti pro nasazení aplikací v Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 03fda62774b930a1cc3603415f3b872050b9cb71
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709940"
---
# <a name="plan-for-and-configure-application-management-in-configuration-manager"></a>Plánování a konfigurace správy aplikací v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Informace v tomto článku vám pomůžou při implementaci nezbytných závislostí pro nasazení aplikací v Configuration Manager.  



## <a name="dependencies-external-to-configuration-manager"></a>Vnější závislosti nástroje Configuration Manager  


### <a name="internet-information-services-iis"></a>Internet Information Services (IIS)

Služba IIS je nutná na serverech, na kterých běží následující role systému lokality:

- Bod správy  
- Distribuční bod  

Další informace najdete v tématu [Požadované součásti lokality a systému lokality](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

> [!Note]  
> Katalog aplikací vyžaduje také službu IIS. Nicméně uživatelské prostředí Silverlight není podporované v aktuální větvi verze 1806. Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací. Podpora končí pro role katalogu aplikací s verzí 1910.  
>
> Další informace najdete v těchto článcích:
>
> - [Konfigurace centra softwaru](plan-for-software-center.md#bkmk_userex)
> - [Odebrané a zastaralé funkce](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  


### <a name="certificates-on-code-signed-applications-for-mobile-devices"></a>Certifikáty pro aplikace podepsané kódem pro mobilní zařízení

Když aplikace přihlásíte pomocí kódu k jejich nasazení do mobilních zařízení, nepoužívejte certifikát, který byl vygenerován pomocí šablony verze 3 (**Windows Server 2008, Enterprise Edition**). Tato šablona certifikátu vytvoří certifikát, který není kompatibilní s Configuration Manager aplikacemi pro mobilní zařízení.

Pokud používáte službu AD CS (Active Directory Certificate Services) k podepisování kódu aplikací pro aplikace mobilních zařízení, nepoužívejte šablonu certifikátu verze 3.


### <a name="audit-sign-in-events-for-user-device-affinity"></a>Auditovat události přihlášení pro spřažení uživatelských zařízení  

Chcete-li automaticky vytvářet spřažení uživatelských zařízení, nakonfigurujte klienty na Auditovat události přihlášení.

Aby bylo možné určit automatické spřažení uživatelských zařízení, klient Configuration Manager čte události přihlášení typu **úspěch** z protokolu událostí zabezpečení systému Windows. Povolte tyto události s následujícími dvěma zásadami auditu:

- **Kontrola událostí přihlášení k účtu**
- **Kontrola událostí přihlášení**

Chcete-li automaticky vytvářet vztahy mezi uživateli a zařízeními, ujistěte se, že tato dvě nastavení jsou na klientských počítačích povolena. K nakonfigurování těchto nastavení můžete použít zásady skupiny systému Windows.

Další informace o spřažení uživatelských zařízení najdete v tématu [propojení uživatelů a zařízení pomocí spřažení uživatelských zařízení](../deploy-use/link-users-and-devices-with-user-device-affinity.md).  



## <a name="configuration-manager-dependencies"></a>Závislosti nástroje Configuration Manager


### <a name="management-point"></a>Bod správy

Klienti kontaktují bod správy, aby stáhli zásady klienta, a našli tak obsah.

Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele.

Ve verzi 1902 a starší používají klienti k připojení ke katalogu aplikací bod správy. Pokud klienti nemají přístup k bodu správy, nemohou používat Katalog aplikací.

> [!Note]  
> Od verze 1806 se už Role katalogu aplikací nevyžadují k zobrazení aplikací dostupných uživatelům v centru softwaru. Další informace najdete v tématu [Konfigurace centra softwaru](plan-for-software-center.md#bkmk_userex).<!--1358309-->  
>
> Počínaje verzí 1906 nemůžete instalovat nové role katalogu aplikací. Podpora končí pro role katalogu aplikací s verzí 1910.  
  

### <a name="distribution-point"></a>Distribuční bod

Předtím, než budete moci nasadit aplikace do klientů, potřebujete alespoň jeden distribuční bod v hierarchii. Ve výchozím nastavení má server lokality během standardní instalace povolenou roli lokality distribučního bodu. Počet a umístění distribučních bodů se liší podle konkrétních požadavků vašeho prostředí.

Další informace o instalaci distribučních bodů a správě obsahu najdete v tématu [Správa obsahu a infrastruktury obsahu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


### <a name="reporting-services-point"></a>Bod služby Reporting services

Chcete-li použít sestavy v Configuration Manager pro správu aplikací, nejprve nainstalujte a nakonfigurujte bod služby Reporting Services.

Další informace najdete v tématu [Úvod do vytváření sestav](../../core/servers/manage/introduction-to-reporting.md).  


### <a name="client-settings"></a>Nastavení klienta

Řada nastavení klienta Určuje, jak klient instaluje aplikace a prostředí uživatele na zařízení. Tato nastavení klienta zahrnují následující skupiny:

- Počítačový agent  
- Restartování počítače  
- Centrum softwaru  
- Nasazení softwaru  
- Spřažení uživatelů a zařízení  

Další informace najdete v těchto článcích:

- [O nastavení klientů](../../core/clients/deploy/about-client-settings.md)  
- [Postup konfigurace nastavení klienta](../../core/clients/deploy/configure-client-settings.md)  


### <a name="security-permissions-for-application-management"></a>Bezpečnostní oprávnění pro správu aplikací

- Role zabezpečení **vytváření aplikací** zahrnuje požadovaná oprávnění k vytváření, změnám a vyřazení aplikací.  

- Role zabezpečení **Správce nasazení aplikací** zahrnuje požadovaná oprávnění pro nasazení aplikací.  

- Role zabezpečení **Správce aplikací** má všechna oprávnění od **autora aplikace** i z **Správce nasazení aplikací** rolí zabezpečení.  

Další informace najdete v tématu [Konfigurace správy na základě rolí](../../core/servers/deploy/configure/configure-role-based-administration.md).  


### <a name="app-v-46-sp1-or-later-client-to-run-virtual-applications"></a>App-V 4.6 SP1 nebo novější klient pro spouštění virtuálních aplikací

Pokud chcete vytvořit virtuální aplikace v Configuration Manager, nainstalujte na zařízení aplikaci App-V 4,6 SP1 nebo novější.

Než nasadíte virtuální aplikace, aktualizujte také klienta sady App-V s opravou hotfix popsanou v [Podpora Microsoftu článku 2645225](https://support.microsoft.com/help/2645225).  


### <a name="application-catalog"></a>Katalog aplikací

> [!Important]  
> Podpora končí pro role katalogu aplikací s verzí 1910.. Další informace najdete v tématu [Odebrání katalogu aplikací](#bkmk_remove-appcat).  

#### <a name="application-catalog-web-service-point"></a>Bod webové služby Katalog aplikací

Bod webové služby Katalog aplikací je role systému lokality, která poskytuje informace o dostupném softwaru z knihovny softwaru na web katalogu aplikací, ke kterému mají uživatelé přístup.

Další informace o tom, jak tuto roli systému lokality nakonfigurovat, najdete v tématu [instalace a konfigurace katalogu aplikací](#bkmk_appcat).  

#### <a name="application-catalog-website-point"></a>Bod webu Katalog aplikací

Bod webu Katalog aplikací je role systému lokality, která uživatelům poskytuje seznam dostupného softwaru.

Další informace o tom, jak tuto roli systému lokality nakonfigurovat, najdete v tématu [instalace a konfigurace katalogu aplikací](#bkmk_appcat).

#### <a name="discovered-user-accounts-for-application-catalog"></a>Zjištěné uživatelské účty pro katalog aplikací

Aby uživatelé mohli zobrazit a požadovat aplikace z katalogu aplikací, Configuration Manager musí nejdřív zjistit uživatelské účty. Další informace najdete v tématu [spuštění zjišťování](../../core/servers/deploy/configure/run-discovery.md).  



## <a name="configure-software-center"></a><a name="bkmk_userex"></a>Konfigurace centra softwaru  

Další informace o konfiguraci a brandingu centra softwaru najdete v tématu [plánování centra softwaru](plan-for-software-center.md).


## <a name="remove-the-application-catalog"></a><a name="bkmk_remove-appcat"></a>Odebrání katalogu aplikací

<!-- SCCMDocs-pr issue 3051 -->

Podpora končí pro role katalogu aplikací s verzí 1910. Další informace najdete v tématu [odebrané a zastaralé funkce](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). Následující seznam shrnuje změny:

- Počínaje verzí 1806 se **uživatelské prostředí Silverlight** pro bod webu Katalog aplikací už nepodporuje.<!--1358309--> Role bodu webové služby katalogu aplikací se už *nepožaduje*, ale pořád se *podporuje*.

- Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací.

- Podpora končí pro role katalogu aplikací s verzí 1910.  

Tato iterativní vylepšení centra softwaru a bodu správy jsou zjednodušení vaší infrastruktury a odstraňují nutnost katalogu aplikací pro nasazení, která jsou k dispozici pro uživatele. Centrum softwaru může doručovat všechna nasazení aplikací bez katalogu aplikací. Pokud povolíte TLS 1,2 a použijete protokol HTTP s katalogem aplikací, uživatelé nebudou moci zobrazit dostupná nasazení cílená pro uživatele. Abyste z těchto vylepšení využili výhody, aktualizujte Configuration Manager na verzi 1906 nebo novější.

1. Aktualizujte všechny klienty na verzi 1806 nebo novější. Doporučuje se verze 1906.  

1. Místo ve vlastnostech role webu Katalog aplikací nastavte branding pro Centrum softwaru. Další informace najdete v tématu [nastavení klienta centra softwaru](../../core/clients/deploy/about-client-settings.md#software-center).  

1. Zkontrolujte výchozí a všechna vlastní nastavení klienta. Ve skupině **Počítačový agent** ověřte, zda je `(none)` **výchozí bod webu Katalog aplikací** .  

    Ve verzi 1902 a starší se klient přepne jenom na použití bodu správy, pokud v hierarchii neexistují žádné role katalogu aplikací. V opačném případě budou klienti dál používat jednu z instancí katalogu aplikací v hierarchii. Toto chování platí pro různé primární lokality.  

1. Odeberte role systému lokality webu **Katalog aplikací** a **webové služby katalogu aplikací** ze všech primárních lokalit.

Po odebrání rolí katalogu aplikací se Centrum softwaru začne používat bod správy pro dostupná nasazení, která jsou cílená pro uživatele. Ve verzi 1902 a novější může trvat až 65 minut, než se tato změna stane. Chcete-li toto chování ověřit u konkrétního klienta, `SCClient_<username>.log`zkontrolujte a vyhledejte položku podobnou následujícímu řádku:

`Using endpoint Url: https://mp.contoso.com/CMUserService_WindowsAuth, Windows authentication`


## <a name="install-and-configure-the-application-catalog"></a><a name="bkmk_appcat"></a>Instalace a konfigurace katalogu aplikací  

> [!Important]  
> Podpora končí pro role katalogu aplikací s verzí 1910. Další informace najdete v tématu [Odebrání katalogu aplikací](#bkmk_remove-appcat).  

### <a name="step-1-web-server-certificate-for-https"></a>Krok 1: certifikát webového serveru pro protokol HTTPS

Pokud používáte připojení HTTPS, Nasaďte certifikát webového serveru na servery systému lokality pro bod webu Katalog aplikací a bod služeb webu Katalog aplikací.

Pokud chcete, aby klienti používali službu Application Catalog z Internetu, Nasaďte certifikát webového serveru alespoň na jeden bod správy. Nakonfigurujte pro připojení klientů z Internetu.

Další informace o požadavcích na certifikát najdete v tématu [požadavky na certifikát PKI](../../core/plan-design/network/pki-certificate-requirements.md).  


### <a name="step-2-client-authentication-certificate-for-https"></a>Krok 2: certifikát ověřování klientů pro protokol HTTPS

Pokud používáte klientský certifikát PKI pro připojení k bodům správy, nasaďte klientský ověřovací certifikát na klientské počítače. I když klienti nepoužívají klientský certifikát PKI pro připojení ke službě Application Catalog, musí se připojit k bodu správy, aby mohli používat Katalog aplikací.

Do klientských počítačů Nasaďte certifikát pro ověřování klientů v následujících scénářích:

- Všechny body správy v intranetu akceptují pouze připojení klientů pomocí protokolu HTTPS.
- Klienti se připojují ke službě Application Catalog z Internetu.

Další informace o požadavcích na certifikát najdete v tématu [požadavky na certifikát PKI](../../core/plan-design/network/pki-certificate-requirements.md).  


### <a name="step-3-install-and-configure-the-application-catalog-roles"></a>Krok 3: instalace a konfigurace rolí katalogu aplikací

Nainstalujte bod služeb webu Katalog aplikací a role webu Katalog aplikací ve stejné lokalitě. Nemusíte je instalovat na stejný server nebo do stejné doménové struktury služby Active Directory. Bod služeb webu Katalog aplikací musí být ale ve stejné doménové struktuře jako databáze lokality.

Další informace o umístění serveru najdete v tématu [plánování systémových serverů lokality a rolí systému lokality](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

> [!NOTE]  
> Nainstalujte katalog aplikací v primární lokalitě. Nemůžete ho nainstalovat do sekundární lokality nebo lokality centrální správy.  

Nainstalujte katalog aplikací na nový server systému lokality nebo na existující server v lokalitě. Další informace o obecném postupu najdete v tématu [Instalace rolí systému lokality](../../core/servers/deploy/configure/install-site-system-roles.md). V průvodci přidejte roli systému lokality nebo vytvořte server systému lokality, v seznamu vyberte následující role:  

- **Bod webové služby Katalog aplikací**  
- **Bod webu Katalog aplikací**  

> [!TIP]  
> Pokud chcete, aby klientské počítače používaly katalog aplikací přes Internet, zadejte plně kvalifikovaný název domény (FQDN) pro Internet.  

#### <a name="verify-the-installation-of-these-site-system-roles"></a>Ověřte instalaci těchto rolí systému lokality.  

- Stavové zprávy: Použijte součásti **SMS_PORTALWEB_CONTROL_MANAGER** a **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Například ID stavu **1015** pro **SMS_PORTALWEB_CONTROL_MANAGER** potvrdí, že správce součástí lokality úspěšně nainstaloval bod webu Katalog aplikací.  

- Soubory protokolu: Hledejte soubory **SMSAWEBSVCSetup.log** a **SMSPORTALWEBSetup.log**.  

    Pokud chcete získat další informace, vyhledejte soubory protokolu **awebsvcMSI. log** a **portlwebMSI. log** .  


### <a name="step-4-configure-client-settings"></a>Krok 4: Konfigurace nastavení klienta

Pokud chcete, aby všichni uživatelé měli stejné nastavení, nakonfigurujte výchozí nastavení klienta. Jinak nakonfigurujte vlastní nastavení klienta pro konkrétní kolekce.

Další informace najdete v těchto článcích:

- [O nastavení klientů](../../core/clients/deploy/about-client-settings.md)  
    - Počítačový agent  
    - Restartování počítače  
    - Centrum softwaru  
    - Nasazení softwaru  
    - Spřažení uživatelů a zařízení  
- [Postup konfigurace nastavení klienta](../../core/clients/deploy/configure-client-settings.md)  

Klient Configuration Manager při příštím stahování zásad klienta nakonfiguruje zařízení s těmito nastaveními. Chcete-li spustit načtení zásad pro jednoho klienta, přečtěte si téma [Správa klientů](../../core/clients/manage/manage-clients.md).


### <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Krok 5: ověření funkčnosti katalogu aplikací

K ověření, zda je katalog aplikací funkční, použijte následující postupy.

> [!NOTE]  
> Činnost koncového uživatele katalogu aplikací vyžaduje program Microsoft Silverlight. Pokud používáte katalog aplikací přímo z prohlížeče, nejprve ověřte, zda je v počítači nainstalován produkt Microsoft Silverlight.  

> [!TIP]  
> Chybějící požadované součásti patří mezi nejčastější důvody, proč katalog aplikací po instalaci nesprávně funguje. Potvrďte předpoklady role pro role systému lokality katalogu aplikací. Další informace najdete v tématu [Požadované součásti lokality a systému lokality](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

V prohlížeči zadejte adresu webu katalogu aplikací. Potvrďte, že webová stránka zobrazuje tři karty: **Katalog aplikací**, **Moje žádosti o aplikace**a **Moje zařízení**.  

Použijte odpovídající adresu pro katalog aplikací z následujícího seznamu, kde `<server>` je název počítače, INTRANETOVÝ název FQDN nebo internetový název FQDN:  

- Připojení klienta prostřednictvím protokolu HTTPS a výchozí nastavení role systému lokality:`https://<server>/CMApplicationCatalog`  

- Připojení klienta prostřednictvím protokolu HTTP a výchozí nastavení role systému lokality:`http://<server>/CMApplicationCatalog`  

- Připojení klienta prostřednictvím protokolu HTTPS a vlastní nastavení role systému lokality:`https://<server>:<port>/<web application name>`  

- Připojení klienta prostřednictvím protokolu HTTP a vlastní nastavení role systému lokality:`http://<server>:<port>/<web application name>`  

> [!NOTE]  
> Pokud jste se k zařízení přihlásili pomocí účtu správce domény, klient Configuration Manager nezobrazuje oznamovací zprávy. Například zprávy indikující, že je k dispozici nový software.  
