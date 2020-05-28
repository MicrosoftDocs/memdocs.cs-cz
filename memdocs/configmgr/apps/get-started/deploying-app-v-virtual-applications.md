---
title: Nasazení virtuálních aplikací App-V
titleSuffix: Configuration Manager
description: V této části najdete informace, které je potřeba vzít v úvahu při vytváření a nasazování virtuálních aplikací.
ms.date: 03/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: ddcad9f2-a542-4079-83ca-007d7cb44995
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df6f550b21523e365055f6a4cdafadca7603c4bf
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906371"
---
# <a name="deploy-app-v-virtual-applications-with-configuration-manager"></a>Nasazení virtuálních aplikací App-V pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pokud ke správě virtuálních aplikací použijete Configuration Manager, získáte následující výhody:  

-   Jediná infrastruktura pro správu  

-   Funkce škálovatelnosti, nasazení a distribuce obsahu, jako jsou kolekce a spřažení uživatelských zařízení  

-   Pokročilé funkce správy aplikací  

-   Nasazení operačního systému, inventář softwaru a hardwaru, měření softwaru a funkce Asset Intelligence pro podporu virtuálních aplikací  

Další informace o tom, jak vytvářet a sekvencovat aplikace pomocí Microsoft Application Virtualization (App-V), najdete v [dokumentaci k Application Virtualization 4](https://docs.microsoft.com/microsoft-desktop-optimization-pack/appv-v4/).  

Kromě dalších Configuration Manager požadavků a postupů pro vytváření aplikací musíte při vytváření a nasazování virtuálních aplikací vzít v úvahu následující skutečnosti:

-   Chcete-li nasadit virtuální aplikace do počítačů, je nutné mít nainstalovaného klienta Configuration Manager a klienta sady App-V na počítačích. Klientská zařízení mohou zahrnovat stolní a přenosné počítače a klienty Infrastruktury virtuálních klientských počítačů (VDI). Software klienta Configuration Manager a App-V společně umožňuje doručování, vyhledávání a spouštění balíčků virtuálních aplikací. Klient Configuration Manager spravuje doručování balíčků virtuálních aplikací klientovi sady App-V. Klient sady App-V spustí virtuální aplikaci v klientovi.  

-   Chcete-li nasadit virtuální aplikaci, musíte nejprve vytvořit virtuální aplikaci pomocí nástroje App-V Application Virtualization Sequencer. Sekvencer sleduje proces instalace a nastavení pro aplikaci a zaznamenává informace, jež jsou potřeba k tomu, aby se mohla aplikace spouštět ve virtuálním prostředí. Pomocí aplikace Sequencer můžete také nastavit, které soubory a konfigurace se použijí pro všechny uživatele a které konfigurace mohou uživatelé přizpůsobit.  

-   Při sekvencování aplikace musíte uložit balíček do umístění, ke kterému má přístup Configuration Manager. Poté můžete vytvořit nasazení aplikace, které obsahuje tuto virtuální aplikaci.  

-   Configuration Manager nepodporuje použití sdílené funkce mezipaměti jen pro čtení sady App-V 4,6.  

-   Configuration Manager podporuje funkci úložiště sdíleného obsahu v App-V 5.  

-   Když vytvoříte typ nasazení pro virtuální aplikaci, Configuration Manager vytvoří typ nasazení pomocí obsahu souboru manifestu aplikace. Jedná se o soubor XML, který obsahuje informace o virtuální aplikaci. Kromě toho Configuration Manager vytvoří požadavky na typ nasazení na základě obsahu souboru. OSD sady App-V, který obsahuje informace o podporovaných operačních systémech pro virtuální aplikaci.  

-   Aby bylo možné nasadit virtuální aplikace v Configuration Manager, musí mít klientské počítače minimálně sadu App-V 4,6 SP1 nebo novější verzi nainstalovaného klienta.  

-   Než budete moct úspěšně nasadit virtuální aplikace, aktualizujte klienta sady App-V s nejnovější opravou hotfix. Další informace najdete v tématu [aktuální seznam verzí sady App-v 4,5 a verze souboru sady App-v 4,6](https://support.microsoft.com/help/2950945/current-list-of-app-v-4-5-and-app-v-4-6-file-versions).

-   Pokud používáte skupiny připojení v App-V 5,0, můžou vaše nasazené virtuální aplikace sdílet stejný systém souborů a registr v klientských počítačích. Na rozdíl od standardních virtuální aplikací mohou tyto aplikace sdílet data mezi sebou. Skupiny připojení si navíc zachovávají uživatelská nastavení pro aplikace, které obsahují. Virtuální prostředí App-V v Configuration Manager slouží k nastavení skupin připojení na klientských počítačích. Při instalaci aplikace nebo vyhodnocování nainstalovaných aplikací klienty dochází k vytvoření nebo úpravám virtuálních prostředí v klientských počítačích. Aplikacím můžete změnit prioritu tak, aby v situaci, kdy se více aplikací pokusí změnit hodnotu v systému souborů nebo registru, měla přednost aplikace s nejvyšší prioritou. Další informace najdete v tématu [Vytvoření virtuálních prostředí App-V](../../apps/deploy-use/create-app-v-virtual-environments.md).  

##  <a name="supported-app-v-versions"></a> Podporované verze sady App-V  
 Configuration Manager podporuje následující verze sady App-V:  

-   **App-v 4,6**: Chcete-li používat virtuální aplikace v Configuration Manager, musí mít klientské počítače nainstalovaného klienta sady App-v 4,6 SP1, App-V 4,6 SP2 nebo App-v 4,6 SP3.  

     Než budete moct úspěšně nasadit virtuální aplikace, aktualizujte klienta sady App-V 4,6 o nejnovější opravu hotfix. Další informace najdete v tématu [aktuální seznam verzí sady App-v 4,5 a verze souboru sady App-v 4,6](https://support.microsoft.com/help/2950945/current-list-of-app-v-4-5-and-app-v-4-6-file-versions).  

-   Sady **App-v 5, App-v 5,0 SP1, App-v 5,0 SP2, App-v 5,0 SP3 a App-v 5,1**: pro sadu App-v 5,0 SP2 je třeba nainstalovat [hotfix Package 5](https://support.microsoft.com/help/2963211) nebo použít App-v 5,0 SP3.  
-   **App-V 5,2**: Tato verze je integrovaná do Windows 10 školství (1607 a novější), Windows 10 Enterprise (1607 a novější) a windows Server 2016.

Další informace o App-V ve Windows 10 najdete v následujících tématech:

- [Co je nového v App-V](https://docs.microsoft.com/windows/application-management/app-v/appv-about-appv)
- [Začínáme s App-V pro Windows 10](https://docs.microsoft.com/windows/application-management/app-v/appv-getting-started)
- [Upgrade na aplikaci App-V pro Windows 10 z existující instalace](https://docs.microsoft.com/windows/application-management/app-v/appv-upgrading-to-app-v-for-windows-10-from-an-existing-installation)

##  <a name="steps-to-manage-app-v-virtual-applications"></a>Kroky týkající se správy virtuálních aplikací App-V  
 Pokud chcete spravovat virtuální aplikace App-V, použijte následující postup:  

1.   **Sekvence**: sekvencování je proces převodu aplikace na virtuální aplikaci pomocí Sequencer sady App-V.

2.   **Vytvořit**: pomocí Průvodce vytvořením typu nasazení importujte sekvencované aplikace do Configuration Managerho typu nasazení, který pak můžete přidat do aplikace. Můžete také vytvořit virtuální prostředí, která umožňují více virtuálním aplikacím sdílet nastavení.

3.   **Distribuce**: distribuce je proces zpřístupnění aplikací sady App-v v Configuration Manager distribučních bodech.

4.   **Nasazení**: nasazení je proces zpřístupnění aplikace v klientských počítačích. To se označuje jako publikování a streamování v plné infrastruktuře sady App-V.  

##  <a name="configuration-manager-virtual-application-delivery-methods"></a>Metody doručení virtuálních aplikací nástroje Configuration Manager  
Configuration Manager podporuje dvě metody doručování virtuálních aplikací klientům: streamování a místní doručování (stažení a spuštění).

Když rozhodujete, kterou metodu doručení použít, porovnejte minimální požadavky na místo na disku pro doručování streamování se zaručenou dostupností aplikací App-V v místním doručování. Požadavek na víc místa na disku klienta v případě místního doručení může být vhodnější než doručování přes vysílání datového proudu, protože tak bude aplikace uživatelům dostupná vždycky a odkudkoli.  

###  <a name="streaming-delivery"></a>Doručení pomocí vysílání datového proudu
Když použijete Configuration Manager ke správě klienta sady App-V, podporuje streamování virtuálních aplikací prostřednictvím protokolu HTTP nebo HTTPS z distribučního bodu. Ve výchozím nastavení je povoleno streamování prostřednictvím protokolu HTTP nebo HTTPS a je nastavené v dialogovém okně pro vlastnosti distribučního bodu. Když nasadíte virtuální aplikaci do klientských počítačů a uživatel spustí virtuální aplikaci, klient Configuration Manager kontaktuje bod správy, aby určil, který distribuční bod se má použít. Pak je aplikace vysílána z distribučního bodu.  

Informace v této tabulce vám pomůžou rozhodnout se, jestli je pro vás nejvhodnější způsob doručení streamování.

|Výhody|Nevýhody|  
|----------------|-------------------|  
|Tato metoda používá standardní síťové protokoly k vysílání obsahu balíčku pomocí datového proudu z distribučních bodů.<br /><br /> Zástupci programů pro virtuální aplikace vyvolají připojení k distribučnímu bodu, takže doručení virtuální aplikace je na vyžádání.<br /><br /> Tato metoda funguje dobře u klientů s připojením s velkou šířkou pásma k distribučním bodům.<br /><br /> Aktualizované virtuální aplikace distribuované v rámci podniku jsou dostupné v podobě zásad přijímání pro klienty, které je informují o tom, že aktuální verze je nahrazena, takže stáhnou pouze změny z předchozí verze.<br /><br /> Přístupová oprávnění jsou definována v distribučním bodě, což zabraňuje uživatelům v přístupu k neoprávněným aplikacím nebo balíčkům.|Virtuální aplikace nejsou vysílány pomocí datového proudu, dokud uživatel poprvé nespustí aplikaci. V tomto scénáři může uživatel obdržet zástupce programů pro virtuální aplikace a poté se před prvním spuštěním virtuálních aplikací odpojit od sítě. Pokud se uživatel pokusí spustit virtuální aplikaci, zatímco je klient v režimu offline, uživatel uvidí chybu a nemůže spustit virtualizované aplikace, protože Configuration Manager distribuční bod není k dispozici pro streamování aplikace. Aplikace nebude dostupná, dokud se uživatel znovu nepřipojí k síti a nespustí aplikaci.<br /><br /> Pokud se tomu chcete vyhnout, můžete k doručování virtuální aplikace klientům použít metodu místního doručení nebo povolit internetovou správu klientů pro doručení přes datový proud.|  

###  <a name="local-delivery-download-and-execute"></a>Místní doručení (stažení a spuštění)  
Stažení a spuštění je nejběžnějším přístupem při použití Configuration Manager, protože tento přístup úzce napodobuje doručování dalších formátů aplikace pomocí Configuration Manager. Když použijete metodu místního doručení, klient Configuration Manager nejprve stáhne celý balíček virtuální aplikace do mezipaměti klienta Configuration Manager. Configuration Manager pak instruuje klienta sady App-V, aby aplikaci streamoval z mezipaměti Configuration Manager do mezipaměti sady App-V. Pokud nasadíte virtuální aplikaci do klientských počítačů a její obsah není v mezipaměti sady App-V, klient sady App-V streamuje obsah aplikace z Configuration Manager mezipaměti klienta nástroje do mezipaměti sady App-V a pak aplikaci spustí. Po úspěšném spuštění aplikace můžete nastavit klienta Configuration Manager, aby odstranil všechny starší verze balíčku v dalším cyklu odstranění, nebo je zachovat v Configuration Manager mezipaměti klienta. Místní zachování obsahu může využít výhod metod optimalizace doručování obsahu balíčku, jako jsou BranchCache a PeerCache.

Informace v této tabulce vám pomůžou rozhodnout se, jestli je místní doručení nejlepší metodou doručování:   

|Výhody|Nevýhody|  
|----------------|-------------------|  
|Ke stažení balíčku se použije standardní funkce distribučního bodu pomocí Služby inteligentního přenosu na pozadí (BITS).<br /><br /> Obsah balíčku virtuální aplikace je doručen místně klientovi. To znamená, že je uživatelé můžou spouštět, když jejich počítač není připojený k síti.<br /><br /> Tato metoda je vhodná pro pomalá nebo nespolehlivá síťová připojení a pro počítače, které se připojují k síti pouze občas.<br /><br /> Configuration Manager využívá funkci Remote Differential Compression (RDC) k posílání klientům pouze bajty v souborech, které se změnily při aktualizaci obsahu balíčku virtuální aplikace. Klient Configuration Manager pomocí algoritmu RDC vytvoří novou verzi balíčku virtuální aplikace na základě aktuální verze balíčku a jakýchkoli změn odeslaných klientovi.<br /><br /> Tato metoda zajistí odolnost aplikace pro mobilní uživatele nebo odpojené uživatele. Správci se můžou rozhodnout zachovat balíček v mezipaměti Configuration Manager po doručení, pokud byla virtuální aplikace nasazená s instalační akcí. Balíček v mezipaměti klienta Configuration Manager slouží jako místní spolehlivý zdroj streamování pro klienta sady App-V pro vyžádání balíčku do mezipaměti.|V klientovi je vyžadováno místo na disku, které se rovná až dvojnásobku velikosti balíčku virtuální aplikace, když je virtuální aplikace trvale uložena v Configuration Manager cache.|  

###  <a name="deployment-from-an-image"></a>Nasazení z Image

Virtuální aplikace můžete také předinstalovat v počítači a poté vytvořit bitovou kopii daného počítače pro účely nasazení do jiných počítačů. Pokud byl však balíček virtuální aplikace vytvořen v jiné lokalitě, Binární rozdílová replikace nebude použita ke stažení aktualizací aplikace. Tato možnost může být užitečná v infrastruktuře virtuálních klientských počítačů, pokud požadujete okamžitou dostupnost aplikací místo stažení aplikací po přihlášení uživatele.    

##  <a name="migrating-from-an-app-v-infrastructure-to-a-configuration-manager-and-app-v-infrastructure"></a> Migrace z infrastruktury sady App-V do infrastruktury nástroje Configuration Manager a sady App-V  
Následující tabulka vám může při plánování migrace z existující infrastruktury sady App-V do správy virtuálních aplikací pomocí Configuration Manager.  

|Krok|Další informace|  
|----------|----------------------|  
|Projděte si aktuální virtuální aplikace a vyberte aplikace, které chcete migrovat do infrastruktury Configuration Manager.|Žádné další informace.|  
|Vyhodnoťte uživatele a zařízení, do kterých budou virtuální aplikace nasazeny.|Vytvořte kolekce Configuration Manager pro seskupení uživatelů a zařízení, do kterých chcete nasadit virtuální aplikace. Viz [Úvod do kolekcí](../../core/clients/manage/collections/introduction-to-collections.md).|  
|Migrujte skupiny připojení sady App-V 5 na Configuration Manager virtuální prostředí.|V tomto tématu se podívejte na část [migrace skupin připojení sady App-V 5 na Configuration Manager Virtual Environment](deploying-app-v-virtual-applications.md#migrating-app-v-5-connection-groups-to-configuration-manager-virtual-environments) .|  
|Prozkoumejte, abyste zjistili, jestli některé z vašich virtuálních aplikací existují jako úplné aplikace v infrastruktuře Configuration Manager.|Pro snadnější správu můžete přidat virtuální aplikaci do existující úplné aplikace jako nový typ nasazení. Viz téma [Create Applications](../../apps/deploy-use/create-applications.md).|  
|Vytvořte aplikace, čímž nahradíte existující balíčky sady App-V.|Viz [Úvod do správy aplikací](../understand/introduction-to-application-management.md) a [vytváření aplikací](../../apps/deploy-use/create-applications.md).|  
|Configuration Manager začne spravovat virtuální aplikace na klientovi po prvním nasazení virtuální aplikace. Potom Configuration Manager nutné spravovat všechny aplikace sady App-V v počítači.|Žádné další informace.|  
|Proveďte distribuci obsahu do příslušných distribučních bodů, čímž umožníte místní doručení aplikací.|Viz [Správa obsahu a infrastruktury obsahu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|Nasaďte aplikaci do Configuration Manager klientů.<br /><br /> Pokud byla aplikace sady App-V vytvořena pomocí dřívější verze aplikace Sequencer, která nevytváří soubor XML manifestu, můžete ji otevřít a uložit v novější verzi aplikace Sequencer a vytvořit tak soubor. Tento soubor je vyžadován pro nasazení virtuálních aplikací pomocí Configuration Manager.<br /><br /> App-V podporuje balíčky virtuálních aplikací, které jsou vytvořené pomocí verzí aplikace Sequencer SoftGrid 4,1 SP1 nebo 4,2.<br /><br /> Pokud byly aplikace předtím nainstalovány místně, je nutné je před nasazením virtuální verze aplikace odinstalovat.|Viz [nasazení aplikací](../../apps/deploy-use/deploy-applications.md).|  
|Configuration Manager již nepodporuje používání balíčků a programů, které obsahují virtuální aplikace. Když migrujete z Configuration Manager 2007 na Configuration Manager aktuální větev, Configuration Manager převede tyto balíčky na aplikace.<br /><br /> Inzerce Configuration Manager 2007 se převedou na následující typy nasazení:<br /><br /> – Migrace balíčků App-V bez inzerce: jeden typ nasazení, který používá výchozí nastavení typu nasazení.<br /><br /> – Migrace balíčků App-V s jednou reklamou: jeden typ nasazení, který používá stejné nastavení jako <br />                Inzerce Configuration Manager 2007.<br /><br /> – Migrace balíčků App-V s více oznámeními: typ nasazení pro každý <br />                Oznámení Configuration Manager 2007, které používá nastavení pro tuto reklamu.|Přečtěte si téma [Plánování migrace objektů Configuration Manager aktuální větve](../../core/migration/planning-for-the-migration-of-objects.md).|  

##  <a name="migrating-app-v-5-connection-groups-to-configuration-manager-virtual-environments"></a>Migrating App-V 5 connection groups to Configuration Manager virtual environments  
Virtuální prostředí App-V v Configuration Manager umožňují virtuálním aplikacím, které jste nasadili, sdílet stejný systém souborů a registr v klientských počítačích. To znamená, že na rozdíl od standardních virtuálních aplikací mohou tyto aplikace mezi sebou sdílet data. Při instalaci aplikace nebo vyhodnocování nainstalovaných aplikací klienty dochází k vytvoření nebo úpravám virtuálních prostředí v klientských počítačích. Virtuální prostředí jsou podobná skupinám připojení v samostatné aplikaci App-V 5.  

Při migraci skupin připojení ze samostatné sady App-V 5 do Configuration Managerho virtuálního prostředí je nutné zajistit, aby Configuration Manager správně spravují skupiny připojení, které již existují v klientských počítačích a aby bylo zachováno prostředí uživatele v rámci těchto skupin připojení.  

Převod skupin připojení sady App-V 5 na Configuration Manager virtuální prostředí:  

1.  Vytváření aplikací Configuration Manager pro všechny aplikace, které existovaly v App-V.  

2.  Nasaďte aplikace uživatelům nebo do zařízení s účelem nasazení **Požadováno**. Nasazení uživatelům musí být nasazeno pro stejné uživatele, kteří aplikaci použili v App-V. Nasazení do počítačů musí být nasazeno do stejných počítačů, které obsahovaly aplikaci v App-V.  

3.  Po dokončení nasazení vytvořte virtuální prostředí odpovídající skupinám připojení, které jsou publikovány v samostatné aplikaci App-V. Virtuální prostředí musí mít stejné balíčky (konkrétně typy nasazení sady App-V 5) ve stejném pořadí.  

Informace o tom, jak vytvořit virtuální prostředí App-V, najdete v tématu [Vytvoření virtuálních prostředí App-v](../../apps/deploy-use/create-app-v-virtual-environments.md).  

Případně můžete všechny skupiny připojení odstranit z klienta sady App-V, než začnete nasazovat aplikace s Configuration Manager. Všechna nastavení, která si uživatelé mohli uložit ve skupinách připojení App-V, se ztratí.  

##  <a name="dynamic-suite-composition-in-app-v-46"></a>Funkce Dynamic Suite Composition v sadě App-V 4.6  
Dynamické složení sady je funkce, která umožňuje definovat jeden balíček virtuální aplikace jako se závislostí na jiném balíčku virtuální aplikace. Když je aplikace spuštěna, na klientech sady App-V je umístěn primární balíček a závislý balíček ve stejném virtuálním prostředí pro aplikace.  

Pro použití této funkce se Configuration Manager musí být nasazeny a registrovány oba balíčky v klientovi sady App-V. Chcete-li zajistit, aby byl obsah závislého balíčku hostován místně na klientském počítači, nastavte nasazení aplikace pro místní doručování (stažení a spuštění).  

Další informace o funkci App-V Dynamic Suite Composition najdete v dokumentaci k App-V.  

##  <a name="converting-app-v-46-applications-to-app-v-5-applications"></a>Převod aplikací sady App-V 4.6 na aplikace sady App-V 5  
Formát balíčku aplikace se mezi verzemi sady App-V 4.6 a App-V 5 změnil. Aplikace, které mají stanovené pořadí pomocí sady App-V 4.6, již podporovány nejsou. Sada App-V 5 ale obsahuje nástroj pro převádění balíčků, který můžete použít k převodu aplikací. Další informace najdete v tématu [Postup převodu balíčku vytvořeného v předchozí verzi sady App-V](https://docs.microsoft.com/microsoft-desktop-optimization-pack/appv-v5/how-to-convert-a-package-created-in-a-previous-version-of-app-v).  

Při převodu aplikací sady App-V 4.6 na aplikace sady App-V 5 postupujte podle následujících kroků:  

1.  Převeďte nebo znovu sesekvencte balíčky sady App-V 4,6 do formátu sady App-V 5.  

2.  Nasaďte klienta sady App-V 5 do počítačů vaší hierarchie.  

3.  Vytvořte nové aplikace obsahující typy nasazení vašich aplikací App-V 5 a vytvořte pravidla nahrazování pro nahrazení aplikací sady App-V 4.6.  

4.  Podle potřeby vytvořte virtuální prostředí.  

5.  Nasaďte aplikace sady App-V 5 do počítačů.  

##  <a name="user-and-deployment-configuration-files"></a> Uživatelské soubory a soubory konfigurace nasazení  
Uživatel a konfigurační soubory nasazení mají nastavení, které řídí chování aplikace. Tyto soubory můžete použít ke změně nastavení aplikace bez změny pořadí aplikace.  

Typická aplikace sady App-V 5 může obsahovat následující soubory:  

-   Soubor balíčku aplikace (. AppV)  

-   Konfigurační soubor uživatele  

-   Konfigurační soubor nasazení  

Konfigurační soubor uživatele obsahuje nastavení, která se vztahují pouze na přihlášeného uživatele. Můžete například upravit konfigurační soubory a změnit informace o zástupci aplikace, který bude nasazen uživatelům. Můžete také vytvořit aplikaci Configuration Manager s více typy nasazení. Každý typ nasazení může obsahovat odlišný konfigurační soubor uživatele a používat pravidla požadavků k zajištění toho, že jsou tyto položky nainstalovány pro příslušné uživatele.  

Konfigurační soubor nasazení obsahuje nastavení, která platí pro počítač, například nastavení registru. Soubor může mít také uživatelská nastavení, která se používají pro všechny uživatele.  

Chcete-li nasadit virtuální aplikace sady App-V 5 s Configuration Manager, všechny tři soubory musí být při vytvoření typu nasazení sady App-V 5 přítomny ve stejné složce. Pokud se ve složce nachází několik souborů, Configuration Manager použije nejnovější.  

Další informace najdete v tématu [o dynamické konfiguraci sady App-V 5,0](https://docs.microsoft.com/microsoft-desktop-optimization-pack/appv-v5/about-app-v-50-dynamic-configuration).  

##  <a name="app-v-local-interaction"></a> Místní interakce sady App-V  
V některých scénářích nasazení aplikací se aplikace instalují místně na klientských počítačích a jiné aplikace se nasazují na stejný klientský počítač jako virtuální aplikace. Ve výchozím nastavení nemohou aplikace nainstalované lokálně vidět virtualizované aplikace přímo nebo s nimi komunikovat. Toto je zamýšlené chování izolace aplikace, které poskytuje App-V. Místní interakce je funkce klienta sady App-V, kterou můžete povolit pro každou aplikaci, aby umožňovala zobrazení a komunikaci s virtualizovanými aplikacemi lokálně nainstalované aplikace, které běží na klientském počítači. Configuration Manager a App-V plně podporují místní interakci.  

Další informace o funkci Místní interakce sady App-V najdete v dokumentaci k sadě App-V.  

##  <a name="app-v-5-shared-content-store"></a>Úložiště sdíleného obsahu sady App-V 5  
Configuration Manager podporuje funkci úložiště sdíleného obsahu sady App-V 5. Další informace najdete v tématu [Plánování pro Úložiště sdíleného obsahu (SCS) App-V 5.0](https://docs.microsoft.com/microsoft-desktop-optimization-pack/appv-v5/planning-for-the-app-v-50-sequencer-and-client-deployment#planning-for-the-app-v-50-shared-content-store-scs).  

##  <a name="monitoring-virtual-applications"></a>Monitorování virtuálních aplikací  

### <a name="virtual-application-reports"></a>Sestavy virtuálních aplikací  
K monitorování sady App-V v prostředí Configuration Manager můžete použít následující sestavy:  

|Název sestavy|Description|  
|-----------------|-----------------|  
|Výsledky virtuálního prostředí sady App-V|Zobrazuje informace o vybraném virtuálním prostředí, které je v určeném stavu pro vybranou kolekci (pouze sada App-V 5).|  
|Výsledky virtuálního prostředí sady App-V pro prostředek|Zobrazuje informace o vybraném virtuálním prostředí pro zadaný prostředek a všechny typy nasazení pro vybrané virtuální prostředí (jenom sady App-V 5).|  
|Stav virtuálního prostředí sady App-V|Zobrazí informace o kompatibilitě pro vybrané virtuální prostředí pro vybranou kolekci. Sloupec **zachovaná** v této sestavě zobrazuje prostředky, ve kterých již neplatí virtuální prostředí, které dříve bylo nastaveno, ale je uchováno pro zachování uživatelských nastavení v aplikacích, které se spouštějí ve virtuálním prostředí (pouze sada App-V 5).|  
|Počítače s určitou virtuální aplikací|Zobrazí shrnutí počítačů, které mají zadaného zástupce App-V, který vytvořila aplikace Application Virtualization Management Sequencer (jenom sady App-V 4,6).|  
|Počítače s určitou sadou virtuální aplikace|Zobrazí seznam počítačů, ve kterých je nainstalován zadaný balíček aplikace sady App-V (pouze sada App-V 4,6).|  
|Počítat všechny instance balíčků virtuální aplikace|Zobrazuje počet všech zjištěných balíčků aplikace App-V (jenom sady App-V 4,6).|  
|Počítat všechny instance virtuálních aplikací|Zobrazuje počet všech zjištěných aplikací sady App-V (pouze sady App-V 4,6).|  

### <a name="log-files"></a>Soubory protokolů  
Configuration Manager zaznamenává informace o nasazení virtuální aplikace do souborů protokolu. Informace o souborech protokolů, které používají virtuální aplikace a Configuration Manager Správa aplikací, najdete v tématu [soubory protokolu](../../core/plan-design/hierarchy/log-files.md).  

V případě Windows 8.1 vyhledejte v klientovi virtualizace C:\ProgramData\Microsoft\Application protokoly pro klienta sady App-V.  
