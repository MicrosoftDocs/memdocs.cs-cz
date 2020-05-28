---
title: Předpoklady pro aktualizace softwaru
titleSuffix: Configuration Manager
description: Přečtěte si o požadavcích na aktualizace softwaru v Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/22/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.openlocfilehash: a870d2bf18b9e7f064e914f450aee0f5e3e2e545
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906707"
---
# <a name="prerequisites-for-software-updates-in-configuration-manager"></a>Předpoklady pro aktualizace softwaru v nástroji Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

V tomto článku jsou uvedeny předpoklady pro aktualizace softwaru v nástroji Configuration Manager. U každého z požadovaných požadavků jsou externí závislosti a vnitřní závislosti uvedeny v samostatných tabulkách.  

## <a name="software-update-dependencies-that-are-external-to-configuration-manager"></a>Závislosti aktualizace softwaru, které jsou externě Configuration Manager  
 V následujících částech jsou uvedeny externí závislosti pro aktualizace softwaru.  

### <a name="internet-information-services"></a>Internet Information Services  
 Pro spuštění bodu aktualizace softwaru, bodu správy a distribučního bodu musí být na serverech systému lokality nainstalována služba Internetová informační služba (IIS). Více informací najdete v tématu [Předpoklady pro role systému lokality](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### <a name="windows-server-update-services"></a>Windows Server Update Services  
 Služba WSUS je nutná pro synchronizaci aktualizací softwaru a pro kontrolu použitelnosti aktualizací softwaru na klientech. Windows Server Update Services Před vytvořením role bodu aktualizace softwaru musí být nainstalován server služby WSUS. Pro bod aktualizace softwaru jsou podporovány následující verze serveru WSUS:  

- Služba WSUS 10.0.14393 (role ve Windows serveru 2016)
- Služba WSUS 10.0.17763 (role ve Windows serveru 2019) (vyžaduje Configuration Manager 1810 nebo novější)
- WSUS 6,2 a 6,3 (role v systému Windows Server 2012 a Windows Server 2012 R2)
  - Pokud nasadíte upgrady Windows 10, pro WSUS 6,2 a 6,3 se vyžadují [kb 3095113 a kb 3159706 (nebo ekvivalentní aktualizace)](#BKMK_wsus2012) .

> [!NOTE]
> - Máte-li v lokalitě více bodů aktualizace softwaru, zajistěte, aby všechny používaly stejnou verzi služby WSUS.

### <a name="wsus-administration-console"></a>Konzola správy služby WSUS  
Pokud je bod aktualizace softwaru na vzdáleném serveru systému lokality a služba WSUS není na serveru lokality již nainstalována, je konzola pro správu služby WSUS požadována na serveru lokality Configuration Manager.  

> [!IMPORTANT]  
> - Verze služby WSUS na serveru lokality musí být stejná jako verze služby WSUS spuštěná v bodech aktualizace softwaru.
> - Nepoužívejte ke konfiguraci nastavení služby WSUS konzolu pro správu služby WSUS. Configuration Manager se připojí k instanci serveru WSUS, která běží v bodě aktualizace softwaru, a nakonfiguruje příslušná nastavení.  


### <a name="windows-update-agent"></a>Windows Update Agent  
 Klient agenta web Windows Update (WUA) je požadován na klientech, aby se mohl připojit k serveru WSUS. WUA načte seznam aktualizací softwaru, které musí kontrolovat dodržování předpisů.  

 Při instalaci Configuration Manager je stažena nejnovější verze agenta WUA. Po instalaci klienta Configuration Manager pak bude Agent WUA v případě potřeby upgradován. Pokud se instalace nezdařila, je nutné použít jinou metodu k upgradu agenta WUA.  

## <a name="software-update-dependencies-that-are-internal-to-configuration-manager"></a>Závislosti aktualizací softwaru, které jsou interní pro Configuration Manager  
 V následujících částech jsou uvedeny interní závislosti pro aktualizace softwaru v nástroji Configuration Manager.  

### <a name="management-points"></a>Body správy  
 Body správy přenášejí informace mezi klientskými počítači a Configuration Manager lokality. Body správy jsou požadovány pro aktualizace softwaru.  

### <a name="software-update-points"></a>Body aktualizace softwaru  
 Chcete-li nasadit aktualizace softwaru v nástroji Configuration Manager, je nutné nainstalovat bod aktualizace softwaru na server WSUS. Další informace najdete v tématu [instalace a konfigurace bodu aktualizace softwaru](../get-started/install-a-software-update-point.md).

### <a name="distribution-points"></a>Distribuční body  
 Distribuční body jsou vyžadovány k ukládání obsahu pro aktualizace softwaru. Další informace o instalaci distribučních bodů a správě obsahu najdete v tématu [Správa obsahu a infrastruktury obsahu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="client-settings-for-software-updates"></a>Nastavení klienta pro aktualizace softwaru  
Ve výchozím nastavení jsou aktualizace softwaru pro klienty povoleny. Existují další dostupná nastavení, která řídí, jak a kdy klienti vyhodnocují dodržování předpisů pro aktualizace softwaru a řídí, jak jsou aktualizace softwaru nainstalovány.  

 Další informace najdete v následujících článcích:  

- [Nastavení klienta pro aktualizace softwaru](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

- [Nastavení klienta pro aktualizace softwaru](../../core/clients/deploy/about-client-settings.md#software-updates)  

### <a name="reporting-services-points"></a>Body služby Reporting services  
 Role systému lokality bodu služeb generování sestav může zobrazovat sestavy pro aktualizace softwaru. Tato role je volitelná, ale doporučuje se. Další informace o vytvoření bodu služby Reporting Services najdete v tématu [Konfigurace generování sestav](../../core/servers/manage/configuring-reporting.md).  

## <a name="which-updates-are-required-on-wsus-62-and-63"></a><a name="BKMK_wsus2012"></a>Které aktualizace jsou vyžadovány ve službě WSUS 6,2 a 6,3?

Pro klasifikaci synchronizovaných **upgradů** ve službě WSUS 6,2 a 6,3 jsou vyžadovány dvě aktualizace. V některých případech se může zobrazit chyba při stahování nebo nasazování upgradů, pokud byly synchronizovány před instalací KB3095113 a KB3159706. Informace o možných problémech najdete v další části.  

- Před synchronizací klasifikace **upgrady** je nutné nainstalovat aktualizaci [KB 3095113](https://support.microsoft.com/kb/3095113)v říjnu 2015 na body aktualizace softwaru a servery lokality.
  - Tato aktualizace umožňuje klasifikaci **upgrady** .
- Aby bylo možné služby Windows 10 verze 1607 a novější, musíte nainstalovat a nakonfigurovat [KB 3159706](https://support.microsoft.com/help/3159706). Znalostní báze KB 3159706 byl vydán v květnu 2016.
  - Tato aktualizace umožňuje službě WSUS nativně dešifrovat soubory používané pro upgrade Windows 10 verze 1607 nebo novější.

>[!IMPORTANT]
> Aktualizace KB 3095113 a KB 3159706 jsou zahrnuté do **měsíčních souhrnů kvality zabezpečení** od července 2017. To znamená, že neuvidíte KB 3095113 a KB 3159706 jako nainstalované aktualizace, protože byly pravděpodobně nainstalovány se souhrnem. Pokud ale některé z těchto aktualizací potřebujete, doporučujeme nainstalovat **Měsíční souhrn kvality zabezpečení** vydaný po 2017. říjnu, protože obsahuje další aktualizaci WSUS pro snížení využití paměti na CLIENTWEBSERVICE serveru WSUS.

## <a name="download-of-windows-10-upgrades-fails-with-error-invalid-certificate-signature-or-0xc1800118"></a><a name="BKMK_RecoverUpgrades"></a>Stažení upgradů Windows 10 se nepovedlo s chybou: neplatný podpis certifikátu nebo 0xc1800118

Aktualizace a problémy popsané v této části se vztahují jenom na službu WSUS spuštěnou v počítačích se systémem Windows Server 2012 nebo Windows Server 2012 R2 (WSUS 6,2 a 6,3). Problémy popsané v této části se obvykle zobrazí jenom v případě, že jste nainstalovali službu WSUS do července 2017 a nedávno jste povolili klasifikaci **upgrady** . Je ale možné, že tyto problémy vidíte i v jiných situacích.

### <a name="historical-information-about-kb-3095113"></a>Historické informace o KB 3095113

 [Znalostní báze KB 3095113](https://support.microsoft.com/kb/3095113) byl [vydán jako oprava hotfix](https://docs.microsoft.com/archive/blogs/wsus/important-update-for-wsus-4-0-kb-3095113) v říjnu 2015 za účelem přidání podpory pro upgrady Windows 10 do služby WSUS. Tato aktualizace umožňuje službě WSUS synchronizovat a distribuovat aktualizace v klasifikaci **upgrady** pro Windows 10.

Pokud synchronizujete upgrady bez první instalace [KB 3095113](https://support.microsoft.com/kb/3095113), naplníte databázi služby WSUS (SUSDB) nepoužitelnými daty. Tato data musí být smazána před tím, než bude možné upgrady správně nasadit. Upgrady Windows 10 v tomto stavu nelze stáhnout pomocí Průvodce stažením aktualizací softwaru.

Chyby, které se podobají následujícímu, se zobrazí na stránce dokončení Průvodce stažením aktualizací softwaru:

``` Output
Error: Upgrade to Windows 10 Pro, version 1511, 10586
Failed to download content id {content_id}. Error: Invalid certificate signature
```

Kromě toho se do souboru PatchDownloader. log zaznamenávají chyby podobné následujícímu:

``` Log
Download http://wsus.ds.b1.download.windowsupdate.com/d/upgr/2015/12/10586.0.151029-1700.th2_release_...esd...
Authentication of file C:\Users\{username}\AppData\Local\Temp\2\{temporary_filename}.tmp failed, error 0x800b0004
ERROR: DownloadContentFiles() failed with hr=0x80073633
# This log is truncated for readability.
```

V minulosti byly při výskytu těchto chyb vyřešeny upravenou verzí [kroků řešení pro službu WSUS](https://docs.microsoft.com/archive/blogs/wsus/how-to-delete-upgrades-in-wsus). Vzhledem k tomu, že se tyto kroky podobají řešení, pokud není potřeba provést ruční kroky po instalaci KB 3159706, zkombinujeme obě sady kroků do jediného řešení v následující části:

- [Obnovení z synchronizace upgradů před instalací kb 3095113 nebo kb 3159706](#bkmk_fix-upgrades).

### <a name="historical-information-about-kb-3159706"></a>Historické informace o KB 3159706

Znalostní báze KB 3148812 byl původně vydaný v dubnu 2016 a umožňuje službě WSUS nativně dešifrovat soubory. ESD používané pro Upgrade balíčků Windows 10. [Kb 3148812 způsobilo pro některé zákazníky problémy](https://docs.microsoft.com/archive/blogs/wsus/the-long-term-fix-for-kb3148812-issues) a byl nahrazen v [KB 3159706](https://support.microsoft.com/help/3159706). Aby bylo možné obsluhovat zařízení se systémem Windows 10 verze 1607 a novější, je nutné nainstalovat na všechny body aktualizace softwaru a servery lokality aktualizaci KB 3159706. Problémy mohou nastat, pokud si nejste vědomi, že KB vyžaduje po instalaci následující ruční kroky:

1. Z příkazového řádku se zvýšenými oprávněními spusťte `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing` .
1. Restartujte službu WSUS na všech serverech WSUS.

Pokud si nejste vědomi, že znalostní báze KB 3159706 obsahovala po instalaci ruční kroky nebo jste v upgradu na systém Windows 10 1607 předtím, než nainstalujete KB 3159706, narazíte na problémy s připojením ke konzole služby WSUS a nasazením upgradu. Když klient stáhl soubor upgradu, získá [kód chyby **0xC1800118** ](https://support.microsoft.com/help/3194588/0xc1800118-error-when-you-push-windows-10-version-1607-by-using-wsus).

Vzhledem k tomu, že postup řešení je podobný rozlišení pro synchronizaci upgradů před instalací KB 3095113, zkombinujeme obě sady kroků do jediného řešení v následující části.
 

### <a name="to-recover-from-synchronizing-the-upgrades-before-you-install-kb-3095113-or-kb-3159706"></a><a name="bkmk_fix-upgrades"></a>Obnovení z synchronizace upgradů před instalací KB 3095113 nebo KB 3159706

Použijte následující postup k vyřešení 0xc1800118 chyby a "Chyba: neplatný podpis certifikátu":

1. Zakažte klasifikaci **upgrady** v WSUS i Configuration Manager. Nechcete, aby k synchronizaci docházelo, dokud nebudete přesměrováni podle těchto pokynů.  
   - Zrušte kontrolu klasifikace **upgrady** ve vlastnostech komponenty bodu aktualizace softwaru v lokalitě nejvyšší úrovně.
     - Další informace najdete v tématu [Konfigurace klasifikací a produktů](../get-started/configure-classifications-and-products.md).
   - Zrušte kontrolu klasifikace **upgrady** ze služby WSUS v části **produkty a klasifikace** na [stránce **Možnosti** ](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/manage/setting-up-update-synchronizations)nebo použijte prostředí PowerShell ISE spuštěné jako správce.
      ```PowerShell
      Get-WsusClassification | Where-Object -FilterScript {$_.Classification.Title -Eq "Upgrades"} | Set-WsusClassification -Disable
      ```  
     - Pokud sdílíte databázi služby WSUS mezi více servery WSUS, stačí pro každou databázi zrušit kontrolu **upgradů** .  
1. Na každém serveru WSUS spusťte z příkazového řádku se zvýšenými oprávněními příkaz: `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing` . Pak restartujte službu WSUS na všech serverech WSUS.
   -  Služba WSUS umístí databázi do [režimu jednoho uživatele](https://docs.microsoft.com/sql/relational-databases/databases/set-a-database-to-single-user-mode) předtím, než zkontroluje, jestli je potřeba servis. Obsluha buď běží, nebo neběží na základě výsledků kontroly. Pak se databáze vrátí zpět do režimu více uživatelů. 
   - Pokud sdílíte databázi služby WSUS mezi více servery WSUS, stačí provést tuto údržbu pouze jednou pro každou databázi.
1. Odstraňte všechny upgrady Windows 10 z každé databáze WSUS pomocí prostředí PowerShell ISE spuštěného jako správce.
   ```PowerShell
   [reflection.assembly]::LoadWithPartialName("Microsoft.UpdateServices.Administration")
   $wsus = [Microsoft.UpdateServices.Administration.AdminProxy]::GetUpdateServer();
   $wsus.GetUpdates() | Where {$_.UpdateClassificationTitle -eq 'Upgrades' -and $_.Title -match 'Windows 10'} `
   | ForEach-Object {$wsus.DeleteUpdate($_.Id.UpdateId.ToString()); Write-Host $_.Title removed}
   ```
1. Odstraňte soubory z tabulky tbFile ze všech databází služby WSUS používaných body aktualizace softwaru. V databázi WSUS spusťte následující příkazy z SQL Server Management Studio:
   ```SQL
   declare @NotNeededFiles table (FileDigest binary(20) UNIQUE)
   insert into @NotNeededFiles(FileDigest) (select FileDigest from tbFile where FileName like '%.esd%'  except select FileDigest from tbFileForRevision)
   delete from tbFileOnServer where FileDigest in (select FileDigest from @NotNeededFiles)
   delete from tbFile where FileDigest in (select FileDigest from @NotNeededFiles)
   ```
1. Spusťte synchronizaci aktualizací softwaru v lokalitě nejvyšší úrovně v Configuration Manager a počkejte, než se dokončí. Úplná synchronizace nastane, protože jsme po odebrání **upgradů**provedli změnu klasifikací Configuration Manager. (Další informace najdete v tématu [synchronizace aktualizací softwaru](../get-started/synchronize-software-updates.md).
1. Vyberte klasifikaci **upgrady** ve vlastnostech komponenty bodu aktualizace softwaru. Pak spusťte jinou synchronizaci aktualizací softwaru, aby se **upgrady** vrátily zpátky do WSUS a Configuration Manager. Nemusíte ve službě WSUS povolit klasifikaci **upgrady** , protože to Configuration Manager za vás.
1. Pokud klienti obdrželi kód chyby **0xC1800118** při stahování upgradu, bude nutné odstranit úložiště dat používané agentem web Windows Update. Může být také nutné odstranit skrytou složku ~ BT na zařízení. Při dalším prohledávání klienta bude na serveru WSUS úplná kontrola, nikoli rozdílová. Můžete použít skript prostředí PowerShell, který je podobný následujícímu ukázkovému skriptu:  
   ```PowerShell
   stop-service wuauserv
   remove-item -path c:\windows\softwaredistribution\datastore -recurse -force
   # If the device has a hidden ~BT folder on the c drive, delete it too by uncommenting the next line.
   # remove-item -path c:\~BT -recurse -force
   start-service wuauserv
   ```

## <a name="next-steps"></a>Další kroky
[Příprava na správu aktualizací softwaru](../get-started/prepare-for-software-updates-management.md)
