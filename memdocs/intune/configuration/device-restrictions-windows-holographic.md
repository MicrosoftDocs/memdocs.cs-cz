---
title: Nastavení zařízení pro Windows holografické firmy – Microsoft Intune – Azure | Microsoft Docs
description: Přečtěte si o a nakonfigurujte nastavení omezení zařízení v Microsoft Intune pro Windows Holografick pro firmy. Řízení zrušení registrace, geografického umístění, hesel, instalace aplikací z App Storu, souborů cookie a automaticky otevíraných oken v Microsoft Edge, Microsoft Defenderu, hledání, cloudu a úložišti, připojení Bluetooth, systémový čas a data o využití.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2cd769b8e3ca4497c095210ea266d225354db24c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88912827"
---
# <a name="windows-holographic-for-business-device-settings-to-allow-or-restrict-features-using-intune"></a>Nastavení zařízení ve Windows-holografické pro firmy, které umožňuje povolit nebo zakázat funkce využívající Intune

Tento článek obsahuje seznam a popis různých nastavení, která můžete řídit na zařízeních s Windows holografickým pro firmy, jako je například Microsoft HoloLens. Jako součást řešení správy mobilních zařízení (MDM) pomocí těchto nastavení můžete povolit nebo zakázat funkce, zabezpečení a další funkce.

Jako správce Intune můžete vytvořit a přiřadit tato nastavení k vašim zařízením.

## <a name="before-you-begin"></a>Než začnete

[Vytvoří konfigurační profil omezení zařízení s Windows 10](device-restrictions-configure.md#create-the-profile).

Když vytvoříte konfigurační profil omezení zařízení s Windows 10, budete mít víc nastavení, než jaké je uvedené v tomto článku. Nastavení v tomto článku jsou podporovaná na zařízeních s Windows holografickým pro firmy.

## <a name="app-store"></a>App Store

- **Automatické aktualizace aplikací ze Storu**: **blok** zabraňuje automatické instalaci aktualizací z Microsoft Store. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat automatickou aktualizaci aplikací nainstalovaných z Microsoft Store.

  [CSP ApplicationManagement/AllowAppStoreAutoUpdate](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **Instalace důvěryhodných aplikací**: vyberte, jestli se můžou instalovat aplikace, které nejsou Microsoft Store, označované taky jako zkušební načtení. Probíhá instalace zkušebního načtení a následné spuštění nebo otestování aplikace, která není certifikována Microsoft Store. Například aplikace, která je interní pro vaši společnost. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Blok**: zabraňuje zkušebnímu načtení. NeMicrosoft Store aplikace se nedají nainstalovat.
  - **Povolit**: umožňuje zkušební načtení. Je možné nainstalovat aplikace, které nejsou Microsoft Store.

  [CSP ApplicationManagement/AllowAllTrustedApps](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **Odemčení pro vývojáře**: umožňuje povolit nastavení vývojářů pro Windows, jako je například umožnění úprav aplikací zkušebně načtené uživateli. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Blok**: znemožní vývojářský režim a aplikace pro zkušební načtení.
  - **Povolit**: povolí vývojářský režim a aplikace pro zkušební načtení.

  [CSP ApplicationManagement/AllowDeveloperUnlock](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowdeveloperunlock)

## <a name="cellular-and-connectivity"></a>Mobilní síť a připojení

- **Bluetooth**: **blok** znemožní uživatelům povolit Bluetooth. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém na zařízení umožňovat Bluetooth.

  [Připojení/AllowBluetooth CSP](/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowbluetooth)

- **Zjistitelnost Bluetooth**: **blok** zabraňuje zařízení, aby bylo zjistitelné jinými zařízeními podporujícími technologii Bluetooth. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém pro zjištění zařízení povolit jiná zařízení s podporou Bluetooth, jako je třeba sluchátka.

  [Zprostředkovatel kryptografických služeb Bluetooth/AllowDiscoverableMode](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **Inzerce Bluetooth**: **blok** zabraňuje zařízení v posílání reklamy Bluetooth. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zařízení odeslat reklamy Bluetooth.

  [Zprostředkovatel kryptografických služeb Bluetooth/AllowAdvertising](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

## <a name="cloud-and-storage"></a>Cloud a úložiště

- **Účet Microsoft**: **blok** zabraňuje uživatelům v přidružení účet Microsoft k zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém přidat a použít účet Microsoft.

  [Accounts/AllowMicrosoftAccountConnection CSP](/windows/client-management/mdm/policy-csp-accounts#accounts-allowmicrosoftaccountconnection)

## <a name="control-panel-and-settings"></a>Ovládací panely a nastavení

- **Změna systémového času**: **blok** znemožní uživatelům měnit nastavení data a času v zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit tato nastavení změnit.

  [Nastavení/CSP AllowDateTime](/windows/client-management/mdm/policy-csp-settings#settings-allowdatetime)

## <a name="general"></a>Obecné

- **Ruční zrušení registrace**: **blok** znemožní uživatelům odstranit pracovní účet pomocí ovládacích panelů na pracovišti na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  [Experience/AllowManualMDMUnenrollment CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowmanualmdmunenrollment)

- **Zeměpisná poloha**: **blok** zabraňuje uživatelům v zapínání služeb zjišťování polohy na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  [Experience/AllowFindMyDevice CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowfindmydevice)

- **Cortana**: **Block** zakáže hlasového asistenta Cortana na zařízení. Když je Cortana vypnutá, uživatelé můžou pořád vyhledávat položky v zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat Cortanu.

  [Experience/AllowCortana CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

## <a name="microsoft-edge-browser"></a>Prohlížeč Microsoft Edge

- **Úvodní prostředí**  >  **Povolit automaticky otevíraná okna**: **Ano** (výchozí) umožňuje automaticky otevíraná okna ve webovém prohlížeči. V prohlížeči **nebrání automaticky** otevíraná okna.

  [CSP pro Browser/AllowPopups](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)

- **Oblíbené položky a hledání**  >  **Zobrazit návrhy hledání**: **Ano** (výchozí) umožňuje vyhledávacímu webu navrhovat při psaní frází hledání na adresním řádku. Tato funkce **není** zabráněno.

  [CSP pro Browser/AllowSearchSuggestionsinAddressBar](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)

- **Ochrana osobních údajů a zabezpečení**  >  **Povolit správce hesel**: **Ano** (výchozí) umožňuje Microsoft Edge automaticky používat Správce hesel, který umožňuje uživatelům ukládat a spravovat hesla v zařízení. **No** zabrání Microsoft Edge v používání Správce hesel.

  [CSP pro Browser/AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)

- **Ochrana osobních údajů a zabezpečení**  >  **Soubory cookie**: Vyberte způsob zpracování souborů cookie ve webovém prohlížeči. Možnosti:
  - **Povoleno**: soubory cookie jsou uloženy v zařízení.
  - **Blokovat všechny soubory cookie**: soubory cookie nejsou uloženy v zařízení.
  - **Blokovat pouze soubory cookie třetích stran**: soubory cookie třetích stran nebo partnerů nejsou uloženy v zařízení.

  [CSP pro Browser/AllowCookies](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)

- **Ochrana osobních údajů a zabezpečení**  >  **Odeslat hlavičky do Not Track**: **Ano** odešle hlavičky do Not Track pro weby požadující informace o sledování (doporučeno). **Ne** (výchozí) neodesílají hlavičky, které umožňují webům sledovat uživatele. Uživatelé můžou toto nastavení nakonfigurovat.

  [CSP pro Browser/AllowDoNotTrack](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)

## <a name="microsoft-defender-smartscreen"></a>Filtr SmartScreen v programu Microsoft Defender

- **Filtr SmartScreen pro Microsoft Edge**: **vyžaduje** zapnutí funkce SmartScreen v programu Microsoft Defender a zabránění uživatelům v jejich vypnutí. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zapnout filtr SmartScreen a povolit uživatelům jeho zapnutí a vypnutí.

  [CSP pro Browser/AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

## <a name="password"></a>Heslo

- **Heslo**: **vyžaduje** , aby uživatelé zadali heslo pro přístup k zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat přístup k zařízením bez hesla. Platí jenom pro místní účty. Hesla doménového účtu zůstávají nakonfigurovaná službou Active Directory (AD) a službou Azure AD.

  [CSP DeviceLock/DevicePasswordEnabled](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

- **Vyžadovat heslo při návratu zařízení ze stavu nečinnosti**: **vyžaduje** , aby uživatelé po nečinnosti odemkli zařízení zadáním hesla. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí po nečinnosti vyžadovat kód PIN nebo heslo.

  [CSP DeviceLock/AllowIdleReturnWithoutPassword](/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

## <a name="reporting-and-telemetry"></a>Vytváření sestav a telemetrie

- **Sdílet data o využití**: vyberte úroveň diagnostických dat, která se odešlou. Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Žádné nastavení není vynuceno. Uživatelé zvolí úroveň, která je odeslána. Ve výchozím nastavení operační systém nemusí sdílet žádná data.
  - **Zabezpečení**: informace, které jsou nutné k zajištění vyššího zabezpečení systému Windows, včetně údajů o nastavení komponenty prostředí s připojeným uživatelem a telemetriem, nástroji pro odebrání škodlivého softwaru a programu Microsoft Defender
  - **Základní**: základní informace o zařízení, včetně dat týkajících se kvality, kompatibility aplikací, dat o využití aplikací a dat z úrovně zabezpečení
  - **Rozšířené**: Další přehledy, včetně toho, jak se používají Windows, Windows Server, System Center a aplikace, jak provádějí, pokročilá data o spolehlivosti a data ze základních i úrovní zabezpečení
  - **Úplné**: všechna data potřebná pro identifikaci a pomoc při řešení problémů a data ze zabezpečení, úrovně Basic a rozšířené úrovně.

  [CSP pro System/AllowTelemetry](/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

## <a name="search"></a>Hledat

- **Umístění pro hledání**: **blok** zabrání službě Windows Search v použití umístění. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto funkci dovolit.

  [Hledání/AllowSearchToUseLocation CSP](/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md)a [sledujte jeho stav](device-profile-monitor.md).