---
title: Vystavení certifikátů PKCS DigiCert pomocí Microsoft Intune
titleSuffix: Microsoft Intune
description: Instalace a konfigurace Intune Certificate Connectoru pro vydávání certifikátů PKCS ze DigiCert platformy PKI do zařízení spravovaných pomocí Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/21/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 99cad94d0d0f56aba94e8d00a091efea914f418e
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990345"
---
# <a name="set-up-intune-certificate-connector-for-digicert-pki-platform"></a>Nastavení Intune Certificate Connectoru pro platformu PKI DigiCert

Použijte Intune Certificate Connector k vydávání certifikátů PKCS z DigiCert platformy PKI do zařízení spravovaných pomocí Intune. Konektor můžete použít jenom s DigiCert certifikační autoritou (CA), nebo s certifikační autoritou DigiCert i s certifikační autoritou Microsoftu.

> [!TIP]
> DigiCert získal zabezpečení webu společnosti Symantec a související řešení PKI podniku. Další informace o této změně najdete v [článku technické podpory společnosti Symantec](https://support.symantec.com/en_US/article.INFO4722.html).

Pokud už používáte Intune Certificate Connector k vydávání certifikátů od certifikační autority Microsoftu pomocí PKCS nebo Simple Certificate Enrollment Protocol (SCEP), můžete stejný konektor použít ke konfiguraci a vydávání certifikátů PKCS z certifikační autority DigiCert. Po dokončení konfigurace pro podporu certifikační autority DigiCert může Intune Certificate Connector vydat následující certifikáty:

* Certifikáty PKCS od certifikační autority Microsoftu
* Certifikáty PKCS z certifikační autority DigiCert
* Endpoint Protection certifikátů od certifikační autority společnosti Microsoft

Pokud nemáte nainstalovaný konektor, ale plánujete ho použít pro certifikační autoritu Microsoftu i pro certifikační autoritu DigiCert, nejdřív dokončete konfiguraci konektoru pro certifikační autoritu Microsoftu. Pak se vraťte k tomuto článku a nakonfigurujte ho tak, aby podporoval taky DigiCert. Další informace o profilech certifikátů a konektoru najdete [v tématu Konfigurace profilu certifikátu pro vaše zařízení v Microsoft Intune](certificates-configure.md).  

Pokud budete konektor používat jenom s certifikační autoritou DigiCert, můžete k instalaci a konfiguraci konektoru použít pokyny v tomto článku.

## <a name="prerequisites"></a>Požadavky

- **Aktivní předplatné v certifikační autoritě DigiCert**: předplatné je potřeba k získání certifikátu registrační autority od certifikační autority DigiCert.
- Microsoft Intune Certificate Connector má stejné požadavky na síť jako [spravovaná zařízení](../fundamentals/intune-endpoints.md#access-for-managed-devices).

## <a name="install-the-digicert-ra-certificate"></a>Instalace certifikátu RA DigiCert

1. Následující fragment kódu uložte jako soubor s názvem **Certreq. ini** a aktualizujte ho podle potřeby (například: *název subjektu ve formátu CN*).

        [Version] 
        Signature="$Windows NT$" 
        
        [NewRequest] 
        ;Change to your,country code, company name and common name 
        Subject = "Subject Name in CN format"
        
        KeySpec = 1 
        KeyLength = 2048 
        Exportable = TRUE 
        MachineKeySet = TRUE 
        SMIME = False 
        PrivateKeyArchive = FALSE 
        UserProtected = FALSE 
        UseExistingKeySet = FALSE 
        ProviderName = "Microsoft RSA SChannel Cryptographic Provider" 
        ProviderType = 12 
        RequestType = PKCS10 
        KeyUsage = 0xa0 
        
        [EnhancedKeyUsageExtension] 
        OID=1.3.6.1.5.5.7.3.2 ; Client Authentication  // Uncomment if you need a mutual TLS authentication
        
        ;----------------------------------------------- 

2. Otevřete příkazový řádek se zvýšenými oprávněními a vygenerujte žádost o podepsání certifikátu (CSR) pomocí následujícího příkazu:

   `Certreq.exe -new certreq.ini request.csr`

3. Otevřete soubor Request. CSR v programu Poznámkový blok a zkopírujte obsah CSR v následujícím formátu:

        -----BEGIN NEW CERTIFICATE REQUEST-----
        MIID8TCCAtkCAQAwbTEMMAoGA1UEBhMDVVNBMQswCQYDVQQIDAJXQTEQMA4GA1UE
        …
        …
        fzpeAWo=
        -----END NEW CERTIFICATE REQUEST-----


4. Přihlaste se k certifikační autoritě DigiCert a přejděte k části **získání certifikátu RA** z těchto úloh.

   a. Do textového pole zadejte obsah CSR od kroku 3.

   b. Zadejte popisný název certifikátu.

   c. Vyberte **Pokračovat**.

   d. Pomocí poskytnutého odkazu Stáhněte certifikát RA do svého místního počítače.

5. Importujte certifikát RA do úložiště certifikátů Windows:

   a. Otevřete konzolu MMC.

   b. Vyberte **soubor**přidat  >  **nebo odebrat certifikát moduly snap-in**  >  **Certificate**  >  **Přidat**.

   c. Vyberte **účet počítače**  >  **Další**.

   d. Vyberte možnost Dokončit **místní počítač**  >  **Finish**.

   e. V okně **Přidat nebo odebrat moduly snap-in** vyberte **OK** . Rozbalte položku **certifikáty (místní počítač)**  >  **osobní**  >  **certifikáty**.

   f. Klikněte pravým tlačítkem myši na uzel **Certifikáty** a vyberte možnost **Všechny úkoly** > **Importovat**.

   g. Vyberte umístění certifikátu RA, který jste stáhli z certifikační autority DigiCert, a pak vyberte **Další**.

   h. Vyberte **osobní úložiště certifikátů**  >  **Další**.

   i. Výběrem **Dokončit** IMPORTUJTE certifikát RA a jeho soukromý klíč do **osobního úložiště místního počítače** .

6. Export a import certifikátu privátního klíče:

   a. Rozbalte položku **certifikáty (místní počítač)**  >  **osobní**  >  **certifikáty**.

   b. Vyberte certifikát naimportovaný v předchozím kroku.

   c. Klikněte pravým tlačítkem na certifikát a vyberte **všechny úkoly**  >  **exportovat**.

   d. Vyberte **Další**a pak zadejte heslo.

   e. Vyberte umístění, do kterého chcete exportovat, a pak vyberte **Dokončit**.

   f. Pomocí postupu z kroku 5 importujte certifikát privátního klíče do **osobního úložiště místního počítače** .

   g. Zaznamenejte kopii kryptografického otisku certifikátu RA bez mezer. Následuje příklad kryptografického otisku:

        RA Cert Thumbprint: "EA7A4E0CD1A4F81CF0740527C31A57F6020C17C5"

    > [!NOTE]
    > Pokud potřebujete pomoc při získávání certifikátu RA od certifikační autority DigiCert, obraťte se na [zákaznickou podporu DigiCert](mailto:enterprise-pkisupport@digicert.com).

## <a name="prepare-to-install-intune-certificate-connector"></a>Příprava k instalaci nástroje Intune Certificate Connector

> [!TIP]
> Tato část platí v případě, že používáte Intune Certificate Connector jenom s certifikační autoritou DigiCert. Pokud používáte Intune Certificate Connector s certifikační autoritou Microsoftu a chcete přidat podporu pro certifikační autoritu DigiCert, přeskočte k [části Konfigurace konektoru pro podporu DigiCert](#configure-the-connector-to-support-digicert).

1. Z následujícího seznamu vyberte jednu z verzí operačního systému Windows a nainstalujte ji na počítač:
   * Windows Server 2012 R2 Datacenter
   * Windows Server 2012 R2 Standard
   * Windows Server 2016 Datacenter
   * Windows Server 2016 Standard

2. Vytvořte uživatele s oprávněními správce a použijte ho k dokončení následujících kroků.

3. Vyhledejte nejnovější aktualizace Windows a nainstalujte je, pokud jsou k dispozici. Po instalaci aktualizací systému Windows restartujte počítač.

4. Instalace .NET Framework 3.5:

   a. Otevřete **Ovládací panely**  >  **programy a funkce**  >  **zapnout nebo vypnout funkce systému Windows**.

   b. Vyberte možnost **.NET Framework 3.5** a rozhraní nainstalujte.

## <a name="install-intune-certificate-connector-for-use-with-digicert"></a>Instalace Intune Certificate Connectoru pro použití s DigiCert

> [!TIP]
> Pokud používáte Intune Certificate Connector s certifikační autoritou Microsoftu a chcete přidat podporu pro certifikační autoritu DigiCert, přeskočte k [části Konfigurace konektoru pro podporu DigiCert](#configure-the-connector-to-support-digicert).

Stáhněte si nejnovější verzi Intune Certificate Connectoru z portálu pro správu Intune a postupujte podle těchto pokynů.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte možnost konektory **pro správu tenanta**  >  **a tokeny**  >  **Certificate Connectors**  >  **+ Add**.

3. Klikněte na *Stáhnout software Certificate Connector* pro konektor pro PKCS #12 a uložte soubor do umístění, ke kterému máte přístup ze serveru, na který budete konektor instalovat.

   ![Stažení softwaru konektoru](./media/certificates-digicert-configure/connector-download.png)

4. Na serveru, na který chcete konektor nainstalovat, spusťte **NDESConnectorSetup. exe** se zvýšenými oprávněními.

5. Na stránce **Možnosti instalace** vyberte **distribuce PFX**.

   ![Vybrat distribuci PFX](./media/certificates-digicert-configure/digicert-ca-connector-install.png)

   > [!IMPORTANT]
   > Pokud budete k vystavování certifikátů od certifikační autority společnosti Microsoft a certifikační autority DigiCert používat Intune Certificate Connector, vyberte **distribuce profilů SCEP a PFX**.

6. Pomocí výchozích výběrů dokončete nastavení konektoru.

## <a name="configure-the-connector-to-support-digicert"></a>Konfigurace konektoru pro podporu DigiCert

Ve výchozím nastavení se Intune Certificate Connector nainstaluje do **%ProgramFiles%\Microsoft Intune\NDESConnectorSvc**.

1. Ve složce **NDESConnectorSvc** otevřete soubor **NDESConnector. exe. config** v programu Poznámkový blok.

   a. Aktualizujte `RACertThumbprint` hodnotu klíče s hodnotou kryptografického otisku certifikátu, kterou jste zkopírovali v předchozí části. Příklad:

        <add key="RACertThumbprint"
        value="EA7A4E0CD1A4F81CF0740527C31A57F6020C17C5"/>

   b. Uložte soubor a zavřete ho.

2. Otevřete **Services. msc**:

   a. Vyberte službu **Intune Connector Service**.

   b. Zastavte službu a pak ji zase spusťte.

   c. Zavřete okno služby.

## <a name="set-up-the-intune-administrator-account"></a>Nastavení účtu správce Intune  

> [!TIP]
> Pokud používáte Intune Certificate Connector s certifikační autoritou Microsoftu a chcete přidat podporu pro certifikační autoritu DigiCert, přeskočte dopředu k [Vytvoření profilu důvěryhodného certifikátu](#create-a-trusted-certificate-profile).
 
1. Otevřete uživatelské rozhraní konektoru NDES z **%ProgramFiles%\Microsoft Intune\NDESConnectorUI\NDESConnectorUI.exe**.

2. Na kartě **registrace** vyberte **Přihlásit**se.

3. Zadejte svoje přihlašovací údaje správce tenanta Intune.

4. Vyberte **Přihlásit**se a pak kliknutím na **OK** potvrďte úspěšný zápis. Pak můžete zavřít uživatelské rozhraní konektoru NDES.

   ![Rozhraní NDES Connector se zprávou o úspěšné registraci](./media/certificates-digicert-configure/certificates-digicert-configure-connector-configure.png)

## <a name="create-a-trusted-certificate-profile"></a>Vytvoření profilu důvěryhodného certifikátu

Certifikáty PKCS, které nasadíte pro zařízení spravovaná pomocí Intune, musí být zřetězené s důvěryhodným kořenovým certifikátem. Pokud chcete tento řetěz vytvořit, vytvořte profil důvěryhodného certifikátu Intune s kořenovým certifikátem z certifikační autority DigiCert a nasaďte profil důvěryhodného certifikátu i profil certifikátu PKCS do stejných skupin.

1. Získání důvěryhodného kořenového certifikátu od certifikační autority DigiCert:

   a. Přihlaste se k portálu pro správu certifikační autority DigiCert.

   b. Vyberte **Správa certifikačních autorit** z **úloh**.

   c. Vyberte ze seznamu příslušnou certifikační autoritu.

   d. Vyberte **Stáhnout kořenový certifikát** pro stažení důvěryhodného kořenového certifikátu.

2. Vytvořte profil důvěryhodného certifikátu na portálu Intune:

   a. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

   b. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.

   c. Zadejte tyto vlastnosti:

      - Zadejte **Název** profilu.
      - Volitelně můžete nastavit **Popis** .
      - Zadejte **Platformu**, na kterou se má profil nasadit.
      - Nastavte **Typ profilu** na **Důvěryhodný certifikát**.

   d. Vyberte **Nastavení**a pak vyhledejte soubor. CER certifikátu důvěryhodné kořenové certifikační autority, který jste exportovali pro použití s tímto profilem certifikátu, a pak vyberte **OK**.

   e. Jenom pro zařízení s Windows 8.1 a Windows 10 vyberte **cílové úložiště** pro důvěryhodný certifikát z těchto možností:
      - **Úložiště počítačových certifikátů – kořenové**
      - **Úložiště certifikátů počítače-zprostředkující**
      - **Úložiště uživatelských certifikátů – zprostředkující**

   f. Až to budete mít, vyberte **OK**, vraťte se zpět do podokna **Vytvořit profil** a vyberte **Vytvořit**.  

  Profil se zobrazí v seznamu profilů v podokně **Konfigurace zařízení – profily** s typem profilu **důvěryhodného certifikátu**.  Nezapomeňte tento profil přiřadit k zařízením, která budou přijímat certifikáty. Pokud chcete přiřadit tento profil ke skupinám, přečtěte si téma [přiřazení profilů zařízení](../configuration/device-profile-assign.md).


## <a name="get-the-certificate-profile-oid"></a>Získání identifikátoru objektu profilu certifikátu  

Identifikátor objektu profilu certifikátu je přidružen k šabloně profilu certifikátu v certifikační autoritě DigiCert. Pokud chcete vytvořit profil certifikátu PKCS v Intune, musí být název šablony certifikátu ve formě identifikátoru objektu profilu certifikátu, který je přidružený k šabloně certifikátu v certifikační autoritě DigiCert.

1. Přihlaste se k portálu pro správu certifikační autority DigiCert.
2. Vyberte možnost **Spravovat profily certifikátů**.
3. Vyberte profil certifikátu, který chcete použít.
4. Zkopírujte identifikátor objektu profilu certifikátu. Vypadá podobně jako v následujícím příkladu:

       Certificate Profile OID = 2.16.840.1.113733.1.16.1.2.3.1.1.47196109 

> [!NOTE]
> Pokud potřebujete pomoc s získáním identifikátoru objektu profilu certifikátu, obraťte se na [zákaznickou podporu DigiCert](mailto:enterprise-pkisupport@digicert.com).

## <a name="create-a-pkcs-certificate-profile"></a>Vytvoření profilu certifikátu PKCS

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.

3. Zadejte tyto vlastnosti:

   - Zadejte **Název** profilu.
   - Volitelně můžete nastavit **Popis** .
   - Zadejte **Platformu**, na kterou se má profil nasadit.
   - Nastavit **typ profilu** na **certifikát PKCS**

4. V podokně **certifikát PKCS** nakonfigurujte parametry s hodnotami z následující tabulky. Tyto hodnoty jsou potřeba k vydávání certifikátů PKCS z certifikační autority DigiCert prostřednictvím Intune Certificate Connectoru.

   |Parametr certifikátu PKCS | Hodnota | Popis |
   | --- | --- | --- |
   | Certifikační autorita | pki-ws.symauth.com | Tato hodnota musí být DigiCert plně kvalifikovaný název domény základní služby certifikační autority bez koncových lomítek. Pokud si nejste jistí, jestli se jedná o správný plně kvalifikovaný název domény základní služby pro předplatné certifikační autority DigiCert, obraťte se na zákaznickou podporu DigiCert. <br><br>V případě *změny od Symantec na DigiCert zůstane tato adresa URL beze změny*. <br><br> Pokud je tento plně kvalifikovaný název domény nesprávný, Intune Certificate Connector nevydá certifikáty PKCS z certifikační autority DigiCert.| 
   | Název certifikační autority | Symantec | Tato hodnota musí být řetězec **Symantec**. <br><br> Pokud dojde ke změně této hodnoty, Intune Certificate Connector nevydá certifikáty PKCS z certifikační autority DigiCert.|
   | Název šablony certifikátu | Identifikátor objektu profilu certifikátu z certifikační autority DigiCert Příklad: **2.16.840.1.113733.1.16.1.2.3.1.1.61904612**| Tato hodnota musí být identifikátor objektu profilu certifikátu [získaného v předchozí části](#get-the-certificate-profile-oid) v šabloně profilu certifikátu certifikační autority DigiCert. <br><br> Pokud Intune Certificate Connector nemůže najít šablonu certifikátu přidruženou k tomuto identifikátoru objektu profilu certifikátu v certifikační autoritě DigiCert, nevydá certifikáty PKCS z certifikační autority DigiCert.|

   ![Výběry pro certifikační autoritu a šablonu certifikátu](./media/certificates-digicert-configure/certificates-digicert-pkcs-example.png)

   > [!NOTE]
   > Profil certifikátu PKCS pro platformy Windows není nutné přidružit k profilu důvěryhodného certifikátu. V jiných systémech než Windows, jako je například Android, je však nutný.

5. Dokončete konfiguraci profilu tak, aby vyhovoval vašim obchodním potřebám, a pak výběrem **vytvořit** uložte profil.

6. Na stránce *Přehled* nového profilu vyberte **přiřazení** a nakonfigurujte příslušnou skupinu, která tento profil obdrží. Aspoň jeden uživatel nebo zařízení musí být součástí přiřazené skupiny.
 
Po dokončení předchozích kroků vystaví Intune Certificate Connector certifikáty PKCS z CA DigiCert do zařízení spravovaných pomocí Intune v přiřazené skupině. Tyto certifikáty budou k dispozici v **osobním** úložišti úložiště certifikátů **aktuálního uživatele** na zařízení spravovaném přes Intune.

### <a name="supported-attributes-for-the-pkcs-certificate-profile"></a>Podporované atributy profilu certifikátu PKCS

|Atribut | Formáty podporované Intune | Formáty podporované DigiCert cloudové CA | result |
| --- | --- | --- | --- |
| Název předmětu |Intune podporuje název subjektu pouze ve třech následujících formátech: <br><br> 1. běžný název <br> 2. běžný název, který obsahuje e-mail <br> 3. běžný název jako e-mail <br><br> Příklad: <br><br> `CN = IWUser0 <br><br> E = IWUser0@samplendes.onmicrosoft.com` | Certifikační autorita DigiCert podporuje více atributů.  Pokud chcete vybrat další atributy, musí být definované s pevnými hodnotami v šabloně profilu certifikátu DigiCert.| V žádosti o certifikát PKCS používáme běžný název nebo e-mail. <br><br> Neshoda v výběru atributů mezi profilem certifikátu Intune a šablonou profilu certifikátu DigiCert nevede k vystavování certifikátů od certifikační autority DigiCert.|
| Alternativní název subjektu | Intune podporuje pouze následující hodnoty polí alternativního názvu subjektu: <br><br> **AltNameTypeEmail** <br> **AltNameTypeUpn** <br> **AltNameTypeOtherName** (zakódovaná hodnota) | DigiCert cloudová certifikační autorita podporuje také tyto parametry. Pokud chcete vybrat další atributy, musí být definované s pevnými hodnotami v šabloně profilu certifikátu DigiCert. <br><br> **AltNameTypeEmail**: Pokud tento typ není v síti SAN nalezen, používá nástroj Intune Certificate Connector hodnotu z **AltNameTypeUpn**.  Pokud se v síti SAN taky nenajde **AltNameTypeUpn** , použije Intune Certificate Connector hodnotu z názvu subjektu, pokud je ve formátu e-mailu.  Pokud se tento typ pořád nenajde, Intune Certificate Connector se nepodaří vystavit certifikáty. <br><br> Příklad: `RFC822 Name=IWUser0@ndesvenkatb.onmicrosoft.com`  <br><br> **AltNameTypeUpn**: Pokud tento typ není v síti SAN nalezen, používá nástroj Intune Certificate Connector hodnotu z **AltNameTypeEmail**. Pokud se v síti SAN taky nenajde **AltNameTypeEmail** , použije Intune Certificate Connector hodnotu z názvu předmětu, pokud je ve formátu e-mailu. Pokud se tento typ pořád nenajde, Intune Certificate Connector se nepodaří vystavit certifikáty.  <br><br> Příklad: `Other Name: Principal Name=IWUser0@ndesvenkatb.onmicrosoft.com` <br><br> **AltNameTypeOtherName**: Pokud se tento typ v síti SAN nenajde, nemůže Intune Certificate Connector vydat certifikáty. <br><br> Příklad: `Other Name: DS Object Guid=04 12 b8 ba 65 41 f2 d4 07 41 a9 f7 47 08 f3 e4 28 5c ef 2c` <br><br>  Hodnota tohoto pole je podporována certifikační autoritou DigiCert pouze v kódovaném formátu (šestnáctková hodnota). Pro libovolnou hodnotu v tomto poli Intune Certificate Connector před odesláním žádosti o certifikát převede na kódování Base64. *Intune Certificate Connector neověřuje, jestli je tato hodnota už zakódovaná, nebo ne.* | Žádné |

## <a name="troubleshooting"></a>Řešení potíží

Protokoly služby Intune Certificate Connector jsou k dispozici ve složce **%ProgramFiles%\Microsoft Intune\NDESConnectorSvc\Logs\Logs** na počítači NDES Connector. Otevřete protokoly v [SvcTraceViewer](https://docs.microsoft.com/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) a vyhledejte výjimky nebo chybové zprávy.

| Problém/chybová zpráva | Postup řešení |
| --- | --- |
| Nepovedlo se přihlásit pomocí účtu správce tenanta Intune v uživatelském rozhraní konektoru NDES. | K tomu může dojít v případě, že místní Certificate Connector není povolený v centru pro správu Microsoft Endpoint Manageru. Řešení tohoto problému: <br><br> 1. Přihlaste se do [centra pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). <br> 2. Vyberte konektory **pro správu tenanta**  >  **a tokeny**  >  **certifikátů**. <br> 3. Vyhledejte Certificate Connector a ujistěte se, že je povolený. <br><br> Po dokončení předchozích kroků se zkuste přihlásit pomocí stejného účtu správce tenanta Intune v uživatelském rozhraní konektoru NDES. |
| Certifikát konektoru NDES Connector se nepodařilo nalézt. <br><br> System. ArgumentNullException: value nemůže mít hodnotu null. | Intune Certificate Connector zobrazuje tuto chybu, pokud se účet správce tenanta Intune nikdy nepřihlásil k uživatelskému rozhraní NDES Connector. <br><br> Pokud tato chyba přetrvává, restartujte konektor služby Intune. <br><br> 1. Otevřete **Services. msc**. <br> 2. Vyberte **službu Intune Connector Service**. <br> 3. Klikněte pravým tlačítkem a vyberte **restartovat**.|
| NDES Connector – IssuePfx – obecná výjimka: <br> System.NullReferenceException: Odkaz na objekt není nastavený na instanci objektu. | Tato chyba je přechodná. Restartujte konektor služby Intune. <br><br> 1. Otevřete **Services. msc**. <br> 2. Vyberte **službu Intune Connector Service**. <br> 3. Klikněte pravým tlačítkem a vyberte **restartovat**. |
| Poskytovatel DigiCert – nepovedlo se získat zásady DigiCert. <br><br>Vypršel časový limit operace. | Intune Certificate Connector přijal při komunikaci s certifikační autoritou DigiCert chybu časového limitu operace. Pokud k této chybě dochází i nadále, zvyšte hodnotu časového limitu připojení a zkuste to znovu. <br><br> Chcete-li zvýšit časový limit připojení: <br> 1. Projděte si počítač konektoru NDES. <br>2. v programu Poznámkový blok otevřete soubor **%ProgramFiles%\Microsoft Intune\NDESConnectorSvc\NDESConnector.exe.config** . <br> 3. Zvyšte hodnotu časového limitu pro následující parametr: <br><br> `CloudCAConnTimeoutInMilliseconds` <br><br> 4. Restartujte službu Intune Certificate Connector. <br><br> Pokud se problém nevyřeší, obraťte se na zákaznickou podporu DigiCert. |
| DigiCert Provider – nepovedlo se získat klientský certifikát. | Službě Intune Certificate Connector se nepodařilo načíst certifikát autorizace prostředku z osobního úložiště certifikátů místního počítače. Pokud chcete tento problém vyřešit, nainstalujte certifikát pro autorizaci prostředků do osobního úložiště certifikátů místního počítače společně s jeho privátním klíčem. <br><br> Certifikát pro autorizaci prostředků se musí získat z certifikační autority DigiCert. Pokud chcete získat další informace, obraťte se na zákaznickou podporu DigiCert. | 
| Poskytovatel DigiCert – nepovedlo se získat zásady DigiCert. <br><br>"Žádost byla přerušena: nelze vytvořit zabezpečený kanál SSL/TLS." | K této chybě dochází v následujících případech: <br><br> 1. služba Intune Certificate Connector nemá oprávnění číst certifikát pro autorizaci prostředků spolu s jeho privátním klíčem z osobního úložiště certifikátů místního počítače. Chcete-li tento problém vyřešit, ověřte, zda je v nástroji Services. msc spuštěný kontextový účet služby konektoru. Služba konektoru musí běžet v kontextu NT AUTHORITY\SYSTEM. <br><br> 2. profil certifikátu PKCS na portálu pro správu Intune může být nakonfigurovaný s neplatným plně kvalifikovaným názvem domény základní služby pro certifikační autoritu DigiCert. Plně kvalifikovaný název domény je podobný **PKI-WS.symauth.com**. Pokud chcete tento problém vyřešit, obraťte se na zákaznickou podporu DigiCert, jestli je adresa URL pro vaše předplatné správná. <br><br> 3. Intune Certificate Connector se nedokáže ověřit pomocí certifikační autority DigiCert prostřednictvím autorizačního certifikátu prostředku, protože nemůže získat privátní klíč. Pokud chcete tento problém vyřešit, nainstalujte certifikát pro autorizaci prostředků spolu s jeho privátním klíčem do osobního úložiště certifikátů místního počítače. <br><br> Pokud se problém nevyřeší, obraťte se na zákaznickou podporu DigiCert. |
| Poskytovatel DigiCert – nepovedlo se získat zásady DigiCert. <br><br>"Element požadavku není srozumitelný." | Službě Intune Certificate Connector se nepodařilo získat šablonu profilu certifikátu DigiCert, protože identifikátor objektu profilu klienta neodpovídá profilu certifikátu Intune. V jiném případě nemůže Intune Certificate Connector najít šablonu profilu certifikátu, která je přidružená k identifikátoru objektu profilu klienta v certifikační autoritě DigiCert. <br><br> Chcete-li vyřešit tento problém, Získejte správný identifikátor objektu profilu klienta z šablony certifikátu DigiCert v certifikační autoritě DigiCert. Pak aktualizujte profil certifikátu PKCS na portálu pro správu Intune. <br><br> Získání identifikátoru objektu profilu klienta z certifikační autority DigiCert: <br> 1. Přihlaste se na portál pro správu certifikační autority DigiCert. <br> 2. Vyberte možnost **Spravovat profily certifikátů**. <br> 3. Vyberte profil certifikátu, který chcete použít. <br> 4. Získejte identifikátor objektu profilu certifikátu. Vypadá podobně jako v následujícím příkladu: <br> `Certificate Profile OID = 2.16.840.1.113733.1.16.1.2.3.1.1.47196109` <br><br> Aktualizujte profil certifikátu PKCS pomocí správného identifikátoru objektu profilu certifikátu: <br>1. Přihlaste se na portál pro správu Intune. <br> 2. otevřete profil certifikátu PKCS a vyberte **Upravit**. <br> 3. aktualizujte identifikátor objektu profilu certifikátu v poli pro název šablony certifikátu. <br> 4. Uložte profil certifikátu PKCS. |
| DigiCert poskytovatele – ověření zásad se nezdařilo. <br><br> Atribut nespadají do seznamu podporovaných atributů šablony certifikátu DigiCert. | Certifikační autorita DigiCert zobrazí tuto zprávu, pokud dojde k nesouladu mezi šablonou profilu certifikátu DigiCert a profilem certifikátu Intune. K tomuto problému pravděpodobně došlo kvůli neshodě atributů v atributu **Subject** nebo **SubjectAltName**. <br><br> Pokud chcete tento problém vyřešit, vyberte v šabloně profilu certifikátu DigiCert atributy podporované v Intune pro atribut **Subject** a **SubjectAltName** . Další informace najdete v tématu Podporované atributy Intune v části **Parametry certifikátu** . |
| Některá zařízení uživatele nepřijímá certifikáty PKCS od certifikační autority DigiCert. | K tomuto problému dochází, pokud hlavní název uživatele (UPN) obsahuje speciální znaky, jako je podtržítko (příklad: `global_admin@intune.onmicrosoft.com` ). <br><br> Certifikační autorita DigiCert nepodporuje speciální znaky v **mail_firstname** a **mail_lastname**. <br><br> Tento problém vyřešíte následujícím postupem: <br><br> 1. Přihlaste se na portál pro správu certifikační autority DigiCert. <br> 2. Projděte si **Správa profilů certifikátů**. <br> 3. Vyberte profil certifikátu, který se používá pro Intune. <br> 4. Vyberte odkaz **Možnosti přizpůsobení** . <br> 5. Vyberte tlačítko **Upřesnit možnosti** . <br> 6. v části **pole certifikátu – rozlišující název předmětu**, přidejte pole **běžný název (CN)** a odstraňte existující pole **běžný název (CN)** . Operace přidávání a odstraňování se musí provádět společně. <br> 7. Vyberte **Save (Uložit**). <br><br> S předchozí změnou profil certifikátu DigiCert vyžádá **"CN = <upn> "** namísto **mail_firstname** a **mail_lastname**. |
| Uživatel ručně odstranil již nasazený certifikát ze zařízení. | Intune znovu nasadí stejný certifikát při dalším vrácení se změnami nebo vynucení zásad. V tomto případě konektor NDES neobdrží žádost o certifikát PKCS. |

## <a name="next-steps"></a>Další kroky

Informace v tomto článku použijte navíc k informacím v tématu [co jsou Microsoft Intune profily zařízení?](../configuration/device-profiles.md) ke správě zařízení organizace a certifikátů v nich.
