---
title: Zásady připojení tenanta – nasazení ochrany koncového bodu zabezpečení Endpoint v centru pro správu Microsoft Endpoint Manageru (Preview)
titleSuffix: Configuration Manager
description: " Vytvořte a nasaďte zásady antivirové ochrany v programu Microsoft Defender z konzoly Microsoft Endpoint Manageru a pro Configuration Manager kolekce."
ms.date: 08/24/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 07379821-02b3-4c61-af03-329c782e10d6
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 214a1ebc6b943edac194f27ee4aa539001026aaf
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194208"
---
# <a name="tenant-attach-create-and-deploy-endpoint-security-antivirus-policy-from-the-admin-center-preview"></a><a name="bkmk_atp"></a> Připojení tenanta: vytvoření a nasazení zásady ochrany koncového bodu Endpoint Security z centra pro správu (Preview)
<!--5691658-->
*Platí pro: Configuration Manager (Current Branch)*

> [!Important]
> Tyto informace se vztahují k funkci ve verzi Preview, která se podstatně změnila předtím, než se komerční verze uvolní. Microsoft neposkytuje žádné záruky, výslovné ani předpokládané, týkající se zde uváděných informací. 

Microsoft Endpoint Manager je integrované řešení pro správu všech vašich zařízení. Společnost Microsoft spojuje Configuration Manager a Intune s jednou konzolou s názvem **Centrum pro správu Microsoft Endpoint Manager**. Vytvořte zásady antivirové ochrany v programu Microsoft Defender v konzole Microsoft Endpoint Manager a nasaďte je do kolekcí Configuration Manager.


## <a name="prerequisites"></a>Předpoklady

- Přístup k [centru pro správu služby Microsoft Endpoint Manager](https://endpoint.microsoft.com/).
- Licence E5 pro [ATP v programu Microsoft Defender](/windows/security/threat-protection/microsoft-defender-atp/minimum-requirements#licensing-requirements).
- Prostředí, které je [klientovi připojené k nahraným zařízením](device-sync-actions.md).
- Minimálně verze Configuration Manager 2006 a odpovídající verze nainstalované konzoly.
   - Upgradujte cílová zařízení na nejnovější verzi klienta Configuration Manager.
- Alespoň jedna kolekce Configuration Manager, která je [k dispozici pro přiřazení zásad zabezpečení koncového bodu](atp-onboard.md#bkmk_collections)

## <a name="supported-antivirus-profile-for-tenant-attached-devices"></a>Podporovaný profil antivirového programu pro zařízení připojená klientovi

[!INCLUDE [Profiles for Configuration Manager tenant attached devices](../../intune/protect/includes/configmgr-antivirus-profiles.md)]

## <a name="assign-antivirus-policies-to-a-collection"></a>Přiřazení zásad antivirové ochrany ke kolekci

1. V prohlížeči, přejít na [https://aka.ms/MDAVTenantAttachPreview](https://aka.ms/MDAVTenantAttachPreview) .
1. Vyberte **Endpoint Security** a pak **Antivirus**.
1. Vyberte **vytvořit zásadu**.
1. Pro **platformu**vyberte **Windows 10 a Windows Server (nástroj ConfigMgr)**.
1. Pro **profil**vyberte možnost **antivirová ochrana v programu Microsoft Defender (Preview)** a pak **vytvořit**.
1. Přiřaďte **název** a volitelně také **Popis** na stránce **základy** .
1. Na stránce **nastavení konfigurace** nakonfigurujte nastavení, které chcete spravovat pomocí tohoto profilu. Po dokončení konfigurace nastavení vyberte **Další**. Další informace o dostupných zásadách najdete v tématu [nastavení zásad antivirové ochrany pro zařízení připojená k tenantovi](../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json).
1. Přiřaďte zásadu ke kolekci Configuration Manager na stránce **přiřazení** .

## <a name="next-steps"></a>Další kroky

[Nastavení zásad antivirové ochrany pro zařízení připojená klientovi](../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json)