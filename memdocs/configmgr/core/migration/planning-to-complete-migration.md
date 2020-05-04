---
title: Dokončení migrace
titleSuffix: Configuration Manager
description: Naučte se, jak dokončit migraci do cílové hierarchie Configuration Manager aktuální větve poté, co zdrojová hierarchie už neobsahuje data.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4854b50-2e8c-414c-a872-9579554dca98
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 76cf6b57a4bc1439f2aa9c2e0484271987f85748
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713006"
---
# <a name="plan-to-complete-migration-in-configuration-manager"></a>Plánování dokončení migrace v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pomocí Configuration Manager můžete proces migrace dokončit, pokud už zdrojová hierarchie neobsahuje data, která chcete migrovat do cílové hierarchie. Dokončení migrace zahrnuje následující obecné kroky:  

-   Ujistěte se, že jsou data, která požadujete, migrována. Před dokončením migrace ze zdrojové hierarchie se ujistěte, že jste úspěšně migrovali všechny prostředky ze zdrojové hierarchie, které požadujete v cílové hierarchii. To může zahrnovat data a klienty.  

-   Zastavení shromažďování dat ze zdrojových lokalit. Aby bylo možné dokončit migraci ze zdrojové hierarchie, je nejprve nutné zastavit shromažďování dat ze zdrojových lokalit.  

-   Vyčištění dat migrace. Až zastavíte shromažďování dat ze všech zdrojových lokalit ve zdrojové hierarchii, můžete z databáze cílové hierarchie odebrat data o procesu migrace a zdrojové hierarchii.  

-   Vyřadí z provozu zdrojovou hierarchii. Po dokončení migrace ze zdrojové hierarchie a tato hierarchie už nebude mít prostředky, které spravujete, můžete lokality ve zdrojové hierarchii vyřadit z provozu a z vašeho prostředí odebrat související infrastrukturu. Informace o tom, jak vyřadit lokality a zdrojové hierarchie z provozu, najdete v dokumentaci k této verzi Configuration Manager.  

Následující části vám pomůžou naplánovat dokončení migrace ze zdrojové hierarchie tím, že zastavují shromažďování dat a mazání dat migrace:  

-   [Plánování zastavení shromažďování dat](#Plan_to_Stop_Data_Gath)  

-   [Plánování vyčištění dat migrace](#Plan_to_clean_up)  

##  <a name="plan-to-stop-gathering-data"></a><a name="Plan_to_Stop_Data_Gath"></a>Plánování zastavení shromažďování dat  
 Před dokončením migrace a vyčištění dat migrace je nutné zastavit shromažďování dat ze všech zdrojových lokalit ve zdrojové hierarchii. Chcete-li zastavit shromažďování dat z jednotlivých zdrojových lokalit, je třeba provést příkaz **Zastavit shromažďování dat** ve zdrojových lokalitách nejnižší úrovně a potom tento postup zopakovat v každé nadřazené lokalitě. Lokalita nejvyšší úrovně ve zdrojové hierarchii musí být poslední lokalitou, u níž shromažďování dat zastavíte. Shromažďování dat je nutné zastavit u každé podřízené lokality před provedením tohoto příkazu v nadřazené lokalitě. Obvykle se shromažďování dat zastavuje jenom v případě, že jste připraveni dokončit proces migrace.  

 Po zastavení shromažďování dat ze zdrojové lokality již nebudou sdílené distribuční body z této lokality nadále k dispozici jako umístění obsahu pro klienty v cílové hierarchii. Proto zajistěte, aby veškerý migrovaný obsah, ke kterému klienti v cílové hierarchii potřebují přístup, zůstal k dispozici pomocí jedné z následujících možností:  

-   V cílové hierarchii distribuujte obsah alespoň do jednoho distribučního bodu.  

-   Než zastavíte shromažďování dat ze zdrojové lokality, upgradujte nebo přeřaďte sdílené distribuční body, které mají požadovaný obsah. Další informace o upgradu nebo změně přiřazení sdílených distribučních bodů najdete v příslušných částech v tématu [Plánování strategie migrace nasazení obsahu](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

Po zastavení shromažďování dat ze všech zdrojových lokalit ve zdrojové hierarchii můžete data migrace vyčistit. Dokud nebudete čistit data migrace, všechny úlohy migrace spuštěné nebo naplánované ke spuštění zůstanou v konzole Configuration Manager dostupné.  

Další informace o zdrojových lokalitách a shromažďování dat najdete v tématu [Plánování strategie zdrojové hierarchie](../../core/migration/planning-a-source-hierarchy-strategy.md).  

##  <a name="plan-to-clean-up-migration-data"></a><a name="Plan_to_clean_up"></a>Plánování vyčištění dat migrace  
 Posledním krokem potřebným k dokončení migrace je vyčištění dat migrace. Po zastavení shromažďování dat pro každou zdrojovou lokalitu ve zdrojové hierarchii můžete použít příkaz **vyčistit data migrace** . Tato volitelná akce odebere z databáze cílové hierarchie data o aktuální zdrojové hierarchii.  

 Když vyčistíte data migrace, většina dat o migraci se odebere z databáze cílové hierarchie. Podrobnosti o migrovaných objektech jsou ale zachované. Pomocí těchto podrobností můžete pracovní prostor **migrace** použít k překonfigurování zdrojové hierarchie s daty, která byla migrována za účelem obnovení migrace z této zdrojové hierarchie, nebo ke kontrole objektů a vlastnictví objektů, které byly dříve migrovány.  
