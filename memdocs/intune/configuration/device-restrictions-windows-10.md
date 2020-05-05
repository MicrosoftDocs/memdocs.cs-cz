---
title: Nastavení omezení zařízení s Windows 10 v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na seznam všech nastavení a jejich popisů pro vytváření omezení zařízení v zařízeních s Windows 10 a novějším. Pomocí těchto nastavení můžete v konfiguračním profilu řídit snímky obrazovky, požadavky na heslo, nastavení veřejného terminálu, aplikace v obchodě, prohlížeči Microsoft Edge, Microsoft Defender, přístup ke cloudu, nabídce Start a další informace v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4babd715df08a905a5ceed6ec881cbfe07f5de19
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2020
ms.locfileid: "82209869"
---
# <a name="windows-10-and-newer-device-settings-to-allow-or-restrict-features-using-intune"></a>Nastavení zařízení s Windows 10 (a novějším) pro povolení nebo omezení funkcí pomocí Intune

Tento článek obsahuje seznam a popis všech různých nastavení, která můžete řídit na zařízeních s Windows 10 a novějším. V rámci řešení pro správu mobilních zařízení (MDM) pomocí těchto nastavení můžete povolit nebo zakázat funkce, nastavit pravidla pro hesla, přizpůsobit zamykací obrazovce, používat Microsoft Defender a další.

Tato nastavení se přidají do konfiguračního profilu zařízení v Intune a pak se přiřadí nebo nasadí na vaše zařízení s Windows 10.

> [!Note]
> Ne všechny možnosti jsou k dispozici ve všech edicích systému Windows. Pokud chcete zobrazit podporované edice, přečtěte si téma [zásady CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider) (otevře se další web společnosti Microsoft).

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte profil konfigurace zařízení](device-restrictions-configure.md#create-the-profile).

## <a name="app-store"></a>App Store

Tato nastavení používají [zprostředkovatele CSP zásad ApplicationManagement](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement), který obsahuje také podporované edice Windows.

- **App Store** (jenom mobilní): **blok** brání koncovým uživatelům v přístupu k obchodu s aplikacemi na mobilních zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém může koncovým uživatelům povolit přístup k obchodu s aplikacemi.
- **Automatické aktualizace aplikací ze Storu**: **blok** zabraňuje automatické instalaci aktualizací z Microsoft Store. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat automatickou aktualizaci aplikací nainstalovaných z Microsoft Store.

  [CSP ApplicationManagement/AllowAppStoreAutoUpdate](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **Instalace důvěryhodných aplikací**: vyberte, jestli se můžou instalovat aplikace, které nejsou Microsoft Store, označované taky jako zkušební načtení. Probíhá instalace zkušebního načtení a následné spuštění nebo otestování aplikace, která není certifikována Microsoft Store. Například aplikace, která je interní pro vaši společnost. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Blok**: zabraňuje zkušebnímu načtení. NeMicrosoft Store aplikace se nedají nainstalovat.
  - **Povolit**: umožňuje zkušební načtení. Je možné nainstalovat aplikace, které nejsou Microsoft Store.
- **Odemčení pro vývojáře**: umožňuje povolit nastavení vývojářů pro Windows, jako je například umožnění úprav aplikací zkušebně načtené koncovými uživateli. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Blok**: znemožní vývojářský režim a aplikace pro zkušební načtení.
  - **Povolit**: povolí vývojářský režim a aplikace pro zkušební načtení.

  [Povolit pro vývoj zařízení](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development) Další informace o této funkci.
  
  [CSP ApplicationManagement/AllowAllTrustedApps](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **Sdílená data aplikací uživatele**: vyberte možnost **umožňuje** sdílet data aplikací mezi různými uživateli na stejném zařízení a dalšími instancemi této aplikace. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit sdílení dat s ostatními uživateli a dalšími instancemi stejné aplikace.

  [CSP ApplicationManagement/AllowSharedUserAppData](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowshareduserappdata)

- **Použít pouze privátní úložiště**: **povolí** možnost stahovat aplikace pouze z privátního úložiště a nestahovat z veřejného úložiště, včetně maloobchodního katalogu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém stahovat aplikace z privátního úložiště a z veřejného úložiště.

  [CSP ApplicationManagement/RequirePrivateStoreOnly](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-requireprivatestoreonly)

- **Spuštění aplikace pocházející ze Storu**: **blokování** zakáže všechny aplikace, které byly v zařízení předem nainstalovány, nebo stažené z Microsoft Store. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tyto aplikace otevřít.

  [CSP ApplicationManagement/DisableStoreOriginatedApps](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-disablestoreoriginatedapps)

- **Nainstalovat data aplikací na systémový svazek**: **blok** zastaví aplikacím ukládat data na systémový svazek zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat aplikacím ukládat data na diskový svazek.

  [CSP ApplicationManagement/RestrictAppDataToSystemVolume](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictappdatatosystemvolume)

- **Nainstalovat aplikace na systémovou jednotku**: **blokovat** znemožní aplikacím instalovat na systémovou jednotku na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat instalaci aplikací na systémovou jednotku.

  [CSP ApplicationManagement/RestrictAppToSystemVolume](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictapptosystemvolume)

- Záznam ze **hry** (jenom Desktop): **blokování** zakáže zaznamenávání a vysílání her ve Windows. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat zaznamenávání a vysílání her.

  [CSP ApplicationManagement/AllowGameDVR](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowgamedvr)

- **Jenom aplikace ze Storu**: Toto nastavení určuje uživatelské prostředí, když uživatelé nainstalují aplikace z jiných míst než z Microsoft Store. Nebrání instalaci obsahu ze zařízení USB, síťových sdílených složek ani jiných zdrojů, které nejsou v Internetu. Pomocí důvěryhodného prohlížeče můžete zajistit, aby tato ochrana fungovala podle očekávání.

  Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Ve výchozím nastavení může operační systém koncovým uživatelům dovolit instalovat aplikace z jiných míst než z Microsoft Store, včetně aplikací definovaných v jiných nastaveních zásad.  
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

- [CSP zásad sítě Wi-Fi](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wifi)

- **Mobilní datový kanál**: vyberte, jestli koncoví uživatelé můžou používat data, jako je procházení webu, při připojení k mobilní síti. Možnosti:
  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Koncoví uživatelé ji můžou vypnout.
  - **Blok**: nepovoluje mobilní datový kanál. Koncoví uživatelé je nemůžou zapnout.
  - **Povolit (není editovatelné)**: povoluje mobilní datový kanál. Koncoví uživatelé ji nemohou vypnout.

- **Datový roaming**: **blokování** zabraňuje mobilním datovým roamingu v zařízení. **Nenakonfigurováno** (výchozí) umožňuje roaming mezi sítěmi při přístupu k datům.
- **VPN přes mobilní síť**: **blok** zabraňuje zařízení v přístupu k připojením VPN v případě připojení k mobilní síti. **Nenakonfigurováno** (výchozí) umožňuje síti VPN použít jakékoli připojení, včetně mobilních.
- **Roaming VPN přes mobilní síť** **: při** roamingu v mobilní síti zastaví zařízení přístup k připojením VPN. **Nenakonfigurováno** (výchozí) umožňuje při roamingu připojení VPN.
- **Služba připojených zařízení**: **blok** zakáže komponentu platformy připojených zařízení (CDP). CDP umožňuje zjišťování a připojení k ostatním zařízením (přes Bluetooth/LAN nebo Cloud), aby podporovala spouštění vzdálených aplikací, vzdálené zasílání zpráv, relace vzdálených aplikací a další prostředí pro různé zařízení. **Nenakonfigurováno** (výchozí) povolí službu připojená zařízení, která umožňuje zjišťování a připojování k ostatním zařízením Bluetooth.
- **NFC**: **Block** zabraňuje možnostem technologie NFC (Near Field Communication). **Nenakonfigurováno** (výchozí) umožňuje uživatelům povolit a konfigurovat funkce NFC na zařízení.
- **Wi-Fi**: **blok** zabraňuje uživatelům v zařízení povolit, konfigurovat, konfigurovat a používat připojení Wi-Fi. **Nenakonfigurováno** (výchozí) umožňuje připojení Wi-Fi.
- **Automaticky se připojovat k Wi-Fi hotspotům**: **blokování** znemožňuje zařízením automaticky se připojovat k Wi-Fi hotspotům. **Nenakonfigurováno** (výchozí) umožňuje zařízením automaticky se připojovat k bezplatným Wi-Fi hotspotům a automaticky pro připojení přijímat jakékoli podmínky a ujednání.
- **Ruční konfigurace Wi-Fi**: **blok** zabraňuje zařízením v připojení k Wi-Fi mimo sítě instalované na MDM serveru. **Nenakonfigurováno** (výchozí) umožňuje koncovým uživatelům přidat a nakonfigurovat vlastní sítě SSID sítě Wi-Fi Connections.
- **Interval kontroly sítě Wi-Fi**: zadejte, jak často zařízení hledají sítě Wi-Fi. Zadejte hodnotu od 1 (nejčastější) do 500 (nejméně časté). Výchozí hodnota `0` je (nula).

### <a name="bluetooth"></a>Bluetooth

Tato nastavení používají [poskytovatele zásad Bluetooth](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth). Zobrazuje se taky podporované edice Windows.

- **Bluetooth**: **blok** znemožní uživatelům povolit Bluetooth. **Nenakonfigurováno** (výchozí) povolí Bluetooth na zařízení.
- **Zjistitelnost Bluetooth**: **blok** zabraňuje zařízení, aby bylo zjistitelné jinými zařízeními podporujícími technologii Bluetooth. **Nenakonfigurováno** (výchozí) umožňuje zjistit zařízení pomocí jiných zařízení s podporou technologie Bluetooth, jako je například sluchátka.
- **Předpárování Bluetooth**: **blokování** zabraňuje konkrétním zařízením Bluetooth, aby se automaticky spároval s hostitelským zařízením. **Nenakonfigurováno** (výchozí) umožňuje automatické párování s hostitelským zařízením.
- **Inzerce Bluetooth**: **blok** zabraňuje zařízení v posílání reklamy Bluetooth. **Nenakonfigurováno** (výchozí) umožňuje zařízení posílat reklamy přes Bluetooth.
- **Povolené služby Bluetooth**: **přidejte** seznam povolených služeb a profilů Bluetooth jako šestnáctkové řetězce, například `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`.

  [Průvodce používáním ServicesAllowedList](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#servicesallowedlist-usage-guide) obsahuje další informace o seznamu služeb.

## <a name="cloud-and-storage"></a>Cloud a úložiště

Tato nastavení používají [CSP v zásadách účtů](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-accounts); Zobrazuje se taky podporované edice Windows.

> [!IMPORTANT]
> Blokování nebo zakázání těchto nastavení účet Microsoft může mít vliv na scénáře registrace, které vyžadují, aby se uživatelé přihlásili ke službě Azure AD. Například používáte [šetrnější pro Autopilotu](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove). Uživatelům se obvykle zobrazuje okno pro přihlášení k Azure AD. Pokud jsou tato nastavení nastavená tak, aby **blokovala** nebo **zakázala**, možnost přihlášení k Azure AD se nemusí zobrazit. Místo toho se uživatelům zobrazí výzva k přijetí smlouvy EULA a vytvoření místního účtu, který nemusí být požadovaný.

- **Účet Microsoft**: **blok** brání koncovým uživatelům v přidružení účet Microsoft k zařízení. **Nenakonfigurováno** (výchozí) umožňuje přidání a použití účet Microsoft.

- **Bez účet Microsoft**: **blok** brání koncovým uživatelům v přidávání účtů mimo Microsoft pomocí uživatelského rozhraní. **Nenakonfigurováno** (výchozí) umožňuje uživatelům přidávat e-mailové účty, které nejsou přidružené k účet Microsoft.
- **Synchronizace nastavení pro účet Microsoft**: **Nenakonfigurováno** (výchozí) povolí synchronizaci nastavení zařízení a aplikací přidružených k účet Microsoftu mezi zařízeními. **Blok** zabraňuje této synchronizaci.
- **Pomocník pro přihlášení k účtu Microsoft**: Pokud je nastavené na **Nenakonfigurováno** (výchozí), koncoví uživatelé můžou spustit a zastavit službu **Microsoft account Signing Assistant** (wlidsvc). Tato služba operačního systému umožňuje uživatelům přihlašovat se k jejich účet Microsoft. **Disable** nakonfiguruje službu pomocníka pro přihlašování Microsoftu (wlidsvc) na zakázanou a zabrání koncovým uživatelům v ručním spuštění.

## <a name="cloud-printer"></a>Cloudová tiskárna

Tato nastavení používají [zprostředkovatele CSP v zásadách EnterpriseCloudPrint](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-enterprisecloudprint). Zobrazuje se taky podporované edice Windows.

- **Adresa URL pro zjišťování tiskáren**: zadejte adresu URL pro hledání cloudových tiskáren. Zadejte například `https://cloudprinterdiscovery.contoso.com`.
- **Adresa URL autority pro přístup k tiskárně**: zadejte adresu URL koncového bodu ověřování a získejte tokeny OAuth. Zadejte například `https://azuretenant.contoso.com/adfs`.
- **Identifikátor GUID nativní klientské aplikace Azure**: zadejte identifikátor GUID klientské aplikace, kterým se povoluje získat tokeny OAuth z OAuthAuthority. Zadejte například `E1CF1107-FF90-4228-93BF-26052DD2C714`.
- **Identifikátor URI prostředku tiskové služby**: zadejte identifikátor URI prostředku OAuth pro tiskovou službu nakonfigurovanou ve Azure Portal. Zadejte například `http://MicrosoftEnterpriseCloudPrint/CloudPrint`.
- **Maximální počet tiskáren pro dotaz**: zadejte maximální počet tiskáren, na které chcete zadat dotaz. Výchozí hodnota je `20`.
- **Identifikátor URI prostředku služby zjišťování tiskáren**: zadejte identifikátor URI prostředku OAuth pro službu zjišťování tiskáren nakonfigurovanou v Azure Portal. Zadejte například `http://MopriaDiscoveryService/CloudPrint`.

> [!TIP]
> Po nastavení [tisku hybridního cloudu Windows serveru](https://docs.microsoft.com/windows-server/administration/hybrid-cloud-print/hybrid-cloud-print-overview)můžete tato nastavení nakonfigurovat a pak nasadit na vaše zařízení s Windows.

## <a name="control-panel-and-settings"></a>Ovládací panely a nastavení

- **Nastavení aplikace**: **blok** zabraňuje koncovým uživatelům v přístupu k aplikaci nastavení systému Windows. **Nenakonfigurováno** (výchozí) umožňuje uživatelům otevřít na zařízení aplikaci nastavení.
  - **System**: **Block** znemožní přístup k systémové oblasti aplikace nastavení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
    - **Změny nastavení napájení a režimu spánku** (jenom desktopové služby): **blok** znemožní koncovým uživatelům měnit nastavení napájení a režimu spánku na zařízení. **Nenakonfigurováno** (výchozí) umožňuje uživatelům změnit nastavení napájení a režimu spánku.
  - **Zařízení**: **blok** znemožní přístup k oblasti zařízení aplikace nastavení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
  - **Síť Internet**: **blok** znemožní přístup k síti & internetovou oblast aplikace nastavení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
  - **Přizpůsobení**: **blok** brání v přístupu k oblasti přizpůsobení aplikace nastavení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
  - **Aplikace**: **blok** znemožní přístup k oblasti aplikace v aplikaci nastavení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
  - **Accounts**: **Block** zabrání přístupu k oblasti účtů aplikace nastavení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
  - **Čas a jazyk**: **blok** znemožní přístup k oblasti času & jazyka aplikace nastavení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
    - **Změna systémového času**: **blok** znemožní koncovým uživatelům změnit nastavení data a času v zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Uživatelé můžou tato nastavení změnit.
    - **Změny nastavení oblasti** (jenom desktopové): **blok** znemožní koncovým uživatelům změnit nastavení oblasti na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Uživatelé můžou tato nastavení změnit.
    - **Změny nastavení jazyka (jenom desktopové verze)**: **blok** znemožní koncovým uživatelům změnit nastavení jazyka v zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Uživatelé můžou tato nastavení změnit.

      [Zásady nastavení – CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings)

  - **Hraní her**: **blok** znemožní přístup k herní oblasti aplikace nastavení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
  - **Usnadnění přístupu**: **blok** znemožní přístup k oblasti snadného přístupu v aplikaci nastavení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
  - **Ochrana osobních údajů**: **blok** znemožní přístup k oblasti soukromí v aplikaci nastavení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
  - **Aktualizace a zabezpečení**: **blok** znemožní přístup k oblasti zabezpečení & aktualizace aplikace nastavení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

## <a name="display"></a>Displej

Tato nastavení používají [zprostředkovatele CSP v zásadách zobrazení](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-display). Zobrazuje se taky podporované edice Windows.

Škálování DPI GDI umožňuje aplikacím, které nepodporují rozlišení DPI, přesměrovat na monitorované rozlišení DPI.

- **Zapnout ŠKÁLOVÁNÍ GDI pro aplikace**: **přidejte** starší verze aplikací, u kterých chcete zapnout škálování dpi GDI. Zadejte například `filename.exe` nebo `%ProgramFiles%\Path\Filename.exe`.

  Měřítko DPI GDI je zapnuté pro všechny starší verze aplikací v seznamu.

- **Vypnout škálování GDI pro aplikace**: **přidejte** starší verze aplikací, u kterých chcete škálování dpi GDI vypnuté. Zadejte například `filename.exe` nebo `%ProgramFiles%\Path\Filename.exe`.

  Měřítko DPI GDI je vypnuto pro všechny starší aplikace v seznamu.

Můžete také **naimportovat** soubor. CSV se seznamem aplikací.

## <a name="general"></a>Obecné

Tato nastavení používají [poskytovatele cloudových zásad](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience) Zobrazuje se taky podporované edice Windows. 

- **Snímek obrazovky** (jenom mobilní): **blok** znemožňuje koncovým uživatelům získat na zařízení snímky obrazovky. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Kopírování a vkládání (jenom mobilní)**: **blok** brání koncovým uživatelům v používání kopírování a vkládání mezi aplikacemi na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Ruční zrušení registrace**: **blok** znemožní koncovým uživatelům odstranit pracovní účet pomocí ovládacích panelů na pracovišti na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  Nastavení této zásady se nepoužije, pokud je počítač připojený k Azure AD a je povolená Automatická registrace.

- **Ruční instalace kořenového certifikátu** (jenom mobilní zařízení): **blok** brání koncovým uživatelům v ruční instalaci kořenových certifikátů a zprostředkujících certifikátů Cap. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Kamera**: **Block** znemožní koncovým uživatelům používat fotoaparát na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat přístup k kameře zařízení.

  Intune spravuje jenom přístup k kameře zařízení. Nemá přístup k obrázkům a videím.

  [CSP pro kameru](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-camera)

- **Synchronizace souborů na OneDrivu**: **blok** brání koncovým uživatelům v synchronizaci souborů s OneDrivem ze zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Vyměnitelné úložiště**: **blok** zabraňuje koncovým uživatelům v používání externích úložných zařízení, jako jsou karty SD, se zařízením. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Zeměpisná poloha**: **blok** brání koncovým uživatelům v zapnutí služby zjišťování polohy na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Sdílení internetu**: **blok** zabraňuje sdílení internetového připojení na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Resetování telefonu**: **blok** brání koncovým uživatelům v vymazání nebo obnovení továrního nastavení v zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Připojení USB**: **blok** zabraňuje přístupu k externímu úložnému zařízení přes připojení USB na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Toto nastavení neovlivňuje zpoplatnění přes USB.
- **Režim AntiTheft** (jenom mobilní): **blok** brání koncovým uživatelům v výběru předvolby režimu AntiTheft na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Cortana**: **Block** zakáže hlasového asistenta Cortany na zařízení. Když je Cortana vypnutá, uživatelé můžou pořád vyhledávat položky v zařízení. **Nenakonfigurováno** (výchozí) umožňuje Cortaně.
- **Záznam hlasu** (jenom mobilní): **blok** znemožní koncovým uživatelům používat na zařízení záznam hlasu zařízení. **Nenakonfigurováno** (výchozí) umožňuje záznam hlasu pro aplikace.
- **Úprava názvu zařízení** (jenom mobilní): **blok** brání koncovým uživatelům ve změně názvu zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Přidat zřizovací balíčky**: **blok** zabraňuje agentovi konfigurace běhu, který instaluje zřizovací balíčky na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Odebrat zřizovací balíčky**: **blok** zabraňuje agentům konfigurace běhu, který ze zařízení odebírá zřizovací balíčky. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Zjišťování zařízení**: **blok** zabraňuje tomu, aby se zařízení zjistilo jinými zařízeními. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Přepínání úloh** (jenom mobilní): **blok** zabraňuje přepínání úloh na zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Chybový dialog SIM karty** (jenom mobilní): **blokovat** zobrazování chybových zpráv na zařízení, pokud se nezjistí žádná SIM karta. **Nenakonfigurováno** (výchozí) zobrazí chybové zprávy.
- **Pracovní prostor Ink**: vyberte, jestli a jak má uživatel přístup k pracovnímu prostoru rukopisu. Možnosti:
  - **Nenakonfigurováno** (výchozí): zapne pracovní prostor rukopisu a uživatel ho může používat nad zamykací obrazovkou.
  - **Zakázáno na zamykací obrazovce**: pracovní prostor Ink je povolen a funkce je zapnutá. Ale uživatel k němu nemá přístup nad zamykací obrazovkou.
  - **Zakázáno**: přístup k pracovnímu prostoru Ink je zakázán. Tato funkce je vypnutá.

  [CSP zásad WindowsInkWorkspace](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsinkworkspace)

- **Automatické opětovné nasazení**: vyberte **Povolit** , aby uživatelé s právy správce mohli odstranit všechna uživatelská data a nastavení pomocí **kombinace kláves Ctrl + Win + R** na zamykací obrazovce zařízení. Zařízení se automaticky překonfiguruje a znovu zaregistruje do správy. **Nenakonfigurováno** (výchozí) zabrání této funkci.
- Vyžadovat, aby se **Uživatelé během instalace zařízení připojili k síti**: vyberte **vyžadovat** , aby se zařízení připojovalo k síti před tím, než bude instalace systému Windows po síti. **Nenakonfigurováno** (výchozí) umožňuje uživatelům přejít přes stránku síť, i když není připojen k síti.

  Nastavení se projeví při příštím vymazání nebo resetování zařízení. Stejně jako u jakékoli jiné konfigurace Intune musí být zařízení zaregistrované a spravované přes Intune, aby přijímalo nastavení konfigurace. Ale jakmile je zaregistrované, a když se dostávají zásady, zařízení resetuje nastavení v průběhu příští instalace Windows.

  [TenantLockdown CSP](https://docs.microsoft.com/windows/client-management/mdm/tenantlockdown-csp)

- **Přímý přístup do paměti**: **blok** zabraňuje přímému přístupu do paměti (DMA) pro všechny bezplatných portů PCI pro příjem dat, dokud se uživatel přihlásí do systému Windows. **Povoleno** (výchozí) umožňuje přístup k DMA i v případě, že uživatel není přihlášený.

  [Poskytovatel CSP pro DataProtection/AllowDirectMemoryAccess](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess)

- **Ukončit procesy ze Správce úloh**: Toto nastavení určuje, jestli uživatelé bez oprávnění správce můžou k ukončení úloh používat Správce úloh. **Blok** zabraňuje standardním uživatelům (bez správců) v používání Správce úloh k ukončení procesu nebo úlohy v zařízení. **Nenakonfigurováno** (výchozí) umožňuje standardním uživatelům ukončit proces nebo úlohu pomocí Správce úloh.

## <a name="locked-screen-experience"></a>Prostředí zamknuté obrazovky

- **Oznámení centra akcí (jenom mobilní)**: **blok** zabraňuje zobrazování oznámení centra akcí na zamykací obrazovce zařízení. **Nenakonfigurováno** (výchozí) umožňuje uživatelům zvolit, které aplikace budou zobrazovat oznámení na zamykací obrazovce.

  [CSP AboveLock/AllowActionCenterNotifications](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#AboveLock_AllowActionCenterNotifications)

- **Adresa URL obrázku pro zamknutou obrazovku (jenom desktopové aplikace)**: zadejte adresu URL obrázku ve formátu jpg, JPEG nebo PNG, který se používá jako tapeta zamykací obrazovky Windows. Zadejte například `https://contoso.com/image.png`. Toto nastavení zamkne obrázek a nedá se změnit.

  [Přizpůsobení/LockScreenImageUrl CSP](https://docs.microsoft.com/windows/client-management/mdm/personalization-csp)

- **Uživatelem konfigurovatelný časový limit obrazovky (jenom mobilní)**: **Povolení** umožňuje uživatelům nakonfigurovat časový limit obrazovky. **Nenakonfigurováno** (výchozí) neuděluje uživatelům tuto možnost.

  [CSP DeviceLock/AllowScreenTimeoutWhileLockedUserConfig](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#DeviceLock_AllowScreenTimeoutWhileLockedUserConfig)

- **Cortana na uzamčené obrazovce** (jenom stolní počítače): **blok** zabraňuje uživatelům v interakci s Cortana, když je zařízení na zamykací obrazovce. **Nenakonfigurováno** (výchozí) umožňuje interakci s Cortana.

  [CSP AboveLock/AllowCortanaAboveLock](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowcortanaabovelock)

- **Informační zprávy na uzamčené obrazovce**: **blok** znemožní zobrazování oznámení na zamykací obrazovce zařízení. **Nenakonfigurováno** (výchozí) povolí tato oznámení.

  [CSP AboveLock/AllowToasts](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowtoasts)

- **Časový limit obrazovky (jenom mobilní zařízení)**: Nastavte dobu trvání (v sekundách) na zamykací obrazovce na obrazovku vypnutí. Podporované hodnoty jsou 11-1800. Zadejte `300` například, pokud chcete nastavit tento časový limit na 5 minut.

  [CSP DeviceLock/ScreenTimeoutWhileLocked](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#DeviceLock_ScreenTimeoutWhileLocked)

## <a name="messaging"></a>Zasílání zpráv

Tato nastavení používají [zásady zasílání zpráv CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-messaging); Zobrazuje se taky podporované edice Windows.

- **Synchronizace zpráv (jenom mobilní zařízení)**: **blok** zakáže zálohování a obnovování textových zpráv a synchronizaci zpráv mezi zařízeními s Windows. Vypnutí pomáhá zabránit ukládání informací na serverech mimo řízení organizace. **Nenakonfigurováno** (výchozí) umožňuje uživatelům měnit tato nastavení a synchronizovat jejich zprávy.
- **MMS (jenom mobilní)**: **blokování** zakáže na zařízení funkci Send a Receive MMS. V případě podniků použijte tuto zásadu k zakázání MMS na zařízeních v rámci požadavku auditování nebo správy. **Nenakonfigurováno** (výchozí) umožňuje odeslat a přijmout MMS.
- **RCS (jenom mobilní)**: **blokování** zakáže na zařízení funkci posílání a přijímání RCS (Rich Communication Services). V případě podniků použijte tuto zásadu k zakázání RCS na zařízeních v rámci požadavku auditování nebo správy. **Nenakonfigurováno** (výchozí) umožňuje RCS Odeslat a přijmout.

## <a name="microsoft-edge-browser"></a>Prohlížeč Microsoft Edge

Tato nastavení používají [zprostředkovatele CSP zásad prohlížeče](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser), který také uvádí podporované edice systému Windows.

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
  - **Vlastní úvodní stránky**: Zadejte úvodní stránky, například `http://www.contoso.com`. Microsoft Edge načte úvodní stránky, které zadáte.
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
- **Tlačítko pro povolení uživatelů změnit domů**: **Ano** umožňuje uživatelům změnit tlačítko domů. Změny uživatele přepíší všechna nastavení správce na tlačítko domů. **Ne** (výchozí) znemožní uživatelům měnit způsob, jakým Správce nakonfiguroval tlačítko domů.
- **Zobrazit stránku prvního spuštění (jenom mobilní)**: **Ano** (výchozí) zobrazuje úvodní stránku použití v Microsoft Edge. **No** zastaví zobrazování úvodní stránky při prvním spuštění Microsoft Edge. Tato funkce umožňuje podnikům, jako jsou například organizace zaregistrované v konfiguracích s nulovou emisemi, blokovat tuto stránku.
- **Umístění seznamu adres URL prvního spuštění** (jenom Windows 10 Mobile): zadejte adresu URL, která odkazuje na soubor XML, který obsahuje adresy URL prvního spuštění stránky. Zadejte například `https://www.contoso.com/sites.xml`.

- **Aktualizovat prohlížeč po době nečinnosti**: zadejte počet minut nečinnosti, než se prohlížeč aktualizuje, od 0-1440 minut. Výchozí hodnota `5` je minuty. Při nastavení na `0` hodnotu (nula) se prohlížeč po nečinnosti neaktualizuje.

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
  - **Na stránkách začátek a nová karta**: zobrazí panel Oblíbené, když se spustí Microsoft Edge a na všech stránkách karty. Koncoví uživatelé můžou toto nastavení změnit.
  - **On Pages**: zobrazí panel Oblíbené na všech stránkách. Koncoví uživatelé nemůžou toto nastavení změnit.
  - **Skrytý**: skryje panel Oblíbené na všech stránkách. Koncoví uživatelé nemůžou toto nastavení změnit.
- **Povolit změny oblíbených položek**: **Ano** (výchozí) použije výchozí nastavení operačního systému, které umožňuje uživatelům změnit seznam. **Žádné** nebrání koncovým uživatelům v přidávání, importu, řazení a úpravách seznamu oblíbených položek.
  - **Seznam oblíbených položek**: přidejte do souboru oblíbených položek seznam adres URL. Přidejte například `http://contoso.com/favorites.html`.
- **Synchronizovat oblíbené položky mezi prohlížeči Microsoft** (jenom desktopové aplikace): **Ano** vynutí, aby Windows synchronizoval oblíbené položky mezi Internet Explorerem a Microsoft Edgem. Přidání, odstranění, úpravy a změna pořadí oblíbených položek jsou sdíleny mezi prohlížeči.  **Ne** (výchozí) používá výchozí nastavení operačního systému, které může uživatelům umožnit synchronizaci oblíbených položek mezi prohlížeči.
- **Výchozí vyhledávací modul**: Vyberte výchozí vyhledávací web na zařízení. Koncoví uživatelé mohou tuto hodnotu kdykoli změnit. Možnosti:
  - Vyhledávací modul v nastavení klienta Microsoft Edge
  - Bing
  - Google
  - Yahoo
  - Vlastní hodnota: v **adrese URL XML OpenSearch**zadejte adresu URL protokolu HTTPS se souborem XML, který obsahuje krátký název a adresu URL vyhledávacího stroje. Zadejte například `https://www.contoso.com/opensearch.xml`.
- **Zobrazit návrhy hledání**: **Ano** (výchozí) umožňuje vyhledávacímu webu navrhovat při psaní frází hledání na adresním řádku. Tato funkce **není** zabráněno.
- **Povolit změny vyhledávacího modulu**: **Ano** (výchozí) umožňuje uživatelům přidávat nové vyhledávací moduly nebo měnit výchozí vyhledávací web na Microsoft Edge. Pokud chcete uživatelům zabránit v přizpůsobení vyhledávacího modulu, klikněte na **ne** .

  Toto nastavení je dostupné, jenom když běží v [normálním režimu (veřejný terminál s více aplikacemi)](#use-microsoft-edge-kiosk-mode).

### <a name="privacy-and-security"></a>Ochrana osobních údajů a zabezpečení

- **Povolit procházení InPrivate**: **Ano** (výchozí) povolí procházení InPrivate v Microsoft Edge. Po zavření všech karet InPrivate odstraní Microsoft Edge data procházení ze zařízení. **Žádné** zabraňuje koncovým uživatelům otevírat relace procházení InPrivate.
- **Uložit historii procházení**: **Ano** (výchozí) povolí ukládání historie procházení v Microsoft Edge. **No** nebrání ukládání historie procházení.
- **Vymazat údaje o procházení při ukončení** (jenom desktopové aplikace): **Ano** vymaže historii a data se procházejí, když uživatel ukončí Microsoft Edge. **Ne** (výchozí) používá výchozí operační systém, který může ukládat data procházení do mezipaměti.
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
- **Odeslat hlavičky do Not Track**: **Ano** odešle hlavičky do Not Track pro weby požadující informace o sledování (doporučeno). **Ne** (výchozí) neodesílají hlavičky, které umožňují webům sledovat uživatele. Uživatel může nakonfigurovat.
- **Zobrazit IP adresu WebRTC localhost**: **Ano** (výchozí) povolí zobrazení IP adresy místního hostitele pro uživatele při telefonickém volání pomocí tohoto protokolu. Možnost **ne** zabrání zobrazení IP adresy místního hostitele uživatele. 
- **Povolit shromažďování dat živé dlaždice**: **Ano** (výchozí) umožňuje Microsoft Edge shromažďovat informace z živých dlaždic připnuté do nabídky Start. **Žádné** nebrání shromažďování těchto informací, což může uživatelům poskytnout omezené prostředí.
- **Uživatel může přepsat chyby certifikátu**: **Ano** (výchozí) umožňuje uživatelům přístup k webům s chybami protokolu SSL/TLS (SSL (Secure Sockets Layer)/Transport Layer Security). **Ne** (doporučeno pro zvýšené zabezpečení) znemožní uživatelům přístup k webům s chybami SSL nebo TLS.

### <a name="additional"></a>Další

- **Povolit prohlížeč Microsoft Edge** (jenom mobilní zařízení): **Ano** (výchozí) umožňuje používat na mobilním zařízení webový prohlížeč Microsoft Edge. Na zařízení **nebrání použití** Microsoft Edge. Pokud zvolíte **ne**, ostatní individuální nastavení platí pouze pro plochu.
- Možnost **Povolit panel Adresa**: **Ano** (výchozí) umožňuje, aby Microsoft Edge zobrazoval rozevírací seznam s panelem Adresa se seznamem návrhů. V takovém případě se v rozevíracím seznamu při psaní **nezastaví zobrazení** seznamu návrhů v Microsoft Edge. Pokud je nastavena na **ne**, můžete:
  - Můžete minimalizovat šířku pásma sítě mezi Microsoft Edge a službami Microsoftu.
  - Zakažte možnost **Zobrazit hledání a návrhy webu při psaní** v nastavení Microsoft Edge >.
- **Povolit režim zobrazení na celé obrazovce**: **Ano** (výchozí) umožňuje, aby Microsoft Edge používal režim celé obrazovky, který zobrazuje jenom webový obsah a skrývá uživatelské rozhraní Microsoft Edge. V Microsoft **Edge znemožní režim** celoobrazovkového režimu.
- **Stránka povolení o příznacích**: **Ano** (výchozí) použije výchozí nastavení operačního systému, které může umožňovat `about:flags` přístup k této stránce. Tato `about:flags` stránka umožňuje uživatelům změnit nastavení vývojáře a povolit experimentální funkce. **Žádné** zabrání koncovým uživatelům v `about:flags` přístupu k stránce v Microsoft Edge.
- **Povolit vývojářské nástroje**: **Ano** (výchozí) umožňuje uživatelům používat nástroje F12 Developer Tools k vytváření a ladění webových stránek ve výchozím nastavení. **Žádné** nebrání koncovým uživatelům v používání vývojářských nástrojů F12.
- **Povolit jazyk JavaScript**: **Ano** (výchozí) umožňuje spouštění skriptů, jako je například JavaScript, v prohlížeči Microsoft Edge. **Žádné** zabraňuje spuštění skriptů Java v prohlížeči.
- **Uživatel může nainstalovat rozšíření**: **Ano** (výchozí) umožňuje koncovým uživatelům instalovat na zařízení rozšíření Microsoft Edge. **Nebrání instalaci** .
- **Povolení zkušebního načtení rozšíření pro vývojáře**: **Ano** (výchozí) používá výchozí operační systém, který může umožňovat zkušební načtení. Zkušební načtení nainstaluje a spustí neověřená rozšíření. Možnost **nijak** nebrání Microsoft Edge ve zkušebním načtení pomocí funkce **rozšíření zatížení** . Nebrání rozšíření zkušebního načtení jiným způsobem, jako je například PowerShell.
- **Požadovaná rozšíření**: vyberte, která rozšíření nemohou být vypnutá koncovými uživateli v Microsoft Edge. Zadejte názvy rodin balíčků a vyberte **Přidat**. Pokyny [pro připojení k síti VPN pro jednotlivé aplikace najdete v části název rodiny balíčků (PFN)](https://docs.microsoft.com/configmgr/protect/deploy-use/find-a-pfn-for-per-app-vpn) .

  Můžete také **importovat** soubor CSV, který obsahuje názvy rodin balíčků. Případně **exportujte** názvy rodin balíčků, které zadáte.

## <a name="network-proxy"></a>Síťový proxy server

Tato nastavení používají [zprostředkovatele CSP zásad NetworkProxy](https://docs.microsoft.com/windows/client-management/mdm/networkproxy-csp), který obsahuje také podporované edice Windows.

- **Automaticky zjišťovat nastavení proxy serveru**: **blokování** zakáže automatické rozpoznání skriptu PAC (proxy auto config) zařízení. **Nenakonfigurováno** (výchozí) povolí tuto funkci. Pokud je tato možnost povolena, zařízení se pokusí najít cestu ke skriptu PAC.
- **Použít skript proxy serveru**: **pokud chcete nakonfigurovat** proxy server, zadejte cestu k vašemu skriptu PAC. **Nenakonfigurováno** (výchozí) neumožňuje zadat adresu URL skriptu PAC.
  - **Nastavení adresy URL skriptu**: zadejte adresu URL skriptu PAC, který chcete použít ke konfiguraci proxy server.
- **Použít ruční proxy server**: vyberte možnost **povoluje** ruční zadání názvu nebo IP adresy a čísla portu TCP proxy server. **Nenakonfigurováno** (výchozí) neumožňuje ručně zadat podrobnosti o proxy server.
  - **Adresa**: zadejte název nebo IP adresu proxy server.
  - **Číslo portu**: zadejte číslo portu proxy server.
  - **Výjimky proxy serveru**: Zadejte všechny adresy URL, které nesmí používat proxy server. Jednotlivé položky oddělte středníkem.
  - **Bypass proxy server pro místní adresu**: **nenakonfigurovaná** (výchozí) zabraňuje použití proxy server pro místní adresy na vašem intranetu. Možnost **Allow** používá proxy server pro místní adresy.

## <a name="password"></a>Heslo

Tato nastavení používají [zprostředkovatele CSP zásad DeviceLock](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock), který obsahuje také podporované edice Windows.

- **Heslo**: **vyžaduje** , aby koncový uživatel zadal heslo pro přístup k zařízení. **Nenakonfigurováno** (výchozí) povolí přístup k zařízení bez hesla. Platí jenom pro místní účty. Hesla doménového účtu zůstávají nakonfigurovaná službou Active Directory (AD) a službou Azure AD.

  - **Vyžadovaný typ hesla**: Vyberte typ hesla. Možnosti:
    - **Nenakonfigurováno**: heslo může obsahovat číslice a písmena.
    - **Číselná**: heslo musí obsahovat pouze čísla.
    - **Alfanumerické**: heslo musí být kombinací číslic a písmen.
  - **Minimální délka hesla**: zadejte minimální počet požadovaných znaků, od 4-16. Zadejte `6` například, pokud chcete, aby délka hesla vyžadovala alespoň šest znaků.
  
    > [!IMPORTANT]
    > Když se požadavek na heslo změní na plochu Windows, uživatelé budou mít vliv na jeho příštím přihlášení, protože to znamená, že zařízení přestane být aktivní. Uživatelům s hesly, kteří splňují požadavky, se stále zobrazí výzva ke změně hesla.
    
  - **Počet neúspěšných přihlášení před vymazáním zařízení**: zadejte počet povolených selhání ověřování, než může být zařízení vymazáno, až 11. Platné číslo, které zadáte, závisí na edici. [DeviceLock/MAXDEVICEPASSWORDFAILEDATTEMPTS CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts) obsahuje seznam podporovaných hodnot. `0`(nula) může zakázat funkci vymazání zařízení.

    Toto nastavení má také jiný dopad v závislosti na edici. Konkrétní podrobnosti o tomto nastavení najdete v tématu [CSP pro DeviceLock/MaxDevicePasswordFailedAttempts](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts).

  - **Maximální počet minut nečinnosti, po kterém se uzamkne obrazovka**: zadejte dobu, po kterou musí být zařízení v nečinnosti, než se zamkne obrazovka.
  - **Vypršení platnosti hesla (dny)**: zadejte dobu ve dnech, kdy musí být heslo zařízení změněno, od 1-365. Zadejte `90` například platnost hesla po 90 dnech.
  - **Zakázat opakované použití předchozích hesel**: zadejte počet dříve použitých hesel, která se nedají použít, od 1-24. Například zadejte `5` , že uživatelé nemůžou nastavit nové heslo na aktuální heslo ani na žádná z předchozích čtyř hesel.
  - **Vyžadovat heslo při návratu zařízení ze stavu nečinnosti** (mobilní a holografické): vyberte **vyžadovat** , aby uživatelé před nečinným zařízením museli odemknout heslo. **Není nakonfigurováno** (výchozí) při obnovení zařízení ze stavu nečinnosti nevyžaduje PIN kód ani heslo.
  - **Jednoduchá hesla**: nastavte **blokování** , aby uživatelé nemohli vytvářet jednoduchá hesla, například `1234` nebo. `1111` Nastavte na **Nenakonfigurováno** (výchozí), aby uživatelé mohli vytvářet `1234` hesla `1111`, například nebo. Toto nastavení také povolí obrázková hesla Windows (nebo je zablokuje).
- **Automatické šifrování během AADJ**: **blok** zabraňuje automatickému šifrování zařízení bitlockerem, když je zařízení připravené k prvnímu použití, když je zařízení připojené ke službě Azure AD. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Další informace o [šifrování zařízení nástrojem BitLocker](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-device-encryption-overview-windows-10#bitlocker-device-encryption).

  [CSP pro zabezpečení/PreventAutomaticDeviceEncryptionForAzureADJoinedDevices](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-security#security-preventautomaticdeviceencryptionforazureadjoineddevices)

- **Zásada FIPS (Federal Information Processing Standard)**: **povoluje** použití zásad FIPS (Federal Information Processing Standard), což je standard státní správy USA pro šifrování, algoritmus hash a podepisování. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Výchozí operační systém nemůže používat FIPS.

  [Kryptografie/AllowFipsAlgorithmPolicy CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-cryptography#cryptography-allowfipsalgorithmpolicy)

- **Ověřování zařízení ve Windows Hello**: **umožňuje** uživatelům používat doprovodné zařízení Windows Hello, jako je telefon, síť vhodnosti nebo zařízení IoT, pro přihlášení k počítači s Windows 10. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Výchozí operační systém může zabránit tomu, aby se doprovodná zařízení Windows Hello mohla ověřit ve Windows.

  [Ověřování/AllowSecondaryAuthenticationDevice CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-allowsecondaryauthenticationdevice)

- **Webové přihlášení** (zastaralé): umožňuje přihlášení Windows pro federované zprostředkovatele bez služby ADFS (Active Directory Federation Services (AD FS)), jako je například Security ASSERTION MARKUP Language (SAML). SAML používá zabezpečené tokeny, které poskytují webovým prohlížečům jednotné přihlašování (SSO). Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Povoleno**: poskytovatel přihlašovacích údajů webu je povolen pro přihlášení.
  - **Zakázáno**: poskytovatel přihlašovacích údajů webu je zakázán pro přihlášení.

  Toto nastavení se v nadcházející verzi odebere. Toto nastavení nepoužívejte.

  [Ověřování/EnableWebSignIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-enablewebsignin)

- **Upřednostňovaná doména tenanta Azure AD**: zadejte název existující domény v organizaci Azure AD. Když se uživatelé v této doméně přihlásí, nemusí zadávat název domény. Zadejte například `contoso.com`. Uživatelé v `contoso.com` doméně se můžou přihlásit pomocí svého uživatelského jména, jako `abby`je místo. `abby@contoso.com`

  [Ověřování/PreferredAadTenantDomainName CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-preferredaadtenantdomainname)

## <a name="per-app-privacy-exceptions"></a>Výjimky ze zásad ochrany osobních údajů pro jednotlivé aplikace

Můžete přidat aplikace, které by měly mít jiné chování ochrany osobních údajů než z toho, co definujete v části "výchozí ochrana osobních údajů".

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

## <a name="printer"></a>Tiskárna

- **Tiskárny**: seznam místních tiskáren, které byly přidány.
- **Výchozí tiskárna**: Nastavte výchozí tiskárnu.
- **Přístup uživatelů k přidávání nových tiskáren**: povolí nebo zablokuje používání místních tiskáren.

## <a name="privacy"></a>Ochrana osobních údajů

Tato nastavení používají [CSP zásady ochrany osobních údajů](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy), který také uvádí podporované edice Windows.

- **Přizpůsobení vstupu**: **blok** zabraňuje použití hlasu pro diktování a komunikaci s Cortana a dalšími aplikacemi, které využívají rozpoznávání řeči od Microsoftu. Je zakázaná a uživatelé nemůžou povolit online rozpoznávání řeči pomocí nastavení. **Nenakonfigurováno** (výchozí) umožňuje uživatelům zvolit. Pokud povolíte tyto služby, může společnost Microsoft shromažďovat hlasová data pro zlepšení služby.
- **Automatické přijetí párování a výzev k souhlasu uživatele s ochranou osobních údajů**: vyberte možnost **umožnit** , aby systém Windows mohl automaticky přijímat párování a zprávy o souhlasu s ochranou osobních údajů při spouštění aplikací. **Nenakonfigurováno** (výchozí) zabraňuje automatickému přijetí párování a okna souhlasu uživatele s ochranou osobních údajů při otevírání aplikací.
- **Publikování aktivit uživatelů**: **blok** zabraňuje sdíleným prostředím a zjišťování naposledy použitých prostředků v informačním kanálu o aktivitách. **Nenakonfigurováno** (výchozí) povolí tuto funkci, aby aplikace mohla publikovat aktivity koncového uživatele.
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

- **Vstup uživatele z přijímačů bezdrátového zobrazení**: **blok** brání vstupu uživatele z přijímačů bezdrátového zobrazení. **Nenakonfigurováno** (výchozí) umožňuje bezdrátové zobrazení odesílání klávesnice, myši, pera a dotykového vstupu zpět na zdrojové zařízení.
- **Projekce na tento počítač**: **blok** znemožní ostatním zařízením najít zařízení pro projekci. **Nenakonfigurováno** (výchozí) umožňuje, aby bylo zařízení zjistitelné a bylo možné projektovat do zařízení nad zamykací obrazovkou.
- **Vyžadovat pro párování PIN**: vyberte **vyžadovat** , když se při připojování k zařízení projekce má vždycky VYZVAT k zadání PIN kódu. **Nenakonfigurováno** (výchozí) nevyžaduje PIN kód pro spárování zařízení se zařízením projekce.

## <a name="reporting-and-telemetry"></a>Generování sestav a telemetrie

- **Sdílet data o využití**: vyberte úroveň diagnostických dat, která se odešlou. Možnosti:
  - **Nenakonfigurováno**: nejsou sdílena žádná data.
  - **Zabezpečení**: informace, které jsou nutné k zajištění vyššího zabezpečení systému Windows, včetně údajů o nastavení komponenty prostředí s připojeným uživatelem a telemetriem, nástroji pro odebrání škodlivého softwaru a programu Microsoft Defender.
  - **Basic**: základní informace o zařízení, včetně dat týkajících se kvality, kompatibility aplikací, dat o využití aplikací a dat z úrovně zabezpečení.
  - **Rozšířené**: Další přehledy, včetně: jak se používají Windows, Windows Server, System Center a aplikace, jak provádějí, pokročilá data o spolehlivosti a data ze základní i úrovně zabezpečení.
  - **Úplné**: všechna data potřebná pro identifikaci a pomoc při řešení problémů a data z úrovní zabezpečení, základní a rozšířené úrovně.

  [CSP pro System/AllowTelemetry](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

- **Odeslat data o procházení Microsoft Edge do Microsoft 365 Analytics**: Pokud chcete tuto funkci používat, nastavte nastavení **sdílet data o využití** na **Rozšířené** nebo **úplné**. Tato funkce řídí, jaká data Microsoft Edge odesílá Microsoft 365 analýze pro podniková zařízení s nakonfigurovaným komerčním ID. Možnosti:
  - **Nenakonfigurováno**: Intune toto nastavení nemění ani neaktualizuje. Výchozí operační systém nemusí odesílat žádná data historie procházení.
  - **Odesílat jenom intranetová data**: umožňuje správcům odesílat historii dat intranetu.
  - **Odesílat pouze Internetová data**: umožňuje správcům odesílat historii internetových dat.
  - **Odesílat intranetová a Internetová data**: umožňuje správcům odesílat historii intranetových a internetových dat.

  [CSP pro Browser/ConfigureTelemetryForMicrosoft365Analytics](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-configuretelemetryformicrosoft365analytics)

- **Proxy server telemetrie**: zadejte plně kvalifikovaný název domény (FQDN) nebo IP adresu proxy server, aby se předaly požadavky na uživatelské prostředí a telemetrie pomocí připojení SSL (Secure SOCKETS Layer) (SSL). Formát pro toto nastavení je *server*:*port*. Pokud pojmenovaný proxy server selhává nebo pokud při povolování této zásady nezadá proxy server, neodesílají se data o prostředích a telemetrii připojené uživatele a zůstanou na místním zařízení.

  Příklady formátů:

  ```
  IPv4: 192.246.246.106:100
  IPv6: [2001:4898:4010:4013:95c1:a8b2:953c:c633]:100
  FQDN: www.contoso.com:345
  ```

  [CSP pro System/TelemetryProxy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-telemetryproxy)

Výběrem **OK** uložte změny.

## <a name="search"></a>Search

Tato nastavení používají [CSP v zásadách hledání](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search), ve kterém jsou uvedeny také podporované edice systému Windows. 

- **Bezpečné vyhledávání (jenom mobilní)**: Určuje, jak Cortana filtruje obsah pro dospělé ve výsledcích hledání. Možnosti:
  - **Definováno uživatelem**: umožňuje koncovým uživatelům zvolit si vlastní nastavení.
  - **Strict**: nejvyšší filtrování obsahu pro dospělé.
  - **Střední**: mírné filtrování obsahu pro dospělé. Platné výsledky hledání nejsou filtrovány.
- **Zobrazit výsledky webu v hledání**: když se nastaví **blokování**, uživatelé nemůžou vyhledávat a výsledky webu nejsou zobrazené ve vyhledávání. **Nenakonfigurováno** (výchozí) umožňuje uživatelům vyhledávat na webu a výsledky se zobrazí na zařízení.

## <a name="start"></a>Spustit

Tato nastavení používají [zprostředkovatele CSP zásad spuštění](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start), který také uvádí podporované edice systému Windows.  

- **Rozložení nabídky Start**: přepište výchozí počáteční rozložení a přizpůsobení nabídky Start na desktopových zařízeních. Nahrajte soubor XML, který obsahuje vaše vlastní nastavení, včetně pořadí, ve kterém jsou aplikace uvedené, a další. Uživatelé nemůžou měnit rozložení nabídky Start, které zadáte.
- **Připnout weby na dlaždice v nabídce Start**: importovat obrázky z Microsoft Edge, které se zobrazují jako odkazy v nabídce Start systému Windows pro stolní zařízení.
- **Odepnout aplikace z panelu úloh**: **blok** znemožní uživatelům odpnutí aplikací z panelu úloh. **Nenakonfigurováno** (výchozí) umožňuje uživatelům odepnout aplikace z panelu úloh.
- **Rychlé přepínání uživatelů**: **blok** zabraňuje přepínání mezi uživateli, kteří jsou přihlášeni současně bez odhlášení. **Nenakonfigurováno** (výchozí) zobrazuje **uživatele přepínače** na dlaždici uživatele.
- **Nejčastěji používané aplikace**: **blok** skryje v nabídce Start nejčastěji používané aplikace. Zároveň se zakáže odpovídající přepínač v aplikaci Nastavení. **Nenakonfigurováno** (výchozí) zobrazuje nejčastěji používané aplikace.
- **Nedávno přidané aplikace**: **blokování** skryje nedávno přidané aplikace v nabídce Start. Zároveň se zakáže odpovídající přepínač v aplikaci Nastavení. **Nenakonfigurováno** (výchozí) zobrazuje nedávno přidané aplikace v nabídce Start.
- **Režim úvodní obrazovky**: Vyberte způsob zobrazení obrazovky Start. Možnosti:
  - **Definováno uživatelem**: nevynucuje velikost začátku. Uživatelé můžou nastavit velikost.
  - **Celá obrazovka**: vynutí celou velikost spuštění.
  - **Neúplná obrazovka**: vynutí počáteční velikost na začátku.
- **Naposledy otevřené položky v seznamech odkazů**: **blokovat** skryje v nabídce Start a na hlavním panelu nedávný seznam odkazů. Zároveň se zakáže odpovídající přepínač v aplikaci Nastavení. **Nenakonfigurováno** (výchozí) zobrazí naposledy otevřené položky v seznamy odkazů.
- **Seznam aplikací**: Vyberte způsob zobrazení seznamů všechny aplikace. Možnosti:
  - **Definováno uživatelem**: žádné nastavení není vynuceno. Uživatelé zvolí, jak se na zařízení zobrazuje seznam aplikací.
  - **Sbalit**: skryje seznam všech aplikací.
  - **Sbalení a zakázání aplikace nastavení**: skrýt seznam všech aplikací a zakázat možnost **Zobrazit seznam aplikací v nabídce Start** v aplikaci nastavení.
  - **Odebere a zakáže aplikaci nastavení**: skrýt seznam všech aplikací, odebrat všechny aplikace a zakázat možnost **Zobrazit seznam aplikací v nabídce Start** v aplikaci nastavení.
- **Tlačítko napájení**: **Block** skryje tlačítko napájení v nabídce Start. **Nenakonfigurováno** (výchozí) zobrazí tlačítko napájení.
- **Dlaždice uživatele**: **blokování** skryje dlaždici uživatele v nabídce Start. **Není nakonfigurováno** (výchozí) zobrazuje dlaždici uživatele a také nastavuje následující nastavení:
  - **Lock**: **Block** skryje možnost **zámku** v zobrazení na dlaždici uživatele v nabídce Start. **Nenakonfigurováno** (výchozí) zobrazí možnost **zámku** .
  - **Odhlásit**: **blok** skryje možnost **Odhlásit** se ze zobrazení na dlaždici uživatele v nabídce Start. **Nenakonfigurováno** (výchozí) zobrazí možnost **Odhlásit** se.
- **Vypnout**: **blokovat** skryje možnosti **aktualizace a vypnutí** a **vypnutí** v nabídce Start na tlačítku napájení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Režim spánku**: **blok** skryje možnost **spánku** v zobrazení tlačítka napájení v nabídce Start. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Hibernace**: **blok** skryje možnost **Hibernace** na tlačítku napájení v nabídce Start. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Přepínač Account**: **Block** skryje na dlaždici uživatele v nabídce Start **účet Switch** . Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Možnosti restartování**: **blokovat** skryje možnosti **aktualizace a restartování** a **restartování** z tlačítka napájení v nabídce Start. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Dokumenty na začátku**: skryje nebo zobrazí složku dokumenty v nabídce Start systému Windows. Možnosti:
  - **Nenakonfigurováno** (výchozí): není vynuceno žádné nastavení. Uživatelé mají možnost zobrazit nebo skrýt zástupce.
  - **Skrýt**: zástupce je skrytý a v aplikaci nastavení se zakáže nastavení.
  - **Zobrazit**: zástupce se zobrazí a zakáže nastavení v aplikaci nastavení.
- **Soubory ke stažení na začátku**: skryje nebo zobrazí složku stažené soubory v nabídce Start systému Windows. Možnosti:
  - **Nenakonfigurováno** (výchozí): není vynuceno žádné nastavení. Uživatelé mají možnost zobrazit nebo skrýt zástupce.
  - **Skrýt**: zástupce je skrytý a v aplikaci nastavení se zakáže nastavení.
  - **Zobrazit**: zástupce se zobrazí a zakáže nastavení v aplikaci nastavení.
- **Průzkumník souborů v nabídce Start**: skrýt nebo zobrazit Průzkumníka souborů v nabídce Start systému Windows. Možnosti:
  - **Nenakonfigurováno** (výchozí): není vynuceno žádné nastavení. Uživatelé mají možnost zobrazit nebo skrýt zástupce.
  - **Skrýt**: zástupce je skrytý a v aplikaci nastavení se zakáže nastavení.
  - **Zobrazit**: zástupce se zobrazí a zakáže nastavení v aplikaci nastavení.
- **Domácí skupina v nabídce Start**: v nabídce Start systému Windows skryjte nebo zobrazte zástupce domácí skupiny. Možnosti:
  - **Nenakonfigurováno** (výchozí): není vynuceno žádné nastavení. Uživatelé mají možnost zobrazit nebo skrýt zástupce.
  - **Skrýt**: zástupce je skrytý a v aplikaci nastavení se zakáže nastavení.
  - **Zobrazit**: zástupce se zobrazí a zakáže nastavení v aplikaci nastavení.
- **Hudba na začátku**: skryje nebo zobrazí složku hudba v nabídce Windows Start. Možnosti:
  - **Nenakonfigurováno** (výchozí): není vynuceno žádné nastavení. Uživatelé mají možnost zobrazit nebo skrýt zástupce.
  - **Skrýt**: zástupce je skrytý a v aplikaci nastavení se zakáže nastavení.
  - **Zobrazit**: zástupce se zobrazí a zakáže nastavení v aplikaci nastavení.
- **Síť v nabídce Start**: skrýt nebo zobrazit síťové vstupy nabídce Windows Start. Možnosti:
  - **Nenakonfigurováno** (výchozí): není vynuceno žádné nastavení. Uživatelé mají možnost zobrazit nebo skrýt zástupce.
  - **Skrýt**: zástupce je skrytý a v aplikaci nastavení se zakáže nastavení.
  - **Zobrazit**: zástupce se zobrazí a zakáže nastavení v aplikaci nastavení.
- **Osobní složka v nabídce Start**: skrýt nebo zobrazit osobní složku v nabídce Start systému Windows. Možnosti:
  - **Nenakonfigurováno** (výchozí): není vynuceno žádné nastavení. Uživatelé mají možnost zobrazit nebo skrýt zástupce.
  - **Skrýt**: zástupce je skrytý a v aplikaci nastavení se zakáže nastavení.
  - **Zobrazit**: zástupce se zobrazí a zakáže nastavení v aplikaci nastavení.
- **Obrázky v nabídce Start**: umožňuje skrýt nebo zobrazit složku pro obrázky v nabídce Windows Start. Možnosti:
  - **Nenakonfigurováno** (výchozí): není vynuceno žádné nastavení. Uživatelé mají možnost zobrazit nebo skrýt zástupce.
  - **Skrýt**: zástupce je skrytý a v aplikaci nastavení se zakáže nastavení.
  - **Zobrazit**: zástupce se zobrazí a zakáže nastavení v aplikaci nastavení.
- **Nastavení na začátku**: v nabídce Start systému Windows skryjte nebo zobrazte zástupce nastavení. Možnosti:
  - **Nenakonfigurováno** (výchozí): není vynuceno žádné nastavení. Uživatelé mají možnost zobrazit nebo skrýt zástupce.
  - **Skrýt**: zástupce je skrytý a v aplikaci nastavení se zakáže nastavení.
  - **Zobrazit**: zástupce se zobrazí a zakáže nastavení v aplikaci nastavení.
- **Videa na začátku**: v nabídce Start systému Windows skryjte nebo zobrazte složku pro videa. Možnosti:
  - **Nenakonfigurováno** (výchozí): není vynuceno žádné nastavení. Uživatelé mají možnost zobrazit nebo skrýt zástupce.
  - **Skrýt**: zástupce je skrytý a v aplikaci nastavení se zakáže nastavení.
  - **Zobrazit**: zástupce se zobrazí a zakáže nastavení v aplikaci nastavení.

## <a name="microsoft-defender-smart-screen"></a>Inteligentní obrazovka Microsoft Defenderu

- **Filtr SmartScreen pro Microsoft Edge**: **vyžaduje** zapnutí funkce SmartScreen v programu Microsoft Defender a zabránění uživatelům v jejich vypnutí. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zapnout filtr SmartScreen a povolit uživatelům jeho zapnutí a vypnutí.

  Microsoft Edge používá filtr SmartScreen v programu Microsoft Defender (zapnutý) k ochraně uživatelů před potenciálními podvodnými zprávami a škodlivým softwarem.

  [CSP pro Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

- **Přístup ke škodlivému webu**: **blok** zabraňuje uživatelům ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a zablokuje jejich přechodu na web. **Nenakonfigurováno** (výchozí) umožňuje uživatelům ignorovat upozornění a pokračovat v lokalitě.

  [CSP pro Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

- **Stahování neověřených souborů**: **blok** zabraňuje uživatelům ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a zablokuje stahování neověřených souborů. **Nenakonfigurováno** (výchozí) umožňuje uživatelům ignorovat upozornění a pokračovat v stahování neověřených souborů.

  [CSP pro Browser/PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)

## <a name="windows-spotlight"></a>Windows Spotlight

Tato nastavení používají [zprostředkovatele kryptografických služeb (CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience)), který obsahuje taky podporované edice Windows.

- **Windows Spotlight**: **blokování** vypne Windows Spotlight na zamykací obrazovce, tipůch pro Windows, funkcích Microsoftu pro uživatele a dalších souvisejících funkcích. Pokud je vaším cílem minimalizovat síťový provoz ze zařízení, nastavte tuto hodnotu na **blokovat**. **Nenakonfigurováno** (výchozí) povolí funkce Windows Spotlight a můžou být řízeny koncovými uživateli. Když je tato možnost povolená, můžete taky povolit nebo zablokovat následující nastavení:

  - **Windows Spotlight na zamykací obrazovce**: **blokovat** zastaví zobrazování informací na zamykací obrazovce zařízení ve Windows Spotlightu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
  - **Návrhy třetích stran ve Windows Spotlightu**: **blok** zastaví Windows Spotlight z návrhu obsahu, který nepublikoval Microsoft. **Nenakonfigurováno** (výchozí): umožňuje navrhovat návrhy aplikací a obsahu od vydavatelů partnerských softwaru ve funkcích Windows Spotlight, jako je Spotlight na zamykací obrazovce, navrhované aplikace v nabídce Start a tipy pro Windows.
  - **Uživatelské funkce**: **blokování** vypne prostředí, která jsou obvykle jenom pro příjemce, jako jsou návrhy spuštění, oznámení o členství, představová instalace aplikace po box a přesměrovat dlaždice. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
  - **Tipy pro Windows**: **blokování** zakáže automaticky otevíraná okna s tipy pro Windows. **Nenakonfigurováno** (výchozí) umožňuje zobrazit tipy pro systém Windows.
  - **Windows Spotlight v centru akcí**: **blok** zabraňuje zobrazování oznámení Windows Spotlightu v centru akcí. **Nenakonfigurováno** (výchozí) může zobrazovat oznámení v centru akcí, které navrhuje aplikace nebo funkce, které uživatelům pomůžou zvýšit produktivitu Windows.
  - **Přizpůsobení Windows Spotlightu**: **blok** zabraňuje systému Windows používat diagnostická data k poskytování přizpůsobených prostředí uživateli. **Nenakonfigurováno** (výchozí) umožňuje Microsoftu používat diagnostická data k poskytování individuálních doporučení, tipů a nabídek k přizpůsobení Windows potřebám uživatelů.
  - **Prostředí uvítání systémem Windows**: **blok** vypne funkci Windows Spotlight Windows Welcome Experience. Prostředí uvítání systémem Windows se nezobrazí, pokud jsou k dispozici aktualizace a změny ve Windows a jejích aplikacích. **Nenakonfigurováno** (výchozí) umožňuje uvítání systémem Windows, které zobrazuje informace o uživateli nových nebo aktualizovaných funkcích.

## <a name="microsoft-defender-antivirus"></a>Antivirová ochrana v programu Microsoft Defender

Tato nastavení používají [zprostředkovatele CSP v zásadách Defenderu](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender), který obsahuje také podporované edice Windows.

- **Sledování v reálném čase**: **Povolení** zapne kontrolu v reálném čase pro malware, spyware a další nežádoucí software. Uživatelé ji nemůžou vypnout. 

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune ponechá nastavení v dřív nakonfigurovaném stavu. Ve výchozím nastavení operační systém tuto funkci zapne a umožňuje uživatelům ji změnit.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/AllowRealtimeMonitoring CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

- **Monitorování chování**: **Povolit** zapne monitorování chování a kontroluje určité známé vzorce podezřelé aktivity na zařízeních. Uživatelé nemůžou monitorování chování vypnout. 

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune ponechá nastavení v dřív nakonfigurovaném stavu. Ve výchozím nastavení operační systém zapne monitorování chování a umožňuje uživatelům ho změnit.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/AllowBehaviorMonitoring CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

- **Systém kontroly sítě (NIS)**: NIS pomáhá chránit zařízení před zneužitím prostřednictvím sítě. Používá signatury známých slabých míst z Centra Microsoftu pro ochranu koncových bodů ke zjištění a blokování škodlivého síťového provozu.

  **Povolit zapne možnost** zapnout ochranu sítě a síťové blokování. Uživatelé ji nemůžou vypnout. Pokud je tato možnost povolená, uživatelé se budou moct připojit ke známým chybám zabezpečení.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune ponechá nastavení v dřív nakonfigurovaném stavu. Ve výchozím nastavení operační systém zapne službu NIS a umožňuje uživatelům ji změnit.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/EnableNetworkProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

- **Prohledat všechny soubory ke stažení**: **Povolit** zapne toto nastavení a Defender zkontroluje všechny soubory stažené z Internetu. Uživatelé toto nastavení nemůžou vypnout. 

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune ponechá nastavení v dřív nakonfigurovaném stavu. Ve výchozím nastavení operační systém toto nastavení zapne a umožňuje uživatelům ho změnit.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/AllowIOAVProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowioavprotection)

- **Kontrolovat skripty načtené do webových prohlížečů Microsoftu**: **Povolit** umožňuje programu Defender kontrolovat skripty, které se používají v Internet Exploreru. Uživatelé toto nastavení nemůžou vypnout. 

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune ponechá nastavení v dřív nakonfigurovaném stavu. Ve výchozím nastavení operační systém toto nastavení zapne a umožňuje uživatelům ho změnit.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/AllowScriptScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning)

- **Přístup koncového uživatele k programu Defender**: **blok** skryje uživatelské rozhraní programu Microsoft Defender před koncovými uživateli. Potlačí se také všechna oznámení programu Microsoft Defender.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Pokud nastavení zablokujete a pak ho změníte zpátky na **není nakonfigurované**, Intune ponechá nastavení v dříve nakonfigurovaném stavu. Ve výchozím nastavení operační systém umožňuje uživateli přístup k uživatelskému rozhraní programu Microsoft Defender a umožňuje uživatelům ho změnit.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  Když toto nastavení změníte, projeví se změna až při příštím restartování počítače koncovým uživatelem.

  [Defender/AllowUserUIAccess CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess)

- **Interval aktualizace Security Intelligence (v hodinách)**: zadejte interval, který Defender kontroluje pro nové Security Intelligence, od 0-24. Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Výchozí operační systém může kontrolovat aktualizace každých 8 hodin.
  - **Nekontrolovat**: Defender nehledá nové aktualizace Security Intelligence.
  - **1-24**: `1` kontroluje každou hodinu, `2` kontroluje každé dvě hodiny, `24` kontroluje každý den atd.
  
  [Defender/SignatureUpdateInterval CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdateinterval)
  
- **Monitorovat aktivitu souborů a programů**: umožňuje programu Defender monitorovat aktivitu souborů a programů na zařízeních. Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Výchozí hodnota operačního systému může monitorovat všechny soubory.
  - **Monitorování zakázáno**
  - **Monitorovat všechny soubory**
  - **Monitorovat pouze příchozí soubory**
  - **Monitorovat jenom odchozí soubory**

  [Defender/RealTimeScanDirection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-realtimescandirection)

- **Dny před odstraněním malwaru v karanténě**: pokračovat v sledování vyřešeného malwaru po dobu, po kterou zadáte, abyste mohli ručně kontrolovat dříve zasažená zařízení. Pokud nastavíte počet dní na `0`, malware zůstane ve složce karanténa a automaticky se neodebere. Pokud je nastaveno `90`na, karanténní položky jsou uloženy po dobu 90 dnů v systému a poté odebrány.

  [Defender/DaysToRetainCleanedMalware CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware)

- **Limit využití procesoru při kontrole**: Omezte množství procesorů, které mohou kontroly využít, od `0` do. `100`
- **Kontrolovat archivní soubory**: **Povolit** zapne Defender, aby kontroloval archivní soubory, jako jsou soubory ZIP nebo CAB. Uživatelé toto nastavení nemůžou vypnout.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune ponechá nastavení v dřív nakonfigurovaném stavu. Ve výchozím nastavení operační systém toto skenování zapne a umožňuje uživatelům ho změnit.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/AllowArchiveScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)

- **Kontrolovat příchozí e-mailové zprávy**: **Povolit** umožňuje programu Defender kontrolovat e-mailové zprávy při jejich doručování do zařízení. Pokud je tento modul povolený, analyzuje poštovní schránku a e-mailové soubory a analyzuje body pošty a přílohy. Můžete kontrolovat formáty. PST (Outlook),. dbx,. mbx, MIME (Outlook Express) a BinHex (Mac).

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune ponechá nastavení v dřív nakonfigurovaném stavu. Ve výchozím nastavení operační systém vypne tuto kontrolu a umožní uživatelům ji změnit.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/AllowEmailScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

- **Kontrolovat vyměnitelné jednotky během úplného prohledávání**: **Povolit zapne možnost** při úplné kontrole zapnout kontrolu vyměnitelných jednotek v Defenderu. Uživatelé toto nastavení nemůžou vypnout.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune ponechá nastavení v dřív nakonfigurovaném stavu. Ve výchozím nastavení operační systém umožňuje programu Defender kontrolovat vyměnitelné jednotky, jako jsou USB hole, a umožňuje uživatelům změnit toto nastavení.

  Během rychlé kontroly mohou být vyměnitelné jednotky stále prohledávány.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/AllowFullScanRemovableDriveScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)

- **Kontrolovat namapované síťové jednotky během úplného prohledávání**: **Povolit** programu Defender prohledává soubory na namapovaných síťových jednotkách. Pokud jsou soubory na disku jen pro čtení, Defender nemůže odebrat žádný malware, který v nich našel. Uživatelé toto nastavení nemůžou vypnout.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune ponechá nastavení v dřív nakonfigurovaném stavu. Ve výchozím nastavení operační systém tuto funkci zapne a umožňuje uživatelům ji změnit.

  Během rychlé kontroly mohou být namapované síťové jednotky stále prohledávány.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/AllowFullScanOnMappedNetworkDrives CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives)

- **Kontrolovat soubory otevřené ze síťových složek**: **možnost Povolit** v programu Defender prohledává soubory otevřené ze síťových složek nebo sdílených síťových jednotek, jako jsou například soubory dostupné z cesty UNC. Uživatelé toto nastavení nemůžou vypnout. Pokud jsou soubory na disku jen pro čtení, Defender nemůže odebrat žádný malware, který v nich našel.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune ponechá nastavení v dřív nakonfigurovaném stavu. Ve výchozím nastavení operační systém kontroluje soubory otevřené ze síťových složek a umožňuje uživatelům jejich změnu.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/AllowScanningNetworkFiles CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

- **Ochrana cloudu**: **Povolit** zapne služba Microsoft Active Protection Service pro příjem informací o činnosti malwaru ze zařízení, která spravujete. Uživatelé toto nastavení nemůžou změnit. 

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Pokud toto nastavení povolíte a pak ho změníte zpátky na **není nakonfigurované**, Intune ponechá nastavení v dřív nakonfigurovaném stavu. Ve výchozím nastavení operační systém umožňuje služba Microsoft Active Protection Service přijímat informace a umožňuje uživatelům změnit toto nastavení.

  Intune tuto funkci nevypne. Pokud ho chcete zakázat, použijte vlastní identifikátor URI.

  [Defender/AllowCloudProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

- **Dotázat se uživatele před odesláním vzorku**: Určuje, jestli se mají do Microsoftu automaticky posílat potenciálně škodlivé soubory, které by mohly vyžadovat další analýzu. Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje. Výchozí nastavení operačního systému může automaticky odesílat bezpečné vzorky.
  - **Vždycky se zeptat**
  - **Dotázat se před odesláním osobních údajů**
  - **Nikdy Neodesílat data**
  - **Odesílat všechna data bez zobrazení výzvy**: data se odesílají automaticky.

  [Defender/SubmitSamplesConsent CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)

- **Čas, kdy se má provést rychlá denní kontrola**: vyberte hodinu spuštění každodenní rychlé kontroly. **Není nakonfigurováno** spustí denní kontrolu. Pokud chcete více úprav, nakonfigurujte **typ kontroly systému na provádění** .

  [Defender/ScheduleQuickScanTime CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime)

- **Typ Systémové kontroly, který se má provést**: naplánovat kontrolu systému, včetně úrovně kontroly a dne a času, kdy se má kontrola spustit. Možnosti:
  - **Nenakonfigurováno**: neplánuje kontrolu systému na zařízení. Koncoví uživatelé můžou na svých zařízeních ručně spouštět kontroly podle potřeby nebo na jejich zařízení.
  - **Zakázat**: zakáže v zařízení kontrolu systémových souborů. Tuto možnost vyberte, pokud používáte řešení antivirové ochrany, které provádí kontrolu zařízení.
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

- **Detekce potenciálně nežádoucích aplikací**: vyberte úroveň ochrany, když systém Windows detekuje potenciálně nežádoucí aplikace. Možnosti:
  - **Nenakonfigurováno** (výchozí): Ochrana před potenciálně nežádoucími aplikacemi v programu Microsoft Defender je zakázaná.
  - **Blok**: Microsoft Defender detekuje potenciálně nežádoucí aplikace a zjištěné položky jsou blokované. Tyto položky se zobrazují v historii spolu s dalšími hrozbami.
  - **Audit**: Microsoft Defender detekuje potenciálně nežádoucí aplikace, ale neprovede žádnou akci. Můžete zkontrolovat informace o aplikacích, které Microsoft Defender provede, na základě těchto akcí. Vyhledejte například události vytvořené v programu Microsoft Defender v Prohlížeč událostí.

  Další informace o potenciálně nežádoucích aplikacích najdete v tématu [zjištění a blokování potenciálně nežádoucích aplikací](https://docs.microsoft.com/windows/threat-protection/windows-defender-antivirus/detect-block-potentially-unwanted-apps-windows-defender-antivirus).

  [Defender/PUAProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

- **Vyjádření souhlasu s ukázkami**: v současné době toto nastavení nemá žádný vliv. Toto nastavení nepoužívejte. Může být odebráno v budoucí verzi.

- **Při přístupu k ochraně**: **blok** zabraňuje kontrole souborů, ke kterým byl přístup nebo stažen. Uživatelé ji nemůžou zapnout.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Pokud nastavení zablokujete a pak ho změníte zpátky na **není nakonfigurované**, Intune nastavení ponechá v předchozím stavu konfigurovaném pro operační systém. Ve výchozím nastavení operační systém tuto funkci povoluje a umožňuje uživatelům ji změnit.

  Intune tuto funkci nezapíná. Pokud ho chcete povolit, použijte vlastní identifikátor URI.

  [Defender/AllowOnAccessProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

- **Akce zjištěných malwarových hrozeb**: vyberte, jak chcete zpracovat vlákna malwaru. **Nenakonfigurováno** (výchozí) umožňuje programu Microsoft Defender zvolit nejlepší možnost. Pokud je nastavena možnost **Povolit**, vyberte akce, které má Defender provést pro každou úroveň hrozby, kterou zjistí: nízká, střední, vysoká a závažná. Možnosti:
  
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

- **Soubory a složky, které se mají vyloučit z kontrol a ochrany v reálném**čase: přidá do seznamu vyloučení jeden nebo víc souborů a složek, jako je **c:\Cesta** nebo **%ProgramFiles%\cesta\soubor.exe** . Tyto soubory a složky nejsou zahrnuté do kontrol probíhajících v reálném čase ani do plánovaných kontrol.
- **Přípony souborů, které se mají vyloučit z kontrol a ochrany v reálném čase**: do seznamu vyloučení přidejte jednu nebo víc přípon souborů, jako je **jpg** nebo **txt** . Všechny soubory s těmito příponami nejsou zahrnuté do kontrol probíhajících v reálném čase ani do plánovaných kontrol.
- **Procesy, které se mají vyloučit z kontrol a ochrany v reálném**čase: přidejte jeden nebo více procesů typu **. exe**, **. com**nebo **. scr** do seznamu vyloučení. Tyto procesy nejsou zahrnuté do kontrol prováděných v reálném čase ani do plánovaných kontrol.

## <a name="power-settings"></a>Nastavení napájení

### <a name="battery"></a>Baterie

- **Úroveň baterie**: Pokud zařízení používá napájení z baterie, zadejte úroveň nabití baterie, abyste zapnuli úsporu energie z 0-100. Zadejte procentuální hodnotu, která označuje úroveň nabití baterie. Výchozí hodnota je 70%. Když je nastavená na 70%, úspora energie se zapne, když má baterie za 70% nebo méně dostupného.

  [CSP pro Power/EnergySaverBatteryThresholdOnBattery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdonbattery)

- **Zavření víka (jenom mobilní)**: Pokud zařízení používá napájení z baterie, vyberte, co se stane po zavření víka. Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Žádná akce**: zařízení zůstává zapnuté a nadále používá napájení z baterie.
  - **Režim spánku**: zařízení přejde do režimu spánku a použije malé množství poplatků za baterii. Počítač je stále zapnutý a otevřené aplikace a soubory jsou uložené v paměti RAM (Random Access Memory).
  - **Hibernace**: zařízení přejde do režimu hibernace. Otevřené aplikace a soubory se ukládají na pevný disk a zařízení se vypne.
  - **Vypnutí**: zařízení se vypíná. Otevřené aplikace a soubory se zavřou bez uložení.

  [CSP pro Power/SelectLidCloseActionOnBattery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactiononbattery)

- **Tlačítko napájení**: Pokud zařízení používá napájení z baterie, vyberte, co se stane po výběru tlačítka napájení. Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Žádná akce**: zařízení zůstává zapnuté a nadále používá napájení z baterie.
  - **Režim spánku**: zařízení přejde do režimu spánku a použije malé množství poplatků za baterii. Počítač je stále zapnutý a otevřené aplikace a soubory jsou uložené v paměti RAM (Random Access Memory).
  - **Hibernace**: zařízení přejde do režimu hibernace. Otevřené aplikace a soubory se ukládají na pevný disk a zařízení se vypne.
  - **Vypnutí**: zařízení se vypíná. Otevřené aplikace a soubory se zavřou bez uložení.

  [CSP pro Power/SelectPowerButtonActionOnBattery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactiononbattery)

- **Tlačítko režimu spánku**: když zařízení používá napájení z baterie, vyberte, co se stane po výběru tlačítka režimu spánku. Možnosti:

  - **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
  - **Žádná akce**: zařízení zůstává zapnuté a nadále používá napájení z baterie.
  - **Režim spánku**: zařízení přejde do režimu spánku a použije malé množství poplatků za baterii. Počítač je stále zapnutý a otevřené aplikace a soubory jsou uložené v paměti RAM (Random Access Memory).
  - **Hibernace**: zařízení přejde do režimu hibernace. Otevřené aplikace a soubory se ukládají na pevný disk a zařízení se vypne.
  - **Vypnutí**: zařízení se vypíná. Otevřené aplikace a soubory se zavřou bez uložení.

  [CSP pro Power/SelectSleepButtonActionOnBattery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactiononbattery)

- **Hybridní režim spánku**: když zařízení používá napájení z baterie, **zakažte zakázat** zabrání zařízení v přechodu do hybridního režimu spánku. V hybridním režimu spánku se otevřené aplikace a soubory ukládají do paměti RAM a na pevném disku. Používá malé množství poplatků za napájení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  [CSP pro Power/TurnOffHybridSleepOnBattery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeponbattery)

### <a name="pluggedin"></a>PluggedIn

- **Úroveň baterie**: Pokud je zařízení napájené z energie, zadejte úroveň nabití baterie, abyste zapnuli úsporu energie z 0-100. Zadejte procentuální hodnotu, která označuje úroveň nabití baterie. Výchozí hodnota je 70%. Když je nastavená na 70%, úspora energie se zapne, když má baterie za 70% nebo méně dostupného.

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

- **Hybridní režim spánku**: když je zařízení napájené ze sítě, **zakažte** zabránit v přechodu do hybridního režimu spánku. V hybridním režimu spánku se otevřené aplikace a soubory ukládají do paměti RAM a na pevném disku. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  [CSP pro Power/TurnOffHybridSleepPluggedIn](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeppluggedin)

## <a name="next-steps"></a>Další kroky

Další technické podrobnosti o jednotlivých nastaveních a podporovaných edicích Windows najdete v [referenčních informacích o poskytovateli konfiguračních služeb pro zásady (CSP) pro Windows 10](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider).
