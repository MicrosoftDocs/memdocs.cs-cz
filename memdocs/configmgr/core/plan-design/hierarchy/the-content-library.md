---
title: Knihovna obsahu
titleSuffix: Configuration Manager
description: Přečtěte si o knihovně obsahu, kterou Configuration Manager používá ke snížení celkové velikosti distribuovaného obsahu.
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 253de522937e48fa1f3939c7303faf7e43e4e047
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720895"
---
# <a name="the-content-library-in-configuration-manager"></a>Knihovna obsahu v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Knihovna obsahu je úložiště obsahu s jednou instancí v Configuration Manager. Lokalita ji používá ke snížení celkové velikosti kombinovaného obsahu, který distribuujete. Knihovna obsahu ukládá všechny soubory obsahu pro nasazení softwaru, například: aktualizace softwaru, aplikace a nasazení operačního systému.  

- Lokalita automaticky vytvoří a udržuje kopii knihovny obsahu na každém serveru lokality a v každém distribučním bodě.  

- Předtím, než nástroj Configuration Manager přidá soubory obsahu na server lokality nebo zkopíruje soubory do distribučních bodů, ověří, zda je každý soubor obsahu již v knihovně obsahu.  

- Pokud je soubor obsahu dostupný, Configuration Manager soubor nezkopíruje. Místo toho přidruží existující soubor obsahu k aplikaci nebo balíčku.  

Na serverech distribučního bodu nakonfigurujte následující možnosti:

- Jedna nebo více diskových jednotek, na kterých chcete vytvořit knihovnu obsahu.  

- Priorita pro každou jednotku, kterou používáte.  

Configuration Manager zkopíruje soubory obsahu na jednotku s nejvyšší prioritou, dokud tato jednotka nebude obsahovat méně než minimální volné místo, které zadáte.  

- Nastavení jednotky můžete konfigurovat během instalace distribučního bodu.  

- Po dokončení instalace nemůžete konfigurovat nastavení jednotky ve vlastnostech distribučního bodu.  

Další informace o konfiguraci nastavení jednotky pro distribuční bod najdete v tématu [Správa obsahu a infrastruktury obsahu](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

> [!IMPORTANT]
> Chcete-li po instalaci přesunout knihovnu obsahu do jiného umístění v distribučním bodě, použijte nástroj pro **přenos knihovny obsahu** v nástrojích Configuration Manager. Další informace najdete v tématu [Nástroj pro přenos knihovny obsahu](../../support/content-library-transfer.md).  


## <a name="about-the-content-library-on-the-central-administration-site"></a>O knihovně obsahu v lokalitě centrální správy

Ve výchozím nastavení Configuration Manager vytvoří při instalaci lokality knihovnu obsahu v lokalitě centrální správy. Knihovna obsahu je umístěna na jednotce serveru lokality, která má nejvíce volného místa na disku. Vzhledem k tomu, že nemůžete nainstalovat distribuční bod v lokalitě centrální správy, nemůžete určit prioritu jednotek pro použití knihovnou obsahu. Podobně jako u knihovny obsahu na jiných serverech lokality a v distribučních bodech, pokud jednotka obsahující knihovnu obsahu vychází z dostupného místa na disku, knihovna obsahu se automaticky rozpíná na další dostupnou jednotku.  

Configuration Manager používá knihovnu obsahu v lokalitě centrální správy v následujících situacích:  

- Obsah se vytváří v lokalitě centrální správy.  

- Migrujete obsah z jiné Configuration Manager lokality a přiřadíte lokalitu centrální správy jako lokalitu, která tento obsah spravuje.  

> [!NOTE]  
> Když vytvoříte obsah v primární lokalitě a pak ho distribuujete do jiné primární lokality nebo sekundární lokality pod jinou primární lokalitou, lokalita centrální správy dočasně uloží tento obsah do složky Doručená pošta Scheduleru v lokalitě centrální správy, ale nepřidá tento obsah do knihovny obsahu.  

Ke správě knihovny obsahu v lokalitě centrální správy použijte následující možnosti:  

- Chcete-li zabránit instalaci knihovny obsahu na konkrétní jednotku, vytvořte prázdný soubor s názvem **NO_SMS_ON_DRIVE. SMS**. Před vytvořením knihovny obsahu ji zkopírujte do kořenového adresáře jednotky.  

- Po vytvoření knihovny obsahu můžete pomocí nástroje pro **přenos knihovny obsahu** z nástrojů Configuration Manager spravovat umístění knihovny obsahu. Další informace najdete v tématu [Nástroj pro přenos knihovny obsahu](../../support/content-library-transfer.md).  

> [!Note]  
> Distribuční body cloudu nepoužívají úložiště s jednou instancí. Lokalita před odesláním do Azure zašifruje balíčky a každý balíček má jedinečný šifrovaný klíč. I v případě, že dva soubory byly identické, šifrované verze by nemusely být stejné.  


## <a name="configure-a-remote-content-library-for-the-site-server"></a><a name="bkmk_remote"></a>Konfigurace vzdálené knihovny obsahu pro server lokality

<!--1357525-->
Pokud chcete nakonfigurovat [vysokou dostupnost webového serveru](../../servers/deploy/configure/site-server-high-availability.md) nebo uvolnit místo na pevném disku na serverech centrální správy nebo primárních lokalit, začněte ve verzi 1806, přemístěte knihovnu obsahu do jiného umístění úložiště. Přesuňte knihovnu obsahu na jinou jednotku na serveru lokality, na samostatný server nebo disky odolné vůči chybám v síti SAN (Storage Area Network). Doporučuje se síť SAN, protože je vysoce dostupná a poskytuje elastické úložiště, které se v průběhu času zvětšuje nebo zmenšuje, aby splňovaly požadavky na změnu obsahu. Další informace najdete v tématu [Možnosti vysoké dostupnosti](../../servers/deploy/configure/site-server-high-availability.md).

Vzdálená knihovna obsahu je předpokladem pro [vysokou dostupnost serveru lokality](../../servers/deploy/configure/site-server-high-availability.md).

> [!Note]  
> Tato akce přesune obsah knihovny obsahu na serveru lokality. Nemá vliv na umístění knihovny obsahu v distribučních bodech. 

> [!Tip]  
> Také Naplánujte správu zdrojového obsahu balíčku, který je externě knihovnou obsahu. Každý softwarový objekt v Configuration Manager má zdroj balíčku ve sdílené síťové složce. Zvažte centralizaci všech zdrojů do jediné sdílené složky, ale ujistěte se, že je toto umístění redundantní a vysoce dostupné.
>
> Pokud přesunete knihovnu obsahu do stejného svazku úložiště jako zdroje balíčků, nemůžete tento svazek označit pro odstranění duplicitních dat. I když knihovna obsahu podporuje odstranění duplicitních dat, svazek zdroje balíčku ho nepodporuje. Další informace najdete v tématu [odstranění duplicitních dat](../configs/support-for-windows-features-and-networks.md#bkmmk_datadedup).<!--SCCMDOcs issue #831-->  

### <a name="prerequisites"></a>Požadavky  

- Účet počítače serveru lokality potřebuje oprávnění **Úplné řízení** k síťové cestě, do které přesouváte knihovnu obsahu. Toto oprávnění platí jak pro sdílenou složku, tak pro systém souborů. Ve vzdáleném systému nejsou nainstalovány žádné součásti.

- Webový server nemůže mít roli distribučního bodu. Distribuční bod také používá knihovnu obsahu a tato role nepodporuje vzdálenou knihovnu obsahu. Po přesunutí knihovny obsahu nelze přidat roli distribučního bodu do serveru lokality.  

> [!Important]  
> Neprovádějte opakované použití sdíleného síťového umístění mezi více lokalitami. Nepoužívejte například stejnou cestu jak pro lokalitu centrální správy, tak pro podřízenou primární lokalitu. Tato konfigurace má potenciál poškodit knihovnu obsahu a vyžadovat, abyste ji znovu sestavili.<!--SCCMDocs-pr issue 2764-->  

### <a name="process-to-manage-the-content-library"></a>Postup správy knihovny obsahu

1. Vytvořte složku ve sdílené síťové složce jako cíl pro knihovnu obsahu. Například, `\\server\share\folder`.  

    > [!Warning]  
    > Nepoužívejte znovu existující složku s obsahem. Nepoužívejte například stejnou složku jako zdroje balíčků. Před kopírováním knihovny obsahu Configuration Manager odebere veškerý existující obsah z umístění, které zadáte.  

2. V konzole Configuration Manager přepněte do pracovního prostoru **Správa** . Rozbalte položku **Konfigurace lokality**, vyberte uzel **lokality** a vyberte lokalitu. Na kartě **Souhrn** v dolní části podokna podrobností si všimněte nového sloupce pro **knihovnu obsahu**.  

3. Na pásu karet vyberte **Spravovat knihovnu obsahu** .  

4. V okně Spravovat knihovnu obsahu se v poli **aktuální umístění** zobrazuje místní jednotka a cesta. Zadejte platnou síťovou cestu pro **nové umístění**. Tato cesta je umístění, do kterého lokalita přesouvá knihovnu obsahu. Musí obsahovat název složky, který již ve sdílené složce existuje, například `\\server\share\folder`. Vyberte **OK**.  

5. Poznamenejte si hodnotu **stav** ve sloupci knihovna obsahu na kartě Souhrn v podokně podrobností. Aktualizuje a zobrazí průběh přesunutí knihovny obsahu.  

   - **V průběhu probíhá**hodnota **přesunu (%)** , která je dokončená v procentech.  

        > [!Note]  
        > Pokud máte rozsáhlou knihovnu obsahu, může se po chvíli `0%` zobrazit průběh v konzole. Například s knihovnou 1 TB musí kopírovat 10 GB před tím, než se zobrazí `1%`. Zkontrolujte **Distmgr. log**, který zobrazuje počet zkopírovaných souborů a bajtů. Počínaje verzí 1810 se v souboru protokolu zobrazuje také Odhadovaný zbývající čas.

   - Pokud dojde k chybovém stavu, zobrazí se ve stavu chyba. K běžným chybám patří **odepřený přístup** nebo **disk je plný**.  

   - Po dokončení se zobrazí **Dokončená**.  

     Podrobnosti najdete v **protokolu Distmgr. log** . Další informace najdete v tématu [protokoly serveru lokality a serveru systému lokality](log-files.md#BKMK_SiteSiteServerLog).  

Další informace o tomto procesu najdete v tématu [vývojový diagram – Správa knihovny obsahu](manage-content-library-flowchart.md).

Lokalita ve skutečnosti *kopíruje* soubory knihovny obsahu do vzdáleného umístění. Tento proces neodstraní soubory knihovny obsahu v původním umístění na serveru lokality. Aby bylo možné uvolnit místo, správce musí tyto původní soubory ručně odstranit.

Pokud původní Knihovna obsahu zahrnuje dvě jednotky, sloučí se do jediné složky v novém cílovém umístění.

V rámci verze 1810 se během kopírování nezpracovávají součásti pro **vyřazování** a **správu distribuce** nové balíčky. Tato akce zajistí, že se obsah během přesouvání nepřidá do knihovny. Tuto změnu při údržbě systému Naplánujte bez ohledu na tuto změnu.

Pokud potřebujete přesunout knihovnu obsahu zpět na server lokality, opakujte tento postup, ale zadejte místní jednotku a cestu k **novému umístění**. Musí obsahovat název složky, který již na disku existuje, například `D:\SCCMContentLib`. Když původní obsah stále existuje, proces rychle přesune konfiguraci do umístění místního serveru lokality.

> [!Tip]  
> Chcete-li přesunout obsah na jinou jednotku na serveru lokality, použijte nástroj pro **přenos knihovny obsahu** . Další informace najdete v tématu [Nástroj pro přenos knihovny obsahu](../../support/content-library-transfer.md).  


## <a name="inside-the-content-library"></a>V knihovně obsahu

> [!Warning]  
> Následující část je k dispozici pouze pro informativní účely. Neměňte, nepřidávejte ani neodstraňujte žádné soubory nebo složky v knihovně obsahu. V takovém případě by mohlo dojít k poškození balíčků, obsahu nebo knihovny obsahu jako celku. Pokud máte podezření, že některá chybějící, poškozená nebo jinak neplatná data, použijte funkci ověřování v konzole Configuration Manager k detekci takových problémů. Pak příslušný obsah znovu distribuujte a opravte problémy.

Ve výchozím nastavení se knihovna obsahu ukládá do kořenového adresáře jednotky ve složce s názvem **SCCMContentLib**. Tato složka je ve výchozím nastavení sdílena jako **SCCMContentLib $**. Složka a sdílená složka mají omezená oprávnění, aby nedocházelo k náhodnému poškození. Všechny změny by se měly provádět z konzoly Configuration Manager. V této složce jsou následující objekty:  

- Knihovna balíčku (**PkgLib** složka): informace o tom, jaké balíčky jsou v distribučním bodě k dispozici.  

- Knihovna dat (složka**DataLib** ): informace o původní struktuře balíčků.  

- Knihovna souborů (složka**filelib** ): původní soubory v balíčku. Tato složka obvykle využívá hromadné úložiště.  

![Přehled diagramu Configuration Manager knihovny obsahu](media/content-library-overview.png)

> [!Tip]  
> Pomocí nástroje **Průzkumník knihovny obsahu** z nástrojů pro Configuration Manager můžete procházet obsah knihovny obsahu. Tento nástroj nelze použít pro úpravu obsahu. Poskytuje přehled o tom, co je k dispozici, a umožňuje ověření a redistribuci. Další informace najdete v tématu [Průzkumník knihovny obsahu](../../support/content-library-explorer.md).  

### <a name="package-library"></a>Knihovna balíčků

Složka knihovny balíčků **PkgLib**obsahuje jeden soubor pro každý balíček distribuovaný do distribučního bodu. Název souboru je ID balíčku, například `ABC00001.INI`. V tomto souboru v `[Packages]` části je seznam ID obsahu, který je součástí balíčku, a další informace, jako je například verze. Například **ABC00001** je starší balíček ve verzi **1**. ID obsahu v tomto souboru je `ABC00001.1`.

### <a name="data-library"></a>Knihovna dat

Složka knihovny dat **DataLib**obsahuje jeden soubor a jednu složku pro každý obsah v každém balíčku. Například tento soubor a složka jsou pojmenované `ABC00001.1.INI` a `ABC00001.1`v uvedeném pořadí. Soubor obsahuje informace pro ověření. Složka znovu vytvoří strukturu složky z původního balíčku.

Soubory v knihovně dat jsou nahrazeny soubory INI s názvem původního souboru v balíčku. Například, `MyFile.exe.INI`. Tyto soubory obsahují informace o původním souboru, jako je například velikost, čas změny a hodnota hash. Použijte první čtyři znaky hash k vyhledání původního souboru v knihovně souborů. Například hodnota hash v souboru MyFile. exe. INI je **DEF98765**a první čtyři znaky jsou **DEF9**.

### <a name="file-library"></a>Knihovna souborů

Pokud knihovna obsahu zahrnuje více jednotek, mohou být soubory balíčku ve složce knihovny souborů **filelib**na kterékoli z těchto jednotek.

Vyhledá konkrétní soubor pomocí prvních čtyř znaků z hodnoty hash, která se nachází v knihovně dat. V rámci složky knihovny souborů je to mnoho složek, z nichž každý má název se čtyřmi znaky. Vyhledá složku, která odpovídá prvních čtyř znakům z hodnoty hash. Po nalezení této složky obsahuje jednu nebo více sad tří souborů. Tyto soubory mají stejný název, ale jeden z nich má příponu INI, jedna má příponu SIG a jedna nemá příponu souboru. Původní soubor je ten bez přípony, jehož název je stejný jako hodnota hash z knihovny dat.

Například složka **DEF9** zahrnuje `DEF98765.INI`, `DEF98765.SIG`a. `DEF98765` `DEF98765`je původní `MyFile.exe`. Soubor INI obsahuje seznam uživatelů nebo ID obsahu, které sdílejí stejný soubor. Lokalita soubor neodebere, pokud není odstraněn také celý tento obsah.

### <a name="drive-spanning"></a>Pokrývání jednotky

Knihovna obsahu může být rozložená mezi několik jednotek. Tyto jednotky zvolíte při vytváření distribučního bodu. Ve výchozím nastavení Configuration Manager automaticky zvolí jednotky při pokrývání knihovny obsahu.

Po výběru jednotek vyberte primární a sekundární jednotku. Lokalita uchovává všechna metadata na primární jednotce. Pouze pokrývá knihovnu souborů napříč sekundární jednotkou. Název sdílené složky pro sekundární jednotky obsahuje písmeno jednotky. Pokud například D: a E: jsou sekundárními jednotkami pro knihovnu obsahu, názvy sdílených složek jsou **SCCMContentLibD $** a **SCCMContentLibE $**.

Pokud jste zvolili možnost **automaticky** , Configuration Manager vybere jednotku s největším množstvím dostupného volného místa jako jeho primární disk. Všechna metadata na této jednotce se uloží. Lokalita pokrývá pouze souborové knihovny napříč sekundárními jednotkami.

Během konfigurace zadáte množství rezervovaného prostoru. Configuration Manager se pokusí použít sekundární disk, protože nejlepší dostupný disk má pouze tuto částku rezervovaného místa zbývající zdarma. Pokaždé, když se vybere nová jednotka pro použití, vybere se jednotka s největším dostupným volným místem.

Nemůžete určit, že distribuční bod by měl používat všechny jednotky kromě konkrétní sady. Zabraňte tomuto chování vytvořením prázdného souboru v kořenovém adresáři jednotky, která `NO_SMS_ON_DRIVE.SMS`je volána. Tento soubor umístěte před Configuration Manager vybere jednotku, která se má použít. Pokud Configuration Manager zjistí tento soubor na kořenovém adresáři jednotky, nepoužije jednotku pro knihovnu obsahu.


## <a name="troubleshooting"></a>Řešení potíží

Následující tipy vám můžou pomoct při odstraňování problémů s knihovnou obsahu:  

- Zkontrolujte protokoly na serveru lokality (**Distmgr. log** a **PkgXferMgr. log**) a distribuční bod (**Smsdpprov. log**) pro všechny ukazatele na chyby.  

- Použijte nástroj [Průzkumník knihovny obsahu](../../support/content-library-explorer.md) .  

- Vyhledat zámky souborů jinými procesy, například antivirovým softwarem. Vylučte knihovnu obsahu na všech jednotkách z automatických antivirových kontrol a také dočasné pracovní adresáře **SMS_DP $**, na jednotlivých jednotkách.  

- Pokud chcete zjistit, jestli nedošlo k žádným hodnotám hash, ověřte balíček z konzoly Configuration Manager.  

- Jako poslední možnost znovu distribuujte obsah. Tato akce by měla vyřešit většinu problémů.  
