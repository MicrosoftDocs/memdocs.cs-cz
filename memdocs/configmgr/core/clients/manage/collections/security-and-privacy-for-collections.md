---
title: Zabezpečení a ochrana osobních údajů kolekce
titleSuffix: Configuration Manager
description: Získejte osvědčené postupy pro zabezpečení a ochranu osobních údajů v kolekcích v Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 30bf2451-5415-4be2-ba8d-21759370cd83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 42345ee91baaad7dcc82eab537fbeb697d6cd7ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714490"
---
# <a name="security-and-privacy-for-collections-in-configuration-manager"></a>Zabezpečení a ochrana osobních údajů pro kolekce v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Toto téma obsahuje osvědčené postupy zabezpečení a informace o ochraně osobních údajů pro kolekce v nástroji Configuration Manager.  

 Pro kolekce v Configuration Manager nejsou k dispozici žádné informace o ochraně osobních údajů. Kolekce jsou kontejnery pro prostředky, jako jsou uživatelé nebo zařízení. Členství v kolekci často závisí na informacích, které Configuration Manager shromažďuje během standardní operace. Například můžete pomocí informací o prostředcích shromážděných ze zjišťování nebo z inventáře nakonfigurovat kolekci, aby obsahovala zařízení, která splňují zadaná kritéria. Kolekce můžou být taky založené na informacích o aktuálním stavu pro operace správy klienta, například nasazování softwaru a kontrolu kompatibility. Kromě těchto kolekcí založených na dotazech můžou do kolekcí přidat prostředky taky administrativní uživatelé.  

 Další informace o kolekcích najdete v tématu [Úvod do kolekcí](../../../../core/clients/manage/collections/introduction-to-collections.md). Další informace o jakýchkoli osvědčených postupech zabezpečení a ochraně osobních údajů pro Configuration Manager operací, které se dají použít ke konfiguraci členství v kolekci, najdete v tématu [osvědčené postupy zabezpečení a ochrana osobních údajů pro Configuration Manager](../../../../core/plan-design/security/security-best-practices-and-privacy-information.md).  

## <a name="security-best-practices-for-collections"></a>Osvědčené postupy zabezpečení pro kolekce  
 Pro kolekce použijte následující osvědčené postupy zabezpečení.  

|Doporučené zabezpečení|Další informace|  
|----------------------------|----------------------|  
|Pokud exportujete nebo importujete kolekci pomocí souboru ve formátu MOF (Managed Object Format), který je uložený v umístění v síti, zabezpečte umístění i síťový kanál.|Omezte přístup k síťové složce neoprávněným uživatelům.<br /><br /> Pro komunikaci mezi umístěním v síti a serverem lokality použijte podepisování SMB (Server Message Block) nebo protokol IPsec (Internet Protocol security). Zabráníte tak případnému útočníkovi v manipulaci s daty exportované kolekce. Pro šifrování dat na síti používejte protokol IPsec, abyste zabránili odhalení informací.|  

### <a name="security-issues-for-collections"></a>Problémy se zabezpečením pro kolekce  
 Kolekce mají následující problémy se zabezpečením:  

-   Když používáte proměnné kolekce, mohou místní správci číst potenciálně citlivé informace.  

     Proměnné kolekce jde použít při nasazování operačního systému.  
