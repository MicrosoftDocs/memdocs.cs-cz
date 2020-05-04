---
title: Řešení potíží při zřizování certifikátů pomocí profilů certifikátů SCEP Microsoft Intune | Microsoft Docs
description: Řešení potíží s používáním SCEP podle zařízení k vyžádání certifikátů, které se mají používat s Intune, včetně komunikace ze zařízení do služby NDES, NDES s certifikačními autoritami a z Intune Certificate Connectoru ke službě Intune.
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
ms.openlocfilehash: ed98ca328bdd196cd9dd7005f5e2d5ac75ff7511
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79328667"
---
# <a name="overview-for-troubleshooting-scep-certificate-profiles-with-microsoft-intune"></a>Přehled řešení potíží s profily certifikátů SCEP pomocí Microsoft Intune

Používání profilů certifikátů Simple Certificate Enrollment Protocol (SCEP) může být náročné na řešení potíží v Intune. Tento článek je přehled, který vám může pomáhat vyřešit problémy:

- Vysvětlení architektury a komunikačního toku procesu SCEP
- Pomáhá zúžit se na to, kde nějaký problém existuje v průběhu komunikace.
- Určení souborů protokolu klíčů, na které se odkazuje v dalších článcích pro řešení potíží s profily certifikátů

Informace v tomto článku a související články týkající se řešení potíží s certifikátem SCEP se vztahují na používání profilů certifikátů SCEP se zařízeními s Androidem, iOS/iPadem a Windows. Podobné informace pro macOS nejsou v tuto chvíli k dispozici.

Řešení potíží se službou zápisu síťových zařízení (NDES) najdete v následujících článcích na support.microsoft.com:

- [Ověření konfigurace NDES v místním prostředí pro certifikáty SCEP v Intune](https://support.microsoft.com/help/4490130/ndes-configuration-on-premises-for-scep-certificates-in-intune)
- [Řešení potíží s konfigurací NDES pro použití s Microsoft Intune profily certifikátů]( https://support.microsoft.com/help/4459540/troubleshoot-ndes-configuration-for-use-with-intune)

Než budete pokračovat, ujistěte se, že splňujete [požadavky na používání profilů certifikátů SCEP](certificates-scep-configure.md#prerequisites-for-using-scep-for-certificates), včetně nasazení kořenového certifikátu přes profil důvěryhodného certifikátu.

## <a name="scep-communication-flow-overview"></a>Přehled komunikačního toku SCEP

Následující obrázek ukazuje základní přehled procesu komunikace SCEP v Intune.

![Tok profilu certifikátu SCEP](../protect/media/troubleshoot-scep-certificate-profiles/scep-certificate-profile-flow.png)

1. [Nasaďte profil certifikátu SCEP](troubleshoot-scep-certificate-profile-deployment.md). Intune vygeneruje řetězec výzvy, který vyžaduje konkrétního uživatele, účel certifikátu a typ certifikátu.

2. [Komunikace zařízení se serverem NDES](troubleshoot-scep-certificate-device-to-ndes.md). Zařízení používá identifikátor URI pro NDES z profilu ke kontaktování serveru NDES, aby mohl zobrazit výzvu.

3. [Komunikace mezi NDES a modulem zásad](troubleshoot-scep-certificate-ndes-policy-module.md). Služba NDES předá výzvu modulu zásad Certificate Connectoru Intune na serveru, který žádost ověří.

4. [NDES pro certifikační autoritu](troubleshoot-scep-certificate-ndes-policy-module.md). NDES dodává platné žádosti o vydání certifikátu certifikační autoritě (CA).

5. [Doručování certifikátů do zařízení](troubleshoot-scep-certificate-delivery.md). Certifikát se doručí do zařízení.

6. [Vytváření sestav nasazení do Intune](troubleshoot-scep-certificate-reporting.md) Intune Certificate Connector hlásí událost vystavení certifikátu do Intune.

## <a name="log-files"></a>Soubory protokolů

Pokud chcete identifikovat problémy pro pracovní postup pro komunikaci a zřizování certifikátů, Projděte si soubory protokolů z serverové infrastruktury i ze zařízení. Pozdější oddíly pro řešení potíží s profily certifikátů SCEP odkazují na soubory protokolu, na které se odkazuje v této části.

- [Protokoly infrastruktury a serveru](#logs-for-on-premises-infrastructure)

Protokoly zařízení závisí na platformě zařízení:  

- [iOS a iPadOS](#logs-for-ios-and-ipados-devices)
- [Android](#logs-for-android-devices)
- [Windows](#logs-for-windows-devices)

### <a name="logs-for-on-premises-infrastructure"></a>Protokoly pro místní infrastrukturu
  
Místní infrastruktura, která podporuje použití profilů certifikátů SCEP pro nasazení certifikátů, zahrnuje Microsoft Intune Certificate Connector, NDES, která běží na Windows serveru a certifikační autoritě.

Soubory protokolu pro tyto role zahrnují Prohlížeč událostí Windows, konzolu certifikátů a různé soubory protokolů, které jsou specifické pro Certificate Connector, NDES nebo jiné role a operace Intune, které jsou součástí místní infrastruktury.

Následující seznam obsahuje protokoly nebo konzoly, na které se odkazuje v následujících článcích o řešení potíží s protokolem SCEP. 

- **NDESConnector_date_time. svclog**:

  Tento protokol zobrazuje komunikaci z Microsoft Intune Certificate Connector do cloudové služby Intune. K zobrazení tohoto souboru protokolu můžete použít [Nástroj Prohlížeč trasování služby](https://docs.microsoft.com/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) .

  Související klíč registru: *HKLM\SW\Microsoft\MicrosoftIntune\NDESConnector\ConnectionStatus*

  Umístění: na serveru, který je hostitelem NDES, na adrese *% program_files% \ Microsoft intune\ndesconnectorsvc\logs\logs*

- **CertificateRegistrationPoint_date_time. svclog**:

  Tento protokol zobrazuje modul zásad NDES, který přijímá a ověřuje žádosti o certifikát. K zobrazení tohoto souboru protokolu můžete použít [Nástroj Prohlížeč trasování služby](https://docs.microsoft.com/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) .

  Umístění: na serveru, který je hostitelem NDES, na adrese *% program_files% \ Microsoft intune\ndesconnectorsvc\logs\logs*

- **Souboru NDESPlugin. log**:

  Tento protokol zobrazuje předávání žádostí o certifikát na bod registrace certifikátu a výsledné ověřování těchto žádostí.

  Umístění: na serveru, který je hostitelem NDES, na adrese *% program_files% \ Microsoft Intune\NDESPolicyModule\logs*

- **Protokoly služby IIS**:

  Protokoly služby IIS zobrazují žádosti o certifikát z mobilních zařízení vstupujících do NDES.

  Umístění: na serveru, který je hostitelem NDES na adrese *c:\inetpub\logs\LogFiles\W3SVC1*

- **Protokol aplikace systému Windows**:

  Tento protokol je užitečný při zkoumání problémů služby IIS, jako je například fond aplikací SCEP.

  Umístění: na serveru, který je hostitelem NDES: Spusťte příkaz **eventvwr. msc** a otevřete Windows Prohlížeč událostí




### <a name="logs-for-android-devices"></a>Protokoly pro zařízení s Androidem

U zařízení se systémem Android použijte soubor protokolu aplikace pro **Android portál společnosti** **OMADM. log**. Než shromáždíte a zkontrolujete protokoly, povolte zajistěte, aby bylo zapnuté [podrobné protokolování](../user-help/use-verbose-logging-to-help-your-it-administrator-fix-device-issues-android.md) , a pak problém reprodukovánte.

Postup shromáždění protokolu OMADM. log ze zařízení najdete v tématu [nahrání a e-mailové protokoly pomocí kabelu USB](../user-help/send-logs-to-your-it-admin-using-cable-android.md).

Můžete také [nahrávat a e-mailem protokoly](../user-help/send-logs-to-your-it-admin-by-email-android.md#upload-and-email-logs-from-microsoft-intune-app) pro podporu.

### <a name="logs-for-ios-and-ipados-devices"></a>Protokoly pro zařízení s iOS a iPadOS

U zařízení se systémem iOS nebo iPadOS používáte protokoly ladění a **Xcode** , které běží na počítači Mac:

1. Připojte zařízení se systémem iOS/**iPadOS k počítači** Mac a potom v okně **aplikace** > otevřete konzolovou aplikaci. 

2. V části **Akce**vyberte **Zahrnout informační zprávy** a **zahrnout zprávy ladění**.

   ![Výběr možností protokolu](../protect/media/troubleshoot-scep-certificate-profiles/message-options.png)

3. Reprodukování problému a uložení protokolů do textového souboru:
   1. Vyberte **Upravit** > **Vybrat vše** , pokud chcete vybrat všechny zprávy na aktuální obrazovce a pak vybrat **Upravit** > **kopii** a zkopírovat zprávy do schránky. 
   2. Otevřete aplikaci TextEdit, vložte zkopírované protokoly do nového textového souboru a uložte soubor.


Protokol Portál společnosti pro zařízení s iOS a iPadOS neobsahuje informace o profilech certifikátů SCEP.

### <a name="logs-for-windows-devices"></a>Protokoly pro zařízení s Windows

U zařízení s Windows použijte protokoly událostí Windows k diagnostice problémů se správou registrace nebo zařízení u zařízení, která spravujete přes Intune.

Na zařízení otevřete **Prohlížeč událostí** > **aplikace a protokoly** > **služeb Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostics-Provider**

![Protokoly událostí Windows](../protect/media/troubleshoot-scep-certificate-profiles/windows-event-log.png)

## <a name="next-steps"></a>Další kroky

Kontrola [nasazení profilů certifikátů SCEP](troubleshoot-scep-certificate-profile-deployment.md) 
