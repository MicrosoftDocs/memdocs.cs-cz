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
ms.openlocfilehash: 066a7517700d85315a04bec55b6f8254d3e49255
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700391"
---
# <a name="tenant-attach-configmgr-client-details-in-the-admin-center-preview"></a><a name="bkmk_mem"></a> Připojení tenanta: podrobnosti o klientovi nástroje ConfigMgr v centru pro správu (Preview)
<!--6024387, 6374854, 6521921, intune 7552762 pubpreview July 7, 2020-->
*Platí pro: Configuration Manager (Current Branch)*

Microsoft Endpoint Manager je integrované řešení pro správu všech vašich zařízení. Společnost Microsoft spojuje Configuration Manager a Intune s jednou konzolou s názvem **Centrum pro správu Microsoft Endpoint Manager**. Podrobnosti o klientech nástroje ConfigMgr můžete zobrazit, včetně kolekcí, členství ve skupině hranic a informací o klientech v reálném čase pro konkrétní zařízení v centru pro správu.

> [!Important]
> - Tyto informace se vztahují k funkci ve verzi Preview, která se podstatně změnila předtím, než se komerční verze uvolní. Microsoft neposkytuje žádné záruky, výslovné ani předpokládané, týkající se zde uváděných informací.
> - Karta skupiny hranic funguje pouze pro samostatné lokality. Karta bude v centru pro správu prázdná, a to i v případě, že se jedná o jinou než samostatnou primární lokalitu.

## <a name="prerequisites"></a>Předpoklady

- Prostředí, které je [klientovi připojené k nahraným zařízením](device-sync-actions.md).
- Jeden z následujících prohlížečů:
  - Microsoft Edge, verze 77 a novější
  - Google Chrome
- Byl zjištěn uživatelský účet s vyhledáváním [uživatelů služby Azure Active Directory (Azure AD)](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) a [zjišťováním uživatelů služby Active Directory](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
  - To znamená, že uživatelský účet musí být synchronizovaný objekt uživatele v Azure.

## <a name="permissions"></a>Oprávnění

Uživatelský účet potřebuje následující oprávnění:

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