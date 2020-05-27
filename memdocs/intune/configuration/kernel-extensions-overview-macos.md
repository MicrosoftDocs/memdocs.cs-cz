---
title: Vytvoření macOS systémů a rozšíření jádra pomocí Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Přidejte nebo vytvořte profil zařízení macOS, který konfiguruje rozšíření systému nebo rozšíření jádra, aby bylo možné přepsat uživatele, přidá identifikátor týmu a přidá do Microsoft Intune sadu prostředků a identifikátor týmu.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/07/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fce8218c9f8fb8757f0aef892f0854f1c386a8bd
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990301"
---
# <a name="add-macos-system-and-kernel-extensions-in-intune"></a>Přidání macOS systémů a rozšíření jádra do Intune

> [!NOTE]
> rozšíření jádra macOS se nahrazují systémovými rozšířeními. Další informace najdete v tématu [Podpora tipů: Použití systémových rozšíření místo rozšíření jádra pro MacOS Catalina 10,15 v Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

Na zařízeních macOS můžete přidat rozšíření jádra a systémová rozšíření. Rozšíření jádra i systémová rozšíření umožňují uživatelům instalovat rozšíření aplikací, která rozšiřuje nativní možnosti operačního systému. Rozšíření jádra spouštějí svůj kód na úrovni jádra. Systémová rozšíření běží v pevně kontrolovaném uživatelském prostoru.

Pokud chcete přidat rozšíření, která se vždycky můžou na svých zařízeních načíst, použijte Microsoft Intune. Intune používá konfigurační profily k vytvoření a přizpůsobení těchto nastavení potřebám vaší organizace. Po přidání těchto funkcí do profilu ho potom nahrajte nebo nasaďte, abyste macOS zařízení ve vaší organizaci.

Tento článek popisuje systémová rozšíření a rozšíření jádra. Také se dozvíte, jak vytvořit profil konfigurace zařízení pomocí rozšíření v Intune.

## <a name="system-extensions"></a>Rozšíření systému

Systémová rozšíření běží v uživatelském prostoru a nepřístupují k jádru. Cílem je zvýšit zabezpečení, poskytnout více koncovým uživatelům řízení a omezit útoky na úrovni jádra. Tato rozšíření mohou být:

- Rozšíření ovladačů, včetně ovladačů na USB, síťových karet (NIC), řadičů sériového portu a zařízení s lidským rozhraním (HID)
- Rozšíření sítě, včetně filtrů obsahu, proxy serverů DNS a klientů VPN
- Rozšíření zabezpečení koncového bodu, včetně zjišťování koncových bodů, odpovědí na koncového bodu a antivirové ochrany

Systémová rozšíření jsou součástí sady aplikace a nainstalují se z aplikace.

Další informace o rozšířeních systému najdete v tématu [systémová rozšíření](https://developer.apple.com/documentation/systemextensions) (otevře web společnosti Apple).

## <a name="kernel-extensions"></a>Rozšíření jádra

Rozšíření jádra přidávají funkce na úrovni jádra. Tyto funkce přistupují k částem operačního systému, ke kterým nemají běžné programy přístup. Vaše organizace může mít konkrétní potřeby nebo požadavky, které nejsou k dispozici v aplikaci, funkci zařízení atd.

Máte třeba program pro kontrolu virů, který v zařízení hledá škodlivý obsah. Toto rozšíření jádra programu pro kontrolu virů můžete přidat jako povolené rozšíření jádra v Intune. Pak přiřaďte rozšíření k zařízením macOS.

Díky této funkci můžou správci uživatelům umožnit přepsat rozšíření jádra, přidat identifikátory týmu a přidat konkrétní rozšíření jádra do Intune.

Další informace o rozšíření jádra najdete v tématu [rozšíření jádra](https://developer.apple.com/library/archive/documentation/Darwin/Conceptual/KernelProgramming/Extend/Extend.html) (Otevírá web společnosti Apple).

## <a name="prerequisites"></a>Požadavky

- Tato funkce platí pro:

  - macOS 10.13.2 a novější (rozšíření jádra)
  - macOS 10,15 a novější (systémová rozšíření)

  Z macOS 10,15 až 10.15.4 se můžou rozšíření jádra a systémová rozšíření spouštět vedle sebe.

- Aby bylo možné tuto funkci používat, musí být zařízení:

  - Zaregistrované v Intune pomocí Program registrace zařízeníu (DEP) společnosti Apple. [Automatická registrace zařízení MacOS](../enrollment/device-enrollment-program-enroll-macos.md) obsahuje další informace.

    NEBO

  - Zaregistrováno v Intune s "uživatelem schváleným zápisem" (termínem Apple). [Příprava na změny rozšíření jádra v MacOS High Sierra](https://support.apple.com/en-us/HT208019) (otevře web společnosti Apple) obsahuje další informace.

## <a name="what-you-need-to-know"></a>Co je potřeba vědět

- Je možné přidat nepodepsaná starší verze jádra a rozšíření systému.
- Nezapomeňte zadat správný identifikátor týmu a ID sady rozšíření. Intune neověřuje hodnoty, které zadáte. Pokud zadáte chybné informace, rozšíření na zařízení nebude fungovat. Identifikátor týmu je přesně 10 alfanumerických znaků dlouhý.

> [!NOTE]
> Informace společnosti Apple, které se týkají podepisování a notarization pro veškerý software. U macOS 10.14.5 a novějších rozšíření jádra nasazená přes Intune nemusí splňovat zásady notarization od společnosti Apple.
>
> Informace o těchto zásadách notarization a všech aktualizacích a změnách najdete v následujících zdrojích informací:
>
> - [Notarizing aplikaci před distribucí](https://developer.apple.com/documentation/security/notarizing_your_app_before_distribution) (otevře web společnosti Apple) 
> - [Příprava na změny rozšíření jádra v MacOS High Sierra](https://support.apple.com/en-us/HT208019) (otevře web společnosti Apple)

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.
3. Zadejte tyto vlastnosti:

    - **Platforma**: vyberte **MacOS**
    - **Profil**: vyberte **rozšíření**.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název zásady. Své zásady pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem zásad je například **MacOS: Přidání antivirové kontroly do rozšíření jádra na zařízeních**.
    - **Popis**: zadejte popis zásady. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.

7. V **nastavení konfigurace**nakonfigurujte nastavení:

    - [macOS](kernel-extensions-settings-macos.md)

8. Vyberte **Další**.
9. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu pro konkrétní IT skupiny, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment` . Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](../fundamentals/scope-tags.md).

    Vyberte **Další**.

10. V části **přiřazení**vyberte uživatele nebo skupiny, které obdrží váš profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](device-profile-assign.md).

    Vyberte **Další**.

11. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

## <a name="next-steps"></a>Další kroky

Profil je po vytvoření připravený k přiřazení. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).
