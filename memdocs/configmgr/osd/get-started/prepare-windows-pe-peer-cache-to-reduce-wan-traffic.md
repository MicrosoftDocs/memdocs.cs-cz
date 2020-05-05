---
title: Příprava sdílené mezipaměti prostředí Windows PE pro omezení provozu v síti WAN
titleSuffix: Configuration Manager
description: Sdílená mezipaměť prostředí Windows PE funguje v prostředí Windows PE, aby získala obsah od místního partnera a minimalizovala provoz v síti WAN, pokud není k dispozici žádný místní distribuční bod.
ms.date: 06/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 6c64f276-b88c-4b1e-8073-331876a03038
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fd622c1a54c1dd3cd3b5071cc62d1b6860a118e3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724038"
---
# <a name="prepare-windows-pe-peer-cache-to-reduce-wan-traffic-in-configuration-manager"></a>Příprava sdílené mezipaměti prostředí Windows PE pro omezení provozu v síti WAN v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Když v Configuration Manager nasadíte nový operační systém, počítače spouštějící pořadí úkolů můžou pomocí sdílené mezipaměti prostředí Windows PE získat obsah od místního partnera (zdroje sdílené mezipaměti) a nemusí stahovat obsah z distribučního bodu. Tím se může minimalizovat provoz v sítích WAN (Wide Area Network) v případě firemních poboček bez místních distribučních bodů.  

 Sdílená mezipaměť prostředí Windows PE je podobná službě [Windows BranchCache](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache), ale funguje v Windows Preinstallation Environment (Windows PE). K popisu klientů, kteří používají sdílenou mezipaměť prostředí Windows PE, se používají následující termíny:  

-   **Klient sdílené mezipaměti** je počítač, ve kterém se nakonfigurovalo použití sdílené mezipaměti systému Windows PE.  

-   **Zdroj sdílené mezipaměti** je klient, který je nakonfigurovaný pro sdílenou mezipaměť a který zpřístupňuje požadovaný obsah ostatním klientům sdílené mezipaměti.  

Pro správu sdílené mezipaměti použijte následující části.

##  <a name="objects-stored-on-a-peer-cache-source"></a><a name="BKMK_PeerCacheObjects"></a>Objekty uložené ve zdroji sdílené mezipaměti  
 Pořadí úkolů, pro které je nakonfigurované použití sdílené mezipaměti prostředí Windows PE, může při spuštění Windows PE získat tyto objekty obsahu:  

- Bitová kopie operačního systému  

- Balíček ovladačů  

- Balíčky a programy (když klient dál spouští pořadí úkolů v plném operačním systému, klient získá tento obsah ze zdroje sdílené mezipaměti, pokud je pořadí úkolů původně nakonfigurované pro sdílenou mezipaměť při spuštění v systému Windows PE.)  

- Další spouštěcí image  

  Následující objekty obsahu se nikdy nepřenášejí pomocí sdílené mezipaměti. Přenášejí se z distribučního bodu nebo pomocí služby Windows BranchCache, pokud jste ji ve svém prostředí nakonfigurovali:  

- Aplikace  

- Aktualizace softwaru  

##  <a name="how-does--windows-pe-peer-cache-work"></a><a name="BKMK_PeerCacheWork"></a>Jak sdílená mezipaměť prostředí Windows PE funguje?  
 Představte si třeba situaci, že firemní pobočka nemá distribuční bod, ale má několik klientů s povoleným použitím sdílené mezipaměti prostředí Windows PE. V několika klientech, které jsou nakonfigurované jako součást zdroje sdílené mezipaměti, nasadíte pořadí úkolů s nakonfigurovaným použitím sdílené mezipaměti. První klient, který spustí toto pořadí úkolů, všesměrově vyšle požadavek na partnera s obsahem. Když žádného nenajde, získá obsah z distribučního bodu pomocí sítě WAN. Klient nainstaluje novou image a pak uloží obsah ve své Configuration Manager klientské mezipaměti, aby mohl fungovat jako zdroj sdílené mezipaměti pro ostatní klienty. Když toto pořadí úkolů spustí další klient, všesměrově vyšle požadavek na zdroj sdílené mezipaměti v podsíti. První klient odpoví a zpřístupní obsah uložený v mezipaměti.  

##  <a name="determine-what--clients-will-be-part-of-the-windows-pe-peer-cache-source"></a><a name="BKMK_PeerCacheDetermine"></a>Určení klientů, kteří budou součástí zdroje sdílené mezipaměti prostředí Windows PE  
 Při určování, které počítače vybrat jako zdroj sdílené mezipaměti prostředí Windows PE, byste měli zvážit několik bodů:  

-   Zdrojem sdílené mezipaměti prostředí Windows PE by měl být stolní počítač, který je vždycky zapnutý a dostupný pro klienty sdílené mezipaměti.  

-   Velikost klientské mezipaměti ve sdílené mezipaměti prostředí Windows PE postačuje pro ukládání bitových kopií.  

##  <a name="requirements-for-a-client-to-use-a--windows-pe-peer-cache-source"></a><a name="BKMK_PeerCacheRequirements"></a>Požadavky na klienty, kteří budou používat zdroj sdílené mezipaměti prostředí Windows PE  
 Aby klienti mohli využívat zdroj sdílené mezipaměti prostředí Windows PE, musí splňovat následující podmínky:  

-   Klient Configuration Manager musí být schopný komunikovat mezi následujícími porty ve vaší síti:  

    -   Port pro počáteční síťové všesměrové vysílání pro vyhledání zdroje sdílené mezipaměti. Ve výchozím nastavení se jedná o port UDP 8004.  

    -   Port pro stahování obsahu ze zdroje sdílené mezipaměti (HTTP a HTTPS). Ve výchozím nastavení se jedná o port TCP 8003.  
    
        Další informace najdete v tématu [porty používané pro připojení](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-ClientWakeUp).  

        > [!TIP]  
        >  Klienti budou ke stahování obsahu využívat protokol HTTPS, pokud je dostupný. Pro HTTP i HTTPS se ale používá stejné číslo portu.  

-   [Konfigurace mezipaměti klienta pro klienty nástroje Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_ClientCache) na klientech zajistí, aby měly dost místa pro uložení nasazovaných imagí. Sdílená mezipaměť prostředí Windows PE neovlivňuje konfiguraci ani chování mezipaměti klienta.  

-   V možnostech pro nasazení pořadí úkolů musí být nakonfigurované nastavení Pokud to vyžaduje spuštění pořadí úloh, stáhnout veškerý obsah místně.  

##  <a name="configure-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheConfigure"></a>Konfigurace sdílené mezipaměti prostředí Windows PE  
 Dál jsou uvedené metody, pomocí kterých klientovi zajistit obsah sdílené mezipaměti, aby mohl sloužit jako zdroj sdílené mezipaměti:  

- Klient sdílené mezipaměti, který nemůže najít zdroj sdílené mezipaměti s obsahem, si příslušný obsah stáhne z distribučního bodu.  Když klient má nastavení klienta, které povoluje využití sdílené mezipaměti, a pro pořadí úkolů je nakonfigurované zachování obsahu v mezipaměti, stane se klient zdrojem sdílené mezipaměti.  

- Klient sdílené mezipaměti může získat obsah od jiného klienta sdílené mezipaměti (zdroj sdílené mezipaměti).  Protože klient má nakonfigurované použití sdílené mezipaměti, při spuštění pořadí úkolů s nakonfigurovaným zachováním obsahu v mezipaměti se stane zdrojem sdílené mezipaměti.  

- Klient spustí pořadí úkolů obsahující volitelný krok [Stáhnout obsah balíčku](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent), který se používá k přípravě souvisejícího obsahu zahrnutého v pořadí úkolů sdílené mezipaměti systému Windows PE. Při použití této metody:  

  -   Klient nemusí instalovat image, která se nasazuje.  

  -   Kromě možnosti **Stáhnout balíček obsahu** musí pořadí úkolů taky využívat možnost **Mezipaměť klienta Správce konfigurace** . Tuto možnost použijete k uložení obsahu v mezipaměti klienta, takže klient může pro ostatní klienty sdílené mezipaměti fungovat jako zdroj sdílené mezipaměti.  

  Následující postupy vám pomůžou nakonfigurovat sdílenou mezipaměť systému Windows PE v klientských počítačích a nakonfigurovat pořadí úkolů podporující sdílenou mezipaměť.  

### <a name="to-configure-the-windows-pe-peer-cache-source-computers"></a>Konfigurace zdrojových počítačů sdílené mezipaměti prostředí Windows PE  

1. V konzole Configuration Manager přejděte na **Správa** > **nastavení klienta**a pak vytvořte nové **vlastní nastavení klientského zařízení** nebo upravte stávající objekt nastavení. Můžete to taky nakonfigurovat pro objekt **Výchozí nastavení klienta** .  

   > [!TIP]  
   >  Pomocí objektu vlastního nastavení upravte, kteří klienti dostanou tuto konfiguraci. Můžete se třeba chtít vyhnout konfiguraci u přenosných počítačů, jejichž uživatelé jsou často na cestách. Vysoce mobilní systém může být slabým zdrojem pro poskytování obsahu dalším klientům sdílené mezipaměti.  
   >   
   >  Nezapomeňte taky, že když konfigurujete toto nastavení jako součást **Výchozího nastavení klienta**, bude se konfigurace vztahovat na všechny klienty ve vašem prostředí.  

2. V části **nastavení mezipaměti klienta**nastavte **Povolit Configuration Manager klienta v úplném operačním systému pro sdílení obsahu** s **hodnotou Ano**.  

   -   Ve výchozím nastavení je povolený jen protokol HTTP. Pokud chcete klientům povolit stahování obsahu přes HTTPS, nastavte **Povolit HTTPS pro komunikaci mezi klienty** na **Ano**.  

   -   Ve výchozím nastavení je port pro všesměrové vysílání nastavený na 8004 a port pro stahování obsahu na 8003. Obě nastavení můžete změnit.  

3. Nastavení klienta uložte a nasaďte do klientů, které jste vybrali jako zdroje sdílené mezipaměti.  

   Po dokončení konfigurace s tímto objektem nastavení je zařízení nakonfigurované tak, že slouží jako zdroj sdílené mezipaměti. Toto nastavení byste měli nasadit do potenciálních klientů sdílené mezipaměti a nakonfigurovat tak potřebné porty a protokoly.  

###  <a name="configure-a-task-sequence-for-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheConfigureTS"></a> Konfigurace pořadí úkolů pro sdílenou mezipaměť prostředí Windows PE  
 Při konfiguraci pořadí úkolů použijte následující proměnné pořadí úkolů jako proměnné kolekce, ve které je pořadí úkolů nasazené:  

- **SMSTSPeerDownload**  

   Hodnota:  TRUE  

   Umožňuje klientovi použít sdílenou mezipaměť systému Windows PE.  

- **SMSTSPeerRequestPort**  

   Hodnota: <číslo portu\>  

   Pokud nepoužijete výchozí port konfigurovaný v nastavení klienta (8004), musíte tuto proměnnou nakonfigurovat s vlastní hodnotou síťového portu, která se má použít pro počáteční všesměrové vysílání.  

- **SMSTSPreserveContent**  

   Hodnota: TRUE  

   Tím se označí obsah v pořadí úkolů, který se zachová v mezipaměti klienta Configuration Manager po nasazení. To se liší od použití proměnné SMSTSPersisContent, který zachovává obsah pouze po dobu trvání pořadí úkolů a používá mezipaměť pořadí úkolů, nikoli mezipaměť klienta Configuration Manager.  

  Další informace najdete v tématu [proměnné pořadí úkolů](../understand/task-sequence-variables.md).  

###  <a name="validate-the-success-of-using-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheValidate"></a>Ověření úspěchu při použití sdílené mezipaměti prostředí Windows PE  
 Když sdílenou mezipaměť prostředí Windows PE použijete k nasazení a instalaci pořadí úkolů a chcete potvrdit, že se sdílená mezipaměť úspěšně použila, zobrazte soubor **smsts.log** v klientovi, který toto pořadí úkolů spustil.  

 V protokolu vyhledejte položku podobnou následující, kde <*SourceServerName*> identifikuje počítač, ze kterého klient získal obsah. Tento počítač by měl být zdroj sdílené mezipaměti, a ne server distribučního bodu. Další podrobnosti se budou lišit v závislosti na místním prostředí a konfiguraci.  

-   *<! [LOG [stažený soubor z http://<SourceServerName\>: 8003/SCCM_BranchCache $/SS10000C/SCCM?/Install.wim to C:\\_SMSTaskSequence \packages\ss10000c\install.wim] log]! ><Time = "14:24:33.329 + 420" date = "06-26-2015" Component = "ApplyOperatingSystem" Context = "" Type = "1" Thread = "1256" File = "Downloadcontent. cpp: 1626" >*  
