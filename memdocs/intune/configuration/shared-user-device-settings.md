---
title: Sdílená nebo nastavení zařízení s více uživateli v Microsoft Intune – Azure | Microsoft Docs
description: Přidejte a používejte zařízení s Windows 10 a Windows holografickým pro firmy, která jsou sdílená nebo používaná více uživateli v Microsoft Intune. Podívejte se na seznam všech nastavení a to, co dělají na zařízeních, včetně Microsoft HoloLens. Řídit účty hostů, spravovat účty a odstraňovat neaktivní účty, umožnit nebo zakázat ukládání do místního úložiště, nastavit možnosti napájení a režimu spánku, vybrat, kdy se mají aktualizace instalovat a používat zařízení ve vzdělávacích prostředích v profilu konfigurace zařízení.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f1a11d9b41d17935d9c74490aabb5b983d04b4e1
ms.sourcegitcommit: b94415467831517f2aeab9c7c8a13fe8db8bc8ed
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/14/2020
ms.locfileid: "83401528"
---
# <a name="control-access-accounts-and-power-features-on-shared-pc-or-multi-user-devices-using-intune"></a>Řízení přístupu, účtů a funkcí napájení na sdílených počítačích nebo zařízeních s více uživateli pomocí Intune

Zařízení, která mají více uživatelů, se nazývají sdílená zařízení a jsou běžnou součástí řešení správy mobilních zařízení (MDM). Pomocí Microsoft Intune můžete přizpůsobit sdílená zařízení s následujícími platformami:

- Windows 10 Professional a novější
- Windows 10 Enterprise a novější
- Windows Holografick pro firmy, jako je například HoloLens

Například školy mají zařízení, která obvykle používá mnoho studentů. S tímto nastavením může správce služby Intune ve službě Shared PC zapnout funkci sdíleného počítače, aby bylo možné v jednom okamžiku povolit jednoho uživatele. Studenti nemůžou v zařízení přepínat mezi různými přihlášenými účty. Po odhlášení studenta se také rozhodnete odebrat všechna nastavení specifická pro uživatele.

Koncoví uživatelé se můžou k těmto sdíleným zařízením přihlašovat pomocí účtu Guest. Až se uživatelé přihlásí, přihlašovací údaje se uloží do mezipaměti. Když zařízení používají, koncoví uživatelé získají přístup jenom k funkcím, které povolíte. Například si můžete vybrat, kdy se zařízení dostane do režimu spánku, pokud uživatelé uvidí a ukládají soubory lokálně, povolí nebo zakáže nastavení řízení spotřeby a další. Můžete také řídit, jestli se účet hosta odstraní, když se uživatel odhlásí, nebo odstranit neaktivní účty, když dojde k dosažení prahové hodnoty.

V tomto článku se dozvíte, jak vytvořit konfigurační profil a obsahuje odkazy na dostupná nastavení s jejich popisy.

Při vytvoření profilu v Intune nasadíte nebo přiřadíte tento profil skupinám zařízení ve vaší organizaci. Tento profil můžete také přiřadit ke skupinám zařízení s typy smíšených zařízení a verzí operačního systému (operačního systému).

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.
3. Zadejte tyto vlastnosti:

   - **Platforma**: vyberte **Windows 10 a novější**.
   - **Profil**: vyberte **sdílené zařízení s více uživateli**.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

   - **Název**: Zadejte popisný název nového profilu.
   - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.
7. Nastavení, která můžete konfigurovat v **nastavení konfigurace**, se liší v závislosti na zvolené platformě. Pro podrobnější nastavení vyberte platformu:

    - [Windows 10 a novější](shared-user-device-settings-windows.md)
    - [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md)

8. Vyberte **Další**.

9. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu pro konkrétní IT skupiny, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment` . Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](../fundamentals/scope-tags.md).

    Vyberte **Další**.

10. V části **přiřazení**vyberte skupinu zařízení, která obdrží váš profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](device-profile-assign.md).

    Vyberte **Další**.

    > [!NOTE]
    > Nezapomeňte profil přiřadit ke skupinám zařízení ve vaší organizaci.

11. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

Při příštím ověření každého zařízení se zásada použije.

## <a name="next-steps"></a>Další kroky

- Podívejte se na všechna nastavení pro [Windows 10 a novější](shared-user-device-settings-windows.md) a [Windows holografick pro firmy](shared-user-device-settings-windows-holographic.md).
- Po [přiřazení profilu](device-profile-assign.md) [sledujte jeho stav](device-profile-monitor.md).
