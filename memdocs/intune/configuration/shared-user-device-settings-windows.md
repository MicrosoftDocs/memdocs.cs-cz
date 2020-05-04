---
title: Nastavení sdíleného zařízení s Windows 10 – Microsoft Intune – Azure | Microsoft Docs
description: Přidejte a použijte Windows 10 ke konfiguraci zařízení, která jsou sdílená nebo používaná více uživateli v Microsoft Intune. Podívejte se na seznam všech nastavení a to, co dělají na zařízeních, včetně Microsoft Surface. Řídit účty hostů, spravovat účty a odstraňovat neaktivní účty, umožnit nebo zakázat ukládání do místního úložiště, nastavit možnosti napájení a režimu spánku, vybrat, kdy se mají aktualizace instalovat a používat zařízení ve vzdělávacích prostředích v profilu konfigurace zařízení.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/10/2020
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
ms.openlocfilehash: c76045413324deef395f546033d37ec47405a28f
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79332247"
---
# <a name="windows-10-and-later-settings-to-manage-shared-devices-using-intune"></a>Nastavení Windows 10 a novějších pro správu sdílených zařízení pomocí Intune

Zařízení se systémem Windows 10 a novějším, jako je například Microsoft Surface, může používat mnoho uživatelů. Zařízení, která mají více uživatelů, se nazývají sdílená zařízení a jsou součástí řešení správy mobilních zařízení (MDM).

Pomocí Microsoft Intune se koncovým uživatelům může přihlásit k těmto sdíleným zařízením pomocí účtu Guest. Když zařízení používají, získají přístup jenom k funkcím, které povolíte. Jako správce Intune nakonfigurujete přístup, zvolíte při odstraňování účtů, řízení řízení spotřeby a další možnosti pro sdílená zařízení s Windows 10.

Tento článek uvádí a popisuje nastavení, která používáte v profilu konfigurace zařízení s Windows 10 (a novějším). Při vytvoření profilu v Intune nasadíte nebo přiřadíte tento profil skupinám zařízení ve vaší organizaci. Tento profil můžete také přiřadit ke skupinám zařízení s typy smíšených zařízení a verzí operačního systému.

Další informace o této funkci v Intune najdete v tématu [řízení přístupu, účtů a funkcí napájení na sdílených počítačích nebo na zařízeních s více uživateli](shared-user-device-settings.md). Další informace o zprostředkovateli kryptografických služeb systému Windows najdete v tématu [SHAREDPC CSP](https://docs.microsoft.com/windows/client-management/mdm/sharedpc-csp).

## <a name="before-your-begin"></a>Před začátkem

[Vytvořte profil](shared-user-device-settings.md).

## <a name="shared-multi-user-device-settings"></a>Sdílená nastavení zařízení s více uživateli

Tato nastavení používají [zprostředkovatele CSP pro SharedPC](https://docs.microsoft.com/windows/client-management/mdm/sharedpc-csp).

- **Režim SDÍLENÉHO počítače**: Pokud chcete zapnout režim sdíleného počítače, vyberte **Povolit** . V tomto režimu se k zařízení v jednom okamžiku přihlašuje jenom jeden uživatel. Jiný uživatel se nemůže přihlásit, dokud se první uživatel odhlásí. **Nenakonfigurováno** (výchozí) Toto nastavení nespravuje Intune a nenabídne žádné zásady pro řízení tohoto nastavení na zařízení.
- **Účet Guest**: vyberte možnost vytvořit hosta na přihlašovací obrazovce. Účty hostů nevyžadují žádné přihlašovací údaje ani ověřování uživatele. Toto nastavení vytvoří nový místní účet pokaždé, když se použije. Možnosti:
  - **Host**: vytvoří na zařízení místně účet hosta.
  - **Doména**: vytvoří účet hosta v Azure Active Directory (AD).
  - **Host a doména**: na zařízení vytvoří účet hosta místně a v Azure Active Directory (AD).
- **Správa účtů**: Nastavte, aby se **povolilo** automatické odstraňování místních účtů vytvořených hosty a účtů v AD a Azure AD. Když se uživatel odhlásí ze zařízení nebo když se spustí údržba systému, tyto účty se odstraní. Pokud je tato možnost povolená, nastaví se také:
  - **Odstranění účtu**: vyberte, kdy se mají účty odstranit: **v prahové hodnotě úložného prostoru**, **v prahové hodnotě úložiště a na neaktivní prahové hodnotě**nebo **hned po odhlášení**. Zadejte také:
    - **Počáteční hodnota odstranění – prahová hodnota (%)**: zadejte procento místa na disku (0-100). Když celková velikost disku nebo úložiště klesne pod hodnotu, kterou zadáte, odstraní se účty v mezipaměti. Neustále odstraňuje účty pro uvolnění místa na disku. Účty, které jsou neaktivní, se nejprve odstraní.
    - **Zastavit odstranění prahové hodnoty (%)**: zadejte procento místa na disku (0-100). Když celkové místo na disku nebo úložišti odpovídá hodnotě, kterou zadáte, odstranění se zastaví.

  Nastavením této hodnoty **zakážete** , aby byly účty místních účtů, AD a Azure AD vytvořené hosty.

- **Místní úložiště**: Pokud chcete zabránit uživatelům v ukládání a zobrazování souborů na pevném disku zařízení, vyberte možnost **povoleno** . Zvolením možnosti **zakázáno** umožníte uživatelům zobrazovat a ukládat soubory místně pomocí Průzkumníka souborů. **Nenakonfigurováno** (výchozí) Toto nastavení nespravuje Intune a nenabídne žádné zásady pro řízení tohoto nastavení na zařízení.
- **Zásady napájení**: Pokud je nastavené na **povoleno**, uživatelé nemůžou vypnout režim hibernace, nemůžou přepsat všechny akce režimu spánku (například zavřít víko) a nemůžou měnit nastavení napájení. Když je tato možnost **zakázaná**, můžou uživatelé zařízení přepnout do režimu hibernace, může zavřít víko zařízení a změnit nastavení napájení. **Nenakonfigurováno** (výchozí) Toto nastavení nespravuje Intune a nenabídne žádné zásady pro řízení tohoto nastavení na zařízení.
- **Časový limit režimu spánku (v sekundách)**: zadejte počet neaktivních sekund (0-18000), než se zařízení přepne do režimu spánku. `0`znamená, že zařízení nikdy nepřejde do režimu spánku. Pokud nenastavíte čas, zařízení přejde do režimu spánku po 3600 sekundách (60 minut).
- **Přihlášení při probuzení z počítače: Pokud**je nastaveno na **povoleno** , bude vyžadovat, aby se uživatelé přihlásili pomocí hesla, když zařízení nepřejde do režimu spánku. Vyberte možnost **zakázáno** , aby uživatelé nemuseli zadávat své uživatelské jméno a heslo. **Nenakonfigurováno** (výchozí) Toto nastavení nespravuje Intune a nenabídne žádné zásady pro řízení tohoto nastavení na zařízení.
- **Čas zahájení údržby (v minutách od půlnoci)**: zadejte čas v minutách (0-1440), kdy se mají spouštět úlohy automatické údržby, například web Windows Update. Výchozí počáteční čas je půlnoc nebo nula (`0`) minut. Změňte čas spuštění zadáním počátečního času v minutách od půlnoci. Například pokud chcete, aby údržba začínala 2., zadejte `120`. Pokud chcete, aby údržba začínala 8. odp. `1200`, zadejte.
- **Zásady vzdělávání**: vyberte možnost **povoleno** pro použití doporučeného nastavení pro zařízení používaná ve školách, které jsou více omezující. Vyberte možnost **zakázáno** , takže se nepoužijí výchozí a doporučené zásady vzdělávání. **Nenakonfigurováno** (výchozí) Toto nastavení nespravuje Intune a nenabídne žádné zásady pro řízení tohoto nastavení na zařízení.

  Další informace o tom, co dělají zásady vzdělávání, najdete v tématu [doporučení konfigurace Windows 10 pro zákazníky ve vzdělávání](https://docs.microsoft.com/education/windows/configure-windows-for-education).

- **Rychlé první přihlášení** (zastaralé): Pokud chcete, aby uživatelé měli rychlý úvodní přihlašovací prostředí, vyberte **povoleno** . Pokud je tato možnost **povolená**, zařízení automaticky připojí nové účty Azure AD, které nejsou správci, k předem nakonfigurovaným místním účtům kandidátů. Výběrem možnosti **zakázáno** zabráníte rychlému prvnímu přihlášení. **Nenakonfigurováno** (výchozí) Toto nastavení nespravuje Intune a nenabídne žádné zásady pro řízení tohoto nastavení na zařízení.

  Toto nastavení se v nadcházející verzi odebere. Toto nastavení nepoužívejte.

  [Ověřování/EnableFastFirstSignIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-enablefastfirstsignin)

> [!TIP]
> [Nastavení sdíleného nebo hostovaného počítače](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc) (otevře si jiný web docs) je skvělým prostředkem této funkce Windows 10, včetně konceptů a zásad skupiny, které je možné nastavit ve sdíleném režimu.

## <a name="next-steps"></a>Další kroky

- [Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).
- Podívejte se na nastavení pro [Windows holografick pro firmy](shared-user-device-settings-windows-holographic.md).
