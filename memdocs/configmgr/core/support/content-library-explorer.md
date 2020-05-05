---
title: Průzkumník knihovny obsahu
titleSuffix: Configuration Manager
description: Pomocí Průzkumníka knihoven obsahu můžete zobrazit a řešit potíže s knihovnou obsahu v Configuration Manager distribučním bodu.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 691896d9-ec0f-461f-a3f2-40378ebd3121
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: aa92fb143815faf693f6c2629c3f6436546c5080
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078528"
---
# <a name="content-library-explorer"></a>Průzkumník knihovny obsahu

*Platí pro: Configuration Manager (Current Branch)*

Průzkumník knihovny obsahu je jedním z [nástrojů Configuration Manager](tools.md). Nástroj použijte pro následující činnosti:  

- Prozkoumat knihovnu obsahu v určitém distribučním bodě  

- Řešení potíží s knihovnou obsahu  

- Kopírovat balíčky, obsah, složky a soubory z knihovny obsahu  

- Znovu distribuovat balíčky do distribučního bodu  

- Ověřit balíčky ve vzdálených distribučních bodech  



## <a name="requirements"></a>Požadavky

- Spusťte nástroj pomocí účtu, který má přístup správce k:  

    - Cílový distribuční bod  

    - Zprostředkovatel rozhraní WMI na serveru lokality  

    - Poskytovatel Configuration Manager  

- Pouze **správce s úplnými** oprávněními a **analytik jen pro čtení** mají dostatečná oprávnění k zobrazení všech informací z tohoto nástroje.  

    - Další role, jako je například **správce aplikace**, mohou zobrazit částečné informace. Další informace najdete v tématu [zakázané balíčky](#bkmk_disabled-packages).  

    - **Analytik s oprávněními jen pro čtení** nemůže znovu distribuovat balíčky z tohoto nástroje.  

- Spusťte nástroj z libovolného počítače, pokud se může připojit k:  

    - Cílový distribuční bod  

    - Server primární lokality  

    - Poskytovatel Configuration Manager  

- Pokud je distribuční bod společně umístěn na serveru lokality, je stále nutné mít přístup pro správu k serveru lokality.  



## <a name="usage"></a>Využití 

Když spustíte **ContentLibraryExplorer. exe**, zadejte plně kvalifikovaný název domény (FQDN) cílového distribučního bodu. Pak se připojí k distribučnímu bodu. Pokud je distribuční bod součástí sekundární lokality, zobrazí se výzva k zadání plně kvalifikovaného názvu domény serveru primární lokality a kódu primární lokality.

V levém podokně zobrazte balíčky distribuované do tohoto distribučního bodu. Rozbalte balíčky a prozkoumejte jejich strukturu složek. Tato struktura odpovídá struktuře složky, ze které jste balíček vytvořili.

Když vyberete složku, zobrazí se v pravém podokně všechny soubory ve složce. Toto zobrazení obsahuje následující informace: 
- Název souboru
- Velikost souboru
- Která jednotka je zapnutá
- Další balíčky, které používají stejný soubor na jednotce
- Kdy se soubor naposledy změnil v distribučním bodě

Nástroj se také připojí k poskytovateli Configuration Manager. Toto připojení určuje, které balíčky jsou distribuovány do distribučního bodu a zda jsou ve skutečnosti v knihovně obsahu distribučního bodu. Například balíček, který čeká na distribuci, ještě nemusí existovat v knihovně obsahu. Takový balíček se v nástroji jeví jako "čeká na vyřízení" a pro tento balíček nejsou povolené žádné akce.


### <a name="disabled-packages"></a><a name="bkmk_disabled-packages"></a>Zakázané balíčky

Některé balíčky jsou k dispozici v distribučním bodě, ale nejsou viditelné v konzole Configuration Manager. Tyto balíčky jsou označené hvězdičkou (\*). U těchto balíčků se nedají provádět žádné akce. Jiné balíčky mohou být označeny hvězdičkou a akce budou zakázány. 

Pro zakázané balíčky existují tři hlavní příčiny:  

- Balíček je Configuration Manager upgrade klienta. Tento balíček obsahuje "CCMSetup. exe".  

- Váš uživatelský účet nemá k balíčku přístup, pravděpodobně v důsledku správy na základě rolí. Například role **Autor aplikace** v konzole nástroje nevidí balíčky ovladačů, takže všechny balíčky ovladačů v distribučním bodě jsou označeny jako zakázané.  

- Balíček je osamocený v distribučním bodě.  


### <a name="validate-packages"></a>Ověřit balíčky

Ověří balíčky pomocí ověření **balíčku** > **Validate** na panelu nástrojů. Nejdřív vyberte uzel balíčku v levém podokně nevybírejte obsah ani složku. Nástroj se připojí k poskytovateli rozhraní WMI v distribučním bodě pro tuto akci. Při spuštění nástroje jsou balíčky, u kterých chybí jeden nebo více obsahu, označeny jako neplatné. Při ověřování balíčku se odhalí chybějící obsah. Pokud je k dispozici veškerý obsah, ale data jsou poškozena, ověřování detekuje poškození.


### <a name="redistribute-packages"></a>Znovu distribuovat balíčky

Znovu distribuujte balíčky pomocí**Redistribuce** **balíčku** > na panelu nástrojů. Nejprve v levém podokně vyberte uzel balíčku. Tato akce vyžaduje oprávnění k opětovné distribuci balíčků.


### <a name="other-actions"></a>Další akce

Pomocí **Úpravy** > **Kopírovat** zkopírujte balíčky, obsah, složky a soubory z knihovny obsahu do zadané složky. Nemůžete zkopírovat samotnou knihovnu obsahu. Vyberte více než jeden soubor, ale nelze vybrat více složek.

Vyhledejte balíčky pomocí **Úpravy** > **Najít balíček**. Tato akce vyhledá váš dotaz v názvu balíčku a ID balíčku.



## <a name="limitations"></a>Omezení

- Nástroj nemůže přímo manipulovat s knihovnou obsahu. Změny v knihovně obsahu mohou způsobit nefunkčnost.  

- Nástroj může znovu distribuovat balíčky, ale pouze do cílového distribučního bodu.  

- Při hledání distribučního bodu se serverem lokality nelze ověřit data balíčku. Místo toho použijte konzolu Configuration Manager. Nástroj tento balíček stále kontroluje, aby se zajistilo, že je přítomen veškerý obsah, i když ne nutně nezůstane beze změny.  

- Pomocí tohoto nástroje nelze odstranit obsah.



## <a name="see-also"></a>Viz také

- [Základní koncepty správy obsahu](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [Knihovna obsahu](../plan-design/hierarchy/the-content-library.md)
