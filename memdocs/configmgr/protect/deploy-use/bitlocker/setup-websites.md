---
title: Nastavení portálů nástroje BitLocker
titleSuffix: Configuration Manager
description: Instalace součástí pro správu nástroje BitLocker pro samoobslužný portál a web pro správu a monitorování
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 1cd8ac9f-b7ba-4cf4-8cd2-d548b0d6b1df
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5dbd782c97d11f8077c18796c87c7880eb26f3f3
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129150"
---
# <a name="set-up-bitlocker-portals"></a>Nastavení portálů nástroje BitLocker

*Platí pro: Configuration Manager (Current Branch)*

<!--3601034-->

Chcete-li použít následující komponenty správy nástroje BitLocker v Configuration Manager, je nutné je nejprve nainstalovat:

- Samoobslužný portál uživatele
- Web pro správu a monitorování (portál helpdesk)

Portály můžete nainstalovat na existující server lokality nebo server systému lokality s nainstalovanou službou IIS nebo k jejich hostování použít samostatný webový server.

> [!NOTE]
> Počínaje verzí 2006 můžete nainstalovat Samoobslužný portál BitLocker a web pro správu a monitorování v lokalitě centrální správy.<!-- 5925693 -->
>
> Ve verzi 2002 a starší nainstalujte jenom Samoobslužný portál a web pro správu a monitorování s databází primární lokality. V hierarchii nainstalujte tyto weby pro každou primární lokalitu.

Než začnete, potvrďte [předpoklady](../../plan-design/bitlocker-management.md#prerequisites) pro tyto komponenty.

## <a name="run-the-script"></a>Spuštění skriptu

Na cílovém webovém serveru proveďte následující akce:

> [!NOTE]
> V závislosti na návrhu lokality možná budete muset skript spustit několikrát. Například spuštěním skriptu v bodu správy nainstalujete web pro správu a monitorování. Pak ho znovu spusťte na samostatném webovém serveru a nainstalujte samoobslužný portál.

1. Zkopírujte následující soubory z `SMSSETUP\BIN\X64` instalační složky nástroje Configuration Manager na serveru lokality do místní složky na cílovém serveru:

    - `MBAMWebSite.cab`
    - `MBAMWebSiteInstaller.ps1`

1. Spusťte PowerShell jako správce a potom spusťte skript podobný následujícímu příkazovému řádku:

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName <ServerName> -SqlInstanceName <InstanceName> -SqlDatabaseName <DatabaseName> -ReportWebServiceUrl <ReportWebServiceUrl> -HelpdeskUsersGroupName <DomainUserGroup> -HelpdeskAdminsGroupName <DomainUserGroup> -MbamReportUsersGroupName <DomainUserGroup> -SiteInstall Both
    ```

    Příklad:

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName sql.contoso.com -SqlInstanceName instance1 -SqlDatabaseName CM_ABC -ReportWebServiceUrl https://rsp.contoso.com/ReportServer -HelpdeskUsersGroupName "contoso\BitLocker help desk users" -HelpdeskAdminsGroupName "contoso\BitLocker help desk admins" -MbamReportUsersGroupName "contoso\BitLocker report users" -SiteInstall Both
    ```

    > [!IMPORTANT]
    > Tento příklad příkazového řádku používá všechny možné parametry k zobrazení jejich použití. Upravte své použití podle vašich požadavků ve vašem prostředí.

Po instalaci přístup k portálům přes následující adresy URL:

- Samoobslužný portál:`https://webserver.contoso.com/SelfService`
- Web pro správu a monitorování:`https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> Společnost Microsoft doporučuje, ale nevyžaduje použití protokolu HTTPS. Další informace najdete v tématu [jak nastavit protokol SSL ve službě IIS](https://docs.microsoft.com/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="script-usage"></a>Použití skriptu

Tento proces používá skript prostředí PowerShell, MBAMWebSiteInstaller.ps1 k instalaci těchto součástí na webový server. Přijímá následující parametry:

- `-SqlServerName <ServerName>`(povinné): plně kvalifikovaný název domény serveru databáze primární lokality.

- `-SqlInstanceName <InstanceName>`: SQL Server název instance databáze primární lokality. Pokud SQL používá výchozí instanci, nezahrnujte tento parametr.

- `-SqlDatabaseName <DatabaseName>`(povinné): název databáze primární lokality, například `CM_ABC` .

- `-ReportWebServiceUrl <ReportWebServiceUrl>`: URL webové služby bodu služby generování sestav primární lokality. Je to hodnota **URL webové služby** ve **službě Reporting Services Configuration Manager**.

    > [!NOTE]
    > Tento parametr slouží k instalaci **sestavy auditu obnovení** , která je propojena z webu pro správu a monitorování. Ve výchozím nastavení Configuration Manager zahrnuje další sestavy správy nástroje BitLocker.

- `-HelpdeskUsersGroupName <DomainUserGroup>`: Například `contoso\BitLocker help desk users` . Skupina uživatelů domény, jejíž členové mají přístup ke **správě čipu TPM** a k řízení oblastí **obnovení** na webu pro správu a monitorování. Při použití těchto možností musí tato role vyplnit všechna pole, včetně názvu domény a účtu uživatele.

- `-HelpdeskAdminsGroupName <DomainUserGroup>`: Například `contoso\BitLocker help desk admins` . Skupina uživatelů domény, jejíž členové mají přístup ke všem oblastem obnovení webu pro správu a monitorování. Při pomoci uživatelům obnovit své jednotky stačí, aby tato role zadala obnovovací klíč.

- `-MbamReportUsersGroupName <DomainUserGroup>`: Například `contoso\BitLocker report users` . Skupina uživatelů domény, jejíž členové mají přístup jen pro čtení k oblasti **sestav** na webu Správa a monitorování.

    > [!NOTE]
    > Skript instalačního programu nevytvoří skupiny uživatelů domény, které zadáte v parametrech **-HelpdeskUsersGroupName**, **-HelpdeskAdminsGroupName**a **-MbamReportUsersGroupName** . Před spuštěním skriptu Nezapomeňte tyto skupiny vytvořit.
    >
    > Když zadáte parametry **-HelpdeskUsersGroupName**, **-HelpdeskAdminsGroupName**a **-MbamReportUsersGroupName** , nezapomeňte zadat název domény i název skupiny. Použijte formát `"domain\user_group"`. Vylučte název domény. Pokud název domény nebo název skupiny obsahuje mezery nebo speciální znaky, uzavřete parametr do uvozovek ( `"` ).

- `-SiteInstall Both`: Určete, které součásti se mají nainstalovat. Mezi platné možnosti patří:
  - `Both`: Nainstalovat obě součásti
  - `HelpDesk`: Instalovat pouze web pro správu a monitorování
  - `SSP`: Instalovat jenom Samoobslužný portál

- `-IISWebSite`: Web, na který skript nainstaluje webové aplikace MBAM. Ve výchozím nastavení používá výchozí web služby IIS. Před použitím tohoto parametru vytvořte vlastní web.

- `-InstallDirectory`: Cesta, kam skript nainstaluje soubory webových aplikací. Ve výchozím nastavení je tato cesta `C:\inetpub` . Před použitím tohoto parametru vytvořte vlastní adresář.

- `-Uninstall`: Odinstaluje webové portály pro správu nástroje BitLocker a samoobslužné webové portály na webovém serveru, kde byly dříve nainstalovány.

## <a name="verify"></a>Ověření

Monitorování a řešení potíží pomocí následujících protokolů:

- Protokoly událostí Windows v části **Microsoft-Windows-MBAM-web**. Další informace najdete v tématu [protokoly událostí BitLockeru](../../tech-ref/bitlocker/about-event-logs.md) a [protokoly událostí serveru](../../tech-ref/bitlocker/server-event-logs.md).

- Protokoly trasování pro jednotlivé komponenty jsou v následujících výchozích umístěních:

  - Samoobslužný portál:`C:\inetpub\Microsoft BitLocker Management Solution\Logs\Self Service Website`

  - Web pro správu a monitorování:`C:\inetpub\Microsoft BitLocker Management Solution\Logs\Help Desk Website`

Další informace o řešení potíží najdete v tématu [řešení potíží s nástrojem BitLocker](../../tech-ref/bitlocker/troubleshoot.md).

## <a name="next-steps"></a>Další kroky

[Přizpůsobení samoobslužného portálu](customize-self-service-portal.md)

Další informace o používání komponent, které jste nainstalovali, najdete v následujících článcích:

- [Web pro správu a monitorování BitLockeru](helpdesk-portal.md)
- [Samoobslužný portál BitLocker](self-service-portal.md)
