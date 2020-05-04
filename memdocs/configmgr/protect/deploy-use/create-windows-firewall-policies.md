---
title: Zásady brány Windows Firewall pro Endpoint Protection
titleSuffix: Configuration Manager
description: Naučte se vytvářet a nasazovat zásady brány firewall pro Endpoint Protection v nástroji System Center 2012 Configuration Manager.
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6ecdfad1-6305-45a8-ae75-3f33b967cb8f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7c017e750e175e09a67deb4651cf7e8eb98f1bc1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715491"
---
# <a name="create-and-deploy-windows-firewall-policies-for-endpoint-protection-in-configuration-manager"></a>Vytvoření a nasazení zásad brány Windows Firewall pro Endpoint Protection v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Zásady brány firewall pro Endpoint Protection v Configuration Manager umožňují provádět základní úlohy konfigurace a údržby brány Windows Firewall v klientských počítačích ve vaší hierarchii. Zásady brány Windows Firewall můžete použít k provedení těchto úloh:  

-   Určení, jestli je brána Windows Firewall zapnutá nebo vypnutá  

-   Určení, jestli jsou pro klientské počítače povolená příchozí připojení  

-   Určení, jestli se uživatelům oznamuje blokování nového programu bránou Windows Firewall  

1.  V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.  

2.  V pracovním prostoru **prostředky a kompatibilita** rozbalte **Endpoint Protection**a pak klikněte na **zásady brány Windows Firewall**.  

3.  Na kartě **Domů** ve skupině **Vytvořit** klikněte na **Vytvořit zásadu brány Windows Firewall**.  

4.  Na stránce **Obecné****Průvodce vytvořením zásad brány Windows Firewall**zadejte název a volitelný popis pro tuto zásadu brány firewall a pak klikněte na **Další**.  

5.  Na stránce **Nastavení profilu** průvodce nakonfigurujte pro jednotlivé profily sítě následující nastavení:  

    > [!NOTE]  
    >  Další informace o profilech sítě najdete v dokumentaci k Windows.  

    -   **Povolit bránu Windows Firewall**  

        > [!NOTE]  
        >  Pokud není **Povolit bránu Windows Firewall** povolené, ostatní nastavení na této stránce průvodce nejsou k dispozici.  

    -   **Blokování všech příchozích připojení, včetně připojení uvedených na seznamu povolených programů**  

    -   **Oznámit uživatelům blokování nového programu bránou Windows Firewall**  

6.  Na stránce **Souhrn** v průvodci zkontrolujte akce, které budou provedeny a pak dokončete průvodce.  

7.  Zkontrolujte, jestli se nové zásady brány Windows Firewall zobrazily v seznamu **Zásady brány Windows Firewall** .  

##  <a name="to-deploy-a-windows-firewall-policy"></a><a name="BKMK_Assign"></a> Nasazení zásady brány Windows Firewall  

1.  V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.  

2.  V pracovním prostoru **prostředky a kompatibilita** rozbalte **Endpoint Protection**a pak klikněte na **zásady brány Windows Firewall**.  

3.  V seznamu **Zásady brány Windows Firewall** vyberte zásadu brány Windows Firewall, kterou chcete nasadit.  

4.  Na kartě **Domů** ve skupině **Nasazení** klikněte na možnost **Nasadit**.  

5.  V dialogovém okně **Nasadit zásadu brány Windows Firewall** určete kolekci, do které chcete přiřadit tuto zásadu brány Windows Firewall, a určete plán přiřazení. Zásada brány Windows Firewall se vyhodnotí z hlediska dodržování předpisů pomocí tohoto plánu a nastavení brány Windows Firewall na klientech, aby došlo k překonfigurování a shodě s touto zásadou brány Windows Firewall.  

6.  Kliknutím na **OK** zavřete dialogové okno **Nasadit zásadu brány Windows Firewall** a nasaďte zásadu brány Windows Firewall.  

    > [!IMPORTANT]  
    >  Když nasazujete zásadu brány Windows Firewall do kolekce, tato zásada se použije na počítače v náhodném pořadí během období 2 hodin, aby nedošlo k zaplavení sítě.
