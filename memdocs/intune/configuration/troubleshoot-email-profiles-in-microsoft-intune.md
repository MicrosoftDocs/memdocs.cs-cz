---
title: Řešení potíží s e-mailovými profily v Microsoft Intune – Azure | Microsoft Docs
description: V tématu běžné problémy a řešení se e-mailovými profily v Microsoft Intune, včetně duplicitních e-mailových profilů a chyb na zařízeních se Samsung KNOX standardem.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: f5c944ea-32a6-48af-bb57-16d5f1f3c588
ROBOTS: ''
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4d7e3b5b9a169baf336b0d4e7d8d66b06af38061
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332195"
---
# <a name="common-issues-and-resolutions-with-email-profiles-in-microsoft-intune"></a>Běžné problémy a řešení v e-mailových profilech v Microsoft Intune

Projděte si některé běžné problémy s e-mailovými profily a zjistěte, jak je řešit.

## <a name="what-you-need-to-know"></a>Co je potřeba vědět

- E-mailové profily se nasazují pro uživatele, který zařízení zaregistroval. Pokud chcete nakonfigurovat e-mailový profil, Intune v e-mailovém profilu uživatele během registrace používá vlastnosti Azure Active Directory (AD). [Přidání nastavení e-mailu do zařízení](email-settings-configure.md) může být dobrým prostředkem.
- V případě Androidu Enterprise nasaďte pomocí spravovaného Obchod Google Play Gmail nebo 9 pro práci. [Přidat spravované aplikace Google Play](../apps/apps-add-android-for-work.md) zobrazí seznam kroků.
- Microsoft Outlook pro iOS/iPadOS a Android nepodporují e-mailové profily. Místo toho Nasaďte zásadu konfigurace aplikace. Další informace najdete v tématu [nastavení konfigurace pro Outlook](../apps/app-configuration-policies-outlook.md).
- Do zařízení se nemusí doručovat e-mailové profily cílené na skupiny zařízení (ne skupiny uživatelů). Pokud má zařízení primárního uživatele, bude mít cílení na zařízení fungovat. Pokud e-mailový profil obsahuje uživatelské certifikáty, ujistěte se, že zacílíte na skupiny uživatelů.
- Uživatelům se zobrazí výzva k zadání hesla pro e-mailový profil. V tomto scénáři ověřte všechny certifikáty, na které se odkazuje v e-mailovém profilu. Pokud není jeden z certifikátů zaměřený na uživatele, pokusí se Intune znovu nasadit e-mailový profil.

## <a name="device-already-has-an-email-profile-installed"></a>Zařízení už má nainstalovaný e-mailový profil

Pokud uživatelé vytvoří e-mailový profil před registrací v Intune nebo Office 365 MDM, e-mailový profil nasazený službou Intune nemusí fungovat podle očekávání:

- **iOS/iPadOS**: Intune detekuje stávající duplicitní e-mailový profil na základě názvu hostitele a e-mailové adresy. Uživatelem vytvořený e-mailový profil zablokuje nasazení profilu vytvořeného v Intune. Toto je běžný problém, když uživatelé iOS/iPadOS obvykle vytvoří e-mailový profil a potom se zaregistrují. Portál společnosti aplikace uvádí, že uživatel není kompatibilní, a může uživateli požádat o odebrání e-mailového profilu.

  Uživatel by měl odebrat svůj e-mailový profil, aby bylo možné nasadit profil Intune. Pokud chcete tomuto problému zabránit, řekněte uživatelům, aby si zaregistrovali a povolili v Intune nasazení e-mailového profilu. Pak uživatelé můžou vytvořit svůj e-mailový profil.

- **Windows**: Intune detekuje stávající duplicitní e-mailový profil na základě názvu hostitele a e-mailové adresy. Intune přepíše existující e-mailový profil vytvořený uživatelem.

- **Samsung KNOX Standard**: Intune identifikuje duplicitní e-mailový účet na základě e-mailové adresy a přepíše ho profilem Intune. Pokud uživatel tento účet nakonfiguruje, profil Intune ho znovu přepíše. To může způsobit nejasnost uživatele, jehož konfigurace účtu bude přepsána.

Samsung KNOX nepoužívá k identifikaci profilu název hostitele. Doporučujeme nevytvářet více e-mailových profilů pro nasazení na stejné e-mailové adresy na různých hostitelích, protože se navzájem přepíší.

## <a name="error-0x87d1fde8-for-knox-standard-device"></a>Chyba 0x87D1FDE8 pro zařízení KNOX Standard

**Problém**: po vytvoření a nasazení e-mailového profilu Exchange Active Sync pro Samsung KNOX standard pro různá zařízení s Androidem **se neúspěšná** Chyba **0x87D1FDE8** nebo nápravy zobrazuje na kartě Vlastnosti zařízení > zásady.

Zkontrolujte konfiguraci svého profilu EAS pro zařízení Samsung KNOX a zdroj zásad. Možnost synchronizace poznámek Samsung už není podporovaná a tato možnost by se ve vašem profilu neměla vybrat. Ujistěte se, že zařízení mají dostatek času na zpracování zásady, a to až 24 hodin.

## <a name="unable-to-send-images-from--email-account"></a>Z e-mailového účtu nelze odesílat obrázky

Uživatelé, kteří mají automaticky nastavené e-mailové účty, nemůžou ze svých zařízení odesílat obrázky ani obrázky. K tomuto scénáři může dojít, pokud není povolená **možnost povolit odesílání e-mailů z aplikací třetích stran** .

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **konfigurační profily**.
3. Vyberte váš e-mailový profil > **vlastnosti** > **Nastavení**.
4. Nastavte povolení **odesílání e-mailů z aplikací třetích stran** na hodnotu **Povolit**.

## <a name="next-steps"></a>Další kroky

Získejte pomoc [od Microsoftu](../fundamentals/get-support.md)nebo využijte [komunitní fóra](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).
