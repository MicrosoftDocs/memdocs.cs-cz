---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 08/23/2019
ms.openlocfilehash: d8eaaa403bd1dd97214b4eff82be79d5c2a6566e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710885"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **spoluspráva** . Klikněte na tlačítko **Konfigurovat spolusprávu** na pásu karet a otevřete tak **Průvodce konfigurací spolusprávy**.

2. Na stránce **předplatné** v průvodci vyberte **Přihlásit**se. Přihlaste se k tenantovi Intune a pak vyberte **Další**.  

3. Na stránce **Povolení** vyberte **Automatický zápis do nastavení Intune** , a to buď jako **pilotní** , nebo jako **všechno**. Pokud uživatel zruší registraci zařízení, při dalším vyhodnocení zásady se znovu zaregistruje. <!--3330596--> 

    Tato akce umožňuje automatický zápis klientů v Intune pro stávající klienty Configuration Manager. Když zvolíte **pilotní nasazení**, do Intune se automaticky zaregistrují jenom Configuration Manager klienti, kteří jsou členy pilotní kolekce. Tato možnost umožňuje povolit spolusprávu u podmnožiny klientů pro prvotní testování spolusprávy a zavedení spolusprávy pomocí dvoufázového přístupu. 

    > [!Note]  
    > Počínaje verzí 1806 není automatický zápis okamžitý pro všechny klienty. Toto chování pomáhá lépe škálovat registraci pro velká prostředí. Configuration Manager náhodně vyčíslit registraci na základě počtu klientů. Pokud má vaše prostředí například klienty 100 000, při povolení tohoto nastavení dojde k zápisu za několik dní.<!--1358003-->  

4. Pro Internetová zařízení, která jsou už zaregistrovaná v Intune, zkopírujte a uložte příkazový řádek na stránce **Povolení** . Tento příkazový řádek můžete použít k instalaci klienta Configuration Manager jako aplikace v Intune. Pokud tento příkazový řádek neuložíte nyní, můžete si kdykoli projít konfiguraci spolusprávy a získat tento příkazový řádek.

5. Na stránce **úlohy** pro každou úlohu vyberte skupinu zařízení, kterou chcete přesunout do správy pomocí Intune. Další informace najdete v tématu [úlohy](../workloads.md).  

    Pokud chcete povolit spolusprávu, nemusíte teď přepínat úlohy. Úlohy můžete přepínat později. Další informace najdete v tématu [Jak přepínat úlohy](../how-to-switch-workloads.md).  

    Nastavení **pilotní služby Intune** přepíná přidruženou úlohu jenom pro zařízení v pilotní kolekci. Nastavení **Intune** přepíná přidruženou úlohu pro všechna zařízení s Windows 10, která jsou společně spravovaná.  

    > [!Important]
    > Než přepnete všechny úlohy, ujistěte se, že jste správně nakonfigurovali a nasadili odpovídající úlohy v Intune. Ujistěte se, že úlohy jsou vždycky spravované jedním z nástrojů pro správu vašich zařízení.  

6. Na stránce **Příprava** nakonfigurujte následující nastavení:  

    - **Pilotní nasazení**: pilotní skupina obsahuje jednu nebo více kolekcí, které vyberete. Tuto skupinu použijte jako součást dvoufázové zavedení spolusprávy. Začněte s malým testovacím kolekcí a potom do pilotní skupiny přidejte další kolekce, které se zavádějí do společné správy pro více uživatelů a zařízení. Kolekce v pilotní skupině můžete kdykoli změnit.  

    - **Výroba**: Nakonfigurujte **skupinu vyloučení** s jednou nebo více kolekcemi. Zařízení, která jsou členem některé z kolekcí v této skupině, se z použití spolusprávy vylučují.  

7. Pokud chcete povolit spolusprávu, dokončete průvodce.  
