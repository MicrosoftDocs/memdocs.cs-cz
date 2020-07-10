---
title: Připojení tenanta – podrobnosti o klientovi ConfigMgr (Preview) v centru pro správu
titleSuffix: Configuration Manager
description: Zobrazení podrobností o klientovi pro zařízení Configuration Manager z centra pro správu.
ms.date: 07/08/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 07b24621fbf12fe7a7c513ea2daaed25abca0f4c
ms.sourcegitcommit: 3806a1850813b7a179d703e002bcc5c7eb1cb621
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/09/2020
ms.locfileid: "86210750"
---
# <a name="tenant-attach-configmgr-client-details-in-the-admin-center-preview"></a><a name="bkmk_mem"></a>Připojení tenanta: podrobnosti o klientovi nástroje ConfigMgr v centru pro správu (Preview)
<!--6024387, 6374854, 6521921, intune 7552762 pubpreview July 7, 2020-->

V centru pro správu Microsoft Endpoint Manageru se teď můžete podívat na podrobnosti o klientech nástroje ConfigMgr, včetně kolekcí, členství ve skupině hranic a informací o klientovi v reálném čase pro konkrétní zařízení.

> [!Important]
> - Tyto informace se vztahují k funkci ve verzi Preview, která se podstatně změnila předtím, než se komerční verze uvolní. Microsoft neposkytuje žádné záruky, výslovné ani předpokládané, týkající se zde uváděných informací.
> - Karta skupiny hranic funguje pouze pro samostatné lokality. Karta bude v centru pro správu prázdná, a to i v případě, že se jedná o jinou než samostatnou primární lokalitu.

## <a name="prerequisites"></a>Požadavky

- Prostředí, které je [klientovi připojené k nahraným zařízením](device-sync-actions.md).
- Jeden z následujících prohlížečů:
  - Microsoft Edge, verze 77 a novější
  - Google Chrome
- Byl zjištěn uživatelský účet s vyhledáváním [uživatelů služby Azure Active Directory (Azure AD)](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) a [zjišťováním uživatelů služby Active Directory](/../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
  - To znamená, že uživatelský účet musí být synchronizovaný objekt uživatele v Azure.

## <a name="permissions"></a>Oprávnění

Uživatelský účet potřebuje následující oprávnění:

- Oprávnění **číst** pro **kolekci** zařízení v Configuration Manager.
- Role **uživatele správce** pro Configuration Manager aplikace mikroslužeb ve službě Azure AD.
  - Přidejte roli ve službě Azure AD z části **podnikové aplikace**  >  **Configuration Manager**  >  **Uživatelé a skupiny**mikroslužeb  >  **Přidat uživatele**. Pokud máte Azure AD Premium, podporují se skupiny.

## <a name="view-configmgr-client-details"></a>Zobrazit podrobnosti o klientovi nástroje ConfigMgr

1. V prohlížeči přejděte na [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. Vyberte **zařízení** a potom **všechna zařízení**.
1. Vyberte zařízení, které se synchronizuje z Configuration Manager prostřednictvím [připojení klienta](device-sync-actions.md).
1. Vyberte **Podrobnosti o klientovi (Preview)**.
   - Primární lokalita aktualizuje následující pole jednou za hodinu:
      - **Poslední žádost o zásady**
      - **Poslední aktivní čas**
      - **Poslední bod správy**.

   :::image type="content" source="media/6024387-device-details.png" alt-text="Podrobnosti o klientovi v centru pro správu služby Microsoft Endpoint Manager" lightbox="media/6024387-device-details.png":::

1. Vyberte **kolekce (Preview) a zobrazte** seznam kolekcí klientů.

   :::image type="content" source="media/6024387-device-collections.png" alt-text="Kolekce klientů v centru pro správu služby Microsoft Endpoint Manager" lightbox="media/6024387-device-collections.png":::

## <a name="next-steps"></a>Další kroky

[Řešení potíží s podrobnostmi klienta](troubleshoot-client-details.md)
