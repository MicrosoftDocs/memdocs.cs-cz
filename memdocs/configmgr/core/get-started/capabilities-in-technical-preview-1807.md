---
title: Technical Preview 1807
titleSuffix: Configuration Manager
description: Přečtěte si o nových funkcích, které jsou k dispozici ve větvi Configuration Manager Technical Preview verze 1807.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bcde47a7-433e-4944-964b-539b17d15d64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 398f16b8f75d894030d76406807f74bdaa4be9d5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714784"
---
# <a name="capabilities-in-configuration-manager-technical-preview-version-1807"></a>Funkce v Configuration Manager Technical Preview verze 1807 

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1807. Nainstalujte tuto verzi, abyste aktualizovali a přidali nové funkce na web Technical Preview. 

Před instalací této aktualizace si přečtěte článek [Technical Preview](technical-preview.md) . V tomto článku se seznámíte s obecnými požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu.     


<!--  Known Issues Template
## Known issues 

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



## <a name="known-issues"></a>Známé problémy 

### <a name="issues-with-office-365-software-updates"></a><a name="ki_o365"></a>Problémy s aktualizacemi softwaru Office 365
<!--521365-->
Pokud ke správě aktualizací Office 365 používáte verzi Technical Preview, verze 1806 a 1806,2, instalace na klienty se nemusí zdařit. 

#### <a name="workaround"></a>Alternativní řešení
- Odstraňte existující balíčky pro nasazení a skupiny aktualizací softwaru pro sadu Office 365.  

- Od 31. července 2018 synchronizujte aktualizace softwaru Office 365 a nasaďte pouze nejnovější aktualizace.  



</br>

**Následující části popisují nové funkce, které je možné v této verzi vyzkoušet:**  


## <a name="community-hub"></a><a name="bkmk_hub"></a>Centrum komunity
<!--1357766-->

Centrum komunity je centralizované místo pro sdílení užitečných Configuration Manager objektů s ostatními. Podívejte se na nový pracovní prostor **komunity** v konzole Configuration Manager a vyberte uzel **hub** . Použijte Centrum komunity ke stažení následujících typů objektů Configuration Manager: 
- Scripts
- Položky konfigurace

![Konzola Configuration Manager, pracovní prostor komunity, uzel centra](media/1357766-hub.png)

Pokud chcete zobrazit další podrobnosti o dostupné položce, klikněte na ni v centru. Na stránce Podrobnosti klikněte na **Stáhnout** a získejte položku. Když si stáhnete položku z centra, automaticky se přidá do vašeho webu. 

![Configuration Manager konzola, pracovní prostor komunity, uzel centra, stránka podrobností](media/1357766-hub-details.png)

Pracovní prostor **komunity** obsahuje také následující uzly:

- **Dokumentace**: zobrazuje [knihovnu dokumentace](https://docs.microsoft.com/sccm/) Configuration Manager  

- **Feedback**: zobrazuje web Configuration Manager [UserVoice](https://configurationmanager.uservoice.com/)  


### <a name="prerequisites"></a>Požadavky

- Použijte konzolu Configuration Manager v operačním systému klienta.  

    - Další, ale nedoporučuje se: na operačním systému serveru zakažte [Internet Explorer: Konfigurace rozšířeného zabezpečení](https://go.microsoft.com/fwlink/?LinkId=253461).  

- Počítač s konzolou vyžaduje přístup k Internetu a připojení k následujícím webům:  
    - `https://aka.ms`  
    - `https://comfigmgr-hub.azurewebsites.net`  
    - `https://configmgronline.visualstudio.com`  


### <a name="known-issue"></a>Známý problém

Přispívající položky do centra nejsou v tuto verzi aktuálně k dispozici. 



## <a name="specify-the-drive-for-offline-os-image-servicing"></a><a name="bkmk_osd"></a>Zadejte jednotku pro obsluhu bitové kopie operačního systému offline  
<!--1358924-->

Na základě vašich [názorů na UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/33506009-gui-option-for-offline-os-image-servicing-drive)teď zadejte jednotku, kterou Configuration Manager používá během offline údržby imagí operačního systému. Tento proces může využívat velké množství místa na disku s dočasnými soubory, takže tato možnost nabízí flexibilitu pro výběr jednotky, která se má použít. 


### <a name="try-it-out"></a>Určitě to udělejte!

Zkuste úkoly dokončit. Potom vám pošle [zpětnou vazbu](capabilities-in-technical-preview-1804.md#bkmk_feedback) k vašim nápadům na funkci.

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** . Na pásu karet klikněte na položku **Konfigurovat součásti webu** a vyberte možnost **bod aktualizace softwaru**.  

2. Přepněte na kartu **Údržba offline** a určete možnost, jakou **má místní jednotka používat offline údržbu imagí**.  

Ve výchozím nastavení je toto nastavení **Automatické**. S touto hodnotou Configuration Manager vybere jednotku, na které je nainstalována. 

Během offline údržby Configuration Manager ukládá do složky dočasné soubory `<drive>:\ConfigMgr_OfflineImageServicing`. Také připojí image operačního systému do této složky. 

Zkontrolujte soubor protokolu **OfflineServicingMgr. log** . 



## <a name="co-managed-device-sync-activity-from-intune"></a><a name="bkmk_comgmt"></a>Souběžně spravovaná aktivita synchronizace zařízení z Intune
<!--1358565-->

Zobrazuje se v konzole Configuration Manager, jestli je spoluspravované zařízení aktivní pomocí Microsoft Intune. Tento stav je založený na datech z [datového skladu Intune](https://docs.microsoft.com/intune/reports-nav-create-intune-reports). Řídicí panel **stav klienta** v konzole Configuration Manager zobrazuje **neaktivní klienty pomocí Intune**. Tato nová kategorie je určena pro spoluspravovaná zařízení, která jsou neaktivní pomocí Configuration Manager, ale během minulého týdne byla synchronizovaná se službou Intune.


### <a name="try-it-out"></a>Určitě to udělejte!

Zkuste úkoly dokončit. Potom vám pošle [zpětnou vazbu](capabilities-in-technical-preview-1804.md#bkmk_feedback) k vašim nápadům na funkci.

Pokud jste již vytvořili web pro spolusprávu: 

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **spoluspráva** . Na pásu karet klikněte na **vlastnosti** .  

2. Přepněte na kartu **vytváření sestav** . klikněte na tlačítko **Přihlásit** a ověřit. Pak kliknutím na **aktualizovat** povolte oprávnění ke čtení pro datový sklad Intune.  

3. Po synchronizaci lokality s Intune přejdete do pracovního prostoru **monitorování** a vyberete uzel **stav klienta** . V části **Celkový stav klienta** se podívejte na řádek **neaktivních klientů pomocí Intune**.  

Další informace o povolení spolusprávy najdete v tématu [společná správa pro zařízení s Windows 10](../../comanage/overview.md).



## <a name="repair-applications"></a><a name="bkmk_app-repair"></a>Opravit aplikace
<!--1357866-->

Na základě vaší [zpětné vazby](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8365071-force-reinstall-of-application)na webu UserVoice teď zadejte příkazový řádek opravy pro instalační služba systému Windows a typy nasazení instalačního programu skriptů. 


### <a name="try-it-out"></a>Určitě to udělejte!

Zkuste úkoly dokončit. Potom vám pošle [zpětnou vazbu](capabilities-in-technical-preview-1804.md#bkmk_feedback) k vašim nápadům na funkci.

1. V konzole Configuration Manager otevřete vlastnosti typu nasazení Instalační služba systému Windows nebo instalační program skriptu.  

2. Přepněte na kartu **programy** . Zadejte příkaz pro **opravný program** .  

3. Nasaďte aplikaci. Na kartě **nastavení nasazení** v nasazení povolte možnost povolit **koncovým uživatelům pokusit se opravit tuto aplikaci**.  


### <a name="known-issue"></a>Známý problém

Tlačítko Nový v centru softwaru pro uživatele, kteří mají **opravit** aplikaci, není v této verzi vidět.  



## <a name="approve-application-requests-via-email"></a><a name="bkmk_email-approve"></a>Schvalování žádostí o aplikace přes e-mail
<!--1321550-->

Nakonfigurujte e-mailová oznámení pro žádosti o schválení aplikace. Když uživatel požádá o aplikaci, obdržíte e-mail. Kliknutím na odkazy v e-mailu schválíte nebo odepřete žádost, aniž byste museli konzolu Configuration Manager.


### <a name="prerequisites"></a>Požadavky

#### <a name="to-send-email-notifications"></a>Odeslání e-mailových oznámení
- Povolit [volitelnou funkci](../servers/manage/install-in-console-updates.md#bkmk_options) **schválit žádosti o aplikace pro uživatele na zařízení**.  

- Konfigurace [e-mailových oznámení pro výstrahy](../servers/manage/use-alerts-and-the-status-system.md#to-configure-email-notification-for-alerts).  

#### <a name="to-approve-or-deny-requests-from-email"></a>Schválení nebo zamítnutí žádostí z e-mailu
Pokud tyto požadavky nenakonfigurujete, lokalita pošle e-mailové oznámení pro žádosti o aplikace bez odkazů na schválení nebo zamítnutí žádosti.  

- Ve vlastnostech lokality **Povolte koncový bod REST pro všechny role poskytovatelů v této lokalitě a umožněte Configuration Manager provozu brány pro správu cloudu**. Další informace najdete v tématu [přístup k datům koncového bodu OData](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access).  

    - Po povolení koncového bodu REST restartujte službu SMS_EXEC.

- [Brána pro správu cloudu](../clients/manage/cmg/plan-cloud-management-gateway.md)  

- Zprovoznění lokality do [služeb Azure](../servers/deploy/configure/azure-services-wizard.md) pro **správu cloudu**  

    - Povolit [zjišťování uživatelů Azure AD](../servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  

    - Pro tuto nativní aplikaci v Azure AD ručně nakonfigurujte následující nastavení:  

        - **Identifikátor URI**pro `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`přesměrování:. Použijte plně kvalifikovaný název domény (FQDN) služby brány pro správu cloudu (CMG), například GraniteFalls.Contoso.com.   

        - **Manifest**: nastavte **oauth2AllowImplicitFlow** na hodnotu true:`"oauth2AllowImplicitFlow": true,`  


### <a name="try-it-out"></a>Určitě to udělejte!

Zkuste úkoly dokončit. Potom vám pošle [zpětnou vazbu](capabilities-in-technical-preview-1804.md#bkmk_feedback) k vašim nápadům na funkci.

1. V konzole Configuration Manager Nasaďte aplikaci jako dostupnou pro kolekci uživatelů. Na stránce **nastavení nasazení** Povolte schválení. Pak zadejte *jednu* e-mailovou adresu pro příjem oznámení.  

     > [!Note]  
     > Kdokoli ve vaší organizaci Azure AD, který obdrží e-mail, může žádost schválit. Nepředávejte e-mail ostatním uživatelům, pokud nechcete, aby provedli akci.  

2. Jako uživatel si vyžádejte aplikaci v centru softwaru.  

3. Obdržíte e-mailové oznámení podobné následujícímu příkladu:  

![Příklad e-mailového oznámení pro schválení aplikace](media/1321550-email.png)

> [!Note]  
> Odkaz na schválení nebo odepření je pro jednorázové použití. Například můžete nakonfigurovat alias skupiny pro příjem oznámení. MB schválí požadavek. Nyní Bruce nemůže žádost zamítnout.  



## <a name="improvement-to-script-output"></a><a name="bkmk_script"></a>Vylepšení výstupu skriptu
<!--1236459-->

Teď si můžete zobrazit podrobný výstup skriptu v nezpracovaném nebo strukturovaném formátu JSON. Toto formátování usnadňuje čtení a analýzu výstupu. Pokud skript vrátí platný text ve formátu JSON, zobrazte podrobný výstup buď jako **výstup JSON** , nebo jako **nezpracovaný výstup**. V opačném případě je jediným z možností **výstup skriptu**. 

#### <a name="example-script-output-is-valid-json"></a>Příklad: výstup skriptu je platný kód JSON.
Systému`$PSVersionTable.PSVersion`  

``` Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

#### <a name="example-script-output-isnt-valid-json"></a>Příklad: výstup skriptu není platný formát JSON.
Systému`Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

``` Output
Microsoft Windows 10 Enterprise
```


### <a name="try-it-out"></a>Určitě to udělejte!

Zkuste úkoly dokončit. Potom vám pošle [zpětnou vazbu](capabilities-in-technical-preview-1804.md#bkmk_feedback) k vašim nápadům na funkci.

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte uzel **kolekce zařízení** . Klikněte pravým tlačítkem na kolekci a vyberte **Spustit skript**. Další informace o vytváření a spouštění skriptů najdete v tématu [Vytvoření a spuštění skriptů PowerShellu z konzoly Configuration Manager](../../apps/deploy-use/create-deploy-scripts.md).  

2. Spusťte skript na cílové kolekci.  

3. Na stránce **sledování stavu skriptu** v Průvodci spuštěním skriptu vyberte v dolní části kartu **Souhrn** . Změňte dva rozevírací seznamy v horní části na výstup a **tabulku dat** **skriptu** . Pak dvakrát klikněte na řádek výsledků a otevřete dialogové okno **podrobný výstup** .  

4. Na stránce **sledování stavu skriptu** v Průvodci spuštěním skriptu vyberte v dolní části kartu **Podrobnosti o spuštění** . Dvojím kliknutím na řádek výsledků otevřete dialogové okno podrobného výstupu pro toto zařízení.  



## <a name="improvement-to-third-party-software-updates"></a><a name="bkmk_3pupdate"></a>Vylepšení aktualizací softwaru třetích stran
<!--1358714-->

Nyní můžete upravit vlastnosti vlastních katalogů.

Další informace najdete v tématu [podpora aktualizací softwaru třetích stran pro vlastní katalogy](capabilities-in-technical-preview-1806-2.md#bkmk_3pupdate).



## <a name="next-steps"></a>Další kroky

Další informace o instalaci nebo aktualizaci větve Technical Preview najdete v tématu [Technical Preview](technical-preview.md).    

Další informace o různých větvích Configuration Manager najdete v tématu [kterou větev Configuration Manager mám použít?](../understand/which-branch-should-i-use.md)
