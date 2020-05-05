---
title: Resetování hesel u zařízení v Microsoft Intune – Azure | Microsoft Docs
description: Odeberte nebo resetujte heslo pomocí akce Odebrat heslo na zařízeních v Intune, která spravujete nebo monitorujete.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 47181d19-4049-4c7a-a8de-422206c4027e
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ef7a076c0a41e84e0028da6655569401f334772c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078970"
---
# <a name="reset-or-remove-a-device-passcode-in-intune"></a>Resetování nebo odebrání hesla zařízení v Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Tento dokument popisuje jak resetování hesla na úrovni zařízení, tak resetování hesla pracovního profilu v Androidu Enterprise (dříve nazývaném zařízení s Androidem for Work nebo AfW). Je důležité si uvědomit, že tento rozdíl mezi požadavky se může lišit. Při resetování hesla na úrovni zařízení se resetuje heslo celého zařízení. Resetování hesla pracovního profilu obnoví heslo pouze pro pracovní profil uživatele na zařízeních s Androidem Enterprise.

## <a name="supported-platforms-for-device-level-passcode-reset"></a>Platformy podporované při resetování hesla zařízení

| Platforma | Podporované? |
| ---- | ---- |
| Zařízení s Androidem verze 6.x nebo starší | Ano |
| Zařízení s Androidem Enterprise zaregistrovaná jako vlastník zařízení | Ano |
| zařízení s iOS/iPadOS | Ano |
| zařízení se systémem iOS/iPadOS zaregistrovaná pomocí zápisu uživatelů | Ne |
| Zařízení s Androidem zaregistrovaná s pracovním profilem | Ne |
| Zařízení s Androidem, verze 7.0 nebo novější | Ne |
| macOS | Ne |
| Windows | Ne |

U zařízení s Androidem to znamená, že obnovení hesla na úrovni zařízení se podporuje jenom na zařízeních s 6. x nebo starším nebo na zařízeních s Androidem Enterprise spuštěnou v celoobrazovkovém režimu. Je to proto, že společnost Google odebrala podporu pro resetování hesla a hesla zařízení s Androidem 7 v rámci aplikace s oprávněním správce zařízení a platí pro všechny dodavatele MDM.

## <a name="supported-platforms-for-android-enterprise-work-profile-passcode-reset"></a>Platformy podporované při resetování hesla pracovního profilu Androidu Enterprise

| Platforma | Podporované? |
| ---- | ---- |
| Zařízení s Androidem Enterprise zaregistrovaná s pracovním profilem a se spuštěnou verzí 8.0 nebo novější | Ano |
| Zařízení s Androidem Enterprise zaregistrovaná s pracovním profilem a se spuštěnou verzí 7.x nebo starší | Ne |
| Zařízení s Androidem se spuštěnou verzí 7.x nebo starší | Ne |

K vytvoření nového hesla pracovního profilu použijte akci Resetovat heslo. Touto akcí vyzvete uživatele k resetování hesla a vytvoření nového, dočasného hesla, které je jenom pro pracovní profil. 

## <a name="reset-a-passcode"></a>Resetování hesla


1. Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) pomocí kterékoli z následujících rolí: Azure Active Directory globální správce, Azure Active Directory Správce služby Intune, pracovník odborné pomoci nebo správce rolí.
2. Vyberte **Zařízení** a potom **Všechna zařízení**.
3. V seznamu zařízení, která spravujete, vyberte zařízení a klikněte na **resetovat heslo**.

## <a name="reset-android-work-profile-and-device-owner-passcodes"></a>Resetovat hesla pracovního profilu Androidu a vlastníka zařízení

Podporovaná zařízení s Androidem Enterprise zaregistrovaná s pracovním profilem dostanou nové heslo k odemknutí spravovaného profilu nebo se koncovému uživateli zobrazí výzva spravovaného profilu.

Pro zařízení s Androidem Enterprise Work Profiling, na kterých běží verze 8. x nebo novější, se koncovým uživatelům zobrazí oznámení o aktivaci resetování hesla hned po dokončení registrace. Oznámení se zobrazí, pokud je nastavené povinné heslo pracovního profilu. Po zadání hesla se oznámení zavře.

Pro vlastníka zařízení s Androidem Enterprise nebo pracovní profil, na kterém běží verze 8. x nebo novější, se po výběru resetování hesla z konzoly zobrazí správce MEM Intune s dočasným heslem. Do zařízení musí být zadáno dočasné heslo. Dočasné heslo pro zařízení se zobrazí v konzole po dobu 7 dnů.


## <a name="remove-iosipados-passcodes"></a>Odebrat hesla pro iOS/iPadOS

Místo obnovování se hesla odeberou ze zařízení se systémem iOS/iPadOS. Pokud jsou nastavené zásady dodržování předpisů vyžadující heslo, zobrazí se uživateli zařízení výzva, aby v Nastavení zadal nové heslo.

## <a name="next-steps"></a>Další kroky

Stav akce, kterou jste spustili, zobrazíte tak, že v podokně **Zařízení** vyberete **Akce zařízení**.
