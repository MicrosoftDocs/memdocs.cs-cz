---
title: Konfigurace inventáře softwaru
titleSuffix: Configuration Manager
description: Nakonfigurujte inventář softwaru a vylučte složky z inventáře softwaru v Configuration Manager.
ms.date: 01/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9663f71118836513d95ec914d0f70b09cda9954f
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693059"
---
# <a name="how-to-configure-software-inventory-in-configuration-manager"></a>Postup konfigurace inventáře softwaru v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento postup nakonfiguruje výchozí nastavení klienta pro inventář softwaru a použije se pro všechny počítače ve vaší hierarchii. Pokud chcete tato nastavení použít jenom pro některé počítače, vytvořte vlastní nastavení klienta zařízení a přiřaďte ho ke kolekci. Další informace o tom, jak vytvořit vlastní nastavení zařízení, najdete v tématu [Postup konfigurace nastavení klienta](../../../../core/clients/deploy/configure-client-settings.md).   

## <a name="to-configure-software-inventory"></a>Konfigurace inventáře softwaru  

1. V konzole Configuration Manager vyberte možnost **Správa**  >  **nastavení klienta****výchozí nastavení klienta**.    

2. Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  

3. V dialogovém okně **výchozí nastavení** vyberte **inventář softwaru**.  

4. V seznamu **Nastavení zařízení** nakonfigurujte následující hodnoty:  

   -   **Povolit inventář softwaru na klientských počítačích** – v rozevíracím seznamu vyberte **true**.  

   -   **Plánování inventáře softwaru a shromažďování souborů** – konfiguruje interval, ve kterém Klienti shromažďují inventář softwaru a soubory.   

5. Nakonfigurujte nastavení klienta, která požadujete. Část [inventáře softwaru](../../../../core/clients/deploy/about-client-settings.md#software-inventory) v článku [o nastavení klienta](../../../../core/clients/deploy/about-client-settings.md) obsahuje seznam nastavení klienta.  

   Při příštím stažení zásad klienta se klientské počítače nakonfigurují tímto nastavením. Pokud chcete iniciovat načtení zásad pro jednoho klienta, přečtěte si téma [Správa klientů](../../../../core/clients/manage/manage-clients.md).  

   > [!TIP]
   >   Kód chyby 80041006 v inventoryprovider. log znamená, že zprostředkovatel rozhraní WMI nemá dostatek paměti. To znamená, že bylo dosaženo limitu kvóty paměti pro poskytovatele a poskytovatel inventáře nemůže pokračovat.
   > V takovém případě Agent pro inventarizace vytvoří sestavu s 0 položkami, takže nebudou hlášeny žádné skladové položky. <br/>
   > Možnou příčinou této chyby je omezit rozsah shromažďování inventáře softwaru. V případě, že dojde k chybě po omezení oboru inventáře, může řešení zvýšit vlastnost [MemoryPerHost](https://techcommunity.microsoft.com/t5/ask-the-performance-team/memory-and-handle-quotas-in-the-wmi-provider-service/ba-p/373319) definovanou ve třídě [_ProviderHostQuotaConfiguration](/windows/win32/wmisdk/--providerhostquotaconfiguration) .

<!--SMS.480648 include WMI Out of memory tip -->


## <a name="to-exclude-folders-from-software-inventory"></a>Vyloučení složek z inventáře softwaru  

1.  Pomocí aplikace Notepad.exe vytvořte prázdný soubor s názvem **Skpswi.dat**.  

2.  Klikněte pravým tlačítkem na soubor **soubor Skpswi. dat** a klikněte na **vlastnosti**. Ve vlastnostech souboru pro soubor Skpswi.dat vyberte atribut **Skrytý** .  

3.  Umístěte soubor **Skpswi.dat** do kořenové složky pevného disku nebo struktury složek, které chcete vyloučit z inventáře softwaru.  

> [!NOTE]  
>  Inventáře softwaru nebude znovu inventarizovat jednotku klienta, dokud se tento soubor neodstraní z jednotky klientského počítače.