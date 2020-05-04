---
title: Package Conversion Manager
titleSuffix: Configuration Manager
description: Přečtěte si o nástroji Package Conversion Manager k převedení balíčků na aplikace v Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f053fa73-c553-4522-a6b9-f885f23fe57c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 075dd860d20662679e5bdf58dae23d0220fa751e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709912"
---
# <a name="package-conversion-manager"></a>Package Conversion Manager

*Platí pro: Configuration Manager (Current Branch)*

<!--1357861-->

Počínaje verzí 1806 Package Conversion Manager pomáhá převést Configuration Manager starších balíčků do aplikací. Aplikace mají další výhody, jako jsou závislosti, pravidla požadavků, metody detekce a spřažení uživatelských zařízení.

> [!Tip]  
> Tato funkce byla poprvé představena ve verzi 1806 jako [funkce předběžné verze](../../core/servers/manage/pre-release-features.md). Počínaje verzí 1810 Tato funkce už není součástí předběžné verze.  


Configuration Manager aplikace obsahuje soubory a programy, které nasadíte do klientských zařízení. Na rozdíl od starších balíčků a programů ale aplikace poskytuje další funkce zaměřené na uživatele. Například aplikace může obsahovat typy nasazení pro místní instalaci softwarových balíčků, virtuální aplikační balíček nebo verzi aplikace pro mobilní zařízení.

Další informace najdete v těchto článcích: 
- [Úvod ke správě aplikací](../understand/introduction-to-application-management.md)  
- [Balíčky a programy](../deploy-use/packages-and-programs.md)  

> [!Important]  
> Pokud jste dříve nainstalovali starší verzi nástroje Package Conversion Manager, před upgradem lokality ji nejprve odinstalujte. Tato integrovaná verze nevyžaduje instalaci, ale může být v konfliktu se stávajícími verzemi.  

Tato integrovaná verze správce převodu balíčků funguje na balíčcích na webu Configuration Manager Current Branch. Nejedná se o samostatný nástroj. Pokud máte balíčky a programy ve starší verzi Configuration Manager, nejprve balíčky migrujte do vaší aktuální lokality. Další informace najdete v tématu [migrace dat mezi hierarchiemi](../../core/migration/migrate-data-between-hierarchies.md).

<!-- SCCMDocs-pr issue #3357 -->
Configuration Manager verze 1902 obsahuje následující vylepšení:
- Plánovaná analýza balíčku se ve výchozím nastavení spouští každých 7 dnů.
- Rutiny PowerShellu pro analýzu a převod balíčků
- Obecné opravy chyb a vylepšení



## <a name="planning"></a>Plánování

Než začnete převádět balíčky do aplikací, vytvořte nejprve plán. Následující postup je příklad plánu:

- [Definice podrobného plánu převodu balíčků](#bkmk_define)  

- [Výběr a příprava balíčků pro převod](#bkmk_prepare)  

- [Vybrat testovací balíčky](#bkmk_test)  

- [Analyzujte, prozkoumejte a převeďte balíčky](#bkmk_analyze)  

- [Testování a nasazení aplikací](#bkmk_deploy)  


### <a name="define-a-detailed-package-conversion-plan"></a><a name="bkmk_define"></a>Definice podrobného plánu převodu balíčků

Tato část popisuje dva ukázkové plány převodu balíčků:  

- [Testovací prostředí s vysokým prostředkem](#bkmk_define-high): máte testovací prostředí s prostředky, oprávněními a architekturou pro úplnou replikaci provozního prostředí.  

- [Testovací prostředí s omezenými prostředky](#bkmk_define-limited): nemáte testovací prostředí, které plně replikuje vaše provozní prostředí.  

Podle potřeby upravte tyto plány pro jiné problémy, které jsou specifické pro vaše prostředí.

#### <a name="sample-plan-for-a-high-resource-test-environment"></a><a name="bkmk_define-high"></a>Ukázkový plán pro testovací prostředí s vysokým prostředkem

Vaše testovací prostředí má prostředky, oprávnění a architekturu, které jsou podobné vašemu provoznímu prostředí. Pomocí testovacího prostředí můžete efektivně analyzovat a převádět všechny balíčky a potom testovat všechny vaše Configuration Manager aplikace. Po dokončení této práce ji přeneste do produkčního prostředí. 

Váš plán převodu balíčků může být podobný následujícímu postupu:  

1.  Vyberte balíčky, které chcete převést.  

2.  Migrujte balíčky pro převod do vašeho testovacího prostředí.  

3.  Připravte balíčky na převod.  

4.  Vyberte testovací balíčky.  

5.  Analyzujte, prozkoumejte a převeďte testovací balíčky.  

6.  Otestujte převedené aplikace.  

7.  Analyzujte a převeďte zbývající (netestové) balíčky.  

8.  Exportujte aplikace z testovacího prostředí. Importujte je do svého produkčního prostředí.  

#### <a name="sample-plan-for-a-limited-resource-test-environment"></a><a name="bkmk_define-limited"></a>Ukázkový plán pro testovací prostředí s omezenými prostředky

Vaše testovací prostředí nemá žádné prostředky, oprávnění a architekturu, které jsou podobné vašemu produkčnímu prostředí. Nemůžete analyzovat, testovat a převádět všechny balíčky. V tomto scénáři Analyzujte, prozkoumejte, převeďte a otestujte balíčky testů. Pak zbývající balíčky migrujte do provozního prostředí, abyste je mohli analyzovat a převádět. 

Váš plán převodu balíčků může být podobný následujícímu postupu:

1.  Vyberte balíčky, které chcete převést.  

2.  Vyberte testovací balíčky.  

3.  Migrujte testovací balíčky do vašeho testovacího prostředí.  

4.  Připravte balíčky testů pro převod.  

5.  Analyzujte, prozkoumejte a převeďte testovací balíčky.  

6.  Otestujte převedené aplikace.  

7.  Exportujte testovací aplikace z testovacího prostředí. Pak je importujte do svého produkčního prostředí.  

8.  Migrujte zbývající balíčky do provozního prostředí a připravte je na převod.  

9.  Analyzujte, prozkoumejte a převeďte zbývající balíčky v produkčním prostředí.  

10. Uvolněte zbývající aplikace do provozního prostředí.  


### <a name="select-and-prepare-packages-for-conversion"></a><a name="bkmk_prepare"></a>Výběr a příprava balíčků pro převod

#### <a name="select-the-packages-that-you-want-to-convert"></a><a name="bkmk_prepare-select"></a>Vyberte balíčky, které chcete převést.

Ne všechny balíčky jsou vhodné pro převod na aplikace. Než začnete s převodem balíčků, identifikujte balíčky, které se nepřevádí. 

Nejlepším typem balíčku pro převod na aplikace jsou ty, které obsahují software směřující na uživatele, například:  

- Soubory Instalační služba systému Windows (. msi a. msu)  

- Programy Microsoft Application Virtualization (App-V)  

- Spustitelné soubory Windows (. exe)  

Typy balíčků, které jsou nejlépe zachované jako balíčky a nepřevádí na aplikace, zahrnují:

- Nástroje údržby systému. Například skripty nebo nástroje pro zálohování.  

- Balíčky pro software, které nepodporují.

> [!Tip]  
> Po určení balíčků, které nejsou vhodné pro převod do aplikací, je přesuňte do samostatné složky v konzole Configuration Manager. Vytvoření složky balíčku v konzole Configuration Manager:  
> - Klikněte pravým tlačítkem na uzel **balíčky** .  
> - Vyberte **složky**a pak vyberte **vytvořit složku**.  
> - Zadejte název složky, například `Not Converted`.  
> - Klikněte na tlačítko **OK**.  

#### <a name="prepare-the-packages-for-conversion"></a>Příprava balíčků na převod

Pro každý balíček, který chcete převést, zajistěte, aby splňoval tyto podmínky:  

- Umístění zdrojových souborů je úplná cesta UNC, například `\\Server\Share\File`.  

- Instalační služba systému Windows soubory používají pouze jeden jedinečný kód produktu.  


### <a name="select-test-packages"></a><a name="bkmk_test"></a>Vybrat testovací balíčky

Pokud je to možné, vaše skupina testovacích balíčků by měla obsahovat balíčky, které splňují následující kritéria:  

- Aspoň jeden testovací balíček se stavem připravenosti **automaticky**.  

- Alespoň jeden testovací balíček se stavem připravenosti **ručně**.  

V ideálním případě by měly být balíčky testů základní, například:  

- Balíčky, o kterých víte dobře.  

- Balíčky, které jsou pro vaši organizaci nejdůležitější.  

- Balíčky, které lze snadno testovat.  

Identifikujte balíčky, které jsou vhodné pro testování. Pak je přesuňte do samostatné složky v konzole Configuration Manager.


### <a name="analyze-investigate-and-convert-packages"></a><a name="bkmk_analyze"></a>Analyzujte, prozkoumejte a převeďte balíčky

#### <a name="analyze-packages"></a>Analyzovat balíčky

Chcete-li analyzovat jednotlivý balíček nebo malou skupinu, použijte nástroj Package Conversion Manager integrovaný do konzoly Configuration Manager. Další informace najdete v tématu [jak analyzovat a převádět balíčky](how-to-analyze-and-convert.md).  

> [!NOTE]  
> Viz uzel **stav převodu balíčku** v pracovním prostoru **monitorování** . Zobrazuje souhrnné informace o procesech analýzy a převodu.  

#### <a name="investigate-analysis-results"></a>Prozkoumat výsledky analýzy

Po analýze testovacích balíčků Prozkoumejte balíčky se stavem připravenosti **ručně** nebo **Chyba**. Určete důvody, proč mají tento stav. Mezi běžné důvody pro stav připravenosti **Ruční** nebo **Chyba** patří:

- Balíček neobsahuje informace potřebné k vytvoření metody detekce v typu nasazení aplikace.  

- Balíček neobsahuje informace požadované pro převod kolekcí na globální podmínky a požadavky.  

- Balíček obsahuje více než jeden program.  

- Balíček je závislý na jiném balíčku, který jste převedli do aplikace.  

Další informace získáte pomocí následujících zdrojů:  

- Přečtěte si chybové zprávy a opravy v [technických informacích o chybových zprávách správce převodu balíčků](error-messages.md) .  

- Zkontrolujte soubor protokolu **PCMTrace. log.**  

- [Řešení potíží s nástrojem Package Conversion Manager](troubleshoot-pcm.md)  

#### <a name="convert-the-packages"></a>Převést balíčky

Další informace o tom, jak převést balíčky, najdete v tématu [jak analyzovat a převádět balíčky](how-to-analyze-and-convert.md).

> [!NOTE]  
> Viz uzel **stav převodu balíčku** v pracovním prostoru **monitorování** . Zobrazuje souhrnné informace o procesech analýzy a převodu.  


### <a name="test-and-deploy-the-applications"></a><a name="bkmk_deploy"></a>Testování a nasazení aplikací

Otestujte aplikace buď v testovacím prostředí, nebo v produkčním prostředí podle vašeho podrobného plánu převodu balíčků.



## <a name="recommendations"></a>Doporučení

- V pracovním prostoru **monitorování** použijte uzel **stav převodu balíčku** . Zobrazuje souhrnné informace o procesech analýzy a převodu.  

- Prozkoumejte programy v balíčcích označované jako obálky. Pomocí modulu plug-in Package Conversion Manager můžete převést své funkce na ekvivalentní Configuration Manager funkce.  

- Před nasazením v produkčním prostředí se ujistěte, že jste všechny převedené aplikace důkladně otestovali.  



## <a name="next-steps"></a>Další kroky

[Jak analyzovat a převést balíčky](how-to-analyze-and-convert.md)
