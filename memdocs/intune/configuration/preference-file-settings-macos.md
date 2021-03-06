---
title: Přidání nastavení souboru předvoleb do zařízení macOS v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Přidejte soubor XML nebo plist, který obsahuje klíčové informace o vaší aplikaci. Pomocí konfiguračního profilu zařízení předvoleb můžete změnit klíčové informace v souboru seznamu vlastností a přiřadit je k zařízením macOS.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/05/2020
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
ms.openlocfilehash: 478cce186d5f2943aeb5730acf90c3e875c8b687
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915309"
---
# <a name="add-a-property-list-file-to-macos-devices-using-microsoft-intune"></a>Přidání souboru se seznamem vlastností do zařízení macOS pomocí Microsoft Intune

Pomocí Microsoft Intune můžete přidat soubor seznamu vlastností (. plist) pro zařízení macOS nebo aplikace na zařízení macOS.

Tato funkce platí pro:

- macOS 10,7 a novější

Soubory seznamu vlastností obsahují informace o aplikacích macOS. Další informace najdete v tématu [informace o souborech se seznamem vlastností](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) (Web společnosti Apple) a [Nastavení vlastních datových částí](https://support.apple.com/guide/mdm/custom-mdm9abbdbe7/1/web/1).

Tento článek obsahuje seznam a popis různých nastavení souboru seznamu vlastností, které můžete přidat do zařízení macOS. Jako součást řešení správy mobilních zařízení (MDM) pomocí těchto nastavení přidejte ID sady prostředků aplikace ( `com.company.application` ) a přidejte soubor. plist aplikace.

Tato nastavení se přidají do konfiguračního profilu zařízení v Intune a pak se přiřadí nebo nasadí do zařízení macOS.

## <a name="what-you-need-to-know"></a>Co je potřeba vědět

- Tato nastavení se neověřují. Před přiřazením profilu k zařízením Nezapomeňte své změny otestovat.
- Pokud si nejste jistí, jak zadat klíč aplikace, změňte nastavení v rámci aplikace. Pak zkontrolujte soubor předvoleb aplikace pomocí [Xcode](https://developer.apple.com/xcode/) a podívejte se, jak je nastavení nakonfigurované. Apple doporučuje před importem souboru odebrat nespravovatelná nastavení pomocí Xcode.
- Pouze některé aplikace pracují se spravovanými preferencemi a nemusí spravovat všechna nastavení.
- Ujistěte se, že jste nahráli soubory seznamu vlastností, které cílí na nastavení kanálu zařízení, ne na nastavení kanálu uživatele. Soubory seznamu vlastností cílí na celé zařízení.

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.
3. Zadejte tyto vlastnosti:

    - **Platforma**: vyberte **MacOS**
    - **Profil**: vyberte **soubor předvoleb**.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název zásady. Své zásady pojmenujte, abyste je později mohli snadno identifikovat. Dobrý název zásady je například **MacOS: přidejte soubor předvolby, který KONFIGURUJE ATP programu Microsoft Defender na zařízeních**.
    - **Popis**: zadejte popis zásady. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.

7. V **nastavení konfigurace**nakonfigurujte nastavení:

    - **Název domény předvolby**: Zadejte ID sady prostředků, například `com.company.application` . Zadejte například `com.Contoso.applicationName` , `com.Microsoft.Edge` nebo `com.microsoft.wdav` .

      Soubory seznamu vlastností se obvykle používají pro webové prohlížeče (Microsoft Edge), [rozšířené ochrany před internetovými útoky v programu Microsoft Defender](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)a vlastní aplikace. Když vytvoříte doménu předvolby, vytvoří se také ID sady prostředků.

    - **Soubor seznamu vlastností**: vyberte soubor seznamu vlastností přidružený k vaší aplikaci. Ujistěte se, že se jedná o `.plist` `.xml` soubor nebo. Například odešlete `YourApp-Manifest.plist` `YourApp-Manifest.xml` soubor nebo.

      Zobrazí se informace o klíči v souboru seznamu vlastností. Pokud potřebujete změnit klíčové informace, otevřete seznam souborů v jiném editoru a pak tento soubor znovu nahrajte do Intune.

    Ujistěte se, že je soubor správně naformátovaný. Soubor by měl obsahovat pouze páry klíč-hodnota a neměl by být zabalen `<dict>` do `<plist>` značek, nebo `<xml>` . Například váš soubor seznamu vlastností by měl vypadat podobně jako v následujícím souboru:

    ```xml
    <key>SomeKey</key>
    <string>someString</string>
    <key>AnotherKey</key>
    <false/>
    ...
    ```

8. Vyberte **Další**.
9. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu pro konkrétní IT skupiny, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment` . Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](../fundamentals/scope-tags.md).

    Vyberte **Další**.

10. V části **přiřazení**vyberte uživatele nebo skupiny, které obdrží váš profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](device-profile-assign.md).

    Vyberte **Další**.

11. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).

Další informace o souborech předvoleb pro Microsoft Edge najdete v tématu [Konfigurace nastavení zásad Microsoft Edge na MacOS](/deployedge/configure-microsoft-edge-on-mac).