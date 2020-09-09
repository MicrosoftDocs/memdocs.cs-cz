---
title: Průvodce instalací
titleSuffix: Configuration Manager
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
author: mestew
ms.author: mstewart
manager: dougeby
description: K instalaci nové lokality použijte Průvodce instalací Configuration Manager.
ms.openlocfilehash: a0956e53af0d8ca4dd182dd3c2be944d3a0a703d
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606187"
---
# <a name="use-the-setup-wizard-to-install-configuration-manager-sites"></a>Instalace Configuration Manager lokalit pomocí Průvodce instalací

*Platí pro: Configuration Manager (Current Branch)*

Chcete-li nainstalovat novou Configuration Manager lokalitu pomocí uživatelského rozhraní s asistencí, použijte Průvodce instalací Configuration Manager (setup.exe). Průvodce podporuje instalaci primární lokality nebo lokality centrální správy. Pomocí Průvodce můžete také [upgradovat zkušební instalaci](upgrade-an-evaluation-install-to-a-full-install.md) Configuration Manager na plně licencovanou instalaci. Pokud nechcete používat Průvodce, můžete místo toho použít [instalační skript](use-a-command-line-to-install-sites.md) a spustit bezobslužnou instalaci příkazového řádku.

Do konzoly Configuration Manager nainstalujte sekundární lokalitu. Sekundární lokality nepodporují instalaci skriptu spouštěného z příkazového řádku.

> [!Note]  
> Počínaje verzí 1906 již soubor **úvodní. HTA** neexistuje v kořenovém adresáři instalačního média. Poskytuje odkazy na následující informace:<!--SCCMDocs-pr#3545-->
>
> - **Nainstalovat web**: `smssetup\bin\x64\setup.exe` . Další informace najdete v tématu [instalace centrální správy nebo primární lokality](#bkmk_primary).
> - **Než začnete**: [navrhnout hierarchii lokalit](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626543 -->
> - **Vyhodnocení připravenosti serveru**: [Kontrola požadovaných součástí](prerequisite-checker.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626546 -->
> - **Stažení požadovaných požadovaných souborů**: `smssetup\bin\x64\setupdl.exe` . Další informace najdete v tématu Nástroj pro [stažení instalačního programu](setup-downloader.md).
> - **Nainstalovat Configuration Manager konzolu**: `smssetup\bin\i386\consolesetup.exe` . Další informace najdete v tématu [instalace konzol](install-consoles.md).
> - [**Stáhnout System Center Updates Publisher**](../../../../sum/tools/updates-publisher.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626548 -->
> - **Stáhnout klienty pro další operační systémy**: <!-- https://go.microsoft.com/fwlink/p/?LinkId=626550 -->
>   - [Klient Microsoft Endpoint Configuration Manager – macOS (64-bit)](https://www.microsoft.com/download/details.aspx?id=100850)
>   - [Klienti pro systémy UNIX a Linux](https://www.microsoft.com/download/details.aspx?id=47719)
> - [**Poznámky k verzi**](release-notes.md) <!-- https://go.microsoft.com/fwlink/?LinkID=626571 -->
> - [**Přečíst dokumentaci**](/sccm)<!-- https://go.microsoft.com/fwlink/p/?LinkId=626547 -->
> - **Získat pomoc s instalací**: [fóra TechNet: Configuration Manager (Current Branch) – nasazení lokality a klienta](https://social.technet.microsoft.com/Forums/en-us/home?forum=ConfigMgrDeployment) <!--NOTE: this link requires en-us locale to work-->   <!-- https://go.microsoft.com/fwlink/p/?LinkId=626549 -->
> - **Configuration Manager komunita**: [komunita System Center: jak se zúčastnit](https://social.technet.microsoft.com/wiki/contents/articles/11504.system-center-community-how-to-participate.aspx) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626544 -->
> - [**Configuration Manager domů**](https://www.microsoft.com/cloud-platform/system-center-configuration-manager) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626545 -->


## <a name="install-a-central-administration-or-primary-site"></a><a name="bkmk_primary"></a> Instalace centrální správy nebo primární lokality

Pomocí následujícího postupu nainstalujete lokalitu centrální správy nebo primární lokalitu. Můžete ji také použít k upgradu zkušební lokality na plně licencovanou Configuration Manager lokalitu.

Před zahájením instalace lokality je třeba znát podrobnosti v následujících článcích:

- [Příprava instalace lokalit](prepare-to-install-sites.md)
- [Předpoklady pro instalaci lokalit](prerequisites-for-installing-sites.md)

Pokud instalujete lokalitu centrální správy jako součást scénáře rozšíření lokality, před použitím následujícího postupu si přečtěte téma [rozšíření samostatné primární lokality](use-the-setup-wizard-to-install-sites.md#bkmk_expand) .

### <a name="process-to-install-a-primary-or-central-administration-site"></a><a name="bkmk_installpri"></a> Postup instalace primární lokality nebo lokality centrální správy

1. V počítači, kam chcete nainstalovat lokalitu, spusťte příkaz `<InstallationMedia>\SMSSETUP\BIN\X64\Setup.exe` a spusťte **Průvodce instalací nástroje Configuration Manager**.  

    > [!NOTE]  
    > Když nainstalujete lokalitu centrální správy pro rozšíření na samostatnou primární lokalitu nebo nainstalujete novou podřízenou primární lokalitu v existující hierarchii, použijte instalační média (zdrojové soubory), která odpovídají verzi existující lokality nebo lokality. Pokud jste nainstalovali konzolové aktualizace, které změnily verzi dříve nainstalovaných webů, nepoužívejte původní instalační médium. Místo toho použijte zdrojové soubory z [disku CD-ROM. Poslední složka](../../manage/the-cd.latest-folder.md) aktualizované lokality. Configuration Manager vyžaduje, abyste použili zdrojové soubory, které odpovídají verzi existující lokality, ke které se vaše lokalita bude připojovat.  

2. Na stránce **než začnete** klikněte na tlačítko **Další**.  

3. Na stránce **Začínáme** vyberte typ lokality, kterou chcete nainstalovat:  

    - **Lokalita centrální správy**, jako první lokalita nové hierarchie nebo při rozšiřování samostatné primární lokality:  

        Vyberte **nainstalovat Configuration Manager lokalitu centrální správy**.  

        V pozdějším kroku tohoto postupu jste si zvolili možnost nainstalovat lokalitu centrální správy jako první lokalitu nové hierarchie, nebo nainstalovat lokalitu centrální správy pro rozšíření na samostatnou primární lokalitu.  

    - **Primární lokalita**jako samostatná primární lokalita, která je první lokalitou nové hierarchie, nebo jako podřízená primární:  

        Vyberte **nainstalovat Configuration Manager primární lokalitu**.  

        > [!TIP]  
        > V případě, že chcete nainstalovat samostatnou primární lokalitu v testovacím prostředí, budete obvykle vybírat jenom možnost **použít typické možnosti instalace samostatné primární lokality** . Když vyberete tuto možnost, instalační program provede následující akce:  
        >
        > - Automaticky nakonfiguruje lokalitu jako samostatnou primární lokalitu.  
        > - Používá výchozí instalační cestu.  
        > - Používá místní instalaci výchozí instance SQL Server pro databázi lokality.  
        > - Nainstaluje bod správy a distribuční bod na počítač serveru lokality.  
        > - Nakonfiguruje lokalitu s použitím angličtiny a jazyka zobrazení operačního systému na primárním serveru lokality, pokud odpovídá jednomu z jazyků, které Configuration Manager podporuje.  

4. Na stránce **kód Product Key** :  

    - Vyberte, jestli se má nainstalovat Configuration Manager jako zkušební edice nebo licencovaná edice.  

        - Pokud vyberete licencovanou verzi, zadejte kód Product Key a klikněte na tlačítko **Další**.  

        - Pokud vyberete zkušební edici, klikněte na tlačítko **Další**. (Instalaci zkušební verze můžete upgradovat na úplnou instalaci později.)  

    - Můžete také zadat **Datum vypršení platnosti licenční smlouvy Software Assurance** . Je to pohodlné připomenutí tohoto data. Pokud toto datum nezadáte během instalace, můžete ho zadat později v konzole Configuration Manager.  

        > [!NOTE]  
        > Microsoft neověřuje datum vypršení platnosti, které jste zadali, a nepoužívá toto datum pro ověření licence. Můžete ji použít jako připomenutí data vypršení platnosti. Toto datum je užitečné, protože Configuration Manager pravidelně kontroluje nové aktualizace softwaru, které jsou k dispozici online. Váš stav licence Software Assurance by měl být aktuální, takže máte nárok na použití těchto dalších aktualizací.  

    Další informace najdete v tématu [licencování a větve](../../../understand/learn-more-editions.md).  

5. Na stránce **licenční podmínky pro software společnosti Microsoft** si přečtěte licenční podmínky a přijměte je.  

6. Na stránce požadované **licence** si přečtěte a přijměte licenční podmínky pro požadovaný software. Instalační program stáhne a automaticky nainstaluje software na systémy lokality nebo klienty, pokud je to nutné. Před pokračováním na další stránku přijměte všechny podmínky.  

7. Na stránce **stažení požadovaných součástí** určete, zda má instalační program stáhnout nejnovější distribuovatelné soubory požadovaných součástí z Internetu nebo použít dříve stažené soubory:  

    - Pokud chcete, aby instalační program v tuto chvíli stáhl soubory, vyberte **Stáhnout požadované soubory**. Pak zadejte umístění pro uložení souborů.  

    - Pokud jste dříve stáhli soubory pomocí nástroje pro [stažení instalačního programu](setup-downloader.md), vyberte možnost **použít dříve stažené soubory**. Pak určete složku pro stahování.  

        > [!TIP]  
        > Pokud použijete dříve stažené soubory, ověřte, zda cesta ke složce pro stahování obsahuje poslední verzi souborů.  

8. Na stránce **Výběr jazyka serveru** vyberte jazyky, které jsou k dispozici pro konzolu Configuration Manager a pro sestavy. (Ve výchozím nastavení je zvolena angličtina a nelze ji odebrat.) Další informace najdete v tématu [jazykové sady](language-packs.md).  

9. Na stránce **Výběr jazyka klienta** vyberte jazyky, které jsou k dispozici pro klientské počítače. Také určete, jestli se mají povolit všechny jazyky klientů pro klienty mobilních zařízení. (Ve výchozím nastavení je zvolena angličtina a nelze ji odebrat.)  

    > [!IMPORTANT]  
    > Pokud používáte lokalitu centrální správy, ujistěte se, že jazyky klienta, které nakonfigurujete v lokalitě centrální správy, zahrnují všechny jazyky klienta, které nakonfigurujete v každé podřízené primární lokalitě. Klienti, kteří instalují z distribučního bodu, mají přístup k jazykům klienta z lokality nejvyšší úrovně, zatímco klienti, kteří instalují bod správy, mají přístup k jazykům klienta ze své přiřazené primární lokality.  

10. Na stránce **nastavení lokality a instalace** zadejte následující nastavení pro novou lokalitu, kterou instalujete:  

    - **Kód lokality**: [každý kód lokality v hierarchii musí být jedinečný](prepare-to-install-sites.md#bkmk_sitecodes). Použijte tři alfanumerické číslice: A až Z a 0 až 9. Vzhledem k tomu, že se kód lokality používá v názvech složek, nepoužívejte názvy rezervované pro systém Windows, včetně:  
        - POMOCNÉ  
        - PŘ  
        - NUL  
        - PRN  
        - SMS  

        > [!NOTE]  
        > Instalace neověřuje, jestli se zadaný kód lokality už používá, nebo jestli se jedná o rezervovaný název.  

    - **Název lokality**: každá lokalita vyžaduje tento popisný název, který vám může přispět k identifikaci lokality.  

    - **Instalační složka**: Tato složka je cesta k instalaci Configuration Manager. Po instalaci lokality nelze umístění změnit. Cesta nesmí obsahovat znaky Unicode ani koncové mezery.  

        > [!NOTE]  
        > Zvažte, zda chcete použít výchozí instalační složku. Pokud použijete výchozí oddíl OS v produkčním prostředí, může v budoucnu docházet k následujícím problémům:  
        >
        > - Pokud Configuration Manager používá další volné místo na disku v oddílu operačního systému, nebude systém Windows ani Configuration Manager správně fungovat. Pokud nainstalujete Configuration Manager do samostatného oddílu, jeho využití disku nebude mít vliv na operační systém.
        > - Configuration Manager výkon je lepší díky rychlému disku. Některé návrhy serverů neoptimalizují disk s operačním systémem na rychlost.
        > - Operační systém můžete obsluhovat, obnovovat nebo přeinstalovat, aniž by to ovlivnilo Configuration Manager instalaci.  

11. Na stránce **instalace lokality** použijte následující možnost, která odpovídá vašemu scénáři:  

    - **Instalujem lokalitu centrální správy:**  

        Na stránce **instalace lokality centrální správy** vyberte možnost **nainstalovat jako první lokalitu v nové hierarchii**a pokračujte výběrem možnosti **Další** .  

    - **Rozšířím samostatnou primární lokalitu do hierarchie s lokalitou centrální správy:**  

        Na stránce **instalace lokality centrální správy** vyberte možnost **rozšířit existující samostatnou primární lokalitu do hierarchie**. Pak zadejte plně kvalifikovaný název domény (FQDN) samostatného primárního serveru lokality a pokračujte kliknutím na tlačítko **Další** .  

        Médium, které použijete k instalaci nové lokality centrální správy, musí odpovídat verzi primární lokality.  

    - **Instalujem samostatnou primární lokalitu:**  

        Na stránce **Instalace primárního webového serveru** vyberte možnost **nainstalovat primární lokalitu jako samostatnou lokalitu**a pak zvolte možnost **Další**.  

    - **Instalujem podřízenou primární lokalitu:**  

        Na stránce **Instalace primárního webového serveru** vyberte možnost **připojit primární lokalitu k existující hierarchii**. Pak zadejte plně kvalifikovaný název domény pro lokalitu centrální správy a zvolte **Další**.  

12. Na stránce **informace o databázi** zadejte následující informace:  

    - **SQL Server název (FQDN)**: ve výchozím nastavení je tato hodnota nastavena na počítač serveru lokality.  

        Pokud používáte vlastní port, přidejte tento port do plně kvalifikovaného názvu domény SQL Server. Použijte plně kvalifikovaný název domény SQL Server čárkou a číslem portu. Například pro server *SQLServer1.fabrikam.com*použijte následující příkaz k zadání portu *1551*: `SQLServer1.fabrikam.com,1551`  

    - **Název instance**: ve výchozím nastavení je tato hodnota prázdná. Používá výchozí instanci SQL na počítači serveru lokality.  

    - **Název databáze**: ve výchozím nastavení je tato hodnota nastavena na `CM_<Sitecode>` . Tuto hodnotu můžete přizpůsobit.  

    - **Port Service Broker**: ve výchozím nastavení je tato hodnota nastavená na použití výchozího portu SQL Server Service Broker (SSB) 4022. SQL ho používá pro komunikaci přímo s databází lokality v jiných lokalitách.  

13. Na stránce s **informacemi o druhé databázi** můžete zadat vlastní umístění pro SQL Server datový soubor a soubor protokolu SQL Server pro databázi lokality:  

    - Ve výchozím nastavení používá výchozí umístění souborů pro SQL Server.  

    - Když použijete cluster SQL Server, možnost zadat vlastní umístění souborů není k dispozici.  

    - Kontrola požadovaných součástí nespustí kontrolu volného místa na disku pro vlastní umístění souborů.  

14. Na stránce **Nastavení poskytovatele služby SMS** zadejte plně kvalifikovaný název domény pro server, na který chcete nainstalovat poskytovatele služby SMS.  

    - Ve výchozím nastavení určuje server lokality.  

    - Po instalaci lokality můžete nakonfigurovat další poskytovatele serveru SMS. Další informace najdete v tématu [plánování poskytovatele serveru SMS](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

15. Na stránce **Nastavení komunikace s klientem** vyberte, zda chcete konfigurovat všechny systémy lokality tak, aby přijímaly pouze komunikaci přes protokol HTTPS od klientů, nebo zda má být metoda komunikace nakonfigurována pro každou roli systému lokality.  

    Když vyberete možnost **všechny role systému lokality přijmout jenom komunikaci přes protokol HTTPS od klientů**, musí mít klientský počítač platný certifikát PKI pro ověření klienta. Další informace najdete v tématu [požadavky na certifikát PKI](../../../plan-design/network/pki-certificate-requirements.md).  

    > [!NOTE]  
    > Tento krok platí jenom při instalaci primární lokality. Pokud instalujete lokalitu centrální správy, tento krok přeskočte.  

16. Na stránce **role systému lokality** vyberte, zda chcete nainstalovat bod správy nebo distribuční bod. Pro každou roli, kterou si zvolíte k instalaci pomocí instalačního programu:  

    - Zadejte **plně kvalifikovaný název domény** pro server, který bude hostitelem role. Pak zvolte metodu připojení klienta, kterou bude server podporovat: HTTP nebo HTTPS.  

    - Pokud jste vybrali možnost **všechny role systému lokality přijímají pouze komunikaci přes protokol HTTPS od klientů** na předchozí stránce, budou nastavení připojení klienta automaticky nakonfigurována pro protokol HTTPS. Toto nastavení nemůžete změnit, pokud se nevrátíte na předchozí stránku.  

    > [!NOTE]  
    > Tento krok platí jenom při instalaci primární lokality. Pokud instalujete lokalitu centrální správy, tento krok přeskočte.  

    > [!NOTE]  
    > Pro instalaci rolí systému lokality instalační program používá **účet instalace systému lokality**. Ve výchozím nastavení se používá účet počítače primární lokality. Aby bylo možné nainstalovat roli systému lokality, musí být tento účet místním správcem na vzdáleném počítači. Pokud tento účet nemá požadovaná oprávnění, zrušte kontrolu rolí systému lokality a nainstalujte je později z konzoly Configuration Manager, a to po nakonfigurování dalších účtů, které se použijí jako účty instalace systému lokality. Další informace najdete v tématu [účty](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).  

17. Na stránce **data o využití** si přečtěte informace o datech, která Microsoft shromažďuje, a pak zvolte **Další**. Další informace najdete v tématu [Diagnostika a data o využití](../../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

18. Stránka pro **Nastavení spojovacího bodu služby** je k dispozici pouze v následujících scénářích:  

    - Při instalaci samostatné primární lokality.  

    - Při instalaci lokality centrální správy.  

    > [!NOTE]  
    > Pokud instalujete podřízenou primární lokalitu, tento krok přeskočte.  

     Pokud instalujete lokalitu centrální správy jako součást scénáře rozšíření lokality a tato role je již nainstalována v samostatné primární lokalitě, nejprve tuto roli Odinstalujte ze samostatné primární lokality. V hierarchii je povolena pouze jedna instance této role a je podporována pouze v lokalitě nejvyšší úrovně v hierarchii.  

     Po výběru konfigurace **spojovacího bodu služby**klikněte na tlačítko **Další**. Po dokončení instalace můžete tuto konfiguraci změnit v konzole Configuration Manager. Další informace najdete v tématu [o spojovacím bodu služby](../configure/about-the-service-connection-point.md).  

19. Na stránce **Souhrn nastavení** zkontrolujte nastavení, které jste vybrali. Až budete připraveni, klikněte na tlačítko **Další** a spusťte kontrolu požadovaných součástí.  

20. Na stránce **Kontrola požadovaných součástí instalace** se zobrazí všechny problémy, které může kontrola identifikovat.  

    - Pokud nástroj pro kontrolu požadovaných součástí nalezne problém, vyberte položku v seznamu, kde najdete podrobnosti o tom, jak tento problém vyřešit.  

    - Než budete moct pokračovat v instalaci lokality, vyřešte **chybné** položky. Také se pokuste vyřešit položky se stavem **Upozornění**, ale neblokuje instalaci lokality.  

    - Po vyřešení problémů vyberte **Spustit kontrolu** a znovu spusťte kontrolu požadovaných součástí.  

        Když se spustí Kontrola požadovaných součástí a žádné kontroly neobdrží stav **selhání** , můžete zvolit možnost spustit **instalaci** a spustit instalaci lokality.  

    > [!TIP]  
    > Kromě zpětné vazby, kterou průvodce poskytuje, můžete najít další informace o problémech se splněním požadavků v souboru **souboru ConfigMgrPrereq. log** . Je v kořenovém adresáři systémové jednotky počítače, do kterého instalujete lokalitu nástroje. Další informace najdete v tématu [seznam kontrol požadovaných součástí](list-of-prerequisite-checks.md).  

21. Na stránce **instalace** zobrazí instalační program stav instalace. Po dokončení instalace základního serveru lokality můžete Průvodce instalací **Zavřít** . Po zavření průvodce budou konfigurace instalace a počáteční lokality pokračovat na pozadí.  

    - Konzolu Configuration Manager můžete připojit k lokalitě před dokončením instalace. Tato konzola se připojuje jako jen pro čtení a umožňuje zobrazit objekty a nastavení, ale nemůžete upravovat cokoli.  

    - Po dokončení instalace můžete připojit konzolu, která může upravovat objekty a nastavení.  


## <a name="expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> Rozšíření samostatné primární lokality

Pokud jste jako první lokalitu nainstalovali samostatnou primární lokalitu, máte možnost později rozšířit tuto lokalitu do větší hierarchie tím, že nainstalujete lokalitu centrální správy.

Když rozbalíte samostatnou primární lokalitu, nainstalujete novou lokalitu centrální správy, která jako referenci používá existující databázi samostatné primární lokality. Po instalaci nové lokality centrální správy funkce samostatná primární lokalita funguje jako podřízená primární lokalita.

- Samostatnou primární lokalitu můžete rozšířit jenom na novou hierarchii.  

- Můžete rozšířit jenom jednu samostatnou primární lokalitu do konkrétní hierarchie. Tuto možnost nemůžete použít k připojení dalších samostatných primárních lokalit do stejné hierarchie. Místo toho použijte Průvodce migrací k migraci dat z jedné hierarchie do jiné. Další informace najdete v tématu [migrace dat mezi hierarchiemi](../../../migration/migrate-data-between-hierarchies.md).  

- Jakmile rozbalíte samostatnou lokalitu do hierarchie s lokalitou centrální správy, můžete přidat další podřízené primární podřízené lokality.  

- Chcete-li odebrat primární lokalitu z hierarchie s lokalitou centrální správy, nejprve odinstalujte primární lokalitu.  

Chcete-li lokalitu rozšířit, použijte Průvodce instalací nástroje Configuration Manager k instalaci nové lokality centrální správy s následujícími omezeními:  

- Nainstalujte lokalitu centrální správy pomocí stejné verze Configuration Manager jako samostatnou primární lokalitu.  

- Na stránce **Začínáme** v Průvodci instalací vyberte možnost instalace lokality centrální správy. V pozdější fázi instalace zvolíte možnost rozšíření existující samostatné primární lokality.  

- Když nakonfigurujete stránku pro **Výběr jazyka klienta** pro novou lokalitu centrální správy, vyberte stejné jazyky klienta, které jsou nakonfigurované pro samostatnou primární lokalitu, kterou rozšiřujete.  

- Na stránce **instalace lokality** vyberte možnost rozšířit samostatnou primární lokalitu.  

Chcete-li rozšířit samostatnou primární lokalitu, nejprve se podívejte na [požadavky pro rozšíření lokality](prerequisites-for-installing-sites.md#bkmk_expand). Pak použijte postup [k instalaci lokality primární nebo centrální správy](use-the-setup-wizard-to-install-sites.md#bkmk_installpri) dříve v tomto článku.


## <a name="install-a-secondary-site"></a><a name="bkmk_secondary"></a> Instalace sekundární lokality

K instalaci sekundární lokality použijte konzolu Configuration Manager.  

- Pokud konzola, kterou používáte, není připojena k primární lokalitě, která bude nadřazenou lokalitou pro novou sekundární lokalitu, bude příkaz pro instalaci lokality replikován do správné primární lokality.  

- Před zahájením instalace lokality se ujistěte, že váš uživatelský účet má požadovaná oprávnění. Také se ujistěte, že server, který bude hostitelem nové sekundární lokality, splňuje všechny předpoklady pro použití jako server sekundární lokality.  

- Když nainstalujete sekundární lokalitu, Configuration Manager nakonfiguruje novou lokalitu tak, aby používala porty komunikace klienta, které jsou nakonfigurované v nadřazené primární lokalitě.  

### <a name="process-to-install-a-secondary-site"></a><a name="bkmk_installsecondary"></a> Proces instalace sekundární lokality  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** . Vyberte lokalitu, která bude nadřazenou primární lokalitou nové sekundární lokality.  

2. Chcete-li spustit **Průvodce vytvořením sekundární lokality**, vyberte možnost **vytvořit sekundární lokalitu** na pásu karet.  

3. Na stránce **než začnete** potvrďte, že primární lokalita, která je uvedená, je lokalitou, kterou chcete být nadřazenou pro novou sekundární lokalitu. Pak klikněte na tlačítko **Další**.  

4. Na stránce **Obecné** určete následující nastavení:  

    - **Kód lokality**: každý kód lokality v hierarchii musí být jedinečný. Použijte tři alfanumerické číslice: A až Z a 0 až 9. Vzhledem k tomu, že se kód lokality používá v názvech složek, nepoužívejte názvy rezervované pro systém Windows, včetně:  

        - POMOCNÉ  
        - PŘ  
        - NUL  
        - PRN  
        - SMS  

    > [!NOTE]  
    > Instalace neověřuje, jestli se zadaný kód lokality už používá, nebo jestli se jedná o rezervovaný název.  

    - **Název serveru lokality**: Tato hodnota je plně kvalifikovaný název domény serveru, na který se bude instalovat nová sekundární lokalita.  

    - **Název lokality**: každá lokalita vyžaduje tento popisný název, který vám může přispět k identifikaci lokality.  

    - **Instalační složka**: Tato složka je cesta k instalaci Configuration Manager. Po instalaci lokality nelze umístění změnit. Cesta nesmí obsahovat znaky Unicode ani koncové mezery.  

    > [!IMPORTANT]  
    > Po zadání podrobností na této stránce můžete vybrat položku **Souhrn** a přejít přímo na stránku **Souhrn** v průvodci. Tato akce použije výchozí nastavení pro zbytek možností sekundární lokality.  
    > 
    > - Tuto možnost použijte pouze v případě, že jste obeznámeni s výchozím nastavením v tomto průvodci a jedná se o nastavení, které chcete použít.  
    > - Když použijete výchozí nastavení, skupiny hranic nejsou přidružené k distribučnímu bodu. Dokud neprovedete konfiguraci skupin hranic, které zahrnují server sekundární lokality, nebudou klienti používat distribuční bod, který je nainstalován v této sekundární lokalitě, jako umístění zdroje obsahu.  

5. Na stránce **zdrojové instalační soubory** vyberte způsob, jakým počítač sekundární lokality získá zdrojové soubory pro instalaci lokality.  

    Při použití CD. Nejnovější zdrojové soubory, které jsou sdíleny v síti nebo lokálně zkopírovány do cílového sekundárního serveru lokality:  

    - **Verze 1802 a starší**

        - Disk CD. Nejnovější umístění zdrojových souborů obsahuje složku s názvem **Redist**. Přesuňte tuto složku pro **redistribuci** jako podsložku do složky **SMSSETUP** .  

            > [!Note]  
            > Pokud dojde k chybám při neshodě hodnoty hash během instalace, aktualizujte složku **Redist** . Nejnovější soubory získáte pomocí nástroje pro [stažení instalačního programu](setup-downloader.md) . Pro všechny soubory, které způsobují chybu neshody hodnoty hash, je také zkopírujte z aktualizované složky **Redist** do složky **SMSSETUP\BIN\X64** .

    - **Verze 1806 a novější**<!-- SCCMDocs-pr issue 3164 -->

        - Disk CD. Nejnovější umístění zdrojových souborů obsahuje složku s názvem **Redist**. Přesuňte tuto složku pro **redistribuci** jako podsložku do složky **SMSSETUP** .  

        - Zkopírujte následující soubory ze složky **Redist** do složky **SMSSETUP\BIN\X64** :  
            - SharedManagementObjects.msi
            - SQLSysClrTypes.msi
            - sqlncli.msi

    - Pokud některý ze souborů z **Redist** není k dispozici, instalace sekundární lokality se nezdařila.  

    - Účet počítače serveru sekundární lokality musí mít oprávnění **ke čtení** pro složku zdrojového souboru a sdílenou složku.  

6. Na stránce **nastavení SQL Server** určete verzi SQL Server, která se má použít, a pak nakonfigurujte související nastavení.  

    > [!NOTE]  
    > Instalační program neověřuje informace, které jste zadali na této stránce, dokud nespustí instalaci. Než budete pokračovat, ověřte tato nastavení.  

    - **Instalace a konfigurace místní kopie SQL Express na počítači sekundární lokality**  

        - **Port služby SQL Server**: zadejte port služby SQL Server pro SQL Server Express, který se má použít. Port služby je obvykle nakonfigurovaný tak, aby používal port TCP 1433, ale můžete nakonfigurovat jiný port.  

        - **Port služby SQL Server Broker**: zadejte port SQL Server Service Broker (SSB), který má SQL Server Express použít. Service Broker je obvykle nakonfigurovaný tak, aby používal port TCP 4022, ale můžete nakonfigurovat jiný port. Zadejte platný port, který žádný jiný web nebo služba nepoužívá a že neblokuje žádná omezení brány firewall.  

    - **Použít existující instanci SQL Server**  

        - **SQL Server plně kvalifikovaný název domény**: Zkontrolujte plně kvalifikovaný název domény počítače, na kterém běží SQL Server. K hostování databáze sekundární lokality je nutné použít místní server se systémem SQL Server a toto nastavení nemůžete změnit.  

        - **SQL Server instance**: zadejte instanci SQL Server, která se má použít jako databáze sekundární lokality. Tuto možnost nechte prázdné, pokud chcete použít výchozí instanci.  

        - **Název databáze lokality nástroje ConfigMgr**: zadejte název, který má být použit pro databázi sekundární lokality.  

        - **Port služby SQL Server Broker**: zadejte port SQL Server Service Broker (SSB), který má SQL Server použít. Zadejte platný port, který žádný jiný web nebo služba nepoužívá a který nebude blokovat omezení brány firewall.  

    > [!TIP]  
    > Seznam verzí SQL Server, které Configuration Manager podporuje, najdete v tématu [podporované verze SQL Server](../../../plan-design/configs/support-for-sql-server-versions.md).  

7. Na stránce **distribuční bod** nakonfigurujte nastavení distribučního bodu, který bude nainstalován na server sekundární lokality.  

    - **Požadovaná nastavení:**  

        - **Určete, jak klientská zařízení komunikují s distribučním bodem**: Zvolte mezi http a HTTPS.  

        - **Vytvoření certifikátu podepsaného svým držitelem nebo Import klientského certifikátu PKI**: vyberte, jestli se má použít certifikát podepsaný svým držitelem nebo jak importovat certifikát z infrastruktury veřejných klíčů (PKI). Certifikát podepsaný svým držitelem vám umožní taky anonymní připojení z Configuration Manager klientů do knihovny obsahu. Certifikát se používá k ověření distribučního bodu do bodu správy předtím, než distribuční bod odešle stavové zprávy. Další informace najdete v tématu [požadavky na certifikát PKI](../../../plan-design/network/pki-certificate-requirements.md).  

    - **Volitelná nastavení:**  

        - V **případě potřeby nainstalujte a NAKONFIGURUJTE IIS pomocí Configuration Manager**: Toto nastavení vyberte, pokud chcete, aby Configuration Manager nainstalovat a nakonfigurovat Internetová informační služba (IIS) na serveru, pokud ještě není nainstalovaná. Služba IIS je vyžadována na všech distribučních bodech.  

            > [!NOTE]  
            > I když je toto nastavení volitelné, musí být na serveru nainstalovaná služba IIS, aby bylo možné úspěšně nainstalovat distribuční bod.  

        - **Povolit a nakonfigurovat službu BranchCache pro tento distribuční bod**  

        - **Popis**: Tato hodnota je popisným popisem distribučního bodu, který vám usnadní jeho rozpoznání.  

        - **Povolit tento distribuční bod pro připravený obsah**  

8. Na stránce **Nastavení jednotky** zadejte nastavení jednotky pro distribuční bod sekundární lokality.  

    Můžete nakonfigurovat až dvě diskové jednotky pro knihovnu obsahu a dvě diskové jednotky pro sdílenou složku balíčku. Configuration Manager ale můžou použít další jednotky, když první dva dosáhnou nakonfigurované rezervy místa na disku. Na stránce **Nastavení jednotky** můžete nakonfigurovat prioritu pro diskové jednotky a množství volného místa na disku, které se má na všech diskových jednotkách zůstat.  

    - **Rezerva místa na disku (MB)**: hodnota, kterou konfigurujete pro toto nastavení, určuje množství volného místa na jednotce, než Configuration Manager zvolí jinou jednotku a pokračuje v procesu kopírování na tuto jednotku. Soubory obsahu mohou být rozmístěny na několika jednotkách.  

    - **Umístění obsahu**: Určete umístění obsahu pro knihovnu obsahu a sdílenou složku balíčku. Configuration Manager kopíruje obsah do primárního umístění obsahu, dokud velikost volného místa nedosáhne hodnoty zadané v poli **Rezerva místa na disku (MB)**.  

    Ve výchozím nastavení jsou umístění obsahu nastavena na hodnotu **automaticky**. Primární umístění obsahu je nastaveno na diskovou jednotku, která má nejvíce místa na disku v době instalace. Sekundární umístění je nastaveno na diskovou jednotku, která má nejvíce volného místa na disku po primární jednotce. Když primární a sekundární jednotky dosáhnou rezervovaného místa na disku, Configuration Manager vybere jinou dostupnou jednotku s největším množstvím volného místa na disku a pokračuje v procesu kopírování.  

9. Na stránce **ověření obsahu** určete, zda má být ověřena integrita souborů obsahu v distribučním bodě.  

    - Když povolíte ověření obsahu podle plánu, Configuration Manager spustí proces v naplánovaném čase. Veškerý obsah v distribučním bodě je ověřen.  

    - Můžete také nakonfigurovat **prioritu ověření obsahu**.  

    - Chcete-li zobrazit výsledky procesu ověřování obsahu, v konzole Configuration Manager klikněte na pracovní prostor **monitorování** , rozbalte položku **stav distribuce**a vyberte uzel **stav obsahu** . Zobrazuje obsah pro každý typ balíčku. Mezi tyto typy patří aplikace, balíčky aktualizací softwaru a spouštěcí image.  

10. Na stránce **skupiny hranic** spravujte skupiny hranic, ke kterým je tento distribuční bod přiřazen:  

    - Během nasazování obsahu musí být klienti ve skupině hranic, která je přidružená k distribučnímu bodu, aby ji bylo možné použít jako zdrojové umístění obsahu.  

    - Můžete vybrat možnost **umožnit záložní umístění zdroje pro obsah** , aby klienti mimo tyto skupiny hranic mohli vracet a používat distribuční bod jako umístění zdroje obsahu, když nejsou k dispozici žádné preferované distribuční body.  

        Další informace najdete v tématu [základní koncepty správy obsahu](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

11. Na stránce **Souhrn** zkontrolujte nastavení a pak kliknutím na tlačítko **Další** nainstalujte sekundární lokalitu. Když průvodce zobrazí stránku **dokončení** , můžete Průvodce zavřít. Instalace sekundární lokality pokračuje na pozadí.  

### <a name="how-to-verify-the-secondary-site-installation-status"></a><a name="bkmk_verify"></a> Ověření stavu instalace sekundární lokality  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** .  

2. Vyberte sekundární lokalitu, kterou instalujete, a poté na pásu karet zvolte možnost **Zobrazit stav instalace** .  

    > [!TIP]  
    > Při instalaci více než jedné sekundární lokality v jednom okamžiku se spustí Kontrola požadovaných součástí na jedné lokalitě. Aby bylo možné spustit další lokalitu, je třeba dokončit lokalitu.