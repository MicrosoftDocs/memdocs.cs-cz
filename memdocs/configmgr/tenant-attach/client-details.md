---
title: Připojení tenanta – podrobnosti o klientovi ConfigMgr (Preview) v centru pro správu
titleSuffix: Configuration Manager
description: Zobrazení podrobností o klientovi pro zařízení Configuration Manager z centra pro správu.
ms.date: 09/09/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: fbe75e34465335450f3a09680b68a78520451bd1
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643393"
---
# <a name="tenant-attach-configmgr-client-details-in-the-admin-center-preview"></a><a name="bkmk_mem"></a> Připojení tenanta: podrobnosti o klientovi nástroje ConfigMgr v centru pro správu (Preview)
<!--6024387, 6374854, 6521921, intune 7552762 pubpreview July 7, 2020-->
*Platí pro: Configuration Manager (Current Branch)*

Microsoft Endpoint Manager je integrované řešení pro správu všech vašich zařízení. Společnost Microsoft spojuje Configuration Manager a Intune s jednou konzolou s názvem **Centrum pro správu Microsoft Endpoint Manager**. Podrobnosti o klientech nástroje ConfigMgr můžete zobrazit, včetně kolekcí, členství ve skupině hranic a informací o klientech v reálném čase pro konkrétní zařízení v centru pro správu.

> [!Important]
> - Tyto informace se vztahují k funkci ve verzi Preview, která se podstatně změnila předtím, než se komerční verze uvolní. Microsoft neposkytuje žádné záruky, výslovné ani předpokládané, týkající se zde uváděných informací.
> - Karta skupiny hranic funguje pouze pro samostatné lokality. Karta bude v centru pro správu prázdná, a to i v případě, že se jedná o jinou než samostatnou primární lokalitu.

## <a name="prerequisites"></a>Požadavky

- Prostředí, které je [klientovi připojené k nahraným zařízením](device-sync-actions.md).
- Jeden z následujících prohlížečů:
  - Microsoft Edge, verze 77 a novější
  - Google Chrome
- Uživatelský účet, který přistupuje k funkcím připojení tenanta v **centru pro správu Microsoft Endpoint Manageru** , se musí vyhodnotit pomocí [zjišťování uživatelů služby Azure Active Directory (Azure AD)](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) i [zjišťování uživatelů služby Active Directory](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
  - To znamená, že uživatelský účet musí být synchronizovaný objekt uživatele v Azure.

## <a name="permissions"></a>Oprávnění

Uživatelský účet přistupující k funkcím pro připojení klienta v centru pro správu Microsoft Endpoint Manageru potřebuje následující oprávnění:

- Oprávnění **číst** pro **kolekci** zařízení v Configuration Manager.
- Role **uživatele správce** pro Configuration Manager aplikace mikroslužeb ve službě Azure AD.
  - Přidejte roli ve službě Azure AD z části **podnikové aplikace**  >  **Configuration Manager**  >  **Uživatelé a skupiny**mikroslužeb  >  **Přidat uživatele**. Pokud máte Azure AD Premium, podporují se skupiny.
   > [!TIP]
   > [Role Správce aplikací v Azure AD](/azure/active-directory/users-groups-roles/directory-assign-admin-roles) má dostatečná oprávnění pro přidání uživatele do role **uživatele správce** aplikace.

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

1. Vyberte **kolekce (Preview) a zobrazte** seznam kolekcí klientů. <!--6024390-->

   :::image type="content" source="media/6024387-device-collections.png" alt-text="Kolekce klientů v centru pro správu služby Microsoft Endpoint Manager" lightbox="media/6024387-device-collections.png":::

## <a name="next-steps"></a>Další kroky

[Řešení potíží s podrobnostmi klienta](troubleshoot-client-details.md)
