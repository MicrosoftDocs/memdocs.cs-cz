---
title: Windows 8.1 nastavení dodržování předpisů v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na seznam všech nastavení, která můžete použít při nastavení dodržování předpisů pro Windows 8.1 a zařízení Windows Phone 8,1 v Microsoft Intune. Ověřte kompatibilitu s minimálním a maximálním operačním systémem, nastavte omezení a délku hesla, povolte šifrování pro úložiště dat a další.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/22/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0189fea7f73b70286a6daf844a10806d4c1e8a5d
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79329667"
---
# <a name="windows-81-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Nastavení Windows 8.1 pro označení zařízení jako kompatibilních nebo nekompatibilních s použitím Intune

Tento článek obsahuje seznam a popis různých nastavení dodržování předpisů, která můžete nakonfigurovat na zařízeních Windows 8.1 v Intune. Jako součást řešení správy mobilních zařízení (MDM) použijte Tato nastavení k blokování jednoduchých hesel, nastavení minimální a maximální verze operačního systému a dalších.

Tato funkce platí pro:

- Windows Phone 8.1
- Windows 8.1 a vyšší

Jako správce Intune můžete pomocí těchto nastavení dodržování předpisů ochránit prostředky vaší organizace. Další informace o zásadách dodržování předpisů a o tom, co dělají, najdete v tématu [Začínáme s dodržováním předpisů pro zařízení](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte zásady dodržování předpisů](create-compliance-policy.md#create-the-policy). V části **platforma**vyberte **Windows Phone 8,1** nebo **Windows 8.1 a novější**.

## <a name="device-properties"></a>Vlastnosti zařízení

### <a name="operating-system-version"></a>Verze operačního systému

**Windows Phone 8,1 a novější**
- **Minimální verze operačního systému pro mobilní zařízení**:  
  Zadejte minimální povolenou verzi. Pokud zařízení nesplňuje požadavek na minimální verzi operačního systému, nahlásí se jako nevyhovující. Zobrazí se odkaz s informacemi, jak upgradovat. Uživatel zařízení si může upgradovat svoje zařízení a pak získat přístup k firemním prostředkům.

- **Maximální verze operačního systému pro mobilní zařízení**:  
  Zadejte maximální povolenou verzi. Pokud zařízení používá verzi operačního systému, která je novější než verze zadaná v pravidle, bude přístup k prostředkům organizace blokovaný. Uživateli zařízení se zobrazí výzva, aby kontaktoval správce IT. Zařízení nemá přístup k prostředkům organizace, dokud se nezmění pravidlo, které povoluje verzi operačního systému.

**Windows 8.1 a vyšší**
- **Minimální verze operačního systému**:  
  Zadejte minimální povolenou verzi. Pokud zařízení nesplňuje požadavek na minimální verzi operačního systému, nahlásí se jako nevyhovující. Zobrazí se odkaz s informacemi, jak upgradovat. Uživatel zařízení si může upgradovat svoje zařízení a pak získat přístup k firemním prostředkům.

- **Maximální verze OS**:  
  Zadejte maximální povolenou verzi. Pokud zařízení používá verzi operačního systému, která je novější než verze zadaná v pravidle, bude přístup k prostředkům organizace blokovaný. Uživateli zařízení se zobrazí výzva, aby kontaktoval správce IT. Zařízení nemá přístup k prostředkům organizace, dokud se nezmění pravidlo, které povoluje verzi operačního systému.

Počítače s Windows 8.1 vrací verzi **3**. Pokud je pravidlo verze operačního systému pro Windows nastavené na Windows 8.1, zařízení se nahlásí jako nedodržující předpisy i v případě, že má zařízení Windows 8.1.

## <a name="system-security"></a>Zabezpečení systému

### <a name="password"></a>Heslo

- **Vyžadovat heslo k odemknutí mobilních zařízení**:  
  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Vyžadovat** – uživatelé musí zadat heslo, aby mohli získat přístup ke svému zařízení.

- **Jednoduchá hesla**:  
  - **Nenakonfigurováno** (*výchozí*) – uživatelé můžou vytvářet jednoduchá hesla, třeba **1234** nebo **1111**.
  - **Blok** – uživatelé nemůžou vytvářet jednoduchá hesla, třeba **1234** nebo **1111**.  

- **Minimální délka hesla**:  
  Zadejte minimální počet číslic nebo znaků, které musí heslo obsahovat.

  U zařízení s Windows, která používají účet Microsoft, se zásada dodržování předpisů nevyhodnotí správně, pokud je splněná některá z následujících podmínek:  
  - Minimální délka hesla je větší než osm znaků.
  - Minimální počet znakových sad je víc než 2.

- **Typ hesla**:  
  Vyberte, jestli má heslo obsahovat jenom **číselné** znaky, nebo jestli má být kombinace čísel a dalších znaků (**alfanumerické**).

  Pokud je nastaveno na *alfanumerické*, je k dispozici následující nastavení.  

  - **Počet nealfanumerických znaků v hesle**:  
    Pokud je *typ hesla* nastavený na **alfanumerické**, určete minimální počet znakových sad, které musí heslo obsahovat. Mezi možnosti patří **0** až **4** sady, výchozí hodnota je **1**.
    
    Jde o tyto čtyři znakové sady:
    - Malá písmena
    - Velká písmena
    - Symboly
    - Čísla

    Po nastavení vyššího čísla bude uživatel muset vytvořit složitější heslo. U zařízení, která jsou v účet Microsoft k dispozici, se zásada dodržování předpisů nevyhodnotí správně, pokud je splněna některá z následujících podmínek:

    - Minimální délka hesla je větší než osm znaků.
    - Minimální počet znakových sad je víc než 2.

- **Maximální počet minut nečinnosti před vyžadováním hesla**:  
  Zadejte dobu nečinnosti, než uživatel musí znovu zadat heslo.

- **Vypršení platnosti hesla (dny)**:  
  Vyberte počet dní do vypršení platnosti hesla a uživatelé musí vytvořit nové.

- **Počet předchozích hesel, která zabrání opakovanému použití**:  
  Zadejte počet dříve použitých hesel, která se nedají použít.

### <a name="encryption"></a>Šifrování

- **Šifrování datového úložiště na zařízení**:  
  - **Nenakonfigurováno** (*výchozí*)
  - **Vyžadovat** *– použít k* šifrování úložiště dat na vašich zařízeních.


<!-- not on phone   
- **Require encryption on mobile device**: **Require** the device to be encrypted to connect to data storage resources.
--> 

## <a name="next-steps"></a>Další kroky

- [Přidejte akce pro zařízení nedodržující předpisy](actions-for-noncompliance.md) a [použijte značky oboru k filtrování zásad](../fundamentals/scope-tags.md).
- [Monitorujte zásady dodržování předpisů](compliance-policy-monitor.md).
- Podívejte se na [nastavení zásad dodržování předpisů pro zařízení s Windows 10 a novějším](compliance-policy-create-windows.md) .