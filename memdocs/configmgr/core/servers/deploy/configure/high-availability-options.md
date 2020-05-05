---
title: Vysoká dostupnost
titleSuffix: Configuration Manager
description: Naučte se, jak nasadit Configuration Manager pomocí možností, které udržují vysokou úroveň dostupné služby.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cf8714aff7235736628d44238561eea82b896698
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073309"
---
# <a name="high-availability-options-for-configuration-manager"></a>Možnosti vysoké dostupnosti pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek popisuje, jak nasadit Configuration Manager pomocí možností, které udržují vysokou úroveň dostupné služby.

K dispozici jsou následující možnosti Configuration Manager podporují vysokou dostupnost:

- Nakonfigurujte samostatnou primární lokalitu s dalším serverem lokality v pasivním režimu.  

- Nakonfigurujte skupinu dostupnosti Always On SQL Server pro databázi lokality v primárních lokalitách a lokalitě centrální správy.

- Lokality podporují více instancí rolí systému lokality, které klientům poskytují důležité služby. Například body správy a distribuční body.  

- Lokality centrální správy a primární lokality podporují zálohování databáze lokality. Databáze lokality ukládá všechny konfigurace pro lokality a klienty. Lokality v hierarchii sdílejí Tato konfigurační data.  

- Integrované možnosti Site Recovery můžou snížit prostoje serveru. Tyto rozšířené možnosti zjednodušují obnovení, když máte hierarchii s lokalitou centrální správy.  

- Klienti mohou automaticky opravovat typické problémy bez zásahu správce.  

- Lokality generují výstrahy o klientech, kteří neodesílají poslední data, což upozorní správce na potenciální problémy.  

- Configuration Manager poskytuje několik předdefinovaných sestav a řídicích panelů. Použijte je k identifikaci problémů a trendů předtím, než se stanou problémy pro operace serveru nebo klienta.  

Configuration Manager obsahuje několik funkcí, které poskytují službu téměř v reálném čase. Pokud jsou tyto funkce kritické pro splnění vašich obchodních požadavků, naplánujte a nakonfigurujte své lokality a hierarchie pro zajištění vysoké dostupnosti. Příklad:  

- [Akce s klientskými oznámeními](../../../clients/manage/manage-clients.md), jako je restartování, spuštění kontroly v programu Windows Defender nebo Vzdálená plocha.  

- Zprávy založené na stavu pro monitorování funkcí, jako jsou aktualizace softwaru a Endpoint Protection.

- [Skripty](../../../../apps/deploy-use/create-deploy-scripts.md)

- [CMPivot](../../manage/cmpivot.md)

Jiné funkce Configuration Manager neposkytují službu v reálném čase. Tyto funkce zahrnují, ale nejsou omezené na nastavení klienta, inventář hardwaru a softwaru, nasazení softwaru a nastavení dodržování předpisů. Očekává, že budou fungovat s určitou latencí dat. Pro většinu scénářů, které zahrnují dočasné přerušení služby, se nedoporučuje, aby se staly kritickým problémem. Abyste minimalizovali prostoje, udrželi autonomii operací a poskytovali vysokou úroveň služby, nakonfigurujte své lokality a hierarchie s vysokou dostupností.  

Například klienti Configuration Manager obvykle pracují samostatně pomocí známých plánů a konfigurací pro operace a plány pro odeslání dat do lokality ke zpracování.  

- Pokud klienti nemohou lokalitu kontaktovat, budou data zadávána do mezipaměti, dokud nebudou moci kontaktovat lokalitu.  

- Klienti, kteří nemohou lokalitu kontaktovat, budou i nadále fungovat. Používají poslední známé plány a informace v mezipaměti, dokud nebudou moci kontaktovat lokalitu a získat nové zásady. Klient může například uchovávat dříve staženou aplikaci, kterou musí spustit nebo nainstalovat.

- Lokalita monitoruje systémy lokality a klienty pro pravidelné aktualizace stavu. Může generovat výstrahy, když se tyto součásti nepodaří zaregistrovat.  

- Předdefinované sestavy poskytují přehled o probíhajících operacích, historických operacích a aktuálních trendech. Configuration Manager také podporuje zprávy na základě stavu, které poskytují informace téměř v reálném čase pro probíhající operace.  


## <a name="high-availability-for-sites-and-hierarchies"></a><a name="bkmk_snh"></a>Vysoká dostupnost pro lokality a hierarchie  

### <a name="use-a-site-server-in-passive-mode"></a>Použití serveru lokality v pasivním režimu

Instalace dalšího serveru lokality v *pasivním* režimu pro samostatnou primární lokalitu. Server lokality v pasivním režimu je kromě stávajícího serveru lokality v *aktivním* režimu. Server lokality v pasivním režimu je k dispozici pro okamžité použití v případě potřeby. Další informace najdete v tématu [Vysoká dostupnost serveru lokality](site-server-high-availability.md).  

### <a name="use-a-remote-content-library"></a>Použít vzdálenou knihovnu obsahu

Přesuňte knihovnu obsahu webu do vzdáleného umístění, které poskytuje úložiště s vysokou dostupností. Tato funkce je požadavek pro vysokou dostupnost serveru lokality. Další informace najdete v [knihovně obsahu](../../../plan-design/hierarchy/the-content-library.md#bkmk_remote).

### <a name="centralize-content-sources"></a>Centralizace zdrojů obsahu

Veškerý obsah softwaru v Configuration Manager vyžaduje umístění zdroje balíčku v síti. Použijte centralizované úložiště s vysokou dostupností pro hostování společného zdrojového umístění balíčku pro veškerý obsah.

### <a name="use-a-sql-server-always-on-availability-group-to-host-the-site-database"></a>Pro hostování databáze lokality použijte skupinu dostupnosti Always On SQL Server.

Hostování databáze lokality v primárních lokalitách a lokalitě centrální správy na SQL Server skupiny dostupnosti Always On. Další informace najdete v tématu [SQL Server Always On pro databázi lokality s vysokou dostupností](sql-server-alwayson-for-a-highly-available-site-database.md).  

### <a name="use-a-sql-server-cluster-to-host-the-site-database"></a>Použití clusteru SQL Server k hostování databáze lokality

Použijete-li cluster SQL Server pro databázi v lokalitě centrální správy nebo v primární lokalitě, použijete podporu převzetí služeb při selhání integrovanou do SQL Server.  

Sekundární lokality nemůžou používat cluster SQL Server a nepodporují zálohování ani obnovení své databáze lokality. Obnovte sekundární lokalitu tím, že přeinstalujete sekundární lokalitu ze své nadřazené primární lokality.  

### <a name="deploy-a-hierarchy-of-sites-with-a-central-administration-site-and-one-or-more-child-primary-sites"></a>Nasazení hierarchie lokalit pomocí lokality centrální správy a jedné nebo několika podřízených primárních lokalit

Tato konfigurace může poskytovat odolnost proti chybám, když vaše lokality spravují překrývající se segmenty vaší sítě. Nabízí také další možnost obnovení pro použití informací ve sdílené databázi dostupné v jiné lokalitě, aby bylo možné znovu sestavit databázi lokality v obnovené lokalitě. Tuto možnost použijte, pokud chcete nahradit neúspěšnou nebo nedostupnou zálohu databáze lokality, která selhala.  

### <a name="create-regular-backups-at-central-administration-sites-and-primary-sites"></a>Vytváření pravidelných záloh v lokalitách centrální správy a primárních lokalitách

Když vytvoříte a otestujete běžnou zálohu lokality, zajistíte tím, že máte potřebná data pro obnovení lokality. V průběhu minimální doby se taky doporučuje obnovování lokality.  

### <a name="install-multiple-instances-of-site-system-roles"></a>Instalace více instancí rolí systému lokality

Když instalujete více instancí důležitých rolí systému lokality, zadáváte klientům redundantní body kontaktu. Například více bodů správy a distribučních bodů poskytuje redundantní službu v případě, že je konkrétní server v režimu offline.  

### <a name="install-multiple-instances-of-the-sms-provider-at-a-site"></a>Instalace více instancí poskytovatele serveru SMS v lokalitě

Poskytovatel serveru SMS poskytuje bod administrativního kontaktu pro jednu nebo více Configuration Manager konzol. Chcete-li poskytnout redundanci pro kontaktní body pro správu lokality a hierarchie, nainstalujte více poskytovatelů serveru SMS.  


## <a name="high-availability-for-site-system-roles"></a><a name="bkmk_ssr"></a>Vysoká dostupnost pro role systému lokality

V každé lokalitě nasadíte role systému lokality, které poskytují služby, které mají klienti v dané lokalitě používat. Databáze lokality obsahuje informace o konfiguraci lokality a všech klientů. Pomocí jedné nebo několika dostupných možností můžete zajistit vysokou dostupnost databáze lokality a obnovení lokality a databáze lokality v případě potřeby.  

### <a name="redundancy-for-important-site-system-roles"></a>Redundance důležitých rolí systému lokality

- Bod webové služby Katalog aplikací  

- Bod webu Katalog aplikací  

- Distribuční bod  

- Bod správy  

- Bod aktualizace softwaru  

- Bod migrace stavu  

Chcete-li zajistit redundanci vytváření sestav na webech a klientech, nainstalujte více instancí bodu služby Reporting Services.

V případě podpory převzetí služeb při selhání bodem aktualizace softwaru použijte Windows PowerShell k instalaci této role do clusteru služby Vyrovnávání zatížení sítě systému Windows (NLB).  

### <a name="built-in-site-backup"></a>Integrované zálohování lokality

Configuration Manager obsahuje integrovanou úlohu zálohování, která vám pomůžou zálohovat lokalitu a důležité informace podle pravidelného plánu. Kromě toho Průvodce instalací Configuration Manager podporuje akce obnovení lokality, které vám pomůžou obnovit lokalitu do provozu.  

### <a name="publishing-to-active-directory-domain-services-and-dns"></a>Publikování do služby Active Directory Domain Services a DNS

Nakonfigurujte jednotlivé lokality, aby publikovaly data o lokalitě pro Active Directory Domain Services a DNS. Publikování umožňuje klientům identifikovat dostupný server v síti. Klienti ji používají také k identifikaci, kdy jsou k dispozici nové servery systému lokality, které poskytují důležité služby, jako jsou body správy.  

### <a name="sms-provider-and-configuration-manager-console"></a>Poskytovatel serveru SMS a konzola Configuration Manager

Configuration Manager podporuje instalaci více poskytovatelů serveru SMS na samostatné servery jako více přístupových bodů pro konzolu nástroje. Pokud je jeden server poskytovatele služby SMS v režimu offline, můžete stále zobrazovat a spravovat lokality a klienty.  

Když se konzola Configuration Manager připojí k lokalitě nástroje, připojí se k instanci poskytovatele serveru SMS v dané lokalitě. Instance poskytovatele serveru SMS je náhodně vybrána. Pokud vybraný poskytovatel serveru SMS není dostupný, máte k dispozici následující možnosti:  

- Znovu připojte konzolu k lokalitě nástroje. Každé nové žádosti o připojení je náhodně přiřazená instance poskytovatele služby SMS. Je možné, že se nové připojení přiřadí k dostupné instanci.  

- Připojte konzolu k jiné Configuration Manager lokalitě a spravujte konfiguraci z tohoto připojení. Tato možnost zavádí mírné zpoždění změny konfigurace nepřesahující několik minut. Poté, co je poskytovatel serveru SMS pro lokalitu online, znovu připojte konzolu Configuration Manager přímo k lokalitě, kterou chcete spravovat.  

Nainstalujte konzolu Configuration Manager do více počítačů, které budou používat správci. Každý poskytovatel serveru SMS podporuje připojení z více než jedné konzoly.  

### <a name="management-point"></a>Bod správy

Nainstalujte několik bodů správy v každé primární lokalitě a umožněte webům publikovat data lokality do vaší infrastruktury služby Active Directory a DNS.  

Více bodů správy usnadňuje vyrovnávání zatížení pomocí jednoho bodu správy více klienty. Zvažte také instalaci jedné nebo více replik databáze pro body správy. Tato konfigurace snižuje operace bodu správy náročné na procesor. Také zvyšuje dostupnost této důležité role systému lokality.  

Sekundární lokality podporují jenom instalaci jednoho bodu správy, který se musí nacházet na serveru sekundární lokality. Body správy v sekundárních lokalitách se nepovažují za konfiguraci s vysokou dostupností.  

> [!NOTE]  
> Zařízení spravovaná pomocí místní správy mobilních zařízení se připojují pouze k jednomu bodu správy v primární lokalitě. Bod správy je přiřazený Configuration Manager mobilnímu zařízení během registrace a pak se nemění. Při instalaci více bodů správy a povolení více než jednoho pro mobilní zařízení je bod správy, který je přiřazen k klientovi mobilního zařízení, Nedeterministický.  
>
> Pokud bod správy, který klient mobilního zařízení používá, nebude k dispozici, je třeba vyřešit problém s tímto bodem správy nebo vymazat mobilní zařízení a znovu zaregistrovat mobilní zařízení, aby bylo možné jej přiřadit k provoznímu bodu správy, který je povolený pro mobilní zařízení.  

### <a name="distribution-point"></a>Distribuční bod

Nainstalujte několik distribučních bodů a nasaďte obsah do více distribučních bodů. Přidejte více než jeden distribuční bod na jednu hraniční skupinu, abyste se ujistili, že klienti získají v žádosti o obsah několik možností. Nakonfigurujte vztahy hraničních skupin tak, aby měly predicable nouzové chování do jiné skupiny hranic nebo cloudového distribučního bodu. Další informace najdete v tématu [Konfigurace skupin hranic](boundary-groups.md).  

### <a name="application-catalog-web-service-point-and-application-catalog-website-point"></a>Bod služeb webu Katalog aplikací a bod webu Katalog aplikací

> [!Important]
> Uživatelské prostředí programu Silverlight v katalogu aplikací není v aktuální větvi verze 1806 podporováno. Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací. Podpora končí pro role katalogu aplikací s verzí 1910.  
>
> Další informace najdete v těchto článcích:
>
> - [Konfigurace centra softwaru](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Odebrané a zastaralé funkce](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Nainstalujte více než jednu instanci každé role systému lokality. Nejlepšího výkonu dosáhnete, když nasadíte jednu z nich na stejný server systému lokality.  

Každá role systému lokality katalogu aplikací poskytuje stejné informace jako jiné instance této role bez ohledu na její umístění v hierarchii. Když klient vytvoří požadavek na katalog aplikací a Vy jste nakonfigurovali klienty na automatické zjišťování výchozího bodu webu katalogu aplikací, klient se přesměruje na dostupnou instanci. Klienti upřednostňují místní instance katalogu aplikací na základě aktuálního umístění v síti klienta.  

Další informace o tomto nastavení klienta a o tom, jak funguje automatické zjišťování, najdete v tématu Nastavení klienta [Počítačový agent](../../../clients/deploy/about-client-settings.md#computer-agent) .  


## <a name="high-availability-for-clients"></a><a name="bkmk_client"></a>Vysoká dostupnost pro klienty  

### <a name="client-operations-are-autonomous"></a>Klientské operace jsou autonomní

Configuration Manager autonomii klienta nástroje zahrnuje následující chování:  

- Klienti nevyžadují nepřetržitý kontakt s žádnými konkrétními servery systému lokality. Používají známé konfigurace k provádění předem nakonfigurovaných akcí podle plánu.  

- Klienti mohou používat jakoukoli dostupnou instanci role systému lokality, která poskytuje služby klientům. Pokusí se kontaktovat známé servery, dokud nenalezne dostupný server.  

- Klienti mohou spustit inventarizaci, nasazení softwaru a podobné plánované akce nezávisle na přímém kontaktu se servery systému lokality.  

- Klienti, kteří jsou nakonfigurováni pro použití náhradního stavového bodu, mohou odeslat podrobnosti do záložního stavového bodu, pokud nemohou komunikovat s bodem správy.  

### <a name="clients-can-repair-themselves"></a>Klienti si můžou sami opravit

Klienti automaticky napravují většinu typických problémů bez přímého zásahu pro správu.  

- Klienti pravidelně vyhodnocují svůj stav. Provádějí kroky k nápravě typických problémů pomocí místní mezipaměti nápravných kroků a zdrojových souborů pro opravy.  

- Když se klientovi nepovede odeslat stavové informace do lokality, může vygenerovat výstrahu. Uživatelé s právy pro správu, kteří obdrží tyto výstrahy, mohou provést okamžitou akci obnovení normálního provozu klienta.  

### <a name="clients-cache-information-to-use-in-the-future"></a>Klienti uloží informace do mezipaměti pro budoucí použití.

Když klient komunikuje s bodem správy, může klient získat a Uložit do mezipaměti následující informace:  

- Nastavení klienta  

- Plány klientů  

- Informace o nasazení softwaru a stažení softwaru, který je naplánován na instalaci klienta, pokud je nasazení nakonfigurováno pro tuto akci.  

Pokud klient nemůže kontaktovat bod správy, klienti místně zadají do mezipaměti informace o stavu, stavu a klientovi, které nahlásí do lokality. Klient přenáší tato data poté, co vytvoří kontakt s bodem správy.  

### <a name="client-can-submit-status-to-a-fallback-status-point"></a>Klient může odeslat stav do bodu stavu pro použití náhradní lokality.

Když nakonfigurujete klienta nástroje tak, aby používal bod záložního stavu, poskytnete klientovi další kontaktní bod pro odeslání důležitých podrobností o jeho provozu. Klienti, kteří jsou nakonfigurováni pro použití náhradního stavového bodu, nadále odesílají stav o operacích do této role systému lokality, i když klient nemůže komunikovat s bodem správy.  

### <a name="central-management-of-client-data-and-client-identity"></a>Centrální správa klientských dat a klientské identity

Databáze lokality místo jednotlivých klientů uchovává důležité informace o identitě jednotlivých klientů a přidruží tato data k určitému počítači nebo uživateli.  

- Zdrojové soubory klienta v počítači lze odinstalovat a znovu nainstalovat, aniž by to ovlivnilo historické záznamy pro počítač, ve kterém je nainstalován klient nástroje.  

- Selhání klientského počítače nemá vliv na integritu informací uložených v databázi. Tyto informace mohou být k dispozici pro vytváření sestav.  


## <a name="options-for-sites-and-site-system-roles-that-arent-highly-available"></a><a name="bkmk_nonHAoptions"></a>Možnosti pro lokality a role systému lokality, které nejsou vysoce dostupné

Některé systémy lokality nepodporují více instancí v lokalitě nebo v hierarchii. Tyto informace vám pomůžou připravit se na tyto systémy lokality, které přechází do stavu offline.  

### <a name="asset-intelligence-synchronization-point-hierarchy"></a>Bod synchronizace katalogu Asset Intelligence (hierarchie)

Tato role systému lokality není považována za kritickou a poskytuje volitelné funkce v Configuration Manager. Pokud je tento systém lokality přepnut do režimu offline, použijte jednu z následujících možností:  

- Vyřešte důvod, proč je systém lokality offline.  

- Odinstalujte roli z aktuálního serveru a nainstalujte roli na nový server.  

### <a name="endpoint-protection-point-hierarchy"></a>Bod Endpoint Protection (hierarchie)

Tato role systému lokality není považována za kritickou a poskytuje volitelné funkce v Configuration Manager. Pokud je tento systém lokality přepnut do režimu offline, použijte jednu z následujících možností:  

- Vyřešte důvod, proč je systém lokality offline.  

- Odinstalujte roli z aktuálního serveru a nainstalujte roli na nový server.  

### <a name="enrollment-point-site"></a>Bod registrace (lokalita)

Tato role systému lokality není považována za kritickou a poskytuje volitelné funkce v Configuration Manager. Pokud je tento systém lokality přepnut do režimu offline, použijte jednu z následujících možností:  

- Vyřešte důvod, proč je systém lokality offline.  

- Odinstalujte roli z aktuálního serveru a nainstalujte roli na nový server.  

### <a name="enrollment-proxy-point-site"></a>Zprostředkující bod registrace (lokalita)

Tato role systému lokality není považována za kritickou a poskytuje volitelné funkce v Configuration Manager. V lokalitě a ve více lokalitách v hierarchii však můžete nainstalovat více instancí této role systému lokality. Pokud je tento systém lokality přepnut do režimu offline, použijte jednu z následujících možností:  

- Vyřešte důvod, proč je systém lokality offline.  

- Odinstalujte roli z aktuálního serveru a nainstalujte roli na nový server.  

Pokud v lokalitě máte více než jednu proxy server registrace, použijte pro název serveru alias DNS. Při použití této konfigurace poskytuje služba DNS pro kruhové dotazování odolnost proti chybám a vyrovnávání zatížení pro uživatele, kteří si zaregistrují svá mobilní zařízení.  

### <a name="fallback-status-point-site-or-hierarchy"></a>Bod záložního stavu (lokalita nebo hierarchie)

Tato role systému lokality není považována za kritickou a poskytuje volitelné funkce v Configuration Manager. Pokud je tento systém lokality přepnut do režimu offline, použijte jednu z následujících možností:  

- Vyřešte důvod, proč je systém lokality offline.  

- Odinstalujte roli z aktuálního serveru a nainstalujte roli na nový server. Vzhledem k tomu, že jsou klienti v průběhu instalace klienta přiřazeni k bodu záložního stavu, je nutné změnit stávající klienty na použití nového serveru systému lokality.  

### <a name="service-connection-point-hierarchy"></a>Bod připojení služby (hierarchie)

I když je tato role systému lokality zásadní pro udržení Configuration Manager aktuální větve, obvykle se nepoužívá často. Pokud tento systém přejde do režimu offline, použijte jednu z následujících možností:

- Vyřešte důvod, proč je systém lokality offline.  

- Odinstalujte roli z aktuálního serveru a nainstalujte roli na nový server.  


## <a name="see-also"></a>Viz také

- [Podporované konfigurace](../../../plan-design/configs/supported-configurations.md)  

- [Doporučený hardware](../../../plan-design/configs/recommended-hardware.md)  

- [Podporované operační systémy pro servery systému lokality](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)

- [Požadavky na lokality a systémy lokalit](../../../plan-design/configs/site-and-site-system-prerequisites.md)  

- [Dopady selhání lokality](../../manage/site-failure-impacts.md)  
