---
title: Scénáře instalace
titleSuffix: Configuration Manager
description: Naučte se techniky pro instalaci nové hierarchie Configuration Manager při aktualizaci nebo upgradu lokality.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a63667faf9590f647c01565f1425081e53bdfc97
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718095"
---
# <a name="scenarios-to-streamline-your-installation-of-configuration-manager"></a>Scénáře pro zjednodušení instalace Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

S vydáním aktualizovaných verzí pro Configuration Manager aktuální větve nástroje existují nové scénáře, které zjednodušují instalaci nové hierarchie na aktualizovanou verzi (například aktualizaci 1610) a upgrade z Configuration Manager Microsoft System Center 2012.

Mezi podporované scénáře patří:  

**Nainstaluje novou Configuration Manager hierarchie aktuální větve** , která spouští verzi aktualizace.  

-   Nainstalujte pouze lokalitu nejvyšší úrovně a potom okamžitě nainstalujte aktualizaci, aby se tato lokalita aktualizovala s aktualizovanou verzí, kterou budete používat. Pak můžete nainstalovat další lokality přímo do této verze aktualizace.  
-   V tomto scénáři přeskočíte proces instalace dalších lokalit do úrovně základní hodnoty a jejich aktualizaci na verzi aktualizace, kterou chcete použít.  
-   V tomto scénáři přeskočíte proces instalace klientů do základní verze a pak je znovu nainstalujete při aktualizaci na novější verzi.  

**Upgradujte infrastrukturu Microsoft System Center 2012 Configuration Manager** na aktualizovanou verzi Configuration Manager.  

-   Před instalací aktualizované verze (například verze 1610) ručně upgradujte lokalitu centrální správy a každou primární lokalitu na základní verzi (například verzi 1606).  
-   Neprovádějte upgrade sekundárních lokalit z nástroje Microsoft System Center 2012 Configuration Manager, dokud vaše primární lokality nespustí verzi aktualizace, kterou budete používat.  
-   Neprovádějte upgrade klientů z nástroje Microsoft System Center 2012 Configuration Manager, dokud vaše primární lokality nespustí verzi aktualizace, kterou budete používat.  

## <a name="scenario-install-a-new-hierarchy-to-an-update-version"></a>Scénář: instalace nové hierarchie do aktualizované verze  
V tomto ukázkovém scénáři nainstalujete první lokalitu hierarchie pomocí základní verze Configuration Manager, jako je verze 1610. Pak nainstalujte aktualizaci 1610 ještě před nasazením dalších lokalit nebo klientů.  

-   Vzhledem k tomu, že máte v úmyslu použít aktualizovanou verzi (například verzi 1610) a nezůstanete u základní verze (například verze 1606), nemusíte instalovat další lokality a pak je upgradovat. To platí i pro klienty.  
-   Neinstalujte sekundární lokality verze 1606 a pak je upgradujte na verzi 1610. Místo toho nainstalujte sekundární lokality po spuštění primárních lokalit verze 1610.  

Postupujte podle tohoto pořadí:  

1. **Nainstalujte lokalitu nejvyšší úrovně pro novou hierarchii** pomocí základního média.  

   -   K instalaci první lokality nové hierarchie můžete použít jenom základní média.  
   -   Například nainstalujte lokalitu nejvyšší úrovně s použitím základní verze 1606. Další informace najdete v tématu [Instalace lokalit pomocí Průvodce instalací](use-the-setup-wizard-to-install-sites.md)nástroje.  

   Po provedení tohoto kroku bude mít lokalita nejvyšší úrovně verzi 1606.  

2. **Pomocí konzolových aktualizací můžete aktualizovat lokalitu nejvyšší úrovně na novější verzi.**  

   -   Před instalací jakýchkoli podřízených lokalit nebo klientů aktualizujte lokalitu nejvyšší úrovně na verzi aktualizace, kterou plánujete použít.  
   -   Například můžete aktualizovat lokalitu nejvyšší úrovně, na které běží verze 1606, na verzi 1610. Další informace najdete v tématu [aktualizace pro Configuration Manager](../../../../core/servers/manage/updates.md).  

   Po provedení tohoto kroku bude mít lokalita nejvyšší úrovně verzi 1610.  

3. **Nainstalujte nové podřízené primární lokality pod lokalitu centrální správy.**  

   - K instalaci podřízených primárních lokalit použijte instalační média ze složky CD.Latest na serveru lokality centrální správy. Další informace najdete [na disku CD. Poslední složka pro Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md).  

     Zdrojové médium zajistí, že verze nové podřízené primární lokality odpovídá verzi lokality centrální správy.  

   Po provedení tohoto kroku budou vaše nové podřízené primární lokality používat verzi 1610.  

4. **V každé primární lokalitě použijte konzolovou možnost k instalaci nových sekundárních lokalit.**  

   -   Protože jste sekundární lokality neinstalovali v době, kdy byly primární lokality ve verzi 1606, nemusíte upgradovat sekundární lokality.  
   -   Místo toho nainstalujte nové sekundární lokality, na kterých běží verze 1610. Další informace najdete v oddílu [Instalace sekundární lokality](use-the-setup-wizard-to-install-sites.md#bkmk_secondary) v tématu [Instalace lokalit pomocí Průvodce instalací](use-the-setup-wizard-to-install-sites.md) .  

   Po provedení tohoto kroku se nainstalují nové sekundární lokality a spustí se verze 1610.  

5. **Nainstalujte nové klienty v primární lokalitě.**  

   -   Vzhledem k tomu, že jste klienty neinstalovali v době, kdy byly primární lokality ve verzi 1606, není nutné upgradovat klienty z verze 1606 na verzi 1610.  
   -   Místo toho nainstalujte nové klienty, kteří používají verzi 1610. Další informace najdete v tématu [nasazení klientů](../../../clients/deploy/deploy-clients-to-windows-computers.md).  

   Po dokončení tohoto kroku se nainstalují noví klienti, kteří používají verzi 1610.  

## <a name="scenario-upgrade-system-center-2012-configuration-manager-to-an-update-version-of-configuration-manager-current-branch"></a>Scénář: upgrade verze System Center 2012 Configuration Manager na aktualizovanou verzi Configuration Manager, aktuální větev  

V tomto ukázkovém scénáři provedete upgrade Configuration Manager infrastruktury nástroje System Center 2012 na aktualizovanou verzi Configuration Manager aktuální větve, jako je verze 1610.  

-   Lokalita centrální správy a každá primární lokalita musí před instalací aktualizace verze 1610 upgradovat na základní verzi 1606.  
-   Sekundární lokality a klienti neupgradují ani neinstalují verzi 1606. Místo toho se přesouvá přímo z nástroje System Center 2012 Configuration Manager na Configuration Manager aktuální větev verze 1610.  

Postupujte podle tohoto pořadí:  

1. **Upgradujte na nejvyšší úroveň serveru System Center 2012 Configuration Manager** na základní verzi aktuální větve pomocí zdrojového média pro Configuration Manager (jako je verze 1606). Další informace najdete v tématu [upgrade na Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

   -   Stejně jako tradiční scénáře upgradu vždy inovujete lokalitu nejvyšší úrovně v hierarchii a potom provedete upgrade podřízených lokalit.  

   Po provedení tohoto kroku bude mít lokalita nejvyšší úrovně verzi 1606.  

2. **Upgradujte každou podřízenou primární lokalitu v hierarchii** na stejnou základní verzi.  

   -   Při upgradu z nástroje Microsoft System Center 2012 Configuration Manager je třeba ručně upgradovat každou primární lokalitu na základní verzi aktuální větve.  
   -   V tuto chvíli nebudete upgradovat sekundární lokality.  

   Po provedení tohoto kroku bude každá primární lokalita používat verzi 1606.  

3. **Nastavení časových intervalů pro správu a údržbu v podřízených primárních lokalitách.** Po upgradu všech primárních lokalit na základní verzi Naplánujte konfiguraci časových intervalů pro správu a údržbu, které určují, kdy budou tyto lokality instalovat aktualizace infrastruktury. Další informace najdete v tématu [použití časových období údržby](../../../../core/clients/manage/collections/use-maintenance-windows.md).  (Časová období údržby se nazývají *Windows Service* ve verzi 1606.)  

   -   Podřízené primární lokality automaticky nainstalují stejné aktualizace, které nainstalujete na lokalitu centrální správy.  
   -   Sekundární lokality neinstalují neinstalují automaticky nové verze. Je nutné je ručně upgradovat v konzole nástroje.  

   Když dokončíte tento krok, pak po instalaci aktualizací na lokalitu centrální správy nainstalují podřízené primární lokality tuto aktualizaci pouze v době, kdy jim to dovolí jejich časové období údržby.  

4. **Nainstalujte aktualizovanou verzi na lokalitu nejvyšší úrovně.** Tím se aktualizuje lokalita nejvyšší úrovně. Jakmile lokalita centrální správy nainstaluje aktualizovanou verzi, každá podřízená primární lokalita automaticky nainstaluje aktualizaci, pokud není instalace blokována časovým obdobím údržby.  

   -   Například můžete aktualizovat lokalitu nejvyšší úrovně z verze 1606 na verzi 1610. Další informace najdete v tématu [aktualizace pro Configuration Manager](../../../../core/servers/manage/updates.md).  

   Po provedení tohoto kroku bude mít lokalita centrální správy a každá primární lokalita verzi 1610.  

5. **Upgradujte sekundární lokality.** Poté, co primární lokalita nainstaluje aktualizaci a spustí verzi 1610, použijte konzolovou možnost pro upgrade sekundárních lokalit.  

   -   Tím se sekundární lokality upgradují přímo z nástroje Microsoft System Center 2012 Configuration Manager na verzi aktualizace, kterou jste nainstalovali v primární lokalitě.  
   -   Informace o tom, jak upgradovat sekundární lokalitu, najdete v tématu [upgrade webů](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade) v tématu upgrade [na Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) .  

6. **Upgradujte klienty.** Chcete-li upgradovat klienty, použijte informace v tématu [Postup upgradu klientů pro počítače se systémem Windows](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

   -   Tato inovace klientů přímo z nástroje Microsoft System Center 2012 Configuration Manager na verzi aktualizace, kterou jste nainstalovali v primární lokalitě.  

   Po provedení tohoto kroku se klienti upgradují na verzi 1610 bez toho, aby se nejdřív upgradovali na verzi 1606.
