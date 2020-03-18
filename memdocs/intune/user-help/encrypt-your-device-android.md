---
title: Zašifrovat zařízení s Androidem pro Intune | Microsoft Docs
description: Postup zapnutí šifrování zařízení s Androidem v případě potřeby službou Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/19/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: ee2d220e308b406251f049e1c17422f89ee36534
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79328307"
---
# <a name="encrypting-your-android-device"></a>Šifrování zařízení s Androidem

Šifrování zařízení chrání soubory a složky před neoprávněným přístupem v případě ztráty nebo odcizení zařízení. Když zapnete šifrování zařízení, přihlaste se k zařízení jenom jednotlivcům se správným heslem nebo PIN kódem. 

Než budete moct získat přístup k školním nebo pracovním prostředkům, může vaše organizace vyžadovat, abyste svoje zařízení s Androidem zašifroval. Některá novější zařízení s Androidem jsou ve výchozím nastavení zašifrována.  

## <a name="turn-on-encryption"></a>Zapnout šifrování

Pokud Portál společnosti nebo aplikace Microsoft Intune vyzve k zašifrování zařízení, proveďte následující kroky. 

> [!Note]
> Některá zařízení s Androidem z Huawei, vivo a OPPO se nedají šifrovat. Další informace najdete [tady](your-device-appears-encrypted-but-cp-says-otherwise-android.md).  

1. Nastavte zámek obrazovky zařízení.  
    a. Přejít na **nastavení** > **zamykací obrazovka a zabezpečení** > **Typ zámku obrazovky**.  
    b. Vyberte možnost **připnout**, **heslo**nebo **vzor**.  
    c. Při konfiguraci zámku obrazovky postupujte podle pokynů na obrazovce.  

2. Vraťte se na **zamykací obrazovku a zabezpečení** a vyberte **zabezpečené spuštění**.
3. Vyberte **vyžadovat připnutí, když se zařízení zapne** > **OK**.
4. Zadejte svůj PIN kód a potvrďte a Zašifrujte své zařízení.
5. Otevřete Portál společnosti nebo Microsoft Intune aplikaci.
    * Portál společnosti uživatelé: Vyberte zařízení a klepněte na **kontrolovat nastavení zařízení**. 
    * Microsoft Intune uživatelé: budete muset počkat, dokud se stránka neaktualizuje, ale v případě, že se váš stav šifrování změní na kompatibilní.  

Zařízení se systémem Android 4,4 a starším nemusí mít možnost **zabezpečeného spuštění** . V takovém případě proveďte následující kroky k zašifrování zařízení.

1. Přejít na **nastavení** > **zabezpečení** > **šifrování zařízení**. Mezi zařízeními s Androidem se liší popisky na obrazovce. Pokud nevidíte možnost **Šifrovat zařízení** , vraťte se změnami:
    * **Šifrování** **úložiště > úložiště**
    * **Úložiště** > **zamykací obrazovce a zabezpečení** > **Další nastavení zabezpečení** 

2. Postupujte podle pokynů na obrazovce. Během šifrování se zařízení může několikrát restartovat.
3. Otevřete Portál společnosti nebo Microsoft Intune aplikaci.
    * Portál společnosti uživatelé: Vyberte zařízení a klepněte na **kontrolovat nastavení zařízení**.  
    * Microsoft Intune uživatelé: budete muset počkat, dokud se stránka neaktualizuje, ale v případě, že se váš stav šifrování změní na kompatibilní.

## <a name="troubleshoot"></a>Řešení problémů  
**Problém**: zařízení jste už zašifrovali a

- Tlačítko pro šifrování je zakázané.
- Zobrazí se zpráva s informacemi o tom, že je stále nutné nastavit šifrování.
- Při pokusu o použití aplikace Portál společnosti nebo Microsoft Intune se zobrazí chyby.

**Možná řešení**

- Ujistěte se, že je zařízení nabité a připojené k nabíječce.  
- Zkontrolujte, že jste na zařízení nastavili PIN kód nebo heslo.  

Potřebujete ještě další pomoc? Obraťte se na svou firemní podporu (kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980)) nebo napište <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">týmu Microsoft Android</a>.  
