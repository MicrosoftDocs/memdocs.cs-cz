---
title: Nová verze 1610
titleSuffix: Configuration Manager
description: Získejte podrobnosti o změnách a nových funkcích zavedených ve verzi 1610 Configuration Manager.
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b3e1a2feaddb7384d76790249152c89dfa8ee2d3
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904804"
---
# <a name="what39s-new-in-version-1610-of-configuration-manager"></a>Co&#39;s novinkou ve verzi 1610 Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Aktualizace 1610 pro Configuration Manager aktuální větev je k dispozici jako aktualizace konzoly pro dříve nainstalované lokality, na kterých běží verze 1511, 1602 nebo 1606.


> [!TIP]  
> Chcete-li nainstalovat novou lokalitu, je nutné použít základní verzi Configuration Manager.  
>
> Další informace:    
> - [Instalace nových lokalit](../../servers/deploy/install/installing-sites.md)  
> - [Instalace aktualizací v lokalitách](../../servers/manage/updates.md)  
> - [Základní a aktualizační verze](../../servers/manage/updates.md#bkmk_Baselines)

Následující části obsahují podrobné informace o změnách a nových funkcích, které jsou představené ve verzi 1610 Configuration Manager.  


## <a name="in-console-monitoring-of-update-installation-status"></a>Monitorování stavu instalace aktualizací v konzole  
Od verze 1610 platí, že při instalaci balíčku aktualizace a monitorování instalace v konzole nástroje je k dispozici nová fáze: **po instalaci**. Tato fáze zahrnuje stav pro úlohy, jako je restartování služby Key Services, a inicializaci monitorování replikace. (Tato fáze není v konzole k dispozici, dokud se vaše lokalita nebude aktualizovat na verzi 1610.) Další informace o stavu instalace aktualizací najdete v tématu [instalace konzolových aktualizací](../../servers/manage/install-in-console-updates.md#bkmk_install).


## <a name="exclude-clients-from-automatic-upgrade"></a>Vyloučit klienty z automatického upgradu
Můžete vyloučit klienty systému Windows z části získání upgradu s novými verzemi klientského softwaru. Provedete to tak, že zahrnete klientské počítače do kolekce, která je určená k vyloučení z upgradu. Klienti ve vyloučené kolekci ignorují žádosti o aktualizaci klientského softwaru.  Další informace najdete v tématu [vyloučení klientů Windows z upgradů](../../clients/manage/upgrade/exclude-clients-windows.md).


## <a name="improvements-for-boundary-groups"></a>Vylepšení pro skupiny hranic
Verze 1610 přináší důležité změny skupin hranic a jejich fungování s distribučními body. Tyto změny mohou zjednodušit návrh infrastruktury obsahu a zároveň vám poskytne lepší kontrolu nad tím, jak a kdy klienti mají možnost Hledat další distribuční body jako umístění zdroje obsahu. To zahrnuje místní i cloudové distribuční body.
Tato vylepšení nahrazují koncepty a chování, se kterými se můžete seznámit (například konfigurace distribučních bodů tak, aby byly rychlé nebo pomalé). Nový model by měl být snazší nastavit a udržovat. Tyto změny také upraví základy pro budoucí změny, které zlepšují jiné role systému lokality, které přiřadíte ke skupinám hranic.

Když aktualizujete na verzi 1610, aktualizace Převede aktuální konfigurace skupiny hranic tak, aby odpovídala novému modelu, aby tyto změny nenarušily stávající konfigurace distribuce obsahu.

Další informace najdete v tématu [skupiny hranic](../../servers/deploy/configure/boundary-groups.md).


## <a name="peer-cache-for-content-distribution-to-clients"></a>Sdílená mezipaměť pro distribuci obsahu klientům
Od verze 1610 klientská **mezipaměť** klienta vám pomůže spravovat nasazení obsahu do klientů ve vzdálených umístěních. Sdílená mezipaměť je integrované řešení Configuration Manager pro klienty, aby mohli sdílet obsah s ostatními klienty, a to přímo z místní mezipaměti.

Po nasazení nastavení klienta, které povoluje sdílené mezipaměti do kolekce, mohou členové této kolekce fungovat jako zdroj obsahu rovnocenného pro ostatní klienty ve stejné skupině hranic.

Můžete také použít nový řídicí panel **zdroje dat klienta** k pochopení použití zdrojů obsahu sdílené mezipaměti ve vašem prostředí.

> [!TIP]  
> Verze 1610, sdílená mezipaměť a řídicí panel zdrojů dat klienta jsou funkce předběžné verze. Pokud je chcete povolit, přečtěte si téma [použití předběžných verzí funkcí z aktualizací](../../servers/manage/install-in-console-updates.md#bkmk_prerelease).

Další informace najdete v tématu sdílená [mezipaměť pro klienty Configuration Manager](../hierarchy/client-peer-cache.md)a [řídicí panel zdrojů dat klienta](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).


## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Migrovat více sdílených distribučních bodů současně
Nyní můžete použít možnost k **opětovnému přiřazení distribučního bodu** , aby Configuration Manager proces souběžně se změnou přiřazení až 50 sdílených distribučních bodů současně. Před touto verzí byly v jednu chvíli zpracovány znovu přiřazené distribuční body. Další informace najdete v tématu [migrace více sdílených distribučních bodů současně](../../migration/planning-a-content-deployment-migration-strategy.md#migrate-multiple-shared-distribution-points-at-the-same-time).

## <a name="cloud-management-gateway-for-managing-internet-based-clients"></a>Brána pro správu cloudu pro správu internetových klientů

Brána pro správu cloudu poskytuje jednoduchý způsob správy Configuration Manager klientů na internetu. Služba Brána pro správu cloudu, která je nasazená do Microsoft Azure a vyžaduje předplatné Azure, se připojí k místní infrastruktuře Configuration Manager pomocí nové role, která se nazývá bod připojení brány pro správu cloudu. Po úplném nasazení a konfiguraci můžou klienti komunikovat s místními Configuration Manager rolí systému lokality a cloudových distribučních bodů bez ohledu na to, jestli jsou připojené k interní privátní síti nebo na internetu. Další informace a informace o tom, jak brána pro správu cloudu porovnává s internetovou správou klientů, najdete v tématu [Správa klientů na internetu](../../clients/manage/manage-clients-internet.md).

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a>Vylepšení zásad upgradu edice Windows 10
V této verzi jsme provedli následující vylepšení tohoto typu zásad:

- Pomocí zásad upgradu edice s počítači s Windows 10, na kterých běží klient Configuration Manager, teď můžete používat i počítače s Windows 10, které jsou zaregistrované v Microsoft Intune.
- Z Windows 10 Professional můžete upgradovat na kteroukoli z platforem v průvodci, které jsou kompatibilní s vaším hardwarem.

## <a name="manage-hardware-identifiers"></a>Správa hardwarových identifikátorů
Teď můžete poskytnout seznam ID hardwaru, který by Configuration Manager měl ignorovat pro účely spouštění pomocí technologie PXE a registrace klienta. Existují dva běžné problémy, které pomáhají vyřešit:

1. Mnoho zařízení, jako je Surface 3, nezahrnuje port připojení k síti Ethernet. Adaptér USB-to-Ethernet se obecně používá k navázání kabelového připojení za účelem nasazení operačního systému. Vzhledem k nákladům a obecné použitelnosti jsou však často sdílené adaptéry. Vzhledem k tomu, že se adresa MAC tohoto adaptéru používá k identifikaci zařízení, se adaptér znovu používá bez dalších akcí správce mezi jednotlivými nasazeními. Nyní ve verzi Configuration Manager 1610 můžete vyloučit adresu MAC tohoto adaptéru, aby bylo možné ho v tomto scénáři snadno použít znovu.
2. ID SMBIOS by mělo být jedinečný identifikátor hardwaru, ale některá z specializovaných hardwarových zařízení jsou sestavená s duplicitními identifikátory. Tento problém nemusí být stejný jako scénář, který je právě popsaný jako scénář USB to-Ethernet Adapter, ale můžete ho vyřešit pomocí seznamu vyloučených ID hardwaru.

Podrobnosti najdete v tématu [Správa duplicitních identifikátorů hardwaru](../../clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers).

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Vylepšení integrace Windows Storu pro firmy s Configuration Manager
Změny v této verzi:
- Dřív jste mohli nasadit jenom bezplatné aplikace z Windows Storu pro firmy. Configuration Manager teď podporuje i nasazení placených online licencovaných aplikací (jenom pro zařízení zaregistrovaná v Intune).
- Nyní můžete zahájit okamžitou synchronizaci mezi Windows Storem pro firmy a Configuration Manager.
- Nyní můžete změnit tajný klíč klienta, který jste získali z Azure Active Directory.
- Předplatné můžete z úložiště odstranit.

Podrobnosti najdete v tématu [Správa aplikací z Windows Storu pro firmy pomocí Configuration Manager](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).


## <a name="policy-sync-for-intune-enrolled-devices"></a>Synchronizace zásad pro zařízení zaregistrovaná v Intune
Teď si můžete vyžádat synchronizaci zásad pro zařízení zaregistrovaná v Intune z konzoly Configuration Manager, abyste nemuseli žádat o synchronizaci z aplikace Portál společnosti na samotném zařízení. Informace o stavu žádosti o synchronizaci jsou k dispozici jako nový sloupec v zobrazeních zařízení nazvaný **stav vzdálené synchronizace**. Informace jsou také k dispozici v části data zjišťování v dialogovém okně **vlastností** pro každé zařízení.


## <a name="use-compliance-settings-to-configure-windows-defender-settings"></a>Použití nastavení dodržování předpisů ke konfiguraci nastavení Windows Defenderu
Teď můžete nakonfigurovat nastavení klienta Windows Defenderu na počítačích s Windows 10 zaregistrovaných v Intune pomocí položek konfigurace v konzole Configuration Manager.
Podrobnosti najdete v části **Windows Defender** v tématu [Vytvoření položek konfigurace pro Windows 8.1 a zařízení s Windows 10 spravovaná bez klienta Configuration Manager](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).



## <a name="general-improvements-to-software-center"></a>Obecná vylepšení centra softwaru
- Uživatelé teď můžou vyžádat aplikace z centra softwaru i z katalogu aplikací.
- Vylepšení, která uživatelům pomůžou pochopit, jaký software je nový a relevantní.

## <a name="new-columns-in-device-collection-views"></a>Nové sloupce v zobrazeních kolekce zařízení
V zobrazeních kolekce zařízení teď můžete zobrazit sloupce pro **IMEI** a **sériové číslo** (pro zařízení s iOS).

## <a name="customizable-branding-for-software-center-dialogs"></a>Přizpůsobitelná značka pro dialogová okna centra softwaru
Vlastní branding pro Centrum softwaru byla představena ve verzi Configuration Manager 1602. Ve verzi 1610 se teď toto branding rozšiřuje na všechna přidružená dialogová okna, aby poskytovala jednotnější prostředí pro uživatele centra softwaru.

Vlastní branding pro Centrum softwaru se používá podle následujících pravidel:

- Pokud není nainstalovaná role serveru lokality bodu webu katalogu aplikací, Centrum softwaru zobrazí název organizace uvedený v klientském nastavení **Počítačový agent** **název organizace zobrazený v centru softwaru**. Pokyny najdete v tématu [Postup konfigurace nastavení klienta](../../clients/deploy/configure-client-settings.md).

- Pokud je nainstalovaná role serveru lokality bodu webu katalogu aplikací, Centrum softwaru zobrazí název organizace a barvu zadanou ve vlastnostech role serveru lokality bodu webu katalogu aplikací. Další informace najdete v tématu [Možnosti konfigurace pro bod webu Katalog aplikací](../../servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).

- Pokud je předplatné Microsoft Intune nakonfigurované a připojené k Configuration Manager prostředí, Centrum softwaru zobrazí název organizace, barvu a logo společnosti zadané ve vlastnostech předplatného Intune.


## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a>Období odkladu vynucování povinného nasazení aplikací a aktualizací softwaru
V některých případech můžete chtít uživatelům poskytnout více času na instalaci požadovaných nasazení aplikací nebo aktualizací softwaru po všech stanovených termínech. To může být například nutné v případě, že počítač byl po delší dobu vypnutý a je potřeba nainstalovat velký počet nasazení aplikace nebo aktualizace. Například pokud se koncový uživatel vrátil jenom z dovolené, může se stát, že budou muset počkat delší dobu, než se nainstalují opožděná nasazení aplikací. Chcete-li tento problém vyřešit, můžete nyní definovat dobu odkladu vynucení nasazením Configuration Manager nastavení klienta do kolekce. 

Pokud chcete nastavit dobu odkladu, proveďte následující akce:
1. Na stránce **Počítačový agent** v nastavení klienta nakonfigurujte **po konečném termínu nasazení (hodiny) novou dobu odkladu** vlastnosti na hodnotu **1** až **120** hodin.
2. V novém požadovaném nasazení aplikace nebo ve vlastnostech stávajícího nasazení na stránce **plánování** zaškrtněte políčko **odložit vynucení tohoto nasazení podle uživatelských předvoleb a až do období odkladu definovaného v nastavení klienta**. Všechna nasazení, která mají toto políčko zaškrtnuto, a jsou zaměřená na zařízení, do kterých jste nasadili také nastavení klienta, bude používat dobu odkladu vynucení.

Pokud nakonfigurujete dobu odkladu vynucení a zaškrtnutím políčka po dosažení konečného termínu instalace aplikace nasadíte do prvního nefiremního okna, které uživatel nakonfigurovali do této lhůty odkladu. Uživatel ale přesto může otevřít Centrum softwaru a nainstalovat aplikaci kdykoli. Jakmile vyprší lhůta odkladu, vynucení se vrátí do normálního chování pro zpožděná nasazení. Podobné možnosti byly přidány do Průvodce nasazením aktualizací softwaru, Průvodce pravidly automatického nasazení a stránky vlastností.



## <a name="improved-functionality-in-dialog-boxes-about-required-software"></a>Vylepšené funkce v dialogových oknech o požadovaném softwaru
Když uživatel obdrží požadovaný software, z nastavení připomenout **a připomenout:** může vybrat z následujícího rozevíracího seznamu hodnot: 
- **Později**. Určuje, že se mají oznámení plánovat na základě nastavení oznámení nakonfigurovaného v nastavení agenta klienta.
- **Pevný čas**. Určuje, že se má u oznámení naplánovat opětovné zobrazení po zvoleném čase (například během 30 minut).

![Stránka Počítačový agent v nastavení agenta klienta](media/client-notification-settings.png)

Maximální doba odložení je založena na hodnotách oznámení konfigurovaných v nastavení agenta klienta. Pokud je například **konečný termín nasazení delší než 24 hodin a nastavení připomenout uživatele každých (hodiny)** na stránce Počítačový agent je nakonfigurováno na 10 hodin a je více než 24 hodin před konečným termínem, uživatel uvidí sadu možností odložení až do 10 hodin. Po dosažení konečného termínu jsou k dispozici méně možností, které jsou konzistentní s příslušnými nastaveními klientského agenta pro každou součást časové osy nasazení.

V případě nasazení s vysokým rizikem, jako je například pořadí úkolů, které nasazuje operační systém, bude uživatelské prostředí upozorňováno nyní výraznější. Místo dočasného oznámení na hlavním panelu se pokaždé, když se uživateli oznámí, že se vyžaduje údržba nejdůležitějšího softwaru, v počítači uživatele se zobrazí dialogové okno, například následující:

![Požadovaný softwarový dialog](media/client-toast-notification.png)


Další informace najdete tady:
- [Nastavení pro správu nasazení s vysokým rizikem](../../servers/manage/settings-to-manage-high-risk-deployments.md)
- [Postup konfigurace nastavení klienta](../../clients/deploy/configure-client-settings.md)

## <a name="software-updates-dashboard"></a>Řídicí panel aktualizace softwaru
Pomocí nového řídicího panelu aktualizace softwaru můžete zobrazit aktuální stav dodržování předpisů u zařízení ve vaší organizaci a rychle analyzovat data a zjistit, která zařízení jsou v ohrožení. Řídicí panel zobrazíte tak, že přejdete na **monitorování**  >  **Přehled**  >  **zabezpečení**  >  **aktualizace softwaru řídicí panel**.

Podrobnosti najdete v tématu [monitorování aktualizací softwaru](../../../sum/deploy-use/monitor-software-updates.md).


## <a name="improvements-to-the-application-request-process"></a>Vylepšení procesu žádosti o aplikace
Po schválení aplikace pro instalaci můžete kliknutím na **Odepřít** v konzole Configuration Manager vybrat možnost Odepřít. Dříve bylo toto tlačítko po schválení zobrazeno šedě.

Tato akce nezpůsobí, že se aplikace odinstaluje z žádného zařízení. Uživatel ale přestane instalovat nové kopie aplikace z centra softwaru.

## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrovat podle velikosti obsahu v pravidlech automatického nasazení
Nyní můžete vyfiltrovat velikost obsahu pro aktualizace softwaru v pravidlech automatického nasazení. Chcete-li například stáhnout pouze aktualizace softwaru, které jsou menší než 2 MB, můžete nastavit filtr **Velikost obsahu (KB)** na **< 2048**. Použití tohoto filtru zabraňuje automatickému stahování velkých aktualizací softwaru, což lépe podporuje zjednodušenou údržbu Windows, pokud je omezená šířka pásma sítě. Podrobnosti najdete tady:
- [Configuration Manager a zjednodušená Údržba Windows na nižší úrovni operačního systému](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configuration-manager-and-simplified-windows-servicing-on-down/ba-p/274056)
- [Automatické nasazení aktualizací softwaru](../../../sum/deploy-use/automatically-deploy-software-updates.md)

Chcete-li nakonfigurovat pole **Velikost obsahu (KB)** , proveďte jednu z následujících akcí:
- Když vytváříte pravidlo automatického nasazení, v Průvodci vytvořením pravidla automatického nasazení přejdete na stránku **aktualizace softwaru** .
- Ve vlastnostech existujícího pravidla automatického nasazení přejdete na kartu **aktualizace softwaru** .

## <a name="office-365-client-management-dashboard"></a>Řídicí panel pro správu klientů Office 365
Řídicí panel pro správu klientů Office 365 je nyní k dispozici v konzole Configuration Manager. Řídicí panel zobrazíte tak, že přejdete do části Přehled **knihovny softwaru**  >  **Overview**  >  **Office 365 Správa klientů**.

Řídicí panel zobrazuje grafy pro následující:

- Počet klientů Office 365
- Verze klientů Office 365
- Jazyky klienta Office 365
- Klientské kanály pro Office 365     

Podrobnosti najdete v tématu [Správa aktualizací Office 365 ProPlus](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

## <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Kroky pořadí úloh pro správu převodu systému BIOS na UEFI
Nyní můžete přizpůsobit pořadí úloh nasazení operačního systému novou proměnnou, TSUEFIDrive, aby krok **restartovat počítač** PŘIPRAVIL oddíl FAT32 na pevném disku pro přechod do rozhraní UEFI. Následující postup popisuje, jak můžete vytvořit kroky pořadí úloh k přípravě pevného disku pro převod systému BIOS na rozhraní UEFI. Podrobnosti najdete v tématu věnovaném [krokům pořadí úkolů ke správě převodu systému BIOS na rozhraní UEFI](../../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md).

##  <a name="improvements-to-the-task-sequence-step-prepare-configmgr-client-for-capture"></a>Vylepšení kroku pořadí úloh: Příprava klienta nástroje ConfigMgr pro zaznamenání  
Krok připravit klienta nástroje ConfigMgr teď zcela odebere klienta Configuration Manager, místo aby se odebraly jenom informace o klíči. Když pořadí úkolů nasadí zachycenou bitovou kopii operačního systému, nainstaluje novou Configuration Manager klienta pokaždé, když bude. Podrobnosti najdete v tématu [kroky pořadí úkolů](../../../osd/understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture).



## <a name="intune-compliance-policy-charts"></a>Grafy zásad dodržování předpisů v Intune
Nyní můžete získat rychlý přehled o celkovém dodržování předpisů pro zařízení a hlavní důvody pro nedodržování předpisů pomocí nových grafů v pracovním prostoru **monitorování** v konzole Configuration Manager. Kliknutím na část v grafu můžete přejít k seznamu zařízení v této kategorii. Podrobnosti najdete v tématu [monitorování zásad dodržování předpisů](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).


## <a name="lookout-integration-for-hybrid-implementations-to-protect-ios-and-android-devices"></a>Prohlédněte si integraci hybridních implementací pro ochranu zařízení s iOS a Androidem.
Microsoft integruje řešení ochrany před mobilními hrozbami z pohledu na ochranu mobilních zařízení s iOS a Androidem, protože na zařízeních detekuje malware, rizikové aplikace a další. Řešení hledání vám pomůže určit úroveň hrozeb, která se dá konfigurovat. Můžete vytvořit pravidlo zásad dodržování předpisů v Configuration Manager k určení dodržování předpisů zařízením na základě posouzení rizik. Pomocí zásad podmíněného přístupu můžete povolit nebo blokovat přístup k prostředkům společnosti na základě stavu dodržování předpisů pro zařízení.

Uživatelům nekompatibilních zařízení s iOS se zobrazí výzva k registraci. Budou se muset nainstalovat Lookout for Work aplikace na jejich zařízení, aktivovat aplikaci a napravit hrozby nahlášené v aplikaci Lookout for Work a získat tak přístup k podnikovým datům.


## <a name="new-compliance-settings-for-configuration-items"></a>Nové nastavení dodržování předpisů pro položky konfigurace
Existuje mnoho nových nastavení, která můžete použít v položkách konfigurace pro různé platformy zařízení. Jedná se o nastavení, která dříve existovala v Microsoft Intune samostatné konfigurace, a jsou teď dostupná, když používáte Intune s Configuration Manager.
Podrobnosti najdete v tématu [položky konfigurace pro zařízení spravovaná bez klienta Configuration Manager](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).

### <a name="new-settings-for-android-devices"></a>Nová nastavení pro zařízení s Androidem
#### <a name="password-settings"></a>Nastavení hesla
- **Pamatovat si historii hesel**
- **Povolit odemknutí otiskem prstu**

#### <a name="security-settings"></a>Nastavení zabezpečení
- **Vyžadovat šifrování u paměťových karet**
- **Povolit snímek obrazovky**
- **Povolit odeslání diagnostických dat**

#### <a name="browser-settings"></a>Nastavení prohlížeče
- **Povolit webový prohlížeč**
- **Povolit automatické vyplňování**
- **Povolit blokování automaticky otevíraných oken**
- **Povolení souborů cookie**
- **Povolit aktivní skriptování**

#### <a name="app-settings"></a>Nastavení aplikace
- **Povolit Google Play Store**

#### <a name="device-capability-settings"></a>Nastavení možností zařízení
- **Povolit vyměnitelné úložiště**
- **Povolit Wi-Fi tethering**
- **Povolit zeměpisnou polohu**
- **Povolit komunikaci NFC**
- **Povolit Bluetooth**
- **Povolit hlasový roaming**
- **Povolit datový roaming**
- **Povolit SMS a MMS zprávy**
- **Povolit hlasového pomocníka**
- **Povolit hlasové vytáčení**
- **Povolit kopírování a vkládání**

### <a name="new-settings-for-ios-devices"></a>Nová nastavení pro zařízení s iOS
#### <a name="password-settings"></a>Nastavení hesla
- **Počet složitých znaků požadovaných v hesle**
- **Povolit jednoduchá hesla**
- **Počet minut nečinnosti před vyžadováním hesla**
- **Pamatovat si historii hesel**

### <a name="new-settings-for-mac-os-x-devices"></a>Nová nastavení pro Mac OS X zařízení
#### <a name="password-settings"></a>Nastavení hesla
- **Počet složitých znaků požadovaných v hesle**
- **Povolit jednoduchá hesla**
- **Pamatovat si historii hesel**
- **Počet minut nečinnosti před aktivací šetřiče obrazovky**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Nová nastavení pro zařízení s Windows 10 Desktop a Mobile
#### <a name="password-settings"></a>Nastavení hesla
- **Minimální počet znakových sad**
- **Pamatovat si historii hesel**
- **Po návratu zařízení ze stavu nečinnosti vyžadovat heslo**

#### <a name="security-settings"></a>Nastavení zabezpečení
- **Vyžadovat šifrování u mobilního zařízení**
- **Povolit manuální zrušení zápisu**

#### <a name="device-capability-settings"></a>Nastavení možností zařízení
- **Povolit VPN v mobilní síti**
- **Povolit VPN v mobilní síti v roamingu**
- **Povolit obnovení továrního nastavení telefonu**
- **Povolit připojení USB**
- **Povolit Cortanu**
- **Povolit oznámení centra akcí**

### <a name="new-settings-for-windows-10-team-devices"></a>Nová nastavení pro zařízení s Windows 10 Team
#### <a name="device-settings"></a>Nastavení zařízení
- **Povolit Azure Operational Insights**
- **Povolit bezdrátové připojení Miracast**
- **Zvolit informace o schůzce zobrazené na úvodní obrazovce**
- **Adresa URL obrázku pozadí zamykací obrazovky**

### <a name="new-settings-for-windows-81-devices"></a>Nová nastavení pro Windows 8.1 zařízení
#### <a name="applicability-settings"></a>Nastavení použitelnosti
- **Použít všechny konfigurace ve Windows 10**

#### <a name="password-settings"></a>Nastavení hesla
- **Vyžadovaný typ hesla**
- **Minimální počet znakových sad**
- **Minimální délka hesla**
- **Počet povolených opakovaných neúspěšných přihlášení, než bude zařízení vymazáno**
- **Počet minut nečinnosti před vypnutím displeje**
- **Vypršení platnosti hesla (dny)**
- **Pamatovat si historii hesel**
- **Znemožnit opakované použití předchozích hesel**
- **Povolit obrázkové heslo a PIN**

#### <a name="browser-settings"></a>Nastavení prohlížeče
- **Povolit automatické zjišťování intranetové sítě**

### <a name="new-settings-for-windows-phone-81-devices"></a>Nová nastavení pro zařízení Windows Phone 8,1
#### <a name="applicability-settings"></a>Nastavení použitelnosti
- **Použít všechny konfigurace ve Windows 10**

#### <a name="password-settings"></a>Nastavení hesla
- **Minimální počet znakových sad**
- **Povolit jednoduchá hesla**
- **Pamatovat si historii hesel**

#### <a name="device-capability-settings"></a>Nastavení možností zařízení
- **Povolit automatické připojení k bezplatným Wi-Fi hotspotům**
