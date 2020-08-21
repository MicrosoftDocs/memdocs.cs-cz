---
title: Vytváření aplikací
titleSuffix: Configuration Manager
description: Vytvářejte aplikace s typy nasazení, detekčními metodami a požadavky pro instalaci softwaru.
ms.date: 07/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 42dc0f65e9e3765de35e6db7f5272aeeaab63fa2
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695286"
---
# <a name="create-applications-in-configuration-manager"></a>Vytváření aplikací v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager aplikace definuje metadata o aplikaci. Aplikace má jeden nebo více typů nasazení. Mezi tyto typy nasazení patří instalační soubory a informace, které jsou nutné k instalaci softwaru do zařízení. Typ nasazení má také pravidla, jako jsou metody detekce a požadavky. Tato pravidla určují, kdy a jak klient software nainstaluje.  

Vytvářejte aplikace pomocí následujících metod:  

- Automatické vytvoření aplikace a typů nasazení načtením instalačních souborů aplikace:  
  - [Vytvoření aplikace](#bkmk_create) a [Automatické zjištění](#bkmk_auto-app) informací o aplikaci
  - [Vytvoření typu nasazení](#bkmk_create-dt) a [Automatické určení](#bkmk_auto-dt) informací o typu nasazení

- Ručně vytvořte aplikaci a pak přidejte typy nasazení později:  
  - [Vytvoření aplikace](#bkmk_create) a [Ruční zadání](#bkmk_manual-app) informací o aplikaci
  - [Vytvoření typu nasazení](#bkmk_create-dt) a [Ruční určení](#bkmk_manual-dt) informací o typu nasazení

- [Import aplikace](#bkmk_import) ze souboru  

Tento článek obsahuje také následující informace o konfiguraci typu nasazení:  

- [Obsah](#bkmk_dt-content)
- [Pořadí úloh](#bkmk_dt-ts)
- [Metoda detekce](#bkmk_dt-detect)
- [Činnost koncového uživatele](#bkmk_dt-ux)
- [Požadavky](#bkmk_dt-require)
- [Návratové kódy](#bkmk_dt-return)
- [Závislosti](#bkmk_dt-depend)

## <a name="create-an-application"></a><a name="bkmk_create"></a> Vytvoření aplikace  

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte položku **Správa aplikací**a vyberte uzel **aplikace** .  

2. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte možnost **vytvořit aplikaci**.  

Potom automaticky zjistí nebo ručně určí informace o aplikaci:  

- [Automatické zjišťování](#bkmk_auto-app) informací o aplikaci k vytvoření základní aplikace s jedním typem nasazení. Například Instalační služba systému Windows soubor, který nemá žádné závislosti nebo požadavky. Po vytvoření aplikace pomocí tohoto postupu ji podle potřeby upravte. Můžete přidávat nebo měnit typy nasazení a přidávat metody detekce, závislosti nebo požadavky.  

- [Ruční zadání](#bkmk_manual-app) informací o aplikaci pro vytváření složitějších aplikací. Definujte více než jeden typ nasazení, závislosti, metody detekce nebo požadavky.  

### <a name="automatically-detect-application-information"></a><a name="bkmk_auto-app"></a> Automaticky zjišťovat informace o aplikaci  

1. Na stránce **Obecné** v nástroji Průvodce vytvořením aplikace vyberte možnost **automaticky zjišťovat informace o této aplikaci z instalačních souborů**.  

2. V rozevíracím seznamu **typ** vyberte typ instalačního souboru aplikace, který chcete použít k detekci informací o aplikaci. Další informace o dostupných typech instalace najdete v tématu [typy nasazení podporované nástrojem Configuration Manager](create-applications.md#bkmk_deploy-types).  

3. Do pole **umístění** zadejte instalační soubor aplikace, který chcete použít k detekci informací o aplikaci. Toto umístění je buď síťová cesta ( `\\server\share\filename` ), nebo odkaz na Store. Musíte mít přístup k síťové cestě a ke všem podsložkám, které obsahují obsah aplikace.  

    > [!IMPORTANT]  
    > Když jako typ aplikace vyberete možnost **Instalační služba systému Windows ( \* soubor. msi)** , lokalita importuje všechny soubory v zadané složce. Pak tyto soubory pošle do distribučních bodů. Ujistěte se, že Zadaná složka obsahuje pouze soubory, které jsou nezbytné k instalaci aplikace. Microsoft testuje Configuration Manager pro podporu až 20 000 souborů v balíčku aplikace. Pokud má vaše aplikace více souborů, zvažte vytvoření více aplikací s menšími soubory.  

4. Na stránce **importovat informace** v nástroji Průvodce vytvořením aplikace zkontrolujte informace a pak vyberte **Další**. V případě potřeby vyberte **Předchozí** , vraťte se zpátky a opravte všechny chyby.  

5. Na stránce **Obecné informace** v nástroji Průvodce vytvořením aplikace zadejte následující informace:  

    > [!NOTE]  
    > Pokud Configuration Manager automaticky detekuje tyto informace z instalačních souborů aplikace, je zde již naplněna. Navíc se mohou zobrazené možnosti lišit v závislosti na typu vytvářené aplikace.  

    - Obecné informace o aplikaci, například **název**aplikace, **Komentáře správce**, **Vydavatel**a **verze softwaru**. Chcete-li najít aplikaci v konzole Configuration Manager, zadejte **volitelný odkaz**nebo vyberte **kategorii správy**.  

    - **Instalační program**: Určete instalační program a všechny požadované vlastnosti, které jsou potřeba k instalaci typu nasazení aplikace.  

        > [!TIP]  
        > Pokud se instalační program nezobrazí, klikněte na tlačítko **Procházet** a přejděte do umístění instalačního programu.  

    - **Chování při instalaci**: vyberte jednu ze tří možností pro způsob, jakým Configuration Manager nainstaluje tento typ nasazení. Další informace o těchto možnostech najdete v tématu [činnost koncového uživatele](#bkmk_dt-ux).  

    - **Použít automatické připojení VPN (Pokud je nakonfigurované)**: Pokud jste nasadili profil sítě VPN do zařízení, na kterém uživatel spouští aplikaci, připojte síť VPN při spuštění aplikace. Tato možnost je určena pouze pro Windows 8.1 a Windows Phone 8,1. Pokud v zařízeních Windows Phone 8,1 nasadíte více než jeden profil sítě VPN do zařízení, automatické připojení VPN se nepodporuje. Další informace najdete v tématu [Profily sítě VPN](../../protect/deploy-use/vpn-profiles.md).  

    - **Zřídit tuto aplikaci pro všechny uživatele na zařízení**<!--1358310-->: Zřízení aplikace s balíčkem aplikace pro Windows pro všechny uživatele v zařízení. Další informace najdete v tématu [vytváření aplikací pro Windows](../get-started/creating-windows-applications.md#bkmk_provision).  

       > [!Tip]  
       > Pokud upravujete existující aplikaci, toto nastavení je na kartě **činnost koncového uživatele** vlastností typu nasazení balíčku aplikace systému Windows.  

6. Klikněte na tlačítko **Další**, na stránce **Souhrn** zkontrolujte informace o aplikaci a pak dokončete Průvodce vytvořením aplikace.  

Nová aplikace se nyní zobrazí v uzlu **aplikace** konzoly Configuration Manager. Dokončili jste vytváření aplikace.

Chcete-li přidat další typy nasazení nebo nakonfigurovat další nastavení, přečtěte si téma [Vytvoření typů nasazení pro aplikaci](#bkmk_create-dt).  

### <a name="manually-specify-application-information"></a><a name="bkmk_manual-app"></a> Ruční zadání informací o aplikaci  

1. Na stránce **Obecné** v nástroji Průvodce vytvořením aplikace vyberte možnost **ručně zadat informace o aplikaci**a pak zvolte možnost **Další**.  

2. Zadejte **Obecné informace** o aplikaci:  

    - **Název** aplikace je povinný a musí mít méně než 256 znaků.  

    - **Komentáře správce**, **Vydavatel**a **verze softwaru** jsou další metadata k dalšímu popisu aplikace.  

    - Chcete-li najít aplikaci v konzole Configuration Manager, zadejte **volitelný odkaz**nebo vyberte **kategorii správy**.  

    - **Datum publikování**  

    - Vyberte uživatele nebo skupiny zodpovědné za tuto aplikaci jako **vlastníky** a **Kontakty podpory**. Ve výchozím nastavení jsou tyto hodnoty nastaveny na vaše uživatelské jméno.  

3. Na stránce **Centrum softwaru** v nástroji Průvodce vytvořením aplikace zadejte následující informace:  

    > [!Note]  
    > Ve verzi 1902 a novější se tato stránka jmenovala jako **Katalog aplikací**.

    - **Vybraný jazyk**: v rozevíracím seznamu vyberte verzi jazyka aplikace, kterou chcete nastavit. Výběrem možnosti **Přidat/odebrat** můžete nastavit další jazyky pro tuto aplikaci.  

    - **Lokalizovaný název aplikace**: zadejte název aplikace ve vybraném jazyce.  

        > [!IMPORTANT]  
        > Pro každou jazykovou verzi, kterou jste nastavili, se vyžaduje lokalizovaný název aplikace.  

    - **Kategorie uživatelů**: zvolte **Upravit** a zadejte kategorie aplikací ve vybraném jazyce. Uživatelé centra softwaru tyto kategorie používají k filtrování a řazení aplikací.  

        > [!Note]  
        > Ve verzi 1902 a starší se kategorie uživatelů vztahují jenom na dostupná nasazení do kolekcí uživatelů. Pokud je aplikace nasazena do kolekce počítačů, kategorie uživatelů budou ignorovány.
        >
        > Počínaje verzí 1906 se kategorie uživatelů pro nasazení aplikací cílené na zařízení zobrazují jako filtry v centru softwaru. Tato nasazení mohou být buď k dispozici, nebo požadovaná.
        >
        > <!-- 4726793 -->Přejmenování nebo odstranění kategorie se automaticky nevztahují na aplikace s touto kategorií. Tyto změny se použijí při další revizi aplikace. Pokud chcete tento problém obejít, přejmenujte nebo odstraňte:
        >
        > - Nejdřív zrušte zaškrtnutí políčka pro kategorii na libovolné aplikaci, která na ni odkazuje. Pak použijte tuto změnu, která aplikaci upraví.
        >     - Místo akce přejmenování vytvořte novou kategorii s novým názvem a přidejte do relevantních aplikací novou kategorii.
        >     - Po úpravě aplikací můžete kategorii odstranit.

    - **Uživatelská dokumentace**: zadejte umístění souboru, ze kterého můžou uživatelé centra softwaru získat další informace o této aplikaci. Toto umístění je adresa webu nebo cesta k síti a název souboru. Ujistěte se, že uživatelé mají k tomuto umístění přístup.  

    - **Text odkazu**: zadejte text, který se zobrazí místo "Další informace" při zadání dokumentace uživatele.  

    - **Adresa URL ochrany osobních údajů**: zadejte adresu webu k prohlášení o zásadách ochrany osobních údajů pro danou aplikaci.  

    - **Lokalizovaný popis**: zadejte popis této aplikace ve vybraném jazyce.  

    - **Klíčová slova**: Zadejte seznam klíčových slov ve vybraném jazyce. Tato klíčová slova pomohou uživatelům centra softwaru Hledat aplikace.  

    - **Ikona**: vyberte **Procházet** a vyberte ikonu pro tuto aplikaci. Pokud neurčíte ikonu, Configuration Manager použije výchozí ikonu. Ikony můžou mít rozměry v pixelech až 512x512.  

4. Na stránce **typy nasazení** v nástroji Průvodce vytvořením aplikace vyberte možnost **Přidat** a vytvořte nový typ nasazení. Další informace najdete v tématu [Vytvoření typů nasazení pro aplikaci](#bkmk_create-dt).  

5. Klikněte na tlačítko **Další**, na stránce **Souhrn** zkontrolujte informace o aplikaci a pak dokončete Průvodce vytvořením aplikace.  

Nová aplikace se nyní zobrazí v uzlu **aplikace** konzoly Configuration Manager.  

## <a name="create-deployment-types-for-the-application"></a><a name="bkmk_create-dt"></a> Vytvoření typů nasazení pro aplikaci  

Pokud [automaticky zjistíte informace o aplikaci](#bkmk_auto-app), možná nebudete muset dokončit některé kroky v této části.  

> [!Note]  
> Po zobrazení vlastností existujícího typu nasazení budou v následujících oddílech odpovídat kartám okna vlastnosti typu nasazení:  
>
> - [Obsah](#bkmk_dt-content)
> - [Pořadí úloh](#bkmk_dt-ts)
> - [Metoda detekce](#bkmk_dt-detect)
> - [Činnost koncového uživatele](#bkmk_dt-ux)
> - [Požadavky](#bkmk_dt-require)
> - [Návratové kódy](#bkmk_dt-return)
> - [Závislosti](#bkmk_dt-depend)
>  
> Informace o kartě **chování při instalaci** u vlastností typu nasazení najdete v tématu [Zkontrolujte spouštění spustitelných souborů](deploy-applications.md#bkmk_exe-check).  

### <a name="start-the-create-deployment-type-wizard"></a>Spuštění Průvodce vytvořením typu nasazení  

Existují tři způsoby, jak spustit Průvodce vytvořením typu nasazení:

- **V uzlu aplikace**: v konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** , rozbalte položku **Správa aplikací**a vyberte uzel **aplikace** . Vyberte aplikaci a pak na pásu karet vyberte **vytvořit typ nasazení** .  

- **Při vytváření aplikace**: při [ručním zadání informací o aplikaci](#bkmk_manual-app) v Průvodci vytvořením aplikace vyberte na stránce typy nasazení možnost **Přidat** .  

- **Z vlastností aplikace**: Vyberte existující aplikaci v uzlu **aplikace** a vyberte **vlastnosti**. Přepněte na kartu **typy nasazení** a vyberte **Přidat**.

Pak použijte jeden z následujících postupů k [Automatické identifikaci](#bkmk_auto-dt) nebo [ručnímu určení](#bkmk_manual-dt) informací o typu nasazení.  

### <a name="automatically-identify-deployment-type-information"></a><a name="bkmk_auto-dt"></a> Automaticky identifikovat informace o typu nasazení  

1. Na stránce **Obecné** v Průvodci vytvořením typu nasazení:  

    1. Vyberte **typ** instalačního souboru aplikace, aby se zjistily informace o typu nasazení.  

    2. Vyberte možnost **automaticky zjišťovat informace o tomto typu nasazení z instalačních souborů**.  

    3. Do pole **umístění** zadejte instalační soubor aplikace, který chcete použít k detekci informací o typu nasazení. Toto umístění je buď síťová cesta ( `\\server\share\filename` ), nebo odkaz na Store. Musíte mít přístup k síťové cestě a ke všem podsložkám, které obsahují obsah aplikace.  

2. Na stránce **importovat informace** v Průvodci vytvořením typu nasazení zkontrolujte informace a pak vyberte **Další**. V případě potřeby vyberte **Předchozí** , vraťte se zpátky a opravte všechny chyby.  

3. Na stránce **Obecné informace** v nástroji Průvodce vytvořením typu nasazení zadejte následující informace:  

    > [!NOTE]  
    > Pokud byly některé informace o typu nasazení dříve načteny z instalačních souborů aplikace, mohou se již na této stránce nacházet. Kromě toho se můžou zobrazené možnosti lišit v závislosti na typu nasazení, který vytváříte.  

    - **Obecné informace** o typu nasazení:  
        - **Název** je povinný.  

        - **Komentáře správce** k dalšímu popisu  

        - **Jazyky** , které jsou k dispozici  

    - **Instalační program**: Určete instalační program a všechny vlastnosti, které jsou potřeba k instalaci typu nasazení.  

    - **Chování při instalaci**: vyberte jednu ze tří možností pro způsob, jakým Configuration Manager nainstaluje tento typ nasazení. Další informace o těchto možnostech najdete v tématu [činnost koncového uživatele](#bkmk_dt-ux).  

    - **Použít automatické připojení VPN (Pokud je nakonfigurované)**: Pokud jste nasadili profil sítě VPN do zařízení, na kterém uživatel spouští aplikaci, připojte síť VPN při spuštění aplikace. Tato možnost je určena pouze pro Windows 8.1 a Windows Phone 8,1. Pokud v zařízeních Windows Phone 8,1 nasadíte více než jeden profil sítě VPN do zařízení, automatické připojení VPN se nepodporuje. Další informace najdete v tématu [Profily sítě VPN](../../protect/deploy-use/vpn-profiles.md).  

4. Klikněte na tlačítko **Další**a potom pokračujte na [Možnosti obsahu typu nasazení](#bkmk_dt-content).  

### <a name="manually-specify-the-deployment-type-information"></a><a name="bkmk_manual-dt"></a> Zadat informace o typu nasazení ručně  

1. Na stránce **Obecné** v nástroji Průvodce vytvořením typu nasazení vyberte v rozevíracím seznamu **typ** možnost Typ instalačního souboru aplikace pro tento typ nasazení.

2. Vyberte možnost **ručně zadat informace o typu nasazení**a potom vyberte možnost **Další**.

3. Na stránce **Obecné informace** v nástroji Průvodce vytvořením typu nasazení zadejte **název** typu nasazení. Volitelně můžete zadat **Komentáře správce**, vybrat **jazyky** pro tento typ nasazení a pak vybrat **Další**.  

4. Pokračovat na [Možnosti obsahu typu nasazení](#bkmk_dt-content).  

### <a name="deployment-type-content-options"></a><a name="bkmk_dt-content"></a> Možnosti **obsahu** typu nasazení  

Na stránce **obsah** zadejte následující informace:  

> [!Note]  
> Když zobrazíte vlastnosti existujícího typu nasazení, některé z těchto možností se zobrazí na kartě **obsah** a některé na kartě **programy** .  

- **Umístění obsahu**: zadejte umístění obsahu pro tento typ nasazení nebo klikněte na tlačítko **Procházet** a vyberte složku obsahu typu nasazení.  

    > [!IMPORTANT]  
    > Systémový účet počítače serveru lokality musí mít oprávnění k zadanému umístění obsahu.  

  - **Zachovat obsah v mezipaměti klienta**: klient Configuration Manager neomezeně ukládá do mezipaměti obsah typu nasazení. Klient uchovává obsah i v případě, že je aplikace už nainstalovaná. Tato možnost je užitečná u některých nasazení, jako je například software založený na Instalační služba systému Windows. Instalační služba systému Windows potřebuje místní kopii zdrojového obsahu pro použití aktualizací. Tato možnost zmenší dostupné místo v mezipaměti. Pokud vyberete tuto možnost, může dojít k selhání velkého nasazení později, pokud v mezipaměti není dostatek volného místa.  

- **Instalační program**: zadejte název instalačního programu a požadované parametry instalace.  

  - **Zahájení instalace v**: Volitelně zadejte složku, která má instalační program pro typ nasazení. Tato složka může představovat absolutní cestu klienta nebo cestu ke složce distribučního bodu, která obsahuje instalační soubory.  

- **Odinstalační program**: Volitelně zadejte název odinstalačního programu a všech požadovaných parametrů.  

  - **Odinstalace byla zahájena v**: Volitelně zadejte složku, která obsahuje odinstalační program pro typ nasazení. Tato složka může být absolutní cesta na straně klienta. Může to být také relativní cesta k distribučnímu bodu složky s balíčkem.  

- **Opravný program**: pro instalační služba systému Windows typy nasazení instalačního programu skriptů volitelně zadejte název opravného programu a všechny požadované parametry.<!--1357866-->  

  - **Opravit začít v**: Volitelně můžete zadat složku, která má opravný program pro typ nasazení. Tato složka může být absolutní cesta na straně klienta. Může to být také relativní cesta k distribučnímu bodu složky s balíčkem.  

- **Spustit instalaci a odinstalační program jako 32 proces na 64 klientech**: k spuštění instalačního programu pro typ nasazení použijte umístění souboru a registru v počítačích 32 se systémem Windows.  

#### <a name="deployment-type-properties-content-options"></a>Vlastnosti typu nasazení – možnosti **obsahu**

Když zobrazíte vlastnosti typu nasazení, na kartě **obsah** se zobrazí následující možnosti:

- **Nastavení obsahu pro odinstalaci**:  

  - **Stejné jako obsah instalace**: Pokud je obsah instalace a odinstalace stejný, vyberte tuto možnost. Tato možnost je výchozí.  

  - **Bez obsahu pro odinstalaci**: Pokud vaše aplikace nepotřebuje obsah pro odinstalaci, vyberte tuto možnost.  

  - **Liší od obsahu instalace**: Pokud se obsah odinstalace liší od obsahu instalace, vyberte tuto možnost.  

    - **Umístění obsahu odinstalace**: zadejte síťovou cestu k obsahu, který se používá k odinstalaci aplikace.  

- **Umožňuje klientům používat distribuční body z výchozí skupiny hranic lokality**: Určete, jestli by klienti měli stáhnout a nainstalovat software z distribučního bodu ve výchozí skupině hranic lokality, když obsah není dostupný z distribučního bodu v aktuálních nebo sousedních skupinách hranic.  

- **Možnosti nasazení**: Určete, jestli by klienti měli aplikaci stáhnout, když použijí distribuční bod ze souseda nebo výchozí skupiny hranic lokality.  

- **Povolit klientům sdílet obsah s ostatními klienty ve stejné podsíti:** Určete, jestli se má povolit použití funkce BranchCache pro stahování obsahu. Další informace najdete v tématu [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). Služba BranchCache je na klientech vždy povolena. Toto nastavení bylo odebráno ve verzi 1802, protože klienti používají službu BranchCache, pokud je distribuční bod podporuje.  

### <a name="deployment-type-task-sequence-options"></a><a name="bkmk_dt-ts"></a> Možnosti **pořadí úloh** typ nasazení

<!--3555953-->

Další informace o typu nasazení pořadí úloh počínaje verzí 2002 najdete v tématu [typ nasazení pořadí úloh](../get-started/creating-windows-applications.md#bkmk_tsdt).

Na stránce **pořadí úloh** zadejte následující informace:

- **Pořadí úloh Instalace**: Vyberte pořadí úloh, které spustí proces instalace této aplikace.

- **Odinstalace pořadí úkolů** (volitelné): vyberte sekvenci úloh, která odebere tuto aplikaci.

> [!TIP]  
> Pokud se pořadí úkolů v seznamu nezobrazí, dvakrát ověřte, že neobsahují žádné kroky pro nasazení operačního systému ani upgrade operačního systému. Ověřte také, že není označena jako vysoce ovlivněné pořadí úkolů. Další informace najdete v části požadavky pro [typ nasazení pořadí úloh](../get-started/creating-windows-applications.md#bkmk_tsdt).

### <a name="deployment-type-detection-method-options"></a><a name="bkmk_dt-detect"></a> Možnosti **metody detekce** typu nasazení

Tento postup nastaví metodu detekce, která označuje přítomnost typu nasazení. Jinými slovy, bez ohledu na to, jestli je v zařízení s Windows už aplikace nainstalovaná. K vytvoření metody detekce použijte jednu ze dvou následujících metod:

- [Konfigurovat pravidla pro detekci přítomnosti tohoto typu nasazení](#bkmk_detect-rule)
- [Pro zjištění přítomnosti tohoto typu nasazení použít vlastní skript](#bkmk_detect-script)

#### <a name="configure-rules-to-detect-the-presence-of-this-deployment-type"></a><a name="bkmk_detect-rule"></a> Konfigurovat pravidla pro detekci přítomnosti tohoto typu nasazení

1. Na stránce **Metoda detekce** je ve výchozím nastavení vybrána možnost **Konfigurovat pravidla pro zjištění přítomnosti tohoto typu nasazení** . Vyberte možnost **Přidat klauzuli**.  

2. V dialogovém okně **pravidlo detekce** vyberte **Typ nastavení** pro zjištění přítomnosti typu nasazení:  

    - **Systém souborů**: zjištění, zda zadaný soubor nebo složka existují v zařízení. Tato detekce indikuje, že je aplikace nainstalovaná. Zadejte následující další podrobnosti:  

        - **Typ**: vyberte, jestli se jedná o soubor nebo složku.  

        - **Cesta** (povinné): zadejte nebo vyhledejte místní cestu k zařízení, které obsahuje soubor nebo složku. Například, `C:\Program Files`. Nelze zadat sdílenou cestu k síti. Pokud vyberete **Procházet**, přejděte do místního systému souborů nebo se připojte k zástupci, který chcete procházet.  

        - **Název souboru nebo složky** (povinné): zadejte konkrétní název souboru nebo složky, který se má zjistit ve výše uvedené cestě. Pokud klient zjistí tento soubor nebo složku v zařízení, považuje aplikace za nainstalovanou na zařízení.  

        - **Tento soubor nebo složka jsou přidruženy k 32 bitové aplikaci v systémech 64**: klient nejprve kontroluje 32 umístění souborů pro zadaný soubor nebo složku. Pokud se soubor nebo složka nenajde, klient vyhledá 64 umístění.  

    - **Registr**: zjišťuje, zda zadaný klíč registru nebo hodnota registru existují v klientském zařízení. Tato detekce indikuje, že je aplikace nainstalovaná. Zadejte následující další podrobnosti:  

        - **Podregistr** (povinné): z rozevíracího seznamu vyberte podregistr registru. Například, `HKEY_LOCAL_MACHINE`.  

        - **Key** (povinné): Zadejte klíč registru, ve kterém se má hledat ve výše uvedeném podregistru. Například, `SOFTWARE\Microsoft\Office`.  

        - **Hodnota** (volitelné): zadejte konkrétní hodnotu, která se má zjistit ve výše uvedeném klíči. Pokud chcete, aby klient rozpoznal (výchozí) hodnotu, povolte možnost **použít (výchozí) hodnotu klíče registru pro detekci**. Když zadáte hodnotu nebo povolíte tuto možnost, budete muset vybrat **datový typ**.  

        - **Tento klíč registru je přidružen k 32 bitové aplikaci v systémech 64**: tuto možnost vyberte, pokud chcete pro zadaný klíč registru nejprve ověřit, zda neexistují umístění registru pro systém 32. Pokud klíč registru nenajde, klient hledá 64 umístění.  

    - **Instalační služba systému Windows**: zjištění, zda zadaný Instalační služba systému Windows soubor existuje v klientském zařízení. Tato detekce indikuje, že je aplikace nainstalovaná. Zadejte **kód produktu** MSI, který se má rozpoznat na klientovi. Pokud vyberete **Procházet**, zvolte soubor MSI, ze kterého chcete číst kód produktu.

3. V dolní části okna pravidla detekce určete, jestli položka musí existovat, nebo splnit pravidlo. Pokud například zjistíte pomocí souboru, je ve výchozím nastavení vybrána následující možnost: **v cílovém systému musí existovat nastavení systému souborů, aby bylo indikováno přítomnosti této aplikace**. Vyberte druhou možnost pro vytvoření pravidla pro zjišťování na základě vlastností souboru nebo složky. Tyto vlastnosti zahrnují datum změny, datum vytvoření, verzi nebo velikost. Tato kritéria pravidla se liší pro každý typ nastavení.  

4. Kliknutím na **tlačítko OK** zavřete dialogové okno **pravidlo detekce** .  

Když vytvoříte více než jednu metodu detekce pro typ nasazení, můžete seskupit klauzule dohromady a vytvořit složitější logiku.  

#### <a name="group-detection-clauses-optional"></a>Klauzule detekce skupiny *(volitelné)*

1. Vytvořte tři nebo více klauzulí metod zjišťování pro typ nasazení.  

2. Vyberte dvě nebo více po sobě jdoucích klauzulí a pak vyberte **Skupina**. V přidružených sloupcích se zobrazí závorky, které ukazují, kde se skupina spouští a končí.  

    Příklad:

    | Konektor  |  ( | Klauzule           |  )  |
    |------------|----|------------------|-----|
    |            |    | Kód produktu MSI |     |
    | Nebo         | (  | Soubor1. text existuje|     |
    | And        |    | file2.txt existuje | )   |

3. Pokud chcete skupinu odebrat, vyberte seskupené klauzule a pak vyberte zrušit **seskupení**.  

*Pokračujte* k další části týkající se použití vlastního skriptu jako metody detekce. Nebo *přejděte* k možnosti [uživatelského prostředí](#bkmk_dt-ux) pro typ nasazení.

#### <a name="use-a-custom-script-to-check-for-the-presence-of-a-deployment-type"></a><a name="bkmk_detect-script"></a> Zjištění přítomnosti typu nasazení pomocí vlastního skriptu  

1. Na stránce **Metoda detekce** zaškrtněte políčko **pro zjištění přítomnosti tohoto typu nasazení použít vlastní skript** . Pak vyberte **Edit** (Upravit).  

2. V dialogovém okně **Editor skriptů** vyberte **typ skriptu** pro zjištění typu nasazení: PowerShell, VBScript nebo JScript.  

    > [!Note]  
    > Když se skript prostředí Windows PowerShell spustí jako metoda detekce aplikace, klient Configuration Manager volá PowerShell s `-NoProfile` parametrem. Tato možnost spustí PowerShell bez profilů. Profil PowerShellu je skript, který se spustí při spuštění PowerShellu. <!--3607762-->  

3. Do pole **obsah skriptů** zadejte skript, který chcete použít, nebo vložte obsah existujícího skriptu do něj. Zvolením možnosti **otevřít** přejděte na existující uložený skript. Chcete-li odebrat text v poli obsah skriptu, vyberte možnost **Zrušit** . V případě potřeby povolte možnost **Spustit skript jako 32 proces na 64 klientech**.  

    > [!NOTE]  
    > Maximální velikost skriptu je 32 KB.  

4. Vyberte **OK** a uložte skript a zavřete dialogové okno **Editor skriptů** . Zpět v Průvodci vytvořením typu nasazení se pole **typ skriptu** a **Délka skriptu** aktualizují o podrobnosti o vašem skriptu.

#### <a name="about-custom-script-detection-methods"></a>Informace o metodách detekce vlastních skriptů  

Configuration Manager kontroluje výsledky ze skriptu. Přečte hodnoty, které skript zapsal do standardního streamu výstupu (STDOUT), standardního streamu chyb (STDERR) a do ukončovacího kódu. Pokud se skript ukončí s nenulovou hodnotou, skript se nezdařil a stav detekce aplikace je *Neznámý*. Pokud je ukončovací kód nulový a STDOUT obsahuje data, je *nainstalován*stav detekce aplikace.

> [!TIP]
> Pokud při psaní skriptu detekce vrátíte nulový ukončovací kód, ale nevrátí výstup (data v STDOUT), aplikace se nerozpozná jako nainstalovaná. Další informace najdete v následujících příkladech.

Pomocí následujících tabulek ověřte, zda je aplikace nainstalována z výstupu skriptu:  

##### <a name="zero-exit-code"></a>Nulový ukončovací kód

|STDOUT|STDERR|Výsledek skriptu|Stav detekce aplikace|
|---------|---------|---------|---------|
|Obsahovat|Obsahovat|Success|Nenainstalováno|
|Obsahovat|Není prázdné|Selhání|Neznámý|
|Není prázdné|Obsahovat|Success|Nainstalovaný|
|Není prázdné|Není prázdné|Success|Nainstalovaný|

##### <a name="non-zero-exit-code"></a>Nenulový ukončovací kód

|STDOUT|STDERR|Výsledek skriptu|Stav detekce aplikace|
|---------|---------|---------|---------|
|Obsahovat|Obsahovat|Selhání|Neznámý|
|Obsahovat|Není prázdné|Selhání|Neznámý|
|Není prázdné|Obsahovat|Selhání|Neznámý|
|Není prázdné|Není prázdné|Selhání|Neznámý|

##### <a name="examples"></a>Příklady

K zápisu vlastních skriptů detekce aplikace použijte následující příklady PowerShellu/VBScript:  

**Příklad 1**: skript vrátí ukončovací kód, který není nula. Tento kód indikuje, že se skript nepodařilo úspěšně spustit. V tomto případě je stav detekce aplikace neznámý.  

``` PowerShell
Exit 1
```

``` VBScript
WScript.Quit(1)
```

**Příklad 2**: skript vrátí ukončovací kód nula, ale hodnota stderr není prázdná. Tento výsledek indikuje, že se skript nepodařilo úspěšně spustit. V tomto případě je stav detekce aplikace neznámý.  

``` PowerShell
Write-Error "Script failed"
Exit 0
```

``` VBScript
WScript.StdErr.Write "Script failed"
WScript.Quit(0)
```

**Příklad 3**: skript vrátí ukončovací kód nula, který indikuje, že byl úspěšně spuštěn. Hodnota pro STDOUT je však prázdná, což znamená, že aplikace není nainstalována.  

``` PowerShell
Exit 0
```

``` VBScript
WScript.Quit(0)
```

**Příklad 4**: skript vrátí ukončovací kód nula, který indikuje, že byl úspěšně spuštěn. Hodnota pro STDOUT není prázdná, což znamená, že je aplikace nainstalovaná.  

``` PowerShell
Write-Host "The application is installed"
Exit 0
```

``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.Quit(0)
```

**Příklad 5**: skript vrátí ukončovací kód nula, který indikuje, že byl úspěšně spuštěn. Hodnoty pro STDOUT a STDERR nejsou prázdné, což znamená, že je aplikace nainstalovaná.  

``` PowerShell
Write-Host "The application is installed"
Write-Error "Completed"
Exit 0
```

``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.StdErr.Write "Completed"
WScript.Quit(0)
```

### <a name="deployment-type-user-experience-options"></a><a name="bkmk_dt-ux"></a> Možnosti **uživatelského prostředí** typu nasazení

Tato nastavení určují, jak klient aplikace nainstaluje do zařízení a co se uživateli zobrazí.  

Na stránce **Činnost koncového uživatele** zadejte následující informace:  

- **Chování při instalaci**: v rozevíracím seznamu vyberte jednu z následujících možností:  

  - **Nainstalovat pro uživatele**: klient nainstaluje aplikaci jenom pro uživatele, na kterého aplikaci nasadíte.  

  - **Nainstalovat pro systém**: klient nainstaluje aplikaci jenom jednou. Je k dispozici pro všechny uživatele.  

  - **Nainstalovat pro systém, pokud je prostředkem zařízení. v opačném případě nainstalujte pro uživatele**: Pokud aplikaci nasadíte do zařízení, klient ji nainstaluje pro všechny uživatele. Pokud nasadíte aplikaci pro uživatele, klient ji nainstaluje jenom pro tohoto uživatele.  

- **Požadavek na přihlášení**: vyberte jednu z následujících možností:  

  - **Pouze je-li přihlášen nějaký uživatel**  

  - **Bez ohledu na to, jestli je uživatel přihlášený**  

  - **Pouze v případě, že není přihlášen žádný uživatel**  

    > [!NOTE]  
    > Tato možnost je standardně **určena pouze v případě, že je uživatel přihlášen**. Pokud v rozevíracím seznamu **chování instalace** vyberete **nainstalovat pro uživatele** , tuto možnost nemůžete změnit.  

- **Viditelnost instalačního programu**: Určete režim, ve kterém se typ nasazení spustí na klientských zařízeních. Vyberte jednu z následujících možností:  

  - **Maximalizováno**: typ nasazení se spustí na klientských zařízeních v maximalizovaném okně. Uživatelům se zobrazí všechny aktivity instalace.  

  - **Normální**: typ nasazení se spouští v normálním režimu založeném na výchozím nastavení systému a programu. Tento režim je výchozí.  

  - **Minimalizovaný**: typ nasazení se spustí na klientských zařízeních v minimalizovaném okně. Uživatelé můžou aktivitu instalace zobrazit v oznamovací oblasti nebo na hlavním panelu.  

  - **Skryté**: typ nasazení běží na klientských zařízeních jako skrytý. Uživatelům se zobrazí žádná aktivita instalace.  

- **Umožněte uživatelům zobrazení a interakci s instalací programu**: Určete, jestli uživatel může při instalaci typu nasazení spolupracovat a nastavit možnosti instalace.  

    Pokud jste v rozevíracím seznamu **chování instalace** vybrali možnost **instalovat pro uživatele** , tato možnost je ve výchozím nastavení povolená.  

    > [!IMPORTANT]  
    > Když vyberete chování **instalace pro systém** , toto nastavení je volitelné. Tato změna je primárně k tomu, aby koncovým uživatelům bylo umožněno interakci s instalací během pořadí úkolů. Například pro spuštění procesu instalace, který vyzve koncového uživatele k provedení různých možností. Některé instalační programy aplikace nemůžou mít netiché výzvy pro uživatele nebo proces instalace může vyžadovat konkrétní hodnoty konfigurace známé jenom pro uživatele. <!--1356976-->  
    >  
    > Instalace v kontextu systému a povolení interakce uživatelům s instalací není zabezpečená konfigurace. Další informace najdete v tématu [zabezpečení a ochrana osobních údajů pro správu aplikací](../plan-design/security-and-privacy-for-application-management.md#bkmk_interact).  

- **Maximální povolená doba běhu (v minutách)**: zadejte maximální dobu v minutách, po kterou se bude typ nasazení spouštět v klientském počítači. Toto nastavení zadejte jako celé číslo větší než nula. Výchozí hodnota je 120 minut (2 hodiny).  

    Tuto hodnotu použijte pro následující akce:  

  - Pro monitorování výsledků z typu nasazení.  

  - Pro kontrolu, zda je typ nasazení nainstalován při definování oken údržby na klientských zařízeních. Když je nastavené časové období údržby, typ nasazení se spustí jenom v případě, že je v okně údržby k dispozici dostatek času pro nastavení **maximální doby povoleného** běhu.  

    > [!IMPORTANT]  
    > Ke konfliktu může dojít, pokud je **maximální povolená doba běhu** delší než plánované časové období údržby. Pokud uživatel nastaví maximální dobu běhu na období delší než délka dostupného okna údržby, tento typ nasazení se nespustí.  

- **Odhadovaná doba instalace (v minutách)**: zadejte odhadovanou dobu instalace typu nasazení. Uživatelům se tato doba zobrazuje v centru softwaru.  

#### <a name="deployment-type-properties-user-experience-options"></a>Vlastnosti typu nasazení možnosti **uživatelského prostředí**

Když zobrazíte vlastnosti typu nasazení, na kartě **činnost koncového uživatele** se zobrazí následující možnosti:

Vynutilo konkrétní chování po instalaci. Vyberte jednu z následujících možností:  

- **Určete chování na základě návratových kódů**: zpracování se restartuje na základě kódů nakonfigurovaných na kartě [návratové kódy](#bkmk_dt-return) . zobrazení centra softwaru **můžou vyžadovat restart**. Pokud je uživatel přihlášen během instalace, zobrazí se mu výzva v závislosti na konfiguraci uživatelského prostředí *nasazení* .  

- **Žádná konkrétní akce**: po instalaci není vyžadováno restartování. Zprávy centra softwaru bez nutnosti restartování.  

- **Instalační program softwaru může vynutit restartování zařízení**: Configuration Manager nekontroluje ani nezahajuje restart, ale samotná instalace může to udělat bez upozornění. Toto nastavení použijte, pokud chcete zabránit Configuration Manager selhání instalace vytváření sestav, když instalační program inicializuje restartování. Zobrazení centra softwaru **můžou vyžadovat restart**.  

- **Configuration Manager klient vynutí povinné restartování zařízení**: Configuration Manager po úspěšné instalaci vynutí restart zařízení. Zprávy centra softwaru vyžadují restartování. Pokud je uživatel přihlášen během instalace, zobrazí se mu výzva v závislosti na konfiguraci uživatelského prostředí *nasazení* .  

### <a name="deployment-type-requirements"></a><a name="bkmk_dt-require"></a>**Požadavky** typu nasazení

Configuration Manager ověří tyto požadavky na zařízeních před instalací typu nasazení. Použijte požadavky k dalšímu upřesnění a řízení zařízení nebo uživatelů, kteří obdrží tuto aplikaci. Pokud například nasadíte aplikaci do kolekce uživatelů, určete požadavky na hardware aplikace zde.

1. Na stránce **požadavky** vyberte **Přidat** a otevřete dialogové okno **vytvořit požadavek** .  

2. V rozevíracím seznamu **kategorie** vyberte, zda je tento požadavek určen pro **zařízení** nebo **uživatele**.  

    Vyberte možnost **vlastní** a použijte dříve vytvořenou globální podmínku. Když vyberete **vlastní**, můžete také zvolit **vytvořit** a vytvořit novou globální podmínku. Další informace o globálních podmínkách najdete v tématu [Vytvoření globálních podmínek](create-global-conditions.md).  

    > [!IMPORTANT]  
    > Pokud nasadíte aplikaci do kolekce zařízení, klient bude ignorovat všechny požadavky na **uživatele** kategorie a podmínku **primární zařízení**.  

3. V rozevíracím seznamu **Podmínka** vyberte podmínku, která vyhodnotí, jestli uživatel nebo zařízení splňuje požadavky na instalaci. Obsah tohoto seznamu se liší v závislosti na vybrané kategorii.  

4. V rozevíracím seznamu **operátor** vyberte operátor, který chcete použít. Tento operátor porovnává vybranou podmínku se zadanou hodnotou. Vyhodnocuje, zda uživatel nebo zařízení splňuje požadavek na instalaci. Dostupné operátory se liší v závislosti na zvolené podmínce. Při použití `One Of` operátoru pole hodnoty obsahuje ověření, že je nutné zadat jednu položku na řádek.

    > [!Note]  
    > Dostupné požadavky se liší v závislosti na typu zařízení, které používá typ nasazení.  

5. V poli **hodnota** zadejte hodnoty, které se mají použít pro porovnání. Tyto hodnoty spolu s vybranou podmínkou a operátorem vyhodnocují, jestli uživatel nebo zařízení splňuje požadavky na instalaci. Dostupné hodnoty se liší v závislosti na zvolené podmínce a zvoleném operátoru.  

6. Kliknutím na **tlačítko OK** uložte požadavek a zavřete dialogové okno **vytvořit požadavek** .  

### <a name="deployment-type-dependencies"></a><a name="bkmk_dt-depend"></a>**Závislosti** typu nasazení  

Závislosti definují jeden nebo více typů nasazení z jiné aplikace, kterou musí klient nainstalovat před instalací tohoto typu nasazení.

> [!IMPORTANT]  
> V některých případech je typ nasazení závislý na typu nasazení, který má také závislosti. Maximální počet podporovaných závislostí v řetězci je pět.  

1. Na stránce **závislosti** vyberte **Přidat**.  

2. V okně Přidat závislost zadejte **název skupiny závislostí**. Tento název odkazuje na tuto skupinu závislostí aplikace.  

3. V okně Přidat závislost vyberte **Přidat**.  

4. V okně **Určení požadované aplikace** vyberte dostupnou aplikaci a alespoň jeden z jejích typů nasazení, které chcete použít jako závislost.  

    > [!TIP]  
    > Výběrem možnosti **Zobrazit** zobrazíte vlastnosti vybrané aplikace nebo typu nasazení.  

5. Výběrem **OK** zavřete okno **zadat požadované aplikace** .  

6. Pokud chcete, aby klient automaticky nainstaloval závislou aplikaci, vyberte možnost **automaticky instalovat** vedle závislosti.  

    > [!NOTE]  
    > Nemusíte nasazovat závislou aplikaci, aby ji klient mohl automaticky nainstalovat.  

7. Pokud přidáte více než jednu závislost, použijte tlačítka **zvýšit prioritu** a **snížit prioritu** . Tyto akce mění pořadí, ve kterém klient vyhodnocuje jednotlivé závislosti.  

8. Výběrem **OK** zavřete okno **Přidat závislost** .  

### <a name="deployment-type-return-codes"></a><a name="bkmk_dt-return"></a>**Návratové kódy** typu nasazení

> [!Note]  
> Tato stránka není v Průvodci vytvořením typu nasazení. Je to jenom karta ve vlastnostech stávajícího typu nasazení.  

Zadejte návratové kódy pro řízení chování po dokončení typu nasazení. Například signalizace, že je vyžadováno restartování, instalace je dokončena.

1. Na kartě **návratové kódy** v okně vlastnosti typu nasazení vyberte **Přidat**.  

2. V okně Přidat návratový kód zadejte **hodnotu návratového kódu** , který jste od tohoto typu nasazení očekávali. Tato hodnota je libovolné kladné nebo záporné celé číslo v rozsahu od `-2147483648` do `2147483647` .  

3. Z rozevíracího seznamu vyberte **typ kódu** . Toto nastavení definuje způsob, jakým Configuration Manager interpretuje zadaný návratový kód z tohoto typu nasazení. Dostupné typy se liší v závislosti na technologii typu nasazení.  

    - **Úspěch (bez restartování)**: typ nasazení byl úspěšně nainstalován a není nutné žádné restartování.  

    - **Chyba (bez restartování)**: Nepodařilo se nainstalovat typ nasazení.  

    - **Pevný restart**: typ nasazení se úspěšně nainstaloval, ale vyžaduje, aby se zařízení restartovalo. Nic jiného není možné nainstalovat, dokud se zařízení nerestartuje.  

    - **Obnovitelné restartování**: typ nasazení se úspěšně nainstaloval, ale vyžaduje, aby se zařízení restartovalo. K dalším instalacím může dojít před restartováním zařízení.  

    - **Rychlé opakování**: na zařízení už probíhá jiná instalace. Klient opakuje každou dvě hodiny (celkem 10).  

4. V případě potřeby zadejte **název** a **Popis** pro tento návratový kód.

5. Výběrem **OK** zavřete okno Přidat návratový kód.  

#### <a name="example-non-zero-success"></a>Příklad: nenulová úspěch

Nasazujete aplikaci, která `1` po úspěšné instalaci vrátí ukončovací kód. Ve výchozím nastavení Configuration Manager detekuje tento nenulový návratový kód jako selhání. Zadejte hodnotu návratového kódu `1` a vyberte typ kódu **úspěch (bez restartování)**. Nyní Configuration Manager interpretuje návratový kód jako úspěch pro tento typ nasazení.

#### <a name="default-return-codes"></a>Výchozí návratové kódy

Když vytvoříte některé typy nasazení, Configuration Manager automaticky přidá následující návratové kódy, které jsou pro tuto technologii běžné:  

##### <a name="windows-installer-msi-file"></a>Instalační služba systému Windows ( \* soubor. msi)

|Hodnota    |Typ kódu|
|---------|---------|
|0        |Úspěch (bez restartování)|
|1707     |Úspěch (bez restartování)|
|3010     |Rychlé restartování|
|1641     |Pevný restart|
|1618     |Rychlé opakování|

##### <a name="script-installer"></a>Instalační služba skriptů

|Hodnota    |Typ kódu|
|---------|---------|
|0        |Úspěch (bez restartování)|
|1641     |Pevný restart|
|3010     |Rychlé restartování|
|1618     |Rychlé opakování|

##### <a name="windows-app-package-appx-appxbundle-msix-msixbundle"></a>Balíček aplikace pro systém Windows ( \* . appx, \* . appxbundle, \* . msix, \* . msixbundle)

|Hodnota    |Typ kódu|
|---------|---------|
|15605    |Rychlé opakování|
|15618    |Rychlé opakování|

## <a name="additional-options-for-app-v-deployment-types"></a><a name="bkmk_appv"></a> Další možnosti pro typy nasazení App-V  

Nakonfigurujte další možnosti, které jsou jedinečné pro typy nasazení pro virtuální aplikace (App-V).  

### <a name="app-v-deployment-type-content-options"></a><a name="bkmk_appv-content"></a> Možnosti **obsahu** typu nasazení sady App-V  

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte položku **Správa aplikací**a vyberte uzel **aplikace** .  

2. Vyberte aplikaci s typem nasazení App-V a vyberte **vlastnosti**.  

3. Ve vlastnostech aplikace přepněte na kartu **typy nasazení** . Vyberte typ nasazení App-V a vyberte **Upravit**.  

4. Ve vlastnostech typu nasazení přepněte na kartu **obsah** . podle potřeby nakonfigurujte následující možnosti:  

    - **Zachovat obsah v mezipaměti klienta**: klient Configuration Manager neodstraní obsah pro tento typ nasazení z mezipaměti.  

    - **Načíst obsah do mezipaměti sady App-v před spuštěním**: před spuštěním aplikace se klient Configuration Manager načte do mezipaměti sady App-v. veškerý obsah tohoto typu nasazení. Klient připnout obsah do mezipaměti. Obsah podle potřeby odstraní.  

5. Kliknutím na **tlačítko OK** zavřete vlastnosti typu nasazení. Pak kliknutím na **OK** zavřete vlastnosti aplikace.  

### <a name="app-v-deployment-type-publishing-options"></a><a name="bkmk_appv-pub"></a> Možnosti **publikování** typu nasazení sady App-V

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte položku **Správa aplikací**a vyberte uzel **aplikace** .  

2. Vyberte aplikaci s typem nasazení App-V a vyberte **vlastnosti**.  

3. Ve vlastnostech aplikace přepněte na kartu **typy nasazení** . Vyberte typ nasazení App-V a vyberte **Upravit**.  

4. Ve vlastnostech typu nasazení přepněte na kartu **publikování** . Vyberte položky ve virtuální aplikaci, které chcete publikovat.  

5. Kliknutím na **tlačítko OK** zavřete vlastnosti typu nasazení. Pak kliknutím na **OK** zavřete vlastnosti aplikace.  

## <a name="import-an-application"></a><a name="bkmk_import"></a> Import aplikace  

K importu aplikace do Configuration Manager použijte následující postup:

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte položku **Správa aplikací**a vyberte uzel **aplikace** .  

2. Na pásu karet na kartě **Domů** a **vytvořit** skupinu vyberte **importovat aplikaci**.  

3. Na stránce **Obecné** v Průvodci importem aplikace zadejte síťovou cestu k **souboru** , který se má importovat. Například, `\\server\share\file.zip`. Tento soubor je platný komprimovaný archivní program (formát ZIP) exportované aplikace Configuration Manager.  

4. Na stránce **obsah souboru** vyberte akci, která se má provést, pokud je tato aplikace duplikátem existující aplikace. Vytvořte novou aplikaci nebo ignorujte duplicitní a přidejte novou revizi do existující aplikace.  

5. Na stránce **Souhrn** zkontrolujte akce a pak dokončete průvodce.  

Nová aplikace se zobrazí v uzlu **Aplikace**.  

> [!TIP]  
> Rutina Windows PowerShellu **Import-CMApplication** má stejnou funkci jako tento postup. Další informace najdete v tématu [Import-CMApplication](/powershell/module/configurationmanager/import-cmapplication?view=sccm-ps).  

Další informace o exportu aplikace najdete v tématu [úlohy správy pro aplikace](management-tasks-applications.md).

## <a name="supported-deployment-types"></a><a name="bkmk_deploy-types"></a> Podporované typy nasazení  

Configuration Manager podporuje pro aplikace následující typy nasazení:

| Název typu závislosti | Popis |
|--------------------------|----------------------|  
| **Instalační služba systému Windows ( \* soubor. msi)** | Soubor Instalační služba systému Windows. |  
| **Balíček aplikace pro systém Windows ( \* . appx, \* . appxbundle, \* . msix, \* . msixbundle)** | Soubor balíčku aplikace systému Windows (. appx), balíček sady prostředků aplikace systému Windows (. appxbundle), balíček aplikace pro Windows 10 (. msix) nebo sada prostředků aplikace Windows 10 (. msixbundle).<!--1357427--> |  
| **Balíček aplikace systému Windows (ve Windows Store)** | Zadejte odkaz na aplikaci ve Windows Storu nebo přejděte do Storu a vyberte aplikaci.<sup>[Poznámka 1](#bkmk_note1)</sup> |  
| **Instalační služba skriptů** | Určete skript nebo program, který je spuštěn na klientech Windows pro instalaci obsahu nebo provedení akce. Tento typ nasazení použijte pro setup.exe instalátory nebo obálky skriptu. |  
| **Microsoft Application Virtualization 4** | Manifest Microsoft App-V v4. |  
| **Microsoft Application Virtualization 5** | Soubor balíčku Microsoft App-V v5. |  
| **Balíček aplikace Windows Phone ( \* soubor. XAP)** | Soubor balíčku aplikace Windows Phone. |  
| **Balíček aplikací systému Windows Phone (ve skladu systému Windows Phone)** | Zadejte odkaz na aplikaci ve Windows Storu. |  
| **Mac OS X** | Pro počítače s macOS, na kterých běží klient Configuration Manager. Vytvořte soubor. cmmac pomocí nástroje **CMAppUtil** . |  
| **Webová aplikace** | Zadejte odkaz na webovou aplikaci. Tento typ nasazení nainstaluje zástupce webové aplikace do zařízení uživatele. |  
| **Instalační služba systému Windows přes MDM ( \* . msi)** | Umožňuje vytvářet a nasazovat aplikace založené na Instalační služba systému Windows na zařízeních s Windows 10. Další informace najdete v tématu [nasazení Instalační služba systému Windows aplikací do zařízení s Windows 10 zaregistrovaných v MDM](../get-started/creating-windows-applications.md#bkmk_mdm-msi). |
| **Pořadí úkolů** | Počínaje verzí 2002 nainstalujte nebo odinstalujte komplexní aplikace s využitím pořadí úkolů. Další informace najdete v tématu [typ nasazení pořadí úloh](../get-started/creating-windows-applications.md#bkmk_tsdt). <!--3555953--> |

> [!NOTE]
> Konzola Configuration Manager může zobrazit další typy nasazení, ale jsou pro platformy, které již nejsou podporovány. Další informace najdete v tématu [co se stalo se hybridem?](../../mdm/understand/what-happened-to-hybrid.md).

### <a name="note-1-windows-app-package-in-the-windows-store"></a><a name="bkmk_note1"></a> Poznámka 1: balíček aplikace systému Windows (ve Windows Storu)

Pokud chcete aplikaci nasadit jako odkaz na Windows Store, nakonfigurujte zásady skupiny, aby se **aplikace pro Store vypnula**. Nastavte tuto zásadu na **zakázanou** nebo **nenakonfigurovanou**. Pokud toto nastavení povolíte, klienti se nebudou moci připojit k Windows Storu a stahovat a instalovat aplikace.

Klienti Windows vždycky vyhodnotí typy nasazení, které používají odkaz na úložiště před jinými typy nasazení. Pak klient vyhodnotí typy nasazení podle priority.

> [!TIP]
> Některé odkazy na úložiště můžou v Průvodci vytvořením aplikace způsobit následující chybu: neplatný odkaz na aplikaci. Tato chyba může způsobovat například některé *aplikace vybrané* pro obchod. Na stránce **Obecné** v průvodci můžete dál vybrat **Další** . Configuration Manager aplikaci úspěšně vytvořili a můžete ji úspěšně nasadit.<!-- SCCMDocs-pr #4716 -->

## <a name="next-steps"></a>Další kroky

Po vytvoření aplikace v Configuration Manager je dalším krokem [nasazení aplikace](deploy-applications.md).

Počínaje verzí 1906 vytvořte skupinu aplikací, které můžete odeslat do kolekce uživatelů nebo zařízení jako jediné nasazení. Další informace najdete v tématu [Vytvoření skupin aplikací](create-app-groups.md).

Další informace o vytváření aplikací na různých platformách operačního systému najdete v následujících článcích:  

- [Vytváření aplikací pro Windows](../get-started/creating-windows-applications.md)
- [Vytváření aplikací pro Mac](../get-started/creating-mac-computer-applications.md)
- [Vytváření aplikací pro servery Linux a UNIX](../get-started/creating-linux-and-unix-server-applications.md)
- [Vytváření aplikací pro Windows Embedded](../get-started/creating-windows-embedded-applications.md)