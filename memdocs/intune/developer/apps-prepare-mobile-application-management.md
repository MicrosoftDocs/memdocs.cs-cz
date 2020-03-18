---
title: Příprava aplikací pro správu mobilních aplikací nástrojem Microsoft Intune
description: Informace v tomto tématu vám pomůžou rozhodnout, kdy byste měli použít nástroj App Wrapping a sadu App SDK, aby vaše vlastní obchodní aplikace mohly používat zásady správy mobilních aplikací.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/02/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 29e22121-8268-48b5-a671-f940a6be1d24
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: af0d79f42f1c8861fe60cb2f4f9b618cb54009d1
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331851"
---
# <a name="prepare-line-of-business-apps-for-app-protection-policies"></a>Příprava obchodních aplikací na zásady ochrany aplikací

Svým aplikacím můžete umožnit použití zásad ochrany aplikací buď prostřednictvím nástroje Intune App Wrapping Tool, nebo pomocí sady Intune App SDK. V tomto tématu se dozvíte, co tyto dvě metody obnáší a kdy je použít.

## <a name="intune-app-wrapping-tool"></a>Nástroj Intune App Wrapping

Nástroj App Wrapping se používá hlavně pro **interní** obchodní aplikace. Je to aplikace příkazového řádku, která vytvoří kolem aplikace obálku, a ta potom umožní správu aplikace pomocí zásad ochrany aplikací Intune. Při ochraně aplikace poskytované nezávislým výrobcem softwaru (ISV) je důležité objasnit, jestli bude ISV podporovat i zabalenou aplikaci.

K použití nástroje nepotřebujete zdrojový kód, ale potřebujete přihlašovací údaje k podepisování. Další informace o přihlašovacích údajích k podepisování najdete v [blogu o Intune](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/25/how-to-obtain-the-prerequisites-for-the-intune-app-wrapping-tool-for-ios/). Dokumentaci k nástroji pro zabalení aplikace najdete v tématu Nástroj pro zabalení [aplikace pro Android](app-wrapper-prepare-android.md) a [Nástroj pro zabalení aplikace pro iOS](app-wrapper-prepare-ios.md).

Nástroj App Wrapping **nepodporuje** aplikace v Apple App Storu nebo obchodu Google Play. Nepodporuje ani některé funkce, které vyžadují vývojářskou integraci (viz následující tabulka s porovnáním funkcí).

Další informace o nástroji App Wrapping Tool pro zásady ochrany aplikací na zařízeních, která nejsou registrovaná do Intune, najdete v článku [Ochrana obchodních aplikací a dat na zařízeních neregistrovaných do Microsoft Intune](../apps/apps-add.md).

### <a name="reasons-to-use-the-app-wrapping-tool"></a>Důvody pro použití nástroje App Wrapping Tool

* Aplikace nemá předdefinované funkce ochrany dat.
* Aplikace je nasazená interně.
* Nemáte přístup ke zdrojovému kódu aplikace.
* Aplikaci jste nevyvinuli.
* Aplikace zahrnuje minimální funkce ověřování uživatelů.

### <a name="supported-app-development-platforms"></a>Podporované platformy vývoje aplikací

|**Nástroj App Wrapping** | **Xamarin** |**Cordova** |
|------|----|----|
|**iOS** |Ano|Ano|
|**Androidemem**|Ne – Použijte [xamarinové vazby sady Intune App SDK](app-sdk-xamarin.md).|Ano|

## <a name="intune-app-sdk"></a>Sada Intune App SDK

Sada App SDK je určená hlavně zákazníkům, kteří mají aplikace v App Storu nebo obchodu Google Play a chtějí mít možnost spravovat je pomocí Intune. Nicméně využít integraci sady SDK může jakákoli aplikace, i obchodní aplikace.

Další informace o sadě SDK najdete v tématu [Přehled](app-sdk.md). Pokud chcete začít používat sadu SDK, přečtěte si téma [Začínáme s Microsoft Intune App SDK](app-sdk-get-started.md).

### <a name="reasons-to-use-the-sdk"></a>Důvody pro použití sady SDK

* Aplikace nemá předdefinované funkce ochrany dat.
* Aplikace je nasazená prostřednictvím veřejného obchodu s aplikacemi, jako je Google Play nebo App Store společnosti Apple.
* Jste vývojář aplikací a máte technické znalosti potřebné k použití sady SDK.
* Aplikace zahrnuje další integrace pomocí sady SDK.
* Aplikace se často aktualizuje.

### <a name="supported-app-development-platforms"></a>Podporované platformy vývoje aplikací

|**Intune App SDK** |**Xamarin** |**Cordova**
|------|----|----|
|**iOS**|Ano – Použijte [xamarinové vazby sady Intune App SDK](app-sdk-xamarin.md).|Ne|
|**Androidemem**| Ano – Použijte [xamarinové vazby sady Intune App SDK](app-sdk-xamarin.md).|Ne|

## <a name="not-using-an-app-development-platform-listed-above"></a>Nepoužíváte platformu pro vývoj aplikací uvedenou výše?

Vývojový tým sady Intune SDK aktivně testuje a udržuje podporu pro aplikace vytvořené s nativními platformami Android, iOS (obj-C, SWIFT), Xamarin, Xamarin. Forms a Cordova. I když se někteří zákazníci dokončí s integrací sady Intune SDK s jinými platformami, jako je například reakce nativních a NativeScript, neposkytujeme explicitní pokyny ani moduly plug-in pro vývojáře aplikací, kteří používají jinou než naše podporované platformy. 

## <a name="feature-comparison"></a>Porovnání funkcí

Tato tabulka obsahuje seznam nastavení, která jsou povolená, pokud aplikace používá sadu App SDK nebo nástroj pro zabalení aplikace. Některé funkce vyžadují, aby vývojáři aplikací použili určitou logiku mimo základní integraci se sadou Intune SDK a jako takové nejsou povolené, pokud aplikace používá nástroj pro zabalení aplikace. 

|Funkce|App SDK (sada)|App Wrapping Tool|
|-----------|---------------------|-----------|
|Omezit zobrazování obsahu webu jenom na podnikový spravovaný prohlížeč|X|X|
|Zabránit zálohování Androidu, iTunes a iCloudu|X|X|
|Povolit aplikaci přenos dat do ostatních aplikací|X|X|
|Povolit aplikaci, aby přijímala data z jiných aplikací|X|X|
|Omezit vyjmutí, kopírování a vkládání v ostatních aplikacích|X|X|
|Zadejte počet znaků, které mohou být vyjmuty nebo zkopírovány ze spravované aplikace.|X|X|
|Požadovat jednoduchý kód PIN pro přístup|X|X|
|Určit počet pokusů o zadání PIN kódu před jeho obnovením|X|X|
|Povolit otisk prstu místo PIN kódu|X|X|
|Povolit rozpoznávání obličeje místo PIN kódu (pouze iOS)|X|X|
|Vyžadovat podnikové přihlašovací údaje pro přístup|X|X|
|Nastavit vypršení platnosti kódu PIN|X|X|
|Blokovat spuštění spravovaných aplikací v zařízení s jailbreakem nebo rootem|X|X|
|Zašifrovat data aplikací|X|X|
|Znovu zkontrolovat požadavky na přístup po zadaném počtu minut|X|X|
|Zadat období odkladu pro offline režim|X|X|
|Blokovat snímek obrazovky (jenom Android)|X|X|
|Podpora MAM bez registrace zařízení|X|X|
|Úplné vymazání dat aplikací|X|X|
|Selektivní vymazání pracovních a školních dat ve scénářích s více identitami <br><br>**Poznámka:** Pro iOS/iPadOS se při odebrání profilu správy odebere i aplikace.|X||
|Zabránit možnosti Uložit jako|X||
|Cílová konfigurace aplikace (nebo konfigurace aplikace prostřednictvím kanálu MAM)|X|X|
|Podpora víc identit|X||
|Přizpůsobitelný styl |X|||
|Připojení VPN aplikace na vyžádání pomocí Citrix mVPN|X|X| 
|Zakázat synchronizaci kontaktů|X|X|
|Zakázat tisk|X|X|
|Vyžadovat minimální verzi aplikace|X|X|
|Vyžadovat minimální operační systém|X|X|
|Vyžadovat minimální verzi oprav zabezpečení Androidu (pouze Android)|X|X|
|Vyžadovat minimální sadu Intune SDK pro iOS (pouze iOS)|X|X|
|Ověření zařízení SafetyNet (jenom Android)|X|X|
|Kontrola hrozeb u aplikací (jenom Android)|X|X|
|Vyžadovat maximální úroveň rizika zařízení u dodavatele ochrany před mobilními hrozbami|X||
|Konfigurace obsahu oznámení aplikace pro účty organizace|X|X|
|Vyžadovat použití schválených klávesnic (jenom Android)|X|X|
|Vyžadovat zásady ochrany aplikací (podmíněný přístup)|X||
|Vyžadovat aplikaci schválenou klienta (podmíněný přístup)|X||

## <a name="next-steps"></a>Další kroky

Další informace o zásadách ochrany aplikací a službě Intune najdete v těchto tématech:

- [Nástroj App Wrapping Tool a aplikace pro Android](app-wrapper-prepare-android.md)<br>
- [Nástroj App Wrapping Tool a aplikace pro iOS](app-wrapper-prepare-ios.md)<br>
- [Použití sady SDK k povolení správy mobilních aplikací pro aplikace](app-sdk.md)
