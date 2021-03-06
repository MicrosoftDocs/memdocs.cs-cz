---
title: Poznámky k verzi
titleSuffix: Configuration Manager
description: Seznamte se s naléhavými problémy, které zatím nejsou v produktu opravené nebo jsou uvedené v článku znalostní báze podpora Microsoftu Knowledge Base.
ms.date: 08/17/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: troubleshooting
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a29c165e13e82144d7fea767ca719a0c84c88023
ms.sourcegitcommit: da5bfbe16856fdbfadc40b3797840e0b5110d97d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/18/2020
ms.locfileid: "88512644"
---
# <a name="release-notes-for-configuration-manager"></a>Poznámky k verzi pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

S Configuration Manager jsou poznámky k verzi produktu omezené na naléhavé problémy. Tyto problémy ještě nejsou v produktu opravené, nebo se podrobně popisuje podpora Microsoftu znalostní báze Knowledge Base.  

Dokumentace ke konkrétním funkcím obsahuje informace o známých problémech, které mají vliv na základní scénáře.  

Tento článek obsahuje poznámky k verzi pro aktuální větev Configuration Manager. Informace o větvi Technical Preview najdete v tématu [Technical Preview](../../../get-started/technical-preview.md) .  

Informace o nových funkcích zavedených s různými verzemi najdete v následujících článcích:

- [Novinky ve verzi 2006](../../../plan-design/changes/whats-new-in-version-2006.md)
- [Novinky ve verzi 2002](../../../plan-design/changes/whats-new-in-version-2002.md)
- [Novinky ve verzi 1910](../../../plan-design/changes/whats-new-in-version-1910.md)
- [Novinky ve verzi 1906](../../../plan-design/changes/whats-new-in-version-1906.md)  

Informace o nových funkcích v Desktop Analytics najdete v tématu [co je nového v rámci služby Desktop Analytics](../../../../desktop-analytics/whats-new.md).

> [!Tip]  
> Pokud chcete dostávat upozornění na aktualizaci této stránky, zkopírujte a vložte následující adresu URL do čtečky informačních kanálů RSS: `https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`

## <a name="set-up-and-upgrade"></a>Nastavení a upgrade  

### <a name="client-automatic-upgrade-happens-immediately-for-all-clients"></a>Automatický upgrade klienta proběhne okamžitě pro všechny klienty.

<!-- 6040412 -->

*Platí pro verzi 1910*

Pokud vaše lokalita používá [Automatický upgrade klienta](../../../clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade), při aktualizaci lokality na verzi 1910 budou všichni klienti hned po úspěšném dokončení aktualizace lokality okamžitě upgradováni. Jedinou náhodou je, že klienti obdrží zásadu, která je ve výchozím nastavení každou hodinu. U velkých webů s mnoha klienty může toto chování spotřebovat značné množství síťových přenosů a zátěžových distribučních bodů.

Další informace o ovlivněných verzích najdete v tématu [aktualizace klienta pro Configuration Manager aktuální větev verze 1910](https://support.microsoft.com/help/4538166).

### <a name="site-server-in-passive-mode-doesnt-update-configurationmof"></a>Server lokality v pasivním režimu neaktualizuje soubor Configuration. mof.

<!-- 5787848 -->

*Platí pro verzi 1910*

Pokud vaše lokalita obsahuje [Server lokality v pasivním režimu](../configure/site-server-high-availability.md), může při aktualizaci lokality dojít ke ztrátě vlastního nastavení inventáře. Lokalita při převzetí služeb při selhání serverem lokality v současné době nesynchronizuje soubor Configuration. mof.

Pokud chcete tento problém obejít, ručně zálohujte a obnovte soubor Configuration. mof lokality.

### <a name="setup-prerequisite-warning-on-domain-functional-level-on-server-2019"></a>Nastavení upozornění na požadavky na úroveň funkčnosti domény na serveru 2019

<!-- 4904376 -->

*Platí pro verzi 1906*

Při instalaci aktualizace pro verzi 1906 v prostředí s řadiči domény se systémem Windows Server 2019 vrátí Kontrola požadavků pro úroveň funkčnosti domény následující upozornění:

`[Completed with warning]:Verify that the Active Directory domain functional level is Windows Server 2003 or later`

Pokud chcete tento problém obejít, ignorujte upozornění.

### <a name="azure-ad-user-discovery-and-collection-group-sync-dont-work-after-site-expansion"></a>Po rozšíření lokality nefunguje služba zjišťování uživatelů Azure AD a synchronizace skupiny kolekcí.

<!-- 4797313 -->
*Platí pro verzi 1906*

Po nakonfigurování některé z následujících funkcí:

- Azure Active Directory zjišťování skupiny uživatelů
- Synchronizace výsledků členství kolekce do skupin Azure Active Directory

Pokud následně rozbalíte samostatnou primární lokalitu do hierarchie s lokalitou centrální správy, zobrazí se v SMS_AZUREAD_DISCOVERY_AGENT. log následující chyba:

`Could not obtain application secret for tenant xxxxx. If this is after a site expansion, please run "Renew Secret Key" from admin console.`

Pokud chcete tento problém obejít, obnovte klíč přidružený k registraci aplikace ve službě Azure AD. Další informace najdete v tématu [obnovení tajného klíče](../configure/azure-services-wizard.md#bkmk_renew).

## <a name="role-based-administration"></a>Správa na základě rolí

### <a name="security-scopes-for-certain-folders-dont-replicate-from-cas-to-primary-sites"></a>Obory zabezpečení pro určité složky se nereplikují z CAS do primárních lokalit.
<!--6306759-->
*Platí pro verzi 1910*

Po upgradu na verzi 1910 se [obory zabezpečení pro složky](../configure/configure-role-based-administration.md#bkmk_config-folder) v kolekcích uživatelů a kolekcích zařízení nereplikují z certifikačních autorit do primárních lokalit.

## <a name="application-management"></a>Správa aplikací

### <a name="unable-to-get-certificate-for-powershell-error-when-deploying-microsoft-edge-version-77-and-later"></a>Nepovedlo se získat certifikát pro chybu PowerShellu při nasazování Microsoft Edge, verze 77 a novější.
<!--5769384-->
*Platí pro: Configuration Manager verze 1910*

Pokud používáte konzolu Configuration Manager v operačním systému, ve kterém je jazyk švédštiny, maďarštiny nebo japonštiny, při nasazení Microsoft Edge verze 77 a novější se zobrazí následující chyba:

`Unable to get certificate for Powershell`

K této chybě dochází `scripts` , protože složka v adresáři neexistuje `AdminConsole\bin` pro švédské, maďarské nebo japonské jazyky. Složka skripty je lokalizována do těchto jazyků operačního systému.

Pokud chcete tento problém obejít, vytvořte složku `scripts` s názvem v `AdminConsole\bin` adresáři. Zkopírujte soubory z lokalizované složky do nově vytvořené `scripts` složky. Po zkopírování souborů nasaďte Microsoft Edge verze 77 a novější.

## <a name="os-deployment"></a>Nasazení operačního systému

### <a name="client-policy-error-when-you-deploy-a-task-sequence"></a>Chyba zásad klienta při nasazení pořadí úloh

<!-- 7970134 -->

*Platí pro: Configuration Manager verze 2006 časné aktualizace Ring*

Když nasadíte pořadí úkolů do klienta, požadovaná sekvence úloh se v konečném termínu nenainstaluje a v centru softwaru se nezobrazí dostupné pořadí úloh. Zobrazí se stavová zpráva 10803 s popisem podobným této chybové zprávě:

*Klientovi se nepovedlo stáhnout zásady. Služba přenosu dat vrátila chybu BITS: odpověď serveru nebyla platná. Server nenásleduje za definovaným protokolem. (-2145386469).*

K tomuto problému dochází, když nakonfigurujete bod správy pro protokol HTTPS a zařízení používá Configuration Manager klienta verze 1906 nebo starší.

Pokud chcete tento problém obejít, aktualizujte klienta Configuration Manager na zařízení na verzi 1910 nebo novější.

### <a name="task-sequences-cant-run-over-cmg"></a>Pořadí úloh nejde spustit přes CMG.

*Platí pro: Configuration Manager verze 2002*

V zařízení, které komunikuje přes bránu pro správu cloudu (CMG), existují dvě instance, ve kterých se pořadí úkolů nedají spustit:

- Nakonfigurujete lokalitu pro rozšířený protokol HTTP a bod správy je HTTP.<!-- 6358851 -->

    Pokud chcete tento problém obejít, aktualizujte na verzi 2006. Případně nakonfigurujte bod správy pro protokol HTTPS.

- Nainstalovali jste a zaregistrovali klienta s hromadnou registračním tokenem pro ověřování.<!-- 6377921 -->

    Pokud chcete tento problém obejít, aktualizujte na verzi 2006. Případně použijte jednu z následujících metod ověřování:

  - Předem zaregistrujte zařízení v interní síti.
  - Konfigurace zařízení pomocí certifikátu pro ověřování klientů
  - Připojení zařízení k Azure AD

## <a name="software-updates"></a>Aktualizace softwaru

### <a name="security-roles-are-missing-for-phased-deployments"></a>Pro dvoufázové nasazení chybí role zabezpečení.

<!--3479337, SCCMDocs-pr issue 3095-->
*Platí pro: Configuration Manager verze 1810, 1902*

Integrovaná role zabezpečení **OS Deployment Manager** má oprávnění k [dvoufázovému nasazení](../../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md). V následujících rolích chybí tato oprávnění:  

- **Správce aplikace**  
- **Správce nasazení aplikací**  
- **Správce aktualizací softwaru**  

Role **autora aplikace** se může zdát, že má některá oprávnění k dvoufázovému nasazení, ale neměla by být schopná vytvářet nasazení.

Uživatel s jednou z těchto rolí může spustit Průvodce vytvořením postupného nasazení a může zobrazit postupná nasazení pro aplikaci nebo aktualizaci softwaru. Nemůžou dokončit průvodce ani dělat změny v existujícím nasazení.

Pokud chcete tento problém obejít, vytvořte vlastní roli zabezpečení. Zkopírujte existující roli zabezpečení a přidejte do třídy objektu **postupného nasazení** následující oprávnění:

- Vytvořit  
- Odstranit  
- Modify  
- Číst  

Další informace najdete v tématu [Vytvoření vlastních rolí zabezpečení](../configure/configure-role-based-administration.md#BKMK_CreateSecRole) .

## <a name="desktop-analytics"></a>Desktop Analytics

### <a name="an-extended-security-update-for-windows-7-causes-them-to-show-as-unable-to-enroll"></a><a name="dawin7-diagtrack"></a>Rozšířená aktualizace zabezpečení pro systém Windows 7 způsobí, že se můžou zobrazit jako **neregistrované** .

<!-- 7283186 -->
_Platí pro: Configuration Manager verze 2002 a starší_

Aktualizace rozšířeného zabezpečení z dubna 2020 (EVJ) pro systém Windows 7 změnila minimální požadovanou verzi diagtrack.dll z 10586 na 10240. Tato změna způsobí, že se zařízení se systémem Windows 7 zobrazují jako **neschopná se zaregistrovat** na řídicím panelu **stavu připojení** Desktop Analytics. Když přejdete do zobrazení zařízení pro tento stav, vlastnost **Konfigurace služby DiagTrack** zobrazí následující stav: `Connected User Experience and Telemetry (diagtrack.dll) component is outdated. Check requirements.`

Pro tento problém není nutné žádné alternativní řešení. Odinstalujte EVJ. dubna. Pokud je v opačném případě správně nakonfigurovaná, zařízení s Windows 7 pořád hlásí diagnostická data do služby Desktop Analytics a pořád se na portálu zobrazují.

### <a name="if-you-use-hardware-inventory-for-distributed-views-you-cant-onboard-to-desktop-analytics"></a>Pokud používáte inventář hardwaru pro distribuovaná zobrazení, nemůžete se připojit k desktopovým analýzám.

<!-- 4950335 -->
*Platí pro: Configuration Manager verze 1902 s kumulativní aktualizací a verze 1906*

Pokud máte hierarchii a povolíte data lokality **inventáře hardwaru** pro [distribuovaná zobrazení](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) na jakýchkoli odkazech na replikaci na základě konfigurace připojení k ploše v Configuration Manager zobrazí se v M365UploadWorker. log následující chyba:

`Unexpected exception 'System.Data.SqlClient.SqlException' Remote access is not supported for transaction isolation level "SNAPSHOT".:    at System.Data.SqlClient.SqlConnection.OnError(SqlException exception, Boolean breakConnection, Action'1 wrapCloseInAction)`

Pokud chcete tento problém obejít, zakažte data lokality **inventáře hardwaru** pro distribuovaná zobrazení na všech odkazech replikace lokality.

### <a name="console-unexpectedly-closes-when-removing-collections"></a>Konzola se neočekávaně zavře při odebírání kolekcí.

<!-- 4749443 -->
*Platí pro: Configuration Manager verze 1902 s kumulativní aktualizací*

Po připojení lokality k [Desktop Analytics](../../../../desktop-analytics/connect-configmgr.md)můžete **vybrat konkrétní kolekce, které se budou synchronizovat s desktopovou analýzou**. Odeberete-li kolekci a použijete změny, okamžitě přidáním nové kolekce dojde k neošetřené výjimce. Konzola se neočekávaně zavře.

Pokud chcete tento problém obejít, při odebírání kolekce vyberte **OK** , čímž zavřete okno Vlastnosti. Pak znovu otevřete vlastnosti a přidejte novou kolekci na kartě připojení k **Desktop Analytics** .

### <a name="pilot-status-tile-shows-some-devices-as-undefined"></a>Dlaždice stavu pilotu zobrazuje některá zařízení jako nedefinované

<!-- 4547783 -->
*Platí pro: Configuration Manager verze 1902 s kumulativní aktualizací*

Když použijete konzolu Configuration Manager k monitorování stavu nasazení pilotního projektu, na dlaždici stav pilota se zobrazí jako **nedefinované** v cílové verzi Windows pro tento plán nasazení.  

Tato **nedefinovaná** zařízení jsou **aktuální** s cílovou verzí operačního systému pro daný plán nasazení. Není nutná žádná další akce.

## <a name="cloud-services"></a>Cloud Services

### <a name="azure-service-for-us-government-cloud-shows-as-public-cloud"></a>Služba Azure pro státní správu USA předvádí veřejné cloudy.

<!-- 6036748 -->

*Platí pro verzi 1910*

Pokud vytvoříte připojení ke službě Azure a nastavíte **prostředí Azure** na Cloud pro státní správu, vlastnosti připojení zobrazí prostředí jako veřejný cloud Azure. Tento problém je jenom problém se zobrazením v konzole, ale služba je v cloudu pro státní správu. Chcete-li konfiguraci potvrdit, spusťte následující dotaz SQL v databázi lokality:

```SQL
Select Environment, Name, TenantID From AAD_Tenant_Ex
```

V případě cloudu pro státní správu je výsledek tohoto dotazu `2` určený pro konkrétního tenanta.

### <a name="cant-download-content-from-a-cloud-management-gateway-enabled-for-tls-12"></a>Nejde stáhnout obsah z brány pro správu cloudu, která je povolená pro TLS 1,2.

<!-- 5771680 -->

*Platí pro verzi 1906, 1910 na začátku aktualizačního kruhu*

Pokud povolíte bránu pro správu cloudu (CMG), aby **fungovala jako distribuční bod cloudu a poskytovala obsah z Azure Storage** a **vynutila TLS 1,2**, může se stát, že stahování obsahu selže.

V DataTransferService. log v klientovi se zobrazí následující chyby:

``` log
Request to https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04 failed with 400
Successfully queued event on HTTP/HTTPS failure for server 'cmg1.contoso.com'.
Error sending DAV request. HTTP code 400, status 'Bad Request'
GetDirectoryList_HTTP('https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04') failed with code 0x87d0027e.
Error retrieving manifest (0x87d0027e).
```

V protokolu CMGContentService. log na serveru se zobrazují následující chyby:

``` log
ERROR: Exception processing request. Microsoft.WindowsAzure.Storage.StorageException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.ComponentModel.Win32Exception: The client and server cannot communicate, because they do not possess a common algorithm...
```

Náhradní řešení tohoto problému:

- Aktualizujte lokalitu na globálně dostupnou verzi 1910, která byla vydána 20. prosince 2019. (Pokud jste se dříve aktualizovali na okruh 1910 brzké aktualizace, je potřeba aktualizovat na toto sestavení, až bude k dispozici.)

- Případně použijte tradiční [distribuční bod cloudu](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md). Tato role nevynutila TLS 1,2, ale je kompatibilní s klienty, kteří vyžadují TLS 1,2.

## <a name="protection"></a>Ochrana

### <a name="bitlocker-management-appears-in-version-1906"></a>Správa nástroje BitLocker se zobrazuje ve verzi 1906.

*Platí pro verzi 1906*

<!-- 5984688 -->

Pokud po 21. listopadu 2019 aktualizujete na verzi 1906 z verze 1902 nebo starší, bude funkce správy nástroje BitLocker zapnutá a dostupná. Tato funkce je volitelnou funkcí počínaje verzí 1910. Nepodporovaná ve verzi 1906. Pokud se ho pokusíte použít ve verzi 1906, může docházet k neočekávaným výsledkům. Pokud tuto funkci nepoužíváte, nebude to mít žádný vliv.

Chcete-li použít [funkci správy BitLockeru](../../../../protect/plan-design/bitlocker-management.md), aktualizujte na verzi 1910.

<!--
## Backup and recovery

## Client deployment and upgrade
-->
