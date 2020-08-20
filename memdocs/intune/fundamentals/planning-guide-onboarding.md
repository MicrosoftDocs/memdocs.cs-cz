---
title: Postup zavádění Intune
titleSuffix: Microsoft Intune
description: V tomto článku najdete všechny podrobnosti, které byste měli vzít v úvahu při zavádění cloudového řešení Microsoft Intune do svého prostředí.
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
ms.assetid: ac7bd764-5365-4920-8fd0-ea57d5ebe039
ms.reviewer: jeffbu, cgerth
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 19de56bfab6e4f4cf2f1243c6cbaf98053e6ba5e
ms.sourcegitcommit: 46d4bc4fa73b22ae2a6a17a2d1cc6ec933a50e89
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88663255"
---
# <a name="implement-your-microsoft-intune-plan"></a>Implementace plánu Microsoft Intune

V zaváděcí fázi budete Intune nasazovat do svého produkčního prostředí. Proces implementace spočívá v nastavení a konfiguraci Intune a externích závislostí (pokud jsou potřeba) na základě [požadavků na použití](planning-guide-requirements.md).

Následující část nabízí přehledný popis procesu implementace Intune, včetně požadavků a nejdůležitějších úkolů.

## <a name="intune-requirements"></a>Požadavky Intune

Požadavky samotné služby Intune:

- Předplatné Enterprise Mobility + Security (EMS) předplatné služby Intune

- Předplatné Office 365 (pro aplikace Office a aplikace spravované zásadou ochrany aplikací)

- Certifikát Apple APNs (pro povolení správy platforem zařízení s iOS/iPadOS)

- Azure AD Connect (pro synchronizaci adresáře)

- Intune On-Premises Connector pro Exchange (pro podmíněný přístup pro místní Exchange, pokud je potřeba)

- Konektor certifikátu Intune (pro nasazení certifikátu SCEP, pokud je potřeba)

>[!TIP]
> Úplný seznam zařízení, která můžete spravovat pomocí Intune, najdete v seznamu [podporovaných zařízení](supported-devices-browsers.md).

## <a name="intune-implementation-process"></a>Proces implementace Intune

Pro implementaci nasazení Intune jsme identifikovali 13 samostatných úloh. V závislosti na požadavcích vaší firmy, stávající infrastruktury a strategie správy zařízení už mohly být některé z těchto úloh provedeny. Některé se nemusí vašeho plánu týkat.

### <a name="task-1-get-an-intune-subscription"></a>1. úkol: Správa předplatného Intune

Jak je uvedeno v části s požadavky pro Intune výše, potřebujete předplatné EMS nebo Intune. Pokud ho organizace nemá, obraťte se na Microsoft nebo na tým, který se stará o účty Microsoft, a informujte je, že se zajímáte o nákup řešení Enterprise Mobility + Security (EMS) nebo Intune.

- Další informace o [nákupu Microsoft Intune](https://www.microsoft.com/cloud-platform/microsoft-intune-pricing).

### <a name="task-2-add-office-365-subscription"></a>2. úkol: Přidání předplatného Office 365

Tento krok je volitelný. Pokud plánujete používat Exchange Online a spravovat mobilní aplikace Office pomocí zásad ochrany aplikací, potřebujete předplatné Office 365. Pokud organizace nemá předplatné Office 365, obraťte se na Microsoft nebo na tým, který se stará o účty Microsoft, a informujte je, že se zajímáte o nákup Office 365.

- Další informace o [nákupu Office 365](https://products.office.com/business/compare-office-365-for-business-plans).

### <a name="task-3-add-users-groups-in-azure-ad"></a>3. úkol: Přidání skupin uživatelů do Azure AD

Na základě scénáře použití a požadavků na nasazení Intune možná bude potřeba přidat do služby Active Directory nebo Azure Active Directory uživatele nebo skupiny zabezpečení. Zkontrolujte současné uživatele a skupiny zabezpečení ve službě Active Directory nebo Azure Active Directory a zjistěte, jestli plně vyhovují vašim potřebám. Při přidávání nových uživatelů a skupin zabezpečení doporučujeme, abyste je přidali ve službě Active Directory a synchronizovali je s Azure Active Directory s použitím Azure AD Connect.

- Další informace o [přidání uživatelů nebo skupin v Intune](users-add.md).
<!---why not send them to the AAD connect topic? Question out to Andre: https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect--->


### <a name="task-4-assign-intune-and-office-365-user-licenses"></a>4. úkol: Přiřazení uživatelských licencí Intune a Office 365

Všichni uživatelé, u kterých budete zavádět EMS/Intune a Office 365, musí mít přiřazenou licenci. Licence EMS/Intune a Office 365 můžete přiřadit v centru pro správu Microsoft 365.

- Další informace o [přiřazení licencí Intune](licenses-assign.md).

### <a name="task-5-set-mobile-device-management-authority-to-intune"></a>5. úkol: Nastavení autority pro správu mobilních zařízení v Intune

Než začnete v Intune nastavovat, konfigurovat, spravovat a registrovat zařízení, musíte nastavit autoritu pro správu mobilních zařízení v Intune.

- Přečtěte si další informace o [tom, jak nastavit autoritu pro správu zařízení](mdm-authority-set.md).

### <a name="task-6-enable-device-platforms"></a>6. úkol: Povolení platforem zařízení

Ve výchozím nastavení jsou povolené většinu platforem zařízení s výjimkou zařízení Apple (iOS/iPadOS a Mac). Aby bylo možné zařízení s iOS/iPadOS registrovat a spravovat v Intune, musí být povolená platforma zařízení. K tomu potřebujete vytvořit MDM Push Certificate a přidat ho do Intune.

- Další informace o [povolení registrace zařízení Apple](../enrollment/apple-mdm-push-certificate-get.md).

### <a name="task-7-add-and-deploy-terms-and-conditions-policies"></a>7. úkol: Přidání a nasazení zásad pro podmínky a ujednání

Intune podporuje zásady pro podmínky a ujednání. Podle potřeby přidejte zásady pro podmínky a ujednání a nasaďte je u cílových skupin na základě způsobu použití nasazené služby Intune a požadavků.

- Další informace o [přidání a nasazení zásad pro podmínky a ujednání](../enrollment/terms-and-conditions-create.md).

### <a name="task-8-add-and-deploy-configuration-policies"></a>8. úkol: Přidání a nasazení zásad konfigurace

Intune podporuje dva typy zásad konfigurace: obecné a vlastní. Podle potřeby přidejte zásady konfigurace a nasaďte je u cílových skupin na základě způsobu použití nasazené služby Intune a požadavků.

- Další informace o [přidání a nasazení zásad konfigurace](../configuration/device-profiles.md).

### <a name="task-9-add-and-deploy-resource-profiles"></a>9. úkol: Přidání a nasazení profilů prostředků

Intune podporuje profily e-mailu, Wi-Fi a VPN. Podle potřeby přidejte tyto profily a nasaďte je u cílových skupin na základě způsobu použití nasazené služby Intune a požadavků.

- Přečtěte si další informace o [povolení přístupu k firemním prostředkům v Intune](../configuration/device-profiles.md).

### <a name="task-10-add-and-deploy-apps"></a>10. úkol: Přidání a nasazení aplikací

Intune podporuje nasazení webových aplikací, obchodních aplikací a aplikací z veřejného Storu. Také můžete spravovat aplikace s integrovanou sadou Intune SDK na základě jejich přidružení k zásadám ochrany aplikací. Podle potřeby přidejte aplikace a nasaďte je u cílových skupin na základě způsobu použití nasazené služby Intune a požadavků.

- Další informace o [přidání a nasazení aplikací](../apps/app-management.md).

### <a name="task-11-add-and-deploy-compliance-policies"></a>11. úkol: Přidání a nasazení zásad dodržování předpisů

Intune podporuje zásady dodržování předpisů. Podle potřeby přidejte zásady dodržování předpisů a nasaďte je u cílových skupin na základě způsobu použití nasazené služby Intune a požadavků.

- Další informace o [zásadách dodržování předpisů](../protect/device-compliance-get-started.md).

### <a name="task-12-enable-conditional-access-policies"></a>Úloha 12: povolení zásad podmíněného přístupu

Intune podporuje podmíněný přístup pro Exchange Online, místní Exchange, SharePoint Online, Online Skype pro firmy a Dynamics CRM Online. Podle potřeby povolte a nakonfigurujte podmíněný přístup na základě způsobu použití nasazené služby Intune a požadavků.

- Přečtěte si další informace o [podmíněném přístupu](../protect/conditional-access.md).

### <a name="task-13-enroll-devices"></a>13. úkol: Registrace zařízení

Intune podporuje platformy zařízení s iOS/iPadOS, Mac OS, Androidem a Windows Desktop. Podle potřeby zaregistrujte požadované platformy mobilních zařízení na základě způsobu použití nasazené služby Intune a požadavků.

- Další informace o [registraci zařízení](../enrollment/device-enrollment.md).


## <a name="next-steps"></a>Další kroky
Přečtěte si pokyny k [testování a ověřování nasazeného řešení Intune](planning-guide-test-validation.md).
