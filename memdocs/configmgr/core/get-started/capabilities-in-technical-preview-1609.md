---
title: Možnosti ve verzi Technical Preview 1609
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview pro Configuration Manager verze 1609.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e2a59116-b2e5-4dd2-90eb-0b8a5eb50b56
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 05ed0daf56275b2e0ed46b2f9dd93fd66eb360be
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995530"
---
# <a name="capabilities-in-technical-preview-1609-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1609 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*



V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1609. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview.      Před instalací této verze Technical Preview si Projděte úvodní téma, [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md), abyste se seznámili se základními požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.    

**Známé problémy v této verzi Technical Preview:**  
*  Když aktualizujete Configuration Manager 1609 Technical Preview, odstraní se všechny zásady upgradu edice, které jste nasadili. Pokud chcete tyto zásady dál používat, musíte je znovu vytvořit a nasadit.


**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  

## <a name="improvements-to-endpoint-protection"></a>Vylepšení Endpoint Protection
Vylepšení Endpoint Protection nastavení antimalwarových zásad – můžete teď zadat úroveň, na které bude služba Endpoint Protection Cloud Protection blokovat podezřelé soubory. Nové nastavení umožňuje správcům určit "rizikové" počítače na základě vysokého množství malwaru, ke kterému narazí.

## <a name="increased-number-of-enrolled-devices"></a>Zvýšený počet zaregistrovaných zařízení
Správci teď můžou uživatelům povolit registraci až 15 zařízení v hybridní správě mobilních zařízení pomocí Intune. V minulosti byl limit 5 zařízení na uživatele.

## <a name="additional-apple-dep-settings"></a>Další nastavení Apple DEP

Správci teď můžou nakonfigurovat následující nastavení Apple Program registrace zařízení (DEP) v profilu DEP pro zařízení s iOS a Mac:
- **Touch ID**
- **Zoom**
- **Siri**

Pokud je tato možnost povolená, Pomocník s nastavením společnosti Apple při aktivaci zařízení zobrazí výzvu k zadání této služby.

## <a name="integration-with-upgrade-analytics"></a>Integrace s Upgrade Analytics

Upgrade Analytics umožňuje vyhodnocovat a analyzovat připravenost a kompatibilitu zařízení s Windows 10, aby bylo možné snadněji a plynulejší upgrady. Díky integraci Upgrade Analytics s Configuration Manager máte přístup k datům o kompatibilitě upgradu v konzole pro správu Configuration Manager a potom v seznamu zařízení, která jsou určená pro upgrade nebo nápravu.


## <a name="native-connection-types-for-windows-10-vpn-hybrid-profiles"></a>Nativní typy připojení pro hybridní profily sítě VPN s Windows 10

Při použití Configuration Manager s Intune teď můžete vytvářet profily sítě VPN pro Windows 10 s typy připojení Microsoft Automatic, IKEv2, PPTP a L2TP v konzole Configuration Manager bez použití OMA-URI.

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Vylepšení integrace Windows Storu pro firmy s Configuration Manager

V této verzi jsme aktualizovali [integraci Windows Storu pro firmy](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) s těmito novými funkcemi:

**Aktualizace:** V aktuálním vydání Technical Preview není funkce okamžité synchronizace funkční.

- Dřív jste mohli nasadit jenom bezplatné aplikace z Windows Storu pro firmy. Configuration Manager teď podporuje i nasazení placených online licencovaných aplikací (jenom pro zařízení zaregistrovaná v Intune).
- Nyní můžete zahájit okamžitou synchronizaci mezi Windows Storem pro firmy a Configuration Manager.
- Nyní můžete změnit tajný klíč klienta, který jste získali z Azure Active Directory

### <a name="try-it-out"></a>Určitě to udělejte!

#### <a name="purchase-and-sync-a-paid-online-licensed-app"></a>Zakoupení a synchronizace placené online licencované aplikace

1. Zakupte si placené online licencované aplikace z Windows Storu pro firmy.
2. V pracovním prostoru **Správa** konzoly Configuration Manager klikněte na **Cloud Services**  >  **aktualizace a obsluha**  >  **Windows Storu pro firmy**.
3. Na kartě **Domů** ve skupině **synchronizace** klikněte na **synchronizovat nyní**.
4. Později se aplikace, kterou jste zakoupili, zobrazí v uzlu **licenční informace pro aplikace pro Store** v pracovním prostoru **Správa aplikací** .

#### <a name="create-and-deploy-a-configuration-manager-application-from-the-synchronized-app-data"></a>Vytvoření a nasazení aplikace Configuration Manager z synchronizovaných dat aplikace

Postup vytvoření a nasazení Configuration Manager aplikace z aplikace placeného úložiště je stejný jako při vytváření aplikace z bezplatné aplikace. Přečtěte si část **Vytvoření a nasazení Configuration Manager aplikace z aplikace Windows Store pro firmy** v tématu [Správa aplikací z Windows Storu pro firmy pomocí Configuration Manager](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).


#### <a name="modify-the-client-secret-key-from-azure-active-directory"></a>Úprava tajného klíče klienta z Azure Active Directory

1. V pracovním prostoru **Správa** konzoly Configuration Manager klikněte na **Cloud Services**  >  **aktualizace a obsluha**  >  **Windows Storu pro firmy**.
2. Vyberte účet ve Windows Storu pro firmy a pak klikněte na **vlastnosti**.
3. V dialogovém okně **vlastnosti účtu ve Windows Storu pro firmy** zadejte nový klíč do pole **tajný klíč klienta** a potom klikněte na **ověřit**. Po ověření klikněte na **použít**a potom dialogové okno zavřete.


## <a name="new-compliance-settings-for-configuration-items"></a>Nové nastavení dodržování předpisů pro položky konfigurace

Přidali jsme spoustu nových nastavení, která můžete použít v položkách konfigurace pro různé platformy zařízení.
Jedná se o nastavení, která dříve existovala v Microsoft Intune samostatné konfigurace, a jsou teď dostupná, když používáte Intune s Configuration Manager.
Pokud potřebujete s některým z těchto nastavení nápovědu, otevřete [Spravovat nastavení a funkce v zařízeních pomocí zásad Microsoft Intune](../../../intune/configuration/device-profiles.md) a pak vyberte dílčí téma nastavení pro požadovanou platformu.


### <a name="new-settings-for-android-devices"></a>Nová nastavení pro zařízení s Androidem

#### <a name="password-settings"></a>Nastavení hesla

- **Pamatovat si historii hesel**
- **Povolit odemknutí otiskem prstu**

#### <a name="security-settings"></a>Nastavení zabezpečení

- **Vyžadovat šifrování u paměťových karet**
- **Povolit snímek obrazovky**
- **Povolit odeslání diagnostických dat**

#### <a name="browser-settings"></a>Nastavení prohlížeče

- **Povolit webový prohlížeč**
- **Povolit automatické vyplňování**
- **Povolit blokování automaticky otevíraných oken**
- **Povolení souborů cookie**
- **Povolit aktivní skriptování**

#### <a name="app-settings"></a>Nastavení aplikace

- **Povolit Google Play Store**

#### <a name="device-capability-settings"></a>Nastavení možností zařízení

- **Povolit vyměnitelné úložiště**
- **Povolit Wi-Fi tethering**
- **Povolit zeměpisnou polohu**
- **Povolit komunikaci NFC**
- **Povolit Bluetooth**
- **Povolit hlasový roaming**
- **Povolit datový roaming**
- **Povolit SMS a MMS zprávy**
- **Povolit hlasového pomocníka**
- **Povolit hlasové vytáčení**
- **Povolit kopírování a vkládání**


### <a name="new-settings-for-ios-devices"></a>Nová nastavení pro zařízení s iOS

#### <a name="password-settings"></a>Nastavení hesla

- **Počet složitých znaků požadovaných v hesle**
- **Povolit jednoduchá hesla**
- **Počet minut nečinnosti před vyžadováním hesla**
- **Pamatovat si historii hesel**

### <a name="new-settings-for-mac-os-x-devices"></a>Nová nastavení pro Mac OS X zařízení

#### <a name="password-settings"></a>Nastavení hesla

- **Počet složitých znaků požadovaných v hesle**
- **Povolit jednoduchá hesla**
- **Pamatovat si historii hesel**
- **Počet minut nečinnosti před aktivací šetřiče obrazovky**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Nová nastavení pro zařízení s Windows 10 Desktop a Mobile

#### <a name="password-settings"></a>Nastavení hesla

- **Minimální počet znakových sad**
- **Pamatovat si historii hesel**
- **Po návratu zařízení ze stavu nečinnosti vyžadovat heslo**

#### <a name="security-settings"></a>Nastavení zabezpečení

- **Vyžadovat šifrování u mobilního zařízení**
- **Povolit manuální zrušení zápisu**

#### <a name="device-capability-settings"></a>Nastavení možností zařízení

- **Povolit VPN v mobilní síti**
- **Povolit VPN v mobilní síti v roamingu**
- **Povolit obnovení továrního nastavení telefonu**
- **Povolit připojení USB**
- **Povolit Cortanu**
- **Povolit oznámení centra akcí**

### <a name="new-settings-for-windows-10-team-devices"></a>Nová nastavení pro zařízení s Windows 10 Team

#### <a name="device-settings"></a>Nastavení zařízení

- **Povolit Azure Operational Insights**
- **Povolit bezdrátové připojení Miracast**
- **Zvolit informace o schůzce zobrazené na úvodní obrazovce**
- **Adresa URL obrázku pozadí zamykací obrazovky**


### <a name="new-settings-for-windows-81-devices"></a>Nová nastavení pro Windows 8.1 zařízení

#### <a name="applicability-settings"></a>Nastavení použitelnosti

- **Použít všechny konfigurace ve Windows 10**

#### <a name="password-settings"></a>Nastavení hesla

- **Vyžadovaný typ hesla**
- **Minimální počet znakových sad**
- **Minimální délka hesla**
- **Počet povolených opakovaných neúspěšných přihlášení, než bude zařízení vymazáno**
- **Počet minut nečinnosti před vypnutím displeje**
- **Vypršení platnosti hesla (dny)**
- **Pamatovat si historii hesel**
- **Znemožnit opakované použití předchozích hesel**
- **Povolit obrázkové heslo a PIN**

#### <a name="browser-settings"></a>Nastavení prohlížeče

- **Povolit automatické zjišťování intranetové sítě**


### <a name="new-settings-for-windows-phone-81-devices"></a>Nová nastavení pro zařízení Windows Phone 8,1

#### <a name="applicability-settings"></a>Nastavení použitelnosti

- **Použít všechny konfigurace ve Windows 10**

#### <a name="password-settings"></a>Nastavení hesla

- **Minimální počet znakových sad**
- **Povolit jednoduchá hesla**
- **Pamatovat si historii hesel**

#### <a name="device-capability-settings"></a>Nastavení možností zařízení

- **Povolit automatické připojení k bezplatným Wi-Fi hotspotům**


## <a name="improvements-for-boundary-groups"></a>Vylepšení pro skupiny hranic
Tato verze Preview přináší důležité změny skupin hranic a jejich fungování s distribučními body. Tyto změny vám pomůžou zjednodušit návrh infrastruktury obsahu a zároveň vám poskytne lepší kontrolu nad tím, jak a kdy klienti mají v případě, že budou prohledávat další distribuční body, jako umístění zdrojových obsahu. To zahrnuje místní i cloudové distribuční body.

Tato vylepšení nahrazují koncepty a chování, které můžete znát v dnešní době (třeba konfigurace distribučních bodů tak, aby byly rychlé nebo pomalé), a nahradí je novým modelem, který by se měl snadněji nastavit a udržovat. Tyto změny jsou také základy pro budoucí změny, které zlepšují jiné role systému lokality, které přiřadíte ke skupinám hranic.  

Během upgradu na 1609 převede upgrade aktuální konfigurace skupiny hranic tak, aby odpovídaly novému modelu, aby tyto změny nenarušily vaše konfigurace distribuce obsahu (viz [aktualizace existujících skupin hranic na nový model](capabilities-in-technical-preview-1609.md#bkmk_update)).

Následující části obsahují podrobnosti o změnách zavedených v této verzi Preview, o tom, jak nový model funguje a co můžete očekávat při upgradu lokality, která již má nakonfigurované skupiny hranic.



### <a name="changes-in-ui-and-behavior-for-boundary-groups-and-content-locations"></a>Změny v uživatelském rozhraní a chování pro skupiny hranic a umístění obsahu
Níže jsou uvedené klíčové změny skupin hranic a způsob, jakým klienti hledají obsah. Mnohé z těchto změn a konceptů společně fungují.
- **Odeberou se konfigurace pro rychlá nebo pomalá:** Už nemusíte konfigurovat jednotlivé distribuční body, aby byly rychlé nebo pomalé.  Místo toho je pro každý systém lokality, který je přidružený ke skupině hranic, zacházeno stejným způsobem. Z důvodu této změny nepodporuje karta **odkazy** v rámci vlastností hraniční skupiny, aby konfigurace byla rychlá nebo pomalá.
- **Nová výchozí skupina hranic v každé lokalitě:**  Každá primární lokalita má novou výchozí skupinu hranic s názvem ***Default-site-hraniční- \<sitecode> Group***.  Pokud klient není v síťovém umístění, které je přiřazeno ke skupině hranic, bude tento klient používat systémy lokality přidružené k výchozí skupině ze své přiřazené lokality. Naplánujte použití této skupiny hranic jako náhrady za koncept záložního umístění obsahu.    
  -  **' Odebrání záložních umístění zdroje pro obsah '** se odeberou: nemusíte explicitně konfigurovat distribuční bod, který se má použít pro použití jako záložní, a možnosti pro nastavení této volby se odeberou z uživatelského rozhraní.

  Kromě toho je výsledkem nastavení **umožnění klientům použít náhradní umístění zdroje obsahu** v typu nasazení pro aplikace. Toto nastavení pro typ nasazení teď umožňuje klientovi použít výchozí skupinu hranic lokality jako umístění zdroje obsahu.

  -  **Vztahy skupin hranic:** Každá skupina hranic může být propojená s jednou nebo více dalšími skupinami hranic. Tyto odkazy tvoří vztahy, které jsou konfigurovány na kartě vlastností nové skupiny hranic s názvem **relace**:
  -   Každá skupina hranic, se kterou je klient přímo přidružený, se nazývá **aktuální** skupina hranic.  
  -   Každá skupina hranic, kterou může klient použít kvůli přidružení mezi *aktuální* skupinou hranic daného klienta a jinou skupinou se nazývá **sousední** skupina hranic.
  -  Je na kartě **relace** , kterou přidáte skupiny hranic, které lze použít jako *sousední* skupinu hranic. Můžete taky nakonfigurovat čas v minutách, který určuje, kdy se klient, který nedokáže najít obsah z distribučního bodu v *aktuální* skupině, začne prohledávat umístění obsahu z těchto *sousedních* skupin hranic.

      Když přidáváte nebo měníte konfiguraci skupiny hranic, budete mít možnost zablokovat pro tuto konkrétní skupinu hranic zálohu z aktuální skupiny, kterou konfigurujete.

  Chcete-li použít novou konfiguraci, definujete explicitní přidružení (odkazy) z jedné skupiny hranic na jinou a nakonfigurujete všechny distribuční body v této přidružené skupině se stejnou dobu v minutách. Čas, který nakonfigurujete, určuje, kdy klient, který nenalezne zdroj obsahu ze své *aktuální* skupiny hranic, může začít hledat zdroje obsahu z této sousední hraniční skupiny.

  Kromě skupin hranic, které výslovně nakonfigurujete, má každá skupina hranic implicitní odkaz na výchozí skupinu hranic lokality. Tento odkaz bude aktivní po 120 minutách, kdy se výchozí skupina hranic lokality stal sousední skupinou hranic, která umožňuje klientům používat distribuční body přidružené k této skupině hranic jako umístění zdroje obsahu.

  Toto chování nahrazuje, co bylo dříve označováno jako nouzové pro obsah.  Toto výchozí chování můžete přepsat 120 minut tím, že explicitně přidružíte výchozí skupinu hranic lokality k *aktuální* skupině a nastavíte určitou dobu v minutách, nebo zablokujete zálohu úplně, aby nedošlo k jejich použití.


- **Klienti se pokusí získat obsah z každého distribučního bodu po dobu až 2 minut:** Když klient hledá umístění zdroje obsahu, pokusí se o přístup ke každému distribučnímu bodu 2 minuty, než se pokusí o další distribuční bod. Jedná se o změnu z předchozích verzí, kde se klienti pokusili připojit k distribučnímu bodu po dobu až 2 hodin.

  - První distribuční bod, který se klient pokusí použít, se náhodně vybere z fondu dostupných distribučních bodů v *aktuální* skupině hranic (nebo skupinách) daného klienta.

  - Pokud klient nenalezne obsah, bude po dvou minutách přepnut do nového distribučního bodu a pokusí se získat obsah z tohoto serveru. Tento proces opakuje každé dvě minuty, dokud klient nenajde obsah nebo nedosáhne posledního serveru v jeho fondu.

  - Pokud klient nemůže najít platné umístění zdroje obsahu ze svého *aktuálního* fondu před dosažením doby přechodu do *sousední* skupiny hranic, klient pak přidá distribuční body z této *sousední* skupiny na konec aktuálního seznamu a pak vyhledá rozbalenou skupinu zdrojových umístění, která zahrnují distribuční body ze skupin hranic obou.

      > [!TIP]  
      > Když vytvoříte explicitní propojení z aktuální skupiny hranic na výchozí skupinu hranic lokality a nadefinujete záložní čas, který je kratší než záložní čas pro odkaz na sousední skupinu hranic, začnou klienti prohledávat umístění zdroje z výchozí skupiny hranic lokality před zahrnutím sousední skupiny.

  - Když se klientovi nepovede získat obsah z posledního serveru ve fondu, zahájí proces znovu.


### <a name="how-the-new-model-works"></a>Jak nový model funguje
Při konfiguraci skupin hranic přidružíte hranice (síťová umístění) a role systému lokality, jako jsou distribuční body, ke skupině hranic. To pomáhá propojit klienty se servery systému lokality, jako jsou distribuční body, které se nacházejí poblíž klientů v síti.   
- Stejnou hranici můžete přiřadit více skupinám hranic.
- Systémové servery lokality, jako jsou distribuční body, se dají přidružit k několika skupinám hranic, takže jsou dostupné v širším rozsahu síťových umístění.
- Pokud distribuční bod není přidružen ke skupině hranic, klienti nebudou moci použít tento distribuční bod jako umístění zdroje obsahu.

Od této verze Technical Preview definujete vztahy hraničních skupin pro konfiguraci nouzového chování pro umístění zdrojů obsahu. Toto nové chování je nakonfigurované na kartě nové **relace** ve vlastnostech skupiny hranic a nahrazuje konfiguraci systémů lokality jako pomalé nebo rychlé a konfiguraci skupiny hranic tak, aby umožňovala záložní umístění zdroje pro obsah.

Na kartě relace přidejte další skupiny hranic pro konfiguraci vztahu k těmto skupinám. Každá relace představuje jednosměrný odkaz z **aktuální** skupiny hranic do skupiny hranic, kterou přidáte, což se označuje jako **sousední**. U každého odkazu, který vytvoříte, můžete nakonfigurovat distribuční body s využitím záložního času v řádu minut. Tato doba se používá k určení, jak dlouho můžou klienti v *aktuální* skupině hranic začít používat distribuční body v *sousední* skupině hranic, pokud nemůžou najít platné umístění zdroje obsahu z aktuální skupiny hranic.

Když klient nemůže najít obsah a začne hledat v umístěních ze sousedních hraničních skupin, zvyšuje se tím fond dostupných distribučních bodů pro tohoto klienta řízeným způsobem.  

- Skupina hranic může mít více než jeden vztah. To vám umožní nakonfigurovat pro přechod k různým sousedním sousedům po různých časových obdobích.
- Klienti se budou moct jenom do hraniční skupiny, která je přímým sousedem aktuální skupiny hranic.
- Když je klient členem několika skupin hranic, je aktuální skupina hranic definovaná jako sjednocení všech skupin hranic daného klienta.  Tento klient pak může přejít k sousedovi kterékoli z těchto původních skupin hranic.

Kromě odkazů, které definujete, je k dispozici implicitní odkaz, který je vytvořen automaticky mezi hraničními skupinami, které vytvoříte, a výchozí skupinou hranic, která je automaticky vytvořena pro každou lokalitu. Tento automatický odkaz:
- Používají klienti, kteří nejsou na hranici přidružené k žádné skupině hranic v hierarchii, automaticky používají výchozí skupinu hranic z jejich přiřazené lokality k identifikaci platných umístění zdroje obsahu.   
-  Je výchozí záložní možnost z aktuální skupiny hranic do výchozí skupiny hranic lokality, která se používá po 120 minutách.

**Příklad použití nového modelu:** Vytvoříte tři skupiny hranic, které nesdílejí hranice nebo servery systému lokality:
- BG_A skupiny s distribučními body DP_A1 a DP_A2 přidruženy ke skupině
- BG_B skupiny s distribučními body DP_B1 a DP_B2 přidruženy ke skupině
- BG_C skupiny s distribučními body DP_C1 a DP_C2 přidruženy ke skupině

Síťová umístění klientů můžete přidat jako hranice pouze do skupiny hranic BG_A a potom můžete nakonfigurovat vztahy z této skupiny hranic na jiné dvě hraniční skupiny:
- Nakonfigurujete distribuční body pro první *sousední* skupinu (BG_B), která se má používat po 10 minutách. Tato skupina obsahuje distribuční body DP_B1 a DP_B2. Obě jsou dobře propojené s prvními hraničními umístěními skupin.
- Druhou *sousední* skupinu (BG_C) nakonfigurujete tak, aby se používala po 20 minutách. Tato skupina obsahuje distribuční body DP_C1 a DP_C2. Obě jsou v síti WAN z dalších dvou hraničních skupin.
- Také přidáte další distribuční bod, který je umístěn na serveru lokality, do výchozí skupiny hranic lokality lokality. Toto je vaše nejmenší preferované umístění zdroje obsahu, ale je centrálně umístěno ve všech skupinách hranic.

  Příklad skupin hranic a záložních časů:

  ![BG_Fallack](media/BG_Fallback.png)


S touto konfigurací:
- Klient zahajuje hledání obsahu z distribučních bodů v *aktuální* skupině hranic (BG_A), přičemž před přepnutím na další distribuční bod ve skupině hranic vyhledá každý distribuční bod dvě minuty. Fond klientů s platnými umístěními zdroje obsahu zahrnuje DP_A1 a DP_A2.
- Pokud se klientovi po 10 minutách nenajde obsah ze své *aktuální* skupiny hranic, přidá distribuční body ze skupiny hranic BG_B do svého hledání. Pak pokračuje v hledání obsahu z distribučního bodu ve sloučeném fondu distribučních bodů, který teď obsahuje tyto skupiny hranic BG_A i BG_B. Klient stále před přechodem na další distribuční bod z fondu pokračuje v každém distribučním bodě na dvě minuty. Fond klientů s platnými umístěními zdroje obsahu zahrnuje DP_A1, DP_A2, DP_B1 a DP_B2.
- Po dalších 10 minutách (celkem 20 minut) Pokud klient stále nenajde distribuční bod s obsahem, rozbalí svůj fond dostupných distribučních bodů, který bude zahrnovat tyto položky z druhé *sousední* skupiny, skupiny hranic BG_C. Klient má nyní 6 distribučních bodů pro vyhledávání (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 a DP_C2) a pokračuje v přechodu na nový distribuční bod každé dvě minuty, dokud nenalezne obsah.
- Pokud klient nenalezl obsah po celkem 120 minut, bude se vrátit k zahrnutí *výchozí skupiny hranic lokality* jako součást jejich pokračování v hledání. Fond distribučních bodů teď zahrnuje všechny distribuční body ze tří nakonfigurovaných skupin hranic a konečný distribuční bod umístěný na počítači serveru lokality.  Klient pak pokračuje v hledání obsahu a mění distribuční body každé dvě minuty, dokud nenalezne obsah.

Konfigurací různých sousedních skupin, které budou k dispozici v různých časech, při kterých budete řídit, kdy se konkrétní distribuční body přidávají jako umístění zdroje obsahu, a když, nebo pokud, klient použije jako bezpečnostní síť pro obsah, který není dostupný z jiného umístění, záložní výchozí skupinu hranic lokality.


### <a name="update-existing-boundary-groups-to-the-new-model"></a><a name="bkmk_update"></a>Aktualizace existujících skupin hranic na nový model
Když nainstalujete verzi 1609 a aktualizujete lokalitu, automaticky se provedou následující konfigurace. Cílem je zajistit, aby vaše aktuální nouzové chování zůstalo k dispozici, dokud nebudete konfigurovat nové skupiny hranic a vztahy.  
- Nechráněné distribuční body v lokalitě se přidají do skupiny hranic *Výchozí-lokalita – hranice skupiny \<sitecode> * této lokality.
- Vytvoří se kopie každé existující skupiny hranic, která obsahuje server lokality nakonfigurovaný s pomalým připojením. Název nové skupiny je *** \<original boundary group name> pomalý – TMP***:  
  -   Systémy lokality, které mají rychlé připojení, jsou ponechány v původní hraniční skupině.
  -   Kopii systémů lokality, které mají pomalé připojení, se přidají do kopie skupiny hranic. Původní systémy lokality nakonfigurované jako pomalé zůstanou v původní skupině hranic kvůli zpětné kompatibilitě, ale nepoužívají se z této skupiny hranic.
  -   K této kopii skupiny hranic nejsou přidruženy hranice. Záložní propojení se ale vytvoří mezi původní skupinou a novou kopií skupiny hranic, která má v záložním čase nastavenou hodnotu nula.

  Následující tabulka uvádí nové nouzové chování, které můžete očekávat od kombinace původních nastavení nasazení a konfigurací distribučních bodů:

Původní konfigurace nasazení pro možnost nespouštět program v pomalých sítích  |Původní konfigurace distribučního bodu pro "umožňuje klientovi používat náhradní umístění zdroje pro obsah"  |Nové nouzové chování  
---------|---------|---------
Vybráno     |  Vybráno    |  **Žádné záložní** použití distribučních bodů v aktuální skupině hranic       
Vybráno     |  Nevybráno|  **Žádné záložní** použití distribučních bodů v aktuální skupině hranic       
Nevybráno |  Nevybráno|  **Záložní pro sousední** síť – použijte distribuční body v aktuální skupině hranic a pak přidejte distribuční body ze sousední skupiny hranic. Pokud není nakonfigurovaný explicitní odkaz na výchozí skupinu hranic lokality, klienti nebudou moct přejít do této skupiny.    
Nevybráno | Vybráno |   **Normální záložní** -použití distribučních bodů v aktuální skupině hranic, pak z sousedních a výchozích skupin hranic lokality

 Všechny ostatní konfigurace nasazení mají za následek **normální zálohu**.  



## <a name="office-365-client-management-dashboard"></a>Řídicí panel pro správu klientů Office 365  
Configuration Manager 1609 Technical Preview zavádí nový řídicí panel. Řídicí panel zobrazíte tak, že v konzole Configuration Manager přejdete na přehled **knihovny softwaru**  >  **Overview**  >  **Sada Office 365 Správa klientů**.
>[!NOTE]
>V pracovním prostoru **co je nového** v konzole Configuration Manager se nový řídicí panel nesprávně jmenuje **řídicí panel údržby Office 365**.

Řídicí panel zobrazuje grafy pro následující:

- Počet klientů Office 365
- Verze klientů Office 365
- Jazyky klienta Office 365
- Klientské kanály pro Office 365     
Další informace najdete v tématu [Přehled kanálů aktualizací pro aplikace Microsoft 365](https://docs.microsoft.com/deployoffice/overview-update-channels).
- Pravidla automatického nasazení, která mají klienta Office 365 vybranou v sadě dostupných produktů.

Na řídicím panelu můžete provádět následující akce:
- V horní části řídicího panelu pomocí rozevíracího seznamu **kolekce** můžete data řídicího panelu filtrovat podle členů určité kolekce.
- V pravém horním rohu řídicího panelu klikněte na **instalační program office 365** a spusťte Průvodce instalací klienta sady Office 365 a nasaďte Microsoft 365 aplikace do klientů. Podrobnosti najdete v tématu [nasazení aplikací Microsoft 365 do klientů](#deploy-microsoft-365-apps-to-clients).
- V pravé prostřední straně řídicího panelu klikněte na **vytvořit** pravidlo automatického nasazení a otevřete Průvodce vytvořením nového pravidla automatického nasazení (ADR). Při vytváření pravidla automatického nasazení pro Microsoft 365 aplikace vyberte **klienta Office 365** při výběru produktu. Další informace najdete v tématu [automatické nasazení aktualizací softwaru](../../sum/deploy-use/automatically-deploy-software-updates.md).
- V pravé dolní části řídicího panelu klikněte na **vytvořit nastavení klientského agenta** a otevřete nastavení agenta klienta. Další informace najdete v tématu [informace o nastavení klienta](../clients/deploy/about-client-settings.md).



Další informace o Microsoft 365 aplikací pro podnikové aktualizace najdete v tématu [Správa aktualizací Microsoft 365 aplikací pomocí Configuration Manager](../../sum/deploy-use/manage-office-365-proplus-updates.md).

## <a name="deploy-microsoft-365-apps-to-clients"></a>Nasazení aplikací Microsoft 365 do klientů
V této verzi můžete z řídicího panelu pro správu klientů Office 365 spustit instalační program Office 365, který vám umožní nakonfigurovat Microsoft 365 nastavení instalace, stahovat soubory ze sítí pro doručování obsahu (sítě CDN) pro Office a nasazovat soubory jako aplikaci v Configuration Manager.

### <a name="limitations-of-microsoft-365-deployment"></a>Omezení nasazení Microsoft 365
- Při pokusu o Import existujícího nastavení klienta (XML) v Průvodci instalací aplikace sady Office 365 mohou nastat problémy. Můžete ručně nakonfigurovat nastavení klienta bez problému.

#### <a name="to-deploy-microsoft-365-apps-to-clients"></a>Nasazení aplikací Microsoft 365 do klientů
1. V konzole Configuration Manager přejděte do části Přehled **knihovny softwaru**  >  **Overview**  >  **Office 365 Správa klientů**.
2. V pravém horním podokně klikněte na **instalační program Office 365** . Otevře se Průvodce instalací klienta sady Office 365.
3. Na stránce **nastavení aplikace** zadejte název a popis aplikace, zadejte umístění pro stažení souborů a potom klikněte na tlačítko **Další**. Všimněte si, že umístění musí být zadáno ve formě &#92;&#92;&#92;*sdílené složky* *serveru* .
4. Na stránce **importovat nastavení klienta** vyberte, zda chcete importovat nastavení Microsoft 365 klienta z existujícího konfiguračního souboru XML nebo ručně zadat nastavení, a poté klikněte na tlačítko **Další**.
Pokud máte existující konfigurační soubor, zadejte umístění souboru a přejděte ke kroku 7. Všimněte si, že umístění musí být zadáno ve formuláři &#92;&#92;*server*&#92;*sdílet*&#92;*filename*. XML.

    > [!IMPORTANT]
    >Pokud se pokusíte importovat existující nastavení klienta (XML) v této verzi Technical Preview, může dojít k problémům.

5. Na stránce **klientské produkty** vyberte Microsoft 365 sadu, kterou chcete použít, vyberte aplikace, které chcete zahrnout, vyberte všechny další produkty Office, které by měly být zahrnuty, a poté klikněte na tlačítko **Další**.
6. Na stránce **nastavení klienta** vyberte nastavení, které chcete zahrnout, a potom klikněte na tlačítko **Další**.
7. Na stránce **nasazení** vyberte, zda chcete aplikaci nasadit, a poté klikněte na tlačítko **Další**.
Pokud se rozhodnete nenasadit balíček v průvodci, přejděte ke kroku 9.
8. Nakonfiguruje zbývající stránky průvodce jako při typickém nasazení aplikace. Další informace najdete v tématu [Vytvoření a nasazení aplikace](../../apps/get-started/create-and-deploy-an-application.md).
9. Dokončete průvodce.
10. Aplikaci můžete nasadit nebo upravit stejně jako jakoukoli jinou aplikaci v Configuration Manager z **knihovny softwaru**  >  **Přehled**  >  **aplikací pro správu aplikací**  >  **Applications**.

>[!NOTE]
>Po nasazení aplikací Microsoft 365 můžete vytvořit pravidla automatického nasazení, která budou aplikace spravovat. Pokud chcete vytvořit pravidlo automatického nasazení pro Microsoft 365 aplikace, klikněte na **vytvořit pravidlo automatického**nasazení a při výběru produktu vyberte **klienta Office 365** . Další informace najdete v tématu [automatické nasazení aktualizací softwaru](../../sum/deploy-use/automatically-deploy-software-updates.md).

## <a name="improvements-for-bios-to-uefi-conversion"></a><a name="BKMK_UEFIConversion"></a>Vylepšení převodu systému BIOS na rozhraní UEFI
Nyní můžete přizpůsobit pořadí úloh nasazení operačního systému novou proměnnou, TSUEFIDrive, aby krok restartovat počítač připravil oddíl FAT32 na pevném disku pro přechod do rozhraní UEFI. Následující postup popisuje, jak můžete vytvořit kroky pořadí úloh k přípravě pevného disku pro převod systému BIOS na rozhraní UEFI.

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Příprava oddílu FAT32 na převod na rozhraní UEFI:
V existujícím pořadí úkolů pro instalaci operačního systému přidáte novou skupinu s postupem, který provede převod systému BIOS na rozhraní UEFI.

1. Po krocích k zaznamenání souborů a nastavení a před instalací operačního systému vytvořte novou skupinu pořadí úkolů. Například vytvořte skupinu za skupinou **zachycení souborů a nastavení** s názvem **BIOS-to-UEFI**.
2. Na kartě **Možnosti** nové skupiny přidejte novou proměnnou pořadí úloh jako podmínku, kde **_SMSTSBootUEFI** se **nerovná hodnotě** **true**. Tím se zabrání spuštění kroků ve skupině v případě, že je počítač již v režimu UEFI.
![Skupina systému BIOS do rozhraní UEFI](media/BIOS-to-UEFI-group.png)
3. V části Nová skupina přidejte krok pořadí úkolů **restartovat počítač** . V části **Určete, co se má spustit po restartování**vyberte **spouštěcí bitová kopie přiřazená k tomuto pořadí úkolů slouží** ke spuštění počítače v systému Windows PE.  
4. Na kartě **Možnosti** přidejte proměnnou pořadí úloh jako podmínku, kde **_SMSTSInWinPE rovná hodnotě false**. Tím se zabrání spuštění tohoto kroku, pokud je počítač již v systému Windows PE.

    ![Krok restartování počítače](media/Restart-in-Windows-PE.png)
5. Přidejte krok, který spustí nástroj výrobce OEM, který převede firmware ze systému BIOS na rozhraní UEFI. Obvykle se jedná o krok **Spustit příkazový řádek** pořadí úkolů s příkazovým řádkem pro spuštění nástroje OEM.
5. Přidejte krok pořadí úkolů formátovat a rozdělit disk na oddíly, který bude rozdělit a naformátovat pevný disk. V kroku udělejte toto:
    1. Před instalací operačního systému vytvořte oddíl FAT32, který bude převeden na rozhraní UEFI. Jako **typ disku**vyberte **GPT** .
    ![Krok formátovat a rozdělit disk na oddíly](media/Format-and-partition-disk.png)
    2. Přejít na vlastnosti oddílu FAT32. Do pole **Proměnná** zadejte **TSUEFIDrive** . Když pořadí úkolů tuto proměnnou detekuje, před restartováním počítače se připraví na přechod rozhraní UEFI.
    ![Vlastnosti oddílu](media/Partition-properties.png)
    3. Vytvořte oddíl NTFS, který modul pořadí úkolů používá k uložení stavu a ukládání souborů protokolu.
6. Přidejte krok pořadí úkolů **restartovat počítač** . V části **Určete, co se má spustit po restartování**vyberte **spouštěcí bitová kopie přiřazená k tomuto pořadí úkolů slouží** ke spuštění počítače v systému Windows PE.  




## <a name="intune-compliance-charts"></a>Grafy dodržování předpisů v Intune
V této verzi můžete získat rychlý přehled o celkovém dodržování předpisů pro zařízení a hlavní důvody pro nedodržování předpisů pomocí nových grafů v části **pracovní prostor monitorování** v konzole Configuration Manager.

#### <a name="to-view-the-intune-compliance-charts"></a>Zobrazení grafů kompatibility Intune
1. V konzole Configuration Manager klikněte na **monitorování**  >  **Přehled**  >  **Nastavení dodržování předpisů**.
2. Zobrazí se **Celkový graf kompatibility zařízení** .
3. Kliknutím na uzel **zásady dodržování předpisů** zobrazíte grafy **celkových požadavků na zařízení** a **nedodržování předpisů** .

### <a name="limitations-of-intune-compliance-charts-in-tp-1609"></a>Omezení grafů dodržování předpisů Intune v TRANSAKČNÍm systému 1609
- Procházení hierarchie **celkového grafu dodržování předpisů zařízením** aktuálně generuje chybu.
- V grafu **nejdůležitějších příčin nedodržení předpisů** je seznam názvů zásad, nikoli individuální důvody pro nedodržování předpisů. Můžete kliknout na zásadu a přejít k podrobnostem a zobrazit zařízení, která nedodržují předpisy pro tyto zásady.

### <a name="try-it-out"></a>Vyzkoušet
Dokončete následující části v uvedeném pořadí:

#### <a name="check-overall-compliance-chart"></a>Zkontroluje celkový graf dodržování předpisů.
1. Přidejte dvě zásady dodržování předpisů pro iOS v Configuration Manager. Jedna zásada by měla mít jednu sadu nastavení pro zařízení (například nastavte délku kódu PIN na 6). Ostatní zásady by měly mít jinou sadu nastavení (například složitost PIN kódu). Nastavení zásad se nesmí překrývat nebo být v konfliktu.
2. Tyto dvě zásady nasaďte do skupiny uživatelů.
3. Zaregistrujte dvě zařízení s iOS v Intune pomocí stejného uživatelského účtu a účtu, který tyto zásady přijal v předchozím kroku. Zařízení by neměla splňovat kritéria zásad dodržování předpisů.
4. V Configuration Manager se podívejte na **Celkový graf dodržování předpisů zařízením** . Obě zařízení by měla hlásit nedodržující předpisy.
<!-- 5. Click the **Non-compliant** section of the chart. Both devices should appear in the filtered view under **Assets and Compliance** > **Overview** > **Device**. -->

#### <a name="check-the-top-non-compliance-reasons-chart"></a>Podívejte se na graf důvodů nedodržení předpisů.
5. Podívejte se na graf **důvodů nedodržení předpisů** . Tento graf obsahuje 5 hlavních důvodů pro nedodržení předpisů, ale v případě, že se v rámci zásad nastavila jenom dvě nastavení dodržování předpisů, zobrazí se jenom 2 nejčastější důvody, které nedodržují předpisy.
6. Klikněte na jeden z oddílů v grafu. Obě zařízení by se měla zobrazit v filtrovaném zobrazení v části **prostředky a**  >  **Přehled**kompatibility  >  **zařízení**.

#### <a name="make-devices-compliant-and-check-the-charts"></a>Nastavení zařízení jako kompatibilních a kontroly grafů
7. Nastavte jedno ze zařízení, která jsou kompatibilní s jednou ze zásad. Ověřte znovu **Celkový graf dodržování předpisů zařízením** . V grafu by se měl zobrazit jedno vyhovující zařízení a jedno zařízení, které nedodržuje předpisy.
8. Nastavte, aby ostatní zařízení dodržovala stejné zásady. V takovém případě bude v jednom zařízení, které bude vyhovovat oběma zásadám, i jednomu zařízení, které bude splňovat jenom jedna ze zásad.
9. Podívejte se na graf **důvodů nedodržení předpisů** . V seznamu by měl být jenom jeden důvod, který nedodržuje předpisy.
<!--7. Click the **Compliant** section of the chart. Only the compliant device should appear in the filtered view. -->





## <a name="see-also"></a>Viz také
[Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md)