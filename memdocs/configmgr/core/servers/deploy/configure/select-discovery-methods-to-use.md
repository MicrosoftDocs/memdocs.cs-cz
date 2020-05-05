---
title: Výběr metod zjišťování
titleSuffix: Configuration Manager
description: Přečtěte si o tom, jaké metody se mají použít a na kterých lokalitách je spustit.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 127ce713-d085-430f-ac7b-2701637fe126
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2f08ab44a11b48b4446a372c4f6065ea0d7c63e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718347"
---
# <a name="select-discovery-methods-to-use-for-configuration-manager"></a>Vyberte metody zjišťování, které se mají použít pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Chcete-li úspěšně a efektivně používat zjišťování pro Configuration Manager, je nutné zvážit, jaké metody se mají použít a na kterých lokalitách je lze spustit.  

 Vzhledem k tomu, že zjišťování může způsobit velké množství síťových přenosů, a výsledné záznamy dat zjišťování (DDR) můžou během zpracování využívat významné prostředky procesoru, používejte jenom ty metody zjišťování, které pro splnění svých cílů potřebujete. Můžete začít používat jenom jednu nebo dvě metody zjišťování a potom později povolit další metody, aby se rozšířila úroveň zjišťování ve vašem prostředí. Informace v tomto tématu vám můžou usnadnit rozhodování.  

 Informace o různých metodách zjišťování najdete v tématu [o metodách zjišťování pro Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  

## <a name="select-methods-to-discover-different-things"></a>Vyberte metody pro zjišťování různých věcí  
 Chcete-li zjistit potenciální Configuration Manager klientských počítačů nebo uživatelských prostředků, je nutné povolit příslušné metody zjišťování. Můžete použít různé kombinace metod zjišťování k vyhledání různých zdrojů a zjištění dalších informací o těchto prostředcích. Metody zjišťování, které použijete, určují typ prostředků, které jsou zjištěny a které Configuration Manager služby a agenti jsou používány v procesu zjišťování. Určují také typ informací o prostředcích, které můžete zjistit.  

### <a name="discover-computers"></a>Zjistit počítače   
Pokud chcete zjišťovat počítače, můžete použít **zjišťování systému služby Active Directory** nebo **zjišťování sítě**.  

 Například pokud chcete zjistit prostředky, které mohou nainstalovat klienta Configuration Manager před použitím nabízené instalace klienta, můžete spustit zjišťování systému služby Active Directory. Pomocí této metody nezjistíte pouze prostředek, ale také základní informace o tom, jak se nachází v Active Directory Domain Services. Tyto informace mohou být užitečné při vytváření složitých dotazů a kolekcí, které slouží k přiřazení nastavení klienta nebo nasazení obsahu.

Případně můžete spustit zjišťování sítě a pomocí jeho možností zjistit operační systém prostředků (vyžaduje se pro pozdější použití nabízené instalace klientů). Zjišťování sítě poskytuje informace o topologii sítě, které nemůžete získat s jinými metodami zjišťování. Tato metoda ale neposkytuje žádné informace o prostředí služby Active Directory.

 K dispozici je také metoda s názvem **zjišťování prezenčního signálu**. Je možné použít jenom zjišťování prezenčního signálu k vynucení zjišťování klientů, které jste nainstalovali pomocí jiných metod než nabízené instalace klienta. Na rozdíl od jiných metod zjišťování ale zjišťování prezenčního signálu nemůže najít počítače, které nemají aktivního Configuration Manager klienta. Vrátí omezené sady informací, jejichž cílem je zachovat existující záznam databáze, a ne být základem daného záznamu. Informace odeslané zjišťováním prezenčního signálu nemusí být dostačující pro vytváření složitých dotazů nebo kolekcí.  

 Pokud ke zjištění členství zadané skupiny používáte **zjišťování skupiny služby Active Directory** , můžete zjistit omezené informace o systému nebo počítači. To nenahrazuje úplné zjišťování počítačů, ale může poskytovat základní informace. Tyto informace jsou pro nabízenou instalaci klienta nedostatečné.  

### <a name="discover-users"></a>Vyhledat uživatele   
Pokud chcete zjišťovat informace o uživatelích, použijte **zjišťování uživatelů služby Active Directory**. Podobně jako zjišťování systému služby Active Directory Tato metoda zjišťuje uživatele ze služby Active Directory. Zahrnuje základní informace kromě rozšířených informací služby Active Directory. Tyto informace můžete použít k vytvoření složitých dotazů a kolekcí podobně jako u počítačů.  

### <a name="discover-group-information"></a>Zjistit informace o skupině   
Pokud chcete zjišťovat informace o skupinách a členství ve skupinách, použijte **zjišťování skupin služby Active Directory**. Tato metoda zjišťování vytváří záznamy o prostředcích pro skupiny zabezpečení.  

 Tuto metodu můžete použít k vyhledání konkrétní skupiny služby Active Directory a identifikaci členů této skupiny, a to i u všech vnořených skupin v této skupině. Tato metoda slouží také k hledání skupin v umístění služby Active Directory a rekurzivnímu hledání jednotlivých podřízených kontejnerů v daném umístění služby Active Directory Domain Services.  

 Tato metoda zjišťování může také vyhledat členství v distribučních skupinách. Můžete tak identifikovat vztahy skupin uživatelů i počítačů.  

 Když zjistíte skupinu, můžete také zjistit omezené informace o jejích členech. To ale nenahrazuje metody zjišťování systému ani uživatele služby Active Directory. Obvykle není dostatek k vytváření složitých dotazů a kolekcí nebo slouží jako základ klientské nabízené instalace.  

### <a name="discover-infrastructure"></a>Zjišťování infrastruktury   
Existují dvě metody, které můžete použít ke zjišťování síťové infrastruktury, **zjišťování doménové struktury služby Active Directory** a **zjišťování sítě**.  

 Zjišťování doménové struktury služby Active Directory můžete použít k vyhledání informací o podsítích a konfiguracích lokality služby Active Directory v doménové struktuře služby Active Directory. Tyto konfigurace je pak možné automaticky zadat do Configuration Manager jako umístění hranic.  

 Pokud chcete zjistit topologii sítě, použijte zjišťování sítě. Zatímco jiné metody zjišťování vracejí informace týkající se Active Directory Domain Services a mohou identifikovat aktuální umístění sítě klienta, neposkytují informace o infrastruktuře v závislosti na topologii podsítě a směrovače vaší sítě.  

##  <a name="discovery-data-is-shared-among-sites"></a><a name="bkmk_shared"></a>Data zjišťování se sdílejí mezi lokalitami.  
 Jakmile Configuration Manager přidá data zjišťování do databáze, bude se rychle sdílet mezi všemi lokalitami v hierarchii. Vzhledem k tomu, že některé informace ve více lokalitách ve vaší hierarchii obvykle nejsou vhodné ke zjišťování stejných informací, zvažte nastavení jedné instance každé metody zjišťování, kterou používáte pro spuštění v jedné lokalitě. To je vhodné provést místo spuštění více instancí jedné metody v různých lokalitách.  

 V některých prostředích ale může být užitečné přiřadit stejnou metodu zjišťování pro spuštění ve více lokalitách, z nichž každá má samostatnou konfiguraci a plán. Pokud například používáte zjišťování sítě, můžete chtít směrovat jednotlivé lokality, abyste zjistili svou místní síť, a nemusíte přitom zkoušet všechna síťová umístění v síti WAN.

Pokud nakonfigurujete více instancí stejných metod zjišťování, které se mají spouštět v různých lokalitách, naplánujte pečlivě konfiguraci každé lokality. Chcete zabránit tomu, aby dvě nebo více lokalit zjistilo stejné prostředky ze sítě nebo služby Active Directory. To může spotřebovávat další šířku pásma sítě a vytvářet duplicitní záznamy DDR.

Následující tabulka uvádí, na kterých lokalitách můžete nastavit různé metody zjišťování.  

|Metoda zjišťování|Podporovaná umístění|  
|----------------------|-------------------------|  
|Zjišťování lokalit a podsítí v doménových strukturách služby Active Directory|Lokalita centrální správy<br /><br /> Primární lokalita|  
|Zjišťování skupiny aktivního adresáře|Primární lokalita|  
|Zjišťování systému aktivního adresáře|Primární lokalita|  
|Zjišťování uživatele Active Directory|Primární lokalita|  
|Zjišťování prezenčního signálu<sup>1</sup>|Primární lokalita|  
|Zjištění sítě|Primární lokalita<br /><br /> Sekundární lokalita|  

 <sup>1</sup> sekundární lokality nemůžou konfigurovat zjišťování prezenčního signálu, ale můžou z klienta přijímat prezenční signály DDR.  

 Když sekundární lokality spustí zjišťování sítě nebo obdrží DDR zjišťování prezenčního signálu, přenesou záznam DDR pomocí replikace na základě souborů do své nadřazené primární lokality. Důvodem je, že pouze primární lokality a lokality centrální správy mohou zpracovávat záznamy DDR. Další informace o zpracování záznamů DDR najdete v tématu [informace o datech zjišťování](../../../../core/servers/deploy/configure/run-discovery.md#BKMK_DDRs).  

## <a name="considerations-for-different-discovery-methods"></a>Požadavky na různé metody zjišťování  
 Vzhledem k tomu, že každý server lokality a síťové prostředí je jiný, je vhodné omezit počáteční konfiguraci pro zjišťování. Pak pečlivě Sledujte každý server lokality, aby bylo možné zpracovat vygenerovaná data zjišťování.  

Pokud používáte metodu zjišťování **služby Active Directory** pro systémy, uživatele nebo skupiny:  

-   Spusťte funkci zjišťování v lokalitě, která má rychlé síťové připojení k řadičům domény.  

-   Prohlédněte si topologii replikace Active Directory, abyste zajistili, že zjišťování bude mít přístup k nejnovějším informacím.  

-   Vezměte v úvahu rozsah konfigurace zjišťování a omezte zjišťování jenom na umístění a skupiny služby Active Directory, které chcete zjistit.  

Pokud používáte **zjišťování sítě**:  

-   K identifikaci topografie vaší sítě použijte omezené počáteční konfiguraci.  

-   Po identifikaci topografie sítě nastavte zjišťování sítě tak, aby běželo v konkrétních lokalitách, které jsou centrální pro oblasti sítě, které chcete efektivněji zjišťovat.  

Vzhledem k tomu, že **zjišťování prezenčního signálu** není spuštěno v konkrétní lokalitě, nemusíte ho brát v úvahu při obecném plánování, kde spustit zjišťování.  

##  <a name="best-practices-for-discovery"></a><a name="bkmk_best"></a>Osvědčené postupy pro zjišťování  
Pro dosažení nejlepších výsledků se zjišťováním doporučujeme následující:

- **Před spuštěním zjišťování skupin služby Active Directory spusťte zjišťování systému služby Active Directory a zjišťování uživatelů služby Active Directory.**  

  Když funkce zjišťování skupiny služby Active Directory identifikuje dříve nenalezeného uživatele nebo počítač jako člena skupiny, pokusí se vyhledat základní podrobnosti pro uživatele nebo počítač. Vzhledem k tomu, že funkce zjišťování skupiny služby Active Directory není pro tento typ zjišťování optimalizovaná, může tento proces způsobit zpomalení. Kromě toho funkce zjišťování skupiny služby Active Directory identifikuje jenom základní podrobnosti o uživatelích a počítačích, které zjistí, a nevytvoří úplný záznam zjišťování uživatele nebo počítače. Když spustíte zjišťování systému služby Active Directory a zjišťování uživatelů služby Active Directory, jsou k dispozici další atributy služby Active Directory pro každý typ objektu. Výsledkem je, že zjišťování skupin služby Active Directory běží efektivněji.  

- **Když nastavujete zjišťování skupin služby Active Directory, určete pouze skupiny, které používáte s Configuration Manager.**  

  Chcete-li lépe řídit používání prostředků podle zjišťování skupin služby Active Directory, zadejte pouze ty skupiny, které používáte s Configuration Manager. Je to proto, že funkce zjišťování skupiny služby Active Directory rekurzivně vyhledává jednotlivé skupiny uživatelů, počítačů a vnořených skupin. Hledání každé vnořené skupiny může rozšířit rozsah zjišťování skupiny služby Active Directory a snížit výkon. Kromě toho, když nastavíte zjišťování rozdílů pro zjišťování skupin služby Active Directory, metoda zjišťování sleduje změny v jednotlivých skupinách. Tím se snižuje výkon, pokud metoda musí hledat zbytečné skupiny.  

- **Nastavte metody zjišťování s delším intervalem pro úplné zjišťování a častým obdobím zjišťování rozdílů.**  

  Vzhledem k tomu, že zjišťování rozdílů používá méně prostředků než plný cyklus zjišťování a dokáže identifikovat nové nebo upravené prostředky ve službě Active Directory, můžete snížit četnost úplných cyklů zjišťování, které se mají spouštět týdně (nebo méně). Zjišťování rozdílů pro zjišťování systémových prostředků služby Active Directory, zjišťování uživatelů služby Active Directory a zjišťování skupin služby Active Directory identifikuje téměř všechny změny objektů služby Active Directory a může udržovat přesná data zjišťování pro prostředky.  

- **Spusťte metody zjišťování služby Active Directory v primární lokalitě, která má síťové umístění, které je nejblíže vašemu řadiči domény služby Active Directory.**  

  Chcete-li zlepšit výkon zjišťování služby Active Directory, je vhodné spustit zjišťování v primární lokalitě, která má rychlé síťové připojení k řadičům domény. Pokud spustíte stejnou metodu zjišťování služby Active Directory ve více lokalitách, nastavte každou metodu zjišťování tak, aby se předešlo překrytí. Na rozdíl od minulých verzí Configuration Manager jsou data zjišťování sdílena mezi lokalitami. Proto není nutné zjišťovat stejné informace ve více lokalitách. Další informace najdete v tématu [data zjišťování se sdílejí mezi lokalitami](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md#bkmk_shared).  

- **Zjišťování doménové struktury služby Active Directory spouštějte jenom v jedné lokalitě, když plánujete automatické vytváření hranic z dat zjišťování.**  

  Pokud spouštíte zjišťování doménové struktury služby Active Directory ve více než jedné lokalitě v hierarchii, je vhodné povolit možnosti pro automatické vytváření hranic v jedné lokalitě. Důvodem je to, že když se v každé lokalitě spustí zjišťování doménové struktury služby Active Directory a vytvoří hranice, Configuration Manager nemůže sloučit tyto hranice do jediného objektu hranice. Když konfigurujete funkci zjišťování doménové struktury služby Active Directory tak, aby automaticky vytvářela hranice na více lokalitách, může být výsledkem duplikované objekty hranice v konzole Configuration Manager.  
