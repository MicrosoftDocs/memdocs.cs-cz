---
author: brenduns
ms.author: brenduns
ms.service: microsoft-intune
ms.subservice: protect
ms.topic: include
ms.date: 08/24/2020
ms.openlocfilehash: 01179c35274ff14d4a91283e9a38aa5e6fee8e03
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/25/2020
ms.locfileid: "88823430"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
1. Z konzoly Configuration Manager připojené k lokalitě nejvyšší úrovně klikněte pravým tlačítkem na kolekci zařízení, kterou synchronizujete do centra pro správu Microsoft Endpoint Manageru, a vyberte **vlastnosti**.

2. Na kartě **synchronizace cloudu** povolte možnost **nastavit tuto kolekci tak, aby bylo možné přiřadit zásady zabezpečení koncového bodu z centra pro správu Microsoft Endpoint Manageru**.

   - Tuto možnost nemůžete vybrat, pokud Configuration Manager hierarchie není připojená ke klientovi.
   - Kolekce, které jsou k dispozici pro tuto možnost, jsou omezeny [oborem kolekce vybraným pro nahrání připojení klienta](../../../configmgr/tenant-attach/device-sync-actions.md#bkmk_edit). <!--CM7423168-->
  
   ![Konfigurace synchronizace cloudu](../media/tenant-attach-intune/cloud-sync.png)

3. Kliknutím na **OK** uložte konfiguraci.

   Zařízení v této kolekci se teď mohou integrovat s Microsoft Defender ATP a podporovat používání zásad zabezpečení koncového bodu Intune.
