---
title: Zabezpečení a ochrana osobních údajů pro aplikace
titleSuffix: Configuration Manager
description: Doprovodné materiály a doporučení pro zabezpečení a ochranu osobních údajů při správě aplikací v Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f7085b7ee6f0f723c9bcf9d10cb85b03f990a44
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709954"
---
# <a name="security-and-privacy-for-application-management-in-configuration-manager"></a>Zabezpečení a ochrana osobních údajů pro správu aplikací v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

## <a name="security-guidance-for-application-management"></a>Pokyny k zabezpečení pro správu aplikací  

### <a name="use-the-software-center-without-the-application-catalog"></a>Použití centra softwaru bez katalogu aplikací

<!--1358309-->

Uživatelské prostředí programu Silverlight v katalogu aplikací není v aktuální větvi verze 1806 podporováno. Tato konfigurace pomáhá snižovat serverovou infrastrukturu potřebnou k doručování aplikací uživatelům.

Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací. Podpora končí pro role katalogu aplikací s verzí 1910. Omezením serverové infrastruktury dojde také k omezení prostoru pro útoky.

K zajištění konzistentního a zabezpečeného aplikačního prostředí pro internetové klienty použijte Azure Active Directory a bránu pro správu cloudu.

Další informace najdete v tématu [Konfigurace centra softwaru](plan-for-software-center.md#bkmk_userex).

### <a name="use-https-with-the-application-catalog"></a>Použití protokolu HTTPS s katalogem aplikací

> [!Important]  
> Podpora končí pro role katalogu aplikací s verzí 1910. Další informace najdete v tématu [Odebrání katalogu aplikací](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Nakonfigurujte bod webu Katalog aplikací a bod webové služby Katalog aplikací, aby přijímaly připojení HTTPS. V této konfiguraci je server ověřený uživatelům. Přenesená data jsou chráněna před manipulací a prohlížením.

Pomůžete zabránit útokům na sociální inženýrství tím, že uživatelům připojovat se pouze k důvěryhodným webům. Informujte uživatele o rizicích škodlivých webů.

Pokud nepoužíváte protokol HTTPS, nepoužívejte možnosti konfigurace značky. Tato nastavení zobrazují název vaší organizace v katalogu aplikací jako ověření identity.  


### <a name="use-role-separation"></a>Použití oddělování rolí

> [!Important]  
> Podpora končí pro role katalogu aplikací s verzí 1910. Další informace najdete v tématu [Odebrání katalogu aplikací](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Nainstalujte bod webu Katalog aplikací a bod webové služby Katalog aplikací na samostatné servery. Pokud dojde k ohrožení bezpečnosti bodu webu, je oddělení od bodu webové služby. Tento návrh pomáhá chránit Configuration Manager klienty a infrastrukturu. Tato konfigurace je zvláště důležitá, pokud bod webu akceptuje připojení klienta z Internetu. Způsobuje větší zranitelnost serveru vůči útokům.  

### <a name="close-browser-windows"></a>Zavřít okna prohlížeče

> [!Important]  
> Podpora končí pro role katalogu aplikací s verzí 1910. Další informace najdete v tématu [Odebrání katalogu aplikací](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Informování uživatelů, aby po dokončení používání katalogu aplikací zavřeli okno prohlížeče Pokud uživatelé procházejí na externí web ve stejném okně prohlížeče, které používali pro katalog aplikací, prohlížeč nadále používá nastavení zabezpečení, která jsou vhodná pro důvěryhodné lokality na intranetu.  

### <a name="centrally-specify-user-device-affinity"></a>Centrální určení spřažení uživatelských zařízení

Místo toho, abyste uživatelům umožnili identifikaci jejich primárního zařízení, ručně zadejte spřažení uživatelského zařízení. Nepovolujte konfiguraci na základě využití.

Neuvažujte informace shromážděné od uživatelů nebo ze zařízení, které se mají autoritativní. Pokud nasadíte software pomocí spřažení uživatelských zařízení, které neurčí důvěryhodný správce, je možné, že se software nainstaluje do počítačů a uživatelům, kteří nemají oprávnění k přijetí tohoto softwaru.  

### <a name="dont-run-deployments-from-distribution-points"></a>Nespouštět nasazení z distribučních bodů

Vždy konfigurujte nasazení pro stahování obsahu z distribučních bodů a nespouštějte ho z distribučních bodů. Když nakonfigurujete nasazení, aby stáhlo obsah z distribučního bodu a běželo místně, klient Configuration Manager po stažení obsahu ověří hodnotu hash balíčku. Klient zahodí balíček, pokud hodnota hash neodpovídá hodnotě hash v zásadě.

Pokud nakonfigurujete nasazení tak, aby běželo přímo z distribučního bodu, klient Configuration Manager neověřuje hodnotu hash balíčku. Toto chování znamená, že klient Configuration Manager může nainstalovat software, který je úmyslně poškozen.

Pokud je nutné spustit nasazení přímo z distribučních bodů, použijte pro balíčky v distribučních bodech alespoň oprávnění NTFS. K zabezpečení kanálu mezi klientem a distribučními body a mezi distribučními body a serverem lokality taky použijte protokol IPsec (Internet Protocol Security).

### <a name="dont-let-users-interact-with-elevated-processes"></a><a name="bkmk_interact"></a>Neumožnit uživatelům interakci s procesy se zvýšenými oprávněními
  
Pokud povolíte, aby se možnosti **spouštěly s právy správce** nebo se **nainstalovaly do systému**, nepovolujte uživatelům interakci s těmito aplikacemi. Když nakonfigurujete aplikaci, můžete nastavit možnost, která **uživatelům umožní zobrazit instalaci programu a pracovat s nimi**. Toto nastavení umožňuje uživatelům reagovat na jakékoli požadované výzvy v uživatelském rozhraní. Pokud také nakonfigurujete aplikaci tak, aby **běžela s právy správce**, nebo počínaje verzí 1802 **instalace pro systém**, útočník v počítači, který spouští program, by mohl použít uživatelské rozhraní pro zvýšení oprávnění na klientském počítači.

Použijte programy, které používají Instalační služba systému Windows pro nastavení a zvýšená oprávnění vázaná na uživatele pro nasazení softwaru, která vyžadují pověření správce. Instalační program musí být spuštěn v kontextu uživatele, který nemá pověření správce. Instalační služba systému Windows zvýšených oprávnění vázaných na uživatele poskytují nejbezpečnější způsob nasazení aplikací, které mají tento požadavek.

### <a name="restrict-whether-users-can-install-software-interactively"></a>Omezit, jestli můžou uživatelé interaktivně instalovat software

Nakonfigurujte nastavení klienta **oprávnění k instalaci** ve skupině **Počítačový agent** . Toto nastavení omezuje typy uživatelů, kteří mohou instalovat software v centru softwaru.

Vytvořte například vlastní nastavení klienta s položkou **Oprávnění k instalaci** nastavenou na **Pouze správci**. Použijte toto nastavení klienta pro kolekci serverů. Tato konfigurace zabraňuje uživatelům bez oprávnění správce instalovat software na tyto servery.  

### <a name="for-mobile-devices-deploy-only-applications-that-are-signed"></a>U mobilních zařízení nasazujte pouze podepsané aplikace

Nasaďte aplikace pro mobilní zařízení jenom v případě, že se jedná o kód podepsaný certifikační autoritou (CA), kterou mobilní zařízení důvěřuje.

Příklad:

- Aplikace od dodavatele, která je podepsána známou certifikační autoritou, jako je například VeriSign.  

- Interní aplikace, kterou podepisujete nezávisle na Configuration Manager pomocí vaší interní certifikační autority.  

- Interní aplikace, kterou podepisujete pomocí Configuration Manager, když vytvoříte typ aplikace a použijete podpisový certifikát.

### <a name="secure-the-location-of-the-mobile-device-application-signing-certificate"></a>Zabezpečení umístění podpisového certifikátu aplikace mobilního zařízení

Pokud podepisujete aplikace mobilních zařízení pomocí **Průvodce vytvořením aplikace** v Configuration Manager, Zabezpečte umístění souboru podpisového certifikátu a zabezpečte komunikační kanál. V zájmu ochrany proti zvýšení oprávnění a proti útokům prostředníkem uložte soubor podpisového certifikátu do zabezpečené složky.

Použijte protokol IPsec mezi následujícími počítači:

- Počítač se spuštěnou konzolou Configuration Manager
- Počítač, ve kterém je uložený soubor pro podepisování certifikátů
- Počítač, ve kterém jsou uloženy zdrojové soubory aplikace

Alternativně podepište aplikaci nezávisle na Configuration Manager a před spuštěním **Průvodce vytvořením aplikace**.

### <a name="implement-access-controls"></a>Implementovat řízení přístupu

Chcete-li chránit referenční počítače, implementujte řízení přístupu. Když nakonfigurujete metodu detekce v typu nasazení tak, že přejdete na referenční počítač, ujistěte se, že počítač není ohrožen.

### <a name="restrict-and-monitor-administrative-users"></a>Omezení a monitorování administrativních uživatelů

Omezte a monitorujte administrativní uživatele, kterým udělíte následující role zabezpečení na základě rolí správy aplikací:

- **Správce aplikace**
- **Autor aplikace**
- **Správce nasazení aplikací**

I když konfigurujete správu na základě rolí, správci, kteří vytvářejí a nasazují aplikace, mohou mít větší oprávnění než si myslíte. Například administrativní uživatelé, kteří vytvářejí nebo mění aplikaci, mohou vybrat závislé aplikace, které nejsou v jejich oboru zabezpečení.

### <a name="configure-app-v-apps-in-virtual-environments-with-the-same-trust-level"></a>Konfigurace aplikací App-V ve virtuálních prostředích se stejnou úrovní důvěryhodnosti

Když konfigurujete virtuální prostředí Microsoft Application Virtualization (App-V), vyberte aplikace, které mají stejnou úroveň důvěryhodnosti ve virtuálním prostředí. Vzhledem k tomu, že aplikace ve virtuálním prostředí App-V můžou sdílet prostředky, jako je schránka, nakonfigurujte virtuální prostředí tak, aby vybrané aplikace měly stejnou úroveň důvěryhodnosti.

Další informace najdete v tématu [Vytvoření virtuálních prostředí App-V](../deploy-use/create-app-v-virtual-environments.md).

### <a name="make-sure-macos-apps-are-from-a-trustworthy-source"></a>Ujistěte se, že aplikace macOS jsou z důvěryhodného zdroje.

Pokud nasadíte aplikace pro zařízení macOS, ujistěte se, že jsou zdrojové soubory z důvěryhodného zdroje. Nástroj CMAppUtil neověřuje podpis zdrojového balíčku. Ujistěte se, že balíček pochází ze zdroje, kterému důvěřujete. Nástroj CMAppUtil nedokáže zjistit, zda soubory nebyly manipulovány.

### <a name="secure-the-cmmac-file-for-macos-apps"></a>Zabezpečení souboru cmmac pro aplikace macOS

Pokud nasadíte aplikace pro počítače macOS, Zabezpečte umístění souboru **. cmmac** . Nástroj CMAppUtil tento soubor vygeneruje a pak ho naimportuje do Configuration Manager. Tento soubor není podepsaný nebo ověřený.

Zabezpečte komunikační kanál při importu tohoto souboru do Configuration Manager. Aby se zabránilo manipulaci s tímto souborem, uložte ho do zabezpečené složky. Použijte protokol IPsec mezi následujícími počítači:

- Počítač se spuštěnou konzolou Configuration Manager  
- Počítač, ve kterém je uložený soubor **. cmmac**  

### <a name="use-https-for-web-applications"></a>Použití protokolu HTTPS pro webové aplikace

Pokud nakonfigurujete typ nasazení webové aplikace, zabezpečte připojení pomocí protokolu HTTPS. Pokud nasadíte webovou aplikaci pomocí odkazu HTTP, a ne pomocí připojení HTTPS, zařízení by mohlo být Přesměrováno na neautorizovaný server. Data přenesená mezi zařízením a serverem by mohla být úmyslně poškozena.


## <a name="security-issues-for-application-management"></a>Problémy se zabezpečením při správě aplikací  

- Uživatelé s nízkými právy mohou kopírovat soubory z mezipaměti klienta na klientský počítač.  

     Uživatelé mohou číst mezipaměť klienta, ale nemohou do ní zapisovat. S oprávněními ke čtení může uživatel kopírovat instalační soubory aplikace z jednoho počítače na druhý.  

- Uživatelé s omezenými právy můžou měnit soubory, které zaznamenávají historii nasazení softwaru na klientském počítači.  

     Vzhledem k tomu, že informace o historii aplikace nejsou chráněné, může uživatel změnit soubory, které hlásí, jestli je aplikace nainstalovaná.  

- Balíčky sady App-V nejsou podepsány.  

     Balíčky sady App-V v Configuration Manager nepodporují podepisování. Digitální podpisy ověřují, zda je obsah z důvěryhodného zdroje a nebyl změněn během přenosu. U tohoto problému se zabezpečením nehrozí žádná zmírnění. Podle osvědčeného postupu zabezpečení Stáhněte obsah z důvěryhodného zdroje a ze zabezpečeného umístění.  

- Publikované aplikace sady App-V mohou instalovat na počítač všichni uživatelé.  

     Když je aplikace sady App-V publikovaná na počítači, všichni uživatelé, kteří se přihlásí k tomuto počítači, mohou aplikaci nainstalovat. Nemůžete omezit uživatele, kteří můžou aplikaci instalovat po publikování.  


## <a name="certificates-for-microsoft-silverlight-5-and-elevated-trust-mode-required-for-the-application-catalog"></a><a name="BKMK_CertificatesSilverlight5"></a>Certifikáty pro Microsoft Silverlight 5 a režim zvýšené důvěryhodnosti vyžadované pro katalog aplikací  

> [!Important]  
> Podpora končí pro role katalogu aplikací s verzí 1910. Další informace najdete v tématu [Odebrání katalogu aplikací](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

Aby mohli uživatelé instalovat software z katalogu aplikací, Configuration Manager klienti verze 1710 a starší vyžadují program Microsoft Silverlight 5, který se musí spustit v režimu zvýšené důvěryhodnosti. Ve výchozím nastavení se aplikace Silverlight spouští v režimu částečně zvýšené důvěryhodnosti, aby aplikace nemohly přistupovat k datům uživatele. Pokud ještě není nainstalovaná, Configuration Manager automaticky nainstaluje Microsoft Silverlight 5 na klienty. Ve výchozím nastavení Configuration Manager nastaví Počítačový agent, aby **povolil aplikacím Silverlight spouštění v režimu zvýšené důvěryhodnosti** na **Ano**. Toto nastavení umožňuje podepsaným a důvěryhodným aplikacím Silverlight požádat o režim zvýšené důvěryhodnosti.  

Když nainstalujete roli systému lokality bodu webu katalogu aplikací, klient nástroje nainstaluje také podpisový certifikát společnosti Microsoft v úložišti certifikátů důvěryhodných vydavatelů v každém Configuration Manager klientském počítači. Aplikace Silverlight podepsané tímto certifikátem běží v režimu zvýšené důvěryhodnosti, který počítače vyžadují k instalaci softwaru z katalogu aplikací. Configuration Manager tento podpisový certifikát automaticky spravuje. Pro zvýšení kontinuity služeb neodstraňujte ani Nepřesunujte tento podpisový certifikát Microsoftu.  

> [!WARNING]  
> Když je tato možnost povolená, umožňuje **aplikacím Silverlight, aby se spouštěly v režimu zvýšené důvěryhodnosti** , všechny aplikace Silverlight, které jsou podepsány certifikáty v úložišti certifikátů důvěryhodných vydavatelů, a to buď v úložišti počítače, nebo v úložišti uživatelů, spuštěné v režimu zvýšené důvěryhodnosti. Nastavení klienta nemůže povolit režim zvýšené důvěryhodnosti, konkrétně pro Configuration Manager katalogu aplikací nebo pro úložiště certifikátů důvěryhodných vydavatelů v úložišti počítače. Pokud malware přidá do úložiště důvěryhodných vydavatelů podvodný certifikát, malware, který používá svou vlastní aplikaci Silverlight, se nyní může také spustit v režimu zvýšené důvěryhodnosti.  

Pokud nastavíte možnost **Povolit aplikacím Silverlight spouštění v režimu zvýšené důvěryhodnosti** na **ne**, klienti neodstraní podpisový certifikát společnosti Microsoft.  

Další informace o důvěryhodných aplikacích v programu Silverlight naleznete v části [důvěryhodné aplikace](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/ee721083\(v=vs.95\)).  


## <a name="privacy-information-for-application-management"></a> Ochrana osobních údajů při správě aplikací  

Správa aplikací umožňuje spouštět jakékoli aplikace, programy nebo skripty na jakémkoli klientovi v hierarchii. Configuration Manager nemá žádnou kontrolu nad typy aplikací, programů nebo skriptů, které spouštíte, nebo typu informací, které odesílá. Během procesu nasazení aplikace může Configuration Manager přenášet informace, které identifikují účty zařízení a přihlašování mezi klienty a servery.  

Configuration Manager uchovává informace o stavu procesu nasazení softwaru. Informace o stavu nasazení softwaru nejsou během přenosu šifrovány, pokud klient nekomunikuje pomocí protokolu HTTPS. Informace o stavu nejsou v databázi uloženy v šifrovaném tvaru.  

Použití instalace aplikace Configuration Manager k vzdálené, interaktivní nebo tiché instalaci softwaru do klientských počítačů může podléhat licenčním podmínkám softwaru pro daný software. Toto použití je oddělené od licenčních podmínek k softwaru Configuration Manager. Před nasazením softwaru pomocí Configuration Manager vždy přečtěte licenční podmínky softwaru a souhlasím s nimi.  

Configuration Manager shromažďuje data o využití a diagnostiku aplikací, které společnost Microsoft používá ke zlepšení budoucích verzí. Další informace najdete v tématu [Diagnostika a data o využití](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).

Nasazení aplikace se ve výchozím nastavení nestane a vyžaduje několik kroků konfigurace.  

Následující funkce vám pomůžou zefektivnit nasazení softwaru:

- **Spřažení uživatelských zařízení** mapuje uživatele na zařízení. Správce Configuration Manager nasadí software pro uživatele. Klient automaticky nainstaluje software na jeden nebo více počítačů, které uživatel používá nejčastěji.  

- **Centrum softwaru** se automaticky nainstaluje na zařízení při instalaci klienta Configuration Manager. Uživatelé mění nastavení, vyhledávají a instalují software z centra softwaru.  

- **Katalog aplikací** je web, který umožňuje uživatelům požádat o instalaci softwaru.  

    > [!Important]  
    > Podpora končí pro role katalogu aplikací s verzí 1910. Další informace najdete v tématu [Odebrání katalogu aplikací](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

### <a name="user-device-affinity-privacy-information"></a><a name="bkmk_privacy-uda"></a>Informace o ochraně osobních údajů spřažení uživatelských zařízení

- Configuration Manager může přenášet informace mezi klienty a systémy lokality bodu správy. Tyto informace mohou identifikovat počítač a účet přihlášení a souhrnné využití účtů pro přihlášení.  

- Informace přenesené mezi klientem a serverem nejsou zašifrované, pokud není bod správy nakonfigurován tak, aby vyžadoval, aby klienti komunikovali pomocí protokolu HTTPS.  

- Informace o využití počítače a účtu přihlášení, které slouží k namapování uživatele na zařízení, jsou uloženy v klientských počítačích, odeslány do bodů správy a pak uloženy v databázi Configuration Manager. Zastaralé informace jsou ve výchozím nastavení z databáze odstraněny po 90 dnech. Chování při odstranění je konfigurovatelné nastavením úkolu údržby lokality **Odstranit zastaralá data o spřažení uživatelských zařízení** .  

- Configuration Manager uchovává informace o stavu spřažení uživatelských zařízení. Informace o stavu nejsou během přenosu šifrovány, pokud klienti nejsou nakonfigurováni tak, aby komunikovali s body správy pomocí protokolu HTTPS. Informace o stavu nejsou v databázi uložené v šifrovaném tvaru.  

- Informace o využití počítače a přihlášení, které se používají k vytvoření spřažení uživatele a zařízení, jsou vždycky povolené. Uživatelé a správci můžou poskytovat informace o spřažení uživatelských zařízení.  

### <a name="software-center-privacy-information"></a><a name="bkmk_privacy-userex"></a>Informace o ochraně osobních údajů centra softwaru

- Centrum softwaru umožňuje správcům Configuration Manager publikovat jakoukoli aplikaci nebo program nebo skript, aby je uživatelé mohli spustit. Configuration Manager nemá žádnou kontrolu nad typy programů nebo skriptů, které jsou publikovány v katalogu nebo typu informací, které odesílá.  

- Configuration Manager může přenášet informace mezi klienty a bodem správy. Tyto informace mohou identifikovat počítač a účty pro přihlášení. Informace přenesené mezi klientem a servery nejsou zašifrované, pokud nenastavíte bod správy, který bude vyžadovat, aby se klienti připojovali pomocí protokolu HTTPS.  

- Informace o žádosti o schválení aplikace jsou uloženy v databázi Configuration Manager. Žádosti, které jsou zrušené nebo zamítnuté a odpovídající položky historie požadavků se po uplynutí 30 dnů odstraní ve výchozím nastavení. Chování při odstranění je konfigurovatelné nastavením úkolu údržby lokality **Odstranit zastaralá data o požadavcích aplikace** . Žádosti o schválení aplikace, které jsou ve stavu schváleno a čekají na stav, se nikdy neodstraní.  

- Centrum softwaru se nainstaluje automaticky při instalaci klienta Configuration Manager do zařízení.  

### <a name="application-catalog-privacy-information"></a>Informace o ochraně osobních údajů v katalogu aplikací

> [!Important]  
> Podpora končí pro role katalogu aplikací s verzí 1910. Další informace najdete v tématu [Odebrání katalogu aplikací](plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

- Katalog aplikací není ve výchozím nastavení nainstalován. Tato instalace vyžaduje několik kroků konfigurování.  

- Katalog aplikací umožňuje správci Configuration Manager publikovat jakoukoli aplikaci nebo program nebo skript, aby je uživatelé mohli spustit. Configuration Manager nemá žádnou kontrolu nad typy programů nebo skriptů, které jsou publikovány v katalogu nebo typu informací, které odesílá.  

- Configuration Manager může přenášet informace mezi klienty a rolemi systému lokality katalogu aplikací. Tyto informace mohou identifikovat počítač a účty pro přihlášení. Informace přenesené mezi klientem a servery nejsou zašifrované, pokud tyto role systému lokality nejsou nakonfigurovány tak, aby vyžadovaly připojení klientů pomocí protokolu HTTPS.  
