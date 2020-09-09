---
title: Údržba skupiny serverů
titleSuffix: Configuration Manager
description: Skupiny serverů byly nahrazeny skupinami Orchestration.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 304a83ea-0f72-437d-9688-2e6e0c7526dd
ms.openlocfilehash: a5475d2a33ebcf7fb2e1500a8dc6573180b9a70c
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608399"
---
# <a name="service-a-server-group"></a>Údržba skupiny serverů

*Platí pro: Configuration Manager (Current Branch)*

>[!IMPORTANT]
> - Počínaje verzí 2002 Configuration Manager skupiny serverů nahradily skupinami Orchestration. Další informace najdete v tématu [skupiny Orchestration](orchestration-groups.md).
> - Předběžné verze funkcí jsou funkce, které jsou v Current Branch pro prvotní testování v produkčním prostředí. Tyto funkce jsou plně podporovány, ale stále jsou aktivním vývojem a mohou obdržet změny, dokud nebudou přesunuty mimo kategorii před prodejem. Tuto funkci musíte zapnout, aby byla dostupná. Další informace najdete v tématu [Použití předběžných verzí funkcí z aktualizací](../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

Configuration Manager počínaje verzí 1606 můžete nakonfigurovat nastavení skupiny serverů pro kolekci, aby bylo možné definovat počet, jaké procento a v jakém pořadí počítače v kolekci budou instalovat aktualizace softwaru. Pro spouštění vlastních akcí můžete také nakonfigurovat skripty PowerShellu před nasazením a po nasazení.

Když nasadíte aktualizace softwaru do kolekce, která má nakonfigurované nastavení skupiny serverů, Configuration Manager určuje, kolik počítačů v kolekci může instalovat aktualizace softwaru v určitou dobu a že je k dispozici stejný počet zámků nasazení. Pouze počítače, které obdrží zámek nasazení, spustí instalaci aktualizace softwaru. Když je k dispozici zámek nasazení, počítač získá zámek nasazení, nainstaluje aktualizace softwaru a po úspěšném dokončení instalace aktualizací softwaru uvolní zámek nasazení. Zámek nasazení pak bude k dispozici pro ostatní počítače. Pokud počítač nemůže uvolnit zámek nasazení, můžete pro kolekci ručně uvolnit všechna blokování nasazení skupiny serverů.

>[!IMPORTANT]
>Všechny počítače v kolekci musí být přiřazeny ke stejné lokalitě.

#### <a name="to-create-a-collection-for-a-server-group"></a>Vytvoření kolekce pro skupinu serverů  
Nastavení skupiny serverů je konfigurováno ve vlastnostech pro kolekci zařízení. Aby bylo možné provést údržbu skupiny serverů, musí být všichni členové kolekce přiřazeni ke stejné lokalitě. Pomocí následujících kroků vytvořte kolekci a nakonfigurujte nastavení skupiny serverů:
1.  [Vytvořte kolekci zařízení](../../core/clients/manage/collections/create-collections.md) , která obsahuje počítače ve skupině serverů.  

2.  V pracovním prostoru **prostředky a kompatibilita** klikněte na **kolekce zařízení**, klikněte pravým tlačítkem na kolekci, která obsahuje počítače ve skupině serverů, a pak klikněte na **vlastnosti**.  

3.  Na kartě **Obecné** vyberte **všechna zařízení jsou součástí stejné skupiny serverů**a pak klikněte na **Nastavení**.  

4.  Na stránce **Nastavení skupiny serverů** zadejte jedno z následujících nastavení:  

    -   **Povolí aktualizaci procenta počítačů současně**: Určuje, že v jednom okamžiku se aktualizují jenom určité procento klientů. Pokud má například kolekce 10 klientů a kolekce je nakonfigurována tak, aby aktualizovala více než 30% klientů současně, nainstaluje aktualizace softwaru v jednom okamžiku pouze 3 klienty.  

    -   **Umožnění aktualizace několika počítačů současně**: Určuje, že v jednom okamžiku se aktualizuje jenom určitý počet klientů.  

    -   **Zadejte sekvenci údržby**: Určuje, že se klienti v kolekci budou aktualizovat po jednom v sekvenci, kterou nakonfigurujete. Po dokončení instalace aktualizací softwaru bude klient instalovat aktualizace softwaru pouze poté, co je klient, který je před ním v seznamu.  

5.  Určete, jestli se má použít skript před nasazením (vyprazdňování uzlu) nebo po nasazení (obnovení uzlu).  

    > [!WARNING]
    > Vlastní skripty nejsou podepsané společností Microsoft. Je vaše zodpovědnost za udržování integrity těchto skriptů.

    > [!TIP]  
    > Následují příklady, které můžete použít v části testování pro skripty před nasazením a po nasazení, které zapisují aktuální čas do textového souboru:  
    >   
    >  **Před nasazením**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\start.txt`  
    >   
    >  **Po nasazení**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\end.txt`  

## <a name="deploy-software-updates-to-the-server-group-and-monitor-status"></a>Nasazení aktualizací softwaru do skupiny serverů a stavu monitorování  
Aktualizace softwaru nasadíte do kolekce skupin serverů pomocí typického procesu nasazení. Po nasazení aktualizací softwaru můžete monitorovat nasazení aktualizace softwaru v konzole Configuration Manager.
1.  [Nasaďte aktualizace softwaru](manually-deploy-software-updates.md) do kolekce skupin serverů.   

2.  [Monitorujte nasazení aktualizace softwaru](monitor-software-updates.md). Kromě standardních zobrazení monitorování pro nasazení aktualizací softwaru se stav **čekání na uzamčení** zobrazí, když klient čeká na instalaci aktualizací softwaru. Další informace najdete v souboru UpdatesDeployment. log.


## <a name="clear-the-deployment-locks-for-computers-in-a-server-group"></a>Vymazat zámky nasazení pro počítače ve skupině serverů  
Když se počítači nepovede uvolnit zámek nasazení, můžete pro kolekci ručně uvolnit všechny zámky nasazení skupiny serverů. Vymažte zámky pouze v případě, že nasazení je zablokováno aktualizací počítačů v kolekci a jsou počítače, které stále nedodržují předpisy.  
1.  V pracovním prostoru **prostředky a kompatibilita** klikněte na **kolekce zařízení**a kliknutím na kolekci vymažte zámky nasazení.  

2.  Na kartě **Domů** ve skupině **nasazení** klikněte na **Vymazat zámky nasazení skupiny serverů**. Pokud se klientům nepodařilo nainstalovat aktualizace softwaru a zabráníte ostatním klientům v instalaci aktualizací softwaru, je možné zámky nasazení ručně vymazat.  
