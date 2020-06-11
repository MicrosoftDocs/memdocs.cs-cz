---
title: Komunitní centrum a GitHub
titleSuffix: Configuration Manager
description: Povolení a použití centra komunity v Configuration Manager
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88cead9a-64fe-471e-b57c-81707cefe46c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 606c9490e56d932176b17eef95ea4ed0c956770e
ms.sourcegitcommit: a198e4efa52b16f87049853b9d8c9854fd9fa057
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/11/2020
ms.locfileid: "84680417"
---
# <a name="community-hub-and-github"></a>Komunitní centrum a GitHub
<!--3555935, 3555936-->

Komunita správce IT vyvinula spoustu znalostí během let. Místo rezásobování položek, jako jsou skripty a sestavy od začátku, jsme sestavili **Configuration Manager centrum komunity** , kde můžou správci IT sdílet. Využitím práce ostatních můžete ušetřit hodiny práce. Centrum komunity podporuje kreativitu tím, že vytváří další práci a má na vás jiné uživatele. GitHub již obsahuje procesy a nástroje pro sdílení v celém oboru. Centrum komunity teď bude tyto nástroje využívat přímo v konzole Configuration Manager jako základní části pro řízení této nové komunity. V případě počáteční verze se obsah, který je dostupný v centru komunity, nahraje jenom Microsoftem. V budoucnu budou správci IT moci nahrávat obsah vlastním pomocí vlastního účtu GitHub.

> [!Note]  
> Komunitní centrum je volitelná cloudová funkce. Byla poprvé zavedena v červnu 2020. Informace o tom, jak se vyjádřit v komunitním centru, najdete v tématu [volitelné funkce](install-in-console-updates.md#bkmk_options).

## <a name="about-community-hub"></a>O komunitním centru

Centrum komunity podporuje následující objekty:
- Skripty PowerShellu
- Sestavy
- Pořadí úloh
- Aplikace
- Položky konfigurace  

## <a name="prerequisites"></a>Požadavky

- Zařízení, které používá konzolu Configuration Manager používané pro přístup k centru komunit, potřebuje následující položky:
   - .NET Framework verze 4,6 nebo vyšší
   - Windows 10 Build 17110 nebo vyšší
      - Windows Server není podporovaný, takže konzola Configuration Manager musí být nainstalovaná na zařízení s Windows 10 oddělená od serveru lokality.
   - Přihlášený uživatelský účet nemůže být předdefinovaným účtem správce.

- Chcete-li stáhnout sestavy, je třeba zapnout možnost **použít Configuration Manager vygenerované certifikáty pro systémy lokality protokolu HTTP** v lokalitě, do které provádíte import. Další informace najdete v tématu [Rozšířená http](/sccm/core/plan-design/hierarchy/enhanced-http).
   1. Přejít na **Administration**  >  **stránku Správa konfigurace lokality**  >  **lokality**.
   1. Vyberte lokalitu a na pásu karet zvolte **vlastnosti** .
   1. Na kartě **zabezpečení komunikace** vyberte možnost **použití Configuration Manager generovaných certifikátů pro systémy lokality http**.

## <a name="permissions"></a>Oprávnění

- Import skriptu: oprávnění **Create** pro třídu **SMS_Scripts** .
- Import sestavy: role zabezpečení správce s úplnými oprávněními.


## <a name="use-the-community-hub"></a>Použití centra komunity

1. V pracovním prostoru **komunity** přejdete do uzlu **Centrum komunity** .
1. Vyberte položku, kterou chcete stáhnout.
1. Pro stažení objektů z centra a jejich importování do lokality budete potřebovat příslušná oprávnění ve vaší Configuration Manager lokalitě.
    - Import skriptu: oprávnění **Create** pro třídu SMS_Scripts.
    - Import sestavy: role zabezpečení správce s úplnými oprávněními.
1. Stažené sestavy jsou nasazeny do složky sestav s názvem **centrum** v bodu služby Reporting Services. Stažené skripty lze zobrazit v uzlu **spustit skripty** .
1. Kliknutím na **soubory ke stažení** z uzlu **komunity komunity** zobrazíte všechny položky stažené z centra vaší organizací.

[![Všechny položky stažené z centra komunity](./media/3555935-community-hub-downloads.png)](./media/3555935-community-hub-downloads.png#lightbox)


## <a name="next-steps"></a>Další kroky

Další informace o vytváření a používání následujících objektů:

- [Vytváření a spouštění powershellových skriptů](../../../apps/deploy-use/create-deploy-scripts.md)
- [Úvod do vytváření sestav](introduction-to-reporting.md)
- [Vytváření a Správa pořadí úloh](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [Vytvoření a nasazení aplikace](../../../apps/get-started/create-and-deploy-an-application.md)
- [Vytváření položek konfigurace](../../../compliance/deploy-use/create-configuration-items.md)