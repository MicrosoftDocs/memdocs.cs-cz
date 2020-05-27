---
title: Registrace zařízení s iOS/iPadOS v Intune
titleSuffix: Microsoft Intune
description: Nastavení registrace zařízení se systémem iOS/iPadOS v Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/23/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 439c33a6-e80c-4da9-ba09-a51fc36f62ad
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: bf413dc551d8be8fd646a03826fb3e5507f4d272
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988934"
---
# <a name="enroll-iosipados-devices-in-intune"></a>Registrace zařízení s iOS/iPadOS v Intune

Intune umožňuje správu mobilních zařízení (MDM) pro iPady a iPhone, aby uživatelé měli zabezpečený přístup k firemním e-mailům, datům a aplikacím.

Jako správce Intune můžete nastavit registraci pro zařízení s iOS/iPadOS a iPadOS, abyste měli přístup k prostředkům společnosti. Uživatelům můžete umožnit registraci zařízení vlastněných osobně, označované jako registrace vlastního zařízení (BYOD). Můžete také nastavit registraci zařízení vlastněných společností.

## <a name="prerequisites-for-iosipados-enrollment"></a>Předpoklady pro registraci zařízení se systémem iOS/iPadOS

Předtím, než budete moci povolit zařízení se systémem iOS/iPadOS, proveďte následující kroky:

- Ujistěte [se, že jsou vaše zařízení podporovaná](../fundamentals/supported-devices-browsers.md).
- [Nastavení Intune](../fundamentals/setup-steps.md) – tento postup slouží k nastavení infrastruktury Intune. Registrace zařízení vyžaduje zejména [nastavení autority MDM](../fundamentals/mdm-authority-set.md).
- [Získání certifikátu Apple MDM push Certificate](apple-mdm-push-certificate-get.md) – Apple vyžaduje certifikát, aby bylo možné povolit správu zařízení se systémem iOS/IPadOS a MacOS.

## <a name="user-owned-iosipados-and-ipados-devices-byod"></a>Zařízení s iOS/iPadOS a iPadOS vlastněná uživatelem (BYOD)

Uživatelům můžete umožnit, aby si zaregistrovali svoje osobní zařízení pro správu Intune. Tato možnost se označuje jako Přineste si vlastní zařízení neboli BYOD. Pro registraci uživatelů existují tři možnosti:
- Zásady ochrany aplikací poskytují nejsvětlejší možnosti BYOD a poskytují správu jenom na úrovni aplikace. Pokud ale chcete zařízení zabezpečit i pomocí šestého složeného kódu PIN, můžete tyto zásady použít spolu s zápisem uživatele.
- Registrace zařízení je to, co si můžete představit jako typické registraci BYOD. Poskytuje správcům široké spektrum možností správy.
- Registrace uživatele je efektivnější proces registrace, který poskytuje správcům podmnožinu možností správy zařízení. Tato funkce je aktuálně ve verzi Preview. 

Po dokončení požadavků a přiřazení uživatelských licencí si uživatelé můžou aplikaci Portál společnosti Intune stáhnout z App Storu a podle pokynů v aplikaci. Portál společnosti prohlášení o zásadách ochrany osobních údajů na zařízeních s iOS/iPadOS můžete přizpůsobit, jak je vysvětleno v tématu [jak přizpůsobit portál společnosti Intune aplikace, portál společnosti web a aplikaci Intune](../apps/company-portal-app.md#configuration).

## <a name="company-owned-iosipados-devices"></a>Zařízení s iOS/iPadOS vlastněná společností

V organizacích, které si kupují zařízení pro své uživatele, podporuje Intune následující metody registrace zařízení, které vlastní společnost pro iOS/iPadOS:

- Automatický zápis zařízení (ADE) společnosti Apple
- Apple School Manager
- Registrace Průvodce nastavením s Apple Configuratorem
- Přímá registrace pomocí Apple Configuratoru

Zařízení s iOS/iPadOS vlastněná společností můžete také zaregistrovat pomocí účtu [správce registrace zařízení](device-enrollment-manager-enroll.md) .

## <a name="automated-device-enrollment"></a>Automatická registrace zařízení

Organizace si můžou koupit zařízení s iOS/iPadOS prostřednictvím automatického zápisu zařízení (ADE) společnosti Apple. ADE umožňuje nasadit registrační profil přes Air, aby bylo možné zařízení spravovat. Další informace najdete v tématu [program registrace zařízení](device-enrollment-program-enroll-ios.md).

## <a name="user-enrollment"></a>Registrace uživatele
Registrace uživatele umožňuje správcům podmnožinu možností správy ve srovnání s jinými metodami registrace. Další informace najdete v tématech [podporované akce při registraci uživatelů, hesla a další možnosti](ios-user-enrollment-supported-actions.md) a [Nastavení registrace uživatelů pro iOS/iPadOS a iPadOS](ios-user-enrollment.md).

## <a name="apple-school-manager"></a>Apple School Manager

Apple School Manager je program nákupu a registrace zařízení pro školy. Podobně jako ADE můžete nasadit profil pro registraci zařízení v rámci správy. Další informace o [Apple School Manageru](apple-school-manager-set-up-ios.md).

## <a name="apple-configurator"></a>Apple Configurator

Můžete zaregistrovat zařízení s iOS/iPadOS pomocí Apple Configuratoru spuštěného na počítači Mac. Zařízení připravíte tak, že je připojíte přes USB a nainstalujete registrační profil. Zařízení můžete pomocí Apple Configuratoru registrovat dvěma způsoby:

- Registrace Pomocníka s nastavením – vymaže zařízení, připraví ho ke spuštění pomocníka s nastavením a nainstaluje zásady společnosti pro nového uživatele zařízení.
- Přímá registrace – Nevymaže zařízení a zaregistruje ho s předdefinovanými zásadami. Tato metoda je vhodná pro zařízení bez přidružení uživatele.

Přečtěte si další informace o [registraci pomocí Apple Configuratoru](apple-configurator-enroll-ios.md).

## <a name="use-the-company-portal-on-ade-enrolled-or-apple-configurator-enrolled-devices"></a>Použití Portál společnosti na zařízeních zaregistrovaných v ADE nebo Apple Configuratoru

Zařízení nakonfigurovaná s přidružením uživatele umožňují instalaci a spuštění aplikace Portál společnosti, která slouží ke stahování aplikací a správě zařízení. Když uživatelé obdrží zařízení, musí provést určitý počet dodatečných kroků, aby dokončili postup Pomocníka s nastavením a nainstalovali aplikaci Portál společnosti.

Přidružení uživatele je nezbytné pro podporu následujících funkcí:

- Aplikace MAM (správa mobilních aplikací)
- Podmíněný přístup k e-mailu a datům společnosti
- Aplikace Portál společnosti

### <a name="how-users-enroll-corporate-owned-iosipados-devices-with-user-affinity"></a>Jak uživatelé registrují zařízení s iOS/iPadOS vlastněná společností s přidružením uživatele

1. Když uživatel zapne své zařízení, zobrazí se výzva k dokončení postupu Pomocníka s nastavením.
2. Po dokončení nastavení se uživateli zobrazí výzva k zadání Apple ID. Aby mohlo zařízení nainstalovat aplikaci Portál společnosti, musí uživatel zadat Apple ID.
3. Zařízení se systémem iOS/iPadOS automaticky nainstaluje aplikaci Portál společnosti z App Storu.
4. Uživatelé by měli aplikaci Portál společnosti spustit a přihlásit se pomocí přihlašovacích údajů (jako je jedinečné osobní jméno nebo hlavní název uživatele), které jsou přidružené k jejich předplatnému v Intune.
5. Po přihlášení se registrace dokončí. Uživatelé teď můžou na zařízení používat kompletní sadu funkcí.

### <a name="about-corporate-owned-managed-devices-with-no-user-affinity"></a>O firemních spravovaných zařízeních bez přidružení uživatele

Zařízení nakonfigurovaná bez přidružení uživatele nepodporují aplikaci Portál společnosti a ta by se na ně neměla instalovat. Portál společnosti je určený pro uživatele, kteří mají firemní přihlašovací údaje a potřebují přístup k podnikovým prostředkům podle svých potřeb (třeba k e-mailu). Zařízení zaregistrovaná bez přidružení uživatele nejsou určená k tomu, aby se k nim přihlašoval jeden vyhrazený uživatel. Typickými případy použití zařízení zaregistrovaných bez přidružení uživatele jsou zařízení veřejných terminálů, pokladny nebo sdílená zařízení.

Pokud je potřeba přidružení uživatele, před registrací zařízení se ujistěte, že je pro registrační profil zařízení vybraná možnost **přidružení uživatele** . Pokud chcete stav přidružení zařízení změnit, musíte zařízení nejdřív vyřadit a potom ho znovu zaregistrovat.

## <a name="see-also"></a>Viz také

[Řešení potíží s registrací zařízení s iOS nebo iPadOS v Microsoft Intune](https://support.microsoft.com/help/4039809)
