---
title: Správa katalogů aktualizací
titleSuffix: Configuration Manager
description: Správa katalogů aktualizací softwaru pro System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 887f8029-1a3a-423c-a9c1-31dc0d693386
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1314e2b4a6adc21b876e6bdbf8b25aa9e4fd3e9a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717766"
---
# <a name="manage-software-update-catalogs-in-updates-publisher"></a>Správa katalogů aktualizací softwaru v nástroji Updates Publisher

*Platí pro: System Center Updates Publisher*

Pomocí **pracovního prostoru** **katalogy** můžete spravovat katalogy aktualizací softwaru. To zahrnuje přidávání nových katalogů, správu stávajících předplatných katalogu a importování informací o aktualizacích z katalogu do úložiště aplikace Updates Publisher.

Katalogy aktualizací softwaru obsahují informace o souvisejících aktualizacích, které jsou vytvářeny jinými organizacemi než Microsoft. Mezi další organizace patří vaše organizace a dodavatelé softwaru třetích stran, kteří zaregistrovali své katalogy v Microsoftu. Registrované katalogy od dodavatelů softwaru se nazývají *katalogy partnerů*. Katalogy, které vytvoříte a které nejsou zaregistrované u Microsoftu, se nazývají katalogy *uživatelů* .

## <a name="add-software-update-catalogs"></a>Přidat katalogy aktualizací softwaru
Aby bylo možné spravovat aktualizace, které obsahuje, je nutné přidat katalog aktualizací do nástroje Updates Publisher. Při přidávání katalogu nástroje Updates Publisher:
-   Vytvoří odběr tohoto katalogu, aby mohl vyhledat aktualizace tohoto katalogu.
-   Přidá katalog do seznamu v okně **katalogy aktualizací softwaru** v **pracovním prostoru katalogy**.  

Informace o každém odebíraném katalogu jsou k dispozici v konzole nástroje. Informace zahrnují adresu URL nebo umístění pro stažení, název společnosti nebo organizace, která katalog vytvořila, a čas posledního importu nebo úprav.

Updates Publisher může automaticky kontrolovat vaše předplatné na změny pokaždé, když se spustí. Tato možnost je nakonfigurovaná jako [pokročilá možnost](updates-publisher-options.md#advanced). Při konfiguraci aplikace Publisher aktualizuje Vydavatel na adresu URL pro stažení nebo informace o umístění pro předplatné a upozorní vás, když dojde ke změnám v katalogu, které byly vytvořeny od posledního importu do úložiště.

Chcete-li ručně vyhledat aktualizaci katalogu, vyberte katalog ze seznamu **katalogy aktualizací softwaru** a zvolte možnost **aktualizovat** na pásu karet.

Kromě přidávání katalogů a zobrazování informací o předplacených katalozích můžete:
-  **Upravte** informace pro katalogy *uživatelů* .
-  **Odstraní** (odebere) katalog z Updates Publisher.
-  **Importujte** aktualizace z katalogu do úložiště aplikace Updates Publisher. Když importujete aktualizace, naimportují se všechny aktualizace obsažené v tomto katalogu. Aktualizace pak můžete zobrazit v pracovním prostoru aktualizace, kde pak můžete vybrat a publikovat aktualizace na server aktualizací.

> [!NOTE]   
> Odstranění katalogu z Updates Publisher vede k aktualizacím v katalogu, který se odebírá z vašeho úložiště. To nemá vliv na aktualizace, které jste publikovali na server aktualizací. Pokud chcete odebrat aktualizace ze serveru aktualizací, které už nejsou ve vašem úložišti, přečtěte si téma [vypršení platnosti neodkazované aktualizace softwaru](updates-publisher-options.md#expire-unreferenced-software-updates).

## <a name="manage-update-catalogs"></a>Správa katalogů aktualizací
Katalogy seznamu, které jste importovali, můžete zobrazit v okně katalogy **aktualizací softwaru** v **pracovním prostoru katalogy**. V tomto pracovním prostoru můžete:

-   **Přidat katalog partnerů:** K vyhledání nových katalogů partnerů použijte jednu z následujících možností:

    -   V konzole nástroje přejít na přehled **pracovní prostor** > **Overview**aktualizace. V okně **Začínáme** vyberte **Přidat katalogy aktualizací partnerských softwaru**.

    -   V konzole nástroje přejdete do části **katalogy pracovní prostor** > **Moje katalogy**. Pak na pásu karet zvolte **Přidat katalogy**.

-   **Přidat katalog uživatelů:** V konzole nástroje přejdete do části **katalogy pracovní prostor** > **Moje katalogy**. Pak na pásu karet zvolte **Přidat katalogy**. Kromě umístění souboru. cab musíte zadat vydavatele, název a popis pro identifikaci katalogu.


-   **Vyhledat aktualizace katalogů:** Vyberte jeden nebo více katalogů a pak na pásu karet vyberte **aktualizovat** .

-   **Úprava katalogu uživatelů:** Vyberte katalog *uživatelů* a pak na pásu karet zvolte **Upravit** . Pak můžete upravit vlastnosti definované uživatelem.

-   **Odstranit katalogy:** Vyberte jeden nebo více katalogů a pak na pásu karet zvolte **Odebrat** . Tím dojde k odebrání katalogu, předplatného a aktualizací z těchto katalogů z úložiště aplikace Updates Publisher.

-   **Přidání aktualizací z katalogu do úložiště**: Pokud chcete průvodce **importem katalogu** spustit, klikněte na pásu karet na tlačítko **importovat** . Další článku najdete v tématu [Import aktualizací](#import-updates) .

## <a name="import-updates"></a>Importovat aktualizace
Při importu katalogu Nástroj Update Manager přidá aktualizace z katalogu do úložiště aplikace Updates Publisher. Po importu aktualizací je můžete publikovat na server aktualizací, abyste je mohli zpřístupnit pro spravovaná zařízení.

### <a name="to-import-updates"></a>Import aktualizací
1. Průvodce **importem katalogu** spustíte tak, že na pásu karet vyberete **importovat** v jednom z následujících pracovních prostorů:

   -   Pracovní prostor katalogů

   -   Pracovní prostor aktualizace

2. Na stránce **typ importu** vyberte jeden nebo více katalogů, které jste přidali do nástroje Updates Publisher, nebo zadejte cestu ke katalogu, který jste ještě nepřidali jako odběr. Kliknutím na tlačítko **Další** zobrazíte obrazovku souhrnu a až budete připraveni, spusťte import kliknutím na tlačítko **Další** .

3. V okně **Upozornění zabezpečení – ověření katalogu** Zkontrolujte certifikát katalogu a až budete připravení, zvolte **přijmout** pro import aktualizací.

   > [!CAUTION]
   > Přijměte aktualizace pouze od vydavatelů, kterým důvěřujete. Aktualizace softwaru od vydavatelů, kteří nejsou důvěryhodní, můžou způsobit poškození klientských počítačů při vyhledávání aktualizací.
   > 
   >  Pokud již nedůvěřujete vydavateli, odeberte tohoto vydavatele ze seznamu důvěryhodných vydavatelů. Pokud chcete získat další informace o přijímání katalogů, klikněte na **Další** v dialogovém okně **Upozornění zabezpečení – ověření katalogu** .

   Pokud se rozhodnete vždy přijmout katalogy od vydavatele, přidá se tento vydavatel do [seznamu důvěryhodných vydavatelů](updates-publisher-options.md#trusted-publishers). Tento seznam můžete zkontrolovat a upravit jako možnost Vydavatel aktualizací.

4. Import přeskočí import aktualizace, když je aktualizace již v úložišti, a jedna z následujících možností je pravdivá:

   -   Aktualizace se od posledního importu nezměnila.

   -   Aktualizace byla upravena a má novou digitální hodnotu hash. Úprava aktualizace zabrání nové aktualizaci, protože by byla původní aktualizace přepsána, protože by došlo k přepsání změn, které jste mohli nasadit.

5. Na stránce **potvrzení** Zkontrolujte výsledky importu.

6. Průvodce dokončíte kliknutím na tlačítko **Zavřít** . Aktualizace pro tento katalog teď můžete zobrazit v pracovním prostoru aktualizace.

## <a name="next-steps"></a>Další kroky
Po importu aktualizací patří mezi běžné akce:
-   [Spravujte aktualizace](manage-updates-with-updates-publisher.md) , přiřaďte je a nasaďte je na server aktualizací.
-   [Vytvořte pravidla použitelnosti](updates-publisher-applicability-rules.md) , která vám pomůžou určit, kdy se aktualizace nasadí na váš server aktualizací.
