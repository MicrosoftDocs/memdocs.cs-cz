---
title: Zabezpečení a ochrana osobních údajů pro správu lokality
titleSuffix: Configuration Manager
description: Optimalizace zabezpečení a ochrany osobních údajů pro správu lokalit v Configuration Manager
ms.date: 04/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1d58176e-abc0-4087-8583-ce70deb4dcf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 923018e35fae1ec1f5e9c0869ef22d43b5de552b
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2020
ms.locfileid: "82182255"
---
# <a name="security-and-privacy-for-site-administration-in-configuration-manager"></a>Zabezpečení a ochrana osobních údajů pro správu lokalit v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek obsahuje informace o zabezpečení a ochraně osobních údajů pro Configuration Manager lokality a hierarchii.

## <a name="security-guidance-for-site-administration"></a><a name="BKMK_Security_Sites"></a>Pokyny k zabezpečení pro správu lokality

Následující pokyny vám pomůžou zabezpečit Configuration Manager lokality a hierarchii.  

### <a name="run-setup-from-a-trusted-source-and-secure-communication"></a>Spustit instalaci z důvěryhodného zdroje a zabezpečit komunikaci

Chcete-li zabránit někomu v manipulaci se zdrojovými soubory, spusťte Configuration Manager instalaci z důvěryhodného zdroje. Pokud soubory ukládáte na síť, zabezpečte umístění v síti.  

Pokud spustíte instalaci z umístění v síti, zabráníte útočníkovi v manipulaci se soubory, které jsou přenášeny přes síť, pomocí protokolu IPsec nebo podepisování SMB mezi umístěním zdroje instalačních souborů a serverem lokality.  

Pokud ke stažení souborů požadovaných instalačním programem používáte nástroj pro stažení instalačního programu, ujistěte se, že zabezpečíte umístění, kde jsou tyto soubory uloženy. Při spuštění instalačního programu také zabezpečte komunikační kanál pro toto umístění.  

### <a name="extend-the-active-directory-schema-and-publish-sites-to-the-domain"></a>Rozšíříte schéma služby Active Directory a publikujete weby v doméně.  

Rozšíření schématu nejsou pro spuštění Configuration Manager nutná, ale vytvářejí bezpečnější prostředí. Klienti a servery lokality mohou načítat informace z důvěryhodného zdroje.  

Pokud se klienti nacházejí v nedůvěryhodné doméně, nasaďte následující role systému lokality do domén klientů:  

- Bod správy  

- Distribuční bod  

> [!NOTE]  
> Důvěryhodná doména pro Configuration Manager vyžaduje ověřování protokolem Kerberos. Pokud se klienti nacházejí v jiné doménové struktuře, která nemá oboustranný vztah důvěryhodnosti s doménovou strukturou serveru lokality, považují se tito klienti za nedůvěryhodnou doménu. Externí vztah důvěryhodnosti není pro tento účel dostatečný.  

### <a name="use-ipsec-to-secure-communications"></a>Použití protokolu IPsec k zabezpečení komunikace

I když Configuration Manager zabezpečenou komunikaci mezi serverem lokality a počítačem, na kterém běží SQL Server, Configuration Manager nezabezpečuje komunikaci mezi rolemi systému lokality a SQL Server. Pro komunikaci v rámci lokality můžete nakonfigurovat pouze některé systémy lokality s protokolem HTTPS.  

Pokud nepoužíváte další kontroly pro zabezpečení těchto kanálů mezi servery, útočníci mohou používat různé falšování a útoky prostředníkem proti systémům lokality. Pokud nemůžete použít protokol IPsec, použijte podepisování SMB.  

> [!Important]  
> Zabezpečte komunikační kanál mezi serverem lokality a zdrojovým serverem balíčku. Tato komunikace používá podepisování SMB. Pokud k zabezpečení této komunikace nemůžete použít protokol IPsec, použijte podepisování SMB a ujistěte se, že se soubory před stažením a spuštěním klientů nepoškodily.  

### <a name="dont-change-the-default-security-groups"></a>Neměnit výchozí skupiny zabezpečení

Neměňte následující skupiny zabezpečení, které Configuration Manager vytváří a spravuje pro komunikaci se systémem lokality:

- **SMS_SiteSystemToSiteServerConnection_MP_&lt;SiteCode\>**  

- **SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;SiteCode\>**  

- **SMS_SiteSystemToSiteServerConnection_Stat_&lt;SiteCode\>**  

Configuration Manager automaticky vytvoří a spravuje tyto skupiny zabezpečení. Toto chování zahrnuje odebrání účtů počítačů, pokud je odebrána role systému lokality.  

Chcete-li zajistit kontinuitu služeb a minimální oprávnění, tyto skupiny neupravujte ručně.  

### <a name="manage-the-trusted-root-key-provisioning-process"></a>Správa procesu zajišťování důvěryhodného kořenového klíče

Pokud klienti nemohou zadat dotaz na globální katalog kvůli Configuration Manager informacím, musí při ověřování platných bodů správy spoléhat na důvěryhodný kořenový klíč. Důvěryhodný kořenový klíč je uložen v registru klienta. Dá se nastavit pomocí zásad skupiny nebo ruční konfigurace.  

Pokud klient nemá kopii důvěryhodného kořenového klíče předtím, než kontaktuje bod správy poprvé, důvěřuje prvnímu bodu správy, se kterým komunikuje. Pro snížení rizika u klientů uvedených v omyl útočníky na neautorizovaný bod správy můžete klientům předem poskytnout důvěryhodný kořenový klíč. Další informace najdete v tématu [Plánování důvěryhodného kořenového klíče](../security/plan-for-security.md#BKMK_PlanningForRTK).  

### <a name="use-non-default-port-numbers"></a>Používat jiná než výchozí čísla portů

Používání jiných než výchozích čísel portů může poskytovat zvýšené zabezpečení. Usnadňují útočníkům prozkoumat prostředí při přípravě na útok. Pokud se rozhodnete použít jiné než výchozí porty, naplánujte si je ještě před instalací Configuration Manager. Používejte je konzistentně napříč všemi lokalitami v hierarchii. Porty požadavků klienta a Wake On LAN jsou příklady, kde můžete používat jiná než výchozí čísla portů.  

### <a name="use-role-separation-on-site-systems"></a>Použití oddělení rolí v systémech lokality

I když můžete nainstalovat všechny role systému lokality na jeden počítač, tento postup se v produkčních sítích používá zřídka. Vytváří jediný bod selhání.  

### <a name="reduce-the-attack-profile"></a>Omezení profilu útoku

Izolování každé role systému lokality na jiném serveru snižuje riziko, že útok na ohrožení zabezpečení v jednom systému lokality lze použít pro jiný systém lokality. Mnoho rolí vyžaduje instalaci služby Internetová informační služba (IIS) v systému lokality a tato nutnost zvyšuje plochu pro útok. Pokud potřebujete kombinovat role, abyste snížili náklady na hardware, slučte role služby IIS pouze s jinými rolemi, které vyžadují službu IIS.  

> [!IMPORTANT]  
> Role záložního stavového bodu je výjimka. Vzhledem k tomu, že tato role systému lokality přijímá neověřená data od klientů, nepřiřazujte roli záložního stavového bodu žádné jiné Configuration Manager role systému lokality.  

### <a name="configure-static-ip-addresses-for-site-systems"></a>Konfigurace statických IP adres pro systémy lokality

Statické IP adresy se snadněji chrání před útoky na překlad adres IP.  

Statické IP adresy také usnadňují konfiguraci protokolu IPsec. Použití protokolu IPsec je osvědčeným postupem zabezpečení pro zabezpečení komunikace mezi systémy lokality v Configuration Manager.  

### <a name="dont-install-other-applications-on-site-system-servers"></a>Na servery systému lokality neinstalujte další aplikace.

Když na servery systému lokality nainstalujete další aplikace, zvýšíte tak pro Configuration Manager prostoru pro útoky. Také riskujete problémy s nekompatibilitou.  

### <a name="require-signing-and-enable-encryption-as-a-site-option"></a>Vyžadovat podepsání a povolit šifrování jako možnost lokality

Povoluje možnosti podepisování a šifrování pro danou lokalitu. Zajistěte, aby všichni klienti mohli podporovat algoritmus hash SHA-256, a pak povolte možnost **vyžadovat SHA-256**.  

### <a name="restrict-and-monitor-administrative-users"></a>Omezení a monitorování administrativních uživatelů

Udělte přístup pro správu k Configuration Manager jenom uživatelům, kterým důvěřujete. Pak jim udělte minimální oprávnění pomocí předdefinovaných rolí zabezpečení nebo přizpůsobením rolí zabezpečení. Uživatelé s právy pro správu, kteří můžou vytvářet, upravovat a nasazovat software a konfigurace, můžou potenciálně ovládat zařízení v hierarchii Configuration Manager.  

Pravidelně přiřazení správců a úroveň jejich autorizace auditujte, abyste ověřili požadované změny.  

Další informace najdete v tématu [Konfigurace správy na základě rolí](../../servers/deploy/configure/configure-role-based-administration.md).  

### <a name="secure-configuration-manager-backups"></a>Zabezpečené zálohování Configuration Manager

Při zálohování Configuration Manager tyto informace obsahují certifikáty a další citlivá data, která by mohl útočník zneužít pro zosobnění.  

Při přenosu dat sítí používejte podepisování SMB nebo protokol IPsec a zabezpečte umístění zálohy.  

### <a name="secure-locations-for-exported-objects"></a>Zabezpečená umístění pro exportované objekty

Kdykoli exportujete nebo importujete objekty z konzoly Configuration Manager do umístění v síti, Zabezpečte umístění a zabezpečte síťový kanál.

Omezte přístup k síťové složce neoprávněným uživatelům.  

Chcete-li zabránit útočníkovi v manipulaci s exportovanými daty, použijte podepisování SMB nebo protokol IPsec mezi umístěním v síti a serverem lokality. Také Zabezpečte komunikaci mezi počítačem, na kterém je spuštěna konzola Configuration Manager a server lokality. Pro šifrování dat na síti používejte protokol IPsec, abyste zabránili odhalení informací.  

### <a name="manually-remove-certificates-from-failed-servers"></a>Ruční odebrání certifikátů ze serverů, které selhaly

Pokud systém lokality není správně odinstalován nebo přestane fungovat a nelze ho obnovit, ručně odeberte certifikáty Configuration Manager pro tento server z jiných serverů Configuration Manager.

Chcete-li odebrat vztah důvěryhodnosti partnerského vztahu, který byl původně vytvořen se systémem lokality a rolemi systému lokality, ručně odeberte certifikáty Configuration Manager pro server, který se nezdařil, v úložišti certifikátů **Důvěryhodné osoby** na ostatních serverech systému lokality. Tato akce je důležitá, pokud server znovu použijete beze změny formátování.  

Další informace najdete v tématu [ovládání kryptografie pro komunikaci serveru](../security/cryptographic-controls-technical-reference.md#cryptographic-controls-for-server-communication).  

### <a name="dont-configure-internet-based-site-systems-to-bridge-the-perimeter-network"></a>Nekonfigurujte internetové systémy lokality pro přemostění hraniční sítě.

Nekonfigurujte servery systému lokality tak, aby byly vícedomé, aby se připojovaly k hraniční síti a intranetu. I když tato konfigurace umožňuje, aby internetové systémy lokality přijímaly připojení klientů z Internetu a intranetu, eliminuje hranice zabezpečení mezi hraniční sítí a intranetem.  

### <a name="configure-the-site-server-to-initiate-connections-to-perimeter-networks"></a>Konfigurace serveru lokality, aby inicializoval připojení k hraničním sítím

Pokud je systém lokality v nedůvěryhodné síti, například hraniční síti, nakonfigurujte server lokality tak, aby inicializoval připojení k systému lokality.

Ve výchozím nastavení systémy lokality inicializují připojení k serveru lokality pro přenos dat. Tato konfigurace může představovat bezpečnostní riziko, když se iniciuje připojení z nedůvěryhodné sítě k důvěryhodné síti. Pokud systémy lokality přijímají připojení z Internetu nebo se nacházejí v nedůvěryhodné doménové struktuře, nakonfigurujte možnost systému lokality tak, aby **vyžadovala, aby server lokality inicializoval připojení k tomuto systému lokality**. Po instalaci systému lokality a všech rolí jsou všechna připojení iniciována serverem lokality z důvěryhodné sítě.  

### <a name="use-ssl-bridging-and-termination-with-authentication"></a>Použití přemostění a ukončení SSL s ověřováním

Pokud používáte webovou proxy server pro internetovou správu klientů, použijte přemostění SSL do SSL, a to pomocí ukončení s ověřením.

Při konfiguraci ukončení protokolu SSL na webovém proxy serveru se pakety z Internetu mohou před předáním do interní sítě kontrolovat. Proxy webový Server ověřuje připojení z klienta, ukončí ho a pak otevře nové ověřené připojení k internetovým systémům lokality.  

Když Configuration Manager klientské počítače používají webový proxy server pro připojení k internetovým systémům lokality, identita klienta (GUID) je bezpečně obsažena v datové části paketu. Bod správy pak nepovažuje webový proxy server za klienta.

Pokud váš webový proxy server nepodporuje požadavky na přemostění SSL, podporuje se i tunelování SSL. Tato možnost je méně bezpečná. Pakety SSL z Internetu se předávají do systémů lokality bez ukončení. Pak se nedají zkontrolovat na škodlivý obsah.  

> [!WARNING]  
> Mobilní zařízení zapsaná službou Configuration Manager nemohou používat přemostění SSL. Musí používat pouze tunelování SSL.  

### <a name="configurations-to-use-if-you-configure-the-site-to-wake-up-computers-to-install-software"></a>Konfigurace, které se mají použít, pokud nakonfigurujete lokalitu, aby probudila počítače pro instalaci softwaru

- Pokud používáte tradiční pakety buzení ze spánku, používejte jednosměrná vysílání namísto všesměrového vysílání směrovaného na podsíť.  

- Pokud musíte použít všesměrová vysílání směrovaná na podsíť, nakonfigurujte směrovače tak, aby povolovaly všesměrové vysílání směrované přes IP Server jenom ze serveru lokality a jenom na jiné než výchozí číslo portu.  

Další informace o různých technologiích Wake On LAN najdete v tématu [plánování probuzení klientů](../../clients/deploy/plan/plan-wake-up-clients.md).

### <a name="if-you-use-email-notification-configure-authenticated-access-to-the-smtp-mail-server"></a>Pokud používáte e-mailové oznámení, nakonfigurujte ověřený přístup k poštovnímu serveru SMTP.

Kdykoli je to možné, použijte poštovní server, který podporuje ověřený přístup. Pro ověřování použijte počítačový účet serveru lokality. Pokud je nutné určit uživatelský účet pro ověření, použijte účet s nejnižšími oprávněními. 

### <a name="enforce-ldap-channel-binding-and-ldap-signing"></a>Vynutili vazbu kanálu LDAP a podepisování LDAP

Zabezpečení řadičů domény služby Active Directory se dá zlepšit konfigurací serveru tak, aby odmítal vazby LDAP rozhraní SASL (Simple Authentication and Security Layer) (SASL), které nevyžadují podepisování nebo odmítají jednoduché vazby protokolu LDAP, které se provádí v nejasném textovém připojení. Počínaje verzí 1910 Configuration Manager podporuje vynucování vazby kanálu LDAP a podepisování LDAP. Další informace najdete v článku [2020 vazby kanálu LDAP a požadavky na podpis LDAP pro Windows](https://support.microsoft.com/help/4520412/2020-ldap-channel-binding-and-ldap-signing-requirements-for-windows). <!--6244453-->


## <a name="security-guidance-for-the-site-server"></a><a name="BKMK_Security_SiteServer"></a>Bezpečnostní pokyny pro server lokality

Následující pokyny vám pomůžou zabezpečit Configuration Manager Server lokality.  

### <a name="install-configuration-manager-on-a-member-server-instead-of-a-domain-controller"></a>Nainstalovat Configuration Manager na členský server místo řadiče domény

Configuration Manager Server lokality a systémy lokality nevyžadují instalaci na řadiči domény. Řadiče domény nemají místní databázi SAM (Security Accounts Management) jinou než doménová databáze. Při instalaci Configuration Manager na členský server můžete účty Configuration Manager udržovat v místní databázi SAM místo databáze domény.  

Tento postup také zmenšuje prostor pro útoky v řadičích domény.  

### <a name="install-secondary-sites-without-copying-the-files-over-the-network"></a>Instalace sekundárních lokalit bez kopírování souborů přes síť

Když spustíte instalační program a vytvoříte sekundární lokalitu, nevybírejte možnost kopírování souborů z nadřazené lokality do sekundární lokality. Nepoužívejte také umístění zdroje sítě. Když kopírujete soubory přes síť, mohl by kvalifikovaný útočník zneužít instalační balíček sekundární lokality a před jeho instalací manipulovat se soubory. Načasování tohoto útoku by bylo obtížné. Tento útok lze zmírnit použitím protokolu IPsec nebo SMB při přenosu souborů.  

Místo kopírování souborů v síti na serveru sekundární lokality zkopírujte zdrojové soubory ze složky Media do místní složky. Pak při spuštění instalačního programu za účelem vytvoření sekundární lokality na stránce **zdrojové instalační soubory** vyberte **použít zdrojové soubory v následujícím umístění na počítači sekundární lokality (nejbezpečnější)** a zadejte tuto složku.  

Další informace najdete v tématu [instalace sekundární lokality](../../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary).

### <a name="site-role-installation-inherits-permissions-from-drive-root"></a>Instalace role lokality dědí oprávnění z kořene jednotky

<!-- SCCMDocs#1380 -->
Před instalací první role systému lokality na libovolný server nezapomeňte správně nakonfigurovat oprávnění k systémové jednotce. Například `C:\SMS_CCM` dědí oprávnění z `C:\`. Pokud kořenový adresář jednotky není správně zabezpečený, můžou uživatelé s nízkými právy přistupovat k obsahu ve složce Configuration Manager a upravovat ho.


## <a name="security-guidance-for-sql-server"></a><a name="BKMK_Security_SQLServer"></a>Pokyny k zabezpečení pro SQL Server

Configuration Manager používá jako back-end databázi SQL Server. Pokud dojde k ohrožení databáze, útočník by mohl obejít Configuration Manager. Pokud mají přístup k SQL Server přímo, můžou spouštět útoky prostřednictvím Configuration Manager. Zvažte útoky na SQL Server vysokým rizikem a omezte jejich náležité omezení.  

Následující bezpečnostní pokyny vám pomůžou zabezpečit SQL Server Configuration Manager.  

### <a name="dont-use-the-configuration-manager-site-database-server-to-run-other-sql-server-applications"></a>Nepoužívejte Server databáze lokality Configuration Manager ke spouštění jiných SQL Server aplikací.

Když zvýšíte přístup k serveru databáze lokality Configuration Manager, tato akce zvyšuje riziko pro vaše Configuration Manager data. Pokud dojde k ohrožení bezpečnosti databáze Configuration Manager, budou ohroženy také další aplikace na stejném SQL Server počítači.  

### <a name="configure-sql-server-to-use-windows-authentication"></a>Konfigurace SQL Server pro použití ověřování systému Windows

I když Configuration Manager přistupuje k databázi lokality pomocí účtu systému Windows a ověřování systému Windows, je stále možné nakonfigurovat SQL Server pro použití SQL Server smíšeného režimu. SQL Server smíšený režim umožňuje přístup k databázi dalším přihlášením SQL. Tato konfigurace není nutná a zvyšuje úroveň útoku.  

### <a name="update-sql-server-express-at-secondary-sites"></a>Aktualizace SQL Server Express v sekundárních lokalitách

Když nainstalujete primární lokalitu, Configuration Manager stáhnout SQL Server Express z webu Microsoft Download Center. Pak zkopíruje soubory na server primární lokality. Když nainstalujete sekundární lokalitu a vyberete možnost, která nainstaluje SQL Server Express, Configuration Manager nainstaluje dříve staženou verzi. Nekontroluje, zda jsou k dispozici nové verze. Chcete-li zajistit, aby sekundární lokalita měla nejnovější verze, proveďte jeden z následujících kroků:  

- Po instalaci sekundární lokality spusťte web Windows Update na serveru sekundární lokality.  

- Před instalací sekundární lokality ručně nainstalujte SQL Server Express na server sekundární lokality. Ujistěte se, že instalujete nejnovější verzi a všechny aktualizace softwaru. Poté nainstalujte sekundární lokalitu a vyberte možnost použití existující instance SQL Server.  

Pravidelně spouštějte web Windows Update pro všechny nainstalované verze SQL Server. Tento postup zajistí, že budou mít nejnovější aktualizace softwaru.  

### <a name="follow-general-guidance-for-sql-server"></a>Postupujte podle obecných pokynů pro SQL Server

Identifikujte a postupujte podle obecných pokynů pro vaši verzi SQL Server. Vezměte ale v úvahu následující požadavky na Configuration Manager:  

- Počítačový účet serveru lokality musí být člen skupiny správců v počítači, na kterém je systém SQL Server spuštěn. Pokud budete postupovat podle SQL Server doporučení "výslovně zřídit hlavní objekty správce", účet, který použijete ke spuštění instalace na serveru lokality, musí být členem skupiny uživatelů systému SQL.  

- Pokud nainstalujete SQL Server pomocí uživatelského účtu domény, ujistěte se, že účet počítače serveru lokality je nakonfigurovaný pro hlavní název služby (SPN), který je publikovaný na Active Directory Domain Services. Bez hlavního názvu služby (SPN) se ověřování protokolu Kerberos nepovede a instalace Configuration Manager se nepovede  


## <a name="security-guidance-for-site-systems-that-run-iis"></a><a name="BKMK_Security_IIS"></a>Bezpečnostní pokyny pro systémy lokality, které spouštějí službu IIS

Několik rolí systému lokality v Configuration Manager vyžaduje službu IIS. Proces zabezpečení služby IIS umožňuje Configuration Manager správně fungovat a snižuje riziko bezpečnostních útoků. Pokud je to praktické, minimalizujte počet serverů, které vyžadují službu IIS. Například spouštějte pouze počet bodů správy, které požadujete pro podporu vaší klientské základny, a vezměte v úvahu vysokou dostupnost a izolaci sítě pro internetovou správu klientů.  

Následující pokyny vám pomůžou zabezpečit systémy lokality, které spouští službu IIS.  

### <a name="disable-iis-functions-that-you-dont-require"></a>Zakažte funkce IIS, které nepotřebujete.

Nainstalujte pouze minimální počet funkcí IIS pro roli systému lokality, kterou instalujete. Další informace najdete v tématu [Požadované součásti lokality a systému lokality](../configs/site-and-site-system-prerequisites.md).  

### <a name="configure-the-site-system-roles-to-require-https"></a>Konfigurace rolí systému lokality pro vyžadování protokolu HTTPS

Pokud se klienti připojují k systému lokality pomocí protokolu HTTP, a ne pomocí protokolu HTTPS, používají ověřování systému Windows. Toto chování se může vrátit k použití ověřování NTLM místo ověřování pomocí protokolu Kerberos. Je-li použito ověřování NTLM, klienti se mohou připojit k podvodnému serveru.  

Výjimkou z těchto pokynů můžou být distribuční body. Účty pro přístup k balíčkům nefungují, pokud je distribuční bod konfigurován pro protokol HTTPS. Účty pro přístup k balíčku umožňují ověření obsahu, aby bylo možné omezit uživatele, kteří mohou k obsahu přistupovat. Další informace najdete v tématu [osvědčené postupy zabezpečení pro správu obsahu](security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement).  

### <a name="configure-a-certificate-trust-list-ctl-in-iis-for-site-system-roles"></a>Konfigurace seznamu důvěryhodných certifikátů (CTL) ve službě IIS pro role systému lokality

Role systému lokality:  

- Distribuční bod, který je konfigurován pro protokol HTTPS  

- Bod správy, který nakonfigurujete pro protokol HTTPS a povolení podpory mobilních zařízení

Seznam CTL je definovaný seznam důvěryhodných kořenových certifikačních autorit (CAs). Když použijete seznam CTL se zásadou skupiny a nasazením infrastruktury veřejných klíčů (PKI), umožní vám seznam CTL doplnit stávající důvěryhodné kořenové certifikační autority, které jsou ve vaší síti nakonfigurované. Například certifikační autority, které se automaticky instalují se systémem Microsoft Windows nebo přidávají prostřednictvím kořenové certifikační autority systému Windows Enterprise. Když je ve službě IIS nakonfigurovaný seznam CTL, definuje podmnožinu těchto důvěryhodných kořenových certifikačních autorit.  

Tato podmnožina nabízí větší kontrolu nad zabezpečením. Seznam CTL omezuje klientské certifikáty, které jsou přijímány pouze k certifikátům vydaným ze seznamu certifikačních autorit v seznamu CTL. Například Windows se dodává s řadou dobře známých certifikátů CA třetích stran, jako jsou VeriSign a Thawte.

Ve výchozím nastavení počítač, ve kterém je spuštěna služba IIS, důvěřuje certifikátům, které jsou zřetězené u těchto známých certifikačních autorit. Pokud službu IIS nenakonfigurujete se seznamem CTL pro uvedené role systému lokality, bude lokalita považována za platného klienta všech zařízení, která mají certifikát vystavený z těchto certifikačních autorit. Pokud službu IIS nakonfigurujete se seznamem CTL, který nezahrnuje tyto certifikační autority, lokalita odmítne připojení klientů, pokud certifikát řetězí k těmto certifikačním autoritám. Aby bylo možné Configuration Manager klienty pro uvedené role systému lokality, je třeba nakonfigurovat službu IIS pomocí seznamu CTL, který určuje certifikační autority používané klienty Configuration Manager.  

> [!NOTE]  
> Pouze uvedené role systému lokality vyžadují, abyste nakonfigurovali seznam CTL ve službě IIS. Seznam vydavatelů certifikátů, který Configuration Manager používá pro body správy, poskytuje stejné funkce pro klientské počítače, když se připojí k bodům správy HTTPS.  

Další informace o tom, jak nakonfigurovat seznam důvěryhodných certifikačních autorit ve službě IIS, najdete v dokumentaci ke službě IIS.  

### <a name="dont-put-the-site-server-on-a-computer-with-iis"></a>Neumísťujte webový server na počítač se službou IIS.

Rozdělení rolí pomáhá omezovat profil útoku a zlepšuje obnovení. Účet počítače serveru lokality má obvykle oprávnění správce ve všech rolích systému lokality. Pokud používáte nabízenou instalaci klienta, může mít také tato oprávnění pro klienty Configuration Manager.  

### <a name="use-dedicated-iis-servers-for-configuration-manager"></a>Použití vyhrazených serverů IIS pro Configuration Manager

I když můžete hostovat několik webových aplikací na serverech IIS, které používá i Configuration Manager, tento postup může významně zvýšit plochu útoku. Nesprávně nakonfigurovaná aplikace by mohla útočníkovi umožnit získat kontrolu nad Configuration Manager systému lokality. Toto porušení může útočníkovi umožnit získat kontrolu nad hierarchií.  

Pokud je nutné spustit další webové aplikace v Configuration Manager systémy lokality, vytvořte vlastní web pro Configuration Manager systémy lokality.  

### <a name="use-a-custom-website"></a>Použití vlastního webu

Pro systémy lokality, na nichž je spuštěna služba IIS, nakonfigurujte Configuration Manager pro použití vlastního webu místo výchozího webu. Pokud je nutné spustit další webové aplikace v systému lokality, je nutné použít vlastní web. Toto nastavení je nastavení pro celá lokalita, nikoli nastavení konkrétního systému lokality.  

### <a name="when-you-use-custom-websites-remove-the-default-virtual-directories"></a>Pokud používáte vlastní weby, odeberte výchozí virtuální adresáře.

Když změníte nastavení z použití výchozího webu na používání vlastního webu, Configuration Manager staré virtuální adresáře neodstraňují. Odeberte virtuální adresáře, které Configuration Manager původně vytvořené pod výchozím webem.  

Odeberte například následující virtuální adresáře pro distribuční bod:  

- SMS_DP_SMSPKG$  

- SMS_DP_SMSSIG$  

- NOCERT_SMS_DP_SMSPKG$  

- NOCERT_SMS_DP_SMSSIG$  

### <a name="follow-iis-server-security-guidance"></a>Sledujte pokyny pro zabezpečení serveru IIS.

Identifikujte a postupujte podle obecných pokynů pro vaši verzi serveru IIS. Vezměte v úvahu všechny požadavky, které Configuration Manager mají pro určité role systému lokality. Další informace najdete v tématu [Požadované součásti lokality a systému lokality](../configs/site-and-site-system-prerequisites.md).  


## <a name="security-guidance-for-the-management-point"></a><a name="BKMK_Security_ManagementPoint"></a>Bezpečnostní pokyny pro bod správy

Body správy jsou primárním rozhraním mezi zařízeními a Configuration Manager. Zvažte útoky proti bodu správy a serveru, na kterém je spuštěný, aby byly vysoké riziko, a vhodným způsobem je zmírnit. Pro neobvyklou aktivitu použijte všechna vhodná bezpečnostní doporučení a monitorování.  

Následující pokyny vám pomůžou zabezpečit bod správy v Configuration Manager.  

### <a name="assign-the-client-on-a-management-point-to-the-same-site"></a>Přiřazení klienta v bodu správy ke stejné lokalitě

Vyhněte se situaci, kdy přiřadíte klienta Configuration Manager, který je v bodu správy, do jiné lokality, než je lokalita bodu správy.  

Pokud migrujete ze starší verze nástroje na Configuration Manager aktuální větev, migrujte klienta v bodu správy na novou lokalitu, jakmile to bude možné.  


## <a name="security-guidance-for-the-fallback-status-point"></a><a name="BKMK_Security_FSP"></a>Pokyny k zabezpečení pro bod stavu pro použití náhradní lokality

Pokud instalujete záložní stavový bod v Configuration Manager, postupujte podle následujících pokynů k zabezpečení:

Další informace o požadavcích na zabezpečení při instalaci bodu stavu pro použití náhradní lokality najdete v tématu [určení, zda potřebujete bod stavu pro použití náhradní lokality](../../clients/deploy/plan/determine-the-site-system-roles-for-clients.md#fallback-status-point).  

### <a name="dont-run-any-other-roles-on-the-same-site-system"></a>Nespouštějte žádné jiné role na stejném systému lokality.

Bod záložního stavu je navržený tak, aby přijímal neověřenou komunikaci z libovolného počítače. Pokud spouštíte tuto roli systému lokality s jinými rolemi nebo řadičem domény, riziko tohoto serveru se významně zvyšuje.  

### <a name="install-the-fallback-status-point-before-you-install-clients-with-pki-certificates"></a>Nainstalujte záložní stavový bod před instalací klientů s certifikáty PKI.

Pokud Configuration Manager systémy lokality nepřijímají komunikaci klienta HTTP, možná nevíte, že klienti nejsou spravováni kvůli problémům s certifikáty PKI. Pokud přiřazujete klienty k bodu stavu pro použití náhradní lokality, nahlásí tyto problémy s certifikátem prostřednictvím záložního stavového bodu.  

Z bezpečnostních důvodů nelze klientům po instalaci přiřadit záložní stavový bod. Tuto roli můžete přiřadit jenom během instalace klienta.  

### <a name="avoid-using-the-fallback-status-point-in-the-perimeter-network"></a>Nepoužívejte bod stavu pro použití náhradní lokality v hraniční síti.

Konstrukce umožňuje, aby bod stavu pro použití náhradní lokality přijímal data od kteréhokoliv klienta. I když bod záložního stavu v hraniční síti může pomoct při odstraňování potíží s internetovými klienty, vyvážit výhody při odstraňování potíží s rizikem systému lokality, který přijímá neověřená data ve veřejně přístupné síti.  

Pokud nainstalujete bod záložního stavu do hraniční sítě nebo nějaké nedůvěryhodné sítě, nakonfigurujte server lokality tak, aby inicializoval přenosy dat. Nepoužívejte výchozí nastavení, které umožňuje, aby bod záložního stavu inicializoval připojení k serveru lokality.  


## <a name="security-issues-for-site-administration"></a><a name="BKMK_SecurityIssues_Clients"></a>Problémy se zabezpečením pro správu lokality

Přečtěte si následující problémy se zabezpečením pro Configuration Manager:  

- Configuration Manager nemá žádnou ochranu proti oprávněnému administrativnímu uživateli, který používá Configuration Manager k útoku na síť. Neoprávnění uživatelé s právy pro správu jsou vysoce bezpečnostní riziko. Mohli by spustit mnoho útoků, mezi které patří následující strategie:  

    - Nasazení softwaru použijte k automatické instalaci a spuštění škodlivého softwaru na každém Configuration Manager klientském počítači v organizaci.  

    - Vzdálené řízení klienta Configuration Manager bez oprávnění klienta.  

    - Konfigurace rychlých intervalů cyklického dotazování a extrémních objemů inventáře. Tato akce vytvoří útoky typu útok na služby na klienty a servery.  

    - Použití jedné lokality v hierarchii k zápisu dat do dat služby Active Directory jiné lokality.  

    Hierarchie lokality je hranicí zabezpečení. Berte v úvahu jenom lokality, které budou mít hranice správy.  

    Proveďte audit aktivity všech uživatelů s právy pro správu a pravidelně kontrolujte protokoly z těchto auditů Vyžadovat, aby všichni Configuration Manager administrativních uživatelů prošli kontrolou na pozadí před jejich přijetím. Vyžadovat pravidelnou kontrolu jako podmínku zaměstnanosti.  

- Pokud dojde k ohrožení bezpečnosti bodu registrace, útočník by mohl získat certifikáty pro ověřování. Mohli by ukrást přihlašovací údaje uživatelů, kteří si zaregistrují svá mobilní zařízení.  

    Bod registrace komunikuje s certifikační autoritou. Může vytvářet, upravovat a odstraňovat objekty služby Active Directory. Nikdy neinstalujte bod registrace do hraniční sítě. Vždy monitorovat neobvyklou aktivitu.  

- Pokud povolíte zásady uživatele pro internetovou správu klientů, zvýšíte svůj profil útoku.  

    Kromě používání certifikátů PKI pro připojení mezi klientem a serverem vyžadují tyto konfigurace ověřování systému Windows. Můžou se vrátit k použití ověřování NTLM místo protokolu Kerberos. Ověřování pomocí protokolu NTLM je zranitelné vůči útokům využívajícím zosobnění a nahrazení. Chcete-li úspěšně ověřit uživatele na internetu, je nutné, abyste povolili připojení z internetového systému lokality k řadiči domény.  

- Na serverech systému lokality se vyžaduje sdílená složka **admin $** .  

    Server lokality Configuration Manager používá sdílenou složku Admin $ k připojení a provádění operací služby v systémech lokality. Tuto sdílenou složku nezakažte ani neodstraňujte.  

- Configuration Manager pro připojení k ostatním počítačům používá službu překladu názvů. Tyto služby je obtížné zabezpečit před těmito útoky zabezpečení:
    - Falšování identity
    - Falšování
    - Popírání odpovědnosti
    - Zpřístupnění informací
    - Odmítnutí služby
    - Zvýšení oprávnění

    Identifikujte a dodržujte případné bezpečnostní pokyny pro verzi DNS, kterou používáte pro překlad názvů.  

## <a name="privacy-information-for-discovery"></a><a name="BKMK_Privacy_Cliients"></a>Informace o ochraně osobních údajů pro zjišťování

Zjišťování vytváří záznamy pro síťové prostředky a ukládá je do databáze Configuration Manager. Záznamy dat zjišťování obsahují informace o počítači, jako jsou například IP adresy, verze operačního systému a názvy počítačů. Můžete také nakonfigurovat metody zjišťování služby Active Directory tak, aby vracely všechny informace, které vaše organizace uchovává v Active Directory Domain Services.  

Jedinou metodou zjišťování, kterou Configuration Manager povolit ve výchozím nastavení, je zjišťování prezenčního signálu. Tato metoda zjišťuje pouze počítače, které již mají nainstalovaný klientský software Configuration Manager.  

Informace o zjišťování nejsou odesílány přímo společnosti Microsoft. Je uložený v databázi Configuration Manager. Configuration Manager uchová informace v databázi, dokud data neodstraní. K tomuto procesu dochází každých 90 dní úlohou údržby lokality **Odstranit stará data zjišťování**.  
