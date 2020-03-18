---
title: Konfigurace zásad ochrany aplikací během migrace
titleSuffix: Microsoft Intune
description: Tento článek popisuje nezbytné kroky postupu k nastavení zásad ochrany aplikací během migrace do Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 93cda587-bf56-4d41-b123-9fe203fad788
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: d033c83865c19638ab9b1d34b9b77ae146d28133
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331299"
---
# <a name="configure-app-protection-policies-optional"></a>Konfigurace zásad ochrany aplikací (volitelné)


Zásady ochrany aplikací umožňují:
* Šifrovat aplikace
* Definovat PIN kód při přístupu k aplikaci
* Blokovat spuštění aplikací na zařízeních s jailbreakem nebo rootem a použít mnoho dalších způsobů ochrany

Pokud uživatel ztratí telefon nebo je mu telefon odcizen, můžete vzdáleně vymazat firemní data, zatímco osobní data uživatele zůstanou nedotčena.

Zásady ochrany aplikací používají zabezpečení na úrovni aplikace, takže zařízení není potřeba registrovat. Dají se použít pro všechna zařízení, ať už jsou zaregistrovaná v Intune nebo ne. Můžete je použít také u zařízení zaregistrovaných u jiných poskytovatelů MDM.

## <a name="app-protection-policies-with-lob-apps"></a>Zásady ochrany obchodních aplikací

Zásady ochrany mobilních aplikací můžete také rozšíříte do obchodních aplikací (LOB) pomocí [sady Microsoft Intune App SDK](../developer/app-sdk-get-started.md) nebo nástroje pro zabalení Microsoft Intune aplikací pro platformy iOS/IPadOS a Android. Další informace najdete v článcích [Nástroj App Wrapping Tool pro iOS](../developer/app-wrapper-prepare-ios.md) a [Nástroj App Wrapping Tool pro Android](./../developer/app-wrapper-prepare-android.md). Dále se můžete podívat na článek [Příprava obchodních aplikací na ochranu aplikací](../developer/apps-prepare-mobile-application-management.md).

## <a name="how-do-app-protection-policies-help-during-migration"></a>Jak zásady ochrany aplikací pomáhají při migraci?

Při migraci je potřeba odebrat zařízení od předchozího poskytovatele MDM a ihned ho zaregistrovat do Intune. Tyto kroky je potřeba naplánovat a domluvit s koncovými uživateli, aby svá zařízení odebrali od předchozího poskytovatele MDM a ihned je zaregistrovali do Intune. Během migrace se ale někteří uživatelé můžou zpozdit s dokončením registrace, takže jejich zařízení nebude spravovat žádný poskytovatel MDM.

V tomto období může být vaše organizace vystavena většímu nebezpečí úniku firemních dat při odcizení zařízení, pokud zůstane povolený přístup k firemním prostředkům. Při zablokování přístupu k firemním prostředkům se může také snížit produktivita uživatelů.

Intune může během migrace nabídnout ochranu podnikových dat, abyste mohli i nadále mít pokrytí zabezpečení pro vaše podniková data, i když nebude žádná Správa na úrovni zařízení.

Když zapnete podmíněný přístup ve starém poskytovateli MDM, můžou uživatelé pořád produktivní, zatímco jsou zaregistrované v Intune.

## <a name="task-list-for-app-protection-policies"></a>Seznam kroků pro zásady ochrany aplikací

- [Vytvoření a přiřazení zásad ochrany aplikací](../apps/app-protection-policies.md)

## <a name="next-steps"></a>Další kroky

[Speciální aspekty migrace](migration-guide-considerations.md)
