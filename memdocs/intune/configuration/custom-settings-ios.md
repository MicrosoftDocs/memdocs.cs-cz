---
title: Přidání vlastního nastavení do zařízení se systémem iOS/iPadOS v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Exportujte nastavení iOS a iPadOS z Apple Configuratoru nebo nástrojů Správce profilů Apple a pak tato nastavení naimportujte do Microsoft Intune. Tato nastavení můžou vytvářet, používat a řídit vlastní nastavení a funkce na zařízeních s iOS/iPadOS. Tento vlastní profil je pak možné přiřadit nebo distribuovat do zařízení se systémem iOS/iPadOS ve vaší organizaci, aby bylo možné vytvořit směrný plán nebo Standard.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1ce86a64955813fba6d202cc3e0e546e8976068b
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2020
ms.locfileid: "90814358"
---
# <a name="use-custom-settings-for-ios-and-ipados-devices-in-microsoft-intune"></a>Použití vlastních nastavení pro zařízení s iOS a iPadOS v Microsoft Intune

Pomocí Microsoft Intune můžete přidat nebo vytvořit vlastní nastavení pro zařízení s iOS/iPadOS pomocí vlastních profilů. Vlastní profily jsou funkcí Intune. Jsou navržené tak, aby bylo možné přidat nastavení a funkce zařízení, které nejsou integrované do Intune.

Při použití zařízení s iOS/iPadOS existují dva způsoby, jak do Intune získat vlastní nastavení:

- [Apple Configurator](https://itunes.apple.com/app/apple-configurator-2/id1037126344?mt=12)
- [Apple Profile Manager](https://support.apple.com/profile-manager)

Tyto nástroje můžete použít k exportu nastavení do konfiguračního profilu. V Intune tento soubor naimportujete a pak ho přiřadíte uživatelům a zařízením s iOS/iPadOS. Po přiřazení jsou nastavení distribuována. Pro iOS/iPadOS ve vaší organizaci taky vytvoří Směrný plán nebo Standard.

Tento článek obsahuje pokyny k používání Apple Configuratoru a Apple Profile Manageru a popisuje vlastnosti, které můžete nakonfigurovat.

## <a name="before-you-begin"></a>Než začnete

Vytvoření [vlastního konfiguračního profilu zařízení s iOS/iPadOS](custom-settings-configure.md).

## <a name="what-you-need-to-know"></a>Co je potřeba vědět

- Při použití **Apple Configuratoru** k vytvoření konfiguračního profilu zkontrolujte, že nastavení, která exportujete, jsou kompatibilní s verzí iOS/iPadOS na zařízeních. Informace potřebné k řešení nekompatibilních nastavení najdete v **referenčních materiálech k profilu konfigurace** a **referenčních materiálech k protokolu správy mobilních zařízení** na webu pro [vývojáře Apple](https://developer.apple.com/).

- Pokud používáte **Apple Profile Manager**, nezapomeňte:

  - Povolit [správu mobilních zařízení](https://help.apple.com/serverapp/mac/5.7/#/apd05B9B761-D390-4A75-9251-E9AD29A61D0C) v Profile Manageru.
  - Přidejte [zařízení s iOS/iPadOS](https://help.apple.com/profilemanager/mac/5.7/#/pm9onzap1984) do Správce profilů.
  - Po přidání zařízení do Správce profilů klikněte v **části**  >  **zařízení** knihovny > vyberte **Nastavení**> zařízení. Zadejte obecné nastavení zařízení.

    Stáhněte a uložte si tento soubor. Zadáte ho v profilu Intune.

  - Ujistěte se, že nastavení, která exportujete z nástroje Apple Profile Manager, jsou kompatibilní s verzí iOS/iPadOS na zařízeních. Informace potřebné k řešení nekompatibilních nastavení najdete v **referenčních materiálech k profilu konfigurace** a **referenčních materiálech k protokolu správy mobilních zařízení** na webu pro [vývojáře Apple](https://developer.apple.com/).

## <a name="custom-configuration-profile-settings"></a>Nastavení vlastního konfiguračního profilu

- **Název vlastního konfiguračního profilu:** Zadejte název zásady. Tento název se zobrazí na zařízení a ve stavu Intune.
- **Soubor konfiguračního profilu:** Přejděte ke konfiguračnímu profilu vytvořenému v Apple Configuratoru nebo Apple Profile Manageru. Maximální velikost souboru je `1000000` bajtů (jen pod 1 MB). Importovaný soubor se zobrazí v části **Obsah souboru**.

  Můžete také přidat tokeny zařízení do vlastních konfiguračních souborů. Tokeny zařízení se používají k přidání informací specifických pro zařízení. Chcete-li například zobrazit sériové číslo, zadejte `{{serialnumber}}` . V zařízení se text zobrazuje podobně jako `123456789ABC` jedinečný pro každé zařízení. Při zadávání proměnných nezapomeňte použít složené závorky `{{ }}` . [Tokeny konfigurace aplikace](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) obsahují seznam proměnných, které se dají použít. Můžete také použít `deviceid` nebo libovolná jiná hodnota specifická pro zařízení.

  > [!NOTE]
  > Proměnné nejsou v uživatelském rozhraní ověřeny a rozlišují se velká a malá písmena. V důsledku toho mohou být profily uloženy s nesprávným vstupem. Pokud například zadáte `{{DeviceID}}` místo `{{deviceid}}` , pak se místo jedinečného ID zařízení zobrazí literální řetězec. Nezapomeňte zadat správné informace.

## <a name="next-steps"></a>Další kroky

Profil je vytvořený, ale zatím se nepoužívá. V dalším kroku [profil přiřadíte](device-profile-assign.md).

Podívejte se, jak [vytvořit profil na zařízeních s macOS](custom-settings-macos.md). 
