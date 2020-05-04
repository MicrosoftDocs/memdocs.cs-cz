---
title: Vytváření virtuálních prostředí App-V
titleSuffix: Configuration Manager
description: Vytvářejte virtuální prostředí pomocí Microsoft Application Virtualization, aby aplikace mohly vzájemně sdílet data.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2280218d3d237f91f0db3150dbc2031bad3e1816
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710416"
---
# <a name="create-app-v-virtual-environments-in-configuration-manager"></a>Vytváření virtuálních prostředí App-V v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Ve virtuálním prostředí Microsoft Application Virtualization (App-V) v Configuration Manager můžou nasazené virtuální aplikace sdílet stejný systém souborů a registr na klientských počítačích s Windows. Na rozdíl od standardních virtuálních aplikací mohou tyto aplikace sdílet data mezi sebou. Virtuální prostředí se vytváří nebo upravují na klientských počítačích při instalaci aplikace nebo při vyhodnocování nainstalovaných aplikací klienty. Aplikace můžete uspořádat tak, aby v situaci, kdy se více aplikací pokusí změnit hodnotu v systému souborů nebo registru, měla prioritu aplikace s nejvyšším pořadím.  

> [!IMPORTANT]  
>  Nespoléhá na to, že virtuální prostředí App-V zajistí ochranu zabezpečení, jako je třeba malware.  

 K vytvoření virtuálního prostředí App-V v Configuration Manager použijte následující postup.  

## <a name="create-an-app-v-virtual-environment"></a>Vytvoření virtuálního prostředí App-V  

1.  V konzole Configuration Manager vyberte možnost **softwarová knihovna** > **Správa** > aplikací**App-V**.  

3.  Na kartě **Domů** ve skupině **vytvořit** klikněte na možnost **vytvořit virtuální prostředí**.  

4.  V dialogovém okně **vytvořit virtuální prostředí** zadejte následující informace:  

    -   **Název**.  Zadejte jedinečný název pro virtuální prostředí (maximálně 128 znaků).  

    -   **Popis**. Volitelné Zadejte popis virtuálního prostředí.  

5.  Chcete-li přidat nový typ nasazení do virtuálního prostředí, vyberte možnost **Přidat**. Musíte přidat alespoň jeden typ nasazení.  

6.  V dialogovém okně **Přidat aplikace** zadejte **název skupiny** (maximálně 128 znaků). Tento název použijete, chcete-li se podívat na skupinu aplikací, které přidáte do virtuálního prostředí.  

7.  Zvolte **Přidat**, vyberte aplikace sady App-V 5 a typy nasazení, které chcete přidat do skupiny, a pak zvolte **OK**.  

8.  V dialogovém okně **Přidat aplikace** můžete vybrat **zvýšit pořadí** nebo **snížit pořadí** , abyste nastavili aplikaci, která má prioritu, pokud se více aplikací pokusí změnit nastavení systému souborů nebo registru ve stejném virtuálním prostředí.  

9. Chcete-li se vrátit do dialogového okna **vytvořit virtuální prostředí** , klikněte na **tlačítko OK**.  

10. Až skončíte s přidáváním skupin, klikněte na **OK** a vytvořte virtuální prostředí. Nové virtuální prostředí se zobrazí v uzlu **virtuální prostředí App-v** konzoly Configuration Manager. Stav virtuálních prostředí můžete monitorovat pomocí sestavy stav virtuálního prostředí App-V.  

    > [!NOTE]  
    >  Virtuální prostředí se přidá nebo upraví na klientských počítačích při instalaci aplikace nebo vyhodnocování nainstalovaných aplikací klientem.  
