---
title: Řešení potíží s modulem zásad Microsoft Intune Certificate Connector | Microsoft Docs
description: Řešení potíží s operací modulu NDES Policy, když modul zpracovává žádost o certifikát při nasazení certifikátů s Intune pomocí profilů certifikátů SCEP
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
ms.openlocfilehash: f58723be1a3fed09173a20a585077aef72e0c8f0
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079106"
---
# <a name="troubleshoot-the-ndes-policy-module-in-microsoft-intune"></a>Řešení potíží s modulem NDES Policy v Microsoft Intune

Informace v tomto článku vám pomůžou ověřit činnost modulu zásad služby zápisu síťových zařízení (NDES), který se instaluje s Microsoft Intune Certificate Connector. Když NDES obdrží žádost o certifikát, přepošle požadavek modulu zásad, který ověří požadavek platný pro zařízení. Po ověření kontaktuje NDES certifikační autoritu (CA), aby vyžádala certifikát jménem zařízení.

Tento článek se týká obou kroků a krok 4 pro [pracovní postup komunikace SCEP](troubleshoot-scep-certificate-profiles.md).

## <a name="ndes-communication-to-the-policy-module"></a>Komunikace NDES s modulem zásad

Po přijetí žádosti o certifikát ze zařízení Služba NDES ověří tuto žádost s Intune prostřednictvím modulu zásad, který se instaluje s Microsoft Intune Certificate Connector. Tyto položky odkazují na *bod registrace certifikátu*.

**Položky protokolu indikující úspěch**:

Pokud chcete potvrdit, že se žádost o ověření odešle do modulu, vyhledejte záznam, který se podobá následujícím příkladům v protokolech na serveru NDES:

- **Protokoly služby IIS**:

  ```
  fe80::f53d:89b8:c3e8:5fec%13 POST /CertificateRegistrationSvc/Certificate/VerifyRequest - 443 - 
  fe80::f53d:89b8:c3e8:5fec%13 NDES_Plugin - 201 0 0 341 875
  ```

- **Protokol souboru NDESPlugin**:

  ```
  Calling VerifyRequest ...  
  Sending request to certificate registration point.
  ```

  Následující příklad indikuje úspěšné ověření žádosti o výzvu zařízení a Služba NDES se teď může připojit k certifikační autoritě:

  ```
  Verify challenge returns true
  Exiting VerifyRequest with 0x0
  ```

- **CertificateRegistrationPoint. svclog**:

  `Validation Phase 1 finished with status True.`  
  `Validation Phase 3 finished with status True.`  
  `VerifyRequest Finished with status True`


**Pokud nejsou dostupné indikátory úspěšnosti**:

Pokud tyto položky nenajdete, začněte tím, že si Projděte pokyny k řešení potíží s [komunikací serveru NDES](troubleshoot-scep-certificate-device-to-ndes.md#troubleshoot-common-errors).

Pokud informace v tomto článku neumožňují vyřešit problém, jsou zde uvedené další položky, které mohou indikovat problémy.

### <a name="ndespluginlog-contains-an-error-12175"></a>Souboru NDESPlugin. log obsahuje chybu 12175

V případě, že protokol obsahuje chybu 12175 podobnou následující, mohlo by se jednat o problém s certifikátem SSL:

```
WINHTTP_CALLBACK_STATUS_FLAG_CERT_CN_INVALID
Failed to send http request /CertificateRegistrationSvc/Certificate/VerifyRequest. Error 12175
```

Moderní prohlížeče a prohlížeče na mobilních zařízeních ignorují *běžný název* certifikátu SSL, pokud jsou k dispozici *alternativní názvy předmětu* .

**Řešení**: vydejte certifikát SSL webového serveru s následujícími atributy pro *běžný* název a *alternativní název předmětu*a pak ho NAVAŽTE na port 443 ve službě IIS:

  - **Název subjektu**  
    CN = název externího serveru
  - **Alternativní název subjektu**  
     Název = název externího serveru  
     Název DNS = interní název serveru

### <a name="ndespluginlog-contains-an-error-403--forbidden-access-is-denied"></a>Souboru NDESPlugin. log obsahuje chybu 403 – zakázáno: přístup byl odepřen.

Pokud následující protokoly obsahují chybu 403, která je podobná následujícímu certifikátu, může být klientský certifikát nedůvěryhodný nebo neplatný:

**Souboru NDESPlugin. log**:

```
Sending request to certificate registration point.
Verify challenge returns <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd"> <html xmlns="http://www.w3.org/1999/xhtml"> <head><meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1"/>
<title>403 - Forbidden: Access is denied.</title>
```

**Protokol IIS**:

```
POST /CertificateRegistrationSvc/Certificate/VerifyRequest - 443 -<IP_address>
NDES_Plugin - 403 16 2148204809 453  
```

K tomuto problému dochází, pokud se v úložišti certifikátů důvěryhodných kořenových certifikačních autorit serveru NDES vyskytují certifikáty zprostředkující certifikační autority.

Pokud je certifikát stejný jako *vydaný* a *vydaný* pro hodnoty, jedná se o kořenový certifikát. V opačném případě se jedná o zprostředkující certifikát.

**Řešení**: Pokud chcete problém vyřešit, identifikujte a odeberte certifikáty zprostředkující certifikační autority z úložiště certifikátů důvěryhodných kořenových certifikačních autorit.

### <a name="ndespluginlog-indicates-the-challenge-returns-false"></a>Souboru NDESPlugin. log znamená, že výzva vrátí hodnotu false.

Pokud výsledek výzvy vrátí **hodnotu false**, vyhledejte chyby v *CertificateRegistrationPoint. svclog* . Například se může zobrazit chyba "podpisový certifikát se nepodařilo načíst", který se podobá následujícímu záznamu:

```
Signing certificate could not be retrieved. System.Security.Cryptography.CryptographicException: m_safeCertContext is an invalid handle. at System.Security.Cryptography.X509Certificates.X509Certificate.ThrowIfContextInvalid() at System.Security.Cryptography.X509Certificates.X509Certificate.GetCertHashString() at Microsoft.ConfigurationManager.CertRegPoint.CRPCertificate.RetrieveSigningCert(String certThumbprint
```

**Řešení**: na serveru, na kterém je nainstalovaný konektor, otevřete Editor registru, vyhledejte klíč `HKLM\SOFTWARE\Microsoft\MicrosoftIntune\NDESConnector` registru a zkontrolujte, jestli hodnota SigningCertificate existuje.

Pokud tato hodnota neexistuje, restartujte službu Intune Connector v Services. msc a potom zkontrolujte, jestli se hodnota objeví v registru. Pokud hodnota stále chybí, často se jedná o problémy s připojením k síti mezi serverem, který je součástí služby NDES a Intune.

## <a name="ndes-passes-the-request-to-issue-the-certificate"></a>NDES předá požadavek na vydání certifikátu.

Po úspěšném ověření bodem registrace certifikátu (modul zásad) Služba NDES předá žádost o certifikát certifikační autoritě jménem zařízení.

**Položky protokolu indikující úspěch**:

- **Protokol souboru NDESPlugin**:

  ```
  Verify challenge returns true
  Exiting VerifyRequest with 0x0
  ```

- **Protokoly služby IIS**:

  ```
  fe80::f53d:89b8:c3e8:5fec%13 GET /certsrv/mscep/mscep.dll/pkiclient.exe ... 80 - 
  fe80::f53d:89b8:c3e8:5fec%13 Mozilla/4.0+(compatible;+Win32;+NDES+client) - 200 0 0 2713 1296
  ```

- **CertificateRegistrationPoint. svclog**:

  `Validation Phase 1 finished with status True.`  
  `Validation Phase 3 finished with status True.`  
  `VerifyRequest Finished with status True`

**Pokud nejsou dostupné indikátory úspěšnosti**:

Pokud nevidíte položky, které indikují úspěch, postupujte podle těchto kroků:

1. Vyhledejte problémy, které jsou protokolovány v *CertificateRegistrationPoint. svclog* , když bod registrace certifikátu ověřuje výzvu. Vyhledejte položky mezi následujícími řádky:

   - VerifyRequest se spustil.
   - VerifyRequest se dokončilo se stavem false.

2. V certifikační autoritě otevřete konzolu MMC Certifikační autorita a vyberte **neúspěšné žádosti** , aby se vyhledaly chyby, které vám pomůžou identifikovat problém. Následující obrázek je příkladem:

   ![Příklad neúspěšné žádosti](../protect/media/troubleshoot-scep-certificate-ndes-policy-module/failed-requests.png)

3. Zkontrolujte chyby v protokolu událostí aplikace v certifikační autoritě. Obvykle můžete zobrazit chyby, které odpovídají čemu v **neúspěšných žádostech** z předchozího kroku. Následující obrázek je příkladem:

   ![Kontrola protokolu aplikace](../protect/media/troubleshoot-scep-certificate-ndes-policy-module/application-log-errors.png)

## <a name="next-steps"></a>Další kroky

Pokud modul zásad NDES žádost ověří a požadavek se předá certifikační autoritě, je dalším krokem kontrola [doručování certifikátů do zařízení](troubleshoot-scep-certificate-delivery.md).
