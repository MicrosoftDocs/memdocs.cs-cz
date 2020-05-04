---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 03/12/2020
ms.openlocfilehash: 37376d137409b06816d4c5dff5a0909f57531443
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710892"
---
<!--3555750 FKA 1357954 --Don't apply H2/H3 in this include file since they are context driven by article-->
1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **spoluspráva** . Klikněte na tlačítko **Konfigurovat spolusprávu** na pásu karet a otevřete tak **Průvodce konfigurací spolusprávy**.

2. Na stránce **předplatné** v průvodci nakonfigurujte následující nastavení:

    - **Prostředí Azure** , které se má použít. Například veřejný cloud Azure nebo Cloud pro státní správu Azure USA.<!--4075452-->  

    - Vyberte **Přihlásit se**. Přihlaste se jako globální správce Azure AD a pak vyberte **Další**.  

        > [!TIP]
        > K tomuto průvodci se přihlašujete jednou pro účely tohoto průvodce. Přihlašovací údaje se neukládají nebo se znovu používají jinde.

3. Na stránce **Povolit** vyberte následující nastavení:

   - **Automatický zápis do Intune** – povolí automatický zápis klientů v Intune pro stávající klienty Configuration Manager. Tato možnost umožňuje povolit spolusprávu u podmnožiny klientů pro prvotní testování spolusprávy a zavedení spolusprávy pomocí dvoufázového přístupu. Pokud uživatel zruší registraci zařízení, při dalším vyhodnocení zásady se znovu zaregistruje. <!--3330596-->

      - **Pilotní nasazení** : do Intune se automaticky zaregistrují jenom klienti Configuration Manager, kteří jsou členy kolekce **automatického zápisu do Intune** .
      - **Vše** – povolí automatický zápis pro všechny systémy Windows 10, verze 1709 nebo novější.

   - **Automatický zápis do Intune** – Tato kolekce by měla obsahovat všechny klienty, které chcete integrovat do společné správy. Je v podstatě nadmnožinou všech dalších pracovních kolekcí.

   ![Zadejte kolekci automatického zápisu do Intune. ](../media/3555750-co-management-onboarding-enablement.png)

      > [!Note]  
      > Počínaje verzí 1806 není automatický zápis okamžitý pro všechny klienty. Toto chování pomáhá lépe škálovat registraci pro velká prostředí. Configuration Manager náhodně vyčíslit registraci na základě počtu klientů. Pokud má vaše prostředí například klienty 100 000, při povolení tohoto nastavení dojde k zápisu za několik dní.<!--1358003-->  
      >
      > Počínaje verzí 1906:
      >
      > - Nové spoluspravované zařízení teď automaticky zaregistruje službu Microsoft Intune na základě tokenu *zařízení* Azure Active Directory (Azure AD). Není nutné čekat, než se uživatel přihlásí k zařízení, aby se mohl spustit automatický zápis. Tato změna pomáhá snižovat počet zařízení se stavem registrace *čeká na přihlášení uživatele*.<!-- 4454491 --> Pro podporu tohoto chování musí zařízení používat Windows 10 verze 1803 nebo novější. Další informace najdete v tématu [stav registrace spolusprávy](../how-to-monitor.md#co-management-enrollment-status).
      >
      > - Pokud už máte zařízení zaregistrovaná v rámci společné správy, nová zařízení se teď registrují hned, jakmile splní [požadavky](../overview.md#prerequisites).<!--4321130-->

4. Pro Internetová zařízení, která jsou už zaregistrovaná v Intune, zkopírujte a uložte příkazový řádek na stránce **Povolení** . Tento příkazový řádek použijete k instalaci klienta Configuration Manager jako aplikace v Intune pro Internetová zařízení. Pokud tento příkazový řádek neuložíte nyní, můžete si kdykoli projít konfiguraci spolusprávy a získat tento příkazový řádek.

5. Na stránce **úlohy** pro každou úlohu vyberte skupinu zařízení, kterou chcete přesunout do správy pomocí Intune. Další informace najdete v tématu [úlohy](../workloads.md). Pokud chcete povolit spolusprávu, nemusíte teď přepínat úlohy. Úlohy můžete přepínat později. Další informace najdete v tématu [Jak přepínat úlohy](../how-to-switch-workloads.md).  

    - **Pilotní nasazení Intune** – přepíná přidruženou úlohu jenom pro zařízení v pilotních kolekcích, které zadáte na **pracovní** stránce. Každé zatížení může mít jinou pilotní kolekci.
    - **Intune** – přepíná přidruženou úlohu pro všechna zařízení s Windows 10, která jsou společně spravovaná.  

    > [!Important]
    > Než přepnete všechny úlohy, ujistěte se, že jste správně nakonfigurovali a nasadili odpovídající úlohy v Intune. Ujistěte se, že úlohy jsou vždycky spravované jedním z nástrojů pro správu vašich zařízení.  

6. Na stránce **Příprava** zadejte pilotní kolekci pro všechny úlohy, které jsou nastavené na **pilotní nasazení Intune**.

   ![Zadejte kolekci automatického zápisu do Intune. ](../media/3555750-co-management-onboarding-staging.png)

7. Pokud chcete povolit spolusprávu, dokončete průvodce.
