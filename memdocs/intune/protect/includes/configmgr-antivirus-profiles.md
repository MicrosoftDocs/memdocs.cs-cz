---
author: brenduns
ms.author: brenduns
ms.service: microsoft-intune
ms.subservice: protect
ms.topic: include
ms.date: 08/24/2020
ms.openlocfilehash: ff48e8117437e45be42551ebffff7cdcf5bce184
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820289"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
Pro zařízení, která spravujete pomocí Configuration Manager aktuální větev 2006 nebo novější, se v rámci scénáře připojení tenanta podporují tyto profily:
<!--The following profiles are supported for devices you manage with Configuration Manager Technical Preview 2007 or later, through the tenant attach scenario:-->

- Platforma: **Windows 10 a Windows Server**

  - Profil: **zásada antivirové ochrany v programu Microsoft Defender (nástroj ConfigMgr)**
  
    Spravujte [nastavení zásad antivirového programu pro zařízení Configuration Manager](../../protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md), když použijete možnost připojit klienta.

    Tento profil se podporuje u zařízení, která jsou připojená k tenantovi, a spouští tyto platformy:
    - Windows 10 a novější (x86, x64, ARM64)
    - Windows 8.1 (počítačích x64, x64)
    - Windows Server 2019 a novější (x64)
    - Windows Server 2016 (x64)
    - Windows Server 2012 R2 (x64)
    - Windows Server 2008 R2 SP1 (x64)
