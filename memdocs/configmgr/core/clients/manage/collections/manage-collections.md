---
title: Spravovat kolekce
titleSuffix: Configuration Manager
description: Proveďte běžné úlohy správy kolekcí v Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 063ce963e805651ffd795e830d2b21dfed6fc043
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693127"
---
# <a name="how-to-manage-collections-in-configuration-manager"></a>Správa kolekcí v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Informace v tomto článku s přehledem vám pomůžou při provádění úloh správy pro kolekce v Configuration Manager.  

> [!NOTE]  
>  Informace o tom, jak vytvořit kolekce Configuration Manager, najdete v tématu [vytváření kolekcí](create-collections.md).



## <a name="how-to-manage-device-collections"></a><a name="bkmk_device"></a> Správa kolekcí zařízení  

V pracovním prostoru **Prostředky a kompatibilita** vyberte **Kolekce zařízení**, vyberte spravovanou kolekci a pak vyberte úlohu správy.  


#### <a name="show-members"></a>Zobrazit členy
Zobrazí všechny prostředky, které jsou členy vybrané kolekce v dočasnému uzlu pod uzlem **Zařízení** .


#### <a name="add-selected-items"></a>Přidat vybrané položky
Poskytuje následující možnosti: 

- **Přidat vybrané položky do existující kolekce zařízení**: otevře dialogové okno **Vybrat kolekci** . Vyberte kolekci, do které chcete přidat členy vybrané kolekce. Vybraná kolekce je zahrnutá v této kolekci pomocí pravidla členství **Zahrnout kolekce** .  

- **Přidat vybrané položky do nové kolekce zařízení**: otevře **Průvodce vytvořením kolekce zařízení** , kde můžete vytvořit novou kolekci. Vybraná kolekce je zahrnutá v této kolekci pomocí pravidla členství **Zahrnout kolekce** .  


Další informace najdete v tématu [vytváření kolekcí](create-collections.md).


#### <a name="install-client"></a>Instalovat klienta
Otevře **Průvodce instalací klienta**. Tento průvodce používá nabízenou instalaci klienta k instalaci klienta Configuration Manager na všech počítačích ve vybrané kolekci. Další informace najdete v tématu [klientská nabízená instalace](../../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).


#### <a name="run-script"></a>Spustit skript
Otevře průvodce **spuštěním skriptu** pro spuštění skriptu PowerShellu na všech klientech v kolekci. Další informace najdete v tématu [vytváření a spouštění skriptů PowerShellu](../../../../apps/deploy-use/create-deploy-scripts.md).


#### <a name="manage-affinity-requests"></a>Správa požadavků na spřažení
Otevře dialogové okno **Spravovat požadavky na spřažení uživatelských zařízení** . Schválí nebo odmítne nevyřízené žádosti o vytvoření spřažení uživatelských zařízení pro zařízení ve vybrané kolekci. Další informace najdete v tématu [propojení uživatelů a zařízení pomocí spřažení zařízení a uživatele](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) .


#### <a name="clear-required-pxe-deployments"></a>Vymazat požadované nasazení PXE
Vymaže všechna požadovaná nasazení spuštění PXE ze všech členů vybrané kolekce. Další informace najdete v tématu [použití technologie PXE k nasazení Windows přes síť](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).


#### <a name="update-membership"></a>Aktualizovat členství
Vyhodnotí členství pro vybranou kolekci. Pro kolekce s mnoha členy může dokončení této aktualizace chvíli trvat. Po dokončení aktualizace zobrazíte nové členy kolekce pomocí akce **Aktualizovat** .


#### <a name="add-resources"></a>Přidat prostředky
Otevře dialogové okno **Přidat prostředky do kolekce** . Vyhledejte nové prostředky, které chcete přidat do vybrané kolekce. Ikona vybrané kolekce zobrazuje symbol přesýpací hodiny, zatímco probíhá aktualizace.


#### <a name="client-notification"></a>Klientské oznámení
Další informace najdete v tématu [oznámení klienta](../client-notification.md).


#### <a name="endpoint-protection"></a>Funkce Endpoint Protection
Další informace najdete v tématu [oznámení klienta](../client-notification.md).


#### <a name="export"></a>Export
Otevře **Průvodce exportem kolekce** , který vám pomůže exportovat tuto kolekci do souboru formát MOF (MANAGED Object Format) (MOF). Tento soubor je pak možné archivovat nebo importovat v jiné Configuration Manager lokalitě. Při exportu kolekce se neexportují odkazované kolekce. Vybraná kolekce odkazuje na odkazovanou kolekci pomocí pravidla **include** nebo **Exclude** .


#### <a name="copy"></a>Kopírovat
Vytvoří kopii vybrané kolekce. Nová kolekce použije vybranou kolekci jako limitující kolekci.


#### <a name="refresh"></a>Aktualizovat
Aktualizujte zobrazení.


#### <a name="delete"></a>Odstranit
Odstraní vybranou kolekci. Můžete také odstranit všechny prostředky v kolekci z databáze lokality. 

Kolekce, které jsou součástí Configuration Manager, nemůžete odstranit. Seznam předdefinovaných kolekcí najdete v tématu [Úvod do kolekcí](introduction-to-collections.md#built-in-collections).


#### <a name="simulate-deployment"></a>Simulovat nasazení
Otevře **Průvodce simulací nasazení aplikace**. Tento průvodce vám umožní otestovat výsledky nasazení aplikace bez instalace nebo odinstalace aplikace. Další informace najdete v tématu [postup simulace nasazení aplikace](../../../../apps/deploy-use/simulate-application-deployments.md).


#### <a name="deploy"></a>Nasazení
Zobrazí následující možnosti:  

- **Aplikace**: otevře **Průvodce nasazením softwaru**. Vyberte a nakonfigurujte nasazení aplikace pro vybranou kolekci. Další informace najdete v tématu [nasazení aplikací](../../../../apps/deploy-use/deploy-applications.md).  

- **Program**: otevře **Průvodce nasazením softwaru**. Vyberte a nakonfigurujte nasazení balíčku a programu pro vybranou kolekci. Další informace najdete v tématu [balíčky a programy](../../../../apps/deploy-use/packages-and-programs.md).  

- **Standardní hodnoty konfigurace**: otevře dialogové okno **nasadit standardní hodnoty konfigurace** . Nakonfigurujte nasazení jedné nebo více směrných plánů konfigurace na vybranou kolekci. Další informace najdete v tématu [postup nasazení standardních hodnot konfigurace](../../../../compliance/deploy-use/deploy-configuration-baselines.md).  

- **Pořadí úloh**: otevře se **Průvodce nasazením softwaru**. Vyberte a nakonfigurujte nasazení pořadí úkolů pro vybranou kolekci. Další informace najdete v tématu [Správa pořadí úkolů pro automatizaci úloh](../../../../osd/deploy-use/deploy-a-task-sequence.md).  

- **Aktualizace softwaru**: otevře **Průvodce nasazením aktualizací softwaru**. Nakonfiguruje nasazení aktualizací softwaru pro prostředky ve vybrané kolekci. Další informace najdete v tématu [Správa aktualizací softwaru](../../../../sum/understand/software-updates-introduction.md).  


#### <a name="clear-server-group-deployment-locks"></a>Vymazat zámky při nasazení skupiny serverů
Pro kolekci ručně uvolněte všechna blokování nasazení skupiny serverů. Další informace najdete v tématu [služba skupiny serverů](../../../../sum/deploy-use/service-a-server-group.md).


#### <a name="move"></a>Přesunout
Přesuňte vybranou kolekci do jiné složky v uzlu **kolekce zařízení** . 


#### <a name="properties"></a>Vlastnosti
Další informace najdete v tématu [vlastnosti kolekce](#BKMK_CollProp).  


## <a name="how-to-manage-user-collections"></a><a name="bkmk_user"></a> Správa kolekcí uživatelů  

V pracovním prostoru **Prostředky a kompatibilita** vyberte **Kolekce uživatelů**, vyberte spravovanou kolekci a pak vyberte úlohu správy.  

> [!Note]  
> V kolekcích uživatelů jsou k dispozici následující akce, ale chování jsou stejná jako u kolekcí zařízení. Kromě nich platí pro kolekce uživatelů a uživatele v rámci. Další informace najdete v odpovídající akci v části [Správa kolekcí zařízení](#bkmk_device).  

- **Zobrazit členy**  
- **Přidat vybrané položky**  
    - **Přidat vybrané položky do existující kolekce uživatelů**  
    - **Přidat vybrané položky do kolekce New User**  
- **Správa požadavků na spřažení**  
- **Aktualizovat členství**  
- **Přidat prostředky**  
- **Export**  
- **Kopírovat**  
- **Aktualizovat**  
- **Odstranit**  
- **Simulovat nasazení**  
- **Nasazení**  
    - **Aplikace**  
    - **Program**  
    - **Standardní hodnoty konfigurace**
- **Přesunout**  
- **Vlastnosti**


##  <a name="collection-properties"></a><a name="BKMK_CollProp"></a> Vlastnosti kolekce  

Když otevřete dialogové okno **vlastnosti** pro kolekci, zobrazte a nakonfigurujte následující možnosti:  

#### <a name="general"></a>Obecné
Zobrazí a nakonfiguruje Obecné informace o vybrané kolekci včetně názvu kolekce a omezení kolekce.

#### <a name="membership-rules"></a>Pravidla členství
Nakonfigurujte pravidla členství definující členství v této kolekci. Další informace najdete v tématu [vytváření kolekcí](create-collections.md).  

#### <a name="power-management"></a>Řízení spotřeby
Nakonfigurujte plány řízení spotřeby, které jste přiřadili počítačům ve vybrané kolekci. Další informace najdete v tématu [Úvod do řízení spotřeby](../power/introduction-to-power-management.md).  

#### <a name="deployments"></a>Nasazení
Zobrazí veškerý software, který jste nasadili na členy vybrané kolekce.  

#### <a name="maintenance-windows"></a>Časové intervaly pro správu a údržbu
Zobrazit a nakonfigurovat časové intervaly pro správu a údržbu, které jsou aplikovány na členy vybrané kolekce. Další informace najdete v tématu [použití časových období údržby](use-maintenance-windows.md).

#### <a name="collection-variables"></a>Proměnné kolekce
Nakonfigurujte proměnné, které se vztahují na tuto kolekci a můžou je používat v pořadí úkolů. Další informace najdete v tématu [nastavení proměnných pořadí úkolů](../../../../osd/understand/using-task-sequence-variables.md#bkmk_set).  

#### <a name="distribution-point-groups"></a>Skupiny distribučních bodů
Přidružte jednu nebo více skupin distribučních bodů ke členům vybrané kolekce. Další informace najdete v tématu [Správa obsahu a infrastruktury obsahu](../../../servers/deploy/configure/manage-content-and-content-infrastructure.md).

#### <a name="aad-group-sync"></a>Synchronizace skupiny AAD
Synchronizuje výsledky členství kolekce do skupin Azure Active Directory. Tato synchronizace je [předběžnou verzí funkce](../../../servers/manage/pre-release-features.md) od verze 1906. Další informace najdete v tématu [Vytvoření kolekcí](create-collections.md#bkmk_aadcollsync).

#### <a name="security"></a>Zabezpečení
Zobrazí uživatele s právy pro správu, kteří mají oprávnění pro vybranou kolekci z přidružených rolí a oborů zabezpečení. Další informace najdete v tématu [základy správy na základě rolí](../../../understand/fundamentals-of-role-based-administration.md).  

#### <a name="alerts"></a>Výstrahy 
Nakonfigurujte, kdy se mají generovat výstrahy pro stav klienta a Endpoint Protection. Další informace najdete v tématech [Postup konfigurace stavu klienta](../../deploy/configure-client-status.md) a [Postup monitorování Endpoint Protection](../../../../protect/deploy-use/monitor-endpoint-protection.md).  
## <a name="using-powershell"></a><a name="bkmk_powershell"></a> Použití PowerShellu

PowerShell se dá použít ke správě kolekcí.  Další informace naleznete v tématu:

* [Get-CMCollection](/powershell/module/configurationmanager/get-cmcollection)
* [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection)
* [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection)
* [Kopírování – CMCollection](/powershell/module/configurationmanager/copy-cmcollection)
* [Remove-CMCollection](/powershell/module/configurationmanager/remove-cmcollection)
* [Import – CMCollection](/powershell/module/configurationmanager/import-cmcollection)
* [Export – CMCollection](/powershell/module/configurationmanager/export-cmcollection)
* [Get-CMCollectionMember](/powershell/module/configurationmanager/get-cmcollectionmember)
* [Get-CMCollectionSetting](/powershell/module/configurationmanager/get-cmcollectionsetting)
* [Invoke – CMCollectionUpdate](/powershell/module/configurationmanager/invoke-cmcollectionupdate)
* [Add-CMCollectionMembershipRule](/powershell/module/configurationmanager/add-cmcollectionmembershiprule)
* [Set-CMCollectionPowerManagement](/powershell/module/configurationmanager/set-cmcollectionpowermanagement)
* [Get-CMCollectionMembershipRule](/powershell/module/configurationmanager/get-cmcollectionmembershiprule)
* [Remove-CMCollectionMembershipRule](/powershell/module/configurationmanager/remove-cmcollectionmembershiprule)
* [Get-CMCollectionDirectMembershipRule](/powershell/module/configurationmanager/get-cmcollectiondirectmembershiprule)
* [Get-CMCollectionQueryMembershipRule](/powershell/module/configurationmanager/get-cmcollectionquerymembershiprule)
* [Get-CMCollectionIncludeMembershipRule](/powershell/module/configurationmanager/get-cmcollectionincludemembershiprule)
* [Add-CMCollectionToAdministrativeUser](/powershell/module/configurationmanager/add-cmcollectiontoadministrativeuser)
* [Remove-CMCollectionQueryMembershipRule](/powershell/module/configurationmanager/remove-cmcollectionquerymembershiprule)
* [Remove-CMCollectionDirectMembershipRule](/powershell/module/configurationmanager/remove-cmcollectiondirectmembershiprule)
* [Get-CMCollectionExcludeMembershipRule](/powershell/module/configurationmanager/get-cmcollectionexcludemembershiprule)
* [Add-CMCollectionToDistributionPointGroup](/powershell/module/configurationmanager/add-cmcollectiontodistributionpointgroup)
* [Remove-CMCollectionIncludeMembershipRule](/powershell/module/configurationmanager/remove-cmcollectionincludemembershiprule)
* [Remove-CMCollectionExcludeMembershipRule](/powershell/module/configurationmanager/remove-cmcollectionexcludemembershiprule)
* [Remove-CMCollectionFromAdministrativeUser](/powershell/module/configurationmanager/remove-cmcollectionfromadministrativeuser)