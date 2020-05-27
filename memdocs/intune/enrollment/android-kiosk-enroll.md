---
title: Nastavení registrace Intune pro vyhrazená podniková zařízení s Androidem
titleSuffix: Microsoft Intune
description: Přečtěte si, jak v Intune zaregistrovat podniková vyhrazená zařízení s Androidem.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 1/15/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 544db0c11894967eca71a5b8c2e107e0fab47ef5
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989002"
---
# <a name="set-up-intune-enrollment-of-android-enterprise-dedicated-devices"></a>Nastavení registrace Intune pro vyhrazená podniková zařízení s Androidem

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Android Enterprise podporuje zařízení s veřejným veřejným stylem, který je ve vlastnictví firmy, a má nastavené řešení pro zařízení s jedním použitím. Taková zařízení se používají k jednomu účelu, například jako zobrazovací zařízení na veřejných místech, k tisku vstupenek nebo k evidenci zásob. Správci omezí použití zařízení na omezenou sadu aplikací a webových odkazů. Uživatelé zároveň nemůžou na tomto zařízení přidávat jiné aplikace ani provádět jiné akce.

Intune vám pomůže nasadit aplikace a nastavení na vyhrazená zařízení s Androidem Enterprise. Konkrétní podrobnosti o Androidu Enterprise najdete v tématu [požadavky na Android Enterprise](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).

Zařízení, která se spravují tímto způsobem, jsou v Intune zaregistrovaná bez uživatelského účtu a nejsou přidružená k žádnému koncovému uživateli. Nejsou určená pro osobní používání aplikací, které závisejí na datech spojených s účtem konkrétního uživatele, jako je Outlook nebo Gmail.

## <a name="device-requirements"></a>Požadavky na zařízení

Zařízení musí splňovat tyto požadavky, aby je bylo možné spravovat jako vyhrazené zařízení se systémem Android Enterprise:

- Operační systém Android verze 6,0 a vyšší.
- Zařízení musí používat distribuci Androidu s připojením ke službě GMS (Google Mobile Services). Zařízení musí mít dostupnou službu GMS a musí být schopna se k této službě připojit.

## <a name="set-up-android-enterprise-dedicated-device-management"></a>Nastavení správy vyhrazených zařízení s Androidem Enterprise

Chcete-li nastavit správu vyhrazené správy zařízení s Androidem Enterprise, postupujte podle následujících kroků:

1. Při přípravě na správu mobilních zařízení musíte [nastavit autoritu pro správu mobilních zařízení (MDM) na **Microsoft Intune**](../fundamentals/mdm-authority-set.md) podle pokynů. Tato možnost se nastavuje jenom jednou při prvním nastavování Intune pro správu mobilních zařízení.
2. [Připojte svůj účet tenanta Intune k vašemu spravovanému účtu Google Play](connect-intune-android-enterprise.md).
3. [Vytvořte profil zápisu.](#create-an-enrollment-profile)
4. [Vytvořte skupinu zařízení](#create-a-device-group).
5. [Zaregistrujte vyhrazená zařízení](#enroll-the-dedicated-devices).

### <a name="create-an-enrollment-profile"></a> Vytvoření profilu zápisu

> [!NOTE]
> Pokud platnost tokenu vypršela, neobjeví se v **zápisu zařízení registrace zařízení**s  >  **Androidem**ve  >  **vlastnictví firmy**zařízení, která jsou k němu přidružená. Pokud chcete zobrazit všechny profily přidružené k aktivním i neaktivním tokenům, klikněte na **Filtr** a zaškrtněte políčka u možnosti aktivní i neaktivní stavy zásad. 

Je nutné vytvořit registrační profil, abyste mohli zaregistrovat vyhrazená zařízení. Po vytvoření poskytne tento profil registrační token (náhodný řetězec) a kód QR. V závislosti na operačním systému Android a verzi zařízení můžete použít buď token, nebo kód QR k [registraci vyhrazeného zařízení](#enroll-the-dedicated-devices).

1. Přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) a vyberte **zařízení**  >  **Android**Android  >  **registrace**  >  **vyhrazených zařízení vlastněných společností**.
2. Zvolte **Vytvořit** a vyplňte požadovaná pole.
    - **Název**: Zadejte název, který použijete při přiřazení tohoto profilu k dynamické skupině zařízení.
    - **Datum vypršení platnosti tokenu**: Datum, kdy vyprší platnost tokenu. Google vynucuje maximálně 90 dnů.
3. Uložte profil pomocí tlačítka **Vytvořit**.

### <a name="create-a-device-group"></a>Vytvoření skupiny zařízení

Aplikace a zásady můžete cílit buď na přiřazené, nebo dynamické skupiny zařízení. Následujícím postupem nakonfigurujete dynamické skupiny zařízení služby AAD tak, aby se automaticky naplnily zařízeními, která se zaregistrují s konkrétním registračním profilem:

1. Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) a vyberte **skupiny**  >  **všechny skupiny**  >  **Nová skupina**.
2. V okně **Skupina** vyplňte požadovaná pole následujícím způsobem:
    - **Typ skupiny**: zabezpečení
    - **Název skupiny**: Zadejte výstižný název (například Zařízení závodu 1).
    - **Typ členství**: Dynamické zařízení
3. Zvolte **Přidat dynamický dotaz**.
4. V okně **Pravidla dynamického členství** vyplňte pole následujícím způsobem:
    - **Přidat dynamické pravidlo členství**: Jednoduché pravidlo
    - **Přidat zařízení, kde**: Název registračního profilu
    - V prostředním poli vyberte **Equals (rovná**se).
    - Do posledního pole zadejte název dříve vytvořeného registračního profilu.
    Další informace o pravidlech dynamického členství najdete v tématu [Pravidla dynamického členství pro skupiny v AAD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership). 
5. Klikněte **na tlačítko Přidat dotaz**  >  **vytvořit**.

### <a name="replace-or-remove-tokens"></a>Nahrazení nebo odebrání tokenů

- **Nahrazení tokenu**: Příkazem Nahradit token můžete vygenerovat nový token nebo kód QR, pokud brzy vyprší platnost stávajícího.
- **Odvolání tokenu**: Platnost tokenu nebo kódu QR můžete nechat okamžitě vypršet. Od tohoto okamžiku nebude token nebo kód QR použitelný. Tuto možnost můžete použít, pokud:
  - Omylem nasdílíte token nebo kód QR s neautorizovanou stranou
  - Dokončíte všechny registrace a token nebo kód QR už nepotřebujete

Nahrazení nebo odvolání tokenu/kódu QR nebude mít žádný vliv na zařízení, která už jsou zaregistrovaná.

1. Přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) a vyberte **zařízení**  >  **Android**Android  >  **registrace**  >  **vyhrazených zařízení vlastněných společností**.
2. Zvolte profil, se kterým chcete pracovat.
3. Zvolte **Token**.
4. Pokud chcete token nahradit, zvolte **Nahradit token**.
5. Pokud chcete token odvolat, zvolte **Odvolat token**.

## <a name="enroll-the-dedicated-devices"></a>Registrace vyhrazených zařízení

Můžete teď [zaregistrovat vyhrazená zařízení](android-dedicated-devices-fully-managed-enroll.md).

> [!NOTE]
> Aplikace **Microsoft Intune** se automaticky nainstaluje při registraci vyhrazeného zařízení.  Tato aplikace se vyžaduje pro zápis a nedá se odinstalovat. 

## <a name="managing-apps-on-android-enterprise-dedicated-devices"></a>Správa aplikací na vyhrazených zařízeních s Androidem Enterprise

Na vyhrazených zařízeních s Androidem Enterprise se můžou nainstalovat jenom aplikace, které mají typ přiřazení [nastaven na požadováno](../apps/apps-deploy.md#assign-an-app) . Aplikace se nainstalují ze spravovaného Google Play Storu stejným způsobem jako zařízení se systémem Android Enterprise Work Profile.

Když vývojář aplikace publikuje aktualizaci do obchodu Google Play, aktualizují se aplikace na spravovaných zařízeních automaticky.

Pokud chcete odebrat aplikaci z vyhrazených zařízení s Androidem Enterprise, můžete provést jednu z následujících akcí:
- Odstranění nasazení povinné aplikace
- Vytvoření nasazení odinstalace pro tuto aplikaci

## <a name="next-steps"></a>Další kroky
- [Nasazení aplikací pro Android](../apps/apps-deploy.md)
- [Přidat zásady konfigurace pro Android](../configuration/device-profiles.md)
