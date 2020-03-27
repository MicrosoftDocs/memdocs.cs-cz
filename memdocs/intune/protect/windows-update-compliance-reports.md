---
title: Použití sestav Update Compliance pro aktualizace Windows v Microsoft Intune
titleSuffix: Microsoft Intune
description: Pomocí OMS Update Compliance můžete zobrazit data sestavy pro aktualizace Windows, které nasazujete v Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/25/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7ad666f21b2ff271b99675486835357dfd071773
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80326505"
---
# <a name="intune-compliance-reports-for-updates"></a>Sestavy dodržování předpisů v Intune pro aktualizace

Když použijete Intune k nasazení služby Windows Update na zařízení s Windows 10, zobrazí se podrobnosti o kompatibilitě aktualizací pomocí Intune nebo bezplatného řešení s názvem *Update Compliance*, které je součástí Microsoft Operations Management Suite (OMS).

## <a name="use-intune"></a>Použití Intune

Chcete-li zkontrolovat sestavu zásad pro stav nasazení pro aktualizační kanály Windows 10, které jste nakonfigurovali:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení** > **Přehled** > **stav aktualizace softwaru**. Uvidíte obecné informace o stavu všech aktualizačních kanálů, které jste přiřadili.

3. Pokud chcete zobrazit další podrobnosti, vyberte **monitorovat**. Potom v části **aktualizace softwaru**vyberte **stav nasazení s kroužkem aktualizace** a zvolte aktualizační kanál nasazení, který chcete zkontrolovat.

   Pokud chcete zobrazit podrobnější informace o aktualizačním kanálu, v sekci **Monitorování** zvolte z těchto sestav:

   - **Stav zařízení**– zobrazí se stav konfigurace zařízení. Podrobnosti najdete v článku o [aktualizaci deviceConfigurationDeviceStatus]( https://docs.microsoft.com/graph/api/intune-deviceconfig-deviceconfigurationdevicestatus-update?view=graph-rest-1.0).

   - **Stav uživatele**– zobrazí se informace o uživatelském jménu, stavu a poslední sestavě, podrobnosti najdete v [seznamu deviceConfigurationUserStatuses](https://docs.microsoft.com/graph/api/intune-deviceconfig-deviceconfigurationuserstatus-list?view=graph-rest-1.0).

   - **Stav aktualizace koncového uživatele**– tím se zobrazí stav aktualizace zařízení se systémem Windows. Podrobnosti najdete v tématu [windowsUpdateState](https://docs.microsoft.com/graph/api/resources/intune-shared-windowsupdatestate?view=graph-rest-beta).

## <a name="use-update-compliance"></a>Použít Update Compliance

Uvádění Windows 10 Update můžete monitorovat pomocí [Update Compliance](https://technet.microsoft.com/itpro/windows/manage/update-compliance-monitor)a řešení Windows Analytics. Update Compliance k dispozici prostřednictvím Azure Portal a jsou dostupné zdarma pro zařízení, která splňují [požadavky](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started#update-compliance-prerequisites).  

Když použijete toto řešení, nasadíte komerční ID do libovolného zařízení s Windows 10 spravovaných pomocí Intune, pro které chcete ohlásit dodržování předpisů pro aktualizace.  

V Intune můžete ke konfiguraci komerčního ID použít nastavení OMA-URI vlastní zásady. Viz [použití vlastních nastavení pro zařízení s Windows 10 v Intune](../configuration/custom-settings-windows-10.md).

Cesta OMA-URI (s rozlišováním velkých a malých písmen) pro konfiguraci komerčního ID je: *./VENDOR/MSFT/DMCLIENT/Provider/MS DM Server/CommercialID*  

V nastavení **Přidat nebo upravit nastavení OMA-URI** můžete použít třeba následující hodnoty:

- **Název nastavení**: Komerční ID pro analýzu Windows
- **Popis nastavení**: Konfigurace komerčního ID pro řešení pro analýzu Windows
- **OMA-URI** (rozlišuje velká a malá písmena): *./Vendor/MSFT/DMClient/Provider/MS DM Server/CommercialID*
- **Datový typ:** Řetězec
- **Hodnota**: \<použít identifikátor GUID zobrazený na kartě telemetrie Windows v pracovním prostoru OMS >

> [!NOTE]
> Podrobnosti o MS DM Serveru najdete v tématu [Poskytovatel konfiguračních služeb DMClient]( https://docs.microsoft.com/windows/client-management/mdm/dmclient-csp).

## <a name="next-steps"></a>Další kroky

[Správa softwarových aktualizací v Intune](windows-update-for-business-configure.md)
