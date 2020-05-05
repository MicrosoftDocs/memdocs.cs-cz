---
title: Modul pro kontrolu požadovaných součástí
titleSuffix: Configuration Manager
description: Zjistěte, jak pomocí nástroje pro kontrolu požadovaných součástí identifikovat a opravit problémy, které by mohly blokovat instalaci lokality nebo role systému lokality.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aaf13bb8-4ba2-4bd7-9fac-d36a9d88a1b6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1ee871d99285bee3a4489d88bf0d203bf74cde3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718172"
---
# <a name="prerequisite-checker-for-configuration-manager"></a>Kontrola požadovaných součástí pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

 Předtím, než spustíte instalační program pro instalaci nebo upgrade lokality Configuration Manager nebo než nainstalujete roli systému lokality na nový server, můžete použít tuto samostatnou aplikaci (**prereqchk. exe**) z verze Configuration Manager, kterou chcete použít k ověření připravenosti serveru. Pomocí kontroly požadovaných součástí identifikujte a opravte problémy, které by blokovaly instalaci lokality nebo role systému lokality.  

> [!NOTE]  
>  Kontrola požadovaných součástí se vždycky spouští jako součást instalace.  

Ve výchozím nastavení, když se spustí Kontrola požadovaných součástí:  

-   Ověřuje server, na kterém běží.  
-   Místní počítač vyhledá existující server lokality a spustí se jenom kontroly, které platí pro tento web.  
-   Pokud se nezjistí žádné existující lokality, spustí se všechna požadovaná pravidla.  
-   Kontroluje pravidla, která ověřují, zda je nainstalován software a nastavení požadované pro instalaci. Je možné, že požadovaný software bude vyžadovat další konfiguraci nebo aktualizace softwaru, které nejsou ověřené nástrojem pro kontrolu požadovaných součástí.  
-   Protokoluje své výsledky do souboru **souboru ConfigMgrPrereq. log** na systémové jednotce počítače. Soubor protokolu může obsahovat další informace, které se nezobrazí v aplikačním rozhraní.  

Když spustíte kontrolu požadovaných součástí na příkazovém řádku a zadáte konkrétní možnosti příkazového řádku:  

-   Nástroj pro kontrolu požadovaných součástí provede pouze kontroly, které jsou spojeny se serverem lokality nebo systémy lokality, které zadáte v příkazovém řádku.  
-   Ke kontrole vzdáleného počítače musí mít váš uživatelský účet oprávnění správce ke vzdálenému počítači.  

Další informace o kontrolách, které provádí kontrola požadovaných součástí, najdete v článku [kontroly požadovaných součástí pro Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md).  

## <a name="copy-prerequisite-checker-files-to-another-computer"></a>Kopírování souborů kontroly požadovaných součástí do jiného počítače  

1.  V Průzkumníku Windows, navštivte jedno z následujících umístění:  

    -   **&lt;*Configuration Manager instalačního média*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager cesta*\>instalace \BIN\X64**  

2.  Zkopírujte následující soubory do cílové složky na druhém počítači:  

    - prereqchk. exe
    - Prereqcore. dll
    - prereqchkres. dll
      - Tento soubor je v podsložce pro jazyk instalace. Například angličtina je v `00000409` podsložce. <!--586808-->
    - basesql. dll
    - basesvr. dll
    - baseutil. dll

##  <a name="run-prerequisite-checker-with-default-checks"></a>Spustit kontrolu požadovaných součástí s výchozími kontrolami  

1.  V Průzkumníku Windows, navštivte jedno z následujících umístění:  

    -   **&lt;*Configuration Manager instalačního média*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager cesta*\>instalace \BIN\X64**  

2.  Spusťte **prereqchk. exe** a spusťte kontrolu požadovaných součástí.   
    Nástroj pro kontrolu požadovaných součástí detekuje existující weby, a pokud se najde, provede kontrolu připravenosti na upgrade. Pokud se nenaleznou žádné lokality, provedou se všechny kontroly. Sloupec **typ lokality** poskytuje informace o serveru lokality nebo systému lokality, ke kterému je pravidlo přidruženo.  

##  <a name="run-prerequisite-checker-from-a-command-prompt-for-all-default-checks"></a>Spusťte kontrolu požadovaných součástí z příkazového řádku pro všechny výchozí kontroly.  

1.  Otevřete okno příkazového řádku a změňte adresáře na jedno z následujících umístění:  

    -   **&lt;*Configuration Manager instalačního média*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Configuration Manager cesta*\>instalace \BIN\X64**  

2.  Zadejte **prereqchk. exe/Local** a spusťte kontrolu požadovaných součástí a na serveru spusťte všechny kontroly požadovaných součástí.  

## <a name="run-prerequisite-checker-from-a-command-prompt-to-use-options"></a>Spuštění kontroly požadovaných součástí z příkazového řádku pro použití možností  

1. Otevřete okno příkazového řádku a změňte adresáře na jedno z následujících umístění:  

   -   **&lt;*Configuration Manager instalačního média*\>\SMSSETUP\BIN\X64**  
   -   **&lt;*Configuration Manager cesta*\>instalace \BIN\X64**  

2. Zadejte **prereqchk. exe** s přidáním jedné nebo více z následujících možností příkazového řádku.  

   Pokud chcete například kontrolovat primární lokalitu, můžete použít následující:  

      **prereqchk. exe [/NOUI]/PRI/SQL &lt;plně kvalifikovaný název\> domény &lt;pro SQL Server/SDK plně\> kvalifikovaný název &lt;domény poskytovatele služby SMS [\>/JOIN plně kvalifikovaný &lt;název domény lokality centrální\>správy] [ &lt;/MP FQDN bodu správy\>] [/DP FQDN distribučního bodu]**  

   **Webový server Centrální správy:**  

   -   **/NOUI**  

        Nepožadováno. Spustí kontrolu požadovaných součástí bez zobrazení uživatelského rozhraní. Tuto možnost je nutné zadat před jakoukoliv jinou možností na příkazovém řádku.  

   -   **/CAS**  

        Povinná hodnota. Ověřuje, že místní počítač splňuje požadavky na lokalitu centrální správy.  

   -   **/SQL &lt; *plně kvalifikovaný název domény SQL Server*>**  

        Povinná hodnota. Pomocí plně kvalifikovaného názvu domény (FQDN) ověří, že zadaný počítač splňuje požadavky pro SQL Server hostování databáze Configuration Manager lokality.  

   -   **/SDK &lt; *plně kvalifikovaný název domény poskytovatele služby SMS*>**  

        Povinná hodnota. Ověřuje, že zadaný počítač splňuje požadavky na poskytovatele služby SMS.  

   -   **/Ssbport**  

        Nepožadováno. Ověřuje, že platí výjimka brány firewall, aby bylo možné navázat komunikaci s portem SQL Server Service Broker (SSB). Výchozí port SSB je 4022.  

   -   **INSTALLDIR &lt; *Configuration Manager cesta k instalaci*>**  

        Nepožadováno. Ověří minimální místo na disku podle požadavků pro instalaci lokality.  

   **Server primární lokality:**  

   -   **/NOUI**  

       Nepožadováno. Spustí kontrolu požadovaných součástí bez zobrazení uživatelského rozhraní. Tuto možnost je nutné zadat před jakoukoliv jinou možností na příkazovém řádku.  

   -   **/PRI**  

        Povinná hodnota. Ověřuje, že místní počítač splňuje požadavky na primární lokalitu.  

   -   **/SQL &lt; *plně kvalifikovaný název domény SQL Server*>**  

        Povinná hodnota. Ověřuje, že zadaný počítač splňuje požadavky pro SQL Server hostování databáze Configuration Manager lokality.  

   -   **/SDK &lt; *plně kvalifikovaný název domény poskytovatele služby SMS*>**  

        Povinná hodnota. Ověřuje, že zadaný počítač splňuje požadavky na poskytovatele služby SMS.  

   -   **/Join &lt; *plně kvalifikovaný název domény lokality centrální správy*>**  

        Nepožadováno. Ověřuje, že místní počítač splňuje požadavky pro připojení k serveru lokality centrální správy.  

   -   **/MP &lt; *plně kvalifikovaný název domény bodu správy*>**  

        Nepožadováno. Ověřuje, že zadaný počítač splňuje požadavky na roli systému lokality bodu správy. Tato možnost je podporována, pouze pokud použijete možnost **/pri** .  

   -   **/DP &lt; *FQDN distribučního bodu*>**  

        Nepožadováno. Ověřuje, že zadaný počítač splňuje požadavky na roli systému lokality distribučního bodu. Tato možnost je podporována, pouze pokud použijete možnost **/pri** .  

   -   **/Ssbport**  

        Nepožadováno. Ověřuje, že platí výjimka brány firewall, aby bylo možné komunikovat na portu SSB. Výchozí port SSB je 4022.  

   -   **INSTALLDIR &lt; *Configuration Manager cesta k instalaci*>**  

        Nepožadováno. Ověří minimální místo na disku podle požadavků pro instalaci lokality.  

   **Server sekundární lokality:**  

   -   **/NOUI**  

        Nepožadováno. Spustí kontrolu požadovaných součástí bez zobrazení uživatelského rozhraní. Tuto možnost je nutné zadat před jakoukoliv jinou možností na příkazovém řádku.  

   -   **/S &lt; *plně kvalifikovaný název domény serveru sekundární lokality*>**  

        Povinná hodnota. Ověřuje, že zadaný počítač splňuje požadavky na sekundární lokalitu.  

   -   **/INSTALLSQLEXPRESS**  

        Nepožadováno. Ověřuje, že SQL Server Express může být nainstalován v zadaném počítači.  

   -   **/Ssbport**  

        Nepožadováno. Ověřuje, že platí výjimka brány firewall, aby bylo možné navázat komunikaci s portem SSB. Výchozí port SSB je 4022.  

   -   **/Sqlport**  

        Nepožadováno. Ověřuje, že platí výjimka brány firewall, aby bylo možné navázat komunikaci s portem služby SQL Server a aby se port nepoužíval jinou pojmenovanou instancí SQL Server. Výchozí port je 1433.  

   -   **INSTALLDIR &lt; *Configuration Manager cesta k instalaci*>**  

        Nepožadováno. Ověří minimální místo na disku podle požadavků pro instalaci lokality.  

   -   **/SourceDir**  

        Nepožadováno. Ověřuje, že účet počítače sekundární lokality má přístup ke složce, která hostuje zdrojové soubory pro instalaci.  

   **Konzola Configuration Manager:**  

   -   **/Adminui**  

        Povinná hodnota. Ověřuje, že místní počítač splňuje požadavky pro instalaci Configuration Manager.  

3. V uživatelském rozhraní nástroje pro kontrolu požadovaných součástí vytvoří nástroj pro kontrolu požadovaných součástí seznam zjištěných problémů v oddílu **výsledek požadované součásti** .  

   -   Kliknutím na položku v seznamu zobrazíte podrobnosti o tom, jak tento problém vyřešit.  
   -   Před instalací serveru lokality, systému lokality nebo konzoly Configuration Manager musíte vyřešit všechny položky v seznamu, které mají stav **Chyba** .  
   -   Můžete také otevřít soubor **souboru ConfigMgrPrereq. log** v kořenovém adresáři jednotky systému a zkontrolovat výsledky kontroly požadovaných součástí. Soubor protokolu může obsahovat další informace, které se nezobrazí v uživatelském rozhraní nástroje pro kontrolu požadovaných součástí.  
