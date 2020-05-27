---
title: Vytvoření a nasazení zásad ochrany aplikací
titleSuffix: Microsoft Intune
description: Toto téma popisuje, jak vytvořit a přiřadit Microsoft Intune zásady ochrany aplikací (aplikace).
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f31b2964-e932-4cee-95c4-8d5506966c85
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 91ca1e8a710e13e393af5bb3723ca1086e37887d
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988606"
---
# <a name="how-to-create-and-assign-app-protection-policies"></a>Vytvoření a přiřazení zásad ochrany aplikací

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Naučte se vytvářet a přiřazovat Microsoft Intune zásady ochrany aplikací (APP) pro uživatele vaší organizace. Toto téma také popisuje, jak změnit existující zásady.

## <a name="before-you-begin"></a>Před zahájením

Zásady ochrany aplikací lze použít pro aplikace běžící na zařízeních, která může nebo nemusí spravovat Intune. Podrobnější popis toho, jak zásady ochrany aplikací fungují, a scénáře podporované zásadami ochrany aplikací Intune najdete v tématu [Přehled zásad ochrany aplikací](app-protection-policy.md).

Volby dostupné v zásadách ochrany aplikací (aplikace) umožňují organizacím přizpůsobit ochranu na jejich konkrétní potřeby. V některých případech nemusí být zřejmé, která nastavení zásad jsou nutná k implementaci kompletního scénáře. Microsoft zavedl taxonomii pro své rozhraní ochrany dat aplikací pro správu mobilních aplikací v iOS a Androidu, aby organizacím pomohly určit prioritu posílení koncových bodů mobilních klientů.

Architektura aplikace Data Protection je rozdělená na tři různé úrovně konfigurace, přičemž každá úroveň se sestavuje na předchozí úrovni:

- **Ochrana podnikových dat** na úrovni Basic (úroveň 1) zajišťuje, aby byly aplikace chráněny pomocí kódu PIN a zašifrované a prováděly operace selektivního vymazání. U zařízení s Androidem Tato úroveň ověřuje ověření zařízení s Androidem. Toto je konfigurace na úrovni vstupu, která poskytuje podobné řízení ochrany dat v zásadách poštovní schránky Exchange Online a zavádí uživatele a naplňování do aplikace.
- **Enterprise Enhanced Data Protection** (úroveň 2) zavádí mechanismy prevence úniku dat aplikace a minimální požadavky na operační systém. Jedná se o konfiguraci, která platí pro většinu mobilních uživatelů, kteří přistupují k pracovním nebo školním datům.
- **Podniková ochrana dat** (úroveň 3) zavádí pokročilé mechanismy ochrany dat, rozšířenou konfiguraci kódu PIN a ochranu před mobilními hrozbami aplikace. Tato konfigurace je žádoucí pro uživatele, kteří mají přístup k datům s vysokým rizikem.

Pokud chcete zobrazit konkrétní doporučení pro jednotlivé úrovně konfigurace a minimální aplikace, které musí být chráněné, přečtěte si téma [Ochrana dat pomocí zásad ochrany aplikací](app-protection-framework.md).

Pokud hledáte seznam aplikací, které mají integrovanou sadu Intune SDK, přečtěte si téma [Microsoft Intune Protected Apps](apps-supported-intune-apps.md).

Informace o přidání obchodních aplikací organizace do Microsoft Intune kvůli přípravě na zásady ochrany aplikací najdete v tématu [Přidání aplikací do Microsoft Intune](apps-add.md).

## <a name="app-protection-policies-for-iosipados-and-android-apps"></a>Zásady ochrany aplikací pro iOS/iPadOS a aplikace pro Android

Když vytvoříte zásady ochrany aplikací pro iOS/iPadOS a aplikace pro Android, budete postupovat podle moderního toku procesu Intune, který má za následek novou zásadu ochrany aplikací.

### <a name="create-an-iosipados-or-android-app-protection-policy"></a>Vytvoření zásad ochrany aplikací pro iOS/iPadOS nebo Android

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. V portálu Intune vyberte **aplikace**  >  **Zásady ochrany aplikací**. Po výběru této možnosti se zobrazí detaily **Zásady ochrany aplikací**, kde můžete vytvářet nové zásady a upravovat stávající.
3. Vyberte **vytvořit zásadu** a vyberte možnost **iOS/iPadOS** nebo **Android**. Zobrazí se podokno **vytvořit zásadu** .
4. Na stránce **základy** přidejte následující hodnoty:

    | Hodnota | Popis |
    |--------------|------------------------------------------------|
    | Name | Název této zásady ochrany aplikací |
    | Popis | Volitelné Popis této zásady ochrany aplikací |


    Hodnota **platformy** je nastavená na základě výše zvolené možnosti.

    ![Snímek stránky základy v podokně vytvořit zásadu](./media/app-protection-policies/app-protection-add-policies-01.png)

5. Kliknutím na **Další** zobrazte stránku **aplikace** .<br>
    Stránka **aplikace** umožňuje zvolit, jak chcete tyto zásady použít pro aplikace na různých zařízeních. Musíte přidat alespoň jednu aplikaci.<p>

    | Hodnota/možnost | Popis |
    |-------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Cíl pro aplikace na všech typech zařízení | Tuto možnost použijte, pokud chcete zásady zaměřit na aplikace na zařízeních libovolného stavu správy. Pokud chcete cílit aplikace na konkrétní typy zařízení, vyberte **ne** . Informace najdete v tématu [cílení zásad ochrany aplikací na základě stavu správy zařízení](#target-app-protection-policies-based-on-device-management-state) . |
    |     Typy zařízení | Tuto možnost použijte, pokud chcete určit, jestli se tato zásada vztahuje na zařízení spravovaná MDM nebo na nespravovaná zařízení. V případě zásad aplikací pro iOS/iPadOS vyberte možnost z **nespravovaných** a **spravovaných** zařízení. V případě zásad aplikací pro Android vyberte z **nespravovaného**, **Správce zařízení s Androidem**a **Android Enterprise**.  |
    | Veřejné aplikace | Klikněte na **Vybrat veřejné aplikace** a vyberte aplikace, které se mají cílit. |
    | Vlastní aplikace | Klikněte na **Vybrat vlastní aplikace** a vyberte vlastní aplikace, které chcete cílit na základě ID sady prostředků. |

    Vybrané aplikace se zobrazí v seznamu veřejné a vlastní aplikace.
6. Kliknutím na **Další** zobrazte stránku **Ochrana dat** .<br>
    Tato stránka poskytuje nastavení pro řízení ochrany před únikem informací (DLP), včetně omezení pro vyjmutí, kopírování, vložení a uložení. Tato nastavení určují, jak uživatelé pracují s daty v aplikacích, které tato zásada ochrany aplikací používá.

    **Nastavení ochrany dat**:<br>
    - **iOS/iPadOS data Protection** – informace najdete v tématu [nastavení zásad ochrany aplikací pro iOS nebo IPadOS – ochrana dat](app-protection-policy-settings-ios.md#data-protection).
    - **Ochrana dat v Androidu** – informace najdete v tématu [nastavení zásad ochrany aplikací pro Android – ochrana dat](app-protection-policy-settings-android.md#data-protection).

7. Kliknutím na **Další** zobrazte stránku **požadavky na přístup** .<br>
    Tato stránka poskytuje nastavení, která umožňují nakonfigurovat požadavky na kód PIN a přihlašovací údaje, které uživatelé musí splnit, aby měli přístup k aplikacím v pracovním kontextu.
 
    **Nastavení požadavků na přístup**:<br>
    - **požadavky na přístup pro iOS/iPadOS** – informace najdete v tématu [nastavení zásad ochrany aplikací pro iOS/iPadOS – požadavky na přístup](app-protection-policy-settings-ios.md#access-requirements).
    - **Požadavky na přístup k Androidu** – informace najdete v tématu [nastavení zásad ochrany aplikací pro Android – požadavky na přístup](app-protection-policy-settings-android.md#access-requirements).

8. Kliknutím na **Další** zobrazte **podmíněný spouštěcí** stránku.<br>
    Tato stránka poskytuje nastavení pro nastavení požadavků na zabezpečení přihlášení pro zásady ochrany aplikací. Vyberte **Nastavení** a do sloupce **Hodnota** zadejte hodnotu, kterou uživatelé musí splnit, aby se přihlásili k firemní aplikaci. Pak vyberte **akci** , kterou chcete provést, pokud uživatelé nesplňují vaše požadavky. V některých případech lze pro jedno nastavení nakonfigurovat více akcí.

    **Nastavení podmíněného spuštění**:<br>
    - **podmíněné spuštění iOS/iPadOS** – informace najdete v tématu [nastavení zásad ochrany aplikací pro iOS/iPadOS – podmíněné spuštění](app-protection-policy-settings-ios.md#conditional-launch).
    - **Podmíněné spuštění Androidu** – informace najdete v tématu [nastavení zásad ochrany aplikací pro Android – podmíněné spuštění](app-protection-policy-settings-android.md#conditional-launch).

9. Kliknutím na tlačítko **Další** zobrazíte stránku **přiřazení** .<br>
   Stránka **přiřazení** vám umožní přiřadit zásady ochrany aplikací skupinám uživatelů.

10. Klikněte na **Další: zkontrolovat + vytvořit** a zkontrolujte hodnoty a nastavení, které jste zadali pro tyto zásady ochrany aplikací.

11. Až skončíte, klikněte na **vytvořit** a vytvořte zásadu ochrany aplikací v Intune.

    > [!TIP]
    > Tato nastavení zásad se vynutí jenom při použití aplikace v pracovním kontextu. Když koncový uživatel použije aplikaci k provedení osobní úlohy, nebudou mít tyto zásady na ni vliv. Upozorňujeme, že když vytvoříte nový soubor, považuje se za osobní soubor.

Koncoví uživatelé můžou stahovat aplikace z App Storu nebo Google Play. Další informace naleznete v tématu:
* [Co očekávat, když ke správě svojí aplikace pro Android používáte zásady ochrany aplikací](../fundamentals/end-user-mam-apps-android.md)
* [Co očekávat, když je vaše aplikace pro iOS/iPadOS spravovaná zásadami ochrany aplikací](../fundamentals/end-user-mam-apps-ios.md)

## <a name="change-existing-policies"></a>Změna existujících zásad
Podle potřeby můžete upravit existující zásady a použít je pro cílové uživatele. Když ale změníte existující zásady, uživatelé, kteří se už přihlásili k aplikacím, neuvidí změny po dobu osmi hodin.

Aby se změny projevily hned, musí se koncový uživatel odhlásit od aplikace a pak se k ní zase přihlásit.

### <a name="to-change-the-list-of-apps-associated-with-the-policy"></a>Změna seznamu aplikací přidružených k zásadě

1. V podokně **Zásady ochrany aplikací** vyberte zásadu, kterou chcete změnit.

2. V podokně *Intune App Protection* vyberte možnost **vlastnosti**.

3. Vedle části s názvem *aplikace*vyberte **Upravit**.

4. Stránka **aplikace** umožňuje zvolit, jak chcete tyto zásady použít pro aplikace na různých zařízeních. Musíte přidat alespoň jednu aplikaci.<p>
    
    | Hodnota/možnost | Popis |
    |-------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Cíl pro aplikace na všech typech zařízení | Tuto možnost použijte, pokud chcete zásady zaměřit na aplikace na zařízeních libovolného stavu správy. Pokud chcete cílit aplikace na konkrétní typy zařízení, vyberte **ne** . Pro toto nastavení může být vyžadována další konfigurace aplikace. Podrobnosti najdete v tématu [Cílení zásad ochrany aplikací na základě stavu správy zařízení](#target-app-protection-policies-based-on-device-management-state). |
    |     Typy zařízení | Tuto možnost použijte, pokud chcete určit, jestli se tato zásada vztahuje na zařízení spravovaná MDM nebo na nespravovaná zařízení. V případě zásad aplikací pro iOS/iPadOS vyberte možnost z **nespravovaných** a **spravovaných** zařízení. V případě zásad aplikací pro Android vyberte z **nespravovaného**, **Správce zařízení s Androidem**a **Android Enterprise**.  |
    | Veřejné aplikace | Klikněte na **Vybrat veřejné aplikace** a vyberte aplikace, které se mají cílit. |
    | Vlastní aplikace | Klikněte na **Vybrat vlastní aplikace** a vyberte vlastní aplikace, které chcete cílit na základě ID sady prostředků. |

    Vybrané aplikace se zobrazí v seznamu veřejné a vlastní aplikace.

5. Klikněte na tlačítko **zkontrolovat + vytvořit** a zkontrolujte aplikace vybrané pro tuto zásadu.

6. Až skončíte, klikněte na **Uložit** a aktualizujte Zásady ochrany aplikací.
 
#### <a name="to-change-the-list-of-user-groups"></a>Změna seznamu skupin uživatelů

1. V podokně **Zásady ochrany aplikací** vyberte zásadu, kterou chcete změnit.

2. V podokně *Intune App Protection* vyberte možnost **vlastnosti**.

3. Vedle části s názvem *přiřazení*vyberte **Upravit**.

4. Pokud chcete přidat k zásadě novou skupinu uživatelů, zvolte na kartě *Zahrnout* možnost **Vybrat skupiny, které se zahrnou** a vyberte skupinu uživatelů. Zvolte **možnost vybrat** a přidejte skupinu. 

5. Pokud chcete vyloučit skupinu uživatelů, zvolte na kartě *vyloučit* **možnost vybrat skupiny, které se mají vyloučit**a vyberte skupinu uživatelů. Skupinu uživatelů odeberte pomocí možnosti **Vybrat**.  

6. Pokud chcete odstranit skupiny, které jste dříve přidali, vyberte na kartách *Zahrnout* nebo *vyloučit* tři tečky (...) a vyberte **Odstranit**.

7. Kliknutím na tlačítko **zkontrolovat + vytvořit** zkontrolujte skupiny uživatelů vybrané pro tuto zásadu.

8. Až budou změny v přiřazení připravené, vyberte **Uložit** a uložte konfiguraci a Nasaďte zásadu na novou skupinu uživatelů. Pokud vyberete **Zrušit** před uložením konfigurace, zahodí se všechny změny, které jste udělali na kartách *zahrnutí* a *vyloučení* .

### <a name="to-change-policy-settings"></a>Změna nastavení zásad

1. V podokně **Zásady ochrany aplikací** vyberte zásadu, kterou chcete změnit.

2. V podokně *Intune App Protection* vyberte možnost **vlastnosti**.

3. Vedle oddílu, který odpovídá nastavení, které chcete změnit, vyberte **Upravit**. Pak tato nastavení změňte na nové hodnoty.

7. Kliknutím na tlačítko **zkontrolovat + vytvořit** zkontrolujte aktualizované nastavení pro tuto zásadu.

4. Kliknutím na **Uložit** uložte změny. Opakováním tohoto postupu vyberte jinou oblast nastavení, udělejte změny a pak je uložte, dokud nebudou všechny změny hotové. Pak můžete podokno *Intune App Protection – Vlastnosti* zavřít. 

## <a name="target-app-protection-policies-based-on-device-management-state"></a>Cílení zásad ochrany aplikací na základě stavu správy zařízení
V mnoha organizacích je běžné, že koncovým uživatelům umožníte používat zařízení spravovaná přes správu mobilních zařízení (MDM) Intune, jako jsou zařízení vlastněná podnikem, a nespravovaná zařízení chráněná jenom pomocí zásad ochrany aplikací Intune. Nespravovaná zařízení se často označují jako BYOD (Bring Your Own Devices).

Vzhledem k tomu, že zásady ochrany aplikací Intune cílí na identitu uživatele, nastavení ochrany pro uživatele se může vztahovat na zaregistrovaná zařízení (spravovaná přes MDM) i na nezaregistrovaná zařízení (bez MDM). Proto můžete cílit na zásady ochrany aplikací Intune buď na zaregistrovaná, nebo na neregistrovaná zařízení s iOS/iPadOS a Androidem. Můžete mít jednu zásadu ochrany pro nespravovaná zařízení, ve kterých jsou zavedené ovládací prvky ochrany před únikem informací (DLP), a samostatné zásady ochrany pro zařízení spravovaná pomocí MDM, kde můžou být ovládací prvky ochrany před únikem informací trochu uvolněné. Další informace o tom, jak funguje na osobních zařízeních s Androidem Enterprise, najdete v tématu [Zásady ochrany aplikací a pracovní profily](android-deployment-scenarios-app-protection-work-profiles.md).

Pokud chcete vytvořit tyto zásady, vyhledejte **Apps**  >  v konzole Intune aplikace**Zásady ochrany aplikací** a potom vyberte **vytvořit zásadu**. Můžete také upravit existující zásadu ochranu aplikací. Pokud chcete, aby se zásady ochrany aplikací nastavily u spravovaných i nespravovaných zařízení, přejděte na stránku **aplikace** a ověřte, že **cíl pro aplikace na všech typech zařízení** je nastavená na **Ano**, což je výchozí hodnota. Pokud chcete členit přiřazení na základě stavu správy, nastavte **cíl pro aplikace na všech typech zařízení** na **ne**. 

### <a name="device-types"></a>Typy zařízení

- **Nespravované**: nespravovaná zařízení jsou zařízení, ve kterých se nezjistila Správa služby Intune MDM. Patří sem zařízení, která spravuje dodavatel MDM třetích stran.
- **Zařízení spravovaná pomocí Intune**: spravovaná zařízení se spravují přes Intune MDM.
- **Správce zařízení s Androidem**: zařízení spravovaná přes Intune, která používají rozhraní API pro správu zařízení s Androidem.
- **Android Enterprise**: zařízení spravovaná pomocí Intune s využitím podnikových profilů Androidu nebo úplné správy zařízení s Androidem Enterprise.

V Androidu se zařízení s Androidem zobrazí výzva k instalaci aplikace Portál společnosti Intune bez ohledu na to, který typ zařízení zvolíte. Pokud například vyberete možnost Android Enterprise, budou se stále zobrazovat uživatelé s nespravovanými zařízeními s Androidem.

Pro iOS/iPadOS se pro výběr typu zařízení vynutilo nespravované zařízení, vyžaduje se další nastavení konfigurace aplikace. Tyto konfigurace budou komunikovat se službou APP Service, že konkrétní aplikace je spravovaná a že nastavení aplikace nebudou platit:

- **IntuneMAMUPN** musí být nakonfigurované pro všechny aplikace spravované pomocí správy mobilních zařízení (MDM). Další informace najdete v tématu [Správa přenosu dat mezi aplikacemi pro iOS/iPadOS v Microsoft Intune](data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm).
- **IntuneMAMDeviceID** musí být nakonfigurované pro všechny aplikace spravované pro správu MDM od třetích stran. **IntuneMAMDeviceID** by mělo být nakonfigurované na token ID zařízení. Například, `key=IntuneMAMDeviceID, value={{deviceID}}`. Další informace najdete v tématu [Přidání zásad konfigurace aplikací pro spravovaná zařízení s iOS/iPadOS](app-configuration-policies-use-ios.md).
- Pokud je nakonfigurované jenom **IntuneMAMDeviceID**, Intune APP bude zařízení považovat za nespravované.

> [!NOTE]
> Konkrétní informace o zásadách ochrany aplikací na základě stavu správy zařízení pro iOS/iPadOS najdete v tématu [Zásady ochrany mam cílené na základě stavu správy](../fundamentals/whats-new-archive.md#mam-protection-policies-targeted-based-on-management-state).

## <a name="policy-settings"></a>Nastavení zásad
Pokud chcete zobrazit úplný seznam nastavení zásad pro iOS/iPadOS a Android, vyberte jeden z následujících odkazů:

- [zásady pro iOS/iPadOS](app-protection-policy-settings-ios.md)
- [Zásady pro Android](app-protection-policy-settings-android.md)

## <a name="next-steps"></a>Další kroky
[Monitorování stavu dodržování předpisů a uživatele](app-protection-policies-monitor.md)

## <a name="see-also"></a>Viz také
* [Co očekávat, když ke správě svojí aplikace pro Android používáte zásady ochrany aplikací](../fundamentals/end-user-mam-apps-android.md)
* [Co očekávat, když je vaše aplikace pro iOS/iPadOS spravovaná zásadami ochrany aplikací](../fundamentals/end-user-mam-apps-ios.md)
