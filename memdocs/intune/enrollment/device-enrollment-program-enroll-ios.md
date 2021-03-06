---
title: Registrace zařízení s iOS/iPadOS – automatický zápis zařízení
titleSuffix: Microsoft Intune
description: Naučte se registrovat zařízení s iOS a iPadOS vlastněná společností pomocí automatického zápisu zařízení.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/10/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7ddbf360-0c61-11e8-ba89-0ed5f89f718b
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 96f6c2a40fa373c73aac30061ddaaaa1ddf0c8a6
ms.sourcegitcommit: 37dc6b78de8bb904b83a9d571f3c9f414b54f321
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "90848398"
---
# <a name="automatically-enroll-iosipados-devices-with-apples-automated-device-enrollment"></a>Automatická registrace zařízení se systémem iOS/iPadOS pomocí Automatické registrace zařízení společnosti Apple

> [!IMPORTANT]
> Apple se nedávno změnil z použití programu Apple Program registrace zařízení (DEP) na Apple Automated Device Enrollment (ADE). Intune je v procesu aktualizace uživatelského rozhraní Intune, aby odrážel. Dokud tyto změny nedokončíte, budete na portálu Intune dál zobrazovat *program registrace zařízení* . Všude, kde se zobrazuje, teď používá automatický zápis zařízení.

Můžete nastavit Intune pro registraci zařízení se systémem iOS/iPadOS zakoupená prostřednictvím [automatického zápisu zařízení (ADE)](https://deploy.apple.com)společnosti Apple. Automatický zápis zařízení vám umožňuje registrovat velké počty zařízení, aniž byste je museli dotýkat. Zařízení, jako jsou iPhone, iPady a MacBooks, se dají dodávat přímo uživatelům. Když uživatel zapne zařízení, Pomocník s nastavením, který zahrnuje typické prostředí pro produkty Apple, běží s předem nakonfigurovaným nastavením a zařízení se zaregistruje do správy.

Pokud chcete povolit ADE, použijte portál Intune i [Apple Business Manager (ABM)](https://business.apple.com/) nebo [Apple School Manager (ASM)](https://school.apple.com/) . Vyžaduje se seznam sériových čísel nebo čísel nákupních objednávek, abyste mohli zařízení přiřadit do Intune pro správu na portálu Apple. V Intune vytvoříte profily zápisu ADE obsahující nastavení, která se v zařízeních při registraci používají. ADE nelze použít s účtem [správce registrace zařízení](device-enrollment-manager-enroll.md) .

> [!NOTE]
> ADE nastaví konfigurace zařízení, které koncoví uživatelé nemusí nutně odebrat. Před [migrací do ADE](../fundamentals/migration-guide-considerations.md)se proto musí zařízení vymazat a vrátit ho do předem připraveného (nového) stavu.

## <a name="automated-device-enrollment-and-the-company-portal"></a>Automatický zápis zařízení a Portál společnosti

Zápisy přes ADE nejsou kompatibilní s verzí aplikace Portál společnosti App Storu. Uživatelům můžete poskytnout přístup k aplikaci Portál společnosti na zařízení ADE. Tento přístup můžete chtít poskytnout uživatelům, aby si zvolili podnikové aplikace, které chtějí používat na svém zařízení, nebo aby mohli dokončit proces registrace pomocí moderního ověřování. 

Pokud chcete povolit moderní ověřování během registrace, nahrajte aplikaci do zařízení pomocí **portál společnosti instalace** pomocí programu VPP (Volume purchase program) v profilu ADE. Další informace najdete v tématu [Automatická registrace zařízení s iOS/iPadOS pomocí ADE společnosti Apple](device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).

Pokud chcete povolit, aby se Portál společnosti automaticky aktualizovala a poskytovala aplikace Portál společnosti na zařízeních, která jsou už zaregistrovaná v ADE, nasaďte aplikaci Portál společnosti přes Intune jako povinnou aplikaci VPP (Volume purchase program) s použitou [zásadou konfigurace aplikace](../apps/app-configuration-policies-use-ios.md) .

## <a name="what-is-supervised-mode"></a>Co je režim Pod dohledem?

Apple představil režim pod dohledem v iOS/iPadOS 5. Zařízení s iOS/iPadOS v režimu pod dohledem je možné spravovat s dalšími ovládacími prvky, jako je například blokování snímku obrazovky a blokování instalace aplikací z App Storu. To je zvlášť užitečné pro zařízení vlastněná firmou. Intune podporuje konfiguraci zařízení pro režim pod dohledem jako součást ADE.

Podpora pro zařízení s nekontrolovaným ADE je v iOS/iPadOS 11 zastaralá. V systému iOS/iPadOS 11 a novějších by měly být nakonfigurovaná zařízení ADE vždy pod dohledem. Příznak *IS_SUPERVISED* ADE se bude ignorovat s iOS/iPadOS 13,0 a novějším. Všechna zařízení s iOS/iPadOS s verzí 13,0 a novější se po registraci pomocí automatického zápisu zařízení automaticky dohlíží pod dohledem. 

<!--
**Steps to enable enrollment programs from Apple**
1. [Get an Apple DEP token and assign devices](#get-the-apple-dep-token)
2. [Create an enrollment profile](#create-an-apple-enrollment-profile)
3. [Synchronize DEP-managed devices](#sync-managed-device)
4. [Assign DEP profile to devices](#assign-an-enrollment-profile-to-devices)
5. [Distribute devices to users](#end-user-experience-with-managed-devices)
-->
## <a name="prerequisites"></a>Požadavky
- Zařízení zakoupená v nástroji [ADE společnosti Apple](https://deploy.apple.com)
- [Autorita pro správu mobilních zařízení (MDM)](../fundamentals/mdm-authority-set.md)
- [Apple MDM push Certificate](apple-mdm-push-certificate-get.md)

## <a name="supported-volume"></a>Podporovaný svazek

- Maximální počet profilů zápisu na token: 1 000  
- Maximální počet automatizovaných zařízení pro zápis zařízení na profil: bez omezení (v rámci maximálního počtu zařízení na token)
- Maximální počet automatizovaných tokenů registrace zařízení na účet Intune: 2 000
- Maximální počet automatizovaných zařízení pro zápis zařízení na token: limit první synchronizace je 75000-80000 zařízení. Intune se bude dál synchronizovat s ABM nebo ASM a každých 12 hodin se vrátit se změnami, aby se při každém přidání dalších zařízení. Ruční synchronizace (která se dá aktivovat každých 15 minut) taky přidá do Intune další dávku zařízení. Synchronizace budou pořád k dispozici a zařízení budou uchovávat synchronizaci z ABM/ASM přes Intune ve velkém množství. 

## <a name="get-an-apple-automated-device-enrollment-token"></a>Získání tokenu registrace Apple Automated Device

Než budete moct registrovat zařízení s iOS/iPadOS pomocí ADE, budete potřebovat soubor tokenu ADE (. p7m) od společnosti Apple. Tento token umožňuje Intune synchronizovat informace o zařízeních ADE, která vaše společnost vlastní. Umožňuje také Intune odeslat společnosti Apple registrační profily a přiřazovat k těmto profilům zařízení.

K vytvoření tokenu použijete portál [Apple Business Manager (ABM)](https://business.apple.com/) nebo [Apple School Manager (ASM)](https://school.apple.com/) . Pomocí portálu ABM/ASM taky přiřadíte zařízení ke správě do Intune.

> [!NOTE]
> Pokud token odstraníte z klasického portálu Intune před migrací do Azure, může Intune obnovit odstraněný token Apple ADE. Token ADE můžete znovu odstranit z Azure Portal.

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-the-token"></a>Krok 1. Stáhněte si certifikát veřejného klíče Intune, který je potřebný k vytvoření tokenu.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **iOS/iPadOS**registrace zařízení s  >  **iOS/iPadOS**.

    ![Stažení tokenu programu registrace zařízení](./media/device-enrollment-program-enroll-ios/ios-enroll.png)

2. Vyberte **tokeny programu registrace**  >  **Přidat**.

3. Výběrem možnosti **Souhlasím** udělte Microsoftu oprávnění k odesílání informací o uživatelích a zařízeních do společnosti Apple.

   > [!NOTE]
   > Až budete postupovat od kroku 2 ke stažení certifikátu veřejného klíče Intune, nezavírejte průvodce ani nevybírejte z této stránky. Tím dojde k zrušení platnosti certifikátu, který jste stáhli, a budete muset tento proces opakovat. Pokud k této situaci dojde, obvykle si všimněte, že tlačítko **vytvořit** na kartě **Revize + vytvořit** je šedé a nemůžete tento proces dokončit.

   ![Snímek obrazovky s podoknem Token Programu registrace v pracovním prostoru Certifikáty Apple pro stažení veřejného klíče](./media/device-enrollment-program-enroll-ios/add-enrollment-program-token-pane.png)

4. Vyberte **Stáhnout veřejný klíč** a stáhněte si a místně uložte soubor šifrovacího klíče (.pem). Soubor. pem slouží k vyžádání certifikátu vztahu důvěryhodnosti z portálu Apple.


### <a name="step-2-use-your-key-to-download-a-token-from-apple"></a>Krok 2. Pomocí klíče si stáhněte token od společnosti Apple.

1. Zvolením možnosti **vytvořit token prostřednictvím Apple Business Manageru** otevřete portál společnosti Apple a přihlaste se pomocí Apple ID vaší společnosti. Toto Apple ID můžete použít k obnovení tokenu ADE.
2. Na [portálu](https://business.apple.com)společnosti Apple vyberte **Začínáme** pro **program registrace zařízení**.

3. Na stránce pro **správu serverů** zvolte, že chcete **přidat server MDM**.
4. Zadejte **název serveru MDM** a zvolte **Další**. Název serveru slouží pro vaši informaci, abyste mohli identifikovat server pro správu mobilních zařízení (MDM). Nejedná se o název nebo adresu URL serveru Microsoft Intune.

5. Otevře se dialogové okno pro **přidání&lt;názvu serveru&gt;**, ve kterém se zobrazí výzva, abyste **nahráli svůj veřejný klíč**. Vyberte **zvolit soubor...** abyste mohli nahrát soubor .pem, a pak zvolte **Další**.

6. Přejděte na **Deployment Programs (Programy nasazení) ** &gt; **Device Enrollment Program (Program registrace zařízení) ** &gt; **Manage Devices** (Spravovat zařízení).
7. V části se **způsobem výběru zařízení** určete způsob identifikace zařízení:
    - **Sériové číslo**
    - **Číslo objednávky**
    - **Nahrát soubor CSV**

   ![Snímek obrazovky s výběrem zařízení podle sériového čísla, nastavením volby akce na přiřazení serveru a výběrem názvu serveru](./media/device-enrollment-program-enroll-ios/enrollment-program-token-specify-serial.png)

8. V možnosti **Vybrat akci** vyberte **Přiřadit k serveru**, vyberte &lt;název_serveru&gt; zadaný pro Microsoft Intune a pak zvolte **OK**. Portál Apple přiřadí daná zařízení k serveru Intune, aby bylo možné je spravovat, a pak zobrazí zprávu o **dokončení přiřazení**.

   Na portálu Apple přejděte na **Programy nasazení** &gt; **Program registrace zařízení** &gt; **Zobrazit historii přiřazení**. Zobrazí se seznam zařízení s přiřazeným serverem MDM.

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>Krok 3. Uložte si Apple ID, které jste použili k vytvoření tohoto tokenu.

V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)zadejte Apple ID pro budoucí referenci.

![Snímek obrazovky s Apple ID použitým k vytvoření tokenu programu registrace a přechodem na token programu registrace](./media/device-enrollment-program-enroll-ios/image03.png)

### <a name="step-4-upload-your-token-and-choose-scope-tags"></a>Krok 4: Nahrajte token a vyberte značky oboru.

1. V poli **token Apple** vyhledejte soubor certifikátu (. p7m), vyberte **otevřít**.
2. Pokud chcete pro tento token DEP použít [značky oboru](../fundamentals/scope-tags.md) , zvolte **rozsah (značky)** a vyberte požadované značky oboru. Značky oboru použité u tokenu budou děděny profily a zařízeními přidanými do tohoto tokenu.
3. Vyberte **vytvořit**.

Pomocí nabízeného certifikátu může Intune registrovat a spravovat zařízení s iOS/iPadOS tím, že zapisuje zásady do zaregistrovaných mobilních zařízení. Intune se automaticky synchronizuje s Apple, aby bylo možné zobrazit účet registračního programu.

## <a name="create-an-apple-enrollment-profile"></a>Vytvoření registračního profilu Apple

Teď, když jste nainstalovali token, můžete vytvořit profil zápisu pro zařízení ADE. Registrační profil zařízení definuje nastavení, která se během registrace použijí pro skupinu zařízení. Pro každý token ADE je k dispozici limit 100 profilů zápisu.

> [!NOTE]
> Zařízení se zablokuje, pokud není k dispozici dostatek Portál společnosti licencí pro token VPP, nebo pokud vypršela platnost tokenu. Intune zobrazí výstrahu, když se brzo vyprší platnost tokenu nebo dojde k nedostatku licencí.
 

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **iOS/iPadOS**  >  **iOS/iPadOS**  >  **tokeny programu registrace**.
2. Vyberte token, zvolte **profily**  >  **vytvořit profil**  >  **iOS/iPadOS**.

    ![Snímek obrazovky pro vytvoření profilu](./media/device-enrollment-program-enroll-ios/image04.png)

3. Na stránce **základy** zadejte **název** a **Popis** profilu pro účely správy. Uživatelé tyto podrobnosti nevidí. 

    ![Název a popis profilu](./media/device-enrollment-program-enroll-ios/image05.png)

4. Vyberte **Další: nastavení správy zařízení**.

5. V části **Přidružení uživatele** zvolte, jestli se zařízení s tímto profilem musí registrovat s přiřazeným uživatelem nebo bez něj.
    - **Zaregistrovat s přidružením uživatele** – tuto možnost vyberte pro zařízení, která patří uživatelům a chtějí používat portál společnosti pro služby, jako je instalace aplikací. Pokud používáte službu AD FS a používáte pomocníka s nastavením k ověřování, je třeba zadat [uživatelské jméno/Smíšený Koncový bod WS-Trust 1,3](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff608241(v=ws.10)) [Další informace](/powershell/module/adfs/get-adfsendpoint?view=win10-ps) .

    - **Zaregistrovat bez přidružení uživatele** – Tuto možnost zvolte pro zařízení nespojená s jedním uživatelem. Tuto možnost použijte pro zařízení, která nemají přístup k místním uživatelským datům. Pokud chcete koncovému uživateli povolit, aby se přihlásil k Portál společnosti iOS a navázal jako primárního uživatele zařízení, pošlete `IntuneUDAUserlessDevice` klíč do portál společnosti pro iOS v zásadách konfigurace aplikace pro spravovaná zařízení. Všimněte si, že jako primární uživatel se naváže jenom první přihlášený uživatel. Pokud se první uživatel odhlásí a druhý uživatel přihlásí, první uživatel zůstane primárním uživatelem zařízení. Další informace najdete v tématu [Konfigurace aplikace Portál společnosti pro podporu zařízení se systémem iOS a IPADOS DEP](../apps/app-configuration-policies-use-ios.md#configure-the-company-portal-app-to-support-ios-and-ipados-dep-devices). 

6. Pokud jste zvolili možnost **registrovat s přidružením uživatele**, můžete uživatelům povolit ověřování pomocí portál společnosti namísto pomocníka s nastavením Apple.

    ![Ověření pomocí portálu společnosti](./media/device-enrollment-program-enroll-ios/authenticatewithcompanyportal.png)

    > [!NOTE]
    > Pokud chcete provést některou z následujících akcí, nastavte **možnost vybrat, kde se musí uživatelé ověřit** , aby **portál společnosti**.
    >    - Použít vícefaktorové ověřování.
    >    - Zobrazit výzvu uživatelům, pokud při prvním přihlášení potřebují změnit heslo.
    >    - Zobrazit výzvu uživatelům, aby při registraci resetovali neplatná hesla.
    >
    > Ty nejsou podporované při ověřování pomocí Pomocníka s nastavením Apple.

7. Pokud jste zvolili **portál společnosti** pro **Vyberte, kde se uživatelé musí ověřit**, můžete k automatické instalaci portál společnosti na zařízení použít token VPP. V takovém případě nemusí uživatel zadávat Apple ID. K instalaci Portálu společnosti pomocí tokenu VPP zvolte token v seznamu **Nainstalovat Portál společnosti pomocí VPP**. Vyžaduje, aby byla Portál společnosti již přidána do tokenu VPP. Aby se zajistilo, že bude aplikace Portál společnosti po registraci nadále aktualizována, ujistěte se, že jste nakonfigurovali nasazení aplikace v Intune (>klientských aplikacích Intune). Takže interakce uživatele není povinná, pravděpodobně budete chtít Portál společnosti jako aplikaci VPP pro iOS/iPadOS, nastavit ji jako požadovanou aplikaci a používat licencování zařízení pro přiřazení. Dbejte na to, aby tokenu nevypršela platnost a abyste měli dost licencí zařízení pro aplikaci Portál společnosti. Pokud vyprší platnost tokenu nebo dojde k nedostatku licencí, Intune nainstaluje místo toho Portál společnosti App Storu a zobrazí výzvu k zadání Apple ID. 

    > [!NOTE]
    > Když vyberete, aby se **Uživatelé musí ověřit** , **portál společnosti**, ujistěte se, že se proces registrace zařízení provádí během prvních 24 hodin aplikace Portál společnosti, který se stahuje do zařízení ADE. Jinak může registrace selhat a k registraci zařízení bude potřeba obnovení továrního nastavení.
    
    ![Snímek obrazovky s instalací portálu společnosti pomocí programu VPP](./media/device-enrollment-program-enroll-ios/install-cp-with-vpp.png)

8. Pokud jste zvolili **Pomocníka s nastavením** pro **Vyberte, kde se uživatelé musí ověřit**, ale také chcete použít podmíněný přístup nebo nasadit firemní aplikace na zařízení, musíte na zařízení nainstalovat portál společnosti. Pokud to chcete udělat, vyberte pro **instalaci portál společnosti** **Ano** .  Pokud chcete, aby uživatelé přijímali Portál společnosti bez nutnosti ověřování do App Storu, zvolte možnost **nainstalovat portál společnosti pomocí programu VPP** a vybrat token VPP. Ujistěte se, že platnost tokenu nevyprší a že máte dost licencí na zařízení, aby mohla aplikace Portál společnosti správně nasadit.

9. Pokud jste zvolili token pro **instalaci portál společnosti pomocí programu VPP**, můžete zařízení uzamknout v režimu jedné aplikace (konkrétně portál společnosti aplikace) hned po dokončení Průvodce nastavením. Tuto možnost nastavíte volbou **Ano** u položky **Spustit Portál společnosti v režimu Jedna aplikace, dokud neproběhne ověření**. Než bude uživatel moct zařízení použít, musí se nejprve ověřit přihlášením na Portálu společnosti.

    Multi-Factor Authentication se nepodporuje v jednom zařízení uzamčeném v režimu jedné aplikace. Toto omezení existuje, protože zařízení nemůže přepnout na jinou aplikaci, aby bylo možné dokončit druhý faktor ověřování. Proto pokud chcete vícefaktorové ověřování na jednom zařízení v režimu aplikace, druhý faktor musí být na jiném zařízení.

    Tato funkce je podporována pouze pro iOS/iPadOS 11.3.1 a novější.

   ![Snímek obrazovky režimu jedné aplikace](./media/device-enrollment-program-enroll-ios/single-app-mode.png)

10. Pokud chcete, aby byla zařízení s tímto profilem pod dohledem, klikněte na **tlačítko Ano** pro **pod dohledem**.

    ![Snímek obrazovky s nastaveními správy zařízení](./media/device-enrollment-program-enroll-ios/supervisedmode.png)

    U zařízení **pod dohledem** je ve výchozím nastavení víc možností správy a je zakázaný zámek aktivace. Microsoft doporučuje použít ADE jako mechanismus pro povolení režimu pod dohledem, obzvláště pokud nasazujete velký počet zařízení s iOS/iPadOS. Zařízení Apple sdíleného iPadu pro firmy musí být pod dohledem.

    Uživatelé se dozvědí, že jejich zařízení jsou pod dohledem, dvěma způsoby:

   - Na zamykací obrazovce se zobrazí oznámení: „Tento iPhone spravuje Contoso.“
   - **Nastavení**  >  **Obecné**  >  **o** obrazovce říká: "Tento iPhone je pod dohledem. Společnost Contoso může monitorovat internetové přenosy a zařízení vyhledat.“

     > [!NOTE]
     > Zařízení zaregistrované bez dohledu se dá resetovat do stavu pod dohledem jenom pomocí Apple Configuratoru. Resetování zařízení tímto způsobem vyžaduje připojení zařízení s iOS/iPadOS k počítači Mac pomocí kabelu USB. Další informace na toto téma získáte v [dokumentaci Apple Configuratoru](http://help.apple.com/configurator/mac/2.3).

11. Vyberte, jestli chcete pro zařízení, která používají tento profil, uzamčenou registraci. **Uzamčená registrace** zakáže nastavení pro iOS/iPadOS, která umožňují odebrání profilu správy z nabídky **Nastavení** . Po registraci zařízení toto nastavení nemůžete změnit bez vymazání zařízení. Taková zařízení musí mít režim správy **Pod dohledem** nastavený na *Ano*. 

    > [!NOTE]
    > Až se zařízení zaregistruje pomocí **zamčené registrace**, nebudou moct uživatelé v portál společnosti aplikaci použít **odebrání zařízení** nebo **obnovení továrního nastavení** . Možnosti nebudou pro uživatele k dispozici. Uživatel také nebude moci zařízení odebrat na webu Portál společnosti ( https://portal.manage.microsoft.com) .
    > Pokud je zařízení BYOD převést na zařízení Apple automatizovaného zápisu zařízení a zaregistrované s uzamčeným profilem s povoleným **zápisem** , bude moct uživatel použít možnost **Odebrat zařízení** a **obnovit tovární nastavení** po dobu 30 dnů a možnosti budou zakázané nebo nedostupné. Odkaz: https://help.apple.com/configurator/mac/2.8/#/cad99bc2a859 .

12. Pokud jste zvolili možnost **zaregistrovat bez přidružení uživatele** a **pod dohledem** výše, musíte se rozhodnout, jestli chcete zařízení nakonfigurovat jako [Apple sdílená zařízení iPad pro firmy](https://support.apple.com/guide/mdm/shared-ipad-overview-cad7e2e0cf56/web). Když pro **sdílený iPad**zvolíte **Ano** , přihlásí se ke stejnému zařízení více uživatelů. Uživatelé se budou ověřovat pomocí svých spravovaných Apple ID a federovaných účtů pro ověřování nebo prostřednictvím dočasné relace (tj. účet Guest). Tato možnost vyžaduje iOS/iPadOS 13,4 nebo novější.

    Pokud jste se rozhodli nakonfigurovat zařízení tak, aby byla Apple sdílená na iPadu pro firmy, musíte nastavit **maximální počet uživatelů v mezipaměti**. Nastavte tuto hodnotu na počet uživatelů, u kterých očekáváte použití sdíleného iPadu. Do mezipaměti můžete ukládat až 24 uživatelů na 32 GB nebo na 64 GB zařízení. Pokud zvolíte velmi nízké číslo, může chvíli trvat, než se data uživatele po přihlášení najdou do zařízení. Pokud zvolíte velmi vysoké číslo, uživatelé nemusí mít dost místa na disku.  

    > [!NOTE]
    > Pokud chcete nastavit Apple Shared iPad pro firmy, nastavte následující: 
    > - **Přidružení uživatele**  =  **Zaregistrovat bez přidružení uživatele** 
    > - **Pod dohledem**  =  **Ano**. 
    > - **Sdílený iPad** = * * Ano * *.
    > Dočasné relace jsou ve výchozím nastavení povolené a umožňují vašim uživatelům přihlašovat se ke sdílenému iPadu bez spravovaného účtu Apple ID. Můžete zakázat dočasné relace na sdíleném iPadu tím, že nakonfigurujete [Nastavení omezení pro zařízení](../configuration/device-restrictions-ios.md)s platformou iOS/iPadOS Shared.  

13. Vyberte, jestli chcete, aby zařízení, která používají tento profil, mohla **synchronizovat s počítači**. Pokud vyberete **Povolit Apple Configurator podle certifikátu**, musíte zvolit certifikát v části **Certifikáty Apple Configuratoru**. Pro iOS/iPadOS 13,0 a novější se toto nastavení už nepoužívá od společnosti Apple. 

     > [!NOTE]
     > Pokud je **synchronizace s počítači** nastavená na **Odepřít vše**, port bude omezený na zařízeních s iOS a iPadOS. Port lze použít pouze pro zpoplatnění a žádné jiné. Port se zablokuje pomocí iTunes nebo Apple Configuratoru 2.
     Pokud je **synchronizace s počítači** nastavená tak, aby **povolovala Apple Configuratoru podle certifikátu**, ujistěte se, že máte místní kopii certifikátu, ke kterému budete mít přístup později. V nahraném kopírování nebudete moct dělat změny a je důležité, aby byl tento certifikát v budoucnu přístupný. Pokud se chcete připojit k zařízení se systémem iOS/iPadOS ze zařízení macOS nebo počítače s, musí být v zařízení nainstalovaný stejný certifikát, který vytváří připojení k zařízení se systémem iOS/iPadOS, které bylo zaregistrováno pomocí profilu automatického zápisu zařízení s touto konfigurací a certifikátem.

14. Pokud jste v předchozím kroku zvolili **Povolit Apple Configurator podle certifikátu**, zvolte certifikát Apple Configuratoru, který se má importovat.

15. Můžete zadat formát pojmenování pro zařízení, která se při registraci a při každém úspěšném vrácení se změnami automaticky používají. Chcete-li vytvořit šablonu pro pojmenování, vyberte možnost **Ano** v části **použít šablonu názvu zařízení**. Pak v poli **šablona názvu zařízení** zadejte šablonu, která se má použít pro názvy používané tímto profilem. Můžete zadat formát šablony, který zahrnuje typ zařízení a sériové číslo. Šablona názvu zařízení zahrnuje podporu pro iPhone, iPad a iPod touch. 
16. Klikněte na tlačítko **Další: přizpůsobení pomocníka s nastavením**.

17. Na stránce **vlastní nastavení Pomocníka s nastavením** nakonfigurujte následující nastavení profilu: ![ přizpůsobení pomocníka s nastavením.](./media/device-enrollment-program-enroll-ios/setupassistantcustom.png)


    | Nastavení oddělení | Description |
    |---|---|
    | <strong>Department Name</strong> | Zobrazí se, když uživatelé klepnou při aktivaci na <strong>O konfiguraci</strong>. |
    |    <strong>Telefon na oddělení</strong>     | Zobrazí se, když uživatel při aktivaci klikne na tlačítko <strong>Potřebuji nápovědu</strong>. |

    Během instalace uživatele můžete skrýt obrazovky pomocníka s nastavením na zařízení.
    - Pokud zvolíte **Skrýt**, obrazovka se při nastavování nezobrazí. Po nastavení zařízení může uživatel přejít do nabídky **Nastavení** a funkci nastavit tam.
    - Pokud zvolíte **Zobrazit**, obrazovka se při nastavování zobrazí. Uživatel může obrazovku někdy přeskočit a neudělat žádnou akci. Může ale později přejít do nabídky zařízení **Nastavení** a funkci nastavit tam. 


    | Nastavení na obrazovce Průvodce nastavením | Pokud zvolíte **Zobrazit**, zařízení při nastavování: |
    |------------------------------------------|------------------------------------------|
    | <strong>Heslo</strong> | Vyzve uživatele k zadání hesla. Vždy vyžadovat heslo pro nezabezpečená zařízení, pokud není přístup kontrolován jiným způsobem (například celoobrazovkový režim, který zařízení omezuje na jednu aplikaci). Pro iOS/iPadOS 7,0 a novější. |
    | <strong>Zjišťování polohy</strong> | Vyzve uživatele k poskytnutí polohy. Pro macOS 10,11 a novější a iOS/iPadOS 7,0 a novější. |
    | <strong>Obnovení</strong> | Zobrazí obrazovku aplikace & data. Tato obrazovka nabídne uživateli při nastavování zařízení možnost obnovit nebo přenést data ze zálohy v iCloudu. Pro macOS 10,9 a novější a iOS/iPadOS 7,0 a novější. |
    | <strong>iCloud a Apple ID</strong> | Umožní uživateli přihlásit se pomocí svého Apple ID a používat iCloud. Pro macOS 10,9 a novější a iOS/iPadOS 7,0 a novější.   |
    | <strong>Podmínky a ujednání</strong> | Požaduje, aby uživatel přijal podmínky a ujednání společnosti Apple. Pro macOS 10,9 a novější a iOS/iPadOS 7,0 a novější. |
    | <strong>Touch ID</strong> | Umožní uživateli nastavit pro zařízení identifikaci otiskem prstu. Pro macOS 10.12.4 a novější a iOS/iPadOS 8,1 a novější. |
    | <strong>Apple Pay</strong> | Umožní uživateli nastavit na zařízení Apple Pay. Pro macOS 10.12.4 a novější a iOS/iPadOS 7,0 a novější. |
    | <strong>Zoom</strong> | Umožní uživateli zvětšit zobrazení při nastavování zařízení. Pro iOS/iPadOS 8,3 a novější. |
    | <strong>Siri</strong> | Umožní uživateli nastavit Siri. Pro macOS 10,12 a novější a iOS/iPadOS 7,0 a novější. |
    | <strong>Diagnostická data</strong> | Zobrazí uživateli obrazovku Diagnostická data. Tato obrazovka umožní uživateli poslat společnosti Apple diagnostická data. Pro macOS 10,9 a novější a iOS/iPadOS 7,0 a novější. |
    | <strong>Tón zobrazení</strong> | Poskytněte uživateli možnost zapnout tónový displej. Pro macOS 10.13.6 a novější a iOS/iPadOS 9.3.2 a novější. |
    | <strong>Ochrana osobních údajů</strong> | Zobrazit obrazovku ochrany osobních údajů uživateli. Pro macOS 10.13.4 a novější a iOS/iPadOS 11,3 a novější. |
    | <strong>Migrace zařízení s Androidem</strong> | Poskytněte uživateli možnost migrovat datum ze zařízení s Androidem. Pro iOS/iPadOS 9,0 a novější.|
    | <strong>iMessage a FaceTime</strong> | Poskytněte uživateli možnost nastavit iMessage a FaceTime. Pro iOS/iPadOS 9,0 a novější. |
    | <strong>Onboarding</strong> | Zobrazuje informační obrazovky pro vzdělávání uživatelů, jako je například titulní stránka a multitasking a řídicí centrum. Pro iOS/iPadOS 11,0 a novější. |
    | <strong>Sledovat migraci</strong> | Poskytněte uživateli možnost migrovat data ze sledovacího zařízení. Pro iOS/iPadOS 11,0 a novější.|
    | <strong>Čas obrazovky</strong> | Zobrazí obrazovku čas obrazovky. Pro macOS 10,15 a novější a iOS/iPadOS 12,0 a novější. |
    | <strong>Aktualizace softwaru</strong> | Zobrazte povinnou obrazovku aktualizace softwaru. Pro iOS/iPadOS 12,0 a novější. |
    | <strong>Nastavení SIM</strong> | Poskytněte uživateli možnost Přidat plán pro mobilní síť. Pro iOS/iPadOS 12,0 a novější. |
    | <strong>Příznaky</strong> | Zobrazit obrazovku vzhled pro uživatele Pro macOS 10,14 a novější a iOS/iPadOS 13,0 a novější. |
    | <strong>Jazyk Express</strong>| Zobrazit obrazovku jazyka Express pro uživatele |
    | <strong>Preferovaný jazyk</strong> | Poskytněte uživateli možnost zvolit si  **preferovaný jazyk**. |
    | <strong>Migrace zařízení do zařízení</strong> | Poskytněte uživateli možnost migrovat data ze starého zařízení do tohoto zařízení. Pro iOS/iPadOS 13,0 a novější. |
    | <strong>Evidenc</strong> | Zobrazit registrační obrazovku uživateli Pro macOS 10,9 a novější. |
    | <strong>FileVault</strong> | Zobrazit na uživateli obrazovku šifrování trezoru 2. Pro macOS 10,10 a novější. |
    | <strong>Diagnostika iCloud</strong> | Zobrazit obrazovku analýzy iCloud pro uživatele Pro macOS 10.12.4 a novější. |
    | <strong>Úložiště iCloud</strong> | Zobrazí uživateli iCloud dokumenty a plochu obrazovky. Pro macOS 10.13.4 a novější. |
    

18. Kliknutím na tlačítko **Další** přejdete na stránku **Revize + vytvořit** .

19. Pokud chcete profil uložit, zvolte **Vytvořit**.

### <a name="dynamic-groups-in-azure-active-directory"></a>Dynamické skupiny v Azure Active Directory

Pole **název** registrace můžete použít k vytvoření dynamické skupiny v Azure Active Directory. Další informace najdete v tématu [Azure Active Directory dynamické skupiny](/azure/active-directory/users-groups-roles/groups-dynamic-membership).

Pomocí názvu profilu můžete definovat [parametr enrollmentProfileName](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices) pro přiřazení zařízení s tímto registračním profilem.

Pokud chcete nejrychlejší doručování zásad na zařízeních ADE s přidružením uživatele, ujistěte se, že je uživatel registrace členem, a to před nastavením zařízení ve skupině uživatelů AAD. 

Přiřazení dynamických skupin k registračním profilům může vést k prodlevám při doručování aplikací a zásad do zařízení po registraci.


## <a name="sync-managed-devices"></a>Synchronizace spravovaných zařízení
Teď, když má Intune oprávnění spravovat vaše zařízení, můžete synchronizovat Intune s Apple, aby se spravovaná zařízení zobrazila v Intune na portálu Azure Portal.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **iOS/iPadOS**  >  **iOS/iPadOS**  >  **tokeny programu registrace**.

2. Vyberte token v seznamu > **Devices** > **synchronizace**zařízení. ![ Snímek obrazovky uzlu zařízení programu registrace a odkaz na synchronizaci.](./media/device-enrollment-program-enroll-ios/image06.png)

   Pokud chcete dodržovat podmínky společnosti Apple pro přijatelný provoz programu registrace, Intune ukládá tato omezení:
   - Úplná synchronizace se nesmí pouštět častěji než jednou za sedm dní. Během úplné synchronizace načte Intune úplný aktualizovaný seznam sériových čísel přiřazených k serveru Apple MDM připojenému k Intune. Pokud se zařízení ADE odstraní z portálu Intune, měl by být na portálu ADE nepřiřazený ze serveru Apple MDM. Pokud není přiřazená, nebude se znovu naimportovat do Intune, dokud se nespustí Úplná synchronizace.   
   - Synchronizace se spouští automaticky každých 12 hodin. Můžete ji také spustit kliknutím na tlačítko **Synchronizovat** (ne častěji než jednou za 15 minut). Každá žádost o synchronizaci má 15 minut na dokončení. Tlačítko **Synchronizovat** bude deaktivované, dokud se synchronizace nedokončí. Při synchronizaci se zaktualizuje stav existujících zařízení a naimportují se nová zařízení přiřazená k serveru Apple MDM.   


## <a name="assign-an-enrollment-profile-to-devices"></a>Přiřazení profilu registrace zařízením
Než se můžou zařízení zaregistrovat, musíte přiřadit profil programu registrace.

>[!NOTE]
>Sériová čísla můžete profilům také přiřadit v okně **sériových čísel Apple**.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **iOS/iPadOS**  >  **iOS/iPadOS**  >  **tokeny programu registrace** > v seznamu vyberte token.
2. Zvolte **Zařízení** > zvolte zařízení v seznamu > **Přiřadit profil**.
3. V části **Přiřadit profil** zvolte profil pro zařízení > **Přiřadit**.

### <a name="assign-a-default-profile"></a>Přiřazení výchozího profilu

Můžete si vybrat výchozí profil, který se má použít pro všechna zařízení, která se registrují s konkrétním tokenem.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **iOS/iPadOS**  >  **iOS/iPadOS**  >  **tokeny programu registrace** > v seznamu vyberte token.
2. Zvolte **Nastavit výchozí profil**, v rozevíracím seznamu zvolte profil a potom zvolte **Uložit**. Tento profil se použije pro všechna zařízení, která se registrují s tímto tokenem.

## <a name="distribute-devices"></a>Distribuujte zařízení.
Povolili jste správu a synchronizaci mezi společností Apple a Intune a přiřadili jste profil, který umožní registraci zařízení ADE. Teď můžete zařízení rozdělit mezi uživatele. U zařízení s přidruženými uživateli je potřeba, aby měl každý uživatel přiřazenu licenci Intune. Zařízení bez přidružení uživatele vyžadují licenci zařízení. Aktivované zařízení nemůže použít registrační profil, dokud se zařízení nevymaže.

Další informace najdete [v tématu Registrace zařízení se systémem iOS/iPadOS v Intune pomocí program registrace zařízení](../user-help/enroll-your-device-dep-ios.md).

## <a name="renew-an-automated-device-enrollment-token"></a>Obnovit automatický token pro zápis zařízení  

> [!NOTE]
> Kromě prodloužení platnosti tokenu ADE je potřeba obnovit token programu registrace v Intune a Apple Business Manageru, když se změní heslo spravovaného Apple ID pro uživatele, který nastavil token v Apple Business Manageru, nebo tento uživatel opouští vaši organizaci Apple Business Manageru.

1. Přejít na business.apple.com.
2. Klikněte na **Nastavení** (vlevo dole).
3. V části **servery MDM**vyberte svůj server MDM přidružený k tokenu ADE/DEP, který chcete obnovit.
4. Klikněte na **Stáhnout token**.

    ![Snímek obrazovky s možností Generate New Token (Vygenerovat nový token)](./media/device-enrollment-program-enroll-ios/generatenewtoken.png)

5. Na příkazovém řádku vyberte možnost stáhnout token serveru.
> [!NOTE]
> Neklepejte na možnost **"Stáhnout token serveru"** , pokud nechcete obnovit token, jak je uvedeno v příkazovém řádku. tím dojde k zrušení platnosti tokenu aktuálně používaného službou Intune (nebo jakéhokoli jiného řešení MDM). Pokud jste token již stáhli, ujistěte se, že jste pokračovali v dalších krocích až do obnovení tokenu.

6. Po stažení tokenu v [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)zvolte **zařízení**  >  **iOS/iPadOS**  >  **iOS/iPadOS**registrace tokenů  >  **programu** > zvolte token.
    ![Snímek obrazovky s možností Tokeny programu registrace](./media/device-enrollment-program-enroll-ios/enrollmentprogramtokens.png)

7. Vyberte **obnovit token** a zadejte Apple ID, které jste použili k vytvoření původního tokenu (Pokud není automaticky vyplněné).  
    ![Snímek obrazovky s možností Generate New Token (Vygenerovat nový token)](./media/device-enrollment-program-enroll-ios/renewtoken.png)

8. Nahrajte nově stažený token.

9. Kliknutím na tlačítko **Další** přejdete na stránku **značky oboru** a v případě potřeby přiřadíte značky oboru.

10. Zvolte **Obnovit token**. Zobrazí se potvrzení, že se token obnovil.   
    ![Snímek obrazovky s potvrzením](./media/device-enrollment-program-enroll-ios/confirmation.png)

## <a name="delete-an-automated-device-enrollment-token-from-intune"></a>Odstranění automatického tokenu pro zápis zařízení z Intune

Tokeny registračního profilu můžete z Intune odstranit, pokud
- k tokenu nejsou přiřazená žádná zařízení.
- k výchozímu profilu nejsou přiřazená žádná zařízení.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **iOS/MacOS**  >  **iOS/MacOS**  >  **tokeny programu registrace** > vyberte token > **zařízení**.
2. Odstraňte všechna zařízení přiřazená k tomuto tokenu.
3. V části **zařízení**  >  **iOS/MacOS**  >  **iOS/MacOS**registrace zápisu  >  **tokeny programu** > vyberte **profily**> tokeny.
4. Pokud existuje výchozí profil, odstraňte ho.
5. V části **zařízení**  >  **iOS/MacOS**  >  **iOS/MacOS**registrace zápisu  >  **tokeny programu** > vyberte token > **Odstranit**.
