---
title: Nastavení omezení zařízení s Windows 10 v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na seznam všech nastavení a jejich popisů pro vytváření omezení zařízení v zařízeních s Windows 10 a novějším. Pomocí těchto nastavení můžete v konfiguračním profilu řídit snímky obrazovky, požadavky na heslo, nastavení veřejného terminálu, aplikace v obchodě, prohlížeči Microsoft Edge, Microsoft Defender, přístup ke cloudu, nabídce Start a další informace v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: e6304c35d93d717be13a564b5bf5dd2bdc0f84d5
ms.sourcegitcommit: d56e1c84e687fe18810f3b81e0a0617925fe6044
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/14/2020
ms.locfileid: "86303449"
---
# <a name="windows-10-and-newer-device-settings-to-allow-or-restrict-features-using-intune"></a>Nastavení zařízení s Windows 10 (a novějším) pro povolení nebo omezení funkcí pomocí Intune

Tento článek obsahuje seznam a popis všech různých nastavení, která můžete řídit na zařízeních s Windows 10 a novějším. V rámci řešení pro správu mobilních zařízení (MDM) pomocí těchto nastavení můžete povolit nebo zakázat funkce, nastavit pravidla pro hesla, přizpůsobit zamykací obrazovce, používat Microsoft Defender a další.

Tato nastavení se přidají do konfiguračního profilu zařízení v Intune a pak se přiřadí nebo nasadí na vaše zařízení s Windows 10.

> [!Note]
> Ne všechny možnosti jsou k dispozici ve všech edicích systému Windows. Pokud chcete zobrazit podporované edice, přečtěte si téma [zásady CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider) (otevře se další web společnosti Microsoft).
>  
> V profilu omezení zařízení s Windows 10 se většina konfigurovatelných nastavení nasadí na úrovni zařízení pomocí skupin zařízení. Zásady nasazené do skupin uživatelů se vztahují na cílové uživatele a vztahují se na uživatele, kteří mají licenci Intune, a přihlaste se k tomuto zařízení.

## <a name="before-you-begin"></a>Než začnete

[Vytvořte profil omezení zařízení s Windows 10](device-restrictions-configure.md#create-the-profile).

## <a name="app-store"></a>App Store

Tato nastavení používají [zprostředkovatele CSP zásad ApplicationManagement](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement), který obsahuje také podporované edice Windows.

- **App Store (jenom mobilní)**: **blok** zabraňuje uživatelům v přístupu k obchodu s aplikacemi na mobilních zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit přístup k obchodu s aplikacemi.
- **Automatické aktualizace aplikací ze Storu**: **blok** zabraňuje automatické instalaci aktualizací z Microsoft Store. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat automatickou aktualizaci aplikací nainstalovaných z Microsoft Store.

  [CSP ApplicationManagement/AllowAppStoreAutoUpdate](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **Instalace důvěryhodných aplikací**: vyberte, jestli se můžou instalovat aplikace, které nejsou Microsoft Store, označované taky jako zkušební načtení. Probíhá instalace zkušebního načtení a následné spuštění nebo otestování aplikace, která není certifikována Microsoft Store. Například aplikace, která je interní pro vaši společnost. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Blok**: zabraňuje zkušebnímu načtení. NeMicrosoft Store aplikace se nedají nainstalovat.
  - **Povolit**: umožňuje zkušební načtení. Je možné nainstalovat aplikace, které nejsou Microsoft Store.

- **Odemčení pro vývojáře**: umožňuje povolit nastavení vývojářů pro Windows, jako je například umožnění úprav aplikací zkušebně načtené uživateli. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Blok**: znemožní vývojářský režim a aplikace pro zkušební načtení.
  - **Povolit**: povolí vývojářský režim a aplikace pro zkušební načtení.

  [Povolit pro vývoj zařízení](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development) Další informace o této funkci.
  
  [CSP ApplicationManagement/AllowAllTrustedApps](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **Sdílená data aplikací uživatele**: vyberte možnost **umožňuje** sdílet data aplikací mezi různými uživateli na stejném zařízení a dalšími instancemi této aplikace. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit sdílení dat s ostatními uživateli a dalšími instancemi stejné aplikace.

  [CSP ApplicationManagement/AllowSharedUserAppData](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowshareduserappdata)

- **Použít pouze privátní úložiště**: **povolí** možnost stahovat aplikace pouze z privátního úložiště a nestahovat z veřejného úložiště, včetně maloobchodního katalogu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat stažení aplikací z privátního úložiště a veřejného úložiště.

  [CSP ApplicationManagement/RequirePrivateStoreOnly](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-requireprivatestoreonly)

- **Spuštění aplikace pocházející ze Storu**: **blokování** zakáže všechny aplikace, které byly v zařízení předem nainstalovány, nebo stažené z Microsoft Store. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tyto aplikace otevřít.

  [CSP ApplicationManagement/DisableStoreOriginatedApps](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-disablestoreoriginatedapps)

- **Nainstalovat data aplikací na systémový svazek**: **blok** zastaví aplikacím ukládat data na systémový svazek zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat aplikacím ukládat data na diskový svazek.

  [CSP ApplicationManagement/RestrictAppDataToSystemVolume](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictappdatatosystemvolume)

- **Nainstalovat aplikace na systémovou jednotku**: **blokovat** znemožní aplikacím instalovat na systémovou jednotku na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat instalaci aplikací na systémovou jednotku.

  [CSP ApplicationManagement/RestrictAppToSystemVolume](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictapptosystemvolume)

- Záznam ze **hry (jenom Desktop)**: **blokování** zakáže zaznamenávání a vysílání her ve Windows. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat zaznamenávání a vysílání her.

  [CSP ApplicationManagement/AllowGameDVR](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowgamedvr)

- **Jenom aplikace ze Storu**: Toto nastavení určuje uživatelské prostředí, když uživatelé nainstalují aplikace z jiných míst než z Microsoft Store. Nebrání instalaci obsahu ze zařízení USB, síťových sdílených složek ani jiných zdrojů, které nejsou v Internetu. Pomocí důvěryhodného prohlížeče můžete zajistit, aby tato ochrana fungovala podle očekávání.

  Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení může operační systém uživatelům dovolit instalovat aplikace z jiných míst než z Microsoft Store, včetně aplikací definovaných v jiných nastaveních zásad.  
  - **Odkudkoli**: vypne doporučení pro aplikace a umožní uživatelům instalovat aplikace z libovolného místa.  
  - **Pouze úložiště**: záměrem je zabránit škodlivému obsahu, který by ovlivnil vaše uživatelská zařízení při stahování spustitelného obsahu z Internetu. Když se uživatelé pokusí nainstalovat aplikace z Internetu, instalace je blokovaná. Uživatelům se zobrazí zpráva, která doporučuje stahovat aplikace z Microsoft Store.
  - **Doporučení**: při instalaci aplikace z webu, který je k dispozici v Microsoft Store, se uživatelům zobrazí zpráva doporučující si ji stáhnout ze Storu.  
  - **Preferovat Store**: upozorní uživatele, když instalují aplikace z jiných míst než z Microsoft Store.

  [Zprostředkovatel SmartScreen/EnableAppInstallControl CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enableappinstallcontrol)

- **Uživatelský ovládací prvek pro instalace**: **blok** znemožní uživatelům měnit možnosti instalace, které jsou obvykle rezervované pro správce systému, jako je například zadání adresáře pro instalaci souborů. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení Instalační služba systému Windows může zabránit uživatelům v změně těchto možností instalace a některé z funkcí zabezpečení Instalační služba systému Windows se přeskočí.

  [CSP ApplicationManagement/MSIAllowUserControlOverInstall](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msiallowusercontroloverinstall)

- **Instalace aplikací se zvýšenými oprávněními**: **zablokování** Instalační služba systému Windows, aby při instalaci jakéhokoli programu do systému používaly zvýšená oprávnění. Tato oprávnění se rozšiřují na všechny programy. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může systém použít oprávnění aktuálního uživatele při instalaci programů, které správce systému neinstaluje nebo nenabízí.

  [CSP ApplicationManagement/MSIAlwaysInstallWithElevatedPrivileges](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msialwaysinstallwithelevatedprivileges)

- **Spouštěné aplikace**: Zadejte seznam aplikací, které se otevřou po přihlášení uživatele k zařízení. Nezapomeňte použít středníkem oddělený seznam názvů (PFN) aplikací pro Windows, které jsou odděleny středníky. Aby tyto zásady fungovaly, musí manifest v aplikacích pro Windows používat úlohu po spuštění.

  [CSP ApplicationManagement/LaunchAppAfterLogOn](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-launchappafterlogon)

## <a name="cellular-and-connectivity"></a>Mobilní síť a připojení

Tato nastavení používají [zásady připojení](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-connectivity) a zprostředkovatele kryptografických služeb sítě [Wi-Fi](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wifi) , které také uvádějí podporované edice Windows.

- **Mobilní datový kanál**: vyberte, jestli uživatelé můžou používat data, jako je procházení webu, při připojení k mobilní síti. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Uživatelé je můžou vypnout.
  - **Blok**: nepovoluje mobilní datový kanál. Uživatelé ji nemůžou zapnout.
  - **Povolit (není editovatelné)**: povoluje mobilní datový kanál. Uživatelé ji nemůžou vypnout.

- **Datový roaming**: **blokování** zabraňuje mobilním datovým roamingu v zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení platí, že při přístupu k datům může být roaming mezi sítěmi povolený.
- **VPN přes mobilní síť**: **blok** zabraňuje zařízení v přístupu k připojením VPN v případě připojení k mobilní síti. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém sítě VPN umožňovat použití libovolného připojení, včetně mobilních.
- **Roaming VPN přes mobilní síť** **: při** roamingu v mobilní síti zastaví zařízení přístup k připojením VPN. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém při roamingu způsobit připojení VPN.
- **Služba připojených zařízení**: **blok** zakáže komponentu platformy připojených zařízení (CDP). CDP umožňuje zjišťování a připojení k ostatním zařízením (přes Bluetooth/LAN nebo Cloud), aby podporovala spouštění vzdálených aplikací, vzdálené zasílání zpráv, relace vzdálených aplikací a další prostředí pro různé zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém povolit službu připojená zařízení, která umožňuje zjišťování a připojování k ostatním zařízením Bluetooth.
- **NFC**: **Block** zabraňuje možnostem technologie NFC (Near Field Communication). Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům umožnit, aby na zařízení povolili a nakonfigurovali funkce NFC.
- **Wi-Fi**: **blok** zabraňuje uživatelům v zařízení povolit, konfigurovat, konfigurovat a používat připojení Wi-Fi. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat připojení Wi-Fi.
- **Automaticky se připojovat k Wi-Fi hotspotům**: **blokování** znemožňuje zařízením automaticky se připojovat k Wi-Fi hotspotům. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém nechat zařízení automaticky se připojovat k bezplatným Wi-Fi hotspotům a automaticky pro připojení přijímat jakékoli podmínky a ujednání.
- **Ruční konfigurace Wi-Fi**: **blok** zabraňuje zařízením v připojení k Wi-Fi mimo sítě instalované na MDM serveru. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit přidat a nakonfigurovat vlastní síťové identifikátory SSID pro připojení Wi-Fi.
- **Interval kontroly sítě Wi-Fi**: zadejte, jak často zařízení hledají sítě Wi-Fi. Zadejte hodnotu od 1 (nejčastější) do 500 (nejméně časté). Výchozí hodnota je `0` (nula).

### <a name="bluetooth"></a>Bluetooth

Tato nastavení používají [poskytovatele zásad Bluetooth](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth), který obsahuje taky podporované edice Windows.

- **Bluetooth**: **blok** znemožní uživatelům povolit Bluetooth. **Nenakonfigurováno** (výchozí) povolí Bluetooth na zařízení.
- **Zjistitelnost Bluetooth**: **blok** zabraňuje zařízení, aby bylo zjistitelné jinými zařízeními podporujícími technologii Bluetooth. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém pro zjištění zařízení povolit jiná zařízení s podporou Bluetooth, jako je třeba sluchátka.

  [Zprostředkovatel kryptografických služeb Bluetooth/AllowDiscoverableMode](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **Předpárování Bluetooth**: **blokování** zabraňuje konkrétním zařízením Bluetooth, aby se automaticky spároval s hostitelským zařízením. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat Automatické párování s hostitelským zařízením.

  [Zprostředkovatel kryptografických služeb Bluetooth/AllowPrepairing](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowprepairing)

- **Inzerce Bluetooth**: **blok** zabraňuje zařízení v posílání reklamy Bluetooth. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zařízení odeslat reklamy Bluetooth.

  [Zprostředkovatel kryptografických služeb Bluetooth/AllowAdvertising](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

- **Dotyková připojení Bluetooth**: **blok** brání uživateli v použití páru SWIFT a dalších scénářů založených na blízkosti. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zařízení odeslat reklamy Bluetooth.

  [Zprostředkovatel kryptografických služeb Bluetooth/AllowPromptedProximalConnections](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections)

- **Povolené služby Bluetooth**: **přidejte** seznam povolených služeb a profilů Bluetooth jako šestnáctkové řetězce, například `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}` .

  [Průvodce používáním ServicesAllowedList](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#servicesallowedlist-usage-guide) obsahuje další informace o seznamu služeb.

  [Zprostředkovatel kryptografických služeb Bluetooth/ServicesAllowedList](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-servicesallowedlist)

## <a name="cloud-and-storage"></a>Cloud a úložiště

Tato nastavení používají [CSP v zásadách účtů](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-accounts), který obsahuje také podporované edice Windows.

> [!IMPORTANT]
> Blokování nebo zakázání těchto nastavení účet Microsoft může mít vliv na scénáře registrace, které vyžadují, aby se uživatelé přihlásili ke službě Azure AD. Například používáte [šetrnější pro Autopilotu](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove). Uživatelům se obvykle zobrazuje okno pro přihlášení k Azure AD. Pokud jsou tato nastavení nastavená tak, aby **blokovala** nebo **zakázala**, možnost přihlášení k Azure AD se nemusí zobrazit. Místo toho se uživatelům zobrazí výzva k přijetí smlouvy EULA a vytvoření místního účtu, který nemusí být požadovaný.

- **Účet Microsoft**: **blok** zabraňuje uživatelům v přidružení účet Microsoft k zařízení. **Blok** může mít také vliv na některé scénáře registrace, které se spoléhají na to, že uživatelé dokončí proces registrace. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém přidat a použít účet Microsoft.
- **Bez účet Microsoft**: **blok** zabraňuje uživatelům v přidávání účtů mimo Microsoft pomocí uživatelského rozhraní. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit přidat e-mailové účty, které nejsou přidružené k účet Microsoft.
- **Synchronizace nastavení pro účet Microsoft**: **blok** zabraňuje nastavení zařízení a aplikací přidružených k účet Microsoft k synchronizaci mezi zařízeními. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto synchronizaci způsobit.
- **Pomocník pro přihlášení k účtu Microsoft**: Tato služba operačního systému umožňuje uživatelům přihlašovat se k jejich účet Microsoft. Ve výchozím nastavení může operační systém uživatelům dovolit, aby spouštěli a zastavili službu wlidsvc ( **Microsoft account Signing Assistant** ).
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení může operační systém uživatelům dovolit, aby spouštěli a zastavili službu wlidsvc ( **Microsoft account Signing Assistant** ).
  - **Disabled (zakázáno**): nastaví službu Pomocník pro přihlášení do Microsoftu (wlidsvc) na zakázanou a zabrání tak uživatelům v ručním spuštění.

      **Zakažte** také může mít vliv na některé scénáře registrace, které se spoléhají na to, že uživatelé dokončí registraci. Například používáte [šetrnější pro Autopilotu](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove). Uživatelům se obvykle zobrazuje okno pro přihlášení k Azure AD. Pokud je nastavené na **Zakázat**, možnost přihlášení k Azure AD se nemusí zobrazit. Místo toho se uživatelům zobrazí výzva k přijetí smlouvy EULA a vytvoření místního účtu, který nemusí být požadovaný.

## <a name="cloud-printer"></a>Cloudová tiskárna

Tato nastavení používají [zprostředkovatele CSP zásad EnterpriseCloudPrint](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-enterprisecloudprint), který obsahuje také podporované edice Windows.

- **Adresa URL pro zjišťování tiskáren**: zadejte adresu URL pro hledání cloudových tiskáren. Zadejte například `https://cloudprinterdiscovery.contoso.com`.
- **Adresa URL autority pro přístup k tiskárně**: zadejte adresu URL koncového bodu ověřování a získejte tokeny OAuth. Zadejte například `https://azuretenant.contoso.com/adfs`.
- **Identifikátor GUID nativní klientské aplikace Azure**: zadejte identifikátor GUID klientské aplikace, kterým se povoluje získat tokeny OAuth z OAuthAuthority. Zadejte například `E1CF1107-FF90-4228-93BF-26052DD2C714`.
- **Identifikátor URI prostředku tiskové služby**: zadejte identifikátor URI prostředku OAuth pro tiskovou službu nakonfigurovanou ve Azure Portal. Zadejte například `http://MicrosoftEnterpriseCloudPrint/CloudPrint`.
- **Maximální počet tiskáren pro dotaz**: zadejte maximální počet tiskáren, na které chcete zadat dotaz. Výchozí hodnota je `20`.
- **Identifikátor URI prostředku služby zjišťování tiskáren**: zadejte identifikátor URI prostředku OAuth pro službu zjišťování tiskáren nakonfigurovanou v Azure Portal. Zadejte například `http://MopriaDiscoveryService/CloudPrint`.

> [!TIP]
> Po nastavení [tisku hybridního cloudu Windows serveru](https://docs.microsoft.com/windows-server/administration/hybrid-cloud-print/hybrid-cloud-print-overview)můžete tato nastavení nakonfigurovat a pak nasadit na vaše zařízení s Windows.

## <a name="control-panel-and-settings"></a>Ovládací panely a nastavení

- **Nastavení aplikace**: **blok** znemožní uživatelům přístup k aplikaci nastavení systému Windows. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit, aby na zařízení otevřeli aplikaci nastavení.
  - **System**: **Block** znemožní přístup k systémové oblasti aplikace nastavení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
    - **Změny nastavení napájení a režimu spánku** (jenom desktopové služby): **blokovat** znemožní uživatelům měnit nastavení napájení a režimu spánku na zařízení. **Nenakonfigurováno** (výchozí) umožňuje uživatelům změnit nastavení napájení a režimu spánku.
  - **Zařízení**: **blok** znemožní přístup k oblasti zařízení aplikace nastavení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
  - **Síť Internet**: **blok** znemožní přístup k síti & internetovou oblast aplikace nastavení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
  - **Přizpůsobení**: **blok** brání v přístupu k oblasti přizpůsobení aplikace nastavení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
  - **Aplikace**: **blok** znemožní přístup k oblasti aplikace v aplikaci nastavení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
  - **Accounts**: **Block** zabrání přístupu k oblasti účtů aplikace nastavení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
  - **Čas a jazyk**: **blok** znemožní přístup k oblasti času & jazyka aplikace nastavení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
    - **Změna systémového času**: **blok** znemožní uživatelům měnit nastavení data a času v zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Uživatelé můžou tato nastavení změnit.
    - **Změny nastavení oblasti** (jenom desktopové): **blokovat** znemožní uživatelům měnit nastavení oblasti na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Uživatelé můžou tato nastavení změnit.
    - **Změny nastavení jazyka (jenom desktopové verze)**: **blokovat** znemožní uživatelům měnit nastavení jazyka v zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Uživatelé můžou tato nastavení změnit.

      [Zásady nastavení – CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings)

  - **Hraní her**: **blok** znemožní přístup k herní oblasti aplikace nastavení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
  - **Usnadnění přístupu**: **blok** znemožní přístup k oblasti snadného přístupu v aplikaci nastavení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
  - **Ochrana osobních údajů**: **blok** znemožní přístup k oblasti soukromí v aplikaci nastavení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
  - **Aktualizace a zabezpečení**: **blok** znemožní přístup k oblasti zabezpečení & aktualizace aplikace nastavení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

## <a name="display"></a>Zobrazení

Tato nastavení používají [zprostředkovatele kryptografických služeb pro zobrazení](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-display), který obsahuje taky podporované edice Windows.

Škálování DPI GDI umožňuje aplikacím, které nepodporují rozlišení DPI, přesměrovat na monitorované rozlišení DPI.

- **Zapnout ŠKÁLOVÁNÍ GDI pro aplikace**: **přidejte** starší verze aplikací, u kterých chcete zapnout škálování dpi GDI. Zadejte například `filename.exe` nebo `%ProgramFiles%\Path\Filename.exe`.

  Měřítko DPI GDI je zapnuté pro všechny starší verze aplikací v seznamu.

- **Vypnout škálování GDI pro aplikace**: **přidejte** starší verze aplikací, u kterých chcete škálování dpi GDI vypnuté. Zadejte například `filename.exe` nebo `%ProgramFiles%\Path\Filename.exe`.

  Měřítko DPI GDI je vypnuto pro všechny starší aplikace v seznamu.

Můžete také **naimportovat** soubor. CSV se seznamem aplikací.

## <a name="general"></a>Obecné

Tato nastavení používají [zprostředkovatele kryptografických služeb (CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience)), který obsahuje taky podporované edice Windows. 

- **Snímek obrazovky** (jenom mobilní): **blok** znemožní uživatelům získat na zařízení snímky obrazovky. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Kopírování a vkládání (jenom mobilní)**: **blok** brání uživatelům v používání kopírování a vkládání mezi aplikacemi na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Ruční zrušení registrace**: **blok** znemožní uživatelům odstranit pracovní účet pomocí ovládacích panelů na pracovišti na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  Nastavení této zásady se nepoužije, pokud je počítač připojený k Azure AD a je povolená Automatická registrace.

- **Ruční instalace kořenového certifikátu** (jenom mobilní zařízení): **blok** zabraňuje uživatelům v ruční instalaci kořenových certifikátů a zprostředkujících certifikátů Cap. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Kamera**: **Block** zabraňuje uživatelům v používání kamery na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat přístup k kameře zařízení.

  Intune spravuje jenom přístup k kameře zařízení. Nemá přístup k obrázkům a videím.

  [CSP pro kameru](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-camera)

- **OneDrive File Sync**: **blok** brání uživatelům v synchronizaci souborů se ze zařízení na OneDrivu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  [CSP pro System/DisableOneDriveFileSync](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-disableonedrivefilesync)

- **Vyměnitelné úložiště**: **blok** zabraňuje uživatelům v používání externích úložných zařízení, jako jsou SD karty se zařízením. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Zeměpisná poloha**: **blok** zabraňuje uživatelům v zapínání služeb zjišťování polohy na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  [CSP pro System/AllowLocation](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowlocation)

- **Sdílení internetu**: **blok** zabraňuje sdílení internetového připojení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Resetování na telefonu**: **blok** brání uživatelům v vymazání nebo obnovení továrního nastavení v zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Připojení USB**: **blok** zabraňuje přístupu k externímu úložnému zařízení přes připojení USB na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Toto nastavení neovlivňuje zpoplatnění přes USB.

  [Připojení/AllowUSBConnection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowusbconnection)

- **Režim AntiTheft** (jenom mobilní): **blok** zabraňuje uživatelům v výběru předvolby režimu AntiTheft na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Cortana**: **Block** zakáže hlasového asistenta Cortany na zařízení. Když je Cortana vypnutá, uživatelé můžou pořád vyhledávat položky v zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat Cortanu.

  [Experience/AllowCortana CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

- **Záznam hlasu** (jenom mobilní): **blok** znemožní uživatelům používat na zařízení záznam hlasu zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat záznam hlasu pro aplikace.
- **Úprava názvu zařízení** (jenom mobilní): **blok** znemožní uživatelům měnit název zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Přidat zřizovací balíčky**: **blok** zabraňuje agentovi konfigurace běhu, který instaluje zřizovací balíčky na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Odebrat zřizovací balíčky**: **blok** zabraňuje agentům konfigurace běhu, který ze zařízení odebírá zřizovací balíčky. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Zjišťování zařízení**: **blok** zabraňuje tomu, aby se zařízení zjistilo jinými zařízeními. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  [Experience/AllowDeviceDiscovery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowdevicediscovery)

- **Přepínání úloh** (jenom mobilní): **blok** zabraňuje přepínání úloh na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Chybový dialog SIM karty** (jenom mobilní): **blokovat** zobrazování chybových zpráv na zařízení, pokud se nezjistí žádná SIM karta. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazit chybové zprávy.
- **Pracovní prostor Ink**: vyberte, jestli a jak má uživatel přístup k pracovnímu prostoru rukopisu. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení může operační systém zapnout pracovní prostor rukopisu a uživatelé ho můžou používat nad zamykací obrazovkou.
  - **Zakázáno na zamykací obrazovce**: pracovní prostor Ink je povolen a funkce je zapnutá. Uživatelé k nim ale nemají přístup nad zamykací obrazovkou.
  - **Zakázáno**: přístup k pracovnímu prostoru Ink je zakázán. Tato funkce je vypnutá.

  [CSP zásad WindowsInkWorkspace](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsinkworkspace)

- **Resetování autopilotu**: vyberte **Povolit** , aby uživatelé s právy správce mohli odstranit všechna uživatelská data a nastavení pomocí **kombinace kláves Ctrl + Win + R** na zamykací obrazovce zařízení. Zařízení se automaticky překonfiguruje a znovu zaregistruje do správy. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit této funkci.
- Vyžadovat, aby se **Uživatelé během instalace zařízení připojili k síti**: vyberte **vyžadovat** , aby se zařízení připojovalo k síti před tím, než bude instalace systému Windows po síti. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit přejít přes stránku síť, a to i v případě, že není připojen k síti.

  Nastavení se projeví při příštím vymazání nebo resetování zařízení. Stejně jako u jakékoli jiné konfigurace Intune musí být zařízení zaregistrované a spravované přes Intune, aby přijímalo nastavení konfigurace. Ale jakmile je zaregistrované, a když se dostávají zásady, zařízení resetuje nastavení v průběhu příští instalace Windows.

  [TenantLockdown CSP](https://docs.microsoft.com/windows/client-management/mdm/tenantlockdown-csp)

- **Přímý přístup do paměti**: **blok** zabraňuje přímému přístupu do paměti (DMA) pro všechny bezplatných portů PCI pro příjem dat, dokud se uživatel přihlásí do systému Windows. **Povoleno** (výchozí) umožňuje přístup k DMA i v případě, že uživatel není přihlášený.

  [Poskytovatel CSP pro DataProtection/AllowDirectMemoryAccess](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess)

- **Ukončit procesy ze Správce úloh**: Toto nastavení určuje, jestli uživatelé bez oprávnění správce můžou k ukončení úloh používat Správce úloh. **Blok** zabraňuje standardním uživatelům (bez správců) v používání Správce úloh k ukončení procesu nebo úlohy v zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém standardně použít k ukončení procesu nebo úlohy pomocí Správce úloh.

  [CSP TaskManager/AllowEndTask](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-taskmanager#taskmanager-allowendtask)

## <a name="locked-screen-experience"></a>Prostředí zamknuté obrazovky

- **Oznámení centra akcí (jenom mobilní)**: **blok** zabraňuje zobrazování oznámení centra akcí na zamykací obrazovce zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit vybrat, které aplikace budou zobrazovat oznámení na zamykací obrazovce.

  [CSP AboveLock/AllowActionCenterNotifications](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#AboveLock_AllowActionCenterNotifications)

- **Adresa URL obrázku pro zamknutou obrazovku (jenom desktopové aplikace)**: zadejte adresu URL obrázku ve formátu jpg, JPEG nebo PNG, který se používá jako tapeta zamykací obrazovky Windows. Zadejte například `https://contoso.com/image.png`. Toto nastavení zamkne obrázek a nedá se změnit.

  [Přizpůsobení/LockScreenImageUrl CSP](https://docs.microsoft.com/windows/client-management/mdm/personalization-csp)

- **Uživatelem konfigurovatelný časový limit obrazovky (jenom mobilní)**: **Povolení** umožňuje uživatelům nakonfigurovat časový limit obrazovky. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí uživatelům dát tuto možnost.

  [CSP DeviceLock/AllowScreenTimeoutWhileLockedUserConfig](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#DeviceLock_AllowScreenTimeoutWhileLockedUserConfig)

- **Cortana na uzamčené obrazovce** (jenom stolní počítače): **blok** zabraňuje uživatelům v interakci s Cortana, když je zařízení na zamykací obrazovce. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat interakci s Cortana.

  [CSP AboveLock/AllowCortanaAboveLock](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowcortanaabovelock)

- **Informační zprávy na uzamčené obrazovce**: **blok** znemožní zobrazování oznámení na zamykací obrazovce zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tato oznámení umožňovat.

  [CSP AboveLock/AllowToasts](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowtoasts)

- **Časový limit obrazovky (jenom mobilní zařízení)**: Nastavte dobu trvání (v sekundách) na zamykací obrazovce na obrazovku vypnutí. Podporované hodnoty jsou 11-1800. Zadejte například, pokud `300` chcete nastavit tento časový limit na 5 minut.

  [CSP DeviceLock/ScreenTimeoutWhileLocked](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#DeviceLock_ScreenTimeoutWhileLocked)

## <a name="messaging"></a>Zasílání zpráv

Tato nastavení používají [CSP zásady zasílání zpráv](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-messaging), ve kterém jsou uvedeny také podporované edice Windows.

- **Synchronizace zpráv (jenom mobilní zařízení)**: **blok** zakáže zálohování a obnovování textových zpráv a synchronizaci zpráv mezi zařízeními s Windows. Vypnutí pomáhá zabránit ukládání informací na serverech mimo řízení organizace. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit tato nastavení měnit a synchronizovat jejich zprávy.
- **MMS (jenom mobilní)**: **blokování** zakáže na zařízení funkci Send a Receive MMS. V případě podniků použijte tuto zásadu k zakázání MMS na zařízeních v rámci požadavku auditování nebo správy. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat odesílání a příjem MMS.
- **RCS (jenom mobilní)**: **blokování** zakáže na zařízení funkci posílání a přijímání RCS (Rich Communication Services). V případě podniků použijte tuto zásadu k zakázání RCS na zařízeních v rámci požadavku auditování nebo správy. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat RCS odesílání a přijímání.

## <a name="microsoft-edge-browser"></a>Prohlížeč Microsoft Edge

Tato nastavení používají [zprostředkovatele CSP zásad prohlížeče](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser), který také uvádí podporované edice systému Windows.

> [!NOTE]
> Použití zprostředkovatele kryptografických služeb zásad prohlížeče se vztahuje na Microsoft Edge verze 45 a starší. Informace o Microsoft Edge Enterprise verze 77 a novějších najdete v tématu [Konfigurace nastavení zásad pro Microsoft Edge pomocí Microsoft Intune](/DeployEdge/configure-edge-with-intune).

### <a name="use-microsoft-edge-kiosk-mode"></a>Použít celoobrazovkový režim Microsoft Edge

Dostupná nastavení se mění v závislosti na tom, co zvolíte. Možnosti:

- **Ne** (výchozí): Microsoft Edge není spuštěný v celoobrazovkovém režimu. Všechna nastavení Microsoft Edge jsou k dispozici pro změnu a konfiguraci.
- **Digitální nebo interaktivní signice (samoobslužný terminál)**: filtruje nastavení Microsoft Edge, která se vztahují k digitálnímu a interaktivnímu registračnímu režimu Microsoft Edge pro použití jenom v terminálech s jednou aplikací ve Windows 10. Toto nastavení vyberte, pokud chcete otevřít adresu URL na celé obrazovce a zobrazit jenom obsah na tomto webu. [Nastavení digitální znaménka](https://docs.microsoft.com/windows/configuration/setup-digital-signage) poskytuje další informace o této funkci.
- **Veřejné procházení InPrivate (samoobslužný terminál)**: filtruje nastavení Microsoft Edge, která se vztahují k veřejnému procházení InPrivate pro použití v terminálech s jednou aplikací ve Windows 10 a v celoobrazovkovém režimu. Spustí více karet verze Microsoft Edge.
- **Normální režim (veřejný terminál s více aplikacemi)**: filtruje nastavení Microsoft Edge, která platí pro normální celoobrazovkový režim Microsoft Edge. Spustí plnou verzi Microsoft Edge se všemi funkcemi pro procházení.
- **Veřejné procházení (veřejný terminál s více aplikacemi)**: filtruje nastavení Microsoft Edge, která se vztahují k veřejnému procházení veřejného terminálu pro více aplikací ve Windows 10.  Spustí na více kartách verzi Microsoft Edge InPrivate.

> [!TIP]
> Další informace o tom, co tyto možnosti dělají, najdete v článku [typy konfigurace celoobrazovkového režimu Microsoft Edge](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

Tento profil omezení zařízení přímo souvisí s profilem veřejného terminálu, který vytvoříte pomocí [Nastavení veřejného terminálu Windows](kiosk-settings-windows.md). Shrnutí:

1. Vytvořte profil [Nastavení veřejného terminálu Windows](kiosk-settings-windows.md) pro spuštění zařízení v celoobrazovkovém režimu. Jako aplikaci vyberte Microsoft Edge a v profilu veřejného terminálu nastavte celoobrazovkový režim Microsoft Edge.
2. Vytvořte profil omezení zařízení, který je popsaný v tomto článku, a nakonfigurujte konkrétní funkce a nastavení povolená v Microsoft Edge. Nezapomeňte zvolit stejný typ celoobrazovkového režimu Microsoft Edge, jak je vybraný v profilu veřejného terminálu ([Nastavení veřejného terminálu pro Windows](kiosk-settings-windows.md)). 

    [Nastavení podporovaného celoobrazovkového režimu](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-policies-for-kiosk-mode) je skvělý prostředek.

> [!IMPORTANT] 
> Ujistěte se, že tento profil Microsoft Edge přiřadíte ke stejným zařízením jako profil veřejného terminálu ([Nastavení veřejného terminálu pro Windows](kiosk-settings-windows.md)).

[ConfigureKioskMode CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-configurekioskmode)

### <a name="start-experience"></a>Úvodní prostředí

- **Spustit Microsoft Edge s**: vyberte, které stránky se otevřou, když se spustí Microsoft Edge. Možnosti:
  - **Vlastní úvodní stránky**: Zadejte úvodní stránky, například `http://www.contoso.com` . Microsoft Edge načte úvodní stránky, které zadáte.
  - **Stránka Nová karta**: zatížení Microsoft Edge se zadává v nastavení **adresy URL nové karty** .
  - **Stránka poslední relace**: Microsoft Edge načte stránku poslední relace.
  - **Úvodní stránky v nastavení místní aplikace**: Microsoft Edge začíná výchozí úvodní stránkou DEFINOVANOU operačním systémem.

- **Umožní uživateli změnit úvodní stránky**: **Ano** (výchozí) umožňuje uživatelům změnit úvodní stránky. Správci můžou použít `EdgeHomepageUrls` k zadání spouštěcích stránek, které se uživatelům zobrazí ve výchozím nastavení při otevření Microsoft Edge. **Žádní** uživatelé neblokují změnu úvodní stránky.
- **Stránka pro povolení webového obsahu na nové kartě**: když je nastavená hodnota **Ano** (výchozí), Microsoft Edge otevře adresu URL zadanou v nastavení **Adresa URL nové karty** . Pokud je **Nová adresa URL karty** prázdná, Microsoft Edge otevře novou stránku karty uvedenou v nastavení Microsoft Edge. Uživatelé je mohou změnit. Pokud je nastavena na **ne**, Microsoft Edge otevře novou kartu s prázdnou stránkou. Uživatelé je nemůžou změnit.
- **Adresa URL nové karty**: zadejte adresu URL, která se má otevřít na stránce Nová karta. Zadejte například `https://www.bing.com` nebo `https://www.contoso.com`.

- **Tlačítko domů**: vyberte, co se stane, když je vybráno tlačítko domů. Možnosti:
  - **Úvodní stránky**: otevře možnost, kterou jste zvolili v části **Spustit Microsoft Edge s** nastavením
  - **Stránka Nová karta**: otevře adresu URL, kterou jste zadali v nastavení **Adresa URL nové karty** .
  - **Adresa URL pro tlačítko domů**: zadejte adresu URL, která se má otevřít. Zadejte například `https://www.bing.com` nebo `https://www.contoso.com`.
  - **Skrýt tlačítko domů**: skryje tlačítko domů.
- **Tlačítko pro povolení uživatelů změnit domů**: **Ano** umožňuje uživatelům změnit tlačítko domů. Změny uživatelů přepíšou všechna nastavení správce na tlačítko domů. **Ne** (výchozí) znemožní uživatelům měnit způsob, jakým Správce nakonfiguroval tlačítko domů.
- **Zobrazit stránku prvního spuštění (jenom mobilní)**: **Ano** (výchozí) zobrazuje úvodní stránku použití v Microsoft Edge. **No** zastaví zobrazování úvodní stránky při prvním spuštění Microsoft Edge. Tato funkce umožňuje podnikům, jako jsou například organizace zaregistrované v konfiguracích s nulovou emisemi, blokovat tuto stránku.
- **Umístění seznamu adres URL prvního spuštění** (jenom Windows 10 Mobile): zadejte adresu URL, která odkazuje na soubor XML, který obsahuje adresy URL prvního spuštění stránky. Zadejte například `https://www.contoso.com/sites.xml`.

- **Aktualizovat prohlížeč po době nečinnosti**: zadejte počet minut nečinnosti, než se prohlížeč aktualizuje, od 0-1440 minut. Výchozí hodnota je `5` minuty. Při nastavení na `0` hodnotu (nula) se prohlížeč po nečinnosti neaktualizuje.

  Toto nastavení je dostupné jenom v případě, že běží ve [veřejném procházení InPrivate (veřejný terminál s jednou aplikací)](#use-microsoft-edge-kiosk-mode).

- **Povolit automaticky otevíraná okna** (jenom desktopové zařízení): **Ano** (výchozí) umožňuje automaticky otevíraná okna ve webovém prohlížeči. V prohlížeči **nebrání automaticky** otevíraná okna.
- **Odesílat intranetový provoz do Internet Exploreru** (jenom desktopové verzi): **Ano** umožňuje uživatelům otevírat intranetové weby v Internet Exploreru místo Microsoft Edge. Toto nastavení je pro zpětnou kompatibilitu. Možnost **ne** (výchozí) umožňuje uživatelům používat Microsoft Edge.
- **Umístění seznamu webů podnikového režimu** (jenom desktopové verze): zadejte adresu URL, která odkazuje na soubor XML obsahující seznam webů, které se otevřou v podnikovém režimu. Uživatelé nemůžou tento seznam měnit. Zadejte například `https://www.contoso.com/sites.xml`.
- **Zpráva při otevírání webů v Internet Exploreru**: pomocí tohoto nastavení můžete nastavit, aby se v Microsoft Edge zobrazovalo oznámení předtím, než se web otevře v Internet Exploreru 11. Možnosti:
  - **Nezobrazovat zprávu**: používá se výchozí chování operačního systému, které nemusí zobrazovat zprávu.
  - **Zobrazit zprávu, že web je otevřen v aplikaci Internet Explorer 11**: Zobrazit zprávu při otevírání webů v aplikaci Internet Explorer. Weby otevřené v aplikaci IE. 
  - **Zobrazit zprávu s možností otevření webů v Microsoft Edge**: Zobrazit zprávu při otevírání webů v Microsoft Edge. Tato zpráva zahrnuje i **nadále odkaz na Microsoft Edge** , takže uživatelé můžou místo IE zvolit Microsoft Edge.

  > [!IMPORTANT]
  > Toto nastavení vyžaduje, abyste používali nastavení **umístění seznamu webů podnikového režimu** , nastavení **odesílat intranetový provoz do aplikace Internet Explorer** nebo obě nastavení.

- **Povolit seznam kompatibility Microsoftu**: **Ano** (výchozí) umožňuje používat seznam kompatibility Microsoftu. **Ne** zabraňuje seznamu kompatibility Microsoftu v Microsoft Edge. Tento seznam od Microsoftu pomáhá společnosti Microsoft Edge správně zobrazit lokality se známými problémy s kompatibilitou.
- **Úvodní stránky a stránka nové karty**: **Ano** (výchozí) použije výchozí chování operačního systému, které může být pro tyto stránky předem načteno. Předběžné načtení minimalizuje čas na spuštění Microsoft Edge a načítá nové karty. **Ne** znemožní Microsoft Edge z přednačtení počátečních stránek a nové stránky karty.
- **Úvodní stránky a stránka nové karty**: **Ano** (výchozí) použije výchozí chování operačního systému, které může být nutné pro tyto stránky spustit znovu. Předběžná spuštění pomáhá s výkonem Microsoft Edge a minimalizuje dobu potřebnou ke spuštění Microsoft Edge. **Žádné** zabraňuje Microsoft Edge v předběžném spuštění stránek Start a nové karty.

### <a name="favorites-and-search"></a>Oblíbené položky a hledání

- **Zobrazit panel Oblíbené**: vyberte, co se stane s panelem oblíbené na libovolné stránce Microsoft Edge. Možnosti:
  - **Na stránkách začátek a nová karta**: zobrazí panel Oblíbené, když se spustí Microsoft Edge a na všech stránkách karty. Uživatelé můžou toto nastavení změnit.
  - **On Pages**: zobrazí panel Oblíbené na všech stránkách. Uživatelé toto nastavení nemůžou změnit.
  - **Skrytý**: skryje panel Oblíbené na všech stránkách. Uživatelé toto nastavení nemůžou změnit.
- **Povolit změny oblíbených položek**: **Ano** (výchozí) použije výchozí nastavení operačního systému, které umožňuje uživatelům změnit seznam. **Žádná** zabraňuje uživatelům v přidávání, importování, řazení a úpravách seznamu oblíbených položek.
  - **Seznam oblíbených položek**: přidejte do souboru oblíbených položek seznam adres URL. Přidejte například `http://contoso.com/favorites.html`.
- **Synchronizovat oblíbené položky mezi prohlížeči Microsoft** (jenom desktopové aplikace): **Ano** vynutí, aby Windows synchronizoval oblíbené položky mezi Internet Explorerem a Microsoft Edgem. Přidání, odstranění, úpravy a změna pořadí oblíbených položek jsou sdíleny mezi prohlížeči.  **Ne** (výchozí) používá výchozí nastavení operačního systému, které může uživatelům umožnit synchronizaci oblíbených položek mezi prohlížeči.
- **Výchozí vyhledávací modul**: Vyberte výchozí vyhledávací web na zařízení. Uživatelé mohou tuto hodnotu kdykoli změnit. Možnosti:
  - Vyhledávací modul v nastavení klienta Microsoft Edge
  - Bing
  - Google
  - Yahoo
  - Vlastní hodnota: v **adrese URL XML OpenSearch**zadejte adresu URL protokolu HTTPS se souborem XML, který obsahuje krátký název a adresu URL vyhledávacího stroje. Zadejte například `https://www.contoso.com/opensearch.xml`.
- **Zobrazit návrhy hledání**: **Ano** (výchozí) umožňuje vyhledávacímu webu navrhovat při psaní frází hledání na adresním řádku. Tato funkce **není** zabráněno.
- **Povolit změny vyhledávacího modulu**: **Ano** (výchozí) umožňuje uživatelům přidávat nové vyhledávací moduly nebo měnit výchozí vyhledávací web na Microsoft Edge. Pokud chcete uživatelům zabránit v přizpůsobení vyhledávacího modulu, klikněte na **ne** .

  Toto nastavení je dostupné, jenom když běží v [normálním režimu (veřejný terminál s více aplikacemi)](#use-microsoft-edge-kiosk-mode).

### <a name="privacy-and-security"></a>Ochrana osobních údajů a zabezpečení

- **Povolit procházení InPrivate**: **Ano** (výchozí) povolí procházení InPrivate v Microsoft Edge. Po zavření všech karet InPrivate odstraní Microsoft Edge data procházení ze zařízení. **Žádná** zabraňuje uživatelům otevírat relace procházení InPrivate.
- **Uložit historii procházení**: **Ano** (výchozí) povolí ukládání historie procházení v Microsoft Edge. **No** nebrání ukládání historie procházení.
- **Vymazat údaje o procházení při ukončení** (jenom desktopové aplikace): **Ano** vymaže historii a data se budou procházet, když uživatelé ukončí Microsoft Edge. **Ne** (výchozí) používá výchozí operační systém, který může ukládat data procházení do mezipaměti.
- **Synchronizovat nastavení prohlížeče mezi zařízeními uživatele**: vyberte, jak chcete synchronizovat nastavení prohlížeče mezi zařízeními. Možnosti:
  - **Povolení**: povoluje synchronizaci nastavení prohlížeče Microsoft Edge mezi zařízeními uživatele.
  - **Zablokovat a povolit přepsání uživatelem**: blokuje synchronizaci nastavení prohlížeče Microsoft Edge mezi zařízeními uživatele. Uživatelé můžou toto nastavení přepsat.
  - **Blokování**: blokování synchronizace nastavení prohlížeče Microsoft Edge mezi zařízeními uživatelů. Uživatelé nemůžou toto nastavení přepsat.

Když je vybraná možnost blokovat a povolit uživatele, může přepsat označení správce.

- **Povolit správce hesel**: **Ano** (výchozí) umožňuje Microsoft Edge automaticky používat Správce hesel, který umožňuje uživatelům ukládat a spravovat hesla v zařízení. **No** zabrání Microsoft Edge v používání Správce hesel.
- **Soubory cookie**: Vyberte způsob zpracování souborů cookie ve webovém prohlížeči. Možnosti:
  - **Povoleno**: soubory cookie jsou uloženy v zařízení.
  - **Blokovat všechny soubory cookie**: soubory cookie nejsou uloženy v zařízení.
  - **Blokovat pouze soubory cookie třetích stran**: soubory cookie třetích stran nebo partnerů nejsou uloženy v zařízení.
- **Povolit automatické vyplňování formulářů**: **Ano** (výchozí) umožňuje uživatelům změnit nastavení automatického dokončování v prohlížeči a automaticky naplnit pole formuláře. Funkce automatického vyplňování **není** na Microsoft Edge zakázaná.
- **Odeslat hlavičky do Not Track**: **Ano** odešle hlavičky do Not Track pro weby požadující informace o sledování (doporučeno). **Ne** (výchozí) neodesílají hlavičky, které umožňují webům sledovat uživatele. Uživatelé můžou toto nastavení nakonfigurovat.
- **Zobrazit IP adresu WebRTC localhost**: **Ano** (výchozí) povolí zobrazení IP adresy místního hostitele pro uživatele při telefonickém volání pomocí tohoto protokolu. Možnost **ne** zabrání zobrazení IP adresy místního hostitele uživatele. 
- **Povolit shromažďování dat živé dlaždice**: **Ano** (výchozí) umožňuje Microsoft Edge shromažďovat informace z živých dlaždic připnuté do nabídky Start. **Žádné** nebrání shromažďování těchto informací, což může uživatelům poskytnout omezené prostředí.
- **Uživatel může přepsat chyby certifikátu**: **Ano** (výchozí) umožňuje uživatelům přístup k webům s chybami protokolu SSL/TLS (SSL (Secure Sockets Layer)/Transport Layer Security). **Ne** (doporučeno pro zvýšené zabezpečení) znemožní uživatelům přístup k webům s chybami SSL nebo TLS.

### <a name="additional"></a>Další

- **Povolit prohlížeč Microsoft Edge** (jenom mobilní zařízení): **Ano** (výchozí) umožňuje používat na mobilním zařízení webový prohlížeč Microsoft Edge. V zařízeních **nebrání použití** Microsoft Edge. Pokud zvolíte **ne**, ostatní individuální nastavení platí pouze pro plochu.
- Možnost **Povolit panel Adresa**: **Ano** (výchozí) umožňuje, aby Microsoft Edge zobrazoval rozevírací seznam s panelem Adresa se seznamem návrhů. V takovém případě se v rozevíracím seznamu při psaní **nezastaví zobrazení** seznamu návrhů v Microsoft Edge. Pokud je nastavena na **ne**, můžete:
  - Můžete minimalizovat šířku pásma sítě mezi Microsoft Edge a službami Microsoftu.
  - Zakažte možnost **Zobrazit hledání a návrhy webu při psaní** v nastavení Microsoft Edge >.
- **Povolit režim zobrazení na celé obrazovce**: **Ano** (výchozí) umožňuje, aby Microsoft Edge používal režim celé obrazovky, který zobrazuje jenom webový obsah a skrývá uživatelské rozhraní Microsoft Edge. V Microsoft **Edge znemožní režim** celoobrazovkového režimu.
- **Stránka povolení o příznacích**: **Ano** (výchozí) použije výchozí nastavení operačního systému, které může umožňovat přístup k této `about:flags` stránce. Tato `about:flags` stránka umožňuje uživatelům změnit nastavení vývojáře a povolit experimentální funkce. **Žádná** zabraňuje uživatelům v přístupu k této `about:flags` stránce v Microsoft Edge.
- **Povolit vývojářské nástroje**: **Ano** (výchozí) umožňuje uživatelům používat nástroje F12 Developer Tools k vytváření a ladění webových stránek ve výchozím nastavení. **Žádné** zabraňuje uživatelům v používání vývojářských nástrojů F12.
- **Povolit jazyk JavaScript**: **Ano** (výchozí) umožňuje spouštění skriptů, jako je například JavaScript, v prohlížeči Microsoft Edge. **Žádné** zabraňuje spuštění skriptů Java v prohlížeči.
- **Uživatel může nainstalovat rozšíření**: **Ano** (výchozí) umožňuje uživatelům instalovat rozšíření Microsoft Edge na zařízení. **Nebrání instalaci** .
- **Povolení zkušebního načtení rozšíření pro vývojáře**: **Ano** (výchozí) používá výchozí operační systém, který může umožňovat zkušební načtení. Zkušební načtení nainstaluje a spustí neověřená rozšíření. Možnost **nijak** nebrání Microsoft Edge ve zkušebním načtení pomocí funkce **rozšíření zatížení** . Nebrání rozšíření zkušebního načtení jiným způsobem, jako je například PowerShell.
- **Požadovaná rozšíření**: vyberte, která rozšíření uživatelé v Microsoft Edge nemůžou vypnout. Zadejte názvy rodin balíčků a vyberte **Přidat**. Pokyny [pro připojení k síti VPN pro jednotlivé aplikace najdete v části název rodiny balíčků (PFN)](https://docs.microsoft.com/configmgr/protect/deploy-use/find-a-pfn-for-per-app-vpn) .

  Můžete také **importovat** soubor CSV, který obsahuje názvy rodin balíčků. Případně **exportujte** názvy rodin balíčků, které zadáte.

## <a name="network-proxy"></a>Síťový proxy server

Tato nastavení používají [zprostředkovatele CSP zásad NetworkProxy](https://docs.microsoft.com/windows/client-management/mdm/networkproxy-csp), který obsahuje také podporované edice Windows.

- **Automaticky zjišťovat nastavení proxy serveru**: **blokování** zakáže zařízením automaticky zjišťovat skript automatické konfigurace proxy serveru (PAC). Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto funkci povolit a zařízení se pokusí najít cestu ke skriptu PAC.
- **Použít skript proxy serveru**: **pokud chcete nakonfigurovat** proxy server, zadejte cestu k vašemu skriptu PAC. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém Neumožnit zadání adresy URL ke skriptu PAC.
  - **Nastavení adresy URL skriptu**: zadejte adresu URL skriptu PAC, který chcete použít ke konfiguraci proxy server.
- **Použít ruční proxy server**: vyberte možnost **povoluje** ruční zadání názvu nebo IP adresy a čísla portu TCP proxy server. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí ručně zadávat podrobnosti o proxy server.
  - **Adresa**: zadejte název nebo IP adresu proxy server.
  - **Číslo portu**: zadejte číslo portu proxy server.
  - **Výjimky proxy serveru**: Zadejte všechny adresy URL, které nesmí používat proxy server. `;`Jednotlivé položky oddělte pomocí středníku ().
  - **Obejít proxy server pro místní adresu**: možnost **zakázat** nepoužívá proxy server pro místní intranetové adresy. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém použít proxy server pro místní adresy na vašem intranetu.

## <a name="password"></a>Heslo

Tato nastavení používají [zprostředkovatele CSP zásad DeviceLock](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock), který obsahuje také podporované edice Windows.

- **Heslo**: **vyžaduje** , aby uživatelé zadali heslo pro přístup k zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat přístup k zařízením bez hesla. Platí jenom pro místní účty. Hesla doménového účtu zůstávají nakonfigurovaná službou Active Directory (AD) a službou Azure AD.

  [CSP DeviceLock/DevicePasswordEnabled](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

  - **Vyžadovaný typ hesla**: Vyberte typ hesla. Možnosti:
    - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení může operační systém heslo obsahovat číslice a písmena.
    - **Alfanumerické**: heslo musí být kombinací číslic a písmen.
    - **Číselná**: heslo musí obsahovat pouze čísla.

    [CSP DeviceLock/AlphanumericDevicePasswordRequired](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-alphanumericdevicepasswordrequired)

  - **Minimální délka hesla**: zadejte minimální počet požadovaných znaků od 4-16. Zadejte například, pokud `6` chcete, aby délka hesla vyžadovala alespoň šest znaků. Ve výchozím nastavení může operační systém nastavit na `4` .
  
    [CSP DeviceLock/MinDevicePasswordLength](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-mindevicepasswordlength)
  
    > [!IMPORTANT]
    > Když se požadavek na heslo změní na plochu Windows, uživatelé budou mít vliv na jeho další přihlášení, protože zařízení přecházejí z nečinnosti na aktivní. Uživatelům s hesly, kteří splňují požadavky, se stále zobrazí výzva ke změně hesla.

  - **Počet neúspěšných přihlášení před vymazáním zařízení**: zadejte počet nesprávných hesel, která se mají povolit, než se zařízení vymaže, až do 11. Platné číslo, které zadáte, závisí na edici. [DeviceLock/MAXDEVICEPASSWORDFAILEDATTEMPTS CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts) obsahuje seznam podporovaných hodnot. `0`(nula) může zakázat funkci vymazání zařízení.

    Toto nastavení má také jiný dopad v závislosti na edici. Konkrétní podrobnosti o tomto nastavení najdete v tématu [CSP pro DeviceLock/MaxDevicePasswordFailedAttempts](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts).

  - **Maximální počet minut nečinnosti, po kterém se uzamkne obrazovka**: zadejte dobu, po kterou musí být zařízení v nečinnosti, než se zamkne obrazovka. Zadejte například, `5` Pokud chcete zařízení zamknout po 5 minutách nečinnosti. Pokud je nastavené na **Nenakonfigurováno**, Intune toto nastavení nezmění ani neaktualizuje. Ve výchozím nastavení se operační systém může nastavit na `0` (nula), což není časový limit.

    [CSP DeviceLock/MaxInactivityTimeDeviceLock](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxinactivitytimedevicelock)

  - **Vypršení platnosti hesla (dny)**: zadejte dobu ve dnech, kdy musí být heslo zařízení změněno, od 1-365. Zadejte například `90` platnost hesla po 90 dnech. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje. Ve výchozím nastavení se operační systém může nastavit na `0` (nula), což není vypršení platnosti.

    [CSP DeviceLock/DevicePasswordExpiration](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordexpiration)

  - **Zakázat opakované použití předchozích hesel**: zadejte počet dříve použitých hesel, která se nedají použít, od 1-24. Například zadejte, `5` že uživatelé nemůžou nastavit nové heslo na aktuální heslo ani na žádná z předchozích čtyř hesel. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje.

    [CSP DeviceLock/DevicePasswordHistory](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordhistory)

  - **Vyžadovat heslo při návratu zařízení ze stavu nečinnosti** (mobilní a holografické): **vyžaduje** , aby uživatelé po nečinnosti odemkli zařízení zadáním hesla. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí po nečinnosti vyžadovat kód PIN nebo heslo.

    [CSP DeviceLock/AllowIdleReturnWithoutPassword](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

  - **Jednoduchá hesla**: **blok** znemožní uživatelům vytvářet jednoduchá hesla, například `1234` nebo `1111` . Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožnit uživatelům vytvářet jednoduchá hesla. Toto nastavení také blokuje použití obrázkových hesel.

    [CSP DeviceLock/AllowSimpleDevicePassword](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowsimpledevicepassword)

- **Automatické šifrování během AADJ**: **blok** zabraňuje automatickému šifrování zařízení bitlockerem, když se zařízení připravují k prvnímu použití, a když jsou zařízení připojená k Azure AD. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém povolit šifrování.

  Další informace o [šifrování zařízení nástrojem BitLocker](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-device-encryption-overview-windows-10#bitlocker-device-encryption).

  [CSP pro zabezpečení/PreventAutomaticDeviceEncryptionForAzureADJoinedDevices](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-security#security-preventautomaticdeviceencryptionforazureadjoineddevices)

- **Zásada FIPS (Federal Information Processing Standard)**: **povoluje** použití zásad FIPS (Federal Information Processing Standard), což je standard státní správy USA pro šifrování, algoritmus hash a podepisování. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí Standard FIPS umožňovat.

  [Kryptografie/AllowFipsAlgorithmPolicy CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-cryptography#cryptography-allowfipsalgorithmpolicy)

- **Ověřování zařízení ve Windows Hello**: **umožňuje** uživatelům používat doprovodné zařízení Windows Hello, jako je telefon, síť vhodnosti nebo zařízení IoT, pro přihlášení k počítači s Windows 10. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit ověřování doprovodných zařízení Windows Hell.

  [Ověřování/AllowSecondaryAuthenticationDevice CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-allowsecondaryauthenticationdevice)

- **Upřednostňovaná doména tenanta Azure AD**: zadejte název existující domény v organizaci Azure AD. Když se uživatelé v této doméně přihlásí, nemusí zadávat název domény. Zadejte například `contoso.com`. Uživatelé v `contoso.com` doméně se můžou přihlásit pomocí svého uživatelského jména, jako `abby` je místo `abby@contoso.com` .

  [Ověřování/PreferredAadTenantDomainName CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-preferredaadtenantdomainname)

## <a name="per-app-privacy-exceptions"></a>Výjimky ze zásad ochrany osobních údajů pro jednotlivé aplikace

**Přidejte** aplikace, které by měly mít jiné chování ochrany osobních údajů než z toho, co definujete v části "výchozí ochrana osobních údajů".

- **Název balíčku**: název řady balíčku aplikace.
- **Název aplikace**: název aplikace.

### <a name="exceptions"></a>Výjimky

- **Informace o účtu**: Definujte, jestli tato aplikace bude mít přístup k uživatelskému jménu, obrázku a dalším kontaktním informacím.
- **Aplikace na pozadí**: Definujte, jestli tato aplikace může běžet na pozadí.
- **Kalendář**: Definujte, jestli tato aplikace bude mít přístup ke kalendáři.
- **Historie volání**: Definujte, jestli tato aplikace bude mít přístup k historii volání.
- **Kamera**: Definujte, jestli tato aplikace bude mít přístup ke kameře.
- **Kontakty**: Definujte, jestli tato aplikace bude mít přístup ke kontaktům.
- **E-mail**: Definujte, jestli tato aplikace bude mít přístup k e-mailu a poslat e-mail.
- **Umístění**: Definujte, jestli tato aplikace bude mít přístup k informacím o poloze.
- **Zasílání zpráv**: Definujte, jestli tato aplikace může číst nebo posílat textové zprávy nebo zprávy MMS.
- **Mikrofon**: Definujte, jestli tato aplikace může používat mikrofon.
- **Pohyb**: Definujte, jestli tato aplikace bude mít přístup k informacím o pohybu zařízení.
- **Oznámení**: Definujte, jestli tato aplikace bude mít přístup k oznámením.
- **Telefon**: Definujte, jestli tato aplikace bude mít přístup k telefonu.
- **Radiostanice**: některé aplikace ve vašem zařízení používají rádiová zařízení k posílání a přijímání dat a potřebují je zapnout nebo vypnout. Definujte, jestli tato aplikace může tyto moduly používat.
- **Úlohy**: Definujte, jestli tato aplikace bude mít přístup k vašim úkolům.
- **Důvěryhodná zařízení**: vyberte, jestli tato aplikace může používat důvěryhodná zařízení. Důvěryhodná zařízení jsou hardware, který jste už připojili, nebo hardware, který se dodává se zařízením. Například používejte televizory, projektory a tak dále jako důvěryhodná zařízení.
- **Zpětná vazba a diagnostika**: Definujte, jestli tato aplikace bude mít přístup k diagnostickým informacím.
- **Synchronizovat se zařízeními**: Určete, jestli tato aplikace může automaticky sdílet a synchronizovat informace s bezdrátovými zařízeními, která se neexplicitně spárují se zařízením.

## <a name="personalization"></a>Personalizace

Tato nastavení používají [zprostředkovatele kryptografických služeb v zásadách přizpůsobení](https://docs.microsoft.com/windows/client-management/mdm/personalization-csp), který obsahuje taky podporované edice Windows.

- **Adresa URL obrázku na pozadí plochy (jenom desktopové aplikace)**: zadejte adresu URL obrázku ve formátu. jpg,. jpeg nebo. png, který chcete použít jako tapetu plochy Windows. Uživatelé nemohou tento obrázek změnit. Zadejte například `https://contoso.com/logo.png`.

  Pokud je ponecháno prázdné, Intune toto nastavení nezmění ani neaktualizuje.

## <a name="printer"></a>Tiskárna

- **Tiskárny**: přidejte tiskárny pomocí názvů síťových hostitelů (název DNS). Operační systém vyhledá a nainstaluje pro každou tiskárnu v zařízení vyhovující ovladače tiskáren. Pokud nezadáte žádnou hodnotu, Intune toto nastavení nezmění ani neaktualizuje.

  [CSP pro vzdělávání/Název_tiskárny](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-education#education-printernames)

- **Výchozí tiskárna**: zadejte název síťového hostitele (název DNS) nainstalované tiskárny, který se použije jako výchozí tiskárna. Pokud nezadáte žádnou hodnotu, Intune toto nastavení nezmění ani neaktualizuje.

  [Poskytovatel CSP pro vzdělávání/DefaultPrinterName](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-education#education-defaultprintername)

- **Přidat nové tiskárny**: **blok** zabraňuje uživatelům v přidávání nových tiskáren. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém přizpůsobit přidávání nových tiskáren.

  [Poskytovatel CSP pro vzdělávání/PreventAddingNewPrinters](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-education#education-preventaddingnewprinters)

## <a name="privacy"></a>Ochrana osobních údajů

Tato nastavení používají [CSP zásady ochrany osobních údajů](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy), který také uvádí podporované edice Windows.

- **Prostředí ochrany osobních údajů**: **blok** zabraňuje otevření ochrany osobních údajů při přihlášení uživatelů a otevření pro nové a aktualizované uživatele. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  [Soukromí/DisablePrivacyExperience](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy#privacy-disableprivacyexperience)

- **Přizpůsobení vstupu**: **blok** zabraňuje použití hlasu pro diktování a komunikaci s Cortana a dalšími aplikacemi, které využívají rozpoznávání řeči od Microsoftu. Je zakázaná a uživatelé nemůžou povolit online rozpoznávání řeči pomocí nastavení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém vybrat možnost Uživatelé. Pokud tyto služby povolíte, může Microsoft kvůli vylepšení služby shromažďovat hlasová data.

  [Soukromí/AllowInputPersonalization CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy#privacy-allowinputpersonalization)

- **Automatické přijetí párování a výzev k souhlasu uživatele s ochranou osobních údajů**: vyberte možnost **umožnit** , aby systém Windows mohl automaticky přijímat párování a zprávy o souhlasu s ochranou osobních údajů při spouštění aplikací. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit automatickému přijetí.

  [Soukromí/AllowAutoAcceptPairingAndPrivacyConsentPrompts CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy#privacy-allowautoacceptpairingandprivacyconsentprompts)

- **Publikování aktivit uživatelů**: **blokování** brání aplikacím a operačnímu systému v publikování aktivit uživatelů. Zabrání taky sdílení a zjišťování naposledy použitých prostředků v informačním kanálu o aktivitách. Aktivity uživatelů sledují stav uživatelských úloh v aplikaci nebo operačním systému. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto funkci povolit, takže aplikace můžou publikovat aktivity uživatelů.

  [Soukromí/PublishUserActivities CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy#privacy-publishuseractivities)

- **Pouze místní aktivity**: **blok** zabraňuje sdíleným prostředím a zjišťování naposledy použitých prostředků v přepínání úloh na základě pouze místních aktivit. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

Můžete nakonfigurovat informace, ke kterým mají přístup všechny aplikace na zařízení. Také definujte výjimky pro jednotlivé aplikace pomocí **výjimek ochrany osobních údajů pro jednotlivé aplikace**.

### <a name="exceptions"></a>Výjimky

- **Informace o účtu**: Definujte, jestli tato aplikace bude mít přístup k uživatelskému jménu, obrázku a dalším kontaktním informacím.
- **Aplikace na pozadí**: Definujte, jestli tato aplikace může běžet na pozadí.
- **Kalendář**: Definujte, jestli tato aplikace bude mít přístup ke kalendáři.
- **Historie volání**: Definujte, jestli tato aplikace bude mít přístup k historii volání.
- **Kamera**: Definujte, jestli tato aplikace bude mít přístup ke kameře.
- **Kontakty**: Definujte, jestli tato aplikace bude mít přístup ke kontaktům.
- **E-mail**: Definujte, jestli tato aplikace bude mít přístup k e-mailu a poslat e-mail.
- **Umístění**: Definujte, jestli tato aplikace bude mít přístup k informacím o poloze.
- **Zasílání zpráv**: Definujte, jestli tato aplikace může číst nebo posílat textové zprávy nebo zprávy MMS.
- **Mikrofon**: Definujte, jestli tato aplikace může používat mikrofon.
- **Pohyb**: Definujte, jestli tato aplikace bude mít přístup k informacím o pohybu zařízení.
- **Oznámení**: Definujte, jestli tato aplikace bude mít přístup k oznámením.
- **Telefon**: Definujte, jestli tato aplikace bude mít přístup k telefonu.
- **Radiostanice**: některé aplikace ve vašem zařízení používají rádiová zařízení k posílání a přijímání dat a potřebují je zapnout nebo vypnout. Definujte, jestli tato aplikace může tyto moduly používat.
- **Úlohy**: Definujte, jestli tato aplikace bude mít přístup k vašim úkolům.
- **Důvěryhodná zařízení**: vyberte, jestli tato aplikace může používat důvěryhodná zařízení. Důvěryhodná zařízení jsou hardware, který jste už připojili, nebo hardware, který je součástí zařízení. Například používejte televizory, projektory a tak dále jako důvěryhodná zařízení.
- **Zpětná vazba a diagnostika**: vyberte, jestli tato aplikace bude mít přístup k diagnostickým informacím.
- **Synchronizovat se zařízeními** – Definujte, jestli tato aplikace může automaticky sdílet a synchronizovat informace s bezdrátovými zařízeními, která se explicitně nepárují s tímto počítačem, tabletem nebo telefonem.

## <a name="projection"></a>Projekce

Tato nastavení používají [zprostředkovatele CSP zásad WirelessDisplay](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay), který obsahuje také podporované edice Windows.

- **Vstup uživatele z přijímačů bezdrátového zobrazení**: **blok** brání vstupu uživatele z přijímačů bezdrátového zobrazení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat bezdrátové zobrazení odesílání klávesnice, myši, pera a dotykového vstupu zpátky na zdrojové zařízení.

  [CSP WirelessDisplay/AllowUserInputFromWirelessDisplayReceiver](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-allowuserinputfromwirelessdisplayreceiver)

- **Projekce na tento počítač**: **blokování** zabrání ostatním zařízením najít zařízení pro projekci a zabrání v projekci do jiných zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém povolit, aby byla zařízení zjistitelná a aby mohla promítnout zařízení nad zamykací obrazovkou.

  [CSP WirelessDisplay/AllowProjectionFromPC](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-allowprojectionfrompc)

- **Vyžadovat pro párování PIN**: při připojování k zařízení projekce **vyžadovat** vždycky výzvy k zadání kódu PIN. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí pro spárování zařízení vyžadovat kód PIN.

  [CSP WirelessDisplay/RequirePinForPairing](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-requirepinforpairing)

## <a name="reporting-and-telemetry"></a>Generování sestav a telemetrie

- **Sdílet data o využití**: vyberte úroveň diagnostických dat, která se odešlou. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Žádné nastavení není vynuceno. Uživatelé zvolí úroveň, která je odeslána. Ve výchozím nastavení operační systém nemusí sdílet žádná data.
  - **Zabezpečení**: informace, které jsou nutné k zajištění vyššího zabezpečení systému Windows, včetně údajů o nastavení komponenty prostředí s připojeným uživatelem a telemetriem, nástroji pro odebrání škodlivého softwaru a programu Microsoft Defender
  - **Základní**: základní informace o zařízení, včetně dat týkajících se kvality, kompatibility aplikací, dat o využití aplikací a dat z úrovně zabezpečení
  - **Rozšířené**: Další přehledy, včetně toho, jak se používají Windows, Windows Server, System Center a aplikace, jak provádějí, pokročilá data o spolehlivosti a data ze základních i úrovní zabezpečení
  - **Úplné**: všechna data potřebná pro identifikaci a pomoc při řešení problémů a data ze zabezpečení, úrovně Basic a rozšířené úrovně.

  [CSP pro System/AllowTelemetry](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

- **Odeslat data o procházení Microsoft Edge do Microsoft 365 Analytics**: Pokud chcete tuto funkci používat, nastavte nastavení **sdílet data o využití** na **Rozšířené** nebo **úplné**. Tato funkce řídí, jaká data Microsoft Edge odesílá Microsoft 365 analýze pro podniková zařízení s nakonfigurovaným komerčním ID. Možnosti:
  - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení operační systém nemusí shromažďovat ani odesílat žádná data historie procházení.
  - **Odesílat jenom intranetová data**: umožňuje správcům odesílat historii dat v intranetu.
  - **Odesílat pouze Internetová data**: umožňuje správcům odesílat historii internetových dat.
  - **Odesílat intranetová a Internetová data**: umožňuje správcům odesílat historii intranetových a internetových dat.

  [CSP pro Browser/ConfigureTelemetryForMicrosoft365Analytics](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-configuretelemetryformicrosoft365analytics)

- **Proxy server telemetrie**: zadejte plně kvalifikovaný název domény (FQDN) nebo IP adresu proxy server, aby se předaly požadavky na uživatelské prostředí a telemetrie pomocí připojení SSL (Secure SOCKETS Layer) (SSL). Formát pro toto nastavení je *server*:*port*. Pokud pojmenovaný proxy server selhává nebo pokud proxy server nezadáte, nebudou se posílat data o prostředích a datech telemetrie připojené uživatele. Zůstane na místním zařízení.

  Pokud nezadáte žádnou hodnotu, Intune toto nastavení nezmění ani neaktualizuje. Ve výchozím nastavení může operační systém odesílat data o zkušenostech uživatelů a telemetrie Microsoftu pomocí výchozí konfigurace proxy serveru.

  Příklady formátů:

  ```
  IPv4: 192.246.246.106:100
  IPv6: [2001:4898:4010:4013:95c1:a8b2:953c:c633]:100
  FQDN: www.contoso.com:345
  ```

  [CSP pro System/TelemetryProxy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-telemetryproxy)

## <a name="search"></a>Hledat

Tato nastavení používají [CSP v zásadách hledání](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search), ve kterém jsou uvedeny také podporované edice systému Windows.

- **Bezpečné vyhledávání (jenom mobilní)**: Určuje, jak Cortana filtruje obsah pro dospělé ve výsledcích hledání. Možnosti:
  - **Definováno uživatelem**: Intune toto nastavení nemění ani neaktualizuje. Žádné nastavení není vynuceno. Uživatelé si zvolí vlastní nastavení.
  - **Strict**: nejvyšší filtrování obsahu pro dospělé
  - **Střední**: mírné filtrování obsahu pro dospělé. Platné výsledky hledání nejsou filtrovány.
- **Zobrazit výsledky webu v hledání**: **blok** zabraňuje uživatelům ve vyhledávání na internetu pomocí služby Windows Search a výsledky webu nejsou zobrazeny ve vyhledávání. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit vyhledat web a výsledky se zobrazí na zařízení.
- **Diakritická znaménka**: **blok** znemožňuje zobrazování diakritických znamének ve Windows Search. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazovat diakritická znaménka.

  [Hledání/AllowUsingDiacritics CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-allowusingdiacritics)

- **Automatické zjišťování jazyka**: **zablokování** zabrání službě Windows Search v automatickém zjišťování jazyka při indexování obsahu nebo vlastností. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto funkci dovolit.

  [Hledání/AlwaysUseAutoLangDetection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-alwaysuseautolangdetection)

- **Umístění pro hledání**: **blok** zabrání službě Windows Search v použití umístění. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto funkci dovolit.

  [Hledání/AllowSearchToUseLocation CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

- **Indexer omezení rychlosti**: **Block** zakáže funkci omezení rychlosti indexeru vyhledávání. Indexování pokračuje s plnou rychlostí, a to i v případě, že je aktivita systému vysoká. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém použít logiku omezení rychlosti k omezení zpětné aktivity indexování v případě vysoké aktivity systému.

  [Hledání/DisableBackoff CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-disablebackoff)

- **Indexování vyměnitelných jednotek**: **blok** zabraňuje přidávání umístění na vyměnitelných jednotkách do knihoven a z indexování. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto funkci dovolit.

  [Hledání/DisableRemovableDriveIndexing CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-disableremovabledriveindexing)

- **Nedostatek místa při indexování**: **Povolení** povoluje automatické indexování, i když je nedostatek místa na disku. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém vypnout automatické indexování, je-li místo na pevném disku 600 MB nebo méně. Pokud mají zařízení ve vaší organizaci omezené místo na pevném disku, nastavte ji na **nenakonfigurovanou**.

  [Hledání/PreventIndexingLowDiskSpaceMB CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-preventindexinglowdiskspacemb)

- **Vzdálené dotazy**: **Povolit** povoluje vzdálené dotazy na index zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit uživatelům ve vzdáleném dotazování na index zařízení.

  [Hledání/PreventRemoteQueries CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-preventremotequeries)

## <a name="start"></a>Spustit

Tato nastavení používají [zprostředkovatele CSP zásad spuštění](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start), který také uvádí podporované edice systému Windows.  

- **Rozložení nabídky Start**: Nahrajte soubor XML, který obsahuje vaše vlastní nastavení, včetně pořadí, ve kterém jsou aplikace uvedené, a další. Soubor XML přepisuje výchozí počáteční rozložení. Uživatelé nemůžou měnit rozložení nabídky Start, které zadáte.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  [Spustit/upravily CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-startlayout)

- **Připnout weby na dlaždice v nabídce Start**: importovat obrázky z Microsoft Edge. Tyto image se zobrazují jako odkazy v nabídce Start systému Windows pro stolní zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  [Spustit/ImportEdgeAssets CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-importedgeassets)

- **Odepnout aplikace z panelu úloh**: **blok** znemožní uživatelům odpnutí aplikací z panelu úloh. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit odepnout aplikace na hlavním panelu.

  [Spustit/NoPinningToTaskbar CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-nopinningtotaskbar)

- **Rychlé přepínání uživatelů**: **blok** zabraňuje přepínání mezi uživateli, kteří jsou přihlášeni současně bez odhlášení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém na dlaždici uživatele zobrazit **přepínač uživatel** .

  [Spustit/HideSwitchAccount CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideswitchaccount)

- **Nejčastěji používané aplikace**: **blok** skryje v nabídce Start nejčastěji používané aplikace. Zároveň se zakáže odpovídající přepínač v aplikaci Nastavení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazit nejčastěji používané aplikace.

  [Spustit/HideFrequentlyUsedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hidefrequentlyusedapps)

- **Nedávno přidané aplikace**: **blok** skryje nedávno přidané aplikace v nabídce Start. Zároveň se zakáže odpovídající přepínač v aplikaci Nastavení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazit nedávno přidané aplikace v nabídce Start.

  [Spustit/HideRecentlyAddedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hiderecentlyaddedapps)

- **Režim úvodní obrazovky**: vyberte velikost obrazovky Start. Možnosti:
  - **Definováno uživatelem**: Intune toto nastavení nemění ani neaktualizuje. Žádné nastavení není vynuceno. Uživatelé můžou nastavit velikost.
  - **Celá obrazovka**: vynutí celou velikost spuštění.
  - Neúplná obrazovka: vynutí **nekompletní**velikost spuštění.

  [Spustit/ForceStartSize CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-forcestartsize)

- **Naposledy otevřené položky v seznamech odkazů**: **blokovat** skryje v nabídce Start a na hlavním panelu nedávný seznam odkazů. Zároveň se zakáže odpovídající přepínač v aplikaci Nastavení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazit nedávno otevřené položky v seznamy odkazů.

  [Spustit/HideRecentJumplists CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hiderecentjumplists)

- **Seznam aplikací**: Vyberte způsob zobrazení seznamů všechny aplikace. Možnosti:
  - **Definováno uživatelem**: Intune toto nastavení nemění ani neaktualizuje. Žádné nastavení není vynuceno. Uživatelé zvolí, jak se zobrazuje seznam aplikací.
  - **Sbalit**: skryje seznam všechny aplikace.
  - **Sbalit a zakázat aplikaci nastavení**: skryje seznam všechny aplikace a zakáže možnost **Zobrazit seznam aplikací v nabídce Start** v aplikaci nastavení.
  - **Odebere a zakáže aplikaci nastavení**: skryje seznam všechny aplikace, odebere všechny aplikace a zakáže možnost **Zobrazit seznam aplikací v nabídce Start** v aplikaci nastavení.

  [Spustit/HideAppList CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideapplist)

- **Tlačítko napájení**: **Block** skryje tlačítko napájení v nabídce Start. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může OS zobrazit tlačítko napájení.

  [Spustit/HidePowerButton CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hidepowerbutton)

- **Dlaždice uživatele**: **blok** skryje dlaždici uživatele v nabídce Start. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může OS zobrazit dlaždici uživatele. Nakonfigurujte tahle nastavení:
  - **Lock**: **Block** skryje možnost **Lock** na dlaždici uživatele v nabídce Start.  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazit možnost **zámku** .
  - **Odhlásit**: **blok** skryje možnost **Odhlásit** se na dlaždici uživatele v nabídce Start. **Nenakonfigurováno** (výchozí) zobrazí možnost **Odhlásit** se.

  [Spustit/HideUserTile CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideusertile)

- **Vypnout**: **blok** skryje možnosti **aktualizace a vypnutí** **a vypnutí na** tlačítku napájení v nabídce Start. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  [Spustit/HideShutDown CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideshutdown)

- **Režim spánku**: **blok** skryje možnost **spánku** na tlačítku napájení v nabídce Start. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  [Spustit/HideSleep CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hidesleep)

- **Hibernace**: **blok** skryje možnost **Hibernace** na tlačítku napájení v nabídce Start. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  [Spustit/HideHibernate CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hidehibernate)

- **Switch Account**: **Block** skryje na dlaždici uživatele v nabídce Start **účet Switch** . Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  [Spustit/HideSwitchAccount CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideswitchaccount)

- **Možnosti restartování**: **blokovat** skryje možnosti **aktualizace a restartování** a **restartování** na tlačítku napájení v nabídce Start. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  [Spustit/HideRestart CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hiderestart)

- **Dokumenty na začátku**: skryje nebo zobrazí složku dokumenty v nabídce Start systému Windows. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Žádné nastavení není vynuceno. Uživatelé mají možnost zobrazit nebo skrýt zástupce.
  - **Skrýt**: zástupce je skrytý a nastavení je v aplikaci nastavení zakázané.
  - **Zobrazit**: zástupce se zobrazí a nastavení je v aplikaci nastavení zakázané.

  [Spustit/AllowPinnedFolderDocuments CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderdocuments)

- **Soubory ke stažení na začátku**: skryje nebo zobrazí složku stažené soubory v nabídce Start systému Windows. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Žádné nastavení není vynuceno. Uživatelé mají možnost zobrazit nebo skrýt zástupce.
  - **Skrýt**: zástupce je skrytý a nastavení je v aplikaci nastavení zakázané.
  - **Zobrazit**: zástupce se zobrazí a nastavení je v aplikaci nastavení zakázané.

  [Spustit/AllowPinnedFolderDownloads CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderdownloads)

- **Průzkumník souborů v nabídce Start**: skrýt nebo zobrazit Průzkumníka souborů v nabídce Start systému Windows. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Žádné nastavení není vynuceno. Uživatelé mají možnost zobrazit nebo skrýt zástupce.
  - **Skrýt**: zástupce je skrytý a nastavení je v aplikaci nastavení zakázané.
  - **Zobrazit**: zástupce se zobrazí a nastavení je v aplikaci nastavení zakázané.

  [Spustit/AllowPinnedFolderFileExplorer CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderfileexplorer)

- **Domácí skupina v nabídce Start**: v nabídce Start systému Windows skryjte nebo zobrazte zástupce domácí skupiny. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Žádné nastavení není vynuceno. Uživatelé mají možnost zobrazit nebo skrýt zástupce.
  - **Skrýt**: zástupce je skrytý a nastavení je v aplikaci nastavení zakázané.
  - **Zobrazit**: zástupce se zobrazí a nastavení je v aplikaci nastavení zakázané.

  [Spustit/AllowPinnedFolderHomeGroup CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderhomegroup)

- **Hudba na začátku**: skryje nebo zobrazí složku hudba v nabídce Windows Start. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Žádné nastavení není vynuceno. Uživatelé mají možnost zobrazit nebo skrýt zástupce.
  - **Skrýt**: zástupce je skrytý a nastavení je v aplikaci nastavení zakázané.
  - **Zobrazit**: zástupce se zobrazí a nastavení je v aplikaci nastavení zakázané.

  [Spustit/AllowPinnedFolderMusic CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldermusic)

- **Síť v nabídce Start**: skrýt nebo zobrazit síťové vstupy nabídce Windows Start. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Žádné nastavení není vynuceno. Uživatelé mají možnost zobrazit nebo skrýt zástupce.
  - **Skrýt**: zástupce je skrytý a nastavení je v aplikaci nastavení zakázané.
  - **Zobrazit**: zástupce se zobrazí a nastavení je v aplikaci nastavení zakázané.

  [Spustit/AllowPinnedFolderNetwork CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldernetwork)

- **Osobní složka v nabídce Start**: skrýt nebo zobrazit osobní složku v nabídce Start systému Windows. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Žádné nastavení není vynuceno. Uživatelé mají možnost zobrazit nebo skrýt zástupce.
  - **Skrýt**: zástupce je skrytý a nastavení je v aplikaci nastavení zakázané.
  - **Zobrazit**: zástupce se zobrazí a nastavení je v aplikaci nastavení zakázané.

  [Spustit/AllowPinnedFolderPersonalFolder CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderpersonalfolder)

- **Obrázky v nabídce Start**: umožňuje skrýt nebo zobrazit složku pro obrázky v nabídce Windows Start. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Žádné nastavení není vynuceno. Uživatelé mají možnost zobrazit nebo skrýt zástupce.
  - **Skrýt**: zástupce je skrytý a nastavení je v aplikaci nastavení zakázané.
  - **Zobrazit**: zástupce se zobrazí a nastavení je v aplikaci nastavení zakázané.

  [Spustit/AllowPinnedFolderPictures CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderpictures)

- **Nastavení na začátku**: v nabídce Start systému Windows skryjte nebo zobrazte zástupce nastavení. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Žádné nastavení není vynuceno. Uživatelé mají možnost zobrazit nebo skrýt zástupce.
  - **Skrýt**: zástupce je skrytý a nastavení je v aplikaci nastavení zakázané.
  - **Zobrazit**: zástupce se zobrazí a nastavení je v aplikaci nastavení zakázané.

  [Spustit/AllowPinnedFolderSettings CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldersettings)

- **Videa na začátku**: v nabídce Start systému Windows skryjte nebo zobrazte složku pro videa. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Žádné nastavení není vynuceno. Uživatelé mají možnost zobrazit nebo skrýt zástupce.
  - **Skrýt**: zástupce je skrytý a nastavení je v aplikaci nastavení zakázané.
  - **Zobrazit**: zástupce se zobrazí a nastavení je v aplikaci nastavení zakázané.

  [Spustit/AllowPinnedFolderVideos CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldervideos)

## <a name="microsoft-defender-smartscreen"></a>Filtr SmartScreen v programu Microsoft Defender

- **Filtr SmartScreen pro Microsoft Edge**: **vyžaduje** zapnutí funkce SmartScreen v programu Microsoft Defender a zabránění uživatelům v jejich vypnutí. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zapnout filtr SmartScreen a povolit uživatelům jeho zapnutí a vypnutí.

  Microsoft Edge používá filtr SmartScreen v programu Microsoft Defender (zapnutý) k ochraně uživatelů před potenciálními podvodnými zprávami a škodlivým softwarem.

  [CSP pro Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

- **Přístup ke škodlivému webu**: **blok** zabraňuje uživatelům ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a zablokuje jejich přechodu na web. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit ignorovat upozornění a pokračovat v lokalitě.

  [CSP pro Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

- **Stahování neověřených souborů**: **blok** zabraňuje uživatelům ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a zablokuje stahování neověřených souborů. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit ignorovat upozornění a pokračovat v stahování neověřených souborů.

  [CSP pro Browser/PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)

## <a name="windows-spotlight"></a>Windows Spotlight

Tato nastavení používají [zprostředkovatele kryptografických služeb (CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience)), který obsahuje taky podporované edice Windows.

- **Windows Spotlight**: **blokování** vypne Windows Spotlight na zamykací obrazovce, tipůch pro Windows, funkcích Microsoftu pro uživatele a dalších souvisejících funkcích. Pokud vaším cílem je minimalizovat síťový provoz ze zařízení, vyberte **Ano**. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat funkce Windows Spotlight a můžou je řídit uživatelé.

  [Experience/AllowWindowsSpotlight CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlight)

  Pokud je nastavené na **Nenakonfigurováno**, můžete také povolí nebo zablokovat následující nastavení:

  - **Windows Spotlight na zamykací obrazovce**: **blokovat** zastaví zobrazování informací na zamykací obrazovce zařízení ve Windows Spotlightu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazit informace Windows Spotlight na zamykací obrazovce.

    [Experience/ConfigureWindowsSpotlightOnLockScreen CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-configurewindowsspotlightonlockscreen)

  - **Návrhy třetích stran ve Windows Spotlightu**: **blok** zastaví Windows Spotlight z návrhu obsahu, který nepublikoval Microsoft. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém pro partnery umožňovat návrhy aplikace a obsahu a v nabídce Start zobrazit navrhované aplikace a tipy k Windows.

    [Experience/AllowThirdPartySuggestionsInWindowsSpotlight CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowthirdpartysuggestionsinwindowsspotlight)

  - **Funkce příjemce**: **blokování** vypíná prostředí, která jsou typicky pro uživatele, jako jsou návrhy zahájení, oznámení o členství, instalace aplikací po ukončení a přesměrování dlaždic. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

    [Experience/AllowWindowsConsumerFeatures CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsconsumerfeatures)

  - **Tipy pro Windows**: **blokování** zakáže automaticky otevíraná okna s tipy pro Windows. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazit tipy pro systém Windows.

    [Experience/AllowWindowsTips CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowstips)

  - **Windows Spotlight v centru akcí**: **blok** zabraňuje zobrazování oznámení Windows Spotlightu v centru akcí. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém v centru akcí zobrazovat oznámení, která navrhují aplikace nebo funkce, které uživatelům pomůžou zvýšit produktivitu Windows.

    [Experience/AllowWindowsSpotlightOnActionCenter CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlightonactioncenter)

  - **Přizpůsobení Windows Spotlightu**: **blok** zabraňuje systému Windows používat diagnostická data k poskytování přizpůsobených prostředí uživatelům. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém společnosti Microsoft umožnit použití diagnostických dat k poskytnutí individuálních doporučení, tipů a nabídek, které přizpůsobí Windows potřebám daného uživatele.

    [Experience/AllowTailoredExperiencesWithDiagnosticData CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowtailoredexperienceswithdiagnosticdata)

  - **Prostředí uvítání systémem Windows**: **blok** vypne funkci Windows Spotlight Windows Welcome Experience. Prostředí uvítání systémem Windows se nezobrazí, pokud jsou k dispozici aktualizace a změny ve Windows a jejích aplikacích. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat uvítání systémem Windows, které zobrazuje informace o uživatelích o nových nebo aktualizovaných funkcích.

    [Experience/AllowWindowsSpotlightWindowsWelcomeExperience CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlightwindowswelcomeexperience)

## <a name="microsoft-defender-antivirus"></a>Antivirová ochrana v programu Microsoft Defender

Tato nastavení používají [zprostředkovatele CSP v zásadách Defenderu](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender), který obsahuje také podporované edice Windows.

- **Sledování v reálném čase**: **Povolení** zapne kontrolu v reálném čase pro malware, spyware a další nežádoucí software. Uživatelé ji nemůžou vypnout. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém tuto funkci zapne a umožňuje uživatelům ji změnit.

  Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune nastavení zůstane v dříve nakonfigurovaném stavu.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/AllowRealtimeMonitoring CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

- **Monitorování chování**: **Povolit** zapne monitorování chování a kontroluje určité známé vzorce podezřelé aktivity na zařízeních. Uživatelé nemůžou monitorování chování vypnout. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zapnout monitorování chování a povolit uživatelům jeho změnu.

  Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune nastavení zůstane v dříve nakonfigurovaném stavu.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/AllowBehaviorMonitoring CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

- **Systém kontroly sítě (NIS)**: NIS pomáhá chránit zařízení před zneužitím prostřednictvím sítě. Používá signatury známých slabých míst z Centra Microsoftu pro ochranu koncových bodů ke zjištění a blokování škodlivého síťového provozu.

  - **Povolit**: zapne ochranu sítě a síťové blokování. Uživatelé ji nemůžou vypnout. Pokud je tato možnost povolená, uživatelé se budou moct připojit ke známým chybám zabezpečení.

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení operační systém zapne službu NIS a umožňuje uživatelům ji změnit.

  Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune nastavení zůstane v dříve nakonfigurovaném stavu.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/EnableNetworkProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

- **Prohledat všechny soubory ke stažení**: **Povolit** zapne toto nastavení a Defender zkontroluje všechny soubory stažené z Internetu. Uživatelé nemůžou toto nastavení vypnout. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zapnout toto nastavení a povolit uživatelům jeho změnu.

  Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune nastavení zůstane v dříve nakonfigurovaném stavu.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/AllowIOAVProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowioavprotection)

- **Kontrolovat skripty načtené do webových prohlížečů Microsoftu**: **Povolit** umožňuje programu Defender kontrolovat skripty, které se používají v Internet Exploreru. Uživatelé nemůžou toto nastavení vypnout. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zapnout toto nastavení a povolit uživatelům jeho změnu.

  Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune nastavení zůstane v dříve nakonfigurovaném stavu.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/AllowScriptScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning)

- **Přístup koncového uživatele k programu Defender**: **blok** skryje uživatelské rozhraní programu Microsoft Defender pro uživatele. Potlačí se také všechna oznámení programu Microsoft Defender. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat uživateli přístup k uživatelskému rozhraní programu Microsoft Defender a umožňuje uživatelům ho změnit.

  Pokud nastavení zablokujete a pak ho změníte zpátky na **není nakonfigurované**, Intune nastavení ponechá v dříve nakonfigurovaném stavu.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  Když se toto nastavení změní, projeví se při příštím restartování zařízení.

  [Defender/AllowUserUIAccess CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess)

- **Interval aktualizace Security Intelligence (v hodinách)**: zadejte interval, který Defender kontroluje pro nové Security Intelligence, od 0-24. Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Výchozí operační systém může kontrolovat aktualizace každých 8 hodin.
  - **Nekontrolovat**: Defender nehledá nové aktualizace Security Intelligence.
  - **1-24**: `1` kontroluje každou hodinu, kontroluje každé `2` dvě hodiny, `24` kontroluje každý den atd.
  
  [Defender/SignatureUpdateInterval CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdateinterval)
  
- **Monitorovat aktivitu souborů a programů**: umožňuje programu Defender monitorovat aktivitu souborů a programů na zařízeních. Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Výchozí hodnota operačního systému může monitorovat všechny soubory.
  - **Monitorování zakázáno**
  - **Monitorovat všechny soubory**
  - **Monitorovat pouze příchozí soubory**
  - **Monitorovat jenom odchozí soubory**

  [Defender/RealTimeScanDirection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-realtimescandirection)

- **Dny před odstraněním malwaru v karanténě**: pokračovat v sledování vyřešeného malwaru po dobu, po kterou zadáte, abyste mohli ručně kontrolovat dříve zasažená zařízení. 

  Pokud toto nastavení nenakonfigurujete nebo nastavíte na `0` dny, malware zůstane ve složce karantény a automaticky se neodebere. Pokud je nastaveno na `90` , karanténní položky jsou uloženy po dobu 90 dnů v systému a poté odebrány.

  [Defender/DaysToRetainCleanedMalware CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware)

- **Limit využití procesoru při kontrole**: Omezte počet procesorů, které mohou kontroly použít, od `0` do `100` procent. Ve výchozím nastavení může operační systém nastavit na 50%.
- **Kontrolovat archivní soubory**: **Povolit** zapne Defender, aby kontroloval archivní soubory, jako jsou soubory ZIP nebo CAB. Uživatelé nemůžou toto nastavení vypnout. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zapnout tuto kontrolu a povolit uživatelům jejich změnu.

  Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune nastavení zůstane v dříve nakonfigurovaném stavu.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/AllowArchiveScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)

- **Kontrolovat příchozí e-mailové zprávy**: **Povolit** umožňuje programu Defender kontrolovat e-mailové zprávy při jejich doručování na zařízeních. Pokud je tento modul povolený, analyzuje poštovní schránku a e-mailové soubory a analyzuje body pošty a přílohy. Můžete kontrolovat formáty. PST (Outlook),. dbx,. mbx, MIME (Outlook Express) a BinHex (Mac).

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém vypne tuto kontrolu a umožní uživatelům ji změnit.

  Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune nastavení zůstane v dříve nakonfigurovaném stavu.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/AllowEmailScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

- **Kontrolovat vyměnitelné jednotky během úplného prohledávání**: **Povolit zapne možnost** při úplné kontrole zapnout kontrolu vyměnitelných jednotek v Defenderu. Uživatelé nemůžou toto nastavení vypnout. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém nechat v programu Defender kontrolovat vyměnitelné jednotky, jako jsou USB hole, a umožnit uživatelům změnit toto nastavení.

  Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune nastavení zůstane v dříve nakonfigurovaném stavu.

  Během rychlé kontroly mohou být vyměnitelné jednotky stále prohledávány.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/AllowFullScanRemovableDriveScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)

- **Kontrolovat namapované síťové jednotky během úplného prohledávání**: **Povolit** programu Defender prohledává soubory na namapovaných síťových jednotkách. Pokud jsou soubory na disku jen pro čtení, Defender nemůže odebrat žádný malware, který v nich našel. Uživatelé nemůžou toto nastavení vypnout.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém tuto funkci zapne a umožňuje uživatelům ji změnit.

  Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune nastavení zůstane v dříve nakonfigurovaném stavu. 

  Během rychlé kontroly mohou být namapované síťové jednotky stále prohledávány.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/AllowFullScanOnMappedNetworkDrives CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives)

- **Kontrolovat soubory otevřené ze síťových složek**: **možnost Povolit** v programu Defender prohledává soubory otevřené ze síťových složek nebo sdílených síťových jednotek, jako jsou například soubory dostupné z cesty UNC. Uživatelé nemůžou toto nastavení vypnout. Pokud jsou soubory na disku jen pro čtení, Defender nemůže odebrat žádný malware, který v nich našel.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém kontroluje soubory otevřené ze síťových složek a umožňuje uživatelům jejich změnu.

  Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune nastavení zůstane v dříve nakonfigurovaném stavu.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/AllowScanningNetworkFiles CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

- **Ochrana cloudu**: **Povolit** zapne služba Microsoft Active Protection Service pro příjem informací o činnosti malwaru ze zařízení, která spravujete. Uživatelé toto nastavení nemůžou změnit. 

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém umožňuje služba Microsoft Active Protection Service přijímat informace a umožňuje uživatelům změnit toto nastavení.

  Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune nastavení zůstane v dříve nakonfigurovaném stavu.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/AllowCloudProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

- **Dotázat se uživatele před odesláním vzorku**: Určuje, jestli se mají do Microsoftu automaticky posílat potenciálně škodlivé soubory, které by mohly vyžadovat další analýzu. Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Výchozí nastavení operačního systému může automaticky odesílat bezpečné vzorky.
  - **Vždycky se zeptat**
  - **Dotázat se před odesláním osobních údajů**
  - **Nikdy Neodesílat data**
  - **Odesílat všechna data bez zobrazení výzvy**: data se odesílají automaticky.

  [Defender/SubmitSamplesConsent CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)

- **Čas, kdy se má provést rychlá denní kontrola**: vyberte hodinu spuštění každodenní rychlé kontroly. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém spustit tuto kontrolu ve 2 dop.

  Pokud chcete další možnosti přizpůsobení, nakonfigurujte **typ Systémové kontroly, který se má provést** .

  [Defender/ScheduleQuickScanTime CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime)

- **Typ Systémové kontroly, který se má provést**: naplánovat kontrolu systému, včetně úrovně kontroly a dne a času, kdy se má kontrola spustit. Možnosti:
  - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje. Žádné nastavení není vynuceno. Uživatelé můžou na svých zařízeních ručně spouštět kontroly podle potřeby nebo na jejich zařízení.
  - **Zakázat**: zakáže všechny systémové kontroly na zařízeních. Tuto možnost vyberte, pokud používáte řešení antivirové ochrany, které provádí kontrolu zařízení.
  - **Rychlá kontrola**: vypadá na běžných místech, kde by mohlo být zaregistrované malware, jako jsou klíče registru a známé spouštěcí složky Windows.
    - **Naplánovaný den**: vyberte den, kdy se má kontrola spustit.
    - **Naplánovaný čas**: vyberte hodiny, kdy se má kontrola spustit.
  - **Úplná kontrola**: hledá na běžných místech, kde by mohla být zaregistrovaná malware, a také zkontroluje všechny soubory a složky v zařízení.
    - **Naplánovaný den**: vyberte den, kdy se má kontrola spustit.
    - **Naplánovaný čas**: vyberte hodiny, kdy se má kontrola spustit.

  > [!TIP]
  > Toto nastavení může být v konfliktu s **časem provedení denního nastavení rychlého prohledávání** . Některá doporučení:  
  >
  > - Pokud chcete naplánovat každodenní rychlou kontrolu a týdenní úplnou kontrolu, postupujte takto:
  >   1. Nakonfigurujte **čas, kdy se má provést nastavení denního rychlého prohledávání** .
  >   2. Nakonfigurujte **typ Systémové kontroly, který se má provést** , aby se prováděla úplná kontrola.
  > 
  > - Pokud chcete, aby jedna rychlá kontrola provedla každý den (bez úplného prohledávání), použijte buď nastavení: **čas k provedení každodenní rychlé kontroly** , nebo **typ Systémové kontroly, který se má provést**. Chcete-li například spustit rychlou kontrolu každé úterý v 9:00, nakonfigurujte **typ kontroly systému na hodnotu provést** .
  > 
  > - Nekonfigurujte **dobu, kdy se má provést nastavení denní rychlé kontroly** současně s **typem kontroly systému, který má být proveden** pro **rychlé prohledání**. Tato nastavení mohou být v konfliktu a kontrola nemusí běžet.

  [Defender/ScanParameter CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)  
  [Defender/ScheduleScanDay CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)  
  [Defender/ScheduleScanTime CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescantime)

- **Zjišťovat potenciálně nežádoucí aplikace**: Tato funkce identifikuje a blokuje potenciálně nežádoucí aplikace (PUA) ze stahování a instalace ve vaší síti. Tyto aplikace nejsou považovány za viry, malware nebo jiné typy hrozeb. Ale můžou spouštět akce u koncových bodů, které mohou ovlivnit jejich výkon nebo použití. Vyberte úroveň ochrany, když systém Windows detekuje PUAs. Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení může Microsoft Defender tuto funkci zakázat.
  - **Vypnuto**: ochrana PUA vypnuto.
  - **Povolit**: Microsoft Defender detekuje PUAs a zjištěné položky jsou blokované. Tyto položky se zobrazují v historii spolu s dalšími hrozbami.
  - **Audit**: Microsoft Defender detekuje PUAs, ale neprovede žádnou akci. Můžete zkontrolovat informace o aplikacích, které Microsoft Defender provede, na základě těchto akcí. Vyhledejte například události vytvořené v programu Microsoft Defender v Prohlížeč událostí.

  Další informace o potenciálně nežádoucích aplikacích najdete v tématu [zjištění a blokování potenciálně nežádoucích aplikací](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-antivirus/detect-block-potentially-unwanted-apps-microsoft-defender-antivirus).

  [Defender/PUAProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

- **Vyjádření souhlasu s ukázkami**: v současné době toto nastavení nemá žádný vliv. Toto nastavení nepoužívejte. Může být odebráno v budoucí verzi.

- **Při přístupu k ochraně**: **blok** zabraňuje kontrole souborů, ke kterým byl přístup nebo stažen. Uživatelé ji nemůžou zapnout. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tuto funkci povolit a umožňuje uživatelům ji změnit.

  Pokud nastavení zablokujete a pak ho změníte zpátky na **není nakonfigurované**, Intune nastavení ponechá v předchozím stavu konfigurovaném pro operační systém.

  Intune tuto funkci nezapíná. Pokud ho chcete povolit, použijte vlastní identifikátor URI.

  [Defender/AllowOnAccessProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

- **Akce u zjištěných malwarových hrozeb**: výběrem možnosti **Povolit** můžete zvolit akce, které má Defender provést pro každou úroveň hrozby, kterou zjistí: nízká, střední, vysoká a závažná. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém aplikace Microsoft Defender zvolit nejlepší možnost.

  Pokud je nastavena možnost **Povolit**, vyberte akci:
  
  - **Odstranit**
  - **Karanténa**
  - **Odebrat**
  - **Povolit**
  - **Definováno uživatelem**
  - **Blokované**

  Pokud vaše akce není možná, pak Microsoft Defender vybere nejlepší možnost, abyste zajistili, že dojde k nápravě hrozby.

  [Defender/ThreatSeverityDefaultAction CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-threatseveritydefaultaction)

### <a name="microsoft-defender-antivirus-exclusions"></a>Vyloučení antivirové ochrany v programu Microsoft Defender

Můžete vyloučit určité soubory z kontroly antivirové ochrany v programu Microsoft Defender úpravou seznamů vyloučení. **Obecně platí, že nebudete muset použít vyloučení**. Antivirová ochrana v programu Microsoft Defender zahrnuje řadu automatických vyloučení na základě známých chování operačního systému a typických souborů pro správu, jako jsou například ty, které se používají v podnikovém řízení, správě databází a dalších podnikových scénářích a situacích.

> [!WARNING]
> **Definování vyloučení snižuje ochranu, kterou nabízí antivirová ochrana v programu Microsoft Defender**. Vždy vyhodnotit rizika spojená s implementací vyloučení. Vylučte jenom soubory, které víte, že nejsou škodlivé.

- **Soubory a složky, které se mají vyloučit z kontrol a ochrany v reálném**čase: přidá do seznamu vyloučení jeden nebo víc souborů a složek, jako je **C:\Cesta** nebo **% ProgramFiles% \Path\filename.exe** . Tyto soubory a složky nejsou zahrnuté do kontrol probíhajících v reálném čase ani do plánovaných kontrol.
- **Přípony souborů, které se mají vyloučit z kontrol a ochrany v reálném čase**: do seznamu vyloučení přidejte jednu nebo víc přípon souborů, jako je **jpg** nebo **txt** . Všechny soubory s těmito příponami nejsou zahrnuté do kontrol probíhajících v reálném čase ani do plánovaných kontrol.
- **Procesy, které se mají vyloučit z kontrol a ochrany v reálném**čase: přidejte jeden nebo více procesů typu **. exe**, **. com**nebo **. scr** do seznamu vyloučení. Tyto procesy nejsou zahrnuté do kontrol prováděných v reálném čase ani do plánovaných kontrol.

## <a name="power-settings"></a>Nastavení napájení

Tato nastavení používají [zprostředkovatele kryptografických služeb pro zásady napájení](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power), který obsahuje taky podporované edice Windows.

### <a name="battery"></a>Baterie

- **Úroveň baterie**: Pokud zařízení používá napájení z baterie, zadejte úroveň nabití baterie, abyste zapnuli úsporu energie, od 0-100. Zadejte procentuální hodnotu, která označuje úroveň nabití baterie. Například když se nastaví na `80` , zapíná úspora energie, když má baterie 80%, nebo méně dostupné.

  Pokud nezadáte žádnou hodnotu, Intune toto nastavení nezmění ani neaktualizuje. Ve výchozím nastavení může operační systém nastavit na 70%.

  [CSP pro Power/EnergySaverBatteryThresholdOnBattery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdonbattery)

- **Zavření víka (jenom mobilní)**: Pokud zařízení používá napájení z baterie, vyberte, co se stane po zavření víka. Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení může operační systém uživatelům dovolit řídit toto nastavení.
  - **Žádná akce**: zařízení zůstává zapnuté a nadále používá napájení z baterie.
  - **Režim spánku**: zařízení přejde do režimu spánku a použije malé množství energie z baterie. Počítač je stále zapnutý a otevřené aplikace a soubory jsou uložené v paměti RAM (Random Access Memory).
  - **Hibernace**: zařízení přejde do režimu hibernace. Otevřené aplikace a soubory se ukládají na pevný disk a zařízení se vypne.
  - **Vypnutí**: zařízení se vypíná. Otevřené aplikace a soubory se zavřou bez uložení.

  [CSP pro Power/SelectLidCloseActionOnBattery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactiononbattery)

- **Tlačítko napájení**: Pokud zařízení používá napájení z baterie, vyberte, co se stane po výběru tlačítka napájení. Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení může operační systém uživatelům dovolit řídit toto nastavení.
  - **Žádná akce**: zařízení zůstává zapnuté a nadále používá napájení z baterie.
  - **Režim spánku**: zařízení přejde do režimu spánku a použije malé množství energie z baterie. Počítač je stále zapnutý a otevřené aplikace a soubory jsou uložené v paměti RAM (Random Access Memory).
  - **Hibernace**: zařízení přejde do režimu hibernace. Otevřené aplikace a soubory se ukládají na pevný disk a zařízení se vypne.
  - **Vypnutí**: zařízení se vypíná. Otevřené aplikace a soubory se zavřou bez uložení.

  [CSP pro Power/SelectPowerButtonActionOnBattery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactiononbattery)

- **Tlačítko režimu spánku**: když zařízení používá napájení z baterie, vyberte, co se stane po výběru tlačítka režimu spánku. Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení může operační systém uživatelům dovolit řídit toto nastavení.
  - **Žádná akce**: zařízení zůstává zapnuté a nadále používá napájení z baterie.
  - **Režim spánku**: zařízení přejde do režimu spánku a použije malé množství poplatků za baterii. Počítač je stále zapnutý a otevřené aplikace a soubory jsou uložené v paměti RAM (Random Access Memory).
  - **Hibernace**: zařízení přejde do režimu hibernace. Otevřené aplikace a soubory se ukládají na pevný disk a zařízení se vypne.
  - **Vypnutí**: zařízení se vypíná. Otevřené aplikace a soubory se zavřou bez uložení.

  [CSP pro Power/SelectSleepButtonActionOnBattery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactiononbattery)

- **Hybridní režim spánku**: Pokud zařízení používá napájení z baterie, vyberte možnost povolit nebo zakázat hybridní režim spánku.

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení může operační systém uživatelům dovolit řídit toto nastavení.
  - **Povolit**: zařízení můžou přejít do hybridního režimu spánku. Otevřené aplikace a soubory jsou uložené v paměti Random Access (RAM) a na pevném disku. Používá malé množství poplatků za napájení.
  - **Zakázat**: zabrání zařízením přejít do hybridního režimu spánku.

  [CSP pro Power/TurnOffHybridSleepOnBattery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeponbattery)

### <a name="pluggedin"></a>PluggedIn

- **Úroveň baterie**: Pokud je zařízení napájené z energie, zadejte úroveň nabití baterie, abyste zapnuli úsporu energie z 0-100. Zadejte procentuální hodnotu, která označuje úroveň nabití baterie. Například když se nastaví na `80` , zapíná úspora energie, když má baterie 80%, nebo méně dostupné.

  Pokud nezadáte žádnou hodnotu, Intune toto nastavení nezmění ani neaktualizuje. Ve výchozím nastavení může operační systém nastavit na 70%.

  [CSP pro Power/EnergySaverBatteryThresholdPluggedIn](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdpluggedin)

- **Zavření víka (jenom mobilní)**: když je zařízení napájené z elektrické sítě, vyberte, co se stane po zavření víka. Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Žádná akce**: zařízení zůstane zapnuté.
  - **Režim spánku**: zařízení přejde do režimu spánku. Počítač je stále zapnutý a otevřené aplikace a soubory jsou uložené v paměti RAM (Random Access Memory).
  - **Hibernace**: zařízení přejde do režimu hibernace. Otevřené aplikace a soubory se ukládají na pevný disk a zařízení se vypne.
  - **Vypnutí**: zařízení se vypíná. Otevřené aplikace a soubory se zavřou bez uložení.
  
    [CSP pro Power/SelectLidCloseActionPluggedIn](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactionpluggedin)
  
- **Tlačítko napájení**: když je zařízení napájené z elektrické sítě, vyberte, co se stane po výběru tlačítka napájení. Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Žádná akce**: zařízení zůstane zapnuté.
  - **Režim spánku**: zařízení přejde do režimu spánku. Počítač je stále zapnutý a otevřené aplikace a soubory jsou uložené v paměti RAM (Random Access Memory).
  - **Hibernace**: zařízení přejde do režimu hibernace. Otevřené aplikace a soubory se ukládají na pevný disk a zařízení se vypne.
  - **Vypnutí**: zařízení se vypíná. Otevřené aplikace a soubory se zavřou bez uložení.

  [CSP pro Power/SelectPowerButtonActionPluggedIn](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactionpluggedin)

- **Tlačítko pro režim spánku**: když je zařízení napájené z elektrické sítě, vyberte, co se stane, když se vybere tlačítko režimu spánku. Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Žádná akce**: zařízení zůstane zapnuté.
  - **Režim spánku**: zařízení přejde do režimu spánku. Počítač je stále zapnutý a otevřené aplikace a soubory jsou uložené v paměti RAM (Random Access Memory).
  - **Hibernace**: zařízení přejde do režimu hibernace. Otevřené aplikace a soubory se ukládají na pevný disk a zařízení se vypne.
  - **Vypnutí**: zařízení se vypíná. Otevřené aplikace a soubory se zavřou bez uložení.

  [CSP pro Power/SelectSleepButtonActionPluggedIn](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactionpluggedin)

- **Hybridní režim spánku**: když je zařízení napájené ze sítě, vyberte možnost povolit nebo zakázat hybridní režim spánku.

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení může operační systém uživatelům dovolit řídit toto nastavení.
  - **Povolit**: zařízení můžou přejít do hybridního režimu spánku. Otevřené aplikace a soubory jsou uložené v paměti Random Access (RAM) a na pevném disku.
  - **Zakázat**: zabrání zařízením přejít do hybridního režimu spánku.

  [CSP pro Power/TurnOffHybridSleepPluggedIn](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeppluggedin)

## <a name="next-steps"></a>Další kroky

Další technické podrobnosti o jednotlivých nastaveních a podporovaných edicích Windows najdete v [referenčních informacích o poskytovateli konfiguračních služeb pro zásady (CSP) pro Windows 10](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider).

[Přiřaďte profil](device-profile-assign.md)a [sledujte jeho stav](device-profile-monitor.md).
