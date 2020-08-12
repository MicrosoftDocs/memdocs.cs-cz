---
title: Plánování aktualizací softwaru
titleSuffix: Configuration Manager
description: Plán pro infrastrukturu bodu aktualizace softwaru je nezbytný, než použijete aktualizace softwaru v Configuration Manager produkčním prostředí.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
ms.openlocfilehash: b7b3ef78924389232ea292d16c6840fbef9bb321
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88123587"
---
# <a name="plan-for-software-updates-in-configuration-manager"></a>Plánování aktualizací softwaru v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Než začnete používat aktualizace softwaru v produkčním prostředí Configuration Manager, je důležité projít si proces plánování. Dobrým plánem infrastruktury bodu aktualizace softwaru je klíč k úspěšné implementaci aktualizací softwaru. Informace o plánování kapacity pro aktualizace softwaru najdete v tématu věnovaném [velikostem a škálováním čísel](../../core/plan-design/configs/size-and-scale-numbers.md#software-update-point).


##  <a name="determine-the-software-update-point-infrastructure"></a><a name="BKMK_SUPInfrastructure"></a>Určení infrastruktury bodu aktualizace softwaru  

Tato část obsahuje následující podtémata:    
- [Seznam bodů aktualizace softwaru](#BKMK_SUPList)
- [Přepínání bodů aktualizace softwaru](#BKMK_SUPSwitching)
- [Ruční přepnutí klientů na nový bod aktualizace softwaru](#BKMK_ManuallySwitchSUPs)
- [Body aktualizace softwaru v nedůvěryhodné doménové struktuře](#BKMK_SUP_CrossForest)
- [Použití existujícího serveru WSUS jako zdroje synchronizace v lokalitě nejvyšší úrovně](#BKMK_WSUSSyncSource)
- [Bod aktualizace softwaru v sekundární lokalitě](#BKMK_SUPSecSite)  
- [Plánování internetových klientů](#bkmk_internet-clients)  
- [Plánování obsahu aktualizace softwaru](#bkmk_content)  
- [Plánování aktualizací třetích stran](#bkmk_thirdparty)  


Lokalita centrální správy a všechny podřízené primární lokality musí mít bod aktualizace softwaru. Při plánování infrastruktury bodu aktualizace softwaru určete následující závislosti:
- Kam se má nainstalovat bod aktualizace softwaru pro lokalitu  
- Které lokality vyžadují bod aktualizace softwaru, který přijímá komunikaci z internetových klientů
- Bez ohledu na to, zda potřebujete bod aktualizace softwaru v sekundárních lokalitách  

> [!IMPORTANT]  
>  Další informace o vnitřních a vnějších závislostech, které jsou požadovány pro aktualizace softwaru naleznete v tématu [předpoklady pro aktualizace softwaru](prerequisites-for-software-updates.md).  

Pokud chcete zajistit odolnost proti chybám, přidejte na Configuration Manager primární lokalitu více bodů aktualizace softwaru. Návrh převzetí služeb při selhání bodu aktualizace softwaru se liší od čistě modelu náhodnosti, který se používá v návrhu bodů správy. Na rozdíl od návrhu bodů správy jsou náklady na výkon klienta a sítě v návrhu bodu aktualizace softwaru, když klienti přepínají na nový bod aktualizace softwaru. Pokud klient přepíná na nový server WSUS, aby na něm vyhledal aktualizace softwaru, výsledkem je zvýšení velikosti katalogu a s tím související zvýšení nároků na výkon klienta a sítě. Klient proto zachovává spřažení s posledním bodem aktualizace softwaru, ze kterého byl úspěšně zkontrolován.  

První bod aktualizace softwaru, který nainstalujete do primární lokality, je zdrojem synchronizací pro všechny další body aktualizace softwaru, které přidáte do primární lokality. Po přidání bodů aktualizace softwaru a spuštění synchronizace zobrazte stav bodů aktualizace softwaru a zdroje synchronizace z uzlu **stav synchronizace bodu aktualizace softwaru** v pracovním prostoru **monitorování** .  

Pokud dojde k selhání bodu aktualizace softwaru nakonfigurovaného jako zdroj synchronizace pro lokalitu, ručně odeberte neúspěšnou roli. Pak vyberte nový bod aktualizace softwaru, který se použije jako zdroj synchronizace. Další informace najdete v tématu [Odebrání role systému lokality](../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#bkmk_role).  


###  <a name="software-update-point-list"></a><a name="BKMK_SUPList"></a> Seznam bodů aktualizace softwaru  

Configuration Manager poskytuje klientovi seznam bodů aktualizace softwaru v následujících scénářích:  

- Nový klient obdrží zásadu, která povolí aktualizace softwaru.  

- Klient nemůže kontaktovat přiřazený bod aktualizace softwaru a potřebuje přepnout na jiný.  

Klient náhodně vybere bod aktualizace softwaru ze seznamu. Určuje prioritu bodů aktualizace softwaru ve stejné doménové struktuře. Configuration Manager poskytuje klientům jiný seznam v závislosti na typu klienta:  

-   **Intranetové klienty**: dostanou seznam bodů aktualizace softwaru, které můžete nakonfigurovat tak, aby povolovaly připojení pouze z intranetu, nebo seznam bodů aktualizace softwaru, které umožňují připojení internetových a intranetových klientů.  

-   **Internetoví klienti**: dostanou seznam bodů aktualizace softwaru, které nakonfigurujete tak, aby povolovaly připojení pouze z Internetu, nebo seznam bodů aktualizace softwaru, které umožňují připojení internetových a intranetových klientů.  


###  <a name="software-update-point-switching"></a><a name="BKMK_SUPSwitching"></a>Přepínání bodů aktualizace softwaru  

> [!NOTE]  
> Klienti používají skupiny hranic k vyhledání nového bodu aktualizace softwaru. Pokud jejich aktuální bod aktualizace softwaru již není přístupný, používají skupiny hranic k záložnímu a hledání nového. Přidejte jednotlivé body aktualizace softwaru do různých skupin hranic, abyste mohli řídit, které servery může klient najít. Další informace najdete v tématu [body aktualizace softwaru](../../core/servers/deploy/configure/boundary-groups.md#bkmk_sup).  

Máte-li v jedné lokalitě více bodů aktualizace softwaru a jeden z nich selže nebo je nedostupný, klienti se připojí k jinému bodu aktualizace softwaru. U tohoto nového serveru budou klienti pokračovat ve vyhledávání nejnovějších aktualizací softwaru. Když se klientovi poprvé přiřadí bod aktualizace softwaru, zůstane přiřazený k tomuto bodu aktualizace softwaru, pokud se nepovede zkontrolovat.  

Vyhledávání aktualizací softwaru může selhat s několika různými kódy chyb s opakováním pokusu nebo bez něj. Pokud vyhledávání selže s kódem chyby s opakováním, klient se znovu pokusí vyhledat aktualizaci softwaru v bodě aktualizace softwaru. Podmínky nejvyšší úrovně, jež vyvolají kód chyby s opakování, jsou typicky způsobeny nedostupností serveru WSUS nebo jeho dočasným přetížením. Když se klientovi nepovede vyhledat aktualizace softwaru, použije následující postup:  

1.  Klient vyhledává aktualizace softwaru:  
    - V naplánovaném čase
    - Při ručním spuštění z ovládacích panelů na klientovi
    - Při ručním spuštění z konzoly Configuration Manager prostřednictvím akce klientského oznámení
    - Při spuštění z metody Configuration Manager SDK  

2.  Pokud se kontrola nezdařila, klient počká 30 minut, než se kontrola zopakuje. Používá stejný bod aktualizace softwaru.  

3.  Klient opakuje nejméně čtyři časy každých 30 minut. Po čtvrtém selhání se klient přesune na další bod aktualizace softwaru v seznamu a až počká dalších dvou minut.  

4.  Klient tento proces zopakuje s novým bodem aktualizace softwaru. Po úspěšné kontrole se klient bude nadále připojovat k novému bodu aktualizace softwaru.  

Následující seznam poskytuje další informace, které je vhodné zvážit pro scénáře opakování a přepínání bodů aktualizace softwaru:  

-   Pokud je klient odpojený od intranetu a nepodaří se mu vyhledat aktualizace softwaru, nepřepne na jiný bod aktualizace softwaru. Tato chyba je očekávaná, protože klient se nemůže připojit k interní síti nebo bodu aktualizace softwaru, který umožňuje připojení z intranetu. Klient Configuration Manager určí dostupnost intranetového bodu aktualizace softwaru.  

-   Pokud spravujete klienty na internetu a nakonfigurovali jste více bodů aktualizace softwaru, aby přijímaly komunikaci od klientů na internetu, proces přepínání bude postupovat podle standardního procesu opakování popsaného výše.  

-   Pokud se spustí proces skenování, ale klient je vypnutý, než se kontrola dokončí, nepovažuje se za selhání kontroly a nepočítá se jako jeden ze čtyř opakovaných pokusů.  

Když Configuration Manager obdrží některý z následujících kódů chyb web Windows Update agenta, klient se pokusí připojení znovu:  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

Chcete-li vyhledat význam kódu chyby, převeďte desítkový kód chyby na šestnáctkové a potom vyhledejte hexadecimální hodnotu v lokalitě, jako je například [Agent web Windows Update –](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx)kód chyby. 2149842970 je hexadecimální 8024001A, což znamená, že WU_E_POLICY_NOT_SET nebyla nastavena hodnota zásad.  


###  <a name="manually-switch-clients-to-a-new-software-update-point"></a><a name="BKMK_ManuallySwitchSUPs"></a>Ruční přepnutí klientů na nový bod aktualizace softwaru

Pokud dojde k problémům s aktivním bodem aktualizace softwaru, přepínejte Configuration Manager klientů na nový bod aktualizace softwaru. Tato změna proběhne pouze v případě, že klient obdrží více bodů aktualizace softwaru z bodu správy.

> [!IMPORTANT]    
> Když přepnete zařízení na použití nového serveru, zařízení k vyhledání nového serveru použije zálohu. Klienti v průběhu příštího cyklu prověřování aktualizací softwaru přepnou na nový bod aktualizace softwaru.<!-- SCCMDocs#1537 -->
>
> Než začnete s touto změnou, zkontrolujte konfigurace skupin hranic a ujistěte se, že jsou body aktualizace softwaru ve správných skupinách hranic. Další informace najdete v tématu [body aktualizace softwaru](../../core/servers/deploy/configure/boundary-groups.md#bkmk_sup).  
>
> Přepnutí na nový bod aktualizace softwaru vygeneruje další síťový provoz. Množství provozu závisí na nastavení konfigurace služby WSUS, například na synchronizovaných klasifikacích a produktech nebo na použití sdílené databáze služby WSUS. Pokud máte v úmyslu přepínat více zařízení, zvažte jejich použití při údržbě systému Windows. Tento čas omezuje dopad na vaši síť, když klienti prohledají pomocí nového bodu aktualizace softwaru.  

#### <a name="process-to-switch-software-update-points"></a>Proces přepínání bodů aktualizace softwaru  
Spustí tuto změnu v kolekci zařízení. Po aktivaci budou klienti při příští kontrole hledat jiný bod aktualizace softwaru.  

1.  V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte uzel **kolekce zařízení** .  

2.  Vyberte cílovou kolekci. Na kartě **Domů** na pásu karet ve skupině **kolekce** klikněte na **klientské oznámení**a pak klikněte na **Přepnout na další bod aktualizace softwaru**.  


###  <a name="software-update-points-in-an-untrusted-forest"></a><a name="BKMK_SUP_CrossForest"></a> Body aktualizace softwaru v nedůvěryhodné doménové struktuře  

Vytvoření jednoho nebo více bodů aktualizace softwaru v lokalitě pro podporu klientů v nedůvěryhodné doménové struktuře. Chcete-li přidat bod aktualizace softwaru v jiné doménové struktuře, nejprve nainstalujte a nakonfigurujte server WSUS v této doménové struktuře. Poté spusťte průvodce a přidejte Configuration Manager Server lokality s rolí systému lokality bodu aktualizace softwaru. V průvodci nakonfigurujte následující nastavení, aby bylo možné připojit se k serveru WSUS v nedůvěryhodné struktuře:  

-   Zadejte **účet instalace systému lokality** , který má přístup k serveru WSUS v nedůvěryhodné doménové struktuře.  

-   Zadejte **účet pro připojení k serveru WSUS** , který se má připojit k serveru WSUS.  

Máte například primární lokalitu ve struktuře A s dvěma softwarovými body (SUP01 a SUP02). Pro stejnou primární lokalitu máte také dva body aktualizace softwaru (SUP03 a SUP04) v doménové struktuře B. Při přechodu na další bod aktualizace softwaru budou klienti upřednostňovat servery ze stejné doménové struktury.  


###  <a name="use-an-existing-wsus-server-as-the-synchronization-source-at-the-top-level-site"></a><a name="BKMK_WSUSSyncSource"></a>Použití existujícího serveru WSUS jako zdroje synchronizace v lokalitě nejvyšší úrovně  

Lokalita vysoké úrovně ve vaší hierarchii je typicky nakonfigurována k synchronizaci metadat aktualizace softwaru pomocí služby Microsoft Update. Pokud zásady zabezpečení vaší organizace nedovolují lokalitě nejvyšší úrovně přístup k Internetu, nakonfigurujte zdroj synchronizace pro lokalitu nejvyšší úrovně tak, aby používal existující server WSUS. Tento server WSUS není ve vaší Configuration Manager hierarchii. Například máte server WSUS v síti připojené k Internetu (DMZ), ale lokalita nejvyšší úrovně je v interní síti bez přístupu k Internetu. Nakonfigurujte server WSUS v DMZ jako zdroj synchronizace pro metadata aktualizací softwaru. Nakonfigurujte server WSUS v DMZ tak, aby synchronizoval aktualizace softwaru se stejnými kritérii, jaká potřebujete v Configuration Manager. V opačném případě nemusí lokalita vysoké úrovně synchronizovat aktualizace softwaru, které byste očekávali. Při instalaci bodu aktualizace softwaru nakonfigurujte účet pro připojení k serveru WSUS. Tento účet potřebuje přístup k serveru WSUS v DMZ. Ověřte také, že brána firewall povoluje provoz pro příslušné porty. Další informace najdete v tématu [porty používané bodem aktualizace softwaru ke zdroji synchronizace](../../core/plan-design/hierarchy/ports.md#BKMK_PortsSUP-WSUS).  


###  <a name="software-update-point-on-a-secondary-site"></a><a name="BKMK_SUPSecSite"></a> Bod aktualizace softwaru v sekundární lokalitě  

Bod aktualizace softwaru je v sekundární lokalitě volitelný. Nainstalujte pouze jeden bod aktualizace softwaru v sekundární lokalitě. Pokud bod aktualizace softwaru není nainstalován v sekundární lokalitě, zařízení v rámci hranic sekundární lokality používají bod aktualizace softwaru v přiřazené primární lokalitě. Bod aktualizace softwaru se obvykle nainstaluje v sekundární lokalitě, pokud je omezena šířka pásma sítě mezi zařízeními v sekundární lokalitě a body aktualizace softwaru v nadřazené primární lokalitě. Tuto konfiguraci můžete použít také v případě, že se bod aktualizace softwaru v primární lokalitě blíží limitu kapacity. Po úspěšné instalaci a konfiguraci bodu aktualizace softwaru v sekundární lokalitě se zásady pro všechny lokality aktualizují pro klienty a začnou používat nový bod aktualizace softwaru.  


### <a name="plan-for-internet-based-clients"></a><a name="bkmk_internet-clients"></a>Plánování internetových klientů

Pokud potřebujete spravovat zařízení, která se v síti přecházejí z vaší sítě na Internet, vytvořte plán, jak spravovat aktualizace softwaru na těchto zařízeních. Configuration Manager podporuje několik technologií pro tento scénář. Použijte jednu nebo kombinaci podle potřeby pro splnění požadavků vaší organizace.

#### <a name="cloud-management-gateway"></a>Brána pro správu cloudu
Vytvořte bránu pro správu cloudu v Microsoft Azure a povolte aspoň jeden místní bod aktualizace softwaru, aby bylo možné povolit přenosy z internetových klientů. Když klienti přecházejí na Internet, budou i nadále kontrolovat body aktualizace softwaru. Všichni internetoví klienti vždycky získají obsah z cloudové služby Microsoft Update. 

Další informace najdete v tématu [Plánování brány pro správu cloudu](../../core/clients/manage/cmg/plan-cloud-management-gateway.md) a [Konfigurace skupin hranic](../../core/servers/deploy/configure/boundary-groups.md#bkmk_sup).  

#### <a name="internet-based-client-management"></a>Internetová správa klientů
Umístěte bod aktualizace softwaru do internetové sítě a umožněte mu povolit provoz z internetových klientů. Když klienti přecházejí na Internet, přepnou se do tohoto bodu aktualizace softwaru pro kontrolu. Všichni internetoví klienti vždycky získají obsah z cloudové služby Microsoft Update.

Další informace o výhodách a nevýhodách internetové správy klientů najdete v tématu [Správa klientů na internetu](../../core/clients/manage/manage-clients-internet.md).

#### <a name="windows-update-for-business"></a>web Windows Update pro firmy
Web Windows Update pro firmy vám umožní udržovat zařízení s Windows 10 vždycky aktuální s nejnovějšími aktualizacemi kvality a funkcí. Tato zařízení se připojují přímo ke cloudové službě web Windows Update. Configuration Manager může rozlišovat mezi počítači s Windows 10, které k získávání aktualizací softwaru používají WUfB a WSUS.

Další informace najdete v tématu [integrace s web Windows Update pro firmy](../deploy-use/integrate-windows-update-for-business-windows-10.md).


### <a name="plan-software-update-content"></a><a name="bkmk_content"></a>Plánování obsahu aktualizace softwaru

Klienti potřebují stáhnout soubory obsahu pro aktualizace softwaru, aby je bylo možné nainstalovat. Configuration Manager poskytuje několik technologií pro podporu správy a doručování tohoto obsahu. Nebo můžete nakonfigurovat nasazení aktualizací softwaru tak, aby klienti mohli nebo potřebují získávat obsah přímo z cloudové služby Microsoft Update.

#### <a name="download-and-distribute-content"></a>Stažení a distribuce obsahu 
Ve výchozím nastavení proces správy aktualizací softwaru v Configuration Manager používá integrované funkce správy obsahu. Mezi tyto funkce patří centralizovaná knihovna obsahu úložiště s jednou instancí a distribuovaná návrh role systému lokality distribučního bodu. Tyto funkce můžete používat při stahování a distribuci balíčků pro nasazení aktualizací softwaru. 

Další informace najdete v tématu [Stažení aktualizací softwaru](../deploy-use/download-software-updates.md).

#### <a name="manage-express-installation-files-for-windows-10"></a>Správa souborů Expresní instalace pro Windows 10
Configuration Manager podporuje použití souborů Expresní instalace pro aktualizace Windows 10. Soubory Expresní aktualizace a podpůrné technologie, jako je optimalizace doručování, mohou přispět k omezení vlivu na síť velkých souborů obsahu, které se stahují do klientů. 

Další informace najdete v tématu [optimalizace doručování aktualizací Windows 10](../deploy-use/optimize-windows-10-update-delivery.md).

#### <a name="clients-download-content-from-the-internet"></a>Klienti stahují obsah z Internetu
Když nasadíte aktualizace softwaru na klienty, nakonfigurujte nasazení pro klienty, aby stahoval obsah z cloudové služby Microsoft Update. Když klienti nebudou moct stahovat obsah z jiného zdroje obsahu, můžou si ho stáhnout i z Internetu. 

Počínaje verzí 1806 není nutné při nasazování aktualizací softwaru vytvořit balíček pro nasazení. Vyberete-li možnost **bez balíčku pro nasazení** , mohou klienti nadále stahovat obsah z místních zdrojů, pokud jsou k dispozici, ale obvykle stahovat z Microsoft Update služby.<!--1357933-->

Internetoví klienti vždycky stahují obsah z cloudové služby Microsoft Update. Nedistribuujte balíčky pro nasazení aktualizace softwaru do distribučního bodu cloudu. Účtuje se vám úložiště s distribučním bodem cloudu, ale klienti tyto balíčky nestahují. 


### <a name="plan-for-third-party-updates"></a><a name="bkmk_thirdparty"></a>Plánování aktualizací třetích stran
Configuration Manager se integruje se službou WSUS, která nativně podporuje aktualizace softwaru publikované Microsoftem. Většina zákazníků používá jiné aplikace třetích stran, které potřebují taky aktualizace. Existuje několik možností, které je potřeba vzít v úvahu, pokud chcete, aby byly aplikace třetích stran v aktuálním stavu.

#### <a name="supersede-applications-to-update"></a>Nahradit aplikace, které se mají aktualizovat
Pokud chcete upgradovat nebo nahradit existující aplikace, použijte ve službě Configuration Manager vztah nahrazování. Při nahrazování aplikace zadejte nový typ nasazení, který nahradí typ nasazení nahrazené aplikace. Také se rozhodněte, jestli chcete před instalací nahrazující aplikace upgradovat nebo odinstalovat nahrazenou aplikaci.

Další informace najdete v tématu [Revize a nahrazování aplikací](../../apps/deploy-use/revise-and-supersede-applications.md).

#### <a name="third-party-software-updates"></a>Aktualizace softwaru třetích stran
Počínaje verzí 1806 použijte uzel **katalogy aktualizací softwaru třetích stran** v konzole Configuration Manager k přihlášení k odběru katalogů třetích stran, publikování jejich aktualizací do bodu aktualizace softwaru a jejich nasazení na klienty.<!--1352101-->

Další informace najdete v tématu [aktualizace softwaru třetích stran](../deploy-use/third-party-software-updates.md).

#### <a name="system-center-updates-publisher"></a>System Center aktualizuje Publisher 2011
System Center Updates Publisher (SCUP) je samostatný nástroj, který umožňuje nezávislým výrobcům softwaru nebo vývojářům obchodních aplikací spravovat vlastní aktualizace. Tyto aktualizace zahrnují ty se závislostmi, jako jsou ovladače a sady aktualizací.

Další informace najdete v tématu [System Center Updates Publisher](../tools/updates-publisher.md).



##  <a name="plan-for-software-update-point-installation"></a><a name="BKMK_SUPInstallation"></a>Plánování instalace bodu aktualizace softwaru  

Tato část obsahuje následující podtémata:  
- [Požadavky na bod aktualizace softwaru](#BKMK_SUPSystemRequirements)
- [Plánování instalace služby WSUS](#BKMK_PlanningForWSUS)
- [Konfigurace bran firewall](#BKMK_ConfigureFirewalls)  


V této části najdete informace o krocích, které je potřeba provést k úspěšnému dokončení plánování a přípravy instalace bodu aktualizace softwaru. Než vytvoříte roli systému lokality pro bod aktualizace softwaru v Configuration Manager, je třeba zvážit několik požadavků. Konkrétní požadavky závisí na vaší infrastruktuře Configuration Manager. Když nakonfigurujete bod aktualizace softwaru tak, aby komunikoval pomocí protokolu HTTPS, je tato část obzvláště důležitá pro kontrolu. Servery s povoleným protokolem HTTPS vyžadují další kroky, aby správně fungovaly.  

###  <a name="requirements-for-the-software-update-point"></a><a name="BKMK_SUPSystemRequirements"></a>Požadavky na bod aktualizace softwaru  

Nainstalujte roli bodu aktualizace softwaru v systému lokality, který splňuje minimální požadavky pro službu WSUS a podporované konfigurace pro Configuration Manager systémy lokality.  

-   Další informace o minimálních požadavcích na roli serveru WSUS v systému Windows Server najdete v tématu [Kontrola důležitých hodnot a požadavky na systém](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/plan/plan-your-wsus-deployment#11-review-considerations-and-system-requirements).  

-   Další informace o podporovaných konfiguracích systémů lokality Configuration Manager najdete v tématu [požadavky na lokalitu a systém lokality](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  


###  <a name="plan-for-wsus-installation"></a><a name="BKMK_PlanningForWSUS"></a>Plánování instalace služby WSUS  

Nainstalujte podporovanou verzi služby WSUS na všechny servery systému lokality, které nakonfigurujete pro roli bodu aktualizace softwaru. Pokud nenainstalujete bod aktualizace softwaru na server lokality, nainstalujte konzolu pro správu služby WSUS na server lokality. Tato součást umožňuje serveru lokality komunikovat se službou WSUS, která běží v bodě aktualizace softwaru.  

Pokud používáte službu WSUS v systému Windows Server 2012 nebo novější, nakonfigurujte další oprávnění, která umožní komponentě **služby WSUS Configuration Manager** v Configuration Manager připojit se ke službě WSUS. Tato součást provádí pravidelné kontroly stavu. Pro konfiguraci požadovaného oprávnění vyberte jednu z následujících možností:  

-   Přidání účtu **SYSTEM** do skupiny **Správci služby WSUS** .  

-   Přidejte účet **NT AUTHORITY\SYSTEM** jako uživatele pro databázi WSUS (SUSDB). Nakonfigurujte minimálně členství v roli databáze webService.  
  
Další informace o tom, jak nainstalovat službu WSUS na Windows Server, najdete v tématu [instalace role serveru WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/1-install-the-wsus-server-role).  

Při instalaci více než jednoho bodu aktualizace softwaru v primární lokalitě použijte stejnou databázi WSUS pro všechny body aktualizace softwaru ve stejné doménové struktuře Active Directory. Sdílení stejné databáze zvyšuje výkon při přepnutí klientů na nový bod aktualizace softwaru. Další informace najdete v tématu [použití sdílené databáze služby WSUS pro body aktualizace softwaru](software-updates-best-practices.md#bkmk_shared-susdb).  

#### <a name="configuring-the-wsus-content-directory-path"></a>Konfigurace cesty k adresáři obsahu služby WSUS

Při instalaci služby WSUS budete muset zadat cestu k adresáři obsahu. Adresář obsahu služby WSUS se primárně používá k ukládání souborů licenčních podmínek pro software společnosti Microsoft, které jsou potřeba pro klienty během kontroly. Configuration Manager adresář obsahu služby WSUS by se neměl překrývat se zdrojovým adresářem obsahu pro balíčky nasazení Configuration Manager softwaru. Překrývající se adresář obsahu služby WSUS a zdroj Configuration Manager balíčku budou mít za následek odebrání nesprávného souboru z adresáře obsahu služby WSUS.

####  <a name="configure-wsus-to-use-a-custom-website"></a><a name="BKMK_CustomWebSite"></a>Konfigurace služby WSUS pro použití vlastního webu  
Při instalaci serveru WSUS je možné použít existující výchozí web IIS nebo vytvořit vlastní web WSUS. Vytvořte vlastní web pro server WSUS, aby služba IIS byla hostitelem služeb WSUS ve vyhrazeném virtuálním webu. V opačném případě sdílí stejný web, který používají ostatní systémy nebo aplikace Configuration Manager lokality. Tato konfigurace je zvlášť nutná při instalaci role bodu aktualizace softwaru na server lokality. Pokud spustíte službu WSUS v systému Windows Server 2012 nebo novější, bude služba WSUS ve výchozím nastavení nakonfigurována tak, aby používala port 8530 pro protokol HTTP a port 8531 pro protokol HTTPS. Při vytváření bodu aktualizace softwaru v lokalitě zadejte tyto porty.  


####  <a name="use-an-existing-wsus-infrastructure"></a><a name="BKMK_WSUSInfrastructure"></a>Použití existující infrastruktury služby WSUS  
Než nainstalujete Configuration Manager jako bod aktualizace softwaru, vyberte server WSUS, který byl aktivní ve vašem prostředí. Pokud je bod aktualizace softwaru nakonfigurován, zadejte nastavení synchronizace. Configuration Manager se připojí k serveru WSUS, na kterém běží na serveru bodu aktualizace softwaru, a nakonfiguruje službu WSUS se stejným nastavením. 

Před konfigurací serveru jako bodu aktualizace softwaru Porovnejte konfiguraci produktů a klasifikací s nastavením Configuration Manager. Pokud jste existující server WSUS synchronizovali před jeho konfigurací jako bod aktualizace softwaru a seznam produktů a klasifikací se liší, synchronizuje všechna metadata aktualizací softwaru bez ohledu na nakonfigurované nastavení. Výsledkem tohoto chování je neočekávaná metadata aktualizace softwaru v databázi lokality. 

Stejné chování se zobrazí při přidávání produktů nebo klasifikací přímo v konzole pro správu služby WSUS a následném zahájení synchronizace. Ve výchozím nastavení se každá hodina Configuration Manager připojí ke službě WSUS a resetuje všechna nastavení, která byla změněna mimo Configuration Manager. Aktualizace softwaru, které neodpovídají produktům a klasifikacím zadaným v nastaveních synchronizace, jsou nastavené jako prošlé. Pak jsou odebrány z databáze lokality.  

Pokud je server WSUS nakonfigurovaný jako bod aktualizace softwaru, už ho nebudete moct používat jako samostatný server WSUS. Pokud potřebujete samostatný samostatný server WSUS, který není spravovaný nástrojem Configuration Manager, nakonfigurujte ho na jiném serveru.  

####  <a name="configure-wsus-as-a-replica-server"></a><a name="BKMK_WSUSAsReplica"></a> Konfigurace serveru WSUS jako serveru repliky  
Když přidáte roli bodu aktualizace softwaru na primární server lokality, nemůžete použít server WSUS, který je nakonfigurovaný jako replika. Pokud je server WSUS nakonfigurovaný jako replika, Configuration Manager se nepovede nakonfigurovat server WSUS a synchronizace WSUS se nezdařila. První bod aktualizace softwaru, který nainstalujete v primární lokalitě, je výchozím bodem aktualizace softwaru. Další body aktualizace softwaru v lokalitě jsou konfigurovány jako repliky výchozího bodu aktualizace softwaru.  

####  <a name="decide-whether-to-configure-wsus-to-use-ssl"></a><a name="BKMK_WSUSandSSL"></a> Rozhodnutí ohledně konfigurace serveru WSUS pro použití protokolu SSL  
Použijte protokol SSL k zajištění zabezpečení bodu aktualizace softwaru. Služba WSUS používá protokol SSL při ověřování klientských počítačů a podřízených serverů WSUS daného serveru. Server WSUS využívá protokol SSL také k šifrování metadat aktualizace softwaru. Pokud se rozhodnete zabezpečit službu WSUS pomocí protokolu SSL, připravte server WSUS před instalací bodu aktualizace softwaru. Další informace najdete v článku [Konfigurace protokolu SSL v serveru WSUS](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) v dokumentaci pro službu WSUS. 

Když nainstalujete a nakonfigurujete bod aktualizace softwaru, vyberte možnost **povolení komunikace SSL pro server WSUS**. V opačném případě Configuration Manager nakonfiguruje službu WSUS, aby nepoužívala protokol SSL. Pokud povolíte protokol SSL v bodě aktualizace softwaru, nakonfigurujte také všechny body aktualizace softwaru v podřízených lokalitách, aby používaly protokol SSL.  


###  <a name="configure-firewalls"></a><a name="BKMK_ConfigureFirewalls"></a>Konfigurace bran firewall  

Bod aktualizace softwaru v Configuration Manager lokalitě centrální správy komunikuje se službou WSUS v bodu aktualizace softwaru. Služba WSUS komunikuje se zdrojem synchronizace a synchronizuje metadata aktualizací softwaru. Body aktualizace softwaru v podřízené lokalitě komunikují s bodem aktualizace softwaru v nadřazené lokalitě. Pokud je v primární lokalitě více než jeden bod aktualizace softwaru, budou další body aktualizace softwaru komunikovat s výchozím bodem aktualizace softwaru. Výchozí rolí je první bod aktualizace softwaru nainstalovaný v lokalitě.  

Možná budete muset nakonfigurovat bránu firewall, aby povolovala přenosy HTTP nebo HTTPS, které služba WSUS používá v následujících scénářích: 
- Mezi bodem aktualizace softwaru a internetem
- Mezi bodem aktualizace softwaru a nadřazeným zdrojem synchronizace
- Mezi dalšími body aktualizace softwaru  

Připojení ke službě Microsoft Update vždy využívá port 80 pro protokol HTTP a port 443 pro protokol HTTPS. Použijte vlastní port pro připojení ze služby WSUS v bodě aktualizace softwaru v podřízené lokalitě ke službě WSUS v bodu aktualizace softwaru v nadřazené lokalitě. Pokud vaše zásada zabezpečení nepovoluje připojení, použijte metodu synchronizace export a import. Další informace najdete v části [zdroj synchronizace](#BKMK_SyncSource) v tomto článku. Další informace o portech, které služba WSUS používá, najdete [v tématu Postup určení nastavení portu používaného službou WSUS v Configuration Manager](../get-started/install-a-software-update-point.md#wsus-settings).  


#### <a name="restrict-access-to-specific-domains"></a>Omezení přístupu ke konkrétním doménám  

Pokud vaše organizace omezuje síťovou komunikaci s Internetem pomocí brány firewall nebo proxy zařízení, je nutné povolit aktivnímu bodu aktualizace softwaru přístup k internetovým koncovým bodům. Služba WSUS a automatické aktualizace pak můžou komunikovat s Microsoft Update cloudovou službou.

Další informace najdete v tématu [požadavky na přístup k Internetu](../../core/plan-design/network/internet-endpoints.md#bkmk_sum).


##  <a name="plan-for-synchronization-settings"></a><a name="BKMK_SyncSettings"></a> Plánování nastavení synchronizace  

Tato část obsahuje následující podtémata:  
- [Zdroj synchronizace](#BKMK_SyncSource)
- [Plán synchronizace](#BKMK_SyncSchedule)
- [Klasifikace aktualizací](#BKMK_UpdateClassifications)
- [Produktech](#BKMK_UpdateProducts)
- [Pravidla nahrazení](#BKMK_SupersedenceRules)
- [Jazyky](#BKMK_UpdateLanguages)  
- [Maximální doba běhu](#bkmk_maxruntime)


Synchronizace aktualizací softwaru v Configuration Manager stahuje metadata aktualizací softwaru na základě kritérií, která nakonfigurujete. Lokalita nejvyšší úrovně ve vaší hierarchii synchronizuje aktualizace softwaru od Microsoft Update. Můžete nakonfigurovat, aby se bod aktualizace softwaru v lokalitě nejvyšší úrovně synchronizoval s existujícím serverem WSUS, nikoli v hierarchii Configuration Manager. Podřízené primární lokality synchronizují metadata aktualizací softwaru z bodu aktualizace softwaru v lokalitě centrální správy. Než nainstalujete a nakonfigurujete bod aktualizace softwaru, naplánujte podle informací v této části nastavení synchronizací.  


###  <a name="synchronization-source"></a><a name="BKMK_SyncSource"></a> Zdroj synchronizace  

Nastavení zdroje synchronizace pro bod aktualizace softwaru určuje umístění, kde bod aktualizace softwaru Získá metadata aktualizace softwaru. Určuje také, zda proces synchronizace vytváří události vytváření sestav služby WSUS.  

-   **Zdroj synchronizace**: ve výchozím nastavení bod aktualizace softwaru v lokalitě nejvyšší úrovně konfiguruje zdroj synchronizace pro Microsoft Update. Lokalitu nejvyšší úrovně můžete synchronizovat s existujícím serverem WSUS. Bod aktualizace softwaru v podřízené primární lokalitě konfiguruje zdroj synchronizace jako bod aktualizace softwaru v lokalitě centrální správy.  

    -  První bod aktualizace softwaru, který nainstalujte v primární lokalitě (výchozí bod aktualizace softwaru), se synchronizuje s lokalitou centrální správy. Další body aktualizace softwaru v primární lokalitě se synchronizují s výchozím bodem aktualizace softwaru v primární lokalitě.  

    - Pokud je bod aktualizace softwaru odpojen od Microsoft Update nebo z nadřazeného serveru aktualizace, nakonfigurujte zdroj synchronizace tak, aby se nesynchronizoval s nakonfigurovaným zdrojem synchronizace. Místo toho ji nakonfigurujte tak, aby používala funkci exportu a importu nástroje **WSUSutil** k synchronizaci aktualizací softwaru. Další informace najdete v tématu [Synchronizace aktualizací softwaru z odpojeného bodu aktualizace softwaru](../get-started/synchronize-software-updates-disconnected.md).  

-   **Události vytváření sestav služby WSUS:** Agent web Windows Update v klientských počítačích může vytvářet zprávy událostí pro vytváření sestav služby WSUS. Tyto události nejsou používány nástrojem Configuration Manager. Proto je ve výchozím nastavení vybrána možnost **Nevytvářet události vytváření sestav služby WSUS**. Pokud se tyto události nevytvářejí, jediný čas, kdy se má klient připojit k serveru WSUS, je během hodnocení aktualizací softwaru a kontroly dodržování předpisů. Pokud jsou tyto události potřeba pro vytváření sestav mimo Configuration Manager, změňte toto nastavení tak, aby se události vytváření sestav služby WSUS vytvořily.  


###  <a name="synchronization-schedule"></a><a name="BKMK_SyncSchedule"></a> Plán synchronizace  

Plán synchronizace nakonfigurujte pouze v bodě aktualizace softwaru v lokalitě nejvyšší úrovně v hierarchii Configuration Manager. Pokud nakonfigurujete plán synchronizace, bude se bod aktualizace softwaru synchronizovat se zdrojem synchronizace v den a čas, který nastavíte. Vlastní plán umožňuje synchronizovat aktualizace softwaru, které se mají optimalizovat pro vaše prostředí. Vezměte v úvahu nároky na výkon serveru WSUS, serveru lokality a sítě. Například 2:00 AM jednou týdně. Případně ručně spusťte synchronizaci v lokalitě nejvyšší úrovně pomocí akce **synchronizace aktualizací softwaru** z uzlu **všechny aktualizace softwaru** nebo **skupiny aktualizací softwaru** v konzole Configuration Manager.  

> [!TIP]  
>  Naplánujte synchronizaci aktualizací softwaru tak, aby běžely, a to s využitím času, který je vhodný pro vaše prostředí. Jednou z běžných scénářů je nastavit plán synchronizace, který se spustí krátce po běžném vydání aktualizace softwaru od společnosti Microsoft v druhém úterý v měsíci. Tento den se obvykle označuje jako *patch úterý*. Použijete-li Configuration Manager k doručování Endpoint Protection a definicí a aktualizací v programu Windows Defender, zvažte nastavení plánu synchronizace na každodenní spouštění.  

Po úspěšné synchronizaci bodu aktualizace softwaru pošle žádost o synchronizaci podřízeným webům. Pokud máte další body aktualizace softwaru v primární lokalitě, pošle požadavek na synchronizaci do každého bodu aktualizace softwaru. Tento proces se opakuje na všech lokalitách v hierarchii.  


###  <a name="update-classifications"></a><a name="BKMK_UpdateClassifications"></a> klasifikace aktualizací;  

Každá aktualizace softwaru je definována pomocí klasifikace aktualizace, která pomáhá organizovat různé typy aktualizací. Během procesu synchronizace lokalita synchronizuje metadata pro zadané klasifikace. 

Configuration Manager podporuje synchronizaci následujících klasifikací aktualizací:  

-   **Důležité aktualizace**: široce vydaná aktualizace pro určitý problém, která řeší kritickou chybu, která nesouvisí se zabezpečením.  

-   **Aktualizace definic**: aktualizace virů nebo jiných definičních souborů.  

-   **Balíčky funkcí**: nové funkce produktu, distribuované mimo vydání produktu a jsou obvykle zahrnuté v příštím plném vydání produktu.  

-   **Aktualizace zabezpečení**: široce vydaná aktualizace pro problém související se zabezpečením určitého produktu.  

-   **Aktualizace Service Pack**: kumulativní sada oprav hotfix, které se aplikují na operační systém nebo aplikaci. Tyto opravy hotfix zahrnují aktualizace zabezpečení, důležité aktualizace a aktualizace softwaru.  

-   **Nástroje**: nástroj nebo funkce, které pomáhají dokončit jednu nebo více úloh.  

-   **Kumulativní aktualizace**: kumulativní sada oprav hotfix, která je zabalená dohromady pro snadné nasazení. Tyto opravy hotfix zahrnují aktualizace zabezpečení, důležité aktualizace a aktualizace softwaru. Kumulativní aktualizace obecně řeší určitou oblast, například zabezpečení nebo součást produktu.  

-   **Aktualizace**: aktualizace aplikace nebo souboru, který je aktuálně nainstalován.  

-   **Upgrady**: aktualizace funkcí na novou verzi Windows 10.  

Nakonfigurujte nastavení klasifikace aktualizace pouze v lokalitě nejvyšší úrovně. Nastavení klasifikace aktualizací není konfigurováno v bodu aktualizace softwaru v podřízených lokalitách, protože metadata aktualizací softwaru se replikují z lokality vysoké úrovně. Když vyberete klasifikace aktualizací, mějte na paměti, že čím více klasifikací zvolíte, tím déle bude synchronizace metadat aktualizací softwaru trvat.  

> [!WARNING]  
>  Jako osvědčený postup vymažte všechny klasifikace před prvním synchronizací. Po počáteční synchronizaci vyberte požadované klasifikace a pak znovu spusťte synchronizaci.  


###  <a name="products"></a><a name="BKMK_UpdateProducts"></a>Produktech  

Metadata pro jednotlivé aktualizace softwaru definují jeden nebo více produktů, pro které je aktualizace k dispozici. Produkt je konkrétní edice operačního systému nebo aplikace. Příkladem produktu je Microsoft Windows 10. Produktová řada je základní operační systém nebo aplikace, ze které jsou jednotlivé produkty odvozené. Příkladem produktové řady je Microsoft Windows, z něhož jsou členové Windows 10 a Windows Server 2016 členy. Vyberte produktovou řadu nebo jednotlivé produkty v rámci řady produktů.  

Pokud se aktualizace softwaru vztahují k více produktům a pro synchronizaci je vybrán alespoň jeden z produktů, v konzole Configuration Manager se zobrazí všechny produkty, i když některé z nich nebyly vybrány. Například vyberete pouze produkt Windows Server 2012. Pokud se aktualizace softwaru vztahuje na systémy Windows Server 2012 a Windows Server 2012 Datacenter Edition, v databázi lokality jsou oba produkty.  

Nastavení produktu konfigurujte pouze v lokalitě nejvyšší úrovně. Nastavení produktu není nakonfigurováno v bodu aktualizace softwaru pro podřízené lokality, protože metadata aktualizací softwaru se replikují z lokality vysoké úrovně. Čím více produktů vyberete, tím déle bude synchronizace metadat aktualizací softwaru trvat.  

> [!IMPORTANT]  
>  Configuration Manager ukládá seznam produktů a řad produktů, které si vyberete při první instalaci bodu aktualizace softwaru. Produkty a řady produktů vydané po vydání Configuration Manager nemusí být k dispozici pro výběr, dokud nedokončíte synchronizaci. Proces synchronizace aktualizuje seznam dostupných produktů a rodin produktů, ze kterých si můžete vybrat. Před první synchronizací aktualizací softwaru vymažte všechny produkty. Po počáteční synchronizaci vyberte požadované produkty a pak znovu spusťte synchronizaci.  


###  <a name="supersedence-rules"></a><a name="BKMK_SupersedenceRules"></a>Pravidla nahrazení  

Aktualizace softwaru, která nahrazuje jinou aktualizaci softwaru, má typicky některé z těchto vlastností:  

-   zdokonaluje, zlepšuje nebo aktualizuje opravu, která byla vydána v některé z předchozích aktualizací.  

-   Zlepšuje efektivitu balíčku balíčku aktualizací, který je nainstalován v klientech nástroje, pokud je aktualizace schválena k instalaci. Nahrazená aktualizace může například obsahovat soubory, které již nejsou důležité pro opravu nebo pro operační systémy, které jsou podporovány novou aktualizací. Tyto soubory nejsou zahrnuty v nahrazujícím balíčku souboru aktualizace.  

-   Aktualizuje novější verze produktu. Jinými slovy, aktualizuje verze, které již nejsou použitelné pro starší verze nebo konfigurace produktu. Aktualizace mohou rovněž nahrazovat jiné aktualizace, pokud byly provedeny úpravy za účelem rozšíření jazykové podpory. Například pozdější revize aktualizace produktu pro Microsoft 365 aplikace může odebrat podporu pro starší operační systém, ale může přidat další podporu nových jazyků v úvodním vydání aktualizace.  

Ve vlastnostech bodu aktualizace softwaru určete, že Nahrazené aktualizace softwaru budou okamžitě vypršet. Toto nastavení brání zahrnutí do nových nasazení. Také označí existující nasazení, aby označovala, že obsahují jednu nebo více aktualizací softwaru s vypršenou platností. Nebo zadejte časový interval, po jehož uplynutí vyprší platnost nahrazených aktualizací softwaru. Tato akce vám umožní pokračovat v jejich nasazení. 

Zvažte následující scénáře, ve kterých může být zapotřebí nasadit nahrazenou aktualizaci softwaru:  

-   Nahrazující aktualizace softwaru podporuje pouze novější verze operačního systému. Některé klientské počítače používají dřívější verze operačního systému.  

-   Nahrazující aktualizace softwaru má více omezené použitelnosti než aktualizace softwaru, kterou nahrazuje. Toto chování by nemohlo být pro některé klienty vhodné.  

-   Pokud nahrazující aktualizace softwaru nebyla schválena k nasazení v produkčním prostředí.  

    > [!NOTE]  
    > - Před verzí 1806 Configuration Manager, když Configuration Manager nastaví platnost nahrazené aktualizace softwaru na **vypršela**, nenastaví aktualizaci na **Odmítnuto** ve službě WSUS. Klienti budou pokračovat ve vyhledávání aktualizace s vypršenou platností, dokud se aktualizace neodmítla ručně nebo prostřednictvím vlastního skriptu.  Po Configuration Manager verze 1806 Configuration Manager také odmítnou nahrazené aktualizace ve službě WSUS. Další informace o úloze vyčištění služby WSUS najdete v tématu [Údržba aktualizací softwaru](../deploy-use/software-updates-maintenance.md).
    > - Od verze Configuration Manager 1810 můžete určit chování pravidel nahrazení pro **aktualizace funkcí** odděleně od **aktualizací bez funkcí**.

###  <a name="languages"></a><a name="BKMK_UpdateLanguages"></a>Jazyky  

Nastavení jazyka bodu aktualizace softwaru vám umožní nakonfigurovat tyto možnosti: 
- Jazyky, pro které se mají synchronizovat souhrnné detaily (metadata aktualizací softwaru) pro aktualizace softwaru  
- Jazyky souboru aktualizace softwaru stažené pro aktualizace softwaru  

#### <a name="software-update-file"></a>Soubor aktualizace softwaru  
Nakonfigurujte jazyky pro nastavení **souboru aktualizace softwaru** ve vlastnostech bodu aktualizace softwaru. Toto nastavení poskytuje výchozí jazyky, které jsou k dispozici při stahování aktualizací softwaru v lokalitě. Pokaždé, když se stáhnou nebo nasadí aktualizace softwaru, upravte jazyky, které jsou ve výchozím nastavení vybrané. Během procesu stahování se budou soubory aktualizací softwaru pro nakonfigurované jazyky stahovat do zdrojového umístění balíčku nasazení, pokud jsou k dispozici ve vybraném jazyce. V dalším kroku se zkopírují do knihovny obsahu na serveru lokality. Pak jsou distribuovány do distribučních bodů nakonfigurovaných pro balíček.  

Nakonfigurujte jazykové nastavení souboru aktualizace softwaru s jazyky, které se nejčastěji používají ve vašem prostředí. Například klienti v lokalitě používají převážně angličtinu a japonštinu pro Windows nebo aplikace. V lokalitě se používá několik dalších jazyků. Při stahování nebo nasazování aktualizace softwaru zaškrtněte ve sloupci **soubor aktualizace softwaru** možnost pouze angličtina a japonština. Tato akce umožňuje použít výchozí nastavení na stránce **Výběr jazyka** Průvodce nasazením a stažením. Tato akce také zabrání stažení nepotřebných souborů aktualizací. Toto nastavení nakonfigurujte u každého bodu aktualizace softwaru v hierarchii Configuration Manager.  



#### <a name="summary-details"></a>Souhrnné detaily  
Během procesu synchronizace se aktualizují informace o souhrnných detailech (metadatech aktualizací softwaru) pro aktualizace softwaru ve vybraných jazycích. Metadata obsahují informace o aktualizaci softwaru, například:
- Název
- Popis
- Produkty, které podporuje tato aktualizace
- Klasifikace aktualizací
- ID článku
- Adresa URL pro stažení
- Pravidla použitelnosti

Nastavení souhrnných podrobností konfigurujte pouze v lokalitě nejvyšší úrovně. Souhrnné podrobnosti nejsou konfigurovány v bodu aktualizace softwaru v podřízených lokalitách, protože metadata aktualizací softwaru se replikují z lokality centrální správy pomocí replikace na základě souborů. Když vybíráte jazyky souhrnných detailů, vybírejte pouze jazyky, které potřebujete ve svém prostředí. Čím více jazyků vyberete, tím déle bude trvat synchronizace metadat aktualizací softwaru. Configuration Manager zobrazuje metadata aktualizací softwaru v národním prostředí operačního systému, ve kterém se spouští konzola nástroje Configuration Manager. Pokud lokalizované vlastnosti pro aktualizace softwaru nejsou k dispozici v národním prostředí tohoto operačního systému, zobrazí se informace o aktualizacích softwaru v angličtině.  

> [!IMPORTANT]  
>  Vyberte všechny jazyky souhrnných detailů, které potřebujete. Když se bod aktualizace softwaru v lokalitě nejvyšší úrovně synchronizuje se zdrojem synchronizace, vybrané jazyky souhrnných detailů určí metadata aktualizací softwaru, která načte. Pokud upravíte jazyky souhrnných detailů poté, co synchronizace proběhla alespoň jednou, načte metadata aktualizací softwaru pro upravené jazyky souhrnných detailů pouze pro nové nebo aktualizované aktualizace softwaru. Aktualizace softwaru, které již byly synchronizovány, nebudou aktualizovány novými metadaty pro upravené jazyky, pokud nedošlo ke změně aktualizace softwaru ve zdroji synchronizace.


###  <a name="maximum-run-time"></a><a name="bkmk_maxruntime"></a>Maximální doba běhu
<!--3734426-->
*(Představené ve verzi 1906)*

Počínaje verzí 1906 můžete zadat maximální dobu, po kterou musí být instalace aktualizace softwaru dokončena. Můžete zadat maximální dobu běhu pro následující:

- **Maximální doba běhu pro aktualizace funkcí Windows (minuty)**
  - **Aktualizace funkcí** – aktualizace, která je v jedné z těchto tří klasifikací:
    - Programů
    - Kumulativní aktualizace
    - Aktualizace Service Pack

- **Maximální doba běhu pro aktualizace Office 365 a aktualizace bez funkcí pro Windows (minuty)**
  - **Aktualizace bez funkcí** – aktualizace, která není upgradem funkce a jejíž produkt je uvedená jako jedna z následujících:
    - Windows 10 (všechny verze)
    - Windows Server 2012
    - Windows Server 2012 R2
    - Windows Server 2016
    - Windows Server 2019
    - Office 365

- Tato nastavení mění jenom maximální dobu běhu pro nové aktualizace, které jsou synchronizované z Microsoft Update. Nemění dobu běhu pro existující funkce nebo aktualizace bez funkcí.
- Pomocí tohoto nastavení nelze konfigurovat všechny ostatní produkty a klasifikace. Pokud potřebujete změnit maximální dobu běhu některé z těchto aktualizací, [nakonfigurujte nastavení aktualizace softwaru](../get-started/manage-settings-for-software-updates.md#BKMK_SoftwareUpdatesSettings)

> [!NOTE]
> Ve verzi 1906 není maximální doba běhu k dispozici při instalaci bodu aktualizace softwaru nejvyšší úrovně. Po instalaci upravte maximální dobu běhu v bodu aktualizace softwaru nejvyšší úrovně.

##  <a name="plan-for-a-software-updates-maintenance-window"></a><a name="BKMK_MaintenanceWindow"></a>Plán pro okno údržby aktualizací softwaru  

Přidejte časové období údržby určené pro instalaci aktualizací softwaru. Tato akce vám umožní nakonfigurovat obecné okno údržby a jiné časové období údržby pro aktualizace softwaru. Při konfiguraci okna obecné údržby a okna údržby aktualizací softwaru budou klienti instalovat aktualizace softwaru pouze během okna údržby aktualizací softwaru. 

Počínaje verzí 1810 Configuration Manager můžete toto chování změnit a nechat instalovat aktualizace softwaru během obecného okna údržby. Další informace o tomto nastavení klienta najdete v tématu [nastavení klienta aktualizace softwaru](../../core/clients/deploy/about-client-settings.md#bkmk_SUMMaint).

Další informace o časových obdobích údržby najdete v tématu [použití časových období](../../core/clients/manage/collections/use-maintenance-windows.md)údržby.  


##  <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a><a name="BKMK_RestartOptions"></a> Možnosti restartování klientů s Windows 10 po instalaci aktualizací softwaru

Když je aktualizace softwaru, která vyžaduje restart, nasazená a nainstalovaná pomocí Configuration Manager, klient naplánuje nedokončené restartování a zobrazí dialogové okno pro restartování.

Když je u Configuration Manager aktualizace softwaru čeká na restartování, možnost **aktualizace a restartování** a **aktualizace a vypnutí** je k dispozici na počítačích s Windows 10 v možnostech napájení systému Windows. Po použití jedné z těchto možností se dialogové okno pro restartování nezobrazí po restartování počítače. V některých případech může operační systém odebrat nedokončené možnosti restartování. K tomu může dojít, pokud je povolená funkce rychlého spuštění ve Windows 10. Další informace najdete v tématu [aktualizace, které se nedají nainstalovat s rychlým spuštěním ve Windows 10](https://support.microsoft.com/help/4011287/windows-updates-not-install-with-fast-startup).

## <a name="evaluate-software-updates-after-a-servicing-stack-update"></a><a name="bkmk_ssu"></a>Vyhodnotit aktualizace softwaru po aktualizaci servisního zásobníku
<!--4639943-->
Počínaje verzí 2002 Configuration Manager zjistí, zda je aktualizace cestou nadřazené (Servicing Stack) součástí instalace více aktualizací. Po zjištění cestou nadřazené se nainstalují jako první. Po instalaci cestou nadřazené se spustí cyklus vyhodnocení aktualizace softwaru, který nainstaluje zbývající aktualizace. Tato změna umožňuje instalaci závislé kumulativní aktualizace po aktualizaci zásobníku pro údržbu. Zařízení není nutné restartovat mezi instalacemi a nemusíte vytvářet další časové období údržby. SSUs se instalují jenom pro instalace, které neinicioval uživatel. Například pokud uživatel zahájí instalaci pro více aktualizací z centra softwaru, cestou nadřazené nemusí být nainstalován jako první. Instalace SSUs není k dispozici pro operační systémy Windows Server při použití Configuration Manager verze 2002. <!--7813007-->Tato funkce se přidala ve verzi Configuration Manager 2006 pro operační systémy Windows Server.



## <a name="next-steps"></a>Další kroky
Když plánujete aktualizace softwaru, přečtěte si téma [Příprava na správu aktualizací softwaru](../get-started/prepare-for-software-updates-management.md).  

Další informace o správě Windows jako služby najdete v tématu [základy Configuration Manager jako služba a Windows jako služba](../../core/understand/configuration-manager-and-windows-as-service.md).
