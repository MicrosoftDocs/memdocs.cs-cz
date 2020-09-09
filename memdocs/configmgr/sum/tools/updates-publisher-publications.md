---
title: Správa publikací
titleSuffix: Configuration Manager
description: Správa skupin aktualizací softwaru jako publikace pomocí System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: e6c1df1d-7728-4980-9199-bc32cde5439e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e3dedef9ffe785ce7127fc371030cfd990d70e38
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608373"
---
# <a name="manage-publications-in-updates-publisher"></a>Správa publikací v nástroji Updates Publisher

*Platí pro: System Center Updates Publisher*

Publikace můžete použít ke správě skupin aktualizací a sad jako jednoho objektu. To zahrnuje publikování aktualizací management server a export publikace jako skupiny pro použití s jinou instalací nástroje Updates Publisher.

## <a name="create-publications"></a>Vytváření publikací
Publikace jsou vytvořeny dvěma způsoby:

-   Když spravujete aktualizace a sady prostředků v **pracovním prostoru aktualizace**, můžete je [přiřadit](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication) k nové publikaci, která je vytvořena v daném čase.

-   V **pracovním prostoru publikace** můžete použít tlačítko **vytvořit** na kartě **publikace** na pásu karet. Tato metoda umožňuje vytvořit publikaci pro budoucí použití. Když později přiřadíte aktualizace, můžete použít tuto publikaci.

## <a name="rename-a-publication"></a>Přejmenování publikace
Chcete-li přejmenovat publikaci, vyberte publikaci v **pracovním prostoru publikace**a pak na kartě **publikace** na pásu karet zvolte možnost **Upravit**.

## <a name="change-the-publication-type-of-updates-in-a-publication"></a>Změna typu publikace aktualizací v publikaci
V **pracovním prostoru publikace**můžete upravit **Typ publikace** aktualizace a sady, které jsou přiřazeny k publikaci.

1. Vyberte publikaci obsahující aktualizace, které chcete upravit, a potom vyberte jednu nebo více aktualizací nebo sad ze seznamu **všechny &lt; názvy publikování> aktualizace členů** .

2. Potom na kartě **Domů** vyberte jednu z následujících možností. Možnosti, které jsou k dispozici, závisí na typu publikace vybraných aktualizací.

   -   **Automaticky**
   -   **Úplný obsah**
   -   **Pouze metadata**

Po provedení změny může být nutné aktualizovat zobrazení publikace, aby se zobrazily nové hodnoty.

Informace o různých typech publikací najdete v tématu [přiřazení aktualizací a sad do publikace](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication).

> [!TIP]    
> Když nastavíte typ publikace sady, budou všechny aktualizace softwaru v této sadě publikovány s typem publikace dané sady.

## <a name="remove-updates-from-a-publication"></a>Odebrání aktualizací z publikace
Chcete-li odebrat aktualizace nebo sady z publikace, vyberte v **pracovním prostoru publikace** publikaci, kterou chcete upravit, a pak vyberte aktualizace a balíčky, které chcete odebrat. Potom na kartě **Domů** na pásu karet vyberte **Odebrat**.

Po odebrání aktualizací z publikace zůstanou v úložišti Publisher Updates k dispozici.

## <a name="publish-publications"></a>Publikování publikací
Když publikujete aktualizace a sady, vydavatel aktualizací přidá informace o těchto aktualizacích a prostředcích (metadata) a případně binárních souborech aktualizací (úplný obsah) na server aktualizací pro nasazení do zařízení.

Než budete mít možnost publikovat, je nutné nakonfigurovat možnost [server aktualizací](updates-publisher-options.md#update-server) pro aplikaci Updates Publisher. Tuto možnost konfigurace otevřete tak, že přejdete na přehled **pracovního prostoru aktualizace** &gt; **Overview** a vyberete **Konfigurace služby WSUS a podpisového certifikátu.** Můžete také přejít na stránku server aktualizací v možnosti Vydavatel aktualizace.

> [!NOTE]   
> Aktualizace Publisher může publikovat pouze aktualizace 375 megabajtů (MB) a jejich méně.

### <a name="to-publish-a-publication"></a>Publikování publikace

1. Otevřete **pracovní prostor publikace**a vyberte publikaci obsahující skupinu aktualizací a sad, které chcete publikovat nebo exportovat. Pak zvolte možnost **publikovat** z karty **Domů** na pásu karet.

2. Na stránce **Vybrat** v průvodci **publikováním** se můžete rozhodnout podepsat všechny aktualizace pomocí nového certifikátu publikování, ale nemůžete změnit typ publikace.

3. Dokončete průvodce.

   Pokud publikování neproběhne úspěšně, zobrazí se odkaz na soubor UpdatesPublisher. log, který může poskytovat další informace.

## <a name="export-a-publication"></a>Export publikace
Publikaci můžete exportovat z úložiště aplikace Updates Publisher. Tím se vyexportují aktualizace a sady, které jsou přiřazené k této publikaci, a vytvoří se katalog aktualizací. Pak můžete tento katalog [Přidat](updates-publisher-catalogs.md#add-software-update-catalogs) a následně ho [importovat](updates-publisher-catalogs.md#import-updates) do jiné instance aplikace Publisher Updates. Můžete také [exportovat aktualizace](manage-updates-with-updates-publisher.md#export-updates) , které nejsou součástí publikace.

Chcete-li exportovat publikaci, otevřete **pracovní prostor publikace** a vyberte publikaci obsahující aktualizace, které chcete exportovat. V jednom okamžiku můžete vybrat jenom jednu publikaci.

Když je vybraná publikace, na kartě **Domů** na pásu karet vyberte **exportovat** a potom zadejte cestu a název souboru pro export katalogu.

Máte také možnost exportovat (zahrnout) závislé aktualizace softwaru jako součást exportu.

## <a name="delete-a-publication"></a>Odstranění publikace
Chcete-li odstranit publikaci, vyberte publikaci **pracovního prostoru**publikace a pak zvolte možnost **Odstranit** na kartě **publikace** na pásu karet.

Po odebrání publikace z nástroje Updates Publisher zůstanou aktualizace v publikaci k dispozici v úložišti Publisher Updates.

## <a name="expire-or-reactivate-updates-and-bundles"></a>Vyprší nebo znovu aktivovat aktualizace a sady
**Pracovní prostor aktualizace** můžete použít k výběru a vypršení platnosti nebo opětovné aktivaci aktualizací a sad. Můžete vypršet a znovu aktivovat aktualizace a sady, kolikrát zvolíte.

-   Pokud **Chcete vypršení platnosti aktualizací nebo svazků**, v pracovním prostoru aktualizace vyberte jednu nebo víc aktualizací nebo sad, jejichž platnost vypršela, a pak zvolte **vypršení platnosti** na kartě **Domů** . Dokud nedokončíte publikování aktualizace nebo sady jako Configuration Manager, můžete ji znovu aktivovat.

    Než budete moct odebrat (odstranit) vlastní aktualizaci nebo sadu z Configuration Manager, musíte ji vypršet a pak pro Configuration Manager publikovat stav s vypršenou platností. Po vypršení platnosti aktualizací nebo sad v Configuration Manager už nemůžete nasadit nebo znovu aktivovat aktualizaci nebo sadu prostředků.

-   **Chcete-li znovu aktivovat aktualizace nebo sady prostředků**, vyberte v pracovním prostoru aktualizace jednu nebo více aktualizací, jejichž platnost vypršela, a pak zvolte možnost **znovu aktivovat** na kartě **Domů** na pásu karet. Pokud byla dříve publikována aktualizace s vypršenou platností Configuration Manager, nebudete ji moci znovu aktivovat.
