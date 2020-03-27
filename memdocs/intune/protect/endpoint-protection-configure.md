---
title: Konfigurace nastavení ochrany koncových bodů v Microsoft Intune – Azure | Microsoft Docs
description: Nastavení ochrany koncových bodů určete při vytváření profilu zařízení s macOS nebo Windows 10 v Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/18/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: karthib
ms.openlocfilehash: 98e72f11781ba13dbe5d4e576643d04e51f3c95d
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80327464"
---
# <a name="add-endpoint-protection-settings-in-intune"></a>Přidání nastavení ochrany koncových bodů v Intune

Pomocí služby Intune můžete pomocí profilů konfigurace zařízení spravovat běžné funkce zabezpečení služby Endpoint Protection na zařízeních, včetně těchto:

- Brána firewall
- BitLocker
- Povolení a blokování aplikací
- Microsoft Defender a šifrování

Můžete například vytvořit profil ochrany koncových bodů, který umožní uživatelům macOS instalovat aplikace jenom z Mac App Storu. Nebo můžete při spouštění aplikací na zařízeních s Windows 10 aktivovat filtr Windows SmartScreen.

Než vytvoříte profil, přečtěte si následující články, které podrobně popisují nastavení ochrany koncových bodů, které Intune může spravovat pro každou podporovanou platformu:

- [Nastavení macOS](endpoint-protection-macos.md)
- [Nastavení Windows 10](endpoint-protection-windows-10.md)

## <a name="create-a-device-profile-containing-endpoint-protection-settings"></a>Vytvoření profilu zařízení obsahujícího nastavení ochrany koncových bodů

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.

3. Zadejte **Název** a **Popis** profilu ochrany koncových bodů.

4. V rozevíracím seznamu **Platforma** vyberte platformu zařízení, u které chcete vlastní nastavení použít. V současné době můžete pro nastavení omezení zařízení zvolit jednu z těchto platforem:

   - **macOS**
   - **Windows 10 a novější**

5. V rozevíracím seznamu **Typ profilu** zvolte **Ochrana koncového bodu**.

6. Nastavení, která můžete konfigurovat, se liší podle zvolené platformy. Viz:

   - [Nastavení macOS](endpoint-protection-macos.md)
   - [Nastavení Windows 10](endpoint-protection-windows-10.md)

7. Až nakonfigurujete příslušná nastavení, vyberte **vytvořit** na stránce **vytvořit profil** .

   Profil se vytvoří a zobrazí se na stránce se seznamem profilů. Pokud chcete přiřadit tento profil ke skupinám, podívejte se na téma [Přiřazení profilů zařízení](../configuration/device-profile-assign.md).

## <a name="add-custom-firewall-rules-for-windows-10-devices"></a>Přidání vlastních pravidel brány firewall pro zařízení s Windows 10

Když nakonfigurujete firewall v programu Microsoft Defender jako součást profilu, který zahrnuje pravidla ochrany koncových bodů pro Windows 10, můžete nakonfigurovat vlastní pravidla pro brány firewall. Vlastní pravidla umožňují rozšíření na předem definovanou sadu pravidel brány firewall, která jsou podporovaná pro Windows 10.

Při plánování profilů s vlastními pravidly brány firewall Vezměte v úvahu následující informace, které by mohly ovlivnit způsob seskupení pravidel brány firewall ve vašich profilech:

- Každý profil podporuje až 150 pravidel brány firewall. Když použijete víc než 150 pravidel, vytvořte další profily, z nichž každá je omezená na pravidla 150.

- Pokud se u každého profilu nepovede použít jedno pravidlo, všechna pravidla v tomto profilu se nezdařila a v zařízení se nepoužijí žádná pravidla.

- Pokud se pravidlo nepovede použít, všechna pravidla v profilu se nahlásí jako neúspěšná. Intune nemůže zjistit, které individuální pravidlo selhalo.  

Pravidla brány firewall, která může Intune spravovat, jsou podrobně popsaná v části [poskytovatel konfiguračních služeb brány Windows Firewall]( https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) (CSP). Seznam vlastních nastavení brány firewall pro zařízení s Windows 10, která Intune podporuje, najdete v tématu [vlastní pravidla brány firewall](endpoint-protection-windows-10.md#firewall-rules).

### <a name="to-add-custom-firewall-rules-to-an-endpoint-protection-profile"></a>Přidání vlastních pravidel brány firewall do profilu Endpoint Protection

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.

3. V části *platforma*vyberte **Windows 10 a novější**a potom jako *typ profilu* vyberte **Endpoint Protection**.

4. Výběrem **firewallu v programu Microsoft Defender** otevřete stránku konfigurace a potom pro *pravidla brány firewall* vyberte **Přidat** a otevřete stránku **vytvořit pravidlo** .

5. Zadejte nastavení pro pravidlo brány firewall a pak ho uložte kliknutím na **tlačítko OK** . Pokud chcete zkontrolovat dostupné vlastní možnosti pravidla brány firewall v dokumentaci, přečtěte si téma [vlastní pravidla brány firewall](endpoint-protection-windows-10.md#firewall-rules).

6. Po uložení se pravidlo zobrazí na stránce *firewall v programu Microsoft Defender* v seznamu pravidel.

7. Chcete-li upravit pravidlo, vyberte pravidlo ze seznamu a otevřete stránku **Upravit pravidlo** .

8. Pokud chcete pravidlo z profilu odstranit, vyberte pro pravidlo tři tečky **(...)** a pak vyberte **Odstranit**.

9. Pokud chcete změnit pořadí, v jakém jsou pravidla zobrazená, vyberte v horní části seznamu pravidel ikonu šipky *nahoru a šipka dolů* .

## <a name="next-steps"></a>Další kroky

Pokud chcete profil přiřadit ke skupinám, podívejte se na téma [Přiřazení profilů zařízení](../configuration/device-profile-assign.md).
