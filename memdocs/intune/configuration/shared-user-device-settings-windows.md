---
title: Nastavení sdíleného zařízení s Windows 10 – Microsoft Intune – Azure | Microsoft Docs
description: Přidejte a použijte Windows 10 ke konfiguraci zařízení, která jsou sdílená nebo používaná více uživateli v Microsoft Intune. Podívejte se na seznam všech nastavení a to, co dělají na zařízeních, včetně Microsoft Surface. Řídit účty hostů, spravovat účty a odstraňovat neaktivní účty, umožnit nebo zakázat ukládání do místního úložiště, nastavit možnosti napájení a režimu spánku, vybrat, kdy se mají aktualizace instalovat a používat zařízení ve vzdělávacích prostředích v profilu konfigurace zařízení.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
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
ms.openlocfilehash: f013074ac67b7622b509d8b9781de3ab5f4041e0
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429495"
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

- **Režim SDÍLENÉHO počítače**: **Povolit** zapne režim sdílení počítače. V tomto režimu se k zařízení v jednom okamžiku přihlašuje jenom jeden uživatel. Jiný uživatel se nemůže přihlásit, dokud se první uživatel odhlásí. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Účet Guest**: vyberte možnost vytvořit hosta na přihlašovací obrazovce. Účty hostů nevyžadují žádné přihlašovací údaje ani ověřování uživatele. Toto nastavení vytvoří nový místní účet pokaždé, když se použije. Možnosti:
  - **Host**: vytvoří na zařízení místně účet hosta.
  - **Doména**: vytvoří účet hosta v Azure Active Directory (AD).
  - **Host a doména**: na zařízení vytvoří účet hosta místně a v Azure Active Directory (AD).
- **Správa účtů**: vyberte, jestli se mají automaticky odstranit účty. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Povoleno**: účty vytvořené hostům a účty v AD a Azure AD se automaticky odstraní. Když se uživatel odhlásí ze zařízení nebo když se spustí údržba systému, tyto účty se odstraní.

    Dále zadejte:

    - **Odstranění účtu**: vyberte, kdy se mají účty odstranit:
      - **V prahové hodnotě prostoru úložiště**
      - **V prahové hodnotě prostoru úložiště a neaktivní prahové hodnoty**
      - **Ihned po odhlášení**

    Dále zadejte:

    - **Počáteční hodnota odstranění – prahová hodnota (%)**: zadejte procento místa na disku (0-100). Když celková velikost disku nebo úložiště klesne pod hodnotu, kterou zadáte, odstraní se účty v mezipaměti. Neustále odstraňuje účty pro uvolnění místa na disku. Účty, které jsou neaktivní, se nejprve odstraní.
    - **Zastavit odstranění prahové hodnoty (%)**: zadejte procento místa na disku (0-100). Když celkové místo na disku nebo úložišti odpovídá hodnotě, kterou zadáte, odstranění se zastaví.
    - **Prahová hodnota neaktivního účtu**: zadejte počet po sobě jdoucích dnů, než se účet odstraní, od 0-60 dnů.

  - **Zakázané**: účty místní, AD a Azure AD vytvořené hosty zůstanou na zařízení a neodstraňují se.

- **Místní úložiště**: pomocí místního úložiště můžou uživatelé ukládat soubory na pevném disku zařízení a zobrazovat je. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Povoleno**: zabraňuje uživatelům v ukládání a zobrazování souborů na pevném disku zařízení.
  - **Zakázáno**: umožňuje uživatelům zobrazovat a ukládat soubory místně pomocí Průzkumníka souborů.

- **Zásady napájení**: povolí nebo zakáže uživatelům měnit nastavení napájení. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Povoleno**: uživatelé nemohou vypnout režim hibernace, nelze přepsat všechny akce režimu spánku (například zavření víka) a nelze změnit nastavení napájení.
  - **Zakázáno**: uživatelé můžou zařízení přepnout do režimu hibernace, může zavřít víko zařízení a změnit nastavení napájení.

- **Časový limit režimu spánku (v sekundách)**: zadejte počet neaktivních sekund (0-18000), než se zařízení přepne do režimu spánku. `0`znamená, že zařízení nikdy nepřejde do režimu spánku. Pokud nenastavíte čas, zařízení přejde do režimu spánku po 3600 sekundách (60 minut).

- **Přihlášení při probuzení z počítače**: vyberte, jestli se uživatelé musí přihlásit, až se zařízení přepne do režimu spánku. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Povoleno**: vyžaduje, aby se uživatelé přihlásili pomocí hesla, když zařízení nepřejde do režimu spánku.
  - **Zakázáno**: uživatelé nemusejí zadávat uživatelské jméno a heslo.

- **Čas zahájení údržby (v minutách od půlnoci)**: zadejte čas v minutách (0-1440), kdy se mají spouštět úlohy automatické údržby, například web Windows Update. Výchozí počáteční čas je půlnoc nebo nula ( `0` ) minut. Změňte čas spuštění zadáním počátečního času v minutách od půlnoci. Například pokud chcete, aby údržba začínala 2., zadejte `120` . Pokud chcete, aby údržba začínala 8. odp., zadejte `1200` .

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

- **Zásady vzdělávání**: vyberte, jestli se mají povolit zásady pro vzdělávací prostředí. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Povoleno**: používá doporučené nastavení pro zařízení používaná ve školách, které jsou přísnější.
  - **Zakázáno**: nepoužívají se výchozí a doporučené zásady vzdělávání.

  Další informace o tom, co dělají zásady vzdělávání, najdete v tématu [doporučení konfigurace Windows 10 pro zákazníky ve vzdělávání](https://docs.microsoft.com/education/windows/configure-windows-for-education).

> [!TIP]
> [Nastavení sdíleného nebo hostovaného počítače](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc) (otevře si jiný web docs) je skvělým prostředkem této funkce Windows 10, včetně konceptů a zásad skupiny, které je možné nastavit ve sdíleném režimu.

## <a name="next-steps"></a>Další kroky

- [Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).
- Podívejte se na nastavení pro [Windows holografick pro firmy](shared-user-device-settings-windows-holographic.md).
