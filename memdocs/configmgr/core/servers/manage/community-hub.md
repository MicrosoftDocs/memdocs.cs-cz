---
title: Komunitní centrum a GitHub
titleSuffix: Configuration Manager
description: Povolení a použití centra komunity v Configuration Manager
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88cead9a-64fe-471e-b57c-81707cefe46c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ae0abdd4a159759037768c8f27d5643bdf612f6e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128167"
---
# <a name="community-hub-and-github"></a>Komunitní centrum a GitHub
<!--3555935, 3555936-->

Komunita správce IT vyvinula spoustu znalostí během let. Místo rezásobování položek, jako jsou skripty a sestavy od začátku, jsme sestavili **Configuration Manager centrum komunity** , kde můžou správci IT sdílet. Využitím práce ostatních můžete ušetřit hodiny práce. Centrum komunity podporuje kreativitu tím, že vytváří další práci a má na vás jiné uživatele. GitHub již obsahuje procesy a nástroje pro sdílení v celém oboru. Centrum komunity teď bude tyto nástroje využívat přímo v konzole Configuration Manager jako základní části pro řízení této nové komunity. V případě počáteční verze se obsah, který je dostupný v centru komunity, nahraje jenom Microsoftem. V budoucnu budou správci IT moci nahrávat obsah vlastním pomocí vlastního účtu GitHub.

> [!Note]  
> Komunitní centrum je volitelná cloudová funkce. Byla poprvé zavedena v červnu 2020. Informace o tom, jak se vyjádřit v komunitním centru, najdete v tématu [volitelné funkce](install-in-console-updates.md#bkmk_options).

## <a name="about-community-hub"></a>O komunitním centru

Centrum komunity podporuje následující objekty:

- Dotazy CMPivot
- Aplikace
- Pořadí úloh
- Položky konfigurace
- Skripty PowerShellu
- Sestavy

## <a name="prerequisites"></a>Požadavky

- Zařízení, které používá konzolu Configuration Manager používané pro přístup k centru komunit, potřebuje následující položky:
   - .NET Framework verze 4,6 nebo vyšší
   - Windows 10 Build 17110 nebo vyšší
      - Windows Server není podporovaný, takže konzola Configuration Manager musí být nainstalovaná na zařízení s Windows 10 oddělená od serveru lokality.
   - Přihlášený uživatelský účet nemůže být předdefinovaným účtem správce.

- [Služba správy](../../../develop/adminservice/set-up.md) v Configuration Manager musí být nastavená a funkční.

- Pokud vaše organizace omezuje síťovou komunikaci s Internetem pomocí brány firewall nebo proxy zařízení, je nutné povolit konzole Configuration Manager přístup k internetovým koncovým bodům. Další informace najdete v tématu [požadavky na přístup k Internetu](../../plan-design/network/internet-endpoints.md#community-hub).

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


## <a name="direct-links-to-community-hub-items"></a><a name="bkmk_deeplink"></a>Přímé odkazy na položky centra komunity
<!--4224406-->
*(Představené ve verzi 2006)* Můžete snadno přejít na položky v uzlu centra komunity konzoly Configuration Manager a odkazovat na ně s přímým odkazem. Záměrem této funkce je usnadnit spolupráci a sdílet odkazy na položky centra komunity se svými kolegy. Tato hluboká propojení jsou aktuálně pouze pro položky v uzlu centra komunity konzoly.

### <a name="prerequisites-for-direct-links"></a>Předpoklady pro přímé odkazy

- Konzola Configuration Manager verze 2006 nebo novější
- Při použití odkazu centra komunity nemůžete použít místní předdefinovaný účet správce.

### <a name="sharing-and-opening-direct-links"></a>Sdílení a otevírání přímých odkazů

Chcete-li sdílet položku:
1. Přejít na položku v centru a vyberte **sdílet**.
1. Vložte zkopírovaný odkaz a nasdílejte ho s ostatními.

Otevření sdíleného odkazu:
1. Klikněte na odkaz z počítače, na kterém je nainstalovaná konzola Configuration Manager.
   - Například pomocí tohoto odkazu můžete sdílet [skript automatické aktualizace hraničního nastavení](https://communityhub.microsoft.com/item/7200) ( `https://communityhub.microsoft.com/item/7200` ).
1. Po zobrazení výzvy vyberte **Spustit centrum komunity** .
1. Konzola se otevře přímo ve skriptu v centru komunity.

## <a name="known-issues"></a><a name="bkmk_known"></a>Známé problémy

### <a name="unable-to-access-community-hub-node-when-running-console-as-a-different-user"></a>Při spuštění konzoly jako jiný uživatel není přístupný uzel centra komunity.
<!--7826897-->
Pokud jste přihlášeni jako uživatel s nižšími právy a chcete otevřít konzolu Configuration Manager **Spustit jako** jiný uživatel, možná nebudete mít přístup k uzlu **komunity komunity** .

### <a name="downloaded-reports-dont-get-removed-from-your-downloads-page"></a>Stažené sestavy se ze stránky stahování neodebraly
<!--7851305-->
Pokud odstraníte staženou sestavu z uzlu sestavy **monitorování**  >  **Reports** , sestava se neodstraní z **centra komunity**  >  **vaše soubory ke stažení** a sestavu nemůžete znovu stáhnout. 

## <a name="next-steps"></a>Další kroky

Další informace o vytváření a používání následujících objektů:

- [Vytváření a spouštění powershellových skriptů](../../../apps/deploy-use/create-deploy-scripts.md)
- [Úvod do vytváření sestav](introduction-to-reporting.md)
- [Vytváření a Správa pořadí úloh](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [Vytvoření a nasazení aplikace](../../../apps/get-started/create-and-deploy-an-application.md)
- [Vytváření položek konfigurace](../../../compliance/deploy-use/create-configuration-items.md)