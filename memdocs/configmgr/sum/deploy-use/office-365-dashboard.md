---
title: Řídicí panel pro správu klientů Office 365
titleSuffix: Configuration Manager
description: Kontrola informací o klientech Office 365 z řídicího panelu pro správu klientů Office 365
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 69f234a2-b04b-445a-b81f-6b4acfc00eaf
ms.openlocfilehash: 7e6ed38d0f4217bfc70d3ddb196527d421e5d7c1
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110385"
---
# <a name="office-365-client-management-dashboard"></a>Řídicí panel pro správu klientů Office 365

*Platí pro: Configuration Manager (Current Branch)*

> [!Note]
> Od 21. dubna 2020 se sada Office 365 ProPlus přejmenovává na **Microsoft 365 aplikace pro podniky**. Další informace najdete v tématu [Změna názvu pro Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). V konzole Configuration Manager se pořád zobrazují odkazy na starý název a podpůrná dokumentace, zatímco se konzola aktualizuje.

Od verze Configuration Manager 1802 můžete zkontrolovat informace o klientech Office 365 z řídicího panelu pro správu klientů 365 Office. Řídicí panel pro správu klientů Office 365 zobrazuje seznam relevantních zařízení, když jsou vybrány oddíly grafu. <!--1357281 -->

## <a name="prerequisites"></a>Požadavky

### <a name="enable-hardware-inventory"></a>Povolit inventář hardwaru

Data zobrazená na řídicím panelu pro správu klientů Office 365 pocházejí z inventáře hardwaru. Povolte inventář hardwaru a pro data, která se mají zobrazit na řídicím panelu, vyberte třídu inventáře hardwaru **Office 365 ProPlus Configurations** .
 
1. Povolte inventář hardwaru, pokud ještě není povolený. Podrobnosti najdete v tématu [Konfigurace inventáře hardwaru](../../core/clients/manage/inventory/configure-hardware-inventory.md).
2. V konzole Configuration Manager přejděte na **Správa** > **Nastavení** > klienta**výchozí nastavení klienta**.  
3. Na kartě **Domů** ve skupině **Vlastnosti** klikněte na možnost **Vlastnosti**.  
4. V dialogovém okně **Výchozí nastavení klienta** klikněte na **Inventář hardwaru**.  
5. V seznamu **Nastavení zařízení** klikněte na **Nastavit třídy**.  
6. V dialogovém okně **třídy inventáře hardwaru** vyberte **Konfigurace Office 365 ProPlus**.  
7. Kliknutím na **OK** uložíte změny a zavřete dialogové okno **Třídy inventáře hardwaru** .

Řídicí panel pro správu klientů Office 365 začne zobrazovat data při hlášení inventáře hardwaru.

### <a name="connectivity-for-top-level-site-server"></a>Připojení pro server lokality nejvyšší úrovně

*(Představené ve verzi 1906 jako předpoklad)*

Webový server nejvyšší úrovně potřebuje přístup k následujícímu koncovému bodu ke stažení souboru připravenosti:

`https://contentstorage.osi.office.net/sccmreadinessppe/sot_sccm_addinreadiness.cab`

> [!NOTE]
> Připojení k Internetu není pro některé z těchto scénářů vyžadováno u klientských zařízení.

### <a name="enable-data-collection-for-office-365-proplus"></a>Povolit shromažďování dat pro Office 365 ProPlus

*(Představené ve verzi 1910 jako předpoklad)*

Počínaje verzí 1910 budete muset povolit shromažďování dat pro Office 365 ProPlus, abyste mohli naplnit informace v **pilotním a řídicím panelu pro sadu office 365**. Data jsou uložená v databázi lokality Configuration Manager a neodesílají se do Microsoftu.

Tato data se liší od diagnostických dat, která jsou popsána v [diagnostických datech odeslaných ze sady Office 365 ProPlus společnosti Microsoft](https://docs.microsoft.com/deployoffice/privacy/overview-privacy-controls#diagnostic-data-sent-from-office-365-proplus-to-microsoft).

Shromažďování dat můžete povolit buď pomocí Zásady skupiny, nebo úpravou registru.

#### <a name="enable-data-collection-from-group-policy"></a>Povolit shromažďování dat z Zásady skupiny

1. Stáhněte si nejnovější [soubory šablon pro správu z webu Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49030).
2. V části `User Configuration\Policies\Administrative Templates\Microsoft Office 2016\Telemetry Dashboard`povolte nastavení zásady pro **Zapnutí shromažďování dat telemetrie** .
    - Případně použijte nastavení zásad ve [službě Office Cloud Policy](https://docs.microsoft.com/DeployOffice/overview-office-cloud-policy-service).
    - Nastavení této zásady se používá i na řídicím panelu telemetrie Office, který nemusíte pro tuto kolekci dat nasazovat.

#### <a name="enable-data-collection-from-the-registry"></a>Povolit shromažďování dat z registru

Níže uvedený příkaz ukazuje, jak povolit shromažďování dat z registru:

```cmd
reg add HKCU\Software\Policies\Microsoft\office\16.0\OSM /v EnableLogging /t REG_DWORD /d 1
```

## <a name="viewing-the-office-365-client-management-dashboard"></a>Zobrazení řídicího panelu pro správu klientů Office 365

Pokud chcete zobrazit řídicí panel pro správu klientů Office 365 v konzole Configuration Manager, přečtěte si v článku > **Přehled** >  **knihovny softwaru****Office 365 Správa klientů**. V horní části řídicího panelu pomocí rozevíracího seznamu **kolekce** můžete data řídicího panelu filtrovat podle členů určité kolekce. Configuration Manager počínaje verzí 1802 se na řídicím panelu pro správu klientů Office 365 po výběru sekcí grafů zobrazuje seznam relevantních zařízení.

Řídicí panel pro správu klientů Office 365 poskytuje grafy pro následující informace:

- Počet klientů Office 365
- Verze klientů Office 365
- Jazyky klienta Office 365
- Kanály klienta Office 365 Další informace najdete v tématu [Přehled kanálů aktualizací pro Office 365 ProPlus](/DeployOffice/overview-of-update-channels-for-office-365-proplus).


## <a name="integration-for-office-365-proplus-readiness"></a><a name="bkmk_o365_readiness"></a>Integrace pro Office 365 ProPlus Readiness
<!--3735402-->
Configuration Manager počínaje verzí 1902 můžete řídicí panel použít k identifikaci zařízení s vysokou jistotou, která je připravená k upgradu na Office 365 ProPlus. Tato integrace poskytuje přehled o potenciálních problémech s kompatibilitou pro doplňky a makra Office ve vašem prostředí. Pak použijte Configuration Manager k nasazení Office do připravených zařízení.

Řídicí panel pro správu klientů Office 365 obsahuje novou dlaždici, **sadu Office 365 ProPlus upgrade Readiness**. Tato dlaždice je pruhový graf zařízení v následujících stavech:
- Nehodnoceno
- Připraveno k upgradu
- Vyžaduje kontrolu

Vyberte stav pro přechod k seznamu zařízení. Tato sestava připravenosti zobrazuje více podrobností o zařízeních. Obsahuje sloupce pro stav kompatibility obou doplňků a maker pro Office.

### <a name="prerequisites-for-office-365-proplus-readiness-integration"></a>Předpoklady pro integraci produktů Office 365 a Readiness

- Povolit inventář hardwaru v nastavení klienta. Další informace najdete v části [požadavky](#prerequisites) .  

- Aby bylo možné stáhnout soubor připravenosti doplňku, musí se zařízení připojit k síti pro doručování obsahu (CDN) pro Office. Další informace najdete v tématu [Content Delivery Networks](https://docs.microsoft.com/office365/enterprise/content-delivery-networks). Pokud zařízení nemůže tento soubor stáhnout, je *nutné zkontrolovat*stav doplňky.  

    > [!Note]  
    > Pro tuto funkci se Microsoftu neodesílají žádná data.  

### <a name="detailed-macro-readiness"></a><a name="bkmk_ort"></a>Podrobná připravenost na makro

Ve výchozím nastavení vyhledává agent vyhledávání v jednotlivých zařízeních seznam naposledy použitých souborů (MRU). Počítá soubory v tomto seznamu, které podporují makra. Mezi tyto soubory patří následující typy:
- Formáty souborů sady Office s povolenými makry (. xlsm) nebo dokument s povolenými makry (. docm) aplikace Excel.  
- Starší formáty Office, které neoznačují, zda je k dispozici obsah makra. Například sešit Excel 97-2003 (. xls).

Pokud potřebujete podrobnější informace o kompatibilitě maker, nasaďte sadu **nástrojů Readiness pro Office** , abyste mohli analyzovat kód v souborech maker. Kontroluje, zda existují potenciální problémy s kompatibilitou. Soubor například používá funkci, která se změnila v novější verzi Office. Po spuštění sady nástrojů Readiness pro Office a vybrání možnosti pro **naposledy použité dokumenty Office a nainstalované doplňky v tomto počítači**nebo použití `-mru` příznaku na příkazovém řádku, můžete výsledky vybrat Configuration Manager agentem inventáře hardwaru. Tato další data zlepšují výpočet připravenosti na zařízení. Další informace najdete v tématu [použití sady nástrojů Readiness Toolkit pro Office k vyhodnocení kompatibility aplikací pro office 365 ProPlus](https://aka.ms/readinesstoolkit).

Všimněte si, že sada nástrojů Readiness Toolkit není nutné instalovat na každé cílové zařízení, aby bylo možné provést kontrolu. Pomocí níže uvedené možnosti příkazového řádku můžete zkontrolovat všechna požadovaná zařízení.  Příznak Output je povinný, ale soubory se nepoužijí k vygenerování výsledků na řídicím panelu, aby bylo možné vybrat jakékoli platné umístění.

```cmd
ReadinessReportCreator.exe -mru -output c:\temp -silent
```

Další informace najdete v tématu [získání informací o připravenosti pro více uživatelů v podniku](/deployoffice/use-the-readiness-toolkit-to-assess-application-compatibility-for-office-365-pro#getting-readiness-information-for-multiple-users-in-an-enterprise).

## <a name="office-365-proplus-upgrade-readiness-dashboard"></a><a name="bkmk_readiness-dash"></a>Řídicí panel připravenosti na upgrade pro Office 365 ProPlus

*(Představené ve verzi 1906)*

<!--4021125-->
Abychom vám pomohli určit, která zařízení jsou připravená k upgradu na Office 365 ProPlus, je k dispozici řídicí panel připravenosti začínající na verzi 1906. Zahrnuje dlaždici **připravenosti na upgrade sady Office 365** , která byla vydaná ve Configuration Manager aktuální verze větve 1902. Následující nové dlaždice na tomto řídicím panelu vám pomůžou zhodnotit Doplňky Office a připravenost makra:

- Nasazení
- Připravenost zařízení
- Připravenost doplňku
- Příkazy podpory doplňku
- Horní doplňky podle počtu verzí
- Počet zařízení, která mají makra
- Připravenost makra
- Poradci maker

Následující video je relace z Ignite 2019, která obsahuje další informace:

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3090]

[Osvědčené postupy pro posouzení kompatibility a systém Microsoft Office 365 ProPlus upgrady pomocí Office Readiness v Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/79338?source=sessions)

### <a name="using-the-office-365-proplus-upgrade-readiness-dashboard"></a>Používání řídicího panelu připravenosti na upgrade pro Office 365 ProPlus

Po ověření splnění [požadavků](#prerequisites)použijte následující pokyny pro použití řídicího panelu:
 
1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte položku **správa klientů Office 365**.
1. Vyberte uzel **ProPlus upgrade Readiness Office 365** .
1. Změňte architekturu **kolekce** a **cílové sady Office** , aby se změnily informace předané na řídicím panelu.

![Řídicí panel připravenosti na upgrade pro Office 365 ProPlus](./media/4021125-office-365-upgrade-readiness-dashboard.png)

![Řídicí panel připravenosti na upgrade pro Office 365 ProPlus](./media/4021125-office-365-to-add-ins.png)

![Řídicí panel připravenosti na upgrade pro Office 365 ProPlus](./media/4021125-office-365-macro-advisories.png)

### <a name="device-readiness-information"></a>Informace o připravenosti na zařízení

Po vyhodnocení inventáře doplňku a makra na jednotlivých zařízeních se pak zařízení seskupí podle informací. Zařízení, jejichž stav je uveden jako **připraveno k upgradu** , pravděpodobně nebudou mít problémy s kompatibilitou.

Výběrem kategorie **připraveno k upgradu** v grafu zobrazíte další podrobnosti o zařízeních v omezování kolekce. Můžete si prohlédnout seznam zařízení, vybrat si podle svých podnikových požadavků a vytvořit novou kolekci zařízení z výběru. Pomocí nové kolekce nasaďte Office 365 ProPlus s Configuration Manager.

Zařízení, která mohou být ohrožena při potížích s kompatibilitou, jsou označena jako **potřebná kontrola**. Tato zařízení můžou vyžadovat, abyste před upgradem na Office 365 ProPlus udělali akci. Například je možné aktualizovat důležité Doplňky na novější verzi.

### <a name="add-in-information"></a>Informace o doplňku

 V každém zařízení se shromáždí inventář všech nainstalovaných doplňků. Inventář se pak porovná s informacemi, které Microsoft má o výkonu doplňku v Office 365 ProPlus. Pokud je nalezen doplněk, který bude po upgradu nejspíš způsobovat problémy, pak jsou všechna zařízení s doplňkem označena ke kontrole.

### <a name="macro-information"></a>Informace o makru

Configuration Manager na každém zařízení prohlíží naposledy použité soubory. Počítá soubory v tomto seznamu, které podporují makra, včetně následujících typů:

- Formáty souborů Office s podporou maker
- Starší formáty Office, které neoznačují, jestli je obsah makra.

Tato sestava slouží k identifikaci zařízení, která nedávno používala soubory, které mohou obsahovat makra. **Sada nástrojů Readiness Toolkit pro Office** se pak dá nasadit pomocí Configuration Manager, aby kontrolovala všechna zařízení, kde jsou potřeba podrobnější informace, a zkontrolujte, jestli neexistují potenciální problémy s kompatibilitou. Například pokud soubor používá funkci, která se změnila v novější verzi Office.

Další informace o tom, jak provést kontrolu, najdete v tématu [Podrobná připravenost k makrům](#bkmk_ort).

## <a name="office-365-proplus-pilot-and-health-dashboard"></a><a name="bkmk_pilot"></a>Pilotní a řídicí panel pro Office 365-plus
<!--4488272, 4488301-->
*(Představené ve verzi 1910)*

Počínaje verzí 1910 se **pilotní a řídicí panel pro office 365 a řídicí panel stavů** vám pomohou naplánovat, nasadit pilotní prostředí a provést nasazení sady office s 365 ProPlus. Řídicí panel poskytuje přehledy stavu pro zařízení s Office 365 ProPlus, které vám pomůžou identifikovat možné problémy, které můžou mít vliv na vaše plány nasazení. **Pilotní a řídicí panel pro sadu Office 365** poskytuje doporučení pro pilotní zařízení založená na inventáři doplňku. Na řídicím panelu jsou následující dlaždice:

- Generování pilotního projektu
- Doporučená zařízení pilotního nasazení
- Nasazení pilotního projektu
- Zařízení odesílající data o stavu
- Zařízení nesplňující cíle stavu
- Doplňky nesplňující cíle stavu
- Makra nesplňující cíle stavu

### <a name="using-the-office-365-proplus-pilot-and-health-dashboard"></a>Použití pilotního řídicího panelu Office 365 ProPlus a stavu

Po ověření splnění [požadavků](#prerequisites)použijte následující pokyny pro použití řídicího panelu:

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte položku **správa klientů Office 365**.
1. Vyberte **pilotní modul Office 365 a uzel stav** .

![Pilotní a řídicí panel pro Office 365-plus](./media/4488272-office-365-pro-plus-pilot.png)


### <a name="generate-pilot"></a>Generování pilotního projektu

Vygenerujte pilotní doporučení z omezené kolekce při kliknutí na tlačítko. Po spuštění akce spustí úloha na pozadí výpočet zkušební kolekce. Vaše omezení kolekce musí obsahovat aspoň jedno zařízení s verzí Office, která není ProPlus.

### <a name="recommended-pilot-devices"></a>Doporučená zařízení pilotního nasazení

**Doporučená pilotní zařízení** představují minimální sadu zařízení, která představují všechny instalované doplňky v rámci omezení kolekce, kterou jste použili při generování pilotního projektu. Přejděte k podrobnostem a získejte seznam těchto zařízení. Pak použijte podrobnosti a v případě potřeby vylučte všechna zařízení z pilotního projektu. Pokud jsou všechny doplňky již na zařízeních se systémem Office 365 ProPlus, zařízení s těmito doplňky nebudou zahrnuta do výpočtu. To také znamená, že v pilotní kolekci nebudete mít žádné výsledky, protože všechny vaše doplňky se zobrazily na zařízeních, kde je nainstalovaná sada Office 365 ProPlus.

### <a name="deploy-pilot"></a>Nasazení pilotního projektu

Po přijetí pilotních zařízení nasaďte Office 365 ProPlus do pilotní kolekce pomocí Průvodce vytvořením postupného nasazení. Správci mohou definovat pilotní a omezující kolekci v průvodci pro správu nasazení.

### <a name="health-data"></a>Data o stavu

Po instalaci Office 365 ProPlus povolte data o stavu na pilotních zařízeních. Data o stavu poskytují přehled o tom, které doplňky a makra nesplňují cíle stavu. **Zařízení připravená k nasazení** grafu identifikují nepilotní zařízení, která jsou připravená k nasazení, pomocí přehledů stavu. Získejte počet zařízení, která odesílají data o stavu ze **zařízení odesílajících data o stavu** .

### <a name="devices-not-meeting-health-goals"></a>Zařízení nesplňující cíle stavu

Tato dlaždice shrnuje zařízení, která mají problémy s doplňky, makry nebo obojím.

### <a name="add-ins-not-meeting-health-goals"></a>Doplňky nesplňující cíle stavu

- Selhání načtení: doplněk se nepovedlo spustit.
- Zhroucení: během běhu doplňku došlo k chybě doplňku.
- Chyba: doplněk ohlásil chybu.
- Více problémů: doplněk má více než jeden z výše uvedených problémů.

### <a name="macros-not-meeting-health-goals"></a>Makra nesplňující cíle stavu

- Selhání načtení: dokument se nepovedlo načíst.
- Chyby za běhu: při běhu makra došlo k chybě. Tyto chyby můžou být závislé na vstupech, takže nemusí vždy dojít k tomu.
- Chyby kompilace: makro nebylo správně zkompilováno, takže se nepokouší spustit.
- Více problémů: makro obsahuje více než jeden z výše uvedených problémů.

> [!NOTE]
> Inventář maker se vyplní daty ze sady nástrojů Readiness Toolkit pro Office a nedávno použitých datových souborů. Stav makra je vyplněný daty o stavu. Z důvodu různých zdrojů dat je možné, že stav maker bude **nutné zkontrolovat** , když není **prohledáváno**inventář makra. <!--5922845-->

### <a name="known-issues"></a>Známé problémy

Došlo k známému problému s dlaždicí **nasazení pilotního nasazení** . V tuto chvíli se nedá použít k nasazení do pilotního projektu. Alternativním řešením je stávající pracovní postup nasazení aplikace pomocí Průvodce dvoufázové nasazení. <!--5525871-->

## <a name="next-steps"></a>Další kroky

[Správa Office 365 ProPlus v Configuration Manageru](manage-office-365-proplus-updates.md)
