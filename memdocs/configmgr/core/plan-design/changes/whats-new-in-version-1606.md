---
title: Novinka ve verzi 1606
titleSuffix: Configuration Manager
description: Získejte podrobnosti o změnách a nových funkcích zavedených ve verzi 1606 Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: df2e57b9-6445-4067-98e7-ace85d4e6aa6
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 2fa46770adfbf3e688bbdc561d8193967f3913cd
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698584"
---
# <a name="what39s-new-in-version-1606-of-configuration-manager"></a>Co&#39;s novinkou ve verzi 1606 Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Aktualizace 1606 pro Configuration Manager je k dispozici jako aktualizace konzoly pro dříve nainstalované lokality, na kterých běží verze 1511 nebo 1602. Verze 1511 je počáteční základní verze, kterou použijete k instalaci nových lokalit Configuration Manager.
> [!TIP]  
> Přečtěte si další informace:  
>   
> - [Instalace nových lokalit](../../servers/deploy/install/prepare-to-install-sites.md) (pomocí základní verze, jako je 1511)  
> - [Instalace aktualizací v lokalitách](../../servers/manage/updates.md) (například aktualizace 1602 nebo 1606)  

 Následující části obsahují podrobné informace o změnách a nových funkcích, které jsou představené ve verzi 1606 Configuration Manager.  



## <a name="updates-and-servicing"></a><a name="updatesandservicing"></a>Aktualizace a údržba

### <a name="changes-for-the-updates-and-servicing-node"></a>Změny pro uzel aktualizace a údržba
Níže jsou uvedené změny v uzlu aktualizace a údržba v konzole Configuration Manager:
> [!NOTE]
> Tyto změny nejsou k dispozici, dokud nenainstalujete verzi 1606.

- **Změna názvu uzlu:**

    V pracovním prostoru **sledování** byl uzel **stav údržby lokality** přejmenován na **stav aktualizace a údržba**.
- **Podrobnosti o dalších stavech instalace:**

    Po zobrazení stavu instalace aktualizace lokality teď konzola zobrazuje samostatné podrobnosti pro následující akce:
    - **Stáhnout** (vztahuje se jenom na lokalitu na nejvyšší úrovni, kde je nainstalovaná role systému lokality spojovacího bodu služby.)
    - **Replikace**
    - **Kontrola předpokladů**
    - **Instalace**

  K dispozici jsou teď podrobnější informace pro každý krok, včetně toho, který soubor protokolu si můžete zobrazit a kde najdete další informace.  
-   **Nová možnost pro opakování neúspěšných požadavků:**

    V pracovních prostorech **Správa** a **monitorování** obsahuje uzel **aktualizace a údržba** na pásu karet nové tlačítko s názvem **Ignorovat upozornění na předpoklady**.

    Při instalaci aktualizací bez použití možnosti ignorovat upozornění na předpoklady (v rámci průvodce aktualizacemi) a aktualizace, která se zastaví z důvodu upozornění, můžete na pásu karet vybrat **Ignorovat upozornění na předpoklady** . Tím se aktivuje automatické pokračování instalace aktualizace.  



- **Zobrazení čisticích aktualizací:**

    V uzlu **aktualizace a údržba** se nyní zobrazí pouze poslední nainstalovaná aktualizace a všechny nové aktualizace, které jsou k dispozici pro instalaci. Chcete-li zobrazit dříve nainstalované aktualizace, klikněte na tlačítko nové **Historie** , které se zobrazí na pásu karet.  

-   **Přejmenovaná možnost pro předprodukční:**

    V uzlu **aktualizace a údržba** se teď tlačítko **Možnosti klienta** označuje jako **zvýšení úrovně předem produkčního klienta**.


###  <a name="pre-release-features"></a>Předběžné verze funkcí
Od verze 1606 musíte udělit souhlas s používáním předběžných verzí funkcí v Configuration Manager, abyste mohli vybrat a povolit jejich použití. Další informace najdete v tématu [Použití předběžných verzí funkcí z aktualizací](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="new-distribution-point-update-behavior"></a>Nové chování aktualizace distribučního bodu
Aktualizace 1606 zavádí změny, které zlepšují dostupnost distribučních bodů při instalaci budoucích aktualizací.

Když je nainstalovaná aktualizace 1606, při další instalaci aktualizace v této lokalitě, která vyžaduje automatickou přeinstalaci rolí systému lokality standardní a distribučního bodu pro vyžádání obsahu, už nejsou všechny distribuční body offline, aby se aktualizovaly ve stejnou dobu. Místo toho server lokality používá nastavení distribuce obsahu lokality k distribuci aktualizace do podmnožiny distribučních bodů v daném čase. Výsledkem je, že pouze některé distribuční body jsou offline, aby se aktualizace nainstalovala. To umožňuje distribučním bodům, které se ještě nezačaly aktualizovat, nebo které aktualizaci dokončily, aby zůstaly online a bylo možné poskytovat obsah klientům.



## <a name="accessibility"></a><a name="accessibility"></a> Přístup
Pro procházení různých uzlů pracovního prostoru teď můžete zadat první písmeno názvu uzlu. Každé stisknutí klávesy přesune kurzor na další uzel, který začíná písmenem. Pro uživatele, kteří mají čtečku obrazovky, čtecí modul přečte název tohoto uzlu. Další informace o možnostech usnadnění najdete v tématu [funkce usnadnění](../../../core/understand/accessibility-features.md).

## <a name="administration"></a><a name="administration"></a>Správa
Níže jsou uvedené změny správy v konzole Configuration Manager:
### <a name="oms-connector"></a>Konektor OMS

Nyní se můžete připojit Configuration Manager jako kolekce z Configuration Manager k [Microsoft Operations Management Suite (OMS)](/azure/azure-monitor/overview). Tím se data, jako jsou kolekce z nasazení Configuration Manager, zobrazují v OMS. Další informace najdete v tématu [synchronizace dat z Configuration Manager do Microsoft Operations Management Suite](/azure/azure-monitor/platform/collect-sccm).

Konektor OMS je předběžnou verzí funkce. Pokud ho chcete povolit, přečtěte si téma [použití předběžných verzí funkcí z aktualizací](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="support-for-cache-size-in-client-settings"></a>Podpora velikosti mezipaměti v nastavení klienta

Velikost složky mezipaměti v klientských počítačích teď můžete nakonfigurovat pomocí **nastavení klienta** v konzole Configuration Manager. Dřív jste mohli nastavit velikost mezipaměti klienta jenom při instalaci nebo přeinstalaci klientského softwaru. Nyní můžete zadat velikost mezipaměti jako nastavení klienta (výchozí nebo vlastní) a pak tato nastavení použít při další aktualizaci zásad na klientovi, aniž by bylo nutné přeinstalovat klienta. Další informace najdete v tématu [Konfigurace mezipaměti klienta pro klienty nástroje Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache).

## <a name="on-premises-mobile-device-management"></a>Místní správa mobilních zařízení

### <a name="support-for-multiple-device-management-points"></a>Podpora více bodů správy zařízení

Místní správa mobilních zařízení (MDM) nyní podporuje novou funkci v rámci aktualizace pro Windows 10, která automaticky konfiguruje zaregistrované zařízení tak, aby bylo možné používat více než jeden bod správy zařízení. Tato funkce umožňuje, aby se zařízení vrátilo do jiného bodu správy zařízení, když není k dispozici ten, který běžně používá. Tato možnost funguje jenom pro počítače a zařízení s nainstalovanou aktualizací Windows 10 pro výročí.


## <a name="application-management"></a>Správa aplikací

### <a name="manage-apps-from-the-windows-store-for-business"></a>Správa aplikací z Windows Storu pro firmy

[Windows Store pro firmy](https://www.microsoft.com/business-store) je místo, kde můžete najít a koupit aplikace pro Windows pro vaši organizaci, a to buď jednotlivě, nebo ve svazku. Připojením úložiště k Configuration Manager můžete synchronizovat seznam aplikací, které jste zakoupili v Configuration Manager, zobrazit je v konzole Configuration Manager a nasazovat je stejně jako jakékoli jiné aplikace.

Podrobnosti najdete v tématu [Správa aplikací z Windows Storu pro firmy pomocí Configuration Manager](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### <a name="manage-ios-volume-purchased-apps"></a>Správa hromadně zakoupených aplikací iOS

Byl vylepšen pracovní postup pro správu hromadně zakoupených aplikací pro iOS a jejich nasazování pomocí Configuration Manager.


### <a name="software-center-user-interface"></a>Uživatelské rozhraní centra softwaru

Uživatelské rozhraní centra softwaru bylo zjednodušeno pro snazší zjišťování.
*  **Stav instalace** a **nainstalované karty softwaru** byly sloučeny do jedné karty **stav instalace** .
*  **Aktualizace**, **operační systémy**a **aplikace** byly rozdělené na tři samostatné karty.
* Pro instalaci teď můžete vybrat víc aktualizací, nebo můžete všechny aktualizace nainstalovat najednou kliknutím na **instalovat vše**.

### <a name="content-status-links"></a>Odkazy na stav obsahu
Ve vlastnostech aplikace nebo balíčku je nyní odkaz, který vás přesměruje na stav tohoto objektu.

## <a name="software-updates"></a>Aktualizace softwaru

### <a name="client-setting-to-manage-the-office-365-client-agent"></a>Nastavení klienta pro správu agenta klienta Office 365
Nyní můžete použít nastavení klienta Configuration Manager ke správě klientského agenta Office 365. Po nastavení a nasazení aktualizací Office 365 funguje agent Configuration Manager klienta s agentem klienta Office 365 ke stažení a instalaci aktualizací Office 365 z distribučního bodu.

Podrobnosti najdete v tématu [Správa aktualizací Office 365 ProPlus pomocí Configuration Manager](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="manually-switch-clients-to-a-new-software-update-point"></a>Ruční přepnutí klientů na nový bod aktualizace softwaru
Nyní můžete povolit možnost, která umožňuje klientům Configuration Manager přepnout na nový bod aktualizace softwaru v případě problémů s aktivním bodem aktualizace softwaru. Jakmile je možnost povolená, klienti budou během příštího vyhledávání hledat jiný bod aktualizace softwaru.

Podrobnosti najdete v tématu [Plánování aktualizací softwaru v Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs).

### <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a>Možnosti restartování klientů s Windows 10 po instalaci aktualizací softwaru
Když je aktualizace softwaru, která vyžaduje restart, nasazená pomocí Configuration Manager a je nainstalovaná na počítači, naplánuje se restartování na více počítačů. Zobrazí se také dialogové okno restartovat. Od verze Configuration Manager 1606 jsou k dispozici možnosti **aktualizovat a restartovat** a **aktualizovat a vypnout** , pokud je pro Configuration Manager aktualizace softwaru čeká na restartování. Tyto možnosti jsou k dispozici v možnostech napájení systému Windows na počítačích s Windows 10. Po použití jedné z těchto možností se dialogové okno restartovat po restartování počítače nezobrazí.

Podrobnosti najdete v tématu [Plánování aktualizací softwaru](../../../sum/plan-design/plan-for-software-updates.md#BKMK_RestartOptions).

### <a name="run-software-updates-compliance-scan-immediately-after-a-client-installs-software-updates-and-restarts"></a>Spustit kontrolu kompatibility aktualizací softwaru ihned po instalaci aktualizací softwaru a restartováním klienta
Nyní můžete spustit kontrolu dodržování předpisů hned poté, co klient nainstaluje aktualizace softwaru a restartuje se. Chcete-li nastavit toto nasazení, na stránce **činnost koncového uživatele** v Průvodci nasazením aktualizace softwaru vyberte možnost **Pokud nějaká aktualizace v tomto nasazení vyžaduje restart systému, po restartu spusťte zkušební cyklus nasazení aktualizací**. To umožňuje klientovi vyhledat další aktualizace softwaru, které se projeví po restartování klienta, a pak je nainstalovat (a kompatibilní) během stejného časového období údržby. Podrobnosti najdete v tématu [automatické nasazení aktualizací softwaru](../../../sum/deploy-use/automatically-deploy-software-updates.md) nebo [Ruční nasazení aktualizací softwaru](../../../sum/deploy-use/manually-deploy-software-updates.md).

## <a name="operating-system-deployment"></a>Nasazení operačního systému

### <a name="improvements-to-the-task-sequence-step-install-software-updates"></a>Vylepšení kroku pořadí úkolů: instalovat aktualizace softwaru
Nové nastavení, **vyhodnoťte aktualizace softwaru z výsledků kontroly uložené v mezipaměti**, nabízí možnost provést úplnou kontrolu aktualizací softwaru namísto použití výsledků kontroly v mezipaměti. Podrobnosti najdete v tématu [kroky pořadí úkolů](../../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates).

K dispozici je také nová proměnná pořadí úloh **SMSTSSoftwareUpdateScanTimeout**. Tato proměnná vám umožní řídit časový limit kontroly aktualizací softwaru během kroku pořadí úkolů instalovat aktualizace softwaru. Výchozí hodnota je 30 minut. Podrobnosti najdete v tématu [předdefinované proměnné pořadí úkolů](../../../osd/understand/task-sequence-variables.md).

### <a name="osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a>Proměnná pořadí úloh OSDPreserveDriveLetter je zastaralá.
Proměnná pořadí úloh OSDPreserveDriveLetter je zastaralá. Počínaje verzí 1606 Configuration Manager instalační program systému Windows určuje nejvhodnější písmeno jednotky, které se má použít (obvykle C:). ve výchozím nastavení se při nasazení operačního systému používá.

Podrobnosti najdete v tématu [předdefinované proměnné pořadí úkolů](../../../osd/understand/task-sequence-variables.md).

### <a name="customize-the-ramdisk-tftp-window-size-for-pxe-enabled-distribution-points"></a>Přizpůsobení velikosti okna TFTP disku paměti RAM pro distribuční body s povoleným PXE
Nyní můžete přizpůsobit velikost okna disku RAM pro distribuční body s povoleným PXE. Pokud jste vaši síť přizpůsobili, může to způsobit, že se stažení spouštěcí image nezdaří s chybou vypršení časového limitu, protože velikost okna je příliš velká. Přizpůsobení velikosti okna disku RAM triviální protokol FTP (File Transfer Protocol) (TFTP) umožňuje optimalizovat přenosy TFTP při použití technologie PXE pro splnění konkrétních požadavků na síť.

Podrobnosti najdete v tématu [Příprava rolí systému lokality pro nasazení operačního systému pomocí Configuration Manager](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="compliance-settings"></a>Nastavení dodržování předpisů

### <a name="smart-lock-setting-for-android-devices"></a>Nastavení Smart Lock pro zařízení s Androidem
Do položky konfigurace Android a Samsung KNOX Standard se přidalo nové nastavení, **povolí Smart Lock a jiné agenty**pro určování důvěryhodnosti.

Toto nastavení umožňuje řídit funkci Smart Lock na kompatibilních zařízeních s Androidem. Tato funkce telefonu, někdy označovaná jako "agenti pro určování důvěryhodnosti", umožňuje zakázat nebo obejít heslo uzamčené obrazovky zařízení, pokud se zařízení nachází v důvěryhodném umístění. Například důvěryhodné umístění může být, pokud je připojené k určitému zařízení Bluetooth nebo když se nachází blízko značky NFC. Pomocí tohoto nastavení můžete uživatelům zabránit v konfiguraci funkce Smart Lock.


## <a name="device-configuration-and-protection"></a>Konfigurace a ochrana zařízení

### <a name="product-name-changes"></a>Změny názvu produktu

* Microsoft Passport for Work se teď označuje jako **Windows Hello pro firmy**.
* Ochrana podnikových dat se nyní označuje jako **Windows Information Protection**.

### <a name="deployment-of-windows-hello-for-business-passport-for-work"></a>Nasazení Windows Hello pro firmy (Passport for Work)

Zásady Windows Hello pro firmy teď můžete nasadit na zařízení s Windows 10 připojená k doméně, která spravuje klient Configuration Manager.

Konzola Configuration Manager se aktualizovala tak, aby odrážela tyto změny.

### <a name="ios-activation-lock"></a>Zámek aktivace pro iOS
Configuration Manager vám může pomáhat spravovat Zámek aktivace pro iOS, což je funkce aplikace Najít iPhone pro zařízení s iOS 7,1 a novějším. Když je zámek aktivace povolený, musí se zadat Apple ID a heslo uživatele, aby bylo možné:
* Vypnout funkci Najít iPhone
* Vymaže zařízení.
* Znovu aktivujte zařízení.

Nástroj Configuration Manager vám může pomoci se správou zámku aktivace dvěma způsoby:

- Povolením zámku aktivace na zařízeních pod dohledem.
- Obejitím zámku aktivace na zařízeních pod dohledem.


### <a name="microsoft-defender-advanced-threat-protection"></a>Rozšířená ochrana před internetovými útoky v programu Microsoft Defender

Endpoint Protection může pomáhat spravovat a monitorovat rozšířenou ochranu před internetovými útoky v programu Microsoft Defender (ATP). Microsoft Defender ATP je nová služba, která podnikům pomůže odhalit, prozkoumat a reagovat na pokročilé útoky v jejich sítích. Zásady Configuration Manager vám můžou pomáhat s připojováním a monitorováním spravovaných počítačů se systémem Windows 10 verze 1607 (Build 14328) nebo novějším.

Podrobnosti najdete v tématu [Rozšířená ochrana před internetovými útoky v programu Microsoft Defender](../../../protect/deploy-use/defender-advanced-threat-protection.md).

### <a name="device-categories"></a>Kategorie zařízení
Můžete vytvořit kategorie zařízení, které se dají použít k automatickému umísťování zařízení do kolekcí zařízení, když používáte Configuration Manager s Microsoft Intune. Uživatelé pak při registraci zařízení v Intune potřebují zvolit kategorii zařízení. Kategorii zařízení můžete také změnit z konzoly Configuration Manager.

Podrobnosti najdete v tématu [Postup automatické kategorizace zařízení do kolekcí pomocí Configuration Manager](../../../core/clients/manage/collections/automatically-categorize-devices-into-collections.md).

### <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Předdeklarace zařízení pomocí sériového čísla IMEI nebo iOS

Zařízení vlastněná společností můžete identifikovat importem jejich mezinárodních čísel IMEI (Mobile Equipment Identity) nebo sériových čísel iOS. Můžete nahrát textový soubor s oddělovači (. csv), který obsahuje čísla zařízení IMEI, nebo můžete ručně zadat informace o zařízení. Importované informace nastaví vlastnictví zařízení, která se v seznamech zařízení registrují jako "firemní". Pro každého uživatele, který přistupuje ke službě, se stále vyžaduje licence Intune.

### <a name="on-premises-health-attestation-service-communication"></a>Komunikace s místními službami ověření stavu

Teď můžete povolit monitorování služby Health Attestation pro počítače s Windows 10 jenom pomocí místní infrastruktury, aby počítače bez přístupu k Internetu mohly nahlásit Ověření stavu zařízení (DHA).

Podrobnosti najdete v tématu [ověření stavu pro Configuration Manager](../../../core/servers/manage/health-attestation.md#how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers).  

## <a name="remote-control"></a>Vzdálené řízení
Umožněte uživatelům, aby přijali nebo odepřeli přenos souborů před přenosem obsahu ze sdílené schránky v relaci vzdáleného řízení. Uživatelé potřebují udělit oprávnění pouze jednou pro každou relaci a prohlížeč nemá možnost udělit oprávnění k pokračování v přenosu souborů. Toto nové nastavení najdete v pracovním prostoru **Správa** . Přejít na **nastavení klienta**a pak ve **výchozím nastavení**otevřete panel **nástrojů Remote Tools** .