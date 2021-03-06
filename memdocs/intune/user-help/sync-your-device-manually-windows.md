---
title: Ruční synchronizace zařízení s Windows | Dokumentace Microsoftu
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/20/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: priyar
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: ba2f9d2e3f9e89d37b1dc8361cd80451155a6869
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820676"
---
# <a name="sync-your-windows-device-manually"></a>Ruční synchronizace zařízení s Windows

Když je rychlost instalace aplikace menší než ideální, Iniciujte ruční synchronizaci zařízení. Ruční synchronizace vynutí, aby se zařízení připojilo k Intune o nejnovější aktualizace a komunikaci. Po dokončení synchronizace zařízení se může rychlost instalace zvýšit.

Intune podporuje ruční synchronizaci z aplikace Portál společnosti, z hlavního panelu plochy, nabídky Start a z aplikace Nastavení zařízení. Funkce aplikace Portál společnosti se podporuje v zařízeních se systémem Windows 10 Creators Update (1703) nebo novějším. 

Všechna zařízení s Windows, včetně následujících, se dají synchronizovat z aplikace Nastavení v zařízení:

* [Stolní počítač s Windows 10](#windows-10-desktop)  
* [Microsoft HoloLens](#microsoft-hololens)   

## <a name="sync-directly-from-company-portal-app-for-windows"></a>Přímá synchronizace z aplikace Portál společnosti pro Windows
Tento postup proveďte, pokud chcete ručně synchronizovat všechna zařízení s Windows 10, na kterých běží aktualizace autora (verze 1709) nebo novější.

1. Na svém zařízení otevřete aplikaci Portál společnosti.

2. Vyberte **Nastavení**  >  **synchronizace**.

    ![Snímek obrazovky s domovskou stránkou aplikace Portál společnosti a zvýrazněnou možností Nastavení](./media/RS1_homePage_settings_04.png)  
    
    ![Snímek obrazovky stránky nastavení v aplikaci Portál společnosti a zvýrazněným tlačítkem Synchronizovat](./media/RS1_settingspage_sync05.png)  

## <a name="sync-from-device-taskbar-or-start-menu"></a>Synchronizace z hlavního panelu zařízení nebo z nabídky Start   

K řízení synchronizace se dá dostat také mimo aplikaci, z plochy vašeho zařízení. To se hodí, pokud máte aplikaci připnutou přímo na hlavním panelu nebo v nabídce Start a chcete synchronizovat rychle.  

1. Ikonu aplikace Portál společnosti najdete na hlavním panelu nebo v nabídce Start.  
2. Když na ni kliknete pravým tlačítkem, zobrazí se její nabídka (říká se jí také seznam odkazů).  

    ![Snímek obrazovky s hlavním panelem Windows na ploše zařízení. Byla vybrána ikona aplikace Portál společnosti a zobrazí se nabídka s možnostmi připnout na hlavní panel, zavřít okno a synchronizovat toto zařízení.](./media/sync-device-from-start-menu-1807.png)  

3. Vyberte **Synchronizovat toto zařízení**. V aplikaci Portál společnosti se otevře stránka **Nastavení** a zahájí se synchronizace.  

## <a name="sync-from-settings-app"></a>Synchronizace z aplikace Nastavení 
Pomocí těchto kroků ručně synchronizujete zařízení Microsoft HoloLens a Windows 10 Desktop z aplikace nastavení.  

### <a name="windows-10-desktop"></a>Stolní počítač s Windows 10
1. V zařízení vyberte **Spustit**  >  **Nastavení**.

2. Vyberte **Účty**.

    ![Volba možnosti Účty na obrazovce Nastavení](./media/win10pc-sync-2-settings-accounts.png)  

3. Pro stolní počítače existuje více verzí systému Windows 10. Porovnejte svoji obrazovku se snímky obrazovky níže a zjistěte, který postup máte provést. 

    * Pokud na své obrazovce vidíte **Přístup do práce nebo do školy**, pokračujte kroky v části [Přístup do práce nebo do školy](#access-work-or-school-steps).

    ![Možnost Přístup do práce nebo do školy v aplikaci Nastavení](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

    * Pokud na své obrazovce vidíte **Přístup do práce**, pokračujte kroky v části [Přístup do práce](#work-access-steps).  

    ![Volba účtu typu Přístup do práce](./media/win10pc-sync-3-work-access.png)

### <a name="microsoft-hololens"></a>Microsoft HoloLens  
Tyto pokyny platí pro zařízení HoloLens se systémem Windows 10 Anniversary Update (označovaným také jako RS1).  

1. Otevřete na svém zařízení aplikaci Nastavení.  

2. Vyberte **účty**  >  **přístup do práce**.  

    ![Snímek obrazovky s aplikací Nastavení HoloLens a zvýrazněným odkazem Účty](./media/RS1_holoLens_SettingsRS1_Accounts_06.png)  

3. Vyberte připojený účet > **Synchronizovat**.  

    ![Snímek obrazovky s aplikací Nastavení HoloLens a zvýrazněným tlačítkem Synchronizovat](./media/RS1_holoLens_SyncRS1_Sync_08.png)   

#### <a name="access-work-or-school-steps"></a>Postup pro Přístup do práce nebo do školy  

1. Vyberte možnost **přístup do práce nebo do školy**.

    ![Snímek obrazovky zobrazující možnost Přístup do práce nebo do školy](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

2. Vyberte účet, vedle kterého je ikona aktovky. Pokud takový účet nevidíte, je možné, že vaše společnost nakonfigurovala nastavení jiným způsobem. Místo toho vyberte účet, který má vedle něho logo Microsoftu.

     ![Volba názvu účtu vedle aktovky nebo loga Microsoftu](./media/win10pc-rs1-sync-info-button.png)

3. Vyberte **informace**. 

4. Vyberte **Synchronizovat**. 

#### <a name="work-access-steps"></a>Postup pro Přístup do práce

1. Vyberte **Přístup do práce**.

    ![Volba účtu typu Přístup do práce](./media/win10pc-sync-3-work-access.png)

2. V části **Zaregistrovat se k správě zařízení** zvolte název své společnosti.

    ![Volba názvu firmy pro správu zařízení](./media/win10pc-sync-4-tap-com-name.png)

3. Vyberte **synchronizovat**. Tlačítko zůstane zakázané, dokud se synchronizace nedokončí.

    ![Volba tlačítka Synchronizovat](./media/win10pc-sync-5-tap-sync.png)  
    
## <a name="next-steps"></a>Další kroky  

Potřebujete ještě další pomoc? Obraťte se na podporu ve vaší společnosti. Kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).
