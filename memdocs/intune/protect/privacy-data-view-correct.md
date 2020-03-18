---
title: Zobrazení a oprava osobních údajů
titleSuffix: Microsoft Intune
description: Přečtěte si, jak zobrazit a opravit osobní údaje.
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
ms.assetid: 1ba77bc7-505e-4eca-a49e-dcdaa75d0043
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6c2bacea3e1e87e6bd1a14c14b22bd6f4c2870fd
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325307"
---
# <a name="view-and-correct-personal-data"></a>Zobrazení a oprava osobních údajů

Správci Intune mohou na základě svých přístupových oprávnění zobrazit některé osobní údaje, ale osobní údaje vlastního zařízení mohou změnit jen sami koncoví uživatelé.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]


## <a name="view-personal-data"></a>Zobrazení osobních údajů

Správcům se osobní údaje koncových uživatelů zobrazují na různých listech uživatelského rozhraní služby Intune. V článcích níže se dozvíte, k jakým informacím správci mají, nebo naopak nemají přístup:
- Článek [Zobrazení podrobností o zařízení v Intune](../remote-actions/device-inventory.md) vysvětluje, jak zobrazit podrobnosti o zařízení koncového uživatele.
- Článek [Monitorování informací a přiřazení aplikace](../apps/apps-monitor.md) vysvětluje, jak zobrazit podrobnosti o aplikacích nainstalovaných na zařízení koncového uživatele.
- Článek [Jaké informace moje společnost uvidí, když si zaregistruji zařízení](https://docs.microsoft.com/user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune) obsahuje seznam údajů, které společnost koncového uživatele vidí nebo nevidí. Nejvhodnější je srozumitelně sdělit uživatelům, jaká data shromažďujete a proč to děláte. Prvním krokem vstříc transparentnosti může být právě tento článek.

### <a name="who-can-view-the-data"></a>Kdo může zobrazit údaje?

Microsoft využívá k určení přístupu k údajům zákazníků přísné kontrolní mechanismy, v rámci kterých se uděluje nejnižší přístupová úroveň nutná k provedení klíčových úloh, a jakmile už není přístup potřeba, odvolá se. 

Přístup k osobním údajům koncových uživatelů můžete zabezpečit a řídit pomocí řízení přístupu na základě role. Podrobnosti najdete v článku [Řízení přístupu na základě role v Microsoft Intune](../fundamentals/role-based-access-control.md).

Další informace o tom, jak Microsoft pracuje s údaji, jsou k dispozici v Podmínkách služeb Microsoft Online Services a v [Prohlášení o zásadách ochrany osobních údajů služeb Microsoft Online Services](https://go.microsoft.com/fwlink/p/?linkid=131004&clcid=0x409). 

## <a name="correct-end-user-personal-data"></a>Oprava osobních údajů koncových uživatelů

Správci nemohou aktualizovat informace specifické pro konkrétní zařízení nebo aplikaci. Pokud si koncový uživatel přeje opravit jakékoli osobní údaje (například název zařízení), musí to provést přímo na svém zařízení. Změny se synchronizují při příštím připojení ke službě Intune.


## <a name="next-steps"></a>Další kroky

Přečtete si, jak [auditovat, exportovat nebo odstranit](privacy-data-audit-export-delete.md) osobní data evidovaná v Intune.
