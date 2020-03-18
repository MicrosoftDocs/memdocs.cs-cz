---
title: Sdílená nebo nastavení zařízení s více uživateli v Microsoft Intune – Azure | Microsoft Docs
description: Přidejte a používejte zařízení s Windows 10 a Windows holografickým pro firmy, která jsou sdílená nebo používaná více uživateli v Microsoft Intune. Podívejte se na seznam všech nastavení a to, co dělají na zařízeních, včetně Microsoft HoloLens. Řídit účty hostů, spravovat účty a odstraňovat neaktivní účty, umožnit nebo zakázat ukládání do místního úložiště, nastavit možnosti napájení a režimu spánku, vybrat, kdy se mají aktualizace instalovat a používat zařízení ve vzdělávacích prostředích v profilu konfigurace zařízení.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/04/2019
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
ms.openlocfilehash: 179314f363c8f086239b2c926c4bed8d09c68204
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79333039"
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
2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.
3. Zadejte následující vlastnosti:

   - **Název**: Zadejte popisný název nového profilu.
   - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.
   - **Platforma**: vyberte **Windows 10 a novější**.
   - **Typ profilu**: vyberte **sdílené zařízení s více uživateli**.

4. Nakonfigurujte nastavení pro [Windows 10 a novější](shared-user-device-settings-windows.md) nebo [Windows holografické pro firmy](shared-user-device-settings-windows-holographic.md).

5. Vyberte **OK** > **Vytvořit** a změny uložte.

Váš profil se vytvoří a zobrazí v seznamu, ale ještě nic nedělá. Nezapomeňte [profil přiřadit](device-profile-assign.md) ke skupinám zařízení ve vaší organizaci.

## <a name="next-steps"></a>Další kroky

- Podívejte se na všechna nastavení pro [Windows 10 a novější](shared-user-device-settings-windows.md) a [Windows holografick pro firmy](shared-user-device-settings-windows-holographic.md).
- [Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).
