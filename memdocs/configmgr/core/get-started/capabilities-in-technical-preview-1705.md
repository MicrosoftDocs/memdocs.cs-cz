---
title: Technical Preview 1705
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview verze 1705 pro Configuration Manager.
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 00684289-d21a-45f8-b1e3-c5c787d73096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 06119bfc096564f70922249121f63c3d2039efe8
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995445"
---
# <a name="capabilities-in-technical-preview-1705-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1705 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1705. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview. Před instalací této verze Technical Preview si přečtěte [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md) , abyste se seznámili se všeobecnými požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.    

**Známé problémy v této verzi Technical Preview:**
-   **Konektor Operations Manager Suite se neupgraduje**. Když upgradujete z předchozí verze Technical Preview, která má nakonfigurovaný konektor OMS, tento konektor se neupgraduje a už není v konzole k dispozici. Po upgradu musíte [použít Průvodce službami Azure](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) a znovu vytvořit připojení k pracovnímu prostoru OMS.
-   **Ovladače Surface se úspěšně nesynchronizují**. I když je podpora pro ovladače Surface uvedena v části **novinky** v konzole Configuration Manager pro verzi Technical Preview, tato funkce ještě nefunguje podle očekávání.
-   **Nepovedlo se vytvořit web Windows Update pro zásady odložení firmy**. I když je možnost konfigurace zásad odložení web Windows Update pro firmy uvedená v části **novinky** v konzole Configuration Manager pro verzi Technical Preview, průvodce se neotevře a nemůžete nakonfigurovat žádné zásady.


<!--  Known Issues Template
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="update-reset-tool"></a>Nástroj pro resetování aktualizací  
Můžete použít nástroj pro obnovení Configuration Manager aktualizace **CMUpdateReset.exe**a opravit problémy v případě, že aktualizace v konzole mají problémy při stahování nebo replikaci. Tento nástroj je součástí verze Technical Preview 1705. Po instalaci verze Preview do složky ***\CD.latest\SMSSETUP\TOOLS*** najdete ji na serveru lokality v lokalitě Technical Preview.

Tento nástroj můžete použít s verzí Technical Preview 1606 nebo novější. Tato zpětná podpora je k dispozici, takže nástroj lze použít s řadou scénářů aktualizace Technical Preview a bez nutnosti čekat, až bude k dispozici další verze Technical Preview.

Tento nástroj můžete použít i v případě, že konzolová aktualizace ještě není nainstalovaná a je ve stavu selhání. Stav selhání může znamenat, že stahování aktualizace zůstává v provozu, ale je zablokované a trvá příliš dlouhou dobu, například hodiny delší než historické očekávání pro aktualizační balíčky podobné velikosti. Může se také jednat o selhání při replikaci aktualizace do podřízených primárních lokalit.  

Když nástroj spustíte, spustí se s aktualizací, kterou určíte. Ve výchozím nastavení Nástroj neodstraní úspěšně nainstalované nebo stažené aktualizace.  

### <a name="prerequisites"></a>Předpoklady
Účet, který použijete ke spuštění nástroje, vyžaduje následující oprávnění:
-   Oprávnění **ke čtení** a **zápisu** do databáze lokality centrální správy a každé primární lokality ve vaší hierarchii. Chcete-li nastavit tato oprávnění, můžete přidat uživatelský účet jako člena **db_datawriter** a **db_datareader** [pevné databázové role](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) v databázi Configuration Manager jednotlivých lokalit. Nástroj nekomunikuje se sekundárními lokalitami.
-   **Místní správce** v lokalitě nejvyšší úrovně ve vaší hierarchii.
-   **Místní správce** na počítači, který je hostitelem spojovacího bodu služby.

Budete potřebovat identifikátor GUID balíčku aktualizací, který chcete obnovit. Získání identifikátoru GUID:
-   V konzole nástroje přejděte na **Správa**  >  **aktualizace a údržba** a potom v podokně zobrazení klikněte pravým tlačítkem myši na záhlaví jednoho ze sloupců (například **stav**) a pak vyberte možnost **identifikátor GUID balíčku**. Tím se tento sloupec přidá do zobrazení a ve sloupci se zobrazí identifikátor GUID balíčku aktualizace.

> [!TIP]  
> Chcete-li zkopírovat identifikátor GUID, vyberte řádek balíčku aktualizací, který chcete obnovit, a potom pomocí kombinace kláves CTRL + C tento řádek zkopírujte. Pokud vložíte zkopírovaný výběr do textového editoru, můžete zkopírovat pouze identifikátor GUID, který se použije jako parametr příkazového řádku při spuštění nástroje.

### <a name="run-the-tool"></a>Spusťte nástroj.    
Nástroj musí být spuštěn v lokalitě nejvyšší úrovně v hierarchii.

Když nástroj spustíte, použijete parametry příkazového řádku k určení SQL Server v lokalitě nejvyšší úrovně v hierarchii, názvu databáze lokality a identifikátoru GUID balíčku aktualizací, který chcete obnovit. Nástroj pak určí další servery, které potřebuje pro přístup, na základě stavu aktualizací.   

Pokud je balíček aktualizace ve stavu *po stažení* , nástroj nevyčistit balíček. Jako možnost můžete vynutit odebrání úspěšného stažení aktualizace pomocí parametru vynutit odstranění (viz parametry příkazového řádku dále v tomto tématu).

Po spuštění nástroje:
-   Pokud byl balíček odstraněn, restartujte lokality nejvyšší úrovně SMS_Executive službu a poté vyhledejte aktualizace pro opětovné stažení balíčku.
-   Pokud se balíček neodstranil, nemusíte provádět žádnou akci, protože aktualizace se znovu inicializuje a znovu spustí replikace nebo instalace.

**Parametry příkazového řádku:**  


|                        Parametr                         |                                                            Popis                                                            |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| **-S &lt; plně kvalifikovaný název domény SQL Server vaší lokality nejvyšší úrovně>** | *Požadováno* <br> Je nutné zadat plně kvalifikovaný název domény SQL Server, která je hostitelem databáze lokality pro lokalitu nejvyšší úrovně ve vaší hierarchii. |
|                **-D &lt; název databáze>**                 |                             *Požadováno* <br> Je nutné zadat název databáze lokalit na nejvyšší úrovni.                             |
|                 **-P &lt;>identifikátor GUID balíčku **                 |                        *Požadováno* <br> Je nutné zadat identifikátor GUID balíčku aktualizací, který chcete obnovit.                        |
|           **-I &lt; SQL Server název instance>**           |                   *Volitelné* <br> Použijte k identifikaci instance SQL Server, která je hostitelem databáze lokality.                   |
|                       **-FDELETE**                       |                      *Volitelné* <br> Toto použijte k vynucení odstranění úspěšně staženého balíčku aktualizace.                      |

 **Příklady:**  
 V typickém scénáři chcete obnovit aktualizaci, která má problémy se stahováním. Plně kvalifikovaný název domény SQL serveru je *Server1.fabrikam.com*, databáze lokality je *CM_XYZ*a identifikátor GUID balíčku je *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Spustíte: ***CMUpdateReset.exe-S Server1.fabrikam.com-D CM_XYZ-P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

 V extrémním scénáři chcete vynutit odstranění problematického balíčku aktualizace. Plně kvalifikovaný název domény SQL serveru je *Server1.fabrikam.com*, databáze lokality je *CM_XYZ*a identifikátor GUID balíčku je *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Spustíte: ***CMUpdateReset.exe-FDELETE-S Server1.fabrikam.com-D CM_XYZ-P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

### <a name="test-the-tool-with-the-technical-preview"></a>Otestujte nástroj ve verzi Technical Preview.  
Tento nástroj můžete použít s verzí Technical Preview 1606 nebo novější. Tato zpětná podpora je k dispozici, takže nástroj lze použít s větším počtem scénářů aktualizace Technical Preview, aniž byste museli čekat, až bude k dispozici další verze Technical Preview.

Spusťte nástroj v balíčku aktualizací pro Technical Preview před touto aktualizací, která dokončuje kontrolu požadovaných součástí. Dokončený stav kontroly požadovaných součástí je identifikován jedním z následujících stavů balíčku v části **Správa**  >  **aktualizace a údržba**:  
-   **Kontrola požadavků byla úspěšná.**
-   **Kontrola požadovaných součástí byla dokončena s upozorněním.**
-   **Kontrola požadovaných součástí se nezdařila.**


## <a name="high-dpi-console-support"></a>Podpora konzoly s vysokým rozlišením DPI

V této verzi jsou problémy s tím, jak Configuration Manager konzola škáluje a zobrazuje různé části uživatelského rozhraní při zobrazení na vysokém počtu DPI (například na Surface).


## <a name="peer-cache-improvements"></a>Vylepšení sdílené mezipaměti
Od této verze Technical Preview už sdílená mezipaměť [nepoužívá účet pro přístup k síti](../plan-design/hierarchy/client-peer-cache.md) k ověřování žádostí o stažení od partnerských uzlů.


## <a name="improvements-for-sql-server-always-on-availability-groups"></a>Vylepšení pro skupiny dostupnosti Always On SQL Server  
V této verzi teď můžete používat repliky asynchronního potvrzení ve skupinách dostupnosti Always On SQL Server, které používáte s Configuration Manager.  To znamená, že můžete přidat další repliky do skupin dostupnosti, které se použijí jako nepřesné (vzdálené) zálohy, a pak je použít ve scénáři zotavení po havárii.  

- Configuration Manager podporuje použití repliky asynchronního potvrzení k obnovení synchronní repliky.  Informace o tom, jak to provést, najdete v tématu [Možnosti obnovení databáze lokality](../servers/manage/recover-sites.md#site-database-recovery-options) v tématu Zálohování a obnovení.

- Tato verze nepodporuje převzetí služeb při selhání pro použití repliky asynchronního potvrzení jako databáze lokality.
  > [!CAUTION]  
  > Vzhledem k tomu, že Configuration Manager neověřuje stav asynchronního svěření repliky, aby bylo možné potvrdit, že je aktuální a [že by taková replika mohla být nesynchronizovaná](/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server?view=sql-server-2014#AvailabilityModes), použití repliky asynchronního potvrzení jako databáze lokality může mít za následek ohrožení integrity vašeho webu a dat.  

- V rámci skupiny dostupnosti můžete použít stejný počet a typ replik, které jsou podporované podle používané verze SQL Server.   (Předchozí podpora byla omezená na dvě repliky synchronního potvrzení.)

### <a name="configure-an-asynchronous-commit-replica"></a>Konfigurace repliky asynchronního potvrzování
Pokud chcete přidat asynchronní repliku do [skupiny dostupnosti, kterou používáte s Configuration Manager](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md), nemusíte spouštět konfigurační skripty potřebné ke konfiguraci synchronní repliky. (Je to proto, že neexistuje žádná podpora k použití této asynchronní repliky jako databáze lokality.) Další informace najdete v tématu [Přidání sekundární repliky do skupiny dostupnosti](/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server?view=sql-server-2014).

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Obnovení lokality pomocí asynchronní repliky
Před použitím asynchronní repliky k obnovení databáze lokality je nutné zastavit aktivní primární lokalitu, aby se zabránilo dalším zápisům do databáze lokality. Po zastavení lokality můžete použít asynchronní repliku místo použití [ručně obnovené databáze](../servers/manage/recover-sites.md#use-a-site-database-that-has-been-manually-recovered).

Chcete-li lokalitu zastavit, můžete použít [Nástroj Hierarchy Maintenance](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md) k zastavení klíčů služby na serveru lokality. Použijte příkazový řádek: **Preinst.exe/stopsite**   

Zastavení webu je ekvivalentem zastavení služby Správce součástí lokality (Sitecomp) a služby SMS_Executive, na serveru lokality.


## <a name="improved-user-notifications-for-microsoft-365-updates"></a>Vylepšená uživatelská oznámení pro aktualizace Microsoft 365
Bylo provedeno vylepšení, které vám umožní využít uživatelské prostředí pro Office Klikni a spusť, když klient nainstaluje aktualizaci Microsoft 365. To zahrnuje automaticky otevíraná okna a oznámení v aplikaci a možnosti odpočítávání. Před touto verzí byla při odeslání Microsoft 365 aktualizace klientovi automaticky zavřeny aplikace sady Office, které byly otevřeny bez upozornění. Po této aktualizaci už nebudou neočekávaně ukončeny aplikace Office.

### <a name="prerequisites"></a>Předpoklady
Tato aktualizace se vztahuje na Microsoft 365 aplikací pro klienty v podnicích.

### <a name="known-issues"></a>Známé problémy
Když klient vyhodnotí Microsoft 365 přiřazení aktualizace poprvé a aktualizace má konečný termín naplánovaný v minulosti, naplánovalo se okamžitě nebo plánuje do 30 minut, uživatelské prostředí Microsoft 365 může být nekonzistentní. Klient může například obdržet dialog pro odpočítávání na 30 minut, ale skutečné vynucení může začít ještě před koncem odpočítávání. Chcete-li se tomuto chování vyhnout, vezměte v úvahu následující skutečnosti:
- Nasaďte aktualizaci Microsoft 365 s konečným termínem, který je naplánován na více než 60 minut před aktuálním časem.
- Nakonfigurujte časové období údržby během nepracovních hodin v kolekci nebo nakonfigurujte dobu odkladu vynucení v nasazení.

### <a name="try-it-out"></a>Určitě to udělejte!
Zkuste provést následující úkoly a pak nám poslat **zpětnou vazbu** z karty **Domů** na pásu karet a sdělte nám, jak se pracovalo:
- Nasazení do klienta Microsoft 365 aktualizace s konečným termínem nastaveným na čas alespoň 60 minut před aktuálním časem. Sledujte nové chování klienta.


## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Konfigurace a nasazení zásad ochrany Application Guard v programu Windows Defender

[Ochrana Application Guard v programu Windows Defender](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) je nová funkce systému Windows, která pomáhá chránit uživatele otevřením nedůvěryhodných webů v zabezpečeném izolovaném kontejneru, který není přístupný jiným součástem operačního systému. V této verzi Technical Preview jsme přidali podporu pro konfiguraci této funkce pomocí Configuration Manager nastavení dodržování předpisů, která nakonfigurujete a následně nasadíte do kolekce.
Tato funkce bude vydána v Preview pro 64 verzi aktualizace Windows 10 Creator. Pokud chcete tuto funkci nyní otestovat, musíte použít verzi Preview této aktualizace.


### <a name="before-you-start"></a>Než začnete

Aby bylo možné vytvářet a nasazovat zásady ochrany Application Guard v programu Windows Defender, musí být na zařízeních s Windows 10, na která tyto zásady nasazujete, nakonfigurovaná zásada izolace sítě. Další podrobnosti najdete v blogovém příspěvku, na který se odkazuje později.
Tato funkce funguje jenom s aktuálními sestaveními Windows 10 Insider. K otestování musí být na vašich klientech spuštěné poslední sestavení Windows 10 Insider.

### <a name="try-it-out"></a>Určitě to udělejte!

Ujistěte se, že jste si přečetli Blogový příspěvek, abyste pochopili Základy ochrany Application Guard v programu Windows Defender.

Chcete-li vytvořit zásadu a vyhledat dostupná nastavení:

1.  V konzole Configuration Manager vyberte **prostředky a kompatibilita**.
2.  V pracovním prostoru **prostředky a kompatibilita** vyberte **Přehled**  >  **Endpoint Protection**  >  **ochrana Application Guard v programu Windows Defender**.
3.  Na kartě **Domů** ve skupině **vytvořit** klikněte na možnost **vytvořit zásadu Application Guard v programu Windows Defender**.
4.  Pomocí příspěvku na blogu jako reference můžete vyhledat a nakonfigurovat dostupná nastavení, abyste mohli tuto funkci vyzkoušet.
5.  Až skončíte, dokončete průvodce a Nasaďte zásadu na jedno nebo více zařízení s Windows 10.

### <a name="further-reading"></a>Další materiály

Další informace o ochraně Application Guard v programu Windows Defender najdete v [tomto blogovém příspěvku]( https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97).
Další informace o samostatném režimu ochrany Application Guard v programu Windows Defender najdete v [tomto blogovém příspěvku](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).




## <a name="new-capabilities-for-azure-ad-and-cloud-management"></a>Nové funkce pro Azure AD a Cloud Management

V této verzi můžete nakonfigurovat cloudové služby tak, aby používaly službu Azure AD, aby podporovaly následující scénář:

- Ručně nainstalujte klienta Configuration Manager z Internetu a přiřaďte ho k webu Configuration Manager.
- K nasazení klienta Configuration Manager do zařízení na internetu použijte Intune.

### <a name="advantages"></a>Výhody

Použití cloudových služeb a Azure AD odstraňuje nutnost používat certifikáty pro ověřování klientů.

Na webu můžete zjistit uživatele Azure AD, aby je bylo možné používat v kolekcích, a dalších operací Configuration Manager.

### <a name="before-you-start"></a>Než začnete

- Musíte mít tenanta Azure AD.
- Vaše zařízení musí používat Windows 10 a být připojená k Azure AD.  Kromě připojeného k Azure AD se taky můžou připojit i k doméně.
- Kromě [stávajících požadavků](../plan-design/configs/site-and-site-system-prerequisites.md) pro roli systému lokality bodu správy musíte také zajistit, aby byla na počítači, který je hostitelem této role systému lokality, povolena **ASP.NET 4,5** (a všechny další možnosti, které jsou automaticky vybrány).
- Nasazení klienta Configuration Manager pomocí Microsoft Intune:
    - Musíte mít funkčního klienta Intune (Configuration Manager a Intune se nemusíte připojit).
    - V Intune jste vytvořili a nasadili aplikaci, která obsahuje klienta Configuration Manager. Podrobnosti o tom, jak to provést, najdete v tématu Postup instalace klientů do zařízení s Windows spravovaných MDM v Intune.
- Postup použití Configuration Manager k nasazení klienta:
    - Alespoň jeden bod správy musí být konfigurován pro režim HTTPS.
    - Musíte nastavit Brána pro správu cloudu.


### <a name="set-up-the-cloud-management-gateway"></a>Nastavení Brána pro správu cloudu

Nastavte Brána pro správu cloudu, aby klienti měli přístup k webu Configuration Manager z Internetu bez použití certifikátů.

V následujících tématech najdete nápovědu k tomu, jak to udělat:

- [Naplánujte bránu pro správu cloudu v Configuration Manager](../clients/manage/cmg/plan-cloud-management-gateway.md).
- [Nastavte bránu pro správu cloudu pro Configuration Manager](../clients/manage/cmg/setup-cloud-management-gateway.md).
- [Monitorujte bránu pro správu cloudu v Configuration Manager](../clients/manage/cmg/monitor-clients-cloud-management-gateway.md).

### <a name="set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Nastavení aplikace služby Azure v Configuration Manager Cloud Services

Tím se váš Configuration Manager web připojí k Azure AD a je předpokladem pro všechny ostatní operace v této části. Použijte následující postup:

1. V pracovním prostoru **Správa** konzoly Configuration Manager rozbalte položku **Cloud Services**a potom klikněte na položku **služby Azure**.
2. Na kartě **Domů** ve skupině **služby Azure** klikněte na **Konfigurovat služby Azure**.
3. Na stránce **služby Azure** v Průvodci službami Azure vyberte možnost **Správa cloudu** , aby se klienti mohli ověřovat s hierarchií pomocí Azure AD.
4. Na stránce **Obecné** v průvodci zadejte název a popis služby Azure.
5. Na stránce **aplikace** v průvodci vyberte prostředí Azure ze seznamu a potom klikněte na **Procházet** a vyberte server a klientské aplikace, které se použijí ke konfiguraci služby Azure:
   - V okně **aplikace serveru** vyberte serverovou aplikaci, kterou chcete použít, a potom klikněte na **OK**. Serverové aplikace jsou webové aplikace Azure, které obsahují konfigurace pro váš účet Azure, včetně ID tenanta, ID klienta a tajného klíče pro klienty. Pokud nemáte k dispozici serverovou aplikaci, použijte jednu z následujících možností:
       - **Vytvořit**: Pokud chcete vytvořit novou serverovou aplikaci, klikněte na **vytvořit**. Zadejte popisný název aplikace a tenanta. Až se pak přihlásíte k Azure, Configuration Manager pro vás vytvořit webovou aplikaci v Azure, včetně ID klienta a tajného klíče pro použití s webovou aplikací. Později je můžete zobrazit z Azure Portal.
       - **Importovat**: Pokud chcete používat webovou aplikaci, která už ve vašem předplatném Azure existuje, klikněte na **importovat**. Zadejte popisný název aplikace a tenanta a pak zadejte ID tenanta, ID klienta a tajný klíč pro webovou aplikaci Azure, kterou chcete použít Configuration Manager. Po ověření informací pokračujte kliknutím na tlačítko **OK** . Tato možnost není aktuálně k dispozici v této verzi Technical Preview.
   - Opakujte stejný postup pro klientskou aplikaci.

   Aby bylo možné nastavit na portálu správná oprávnění, je nutné udělit oprávnění *číst data* aplikace v adresáři při použití nástroje Import aplikace. Pokud použijete vytváření aplikací, automaticky se vytvoří oprávnění s aplikací, ale přesto musíte udělit souhlas s aplikací v Azure Portal.
6. Na stránce **zjišťování** v průvodci volitelně **Povolte Azure Active Directory zjišťování uživatelů**a pak klikněte na **Nastavení**.
   V dialogovém okně **nastavení zjišťování uživatelů služby Azure AD** nakonfigurujte plán, kdy proběhne zjišťování. Můžete také povolit zjišťování rozdílů, které kontroluje jenom nové nebo změněné účty v Azure AD.
7. Dokončete průvodce.

V tuto chvíli jste připojili Configuration Manager web k Azure AD.


### <a name="install-the-cm-client-from-the-internet"></a>Instalace klienta CM z Internetu

Než začnete, ujistěte se, že zdrojové soubory instalace klienta jsou uložené lokálně na zařízení, do kterého chcete klienta nainstalovat.
Pak postupujte podle pokynů v tématu [nasazení klientů do počítačů se systémem Windows](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual) pomocí následujícího instalačního příkazového řádku (nahraďte hodnoty v příkladu vlastními hodnotami):

**ccmsetup.exe/NoCrlCheck/Source: C:\CLIENT CCMHOSTNAME = SCCMPROXYCONTOSO. CLOUDAPP. NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode = HEC AADTENANTID = 780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME = contoso AADCLIENTAPPID = \<GUID> AADRESOURCEURI =<code>https://contososerver</code>**

- **/NoCrlCheck**: Pokud váš bod správy nebo brána pro správu cloudu používá certifikát bez veřejného serveru, klient nemusí být schopný získat přístup k umístění seznamu CRL.
- **/Source**: místní složka: umístění instalačních souborů klienta.
- **CCMHOSTNAME**: název vašeho internetového bodu správy. To můžete najít spuštěním **gwmi-Namespace root\ccm\locationservices-class SMS_ActiveMPCandidate** z příkazového řádku ve spravovaném klientovi.
- **SMSMP**: název vašeho bodu správy vyhledávání – může to být na intranetu.
- **SMSSiteCode**: kód lokality Configuration Manager.
- **AADTENANTID**, **AADTENANTNAME**: ID a název tenanta Azure AD, který jste propojili s Configuration Manager. To můžete zjistit spuštěním dsregcmd.exe/status z příkazového řádku na zařízení připojeném k Azure AD.
- **AADCLIENTAPPID**: ID klientské aplikace Azure AD. Nápovědu najdete v tématu [použití portálu k vytvoření Azure Active Directory aplikace a instančního objektu, který má přístup k prostředkům](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).
- **AADResourceUri**: identifikátor URI ID aplikace serveru Azure AD.

## <a name="use-azure-services-wizard-to-configure-a-connection-to-oms"></a>Použití Průvodce službami Azure ke konfiguraci připojení k OMS
Od verze 1705 Technical Preview můžete pomocí **Průvodce službami Azure** nakonfigurovat připojení z Configuration Manager ke cloudové službě Operations Management Suite (OMS). Průvodce nahrazuje předchozí pracovní postupy konfigurace tohoto připojení.

-   Průvodce se používá ke konfiguraci Cloud Services pro Configuration Manager, jako je OMS, Windows Store pro firmy (WSfB) a Azure Active Directory (Azure AD).  

-   Configuration Manager se připojuje k OMS pro funkce, jako je Log Analytics nebo Upgrade Readiness.

### <a name="prerequisites-for-the-oms-connector"></a>Předpoklady pro konektor OMS
Požadavky na konfiguraci připojení k OMS se nezměnily z těch, které jsou [zdokumentované pro Current Branch verze 1702](/azure/azure-monitor/platform/collect-sccm). Tyto informace se opakují tady:  

-   Poskytování Configuration Manager oprávnění pro OMS.

-   Konektor OMS musí být nainstalovaný na počítači, který je hostitelem [spojovacího bodu služby](../servers/deploy/configure/about-the-service-connection-point.md) , který je v [online režimu](../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes).

-   Je nutné nainstalovat Microsoft Monitoring Agent pro OMS nainstalované v spojovacím bodě služby spolu s konektorem OMS. Agent a konektor OMS musí být nakonfigurované tak, aby používali stejný **pracovní prostor OMS**. Pokud chcete nainstalovat agenta, přečtěte si téma [Stažení a instalace agenta](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) v dokumentaci k OMS.
-   Po instalaci konektoru a agenta je nutné nakonfigurovat OMS, aby používal data Configuration Manager. Provedete to tak, že na portálu OMS [importujete Configuration Manager kolekce](/azure/log-analytics/log-analytics-sccm#import-collections).

### <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>Použití Průvodce službami Azure ke konfiguraci připojení k OMS

1.  V konzole nástroje v části Přehled **správy**  >  **Overview**  >  **Cloud Services**  >  **služby Azure**a pak zvolte **Konfigurovat služby Azure** na kartě **Domů** na pásu karet a spusťte **Průvodce službami Azure**.

2.  Na stránce **služby Azure** Vyberte cloudovou službu Operations Management Suite. Zadejte popisný název **služby Azure** a případně jeho popis a pak klikněte na **Další**.

3.  Na stránce **aplikace** určete své prostředí Azure (Technical Preview podporuje jenom veřejný cloud). Potom kliknutím na tlačítko **Procházet** otevřete okno serverová aplikace.

4.  Vyberte webovou aplikaci:

    -   **Importovat**: Pokud chcete používat webovou aplikaci, která už ve vašem předplatném Azure existuje, klikněte na **importovat**. Zadejte popisný název aplikace a tenanta a pak zadejte ID tenanta, ID klienta a tajný klíč pro webovou aplikaci Azure, kterou chcete použít Configuration Manager. Po **ověření** informací pokračujte kliknutím na tlačítko **OK** .   

    > [!NOTE]   
    > Při konfiguraci OMS s touto verzí Preview podporuje OMS jenom funkci *Import* pro webovou aplikaci. Vytvoření nové webové aplikace se nepodporuje. Podobně nemůžete znovu použít stávající aplikaci pro OMS.

5.  Pokud jste úspěšně provedli všechny ostatní postupy, zobrazí se na této stránce automaticky informace na obrazovce **Konfigurace připojení OMS** . Pro vaše **předplatné Azure**, **skupinu prostředků Azure**a **pracovní prostor služby Operations Management Suite**by se měly zobrazit informace o nastavení připojení.

6.  Průvodce se připojí ke službě OMS pomocí vámi zadaných informací. Vyberte kolekce zařízení, které chcete synchronizovat s OMS, a pak klikněte na **Přidat**.

7.  Ověřte nastavení připojení na obrazovce **Souhrn** a pak vyberte **Další**. Obrazovka **průběh** zobrazuje stav připojení a pak by měla být **dokončena**.

8.  Po dokončení průvodce se v konzole Configuration Manager ukáže, že jste nakonfigurovali **Operations Management Suite** jako **typ cloudové služby**.