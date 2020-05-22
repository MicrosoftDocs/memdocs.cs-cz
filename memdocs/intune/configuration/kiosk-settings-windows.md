---
title: Nastavení veřejného terminálu pro Windows 10 v Microsoft Intune – Azure | Microsoft Docs
description: Nakonfigurujte zařízení s Windows 10 (a novějšími) jako veřejné terminály s jednou aplikací a více aplikacemi, přizpůsobte nabídku Start, přidejte aplikace, zobrazte panel úloh a nakonfigurujte webový prohlížeč v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/21/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: ae89a939e35f68f55d2e63e7495a9b743cc0fa34
ms.sourcegitcommit: fb77170957f50aa386ff825fb4183b4fd9e3e488
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/22/2020
ms.locfileid: "83791770"
---
# <a name="windows-10-and-later-device-settings-to-run-as-a-kiosk-in-intune"></a>Nastavení zařízení s Windows 10 a novějším, která se mají spustit jako veřejný terminál v Intune

V zařízeních se systémem Windows 10 nebo novějším můžete tato zařízení nakonfigurovat tak, aby běžela v celoobrazovkovém režimu jedné aplikace nebo celoobrazovkovém režimu s více aplikacemi.

Tento článek obsahuje seznam a popis různých nastavení, která můžete řídit na zařízeních s Windows 10 a novějších. Jako součást řešení správy mobilních zařízení (MDM) pomocí těchto nastavení můžete nakonfigurovat zařízení s Windows 10 a novějším tak, aby běžela v celoobrazovkovém režimu.

Jako správce Intune můžete vytvořit a přiřadit tato nastavení k vašim zařízením.

Další informace o funkci veřejného terminálu Windows v Intune najdete v tématu [Konfigurace nastavení veřejného terminálu](kiosk-settings.md).

## <a name="before-you-begin"></a>Před zahájením

- [Vytvořte profil](kiosk-settings.md#create-the-profile).

- Tento profil veřejného terminálu přímo souvisí s profilem omezení zařízení, které vytvoříte pomocí [nastavení Microsoft Edge](device-restrictions-windows-10.md#microsoft-edge-browser)na veřejném terminálu. Shrnutí:

  1. Vytvořte tento profil veřejného terminálu pro spuštění zařízení v celoobrazovkovém režimu.
  2. Umožňuje vytvořit [profil omezení zařízení](device-restrictions-windows-10.md#microsoft-edge-browser)a nakonfigurovat konkrétní funkce a nastavení povolená v Microsoft Edge.

- Ujistěte se, že jsou všechny soubory, skripty a zástupci v místním systému. Další informace, včetně dalších požadavků na Windows, najdete v tématu [přizpůsobení a export počátečního rozložení](https://docs.microsoft.com/windows/configuration/customize-and-export-start-layout).

> [!IMPORTANT]
> Ujistěte se, že tento profil pro terminál přiřadíte ke stejným zařízením jako váš [profil Microsoft Edge](device-restrictions-windows-10.md#microsoft-edge-browser).

## <a name="single-app-full-screen-kiosk"></a>Jedna aplikace, celoobrazovkový terminál na celé obrazovce

Spustí na zařízení jenom jednu aplikaci.

- **Vyberte celoobrazovkový režim**: zvolte možnost **jediná aplikace, terminál na celé obrazovce**.

- **Typ přihlášení uživatele**: Vyberte typ účtu, ve kterém se aplikace spouští. Možnosti:

  - **Automatické přihlašování (Windows 10 verze 1803 a novější)**: Používejte veřejné terminály ve veřejných prostředích, která nevyžadují, aby se uživatel přihlásil, podobně jako účet Guest. Toto nastavení využívá [poskytovatele konfiguračních služeb AssignedAccess](https://docs.microsoft.com/windows/client-management/mdm/assignedaccess-csp).
  - **Účet místního uživatele**: Zadejte účet místního uživatele (v zařízení). Účet, který zadáte, se přihlaste k veřejnému terminálu.

- **Typ aplikace**: Vyberte typ aplikace. Možnosti:

  - **Přidat prohlížeč Microsoft Edge**: vyberte **prohlížeč Microsoft**Edge a zvolte **typ celoobrazovkového režimu Microsoft Edge**:

    - **Digitální/interaktivní podpis**: otevře stránku URL na celé obrazovce a zobrazí pouze obsah na tomto webu. [Nastavení digitální znaménka](https://docs.microsoft.com/windows/configuration/setup-digital-signage) poskytuje další informace o této funkci.
    - **Veřejné procházení (InPrivate)**: spouští omezené víceúrovňové verze Microsoft Edge. Uživatelé můžou procházet veřejně nebo ukončit jejich relaci procházení.

    Další informace o těchto možnostech najdete v tématu [nasazení celoobrazovkového režimu Microsoft Edge](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

    > [!NOTE]
    > Toto nastavení povolí prohlížeči Microsoft Edge na zařízení. Pokud chcete nakonfigurovat nastavení specifické pro Microsoft Edge, vytvořte profil omezení zařízení (**Devices**  >  **Konfigurace zařízení profily**  >  **vytvořit profil**  >  **Windows 10** pro platformu > **omezení zařízení**  >  **prohlížeč Microsoft Edge**). Seznam dostupných nastavení najdete v [prohlížeči Microsoft Edge](device-restrictions-windows-10.md#microsoft-edge-browser) .

  - **Přidat webový prohlížeč**na veřejném terminálu: vyberte **nastavení prohlížeče veřejného terminálu**. Tato nastavení řídí aplikaci webového prohlížeče na veřejném terminálu. Ujistěte se, že jste si z obchodu získali [aplikaci celoobrazovkového prohlížeče](https://businessstore.microsoft.com/store/details/kiosk-browser/9NGB5S5XG2KP) , přidejte ji do Intune jako [klientskou aplikaci](../apps/apps-add.md). Pak aplikaci přiřaďte k veřejnému zařízení.

    Zadejte následující nastavení:

    - **Výchozí adresa URL domovské stránky**: zadejte výchozí adresu URL, která se zobrazí po otevření prohlížeče veřejného terminálu, nebo při restartu prohlížeče. Zadejte například `http://bing.com` nebo `http://www.contoso.com`.

    - **Tlačítko Domů**: **Zobrazí ** nebo **skryje** tlačítko Domů Kiosk Browseru. Ve výchozím nastavení se tlačítko nezobrazuje.

    - **Navigační tlačítka**: **Zobrazí** nebo **skryje** tlačítka pro přechod vpřed nebo vzad. Ve výchozím nastavení se navigační tlačítka nezobrazují.

    - **Tlačítko pro ukončení relace**: **Zobrazí** nebo **skryje** tlačítko pro ukončení relace. Když je zobrazené a uživatel tlačítko vybere, dojde k výzvě pro ukončení relace. Po potvrzení prohlížeč vymaže všechny údaje o procházení (soubory cookie, mezipaměť atd.) a otevře výchozí adresu URL. Ve výchozím nastavení se tlačítko nezobrazuje.

    - **Aktualizovat prohlížeč po nečinnosti**: zadejte dobu nečinnosti, od 1-1440 minut, než se prohlížeč veřejného terminálu restartuje v neaktivním stavu. Doba nečinnosti je počet minut od poslední interakce uživatele. Ve výchozím nastavení je hodnota prázdná, což znamená, že neexistuje žádný časový limit nečinnosti.

    - **Povolené weby**: Toto nastavení použijte, pokud chcete povolit otevírání konkrétních webů. Jinými slovy, tuto funkci použijte k omezení nebo zabránění spouštění webů na zařízení. Můžete například povolit, aby se otevíraly všechny weby na `http://contoso.com`. Ve výchozím nastavení jsou povolené všechny weby.

      Pokud chcete povolit konkrétní weby, nahrajte soubor, který obsahuje seznam povolených webů na samostatných řádcích. Pokud soubor nepřidáte, jsou povolené všechny weby. Ve výchozím nastavení Intune umožňuje všechny subdomény webu. Například můžete zadat `sharepoint.com` doménu. Intune automaticky povoluje všechny subdomény, například `contoso.sharepoint.com` , `my.sharepoint.com` a tak dále. Nezadávejte zástupné znaky, například hvězdičku ( `*` ).

      Váš ukázkový soubor by se měl podobat následujícímu seznamu:

      `http://bing.com`  
      `https://bing.com`  
      `http://contoso.com`  
      `https://contoso.com`  
      `office.com`

    > [!NOTE]
    > Veřejné terminály s Windows 10 s povoleným přihlašováním pomocí prohlížeče veřejného terminálu Microsoftu musí používat licenci offline od Microsoft Store pro firmy. Důvodem je to, že automatické přihlašování používá místní uživatelský účet bez přihlašovacích údajů Azure Active Directory (AD). Licence Online proto nejde vyhodnotit. Další informace najdete v tématu [distribuce offline aplikací](https://docs.microsoft.com/microsoft-store/distribute-offline-apps).

  - **Přidat aplikaci pro Store**: vyberte **Přidat aplikaci ze Storu**a zvolte aplikaci ze seznamu.

    Nejsou v seznamu žádné aplikace? Přidejte aplikace pomocí postupu v části [Klientské aplikace](../apps/apps-add.md).

- **Zadejte časové období údržby pro restartování aplikací**: některé aplikace vyžadují restart k dokončení instalace aplikace nebo dokončení instalace aktualizací. **Vyžaduje** vytvoření časového období údržby. Pokud aplikace vyžaduje restart, během tohoto okna se restartuje.

  Dále zadejte:

  - **Čas spuštění časového období údržby**: vyberte datum a čas, kdy chcete spustit kontrolu klientů pro všechny aktualizace aplikací, které vyžadují restart. Výchozí počáteční čas je půlnoc nebo nula minut. Pokud je toto pole prázdné, aplikace se po instalaci aktualizace aplikace restartují v neplánovaném čase 3 dny.

  - **Opakování časového období údržby**: výchozí hodnota je denně. Vyberte, jak často se mají aktualizovat okna údržby pro aktualizace aplikací. Aby nedocházelo k neplánovanému restartování aplikace, doporučení je **denně**.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  [CSP ApplicationManagement/ScheduleForceRestartForUpdateFailures](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-scheduleforcerestartforupdatefailures)

## <a name="multi-app-kiosk"></a>Veřejný terminál s více aplikacemi

Aplikace v tomto režimu jsou k dispozici v nabídce Start. Tyto aplikace jsou jedinými aplikacemi, které může uživatel spustit. Pokud má aplikace závislost na jiné aplikaci, musí být v seznamu povolené aplikace zahrnutá obě. Například v aplikaci Internet Explorer 64-bit je závislá na aplikaci Internet Explorer 32-bit, takže je třeba umožnit možnost "C:\Program Files\internet Explorer\iexplore.exe" a "C:\Program Files (x86) \Internet Explorer\iexplore.exe". 

- **Vyberte celoobrazovkový režim**: Vyberte veřejný **terminál s více aplikacemi**.

- **Cílová zařízení s Windows 10 v režimu S**:
  - **Ano**: povoluje aplikace pro Store a aplikace AUMID v profilu veřejného terminálu. Nezahrnuje aplikace Win32.
  - **Ne**: umožňuje aplikace pro Store, aplikace Win32 a aplikace AUMID v profilu veřejného terminálu. Tento profil veřejného terminálu není nasazený do zařízení S režimem S.

- **Typ přihlášení uživatele**: Vyberte typ účtu, ve kterém se budou aplikace spouštět. Možnosti:

  - **Automatické přihlašování (Windows 10 verze 1803 a novější)**: Používejte veřejné terminály ve veřejných prostředích, která nevyžadují, aby se uživatel přihlásil, podobně jako účet Guest. Toto nastavení využívá [poskytovatele konfiguračních služeb AssignedAccess](https://docs.microsoft.com/windows/client-management/mdm/assignedaccess-csp).
  - **Účet místního uživatele**: **Přidejte** účet místního uživatele (v zařízení). Účet, který zadáte, se přihlaste k veřejnému terminálu.
  - **Uživatel nebo skupina Azure AD (Windows 10 verze 1803 a novější)**: vyberte **Přidat**a v seznamu zvolte uživatele nebo skupiny Azure AD. Můžete vybrat více uživatelů a skupin. Zvolením možnosti **Vybrat** uložte změny.
  - **Návštěvník HoloLens**: Účet návštěvníka je účtem hosta, který nevyžaduje žádné přihlašovací údaje uživatele ani ověřování, viz článek o [konceptech režimu sdíleného počítače](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts).

- **Prohlížeč a aplikace**: Přidejte aplikace, které se mají spustit v celoobrazovkovém zařízení. Nezapomeňte, že můžete přidat několik aplikací.

  :::image type="content" source="./media/kiosk-settings-windows/multi-app-kiosk-add-applications-browser.png" alt-text="Přidejte prohlížeče nebo aplikace do profilu veřejného terminálu s více aplikacemi v Microsoft Intune.":::  

  - **Browsers**

    - **Přidat Microsoft Edge**: Microsoft Edge se přidá do mřížky aplikace a všechny aplikace můžou běžet na tomto terminálu. Vyberte **typ beznabídkového režimu Microsoft Edge**:

      - **Normální režim (plná verze Microsoft Edge)**: spustí plnou verzi Microsoft Edge se všemi funkcemi pro procházení. Data a stav uživatele jsou ukládána mezi relacemi.
      - **Veřejné procházení (InPrivate)**: spouští vícevrstvou verzi Microsoft Edge InPrivate s přizpůsobeným prostředím pro veřejné terminály, které běží v režimu celé obrazovky.

      Další informace o těchto možnostech najdete v tématu [nasazení celoobrazovkového režimu Microsoft Edge](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

      > [!NOTE]
      > Toto nastavení povolí prohlížeči Microsoft Edge na zařízení. Pokud chcete nakonfigurovat nastavení specifické pro Microsoft Edge, vytvořte profil omezení zařízení (**Devices**  >  **profily konfigurace**zařízení  >  **vytvořit profil** > > **Windows 10** pro platformu > **zařízení omezení**  >   **prohlížeče Microsoft Edge**). Seznam dostupných nastavení najdete v [prohlížeči Microsoft Edge](device-restrictions-windows-10.md#microsoft-edge-browser) .

    - **Přidat webový prohlížeč**na veřejném terminálu: Tato nastavení ovládají aplikaci webového prohlížeče na veřejném terminálu. K nasazení aplikace webového prohlížeče do zařízení s beznabídkovým režimem použijte [klientské aplikace](../apps/apps-add.md).

      Zadejte následující nastavení:

      - **Výchozí adresa URL domovské stránky**: zadejte výchozí adresu URL, která se zobrazí po otevření prohlížeče veřejného terminálu, nebo při restartu prohlížeče. Zadejte například `http://bing.com` nebo `http://www.contoso.com`.

      - **Tlačítko Domů**: **Zobrazí ** nebo **skryje** tlačítko Domů Kiosk Browseru. Ve výchozím nastavení se tlačítko nezobrazuje.

      - **Navigační tlačítka**: **Zobrazí** nebo **skryje** tlačítka pro přechod vpřed nebo vzad. Ve výchozím nastavení se navigační tlačítka nezobrazují.

      - **Tlačítko pro ukončení relace**: **Zobrazí** nebo **skryje** tlačítko pro ukončení relace. Když je zobrazené a uživatel tlačítko vybere, dojde k výzvě pro ukončení relace. Po potvrzení prohlížeč vymaže všechny údaje o procházení (soubory cookie, mezipaměť atd.) a otevře výchozí adresu URL. Ve výchozím nastavení se tlačítko nezobrazuje.

      - **Aktualizovat prohlížeč po určité době nečinnosti**: Zadejte dobu nečinnosti (1 až 1 440 minut), než se Kiosk Browser restartuje a obnoví. Doba nečinnosti je počet minut od poslední interakce uživatele. Ve výchozím nastavení je hodnota prázdná, což znamená, že neexistuje žádný časový limit nečinnosti.

      - **Povolené weby**: Toto nastavení použijte, pokud chcete povolit otevírání konkrétních webů. Jinými slovy, tuto funkci použijte k omezení nebo zabránění spouštění webů na zařízení. Můžete například povolit, aby se otevíraly všechny weby na `contoso.com*`. Ve výchozím nastavení jsou povolené všechny weby.

        Pokud chcete povolit konkrétní weby, nahrajte soubor CSV, který obsahuje seznam povolených webů. Pokud soubor CSV nepřidáte, budou povolené všechny weby.

      > [!NOTE]
      > Veřejné terminály s Windows 10 s povoleným přihlašováním pomocí prohlížeče veřejného terminálu Microsoftu musí používat licenci offline od Microsoft Store pro firmy. Důvodem je to, že automatické přihlašování používá místní uživatelský účet bez přihlašovacích údajů Azure Active Directory (AD). Licence Online proto nejde vyhodnotit. Další informace najdete v tématu [distribuce offline aplikací](https://docs.microsoft.com/microsoft-store/distribute-offline-apps).

  - **Aplikace**

    - **Přidat aplikaci pro Store**: Přidejte aplikaci z Microsoft Storu pro firmy. Pokud nejsou zobrazené žádné aplikace, můžete je získat a [přidat do Intune](../apps/store-apps-windows.md). Můžete například přidat Kiosk Browser, Excel, OneNote a další.

    - **Přidat aplikaci Win32**: Aplikace Win32 je tradiční desktopová aplikace, jako je například Visual Studio Code nebo Google Chrome. Zadejte tyto vlastnosti:

      - **Název aplikace**: Povinné. Zadejte název aplikace.
      - **Místní cesta ke spustitelnému souboru aplikace**: povinné. Zadejte cestu ke spustitelnému souboru, například `C:\Program Files (x86)\Microsoft VS Code\Code.exe` nebo `C:\Program Files (x86)\Google\Chrome\Application\chrome.exe`.
      - **ID modelu uživatele aplikace (AUMID) pro aplikaci Win32**: Zadejte ID modelu uživatele aplikace (AUMID) aplikace Win32. Toto nastavení určuje rozložení nabídky Start na dlaždici na ploše. Pokud chcete získat toto ID, přečtěte si téma [Get-StartApps](https://docs.microsoft.com/powershell/module/startlayout/get-startapps?view=win10-ps).

    - **Přidat podle AUMID**: Tuto možnost použijte pro přidání aplikací pro Windows, například Poznámkového bloku nebo Kalkulačky. Zadejte tyto vlastnosti:

      - **Název aplikace**: Povinné. Zadejte název aplikace.
      - **ID modelu uživatele aplikace (AUMID)**: Povinné. Zadejte ID modelu uživatele aplikace (AUMID) aplikace pro Windows. Pokud chcete získat toto ID, přečtěte si článek o tom, [jak u nainstalované aplikace najít ID modelu uživatele aplikace](https://docs.microsoft.com/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app).

    - **AUTOLAUNCH**: volitelné. Po přidání aplikací a prohlížeče vyberte jednu aplikaci nebo prohlížeč, které se automaticky otevřou, když se uživatel přihlásí. Spustit se dá jenom jedna aplikace nebo prohlížeč.
    - **Velikost dlaždice**: Povinné. Po přidání aplikací vyberte malou, střední, širokou nebo velkou velikost dlaždice aplikace.

      :::image type="content" source="./media/kiosk-settings-windows/multi-app-kiosk-autolaunch-tiles.png" alt-text="Automatické spuštění aplikace nebo prohlížeče a výběr velikosti dlaždice v profilu veřejného terminálu s více aplikacemi v Microsoft Intune.":::

  > [!TIP]
  > Po přidání všech aplikací můžete změnit pořadí zobrazování tak, že na aplikace v seznamu kliknete a pomocí myši je přetáhnete, kam potřebujete.  

- **Použít alternativní počáteční rozložení**: vyberte **Ano** , pokud chcete zadat soubor XML, který popisuje, jak se aplikace objeví v nabídce Start, včetně pořadí aplikací. Tuto možnost použijte, pokud v nabídce Start potřebujete větší míru přizpůsobení. [Upravit a exportovat úvodní rozložení](https://docs.microsoft.com/windows/configuration/customize-and-export-start-layout) obsahuje doprovodné materiály a ukázkové XML.

- **Hlavní panel Windows**: U hlavního panelu si můžete vybrat, zda se má **zobrazit** nebo **skrýt**. Ve výchozím nastavení se hlavní panel nezobrazuje. Ikony, jako je ikona sítě Wi-Fi, se zobrazí, ale koncoví uživatelé je nemůžou změnit.

- **Povolení přístupu ke složce stažené soubory**: vyberte **Ano** , pokud chcete, aby uživatelé měli přístup ke složce stažené soubory v Průzkumníkovi Windows. Ve výchozím nastavení je přístup ke složce stažené soubory zakázán. Tato funkce se běžně používá pro koncové uživatele k přístupu k položkám staženým z prohlížeče.

- **Zadejte časové období údržby pro restartování aplikací**: některé aplikace vyžadují restart k dokončení instalace aplikace nebo dokončení instalace aktualizací. **Vyžaduje** vytvoření časového období údržby. Pokud aplikace vyžadují restart, restartují se v průběhu tohoto okna.

  Dále zadejte:

  - **Čas spuštění časového období údržby**: vyberte datum a čas, kdy chcete spustit kontrolu klientů pro všechny aktualizace aplikací, které vyžadují restart. Výchozí počáteční čas je půlnoc nebo nula minut. Pokud je toto pole prázdné, aplikace se po instalaci aktualizace aplikace restartují v neplánovaném čase 3 dny.

  - **Opakování časového období údržby**: výchozí hodnota je denně. Vyberte, jak často se mají aktualizovat okna údržby pro aktualizace aplikací. Aby nedocházelo k neplánovanému restartování aplikace, doporučení je **denně**.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  [CSP ApplicationManagement/ScheduleForceRestartForUpdateFailures](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-scheduleforcerestartforupdatefailures)

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md)a [sledujte jeho stav](device-profile-monitor.md).

Můžete také vytvořit profily celoobrazovkového pro zařízení s [Androidem](device-restrictions-android.md#kiosk), [Androidem Enterprise](device-restrictions-android-for-work.md#dedicated-devices)a [Windows holografickým pro firmy](kiosk-settings-holographic.md) .

Viz také [Nastavení veřejného terminálu pro jednu aplikaci](https://docs.microsoft.com/windows/configuration/kiosk-single-app) nebo [Nastavení veřejného terminálu s více aplikacemi](https://docs.microsoft.com/windows/configuration/lock-down-windows-10-to-specific-apps) v doprovodné příručce k Windows.
