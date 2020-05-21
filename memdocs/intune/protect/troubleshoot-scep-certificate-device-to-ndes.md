---
title: Řešení potíží se spravovaným zařízením a komunikací NDES v Microsoft Intune | Microsoft Docs
description: Řešení potíží se spravovaným zařízením na server NDES při použití profilů certifikátů SCEP k nasazení certifikátů v Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/30/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c538236d57961298ff7caedd6d5e00e7cc78c4a6
ms.sourcegitcommit: 6ca5e75ed7a6fd2186fbe51c177960004d5ec81f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/19/2020
ms.locfileid: "83633373"
---
# <a name="troubleshoot-device-to-ndes-server-communication-for-scep-certificate-profiles-in-microsoft-intune"></a>Řešení potíží s komunikací serveru NDES pro profily certifikátů SCEP v Microsoft Intune

Pomocí následujících informací zjistíte, jestli zařízení, které přijalo a zpracovalo profil certifikátu SCEP (Intune Simple Certificate Enrollment Protocol), může úspěšně kontaktovat službu zápisu síťových zařízení (NDES), aby se mohla zobrazit výzva. Na zařízení se vygeneruje soukromý klíč a žádost o podepsání certifikátu (CSR) a výzva se ze zařízení předává na server NDES. Pokud chcete kontaktovat server NDES, zařízení použije identifikátor URI z profilu certifikátu SCEP.

Tento článek se odkazuje na krok 2 [přehledu komunikačního toku SCEP](troubleshoot-scep-certificate-profiles.md).

## <a name="review-iis-logs-for-a-connection-from-the-device"></a>Přečtěte si protokoly služby IIS pro připojení ze zařízení.

Protokoly služby IIS obsahují stejný typ položek pro všechny platformy.


1. Na serveru NDES otevřete nejnovější soubor protokolu služby IIS, který najdete v následující složce: *%systemdrive%\inetpub\logs\LogFiles\W3SVC1*

2. V protokolu vyhledejte položky podobné následujícím příkladům. Oba příklady obsahují stav **200**, který se zobrazí poblíž konce:

   `fe80::f53d:89b8:c3e8:5fec%13 GET /certsrv/mscep/mscep.dll/pkiclient.exe operation=GetCACaps&message=default 80 - fe80::f53d:89b8:c3e8:5fec%13 Mozilla/4.0+(compatible;+Win32;+NDES+client) - 200 0 0 186 0.`

   And

   `fe80::f53d:89b8:c3e8:5fec%13 GET /certsrv/mscep/mscep.dll/pkiclient.exe operation=GetCACert&message=default 80 - fe80::f53d:89b8:c3e8:5fec%13 Mozilla/4.0+(compatible;+Win32;+NDES+client) - 200 0 0 3567 0`

3. Když zařízení kontaktuje službu IIS, zaprotokoluje se požadavek HTTP GET pro mscep. dll.

   Zkontrolujte stavový kód na konci tohoto požadavku:
   - **Stavový kód 200**: Tento stav označuje úspěšné připojení k serveru NDES.
   - **Stavový kód 500**: Skupina IIS_IURS pravděpodobně nemá správná oprávnění. Viz část [stavový kód 500](#status-code-500)dále v tomto článku.
   - Pokud kód stavu není 200 nebo 500:

     - Další informace o ověření konfigurace najdete v části [test adresy URL serveru SCEP](#test-the-scep-server-url) dále v tomto článku.

     - Informace o méně běžných kódech chyb najdete v [kódu stavu HTTP ve službě IIS 7 a novějších verzích](https://support.microsoft.com/help/943891) .

   Pokud se žádost o připojení nezaznamená, může být kontakt ze zařízení blokovaný v síti mezi zařízením a serverem NDES.

## <a name="review-device-logs-for-connections-to-ndes"></a>Kontrola protokolů zařízení pro připojení k NDES

### <a name="android-devices"></a>Zařízení s Androidem

Zkontrolujte [protokol OMADM zařízení](troubleshoot-scep-certificate-profiles.md#logs-for-android-devices). Vyhledat položky, které se podobají následujícímu protokolu, které jsou protokolovány při připojení zařízení k NDES:

```
2018-02-27T05:16:08.2500000  VERB  Event  com.microsoft.omadm.platforms.android.certmgr.CertificateEnrollmentManager  18327    10  There are 1 requests
2018-02-27T05:16:08.2500000  VERB  Event  com.microsoft.omadm.platforms.android.certmgr.CertificateEnrollmentManager  18327    10  Trying to enroll certificate request: ModelName=AC_51bad41f-3854-4eb5-a2f2-0f7a94034ee8%2FLogicalName_39907e78_e61b_4730_b9fa_d44a53e4111c;Hash=1677525787
2018-02-27T05:16:09.5530000  VERB  Event  org.jscep.transport.UrlConnectionGetTransport  18327    10  Sending GetCACaps(ca) to https://<server>.msappproxy.net/certsrv/mscep/mscep.dll?operation=GetCACaps&message=ca
2018-02-27T05:16:14.6440000  VERB  Event  org.jscep.transport.UrlConnectionGetTransport  18327    10  Received '200 OK' when sending GetCACaps(ca) to https://<server>.msappproxy.net/certsrv/mscep/mscep.dll?operation=GetCACaps&message=ca
2018-02-27T05:16:21.8220000  VERB  Event  org.jscep.message.PkiMessageEncoder  18327     10 Encoding message: org.jscep.message.PkcsReq@2b06f45f[messageData=org.<server>.pkcs.PKCS10CertificationRequest@699b3cd,messageType=PKCS_REQ,senderNonce=Nonce [D447AE9955E624A56A09D64E2B3AE76E],transId=251E592A777C82996C7CF96F3AAADCF996FC31FF]
2018-02-27T05:16:21.8790000  VERB  Event  org.jscep.message.PkiMessageEncoder  18327     10  Signing pkiMessage using key belonging to [dn=CN=<uesrname>; serial=1]
2018-02-27T05:16:21.9580000  VERB  Event  org.jscep.transaction.EnrollmentTransaction  18327     10  Sending org.<server>.cms.CMSSignedData@ad57775
```

Klíčové položky obsahují následující vzorové textové řetězce:

- K dispozici jsou 1 žádosti.
- Při odesílání GetCACaps (CA) do serveru https://byla přijata zpráva "200 OK" \<>. msappproxy.net/certsrv/mscep/mscep.dll?operation=GetCACaps&zpráva = CA
- Podepisování pkiMessage pomocí klíče patřícího k [DN = CN = \< username>; Serial = 1]


Služba IIS protokoluje i připojení ve složce%SystemDrive%\inetpub\logs\LogFiles\W3SVC1\ serveru NDES. Například:

```
fe80::f53d:89b8:c3e8:5fec%13 GET /certsrv/mscep/mscep.dll operation=GetCACert&message=ca 443 - 
fe80::f53d:89b8:c3e8:5fec%13 Dalvik/2.1.0+(Linux;+U;+Android+5.0;+P01M+Build/LRX21V) - 200 0 0 3909 0
fe80::f53d:89b8:c3e8:5fec%13 GET /certsrv/mscep/mscep.dll operation=GetCACaps&message=ca 443 - 
fe80::f53d:89b8:c3e8:5fec%13 Dalvik/2.1.0+(Linux;+U;+Android+5.0;+P01M+Build/LRX21V) - 200 0 0 421 
```

### <a name="iosipados-devices"></a>zařízení s iOS/iPadOS

Zkontrolujte [protokol ladění zařízení](troubleshoot-scep-certificate-profiles.md#logs-for-ios-and-ipados-devices). Vyhledat položky, které se podobají následujícímu protokolu, které jsou protokolovány při připojení zařízení k NDES:

```
debug    18:30:53.691033 -0500    profiled    Performing synchronous URL request: https://<server>-contoso.msappproxy.net/certsrv/mscep/mscep.dll?operation=GetCACert&message=SCEP%20Authority\ 
debug    18:30:54.640644 -0500    profiled    Performing synchronous URL request: https://<server>-contoso.msappproxy.net/certsrv/mscep/mscep.dll?operation=GetCACaps&message=SCEP%20Authority\ 
default    18:30:55.483977 -0500    profiled    Attempting to retrieve issued certificate...\ 
debug    18:30:55.487798 -0500    profiled    Sending CSR via GET.\  
debug    18:30:55.487908 -0500    profiled    Performing synchronous URL request: https://<server>-contoso.msappproxy.net/certsrv/mscep/mscep.dll?operation=PKIOperation&message=MIAGCSqGSIb3DQEHAqCAMIACAQExDzANBglghkgBZQMEAgMFADCABgkqhkiG9w0BBwGggCSABIIZfzCABgkqhkiG9w0BBwOggDCAAgEAMYIBgjCCAX4CAQAwZjBPMRUwEwYKCZImiZPyLGQBGRYFbG9jYWwxHDAaBgoJkiaJk/IsZAEZFgxmb3VydGhjb2ZmZWUxGDAWBgNVBAMTD0ZvdXJ0aENvZmZlZSBDQQITaAAAAAmaneVjEPlcTwAAAAAACTANBgkqhkiG9w0BAQEFAASCAQCqfsOYpuBToerQLkw/tl4tH9E+97TBTjGQN9NCjSgb78fF6edY0pNDU+PH4RB356wv3rfZi5IiNrVu5Od4k6uK4w0582ZM2n8NJFRY7KWSNHsmTIWlo/Vcr4laAtq5rw+CygaYcefptcaamkjdLj07e/Uk4KsetGo7ztPVjSEFwfRIfKv474dLDmPqp0ZwEWRQGZwmPoqFMbX3g85CJT8khPaqFW05yGDTPSX9YpuEE0Bmtht9EwOpOZe6O7sd77IhfFZVmHmwy5mIYN7K6mpx/4Cb5zcNmY3wmTBlKEkDQpZDRf5PpVQ3bmQ3we9XxeK1S4UsAXHVdYGD+bg/bCafMIAGCSqGSIb3DQEHATAUBggqhkiG9w0DBwQI5D5J2lwZS5OggASCF6jSG9iZA/EJ93fEvZYLV0v7GVo3JAsR11O7DlmkIqvkAg5iC6DQvXO1j88T/MS3wV+rqUbEhktr8Xyf4sAAPI4M6HMfVENCJTStJw1PzaGwUJHEasq39793nw4k268UV5XHXvzZoF3Os2OxUHSfHECOj
```

Klíčové položky obsahují následující vzorové textové řetězce:

- operace = GetCACert
- Probíhá pokus o načtení vystaveného certifikátu.
- Odeslání CSR prostřednictvím GET
- operace = PKIOperation

### <a name="windows-devices"></a>Zařízení s Windows

Na zařízení s Windows, které provádí připojení ke službě NDES, můžete zobrazit Prohlížeč událostí zařízení s Windows a vyhledat indikaci úspěšného připojení. Připojení se protokolují jako ID události **36** v DeviceManagement zařízení *-Enterprise-Diagnostics – poskytnutí*  >  protokolu**správce** .

Postup otevření protokolu:

1. Na zařízení spusťte příkaz **eventvwr. msc** a otevřete Prohlížeč událostí Windows.

2. Rozbalte položku **protokoly aplikací a služeb**  >  **Microsoft**  >  **Windows**  >  **DeviceManagement-Enterprise-Diagnostic-Provider**  >  **admin**.

3. Vyhledejte událost **36**, která se podobá následujícímu příkladu, a to pomocí klíčového řádku protokolu **SCEP: žádost o certifikát se úspěšně vygenerovala**:

   ```
   Event ID:      36
   Task Category: None
   Level:         Information
   Keywords:
   User:          <UserSid>
   Computer:      <Computer Name>
   Description:
   SCEP: Certificate request generated successfully. Enhanced Key Usage: (1.3.6.1.5.5.7.3.2), NDES URL: (https://<server>/certsrv/mscep/mscep.dll/pkiclient.exe), Container Name: (), KSP Setting: (0x2), Store Location: (0x1).
   ```

## <a name="troubleshoot-common-errors"></a>Odstraňování běžných chyb

Následující části vám pomohou při běžných potížích s připojením ze všech platforem zařízení do NDES.

### <a name="status-code-500"></a>Stavový kód 500

Připojení, která se podobají následujícímu příkladu, s kódem stavu 500, označují *zosobnění klienta po ověření* uživatele, které není přiřazeno ke skupině IIS_IURS na serveru NDES. Stavová hodnota **500** se zobrazí na konci:

```
2017-08-08 20:22:16 IP_address GET /certsrv/mscep/mscep.dll operation=GetCACert&message=SCEP%20Authority 443 - 10.5.14.22 profiled/1.0+CFNetwork/811.5.4+Darwin/16.6.0 - 500 0 1346 31
```

**Chcete-li tento problém vyřešit**:

1. Na serveru NDES spusťte **secpol. msc** a otevřete místní zásady zabezpečení.

2. Rozbalte **místní zásady**a pak klikněte na **přiřazení uživatelských práv**.

3. Po ověření v pravém podokně dvakrát klikněte na **zosobnit klienta** .

4. Klikněte **na Přidat uživatele nebo skupinu...**, do **pole zadejte názvy objektů k výběru**zadejte **IIS_IURS** a pak klikněte na **OK**.

5. Klikněte na tlačítko **OK**.

6. Restartujte počítač a potom se znovu pokuste o připojení ze zařízení.

### <a name="test-the-scep-server-url"></a>Otestování adresy URL serveru SCEP

Pomocí následujícího postupu otestujte adresu URL, která je zadaná v profilu certifikátu SCEP.

1. V Intune upravte svůj profil certifikátu SCEP a zkopírujte adresu URL serveru. Adresa URL by měla vypadat přibližně takto `https://contoso.com/certsrv/mscep/mscep.dll` .

2. Otevřete webový prohlížeč a přejděte na adresu URL serveru SCEP. Výsledek by měl být: **Chyba protokolu HTTP 403,0 – zakázáno**. Tento výsledek indikuje, že adresa URL funguje správně.

   Pokud se tato chyba nezobrazuje, vyberte odkaz, který se podobá chybě, která se zobrazí při zobrazení pokynů pro konkrétní problém:
   - [Zobrazuje se obecná zpráva služby zápisu síťových zařízení.](#general-ndes-message)
   - [Zobrazuje se zpráva "Chyba protokolu HTTP 503. Služba není k dispozici. "](#http-error-503)
   - [Zobrazuje se chyba "GatewayTimeout"](#gatewaytimeout)
   - [Zobrazuje se příliš dlouhý identifikátor požadavku HTTP 414.](#http-414-request-uri-too-long)
   - [Zobrazuje se mi tato stránka se nedá zobrazit.](#this-page-cant-be-displayed)
   - [Zobrazuje se zpráva "500 – interní chyba serveru"](#internal-server-error)

#### <a name="general-ndes-message"></a>Obecná zpráva NDES

Když přejdete na adresu URL serveru SCEP, obdržíte následující zprávu služby zápisu síťových zařízení:

![Adresa URL serveru SCEP](../protect/media/troubleshoot-scep-certificate-device-to-ndes/ndes-server-url-message.png)

- **Příčina**: k tomuto problému obvykle dochází v případě potíží s instalací konektoru Microsoft Intune.

  Mscep. dll je rozšíření ISAPI, které zachycuje příchozí požadavek a zobrazí chybu HTTP 403, pokud je správně nainstalován.
  
  **Řešení**: Zkontrolujte soubor *SetupMsi. log* a zjistěte, zda byl konektor Microsoft Intune úspěšně nainstalován. V následujícím příkladu se *instalace úspěšně dokončila* a byla dokončena *instalace nebo stav chyby: 0* označuje úspěšnou instalaci:

  ```
  MSI (c) (28:54) [16:13:11:905]: Product: Microsoft Intune Connector -- Installation completed successfully.
  MSI (c) (28:54) [16:13:11:999]: Windows Installer installed the product. Product Name: Microsoft Intune Connector. Product Version: 6.1711.4.0. Product Language: 1033. Manufacturer: Microsoft Corporation. Installation success or error status: 0.
  ```

  Pokud instalace neproběhne úspěšně, odeberte konektor Microsoft Intune a pak ho znovu nainstalujte.

#### <a name="http-error-503"></a>Chyba protokolu HTTP 503

Když přejdete na adresu URL serveru SCEP, zobrazí se následující chyba:

![Chyba protokolu HTTP 503. Služba není k dispozici.](../protect/media/troubleshoot-scep-certificate-device-to-ndes/service-unavailable.png)

K tomuto problému obvykle dochází, protože ve službě IIS není spuštěn fond aplikací **SCEP** . Na serveru NDES otevřete **Správce služby IIS** a pokračujte na **fondy aplikací**. Vyhledejte fond aplikací **SCEP** a potvrďte jeho spuštění.

Pokud není fond aplikací SCEP spuštěný, podívejte se na protokol událostí aplikace na serveru:

1. Na zařízení spusťte příkaz **eventvwr. msc** , který otevřete **Prohlížeč událostí** a přejdete do části **Windows logs**  >  **aplikace**.

2. Vyhledejte událost, která je podobná následujícímu příkladu, což znamená, že fond aplikací selže při přijetí žádosti:

   ```
   Log Name:      Application
   Source:        Application Error
   Event ID:      1000
   Task Category: Application Crashing Events
   Level:         Error
   Keywords:      Classic
   Description: Faulting application name: w3wp.exe, version: 8.5.9600.16384, time stamp: 0x5215df96
   Faulting module name: ntdll.dll, version: 6.3.9600.18821, time stamp: 0x59ba86db
   Exception code: 0xc0000005
   ```

**Běžné příčiny selhání fondu aplikací**:

- **Příčina 1**: v úložišti certifikátů důvěryhodných kořenových certifikačních AUTORIT serveru NDES jsou k dispozici zprostředkující certifikáty certifikační autority (bez podpisu držitele).

  **Řešení**: Odeberte zprostředkující certifikáty z úložiště certifikátů důvěryhodných kořenových certifikačních autorit a pak restartujte server NDES.
  
  Chcete-li identifikovat všechny zprostředkující certifikáty v úložišti certifikátů důvěryhodných kořenových certifikačních autorit, spusťte následující rutinu prostředí PowerShell:`Get-Childitem -Path cert:\LocalMachine\root -Recurse | Where-Object {$_.Issuer -ne $_.Subject}`

  Certifikát, který má stejný **stav vydaný pro** a **vydaný** hodnotou, je kořenový certifikát. V opačném případě se jedná o zprostředkující certifikát.

  Po odebrání certifikátů a restartování serveru znovu spusťte rutinu PowerShellu a potvrďte, že nejsou k dispozici žádné zprostředkující certifikáty. Pokud existují, ověřte, zda Zásady skupiny předá zprostředkující certifikáty k serveru NDES. Pokud ano, vylučte Server NDES ze Zásady skupiny a znovu odeberte zprostředkující certifikáty.

- **Příčina 2**: adresy URL v seznamu odvolaných certifikátů (CRL) jsou blokované nebo nedosažitelné pro certifikáty, které používá Certificate Connector služby Intune.

  **Řešení**: Pokud chcete získat další informace, povolte další protokolování:
  1. Otevřete Prohlížeč událostí, klikněte na tlačítko **Zobrazit**, ujistěte se, že je zaškrtnuta možnost **Zobrazit protokoly o analýze a ladění** .
  2. Přejděte do části **protokoly aplikací a služeb**  >  **Microsoft**  >  **Windows**  >  **CAPI2**  >  **provoz**, klikněte pravým tlačítkem na **operační**a pak klikněte na **Povolit protokol**.
  3. Jakmile je povoleno protokolování CAPI2, reprodukování problému a Projděte si protokol událostí, abyste mohli problém vyřešit.

- **Příčina 3**: oprávnění služby IIS v **CertificateRegistrationSvc** má povolené **ověřování systému Windows** .

  **Řešení**: Povolte **anonymní ověřování** a zakažte **ověřování systému Windows**a pak restartujte server NDES.

  ![Oprávnění služby IIS](../protect/media/troubleshoot-scep-certificate-device-to-ndes/iis-permissions.png)

- **Příčina 4**: vypršela platnost certifikátu modulu NDESPolicy.

  Protokol CAPI2 (viz řešení příčiny 2) zobrazí chyby související s certifikátem, na který odkazuje "HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Cryptography\MSCEP\Modules\NDESPolicy\NDESCertThumbprint" mimo období platnosti certifikátu.

  **Řešení**: Aktualizujte odkaz pomocí kryptografického otisku platného certifikátu.
  1. Identifikujte náhradní certifikát:
     - Obnovit existující certifikát
     - Vyberte jiný certifikát s podobným vlastnosti (předmět, rozšířené použití klíče, typ a délka atd.).
     - Registrace nového certifikátu
  2. Exportujte `NDESPolicy` klíč registru pro zálohování aktuálních hodnot.
  3. Nahraďte data `NDESCertThumbprint` hodnoty registru kryptografickým otiskem nového certifikátu, odeberete všechny prázdné znaky a text převede na malá písmena.
  4. Restartujte fondy aplikací NDES služby IIS nebo je spusťte `iisreset` z příkazového řádku se zvýšenými oprávněními.

#### <a name="gatewaytimeout"></a>GatewayTimeout

Když přejdete na adresu URL serveru SCEP, zobrazí se následující chyba:

![Chyba Gatewaytimeout](../protect/media/troubleshoot-scep-certificate-device-to-ndes/gateway-timeout.png)

- **Příčina**: Služba **Microsoft AAD Application proxy Connector** není spuštěná.

  **Řešení**: Spusťte **Services. msc**a potom se ujistěte, že je spuštěná služba **Microsoft AAD Application proxy Connector** a že **Typ spuštění** je nastaven na hodnotu **automaticky**.

#### <a name="http-414-request-uri-too-long"></a>Požadavek HTTP 414 – identifikátor URI je příliš dlouhý.

Když přejdete na adresu URL serveru SCEP, zobrazí se následující chyba:`HTTP 414 Request-URI Too Long`

- **Příčina**: filtrování požadavků služby IIS není nakonfigurováno pro podporu dlouhých adres URL (dotazů), které služba NDES obdrží. Tato podpora se konfiguruje při [konfiguraci služby NDES](certificates-scep-configure.md#configure-the-ndes-service) pro použití s infrastrukturou pro SCEP.

- **Řešení**: Nakonfigurujte podporu dlouhých adres URL.

  1. Na serveru NDES otevřete Správce služby IIS, vyberte **výchozí webový server**  >  **filtrování požadavků**  >  **Upravit nastavení funkce** a otevřete stránku **Upravit nastavení filtrování požadavků** .

  2. Nakonfigurujte tahle nastavení:
     - **Maximální délka adresy URL (bajty)** = 65534
     - **Maximální délka řetězce dotazu (bajty)** = 65534

  3. Výběrem **OK** tuto konfiguraci uložte a zavřete Správce služby IIS.

  4. Ověřte tuto konfiguraci tak, že vyhledáte následující klíč registru a ověříte tak, že má uvedené hodnoty:

     HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HTTP\Parameters

     Následující hodnoty jsou nastavené jako položky DWORD:
     - Název: **MaxFieldLength**, s desetinnou hodnotou **65534**
     - Název: **MaxRequestBytes**, s desetinnou hodnotou **65534**

  5. Restartujte server NDES.

#### <a name="this-page-cant-be-displayed"></a>Tuto stránku nejde zobrazit.

Máte nakonfigurovanou službu Azure Proxy aplikací služby AD. Když přejdete na adresu URL serveru SCEP, zobrazí se následující chyba:

`This page can't be displayed`

- **Příčina**: k tomuto problému dochází v případě, že externí adresa URL SCEP není v konfiguraci proxy aplikace správná. Příkladem této adresy URL je `https://contoso.com/certsrv/mscep/mscep.dll` .

  **Řešení**: použijte výchozí doménu *yourtenant.msappproxy.NET* pro externí adresu URL SCEP v konfiguraci proxy aplikace.

#### <a name="500---internal-server-error"></a><a name="internal-server-error"></a>500 – interní chyba serveru

Když přejdete na adresu URL serveru SCEP, zobrazí se následující chyba:

![500 – interní chyba serveru](../protect/media/troubleshoot-scep-certificate-device-to-ndes/500-internal-server-error.png)

- **Příčina 1**: účet služby NDES je zamčený nebo jeho heslo vypršelo.

  **Řešení**: Odemkněte účet nebo resetujte heslo.

- **Příčina 2**: vypršela platnost certifikátů mscep-RA.

  **Řešení**: Pokud vypršela platnost certifikátů mscep-RA, nainstalujte znovu roli NDES, nebo požádejte o nové šifrování CEP a certifikáty agenta pro zápis k Exchangi (offline žádosti).

  Pokud chcete požádat o nové certifikáty, postupujte takto:

  1. V certifikační autoritě (CA) nebo vystavující certifikační autoritě otevřete šablony certifikátů MMC. Ujistěte se, že přihlášený uživatel a server NDES mají oprávnění **ke čtení** a **zápisu** pro šablony certifikátů CEP Encryption a Agent pro zápis systému Exchange (žádost offline).

  2. Ověřte certifikáty s vypršenou platností na serveru NDES a zkopírujte informace o **subjektu** z certifikátu.

  3. Otevřete modul snap-in Certifikáty konzoly MMC pro **účet počítače**.

  4. Rozbalte **osobní**, klikněte pravým tlačítkem na **certifikáty**a pak vyberte **všechny úkoly**  >  **požádat o nový certifikát**.

  5. Na stránce **Vyžádat certifikát** vyberte **šifrování CEP**a pak klikněte na **Další informace, které se vyžadují k registraci tohoto certifikátu. Kliknutím sem můžete nakonfigurovat nastavení**.

     ![Vybrat šifrování CEP](../protect/media/troubleshoot-scep-certificate-device-to-ndes/select-scep-encryption.png)

  6. V části **Vlastnosti certifikátu**klikněte na kartu **Předmět** , vyplňte **název subjektu** informacemi, které jste shromáždili v kroku 2, klikněte na tlačítko **Přidat**a potom klikněte na tlačítko **OK**.

  7. Dokončete zápis certifikátu.

  8. Otevřete modul snap-in Certifikáty konzoly MMC pro **svůj uživatelský účet**.

     Když se zaregistrujete k certifikátu agenta zápisu Exchange (offline žádosti), musí se provést v kontextu uživatele. Vzhledem k tomu, že **typ subjektu** této šablony certifikátu je nastaven na hodnotu **uživatel**.

  9. Rozbalte **osobní**, klikněte pravým tlačítkem na **certifikáty**a pak vyberte **všechny úkoly**  >  **požádat o nový certifikát**.

  10. Na stránce **Vyžádat certifikát** vyberte možnost **Agent pro zápis systému Exchange (žádost v režimu offline)** a pak klikněte na tlačítko **Další informace, které se vyžadují k registraci tohoto certifikátu. Kliknutím sem můžete nakonfigurovat nastavení**.

      ![Vybrat agenta zápisu systému Exchange](../protect/media/troubleshoot-scep-certificate-device-to-ndes/select-exchange-enrollment-agent.png)

  11. V části **Vlastnosti certifikátu**klikněte na kartu **subjekt** , vyplňte **název subjektu** informacemi, které jste shromáždili v kroku 2, klikněte na tlačítko **Přidat**.

      ![Vlastnosti certifikátu](../protect/media/troubleshoot-scep-certificate-device-to-ndes/certificate-properties.png)

      Vyberte kartu **privátní klíč** , vyberte možnost **Označit privátní klíč jako exportovatelný**a pak klikněte na **OK**.

      ![Privátní klíč](../protect/media/troubleshoot-scep-certificate-device-to-ndes/private-key.png)

  12. Dokončete zápis certifikátu.

  13. Exportujte certifikát agenta zápisu serveru Exchange (offline žádosti) z úložiště certifikátů aktuálního uživatele. V Průvodci exportem certifikátu vyberte **Ano, exportovat soukromý klíč**.

  14. Importujte certifikát do úložiště certifikátů místního počítače.

  15. V konzole MMC certifikáty proveďte u každého nového certifikátu následující akci:

      Klikněte pravým tlačítkem na certifikát, klikněte na **všechny úlohy**  >  **spravovat soukromé klíče**a přidejte oprávnění **číst** k účtu služby NDES.

  16. Spusťte příkaz **iisreset** a restartujte službu IIS.

## <a name="next-steps"></a>Další kroky

Pokud zařízení úspěšně dosáhne serveru NDES, aby mohl předložit žádost o certifikát, je dalším krokem kontrola [modulu zásad konektorů certifikátů Intune](troubleshoot-scep-certificate-ndes-policy-module.md).
