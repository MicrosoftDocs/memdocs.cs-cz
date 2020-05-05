---
title: Vyloučení antivirové ochrany
titleSuffix: Configuration Manager
description: Seznamte se s doporučenými vyloučeními antivirového programu pro použití při řešení možných problémů.
ms.date: 10/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb470e3-6f6b-4ccf-b3d8-1598d79d3490
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: df951bfb44313cfec8dacb8c0df34abb7beb0c56
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720293"
---
# <a name="recommended-antivirus-exclusions-for-configuration-manager"></a>Doporučená vyloučení antivirového programu pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek obsahuje doporučení, která správcům pomohou určit příčinu potenciální nestability v počítači, na kterém je spuštěná podporovaná verze Configuration Manager servery lokality, systémy lokality a klienty, pokud se používají společně s antivirovým softwarem.

> [!IMPORTANT]
>
> - Doporučujeme, abyste tyto postupy dočasně použili k vyhodnocení systému. Pokud je výkon systému nebo stabilita vylepšena doporučeními provedenými v tomto článku, obraťte se na dodavatele antivirového softwaru s pokyny nebo na aktualizovanou verzi antivirového softwaru.
> - Tento článek obsahuje informace, které ukazují, jak můžete snížit nastavení zabezpečení nebo jak dočasně vypnout funkce zabezpečení v počítači. Tyto změny můžete využít k pochopení povahy konkrétního problému. Než provedete tyto změny, doporučujeme, abyste vyhodnotili rizika spojená s implementací tohoto řešení v konkrétním prostředí.

## <a name="possible-symptoms"></a>Možné příznaky 

Antivirová ochrana v reálném čase může způsobit mnoho problémů na Configuration Manager serverech lokality, systémech lokality a klientech.

Níže je seznam možných příznaků, které jsou nevyčerpávající:

- Vzdálené součásti systému lokality nejsou nainstalovány. SiteComp. log, Distmgr. log, hman. log nebo jiné soubory protokolu Configuration Manager mohou obsahovat chyby, například Chyba 80070005.
- Klienta Configuration Manager nelze nainstalovat pomocí klientské nabízené instalace.
- Informace o inventáři klienta jsou nepřesné, chybí nebo nejsou aktuální.
- K nevyřízeným položkám dojde ve složkách *Install_Directory*\Program Files\Microsoft Configuration Manager\Inboxes.
- Software Center není vyplněn nasazeným softwarem v klientských systémech nebo není spuštěn. Soubor CCMRepair. log také může obsahovat chyby, které se podobají následujícímu příkladu:

  > Ověření databáze se nezdařilo s výsledkem: 0x80004005, ale DB: C:\Windows\CCM\filename.sdf by bylo možné otevřít, oprava databáze bude přeskočena.

- Software, který je nasazený pro klienty, nejde nainstalovat.
- Data dodržování předpisů pro nasazení softwaru jsou nepřesná.

## <a name="exclusions"></a>Vyloučení

Chcete-li těmto problémům zabránit, doporučujeme přidat následující vyloučení ochrany v reálném čase:

### <a name="default-installation-folders"></a>Výchozí instalační složky

|  |  |
| - | - |
|*Instalační složka nástroje ConfigMgr*  |  %ProgramFiles%\Microsoft Configuration Manager  |  
|*Instalační složka sady MP*  |% ProgramFiles% \ SMS_CCM  |  
|*Instalační složka klienta*  |%Windir%\CCM  |  

### <a name="folder-exclusions-for-site-servers"></a>Vyloučení složky pro servery lokality

- *Instalační složka nástroje ConfigMgr*\Inboxes
- *Instalační složka nástroje ConfigMgr*\Logs.
- *Instalační složka nástroje ConfigMgr*\EasySetupPayload

### <a name="folder-exclusions-for-site-systems"></a>Vyloučení složek pro systémy lokality

- Body správy
  - \ServiceData *instalační složky sady MP*
  - Jednu z následujících:
    - *Instalační složka nástroje ConfigMgr*\MP\OUTBOXES
    - *Instalační jednotka*\SMS\MP\OUTBOXES
- Distribuční body
  - \ServiceData *instalační složky klienta*
  - *ContentLib_Drive*\ SMS_DP $
  - *ContentLib_Drive*\SMSPKG*Drive_Letter*$
  - *ContentLib_Drive*\SMSPKG
  - *ContentLib_Drive*\SMSPKGSIG
  - *ContentLib_Drive*\SMSSIG $
- Servery databáze lokality
  - [Jak zvolit antivirový software, který se má spustit na počítačích se spuštěným SQL Server](https://support.microsoft.com/en-us/help/309422)

### <a name="folder-exclusions-for-clients"></a>Vyloučení složek pro klienty

- *Instalační složka*\\\*klienta. sdf
- \ServiceData *instalační složky klienta*
- C:\Windows\CCMCache
- C:\Windows\CCMSetup
- \Logs. *instalační složky klienta*

### <a name="file-exclusions-for-mps"></a>Vyloučení souborů pro sady Management Pack

- POL00000. Pol v
  - \PolReqStaging *instalační složky sady MP*

### <a name="process-exclusions"></a>Vyloučení procesů

Vyloučení procesů jsou nutná pouze v případě, že agresivní antivirové programy považují za vysoce rizikové procesy Configuration Manager programových souborů (soubory. exe).

- *Instalační složka nástroje ConfigMgr*\bin\64\Smsexec.exe
- Jeden z následujících procesů:
  - \Ccmexec.exe *instalační složky klienta*
  - \Ccmexec.exe *instalační složky sady MP*
- *Instalační složka klienta*\CmRcService.exe (na straně klienta)
- *Instalační složka nástroje ConfigMgr*\bin\64\Sitecomp.exe
- *Instalační složka nástroje ConfigMgr*\bin\64\Smswriter.exe
- *Instalační složka nástroje ConfigMgr*\bin\64\Smssqlbkup.exe nebo SMS_*SQLFQDN*\bin\x64\Smssqlbkup.exe
- *Instalační složka nástroje ConfigMgr*\bin\64\Cmupdate.exe
- *Instalační složka klienta*\Ccmrepair.exe (na straně klienta)
- %*windir*% \ CCMSetup\Ccmsetup.exe (na straně klienta)

## <a name="next-steps"></a>Další kroky

Další informace o výjimkách antivirové ochrany najdete v následujících článcích:

[Vyloučení antivirové ochrany Configuration Manager Current Branch – blog System Center Premier Field inženýr](https://blogs.technet.microsoft.com/systemcenterpfe/2017/05/24/configuration-manager-current-branch-antivirus-update/)

[Aktualizace softwaru System Center 2012 Configuration Manager vyloučení antivirové ochrany s dalšími podrobnostmi o technologiích OSD a spouštěcích bitových kopiích](https://blogs.technet.microsoft.com/systemcenterpfe/2013/01/11/updated-system-center-2012-configuration-manager-antivirus-exclusions-with-more-details-on-osd-and-boot-images-etc/)

[Jak zvolit antivirový software, který se má spustit na počítačích se spuštěným SQL Server](https://support.microsoft.com/en-us/help/309422/how-to-choose-antivirus-software-to-run-on-computers-that-are-running-sql-server)

[Doporučení pro kontrolu virů pro podnikové počítače, na kterých běží aktuálně podporované verze Windows](https://support.microsoft.com/en-us/help/822158/virus-scanning-recommendations-for-enterprise-computers-that-are-running-currently-supported-versions-of-windows)
