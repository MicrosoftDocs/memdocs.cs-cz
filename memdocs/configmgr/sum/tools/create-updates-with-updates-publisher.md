---
title: Vytvoření aktualizací
titleSuffix: Configuration Manager
description: Vytváření a kompletování aktualizací softwaru pomocí System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 46a1a8ac-126c-4ee6-ae09-32dfbdb83368
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b2445158732f5adf21c43d73b13039f9e41610c8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723982"
---
# <a name="create--software-updates-and-update-bundles-with-updates-publisher"></a>Vytváření aktualizací softwaru a sad aktualizací pomocí programu Updates Publisher

*Platí pro: System Center Updates Publisher*

Pomocí nástroje Updates Publisher můžete pomocí průvodce **vytvořením aktualizace** vytvořit vlastní aktualizace a průvodce **vytvořením sady** vytvořit sady aktualizací.

Vzhledem k tomu, že tito dva průvodci mají podobný pracovní postup, postup vytvoření sady aktualizací odkazuje na postup vytvoření aktualizací s podrobnými podrobnostmi.

## <a name="use-the-create-update-wizard"></a>Použití Průvodce vytvořením aktualizace
1. V konzole nástroje přejdete do **pracovního prostoru aktualizace**a potom v podokně **Začínáme** na kartě **Domů** na pásu karet na tlačítko **aktualizovat** . Tím se otevře průvodce **vytvořením aktualizace** .

2. Na stránce **balíček** použijte následující informace, které vám pomůžou při konfiguraci aktualizace:

   -   Vyberte **Procházet** a vyhledejte balíček aktualizace softwaru, který budete používat jako zdroj balíčku. Mezi platné zdroje patří. MSI,. MSP nebo. Soubory EXE. Aktualizace Vydavatel vyžaduje přístup k souboru pro vytvoření hodnoty hash souboru. Hodnota hash a název souboru se pak použijí v metadatech aktualizace pro vytvářenou aktualizaci.

   -   Zadejte zdrojové umístění obsahu pro tuto aktualizaci. Obvykle je to místo, kde se během publikování do serveru WSUS stáhne binární soubor aktualizace.  Pokud je vybraná možnost **použít místní zdroj k publikování obsahu aktualizace softwaru** , cesta se nevyžaduje.

       Později po publikování aktualizace na serveru WSUS stáhne Publisher binární soubory pro aktualizaci z uvedeného umístění zdroje.  Pokud není zadána žádná cesta, aplikace Update Publisher prohledá [cestu publikování v místním zdroji](updates-publisher-options.md#advanced) pro binární aktualizaci.

   -   Zadejte **binární jazyk** aktualizace softwaru.

   -   Zadejte **návratové kódy úspěchu**a **úspěšné pokusy o restartování** pro aktualizaci. Více návratových kódů oddělte pomocí čárky. Pomocí návratových kódů můžete určit, kdy byla instalace aktualizace úspěšná, a když se vyžadují restartování.

       -   Soubory a opravy Instalační služby systému Windows (. MSI a. Soubory MSP) tyto hodnoty automaticky nastavily a nelze je upravit.

       -   For. EXE aktualizuje výchozí kódy definované. Soubor EXE se používá, pokud nejsou zadány žádné návratové kódy.

   -   Zadejte všechny argumenty příkazového řádku, které jsou nutné k instalaci aktualizace softwaru.

       -   Soubory a opravy Instalační služby systému Windows (. MSI a. Soubory MSP) automaticky tyto hodnoty nastaví. Pro tyto typy souborů musí být argumenty zadány jako ** \[hodnota\]=\[\]Name**. Kromě toho nejsou podporovány všechny možnosti, které začínají **/** na (například **/qn**). MSI nebo. Aktualizace softwaru MSP.

       -   For. Aktualizace EXE jsou platné všechny argumenty.

3. Na stránce **informace** zadejte podrobnosti o aktualizaci, která je zahrnutá při publikování nebo exportu aktualizace. Podrobnosti zahrnují lokalizované vlastnosti, jako je název aktualizací (název) a popis. Pak zadáte obecnější podrobnosti, jako je například klasifikace, dodavatel a produkt a kde se dozvíte další informace o této aktualizaci.

    __Lokalizované vlastnosti:__

   - **Jazyk**: Vyberte jazyk a potom zadejte název a popis. Pak můžete vybrat další jazyky, jeden v čase, přičemž každý jazyk podporuje vlastní název a popis.

   - **Title**: zadejte název aktualizace. Tento název se zobrazí v pracovním prostoru aktualizace konzoly nástroje Updates Publisher.

   - **Popis**: Popis aktualizace je popisný. Můžete zahrnout, co se aktualizace nainstaluje, a proč nebo kdy se má použít.

   **Klasifikace:** Níže jsou uvedeny běžné popisy různých klasifikací.

   - **Aktualizace**: aktualizace aplikace nebo souboru, který je aktuálně nainstalován.

   - **Kritické**: široce vydaná aktualizace pro určitý problém, která řeší kritickou chybu, která nesouvisí se zabezpečením.

   - **Balíček funkcí**: nové funkce produktu, distribuované mimo vydání produktu a jsou obvykle zahrnuté v příštím plném vydání produktu.

   - **Zabezpečení**: široce vydaná aktualizace pro problém specifický pro daný produkt, který souvisí se zabezpečením.

   - **Kumulativní aktualizace**: kumulativní sada oprav hotfix, které jsou zabaleny dohromady pro snadné nasazení. Tyto opravy hotfix mohou zahrnovat aktualizace zabezpečení, kritické aktualizace, aktualizace atd. Kumulativní aktualizace obecně řeší určitou oblast, například zabezpečení nebo funkci produktu.

   - **Aktualizace Service Pack**: kumulativní sada oprav hotfix, které se aplikují na aplikaci. Tyto opravy mohou zahrnovat aktualizace zabezpečení, důležité aktualizace, aktualizace softwaru atd.

   - **Nástroj**: Určuje nástroj nebo funkci, která pomáhá dokončit jednu nebo více úloh.

   - **Ovladač**: aktualizace pro software ovladače.

   **Dodavatel:** Určete dodavatele pro aktualizaci. Rozevírací seznam můžete použít k použití hodnot z aktualizací, které jsou v úložišti. Když zadáte dodavatele, průvodce vytvoří složku s názvem dodavatele v části **všechny aktualizace softwaru** v **pracovním prostoru aktualizace** , pokud tato složka ještě neexistuje. Níže jsou uvedené rezervované názvy služby WSUS (Windows Server Update Services), které se nedají zadat pro vámi vytvořené aktualizace:
   - Microsoft Corporation
   - Microsoft
   - Aktualizace
   - Aktualizace softwaru
   - Nástroje
   - Nástroj
   - Kritická
   - Důležité aktualizace
   - Zabezpečení
   - Aktualizace zabezpečení
   - Balíček funkcí
   - Kumulativní aktualizace
   - Aktualizace Service Pack
   - Ovladač
   - Aktualizace ovladačů
   - Nabídky
   - Aktualizace sady prostředků

   **Produkt**: Určete typ produktu, pro který je aktualizace určena. Rozevírací seznam můžete použít k použití hodnot z aktualizací, které jsou v úložišti. Stejný seznam názvů rezervovaných službou WSUS, které nelze použít pro **dodavatele**, nelze použít pro **produkt**.

   **Adresa URL s dalšími**informacemi: zadejte adresu URL, kde můžete najít další informace o této aktualizaci. Když zadáte tuto adresu URL, musíte použít malá písmena pro **protokol HTTPS** nebo **http** .

4. Na stránce **volitelné informace** můžete nakonfigurovat podrobnosti, které poskytují další informace o této aktualizaci.

   -   **ID bulletinu**: ID bulletinů jsou obvykle, ale ne vždy, poskytované dodavateli aktualizací.

   -   **ID článku**: Pokud je k dispozici článek aktualizace softwaru, ID článku může být užitečné pro jednotlivce, kteří hledají další informace o této aktualizaci.

   -   **CVE ID:** Seznamte se s jedním nebo více běžnými identifikátory chyb zabezpečení a ohrožení (CVE), které poskytují informace o zabezpečení sady Update nebo Update. Při výpisu více než jednoho použijte středník pro oddělení CVEs jako v tomto příkladu: *CVE1; CVE2.*

   -   **Adresa URL podpory:** Uveďte adresu URL, která obsahuje informace o podpoře pro tuto aktualizaci, pokud je k dispozici. Když zadáte tuto adresu URL, musíte použít malá písmena pro **protokol HTTPS** nebo **http** .

   -   **Závažnost:** Nastavte úroveň závažnosti pro tuto aktualizaci.

   -   **Dopad:** K určení dopadu lze použít následující možnosti:
       -   **Normální –** Použijte k označení, že aktualizace vyžaduje typické postupy instalace.
       -   **Vedlejší –** Toto použijte k označení aktualizace vyžaduje minimální instalační postupy.
       -   **Vyžaduje výhradní zpracování –** Toto použijte k označení, že aktualizace musí být nainstalována samostatně, a to výhradně z jiných aktualizací.   <br /><br />

   -   **Chování při restartování:** Slouží k zadání informací o chování při restartování aktualizací. Toto nastavení nemá vliv na skutečné chování instalace aktualizace.

       -   **Nikdy**nerestartovat: počítač po instalaci aktualizace softwaru nikdy neprovede restart systému.
       -   **Vždy vyžaduje restart**: počítač po instalaci aktualizace softwaru vždy provádí restart systému.
       -   **Může vyžádat restartování**: po instalaci aktualizace softwaru počítač požádá o restartování systému pouze v případě, že je nutné restartovat počítač. Uživatel má možnost odložit restartování. Toto je výchozí hodnota. <br /><br />

5. Na stránce **požadované** součásti Určete požadavky, které musí být nainstalovány na počítači, než bude možné nainstalovat tuto aktualizaci. Požadavky mohou být **detectoids** nebo jiné aktualizace. Detectoids jsou pravidla vysoké úrovně, jako je třeba ta, která vyžaduje, aby procesor počítačů byl 64 procesor. Detectoids může také určit konkrétní aktualizace, které musí být nainstalovány před instalací této aktualizace.

   -   Pro lepší výkon použijte detectoids namísto vytváření *instalovatelných* a *nainstalovaných pravidel* , která provádějí stejnou kontrolu nebo akci.

   Pomocí možnosti hledání **dostupných aktualizací softwaru a detectoids** vám pomůžou najít konkrétní aktualizace nebo detectoids. Můžete například vyhledat **procesor** a vyhledat tak detectoids, který vám umožní omezit instalaci na základě konkrétní architektury procesoru.

   Můžete vybrat jednu nebo více položek v čase, které chcete přidat jako požadované součásti. Při přidávání požadovaných součástí se vybrané detectoids přidávají jako jedna nebo víc skupin. Aby mohl počítač nárokovat na instalaci, musí splňovat požadavek aspoň jednoho člena každé skupiny, kterou nakonfigurujete:

   -   Když kliknete na **Přidat předpoklad,** všechny vybrané položky se přidají do samostatných, individuálních a skupin. Aby tato aktualizace mohla být oprávněná, musí počítač splňovat požadavky v této skupině a předávat požadavky na všechny další skupiny, které jsou nakonfigurované.

   -   Když kliknete na **Přidat skupinu,** všechny položky, které jste vybrali, se přidají do jedné skupiny. Aby tato aktualizace měla nárok na tuto aktualizaci, musí počítač splňovat alespoň jeden z požadavků v této skupině a předávat požadavky na všechny nakonfigurované další skupiny.

6. Na stránce **nahrazování** určete aktualizace nahrazené (nahrazené) touto aktualizací. Po publikování této aktualizace aplikace Configuration Manager označí každou aktualizaci, která byla nahrazena **platností**. Klienti si pak tuto aktualizaci nainstaluje místo nahrazených aktualizací.

7. Na stránce **použitelnosti** pomocí **editoru pravidel** Definujte sadu pravidel, která určí, jestli zařízení tuto aktualizaci potřebuje. (Tato stránka je podobná **nainstalované** stránce, která za ní následuje.)

   Pokud chcete přidat nové pravidlo, klikněte na ![Nové pravidlo](media/newrule.png). Otevře se stránka s pravidlem použitelnosti, kde můžete nakonfigurovat pravidla.

   Mezi typy pravidel, která můžete vytvořit, patří:

   -   **Soubor** – toto pravidlo použijte, pokud požadujete, aby zařízení mělo soubor s vlastnostmi, které splňují jedno nebo více kritérií, která zadáte před použitím této aktualizace.

   -   **Registr –** Tento typ slouží k zadání podrobností registru, které musí být přítomné předtím, než se zařízení zaregistruje pro instalaci této aktualizace.

   -   **Systém –** Toto pravidlo používá systémové podrobnosti k určení použitelnosti. Můžete si vybrat, jestli se má definovat verze Windows, jazyk Windows, architekturu procesoru, nebo zadat dotaz rozhraní WMI k identifikaci operačního systému zařízení.

   -   **Instalační služba systému Windows –** Tento typ pravidla použijte k určení použitelnosti na základě nainstalovaného. MSI nebo Instalační služba systému Windows patch (. MSP). Můžete také určit, zda jsou v rámci požadavku nainstalovány konkrétní součásti nebo funkce.

       > [!IMPORTANT]  
       > Na spravovaných zařízeních Agent web Windows Update nedokáže detekovat balíčky instalace systému Windows, které jsou nainstalované pro jednotlivé uživatele. Když použijete tento typ pravidla, nakonfigurujete další pravidla použitelnosti, například verze souborů nebo hodnoty klíčů registru, aby balíček Instalační služba systému Windows mohl být správně zjištěn bez ohledu na uživatele nebo na systém.

   -   **Uložené pravidlo –** Tato možnost umožňuje vyhledat a použít pravidla, která jste *vytvořili v pracovním prostoru pravidla*.

       Po vytvoření pravidla můžete použít jiné ikony k úpravě pravidla a v případě, že existuje více pravidel pro definování vztahů mezi těmito pravidly.

   Po dokončení vytváření a přidávání pravidel klikněte na **OK** v dialogovém okně **vytvořit sadu pravidel** a tuto sadu uložte. Pak můžete vytvořit **nové** pravidlo a přidat ho do sady také.

   Pokud máte více pravidel nebo sad pravidel pro přidání do aktualizace, můžete pomocí logických operátorů v **editoru pravidel** určit podmínky mezi pravidly a v pořadí, v jakém jsou zpracovány.

8. Na **nainstalované** stránce použijte **Editor pravidel a** Definujte sadu pravidel, která určují, jestli je v zařízení už nainstalovaná aktualizace, kterou konfigurujete. (Tato stránka je podobná stránce s **použitelností** , která tuto stránku pokračuje.)

   Tato stránka Průvodce podporuje konfiguraci pravidel se stejnými možnostmi a kritérii jako na stránce **použitelnost** .

   Po dokončení průvodce se nová aktualizace přidá do uzlu v **pracovním prostoru aktualizace** , který je identifikovaný **dodavatelem** a názvem **produktu** použitým pro danou aktualizaci.

## <a name="use-the-create-bundle-wizard"></a>Použití Průvodce vytvořením sady prostředků
Vzhledem k tomu, že tento průvodce používá stejný pracovní postup jako [Průvodce vytvořením aktualizace](#use-the-create-update-wizard), použijte tento pracovní postup, ale Všimněte si následujícího rozdílu pro sady prostředků:

1.  Průvodce spustíte tak, že v konzole přejdete do **pracovního prostoru aktualizace**a pak na kartě **Domů** na pásu karet vyberete **sada** .

2.  Na rozdíl od Průvodce vytvořením aktualizace není při vytváření sady prostředků žádná stránka balíčku.

3.  Na stránce **informace** zadejte podrobnosti o sadě aktualizací, které jsou zahrnuté při publikování nebo exportu aktualizace.

4.  Na stránce **volitelné informace** můžete nakonfigurovat podrobnosti, které poskytují další informace o sadě aktualizací. Dostupné možnosti jsou stejné jako při vytváření aktualizace. Nicméně možnosti pro dopad a chování při restartování nejsou k dispozici, protože se nevztahují na sady prostředků.

5.  Na stránce **požadavků** Určete požadavky, které musí být nainstalovány na počítači, než bude možné tuto sadu nainstalovat. Tato pravidla jsou stejná jako v případě jednotlivých aktualizací.

6.  Na stránce **nahrazování** určete aktualizace nahrazené (nahrazené) sadou aktualizací. Tato pravidla jsou stejná jako v případě jednotlivých aktualizací.

7.  Na stránce **Členové** vyberte aktualizace, které chcete přidat do sady aktualizací. K dispozici jsou pouze aktualizace, které jste vytvořili nebo importovali do aplikace Updates Publisher.

Po dokončení průvodce se nová sada aktualizací přidá do uzlu v **pracovním prostoru aktualizace** , který je identifikovaný názvem **dodavatele** , který jste použili pro sadu aktualizací.
