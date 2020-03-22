---
title: Vytvoření profilů zařízení v Microsoft Intune – Azure | Microsoft Docs
description: Přidání nebo konfigurace profilu konfigurace zařízení v Microsoft Intune. Vyberte typ platformy, nakonfigurujte nastavení, přidejte značku oboru.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d98aceff-eb35-4e3e-8e40-5f300e7335cc
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 462f9ca9618d16c0291792f86d00c46f641c6cc8
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084063"
---
# <a name="create-a-device-profile-in-microsoft-intune"></a>Vytvořte profil zařízení v Microsoft Intune

Profily zařízení umožňují přidat a nakonfigurovat nastavení a potom tato nastavení nasdílet do zařízení ve vaší organizaci. Použití [funkcí a nastavení na vašich zařízeních pomocí profilů zařízení](device-profiles.md) obsahuje více podrobností, včetně toho, co můžete dělat.

V tomto článku najdete:

- Seznam kroků pro vytvoření profilu.
- Ukazuje, jak přidat značku oboru do "Filter" Profile.
- Popisuje pravidla použitelnosti na zařízeních s Windows 10 a ukazuje, jak vytvořit pravidlo.
- Vypíše časy obnovení při vracení se změnami, když zařízení obdrží profily a všechny aktualizace profilu.

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení** > **konfigurační profily**. Máte následující možnosti:

    - **Přehled**: zobrazuje stav profilů a poskytuje další podrobnosti o profilech, které jste přiřadili uživatelům a zařízením.
    - **Správa**: vytváření profilů zařízení, nahrávání vlastních [skriptů PowerShellu](../apps/intune-management-extension.md) , které se mají spustit v rámci profilu, a Přidání datových plánů do zařízení pomocí [eSIM karty](esim-device-configuration.md).
    - **Monitorování**: Zkontrolujte stav profilu pro úspěch nebo neúspěch a také si prohlédněte protokoly v profilech.
    - **Nastavení**: přidejte certifikační autoritu SCEP nebo PFX nebo povolte [správu telekomunikačních výdajů](telecom-expenses-monitor.md) v profilu.

3. Vyberte **vytvořit profil**. Zadejte následující vlastnosti:

   - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například **e-mailový profil WP pro celou firmu**.
   - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.
   - **Platforma**: vyberte platformu zařízení. Možnosti:  

       - **Správce zařízení s Androidem**
       - **Android Enterprise**
       - **iOS/iPadOS**
       - **macOS**
       - **Windows Phone 8.1**
       - **Windows 8.1 a novější**
       - **Windows 10 a novější**

   - **Typ profilu**: Vyberte typ nastavení, které chcete vytvořit. Zobrazený seznam závisí na zvolené **platformě** .
   - **Nastavení**: následující články popisují nastavení pro jednotlivé typy profilů:

       - [Šablony pro správu](administrative-templates-windows.md)
       - [Vlastní](custom-settings-configure.md)
       - [Optimalizace doručení](delivery-optimization-windows.md)
       - [Funkce zařízení](device-features-configure.md)
       - [Omezení zařízení](device-restrictions-configure.md)
       - [Připojení k doméně](domain-join-configure.md)
       - [Upgrade edice a přepínač režimu](edition-upgrade-configure-windows-10.md)
       - [Školení](education-settings-configure.md)
       - [E-mail](email-settings-configure.md)
       - [Endpoint Protection](../protect/endpoint-protection-configure.md)
       - [Ochrana identit](../protect/identity-protection-configure.md)  
       - [Veřejný terminál](kiosk-settings.md)
       - [ATP v programu Microsoft Defender](../protect/advanced-threat-protection.md)
       - [Certifikát PKCS](../protect/certficates-pfx-configure.md)
       - [Importovaný certifikát PKCS](../protect/certificates-imported-pfx-configure.md)
       - [Soubor předvoleb](preference-file-settings-macos.md)
       - [Certifikát SCEP](../protect/certificates-scep-configure.md)
       - [Důvěryhodný certifikát](../protect/certificates-configure.md)
       - [Aktualizovat zásady](../protect/software-updates-ios.md)
       - [VPN](vpn-settings-configure.md)
       - [Wi-Fi](wi-fi-settings-configure.md)
       - [Windows Information Protection](../protect/windows-information-protection-configure.md)

     Pokud třeba pro platformu vyberete **iOS/iPadOS** , možnosti typu vašeho profilu vypadají podobně jako v následujícím profilu:

     > [!div class="mx-imgBorder"]
     > ![vytvořit profil iOS/iPadOS v Intune](./media/device-profile-create/create-device-profile.png)

4. Po dokončení vyberte **OK** > **vytvořit** a uložte provedené změny. Profil se vytvoří a zobrazí se v seznamu.

## <a name="scope-tags"></a>Značky oboru

Po přidání nastavení můžete do profilu přidat také značku oboru. Značky oboru vyfiltrují profily na konkrétní IT skupiny, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment`.

Další informace o značkách oboru a o tom, co můžete dělat, najdete v tématu [použití značek RBAC a Scope pro distribuci](../fundamentals/scope-tags.md).

### <a name="add-a-scope-tag"></a>Přidat značku oboru

1. Vyberte **obor (značky)** .
2. Vyberte **Přidat** a vytvořte novou značku oboru. Nebo vyberte ze seznamu existující značku oboru.
3. Výběrem **OK** uložte změny.

## <a name="applicability-rules"></a>Pravidla použitelnosti

Platí pro:

- Windows 10 a novější

Pravidla použitelnosti umožňují správcům cílit na zařízení ve skupině, která splňuje určitá kritéria. Například vytvoříte profil omezení zařízení, který se vztahuje na skupinu **všech zařízení s Windows 10** . A potřebujete jenom profil přiřazený k zařízením s Windows 10 Enterprise.

Chcete-li provést tuto úlohu, vytvořte **pravidlo použitelnosti**. Tato pravidla jsou ideální pro následující scénáře:

- Používáte Windows 10 školství (EDU). V Bellows školy chcete cílit na všechna zařízení s Windows 10 EDU mezi RS3 a RS4.
- Chcete cílit všechny uživatele v lidských zdrojích na společnosti Contoso, ale přejete si pouze zařízení se systémem Windows 10 Professional nebo Enterprise.

Pro přístup k těmto scénářům máte tyto možnosti:

- Vytvořte skupinu zařízení, která zahrnuje všechna zařízení na Bellows škole. V profilu přidejte pravidlo použitelnosti, aby se naplatilo, pokud je minimální verze operačního systému `16299` a že je `17134`maximální verze. Přiřaďte tento profil ke skupině zařízení Bellows školy.

  Po přiřazení se profil vztahuje na zařízení mezi minimální a maximální verzí, které zadáte. U zařízení, která nepatří mezi minimální a maximální verze, které zadáte, se jejich stav zobrazuje jako **nepoužitý**.

- Vytvořte skupinu uživatelů, která bude obsahovat všechny uživatele v lidských zdrojích (HR) ve společnosti Contoso. V profilu přidejte pravidlo použitelnosti, aby se používalo pro zařízení s Windows 10 Professional nebo Enterprise. Přiřaďte tento profil skupině uživatelů personální oddělení.

  Po přiřazení se profil vztahuje na zařízení s Windows 10 Professional nebo Enterprise. U zařízení, která nepoužívají tyto edice, se jejich stav zobrazuje jako **nepoužitý**.

- Pokud existují dva profily s přesným nastavením, použije se profil bez pravidla použitelnosti. 

  Například profilace cílí na skupinu zařízení s Windows 10, povolí BitLocker a nemá pravidlo použitelnosti. ProfileB cílí na stejnou skupinu zařízení s Windows 10, umožňuje BitLocker a má pravidlo použitelnosti, které profil použije jenom na Windows 10 Enterprise.

  Při přiřazení obou profilů se použije profilace, protože nemá pravidlo použitelnosti. 

Když přiřadíte profil ke skupinám, budou pravidla použitelnosti fungovat jako filtr a budou cílit jenom na zařízení, která splňují vaše kritéria.

### <a name="add-a-rule"></a>Přidat pravidlo

1. Vyberte **pravidla použitelnosti**. Můžete zvolit **pravidlo**, **vlastnost**a **edici OS**:

    > [!div class="mx-imgBorder"]
    > ![přidat pravidlo použitelnosti do konfiguračního profilu zařízení v Microsoft Intune](./media/device-profile-create/applicability-rules.png)

2. V možnosti **pravidlo**vyberte, jestli chcete zahrnout nebo vyloučit uživatele nebo skupiny. Možnosti:

    - **Přiřadit profil, pokud**: obsahuje uživatele nebo skupiny, které splňují zadaná kritéria.
    - **Nepřiřazovat profil, pokud**: vyloučí uživatele nebo skupiny, které splňují zadaná kritéria.

3. V **vlastnosti**vyberte filtr. Možnosti: 

    - **Edice OS**: v seznamu vyhledejte edice Windows 10, které chcete zahrnout (nebo vyloučit) ve vašem pravidle.
    - **Verze operačního systému**: zadejte **minimální** a **maximální** číslo verze Windows 10, které chcete zahrnout (nebo vyloučit) ve vašem pravidle. Obě hodnoty jsou povinné.

      Můžete například zadat `10.0.16299.0` (RS3 nebo 1709) pro minimální verzi a `10.0.17134.0` (RS4 nebo 1803) pro maximální verzi. Nebo můžete být přesnější a zadat `10.0.16299.001` pro minimální verzi a `10.0.17134.319` pro maximální verzi.

4. Pokud chcete změny uložit, vyberte **Přidat** .

## <a name="refresh-cycle-times"></a>Aktualizovat časy cyklů

Intune používá ke kontrole aktualizací konfiguračních profilů různé aktualizační cykly. Pokud se zařízení nedávno zaregistrovalo, vrácení se změnami se spouští častěji. V [cyklech aktualizace zásad a profilů](device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) se zobrazí odhadované časy aktualizace.

Uživatelé mohou kdykoli otevřít aplikaci Portál společnosti a synchronizovat zařízení, aby ihned kontrolovala aktualizace profilu.

## <a name="recommendations"></a>Doporučení

Při vytváření profilů Vezměte v úvahu následující doporučení:

- Pojmenujte své zásady, abyste věděli, co jsou a co dělají. Všechny [zásady dodržování předpisů](../protect/create-compliance-policy.md) a [konfigurační profily](../configuration/device-profile-create.md) mají volitelnou vlastnost **Description** . V **popisu**se jedná o konkrétní a zahrnuté informace, aby ostatní věděli, co zásady dělá.

  Mezi příklady konfiguračních profilů patří:

  **Název profilu**: Šablona správce – konfigurační profil OneDrivu pro všechny uživatele Windows 10  
  **Popis profilu**: Profil šablony správce OneDrivu, který obsahuje minimální a základní nastavení pro všechny uživatele Windows 10. Vytvořeno pomocí user@contoso.com, aby uživatelé nemohli sdílet data organizace s osobními účty OneDrive.

  **Název profilu**: profil VPN pro všechny uživatele iOS/iPadOS  
  **Popis profilu**: profil VPN, který obsahuje minimální a základní nastavení pro všechny uživatele iOS/iPadOS pro připojení k síti Contoso VPN. Vytvořeno pomocí user@contoso.com, aby se uživatelé k síti VPN automaticky ověřovali a místo toho byli vyzváni k zadání uživatelského jména a hesla.

- Vytvořte svůj profil podle úkolu, jako je konfigurace nastavení Microsoft Edge, povolení ochrany proti virům v programu Microsoft Defender, blokování zařízení s iOS/iPadOS s jailbreakem a tak dále.

- Vytvářejte profily, které se vztahují na konkrétní skupiny, jako jsou marketing, prodej, správci IT nebo umístění nebo školní systém.

- Samostatné zásady uživatele ze zásad zařízení.

  Například [šablony pro správu v Intune](administrative-templates-windows.md) mají stovky nastavení ADMX. Tyto šablony ukazují, jestli se nastavení vztahují na uživatele nebo zařízení. Při vytváření šablon pro správu přiřaďte nastavení uživatelů ke skupině uživatelů a přiřaďte nastavení zařízení ke skupině zařízení.

  Následující obrázek ukazuje příklad nastavení, které se může vztahovat na uživatele nebo použít na zařízení:

  > [!div class="mx-imgBorder"]
  > ![šablonu správce Intune, která se vztahuje na uživatele a zařízení](./media/device-profile-create/setting-applies-to-user-and-device.png)

- Pokaždé, když vytvoříte omezující zásadu, sdělte tuto změnu vašim uživatelům. Pokud například měníte požadavek na přístupový kód ze 4 znaků na 6 znaků, dejte uživatelům informace o tom, než zásadu přiřadíte.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).
