---
title: Konfigurace nastavení e-mailu v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Vytvořte e-mailový profil v Microsoft Intune a nasaďte tento profil na zařízení s Androidem pro správce zařízení, Android Enterprise, iOS, iPadOS a Windows. Použijte e-mailové profily ke konfiguraci běžných nastavení e-mailu, včetně e-mailového serveru a metod ověřování pro připojení k firemnímu e-mailu na zařízeních,
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 99f3dcd944270acef98cc0f1f06138d75dba4453
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996414"
---
# <a name="add-email-settings-to-devices-using-intune"></a>Přidání nastavení e-mailu do zařízení pomocí Intune

Microsoft Intune obsahuje různá nastavení e-mailu, která můžete nasadit do zařízení ve vaší organizaci. Správce IT vytvoří e-mailové profily s konkrétním nastavením pro připojení k poštovnímu serveru, například Microsoft 365 a gmail. Koncoví uživatelé pak propojí, ověřují a synchronizují e-mailové účty organizace na svých mobilních zařízeních. Vytvořením a nasazením e-mailového profilu můžete potvrdit, že nastavení jsou standardně v mnoha zařízeních. Zároveň vám to pomůže omezit žádosti o podporu od koncových uživatelů, kteří neznají správná nastavení e-mailu.

E-mailové profily umožňují nakonfigurovat nastavení integrovaného e-mailu na následujících zařízeních:

- Správce zařízení s Androidem na Samsung KNOX standard 5,0 a novějších
- Android Enterprise
- iOS 11,0 a novější
- iPadOS 13,0 a novější
- Windows 10 (Desktop)

V tomto článku se dozvíte, jak vytvořit e-mailový profil v Microsoft Intune. Obsahuje také odkazy na různé platformy s podrobnějším nastavením.

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.
3. Zadejte tyto vlastnosti:

    - **Platforma**: vyberte platformu zařízení. Možnosti:  

        - **Správce zařízení s Androidem** (jenom Samsung Android Knox Standard)
        - **Android Enterprise**
        - **iOS/iPadOS**
        - **Windows 10 a novější**

    - **Profil**: vyberte **e-mail**.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název zásady. Své zásady pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem zásad je například **Windows 10: nastavení e-mailu pro všechna zařízení s Windows 10**.
    - **Popis**: zadejte popis zásady. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.

7. Nastavení, která můžete konfigurovat v **nastavení konfigurace**, se liší v závislosti na zvolené platformě. Pro podrobnější nastavení vyberte platformu:

    - [Správce zařízení s Androidem (Samsung KNOX Standard)](email-settings-android.md)
    - [Android Enterprise](email-settings-android-enterprise.md)
    - [iOS/iPadOS](email-settings-ios.md)
    - [Windows 10](email-settings-windows-10.md)

8. Vyberte **Další**.
9. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu pro konkrétní IT skupiny, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment` . Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](../fundamentals/scope-tags.md).

    Vyberte **Další**.

10. V části **přiřazení**vyberte skupiny uživatelů nebo zařízení, které obdrží váš profil. Další informace o přiřazování profilů najdete v tématu [co potřebujete znát](#what-you-need-to-know) (v tomto článku). [Přiřaďte profily uživatelů a zařízení](device-profile-assign.md) i některé doprovodné materiály.

    Vyberte **Další**.

11. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

## <a name="what-you-need-to-know"></a>Co je potřeba vědět

- E-mailové profily se nasazují pro uživatele, který zařízení zaregistroval. Pokud chcete nakonfigurovat e-mailový profil, Intune v e-mailovém profilu uživatele během registrace používá vlastnosti Azure Active Directory (AD).

- Zařízení Microsoft Outlook pro iOS/iPadOS a Android nepodporují e-mailové profily. Místo toho Nasaďte zásadu konfigurace aplikace. Další informace najdete v tématu [nastavení konfigurace pro Outlook](../apps/app-configuration-policies-outlook.md).

  Na zařízeních s Androidem Enterprise nasaďte pomocí spravovaného Obchod Google Play Gmail nebo 9 pro práci. [Přidat spravované aplikace Google Play](../apps/apps-add-android-for-work.md) zobrazí seznam kroků.

- E-mail je založený na identitě a uživatelském nastavení. E-mailové profily se obvykle přiřazují skupinám uživatelů, nikoli skupinám zařízení. Některé okolnosti:

  - Pokud e-mailový profil obsahuje uživatelské certifikáty, přiřaďte tento e-mailový profil skupinám uživatelů. Můžete mít přiřazeno několik profilů uživatelských certifikátů. Tyto více profilů vytvoří řetěz nasazení profilu. Nasaďte tento řetěz profilu do skupin uživatelů.

    Pokud je jeden profil v tomto řetězu nasazený do skupiny zařízení, můžou se uživatelům při zadávání hesla zobrazovat výzva.

  - Skupiny zařízení se obvykle používají, pokud není primární uživatel nebo Pokud nevíte, kdo bude uživatel. Do zařízení se nemusí doručovat e-mailové profily cílené na skupiny zařízení (ne skupiny uživatelů).

    Pokud se například váš e-mailový profil zaměřuje na skupinu zařízení se systémem iOS/iPadOS, ujistěte se, že všechna tato zařízení mají uživatele. Pokud nějaké zařízení nemá uživatele, e-mailový profil se nemusí nasadit. Pak tento profil omezíte a mohli byste přijít o některá zařízení. Pokud má zařízení primárního uživatele, musí fungovat nasazení na skupiny zařízení.

    Další informace o možných problémech s používáním skupin zařízení najdete v tématu [běžné problémy s e-mailovými profily](troubleshoot-email-profiles-in-microsoft-intune.md).

## <a name="remove-an-email-profile"></a>Odebrání e-mailového profilu

Existují různé způsoby, jak ze zařízení odebrat e-mailový profil, i když je v zařízení jenom jeden profil:

- **Možnost 1**: Otevřete e-mailový**Devices**profil (  >  **profily konfigurací** zařízení > vyberte svůj profil) a zvolte **přiřazení**. Na kartě **Zahrnout** jsou skupiny, které jsou k profilu přiřazené. Klikněte na skupinu pravým tlačítkem > **Odebrat**. Nezapomeňte změny uložit kliknutím na **Uložit**.

- **2. možnost:**[Vymažte zařízení nebo ho vyřaďte](../remote-actions/devices-wipe.md). Tyto akce můžete použít k selektivnímu nebo úplnému odebrání dat a nastavení.

## <a name="secure-email-access"></a>Zabezpečení přístupu k e-mailu

E-mailové profily můžete zabezpečit pomocí následujících možností:

- **Certifikáty:** Při vytváření e-mailového profilu zvolíte profil certifikátu dříve vytvořený v Intune. Tento certifikát se označuje jako certifikát identity. Ověřuje se s profilem důvěryhodného certifikátu nebo kořenovým certifikátem, aby bylo možné potvrdit, že se zařízení uživatele může připojit. Tento důvěryhodný certifikát je přiřazený počítači, který ověřuje připojení k e-mailu. Tímto počítačem je zpravidla nativní poštovní server.

  Pokud používáte pro svůj e-mailový profil ověřování pomocí certifikátů, pak nasaďte e-mailový profil, profil certifikátu a důvěryhodný kořenový profil do stejných skupin. Toto nasazení zajišťuje, že každé zařízení dokáže rozpoznat legitimitu certifikační autority.

  Další informace o vytváření a používání profilů certifikátů v Intune najdete v tématu [Jak konfigurovat certifikáty pomocí Intune](../protect/certificates-configure.md).

- **Uživatelské jméno a heslo**: koncový uživatel se ověřuje na nativním poštovním serveru zadáním uživatelského jména a hesla. Heslo v e-mailovém profilu neexistuje. Proto koncový uživatel zadá heslo při připojování k e-mailu.

## <a name="how-intune-handles-existing-email-accounts"></a>Jak Intune nakládá s existujícími e-mailovými účty

Pokud si už uživatel e-mailový účet nakonfiguroval, přiřadí se e-mailový profil jinak, a to v závislosti na platformě.

- **iOS/iPadOS**: na základě názvu hostitele a e-mailové adresy se detekuje existující duplicitní e-mailový profil. Duplicitní e-mailový profil zablokuje přiřazení profilu Intune. V takovém případě aplikace Portál společnosti upozorní uživatele, že nedodržují předpisy, a vyzve koncového uživatele k ručnímu odebrání nakonfigurovaného profilu. Aby se zabránilo tomuto scénáři, řekněte koncovým uživatelům, aby se zaregistrovali *před* instalací e-mailového profilu, který umožňuje službě Intune nastavit profil.

- **Windows:** Na základě názvu hostitele a e-mailové adresy se detekuje existující duplicitní e-mailový profil. Intune přepíše existující e-mailový profil vytvořený koncovým uživatelem.

- **Android Samsung KNOX Standard**: na základě e-mailové adresy se detekuje existující duplicitní e-mailový profil a přepíše ho profilem Intune. Android nepoužívá k identifikaci profilu název hostitele. Nevytvářejte více e-mailových profilů se stejnou e-mailovou adresou na různých hostitelích. Profily se vzájemně přepíší.

- **Pracovní profily Androidu**: Intune nabízí dva pracovní e-mailové profily pro Android: jednu pro aplikaci Gmail a jednu pro devět pracovních aplikací. Tyto aplikace jsou dostupné v Obchod Google Play a instalují se do pracovního profilu zařízení. Tyto aplikace nevytvářejí duplicitní profily. Obě aplikace podporují připojení k Exchangi. Pokud chcete použít připojení k e-mailu, nasaďte jednu z těchto e-mailových aplikací do zařízení uživatelů. Pak vytvořte a nasaďte e-mailový profil. Můžete použít konfigurační profily gmail a devět e-mailů, které pracují pro pracovní profil a plně spravované, vyhrazené a podnikové typy registrace pracovních profilů, včetně použití profilů certifikátů v obou typech konfigurace e-mailu. V zařízení se nadále vztahují všechny zásady Gmail nebo devět, které vytvoříte v části Konfigurace zařízení pro pracovní profily. Není nutné je přesouvat do zásad konfigurace aplikací. E-mailové aplikace, například devět práce, nemusí být bezplatné. Přečtěte si podrobnosti o licencování aplikace nebo se obraťte na společnost s případnými dotazy.

## <a name="changes-to-assigned-email-profiles"></a>Změny přiřazených e-mailových profilů

Pokud provedete změny e-mailového profilu, který jste předtím přiřadili, může se koncovým uživatelům zobrazit zpráva s žádostí, aby schválili rekonfiguraci nastavení e-mailu.

## <a name="next-steps"></a>Další kroky

Když je profil vytvořený, není ještě aktivní. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).
