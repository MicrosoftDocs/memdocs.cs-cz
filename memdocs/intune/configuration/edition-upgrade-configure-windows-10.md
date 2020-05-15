---
title: Upgrade nebo použití režimu S v zařízeních S Windows 10 – Microsoft Intune – Azure | Microsoft Docs
description: Pomocí Microsoft Intune můžete upgradovat zařízení s Windows 10 na jinou edici nebo přepnout na režim S. Správci můžou použít konfigurační profil zařízení k upgradu Windows 10 Professional na Windows 10 Enterprise a přepnutí z režimu S. Seznamte se s podporovanými způsoby upgradu pro Windows 10 pro, N Edition, školství, Cloud, Enterprise, Core, holografická a mobilní zařízení.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ae8b6528-7979-47d8-abe0-58cea1905270
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b7c75d75b6afef728b23093dd4313f1c028fc5c7
ms.sourcegitcommit: b94415467831517f2aeab9c7c8a13fe8db8bc8ed
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/14/2020
ms.locfileid: "83401731"
---
# <a name="upgrade-windows-10-editions-or-switch-out-of-s-mode-on-devices-using-microsoft-intune"></a>Upgradovat edice Windows 10 nebo zapínat na zařízeních v režimu S použitím Microsoft Intune

V rámci řešení pro správu mobilních zařízení (MDM) můžete chtít upgradovat zařízení s Windows 10. Například chcete upgradovat zařízení s Windows 10 Professional na Windows 10 Enterprise. Nebo chcete, aby zařízení přepnulo režim S.

[Režim Windows 10 S](https://support.microsoft.com/help/4456067/windows-10-switch-out-of-s-mode) (otevře jiný web společnosti Microsoft) je navržený pro zabezpečení a výkon. K přepnutí do režimu S můžete použít Intune. Přepnutí z režimu S se nedá vrátit. Jakmile se přepnete z režimu S, nemůžete se do tohoto režimu Windows 10 vrátit.

Podívejte se [na nejčastější dotazy](https://support.microsoft.com/help/4020089/windows-10-in-s-mode-faq) týkající se režimu S.

Tato funkce platí pro:

- Windows 10 a novější
- Windows 10 1809 nebo novější pro režim S
- Windows Holographic for Business

Tyto funkce jsou dostupné v Intune a správce je může nakonfigurovat. Intune používá konfigurační profily k vytvoření a přizpůsobení těchto nastavení potřebám vaší organizace. Po přidání těchto funkcí do profilu můžete tento profil vložit nebo nasadit do zařízení s Windows 10 ve vaší organizaci. Když nasadíte profil, Intune automaticky upgraduje zařízení nebo přepne z režimu S.

Tento článek obsahuje seznam podporovaných cest upgradu a ukazuje, jak vytvořit profil konfigurace zařízení. Můžete si také prohlédnout všechna dostupná nastavení upgradu a režimu S [Windows 10](edition-upgrade-windows-settings.md).

> [!NOTE]
> Pokud přiřazení zásady odeberete později, verze Windows na zařízení se nevrátí. Zařízení bude nadále fungovat normálně.

## <a name="prerequisites"></a>Požadavky

Před upgradem zařízení se ujistěte, že máte následující požadavky:

- Platný kód Product Key k instalaci aktualizované verze Windows na všechna zařízení, na která touto zásadou cílíte (pro edice Windows 10 Desktop). Můžete využít klíče k vícenásobné aktivaci (MAK) nebo kódy serveru správy klíčů (KMS).
- Pro edice Windows 10 Mobile a Windows 10 je možné použít soubor s licencí společnosti Microsoft. Soubor s licencí obsahuje licenční informace pro instalaci aktualizované edice na všechna zařízení, na která tato zásada cílíte.
- Zařízení s Windows 10, kterým zásady přiřazujete, jsou zaregistrovaná v Microsoft Intune. Zásadu upgradu edice nemůžete použít u počítačů s klientským softwarem Intune pro počítače.

## <a name="supported-upgrade-paths"></a>Podporované možnosti upgradu

V následující tabulce jsou podporované cesty upgradu pro profil upgradu edice Windows 10.

| Upgradovat z | Upgrade na |
|---|---|
| Windows 10 Pro | Windows 10 Education <br/>Windows 10 Enterprise <br/>Windows 10 Pro Education |
| Edice Windows 10 Pro N | Edice Windows 10 Education N <br/>Edice Windows 10 Enterprise N <br/>Edice Windows 10 Pro Education N | 
| Windows 10 Pro Education | Windows 10 Education | 
| Edice Windows 10 Pro Education N | Edice Windows 10 Education N |
| Windows 10 Cloud | Windows 10 Education <br/>Windows 10 Enterprise <br/>Windows 10 Pro <br/>Windows 10 Pro Education | 
| Edice Windows 10 Cloud N | Edice Windows 10 Education N <br/>Edice Windows 10 Enterprise N <br/>Edice Windows 10 Pro N <br/>Edice Windows 10 Pro Education N | 
| Windows 10 Enterprise | Windows 10 Education | 
| Edice Windows 10 Enterprise N | Edice Windows 10 Education N | 
| Windows 10 Core | Windows 10 Education <br/>Windows 10 Enterprise <br/>Windows 10 Pro Education | 
| Edice Windows 10 Core N | Edice Windows 10 Education N <br/>Edice Windows 10 Enterprise N <br/>Edice Windows 10 Pro Education N | 
| Windows 10 Holographic | Windows 10 Holographic for Business |
| Windows 10 Mobile | Windows 10 Mobile Enterprise |

<!--The following table provides information about the supported upgrade paths for Windows 10 editions in this policy:

![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)  (X) = not supported    
![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)    (green checkmark) = supported    

|Upgrade from edition\Upgrade to edition|Education|Education N|Pro Education|Pro Education N|Enterprise|Enterprise N|Professional|Professional N|Mobile Enterprise|Holographic for Business|
|--------|--------|--------|--------|--------|--------|--------|--------|--------|--------|--------|--------|
|Pro|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Pro N|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Pro Education|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Pro Education N|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Cloud|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Cloud N|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Enterprise|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Enterprise N|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Core|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Core N|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Mobile|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Holographic|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png) -->

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.
3. Zadejte tyto vlastnosti:

    - **Platforma**: vyberte **Windows 10 a novější**.
    - **Profil**: vyberte **upgrade edice**.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

    - **Název**: Zadejte popisný název nového profilu. Zadejte například něco jako `Windows 10 edition upgrade profile` nebo `Windows 10 switch off S mode` .
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.
7. V **nastavení konfigurace**zadejte nastavení, které chcete konfigurovat. Seznam všech nastavení a o tom, co dělají, najdete v těchto tématech:

    - [Upgrade a režim S Windows 10](edition-upgrade-windows-settings.md)
    - [Windows Holographic for Business](holographic-upgrade.md)

8. Vyberte **Další**.

9. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu pro konkrétní IT skupiny, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment` . Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](../fundamentals/scope-tags.md).

    Vyberte **Další**.

10. V části **přiřazení**vyberte uživatele nebo skupinu uživatelů, kteří obdrží váš profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](device-profile-assign.md).

    Vyberte **Další**.

11. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

Při příštím ověření každého zařízení se zásada použije.

## <a name="next-steps"></a>Další kroky

Po [přiřazení profilu](device-profile-assign.md) [sledujte jeho stav](device-profile-monitor.md).

Podívejte se na nastavení upgradu a režimu S pro zařízení S [Windows 10](edition-upgrade-windows-settings.md) a [Windows holografickým pro firmy](holographic-upgrade.md) .
