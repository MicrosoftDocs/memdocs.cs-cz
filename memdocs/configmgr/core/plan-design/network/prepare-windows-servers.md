---
title: Příprava serverů Windows
titleSuffix: Configuration Manager
description: Ujistěte se, že počítač splňuje předpoklady pro použití jako server lokality nebo server systému lokality pro Configuration Manager.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2aca914f-641e-4bc8-98d4-bbf0a2a5276f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8889c0ee306eaaf682563b2e8e72d5482054d1c7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710787"
---
# <a name="prepare-windows-servers-to-support-configuration-manager"></a>Příprava serverů Windows na podporu nástroje Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Než budete moct použít počítač s Windows jako server systému lokality pro Configuration Manager, musí počítač splňovat požadavky pro zamýšlené použití jako server lokality nebo server systému lokality.  

- Tyto požadavky často zahrnují jednu nebo více funkcí nebo rolí Windows, které jsou povolené pomocí Správce serveru počítače.  

- Vzhledem k tomu, že metoda povolení funkcí a rolí systému Windows se liší v různých verzích operačního systému, přečtěte si dokumentaci k verzi operačního systému, kde najdete podrobné informace o nastavení operačního systému, který používáte.  

Informace v tomto článku obsahují přehled typů konfigurací systému Windows, které jsou požadovány pro podporu Configuration Manager systémů lokality. Podrobnosti o konfiguraci konkrétních rolí systému lokality najdete v tématu [požadavky na lokalitu a systém lokality](../configs/site-and-site-system-prerequisites.md).

##  <a name="windows-features-and-roles"></a><a name="BKMK_WinFeatures"></a>Funkce a role Windows  
Když nastavíte funkce a role Windows v počítači, může být nutné restartovat počítač, aby se tato konfigurace dokončila. Proto je vhodné identifikovat počítače, které budou hostovat konkrétní role systému lokality, než nainstalujete lokalitu Configuration Manager nebo server systému lokality.

### <a name="features"></a>Funkce  
Na určitých serverech systému lokality se vyžadují následující funkce Windows a měli byste je nastavit předtím, než na tento počítač nainstalujete roli systému lokality.  

- **.NET Framework:** Včetně  

    - ASP.NET  
    - Aktivace protokolem HTTP  
    - Aktivace jiným protokolem než HTTP  
    - Služby Windows Communication Foundation (WCF)  

    Různé role systému lokality vyžadují různé verze .NET Framework.  

    Vzhledem k tomu, že .NET Framework 4,0 a novější nejsou zpětně kompatibilní, aby nahradily 3,5 a starší verze, pokud jsou různé verze uvedeny podle potřeby, naplánujte povolení jednotlivých verzí na jednom počítači.  

- **Služba inteligentního přenosu na pozadí (BITS)**: body správy vyžadují, aby služba BITS (a automaticky vybrané možnosti) podporovala komunikaci se spravovanými zařízeními.  

- **BranchCache**: distribuční body lze nastavit pomocí služby BranchCache, aby podporovaly klienty, kteří používají službu BranchCache.  

- **Odstranění duplicitních dat**: distribuční body lze nastavit pomocí funkce odstranění duplicitních dat a využívat je.  

- **Remote Differential Compression (RDC)**: každý počítač, který je hostitelem serveru lokality nebo distribučního bodu, vyžaduje funkci RDC. Funkce RDC se používá pro generování podpisů balíčků a porovnávání balíčků.  

### <a name="roles"></a>Role  
Následující role systému Windows jsou vyžadovány pro podporu konkrétních funkcí, jako jsou aktualizace softwaru a nasazení operačního systému, zatímco služba IIS je požadována nejběžnějšími rolemi systému lokality.  

- **Služba zápisu síťových zařízení** (v rámci služby Active Directory Certificate Services): Tato role Windows je předpokladem pro použití profilů certifikátů v Configuration Manager.  

- **Webový server (IIS)**: zahrnuje:  
    - Společné funkce protokolu HTTP  
          - Přesměrování protokolu HTTP  
    - Vývoj aplikací  
          - Rozšiřitelnost rozhraní .NET  
          - ASP.NET  
          - Rozšíření ISAPI  
          - Filtry ISAPI  
    - Nástroje pro správu  
          - Kompatibilita správy služby IIS 6  
          - Kompatibilita metabáze služby IIS 6  
          - Kompatibilita služby IIS 6 rozhraní WMI (Windows Management Instrumentation) (WMI)  
    - Zabezpečení  
          - Filtrování požadavků  
          - Ověřování systému Windows  

  Následující role systému lokality používají jednu nebo více uvedených konfigurací služby IIS:  
  - Bod služeb webu Katalog aplikací  
  - Bod webu Katalog aplikací  
  - Distribuční bod  
  - Bod registrace  
  - Zprostředkující bod registrace  
  - Bod záložního stavu  
  - Bod správy  
  - Bod aktualizace softwaru  
  - Bod migrace stavu     

  Minimální požadovaná verze služby IIS je verze dodaná s operačním systémem serveru lokality.  

  Kromě těchto konfigurací služby IIS možná budete muset nastavit [filtrování požadavků služby IIS pro distribuční body](#BKMK_IISFiltering).  

- **Služba pro nasazení systému Windows**: Tato role se používá při nasazení operačního systému.  

- **Windows Server Update Services**: Tato role je vyžadována pro aktualizace softwaru.  


##  <a name="iis-request-filtering-for-distribution-points"></a><a name="BKMK_IISFiltering"></a>Filtrování požadavků služby IIS pro distribuční body  
Služba IIS ve výchozím nastavení používá filtrování žádostí, čímž blokuje přístup protokolu HTTP nebo HTTPS k některým příponám názvu souborů a umístěním složek. V distribučním bodě zabráníte klientům stahovat balíčky, které mají blokované přípony nebo umístění složek.  

Pokud mají zdrojové soubory balíčku rozšíření, která jsou ve službě IIS blokována vaší konfigurací filtrování požadavků, je nutné nastavit filtrování požadavků tak, aby je povolilo. To se provádí [úpravou funkce filtrování žádostí](https://technet.microsoft.com/library/hh831621.aspx) ve Správci služby IIS na počítačích distribučních bodů.  

Configuration Manager pro balíčky a aplikace se navíc používají následující přípony názvů souborů. Ujistěte se, že vaše konfigurace filtrování požadavků neblokují tyto přípony souborů:  

- .PCK  
- .PKG  
- .STA  
- .TAR  

Například zdrojové soubory pro nasazení softwaru mohou zahrnovat složku pojmenovanou **bin** nebo mají soubor s příponou názvu souboru **. mdb** .  

- Ve výchozím nastavení filtrování žádostí služby IIS blokuje přístup k těmto prvkům (**bin** je blokována jako skrytý segment a přípona **. mdb** je jako přípona názvu souboru zablokovaná).  

- Použijete-li v distribučním bodě výchozí konfiguraci služby IIS, klientům používajícím služby BITS se nepodařilo stáhnout toto nasazení softwaru z distribučního bodu a označit, že čekají na obsah.  

- Aby klienti mohli stáhnout tento obsah, v každém příslušném distribučním bodě upravte **filtrování žádostí** ve Správci služby IIS tak, aby umožňovalo přístup k příponám souborů a složkám, které jsou v balíčcích a aplikacích, které nasazujete.  

> [!IMPORTANT]  
> Úpravy filtru požadavků mohou zvýšit plochu pro útok na počítač.  
> 
> - Úpravy, které provedete na úrovni serveru, platí pro všechny weby na serveru.   
>     - Úpravy provedené u jednotlivých webů platí pouze pro tento web.  
> 
> Osvědčeným postupem zabezpečení je spuštění Configuration Manager na vyhrazeném webovém serveru. Pokud na webovém serveru musíte spustit další aplikace, použijte pro Configuration Manager vlastní web. Informace najdete v tématu [weby pro servery systému lokality](websites-for-site-system-servers.md).  

## <a name="http-verbs"></a>Příkazy HTTP
**Body správy:** Aby bylo zajištěno, že klienti mohou úspěšně komunikovat s bodem správy, v serveru bodu správy zkontrolujte, zda jsou povoleny následující příkazy protokolu HTTP:  
- GET
- POST
- CCM_POST
- HEAD
- PROPFIND

**Distribuční body:** Distribuční body vyžadují, aby následující příkazy HTTP byly povolené:
- GET
- HEAD
- PROPFIND

Další informace najdete v tématu [Konfigurace filtrování požadavků ve službě IIS](https://technet.microsoft.com/library/hh831621.aspx#Verbs). 
