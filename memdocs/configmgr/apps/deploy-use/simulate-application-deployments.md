---
title: Simulace nasazení aplikace
titleSuffix: Configuration Manager
description: Vyhodnotit metodu detekce, požadavky a závislosti pro typ nasazení bez instalace aplikace.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bed491b4800dd6ae8b53a837618abf3d8a5a597d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710591"
---
# <a name="simulate-application-deployments-with-configuration-manager"></a>Simulace nasazení aplikací pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Simulovaná nasazení můžete použít k otestování nasazení aplikace bez instalování nebo odinstalování aplikace. Simulované nasazení vyhodnocuje metodu detekce, požadavky a závislosti pro typ nasazení. Nahlásí výsledky v uzlu **nasazení** pracovního prostoru **monitorování** . Pomocí postupu v tomto tématu můžete simulovat nasazení aplikace v Configuration Manager.  

> [!NOTE]  
> Simulovaná nasazení nelze použít pro kolekce mobilních zařízení.  
>   
> Nelze nasadit aplikaci s účelem nasazení **Odinstalovat** , pokud je simulované nasazení stejné aplikace aktivní.  

## <a name="configure-a-simulated-application-deployment"></a>Konfigurace simulovaného nasazení aplikace

1.  V konzole Configuration Manager vyberte jednu z následujících možností:  
    -   Kolekce uživatelů.  
    -   Kolekce zařízení.  
    -   Aplikace Configuration Manager.  

2.  Na kartě **Domů** ve skupině **nasazení** vyberte **simulovat nasazení**.  

3.  V průvodci simulací nasazení aplikace nastavte následující podrobnosti pro simulované nasazení:  

    -   **Aplikace**. Zvolte **Procházet**a pak vyberte aplikaci, pro kterou chcete vytvořit simulované nasazení.  

    -   **Kolekce**. Zvolte **Procházet**a pak vyberte kolekci, kterou chcete použít pro simulované nasazení.  

    -   **Akce**. V rozevíracím seznamu vyberte, zda chcete simulovat instalaci nebo odinstalaci vybrané aplikace.  

    -   **Nasadit automaticky s přihlášením uživatele nebo bez něj**. Pokud je tato možnost zaškrtnutá, klienti vyhodnotí simulované nasazení bez ohledu na to, jestli jsou klienti přihlášení nebo ne.  

4.  Klikněte na **Další**, zkontrolujte informace na stránce **Souhrn** a pak dokončete průvodce a vytvořte simulované nasazení aplikace.  

5.  Simulované aplikace se zobrazí v uzlu **nasazení** v pracovním prostoru **monitorování** s účelem **simulovat**. Další informace o monitorování nasazení aplikací najdete v tématu [monitorování aplikací z konzoly Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md).  
