---
title: Úlohy správy pro aplikace
titleSuffix: Configuration Manager
description: Umožňuje spravovat Configuration Manager aplikace a typy nasazení.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c4041e21-21ff-4d95-ab05-14007e0047cf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 15c1be9ed388356e17f8591123114dccf7bcd612
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695201"
---
# <a name="management-tasks-for-configuration-manager-applications"></a>Úlohy správy pro aplikace Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Informace v tomto článku vám pomůžou při správě Configuration Manager aplikací a typů nasazení.  

Nápovědu k vytváření aplikací a typů nasazení najdete v tématu věnovaném [vytváření aplikací](../../apps/deploy-use/create-applications.md).  

> [!IMPORTANT]  
>  V závislosti na typu aplikace nebo typu nasazení nemusí být některé možnosti správy k dispozici.  

##  <a name="manage-applications"></a>Správa aplikací  
 V pracovním prostoru **softwarová knihovna** rozbalte položku aplikace pro **správu aplikací**  >  **Applications**, zvolte aplikaci, kterou chcete spravovat, a poté vyberte úlohu správy.  

|Úkol|Podrobnosti|  
|----------|-------------|  
|**Správa účtů pro přístup**|Otevře dialogové okno **Správa účtů pro přístup** , ve kterém můžete zadat povolenou úroveň přístupu pro obsah spojený s vybranou aplikací.|  
|**Vytvořit soubor připraveného obsahu**|Otevře stránku **Vytvořit Průvodce souborem připraveného obsahu** , která vám pomůže při správě distribuce obsahu do vzdálených distribučních bodů. Když plánování a sdružování nenabízí vhodné řešení pro vzdálený distribuční bod, můžete obsah distribučního bodu předem připravit.<br /><br /> Viz [Správa obsahu a infrastruktury obsahu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Historie revizí**|Otevře dialogové okno **Historie revizí aplikace** , které umožňuje zobrazit vlastnosti revizí, které byly provedeny v této aplikaci, odstranit staré revize aplikace a obnovit staré verze této aplikace.<br /><br /> Podívejte [se, jak revidovat a nahradit aplikace](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Vytvořit typ nasazení**|Otevře **Průvodce vytvořením typu nasazení** , který umožňuje přidat do vybrané aplikace nový typ nasazení.<br /><br /> Viz téma [Create Applications](../../apps/deploy-use/create-applications.md).|  
|**Aktualizovat statistiku**|Aktualizuje informace zobrazené v uzlu **Nasazení** pracovního prostoru **Sledování** , které se týkají nasazení této aplikace.<br /><br /> Viz [monitorování aplikací z konzoly Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md).|  
|**Obnovit vyřazenou aplikaci**|Obnoví aplikaci, která byla vyřazena pomocí úlohy správy **vyřadit** .|  
|**Vyřadit**|Když vyřadíte aplikaci, nebude již k dispozici pro nasazení, aplikace a nasazení aplikace však nebudou odstraněny. Stávající kopie aplikace instalované v klientských počítačích nebudou odebrány. Jakékoli revize aplikace se z Configuration Manageru odstraní po 60 dnech. Instalované kopie aplikace však odebrány nejsou.<br /><br /> Chcete-li odstranit aplikaci, je nutné nejprve vyřadit z aplikace, odstranit všechna nasazení, odebrat odkazy na aplikaci jinými nasazeními a poté odstranit všechny revize aplikace.<br /><br /> Viz [Revize a nahrazování aplikací](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Export**|Otevře **Průvodce exportem aplikace** , který umožňuje exportovat vybrané aplikace do souboru. zip, který pak můžete archivovat nebo nainstalovat do jiné lokality. Pokud se rozhodnete exportovat obsah aplikace, bude vytvořena složka s obsahem.<br /><br /> Můžete také exportovat závislosti aplikace, vztahy a podmínky nahrazení a obsah aplikace a jejích závislostí.<br /><br /> Rutina Windows PowerShellu **Export-CMApplication**má stejnou funkci. Další informace najdete v tématu [Export-CMApplication](/powershell/module/configurationmanager/export-cmapplication?view=sccm-ps).|  
|**Odstranit**|Odstraní právě vybranou aplikaci.<br /><br /> Nelze odstranit aplikaci, na níž jsou závislé jiné aplikace, ani aplikaci, která má aktivní nasazení nebo závislá pořadí úloh.|  
|**Simulovat nasazení**|Otevře **Průvodce simulací nasazení aplikace** , kde můžete testovat výsledky nasazení aplikace do počítačů bez skutečné instalace nebo odinstalace aplikace.<br /><br /> Viz [simulovat nasazení aplikace](../../apps/deploy-use/simulate-application-deployments.md).|  
|**Nasazení**|Otevře **Průvodce nasazením softwaru** , kde můžete nasadit vybranou aplikaci do kolekcí počítačů v hierarchii.<br /><br /> Viz [nasazení aplikací](../../apps/deploy-use/deploy-applications.md).|  
|**Distribuovat obsah**|Otevře **Průvodce distribucí obsahu** , kde můžete kopírovat obsah vybrané aplikace do distribučních bodů v hierarchii.<br /><br /> Viz [Správa obsahu a infrastruktury obsahu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Zobrazit vztahy**|Zobrazí grafický diagram vztahů vybraných aplikací k jiným aplikacím. Vyberte jednu z následujících možností:<br><br><ul><li>**Závislost** – zobrazí aplikace, které jsou závislé na vybrané aplikaci, a aplikace, na kterých vybraná aplikace závisí.</li><li>**Nahrazování** – zobrazí aplikace, které vybraná aplikace nahrazuje, a aplikace, které vybraná aplikace nahrazuje.</li><li>**Globální podmínky** – zobrazí globální podmínky, na které se odkazuje v této aplikaci.</li></ol><br /> Viz [Revize a nahrazování aplikací](../../apps/deploy-use/revise-and-supersede-applications.md) a [vytváření globálních podmínek](../../apps/deploy-use/create-global-conditions.md).|  
|**Kopírovat aplikace**|Kopírování nebo duplikování Configuration Manager aplikací pro vytvoření nového. Tato akce je užitečná k otestování nějakého nebo v případě, že potřebujete vytvořit podobnou aplikaci. Lokalita vytvoří novou aplikaci, která je **připojena k** názvu. Zatímco lokalita kopíruje většinu metadat do nové aplikace, nekopíruje žádná nasazení.|

##  <a name="manage-deployment-types"></a>Spravovat typy nasazení  
 V pracovním prostoru **softwarová knihovna** rozbalte položku **Správa aplikací**, zvolte možnost **aplikace**a pak zvolte aplikaci, která má typ nasazení, který chcete spravovat. V podokně podrobností klikněte na kartu **typy nasazení** , vyberte typ nasazení, který chcete spravovat, a pak vyberte úlohu správy.  

|Úkol|Podrobnosti|  
|----------|-------------|  
|**Zvýšit prioritu**|Zvýší prioritu vybraného typu nasazení. Typy nasazení jsou vyhodnocovány v pořadí priority. Pokud typ nasazení splňuje zadané požadavky, bude spuštěn a následně nebudou vyhodnoceny žádné další typy nasazení v seznamu priorit.|  
|**Snížit prioritu**|Sníží prioritu vybraného typu nasazení.|  
|**Odstranit**|Odstraní vybraný typ nasazení.<br><br>Nelze odstranit typ nasazení, na který se odkazuje typ nasazení v jiné aplikaci.<br>Chcete-li odstranit typ nasazení, je nutné odebrat všechny závislosti na typu nasazení, které jsou v jiných typech nasazení.<br>Kromě toho je nutné odebrat také předchozí revize všech aplikací, které mají typ nasazení, který odkazuje na typ nasazení, který chcete odstranit.|  
|**Aktualizovat obsah**|Aktualizuje obsah vybraného typu nasazení.<br /><br /> Když spustíte tohoto průvodce pro typ nasazení, který má virtuální aplikaci, bude spuštěn **Průvodce aktualizací obsahu** . Tento průvodce umožňuje změnit možnosti publikování a pravidla požadavků pro vybranou virtuální aplikaci. Další informace najdete v tématu věnovaném [vytváření aplikací](../../apps/deploy-use/create-applications.md).<br /><br /> Když aktualizujete obsah typu nasazení, je vytvořena nová revize aplikace. To může mít za následek aktualizaci aplikace v klientských zařízeních.|