---
title: Šifrování zařízení s Androidem – Microsoft Intune | Microsoft Docs
description: Zjistěte, jak v případě potřeby v Intune zapnout šifrování zařízení s Androidem.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/22/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d4430e92-04cc-48e9-a77a-81b95a90b6b3
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 98950a6907db0ac6869b55ae26718a2919048154
ms.sourcegitcommit: fdd6d3c4b906e895ebec2856ebc38b0656296d2c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "91002643"
---
# <a name="encrypting-your-android-device"></a>Šifrování zařízení s Androidem

Šifrování zařízení chrání soubory a složky před neoprávněným přístupem v případě ztráty nebo odcizení zařízení. Data jsou nepřístupná a nečitelná pro uživatele, kteří nemají heslo. 

Než budete moct přistupovat do školních nebo pracovních prostředků, vaše organizace může vyžadovat:

* [Zašifrování zařízení](#encrypt-device)
* [Povolit zabezpečené spuštění](#enable-secure-startup)
* [Nastavení spouštěcího hesla, kódu PIN nebo jiné metody ověřování](#set-startup-passcode)  

> [!Note]
> Některá zařízení s Androidem z Huawei, vivo a OPPO se nedají šifrovat. Další informace najdete v tématu [šifrování zařízení, ale aplikace říká jinak](your-device-appears-encrypted-but-cp-says-otherwise-android.md).  

## <a name="encrypt-device"></a>Šifrovat zařízení

Pomocí těchto kroků Zašifrujte své zařízení. Vaše zařízení se může několikrát restartovat. Název a umístění možnosti šifrování se budou lišit v závislosti na výrobci zařízení a verzi Androidu. 

1. Otevřete aplikaci **Nastavení**.
2. V panelu hledání zadejte **zabezpečení** nebo **Zašifrujte** , chcete-li najít související nastavení.  
3. Klepněte na možnost k zašifrování zařízení. Postupujte podle pokynů na obrazovce.  
4. Po zobrazení výzvy nastavte heslo zamykací obrazovky, kód PIN nebo jinou metodu ověřování (pokud to vaše organizace dovoluje). 
5. Chcete-li znovu kontrolovat nastavení, otevřete Portál společnosti nebo Microsoft Intune aplikaci.
    * Portál společnosti uživatelé: Vyberte zařízení a klepněte na **kontrolovat nastavení zařízení**. 
    * Microsoft Intune uživatelé: budete muset počkat, dokud se stránka neaktualizuje, ale v případě, že se váš stav šifrování změní na kompatibilní. 

## <a name="enable-secure-startup"></a>Povolit zabezpečené spuštění

Vaše organizace může vyžadovat, abyste povolili *Zabezpečené spouštění*. Zabezpečené spuštění chrání vaše zařízení tím, že při každém zapnutí zařízení vyžaduje heslo nebo kód PIN. V závislosti na tom, co vaše organizace povoluje, můžou být k dispozici další možnosti ověřování, které můžete použít. 

Název a umístění možnosti zabezpečeného spuštění se budou lišit také v závislosti na výrobci zařízení a verzi Androidu. V některých zařízeních se toto nastavení nazývá **silná ochrana**. 

1. Otevřete aplikaci **Nastavení**.
2. Zadejte **zabezpečené spuštění** na panelu hledání aplikace.
3. Klepněte na **zabezpečené spuštění**  >  **vyžadovat při zapnutí zařízení PIN kód**.
4. Po zobrazení výzvy zadejte PIN kód zařízení.   
5. Chcete-li znovu kontrolovat nastavení, otevřete Portál společnosti nebo Microsoft Intune aplikaci.
    * Portál společnosti uživatelé: Vyberte zařízení a klepněte na **kontrolovat nastavení zařízení**. 
    * Microsoft Intune uživatelé: budete muset počkat, dokud se stránka neaktualizuje, ale v případě, že se váš stav šifrování změní na kompatibilní.  


## <a name="set-startup-passcode"></a>Nastavit spouštěcí heslo   
Po zašifrování zařízení a zapnutí zabezpečeného spuštění se zobrazí výzva k nastavení kódu PIN, hesla nebo jiné metody ověřování (pokud to vaše organizace dovoluje). Konkurenční krok bude vyhovovat požadavku na spouštěcí heslo. 

Chcete-li na zařízení nastavit zamykací obrazovku nebo změnit typ, který aktuálně používáte:  

1. Otevřete aplikaci **Nastavení**.
2. Na panelu hledání aplikace zadejte **Zámek obrazovky** .
3. Klepněte na **Typ zámku obrazovky**.
4. Klepněte na typ zámku obrazovky, který chcete použít, a postupujte podle pokynů na obrazovce.  

## <a name="troubleshoot"></a>Řešení potíží    
**Problém**: tlačítko šifrování je zakázané.   

**Můžete vyzkoušet**: 
* Ujistěte se, že je zařízení plně účtované a připojené. Šifrování může chvíli trvat a vyžaduje plnou baterii.   

**Problém**: zobrazí se zpráva oznamující, že pořád potřebujete šifrovat vaše zařízení.  

**Možná řešení**:
   *  Nastavte na svém zařízení [zamykací obrazovku](#set-startup-passcode) . 
   * [Povolit zabezpečené spuštění](#enable-secure-startup).

Potřebujete ještě další pomoc? Obraťte se na firemní podporu (kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980)) nebo napište <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having trouble with encryption on my Android device&body=Describe the issue you're experiencing here.">týmu Microsoft Android</a>.  
