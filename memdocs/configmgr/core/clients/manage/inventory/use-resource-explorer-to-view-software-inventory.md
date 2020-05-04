---
title: Zobrazení inventáře softwaru pomocí Průzkumník prostředků
titleSuffix: Configuration Manager
description: Pomocí Průzkumník prostředků můžete zobrazit inventář softwaru v Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 08905a72b6af6e9eae4d2cef9f4732ef692dc134
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710654"
---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-configuration-manager"></a>Použití Průzkumník prostředků k zobrazení inventáře softwaru v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pomocí Průzkumník prostředků v Configuration Manager můžete zobrazit informace o inventáři softwaru, které byly shromážděny z počítačů ve vaší hierarchii.  

> [!NOTE]  
>  Průzkumník prostředků nezobrazí žádná data inventáře, dokud na klientovi neproběhne cyklus inventarizace softwaru.  

 Průzkumník prostředků poskytuje následující informace o inventáři softwaru:  

-   **Software**:  

    -   **Shromážděné soubory** – soubory, které byly shromážděny během inventarizace softwaru.  

    -   **Podrobnosti o souboru** – soubory, které byly v inventáři během inventáře softwaru, které nejsou přidružené k určitému produktu nebo výrobci.  

    -   **Poslední kontrola softwaru** – datum a čas posledního inventáře softwaru a kolekce souborů pro klientský počítač.  

    -   **Podrobnosti o produktu** – softwarové produkty, které byly v inventáři podle inventáře softwaru, seskupené podle výrobce.  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Spuštění Průzkumníka prostředků z konzoly nástroje Configuration Manager  

1.  V konzole Configuration Manager vyberte **prostředky a kompatibilita** .

2.  V pracovním prostoru **prostředky a kompatibilita** vyberte možnost **zařízení** nebo otevřete jakoukoli kolekci, která zobrazí zařízení.  

3.  Zvolte počítač obsahující inventář, který chcete zobrazit, a potom na kartě **Domů** > skupině **zařízení** zvolte **Spustit** > **Průzkumník prostředků**.

4.  Kliknutím pravým tlačítkem myši na libovolnou položku v pravém podokně Průzkumník prostředkůho okna a výběrem **Možnosti vlastnosti** zobrazíte shromážděné informace o inventáři v čitelnějším formátu.  
 
## <a name="view-and-manage-collected-diagnostic-files"></a><a name="bkmk_diag"> </a> Zobrazit a spravovat shromážděné diagnostické soubory

Počínaje verzí 2002 Configuration Manager pomocí Průzkumník prostředků zobrazit a spravovat soubory shromážděné při použití klientského oznámení ke [shromažďování protokolů klienta](../client-notification.md#client-diagnostics). 

1. V uzlu **zařízení** klikněte pravým tlačítkem myši na zařízení, pro které chcete zobrazit protokoly.
1. Vyberte **Start**a pak **Průzkumník prostředků**.
1. V **Průzkumník prostředků**klikněte na **diagnostické soubory**.
1. V seznamu **diagnostické soubory** vidíte datum shromažďování souborů. Formát názvu protokolů klienta je `Support_<guid>.zip`.
1. Klikněte pravým tlačítkem na soubor zip a vyberte jednu z následujících možností:
    - **Otevřete centrum pro podporu**: spustí [Support Center](../../../support/support-center.md).
    - **Kopírovat**: zkopíruje informace o řádku z Průzkumník prostředků.
    - **Zobrazit soubor**: otevře složku, kde se nachází soubor zip, v Průzkumníkovi souborů.
    - **Uložit**: otevře dialogové okno Uložit soubor pro vybraný soubor.
    - **Export**: uloží Průzkumník prostředků sloupce zobrazené v **diagnostických souborech**.
    - **Refresh**: aktualizuje seznam souborů.
    - **Properties (vlastnosti**): vrátí vlastnosti vybraného souboru. 

[![Zkontrolujte a uložte protokoly klienta z Průzkumník prostředků](./../media/4226618-view-collected-client-logs.png)](./../media/4226618-view-collected-client-logs.png#lightbox)

## <a name="next-steps"></a>Další kroky

K zobrazení shromážděných diagnostických souborů [použijte Support Center](../../../support/support-center.md) .
