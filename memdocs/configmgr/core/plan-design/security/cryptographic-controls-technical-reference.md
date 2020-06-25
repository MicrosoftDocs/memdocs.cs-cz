---
title: Technické informace o kryptografických ovládacích prvcích
titleSuffix: Configuration Manager
description: Přečtěte si, jak podepisování a šifrování může přispět k ochraně útoků před čtením dat v Configuration Manager.
ms.date: 12/08/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe50aad3cb35ab5908f604560f4dcd22800919a5
ms.sourcegitcommit: 22e1095a41213372c52d85c58b18cbabaf2300ac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/25/2020
ms.locfileid: "85353441"
---
# <a name="cryptographic-controls-technical-reference"></a>Technické informace o kryptografických ovládacích prvcích

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager používá podepisování a šifrování, které vám pomůžou chránit správu zařízení v Configuration Manager hierarchii. V případě, že se data po přenosu změnila, je zahozena. Šifrování pomáhá zabránit útočníkovi v přečtení dat pomocí analyzátoru protokolu sítě.  

 Primární algoritmus hash, který Configuration Manager používá k podepisování, je SHA-256. Když vzájemně komunikují dvě Configuration Manager lokality, podepisují svoji komunikaci pomocí algoritmu SHA-256. Primární šifrovací algoritmus implementovaný v Configuration Manager je 3DES. Slouží k ukládání dat do Configuration Manager databáze a pro komunikaci klienta s protokolem HTTP. Pokud používáte komunikaci klienta přes protokol HTTPS, můžete nakonfigurovat infrastrukturu veřejných klíčů (PKI) tak, aby používala certifikáty RSA s maximálními algoritmy hash a délkou klíčů, které jsou zdokumentovány v [požadavcích na certifikát PKI](../network/pki-certificate-requirements.md).  

 Pro většinu kryptografických operací pro operační systémy Windows Configuration Manager používat algoritmy SHA-2, 3DES a AES a RSA z knihovny Windows CryptoAPI rsaenh.dll.  

> [!IMPORTANT]  
>  Viz informace o doporučovaných změnách v reakci na slabá místa zabezpečení SSL v tématu [About SSL Vulnerabilities](#about-ssl-vulnerabilities).  

##  <a name="cryptographic-controls-for-configuration-manager-operations"></a>Ovládání kryptografie pro operace Configuration Manager  
 Informace v Configuration Manager můžou být podepsané a šifrované bez ohledu na to, jestli používáte certifikáty PKI s Configuration Manager.  

### <a name="policy-signing-and-encryption"></a>Podepisování a šifrování zásad  
 Přiřazení zásad klienta se podepisují pomocí podepisovacího certifikátu serveru lokality s podpisem držitele, aby nedocházelo k bezpečnostnímu riziku narušeného bodu správy odesíláním zásad, které byly pozměněny. To je důležité, pokud používáte internetovou správu klientů, protože toto prostředí vyžaduje bod správy, který je vystavený pro internetovou komunikaci.  

 Zásada je zašifrovaná pomocí algoritmu 3DES, pokud obsahuje citlivá data. Zásady obsahující citlivá data jsou odesílány pouze autorizovaným klientům. Zásady, které neobsahují citlivá data nejsou šifrovány.  

 Když jsou zásady uložené na klientech, zašifrují se pomocí programovacího rozhraní aplikace ochrany dat (DPAPI).  

### <a name="policy-hashing"></a>Hashování zásad  
 Když klienti vyžadují zásadu Configuration Manager, nejprve získají přiřazení zásady, takže vědí, které zásady pro ně platí a pak požadují jenom tyto orgány zásad. Každé přiřazení zásady obsahuje vypočtený hash pro příslušné tělo zásady. Klient načte platná těla zásad a pak vypočte hash k tomuto tělu. Pokud se hash ve staženém těle zásady neshoduje s hash klíčem v přiřazení zásady, pak klient tělo zásady zahodí.  

 Algoritmus hash pro zásady je SHA-1 a SHA-256.  

### <a name="content-hashing"></a>Hashování obsahu  

Služba správy distribuce na serveru lokality hashuje soubory obsahu pro všechny balíčky. Poskytovatel zásad zahrnuje hash klíče do zásad distribuce softwaru. Když klient Configuration Manager stáhne obsah, klient znovu vygeneruje hash místně a porovná ho s rozhraním zadaným v zásadách. Pokud se klíče hash shodují, pak nebyl obsah pozměněn a klient ho nainstaluje. Pokud byl jediný bajt obsahu pozměněn, pak se klíče hash neshodují a software nebude nainstalován. Tato kontrola pomáhá zajistit, že bude nainstalován správný software, jelikož skutečný obsah je kontrolován oproti zásadě.  

Výchozí algoritmus hash pro obsah je SHA-256.

Ne všechna zařízení mohou podporovat hashování obsahu. Mezi výjimky patří:  

- Klienti systému Windows, kteří streamují obsah App-V.  

- Klienti Windows Phone, i když tito klienti ověřují podpis aplikace, která je podepsaná důvěryhodným zdrojem.  

- Klient Windows RT, i když tito klienti ověřují podpis aplikace, která je podepsaná důvěryhodným zdrojem, a také používají ověřování celého názvu balíčku (PFN).  

- Klienti, kteří jsou spuštění na verzích systémů Linux a UNIX, které nepodporují šifrování SHA-256. Další informace najdete v tématu [Plánování nasazení klienta na počítače se systémy Linux a UNIX](../../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md).  

### <a name="inventory-signing-and-encryption"></a>Podepisování a šifrování inventáře  
 Inventář, který klienti zasílají do bodů správy je vždy podepisován pomocí zařízení, nezávisle na tom, zda zařízení komunikují s body správy pomocí protokolu HTTP nebo HTTPS. Pokud používají protokol HTTP, můžete si zvolit šifrování těchto dat, což je nejlepší postup zabezpečení.  

### <a name="state-migration-encryption"></a>Šifrování migrace stavu  
 Data uložená v bodech stavu migrace pro nasazení operačního systému jsou vždy šifrována pomocí nástroje přenesení stavu uživatele (USMT) pomocí 3DES.  

### <a name="encryption-for-multicast-packages-to-deploy-operating-systems"></a>Šifrování pro balíčky pro vícesměrové vysílání pro nasazení operačních systémů  
 Při přenosu balíčku pomocí vícesměrového vysílání máte možnost povolit šifrování, a to v případě každého balíčku nasazení operačního systému. Šifrování používá rozšířený standard šifrování (AES). Pokud šifrování povolíte, nebude vyžadována konfigurace dalšího certifikátu. Distribuční bod s povoleným vícesměrovým vysíláním automaticky vygeneruje symetrické klíče pro šifrování balíčku. Každý balíček obsahuje odlišný šifrovací klíč. Klíče je uložen v distribučním bodě s vícesměrovým vysíláním pomocí standardních API systému Windows. Když se klient připojí do relace vícesměrového vysílání, dojde k výměně klíčů pomocí šifrovaného kanálu pomocí certifikátu ověřování klienta vydaného PKI (pokud klient používá protokol HTTPS) nebo certifikátu podepsaného držitelem (pokud klient používá protokol HTTP). Klient uloží klíč do paměti pouze po dobu trvání relace vícesměrového vysílání.  

### <a name="encryption-for-media-to-deploy-operating-systems"></a>Šifrování médií pro nasazení operačních systémů  
 Použijete-li k nasazení operačních systémů médium a zadáte heslo pro ochranu média, jsou proměnné prostředí šifrovány pomocí standard AES (Advanced Encryption Standard) (AES) s 128 bitovou velikostí klíče. Další data v médiu, včetně balíčků a obsahu aplikací, nejsou šifrována.  

### <a name="encryption-for-content-that-is-hosted-on-cloud-based-distribution-points"></a>Šifrování obsahu, který je hostován v cloudových distribučních bodech  
 Od verze System Center 2012 Configuration Manager SP1 Pokud používáte cloudové distribuční body, je obsah, který nahrajete do těchto distribučních bodů, zašifrovaný pomocí standard AES (Advanced Encryption Standard) (AES) s velikostí klíče 256. Obsah je znovu zašifrován kdykoliv ho aktualizujete. Pokud klient stáhne obsah, je zašifrován a chráněn pomocí připojení HTTPS.  

### <a name="signing-in-software-updates"></a>Přihlášení k aktualizacím softwaru  
 Veškeré softwarové aktualizace musí být podepsány důvěryhodným vydavatelem jako ochrana proti manipulaci. V klientských počítačích agent Windows Update (WUA) skenuje aktualizace z katalogu, ale neinstaluje je, pokud nemůže najít digitální certifikát v úložišti důvěryhodných vydavatelů v místním počítači. Pokud byl certifikát podepsaný držitelem použit pro publikaci katalogu aktualizací, například certifikát WSUS vydavatelů podepsaný držitelem, musí se také nacházet v úložišti certifikátů úřadu pro vydávání důvěryhodných kořenových certifikátů. WUA také kontroluje, zda je nastavení **Povolit podepsaný obsah ze skupiny zásad služby Microsoft Update intranetu** povoleno v místním počítači. Toto nastavení zásady musí být povoleno, aby mohl nástroj WUA skenovat aktualizace, které byly vytvořeny a publikovány pomocí nástroje Updates Publisher.  

 Jsou-li softwarové aktualizace publikovány v nástroji System Center Updates Publisher, digitální certifikát podepisuje softwarové aktualizace, když jsou publikovány na server aktualizací. Můžete buď určit certifikát PKI nebo provést konfiguraci nástroje Updates Publisher a vygenerovat certifikát podepsaný držitelem pro podepisování softwarových aktualizací.  

### <a name="signed-configuration-data-for-compliance-settings"></a>Podepsaná data konfigurace pro nastavení dodržování předpisů  
 Když importujete konfigurační data, Configuration Manager ověří digitální podpis souboru. Pokud nebyly soubory podepsány, nebo pokud digitální podpis ověření selže, budete varováni vyzváni, zda chcete pokračovat v importu. V importu konfiguračních dat pokračuje pouze v případě, že výhradně důvěřujete vydavateli a integritě souborů.  

### <a name="encryption-and-hashing-for-client-notification"></a>Šifrování a hashování pro klientské oznámení  
 Pokud použijete oznámení klienta, bude veškerá komunikace používat TLS a nejlepší šifrování, jaké dokáže server a operační systémy klienta vyjednat. Například klientský počítač se systémem Windows 7 a bod správy s Windows Serverem 2008 R2 může podporovat šifrování AES (128), zatímco klientský počítač se systémem Vista se stejným bodem správy bude vyjednávat z hlediska šifrování 3DES. Ke stejnému vyjednávání dochází při hashování balíčků, které jsou přenášeny během oznámení klienta, které používá SHA-1 nebo SHA-2.  

##  <a name="certificates-used-by-configuration-manager"></a>Certifikáty, které používá Configuration Manager  
 Seznam certifikátů infrastruktury veřejných klíčů (PKI), které mohou používat Configuration Manager, všechny zvláštní požadavky nebo omezení a způsob používání certifikátů najdete v tématu [požadavky na certifikát PKI](../network/pki-certificate-requirements.md). Tento seznam obsahuje podporované hashovací algoritmy a délky klíčů. Většina certifikátů podporuje klíče SHA-256 a délku klíče 2 048 bitů.  

> [!NOTE]  
>  Všechny certifikáty, které Configuration Manager používá, musí v názvu subjektu nebo alternativním názvu subjektu obsahovat pouze jednobajtové znaky.  

 Certifikáty PKI jsou nezbytné pro následující scénáře:  

- Když spravujete Configuration Manager klientů na internetu.  

- Když spravujete Configuration Manager klienty na mobilních zařízeních.  

- Při správě počítačů se systémem Mac.  

- Pokud používáte cloudové distribuční body.  

  Pro většinu dalších Configuration Manager komunikací, které vyžadují certifikáty pro ověřování, podepisování nebo šifrování, Configuration Manager automaticky používá certifikáty PKI, pokud jsou k dispozici. Pokud nejsou k dispozici, Configuration Manager generuje certifikáty podepsané svým držitelem.  

  Configuration Manager nepoužívá certifikáty PKI při správě mobilních zařízení pomocí konektoru systému Exchange Server.  

### <a name="mobile-device-management-and-pki-certificates"></a>Správa mobilních zařízení a certifikátů PKI  
 Pokud mobilní zařízení není uzamčené mobilním operátorem, můžete k vyžádání a instalaci klientského certifikátu použít Configuration Manager nebo Microsoft Intune. Tento certifikát zajišťuje vzájemné ověření mezi klientem v mobilním zařízení a Configuration Manager systémy lokality nebo služby Microsoft Intune. Pokud je mobilní zařízení uzamčené, nemůžete k nasazení certifikátů použít Configuration Manager ani Intune.  

 Pokud povolíte inventář hardwaru pro mobilní zařízení, Configuration Manager nebo Intune také inventarizaci certifikátů, které jsou nainstalované v mobilním zařízení.   

### <a name="operating-system-deployment-and-pki-certificates"></a>Nasazení operačního systému a certifikáty PKI  
 Použijete-li Configuration Manager k nasazení operačních systémů a bod správy vyžaduje připojení klienta pomocí protokolu HTTPS, musí mít klientský počítač také certifikát pro komunikaci s bodem správy, i když je v přechodné fázi, jako je například spuštění z média pořadí úloh nebo distribuční bod s povoleným PXE. Pro podporu tohoto scénáře musíte vytvořit certifikát ověřování klienta PKI a exportovat ho pomocí privátního klíče a pak ho importovat do vlastností serveru lokality a také přidat důvěryhodný kořenový certifikát CA bodu správy.  

 Pokud vytváříte spustitelné médium, importujete certifikát ověřování klienta, když vytvoříte spustitelné médium. Proveďte konfiguraci hesla spustitelného média jako pomoc při ochraně soukromého klíče a dalších citlivých dat konfigurovaných v pořadí úloh. Každý počítač, který se spouští ze spustitelného média poskytne bodu správy stejný certifikát, což je požadavek pro funkce klienta, například požadavek na zásady klienta.  

 Pokud použijete spouštění PXE, provedete import certifikátu ověřování klienta do distribučního bodu s povoleným PXE a ten použije stejný certifikát na všechny klienty, kteří se spouští z tohoto distribučního bodu s povoleným PXE. Nejlepším postupem zabezpečení je vyžadovat od uživatelů, kteří připojují své počítače ke službě PXE, aby zadali heslo, které pomáhá chránit soukromý klíč a další citlivá data v pořadí úloh.  

 Pokud dojde k narušení kteréhokoliv z těchto certifikátů ověřování klienta, zablokujte je v uzlu **Certifikáty** v pracovním prostoru **Správa** v uzlu **Zabezpečení** . Chcete-li spravovat tyto certifikáty, musíte mít oprávnění **Správa certifikátu nasazení operačního systému** .  

 Po nasazení operačního systému a nainstalování Configuration Manager bude klient vyžadovat vlastní certifikát ověřování klienta PKI pro komunikaci klienta pomocí protokolu HTTPS.  

### <a name="isv-proxy-solutions-and-pki-certificates"></a>Řešení ISV proxy a certifikáty PKI  
 Nezávislí výrobci softwaru (ISV) mohou vytvářet aplikace, které přesahují Configuration Manager. Například může ISV vytvořit rozšíření, které podporují klientské platformy nevyužívající systém Windows, například počítače se systémem Macintosh nebo UNIX. Pokud ale systémy lokality vyžadují připojení ke klientům přes HTTPS, musí tito klienti používat ke komunikaci s lokalitou taky certifikáty PKI. Configuration Manager zahrnují možnost přiřadit certifikát k ISV proxy, který umožňuje komunikaci mezi klienty ISV proxy a bodem správy. Pokud použijete rozšíření, které vyžaduje certifikáty ISV proxy, obraťte se na dokumentaci daného produktu. Další informace o tom, jak vytvořit certifikáty ISV proxy, najdete v sadě Configuration Manager Software Developer Kit (SDK).  

 Pokud dojde k ohrožení bezpečnosti certifikátu ISV, zablokujte certifikát v uzlu **Certifikáty** v pracovním prostoru **Správa** , uzel **Zabezpečení** .  

### <a name="asset-intelligence-and-certificates"></a>Funkce Asset Intelligence a certifikáty  
 Configuration Manager se nainstaluje s certifikátem X. 509, který bod synchronizace funkce Asset Intelligence používá pro připojení k Microsoftu. Configuration Manager používá tento certifikát k vyžádání certifikátu ověřování klienta z certifikační služby společnosti Microsoft. Certifikát ověřování klienta je nainstalován v bodě synchronizace služby Asset Intelligence serveru systému lokality a používá se k ověřování serveru ve společnosti Microsoft. Nástroj Configuration Manager používání certifikát ověřování klienta ke stahování katalogu služby Asset Intelligence a k nahrávání názvů softwaru.  

 Tento certifikát obsahuje klíč o délce 1 024 bitů.  

### <a name="cloud-based-distribution-points-and-certificates"></a>Cloudové distribuční body a certifikáty  
 Od verze System Center 2012 Configuration Manager SP1 cloudové distribuční body vyžadují certifikát pro správu (podepsaný držitelem nebo PKI), který nahrajete do Microsoft Azure. Certifikát pro správu vyžaduje schopnost ověřování serveru a délku klíče certifikátu o hodnotě 2 048 bitů. Navíc je nutné provést konfiguraci certifikátu služby pro každý cloudový distribuční bod, který nemůže být podepsaný držitelem, ale také obsahuje schopnost ověřování serveru a má minimální dílku klíče certifikátu o hodnotě 2 048 bitů.  

> [!NOTE]  
>  Certifikát pro správu podepsaný držitelem je určen pouze pro testovací účely a není určen pro použití ve výrobních sítích.  

 Klienti nevyžadují, aby certifikát klienta PKI používal cloudové distribuční body. Klienti provádí ověřování oproti správě pomocí certifikátu podepsaného držitelem nebo certifikátu PKI klienta. Bod správy poté vydá přístup k Configuration Manager přístupovému tokenu klientovi, který klient prezentuje v cloudovém distribučním bodě. Token platí po dobu 8 hodin.  

### <a name="the-microsoft-intune-connector-and-certificates"></a>Konektor Microsoft Intune a certifikáty  
 Když Microsoft Intune zaregistruje mobilní zařízení, můžete tato mobilní zařízení spravovat v Configuration Manager vytvořením konektoru Microsoft Intune. Konektor využívá certifikát PKI se schopností ověřování klienta k ověření Configuration Manager k Microsoft Intune a k přenosu všech informací mezi nimi pomocí protokolu SSL. Délka klíče certifikátu činí 2048 bitů a využívá hashovací algoritmus SHA-1.  

 Po instalaci konektoru dojde k vytvoření a uložení podepisovacího certifikátu na serveru lokality pro klíče zkušebního načtení a vytvoření a uložení šifrovacího certifikátu v bodě registrace certifikátu pro zašifrování výzvy protokolu SCEP (Simple Certificate Enrollment Protocol). Tyto certifikáty také mají velikost klíče o hodnotě 2 048 bitů a využívají hashovací algoritmus SHA-1.  

 Když Intune zaregistruje mobilní zařízení, nainstaluje na mobilní zařízení certifikát PKI. Tento certifikát má schopnost ověřování klienta, používá klíč o délce 2 048 bitů a využívá hashovací algoritmus SHA-1.  

 Tyto certifikáty PKI se automaticky vyžádají, vygenerují a nainstalují pomocí Microsoft Intune.  

### <a name="crl-checking-for-pki-certificates"></a>Kontrola CRL pro certifikáty PKI  
 Seznam odvolaných certifikátů PKI (CRL) zvyšuje režii správy a zpracování, ale je bezpečnější. Pokud je však kontrola CRL povolena, ale CRL je nedostupné, připojení PKI selže. Další informace najdete v tématu [zabezpečení a ochrana osobních údajů pro Configuration Manager](security-and-privacy.md).  

 Kontrola seznamu odvolaných certifikátů (CRL) je ve výchozím nastavení povolena ve službě IIS, takže pokud používáte seznam CRL s nasazením PKI, není pro většinu Configuration Manager systémů lokalit, které spouští službu IIS, konfigurováno žádné další konfigurace. Výjimkou jsou softwarové aktualizace, které vyžadují ruční krok k povolení kontroly CRL pro ověření podpisů v souborech softwarových aktualizací.  

 Kontrola CRL je ve výchozím nastavení povolena pro klientské počítače, pokud používají připojení klientů protokolu HTTPS. Nemůžete zakázat kontrolu CRL pro klienty na počítačích Mac v Configuration Manager SP1 nebo novějším.  

 Kontrola CRL není podporovaná pro následující připojení v Configuration Manager:  

-   Vzájemné připojení serverů.  

-   Mobilní zařízení zaregistrovaná službou Configuration Manager.  

-   Mobilní zařízení zaregistrovaná službou Microsoft Intune.  

##  <a name="cryptographic-controls-for-server-communication"></a>Ovládání kryptografie pro komunikaci serveru  
 Configuration Manager používá následující kryptografické ovládací prvky pro komunikaci serveru.  

### <a name="server-communication-within-a-site"></a>Komunikace serveru v rámci lokality  
 Každý server systému lokality používá certifikát k přenosu dat do dalších systémů lokality ve stejné Configuration Manager lokalitě. Některé role systému lokality také používají certifikáty pro ověřování. Pokud například nainstalujete zprostředkující bod registrace na jeden server a bod registrace na druhý server, mohou se ověřit navzájem pomocí tohoto certifikátu identity. Pokud Configuration Manager používá certifikát pro tuto komunikaci, pokud je k dispozici certifikát PKI, který má schopnost ověřování serveru, Configuration Manager ho automaticky používá. Pokud ne, Configuration Manager vygeneruje certifikát podepsaný svým držitelem. Tento certifikát podepsaný držitelem obsahuje schopnost ověřování serveru, využívá algoritmus SHA-256 a má délku klíče 2048 bitů. Configuration Manager zkopíruje certifikát do úložiště důvěryhodných osob na dalších serverech systému lokality, které by mohly potřebovat důvěřovat systému lokality. Systémy lokality si následně mohou důvěřovat navzájem pomocí těchto certifikátů a služby PeerTrust.  

 Kromě tohoto certifikátu pro každý server systému lokality Configuration Manager vygeneruje certifikát podepsaný svým držitelem pro většinu rolí systému lokality. Pokud se v jedné lokalitě nachází více než jedna instance role systému lokality, pak sdílí stejný certifikát. Například můžete mít více bodů správy nebo více bodů zápisu ve stejné lokalitě. Tento certifikát podepsaný držitelem také používá algoritmus SHA-256 a obsahuje klíč o délce 2048 bitů. Je také zkopírován do úložiště důvěryhodných osob na serverech systému lokality, u kterých je nutné, aby mu důvěřovaly Tento certifikát generují následující role systému lokality:  

- Bod služeb webu Katalog aplikací  

- Bod webu Katalog aplikací  

- Bod synchronizace katalogu Asset Intelligence  

- Bod registrace certifikátu  

- Bod ochrany koncového bodu Endpoint Protection  

- Bod registrace  

- Bod záložního stavu  

- Bod správy  

- Distribuční bod s povoleným vícesměrovým vysíláním  

- Bod služby Reporting services  

- Bod aktualizace softwaru  

- Bod migrace stavu  

- Konektor služby Microsoft Intune  

Tyto certifikáty jsou spravovány automaticky pomocí Configuration Manager a v případě potřeby automaticky vygenerovány.  

Configuration Manager používá taky certifikát pro ověřování klientů k posílání stavových zpráv z distribučního bodu do bodu správy. Pokud je konfigurace bodu správy pro samotná připojení klienta provedena pouze pomocí protokolu HTTPS, je nutné použít certifikát PKI. Pokud bod správy přijme připojení protokolu HTTP, můžete certifikát PKI použít nebo vyberte možnost k použití certifikátu podepsaného držitelem, který má schopnosti ověřování klienta, používá algoritmus SHA-256 a má délku klíče 2 048 bitů.  

### <a name="server-communication-between-sites"></a>Komunikace serveru mezi lokalitami  
 Configuration Manager přenáší data mezi lokalitami pomocí replikace databáze a replikace na základě souborů. Další informace najdete v tématu [komunikace mezi koncovými body](../hierarchy/communications-between-endpoints.md).  

 Configuration Manager automaticky konfiguruje replikaci databáze mezi lokalitami a používá certifikáty PKI, které mají schopnost ověřování serveru, pokud jsou k dispozici. v takovém případě Configuration Manager vytvoří certifikáty podepsané držitelem pro ověřování serveru. V obou případech bude ověřování mezi lokalitami zahájeno pomocí certifikátů v úložišti důvěryhodných osob, které používají službu PeerTrust. Toto úložiště certifikátů se používá k zajištění, aby se replikace mezi lokalitami účastnila pouze SQL Server počítačů, které jsou používány Configuration Manager hierarchii. Zatímco primární lokality a centrální lokality pro správu mohou replikovat změny konfigurace pro všechny lokality v hierarchii, sekundární lokality mohou replikovat změny konfigurace pouze v podřízené lokalitě.  

 Servery lokality zahajují vzájemnou komunikace lokalit pomocí zabezpečené výměny klíčů, ke které dochází automaticky. Zasílající server lokality generuje součet hash a podepíše ho pomocí soukromého klíče. Přijímající server lokality zkontroluje podpis pomocí veřejného klíče a porovná součet hash s místně vygenerovanou hodnotou. Pokud se shodují, přijímající lokalita přijme replikovaná data. Pokud se hodnoty neshodují, Configuration Manager odmítne data replikace.  

 Replikace databáze v Configuration Manager používá SQL Server Service Broker k přenosu dat mezi lokalitami pomocí následujících mechanismů:  

- Připojení mezi systémy SQL Server: Tento mechanismus využívá přihlašovací údaje Windows k ověření serveru a certifikátů podepsaných držitelem s 1 024 bity k podepisování a šifrování dat pomocí standardu AES (Advanced Encryption Standard). Pokud jsou dostupné certifikáty PKI se schopností ověřování serveru, budou použity. Certifikát se musí nacházet v osobním úložišti úložiště certifikátů počítače.  

- Služba SQL Service Broker: Tato služba využívá certifikáty podepsané držitelem s 2 048 bity k ověřování a k podepisování a šifrování dat pomocí standardu AES (Advanced Encryption Standard). Certifikát se musí nacházet v hlavní databázi systému SQL Server.  

  Replikace na základě souborů využívá protokol SMB (Server Message Block) a využívá algoritmus SHA-256 k podepisování dat, která nejsou šifrována, ale neobsahují citlivé údaje. Chcete-li tato data zašifrovat, můžete použít protokol IPsec a tuto možnost je nutné implementovat nezávisle na Configuration Manager.  

##  <a name="cryptographic-controls-for-clients-that-use-https-communication-to-site-systems"></a>Ovládání kryptografie pro klienty, kteří používají komunikaci pomocí protokolu HTTPS se systémy lokality  
 Pokud role systému lokality přijme připojení klienta, můžete je konfigurovat k přijímání připojení protokolů HTTPS a HTTP nebo pouze připojení HTTPS. Role systému lokality, které přijímají připojení z Internetu přijímají pouze připojení klienta přes protokol HTTPS.  

 Připojení klienta přes protokol HTTPS nabízí vyšší úroveň zabezpečení integrací s infrastrukturou veřejných klíčů (PKI) a pomáhají chránit komunikace mezi klientem a serverem. Konfigurace připojení klientů HTTPS bez pečlivého pochopení plánování, nasazení a činností PKI vás přesto může zanechat zranitelné. Pokud například nezabezpečíte kořenové CA, útočníci mohou narušit důvěru celé infrastruktury PKI. Pokud nenasadíte a nespravujete certifikáty PKI pomocí kontrolovaných a zabezpečených procesů, může dojít k situaci, že nespravovaní klienti nebudou moci přijímat klíčové softwarové aktualizace nebo balíčky.  

> [!IMPORTANT]  
>  Certifikáty PKI, které se používají ke komunikaci klientů, chrání komunikaci pouze mezi klientem a některými systémy lokality. Nechrání komunikační kanál mezi serverem lokality a systémy lokality nebo mezi servery lokalit.  

### <a name="communication-that-is-unencrypted-when-clients-use-https-communication"></a>Nešifrovaná komunikace, pokud klienti používají komunikaci pomocí protokolu HTTPS  
 Pokud klienti komunikují se systémy lokalit pomocí protokolu HTTPS, bude komunikace obvykle šifrována pomocí SSL. V následujících situacích však klienti komunikují se systémy lokalit bez použití šifrování:  

- Klientovi se nepodaří vytvořit připojení pomocí protokolu HTTPS na intranetu a vrátí se zpět k použití protokolu HTTP, pokud systémy lokality tuto konfiguraci umožňují.  

- Komunikace s následujícími rolemi systému lokality:  

  -   Klient odešle stavové zprávy do bodu stavu pro použití náhradní lokality  

  -   Klient odešle požadavky PXE do distribučního bodu s povoleným PXE  

  -   Klient odešle data oznámení do bodu správy  

  Body služeb generování sestav jsou konfigurovány k použití protokolu HTTP nebo HTTPS nezávisle na režimu komunikace klienta.  

##  <a name="cryptographic-controls-for-clients-chat-use-http-communication-to-site-systems"></a>Ovládání kryptografie pro klienty konverzace použít komunikaci pomocí protokolu HTTP se systémy lokality  
 Pokud klienti používají komunikaci pomocí protokolu HTTP s rolemi systému lokality, mohou používat certifikáty PKI pro ověřování klienta nebo certifikáty podepsané držitelem, které Configuration Manager generuje. Když Configuration Manager generuje certifikáty podepsané svým držitelem, mají vlastní identifikátor objektu pro podepisování a šifrování a tyto certifikáty se používají k jednoznačné identifikaci klienta. Pro všechny podporované operační systémy kromě systému Windows Server 2003 tyto certifikáty podepsané držitelem používají technologii SHA-256 a délku klíče 2 048 bitů. Pro systém Windows Server 2003 se používá technologie SHA1 s délkou klíče 1 024 bitů.  

### <a name="operating-system-deployment-and-self-signed-certificates"></a>Nasazení operačního systému a certifikáty podepsané svým držitelem  
 Při použití Configuration Manager k nasazení operačních systémů s certifikáty podepsanými držitelem musí mít klientský počítač také certifikát pro komunikaci s bodem správy, a to i v případě, že je počítač v přechodové fázi, například spouštění z média pořadí úloh nebo distribučního bodu s povoleným PXE. Pro podporu tohoto scénáře pro připojení klienta pomocí protokolu HTTP Configuration Manager vygeneruje certifikáty podepsané držitelem, které mají vlastní identifikátor objektů pro podepisování a šifrování. Tyto certifikáty se používají k jednoznačné identifikaci klienta. Pro všechny podporované operační systémy kromě systému Windows Server 2003 tyto certifikáty podepsané držitelem používají technologii SHA-256 a délku klíče 2 048 bitů. Pro systém Windows Server 2003 se používá technologie SHA1 s délkou klíče 1 024 bitů. Pokud dojde k ohrožení těchto certifikátů podepsaných držitelem a chcete-li útočníkům zabránit v jejich používání za účelem vydávání se za důvěryhodné klienty, je třeba zablokovat certifikáty v uzlu **Certifikáty** v pracovním prostoru **Správa** v uzlu **Zabezpečení** .  

### <a name="client-and-server-authentication"></a>Ověřování klienta a serveru  
 Pokud se klienti připojují přes protokol HTTP, ověřují body správy pomocí Active Directory Domain Services nebo pomocí Configuration Manager důvěryhodného kořenového klíče. Klienti neověřují jiné role systému lokality, například body migrace stavu nebo body aktualizace softwaru.  

 Když bod správy poprvé ověří klienta pomocí certifikátu klienta podepsaného držitelem, tento mechanismus nabízí minimální zabezpečení, protože certifikát podepsaný držitelem může vygenerovat kterýkoli počítač. V tomto scénáři musí být proces identity klienta rozšířen o schválení. Schvalovat se musí jenom důvěryhodné počítače, a to buď automaticky Configuration Manager, nebo ručně pomocí správce. Další informace najdete v části schválení v tématu [komunikace mezi koncovými body](../hierarchy/communications-between-endpoints.md).  

## <a name="about-ssl-vulnerabilities"></a>O chybách SSL
Chcete-li zvýšit zabezpečení Configuration Manager klientů a serverů, postupujte následovně:

- Povolení protokolu TLS 1.2

  Pokud chcete povolit TLS 1,2 pro Configuration Manager, přečtěte si téma [Jak povolit tls 1,2 pro Configuration Manager](enable-tls-1-2.md).
- Zakázání SSL 3,0, TLS 1,0 a TLS 1,1 
- Změna pořadí šifrovacích sad souvisejících s protokolem TLS 

Další informace najdete v tématu [jak omezit použití určitých kryptografických algoritmů a protokolů v Schannel.dll](https://support.microsoft.com/help/245030/) a [stanovení priorit šifrovacích sad Schannel](https://docs.microsoft.com/windows/win32/secauthn/prioritizing-schannel-cipher-suites). Tyto postupy neovlivňují Configuration Manager funkce.

