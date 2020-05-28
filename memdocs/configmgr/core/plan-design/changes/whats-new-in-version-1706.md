---
title: Nová verze 1706
titleSuffix: Configuration Manager
description: Získejte podrobnosti o změnách a nových funkcích zavedených ve verzi 1706 Configuration Manager.
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ac034143-003e-4629-aac2-99eaffef4db1
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: a8a4ce1c3d54311db18decc85f57d3e03298d339
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904692"
---
# <a name="what39s-new-in-version-1706-of-configuration-manager"></a>Co&#39;s novinkou ve verzi 1706 Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Aktualizace 1706 pro Configuration Manager aktuální větev je k dispozici jako aktualizace konzoly pro dříve nainstalované lokality, na kterých běží verze 1606, 1610 nebo 1702.

> [!TIP]  
> Chcete-li nainstalovat novou lokalitu, je nutné použít základní verzi Configuration Manager.  
>
> Další informace:    
> - [Instalace nových lokalit](../../servers/deploy/install/installing-sites.md)  
> - [Instalace aktualizací v lokalitách](../../servers/manage/updates.md)  
> - [Základní a aktualizační verze](../../servers/manage/updates.md#bkmk_Baselines)  

Následující části obsahují podrobné informace o změnách a nových funkcích, které jsou představené ve verzi 1706 Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1706 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infrastruktura webu

### <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Podpora souborů Expresní instalace v klientu sdílené mezipaměti pro Windows 10 a Office 365  
<!-- 1352486 -->
Od této verze sdílená mezipaměť podporuje distribuci souborů Expresní instalace obsahu pro Windows 10 a souborů aktualizací pro Office 365. Pro podporu této změny nejsou potřeba žádné další konfigurace.

### <a name="updates-for-the-data-warehouse"></a>Aktualizace datového skladu
<!-- 1277922 -->
Datový sklad už není součástí předběžné verze. Také jsme aktualizovali požadavky, aby zahrnovaly podporu pro databázi v SQL Server skupiny dostupnosti Always On a clustery s podporou převzetí služeb při selhání. Další informace najdete v [bodu služby datového skladu](../../servers/manage/data-warehouse.md).

### <a name="accessibility-improvements"></a>Vylepšení přístupnosti
<!-- 1253000 -->
Přidali jsme další vylepšení usnadnění pro Configuration Manager konzolu. Podrobnosti najdete v tématu [funkce usnadnění](../../understand/accessibility-features.md).

### <a name="improvements--for-sql-server-always-on-availability-groups"></a>Vylepšení pro skupiny dostupnosti Always On SQL Server
<!-- 1352094 -->
V této verzi teď můžete používat repliky asynchronního potvrzení ve skupinách dostupnosti Always On SQL Server, které používáte s Configuration Manager. To znamená, že můžete přidat další repliky do skupin dostupnosti, které se použijí jako nepřesné (vzdálené) zálohy, a pak je použít ve scénáři zotavení po havárii.  
- Configuration Manager podporuje použití repliky asynchronního potvrzení k obnovení synchronní repliky. Informace o tom, jak to provést, najdete v tématu [Možnosti obnovení databáze lokality](../../servers/manage/recover-sites.md#site-database-recovery-options) v tématu Zálohování a obnovení.
- Tato verze nepodporuje převzetí služeb při selhání pro použití repliky asynchronního potvrzení jako databáze lokality.
Další informace najdete v tématu [Příprava na používání skupin dostupnosti Always On](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="update-reset-tool"></a>Nástroj pro resetování aktualizací
<!-- 1324589 -->
Počínaje verzí 1706, Configuration Manager primárními lokalitami a lokalitami centrální správy zahrnuje nástroj pro resetování aktualizací Configuration Manager **CMUpdateReset. exe**. Tento nástroj použijte u libovolné verze aktuální větve, která zůstává v rámci podpory, a opravte problémy, když mají aktualizace v konzole problémy při stahování nebo replikaci. Další informace najdete v tématu [Nástroj pro obnovení aktualizací](../../servers/manage/update-reset-tool.md).

### <a name="high-dpi-console-support"></a>Podpora konzoly s vysokým rozlišením DPI  
<!-- 1353476 -->
V této verzi jsou problémy s tím, jak Configuration Manager konzola škáluje a zobrazuje různé části uživatelského rozhraní při zobrazení na vysokém počtu DPI (například na Surface).

### <a name="improved-boundary-groups-for-software-update-points"></a>Vylepšené skupiny hranic pro body aktualizace softwaru
<!-- 1324591 -->
Tato verze zahrnuje vylepšení způsobu práce bodů aktualizace softwaru se skupinami hranic. Následující shrnuje nové nouzové chování:
- Záloha pro body aktualizace softwaru teď používá konfigurovatelný čas pro přechod do sousedních skupin hranic.
- Nezávisle na záložní konfiguraci se klient pokusí spojit s posledním bodem aktualizace softwaru, který se použil po dobu 120 minut. Po neúspěšném pokusu o dosažení tohoto serveru na 120 minut klient zkontroluje svůj fond dostupných bodů aktualizace softwaru, aby mohl najít nový.
- Po neúspěšném přístupu k původnímu serveru po dobu dvou hodin se klient přepne na kratší cyklus, aby se obrátil na nový bod aktualizace softwaru. To znamená, že pokud se klient nemůže připojit k novému serveru, rychle vybere další server z fondu dostupných serverů a pokusí se ho kontaktovat.

Další informace najdete v tématu [body aktualizace softwaru](../../servers/deploy/configure/boundary-groups.md#software-update-points) v tématu skupiny hranic pro Current Branch.

### <a name="azure-ad-integration-with-configuration-manager"></a>Integrace Azure AD s Configuration Manager
<!-- 1248187, 1290765, 1258052, 1298097, 1319334, 1319883, 1352135, 1353331 -->
V této verzi jsme vylepšili integraci Configuration Manager a Azure Active Directory (Azure AD).  Tato vylepšení zjednodušují konfiguraci služeb Azure, které používáte s Configuration Manager, a umožňují spravovat klienty a uživatele, kteří se ověřují i přes Azure AD.

Vylepšená integrace přináší tyto možnosti:  
- Průvodce službami Azure – Tento průvodce poskytuje společné prostředí pro konfiguraci, které nahrazuje jednotlivé pracovní postupy, aby bylo možné nastavit následující služby Azure, které používáte s Configuration Manager.
  - **Správa cloudu** Umožněte klientům ověřování pomocí Azure Active Directory (Azure AD). Můžete taky nakonfigurovat zjišťování uživatelů Azure AD.
  - **Konektor Log Analytics** Připojte se k Azure Log Analytics a synchronizujte data kolekce.
  - **Upgrade Readiness** Připojení k Upgrade Readiness a zobrazení dat o kompatibilitě klienta s upgradem.
  - **Windows Store pro firmy** Připojte se k online obchodu pro Windows Store pro firmy a Získejte aplikace pro vaši organizaci, které můžete nasadit pomocí Configuration Manager.


  K tomu je potřeba použít [webovou aplikaci Azure Server](/azure/app-service/app-service-authentication-overview) k poskytnutí podrobností o předplatném a konfiguraci, které jinak zadáte pokaždé, když nastavíte novou Configuration Manager komponentu nebo službu s Azure. Další informace najdete v tématu [Průvodce službami Azure](../../servers/deploy/configure/azure-services-wizard.md).

- Pomocí Azure AD můžete ověřovat klienty na internetu a přistupovat k webům Configuration Manager. Azure AD nahrazuje nutnost konfigurovat a používat certifikáty pro ověřování klientů. To vyžaduje roli systému lokality brány pro správu cloudu. Další informace najdete v tématu [instalace a přiřazení klientů Configuration Manager z Internetu pomocí Azure AD pro ověřování](../../clients/deploy/deploy-clients-cmg-azure.md).

- Nainstalujte a spravujte klienta Configuration Manager v počítačích, které jsou umístěné na internetu. To vyžaduje použití role systému lokality brány pro správu cloudu. Další informace najdete v tématu [instalace a přiřazení klientů Configuration Manager z Internetu pomocí Azure AD pro ověřování](../../clients/deploy/deploy-clients-cmg-azure.md).

- Nakonfigurujte zjišťování uživatelů Azure AD.  Tuto novou metodu zjišťování můžete nakonfigurovat pomocí Průvodce službami Azure. Tato nová metoda se dotazuje na data uživatelů v Azure AD, která pak můžete použít společně s tradičními daty zjišťování.  Podporují se úplné i rozdílové synchronizace.  Další informace najdete v tématu [zjišťování uživatelů Azure AD](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc).

### <a name="peer-cache-improvements"></a>Vylepšení sdílené mezipaměti
<!-- 1252345 -->
Sdílená mezipaměť již nepoužívá účet přístupu k síti k ověřování požadavků na stažení od partnerských uzlů. Tato výstraha je k dispozici v případě, že účet zůstává vyžadován klienty. To zůstává nutné pro klienty, kteří se spouštějí do prostředí WinPE, a pak mají přístup k obsahu ze zdroje sdílené mezipaměti. Další informace najdete v tématu [požadavky a požadavky pro](../hierarchy/client-peer-cache.md#requirements)sdílenou mezipaměť.


<!-- ## Migration  -->


<!-- ## Client management  -->


## <a name="compliance-settings"></a>Nastavení dodržování předpisů

### <a name="new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client"></a>Nové nastavení konfigurace pro zařízení s Windows 10, která nejsou spravovaná pomocí klienta Configuration Manager.
<!-- 1354715 -->
V této verzi jsme přidali nové nastavení položky konfigurace pro zařízení s Windows 10, která jsou zaregistrovaná v Intune, nebo spravovaná místně pomocí Configuration Manager. Nastavení:

- **Heslo**
  - Šifrování zařízení
- **Zařízení**
  - Změny nastavení oblasti (jenom desktopové)
  - Úprava nastavení napájení a režimu spánku
  - Změny nastavení jazyka
  - Změna systémového času
  - Úprava názvu zařízení
- **Store**
  - Automaticky aktualizovat aplikace ze Storu
  - Použít pouze privátní úložiště
  - Spuštění aplikace pocházející ze Storu
- **Microsoft Edge**
  - Zablokovat přístup k about: Flags
  - Přepsání výzvy SmartScreen
  - Přepsání výzvy SmartScreen pro soubory
  - IP adresa WebRTC localhost
  - Výchozí vyhledávací modul
  - Adresa URL XML pro OpenSearch
  - Domovské stránky (jenom desktopové)

Podrobnosti o všech nastaveních Windows 10 najdete v tématu [Vytvoření položek konfigurace pro Windows 8.1 a zařízení s Windows 10 spravovaná bez klienta Configuration Manager](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).

### <a name="new-device-compliance-policy-rules"></a>Nová pravidla zásad dodržování předpisů pro zařízení

* **Požadovaný typ hesla**. Určete, zda musí uživatel vytvořit alfanumerické nebo číselné heslo. U alfanumerických hesel je také možné zadat minimální počet znakových sad, které musí heslo obsahovat. Jedná se o čtyři znakové sady: malá písmena, Velká písmena, symboly a čísla.

  **Podporované platformy:**
  * Windows Phone 8+
  * Windows 8.1 +
  * iOS 6+
  <br></br>
* **Blokuje na zařízení ladění USB**. Toto nastavení nemusíte konfigurovat, protože ladění USB je už na zařízeních s Androidem for Work zakázané.

  **Podporované platformy:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  <br></br>
* **Blokuje aplikace z neznámých zdrojů**. Vyžadovat, aby zařízení bránila instalaci aplikací z neznámých zdrojů. Toto nastavení nemusíte konfigurovat, protože zařízení s Androidem for Work vždycky omezují instalaci z neznámých zdrojů.

  **Podporované platformy:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  <br></br>
* **Vyžadovat kontrolu hrozeb u aplikací** Toto nastavení určuje, že je na zařízení povolená funkce ověřovat aplikace.

  **Podporované platformy:**
  * Android 4,2 až 4,4
  * Samsung KNOX Standard 4.0+


## <a name="application-management"></a>Správa aplikací

### <a name="run-powershell-scripts-from-the-configuration-manager-console"></a>Spouštění skriptů PowerShellu z konzoly Configuration Manager
<!-- 1236459 -->

V Configuration Manager můžete do klientských zařízení nasadit skripty pomocí balíčků a programů. V této verzi jsme přidali nové funkce, které vám umožní provést následující akce:

- Import skriptů PowerShellu pro Configuration Manager
- Úprava skriptů z konzoly Configuration Manager (jenom pro nepodepsané skripty)
- Označení skriptů jako schválených nebo odepřených pro zlepšení zabezpečení
- Spouštějte skripty na kolekcích klientských počítačů s Windows a na místních spravovaných počítačích s Windows. Skripty nesadíte místo toho, aby byly spouštěny téměř v reálném čase na klientských zařízeních.
- Projděte si výsledky vracené skriptem v konzole Configuration Manager.

Další informace najdete v tématu [Vytvoření a spuštění skriptů PowerShellu z konzoly Configuration Manager](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="new-mobile-application-management-policy-settings"></a>Nová nastavení zásad správy mobilních aplikací    
<!--1324760-->
Od této verze můžete použít tři nová nastavení zásad správy mobilních aplikací (MAM):

- **Blokovat snímek obrazovky (jenom zařízení s Androidem):** Určuje, že při použití této aplikace jsou při používání této aplikace zablokované možnosti zachycení obrazovky zařízení.


## <a name="operating-system-deployment"></a>Nasazení operačního systému

### <a name="hardware-inventory-collects-secure-boot-information"></a>Inventář hardwaru shromažďuje informace o zabezpečeném spuštění.
Inventář hardwaru nyní shromažďuje informace o tom, zda je na klientech povoleno zabezpečené spouštění. Tyto informace jsou uloženy ve třídě **SMS_Firmware** (představené ve verzi 1702) a jsou ve výchozím nastavení povoleny v inventáři hardwaru. Další informace o inventáři hardwaru najdete v tématu [Konfigurace inventáře hardwaru](../../clients/manage/inventory/configure-hardware-inventory.md).

### <a name="collapsible-task-sequence-groups"></a>Sbalitelné skupiny pořadí úloh
Tato verze přináší možnost Rozbalit a sbalit skupiny pořadí úloh. Můžete rozbalit nebo sbalit jednotlivé skupiny nebo rozbalit nebo sbalit všechny skupiny najednou.

### <a name="reload-boot-images-with-current-windows-pe-version"></a>Opětovné načtení spouštěcích imagí s aktuální verzí prostředí Windows PE
Když spouštíte **distribuční body aktualizace** na vybrané spouštěcí imagi, můžete si teď zvolit, že se má v spouštěcí imagi znovu načíst nejnovější verze prostředí Windows PE (z instalačního adresáře Windows ADK). Další informace najdete v tématu [aktualizace distribučních bodů pomocí spouštěcí bitové kopie](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image).

## <a name="software-updates"></a>Aktualizace softwaru

### <a name="improvements-to-express-update-download-time"></a>Vylepšení času stahování aktualizace Express
V této verzi jsme výrazně vylepšili dobu stahování expresních aktualizací. Další informace najdete v tématu [Správa souborů Expresní instalace pro aktualizace Windows 10](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).

### <a name="manage-microsoft-surface-driver-updates"></a>Spravovat aktualizace ovladačů Microsoft Surface
<!-- 1098490 -->
Teď můžete pomocí Configuration Manager spravovat aktualizace ovladačů Microsoft Surface.    


#### <a name="prerequisites"></a>Požadavky
- Všechny body aktualizace softwaru musí používat systém Windows Server 2016.    
- Toto je předběžná verze funkce, kterou musíte zapnout, aby byla dostupná. Další informace najdete v tématu [Použití předběžných verzí funkcí z aktualizací](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

#### <a name="to-manage-surface-driver-updates"></a>Správa aktualizací ovladačů Surface

1. Povolte synchronizaci pro ovladače Microsoft Surface. Použijte postup v části [Konfigurace klasifikace a produkty](../../../sum/get-started/configure-classifications-and-products.md) a zaškrtněte políčko **zahrnout ovladače Microsoft Surface a aktualizace firmwaru** na kartě **klasifikace** a povolte tak ovladače Surface.
2. [Synchronizovat ovladače Microsoft Surface](../../../sum/get-started/synchronize-software-updates.md).
3. [Nasazení synchronizovaných ovladačů Microsoft Surface](../../../sum/deploy-use/deploy-software-updates.md)

### <a name="configure-windows-update-for-business-deferral-policies"></a>Konfigurace zásad odložení web Windows Update pro firmy
<!-- 1290890 -->
Teď můžete nakonfigurovat zásady odložení pro aktualizace funkcí Windows 10 nebo aktualizace kvality pro zařízení s Windows 10 spravovaná přímo pomocí web Windows Update pro firmy. Zásady odložení můžete spravovat v uzlu nové **zásady web Windows Update pro firmy** v části **softwarová knihovna**  >  **Windows 10 – Údržba**.

Podrobnosti najdete v tématu [integrace s web Windows Update pro firmy ve Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md#configure-windows-update-for-business-deferral-policies).

### <a name="improved-user-notifications-for-office-365-updates"></a>Vylepšená uživatelská oznámení pro aktualizace Office 365
V případě, že klient nainstaluje aktualizaci Office 365, provedli jsme vylepšení využití uživatelského prostředí Klikni a spusť pro Office. To zahrnuje automaticky otevíraná okna a oznámení v aplikaci a možnosti odpočítávání. Další informace najdete v tématu [chování při restartování a oznámení klientů pro aktualizace Office 365](../../../sum/deploy-use/manage-office-365-proplus-updates.md#restart-behavior-and-client-notifications-for-office-365-updates) .

## <a name="reporting"></a>Vytváření sestav

### <a name="use-windows-analytics-with-configuration-manager"></a>Použití Windows Analytics s Configuration Manager
<!-- 1318608 -->
Windows Analytics je sada řešení, která umožňují vytvořit přehled o aktuálním stavu vašeho prostředí. Zařízení ve vašem prostředí sestavují data telemetrie ve Windows. K datům je možné přistupovat prostřednictvím Azure Portal. V případě Upgrade Readiness jsou data přímo k dispozici v uzlu monitorování konzoly Configuration Manager.


<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Správa mobilních zařízení

### <a name="updates-to-android-for-work-sharing-configuration"></a>Aktualizace konfigurace pro sdílení Androidu for Work
<!-- 1338403 -->
V této verzi byly aktualizovány hodnoty pro nastavení **Povolení sdílení dat mezi pracovním a osobním profilem** ve skupině nastavení **pracovního profilu** . Přidali jsme také vlastní nastavení pro blokování kopírování a vkládání mezi pracovními a osobními profily.


### <a name="android-and-ios-enrollment-restrictions"></a>Omezení registrace pro Android a iOS
<!-- 1290826 -->
V této verzi teď můžete určit, že uživatelé nebudou moct registrovat osobní zařízení s Androidem nebo iOS. Nová nastavení omezení zařízení umožňují omezit registraci zařízení s Androidem na předem deklarovaná zařízení. U zařízení se systémem iOS můžete zablokovat registraci všech zařízení kromě těch, které jsou zaregistrované ve službě Apple Program registrace zařízení, Apple Configuratoru nebo v rámci účtu správce registrace zařízení v Intune.

## <a name="protect-devices"></a>Ochrana zařízení

### <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Zahrnout vztah důvěryhodnosti pro konkrétní soubory a složky v zásadách Device Guard
<!--1324676-->
V této verzi jsme přidali další možnosti správy zásad Device Guard.

Nyní můžete volitelně přidat vztah důvěryhodnosti pro konkrétní soubory pro složky v zásadách ochrany zařízení. To vám umožní:

- Překonání problémů s chováním spravované instalační služby
- Důvěřovat obchodním aplikacím, které se nedají nasadit pomocí Configuration Manager
- Důvěryhodné aplikace, které jsou součástí bitové kopie nasazení operačního systému

Další podrobnosti najdete v tématu [Správa ochrany zařízení pomocí Configuration Manager](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md).
