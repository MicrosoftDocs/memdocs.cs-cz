---
title: Najít prostředky webu
titleSuffix: Configuration Manager
description: Naučte se, jak a kdy klienti Configuration Manager používají umístění služby k nalezení prostředků lokality.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ae72df4b-5f5d-4e19-9052-bda28edfbace
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 262234edbd6fac6973653ca6cac62853fde23b2d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700108"
---
# <a name="learn-how-clients-find-site-resources-and-services-for-configuration-manager"></a>Informace o tom, jak klienti hledají služby a prostředky lokality pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Klienti Configuration Manager používají proces nazvaný *umístění služby* k vyhledání serverů systému lokality, se kterými můžou komunikovat, a které poskytují služby směrované na použití klienty. Porozumění, jak a kdy klienti používají umístění služby k nalezení prostředků lokality, vám může pomoci nakonfigurovat vaše weby tak, aby úspěšně podporovaly úlohy klienta. Tyto konfigurace můžou vyžadovat, aby lokalita komunikovala s konfiguracemi domén a sítí, jako jsou Active Directory Domain Services (služba AD DS) a DNS. Nebo můžou vyžadovat, abyste nakonfigurovali složitější alternativy.  

Mezi role systému lokality, které poskytují služby, patří:

- Základní server systému lokality pro klienty nástroje.
- Bod správy.
- Další servery systému lokality, se kterými může klient komunikovat, jako jsou distribuční body a body aktualizace softwaru.  



##  <a name="fundamentals-of-service-location"></a><a name="bkmk_fund"></a> Základy umístění služby  
 Klient vyhodnotí svoje aktuální umístění v síti, předvolby komunikačního protokolu a přiřazenou lokalitu, když používá umístění služby k vyhledání bodu správy, se kterým může komunikovat.  

**Klient komunikuje s bodem správy na:**  
- Stáhněte si informace o dalších bodech správy pro lokalitu, aby bylo možné vytvořit seznam známých bodů správy (označovaný jako *seznam MP*) pro budoucí cykly umístění služby.  
- Odešlete podrobnosti o konfiguraci, jako je inventarizace a stav.  
- Stáhněte si zásadu, která nastavuje konfigurace na klientovi a může informovat klienta o softwaru, který může nebo musí nainstalovat, a dalších souvisejících úlohách.  
- Vyžádá informace o dalších rolích systému lokality, které poskytují služby, které jsou nakonfigurovány pro použití klientem. Mezi příklady patří distribuční body pro software, který může klient instalovat, nebo bod aktualizace softwaru, ze kterého se mají získat aktualizace.  

**Klient Configuration Manager vytvoří požadavek na umístění služby:**  
- Každých 25 hodin nepřetržité operace.  
- Když klient zjistí změnu v jeho konfiguraci nebo umístění v síti.  
- Při spuštění služby **ccmexec.exe** v počítači (jádro klientské služby).  
- Když klient musí najít roli systému lokality, která poskytuje požadovanou službu.  

**Když se klient pokouší najít servery, které jsou hostiteli rolí systému lokality**, používá umístění služby k nalezení role systému lokality, která podporuje protokol klienta (http nebo https). Ve výchozím nastavení používají klienti nejbezpečnější metodu, která je k dispozici. Zvažte použití těchto zdrojů:  

- Aby mohl používat protokol HTTPS, musíte mít infrastrukturou veřejných klíčů (PKI) a musíte mít na klientech a na serverech nainstalované certifikáty PKI. Informace o používání certifikátů najdete v tématu požadavky na [certifikát PKI pro Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

- Když nasadíte roli systému lokality, která používá službu Internet Information Services (IIS) a podporuje komunikaci od klientů, je třeba zadat, jestli se klienti připojují k systému lokality pomocí protokolu HTTP nebo HTTPS. Jestliže používáte protokol HTTP, musíte taky zvážit možnosti podepisování a šifrování. Další informace najdete v tématu  [Plánování podepisování a šifrování](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) v [plánu pro zabezpečení](../../../core/plan-design/security/plan-for-security.md).  

##  <a name="service-location-and-how-clients-determine-their-assigned-management-point"></a><a name="BKMK_Plan_Service_Location"></a> Umístění služby a jak klienti zjišťují přiřazený bod správy  
Když se klient poprvé přiřadí k primární lokalitě, vybere výchozí bod správy pro tuto lokalitu. Primární lokality podporují více bodů správy a každý klient nezávisle identifikuje bod správy jako výchozí bod správy. Tento výchozí bod správy pak bude použit jako bod správy přiřazený klientovi. (Můžete také použít příkazy instalace klienta pro nastavení přiřazeného bodu správy pro klienta při jeho instalaci.)  

Klient vybere bod správy, se kterým bude komunikovat, a to na základě aktuálního umístění v síti a konfigurací skupiny hranic. I když má přiřazený bod správy, nemusí to být bod správy, který klient používá.  

> [!NOTE]  
> Klient vždy používá přiřazený bod správy pro registrační zprávy a některé zprávy zásad, i když se ostatní komunikace posílá na proxy server nebo místní bod správy.

Můžete použít upřednostňované body správy. Preferované body správy jsou body správy z lokality přiřazené klientovi, které jsou přidruženy ke skupině hranic, kterou klient používá při hledání serverů systému lokality. Upřednostňovanou asociací bodu správy se skupinou hranic jako serverem systému lokality je podobný způsob, jakým jsou distribuční body nebo body migrace stavu přidruženy ke skupině hranic. Pokud povolíte upřednostňované body správy pro hierarchii, když klient používá bod správy z jeho přiřazené lokality, pokusí se použít upřednostňovaný bod správy před použitím jiného bodu správy z jeho přiřazené lokality.  

Můžete také použít informace na blogu [spřažení bodu správy](/archive/blogs/jchalfant/management-point-affinity-added-in-configmgr-2012-r2-cu3) ke konfiguraci spřažení bodů správy. Spřažení bodů správy přepisuje výchozí chování pro přiřazené body správy a umožňuje klientovi používat jeden nebo více konkrétních bodů správy.  

Pokaždé, když klient potřebuje kontaktovat bod správy, zkontroluje seznam MP, který je uložený místně v rozhraní WMI (Windows Management Instrumentation) (WMI). Klient vytvoří počáteční seznam MP při jeho instalaci. Klient pak pravidelně aktualizuje seznam o podrobnosti o jednotlivých bodech správy v hierarchii.  

Pokud klient nemůže v seznamu MP najít platný bod správy, prohledá následující zdroje umístění služby, dokud nenajde bod správy, který může použít:  

1.  Bod správy  
2.  AD DS  
3.  DNS  
4.  WINS  

Jakmile klient úspěšně vyhledá a kontaktuje bod správy, stáhne aktuální seznam bodů správy, které jsou v hierarchii k dispozici, a aktualizuje místní seznam MP. Platí to jak pro klienty, kteří jsou přidaní do domény, tak pro ty, kteří nejsou.  

Například pokud se klient Configuration Manager, který je na internetu, připojí k internetovému bodu správy, bod správy pošle tomuto klientovi seznam dostupných internetových bodů správy v lokalitě. Podobně klienti, kteří jsou přidaní do domény nebo jsou v pracovních skupinách, taky dostanou seznam bodů správy, které můžou používat.  

Klient, který není nakonfigurovaný pro Internet, není určený jenom pro internetové body správy. Klienti pracovní skupiny nakonfigurované pro Internet komunikují jenom s internetovými body správy.  

##  <a name="the-mp-list"></a><a name="BKMK_MPList"></a> Seznam MP  
Seznam MP je upřednostňovaným zdrojem umístění služby pro klienta, protože se jedná o prioritní seznam bodů správy, které klient předtím identifikoval. Tento seznam je seřazený podle jednotlivých klientů na základě jejich umístění v síti v době, kdy klient seznam aktualizoval a pak je uložil místně na klientovi v rozhraní WMI.  

### <a name="building-the-initial-mp-list"></a>Sestavování počátečního seznamu MP  
Během instalace klienta se při vytváření počátečního seznamu MP klienta použijí následující pravidla:  

- Počáteční seznam obsahuje body správy zadané při instalaci klienta (při použití možnosti **SMSMP**= nebo **/MP** ).  
- Klient se dotazuje služba AD DS publikovaných bodů správy. Aby bylo možné identifikovat z služba AD DS, musí být bod správy z přiřazené lokality klienta a musí mít stejnou verzi produktu jako klient.  
- Pokud během instalace klienta není zadaný žádný bod správy a schéma služby Active Directory není rozšířené, klient zkontroluje publikované body správy v DNS a WINS.  
- Když klient vytvoří počáteční seznam, informace o některých bodech správy v hierarchii nemusí být známé.  

### <a name="organizing-the-mp-list"></a>Uspořádání seznamu MP  
Klienti organizují svůj seznam bodů správy pomocí následujících klasifikací:  

- **Proxy server**: bod správy v sekundární lokalitě.  
- **Místní**: jakýkoliv bod správy, který je přidružený k aktuálnímu umístění v síti klienta podle definice hranic lokality. Poznamenejte si následující informace o hranicích:
  - Když klient patří do víc skupin hranic, seznam místních bodů správy se určí ze sjednocení všech hranic, které obsahují aktuální umístění v síti klienta.  
  - Místní body správy jsou obvykle podmnožinou přiřazených bodů správy klienta, pokud klient není v síťovém umístění, které je přidruženo k jiné lokalitě s body správy obsluhujícími svoje skupiny hranic.   


- **Přiřazený**: jakýkoliv bod správy, který je systém lokality pro lokalitu přiřazenou klientovi.  

Můžete použít upřednostňované body správy. Body správy v lokalitě, které nejsou přidružené ke skupině hranic nebo které nejsou ve skupině hranic přidružené k aktuálnímu umístění v síti klienta, se nepovažují za preferované. Budou použity, když klient nemůže identifikovat dostupný upřednostňovaný bod správy.  

### <a name="selecting-a-management-point-to-use"></a>Výběr používaného bodu správy  
Pro typickou komunikaci se klient pokusí použít bod správy z klasifikací v uvedeném pořadí podle umístění v síti klienta:  

1.  Proxy server  
2.  Místní  
3.  Přiřazené  

Klient ale vždycky používá přiřazený bod správy pro registrační zprávy a některé zprávy zásad, i když jsou ostatní komunikace odeslané na server proxy nebo místní bod správy.  

V rámci každé klasifikace (proxy, místní nebo přiřazený) se klient pokusí použít bod správy na základě předvoleb v tomto pořadí:  

1.  S podporou protokolu HTTPS v důvěryhodné nebo místní doménové struktuře (pokud je klient nakonfigurovaný pro komunikaci HTTPS)  
2.  Podporující protokol HTTPS není v důvěryhodné nebo místní doménové struktuře (Pokud je klient nakonfigurovaný pro komunikaci HTTPS)  
3.  S podporou protokolu HTTP v důvěryhodné nebo místní doménové struktuře  
4.  Nepodporující protokol HTTP v důvěryhodné nebo místní doménové struktuře  

Ze sady bodů správy seřazených podle předvoleb se klient pokusí použít první bod správy na seznamu. Tento seřazený seznam bodů správy je náhodný a nelze jej seřadit. Pořadí seznamu se může změnit pokaždé, když klient aktualizuje svůj seznam MP.  

Když klient nemůže navázat kontakt s prvním bodem správy, pokusí se na svém seznamu každý postup po sobě jdoucích bodů správy. Před vyzkoušením neupřednostňovaných bodů správy se pokusí každý upřednostňovaný bod správy v klasifikaci. Pokud klient nemůže úspěšně komunikovat s žádným bodem správy v klasifikaci, pokusí se kontaktovat preferovaný bod správy z další klasifikace, a tak dále, dokud nenajde bod správy, který se má použít.  

Poté, co klient naváže komunikaci s bodem správy, pokračuje v používání stejného bodu správy, dokud:  

- 25 hodin uplynulo.  
- Klient nemůže komunikovat s bodem správy po dobu pěti pokusů o zadání v období 10 minut.

Klient pak náhodně vybere nový bod správy, který se má použít.  

##  <a name="active-directory"></a><a name="bkmk_ad"></a> Služba Active Directory  
Klienti přidaní do domény můžou pro umístění služby použít AD DS. To vyžaduje, aby lokality [publikovaly data do Active Directory](../../servers/deploy/configure/publish-site-data.md).  

Klient nástroje může použít služba AD DS pro umístění služby, když jsou splněné všechny následující podmínky:  

- Schéma služby Active Directory [se rozšířilo](../network/extend-the-active-directory-schema.md) nebo se rozšířilo pro System Center 2012 Configuration Manager.  
- [Doménová struktura služby Active Directory je nakonfigurovaná pro publikování](../../servers/deploy/configure/publish-site-data.md)a Configuration Manager lokality jsou nakonfigurované pro publikování.  
- Klientský počítač je členem domény služby Active Directory a má přístup na server globálního katalogu.  

Pokud klient nemůže najít bod správy, který se má použít pro umístění služby z služba AD DS, pokusí se použít DNS.  

##  <a name="dns"></a><a name="bkmk_dns"></a> NÁZV  
Klienti v intranetu můžou pro umístění služby použít DNS. Aby bylo možné publikovat informace o bodech správy do DNS, musí být v hierarchii aspoň jedna lokalita.  

Zvažte pro umístění služby použití DNS, pokud je splněná některá z následujících podmínek:
- Služba AD DS schéma není rozšířeno na podporu Configuration Manager.
- Klienti v intranetu jsou umístěni v doménové struktuře, která není pro publikování Configuration Manager povolena.  
- Máte klienty na počítačích v pracovní skupině a klienti nejsou nakonfigurováni pro správu pouze internetových klientů. (Klient pracovní skupiny nakonfigurovaný pro Internet bude komunikovat jenom s internetovými body správy a nebude pro umístění služby používat DNS.)  
- Můžete [klienty nakonfigurovat tak, aby hledali body správy z DNS](../../clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md).  

Pokud lokalita publikuje záznamy umístění služby pro body správy na DNS:  

- Publikování se vztahuje jenom na body správy, které přijímají připojení klientů z intranetu.  
- Publikování přidá záznam prostředku umístění služby (SRV RR) v zóně DNS pro počítač bodu správy. Pro takový počítač musí existovat odpovídající záznam hostitele v DNS.  

Ve výchozím nastavení klienti připojení k doméně hledají záznamy bodů správy v DNS z místní domény klienta. Můžete nakonfigurovat vlastnost klienta, která určuje příponu domény pro doménu, která obsahuje informace o bodech správy publikované ve službě DNS.  

Další informace o tom, jak nakonfigurovat vlastnost klienta přípon DNS, najdete v tématu [Postup konfigurace klientských počítačů pro vyhledání bodů správy pomocí publikování DNS](../../../core/clients/deploy/configure-client-computers-to-find-management-points-by-using-dns-publishing.md).  

Pokud klient nemůže najít bod správy, který se má použít pro umístění služby z DNS, pokusí se použít službu WINS.  

### <a name="publish-management-points-to-dns"></a>Publikování bodů správy ve službě DNS  
Pokud chcete publikovat body správy ve službě DNS, musí být splněné tyto dvě podmínky:  

- Vaše servery DNS podporují zdrojové záznamy o umístění služby a využívají protokol BIND verze 8.1.2 nebo vyšší.  
- Zadané intranetové plně kvalifikované názvy domény pro body správy v Configuration Manager mají záznamy hostitele (například záznamy) ve službě DNS.  

> [!IMPORTANT]  
> Configuration Manager publikování DNS nepodporuje oddělený obor názvů. Pokud máte oddělený obor názvů, můžete publikovat body správy do služby DNS ručně nebo použít některou z dalších metod umístění služby, které jsou popsány v této části.  

**Pokud vaše servery DNS podporují automatické aktualizace**, můžete nakonfigurovat Configuration Manager pro automatické publikování bodů správy na intranetu ve službě DNS, nebo můžete tyto záznamy publikovat ručně na DNS. Pokud jsou body správy publikované ve DNS, budou jejich intranetový plně kvalifikovaný název domény a číslo portu publikované v záznamu o umístění služby (SRV). Publikování DNS se konfiguruje v lokalitě ve vlastnostech komponenty bodu správy lokality. Další informace najdete v tématu  [součásti lokality pro Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

**Pokud je vaše zóna DNS nastavená na hodnotu pouze zabezpečení pro dynamické aktualizace**, může to provést jenom první bod správy, který se má publikovat do DNS, a to úspěšně s výchozími oprávněními.

Pokud pouze jeden bod správy může úspěšně publikovat a změnit svůj záznam DNS a server bodu správy je v pořádku, mohou klienti získat úplný seznam MP z tohoto bodu správy a potom najít upřednostňovaný bod správy.


**Pokud vaše servery DNS nepodporují automatické aktualizace, ale podporují záznamy o umístění služby**, můžete body správy publikovat v DNS ručně. V takovém případě je třeba v DNS ručně zadat zdrojový záznam o umístění služby (SRV RR).  

Configuration Manager podporuje specifikaci RFC 2782 pro záznamy umístění služby. Tyto záznamy mají následující formát:   *_Service. _Proto. Name TTL Class SRV Priorita váha port cíl*  

Pokud chcete publikovat bod správy pro Configuration Manager, zadejte následující hodnoty:  

- **_Service**: zadejte **_mssms_mp**_ &lt; SiteCode \> , kde &lt; SiteCode \> je kód lokality bodu správy.  
- **._Proto**: Zadejte **._tcp**.  
- **.Name**: Zadejte příponu DNS bodu správy, třeba **contoso.com**.  
- **TTL**: Zadejte **14400**, tj. čtyři hodiny.  
- **Třída**: Zadejte **IN** (v souladu s definicí RFC 1035).  
- **Priorita**: Configuration Manager nepoužívá toto pole.
- **Váha**: Configuration Manager nepoužívá toto pole.  
- **Port**: Zadejte číslo portu, který využívá bod správy, třeba **80** pro HTTP a **443** pro HTTPS.  

  > [!NOTE]  
  >  Port záznamu SRV musí odpovídat komunikačnímu portu, který používá bod správy. Ve výchozím nastavení je to **80** pro komunikaci HTTP a **443** pro komunikaci pomocí protokolu HTTPS.  

- **Cíl**: Zadejte plně kvalifikovaný název domény intranetu zadaný pro systém lokality, který je nastavený s rolí lokality bodu správy.  

Pokud používáte službu DNS Windows Serveru, můžete k zadání tohoto záznamu pro intranetové body správy použít následující postup. Pokud pro službu DNS používáte jinou implementaci, použijte informace uvedené v této části o hodnotách polí, přečtěte si dokumentaci ke službě DNS a postup si odpovídajícím způsobem upravte.  

##### <a name="to-configure-automatic-publishing"></a>Pokud chcete konfigurovat automatické publikování:  

1.  V konzole Configuration Manager rozbalte položku **Správa**  >  **Konfigurace lokality**  >  **lokality**.  

2.  Vyberte svou lokalitu a pak zvolte **Konfigurovat součásti webu**.  

3.  Vyberte **bod správy**.  

4.  Vyberte body správy, které chcete publikovat. (Tento výběr platí pro publikování na služba AD DS a DNS.)  

5.  Zaškrtněte políčko pro publikování v DNS. Toto pole:  

    - Umožňuje vybrat, které body správy se mají publikovat na serveru DNS.  

    - Nekonfiguruje publikování na služba AD DS.  

##### <a name="to-manually-publish-management-points-to-dns-on-windows-server"></a>Ruční publikování bodů správy v DNS na Windows Serveru  

1.  V konzole Configuration Manager zadejte intranetové plně kvalifikované názvy domén systémů lokality.  

2.  V konzoli správy serverů DNS zvolte zónu DNS pro počítač bodu správy.  

3.  Ověřte, že je vytvořený záznam hostitele (A nebo AAAA) pro intranetový plně kvalifikovaný název domény systému lokality. Pokud tento záznam neexistuje, vytvořte ho.  

4.  Pomocí možnosti **nové ostatní záznamy** zvolte možnost **umístění služby (SRV)** v dialogovém okně **typ záznamu o prostředku** , zvolte možnost **vytvořit záznam**, zadejte následující informace a pak zvolte možnost **Hotovo**:  

    - **Doména**: Pokud je to nutné, zadejte příponu DNS bodu správy, například **contoso.com**.  
    - **Služba**: zadejte **_mssms_mp**_ &lt; SiteCode \> , kde &lt; SiteCode \> je kód lokality bodu správy.  
    - **Protokol**: Zadejte **_tcp**.  
    - **Priorita**: Configuration Manager nepoužívá toto pole.  
    - **Váha**: Configuration Manager nepoužívá toto pole.  
    - **Port**: Zadejte číslo portu, který využívá bod správy, třeba **80** pro HTTP a **443** pro HTTPS.  

      > [!NOTE]  
      > Port záznamu SRV musí odpovídat komunikačnímu portu, který používá bod správy. Ve výchozím nastavení je to **80** pro komunikaci HTTP a **443** pro komunikaci pomocí protokolu HTTPS.  

    - **Hostitel nabízející tuto službu**: zadejte plně kvalifikovaný název domény intranetu zadaný pro systém lokality, který je nakonfigurovaný s rolí lokality bodu správy.  

Tento postup opakujte pro všechny body správy na intranetu, které chcete publikovat ve službě DNS.  

##  <a name="wins"></a><a name="bkmk_wins"></a> UDÁVANÁ  
Pokud ostatní mechanismy umístění služby selžou, klienti mohou najít prvotní bod správy ve službě WINS.  

Ve výchozím nastavení primární lokalita publikuje do služby WINS první bod správy v lokalitě, který je konfigurován pro protokol HTTP a první bod správy, který je nakonfigurován pro protokol HTTPS.  

Pokud nechcete, aby klienti ve službě WINS vyhledávali body správy s protokolem HTTP, nastavte klienty pomocí vlastnosti CCMSetup.exe Client.msi **SMSDIRECTORYLOOKUP=NOWINS**.