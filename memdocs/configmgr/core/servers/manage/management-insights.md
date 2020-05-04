---
title: Přehledy správy
titleSuffix: Configuration Manager
description: Přečtěte si informace o funkcích přehledů správy dostupných v konzole Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e9aae1da48deabd0cc339cd25055827caf07354b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713734"
---
# <a name="management-insights-in-configuration-manager"></a>Přehledy správy v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Přehledy správy v Configuration Manager poskytují informace o aktuálním stavu vašeho prostředí. Informace jsou založeny na analýze dat z databáze lokality. Přehledy vám pomůžou lépe pochopit vaše prostředí a provádět akce na základě přehledu. <!--1353967-->

## <a name="review-management-insights"></a>Kontrola přehledů správy

Chcete-li zobrazit pravidla, váš účet potřebuje oprávnění **číst** pro objekt **lokalita** .

1. Otevřete konzolu Configuration Manager.  

2. Otevřete pracovní prostor **Správa** , rozbalte **přehledy pro správu**a vyberte **všechny přehledy**.  

    > [!Note]  
    > Když vyberete uzel **přehledy správy** , zobrazí se [řídicí panel přehledy správy](#bkmk_insights).  

3. Otevřete název skupiny Management Insights, který chcete zkontrolovat. Na pásu karet vyberte **Zobrazit přehledy** .  

K dispozici jsou následující čtyři karty ke kontrole:

- **Všechna pravidla**: poskytuje úplný seznam pravidel pro vybranou skupinu pro správu.  

- **Complete**: vypíše pravidla, která nevyžadují žádnou akci.  

- **Probíhá**: zobrazuje pravidla, u kterých jsou splněné některé předpoklady, ale ne všechny.  

- **Nutná akce**: jsou uvedena pravidla, která vyžadují akce. Pokud chcete načíst konkrétní položky, které vyžadují akci, vyberte **Další podrobnosti** .  

V podokně **požadavky** najdete seznam požadovaných položek potřebných ke spuštění pravidla.

### <a name="all-rules-and-prerequisites-for-the-cloud-services-group"></a>Všechna pravidla a požadavky pro skupinu Cloud Services

![Přehledy pro správu – všechna pravidla a předpoklady pro skupinu Cloud Services](./media/Management-insights-all-cloud-rules.png)

Vyberte pravidlo a pak kliknutím na **Další podrobnosti** zobrazte podrobnosti o pravidle.

## <a name="operations"></a>Operace

Pravidla přehledu správy přehodnotí své použitelnosti na týdenní plán. Pokud chcete pravidlo znovu vyhodnotit na vyžádání, klikněte na něj pravým tlačítkem a vyberte **znovu vyhodnotit**.

Soubor protokolu pro pravidla přehledu pro správu je **SMS_DataEngine. log** na serveru lokality.

<!--1357930-->
Některá pravidla umožňují provést akci. Vyberte pravidlo, klikněte na **Další podrobnosti**a pak pokud je dostupná **Akce vybrat provést**.

V závislosti na pravidle má tato akce jedno z následujících chování:  

- Automaticky navigujte v konzole nástroje na uzel, kde můžete provádět další akce. Pokud například služba Management Insights doporučuje změnit nastavení klienta, převezme akce Přejít na uzel nastavení klienta. Pak proveďte další akci úpravou výchozího nebo vlastního objektu nastavení klienta.  

- Přejděte do filtrovaného zobrazení na základě dotazu. Například provedení akce na základě pravidla prázdné kolekce zobrazí v seznamu kolekcí pouze tyto kolekce. Pak proveďte další akce, jako je odstranění kolekce nebo změna pravidel členství.  

## <a name="management-insights-dashboard"></a><a name="bkmk_insights"></a>Řídicí panel Management Insights

<!--1357979-->

Uzel **Management Insights** obsahuje grafický řídicí panel. Tento řídicí panel zobrazuje přehled stavů pravidel, což usnadňuje zobrazení průběhu.

K upřesnění zobrazení použijte následující filtry v horní části řídicího panelu:

- Zobrazit dokončené
- Nepovinné
- Doporučené
- Kritická

Řídicí panel obsahuje tyto dlaždice:  

- **Index Insights pro správu**: sleduje celkový pokrok v pravidlech přehledů správy. Index je vážený průměr. Jsou to nejvíce nejdůležitější pravidla. Tento index poskytuje nejmenší váhu volitelným pravidlům.  

- **Skupiny Insights pro správu**: zobrazuje procento pravidel v každé skupině, které dodržují filtry. Vyberte skupinu pro přechod k podrobnostem o konkrétních pravidlech v této skupině.  

- **Priorita Management Insights**: zobrazuje procento pravidel podle priority a respektování filtrů.  

- **Všechny přehledy**: tabulka přehledů, včetně priority a stavu. Použijte pole **filtru** v horní části tabulky, aby se shodovaly s řetězci v libovolném dostupném sloupci. Řídicí panel seřadí tabulku v následujícím pořadí:

  - Stav: akce je vyžadována, dokončeno, neznámá  
  - Priorita: kritická, doporučená, volitelná  
  - Poslední změna: starší kalendářní data nahoře  

![Snímek obrazovky s řídicím panelem Management Insights](media/1357979-management-insights-dashboard.png)

## <a name="groups-and-rules"></a>Skupiny a pravidla

Pravidla jsou uspořádaná do následujících skupin přehledů správy:

- [Aplikace](#applications)
- [Cloudové služby](#cloud-services)
- [Kolekce](#collections)
- [Posouzení Configuration Manager](#configuration-manager-assessment)
- [Proaktivní údržba](#proactive-maintenance)
- [Zabezpečení](#security)
- [Zjednodušená správa](#simplified-management)
- [Centrum softwaru](#software-center)
- [Windows 10](#windows-10)

### <a name="applications"></a>Aplikace

Přehledy pro správu vaší aplikace

- **Aplikace bez nasazení**: Vypíše aplikace v prostředí, které nemají aktivní nasazení. Toto pravidlo vám pomůže najít a odstranit nepoužívané aplikace a zjednodušit tak seznam aplikací zobrazených v konzole nástroje. Další informace najdete v tématu [nasazení aplikací](../../../apps/deploy-use/deploy-applications.md).  

### <a name="cloud-services"></a>Cloud Services

Umožňuje integraci s mnoha Cloud Services, což umožňuje moderní správu vašich zařízení.

- **Posouzení připravenosti spolusprávy**: pomůže vám pochopit, jaké kroky je potřeba k povolení spolusprávy. Toto pravidlo má požadavky. Další informace najdete v tématu [Přehled spolusprávy](../../../comanage/overview.md).  

- **Zařízení neodeslaná do Azure AD**: počínaje verzí 2002 toto pravidlo obsahuje zařízení, která nejsou nahraná do Azure AD, protože lokalita není správně nakonfigurovaná pro protokol HTTPS.<!--6268489--> Nakonfigurujte [Rozšířený protokol HTTP](../../plan-design/hierarchy/enhanced-http.md)nebo povolte alespoň jeden bod správy pro protokol HTTPS. Pokud jste již lokalitu nakonfigurovali pro komunikaci pomocí protokolu HTTPS, toto pravidlo se nezobrazí.

- **Konfigurace služeb Azure pro použití s Configuration Manager**: Toto pravidlo vám pomůže připojit se Configuration Manager ke službě Azure AD, která umožňuje klientům ověřování pomocí Azure AD s lokalitou. Další informace najdete v tématu [Konfigurace služeb Azure](../deploy/configure/azure-services-wizard.md).  

- **Povolit, aby zařízení byla připojená k hybridnímu Azure Active Directory**: zařízení připojená k Azure AD umožňují uživatelům přihlašovat se pomocí svých přihlašovacích údajů do domény a zajistit, aby zařízení splňovala standardy zabezpečení a dodržování předpisů organizace. Další informace najdete v tématu věnovaném [faktorům pro návrh hybridní identity Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview).  

- **Lokality, které nemají správnou konfiguraci protokolu HTTPS**: počínaje verzí 2002 toto pravidlo vypíše lokality v hierarchii, které nejsou správně nakonfigurované pro protokol HTTPS. Tato konfigurace brání lokalitě v [synchronizaci výsledků členství kolekce do skupin Azure Active Directory (Azure AD)](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync). Může to způsobit, že synchronizace služby Azure AD nebude nahrávat všechna zařízení. Správa těchto klientů nemusí fungovat správně.<!--6268489--> Nakonfigurujte [Rozšířený protokol HTTP](../../plan-design/hierarchy/enhanced-http.md)nebo povolte alespoň jeden bod správy pro protokol HTTPS. Pokud jste již lokalitu nakonfigurovali pro komunikaci pomocí protokolu HTTPS, toto pravidlo se nezobrazí.

- **Aktualizace klientů na nejnovější verzi Windows 10**: Windows 10, verze 1709 nebo vyšší zlepšuje a modernizes výpočetní prostředí vašich uživatelů. Další informace najdete v části [klíčové články o přijetí Windows jako služby](../../understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service).  

### <a name="collections"></a>Kolekce

Přehledy, které zjednodušují správu tím, že čistí a mění konfiguraci kolekcí.

- **Prázdné kolekce**: vypíše kolekce v prostředí, které nemají žádné členy. Další informace najdete v tématu [Správa kolekcí](../../clients/manage/collections/manage-collections.md).  

Počínaje verzí 1902 jsou k dispozici nová pravidla s doporučeními pro správu kolekcí.<!--3555752--> Pomocí těchto přehledů můžete zjednodušit správu a zvýšit výkon:

- **Kolekce bez pravidel dotazů a přímých členů**: Chcete-li zjednodušit seznam kolekcí ve vaší hierarchii, odstraňte tyto kolekce.  

- **Kolekce se stejným časem zahájení přehodnocení**: tyto kolekce mají stejný čas opětovného vyhodnocení jako jiné kolekce. Upravte čas opakovaného vyhodnocení, aby nedošlo ke konfliktu.  

- **Kolekce s časem dotazu během dvou sekund**: Zkontrolujte pravidla dotazu pro tuto kolekci. Zvažte úpravu nebo odstranění kolekce.

- Následující pravidla zahrnují konfigurace, které potenciálně způsobují zbytečné zatížení webu. Zkontrolujte tyto kolekce, pak je buď odstraňte, nebo vyhodnocování pravidla vypněte:  

  - **Kolekce bez povolených pravidel dotazů a přírůstkových aktualizací**  

  - **Kolekce bez pravidel dotazů a povolené pro plánované nebo přírůstkové hodnocení**  

  - **Kolekce bez pravidel dotazů a plánovaného úplného vyhodnocení**  

### <a name="configuration-manager-assessment"></a>Posouzení Configuration Manager

<!--3607758-->

Od verze 2002 se tato skupina nepoužívá v oblasti technické podpory Microsoft Premier. Tato pravidla jsou ukázkou mnoha dalších kontrol, které Microsoft Premier nabízí v [centru služeb](https://docs.microsoft.com/services-hub/health/getting_started_with_on_demand_assessments).

- **Zjišťování skupiny zabezpečení služby Active Directory je nakonfigurované tak, aby se spouštělo příliš často**: obvykle není potřeba konfigurovat zjišťování skupin zabezpečení služby Active Directory tak, aby probíhalo častěji než v každé tři hodiny. Častější konfigurace může mít negativní dopad na výkon služby Active Directory, sítě a Configuration Manager. Místo použití úplného plánu synchronizace povolte přírůstkovou synchronizaci. Další informace najdete v tématu [zjišťování skupin služby Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutGroup).

- **Zjišťování systémových souborů služby Active Directory je nakonfigurováno tak, aby běželo příliš často**: nemusíte obvykle konfigurovat zjišťování systému služby Active Directory tak, aby probíhalo častěji než každé tři hodiny. Častější konfigurace může mít negativní dopad na výkon služby Active Directory, sítě a Configuration Manager. Místo použití úplného plánu synchronizace povolte přírůstkovou synchronizaci. Další informace najdete v tématu [zjišťování systémových informací služby Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutSystem).

- **Zjišťování uživatelů služby Active Directory je nakonfigurováno tak, aby běželo příliš často**: nemusíte obvykle konfigurovat zjišťování uživatelů služby Active Directory tak, aby probíhalo častěji než každé tři hodiny. Častější konfigurace může mít negativní dopad na výkon služby Active Directory, sítě a Configuration Manager. Místo použití úplného plánu synchronizace povolte přírůstkovou synchronizaci. Další informace najdete v tématu [zjišťování uživatelů služby Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

- **Kolekce omezené na všechny systémy nebo všechny uživatele**: Projděte si všechny kolekce, které používají kolekce **všechny systémy** nebo **Všichni uživatelé** jako omezení kolekce. Configuration Manager aktualizuje členství těchto výchozích kolekcí s daty z metod zjišťování služby Active Directory. Tato data nemusí být platná informace pro klienty Configuration Manager.

- **Zjišťování prezenčního signálu je zakázané**: zjišťování prezenčního signálu vyžaduje, abyste na zařízení nainstalovali klienta Configuration Manager. Je to jediná metoda zjišťování, kterou klienti spouštějí. Všechny ostatní metody se vyskytují na serverech lokality. Zjišťování prezenčního signálu je nezbytné pro udržení stavu aktivity klienta v aktuálním stavu. Tím se zajistí, že lokalita nebude náhodně vymezit záznamy o prostředcích z databáze lokality. Další informace najdete v tématu [zjišťování prezenčního signálu](../deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).

- **Dlouhotrvající dotazy na kolekci povolené pro přírůstkové aktualizace**: kolekce s časem poslední přírůstkové aktualizace delší než 30 sekund používají server lokality a databázové prostředky, což může potenciálně ovlivnit celkový Configuration Manager výkon. Další informace najdete v tématu [osvědčené postupy pro kolekce](../../clients/manage/collections/best-practices-for-collections.md).

- **Snižte počet aplikací a balíčků v distribučních bodech**: Společnost Microsoft oficiálně podporuje kombinovaný součet až 10 000 balíčků a aplikací v distribučním bodě. Překročení tohoto celkového množství může vést k provozním problémům. Další informace naleznete v tématu [size and Scale Numbers-Distribution Point](../../plan-design/configs/size-and-scale-numbers.md#distribution-point).

- **Problémy při instalaci sekundárního webového serveru**: stav instalace některých sekundárních lokalit **čeká na vyřízení** nebo **selhal**. Tato stavová skutečnost znamená, že jste spustili instalaci, ale ta se nedokončila úspěšně. Až se instalace sekundární lokality dokončí, klienti nemusí správně komunikovat s primární lokalitou. Ověřte pracovní prostor **monitorování** a zkuste instalaci zopakovat. Další informace najdete v tématu [opakování instalace aktualizace, která se nezdařila](install-in-console-updates.md#bkmk_retry).

- **Aktualizovat všechny lokality na stejnou verzi**: použijte stejnou verzi Configuration Manager v hierarchii. Tato konfigurace zajišťuje, že všechny lokality poskytují stejné funkce. Lokality různých verzí ve stejné hierarchii představují scénáře interoperability. Novější verze Configuration Manager zahrnují nové funkce a řeší známé problémy. Další informace najdete v tématu [vzájemná funkční spolupráce mezi různými verzemi](../../plan-design/hierarchy/interoperability-between-different-versions.md).

Další informace o těchto pravidlech najdete v tématu [opravné kroky pro Configuration Manager přehledy správy](https://docs.microsoft.com/services-hub/health/remediation-steps-configmgr).

> [!TIP]
> Pokud už jste zákazníkem Microsoft Unified nebo Microsoft Premier, přihlaste se k [centru služeb](https://serviceshub.microsoft.com/assessments/) , kde najdete další posouzení na vyžádání.
>
> Další informace o službách Microsoftu najdete v tématu [Podpora řešení](https://www.microsoft.com/enterprise/services/support).

### <a name="proactive-maintenance"></a>Proaktivní údržba

<!--1352184-->
Pravidla v této skupině zvýrazňují možné problémy s konfigurací, abyste se vyhnuli udržováním Configuration Manager objektů.

- **Hraniční skupiny bez přiřazených systémů lokality**: bez přiřazených systémů lokality lze skupiny hranic použít pouze pro přiřazení lokality. Další informace najdete v tématu [Konfigurace skupin hranic](../deploy/configure/boundary-groups.md).  

- **Skupiny hranic bez členů**: skupiny hranic nejsou použitelné pro přiřazení lokality nebo vyhledávání obsahu, pokud nemají žádné členy. Další informace najdete v tématu [Konfigurace skupin hranic](../deploy/configure/boundary-groups.md).  

- **Distribuční body, které neobsluhují obsah pro klienty**: distribuční body, které klientům za posledních 30 dní nesloužili obsahu. Tato data jsou založená na sestavách od klientů jejich historie stahování. Další informace najdete v tématu [instalace a konfigurace distribučních bodů](../deploy/configure/install-and-configure-distribution-points.md).  

- **Povolit službu WSUS Cleanup**: ověřuje, že jste povolili možnost spustit čištění služby WSUS ve vlastnostech komponenty bodu aktualizace softwaru. Tato možnost pomáhá zlepšit výkon služby WSUS. Další informace najdete v tématu [Údržba aktualizací softwaru](../../../sum/deploy-use/software-updates-maintenance.md).  

- **Nepoužívané spouštěcí bitové kopie**: spouštěcí bitové kopie neodkazují na spouštění pomocí technologie PXE nebo použití pořadí úloh. Další informace najdete v tématu [Správa spouštěcích imagí](../../../osd/get-started/manage-boot-images.md).  

- **Nepoužité položky konfigurace**: položky konfigurace, které nejsou součástí standardních hodnot konfigurace a jsou starší než 30 dní. Další informace najdete v tématu [Vytvoření standardních hodnot konfigurace](../../../compliance/deploy-use/create-configuration-baselines.md).  

- **Upgradovat zdroje sdílené mezipaměti na nejnovější verzi Configuration Manager klienta**: Identifikujte klienty, kteří slouží jako zdroj sdílené mezipaměti, ale neupgradovali se z verze klienta starší než 1806. Klienty starších než 1806 nelze použít jako zdroj sdílené mezipaměti pro klienty, kteří používají verzi 1806 nebo novější. Výběrem možnosti **provést akci** otevřete zobrazení zařízení, které zobrazí seznam klientů.<!--1358008-->  

### <a name="security"></a>Zabezpečení

Přehledy pro zlepšení zabezpečení infrastruktury a zařízení.

- **Je povolená záloha protokolu NTLM**:<!--4572953--> Počínaje verzí 1906 toto pravidlo zjistí, zda jste u lokality povolili metodu Fallback pro použití méně zabezpečených ověření NTLM. Při použití metody push klienta pro instalaci klienta Configuration Manager může lokalita vyžadovat vzájemné ověřování protokolem Kerberos. Toto vylepšení pomáhá zabezpečit komunikaci mezi serverem a klientem. Další informace najdete v tématu [instalace klientů pomocí klientské nabízené instalace](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).

- **Nepodporované verze antimalwarového klienta**: na více než 10% klientů běží verze Endpoint Protection System Center, které se nepodporují. Další informace najdete v tématu [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).  

### <a name="simplified-management"></a>Zjednodušená správa

Přehledy, které vám pomůžou zjednodušit každodenní správu vašeho prostředí.

- **Připojení lokality k Microsoft cloudu pro Configuration Manager aktualizace**: Toto pravidlo zajišťuje, že se váš spojovací bod služby Configuration Manager v posledních sedmi dnech připojil ke cloudu Microsoftu. Toto připojení umožňuje stahovat obsah pro pravidelné aktualizace. Zkontrolujte protokol DMPDownloader. log a hman. log. Další informace najdete v tématu [požadavky na přístup k Internetu](../../plan-design/network/internet-endpoints.md#bkmk_scp-updates).

- **Verze klientů nepatřících k síti pro vyžádání**: zobrazí seznam všech klientů, jejichž verze není sestavením aktuální větve. Další informace najdete v tématu [upgrade klientů](../../clients/manage/upgrade/upgrade-clients.md).  

- **Aktualizace klientů na podporovanou verzi Windows 10**: počínaje verzí 1902 toto pravidlo vytváří sestavy na klientech, na kterých běží verze Windows 10, která už není podporovaná. Zahrnuje taky klienty s verzí Windows 10, která se blíží konci služby (tři měsíce).<!--3897268-->  

### <a name="software-center"></a>Centrum softwaru

Přehledy pro správu centra softwaru

- **Směrování uživatelů do centra softwaru namísto katalogu aplikací**: Ověřte, zda uživatelé v posledních 14 dnech nainstalovali nebo požadovali aplikace z katalogu aplikací. Hlavní funkce katalogu aplikací je teď součástí centra softwaru. Podpora končí pro role katalogu aplikací s verzí 1910. Další informace najdete v tématu [zastaralé funkce](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).  

- **Používat novou verzi centra softwaru**: předchozí verze centra softwaru už není podporovaná. Nastavte klienty na použití nového centra softwaru tak, že povolíte nastavení klienta **použít nové centrum softwaru** ve skupině **Počítačový agent** . Další informace najdete v tématu [informace o nastavení klienta](../../clients/deploy/about-client-settings.md#use-new-software-center).  

### <a name="software-updates"></a>Aktualizace softwaru

- **Nastavení klienta není nakonfigurováno tak, aby umožňovalo klientům stahovat rozdílový obsah**: některé aktualizace softwaru synchronizované ve vašem prostředí zahrnují rozdílový obsah. Povolte nastavení klienta **Povolit klientům stahování rozdílových obsahu, pokud je k dispozici**. Pokud toto nastavení nepovolíte, bude klient při nasazení těchto aktualizací zbytečně stahovat více obsahu, než potřebují. Další informace najdete v tématu [nastavení klienta – aktualizace softwaru](../../clients/deploy/about-client-settings.md#software-updates).

- **Povolit kategorii produktů aktualizace softwaru ' Windows 10, verze 1903 a novější '**: pro Windows 10, verze 1903 a novější je k dispozici nová kategorie produktů aktualizace softwaru. Pokud synchronizujete aktualizace Windows 10 a máte klienty se systémem Windows 10, verze 1903 nebo novější, vyberte ve vlastnostech komponenty bodu aktualizace softwaru kategorii produktů **Windows 10, verze 1903 a novější** . Další informace najdete v tématu[Konfigurace klasifikací a produktů k synchronizaci](../../../sum/get-started/configure-classifications-and-products.md).

### <a name="windows-10"></a>Windows 10

Přehledy související s nasazením a obsluhou Windows 10 Skupina Windows 10 Management Insights je dostupná jenom v případě, že na víc než polovinu klientů běží Windows 7, Windows 8 nebo Windows 8.1.

- **Konfigurace diagnostických dat Windows a klíče komerčního ID**: Pokud chcete používat data z Desktop Analytics, nakonfigurujte zařízení pomocí kódu komerčního ID a povolte shromažďování diagnostických dat. Nastavte zařízení s Windows 10 na úroveň **Rozšířené (omezené)** nebo vyšší. Další informace najdete v tématu [Povolení sdílení dat pro desktopovou analýzu](../../../desktop-analytics/enable-data-sharing.md).

#### <a name="windows-10-management-insights-rules"></a>Pravidla Windows 10 Management Insights

![Přehledy správy – pravidla pro Windows 10](./media/Windows-10-insights-group.png)
