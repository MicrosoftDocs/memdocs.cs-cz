---
title: Doporučený hardware
titleSuffix: Configuration Manager
description: Získejte Hardwarová doporučení, která vám pomůžou škálovat Configuration Manager prostředí nad rámec základního nasazení.
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d741e34325da859d4fe1f0af554544ce146a42f9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719159"
---
# <a name="recommended-hardware-for-configuration-manager"></a>Doporučený hardware pro nástroj Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Následující doporučení jsou pokyny, které vám pomohou škálovat Configuration Manager prostředí, aby podporovaly více než velmi základní nasazení lokalit, systémů lokalit a klientů. Nepokrývají všechny možné konfigurace lokalit a hierarchie.  

Informace v následujících částech vám pomohou při plánování hardwaru, který může splňovat požadavky na zpracování pro klienty a lokality, které používají dostupné funkce Configuration Manager s výchozími konfiguracemi.  



##  <a name="site-systems"></a><a name="bkmk_ScaleSieSystems"></a>Systémy lokality  
V této části najdete doporučené hardwarové konfigurace pro Configuration Manager systémy lokalit pro nasazení, která podporují maximální počet klientů a využívají většinu nebo všechny Configuration Manager funkce. Nasazení, která podporují méně než maximální počet klientů a nepoužívají všechny dostupné funkce, mohou vyžadovat méně prostředků počítače. Celkový výkon systému obecně ovlivňují následující hlavní parametry (v uvedeném pořadí):  

1.  Výkon diskových operací  

2.  Dostupná paměť  

3.  Procesor  

Nejlepšího výkonu dosáhnete, když použijete konfiguraci RAID 10 pro všechny datové jednotky a síť Ethernet s rychlostí 1 GB/s.  

###  <a name="site-servers"></a><a name="bkmk_ScaleSiteServer"></a>Servery lokality  

|Konfigurace lokality|PROCESOR (jádra)|Paměť (GB)|Přidělení paměti pro SQL Server (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Samostatný server primární lokality s rolí databázového serveru na stejném serveru<sup>1</sup>|16|96|80|  
|Server samostatné primární lokality se vzdálenou databází lokality|8|16|-|  
|Vzdálený databázový server pro samostatnou primární lokalitu|16|72|90|  
|Webový server Centrální správy s rolí databázového serveru na stejném serveru<sup>1</sup>|20|128|80|  
|Server lokality centrální správy se vzdálenou databází lokality|8|16|-|  
|Vzdálená databázový server pro lokalitu centrální správy|16|96|90|  
|Podřízená primární lokalita s rolí databázového serveru na stejném serveru|16|96|80|  
|Server podřízené primární lokality se vzdálenou databází lokality|8|16|-|  
|Vzdálený databázový server pro podřízenou primární lokalitu|16|72|90|  
|Server sekundární lokality|8|16|-|  

<sup>1</sup> Pokud je server lokality a SQL Server nainstalovaný na stejném počítači, nasazení podporuje maximální [hodnoty velikosti a škálování](size-and-scale-numbers.md) pro lokality a klienty. Tato konfigurace ale může omezit [Možnosti vysoké dostupnosti pro Configuration Manager](../../servers/deploy/configure/high-availability-options.md), jako je například použití clusteru SQL Server. Z důvodu vyššího počtu vstupně-výstupních požadavků, které jsou potřeba k podpoře SQL Server i serveru lokality Configuration Manager, když pracujete na stejném počítači, je vhodné zvážit použití konfigurace se vzdáleným SQL Server počítačem, pokud máte větší nasazení.  

###  <a name="remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a>Vzdálené servery systému lokality  
Následující pokyny jsou pro počítače, které obsahují jednu roli systému lokality. Pokud instalujete víc rolí systému lokality na stejném počítači, počítejte s úpravami.  

|Role systému lokality|PROCESOR (jádra)|Paměť (GB)|Místo na disku (GB)|  
|----------------------|---------------|---------------|--------------------|  
|Bod správy|4|8|50|  
|Distribuční bod|2|8|Podle požadavků operačního systému a ukládání obsahu, který nasazujete|  
|Bod aktualizace softwaru<sup>1</sup>|8|16|Podle požadavků operačního systému a ukládání aktualizací, které nasadíte|  
|Všechny ostatní role systémů lokalit|4|8|50|  

<sup>1</sup> počítač, který je hostitelem bodu aktualizace softwaru, vyžaduje následující konfigurace pro fondy aplikací IIS:  

- Zvyšte **délku fronty nastavení WsusPool** na **2000**.  

- Zvyšte **limit soukromé paměti nastavení WsusPool** o čtyřikrát nebo ji nastavte na **0** (neomezeno).  

###  <a name="disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a>Místo na disku pro systémy lokality  
Přidělení disku a jeho konfigurace přispívá k výkonu Configuration Manager. Vzhledem k tomu, že se každé Configuration Manager prostředí liší, hodnoty, které implementujete, se můžou lišit od následujících pokynů.  

Nejlepšího výkonu dosáhnete umístěním každého objektu na samostatný vyhrazený svazek RAID. Pro všechny datové svazky (Configuration Manager a jeho databázové soubory) použijte k dosažení nejlepšího výkonu RAID 10.  

|Využití dat|Minimální místo na disku|25 000 klientů|50 000 klientů|100 000 klientů|150 000 klientů|700 000 klientů (lokalita centrální správy)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Operační systém|Viz příručka pro operační systém.|Viz příručka pro operační systém.|Viz příručka pro operační systém.|Viz příručka pro operační systém.|Viz příručka pro operační systém.|Viz příručka pro operační systém.|  
|Configuration Manager aplikace a soubory protokolu|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|Soubor MDF databáze lokality|75 GB pro každých 25 000 klientů|75 GB|150 GB|300 GB|500 GB|2 TB|  
|Soubor LDF databáze lokality|25 GB pro každých 25 000 klientů|25 GB|50 GB|100 GB|150 GB|100 GB|  
|Dočasné soubory databáze (MDF a LDF)|Podle potřeby|Podle potřeby|Podle potřeby|Podle potřeby|Podle potřeby|Podle potřeby|  
|Obsah (sdílené složky distribučních bodů)|Podle potřeby<sup>1</sup>|Podle potřeby<sup>1</sup>|Podle potřeby<sup>1</sup>|Podle potřeby<sup>1</sup>|Podle potřeby<sup>1</sup>|Podle potřeby<sup>1</sup>|  

<sup>1</sup> Doporučené místo na disku nezahrnuje prostor potřebný pro obsah umístěný v knihovně obsahu na serveru lokality nebo v distribučních bodech. Informace o plánování knihovny obsahu najdete v tématu [Knihovna obsahu](../../../core/plan-design/hierarchy/the-content-library.md).  

Kromě předchozích doporučení zvažte při plánování místa na disku následující pokyny:  

- Každý klient potřebuje přibližně 5 MB místa.  

- Při plánování velikosti dočasné databáze primární lokality Naplánujte kombinovanou velikost, která je 25% až 30% souboru MDF databáze lokality. Skutečná velikost může být výrazně menší nebo větší – závisí na výkonu serveru lokality a objemu příchozích dat v průběhu krátkého i dlouhého časového období.  

  > [!NOTE]  
  >  Pokud máte v lokalitě 50 000 nebo více klientů, naplánujte použití čtyř nebo více souborů. mdf databáze Temp.  

- Velikost dočasné databáze pro lokalitu centrální správy je obvykle mnohem menší než u primární lokality.  

- Databáze sekundární lokality má následující omezení velikosti:  

  - SQL Server 2012 Express: 10 GB  

  - SQL Server 2014 Express: 10 GB  

##  <a name="clients"></a><a name="bkmk_ScaleClient"></a>Klienti  
Tato část poskytuje doporučené hardwarové konfigurace pro počítače, které spravujete pomocí Configuration Manager klientského softwaru.  

### <a name="client-for-windows-computers"></a>Klient pro počítače s Windows  
Níže jsou uvedené minimální požadavky na počítače se systémem Windows, které spravujete pomocí Configuration Manager, včetně integrovaných operačních systémů:  

- **Procesor a paměť:** Přečtěte si požadavky na procesor a paměť RAM pro operační systém počítače.  

- **Místo na disku:** 500 MB volného místa na disku, doporučuje se 5 GB pro Configuration Manager mezipaměť klienta. Pokud k instalaci Configuration Manager klienta použijete vlastní nastavení, je potřeba méně místa na disku:  

    - Pokud chcete nastavit soubor mezipaměti s menší než výchozí velikostí (5120 MB), použijte vlastnost souboru Client.msi SMSCACHESIZE. Minimální velikost je 1 MB. Například `CCMSetup.exe SMSCachesize=2` vytvoří mezipaměť o velikosti 2 MB.  

    Další informace o těchto nastaveních instalace klienta najdete v tématu [informace o vlastnostech instalace klienta](../../../core/clients/deploy/about-client-installation-properties.md).  

    > [!TIP]  
    > Instalace klienta tak, aby zabíral co nejméně místa na disku, může být užitečná u zařízení se systémem Windows Embedded, která většinou mívají menší velikost disku než standardní počítače se systémem Windows.  

Níže najdete další minimální požadavky na hardware pro volitelné funkce v Configuration Manager.  

- **Nasazení operačního systému:** 384 MB paměti RAM  

- **Centrum softwaru:** procesor 500 MHz  

- **Vzdálené řízení:** Procesor Pentium 4 hyper-threaded 3 GHz (Single core) nebo srovnatelný procesor s pamětí alespoň 1 GB RAM pro optimální prostředí  

### <a name="client-for-linux-and-unix"></a>Klient operačních systémů Linux a UNIX  
Níže jsou uvedené minimální požadavky na servery se systémy Linux a UNIX, které spravujete pomocí nástroje Configuration Manager.  

|Požadavek|Podrobnosti|  
|-----------------|-------------|  
|Procesor a paměť|Přečtěte si požadavky na procesor a paměť RAM pro operační systém počítače.|  
|Místo na disku|500 MB volného místa na disku, doporučuje se 5 GB pro Configuration Manager mezipaměť klienta.|  
|Připojení k síti|Configuration Manager klientské počítače musí mít připojení k síti, aby bylo možné Configuration Manager systémy lokality, aby bylo možné správu povolit.|  

##  <a name="configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a>Konzola Configuration Manager  
Požadavky v následující tabulce platí pro každý počítač, který spouští konzolu Configuration Manager.  

**Minimální konfigurace hardwaru:**  

- Intel i3 nebo srovnatelný procesor  

- 2 GB paměti RAM  

- 2 GB místa na disku  

|Nastavení DPI|Minimální rozlišení|  
|-----------------|------------------------|  
|96 / 100 %|1024 x 768|  
|120 /125 %|1280 x 960|  
|144 / 150 %|1600 x 1200|  
|196 / 200 %|2500 x 1600|  

**Podpora pro PowerShell:**  

Když instalujete podporu PowerShellu na počítači, na kterém běží Konzola Configuration Manager, můžete na tomto počítači spustit rutiny prostředí PowerShell pro správu Configuration Manager.

- PowerShell 3,0 nebo novější je podporovaný.

Kromě PowerShellu se podporuje rozhraní Windows Management Framework (WMF) verze 3,0 nebo novější.   


##  <a name="lab-deployments"></a><a name="bkmk_ScaleLab"></a>Nasazení testovacího prostředí  
Použijte následující minimální hardwarová doporučení pro testovací prostředí a testovací nasazení Configuration Manager. Tato doporučení se vztahují na všechny typy lokalit až na 100 klientů:  

|Role|PROCESOR (jádra)|Paměť (GB)|Místo na disku (GB)|  
|----------|---------------|-------------------|-----------------------|  
|Server databáze a lokality|2 - 4|8 - 12|100|  
|Server systému lokality|1 - 4|2 - 4|50|  
|Klient|1 - 2|1 - 3|30|  
