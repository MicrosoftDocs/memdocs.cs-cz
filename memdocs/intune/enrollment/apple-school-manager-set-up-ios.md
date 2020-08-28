---
title: Registrace programu Apple School Manager pro zařízení s iOS/iPadOS
titleSuffix: Microsoft Intune
description: Naučte se, jak pomocí Intune nastavit registraci programu Apple School Manager pro zařízení s iOS a iPadOS vlastněná společností.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 4c35a23e-0c61-11e8-ba89-0ed5f89f718b
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 431dc3fec49609c4f163c9d7f471b60565611bc3
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/27/2020
ms.locfileid: "88992833"
---
# <a name="set-up-iosipados-device-enrollment-with-apple-school-manager"></a>Nastavení registrace zařízení se systémem iOS/iPadOS pomocí Apple School Manageru

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Můžete nastavit Intune pro registraci zařízení se systémem iOS/iPadOS zakoupených prostřednictvím programu [Apple School Manager](https://school.apple.com/) . Pomocí Intune s Apple School Managerem můžete registrovat velké počty zařízení s iOS/iPadOS, aniž byste je museli dotýkat. Když student nebo učitel zařízení zapne, Pomocník s nastavením provede předem nakonfigurovaná nastavení a zařízení se zaregistruje ke správě.

Při povolení registrace přes Apple School Manager budete používat portál Intune i portál Apple School Manager. Abyste mohli zařízení přiřadit do Intune ke správě, potřebujete seznam sériových čísel nebo čísla nákupních objednávek. Vytvoříte profily zápisu automatizovaného zápisu zařízení (ADE), které obsahují nastavení, která se v zařízeních při registraci používala.

Registraci Apple School Manageru nejde použít s [automatickým zápisem zařízení ](device-enrollment-program-enroll-ios.md) (DEP) společnosti Apple ani se [správcem registrace zařízení](device-enrollment-manager-enroll.md).

**Požadavky**
- [Nabízený certifikát pro správu mobilních zařízení Apple (MDM)](apple-mdm-push-certificate-get.md)
- [Autorita MDM](../fundamentals/mdm-authority-set.md)
- Při použití ADFS vyžaduje přidružení uživatelů [koncový bod WS-Trust 1.3 Username/Mixed](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff608241(v=ws.10)). [Přečtěte si další informace](/powershell/module/adfs/get-adfsendpoint?view=win10-ps).
- Zařízení zakoupená z programu [Apple School Management](http://school.apple.com)

## <a name="get-an-apple-token-and-assign-devices"></a>Získání tokenu Apple a přiřazení zařízení

Než budete moct pomocí Apple School Manageru registrovat zařízení s iOS a iPadOS vlastněná společností, potřebujete od společnosti Apple soubor tokenu (. p7m). Tento token umožňuje Intune synchronizovat informace o zařízeních v Apple School Manageru. Token také umožňuje Intune odesílat společnosti Apple registrační profily a přiřazovat k těmto profilům zařízení. Na portálu společnosti Apple můžete také přiřadit sériová čísla zařízení pro správu.

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-an-apple-token"></a>Krok 1. Stáhněte si certifikát veřejného klíče Intune, který je potřebný k vytvoření tokenu Apple.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **iOS/iPadOS**  >  **iOS/iPadOS registrace**  >  **tokeny programu registrace**  >  **Přidat**.

   ![Stažení tokenu programu registrace zařízení](./media/apple-school-manager-set-up-ios/image01.png)

2. V okně **Token Programu registrace** zvolte **Stáhnout veřejný klíč** a stáhněte a místně uložte soubor šifrovacího klíče (.pem). Soubor .pem slouží k vyžádání certifikátu vztahu důvěryhodnosti z portálu Apple School Manager.
     ![Podokno Token Programu registrace zařízení](./media/apple-school-manager-set-up-ios/image02.png)

### <a name="step-2-download-a-token-and-assign-devices"></a>Krok 2. Stáhněte si token a přiřaďte zařízení.
1. Zvolte **Vytvořit token prostřednictvím Apple School Manageru** a přihlaste se k Apple School pomocí Apple ID vaší společnosti. Toto Apple ID můžete použít k obnovení tokenu Apple School Manageru.
2. Na portálu [Apple School Manager](https://school.apple.com) přejděte na **MDM Servers** (MDM servery) a vpravo nahoře zvolte **Add MDM Server** (Přidat MDM server).
3. Zadejte **název MDM serveru**. Název serveru slouží pro vaši informaci, abyste mohli identifikovat server pro správu mobilních zařízení (MDM). Nejedná se o název nebo adresu URL serveru Microsoft Intune.
   ![Snímek obrazovky portálu Apple School Manager s vybranou možností Sériové číslo](./media/apple-school-manager-set-up-ios/asm-server-assignment.png)

4. Na portálu společnosti Apple zvolte **Upload File...** (Nahrát soubor...), vyhledejte soubor .pem a vpravo dole zvolte **Save MDM Server** (Uložit MDM server).
5. Zvolte **Get Token** (Získat token) a stáhněte si soubor tokenu serveru (.p7m) do svého počítače.
6. Přejděte na **Device Assignments** (Přiřazení zařízení) a **vyberte zařízení** pomocí možností **Serial Numbers** (Sériová čísla), **Order Number** (Číslo objednávky) nebo **Upload CSV File** (Nahrát CSV soubor).
     ![Snímek obrazovky portálu Apple School Manager s vybranou možností Sériové číslo](./media/apple-school-manager-set-up-ios/asm-device-assignment.png)
7. Zvolte akci **Assign to Server** (Přiřadit k serveru) a zvolte **MDM Server**, který jste vytvořili.
8. Určete, jak **Vybrat zařízení**, a pak zadejte informace o zařízení a podrobnosti.
9. Zvolte **Assign to Server** (Přiřadit k serveru), zvolte &lt;název serveru&gt; zadaný pro Microsoft Intune a potom zvolte **OK**.

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>Krok 3. Uložte si Apple ID, které jste použili k vytvoření tohoto tokenu.

V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)zadejte Apple ID pro budoucí referenci.

![Snímek obrazovky s Apple ID použitým k vytvoření tokenu programu registrace a přechodem na token programu registrace](./media/apple-school-manager-set-up-ios/image03.png)

### <a name="step-4-upload-your-token"></a>Krok 4: Nahrajte token.
V poli **Token Apple** přejděte k souboru certifikátu (.pem), zvolte **Otevřít** a pak zvolte **Vytvořit**. Pomocí nabízeného certifikátu může Intune registrovat a spravovat zařízení s iOS/iPadOS tím, že zapisuje zásady do zaregistrovaných mobilních zařízení. Intune automaticky synchronizuje vaše zařízení Apple School Manageru z portálu společnosti Apple.

## <a name="create-an-apple-enrollment-profile"></a>Vytvoření registračního profilu Apple
Po nainstalování tokenu můžete vytvořit registrační profil pro zařízení Apple School. Registrační profil zařízení definuje nastavení, která se během registrace použijí pro skupinu zařízení.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **iOS/iPadOS**  >  **iOS/iPadOS**  >  **tokeny programu registrace**.
2. Vyberte token, zvolte **Profily** a potom zvolte **Vytvořit profil**.

3. V části **Vytvořit profil** zadejte **Název** a **Popis** profilu pro účely správy. Uživatelé tyto podrobnosti nevidí. Pole **Název** můžete využít k vytvoření dynamické skupiny v Azure Active Directory. Název profilu použijte k definování parametru enrollmentProfileName pro přiřazení zařízení s tímto registračním profilem. Přečtěte si další informace o [Azure Active Directory dynamických skupinách](/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal#rules-for-devices).

    ![Název a popis profilu](./media/apple-school-manager-set-up-ios/image05.png)

4. V části **Přidružení uživatele** zvolte, jestli se zařízení s tímto profilem musí registrovat s přiřazeným uživatelem nebo bez něj.
    - **Zaregistrovat s přidružením uživatele** – Tuto možnost zvolte pro zařízení, která patří uživatelům a chtějí pro služby, jako je instalace aplikací, používat portál společnosti. Tato možnost také umožňuje uživatelům ověřovat svoje zařízení pomocí portálu společnosti. Při použití ADFS vyžaduje přidružení uživatelů [koncový bod WS-Trust 1.3 Username/Mixed](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff608241(v=ws.10)). [Přečtěte si další informace](/powershell/module/adfs/get-adfsendpoint?view=win10-ps).   Režim Sdílený iPad programu Apple School Manager vyžaduje registraci uživatele bez přidružení uživatele.

    - **Zaregistrovat bez přidružení uživatele** – Tuto možnost zvolte pro zařízení nespojená s jedním uživatelem, například sdílená zařízení. Použijte ji pro zařízení určená k plnění úkolů, u kterých není potřeba přístup k místním uživatelským datům. Aplikace, jako je Portál společnosti aplikace, nefungují.

5. Pokud jste zvolili možnost **registrovat s přidružením uživatele**, můžete uživatelům povolit ověřování pomocí portál společnosti namísto pomocníka s nastavením Apple.

    ![Ověření pomocí portálu společnosti](./media/apple-school-manager-set-up-ios/authenticatewithcompanyportal.png)

    > [!NOTE]
    > Pokud chcete provést některou z následujících akcí, nastavte možnost **ověření na Portálu společnosti místo v Průvodci nastavením Applu** na **Ano**.
    >    - Použít vícefaktorové ověřování.
    >    - Zobrazit výzvu uživatelům, pokud při prvním přihlášení potřebují změnit heslo.
    >    - Zobrazit výzvu uživatelům, aby při registraci resetovali neplatná hesla.
    >
    > Ty nejsou podporované při ověřování pomocí Pomocníka s nastavením Apple.

6. Vyberte **Nastavení správy zařízení** a vyberte, jestli chcete, aby byla zařízení, která používají tento profil, pod dohledem.
    U zařízení **pod dohledem** je ve výchozím nastavení víc možností správy a je zakázaný zámek aktivace. Microsoft doporučuje použít ADE jako mechanismus pro povolení režimu pod dohledem v Intune, zejména pro organizace, které nasazují velký počet zařízení s iOS/iPadOS.

    Uživatelé se dozvědí, že jejich zařízení jsou pod dohledem, dvěma způsoby:

   - Na zamykací obrazovce se zobrazí oznámení: „Tento iPhone spravuje Contoso.“
   - **Nastavení**  >  **Obecné**  >  **o** obrazovce říká: "Tento iPhone je pod dohledem. Společnost Contoso může monitorovat internetové přenosy a zařízení vyhledat.“

     > [!NOTE]
     > Zařízení zaregistrované bez dohledu se dá resetovat do stavu pod dohledem jenom pomocí Apple Configuratoru. Resetování zařízení tímto způsobem vyžaduje připojení zařízení s iOS/iPadOS k počítači Mac pomocí kabelu USB. Další informace na toto téma získáte v [dokumentaci Apple Configuratoru](http://help.apple.com/configurator/mac/2.3).

7. Vyberte, jestli chcete pro zařízení, která používají tento profil, uzamčenou registraci. **Uzamčená registrace** zakáže nastavení pro iOS/iPadOS, která umožňují odebrání profilu správy z nabídky **Nastavení** . Po registraci zařízení toto nastavení nemůžete změnit bez vymazání zařízení. Taková zařízení musí mít režim správy **Pod dohledem** nastavený na *Ano*. 

8. Přihlášení k zaregistrovaným iPady pomocí spravovaného Apple ID se dá dát více uživatelům. Uděláte to tak, že v části **sdílený iPad** kliknete na **Ano** (Tato možnost vyžaduje **zápis bez přidružení uživatele** a režim **pod dohledem** nastavený na **Ano**). Spravovaná Apple ID se vytvářejí na portálu Apple School Manager. Další informace o [sdíleném iPadu](../fundamentals/education-settings-configure-ios-shared.md) a [požadavcích Applu na sdílený iPad](https://help.apple.com/classroom/ipad/2.0/#/cad7e2e0cf56)

9. Vyberte, jestli chcete, aby zařízení, která používají tento profil, mohla **synchronizovat s počítači**. **Deny All** znamená, že všechna zařízení, která používají tento profil, nebudou moct synchronizovat s daty z libovolného počítače. Pokud vyberete **Povolit Apple Configurator podle certifikátu**, musíte zvolit certifikát v části **Certifikáty Apple Configuratoru**.

10. Pokud jste v předchozím kroku zvolili **Povolit Apple Configurator podle certifikátu**, zvolte certifikát Apple Configuratoru, který se má importovat.

11. Můžete zadat formát názvů pro zařízení, která se při registraci automaticky používají. Provedete to tak, že v části **použít šablonu názvu zařízení**vyberete **Ano** . Pak v poli **šablona názvu zařízení** zadejte šablonu, která se má použít pro názvy používané tímto profilem. Můžete zadat formát šablony, který zahrnuje typ zařízení a sériové číslo.

12. Vyberte **OK**.

13. Zvolte **Nastavení Průvodce nastavením** a nakonfigurujte následující nastavení profilu: ![Přizpůsobení Průvodce nastavením](./media/apple-school-manager-set-up-ios/setupassistantcustom.png).


    |                 Nastavení                  |                                                                                               Popis                                                                                               |
    |------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    |     <strong>Department Name</strong>     |                                                             Zobrazí se, když uživatelé klepnou při aktivaci na <strong>O konfiguraci</strong>.                                                              |
    |    <strong>Telefon na oddělení</strong>     |                                                          Zobrazí se, když uživatel při aktivaci klikne na tlačítko <strong>Potřebuji nápovědu</strong>.                                                          |
    | <strong>Možnosti Průvodce nastavením</strong> |                                                     Následující volitelná nastavení se dají nastavit později v nabídce <strong>Nastavení</strong> pro iOS/iPadOS.                                                      |
    |        <strong>Heslo</strong>         | Při aktivaci se zobrazí výzva k zadání hesla. Vždy vyžadovat heslo pro nezabezpečená zařízení, pokud není přístup kontrolován jiným způsobem (například celoobrazovkový režim, který zařízení omezuje na jednu aplikaci). |
    |    <strong>Zjišťování polohy</strong>    |                                                                 V případě povolení Průvodce nastavením zobrazí během aktivace výzvu pro tuto službu.                                                                  |
    |         <strong>Obnovení</strong>         |                                                                Pokud je toto nastavení povolené, Průvodce nastavením zobrazí při aktivaci výzvu k zálohování na iCloud.                                                                 |
    |   <strong>iCloud a Apple ID</strong>   |                         Pokud je toto nastavení povolené, Průvodce nastavením vyzve uživatele k přihlášení Apple ID a na obrazovce Aplikace a data bude možné obnovit zařízení ze zálohy na iCloudu.                         |
    |  <strong>Podmínky a ujednání</strong>   |                                                   V případě povolení Průvodce nastavením vyzve uživatele k přijetí podmínek a ujednání společnosti Apple během aktivace.                                                   |
    |        <strong>Touch ID</strong>         |                                                                 V případě povolení Průvodce nastavením zobrazí během aktivace výzvu pro tuto službu.                                                                 |
    |        <strong>Apple Pay</strong>        |                                                                 V případě povolení Průvodce nastavením zobrazí během aktivace výzvu pro tuto službu.                                                                 |
    |          <strong>Zoom</strong>           |                                                                 V případě povolení Průvodce nastavením zobrazí během aktivace výzvu pro tuto službu.                                                                 |
    |          <strong>Siri</strong>           |                                                                 V případě povolení Průvodce nastavením zobrazí během aktivace výzvu pro tuto službu.                                                                 |
    |     <strong>Diagnostická data</strong>     |                                                                 V případě povolení Průvodce nastavením zobrazí během aktivace výzvu pro tuto službu.                                                                 |


14. Vyberte **OK**.

15. Pokud chcete profil uložit, zvolte **Vytvořit**.

## <a name="connect-school-data-sync"></a>Připojení služby School Data Sync
(Volitelné) Apple School Manager podporuje synchronizaci třídních seznamů do Azure Active Directory (AD) pomocí služby Microsoft School Data Sync (SDS). Pomocí SDS můžete synchronizovat jenom jeden token. Pokud pomocí School Data Sync nastavíte další token, odebere se SDS z tokenu, který měl SDS předtím. Nové připojení nahradí aktuální token. Pokud chcete použít službu SDS k synchronizaci školních dat, proveďte následující kroky.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **iOS/iPadOS**  >  **iOS/iPadOS**  >  **tokeny programu registrace**.
2. Vyberte token Apple School Manageru a potom zvolte **Synchronizace školních dat**.
3. V části **Synchronizace školních dat** zvolte **Povolit**. Toto nastavení umožňuje službě Intune připojení k SDS v Microsoft 365.
4. Pokud chcete povolit připojení mezi Apple School Managerem a Azure AD, vyberte **nastavit Microsoft School data Sync**. Přečtěte si další informace o [tom, jak nastavit synchronizaci školních dat](https://support.office.com/article/Install-the-School-Data-Sync-Toolkit-8e27426c-8c46-416e-b0df-c29b5f3f62e1).
5. Klikněte na **Uložit**  >  **OK**.

## <a name="sync-managed-devices"></a>Synchronizace spravovaných zařízení

Až ke službě Intune přiřadíte oprávnění ke správě zařízení Apple School Manageru, synchronizujte Intune se službou Apple, aby se spravovaná zařízení zobrazila v Intune.

V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **iOS/iPadOS**  >  **iOS/iPadOS**  >  **tokeny programu registrace** , > v seznamu > synchronizace zařízení vyberte token **Devices**  >  **Sync**. ![ Snímek obrazovky uzlu zařízení programu registrace a odkaz na synchronizaci.](./media/device-enrollment-program-enroll-ios/image06.png)

Pokud chcete dodržovat podmínky společnosti Apple pro přijatelný provoz programu registrace, Intune ukládá tato omezení:
- Úplná synchronizace se nesmí pouštět častěji než jednou za sedm dní. Během úplné synchronizace Intune aktualizuje všechna sériová čísla Apple přiřazená Intune. Pokud se během sedmi dnů od předchozí úplné synchronizace pokusí se Úplná synchronizace, aktualizuje Intune jenom sériová čísla, která ještě nejsou uvedená v Intune.
- Každá žádost o synchronizaci má 15 minut na dokončení. Po tuto dobu nebo do úspěšného vykonání požadavku je tlačítko **Synchronizovat** neaktivní.
- Intune synchronizuje nová a odebraná zařízení se společností Apple každých 24 hodin.

>[!NOTE]
>V okně **Zařízení Programu registrace** můžete také přiřadit sériová čísla Apple School Manageru k profilům.

## <a name="assign-a-profile-to-devices"></a>Přiřazení profilu k zařízením
Zařízení Apple School Manageru spravovaná přes Intune musí mít před registrací přiřazený registrační profil.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **iOS/iPadOS**  >  **iOS/iPadOS**  >  **tokeny programu registrace** > v seznamu vyberte token.
2. Zvolte **Zařízení** > zvolte zařízení v seznamu > **Přiřadit profil**.
3. V části **přiřadit profil**zvolte profil pro zařízení a pak zvolte **přiřadit**.

## <a name="distribute-devices-to-users"></a>Distribuce zařízení uživatelům

Povolili jste správu a synchronizaci mezi společností Apple a Intune a přiřadili jste profil, který umožní registraci zařízení Apple School. Teď můžete zařízení rozdělit mezi uživatele. Když je zařízení Apple School Manageru pro iOS/iPadOS zapnuté, zaregistruje se pro správu službou Intune. Profily nelze použít na aktivované zařízení, která jsou aktuálně používána, dokud nebude vymazáno zařízení.