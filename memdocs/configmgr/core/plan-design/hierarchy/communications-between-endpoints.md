---
title: Komunikace mezi koncovými body
titleSuffix: Configuration Manager
description: Přečtěte si, jak Configuration Manager systémy lokality a součásti komunikují přes síť.
ms.date: 10/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0f60d268e1f9bfad9c062041e810be2092da5508
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587231"
---
# <a name="communications-between-endpoints-in-configuration-manager"></a>Komunikace mezi koncovými body v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek popisuje, jak Configuration Manager systémy lokalit a klientů komunikují napříč vaší sítí. Obsahuje následující oddíly:  

- [Komunikace mezi systémy lokality v lokalitě](#Planning_Intra-site_Com)  
  - [Server lokality do distribučního bodu](#bkmk_site2dp)  

- [Komunikace z klientů do služeb a systémů lokality](#Planning_Client_to_Site_System)  
  - [Komunikace mezi klientem a bodem správy](#bkmk_client2mp)  
  - [Komunikace mezi klientem a distribučním bodem](#bkmk_client2dp)  
  - [Požadavky na komunikaci klienta z Internetu nebo nedůvěryhodné doménové struktury](#BKMK_clientspan)  

- [Komunikace mezi doménovými strukturami služby Active Directory](#Plan_Com_X-Forest)  
  - [Podpora počítačů domény v doménové struktuře, která není důvěryhodná pro doménovou strukturu serveru lokality](#bkmk_noforesttrust)  
  - [Podpora počítačů v pracovní skupině](#bkmk_workgroup)  
  - [Scénáře podpory lokality nebo hierarchie, která zahrnuje víc domén a doménových struktur](#bkmk_span)  

## <a name="communications-between-site-systems-in-a-site"></a><a name="Planning_Intra-site_Com"></a>Komunikace mezi systémy lokality v lokalitě  

Když Configuration Manager systémy lokality nebo součásti komunikují přes síť s dalšími systémy lokality nebo komponentami v lokalitě, používají jeden z následujících protokolů v závislosti na tom, jak lokalitu nakonfigurujete:  

- SMB (Server Message Block)  

- HTTP  

- HTTPS  

S výjimkou komunikace ze serveru lokality do distribučního bodu může být komunikace mezi servery v lokalitě kdykoli k dispozici. Tato komunikace nepoužívá mechanismy k řízení šířky pásma sítě. Vzhledem k tomu, že nemůžete řídit komunikaci mezi systémy lokality, ujistěte se, že instalujete servery systému lokality do umístění, kde jsou k dispozici rychlé a dobře propojené sítě.  

### <a name="site-server-to-distribution-point"></a><a name="bkmk_site2dp"></a>Server lokality do distribučního bodu

Pro usnadnění správy přenosu obsahu ze serveru lokality do distribučních bodů použijte následující strategie:  

- Konfigurace distribučního bodu pro řízení šířky pásma sítě a plánování. Tyto ovládací prvky připomínají konfigurace používané adresami mezi lokalitami. Tuto konfiguraci použijte místo instalace jiné Configuration Manager lokality, pokud přenos obsahu do vzdálených síťových umístění je vaším hlavním aspektem šířky pásma.  

- Distribuční bod můžete nainstalovat jako připravený distribuční bod. Připravený distribuční bod vám umožní používat obsah, který je ručně umístěný na server distribučního bodu, a eliminuje požadavek na přenos souborů obsahu v síti.  

Další informace najdete v tématu [Správa šířky pásma sítě pro správu obsahu](manage-network-bandwidth.md).

## <a name="communications-from-clients-to-site-systems-and-services"></a><a name="Planning_Client_to_Site_System"></a>Komunikace od klientů až po systémy lokality a služby

Klienti iniciují komunikaci s rolemi systému lokality, Active Directory Domain Services a online služby. Aby bylo možné tuto komunikaci povolit, musí brány firewall umožňovat síťový provoz mezi klienty a koncovým bodem jejich komunikace. Další informace o portech a protokolech používaných klienty při komunikaci s těmito koncovými body najdete v tématu [porty používané v Configuration Manager](ports.md).  

Předtím, než klient může komunikovat s rolí systému lokality, klient nástroje použije umístění služby k nalezení role, která podporuje protokol klienta (HTTP nebo HTTPS). Ve výchozím nastavení klienti používají nejbezpečnější metodu, která je k dispozici. Další informace najdete v tématu [Vysvětlení způsobu, jakým klienti hledají služby a prostředky lokality](understand-how-clients-find-site-resources-and-services.md).  

Pokud chcete použít protokol HTTPS, nakonfigurujte jednu z následujících možností:  

- Použijte infrastrukturu veřejných klíčů (PKI) a nainstalujte certifikáty PKI na klienty a servery. Informace o používání certifikátů najdete v tématu požadavky na [certifikát PKI](../network/pki-certificate-requirements.md).  

- Počínaje verzí 1806 nakonfigurujte lokalitu tak, aby **používala Configuration Manager certifikáty generované pro systémy lokality http**. Další informace najdete v tématu [Rozšířená http](enhanced-http.md).  

Když nasadíte roli systému lokality, která používá službu Internet Information Services (IIS) a podporuje komunikaci od klientů, je třeba zadat, jestli se klienti připojují k systému lokality pomocí protokolu HTTP nebo HTTPS. Jestliže používáte protokol HTTP, musíte taky zvážit možnosti podepisování a šifrování. Další informace najdete v tématu [Plánování podepisování a šifrování](../security/plan-for-security.md#BKMK_PlanningForSigningEncryption).  

### <a name="client-to-management-point-communication"></a><a name="bkmk_client2mp"></a>Komunikace mezi klientem a bodem správy

V případě, že klient komunikuje s bodem správy, existují dvě fáze: ověřování (Transport) a autorizace (zpráva). Tento proces se liší v závislosti na následujících faktorech:

- Konfigurace lokality: jenom HTTPS, povoluje protokol HTTP nebo HTTPS nebo povoluje HTTP nebo HTTPS s povoleným rozšířeným protokolem HTTP.
- Konfigurace bodu správy: HTTPS nebo HTTP
- Identita zařízení pro scénáře zaměřené na zařízení
- Identita uživatele pro scénáře zaměřené na uživatele

Pomocí následující tabulky můžete pochopit, jak tento proces funguje:  

| Typ MP  | Ověření klienta  | Autorizace klienta<br>Identita zařízení  | Autorizace klienta<br>Identita uživatele  |
|----------|---------|---------|---------|
| HTTP     | Anonymní<br>Při rozšířeném protokolu HTTP lokalita ověří token *uživatele* nebo *zařízení* Azure AD. | Požadavek na umístění: anonymní<br>Klientský balíček: anonymní<br>Registrace pomocí jedné z následujících metod k prokázání identity zařízení:<br> Anonymní (ruční schválení)<br> -Windows – integrované ověřování<br> – Token *zařízení* Azure AD (rozšířený protokol HTTP)<br>Po registraci klient pomocí podepisování zprávy prokáže identitu zařízení. | Pro scénáře zaměřené na uživatele pomocí jedné z následujících metod prokázání identity uživatele:<br> -Windows – integrované ověřování<br> – Token *uživatele* Azure AD (rozšířený protokol HTTP) |
| HTTPS    | Použijte jednu z následujících metod:<br> – Certifikát PKI<br> -Windows – integrované ověřování<br> – Token *uživatele* nebo *zařízení* Azure AD | Požadavek na umístění: anonymní<br>Klientský balíček: anonymní<br>Registrace pomocí jedné z následujících metod k prokázání identity zařízení:<br> Anonymní (ruční schválení)<br> -Windows – integrované ověřování<br> – Certifikát PKI<br> – Token *uživatele* nebo *zařízení* Azure AD<br>Po registraci klient pomocí podepisování zprávy prokáže identitu zařízení. | Pro scénáře zaměřené na uživatele pomocí jedné z následujících metod prokázání identity uživatele:<br> -Windows – integrované ověřování<br> – Token *uživatele* Azure AD |

> [!Tip]  
> Další informace o konfiguraci bodu správy pro různé typy identit zařízení a o bráně pro správu cloudu najdete v tématu [Povolení bodu správy pro protokol HTTPS](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

### <a name="client-to-distribution-point-communication"></a><a name="bkmk_client2dp"></a>Komunikace mezi klientem a distribučním bodem

Když klient komunikuje s distribučním bodem, musí se před stažením obsahu ověřit. Pomocí následující tabulky můžete pochopit, jak tento proces funguje:

| DP – typ  | Ověření klienta  |
|----------|---------|
| HTTP     | -Anonymní, pokud je povoleno<br>– Ověřování integrované v systému Windows s účtem počítače nebo účtem přístupu k síti<br> -Přístupový token obsahu (rozšířený protokol HTTP) |
| HTTPS    | – Certifikát PKI<br> – Ověřování integrované v systému Windows s účtem počítače nebo účtem přístupu k síti<br> -Přístupový token obsahu |

### <a name="considerations-for-client-communications-from-the-internet-or-an-untrusted-forest"></a><a name="BKMK_clientspan"></a>Požadavky na komunikaci klienta z Internetu nebo nedůvěryhodné doménové struktury

Další informace najdete v těchto článcích:

- [Plánování brány pro správu cloudu](../..//clients/manage/cmg/plan-cloud-management-gateway.md)

- [Plánování internetové správy klientů](../../clients/manage/plan-internet-based-client-management.md)

##  <a name="communications-across-active-directory-forests"></a><a name="Plan_Com_X-Forest"></a>Komunikace napříč doménovými strukturami služby Active Directory  

Configuration Manager podporuje lokality a hierarchie, které zahrnují doménové struktury služby Active Directory. Zároveň podporuje počítače domény, které nejsou ve stejné doménové struktuře služby Active Directory jako server lokality, a počítače, které jsou v pracovních skupinách.  

### <a name="support-domain-computers-in-a-forest-thats-not-trusted-by-your-site-servers-forest"></a><a name="bkmk_noforesttrust"></a>Podpora počítačů domény v doménové struktuře, která není důvěryhodná pro doménovou strukturu serveru lokality

- Nainstalovat role systému lokality v této nedůvěryhodné doménové struktuře, s možností publikovat informace o lokalitě v příslušné doménové struktuře služby Active Directory  

- Spravovat tyto počítače, jako by se jedná o počítače pracovní skupiny  

Když nainstalujete servery systému lokality do nedůvěryhodné doménové struktury služby Active Directory, komunikace mezi klientem a serverem od klientů v této doménové struktuře zůstane v této doménové struktuře a Configuration Manager může ověřit počítač pomocí protokolu Kerberos. Když publikujete informace o lokalitě do doménové struktury klienta, klienti budou moci načíst informace o lokalitě, jako je například seznam dostupných bodů správy, ze své doménové struktury služby Active Directory, nikoli stahovat tyto informace z přiřazeného bodu správy.  

> [!NOTE]  
> Pokud chcete spravovat zařízení, která jsou na internetu, můžete nainstalovat internetové role systému lokality do hraniční sítě, když jsou servery systému lokality v doménové struktuře služby Active Directory. Tento scénář nevyžaduje oboustranný vztah důvěryhodnosti mezi hraniční sítí a doménovou strukturou serveru lokality.  

### <a name="support-computers-in-a-workgroup"></a><a name="bkmk_workgroup"></a>Podpora počítačů v pracovní skupině  

- Ručně schválit počítače v pracovních skupinách, pokud pro připojení k rolím systému lokality používají klientská připojení HTTP. Configuration Manager nemůže tyto počítače ověřit pomocí protokolu Kerberos.  

- Nakonfigurovat použití účtu přístupu k síti pro klienty pracovní skupiny, aby tyto počítače mohly načítat obsah z distribučních bodů.  

- Poskytnout alternativní mechanismus, který klientům pracovní skupiny umožní najít body správy. Použijte publikování DNS, službu WINS nebo přímo přiřaďte bod správy. Tito klienti nemohou načítat informace o lokalitě z Active Directory Domain Services.  

Další informace najdete v těchto článcích:  

- [Správa konfliktních záznamů](../../clients/manage/manage-clients.md#BKMK_ConflictingRecords)  

- [Účet přístupu k síti](fundamental-concepts-for-content-management.md#accounts-used-for-content-management)  

- [Postup instalace klientů Configuration Manager v počítačích v pracovní skupině](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)  

### <a name="scenarios-to-support-a-site-or-hierarchy-that-spans-multiple-domains-and-forests"></a><a name="bkmk_span"></a> Scénáře podpory lokality nebo hierarchie, která zahrnuje víc domén a doménových struktur  

#### <a name="scenario-1-communication-between-sites-in-a-hierarchy-that-spans-forests"></a>Scénář 1: komunikace mezi lokalitami v hierarchii, která zahrnuje doménové struktury

Tento scénář vyžaduje obousměrnou důvěryhodnost mezi doménami, která podporuje ověřování pomocí protokolu Kerberos.  Pokud nemáte oboustranně důvěryhodný vztah důvěryhodnosti, který podporuje ověřování protokolem Kerberos, Configuration Manager nepodporuje podřízenou lokalitu ve vzdálené doménové struktuře.  

Configuration Manager podporuje instalaci podřízené lokality ve vzdálené doménové struktuře, která má požadovanou obousměrnou důvěryhodnost s doménovou strukturou nadřazené lokality. Můžete například umístit sekundární lokalitu v jiné doménové struktuře z primární nadřazené lokality, pokud existuje požadovaný vztah důvěryhodnosti.  

> [!NOTE]  
> Podřízená lokalita může být primární lokalitou (kde lokalita centrální správy je nadřazená lokalita) nebo sekundární lokalita.  

Komunikace mezi lokalitami v Configuration Manager používá replikaci databáze a souborové přenosy. Když nainstalujete lokalitu, musíte zadat účet, pomocí kterého se má lokalita nainstalovat na určený server. Tento účet také umožní navázání a udržování komunikace mezi lokalitami. Po úspěšné instalaci lokality a iniciování přenosů na základě souborů a replikace databáze není nutné pro komunikaci s lokalitou nic dalšího konfigurovat.  

Když existuje obousměrný vztah důvěryhodnosti mezi doménovými strukturami, Configuration Manager nevyžaduje žádné další kroky konfigurace.  

Ve výchozím nastavení se při instalaci nové podřízené lokality Configuration Manager nakonfigurují následující komponenty:  

- Nastavení postupu replikace na základě souborů mezi lokalitami na všech lokalitách, které používají účet počítače serveru lokality. Configuration Manager do cílového počítače přidá počítačový účet každého počítače do **skupiny&lt;SMS_SiteToSiteConnection_\> SiteCode** .  

- Replikace databáze mezi servery SQL v každé lokalitě.  

Nastavte také následující konfigurace:  

- Používané brány firewall a síťová zařízení musí umožňovat síťové pakety, které Configuration Manager vyžaduje.  

- Mezi doménovými strukturami musí fungovat překlad adres IP.  

- Chcete-li nainstalovat lokalitu nebo roli systému lokality, je třeba na určený počítač zadat účet s oprávněním správce.  

#### <a name="scenario-2-communication-in-a-site-that-spans-forests"></a>Scénář 2: komunikace v lokalitě, která zahrnuje doménové struktury

Tento scénář nevyžaduje oboustranný vztah důvěryhodnosti mezi doménami.  

Primární lokality podporují instalace rolí systému lokality na počítačích ve vzdálených doménových strukturách.  

- Jedinou výjimkou je bod služeb webu Katalog aplikací.  Podporuje se jenom ve stejné doménové struktuře jako server lokality.  

- Když role systému lokality akceptuje připojení z Internetu, jako osvědčený postup zabezpečení nainstalujte role systému lokality do umístění, kde hranice doménové struktury poskytuje ochranu pro server lokality (třeba v hraniční síti).  

Chcete-li nainstalovat roli systému lokality na počítač v nedůvěryhodné doménové struktuře:  

- Zadejte **účet instalace systému lokality**, který lokalita používá k instalaci role systému lokality. (Tento účet musí mít místní pověření správce pro připojení.) Pak na určený počítač nainstalujte role systému lokality.  

- Vyberte možnost systému lokality **vyžadovat, aby server lokality inicializoval připojení k tomuto systému lokality**. Toto nastavení vyžaduje, aby server lokality navázal spojení se systémovým serverem lokality pro přenos dat. Tato konfigurace brání počítači v nedůvěryhodném umístění v navázání kontaktu se serverem lokality, který je ve vaší důvěryhodné síti. Tato připojení používají **Účet instalace systému lokality**.  

Chcete-li použít roli systému lokality, která byla nainstalovaná v nedůvěryhodné doménové struktuře, musí brány firewall umožňovat síťový provoz i v případě, že server lokality zahájí přenos dat.  

Následující role systému lokality navíc vyžadují přímý přístup do databáze lokality. Brány firewall proto musí umožňovat příslušný provoz z nedůvěryhodné doménové struktury do SQL Server lokality:  

- Bod synchronizace katalogu Asset Intelligence  

- Bod ochrany koncového bodu Endpoint Protection  

- Bod registrace  

- Bod správy  

- Bod služby Reporting services  

- Bod migrace stavu  

Další informace najdete v tématu [porty používané v Configuration Manager](ports.md).  

Je možné, že budete muset nakonfigurovat bod správy a bod registrace přístup k databázi lokality.

- Ve výchozím nastavení se při instalaci těchto rolí Configuration Manager nakonfiguruje účet počítače nového serveru systému lokality jako účet připojení pro roli systému lokality. Pak účet přidá k příslušné roli databáze SQL Server.  

- Při instalaci těchto rolí systému lokality v nedůvěryhodné doméně nakonfigurujte účet pro připojení role systému lokality, aby role systému lokality mohla získávat informace z databáze.  

Pokud pro tyto role systému lokality nakonfigurujete účet uživatele domény tak, aby byl účtem pro připojení, ujistěte se, že uživatelský účet domény má odpovídající přístup k databázi SQL Server v této lokalitě:  

- Bod správy: **Účet připojení k databázi bodu správy**  

- Bod registrace: **Účet připojení k bodu registrace**  

Při plánování rolí systému lokality v jiných doménových strukturách zvažte následující doplňkové informace:  

- Pokud používáte bránu Windows Firewall, nakonfigurujte příslušné profily brány firewall tak, aby předávaly komunikaci mezi serverem databáze lokality a počítači, které jsou nainstalovány s rolemi vzdáleného systému lokality.

- Pokud internetový bod správy důvěřuje doménové struktuře, která obsahuje uživatelské účty, jsou podporovány zásady uživatele. Pokud zde vztah důvěryhodnosti není, jsou podporovány pouze zásady počítače.  

#### <a name="scenario-3-communication-between-clients-and-site-system-roles-when-the-clients-arent-in-the-same-active-directory-forest-as-their-site-server"></a>Scénář 3: komunikace mezi klienty a rolemi systému lokality, pokud klienti nejsou ve stejné doménové struktuře služby Active Directory jako jejich server lokality

Configuration Manager podporuje následující scénáře pro klienty, kteří nejsou ve stejné doménové struktuře jako jejich server lokality:  

- Mezi doménovou strukturou klienta a doménovou strukturou serveru lokality existuje obousměrný vztah důvěryhodnosti mezi doménami.  

- Server role systému lokality je umístěn ve stejné doménové struktuře jako klient nástroje.  

- Klient se nachází v počítači domény, který nemá oboustranný vztah důvěryhodnosti se serverem lokality, a role systému lokality nejsou v doménové struktuře klienta nainstalovány.  

- Klient se nachází v počítači pracovní skupiny.  

Klienti na počítači připojeném k doméně můžou použít Active Directory Domain Services pro umístění služby, když je jejich lokalita publikovaná v doménové struktuře služby Active Directory.  

Publikování informací o lokalitě v jiné doménové struktuře služby Active Directory:  

- Zadat doménovou strukturu a poté povolit publikování v této doménové struktuře v uzlu **Doménové struktury služby Active Directory** v pracovním prostoru **Správa** .  

- Nakonfigurovat, aby všechny lokality publikovaly svoje data ve službě Active Directory Domain Services. Tato konfigurace umožňuje klientům v dané doménové struktuře získávat informace o lokalitě a vyhledávat body správy. U klientů, kteří nemohou používat Active Directory Domain Services pro umístění služby, můžete použít DNS, WINS nebo bod správy přiřazený klientovi.  

#### <a name="scenario-4-put-the-exchange-server-connector-in-a-remote-forest"></a><a name="bkmk_xchange"></a>Scénář 4: umístění konektoru systému Exchange Server ve vzdálené doménové struktuře  

Pro podporu tohoto scénáře se ujistěte, že překlad názvů funguje mezi doménovými strukturami. Například nakonfigurujte přeposílání DNS. Při konfiguraci konektoru serveru Exchange Server zadejte intranetový plně kvalifikovaný název domény serveru Exchange. Další informace najdete v tématu [Správa mobilních zařízení pomocí Configuration Manager a Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="see-also"></a>Viz také

- [Plánování zabezpečení](../security/plan-for-security.md)  

- [Zabezpečení a ochrana osobních údajů pro klienty Configuration Manager](../../clients/deploy/plan/security-and-privacy-for-clients.md)  
