---
title: Nasazení aktualizací softwaru
titleSuffix: Configuration Manager
description: Přečtěte si, jak ručně nebo automaticky nasadit aktualizace softwaru v konzole Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.openlocfilehash: 5cee950e2b42d73f20921c2baf08b98d2d206586
ms.sourcegitcommit: 8fc7f2864c5e3f177e6657b684c5f208d6c2a1b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/19/2020
ms.locfileid: "88591184"
---
# <a name="deploy-software-updates"></a>Nasazení aktualizací softwaru  

*Platí pro: Configuration Manager (Current Branch)*

Fáze nasazení aktualizace softwaru je proces nasazení aktualizací softwaru. Bez ohledu na to, jak nasazujete aktualizace softwaru, lokalita:
- Přidá aktualizace do skupiny aktualizací softwaru.
- Distribuuje obsah aktualizace do distribučních bodů.
- Nasadí skupinu aktualizací do klientů.  

Po vytvoření nasazení lokalita odešle do cílových klientů přidruženou zásadu aktualizace softwaru. Klienti stáhnou soubory obsahu aktualizace softwaru ze zdroje obsahu do místní mezipaměti. Klienti na internetu vždycky stahují obsah z cloudové služby Microsoft Update. Aktualizace softwaru jsou následně k dispozici pro instalaci klientem.   

> [!Tip]  
>  Pokud distribuční bod není k dispozici, mohou klienti v intranetu stahovat také aktualizace softwaru z Microsoft Update.  

> [!NOTE]  
>  Na rozdíl od jiných typů nasazení jsou všechny aktualizace softwaru staženy do mezipaměti klienta. To je bez ohledu na nastavení maximální velikosti mezipaměti v klientovi. Další informace o nastavení mezipaměti klienta najdete v tématu [Konfigurace mezipaměti klienta pro klienty Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

Chcete-li konfigurovat požadované nasazení aktualizace softwaru, aktualizace softwaru budou automaticky nainstalovány v plánovaném termínu. Případně může uživatel na klientském počítači naplánovat nebo zahájit instalaci aktualizace softwaru před termínem. Po pokusu o instalaci klientské počítače odešlou stavové zprávy zpět na server lokality, což značí úspěšnou instalaci aktualizace softwaru. Další informace o nasazení aktualizace softwaru najdete v tématu [Pracovní postupy nasazení aktualizací softwaru](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows).  

Existují tři hlavní scénáře nasazení aktualizací softwaru: 
- [Ruční nasazení](#BKMK_ManualDeployment)  
- [Automatické nasazení](#bkmk_auto)  
- [Dvoufázové nasazení](#bkmk_phased)  

Obvykle zahájíte ručním nasazením aktualizací softwaru k vytvoření směrného plánu pro klienty a potom můžete aktualizace softwaru na klienty spravovat pomocí automatického nebo dvoufázového nasazení.  

> [!Note]  
> Nemůžete použít pravidlo automatického nasazení se dvoufázovém nasazením.



## <a name="manually-deploy-software-updates"></a><a name="BKMK_ManualDeployment"></a> Ruční nasazení aktualizací softwaru
V konzole Configuration Manager vyberte aktualizace softwaru a ručně spusťte proces nasazení. Tato metoda nasazení se obvykle používá pro:  

- Před vytvořením pravidel automatického nasazení, která spravují měsíční nasazení, Získejte klienty v aktuálním stavu pomocí požadovaných aktualizací softwaru.  

- Nasazení aktualizací softwaru mimo IP síť  


Následující seznam shrnuje obecný postup ručního nasazení aktualizací softwaru:  

1. Vyfiltrování aktualizací softwaru využívajících konkrétní požadavky. Například zadejte kritéria, která načte všechny aktualizace zabezpečení nebo kritické aktualizace softwaru, které jsou vyžadovány více než 50 klientů.  

2. Vytvoření skupiny aktualizací softwaru, která obsahuje aktualizace softwaru.  

3. Stažení obsahu aktualizací softwaru ve skupině aktualizací softwaru.  

4. Ruční nasazení skupiny aktualizací softwaru.  

Další informace a podrobné pokyny najdete v tématu [Ruční nasazení aktualizací softwaru](manually-deploy-software-updates.md).

> [!Note]
> - Od 21. dubna 2020 se sada Office 365 ProPlus přejmenovává na **Microsoft 365 aplikace pro podniky**. Další informace najdete v tématu [Změna názvu pro Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). V konzole Configuration Manager se pořád zobrazují odkazy na starý název a podpůrná dokumentace, zatímco se konzola aktualizuje.
> - Když ručně nasazujete aktualizace klienta Microsoft 365 Apps, najdete je v uzlu **aktualizace sady office 365** v části **Správa klientů v sadě Office 365** v pracovním prostoru **softwarová knihovna** . 

## <a name="automatically-deploy-software-updates"></a><a name="bkmk_auto"></a> Automaticky nasadit aktualizace softwaru

Nakonfigurujte automatické nasazení aktualizací softwaru pomocí pravidla automatického nasazení (ADR). Tato metoda nasazení je společná pro měsíční aktualizace softwaru (obvykle se označuje jako "patch úterý") a ke správě aktualizací definic. Určete kritéria pro pravidlo automatického nasazení pro automatizaci procesu nasazení. Následující seznam poskytuje obecný pracovní postup pro automatické nasazení aktualizací softwaru:  

1.  Vytvořte pravidlo automatického nasazení, které určuje nastavení nasazení.  

2.  Lokalita přidá aktualizace softwaru do skupiny aktualizace softwaru.  

3.  Lokalita nasadí skupinu aktualizace softwaru na klienty v cílové kolekci.  

Nejprve určete automatickou strategii nasazení aktualizace softwaru. Můžete například vytvořit pravidlo automatického nasazení na počáteční cílovou kolekci testovacích klientů. Po ověření, že testovací skupina úspěšně nainstalovala aktualizace softwaru, přidejte do pravidla nové nasazení. Můžete také změnit cílovou kolekci v existujícím nasazení na jednu, která obsahuje větší skupinu klientů. Při rozhodování o strategii, která se má použít, vezměte v úvahu následující chování:  

- Můžete upravit vlastnosti objektů aktualizace softwaru, které vytvoří ADR.   

- ADR automaticky nasadí aktualizace softwaru na klienty, když je přidáte do cílové kolekce.  

- Když vy nebo ADR přidáte do skupiny aktualizace softwaru nové aktualizace softwaru, lokalita je automaticky nasadí do klientů v cílové kolekci.  

- Povolte nebo zakažte nasazení kdykoli pro pravidlo automatického nasazení.  


Po vytvoření pravidla automatického nasazení přidejte do pravidla další nasazení. Tato akce vám pomůže spravovat složitost nasazení různých aktualizací do různých kolekcí. Každé nové nasazení má plný rozsah funkcí a možností monitorování.  

Každé nové nasazení, které přidáte:  

- Používá stejnou skupinu aktualizací a balíček, které pravidla automatického nasazení vytvoří při prvním spuštění.  
- Může cílit na jinou kolekci.  
- Podporuje jedinečné vlastnosti nasazení včetně vlastností:  
  -   Čas aktivace  
  -   Termín  
  -   Uživatelské prostředí  
  -   Samostatné výstrahy pro každé nasazení  


Další informace a podrobné pokyny najdete v tématu [automatické nasazení aktualizací softwaru](automatically-deploy-software-updates.md) .



## <a name="deploy-software-updates-in-phases"></a><a name="bkmk_phased"></a> Nasazení aktualizací softwaru ve fázích

<!--1358146-->
Počínaje verzí 1810 vytvořte dvoufázové nasazení pro aktualizace softwaru. Postupné nasazení vám umožní orchestrovat koordinované, sekvenční zavedení softwaru na základě přizpůsobitelných kritérií a skupin.

Další informace najdete v tématu [Vytvoření dvoufázové nasazení](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json).

