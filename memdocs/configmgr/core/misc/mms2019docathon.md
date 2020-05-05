---
title: MMS 2019 Docathon
ms.date: 05/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8fe2ecfc-f5c1-4fa6-8703-245339400723
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e671118578d059e2b8416e6854a701ce7c405c0f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718522"
---
# <a name="mms-2019-docathon"></a>MMS 2019 Docathon

Během Středozápadě Management summit (MMS) 2019 se v týmu obsahu Microsoft pro Configuration Manager a Microsoft Intune spouští docathon. Pokud se účastníte praktické relace [docs.Microsoft.com praktická cvičení](https://sched.co/N6fd) v pondělí, může tato doba fungovat na příspěvcích s podporou zapisovače Microsoftu. Docathon spustí celou konferenci a každý registrovaný účastník pro MMS 2019 se může zúčastnit.

Proč byste se měli zúčastnit? Docs.microsoft.com je open source platforma pro produktovou dokumentaci Microsoftu, která využívá GitHub. Microsoft doporučuje všem uživatelům přispívat k dokumentům! Při přispívat vám platforma rozpozná v seznamu přispěvatelů v každém článku. Následující příspěvky jsou některé z typů, které může komunita poskytnout:

- Překlepy
- Vyjasnění
- Příklady
- Doprovodné materiály a tipy pro reálný svět
- Revize obsahu, aktuálnost

## <a name="set-up"></a>Nastavení

Pokud ještě nejste nastaveni na přispívání, udělejte tyto kroky předem.

### <a name="github-account"></a>Účet GitHub

Vytvoření [účtu GitHub](https://github.com/join)

- Identifikujte všechna afilace ve vašem profilu.  

- Povolení dvoufaktorového ověřování  

#### <a name="additional-considerations"></a>Další aspekty

- Podívejte se na zásady společnosti týkající se Open Source příspěvků.  

    > [!Note]  
    > Větší příspěvky budou vyžadovat, abyste přijali [licenční smlouvu pro přispěvatele](https://cla.opensource.microsoft.com/)v programu Microsoft Open Source. Přečtěte si tuto smlouvu předem.  

- Příspěvky do docs.microsoft.com počtu k posouzení ocenění MVP  

- Zaměstnanci Microsoftu mají několik povinných kroků v jednom čase a mírně odlišný proces přispívání.  

Další informace najdete v tématu [Nastavení účtu GitHub](https://docs.microsoft.com/contribute/get-started-setup-github) v příručce pro Docs.Microsoft.com pro přispěvatele.

## <a name="scope"></a>Rozsah

Tato událost se týká pouze následujících úložišť GitHub:

- [IntuneDocs](https://github.com/MicrosoftDocs/IntuneDocs)
- [SCCMDocs](https://github.com/MicrosoftDocs/SCCMdocs)
- [SCCM-docs-PowerShell-ref](https://github.com/MicrosoftDocs/sccm-docs-powershell-ref)

Také jste připraveni, abyste provedli změny v jiném docs.microsoft.com obsahu, ale nebudete k této události zaúčtovány.

## <a name="learn-the-process"></a>Informace o procesu

Přečtěte si informace o [tom, jak](../understand/use-docs.md#bkmk_docfeedback) zamezit problémy a [jak přispívat](../understand/use-docs.md#bkmk_contribute). Většinu základních změn je možné provádět prostřednictvím prostředí prohlížeče GitHub.  

> [!Note]  
> Pokud vás zajímá složitější pracovní postup s Git a VSCode, přečtěte si téma [Instalace nástrojů pro vytváření obsahu](https://docs.microsoft.com/contribute/get-started-setup-tools). A/nebo požádejte o pomoc Aaron/Erik. Následující akce jsou některé z důvodů, proč použít složitější pracovní postup:
>
> - Vytvořit nový článek
> - Přidání obrázků
> - Hledání a nahrazování řetězců, včetně regulárních výrazů
> - Větší a složitější změny  

## <a name="determine-your-goals"></a>Určení cílů

Začněte přemýšlet o a naplánujte svůj cíl pro tuto událost. Co chcete provést?

- Prohlédněte si stávající problémy v úložištích oborů. U popisků, jako jsou **dobrý první problém** nebo **help-požadováno** , může být možné identifikovat dobré počáteční body. Pokud chcete některý z těchto problémů řešit, přidejte k němu komentář pomocí **#MMS2019Docathon** a označte ho a požádejte ho @author, aby vám tento problém přiřadil. Jinými slovy, [zavolejte DIB](https://www.merriam-webster.com/words-at-play/word-origin-dibs) na IT. Tento postup opakujte tolikrát, kolikrát chcete.  
    Například v SCCMDocs, kde Aaron je Autor článku:`@aczechowski I'm claiming this issue for #MMS2019Docathon`

- Víte, že se jedná o problém s článkem, ale ještě tam neexistovala žádná zpětná vazba. Jinými slovy, v dolní části článku neexistuje žádná **Zpětná vazba** . Zaznamenání nového problému a pak použijte stejné pokyny jako výše, abyste ho mohli uplatnit.  

    - Přidejte například ukázku kódu, příklad reálného světa nebo běžný Tip.  

    - Vyhněte se změnám gramatiky nebo stylu, pokud nebudete mluvit s Aaron/Erik předem.  

    - Váš oblíbený článek má datum starší než 90 dní, do 6. února 2019. Můžete ji zkontrolovat a pak je vaše úprava vlastností metadat **MS. Date** . Tento příspěvek znamená: "Tento článek byl zkontrolován a je stále technicky přesný, takže aktualizujte datum." Zapište problém, který ho vyžádá.  

    - Nejprve si Projděte svůj názor na článek, abyste se ujistili, že neexistují otevřené problémy pro někoho, kdo ho už požadoval. Tato akce není technicky povinná. Pokud to neuděláte a někdo jiný odešle jako první, provedeme jenom první příspěvek.  

- Relace hodinového pracovního dne v pondělí je vyhrazená doba pro práci směrem k těmto cílům. Aaron & Erik jsou k dispozici pro snazší dotazy nebo problémy.

## <a name="contest-summary"></a>Souhrn soutěží

Soutěž se spouští každý týden, 6-9. Každý registrovaný účastník pro MMS 2019 se může zúčastnit. Odeslat záznamy od středu 3:00./odp. ve čtvrtek, 9. května 2019. Ceny se budou vyhovět ve čtvrtek 9. května po [&týmu ConfigMgr Q Session](https://sched.co/N6ge). Musíte být na MMS 2019 pro Win, ale nemusíte tuto relaci navštěvovat. Pokud nejste v relaci, chcete-li získat sazbu, obraťte se na Aaron, než opustí pátek ráno.

> [!Important]  
> Je nutné zahrnout **#MMS2019Docathon** hashtag do všech příspěvků pro kredit.

### <a name="award-categories"></a>Kategorie ocenění

#### <a name="grand-prize"></a>Celková cena

- **Největší dopad**na: na základě následujících kritérií, která jsou posouzená nástrojem Aaron & Erik. Pokud si myslíte, že by vám odeslání mělo nárok, požádejte o pomoc v žádosti o přijetí změn.

    - Zvýhodnění komunitou (50%)
    - Dodržování stylu Microsoftu (25%)
    - Správný Markdownu (25%)  

Vítěz celkové ceny obdrží následující ceny:

- Registrační průchod pro [MMS Jazz Edition](https://mmsmoa.com/sessions/jazz-edition.html), zdvořilostní řídící výbor MMS, hodnota $1799!
- Branding Yeti Rambler 30 oz Tumbler
- Popsocket auta pro připojení a držadlo s brandingem

#### <a name="first-place-prizes"></a>Na první místo ceny

Následující ocenění se počítá podle počtu oprávněných příspěvků do úložišť v oboru. Nemusejí být sloučeny nebo publikovány, stačí odeslat žádost o přijetí změn na konci konference. Vyhrazujeme si právo vyhradit všem, kdo se zdá, že se podaří na hraní systému. Vítěz v každé kategorii obdrží značku Yeti Rambler 30 oz Tumbler a příruční připojení automobilu na Popsocket auta a držadl. Jeden vítěz na kategorii

- **Většina odeslaných potvrzení**

- **Většina řádků se změnila**

- **Většina článků se dodotkla**

> [!Note]  
> Za nejvíc zaznamenaných problémů nebereme žádnou cenu. Zpětná vazba je užitečná, ale bodem této události je přispět.

## <a name="resources"></a>Zdroje a prostředky

- [Styl Microsoft](https://aka.ms/MicrosoftStyle)

    - [Rychlý start](https://docs.microsoft.com/contribute/style-quick-start)

    - [10 nejoblíbenějších tipů pro Microsoft Style a Voice](https://docs.microsoft.com/style-guide/top-10-tips-style-voice)

- [Průvodce pro přispěvatele](https://docs.microsoft.com/contribute)

- [Používání Markdownu pro vytváření článků na webu Docs](https://docs.microsoft.com/contribute/markdown-reference)

## <a name="official-rules"></a>Oficiální pravidla

Microsoft Cloud + AI – obsah vztahů pro vývojáře & učení s výukou MMS 2019 Docathon oficiální pravidla pro soutěž události

1. MĚL

    Tato oficiální pravidla ("pravidla") řídí provoz sady Microsoft C + AI DevRel Content na základě soutěže na zprávy MMS 2019 Docathon ("soutěž"). Microsoft Corporation je sponzor ("sponzor").

2. DEFINICI

    V těchto pravidlech se v tématu "Microsoft", "my", "my" a "US" Podívejte na sponzora. "Vy" a "sami" se rozumí účastník pro soutěž. "Event" odkazuje na událost Docathon 2019 MMS v Minneapolis, MN. Když zadáte, souhlasíte s tím, že je budete svázat s těmito pravidly.

3. VSTUPNÍ OBDOBÍ

    Soutěž bude fungovat během pravidelných hodin od 6. května 2019 do 9. května 2019 ("vstupní období").

4. VZNIK

    Otevřete u kteréhokoli účastníka registrované události 18 let stáří nebo starší, který je zákonným rezidentem 50 USA (včetně oblasti Kolumbie). Zaměstnanci a ředitelé společnosti Microsoft Corporation a jejich dceřiné společnosti, osoby účastnící se provádění nebo správy této propagační akce a rodinných členů každého (závislých, rodinných členů a jednotlivců žijících ve stejné domácnosti) nejsou způsobilé. Neplatný, je-li zakázán.

    Pro obchodní/tradeshow události: Pokud se účastníte události ve vaší kapacitě jako zaměstnanec, je vaší výhradní zodpovědností dodržovat zásady dárku z vašeho zaměstnavatele. Společnost Microsoft se nebude stranou žádných sporů ani akcí souvisejících s touto záležitostí. ZAMĚSTNANCI státní správy, včetně PEDAGOGů: Společnost Microsoft se zavazuje, že bude mít nárok na finanční služby a pravidla etických institucí, a proto zaměstnanci z oblasti státní správy a veřejného sektoru nejsou oprávněni

5. JAK ZADAT

    Chcete-li vytvořit položku, odešlete úpravy článků v následujících úložištích GitHub: IntuneDocs, SCCMDocs, SCCM-docs-PowerShell-ref. Další informace o procesu odeslání najdete v tématu [jak přispívat](https://docs.microsoft.com/sccm/core/understand/use-docs#bkmk_contribute).

    Pokud chcete odeslat položku, odešlete žádost o přijetí změn na GitHubu.

    Můžete odeslat neomezený počet položek. Pro každou kategorii na osobu budeme zakládat jenom jednu cenu.

    Nezodpovídáme za přebytky, ztráty, opožděné, poškozené nebo neúplné položky. Pokud byly sporné, považují se za položky odeslané oprávněným držitelem účtu GitHub.

6. OPRÁVNĚNÁ POLOŽKA

    Aby byla položka oprávněná, musí splňovat následující požadavky na obsah a technickou podporu:

    - Vaše položka musí být vaše vlastní původní práce; ani
    - Vaše položka musn't byla vybrána jako vítěz v jakékoliv jiné soutěži; ani
    - Musíte získat všechny souhlasy, schválení nebo licence potřebné k odeslání položky. ani
    - V rozsahu, ve kterém vstup vyžaduje odeslání uživatelem vygenerované soutěže, jako je software, fotografie, videa, hudba, fotografie, esejí atd., zaručí, že jejich vstup je původní práce, nemusely být kopírovány z jiných uživatelů bez oprávnění nebo zjevné právo a nenarušil soukromí, práva duševního vlastnictví nebo jiná práva jakékoli jiné osoby nebo subjektu. Můžete zahrnout ochranné známky, loga a návrhy Microsoftu, pro které vám Microsoft uděluje omezené licence pro použití výhradně pro účely odeslání položky do této soutěže. ani
    - Vaše položka nemusí obsahovat, jak je určeno v naší výlučné a absolutní úvaze, veškerý obsah, který je obscénního nebo urážlivý, násilný, POMLOUVAČNÉHO, pohrdavé nebo nezákonný, nebo který propaguje alkohol, nelegální drogy, tabák nebo konkrétní politickou agendu, nebo který komunikuje s negativním významem, který se může negativně projevit na vůli společnosti Microsoft.

7. POUŽITÍ POLOŽEK

    Nežádáme o vlastnická práva k vašemu odeslání. Když ale odešlete nějakou položku, poskytneme vám nevratnou, bezplatnou, celosvětovou právo a licenci k používání, revizi, posouzení, testování a jiné analýze vašeho záznamu a veškerého jeho obsahu v souvislosti s touto soutěží, a využijte svůj záznam na jakémkoli médiu, který je teď známý nebo později vymysleli pro jakýkoli nekomerční nebo komerční účel, včetně, ale ne omezení na nebo povýšení produktů nebo služeb společnosti Microsoft bez dalších oprávnění od vás. Nebudete dostávat žádné kompenzace ani kredity pro použití vaší položky, kromě těch, které jsou popsané v těchto oficiálních pravidlech.

    Tím, že zadáte, potvrzujete, že můžeme vystavit nebo vyřadit podobné materiály, které jsou stejné nebo stejné jako u vaší položky, a nebudete mít k dispozici žádné deklarace vyplývající z jakýchkoli podobností. Dále si porozumíte, že nebudeme omezovat pracovní přiřazení zástupců, kteří mají přístup k vaší položce, a souhlasíte s tím, že v rámci této smlouvy nebo zákona o používání těchto produktů nebo služeb nevzniká odpovědnost za použití informací v nevědomé paměti pro naše zástupce.

    Vaše položka se může publikovat na veřejném webu. Nezodpovídáme za jakékoli neoprávněné použití vaší položky návštěvníkům tohoto webu. Společnost Microsoft není povinná používat vaši položku pro jakýkoliv účel, a to ani v případě, že byla vybrána jako vítězná položka.

8. VÍTĚZNÝ VÝBĚR A OZNÁMENÍ

    Čeká se na potvrzení způsobilosti, potenciální cena WINNERS vybere společnost Microsoft nebo její agent nebo kvalifikovaný panel pro rozhodování ze všech oprávněných položek přijatých na základě následujících kritérií:

    - Celková cena: největší dopad na základě následujících kritérií:
        - 50% – výhoda komunity
        - 25% – dodržování stylu Microsoftu
        - 25% – řádný Markdownu
    - Následující ceny jsou na začátku ceny vypočítané počtem oprávněných příspěvků do úložišť v oboru. Nemusejí být sloučeny nebo publikovány, stačí odeslat žádost o přijetí změn na konci konference. Vyhrazujeme si právo vyhradit všem, kdo se zdá, že se podaří na hraní systému.
        - Většina odeslaných potvrzení
        - Většina řádků se změnila
        - Většina článků se dodotkla

    WINNERS se vybere po času 3:00. čas středu ve čtvrtek, 9. května 2019.

    WINNERS se bude informovat na událost a před ukončením události musí mít nárok na ni.

    Pokud existuje propojení mezi všemi oprávněnými položkami, další soudce na základě výše popsaných kritérií zruší vazbu. Rozhodnutí soudců jsou finální a závazná. Pokud neobdržíme dostatečný počet položek, které splňují požadavky na vstupy, můžeme podle vlastního uvážení vybrat méně WINNERS, než kolik cen soutěží popsaných níže.

    WINNERS se bude informovat prostřednictvím kontaktních údajů, které jsou uvedené během vstupu a můžou se vyžadovat, aby se vyžádala cena za e-mail a daňové formuláře ("formuláře"). Pokud se vybraný vítěz nedá kontaktovat, je neoprávněný, nenárokuje na ni nárok nebo nevrátí žádné formuláře, vybraný vítěz propadne na svou příležitost a bude vybraný čas. Vyberou se jenom tři alternativní WINNERS, po kterých budou neuplatněné ceny zůstat neoceněné.  

9. VĚCNÉ ceny

    Budou se přidávají následující ceny:

    - Jedna (1) Celková cena Balíček o Cena, který se skládá z následujících položek:
        - Registrační průchod pro [MMS Jazz Edition](https://mmsmoa.com/sessions/jazz-edition.html) (poskytovaný řídícím výborem MMS). Přibližná maloobchodní hodnota (ARV) $1799.
        - Yeti Rambler 30 oz Tumbler. Přibližná maloobchodní hodnota (ARV) $35,00.
        - Připojení a úchyt Popsocket auta. Přibližná maloobchodní hodnota (ARV) $15,00.

        Celková Přibližná maloobchodní hodnota (ARV) tohoto balíčku je $1849.

    - Tři (3) první cena (y). Balíček o Cena, který se skládá z následujících položek:
        - Yeti Rambler 30 oz Tumbler. Přibližná maloobchodní hodnota (ARV) $35,00.
        - Připojení a úchyt Popsocket auta. Přibližná maloobchodní hodnota (ARV) $15,00.

        Celková Přibližná maloobchodní hodnota (ARV) tohoto balíčku je $50.

    Celková přibližná hodnota maloobchodního prodeje (ARV) všech cen: $1999

    Vybereme jenom jednu (1) cenu na osobu. Nebude uděleno více než stanovený počet cen. Nepovoluje se žádná náhrada, přenos nebo přiřazení dovolené, s tím rozdílem, že společnost Microsoft si vyhrazuje nárok na náhradu za stejnou nebo větší hodnotu v případě, že nabízená cena není k dispozici. Ceny jsou poskytovány "tak, jak jsou", a to bez záruky jakéhokoli druhu, ať už výslovně nebo mlčky předpokládaného, včetně neomezeného odůvodnění nebo OBCHODOVATELNOSTI, vhodnosti pro určitý účel nebo neporušení. Cena WINNERS může být nutná k dokončení a vrácení nároku na cena nebo daňové formuláře ("formuláře") ve lhůtě uvedené v oznámení vítěze. Daňové poplatky, pokud jsou nějaké, jsou výhradně zodpovědností za toho, kdo má za úkol Hledat nezávislé poradenství v souvislosti s daňovými důsledky přijetí. Když přijmete určitou částku, souhlasíte s tím, že společnost Microsoft může používat vaše zadání, název, image a rodiště online a na jakémkoli jiném médiu, a to v souvislosti s touto soutěží bez placení nebo kompenzace, s výjimkou případů zakázaných zákonem.

10. LICHÁ

    Lichá výhry vycházejí z počtu a kvality obdržených nárokových položek.

11. OBECNÉ PODMÍNKY A VYDÁNÍ ODPOVĚDNOSTI

    V rozsahu povoleném zákonem stačí, když souhlasíte s vydáním a ztrátou společnosti Microsoft a jejích příslušných rodičů, partnerů, poboček, poboček, zaměstnanců a agentů vyplývajících ze všech závazků nebo jakékoli škody, ztráty nebo poškození jakéhokoli druhu vzniklého v souvislosti s touto soutěží nebo vydanou příležitostí.

    Použijí se všechny místní zákony. Rozhodnutí Microsoftu jsou konečná a závazná.

    Vyhrazujeme si právo tuto soutěž zrušit, změnit nebo pozastavit z jakéhokoli důvodu, včetně podváděním, selhání technologie, pohromě, války nebo jakékoli jiné nepředvídatelné nebo neočekávané události, která má vliv na integritu této soutěže, ať už je to lidské nebo mechanické. Pokud se integrita soutěže nedá obnovit, můžeme vybrat WINNERS ze všech oprávněných položek obdržených před tím, než jsme museli tuto soutěž zrušit, změnit nebo pozastavit. Porušující se pravidla budou trestně v celém rozsahu zákonů a můžou být zakázaná z účasti na soutěžech Microsoftu.

12. SEZNAM WINNERS

    Seznam ceníkové WINNERS se bude účtovat do https://aka.ms/mms2019docathon 30 dnů od 9. května 2019.

13. OCHRANA OSOBNÍCH ÚDAJŮ

    V Microsoftu jsme se zavázali chránit vaše osobní údaje. Společnost Microsoft používá informace, které zadáte v tomto formuláři, k upozorňování na důležité informace o našich produktech, upgradech a vylepšeních a k odesílání informací o dalších produktech a službách společnosti Microsoft. Společnost Microsoft nesdílí informace, které poskytnete u třetích stran bez vašeho svolení, s výjimkou případů, kdy je potřeba dokončit služby nebo transakce, které jste požadovali, nebo podle požadavků zákonů. Společnosti Microsoft se zavazuje chránit bezpečnost vašich osobních údajů. Používáme řadu technologií a postupů pro zabezpečení, které pomáhají chránit vaše osobní informace před neoprávněným přístupem, použitím nebo sdělením. Vaše osobní údaje nejsou nikdy sdíleny mimo společnost bez vašeho svolení, s výjimkou podmínek popsaných výše.

    Pokud se domníváte, že společnost Microsoft nedodržuje toto prohlášení, obraťte se na privrc@microsoft.com společnost Microsoft odesláním e-mailu nebo poštovní pošty do služby Microsoft Privacy Response Center, Microsoft Corporation, One Microsoft Way, Redmond, WA 98052.
