---
title: Technical Preview 1806,2
titleSuffix: Configuration Manager
description: Seznamte se s novými funkcemi dostupnými v Configuration Manager Technical Preview verze 1806,2.
ms.date: 06/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3af2a69d-30e7-4dce-832d-82b7a1c082f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b7643c73d2e9dad00e926bdc3db905016c45860a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905223"
---
# <a name="capabilities-in-technical-preview-18062-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1806,2 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1806,2. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Technical Preview. 

Před instalací této aktualizace si přečtěte článek [Technical Preview](technical-preview.md) . V tomto článku se seznámíte s obecnými požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->

## <a name="known-issues-in-this-technical-preview"></a>Známé problémy v této verzi Technical Preview

### <a name="clients-dont-automatically-update"></a><a name="ki_sqlncli"></a>Klienti se neaktualizují automaticky
<!--518760-->
Při aktualizaci na verzi 1806,2 lokalita také aktualizuje SQL Native Client, což může způsobit nedokončené restartování serveru lokality. Tato prodleva způsobí, že se některé soubory neaktualizují, což má dopad na automatický upgrade klienta.

#### <a name="workarounds"></a>Alternativní řešení
Vyhněte se tomuto problému ručním upgradem SQL Native Client *před aktualizací* Configuration Manager na verzi 1806,2. Další informace najdete v tématu [nejnovější aktualizace údržby pro nativního klienta SQL Server 2012](https://www.microsoft.com/download/details.aspx?id=50402).

Pokud jste web již aktualizovali, automatický upgrade klienta a nabízená instalace klienta nebudou fungovat. Aby bylo možné plně testovat většinu nových funkcí, je nutné aktualizovat klienty. Aktualizujte klienty Technical Preview ručně pomocí následujícího postupu:  

1. Vyhledejte zdrojové soubory klienta ve Configuration Manager složce **CMUClient** instalačního adresáře na serveru lokality. Například `C:\Program Files\Configuration Manager\CMUClient`.  

2. Zkopírujte celou složku CMUClient do klientského zařízení. Například `C:\Temp\CMUClient`.  

    Toto umístění může být sdílená síťová složka, která je přístupná z klientů.  

3. Z příkazového řádku se zvýšenými oprávněními spusťte následující příkazový řádek:`C:\Temp\CMUClient\ccmsetup.exe /source:C:\Temp\CMUClient`  

Pokud instalujete nového klienta v lokalitě verze Technical Preview 1806,2, použijte stejný postup. 

> [!Important]  
> `/MP`V tomto scénáři nepoužívejte parametr příkazového řádku. Tento parametr má přednost před `/source` a způsobuje, že služba CCMSetup stahuje obsah klienta z bodu správy nebo distribučního bodu.
> 
> Vlastnosti příkazového řádku, jako je například SMSSITECODE nebo CCMLOGLEVEL, jsou v pořádku, ale neměly by být nutné při upgradu stávajícího klienta. 


### <a name="version-18062-shows-version-1806-in-about-configuration-manager"></a><a name="ki_version"></a>Verze 1806,2 ukazuje verze 1806 v o Configuration Manager
<!--518148-->
Pokud po upgradu na verzi Technical Preview 1806,2 Otevřete okno **o Configuration Manager** v levém horním rohu konzoly, pořád se zobrazuje **verze 1806**. 

#### <a name="workaround"></a>Alternativní řešení
Pomocí vlastnosti **verze lokality** určete rozdíl mezi 1806 a 1806,2:

| Verze lokality  | Verze
|---------|---------|
| 5,0.**8672**. 1000 | 1806 |
| 5,0.**8685**. 1000 | 1806,2 |
 


</br>

**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  


## <a name="improvements-to-phased-deployments"></a><a name="bkmk_pod"></a>Vylepšení postupného nasazení

Tato verze zahrnuje následující vylepšení [postupného nasazení](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md):
- [Stav postupného nasazení](#bkmk_pod-monitor)
- [Dvoufázové nasazení aplikací](#bkmk_pod-app)
- [Postupné zavedení při dvoufázovém nasazení](#bkmk_pod-throttle)


### <a name="phased-deployment-status"></a><a name="bkmk_pod-monitor"></a>Stav postupného nasazení
<!--1358577-->
Postupná nasazení nyní mají nativní prostředí monitorování. V uzlu **nasazení** v pracovním prostoru **monitorování** vyberte postupné nasazení a pak na pásu karet klikněte na **Stav postupného nasazení** .

![Řídicí panel stavu postupného nasazení zobrazující stav dvou fází](media/1358577-phased-deployment-status.png)

Tento řídicí panel zobrazuje pro každou fázi nasazení následující informace:  

- **Celkem zařízení**: kolik zařízení cílí touto fází.  

- **Status (stav**): aktuální stav této fáze. Každá fáze může být v jednom z následujících stavů:  

    - **Nasazení vytvořeno**: dvoufázové nasazení vytvořilo nasazení softwaru do kolekce pro tuto fázi. Klienti jsou aktivně zacíleni na tento software.  

    - **Čekání**: předchozí fáze ještě nedosáhla kritérií úspěchu, aby nasazení pokračovalo v této fázi.  

    - **Pozastaveno**: Správce pozastavil nasazení.  

- **Průběh**: barevně kódované stavy nasazení od klientů. Například: úspěch, probíhá, chyba, požadavky nejsou splněny a neznámé. 


#### <a name="known-issue"></a>Známý problém
Řídicí panel stavu postupného nasazení může zobrazit několik řádků pro stejnou fázi.<!--518510-->


### <a name="phased-deployment-of-applications"></a><a name="bkmk_pod-app"></a>Dvoufázové nasazení aplikací
<!--1358147-->
Vytvoření postupného nasazení pro aplikace Postupné nasazení vám umožní orchestrovat koordinované, sekvenční zavedení softwaru na základě přizpůsobitelných kritérií a skupin.

V konzole Configuration Manager klikněte na **Knihovna softwaru**, rozbalte položku **Správa aplikací**a vyberte možnost **aplikace**. Vyberte aplikaci a potom na pásu karet klikněte na **vytvořit dvoufázové nasazení** . 

Chování při dvoufázovém nasazení aplikace je stejné jako u pořadí úloh. Další informace najdete v tématu [vytvoření postupného nasazení pro pořadí úkolů](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md).

#### <a name="prerequisite"></a>Požadavek
Před vytvořením postupného nasazení distribuujte obsah aplikace do distribučního bodu.<!--518293-->

#### <a name="known-issue"></a>Známý problém
Nemůžete ručně vytvořit fáze pro aplikaci. Průvodce automaticky vytvoří dvě fáze pro nasazení aplikací.


### <a name="gradual-rollout-during-phased-deployments"></a><a name="bkmk_pod-throttle"></a>Postupné zavedení při dvoufázovém nasazení
<!--1358578-->
Během dvoufázového nasazení teď může probíhat v každé fázi postupně. Toto chování pomáhá zmírnit riziko problémů s nasazením a snižuje zatížení sítě způsobené distribucí obsahu na klienty. V lokalitě může být software postupně dostupný v závislosti na konfiguraci pro každou fázi. Každý klient ve fázi má konečný termín relativně k době, kdy byl software zpřístupněn. Časový interval mezi dostupným časem a konečným termínem je stejný pro všechny klienty ve fázi. 

Když vytvoříte postupné nasazení a ručně nakonfigurujete fázi, na stránce **nastavení fáze** Průvodce přidáním fáze nebo na stránce **Nastavení** v Průvodci vytvořením fáze nasazení nastavte možnost: **postupně zpřístupnit tento software v tomto časovém intervalu (ve dnech)**. Výchozí hodnota tohoto nastavení je **0**, takže ve výchozím nastavení není nasazení omezené.

> [!Note]  
> Tato možnost je v tuto chvíli dostupná jenom pro fáze nasazení pořadí úkolů.  



## <a name="support-for-new-windows-app-package-formats"></a><a name="bkmk_msix"></a>Podpora pro nové formáty balíčků aplikací pro Windows
<!--1357427-->
Configuration Manager teď podporuje nasazení nového balíčku aplikace pro Windows 10 (. msix) a formátů sady prostředků aplikace (. msixbundle). Nejnovější buildy [Windows Insider ve verzi Preview](https://insider.windows.com/) aktuálně podporují tyto nové formáty.

Přehled MSIX najdete v tématu o tom, jak se [podíváte na MSIX](https://docs.microsoft.com/archive/blogs/sgern/a-closer-look-at-msix).

Informace o tom, jak vytvořit novou aplikaci MSIX, najdete [v článku podpora MSIX představená v programu Insider build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).

### <a name="prerequisites"></a>Požadavky
- Klient s Windows 10, na kterém běží aspoň Windows Insider Preview build 17682
- Balíček aplikace systému Windows ve formátu MSIX

### <a name="try-it-out"></a>Určitě to udělejte!
Zkuste úkoly dokončit. Potom vám pošleme [názor](capabilities-in-technical-preview-1804.md#bkmk_feedback) , abychom věděli, jak pracovali.

1. V konzole Configuration Manager [vytvořte aplikaci](../../apps/deploy-use/create-applications.md). 
2. Vyberte **typ** instalačního souboru aplikace jako **balíček aplikace systému Windows ( \* . appx, \* . appxbundle, \* . msix, \* . msixbundle)**.
3. [Nasaďte aplikaci](../../apps/deploy-use/deploy-applications.md) do klienta, na kterém běží nejnovější Build Windows Insider Preview.



## <a name="improvement-to-client-push-security"></a><a name="bkmk_client-push"></a>Zlepšení zabezpečení nabízených oznámení klientů
<!--1358204-->
Při použití metody [push klienta](../clients/deploy/plan/client-installation-methods.md#client-push-installation) pro instalaci klienta Configuration Manager Server lokality vytvoří vzdálené připojení ke klientovi, aby mohl spustit instalaci. Od této verze může lokalita vyžadovat vzájemné ověřování protokolem Kerberos tím, že před vytvořením připojení nepovolí použití protokolu NTLM pro ověřování. Toto vylepšení pomáhá zabezpečit komunikaci mezi serverem a klientem. 

V závislosti na zásadách zabezpečení může vaše prostředí již upřednostňovat nebo vyžadovat protokol Kerberos přes starší ověřování NTLM. Další informace o bezpečnostních faktorech těchto ověřovacích protokolů najdete v [nastavení zásad zabezpečení systému Windows k omezení protokolu NTLM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).


### <a name="prerequisite"></a>Požadavek

Aby bylo možné tuto funkci používat, musí být klienti v důvěryhodné doménové struktuře služby Active Directory. Protokol Kerberos v systému Windows spoléhá na vzájemné ověřování služby Active Directory. 


### <a name="try-it-out"></a>Určitě to udělejte!

Zkuste úkoly dokončit. Potom vám pošleme [názor](capabilities-in-technical-preview-1804.md#bkmk_feedback) , abychom věděli, jak pracovali.

Při upgradu lokality přetrvává stávající chování. Jakmile *otevřete* vlastnosti nabízené instalace klienta, lokalita automaticky povolí kontrolu protokolu Kerberos. V případě potřeby můžete připojení použít k použití méně zabezpečeného připojení NTLM, což se nedoporučuje. 

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte možnost **lokality**. Vyberte cílový web. Na pásu karet klikněte na **nastavení instalace klienta** a vyberte **klientská nabízená instalace**.  

2. Lokalita nyní povolila kontrolu protokolu Kerberos pro nabízenou registraci klienta. Kliknutím na tlačítko **OK** zavřete toto okno.  

3. V případě potřeby v okno Vlastnosti klientské nabízené instalace na kartě **Obecné** si přečtěte možnost **Povolení použití náhradního připojení k NTLM**. Tato možnost je ve výchozím nastavení zakázána. 



## <a name="management-insights-for-proactive-maintenance"></a><a name="bkmk_insights"></a>Přehledy správy pro proaktivní údržbu
<!--1352184,et al-->
V této verzi jsou k dispozici další přehledy správy pro zdůraznění potenciálních problémů s konfigurací. Projděte si následující pravidla v nové **proaktivní** skupině pro údržbu:  

- **Nepoužité položky konfigurace**: položky konfigurace, které nejsou součástí standardních hodnot konfigurace a jsou starší než 30 dní.  

- **Nepoužívané spouštěcí bitové kopie**: spouštěcí bitové kopie neodkazují na spouštění pomocí technologie PXE nebo použití pořadí úloh.  

- **Hraniční skupiny bez přiřazených systémů lokality**: bez přiřazených systémů lokality lze skupiny hranic použít pouze pro přiřazení lokality.  

- **Skupiny hranic bez členů**: skupiny hranic nejsou použitelné pro přiřazení lokality nebo vyhledávání obsahu, pokud nemají žádné členy.  

- **Distribuční body, které neobsluhují obsah pro klienty**: distribuční body, které klientům za posledních 30 dní nesloužili obsahu. Tato data jsou založená na sestavách od klientů jejich historie stahování.  

- **Nalezené aktualizace s vypršenou platností**: aktualizace, jejichž platnost vypršela   



## <a name="transition-mobile-apps-workload-for-co-managed-devices"></a><a name="bkmk_comgmt"></a>Přechod úlohy mobilní aplikace pro spoluspravovaná zařízení
<!--1357892-->
Umožňuje spravovat mobilní aplikace pomocí Microsoft Intune a přitom dál používat Configuration Manager k nasazení desktopových aplikací pro Windows. Pokud chcete převést úlohu moderních aplikací, přejděte na stránku vlastností spolusprávy. Přesuňte posuvník z Configuration Manager na pilot nebo vše. 

Po přechodu na tuto úlohu jsou všechny dostupné aplikace nasazené z Intune dostupné v Portál společnosti. Aplikace, které nasazujete z Configuration Manager, jsou k dispozici v centru softwaru. 

Další informace najdete v následujících článcích:  

- [Spoluspráva pro zařízení s Windows 10](../../comanage/overview.md)  

- [Co je správa aplikací v Microsoft Intune?](https://docs.microsoft.com/intune/app-management)  



## <a name="boundary-group-options-for-peer-downloads"></a><a name="bkmk_bgoptions"></a>Možnosti skupiny hranic pro rovnocenné soubory ke stažení
<!--1356193-->
Skupiny hranic teď obsahují další nastavení, která vám poskytnou větší kontrolu nad distribucí obsahu ve vašem prostředí. Tato verze přidává následující možnosti:  

- **Povolit stahování ze strany partnerů v této skupině hranic**: Toto nastavení je ve výchozím nastavení povolené. Bod správy poskytuje klientům seznam umístění obsahu, která obsahují partnerské zdroje. <!--This setting also affects applying Group IDs for Delivery Optimization.518268-->  

    Existují dva běžné scénáře, ve kterých byste měli zvážit zakázání této možnosti:  

    - Máte-li skupinu hranic, která zahrnuje hranice geograficky rozptýlených umístění, jako je například síť VPN. Dva klienti můžou být ve stejné skupině hranic, protože jsou připojení prostřednictvím sítě VPN, ale v rozsáhlých různých umístěních, která jsou nevhodná pro sdílení obsahu v partnerském vztahu.  

    - Použijete-li jednu velkou skupinu hranic pro přiřazení lokality, která neodkazuje na žádné distribuční body.  

- **Během stahování po straně druhé se používají jenom partnerské uzly ve stejné podsíti**: Toto nastavení závisí na výše uvedeném. Pokud tuto možnost povolíte, bude bod správy obsahovat jenom v seznamu umístění obsahu partnerské zdroje, které jsou ve stejné podsíti jako klient.

    Běžné scénáře pro povolení této možnosti:

    - Návrh skupiny hranic pro distribuci obsahu zahrnuje jednu velkou skupinu hranic, která překrývá jiné menší skupiny hranic. Díky tomuto novému nastavení seznam zdrojů obsahu, které bod správy poskytuje klientům, zahrnuje pouze partnerské zdroje ze stejné podsítě.

    - Máte jednu velkou skupinu hranic pro všechna Odloučená pracoviště. Tuto možnost povolte a klienti sdílejí obsah v rámci podsítě jenom na vzdáleném pracovišti místo rizikového sdílení obsahu mezi umístěními.


### <a name="known-issue"></a>Známý problém
Pokud má klient s partnerským vztahem více než jednu IP adresu (IPv4, IPv6 nebo obojí), pak sdílené mezipaměti nefungují. Tato nová možnost **při stahování přes rovnocenné sítě používá jenom partnerské uzly v rámci stejné podsítě**, nemá žádný vliv, pokud má partnerský zdroj více než jednu IP adresu.<!--518661-->   



## <a name="third-party-software-updates-support-for-custom-catalogs"></a><a name="bkmk_3pupdate"></a>Podpora aktualizací softwaru třetích stran pro vlastní katalogy
<!--1358714-->
Tato verze dále prochází podporu aktualizací softwaru třetích stran v důsledku vaší [zpětné vazby](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co)na webu UserVoice. [Technical Preview verze 1806](capabilities-in-technical-preview-1806.md#bkmk-3pupdate) poskytuje podporu pro *partnerské katalogy*, které jsou registrované katalogy od dodavatelů softwaru. Katalogy, které zadáte, které nejsou registrované u Microsoftu, se nazývají *vlastní katalogy*. Přidejte vlastní katalogy v konzole Configuration Manager.  


### <a name="prerequisites"></a>Požadavky 

- Nastavte [aktualizace softwaru třetích stran](capabilities-in-technical-preview-1806.md#bkmk-3pupdate). Dokončete fázi 1: Povolte a nastavte funkci.   

- Digitálně podepsaný vlastní katalog, který obsahuje digitálně podepsané aktualizace softwaru.  

- Správce vyžaduje následující oprávnění:  

    - Lokalita: vytvořit, upravit  


### <a name="try-it-out"></a>Určitě to udělejte!

Zkuste úkoly dokončit. Potom vám pošleme [názor](capabilities-in-technical-preview-1804.md#bkmk_feedback) , abychom věděli, jak pracovali.

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** , rozbalte možnost **aktualizace softwaru**a vyberte uzel **katalogy aktualizací softwaru třetích stran** . Na pásu karet klikněte na **Přidat vlastní katalog** .  

2. Na stránce **Obecné** zadejte následující podrobnosti:  

    - **Adresa URL pro stahování**: platná adresa https vlastního katalogu.  

    - **Vydavatel**: název organizace, která publikuje katalog.  

    - **Name (název**): název katalogu, který se má zobrazit v konzole Configuration Manager.  

    - **Popis**: Popis katalogu.  

    - **Adresa URL podpory** (volitelné): platná adresa HTTPS webu, která má získat nápovědu ke katalogu.  

    - **Kontakt podpory** (volitelné): kontaktní informace, které vám pomůžou s katalogem.  

3. Dokončete průvodce. Průvodce přidá nový katalog do neodebíraného stavu.  

4. Přihlaste se k odběru vlastního katalogu pomocí existující akce **přihlášení k odběru katalogu** . Další informace najdete v části [fáze 2: přihlášení k odběru katalogu třetích stran a aktualizace pro synchronizaci](capabilities-in-technical-preview-1806.md#phase-2-subscribe-to-a-third-party-catalog-and-sync-updates).  

> [!Note]  
> Nelze přidat katalogy se stejnou adresou URL pro stažení a nelze upravit vlastnosti katalogu. Pokud zadáte nesprávné vlastnosti vlastního katalogu, odstraňte katalog, abyste ho mohli znovu přidat.  


#### <a name="unsubscribe-from-a-catalog"></a>Zrušení odběru katalogu
Pokud chcete zrušit odběr katalogu, v seznamu vyberte požadovaný katalog a na pásu karet klikněte na **zrušit odběr katalogu** . Pokud zrušíte odběr katalogu, dojde k následujícím akcím a chování: 
- Lokalita zastaví synchronizaci nových aktualizací. 
- Lokalita zablokuje přidružené certifikáty pro podepisování katalogu a aktualizaci obsahu. 
- Stávající aktualizace se neodeberou, ale možná je nebudete moct publikovat ani nasadit.

#### <a name="delete-a-custom-catalog"></a>Odstranění vlastního katalogu
Odstraňte vlastní katalogy ze stejného uzlu konzoly. Vyberte vlastní katalog ve stavu bez *odběru* a klikněte na **Odstranit vlastní katalog**. Pokud jste se už k odběru katalogu přihlásili, odhlaste se před jeho odstraněním. Nemůžete odstranit katalogy partnerů. Odstranění vlastního katalogu ho odebere ze seznamu katalogů. Tato akce neovlivní žádné aktualizace softwaru, které jste publikovali do bodu aktualizace softwaru.


### <a name="known-issue"></a>Známý problém
Akce odstranit u vlastního katalogu je šedá, takže nemůžete odstranit vlastní katalogy z konzoly. Chcete-li tento problém vyřešit, použijte nástroj **WBEMTest** na serveru lokality. Dotaz na instanci, kterou chcete odstranit, pomocí názvu nebo adresy URL pro stažení, například: `select * from SMS_ISVCatalog where DownloadURL="http://www.contoso.com/catalog.cab"` . V okně výsledek dotazu vyberte objekt a klikněte na **Odstranit**.<!--518676-->  



## <a name="improvements-to-cloud-management-features"></a><a name="bkmk_cloud"></a>Vylepšení funkcí pro správu cloudu

Tato verze zahrnuje následující vylepšení:  

- Následující funkce teď podporují používání cloudu státní správy Azure USA:<!--511980-->  

    - Zprovoznění lokality pro **správu cloudu** prostřednictvím [služeb Azure](../servers/deploy/configure/azure-services-wizard.md)  

    - Nasazení [brány pro správu cloudu pomocí Azure Resource Manager](../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)  

    - Nasazení [distribučního bodu cloudu pomocí Azure Resource Manager](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager)  

- Zákazníci používají Windows autopilot k zřizování Windows 10 na zařízeních připojených k Azure Active Directory, která jsou připojená k místní síti. Pokud chcete nainstalovat nebo upgradovat klienta Configuration Manager na těchto zařízeních, nepotřebujete teď cloudový distribuční bod nebo místní distribuční bod, aby se **klienti mohli anonymně připojit**. Místo toho povolte možnost lokalita pro **použití Configuration Manager generovaných certifikátů pro systémy lokality http**, což klientovi připojenému k doméně umožňuje komunikovat s místním distribučním bodem s POVOLENým protokolem HTTP. Další informace najdete v tématu [Vylepšená zabezpečená komunikace klientů](https://docs.microsoft.com/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications).<!--515854-->  



## <a name="new-software-updates-compliance-report"></a><a name="bkmk_report"></a>Nová sestava dodržování předpisů pro aktualizace softwaru
<!--1357775-->
Zobrazení sestav pro dodržování předpisů aktualizací softwaru obvykle zahrnuje data z klientů, kteří se nedávno nepřipojili k lokalitě. Nová sestava umožňuje filtrovat výsledky dodržování předpisů pro konkrétní skupinu aktualizací softwaru podle "zdravých" klientů. Tato sestava obsahuje realističtější stav dodržování předpisů aktivních klientů ve vašem prostředí. 
 
Sestavu zobrazíte tak, že přejdete do pracovního prostoru **monitorování** , rozbalíte **vytváření sestav**, rozbalíte **sestavy**, rozbalíte **aktualizace softwaru –** a vyberete dodržování **předpisů 9 – celkový stav a dodržování předpisů**. Zadejte **skupinu aktualizací**, **název kolekce**a stav **klienta** .

Sestava obsahuje následující části:
- **V pořádku klienti vs celkem klientů**: Tento pruhový graf porovnává "v pořádku" klienti, kteří s lokalitou komunikovali v zadaném časovém období vzhledem k celkovému počtu klientů v zadané kolekci.
- **Přehled dodržování předpisů**: Tento výsečový graf zobrazuje celkový stav dodržování předpisů pro konkrétní skupinu aktualizací softwaru na aktivních klientech v zadané kolekci.
- **Hlavní 5 nekompatibilní podle ID článku**: Tento pruhový graf zobrazuje horní pět aktualizací softwaru v zadané skupině, které nedodržují předpisy aktivních klientů v zadané kolekci.
- Dolní část sestavy je tabulka s dalšími podrobnostmi, které obsahují seznam aktualizací softwaru v zadané skupině.



## <a name="next-steps"></a>Další kroky
Informace o instalaci nebo aktualizaci větve Technical Preview najdete v tématu [Technical Preview pro Configuration Manager](technical-preview.md).    
