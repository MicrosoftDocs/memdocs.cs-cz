---
title: Přidání nebo konfigurace nastavení vzdělávání v Microsoft Intune – Azure | Microsoft Docs
description: Použijte aplikaci pořizovat test v profilu konfigurace zařízení v zařízení s Windows 10 a novějším v Microsoft Intune. Vytvořte konfigurační profil pomocí nastavení vzdělávání a zadejte adresu URL testovací aplikace, vyberte způsob, jakým se uživatelé přihlásí, monitorovat obrazovku během testu a při testování povolí nebo zakáže návrhy textu.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7b1a605e456edb525afec306ff594ba7cc3895aa
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88912725"
---
# <a name="use-the-take-a-test-app-on-windows-10-devices-in-microsoft-intune"></a>Použití aplikace nabrat na zařízeních s Windows 10 v Microsoft Intune

Vzdělávací profily v Intune jsou navržené pro studenty, kteří můžou na zařízeních pořizovat test nebo zkoušku. Tato funkce **zahrnuje testovací URL aplikaci a** nastavení, které umožňují přidat testovací adresu URL, zvolit způsob, jakým se koncoví uživatelé přihlásí k testu, a další. Tato funkce podporuje následující platformu:

- Windows 10 a novější

Když se uživatel přihlásí, automaticky se otevře testovací aplikace se zadaným testem. V zařízení nemůžou běžet žádné jiné aplikace, zatímco probíhá test. [Pořizovat testy ve Windows 10](/education/windows/take-tests-in-windows-10) poskytují další podrobnosti o aplikaci převzít test.

V tomto článku jsou uvedené kroky pro vytvoření profilu konfigurace zařízení v Microsoft Intune. Obsahuje také informace o dostupných nastaveních vzdělávání pro vaše zařízení s Windows 10.

## <a name="create-a-device-profile"></a>Vytvoření profilu zařízení

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.
3. Zadejte tyto vlastnosti:

    - **Platforma**: vyberte **Windows 10 a novější**.
    - **Profil**: vyberte **zabezpečené hodnocení (vzdělávání)**.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

    - **Název**: Zadejte popisný název nového profilu.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.
7. V **nastavení konfigurace**zadejte nastavení, která chcete nakonfigurovat:

    - [Windows 10 a novější](education-settings-windows.md)

8. Vyberte **Další**.

9. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu pro konkrétní IT skupiny, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment` . Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](../fundamentals/scope-tags.md).

    Vyberte **Další**.

10. V části **přiřazení**vyberte uživatele nebo skupinu uživatelů, kteří obdrží váš profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](device-profile-assign.md).

    Vyberte **Další**.

11. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

Při příštím ověření každého zařízení se zásada použije.

## <a name="next-steps"></a>Další kroky

Podívejte se na seznam [Nastavení vzdělávání pro Windows 10](education-settings-windows.md) a jejich popis.

Po [přiřazení profilu](device-profile-assign.md) [sledujte jeho stav](device-profile-monitor.md).