---
title: registrace zařízení s iOS/iPadOS – Apple Configuratoru – Pomocník s nastavením
titleSuffix: Microsoft Intune
description: Naučte se používat Apple Configuratoru k registraci zařízení s iOS a iPadOS vlastněných společností pomocí Pomocníka s nastavením.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/04/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 671e4d76-0c61-11e8-ba89-0ed5f89f718b
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7101ad9bffcd80bd608690f22db37abbbc7a7895
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093783"
---
# <a name="set-up-iosipados-device-enrollment-with-apple-configurator"></a>Nastavení registrace zařízení se systémem iOS/iPadOS pomocí nástroje Apple Configurator

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune podporuje registraci zařízení se systémem iOS/iPadOS pomocí [Apple Configuratoru](https://itunes.apple.com/app/apple-configurator-2/id1037126344) spuštěného na počítači Mac. Registrace pomocí Apple Configuratoru vyžaduje, aby každé zařízení s platformou iOS/iPadOS připojení k počítači Mac pomocí USB a nastavilo registraci podnikového zápisu. Zařízení můžete do služby Intune registrovat pomocí Apple Configuratoru dvěma způsoby:
- **Registrace Pomocníka s nastavením** – Vymaže zařízení a připraví ho k registraci Pomocníka s nastavením.
- **Přímá registrace** – nevymaže zařízení a zaregistruje zařízení prostřednictvím nastavení pro iOS/iPadOS. Tato metoda podporuje jenom **zařízení bez přidružení uživatele**.

Metoda registrace pomocí Apple Configuratoru se nedá použít se [Správcem registrace zařízení](device-enrollment-manager-enroll.md).

## <a name="prerequisites"></a>Požadavky

- Fyzický přístup k zařízením s iOS/iPadOS
- [Nastavení autority pro správu mobilních zařízení (MDM)](../fundamentals/mdm-authority-set.md)
- [Certifikát Apple MDM push certificate](apple-mdm-push-certificate-get.md)
- Sériová čísla zařízení (jenom u registrace Pomocníka s nastavením)
- Propojovací kabely USB
- Počítač s macOS s [Apple Configuratorem 2.0](https://itunes.apple.com/app/apple-configurator-2/id1037126344)

## <a name="create-an-apple-configurator-profile-for-devices"></a>Vytvoření profilu Apple Configuratoru pro zařízení

Profil registrace zařízení definuje nastavení, která se během registrace použijí. Tato nastavení se použijí jenom jednou. Pomocí těchto kroků vytvořte registrační profil pro registraci zařízení se systémem iOS/iPadOS pomocí Apple Configuratoru.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **iOS/iPadOS**  >  **iOS/iPadOS registrace**  >  **Apple Configuratoru**.

    ![Vytvoření profilu pro Apple Configurator](./media/apple-configurator-enroll-ios/apple-configurator.png)

2. Vyberte **profily**  >  **vytvořit**.

3. V části **Vytvořit registrační profil** zadejte **Název** a **Popis** profilu pro účely správy. Uživatelům se tyto údaje nezobrazí. Pole Název můžete využít k vytvoření dynamické skupiny v Azure Active Directory. Název profilu použijte k definování parametru enrollmentProfileName pro přiřazení zařízení s tímto registračním profilem. Přečtěte si další informace o dynamických skupinách Azure Active Directory.

    ![Snímek obrazovky Vytvořit profil s vybranou volbou Zaregistrovat s přidružením uživatele](./media/apple-configurator-enroll-ios/apple-configurator-profile-create.png)

4. V části **Přidružení uživatele** zvolte, jestli se zařízení s tímto profilem musí registrovat s přiřazeným uživatelem nebo bez něj.

    - **Zaregistrovat s přidružením uživatele** – tuto možnost vyberte pro zařízení, která patří uživatelům a chtějí používat portál společnosti pro služby, jako je instalace aplikací. Zařízení musí mít přidruženého uživatele (pomocí Průvodce nastavením), aby mohlo dostat přístup k firemním datům a e-mailu. Tato možnost je podporovaná jenom pro registraci Pomocníka s nastavením. Přidružení uživatelů vyžaduje [koncový bod WS-Trust 1.3 Username/Mixed](https://technet.microsoft.com/library/adfs2-help-endpoints). [Přečtěte si další informace](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint).

    - **Zaregistrovat bez přidružení uživatele** – Tuto možnost zvolte pro zařízení nespojená s jedním uživatelem. Použijte ji pro zařízení určená k plnění úkolů, u kterých není potřeba přístup k místním uživatelským datům. Aplikace, které vyžadují přidružení uživatele (včetně aplikace Portál společnosti používané pro instalaci obchodních aplikací), nebudou fungovat. Vyžaduje se pro přímou registraci.

     > [!NOTE]
     > Když je vybraná možnost **zaregistrovat s přidružením uživatele** , ujistěte se, že je zařízení přidružené k uživateli s průvodcem nastavením během prvních 24 hodin zaregistrovaných zařízení. Jinak může registrace selhat a k registraci zařízení bude potřeba obnovení továrního nastavení.

5. Pokud jste zvolili **Zaregistrovat s přidružením uživatele**, máte možnost povolit, aby se uživatelé ověřovali pomocí portálu společnosti místo v Průvodci nastavením společnosti Apple.

    > [!NOTE]
    > Pokud chcete provést některou z následujících akcí, nastavte možnost **ověření na Portálu společnosti místo v Průvodci nastavením Applu** na **Ano**.
    >    - Použít vícefaktorové ověřování.
    >    - Zobrazit výzvu uživatelům, pokud při prvním přihlášení potřebují změnit heslo.
    >    - Zobrazit výzvu uživatelům, aby při registraci resetovali neplatná hesla.
    >
    > Tato možnost není podporovaná, pokud se k ověření použije Průvodce nastavením společnosti Apple.


6. Uložte profil pomocí tlačítka **Vytvořit**.

## <a name="setup-assistant-enrollment"></a>Registrace Pomocníka s nastavením

### <a name="add-apple-configurator-serial-numbers"></a>Přidání sériových čísel Apple Configuratoru

1. Vytvořte seznam hodnot oddělených čárkami se dvěma sloupci (.csv) bez záhlaví. Do levého sloupce přidejte sériové číslo a v pravém sloupci uveďte podrobnosti. Aktuálně je maximální počet řádků v seznamu 5 000. V textovém editoru vypadá seznam .csv takto:

    F7TLWCLBX196,podrobnosti o zařízení</br>
    DLXQPCWVGHMJ,podrobnosti o zařízení

   Přečtěte si, [Jak najít sériové číslo zařízení se systémem iOS/iPadOS](https://support.apple.com/HT204073).
2. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **iOS/iPadOS**  >  **iOS/iPadOS registrace**  >  **zařízení Apple Configuratoru**  >  **Devices**  >  **Přidat**.

5. Vyberte **profil registrace**, jehož prostřednictvím použijete importovaná sériová čísla. Pokud chcete, aby podrobnosti nového sériového čísla přepsaly všechny existující podrobnosti, zvolte **Přepište podrobnosti u existujících identifikátorů**.
6. V části **Importovat zařízení** přejděte k souboru CSV se sériovými čísly a vyberte **Přidat**.

### <a name="reassign-a-profile-to-device-serial-numbers"></a>Opětovné přiřazení profilu k sériovým číslům zařízení

Registrační profil můžete přiřadit při importu sériových čísel iOS/iPadOS pro registraci Apple Configuratoru. Profily můžete také přiřazovat ze dvou míst na portálu Azure Portal:
- **Zařízení Apple Configuratoru**
- **Profily AC**

#### <a name="assign-from-apple-configurator-devices"></a>Přiřazení v části Zařízení Apple Configuratoru
1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **iOS/iPadOS**  >  **iOS/iPadOS registrace**  >  **zařízení Apple Configuratoru**  >  **Devices** > vyberte sériová čísla > **přiřadit profil**.
2. V části **Přiřadit profil** zvolte **nový profil**, který chcete přiřadit, a pak zvolte **Přiřadit**.

#### <a name="assign-from-profiles"></a>Přiřazení z profilů
1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **iOS/iPadOS**  >  **iOS/iPadOS registrace**  >  **Apple Configuratoru**  >  **profily** > vyberte profil.
2. V profilu zvolte **Přiřazená zařízení** a pak **Přiřadit**.
3. Pomocí filtru vyhledejte sériová čísla zařízení, která chcete k profilu přiřadit, vyberte zařízení a zvolte **Přiřadit**.

### <a name="export-the-profile"></a>Export profilu
Po vytvoření profilu a přiřazení sériových čísel je potřeba profil exportovat z Intune jako adresu URL. Tu pak importujete do Apple Configuratoru na počítači Mac, odkud můžete profil nasadit do zařízení.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **iOS/iPadOS**  >  **iOS/iPadOS registrace**  >  **Apple Configuratoru**  >  **Profiles** > vyberte profil, který chcete exportovat.
2. V profilu vyberte **Exportovat profil**.
3. Zkopírujte **adresu URL profilu**. Pak ho můžete přidat do Apple Configuratoru a definovat profil Intune používaný zařízeními se systémem iOS/iPadOS.

   Při dalším importu tohoto profilu do Apple Configuratoru v následujícím postupu můžete definovat profil Intune používaný zařízeními se systémem iOS/iPadOS.

### <a name="enroll-devices-with-setup-assistant"></a>Registrace zařízení s využitím Pomocníka s nastavením

1. Na počítači Mac otevřete **Apple Configurator 2**. V panelu nabídek vyberte **Apple Configurator 2** a potom **Předvolby**.
    > [!WARNING]
    > V průběhu registrace se v zařízeních obnoví tovární konfigurace. Doporučuje se zařízení resetovat a zapnout ho. Zařízení by při připojení měla mít nastavenou **úvodní obrazovku**.
    > Pokud je zařízení už zaregistrované u účtu Apple ID, musí se před zahájením procesu registrace odstranit ze zařízení Apple iCloud. Chyba výzvy se zobrazí jako "nelze aktivovat [název zařízení]".

2. V podokně **Předvolby** vyberte **servery** a kliknutím na symbol plus (+) spusťte Průvodce serveru MDM. Zvolte **Další**.
3. V části registrace Průvodce nastavením pro zařízení Microsoft Intune s iOS/iPadOS zadejte **název hostitele nebo adresu URL** a **adresu URL pro registraci** serveru MDM. Jako adresu URL pro registraci zadejte adresu URL profilu pro registraci exportovanou z Intune. Zvolte **Další**.  
    Upozornění na neověřenou adresu URL serveru můžete ignorovat. Vyberte **Další** a pokračujte až do konce průvodce.
4. Připojte mobilní zařízení s iOS/iPadOS k počítači Mac pomocí adaptéru USB.
5. Vyberte zařízení s iOS/iPadOS, která chcete spravovat, a pak zvolte **připravit**. V podokně **připravit zařízení se systémem iOS/iPadOS** vyberte možnost **ručně**a pak zvolte možnost **Další**.
6. V podokně **Enroll in MDM Server** (Registrovat na serveru MDM) vyberte název vytvořeného serveru a zvolte **Next** (Další).
7. V podokně **Supervise Devices** (Dohled nad zařízeními) vyberte úroveň dohledu a potom vyberte **Další**.
8. V podokně **Create an Organization** (Vytvořit organizaci) zvolte **organizaci** nebo vytvořte novou organizaci a pak zvolte **Next** (Další).
9. V podokně **Konfigurace pomocníka s nastavením pro iOS/iPadOS** vyberte kroky, které chcete uživateli předložit, a pak zvolte **připravit**. Pokud se zobrazí výzva, proveďte ověření, aby se aktualizovalo nastavení důvěry.  
10. Až se dokončí příprava zařízení s iOS/iPadOS, odpojte kabel USB.  

### <a name="distribute-devices"></a>Distribuujte zařízení.
Zařízení jsou připravená na registraci ve společnosti. Vypněte zařízení a rozdejte je uživatelům. Když uživatelé zařízení zapnou, spustí se Pomocník s nastavením.

Po převzetí zařízení musí uživatelé projít postupem Pomocníka s nastavením. Zařízení nakonfigurovaná s přidružením uživatele umožňují instalaci a spuštění aplikace Portál společnosti, která slouží ke stahování aplikací a správě zařízení.

## <a name="direct-enrollment"></a>Přímá registrace
Při přímé registraci zařízení s iOS/iPadOS pomocí Apple Configuratoru můžete zaregistrovat zařízení bez získání sériového čísla zařízení. Můžete také zařízení pro potřeby identifikace pojmenovat před tím, než Intune zachytí název zařízení během registrace. U zařízení zaregistrovaných přímo není podporovaná aplikace Portál společnosti. Pomocí této metody se zařízení nevymaže.

Aplikace, které vyžadují přidruženého uživatele (včetně aplikace Portál společnosti používané k instalaci obchodních aplikací), se nedají nainstalovat.

### <a name="export-the-profile-as-mobileconfig-to-iosipados-devices"></a>Exportovat profil jako. mobileconfig do zařízení se systémem iOS/iPadOS

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **iOS/iPadOS**  >  **iOS/iPadOS registrace**  >  **Apple Configuratoru**  >  **profily** > vyberte profil pro export > **exportovat profil**.
2. V části **Přímá registrace** zvolte **Stáhnout profil** a soubor uložte. Soubor registračního profilu je platný jenom po dobu dvou týdnů, po které ho bude nutné znovu vytvořit.
3. Přeneste soubor do počítače Mac, na kterém běží [Apple Configuratoru](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) , a nahrajte ho přímo jako profil pro správu do zařízení se systémem iOS/iPadOS.
4. Připravte zařízení pomocí Apple Configuratoru podle následujících kroků:
    1. Na počítači Mac otevřete Apple Configurator 2.0.
    2. Připojte zařízení s iOS/iPadOS k počítači Mac pomocí kabelu USB. Zavřete Fotky, iTunes a další aplikace, které se otevřou při zjištění zařízení.
    3. V Apple Configuratoru zvolte připojené zařízení se systémem iOS/iPadOS a pak klikněte na tlačítko **Přidat** . V rozevíracím seznamu se zobrazí možnosti, které se dají přidat do zařízení. Vyberte **Profily**.

        ![Snímek obrazovky Exportovat profil pro registraci Pomocníka s nastavením se zvýrazněnou adresou URL profilu](./media/apple-configurator-enroll-ios/ios-apple-configurator-add-profile.png)

    4. Pomocí nástroje pro výběr souborů vyberte soubor .mobileconfig, který jste exportovali z Intune, a zvolte **Přidat**. Profil se přidá do zařízení. Pokud má zařízení nastavenou možnost Bez dohledu, vyžaduje instalace přijetí na zařízení.
5. Pomocí následujících kroků nainstalujte profil na zařízení se systémem iOS/iPadOS. Je potřeba, aby už byl v zařízení dokončený Pomocník s nastavením a aby bylo připravené k použití. Pokud registrace zahrnuje nasazení aplikací, zařízení by mělo mít nastavené Apple ID, protože při nasazení aplikace bude potřeba přihlásit se do App Storu pomocí Apple ID.
    1. Odemkněte zařízení s iOS/iPadOS.
    2. V dialogovém okně **Nainstalovat profil** pro **Profil správy** zvolte **Instalovat**.
    3. V případě potřeby zadejte heslo zařízení nebo Apple ID.
    4. Potvrďte **upozornění** a zvolte **Instalovat**.
    5. Potvrďte **vzdálené upozornění** a zvolte **Důvěřovat**.
    6. Když se v okně **profil nainstalován** potvrdí, že se profil nainstaloval, klikněte na **Hotovo**.

6. Na zařízení se systémem iOS/iPadOS otevřete **Nastavení** a přejdete na **Obecné**  >  **Device Management**  >  **Profil správy**správy zařízení. Potvrďte, že je uvedená instalace profilu, a zkontrolujte omezení zásad pro iOS/iPadOS a nainstalované aplikace. Zobrazení omezení vyplývajících ze zásad a aplikací na zařízení může trvat až 10 minut.

7. Distribuujte zařízení. Zařízení s iOS/iPadOS je teď zaregistrované v Intune a spravované.





