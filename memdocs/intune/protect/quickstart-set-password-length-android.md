---
title: Rychlý Start – zásada dodržování předpisů heslem pro zařízení s Androidem
titleSuffix: Microsoft Intune
description: V tomto rychlém startu použijete Microsoft Intune k nastavení délky hesla potřebného pro zařízení s Androidem.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/21/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 81b4fa08-5333-4c54-9f49-8db5f6984ed2
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b2e2d5fb2f698d7e0b544dbdbd4ab05f2b94b7ea
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80325461"
---
# <a name="quickstart-create-a-password-compliance-policy-for-android-devices"></a>Rychlý start: Vytvoření zásady dodržování předpisů pro hesla pro zařízení s Androidem

V tomto rychlém startu použijete Microsoft Intune k tomu, aby uživatelé Androidu od zaměstnanců mohli zadat heslo určité délky, než se udělí přístup k informacím v jejich zařízeních s Androidem.

Zásada dodržování předpisů Intune pro zařízení určuje pravidla a nastavení, která zařízení musí splňovat, aby bylo považováno za dodržující předpisy. Zásady dodržování předpisů s podmíněným přístupem můžete použít k povolení nebo blokování přístupu k prostředkům společnosti. Můžete také získat sestavy zařízení a provádět akce v případě nedodržování předpisů.

> [!IMPORTANT]
> Kromě nastavení hesla byste také měli zvážit další nastavení zabezpečení systému pro ochranu pracovníků. Další informace najdete v tématu [Systémové nastavení zabezpečení](compliance-policy-create-android-for-work.md).

Pokud nemáte předplatné Intune, [Zaregistrujte si bezplatný zkušební účet](../fundamentals/free-trial-sign-up.md).

## <a name="sign-in-to-intune"></a>Přihlášení k Intune

Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) jako [globální správce](../fundamentals/users-add.md#types-of-administrators) nebo [Správce služby](../fundamentals/users-add.md#types-of-administrators)Intune.

## <a name="create-a-device-compliance-policy"></a>Vytváření zásad dodržování předpisů pro zařízení

Vytvořte zásadu dodržování předpisů pro zařízení, která bude vyžadovat, aby uživatelé v Androidu mohli zadat heslo určité délky předtím, než se udělí přístup k informacím v jejich zařízeních s Androidem.

1. V Intune vyberte **zařízení** > **zásady dodržování předpisů** > **vytvořit zásadu**.

2. Jako **Název** přidejte **Dodržování předpisů v Androidu**. Přidejte také **Popis**.

3. Jako **platformu**vyberte **Android Enterprise**.

4. Jako **typ profilu**vyberte **pracovní profil**.

5. Vyberte **Nastavení** > **Zabezpečení systému** a zobrazte okno **Zabezpečení systému** Androidu.

6. U možnosti **Vyžadovat heslo k odemknutí mobilních zařízení** vyberte **Vyžadovat**.

7. Pro **požadovaný typ hesla**vyberte **aspoň číslice**.

8. Pro **minimální délku hesla**zadejte **6**.

    ![Snímek obrazovky s vytvořením skupiny v Microsoft Intune](./media/quickstart-set-password-length-android/quickstart-set-password-length-android-01.png)

9. Až to budete mít, vyberte **ok** ** > v** > **vytvořit** vytvořte zásadu.

Po úspěšném vytvoření zásady se zobrazí v seznamu zásad complice zařízení.

## <a name="clean-up-resources"></a>Vyčištění prostředků

Až tuto zásadu nebudete potřebovat, odstraňte ji. Uděláte to tak, že tuto zásadu dodržování předpisů vyberete a kliknete na **Odstranit**.

## <a name="next-steps"></a>Další kroky

V tomto rychlém startu jste v Intune vytvořili zásadu dodržování předpisů pro firemní zařízení s Androidem, která vyžaduje zadání hesla o minimální délce šesti znaků. Další informace o vytváření zásad dodržování předpisů najdete v článku [Začínáme se zásadami dodržování předpisů zařízeními v Intune](device-compliance-get-started.md).

Pokud chcete postupovat podle této série rychlých startů Intune, pokračujte k dalšímu rychlému startu.

> [!div class="nextstepaction"]
> [Rychlý start: Odeslání oznámení zařízením nedodržujícím předpisy](quickstart-send-notification.md)
