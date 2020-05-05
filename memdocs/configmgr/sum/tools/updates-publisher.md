---
title: Aktualizace Publisheru
titleSuffix: Configuration Manager
description: Správa vlastních aktualizací pomocí System Center Updates Publisher
ms.date: 11/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dc1e662eb8eca4740e70743d0971e2d65410f3f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717696"
---
# <a name="system-center-updates-publisher"></a>System Center aktualizuje Publisher 2011

*Platí pro: System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) je samostatný nástroj, který umožňuje nezávislým výrobcům softwaru nebo vývojářům obchodních aplikací spravovat vlastní aktualizace. Tato vlastní Správa aktualizací obsahuje aktualizace, které mají závislosti, jako jsou ovladače a sady aktualizací.

Pomocí nástroje Updates Publisher můžete:

-   Naimportujte aktualizace z externích katalogů (katalogy aktualizací od jiných společností než Microsoft).
-   Upravte definice aktualizací včetně použitelnosti a metadat nasazení.
-   Exportujte aktualizace do externích katalogů.
-   Publikování aktualizací na server aktualizací.

Po publikování aktualizací na server aktualizací můžete použít Configuration Manager k detekci a nasazení těchto aktualizací do spravovaných zařízení.

## <a name="workspaces"></a>Pracovní prostory
Po otevření nástroje Updates Publisher se použije výchozí uzel přehled v *pracovním prostoru aktualizace.*

![Aktualizuje konzolu vydavatele.](media/console1.png)


Aplikace Updates Publisher má čtyři pracovní prostory, které jim usnadňují uspořádání.


**Pracovní prostor aktualizace:** Tento pracovní prostor slouží k [vytváření](create-updates-with-updates-publisher.md) a [správě](manage-updates-with-updates-publisher.md) aktualizací softwaru a sad aktualizací. Tento pracovní prostor zahrnuje přiřazení aktualizací a sad k publikování, publikování a exportu do jiného úložiště pro aktualizace.

**Pracovní prostor publikace:** V tomto pracovním prostoru můžete [spravovat publikace](updates-publisher-publications.md). Publikace je skupina aktualizací, které vytvoříte pro zjednodušení exportu a publikování aktualizací.

Správa publikací zahrnuje publikování aktualizací na serveru, aby je klienti mohli najít a nainstalovat, exportovat aktualizace a sady pro použití jinými aktualizacemi instalace aplikace Publisher nebo úpravou obsahu nebo podrobností publikace.

**Pracovní prostor pravidla:** Tady je místo, kde můžete [Spravovat pravidla použitelnosti](updates-publisher-applicability-rules.md) , která se dají uložit a pak použít s aktualizacemi, které nasadíte. Existují dva typy pravidel:

-   Instalovatelný pravidla – tato pravidla vám pomůžou určit, jestli má klient nainstalovat aktualizaci.
-   Nainstalovaná pravidla – tato pravidla ověřují, jestli je aktualizace už nainstalovaná.

**Pracovní prostor katalogů:** Pomocí tohoto pracovního prostoru můžete přidat a [Spravovat katalogy aktualizací softwaru](updates-publisher-catalogs.md). Tento pracovní prostor zahrnuje import aktualizací softwaru z těchto katalogů do úložiště aplikace Updates.

## <a name="whats-new-in-system-center-updates-publisher"></a>Co je nového v System Center Updates Publisher

>[!NOTE] 
> Nejnovější verzi System Center Updates Publisher vydaná 6. listopadu 2019. Další informace najdete v části [Historie verzí](#release-history) .

K dispozici je nový režim vytváření System Center Updates Publisher, který vám může pomáhat s vytvářením aktualizací. Když povolíte režim vytváření, do úvodní obrazovky se přidá **pracovní prostor kategorie** . Nové tlačítko **Detectoid** je také přidáno do **pracovního prostoru aktualizace** , když je povolen režim vytváření obsahu.

### <a name="to-enable-authoring-mode"></a>Postup povolení režimu vytváření

1. V levém horním rohu konzoly klikněte na kartu **vlastnosti** nástroje **Updates Publisher** a pak zvolte **Možnosti**.
1. Přejít na možnosti **vytváření obsahu** .
1. Zaškrtněte políčko **Povolit režim vytváření obsahu**.

![Povolit režim vytváření pro nástroj Updates Publisher](media/scup-enable-authoring-mode.png)

### <a name="about-the-categories-workspace"></a>O pracovním prostoru kategorie

Pracovní prostor kategorie umožňuje autorům aktualizací uspořádat aktualizace, které patří dohromady. Pokud jste například výrobcem OEM, možná budete chtít uspořádat aktualizace na základě modelů nebo produktů produktu. Můžete definovat více kategorií a podřízených kategorií, ale ne celkových podřízených kategorií, protože jsou omezeny na dvě úrovně.

![Snímek obrazovky pracovního prostoru kategorie](media/scup-categories-workspace.png)

### <a name="assign-an-update-to-a-category"></a>Přiřazení aktualizace ke kategorii

Po vytvoření aktualizace ji můžete přiřadit ke kategorii tak, že ji vyberete a potom kliknete na tlačítko **zařadit do kategorií** . Můžete také kliknout pravým tlačítkem na aktualizaci a vybrat **kategorizovat**.

![Snímek obrazovky s kategorií aktualizace](media/scup-categorize-update.png)

### <a name="about-detectoids"></a>O detectoids

Po povolení režimu vytváření obsahu můžete vytvořit detectoids pro aktualizace. Detectoids jsou užitečné v případě, že máte více aktualizací, které používají stejné pravidlo (nebo sadu pravidel) k určení použitelnosti. V těchto případech byste vytvořili detectoid a přiřadíte ho jako požadavek pro aktualizaci. K vytvořené aktualizaci můžete přiřadit více detectoids.


### <a name="create-a-detectoid"></a>Vytvoření detectoid

1. Otevřete **pracovní prostor aktualizace**.
1. Na pásu karet klikněte na tlačítko **Detectoid** .
1. Při vytváření detectoid postupujte podle pokynů v průvodci.



![Aktualizace požadavků pomocí detectoid](media/scup-detectoid-as-prerequisite.png)

## <a name="release-history"></a>Historie verzí

- [2019 RTW verze 6.0.394.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/SCUP-adds-support-for-update-categories/ba-p/990111). Vydáno v listopadu 6. listopadu 2019
- [Aktualizuje kumulativní verzi 6.0.283.0 z KB4462765](https://support.microsoft.com/help/4462765/update-rollup-for-system-center-updates-publisher). Vydáno 7. září 2018.
- [2017 RTW verze 6.0.276.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/System-Center-Updates-Publisher-adds-support-for-new-OSes/ba-p/274986). Vydáno 26. března 2018.


## <a name="next-steps"></a>Další kroky
Začněte tím, že nejdřív [nainstalujete](install-updates-publisher.md)a pak [nakonfigurujete možnosti](updates-publisher-options.md) pro aplikaci Updates Publisher.
