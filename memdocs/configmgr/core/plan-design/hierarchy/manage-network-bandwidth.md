---
title: Správa šířky pásma sítě pro obsah
titleSuffix: Configuration Manager
description: Nakonfigurujte plánování, omezování a předzpracovaný obsah pro Configuration Manager.
ms.date: 02/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e80d1151-91db-4a27-8411-a957297b67d0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df3188e827623db8faa0b27be2fe282031e9fa50
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126388"
---
# <a name="manage-network-bandwidth-for-content"></a>Správa šířky pásma sítě pro obsah
Aby vám pomohla spravovat šířku pásma sítě, která se používá pro proces správy obsahu Configuration Manager, můžete použít předdefinované ovládací prvky pro plánování a omezování. Můžete také použít připravený obsah. V následujících částech najdete podrobnější popis uvedených možností.

##  <a name="scheduling-and-throttling"></a><a name="BKMK_PlanningForThrottling"></a>Plánování a omezování  

 Když vytvoříte balíček, změníte zdrojovou cestu k obsahu nebo aktualizujete obsah v distribučním bodě, soubory se zkopírují ze zdrojové cesty do knihovny obsahu na serveru lokality. Pak se obsah zkopíruje z knihovny obsahu na serveru lokality do knihovny obsahu v distribučních bodech. Když se aktualizují zdrojové soubory obsahu a zdrojové soubory už jsou distribuované, Configuration Manager načte jenom nové nebo aktualizované soubory a pak je pošle do distribučního bodu.

 Můžete použít plánování a omezování pro komunikaci mezi lokalitami a pro komunikaci mezi serverem lokality a vzdáleným distribučním bodem. Pokud je šířka pásma sítě omezená i po nastavení ovládacích prvků plánování a omezování, můžete zvážit přednastavení obsahu v distribučním bodě.  

 V Configuration Manager můžete nastavit plán a určit nastavení omezování na vzdálených distribučních bodech, které určují, kdy a jak se bude provádět distribuce obsahu. Každý vzdálený distribuční bod může mít různé konfigurace, které umožňují řešit omezení šířky pásma sítě ze serveru lokality do vzdáleného distribučního bodu. Ovládací prvky pro plánování a omezování vzdáleného distribučního bodu jsou podobné nastavením pro standardní adresu odesílatele. V takovém případě se nastavení používá v nové komponentě s názvem správce přenosu balíčků.

 Správce přenosu balíčků distribuuje obsah ze serveru lokality, jako primární nebo sekundární lokality, do distribučního bodu, který je nainstalován v systému lokality. Nastavení omezování je zadáno na kartě **omezení přenosové rychlosti** a nastavení plánování je zadáno na kartě **plán** pro distribuční bod, který není na serveru lokality. Nastavení času je založeno na časovém pásmu z odesílajícího webu, nikoli v distribučním bodě.  

> [!IMPORTANT]  
>  Karty **omezení přenosové rychlosti** a **plán** se zobrazují pouze ve vlastnostech distribučních bodů, které nejsou nainstalovány na serveru lokality.  

Další informace najdete v tématu [instalace a konfigurace distribučních bodů pro Configuration Manager](../../servers/deploy/configure/install-and-configure-distribution-points.md).  

##  <a name="prestaged-content"></a><a name="BKMK_PrestagingContent"></a>Připravený obsah  
 Před distribucí obsahu můžete připravit obsah a přidat soubory obsahu do knihovny obsahu na serveru lokality nebo v distribučním bodě. Protože soubory obsahu jsou již v knihovně obsahu, při distribuci obsahu se nepřenášejí přes síť. Soubory obsahu můžete připravit pro aplikace a balíčky.  

V konzole Configuration Manager vyberte obsah, který chcete připravit, a pak použijte **Průvodce vytvořením souboru připraveného obsahu**. Tím se vytvoří komprimovaný soubor připraveného obsahu, který obsahuje soubory a související metadata pro obsah. Pak můžete obsah ručně importovat na serveru lokality nebo v distribučním bodě. Je třeba počítat s následujícím:  

-   Když importujete soubor připraveného obsahu na server lokality, soubory obsahu se přidají do knihovny obsahu na serveru lokality a potom se zaregistrují v databázi serveru lokality.  

-   Když importujete soubor připraveného obsahu do distribučního bodu, soubory obsahu budou přidány do knihovny obsahu v distribučním bodě. Do serveru lokality se pošle stavová zpráva, která lokalitu informuje o tom, že obsah je k dispozici v distribučním bodě.  

Volitelně můžete nakonfigurovat distribuční bod jako **připravený** , aby bylo možné lépe spravovat distribuci obsahu. Při distribuci obsahu pak můžete zvolit, zda chcete:  

-   Vždy připravit obsah v distribučním bodě.  

-   Připraví počáteční obsah balíčku a pak použijte standardní proces distribuce obsahu, pokud jsou k dispozici aktualizace obsahu.  

-   Vždy používejte standardní proces distribuce obsahu pro obsah v balíčku.  

###  <a name="determine-whether-to-prestage-content"></a><a name="BKMK_DetermineToPrestageContent"></a>Určete, jestli se má připravit obsah  
 Zvažte přípravu obsahu pro aplikace a balíčky v následujících scénářích:  

-   **K vyřešení problému omezené šířky pásma sítě ze serveru lokality do distribučního bodu.** Pokud plánování a omezování nestačí pro splnění vašich obav o šířku pásma, zvažte přednastavení obsahu v distribučním bodě. Každý distribuční bod má nastavení **Povolit tento distribuční bod pro připravený obsah** , který můžete zvolit ve vlastnostech distribučního bodu. Povolíte-li tuto možnost, bude distribuční bod identifikován jako připravený distribuční bod a můžete zvolit způsob správy obsahu na základě jednotlivých balíčků.  

    Následující nastavení jsou k dispozici ve vlastnostech aplikace, balíčku, balíčku ovladačů, spouštěcí bitové kopie, instalačního programu operačního systému a obrázku. Tato nastavení umožňují zvolit způsob správy distribuce obsahu ve vzdálených distribučních bodech, které jsou označeny jako připravené:  

    -   **Automaticky stahovat obsah, když jsou balíčky přiřazeny distribučním bodům**: tuto možnost použijte, pokud máte menší balíčky a nastavení plánování a omezení poskytuje dostatečnou kontrolu pro distribuci obsahu.  

    -   **Stahovat do distribučního bodu pouze změny obsahu**: tuto možnost použijte, pokud očekáváte, že budoucí aktualizace obsahu v balíčku budou obecně menší než počáteční balíček. Můžete například připravit aplikaci, například Microsoft 365 aplikace, protože počáteční velikost balíčku je větší než 700 MB a je příliš velká pro odeslání přes síť. Aktualizace obsahu tohoto balíčku ale můžou být méně než 10 MB a je přijatelné, aby se mohly distribuovat přes síť. Dalším příkladem mohou být balíčky ovladačů, kde počáteční velikost balíčku je velká, ale přírůstkové přidávání ovladačů do balíčku může být malé.  

    -   **Ručně kopírovat obsah tohoto balíčku do distribučního bodu**: tuto možnost použijte, pokud máte velké balíčky s obsahem, jako je například operační systém, a nikdy nechcete používat síť k distribuci obsahu do distribučního bodu. Když vyberete tuto možnost, musíte připravit obsah v distribučním bodě.  

    > [!IMPORTANT]  
    >  Předchozí možnosti platí pro jednotlivé balíčky a používají se pouze v případě, že je distribuční bod identifikován jako připravený. Distribuční body, které nebyly označeny jako připravené, ignorují tato nastavení. V takovém případě je obsah vždy distribuován přes síť ze serveru lokality do distribučních bodů.  

-   **K obnovení knihovny obsahu na serveru lokality.** Pokud dojde k chybě serveru lokality, budou informace o balíčcích a aplikacích, které jsou obsaženy v knihovně obsahu, obnoveny v rámci procesu obnovení do databáze lokality, ale soubory knihovny obsahu nejsou obnoveny v rámci procesu. Pokud nemáte zálohu systému souborů k obnovení knihovny obsahu, můžete vytvořit soubor připraveného obsahu z jiné lokality, která obsahuje balíčky a aplikace, které musíte mít. Pak můžete soubor připraveného obsahu rozbalit na obnovený server lokality. Další informace o zálohování a obnovení serveru lokality najdete v tématu [zálohování a obnovení pro Configuration Manager](../../servers/manage/backup-and-recovery.md).  
