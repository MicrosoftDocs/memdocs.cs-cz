---
title: Přehledy správy
titleSuffix: Configuration Manager
description: Přečtěte si informace o funkcích přehledů správy dostupných v konzole Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3d65c83d0a9fd009fa21a3b9e623145f87cc9498
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128105"
---
# <a name="management-insights-in-configuration-manager"></a>Přehledy správy v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Přehledy správy v Configuration Manager poskytují informace o aktuálním stavu vašeho prostředí. Informace jsou založeny na analýze dat z databáze lokality. Přehledy vám pomůžou lépe pochopit vaše prostředí a provádět akce na základě přehledu. <!--1353967-->

## <a name="review-management-insights"></a>Kontrola přehledů správy

Pokud chcete zobrazit přehledy, váš účet potřebuje oprávnění **číst** pro objekt **lokalita** .

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte **přehledy pro správu**a vyberte **všechny přehledy**.

    > [!NOTE]
    > Když vyberete uzel **přehledy správy** , zobrazí se [řídicí panel přehledy správy](#bkmk_insights).

1. Otevřete název skupiny Management Insights, který chcete zkontrolovat.

1. Na pásu karet vyberte **Zobrazit přehledy**.

K dispozici jsou následující čtyři karty ke kontrole:

- **Všechna pravidla**: poskytuje úplný seznam přehledů pro zvolenou skupinu.

- **Dokončeno**: vypíše přehledy, v nichž není nutné provádět žádnou akci.

- **Probíhá**: zobrazuje přehledy o tom, kde jsou některé, ale ne všechny, požadavky dokončeny.

- Je **potřeba akce**: na této kartě jsou uvedeny přehledy, které potřebují provést akci. Chcete-li zobrazit konkrétní položky, kde je vyžadována akce, vyberte **Další podrobnosti** .

V podokně **požadavky** najdete seznam všech požadovaných položek potřebných ke spuštění vybraného přehledu.

Například následující snímek obrazovky ukazuje příklad karty **všechna pravidla** pro skupinu **Cloud Services** :

:::image type="content" source="media/management-insights-all-cloud-rules.png" alt-text="Přehledy správy: všechna pravidla a požadavky pro skupinu Cloud Services":::

Pokud chcete zobrazit podrobnosti, vyberte přehled a pak vyberte **Další podrobnosti**.

## <a name="operations"></a>Operace

Lokalita znovu vyhodnocuje použitelnost přehledů správy s týdenním plánem. Pokud chcete ručně přehodnotit přehled, klikněte pravým tlačítkem na přehled a vyberte **znovu vyhodnotit**.

Soubor protokolu pro přehledy správy je **SMS_DataEngine. log** na serveru lokality.

<!--1357930-->
Některé přehledy umožňují provádět akce. Vyberte přehled, vyberte **Další podrobnosti**a pak pokud je dostupná akce vybrat **provést**. V závislosti na tomto přehledu má tato akce jedno z následujících chování:

- Automaticky navigujte v konzole nástroje na uzel, kde můžete provádět další akce. Pokud například služba Management Insights doporučuje změnit nastavení klienta, převezme akce Přejít na uzel **nastavení klienta** . Pak proveďte další akci úpravou výchozího nebo vlastního objektu nastavení klienta.

- Přejděte do filtrovaného zobrazení na základě dotazu. Například při provádění akce v přehledu prázdných kolekcí se v seznamu kolekcí zobrazí pouze tyto kolekce. Pak proveďte další akce, jako je odstranění kolekce nebo změna pravidel členství.

## <a name="management-insights-dashboard"></a><a name="bkmk_insights"></a>Řídicí panel Management Insights

<!--1357979-->

Vyberte uzel **přehledy správy** pro zobrazení grafického řídicího panelu. Tento řídicí panel zobrazuje přehled stavů Insight, což vám usnadní zobrazení vašeho pokroku.

K upřesnění zobrazení použijte následující filtry v horní části řídicího panelu:

- Zobrazit dokončené
- Volitelné
- Doporučeno
- Kritické

Řídicí panel obsahuje tyto dlaždice:  

- **Index Insights pro správu**: sleduje celkový pokrok v přehledech správy. Index je vážený průměr. Jsou to nejvíc nejdůležitější přehledy. Tento index poskytuje minimální váhu pro volitelné přehledy.

- **Skupiny přehledů správy**: zobrazuje procento přehledů v každé skupině, které dodržují filtry. Vyberte skupinu, abyste přešli na konkrétní přehledy v této skupině.

- **Priorita Management Insights**: zobrazuje procento přehledů podle priority a respektování filtrů.

- **Prvních 10 použitelných pravidel pro přehled**: tabulka přehledů včetně priority a stavu. Použijte pole **filtru** v horní části tabulky, aby se shodovaly s řetězci v libovolném dostupném sloupci. Řídicí panel seřadí tabulku v následujícím pořadí:

  - Stav: akce je vyžadována, dokončeno, neznámá  
  - Priorita: kritická, doporučená, volitelná  
  - Poslední změna: starší kalendářní data nahoře  

:::image type="content" source="media/1357979-management-insights-dashboard.png" alt-text="Snímek obrazovky s řídicím panelem Management Insights" lightbox="media/1357979-management-insights-dashboard.png":::

## <a name="groups-and-insights"></a>Skupiny a přehledy

Přehledy jsou uspořádány do následujících skupin přehledů správy:

- [Aplikace](#applications)
- [Cloudové služby](#cloud-services)
- [Kolekce](#collections)
- [Posouzení Configuration Manager](#configuration-manager-assessment)
- [Optimalizovat pro vzdálené pracovníky](#optimize-for-remote-workers)
- [Proaktivní údržba](#proactive-maintenance)
- [Zabezpečení](#security)
- [Zjednodušená správa](#simplified-management)
- [Centrum softwaru](#software-center)
- [Aktualizace softwaru](#software-updates)
- [Windows 10](#windows-10)

> [!NOTE]
> Váš web nemusí zobrazovat všechny následující skupiny a přehledy. Některé přehledy se nezobrazí, pokud jste již lokalitu pro doporučení nakonfigurovali.

### <a name="applications"></a>Aplikace

Přehledy pro správu vaší aplikace

- **Aplikace bez nasazení nebo odkazů**: Vypíše aplikace v prostředí, které nemají aktivní nasazení nebo odkazy. Odkazy zahrnují závislosti, pořadí úloh a virtuální prostředí. Tento přehled vám pomůže najít a odstranit nepoužívané aplikace a zjednodušit tak seznam aplikací zobrazených v konzole. Další informace najdete v tématu [nasazení aplikací](../../../apps/deploy-use/deploy-applications.md).<!-- B585E3FF-585F-4CE9-AE2C-648A7CA2F143 -->

### <a name="cloud-services"></a>Cloud Services

Umožňuje integraci s mnoha Cloud Services, což umožňuje moderní správu vašich zařízení.

- **Posouzení připravenosti spolusprávy**: pomůže vám pochopit, jaké kroky je potřeba k povolení spolusprávy. Tento přehled má požadavky. Další informace najdete v tématu [Přehled spolusprávy](../../../comanage/overview.md).<!-- D99F094A-A965-402F-AFE5-EE00CCAF0A12 -->

- **Zařízení neodeslaná do Azure AD**: od verze 2002 se v tomto přehledu zobrazí seznam zařízení, která lokalita neodeslala do Azure Active Directory (Azure AD), protože jste ji nenakonfigurovali pro protokol HTTPS.<!--6268489--> Nakonfigurujte [Rozšířený protokol HTTP](../../plan-design/hierarchy/enhanced-http.md)nebo povolte alespoň jeden bod správy pro protokol HTTPS. Pokud jste již lokalitu nakonfigurovali pro komunikaci pomocí protokolu HTTPS, tento přehled se nezobrazí.<!-- 609F03D4-D9B4-4D0D-A67F-9E365F6C0DD0 -->

- **Povolit bránu pro správu cloudu**: Brána pro správu cloudu (CMG) poskytuje jednoduchý způsob, jak spravovat Configuration Manager klientů přes Internet. Nasazením CMG jako cloudové služby v Microsoft Azure můžete dál spravovat a obsluhovat obsah klientům, kteří se přecházejí na Internet. V CMG není potřeba žádná další místní infrastruktura dostupná pro Internet. Další informace najdete v tématu [plánování pro CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md).<!-- 451B9B3A-D86A-4EF1-ACC3-FE6A207886BA -->

- **Povolit, aby zařízení byla připojená k hybridnímu Azure Active Directory**: zařízení připojená k Azure AD umožňují uživatelům přihlašovat se pomocí svých přihlašovacích údajů do domény a zajistit, aby zařízení splňovala standardy zabezpečení a dodržování předpisů v organizaci. Další informace najdete v tématu věnovaném [faktorům pro návrh hybridní identity Azure AD](https://docs.microsoft.com/azure/active-directory/hybrid/plan-hybrid-identity-design-considerations-overview).<!-- 6DC6B149-8B48-45E9-B189-F1E12A62D994 -->

- **Lokality, které nemají správnou konfiguraci protokolu HTTPS**: počínaje verzí 2002 se v tomto přehledu zobrazí seznam lokalit v hierarchii, které nejsou správně nakonfigurované pro protokol HTTPS. Tato konfigurace brání lokalitě v [synchronizaci výsledků členství kolekce do skupin Azure AD](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync). Může to způsobit, že synchronizace služby Azure AD nebude nahrávat všechna zařízení. Správa těchto klientů nemusí fungovat správně.<!--6268489--> Nakonfigurujte [Rozšířený protokol HTTP](../../plan-design/hierarchy/enhanced-http.md)nebo povolte alespoň jeden bod správy pro protokol HTTPS. Pokud jste již lokalitu nakonfigurovali pro komunikaci pomocí protokolu HTTPS, tento přehled se nezobrazí.<!-- 73884047-3395-430E-B971-F853806D4349 -->

- **Aktualizace klientů na nejnovější verzi Windows 10**: Windows 10, verze 1709 nebo vyšší zlepšuje a modernizes výpočetní prostředí vašich uživatelů. Další informace najdete v části [klíčové články o přijetí Windows jako služby](../../understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service).<!-- FD2C7B93-E5C6-4DCB-89AF-9EFCFCD01524 -->

### <a name="collections"></a>Kolekce

Přehledy, které zjednodušují správu tím, že čistí a mění konfiguraci kolekcí.

- **Prázdné kolekce**: vypíše kolekce v prostředí, které nemají žádné členy. Další informace najdete v tématu [Správa kolekcí](../../clients/manage/collections/manage-collections.md).<!-- 4266054A-695D-4BCA-8000-27BD32F7C006 -->

<!--3555752-->
- **Kolekce bez pravidel dotazů a přímých členů**: Chcete-li zjednodušit seznam kolekcí ve vaší hierarchii, odstraňte tyto kolekce.<!-- 3C234964-B3F3-49EE-AA13-048CD2021924 -->

- **Kolekce se stejným časem zahájení přehodnocení**: tyto kolekce mají stejný čas opětovného vyhodnocení jako jiné kolekce. Upravte čas opakovaného vyhodnocení, aby nedošlo ke konfliktu.<!-- A85B79A6-BA81-404F-8DA4-DD7C87582CCD -->

- **Kolekce s časem dotazu za 5 minut**: Zkontrolujte pravidla dotazu pro tuto kolekci. Zvažte úpravu nebo odstranění kolekce.<!-- 6AF42536-BDF4-4535-87C1-535AE1B813DA -->

- Následující přehledy obsahují konfigurace, které potenciálně způsobují zbytečné zatížení webu. Zkontrolujte tyto kolekce, pak je buď odstraňte, nebo zakažte vyhodnocování pravidel shromažďování:

  - **Kolekce bez povolených pravidel dotazů a přírůstkových aktualizací**<!-- 6A4845AB-6D2C-4F2A-B7AB-EC77C81FD571 -->

  - **Kolekce bez pravidel dotazů a povolených pro libovolný plán**<!-- 219B9C45-BD02-4E7E-A29D-B66094366200 -->

  - **Kolekce bez pravidel dotazů a plánovaného úplného vyhodnocení**<!-- 8A401207-5A7C-4200-A1DB-990A197458FA -->

### <a name="configuration-manager-assessment"></a>Posouzení Configuration Manager

<!--3607758-->

Od verze 2002 se tato skupina nepoužívá v oblasti technické podpory Microsoft Premier. Tyto přehledy jsou ukázkou mnoha dalších kontrol, které Microsoft Premier nabízí v [centru služeb](https://docs.microsoft.com/services-hub/health/getting_started_with_on_demand_assessments).

- **Zjišťování skupiny zabezpečení služby Active Directory je nakonfigurované tak, aby se spouštělo příliš často**: obvykle není potřeba konfigurovat zjišťování skupin zabezpečení služby Active Directory tak, aby probíhalo častěji než v každé tři hodiny. Častější konfigurace může mít negativní dopad na výkon služby Active Directory, sítě a Configuration Manager. Místo použití úplného plánu synchronizace povolte přírůstkovou synchronizaci. Další informace najdete v tématu [zjišťování skupin služby Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutGroup).<!-- 4E739B65-AEC9-4B1D-8B36-AC6AC4A72022 -->

- **Zjišťování systémových souborů služby Active Directory je nakonfigurováno tak, aby běželo příliš často**: nemusíte obvykle konfigurovat zjišťování systému služby Active Directory tak, aby probíhalo častěji než každé tři hodiny. Častější konfigurace může mít negativní dopad na výkon služby Active Directory, sítě a Configuration Manager. Místo použití úplného plánu synchronizace povolte přírůstkovou synchronizaci. Další informace najdete v tématu [zjišťování systémových informací služby Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutSystem).<!-- 353CAFBC-AC90-4FD3-B3CF-51D6D9FB376C -->

- **Zjišťování uživatelů služby Active Directory je nakonfigurováno tak, aby běželo příliš často**: nemusíte obvykle konfigurovat zjišťování uživatelů služby Active Directory tak, aby probíhalo častěji než každé tři hodiny. Častější konfigurace může mít negativní dopad na výkon služby Active Directory, sítě a Configuration Manager. Místo použití úplného plánu synchronizace povolte přírůstkovou synchronizaci. Další informace najdete v tématu [zjišťování uživatelů služby Active Directory](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).<!-- 2E742924-7319-4013-B1E1-97DE7EB16B74 -->

- **Kolekce omezené na všechny systémy nebo všechny uživatele**: Projděte si všechny kolekce, které používají kolekce **všechny systémy** nebo **Všichni uživatelé** jako omezení kolekce. Configuration Manager aktualizuje členství těchto výchozích kolekcí s daty z metod zjišťování služby Active Directory. Tato data nemusí být platná informace pro klienty Configuration Manager.<!-- 2382F0C9-A36D-4079-AB37-E3D8EE47E8D4 -->

- **Zjišťování prezenčního signálu je zakázané**: zjišťování prezenčního signálu vyžaduje, abyste na zařízení nainstalovali klienta Configuration Manager. Je to jediná metoda zjišťování, kterou klienti spouštějí. Všechny ostatní metody se vyskytují na serverech lokality. Zjišťování prezenčního signálu je nezbytné pro udržení stavu aktivity klienta v aktuálním stavu. Tím se zajistí, že lokalita nebude náhodně vymezit záznamy o prostředcích z databáze lokality. Další informace najdete v tématu [zjišťování prezenčního signálu](../deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).<!-- A3089798-DF4E-490A-AF78-4AF474B214CF -->

- **Dlouhotrvající dotazy na kolekci povolené pro přírůstkové aktualizace**: kolekce s časem poslední přírůstkové aktualizace delší než 30 sekund používají server lokality a databázové prostředky, což může potenciálně ovlivnit celkový Configuration Manager výkon. Další informace najdete v tématu [osvědčené postupy pro kolekce](../../clients/manage/collections/best-practices-for-collections.md).<!-- 21F14C0E-008B-47F3-B1E2-19CF79DC97B4 -->

- **Snižte počet aplikací a balíčků v distribučních bodech**: Společnost Microsoft oficiálně podporuje kombinovaný součet až 10 000 balíčků a aplikací v distribučním bodě. Překročení tohoto celkového množství může vést k provozním problémům. Další informace naleznete v tématu [size and Scale Numbers-Distribution Point](../../plan-design/configs/size-and-scale-numbers.md#distribution-point).<!-- FFE6906E-932E-4927-8EE0-BA25C37943CB -->

- **Problémy při instalaci sekundárního webového serveru**: stav instalace některých sekundárních lokalit **čeká na vyřízení** nebo **selhal**. Tato stavová skutečnost znamená, že jste spustili instalaci, ale ta se nedokončila úspěšně. Až se instalace sekundární lokality dokončí, klienti nemusí správně komunikovat s primární lokalitou. Ověřte pracovní prostor **monitorování** a zkuste instalaci zopakovat. Další informace najdete v tématu [opakování instalace aktualizace, která se nezdařila](install-in-console-updates.md#bkmk_retry).<!-- ED3F5BDD-2F02-44A4-87F4-BB2C1032D4DE -->

- **Aktualizovat všechny lokality na stejnou verzi**: použijte stejnou verzi Configuration Manager v hierarchii. Tato konfigurace zajišťuje, že všechny lokality poskytují stejné funkce. Lokality různých verzí ve stejné hierarchii představují scénáře interoperability. Novější verze Configuration Manager zahrnují nové funkce a řeší známé problémy. Další informace najdete v tématu [vzájemná funkční spolupráce mezi různými verzemi](../../plan-design/hierarchy/interoperability-between-different-versions.md).<!-- 88C630A5-6D6B-4DDB-95D7-78E12107970D -->

Další informace o těchto přehledech najdete v tématu [opravné kroky pro Configuration Manager přehledy správy](https://docs.microsoft.com/services-hub/health/remediation-steps-configmgr).

> [!TIP]
> Pokud už jste zákazníkem Microsoft Unified nebo Microsoft Premier, přihlaste se k [centru služeb](https://serviceshub.microsoft.com/assessments/) , kde najdete další posouzení na vyžádání.
>
> Další informace o službách Microsoftu najdete v tématu [Podpora řešení](https://www.microsoft.com/enterprise/services/support).

### <a name="operating-system-deployment"></a>Nasazení operačního systému

<!--6982275-->

Od verze 2006 vám následující přehledy správy pomůžou spravovat velikost zásad pořadí úkolů. Když velikost zásad pořadí úkolů překročí 32 MB, klient nedokáže zpracovat velkou zásadu. Klient pak nemůže spustit nasazení pořadí úloh.

- **Velká pořadí úkolů mohou přispět k překročení maximální velikosti zásad**: Pokud nasadíte tato pořadí úkolů, klienti nebudou moci zpracovat velké objekty zásad. Zmenšete velikost zásady pořadí úkolů, aby nedocházelo k potenciálním problémům při zpracování zásad.<!-- D9A15248-832E-4780-8151-ACD1B9E53FE1 -->

- **Celková velikost zásad pro pořadí úloh překračuje limit zásad**: klienti nemůžou zpracovat zásady pro tato pořadí úloh, protože je moc velká. Zmenšete velikost zásady pořadí úkolů, aby bylo možné spustit nasazení na klientech.<!-- 6568F6A3-D1D8-4E63-940B-FE44F8349802 -->

Další informace najdete v tématu [zmenšení velikosti zásad pořadí úkolů](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_policysize).

Ve verzi 2006 se následující přehled přesunul do této skupiny z proaktivní skupiny pro **údržbu** :

- **Nepoužívané spouštěcí bitové kopie**: spouštěcí bitové kopie neodkazují na spouštění pomocí technologie PXE nebo použití pořadí úloh. Další informace najdete v tématu [Správa spouštěcích imagí](../../../osd/get-started/manage-boot-images.md).<!-- 4C1FBA51-AD56-4CA8-8326-066F65D24F0E -->

### <a name="optimize-for-remote-workers"></a>Optimalizovat pro vzdálené pracovníky

<!--6982226-->

Počínaje verzí 2006 vám následující přehledy pomůžou vytvořit lepší prostředí pro vzdálené pracovníky a snížit zatížení vaší infrastruktury:

- **Nakonfigurovat klienty připojené k síti VPN k preferovat cloudové zdroje obsahu**: Pokud chcete snížit zatížení sítě VPN, povolte možnost skupiny hranic, která **upřednostňuje cloudové zdroje přes místní zdroje**. Tato možnost umožňuje klientům stahovat obsah z Internetu místo distribučních bodů napříč sítí VPN. Další informace najdete v tématu [Možnosti skupiny hranic](../deploy/configure/boundary-groups.md#bkmk_bgoptions4).<!-- 1BFD7A7A-077C-4E8A-9EAA-4559E41D400A -->

- **Definování skupin hranic sítě VPN**: vytvořte hranici sítě VPN a přidružte ji ke skupině hranic. Přidružte systémy lokality specifické pro síť VPN ke skupině a nakonfigurujte nastavení pro vaše prostředí. Tento přehled zkontroluje aspoň jednu skupinu hranic, která má alespoň jednu hranici sítě VPN. Z vlastností tohoto přehledu vyberte **zkontrolovat akce** a přejdete na uzel **skupiny hranic** . Další informace najdete v tématu [typ hranice sítě VPN](../deploy/configure/boundaries.md#vpn).<!-- E44BF0CC-0ADA-4B00-A4DF-4005256DF73E -->

- **Zakázat sdílení obsahu peer-to-peer pro klienty připojené k síti VPN**: Pokud chcete zabránit zbytečným přenosům peer-to-peer, které by nejspíš nevyužily vzdálené klienty, zakažte možnost skupiny hranic, aby **bylo možné v této skupině hranic povolit stahování**. Další informace najdete v tématu [Možnosti skupiny hranic](../deploy/configure/boundary-groups.md#bkmk_bgoptions1).<!-- 60404B23-96A9-4EE2-B8D6-1F226C2F2F5A -->

### <a name="proactive-maintenance"></a>Proaktivní údržba

<!--1352184-->
Přehledy v této skupině zvýrazňují možné problémy s konfigurací, abyste se vyhnuli udržováním Configuration Manager objektů.

- **Hraniční skupiny bez přiřazených systémů lokality**: bez přiřazených systémů lokality lze skupiny hranic použít pouze pro přiřazení lokality. Další informace najdete v tématu [Konfigurace skupin hranic](../deploy/configure/boundary-groups.md).<!-- 01E5A4BC-0E31-494E-A553-2B32C410FA5B -->

- **Skupiny hranic bez členů**: skupiny hranic nejsou použitelné pro přiřazení lokality nebo vyhledávání obsahu, pokud nemají žádné členy. Další informace najdete v tématu [Konfigurace skupin hranic](../deploy/configure/boundary-groups.md).<!-- 4f0d37b1-f979-4ba3-b15b-7fe3c915f239 -->

- **Distribuční body, které neobsluhují obsah pro klienty**: distribuční body, které klientům za posledních 30 dní nesloužili obsahu. Tato data jsou založená na sestavách od klientů jejich historie stahování. Další informace najdete v tématu [instalace a konfigurace distribučních bodů](../deploy/configure/install-and-configure-distribution-points.md).<!-- 9A115092-F8D4-4AB7-B846-C09143B9B9B0 -->

- **Povolit službu WSUS Cleanup**: ověřuje, že jste povolili možnost spustit čištění služby WSUS ve vlastnostech komponenty bodu aktualizace softwaru. Tato možnost pomáhá zlepšit výkon služby WSUS. Další informace najdete v tématu [Údržba aktualizací softwaru](../../../sum/deploy-use/software-updates-maintenance.md).<!-- D43080F1-FE98-4F24-94ED-FEB1C2DDEF50 -->

- **Nepoužité položky konfigurace**: položky konfigurace, které nejsou součástí standardních hodnot konfigurace a jsou starší než 30 dní. Další informace najdete v tématu [Vytvoření standardních hodnot konfigurace](../../../compliance/deploy-use/create-configuration-baselines.md).<!-- 0597907B-17D4-4EA5-92E4-CCE692E1468D -->

- **Upgradujte zdroje sdílené mezipaměti na nejnovější verzi Configuration Manager klienta**:<!--1358008--> Identifikujte klienty, kteří slouží jako zdroj sdílené mezipaměti, ale nebyly upgradováni z verze klienta starší než 1806. Klienty starších než 1806 nelze použít jako zdroj sdílené mezipaměti pro klienty, kteří používají verzi 1806 nebo novější. Výběrem možnosti **provést akci** otevřete zobrazení zařízení, které zobrazí seznam klientů.<!-- B51C6733-F9FF-46BC-8F5E-624F2CBED719 -->

> [!TIP]
> Ve verzi 2006 se přehled pro **nepoužívané spouštěcí image** přesunul do nové skupiny [nasazení operačního systému](#operating-system-deployment) .

### <a name="security"></a>Zabezpečení

Přehledy pro zlepšení zabezpečení infrastruktury a zařízení.

- **Je povolená záloha protokolu NTLM**:<!--4572953--> Počínaje verzí 1906 tento Insight zjistí, jestli jste u lokality povolili metodu Fallback pro použití méně zabezpečeného ověřování NTLM. Při použití metody push klienta pro instalaci klienta Configuration Manager může lokalita vyžadovat vzájemné ověřování protokolem Kerberos. Toto vylepšení pomáhá zabezpečit komunikaci mezi serverem a klientem. Další informace najdete v tématu [instalace klientů pomocí klientské nabízené instalace](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).<!-- C16C6826-8209-47A9-BA71-14A8C83E4C35 -->

- **Nepodporované verze antimalwarového klienta**: na více než 10% klientů běží verze Endpoint Protection System Center, které se nepodporují. Další informace najdete v tématu [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).<!-- ACD63321-CF15-4CDD-B1A3-69005887C633 -->

### <a name="simplified-management"></a>Zjednodušená správa

Přehledy, které vám pomůžou zjednodušit každodenní správu vašeho prostředí.

- **Připojení lokality k Microsoft cloudu pro Configuration Manager aktualizace**: Tento přehled zajišťuje, že se váš spojovací bod služby Configuration Manager v posledních sedmi dnech připojil ke cloudu Microsoftu. Toto připojení umožňuje stahovat obsah pro pravidelné aktualizace. Zkontrolujte protokol DMPDownloader. log a hman. log. Další informace najdete v tématu [požadavky na přístup k Internetu](../../plan-design/network/internet-endpoints.md#bkmk_scp-updates).<!-- AC662C91-54DF-4B43-B09A-B19D2766144B -->

- **Verze klientů nepatřících k síti pro vyžádání**: zobrazí seznam všech klientů, jejichž verze není sestavením aktuální větve. Další informace najdete v tématu [upgrade klientů](../../clients/manage/upgrade/upgrade-clients.md).<!-- 450090EA-DF71-428C-AB49-6DEBB85A004C -->

- **Aktualizace klientů na podporovanou verzi Windows 10**:<!--3897268--> Tento Insight se sestavuje na klientech, na kterých běží verze Windows 10, která už není podporovaná. Zahrnuje taky klienty s verzí Windows 10, která se blíží konci služby (tři měsíce).<!-- 560669D6-1756-4814-9505-C54BDB4930D0 -->

### <a name="software-center"></a>Centrum softwaru

Přehledy pro správu centra softwaru

- **Směrování uživatelů do centra softwaru namísto katalogu aplikací**: Ověřte, zda uživatelé v posledních 14 dnech nainstalovali nebo požadovali aplikace z katalogu aplikací. Hlavní funkce katalogu aplikací je teď součástí centra softwaru. Podpora končí pro role katalogu aplikací s verzí 1910. Další informace najdete v tématu [zastaralé funkce](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).<!-- DB9E65CF-C59C-4B76-B6A0-ADB95D809246 -->

- **Používat novou verzi centra softwaru**: předchozí verze centra softwaru už není podporovaná. Nastavte klienty na použití nového centra softwaru tak, že povolíte nastavení klienta **použít nové centrum softwaru** ve skupině **Počítačový agent** . Další informace najdete v tématu [informace o nastavení klienta](../../clients/deploy/about-client-settings.md#use-new-software-center).<!-- A9BCA10D-834F-4F39-89F5-CDCCE8F80C56 -->

### <a name="software-updates"></a>Aktualizace softwaru

- **Nastavení klienta není nakonfigurováno tak, aby umožňovalo klientům stahovat rozdílový obsah**: některé aktualizace softwaru synchronizované ve vašem prostředí zahrnují rozdílový obsah. Povolte nastavení klienta **Povolit klientům stahování rozdílových obsahu, pokud je k dispozici**. Pokud toto nastavení nepovolíte, bude klient při nasazení těchto aktualizací zbytečně stahovat více obsahu, než potřebují. Další informace najdete v tématu [nastavení klienta – aktualizace softwaru](../../clients/deploy/about-client-settings.md#software-updates).<!-- 3E2E9E10-1CDC-47E3-BFC9-3A46AB7FE1BD -->

- **Povolit kategorii produktů aktualizace softwaru ' Windows 10, verze 1903 a novější '**: pro Windows 10, verze 1903 a novější je k dispozici nová kategorie produktů aktualizace softwaru. Pokud synchronizujete aktualizace Windows 10 a máte klienty se systémem Windows 10, verze 1903 nebo novější, vyberte ve vlastnostech komponenty bodu aktualizace softwaru kategorii produktů **Windows 10, verze 1903 a novější** . Další informace najdete v tématu[Konfigurace klasifikací a produktů k synchronizaci](../../../sum/get-started/configure-classifications-and-products.md).<!-- 16B1152D-6511-4DC7-824E-539B2597F9B0 -->

### <a name="windows-10"></a>Windows 10

Přehledy související s nasazením a obsluhou Windows 10 Skupina Windows 10 Management Insights je dostupná jenom v případě, že na víc než polovinu klientů běží Windows 7, Windows 8 nebo Windows 8.1.

- **Konfigurace diagnostických dat Windows a klíče komerčního ID**: Pokud chcete používat data z Desktop Analytics, nakonfigurujte zařízení pomocí kódu komerčního ID a povolte shromažďování diagnostických dat. Nastavte zařízení s Windows 10 na úroveň **Rozšířené (omezené)** nebo vyšší. Další informace najdete v tématu [Povolení sdílení dat pro desktopovou analýzu](../../../desktop-analytics/enable-data-sharing.md).<!-- B224393F-B255-4C80-A1D1-1014BE1DC7D4 -->
