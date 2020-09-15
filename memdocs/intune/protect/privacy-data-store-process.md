---
title: Ukládání a zpracovávání údajů v Intune
titleSuffix: Microsoft Intune
description: Přečtěte si informace o ukládání a zpracovávání osobních údajů v Intune.
keywords: data, ochrana osobních údajů
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/01/2020
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
ms.openlocfilehash: 92c7c597a6d196ab5f8c3170cd5880682a280e73
ms.sourcegitcommit: e2deac196e5e79a183aaf8327b606055efcecc82
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076059"
---
# <a name="data-storage-and-processing-in-intune"></a>Ukládání a zpracovávání údajů v Intune

### <a name="storing-customer-data"></a>Ukládání zákaznických dat

Jakmile Intune [data shromáždí](privacy-data-collect.md), Intune sleduje standardní zásady zpracování dat pro Microsoft 365, které určují, jak se budou zákaznická data ukládat a zpracovávat. Podívejte [se, kde jsou uložená zákaznická data Microsoft 365](https://docs.microsoft.com/microsoft-365/enterprise/o365-data-locations). Osobní údaje jsou zpracovávány v rámci auditované hranice dodržování předpisů služby Intune v rámci opatření technického zabezpečení, která jsou zajištěna prostřednictvím [podmínek služby Microsoft Online Services (OST)](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).

### <a name="storage-locations"></a>Umístění úložišť

Microsoft nabízí a provozuje služby Intune v mnoha oblastech po celém světe. Intune respektuje volbu umístění úložiště pro zákaznická data provedenou správcem.

Další informace najdete v tématu [umístění datového centra](https://docs.microsoft.com/microsoft-365/enterprise/o365-data-locations?view=o365-worldwide#data-center-locations) .

### <a name="personal-data-retention"></a>Uchovávání osobních údajů

Microsoft 365 standardní zásady pro zpracování dat určují, jak dlouho se budou data zákazníků uchovávat po odstranění. Existují dva scénáře, ve kterých jsou odstraněna zákaznická data:

-**Aktivní odstranění**: tenant má aktivní předplatné a uživatel nebo správce odstraní data nebo správce odstraní uživatele.
-**Pasivní odstranění**: předplatné tenanta skončí.

Pro každý scénář odstranění najdete informace v tématu [uchovávání, odstraňování a zničení dat v Microsoft 365](https://docs.microsoft.com/microsoft-365/enterprise/microsoft-365-data-retention-deletion-and-destruction-overview?view=o365-worldwide).  

Obecně platí, že osobní údaje shromážděné službou Intune budou odebrány do 30 dnů po odstranění. Protokoly auditu se uchovávají až po dobu jednoho roku z hlediska zabezpečení. 


## <a name="processing-personal-data"></a>Zpracovávání osobních údajů

Intune zpracovává osobní údaje pomocí systémů s certifikací ISO. Další informace najdete na portálu [Service Trust Portal](https://www.microsoft.com/en-us/TrustCenter/stp).

### <a name="profiling-and-marketing"></a>Profilace a marketing

Žádné osobní údaje shromážděné v rámci poskytování služeb nejsou službou Microsoft Intune využívány k profilování ani marketingovým účelům. 

## <a name="next-steps"></a>Další kroky

Přečtěte si další informace o tom, jak služba Intune [zabezpečuje a sdílí](privacy-data-secure-share.md) osobní údaje. 
