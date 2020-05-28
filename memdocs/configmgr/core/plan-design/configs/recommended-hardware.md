---
title: Doporučený hardware
titleSuffix: Configuration Manager
description: Získejte Hardwarová doporučení, která vám pomůžou škálovat Configuration Manager prostředí nad rámec základního nasazení.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 36b90627f25c5cf19b867a78e141b69266478c58
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428782"
---
# <a name="recommended-hardware-for-configuration-manager"></a>Doporučený hardware pro nástroj Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Následující doporučení jsou pokyny, které vám pomohou škálovat Configuration Manager prostředí, aby podporovaly více než velmi základní nasazení lokalit, systémů lokalit a klientů. Nejsou určené k pokrytí všech možných konfigurací lokality a hierarchie.  

Informace v následujících částech použijte jako vodítko, které vám pomohou při plánování hardwaru. Ujistěte se, že hardware může splňovat zátěže zpracování pro klienty a weby, které používají dostupné funkce Configuration Manager.

Další informace najdete v tématu [dokumentace k Configuration Manager výkon a škálování](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e).

## <a name="site-systems"></a><a name="bkmk_ScaleSieSystems"></a>Systémy lokality

Tato část poskytuje doporučené hardwarové konfigurace pro Configuration Manager systémy lokality. Tato doporučení použijte k podpoře maximálního počtu klientů a používání většiny nebo všech Configuration Manager funkcí. Pokud vaše prostředí podporuje méně než maximální počet klientů a nepoužívá všechny dostupné funkce, může to vyžadovat méně prostředků. Obecně platí, že následující klíčové faktory omezují výkon celkového systému:

1. Výkon diskových operací

2. Dostupná paměť

3. Procesor

Nejlepšího výkonu dosáhnete, když použijete konfiguraci RAID 10 pro všechny datové jednotky a síť Ethernet s rychlostí 1 GB/s.

### <a name="site-servers"></a><a name="bkmk_ScaleSiteServer"></a>Servery lokality

|Konfigurace lokality|PROCESOR (jádra)|Paměť (GB)|Přidělení paměti pro SQL Server (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Samostatný server primární lokality s rolí databázového serveru na stejném serveru <sup> [Poznámka 1](#bkmk_note1)</sup>|16|96|80|  
|Server samostatné primární lokality se vzdálenou databází lokality|8|16|-|  
|Vzdálený databázový server pro samostatnou primární lokalitu|16|72|90|  
|Server lokality centrální správy s rolí databázového serveru na stejném serveru <sup> [Poznámka 1](#bkmk_note1)</sup>|20|128|80|  
|Server lokality centrální správy se vzdálenou databází lokality|8|16|-|  
|Vzdálená databázový server pro lokalitu centrální správy|16|96|90|  
|Podřízená primární lokalita s rolí databázového serveru na stejném serveru|16|96|80|  
|Server podřízené primární lokality se vzdálenou databází lokality|8|16|-|  
|Vzdálený databázový server pro podřízenou primární lokalitu|16|72|90|  
|Server sekundární lokality|8|16|-|  

#### <a name="note-1-collocated-sql"></a><a name="bkmk_note1"></a>Poznámka 1: společně umístěného SQL

Když nainstalujete server lokality a SQL Server ve stejném počítači, nasazení podporuje maximální [hodnoty velikosti a škálování](size-and-scale-numbers.md) pro lokality a klienty. Tato konfigurace může omezit [Možnosti vysoké dostupnosti](../../servers/deploy/configure/high-availability-options.md), jako je například použití clusteru SQL Server. Pokud máte větší prostředí, z důvodu vyšších požadavků na vstupně-výstupní operace pro podporu obou rolí na stejném počítači zvažte použití vzdáleného SQL Server.

### <a name="remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a>Vzdálené servery systému lokality

Následující pokyny jsou pro počítače, které obsahují jednu roli systému lokality. Naplánujte úpravu při instalaci více rolí systému lokality do stejného počítače.

|Role systému lokality|PROCESOR (jádra)|Paměť (GB)|Místo na disku (GB)|  
|----------------------|---------------|---------------|--------------------|  
|Bod správy|4|8|50|  
|Distribuční bod|2|8|Podle požadavků operačního systému a ukládání obsahu, který nasazujete|  
|Poznámka k bodu aktualizace softwaru <sup> [2](#bkmk_note2)</sup>|8|16|Podle požadavků operačního systému a ukládání aktualizací, které nasadíte|  
|Všechny ostatní role systémů lokalit|4|8|50|  

#### <a name="note-2-wsus-configurations"></a><a name="bkmk_note2"></a>Poznámka 2: Konfigurace služby WSUS

Počítač, který je hostitelem bodu aktualizace softwaru, vyžaduje následující konfigurace pro fondy aplikací IIS:  

- Zvyšte **délku fronty nastavení WsusPool** na **2000**.  

- Zvyšte **limit soukromé paměti nastavení WsusPool** o čtyřikrát nebo ji nastavte na **0** (neomezeno).  

### <a name="disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a>Místo na disku pro systémy lokality

Přidělení a konfigurace disku přispívají k výkonu Configuration Manager. Vzhledem k tomu, že se každé Configuration Manager prostředí liší, hodnoty, které implementujete, se můžou lišit od následujících pokynů.

Nejlepšího výkonu dosáhnete umístěním každého objektu na samostatný vyhrazený svazek RAID. Pro všechny datové svazky pro Configuration Manager a jeho databázové soubory použijte k dosažení nejlepšího výkonu RAID 10.

|Využití dat|Minimální místo na disku|25 000 klientů|50 000 klientů|100 000 klientů|150 000 klientů|700 000 klientů (lokalita centrální správy)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Configuration Manager aplikace a soubory protokolu|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|Soubor MDF databáze lokality|75 GB pro každých 25 000 klientů|75 GB|150 GB|300 GB|500 GB|2 TB|  
|Soubor LDF databáze lokality|25 GB pro každých 25 000 klientů|25 GB|50 GB|100 GB|150 GB|100 GB|  
|Dočasné soubory databáze (MDF a LDF)|Podle potřeby|Podle potřeby|Podle potřeby|Podle potřeby|Podle potřeby|Podle potřeby|  

Informace o systémových discích Windows najdete v pokynech k určení velikosti nainstalované verze operačního systému.

V případě obsahu v distribučních bodech závisí na nasazeních. Tyto doprovodné materiály neobsahují místo na disku potřebné pro knihovnu obsahu na serveru lokality nebo v distribučních bodech. Další informace najdete v [knihovně obsahu](../../../core/plan-design/hierarchy/the-content-library.md).

Při plánování požadavků na místo na disku Vezměte v úvahu následující další pokyny:

- Každý klient vyžaduje přibližně 5-10 MB místa v databázi. Toto číslo závisí na typu hierarchie, konfiguraci a počtu klientů. Velikost je pro větší prostředí obecně menší. Menší weby mají větší využití databáze na jednoho klienta.<!-- SCCMDocs#1048 -->

- V případě dočasné databáze primární lokality Naplánujte kombinovanou velikost, která je 25% až 30% souboru MDF databáze lokality. Skutečná velikost může být menší nebo větší. Závisí na výkonu serveru lokality a objemu příchozích dat v průběhu krátkého i dlouhého časového období.

  > [!NOTE]
  > Pokud máte v lokalitě 50 000 nebo více klientů, naplánujte použití čtyř nebo více souborů. mdf databáze Temp.

- Velikost dočasné databáze pro lokalitu centrální správy je obvykle mnohem menší než u primární lokality.

- Použijete-li SQL Server Express pro databázi sekundární lokality, omezí se velikost databáze na 10 GB.

## <a name="clients"></a><a name="bkmk_ScaleClient"></a>Klienti

Tato část poskytuje doporučené hardwarové konfigurace pro počítače, které spravujete pomocí Configuration Manager klientského softwaru.

### <a name="client-for-windows-computers"></a>Klient pro počítače s Windows

Následující minimální požadavky jsou určené pro počítače se systémem Windows, které spravujete pomocí Configuration Manager, včetně vložených edicí:

- **Procesor a paměť:** Přečtěte si požadavky na procesor a paměť RAM pro operační systém.

- **Místo na disku:** 500 MB volného místa na disku, doporučuje se 5 GB pro Configuration Manager mezipaměť klienta. Pokud k instalaci klienta Configuration Manager použijete vlastní nastavení, je vyžadováno méně místa na disku.

  - Použijte vlastnost Client. msi **SMSCACHESIZE** a nastavte velikost mezipaměti menší, než je výchozí hodnota 5120 MB. Minimální velikost je 1 MB. Následující příklad vytvoří mezipaměť o velikosti 2 MB:`CCMSetup.exe SMSCACHESIZE=2`

    Další informace najdete v tématu [o vlastnostech instalace klienta](../../../core/clients/deploy/about-client-installation-properties.md).

    > [!TIP]
    > Instalace klienta tak, aby zabíral co nejméně místa na disku, může být užitečná u zařízení se systémem Windows Embedded, která většinou mívají menší velikost disku než standardní počítače se systémem Windows.

Následující další minimální požadavky na hardware jsou pro volitelné funkce v Configuration Manager:

- **Nasazení operačního systému:** Minimálně 384 MB paměti RAM

- **Centrum softwaru:** Alespoň procesor 500 MHz

- **Vzdálené řízení:** Optimálního prostředí je alespoň 1 GB technologie hyper-threaded s procesorem Pentium 3 GHz (Single core) nebo srovnatelný procesor s PAMĚTí alespoň 1 GB.

### <a name="client-for-linux-and-unix"></a>Klient operačních systémů Linux a UNIX

Následující minimální požadavky jsou pro servery se systémy Linux a UNIX, které spravujete pomocí nástroje Configuration Manager.

|Požadavek|Podrobnosti|  
|-----------------|-------------|  
|Procesor a paměť|Přečtěte si požadavky na procesor a paměť RAM pro operační systém počítače.|  
|Místo na disku|500 MB volného místa na disku, doporučuje se 5 GB pro Configuration Manager mezipaměť klienta.|  
|Připojení k síti|Configuration Manager klientské počítače musí mít připojení k síti, aby bylo možné Configuration Manager systémy lokality, aby bylo možné správu povolit.|  

## <a name="configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a>Konzola Configuration Manager

U každého počítače, na kterém je spuštěna konzola Configuration Manager, platí následující minimální požadavky na hardware:

- Intel i3 nebo srovnatelný procesor  

- 2 GB paměti RAM  

- 2 GB místa na disku  

|Nastavení DPI|Minimální rozlišení|  
|-----------------|------------------------|  
|96 / 100 %|1024 x 768|  
|120 /125 %|1280 x 960|  
|144 / 150 %|1600 x 1200|  
|196 / 200 %|2500 x 1600|  

## <a name="lab-deployments"></a><a name="bkmk_ScaleLab"></a>Nasazení testovacího prostředí

Použijte následující minimální hardwarová doporučení pro testovací prostředí a testovací nasazení Configuration Manager. Tato doporučení se vztahují na všechny typy lokalit až na 100 klientů:  

|Role|PROCESOR (jádra)|Paměť (GB)|Místo na disku (GB)|  
|----------|---------------|-------------------|-----------------------|  
|Server databáze a lokality|2 - 4|8 - 12|100|  
|Server systému lokality|1 - 4|2 - 4|50|  
|Klient|1 - 2|1 - 3|30|  
