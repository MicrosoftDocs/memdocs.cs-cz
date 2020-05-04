---
title: Nastavení sdíleného zařízení ve Windows holografické firmy – Microsoft Intune – Azure | Microsoft Docs
description: Přidejte a použijte Windows Holografick pro firmy ke konfiguraci zařízení, která jsou sdílená nebo používaná více uživateli v Microsoft Intune. Podívejte se na seznam nastavení správy účtů a o tom, co dělají na zařízeních, včetně Microsoft HoloLens.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/09/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5b7e77933134dae3523edaf45f8b345aca4fc162
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79326635"
---
# <a name="windows-holographic-for-business-settings-to-manage-shared-devices-using-intune"></a>Nastavení Windows holografického pro firmy pro správu sdílených zařízení pomocí Intune

Zařízení s Windows holografickým pro firmy, jako je Microsoft HoloLens, můžou používat víc uživatelů. Zařízení, která mají více uživatelů, se nazývají sdílená zařízení a jsou součástí řešení správy mobilních zařízení (MDM).

Pomocí Microsoft Intune se uživatelé můžou k těmto sdíleným zařízením přihlašovat pomocí účtu Guest. Když zařízení používají, získají přístup jenom k funkcím, které povolíte.

Tento článek uvádí a popisuje nastavení, která používáte v profilu konfigurace zařízení ve Windows holografické pro firmy. Když profil vytvoříte v Intune, nasadíte nebo přiřadíte tento profil skupinám zařízení ve vaší organizaci. Tento profil můžete také přiřadit ke skupině zařízení s typy smíšených zařízení a verzí operačního systému.

Další informace o této funkci v Intune najdete v tématu [řízení přístupu, účtů a funkcí napájení na sdílených počítačích nebo na zařízeních s více uživateli](shared-user-device-settings.md). Další informace o zprostředkovateli kryptografických služeb systému Windows najdete v tématu [službu ACCOUNTMANAGEMENT CSP](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp).

## <a name="before-your-begin"></a>Před začátkem

[Vytvořte profil](shared-user-device-settings.md).

## <a name="shared-multi-user-device-settings"></a>Sdílená nastavení zařízení s více uživateli

> [!NOTE]
> Zařízení, která používají Windows Holografick pro firmy, včetně Microsoft HoloLens, podporují jenom nastavení **správy účtů** . Pokud nakonfigurujete některá z dalších nastavení zobrazených v Intune, včetně **režimu SDÍLENÉHO počítače**, nemá to na těchto zařízeních žádný vliv.

- **Správa účtů**: Nastavte, aby se **povolilo** automatické odstraňování místních účtů vytvořených hosty a účtů v AD a Azure AD. Když se uživatel odhlásí ze zařízení nebo když se spustí údržba systému, tyto účty se odstraní. Pokud je tato možnost povolená, nastaví se také:
  - **Odstranění účtu**: vyberte, kdy se mají účty odstranit: **v prahové hodnotě úložného prostoru**, **v prahové hodnotě úložiště a na neaktivní prahové hodnotě**nebo **hned po odhlášení**. Zadejte také:
    - **Počáteční hodnota odstranění – prahová hodnota (%)**: zadejte procento místa na disku (0-100). Když celková velikost disku nebo úložiště klesne pod hodnotu, kterou zadáte, odstraní se účty v mezipaměti. Neustále odstraňuje účty pro uvolnění místa na disku. Účty, které jsou neaktivní, se nejprve odstraní.
    - **Zastavit odstranění prahové hodnoty (%)**: zadejte procento místa na disku (0-100). Když celkové místo na disku nebo úložišti odpovídá hodnotě, kterou zadáte, odstranění se zastaví.

  Nastavením této hodnoty **zakážete** , aby byly účty místních účtů, AD a Azure AD vytvořené hosty.

  > [!NOTE]
  > Zařízení Microsoft HoloLens podporují pouze nastavení **správy účtů** .

## <a name="next-steps"></a>Další kroky

- [Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).
- Podívejte se na nastavení pro [Windows 10 a novější](shared-user-device-settings-windows.md).
