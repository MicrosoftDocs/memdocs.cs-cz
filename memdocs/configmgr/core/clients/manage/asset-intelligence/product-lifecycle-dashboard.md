---
title: Řídicí panel životního cyklu produktu
titleSuffix: Configuration Manager
description: Prohlédněte si zásady životního cyklu Microsoftu pomocí řídicího panelu životní cyklus produktu v Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 178331865c8f3efd660e4a0037674eed3621fe6b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714238"
---
# <a name="manage-microsoft-lifecycle-policy-with-configuration-manager"></a>Správa zásad životního cyklu Microsoftu pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Počínaje verzí 1806 můžete zobrazit zásady životního cyklu Microsoftu pomocí řídicího panelu životního cyklu Configuration Managerho produktu. Řídicí panel zobrazuje stav zásad životního cyklu Microsoftu pro produkty Microsoftu nainstalované na zařízeních spravovaných pomocí Configuration Manager. Poskytuje vám taky informace o produktech Microsoftu ve vašem prostředí, stavu podpory a koncových datech podpory. Pomocí řídicího panelu můžete pochopit dostupnost podpory jednotlivých produktů. Tyto informace vám pomohou při plánování, kdy aktualizovat produkty od společnosti Microsoft, které používáte, před dosažením jejich aktuálního konce podpory.  

Další informace najdete v tématu [Zásady životního cyklu Microsoftu](https://support.microsoft.com/lifecycle).

Počínaje verzí 1810 řídicí panel obsahuje informace pro System Center 2012 Configuration Manager a novější.<!--1358702-->  



## <a name="prerequisites"></a>Požadavky 

 Chcete-li zobrazit data na řídicím panelu životní cyklus produktu, jsou vyžadovány následující komponenty:  

- Na počítači, na kterém je spuštěná konzola Configuration Manager, musí být nainstalovaný Internet Explorer 9 nebo novější.  

- Musí být nainstalovaná a nakonfigurovaná role spojovacího bodu služby. Chcete-li získat aktualizace dat na tomto řídicím panelu, spojovací bod služby musí být online nebo synchronizován pravidelně, pokud je offline. Další informace najdete v tématu [o spojovacím bodu služby](../../../servers/deploy/configure/about-the-service-connection-point.md).

- Pro funkce hypertextového odkazu na řídicím panelu je vyžadován bod služeb generování sestav. Řídicí panel odkazuje na sestavy SQL Server Reporting Services (SSRS). Další informace najdete v tématu [Úvod do vytváření sestav](../../../servers/manage/introduction-to-reporting.md).  

- Synchronizační bod katalogu Asset Intelligence musí být nakonfigurovaný a synchronizovaný. Řídicí panel používá katalog Asset Intelligence jako metadata pro názvy produktů. Metadata se porovnávají s daty inventáře ve vaší hierarchii. Další informace najdete v tématu [Konfigurace funkce Asset Intelligence v Configuration Manager](configuring-asset-intelligence.md).  
  - Pokud službu Asset Intelligence konfigurujete poprvé, ujistěte se, že jste [povolili třídy inventáře hardwaru funkce Asset Intelligence](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence). Řídicí panel životní cyklus závisí na těchto třídách inventáře hardwaru funkce Asset Intelligence. Řídicí panel nebude zobrazovat data, dokud klienti nehledají a vrátí inventář hardwaru.  
  - Chcete-li zobrazit informace o rozšířených aktualizacích zabezpečení (EVJ) v tomto řídicím panelu, povolte třídu inventáře hardwaru **produkt – funkce Asset Intelligence (SoftwareLicensingProduct)**. Další informace najdete v tématu [Povolení tříd inventáře hardwaru funkce Asset Intelligence](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence). <!--4962901-->



## <a name="use-the-product-lifecycle-dashboard"></a>Použití řídicího panelu životní cyklus produktu

Na základě dat inventáře, která lokalita shromažďuje ze spravovaných zařízení, zobrazuje řídicí panel informace o všech aktuálních produktech. Informace zobrazované pro operační systémy a SQL Server jsou ale omezené na tyto verze:

- Windows Server 2008 a novější
- Windows XP a novější
- SQL Server 2008 a novější

Přístup k řídicímu panelu životní cyklus v konzole Configuration Manager získáte tak, že přejdete do pracovního prostoru **prostředky a kompatibilita** , rozbalíte **funkce Asset Intelligence**a vyberete uzel **životní cyklus produktu** .

> [!NOTE]  
> Data na řídicím panelu jsou založená na lokalitě, ke které se konzola Configuration Manager připojuje. Pokud se konzola nástroje připojuje k vaší lokalitě nejvyšší úrovně, zobrazí se data pro celou hierarchii. Při připojení k podřízené primární lokalitě se zobrazí pouze data z této lokality.

### <a name="product-lifecycle-dashboard"></a>Řídicí panel životního cyklu produktu

![Snímek obrazovky s řídicím panelem životní cyklus produktu v konzole nástroje](media/product-lifecycle-dashboard.png)

Změňte zobrazení tak, že v seznamu **Kategorie produktů** vyberete jednu z následujících možností:  
- **Vše**: Zobrazit všechny produkty dohromady  
- **Klient Windows**: zobrazení verzí klientských operačních systémů Windows  
- **Windows Server**: zobrazení verzí operačního systému Windows Server  
- **Databáze**: zobrazení verzí SQL Server  
- **Configuration Manager**: počínaje verzí 1810 se zobrazí Configuration Manager verze 
- **Systém Microsoft Office**: počínaje verzí 1902 se zobrazují informace o nainstalovaných verzích Office 2003 až Office 2016. <!--3556026-->

Řídicí panel obsahuje tyto dlaždice:  

- **Nejoblíbenějších pět produktů po skončení životnosti**: Tato dlaždice je konsolidovaná zobrazení dat produktů nalezených ve vašem prostředí po jejich ukončení životního cyklu. V grafu se zobrazuje nainstalovaný software, jehož platnost vypršela v porovnání s životním cyklem podpory pro operační systémy a produkty SQL serveru.  

- **Pět nejoblíbenějších produktů**, jejichž životnost: Tato dlaždice je konsolidovaná data o produktech nalezených ve vašem prostředí, která se blíží době životnosti v příštích 18 měsících. V grafu se zobrazuje nainstalovaný software, který je v porovnání s životním cyklem podpory pro operační systémy a produkty SQL serveru v průběhu 18 měsíců od konce životnosti.  

- **Data životního cyklu pro nainstalované produkty**: Tato dlaždice poskytuje obecnou představu o tom, kdy produkt přejde do stavu s vypršenou platností. Graf poskytuje rozpis počtu klientů, ve kterých je produkt nainstalován, stav dostupnosti podpory a odkaz na Další informace o dalších krocích, které je potřeba provést. V grafu jsou zahrnuty následující informace:     
    - Zbývající čas podpory
    - Číslo v prostředí 
    - Datum ukončení běžné podpory
    - Datum ukončení rozšířené podpory
    - Další kroky  

> [!IMPORTANT]  
> Informace zobrazené na tomto řídicím panelu jsou určené pro vaši pohodlí a jenom pro interní použití ve vaší společnosti. Neměli byste výhradně spoléhat na tyto informace, abyste potvrdili dodržování předpisů. Ujistěte se, že jste ověřili přesnost informací, které jsou vám k dispozici, spolu s dostupností informací o podpoře návštěvou [zásad životního cyklu Microsoftu](https://support.microsoft.com/lifecycle).  



## <a name="reporting"></a>Generování sestav

K dispozici jsou také další sestavy. V konzole Configuration Manager otevřete pracovní prostor **monitorování** , rozbalte položku **vytváření sestav**a rozbalte položku **sestavy**. Do kategorie **funkce Asset Intelligence**přidány následující nové sestavy:  

- **Životní cyklus 01A – počítače s konkrétním softwarovým produktem**: Prohlédněte si seznam počítačů, ve kterých se zjistil zadaný produkt.  

- **Životní cyklus 02A – seznam počítačů s produkty, jejichž platnost vypršela v organizaci**, najdete v počítačích, na kterých skončila platnost produktů. Tuto sestavu můžete filtrovat podle názvu produktu.

- **Životní cyklus 03A – seznam produktů s vypršenou platností nalezených v organizaci**: Zobrazit podrobnosti o produktech ve vašem prostředí, jejichž data životního cyklu vypršela.  

- **Životní cyklus 04A – obecný přehled životního cyklu produktu**: zobrazení seznamu životního cyklu produktu. Vyfiltruje seznam podle názvu produktu a dnů pro vypršení platnosti.  

- **Životní cyklus 05A – řídicí panel životního cyklu produktu**: počínaje verzí 1810 Tato sestava obsahuje podobné informace jako na řídicím panelu v konzole. Vyberte kategorii pro zobrazení počtu produktů ve vašem prostředí a dnů zbývající podpory.  

Další informace najdete v tématu [Seznam sestav](../../../servers/manage/list-of-reports.md#asset-intelligence).<!--SCCMDocs issue 997-->  
