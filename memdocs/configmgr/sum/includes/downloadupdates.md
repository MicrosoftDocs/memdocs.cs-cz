1.  V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** a vyberte uzel **aktualizace softwaru** .  

2.  Pomocí jedné z následujících metod vyberte aktualizace softwaru, které chcete stáhnout:  

    -   Vyberte jednu nebo více skupin aktualizací softwaru z uzlu **skupiny aktualizací softwaru** . Pak na pásu karet klikněte na **Stáhnout** .  

    -   Vyberte jednu nebo více aktualizací softwaru z uzlu **všechny aktualizace softwaru** . Pak na pásu karet klikněte na **Stáhnout** .  

        > [!NOTE]  
        >  V uzlu **všechny aktualizace softwaru** Configuration Manager zobrazuje pouze aktualizace softwaru s klasifikací **kritická** a **zabezpečení** , které byly vydány v posledních 30 dnech.  

        > [!TIP]  
        >  Kliknutím na možnost **Přidat kritéria** můžete filtrovat aktualizace softwaru, které jsou zobrazeny v uzlu **všechny aktualizace softwaru** . Uložte často použitá kritéria hledání a potom spravujte uložená hledání na kartě **Vyhledat** .  


3.  Na stránce **balíček pro nasazení** v průvodci stažením aktualizací softwaru nakonfigurujte následující nastavení:  

    -  **Vybrat balíček pro nasazení:** Toto nastavení vyberte, pokud chcete zvolit existující balíček pro nasazení pro aktualizace softwaru, které jsou v nasazení.  

        > [!NOTE]  
        >  Aktualizace softwaru, které web již stáhl do vybraného balíčku pro nasazení, se znovu nestáhnou.  

    -  **Vytvořit nový balíček pro nasazení:** Toto nastavení vyberte, pokud chcete pro aktualizace softwaru v nasazení vytvořit nový balíček pro nasazení. Nakonfigurujte tahle nastavení:  

        -   **Název:** Určuje název balíčku pro nasazení. Tento balíček musí mít jedinečný název, který stručně popisuje obsah balíčku. Je omezena na 50 znaků.  

        -   **Popis**: Zadejte popis, který poskytuje informace o balíčku pro nasazení. Nepovinný popis je omezený na 127 znaků.    

        -   **Zdroj balíčku:** Určuje umístění zdrojových souborů aktualizace softwaru. Zadejte síťovou cestu k umístění zdroje, například `\\server\sharename\path` , nebo klikněte na tlačítko **Procházet** a vyhledejte umístění v síti. Než přejdete na další stránku, vytvořte sdílenou složku pro zdrojové soubory balíčku pro nasazení.  

             - Zadané umístění nemůžete použít jako zdroj jiného balíčku pro nasazení softwaru.  

             - Umístění zdroje balíčku můžete změnit ve vlastnostech balíčku nasazení po Configuration Manager vytvoří balíček pro nasazení. V takovém případě zkopírujte obsah z původního zdroje balíčku do nového umístění zdroje balíčku.  

             -  Počítačový účet poskytovatele služby SMS a uživatel, který spouští Průvodce pro stažení aktualizací softwaru, musí mít oprávnění k **zápisu** do umístění pro stahování. Omezte přístup k umístění pro stahování. Toto omezení snižuje riziko manipulace se zdrojovými soubory aktualizací softwaru.  

        - **Povolit binární rozdílovou replikaci**: Toto nastavení povolte, pokud chcete minimalizovat síťový provoz mezi lokalitami. Binární rozdílová replikace (binární ROZDÍLOVÁ replikace) aktualizuje jenom obsah, který se v balíčku změnil, místo aktualizace obsahu celého balíčku. Další informace najdete v tématu [binární rozdílová replikace](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

4.  Na stránce **distribuční body** určete distribuční body nebo skupiny distribučních bodů, které budou hostovat soubory aktualizace softwaru. Další informace o distribučních bodech najdete v tématu [Konfigurace distribučních bodů](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs). Tato stránka je dostupná pouze tehdy, když vytvoříte nový balíček pro nasazení aktualizací softwaru.  

5.  Stránka **Nastavení distribuce** je k dispozici pouze při vytvoření nového balíčku pro nasazení aktualizace softwaru. Zadejte následující nastavení:  

    -   **Priorita distribuce:** Toto nastavení použijte, pokud chcete určit prioritu distribuce balíčku pro nasazení. Priorita distribuce je důležitá při odesílání balíčku pro nasazení do distribučních bodů v podřízených lokalitách. Balíčky pro nasazení se odesílají v pořadí podle priority: vysoká, střední nebo nízká. Balíčky se stejnou prioritou jsou zasílány v pořadí podle data vytvoření. Pokud neexistují žádné nevyřízené položky, balíček okamžitě zpracuje bez ohledu na jeho prioritu. Ve výchozím nastavení lokalita odesílá balíčky se **střední** prioritou.  

    -   **Povolit distribuci na vyžádání**: pomocí tohoto nastavení můžete povolit distribuci obsahu na vyžádání do distribučních bodů konfigurovaných pro tuto funkci a v aktuální skupině hranic klienta. Pokud povolíte toto nastavení, bod správy vytvoří Trigger pro správce distribuce k distribuci obsahu do všech distribučních bodů, když klient požaduje obsah balíčku a obsah není k dispozici. Další informace najdete v tématu [distribuce obsahu na vyžádání](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).  

    -   **Nastavení připraveného distribučního bodu:** Toto nastavení slouží k určení způsobu distribuce obsahu do připravených distribučních bodů. Zvolte jednu z následujících možností:  

        -   **Automaticky stahovat obsah, když jsou balíčky přiřazeny distribučním místům:** Pomocí tohoto nastavení můžete ignorovat nastavení přípravy a distribuovat obsah do distribučního bodu.   

        -   **Stahovat do distribučního bodu pouze změny obsahu:** Pomocí tohoto nastavení můžete připravit původní obsah na distribučním bodu a následně do distribučního bodu distribuovat změny obsahu.  

        -   **Ručně kopírovat obsah tohoto balíčku do distribučního bodu:** Pomocí toho nastavení určíte, že obsah se má vždycky připravit v distribučním bodě. Tato možnost je výchozí.  

        Další informace o tom, jak předem připravit obsah v distribučních bodech, najdete v tématu [Použít připravený obsah](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  


6.  Na stránce **umístění pro stahování** zadejte umístění, které Configuration Manager používá ke stažení zdrojových souborů aktualizace softwaru. Použijte jednu z následujících možností:  

    -   **Stáhnout softwarové aktualizace z Internetu**: Toto nastavení vyberte, pokud chcete stáhnout aktualizace softwaru z umístění na internetu. Tato možnost je výchozí.  

    -   **Stáhnout softwarové aktualizace z místa v mé síti**: pomocí tohoto nastavení můžete stáhnout aktualizace softwaru z místního adresáře nebo sdílené složky. Toto nastavení je užitečné, když počítač, na kterém spouštíte Průvodce, nemá přístup k Internetu. Každý počítač s přístupem k Internetu může předběžně stáhnout aktualizace softwaru. Pak je uložte do umístění v místní síti, které je přístupné z počítače, na kterém běží průvodce.  


7.  Na stránce **Výběr jazyka** vyberte jazyky, ve kterých bude lokalita stahovat vybrané aktualizace softwaru. Lokalita stáhne pouze ty aktualizace, pokud jsou k dispozici ve vybraných jazycích. Aktualizace softwaru, které nejsou specifické pro konkrétní jazyk, budou staženy vždy. Ve výchozím nastavení Průvodce vybírá jazyky, které jste nakonfigurovali ve vlastnostech bodu aktualizace softwaru. Před přechodem na další stránku je třeba vybrat alespoň jeden jazyk. Když vyberete jenom jazyky, které aktualizace softwaru nepodporuje, stahování se pro aktualizaci nepovede.  

8. Na stránce **Souhrn** zkontrolujte nastavení, která jste vybrali v průvodci, a poté kliknutím na tlačítko **Další** Stáhněte aktualizace softwaru.  

9. Na stránce **dokončení** ověřte, zda byly aktualizace softwaru úspěšně staženy, a poté klikněte na tlačítko **Zavřít**.  
