---
title: Přehled souvisejících scénářů
titleSuffix: Microsoft Intune
description: Přečtěte si informace o scénářích s asistencí pro Intune, které jsou dostupné na portálu pro správu zařízení Microsoft 365.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/13/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 838c693bc8b5feefaaeb6386ecd02c3a4d1c82db
ms.sourcegitcommit: 1aeb4a11e89f68e8081d76ab013aef6b291c73c1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/14/2020
ms.locfileid: "88217191"
---
# <a name="intune-guided-scenarios-overview"></a>Přehled scénářů s asistencí pro Intune 

Scénář s asistencí je přizpůsobený sled kroků, které jsou na začátku celého případu použití. Běžné scénáře jsou založené na roli, kterou správce, uživatel nebo zařízení hraje ve vaší organizaci. Tyto role obvykle vyžadují kolekci pečlivě Orchestrované profily, nastavení, aplikace a kontroly zabezpečení, které poskytují nejlepší uživatelské prostředí a zabezpečení.    

Pokud nejste obeznámeni se všemi kroky a prostředky potřebnými k implementaci konkrétního scénáře Intune, můžete použít jako výchozí bod scénáře s asistencí. Ve scénáři s asistencí se automaticky sestaví zásady, aplikace, přiřazení a další konfigurace správy. Kromě toho můžou scénáře s asistencí záměrně vynechat některé možnosti, které nejsou pro daný scénář vhodné nebo nejsou běžné. 

Scénáře s asistencí nepatří mezi běžné pracovní postupy Intune o jiný prostor pro správu. Tyto pracovní postupy jsou určené k použití ve spojení s existujícími pracovními postupy služby Intune pro profily, aplikace a zásady. Po dokončení průvodce se musí v existujících nabídkách pro zásady, aplikace a profily provést veškerá budoucí Správa tohoto scénáře. Scénář s asistencí neukládá typ prostředku "s asistencí" nebo sleduje budoucí změny provedené v prostředcích. Všechny prostředky vytvořené ve scénáři s asistencí se zobrazí v příslušných úlohách. Všechny možnosti, i tyto možnosti vynechané ve scénáři s asistencí, budou k dispozici pro úpravy v existujících nabídkách.  

## <a name="types-of-guided-scenarios"></a>Typy scénářů s průvodcem 

V zájmu jednoduchosti vynechává všechny scénáře s asistencí složité funkce oboru, například značky oboru, skupiny vyloučení a přiřazení virtuálních skupin. Všechny prostředky vytvořené ve scénáři s asistencí zdědí všechny značky oboru správce, který dokončí scénář. Některé scénáře nabízejí určitou úroveň přizpůsobení pro běžné nastavení, které pokrývá úzce související scénáře. Tyto scénáře, přiřazení skupiny podpory pouze pro skupiny zahrnutí. U dalších scénářů s asistencí celý scénář garantuje jednotné prostředí tím, že nabízí žádné přizpůsobení a automaticky vygeneruje novou skupinu pro příjem všech přiřazení. Až se průvodce dokončí, budete moct používat složitější přiřazení přímo prostřednictvím stávajících zásad, úloh aplikací a profilů.  

Následující scénáře jsou vedeny: 
- Nasazení Microsoft Edge pro mobilní zařízení 
- Vyzkoušejte si cloudový počítač spravovaný
- Zabezpečená systém Microsoft Office pro mobilní zařízení 

## <a name="guided-scenario-functionality"></a>Funkce scénáře s asistencí 

Scénáře s asistencí nabízejí konkrétní funkce. Následující podrobnosti vám pomohou vysvětlit, co můžete a nemůžete provést během postupu s asistencí.

### <a name="launching"></a>Spouštění  

Všechny scénáře s asistencí jsou k dispozici na **[portálu pro správu zařízení](https://endpoint.microsoft.com)**  >  **řešení potíží a**ve  >  **scénářích s asistencí**. 

Scénář s asistencí začíná úvodem, který vysvětluje účel scénáře a všechny nezbytné součásti potřebné k dokončení instalace. V tomto okamžiku se kontrolují vaše oprávnění správce, aby se ověřilo, že máte všechna potřebná oprávnění k dokončení tohoto scénáře.  

Po předání všech kontrol požadovaných součástí scénář nabízí vhodná nastavení pro přizpůsobení. Scénáře s asistencí mají za cíl vyžadovat vstup jenom pro minimální počet nastavení a skrýt neobvyklá nebo Pokročilá nastavení, dokud to nepotřebuje nebo na základě zvláštních okolností. Jednotlivé scénáře s průvodcem odkazují na dokumentaci, která obsahuje další podrobnosti. 

Po zadání všech povinných nastavení zobrazí scénář s asistencí Souhrn zadaných nastavení a prostředků, které scénář vyžaduje. V tomto okamžiku se nic neuložilo, pokud není výslovně uvedeno.

Dalším krokem je nasazení scénáře. Nasazení scénáře vytvoří a uloží všechny nezbytné prostředky a vybraná nastavení. Čas potřebný k dokončení nasazení se liší podle scénáře. Po dokončení nasazení zobrazí scénář s asistencí seznam vytvořených prostředků s odkazy na zobrazení správy jednotlivých prostředků, na normální úlohy a dokumentaci prostředku. 

> [!IMPORTANT]
> Seznam uvedený na konci scénáře s asistencí není uložen a je možné jej zobrazit pouze v případě, že je otevřený scénář s asistencí.  
Pokud při nasazení scénáře dojde k chybě, všechny změny se vrátí. 

### <a name="editing"></a>Probíhají úpravy 

Scénáře s asistencí nelze použít pro úpravu existujících prostředků. Po vytvoření se musí všechny prostředky, skupiny a přiřazení upravovat pomocí stávajících úloh.

### <a name="monitoring"></a>Monitorování 

Scénáře s asistencí nelze použít k monitorování existujících prostředků kromě procesu prvotního vytvoření. Po vytvoření se musí všechny prostředky, skupiny a přiřazení monitorovat pomocí stávajících úloh. 

### <a name="retiring"></a>Vyřazení 

Scénáře s asistencí nelze použít k vyřazení existujících prostředků Kromě automatického vyčištění během chyby při počátečním nasazení. Po vytvoření musí být všechny prostředky, skupiny a přiřazení vyřazeny pomocí stávajících úloh. 

### <a name="updating"></a>Doplnění

V době, kdy se vyvíjí technologie, může Intune čas od času aktualizovat scénář s asistencí pro zlepšení uživatelského prostředí, zabezpečení nebo dalších aspektů scénáře. Tato aktualizace bude mít vliv jenom na nová nasazení vytvořená ve scénáři s asistencí. Intune nebude aktualizovat existující prostředky dřív vygenerované scénářem s asistencí, aby odpovídaly novým osvědčeným postupům nebo doporučením.  

## <a name="next-steps"></a>Další kroky

Pokud chcete rychle začít pracovat na Microsoft Intune, Projděte si scénáře s asistencí pro Intune. Pokud s Intune začínáte, nastavte svého tenanta Intune podle pokynů k [rychlému zprovoznění bezplatné zkušební verze](free-trial-sign-up.md).
