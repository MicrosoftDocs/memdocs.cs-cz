---
title: Zabalení aplikací pro iOS nástrojem Intune App Wrapping
description: Naučte se balit aplikace pro iOS beze změny samotného kódu aplikace. Připravte aplikace, abyste mohli použít zásady správy mobilních aplikací.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/02/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 99ab0369-5115-4dc8-83ea-db7239b0de97
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 373a5e55a28c6fab740a86a3ad2ad69c5fa08848
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078137"
---
# <a name="prepare-ios-apps-for-app-protection-policies-with-the-intune-app-wrapping-tool"></a>Příprava aplikací pro iOS na zásady ochrany aplikací pomocí nástroje Intune App Wrapping Tool

Pomocí nástroje Microsoft Intune App Wrapping Tool pro iOS můžete zapnout zásady ochrany aplikací Intune pro interní aplikace pro iOS, aniž byste museli měnit kód samotné aplikace.

Tento nástroj je vlastně aplikace příkazového řádku systému Mac OS, která vytvoří obálku aplikace. Až se aplikace zpracuje, můžete její funkce změnit tak, že do ní nasadíte [zásady ochrany aplikací](../apps/app-protection-policies.md).

Nástroj si můžete stáhnout na stránce [Microsoft Intune App Wrapping Tool pro iOS](https://github.com/msintuneappsdk/intune-app-wrapping-tool-ios) v GitHubu.

## <a name="general-prerequisites-for-the-app-wrapping-tool"></a>Obecné požadavky pro nástroj App Wrapping Tool

Než nástroj App Wrapping Tool spustíte, musíte splnit některé obecné požadavky:

* Stáhněte si nástroj [Microsoft Intune App Wrapping Tool pro iOS](https://github.com/msintuneappsdk/intune-app-wrapping-tool-ios) z GitHubu.

* Potřebujete počítač s macOS, na kterém běží OS X 10.8.5 nebo novější a je na něm nainstalovaná sada nástrojů Xcode verze 9 nebo novější.

* Vstupní aplikaci pro iOS musí vyvinout a podepsat vaše společnost nebo nezávislý výrobce softwaru (ISV).

  * Soubor vstupní aplikace musí mít příponu **.ipa** nebo **.app**.

  * Vstupní aplikace musí být zkompilována pro iOS 11 nebo novější.

  * Vstupní aplikace nemůže být zašifrovaná.

  * Vstupní aplikace nemůže mít rozšířené atributy souborů.

  * Před zpracováním v nástroji Intune App Wrapping Tool musí mít aplikace nastavené nároky. [Nároky](https://developer.apple.com/library/content/documentation/Miscellaneous/Reference/EntitlementKeyReference/Chapters/AboutEntitlements.html) aplikaci poskytují další oprávnění a možnosti nad rámec těch, které se udělují obvykle. Pokyny najdete v části [Nastavení oprávnění aplikace](#setting-app-entitlements).

## <a name="apple-developer-prerequisites-for-the-app-wrapping-tool"></a>Požadavky na Apple Developer pro nástroj App Wrapping Tool

Abyste zabalené aplikace mohli distribuovat výhradně uživatelům vaší organizace, potřebujete účet v programu [Apple Developer Enterprise Program](https://developer.apple.com/programs/enterprise/) a několik entit pro podepisování aplikací propojených s vaším účtem Apple Developer.

Další informace o interní distribuci aplikací pro iOS uživatelům organizace najdete v oficiální příručce [Distributing Apple Developer Enterprise Program Apps](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppDistributionGuide/DistributingEnterpriseProgramApps/DistributingEnterpriseProgramApps.html#//apple_ref/doc/uid/TP40012582-CH33-SW1) (v angličtině).

K distribuci aplikací zabalených pomocí Intune budete potřebovat toto:

* Vývojářský účet v programu Apple Developer Enterprise Program

* Podpisový certifikát pro interní a ad hoc distribuci s platným identifikátorem týmu

  * Hodnotu hash SHA1 podpisového certifikátu budete potřebovat jako parametr do nástroje Intune App Wrapping Tool.


* Zřizovací profil pro interní distribuci

### <a name="steps-to-create-an-apple-developer-enterprise-account"></a>Postup při vytvoření účtu Apple Developer Enterprise

1. Přejděte na [web Apple Developer Enterprise Program](https://developer.apple.com/programs/enterprise/).

2. Vpravo nahoře na stránce klikněte na **Enroll** (Zaregistrovat).

3. Přečtěte si kontrolní seznam věcí, které k registraci potřebujete. Klikněte na **Start Your Enrollment** (Začít s registrací) v dolní části stránky.

4. **Přihlaste se** (Sign in) s Apple ID vaší organizace. Pokud žádné nemáte, klikněte na **Create Apple ID** (Vytvořit Apple ID).

5. Vyberte svůj **typ entity** (Entity Type) a klikněte na **Continue** (Pokračovat).

6. Vyplňte formulář údaji o vaší organizaci. Klikněte na **Pokračovat**. V tuto chvíli vás Apple kontaktuje, aby ověřil, že máte autorizaci registrovat svoji organizaci.

7. Po ověření klikněte na **Agree to License** (Souhlasím s licencí).

8. Po vyjádření souhlasu s licencí proces dokončete tak, že **program zakoupíte a aktivujete**.

9. Pokud jste agentem týmu (osoba, která se k programu Apple Developer Enterprise Program připojuje jménem vaší organizace), nejdříve svůj tým sestavte tak, že pozvete členy týmu a přiřadíte jim role. Informace o tom, jak se tým spravuje, najdete v dokumentaci Applu na stránce [Managing Your Developer Account Team](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppDistributionGuide/ManagingYourTeam/ManagingYourTeam.html#//apple_ref/doc/uid/TP40012582-CH16-SW1) (v angličtině).

### <a name="steps-to-create-an-apple-signing-certificate"></a>Postup vytvoření podpisového certifikátu Apple

1. Přejděte na [portál Apple Developer](https://developer.apple.com/).

2. Vpravo nahoře na stránce klikněte na **Account** (Účet).

3. **Přihlaste se** (Sign in) pomocí Apple ID organizace.

4. Klikněte na **Certificates, IDs & Profiles** (Certifikáty, ID a profily).

   ![Portál pro vývojáře Apple – certifikáty, ID & profily](./media/app-wrapper-prepare-ios/iOS-signing-cert-1.png)

5. Klikněte na ![znaménko plus portálu Apple Developer](./media/app-wrapper-prepare-ios/iOS-signing-cert-2.png) v pravém horním rohu, abyste mohli přidat certifikát iOS.

6. V části **Production** (Výroba) zvolte možnost vytvořit **In-House and Ad Hoc** (Interní a ad hoc) certifikát.

   ![Výběr vnitřního a ad hoc certifikátu](./media/app-wrapper-prepare-ios/iOS-signing-cert-3.png)

   >[!NOTE]
   >Pokud nechcete aplikaci distribuovat, ale jenom ji interně testovat, můžete místo certifikátu pro výrobu použít certifikát pro vývoj aplikací pro iOS. Když použijete certifikát pro vývoj, zajistěte, aby mobilní zřizovací profil odkazoval na zařízení, na která se bude aplikace instalovat.

7. V dolní části stránky klikněte na **Next** (Další).

8. Přečtěte si pokyny k vytváření **žádosti o podepsání certifikátu (CSR)** pomocí aplikace Klíčenka na počítači s macOS.

   ![Přečtěte si pokyny, jak vytvořit CSR](./media/app-wrapper-prepare-ios/iOS-signing-cert-4.png)

9. Pomocí pokynů výše vytvořte žádost o podepsání certifikátu. Na počítači s macOS spusťte aplikaci **Klíčenka**.

10. V nabídce macOS v horní části obrazovky přejděte na **Klíčenka > Průvodce certifikací > Vyžádat si certifikát od certifikační autority**.  

    ![Žádost o certifikát od certifikační autority v Klíčence](./media/app-wrapper-prepare-ios/iOS-signing-cert-5.png)

11. Pomocí pokynů na webu Apple Developer výše vytvořte soubor CSR. Uložte soubor CSR na svůj počítač s macOS.

    ![Zadejte informace pro certifikát, který požadujete.](./media/app-wrapper-prepare-ios/iOS-signing-cert-6.png)

12. Vraťte se na web Apple Developer. Klikněte na **Pokračovat**. Pak nahrajte soubor CSR.

13. Apple vygeneruje váš podpisový certifikát. Stáhněte a uložte si ho do počítače s macOS na nějaké snadno zapamatovatelné místo.

    ![Stažení podpisového certifikátu](./media/app-wrapper-prepare-ios/iOS-signing-cert-7.png)

14. Na certifikát, který jste si právě stáhli, poklikejte, aby se uložil do svazku klíčů.

15. Znovu otevřete **Klíčenku**. Vyhledejte certifikát zadáním jeho názvu do panelu hledání v pravém horním rohu. Klikněte pravým tlačítkem na danou položku, aby se zobrazila nabídka, a pak klikněte na **Get Info** (Získat informace). V ukázkových obrazovkách používáme místo certifikátu pro výrobu certifikát pro vývoj.

    ![Přidání certifikátu do svazku klíčů](./media/app-wrapper-prepare-ios/iOS-signing-cert-8.png)

16. Zobrazí se informační okno. Posuňte se až dolů a podívejte se pod popisek **Fingerprints** (Otisky). Zkopírujte řetězec **SHA1** (rozostřený), který se použije jako argument pro parametr „-c“ nástroje App Wrapping Tool.

    ![informace o iPhonu – řetězec SHA1 otisků prstů](./media/app-wrapper-prepare-ios/iOS-signing-cert-9.png)

### <a name="steps-to-create-an-in-house-distribution-provisioning-profile"></a>Postup vytvoření zřizovacího profilu pro interní distribuci

1. Přejděte zpátky na [portál účtu Apple Developer](https://developer.apple.com/account/) a **přihlaste** se pomocí Apple ID organizace.

2. Klikněte na **Certificates, IDs & Profiles** (Certifikáty, ID a profily).

3. Klikněte na ![znaménko plus portálu Apple Developer](./media/app-wrapper-prepare-ios/iOS-signing-cert-2.png) v pravém horním rohu, abyste mohli přidat zřizovací profil iOS.

4. V části **Distribution** (Distribuce) zvolte možnost vytvořit **In House** (Interní) zřizovací profil.

   ![Výběr interního zřizovacího profilu](./media/app-wrapper-prepare-ios/iOS-provisioning-profile-1.png)

5. Klikněte na **Pokračovat**. Nezapomeňte propojit předtím vygenerovaný podpisový certifikát se zřizovacím profilem.

6. Podle pokynů si stáhněte svůj profil (s příponou .mobileprovision) na svůj počítač s macOS.

7. Uložte si soubor na snadno zapamatovatelné místo. Tento soubor se využije při používání nástroje App Wrapping Tool jako parametr -p.

## <a name="download-the-app-wrapping-tool"></a>Stažení nástroje App Wrapping Tool

1. Stáhněte si soubory pro nástroj App Wrapping Tool z [GitHubu](https://github.com/msintuneappsdk/intune-app-wrapping-tool-ios) do počítače s macOS.

2. Poklikejte na soubor **Microsoft Intune App Wrapping Tool for iOS.dmg**. Zobrazí se okno s licenční smlouvou s koncovým uživatelem (EULA). Dokument si pozorně přečtěte.

3. Výběrem možnosti **Souhlasím** přijměte podmínky smlouvy EULA. Tím připojíte balíček k počítači.

## <a name="run-the-app-wrapping-tool"></a>Spuštění nástroje App Wrapping Tool

### <a name="use-terminal"></a>Použití terminálu

Otevřete terminál macOS a spusťte tento příkaz:

```bash
/Volumes/IntuneMAMPackager/Contents/MacOS/IntuneMAMPackager -i /<path of input app>/<app filename> -o /<path to output folder>/<app filename> -p /<path to provisioning profile> -c <SHA1 hash of the certificate> [-b [<output app build string>]] [-v] [-e] [-x /<array of extension provisioning profile paths>]
```

> [!NOTE]
> Některé parametry jsou volitelné, jak je vidět v následující tabulce.

**Příklad:** V tomto ukázkovém příkazu se nástroj App Wrapping Tool spouští v aplikaci s názvem MyApp.ipa. Profil zřizování a algoritmus hash SHA-1 podepisujícího certifikátu jsou definovány a použijí se k podepsání zabalené aplikace. Vytvoří se výstupní aplikace (MyApp_Wrapped.ipa), která se uloží do složky Desktop.

```bash
./IntuneMAMPackager/Contents/MacOS/IntuneMAMPackager -i ~/Desktop/MyApp.ipa -o ~/Desktop/MyApp_Wrapped.ipa -p ~/Desktop/My_Provisioning_Profile_.mobileprovision -c "12 A3 BC 45 D6 7E F8 90 1A 2B 3C DE F4 AB C5 D6 E7 89 0F AB"  -v true
```

### <a name="command-line-parameters"></a>Parametry příkazového řádku

V nástroji App Wrapping Tool můžete používat následující parametry příkazového řádku:

|Vlastnost|Jak ji použít|
|---------------|--------------------------------|
|**– i**|`<Path of the input native iOS application file>`. Název souboru musí končit na .app nebo .ipa. |
|**– o**|`<Path of the wrapped output application>` |
|**-p**|`<Path of your provisioning profile for iOS apps>`|
|**-c**|`<SHA1 hash of the signing certificate>`|
|**-h**| Zobrazí podrobné informace o použití dostupných vlastností příkazového řádku nástroje App Wrapping. |
|**– AA**|Volitelné `<Authority URI of the input app if the app uses the Azure Active Directory Authentication Library>` tj. `login.windows.net/common` |
|**– AC**|Volitelné `<Client ID of the input app if the app uses the Azure Active Directory Authentication Library>` Toto je identifikátor GUID v poli ID klienta je ze seznamu vaší aplikace v okně registrace aplikace. |
|**– ar**|Volitelné `<Redirect/Reply URI of the input app if the app uses the Azure Active Directory Authentication Library>` Toto je identifikátor URI přesměrování konfigurovaný v registraci vaší aplikace. Obvykle by to byl protokol adresy URL aplikace, kterou Microsoft Authenticator aplikace vrátila po zprostředkované ověřování. |
|**-v**| (Nepovinná) Zobrazí v konzole podrobné zprávy. Tento příznak doporučujeme používat k ladění všech chyb. |
|**-e**| (Nepovinná) Tímto příznakem zajistíte, že nástroj App Wrapping při zpracování aplikace odebere chybějící oprávnění. Další podrobnosti najdete v tématu [Nastavení nároků aplikace](#setting-app-entitlements) .|
|**-xe**| (Nepovinná) Zobrazí informace o rozšířeních iOS v aplikaci a o oprávněních, která potřebujete k jejich používání. Další podrobnosti najdete v tématu [Nastavení nároků aplikace](#setting-app-entitlements) . |
|**– x**| (Nepovinná) `<An array of paths to extension provisioning profiles>` Tuto vlastnost použijte v případě, že vaše aplikace potřebuje zřizovací profily rozšíření.|
|**– b**|(Nepovinná) Pokud chcete, aby měla zabalená výstupní aplikace stejnou verzi balíčku jako vstupní aplikace, použijte vlastnost -b bez argumentu (nedoporučuje se to). <br/><br/> Když chcete, aby měla zabalená aplikace vlastní verzi balíčku (CFBundleVersion), použijte vlastnost `-b <custom bundle version>`. Pokud se rozhodnete zadat vlastní CFBundleVersion, je vhodné zvýšit CFBundleVersion nativní aplikace o nejmenší významnou součást, například 1.0.0-> 1.0.1. |
|**– Citrix**|Volitelné Zahrňte sadu Citrix XenMobile App SDK (variantu jenom sítě). Abyste mohli použít tuto možnost, musíte mít nainstalovanou [sadu Citrix MDX Toolkit](https://docs.citrix.com/en-us/mdx-toolkit/about-mdx-toolkit.html) . |
|**-f**|(Nepovinná) `<Path to a plist file specifying arguments.>` Pokud se rozhodnete zadat zbývající vlastnosti nástroje IntuneMAMPackager, jako je -i, -o a -p, šablonou plist, použijte tento příznak před souborem [plist](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/PropertyLists/Introduction/Introduction.html). Další informace najdete v části, která vysvětluje použití souboru plist k zadání argumentů. |

### <a name="use-a-plist-to-input-arguments"></a>Zadání argumentů pomocí souboru plist

App Wrapping Tool se dá jednoduše spustit zadáním všech argumentů příkazu do souboru [plist](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/PropertyLists/Introduction/Introduction.html). Formát souboru plist je podobný formátu XML. Můžete ho použít k zadání argumentů příkazového řádku s využitím rozhraní formuláře.

Ve složce IntuneMAMPackager/Contents/MacOS otevřete `Parameters.plist` (prázdná šablona souboru plist). Použijte k tomu textový editor nebo Xcode. Zadejte požadované argumenty následujících klíčů:

| Klíč souboru plist | Typ |  Výchozí hodnota | Poznámky |
|------------------|-----|--------------|-----|
| Input Application Package Path |Řetězec|empty| Odpovídá vlastnosti -i.|
| Output Application Package Path |Řetězec|empty| Odpovídá vlastnosti -o.|
| Provisioning Profile Path |Řetězec|empty| Odpovídá vlastnosti -p.|
| SHA-1 Certificate Hash |Řetězec|empty| Odpovídá vlastnosti -c.|
| Autorita ADAL |Řetězec|empty| Stejné jako-AA|
| ID klienta ADAL |Řetězec|empty| Stejné jako-AC|
| Identifikátor URI odpovědi ADAL |Řetězec|empty| Stejné jako – ar|
| Verbose Enabled |Logická hodnota|false (nepravda)| Odpovídá vlastnosti -v.|
| Remove Missing Entitlements |Logická hodnota|false (nepravda)| Odpovídá vlastnosti -c.|
| Zabránit výchozí aktualizaci sestavení |Logická hodnota|false (nepravda)| Odpovídá použití vlastnosti -b bez argumentů.|
| Build String Override |Řetězec|empty| Vlastní verze balíčku (CFBundleVersion) zabalené výstupní aplikace|
| Zahrnout sadu Citrix XenMobile App SDK (jenom síť variant)|Logická hodnota|false (nepravda)| Stejné jako – Citrix|
| Extension Provisioning Profile Paths |Pole řetězců|empty| Pole zřizovacích profilů rozšíření pro aplikaci

Spusťte nástroj IntuneMAMPackager a jako jediný argument použijte soubor plist:

```bash
./IntuneMAMPackager –f Parameters.plist
```

### <a name="post-wrapping"></a>Po zabalení

Po dokončení procesu zabalení se zobrazí zpráva The application was successfully wrapped (Zabalení aplikace proběhlo úspěšně.). Pokud dojde k chybě, zobrazte nápovědu v tématu [chybové zprávy](#error-messages-and-log-files) .

Zabalená aplikace se uloží do výstupní složky, kterou jste určili předtím. Aplikaci můžete nahrát do konzoly pro správu Intune a přidružit ji k zásadě správy mobilní aplikace.

> [!IMPORTANT]
> Pokud je už v Intune nasazená starší (zabalená nebo nativní) verze aplikace, můžete tuto starší verzi zkusit při nahrávání zabalené aplikace aktualizovat. Když se to nepovede, nahrajte aplikaci jako novou a starší verzi odstraňte.

Teď můžete aplikaci nasadit do skupin uživatelů a zásad ochrany cílové aplikace. Aplikace se bude spouštět na zařízení pomocí zásad ochrany aplikace, které jste určili.

## <a name="how-often-should-i-rewrap-my-ios-application-with-the-intune-app-wrapping-tool"></a>Jak často mám balit svoji aplikaci pro iOS pomocí nástroje Intune App Wrapping Tool?

Hlavní situace, ve kterých potřebujete znovu zabalit svoje aplikace, jsou tyto:

* Aplikace sama vydala novou verzi. Do konzoly Intune byla zabalena a nahrána předchozí verze aplikace.
* Vydala se nová verze nástroje Intune App Wrapping Tool pro iOS, která přináší důležité opravy chyb nebo nové specifické funkce zásad ochrany aplikací Intune. Pro [Microsoft Intune App Wrapping Tool pro iOS](https://github.com/msintuneappsdk/intune-app-wrapping-tool-ios) se toto děje každých 6–8 týdnů prostřednictvím úložiště GitHub.

Pro iOS/iPadOS, přestože je možné zabalit jiný profil pro registraci a zřízení než původní použitý k podepsání aplikace, pokud se oprávnění uvedená v aplikaci nezahrnují do nového zřizovacího profilu, balení se nezdaří. Když použijete možnost příkazového řádku "-e", která odebere z aplikace chybějící oprávnění, aby se vynutilo selhání v tomto scénáři, mohlo by dojít k porušení funkčnosti v aplikaci.

Mezi osvědčené postupy pro opětovné balení patří:

* Zajistěte, aby jiný profil zřizování měl všechna požadovaná oprávnění jako každý předchozí profil zřizování. 

## <a name="error-messages-and-log-files"></a>Chybové zprávy a soubory protokolu

K řešení potíží s nástrojem App Wrapping použijte následující informace.

### <a name="error-messages"></a>Chybové zprávy

Pokud se nástroji App Wrapping nepodaří aplikaci zabalit, zobrazí konzola některou z následujících chybových zpráv:

|Chybová zpráva|Další informace|
|-----------------|--------------------|
|Je nutné zadat platný profil zřizování iOS.|Váš profil zřizování nemusí být platný. Zkontrolujte, že máte pro zařízení správná oprávnění a že máte správně zaměřený profil pro vývoj nebo distribuci. Je taky možné, že vypršela platnost vašeho profilu zřizování.|
|Zadejte platný vstupní název aplikace.|Ujistěte se, že je správný název vstupní aplikace, který jste zadali.|
|Zadejte platnou cestu k výstupní aplikaci.|Ujistěte se, jestli existuje cesta k výstupní aplikace, kterou jste zadali, a jestli je správná.|
|Zadejte platný vstupní profil zřizování.|Ujistěte se, jestli jste zadali platný název a příponu profilu zřizování. V profilu zřizování mohou chybět oprávnění nebo jste neuvedli parametr příkazového řádku –p.|
|Nenašla se zadaná vstupní aplikace. Zadejte platný název a cestu vstupní aplikace.|Přesvědčte se, jestli je cesta ke vstupní aplikaci platná a existuje. Ujistěte se, jestli vstupní aplikace existuje v tomto umístění.|
|Zadaný soubor vstupního profilu zřizování se nenašel. Zadejte platný soubor vstupního profilu zřizování.|Ujistěte se, jestli je cesta k vstupnímu souboru profilu zřizování platná a jestli existuje soubor, který jste zadali.|
|Zadaná složka výstupní aplikace se nenašla. Zadejte platnou cestu k výstupní aplikaci.|Ujistěte se, jestli je zadaná výstupní cesta platná a existuje.|
|Výstupní aplikace nemá příponu **. ipa** .|Nástroj App Wrapping přijímá jenom aplikace s příponou **.app** a **.ipa**. Ujistěte se, že výstupní má platnou příponu.|
|Je zadaný neplatný podpisový certifikát. Zadejte platný podpisový certifikát Apple.|Ujistěte se, že jste stáhli správný podpisový certifikát z portálu pro vývojáře Apple. Platnost vašeho certifikátu nejspíš vypršela nebo je možné, že chybí veřejný nebo privátní klíč. Pokud můžete certifikát Apple a zřizovací profil použít ke správnému podepsání aplikace v Xcodu, platí tyto položky i pro nástroj App Wrapping.|
|Zadaná vstupní aplikace je neplatná. Zadejte platnou aplikaci.|Ujistěte se, že máte platnou aplikaci iOS, která je kompilovaná jako soubor .app nebo .ipa.|
|Zadaná vstupní aplikace je zašifrovaná. Zadejte platnou nezašifrovanou aplikaci.|Nástroj App Wrapping nepodporuje šifrované aplikace. Použijte aplikaci, která šifrovaná není.|
|Zadaná vstupní aplikace není ve formátu Position Independent Executable (PIE). Zadejte platnou aplikaci ve formátu PIE.|Aplikace ve formátu Position Independent Executable (PIE) je možné při spuštění načíst s náhodnou adresou v paměti. Může to být výhodné kvůli zabezpečení. Další informace o výhodách týkajících se zabezpečení najdete v dokumentaci pro vývojáře Apple.|
|Zadaná vstupní aplikace už je zabalená. Zadejte platnou nezabalenou aplikaci.|Nejde zpracovat aplikaci, kterou už nástroj zpracoval. Pokud chcete ke aplikaci znovu zpracovat, spusťte nástroj pomocí původní verze aplikace.|
|Zadaná vstupní aplikace není podepsaná. Zadejte platnou podepsanou aplikaci.|Nástroj pro zabalení aplikace vyžaduje, aby aplikace byla podepsaná. Vyhledejte v dokumentaci pro vývojáře, jak podepsat zabalenou aplikaci.|
|Zadaná vstupní aplikace musí být ve formátu .ipa nebo .app.|Nástroj pro zabalení aplikace přijímá jenom přípony .app a .ipa. Ujistěte se, že vstupní soubor má platnou příponu a je kompilovaný jako soubor .app nebo .ipa.|
|Vstupní aplikace, kterou jste zadali, už je zabalená a má nejnovější verzi šablony zásad.|Nástroj App Wrapping znovu nezabalí stávající zabalenou aplikaci do nejnovější verze šablony zásad.|
|UPOZORNĚNÍ: Nezadali jste hash SHA1 certifikátu. Ujistěte se, že zabalená aplikace je před nasazením podepsaná.|Ověřte, že jste za příznakem příkazového řádku –c zadali platný hash SHA1. |

### <a name="collecting-logs-for-your-wrapped-applications-from-the-device"></a>Shromažďování protokolů pro zabalené aplikace ze zařízení
Následující postup vám pomůže získat protokoly zabalených aplikací, které vám pomůžou při řešení potíží.

1. Na zařízení přejděte do aplikace Nastavení v iOSu a vyberte podnikovou aplikaci.
2. Přepněte **diagnostickou konzolu** na **Zapnuto**.
3. Spusťte podnikovou aplikaci.
4. Klikněte na odkaz „Začínáme“.
5. Teď můžete protokoly sdílet prostřednictvím e-mailu nebo je můžete kopírovat do umístění na OneDrivu.

> [!NOTE]
> Funkce protokolování je zapnutá pro aplikace zabalené nástrojem Intune App Wrapping Tool verze 7.1.13 nebo vyšší.

### <a name="collecting-crash-logs-from-the-system"></a>Shromažďování protokolů selhání ze systému

Vaše aplikace může přihlašovat užitečné informace do konzoly klientského zařízení iOS. Tyto informace jsou užitečné v případě, že máte problémy s aplikací a potřebujete určit, jestli problém souvisí s nástrojem pro zabalení aplikace nebo samotným aplikací. Pro načtení těchto informací použijte následující kroky:

1. Reprodukujte problém spuštěním aplikace.

2. Shromážděte výstup konzoly podle pokynů společnosti Apple pro [ladění nasazených aplikací pro iOS](https://developer.apple.com/library/ios/qa/qa1747/_index.html).

Zabalené aplikace taky uživatelům nabídnou možnost odeslat protokoly přímo ze zařízení prostřednictvím e-mailu v případě chyby aplikace. Protokoly můžou uživatelé poslat ke kontrole vám a vy je případně můžete přeposlat Microsoftu.

### <a name="certificate-provisioning-profile-and-authentication-requirements"></a>Požadavky na certifikát, profil pro zřizování a ověřování

Aby bylo možné zaručit plnou funkčnost nástroje App Wrapping Tool pro iOS, je potřeba splnit určité požadavky.

|Požadavek|Podrobnosti|
|---------------|-----------|
|Profil pro zřizování iOS|Zkontrolujte platnost zřizovacího profilu, než ho zahrnete. Při zpracování aplikace pro iOS nástroj App Wrapping nekontroluje, jestli vypršela platnost zřizovacího profilu. Když je zadaný profil zřizování s ukončenou platností, bude nástroj pro zabalení aplikace zahrnovat tento profil a vy nepoznáte, jestli existuje problém, dokud neselže instalace aplikace na zařízení s iOSem.|
|Podpisový certifikát iOS|Před zadáním podpisového certifikátu zkontrolujte jeho platnost. Nástroj při zpracování aplikací pro iOS nekontroluje, jestli nevypršela platnost certifikátu. Pokud je zadaný hash pro prošlý certifikát, nástroj zpracuje a podepíše aplikaci, ale nenainstaluje ji na zařízení.<br /><br />Zkontrolujte, jestli se certifikát dodaný k podpisu zabalené aplikace shoduje se zřizovacím profilem. Nástroj neověřuje, jestli pro certifikát poskytnutý k podepsání zabalené aplikace existuje shoda ve zřizovacím profilu.|
|Authentication|Aby šifrování fungovalo, musí mít zařízení PIN. Když se uživatel zařízení, do kterého jste nasadili zabalenou aplikaci, dotkne stavového řádku, musí se znovu přihlásit přes svůj pracovní nebo školní účet. Podle výchozí zásady zabalené aplikace probíhá *ověřování při opakovaném spuštění*. V iOSu se každé externí oznámení (třeba při telefonním hovoru) zpracuje tak, že se aplikace ukončí a potom znovu spustí.

## <a name="setting-app-entitlements"></a>Nastavení oprávnění aplikace

Než aplikaci zabalíte, můžete jí udělit taková *oprávnění*, kterými získá další oprávnění a funkce nad rámec obvyklých možností. Při podepisování kódu se pomocí *souboru oprávnění* určí v aplikaci speciální oprávnění (například přístup ke sdílenému řetězci klíčů). Konkrétní služby App Services označované jako *Možnosti* jsou v rámci Xcode při vývoji aplikací povolené. Jakmile se tyto schopnosti povolí, odrazí se to v souboru oprávnění. Další informace o oprávněních a schopnostech najdete v článku věnovaném [přidání schopností](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html) na webu iOS Developer Library. Úplný seznam podporovaných funkcí najdete v tématu [podporované funkce](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/SupportedCapabilities/SupportedCapabilities.html).

### <a name="supported-capabilities-for-the-app-wrapping-tool-for-ios"></a>Podporované schopnosti nástroje App Wrapping pro iOS

|Schopnost|Popis|Doporučené pokyny|
|--------------|---------------|------------------------|
|Skupiny aplikací|Ve skupinách aplikací můžete více aplikacím povolit přístup ke sdíleným kontejnerům a povolit mezi aplikacemi další komunikaci na úrovni procesů.<br /><br />Pokud chcete povolit skupiny aplikací, otevřete podokno **Schopnosti** a v části **Skupiny aplikací** klikněte na **ZAPNUTO**. Můžete přidat nové skupiny aplikací nebo vybrat stávající.|U skupin aplikací používejte zpětný zápis DNS:<br /><br />*group.com.companyName.AppGroup*|
|Režimy pozadí|Pokud povolíte režimy pozadí, může vaše aplikace pro iOS běžet dál na pozadí.||
|Ochrana dat|Ochrana dat přidá do souborů, které aplikace iOS uložení na disk, úroveň zabezpečení. Ochrana dat využívá integrovaný šifrovací hardware přítomný v určitých zařízeních k ukládání souborů na disk v zašifrovaném formátu. Pokud má vaše aplikace používat ochranu dat, musí být zřízená.||
|Nákupy v aplikaci|Nákupy v aplikaci vloží přímo do aplikace obchod tím, že vám umožní připojit se k obchodu a bezpečně zpracovávat platby uživatele. Nákupy v aplikaci umožňují inkasovat platby za rozšířené funkce a další obsah využitelný v aplikaci.||
|Sdílení řetězce klíčů|Pokud povolíte sdílení řetězce klíčů, můžete aplikace pomocí řetězce klíčů sdílet hesla s jinými aplikacemi, které vyvinul váš tým.|Při sdílení řetězce klíčů použijte zpětný způsob zápisu DNS:<br /><br />*com.companyName.KeychainGroup*|
|Osobní VPN|Můžete povolit osobní síť VPN, aby mohla vaše aplikace vytvářet a řídit vlastní systémovou konfiguraci sítě VPN s využitím rámce pro rozšíření sítě.||
|Nabízená oznámení|Služba APNs (Apple Push Notification Service) umožňuje aplikaci, která není spuštěná v popředí, informovat uživatele o tom, že má pro uživatele informace.|Nabízená oznámení fungují jenom tehdy, když pro konkrétní aplikaci použijete profil zřizování.<br /><br />Postupujte podle kroků v [dokumentaci pro vývojáře Apple](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).|
|Konfigurace bezdrátového příslušenství|Když povolíte konfiguraci bezdrátového příslušenství, přidáte do svého projektu rozhraní externího příslušenství a umožníte tím aplikaci nastavit příslušenství MFi s připojením Wi-Fi.||

### <a name="steps-to-enable-entitlements"></a>Postup pro povolení oprávnění

1. Povolení schopností v aplikaci:

    a.  V Xcode přejděte na cíl vaší aplikace a klikněte na **Možnosti**.

    b.  Zapněte příslušné schopnosti. Podrobné informace o jednotlivých schopnostech a o tom, jak určit správné hodnoty, najdete v článku věnovaném [přidání schopností](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html) na webu iOS Developer Library.

    c.  Poznamenejte si všechna ID, která v průběhu procesu vytvoříte. Můžou se označovat také jako hodnoty `AppIdentifierPrefix`.

    d.  Sestavte a podepište aplikaci, kterou chcete zabalit.

2. Ve svém profilu pro zřizování povolte oprávnění:

    a.  Přihlaste se do Centra pro vývojáře Apple.

    b.  Vytvořte pro svoji aplikaci profil pro zřizování. Pokyny najdete v tématu [postup získání požadavků pro nástroj pro zabalení aplikace Intune pro iOS](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/25/how-to-obtain-the-prerequisites-for-the-intune-app-wrapping-tool-for-ios/).

    c.  V profilu pro zřizování povolte stejná oprávnění, jaká máte ve své aplikaci. Budete muset zadat stejná ID (hodnoty `AppIdentifierPrefix`), která jste zadali během vývoje aplikace. 

    d.  Dokončete průvodce zřizovacím profilem a stáhněte si soubor.

3. Ujistěte se, že jste splnili všechny předpoklady, a zabalte aplikaci.

### <a name="troubleshoot-common-errors-with-entitlements"></a>Řešení potíží s běžnými chybami spojenými s oprávněními

Pokud nástroj App Wrapping pro iOS zobrazí chybu oprávnění, zkuste vyřešit potíže následujícími postupy.

|Problém|Příčina|Řešení|
|---------|---------|--------------|
|Nepodařilo se analyzovat oprávnění vygenerovaná vstupní aplikací.|Nástroj App Wrapping nemůže přečíst soubor oprávnění extrahovaný z aplikace. Soubor oprávnění může být poškozený.|Zkontrolujte soubor oprávnění pro svoji aplikaci. Následující pokyny vysvětlují postup. Při kontrole souboru oprávnění hledejte případy poškozené syntaxe. Soubor by měl být ve formátu XML.|
|V profilu pro zřizování chybí oprávnění (s uvedením chybějících oprávnění). Znovu zabalte aplikaci pomocí profilu pro zřizování, který má tato oprávnění.|Oprávnění povolená v profilu pro zřizování neodpovídají schopnostem povoleným v aplikaci. Tyto rozdíly platí také pro ID přidružená k určitým schopnostem (například skupiny aplikací a přístup k řetězci klíčů).|Obecně platí, že můžete vytvořit nový profil pro zřizování, který povolí stejné schopnosti jako aplikace. Pokud ID v profilu neodpovídají ID v aplikaci, nástroj App Wrapping tato ID nahradí, pokud to bude možné. Pokud se chyba zobrazuje i po vytvoření nového zřizovacího profilu, můžete zkusit aplikaci odebrat oprávnění parametrem –e (viz část Použití parametru –e k odebrání oprávnění z aplikace).|

### <a name="find-the-existing-entitlements-of-a-signed-app"></a>Vyhledání stávajících oprávnění v podepsané aplikaci

Postup pro kontrolu oprávnění v podepsané aplikaci a profilu pro zřizování:

1. Najděte soubor .ipa a změňte jeho příponu na .zip.

2. Rozbalte soubor .zip. Vznikne tak složka datové části, která obsahuje sadu .app.

3. Ke kontrole oprávnění u sady .app použijte nástroj na podpis kódu, kde `YourApp.app` je skutečný název vaší sady .app:

    ```bash
    codesign -d --entitlements :- "Payload/YourApp.app"
    ```

4. Ke kontrole oprávnění u vloženého zřizovacího profilu aplikace použijte bezpečnostní nástroj, kde `YourApp.app` je skutečný název vaší sady .app:

    ```bash
    security cms -D -i "Payload/YourApp.app/embedded.mobileprovision"
    ```

### <a name="remove-entitlements-from-an-app-by-using-the-e-parameter"></a>Použití parametru –e k odebrání oprávnění z aplikace

Tento příkaz odebere z aplikace všechny povolené schopnosti, které nejsou v souboru oprávnění. Pokud odeberete oprávnění, které aplikace využívá, může ji to poškodit. Příkladem, kdy je možné odebrat chybějící schopnosti, je aplikace vytvořená dodavatelem, která má ve výchozím nastavení všechny schopnosti.

```bash
./IntuneMAMPackager/Contents/MacOS/IntuneMAMPackager –i /<path of input app>/<app filename> -o /<path to output folder>/<app filename> –p /<path to provisioning profile> –c <SHA1 hash of the certificate> -e
```

## <a name="security-and-privacy-for-the-app-wrapping-tool"></a>Zabezpečení a ochrana osobních údajů nástrojem App Wrapping

Při používání nástroje App Wrapping použijte následující doporučené postupy pro zabezpečení a ochranu osobních údajů.

- Podpisový certifikát, zřizovací profil a obchodní aplikace, které zadáte, musí být na stejném počítači s Mac OS, na jakém spouštíte nástroj App Wrapping. Pokud soubory leží na cestě UNC, ověřte, že jsou pro počítač s Mac OS přístupné. Cesta musí být zabezpečená pomocí protokolu IPsec nebo podepsání SMB.

    Zabalená aplikace naimportovaná do konzoly pro správu by měla být na počítači, na kterém jste nástroj spustili. Pokud je soubor v cestě UNC, zajistěte, aby byl přístupný na počítači se spuštěnou konzolou pro správu. Cesta musí být zabezpečená pomocí protokolu IPsec nebo podepsání SMB.

- Prostředí, do kterého nástroj App Wrapping stahujete z úložiště GitHubu, musí být zabezpečené protokolem IPsec nebo SMB.

- Zpracovávaná aplikace musí kvůli zajištění ochrany před útoky pocházet z důvěryhodného zdroje.

- Zkontrolujte, že výstupní složka zadaná v nástroji App Wrapping je zabezpečená. To platí zejména v případě, že jde o vzdálenou složku.

- V aplikacích pro iOS s dialogovým oknem pro nahrávání souborů mohou uživatelé obejít omezení aplikace, která se vztahují na vyjmutí, kopírování a vložení. Uživatel může například pomocí dialogového okna pro nahrání souboru nahrát snímek obrazovky dat aplikace.

- Když ze zabalené aplikace monitorujete složku dokumentů v zařízení, může se zobrazit složka s názvem .msftintuneapplauncher. Pokud tuto složku změníte nebo odstraníte, může to mít vliv na správné fungování omezených aplikací.

## <a name="intune-app-wrapping-tool-for-ios-with-citrix-mdx-mvpn"></a>Nástroj Intune App Wrapping pro iOS s Citrix MDX mVPN

Tato funkce je integrací s obálkou aplikace Citrix MDX pro iOS/iPadOS. Tato integrace je jednoduše další volitelný příznak příkazového řádku (`-citrix`) k obecným nástrojům Intune App Wrapping Tools.

### <a name="requirements"></a>Požadavky

Abyste mohli použít příznak `-citrix`, musíte také na stejný počítač s macOS nainstalovat [obálku aplikací (app wrapper) Citrix MDX pro iOS](https://docs.citrix.com/en-us/mdx-toolkit/10/xmob-mdx-kit-app-wrap-ios.html). Soubory ke stažení najdete na webu [Citrix XenMobile Downloads](https://www.citrix.com/downloads/xenmobile/). Přístup k nim získají jenom zákazníci Citrixu po přihlášení. Zajistěte, aby se do výchozího umístění nainstalovalo toto: `/Applications/Citrix/MDXToolkit`. 

> [!NOTE] 
> Podpora integrace Intune a Citrixu je omezená jenom na zařízení s iOSem 10+.

### <a name="use-the--citrix-flag"></a>Použití příznaku `-citrix`

Jednoduše spusťte obecný příkaz pro balení aplikací s připojeným příznakem `-citrix`. Příznak `-citrix` momentálně nepřijímá žádné argumenty.

**Formát použití:**

```bash
./IntuneMAMPackager/Contents/MacOS/IntuneMAMPackager -i /<path of input app>/<app filename> -o /<path to output folder>/<app filename> -p /<path to provisioning profile> -c <SHA1 hash of the certificate> [-b [<output app build string>]] [-v] [-e] [-x /<array of extension provisioing profile paths>] [-citrix]
```

**Příklad příkazu**:

```bash
./IntuneMAMPackager/Contents/MacOS/IntuneMAMPackager -i ~/Desktop/MyApp.ipa -o ~/Desktop/MyApp_Wrapped.ipa -p ~/Desktop/My_Provisioning_Profile_.mobileprovision -c 12A3BC45D67EF8901A2B3CDEF4ABC5D6E7890FAB  -v true -citrix
```

## <a name="see-also"></a>Viz také

- [Rozhodování o způsobu přípravy aplikací na správu mobilních aplikací v Microsoft Intune](apps-prepare-mobile-application-management.md)
- [Běžné otázky, problémy a řešení se zásadami a profily zařízení](../configuration/device-profile-troubleshoot.md)
- [Použití sady SDK k povolení správy mobilních aplikací pro aplikace](app-sdk.md)
