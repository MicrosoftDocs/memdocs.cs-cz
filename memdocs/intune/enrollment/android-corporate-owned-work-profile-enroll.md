---
title: Nastavení registrace Intune pro zařízení s Androidem Enterprise ve vlastnictví firmy s pracovním profilem
titleSuffix: Microsoft Intune
description: Naučte se registrovat zařízení vlastněná podnikem v Androidu s pracovním profilem v Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 7/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: shthilla
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9a19a78002d0655cf63a8b757ea252fb8992603f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915258"
---
# <a name="set-up-intune-enrollment-of-android-enterprise-corporate-owned-devices-with-work-profile"></a>Nastavení registrace zařízení s Androidem Enterprise vlastněných podnikem v Intune s pracovním profilem

Zařízení s Androidem Enterprise, která jsou ve vlastnictví firmy s pracovním profilem, jsou jediná uživatelská zařízení, která jsou určená pro podnikové a osobní použití.

Koncoví uživatelé můžou uchovávat své pracovní a osobní údaje odděleně a jsou zaručené, že jejich osobní data a aplikace zůstanou soukromé. Správci můžou řídit některá nastavení a funkce pro celé zařízení, včetně těchto:

- Nastavení požadavků pro heslo zařízení
- Řízení Bluetooth a roaming dat
- Konfigurace ochrany továrního obnovení

Intune vám pomůže nasadit aplikace a nastavení do zařízení se systémem Android Enterprise ve vlastnictví firmy pomocí pracovního profilu. Konkrétní podrobnosti o Androidu Enterprise najdete v tématu [požadavky na Android Enterprise](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).

## <a name="device-requirements"></a>Požadavky na zařízení

Zařízení musí splňovat tyto požadavky, aby je bylo možné spravovat jako zařízení s pracovními profily ve vlastnictví firmy Android Enterprise:

- Operační systém Android verze 8,0 a vyšší.
- Zařízení musí používat distribuci Androidu s připojením ke službě GMS (Google Mobile Services). Zařízení musí mít dostupnou službu GMS a musí být schopna se k této službě připojit.

## <a name="set-up-android-enterprise-corporate-owned-work-profile-device-management"></a>Nastavení správy zařízení pracovního profilu ve vlastnictví firmy Android Enterprise

Chcete-li nastavit správu zařízení pracovního profilu ve vlastnictví firmy Android Enterprise, postupujte takto:

1. Při přípravě na správu mobilních zařízení musíte [nastavit autoritu pro správu mobilních zařízení (MDM) na **Microsoft Intune**](../fundamentals/mdm-authority-set.md) podle pokynů. Tato možnost se nastavuje jenom jednou při prvním nastavování Intune pro správu mobilních zařízení.
2. [Připojte svůj účet tenanta Intune k vašemu spravovanému účtu Google Play](connect-intune-android-enterprise.md).
3. [Vytvořte profil zápisu.](#create-an-enrollment-profile)
4. [Vytvořte skupinu zařízení](#create-a-device-group).
5. [Zaregistrujte zařízení pracovních profilů vlastněných společností](#enroll-the-corporate-owned-work-profile-devices).

### <a name="create-an-enrollment-profile"></a> Vytvoření profilu zápisu

> [!NOTE]
> Tokeny pro zařízení vlastněná společností s pracovním profilem nebudou automaticky vypršet. Pokud se správce rozhodne o odvolání tokenu, nezobrazí se v **zařízeních**se systémem  >  **Android**  >  **Android registrace**  >  **zařízení vlastněných společností s pracovním profilem (Preview)**, že se k němu přidružený profil nezobrazuje. Pokud chcete zobrazit všechny profily přidružené k aktivním i neaktivním tokenům, klikněte na **Filtr** a zaškrtněte políčka u možnosti aktivní i neaktivní stavy zásad. 

Je nutné vytvořit registrační profil, aby uživatelé mohli registrovat zařízení pracovních profilů vlastněných společností. Po vytvoření poskytne tento profil registrační token (náhodný řetězec) a kód QR. V závislosti na operačním systému Android a verzi zařízení můžete použít buď token, nebo kód QR k [registraci vyhrazeného zařízení](#enroll-the-corporate-owned-work-profile-devices).

1. Přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) a vyberte **zařízení**  >  **Android**Android  >  **registrace**  >  **zařízení vlastněných společností pomocí pracovního profilu (Preview)**.
2. Vyberte **vytvořit profil** a vyplňte pole.
    - **Název**: Zadejte název, který použijete při přiřazení tohoto profilu k dynamické skupině zařízení.
    - **Popis**: přidejte popis profilu (volitelné).
3. Zvolte **Další**.
5. Na stránce **Revize + vytvořit** vyberte **vytvořit** a vytvořte zásadu.

### <a name="create-a-device-group"></a>Vytvoření skupiny zařízení

Aplikace a zásady můžete cílit buď na přiřazené, nebo dynamické skupiny zařízení. Pomocí následujících kroků můžete nakonfigurovat dynamické skupiny zařízení Azure AD tak, aby automaticky naplnily zařízení zaregistrovaná pomocí konkrétního profilu zápisu:

1. Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) a vyberte **skupiny**  >  **všechny skupiny**  >  **Nová skupina**.
2. V okně **Skupina** vyplňte požadovaná pole následujícím způsobem:
    - **Typ skupiny**: Zabezpečení
    - **Název skupiny**: Zadejte výstižný název (například Zařízení závodu 1).
    - **Typ členství**: Dynamické zařízení
3. Zvolte **Přidat dynamický dotaz**.
4. V okně **Pravidla dynamického členství** vyplňte pole následujícím způsobem:
    - **Přidat dynamické pravidlo členství**: Jednoduché pravidlo
    - **Přidat zařízení, kde**: Název registračního profilu
    - V prostředním poli vyberte **Equals (rovná**se).
    - Do posledního pole zadejte název dříve vytvořeného registračního profilu.
    Další informace o pravidlech dynamického členství najdete v tématu [Pravidla dynamického členství pro skupiny v AAD](/azure/active-directory/users-groups-roles/groups-dynamic-membership). 
5. Klikněte **na tlačítko Přidat dotaz**  >  **vytvořit**.

### <a name="revoke-tokens"></a>Odvolat tokeny

Platnost tokenu nebo kódu QR můžete hned ukončit. Od tohoto okamžiku nebude token nebo kód QR použitelný. Tuto možnost můžete použít, pokud:
  - Omylem nasdílíte token nebo kód QR s neautorizovanou stranou
  - Dokončíte všechny registrace a token nebo kód QR už nepotřebujete

Odvolání tokenu nebo kódu QR nebude mít žádný vliv na zařízení, která jsou už zaregistrovaná.

1. Přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) a vyberte **zařízení**  >  **Android**Android  >  **registrace**  >  **zařízení vlastněných společností pomocí pracovního profilu (Preview)**.
2. Zvolte profil, se kterým chcete pracovat.
3. Zvolte **Token**.
5. Chcete-li token odvolat, vyberte možnost **odvolat token**  >  **Ano**.

## <a name="enroll-the-corporate-owned-work-profile-devices"></a>Registrace zařízení pracovního profilu vlastněných společností

Uživatelé teď můžou [zaregistrovat svoje zařízení pracovních profilů vlastněných společností](android-dedicated-devices-fully-managed-enroll.md).

> [!NOTE]
> Aplikace **Microsoft Intune** se automaticky nainstaluje během registrace zařízení pracovního profilu vlastněné společností.  Tato aplikace se vyžaduje pro zápis a nedá se odinstalovat. 

## <a name="managing-apps-on-android-enterprise-corporate-owned-work-profile-devices"></a>Správa aplikací na zařízeních s pracovními profily vlastněných podnikem v Androidu

Na zařízeních s pracovními profily vlastněných podnikem v Androidu se můžou nainstalovat jenom aplikace, které mají typ přiřazení [nastaven na požadováno](../apps/apps-deploy.md#assign-an-app) . Aplikace se nainstalují ze spravovaného Google Play Storu stejným způsobem jako zařízení se systémem Android Enterprise Work Profile.

Když vývojář aplikace publikuje aktualizaci do obchodu Google Play, aktualizují se aplikace na spravovaných zařízeních automaticky.

Pokud chcete odebrat aplikaci ze zařízení s pracovním profilem ve vlastnictví společnosti Android Enterprise, můžete provést jednu z následujících akcí:
- Odstranění nasazení povinné aplikace
- Vytvoření nasazení odinstalace pro tuto aplikaci

## <a name="next-steps"></a>Další kroky
- [Nasazení aplikací pro Android](../apps/apps-deploy.md)
- [Přidat zásady konfigurace pro Android](../configuration/device-profiles.md)