---
title: Výjimky zásad přenosu dat pro aplikace
titleSuffix: Microsoft Intune
description: Vytvořte výjimky zásad pro přenos dat zásad Intune App Protection (APP).
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f9015e3a-c22c-42eb-90e6-ba48dee3a41d
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fb0dc3f7ccdfbf494eb28bba49bc5dc372b5dd06
ms.sourcegitcommit: 1aeb4a11e89f68e8081d76ab013aef6b291c73c1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/14/2020
ms.locfileid: "88217613"
---
# <a name="how-to-create-exceptions-to-the-intune-app-protection-policy-app-data-transfer-policy"></a>Jak vytvořit výjimky zásad pro přenos dat zásad Intune App Protection (APP)

Jako správce můžete vytvořit výjimky zásad pro přenos dat zásad Intune App Protection (APP). Pomocí výjimky lze konkrétně vybrat nespravované aplikace, které budou moct přenášet data do spravovaných aplikací a ze spravovaných aplikací. Vaše IT oddělení musí důvěřovat nespravovaným aplikacím, které jste zahrnuli do seznamu výjimek. 

>[!WARNING] 
> Za provádění změn v zásadách výjimek přenosu dat nesete zodpovědnost. Nespravované aplikace (aplikace, které nejsou spravované pomocí Intune), které přidáte do těchto zásad, budou mít přístup k datům chráněným pomocí spravovaných aplikací. Takový přístup k chráněným datům může mít za následek porušení zabezpečení dat. Výjimky přenosu dat přidávejte jenom pro aplikace, které vaše organizace musí používat, ale které nepodporují zásady ochrany aplikací Intune. Kromě toho přidávejte výjimky jenom pro aplikace, které nepovažujete za rizikové z hlediska úniku dat.

V rámci zásad ochrany aplikací Intune nastavení **Allow aplikace pro přenos dat do jiných aplikací** do **aplikací spravovaných podle zásad** znamená, že aplikace může přenášet data jenom do aplikací spravovaných přes Intune. Pokud potřebujete povolit přenos dat do konkrétních aplikací, které nepodporují aplikaci Intune, můžete k této zásadě vytvořit výjimky pomocí **vybrat aplikace, které se mají vyloučit**. Výjimky umožňují aplikacím spravovaným v Intune vyvolat nespravované aplikace založené na protokolu URL (iOS/iPadOS) nebo názvu balíčku (Android). Intune přidává ve výchozím nastavení důležité nativní aplikace do seznamu výjimek. 

> [!NOTE]
> Změna nebo přidání aplikací do výjimek zásad přenosu dat nemá vliv na jiné zásady ochrany aplikací, jako jsou omezení vyjmutí, kopírování a vložení. 

## <a name="ios-data-transfer-exceptions"></a>Výjimky přenosu dat pro iOS
U zásad cílících na iOS/iPadOS můžete nakonfigurovat výjimky přenosu dat pomocí protokolu URL. Pokud chcete přidat výjimku, vyhledejte informace o podporovaných protokolech URL v dokumentaci od vývojáře příslušné aplikace. Další informace o výjimkách přenosu dat pro iOS/iPadOS najdete v tématu [nastavení zásad ochrany aplikací pro iOS/iPadOS – výjimky přenosu dat](app-protection-policy-settings-ios.md#data-transfer-exemptions).

> [!NOTE]
> U aplikací jiných výrobců Microsoft nenabízí metodu ručního vyhledání protokolu adresy URL pro vytváření výjimek aplikací. 

## <a name="android-data-transfer-exceptions"></a>Výjimky přenosu dat pro Android
U zásad cílících na Android můžete nakonfigurovat výjimky přenosu dat pomocí názvu balíčku aplikace. Název balíčku aplikace můžete vyhledat na stránce obchodu **Google Play** pro aplikaci, pro kterou chcete přidat výjimku. Další informace o výjimkách přenosu dat pro Android najdete v tématu [nastavení zásad ochrany aplikací pro Android – výjimky přenosu dat](app-protection-policy-settings-android.md#data-transfer-exemptions).


>[!TIP]
> ID balíčku aplikace najdete tak, že na tuto aplikaci přejdete v obchodě Google Play. ID balíčku je součástí adresy URL stránky aplikace. Třeba aplikace Microsoft Word má ID balíčku **com.microsoft.office.word**.

### <a name="example"></a>Příklad
Po přidání balíčku **Webex** jako výjimky k zásadám přenosu dat MAM se budou moct odkazy Webex v e-mailové zprávě spravovaného Outlooku otevírat přímo v aplikaci Webex. V ostatních nespravovaných aplikacích bude přenos dat i nadále omezený.

- Příklad **WebEx** pro iOS/iPadOS: Pokud chcete aplikaci **WebEx** vyloučit, aby ji mohly vyvolávat spravované aplikace Intune, musíte přidat výjimku přenosu dat pro následující řetězec: <code>wbx</code>
    
- Příklad **map** pro iOS/iPadOS: Pokud chcete určit výjimku pro nativní aplikaci **Maps** , aby ji mohly vyvolávat spravované aplikace Intune, je nutné přidat výjimku přenosu dat pro následující řetězec: <code>maps</code>

- Příklad **WebEx** pro Android: Pokud chcete určit výjimku pro aplikaci **WebEx** , aby ji mohly vyvolávat spravované aplikace Intune, je nutné přidat výjimku přenosu dat pro následující řetězec: <code>com.cisco.webex.meetings</code>
    
- Příklad **SMS** pro Android: Pokud chcete určit výjimku pro nativní aplikaci **SMS** , aby ji mohly vyvolávat spravované aplikace Intune v různých aplikacích pro zasílání zpráv a zařízeních s Androidem, musíte přidat výjimky přenosu dat pro následující řetězce: 
    <code>com.google.android.apps.messaging</code>
    
    <code>com.android.mms</code>
    
    <code>com.samsung.android.messaging</code>

## <a name="next-steps"></a>Další kroky

- [Vytvoření a nasazení zásad ochrany aplikací](app-protection-policies.md)
- [nastavení zásad ochrany aplikací pro iOS/iPadOS – výjimky přenosu dat](app-protection-policy-settings-ios.md#data-transfer-exemptions)
- [Nastavení zásad ochrany aplikací pro Android – výjimky přenosu dat](app-protection-policy-settings-android.md#data-transfer-exemptions)
