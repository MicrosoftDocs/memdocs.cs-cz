---
title: Zabezpečení a sdílení údajů v Intune
titleSuffix: Microsoft Intune
description: Přečtěte si informace o zabezpečení a sdílení osobních údajů v Intune.
keywords: Ochrana osobních údajů, data
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 68921fd6-5f50-456c-a3af-83d7bc4b134b
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 34e99a53165afdccd5ee9a2f3f190c78f673a507
ms.sourcegitcommit: 15450a1e92d9f67f74ae619ffe192c15948107c5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2020
ms.locfileid: "89516252"
---
# <a name="data-security-and-sharing-in-intune"></a>Zabezpečení a sdílení údajů v Intune


## <a name="data-security"></a>Zabezpečení dat

Microsoft Intune je klíčovou komponentou nabídky cloudových služeb Microsoft Enterprise Mobility + Security. V rámci podpory [strategie datového dozoru](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx) jsou všechny cloudové služby Microsoftu vyvíjeny v souladu s metodologiemi [Ochrana osobních údajů společnosti Microsoft](https://www.microsoft.com/en-us/trustcenter/privacy) a [Zabezpečení Microsoft](https://www.microsoft.com/en-us/trustcenter/security/).  

Microsoft Intune se řídí stejnými technickými a organizačními opatřeními, jako využívají servisní týmy Microsoft Azure k zabezpečení proti úniku dat.

Další informace najdete na portálu [Service Trust Portal](https://www.microsoft.com/en-us/TrustCenter/stp).

### <a name="data-breach-reporting"></a>Ohlašování úniků dat

Při zjištění bezpečnostního incidentu ohlašovaného zákazníkům (CRSI) se zákazníkům zasílá oznámení. Tento proces zahrnuje práci s Microsoft 365 týmem ke sdělení oznámení o porušení pro všechny Microsoft 365 zákazníky pomocí Intune.

## <a name="data-sharing"></a>Sdílení údajů

Když správci tenantů povolí některou z funkcí (například Program registrace zařízení Apple), získá Microsoft Intune souhlas správce se sdílením dat s příslušnými třetími stranami. V takovém případě může Intune sdílet osobní údaje s těmito subjekty:

- Třetí strany fungují jako zástupci Microsoftu.
- Třetí strany nefungují jako zástupci Microsoftu, ale jenom když oprávnění k tomu udělí správci tenanta explicitně.

Všechny třetí strany fungující jako Microsoft agenti jsou součástí [seznamu subdodavatelů služeb Online Services](https://aka.ms/Online_Serv_Subcontractor_List).

Účelem sdílení dat s těmito entitami je pomáhat zákaznické a technické podpoře, údržbě služeb a dalším operacím.

Smlouva tenanta s třetí stranou řídí osobní údaje Intune držené v rámci služby třetí strany. Kromě toho uděluje službě Intune oprávnění k přenosu dat do služby třetí strany.  

Informace o datech sdílených s některými třetími stranami najdete v následujících článcích:
- [Data z Intune odesílaná Applu](data-intune-sends-to-apple.md)
- [Data z Intune odesílaná Googlu](data-intune-sends-to-google.md)
- [Data odesílaná Applem do Intune](data-apple-sends-to-intune.md)
- [Data odesílaná Googlem do Intune](data-google-sends-to-intune.md)
- [Data, která Jamf Pro odesílaná do Intune](data-jamf-sends-to-intune.md)

### <a name="microsoft-endpoint-configuration-manager-data-sharing"></a>Sdílení dat v Microsoft Endpoint Configuration Manager

Microsoft Intune nesdílí žádná data s Configuration Manager. Configuration Manager je místní produkt nasazený, spravovaný a provozovaný přímo zákazníkem. Diagnostická data a data o využití shromažďovaná Configuration Managerem se využívají pouze ke zlepšení instalace produktu, kvality a zabezpečení budoucích verzí.

Další informace najdete v tématu [Diagnostika a data o využití pro Configuration Manager](/configmgr/core/plan-design/diagnostics/diagnostics-and-usage-data). 


## <a name="next-steps"></a>Další kroky

Přečtěte si, jak v Intune [zobrazit a opravit](privacy-data-view-correct.md) osobní údaje.
