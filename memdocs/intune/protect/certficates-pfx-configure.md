---
title: Použití privátních certifikátů a certifikátů veřejných klíčů v Microsoft Intune – Azure | Microsoft Docs
description: Použijte certifikáty PKCS (Public Key Cryptography Standards) s Microsoft Intune, pracujte s kořenovými certifikáty a šablonami certifikátů, nainstalujte konektor Microsoft Intune (NDES) a použijte profily konfigurace zařízení pro certifikát PKCS.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/21/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 02212ddeb4c2522738389c152c038e59fe1db92b
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2020
ms.locfileid: "90814881"
---
# <a name="configure-and-use-pkcs-certificates-with-intune"></a>Konfigurace a používání certifikátů PKCS pomocí Intune

Intune podporuje použití privátních certifikátů a certifikátů PKCS (Public Key párové). Tento článek vám může při konfiguraci požadované infrastruktury, jako jsou místní Certificate connectory, exportovat certifikát PKCS a pak certifikát přidat do profilu konfigurace zařízení v Intune.

Microsoft Intune zahrnuje vestavěná nastavení pro používání certifikátů PKCS pro přístup k prostředkům vaší organizace a jejich ověřování. Certifikáty ověřují a zabezpečují přístup k podnikovým prostředkům, jako je síť VPN nebo Wi-Fi. Tato nastavení nasadíte do zařízení pomocí profilů konfigurace zařízení v Intune.

Informace o použití importovaných certifikátů PKCS najdete v tématu [importované certifikáty PFX](certificates-imported-pfx-configure.md).


## <a name="requirements"></a>Požadavky

Pokud chcete používat certifikáty PKCS s Intune, musíte mít následující infrastrukturu:

- **Doména služby Active Directory**:  
  Všechny servery uvedené v této části se musí připojit k doméně služby Active Directory.

  Další informace o instalaci a konfiguraci Active Directory Domain Services (služba AD DS) najdete v článku [Služba AD DS návrh a plánování](/windows-server/identity/ad-ds/plan/ad-ds-design-and-planning).

- **Certifikační autorita**:  
   Certifikační autorita organizace (CA).

  Informace o tom, jak nainstalovat a nakonfigurovat službu AD CS (Active Directory Certificate Services), najdete v [podrobné příručce ke službě Active Directory Certificate Services](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772393(v=ws.10)).

  > [!WARNING]  
  > Intune vyžaduje, abyste službu AD CS spustili pomocí certifikační autority (CA) organizace, nikoli pomocí samostatné certifikační autority.

- **Klient**:  
  Pro připojení k certifikační autoritě organizace.

- **Kořenový certifikát**:  
  Je třeba mít vyexportovanou kopii kořenového certifikátu z vaší certifikační autority organizace.

- **Konektor certifikátu PFX pro Microsoft Intune**:

  Informace o konektoru certifikátů PFX, včetně požadavků a verzí vydání, najdete v tématu [konektory certifikátů](certificate-connectors.md).

  > [!IMPORTANT]
  > Počínaje verzí konektoru PFX Certificate Connector verze 6.2008.60.607 již není pro profily certifikátů PKCS vyžadován konektor Microsoft Intune. 
  
## <a name="export-the-root-certificate-from-the-enterprise-ca"></a>Export kořenového certifikátu z certifikační autority organizace

K ověření zařízení pomocí sítě VPN, Wi-Fi nebo jiných prostředků potřebuje zařízení kořenový certifikát nebo certifikát zprostředkující certifikační autority. Následující kroky popisují, jak získat požadovaný certifikát z certifikační autority organizace.

**Použijte příkazový řádek**:  

1. Přihlaste se ke kořenovému serveru certifikační autority pomocí účtu správce.

2. Přejděte na **Spustit**  >  **běh**a pak zadáním **cmd** otevřete příkazový řádek.

3. Zadáním **příkazu certutil-CA. cert CA_NAME. cer** exportujte kořenový certifikát jako soubor s názvem *CA_NAME. cer*.

## <a name="configure-certificate-templates-on-the-ca"></a>Konfigurace šablon certifikátů v certifikační autoritě

1. Přihlaste se do certifikační autority organizace pomocí účtu, který má oprávnění správce.
2. Otevřete konzolu **Certifikační autorita** klikněte pravým tlačítkem myši na **Šablony certifikátů** a vyberte **Spravovat**.
3. Vyhledejte šablonu certifikátu **uživatel** , klikněte na ni pravým tlačítkem myši a vyberte možnost **Duplikovat šablonu** , čímž otevřete **Vlastnosti nové šablony**.

    > [!NOTE]
    > K podepisování a šifrování e-mailů pomocí S/MIME používá mnoho správců samostatné certifikáty pro podepisování a šifrování. Pokud používáte službu Microsoft Active Directory Certificate Services, můžete pro podpisové certifikáty e-mailu S/MIME použít šablonu **Pouze podpis serveru Exchange** a pro šifrovací certifikáty S/MIME můžete použít šablonu **Uživatel serveru Exchange**.  Pokud používáte certifikační autoritu třetí strany, doporučujeme vám projít si pokyny k nastavení podpisových a šifrovacích šablon.

4. Na kartě **Kompatibilita** :

    - Nastavte pole **Certifikační autorita** na **Windows Server 2008 R2**.
    - Nastavte pole **Příjemce certifikátu** na **Windows 7 / Server 2008 R2**.

5. Na kartě **Obecné** nastavte **Zobrazovaný název šablony**. Použijte popisný název.

    > [!WARNING]
    > **Název šablony** je ve výchozím nastavení stejný jako **Zobrazovaný název šablony**, pouze *bez mezer*. Poznamenejte si název šablony, budete ho potřebovat později.

6. Ve **Vyřízení žádosti** vyberte **Umožnit export soukromého klíče**.

    > [!NOTE]
    > V rozporu s protokolem SCEP se ve formátu PKCS vygeneruje privátní klíč certifikátu na serveru, na kterém je konektor nainstalovaný, a ne na zařízení. Je nutné, aby šablona certifikátu mohla exportovat soukromý klíč, aby konektor Certificate Connector mohl exportovat certifikát PFX a odeslat ho do zařízení. 
    >
    > Upozorňujeme ale, že certifikáty se nainstalují do samotného zařízení s tímto privátním klíčem, který je označený jako exportovatelný.

7. V **Kryptografii** zkontrolujte, že je **Minimální velikost klíče** nastavená na hodnotu 2048.
8. V **Názvu subjektu** zvolte **Dodat v žádosti**.
9. V **Rozšíření** zkontrolujte, jestli jsou v rozšíření **Zásady použití** položky Šifrování systému souborů, Zabezpečení e-mailu a Ověření klienta.

    > [!IMPORTANT]
    > V případě šablon certifikátů pro iOS/iPadOS otevřete kartu **rozšíření** , aktualizujte **použití klíče**a potvrďte, že není vybraná možnost **podpis je důkazem původu** .

10. V části **zabezpečení**přidejte účet počítače pro server, na který instalujete konektor Microsoft Intune. Pro tento účet povolte oprávnění **Číst** a **Zaregistrovat**.
11. Kliknutím na tlačítko **použít**  >  **OK** uložte šablonu certifikátu. Zavřete **konzolu šablony certifikátů**.
12. V konzole **Certifikační autorita** klikněte pravým tlačítkem myši na **Šablony certifikátů** > **Nová** > **Vystavovaná šablona certifikátu**. Zvolte šablonu, kterou jste vytvořili v předchozím postupu. Vyberte **OK**.
13. Aby server spravoval certifikáty pro zaregistrovaná zařízení a uživatele, použijte následující postup:

    1. Klikněte pravým tlačítkem na certifikační autoritu a potom vyberte **Vlastnosti**.
    2. Na kartě zabezpečení přidejte účet počítače serveru, na kterém konektory spouštíte (konektor**Microsoft Intune** nebo **PFX Certificate Connector pro Microsoft Intune**). 
    3. Udělte oprávnění účtu počítače, která povolují **Vydávat a spravovat certifikáty** a **Vyžádat certifikáty**.

14. Odhlaste se z certifikační autority organizace.

## <a name="download-install-and-configure-the-pfx-certificate-connector"></a>Stažení, instalace a konfigurace konektoru certifikátů PFX

Než začnete, [Zkontrolujte požadavky konektoru](certificate-connectors.md) a ujistěte se, že vaše prostředí a Windows Server jsou připravené k podpoře konektoru.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte možnost konektory **pro správu tenanta**  >  **a tokeny**  >  **Certificate Connectors**  >  **+ Add**.

3. Klikněte na *Stáhnout software Certificate Connector* pro konektor pro PKCS #12 a uložte soubor do umístění, ke kterému máte přístup ze serveru, na který budete konektor instalovat.

   ![Stažení konektoru Microsoft Intune](./media/certficates-pfx-configure/download-connector.png)

4. Po dokončení stahování se přihlaste k serveru a spusťte instalační program (PfxCertificateConnectorBootstrapper.exe).  
   - Když přijmete výchozí umístění instalace, konektor se nainstaluje do `Program Files\Microsoft Intune\PFXCertificateConnector` .
   - Služba konektoru běží pod místním systémovým účtem. Pokud je pro přístup k Internetu vyžadován proxy server, ověřte, že účet místní služby má přístup k nastavení proxy serveru.

5. Konektor certifikátu PFX pro Microsoft Intune se po instalaci otevře na kartě **Zápis**. Pokud chcete povolit připojení k Intune, **přihlaste se** a zadejte účet s globálním oprávněním správce pro Azure nebo s oprávněním správce pro Intune.

   > [!WARNING]
   > Ve výchozím nastavení je **Konfigurace rozšířeného zabezpečení** Windows serveru IE nastavená na **zapnuto** , což může způsobit problémy s přihlášením k Office 365.

6. Vyberte kartu **účet certifikační autority** a potom zadejte přihlašovací údaje pro účet, který má oprávnění vydávat a spravovat certifikáty ve vaší vydávající certifikační autoritě. Tyto přihlašovací údaje budou použity k odvolání certifikátu u certifikační autority. 

    Provedené změny **použijte**.

7. Zavřete okno.

8. V centru pro správu Microsoft Endpoint Manageru se vraťte k konektorům **pro správu tenanta**  >  **a tokenům**  >  **certifikátů**. Za chvíli se zobrazí zelená značka zaškrtnutí a aktualizuje se stav připojení. Server konektoru teď může komunikovat s Intune.

## <a name="create-a-trusted-certificate-profile"></a>Vytvoření profilu důvěryhodného certifikátu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte a přejdete na konfigurace **zařízení**  >  **profily**  >  **vytvořit profil**.

3. Zadejte tyto vlastnosti:
   - **Platforma**: vyberte platformu zařízení, která obdrží tento profil.
   - **Profil**: vyberte **důvěryhodný certifikát** .
  
4. Vyberte **Vytvořit**.

5. V části **základy**zadejte následující vlastnosti:
   - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například *profil důvěryhodného certifikátu pro celou firmu*.
   - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.

7. V části **nastavení konfigurace**zadejte soubor. cer kořenový certifikát certifikační autority, který jste předtím exportovali.

   > [!NOTE]
   > V závislosti na platformě, kterou jste zvolili v **kroku 3**, můžete nebo nemůžete mít možnost vybrat **cílové úložiště** certifikátu.

   ![Vytvoření profilu a nahrání důvěryhodného certifikátu](./media/certficates-pfx-configure/certificates-pfx-configure-profile-fill.png)

8. Vyberte **Další**.

9. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu pro konkrétní IT skupiny, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment` . Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](../fundamentals/scope-tags.md).

   Vyberte **Další**.

10. V části **přiřazení**vyberte uživatele nebo skupiny, které obdrží váš profil. Naplánujte nasazení tohoto profilu certifikátu do stejných skupin, které obdrží profil certifikátu PKCS. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](../configuration/device-profile-assign.md).

    Vyberte **Další**.

11. (*Platí jenom pro Windows 10*) V části **pravidla použitelnosti**zadejte pravidla použitelnosti pro upřesnění přiřazení tohoto profilu. Můžete vybrat, že chcete profil přiřadit nebo nepřiřadit, na základě edice nebo verze operačního systému zařízení.

  Další informace najdete v tématu [pravidla použitelnosti](../configuration/device-profile-create.md#applicability-rules) v tématu *Vytvoření profilu zařízení v Microsoft Intune*.

12. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete vytvořit, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

## <a name="create-a-pkcs-certificate-profile"></a>Vytvoření profilu certifikátu PKCS

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte a přejdete na konfigurace **zařízení**  >  **profily**  >  **vytvořit profil**.

3. Zadejte tyto vlastnosti:
   - **Platforma**: vyberte platformu zařízení. Možnosti:
     - Správce zařízení s Androidem
     - Android Enterprise > plně spravovaný, vyhrazený a podnikový pracovní profil
     - Jenom pracovní profil pro Android Enterprise >
     - iOS/iPadOS
     - macOS
     - Windows 10 a novější
   - **Profil**: vyberte **certifikát PKCS** .

   > [!NOTE]
   > V zařízeních s profilem podnikového systému Android nejsou v zařízení vidět certifikáty nainstalované pomocí profilu certifikátu PKCS. Pokud chcete potvrdit úspěšné nasazení certifikátu, zkontrolujte stav profilu v konzole Intune.
4. Vyberte **Vytvořit**.

5. V části **základy**zadejte následující vlastnosti:
   - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například *profil PKCS pro celou firmu*.
   - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.
7. Nastavení, která můžete konfigurovat v **nastavení konfigurace**, se liší v závislosti na zvolené platformě. Pro podrobnější nastavení vyberte svou platformu:
   - Správce zařízení s Androidem
   - Android Enterprise
   - iOS/iPadOS
   - Windows 10
   
   |Nastavení     | Platforma     | Podrobnosti   |
   |------------|------------|------------|
   |**Prahová hodnota obnovení (%)**        |<ul><li>Vše         |Doporučuje se 20%  | 
   |**Období platnosti certifikátu**  |<ul><li>Vše         |Pokud jste šablonu certifikátu nezměnili, může být tato možnost nastavená na jeden rok. |
   |**Zprostředkovatel úložiště klíčů (KSP)**   |<ul><li>Windows 10  |V případě systému Windows vyberte místo, kam chcete uložit klíče na zařízení. |
   |**Certifikační autorita**      |<ul><li>Vše         |Zobrazuje interní plně kvalifikovaný název domény (FQDN) vaší certifikační autority organizace.  |
   |**Název certifikační autority** |<ul><li>Vše         |Zobrazuje název vaší certifikační autority organizace, například "certifikační autorita společnosti Contoso". |
   |**Název šablony certifikátu**    |<ul><li>Vše         |Zobrazuje název šablony certifikátu. |
   |**Typ certifikátu**             |<ul><li>Android Enterprise (*pracovní profil*)</li><li>iOS</li><li>macOS</li><li>Windows 10 a novější|Vyberte typ: <ul><li> Certifikáty **uživatelů** mohou obsahovat atributy uživatele i zařízení v předmětu a alternativním názvu předmětu (San) certifikátu. </il><li>Certifikáty **zařízení** mohou obsahovat pouze atributy zařízení v předmětu a San certifikátu. Použijte zařízení pro scénáře, jako jsou například zařízení bez uživatele, jako jsou veřejné terminály nebo jiná sdílená zařízení.  <br><br> Tento výběr má vliv na formát názvu subjektu. |
   |**Formát názvu subjektu**          |<ul><li>Vše         |Podrobnosti o tom, jak nakonfigurovat formát názvu subjektu, najdete v části [Formát názvu subjektu](#subject-name-format) dále v tomto článku.  <br><br> U většiny platforem použijte možnost **běžný název** , pokud není vyžadováno jinak. <br><br>U následujících platforem se formát názvu subjektu určuje podle typu certifikátu: <ul><li>Android Enterprise (*pracovní profil*)</li><li>iOS</li><li>macOS</li><li>Windows 10 a novější</li></ul>  <p>  |
   |**Alternativní název subjektu**     |<ul><li>Vše         |V případě *atributu*vyberte **hlavní název uživatele (UPN)** , pokud není vyžadováno jinak, nakonfigurujte odpovídající *hodnotu*a klikněte na tlačítko **Přidat**. <br><br> Pro síť SAN obou typů certifikátů můžete použít proměnné nebo statický text. Použití proměnné není vyžadováno.<br><br>Další informace najdete v části [Formát názvu subjektu](#subject-name-format) dále v tomto článku.|
   |**Rozšířené použití klíče**           |<ul><li> Správce zařízení s Androidem </li><li>Android Enterprise (*vlastník zařízení*, *pracovní profil*) </li><li>Windows 10 |Certifikáty obvykle vyžadují *ověření klienta* , aby se mohl uživatel nebo zařízení ověřit na serveru. |
   |**Povolí všem aplikacím přístup k privátnímu klíči.** |<ul><li>macOS  |Nastavením této vlastnosti **povolíte** aplikacím, které jsou nakonfigurované pro přidružené zařízení Mac, přístup k privátnímu klíči certifikátů PKCS. <br><br> Další informace o tomto nastavení najdete v tématu *AllowAllAppsAccess* v části referenční část certifikátu [konfiguračního profilu](https://developer.apple.com/business/documentation/Configuration-Profile-Reference.pdf) v dokumentaci pro vývojáře Apple. |
   |**Kořenový certifikát**             |<ul><li>Správce zařízení s Androidem </li><li>Android Enterprise (*vlastník zařízení*, *pracovní profil*) |Vyberte profil certifikátu od kořenové certifikační autority, který byl dříve přiřazen. |

8. Vyberte **Další**.

9. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu pro konkrétní IT skupiny, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment` . Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](../fundamentals/scope-tags.md).

   Vyberte **Další**.

10. V části **přiřazení**vyberte uživatele nebo skupiny, které obdrží váš profil. Naplánujte nasazení tohoto profilu certifikátu do stejných skupin, které obdrží profil důvěryhodného certifikátu. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](../configuration/device-profile-assign.md).

    Vyberte **Další**.

11. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete vytvořit, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.


### <a name="subject-name-format"></a>Formát názvu subjektu

Když vytváříte profil certifikátu PKCS pro následující platformy, možnosti pro formát názvu subjektu závisí na zvoleném typu certifikátu. buď na **uživatele** , nebo na **zařízení**.  

Platformu

- Android Enterprise (*pracovní profil*)
- iOS
- macOS
- Windows 10 a novější

> [!NOTE]
> K dispozici je známý problém s používáním PKCS k získání certifikátů, [které mají stejný problém jako u protokolu SCEP](certificates-profile-scep.md#avoid-certificate-signing-requests-with-escaped-special-characters) , když název subjektu v výsledné žádosti o podepsání certifikátu (CSR) obsahuje jeden z následujících znaků jako řídicí znak (pokračuje zpětným lomítkem \\ ):
> - \+
> - ;
> - ,
> - =

- **Typ uživatelského certifikátu**  
  Možnosti formátu pro *Formát názvu subjektu* zahrnují dvě proměnné: **běžný název (CN)** a **e-mail (e)**. **Běžný název (CN)** můžete nastavit na některou z těchto proměnných:

  - **CN = {{username}}**: hlavní název uživatele (UPN), například janedoe@contoso.com .
  - **CN={{AAD_Device_ID}}**: ID přiřazené při registraci zařízení ve službě AD (Azure Active Directory). Toto ID se obvykle používá k ověření ve službě Azure AD.
  - **CN = {{sériové}}**: jedinečné sériové číslo (SN) obvykle používané výrobcem k identifikaci zařízení.
  - **CN = {{IMEINumber}}**: jedinečné číslo IMEI (International Mobile Equipment Identity), které se používá k identifikaci mobilního telefonu.
  - **CN = {{OnPrem_Distinguished_Name}}**: sekvence relativních rozlišujících názvů oddělená čárkou, například *CN = Jana Karásek, OU = UserAccounts, DC = Corp, DC = contoso, DC = com*.

    Pokud chcete použít proměnnou *{{OnPrem_Distinguished_Name}}* , proveďte synchronizaci atributu uživatele *onpremisesdistinguishedname* pomocí [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect) do služby Azure AD.

  - **CN = {{onPremisesSamAccountName}}**: Správci můžou synchronizovat atribut sAMAccountName ze služby Active Directory do Azure AD pomocí služby Azure AD Connect do atributu s názvem *onPremisesSamAccountName*. Intune může tuto proměnnou nahradit jako součást žádosti o vystavení certifikátu v předmětu certifikátu. Atribut samAccountName je přihlašovací jméno uživatele používané k podpoře klientů a serverů z předchozí verze Windows (Pre-Windows 2000). Formát přihlašovacího jména uživatele je: *DomainName\testUser*nebo pouze *testUser*.

    Pokud chcete použít proměnnou *{{onPremisesSamAccountName}}* , nezapomeňte synchronizovat atribut uživatele *onPremisesSamAccountName* pomocí [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect) do Azure AD.

  Kombinací jedné nebo několika těchto proměnných a statických řetězců můžete vytvořit vlastní formát názvu subjektu, jako třeba:  
  - **CN={{UserName}},E={{EmailAddress}},OU=Mobile,O=Finance Group,L=Redmond,ST=Washington,C=US**
  
  Tento příklad zahrnuje formát názvu subjektu, který používá proměnné CN a E a řetězce pro hodnoty organizační jednotky, organizace, umístění, stav a země. Článek [Funkce CertStrToName](/windows/win32/api/wincrypt/nf-wincrypt-certstrtonamea) popisuje tuto funkci a její podporované řetězce.

- **Typ certifikátu zařízení**  
  Možnosti formátu pro formát názvu subjektu zahrnují následující proměnné: 
  - **{{AAD_Device_ID}}**
  - **{{Device_Serial}}**
  - **{{Device_IMEI}}**
  - **{{Sériové}}**
  - **{{IMEINumber}}**
  - **{{AzureADDeviceId}}**
  - **{{WiFiMacAddress}}**
  - **{{IMEI}}**
  - **{{Název_zařízení}}**
  - **{{FullyQualifiedDomainName}}** *(platí jenom pro zařízení se systémem Windows a zařízení připojená k doméně)*
  - **{{MEID}}**

  Tyto proměnné můžete zadat následovaný textem pro proměnnou v textovém poli. Například běžný název pro zařízení s názvem *zařízení1* se dá přidat jako **CN = {{název_zařízení}} zařízení1**.

  > [!IMPORTANT]  
  > - Když zadáte proměnnou, uveďte její název do složených závorek {}, jak je vidět v příkladu, aby nedošlo k chybě.  
  > - Vlastnosti zařízení používané v *předmětu* nebo *síti SAN* certifikátu zařízení, jako jsou **IMEI**, **sériové**a **FullyQualifiedDomainName**, jsou vlastnosti, které by mohly být falešné osobou, která by mohla mít přístup k zařízení.
  > - Zařízení musí podporovat všechny proměnné určené v profilu certifikátu pro daný profil k instalaci na toto zařízení.  Pokud se například používá **{{IMEI}}** v názvu subjektu profilu SCEP a je přiřazeno k zařízení, které nemá číslo IMEI, profil se nepodaří nainstalovat.

## <a name="next-steps"></a>Další kroky

[Použijte SCEP pro certifikáty](certificates-scep-configure.md)nebo [vydejte certifikáty PKCS z webové služby správce infrastruktury veřejných klíčů Symantec](certificates-digicert-configure.md).

[Řešení potíží s profily certifikátů PKCS](../protect/troubleshoot-pkcs-certificate-profiles.md)
