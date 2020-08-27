---
title: Přidání vlastních nastavení do zařízení s Windows Phone 8.1 v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Přidejte nebo vytvořte vlastní profil, abyste v Microsoft Intune mohli u zařízení s Windows Phone 8.1 používat nastavení OMA-URI.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ROBOTS: NOINDEX
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c0adb573dbb40f00a1b43b9fb356cdc20b97b669
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910073"
---
# <a name="use-custom-settings-for-windows-phone-81-devices-in-intune"></a>Použití vlastních nastavení pro zařízení s Windows Phone 8.1 v Intune

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

V Microsoft Intune můžete vlastní profily použít k přidání nebo vytvoření vlastního nastavení u zařízení s Windows Phone 8.1. Vlastní profily jsou funkcí Intune. Jsou navržené tak, aby bylo možné přidat nastavení a funkce zařízení, které nejsou integrované do Intune.

Vlastní profily zařízení s Windows Phone 8.1 používají nastavení OMA-URI (Open Mobile Alliance Uniform Resource Identifier) ke konfiguraci různých funkcí. Tato nastavení obvykle používají výrobci mobilních zařízení k řízení funkcí na zařízení. [Dokumentace k protokolu Windows Phone 8,1 MDM](/previous-versions/windows/it-pro/windows-phone/dn499787(v=technet.10)) obsahuje seznam nastavení.

V tomto článku si ukážeme, jak vytvořit vlastní profil pro zařízení s Windows Phone 8.1. 

## <a name="before-you-begin"></a>Než začnete

[Vytvořte vlastní profil Windows Phone 8,1](custom-settings-configure.md).

## <a name="custom-oma-uri-settings"></a>Vlastní nastavení OMA-URI

- **Nastavení OMA-URI**: **přidejte** následující nastavení:

  - **Název:** Zadejte jedinečný název nastavení OMA-URI, abyste ho v seznamu poznali.
  - **Popis:** Zadejte popis, který přehledně vystihuje nastavení, a další důležité informace kvůli jeho snadnějšímu vyhledání.
  - **OMA-URI** (rozlišuje velká a malá písmena): Zadejte nastavení OMA-URI, které chcete použít.
  - **Datový typ**: vyberte datový typ, který budete používat pro toto nastavení OMA-URI. Možnosti:

    - Řetězec
    - Řetězec (soubor XML)
    - Datum a čas
    - Integer
    - Plovoucí desetinná čárka
    - Logická hodnota
    - Base64 (soubor)

  - **Hodnota:** Zadejte datovou hodnotu, kterou chcete přidružit k zadanému nastavení OMA-URI. Hodnota závisí na vybraném datovém typu. Pokud například vyberete položku **Datum a čas**, vyberte hodnotu z ovládacího prvku pro výběr data.

  Po přidání nastavení můžete vybrat **Exportovat**. **Export** vytvoří seznam všech hodnot, které jste přidali do souboru hodnot oddělených čárkou (.csv).

## <a name="example"></a>Příklad

V následujícím příkladu se zařízení Windows 8.1 Phone zabraňují změnám mobilních sítí, když cestují mimo oblast pokrytí dopravců.

- **Název**: Povolení roamingu mobilních dat
- **Popis**: povolení nebo zákaz roamingu mobilních dat
- **OMA-URI** (rozlišuje velká a malá písmena):./Vendor/MSFT/PolicyManager/my/Connectivity/AllowCellularDataRoaming
- **Datový typ**: celé číslo
- **Hodnota**: 0

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md)a [sledujte jeho stav](device-profile-monitor.md).

Vytvořte si [vlastní profil na zařízeních s Windows 10](custom-settings-windows-10.md).