---
title: Správa aktualizací
titleSuffix: Configuration Manager
description: Správa aktualizací, která nasazujete a vytváříte pomocí System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: cd64994c-b426-4465-96cd-54b0edc2778d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d2cb1d1547c23357adbaa26e649e4e22a78e0f39
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717808"
---
# <a name="manage-software-updates-in-updates-publisher"></a>Správa aktualizací softwaru v nástroji Updates Publisher

*Platí pro: System Center Updates Publisher*     

V System Center Updates Publisher pomocí **pracovního prostoru aktualizace** spravujte aktualizace softwaru a sady, které jste naimportovali do úložiště.  

Úlohy správy zahrnují duplikování, úpravy a vypršení platnosti aktualizací a sad a přiřazování aktualizací a svazků do publikací. Můžete také exportovat vlastní katalogy pro použití s jinými aktualizacemi instalace aplikace Publisher.

Chcete-li získat aktualizace, které můžete spravovat:
-  [Přidání katalogu aktualizací](updates-publisher-catalogs.md#add-software-update-catalogs) do instalace aktualizací Updates Publisher
-  [Importujte](updates-publisher-catalogs.md#import-updates) aktualizace z tohoto katalogu do svého úložiště.

Můžete také [vytvořit vlastní aktualizace](create-updates-with-updates-publisher.md).



## <a name="create-a-duplicate-of-an-update"></a>Vytvořit duplikát aktualizace
Můžete vytvořit duplikáty nebo kopie aktualizací, které jsou v úložišti. Pak můžete místo změny původní aktualizace upravit kopii. Nemůžete vytvářet kopie sad aktualizací.

Chcete-li vytvořit kopii, vyberte aktualizaci v **pracovním prostoru aktualizace**a klikněte na možnost **Duplikovat**. Kopie aktualizace se zobrazí ve stejném umístění v pracovním prostoru aktualizace s *kopií* přidané do svého názvu.

Nová kopie, kterou vytvoříte, má neplatnou **hodnotu, ale**v opačném případě zachová nastavení původního stavu.

## <a name="edit-updates-and-bundles"></a>Upravit aktualizace a sady
Můžete vybrat aktualizace a sady, které jsou v úložišti, a upravit je.

V **pracovním prostoru aktualizace** vyberte aktualizaci nebo sadu a pak výběrem **Upravit** na kartě **Domů** otevřete Průvodce úpravou. Jednotlivé aktualizace a sady obsahují samostatné, ale úzce související průvodce, které obsahují stejné možnosti jako průvodce [vytvořením aktualizace](create-updates-with-updates-publisher.md#use-the-create-update-wizard) nebo [Vytvoření sady prostředků](create-updates-with-updates-publisher.md#use-the-create-bundle-wizard) .

Při úpravách můžete změnit všechny dostupné podrobnosti o aktualizaci nebo balíčku, aby bylo možné je použít ve vašem prostředí. Můžete například upravit pravidla použitelnosti nebo přednosti nebo změnit jazyk. Můžete také změnit produkt a dodavatele a přesunout aktualizaci nebo sadu do vlastní složky a seskupit aktualizace pro vlastní použití.

## <a name="assign-updates-and-bundles-to-a-publication"></a>Přiřazení aktualizací a sad k publikaci
Můžete vybrat aktualizace a sady v **pracovním prostoru aktualizace** a pak vybrat **přiřadit** na kartě **Domů** na pásu karet a přidat je do publikace. Tím spustíte průvodce **přiřazením aktualizací softwaru** .
-  Informace o tom, jak vybrat a publikovat aktualizace a sady jako jeden úkol, najdete v tématu [publikování aktualizací a sad](#publish-updates-and-bundles-from-the-updates-workspace) .
-  Informace o tom, jak spravovat skupiny aktualizací a sady jako jeden objekt, najdete v tématu [Správa publikací](updates-publisher-publications.md) . Po přiřazení aktualizací k publikaci můžete tuto publikaci spravovat, která zase zahrnuje všechny její přiřazené aktualizace.

Při přiřazování aktualizací k publikaci:

-   Do stejné publikace můžete zahrnout aktualizace a sady, jejichž platnost vypršela, a nevypršela jejich platnost.

-   Zadejte typ publikace:

    -   **Úplný obsah** – tím se publikuje celý obsah aktualizace serveru WSUS. Patří sem metadata a binární soubory aktualizace.

    -   **Jenom metadata** – tím se publikují jenom metadata; binární soubory aktualizace nejsou publikované. Tuto možnost můžete zvolit, pokud chcete shromažďovat data o dodržování předpisů.

    -   **Automaticky** – tento režim je k dispozici pouze v případě, že jste připojeni k Configuration Manager nástroje Updates Publisher (viz možnost [Server ConfigMgr](updates-publisher-options.md#configmgr-server) )

    Pomocí tohoto typu aktualizuje Vydavatel dotazy Configuration Manager k určení, jestli se mají aktualizace nebo sady prostředků publikovat s úplným obsahem nebo jenom s metadaty. Úplný obsah pro aktualizaci je publikovaný pouze v případě, že tato aktualizace splňuje **požadovanou prahovou hodnotu počtu klientů** a **prahovou hodnotu velikosti zdroje balíčku,** která je uvedena na stránce **Server nástroje ConfigMgr** v části aktualizace aplikace Publisher.

-   Vybrat publikaci:

    -   Pokud jste již vytvořili publikaci, kterou chcete použít, použijte **přiřazení aktualizace softwaru pro existující publikace** . Tato možnost není k dispozici, dokud neexistuje alespoň jedna publikace.

    -   Pokud nemáte vhodnou publikaci, použijte **přiřazení aktualizace softwaru k nové publikaci** . Tím se vytvoří nová publikace s názvem, který zadáte.

Po přiřazení aktualizací k publikaci můžete použít **pracovní prostor publikace** k [publikování](updates-publisher-publications.md#publish-publications) nebo [exportu](updates-publisher-publications.md#export-a-publication) publikace jako skupiny.

## <a name="publish-updates-and-bundles-from-the-updates-workspace"></a>Publikování aktualizací a sad z pracovního prostoru aktualizace
Když publikujete aktualizace a sady, vydavatel aktualizací přidá informace o těchto aktualizacích a prostředcích (metadata) a případně binárních souborech aktualizací (úplný obsah) na server aktualizací pro nasazení do zařízení.

Než budete mít možnost publikovat, je nutné nakonfigurovat možnost [server aktualizací](updates-publisher-options.md#update-server) pro aplikaci Updates Publisher. Tuto možnost konfigurace otevřete tak, že přejdete na &gt; **Přehled** **pracovního prostoru aktualizace** a vyberete **Konfigurace služby WSUS a podpisového certifikátu.** Můžete také přejít na stránku server aktualizací v možnosti Vydavatel aktualizace.

Existují dva způsoby, jak publikovat aktualizace a sady:
-   Přímo z pracovního prostoru aktualizace. (Pokud *chcete publikovat aktualizace a sady*, Projděte si následující postup.)
-   Jako [publikace](updates-publisher-publications.md#publish-publications) z pracovního prostoru publikace.  

> [!NOTE]   
> Aktualizace Publisher může publikovat pouze aktualizace 375 megabajtů (MB) a jejich méně.

### <a name="to-publish-updates-and-bundles"></a>Publikování aktualizací a svazků
1.  V **pracovním prostoru aktualizace** vyberte jednu nebo více aktualizací a sad, které chcete publikovat. Pak zvolte možnost **publikovat** z karty **Domů** na pásu karet.

2.  Na stránce **Vybrat** v průvodci **publikováním** vyberte, jak chcete aktualizace publikovat. Možnosti jsou stejné jako u [přiřazení aktualizací](#assign-updates-and-bundles-to-a-publication): **úplný obsah**, **pouze metadata**nebo **Automatické**.

    Můžete se také rozhodnout, že se všechny aktualizace budou podepisovat pomocí nového certifikátu publikování.

3.  Dokončete průvodce.

Pokud publikování neproběhne úspěšně, zobrazí se odkaz na soubor UpdatesPublisher. log, který může poskytovat další informace.

## <a name="export-updates"></a>Exportovat aktualizace
Můžete exportovat aktualizace a sady z úložiště vydavatelů aktualizací a vytvořit vlastní katalog aktualizací. Pak můžete tento katalog [Přidat](updates-publisher-catalogs.md#add-software-update-catalogs) a potom ho [importovat](updates-publisher-catalogs.md#import-updates) do jiné instance nástroje Updates Publisher. (Můžete také [exportovat aktualizace jako publikaci](updates-publisher-publications.md#export-a-publication).)

Pokud chcete exportovat přímo, > v **pracovním prostoru aktualizace aktualizujte****všechny aktualizace softwaru** a vyberte jednu nebo víc aktualizací a sad. Nemůžete exportovat dodavatele nebo složku produktů, ale můžete vybrat složku a pak vybrat aktualizace v této složce pro export.

Když vyberete jednu nebo víc aktualizací, na kartě **Domů** na pásu karet vyberte **exportovat** a pak zadejte cestu a název souboru pro export katalogu.

Budete mít možnost exportovat (zahrnout) závislé aktualizace softwaru.

## <a name="delete-updates-and-bundles"></a>Odstranit aktualizace a sady
Aktualizace a sady aktualizací můžete odstranit, abyste je odebrali z úložiště aplikace Updates Publisher.

V >  **pracovním prostoru aktualizace aktualizujte****všechny aktualizace softwaru** a vyberte jednu nebo více jednotlivých aktualizací. Pak na kartě **Domů** na pásu karet zvolte **Odstranit** .

-   Pokud Váš výběr obsahuje pouze aktualizace nebo sady, které nebyly publikovány nebo jejichž platnost vypršela, zobrazí se výzva k potvrzení odstranění před odebráním.

-   Pokud Váš výběr obsahuje aktualizaci nebo sadu, které byly publikovány a ještě neprošly, zobrazí se vám upozornění. Tyto aktualizace byste měli [vypršet](updates-publisher-publications.md#expire-or-reactivate-updates-and-bundles) a pak tuto změnu publikovat, než je odstraníte z úložiště.  

Pokud odstraníte aktualizaci nebo sadu z dodavatele a pak znovu importujete tento katalog, aktualizace se obnoví do vašeho úložiště.

## <a name="manage-vendor-and-product-folders"></a>Správa složek dodavatel a produkt
Chcete-li zobrazit seznam dodavatelů a produktů pro každého dodavatele, pro které jste naimportovali nebo vytvořili aktualizace, přejít na **Web** > aktualizace**Přehled** > **všech aktualizací softwaru**.

Složky pro dodavatele a produkty se automaticky vytvoří nástrojem Updates Publisher, když použijete Průvodce pro import nebo vytvoření aktualizace nebo sady softwaru. Tyto složky můžete vytvořit také ručně.

-   Složku dodavatele vytvoříte tak, že v navigačním podokně **pracovního prostoru aktualizace**kliknete pravým tlačítkem na **všechny aktualizace softwaru**a pak zvolíte **vytvořit dodavatele**.

-   Složku produktů ve složce dodavatele vytvoříte tak, že kliknete pravým tlačítkem na složku dodavatele a zvolíte **vytvořit produkt**.

Kromě vytváření složek můžete přejmenovat nebo odstranit libovolný dodavatel nebo produktovou složku v úložišti. Provedete to tak, že kliknete pravým tlačítkem na složku a zvolíte požadovanou možnost, **Přejmenovat** nebo **Odstranit**. Odstraněním složky se odstraní všechny aktualizace a sady v této složce a složky produktů z úložiště Publisher Updates.

Mezi dodavatele a složky produktu můžete přesunout aktualizace, včetně do složek, které vytvoříte. Chcete-li přesunout aktualizaci nebo sadu do nové složky, je nutné vybrat a následně **Upravit** aktualizaci nebo sadu prostředků. Potom můžete na stránce **informace** v průvodci úpravami aktualizace přiřadit dodavatele a produkt. Po dokončení průvodce **úpravou aktualizace** se tato změna použije a aktualizace se přesune do nové složky.

## <a name="view-the-xml-of-an-update-or-bundle"></a>Zobrazení souboru XML aktualizace nebo sady prostředků
Můžete vybrat jednu aktualizaci nebo sadu v **pracovním prostoru aktualizace** a potom zvolit **zobrazení** XML pro zobrazení struktury XML této aktualizace. Přímo neexistují žádné možnosti pro úpravu struktury XML.
