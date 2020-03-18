---
title: Konfigurace dodržování předpisů zařízení a aplikací během migrace do Intune
titleSuffix: Microsoft Intune
description: Tento článek popisuje kroky potřebné ke konfiguraci zásad dodržování předpisů zařízením a správy aplikací během migrace do Microsoft Intune.
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
ms.assetid: 0062d08e-e5b3-4f73-8b64-5ad95adbe945
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5f0f4106921f7b4ef1d33e72a217246543512bb5
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331231"
---
# <a name="configure-device-compliance-and-app-management-policies-when-migrating-to-microsoft-intune"></a>Konfigurace zásad dodržování předpisů zařízením a správy aplikací během migrace do Microsoft Intune

Hlavním cílem při migraci do Intune je zajistit, aby se všechna zařízení zaregistrovala ve službě Intune a dodržovala její zásady. Zásady pro zařízení pomáhají spravovat nejen zařízení vlastněná společností, která mají jednoho uživatele, ale také osobní zařízení uživatelů (BYOD), sdílená zařízení, jako jsou veřejné terminály, počítače v prodejnách nebo tablety sdílené více studenty ve třídě, a zařízení bez uživatelů (jenom iOS).

Každé zařízení využívá jinou platformu s jinými nastaveními. Zásady zařízení Intune ale fungují na všech těchto platformách, pro které poskytují následující možnosti správy mobilních zařízení:

- Určení počtu zařízení, která si jednotliví uživatelé můžou zaregistrovat

- Správa nastavení zařízení (například šifrování na úrovni zařízení, délka hesla nebo používání kamery)

- Dodávání aplikací, e-mailových profilů, profilů VPN apod.

- Vyhodnocení kritérií pro zásady dodržování předpisů zabezpečení na úrovni zařízení

> [!IMPORTANT]
> Zásady správy zařízení se nepřiřazují přímo jednotlivým zařízením nebo uživatelům, ale skupinám uživatelů. Zásady je možné použít přímo pro skupinu uživatelů a tím současně pro zařízení uživatelů, nebo je možné je použít pro skupinu zařízení a tím současně pro členy skupiny.

## <a name="task-list-for-device-compliance-policies"></a>Seznam kroků zavedení zásad dodržování předpisů pro zařízení

### <a name="task-1-add-device-groups-optional"></a>Krok 1: Přidání skupin zařízení (volitelné)

Skupiny zařízení můžete vytvořit, když potřebujete provádět úlohy správy, které jsou založené na identitě zařízení (místo na identitě uživatele).

Skupiny zařízení jsou užitečné ke správě zařízení bez vyhrazených uživatelů, jako jsou veřejné terminály nebo zařízení sdílená pracovníky ve směnném provozu nebo přiřazená určitému umístění.

Když nakonfigurujete skupiny zařízení ještě před registrací zařízení, můžete využít kategorie zařízení k tomu, aby se zařízení při registraci automaticky seskupovala. Automaticky pak obdrží zásady zařízení příslušné skupiny. Další informace najdete v článku [Začínáme se skupinami](groups-get-started.md).

### <a name="task-2-use-resource-access-profiles-wi-fi-vpn-and-email-certificates"></a>Krok 2: Použití profilů přístupu k prostředkům (sítím Wi-Fi, VPN a e-mailovým certifikátům)

Profily přístupu k prostředkům dodají pro registrovaná zařízení certifikáty a nastaví konfiguraci přístupu. Pokud používáte ověřování pomocí certifikátů, [nakonfigurujte certifikáty](../protect/certificates-configure.md).

### <a name="task-3-create-and-deploy-device-configuration-profiles"></a>Krok 3: Vytvoření a nasazení profilů konfigurace zařízení

Je potřeba vytvořit profil konfigurace zařízení k vynucení nastavení na úrovni zařízení, například: zakázání fotoaparátu nebo obchodu s aplikacemi, konfigurace režimu jedné aplikace, nastavení domovské obrazovky apod. Přečtěte si další informace o [profilech zařízení](../configuration/device-profiles.md).

#### <a name="directly-import-iosipados-configuration-profiles-optional"></a>Přímo importovat konfigurační profily pro iOS/iPadOS (volitelné)

- **Profily Apple Configuratoru pro iOS (7.1 a novější):** Pokud vaše existující řešení MDM používá profily Apple Configuratoru (soubory .mobileconfig), Intune je může přímo importovat jako vlastní zásady konfigurace.

- **zásady konfigurace mobilních aplikací pro iOS:** Pokud vaše existující řešení MDM používá zásady konfigurace mobilních aplikací pro iOS/iPadOS, Intune je může přímo importovat, pokud odpovídají formátu XML určenému společností Apple pro seznamy vlastností.

- Zjistěte, jak přidat vlastní zásady pro [iOS](../configuration/custom-settings-ios.md).

### <a name="task-4-create-and-deploy-device-compliance-policies-optional"></a>Krok 4: Vytvoření a nasazení zásad dodržování předpisů pro zařízení (volitelné)

Zásady dodržování předpisů pro zařízení vyhodnocují nastavení týkající se zabezpečení a vytvářejí sestavy, které ukazují, jestli jsou zařízení v souladu s firemními standardy. Nastavení zahrnují:

- Délka PIN kódu

- Stav jailbreaku

- Verze operačního systému

Podívejte se na další materiály k nastavení kompatibility zařízení:

- Informace o [zásadách dodržování předpisů pro zařízení](../protect/device-compliance-get-started.md).

### <a name="task-5-publish-and-deploy-apps"></a>Krok 5: Publikování a nasazení aplikací

Pokud používáte správu mobilních zařízení (MDM) v Intune, můžete dodat aplikace vyžádáním jejich automatické instalace nebo jejich zpřístupněním v Portálu společnosti.

- [Jak přidat aplikace](../apps/apps-add.md)

- [Jak nasadit aplikace](../apps/apps-deploy.md)

### <a name="task-6-enable-device-enrollment"></a>Krok 6: Povolení registrace zařízení

Registrace zařízení je nezbytná k jejich správě. Zjistěte, [jak se připravit na registraci firemních zařízení a osobních zařízení uživatelů](../enrollment/device-enrollment.md).

## <a name="next-steps"></a>Další kroky

[Konfigurace zásad ochrany aplikací (volitelné)](../apps/app-protection-policies.md)
