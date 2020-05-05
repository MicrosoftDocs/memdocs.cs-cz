---
title: Přiřazení klientů k lokalitě
titleSuffix: Configuration Manager
description: Přiřazení klientů k lokalitě v Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: ba9b623f-6e86-4006-93f2-83d563de0cd0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ab2270435ac13585cb0b7d3271f1faa02cc728d3
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075740"
---
# <a name="how-to-assign-clients-to-a-site-in-configuration-manager"></a>Přiřazení klientů k lokalitě v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Po instalaci klienta Configuration Manager se musí připojit k Configuration Manager primární lokalitě, aby ji bylo možné spravovat. Lokalita, ke které se klient připojuje, se nazývá *přiřazená lokalita*. Klienty nelze přiřadit k lokalitě centrální správy ani k sekundární lokalitě.  

K procesu přiřazení dochází po úspěšné instalaci klienta a určení lokality, která spravuje klientský počítač. Klienta můžete buď přímo přiřadit k lokalitě, nebo můžete použít automatické přiřazení lokality, kde klient automaticky najde příslušný web na základě jeho aktuálního umístění v síti nebo záložní lokality, která byla nakonfigurovaná pro hierarchii.

Když nainstalujete klienta mobilního zařízení během registrace Configuration Manager, zařízení se vždy automaticky přiřadí k lokalitě nástroje. Při instalaci klienta nástroje do počítače můžete zvolit, zda chcete klienta přiřadit k lokalitě nástroje. Pokud je však klient nainstalován, ale ne přiřazen, klient nebude spravován, dokud neproběhne úspěšné přiřazení lokality.  
 

> [!NOTE]  
>  Vždy přiřazujte klienty do lokalit, na kterých běží stejná verze Configuration Manager. Nepřiřazujte klienta Configuration Manager z novější verze do lokality ze starší verze.   V případě potřeby aktualizujte primární lokalitu na stejnou verzi Configuration Manager, kterou používáte pro klienty.  

Po přiřazení klienta k lokalitě zůstane k této lokalitě přiřazen, i když klient změní adresu IP a přemístí se do jiné lokality. Pouze správce může ručně přiřadit klienta k jiné lokalitě nebo odebrat přiřazení klienta.  

> [!WARNING]  
>  Klient zůstane k lokalitě přiřazen pouze tehdy, když klienta přiřadíte v zařízení se systémem Windows Embedded, když jsou povoleny filtry zápisu. Pokud před přiřazením klienta filtry zápisu nezakážete, stav přiřazení lokality klienta se při příštím restartu zařízení vrátí do původního stavu.  
>   
>  Například pokud je klient konfigurován na automatické přiřazení lokality, bude znovu přiřazen při spuštění a může být přiřazen jiné lokalitě. Pokud klient není nakonfigurován pro automatické přiřazení lokality, ale vyžaduje ruční přiřazení lokality, musíte klienta po spuštění ručně znovu přiřadit, aby bylo možné tohoto klienta znovu spravovat pomocí Configuration Manager.  
>   
>  Chcete-li se tomuto chování vyhnout, před přiřazením klienta v zařízeních se systémem Embedded zakažte filtry zápisu a po ověření úspěšného přiřazení lokality je opět povolte.  

Pokud přiřazení klienta selže, software klienta zůstane nainstalován, ale nebude spravován. Klient je považován za nespravovaného, když je nainstalován, ale není přiřazen k lokalitě, nebo když je přiřazen k lokalitě, ale nemůže komunikovat s bodem správy.  

##  <a name="using-manual-site-assignment-for-computers"></a>Používání ručního přiřazení pro počítače  
 Klientské počítače lze k lokalitě přiřadit ručně pomocí následujících dvou metod:  

-   Použijte vlastnost instalace klienta, která určuje kód lokality.  

-   V ovládacích panelech v nabídce **Configuration Manager**zadejte kód lokality.  

> [!NOTE]  
>  Pokud klientský počítač ručně přiřadíte do Configuration Manager kódu lokality, který neexistuje, přiřazení lokality se nepovede.   

##  <a name="using-automatic-site-assignment-for-computers"></a><a name="BKMK_AutomaticAssignment"></a>Použití automatického přiřazení lokality pro počítače  
 Automatické přiřazení lokality může probíhat během nasazení klienta, nebo když kliknete na položku **Vyhledat lokalitu** na kartě **Upřesnit** v nabídce **Vlastnosti nástroje Configuration Manager** v Ovládacích panelech. Klient Configuration Manager porovná své vlastní síťové umístění s hranicemi konfigurovanými v hierarchii Configuration Manager. Pokud umístění sítě klienta spadá do skupiny hranic, která je pro přiřazení lokality povolena, nebo pokud je konfigurována hierarchie pro záložní lokalitu, klient bude automaticky přiřazen dané lokalitě, aniž by bylo třeba zadávat kód lokality.  

 Hranice je možné konfigurovat pomocí jednoho nebo několika následujících parametrů:  

-   Podsíť protokolu IP  

-   Lokalita Active Directory  

-   předpona protokolu IP v6,  

-   Rozsah IP adres  

> [!NOTE]  
>  Pokud má klient Configuration Manager více síťových adaptérů, a proto má několik IP adres, IP adresa použitá k vyhodnocení přiřazení lokality klienta se přiřadí náhodně.  

 Informace o konfiguraci skupin hranic pro přiřazení lokality a způsobu konfigurace záložní lokality pro automatické přiřazení lokality najdete v tématu [definice hranic lokality a skupin hranic pro Configuration Manager](../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).  

 Configuration Manager klienti, kteří používají automatické přiřazení lokality, se pokusí vyhledat skupiny hranic lokality, které jsou publikovány do Active Directory Domain Services. Pokud se to nepovede (například když není schéma služby Active Directory rozšířené pro Configuration Manager nebo jsou klienti počítače pracovní skupiny), mohou klienti získat informace o skupině hranic z bodu správy.  

 Při instalaci je možné určit bod správy pro klientské počítače, který mají používat, nebo mohou klienti vyhledat bod správy pomocí publikování služby DNS nebo WINS.  

 Pokud klient nemůže najít lokalitu, která je přidružena ke skupině hranic obsahující síťové umístění, a hierarchie nemá záložní lokalitu, klient pokus obnovuje každých 10 minut, dokud jej nebude možné přiřadit k lokalitě.  

 Configuration Manager klientské počítače nelze automaticky přiřadit k lokalitě, pokud platí některá z následujících možností a poté je nutné ručně přiřadit:  

-   Jsou přiřazeny k lokalitě.  

-   Jsou připojeni k internetu nebo konfigurováni pouze jako internetoví klienti.  

-   Jejich síťové umístění nespadá do jedné z konfigurovaných skupin hranic v hierarchii nástroje Configuration Manager a pro hierarchii není k dispozici žádná záložní lokalita.  

##  <a name="completing-site-assignment-by-checking-site-compatibility"></a>Dokončení přiřazení lokality kontrolou kompatibility lokality  
 Jakmile klient najde přiřazenou lokalitu, bude zkontrolována verze a operační systém klienta, aby se zajistilo, že Configuration Manager web může spravovat. Configuration Manager například nemůže spravovat klienty Configuration Manager 2007, klienta System Center 2012 Configuration Manager klienty nebo klienty se systémem Windows 2000.  

 Přiřazení lokality se nezdařila, pokud přiřadíte klienta se systémem Windows 2000 k Configuration Manager lokalitě. Když přiřadíte klienta Configuration Manager 2007 nebo klienta nástroje System Center 2012 Configuration Manager do Configuration Manager (aktuální větev), přiřazení lokality se podaří, aby podporovala automatický upgrade klienta. Dokud však klienti starší generace nebudou upgradováni na klienta Configuration Manager (aktuální větev), Configuration Manager nemůže tohoto klienta spravovat pomocí nastavení klienta, aplikací nebo aktualizací softwaru.  

> [!NOTE]  
>  Aby bylo možné podporovat přiřazení lokality Configuration Manager 2007 nebo klienta nástroje System Center 2012 Configuration Manager ke službě Configuration Manager (Current Branch), je nutné nakonfigurovat automatický upgrade klienta pro hierarchii. Další informace najdete v tématu [Postup upgradu klientů pro počítače se systémem Windows](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

Configuration Manager také zkontroluje, zda jste přiřadili klienta Configuration Manager (Current Branch) k lokalitě, která ho podporuje. Následující scénáře mohou nastat během migrace z předchozích verzí nástroje Configuration Manager.  

- Scénář: použili jste automatické přiřazení lokality a hranice se překrývají s definicemi definovanými v předchozí verzi Configuration Manager.  

   V takovém případě se klient automaticky pokusí najít web Configuration Manager (Current Branch).  

   Klient nejprve zkontroluje Active Directory Domain Services a pokud najde publikovanou lokalitu Configuration Manager (aktuální větev), přiřazení lokality je úspěšné. Pokud se tato chyba nezdařila (například lokalita Configuration Manager není publikována nebo je počítač klientem pracovní skupiny), klient zkontroluje informace o lokalitě z přiřazeného bodu správy.  

  > [!NOTE]  
  >  Bod správy lze přiřadit klientovi během instalace klienta pomocí vlastnosti Client. msi **SMSMP =&lt;server_name>**.  

   Pokud selžou obě tyto metody, přiřazení lokality se nezdaří a klienta bude nutné přiřadit ručně.  

- Scénář: přiřadili jste klienta Configuration Manager (Current Branch) pomocí určitého kódu lokality, nikoli pomocí automatického přiřazení lokality, a omylem jste zadali kód lokality pro verzi Configuration Manager starší než System Center 2012 R2 Configuration Manager.  

   V takovém případě se přiřazení lokality nezdařilo a klienta je nutné ručně znovu přiřadit k lokalitě Configuration Manager (aktuální větev).  

  Kontrola kompatibility lokality vyžaduje splnění jedné z následujících podmínek:  

- Klient může získat informace o lokalitě, které jsou publikovány do služby AD DS (Active Directory Domain Services).  

- Klient může komunikovat s bodem správy v lokalitě.  

  Pokud se ověření kompatibility lokality nepodaří úspěšně dokončit, přiřazení lokality se nezdaří a klient zůstane nespravovaný, dokud se nespustí ověření kompatibility lokality a nebude úspěšné.  

  Výjimka kontroly kompatibility lokality nastává, pokud je klient konfigurován pro internetový bod správy. V tomto případě není provedena žádná kontroly kompatibility lokality. Pokud přiřazujete klienty k lokalitě, která obsahuje internetové systémy lokality, a zadáte internetové body správy, ujistěte se, že klienta přiřazujete ke správné lokalitě. Pokud klienta omylem přiřadíte k lokalitě Configuration Manager 2007, webu nástroje System Center 2012 Configuration Manager nebo k Configuration Manager lokalitě, která nemá role internetového systému lokality, klient bude nespravován.  

##  <a name="locating-management-points"></a>Hledání bodů správy  
 Po úspěšném přiřazení klienta k lokalitě je možné vyhledat bod správy v lokalitě.  

 Klientské počítače stáhnou seznam bodů správy, ke kterým se mohou v lokalitě připojit. K tomu dochází vždy při restartování klienta nebo každých 25 hodin, nebo pokud klient zjistí změnu v síti, například když se počítač odpojí a znovu připojí k síti nebo obdrží novou IP adresu. Seznam obsahuje body správy na intranetu a informaci o tom, zda přijímají připojení klienta pomocí protokolu HTTP nebo HTTPS. Pokud je klientský počítač připojen k Internetu a klient ještě nemá seznam bodů správy, připojí se k zadanému internetovému bodu správy, aby získal seznam bodů správy. Jakmile klient získá seznam bodů správy pro přiřazenou lokalitu, vybere jeden, ke kterému se připojí:  

-   Když je klient připojen k intranetu a má platný certifikát PKI, který může použít, klient zvolí body správy protokolu HTTPS před body správy HTTP. Poté vyhledá nejbližší bod správy na základě členství v doménové struktuře.  

-   Když je klient připojen k Internetu, náhodně zvolí jeden z internetových bodů správy.  

Klienti mobilních zařízení, kteří jsou zaregistrovaní nástrojem Configuration Manager se připojují pouze k jednomu bodu správy v přiřazené lokalitě a nikdy se nepřipojují k bodům správy v sekundárních lokalitách. Tito klienti se vždy připojují přes protokol HTTPS a bod správy musí být konfigurován na připojení klientů přes internet. Pokud je pro klienty mobilních zařízení v primární lokalitě k dispozici více než jeden bod správy, Configuration Manager v rámci přiřazení náhodně zvolit jeden z těchto bodů správy a klient mobilního zařízení bude nadále používat stejný bod správy.  

Pokud klient stáhl zásady klienta z bodu správy v lokalitě, stane se spravovaným klientem.  

##  <a name="downloading-site-settings"></a>Stažení nastavení lokality  
 Po úspěšném přiřazení lokality a nalezení bodu správy klientem klientský počítač, který používá ke kontrole kompatibility lokality službu AD DS (Active Directory Domain Services), stáhne nastavení lokality související s klientem pro jemu přiřazenou lokalitu. Tato nastavení zahrnují kritéria výběru certifikátu klienta, použití seznamu odvolaných klientů a čísla portů požadavků klienta. Klient bude tato nastavení pravidelně kontrolovat.  

 Pokud klientský počítač nemůže získat nastavení lokality ze služby AD DS (Active Directory Domain Services), stáhnou je z bodu správy. Klientské počítače mohou nastavení lokality získat také při jejich instalaci pomocí klientské nabízené instalace, nebo je můžete zadat ručně pomocí souboru CCMSetup. exe a vlastností instalace klienta. Další informace o vlastnostech instalace klienta najdete v tématu [informace o vlastnostech instalace klienta](../../../core/clients/deploy/about-client-installation-properties.md).  

##  <a name="downloading-client-settings"></a>Stažení nastavení klienta  
 Všichni klienti stahují výchozí zásady nastavení klienta a jakékoli vlastní související zásady nastavení klienta. Centrum softwaru využívá tyto zásady konfigurace klienta pro počítače se systémem Windows a upozorní uživatele, že centrum softwaru nelze spustit, dokud nebudou staženy tyto informace o konfiguraci. V závislosti na nastaveních klienta, jež jsou konfigurována, může prvotní stažení nastavení klienta trvat delší dobu a některé úlohy správy klienta nemusí být možné spustit, dokud nebude postup dokončen.  

##  <a name="verifying-site-assignment"></a>Ověření přiřazení lokality  
 Úspěšnost přiřazení lokality můžete ověřit pomocí některé z následujících metod:  

-   U klientů v počítačích se systémem Windows použijte Configuration Manager v Ovládacích panelech a ověřte, zda je kód lokality správně zobrazen na kartě **Web** .  

-   U klientských počítačů **v uzlu >** pracovního prostoru **prostředky a kompatibilita** ověřte, zda je ve sloupci **klient** zobrazena hodnota **Ano** a ve sloupci **kód lokality** správný kód primární lokality.  

-   U klientů mobilních zařízení v pracovním prostoru **Prostředky a kompatibilita** použijte kolekci **Všechna mobilní zařízení** a ověřte, zda je ve sloupci **Klient** zobrazena hodnota **Ano** a ve sloupci **Kód lokality** správný kód primární lokality.  

-   Použijte sestavy přiřazení klientů a zápisu mobilních zařízení.  

-   U klientských počítačů použijte soubor klienta LocationServices.log.  

##  <a name="roaming-to-other-sites"></a>Přemístění do jiných lokalit  
 Když klientské počítače v intranetu přiřazené k primární lokalitě změní své umístění v síti tak, že spadají do hraniční skupiny konfigurované pro jinou lokalitu, hovoříme o jejich přemístění do jiné lokality. Pokud se jedná o sekundární lokalitu jim přiřazené lokality, klienti mohou použít bod správy v sekundární lokalitě ke stažení zásad klienta a odeslání klientských dat. Nemusí tedy přenášet data přes potenciálně pomalou síť. Pokud však dojde k přemístění klientů za hranice jiné primární lokality nebo sekundární lokality, která není podřízena jim přiřazené lokalitě, klienti budou při stahování zásad klienta a odesílání dat do své lokality vždy používat bod správy v jim přiřazené lokalitě.  

 Klientské počítače přemístěné do jiných primárních či sekundárních lokalit mohou vždy použít body správy v jiných lokalitách pro požadavky na umístění obsahu. Body správy v aktuální lokalitě mohou klientům poskytnout seznam distribučních bodů s obsahem, který tito klienti požadují.  

 Pro klientské počítače, které jsou nakonfigurovány pro správu pouze internetových klientů, a pro mobilní zařízení a počítače se systémem Mac, které jsou zapsány Configuration Manager, budou tito klienti komunikovat pouze s body správy v jim přiřazené lokalitě. Tito klienti nikdy nekomunikují s body správy v sekundárních lokalitách ani s body správy v jiných primárních lokalitách.  
