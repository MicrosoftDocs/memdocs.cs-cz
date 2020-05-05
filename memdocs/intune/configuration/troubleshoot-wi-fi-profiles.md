---
title: Řešení potíží a kontrola protokolů profilů zařízení Wi-Fi v Microsoft Intune – Azure | Microsoft Docs
description: Pochopení a řešení potíží s profilem konfigurace zařízení Wi-Fi pro zařízení s Androidem, iOS/iPadOS a Windows v Microsoft Intune. Zkontrolujte protokoly a podívejte se na některé běžné problémy a možná řešení.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 40eaf6be1b5f6cdb0222fc5bd79e8e5a5b72a947
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078205"
---
# <a name="troubleshoot-wi-fi-device-configuration-profiles-in-microsoft-intune"></a>Řešení potíží s profily konfigurace zařízení Wi-Fi v Microsoft Intune

V Intune můžete vytvořit profily konfigurace zařízení, které zahrnují nastavení připojení pro vaši síť Wi-Fi. Pomocí těchto nastavení můžete k síti organizace připojit zařízení s Androidem, iOS/iPadOS a Windows.

Tento článek ukazuje, jak profil sítě Wi-Fi vypadá, když se na zařízeních úspěšně vztahuje. Obsahuje také informace protokolu, běžné problémy a další. Pomocí tohoto článku můžete pomoct s řešením vašich profilů sítě Wi-Fi.

Další informace o profilech sítě Wi-Fi v Intune najdete v tématu [Přidání a použití nastavení Wi-Fi na vašich zařízeních](wi-fi-settings-configure.md).

## <a name="before-you-begin"></a>Před zahájením

Příklady v tomto článku používají pro profily Intune ověřování pomocí certifikátu SCEP. Také předpokládá, že důvěryhodné kořenové a profily SCEP fungují na zařízení správně.

## <a name="android"></a>Android

V této části jsme při instalaci konfiguračních profilů na zařízení s Androidem provedli kroky koncového uživatele.

### <a name="end-user-experience-example"></a>Příklad činnosti koncového uživatele

V tomto scénáři se používá zařízení Nokia 6,1. Předtím, než se profil sítě Wi-Fi nainstaluje do zařízení, nainstalujte důvěryhodný kořenový certifikát a profily SCEP.

1. Koncovým uživatelům se zobrazí oznámení o instalaci profilu důvěryhodného kořenového certifikátu:

    > [!div class="mx-imgBorder"]
    > ![Ukázka Portál společnosti oznámení aplikace na Androidu pro instalaci profilu důvěryhodného kořenového certifikátu](./media/troubleshoot-wi-fi-profiles/android-end-user-company-portal-trusted-root.png)

2. Další oznámení vám vyzve k instalaci profilu certifikátu SCEP:

    > [!div class="mx-imgBorder"]
    > ![Ukázka Portál společnosti oznámení aplikace na Androidu pro instalaci profilu certifikátu SCEP](./media/troubleshoot-wi-fi-profiles/android-end-user-company-portal-scep-certificate.png)

    > [!TIP]
    > Pokud používáte zařízení se systémem Android spravovaná správcem zařízení, může být uvedeno více certifikátů. Při odvolání nebo odebrání profilu certifikátu zůstane certifikát na zařízení. V tomto scénáři vyberte nejnovější certifikát. Obvykle se jedná o poslední certifikát zobrazený v seznamu.
    >
    > K této situaci nedochází v zařízeních s Androidem Enterprise a Samsung KNOX. Další informace najdete v tématech [Správa zařízení s pracovním profilem Androidu](../enrollment/android-enterprise-overview.md) a [odebírání certifikátů SCEP a PKCS](../protect/remove-certificates.md#android-knox-devices).

3. V dalším kroku obdrží uživatelé oznámení o instalaci profilu sítě Wi-Fi:

    > [!div class="mx-imgBorder"]
    > ![Ukázka Portál společnosti oznámení aplikace na Androidu pro instalaci profilu certifikátu SCEP](./media/troubleshoot-wi-fi-profiles/android-end-user-install-wifi-profile.png)

4. Po dokončení se připojení Wi-Fi zobrazí jako uložená síť:

    > [!div class="mx-imgBorder"]
    > ![Připojení Wi-Fi ukazuje jako uloženou síť.](./media/troubleshoot-wi-fi-profiles/android-end-user-saved-networks.png)

### <a name="review-company-portal-app-logs"></a>Kontrola Portál společnosti protokolů aplikací

V Androidu soubor **Omadmlog. log** podrobně popisuje aktivity profilu Wi-Fi při instalaci do zařízení. Můžete mít až pět souborů protokolu Omadmlog. Nezapomeňte získat časové razítko poslední synchronizace, protože vám pomůže najít související položky protokolu.

V následujícím příkladu použijte [CMTrace](https://docs.microsoft.com/configmgr/core/support/cmtrace) ke čtení protokolů a vyhledejte "wifimgr":

> [!div class="mx-imgBorder"]
> ![Připojení Wi-Fi ukazuje jako uloženou síť.](./media/troubleshoot-wi-fi-profiles/android-cmtrace-filter-wifimgr.png)

Následující protokol zobrazuje výsledky hledání a zobrazuje profil sítě Wi-Fi byl úspěšně použit:

```log
2019-08-01T19:22:46.7340000    VERB    com.microsoft.omadm.platforms.android.wifimgr.WifiProfile    15118    04142    Starting to parse Wifi Profile XML with name '<profile ID>'.
2019-08-01T19:22:46.7490000    VERB    com.microsoft.omadm.platforms.android.wifimgr.OneX    15118    04142    Starting to parse OneX from Wifi XML.
2019-08-01T19:22:46.8100000    VERB    com.microsoft.omadm.platforms.android.wifimgr.OneX    15118    04142    Completed parsing OneX from Wifi XML.
2019-08-01T19:22:46.8209999    VERB    com.microsoft.omadm.platforms.android.wifimgr.WifiProfile    15118    04142    Completed parsing Wifi Profile XML with name '<profile ID>'.
2019-08-01T19:22:46.8240000    INFO    com.microsoft.omadm.utils.CertificateSelector    15118    04142    Selected ca certificate with alias: 'user:205xxxxx.0' and thumbprint '<thumbprint>'.
2019-08-01T19:22:47.0990000    VERB    com.microsoft.omadm.platforms.android.certmgr.CertificateChainBuilder    15118    04142    Complete certificate chain built with Complete certs.
2019-08-01T19:22:47.1010000    VERB    com.microsoft.omadm.utils.CertUtils    15118    04142    1 cert(s) matched criteria: User<ID>[i:<ID>,17CECEA1D337FAA7D167AD83A8CC7A8FCBF9xxxx;eku:1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2]
2019-08-01T19:22:47.1090000    VERB    com.microsoft.omadm.utils.CertUtils    15118    04142    0 cert(s) excluded by criteria:
2019-08-01T19:22:47.1110000    INFO    com.microsoft.omadm.utils.CertificateSelector    15118    04142    Selected client cert with alias 'User<ID>' and requestId 'ModelName=<ModelName>%2FLogicalName_<LogicalName>;Hash=-912418295'.
2019-08-01T19:22:47.4120000    VERB    com.microsoft.omadm.Services    15118    04142    Successfully applied, enabled and saved wifi profile '<profile ID>'
2019-08-01T19:22:47.4240000    VERB    com.microsoft.omadm.platforms.android.wifimgr.OneX    15118    04142    Starting to parse OneX from Wifi XML.
2019-08-01T19:22:47.4910000    VERB    com.microsoft.omadm.platforms.android.wifimgr.OneX    15118    04142    Completed parsing OneX from Wifi XML.
2019-08-01T19:22:47.4970000    VERB    com.microsoft.omadm.platforms.android.wifimgr.WifiProfile    15118    04142    Starting to parse Wifi Profile XML with name '<profile ID>'.
2019-08-01T19:22:47.5080000    VERB    com.microsoft.omadm.platforms.android.wifimgr.OneX    15118    04142    Starting to parse OneX from Wifi XML.
2019-08-01T19:22:47.5820000    VERB    com.microsoft.omadm.platforms.android.wifimgr.OneX    15118    04142    Completed parsing OneX from Wifi XML.
2019-08-01T19:22:47.5900000    VERB    com.microsoft.omadm.platforms.android.wifimgr.WifiProfile    15118    04142    Completed parsing Wifi Profile XML with name '<profile ID>'.
2019-08-01T19:22:47.5910000    INFO    com.microsoft.omadm.platforms.android.wifimgr.WifiProfileManager    15118    04142    Applied profile <profile ID>

```

## <a name="iosipados"></a>iOS/iPadOS

Po instalaci profilu sítě Wi-Fi na zařízení se zobrazí v **profilu správy**:

> [!div class="mx-imgBorder"]
> ![Profil správy v zařízení se systémem iOS/iPadOS v Intune](./media/troubleshoot-wi-fi-profiles/ios-management-profile.png)

> [!div class="mx-imgBorder"]
> ![Připojení Wi-Fi ukazuje jako síť Wi-Fi v zařízení s iOS nebo iPadOS v Intune.](./media/troubleshoot-wi-fi-profiles/ios-wifi-connection-in-management-profile.png)

### <a name="review-the-iosipados-console-and-device-logs"></a>Zkontrolujte konzolu iOS/iPadOS a protokoly zařízení.

V zařízeních se systémem iOS/iPadOS neobsahuje protokol aplikací Portál společnosti informace o profilech sítě Wi-Fi. Chcete-li zobrazit podrobnosti o instalaci profilů sítě Wi-Fi, použijte protokoly konzoly nebo zařízení:

1. Připojte zařízení s iOS/iPadOS k počítači Mac. Přejdete na**nástroje** **aplikace** > a otevřete konzolovou aplikaci.
2. V části **Akce**vyberte **Zahrnout informační zprávy** a **zahrnout zprávy ladění**:

    > [!div class="mx-imgBorder"]
    > ![Zahrnutí informací o zprávách a zahrnutí zpráv ladění do konzolové aplikace iOS/iPadOS](./media/troubleshoot-wi-fi-profiles/ios-console-app-include-info-messages-debug-messages.png)

3. Reprodukování scénáře a uložení protokolů do textového souboru:

    1. Vyberte všechny zprávy na aktuální obrazovce: **Upravit** > **Vybrat vše**.
    2. Zkopírujte zprávy: **Upravit** > **kopii**.
    3. Vložte data protokolu do textového editoru a soubor uložte.

4. Pokud chcete zobrazit podrobné informace, prohledejte uložený soubor protokolu. Po úspěšné instalaci profilu bude výstup vypadat podobně jako v následujícím protokolu:

    ```log
    Line 390870: debug    11:19:58.994815 -0400    profiled    Adding dependent www.windowsintune.com.wifi.Contoso to parent Microsoft.Profiles.MDM in domain ManagingProfileToManagedProfile to system\
    Line 390872: debug    11:19:58.995210 -0400    profiled    Adding dependent Microsoft.Profiles.MDM to parent www.windowsintune.com.wifi.Contoso in domain ManagedProfileToManagingProfile to system\
    Line 392346: default    11:19:59.360460 -0400    profiled    Profile \'93www.windowsintune.com.wifi.Contoso\'94 installed.\
    ```

## <a name="windows"></a>Windows

Po instalaci profilu sítě Wi-Fi na zařízení přejděte na **Nastavení** > **účty** > **přístup do práce nebo do školy**. Vyberte > **informace o**účtu:

> [!div class="mx-imgBorder"]
> ![Přístup do práce nebo do školy a výběr informací na zařízení s Windows](./media/troubleshoot-wi-fi-profiles/windows-access-work-school-info.png)

V **oblastech spravovaných Microsoftem**se zobrazí **Wi-Fi** :

> [!div class="mx-imgBorder"]
> ![V oblastech spravovaných Microsoftem najdete informace o Wi-Fi uvedené ve Windows.](./media/troubleshoot-wi-fi-profiles/windows-wifi-areas-managed-by-microsoft.png)

Připojení Wi-Fi zobrazíte tak, že přejdete na **Nastavení** > **Network & Internet**  > **Wi-Fi**:

> [!div class="mx-imgBorder"]
> ![V systému Windows se v nastavení zobrazí připojení Wi-Fi jako známá síť.](./media/troubleshoot-wi-fi-profiles/windows-wifi-connection-known-networks.png)

### <a name="review-event-viewer-logs"></a>Kontrola protokolů prohlížeče událostí

V zařízeních s Windows se v Prohlížeč událostí protokolují podrobnosti o profilech sítě Wi-Fi:

1. Otevřete aplikaci **Prohlížeč událostí** .
2. V nabídce **zobrazení** vyberte možnost **Zobrazit protokoly pro ladění a analýzu**.
3.  > Rozbalte **protokoly aplikací a služeb****Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostic-Provider** > **admin** .

Výstup bude vypadat podobně jako v následujících protokolech:

```log
Log Name:      Microsoft-Windows-DeviceManagement-Enterprise-Diagnostics-Provider/Admin
Source:        Microsoft-Windows-DeviceManagement-Enterprise-Diagnostics-Provider
Date:          8/7/2019 8:01:41 PM
Event ID:      1506
Task Category: (1)
Level:         Information
Keywords:      (2)
User:          SYSTEM
Computer:      <Computer Name>
Description:
WiFiConfigurationServiceProvider: Node set value, type: (0x4), Result: (The operation completed successfully.).
```

## <a name="common-issues"></a>Běžné problémy

### <a name="issue-1-the-wi-fi-profile-isnt-deployed-to-the-device"></a>Problém 1: profil sítě Wi-Fi není v zařízení nasazený.

- Potvrďte, že je profil sítě Wi-Fi přiřazen ke správné skupině:

    1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **Devices** > **Konfigurace zařízení profily konfigurace**.
    2. Vyberte profil > **přiřazení**. Potvrďte, že vybrané skupiny jsou správné.
    3. Ve Správci koncového bodu vyberte **řešení potíží + podpora**. Zkontrolujte informace o **přiřazení** .

- Ve Správci koncového bodu vyberte **řešení potíží + podpora**. Zkontrolujte, jestli se zařízení může synchronizovat s Intune, a to tak, že zkontroluje **Poslední čas vrácení se změnami** .

- Pokud je profil sítě Wi-Fi propojený s důvěryhodným kořenovým a profilem SCEP, potvrďte, že oba profily budou nasazeny do zařízení. Profil sítě Wi-Fi má závislost na těchto profilech.

- V zařízeních se systémem Windows 10 a novějšími zkontrolujte protokol diagnostické informace MDM:

  1. Přejděte na **Nastavení** > **účty** > **přístup do práce nebo do školy**.
  2. Vyberte svůj pracovní nebo školní účet > **informace**.
  3. V dolní části stránky **Nastavení** vyberte **vytvořit sestavu**.
  4. Otevře se okno, které zobrazuje cestu k souborům protokolu. Vyberte **Exportovat**.
  5. Přejít na `\Users\Public\Documents\MDMDiagnostics` cestu a zobrazit sestavu:

      > [!div class="mx-imgBorder"]
      > ![Ukázkové diagnostické informace MDM zobrazující konfiguraci profilu Wi-Fi na zařízeních s Windows 10](./media/troubleshoot-wi-fi-profiles/windows-mdm-diagnostic-info.png)

  > [!TIP]
  > Další informace najdete v tématu [Diagnostika selhání MDM ve Windows 10](https://docs.microsoft.com/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10).

- Pokud v zařízeních s Androidem nejsou nainstalované důvěryhodné kořenové a profily SCEP na zařízení, zobrazí se v souboru Portál společnosti App Omadmlog následující položka:

  ``` log
  2019-08-01T19:18:13.5120000    INFO    com.microsoft.omadm.platforms.android.wifimgr.WifiProfileManager    15118    04105    Skipping Wifi profile <profile ID> because it is pending certificates.
  ```

  - Když jsou důvěryhodné kořenové a profily SCEP na zařízení s Androidem a vyhovují předpisům, profil sítě Wi-Fi nemusí být na zařízení. K tomuto problému dochází, když poskytovatel **CertificateSelector** z aplikace Portál společnosti nenajde certifikát, který by odpovídal zadaným kritériím. Konkrétní kritéria můžou být v šabloně certifikátu nebo v profilu SCEP.

    Pokud se nenašel shodný certifikát, certifikáty v zařízení nejsou nainstalované. Profil Wi-Fi se nepoužije, protože nemá správný certifikát. V tomto scénáři se v souboru Portál společnosti App Omadmlog zobrazí následující položka:

    ` Skipping Wifi profile <profile ID> because it is pending certificates.`

    Následující vzorový protokol zobrazuje Vyloučené certifikáty, protože byla zadána kritéria rozšířeného použití klíče (EKU) pro **jakékoli účely** . Ale certifikáty přiřazené k zařízení nemají tyto rozšířené použití klíče:

    ```log
    2018-11-27T21:10:37.6390000    VERB     com.microsoft.omadm.utils.CertUtils      14210    00948    Excluding cert with alias User<ID1> and requestId <requestID1> as it does not have any purpose EKU.
    2018-11-27T21:10:37.6400000    VERB     com.microsoft.omadm.utils.CertUtils      14210    00948    Excluding cert with alias User<ID2> and requestId <requestID2> as it does not have any purpose EKU.
    2018-11-27T21:10:37.6400000    VERB     com.microsoft.omadm.utils.CertUtils      14210    00948    0 cert(s) matched criteria:
    2018-11-27T21:10:37.6400000    VERB     com.microsoft.omadm.utils.CertUtils      14210    00948    2 cert(s) excluded by criteria:
    2018-11-27T21:10:37.6400000    INFO       com.microsoft.omadm.platforms.android.wifimgr.WifiProfileManager       14210                00948     Skipping Wifi profile <profile ID> because it is pending certificates.
    ```

    Následující ukázka znázorňuje profil SCEP, který jste zadali pro **účely** rozšířené použití klíče. Ale není zadaný v šabloně certifikátu certifikační autority (CA). Chcete-li tento problém vyřešit, přidejte do šablony certifikátu možnost **libovolný účel** . Případně z profilu SCEP odeberte možnost **libovolný účel** .

    > [!div class="mx-imgBorder"]
    > ![V Androidu přidejte jakýkoli účel do šablony certifikátu v certifikační autoritě.](./media/troubleshoot-wi-fi-profiles/android-add-any-purpose-eku.png)

    > [!div class="mx-imgBorder"]
    > ![V Androidu přidejte libovolný účel do konfiguračního profilu certifikátu SCEP v Intune.](./media/troubleshoot-wi-fi-profiles/android-any-purpose-scep-device-config-profile.png)

  - Potvrďte, že všechny požadované certifikáty v rámci kompletního řetězu certifikátů jsou na zařízení s Androidem. V opačném případě se profil sítě Wi-Fi nedá na zařízení nainstalovat. Další informace najdete v tématu [chybějící zprostředkující certifikační autorita](https://developer.android.com/training/articles/security-ssl#MissingCa) (otevře web v Androidu).
  - Vyfiltrujte Omadmlog s klíčovými slovy pro hledání informací, například který certifikát se používá v profilu sítě Wi-Fi, a pokud byl profil úspěšně použit.

    Můžete například použít [CMTrace](https://docs.microsoft.com/configmgr/core/support/cmtrace) ke čtení protokolů. Pomocí vyhledávacího řetězce vyfiltrujte "wifimgr":

    > [!div class="mx-imgBorder"]
    > ![Filtrovat CMTrace, aby se vyhledaly konfigurační profily WiFiMgr na zařízeních s Androidem](./media/troubleshoot-wi-fi-profiles/cmtrace-filter-wifimgr.png)

    Výstup bude vypadat podobně jako v následujícím protokolu:

    > [!div class="mx-imgBorder"]
    > ![Ukázkový výstup protokolu CMTrace, který zobrazuje profil konfigurace Wi-Fi na zařízeních byl úspěšně použit](./media/troubleshoot-wi-fi-profiles/cmtrace-sample-log-output.png)

    Pokud se v protokolu zobrazí chyba, zkopírujte časové razítko chyby a Odfiltrujte protokol. Pak použijte možnost najít s časovým razítkem, abyste zjistili, co se stalo hned před chybou.

### <a name="issue-2-the-wi-fi-profile-is-deployed-to-the-device-but-the-device-cant-connect-to-the-network"></a>Problém 2: profil Wi-Fi se nasadí do zařízení, ale zařízení se nemůže připojit k síti.

K tomuto problému obvykle dochází z nějakého důvodu mimo Intune. Následující úkoly vám můžou pomoct pochopit a řešit potíže s připojením:

- Ručně se připojte k síti pomocí certifikátu se stejnými kritérii, která jsou v profilu sítě Wi-Fi.

  Pokud se můžete připojit, podívejte se na vlastnosti certifikátu v ručním připojení. Pak aktualizujte profil Wi-Fi v Intune se stejnými vlastnostmi certifikátu.
- Chyby připojení se obvykle protokolují v protokolu serveru RADIUS. Například by se mělo zobrazit, jestli se zařízení pokusilo připojit k profilu sítě Wi-Fi.

## <a name="need-more-help"></a>Potřebujete další podrobnější informace

- Použijte [fóra uživatelů Intune](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc) nebo [Získejte podporu od Microsoftu](../fundamentals/get-support.md).

- Další informace o profilech Wi-Fi v Microsoft Intune najdete v následujících článcích:

  - Přidejte nastavení Wi-Fi pro zařízení se systémem [Android](wi-fi-settings-android.md), [iOS/iPadOS](wi-fi-settings-ios.md)a [Windows 10 a novějším](wi-fi-settings-windows.md).
  - [Tip podpory – jak nakonfigurovat NDES pro nasazení certifikátů SCEP v Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-How-to-configure-NDES-for-SCEP-certificate/ba-p/455125)
  - Řešení potíží s [nasazením profilu certifikátu SCEP](https://support.microsoft.com/help/4526725/troubleshooting-scep-profile-deployment-to-android-devices-in-intune) a [konfigurací NDES](https://support.microsoft.com/help/4459540/troubleshoot-ndes-configuration-for-use-with-intune).

- Nejnovější novinky, informace a technické tipy najdete v oficiálních blogech:
  - [Blog týmu podpory pro Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
  - [Microsoft Enterprise mobility and Security blog](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity)

## <a name="next-steps"></a>Další kroky

[Monitorujte své profily](device-profile-monitor.md).
