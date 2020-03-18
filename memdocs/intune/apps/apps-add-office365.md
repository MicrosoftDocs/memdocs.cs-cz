---
title: Přidání aplikací Office 365 do zařízení s Windows 10 pomocí Microsoft Intune
titleSuffix: ''
description: Naučte se, jak můžete pomocí Microsoft Intune instalovat aplikace Office 365 na zařízeních s Windows 10.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/10/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3292671a-5f5a-429e-90f7-b20019787d22
ms.reviewer: craigma
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, seoapril2019
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1e72993141de963d78d6aeaf512af0165d747c9e
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325979"
---
# <a name="add-office-365-apps-to-windows-10-devices-with-microsoft-intune"></a>Přidání aplikací Office 365 do zařízení s Windows 10 pomocí Microsoft Intune

Než budete moct přiřadit, monitorovat, konfigurovat nebo chránit aplikace, musíte je přidat do Intune. Jedním z dostupných [typů aplikací](apps-add.md#app-types-in-microsoft-intune) jsou aplikace Office 365 pro zařízení s Windows 10. Když vyberete tento typ aplikace v Intune, můžete přiřadit a nainstalovat aplikace Office 365 na zařízení, která spravujete pomocí Windows 10. Můžete také přiřadit a nainstalovat aplikace pro klienta Microsoft Project Online Desktop a Microsoft Visio Online Plan 2, pokud vlastníte jejich licence. Dostupné aplikace Office 365 se zobrazují jako jedna položka v seznamu aplikací v konzole Intune v rámci Azure.

> [!NOTE]
> K aktivaci aplikací Office 365 ProPlus nasazených prostřednictvím Microsoft Intune musíte použít licence Office 365 ProPlus. Intune podporuje Office 365 Business Edition, ale je potřeba nakonfigurovat sadu aplikací sady Office 365 Business Edition pomocí dat XML. Další informace najdete v tématu [Konfigurace sady aplikací s využitím dat XML](apps-add-office365.md#step-2---option-2-configure-app-suite-using-xml-data).

## <a name="before-you-start"></a>Než začnete

> [!IMPORTANT]
> Pokud se na zařízení koncového uživatele nacházejí aplikace Office MSI, je nutné tyto aplikace bezpečně odinstalovat pomocí funkce pro **odebrání MSI**. Jinak se instalace aplikací Office 365 doručených pomocí Intune nezdaří.

- Zařízení, na která chcete tyto aplikace nasadit, musí mít aktualizaci Windows 10 Creators Update nebo novější.
- Intune podporuje přidání aplikací Office jenom ze sady Office 365.
- Pokud jsou spuštěné nějaké aplikace Office, když Intune instaluje sadu aplikací, může instalace selhat a uživatelé můžou přijít o data z neuložených souborů.
- Tato metoda instalace není podporovaná v zařízeních Windows Home, Windows Team, Windows Holografick nebo Windows holografických pro firmy.
- Intune nepodporuje instalaci desktopových aplikací Office 365 z Microsoft Storu (označovaných jako aplikace Office Centennial) na zařízení, na která jste už nasadili aplikace Office 365 pomocí Intune. Pokud nainstalujete tuto konfiguraci, může to způsobit ztrátu nebo poškození dat.
- V případě vícenásobného přiřazení požadovaných nebo dostupných aplikací nemá novější přiřazení aditivní účinek. Novější přiřazení aplikací přepíše dříve existující přiřazení nainstalovaných aplikací. Pokud například první sada aplikací Office obsahuje Word a novější sada ho neobsahuje, Word se odinstaluje. To se netýká aplikací Visio a Project.
- Více nasazení sady Office 365 není aktuálně podporováno. Do zařízení se doručí jenom jedno nasazení.
- **Verze Office**: Vyberte, jestli chcete přiřadit 32bitovou nebo 64bitovou verzi Office. 32bitovou verzi můžete nainstalovat na 32bitová i 64bitová zařízení, ale 64bitovou verzi můžete nainstalovat jenom na 64bitová zařízení.
- **Odebrat MSI ze zařízení koncových uživatelů**: Vyberte, jestli chcete ze zařízení koncových uživatelů odebrat dřívější aplikace Office .MSI. Instalace se nezdaří, pokud již existuje. Aplikace MSI na zařízeních koncových uživatelů. Aplikace k odinstalování se neomezují jen na ty, které jsou vybrané pro instalaci v nastavení **Nakonfigurovat sadu aplikací**, protože ze zařízení koncového uživatele se odeberou všechny aplikace Office (MSI). Další informace najdete v článku věnovaném [odebrání stávajících verzí služby MSI v systému Office při upgradu na Office 365 ProPlus](https://docs.microsoft.com/deployoffice/upgrade-from-msi-version). Když Intune přeinstaluje Office na počítače koncových uživatelů, získají koncoví uživatelé automaticky stejné jazykové sady, které měli s předchozími instalacemi Office .MSI.

## <a name="select-the-office-365-suite-app-type"></a>Vyberte typ aplikace Office 365 Suite.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > **všechny aplikace** > **Přidat**.
3. V části **Sada Office 365** v podokně **Vybrat typ aplikace** vyberte **Windows 10** .
4. Klikněte na **Vybrat**. Zobrazí se kroky **Přidat sadu Office 365** .


## <a name="step-1---app-suite-information"></a>Krok 1 – informace o sadě aplikací

V tomto kroku zadáte informace o sadě aplikací. Tyto informace vám pomůžou sadu aplikací identifikovat v Intune a uživatelům ji pomůžou najít na portálu společnosti.

1. Na stránce **informace o sadě aplikací** můžete potvrdit nebo upravit výchozí hodnoty:
    - **Název sady**: Zadejte název sady aplikací, který se zobrazí na portálu společnosti. Názvy všech používaných sad musí být jedinečné. Pokud stejný název sady aplikací existuje dvakrát, zobrazí se na portálu společnosti uživatelům jenom jedna z aplikací.
    - **Popis sady**: Zadejte popis sady aplikací. Můžete například uvést aplikace, které jste vybrali pro zahrnutí.
    - **Vydavatel**: Jako vydavatel se zobrazí Microsoft.
    - **Kategorie**: Můžete vybrat jednu nebo několik předdefinovaných kategorií nebo kategorii, kterou jste vytvořili. Díky tomuto nastavení uživatelé dokážou sadu aplikací při procházení portálu společnosti jednodušeji najít.
    - **Zobrazit tuto aplikaci jako doporučenou aplikaci v portál společnosti**: tuto možnost vyberte, pokud chcete, aby se sada aplikací zobrazovala na hlavní stránce portálu společnosti, když uživatelé vyhledávají aplikace.
    - **Adresa URL informací**: Volitelně můžete zadat adresu URL webu, který obsahuje informace o této aplikaci. Adresa URL se zobrazí uživatelům na portálu společnosti.
    - **Adresa URL informací o ochraně osobních údajů**: Volitelně zadejte adresu URL webu, který obsahuje informace o ochraně osobních údajů v této aplikaci. Adresa URL se zobrazí uživatelům na portálu společnosti.
    - **Vývojář**: Jako vývojář se zobrazí Microsoft.
    - **Vlastník**: Jako vlastník se zobrazí Microsoft.
    - **Poznámky**: Zadejte jakékoli poznámky, které chcete k aplikaci přidružit.
    - **Logo**: Logo Office 365 se zobrazí u aplikace, když uživatelé procházejí Portál společnosti.
2. Kliknutím na **Další** zobrazte stránku **Konfigurovat sadu aplikací** .

## <a name="step-2---option-1-configure-app-suite-using-the-configuration-designer"></a>Krok 2 – (**možnost 1**) konfigurace sady aplikací pomocí návrháře konfigurace 

Můžete zvolit způsob konfigurace nastavení aplikace výběrem **formátu nastavení konfigurace**. Mezi možnosti formátu nastavení patří:
- Návrhář konfigurace
- Zadání XML dat

Když zvolíte **Configuration Designer** , změní se podokno **Přidat aplikaci** na nabídku tři další oblasti nastavení:
- Konfigurace sady aplikací
- Informace o sadě aplikací
- Vlastnosti

<img alt="Add Office 365 - Configuration designer" src="./media/apps-add-office365/apps-add-office365-02.png" width="700">

1. Na stránce **sada konfiguračních aplikací** vyberte **Návrhář konfigurace**.
   - **Vyberte aplikace Office**: v rozevíracím seznamu vyberte aplikace, které chcete přiřadit k zařízením, a vyberte standardní aplikace Office, které chcete přiřadit k zařízením.
   - **Vybrat jiné aplikace Office (vyžaduje se licence)** : vyberte další aplikace Office, které chcete přiřadit k zařízením a k jejichž licencím máte licence, a to tak, že vyberete aplikace v rozevíracím seznamu. Mezi tyto aplikace patří licencované aplikace, jako je Microsoft Project Online Desktop Client a Microsoft Visio Online Plan 2.
   - **Architektura**: vyberte, jestli chcete přiřadit **32** nebo **64** verzi sady Office ProPlus. 32bitovou verzi můžete nainstalovat na 32bitová i 64bitová zařízení, ale 64bitovou verzi můžete nainstalovat jenom na 64bitová zařízení.
    - **Kanál aktualizací**: Zvolte, jak se na těchto zařízeních aktualizuje Office. Informace o různých kanálech aktualizací najdete v článku [Přehled kanálů aktualizací pro Office 365 ProPlus](https://docs.microsoft.com/DeployOffice/overview-of-update-channels-for-office-365-proplus). Vybírejte z těchto možností:
        - **Měsíčně**
        - **Měsíční (cílený)**
        - **Půlroční**
        - **Půlroční (cílený)**

        Po výběru kanálu můžete vybrat následující možnosti:
        - **Odebrat jiné verze**: Pokud chcete z uživatelských zařízení odebrat jiné verze Office (MSI), vyberte **Ano** . Tuto možnost vyberte, když chcete odebrat již existující sadu Office. Aplikace MSI ze zařízení koncových uživatelů. Instalace se nezdaří, pokud již existuje. Aplikace MSI na zařízeních koncových uživatelů. Aplikace k odinstalování se neomezují jen na ty, které jsou vybrané pro instalaci v nastavení **Nakonfigurovat sadu aplikací**, protože ze zařízení koncového uživatele se odeberou všechny aplikace Office (MSI). Další informace najdete v článku věnovaném [odebrání stávajících verzí služby MSI v systému Office při upgradu na Office 365 ProPlus](https://docs.microsoft.com/deployoffice/upgrade-from-msi-version). Když Intune přeinstaluje Office na počítače koncových uživatelů, získají koncoví uživatelé automaticky stejné jazykové sady, které měli s předchozími instalacemi Office .MSI. 
        - **Verze, která se má nainstalovat**: vyberte verzi Office, která se má nainstalovat.
        - **Konkrétní verze**: Pokud jste ve výše uvedeném nastavení vybrali **konkrétní** verzi, kterou **chcete nainstalovat** , můžete vybrat instalaci konkrétní verze Office pro vybraný kanál na zařízeních koncových uživatelů. 
            
            Dostupné verze se budou v průběhu času měnit. Při vytváření nového nasazení tedy můžou být dostupné novější verze a některé starší verze nemusí být k dispozici. Aktuální nasazení budou dál nasazovat starší verzi, ale seznam verzí se bude průběžně aktualizovat podle kanálu.
            
            Pokud se nainstalovala starší verze, na zařízeních, které aktualizují připnutou verzi (nebo jakékoli jiné vlastnosti) a nasazují se jako dostupné, se až do ohlášení zařízení zobrazí stav hlášení Nainstalováno. Když se zařízení ohlásí, stav se dočasně změní na Neznámé, ale nezobrazí se uživateli. Jakmile uživatel zahájí instalaci novější dostupné verze, uvidí změněný stav Nainstalováno.
            
            Další informace najdete v článku [Základní informace o aktualizačních kanálech Office 365 ProPlus](https://docs.microsoft.com/DeployOffice/overview-of-update-channels-for-office-365-proplus).
    - **Použít aktivaci pro sdílené počítače**: Tuto možnost vyberte, když počítač sdílí více uživatelů. Další informace najdete v článku s [přehledem aktivace pro sdílené počítače pro Office 365](https://docs.microsoft.com/DeployOffice/overview-of-shared-computer-activation-for-office-365-proplus).
    - **Automaticky přijmout licenční smlouvu s koncovým uživatelem aplikace**: Tuto možnost vyberte, pokud nevyžadujete přijetí licenční smlouvy koncovými uživateli. Intune pak smlouvu přijme automaticky.
    - **Jazyky**: Office se automaticky nainstaluje ve všech podporovaných jazycích nainstalovaných s Windows na zařízení koncových uživatelů. Tuto možnost zvolte, pokud chcete nainstalovat se sadou aplikací další jazyky. <p></p>
        Můžete nasadit další jazyky pro aplikace Office 365 Pro Plus spravované prostřednictvím Intune. Seznam dostupných jazyků zahrnuje **Typ** jazykové sady (Základní, Částečná a Kontrola pravopisu). V Azure Portal vyberte **Microsoft Intune** > **aplikace** > **všechny aplikace** > **Přidat**. V seznamu **Typ aplikace** v podokně **Přidat aplikaci** vyberte v části sada **Office 365**možnost **Windows 10** . V podokně **nastavení sady App Suite** vyberte **jazyky** . Další informace najdete v tématu s [přehledem jazyků nasazení v Office 365 ProPlus](https://docs.microsoft.com/deployoffice/overview-of-deploying-languages-in-office-365-proplus).
2. Kliknutím na tlačítko **Další** zobrazíte stránku **značky oboru** .

## <a name="step-2---option-2-configure-app-suite-using-xml-data"></a>Krok 2 – (**možnost 2**) konfigurace sady aplikací s využitím dat XML 

Pokud jste vybrali možnost **zadat data XML** v rozevíracím seznamu **formát nastavení** na stránce **Konfigurovat sadu aplikací** , můžete sadu Office App Suite nakonfigurovat pomocí vlastního konfiguračního souboru.

![Přidat návrháře konfigurace sady Office 365](./media/apps-add-office365/apps-add-office365-01.png)

1. Přidali jste konfigurační XML.

    > [!NOTE]
    > ID produktu může být buď obchodní (`O365BusinessRetail`) nebo ProPlus (`O365ProPlusRetail`). Sadu aplikací sady Office 365 Business Edition však můžete nakonfigurovat pouze pomocí dat XML. 

2. Kliknutím na tlačítko **Další** zobrazíte stránku **značky oboru** .

Další informace o zadávání dat XML najdete v tématu [Možnosti konfigurace pro nástroj pro nasazení Office](https://docs.microsoft.com/DeployOffice/configuration-options-for-the-office-2016-deployment-tool).

## <a name="step-3---select-scope-tags-optional"></a>Krok 3 – výběr značek oboru (volitelné)
Pomocí značek Scope můžete určit, kdo může v Intune zobrazit informace o klientské aplikaci. Úplné podrobnosti o značkách oboru najdete v tématu [použití značek řízení přístupu na základě role a rozsahu pro distribuci IT](../fundamentals/scope-tags.md).

1. Klikněte na **Vybrat značky oboru** a volitelně přidejte značky oboru pro sadu aplikací.
2. Kliknutím na tlačítko **Další** zobrazíte stránku **přiřazení** .

## <a name="step-4---assignments"></a>Krok 4 – přiřazení

1. Vyberte **požadované**, **dostupné pro zaregistrovaná zařízení**nebo **odinstalujte** přiřazení skupin pro sadu aplikací. Další informace najdete v tématech [Přidání skupin pro uspořádání uživatelů a zařízení](../fundamentals/groups-add.md) a [přiřazení aplikací do skupin pomocí Microsoft Intune](apps-deploy.md).
2. Kliknutím na **Další** zobrazte stránku **Revize + vytvořit** .

## <a name="step-5---review--create"></a>Krok 5 – přezkoumání a vytvoření

1. Zkontrolujte hodnoty a nastavení, které jste zadali pro sadu aplikací.
2. Po dokončení klikněte na **vytvořit** , aby se aplikace přidala do Intune.

    Zobrazí se okno s **přehledem** sady aplikací Office 365 Window 10, kterou jste vytvořili.

## <a name="deployment-details"></a>Podrobnosti o nasazení

Jakmile se zásada nasazení z Intune přiřadí cílovým počítačům prostřednictvím [zprostředkovatele CSP (Office Configuration Service Provider)](https://docs.microsoft.com/windows/client-management/mdm/office-csp), bude koncové zařízení automaticky stahovat instalační balíček z umístění *officecdn.Microsoft.com* . V adresáři *Program Files* se zobrazí dva adresáře:

![Instalační balíčky Office v adresáři Program Files](./media/apps-add-office365/office-folder.png)

V adresáři *systém Microsoft Office* se vytvoří nová složka, kde jsou uložené instalační soubory:

![Nová vytvořená složka v adresáři systém Microsoft Office Directory](./media/apps-add-office365/created-folder.png)

V adresáři *systém Microsoft Office 15* jsou uloženy instalační soubory nástroje Klikni a spusť sady Office. Instalace se spustí automaticky, pokud je vyžadován typ přiřazení:

![Kliknutím spustíte instalační soubory instalačního programu.](./media/apps-add-office365/clicktorun-files.png)

Instalace bude v tichém režimu, pokud je přiřazení sady O365 nakonfigurované podle požadavků. Po úspěšném dokončení instalace budou stažené instalační soubory odstraněny. Pokud je přiřazení nakonfigurované jako **dostupné**, aplikace Office se zobrazí v aplikaci Portál společnosti, takže koncoví uživatelé můžou instalaci aktivovat ručně.

## <a name="troubleshooting"></a>Odstraňování potíží
Intune používá [Nástroj pro nasazení Office](https://docs.microsoft.com/DeployOffice/overview-of-the-office-2016-deployment-tool) ke stažení a nasazení Office 365 ProPlus do klientských počítačů pomocí [sady Office 365 CDN](https://docs.microsoft.com/office365/enterprise/content-delivery-networks). Na základě doporučených postupů uvedených v článku [Správa koncových bodů Office 365](https://docs.microsoft.com/office365/enterprise/managing-office-365-endpoints) můžete zajistit, aby vaše síťová konfigurace mohla klientům přistupovat přímo k CDN místo směrování provozu prostřednictvím centrálních proxy serverů, aby nedocházelo k zbytečnému zavlečení latence.

Pokud narazíte na problémy s instalací nebo v době běhu, spusťte [průvodce podpora Microsoftu a obnovení pro Office 365](https://diagnostics.office.com) na cílovém zařízení.

### <a name="additional-troubleshooting-details"></a>Další podrobnosti o řešení potíží

Nemůžete-li nainstalovat aplikace O365 do zařízení, je nutné zjistit, zda se jedná o problém s intunem nebo s operačním systémem nebo Office. Pokud vidíte dvě složky *systém Microsoft Office* a v adresáři *Program Files* v zařízení se zobrazí *systém Microsoft Office 15* , můžete potvrdit, že Intune úspěšně iniciovalo nasazení. Pokud se tyto dvě složky nezobrazují v části *programové soubory*, měli byste potvrdit následující případy:

- Zařízení je správně zaregistrované do Microsoft Intune. 
- V zařízení je aktivní síťové připojení. Pokud je zařízení v režimu v letadle, je vypnuté nebo se nachází v umístění bez služby, zásada se nepoužije, dokud nebude navázáno připojení k síti.
- Jsou splněné požadavky na síť Intune i Office 365 a související rozsahy IP adres jsou dostupné v závislosti na následujících článcích:

  - [Požadavky na konfiguraci sítě a šířka pásma pro Intune](https://docs.microsoft.com/intune/network-bandwidth-use)
  - [Adresy URL a rozsahy IP adres pro Office 365](https://docs.microsoft.com/office365/enterprise/urls-and-ip-address-ranges)

- Této sadě aplikací O365 byly přiřazeny správné skupiny. 

Kromě toho Sledujte velikost adresáře *C:\Program Files\Microsoft Office\Updates\Download*. Instalační balíček stažený z cloudu Intune se uloží do tohoto umístění. Pokud se velikost nezvětšuje nebo se zvětšuje jenom velmi pomalu, doporučuje se, abyste provedli připojení k síti a šířku pásma.

Až se rozhodnete, že jak Intune, tak i síťová infrastruktura fungují podle očekávání, měli byste problém dále analyzovat z perspektivy operačního systému. Vezměte v úvahu následující podmínky:

- Cílové zařízení musí běžet ve Windows 10 Creators Update nebo novějším.
- Během nasazování aplikací Intune se neotevřou žádné existující aplikace Office.
- Existující verze Office MSI sady Office byly ze zařízení správně odebrány. Intune využívá Office Klikni a spusť, což není kompatibilní s Office MSI. Toto chování se dále zmiňuje v tomto dokumentu:<br>
  [Office nainstalované s kliknou a Instalační služba systému Windows na stejném počítači se nepodporuje.](https://support.office.com/article/office-installed-with-click-to-run-and-windows-installer-on-same-computer-isn-t-supported-30775ef4-fa77-4f47-98fb-c5826a6926cd)
- Přihlášený uživatel by měl mít oprávnění k instalaci aplikací do zařízení.
- Potvrďte, že neexistují žádné problémy založené na protokolech Windows Prohlížeč událostí protokolů **windows** -> **aplikacích**.
- Zachytit podrobné protokoly instalace Office během instalace Tuto akci provedete následovně:<br>
    1. Aktivujte podrobné protokolování pro instalaci Office na cílových počítačích. Chcete-li to provést, spusťte následující příkaz pro úpravu registru:<br>
        `reg add HKLM\SOFTWARE\Microsoft\ClickToRun\OverRide /v LogLevel /t REG_DWORD /d 3`<br>
    2. Znovu nasaďte sadu Office 365 do cílových zařízení.<br>
    3. Počkejte přibližně 15 až 20 minut a do složky **% TEMP%** a do složky **%windir%\temp** , řadit podle **data změny**, vyberte *{název počítače} – {timestamp}. soubory protokolu* , které jsou upravené podle vašeho reprodukci času.<br>
    4. Spuštěním následujícího příkazu zakažte podrobný protokol:<br>
        `reg delete HKLM\SOFTWARE\Microsoft\ClickToRun\OverRide /v LogLevel /f`<br>
        Podrobné protokoly můžou poskytovat podrobnější informace o procesu instalace.

## <a name="errors-during-installation-of-the-app-suite"></a>Chyby při instalaci sady aplikací

Informace o tom, jak zobrazit podrobné protokoly instalace, najdete v tématu [Jak povolit protokolování ULS pro Office 365](/office/troubleshoot/diagnostic-logs/how-to-enable-office-365-proplus-uls-logging) .

V následující tabulce jsou uvedené běžné kódy chyb, se kterými se můžete setkat, a jejich význam.

### <a name="status-for-office-csp"></a>Stav pro Office CSP

| Stav | Fáze | Popis |
|--------------------------------------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1460 (ERROR_TIMEOUT) | Stáhnout | Nepodařilo se stáhnout nástroj pro nasazení Office. |
| 13 (ERROR_INVALID_DATA) | - | Nelze ověřit podpis staženého nástroje pro nasazení Office. |
| Kód chyby z CertVerifyCertificateChainPolicy | - | Nezdařila se kontrola certifikace staženého nástroje pro nasazení Office. |
| 997 | WIP | Instalace |
| 0 | Po instalaci | Instalace proběhla úspěšně. |
| 1603 (ERROR_INSTALL_FAILURE) | - | Neúspěšná Kontrola požadavků, například: SxS (pokus o instalaci, když je nainstalováno 2016 MSI) verze mismatchOthers |
| 0x8000ffff (E_UNEXPECTED) | - | Pokus odinstalovat, když na počítači není technologie Office Klikni a spusť |
| 17002 | - | Scénář se nepodařilo dokončit (nainstalovat). Možné důvody: instalace zrušila zrušením userInstallation pomocí jiného instalačního místa na disku během ID jazyka installationUnknown. |
| 17004 | - | Neznámé skladové položky |


### <a name="office-deployment-tool-error-codes"></a>Kódy chyb nástroje pro nasazení Office

| Scénář | Návratový kód | Uživatelské rozhraní | Poznámka |
|------------------------------------------------------------------------------------------------------------------|---------------------------------------|----------------------------------------------------|------------------------------------|
| Pokus odinstalovat bez aktivní instalace Klikni a spusť | -2147418113, 0x8000ffff nebo 2147549183 | Kód chyby: 30088-1008Error kód: 30125-1011 (404) | Nástroj pro nasazení systému Office |
| Instalace, když je nainstalovaná verze MSI | 1603 | - | Nástroj pro nasazení systému Office |
| Instalace byla zrušena uživatelem nebo jinou instalací. | 17002 | - | Klikni a spusť |
| Pokus nainstalovat 64bitovou verzi na zařízení, na kterém je nainstalovaná 32bitová verze. | 1603 | - | Návratový kód nástroje pro nasazení Office |
| Pokus nainstalovat neznámou skladovou položku (případ neoprávněného použití Office CSP, protože je nutné předávat jenom platné skladové položky) | 17004 | - | Klikni a spusť |
| Nedostatek místa | 17002 | - | Klikni a spusť |
| Klienta s technologií Klikni a spusť se nepodařilo spustit (neočekávané) | 17000 | - | Klikni a spusť |
| U klienta s technologií Klikni a spusť se nepodařilo zařadit scénář do fronty (neočekávané) | 17001 | - | Klikni a spusť |

## <a name="next-steps"></a>Další kroky

- Pokud chcete sadu aplikací přiřadit k dalším skupinám, přečtěte si téma [přiřazení aplikací do skupin](/intune-azure/manage-apps/deploy-apps).
