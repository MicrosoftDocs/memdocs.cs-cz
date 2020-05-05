---
title: Zahájení kampaně k migraci do Intune
titleSuffix: Microsoft Intune
description: Tento článek obsahuje pokyny, jak spustit kampaň migrace do Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f781b029-50f2-46ee-8ff7-03b4a6719e80
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9a15bc7c1fd74aa3741a9bd699778795cbf3faab
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82080024"
---
# <a name="phase-2-migration-campaign"></a>Fáze 2: Kampaň migrace

Zvolte takový postup migrace, který bude nejvíc vyhovovat potřebám organizace, a přizpůsobte taktiku implementace vlastním požadavkům. Zbývající část tohoto průvodce vás seznámí s nástroji, které potřebujete k dosažení cíle získání uživatelských zařízení zaregistrovaných do Intune.

## <a name="keys-to-a-successful-migration"></a>Klíč k úspěšné migraci

Klíčové předpoklady pro úspěšnou migraci od jiného poskytovatele MDM do Intune:

- Výpadky koncových uživatelů a jejich nespokojenost může minimalizovat srozumitelná a užitečná komunikace.

- Poskytněte uživatelům konkrétní pokyny k migraci.

- Před registrací do Intune musí být zrušena registrace všech spravovaných zařízení u vašeho stávajícího poskytovatele MDM.

- Předejte koncovým uživatelům pokyny týkající se zrušení registrace zařízení od vašeho stávajícího poskytovatele MDM.

- Proveďte migraci v několika fázích. Začněte s malou, zkušební skupinou uživatelů a postupně přidávejte další skupiny uživatelů, dokud nedosáhnete nasazení v plném rozsahu.

- Monitorujte vytíženost technické podpory a úspěšnost registrace v jednotlivých cyklech. Ponechte si časovou rezervu, abyste mohli vyhodnotit kritéria úspěšnosti migrace každé skupiny, než přejdete k migraci další skupiny. Při pilotním nasazení byste měli zhodnotit následující:

  - Míra úspěchu a selhání registrací je v rámci očekávání.

  - Produktivita uživatelů:

    - Firemní prostředky, například sítě VPN a Wi-Fi, e-mail a certifikáty, jsou funkční.

    - Uživatelé mají přístup ke zřízeným aplikacím.

  - Zabezpečení dat:

    - Generují se sestavy dodržování předpisů.

    - Vynucuje se ochrana mobilních aplikací.

Pokud jste spokojení s první fází migrace, zopakujte daný [cyklus migrace](migration-guide-cycle.md) v další fázi.

- Opakujte cykly migrace, dokud nebudou všichni uživatelé migrovaní do Intune.

- Zajistěte připravenost týmu technické podpory pomoct během kampaně migrace koncovým uživatelům. Spusťte dobrovolnou migraci, abyste byli schopni odhadnout zátěž telefonních linek technické podpory.

- Nevytvářejte konečné termíny pro registraci, dokud si pracovník helpdesku nedokáže zpracovat zbývající populace.

> [!IMPORTANT]
> Vyhněte se tomu, abyste konfigurovali použití ovládacích prvků přístupu k prostředkům, jako je Exchange nebo SharePoint Online, současně pro Intune i vaše stávající řešení MDM. Kromě toho by měla být zařízení registrována vždy jen v jednom řešení.

## <a name="next-steps"></a>Další kroky

Vytvořte svůj [plán komunikace](migration-guide-communication-plan.md).
