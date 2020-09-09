---
title: Klient – připojení – Průzkumník prostředků – centrum pro správu (Preview)
titleSuffix: Configuration Manager
description: Zobrazení inventáře hardwaru pro nahraná Configuration Manager zařízení pomocí Průzkumníka prostředků v centru pro správu.
ms.date: 09/08/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 963dda08-87b8-4e80-90a7-25625efe8861
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: fabd91df79945580005e1c56893e78dec00d0202
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564290"
---
# <a name="tenant-attach-resource-explorer-in-the-admin-center-preview"></a><a name="bkmk_hinv"></a> Připojení tenanta: Průzkumník prostředků v centru pro správu (Preview)
<!--cm 6479284 in 7220536 pubpreview Sept 8, 2020-->
*Platí pro: Configuration Manager (Current Branch)*

> [!Important]
> - Tyto informace se vztahují k funkci ve verzi Preview, která se podstatně změnila předtím, než se komerční verze uvolní. Microsoft neposkytuje žádné záruky, výslovné ani předpokládané, týkající se zde uváděných informací.

Microsoft Endpoint Manager je integrované řešení pro správu všech vašich zařízení. Společnost Microsoft spojuje Configuration Manager a Intune s jednou konzolou s názvem **Centrum pro správu Microsoft Endpoint Manager**. V centru pro správu Microsoft Endpoint Management můžete zobrazit inventář hardwaru pro nahraná Configuration Manager zařízení pomocí Průzkumníka prostředků.

   :::image type="content" source="media/6479284-resource-explorer.png" alt-text="Průzkumník prostředků v centru pro správu Microsoft Endpoint Manageru" lightbox="media/6479284-resource-explorer.png":::

## <a name="prerequisites"></a>Požadavky

Pro použití Průzkumníka prostředků z centra pro správu se vyžadují tyto položky:

- Všechny předpoklady pro [připojení tenanta: podrobnosti o klientovi nástroje ConfigMgr](client-details.md).
- Minimálně verze Configuration Manager 2006 a odpovídající verze nainstalované konzoly.
- Upgradujte cílová zařízení na nejnovější verzi klienta Configuration Manager.

## <a name="permissions"></a>Oprávnění

Uživatelský účet potřebuje následující oprávnění:

- Oprávnění **číst** pro **kolekci** zařízení v Configuration Manager.
- Oprávnění **číst prostředek** pro **kolekci** zařízení v Configuration Manager.
- Role **uživatele správce** pro Configuration Manager aplikace mikroslužeb ve službě Azure AD.
  - Přidejte roli ve službě Azure AD z části **podnikové aplikace**  >  **Configuration Manager**  >  **Uživatelé a skupiny**mikroslužeb  >  **Přidat uživatele**. Pokud máte Azure AD Premium, podporují se skupiny.

## <a name="launch-resource-explorer"></a><a name="bkmk_launch"></a> Spustit Průzkumníka prostředků

1. V prohlížeči přejděte na [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. Vyberte **zařízení** a potom **všechna zařízení**.
1. Vyberte zařízení, které se synchronizuje z Configuration Manager prostřednictvím [připojení klienta](device-sync-actions.md).
1. Vyberte možnost **Průzkumník prostředků (Preview)** k zobrazení inventáře hardwaru.
1. Vyhledejte nebo vyberte třídu pro načtení informací z klienta.

   :::image type="content" source="media/6479284-resource-explorer-details.png" alt-text="Průzkumník prostředků se zvolenou třídou základní desky" lightbox="media/6479284-resource-explorer-details.png":::

## <a name="close-resource-explorer"></a>Zavřít Průzkumníka prostředků

Chcete-li zavřít Průzkumníka prostředků a vrátit se k informacím o zařízení, použijte `X` ikonu v pravém horním rohu Průzkumníka prostředků.

   :::image type="content" source="media/6479284-close-resource-explorer.png" alt-text="Zavření Průzkumníka prostředků pomocí ikony x v centru pro správu Microsoft Endpoint Manageru" lightbox="media/6479284-close-resource-explorer.png":::

## <a name="next-steps"></a>Další kroky

[Řešení potíží s Průzkumníkem prostředků](troubleshoot-resource-explorer.md)