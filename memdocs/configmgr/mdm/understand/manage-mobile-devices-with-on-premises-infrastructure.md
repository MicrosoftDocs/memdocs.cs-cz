---
title: Místní správa MDM
titleSuffix: Configuration Manager
description: Přečtěte si o místní správě mobilních zařízení (MDM) v Configuration Manager
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 38d68447093d098f1a8157a2e18e19a6c4f88364
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721833"
---
# <a name="on-premises-mdm-in-configuration-manager"></a>Místní MDM v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager místní správy mobilních zařízení (MDM) je řešení pro správu zařízení, které spoléhá na integrované funkce správy systému Windows. Tato funkce je založená na standardu DM (Open Mobile Alliance) pro správu mobilních zařízení (OMA). Pro správu a údržbu zařízení používá infrastrukturu Configuration Manager vaší organizace. Vaše organizace vyžaduje, aby tato funkce používala licence Microsoft Intune, ale nevyžaduje žádné cloudové připojení. Configuration Manager ukládá všechna data o vašich zařízeních do místní databáze lokality.

Místní MDM se liší od Microsoft Intune, což taky spoléhá na integrované funkce OMA DM. Všechny funkce správy v Intune se doručují prostřednictvím cloudových služeb. Místní MDM se také liší od řešení správy založeného na klientech, které tradičně nabízí Configuration Manager. Spoléhá se na podobnou infrastrukturu, ale nepoužívá samostatně instalovaný klientský software na zařízeních, která spravuje.  

## <a name="comparison"></a>Srovnání

V následujících částech jsou uvedeny výhody a nevýhody místní správy mobilních zařízení ve srovnání s tradiční správou na základě klientů:  

### <a name="advantages"></a>Výhody

- **Zjednodušená infrastruktura**: vyžaduje se méně rolí systému lokality.

- **Snazší údržba**: vzhledem k tomu, že funkce správy jsou integrované v operačním systému zařízení, nové verze Configuration Manager klienta se nevyžadují při zavedení nových funkcí správy do lokality.

- **Místní**: – veškerá správa a data se uchovávají místně.

### <a name="disadvantages"></a>Nevýhody

**Méně funkcí správy klientů**: bez orchestrace, měření softwaru, integrace třetích stran, pořadí úkolů nebo podpora centra softwaru.

- **Omezená podpora zařízení**: místní MDM nepodporuje jako klienta Configuration Manager tolik verzí operačního systému. Další informace najdete v tématu [podporované verze operačních systémů pro klienty a zařízení](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).

## <a name="next-step"></a>Další krok

Přečtěte si, co je potřeba vzít v úvahu při nastavování infrastruktury Configuration Manager a plánování registrace zařízení v místní MDM.

> [!div class="nextstepaction"]
> [Plánování místní správy MDM](../plan-design/plan-on-premises-mdm.md)  
