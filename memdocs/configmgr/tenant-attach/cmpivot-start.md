---
title: Spustit CMPivot připojené klienta (Preview)
titleSuffix: Configuration Manager
description: Spusťte CMPivot pro zařízení připojená ke klientovi Microsoft Endpoint Manager.
ms.date: 09/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ae6c0c83-2299-4463-958d-5555e3fcbdbe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: eb30d1ec371060223e6f776497037dc34b81184b
ms.sourcegitcommit: af4fc4f928203c1bfdb27499a56c91fe0ebae854
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/18/2020
ms.locfileid: "90802890"
---
# <a name="tenant-attach-launch-cmpivot-from-the-admin-center-preview"></a><a name="bkmk_cmpivot"></a> Připojení tenanta: spuštění CMPivot z centra pro správu (Preview)

*Platí pro: Configuration Manager (Current Branch)* 

> [!Important]
> - Tyto informace se vztahují k funkci ve verzi Preview, která se podstatně změnila předtím, než se komerční verze uvolní. Microsoft neposkytuje žádné záruky, výslovné ani předpokládané, týkající se zde uváděných informací.

<!--6024392-->
Využijte sílu místních [CMPivot](../core/servers/manage/cmpivot.md) do centra pro správu Microsoft Endpoint Manageru. Umožněte dalším osoby, jako je helpdesk, aby bylo možné iniciovat dotazy v reálném čase z cloudu proti jednotlivým zařízením spravovaným nástrojem ConfigMgr a vracet výsledky zpátky do centra pro správu. To poskytuje všechny tradiční výhody CMPivot, které správcům IT a dalším určeným osoby schopnost rychle vyhodnotit stav zařízení ve svém prostředí a provést akci.

## <a name="prerequisites"></a>Požadavky

Pro použití CMPivot z centra pro správu se vyžadují tyto položky:

- Všechny předpoklady pro [připojení tenanta: podrobnosti o klientovi nástroje ConfigMgr](client-details.md)
- Minimální verze Configuration Manager verze 2002 s [kumulativní aktualizací](https://support.microsoft.com/help/4560496/) a odpovídající verzí konzoly, která je nainstalována.
- Upgradujte cílová zařízení na nejnovější verzi klienta Configuration Manager.  
- Cíloví klienti vyžadují minimálně verzi 4 prostředí PowerShell.
- Aby bylo možné shromažďovat data pro následující entity, vyžadují Cíloví klienti minimálně verzi PowerShellu 5,0:  
  - Správci
  - Připojení
  - Příkazu
  - SMBConfig

## <a name="permissions"></a>Oprávnění

Uživatelský účet potřebuje následující oprávnění:

- Oprávnění **číst** pro **kolekci** zařízení v Configuration Manager.
- Oprávnění **Run CMPivot** pro **kolekci** v Configuration Manager
- Role **uživatele správce** pro Configuration Manager aplikace mikroslužeb ve službě Azure AD.
  - Přidejte roli ve službě Azure AD z části **podnikové aplikace**  >  **Configuration Manager**  >  **Uživatelé a skupiny**mikroslužeb  >  **Přidat uživatele**. Pokud máte Azure AD Premium, podporují se skupiny.


## <a name="launch-cmpivot"></a><a name="bkmk_launch"></a> Spustit CMPivot

1. V prohlížeči přejděte na [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. Vyberte **zařízení** a potom **všechna zařízení**.
1. Vyberte zařízení, které se synchronizuje z Configuration Manager prostřednictvím [připojení klienta](device-sync-actions.md).
1. Vyberte **CMPivot (Preview)**.
1. Zadejte dotaz do podokna skript a pak vyberte **Spustit**.

## <a name="close-cmpivot"></a>Zavřít CMPivot

Pokud chcete zavřít CMPivot a vrátit se k informacím o zařízení, použijte `X` ikonu v pravém horním rohu CMPivot.

   :::image type="content" source="media/6024392-close-cmpivot.png" alt-text="Zavřít CMPivot s ikonou X v centru pro správu Microsoft Endpoint Manageru" lightbox="media/6024392-close-cmpivot.png":::

## <a name="next-steps"></a>Další kroky

- Příklady dotazů naleznete v tématu [CMPivot Sample Scripts](cmpivot-samples-attached.md).
- Informace o entitách, operátorech a funkcích CMPivot najdete v tématu [Přehled využití CMPivot](cmpivot-overview-attached.md).
- [Řešení potíží s CMPivot](troubleshoot-cmpivot.md) pro zařízení odeslaná do centra pro správu