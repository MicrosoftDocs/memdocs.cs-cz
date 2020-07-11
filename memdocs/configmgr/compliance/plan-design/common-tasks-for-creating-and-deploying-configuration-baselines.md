---
title: 'Běžné úlohy pro standardní hodnoty konfigurace '
titleSuffix: Configuration Manager
description: Přečtěte si, jak vytvořit a nasadit Configuration Manager standardní hodnoty konfigurace.
ms.date: 07/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4bb6afeb-d267-4f9b-ade2-26e5400c223b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 40f0fe1adc723587316dcc5f03d710ae4b31b78b
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240690"
---
# <a name="common-tasks-for-creating-and-deploying-configuration-baselines-with-configuration-manager"></a>Běžné úlohy pro vytváření a nasazování standardních hodnot konfigurace pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Toto téma obsahuje běžné scénáře, které vám pomůžou zjistit, jak vytvořit a nasadit Configuration Manager standardní hodnoty konfigurace.  

 Pokud jste již obeznámeni s nastavením dodržování předpisů, můžete najít podrobnou dokumentaci ke všem funkcím, které používáte, v tématech [Vytvoření standardních hodnot konfigurace](../../compliance/deploy-use/create-configuration-baselines.md) a [nasazení standardních hodnot konfigurace](../../compliance/deploy-use/deploy-configuration-baselines.md) .  

 Než začnete, přečtěte si téma [Začínáme s nastavením dodržování předpisů](../../compliance/get-started/get-started-with-compliance-settings.md) a seznamte se se základy nastavení dodržování předpisů a [Naplánujte a nakonfigurujte nastavení dodržování předpisů](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) k implementaci všech nezbytných požadavků.  

## <a name="create-a-configuration-baseline"></a>Vytvoření standardních hodnot konfigurace  
 V tomto příkladu jste vytvořili položku konfigurace jenom pro počítače s Windows 10, na kterých běží klient Configuration Manager.  

 Tato položka konfigurace vynucuje pro těchto 10 počítačů s Windows délku hesla nejméně 6 znaků. Položka konfigurace má název **Windows 10 - vynucení hesla**.  

Pomocí následujícího postupu se dozvíte, jak přidat tuto položku konfigurace do standardních hodnot konfigurace a připravit ji pro nasazení.  

1. V konzole Configuration Manager klikněte na **prostředky a dodržování předpisů**  >  **Nastavení dodržování**předpisů  >  **standardní hodnoty konfigurace**.  

2. Na kartě **Domů** ve skupině **Vytvořit** klikněte na **Vytvořit standardní hodnoty konfigurace**.  

3. V dialogovém okně **Vytvoření standardních hodnot konfigurace** nakonfigurujte následující nastavení:  

   -   **Název** – zadejte **Windows 10 - vynucení hesla** (nebo jiný název, který si vyberete)  

4. Klikněte na **Přidat**  >  **položky konfigurace**.  

5. V dialogovém okně **Přidat položky konfigurace** vyberte položku konfigurace **Windows 10 - vynucení hesla** , kterou jste vytvořili výše, a klikněte na **Přidat**.  

6. Kliknutím na tlačítko OK zavřete dialogové okno **Přidat položky konfigurace** a vraťte se do dialogového okna **vytvořit standardní hodnoty konfigurace** .

7. V dialogovém okně **Vytvoření standardních hodnot konfigurace** klikněte na **OK** .  

   V uzlu **standardní hodnoty konfigurace** konzoly Configuration Manager se teď můžete podívat na standardní hodnoty konfigurace.  

## <a name="deploy-the-configuration-baseline"></a>Nasazení standardních hodnot konfigurace  
 V tomto příkladu nasadíte standardní hodnoty konfigurace, které jste vytvořili v předchozím postupu, do kolekce počítačů.  

1. V konzole Configuration Manager klikněte na **prostředky a dodržování předpisů**  >  **Nastavení dodržování**předpisů  >  **standardní hodnoty konfigurace**.  

2. Ze seznamu standardních hodnot konfigurace vyberte **Windows 10 - vynucení hesla**.  

3. Na kartě **Domů** ve skupině **Nasazení** klikněte na možnost **Nasadit**.  

4. V dialogovém okně **nasazení standardních hodnot konfigurace** nakonfigurujte následující nastavení:  

   -   **Vybrané standardní hodnoty konfigurace** – zkontrolujte, jestli byly do tohoto seznamu automaticky přidané standardní hodnoty konfigurace **Windows 10 - vynucení hesla** .  

   -   **Napravit pravidla nesplňující požadavky** , je-li to podporováno – zaškrtněte toto políčko, aby se zajistilo, že pokud se na cílových zařízeních nevyskytují správná nastavení, budou opravena Configuration Manager.  

   -   **Kolekce** – klikněte na tlačítko **Procházet** a vyberte kolekci počítačů, ve kterých se standardní hodnoty konfigurace vyhodnotí a napravují pro dodržování předpisů. V tomto příkladu byly nasazené standardní hodnoty konfigurace do vestavěné kolekce **Všechny desktopové a serverové klienty** .  

       > [!TIP]  
       >  Nebojte se, pokud vybraná kolekce obsahuje počítače nebo zařízení bez Windows 10. Pokud jste ve vytvořené položce konfigurace nakonfigurovali podporované platformy, vyhodnotí se dodržování předpisů jenom pro počítače s Windows 10.  

   -   V případě potřeby nakonfigurujte plán, podle kterého se standardní hodnoty konfigurace vyhodnotí. Jinak použijte výchozí hodnotu **7 dní**.  

5. Kliknutím na **OK** zavřete dialogové okno **Nasazení standardních hodnot konfigurace** a vytvořte nasazení.  

   Pokud chcete rychle zkontrolovat statistiku shody s tímto nasazením, klikněte v pracovním prostoru **Sledování** na tlačítko **Nasazení**. V dolní části obrazovky uvidíte graf **statistiky dodržování předpisů** .  

## <a name="next-steps"></a>Další kroky 

Podrobnější informace o tom, jak monitorovat standardní hodnoty konfigurace, najdete v tématu [monitorování nastavení dodržování předpisů](../../compliance/deploy-use/monitor-compliance-settings.md).  
