---
title: Konfigurace nastavení ochrany koncových bodů v Microsoft Intune – Azure | Microsoft Docs
description: Nastavení ochrany koncových bodů určete při vytváření profilu zařízení s macOS nebo Windows 10 v Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2020
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
ms.openlocfilehash: 6b5d0f88222c8d48da4f91ff3cf8d4628ccb179d
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/02/2020
ms.locfileid: "80551579"
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

> [!NOTE]
> Uživatelské rozhraní (UI) Intune se aktualizuje na celé obrazovce a může trvat několik týdnů. Až do chvíle, kdy váš tenant obdrží tuto aktualizaci, budete mít při vytváření nebo úpravách nastavení popsaných v tomto článku mírně odlišný pracovní postup.

## <a name="create-a-device-profile-containing-endpoint-protection-settings"></a>Vytvoření profilu zařízení obsahujícího nastavení ochrany koncových bodů

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.

3. Zadejte následující vlastnosti:

    - **Platforma**: vyberte platformu zařízení. Možnosti:

        - **macOS**
        - **Windows 10 a novější**

    - **Profil**: vyberte **Endpoint Protection**.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název zásady. Své zásady pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem zásad je například **MacOS: Endpoint Protection profil, který konfiguruje bránu firewall pro všechna zařízení MacOS**.
    - **Popis**: zadejte popis zásady. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.

7. Nastavení, která můžete konfigurovat v **nastavení konfigurace**, se liší v závislosti na zvolené platformě. Pro podrobnější nastavení vyberte platformu:

   - [Nastavení macOS](endpoint-protection-macos.md)
   - [Nastavení Windows 10](endpoint-protection-windows-10.md)

8. Vyberte **Další**.
9. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu na konkrétní skupiny IT, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment`. Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](../fundamentals/scope-tags.md).

    Vyberte **Další**.

10. V části **přiřazení**vyberte uživatele nebo skupiny, které obdrží váš profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](../configuration/device-profile-assign.md).

    Vyberte **Další**.

11. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

## <a name="add-custom-firewall-rules-for-windows-10-devices"></a>Přidání vlastních pravidel brány firewall pro zařízení s Windows 10

Když nakonfigurujete firewall v programu Microsoft Defender jako součást profilu, který zahrnuje pravidla ochrany koncových bodů pro Windows 10, můžete nakonfigurovat vlastní pravidla pro brány firewall. Vlastní pravidla umožňují rozšíření na předem definovanou sadu pravidel brány firewall, která jsou podporovaná pro Windows 10.

Při plánování profilů s vlastními pravidly brány firewall Vezměte v úvahu následující informace, které by mohly ovlivnit způsob seskupení pravidel brány firewall ve vašich profilech:

- Každý profil podporuje až 150 pravidel brány firewall. Když použijete víc než 150 pravidel, vytvořte další profily, z nichž každá je omezená na pravidla 150.

- Pokud se u každého profilu nepovede použít jedno pravidlo, všechna pravidla v tomto profilu se nezdařila a v zařízení se nepoužijí žádná pravidla.

- Pokud se pravidlo nepovede použít, všechna pravidla v profilu se nahlásí jako neúspěšná. Intune nemůže zjistit, které individuální pravidlo selhalo.  

Pravidla brány firewall, která může Intune spravovat, jsou podrobně popsaná v části [poskytovatel konfiguračních služeb brány Windows Firewall](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) (CSP). Seznam vlastních nastavení brány firewall pro zařízení s Windows 10, která Intune podporuje, najdete v tématu [vlastní pravidla brány firewall](endpoint-protection-windows-10.md#firewall-rules).

### <a name="to-add-custom-firewall-rules-to-an-endpoint-protection-profile"></a>Přidání vlastních pravidel brány firewall do profilu Endpoint Protection

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.

3. V části *platforma*vyberte **Windows 10 a novější**a potom pro *profil* vyberte **Endpoint Protection**.

    Vyberte **Vytvořit**.

4. Zadejte **název** profilu > **Další**.
5. V **nastavení konfigurace**vyberte **firewall v programu Microsoft Defender**. Pro *pravidla brány firewall*vyberte **Přidat** a otevřete stránku **vytvořit pravidlo** .

6. Zadejte nastavení pro pravidlo brány firewall a pak ho uložte kliknutím na **tlačítko OK** . Pokud chcete zkontrolovat dostupné vlastní možnosti pravidla brány firewall v dokumentaci, přečtěte si téma [vlastní pravidla brány firewall](endpoint-protection-windows-10.md#firewall-rules).

    1. Pravidlo se zobrazí na stránce *firewall v programu Microsoft Defender* v seznamu pravidel.
    2. Chcete-li upravit pravidlo, vyberte pravidlo ze seznamu a otevřete stránku **Upravit pravidlo** .
    3. Pokud chcete pravidlo z profilu odstranit, vyberte pro pravidlo tři tečky **(...)** a pak vyberte **Odstranit**.
    4. Pokud chcete změnit pořadí, v jakém jsou pravidla zobrazená, vyberte v horní části seznamu pravidel ikonu šipky *nahoru a šipka dolů* .

7. Vyberte **Další** , dokud se nedostanete k **revizi + vytvoření**. Když vyberete **vytvořit**, změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

## <a name="next-steps"></a>Další kroky

Profil se vytvoří, ale nemusí ještě nic dělat. Dále [Přiřaďte profil](../configuration/device-profile-assign.md) a [sledujte jeho stav](../configuration/device-profile-monitor.md).
