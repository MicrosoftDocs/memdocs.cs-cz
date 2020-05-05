---
title: Odinstalování aplikací
titleSuffix: Configuration Manager
description: Odinstalace aplikace pomocí Configuration Manager
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d9b5152c094ecc1470f748c57f2831cfdd66474
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075842"
---
# <a name="uninstall-applications-with-configuration-manager"></a>Odinstalace aplikací pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*


Chcete-li odinstalovat aplikaci, kterou jste předtím nasadili, proveďte následující akce.

-   Zadejte příkazový řádek pro odinstalaci obsahu typu nasazení na stránce **obsah** v Průvodci vytvořením typu nasazení.  

-   Nasaďte aplikaci s použitím akce nasazení **Odinstalovat**.  

> [!IMPORTANT]  
> Některé aplikace nepodporují odinstalaci.  

 Tento seznam obsahuje další informace o tom, jak funguje odinstalace aplikace:  

-   Když odinstalujete aplikaci Configuration Manager (Configuration Manager), nebudou automaticky odinstalovány žádné závislé aplikace.  

-   Pokud nasadíte aplikaci, která používá akci **odinstalace** pro uživatele, a aplikace byla nainstalována pro všechny uživatele počítače, odinstalace může selhat, pokud účet uživatele nemá oprávnění k odinstalaci aplikace.  

-   Pokud odeberete uživatele nebo zařízení z kolekce, do které je nasazená aplikace, aplikace se ze zařízení automaticky neodebere.  

-   Nasazení prováděné s účelem **Odinstalovat** nekontroluje pravidla požadavků. Je-li aplikace instalována v počítači, kde je nasazení spuštěno, bude odinstalována.  

> [!IMPORTANT]  
> Chcete-li nasadit aplikaci pomocí akce odinstalovat, je nutné nejprve odstranit všechna existující nasazení aplikace, simulovaná nasazení nebo nasazení pořadí úloh, která zahrnují tuto aplikaci. 

 Další informace o tom, jak vytvořit typ nasazení, naleznete v tématu [Create Applications](../../apps/deploy-use/create-applications.md).  

 Další informace o tom, jak nasadit aplikaci, najdete v tématu [nasazení aplikací](../../apps/deploy-use/deploy-applications.md).  

## <a name="uninstall-an-application"></a>Odinstalace aplikace  

1.  Konfigurujte typ nasazení aplikace s příkazovým řádkem pro odinstalaci pomocí některé z následujících metod:  

    -   Na stránce **Obecné** v Průvodci vytvořením nasazení vyberte možnost **automaticky zjišťovat informace o tomto typu nasazení z instalačních souborů**. Jsou-li informace v instalačních souborech k dispozici, průvodce automaticky přidá příkazový řádek pro odinstalaci do vlastností typu nasazení.  

    -   Na stránce **obsah** v Průvodci vytvořením typu nasazení v poli **odinstalační program** zadejte příkazový řádek pro odinstalaci aplikace.  

        > [!NOTE]  
        >  Stránka **obsah** se zobrazí jenom v případě, že jste na stránce **Obecné** v Průvodci vytvořením typu nasazení vybrali možnost **ručně zadat informace o typu nasazení** .  

    -   Na kartě **Programs** ** <programy v dialogovém okně *název typu nasazení*> vlastnosti** zadejte příkazový řádek pro odinstalaci aplikace v poli **odinstalační program** .  

2.  Nasaďte aplikaci a pak na stránce **nastavení nasazení** v Průvodci nasazením softwaru vyberte **odinstalovat** akci nasazení.  

    > [!NOTE]  
    >  Když vyberete akci nasazení **Odinstalovat**, účel nasazení je automaticky nastaven na možnost **Požadováno**.  
