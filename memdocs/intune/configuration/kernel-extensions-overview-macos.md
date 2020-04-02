---
title: Vytvoření profilu zařízení rozšíření jádra macOS pomocí Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Přidejte nebo vytvořte profil zařízení macOS a potom nakonfigurujte rozšíření jádra, aby bylo možné přepsat uživatele, přidat identifikátor týmu a sadu prostředků a identifikátor týmu v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8f9212d275b17db6a40e3133b5363cd13c9d13d6
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/02/2020
ms.locfileid: "80551430"
---
# <a name="add-macos-kernel-extensions-in-intune"></a>Přidání rozšíření jádra macOS v Intune

> [!NOTE]
> rozšíření jádra macOS se nahrazují systémovými rozšířeními. Další informace najdete v tématu [Podpora tipů: Použití systémových rozšíření místo rozšíření jádra pro MacOS Catalina 10,15 v Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

Na zařízeních macOS můžete přidat funkce na úrovni jádra. Tyto funkce přistupují k částem operačního systému, ke kterým nemají běžné programy přístup. Vaše organizace může mít konkrétní potřeby nebo požadavky, které nejsou k dispozici v aplikaci, funkci zařízení atd. 

Pokud chcete přidat rozšíření jádra, která se vždycky můžou v zařízeních načíst, přidejte do Microsoft Intune rozšíření jádra (KEXT) a potom tato rozšíření nasaďte do svých zařízení.

Máte třeba program pro kontrolu virů, který v zařízení hledá škodlivý obsah. Toto rozšíření jádra programu pro kontrolu virů můžete přidat jako povolené rozšíření jádra v Intune. Pak přiřaďte rozšíření k zařízením macOS.

Díky této funkci můžou správci uživatelům umožnit přepsat rozšíření jádra, přidat identifikátory týmu a přidat konkrétní rozšíření jádra do Intune.

Tato funkce platí pro:

- macOS 10.13.2 a novější

Aby bylo možné tuto funkci používat, musí být zařízení:

- Zaregistrované v Intune pomocí Program registrace zařízeníu (DEP) společnosti Apple. [Automatická registrace zařízení MacOS](../enrollment/device-enrollment-program-enroll-macos.md) obsahuje další informace.

  NEBO

- Zaregistrováno v Intune s "uživatelem schváleným zápisem" (termínem Apple). [Příprava na změny rozšíření jádra v MacOS High Sierra](https://support.apple.com/en-us/HT208019) (otevře web společnosti Apple) obsahuje další informace.

Intune používá konfigurační profily k vytvoření a přizpůsobení těchto nastavení potřebám vaší organizace. Po přidání těchto funkcí do profilu můžete profil vložit nebo nasadit, abyste macOS zařízení ve vaší organizaci.

V tomto článku se dozvíte, jak vytvořit profil konfigurace zařízení pomocí rozšíření jádra v Intune.

> [!TIP]
> Další informace o rozšíření jádra najdete v tématu [Přehled rozšíření jádra](https://developer.apple.com/library/archive/documentation/Darwin/Conceptual/KernelProgramming/Extend/Extend.html) (otevření webu společnosti Apple).

## <a name="what-you-need-to-know"></a>Co je potřeba vědět

- Je možné přidat nepodepsaná starší verze rozšíření jádra.
- Nezapomeňte zadat správný identifikátor týmu a ID sady rozšíření jádra. Intune neověřuje hodnoty, které zadáte. Pokud zadáte chybné informace, rozšíření na zařízení nebude fungovat. Identifikátor týmu je přesně 10 alfanumerických znaků dlouhý. 

> [!NOTE]
> Informace společnosti Apple, které se týkají podepisování a notarization pro veškerý software. U macOS 10.14.5 a novějších rozšíření jádra nasazená přes Intune nemusí splňovat zásady notarization od společnosti Apple.
>
> Informace o těchto zásadách notarization a všech aktualizacích a změnách najdete v následujících zdrojích informací:
>
> - [Notarizing aplikaci před distribucí](https://developer.apple.com/documentation/security/notarizing_your_app_before_distribution) (otevře web společnosti Apple) 
> - [Příprava na změny rozšíření jádra v MacOS High Sierra](https://support.apple.com/en-us/HT208019) (otevře web společnosti Apple)

> [!NOTE]
> Uživatelské rozhraní (UI) Intune se aktualizuje na celé obrazovce a může trvat několik týdnů. Až do chvíle, kdy váš tenant obdrží tuto aktualizaci, budete mít při vytváření nebo úpravách nastavení popsaných v tomto článku mírně odlišný pracovní postup.

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.
3. Zadejte následující vlastnosti:

    - **Platforma**: vyberte **MacOS**
    - **Profil**: vyberte **rozšíření**.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název zásady. Své zásady pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem zásad je například **MacOS: Přidání rozšíření jádra do zařízení**.
    - **Popis**: zadejte popis zásady. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.

7. V **nastavení konfigurace**nakonfigurujte nastavení:

    - [macOS](kernel-extensions-settings-macos.md)

8. Vyberte **Další**.
9. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu na konkrétní skupiny IT, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment`. Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](../fundamentals/scope-tags.md).

    Vyberte **Další**.

10. V části **přiřazení**vyberte uživatele nebo skupiny, které obdrží váš profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](device-profile-assign.md).

    Vyberte **Další**.

11. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

## <a name="next-steps"></a>Další kroky

Profil je po vytvoření připravený k přiřazení. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).
