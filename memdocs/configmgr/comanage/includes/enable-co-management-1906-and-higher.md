---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: b0c25174873e00cf23dacd2c77208775f1fb1ced
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89644179"
---
<!--3555750 FKA 1357954 --Don't apply H2/H3 in this include file since they are context driven by article-->

Při povolování spolusprávy můžete použít veřejný cloud Azure, Azure USA pro státní správu USA nebo Microsoft Azure Čína 21Vianet (přidáno ve verzi 2006). Pokud chcete povolit spolusprávu od verze Configuration Manager 1906, postupujte podle následujících pokynů:

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **spoluspráva** . Vyberte možnost **Konfigurovat spolusprávu** na pásu karet a otevřete tak **Průvodce konfigurací spolusprávy**.

1. Na stránce průvodce **připojování tenanta** nakonfigurujte **prostředí Azure** tak, aby se používalo. Vyberte jedno z následujících prostředí:

   - Veřejný cloud Azure
   - Cloud Azure pro státní správu USA.<!--4075452-->
   - Cloud Azure Čína (přidaný ve verzi 2006)<!--7133238-->
      - Než se připojíte ke cloudu Azure Čína, aktualizujte klienta Configuration Manager na nejnovější verzi na vašich zařízeních. <!--7630213--> 

   Když vyberete Azure Čína Cloud nebo Azure USA pro státní správu, je možnost **Odeslat do centra pro správu služby Microsoft Endpoint Manager** pro [připojení tenanta](../../tenant-attach/device-sync-actions.md) zakázaná.

1. Vyberte **Přihlásit se**. Přihlaste se jako globální správce Azure AD a pak vyberte **Další**. K tomuto průvodci se přihlašujete jednou pro účely tohoto průvodce. Přihlašovací údaje se neukládají nebo se znovu používají jinde.

1. Na stránce **Povolit** vyberte následující nastavení:

   - **Automatický zápis do Intune** – povolí automatický zápis klientů v Intune pro stávající klienty Configuration Manager. Tato možnost umožňuje povolit spolusprávu u podmnožiny klientů pro prvotní testování spolusprávy a zavedení spolusprávy pomocí dvoufázového přístupu. Pokud uživatel zruší registraci zařízení, při dalším vyhodnocení zásady se znovu zaregistruje. <!--3330596-->

      - **Pilotní nasazení** : do Intune se automaticky zaregistrují jenom klienti Configuration Manager, kteří jsou členy kolekce **automatického zápisu do Intune** .
      - **Vše** – povolí automatický zápis pro všechny systémy Windows 10, verze 1709 nebo novější.

   - **Automatický zápis do Intune** – Tato kolekce by měla obsahovat všechny klienty, které chcete integrovat do společné správy. Je v podstatě nadmnožinou všech dalších pracovních kolekcí.

   ![Zadejte kolekci automatického zápisu do Intune. ](../media/3555750-co-management-onboarding-enablement.png)
      
      Automatický zápis není pro všechny klienty okamžitý. Toto chování pomáhá lépe škálovat registraci pro velká prostředí. Configuration Manager náhodně vyčíslit registraci na základě počtu klientů. Pokud má vaše prostředí například klienty 100 000, při povolení tohoto nastavení dojde k zápisu za několik dní.<!--1358003-->

      > [!Note]  
      > Počínaje verzí 1906:
      >
      > - Nové spoluspravované zařízení teď automaticky zaregistruje službu Microsoft Intune na základě tokenu *zařízení* Azure Active Directory (Azure AD). Není nutné čekat, než se uživatel přihlásí k zařízení, aby se mohl spustit automatický zápis. Tato změna pomáhá snižovat počet zařízení se stavem registrace *čeká na přihlášení uživatele*.<!-- 4454491 --> Pro podporu tohoto chování musí zařízení používat Windows 10 verze 1803 nebo novější. Další informace najdete v tématu [stav registrace spolusprávy](../how-to-monitor.md#co-management-enrollment-status).
      >
      > - Pokud už máte zařízení zaregistrovaná v rámci společné správy, nová zařízení se teď registrují hned, jakmile splní [požadavky](../overview.md#prerequisites).<!--4321130-->

1. Pro Internetová zařízení, která jsou už zaregistrovaná v Intune, zkopírujte a uložte příkazový řádek na stránce **Povolení** . Tento příkazový řádek použijete k instalaci klienta Configuration Manager jako aplikace v Intune pro Internetová zařízení. Pokud tento příkazový řádek neuložíte nyní, můžete si kdykoli projít konfiguraci spolusprávy a získat tento příkazový řádek.

1. Na stránce **úlohy** pro každou úlohu vyberte skupinu zařízení, kterou chcete přesunout do správy pomocí Intune. Další informace najdete v tématu [úlohy](../workloads.md). Pokud chcete povolit spolusprávu, nemusíte teď přepínat úlohy. Úlohy můžete přepínat později. Další informace najdete v tématu [Jak přepínat úlohy](../how-to-switch-workloads.md).  

    - **Pilotní nasazení Intune** – přepíná přidruženou úlohu jenom pro zařízení v pilotních kolekcích, které zadáte na **pracovní** stránce. Každé zatížení může mít jinou pilotní kolekci.
    - **Intune** – přepíná přidruženou úlohu pro všechna zařízení s Windows 10, která jsou společně spravovaná.  

    > [!Important]
    > Než přepnete všechny úlohy, ujistěte se, že jste správně nakonfigurovali a nasadili odpovídající úlohy v Intune. Ujistěte se, že úlohy jsou vždycky spravované jedním z nástrojů pro správu vašich zařízení.  

1. Na stránce **Příprava** zadejte pilotní kolekci pro všechny úlohy, které jsou nastavené na **pilotní nasazení Intune**.

   ![Průvodce konfigurací spolusprávy, pracovní stránka, určení pilotních kolekcí](../media/3555750-co-management-onboarding-staging.png)

1. Pokud chcete povolit spolusprávu, dokončete průvodce.
