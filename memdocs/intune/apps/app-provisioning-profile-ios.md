---
title: Zřizovací profily aplikací pro iOS/iPadOS v Microsoft Intune
titleSuffix: ''
description: Intune poskytuje nástroje umožňující proaktivně přiřadit nový zřizovací profil k zařízením s aplikacemi, kterým brzy vyprší platnost.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: bbc3ba4a-df48-4aeb-988b-69a177764e3a
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a1ce95391e8dbfa9fd8f5a8e2347f9c4249ee79f
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80323438"
---
# <a name="use-ios-app-provisioning-profiles-to-prevent-your-apps-from-expiring"></a>Jak zabránit vypršení platnosti aplikací pomocí zřizovacích profilů pro aplikace pro iOS

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

## <a name="introduction"></a>Úvod

Obchodní aplikace Apple iOS/iPadOS, které jsou přiřazené k iPhonu a iPady, jsou vytvořené pomocí zahrnutého zřizovacího profilu a kódu, který je podepsaný certifikátem. Po spuštění aplikace iOS/iPadOS potvrdí integritu aplikace pro iOS/iPadOS a vynutila zásady, které jsou definované zřizovacím profilem. Provedou se k následující ověření:

- **Integrita instalačního souboru** – iOS/iPadOS porovnává podrobnosti aplikace s veřejným klíčem podpisového certifikátu společnosti. Pokud se liší, je možné, že se obsah aplikace změnil, a její spuštění se nepovolí.
- **Vynucení schopností** – iOS/iPadOS se pokusí vynucovat možnosti aplikace ze zřizovacího profilu podniku (ne z individuálních zřizovacích profilů pro vývojáře), které jsou v souboru instalace aplikace (. IPA).


Podpisový certifikát společnosti, který se používá k podepisování aplikací, má obvykle platnost tři roky. Platnost zřizovacího profilu ale vyprší už po roce. Během platnosti certifikátu poskytuje Intune nástroje k proaktivnímu přiřazení nového zřizovacího profilu k zařízením s aplikacemi, kterým brzy vyprší platnost.
Po vypršení platnosti certifikátu musíte aplikaci znovu podepsat pomocí nového certifikátu a vložit nový zřizovací profil s klíčem tohoto nového certifikátu.

Jako správce můžete zahrnout a vyloučit skupiny zabezpečení a přiřadit konfiguraci zřizování aplikací pro iOS/iPadOS. Můžete například přiřadit konfiguraci zřizování aplikací pro iOS/iPadOS všem uživatelům, ale vyloučit skupinu Executive.

## <a name="how-to-create-an-ios-mobile-app-provisioning-profile"></a>Jak vytvořit mobilní zřizovací profil aplikace pro iOS

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > **profily zřizování aplikací pro iOS** > **vytvořit profil**.
3. Na stránce **základy** přidejte následující hodnoty:
    - **Název** – Zadejte název tohoto mobilního zřizovacího profilu.
    - **Popis** – Volitelně zadejte popis pro tuto zásadu.
    - **Odeslat soubor profilu** – zvolte ikonu **otevřít** a pak zvolte soubor konfiguračního profilu Apple Mobile (s rozšířením `.mobileprovision`), který jste stáhli z [webu pro vývojáře Apple](https://developer.apple.com/).

   **Datum vypršení platnosti** se naplní hodnotou v souboru konfiguračního profilu Apple Mobile, který jste přidali výše.<br>

   <img alt="Create profile - Basics" src="./media/app-provisioning-profile-ios/app-provisioning-profile-ios-01.png">

4. Klikněte na tlačítko **Další: značky oboru**.<br>
   Na stránce **značky oboru** můžete volitelně nakonfigurovat značky oboru, které určují, kdo může v Intune Zobrazit profil zřizování aplikací pro iOS/iPadOS. Další informace o značkách oboru najdete v tématu [použití značek řízení přístupu na základě role a rozsahu pro distribuci IT](../fundamentals/scope-tags.md).
5. Klikněte na **Další: přiřazení**.<br>
   Stránka **přiřazení** umožňuje přiřadit profil uživatelům a zařízením. Je důležité si uvědomit, že k zařízení můžete přiřadit profil bez ohledu na to, jestli zařízení spravuje Intune.
6. Klikněte na **Další: zkontrolovat + vytvořit** a zkontrolujte hodnoty, které jste zadali pro profil.
7. Až skončíte, kliknutím na **vytvořit** vytvořte profil zřizování aplikace pro iOS/iPadOS v Intune. 

## <a name="next-steps"></a>Další kroky

Přiřaďte profil k požadovaným zařízením se systémem iOS/iPadOS. Další informace najdete v postupu v článku [Přiřazení profilů zařízení](../configuration/device-profile-assign.md).
