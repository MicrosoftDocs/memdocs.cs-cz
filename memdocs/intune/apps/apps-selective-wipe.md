---
title: Jak z aplikací vymazat jenom firemní data
titleSuffix: Microsoft Intune
description: Naučte se, jak selektivně vymazat jenom firemní data z aplikací spravovaných přes Intune pomocí Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/10/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 42605e6e-5b84-44ff-b86e-346ea123b53e
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2d5e73961daae140a039ba243e7364ffd6b06502
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83984101"
---
# <a name="how-to-wipe-only-corporate-data-from-intune-managed-apps"></a>Jak z aplikací spravovaných pomocí Intune vymazat jenom firemní data

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

V případě ztráty nebo odcizení zařízení nebo když zaměstnanec opouští společnost, je vhodné se ujistit, že byla ze zařízení odebraná firemní data. Nemusí ale být vhodné odebrat ze zařízení osobní data, zvlášť jestli je to zařízení, které vlastní zaměstnanec.

>[!NOTE]
> Platformy iOS/iPadOS, Androidem a Windows 10 jsou jediné platformy, které jsou aktuálně podporované pro mazání podnikových dat ze spravovaných aplikací Intune. Spravované aplikace Intune jsou aplikace, které obsahují sadu Intune APP SDK a mají licencovaný uživatelský účet pro vaši organizaci. Nasazení zásad ochrany aplikací není nutné k povolení selektivního vymazání aplikace.

Pokud chcete selektivně odebrat data firemních aplikací, vytvořte žádost o vymazání pomocí kroků v tomto tématu. Po dokončení žádosti se při příštím spuštění aplikace na zařízení z aplikace odeberou firemní data. Kromě vytvoření žádosti o vymazání můžete nakonfigurovat selektivní vymazání dat organizace jako novou akci, když nejsou splněny podmínky nastavení přístupu zásad ochrany aplikací. Tato funkce umožňuje automaticky chránit a odebírat citlivá data organizace z aplikací na základě předem nakonfigurovaných kritérií.

>[!IMPORTANT]
> Kontakty synchronizované přímo z aplikace do nativního adresáře se odeberou. Kontakty synchronizované z nativního adresáře do dalšího externího zdroje není možné vymazat. V současnosti to platí jen pro aplikaci Microsoft Outlook.

## <a name="deployed-wip-policies-without-user-enrollment"></a>Nasazené zásady WIP bez registrace uživatele 
Zásady Windows Information Protection (NV) se dají nasadit, aniž by uživatelé MDM museli zaregistrovat svoje zařízení s Windows 10. Tato konfigurace umožňuje společnostem chránit jejich podnikové dokumenty na základě konfigurace WIP a zároveň umožňuje uživatelům uchovat si správu svých vlastních zařízení s Windows. Po ochraně dokumentů pomocí zásad nedokončené výroby je možné chráněná data selektivně vymazat správce Intune ([globální správce nebo správce služby Intune](../fundamentals/users-add.md#types-of-administrators)). Výběrem uživatele a zařízení a odesláním žádosti o vymazání se veškerá data chráněná prostřednictvím zásad WIP stanou nepoužitelnými. Z Intune v Azure Portal vyberte možnost **klientská**  >  **aplikace aplikace selektivní vymazání**. Další informace najdete v článku [Vytvoření a nasazení zásady ochrany aplikací WIP (Windows Information Protection) u Intune](windows-information-protection-policy-create.md).

## <a name="create-a-device-based-wipe-request"></a>Vytvoření žádosti o vymazání na základě zařízení

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace aplikace**  >  **selektivní vymazání**  >  **vytvořit žádost o vymazání**.<br>
   Zobrazí se podokno **vytvořit žádost o vymazání** .
3. Klikněte na **Vybrat uživatele**, vyberte uživatele, jehož data aplikací chcete vymazat, a klikněte na **Vybrat** v dolní části podokna **Vybrat uživatele** .

    ![Snímek obrazovky s podoknem vybrat uživatele](./media/apps-selective-wipe/apps-selective-wipe-01.png)

4. Klikněte na **Vybrat zařízení**, zvolte zařízení a v dolní části podokna **Vybrat zařízení** klikněte na **Vybrat** .

    ![Snímek obrazovky s podoknem vytvořit žádost o vymazání, kde je vybrané zařízení](./media/apps-selective-wipe/apps-selective-wipe-02.png)

5. Kliknutím na **vytvořit** vytvořte žádost o vymazání.

Služba vytvoří a sleduje samostatnou žádost o vymazání pro každou chráněnou aplikaci na zařízení a uživatele přidruženého k této žádosti o vymazání.

   ![Snímek obrazovky s podoknem klientské aplikace – selektivní vymazání aplikace](./media/apps-selective-wipe/apps-selective-wipe-03.png)

## <a name="create-a-user-based-wipe-request"></a>Vytvoření žádosti o vymazání na základě uživatele

Přidáním uživatele do vymazání na úrovni uživatele budeme automaticky vydávat příkazy pro vymazání všech aplikací na všech zařízeních uživatele.  Uživatel bude nadále získávat příkazy vymazání při každém vrácení se změnami ze všech zařízení.  Chcete-li uživatele znovu povolit, je nutné je odebrat ze seznamu.  

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace aplikace**  >  **selektivní vymazání**  >  **vytvořit žádost o vymazání**.<br>
   Výběr **vymazání na úrovni uživatele**
3. Klikněte na tlačítko **Přidat** a **Vyberte podokno uživatel** .
4. Zvolte uživatele, jehož data aplikací chcete vymazat, a klikněte na **Vybrat**.

## <a name="monitor-your-wipe-requests"></a>Monitorování žádostí o vymazání

Můžete získat souhrnnou sestavu, která zobrazuje celkový stav žádostí o vymazání a také počet nevyřízených a neúspěšných žádostí. Další podrobnosti získáte tímto postupem:

1. V podokně **aplikace**s  >  **selektivním vymazáním aplikace** můžete zobrazit seznam žádostí seskupených podle uživatelů. Protože systém vytvoří žádost o vymazání pro každou chráněnou aplikaci spuštěnou na zařízení, může být u uživatele více žádostí. Stav označuje, jestli je žádost o vymazání **nevyřízená**, **selhala** nebo byla **úspěšná**.

    ![Snímek obrazovky se stavem žádosti o vymazání v podokně Selektivní vymazání aplikace](./media/apps-selective-wipe/wipe-request-status-1.png)

Uvidíte také název zařízení a jeho typ, což vám pomůže při orientaci v sestavách.

>[!IMPORTANT]
> Aby k vymazání došlo, musí uživatel otevřít aplikaci. Po zadání požadavku může vymazání samotné trvat až 30 minut.

## <a name="delete-a-device-wipe-request"></a>Odstranění žádosti o vymazání zařízení

Vymazání v čekajícím stavu se zobrazují, dokud je ručně neodstraníte. Ruční odstranění žádosti o vymazání:

1. Přejděte do podokna **Klientské aplikace – Selektivní vymazání aplikace**.

2. V seznamu klikněte pravým tlačítkem na žádost o vymazání, kterou chcete odstranit, a zvolte **Odstranit žádost o vymazání**.

    ![Snímek obrazovky se seznamem žádostí o vymazání v podokně Selektivní vymazání aplikace](./media/apps-selective-wipe/delete-wipe-request.png)

3. Zobrazí se výzva k potvrzení odstranění. Zvolte **Ano** nebo **Ne** a klikněte na **OK**.

## <a name="delete-a-user-wipe-request"></a>Odstranění žádosti o vymazání uživatele

Vymazání uživatele zůstane v seznamu, dokud ho neodebere správce. Odebrání uživatele ze seznamu:

1. V podokně **klientské aplikace – selektivní vymazání aplikace** vyberte **Vymazat na úrovni uživatele** .
2. V seznamu klikněte pravým tlačítkem na uživatele, kterého chcete odstranit, a pak zvolte **Odstranit**. 


## <a name="see-also"></a>Viz také
[Zásady ochrany aplikací](app-protection-policy.md)

[Co je správa aplikací?](app-management.md)
