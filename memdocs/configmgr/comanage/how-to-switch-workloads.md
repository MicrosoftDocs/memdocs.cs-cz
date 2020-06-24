---
title: Přepínání úloh spolusprávy
titleSuffix: Configuration Manager
description: Naučte se, jak přepínat úlohy aktuálně spravované pomocí Configuration Manager Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-comanage
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/06/2019
ms.topic: how-to
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: 88c8b34437ba52e700ef97885aafed40734a0f32
ms.sourcegitcommit: 7b2f7918d517005850031f30e705e5a512959c3d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/15/2020
ms.locfileid: "84776952"
---
# <a name="how-to-switch-configuration-manager-workloads-to-intune"></a>Postup přepnutí úloh Configuration Manager do Intune

Jednou z výhod spolusprávy je přepínání úloh z Configuration Manager na Microsoft Intune. Když má zařízení s Windows 10 klienta Configuration Manager a je zaregistrované v Intune, získáte výhody obou služeb. Vy budete řídit, které úlohy (pokud existují), přepnete autoritu z Configuration Manager na Intune. Configuration Manager nadále spravuje všechny ostatní úlohy, včetně úloh, které nepřepnete do Intune, a všech ostatních funkcí Configuration Manager, které spoluspráva nepodporuje.

Pokud úlohu přepnete do Intune, ale později ji změníte, můžete ji přepnout zpátky na Configuration Manager.

Další informace o podporovaných úlohách najdete v tématu [úlohy](workloads.md).

## <a name="switch-workloads-starting-in-version-1906"></a>Přepínání úloh počínaje verzí 1906
<!--3555750 FKA 1357954 -->
Počínaje verzí 1906 můžete nakonfigurovat různé pilotní kolekce pro každou úlohu spolusprávy. Možnost používat jiné pilotní kolekce vám umožní podrobnější přístup při posunování zatížení. Úlohy můžete přepínat, když povolíte spolusprávu, nebo později, až budete připraveni. Pokud jste ještě nepovolili spolusprávu, udělejte to jako první. Další informace najdete v tématu [Jak povolit spolusprávu](how-to-enable.md). Po povolení spolusprávy upravte nastavení ve vlastnostech spolusprávy.

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **spoluspráva** .  
2. Vyberte objekt spoluspráva a pak na pásu karet klikněte na tlačítko **vlastnosti** .  
3. Přepněte na kartu **úlohy** . Ve výchozím nastavení jsou všechny úlohy nastavené na nastavení **Configuration Manager** . Chcete-li přepnout úlohu, přesuňte ovládací prvek posuvníku pro tuto úlohu na požadované nastavení.  

    ![Obrazovka karty úlohy na stránce vlastností spolusprávy](media/3555750-co-management-workloads-tab.png)

    - **Configuration Manager**: Configuration Manager nadále spravuje tuto úlohu.  

    - **Pilotní nasazení Intune**: tuto úlohu můžete přepnout jenom pro zařízení v pilotní kolekci. **Pilotní kolekce** můžete změnit na kartě **fázování** stránky vlastností spolusprávy.  

    - **Intune**: přepněte tuto úlohu pro všechna zařízení s Windows 10 zaregistrovaná v rámci spolusprávy.  

4. Pokud je to potřeba, přejděte na kartu **fázování** a v případě potřeby změňte **pilotní kolekci** pro jakékoli úlohy.
  
   ![Obrazovka karty úlohy na stránce vlastností spolusprávy](media/3555750-co-management-staging-tab.png)

> [!Important]  
> - Než přepnete všechny úlohy, ujistěte se, že jste správně nakonfigurovali a nasadili odpovídající úlohy v Intune. Ujistěte se, že úlohy jsou vždycky spravované jedním z nástrojů pro správu vašich zařízení.
> - Když v Configuration Manager verze 1806 přepínáte úlohu spolusprávy, spoluspravovaná zařízení automaticky synchronizují zásady MDM z Microsoft Intune. K této synchronizaci dojde také v případě, že spustíte akci pro **stažení zásad počítače** z oznámení klienta v konzole Configuration Manager. Další informace najdete v tématu [spuštění načtení zásad klienta pomocí klientského oznámení](../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval). <!--1357377-->

## <a name="switch-workloads-in-version-1902-and-earlier"></a>Přepínání úloh ve verzi 1902 a starší

Úlohy můžete přepínat, když povolíte spolusprávu, nebo později, až budete připraveni. Pokud jste ještě nepovolili spolusprávu, udělejte to jako první. Další informace najdete v tématu [Jak povolit spolusprávu](how-to-enable.md). Po povolení spolusprávy upravte nastavení ve vlastnostech spolusprávy.

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **spoluspráva** .  

2. Vyberte objekt spoluspráva a pak na pásu karet klikněte na tlačítko **vlastnosti** .
   - Zobrazí se výzva, abyste se přihlásili do Azure AD. Výzva vám nebrání v aktualizaci registrace. Při každém otevření stránky **vlastností** se ale zobrazí výzva, dokud se nebudete přihlašovat.

3. Přepněte na kartu **úlohy** . Ve výchozím nastavení jsou všechny úlohy nastavené na nastavení **Configuration Manager** . Chcete-li přepnout úlohu, přesuňte ovládací prvek posuvníku pro tuto úlohu na požadované nastavení.  

    ![Obrazovka karty úlohy na stránce vlastností spolusprávy](media/properties-workloads.png)

    - **Configuration Manager**: Configuration Manager nadále spravuje tuto úlohu.  

    - **Pilotní nasazení Intune**: tuto úlohu můžete přepnout jenom pro zařízení v pilotní kolekci. **Pilotní kolekci** můžete změnit na kartě **fázování** stránky vlastností spolusprávy.  

    - **Intune**: přepněte tuto úlohu pro všechna zařízení s Windows 10 zaregistrovaná v rámci spolusprávy.  

4. Na kartě **fázování** stránky vlastností spolusprávy změňte v případě potřeby **pilotní kolekci** pro vaše úlohy.

5. Kliknutím na **OK** uložte a zavřete vlastnosti spolusprávy.

> [!Important]  
> - Než přepnete všechny úlohy, ujistěte se, že jste správně nakonfigurovali a nasadili odpovídající úlohy v Intune. Ujistěte se, že úlohy jsou vždycky spravované jedním z nástrojů pro správu vašich zařízení. 
> - Když v Configuration Manager verze 1806 přepínáte úlohu spolusprávy, spoluspravovaná zařízení automaticky synchronizují zásady MDM z Microsoft Intune. K této synchronizaci dojde také v případě, že spustíte akci pro **stažení zásad počítače** z oznámení klienta v konzole Configuration Manager. Další informace najdete v tématu [spuštění načtení zásad klienta pomocí klientského oznámení](../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval). <!--1357377-->

## <a name="next-steps"></a>Další kroky

[Sledování spolusprávy](how-to-monitor.md)
