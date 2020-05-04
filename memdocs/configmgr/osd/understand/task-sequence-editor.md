---
title: Použití editoru pořadí úloh
titleSuffix: Configuration Manager
description: Vysvětlení použití editoru pořadí úloh v konzole Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a4e8bb56-ee85-49fd-8b1c-c8f513cec671
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2047ae9e276ac94b633d1dc30814ed641cd34d03
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711424"
---
# <a name="use-the-task-sequence-editor"></a>Použití editoru pořadí úloh

*Platí pro: Configuration Manager (Current Branch)*

Pomocí **editoru pořadí úloh**upravte pořadí úloh v konzole Configuration Manager. Editor použijte k těmto akcím:  

- Otevření zobrazení pořadí úkolů jen pro čtení

- Přidat nebo odebrat kroky z pořadí úloh  

- Změna pořadí kroků pořadí úloh  

- Přidat nebo odebrat skupiny kroků  

- Kopírování a vkládání kroků mezi pořadím úkolů

- Nastavení možností kroku, například zda pořadí úloh pokračuje v případě výskytu chyby  

- Přidání podmínek do kroků a skupin pořadí úkolů  

- Kopírování a vkládání podmínek mezi kroky v pořadí úkolů

- Pokud chcete rychle najít kroky, prohledejte pořadí úkolů.

Než budete moct upravit pořadí úkolů, musíte ho vytvořit. Další informace najdete v tématu [Správa a vytváření pořadí úkolů](../deploy-use/manage-task-sequences-to-automate-tasks.md).

## <a name="about-the-task-sequence-editor"></a>O editoru pořadí úloh

Editor pořadí úkolů zahrnuje následující součásti:

![Snímek obrazovky s komentovaným ukázkovým oknem Editor pořadí úloh](media/task-sequence-editor.png)

<!-- The following numbered steps correspond to annotations in the above screenshot. Don't change the step numbers without also revising the image! -->

1. Název pořadí úloh
2. Nápovědě. Další informace najdete v tématu [hledání](#bkmk_search).
3. **Vlastnosti** pro vybranou skupinu nebo krok v sekvenci

    Další informace o vlastnostech a možnostech konkrétního kroku najdete v tématu [o krocích pořadí úkolů](task-sequence-steps.md).

4. **Možnosti** pro vybranou skupinu nebo krok v sekvenci

    Další informace o obecných možnostech všech kroků nebo možnostech konkrétního kroku najdete v tématu [o krocích pořadí úkolů](task-sequence-steps.md).

    Další informace o tom, jak konfigurovat podmínky, najdete v tématu [podmínky](#bkmk_conditions).

5. **Přidat** skupinu nebo kroky
6. **Odebrání** skupiny nebo kroků
7. Sbalit všechny skupiny nebo rozbalit všechny skupiny
8. Přesunutí pozice skupiny nebo kroku v sekvenci (nahoru, dolů)
9. Pořadí úkolů:
    - Podívejte se na pořadí kroků a skupin.
    - Rozbalí nebo sbalí skupinu.
    - Když zapnete krok nebo skupinu podle svých **možností**, bude v sekvenci šedé.
    - Pokud dojde k potížím s krokem, změní se ikona kroku na červenou chybu. Například chybí požadovaná hodnota.
10. **OK**: Uložit a zavřít
11. **Zrušit**: zavřít bez uložení změn
12. **Použít**: Uložit změny a ponechat otevřené

Editor pořadí úloh lze změnit pomocí standardních ovládacích prvků systému Windows. Chcete-li změnit velikost šířek dvou hlavních podoken, pomocí myši vyberte pruh mezi pořadím úkolů a vlastností kroku a pak jej přetáhněte doleva nebo doprava.

## <a name="view-a-task-sequence"></a><a name="bkmk_view"></a>Zobrazení pořadí úkolů

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a potom vyberte uzel **pořadí úloh** .  

2. V seznamu **pořadí úloh** vyberte pořadí úloh, které chcete zobrazit.  

3. Na kartě **Domů** na pásu karet ve skupině **pořadí úloh** vyberte **Zobrazit**.

    > [!TIP]
    > Tato akce je výchozí. Pokud dvakrát kliknete na pořadí úkolů, **zobrazí** se pořadí úkolů.

Tato akce otevře Editor pořadí úloh v režimu jen pro čtení. V tomto režimu můžete provádět následující akce:

- Zobrazit všechny skupiny, kroky, vlastnosti a možnosti
- Rozbalení a sbalení skupin
- Hledání v pořadí úkolů
- Změna velikosti okna editoru

V tomto režimu jen pro čtení nemůžete dělat žádné změny, včetně kopírování kroku nebo podmínky. Tato akce také nezamkne pořadí úkolů pro úpravy. Další informace o těchto zámkech najdete v tématu o [uvolnění zámku pro úpravy pořadí úkolů](#bkmk_sedo).

Chcete-li provést změny v pořadí úkolů, zavřete Editor pořadí úloh, který jste otevřeli v režimu jen pro čtení. Pak [upravte](#bkmk_edit) pořadí úkolů.

> [!NOTE]  
> Když zobrazíte nebo upravíte pořadí úkolů vytvořené Průvodcem vytvořením pořadí úloh, název kroku může být akce nebo typ kroku. Může se například zobrazit krok s názvem partition disk 0, který je akcí pro krok typu [Format a partition disk](task-sequence-steps.md#BKMK_FormatandPartitionDisk). Všechny kroky pořadí úloh jsou dokumentovány podle jejich *typu*, nikoli nutně podle názvu kroku, který Editor zobrazuje.  

## <a name="edit-a-task-sequence"></a><a name="bkmk_edit"></a>Úprava pořadí úloh

Chcete-li upravit existující pořadí úloh, použijte následující postup:  

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a potom vyberte uzel **pořadí úloh** .  

2. V seznamu **Pořadí úloh** vyberte pořadí úloh, které chcete upravit.  

3. Na kartě **Domů** na pásu karet ve skupině **pořadí úloh** vyberte **Upravit**. Pak proveďte některou z následujících akcí:  

    - **Přidejte krok**: vyberte **Přidat**, vyberte kategorii a pak vyberte krok, který chcete přidat. Například pro přidání kroku [Spustit příkazový řádek](task-sequence-steps.md#BKMK_RunCommandLine) : vyberte **Přidat**, zvolte kategorii **Obecné** a pak vyberte **Spustit příkazový řádek**. Tato akce přidá krok za aktuálně vybraný krok.

    - **Přidejte skupinu**: vyberte **Přidat**a pak zvolte **Nová skupina**. Po přidání skupiny přidejte do ní kroky.  

    - **Změňte pořadí**: Vyberte krok nebo skupinu, u kterých chcete změnit pořadí. Pak použijte ikony **Přesunout nahoru** nebo **Přesunout dolů** . Současně nelze přesunout více než jeden krok nebo skupinu. Tyto akce jsou také k dispozici, když kliknete pravým tlačítkem myši na skupinu nebo krok.

        Můžete vyjmout, kopírovat a vložit skupinu nebo krok. Klikněte na položku pravým tlačítkem a vyberte akci. Pro každou akci můžete použít také standardní klávesové zkratky:

        - Vyjmout: **CTRL** + **X**
        - Kopírovat: **CTRL** + **C**
        - Vložit: **CTRL** + **V**

    - **Odebrat krok nebo skupinu**: Vyberte krok nebo skupinu a zvolte **Odebrat**.  

4. Výběrem **OK** uložte změny a zavřete okno. Vyberte **Zrušit** , pokud chcete zahodit změny a zavřít okno. Výběrem **použít** uložte změny a nechejte Editor pořadí úloh otevřený.  

Seznam dostupných kroků pořadí úkolů najdete v tématu [kroky pořadí úkolů](task-sequence-steps.md).  

> [!IMPORTANT]  
> Pokud pořadí úkolů obsahuje v důsledku úpravy nějaké nepřidružené odkazy na objekt, Editor vyžaduje, abyste před zavřením odstranili odkaz. Mezi možné akce patří:  
>
> - Opravte odkaz.
> - Odstraní neodkazovaný objekt z pořadí úloh.  
> - Dočasně zakažte krok neúspěšného pořadí úkolů, dokud nebude poškozený odkaz opraven nebo odebrán.  

Současně můžete otevřít více než jednu instanci editoru pořadí úloh. Toto chování umožňuje porovnávat více pořadí úloh nebo mezi nimi kopírovat a vkládat jednotlivé kroky. Můžete **Upravit** jedno pořadí úloh a **Zobrazit** další, ale nemůžete provádět obě akce ve stejném pořadí úkolů.

## <a name="conditions"></a><a name="bkmk_conditions"></a>Stavu

Podmínky použijte k řízení toho, jak se pořadí úkolů chová. Přidejte podmínky do jednoho kroku nebo do skupiny kroků. Pořadí úkolů vyhodnotí podmínky před spuštěním kroku na zařízení. Tento krok spustí pouze v případě, že se podmínky vyhodnotí jako pravdivé. Pokud podmínka vyhodnotí hodnotu false, pořadí úkolů přeskočí skupinu nebo krok.

Ke správě podmínek použijte kartu **Možnosti** :

![Spravovat podmínky na kartě Možnosti v editoru pořadí úloh](media/4621098-copy-paste-ts-condition.png)

K dispozici jsou tyto typy podmínek:

- **If – příkaz**: použijte příkaz *if* pro seskupení podmínek. Můžete vyhodnotit **všechny podmínky**, **podmínky**nebo **žádné**.

- **Proměnná pořadí úkolů**. V prostředí pořadí úloh Vyhodnoťte aktuální hodnotu jakékoli předdefinované [proměnné pořadí úkolů](task-sequence-variables.md) , akce, vlastní nebo jen pro čtení. Další informace najdete v tématu [podmínky pro krok](using-task-sequence-variables.md#bkmk_access-condition).

    > [!NOTE]
    > V této podmínce lze použít proměnnou pole, je však nutné zadat konkrétního člena pole. Například určuje, `OSDAdapter0EnableDHCP` zda *první* síťový adaptér povolí protokol DHCP. Další informace naleznete v tématu [proměnné pole](using-task-sequence-variables.md#bkmk_array).

- **Verze operačního systému**: vyhodnotí verzi operačního systému zařízení, ve kterém se spouští pořadí úkolů. V tomto seznamu jsou obecné verze operačních systémů používané v rámci Configuration Manager. Pokud chcete vyhodnotit podrobnější verzi operačního systému, třeba konkrétní verzi Windows 10, použijte dotaz na podmínku **WMI** .

- **Jazyk operačního systému**: vyhodnoťte jazyk operačního systému zařízení, ve kterém pořadí úkolů běží. Tento seznam obsahuje jazyky 257, které systém Windows podporuje.

- **Vlastnosti souboru**: vyhodnoťte verzi nebo časové razítko libovolného souboru v zařízení, ve kterém je spuštěno pořadí úloh.

- **Vlastnosti složky**: vyhodnoťte časové razítko každé složky v zařízení, ve kterém je spuštěno pořadí úloh.

- **Nastavení registru**: vyhodnoťte všechny hodnoty klíčů registru zařízení, ve kterém je spuštěno pořadí úloh.

- **Dotaz na rozhraní WMI**: zadejte obor názvů a dotaz k vyhodnocení v zařízení, ve kterém je spuštěno pořadí úloh.

- **Nainstalovaný software**: určete soubor Instalační služba systému Windows pro načtení informací o produktu, který se má shodovat se zařízením, na kterém je spuštěno pořadí úloh. Můžete se shodovat s konkrétním produktem nebo libovolnou verzí produktu.

### <a name="cmdlets-for-conditions"></a>Rutiny pro podmínky

Spravujte podmínky pomocí následujících rutin PowerShellu:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConditionFile](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionFile?view=sccm-ps)
- [Get-CMTSStepConditionFolder](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionFolder?view=sccm-ps)
- [Get-CMTSStepConditionIfStatement](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionIfStatement?view=sccm-ps)
- [Get-CMTSStepConditionOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionOperatingSystem?view=sccm-ps)
- [Get-CMTSStepConditionQueryWmi](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionQueryWmi?view=sccm-ps)
- [Get-CMTSStepConditionRegistry](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionRegistry?view=sccm-ps)
- [Get-CMTSStepConditionSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionSoftware?view=sccm-ps)
- [Get-CMTSStepConditionVariable](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionVariable?view=sccm-ps)

### <a name="copy-and-paste-conditions"></a>Podmínky kopírování a vložení

<!-- 4621098 -->

Chcete-li znovu použít podmínky z jednoho kroku na jiný, počínaje verzí 1910, můžete nyní zkopírovat a vložit podmínky v editoru pořadí úloh. Vyberte podmínku pro vyjmutí nebo zkopírování. Pokud má podmínka podřízené položky, zkopíruje celý blok. Pokud je ve schránce nějaká podmínka, můžete ji vložit s následujícími možnostmi:

- Vložit před
- Vložit za
- Vložit do (platí pouze pro vnořené podmínky)

Pomocí standardních klávesových zkratek můžete kopírovat (**CTRL** + **C**) a vyjmout (**CTRL** + **X**). Standardní klávesová**zkratka v** **kombinaci kláves CTRL +** + provede **vložení po** akci.

K dispozici jsou také nové možnosti přesunutí podmínek v seznamu nahoru nebo dolů.

> [!Note]  
> Podmínky můžete kopírovat a vkládat mezi kroky v pořadí úkolů. Tuto akci nepodporuje mezi různými pořadími úloh.

## <a name="reclaim-lock-for-editing"></a><a name="bkmk_sedo"></a>Uvolnit zámek pro úpravy

<!--3699337-->
Pokud konzola Configuration Manager přestane reagovat, můžete se před 30 Minuti zablokovat a provést další změny, dokud zámek nevyprší. Tento zámek je součástí Configuration Manager SEDO (serializovaná úprava distribuovaných objektů). Další informace najdete v tématu [Configuration Manager SEDO](../../develop/core/understand/sedo.md).

Počínaje verzí 1906 můžete zrušit zámek pro pořadí úkolů. Tato akce se vztahuje jenom na váš uživatelský účet, který má zámek, a na stejném zařízení, ze kterého web udělil zámek. Když se pokusíte o přístup k uzamčenému pořadí úkolů, můžete nyní **zrušit změny**a pokračovat v úpravách objektu. Tyto změny by se ztratily i po vypršení platnosti zámku.

> [!TIP]
> Počínaje verzí 1910 můžete zrušit zámek pro libovolný objekt v konzole Configuration Manager. Další informace najdete v tématu [použití konzoly Configuration Manager](../../core/servers/manage/admin-console.md#bkmk_sedo).<!--4786915-->

## <a name="search"></a><a name="bkmk_search"></a>Nápovědě

<!-- 4621085 -->

Pokud máte velké pořadí úkolů s mnoha skupinami a kroky, může být obtížné najít konkrétní kroky. Počínaje verzí 1910 teď můžete hledat v editoru pořadí úloh. Tato akce vám umožní rychleji vyhledat kroky v pořadí úkolů.

![Hledání v editoru pořadí úloh](media/4621085-task-sequence-search.png)

Zadejte hledaný termín, který chcete spustit. Můžete určit rozsah hledání pomocí následujících typů:

- Název kroku
- Popis kroku
- Typ kroku
- Název skupiny
- Popis skupiny
- Název proměnné
- Podmínky
- Další obsah, například řetězce jako proměnné hodnoty nebo příkazové řádky

Ve výchozím nastavení povolí všechny rozsahy.

Můžete také filtrovat všechny kroky s následujícími atributy:

- Pokračovat při chybě
- Má podmínky

Ve výchozím nastavení nepovoluje žádný filtr.

Při hledání se okno editoru zvýrazní žlutým postupem, který odpovídá kritériím hledání.

Pomocí následujících klávesových zkratek získáte rychlý přístup k těmto vyhledávacím polím a procházejte výsledky hledání:

- **CTRL** + **F**: Zadejte hledaný řetězec.
- **CTRL** + **O**: vyberte možnosti hledání pro určení rozsahu výsledků.
- **F3** nebo **ENTER**: krok dopřed výsledky
- **Shift** + **F3**: krok zpět výsledky

## <a name="see-also"></a>Viz také

- [Správa a vytváření pořadí úkolů](../deploy-use/manage-task-sequences-to-automate-tasks.md)

- [O krocích pořadí úkolů](task-sequence-steps.md)

- [Jak používat proměnné pořadí úkolů](using-task-sequence-variables.md)

- [Použití konzoly Configuration Manager](../../core/servers/manage/admin-console.md)
