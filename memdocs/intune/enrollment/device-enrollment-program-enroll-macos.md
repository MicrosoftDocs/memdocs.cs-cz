---
title: Registrace zařízení macOS – Apple Business Manager nebo Apple School Manager
titleSuffix: ''
description: Naučte se registrovat zařízení macOS vlastněná společností.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/06/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7afe3897c040673ad869584e1e8e8f55f4fc08ff
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911892"
---
# <a name="automatically-enroll-macos-devices-with-the-apple-business-manager-or-apple-school-manager"></a>Automatická registrace zařízení macOS pomocí Apple Business Manageru nebo Apple School Manageru

> [!IMPORTANT]
> Apple se nedávno změnil z použití programu Apple Program registrace zařízení (DEP) na Apple Automated Device Enrollment (ADE). Intune je v procesu aktualizace uživatelského rozhraní Intune, aby odrážel. Dokud tyto změny nedokončíte, budete na portálu Intune dál zobrazovat *program registrace zařízení* . Všude, kde se zobrazuje, teď používá automatický zápis zařízení.

Můžete nastavit registraci v Intune pro zařízení macOS zakoupená prostřednictvím [Apple Business Manageru](https://business.apple.com/) nebo [Apple School Manageru](https://school.apple.com/). U velkého počtu zařízení můžete použít kteroukoli z těchto registrací, aniž byste je museli dotýkat. Tato zařízení s macOS můžete dát rovnou uživatelům. Když uživatel zařízení zapne, Průvodce nastavením spustí předem nakonfigurovaná nastavení a zařízení se zaregistruje do správy v Intune.

Pokud chcete nastavit registraci, použijte portál Intune i Apple. Vytvoříte profily zápisu obsahující nastavení, která se v zařízeních nastavila během registrace.

Pomocí [správce registrace zařízení](device-enrollment-manager-enroll.md)nefunguje zápis z Apple Business Manageru ani Apple School Manager.

<!--
**Steps to enable enrollment programs from Apple**
1. [Get an Apple DEP token and assign devices](#get-the-apple-dep-token)
2. [Create an enrollment profile](#create-an-apple-enrollment-profile)
3. [Synchronize DEP-managed devices](#sync-managed-device)
4. [Assign DEP profile to devices](#assign-an-enrollment-profile-to-devices)
5. [Distribute devices to users](#end-user-experience-with-managed-devices)
-->
## <a name="prerequisites"></a>Předpoklady

- Zařízení zakoupená v [Apple School Manageru](https://school.apple.com/) nebo v programu [automatizované registrace zařízení společnosti Apple](http://deploy.apple.com)
- Seznam sériových čísel nebo čísel nákupních objednávek
- [Autorita MDM](../fundamentals/mdm-authority-set.md)
- [Apple MDM push Certificate](../enrollment/apple-mdm-push-certificate-get.md)

## <a name="get-an-apple-ade-token"></a>Získání tokenu Apple ADE

Než budete moct zaregistrovat zařízení macOS pomocí ADE nebo Apple School Manageru, budete potřebovat soubor tokenu (. p7m) od společnosti Apple. Tento token umožňuje Intune synchronizovat informace o zařízeních, která vaše organizace vlastní. Umožňuje také Intune nahrát profily registrace do Applu a přiřadit tyto profily zařízením.

K vytvoření tokenu použijete portál Apple. K přiřazení zařízení do Intune pro správu se používá také portál Apple.

> [!NOTE]
> Pokud token odstraníte z klasického portálu Intune před migrací do Azure, může Intune obnovit odstraněný token Apple. Token můžete znovu odstranit z Azure Portal.

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-the-token"></a>Krok 1. Stáhněte si certifikát veřejného klíče Intune, který je potřebný k vytvoření tokenu.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **MacOS**  >  **MacOS registrace**  >  **tokeny programu registrace**  >  **Přidat**.

    ![Stažení tokenu programu registrace zařízení](./media/device-enrollment-program-enroll-macos/image01.png)

2. Výběrem možnosti **Souhlasím** udělte Microsoftu oprávnění k odesílání informací o uživatelích a zařízeních do společnosti Apple.

   ![Snímek obrazovky s podoknem Token Programu registrace v pracovním prostoru Certifikáty Apple pro stažení veřejného klíče](./media/device-enrollment-program-enroll-ios/add-enrollment-program-token-pane.png)

3. Vyberte **Stáhnout veřejný klíč** a stáhněte si a místně uložte soubor šifrovacího klíče (.pem). Soubor. pem slouží k vyžádání certifikátu vztahu důvěryhodnosti z portálu Apple.

### <a name="step-2-use-your-key-to-download-a-token-from-apple"></a>Krok 2. Použijte svůj klíč ke stažení tokenu od společnosti Apple.

1. Vyberte **vytvořit token pro prostřednictvím Apple Business Manageru** nebo **vytvořte token prostřednictvím Apple School Manageru** a otevřete příslušný portál Apple a přihlaste se pomocí Apple ID vaší společnosti. Toto Apple ID můžete použít k obnovení tokenu.
2. V případě programu DEP na portálu Apple vyberte **Začínáme** pro **program registrace zařízení**  >  **Spravovat servery**  >  **Přidat MDM Server**.
3. V případě správy Apple School klikněte na portálu Apple na **servery MDM**  >  **Přidat MDM Server**.
4. Zadejte **název serveru MDM** a zvolte **Další**. Název serveru slouží pro vaši informaci, abyste mohli identifikovat server pro správu mobilních zařízení (MDM). Není to název serveru Microsoft Intune ani jeho URL.

5. Otevře se dialogové okno pro **přidání&lt;názvu serveru&gt;**, ve kterém se zobrazí výzva, abyste **nahráli svůj veřejný klíč**. Vyberte **zvolit soubor...** abyste mohli nahrát soubor .pem, a pak zvolte **Další**.

6. Přejděte na **Deployment Programs (Programy nasazení) ** &gt; **Device Enrollment Program (Program registrace zařízení) ** &gt; **Manage Devices** (Spravovat zařízení).
7. V části se **způsobem výběru zařízení** určete způsob identifikace zařízení:
    - **Sériové číslo**
    - **Číslo objednávky**
    - **Nahrát soubor CSV**

   ![Snímek obrazovky s výběrem zařízení podle sériového čísla, nastavením volby akce na přiřazení serveru a výběrem názvu serveru](./media/device-enrollment-program-enroll-macos/enrollment-program-token-specify-serial.png)

8. V možnosti **Vybrat akci** vyberte **Přiřadit k serveru**, vyberte &lt;název_serveru&gt; zadaný pro Microsoft Intune a pak zvolte **OK**. Portál Apple přiřadí daná zařízení k serveru Intune, aby bylo možné je spravovat, a pak zobrazí zprávu o **dokončení přiřazení**.

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>Krok 3. Uložte si Apple ID, které jste použili k vytvoření tohoto tokenu.

V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)zadejte Apple ID pro budoucí referenci.

![Snímek obrazovky s Apple ID použitým k vytvoření tokenu programu registrace a přechodem na token programu registrace](./media/device-enrollment-program-enroll-ios/image03.png)

### <a name="step-4-upload-your-token"></a>Krok 4: Nahrajte token.
V poli **Token Apple** přejděte k souboru certifikátu (.pem), zvolte **Otevřít** a pak zvolte **Vytvořit**. Certifikát Push Certificate umožňuje Intune registrovat a spravovat zařízení s macOS tím, že do registrovaných zařízení doručí zásady. Intune se automaticky synchronizuje s Apple, aby bylo možné zobrazit účet registračního programu.

## <a name="create-an-apple-enrollment-profile"></a>Vytvoření registračního profilu Apple

Teď, když máte nainstalovaný token, můžete pro zařízení vytvořit profil zápisu. Registrační profil zařízení definuje nastavení, která se během registrace použijí pro skupinu zařízení.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **MacOS**  >  **MacOS registrace**  >  **tokenů programu registrace**.
2. Vyberte token, zvolte **profily**a pak zvolte **vytvořit profil**  >  **MacOS**.

    ![Snímek obrazovky pro vytvoření profilu](./media/device-enrollment-program-enroll-macos/image04.png)

3. Na stránce **základy** zadejte **název** a **Popis** profilu pro účely správy. Uživatelům se tyto údaje nezobrazí. Pole **Název** můžete využít k vytvoření dynamické skupiny v Azure Active Directory. Název profilu použijte k definování parametru enrollmentProfileName pro přiřazení zařízení s tímto registračním profilem. Přečtěte si další informace o [Azure Active Directory dynamických skupinách](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices).

    ![Název a popis profilu](./media/device-enrollment-program-enroll-macos/createprofile.png)

4. Jako **platformu** zvolte **macOS**.

5. Kliknutím na tlačítko **Další** přejdete na stránku **Nastavení správy** .

6. V části **Přidružení uživatele** vyberte, jestli zařízení s tímto profilem musí mít při registraci přiřazeného uživatele.
    - **Zaregistrovat s přidružením uživatele** – tuto možnost vyberte u zařízení patřících uživatelům, kteří chtějí aplikaci Portál společnosti používat pro služby, jako je instalace aplikací. Při použití ADFS vyžaduje přidružení uživatelů [koncový bod WS-Trust 1.3 Username/Mixed](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff608241(v=ws.10)). [Další informace](/powershell/module/adfs/get-adfsendpoint?view=win10-ps) Vícefaktorové ověřování se nepodporuje u zařízení macOS ADE s přidružením uživatele.

    - **Zaregistrovat bez přidružení uživatele** – Tuto možnost zvolte pro zařízení nespojená s jedním uživatelem. Použijte ji pro zařízení určená k plnění úkolů, u kterých není potřeba přístup k místním uživatelským datům. Aplikace, jako je Portál společnosti aplikace, nefungují.

6. V případě **zamčené registrace**vyberte, jestli chcete pro zařízení, která používají tento profil, uzamčenou registraci. Hodnota **Ano** zakáže nastavení MacOS, která umožňují odebrání profilu správy z nabídky **Předvolby systému** nebo prostřednictvím **terminálu**. Po registraci zařízení nemůžete toto nastavení změnit bez vymazání zařízení.

7. Kliknutím na tlačítko **Další** přejdete na stránku **Pomocníka s nastavením** .

8. Na stránce **Pomocník s nastavením** nakonfigurujte následující nastavení profilu:

    ![Přizpůsobení pomocníka s nastavením.](./media/device-enrollment-program-enroll-macos/setupassistantcustom-macos.png)

    | Nastavení oddělení | Popis |
    |---|---|
    | <strong>Department Name</strong> | Zobrazí se, když uživatelé klepnou při aktivaci na <strong>O konfiguraci</strong>. |
    | <strong>Telefon na oddělení</strong> | Zobrazí se, když uživatel při aktivaci klikne na tlačítko <strong>Potřebuji nápovědu</strong>. |

    Můžete zvolit, jestli se různé obrazovky Průvodce nastavením mají uživateli zobrazit nebo skrýt.
    - Pokud zvolíte **Skrýt**, obrazovka se při nastavování nezobrazí. Po nastavení zařízení může uživatel přejít do nabídky **Nastavení** a funkci nastavit tam.
    - Pokud zvolíte **Zobrazit**, obrazovka se při nastavování zobrazí. Uživatel může obrazovku někdy přeskočit a neudělat žádnou akci. Může ale později přejít do nabídky zařízení **Nastavení** a funkci nastavit tam. 

    | Nastavení na obrazovce Průvodce nastavením | Pokud zvolíte **Zobrazit**, zařízení při nastavování: |
    |------------------------------------------|------------------------------------------|
    | <strong>Heslo</strong> | Vyzve uživatele k zadání hesla. Vždy vyžadovat heslo pro nezabezpečená zařízení, pokud není přístup kontrolován jiným způsobem (například celoobrazovkový režim, který zařízení omezuje na jednu aplikaci). Pro iOS/iPadOS 7,0 a novější. |
    | <strong>Zjišťování polohy</strong> | Vyzve uživatele k poskytnutí polohy. Pro macOS 10,11 a novější a iOS/iPadOS 7,0 a novější. |
    | <strong>Obnovení</strong> | Zobrazí obrazovku aplikace & data. Tato obrazovka nabídne uživateli při nastavování zařízení možnost obnovit nebo přenést data ze zálohy v iCloudu. Pro macOS 10,9 a novější a iOS/iPadOS 7,0 a novější. |
    | <strong>Apple ID</strong> | Umožní uživateli přihlásit se pomocí svého Apple ID a používat iCloud. Pro macOS 10,9 a novější a iOS/iPadOS 7,0 a novější.   |
    | <strong>Podmínky a ujednání</strong> | Požaduje, aby uživatel přijal podmínky a ujednání společnosti Apple. Pro macOS 10,9 a novější a iOS/iPadOS 7,0 a novější. |
    | <strong>Touch ID</strong> | Umožní uživateli nastavit pro zařízení identifikaci otiskem prstu. Pro macOS 10.12.4 a novější a iOS/iPadOS 8,1 a novější. |
    | <strong>Apple Pay</strong> | Umožní uživateli nastavit na zařízení Apple Pay. Pro macOS 10.12.4 a novější a iOS/iPadOS 7,0 a novější. |
    | <strong>Zoom</strong> | Umožní uživateli zvětšit zobrazení při nastavování zařízení. Pro iOS/iPadOS 8,3 a novější. |
    | <strong>Siri</strong> | Umožní uživateli nastavit Siri. Pro macOS 10,12 a novější a iOS/iPadOS 7,0 a novější. |
    | <strong>Diagnostická data</strong> | Zobrazí uživateli obrazovku Diagnostická data. Tato obrazovka umožní uživateli poslat společnosti Apple diagnostická data. Pro macOS 10,9 a novější a iOS/iPadOS 7,0 a novější. |
    | <strong>FileVault</strong> | Zobrazit na uživateli obrazovku šifrování trezoru 2. Pro macOS 10,10 a novější. |
    | <strong>Diagnostika iCloud</strong> | Zobrazit obrazovku analýzy iCloud pro uživatele Pro macOS 10.12.4 a novější. |
    | <strong>Úložiště iCloud</strong> | Zobrazí uživateli iCloud dokumenty a plochu obrazovky. Pro macOS 10.13.4 a novější. |
    | <strong>Tón zobrazení</strong> | Poskytněte uživateli možnost zapnout tónový displej. Pro macOS 10.13.6 a novější a iOS/iPadOS 9.3.2 a novější. |
    | <strong>Příznaky</strong> | Zobrazit obrazovku vzhled pro uživatele Pro macOS 10,14 a novější a iOS/iPadOS 13,0 a novější. |
    | <strong>Evidenc</strong> | Zobrazit registrační obrazovku uživateli Pro macOS 10,9 a novější. |
    | <strong>Čas obrazovky</strong> | Zobrazí obrazovku čas obrazovky. Pro macOS 10,15 a novější a iOS/iPadOS 12,0 a novější. |
    | <strong>Ochrana osobních údajů</strong> | Zobrazit obrazovku ochrany osobních údajů uživateli. Pro macOS 10.13.4 a novější a iOS/iPadOS 11,3 a novější. |
    
9. Kliknutím na tlačítko **Další** přejdete na stránku **Revize + vytvořit** .

10. Pokud chcete profil uložit, zvolte **Vytvořit**.

## <a name="sync-managed-devices"></a>Synchronizace spravovaných zařízení

Teď, když má Intune oprávnění spravovat vaše zařízení, můžete synchronizovat Intune s Apple, aby se spravovaná zařízení zobrazila v Intune na portálu Azure Portal.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **MacOS**  >  **MacOS registrace**  >  **tokenů programu registrace**.

2. Vyberte token v seznamu > **Devices** > **synchronizace**zařízení. ![ Snímek obrazovky s vybraným uzlem zařízení programu registrace a vybraným odkazem pro synchronizaci](./media/device-enrollment-program-enroll-macos/image06.png)

   Pro zajištění souladu s podmínkami společnosti Apple za účelem přijatelného provozu registračního programu ukládá Intune následující omezení:
   - Úplná synchronizace se nesmí pouštět častěji než jednou za sedm dní. Během úplné synchronizace načte Intune úplný aktualizovaný seznam sériových čísel přiřazených k serveru Apple MDM připojenému k Intune. Po odstranění zařízení programu registrace z portálu Intune bez jeho přiřazení ze serveru Apple MDM na portálu Apple se nebude znovu naimportovat do Intune, dokud se nespustí Úplná synchronizace.   
   - Synchronizace se spouští automaticky každých 24 hodin. Můžete ji také spustit kliknutím na tlačítko **Synchronizovat** (ne častěji než jednou za 15 minut). Každá žádost o synchronizaci má 15 minut na dokončení. Tlačítko **Synchronizovat** bude deaktivované, dokud se synchronizace nedokončí. Při synchronizaci se zaktualizuje stav existujících zařízení a naimportují se nová zařízení přiřazená k serveru Apple MDM.

## <a name="assign-an-enrollment-profile-to-devices"></a>Přiřazení profilu registrace zařízením

Než se můžou zařízení zaregistrovat, musíte přiřadit profil programu registrace.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **MacOS**  >  **MacOS registrace**  >  **tokenů programu** > v seznamu vyberte token.
2. Zvolte **Zařízení** > zvolte zařízení v seznamu > **Přiřadit profil**.
3. V části **Přiřadit profil** zvolte profil pro zařízení > **Přiřadit**.

### <a name="assign-a-default-profile"></a>Přiřazení výchozího profilu

Můžete vybrat výchozí macOS a profil iOS/iPadOS, který se použije na všechna zařízení zaregistrovaná pomocí konkrétního tokenu. 

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **MacOS**  >  **MacOS registrace**  >  **tokenů programu** > v seznamu vyberte token.
2. Zvolte **Nastavit výchozí profil**, v rozevíracím seznamu zvolte profil a potom zvolte **Uložit**. Tento profil se použije pro všechna zařízení, která se registrují s tímto tokenem.

## <a name="distribute-devices"></a>Distribuujte zařízení.

Povolili jste správu a synchronizaci mezi společností Apple a Intune a přiřadili jste profil, který umožní registraci zařízení. Teď můžete zařízení rozdělit mezi uživatele. U zařízení s přidruženými uživateli je potřeba, aby měl každý uživatel přiřazenu licenci Intune. Zařízení bez přidružení uživatele vyžadují licenci zařízení. Aktivované zařízení nemůže použít profil registrace, dokud se zařízení nevymaže.

## <a name="renew-an-ade-token"></a>Prodloužit platnost tokenu ADE

1. Přejděte na deploy.apple.com.  
2. V části **Manage Servers** (Spravovat servery) zvolte server MDM přidružený k souboru tokenu, který chcete obnovit.
3. Zvolte **Generate New Token** (Vygenerovat nový token).

    ![Snímek obrazovky s možností Generate New Token (Vygenerovat nový token)](./media/device-enrollment-program-enroll-macos/generatenewtoken.png)

4. Zvolte **Your Server Token** (Token vašeho serveru).  
5. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **registrace zařízení**registrace  >  **Apple**  >  **tokeny programu registrace** > vyberte token.
    ![Snímek obrazovky s možností Tokeny programu registrace](./media/device-enrollment-program-enroll-ios/enrollmentprogramtokens.png)

6. Vyberte možnost **Obnovit token** a zadejte Apple ID, které jste použili k vytvoření původního tokenu.  
    ![Snímek obrazovky s možností Generate New Token (Vygenerovat nový token)](./media/device-enrollment-program-enroll-ios/renewtoken.png)

7. Nahrajte nově stažený token.  
8. Zvolte **Obnovit token**. Zobrazí se potvrzení, že se token obnovil.
    ![Snímek obrazovky s potvrzením](./media/device-enrollment-program-enroll-macos/confirmation.png)

## <a name="next-steps"></a>Další kroky

Po zaregistrování zařízení macOS můžete začít [Spravovat](../remote-actions/device-management.md).