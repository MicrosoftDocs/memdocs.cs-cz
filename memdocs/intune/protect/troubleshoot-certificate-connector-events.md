---
title: Řešení potíží s Microsoft Intune Certificate Connectoru a ID událostí | Microsoft Docs
titleSuffix: Microsoft Intune
description: Poradce při potížích s Microsoft Intune Certificate Connectoru najdete v popisu událostí a popisech a v diagnostických kódech pro službu Intune Connector.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/01/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 592b42ca5f21cd68eaad01acf9895f7e5f4b5c73
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079157"
---
# <a name="intune-certificate-connector-events-and-diagnostic-codes"></a>Události a diagnostické kódy Intune Certificate Connectoru

Služba Intune Connector od verze 6.1806.x.x zaznamenává události do **Prohlížeče událostí** (**Protokoly aplikací a služeb** > **Microsoft Intune Connector**). Tyto události vám můžou pomoct při řešení možných problémů v konfiguraci konektoru Intune. Tyto události zaznamenávají úspěšné a neúspěšné operace a obsahují také diagnostické kódy se zprávami, které můžou správci IT usnadnit řešení problémů.

> [!TIP]  
> Informace o řešení problémů a ověření nastavení konektoru Intune najdete v tématu [ukázky skriptů pro certifikační autoritu](https://aka.ms/intuneconnectorverificationscript).

## <a name="event-ids-and-descriptions"></a>ID událostí a jejich popisy

| ID události      | Název události    | Popis události | Související diagnostické kódy |
| ------------- | ------------- | -------------     | -------------            |
| 10010 | StartedConnectorService  | Služba konektoru se spustila. | 0x00000000, 0x0FFFFFFF |
| 10020 | StoppedConnectorService  | Služba konektoru se zastavila. | 0x00000000, 0x0FFFFFFF |
| 10100 | CertificateRenewal_Success  | Certifikát registrace konektoru se úspěšně obnovil. | 0x00000000, 0x0FFFFFFF |
| 10102 | CertificateRenewal_Failure  | Certifikát registrace konektoru se nepodařilo obnovit. Přeinstalujte konektor. | 0x00000000, 0x00000405, 0x0FFFFFFF |
| 10302 | RetrieveCertificate_Error  | Certifikát registrace konektoru se nepodařilo načíst z registru. V podrobnostech události zkontrolujte kryptografický otisk certifikátu, který se vztahuje k této události. | 0x00000000, 0x00000404, 0x0FFFFFFF |
| 10301 | RetrieveCertificate_Warning  | V podrobnostech události zkontrolujte diagnostické informace. | 0x00000000, 0x00000403, 0x0FFFFFFF |
| 20100 | PkcsCertIssue_Success  | Certifikát PKCS se úspěšně vystavil. V podrobnostech události zkontrolujte ID zařízení, ID uživatele, název certifikační autority, název šablony certifikátu a kryptografický otisk certifikátu, které se vztahují k této události. | 0x00000000, 0x0FFFFFFF |
| 20102 | PkcsCertIssue_Failure  | Certifikát PKCS se nepodařilo vystavit. V podrobnostech události zkontrolujte ID zařízení, ID uživatele, název certifikační autority, název šablony certifikátu a kryptografický otisk certifikátu, které se vztahují k této události. | 0x00000000, 0x00000400, 0x00000401, 0x0FFFFFFF |
| 20200 | RevokeCert_Success  | Certifikát se úspěšně odvolal. V podrobnostech události zkontrolujte ID zařízení, ID uživatele, název certifikační autority a sériové číslo certifikátu, které se vztahují k této události. | 0x00000000, 0x0FFFFFFF |
| 20202 | RevokeCert_Failure | Certifikát se nepovedlo odvolat. V podrobnostech události zkontrolujte ID zařízení, ID uživatele, název certifikační autority a sériové číslo certifikátu, které se vztahují k této události. Další informace najdete v protokolech SVC NDES.   | 0x00000000, 0x00000402, 0x0FFFFFFF |
| 20300 | Upload_Success | Žádost o certifikát nebo data odvolání se úspěšně nahrály. V podrobnostech události zkontrolujte podrobnosti o nahrání. | 0x00000000, 0x0FFFFFFF |
| 20302 | Upload_Failure | Nepovedlo se nahrát data žádosti nebo odvolání certifikátu. V podrobnostech události zkontrolujte stav nahrávání, abyste zjistili, kde došlo k chybě.| 0x00000000, 0x0FFFFFFF |
| 20400 | Download_Success | Žádost o podepsání certifikátu se úspěšně stáhla, stáhněte si klientský certifikát nebo odvolejte certifikát. V podrobnostech události zkontrolujte podrobnosti o stažení.  | 0x00000000, 0x0FFFFFFF |
| 20402 | Download_Failure | Žádost o podepsání certifikátu se nepodařilo stáhnout, stáhněte si klientský certifikát nebo odvolejte certifikát. V podrobnostech události zkontrolujte podrobnosti o stažení. | 0x00000000, 0x0FFFFFFF |
| 20500 | CRPVerifyMetric_Success  | Bod registrace certifikátu úspěšně dokončil ověřovací test klienta. | 0x00000000, 0x0FFFFFFF |
| 20501 | CRPVerifyMetric_Warning  | Bod registrace certifikátu se dokončil, ale žádost se zamítla. Další podrobnosti poskytne diagnostický kód a zpráva. | 0x00000000, 0x00000411, 0x0FFFFFFF |
| 20502 | CRPVerifyMetric_Failure  | Bodu registrace certifikátu se nepodařilo ověřovací test klienta úspěšně dokončit. Další podrobnosti poskytne diagnostický kód a zpráva. V podrobnostech zprávy o události vyhledejte ID zařízení, které se vztahuje k tomuto ověřovacímu testu. | 0x00000000, 0x00000408, 0x00000409, 0x00000410, 0x0FFFFFFF |
| 20600 | CRPNotifyMetric_Success  | Bod registrace certifikátu úspěšně dokončil proces oznamování a odeslal certifikát do klientského zařízení. | 0x00000000, 0x0FFFFFFF |
| 20602 | CRPNotifyMetric_Failure  | Bodu registrace certifikátu se nepodařilo dokončit proces oznamování. V podrobnostech zprávy o události vyhledejte informace o této žádosti. Ověřte připojení mezi serverem NDES a certifikační autoritou. | 0x00000000, 0x0FFFFFFF |

## <a name="diagnostic-codes"></a>Diagnostické kódy

| Diagnostický kód | Název diagnostiky | Diagnostická zpráva |
| -------------   | -------------   | -------------      |
| 0x00000000 | Úspěch  | Úspěch |
| 0x00000400 | PKCS_Issue_CA_Unavailable  | Certifikační autorita není platná nebo není dostupná. Ověřte, že je certifikační autorita dostupná a že s ní váš server může komunikovat. |
| 0x00000401 | Symantec_ClientAuthCertNotFound  | Certifikát ověřování klienta Symantec se v místním úložišti certifikátů nenašel. Další informace najdete v článku o [instalaci certifikátu RA Symantec](certificates-digicert-configure.md#install-the-digicert-ra-certificate).  |
| 0x00000402 | RevokeCert_AccessDenied  | Zadaný účet nemá oprávnění k odvolání certifikátu z certifikační autority. V podrobnostech zprávy o události vyhledejte pole Název certifikační autority, abyste zjistili vydávající certifikační autoritu.  |
| 0x00000403 | CertThumbprint_NotFound  | Certifikát odpovídající vašemu vstupu se nepodařilo najít. Zaregistrujte si Certificate Connector a zkuste to znovu. |
| 0x00000404 | Certificate_NotFound  | Certifikát odpovídající zadanému vstupu se nepodařilo najít. Zaregistrujte si znovu Certificate Connector a zkuste to znovu. |
| 0x00000405 | Certificate_Expired  | Platnost certifikátu vypršela. Zaregistrujte si znovu Certificate Connector, aby se certifikát obnovil, a zkuste to znovu. |
| 0x00000408 | CRPSCEPCert_NotFound  | Certifikát šifrování CRP se nepodařilo najít. Ověřte správné nastavení NDES a konektoru Intune. |
| 0x00000409 | CRPSCEPSigningCert_NotFound  | Podpisový certifikát se nepodařilo načíst. Ověřte, že je služba konektoru Intune správně nakonfigurovaná a že je spuštěná. Ověřte také, že se úspěšně dokončily události stažení certifikátu. |
| 0x00000410 | CRPSCEPDeserialize_Failed  | Žádost ověřovacího testu SCEP se nepodařilo deserializovat. Ověřte správné nastavení NDES a konektoru Intune. |
| 0x00000411 | CRPSCEPChallenge_Expired  | Žádost se zamítla kvůli vypršení platnosti ověřovacího testu certifikátu. Po načtení nového ověřovacího testu ze serveru pro správu může klientské zařízení pokus opakovat. |
| 0x0FFFFFFFF | Unknown_Error  | Vaši žádost nemůžeme dokončit, protože došlo k chybě na straně serveru. Zkuste to prosím znovu. |


## <a name="next-steps"></a>Další kroky
Pokud potřebujete další pomoc, použijte [Poradce při potížích s nasazením profilu certifikátu SCEP v Microsoft Intune](https://support.microsoft.com/help/4457481/troubleshooting-scep-certificate-profile-deployment-in-intune) příručce.
