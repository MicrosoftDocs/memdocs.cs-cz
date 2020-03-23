---
title: Nastavení zásad ochrany aplikací pro Android
titleSuffix: Microsoft Intune
description: Toto téma popisuje nastavení zásad ochrany aplikací pro zařízení s Androidem.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 9e9ef9f5-1215-4df1-b690-6b21a5a631f8
ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c5dbe2abf7a23be9f9e0051a2ff26590e749f98c
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79326199"
---
# <a name="android-app-protection-policy-settings-in-microsoft-intune"></a>Nastavení zásad ochrany aplikací pro Android v Microsoft Intune
Tento článek popisuje nastavení zásad ochrany aplikací pro zařízení s Androidem. Popsaná nastavení zásad lze [nakonfigurovat](app-protection-policies.md) pro zásady ochrany aplikací v podokně **Nastavení** v Azure Portal.
Existují tři kategorie nastavení zásad: nastavení ochrany dat, požadavky na přístup a podmíněné spuštění. Termín *aplikace spravované podle zásad* v tomto článku označuje aplikace, které mají nakonfigurované zásady ochrany aplikací.

> [!IMPORTANT]
> Na zařízení se vyžaduje Portál společnosti Intune pro příjem zásad ochrany aplikací pro zařízení s Androidem. Další informace najdete v tématu [požadavky aplikace Portál společnosti Intune Access](../fundamentals/end-user-mam-apps-android.md).

## <a name="data-protection"></a>Ochrana dat 
### <a name="data-transfer"></a>Přenos dat
| Nastavení | Způsob použití | Výchozí hodnota |
|------|------|------|
| **Zálohování dat organizace do zálohovacích služeb pro Android** | Vyberte možnost **blokovat** , pokud chcete této aplikaci zabránit v zálohování pracovních nebo školních dat do [zálohovací služby pro Android](https://developer.android.com/google/backup/index.html).<br><br> Výběrem této možnost **povolíte** této aplikaci zálohování pracovních nebo školních dat.| **Povoleno** |
| **Posílání organizačních dat do jiných aplikací** | Určete, jaké aplikace můžou přijímat data z této aplikace: <ul><li> **Aplikace spravované podle zásad:** Povoluje přenos jenom do jiných aplikací spravovaných podle zásad.</li> <li>**Všechny aplikace**: Povoluje přenos do všech aplikací. </li> <li>**Žádné:** Nepovoluje přenos dat do žádné aplikace, včetně ostatních aplikací spravovaných podle zásad.</li></ul> <p>U některých aplikací a služeb, které mají výjimku, může být v Intune standardně povolený přenos dat. Pokud potřebujete povolit přenos dat do aplikace, která nepodporuje zásady ochrany aplikací Intune, můžete vytvořit vlastní výjimky. Další informace najdete v tématu [výjimky přenosu dat](app-protection-policy-settings-android.md#data-transfer-exemptions).<p>Tato zásada může platit také pro odkazy na aplikace pro Android.  Obecné webové odkazy se spravují pomocí **odkazů otevřít aplikace v** nastavení zásad Intune Managed Browser.<p><div class="NOTE"><p>Poznámka</p><p>Intune v současné době nepodporuje funkci rychlých aplikací pro Android. Intune jakékoli datové připojení k aplikaci nebo z aplikace zablokuje. Další informace najdete v tématu [Android Instant Apps](https://developer.android.com/topic/instant-apps/index.html) v dokumentaci pro vývojáře pro Android.</p><p>Pokud jsou pro **všechny aplikace**nakonfigurované **údaje pro odesílání organizačních dat do jiných aplikací** , můžou se textová data dál přenášet prostřednictvím sdílení operačního systému do schránky.</p></div> | **Všechny aplikace** | 
|<ul><ui>**vybrat aplikace, které se mají vyloučit** | Tato možnost je k dispozici, když pro předchozí možnost vyberete možnost *aplikace spravované zásadou* . | |
|<ul><ui>**Uložit kopie dat org** | Zvolením možnosti **blokovat** zakážete použití možnosti Uložit jako v této aplikaci. Vyberte možnost **povoleno** , pokud chcete povolí použití možnosti Uložit jako. **Poznámka:** *Toto nastavení je podporováno pro aplikace Microsoft Excel, OneNote, PowerPoint a Word. Můžou je podporovat i obchodní aplikace třetích stran.*| **Povoleno** |  
|<ul><ui>**umožňuje uživateli ukládat kopie do vybraných služeb** . |Uživatelé můžou k ukládání používat vybrané služby (OneDrive pro firmy, SharePoint a místní úložiště). Všechny ostatní služby budou blokované.  | **0 vybráno** |
| **Příjem dat z jiných aplikací** | Určete, jaké aplikace můžou převádět data do této aplikace: <ul><li>**Aplikace spravované podle zásad:** Povoluje přenos jenom z jiných aplikací spravovaných podle zásad.</li><li>**Všechny aplikace**: Povoluje přenos dat ze všech aplikací.</li><li>**Žádné:** Nepovoluje přenos dat z žádné aplikace, včetně ostatních aplikací spravovaných podle zásad. </li></ul> <p>Z některých aplikací a služeb, které mají výjimku, může Intune povolit přenos dat. Úplný seznam takových aplikací a služeb najdete v části [Výjimky přenosu dat](app-protection-policy-settings-android.md#data-transfer-exemptions). | **Všechny aplikace** |
|<ul><ui>**otevřít data do organizačních dokumentů** | Tato možnost je k dispozici, když pro předchozí možnost vyberete možnost *aplikace spravované zásadou* . Vybírejte z těchto možností: <ul><li>**Blok**: zakáže použití možnosti *otevřít* nebo jiných možností pro sdílení dat mezi účty v této aplikaci. </li><li>**Allow**: povolí použití *otevřených* a dalších možností ke sdílení dat mezi účty v této aplikaci.||
|<ul><ui>**uživatelům dovolit, aby otevírali data z vybraných služeb** | Tato možnost je k dispozici, když pro předchozí možnost vyberete možnost *blok* . Vyberte služby úložiště aplikací, ze kterých uživatelé můžou data otevírat. Všechny ostatní služby jsou blokované. Výběrem možnosti žádné služby znemožníte uživatelům otevírat data.| |
| **Omezit vyjmutí, kopírování a vkládání mezi ostatními aplikacemi** | Určete, kdy se můžou v této aplikaci použít akce vyjmutí, kopírování a vložení. Vybírejte z těchto možností: <ul><li>**Blokováno:** Nepovoluje akce vyjmutí, kopírování a vložení mezi touto a jakoukoliv jinou aplikací.</li><li>**Aplikace spravované podle zásad:** Povoluje operace vyjmutí, kopírování a vložení mezi touto aplikací a jinými aplikacemi spravovanými podle zásad.</li><li>**Aplikace s vložením spravované podle zásad:** Povoluje vyjmutí a kopírování mezi touto aplikací a jinými aplikacemi spravovanými podle zásad. Povoluje vložení dat z jakékoliv aplikace do této aplikace.</li><li>**Libovolná aplikace:** Operace vyjmutí, kopírování a vložení do a z této aplikace nejsou nijak omezené. | **Libovolná aplikace** |
| <ul><ui>**vyjmutí a zkopírování limitu znaků u jakékoli aplikace** | Zadejte počet znaků, které mohou být vyjmuty nebo zkopírovány z dat a účtů organizace.  To umožní sdílet zadaný počet znaků, pokud by byl jinak zablokován nastavením "Omezit vyjmutí, kopírování a vložení s jinými aplikacemi".<p>Výchozí hodnota = 0<p>**Poznámka**: vyžaduje portál společnosti Intune verze 5.0.4364.0 nebo novější.  | **0** |
| **Snímek obrazovky a pomocník Google** | Vyberte **blok** pro blokování snímku obrazovky a schopnosti zařízení **Google Assistant** při používání této aplikace. Když **zvolíte možnost** při použití této aplikace s pracovním nebo školním účtem, rozostří se i obrázek náhledu s přepínačem aplikace.| **Blokováno** |
| **Schválené klávesnice**  | Vyberte *vyžadovat* a pak zadejte seznam schválených klávesnic pro tuto zásadu. <p>Uživatelům, kteří nepoužívají schválenou klávesnici, se zobrazí výzva ke stažení a instalaci schválené klávesnice před tím, než budou moci používat chráněnou aplikaci. Toto nastavení vyžaduje, aby měla aplikace sadu Intune SDK pro Android verze 6.2.0 nebo novější. | **Nepožadováno** |
| <ul><ui>**výběru klávesnic ke schválení** | Tato možnost je k dispozici, když vyberete možnost *vyžadovat* u předchozí možnosti. Zvolením možnosti *Vybrat* můžete spravovat seznam klávesnic a metod zadávání, které se dají používat s aplikacemi chráněnými touto zásadou. Do seznamu můžete přidat další klávesnice a odebrat všechny výchozí možnosti. Chcete-li uložit nastavení, musíte mít alespoň jednu schválenou klávesnici. Pokud chcete přidat klávesnici, zadejte: <ul><li>**Název**: popisný název, který identifikuje klávesnici a je viditelný pro uživatele. </li><li>**ID balíčku**: ID balíčku aplikace v Google Play Storu. Pokud je například adresa URL aplikace v obchodě Play `https://play.google.com/store/details?id=com.contoskeyboard.android.prod`, ID balíčku je `com.contosokeyboard.android.prod`. ID tohoto balíčku se zobrazí uživateli jako jednoduchý odkaz pro stažení klávesnice z Google Play. <p><div class="NOTE"><p>Poznámka</p><p>Uživateli, kterému je přiřazeno více zásad ochrany aplikací, bude povoleno používat pouze schválené klávesnice společné pro všechny zásady.</p> | |

### <a name="encryption"></a>Šifrování
| Nastavení | Způsob použití | Výchozí hodnota |
|------|------|------|
| **Šifrování dat organizace** | Vyberte **vyžadovat** , pokud chcete v této aplikaci povolit šifrování pracovních nebo školních dat. Intune používá k bezpečnému šifrování dat aplikací rozhraní OpenSSL (256) šifrování AES a systém úložiště klíčů pro Android. Data jsou mezi vstupně-výstupními úlohami souborů synchronně šifrovaná. Obsah v úložišti zařízení je zašifrovaný vždycky. Nové soubory budou šifrovány pomocí 256 bitových klíčů. Stávající 128 zašifrované soubory budou podrobeny pokusu o migraci do 256 klíčů, ale proces není zaručen. Soubory zašifrované pomocí 128 bitových klíčů budou moci být čitelné. <br><br> Metoda šifrování je ověřená FIPS 140-2; Další informace najdete v tématu [Knihovna FIPS OpenSSL a příručka pro Android](https://wiki.openssl.org/images/7/76/OpenSSL_FIPS_Library_and_Android_Guide.pdf).     |  **Žádá**|  
| <ul><ui>**šifrování dat organizace v zaregistrovaných zařízeních** | Vyberte **vyžadovat** , pokud chcete vynutit šifrování organizačních dat pomocí šifrování aplikační vrstvy Intune na všech zařízeních. Pokud nechcete vymáhat šifrování organizačních dat pomocí šifrování vrstvy aplikace Intune v zaregistrovaných zařízeních, vyberte **není nutné** .| **Žádá** |


### <a name="functionality"></a>Funkce
| Nastavení | Způsob použití | Výchozí hodnota |
|------|------|------|
| **Synchronizace aplikace s nativní aplikací kontaktů** | Vyberte možnost **blokovat** , pokud chcete, aby aplikace neukládala data do nativní aplikace kontakty na zařízení. Pokud zvolíte možnost **Povolení**, aplikace může ukládat data do nativní aplikace kontakty na zařízení. <br><br>Když budete z aplikace selektivně mazat pracovní nebo školní data, odeberou se kontakty synchronizované přímo z aplikace do nativní aplikace Kontakty. Kontakty synchronizované z nativního adresáře do dalšího externího zdroje není možné vymazat. To se v současné době týká jenom aplikace Microsoft Outlook. | **Povoleno** |
| **Tisk organizačních dat** | Vyberte možnost **blokovat** , pokud chcete aplikaci zabránit v tisku pracovních nebo školních dat. Pokud necháte toto nastavení **povolené**, budou uživatelé moci exportovat a tisknout všechna organizační data. | **Povoleno** |
|**Omezit přenos webového obsahu s jinými aplikacemi** | Určete, jakým způsobem se otevírá webový obsah (odkazy http/https) z aplikací spravovaných zásadami. Vybírejte z těchto možností: <ul><li>**Libovolná aplikace**: umožňuje webové odkazy v libovolné aplikaci.</li><li>**Intune Managed Browser**: povolí otevření webového obsahu jenom v Intune Managed Browser. Tento prohlížeč je prohlížeč spravovaný pomocí zásad.</li><li>**Microsoft Edge**: povolí otevření webového obsahu jenom v Microsoft Edge. Tento prohlížeč je prohlížeč spravovaný pomocí zásad.</li><li>**Nespravovaný prohlížeč**: povolí otevření webového obsahu v nespravovaném prohlížeči definovaném nastavením **nespravovaného protokolu prohlížeče** . Webový obsah nebude v cílovém prohlížeči spravovaný.<br>**Poznámka**: vyžaduje portál společnosti Intune verze 5.0.4415.0 nebo novější.</li><br><br>**Prohlížeče spravované zásadami**<br>Pokud není nainstalovaný ani Intune Managed Browser ani Microsoft Edge, mohou si v Androidu koncoví uživatelé zvolit z jiných aplikací spravovaných zásadami, které podporují odkazy http/https.<p>Pokud je vyžadován prohlížeč spravovaný v zásadách, ale není nainstalován, budou koncoví uživatelé vyzváni k instalaci Microsoft Edge.<p>Pokud se vyžaduje prohlížeč spravovaný zásadami, jsou odkazy na aplikace pro Android spravované nastavením zásady **Povolit aplikaci posílat data do jiných aplikací**.<p>**Registrace zařízení v Intune**<br>Pokud ke správě zařízení používáte Intune, přečtěte si téma [Správa přístupu k internetu pomocí zásad spravovaného prohlížeče v Microsoft Intune](app-configuration-managed-browser.md).<p>**Microsoft Edge spravovaný zásadami**<br>Prohlížeč Microsoft Edge pro mobilní zařízení (iOS/iPadOS a Android) podporuje zásady ochrany aplikací Intune. Uživatelé, kteří se v aplikaci prohlížeče Microsoft Edge přihlásí svými podnikovými účty Azure AD, budou chráněni službou Intune. Prohlížeč Microsoft Edge integruje sadu APP SDK a podporuje všechny zásady ochrany dat, a to s výjimkou prevence těchto zásad:<br><ul><li>**Uložit jako**: Prohlížeč Microsoft Edge neumožňuje uživateli přidávat přímá připojení z aplikací k poskytovatelům cloudového úložiště (jako je třeba OneDrive).</li><li>**Synchronizace kontaktů**: Prohlížeč Microsoft Edge neukládá do nativních seznamů kontaktů.</li></ul>**Poznámka:** *sada App SDK nemůže určit, jestli je cílová aplikace prohlížeč. V zařízeních s Androidem jsou povolené i další aplikace spravovaného prohlížeče, které podporují záměr http/https.* | **Nenakonfigurované** |
|<ul><ui>**ID nespravovaného prohlížeče** | Zadejte ID aplikace pro jeden prohlížeč. Webový obsah (odkazy http/https) z aplikací spravovaných zásadou se otevřou v zadaném prohlížeči.  Webový obsah nebude v cílovém prohlížeči spravovaný. | **Trhnout** |
|<ul><ui>**název nespravovaného prohlížeče** | Zadejte název aplikace pro prohlížeč přidružený k **nespravovanému ID prohlížeče**. Tento název se zobrazí uživatelům, pokud není nainstalovaný zadaný prohlížeč.  | **Trhnout** |
| **Oznámení o datech organizace** | Určete, kolik dat organizace se sdílí pomocí oznámení operačního systému pro účty org. Nastavení této zásady ovlivní místní zařízení a veškerá připojená zařízení, například wearables a inteligentní reproduktory. Aplikace můžou poskytovat další ovládací prvky pro přizpůsobení chování oznámení nebo se můžou rozhodnout Nedodržovat všechny hodnoty. Vyberte z těchto možností: <ul><li>**Blokovat**: Nesdílet oznámení.</li><ul><li>Pokud aplikace nepodporuje, budou oznámení povolena.</li></ul><li>**Blokovat organizační data**: nesdílejte data organizace v oznámeních. Například "máte novou poštu"; "Máte schůzku"</li><UL><li>Pokud aplikace nepodporuje, budou oznámení zablokovaná.</li></ul><li>**Allow**: sdílení dat organizace v oznámeních</li></ul> <p>**Poznámka**: *Toto nastavení vyžaduje podporu aplikace. V tuto chvíli bude aplikace Outlook pro Android 4.95.0 nebo novější podporovat toto nastavení, což očekává, že vydáte týden od 16. prosince 2019.* | **Povoleno**   |

## <a name="data-transfer-exemptions"></a>Výjimky přenosu dat

U některých aplikací a služeb platformy, které mají výjimku, můžou zásady ochrany aplikací Intune umožňovat přenos dat do a z. Všechny aplikace na Androidu spravované přes Intune například musí mít možnost přenášet data do a z Převodu textu na řeč Google, aby se mohl nahlas číst text z obrazovky mobilního zařízení. Tento seznam se může měnit. Obsahuje služby a aplikace, které se považují za užitečné pro bezpečné a produktivní použití.

### <a name="full-exemptions"></a>Úplné výjimky

  Tyto aplikace můžou bez omezení přenášet data do aplikací spravovaných službou Intune a z nich.

  |Název aplikace nebo služby | Popis |
  | ------ | ---- |
  | com.android.phone | Nativní telefonní aplikace
  | com.android.vending | Obchod Google Play |
  | com.android.documentsui | Výběr dokumentů pro Android|
  | com.google.android.webview | Třída [WebView](https://developer.android.com/reference/android/webkit/WebView.html), která je nutná pro mnoho aplikací včetně Outlooku |
  | com.android.webview |Třída [WebView](https://developer.android.com/reference/android/webkit/WebView.html), která je nutná pro mnoho aplikací včetně Outlooku|
  | com.google.android.tts | Převod textu na řeč Google |
  | com.android.providers.settings | Nastavení systému Android |
  | com.android.settings | Nastavení systému Android |
  | com.azure.authenticator | Aplikace Azure Authenticator, která je nutná k úspěšnému ověřování v mnoha situacích |
  | com.microsoft.windowsintune.companyportal | Portál společnosti Intune|

### <a name="conditional-exemptions"></a>Podmíněné výjimky
  Tyto aplikace můžou přenášet data do aplikací spravovaných službou Intune a z nich za určitých podmínek.

  |Název aplikace nebo služby | Popis | Podmínka výjimky|
  | ------ | ---- | --- |
  | com.android.chrome | Prohlížeč Google Chrome | Prohlížeč Chrome se používá pro některé komponenty WebView na Androidu 7.0+ a není nikdy skrytý. Tok dat do aplikace a z ní je ale vždy omezený.  |
  | com.skype.raider | Skype | Aplikace Skype je povolená jenom pro určité akce, jejichž výsledkem je telefonní hovor. |
  | com.android.providers.media | Poskytovatel multimediálního obsahu pro Android | Poskytovatel multimediálního obsahu je povolený jenom pro akci výběru vyzváněcího tónu. |
  | com.google.android.gms, com.google.android.gsf | Balíčky Služeb Google Play | Tyto balíčky jsou povolené pro akce Google Cloud Messaging, například pro nabízená oznámení. |
  | com. Google. Android. Apps. Maps | Mapy Google | Adresy jsou povoleny pro navigaci. |

Další informace najdete v tématu [Výjimky zásad přenosu dat pro aplikace](app-protection-policies-exception.md).

## <a name="access-requirements"></a>Požadavky na přístup

| Nastavení | Způsob použití |  
|------|------| 
| **Připnout pro přístup** | Vyberte **vyžadovat** , pokud chcete, aby se tato aplikace používala pro PIN. Uživateli se zobrazí výzva k nastavení tohoto kódu PIN při prvním spuštění aplikace v pracovním nebo školním kontextu. <br><br> Výchozí hodnota = **vyžadovat**<br><br> Sílu PIN můžete nakonfigurovat pomocí nastavení dostupných v části kód PIN pro přístup.
| <ul>**typ kódu PIN** <ui> | Než budete mít přístup k aplikaci, která má použité zásady ochrany aplikací, nastavte pro PIN kód buď číselné nebo textové kódy. Číselná podoba vyžaduje jen číslice, zatímco heslo může být definované s minimálně 1 abecedním písmenem **nebo** s minimálně 1 speciálním znakem. <br><br> Výchozí hodnota = **Čísla**<br><br> **Poznámka:** Povolené speciální znaky zahrnují speciální znaky a symboly na anglické klávesnici pro Android. |
| <ul><ui> **jednoduchý PIN kód** | Pokud chcete uživatelům dovolit používat jednoduché posloupnosti kódu PIN jako *1234*, *1111*, *abcd* nebo *AAAA*, vyberte možnost **povoleno** . Vyberte **bloky** a zabráníte tak použití jednoduchých sekvencí. Jednoduché posloupnosti jsou zkontrolovány v oknech se třemi znaky. Pokud je **blok** nakonfigurovaný, 1235 nebo 1112 by se nepřijal jako PIN kód nastavený koncovým uživatelem, ale 1122 by bylo povolené. <br><br>Výchozí hodnota = **Allow** <br><br>**Poznámka:** Pokud je nakonfigurován kód PIN pro typ hesla a v kódu PIN je nastavená možnost jednoduchý kód PIN, uživatel potřebuje alespoň jedno písmeno **nebo** aspoň jeden speciální znak ve svém PIN kódu. Pokud je nakonfigurován kód PIN pro typ hesla a jednoduchý kód PIN je nastaven na blokovat, uživatel potřebuje alespoň jednu číslici **a** jedno písmeno **a** alespoň jeden speciální znak ve svém PIN kódu. </li> |
| <ul><ui> **Vybrat minimální délku PIN kódu** | Určuje minimální počet číslic v posloupnosti kódu PIN. <br><br>Výchozí hodnota = **4** | 
| <ul><ui> **otisk prstu místo PIN kódu pro přístup (Android 6.0 +)** | Vyberte možnost **povoluje** uživateli, aby místo kódu PIN pro přístup k aplikacím používal [ověřování pomocí otisku prstu](https://developer.android.com/about/versions/marshmallow/android-6.0.html#fingerprint-authentication) . <br><br>Výchozí hodnota = **Allow** <br><br>**Poznámka:** Tato funkce podporuje obecné ovládací prvky pro biometriky v zařízeních s Androidem. Nastavení biometriky specifické pro výrobce OEM, jako je například Samsung Pass, *se nepodporuje.* <br><br>V Androidu můžete nechat uživatele prokázat svoji identitu [ověřením otiskem prstu v Androidu](https://developer.android.com/about/versions/marshmallow/android-6.0.html#fingerprint-authentication) namísto PIN kódu. Když se uživatel pokusí použít tuto aplikaci se svým pracovním nebo školním účtem, zobrazí se výzva k zadání otisku prstu a uživatel nemusí zadávat PIN kód. <br><br> Zařízení zaregistrovaná do pracovního profilu Android vyžadují pro vynucení zásad přístupu registraci samostatného otisku prstu **místo kódu PIN** . Tyto zásady platí jenom pro aplikace spravované pomocí zásad, které jsou nainstalované v pracovním profilu Androidu. Až se registrací na Portálu společnosti vytvoří pracovní profil Androidu, musí se samostatný otisk prstu zaregistrovat na zařízení. Další informace o otiscích prstů pro pracovní profily Androidu najdete v článku o [uzamknutí pracovního profilu](https://support.google.com/work/android/answer/7029958). |
| <ul>**po vypršení časového limitu <ui>přepsat otisk prstu kódem PIN**| Chcete-li použít toto nastavení, vyberte možnost **vyžadovat** a pak nakonfigurujte časový limit nečinnosti. <br><br>Výchozí hodnota = **vyžadovat** |
| <ul><ui><ul><ui> **časový limit (v minutách neaktivity)**| Zadejte dobu v minutách, po které bude PIN kód nebo číselný kód (jak je nakonfigurováno) přepsat používání otisku prstu. Hodnota časového limitu by měla být větší než hodnota zadaná v možnosti znovu ověřit požadavky na přístup po (minuty neaktivity).<br><br>Výchozí hodnota = **30** |
| <ul><ui>**Resetování PIN kódu po počtu dní** | Vyberte **Ano** , pokud chcete, aby uživatelé po nastaveném časovém intervalu (ve dnech) změnili PIN kód aplikace.  <br><br>Když nastavíte *Ano*, nakonfigurujete počet dní, než se bude vyžadovat Resetování PIN kódu. <br><br> Výchozí hodnota = **Ne**  |  
| <ul><ui><ul><ui> **počet dnů** | Nakonfigurujte počet dní, než se vyžaduje Resetování PIN kódu. <br><br> Výchozí hodnota = **90**  |
| <ul><ui>**vybrat počet předchozích hodnot PIN, které se mají zachovat** | Toto nastavení určuje počet předchozích PIN kódů, které Intune bude uchovávat. Jakékoli nové PIN kódy se musí lišit od těch, které Intune udržuje. <br><br> Výchozí hodnota = **0** | 
| <ul><ui>**PIN kód aplikace, když je nastavený PIN kód zařízení** | Vyberte **není nutné** , pokud chcete zakázat PIN kód aplikace, když se na zaregistrovaném zařízení zjistí zámek zařízení s nakonfigurovaným portál společnosti. <br><br> Výchozí hodnota = **vyžadovat**. | 
| **Přihlašovací údaje k pracovnímu nebo školnímu účtu pro přístup** | Vyberte **vyžadovat** , pokud chcete, aby se uživatel přihlásil pomocí svého pracovního nebo školního účtu místo zadání kódu PIN pro přístup k aplikaci. Pokud je nastavena možnost **vyžadovat**a jsou zapnuté výzvy k zadání kódu PIN nebo biometriky, zobrazí se jak přihlašovací údaje, tak PIN nebo biometrické. <br><br>Výchozí hodnota = **není požadováno** |
| **Znovu ověřit požadavky na přístup po (minuty neaktivity)** | Nakonfigurujte následující nastavení: <ul><li>**Časový limit:** Toto je počet minut před opakovaným zkontrolováním požadavků na přístup k aplikaci (definovaným dříve v zásadách). Správce například v zásadách zapne PIN kód a zablokuje zařízení s rootem. Uživatel otevře aplikaci spravovanou přes Intune, musí zadat PIN kód a musí aplikaci používat na zařízení bez rootu. Při tomto nastavení nemusí uživatel v žádné aplikaci spravované v Intune zadávat PIN ani podstupovat další kontrolu výskytu rootu po dobu, která odpovídá nakonfigurované hodnotě.  <br><br>Tento formát nastavení zásady podporuje kladné celé číslo. <br><br> Výchozí hodnota = **30 minut** <br><br> **Poznámka:** V Androidu se kód PIN sdílí se všemi aplikacemi spravovanými přes Intune. Časovač kódu PIN se vynuluje, když se aplikace v zařízení přestane zobrazovat na popředí. Uživatel nebude muset zadávat kód PIN na jakékoli aplikaci spravované přes Intune, která po dobu trvání časového limitu definovaného v tomto nastavení sdílí svůj PIN kód. <br><br></li> |

> [!NOTE]  
> Další informace o tom, jak v Androidu fungují různá nastavení Intune App Protection nakonfigurovaná v části Přístup u stejné skupiny aplikací a uživatelů, najdete v článku věnovaném [častým otázkám k Intune MAM](mam-faq.md) a v článku [Selektivní vymazání dat pomocí akcí přístupu zásad ochrany aplikací v Intune](app-protection-policies-access-actions.md).


## <a name="conditional-launch"></a>Podmíněné spouštění
Pokud chcete ve svých zásadách ochrany přístupu nastavit bezpečnostní požadavky, které se týkají přihlašování, nakonfigurujte podmíněné spouštění. 

Výchozí nastavení obsahuje předem nakonfigurované hodnoty a akce. Některé nastavení můžete odstranit, třeba *Minimální verze operačního systému*. Z rozevíracího seznamu **Vyberte jednu možnost** můžete také vybrat další nastavení. 

| Nastavení | Způsob použití |  
|---------|------------| 
| **Maximální počet pokusů o zadání PIN kódu** | Zadejte počet pokusů, které uživatel bude mít k úspěšnému zadání PIN kódu před provedením nakonfigurované akce. Tento formát nastavení zásady podporuje kladné celé číslo. *Akce* zahrnují: <br><ul><li>**Resetovat PIN kód** – uživatel musí resetovat svůj PIN.</li></ul> <ul><li>**Vymazat data** – uživatelský účet, který je přidružený k aplikaci, se ze zařízení vymaže.  </li></ul> </li></ul> Výchozí hodnota = **5** |
| **Období odkladu pro offline režim** | Kolik minut můžou aplikace MAM běžet offline. Zadejte dobu (v minutách) před opakovaným zkontrolováním požadavků na přístup k aplikaci. *Akce* zahrnují: <br><ul><li>**Zablokovat přístup (minuty)** – kolik minut můžou aplikace MAM běžet offline. Zadejte dobu (v minutách) před opakovaným zkontrolováním požadavků na přístup k aplikaci. Aby mohla aplikace po uplynutí této doby dál běžet, vyžaduje ověření uživatele v Azure Active Directory (Azure AD). <br><br>Tento formát nastavení zásady podporuje kladné celé číslo. <br><br>Výchozí hodnota = **720** minut (12 hodin) </li></ul> <ul><li>**Vymazat data (dny)** – po kolika dnech (definovaných správcem) provozu offline bude aplikace vyžadovat, aby se uživatel připojil k síti a znovu se přihlásil. Pokud je ověření uživatele úspěšné, může ke svým datům dál přistupovat a doba v offline režimu se resetuje.  Pokud se ověření uživatele nezdaří, aplikace provede selektivní vymazání uživatelova účtu a dat. Další informace najdete v tématu [Jak z aplikací spravovaných pomocí Intune vymazat jenom firemní data](apps-selective-wipe.md).</li></ul> Tento formát nastavení zásady podporuje kladné celé číslo. <br><br>  Výchozí hodnota = **90 dní** </li></ul> <br><br>  Tato položka se může zobrazit vícekrát. V takovém případě každá instance podporuje jinou akci. |   
| **Zařízení s jailbreakem nebo rootem** |U tohoto nastavení se nezadává žádná hodnota. *Akce* zahrnují: <br><ul><li>**Blokovat přístup** – brání spuštění aplikace na zařízeních s jailbreakem nebo rootem (která mají odblokovaný systém). Uživatel může aplikaci dále používat pro své osobní účely, ale pokud v ní chce pracovat s pracovními nebo školními daty, musí použít jiné zařízení.</li></ul> <ul><li>**Vymazat data** – uživatelský účet, který je přidružený k aplikaci, se ze zařízení vymaže.  </li></ul> |
| **Minimální verze operačního systému** | Zadejte minimální operační systém pro Android, který je nutný k použití této aplikace. *Akce* zahrnují: <br><ul><li>**Upozornit** – pokud verze Androidu v zařízení nevyhovuje tomuto požadavku, zobrazí se uživateli oznámení. Toto oznámení je možné zavřít.  </li></ul> <ul><li>**Blokovat přístup** – pokud verze iOSu v zařízení nevyhovuje tomuto požadavku, bude uživatel zablokován.</li></ul> <ul><li>**Vymazat data** – uživatelský účet, který je přidružený k aplikaci, se ze zařízení vymaže.  </li></ul> </li></ul>Tento formát nastavení zásady podporuje vlastnosti major.minor, major.minor.build a major.minor.build.revision. |
| **Minimální verze aplikace** | Zadejte minimální verzi operačního systému. *Akce* zahrnují: <br><ul><li>**Upozornit** – pokud verze aplikace v zařízení nevyhovuje tomuto požadavku, zobrazí se uživateli oznámení. Toto oznámení je možné zavřít.</li></ul> <ul><li>**Blokovat přístup** – pokud verze aplikace v zařízení nevyhovuje tomuto požadavku, zablokuje se uživateli přístup. </li></ul> <ul><li>**Vymazat data** – uživatelský účet, který je přidružený k aplikaci, se ze zařízení vymaže. </li></ul> </li></ul> Vzhledem k tomu, že aplikace mívají často odlišná schémata verzí, vytvořte zásadu, ve které bude jedna minimální verze zacílená na jednu aplikaci (např. *Zásada verze Outlooku*).<br><br> Tato položka se může zobrazit vícekrát. V takovém případě každá instance podporuje jinou akci.<br><br> Tento formát nastavení zásady podporuje vlastnosti major.minor, major.minor.build a major.minor.build.revision.<br><br> Kromě toho můžete nakonfigurovat **, kde** můžou koncoví uživatelé získat aktualizovanou verzi obchodní aplikace (LOB). Koncovým uživatelům se zobrazí v dialogovém okně minimální spuštění podmíněné **verze aplikace** , ve kterém se koncovým uživatelům zobrazí výzva k aktualizaci na minimální verzi aplikace LOB. V Androidu Tato funkce používá Portál společnosti. Pokud chcete nakonfigurovat, kde by koncový uživatel měl aktualizovat obchodní aplikaci, potřebuje aplikace, aby ji poslala [Zásada Konfigurace spravované aplikace](app-configuration-policies-managed-app.md) s klíčem, `com.microsoft.intune.myappstore`. Hodnota odeslané bude určovat, ze kterého Storu bude koncový uživatel aplikaci stahovat. Pokud je aplikace nasazená prostřednictvím Portál společnosti, musí být hodnota `CompanyPortal`. Pro jakékoli jiné úložiště musíte zadat úplnou adresu URL. |
| **Minimální verze opravy** | Vyžaduje, aby na zařízení byla nainstalovaná minimální oprava zabezpečení Androidu vydaná Googlem.  <br><ul><li>**Upozornit** – pokud verze Androidu v zařízení nevyhovuje tomuto požadavku, zobrazí se uživateli oznámení. Toto oznámení je možné zavřít.  </li></ul> <ul><li>**Blokovat přístup** – pokud verze iOSu v zařízení nevyhovuje tomuto požadavku, bude uživatel zablokován.</li></ul> <ul><li>**Vymazat data** – uživatelský účet, který je přidružený k aplikaci, se ze zařízení vymaže.  </li></ul></li></ul> Nastavení zásady podporuje formát kalendářního data *RRRR-MM-DD*. |
| **Výrobci zařízení** | Zadejte seznam výrobců oddělených středníkem (ů). U těchto hodnot se nerozlišují velká a malá písmena. *Akce* zahrnují: <br><ul><li>**Povolit zadané (blokovat nezadané)** – aplikaci můžou používat jenom zařízení, která odpovídají zadanému výrobci. Všechna ostatní zařízení se zablokují. </li></ul> <ul><li>**Povolit zadané (vymazat nezadané)** – uživatelský účet, který je přidružený k aplikaci, se ze zařízení vymaže. </li></ul> Další informace o použití tohoto nastavení najdete v tématu [podmíněné akce spuštění](app-protection-policies-access-actions.md#android-policy-settings). |
| **Ověření zařízení SafetyNet** | Zásady ochrany aplikací podporují některá Google Play chránit rozhraní API. Toto nastavení konkrétně konfiguruje ověřování SafetyNet Google na zařízeních koncových uživatelů. Zadejte buď **základní integritu** , nebo **základní integritu a certifikovaná zařízení**. **Základní integrita** obsahuje informace o obecné integritě zařízení. Zařízení s rootem, emulátory, virtuální zařízení a zařízení se znaménkem neoprávněného selhání základní integrity. **Základní integrita & certifikovaným zařízením** se dozvíte o kompatibilitě zařízení s službami Google. Tuto kontrolu můžou předat jenom nezměněná zařízení, která získala certifikace od společnosti Google. *Akce* zahrnují: <br><ul><li>**Upozornit** – uživatel uvidí oznámení, pokud zařízení nesplňuje požadavky na kontrolu ověření identity na Google SafetyNet na základě konfigurované hodnoty. Toto oznámení je možné zavřít. </li></ul><ul><li>**Blokovat přístup** – uživateli je zablokován přístup, pokud zařízení nesplňuje SafetyNet kontrolu ověření identity od společnosti Google na základě nastavené hodnoty. </li></ul> <ul><li>**Vymazat data** – uživatelský účet, který je přidružený k aplikaci, se ze zařízení vymaže. </li></ul> </li></ul> Nejčastější dotazy týkající se tohoto nastavení najdete v tématu [Nejčastější dotazy k mam a ochraně aplikací](mam-faq.md#app-experience-on-android). |
| **Vyžadovat kontrolu hrozeb u aplikací** | Zásady ochrany aplikací podporují některá Google Play chránit rozhraní API. Toto nastavení konkrétně zajišťuje, aby byla pro zařízení koncových uživatelů zapnutá kontrola aplikací pro ověřování Google. V případě konfigurace bude koncový uživatel zablokován přístup, dokud nezapnete kontrolu aplikací Google na svém zařízení s Androidem. *Akce* zahrnují: <br><ul><li>**Upozornit** – uživateli se zobrazí oznámení, pokud není zapnutá kontrola aplikací v zařízení Google pro ověřování aplikací. Toto oznámení je možné zavřít. </li></ul><ul><li>**Blokovat přístup** – uživateli je zablokován přístup, pokud není zapnutá kontrola aplikací Google na zařízení. </li></ul></li></ul> Výsledky kontroly aplikací pro ověření Google jsou v konzole v sestavě **potenciálně škodlivé aplikace** . |
| **Minimální verze Portál společnosti** | Pomocí **Minimální verze portál společnosti**můžete zadat konkrétní minimální verzi portál společnosti, která se vynutila na zařízení koncového uživatele. Toto nastavení podmíněného spuštění umožňuje nastavit hodnoty pro **blokování přístupu**, **vymazání dat**a **Upozornění** jako na možné akce, když se jednotlivá hodnota nesplní. Možné formáty pro tuto hodnotu se řídí vzorem *[hlavní]. [ Vedlejší]* , *[hlavní]. [ Vedlejší]. [Build]* nebo *[hlavní]. [ Vedlejší]. [Build]. [Revize]* . Vzhledem k tomu, že někteří koncoví uživatelé nemusí preferovat vynucenou aktualizaci aplikací na místě, může být při konfiguraci tohoto nastavení ideální možnost upozornění. Obchod Google Play je dobrým úkolem, který odesílá jenom rozdílové bajty pro aktualizace aplikací, ale může to být i velké množství dat, které uživatel nemusí použít, pokud se v době aktualizace data používají. Vynucení aktualizace a stažení aktualizované aplikace může vést k neočekávaným poplatkům za data v době aktualizace. Další informace najdete v tématu [nastavení zásad pro Android](app-protection-policies-access-actions.md#android-policy-settings). |
| **Maximální povolená úroveň hrozby pro zařízení** | Zásady ochrany aplikací můžou využívat konektor Intune-MTD. Zadejte maximální povolenou úroveň hrozeb pro použití této aplikace. Hrozby se určují podle vaší zvolené aplikace dodavatele ochrany před mobilními hrozbami (MTD) na zařízení koncového uživatele. Zadejte buď *Secure*, *Nízká*, *střední*nebo *High*. *Zabezpečené* nevyžaduje na zařízení žádné hrozby a je to nejvíce omezující konfigurovatelná hodnota, zatímco *Vysoká* vyžaduje aktivní připojení Intune-to-MTD. *Akce* zahrnují: <br><ul><li>**Blokovat přístup** – uživateli bude zablokován přístup, pokud úroveň hrozeb určená vaší zvolenou aplikací dodavatele ochrany před mobilními hrozbami (MTD) na zařízení koncového uživatele nesplňuje tento požadavek.</li></ul> <ul><li>**Vymazat data** – uživatelský účet, který je přidružený k aplikaci, se ze zařízení vymaže.</li></ul>Další informace o použití tohoto nastavení najdete v tématu [povolení konektoru ochrany před mobilními hrozbami v Intune pro neregistrovaná zařízení](../protect/mtd-enable-unenrolled-devices.md). |