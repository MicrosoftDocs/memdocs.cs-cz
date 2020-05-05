---
title: Ukládání a zpracovávání údajů v Intune
titleSuffix: Microsoft Intune
description: Přečtěte si informace o ukládání a zpracovávání osobních údajů v Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: edb07842-6a16-482e-8c1d-541a29e169a8
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9bb40b21d9a257586bbd38d24b2e9b6b0a9f8ce3
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079531"
---
# <a name="data-storage-and-processing-in-intune"></a>Ukládání a zpracovávání údajů v Intune

Jakmile Intune [shromáždí údaje](privacy-data-collect.md), následuje jejich uložení a zpracování popsané níže.

## <a name="storing-personal-data"></a>Ukládání osobních údajů

Veškeré shromážděné údaje, které nepatří mezi telemetrická data, se zpracovávají prostřednictvím služby Intune a ukládají nejméně v jednom z následujících umístění: 

- SQLAzure 
- Spolehlivé kolekce (Service Fabric)  
- Úložiště Azure 

Telemetrie (protokoly služeb, protokoly výkonu, chyby atd.), které jsou klíčem k monitorování a poskytování stabilní služby se odesílají do úložišť dat telemetrie Microsoftu.

### <a name="storage-locations"></a>Umístění úložišť

Microsoft nabízí a provozuje služby Intune v mnoha oblastech po celém světe. Intune respektuje volbu umístění úložiště pro zákaznická data provedenou správcem.

Další informace najdete v tématu [kde se nacházejí vaše data?](https://www.microsoft.com/trust-center/privacy/data-location)

### <a name="personal-data-retention"></a>Uchovávání osobních údajů

Obecně platí, že Intune uchovává osobní údaje až po dobu 30 dnů od odebrání uživatele ze správy Intune.

Data telemetrie shromážděná jako součást využití Intune se uchovávají po dobu maximálně 30 dnů.

Protokoly auditů se uchovávají až jeden rok.

## <a name="processing-personal-data"></a>Zpracovávání osobních údajů

Intune zpracovává osobní údaje pomocí systémů s certifikací ISO. Další informace najdete na portálu [Service Trust Portal](https://www.microsoft.com/en-us/TrustCenter/stp).

### <a name="profiling-and-marketing"></a>Profilace a marketing

Žádné osobní údaje shromážděné v rámci poskytování služeb nejsou službou Microsoft Intune využívány k profilování ani marketingovým účelům. 

### <a name="restrict-processing-of-personal-data"></a>Omezení zpracování osobních údajů

Chcete-li omezit zpracování osobních údajů uživatele, můžete účet uživatele odstranit pomocí:
1. Export elektronické kopie osobních údajů uživatele, jejíž součástí jsou také:
    - accounts
    - Data služby
    - přidružených protokolů.
2. Odstraňuje se účet uživatele a přidružená data z Intune.

## <a name="next-steps"></a>Další kroky

Přečtěte si další informace o tom, jak služba Intune [zabezpečuje a sdílí](privacy-data-secure-share.md) osobní údaje. 
