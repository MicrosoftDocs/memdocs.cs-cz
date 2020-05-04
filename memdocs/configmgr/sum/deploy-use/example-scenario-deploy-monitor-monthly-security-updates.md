---
title: Ukázkový scénář pro nasazení a monitorování aktualizací
titleSuffix: Configuration Manager
description: Použití aktualizací softwaru v Configuration Manager k nasazení a monitorování měsíčních aktualizací softwaru.
ms.date: 10/21/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: c32f757a-02da-43f2-b055-5cfd097d8c43
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ea654c4ec13b95b78a65c85d9d36ce576619854e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714910"
---
# <a name="example-scenario-to-deploy-and-monitor-monthly-software-updates"></a>Příklad scénáře nasazení a monitorování měsíčních aktualizací softwaru

*Platí pro: Configuration Manager (Current Branch)*

V tomto tématu najdete příklad scénáře použití aktualizací softwaru v nástroji Configuration Manager k nasazení a monitorování aktualizací zabezpečení softwaru, které společnost Microsoft vydává měsíčně.  

 V tomto scénáři sledujeme akce správce Configuration Manager v Woodgrove Bank. Správce musí vytvořit strategii nasazení aktualizace softwaru s následujícími podmínkami a požadavky:  

- Aktivní nasazení aktualizací softwaru probíhá jeden týden poté, kdy společnost Microsoft druhé úterý v každém měsíci vydá aktualizace zabezpečení softwaru. Tato událost je obvykle označována jako úterní oprava (Patch Tuesday).  

- Aktualizace softwaru jsou staženy a připraveny v distribučních bodech. Pak je nasazení otestováno na podmnožinu klientů před tím, než správce nástroje ConfigMgr plně nasadí aktualizace softwaru ve svém provozním prostředí.  

- Správce musí být schopný monitorovat dodržování předpisů pro aktualizace softwaru po měsících nebo po rocích.  

  Tento scénář předpokládá, že již byla implementována infrastruktura bodů aktualizace softwaru. Následující informace použijte k naplánování a konfiguraci aktualizací softwaru v nástroji Configuration Manager.  

|Proces|Referenční informace|  
|-------------|---------------|  
|Posouzení klíčových koncepcí aktualizací softwaru.|[Úvod do aktualizací softwaru](../understand/software-updates-introduction.md)|  
|Plánování aktualizací softwaru. Tyto informace vám pomohou při plánování kapacit, návrhu infrastruktury bodů aktualizace softwaru, instalaci bodů aktualizace softwaru, nastavení synchronizace a nastavení klientů pro aktualizace softwaru.|[Plánování aktualizací softwaru](../plan-design/plan-for-software-updates.md)|  
|Konfigurace aktualizací softwaru. Tyto informace vám pomohou při instalaci a konfiguraci bodů aktualizace softwaru v hierarchii a při konfiguraci a synchronizaci aktualizací softwaru.<br /><br /> V tomto scénáři správce nástroje ConfigMgr nakonfiguruje plán synchronizace aktualizací softwaru tak, aby se vyskytnout v druhé středu každého měsíce, aby bylo zajištěno, že získají nejnovější aktualizace zabezpečení softwaru od Microsoftu.|[Synchronizace aktualizací softwaru](../get-started/synchronize-software-updates.md)|  

 V následujících částech tohoto tématu najdete příklady kroků, které vám pomůžou nasadit a monitorovat aktualizace softwaru Configuration Manager zabezpečení ve vaší organizaci.

##  <a name="step-1-create-a-software-update-group-for-yearly-compliance"></a><a name="BKMK_Step1"></a>Krok 1: Vytvoření skupiny aktualizace softwaru pro roční dodržování předpisů  
 Správce Configuration Manager vytvoří skupinu aktualizací softwaru, která se dá použít k monitorování dodržování předpisů pro všechny aktualizace zabezpečení softwaru vydané v 2016. Správce provede kroky uvedené v následující tabulce.  

|Proces|Referenční informace|  
|-------------|---------------|  
|V uzlu **všechny aktualizace softwaru** v konzole Configuration Manager přidá správce Configuration Manager kritéria k zobrazení pouze aktualizací zabezpečení softwaru, které byly vydány nebo revidovány v roce 2015, které splňují následující kritéria:<br /><br /><ul><li>**Kritéria**: Datum vydání nebo revize</li><li>**Podmínka**: je větší nebo rovno určitému datu<br />**Hodnota**: 1. 1. 2015</li><li>**Kritéria**: Klasifikace aktualizací<br />**Hodnota**: Aktualizace zabezpečení</li><li>**Kritéria**: Konec platnosti <br />**Hodnota**: Ne</li></ul>|Žádné další informace|
|Správce nástroje ConfigMgr přidá všechny filtrované aktualizace softwaru do nové skupiny aktualizací softwaru s následujícími požadavky:<br /><br /><ul><li>**Název**: Skupina dodržování předpisů – Aktualizace zabezpečení Microsoftu 2015</li><li>**Popis**: Aktualizace softwaru|[Přidání aktualizací softwaru do skupiny aktualizací](add-software-updates-to-an-update-group.md)|  

##  <a name="step-2-create-an-automatic-deployment-rule-for-the-current-month"></a><a name="BKMK_Step2"></a>Krok 2: vytvoření pravidla automatického nasazení pro aktuální měsíc  
 Správce Configuration Manager vytvoří pravidlo automatického nasazení pro aktualizace zabezpečení softwaru vydané společností Microsoft pro aktuální měsíc. Správce provede kroky uvedené v následující tabulce.  

|Proces|Referenční informace|  
|-------------|---------------|  
|Správce nástroje ConfigMgr vytvoří pravidlo automatického nasazení s následujícími požadavky:<br /><br /><ol><li>Na kartě **Obecné** nakonfiguruje správce nástroje ConfigMgr následující:<br /> <ul><li>Určuje **měsíční aktualizace zabezpečení** pro název.</li><li>Vybere testovací kolekci s omezenými klienty.</li><li>Vybere **vytvořit novou skupinu aktualizací softwaru**.</li><li>Ověří, jestli není vybraná **možnost povolit nasazení po spuštění tohoto pravidla** .</li></ul></li><li>Na kartě **nastavení nasazení** vybere správce nástroje ConfigMgr výchozí nastavení.</li><li>Na stránce **aktualizace softwaru** nakonfiguruje správce nástroje ConfigMgr následující filtry vlastností a kritéria vyhledávání:<br /><ul><li>Datum vydání nebo revize **Poslední 1 měsíc**.</li><li>Klasifikace aktualizací **Aktualizace zabezpečení**.</li></ul></li><li>Na stránce **vyhodnocení** povolí správce ConfigMgr pravidlo, které se spustí podle plánu **druhého čtvrtek** v každém **měsíci**.  Správce nástroje ConfigMgr taky ověří, že je jeho plán synchronizace nastavený tak, aby běžel ve **druhé středu** v každém **měsíci**.</li><li>Správce nástroje ConfigMgr používá výchozí nastavení na stránkách plán nasazení, činnost koncového uživatele, výstrahy a nastavení stahování.</li><li>Na stránce **balíček pro nasazení** určí správce ConfigMgr nový balíček pro nasazení.</li><li>Správce nástroje ConfigMgr používá výchozí nastavení na stránkách umístění pro stahování a výběr jazyka.</li></ol>|[Automatické nasazení aktualizací softwaru](automatically-deploy-software-updates.md)|  

##  <a name="step-3-verify-that-software-updates-are-ready-to-deploy"></a><a name="BKMK_Step3"></a>Krok 3: Ověření připravenosti aktualizací softwaru k nasazení  
 Ve druhém čtvrtek v každém měsíci správce nástroje ConfigMgr ověří, zda jsou aktualizace softwaru připraveny k nasazení. Správce provede následující krok.  

|Proces|Referenční informace|  
|-------------|---------------|  
|Správce nástroje ConfigMgr ověří, zda synchronizace aktualizací softwaru byla úspěšně dokončena.|[Stav synchronizace aktualizace softwaru](monitor-software-updates.md#BKMK_SUSyncStatus)|  

##  <a name="step-4-deploy-the-software-update-group"></a><a name="BKMK_Step4"></a>Krok 4: nasazení skupiny aktualizací softwaru  
 Poté, co správce nástroje ConfigMgr ověří, že aktualizace softwaru jsou připraveny k nasazení, nasadí aktualizace softwaru. Správce provede kroky uvedené v následující tabulce.  

|Proces|Referenční informace|  
|-------------|---------------|  
|Správce nástroje ConfigMgr vytvoří pro novou skupinu aktualizací softwaru dvě testovací nasazení. Správce pro každé nasazení bere v úvahu následující prostředí:<br /><br /> **Nasazení testu pracovní stanice**: Správce nástroje ConfigMgr považuje při nasazení testu pracovní stanice za následující:<br /><br /><ul><li>Určuje kolekci nasazení, která obsahuje podmnožinu klientů pracovní stanice pro ověření nasazení.</li><li>Konfiguruje nastavení nasazení, která jsou vhodná pro klienty pracovní stanice ve svém prostředí.</li></ul><br />**Nasazení testovacího serveru**: Správce nástroje ConfigMgr považuje za pro nasazení serveru test za následující:<br /><br /><ul><li>Určuje kolekci nasazení, která obsahuje podmnožinu serverových klientů pro ověření nasazení.</li><li>Konfiguruje nastavení nasazení, která jsou vhodná pro klienty serveru ve svém prostředí.</li></ul>|[Nasazení aktualizací softwaru](deploy-software-updates.md)|  
|Správce nástroje ConfigMgr ověří, zda se testovací nasazení úspěšně nasadilo.|[Stav nasazení aktualizací softwaru](monitor-software-updates.md#BKMK_SUDeployStatus)|  
|Správce nástroje ConfigMgr aktualizuje dvě nasazení novými kolekcemi, které zahrnují provozní pracovní stanice a servery.|Žádné další informace|  

##  <a name="step-5-monitor-compliance-for-deployed-software-updates"></a><a name="BKMK_Step5"></a>Krok 5: monitorování dodržování předpisů nasazených aktualizací softwaru  
 Správce nástroje ConfigMgr monitoruje dodržování předpisů pro nasazení aktualizací softwaru. Správce provede krok v následující tabulce.  

|Proces|Referenční informace|  
|-------------|---------------|  
|Správce nástroje ConfigMgr monitoruje stav nasazení aktualizací softwaru v konzole Configuration Manager a kontroluje sestavy nasazení aktualizací softwaru, které jsou k dispozici v konzole nástroje.|[Monitorování aktualizací softwaru](../../sum/deploy-use/monitor-software-updates.md)|  

##  <a name="step-6-add-monthly-software-updates-to-the-yearly-update-group"></a><a name="BKMK_Step6"></a>Krok 6: Přidání měsíčních aktualizací softwaru do roční skupiny aktualizací  
 Správce nástroje ConfigMgr přidá aktualizace softwaru z měsíční skupiny aktualizací softwaru do roční skupiny aktualizací softwaru. Správce provede krok v následující tabulce.  

|Proces|Referenční informace|  
|-------------|---------------|  
|Správce nástroje ConfigMgr vybere aktualizace softwaru z měsíční skupiny aktualizací softwaru a přidá aktualizace softwaru do skupiny aktualizací softwaru, které byly vytvořeny pro roční dodržování předpisů. Správce sleduje dodržování aktualizací softwaru a vytváří různé sestavy pro správu.|[Přidání aktualizací softwaru do nasazené skupiny aktualizace](add-software-updates-to-an-update-group.md)|  

Správce nástroje ConfigMgr úspěšně dokončil měsíční nasazení aktualizací zabezpečení softwaru. Správce bude nadále monitorovat a sestavovat dodržování předpisů aktualizace softwaru, aby zajistil, že klienti ve svém prostředí jsou v rámci přijatelné úrovně dodržování předpisů.  

##  <a name="recurring-monthly-process-to-deploy-software-updates"></a><a name="BKMK_MonthlyProcess"></a>Opakovaný měsíční proces nasazení aktualizací softwaru  
 Po prvním měsíci, kdy náš správce nástroje ConfigMgr nasadí aktualizace softwaru, správce provede kroky tři až šest pro nasazení měsíčních aktualizací zabezpečení softwaru vydaných společností Microsoft.  
