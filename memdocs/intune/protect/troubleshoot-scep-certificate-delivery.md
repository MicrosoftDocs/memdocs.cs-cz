---
title: Řešení potíží s doručováním certifikátů SCEP pro Intune | Microsoft Docs
description: Řešení potíží s doručováním certifikátu do zařízení z certifikační autority při použití profilů certifikátů SCEP s Intune k nasazení certifikátů.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/30/2020
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
ms.openlocfilehash: 401bc2abe1be925f78436ff6557896ed51e37cb1
ms.sourcegitcommit: 42a4a4454e56fa681f0ad39f5e585492dfbad286
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/03/2020
ms.locfileid: "84330895"
---
# <a name="troubleshoot-the-delivery-of-certificates-provisioned-by-scep-to-devices-in-microsoft-intune"></a>Řešení potíží s doručováním certifikátů zajištěných pomocí protokolu SCEP do zařízení v Microsoft Intune

Informace v tomto článku vám pomůžou prozkoumat doručování certifikátů do zařízení při použití Simple Certificate Enrollment Protocol (SCEP) ke zřízení certifikátů v Intune. Poté, co server služby zápisu síťových zařízení (NDES) obdrží požadovaný certifikát pro zařízení od certifikační autority (CA), tento certifikát předá do zařízení.

Tento článek se týká kroku 5 [pracovního postupu komunikace SCEP](troubleshoot-scep-certificate-profiles.md); doručení certifikátu do zařízení, které odeslalo žádost o certifikát.

## <a name="review-the-certification-authority"></a>Kontrola certifikační autority

Pokud certifikační autorita vydala certifikát, zobrazí se v certifikační autoritě položka podobná následujícímu příkladu:

![Příklad vydaných certifikátů](../protect/media/troubleshoot-scep-certificate-delivery/certificate-authority.png)

## <a name="review-the-device"></a>Kontrola zařízení

### <a name="android"></a>Android

U zaregistrovaných zařízení Správce zařízení se zobrazí oznámení podobné následujícímu obrázku, který vás vyzve k instalaci certifikátu:

![Oznámení pro Android](../protect/media/troubleshoot-scep-certificate-delivery/android-notification.png)

Pro Android Enterprise nebo Samsung KNOX je instalace certifikátu automatická a tichá.

Pokud si chcete zobrazit nainstalovaný certifikát na Androidu, použijte aplikaci pro zobrazení certifikátů třetích stran.

Můžete si také prohlédnout [protokol OMADM zařízení](troubleshoot-scep-certificate-profiles.md#logs-for-android-devices). Vyhledat položky, které se podobají následujícímu protokolu, které jsou protokolovány při instalaci certifikátů:

**Kořenový certifikát**:

```
2018-02-27T04:50:52.1890000    INFO    Event     com.microsoft.omadm.platforms.android.certmgr.state.NativeRootCertInstallStateMachine     9595        9    Root cert '17…' state changed from CERT_INSTALL_REQUESTED to CERT_INSTALL_REQUESTED
2018-02-27T04:53:31.1300000    INFO    Event     com.microsoft.omadm.platforms.android.certmgr.state.NativeRootCertInstallStateMachine     9595        0    Root cert '17…' state changed from CERT_INSTALL_REQUESTED to CERT_INSTALLING
2018-02-27T04:53:32.0390000    INFO    Event     com.microsoft.omadm.platforms.android.certmgr.state.NativeRootCertInstallStateMachine     9595       14    Root cert '17…' state changed from CERT_INSTALLING to CERT_INSTALL_SUCCESS
```

**Certifikát zřízený pomocí protokolu SCEP**

```
2018-02-27T05:16:08.2500000    VERB    Event     com.microsoft.omadm.platforms.android.certmgr.CertificateEnrollmentManager    18327       10    There are 1 requests
2018-02-27T05:16:08.2500000    VERB    Event     com.microsoft.omadm.platforms.android.certmgr.CertificateEnrollmentManager    18327       10    Trying to enroll certificate request: ModelName=AC_51…%2FLogicalName_39907…;Hash=1677525787
2018-02-27T05:16:20.6150000    VERB    Event     org.jscep.transport.UrlConnectionGetTransport    18327       10    Sending GetCACert(ca) to https://<server>-contoso.msappproxy.net/certsrv/mscep/mscep.dll?operation=GetCACert&message=ca
2018-02-27T05:16:20.6530000    VERB    Event     org.jscep.transport.UrlConnectionGetTransport    18327       10    Received '200 OK' when sending GetCACert(ca) to https://<server>-contoso.msappproxy.net/certsrv/mscep/mscep.dll?operation=GetCACert&message=ca
2018-02-27T05:16:21.7460000    VERB    Event     org.jscep.transport.UrlConnectionGetTransport    18327       10    Sending GetCACaps(ca) to https://<server>-contoso.msappproxy.net/certsrv/mscep/mscep.dll?operation=GetCACaps&message=ca
2018-02-27T05:16:21.7890000    VERB    Event     org.jscep.transport.UrlConnectionGetTransport    18327       10    Received '200 OK' when sending GetCACaps(ca) to https://<server>-contoso.msappproxy.net/certsrv/mscep/mscep.dll?operation=GetCACaps&message=ca
2018-02-27T05:16:28.0340000    VERB    Event     org.jscep.transaction.EnrollmentTransaction    18327       10    Response: org.jscep.message.CertRep@3150777b[failInfo=<null>,pkiStatus=SUCCESS,recipientNonce=Nonce [GUID],messageData=org.spongycastle.cms.CMSSignedData@27cc8998,messageType=CERT_REP,senderNonce=Nonce [GUID],transId=TRANSID]
2018-02-27T05:16:28.2440000    INFO    Event     com.microsoft.omadm.platforms.android.certmgr.state.NativeScepCertInstallStateMachine    18327       10    SCEP cert 'ModelName=AC_51…%2FLogicalName_39907…;Hash=1677525787' state changed from CERT_ENROLLED to CERT_INSTALL_REQUESTED
2018-02-27T05:18:44.9820000    INFO    Event     com.microsoft.omadm.platforms.android.certmgr.state.NativeScepCertInstallStateMachine    18327        0    SCEP cert 'ModelName=AC_51…%2FLogicalName_39907…;Hash=1677525787' state changed from CERT_INSTALL_REQUESTED to CERT_INSTALLING
2018-02-27T05:18:45.3460000    INFO    Event     com.microsoft.omadm.platforms.android.certmgr.state.NativeScepCertInstallStateMachine    18327       14    SCEP cert 'ModelName=AC_51…%2FLogicalName_39907…;Hash=1677525787' state changed from CERT_INSTALLING to CERT_ACCESS_REQUESTED
2018-02-27T05:20:15.3520000    INFO    Event     com.microsoft.omadm.platforms.android.certmgr.state.NativeScepCertInstallStateMachine    18327       21    SCEP cert 'ModelName=AC_51…%2FLogicalName_39907…;Hash=1677525787' state changed from CERT_ACCESS_REQUESTED to CERT_ACCESS_GRANTED
```

### <a name="iosipados"></a>iOS/iPadOS

V zařízení se systémem iOS/iPadOS nebo iPadOS můžete certifikát zobrazit pod profilem správy zařízení. Podrobné informace o nainstalovaných certifikátech najdete v tématu.

![certifikát iOS](../protect/media/troubleshoot-scep-certificate-delivery/ios-certificate.png)

Můžete také vyhledat položky, které se podobají následujícímu v [protokolu ladění iOS](troubleshoot-scep-certificate-profiles.md#logs-for-ios-and-ipados-devices):

```
Debug 18:30:53.691033 -0500 profiled Performing synchronous URL request: https://<server>-contoso.msappproxy.net/certsrv/mscep/mscep.dll?operation=GetCACert&message=SCEP%20Authority\  
Debug 18:30:54.640644 -0500 profiled Performing synchronous URL request: https://<server>-contoso.msappproxy.net/certsrv/mscep/mscep.dll?operation=GetCACaps&message=SCEP%20Authority\ 
Debug 18:30:55.487908 -0500 profiled Performing synchronous URL request: https://<server>-contoso.msappproxy.net/certsrv/mscep/mscep.dll?operation=PKIOperation&message=MIAGCSqGSIb3DQEHAqCAMIACAQExDzANBglghkgBZQMEAgMFADCABgkqhkiG9w0BBwGggCSABIIZfzCABgkqhkiG9w0BBwOggDCAAgEAMYIBgjCCAX4CAQAwZjBPMRUwEwYKCZImiZPyLGQBGRYFbG9jYWwxHDAaBgoJkiaJk/IsZAEZFgxmb3VydGhjb2ZmZWUxGDAWBgNVBAMTD0ZvdXJ0aENvZmZlZSBDQQITaAAAAAmaneVjEPlcTwAAAAAACTANBgkqhkiG9w0BAQEFAASCAQCqfsOYpuBToerQLkw/tl4tH9E+97TBTjGQN9NCjSgb78fF6edY0pNDU+PH4RB356wv3rfZi5IiNrVu5Od4k6uK4w0582ZM2n8NJFRY7KWSNHsmTIWlo/Vcr4laAtq5rw+CygaYcefptcaamkjdLj07e/Uk4KsetGo7ztPVjSEFwfRIfKv474dLDmPqp0ZwEWRQG 
Debug 18:30:57.285730 -0500 profiled Adding dependent Microsoft.Profiles.MDM to parent www.windowsintune.com.SCEP.ModelName=AC_51bad41f.../LogicalName_1892fe4c...;Hash=-912418295 in domain ManagedProfileToManagingProfile to system\ 
Default 18:30:57.320616 -0500 profiled Profile \'93www.windowsintune.com.SCEP.ModelName=AC_51bad41f.../LogicalName_1892fe4c...;Hash=-912418295\'94 installed.\ 
```

### <a name="windows"></a>Windows

Na zařízení se systémem Windows ověřte, zda byl certifikát dodán:

- Spusťte příkaz **eventvwr. msc** a otevřete Prohlížeč událostí. Přejít na **protokoly aplikací a služeb**  >  **Microsoft**  >  **Windows**  >  **DeviceManagement-Enterprise-Diagnostic-Provider**  >  **admin** a vyhledejte **událost 39**. Tato událost by měla mít obecný popis: **SCEP: certifikát byl úspěšně nainstalován.**

   ![Událost 39 v protokolu aplikace systému Windows](../protect/media/troubleshoot-scep-certificate-delivery/device-app-log.png)

Chcete-li zobrazit certifikát na zařízení, spusťte příkaz **certmgr. msc** a otevřete konzolu MMC a ověřte, zda jsou certifikáty root a SCEP nainstalovány na zařízení v osobním úložišti správně:

   1. V části **certifikáty (místní počítač)**  >  **Důvěryhodné kořenové certifikační autority**  >  **certifikátů**a ověřte, jestli je přítomen kořenový certifikát z vaší certifikační autority. Hodnoty pro *vystavení* a *vystavení* budou stejné.
   2. V modulu snap-in Certifikáty konzoly MMC klikněte na **Certifikáty – aktuální**  >  **osobní**  >  **certifikáty**uživatele a ověřte, že je přítomný požadovaný certifikát, který se *vystaví jako* stejný jako název certifikační autority.

## <a name="troubleshoot-failures"></a>Řešení chyb

### <a name="android"></a>Android

Pokud chcete tento krok vyřešit, přečtěte si chyby zaznamenané v protokolu OMA DM.

### <a name="iosipados"></a>iOS/iPadOS

Pokud chcete tento krok vyřešit, Projděte si chyby zaznamenané v protokolu ladění zařízení.

### <a name="windows"></a>Windows

Pokud chcete řešit problémy s certifikátem, který není v zařízení nainstalovaný, vyhledejte v protokolu událostí systému Windows chyby, které navrhují problémy:

- Na zařízení spusťte příkaz **eventvwr. msc** a otevřete Prohlížeč událostí a potom v části **protokoly aplikací a služeb**  >  **Microsoft**  >  **Windows**  >  **DeviceManagement-Enterprise-Diagnostic-Provider**  >  **admin**.

Chyby při doručování a instalaci certifikátu do zařízení obvykle souvisí s operacemi systému Windows a nikoli s Intune.

## <a name="next-steps"></a>Další kroky

Když se certifikát úspěšně nasadí do zařízení, ale Intune neohlásí úspěch, přečtěte si téma [ohlašování sestav do Intune](troubleshoot-scep-certificate-reporting.md) a řešení potíží s vytvářením sestav.
