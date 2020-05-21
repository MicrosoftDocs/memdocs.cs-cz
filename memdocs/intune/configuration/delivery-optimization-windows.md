---
title: Nastavení optimalizace doručování pro Windows 10 v Microsoft Intune – Azure | Microsoft Docs
description: Nakonfigurujte, jak zařízení s Windows 10 spravovaná pomocí služby Intune využívají optimalizaci doručování. V Intune vytvořte profil konfigurace zařízení pro instalaci aktualizací z Internetu. Přečtěte si taky, jak nahradit existující aktualizační kanály profilem Optimalizace doručení.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: kerimh
ms.openlocfilehash: 91989d2d8c5c68be9c560e306ea24cd33052a22c
ms.sourcegitcommit: 5d32dd481e2a944465755ce74e14c835cce2cd1c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/18/2020
ms.locfileid: "83551855"
---
# <a name="delivery-optimization-settings-in-microsoft-intune"></a>Nastavení Optimalizace doručení v Microsoft Intune

S Intune můžete použít nastavení optimalizace doručování pro zařízení s Windows 10 a snížit tak spotřebu šířky pásma, když tato zařízení stahují aplikace a aktualizace. Nakonfigurujte optimalizace doručování jako součást vašich profilů konfigurace zařízení.  

Tento článek popisuje, jak nakonfigurovat nastavení Optimalizace doručení v rámci profilu konfigurace zařízení. Po vytvoření profilu ho přiřadíte nebo nasadíte do zařízení s Windows 10.

Seznam nastavení Optimalizace doručení, která Intune podporuje, najdete v tématu [nastavení Optimalizace doručení pro Intune](delivery-optimization-settings.md).  

Další informace o optimalizaci doručení ve Windows 10 najdete v tématu [aktualizace pro optimalizaci doručení](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) v dokumentaci k Windows.  

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.

3. Zadejte tyto vlastnosti:

   - **Platforma**: vyberte **Windows 10 a novější**.
   - **Profil**: vyberte možnost **Optimalizace doručení**.

4. Vyberte **Vytvořit**.

5. V části **základy**zadejte následující vlastnosti:

   - **Název**: Zadejte popisný název nového profilu.
   - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.

7. Na stránce **nastavení konfigurace** definujte, jak chcete stahovat aktualizace a aplikace. Informace o dostupných nastaveních najdete v tématu věnovaném [nastavení optimalizace doručování pro Intune](delivery-optimization-settings.md).

   Po dokončení konfigurace nastavení vyberte **Další**.

8. Na stránce **obor (značky)** vyberte **Vybrat značky oboru** a otevřete tak podokno *Vybrat značky* , abyste přiřadili značky oboru k profilu.
  
   Pokračujte výběrem tlačítka **Next** (Další).

9. Na stránce **přiřazení** vyberte skupiny, které získají tento profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](../configuration/device-profile-assign.md).

   Vyberte **Další**.

10. Na stránce **pravidla použitelnosti** použijte možnosti **pravidlo**, **vlastnost**a **hodnota** k definování způsobu, jakým se tento profil vztahuje v rámci přiřazených skupin.

11. Po dokončení na stránce **Revize + vytvořit** klikněte na **vytvořit**. Profil se vytvoří a zobrazí se v seznamu.

Při příštím ověření každého zařízení se zásada použije.

## <a name="remove-delivery-optimization-from-windows-10-update-rings"></a>Odebrat optimalizaci doručování z aktualizačních kanálů Windows 10

Optimalizace doručení byla dříve nakonfigurována jako součást přenosů aktualizací softwaru. Od února 2019 se nastavení Optimalizace doručení nakonfigurují jako součást profilu konfigurace zařízení s optimalizací doručení, což zahrnuje další nastavení, která mají vliv na více než doručování aktualizací softwaru do zařízení. Pokud jste to ještě neudělali, odeberte nastavení optimalizace doručování z aktualizačních kanálů, a to tak, že ho nastavíte na *není nakonfigurované*, a pak pomocí profilu optimalizace doručování spravujte větší rozsah dostupných možností.

1. Vytvořit konfigurační profil zařízení pro optimalizaci doručení:

    1. V centru pro správu Microsoft Endpoint Manageru vyberte **zařízení**  >  **Konfigurace profily**  >  **vytvořit profil**.
    2. Zadejte tyto vlastnosti:

        - **Platforma**: vyberte **Windows 10 a novější**.
        - **Profil**: vyberte možnost **Optimalizace doručení**.

    3. Vyberte **Vytvořit**.
    4. V části **základy**zadejte následující vlastnosti:

        - **Název**: Zadejte popisný název nového profilu.
        - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.

    5. Vyberte **Další**.
    6. V **Configuration settings**  >  **režimu stahování**nastavení konfigurace vyberte stejný režim, který je používán existujícím kanálem aktualizace softwaru, *Pokud* nechcete změnit nastavení, která se vztahují na vaše zařízení. Možnosti:

        - **Není nakonfigurováno**
        - **Jenom HTTP bez partnerských vztahů**
        - **HTTP se provedlo při vytváření partnerských vztahů za stejným NAT.**
        - **HTTP Blend s partnerským vztahem přes soukromou skupinu**
        - **HTTP Blend s partnerským vztahem na internetu**
        - **Jednoduchý režim stahování bez partnerských vztahů**
        - **Režim obcházení**

    7. Nakonfigurujte [všechna další nastavení](delivery-optimization-settings.md) , která chcete spravovat, a pokračujte v vytváření profilu.

        V části **přiřazení**přiřaďte tento nový profil ke stejným zařízením a uživatelům jako stávající kanál aktualizace softwaru. Další informace najdete v tématu [přiřazení profilu](device-profile-assign.md).

2. Odkonfigurujte stávající softwarový kanál:

    1. V centru pro správu Microsoft Endpoint Manageru, navštivte **aktualizace softwaru** > aktualizační kanály Windows 10.
    2. V seznamu vyberte aktualizační kanál.
    3. V nastavení nastavte **režim stažení optimalizace doručování** na **Nenakonfigurováno**.
    4. **OK**  >  **Uložte** změny.

## <a name="next-steps"></a>Další kroky

Po [přiřazení profilu](device-profile-assign.md) [sledujte jeho stav](device-profile-monitor.md) .

Zobrazit [nastavení Optimalizace doručení](delivery-optimization-settings.md) pro Intune
