---
title: Připojení tenanta – připojení Configuration Manager klientů k ochraně ATP v programu Microsoft Defender z centra pro správu Microsoft Endpoint Manageru (Preview)
titleSuffix: Configuration Manager
description: Nasaďte zásady registrace a odezvy (EDR) služby Microsoft Defender ATP pro Configuration Manager spravovaných klientů z centra pro správu.
ms.date: 08/24/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 50f8e206-a2af-469a-9f1b-0f7a87166f48
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: a2862812145e33a992ceaa346e138606eee5fad0
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194215"
---
# <a name="tenant-attach-onboard-configuration-manager-clients-to-microsoft-defender-atp-from-the-admin-center-preview"></a><a name="bkmk_atp"></a> Připojení tenanta: zprovoznění klientů Configuration Manager do služby Microsoft Defender ATP z centra pro správu (Preview)
<!--5691658-->
*Platí pro: Configuration Manager (Current Branch)*

> [!Important]
> Tyto informace se vztahují k funkci ve verzi Preview, která se podstatně změnila předtím, než se komerční verze uvolní. Microsoft neposkytuje žádné záruky, výslovné ani předpokládané, týkající se zde uváděných informací.

Microsoft Endpoint Manager je integrované řešení pro správu všech vašich zařízení. Společnost Microsoft spojuje Configuration Manager a Intune s jednou konzolou s názvem **Centrum pro správu Microsoft Endpoint Manager**. Můžete nasadit zásady registrace koncových bodů (EDR) v programu Microsoft Defender ATP pro Configuration Manager spravované klienty. Tito klienti nevyžadují registraci v Azure AD ani MDM a zásady jsou zaměřené na kolekce nástroje ConfigMgr místo skupin Azure AD.

## <a name="prerequisites"></a>Předpoklady

- Přístup k [centru pro správu služby Microsoft Endpoint Manager](https://endpoint.microsoft.com/).
- Licence E5 pro [ATP v programu Microsoft Defender](/windows/security/threat-protection/microsoft-defender-atp/minimum-requirements#licensing-requirements).
- Prostředí, které je [klientovi připojené k nahraným zařízením](device-sync-actions.md).
- Minimálně verze Configuration Manager 2006 a odpovídající verze nainstalované konzoly.
   - Upgradujte cílová zařízení na nejnovější verzi klienta Configuration Manager.

## <a name="make-configuration-manager-collections-available-to-assign-endpoint-security-policies"></a><a name="bkmk_collections"></a> Nastavit kolekce Configuration Manager k dispozici pro přiřazení zásad zabezpečení koncového bodu

Když povolíte shromažďování zařízení pro práci se zásadami zabezpečení koncového bodu služby Intune, konfigurujete zařízení v těchto kolekcích tak, aby se připojila ke službě Microsoft Defender ATP.

[!INCLUDE [Enable endpoint security policies for a Configuration Manager collection](../../intune/protect/includes/make-configmgr-collection-available-edr.md)]

## <a name="create-microsoft-defender-atp-endpoint-detection-and-response-edr-onboarding-policies"></a><a name="bkmk_onboard"></a> Vytvoření zásad registrace a odezvy pro zjišťování koncových bodů služby Microsoft Defender ATP (EDR)

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://endpoint.microsoft.com).

1. Vyberte zásady zjišťování koncových bodů **zabezpečení koncového bodu**  >  **a odpověď**  >  **vytvořit**.

1. Pro zásady vyberte tuto platformu a profil:

   - Platforma: **Windows 10 a Windows Server (ConfigMgr)**
   - Profil: **detekce a odpověď koncového bodu (ConfigMgr)**

1. Vyberte **Create** (Vytvořit).

1. Na stránce **základy** zadejte název a popis profilu a pak klikněte na tlačítko **Další**.

1. Na stránce **nastavení konfigurace** nakonfigurujte nastavení, které chcete spravovat pomocí tohoto profilu. Balíček pro registraci je automaticky zahrnutý a není to, co můžete konfigurovat.

   Po dokončení konfigurace nastavení vyberte **Další**.

1. Na stránce **přiřazení** vyberte kolekce, které tyto zásady dostanou. Vyberte kolekce z Configuration Manager, které jste synchronizoval s centrem pro správu Microsoft Endpoint Manageru a jsou povolené pro zásady ochrany ATP v programu Microsoft Defender.

   V tuto chvíli se můžete rozhodnout nepřiřazovat kolekce a později zásadu upravit a přidat přiřazení.

   Až budete připraveni pokračovat, vyberte **Další**.

1. Po dokončení na stránce **Revize + vytvořit** klikněte na **vytvořit**.

   Nový profil se zobrazí v seznamu, když vyberete typ zásady pro profil, který jste vytvořili.

## <a name="next-steps"></a>Další kroky

[Vytvoření a nasazení zásad ochrany koncového bodu zabezpečení Endpoint na zařízení připojená klientovi](deploy-antivirus-policy.md)