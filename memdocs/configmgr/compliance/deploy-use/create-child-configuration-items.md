---
title: Vytváření podřízených položek konfigurace
titleSuffix: Configuration Manager
description: Vytvořte podřízené položky konfigurace v Configuration Manager.
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 319f673200244d4451b957dcb778ce378f9569fa
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240316"
---
# <a name="how-to-create-child-configuration-items-in-configuration-manager"></a>Vytvoření podřízených položek konfigurace v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Podřízené položky konfigurace v Configuration Manager jsou kopie položek konfigurace, které uchovávají vztah k původní položce konfigurace v tom, že dědí původní konfiguraci z nadřazené položky konfigurace.  

Když zobrazíte vlastnosti podřízené položky konfigurace v konzole Configuration Manager, nemůžete upravit zděděné objekty a nastavení pomocí jejich ověřovacích kritérií. Můžete ale přidat a pak upravit další ověřovací kritéria pro podřízenou položku konfigurace a můžete také přidávat podřízené položce konfigurace nové objekty a nastavení.
Příkladem vytváření a úprav podřízené položky konfigurace je upřesnění původní položky konfigurace, aby splňovala vaše obchodní požadavky.  

> [!NOTE]  
>  Podřízené položky konfigurace můžete vytvářet jenom z položek konfigurace typu **Stolní počítače a servery s Windows (vlastní)**.  

## <a name="to-create-a-child-configuration-item"></a>Vytvoření podřízené položky konfigurace  

1.  V konzole Configuration Manager klikněte na **prostředky a**kompatibilita  >  **Nastavení dodržování**předpisů  >  **položky konfigurace**.  

3.  V seznamu **Položky konfigurace** vyberte položku konfigurace, pro kterou chcete vytvořit podřízenou položku konfigurace, a pak na kartě **Domů** ve skupině **Položka konfigurace** klikněte na **Vytvořit podřízenou položku konfigurace**.  

4.  Na stránce **Obecné** v **Průvodci vytvořením podřízené položky konfigurace**můžete vybrat konkrétní revizi nadřazené položky konfigurace, kterou chcete k vytvoření podřízené položky použít. Další kroky v tomto průvodci jsou stejné jako ty, které můžete použít k vytvoření položky standardní konfigurace. Další informace najdete v tématu [postup vytváření vlastních položek konfigurace pro počítače a serverové počítače s Windows](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md).  

5.  Dokončete průvodce. Nová podřízená položka konfigurace se zobrazí v seznamu **Položky konfigurace** .  
