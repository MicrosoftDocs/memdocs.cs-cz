---
title: Revidování a nahrazování aplikací
titleSuffix: Configuration Manager
description: Naučte se pracovat s Configuration Managermi verzemi aplikací a nahrazovat aplikace.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 30170d70-489f-47f7-bebf-9ed0115db26b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 6afed00b8207edb338b2a6dc62e083a5267fa47e
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343129"
---
# <a name="revise-and-supersede-applications-in-configuration-manager"></a>Revize a nahrazování aplikací v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

V tomto tématu se dozvíte, jak pracovat s Configuration Managermi verzemi aplikací a jak nahrazovat aplikace novou verzí.  

##  <a name="application-revisions"></a> Revize aplikací  
 Když provedete revize aplikace nebo typu nasazení, který je obsažen v aplikaci, Configuration Manager vytvoří novou revizi aplikace. Můžete zobrazit historii revizí každé aplikace. Také můžete zobrazit její vlastnosti, obnovit předchozí revizi aplikace nebo odstranit starší revizi.  

### <a name="to-display-an-application-revision-history"></a>Zobrazení historie revizí aplikace  

1.  V konzole Configuration Manager zvolte možnost aplikace **softwarová knihovna**  >  **Správa aplikací**  >  **Applications**a pak zvolte požadovanou aplikaci.  

3.  Na kartě **Domů** ve skupině **aplikace** kliknutím na možnost **Historie revizí** otevřete dialogové okno **Historie revizí aplikace** .  

### <a name="to-view-an-application-revision"></a>Zobrazení revize aplikace  

1.  V dialogovém okně **Historie revizí aplikace** vyberte revizi aplikace a pak zvolte možnost **Zobrazit**.  

2.  V dialogovém okně **Vlastnosti** zkontrolujte vlastnosti vybrané aplikace.  

    > [!NOTE]  
    >  Zobrazené vlastnosti aplikace jsou pouze ke čtení.  

3.  Zavřete dialogové okno **Vlastnosti** .  

### <a name="to-restore-an-application-revision"></a>Obnovení revize aplikace  

1.  V dialogovém okně **Historie revizí aplikace** vyberte revizi aplikace a pak zvolte **obnovit**.  

2.  V dialogovém okně **Potvrdit obnovení revize** kliknutím na **tlačítko Ano** obnovte vybranou revizi aplikace.  

### <a name="to-delete-an-application-revision"></a>Odstranění revize aplikace  

1.  V dialogovém okně **Historie revizí aplikace** vyberte revizi aplikace a pak zvolte **Odstranit**.  

2.  V dialogovém okně **Odstranit revizi aplikace** vyberte **Ano**.  

> [!IMPORTANT]  
>  Aktuální revizi aplikace můžete odstranit pouze v případě, že je aplikace vyřazena a neobsahuje žádné odkazy.  

##  <a name="application-supersedence"></a> Nahrazování aplikací  
 Správa aplikací v Configuration Manager umožňuje upgradovat nebo nahradit stávající aplikace pomocí vztahu nahrazování. Pokud nahrazujete aplikaci, můžete určit nový typ nasazení, který nahradí typ nasazení nahrazené aplikace, a také rozhodnout, zda má být nahrazena nebo odinstalována nahrazená aplikace, než bude nainstalována nahrazující aplikace. Obecně řečeno, doporučujeme omezit řetězce nahrazení na pět úrovní na maximum.
 
> [!IMPORTANT]  
>  Když je vybrána možnost odinstalování nahrazovaného typu nasazení, typ nasazení nemůže být nahrazen typem nasazení, který byl nasazen na jiný typ kolekce.  Například nelze typ nasazení, který byl nasazen na kolekci zařízení, nahradit typem nasazení, který byl nasazen na kolekci uživatelů, pokud je vybrána možnost odinstalování nahrazovaného typu nasazení.  

### <a name="decide-whether-to-upgrade-or-replace-an-application"></a>Rozhodování, zda chcete aplikaci upgradovat, nebo nahradit  
 V dialogovém okně **Určit vztah nahrazení** v rámci okna vlastností aplikace můžete nastavit, zda chcete aplikaci nahradit, nebo upgradovat. Typ nahrazení je určen zaškrtnutím políčka **Odinstalovat** v tomto dialogovém okně:  

-   Pokud chcete aktualizovat na novější verzi stejné aplikace (se stejným ID aplikace **), neprovádějte kontrolu** **odinstalace**.  

-   Pokud chcete přejít na novou aplikaci (s jiným ID aplikace ID), políčko **Odinstalovat**zaškrtněte. Je nutné odebrat nahrazenou verzi aplikace.  

### <a name="supersede-dependent-applications"></a>Nahradit závislé aplikace  
 V tomto příkladu **hlavní aplikace** označuje aplikaci, kterou nasazujete, která má závislosti.  

 Můžete vytvořit vztah nahrazení, který aktualizuje závislou aplikaci na novou verzi.  

1. Zajistěte, aby nová závislá aplikace a původní závislá aplikace byly ve stejné skupině závislostí hlavní aplikace.  

2. Vytvořte vztah nahrazení, který provede nahrazení původní závislé aplikace novou závislou aplikací.  

   Při nových instalacích hlavní aplikace je nainstalována nová závislá aplikace. Existující instalace hlavní aplikace se aktualizují s použitím nové závislé aplikace.  

   Konečným výsledkem je, že všechna nasazení hlavní aplikace používají novou závislou aplikaci.  

### <a name="further-considerations"></a>Další pravidla  

-   Můžete určit více vztahů nahrazení pro závislé aplikace. Instalována bude nejvyšší závislá aplikace v řetězci nahrazení.  

-   Závislé aplikace musí být nasazeny do zařízení, kde je nainstalována hlavní aplikace, jinak nebude nainstalována závislá aplikace.  

-   Pro nové instalace hlavní aplikace platí, že máte-li více závislostí, pak pořadí závislostí určuje, která verze závislé aplikace bude nainstalována.  

### <a name="to-specify-a-supersedence-relationship"></a>Určení vztahu nahrazení  

1.  V konzole Configuration Manager zvolte možnost **softwarová knihovna**aplikace  >  **Správa aplikací**  >  **Applications**a pak zvolte aplikaci, která nahrazuje jinou aplikaci.  

3.  Na kartě **Domů** ve skupině **vlastnosti** kliknutím na možnost **vlastnosti** otevřete dialogové okno **vlastnosti** názvu aplikace.  

4.  Na kartě **nahrazování** v dialogovém okně *<název \> aplikace* – **vlastnosti** klikněte na tlačítko **Přidat**.  

5.  V dialogovém okně **Určit vztah nahrazení** klikněte na tlačítko **Procházet**.  

6.  V dialogovém okně **Zvolit aplikaci** zvolte aplikaci, kterou chcete nahradit, a pak zvolte **OK**.  

7.  V dialogovém okně **určit vztah nahrazení** vyberte typ nasazení, který nahrazuje typ nasazení nahrazené aplikace.  

    > [!NOTE]  
    >  Ve výchozím nastavení nový typ nasazení neodinstaluje typ nasazení nahrazené aplikace. Tento případ se obvykle používá, když chcete nasadit upgradování na existující aplikaci. Vyberte možnost **Odinstalovat** k odebrání existujícího typu nasazení před nainstalováním nového typu nasazení. Pokud se rozhodnete upgradovat aplikaci, nejdříve zajistěte otestování tohoto upgradování v laboratorním prostředí.  

8.  Kliknutím na **tlačítko OK** zavřete dialogové okno **určit vztah nahrazení** .  

9. Kliknutím na **tlačítko OK** zavřete dialogové okno *<\> název aplikace* **vlastnosti** .  

### <a name="to-display-applications-that-supersede-the-current-application"></a>Zobrazení aplikací, které nahrazují aktuální aplikaci  

1.  V konzole Configuration Manager vyberte možnost **softwarová knihovna**.  

2.  V pracovním prostoru **softwarová knihovna** rozbalte položku **Správa aplikací**, zvolte možnost **aplikace**a pak zvolte požadovanou aplikaci.  

3.  Na kartě **Domů** ve skupině **vlastnosti** kliknutím na možnost **vlastnosti** otevřete dialogové okno *<\> název aplikace* **vlastnosti** .  

4.  Na kartě **odkazy** v dialogovém okně *<aplikace vlastnosti \> název aplikace* vyberte **aplikace, které nahrazují tuto aplikaci** , z rozevíracího seznamu **typ vztahu** . **Properties**  

5.  Zkontrolujte seznam aplikací, které nahrazují vybranou aplikaci, a pak kliknutím na **tlačítko OK** zavřete dialogové okno *<název \> aplikace* **vlastnosti** .  
