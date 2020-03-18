---
title: Nastavení optimalizace doručování pro Windows 10 v Microsoft Intune – Azure | Microsoft Docs
description: Nakonfigurujte, jak zařízení s Windows 10 spravovaná pomocí služby Intune využívají optimalizaci doručování. V Intune vytvořte profil konfigurace zařízení pro instalaci aktualizací z Internetu. Přečtěte si taky, jak nahradit existující aktualizační kanály profilem Optimalizace doručení.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/10/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: kerimh
ms.openlocfilehash: 71039737a74aebb3066c001536aaf677a0467696
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79327351"
---
# <a name="delivery-optimization-settings-in-microsoft-intune"></a>Nastavení Optimalizace doručení v Microsoft Intune

S Intune můžete použít nastavení optimalizace doručování pro zařízení s Windows 10 a snížit tak spotřebu šířky pásma, když tato zařízení stahují aplikace a aktualizace. Nakonfigurujte optimalizace doručování jako součást vašich profilů konfigurace zařízení.  

Tento článek popisuje, jak nakonfigurovat nastavení Optimalizace doručení v rámci profilu konfigurace zařízení. Po vytvoření profilu ho přiřadíte nebo nasadíte do zařízení s Windows 10.

Seznam nastavení Optimalizace doručení, která Intune podporuje, najdete v tématu [nastavení Optimalizace doručení pro Intune](delivery-optimization-settings.md).  

Další informace o optimalizaci doručení ve Windows 10 najdete v tématu [aktualizace pro optimalizaci doručení](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) v dokumentaci k Windows.  

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.

3. Zadejte následující vlastnosti:

    - **Název**: Zadejte popisný název nového profilu.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.
    - **Platforma**: vyberte **Windows 10 a novější**.
    - **Typ profilu**: vyberte **Optimalizace doručení**.

4. Vyberte **nastavení** > **Konfigurovat**a určete, jak se mají aktualizace a aplikace stahovat. Informace o dostupných nastaveních najdete v tématu věnovaném [nastavení optimalizace doručování pro Intune](delivery-optimization-settings.md).

5. Po dokončení vyberte **OK** > **vytvořit** a uložte provedené změny.

Profil se vytvoří a zobrazí se v seznamu. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).

<!-- ## Move existing update rings to delivery optimization

**Delivery optimization** settings replace **Software updates – Windows 10 Update Rings**. Your existing update rings can be easily changed to use the **Delivery optimization** settings. To maintain the same settings when you create a delivery optimization profile, use the same *Delivery optimization download mode* and then set the same settings as you already use. However, you can choose to reconfigure delivery optimization settings to take advantage of the full range of addition settings that the Delivery Optimization profile can manage. 
-->

## <a name="remove-delivery-optimization-from-windows-10-update-rings"></a>Odebrat optimalizaci doručování z aktualizačních kanálů Windows 10

Optimalizace doručení byla dříve nakonfigurována jako součást přenosů aktualizací softwaru. Od února 2019 se nastavení Optimalizace doručení nakonfigurují jako součást profilu konfigurace zařízení s optimalizací doručení, což zahrnuje další nastavení, která mají vliv na více než doručování aktualizací softwaru do zařízení. Pokud jste to ještě neudělali, odeberte nastavení optimalizace doručování z aktualizačních kanálů, a to tak, že ho nastavíte na *není nakonfigurované*, a pak pomocí profilu optimalizace doručování spravujte větší rozsah dostupných možností.

1. Vytvořit konfigurační profil zařízení pro optimalizaci doručení:

    1. V centru pro správu Microsoft Endpoint Manageru vyberte **zařízení** > **konfigurační profily** > **vytvořit profil**.
    2. Zadejte následující vlastnosti:

        - **Název**: Zadejte popisný název nového profilu.
        - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.
        - **Platforma**: vyberte **Windows 10 a novější**.
        - **Typ profilu**: vyberte **Optimalizace doručení**.
        - **Nastavení**: **režim stahování pro optimalizaci doručení**vyberte stejný režim, který je používán existujícím kanálem aktualizace softwaru, pokud nechcete změnit nastavení, která se vztahují na vaše zařízení. Možnosti:
            - **Nenakonfigurované**
            - **Jenom HTTP bez partnerských vztahů**
            - **HTTP se provedlo při vytváření partnerských vztahů za stejným NAT.**
            - **HTTP Blend s partnerským vztahem přes soukromou skupinu**
            - **HTTP Blend s partnerským vztahem na internetu**
            - **Jednoduchý režim stahování bez partnerských vztahů**
            - **Režim obcházení**
    3. Nakonfigurujte všechna další nastavení, která budete chtít spravovat.

2. Přiřaďte tento nový profil ke stejným zařízením a uživatelům jako stávající kanál aktualizace softwaru. [Přiřaďte profil](device-profile-assign.md) seznamu kroků.

3. Odkonfigurujte stávající softwarový kanál:
    1. V centru pro správu Microsoft Endpoint Manageru, navštivte **aktualizace softwaru** > aktualizační kanály Windows 10.
    2. V seznamu vyberte aktualizační kanál.
    3. V nastavení nastavte **režim stažení optimalizace doručování** na **Nenakonfigurováno**.
    4. **OK** > **Uložit** změny.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [Sledujte](device-profile-monitor.md) jeho stav.  
Zobrazit [nastavení Optimalizace doručení](delivery-optimization-settings.md) pro Intune
