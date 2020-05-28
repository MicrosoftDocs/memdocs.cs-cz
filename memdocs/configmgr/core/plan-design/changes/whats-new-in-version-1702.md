---
title: Nová verze 1702
titleSuffix: Configuration Manager
description: Získejte podrobnosti o změnách a nových funkcích zavedených ve verzi 1702 Configuration Manager.
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: eacf64245f4cfc779dc92be73e8d7e387b34f909
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427940"
---
# <a name="what39s-new-in-version-1702-of-configuration-manager"></a>Co&#39;s novinkou ve verzi 1702 Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Aktualizace 1702 pro Configuration Manager aktuální větev je k dispozici jako aktualizace konzoly pro dříve nainstalované lokality, na kterých běží verze 1602, 1606 nebo 1610. Je také k dispozici jako základní verze, kterou můžete použít při instalaci nového nasazení.

> [!TIP]  
> Chcete-li nainstalovat novou lokalitu, je nutné použít základní verzi Configuration Manager.  
>
> Další informace:    
> - [Instalace nových lokalit](../../servers/deploy/install/installing-sites.md)  
> - [Instalace aktualizací v lokalitách](../../servers/manage/updates.md)  
> - [Základní a aktualizační verze](../../servers/manage/updates.md#bkmk_Baselines)

Následující části obsahují podrobné informace o změnách a nových funkcích, které jsou představené ve verzi 1702 Configuration Manager.  

## <a name="deprecated-features-and-operating-systems"></a>Zastaralé funkce a operační systémy
Přečtěte si o změnách podpory před jejich implementací v [odebraných a zastaralých položkách](deprecated/removed-and-deprecated.md).

Verze 1702 vyřazuje podporu pro následující produkty:
- **SQL Server 2008 R2**pro databázové servery lokality. Vyřazení podpory bylo [poprvé oznámeno](deprecated/removed-and-deprecated-server.md#sql-server) 10. července 2015. Tato verze SQL Server zůstane podporovaná, když použijete Configuration Manager verzi starší než verze 1702.
- **Windows Server 2008 R2**pro servery systému lokality a většinu rolí systému lokality. Vyřazení podpory bylo [poprvé oznámeno](deprecated/removed-and-deprecated-server.md#server-os) 10. července 2015. Tato verze Windows zůstane podporovaná, když použijete Configuration Manager verzi před verzí 1702.  
- **Windows Server 2008**pro servery systému lokality a většinu rolí systému lokality. Vyřazení podpory bylo [poprvé oznámeno](deprecated/removed-and-deprecated-server.md#server-os) 10. července 2015.
- **Windows XP Embedded**jako klientský operační systém. Vyřazení bylo [poprvé oznámeno](deprecated/removed-and-deprecated-client.md#deprecated-client-operating-systems) 10. července 2015. Tato verze Windows zůstane podporovaná, když použijete Configuration Manager verzi před verzí 1702.




## <a name="site-infrastructure"></a>Infrastruktura webu

### <a name="improvements-for-in-console-search"></a>Vylepšení vyhledávání v konzole
Níže najdete vylepšení použití vyhledávání v konzole Configuration Manager:
- **Cesta k objektu:**  
  Řada objektů nyní podporuje sloupec s názvem **cesta k objektu**.  Při hledání a zahrnutí tohoto sloupce do výsledků zobrazení můžete zobrazit cestu k jednotlivým objektům. Například pokud spustíte hledání aplikací v uzlu aplikace a také prohledáváte v poduzlech, sloupec *cesta objektu* v podokně výsledků zobrazí cestu k jednotlivým vráceným objektům.   

- **Zachování hledaného textu:**  
  Když zadáte text do textového pole Hledat a potom převedete mezi hledáním poduzlu a aktuálního uzlu, text, který zadáte, bude nyní zachován a zůstane dostupný pro nové hledání bez nutnosti jeho opětovného zadání.

- **Zachování vašeho rozhodnutí pro hledání poduzlů:**  
  Možnost, kterou zvolíte pro hledání *aktuálního uzlu* nebo *všech podřízených uzlů* , nyní přetrvává při změně uzlu, ve kterém pracujete. Toto nové chování znamená, že při přesunu kolem konzoly nemusíte toto rozhodnutí neustále obnovovat. Ve výchozím nastavení, když otevřete konzolu, možnost bude hledat pouze aktuální uzel.


### <a name="send-feedback-from-the-configuration-manager-console"></a>Odeslat názor z konzoly Configuration Manager

Můžete použít možnosti zpětné vazby z konzoly k odeslání zpětné vazby přímo vývojovému týmu.

Můžete najít možnost **zpětné vazby** :
- Na pásu karet úplně vlevo od karty Domů každého uzlu.  
  ![Pásem](./media/feedback-home.png)

- Když kliknete pravým tlačítkem na libovolný objekt v konzole nástroje.   
   ![Righ – možnost kliknutí](./media/feedback-option.png)   

  Zvolení **zpětné vazby** otevře váš prohlížeč na [webu Configuration Manager na webu pro odeslání názoru na web UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas).


###  <a name="changes-for-updates-and-servicing"></a>Změny aktualizací a údržby
Níže jsou uvedené změny pro aktualizace a údržbu:

- **Umístění uzlu**   
  Po instalaci verze 1702 se uzel **aktualizace a údržba** zobrazí jako uzel nejvyšší úrovně v části **Správa**. Již není podřízeným uzlem **Cloud Services**.

- **Nové stavy aktualizace**  
  Když zobrazíte dostupné aktualizace v konzole nástroje, existují dva nové stavy:  
  - **K dispozici pro instalaci** – jedná se o aktualizaci, která byla stažena a připravena k instalaci.
  - **Připraveno ke stažení** – Tato aktualizace je k dispozici, ale nebyla stažena. Tuto aktualizaci si můžete stáhnout, ale ta byla nahrazena novější aktualizací.


- **Jednodušší možnosti aktualizace**  
  Až bude vaše infrastruktura u dvou nebo více aktualizací vyhodnocena, stáhne se pouze nejnovější aktualizace. Pokud je například vaše aktuální verze lokality dvě nebo víc starší než nejnovější verze, která je k dispozici, automaticky se stáhne pouze nejnovější verze aktualizace.  

  Můžete si stáhnout a nainstalovat i další dostupné aktualizace, i když nejsou aktuální verze. Pokud stáhnete starší aktualizaci, zobrazí se upozornění, že byla aktualizace nahrazena novějším. Chcete-li stáhnout aktualizaci, která je *k dispozici ke stažení*, vyberte aktualizaci v konzole nástroje a klikněte na tlačítko **Stáhnout**.

- **Vylepšené vyčištění starších aktualizací**   
  Přidali jsme funkci automatického vyčištění, která odstraní nepotřebné soubory ke stažení ze složky EasySetupPayload na vašem serveru lokality. Vzhledem k tomu, že se jedná o verzi 1702, vyčištění začne fungovat po instalaci následné aktualizace, jako je kumulativní aktualizace nebo verze budoucí aktualizace.  


### <a name="data-warehouse-service-point"></a>Bod služby datového skladu
Pomocí bodu služby datového skladu můžete ukládat a vykazovat dlouhodobá historická data pro nasazení Configuration Manager.

Datový sklad podporuje až 2 TB dat s časovými razítky pro sledování změn. Úložiště dat je zajištěno automatickými synchronizacemi z databáze Configuration Manager lokality do databáze datového skladu. Tyto informace jsou pak přístupné z vašeho bodu služby Reporting Services.

Další informace najdete v [bodu služby datového skladu](../../servers/manage/data-warehouse.md).


### <a name="peer-cache-improvements"></a>Vylepšení sdílené mezipaměti
Od verze 1702 bude zdrojový počítač sdílené mezipaměti zamítnout žádost o obsah, když zdrojový počítač sdílené mezipaměti splňuje některé z následujících podmínek:  
-  Je v režimu nízké baterie.
-  Zatížení procesoru překračuje 80% v době, kdy je požadován obsah.
-  Vstup/výstup disku má *AvgDiskQueueLength* , který překračuje 10.
-  K počítači nejsou k dispozici žádná další připojení.   
Další informace najdete v tématu **omezený přístup ke zdroji sdílené mezipaměti** v [sdílené mezipaměti pro klienty Configuration Manager](../hierarchy/client-peer-cache.md).   

Do vašeho bodu generování sestav se navíc přidají tři nové sestavy. Tyto sestavy můžete použít k pochopení dalších podrobností o zamítnutých požadavcích na obsah, včetně toho, kterou skupinu hranic, počítač a obsah zahrnovali. Viz téma [monitorování](../hierarchy/client-peer-cache.md#monitoring) v rámci sdílené mezipaměti.

### <a name="content-library-cleanup-tool"></a>Content Library Cleanup Tool
Nástroj pro [Vyčištění knihovny obsahu](../hierarchy/content-library-cleanup-tool.md) použijte k odebrání obsahu z distribučních bodů, když tento obsah již není přidružen k aplikaci.


### <a name="use-the-oms-connector-with-the-azure-government-cloud"></a>Použití konektoru OMS s Azure Governmentm cloudem
Konektor OMS můžete použít pro připojení k OMS Log Analytics v Microsoft Azure Government cloudu. To vyžaduje, abyste před instalací konektoru OMS upravili konfigurační soubor, aby konektor mohl pracovat s cloudem pro státní správu. Další informace najdete v tématu [použití konektoru OMS s Azure Governmentm cloudem](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm).

### <a name="software-update-points-are-added-to-boundary-groups"></a>Body aktualizace softwaru se přidají do skupin hranic.
Počínaje verzí 1702 používají klienti skupiny hranic k nalezení nového bodu aktualizace softwaru, k zálohování a hledání nového bodu aktualizace softwaru, pokud už jejich stávající bod aktualizace není dostupný. Jednotlivé body aktualizace softwaru můžete přidat do různých skupin hranic, abyste mohli řídit, které servery může klient najít. Další informace najdete v tématu [body aktualizace softwaru](../../servers/deploy/configure/boundary-groups.md#software-update-points) v tématu [Konfigurace skupin hranic](../../servers/deploy/configure/boundary-groups.md) .


<!-- ## Migration  -->

<!-- ## Client management  -->

## <a name="compliance-settings"></a>Nastavení dodržování předpisů

### <a name="new-compliance-settings-for-ios"></a>Nové nastavení dodržování předpisů pro iOS

Přidali jsme spoustu nových nastavení pro zařízení s iOS, aby odpovídala dostupným Microsoft Intune.


## <a name="application-management"></a>Správa aplikací

### <a name="improved-support-for-windows-store-for-business-apps"></a>Vylepšená podpora pro aplikace Windows Store pro firmy

Nyní můžete nasadit licencované aplikace online z Windows Storu pro firmy do počítačů s Windows 10, které spravujete pomocí klienta Configuration Manager.
Další informace najdete v tématu [Správa aplikací z Windows Storu pro firmy](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### <a name="check-for-running-executable-files-before-installing-an-application"></a>Kontrolovat spouštění spustitelných souborů před instalací aplikace

V dialogovém okně **vlastnosti** typu nasazení můžete na kartě **chování při instalaci** zadat jeden z více spustitelných souborů, které při spuštění zablokují instalaci typu nasazení. Předtím, než bude možné nainstalovat typ nasazení, musí uživatel zavřít běžící spustitelný soubor (nebo ho lze zavřít automaticky pro nasazení s účelem požadované).

Pokud byla aplikace nasazená jako **dostupná**a koncový uživatel se pokusí nainstalovat aplikaci, zobrazí se výzva k zavření všech spuštěných spustitelných souborů, které jste zadali předtím, než budou moci pokračovat v instalaci.

Pokud byla aplikace nasazena jako **povinná**a možnost **automaticky zavře všechny spuštěné spustitelné soubory, které jste zadali na kartě chování při instalaci v dialogovém okně vlastnosti typu nasazení** , zobrazí se dialogové okno, které je informuje o tom, že spustitelné soubory, které jste zadali, budou automaticky uzavřeny po dosažení konečného termínu instalace aplikace.

### <a name="app-management-improvements-for-hybrid-mdm"></a>Vylepšení správy aplikací pro hybridní MDM

- [Nasazení hromadně zakoupených aplikací pro iOS do kolekcí zařízení](#deploy-volume-purchased-ios-apps-to-device-collections)
- [Podpora programu Volume purchase program pro iOS pro vzdělávání](#support-for-ios-volume-purchase-program-for-education)
- [Podpora více tokenů programu Volume purchase program](#support-for-multiple-volume-purchase-program-tokens)


## <a name="operating-system-deployment"></a>Nasazení operačního systému

### <a name="expire-stand-alone-media"></a>Vypršení platnosti samostatného média
Při vytváření samostatných médií jsou k dispozici nové možnosti nastavení volitelného data zahájení a vypršení platnosti média. Tato nastavení jsou ve výchozím nastavení zakázaná. Data jsou porovnána se systémovým časem v počítači před spuštěním samostatného média. Pokud je systémový čas dřívější než čas spuštění nebo pozdější než čas vypršení platnosti, nebude samostatné médium spuštěno. Tyto možnosti jsou dostupné taky pomocí rutiny New-CMStandaloneMedia prostředí PowerShell. Podrobnosti najdete v tématu [vytvoření samostatného média](../../../osd/deploy-use/create-stand-alone-media.md).

### <a name="package-id-displayed-in-task-sequence-steps"></a>ID balíčku zobrazené v krocích pořadí úloh
Libovolný krok pořadí úkolů, který odkazuje na balíček, balíček ovladačů, bitovou kopii operačního systému, spouštěcí bitovou kopii nebo balíček s upgradem operačního systému, zobrazí nyní ID balíčku odkazovaného objektu. Když krok pořadí úkolů odkazuje na aplikaci, zobrazí se ID objektu.

### <a name="support-for-additional-content-in-stand-alone-media"></a>Podpora dalšího obsahu v samostatném médiu
Další obsah se teď podporuje v samostatném médiu. Můžete vybrat další balíčky, balíčky ovladačů a aplikace, které mají být připravené na médiu, spolu s dalším obsahem, na který je odkazováno v pořadí úkolů. Dříve byl na samostatném médiu připraven pouze obsah odkazovaný v pořadí úkolů. Podrobnosti najdete v tématu [vytvoření samostatného média](../../../osd/deploy-use/create-stand-alone-media.md).

### <a name="hardware-inventory-collects-uefi-information"></a>Inventář hardwaru shromažďuje informace o rozhraní UEFI.
K dispozici je nová třída inventáře hardwaru (**SMS_Firmware**) a vlastnost (**UEFI**), která vám pomůže určit, jestli se počítač spustí v režimu UEFI. Pokud je počítač spuštěn v režimu UEFI, vlastnost **UEFI** je nastavena na **hodnotu true**. Tato možnost je ve výchozím nastavení povolená v inventáři hardwaru. Další informace o inventáři hardwaru najdete v tématu [Konfigurace inventáře hardwaru](../../clients/manage/inventory/configure-hardware-inventory.md).

### <a name="improvements-to-software-center-warning-messages-for-high-impact-task-sequences"></a>Vylepšení varovných zpráv centra softwaru pro pořadí úkolů s vysokým dopadem
Tato verze zahrnuje následující vylepšení zpráv centra softwaru pro pořadí úloh nasazení s vysokým dopadem:

- Ve vlastnostech pořadí úkolů teď můžete nakonfigurovat jakékoli pořadí úkolů, včetně pořadí úkolů neoperačního systému, jako vysoce rizikové nasazení. Pořadí úkolů, které splňuje určité podmínky, je automaticky definováno jako vysoce ovlivněno. Podrobnosti najdete v tématu [Správa nasazení s vysokým rizikem](../../servers/manage/settings-to-manage-high-risk-deployments.md).
- Ve vlastnostech pořadí úkolů můžete zvolit použití výchozí zprávy oznámení nebo vytvořit vlastní zprávu oznámení pro nasazení s vysokým dopadem.
- Ve vlastnostech pořadí úkolů můžete nakonfigurovat vlastnosti centra softwaru, které zahrnují nastavení vyžadovaná k restartování, velikost stahování pořadí úkolů a odhadovanou dobu běhu.
- Výchozí zpráva o nasazení s vysokým dopadem pro místní upgrady nyní uvádí, že vaše aplikace, data a nastavení se migrují automaticky. Předchozí zpráva pro jakoukoli instalaci operačního systému ukázala, že všechny aplikace, data a nastavení budou ztraceny, což nebylo pro místní upgrade pravdivé.

Podrobnosti najdete v tématu [Konfigurace nastavení pořadí úkolů s vysokým dopadem](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#set-a-task-sequence-as-a-high-impact-task-sequence) .

### <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Vrátit se na předchozí stránku, když pořadí úkolů dojde k chybě
Při spuštění pořadí úkolů se teď můžete vrátit na předchozí stránku a dojde k selhání. Před touto verzí jste museli pořadí úkolů restartovat, pokud došlo k selhání. Například můžete použít tlačítko **Předchozí** v následujících scénářích:

- Když se počítač spustí v prostředí Windows PE, může se dialogové okno spuštění pořadí úkolů zobrazit předtím, než bude pořadí úkolů k dispozici. Když v tomto scénáři kliknete na další, na poslední stránce pořadí úkolů se zobrazí zpráva, že nejsou k dispozici žádná pořadí úkolů. Nyní můžete kliknutím na tlačítko **Předchozí** Hledat v dostupných pořadích úloh znovu. Tento postup můžete opakovat až do chvíle, kdy je pořadí úkolů k dispozici.
- Když spouštíte pořadí úkolů, ale závislé balíčky obsahu ještě nejsou v distribučních bodech k dispozici, pořadí úkolů se nezdařilo. Nyní můžete distribuovat chybějící obsah (Pokud ještě nebyl distribuován) nebo počkat, až bude obsah k dispozici v distribučních bodech, a potom kliknutím na tlačítko **Předchozí** vyhledáte znovu pořadí úloh pro daný obsah.

### <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Obsah předběžné mezipaměti pro dostupná nasazení a pořadí úkolů
Počínaje verzí 1702 můžete pro dostupná nasazení pořadí úkolů použít předběžnou mezipaměť obsahu. Obsah předběžného ukládání do mezipaměti vám poskytne možnost, aby klient mohl stahovat jenom příslušný obsah hned po přijetí nasazení. Proto když uživatel klikne na **instalovat** v centru softwaru, obsah je připravený a instalace se spustí rychle, protože obsah je na místním pevném disku. Podrobnosti najdete v tématu [Konfigurace obsahu před ukládáním do mezipaměti](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#configure-pre-cache-content).

### <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Převod ze systému BIOS na rozhraní UEFI během místního upgradu
Windows 10 Creators Update zavádí jednoduchý nástroj pro převod, který automatizuje proces opětovného rozdělení pevného disku na hardware s podporou rozhraní UEFI a integruje Nástroj pro převod do místního procesu upgradu Windows 7 na Windows 10. Pokud tento nástroj zkombinujete s pořadím úkolů upgradu operačního systému a nástrojem OEM, který převede firmware ze systému BIOS na rozhraní UEFI, můžete počítače převést na systém BIOS na rozhraní UEFI v rámci místního upgradu na aktualizaci Windows 10 Creators Update. Podrobnosti najdete v tématu věnovaném [krokům pořadí úkolů ke správě převodu systému BIOS na rozhraní UEFI](../../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).

### <a name="improvements-to-the-install-applications-task-sequence-step"></a>Vylepšení kroku pořadí úkolů instalovat aplikace
Tato verze zavedla následující vylepšení:
- Zvýšila se maximální počet aplikací, které můžete nainstalovat do 99 v kroku pořadí úkolů **instalovat aplikace** . Předchozí maximální počet aplikací byl 9.
- Když přidáváte aplikace do kroku pořadí úloh **instalovat aplikace** v editoru pořadí úloh, teď můžete v podokně **Vybrat aplikaci k instalaci** vybrat více aplikací.

### <a name="improvements-to-the-auto-apply-driver-task-sequence"></a>Vylepšení pořadí úkolů automaticky použít ovladač
Nové proměnné pořadí úkolů jsou nyní k dispozici ke konfiguraci hodnoty časového limitu pro krok pořadí úkolů automaticky použít ovladač při vytváření požadavků katalogu HTTP. K dispozici jsou následující proměnné a výchozí hodnoty (v sekundách):
- SMSTSDriverRequestResolveTimeOut  
  Výchozí: 60
- SMSTSDriverRequestConnectTimeOut  
  Výchozí: 60
- SMSTSDriverRequestSendTimeOut  
  Výchozí: 60
- SMSTSDriverRequestReceiveTimeOut  
  Výchozí: 480

### <a name="windows-10-adk-tracked-by-build-version"></a>Windows 10 ADK sledovaný podle verze buildu
Windows 10 ADK je teď sledováno pomocí verze sestavení, aby se zajistilo více podporované prostředí při přizpůsobení spouštěcích imagí s Windows 10. Pokud například lokalita používá Windows ADK pro Windows 10 verze 1607, můžete v konzole přizpůsobit jenom spouštěcí image s verzí 10.0.14393. Podrobnosti o přizpůsobení verzí prostředí WinPE najdete v tématu [Přizpůsobení spouštěcích bitových kopií](../../../osd/get-started/customize-boot-images.md).

### <a name="default-boot-image-source-path-can-no-longer-be-changed"></a>Výchozí zdrojovou cestu spouštěcí bitové kopie již nelze změnit.
Výchozí spouštěcí image jsou spravované pomocí Configuration Manager a výchozí zdrojovou cestu spouštěcí bitové kopie již nelze změnit v konzole Configuration Manager nebo pomocí sady Configuration Manager SDK. Můžete pokračovat v konfiguraci vlastní zdrojové cesty pro vlastní spouštěcí image.

### <a name="default-boot-images-are-regenerated-after-upgrading-configuration-manager-to-a-new-version"></a>Po upgradu Configuration Manager na novou verzi se znovu vygenerují výchozí spouštěcí image.
Od této verze, když upgradujete verzi Windows ADK a pak pomocí aktualizace a údržby nainstalujete nejnovější verzi Configuration Manager, Configuration Manager obnoví výchozí spouštěcí image. To zahrnuje novou verzi Windows PE z aktualizovaného ADK Windows, nové verze klienta Configuration Manager, ovladačů, přizpůsobení atd. Vlastní spouštěcí image se nemění. Podrobnosti najdete v tématu [Správa spouštěcích imagí](../../../osd/get-started/manage-boot-images.md#BKMK_BootImageDefault).

## <a name="software-updates"></a>Aktualizace softwaru

### <a name="deploy-office-365-apps-to-clients"></a>Nasazení aplikací Office 365 na klienty
Počínaje verzí 1702 na řídicím panelu pro správu klientů Office 365 můžete spustit instalační program sady Office 365, který vám umožní nakonfigurovat nastavení instalace systému Office 365, stahovat soubory ze sítí Office Content Delivery Network (sítě CDN) a nasazovat soubory jako aplikace v Configuration Manager. Podrobnosti najdete v tématu [Správa aktualizací Office 365 ProPlus](../../../sum/deploy-use/manage-office-365-proplus-updates.md#deploy-office-365-apps).

> [!IMPORTANT]
> Aplikaci Office 365, kterou vytvoříte a nasadíte pomocí Průvodce aplikací Office 365 v Configuration Manager není automaticky spravovaná pomocí Configuration Manager, dokud nepovolíte možnost **Povolit správu klienta aktualizace softwaru pro klienta sady office 365 znovu** . Podrobnosti najdete v tématu [informace o nastavení klienta](../../clients/deploy/about-client-settings.md).

### <a name="manage-express-installation-files-for-windows-10-updates"></a>Správa souborů expresní instalace pro aktualizace Windows 10
Počínaje verzí 1702 Configuration Manager podporuje soubory Expresní instalace pro aktualizace Windows 10. Pokud používáte podporovanou verzi Windows 10, můžete použít nastavení Configuration Manager ke stažení jenom změn mezi kumulativní aktualizací Windows 10 aktuálního měsíce a aktualizací z předchozího měsíce. Bez souborů Expresní instalace Configuration Manager stáhne každý měsíc úplnou kumulativní aktualizaci Windows 10 (včetně všech aktualizací z předchozích měsíců). Použití souborů Expresní instalace poskytuje menší soubory ke stažení a rychlejší instalaci u klientů. Podrobnosti najdete v tématu [Správa souborů Expresní instalace pro aktualizace Windows 10](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).


<!-- ## Reporting  -->

<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Správa mobilních zařízení

### <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>Verze Androidu a iOS už nejsou cílené v průvodcích vytváření pro hybridní správu mobilních zařízení (MDM).

Počínaje verzí 1702 pro hybridní správu mobilních zařízení (MDM) už nemusíte při vytváření nových zásad a profilů pro zařízení spravovaná přes Intune cílit na konkrétní verze Androidu a iOS. Místo toho vyberte jeden z následujících typů zařízení:

- Android
- Samsung KNOX Standard 4,0 a vyšší
- iPhone
- iPad

Tato změna má vliv na průvodce vytvářením následujících položek:

- Položky konfigurace
- Compliance zásady
- Profily certifikátů
- E-mailové profily.
- Profily sítě VPN
- Profily sítě Wi-Fi

Díky této změně můžou hybridní nasazení poskytovat rychlejší podporu pro nové verze Androidu a iOS, aniž by bylo potřeba nové vydání Configuration Manager nebo rozšíření. Jakmile je nová verze v Intune samostatně podporovaná, uživatelé budou moct mobilní zařízení upgradovat na tuto verzi.

Aby se zabránilo problémům při upgradu z předchozích verzí Configuration Manager, jsou verze mobilního operačního systému stále k dispozici na stránkách vlastností pro tyto položky. Pokud stále potřebujete cílit na konkrétní verzi, můžete vytvořit novou položku a pak na stránce vlastností nově vytvořené položky zadat cílovou verzi. 

> [!NOTE]
> Poslední verze mobilního operačního systému, která je k dispozici na stránkách vlastností, se vztahuje na tuto verzi a všechny následné verze. Stránky vlastností poskytují následující možnosti pro cílení na operační systémy novější než Android 7 a iOS 10: 
> - **Android 7 a novější**
> - **Všechna zařízení iPhone nebo iPod touch s iOS 10 a vyšším**
> - **Všechna zařízení iPad s iOS 10 a vyšším**

### <a name="android-for-work-support"></a>Podpora programu Android for Work
Počínaje 1702 se v hybridní správě mobilních zařízení s Microsoft Intune teď podporuje registrace a Správa zařízení s Androidem for Work.

### <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Nasazení hromadně zakoupených aplikací pro iOS do kolekcí zařízení

Můžete teď nasadit licencované aplikace do zařízení i pro uživatele. V závislosti na možnosti aplikace podporovat licencování zařízení bude při nasazování k vhodné licence, a to následujícím způsobem:

|||||
|-|-|-|-|
|Verze Configuration Manager|Aplikace podporuje licencování zařízení?|Typ kolekce nasazení|Deklarovaná licence|
|Starší než 1702|Ano|Uživatel|Uživatelská licence|
|Starší než 1702|Ne|Uživatel|Uživatelská licence|
|Starší než 1702|Ano|Zařízení|Uživatelská licence|
|Starší než 1702|Ne|Zařízení|Uživatelská licence|
|1702 a novější|Ano|Uživatel|Uživatelská licence|
|1702 a novější|Ne|Uživatel|Uživatelská licence|
|1702 a novější|Ano|Zařízení|Licence zařízení|
|1702 a novější|Ne|Zařízení|Uživatelská licence|

### <a name="support-for-ios-volume-purchase-program-for-education"></a>Podpora programu Volume purchase program pro iOS pro vzdělávání

Nyní můžete nasazovat a sledovat aplikace, které jste koupili v programu Volume purchase program pro iOS pro vzdělávání.

### <a name="support-for-multiple-volume-purchase-program-tokens"></a>Podpora více tokenů programu Volume purchase program

Nyní můžete k Configuration Manager přidružit více tokenů programu Apple Volume purchase program.

### <a name="support-for-line-of-business-apps-in-windows-store-for-business"></a>Podpora obchodních aplikací ve Windows Storu pro firmy

Nyní můžete synchronizovat vlastní obchodní aplikace z Windows Storu pro firmy.

### <a name="conditional-access-device-compliance-policy-improvements"></a>Vylepšení zásad dodržování předpisů pro zařízení podmíněného přístupu

K dispozici je nové pravidlo zásad dodržování předpisů pro zařízení, které vám umožní blokovat přístup k firemním prostředkům, které podporují podmíněný přístup, když uživatelé používají aplikace, které jsou součástí seznamu nekompatibilních aplikací. Seznam aplikací, které nedodržují předpisy, může správce definovat při přidávání nových aplikací pro dodržování předpisů **, které se nedají nainstalovat**. Toto pravidlo vyžaduje, aby správce při přidávání aplikace do seznamu nevyhovujících předpisů zadal **název aplikace**, **ID aplikace**a **vydavatele aplikace** (volitelné). Toto nastavení platí jenom pro zařízení s iOS a Androidem.

Kromě toho pomáhá organizacím zmírnit únik dat prostřednictvím nezabezpečených aplikací a zabránit nadměrné spotřebě dat prostřednictvím určitých aplikací.


### <a name="new-mobile-threat-defense-monitoring-tools"></a>Nové nástroje pro monitorování ochrany před mobilními hrozbami

Počínaje verzí 1702 máte nové způsoby, jak monitorovat stav dodržování předpisů vaším poskytovatelem služby ochrany před mobilními hrozbami.


## <a name="protect-devices"></a>Ochrana zařízení

### <a name="detect-outdated-antimalware-client-versions"></a>Zjistit zastaralé verze antimalwarového klienta
Počínaje verzí 1702 můžete nakonfigurovat výstrahu, aby se zajistilo, že Endpoint Protection klienti nebudou zastaralí. Další informace najdete v tématu [výstraha pro zastaralého klienta malwaru](../../../protect/deploy-use/endpoint-configure-alerts.md#alert-for-outdated-malware-client).

### <a name="device-health-attestation-updates"></a>Aktualizace ověření stavu zařízení
Služba ověření stavu zařízení pro místní klienty se teď dá nakonfigurovat a spravovat z bodu správy. Další informace najdete v tématu [ověření stavu](../../servers/manage/health-attestation.md).

### <a name="certificate-profiles-for-windows-hello-for-business"></a>Profily certifikátů pro Windows Hello pro firmy

Pokud máte v úmyslu ukládat profily certifikátů do kontejneru klíčů Windows Hello pro firmy a profil certifikátu používá rozšířené použití klíče pro přihlášení pomocí čipové karty, musíte nakonfigurovat oprávnění pro registraci klíče, aby se ověřilo správné ověření certifikátu.
Další informace najdete v tématu [nastavení Windows Hello pro firmy](../../../protect/deploy-use/windows-hello-for-business-settings.md).

### <a name="new-windows-hello-for-business-notification-for-end-users"></a>Nové oznámení Windows Hello pro firmy pro koncové uživatele
Nové oznámení Windows 10 informuje koncové uživatele o tom, že musí podniknout další kroky k dokončení nastavení Windows Hello pro firmy (například nastavení PIN kódu).
