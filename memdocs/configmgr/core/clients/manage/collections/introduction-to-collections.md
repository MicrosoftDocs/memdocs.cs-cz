---
title: Úvod do kolekcí
titleSuffix: Configuration Manager
description: Seznámení s použitím kolekcí v Configuration Manager.
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4e43f5a36f2a1bf44959b9645c2fb48a22cc71f1
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126769"
---
# <a name="introduction-to-collections-in-configuration-manager"></a>Seznámení s kolekcemi v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Kolekce usnadňují uspořádání prostředků do spravovatelných jednotek. Můžete vytvořit kolekce, které budou odpovídat potřebám správy klientů, a provádět operace s více prostředky najednou. 

Většina úloh správy spoléhá na nebo vyžaduje použití jedné nebo více kolekcí. I když můžete použít předdefinovanou kolekci všech systémů, použití IT pro úlohy správy není osvědčeným postupem. Vytvořte vlastní kolekce, které budou přesněji identifikovat zařízení nebo uživatele pro úlohu.  

 Předdefinované a vlastní kolekce se zobrazí v uzlech kolekce **uživatelů** a **kolekce zařízení** v pracovním prostoru **prostředky a kompatibilita** v konzole Configuration Manager.  

 Kolekce, které jste zobrazili v poslední době, se zobrazí v uzlu **Uživatelé** a v uzlu **zařízení** v pracovním prostoru **prostředky a kompatibilita** .  

Tady je několik příkladů použití kolekce:  

|Operace|Příklad|  
|---------|-------|  
|Seskupení prostředků|Můžete vytvořit kolekce, které seskupují prostředky na základě hierarchie vaší organizace.<br /><br /> Můžete například vytvořit kolekci všech počítačů v organizační jednotce (OU) služby Active Directory. Další informace o tom, jak vytvořit tento typ kolekce, najdete v tématu [vytváření kolekcí](../../../../core/clients/manage/collections/create-collections.md).<br /><br /> Tuto kolekci můžete použít pro operace, jako je konfigurace nastavení Endpoint Protection, konfigurace nastavení řízení spotřeby zařízení nebo instalace klienta Configuration Manager.|  
|Nasazení aplikací|Můžete vytvořit kolekci všech počítačů, které nemají nainstalované aplikace Microsoft Microsoft 365, a pak ji nasadit do všech počítačů v této kolekci.<br /><br /> K provedení této úlohy můžete využít taky požadavky aplikací. Další informace najdete v tématu [vytváření aplikací pomocí Configuration Manager](../../../../apps/deploy-use/create-applications.md).|  
|[Správa nastavení klienta](../../../../core/clients/deploy/about-client-settings.md)|Přestože se výchozí nastavení klienta v nástroji Configuration Manager vztahuje na všechna zařízení a všechny uživatele, můžete vytvořit vlastní nastavení klienta, která se použijí jenom pro kolekci zařízení nebo uživatelů.<br /><br /> Například pokud chcete, aby bylo vzdálené řízení k dispozici na všech zařízeních kromě několika, nakonfigurujte výchozí nastavení klienta tak, aby povolovalo vzdálené řízení, a potom nakonfigurujte vlastní nastavení klienta, která neumožňují vzdálené řízení, a nasaďte je do kolekce mimořádných klientů. |  
|[Řízení spotřeby](../power/introduction-to-power-management.md)|Pro každou kolekci můžete nakonfigurovat konkrétní nastavení napájení.|  
|[Správa na základě rolí](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|Pomocí kolekcí můžete řídit, které skupiny uživatelů mají přístup k různým funkcím v konzole Configuration Manager.|  
|[Okna údržby](../../../../core/clients/manage/collections/use-maintenance-windows.md)|S časovými intervaly pro správu a údržbu můžete definovat časové období, kdy se můžou na členech kolekce zařízení provádět různé operace Configuration Manager. |  


## <a name="collection-types-in-configuration-manager"></a>Typy kolekcí v nástroji Configuration Manager  
 Configuration Manager má předdefinované kolekce pro běžné operace a můžete také vytvořit vlastní kolekce.   

### <a name="built-in-collections"></a>Předdefinované kolekce  
 Ve výchozím nastavení Configuration Manager obsahuje následující kolekce, které nelze upravit.  

|**Název kolekce**|Popis|  
|-------------------------|-----------------|  
|**Všechny skupiny uživatelů**|Obsahuje skupiny uživatelů, které se zjistí pomocí zjišťování skupin zabezpečení služby Active Directory.|  
|**Všichni uživatelé**|Obsahuje uživatele, kteří se zjistí pomocí zjišťování uživatelů služby Active Directory.|  
|**Všichni uživatelé a skupiny uživatelů**|Obsahuje kolekce Všichni uživatelé a Všechny skupiny uživatelů. Tato kolekce obsahuje největší rozsah prostředků uživatelů a skupin uživatelů.|  
|**Všechny desktopové a serverové klienty**|Obsahuje serverová a desktopová zařízení s nainstalovaným klientem Configuration Manager. Členství se spravuje pomocí zjišťování prezenčního signálu.|  
|**Všechna mobilní zařízení**|Obsahuje mobilní zařízení spravovaná nástrojem Configuration Manager. Členství je omezené na tato mobilní zařízení, která jsou úspěšně přiřazená k lokalitě nebo zjištěná konektorem systému Exchange Server.|  
|**Všechny systémy**|Obsahuje kolekce všechny desktopové a serverové klienty, všechna mobilní zařízení a všechny neznámé počítače a všechna mobilní zařízení zapsaná službou Microsoft Intune. Tato kolekce obsahuje největší rozsah prostředků zařízení.|  
|**Všechny neznámé počítače**|Obsahuje obecné počítačové záznamy pro několik počítačových platforem. Tuto kolekci můžete použít k nasazení operačního systému pomocí pořadí úkolů a spuštění pomocí technologie PXE, spouštěcího média nebo předzpracovaného média.|  

### <a name="custom-collections"></a>Vlastní kolekce  
 Když vytvoříte vlastní kolekci v Configuration Manager, členství v této kolekci je určené jedním nebo více pravidly shromažďování, jak je popsáno v tématu [Vytvoření kolekce](../../../../core/clients/manage/collections/create-collections.md). 

