---
title: Zjistit prostředky zařízení a uživatele
titleSuffix: Configuration Manager
description: Přečtěte si přehled procesu zjišťování a záznamů dat zjišťování.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1869c9e6de455b7086a051db91bb26bc00a91a5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718368"
---
# <a name="run-discovery-for-configuration-manager"></a>Spustit zjišťování pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pomocí jedné nebo několika metod zjišťování v nástroji Configuration Manager můžete najít prostředky zařízení a uživatele, které můžete spravovat. K identifikaci síťové infrastruktury ve vašem prostředí můžete také použít zjišťování. K dispozici je několik různých metod, které můžete použít ke zjištění různých věcí, přičemž každá z metod má svou vlastní konfiguraci a omezení.  

## <a name="overview-of-discovery"></a>Přehled zjišťování  
 Zjišťování je proces, pomocí kterého se Configuration Manager seznámí s akcemi, které můžete spravovat. Dostupné metody zjišťování jsou následující:  

-   Zjišťování lokalit a podsítí v doménových strukturách služby Active Directory  

-   Zjišťování skupiny aktivního adresáře  

-   Zjišťování systému aktivního adresáře  

-   Zjišťování uživatele Active Directory  

-   Zjišťování prezenčního signálu  

-   Zjištění sítě  

-   Zjišťování serveru  

> [!TIP]  
>  Informace o jednotlivých metodách zjišťování najdete v části [informace o metodách zjišťování pro Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  
>   
>  Pomoc při výběru metod, které se mají použít, a na kterých lokalitách ve vaší hierarchii najdete v tématu [Výběr metod zjišťování, které se mají použít pro Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md).  

 Chcete-li použít většinu metod zjišťování, musíte v lokalitě povolit metodu a nastavit ji tak, aby prohledala umístění v síti nebo ve službě Active Directory. Po spuštění se dotazuje na zadané umístění pro informace o zařízeních nebo uživatelích, které Configuration Manager můžou spravovat. Když metoda zjišťování úspěšně vyhledá informace o prostředku, uloží tyto informace do souboru s názvem záznam dat zjišťování (DDR). Tento soubor pak zpracovává primární lokalita nebo lokalita centrální správy. Při zpracování záznamu DDR se vytvoří nový záznam v databázi lokality pro nově zjištěné prostředky nebo se novými informacemi aktualizují existující záznamy.  

 Některé metody zjišťování můžou generovat velký objem síťových přenosů a záznamy DDR, které vytvářejí, můžou během zpracování způsobit výrazné využití prostředků procesoru. Proto naplánujte použití pouze těch metod zjišťování, které požadujete pro splnění vašich cílů. Můžete začít používat jenom jednu nebo dvě metody zjišťování a později kontrolovaně povolit další metody, a rozšířit tak úroveň zjišťování ve vašem prostředí.  

 Po přidání informací o zjišťování do databáze lokality se tyto informace replikují do každé lokality v hierarchii, bez ohledu na to, kde se zjistily nebo zpracovaly. Proto můžete nastavit různé plány a nastavení pro metody zjišťování v různých lokalitách, ale můžete spustit konkrétní metodu zjišťování pouze v jedné lokalitě. Tím se snižuje využití šířky pásma sítě prostřednictvím duplicitních akcí zjišťování a snižuje se zpracování redundantních dat zjišťování ve více lokalitách.  

 Data zjišťování můžete použít k vytvoření vlastních kolekcí a dotazů, které logicky seskupují prostředky pro úlohy správy. Příklad:  

-   Doručování instalací klienta nebo upgrade.  

-   Nasazení obsahu pro uživatele nebo zařízení.  

-   Nasazení nastavení klienta a souvisejících konfigurací.

##  <a name="about-discovery-data-records"></a><a name="BKMK_DDRs"></a>Záznamy dat zjišťování  
 Záznamy DDR jsou soubory vytvořené metodou zjišťování. Obsahují informace o prostředku, který můžete spravovat v Configuration Manager, jako jsou počítače, uživatelé a v některých případech i síťová infrastruktura. Jsou zpracovávány v primárních lokalitách nebo v lokalitách centrální správy. Po zadání informací o zdroji v záznamu DDR do databáze je záznam DDR vymazán a informace jsou replikovány jako globální data do všech lokalit v hierarchii.  

 Lokalita, ve které je záznam DDR zpracováván, závisí na informacích, které záznam obsahuje:  

-   Záznamy DDR pro nově zjištěné prostředky, které nejsou v databázi, jsou zpracovávány v lokalitě nejvyšší úrovně v hierarchii. Lokalita nejvyšší úrovně vytvoří nový záznam o prostředku v databázi a přiřadí mu jedinečný identifikátor. DDR se přenášejí pomocí replikace na základě souborů, dokud se nedostanou do lokality nejvyšší úrovně.  

-   Záznamy DDR pro dříve nalezené objekty jsou zpracovávány v primárních lokalitách. Podřízené primární lokality nepřenášejí záznamy DDR do lokality centrální správy, když záznam DDR obsahuje informace o zdroji, který se již v databázi nachází.  

-   Sekundární lokality nezpracovávají záznamy DDR a vždy je přenáší pomocí replikace na základě souborů do své nadřazené primární lokality.  

Soubory záznamů DDR jsou identifikovány příponou .ddr a obvykle mají velikost asi 1 kB.  

## <a name="get-started-with-discovery"></a>Začínáme se zjišťováním  
 Předtím, než použijete konzolu Configuration Manager k nastavení zjišťování, byste měli porozumět rozdílům mezi metodami, co můžou dělat, a v některých případech i jejich omezení.  

Následující témata mohou vytvořit základ, který vám pomůže úspěšně používat metody zjišťování:  

-   [O metodách zjišťování pro Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [Vyberte metody zjišťování, které se mají použít pro Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)  

Až porozumíte metodám, které chcete použít, najdete pokyny k nastavení jednotlivých metod v části [Konfigurace metod zjišťování pro Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  
