---
title: Migrace obsahu
titleSuffix: Configuration Manager
description: Pomocí distribučních bodů můžete spravovat obsah při migraci dat do cílové hierarchie Configuration Manager aktuální větve.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 66f7759c-6272-4116-aad7-0d05db1d46cd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: afb39af5087daaca3b2bb6eb15f33d81d959beec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719684"
---
# <a name="plan-a-content-deployment-migration-strategy-in-configuration-manager"></a>Plánování strategie migrace nasazení obsahu v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Když aktivně migrujete data do cílové hierarchie Configuration Manager aktuální větve, klienti Configuration Manager ve zdrojové i cílové hierarchii můžou udržovat přístup k obsahu, který jste nasadili ve zdrojové hierarchii. Pomocí migrace můžete také upgradovat nebo znovu přiřadit distribuční body ze zdrojové hierarchie, aby se staly distribučními body v cílové hierarchii. Když sdílíte a upgradujete nebo znovu přiřazujete distribuční body, může vám tato strategie pomoci vyhnout se nutnosti nasazení obsahu do nových serverů v cílové hierarchii pro klienty, které migrujete.  

I když můžete znovu vytvořit a distribuovat obsah do cílové hierarchie, můžete pro správu tohoto obsahu použít také následující možnosti:  

-   Sdílet distribuční body ve zdrojové hierarchii s klienty v cílové hierarchii.  

-   Upgradujte samostatné Configuration Manager 2007 distribučních bodů nebo Configuration Manager 2007 sekundárních lokalit ve zdrojové hierarchii, aby se staly distribučními body v cílové hierarchii.  

-   Znovu přiřadit distribuční body ze zdrojové hierarchie Configuration Manager do lokality v cílové hierarchii.  

##  <a name="share-distribution-points-between-source-and-destination-hierarchies"></a><a name="About_Shared_DPs_in_Migration"></a> Sdílení distribučních bodů mezi zdrojovými a cílovými hierarchiemi  
Během migrace můžete sdílet distribuční body ze zdrojové hierarchie s cílovou hierarchií. Sdílené distribuční body můžete použít k okamžitému zpřístupnění obsahu, který jste migrovali ze zdrojové hierarchie, klientům v cílové hierarchii bez nutnosti opětného vytváření tohoto obsahu a pak jej distribuovat do nových distribučních bodů v cílové hierarchii. Když klienti v cílové hierarchii požadují obsah, který je nasazen v distribučních bodech, které sdílíte, lze klientům poskytnout tyto sdílené distribuční body jako platná umístění obsahu.  

 Kromě platného umístění obsahu pro klienty v cílové hierarchii, zatímco migrace ze zdrojové hierarchie zůstává aktivní, je možné upgradovat nebo znovu přiřadit distribuční bod cílové hierarchii. Můžete upgradovat Configuration Manager 2007 sdílených distribučních bodů a znovu přiřadit služby System Center 2012 Configuration Manager Shared Distribution Points. Když upgradujete nebo znovu přiřadíte sdílený distribuční bod, ze zdrojové hierarchie je distribuční bod odstraněn a stává se distribučním bodem v cílové hierarchii. Po upgradování nebo opětném přiřazení distribučního bodu můžete dále používat distribuční bod v cílové hierarchii po dokončení migrace ze zdrojové hierarchie. Další informace o upgradu sdíleného distribučního bodu najdete v tématu [plánování upgradu Configuration Manager 2007 sdílených distribučních bodů](#Planning_to_Upgrade_DPs). Další informace o tom, jak znovu přiřadit sdílený distribuční bod, najdete v tématu [Plánování opětovného přiřazení Configuration Manager distribučních bodů](#BKMK_ReassignDistPoint).  

 Sdílení distribučních bodů můžete zvolit v kterékoli zdrojové lokalitě ve vaší zdrojové hierarchii. Když sdílíte distribuční body pro zdrojovou lokalitu, podřízené sekundární lokality se sdílejí v každém opravňujícím distribučním bodu v této primární lokalitě a v každé primární lokalitě. Aby bylo možné zajistit, aby se jedná o sdílený distribuční bod, musí být server systému lokality, který je hostitelem distribučního bodu, nastaven s plně kvalifikovaným názvem domény (FQDN). Všechny distribuční body, které jsou nastaveny s názvem NetBIOS, jsou ignorovány.  

> [!TIP]  
>  Configuration Manager 2007 nevyžaduje, abyste nastavili plně kvalifikovaný název domény pro servery systému lokality.  

Následující informace vám pomohou plánovat sdílené distribuční body:  

-   Distribuční body, které sdílíte, musí splňovat nezbytné podmínky pro sdílené distribuční body. Další informace o těchto požadavcích najdete v tématu [požadované konfigurace pro migraci](../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations) v části [požadavky pro migraci](../../core/migration/prerequisites-for-migration.md).  

-   Akce sdíleného distribučního bodu je nastavení pro celou lokalitu sdílející všechny oprávněné distribuční body ve zdrojové lokalitě a ve všech přímých podřízených sekundárních lokalitách. Když povolíte sdílení distribučních bodů, nemůžete ke sdílení zvolit jednotlivé distribuční body.  

-   Klienti v cílové hierarchii mohou přijímat informace o umístění obsahu pro balíčky, které jsou distribuovány do distribučních bodů, které jsou sdíleny ze zdrojové hierarchie. U distribučních bodů ze zdrojové hierarchie Configuration Manager 2007 zahrnuje distribuční body větve, distribuční body na sdílených složkách serveru a standardní distribuční body.  

    > [!WARNING]  
    >  Pokud změníte zdrojovou hierarchii, sdílené distribuční body z původní zdrojové hierarchie již nebudou dostupné a nelze je poskytnout jako umístění obsahu pro klienty v cílové hierarchii. Pokud překonfigurujete migraci k použití původní zdrojové hierarchie, dříve sdílené distribuční body se obnoví jako platné servery umístění obsahu.  

-   Když migrujete balíček, jejímž hostitelem je sdílený distribuční bod, verze balíčku musí zůstat stejná ve zdrojové i cílové hierarchii. Pokud verze balíčku není stejná ve zdrojové i cílové hierarchii, klienti v cílové hierarchii nemohou načíst tento obsah ze sdíleného distribučního bodu. Proto když aktualizujete balíček ve zdrojové hierarchii, musíte znovu migrovat data balíčku, aby klienti v cílové hierarchii mohli načíst tento obsah ze sdíleného distribučního bodu.  

    > [!NOTE]  
    >  Pokud zobrazíte podrobnosti balíčku, jehož hostitelem je sdílený distribuční bod, počet balíčků, který se zobrazuje jako **hostované migrované balíčky** na kartě **sdílené distribuční body** zdrojové lokality, není aktualizován, dokud není dokončen další cyklus shromažďování dat.  

-   Sdílené distribuční body a jejich vlastnosti můžete zobrazit v uzlu **zdrojová hierarchie** pracovního prostoru **Správa** v konzole nástroje Configuration Manager, která se připojuje k cílové hierarchii.  

-   Sdílený distribuční bod ze zdrojové hierarchie Configuration Manager 2007 nelze použít k hostování balíčků pro Microsoft Application Virtualization (App-V). Balíčky App-V musí migrovat a musí být převedeny pro používání klienty v cílové hierarchii. Pro hostování balíčků App-V pro klienty v cílové hierarchii ale můžete použít sdílený distribuční bod ze služby System Center 2012 Configuration Manager nebo Configuration Manager aktuální zdrojové hierarchie větve.  

-   Když sdílíte chráněný distribuční bod ze zdrojové hierarchie Configuration Manager 2007, cílová hierarchie vytvoří skupinu hranic, která zahrnuje chráněná síťová umístění tohoto distribučního bodu. Tuto skupinu hranic v cílové hierarchii nemůžete změnit. Pokud však změníte informace o chráněném hraničním umístění distribučního bodu ve zdrojové hierarchii Configuration Manager 2007, tato změna se projeví v cílové hierarchii po dokončení příštího cyklu shromažďování dat.  

    > [!NOTE]  
    >  Služby System Center 2012 Configuration Manager a Configuration Manager aktuální pobočky používají koncept upřednostňovaných distribučních bodů místo chráněných distribučních bodů. Tato podmínka platí pouze pro distribuční body, které jsou sdíleny ze zdrojových lokalit Configuration Manager 2007.  

Po sdílení distribučních bodů ze zdrojové lokality nejsou způsobilé distribuční body viditelné v konzole Configuration Manager. Po sdílení distribučních bodů jsou uvedeny pouze distribuční body, které jsou úspěšně sdíleny.  

Po sdílení distribučních bodů můžete změnit konfiguraci kteréhokoli sdíleného distribučního bodu ve zdrojové hierarchii. Změny, které provedete v konfiguraci distribučního bodu se odrazí v cílové hierarchii po příštím cyklu shromažďování dat. Distribuční body, které jste aktualizovali k získání oprávnění pro sdílení, jsou sdíleny automaticky, zatímco distribuční body, které již nemají oprávnění, ukončí sdílení. Můžete mít například distribuční bod, který není nastaven s intranetovým plně kvalifikovaným názvem domény a původně sdílený s cílovou hierarchií. Po nastavení plně kvalifikovaného názvu domény pro tento distribuční bod Tato konfigurace identifikuje další cyklus shromažďování dat a distribuční bod bude poté sdílen s cílovou hierarchií.  

##  <a name="plan-to-upgrade-configuration-manager-2007-shared-distribution-points"></a><a name="Planning_to_Upgrade_DPs"></a>Plánování upgradu Configuration Manager 2007 sdílených distribučních bodů  
Když migrujete ze zdrojové hierarchie Configuration Manager 2007, můžete upgradovat sdílený distribuční bod a vytvořit tak Configuration Manager aktuální distribuční bod větve. Distribuční body můžete upgradovat v primárních a sekundárních lokalitách. Proces upgradu odstraní distribuční bod z hierarchie Configuration Manager 2007 a vytvoří ho jako server systému lokality v cílové hierarchii. Tento proces také zkopíruje existující obsah, který je v distribučním bodě, do nového umístění v počítači distribučního bodu. Proces upgradování pak upravením kopie obsahu vytvoří samostatné úložiště instance k použití při nasazení obsahu v cílové hierarchii. Proto když upgradujete distribuční bod, nemusíte znovu distribuovat migrovaný obsah, který byl hostován v distribučním bodu Configuration Manager 2007.  

Jakmile Configuration Manager převede obsah na ukládání jediné instance, Configuration Manager odstraní původní zdrojový obsah na počítači distribučního bodu a uvolní místo na disku. Configuration Manager nepoužívá původní umístění zdrojového obsahu.  

Ne všechny distribuční body Configuration Manager 2007, které můžete sdílet, jsou způsobilé pro upgrade na Configuration Manager aktuální větev. Aby byl distribuční bod Configuration Manager 2007 pro upgrade způsobilý, musí splňovat podmínky pro upgrade. Tyto podmínky zahrnují server systému lokality, na kterém je distribuční bod nainstalován, a typ Configuration Manager 2007 distribučního bodu, který je nainstalován. Například nemůžete upgradovat typ distribučního bodu, který je nainstalován na počítači serveru primární lokality, ale můžete upgradovat standardní distribuční bod, který je nainstalován na počítači serveru sekundární lokality.  

> [!NOTE]  
>  Můžete upgradovat pouze ty sdílené distribuční body Configuration Manager 2007, které se nacházejí v počítači, na kterém je spuštěna verze operačního systému, která je podporována pro distribuční body v cílové hierarchii. I když například můžete sdílet distribuční bod Configuration Manager 2007, který je v počítači se systémem Windows Vista, nemůžete tento sdílený distribuční bod upgradovat, protože operační systém není podporován Configuration Manager aktuální větev pro použití jako distribuční bod.  

Následující tabulka uvádí podporovaná umístění pro každý typ Configuration Manager 2007 distribuční bod, který můžete upgradovat.  

|Typ distribučního bodu|Distribuční bod na jiném počítači systému lokality, než je server lokality|Distribuční bod na jiném počítači systému lokality, než je server lokality a který je hostitelem jiných rolí systému lokality|Distribuční bod na serveru sekundární lokality|  
|--------------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------------------------------------------|  
|Standardní distribuční bod|Ano|Ne|Ano|  
|Distribuční bod na sdíleních serveru<sup>1</sup>|Ano|Ne|Ne|  
|Distribuční bod větve|Ano|Ne|Ne|  

 <sup>1</sup> Configuration Manager aktuální větev nepodporuje sdílení serverů pro systémy lokalit, ale podporuje upgrade Configuration Manager 2007 distribučního bodu, který je na sdílené složce serveru. Když upgradujete distribuční bod Configuration Manager 2007, který je ve sdílené složce serveru, typ distribučního bodu je automaticky převeden na server a musíte vybrat jednotku na počítači distribučního bodu, na které bude uloženo úložiště obsahu jediné instance.  

> [!WARNING]  
>  Před upgradem distribučního bodu větve odinstalujte klientský software Configuration Manager 2007. Když upgradujete distribuční bod větve, který má nainstalovaný klientský software Configuration Manager 2007, obsah, který byl dříve na počítači nasazen, bude z počítače odstraněn a upgrade distribučního bodu se nezdařil.  

Chcete-li identifikovat distribuční body, které mají nárok na upgrade v konzole Configuration Manager v uzlu **zdrojová hierarchie** , vyberte zdrojovou lokalitu a pak vyberte kartu **sdílené distribuční body** . způsobilých distribučních bodů se ve sloupci **způsobilo pro upgrade** zobrazují **Ano** .  

Když upgradujete distribuční bod, který je nainstalován na sekundárním serveru lokality Configuration Manager 2007, je sekundární lokalita odinstalována ze zdrojové hierarchie. Přestože se tento scénář nazývá upgrade sekundární lokality, vztahuje se pouze na role systému lokality distribučního bodu. Výsledkem je, že sekundární lokalita není upgradována, a místo toho je odinstalována. Tím se v počítači, který byl serverem sekundární lokality, opustí distribuční bod z cílové hierarchie. Pokud plánujete upgrade distribučního bodu na sekundární lokalitě, přečtěte si téma [plánování upgradu Configuration Manager 2007 sekundárních lokalit](#BKMK_UpgradeSS) v tomto tématu.  

###  <a name="distribution-point-upgrade-process"></a><a name="BKIMK_UpgradeProcess"></a>Proces upgradu distribučního bodu  
K upgradu Configuration Manager 2007 distribučních bodů, které jste sdíleli s cílovou hierarchií, můžete použít konzolu Configuration Manager. Při upgradu sdíleného distribučního bodu je distribuční bod odinstalován z lokality Configuration Manager 2007. Pak je nainstalován jako distribuční bod, který je připojen k primární nebo sekundární lokalitě, kterou zadáte v cílové hierarchii. Proces upgradu vytváří kopii migrovaného obsahu, který je uložen na distribučním bodu, a následně převádí kopii do ukládání obsahu jediné instance. Když Configuration Manager převede balíček na ukládání obsahu jediné instance, odstraní tento balíček ze sdílené složky SMSPKG na počítači distribučního bodu, pokud balíček nemá alespoň jednu reklamu, která je nastavená tak, aby **spouštěla program z distribučního bodu**.  

K upgradu distribučního bodu Configuration Manager používá účet pro **přístup ke zdrojové lokalitě** , který je nastaven na shromažďování dat od poskytovatele serveru SMS zdrojové lokality. Přestože tento účet vyžaduje ke shromažďování dat ze zdrojové lokality pouze oprávnění **ke čtení** pro objekty lokality, musí mít rovněž oprávnění k **odstranění** a **změně** ve třídě **lokalita** , aby mohl během upgradu úspěšně odebrat distribuční bod z lokality Configuration Manager 2007.  

> [!NOTE]  
>  Configuration Manager může převést obsah na ukládání jediné instance současně pouze na jednom distribučním bodu. Při nastavování více upgradů distribučních bodů jsou distribuční body zařazeny do fronty pro upgrade a zpracování v jednom okamžiku.  

Před upgradem sdíleného distribučního bodu se ujistěte, že je migrován všechen obsah, který je nasazen na distribučním bodu. Obsah, jehož migraci neprovedete před upgradem distribučního bodu, nebude po dokončení upgradu v cílové hierarchii dostupný. Když upgradujete distribuční bod, je obsah v migrovaných balíčcích převeden do formátu, který je kompatibilní s ukládáním jediné instance cílové hierarchie.  

Chcete-li upgradovat distribuční bod z konzoly Configuration Manager, musí server systému lokality Configuration Manager 2007 splňovat následující podmínky:  

-   Konfigurace a umístění distribučního bodu musí být vhodné k upgradu.  

-   Počítač distribučního bodu musí mít dostatek místa na disku pro převod obsahu z formátu úložiště obsahu Configuration Manager 2007 do formátu ukládání jediné instance. Tento převod vyžaduje volné místo na disku odpovídající velikosti největšího balíčku, který je uložený na distribučním bodu.  

-   Počítače distribučního bodu musí používat verzi operačního systému, kterou podporuje distribuční bod v cílové hierarchii.  

    > [!NOTE]  
    >  Když Configuration Manager kontroluje způsobilost distribučního bodu pro upgrade, neověřuje verzi operačního systému počítače distribučního bodu.  

Chcete-li upgradovat distribuční bod, rozbalte v pracovním prostoru **Správa** položku **migrace**, rozbalte uzel **zdrojová hierarchie** a poté vyberte lokalitu, která má distribuční bod, který chcete upgradovat. Dále na kartě **Sdílené distribuční body** v podokně podrobností vyberte distribuční bod, který chcete upgradovat.  

Můžete potvrdit, že je distribuční bod připravený k upgradu, zobrazením stavu ve sloupci **Vhodné k opětovnému přiřazení** .  Pak na pásu karet konzoly Configuration Manager na kartě **distribuční body** ve skupině **distribuční bod** vyberte **znovu přiřadit**. Tím se otevře Průvodce, který použijete k dokončení upgradu distribučního bodu.  

Po upgradování distribučního bodu musíte přiřadit distribuční bod primární nebo sekundární lokalitě dle vlastního výběru v cílové hierarchii. Po upgradu distribučního bodu spravujte distribuční bod jako distribuční bod v cílové hierarchii, stejně jako jakýkoli jiný distribuční bod.  

Průběh upgradu distribučního bodu můžete sledovat v konzole Configuration Manager, a to tak, že v uzlu **migrace** v pracovním prostoru **Správa** vyberete uzel **migrace distribučního bodu** . Rovněž můžete zobrazit informace v souboru **Migmctrl.log** na serveru lokality centrální správy cílové hierarchie, nebo v souboru **distmgr.log** na serveru lokality v cílové hierarchii, který spravuje upgradovaný distribuční bod.  

> [!NOTE]  
>  Když upgradujete distribuční bod do cílové hierarchie, role systému lokality distribučního bodu se odebere ze zdrojové lokality Configuration Manager 2007. Balíčky, které byly odeslány do distribučního bodu, však nejsou aktualizovány v hierarchii Configuration Manager 2007. V konzole Configuration Manager 2007 budou balíčky, které byly odeslány do distribučního bodu, dál zobrazovat počítač systému lokality jako distribuční bod s **neznámým** **typem** . Následné aktualizace balíčku v Configuration Manager 2007 vedou v případě, že se lokalita pokusí aktualizovat balíček na neznámém systému lokality, v případě, že dojde k chybám při vytváření sestav v nástroji Distmgr. log pro daný web.  

Pokud se rozhodnete, že nechcete upgradovat sdílený distribuční bod, můžete i nadále instalovat distribuční bod z cílové hierarchie na dřívější Configuration Manager 2007 distribuční bod. Před instalací nového distribučního bodu musíte nejprve z počítače distribučního bodu odinstalovat všechny role systému lokality Configuration Manager 2007. To zahrnuje lokalitu Configuration Manager 2007, pokud se jedná o počítač serveru lokality. Pokud odinstalujete distribuční bod Configuration Manager 2007, obsah, který byl nasazen do distribučního bodu, není z počítače odstraněn.  

###  <a name="plan-to-upgrade-configuration-manager-2007-secondary-sites"></a><a name="BKMK_UpgradeSS"></a>Plánování upgradu sekundárních lokalit Configuration Manager 2007  
 Když použijete migraci k upgradu sdíleného distribučního bodu, který je hostovaný na serveru sekundární lokality Configuration Manager 2007, Configuration Manager upgraduje roli systému lokality distribučního bodu tak, aby byl distribučním bodem v cílové hierarchii. Rovněž odinstaluje sekundární lokalitu ze zdrojové hierarchie. Výsledkem je Configuration Manager aktuální distribuční bod větve, ale ne sekundární lokalita.  

 Aby byl distribuční bod na počítači serveru lokality způsobilý k upgradu, Configuration Manager musí být schopný odinstalovat sekundární lokalitu a všechny role systému lokality v tomto počítači. Sdílený distribuční bod na sdílené složce serveru Configuration Manager 2007 je obvykle způsobilý k upgradu. Pokud však sdílená složka serveru existuje na sekundárním serveru lokality, nejsou sekundární lokalita a žádné distribuční body na tomto počítači k upgradu vhodné. Důvodem je to, že sdílená složka serveru je považována za další objekt systému lokality, když se proces pokusí odinstalovat sekundární lokalitu, a tento proces nemůže tento objekt odinstalovat. V tomto scénáři můžete povolit standardní distribuční bod na sekundárním serveru lokality a poté opětovně distribuovat obsah tohoto standardního distribučního bodu. Tento proces nepoužívá šířku pásma sítě a po dokončení můžete distribuční bod na sdílené složce serveru odinstalovat, odebrat sdílenou složku serveru a následně upgradovat distribuční bod a sekundární lokalitu.  

 Před upgradem sdíleného distribučního bodu Zkontrolujte konfiguraci distribučního bodu v Configuration Manager 2007, aby nedošlo k upgradu distribučního bodu v sekundární lokalitě, kterou stále chcete používat s Configuration Manager 2007. To je dobrý postup, protože po upgradu sdíleného distribučního bodu, který je na sekundárním serveru lokality, je server systému lokality odebrán z hierarchie Configuration Manager 2007 a již není k dispozici pro použití s touto hierarchií. Když je sekundární lokalita odebrána, všechny zbývající distribuční body této sekundární lokality osiří. To znamená, že se stane nespravovanými z Configuration Manager 2007 a již nejsou sdíleny nebo nejsou vhodné k upgradu.  

> [!WARNING]  
>  Při prohlížení sdílených distribučních bodů v konzole Configuration Manager neexistuje žádné viditelné označení sdíleného distribučního bodu na vzdáleném serveru systému lokality nebo na serveru sekundární lokality.  

 Pokud máte sekundární lokalitu ve vzdálené lokalitě sítě, která se používá primárně k řízení nasazení obsahu do tohoto vzdáleného umístění, zvažte upgrade sekundárních lokalit, které mají sdílený distribuční bod. Vzhledem k tomu, že můžete nastavit řízení šířky pásma při distribuci obsahu do Configuration Manager distribučního bodu aktuální větve, můžete často upgradovat sekundární lokalitu na distribuční bod, nastavit distribuční bod pro řízení šířky pásma a vyhnout se instalaci sekundární lokality v umístění v síti v cílové hierarchii.  

 Proces upgradu sdíleného distribučního bodu na sekundárním serveru lokality je stejný jako jakýkoli jiný upgrade sdíleného distribučního bodu. Obsah je zkopírován a převeden na ukládání jediné instance používané cílovou hierarchií. Když však upgradujete sdílený distribuční bod, který je na sekundárním serveru lokality, proces upgradu také odinstaluje bod správy (pokud existuje) a pak odinstaluje sekundární lokalitu ze serveru. Výsledkem je, že je sekundární lokalita odebrána z hierarchie Configuration Manager 2007. Chcete-li odinstalovat sekundární lokalitu, Configuration Manager používá účet, který je nastaven pro shromažďování dat ze zdrojové lokality.  

 Během upgradu dochází ke zpoždění mezi tím, kdy je odinstalována sekundární lokalita Configuration Manager 2007 a když je zahájena instalace distribučního bodu v cílové hierarchii. Cyklus shromažďování dat určuje toto zpoždění až na čtyři hodiny. Zpoždění má poskytnout čas pro odinstalaci sekundární lokality před zahájením instalace nového distribučního bodu.  

 Další informace o upgradu sdíleného distribučního bodu najdete v tématu [plánování upgradu Configuration Manager 2007 sdílených distribučních bodů](#Planning_to_Upgrade_DPs).  

##  <a name="plan-to-reassign-configuration-manager-distribution-points"></a><a name="BKMK_ReassignDistPoint"></a>Plánování opětovného přiřazení distribučních bodů Configuration Manager  
 Když migrujete z podporované verze nástroje System Center 2012 Configuration Manager do hierarchie stejné verze, můžete znovu přiřadit sdílený distribuční bod ze zdrojové hierarchie do lokality v cílové hierarchii. To je třeba v konceptu upgradu distribučního bodu Configuration Manager 2007, který se stane distribučním bodem v cílové hierarchii. Distribuční body můžete znovu přiřadit z primárních a sekundárních lokalit. Akce opětovného přiřazení distribučního bodu odebere distribuční bod ze zdrojové hierarchie a nastaví počítač a jeho distribuční bod jako server systému lokality lokality, kterou vyberete v cílové hierarchii.  

 Při opětovném přiřazení distribučního bodu nemusíte znovu distribuovat migrovaný obsah, který byl hostován na zdrojovém distribučním bodu lokality. Kromě toho, na rozdíl od upgradu distribučního bodu Configuration Manager 2007, změna přiřazení distribučního bodu nevyžaduje další místo na disku v počítači distribučního bodu. Důvodem je to, že od verze System Center 2012 Configuration Manager distribuční body pro obsah použít formát ukládání jediné instance. Obsah v počítači distribučního bodu není třeba převádět, když je distribuční bod znovu přiřazen mezi hierarchiemi.  

 Aby byl distribuční bod nástroje System Center 2012 Configuration Manager způsobilý k opětovnému přiřazení, musí splňovat následující kritéria:  

-   Sdílený distribuční bodu musí být nainstalován na počítači, který není serverem lokality.  

-   Sdílený distribuční bodu nemůže být umístěn společně s dalšími rolemi systému lokality.  

Chcete-li identifikovat distribuční body, které mají nárok na změnu přiřazení v konzole Configuration Manager v uzlu **zdrojová hierarchie** , vyberte zdrojovou lokalitu a pak vyberte kartu **sdílené distribuční body** . způsobilých distribučních bodů se zobrazí **Ano** ve sloupci **způsobilo změnu přiřazení** (u tohoto sloupce je určen **nárok na upgrade** před verzí System Center 2012 R2 Configuration Manager).  

###  <a name="distribution-point-reassignment-process"></a><a name="BKMK_ReassignProcess"></a> Proces opětovného přiřazení distribučního bodu  
 K opětovnému přiřazení distribučních bodů, které jste sdíleli z aktivní zdrojové hierarchie, můžete použít konzolu Configuration Manager. Při opětovném přiřazení sdíleného distribučního bodu je distribuční bod odinstalován ze zdrojové lokality a poté je nainstalován jako distribuční bod, který je připojen k primární nebo sekundární lokalitě, kterou zadáte v cílové hierarchii.  

 K opětovnému přiřazení distribučního bodu používá cílová hierarchie účet pro přístup ke zdrojové lokalitě, který je nastaven na shromažďování dat od poskytovatele serveru SMS zdrojové lokality. Informace o požadovaných oprávněních a dalších požadavcích najdete v tématu [předpoklady pro migraci](../../core/migration/prerequisites-for-migration.md).  

## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Migrovat více sdílených distribučních bodů současně
Počínaje verzí 1610 můžete použít možnost **změnit přiřazení distribučního bodu** , aby Configuration Manager proces souběžně se změnou přiřazení až 50 sdílených distribučních bodů současně. To zahrnuje sdílené distribuční body z podporovaných zdrojových lokalit, na kterých běží:  
- Configuration Manager 2007
- System Center 2012 Configuration Manager
- System Center 2012 R2 Configuration Manager
- Configuration Manager (aktuální větev)

Při opětovném přiřazení distribučních bodů musí být každý distribuční bod oprávněn buď aktualizovat, nebo znovu přiřadit. Název akce a procesu (upgrade nebo změna přiřazení) závisí na verzi Configuration Manager, kterou zdrojová lokalita používá. Konečné výsledky obou akcí jsou stejné: distribuční bod je přiřazen k jednomu z vašich Current Branch webů s jeho obsahem.

Před verzí 1610 by Configuration Manager mohl zpracovat pouze jeden distribuční bod v jednom okamžiku. Nyní můžete přiřadit libovolný počet distribučních bodů s následujícími omezeními:  
- I když nemůžete vybrat distribuční body, které se mají znovu přiřadit, při zařazení do fronty více než jedné se Configuration Manager zpracuje paralelně namísto čekání na dokončení dalšího.  
- Ve výchozím nastavení jsou souběžně zpracovávány až 50 distribučních bodů. Po opětovném přiřazení prvního distribučního bodu bude Configuration Manager začít zpracovávat 51st a tak dále.  
- Když použijete sadu Configuration Manager SDK, můžete změnit **SharedDPImportThreadLimit** a upravit tak počet přiřazených distribučních bodů, které Configuration Manager může zpracovávat paralelně.


##  <a name="assign-content-ownership-when-migrating-content"></a><a name="About_Migrating_Content"></a>Přiřazení vlastnictví obsahu při migrování obsahu  
 Při migraci obsahu pro nasazení je nutné objekt obsahu přiřadit k lokalitě v cílové hierarchii. Tato lokalita se pak stává vlastníkem tohoto obsahu v cílové hierarchii. Přestože je lokalita nejvyšší úrovně ve vaší cílové hierarchii lokalitou, která migruje metadata pro obsah, jedná se o přiřazenou lokalitu, která používá původní zdrojové soubory pro obsah v síti.  

 V rámci minimalizace šířky pásma sítě, které je využíváno k migraci obsahu, zvažte přenos vlastnictví obsahu na lokalitu v cílové hierarchii, která je v síti v blízkosti umístění obsahu ve zdrojové hierarchii. Jelikož jsou informace o obsahu v cílové hierarchii globálně sdíleny, budou k dispozici v každé lokalitě.  

 Přestože jsou informace o obsahu sdíleny se všemi lokalitami pomocí replikace databáze, veškerý obsah, který přiřadíte k primární lokalitě a následně nasadíte do distribučních bodů v ostatních primárních lokalitách, se přenáší pomocí replikace na základě souborů. Tento přenos je směrován přes lokalitu centrální správy a následně na další primární lokalitu. Přenos dat mezi sítěmi s malou šířkou pásma můžete snížit tím, že sbalíte balíčky, které plánujete distribuovat do několika primárních lokalit před nebo během migrace, když přiřadíte lokalitu jako vlastníka obsahu.
