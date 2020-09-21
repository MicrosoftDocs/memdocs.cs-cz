---
title: Připojení klienta – spuštění skriptů (Preview) z centra pro správu
titleSuffix: Configuration Manager
description: Spouštějte skripty pro Configuration Manager zařízení z centra pro správu.
ms.date: 09/18/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 6b6c0a9b-01c6-4e3f-9ae4-45c780b46f8b
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: db3656f98949bfbff2bf31b19b50b0ccb9959845
ms.sourcegitcommit: af4fc4f928203c1bfdb27499a56c91fe0ebae854
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/18/2020
ms.locfileid: "90803275"
---
# <a name="tenant-attach-run-scripts-preview-from-the-admin-center"></a><a name="bkmk_scripts"></a> Připojení tenanta: spustit skripty (Preview) z centra pro správu
<!--CM6234688, IN7220536-->
*Platí pro: Configuration Manager (Current Branch)*

> [!Important]
> - Tyto informace se vztahují k funkci ve verzi Preview, která se podstatně změnila předtím, než se komerční verze uvolní. Microsoft neposkytuje žádné záruky, výslovné ani předpokládané, týkající se zde uváděných informací.

Využijte možnosti Configuration Manager funkce místního spouštění skriptů do centra pro správu Microsoft Endpoint Manager. Umožněte dalším osoby, jako je helpdesk, ke spouštění skriptů PowerShellu z cloudu na základě individuální Configuration Manager spravovaného zařízení v reálném čase. To poskytuje všechny tradiční výhody skriptů PowerShellu, které již byly definovány a schváleny správcem Configuration Manager k tomuto novému prostředí.

:::image type="content" source="./media/6234688-scripts.png" alt-text="Snímek obrazovky se seznamem skriptů v centru pro správu" lightbox="./media/6234688-scripts.png":::


## <a name="prerequisites"></a>Požadavky

Spouštění skriptů z centra pro správu vyžaduje následující položky:

- Všechny předpoklady pro [připojení tenanta: podrobnosti o klientovi nástroje ConfigMgr](client-details.md#prerequisites)
- Minimální verze Configuration Manager 2006 s [KB4580678-tenant připojovat pro Configuration Manager aktuální větev, verze 2006](https://support.microsoft.com/help/4580678) .
   - Všechny lokality v hierarchii musí splňovat požadavek na minimální verzi Configuration Manager.
- Klienti Configuration Manager musí používat nejnovější verzi klienta.
- Aby bylo možné spouštět skripty prostředí PowerShell, musí být v klientovi spuštěný PowerShell verze 3,0 nebo novější.
   - Pokud skript, který spouštíte, obsahuje funkčnost z novější verze prostředí PowerShell, musí klient, na kterém spouštíte skript, používat novější verzi PowerShellu.
- Alespoň jeden skript, který je již vytvořen a schválen v Configuration Manager.
   - Skripty, které mají parametry, nejsou v tuto chvíli podporované a v centru pro správu Microsoft Endpoint Manageru se nezobrazí.
   - V centru pro správu se zobrazí pouze skripty, které jsou již vytvořeny a schváleny. Další informace o schvalování skriptů najdete v tématu [schválení nebo zamítnutí skriptu](../apps/deploy-use/create-deploy-scripts.md#run-script-authors-and-approvers).

## <a name="permissions"></a>Oprávnění

Uživatelský účet potřebuje následující oprávnění:

- Oprávnění **číst** pro **kolekci** zařízení v Configuration Manager.
- Oprávnění **číst prostředek** pro **kolekci** zařízení v Configuration Manager.
- Role **uživatele správce** pro Configuration Manager aplikace mikroslužeb ve službě Azure AD.
  - Přidejte roli ve službě Azure AD z části **podnikové aplikace**  >  **Configuration Manager**  >  **Uživatelé a skupiny**mikroslužeb  >  **Přidat uživatele**. Pokud máte Azure AD Premium, podporují se skupiny.
- Chcete-li použít skripty, musíte být členem příslušné role zabezpečení Configuration Manager. Další informace najdete v tématu [obory zabezpečení pro skripty pro spuštění](../apps/deploy-use/create-deploy-scripts.md#bkmk_ScriptRoles).
- Aby bylo možné spouštět skripty, musí mít účet oprávnění **Run Script** pro **kolekce**.

## <a name="run-a-script"></a>Spuštění skriptu

1. V prohlížeči přejděte na [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. Vyberte **zařízení** a potom **všechna zařízení**.
1. Vyberte zařízení, které se synchronizuje z Configuration Manager prostřednictvím [připojení klienta](device-sync-actions.md).
1. Vyberte **skripty**.
   
   Skripty, které byly nedávno spuštěny přímo zaměřené na zařízení, budou již uvedeny v seznamu. Seznam obsahuje skripty spouštěné z centra pro správu, sady SDK nebo konzoly Configuration Manager. Skripty iniciované z místní konzoly se nebudou zobrazovat na kolekcích, které obsahují zařízení, pokud se skripty neiniciovaly konkrétně pro jednotlivá zařízení.

   :::image type="content" source="./media/6234688-run-script.png" alt-text="Spuštění skriptu z centra pro správu" lightbox="./media/6234688-run-script.png":::

1. Vyberte **Spustit skript**.
   
   Zobrazí se skripty, které jsou k dispozici pro správce na základě oborů přiřazených v Configuration Manager.
1. Vyberte **Spustit** a spusťte skript.

1. Budete upozorněni na spuštění skriptu. Nemusíte čekat, než se skript dokončí, než se do zařízení pošle další.
1. Na hlavní stránce vyberte **aktualizovat** , aby se seznam aktualizoval o poslední stav skriptu a čas posledního spuštění.

1. Po dokončení skriptu můžete vybrat skript pro zobrazení výsledků v podokně **výstup** . Text výstupu skriptu můžete zkopírovat. Vyberte **znovu spustit skript** , pokud chcete, aby byl skript znovu spuštěn.

   :::image type="content" source="./media/6234688-script-output.png" alt-text="Výstup skriptu v centru pro správu" lightbox="./media/6234688-script-output.png":::

## <a name="next-steps"></a>Další kroky

[Instalace aplikace z centra pro správu](applications.md)

[Další informace o zabezpečení PowerShellových skriptů](../apps/deploy-use/learn-script-security.md)