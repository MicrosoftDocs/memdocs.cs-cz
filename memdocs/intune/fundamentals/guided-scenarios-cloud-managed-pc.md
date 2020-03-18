---
title: Scénář s asistencí – moderní plocha spravovaná cloudem
titleSuffix: Microsoft Intune
description: Přečtěte si informace o scénáři s průvodcem, jak nastavit a nakonfigurovat základní moderní plochu z portálu pro správu zařízení Microsoft 365.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/26/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8720eec22c8e7fd8a9c8c2303b50e71db0e834ad
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332555"
---
# <a name="guided-scenario---cloud-managed-modern-desktop"></a>Scénář s asistencí – moderní plocha spravovaná cloudem

Moderní plocha je špičkovou produkční platformou pro informačního pracovníka. Office 365 ProPlus a Windows 10 jsou základními komponentami moderního počítače spolu s nejnovějšími směrnými plány zabezpečení pro Windows 10 a rozšířené možnosti ochrany před internetovými útoky v programu Microsoft Defender.

Správa moderního stolního počítače z cloudu přináší přidaný přínos pro vzdálené akce v rámci Internetu. Správa cloudu využívá integrované zásady správy mobilních zařízení systému Windows a odebírá závislosti v místních zásadách skupiny služby Active Directory.

Pokud chcete vyhodnotit cloudovou moderní plochu ve vaší vlastní organizaci, tento scénář s asistencí předem definuje všechny nezbytné konfigurace pro základní nasazení. V tomto scénáři vytvoříte zabezpečené prostředí, kde si můžete vyzkoušet možnosti správy zařízení v Intune.

## <a name="prerequisites"></a>Požadavky

- [Nastavení autority MDM na Intune](../fundamentals/mdm-authority-set.md#set-mdm-authority-to-intune) – nastavení autority správy mobilních zařízení (MDM) určuje způsob správy zařízení. Jako správce IT musíte nastavit autoritu MDM, aby uživatelé mohli registrovat zařízení pro správu.
- M365 E3 minimum (nebo M365 E5 pro nejlepší zabezpečení)
- Zařízení s Windows 10 1903 (zaregistrované s Windows autopilotem pro nejvyšší prostředí pro koncové uživatele)
- Oprávnění správce Intune potřebná k dokončení tohoto scénáře s asistencí:
  - Konfigurace zařízení – číst, vytvořit, odstranit, přiřadit a aktualizovat
  - Programy pro registraci číst zařízení, číst profil, vytvořit profil, přiřadit profil, odstranit profil
  - Mobilní aplikace – číst, vytvořit, odstranit, přiřadit a aktualizovat
  - Čtení a aktualizace organizace
  - Základní hodnoty zabezpečení číst, vytvořit, odstranit, přiřadit a aktualizovat
  - Sady zásad – číst, vytvořit, odstranit, přiřadit a aktualizovat

## <a name="step-1---introduction"></a>Krok 1 – Úvod

V tomto scénáři nastavíte testovacího uživatele, zaregistrujete zařízení v Intune a nasadíte zařízení s použitím nastavení doporučeného pro Intune i Windows 10 a Office ProPlus. Pokud se rozhodnete [tuto ochranu povolit v Intune](../protect/advanced-threat-protection.md#enable-microsoft-defender-atp-in-intune), vaše zařízení se taky nakonfiguruje pro rozšířenou ochranu před internetovými útoky v programu Microsoft Defender. Uživatel, kterého jste nastavili, a zařízení, které zaregistrujete, bude přidáno do nových skupin zabezpečení a bude nakonfigurováno s doporučeným nastavením pro zabezpečení a produktivitu.

### <a name="what-you-will-need-to-continue"></a>Co budete potřebovat k pokračování

V tomto scénáři s asistencí je nutné dodat testovací zařízení a testovacího uživatele. Ujistěte se, že jste dokončili následující úlohy:

- Nastavte účet testovacího uživatele v Azure Active Directory.
- Vytvořte testovací zařízení s Windows 10 verze 1903 nebo novější.
- Volitelné [Zaregistrujte testovací zařízení pomocí modulu Windows autopilot](../enrollment/enrollment-autopilot.md#add-devices).
- Volitelné Povolte [branding na přihlašovací stránce Azure Active Directory vaší organizace](https://go.microsoft.com/fwlink/?linkid=2102455).

## <a name="step-2---user"></a>Krok 2 – uživatel

Vyberte uživatele, kterého chcete na zařízení nastavit. Tato osoba bude primárním uživatelem zařízení.

Pokud chcete do této konfigurace přidat další uživatele nebo zařízení, stačí přidat uživatele a zařízení do skupin zabezpečení AAD generovaných průvodcem. Na rozdíl od jiných scénářů s asistencí nemusíte spustit Průvodce více než jednou, protože konfigurace není přizpůsobitelná. Stačí přidat další uživatele a zařízení do vytvořených skupin AAD. Po dokončení průvodce budete moct zobrazit skupinu vygenerovanou doporučenými nasazenými policejními.

## <a name="step-3---device"></a>Krok 3 – zařízení

Ujistěte se, že na zařízení běží Windows 10 verze 1903 nebo novější.  Primární uživatel bude muset zařízení nastavit, když ho dostanou. Pro uživatele jsou k dispozici dvě možnosti instalace.

### <a name="option-a--windows-autopilot"></a>Možnost A – Windows autopilot

Windows autopiloter automatizuje konfiguraci nových zařízení, aby je uživatelé mohli nastavovat mimo jiné bez pomoci. Pokud je vaše zařízení už zaregistrované u Windows autopilotu, vyberte ho podle jeho sériového čísla. Další informace o použití automatického pilotního nasazení systému Windows najdete v tématu [registrace zařízení pomocí automatického pilotního projektu Windows (volitelné)](../fundamentals/guided-scenarios-cloud-managed-pc.md#register-device-with-windows-autopilot-optional).

### <a name="option-b--manual-device-enrollment"></a>Možnost B – Ruční registrace zařízení

Uživatelé ručně nastaví a zaregistrují nová zařízení ve správě mobilních zařízení. Po dokončení tohoto scénáře resetujte zařízení a poskytněte primárnímu uživateli pokyny k registraci pro zařízení s Windows. Další informace najdete v tématu [připojení zařízení s Windows 10 k Azure AD během prvního spuštění prostředí](https://docs.microsoft.com/azure/active-directory/devices/azuread-joined-devices-frx#joining-a-device).

## <a name="step-4---review--create"></a>Krok 4 – přezkoumání a vytvoření

Poslední krok vám umožní zkontrolovat souhrn nastavení, která jste nakonfigurovali. Po kontrole voleb klikněte na **nasadit** a dokončete scénář s asistencí. Po dokončení průvodce se zobrazí tabulka prostředků. Tyto prostředky můžete upravit později. když ale necháte souhrnné zobrazení, tabulka se neuloží.

> [!IMPORTANT]
> Po dokončení průvodce se zobrazí souhrn. Prostředky uvedené v souhrnu můžete upravit později, ale Tabulka zobrazující tyto prostředky se neuloží.

### <a name="verification"></a>Ověření

1. Ověřte, že vybraná možnost má přiřazený obor uživatele MDM.
    - Zajistěte, aby byl [uživatelský rozsah MDM](../enrollment/windows-enroll.md#enable-windows-10-automatic-enrollment) :
        - Nastavte na **vše** pro aplikaci **Microsoft Intune** nebo,
        - Nastavte na **nějaké**. Přidejte také skupinu uživatelů vytvořenou tímto scénářem s asistencí.
2. Ověřte, jestli je vybraný uživatel schopný připojit zařízení k Azure Active Directory.
    - Ujistěte se, že je připojení AAD:
        - Nastavte na **vše** nebo,
        - Nastavte na **nějaké**. Přidejte také skupinu uživatelů vytvořenou tímto scénářem s asistencí.
3. Postupujte podle příslušných kroků v zařízení a připojte je k Azure AD na základě následujících kroků:
    - S autopilotem. Další informace najdete v tématu [režim založený na uživatelském režimu Windows autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven).
    - Bez automatického pilotního nasazení: Další informace najdete v tématu [připojení zařízení s Windows 10 k Azure AD během prvního spuštění prostředí](https://docs.microsoft.com/azure/active-directory/devices/azuread-joined-devices-frx#joining-a-device).

### <a name="what-happens-when-i-click-deploy"></a>Co se stane, když kliknu na nasadit?
Uživatel a zařízení se přidají do nových skupin zabezpečení. Budou taky nakonfigurované s použitím nastavení doporučeného pro zabezpečení a produktivitu v práci nebo ve škole. Jakmile uživatel připojí zařízení k Azure AD, do zařízení se přidají další aplikace a nastavení. Další informace o těchto dalších konfiguracích najdete v tématu [rychlý Start: registrace zařízení s Windows 10](../enrollment/quickstart-enroll-windows-device.md).

## <a name="additional-information"></a>Další informace

### <a name="register-device-with-windows-autopilot-optional"></a>Registrace zařízení pomocí Windows autopilotu (volitelné)

Volitelně můžete zvolit použití registrovaného autopilotního zařízení. U automatického pilotního scénáře přiřadí tento průvodce profil nasazení autopilotu a profil stránky stavu registrace. Profil nasazení autopilotu se nakonfiguruje takto:

- Režim řízený uživatelem – tj. vyžaduje, aby koncový uživatel zadal uživatelské jméno a heslo během instalace systému Windows.
- Připojení k Azure AD.
- Přizpůsobení instalačního programu systému Windows:
  - Skrýt obrazovku licenční podmínky pro software společnosti Microsoft
  - Skrýt nastavení ochrany osobních údajů 
  - Vytvoření místního profilu uživatele bez oprávnění místního správce
  - Skrýt možnosti změnit účet na přihlašovací stránce podnikového přihlášení

Stránka stavu registrace se nakonfiguruje tak, aby se povolila jenom pro zařízení autopilotu, a neblokuje čekání na instalaci všech aplikací.

Ve scénáři s asistencí se uživatel přiřadí k vybranému zařízení autopilotu pro individuální nastavení.

#### <a name="post-requisites"></a>Po požadavku

Jakmile uživatel připojí zařízení k Azure Active Directory, na zařízení se použijí následující konfigurace:

1. Do počítače spravovaného v cloudu se automaticky nainstaluje Office 365 ProPlus. Zahrnuje aplikace, se kterými jste obeznámeni, včetně přístupu, Excelu, OneNotu, Outlooku, PowerPointu, vydavatele, Skypu pro firmy a Wordu. Tyto aplikace můžete použít pro připojení ke službám Office 365, jako je SharePoint Online, Exchange Online a Online Skype pro firmy. Sada Office 365 ProPlus se pravidelně aktualizuje novými funkcemi, na rozdíl od verzí Office, které nejsou předplatné. Seznam nových funkcí najdete v tématu Co je nového v Office 365.
2. Do počítače spravovaného v cloudu se nainstalují standardní hodnoty zabezpečení systému Windows. Pokud jste nastavili rozšířenou ochranu před internetovými útoky v programu Microsoft Defender, ve scénáři s asistencí se také nakonfigurují základní nastavení pro Defender. Program Defender Advanced Threat Protection poskytuje novou vrstvu ochrany před porušením zásobníku pro Windows 10 Security. Díky kombinaci technologie klienta integrované do systému Windows 10 a robustní cloudové služby vám pomůže detekovat hrozby, které provedly v minulosti po jiné obrany. 

## <a name="next-steps"></a>Další kroky

- Pokud používáte pokročilou detekci hrozeb v programu Microsoft Defender, vytvořte [zásady dodržování předpisů Intune](../protect/advanced-threat-protection.md#create-and-assign-the-compliance-policy) , které budou vyžadovat analýzu hrozeb v Defenderu, aby splňovaly dodržování předpisů.
- Vytvořte [zásady podmíněného přístupu na základě zařízení](../protect/advanced-threat-protection.md#create-a-conditional-access-policy) , které zablokují přístup, pokud zařízení nesplňuje podmínky Intune.
