---
title: Konfigurace bodu aktualizace softwaru pro použití protokolu TLS/SSL s kurzem certifikátu PKI
titleSuffix: Configuration Manager
description: Kurz – konfigurace serverů Windows Server Update Services (WSUS) a bodů aktualizace softwaru pro použití protokolu TLS/SSL s certifikátem PKI.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/16/2020
ms.topic: tutorial
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: bd9989b8-ccaf-4d51-8262-b4a99b600d12
ms.openlocfilehash: e8359077ac363d2d732b2ffa6712c9b938a2c709
ms.sourcegitcommit: 6176a7825d6c663faa318a6818b7764bc70f08fc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/17/2020
ms.locfileid: "90718958"
---
# <a name="tutorial-configure-a-software-update-point-to-use-tlsssl-with-a-pki-certificate"></a>Kurz: konfigurace bodu aktualizace softwaru pro použití TLS/SSL s certifikátem PKI

*Platí pro: Configuration Manager (Current Branch)*

Konfigurace serverů Windows Server Update Services (WSUS) a jejich odpovídajících bodů aktualizace softwaru (SUP) k používání protokolu TLS/SSL může snížit schopnost potenciálně útočníka vzdáleně napadnout klienta a zvýšit oprávnění. Aby bylo zajištěno, že jsou zavedeny nejlepší protokoly zabezpečení, důrazně doporučujeme používat protokol TLS/SSL k zabezpečení vaší infrastruktury aktualizace softwaru. Tento článek vás provede kroky potřebnými ke konfiguraci každého serveru WSUS a bodu aktualizace softwaru pro použití protokolu HTTPS. Další informace o zabezpečení služby WSUS najdete v článku [Zabezpečená služba WSUS pomocí SSL (Secure Sockets Layer) protokolu](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) v dokumentaci ke službě WSUS.

V tomto kurzu provedete následující:
> [!div class="checklist"]
> * V případě potřeby obstarejte certifikát PKI
> * Připojte certifikát k webu správy služby WSUS.
> * Nakonfigurujte webové služby WSUS tak, aby vyžadovaly protokol SSL.
> * Konfigurace aplikace WSUS pro použití protokolu SSL
> * Ověřte, že připojení konzoly WSUS může používat protokol SSL.
> * Nakonfigurujte bod aktualizace softwaru tak, aby vyžadoval komunikaci SSL se serverem WSUS.
> * Ověření funkčnosti pomocí Configuration Manager

## <a name="considerations-and-limitations"></a>Důležité informace a omezení

Služba WSUS používá protokol TLS/SSL k ověřování klientských počítačů a serverů WSUS pro příjem dat na nadřazený server WSUS. Služba WSUS používá k šifrování metadat aktualizace taky protokol TLS/SSL. Služba WSUS pro soubory obsahu aktualizace nepoužívá protokol TLS/SSL. Soubory obsahu jsou podepsané a hodnota hash souboru je obsažena v metadatech aktualizace. Předtím, než se soubory stáhnou a nainstalují klientem, se kontroluje jak digitální podpis, tak i hodnota hash. Pokud se některá z těchto kontrol nezdařila, aktualizace se nenainstaluje.

Při použití TLS/SSL při zabezpečení nasazení WSUS Vezměte v úvahu následující omezení:

- Používání protokolu TLS/SSL zvyšuje zatížení serveru. Měli byste očekávat malou ztrátu výkonu při šifrování všech metadat, která se odesílají přes síť.
- Pokud používáte službu WSUS se vzdálenou službou SQL Server Database, připojení mezi serverem WSUS a databázovým serverem není zabezpečeno protokolem TLS/SSL. Pokud je nutné připojení k databázi zabezpečit, vezměte v úvahu následující doporučení:
   - Přesuňte databázi WSUS na server WSUS.
   - Přesuňte vzdálený databázový server a server WSUS do privátní sítě.
   - Nasaďte protokol IPsec (Internet Protocol security), který zvýší zabezpečení síťového provozu.

Při konfiguraci serverů WSUS a jejich bodů aktualizace softwaru, aby používaly protokol TLS/SSL, můžete chtít fáze změny pro velké Configuration Manager hierarchie. Pokud se v těchto změnách rozhodnete ke fázím, začněte v dolní části hierarchie a pohybujte směrem nahoru s lokalitou centrální správy.

## <a name="prerequisites"></a>Požadavky

Tento kurz se zabývá Nejběžnější metodou získání certifikátu pro použití s Internetová informační služba (IIS). Bez ohledu na to, jakou metodu vaše organizace používá, se ujistěte, že certifikát splňuje [požadavky na certifikát PKI](../../core/plan-design/network/pki-certificate-requirements.md) pro Configuration Manager bod aktualizace softwaru. Stejně jako u všech certifikátů musí být certifikační autorita důvěryhodná zařízeními komunikujícími se serverem WSUS.

- Server služby WSUS s nainstalovanou rolí bodu aktualizace softwaru
- Před povolením protokolu TLS/SSL ověřte, že jste postupovali podle [osvědčených postupů](/troubleshoot/mem/configmgr/windows-server-update-services-best-practices#disable-recycling-and-configure-memory-limits) pro zakázání recyklace a konfiguraci limitů paměti pro službu WSUS.
- Jedna z následujících dvou možností:
   - Příslušný certifikát PKI již v **osobním** úložišti certifikátů serveru WSUS.
   - Možnost vyžádat si a získat příslušný certifikát PKI pro server WSUS od kořenové certifikační autority (CA) vaší organizace.
      - Ve výchozím nastavení většina šablon certifikátů, včetně šablony certifikátu serveru webserver, bude mít problémy jenom správcům domén. Pokud se přihlášený uživatel nejedná o správce domény, musí být jeho uživatelskému účtu udělené oprávnění k **zápisu** v šabloně certifikátu.

## <a name="obtain-the-certificate-from-the-ca-if-needed"></a><a name="bkmk_pki"></a> V případě potřeby Získejte certifikát od certifikační autority.

Pokud už máte příslušný certifikát v úložišti **osobních** certifikátů serveru WSUS, přeskočte tuto část a začněte s částkou [vytvoření vazby certifikátu](#bkmk_bind) . Pokud chcete odeslat žádost o certifikát do vaší interní certifikační autority pro instalaci nového certifikátu, postupujte podle pokynů v této části.
 
1. Na serveru WSUS otevřete příkazový řádek pro správu a spusťte příkaz `certlm.msc` . Aby bylo možné spravovat certifikáty pro místní počítač, musí být váš uživatelský účet místním správcem.

   Zobrazí se nástroj Správce certifikátů pro místní zařízení.

1. Rozbalte položku **osobní**a potom klikněte pravým tlačítkem na **certifikáty**.
1. Vyberte **všechny úlohy** a pak **požádejte o nový certifikát**.
1. Kliknutím na tlačítko **Další** zahajte zápis certifikátu.
1. Vyberte typ certifikátu, který chcete zaregistrovat. Účelem certifikátu je **ověřování serveru** a šablona certifikátu společnosti Microsoft, která se má použít, je **webový server** nebo vlastní šablona, která má **ověřování serveru** zadáno jako **rozšířené použití klíče**. Může se zobrazit výzva k zadání dalších informací k registraci certifikátu. Obvykle zadáte minimálně tyto informace:
   - **Běžný název:** Nachází se na kartě **subjekt** , nastavte hodnotu na plně kvalifikovaný název domény serveru WSUS.
   - **Popisný název:** Na kartě **Obecné** nastavte hodnotu na popisný název, abyste mohli certifikát později identifikovat.
:::image type="content" source="media/certificate-properties.png" alt-text="Okno vlastností certifikátu pro určení dalších informací pro registraci":::
1. **Kliknutím na** **Registrovat** dokončete registraci.
1. Otevřete certifikát, pokud chcete zobrazit podrobnosti, jako je například kryptografický otisk certifikátu.

> [!TIP]
> Pokud je server WSUS internetový, budete potřebovat externí plně kvalifikovaný název domény v předmětu nebo alternativním názvu subjektu (SAN) ve vašem certifikátu.

## <a name="bind-the-certificate-to-the-wsus-administration-site"></a><a name="bkmk_bind"></a> Navažte certifikát na web správy služby WSUS.

Jakmile máte certifikát v úložišti osobních certifikátů serveru WSUS, připojte jej k webu správy služby WSUS ve službě IIS.

1. Na serveru služby WSUS otevřete správce služby Internet Information Services (IIS).
1. Přejít na **lokality**  >  **Správa služby WSUS**.
1. V nabídce Akce nebo kliknutím pravým tlačítkem myši na webu vyberte **vazby** .
1. V okně **vazby webu** vyberte řádek pro **https**a pak vyberte **Upravit...**.
   - Neodstraňujte vazbu webu HTTP. Služba WSUS používá pro soubory obsahu aktualizace protokol HTTP.
1. V části **certifikát SSL** vyberte certifikát, který chcete vytvořit pro web správy služby WSUS. V rozevírací nabídce se zobrazí popisný název certifikátu. Pokud není zadaný popisný název, `IssuedTo` zobrazí se pole certifikátu. Pokud si nejste jisti, který certifikát se má použít, vyberte **Zobrazit** a ověřte, jestli se kryptografický otisk shoduje s vámi získanou.  
   :::image type="content" source="media/edit-site-binding.png" alt-text="Upravit okno vazby webu pomocí výběru certifikátu SSL":::
1. Až skončíte, vyberte **OK** a pak **zavřete** , aby se vazby lokality ukončily. Správce služby Internetová informační služba (IIS) zůstane otevřený pro další kroky.



## <a name="configure-the-wsus-web-services-to-require-ssl"></a><a name="bkmk_webserv"></a> Nakonfigurujte webové služby WSUS tak, aby vyžadovaly protokol SSL.

1. Ve Správci služby IIS na serveru WSUS klikněte na **lokality**  >  **Správa služby WSUS**.
1. Rozbalte web správy služby WSUS, abyste viděli seznam webových služeb a virtuálních adresářů pro službu WSUS.
1. Pro každou z následujících webových služeb WSUS:
   - ApiRemoting30
   - ClientWebService
   - DSSAuthWebService
   - ServerSyncWebService
   - SimpleAuthWebService

   Proveďte následující změny:

      1. Vyberte **Nastavení SSL**.
      1. Povolte možnost **vyžadovat protokol SSL** .
      1. Ověřte, jestli je možnost **klientské certifikáty** nastavená na **Ignorovat**.
      1. Vyberte **Použít**.

Neinstalujte nastavení SSL na nejvyšší úrovni lokality pro správu služby WSUS, protože některé funkce, například obsah, potřebují používat protokol HTTP.

## <a name="configure-the-wsus-application-to-use-ssl"></a><a name="bkmk_wsusutil"></a> Konfigurace aplikace WSUS pro použití protokolu SSL

Jakmile budou webové služby nastaveny tak, aby vyžadovaly protokol SSL, musí být aplikace WSUS upozorněna, aby mohla provést nějakou další konfiguraci pro podporu změny.

1. Otevřete příkazový řádek správce na serveru WSUS. Uživatelský účet, který spouští tento příkaz, musí být členem skupiny Správci služby WSUS nebo místní skupiny Administrators.
1. Změňte adresář na složku Tools pro službu WSUS:  
   `cd "c:\Program Files\Update Services\Tools"`
1. Nakonfigurujte službu WSUS tak, aby používala protokol SSL, s následujícím příkazem:

    `WsusUtil.exe configuressl server.contoso.com`
   
   Kde *Server.contoso.com* je plně kvalifikovaný název domény serveru WSUS.
1. WsusUtil vrátí adresu URL serveru WSUS s číslem portu zadaným na konci. Port bude buď 8531 (výchozí), nebo 443. Ověřte, že vrácená adresa URL je to, co jste očekávali. Pokud něco nebylo naproti nějakému typu, můžete znovu spustit příkaz.

   :::image type="content" source="media/wsusutil.png" alt-text="Příkaz WSUSutil configuressl vracející adresu URL HTTPS pro službu WSUS":::

> [!TIP] 
> Pokud je server WSUS na internetu, zadejte při běhu externí plně kvalifikovaný název domény `WsusUtil.exe configuressl` .

## <a name="verify-the-wsus-console-can-connect-using-ssl"></a><a name="bkmk_wsus_console"></a> Ověření, že se konzola WSUS může připojit pomocí protokolu SSL

Konzola WSUS používá pro připojení webovou službu ApiRemoting30. Configuration Manager bod aktualizace softwaru (SUP) taky používá stejnou webovou službu k přímému směrování WSUS, aby provedl určité akce, jako například:

- Zahájení synchronizace aktualizace softwaru
- Nastavení správného nadřazeného serveru pro službu WSUS, který závisí na tom, kde se lokalita SUP nachází ve vaší Configuration Manager hierarchii
- Přidávání nebo odebírání produktů a klasifikací pro synchronizaci ze serveru WSUS na nejvyšší úrovni hierarchie.
- Odebírají se aktualizace s vypršenou platností

Otevřete konzolu služby WSUS a ověřte, zda můžete použít připojení SSL k webové službě ApiRemoting30 serveru WSUS. Některé další webové služby budeme testovat později.

1. Otevřete konzolu WSUS a vyberte **Akce**  >  **připojit k serveru**.
1. Pro možnost **název serveru** zadejte plně kvalifikovaný název domény serveru WSUS.
1. Vyberte **číslo portu** vrácené v adrese URL z WSUSutil.
1. Možnost **použít SSL (Secure Sockets Layer) (SSL) pro připojení k tomuto serveru** automaticky povolí, když zvolíte buď 8531 (výchozí), nebo 443.
       :::image type="content" source="media/connect-wsus-console.png" alt-text="Připojte se ke konzole služby WSUS přes port HTTPS.":::
1. Pokud je server lokality Configuration Manager vzdálený z bodu aktualizace softwaru, spusťte konzolu služby WSUS ze serveru lokality a ověřte, zda se Konzola služby WSUS může připojit přes protokol SSL.
   - Pokud se Vzdálená konzola služby WSUS nemůže připojit, může to vést k potížím s důvěryhodným certifikátem, překladem názvů nebo blokovaným portem.

## <a name="configure-the-software-update-point-to-require-ssl-communication-to-the-wsus-server"></a><a name="bkmk_cm_sup"></a> Nakonfigurujte bod aktualizace softwaru tak, aby vyžadoval komunikaci SSL se serverem WSUS.

Jakmile je služba WSUS nastavená tak, aby používala protokol TLS/SSL, budete muset aktualizovat odpovídající Configuration Manager bod aktualizace softwaru tak, aby vyžadoval i protokol SSL. Po provedení této změny bude Configuration Manager:

- Ověřte, že může server WSUS pro bod aktualizace softwaru nakonfigurovat.
- Přímé klienty, aby používali port SSL, když mají pokyn ke kontrole na tomto serveru WSUS.

Chcete-li nakonfigurovat bod aktualizace softwaru tak, aby vyžadoval komunikaci SSL se serverem služby WSUS, proveďte následující kroky: 

1. Otevřete konzolu Configuration Manager a připojte se buď k lokalitě centrální správy, nebo k serveru primární lokality pro bod aktualizace softwaru, který chcete upravit.
1. Přejít na **Administration**  >  **Přehled**správy  >  **Konfigurace**  >  **servery lokality a role systému lokality**.
1. Vyberte server systému lokality, kde je služba WSUS nainstalována, a pak vyberte roli systému lokality bodu aktualizace softwaru.
1. Na pásu karet vyberte možnost **vlastnosti**.
1. Povolte možnost **vyžadovat komunikaci SSL s možností serveru služby WSUS** .

   :::image type="content" source="media/sup-properties.png" alt-text="Vlastnosti SUP ukazující možnost vyžadovat komunikaci SSL se serverem WSUS":::
1. V [**WCM. log**](../../core/plan-design/hierarchy/log-files.md#BKMK_SUPLog) pro lokalitu se při uplatnění změny zobrazí následující položky:

   ```
   SCF change notification triggered.
   Populating config from SCF
   Setting new configuration state to 1 (WSUS_CONFIG_PENDING)
   ...
   Attempting connection to local WSUS server
   Successfully connected to local WSUS server
   ...
   Setting new configuration state to 2 (WSUS_CONFIG_SUCCESS)
   ```

Příklady souborů protokolu byly upraveny pro odebrání nepotřebných informací v tomto scénáři.  

## <a name="verify-functionality-with-configuration-manager"></a><a name="bkmk_cm_verify"></a> Ověření funkčnosti pomocí Configuration Manager

### <a name="verify-the-site-server-can-sync-updates"></a>Ověření, zda může server lokality synchronizovat aktualizace

1. Připojte konzolu Configuration Manager k lokalitě nejvyšší úrovně.
1. Přejít na přehled softwarových **knihoven**  >  **Overview**  >  **aktualizace softwaru**  >  **všechny aktualizace softwaru**.
1. Na pásu karet vyberte možnost **synchronizovat aktualizace softwaru**.
1. Vyberte **Ano** pro oznámení s dotazem, zda chcete zahájit synchronizaci v rámci lokality pro aktualizace softwaru.
   - Vzhledem k tomu, že se konfigurace služby WSUS změnila, proběhne úplná synchronizace aktualizací softwaru, nikoli rozdílová synchronizace.
1. Otevřete **souboru wsyncmgr. log** pro lokalitu. Pokud sledujete podřízenou lokalitu, budete muset počkat, než se nejdřív Nadřazená lokalita dokončí synchronizace. Ověřte, že se server úspěšně synchronizuje, a to tak, že zkontroluje protokol pro položky podobné následujícímu:

   ```
   Starting Sync
   ...
   Full sync required due to changes in main WSUS server location.
   ...
   Found active SUP SERVER.CONTOSO.COM from SCF File.
   ...
   https://SERVER.CONTOSO.COM:8531
   ...
   Done synchronizing WSUS Server SERVER.CONTOSO.COM
   ...
   sync: Starting SMS database synchronization
   ...
   Done synchronizing SMS with WSUS Server SERVER.CONTOSO.COM
   ```

### <a name="verify-a-client-can-scan-for-updates"></a>Ověření, že klient může vyhledat aktualizace

Změníte-li bod aktualizace softwaru tak, aby vyžadoval protokol SSL, Configuration Manager klienti obdrží aktualizovanou adresu URL služby WSUS, když se v něm vytvoří žádost o umístění bodu aktualizace softwaru. Otestováním klienta můžeme:
-  Určete, zda klient důvěřuje certifikátu serveru WSUS. 
- Pokud jsou funkce SimpleAuthWebService a ClientWebService pro službu WSUS funkční.
-  Zda je virtuální adresář obsahu služby WSUS funkční a v případě, že klientovi došlo k získání smlouvy EULA během kontroly

1. Identifikujte klienta, který v nedávné době změnil použití protokolu TLS/SSL v bodu aktualizace softwaru. Pokud potřebujete pomáhat s určením klienta, použijte [skripty spouštěné](../..//apps/deploy-use/create-deploy-scripts.md) pod skriptem prostředí PowerShell:

   ```powershell
   $Last = (Get-CIMInstance -Namespace "root\CCM\Scanagent" -Class "CCM_SUPLocationList").LastSuccessScanPath
   $Current= Write-Output (Get-CIMInstance -Namespace "root\CCM\Scanagent" -Class "CCM_SUPLocationList").CurrentScanPath
   Write-Host "LastGoodSUP- $last"
   Write-Host "CurrentSUP- $current"
   ```

1. Spusťte v testovacím klientovi cyklus prověřování aktualizací softwaru. Kontrolu můžete vynutit pomocí následujícího skriptu prostředí PowerShell:

   ```powershell
   Invoke-WMIMethod -Namespace root\ccm -Class SMS_CLIENT -Name TriggerSchedule "{00000000-0000-0000-0000-000000000113}"
   ```

1. Zkontrolujte, zda byla přijata zpráva pro kontrolu proti bodu aktualizace softwaru v **ScanAgent. log** klienta.

   ```
   Message received: '<?xml version='1.0' ?>
   <UpdateSourceMessage MessageType='ScanByUpdateSource'>
      <ForceScan>TRUE</ForceScan>
      <UpdateSourceIDs>
            <ID>{A1B2C3D4-1234-1234-A1B2-A1B2C3D41234}</ID>
      </UpdateSourceIDs>
    </UpdateSourceMessage>'
   ```

1. Zkontrolujte **protokol LocationServices. log** a ověřte, zda klient vidí správnou adresu URL služby WSUS.
**LocationServices.log**
   ```
   WSUSLocationReply : <WSUSLocationReply SchemaVersion="1
   ...
   <LocationRecord WSUSURL="https://SERVER.CONTOSO.COM:8531" ServerName="SERVER.CONTOSO.COM"
   ...
   </WSUSLocationReply>
   ```

1. Zkontrolujte **protokol WUAHandler. log** a ověřte, zda se může klient úspěšně prohledávat.

   ```
   Enabling WUA Managed server policy to use server: https://SERVER.CONTOSO.COM:8531
   ...
   Successfully completed scan.
   ```

## <a name="next-steps"></a>Další kroky

[Nasazení aktualizací softwaru](../deploy-use/deploy-software-updates.md)