---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 98e3dd75316acfeaf88715b8f80762b1d6c587c6
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128324"
---
<!--This file is shared by the cmpivot.md file and the cmpivot-changes.md file and contains information on how to run CMPivot standalone. H2s or HJ3s are determined by the article for which the include file is used.-->
<!--3555890, 4619340, 4683130 -->

Počínaje verzí 1906 můžete použít CMPivot jako samostatnou aplikaci. CMPivot Standalone je k dispozici pouze v angličtině. Spusťte CMPivot mimo konzolu Configuration Manager, abyste zobrazili stav zařízení ve vašem prostředí v reálném čase. Tato změna umožňuje používat CMPivot na zařízení bez první instalace konzoly.

> [!Tip]  
> Tato funkce byla poprvé představena ve verzi 1906 jako [funkce předběžné verze](../pre-release-features.md). Od verze 2002 už není k dispozici funkce předběžného vydání.  

Výkon CMPivot můžete sdílet s ostatními osoby, jako jsou Helpdesk nebo správci zabezpečení, kteří nemají na svém počítači nainstalovanou konzolu. Tyto další osoby můžou použít CMPivot k dotazování Configuration Manager společně s jinými nástroji, které tradičně používají. Sdílením těchto dat s bohatou správou můžete společně proaktivně řešit obchodní problémy, které mezi rolemi pracují.

#### <a name="install-cmpivot-standalone"></a>Nainstalovat samostatnou CMPivot

1. Nastavte oprávnění potřebná ke spuštění CMPivot. Další informace najdete v tématu [předpoklady](../cmpivot.md#prerequisites). Pokud jsou oprávnění vhodná pro uživatele, můžete také použít [roli správce zabezpečení](../cmpivot-changes.md#bkmk_cmpivot_secadmin1906) .
2. V následující cestě Najděte instalační program aplikace CMPivot: `<site install path>\tools\CMPivot\CMPivot.msi` . Můžete ji spustit z této cesty nebo ji zkopírovat do jiného umístění.
3. Po spuštění samostatné aplikace CMPivot se zobrazí výzva, abyste se připojili k webu. Zadejte plně kvalifikovaný název domény nebo název počítače buď centrální správy, nebo primárního serveru lokality.
   - Pokaždé, když otevřete samostatnou CMPivot, budete vyzváni k připojení k serveru lokality.
4. Přejděte do kolekce, ve které chcete spustit CMPivot, a pak spusťte dotaz.

   ![Přejděte do kolekce, u které chcete spustit dotaz.](../media/3555890-cmpivot-standalone-browse-collection.png)

> [!NOTE]
> - Kliknutím pravým tlačítkem myši na akce, například **spouštět skripty**, **Průzkumník prostředků**a hledání na webu nejsou k dispozici v CMPivot Standalone. Primární použití samostatného CMPivot se dotazuje nezávisle na Configuration Manager infrastruktuře. Pro usnadnění správců zabezpečení zahrnuje CMPivot Standalone možnost připojit se k programu Microsoft Defender Security Center. <!--5605358-->
> - Počínaje verzí 1910 můžete provádět [vyhodnocení dotazů na místní zařízení pomocí CMPivot Standalone](../cmpivot-changes.md#bkmk_local-eval). <!--3197353--> 