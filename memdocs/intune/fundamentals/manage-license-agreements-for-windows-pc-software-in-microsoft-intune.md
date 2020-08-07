---
title: Správa licenčních smluv k softwaru v počítačích se softwarovým klientem Intune
titleSuffix: Microsoft Intune
description: Intune můžete použít ke správě licenčních smluv pro software zakoupený prostřednictvím multilicenční smlouvy s Microsoftem i pro jinak zakoupený software.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/01/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid: c59d8635-3f66-40f5-824a-a71c738e0341
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: 080b7237eb95ba729e4152e646ff8de7466309a0
ms.sourcegitcommit: 4f10625e8d12aec294067a1d9138cbce19707560
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/07/2020
ms.locfileid: "87912273"
---
# <a name="manage-license-agreements-for-windows-pc-software-in-microsoft-intune"></a>Správa licenčních smluv pro software počítačů s Windows v Microsoft Intune

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

Microsoft Intune umožňuje přidávat a spravovat informace o licenční smlouvě pro software zakoupený prostřednictvím multilicenční smlouvy s Microsoftem. To můžete provést i pro software Microsoftu nebo třetího výrobce, zakoupený jiným způsobem. Tyto informace můžete uspořádat do logických skupin.

> [!IMPORTANT]
> Tato funkce slouží pouze ke zvýšení pohodlí. Její přesnost není zaručena. Neměli byste na ni tedy spoléhat při ověřování shody s multilicenční smlouvou s Microsoftem. Microsoft shromážděná data nepoužije k vyšetřování případných přestupků nebo porušení licenčních smluv, které jste s ním uzavřeli.
>
> Licence, které přidáte do Intune, nebudou mít vliv na vaše licenční smlouvy ani na váš nárok na používání softwaru. Když například z Intune odstraníte pár licence/smlouva, neodstraní ani nezruší se tím licenční smlouvy, které jste s Microsoftem uzavřeli.

Akce, které je možné provést v konzole pro správu Intune v pracovním prostoru **Licence**:

- Přidávání a úprava multilicenčních smluv uzavřených s Microsoftem

- Přidávání a úprava licenčních smluv k jinému softwaru

- Správa licencí a skupin

- Porovnávání informací o nárocích, které Intune načte z webu Volume Licensing Service Center (VLSC), s inventářem softwaru od Microsoftu, který Intune detekuje na vámi spravovaných počítačích s Windows.

Můžete taky generovat sestavy, které u softwarových titulů zobrazují počty instalací a licencí. Sestavy licencí vám můžou pomoct vyhodnotit vaši kompletní licenční pozici pro software Microsoftu a software jiných společností.

> [!TIP]
>  Pracovní prostor **Licence** se v konzole správce nezobrazí, pokud nespravujete aspoň jeden počítač s Windows a klientem Intune pro počítače s Windows.

## <a name="add-microsoft-volume-licensing-agreements"></a>Přidání multilicenčních smluv uzavřených s Microsoftem
Multilicenční smlouvy Intune poskytují informace o licenci pro software, který je zakoupený prostřednictvím multilicenčních smluv s Microsoftem. Multilicenční smlouvy s Microsoftem můžete přidat do Intune tak, že zadáte odpovídající páry čísel smluv. Čísla smluv nebo autorizační čísla musí odpovídat správným číslům licencí nebo registrací. Páry čísel smluv získáte při nákupu vašich licenčních smluv na webu [Volume Licensing Service Center (VLSC)](https://go.microsoft.com/fwlink/?LinkID=223842).

1. V [konzole pro správu Microsoft Intune](https://admin.manage.microsoft.com/) vyberte **Licence**.

2. Na stránce **Přidat smlouvy** v části **Zvolit typ smlouvy**vyberte **Multilicenční smlouva**.

3. V části **Přidat podrobnosti smlouvy** vyberte, zda chcete nahrát soubor, nebo zadat údaje ručně.

    - **Odeslání souboru CSV s podrobnostmi o smlouvě**. Klikněte na **Procházet** a vyberte soubor CSV, který chcete nahrát.

        - Soubor může obsahovat dva nebo tři sloupce. Dva jsou pro samotné páry smluv. Tři sloupce použijte, pokud chcete přidat popisný název pro jednotlivé páry smluv.

        - Celkový počet znaků v páru čísel smluv nesmí překročit 16 znaků ASCII.

        - Podporují se jenom znaky ASCII.

        - V názvu smlouvy nejsou povolené následující znaky: **~ ! @ # $ ^ &amp; &#42; ( ) = + [ ] { } \ | ; : ' " &lt; &gt; /**. Název může obsahovat mezery.

        - Název souboru nesmí být delší než 128 znaků.

        - Soubor musí obsahovat aspoň jeden pár smluv a nesmí obsahovat víc než 5 000 párů smluv.

        **Formát souboru**

        Soubor vytvoříte tak, že do obyčejného textového dokumentu přidáte páry smluv. Soubor musí být v některém z následujících formátů podle typu organizace, který jste zaregistrovali na webu VLSC. Na řádku uveďte jednu dvojici čísel smluv.

        - **Zákazníci s programem Open Value:** *číslo smlouvy*, *opakujte číslo smlouvy*, *název smlouvy*

        - **Zákazníci s programem Open:** *autorizační číslo*, *číslo související licence*, *název smlouvy*

        - **Zákazníci s programy Select a Enterprise:** *číslo smlouvy*, *číslo související prováděcí smlouvy*, *název smlouvy*

        Při přidání nové smlouvy zobrazí formulář **Přidat smlouvy** výzvu k vyhledání tohoto souboru.

        Následuje příklad obsahu souboru CSV pro zákazníka s programem Open Value.

        `01-07001, 01-07001, Office agreements`

    - **Ruční zadání údajů o smlouvě**. Zadejte následující údaje a pak do polí **Autorizační číslo nebo číslo smlouvy** a **Číslo licence, prováděcí smlouvy nebo zákazníka** zadejte páry čísel smluv. Po zadání obou čísel klikněte na ikonu **Přidat pár** a uložte vaše čísla, potom můžete případně zadat další pár.

        - **Název smlouvy** – zadejte jedinečný název smlouvy.

            Název smlouvy může mít maximálně 256 znaků a nesmí obsahovat následující znaky: **~ ! @ # $ ^ &amp; &#42; ( ) = + [ ] { } \ | ; : ' " &lt; &gt; /**. Název může obsahovat mezery.

        - **Autorizační číslo nebo číslo smlouvy** – zadejte autorizační číslo nebo číslo smlouvy, které odpovídá licenčnímu páru.

        - **Číslo licence, prováděcí smlouvy nebo zákazníka** – zadejte číslo licence, prováděcí smlouvy nebo zákazníka, které odpovídá licenčnímu páru.

        > [!NOTE]
        > Pokud přidáte několik párů čísel smluv, Intune vytvoří jednu smlouvu s vámi určeným názvem a všechny vámi přidané páry budou součástí této smlouvy.

    Můžete zvolit **+** , že chcete přidat další dvojici čísel smlouvy, nebo **-** Odebrat dvojici čísel smlouvy, kterou jste již zadali.

4. V oblasti **Vybrat skupinu licencí** proveďte některou z těchto akcí:

    - **Přidání smluv do skupiny Nepřiřazené smlouvy**. Tuto možnost vyberte, když nové smlouvy nechcete přidat do skupiny licencí.

    - **Přidání smluv do nové skupiny licencí**. Zadejte název nové skupiny licencí.

    - **Přidání smlouvy do existující skupiny licencí**. V seznamu **Název skupiny** vyberte skupinu licencí, do které chcete smlouvy přidat.

5. Vyberte **OK**.

Zobrazí se seznam **Všechny smlouvy** a služba Intune se připojí k centru Microsoft VLSC, aby ověřila vámi zadané páry čísel smluv.

Pokud chcete po přidání licenčních smluv v Intune aktualizovat informace o multilicencích, klikněte na stránce **Přehled licencí** na **Aktualizovat**. Tato akce načte aktuální informace o licenci z [Microsoft Volume Licensing Service Center (VLSC)](https://go.microsoft.com/fwlink/?LinkId=223842).

> [!IMPORTANT]
> Dokud neaktualizujete informace o multilicencích, můžou se vám v seznamu smluv a informacích o nárocích na stránce **Přehled smluv** zobrazovat rozdílné informace.

Jakmile informace o multilicencích aktualizujete, můžete je v pracovním prostoru **Aplikace** porovnat se zjištěným softwarem od Microsoftu. Můžete taky spustit následující licenční sestavy:

- **Sestavy zakoupených licencí** – zobrazují licencovaný software ve vybraných skupinách licencí a umožňují najít mezery v pokrytí.

- **Sestavy nainstalovaných licencí** – pomáhají zjistit, jestli je pokrytí licenčními smlouvami dostatečné.

> [!NOTE]
> **Název produktu** zobrazený pro všechny multilicenční smlouvy s Microsoftem není **k dispozici**.

## <a name="add-and-edit-other-software-licensing-agreements"></a>Přidávání a úprava licenčních smluv k jinému softwaru
Kromě multilicenčních smluv uzavřených s Microsoftem můžete do Intune přidávat i jiné typy licenčních smluv. Tyto smlouvy můžou zahrnovat software jiného výrobce nebo software Microsoftu zakoupený prostřednictvím prodejce.

> [!IMPORTANT]
> Než přidáte smlouvu, musíte mít v Intune zaregistrovaný aspoň jeden počítač s Windows.  Navíc musí aspoň jeden zaregistrovaný počítač odeslat softwarový balíček, který je provozovatelný v licenci a který použijete k přidání licenční smlouvy.

### <a name="to-add-other-software-agreements"></a>Přidání jiných smluv na software

1. V [konzole pro správu Microsoft Intune](https://admin.manage.microsoft.com/) vyberte **Licence**.

2. Vyberte **Přidat smlouvy** v části **Licenční smlouvy na ostatní software**.

3. Na stránce **Přidat smlouvy** v části **Zvolit typ smlouvy** vyberte **Licenční smlouva na ostatní software**.

4. V části **Přidat podrobnosti smlouvy** zadejte toto:

    - **Agreement name** (povinné) Název smlouvy může mít maximálně 256 znaků a nesmí obsahovat následující znaky: **~ ! @ # $ ^ &amp; &#42; ( ) = + [ ] { } \ | ; : ' " &lt; &gt; /**. Název může obsahovat mezery.

    - **Vydavatel** (povinné) Když začnete psát název vydavatele, služba načte všechny názvy vydavatelů obsahující vámi zadaná písmena. Pokud například zadáte "Soft", služba načte všechny názvy vydavatelů, které jako součást názvu obsahují text "Soft", například "Microsoft" a "Microsoft Research". Názvy vydavatelů se načítají z katalogu Software Asset Catalog. Než budete moct zadat název produktu, musíte vybrat vydavatele.

        > [!IMPORTANT]
        > Společnost, kterou chcete přidat, se v seznamu nemusí zobrazit. Smlouvy na software můžete přidávat jenom pro společnosti, které už figurují v katalogu Software Asset Catalog. Microsoft ale neustále pracuje na přidávání nejoblíbenějších softwarových produktů. Pokud chcete odeslat žádost o přidání společnosti do tohoto seznamu, můžete to udělat na [webu Intune UserVoice](https://microsoftintune.uservoice.com/).

    - **Název produktu** (povinné) Když začnete psát název produktu, služba načte všechny názvy produktů obsahující vámi zadaná písmena. Než budete moct zadat **Název produktu** , musíte určit **Vydavatele**.

    - **Počet licencí** (povinné) Zadejte počet zakoupených licencí.

    - **Počáteční datum licence** Zadejte počáteční datum platnosti licence.

    - **Koncové datum licence** Zadejte koncové datum platnosti licence.

    - **Podrobnosti smlouvy** Volitelně můžete zadat kontaktní informace, registrační kódy a další informace.

5. V oblasti **Vybrat skupinu licencí** proveďte některou z těchto akcí:

    - Pokud nechcete přidávat nové smlouvy do nové nebo existující skupiny licencí, vyberte **Přidat smlouvy do skupiny Nepřiřazené smlouvy** . Smlouvy můžete kdykoli přidat do uživatelem definovaných skupin licencí.

    - Pokud chcete nové smlouvy přidávat do nové skupiny licencí, vyberte **Přidat smlouvy do nové skupiny licencí**. Zobrazí se výzva k zadání názvu nové skupiny licencí.

    - Pokud chcete nové smlouvy přidávat do existující skupiny licencí, vyberte **Přidat smlouvy do existující skupiny licencí**. V seznamu **Název skupiny** vyberte skupinu licencí, do které chcete smlouvy přidat.

6. Vyberte **OK**.

Zobrazí se zobrazení seznamu **Všechny smlouvy**.

## <a name="manage-license-agreements"></a>Správa licenčních smluv
Licenční smlouvy na software se dají přidat do skupin licencí. Skupiny licencí můžete použít k uspořádání licenčních smluv v jednotkách vhodných pro vaši organizaci. Můžete taky odstranit licenční smlouvy, které jste vytvořili v minulosti.

| Úkol | Podrobnosti |
| ---- | ------- |
|   Vytvoření skupiny licencí   |                                                            V pracovním prostoru <strong>Licence</strong> na stránce <strong>Přehled</strong> vyberte v nabídce <strong>Úlohy</strong> možnost <strong>Vytvořit skupinu licencí</strong>. <strong>Poznámka:</strong> Můžete vytvořit maximálně 500 skupin licencí.                                                             |
|   Přejmenování skupiny licencí   |                                                                                                      V pracovním prostoru <strong>Licence</strong> zvolte skupinu licencí a pak v nabídce <strong>Úlohy</strong> klikněte na <strong>Upravit skupinu licencí</strong>.                                                                                                       |
|   Odstranění skupiny licencí   |                                 V pracovním prostoru <strong>Licence</strong> zvolte skupinu licencí a pak v nabídce <strong>Úlohy</strong> klikněte na <strong>Odstranit skupinu licencí</strong>. <strong>Tip:</strong> Všechny licence se z odstraněné skupiny přesunou do skupiny licencí <strong>Nepřiřazené smlouvy</strong>.                                 |
| Odstranění licenční smlouvy | V pracovním prostoru <strong>Licence</strong> zvolte smlouvu a klikněte na <strong>Odstranit</strong>. <strong>Tip:</strong> Pokud chcete po odstranění multilicenčních smluv aktualizovat informace o licencích, klikněte na <strong>Aktualizovat</strong> na stránce <strong>Přehled licencí</strong> nebo na kartě <strong>Obecné</strong> konkrétní skupiny licencí. |

