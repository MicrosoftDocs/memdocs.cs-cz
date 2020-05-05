---
title: Plánování zabezpečení
titleSuffix: Configuration Manager
description: Získejte osvědčené postupy a další informace o zabezpečení v Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 53a30f376bd288e8d50d88ea8f33af37f3cd599e
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110147"
---
# <a name="plan-for-security-in-configuration-manager"></a>Plánování zabezpečení v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek popisuje koncepty, které byste měli vzít v úvahu při plánování zabezpečení pomocí implementace Configuration Manager. Obsahuje následující oddíly:  

- [Plánování certifikátů (podepsaných svým držitelem a PKI)](#BKMK_PlanningForCertificates)  
  - [Kryptografie: certifikáty nové generace (CNG)](#bkmk_plan-cng)  
  - [Vylepšený protokol HTTP](#bkmk_plan-ehttp)  
  - [Certifikáty pro CMG a CDP](#bkmk_plan-cmgcdp)  
  - [Podpisový certifikát serveru lokality (podepsaný svým držitelem)](#bkmk_plansitesign)  
  - [Odvolání certifikátu PKI](#BKMK_PlanningForCRLs)  
  - [Důvěryhodné kořenové certifikáty PKI a Vystavitelé certifikátů](#BKMK_PlanningForRootCAs)  
  - [Výběr klientského certifikátu PKI](#BKMK_PlanningForClientCertificateSelection)  
  - [Strategie přechodu pro certifikáty PKI a internetovou správu klientů](#BKMK_PlanningForPKITransition)  

- [Plánování důvěryhodného kořenového klíče](#BKMK_PlanningForRTK)  

- [Plánování podepisování a šifrování](#BKMK_PlanningForSigningEncryption)  

- [Plánování správy na základě rolí](#BKMK_PlanningForRBA)  

- [Plánování Azure Active Directory](#bkmk_planazuread)  

- [Plánování ověřování poskytovatele služby SMS](#bkmk_auth)



##  <a name="plan-for-certificates-self-signed-and-pki"></a><a name="BKMK_PlanningForCertificates"></a>Plánování certifikátů (podepsaných svým držitelem a PKI)  

Configuration Manager používá kombinaci certifikátů podepsaných svým držitelem a certifikátů infrastruktury veřejných klíčů (PKI).  

Pokud je to možné, používejte certifikáty PKI. Další informace najdete v tématu [požadavky na certifikát PKI](../network/pki-certificate-requirements.md). Pokud Configuration Manager vyžádá certifikáty PKI během zápisu pro mobilní zařízení, musíte použít Active Directory Domain Services a certifikační autoritu organizace. Pro všechny ostatní certifikáty PKI je nasaďte a spravujte nezávisle na Configuration Manager. 

Certifikáty PKI jsou požadovány, když se klientské počítače připojují k internetovým systémům lokality. Některé scénáře s bránou pro správu cloudu a distribučním bodem cloudu také vyžadují certifikáty PKI. Další informace najdete v tématu [Správa klientů na internetu](../../clients/manage/manage-clients-internet.md).

Pokud používáte infrastrukturu veřejných klíčů (PKI), můžete také pomocí protokolu IPsec zvýšit zabezpečení komunikace mezi servery mezi systémy lokality v lokalitě, mezi lokalitami a dalšími přenosy dat mezi počítači. Implementace protokolu IPsec je nezávislá na Configuration Manager.  

Pokud nejsou certifikáty PKI k dispozici, Configuration Manager automaticky vygeneruje certifikáty podepsané svým držitelem. Některé certifikáty v Configuration Manager jsou vždy podepsané svým držitelem. Ve většině případů Configuration Manager automaticky spravuje certifikáty podepsané svým držitelem a vy nemusíte provádět žádné další akce. Jedním z příkladů je podpisový certifikát serveru lokality. Tento certifikát je vždy podepsaný svým držitelem. Ujistěte se, že zásady, které klienti stahují z bodu správy, byly odeslány ze serveru lokality a nebylo v něm manipulováno.  


### <a name="cryptography-next-generation-cng-certificates"></a><a name="bkmk_plan-cng"></a>Kryptografie: certifikáty nové generace (CNG)  

Configuration Manager podporuje certifikáty kryptografie: Next Generation (CNG). Klienti služby Configuration Manager můžou používat certifikát ověřování klientů PKI s privátním klíčem v CNG (klíč úložiště klíčů). S podporou KSP Configuration Manager klienti podporují privátní klíč založený na hardwaru, jako je například KSP čipu TPM pro certifikáty ověřování klientů PKI. Další informace najdete v tématu [Přehled certifikátů CNG](../network/cng-certificates-overview.md).


### <a name="enhanced-http"></a><a name="bkmk_plan-ehttp"></a>Vylepšený protokol HTTP  

Pro všechny Configuration Manager komunikačních cest se doporučuje používat komunikaci přes protokol HTTPS, ale u některých zákazníků je to náročné, protože se jedná o režii při správě certifikátů PKI. Zavedení integrace služby Azure Active Directory (Azure AD) omezuje některé, ale ne všechny požadavky na certifikáty. Počínaje verzí 1806 můžete povolit, aby lokalita používala **Rozšířený protokol HTTP**. Tato konfigurace podporuje protokol HTTPS v systémech lokality pomocí kombinace certifikátů podepsaných svým držitelem a Azure AD. Nevyžaduje infrastrukturu veřejných klíčů. Další informace najdete v tématu [Rozšířená http](../hierarchy/enhanced-http.md).  


### <a name="certificates-for-cmg-and-cdp"></a><a name="bkmk_plan-cmgcdp"></a>Certifikáty pro CMG a CDP

Správa klientů na internetu prostřednictvím brány pro správu cloudu (CMG) a distribučního bodu cloudu (CDP) vyžaduje použití certifikátů. Počet a typ certifikátů se liší v závislosti na konkrétních scénářích. Další informace najdete v těchto článcích:
- [Certifikáty pro bránu pro správu cloudu](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md)  
- [Certifikáty pro distribuční bod cloudu](../hierarchy/use-a-cloud-based-distribution-point.md#bkmk_certs)  


### <a name="plan-for-the-site-server-signing-certificate-self-signed"></a><a name="bkmk_plansitesign"></a>Plánování podpisového certifikátu serveru lokality (podepsaného svým držitelem)  

Klienti mohou bezpečně získat kopii podpisového certifikátu serveru lokality z Active Directory Domain Services a z nabízené instalace klienta. Pokud klienti nemůžou kopii tohoto certifikátu získat pomocí některého z těchto mechanismů, nainstalujte ho při instalaci klienta. Tento postup je zvlášť důležitý, pokud je první komunikace klienta s lokalitou v internetovém bodě správy. Vzhledem k tomu, že tento server je připojený k nedůvěryhodné síti, je zranitelnější vůči útokům. Pokud tento další krok neprovedete, klienti automaticky stáhnou kopii podpisového certifikátu serveru lokality z bodu správy.  

Klienti nemohou bezpečně získat kopii certifikátu serveru lokality v následujících scénářích:  

- Klienta nenainstalujete pomocí klientské nabízené instalace a:  

  - Nerozšířili jste schéma služby Active Directory pro Configuration Manager.  

  - Nepublikovali jste lokalitu klienta na Active Directory Domain Services.  

  - Klient pochází z nedůvěryhodné doménové struktury nebo pracovní skupiny.  

- Používáte internetovou správu klientů a nainstalujete klienta nástroje, pokud je připojen k Internetu.  

#### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>Pro instalaci klientů s kopií podpisového certifikátu serveru lokality  

1.  Vyhledejte podpisový certifikát serveru lokality na serveru primární lokality. Certifikát je uložen v úložišti certifikátů **SMS** systému Windows. Má název subjektu **Server lokality** a popisný název, **podpisový certifikát serveru lokality**.  

2.  Exportujte certifikát bez privátního klíče, bezpečně soubor uložte a přistoupit k němu jenom z zabezpečeného kanálu.  

3.  Nainstalujte klienta pomocí následující vlastnosti Client. msi:`SMSSIGNCERT=<full path and file name>`  


###  <a name="plan-for-pki-certificate-revocation"></a><a name="BKMK_PlanningForCRLs"></a>Plánování odvolání certifikátu PKI  

Pokud používáte certifikáty PKI s Configuration Manager, naplánujte použití seznamu odvolaných certifikátů (CRL). Zařízení používají seznam CRL k ověření certifikátu na připojujícím se počítači. Seznam odvolaných certifikátů je soubor, který certifikační autorita (CA) vytváří a podepisuje. Obsahuje seznam certifikátů, které certifikační autorita vystavila, ale odvolala. Když správce certifikátů odvolá certifikáty, jeho kryptografický otisk se přidá do seznamu CRL. Například pokud je vydaný certifikát známý nebo je podezřelý z ohrožení.

> [!IMPORTANT]  
> Vzhledem k tomu, že umístění seznamu CRL se přidá k certifikátu, když ho CA vystavuje, nezapomeňte naplánovat seznam CRL, než nasadíte jakékoli certifikáty PKI, které Configuration Manager používá.  

Služba IIS vždycky kontroluje seznam CRL pro klientské certifikáty a tuto konfiguraci nemůžete změnit v Configuration Manager. Ve výchozím nastavení klienti Configuration Manager vždycky kontrolují seznam CRL pro systémy lokalit. Toto nastavení zakažte zadáním vlastnosti lokality a zadáním vlastnosti CCMSetup.  

Počítače, které používají kontrolu odvolání certifikátů, ale nemůžou najít seznam CRL, jako by byly odvolány všechny certifikáty v certifikačním řetězci. Důvodem tohoto chování je skutečnost, že nemůžou ověřit, jestli se certifikáty nacházejí v seznamu odvolaných certifikátů. V tomto scénáři selžou všechna připojení, která vyžadují certifikáty a zahrnují kontrolu CRL. Při ověřování, že je váš seznam odvolaných certifikátů přístupný, můžete přejít na jeho umístění HTTP, takže je důležité si uvědomit, že Configuration Manager klient běží jako místní systém. Proto může být testování dostupnosti seznamu CRL s webovým prohlížečem spuštěným v uživatelském kontextu úspěšné, ale při pokusu o vytvoření připojení HTTP ke stejné adrese URL seznamu CRL z důvodu interního řešení webového filtrování může dojít k zablokování účtu počítače. V této situaci může být nutné v případě, že je povolená adresa URL seznamu CRL u všech řešení pro filtrování webu.

Kontrola seznamu CRL při každém použití certifikátu nabízí lepší zabezpečení před použitím odvolaného certifikátu. I když se v klientovi zavádí zpoždění připojení a další zpracování. Vaše organizace může vyžadovat tuto dodatečnou kontrolu zabezpečení pro klienty na internetu nebo v nedůvěryhodné síti.  

Než se rozhodnete, jestli Configuration Manager klienti musí kontrolovat seznam CRL, obraťte se na správce infrastruktury veřejných klíčů. Pak zvažte zachování této možnosti povolené v Configuration Manager, pokud jsou splněné obě následující podmínky:  

- Vaše infrastruktura PKI podporuje seznam CRL a je publikována tam, kde ji všichni Configuration Manager klienti můžou najít. Tito klienti můžou zahrnovat zařízení na internetu a ty v nedůvěryhodných doménových strukturách.  

- Požadavek na kontrolu seznamu odvolaných certifikátů pro každé připojení k systému lokality, který je nakonfigurován pro použití certifikátu PKI, je větší než následující požadavky:  
  - Rychlejší připojení  
  - Efektivní zpracování na klientovi  
  - Riziko, že se klienti nedaří připojit k serverům, pokud se seznam CRL nedá najít  


###  <a name="plan-for-the-pki-trusted-root-certificates-and-the-certificate-issuers-list"></a><a name="BKMK_PlanningForRootCAs"></a>Plánování důvěryhodných kořenových certifikátů PKI a seznamu vystavitelů certifikátů  

Pokud vaše systémy lokality IIS používají klientské certifikáty PKI pro ověřování klientů prostřednictvím protokolu HTTP nebo pro ověřování klientů a šifrování prostřednictvím protokolu HTTPS, bude pravděpodobně nutné importovat certifikáty kořenové certifikační autority jako vlastnost lokality. Tady jsou dva scénáře:  

- Operační systémy nasazujete pomocí Configuration Manager a body správy přijímají pouze připojení klientů přes protokol HTTPS.  

- Použijete klientské certifikáty PKI, které neřetězují k kořenovému certifikátu, ke kterému mají body správy vztah důvěryhodnosti.  

  > [!NOTE]  
  > Když vydáte klientské certifikáty PKI ze stejné hierarchie certifikační autority, která vydává certifikáty serveru, které používáte pro body správy, nemusíte tento certifikát od kořenové certifikační autority zadávat. Pokud však používáte více hierarchií certifikačních autorit a nejste si jisti, zda vzájemně důvěřují, importujte kořenovou certifikační autoritu pro hierarchii certifikačních autorit klientů.  

Pokud je nutné importovat certifikáty kořenové certifikační autority pro Configuration Manager, exportujte je z vydávající certifikační autority nebo z klientského počítače. Pokud exportujete certifikát z vydávající certifikační autority, která je také kořenovou certifikační autoritou, ujistěte se, že neexportujete privátní klíč. Uložte exportovaný soubor certifikátu do zabezpečeného umístění, aby nedocházelo k manipulaci. Při nastavování lokality potřebujete přístup k souboru. Pokud přistupujete k souboru přes síť, ujistěte se, že komunikace je chráněná před manipulací pomocí protokolu IPsec.  

Pokud se obnoví jakýkoli certifikát kořenové certifikační autority, který importujete, musíte importovat obnovený certifikát.  

Tyto importované certifikáty kořenové certifikační autority a certifikát kořenové certifikační autority každého bodu správy vytvoří seznam vystavitelů certifikátů, který Configuration Manager počítače používat následujícími způsoby:  

- Když se klienti připojují k bodům správy, bod správy ověří, že je klientský certifikát zřetězený do důvěryhodného kořenového certifikátu v seznamu vystavitelů certifikátů lokality. Pokud tomu tak není, certifikát je odmítnut a připojení PKI se nezdařilo.  

- Když klienti vyberou certifikát PKI a mají seznam vystavitelů certifikátů, vyberou certifikát, který je zřetězený s důvěryhodným kořenovým certifikátem v seznamu vystavitelů certifikátů. Pokud se neshodují, klient nevybere certifikát PKI. Další informace najdete v tématu [plánování výběru klientského certifikátu PKI](#BKMK_PlanningForClientCertificateSelection).  


###  <a name="plan-for-pki-client-certificate-selection"></a><a name="BKMK_PlanningForClientCertificateSelection"></a>Plánování výběru klientského certifikátu PKI  

Pokud vaše systémy lokality IIS používají klientské certifikáty PKI pro ověřování klientů prostřednictvím protokolu HTTP nebo pro ověřování klientů a šifrování prostřednictvím protokolu HTTPS, Naplánujte způsob, jakým klienti Windows vyberou certifikát, který se má použít pro Configuration Manager.  

> [!NOTE]  
> Některá zařízení nepodporují metodu výběru certifikátu. Místo toho automaticky vyberou první certifikát, který splňuje požadavky na certifikát. Například klienti na počítačích Mac a mobilních zařízeních nepodporují metodu výběru certifikátu.  

V mnoha případech je výchozí konfigurace a chování dostačující. Klient Configuration Manager v počítačích se systémem Windows filtruje více certifikátů pomocí těchto kritérií v tomto pořadí:  

1.  Seznam vydavatelů certifikátů: certifikát řetězí ke kořenové certifikační autoritě, která je pro bod správy důvěryhodná.  

2.  Certifikát se nachází ve výchozím úložišti certifikátů nazvaném **Osobní**.  

3.  Certifikát je platný, není odvolaný ani s prošlou platností. Při kontrole platnosti se taky ověří, jestli je privátní klíč přístupný.  

4.  Certifikát má schopnost ověřování klienta, nebo je vydaný pro název počítače.  

5.  Certifikát má nejdelší dobu platnosti.  

Nakonfigurujte klienty tak, aby používali seznam vystavitelů certifikátů, a to pomocí následujících mechanismů:  

- Publikujte ji pomocí Configuration Manager informací o lokalitě Active Directory Domain Services.  

- Nainstalujte klienty pomocí klientské nabízené instalace.  

- Klienti ho stáhnou z bodu správy poté, co jsou úspěšně přiřazeni ke své lokalitě.  

- Zadejte v průběhu instalace klienta jako vlastnost CCMSetup Client. msi CCMCERTISSUERS.  

Klienti, kteří nemají seznam vydavatelů certifikátů při první instalaci a ještě nejsou přiřazeni k lokalitě, tuto kontrolu přeskočí. Když klienti mají seznam vystavitelů certifikátů a nemají certifikát PKI, který je v seznamu vystavitelů certifikátů zřetězený s důvěryhodným kořenovým certifikátem, výběr certifikátu se nezdařil. Klienti nepokračují s dalšími kritérii výběru certifikátu.  

Ve většině případů klient Configuration Manager správně identifikuje jedinečný a vhodný certifikát PKI. Pokud se však toto chování nejedná o tento případ, místo abyste vybrali certifikát na základě schopnosti ověřování klientů, můžete nastavit dvě alternativní metody výběru:  

- Částečná shoda řetězců v názvu předmětu certifikátu klienta. Tato metoda rozlišuje nerozlišovat velká a malá písmena. To je vhodné, pokud používáte plně kvalifikovaný název domény (FQDN) počítače v poli subjekt a chcete, aby výběr certifikátu byl založen na příponě domény, například **contoso.com**. Tuto metodu výběru však můžete použít k identifikaci libovolného řetězce sekvenčních znaků v názvu subjektu certifikátu, který rozlišuje certifikát od ostatních v úložišti certifikátů klienta.  

  > [!NOTE]
  > Nemůžete použít částečnou shodu řetězců s alternativním názvem subjektu (SAN) jako s nastavením lokality. I když můžete určit částečnou shodu řetězců pro síť SAN pomocí služby CCMSetup, bude tato vlastnost přepsána vlastnostmi lokality v následujících scénářích:  
  > 
  > - Klienti načtou informace o lokalitě publikované do Active Directory Domain Services.  
  >   - Klienti jsou instalováni pomocí nabízené instalace klienta.  
  > 
  >   Částečnou shodu řetězců v síti SAN použijte, pouze když instalujete klienty ručně a pokud nezískávají informace o lokalitě z Active Directory Domain Services. Tyto podmínky se vztahují například jenom na internetové klienty.  

- Shoda s hodnotami atributu názvu předmětu certifikátu klienta nebo hodnotami atributu alternativní název subjektu (SAN). Tato metoda je shodná s rozlišením velkých a malých písmen. Je vhodný, pokud používáte rozlišující název X500 nebo ekvivalentní identifikátory objektu (OID) v souladu s dokumentem RFC 3280 a chcete, aby výběr certifikátu byl založen na hodnotách atributů. Je možné určit pouze atributy a jejich hodnoty, které požadujete k jedinečné identifikaci nebo ověření certifikátu a odlišení certifikátu od jiných v úložišti certifikátů.  

Následující tabulka uvádí hodnoty atributů, které Configuration Manager podporuje pro kritéria výběru klientského certifikátu.  

|Atribut OID|Rozlišující název atributu|Definice atributu|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Součást domény|  
|1.2.840.113549.1.9.1|E nebo e-mail|E-mailová adresa|  
|2.5.4.3|CN|Běžný název|  
|2.5.4.4|SN|Název předmětu|  
|2.5.4.5|SERIALNUMBER|Sériové číslo|  
|2.5.4.6|C|Kód země|  
|2.5.4.7|L|Lokalita|  
|2.5.4.8|S nebo ST|Název státu nebo oblasti|  
|2.5.4.9|STREET|Ulice a číslo|  
|2.5.4.10|O|Název organizace|  
|2.5.4.11|OU|Organizační jednotka|  
|2.5.4.12|T nebo Title|Nadpis|  
|2.5.4.42|G nebo GN nebo GivenName|Křestní jméno|  
|2.5.4.43|I nebo Initials|Iniciály|  
|2.5.29.17|(žádná hodnota)|Alternativní název subjektu|  

Pokud je po použití kritérií výběru použit více než jeden vhodný certifikát, můžete přepsat výchozí konfiguraci a vybrat certifikát s nejdelší dobou platnosti a místo toho určit, že není vybrán žádný certifikát. V tomto scénáři klient nebude moci komunikovat se systémy lokality IIS pomocí certifikátu PKI. Klient pošle do přiřazeného záložního stavového bodu chybovou zprávu, která vás upozorní na selhání výběru certifikátu, abyste mohli změnit nebo Upřesnit kritéria výběru certifikátu. Chování klienta poté bude záviset na tom, že připojení, jež selhalo, bylo založeno na protokolu HTTPS nebo HTTP:  

- Pokud selhalo připojení prostřednictvím protokolu HTTPS: klient se pokusí připojit přes protokol HTTP a použije certifikát klienta podepsaný svým držitelem.  

- Pokud selhalo připojení prostřednictvím protokolu HTTP: klient se pokusí o připojení znovu přes protokol HTTP pomocí certifikátu klienta podepsaného svým držitelem.  

Chcete-li identifikovat jedinečný klientský certifikát PKI, můžete také zadat vlastní úložiště jiné než výchozí **osobní** v úložišti **počítače** . Toto úložiště je však třeba vytvořit nezávisle na Configuration Manager. Musíte být schopni nasadit certifikáty do tohoto vlastního úložiště a obnovit je před vypršením doby platnosti.  

Další informace najdete v tématu [Konfigurace nastavení pro klientské certifikáty PKI](configure-security.md#BKMK_ConfigureClientPKI).  


###  <a name="plan-a-transition-strategy-for-pki-certificates-and-internet-based-client-management"></a><a name="BKMK_PlanningForPKITransition"></a>Plánování strategie přechodu pro certifikáty PKI a internetovou správu klientů  

Flexibilní možnosti konfigurace v Configuration Manager umožňují postupně převádět klienty a lokalitu, aby používaly certifikáty PKI k zabezpečení koncových bodů klienta. Certifikáty PKI poskytují lepší zabezpečení a umožňují správu internetových klientů.  

Z důvodu počtu možností konfigurace a voleb v Configuration Manager neexistuje žádný jediný způsob, jak převést lokalitu, aby všichni klienti používali připojení HTTPS. Je však možné provést následující kroky:  

1. Nainstalujte lokalitu Configuration Manager a nakonfigurujte ji tak, aby systémy lokality přijímaly připojení klientů přes protokol HTTPS a HTTP.  

2. Nakonfigurujte kartu **komunikace s klientským počítačem** ve vlastnostech lokality tak, aby **nastavení systému lokality** byla **http nebo https**, a vyberte **použít klientský certifikát PKI (schopnost ověřování klientů), pokud je k dispozici**.  Další informace najdete v tématu [Konfigurace nastavení pro klientské certifikáty PKI](configure-security.md#BKMK_ConfigureClientPKI).  

    > [!Note]
    > Počínaje verzí 1906 se tato karta nazývá **zabezpečení komunikace**.<!-- SCCMDocs#1645 -->  

3. Proveďte zavedení PKI pro klientské certifikáty. Ukázkové nasazení najdete v tématu [Nasazení certifikátu klienta pro počítače se systémem Windows](../network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).  

4. Nainstalujte klienty pomocí metody nabízené instalace klienta. Další informace najdete v tématu [instalace klientů Configuration Manager pomocí klientské nabízené instalace](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

5. Monitorujte nasazení a stav klienta pomocí sestav a informací v konzole Configuration Manager.  

6. Sledujte, kolik klientů používá certifikát klienta PKIm, zobrazením sloupce **Certifikát klienta** v pracovním prostoru **Prostředky a kompatibilita** v uzlu **Zařízení** .  

    Do počítačů lze také nasadit nástroj pro vyhodnocení připravenosti HTTPS Configuration Manager (**cmHttpsReadiness. exe**). Pak můžete pomocí sestav zobrazit, kolik počítačů může používat klientský certifikát PKI s Configuration Manager.  

   > [!NOTE]
   >  Při instalaci klienta Configuration Manager nainstaluje nástroj **CMHttpsReadiness. exe** do `%windir%\CCM` složky. Při spuštění tohoto nástroje jsou k dispozici následující možnosti příkazového řádku:  
   > 
   > - `/Store:<name>`: Tato možnost je stejná jako vlastnost Client. msi **CCMCERTSTORE** .  
   > - `/Issuers:<list>`: Tato možnost je stejná jako vlastnost Client. msi **CCMCERTISSUERS** .    
   > - `/Criteria:<criteria>`: Tato možnost je stejná jako vlastnost Client. msi **CCMCERTSEL** .    
   > - `/SelectFirstCert`: Tato možnost je stejná jako vlastnost Client. msi **CCMFIRSTCERT** .    
   > 
   >   Další informace najdete v tématu [o vlastnostech instalace klienta](../../clients/deploy/about-client-installation-properties.md).  

7. Pokud jste si jistí, že všichni klienti úspěšně používají svůj klientský certifikát PKI k ověřování prostřednictvím protokolu HTTP, postupujte podle těchto kroků:  

   1.  Nasaďte certifikát PKI webového serveru na členský server, na kterém běží další bod správy pro lokalitu, a nakonfigurujte tento certifikát ve službě IIS. Další informace najdete v tématu [Nasazení certifikátu webového serveru pro systémy lokality, které spouštějí službu IIS](../network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  

   2.  Nainstalujte roli bodu správy na tomto serveru a nakonfigurujte možnost **Připojení klientů** ve vlastnostech bodu správy pro protokol **HTTPS**.  

8. Monitorujte a ověřte, zda klienti, kteří mají certifikát PKI, používají nový bod správy pomocí protokolu HTTPS. K ověření můžete použít čítače protokolování nebo výkonu služby IIS.  

9. Rekonfigurujte další role systému lokality pro použití připojení klienta prostřednictvím protokolu HTTPS. Chcete-li spravovat klienty na internetu, ujistěte se, že systémy lokality mají internetový plně kvalifikovaný název domény. Nakonfigurujte jednotlivé body správy a distribuční body pro přijetí připojení klienta z Internetu.  

    > [!IMPORTANT]  
    > Než nastavíte role systému lokality pro příjem připojení z Internetu, zkontrolujte informace o plánování a požadavky pro internetovou správu klientů. Další informace najdete v tématu [komunikace mezi koncovými body](../hierarchy/communications-between-endpoints.md).  

10. Rozšíříte zavedení certifikátu PKI pro klienty a systémy lokality, které spouští službu IIS. V případě potřeby nastavte role systému lokality pro připojení klientů přes protokol HTTPS a připojení k Internetu.  

11. Nejvyšší zabezpečení: Pokud jste si jistí, že všichni klienti používají klientský certifikát PKI k ověřování a šifrování, změňte vlastnosti lokality tak, aby používaly pouze HTTPS.  

    Tento plán nejdřív zavádí certifikáty PKI pro ověřování pouze přes protokol HTTP a pak pro ověřování a šifrování prostřednictvím protokolu HTTPS. Když použijete tento plán k následnému zavedení těchto certifikátů, snížíte riziko, že se klienti stanou nespravovanými. Výhodou je také nejvyšší zabezpečení, které Configuration Manager podporuje.  

##  <a name="plan-for-the-trusted-root-key"></a><a name="BKMK_PlanningForRTK"></a>Plánování důvěryhodného kořenového klíče  

Configuration Manager důvěryhodný kořenový klíč poskytuje mechanismus pro klienty Configuration Manager, aby ověřil systémy lokality patřící do jejich hierarchie. Každý server lokality generuje klíč pro výměnu lokalit, který slouží ke komunikaci s dalšími lokalitami. Klíč pro výměnu lokality z lokality nejvyšší úrovně v hierarchii je označován jako důvěryhodný kořenový klíč.  

Funkce důvěryhodného kořenového klíče v Configuration Manager se podobá kořenovému certifikátu v infrastruktuře veřejných klíčů. Všechny položky podepsané soukromým klíčem důvěryhodného kořenového klíče jsou důvěryhodné i mimo hierarchii. Klienti ukládají kopii důvěryhodného kořenového klíče lokality do oboru názvů služby **Root\ccm\locationservices** WMI. 

Lokalita například vystaví certifikát pro bod správy, který se podepisuje soukromým klíčem důvěryhodného kořenového klíče. Lokalita sdílí s klienty veřejný klíč jeho důvěryhodného kořenového klíče. Klienti pak mohou rozlišovat mezi body správy, které jsou v jejich hierarchii, a body správy, které nejsou v jejich hierarchii.   

Klienti automaticky načtou veřejnou kopii důvěryhodného kořenového klíče pomocí dvou mechanismů:  

- Rozšíříte schéma služby Active Directory pro Configuration Manager a publikujete web do Active Directory Domain Services. Klienti pak tyto informace o lokalitě načtou ze serveru globálního katalogu. Další informace najdete v tématu [Příprava služby Active Directory pro publikování lokality](../network/extend-the-active-directory-schema.md).  

- Když instalujete klienty pomocí metody nabízené instalace klienta. Další informace najdete v tématu [klientská nabízená instalace](../../clients/deploy/plan/client-installation-methods.md#client-push-installation).  

Pokud klienti nemohou získat důvěryhodný kořenový klíč pomocí jednoho z těchto mechanismů, důvěřují důvěryhodnému kořenovému klíči, který je poskytován prvním bodem správy, se kterým komunikuje. V tomto scénáři může být klient omylem přesměrován na bod správy útočníka, kde by získal zásady z podvodného bodu správy. Tato akce vyžaduje sofistikovaného útočníka. Tento útok je omezený na krátkou dobu před tím, než klient získá důvěryhodný kořenový klíč z platného bodu správy. Chcete-li snížit toto riziko, že by útočník nasměroval klienty na podvodný bod správy, zajistěte klientům důvěryhodný kořenový klíč předem.  

Pomocí následujících postupů můžete předem zřídit a ověřit důvěryhodný kořenový klíč pro klienta Configuration Manager:  

- [Předem zřídit klienta s důvěryhodným kořenovým klíčem pomocí souboru](#bkmk_trk-provision-file)  

- [Předem zřídit klienta s důvěryhodným kořenovým klíčem bez použití souboru](#bkmk_trk-provision-nofile)  

- [Ověření důvěryhodného kořenového klíče na klientovi](#bkmk_trk-verify)  

- [Odeberte nebo nahraďte důvěryhodný kořenový klíč.](#bkmk_trk-reset)  

  > [!NOTE]  
  > Pokud klienti mohou získat důvěryhodný kořenový klíč z Active Directory Domain Services nebo klientskou nabízenou instalaci, nemusíte ho předem zřizovat. 
  > 
  > Pokud klienti používají komunikaci pomocí protokolu HTTPS s body správy, nemusíte mít předem zajištěný důvěryhodný kořenový klíč. Vytvářejí důvěryhodnost certifikáty PKI.  


### <a name="pre-provision-a-client-with-the-trusted-root-key-by-using-a-file"></a><a name="bkmk_trk-provision-file"></a>Předem zřídit klienta s důvěryhodným kořenovým klíčem pomocí souboru  

1.  Na serveru lokality otevřete v textovém editoru následující soubor:`<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  Vyhledejte položku **SMSPublicRootKey =**. Zkopírujte klíč z daného řádku a zavřete soubor bez jakýchkoli změn.  

3.  Vytvořte nový textový soubor a vložte informace o klíči, které jste zkopírovali ze souboru mobileclient. tcf.  

4.  Uložte soubor do umístění, kam k němu mají přístup všechny počítače, ale v případě, že je soubor bezpečný proti falšování.  

5.  Nainstalujte klienta pomocí libovolné metody instalace, která podporuje vlastnosti Client. msi. Zadejte následující vlastnost:`SMSROOTKEYPATH=<full path and file name>`  

    > [!IMPORTANT]  
    > Pokud během instalace klienta určíte důvěryhodný kořenový klíč, zadejte také kód lokality. Použijte následující vlastnost Client. msi:`SMSSITECODE=<site code>`   


### <a name="pre-provision-a-client-with-the-trusted-root-key-without-using-a-file"></a><a name="bkmk_trk-provision-nofile"></a>Předem zřídit klienta s důvěryhodným kořenovým klíčem bez použití souboru  

1.  Na serveru lokality otevřete v textovém editoru následující soubor:`<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  Vyhledejte položku **SMSPublicRootKey =**. Zkopírujte klíč z daného řádku a zavřete soubor bez jakýchkoli změn.  

3.  Nainstalujte klienta pomocí libovolné metody instalace, která podporuje vlastnosti Client. msi. Zadejte následující vlastnost Client. msi: `SMSPublicRootKey=<key>` kde `<key>` je řetězec, který jste zkopírovali z MobileClient. tcf.  

    > [!IMPORTANT]  
    >  Pokud během instalace klienta určíte důvěryhodný kořenový klíč, zadejte také kód lokality. Použijte následující vlastnost Client. msi:`SMSSITECODE=<site code>`   


### <a name="verify-the-trusted-root-key-on-a-client"></a><a name="bkmk_trk-verify"></a>Ověření důvěryhodného kořenového klíče na klientovi  

1. Otevřete konzolu Windows PowerShellu jako správce.  

2. Spusťte následující příkaz:  

    ``` PowerShell
    (Get-WmiObject -Namespace root\ccm\locationservices -Class TrustedRootKey).TrustedRootKey
    ```

Vrácený řetězec je důvěryhodný kořenový klíč. Ověřte, že se shoduje s hodnotou **SMSPublicRootKey** v souboru mobileclient. TCF na serveru lokality.  


### <a name="remove-or-replace-the-trusted-root-key"></a><a name="bkmk_trk-reset"></a>Odeberte nebo nahraďte důvěryhodný kořenový klíč.  

Odeberte důvěryhodný kořenový klíč z klienta pomocí vlastnosti Client. msi, **RESETKEYINFORMATION = true**. 

Pokud chcete důvěryhodný kořenový klíč nahradit, přeinstalujte klienta společně s novým důvěryhodným kořenovým klíčem. Použijte například nabízenou klientské nabízení nebo určete vlastnost Client. msi **SMSPublicRootKey**.  

Další informace o těchto vlastnostech instalace najdete v tématu [informace o parametrech instalace a vlastnostech klienta](../../clients/deploy/about-client-installation-properties.md).



##  <a name="plan-for-signing-and-encryption"></a><a name="BKMK_PlanningForSigningEncryption"></a>Plánování podepisování a šifrování  
 
Při použití certifikátů PKI pro veškerou komunikaci s klienty není nutné plánovat podepisování a šifrování, aby bylo možné zabezpečit komunikaci s daty klienta. Pokud nastavíte systémy lokality, které spouštějí službu IIS, aby umožňovaly připojení klienta prostřednictvím protokolu HTTP, rozhodněte se, jak zajistit zabezpečení komunikace klienta pro danou lokalitu.  

Aby bylo možné chránit data, která klienti odesílají do bodů správy, můžete požadovat, aby klienti podepsali data. Pro podepisování můžete také vyžadovat algoritmus SHA-256. Tato konfigurace je bezpečnější, ale nevyžaduje SHA-256, pokud ji všichni klienti nepodporují. Mnohé operační systémy tento algoritmus nativně podporují, ale starší operační systémy můžou vyžadovat aktualizaci nebo opravu hotfix. 

I když podepisování pomáhá chránit data před manipulací, šifrování pomáhá chránit data před odhalením informací. Lze povolit šifrování 3DES pro data inventáře a stavové zprávy, které klienti odesílají do bodů správy. Pro podporu této možnosti není nutné instalovat žádné aktualizace do klientů. Klienti a body správy vyžadují pro šifrování a dešifrování dodatečné využití procesoru.  

Další informace o tom, jak nakonfigurovat nastavení pro podepisování a šifrování, najdete v tématu [Konfigurace podepisování a šifrování](configure-security.md#BKMK_ConfigureSigningEncryption).  



##  <a name="plan-for-role-based-administration"></a><a name="BKMK_PlanningForRBA"></a>Plánování správy na základě rolí  

Další informace najdete v tématu [základy správy na základě rolí](../../understand/fundamentals-of-role-based-administration.md).  



## <a name="plan-for-azure-active-directory"></a><a name="bkmk_planazuread"></a>Plánování Azure Active Directory

Configuration Manager se integruje s Azure Active Directory (Azure AD), aby mohl web a klienti používat moderní ověřování. Připojování webu pomocí Azure AD podporuje následující scénáře Configuration Manager:

**Klient**  

- [Správa klientů na internetu přes bránu pro správu cloudu](../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios)  

- [Správa cloudových zařízení připojených k doméně](../../clients/deploy/deploy-clients-cmg-azure.md)  

- [Spoluspráva](../../../comanage/overview.md)  

- [Nasazení aplikací dostupných pro uživatele](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices)  

- [Aplikace pro online Microsoft Store pro firmy](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  

- Snižte požadavky na infrastrukturu. Například [Centrum softwaru s použitím bodu správy](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex) místo katalogu aplikací  

- [Správa aplikací Microsoft 365 pro podniky](../../../sum/deploy-use/manage-office-365-proplus-updates.md)  


**Server**  

- [Desktop Analytics](../../../desktop-analytics/overview.md)  

- [Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)  

- [Centrum komunity](../../get-started/capabilities-in-technical-preview-1807.md#bkmk_hub)  

- [Distribuční bod cloudu](../hierarchy/use-a-cloud-based-distribution-point.md)  

- [Zjišťování uživatelů](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  


Další informace o připojení lokality ke službě Azure AD najdete v tématu [Konfigurace služeb Azure](../../servers/deploy/configure/azure-services-wizard.md).


Další informace o Azure AD najdete v [dokumentaci Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).



## <a name="plan-for-sms-provider-authentication"></a><a name="bkmk_auth"></a>Plánování ověřování poskytovatele služby SMS
<!--1357013--> 

Počínaje verzí 1810 můžete určit minimální úroveň ověřování pro správce pro přístup k Configuration Manager lokalit. Tato funkce vynutila správcům přihlášení k systému Windows s požadovanou úrovní. Platí pro všechny komponenty, které přistupují k poskytovateli serveru SMS. Například konzola Configuration Manager, metody sady SDK a rutiny prostředí Windows PowerShell. 

Tato konfigurace je nastavení v rámci hierarchie. Než toto nastavení změníte, ujistěte se, že se všichni správci Configuration Manager můžou přihlásit k Windows s požadovanou úrovní ověřování. 

K dispozici jsou následující úrovně:

- **Ověřování systému Windows**: vyžadovat ověřování pomocí přihlašovacích údajů domény služby Active Directory.   

- **Ověřování certifikátu**: vyžaduje ověření pomocí platného certifikátu, který vystavila důvěryhodná certifikační autorita PKI.  

- **Ověřování ve Windows Hello pro firmy**: vyžaduje ověřování pomocí silného dvojúrovňového ověřování, které je vázané na zařízení a používá BIOMETRIKA nebo PIN.  

Další informace najdete v tématu [plánování poskytovatele serveru SMS](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth). 



## <a name="see-also"></a>Viz také
- [Zabezpečení a ochrana osobních údajů pro klienty Configuration Manager](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Konfigurace zabezpečení](configure-security.md)  

- [Komunikace mezi koncovými body](../hierarchy/communications-between-endpoints.md)  

- [Technické informace o kryptografických ovládacích prvcích](cryptographic-controls-technical-reference.md)  

- [Požadavky na certifikát PKI](../network/pki-certificate-requirements.md)  

