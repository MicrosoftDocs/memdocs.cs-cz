---
title: Replikace na základě souborů
titleSuffix: Configuration Manager
description: Přečtěte si, jak Configuration Manager používá replikaci na základě souborů k přenosu dat mezi lokalitami v hierarchii.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 65fcc1a8-214e-4dd9-8093-de4cd4a00442
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b7d7f1564057a7a942fc4a32064eb54cdbfa890d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720167"
---
# <a name="file-based-replication"></a>Replikace na základě souborů

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager používá replikaci na základě souborů k přenosu dat založených na souborech mezi lokalitami v hierarchii. Tato data zahrnují aplikace a balíčky, které chcete nasadit do distribučních bodů v podřízených lokalitách. Zpracovává také nezpracované záznamy dat zjišťování, které lokalita přenáší do své nadřazené lokality a následně zpracuje.  

Komunikace na základě souborů mezi lokalitami používá protokol SMB ( *Server Message Block* ) na portu TCP/IP 445. Chcete-li řídit objem dat přenášených lokalitami přes síť, zadejte omezení šířky pásma a režim impulsů. Pomocí plánů můžete řídit, kdy se mají data v síti odesílat.  

## <a name="routes"></a><a name="bkmk_routes"></a>Tras

Následující informace vám pomůžou nastavit a používat postupy replikace souborů.  

### <a name="file-replication-route"></a>Postup replikace souborů

Každý postup replikace souborů identifikuje cílovou lokalitu, do které lokalita přenáší data založená na souborech. Každá lokalita podporuje jeden postup replikace souborů do určité cílové lokality.  

Pokud chcete spravovat postup replikace souborů, přečtěte si pracovní prostor **Správa** . Rozbalte uzel **Konfigurace hierarchie** a pak vyberte **replikace souborů**.  

Pro postupy replikace souborů můžete změnit následující nastavení:  

#### <a name="file-replication-account"></a>Účet replikace souborů

Tento účet se připojí k cílové lokalitě a zapisuje data do **SMS_Site** sdílené složky tohoto webu. Přijímající lokalita zpracovává data zapsaná do této sdílené složky. Ve výchozím nastavení, když přidáte lokalitu do hierarchie nástroje, Configuration Manager přiřadí účet počítače serveru nové lokality jako svůj účet replikace souborů. Pak tento účet přidá do `SMS_SiteToSiteConnection_<sitecode>` skupiny cílové lokality. Tato skupina je místní k počítači, který uděluje přístup ke sdílené složce SMS_Site. Tento účet jde změnit na uživatelský účet Windows. Pokud účet změníte, ujistěte se, že jste přidali nový účet do `SMS_SiteToSiteConnection_<sitecode>` skupiny cílové lokality.  

> [!NOTE]  
> Sekundární lokality vždycky používají účet počítače serveru sekundární lokality jako **účet replikace souborů**.  

#### <a name="schedule"></a>Plán

Nastavte plán pro každý postup replikace souborů. Tato akce omezí typ dat a čas, kdy se můžou data přenést do cílové lokality.  

#### <a name="rate-limits"></a>Omezení rychlosti

Zadejte pro každý postup replikace souborů omezení přenosové rychlosti. Tato akce řídí šířku pásma sítě, kterou lokalita používá, když přenáší data do cílové lokality:  

- **Pulse – režim**: zadejte velikost datových bloků, které lokalita odesílá do cílové lokality. Můžete také určit prodlevu mezi odesíláním jednotlivých bloků dat. Tuto možnost použijte, pokud musíte odesílat data přes síťové připojení s malou šířkou pásma do cílové lokality.

    Například máte omezení pro posílání 1 KB dat každých pět sekund, ale ne 1 KB každé tři sekundy. Toto omezení je bez ohledu na rychlost propojení nebo jeho využití v daném okamžiku.

- **Omezeno na maximální přenosové rychlosti za hodinu**: lokalita odesílá data do cílové lokality pouze pomocí zadaného procenta času. Configuration Manager neidentifikuje dostupnou šířku pásma sítě. Rozdělí čas, který může odesílat data do řezů času. Pak data pošle v krátkém časovém úseku, po kterém následují časové úseky, kdy data neodesílají.

    Například můžete nastavit maximální rychlost na **50%**. Configuration Manager přenáší data po určitou dobu následovanou stejným časovým obdobím, kdy neodesílají data. Nespravuje skutečnou velikost datového bloku, který odesílá. Lokalita spravuje pouze dobu, během které odesílá data.  

    > [!CAUTION]  
    > Ve výchozím nastavení může lokalita k přenosu dat do cílové lokality použít až tři **souběžná odesílání** . Když u postupu replikace souborů povolíte omezení přenosové rychlosti, omezí se **Souběžná odesílání** na tuto lokalitu na jednu. Toto chování platí i v případě, že je **Maximální dostupná šířka pásma (%)** nastavená na **100%**. Pokud například použijete výchozí nastavení pro odesílatele, omezí se tím přenosová rychlost do cílové lokality na jednu třetinu výchozí kapacity.  

#### <a name="routes-between-secondary-sites"></a>Trasy mezi sekundárními lokalitami

Nakonfigurujte postup replikace souborů mezi dvěma sekundárními lokalitami pro směrování obsahu založeného na souborech mezi těmito lokalitami.  


### <a name="sender"></a>Odesílatel

Každá lokalita má jednoho odesílatele. Odesílatel spravuje síťové připojení z jedné lokality do cílové lokality. Může vytvořit připojení k několika lokalitám současně. Odesílatel používá pro připojení k lokalitě postup replikace souborů do lokality a identifikuje účet, který používá k vytvoření síťového připojení. Odesílatel používá tento účet také k zápisu dat do SMS_Site sdílené složky cílové lokality.  

Ve výchozím nastavení odesílatel zapisuje data do cílové lokality pomocí několika **souběžných odesílání**nebo *vlákna*. Každé vlákno může přenést jiný objekt založený na souborech do cílové lokality. Když odesilatel začne odeslat objekt, pokračuje v zápisu bloků dat pro daný objekt, dokud neodešle celý objekt. Po odeslání všech dat objektu se může nový objekt zahájit odeslání tohoto vlákna.  

Chcete-li spravovat odesílatele webu, klikněte na pracovní prostor **Správa** a rozbalte uzel **Konfigurace lokality** . Vyberte uzel **lokality** a pak vyberte **vlastnosti** pro lokalitu, kterou chcete spravovat. Chcete-li změnit nastavení odesílatele, přepněte na kartu **Odesílatel** .  

Pro odesílatele můžete změnit následující nastavení:  

#### <a name="maximum-concurrent-sendings"></a>Maximální počet současných odesílání

Ve výchozím nastavení používá každá lokalita pět současných odeslání (vlákna). Tři vlákna jsou k dispozici pro použití při odesílání dat do libovolné cílové lokality. Pokud tento počet zvýšíte, můžete zvýšit propustnost dat mezi lokalitami. Více vláken znamená, že Configuration Manager může přenášet více souborů současně. Zvýšením tohoto počtu se taky zvýší poptávka po šířce pásma sítě mezi lokalitami.  

#### <a name="retry-settings"></a>Nastavení opakování

Ve výchozím nastavení každá lokalita opakuje připojení k problému dvakrát, přičemž mezi pokusy o připojení uplyne prodleva s jednou minutou. Můžete upravit počet pokusů o připojení, které lokalita provede, a dobu čekání mezi pokusy.  


## <a name="next-steps"></a>Další kroky

[Replikace databáze](database-replication.md)
