---
title: Řešení potíží s použitím profilů certifikátů PKCS k zřizování certifikátů s Microsoft Intune | Microsoft Docs
description: Řešení potíží s používáním profilů privátních a veřejných klíčů (PKCS) podle zařízení k vyžádání certifikátů pro použití s Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/11/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: acc61df344cb4134a863d75fff517047e78d067d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914782"
---
# <a name="troubleshoot-pkcs-certificate-deployment-in-microsoft-intune"></a>Řešení potíží s nasazením certifikátu PKCS v Microsoft Intune

Informace v tomto článku vám pomůžou vyřešit několik běžných problémů při nasazení privátních a veřejných certifikátů (PKCS) v Microsoft Intune. Před řešením potíží se ujistěte, že jste dokončili následující úlohy, které najdete v části [Konfigurace a používání certifikátů PKCS s Intune](../protect/certficates-pfx-configure.md#export-the-root-certificate-from-the-enterprise-ca):

- Přečtěte si [požadavky na používání profilů certifikátů PKCS](../protect/certficates-pfx-configure.md#requirements) .
- Export kořenového certifikátu od certifikační autority rozlehlé sítě (CA)
- Konfigurace šablon certifikátů v certifikační autoritě
- Instalace a konfigurace Intune Certificate Connectoru
- Vytvoření a nasazení profilu důvěryhodného certifikátu pro nasazení kořenového certifikátu
- Vytvoření a nasazení profilu certifikátu PKCS

Nejběžnějším zdrojem problémů s profily certifikátů PKCS je konfigurace profilu certifikátu PKCS. Zkontrolujte konfiguraci profilů a vyhledejte překlepy v názvech serverů nebo plně kvalifikované názvy domény (FQDN) a ověřte správnost názvu **certifikační autority** a **certifikační autority** .

- **Certifikační autorita**: interní plně kvalifikovaný název domény počítače certifikační autority. Například Server1. domain. Local.
- **Název certifikační autority**: název certifikační autority, jak se zobrazuje v konzole MMC Certifikační autorita. Podívejte se na části **certifikační autorita (místní)** .

K potvrzení správného názvu certifikační autority a názvu certifikační autority můžete použít [program příkazového řádku Certutil](/windows-server/administration/windows-commands/certutil) v certifikační autoritě.

## <a name="pkcs-communication-overview"></a>Přehled komunikace PKCS

Následující obrázek poskytuje základní přehled procesu nasazení certifikátu PKCS v Intune.

> [!div class="mx-imgBorder"]
> ![Tok profilu certifikátu PKCS](./media/troubleshoot-pkcs-certificate-profiles/pkcs-overview-graphic.png)

1. Správce vytvoří profil certifikátu PKCS v Intune.
2. Služba Intune vyžaduje, aby místní Intune Certificate Connector vytvořil pro uživatele nový certifikát.
3. Intune Certificate Connector pošle objekt BLOB PFX a zašle žádost certifikační autoritě Microsoftu.
4. Certifikační autorita vydá a pošle certifikát uživatele PFX zpátky do Intune Certificate Connectoru.
5. Intune Certificate Connector nahraje zašifrovaný certifikát uživatele PFX do Intune.
6. Intune dešifruje certifikát uživatele PFX a znovu zašifruje zařízení pomocí certifikátu správy zařízení.  Intune pak odešle certifikát uživatele PFX do zařízení.
7. Zařízení nahlásí stav certifikátu do Intune.

## <a name="data-and-log-files"></a>Data a soubory protokolů

Pokud chcete identifikovat problémy pro pracovní postup pro komunikaci a zřizování certifikátů, Projděte si soubory protokolů z serverové infrastruktury i ze zařízení. Pozdější oddíly pro odstraňování potíží se profily certifikátů PKCS najdete v souborech protokolu, na které odkazuje tato část.

- [Protokoly infrastruktury a serveru](#logs-for-on-premises-infrastructure)

Protokoly zařízení závisí na platformě zařízení:

- [iOS a iPadOS](#logs-for-ios-and-ipados-devices)
- [Android](#logs-for-android-devices)
- [Windows](#logs-for-windows-devices)

### <a name="logs-for-on-premises-infrastructure"></a>Protokoly pro místní infrastrukturu
  
Místní infrastruktura, která podporuje použití profilů certifikátů PKCS pro nasazení certifikátů, zahrnuje Microsoft Intune Certificate Connector, NDES, která běží na Windows serveru a certifikační autoritě.

Soubory protokolu pro tyto role zahrnují Prohlížeč událostí Windows, konzolu certifikátů a různé soubory protokolů, které jsou specifické pro Certificate Connector, NDES nebo jiné role a operace Intune, které jsou součástí místní infrastruktury.

- **NDESConnector_date_time. svclog**:

  Tento protokol zobrazuje komunikaci z Microsoft Intune Certificate Connector do cloudové služby Intune. K zobrazení tohoto souboru protokolu můžete použít [Nástroj Prohlížeč trasování služby](/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) .

  Související klíč registru: *HKLM\SW\Microsoft\MicrosoftIntune\NDESConnector\ConnectionStatus*

  Umístění: na serveru, který je hostitelem NDES, na adrese *% program_files% \ Microsoft intune\ndesconnectorsvc\logs\logs*

- **CertificateRegistrationPoint_date_time. svclog**:

  Tento protokol zobrazuje modul zásad NDES, který přijímá a ověřuje žádosti o certifikát. K zobrazení tohoto souboru protokolu můžete použít [Nástroj Prohlížeč trasování služby](/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) .

  Umístění: na serveru, který je hostitelem NDES, na adrese *% program_files% \ Microsoft intune\ndesconnectorsvc\logs\logs*

- **Souboru NDESPlugin. log**:

  Tento protokol zobrazuje předávání žádostí o certifikát na bod registrace certifikátu a výsledné ověřování těchto žádostí.

  Umístění: na serveru, který je hostitelem NDES, na adrese *% program_files% \ Microsoft Intune\NDESPolicyModule\logs*

- **Protokol aplikace systému Windows**:

  Umístění: na serveru, který je hostitelem NDES: Spusťte příkaz **eventvwr. msc** a otevřete Windows Prohlížeč událostí

### <a name="logs-for-android-devices"></a>Protokoly pro zařízení s Androidem

U zařízení se systémem Android použijte soubor protokolu aplikace pro **Android portál společnosti** **OMADM. log**. Než shromáždíte a zkontrolujete protokoly, povolte zajistěte, aby bylo zapnuté [podrobné protokolování](../user-help/use-verbose-logging-to-help-your-it-administrator-fix-device-issues-android.md) , a pak problém reprodukovánte.

Postup shromáždění protokolu OMADM. log ze zařízení najdete v tématu [nahrání a e-mailové protokoly pomocí kabelu USB](../user-help/send-logs-to-your-it-admin-using-cable-android.md).

Můžete také [nahrávat a e-mailem protokoly](../user-help/send-logs-to-your-it-admin-by-email-android.md#upload-and-email-logs-from-microsoft-intune-app) pro podporu.

### <a name="logs-for-ios-and-ipados-devices"></a>Protokoly pro zařízení s iOS a iPadOS

U zařízení se systémem iOS nebo iPadOS používáte protokoly ladění a **Xcode** , které běží na počítači Mac:

1. Připojte zařízení se systémem iOS/iPadOS k počítači Mac a potom **Applications**  >  **Utilities** v okně aplikace otevřete konzolovou aplikaci.

2. V části **Akce**vyberte **Zahrnout informační zprávy** a **zahrnout zprávy ladění**.

   ![Výběr možností protokolu](../protect/media/troubleshoot-pkcs-certificate-profiles/message-options.png)

3. Reprodukování problému a uložení protokolů do textového souboru:
   1. Vyberte **Upravit**  >  **Vybrat vše** , pokud chcete vybrat všechny zprávy na aktuální obrazovce a pak vybrat **Upravit**  >  **kopii** a zkopírovat zprávy do schránky.
   2. Otevřete aplikaci TextEdit, vložte zkopírované protokoly do nového textového souboru a uložte soubor.

Protokol Portál společnosti pro zařízení s iOS a iPadOS neobsahuje informace o profilech certifikátů PKCS.

### <a name="logs-for-windows-devices"></a>Protokoly pro zařízení s Windows

U zařízení s Windows použijte protokoly událostí Windows k diagnostice problémů se správou registrace nebo zařízení u zařízení, která spravujete přes Intune.

Na zařízení otevřete **Prohlížeč událostí**  >  **aplikace a protokoly služeb**  >  **Microsoft**  >  **Windows**  >  **DeviceManagement-Enterprise-Diagnostics-Provider**

![Protokoly událostí Windows](../protect/media/troubleshoot-pkcs-certificate-profiles/windows-event-log.png)

## <a name="antivirus-exclusions"></a>Vyloučení antivirové ochrany

Zvažte přidání vyloučení antivirové ochrany na servery, které hostují NDES nebo Certificate Connector v těchto případech:

- Žádosti o certifikát mají přístup k serveru nebo k Intune Certificate Connectoru, ale nezpracovávají se úspěšně. 
- Certifikáty jsou vydávány pomalu

Tady jsou příklady umístění, která byste mohli vyloučit:

- *% program_files%* \Microsoft Intune\PfxRequest
- *% program_files%* \Microsoft Intune\CertificateRequestStatus
- *% program_files%* \Microsoft Intune\CertificateRevocationStatus

## <a name="common-errors"></a>Běžné chyby

Všechny následující běžné chyby jsou řešeny v následující části:

- [Server RPC je nedostupný 0x800706ba](#the-rpc-server-is-unavailable-0x800706ba)
- [Server zásad zápisu nejde najít 0x80094015](#an-enrollment-policy-server-cannot-be-located-0x80094015)
- [Odeslání čeká na vyřízení.](#the-submission-is-pending)
- [Parametr je nesprávný 0x80070057.](#the-parameter-is-incorrect-0x80070057)
- [Zakázáno modulem zásad](#denied-by-policy-module)
- [Profil certifikátu se zablokuje jako dokončený.](#certificate-profile-stuck-as-pending)
- [Chyba-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED](#error--2146875374-certsrv_e_subject_email_required)

### <a name="the-rpc-server-is-unavailable-0x800706ba"></a>Server RPC je nedostupný 0x800706ba

Během nasazování PFX se důvěryhodný kořenový certifikát zobrazí v zařízení, ale certifikát PFX se v zařízení nezobrazí. Soubor protokolu NDESConnector obsahuje řetězec, **který server RPC není k dispozici. 0x800706ba**, jak je vidět na prvním řádku následujícího příkladu:

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x800706BA): CCertRequest::Submit: The RPC server is unavailable. 0x800706ba (WIN32: 1722 RPC_S_SERVER_UNAVAILABLE)
IssuePfx -Generic Exception: System.ArgumentException: CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094800): The requested certificate template is not supported by this CA. (Exception from HRESULT: 0x80094800)
```

#### <a name="cause-1---incorrect-configuration-of-the-ca-in-intune"></a>Příčina 1 – nesprávné konfigurace certifikační autority v Intune

K tomuto problému může dojít, když profil certifikátu PKCS určuje nesprávný Server nebo obsahuje pravopisné chyby pro název nebo plně kvalifikovaný název domény certifikační autority. Certifikační autorita je určena v následujících vlastnostech profilu:

- Certification authneboity
- Název certifikační autority

**Řešení**:

Zkontrolujte následující nastavení a opravte, pokud jsou nesprávné:

- Vlastnost **certifikační autorita** zobrazuje interní plně kvalifikovaný název domény serveru certifikační autority.
- Vlastnost **název certifikační autority** zobrazuje název vaší certifikační autority.

#### <a name="cause-2---ca-doesnt-support-certificate-renewal-for-requests-signed-by-previous-ca-certificates"></a>Příčina 2 – certifikační autorita nepodporuje obnovení certifikátu pro požadavky podepsané předchozími certifikáty certifikační autority.

Pokud je plně kvalifikovaný název domény a název certifikační autority správný v profilu certifikátu PKCS, zkontrolujte protokol aplikací systému Windows, který je na serveru certifikační autority. Vyhledejte událost s **ID 128** , která se podobá následujícímu příkladu:

```
Log Name: Application:
Source: Microsoft-Windows-CertificationAuthority
Event ID: 128
Level: Warning
Details:
An Authority Key Identifier was passed as part of the certificate request 2268. This feature has not been enabled. To enable specifying a CA key for certificate signing, run: "certutil -setreg ca\UseDefinedCACertInRequest 1" and then restart the service.
```

Po obnovení certifikátu certifikační autority musí být certifikát pro podepisování odpovědí protokolu OCSP (Online Certificate Status Protocol) podepsán. Podepisování umožňuje certifikátu Podepisování odpovědí protokolu OCSP ověřit další certifikáty kontrolou jejich stavu odvolání. Toto podepisování není ve výchozím nastavení povolené.

**Řešení**:

Ruční vynucení podepsání certifikátu:

1. Na serveru certifikační autority otevřete příkazový řádek se zvýšenými oprávněními a spusťte následující příkaz: **certutil-setreg ca\UseDefinedCACertInRequest 1**
2. Restartujte službu Certificate Services.

Po restartování služby Certificate Services můžou zařízení přijímat certifikáty.

### <a name="an-enrollment-policy-server-cannot-be-located-0x80094015"></a>Server zásad zápisu nejde najít 0x80094015

**Server zásad zápisu nejde najít** a **0x80094015**, jak je vidět v následujícím příkladu:

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094015): An enrollment policy server cannot be located. (Exception from HRESULT: 0x80094015)
```

#### <a name="cause---certificate-enrollment-policy-server-name"></a>Příčina – název serveru zásad zápisu certifikátů

K tomuto problému dochází, pokud počítač, který je hostitelem konektoru NDES služby Intune, nemůže najít server zásad zápisu certifikátů.

**Řešení**:

Ručně nakonfigurujte název serveru zásad zápisu certifikátů na počítači, který je hostitelem konektoru NDES. Pokud chcete nakonfigurovat název, použijte rutinu prostředí PowerShell [Add-CertificateEnrollmentPolicyServer](/powershell/module/pkiclient/add-certificateenrollmentpolicyserver?view=win10-ps) .

### <a name="the-submission-is-pending"></a>Odeslání čeká na vyřízení.

Po nasazení profilu certifikátu PKCS do mobilních zařízení se certifikáty nezískávají a protokol NDESConnector obsahuje řetězec, **který odeslání čeká na vyřízení**, jak je vidět v následujícím příkladu:

```
IssuePfx - The submission is pending: Taken Under Submission
IssuePfx -Generic Exception: System.InvalidOperationException: IssuePfx - The submission is pending
```

Na serveru certifikační autority můžete navíc ve složce **nedokončené žádosti** zobrazit žádost o PFX:

> [!div class="mx-imgBorder"]
> ![Snímek složky nedokončené žádosti certifikační autority](./media/troubleshoot-pkcs-certificate-profiles/pending-requests.png)

#### <a name="cause---incorrect-configuration-for-request-handling"></a>Příčina – nesprávná konfigurace pro zpracování žádostí

K tomuto problému dochází, pokud možnost **nastaví stav požadavku na čeká na vyřízení. Správce musí explicitně vydat certifikát, který** je vybrán v dialogovém okně vlastnosti **Properties**  >  **modulu zásad**certifikační autority  >  **Properties** .

> [!div class="mx-imgBorder"]
> ![Snímek obrazovky s vlastnostmi modulu zásad](./media/troubleshoot-pkcs-certificate-profiles/policy-module-properties.png)

**Řešení**:

Upravte vlastnosti modulu zásad tak, aby se nastavily: **postupujte podle nastavení v šabloně certifikátu (Pokud je k dispozici). V opačném případě automaticky vystavte certifikát.**

### <a name="the-parameter-is-incorrect-0x80070057"></a>Parametr je nesprávný 0x80070057.

Po úspěšné instalaci a konfiguraci Intune Certificate Connectoru zařízení neobdrží certifikáty PKCS a protokol NDESConnector obsahuje řetězec **, který má parametr nesprávný. 0x80070057**, jak je vidět v následujícím příkladu:

```
CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
```

#### <a name="cause---configuration-of-the-pkcs-profile"></a>Příčina – konfigurace profilu PKCS

K tomuto problému dochází, pokud je profil PKCS v Intune nesprávně nakonfigurovaný. Zde jsou běžné nepoužívané konfigurace:

- Profil obsahuje nesprávný název certifikační autority.
- Alternativní název subjektu (SAN) je nakonfigurován pro e-mailovou adresu, ale cílový uživatel ještě nemá platnou e-mailovou adresu. Tato kombinace má za následek hodnotu null pro síť SAN, která je neplatná.

**Řešení**:

Ověřte následující konfigurace profilu PKCS a potom počkejte, než se zásada aktualizuje na zařízení:

- Nakonfigurováno s názvem certifikační autority
- Přiřazeno ke správné skupině uživatelů
- Uživatelé ve skupině mají platné e-mailové adresy.

Další informace najdete v tématu [Konfigurace a používání certifikátů PKCS pomocí Intune](../protect/certficates-pfx-configure.md).

### <a name="denied-by-policy-module"></a>Zakázáno modulem zásad

Když zařízení obdrží důvěryhodný kořenový certifikát, ale neobdrží certifikát PFX a protokol NDESConnector obsahuje řetězec **, který odeslání selhalo: zamítnuto modulem zásad**, jak je vidět v následujícím příkladu:

```
IssuePfx - The submission failed: Denied by Policy Module
IssuePfx -Generic Exception: System.InvalidOperationException: IssuePfx - The submission failed
   at Microsoft.Management.Services.NdesConnector.MicrosoftCA.GetCertificate(PfxRequestDataStorage pfxRequestData, String containerName, String& certificate, String& password)
Issuing Pfx certificate for Device ID <Device ID> failed  
```

#### <a name="cause--computer-account-permissions-to-the-certificate-template"></a>Příčina – oprávnění účtu počítače pro šablonu certifikátu

K tomuto problému dochází, když počítačový účet serveru, který je hostitelem Intune Certificate Connectoru, nemá oprávnění k šabloně certifikátu.

**Řešení**:

1. Přihlaste se do certifikační autority organizace pomocí účtu, který má oprávnění správce.
2. Otevřete konzolu **certifikační autorita** , klikněte pravým tlačítkem na **šablony certifikátů a vyberte Spravovat**.
3. Vyhledejte šablonu certifikátu a otevřete dialogové okno **vlastnosti** šablony.
4. Vyberte kartu **zabezpečení** a přidejte účet počítače pro server, na který jste nainstalovali Microsoft Intune Certificate Connector. Udělte účtu oprávnění **ke čtení** a **zápisu** .
5. Kliknutím na tlačítko **použít**  >  **OK** uložte šablonu certifikátu a poté zavřete konzolu **šablony certifikátů** .
6. V konzole **Certifikační autorita** klikněte pravým tlačítkem myši na **Šablony certifikátů** > **Nová** > **Vystavovaná šablona certifikátu**.
7. Vyberte šablonu, kterou jste upravili, a poté klikněte na tlačítko **OK**.

Další informace najdete v tématu [Konfigurace šablon certifikátů v certifikační autoritě](../protect/certficates-pfx-configure.md#configure-certificate-templates-on-the-ca).

### <a name="certificate-profile-stuck-as-pending"></a>Profil certifikátu se zablokuje jako dokončený.

V centru pro správu Microsoft Endpoint Manageru se nedaří nasadit profily certifikátů PKCS se stavem **čeká na vyřízení**. V souboru protokolu NDESConnector nejsou žádné zjevné chyby.
Vzhledem k tomu, že příčina tohoto problému není v protokolech jasně identifikovaná, pracujte v následujících příčinách.

#### <a name="cause-1---unprocessed-request-files"></a>Příčina 1 – nezpracované soubory žádostí

Zkontrolujte soubory žádostí o chyby, které indikují, proč se nezdařily zpracování.

1. V počítači, který je hostitelem konektoru NDES, přejděte pomocí Průzkumníka souborů na **%ProgramFiles%\Microsoft Intune\PfxRequest**.
2. Zkontrolujte soubory v **neúspěšných** a **zpracovávaných** složkách pomocí oblíbeného textového editoru.

   > [!div class="mx-imgBorder"]
   > ![Kontrola složky PfxRequest](./media/troubleshoot-pkcs-certificate-profiles/pfxrequest-folder.png)

3. V těchto souborech hledejte záznamy, které označují chyby nebo Navrhujte problémy. Pomocí webového vyhledávání vyhledejte chybové zprávy, které se týkají, proč se žádost nezdařila, a pro řešení těchto problémů.

#### <a name="cause-2---misconfiguration-for-the-pkcs-certificate-profile"></a>Příčina 2 – chyby konfigurace profilu certifikátu PKCS

Pokud nenajdete soubory požadavků ve složkách, které **selhaly**, **zpracování**nebo jsou **úspěšné** , příčinou může být to, že je k profilu certifikátu PKCS přidružen nesprávný certifikát. Například podřízená certifikační autorita je přidružena k profilu, nebo je použit nesprávný kořenový certifikát.

**Řešení**:

1. Zkontrolujte profil důvěryhodného certifikátu a ujistěte se, že jste nasadili kořenový certifikát z certifikační autority organizace na zařízení.
2. Zkontrolujte svůj profil certifikátu PKCS a ujistěte se, že odkazuje na správnou certifikační autoritu, typ certifikátu a profil důvěryhodného certifikátu, který nasadí kořenový certifikát do zařízení.

Další informace najdete v tématu [použití certifikátů pro ověřování](../protect/certificates-configure.md) v Microsoft Intune.

### <a name="error--2146875374-certsrv_e_subject_email_required"></a>Chyba-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED

Certifikáty PKCS se nepodařilo nasadit a konzola certifikátů ve vydávající certifikační autoritě zobrazí zprávu s řetězcem **2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED**, jak je vidět v následujícím příkladu:

```
Active Directory Certificate Services denied request abc123 because The Email name is unavailable and cannot be added to the Subject or Subject Alternate name. 0x80094812 (-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED). The request was for CN=” Common Name”.  Additional information: Denied by Policy Module”.
```

#### <a name="cause---supply-in-the-request-is-miscongifured"></a>Příčina – "poskytnutí v žádosti" je miscongifured

K tomuto problému dochází, pokud není v dialogovém okně **vlastnosti** šablony certifikátu na kartě **název subjektu** povolená možnost **dodávat v žádosti** .

> [!div class="mx-imgBorder"]
> ![Konfigurace vlastností NDES](./media/troubleshoot-pkcs-certificate-profiles/supply-in-the-request.png)

**Řešení**:

Upravte šablonu pro vyřešení problému s konfigurací:

1. Přihlaste se do certifikační autority organizace pomocí účtu, který má oprávnění správce.
2. Otevřete konzolu **Certifikační autorita** klikněte pravým tlačítkem myši na **Šablony certifikátů** a vyberte **Spravovat**.
3. Otevřete dialogové okno Vlastnosti šablony certifikátu.
4. Na kartě **Název subjektu** vyberte možnost **Dodán v žádosti**.
5. Výběrem **OK** uložte šablonu certifikátu a pak zavřete konzolu **šablony certifikátů** .
6. V konzole **certifikační autorita** klikněte pravým tlačítkem na **šablony**  >  **Nová**  >  **Šablona certifikátu k vystavení**.
7. Vyberte šablonu, kterou jste upravili, a pak vyberte **OK**.

## <a name="next-steps"></a>Další kroky

Pokud stále potřebujete nějaké řešení nebo chcete získat další informace o Intune, odešlete na našem [Microsoft Intune Fórum](https://social.technet.microsoft.com/Forums/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)dotaz. Mnohé pracovníky podpory, MVP a členové našeho vývojového týmu se často vyskytují ve fórech, takže je velmi pravděpodobné, že vám někdo může pomoci.

Pokud chcete otevřít žádost o podporu pro tým podpory Microsoft Intune produktů, přečtěte si téma [Jak získat podporu pro Microsoft Intune](../fundamentals/get-support.md).
Další informace o nasazení certifikátů PKCS najdete v následujících článcích:

- [Konfigurace a používání certifikátů PKCS pomocí Intune](../protect/certficates-pfx-configure.md)
- [Konfigurace profilu certifikátu pro zařízení v Microsoft Intune](../protect/certificates-configure.md)
- [Odebrání certifikátů SCEP a PKCS v Microsoft Intune](../protect/remove-certificates.md)