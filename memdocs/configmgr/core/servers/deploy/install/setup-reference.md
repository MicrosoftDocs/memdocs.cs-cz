---
title: Referenční informace o instalaci
titleSuffix: Configuration Manager
description: Přečtěte si tento odkaz, který vám umožní připravit se na instalaci Configuration Manager lokality nebo hierarchie.
ms.date: 04/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d948452da54a41e35095b01cb0e942e02a7a597f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718067"
---
# <a name="reference-for-configuration-manager-setup"></a>Referenční informace k instalaci Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager instalační program poskytuje odkazy na několik témat, která jsou podrobně popsána v následujících částech. Informace, které jsou tady uvedené, vám pomohou připravit se na instalaci Configuration Manager lokality nebo hierarchie a pomáhat vám při přípravě na některá rozhodnutí, která je nutné provést během instalace.  


##  <a name="before-you-begin"></a><a name="bkmk_start"></a>Než začnete  
Než nainstalujete nové lokality Configuration Manager, ujistěte se, že jste zkontrolovali následující informace, které vám můžou usnadnit nastavení fáze úspěšného návrhu nasazení:  

-   [Základy nástroje Configuration Manager](../../../../core/understand/fundamentals.md)  
-   [Plánování infrastruktury Configuration Manager](../../../plan-design/network/configure-firewalls-ports-domains.md)  
-   [Příprava na instalaci Configuration Managerch lokalit](prepare-to-install-sites.md)  

##  <a name="assess-server-readiness"></a><a name="bkmk_assess"></a>Vyhodnocení připravenosti serveru  
Než začnete s instalací nové lokality, ujistěte se, že server lokality a vzdálené servery systému lokality, které chcete používat pro lokalitu (například server, který je hostitelem databáze lokality), splňují všechny požadované konfigurace. Tato témata v knihovně dokumentace vám mohou pomáhat:  

-   [Podporované konfigurace pro Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)  
-   [Kontrola požadovaných součástí](prerequisite-checker.md)  

##  <a name="clients-for-additional-operating-systems"></a><a name="bkmk_Addclients"></a>Klienti pro další operační systémy  
Klientský software pro Configuration Manager můžete stáhnout z webu Microsoft Download Center pro následující operační systémy:  

- macOS (Apple)
- UNIX
- Linux

Pomocí následujících odkazů můžete stáhnout klienty pro verzi Configuration Manager, kterou používáte:  

- [Klient Microsoft Endpoint Configuration Manager – macOS (64-bit)](https://www.microsoft.com/download/details.aspx?id=100850)

- [Klienti Microsoft Configuration Manager pro další operační systémy](https://www.microsoft.com/download/details.aspx?id=47719)

##  <a name="usage-data-levels-and-settings"></a><a name="bkmk_usage"></a> Úrovně a nastavení dat o využití  
Při instalaci první lokality Configuration Manager Configuration Manager automaticky nainstaluje a nakonfiguruje novou roli systému lokality, **spojovací bod služby**na serveru lokality. Spojovací bod služby má tato výchozí nastavení:  

-   **Online** režim (k dispozici je také offline režim)  
-   **Rozšířená** úroveň shromažďování dat (jsou k dispozici i ostatní úrovně shromažďování dat, základní a plná)  

Když je role systému lokality spojovacího bodu služby online, může společnost Microsoft automaticky shromažďovat informace o diagnostice a využití přes Internet. Shromážděné informace nám pomáhají:  

-   Identifikovat a řešit problémy  
-   Zlepšovat naše produkty a služby  
-   Identifikovat aktualizace pro Configuration Manager, které se vztahují na používanou verzi nástroje Configuration Manager  

### <a name="levels-of-data-collection"></a>Úrovně shromažďování dat  
Shromažďování dat zahrnuje tyto tři úrovně:

-   **Základní** zahrnuje data o nastavení a upgradu, jako je počet lokalit a které Configuration Manager funkce jsou povolené. Nepřenáší se žádné identifikovatelné osobní údaje.  

-   **Rozšířené** zahrnuje data v nastavení základní úrovně, a navíc přenáší data o hierarchii, způsobu použití jednotlivých funkcí (četnost a doba trvání) a rozšířené diagnostické informace, jako je stav paměti serveru, když dojde k chybě systému nebo aplikace. Nepřenáší se žádné identifikovatelné osobní údaje.  

-   **Úplný** zahrnuje data v nastavení základní a rozšířené úrovně a také odesílá rozšířené diagnostické informace, jako jsou systémové soubory a snímky paměti. Tato možnost může zahrnovat identifikovatelné osobní údaje, ale tyto informace nebudeme používat k tomu, aby vás identifikovala nebo kontaktovala, nebo aby vám mohla být zacílena na reklamu.  

Další informace, včetně informací o zpřístupnění podrobností shromážděných jednotlivými úrovněmi, najdete v tématu [Diagnostika a data o využití pro Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

Chcete-li zobrazit Configuration Manager prohlášení o zásadách ochrany osobních údajů na [https://go.microsoft.com/fwlink/?LinkID=626527](https://go.microsoft.com/fwlink/?LinkID=626527)řádku, použijte.
