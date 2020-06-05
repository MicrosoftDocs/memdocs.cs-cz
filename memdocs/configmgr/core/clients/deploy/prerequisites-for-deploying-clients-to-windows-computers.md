---
title: Předpoklady pro nasazení klienta Windows
titleSuffix: Configuration Manager
description: Přečtěte si informace o požadavcích nasazení klienta Configuration Manager do počítačů se systémem Windows.
ms.date: 06/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2aa375d0521e6088904ebe9a1f10af83f4bc261f
ms.sourcegitcommit: 92e6d2899b1cf986c29c532d0cd0555cad32bc0c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428558"
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-configuration-manager"></a>Předpoklady pro nasazení klientů do počítačů s Windows v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Nasazení Configuration Manager klientů ve vašem prostředí má následující externí závislosti a závislosti v rámci produktu. Každá metoda nasazení klienta má navíc vlastní závislosti, které musí být k úspěšné instalaci klienta splněny.  

Další informace o minimálních požadavcích na hardware a operační systém pro klienta Configuration Manager najdete v části [podporované konfigurace](../../plan-design/configs/supported-configurations.md).  

> [!NOTE]  
> Čísla verzí softwaru uvedená v tomto článku pouze označují čísla minimálních požadovaných verzí.  

## <a name="prerequisites-for-windows-clients"></a><a name="BKMK_prereqs_computers"></a>Předpoklady pro klienty Windows  

Pomocí následujících informací určete předpoklady pro instalaci klienta Configuration Manager do zařízení se systémem Windows.  

### <a name="dependencies-external-to-configuration-manager"></a>Vnější závislosti nástroje Configuration Manager

Mnohé z těchto součástí jsou služby nebo funkce, které Windows ve výchozím nastavení povoluje. Tyto komponenty nebudete v Configuration Manager klientech zakazovat.

|Součást|Description|
|---|---|
|Instalační služba systému Windows|Vyžaduje se k podpoře použití Instalační služba systému Windows souborů pro aplikace a aktualizace softwaru.|
|Služba inteligentního přenosu na pozadí (BITS)|Vyžaduje se k tomu, aby se omezily přenosy dat mezi klientským počítačem a Configuration Manager systémy lokality.|
|Microsoft Task Scheduler|Vyžaduje se pro klientské operace, jako je například pravidelné vyhodnocení stavu klienta Configuration Manager.|
|Microsoft Remote Differential Compression (RDC)|Algoritmus vyžadovaný k optimalizaci přenosu dat prostřednictvím sítě.|
|Podpora podepisování kódu SHA-2|Počínaje verzí 1906 vyžadují klienti podporu pro podpisový algoritmus kódu SHA-2. Další informace najdete v tématu [Podpora podepisování kódu SHA-2](#bkmk_sha2).|

#### <a name="sha-2-code-signing-support"></a><a name="bkmk_sha2"></a>Podpora podepisování kódu SHA-2

<!--SCCMDocs-pr#3404-->
Z důvodu slabých míst v algoritmu SHA-1 a pro zajištění souladu s oborovou normou společnost Microsoft nyní pouze podepisuje Configuration Manager binárních souborů pomocí bezpečnějšího algoritmu SHA-2. Starší verze operačních systémů Windows vyžadují aktualizaci pro podporu podepisování kódu SHA-2. Další informace najdete v tématu [požadavky na podporu podepisování kódu 2019 SHA-2 pro Windows a WSUS](https://support.microsoft.com/help/4472027/2019-sha-2-code-signing-support-requirement-for-windows-and-wsus).

Pokud tyto verze operačních systémů neaktualizujete, nemůžete nainstalovat klienta Configuration Manager verze 1906. Toto chování se týká buď nové instalace nebo aktualizace klienta z předchozí verze.

Pokud potřebujete spravovat klienta ve verzi Windows, která není aktualizovaná, nebo starší než výše uvedená verze, použijte klienta Configuration Manager EICed pro interoperabilitu () verze 1902. Další informace najdete v tématu [Rozšířený klient interoperability](../../understand/interoperability-client.md).

> [!Tip]  
> Pokud nepoužíváte [automatickou aktualizaci klienta](../manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)a aktualizujete klienty s jiným mechanismem, nezapomeňte aktualizovat verzi programu CCMSetup. Starší verze programu CCMSetup nemusí správně ověřit nový certifikát podepisování kódu SHA-2 v binárních souborech klienta verze 1906. Například pokud kopírujete program CCMSetup. exe do sdílené složky nebo použijete soubor CCMSetup. msi se zásadami skupiny.<!-- 4963362 -->
>
> Následující mechanismy aktualizace klientů by neměly být ovlivněné:
>
> - Klientská nabízená instalace: používá balíček klienta z lokality.
> - Instalace na základě aktualizace softwaru: aktualizace lokality se znovu publikuje ve službě WSUS.
> - Zařízení s Windows spravovaná pomocí Intune MDM: podporovaná verze pro tento mechanismus už podporuje podepisování kódu SHA-2, ale je ale důležité použít nejnovější soubor CCMSetup. msi.

### <a name="dependencies-external-to-configuration-manager-and-automatically-downloaded-during-installation"></a><a name="bkmk_ExternalDependencies"></a>Vnější závislosti Configuration Manager a automaticky stažené při instalaci  

Klient Configuration Manager má vnější závislosti. Tyto závislosti závisí na verzi operačního systému a nainstalovaném softwaru na klientském počítači.  

Pokud klient vyžaduje, aby tyto závislosti dokončí instalaci, nainstaluje je automaticky.

|Součást|Description|
|---|---|
|Microsoft Core XML Services (MSXML) verze 6.20.5002 nebo novější ( `msxml6.msi` )|Služba vyžadovaná jako podpora zpracování dokumentů XML v systému Windows.|
|Microsoft Visual C++ 2013 Redistributable verze 12.0.40660.0 ( `vcredist_x*.exe` )|Balíček vyžadovaný jako podpora činnosti klienta. Při instalaci této aktualizace do klientských počítačů může dokončení instalace vyžadovat restart.|<!-- SCCMDocs#1526 -->
|Rozhraní API Windows Imaging 6.0.6001.18000 nebo novější ( `wimgapi.msi` )|Vyžaduje se, aby Configuration Manager mohl spravovat soubory Windows Image (. wim).|
|Microsoft Policy Platform 1.2.3514.0 nebo novější ( `MicrosoftPolicyPlatformSetup.msi` )|Služba vyžadovaná k tomu, aby mohli klienti vyhodnocovat nastavení shody.|  
|Microsoft .NET Framework verze 4.5.2 nebo novější ( `NDP452-KB2901907-x86-x64-AllOS-ENU.exe` )|Balíček vyžadovaný jako podpora činnosti klienta. Automaticky nainstalováno v klientském počítači, pokud nemá nainstalovánu verzi Microsoft .NET Framework verze 4,5 nebo novější. Další informace najdete v tématu [Další podrobnosti o rozhraní Microsoft .NET Framework verze 4.5.2](#dotNet).|  
|Součásti Microsoft SQL Server Compact 4,0 SP1|Vyžadovány k ukládání informací souvisejících s činností klienta.|  

> [!Important]
> Uživatelské prostředí programu Silverlight v katalogu aplikací není v aktuální větvi verze 1806 podporováno. Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací. Podpora končí pro role katalogu aplikací s verzí 1910.  
>
> Další informace najdete v následujících článcích:
>
> - [Konfigurace centra softwaru](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Odebrané a zastaralé funkce](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  
>
> Pokud stále používáte uživatelské prostředí webu Katalog aplikací, klient vyžaduje program Microsoft Silverlight 5.1.41212.0. Klient nebude automaticky instalovat program Silverlight. Hlavní funkce katalogu aplikací je teď součástí centra softwaru.<!--1356195-->

#### <a name="additional-details-about-microsoft-net-framework-version-452"></a><a name="dotNet"></a>Další podrobnosti o Microsoft .NET Framework verze 4.5.2  

> [!NOTE]  
> Rozhraní .NET 4,0, 4,5 a 4.5.1 již nejsou podporována. Další informace najdete v tématu [Nejčastější dotazy k zásadám životního cyklu podpory pro Microsoft .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework).  

Microsoft .NET Framework verze 4.5.2 může vyžadovat restart k dokončení instalace. Uživateli se na hlavním panelu systému zobrazí oznámení **vyžadované k restartování** . Následující běžné scénáře vyžadují restartování klientských počítačů:  

- V počítači jsou spuštěné služby nebo aplikace .NET.  

- Chybí jedna nebo několik aktualizací vyžadovaných pro instalaci technologie .NET.  

- Počítač čeká na restartování z předchozí instalace aktualizací softwaru .NET Framework.  

Po nainstalování .NET Framework 4.5.2 může vyžadovat další aktualizace. Tyto pozdější aktualizace mohou vyžadovat další restartování počítače.  

### <a name="configuration-manager-dependencies"></a>Závislosti nástroje Configuration Manager  

Další informace najdete v tématu [Určení rolí systému lokality pro klienty](plan/determine-the-site-system-roles-for-clients.md)nástroje.  

|Součást|Description|  
|---|---|  
|Bod správy|Chcete-li nasadit klienta Configuration Manager, nebudete potřebovat bod správy. Klienti vyžadují bod správy pro přenos informací s lokalitou. Bez bodu správy nemůžete spravovat klientské počítače.|  
|Distribuční bod|Distribuční bod je volitelná, ale doporučená role systému lokality pro nasazení a správu klientů. Všechny distribuční body hostují zdrojové soubory klienta. Klienti hledají nejbližší distribuční bod, ze kterého se mají stáhnout zdrojové soubory během nasazování nebo aktualizace klienta. Pokud lokalita nemá distribuční bod, počítače stáhnou zdrojové soubory klienta ze svého bodu správy.|  
|Bod záložního stavu|Bod záložního stavu je při nasazování klienta volitelná, avšak doporučená role systému lokality. Bod záložního stavu sleduje nasazování klienta a umožňuje počítačům v Configuration Manager lokality odesílat stavové zprávy, když nemohou komunikovat s bodem správy.|  
|Bod služby Reporting services|Bod služby Reporting Services je volitelná, ale doporučená role systému lokality. Zobrazuje sestavy týkající se nasazení a správy klientů. Další informace najdete v tématu [Úvod do vytváření sestav](../../servers/manage/introduction-to-reporting.md).|  

### <a name="installation-method-dependencies"></a>Závislosti metod instalace  

Podle konkrétní metody instalace klienta může být vyžadováno splnění těchto podmínek:  

#### <a name="client-push-installation"></a>Klientská nabízená instalace  

- Lokalita používá účty klientské nabízené instalace pro připojení k počítačům pro instalaci klienta. Na kartě **účty** ve vlastnostech klientské nabízené instalace zadejte tyto účty. Účet musí být v cílovém počítači členem místní skupiny Administrators.  

    Pokud nezadáte účet klientské nabízené instalace, server lokality použije svůj účet počítače.  

- Lokalita musí zjistit počítač, na který klienta instalujete. Vyžaduje se aspoň jedna metoda zjišťování Configuration Manager.  

- V počítači je sdílená složka ADMIN$.  

- Pokud chcete automaticky nabízet klienta Configuration Manager ke zjištěným prostředkům, vyberte možnost **Povolit nabízenou instalaci klienta pro přiřazené prostředky** ve vlastnostech klientské nabízené instalace.  

- Klientský počítač musí komunikovat s distribučním bodem nebo bodem správy, aby mohl stáhnout zdrojové soubory.  

- Pokud vyžadujete vzájemné ověřování pomocí protokolu Kerberos, klienti musí být v důvěryhodné doménové struktuře služby Active Directory. Protokol Kerberos v systému Windows spoléhá na vzájemné ověřování služby Active Directory.<!--1358204-->  

Chcete-li použít klientskou nabízenou instalací, potřebujete následující oprávnění zabezpečení:  

- Konfigurace účtu klientské nabízené instalace: oprávnění **Upravit** a **číst** pro objekt **lokalita** .  

- Použití klientské nabízené instalace k instalaci klienta do kolekcí, zařízení a dotazů: oprávnění **Upravit prostředek** a **číst** pro objekt **kolekce** .  

Role zabezpečení výchozí **správce infrastruktury** zahrnuje požadovaná oprávnění ke správě nabízených instalací klienta.  

#### <a name="software-update-point-based-installation"></a>Instalace aktualizace softwaru z bodu  

- Pokud jste nerozšířili schéma služby Active Directory nebo pokud instalujete klienty z jiné doménové struktury, pomocí zásad skupiny zřídíte parametry instalace pro soubor CCMSetup. exe. Další informace najdete v tématu [jak zřídit vlastnosti instalace klienta](deploy-clients-to-windows-computers.md#BKMK_Provision).  

- Publikujte klienta Configuration Manager do bodu aktualizace softwaru.  

- Chcete-li stáhnout zdrojové soubory, musí klientský počítač komunikovat s distribučním bodem nebo bodem správy.  

Oprávnění zabezpečení potřebná ke správě Configuration Manager aktualizací softwaru najdete v tématu [předpoklady pro aktualizace softwaru](../../../sum/plan-design/prerequisites-for-software-updates.md).  

#### <a name="group-policy-based-installation"></a>Instalace na základě zásad skupiny  

- Pokud jste nerozšířili schéma služby Active Directory nebo pokud instalujete klienty z jiné doménové struktury, pomocí zásad skupiny zřídíte parametry instalace pro soubor CCMSetup. exe. Další informace najdete v tématu [jak zřídit vlastnosti instalace klienta](deploy-clients-to-windows-computers.md#BKMK_Provision).  

- Chcete-li stáhnout zdrojové soubory, musí klientský počítač komunikovat s distribučním bodem nebo bodem správy.  

#### <a name="logon-script-based-installation"></a>Instalace pomocí přihlašovacího skriptu  

Chcete-li stáhnout zdrojové soubory, musí klientský počítač komunikovat s distribučním bodem nebo bodem správy. Pokud jste nezadali program CCMSetup. exe s následujícím parametrem příkazového řádku:`ccmsetup /source`  

#### <a name="manual-installation"></a>Ruční instalace  

Chcete-li stáhnout zdrojové soubory, musí klientský počítač komunikovat s distribučním bodem nebo bodem správy. Pokud jste nezadali program CCMSetup. exe s následujícím parametrem příkazového řádku:`ccmsetup /source`  

#### <a name="microsoft-intune-mdm-installation"></a>Instalace Microsoft Intune MDM

- Vyžaduje předplatné Microsoft Intune a příslušné licence.  

- Vyžaduje, aby zařízení mělo přístup k Internetu, a to i v případě, že není na internetu.  

- V závislosti na případu použití můžete také vyžadovat jednu nebo obě následující technologie:  

    - Azure Active Directory  

    - Brána pro správu cloudu  

#### <a name="workgroup-computer-installation"></a>Instalace do počítačů v pracovní skupině  

Chcete-li získat přístup k prostředkům v doméně serveru Configuration Manager lokality, nakonfigurujte účet přístupu k síti pro lokalitu.  

Další informace o tom, jak nakonfigurovat účet přístupu k síti, najdete v tématu [základní koncepty správy obsahu](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

#### <a name="software-distribution-based-installation-for-upgrades-only"></a>Instalace s využitím distribuce softwaru (pouze upgrade)  

- Pokud jste nerozšířili schéma služby Active Directory nebo pokud instalujete klienty z jiné doménové struktury, pomocí zásad skupiny zřídíte parametry instalace pro soubor CCMSetup. exe. Další informace najdete v tématu [jak zřídit vlastnosti instalace klienta](deploy-clients-to-windows-computers.md#BKMK_Provision).

- Chcete-li stáhnout zdrojové soubory, musí klientský počítač komunikovat s distribučním bodem nebo bodem správy.  

Informace o oprávněních zabezpečení vyžadovaných k upgradu klienta Configuration Manager pomocí správy aplikací najdete v tématu [zabezpečení a ochrana osobních údajů pro správu aplikací](../../../apps/plan-design/security-and-privacy-for-application-management.md).  

#### <a name="automatic-client-upgrades"></a>Automatický upgrade klienta  

Chcete-li konfigurovat automatický upgrade klienta, musíte být členem role zabezpečení **Správce s úplnými oprávněními**.  

### <a name="firewall-requirements"></a>Požadavky na bránu firewall  

Pokud existuje brána firewall mezi servery systému lokality a počítači, na které chcete nainstalovat klienta Configuration Manager, přečtěte si téma [nastavení brány Windows Firewall a portů pro klienty](windows-firewall-and-port-settings-for-clients.md).  


## <a name="prerequisites-for-mobile-device-clients"></a><a name="BKMK_prereqs_mobiledevices"></a>Předpoklady pro klienty mobilních zařízení  

Když instalujete klienta Configuration Manager na mobilních zařízeních a zaregistrujete je, použijte tyto informace k určení požadovaných součástí.  

### <a name="dependencies-external-to-configuration-manager"></a>Vnější závislosti nástroje Configuration Manager

- Certifikační autorita (CA) organizace od společnosti Microsoft s šablonami nasazení, které mají být nasazeny a používány ke správě certifikátů vyžadovaných pro mobilní zařízení.  

    Vydávající CA musí během procesu zápisu automaticky schvalovat žádosti o certifikát od uživatelů mobilních zařízení.  

    Další informace o požadavcích na certifikát najdete v tématu [zabezpečení a ochrana osobních údajů pro profily certifikátů](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md).  

- Skupina zabezpečení obsahující uživatele, kteří mohou zapsat mobilní zařízení.  

    Skupina zabezpečení slouží ke konfiguraci šablony certifikátu používané při zápisu mobilního zařízení.  

- Volitelné, ale doporučené: alias DNS (záznam CNAME) s názvem **ConfigMgrEnroll**. Nakonfigurujte tento alias pro název serveru zprostředkujícího bodu registrace.  

    Tento alias DNS je nutný k podpoře automatického zjišťování pro službu zápisu. Pokud tento záznam DNS nenakonfigurujete, uživatelé musí jako součást procesu registrace ručně zadat název zprostředkujícího bodu registrace.  

- Závislosti role systému lokality pro počítače, na kterých se spouští bod registrace a role systému lokality zprostředkujícího bodu registrace.  

    Další informace najdete v tématu [podporované operační systémy pro servery systému lokality](../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).  

### <a name="configuration-manager-dependencies"></a>Závislosti nástroje Configuration Manager

Další informace najdete v tématu [Určení rolí systému lokality pro klienty](plan/determine-the-site-system-roles-for-clients.md)nástroje.  

- Bod správy nakonfigurovaný pro připojení klientů přes protokol HTTPS a povolený pro mobilní zařízení  

    Pro instalaci klienta Configuration Manager do mobilních zařízení je vždy vyžadován bod správy. Kromě požadavků na konfiguraci HTTPS a povolených pro mobilní zařízení musí být bod správy nakonfigurovaný pomocí internetového plně kvalifikovaného názvu domény a přijímají připojení klientů z Internetu.  

- Bod registrace a zprostředkující bod registrace  

    Zprostředkující bod registrace spravuje žádosti o zápis z mobilních zařízení, proces zápisu pak dokončuje bod registrace. Bod zápisu musí být ve stejné doménové struktuře služby Active Directory jako server lokality, zprostředkující bod registrace může být v jiné doménové struktuře.  

- Nastavení klientů pro zápis mobilních zařízení  

    Nakonfigurujte klienta tak, aby uživatelům umožňoval zapsat mobilní zařízení a nakonfigurovat alespoň jeden profil zápisu.  

- Bod služby Reporting services  

    Bod služby Reporting services je volitelná, avšak doporučená role systému lokality, která může zobrazovat sestavy k zápisu mobilních zařízení a správě klienta.  

    Další informace najdete v tématu [Úvod do vytváření sestav](../../servers/manage/introduction-to-reporting.md).  

- Chcete-li nakonfigurovat zápis pro mobilní zařízení, musíte mít následující oprávnění zabezpečení:  

    - K přidávání, úpravám a odstraňování zápisových rolí systému lokality: Oprávnění **Upravit** pro objekt **Lokalita**.  

    - Ke konfiguraci nastavení klienta k zápisu: Výchozí nastavení klienta vyžaduje oprávnění **Upravit** pro objekt **Lokalita**, a vlastní nastavení klienta vyžaduje oprávnění **Klientský agent**.  

    Výchozí role zabezpečení **úplný správce** zahrnuje požadovaná oprávnění ke konfiguraci rolí systému lokality pro zápis.  

- Chcete-li spravovat zapsaná mobilní zařízení, musíte mít následující oprávnění zabezpečení:  

    - K vymazání nebo vyřazení mobilního zařízení: Oprávnění **Odstranit prostředek** pro objekt **Kolekce**.  

    - Ke zrušení příkazu vymazání nebo vyřazení: Oprávnění **Odstranit prostředek** pro objekt **Kolekce**.  

    - Povolení a blokování mobilních zařízení: **Upravit prostředek** pro objekt **Kolekce** .  

    - Ke vzdálenému uzamčení nebo resetování hesla mobilního zařízení: Oprávnění **Upravit prostředek** pro objekt **Kolekce**.  

    Výchozí role zabezpečení **správce operací** zahrnuje požadovaná oprávnění ke správě mobilních zařízení.  

    Další informace o tom, jak nakonfigurovat oprávnění zabezpečení, najdete v tématu [základy správy na základě rolí](../../understand/fundamentals-of-role-based-administration.md) a [Konfigurace správy na základě rolí](../../servers/deploy/configure/configure-role-based-administration.md).  

### <a name="firewall-requirements"></a>Požadavky na bránu firewall

Použitá síťová zařízení, jako jsou směrovače a brány firewall, případně i brána Windows Firewall, musí umožňovat provoz související se zápisem mobilních zařízení:  

- Mezi mobilními zařízeními a proxy bodu zápisu: HTTPS (standardně, TCP 443)  

- Mezi proxy bodu zápisu a bodem zápisu: HTTPS (standardně, TCP 443)  

Pokud používáte webový proxy server, musí být nakonfigurován pro tunelování SSL. Přemostění SSL není u mobilních zařízení podporováno.  
