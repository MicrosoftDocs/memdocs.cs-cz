---
title: Přidání nastavení souboru předvoleb do zařízení macOS v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Přidejte soubor XML nebo plist, který obsahuje klíčové informace o vaší aplikaci. Pomocí konfiguračního profilu zařízení předvoleb můžete změnit klíčové informace v souboru seznamu vlastností a přiřadit je k zařízením macOS.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/09/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d226888c3d710a7b80357ebb92130b34ab2fef94
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331991"
---
# <a name="add-a-property-list-file-to-macos-devices-using-microsoft-intune"></a>Přidání souboru se seznamem vlastností do zařízení macOS pomocí Microsoft Intune

Pomocí Microsoft Intune můžete přidat soubor seznamu vlastností (. plist) pro zařízení macOS nebo aplikace na zařízení macOS.

Tato funkce platí pro:

- zařízení macOS se systémem 10,7 a novějším

Soubory seznamu vlastností obvykle obsahují informace o aplikacích macOS. Další informace najdete v tématu [informace o souborech se seznamem vlastností](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) (Web společnosti Apple) a [Nastavení vlastních datových částí](https://support.apple.com/guide/mdm/custom-mdm9abbdbe7/1/web/1).

Tento článek obsahuje seznam a popis různých nastavení souboru seznamu vlastností, které můžete přidat do zařízení macOS. Jako součást řešení správy mobilních zařízení (MDM) pomocí těchto nastavení přidejte ID sady prostředků aplikace (`com.company.application`) a přidejte jeho soubor. plist.

Tato nastavení se přidají do konfiguračního profilu zařízení v Intune a pak se přiřadí nebo nasadí do zařízení macOS.

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte profil](device-profile-create.md).

## <a name="what-you-need-to-know"></a>Co je potřeba vědět

- Tato nastavení se neověřují. Před přiřazením profilu k zařízením Nezapomeňte své změny otestovat.
- Pokud si nejste jistí, jak zadat klíč aplikace, změňte nastavení v rámci aplikace. Pak zkontrolujte soubor předvoleb aplikace pomocí [Xcode](https://developer.apple.com/xcode/) a podívejte se, jak je nastavení nakonfigurované. Apple doporučuje před importem souboru odebrat nespravovatelná nastavení pomocí Xcode.
- Pouze některé aplikace pracují se spravovanými preferencemi a nemusí spravovat všechna nastavení.
- Ujistěte se, že jste nahráli soubory seznamu vlastností, které cílí na nastavení kanálu zařízení, ne na nastavení kanálu uživatele. Soubory seznamu vlastností cílí na celé zařízení.

## <a name="preference-file"></a>Soubor předvoleb

- **Název domény předvolby**: soubory seznamu vlastností se obvykle používají pro webové prohlížeče (Microsoft Edge), [rozšířené ochrany před internetovými útoky v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)a vlastní aplikace. Když vytvoříte doménu předvolby, vytvoří se také ID sady prostředků. Zadejte ID sady prostředků, například `com.company.application`. Zadejte například `com.Contoso.applicationName`, `com.Microsoft.Edge`nebo `com.microsoft.wdav`.
- **Soubor seznamu vlastností**: vyberte soubor seznamu vlastností přidružený k vaší aplikaci. Ujistěte se, že se jedná o soubor `.plist` nebo `.xml`. Například nahrajte soubor `YourApp-Manifest.plist` nebo `YourApp-Manifest.xml`.
- **Obsah souboru**: zobrazí se informace o klíči v souboru seznamu vlastností. Pokud potřebujete změnit klíčové informace, otevřete seznam souborů v jiném editoru a pak tento soubor znovu nahrajte do Intune.

Ujistěte se, že je soubor správně naformátovaný. Soubor by měl mít jenom páry klíč-hodnota a neměl by být zabalené do `<dict>`, `<plist>`nebo značek `<xml>`. Například váš soubor seznamu vlastností by měl vypadat podobně jako v následujícím souboru:

```xml
<key>SomeKey</key>
<string>someString</string>
<key>AnotherKey</key>
<false/>
...
```

Vyberte **OK** > **Vytvořit** a změny uložte. Profil se vytvoří a zobrazí se v seznamu profily.

## <a name="next-steps"></a>Další kroky

Profil je vytvořený, ale zatím se nepoužívá. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).

Další informace o souborech předvoleb pro Microsoft Edge najdete v tématu [Konfigurace nastavení zásad Microsoft Edge na MacOS](https://docs.microsoft.com/deployedge/configure-microsoft-edge-on-mac).
