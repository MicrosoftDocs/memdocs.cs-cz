---
title: Archiv novinek v klasickém portálu Microsoft Intune
description: Archivovaná oznámení novinek v Microsoft Intune
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/08/2017
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ed2db991-4729-49a7-a1e6-be2ffa0d03d1
ROBOTS: noindex,nofollow
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: edc5cd2926f85ebf2f81d681646be7973e6ba444
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79330059"
---
# <a name="whats-new-in-the-intune-classic-portal---previous-months"></a>Co je nového na klasickém portálu Intune – předchozí měsíce

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

Tato stránka obsahuje seznam nových funkcí a oznámení dříve zveřejněných na [stránce novinek](whats-new.md) pro klasický portál Intune.

## <a name="april-2017"></a>Duben 2017

### <a name="new-capabilities"></a>Nové funkce

#### <a name="myapps-available-for-managed-browser---822308-822303--"></a>Aplikace MyApp k dispozici pro Managed Browser <!--822308, 822303-->

Microsoft MyApps teď mají lepší podporu v Managed Browseru. Uživatelé Managed Browseru, kteří nejsou cílem správy, budou přeneseni rovnou do služby MyApps, kde mají přístup k aplikacím SaaS, které jim zajistil správce. Uživatelé, kteří jsou cílem správy Intune, budou mít k MyApps dál přístup z integrované záložky Managed Browseru.

#### <a name="new-icons-for-the-managed-browser-and-the-company-portal---918433-918431-971473--"></a>Nové ikony pro Managed Browser a Portál společnosti <!--918433, 918431, 971473-->

Managed Browser dostal aktualizované ikony pro verze aplikace pro Android i iOS. Nová ikona bude obsahovat aktualizovaný odznak Intune, aby byla konzistentnější s ostatními aplikacemi v Enterprise Mobility + Security (EM+S). Novou ikonu pro Managed Browser uvidíte na [stránce s novinkami v uživatelském rozhraní aplikace Intune](whats-new-app-ui.md).

Portál společnosti také dostal aktualizované ikony pro verze aplikace pro Android, iOS i Windows, aby byly konzistentnější s ostatními aplikacemi v EM+S. Tyto ikony se budou postupně vydávat pro všechny platformy od dubna do konce května.

#### <a name="sign-in-progress-indicator-in-android-company-portal---953374--"></a>Indikátor průběhu přihlašování v Androidu Portál společnosti <!--953374-->

Aktualizace aplikace Portál společnosti pro Android zobrazuje indikátor průběhu přihlášení, když uživatel aplikaci spustí nebo pokračuje v jejím používání. Než uživatel získá přístup k aplikaci, indikátor postupně zobrazuje nové stavy od „Připojování...“ přes „Přihlašování...“ po „Kontrolují se požadavky na zabezpečení...“. Nové obrazovky pro aplikaci Portál společnosti pro Android uvidíte na [stránce s novinkami v uživatelském rozhraní aplikace Intune](whats-new-app-ui.md).

#### <a name="block-apps-from-accessing-sharepoint-online----679339---"></a>Zablokovat aplikacím přístup k SharePointu Online <!-- 679339 -->

Teď můžete vytvořit zásadu podmíněného přístupu na základě aplikace, která bude blokovat aplikace, které pro ně nepoužívají zásady ochrany aplikací, a to od přístupu k [SharePointu Online](../protect/app-based-conditional-access-intune-create.md). V případě podmíněného přístupu založeného na aplikacích můžete určit aplikace, které mají mít přístup k SharePointu Online, pomocí Azure Portal.

#### <a name="single-sign-on-support-from-the-company-portal-for-ios-to-outlook-for-ios---834012--"></a>Podpora jednotného přihlašování z Portál společnosti pro iOS do Outlooku pro iOS <!--834012-->
Uživatelé už se nemusí přihlašovat k aplikaci Outlook, pokud jsou na stejném zařízení pomocí stejného účtu přihlášení k aplikaci Portál společnosti pro iOS. Při spuštění aplikace Outlook budou uživatelé moct zvolit svůj účet a přihlásit se automaticky. Pracujeme také na tom, abychom tuto funkci přidali i pro další aplikace Microsoftu.

#### <a name="improved-status-messaging-in-the-company-portal-app-for-ios---744866--"></a>Vylepšené zasílání zpráv o stavu v aplikaci Portál společnosti pro iOS <!--744866-->
V aplikaci Portál společnosti pro iOS se teď budou zobrazovat nové a konkrétnější chybové zprávy poskytující přístupnější informace o tom, co se děje na zařízeních. Tyto případy chyb byly dříve součástí obecné chybové zprávy s názvem „Portál společnosti dočasně nedostupný“. Kromě toho, pokud uživatel aplikaci Portál společnosti spustí v iOSu, když chybí připojení k internetu, uvidí teď na domovské stránce trvalý stavový řádek s oznámením o tom, že chybí připojení k internetu.

#### <a name="improved-app-install-status-for-the-windows-10-company-portal-app---676495--"></a>Vylepšený stav instalace aplikace pro Portál společnosti aplikaci pro Windows 10 <!--676495-->

Nová vylepšení pro instalaci aplikace spuštěna v aplikaci portál společnosti pro Windows 10 patří:
- Rychlejší generování sestav o průběhu instalace pro balíčky MSI
- Rychlejší generování sestav o průběhu instalace pro moderní aplikace na zařízeních s Windows 10 Anniversary Update a novějšími verzemi
- Nový indikátor průběhu pro všechny instalace moderních aplikací na zařízeních s Windows 10 Anniversary Update a novějšími verzemi

Nový indikátor průběhu najdete na stránce[Co je nového v uživatelském rozhraní aplikací Intune](whats-new-app-ui.md).

#### <a name="bulk-enroll-windows-10-devices----747607---"></a>Hromadná registrace zařízení s Windows 10 <!-- 747607 -->

K Azure Active Directory a Intune můžete teď pomocí Windows Configuration Designeru (WCD) připojit velký počet zařízení s Windows 10 Creators Updatem. Pokud chcete pro svého tenanta Azure AD povolit [hromadnou registraci MDM](../enrollment/windows-bulk-enroll.md), vytvořte zřizovací balíček, který zařízení k tenantovi Azure AD připojí pomocí Windows Configuration Designeru, a použijte balíček na zařízení ve vlastnictví firmy, která chcete hromadně zaregistrovat a spravovat. Po použití balíčku se zařízení připojí k Azure AD, zaregistrují v Intune a jsou připravená na přihlašování vašich uživatelů z Azure AD.  Uživatelé Azure AD jsou na těchto zařízeních standardními uživateli a obdrží přiřazené zásady a požadované aplikace. Samoobslužné scénáře a scénáře s Portálem společnosti v současnosti nejsou podporované.

### <a name="whats-new-in-the-public-preview-of-intune-in-the-azure-portal--736542--"></a>Co je nového ve verzi Public Preview služby Intune v Azure Portal<!--736542-->

V rané kalendářním roce 2017 budeme migrovat naše ucelené prostředí pro správu do Azure, které umožňuje výkonnou a integrovanou správu základních pracovních postupů EMS na moderní platformě služby, která je rozšiřitelná pomocí rozhraní Graph API.

Noví zkušební tenanti se začnou objevovat ve veřejné verzi Preview nového prostředí pro správu na webu Azure Portal tento měsíc. Funkce a parita se stávající konzolou Intune se ve verzi Preview budou zavádět postupně.

Prostředí pro správu na webu Azure Portal bude využívat nové funkce seskupování a cílení, které už byly oznámeny. Při migraci vašeho stávajícího tenanta do nového prostředí seskupování se provede také vaše migrace do verze Preview nového prostředí pro správu vašeho tenanta. Pokud si chcete otestovat nebo prohlédnout některé nové funkce ještě před migrací vašeho tenanta, zaregistrujte si nový zkušební účet Intune nebo se podívejte na [novou dokumentaci](whats-new.md).

Novinky ve verzi Intune v Azure najdete [zde](whats-new.md).

### <a name="notices"></a>Oznámení

#### <a name="direct-access-to-apple-enrollment-scenarios---951869--"></a>Přímý přístup ke scénářům registrace Apple <!--951869-->

U účtů Intune vytvořených po lednu 2017 umožňuje Intune přímý přístup ke scénářům registrace Apple pomocí úlohy Registrovat zařízení na portálu Azure Preview. Náhled na registraci Apple byl předtím přístupný jen přes odkazy na Azure Portalu. Zpřístupnění těchto funkcí v Azure bude u účtů Intune vytvořených před lednem 2017 vyžadovat jednorázovou migraci. Plán této migrace zatím nebyl oznámen, podrobnosti ale budou zpřístupněny co nejdříve. Pokud váš existující účet nemá k tomuto náhledu přístup, k otestování tohoto nového prostředí důrazně doporučujeme vytvořit zkušební účet.

#### <a name="whats-coming-for-appx-in-intune-in-the-azure-portal----1000270---"></a>Co přichází pro appx v Intune v Azure Portal <!-- 1000270 -->

Součástí migrace na Intune na Azure Portalu jsou tři změny appx:

1. Přidání nového typu aplikace appx v konzole Intune, který se dá nasadit jenom na zařízení zaregistrovaná v MDM
2. Změna účelu stávajícího typu aplikace appx, aby byl zacílený jenom na počítače PC spravované pomocí agenta Intune pro počítače PC
3. Převedení všech stávajících appx na appx MDM v rámci migrace

##### <a name="how-does-this-affect-me"></a>Co to pro mě znamená?

Nebude to mít vliv na žádné z vašich stávajících nasazení do zařízení spravovaných pomocí agenta Intune pro počítače PC. Po migraci ale nebudete moct tyto migrované appx nasadit do žádných nových zařízení spravovaných pomocí agenta Intune pro počítače PC, pokud na ně předtím nebylo zacíleno.

##### <a name="what-action-do-i-need-to-take"></a>Co musím udělat

Pokud budete chtít provést nová nasazení do počítačů PC, budete muset po migraci znovu nahrát appx jako appx pro počítače PC. Další informace najdete v článku o [změnách Appx v Intune na Azure Portalu](https://aka.ms/appxchange) na blogu týmu podpory Intune.  

#### <a name="administration-roles-being-replaced-in-azure-portal"></a>Nahrazení rolí správy na portálu Azure Portal

Existující role pro správu mobilních aplikací (MAM) (Přispěvatel, Vlastník a Jen pro čtení) používané v klasickém portálu Intune (Silverlight) byly na portálu Azure Portal pro Intune nahrazeny celou řadou nových možností řízení přístupu na základě role (RBAC). Jakmile migrujete na portál Azure Portal, bude potřeba, abyste svým správcům přiřadili tyto nové role správy. Další informace o RBAC a nových rolích najdete v článku [Řízení přístupu na základě role pro Microsoft Intune](role-based-access-control.md).

### <a name="whats-coming"></a>Co připravujeme

#### <a name="improved-sign-in-experience-across-company-portal-apps-for-all-platforms---user-story-1132123--"></a>Vylepšené přihlašování napříč Portál společnosti aplikacemi pro všechny platformy <!--User Story 1132123-->

Avizujeme změnu, kterou uvedeme během několika nadcházejících měsíců a která vylepší přihlašování k aplikacím Portál společnosti Intune v systémech Android, iOS a Windows. Nové uživatelské prostředí se automaticky zobrazí na všech platformách pro aplikaci Portál společnosti, až Azure AD tuto změnu provede. Kromě toho se teď uživatelé můžou k Portálu společnosti přihlašovat z jiného zařízení pomocí vygenerovaného kódu na jedno použití. To se hodí hlavně v případech, kdy se uživatelé potřebují přihlásit bez přihlašovacích údajů.

Snímky obrazovky předchozího způsobu přihlašování, nového způsobu přihlašování zadáním přihlašovacích údajů a nového způsobu přihlašování z jiného zařízení najdete na stránce [novinek v uživatelském rozhraní aplikací](whats-new-app-ui.md).

#### <a name="plan-for-change-intune-is-changing-the-intune-partner-portal-experience----1050016---"></a>Plánování změn: Intune mění prostředí portálu pro partnery Intune. <!-- 1050016 -->

Počínaje aktualizací služby v polovině května 2017 odstraníme stránku Intune Partner z manage.microsoft.com.  

Pokud jste partnerským správcem, nebude už moct stránku Intune Partner zobrazit a provádět z ní jménem vašich zákazníků kroky, ale místo toho se budete muset přihlásit k jednomu ze dvou dalších partnerských portálů Microsoftu.

[Partnerské centrum Microsoftu](https://partnercenter.microsoft.com/) i [centrum pro správu Microsoft 365](https://admin.microsoft.com/) vám umožní přihlašovat se k účtům zákazníků, které spravujete. V budoucnu jako partneři prosím ke správě svých zákazníků používejte jeden z těchto webů.


#### <a name="apple-to-require-updates-for-application-transport-security---748318--"></a>Apple pro vyžadování aktualizací pro zabezpečení přenosu aplikací <!--748318-->

Apple oznámil, že začne vynucovat specifické požadavky na ATS (Application Transport Security). ATS slouží k vynucení vyššího zabezpečení veškeré komunikace aplikací přes protokol HTTPS. Tato změna ovlivní zákazníky Intune, kteří používají aplikace Portál společnosti pro iOS.

Prostřednictvím programu Apple TestFlight, který vynucuje nové požadavky na ATS, jsme zpřístupnili verzi aplikace Portál společnosti pro iOS. Pokud si ji chcete vyzkoušet a otestovat, jestli ATS dodržujete, napište nám na adresu <a href="mailto:CompanyPortalBeta@microsoft.com?subject=Register to TestFlight ATS Company Portal app">CompanyPortalBeta@microsoft.com</a> zprávu s vaším jménem a příjmením, e-mailovou adresou a názvem společnosti. Další podrobnosti najdete v [blogu podpory služby Intune](https://aka.ms/compportalats).

## <a name="march-2017"></a>Březen 2017

### <a name="new-capabilities"></a>Nové funkce

#### <a name="support-for-skycure"></a>Podpora aplikace Skycure

Přístup mobilních zařízení k podnikovým prostředkům teď můžete řídit pomocí podmíněného přístupu na základě posouzení rizik, které provádí Skycure, řešení ochrany před mobilními hrozbami, které se integruje s Microsoft Intune. Riziko se posuzuje na základě telemetrie, která se shromažďuje ze zařízení, na kterých běží služba Skycure. Patří do ní:

- Fyzická ochrana
- Síťová ochrana
- Ochrana aplikací
- Ochrana chyb zabezpečení

Pomocí zásad dodržování předpisů zařízením v Intune můžete nakonfigurovat zásady podmíněného přístupu EMS na základě posouzení rizik v rámci Symantec Endpoint Protection Mobile (Skycure). Tyto zásady můžete použít k povolení nebo blokování přístupu zařízení nesplňujících požadavky k podnikovým prostředkům na základě zjištěných hrozeb. Další informace najdete v tématu [Symantec Endpoint Protection Mobile Connector](../protect/skycure-mobile-threat-defense-connector.md).

#### <a name="new-user-experience-for-the-company-portal-app-for-android---621622--"></a>Nové uživatelské prostředí pro aplikaci Portál společnosti pro Android <!--621622-->

Kvůli modernějšímu vzhledu a chování a lepšímu uživatelskému prostředí bude aktualizováno uživatelské rozhraní aplikace Portál společnosti pro Android. K významným aktualizacím patří:

- Barvy: IT oddělení může v záhlaví karet aplikace Portál společnosti definovat firemní barvy.
- Aplikace: Na kartě **Aplikace** jsou aktualizovaná tlačítka **Vybrané aplikace** a **Všechny aplikace**.
- Hledání: Na kartě **Aplikace** má tlačítko **Hledat** podobu plovoucího tlačítka akce.
- Navigace mezi aplikacemi: Zobrazení **Všechny aplikace** obsahuje karty **Doporučené**, **Vše** a **Kategorie**, které zjednodušují navigaci.
- Podpora: Karty **Moje zařízení** a **Kontaktovat IT** jsou aktualizované tak, aby byly zřetelnější.

Další podrobnosti o těchto změnách najdete v článku [Aktualizace uživatelského rozhraní pro aplikace Intune pro koncové uživatele](whats-new-app-ui.md).

#### <a name="non-managed-devices-can-access-assigned-apps---664691--"></a>Nespravovaná zařízení mají přístup k přiřazeným aplikacím. <!--664691-->

Jako součást změn v návrhu na webu Portál společnosti budou moci uživatelé iOSu a Androidu na svoje nespravovaná zařízení instalovat aplikace, které mají přiřazené jako dostupné bez registrace. S použitím přihlašovacích údajů pro Intune se budou moct uživatelé přihlásit na web Portál společnosti a zobrazit seznam aplikací, které mají přiřazené. Balíčky aplikací, které jsou dostupné bez registrace, jsou k dispozici ke stažení prostřednictvím webu Portál společnosti. Aplikace, které vyžadují registraci, aby je bylo možné nainstalovat, nejsou touto změnou ovlivněny, protože když budou chtít tyto aplikace uživatelé nainstalovat, zobrazí se jim výzva k registraci.

#### <a name="signing-script-for-windows-10-company-portal---941642--"></a>Podpisový skript pro Windows 10 Portál společnosti <!--941642-->

Pokud potřebujete stáhnout aplikaci Portál společnosti pro Windows 10 a nainstalovat ji bokem, můžete použít skript, který zjednoduší a zefektivní proces podepisování aplikací ve vaší organizaci.   Informace o tom, jak tento skript stáhnout, a pokyny k jeho použití najdete v článku [Microsoft Intune Signing Script for Windows 10 Company Portal](https://aka.ms/win10cpscript) (Podepisovací skript Microsoft Intune pro Portál společnosti pro Windows 10) na webu TechNet. Další podrobnosti o tomto oznámení najdete v článku [Updating your Windows 10 Company Portal app](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) (Aktualizace aplikace Portál společnosti pro Windows 10) na blogu týmu podpory Intune.


### <a name="notices"></a>Oznámení

#### <a name="support-for-ios-103"></a>Podpora pro iOS 10.3

Uživatelé iOSu mají k dispozici verzi iOS 10.3 od 27. března 2017. Všechny stávající scénáře Intune MDM a MAM jsou kompatibilní s nejnovější verzí operačního systému od společnosti Apple. Předpokládáme, že všechny existující funkce Intune aktuálně dostupné pro správu zařízení s iOSem budou v zařízeních a aplikacích uživatelů nadále fungovat, i když si iOS upgradují na iOS 10.3.

V současnosti nejsou známy žádné problémy. Pokud se vyskytne problém s iOSem 10.3, kontaktujte prosím [tým podpory Intune](get-support.md).

#### <a name="improved-support-for-android-users-based-in-china---720444--"></a>Vylepšená podpora pro uživatele Androidu založená na Číně <!--720444-->

Vzhledem k absenci obchodu Google Play v Číně musí zařízení s Androidem získávat aplikace z čínských obchodů. Portál společnosti bude tuto situaci podporovat tím, že uživatele Androidu v Číně přesměruje na stažení aplikací Portál společnosti a Outlook z místních obchodů s aplikacemi. Tato změna vylepší uživatelské prostředí při povolených zásadách podmíněného přístupu, a to jak při správě mobilních zařízení, tak při správě mobilních aplikací. Aplikace Portál společnosti a Outlook pro Android jsou dostupné v následujících čínských obchodech s aplikacemi:

- [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
- [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
- [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
- [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

#### <a name="best-practice-make-sure-your-company-portal-apps-are-up-to-date---879465--"></a>Osvědčený postup: Ujistěte se, že jsou vaše aplikace Portál společnosti v aktuálním stavu. <!--879465-->

V prosinci 2016 jsme vydali aktualizaci umožňující vynucení pro vícefaktorové ověřování (MFA) u skupiny uživatelů, když zaregistrují zařízení s iOSem, Androidem, Windows 8.1+ nebo Windows Phone 8.1+. Tato funkce nefunguje bez některých základních verzí aplikace Portál společnosti pro Android (v5.0.3419.0+) a iOS (v2.1.17+).

Microsoft průběžně zdokonaluje Intune přidáváním nových funkcí do konzoly i do aplikací Portál společnosti na všech podporovaných platformách. Microsoft proto vydává opravy jenom pro problémy, které se vyskytly v aktuální verzi aplikace Portál společnosti. Aby se vám tedy s aplikacemi pracovalo co nejlépe, doporučujeme používat nejnovější verze aplikací Portál společnosti.

>[!Tip]
> Požádejte uživatele, aby si na svých zařízeních nastavili automatické aktualizace aplikací z příslušného obchodu s aplikacemi. Pokud jste ve sdílené síťové složce zpřístupnili aplikaci Portál společnosti pro Android, můžete její nejnovější verzi stáhnout z webu [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49140).

#### <a name="microsoft-teams-is-now-enabled-for-mam-on-ios-and-android"></a>Aplikace Microsoft Teams jsou teď povolené pro správu mobilních aplikací (MAM) v iOSu a Androidu

Společnost Microsoft oznámila obecnou dostupnost aplikací Microsoft Teams. Aktualizované aplikace Microsoft Teams pro iOS a Android teď můžou využívat možnosti správy mobilních aplikací (MAM) v Intune. Vaše týmy tedy můžou spolupracovat na různých zařízeních a zároveň je zajištěná ochrana konverzací a firemních dat. Další podrobnosti najdete v [oznámení o Microsoft Teams](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/) na blogu Enterprise Mobility and Security.


## <a name="february-2017"></a>Únor 2017

### <a name="new-capabilities"></a>Nové funkce

### <a name="modernizing-the-company-portal-website---753980--"></a>Modernizaci web Portál společnosti <!--753980-->
Web Portál společnosti bude podporovat aplikace zaměřené na uživatele, kteří nemají spravovaná zařízení. Tento web bude podobně jako ostatní produkty a služby Microsoftu používat nové kontrastní barevné schéma, dynamické ilustrace a „hamburgerovou“ nabídku ![Obrázek hamburgerové nabídky, která je teď přidaná v levém horním rohu webu Portál společnosti](./media/whats-new-archive-classic/CP_hamburger_menu.png).

### <a name="notices"></a>Oznámení

#### <a name="group-migration-will-not-require-any-updates-to-groups-or-policies-for-ios-devices---898837--"></a>Migrace skupiny nebude vyžadovat žádné aktualizace skupin ani zásad pro zařízení s iOS. <!--898837-->
Pro každou skupinu zařízení Intune předem přiřazenou profilem Registrace podnikového zařízení se v AAD vytvoří odpovídající dynamická skupina zařízení v závislosti na názvu profilu Registrace podnikového zařízení během migrace na Azure Active Directory skupiny zařízení. Zajistí se tak, že se budou zařízení během registrace automaticky seskupovat a přijmou stejné zásady a aplikace jako původní skupina Intune.

Jakmile tenant zahájí proces migrace pro seskupování a zacílení, vytvoří Intune automaticky dynamickou skupinu AAD tak, aby odpovídala skupině Intune, na kterou je zacílený profil registrace podnikového zařízení. Pokud správce Intune odstraní cílovou skupinu Intune, neodstraní se odpovídající dynamická skupina AAD. Smažou se členové skupiny a dynamický dotaz, ale skupina samotná zůstane, dokud ji správce IT neodebere přes portál AAD.

Podobně, pokud správce IT změní to, která skupina Intune je cílem profilu registrace podnikového zařízení, vytvoří Intune novou dynamickou skupinu odrážející nové přiřazení profilu, ale neodebere se dynamická skupina vytvořená pro staré přiřazení.

### <a name="defaulting-to-managing-windows-desktop-devices-through-windows-settings---663050--"></a>Výchozí nastavení pro správu stolních zařízení s Windows prostřednictvím nastavení Windows <!--663050-->
Výchozí chování registrace stolních počítačů s Windows 10 se mění. Nové registrace se budou provádět obvyklým tokem registrace agenta MDM, nikoli přes agenta pro počítače. Web Portál společnosti bude uživatelům stolních počítačů s Windows 10 poskytovat pokyny k registraci, které je provedou procesem přidání stolních počítačů s Windows 10 jako mobilní zařízení. Tato změna nebude mít vliv na už zaregistrované počítače, a [pokud chcete](manage-windows-pcs-with-microsoft-intune.md), může stolní počítače s Windows 10 vaše organizace pořád spravovat přes agenta pro počítače.

#### <a name="improving-mobile-app-management-support-for-selective-wipe---581242--"></a>Vylepšení podpory správy mobilních aplikací pro selektivní vymazání <!--581242-->
Koncovým uživatelům se dostanou další doprovodné materiály, jak znovu získat přístup k pracovním nebo školním datům, když se data automaticky odeberou kvůli zásadám "interval v offline režimu před vymazáním dat aplikace".<!--, or the removal of the Intune Company Portal on Android.-->

#### <a name="company-portal-for-ios-links-open-inside-the-app---665954--"></a>Portál společnosti pro odkazy iOS otevřené v aplikaci <!--665954-->
Odkazy v aplikaci Portálu společnosti pro iOS, včetně těch, které vedou na dokumentaci a aplikace, se budou otevírat přímo v aplikaci Portál společnosti pomocí integrovaného zobrazení Safari. Tato aktualizace se bude dodávat odděleně od aktualizace služby v lednu.

#### <a name="new-mdm-server-address-for-windows-devices---893007--"></a>Nová adresa serveru MDM pro zařízení s Windows <!--893007-->
Uživatelům Windows a Windows Phone se při pokusu o registraci zařízení zobrazí chyba, pokud zadají jako adresu serveru MDM __manage.microsoft.com__ (když se zobrazí výzva). Adresa serveru MDM se mění z __manage.microsoft.com__ na __enrollment.manage.microsoft.com__. Upozorněte uživatele, že mají jako adresu serveru MDM použít __enrollment.manage.microsoft.com__, když se jim zobrazí výzva při registraci zařízení s Windows nebo zařízení Windows Phone. Nastavení CNAME nevyžaduje žádné změny. Další informace o této změně najdete na webu [aka.ms/intuneenrollsvrchange](https://aka.ms/intuneenrollsvrchange).

#### <a name="new-user-experience-for-the-company-portal-app-for-android---621622--"></a>Nové uživatelské prostředí pro aplikaci Portál společnosti pro Android <!--621622-->
Od března bude aplikace Portál společnosti pro Android odpovídat [specifikacím Material Design](https://material.io/guidelines/material-design/introduction.html) a získá tak modernější vzhled a chování. Toto vylepšené uživatelské prostředí zahrnuje:

* __Barvy__: Záhlaví karet můžou mít barvy podle vaší vlastní palety barev.
* __Rozhraní__: tlačítka vybrané aplikace a všechny aplikace byly aktualizovány na kartě aplikace. Tlačítko Hledat je nyní plovoucí tlačítko akce.
* __Navigace__: V části Všechny aplikace se teď zobrazují karty Doporučené, Vše a Kategorie, které zjednodušují navigaci.
* __Služba__: Zlepšila se čitelnost karet Moje zařízení a Kontaktovat IT.

Obrázky před a po najdete na [stránce s aktualizacemi uživatelského rozhraní](whats-new-app-ui.md).

### <a name="associate-multiple-management-tools-with-the-microsoft-store-for-business---926135--"></a>Přidružení více nástrojů pro správu k Microsoft Store pro firmy <!--926135-->
Pokud k nasazování aplikací pro Microsoft Store pro firmy používáte více nástrojů pro správu, mohli jste k Microsoft Storu pro firmy dříve přidružit jenom jeden z nich. Teď už můžete ke Storu přidružit více nástrojů pro správu, například Intune a Configuration Manager. Podrobnosti najdete v článku [Správa aplikací koupených v Microsoft Storu pro firmy v Microsoft Intune](../apps/windows-store-for-business.md).

## <a name="whats-new-in-the-public-preview-of-intune-in-the-azure-portal---736542--"></a>Co je nového ve verzi Public Preview služby Intune v Azure Portal <!--736542-->

V rané kalendářním roce 2017 budeme migrovat naše ucelené prostředí pro správu do Azure, které umožňuje výkonnou a integrovanou správu základních pracovních postupů EMS na moderní platformě služby, která je rozšiřitelná pomocí rozhraní Graph API.

Noví zkušební tenanti se začnou objevovat ve veřejné verzi Preview nového prostředí pro správu na webu Azure Portal tento měsíc. Funkce a parita se stávající konzolou Intune se ve verzi Preview budou zavádět postupně.

Prostředí pro správu na webu Azure Portal bude využívat nové funkce seskupování a cílení, které už byly oznámeny. Při migraci vašeho stávajícího tenanta do nového prostředí seskupování se provede také vaše migrace do verze Preview nového prostředí pro správu vašeho tenanta. Pokud si chcete otestovat nebo prohlédnout některé nové funkce ještě před migrací vašeho tenanta, zaregistrujte si nový zkušební účet Intune nebo se podívejte na [novou dokumentaci](whats-new.md).

Novinky ve verzi Intune v Azure najdete [zde](whats-new.md).

## <a name="january-2017"></a>Leden 2017

### <a name="new-capabilities"></a>Nové funkce

#### <a name="in-console-reports-for-mam-without-enrollment---677961--"></a>Sestavy v konzole pro MAM bez registrace <!--677961-->
Pro registrovaná i nezaregistrovaná zařízení se přidaly nové sestavy pro ochranu aplikací. Přečtěte si o tom, jak můžete [pomocí Intune monitorovat zásady správy mobilních aplikací](../apps/app-protection-policies-monitor.md).

#### <a name="android-711-support---694397--"></a>Podpora Androidu 7.1.1 <!--694397-->
Intune teď plně podporuje a spravuje Android 7.1.1.

#### <a name="resolve-issue-where-ios-devices-are-inactive-or-the-admin-console-cannot-communicate-with-them---unknown--"></a>Řešení problému, kdy zařízení s iOSem nejsou aktivní nebo s nimi nemůže konzola správce komunikovat <!--unknown-->
Když zařízení uživatelů ztratí kontakt s Intune, můžete jim poskytnout nové kroky pro řešení potíží, které jim pomohou znovu získat přístup k firemním prostředkům. Viz [Zařízení nejsou aktivní nebo s nimi nemůže konzola správce komunikovat](../enrollment/troubleshoot-device-enrollment-in-intune.md#devices-are-inactive-or-the-admin-console-cant-communicate-with-them).

### <a name="notices"></a>Oznámení

#### <a name="defaulting-to-managing-windows-desktop-devices-through-windows-settings---663050--"></a>Výchozí nastavení pro správu stolních zařízení s Windows prostřednictvím nastavení Windows <!--663050-->
Výchozí chování registrace stolních počítačů s Windows 10 se mění. Nové registrace se budou provádět obvyklým tokem registrace agenta MDM, nikoli přes agenta pro počítače.

Web Portál společnosti bude uživatelům stolních počítačů s Windows 10 poskytovat pokyny k registraci, které je provedou procesem přidání stolních počítačů s Windows 10 jako mobilní zařízení. Tato změna nebude mít vliv na už zaregistrované počítače, a [pokud chcete](manage-windows-pcs-with-microsoft-intune.md), může stolní počítače s Windows 10 vaše organizace pořád spravovat přes agenta pro počítače.

#### <a name="improving-mobile-app-management-support-for-selective-wipe---581242--"></a>Vylepšení podpory správy mobilních aplikací pro selektivní vymazání <!--581242-->
Koncovým uživatelům se dostanou další doprovodné materiály, jak znovu získat přístup k pracovním nebo školním datům, když se data automaticky odeberou kvůli zásadám "interval v offline režimu před vymazáním dat aplikace".<!--, or the removal of the Intune Company Portal on Android.-->

#### <a name="company-portal-for-ios-links-open-inside-the-app---665954--"></a>Portál společnosti pro odkazy iOS otevřené v aplikaci <!--665954-->
Odkazy v aplikaci Portálu společnosti pro iOS, včetně těch, které vedou na dokumentaci a aplikace, se budou otevírat přímo v aplikaci Portál společnosti pomocí integrovaného zobrazení Safari. Tato aktualizace se bude dodávat odděleně od aktualizace služby v lednu.

#### <a name="modernizing-the-company-portal-website---753980--"></a>Modernizaci web Portál společnosti <!--753980-->
Od února bude web Portál společnosti podporovat aplikace zaměřené na uživatele, kteří nemají spravovaná zařízení. Tento web bude podobně jako ostatní produkty a služby Microsoftu používat nové kontrastní barevné schéma, dynamické ilustrace a „hamburgerovou“ nabídku ![Hamburgerová nabídka na webu Portál společnosti](./media/whats-new-archive-classic/CP_hamburger_menu.png).

#### <a name="new-documentation-for-app-protection-policies---583398--"></a>Nová dokumentace k zásadám ochrany aplikací <!--583398-->
Aktualizovali jsme naši dokumentaci pro správce a vývojáře aplikací, kteří chtějí ve svých aplikacích pro iOS a Android zapnout zásady ochrany aplikací (známé jako zásady MAM) pomocí nástroje Intune App Wrapping Tool nebo sady Intune App SDK.

Aktualizovaly se tyto články:

* [Rozhodování o způsobu přípravy aplikací na jejich správu v Microsoft Intune](../developer/apps-prepare-mobile-application-management.md)
* [Příprava aplikací pro iOS na správu mobilních aplikací přes nástroj Intune App Wrapping](../developer/app-wrapper-prepare-ios.md)
* [Začínáme s Microsoft Intune App SDK](../developer/app-sdk-get-started.md)
* [Intune App SDK pro iOS – Příručka pro vývojáře](../developer/app-sdk-ios.md)

Následující články jsou v knihovně dokumentů nové:

* [Modul plug-in Cordova sady Intune App SDK](../developer/app-sdk.md)
* [Komponenta Xamarin sady Intune App SDK](../developer/app-sdk-xamarin.md)

#### <a name="progress-bar-when-launching-the-company-portal-on-ios---665978--"></a>Indikátor průběhu při spouštění Portál společnosti v iOS <!--665978-->
Portál společnosti pro iOS zavádí na obrazovce spuštění indikátor průběhu, který uživateli poskytuje informace o probíhajících procesech načítání. Indikátor průběhu bude postupně nahrazovat ikonu zaneprázdnění. To znamená, že někteří uživatelé uvidí nový indikátor průběhu, zatímco jiným se bude dále zobrazovat ikona zaneprázdnění.

## <a name="december-2016"></a>Prosinec 2016

### <a name="public-preview-of-intune-in-the-azure-portal--736542--"></a>Verze Public Preview služby Intune v Azure Portal<!--736542-->
V úvodním kalendářním roce 2017 budeme migrovat naše ucelené prostředí pro správu do Azure, které umožňuje výkonnou a integrovanou správu základních pracovních postupů EMS na moderní platformě pro služby, která je rozšiřitelná pomocí rozhraní Graph API. Před všeobecnou dostupností tohoto portálu pro všechny tenanty Intune s radostí oznamujeme, že později tento měsíc začneme vybraným tenantům zavádět verzi Preview tohoto nového prostředí pro správce.

Prostředí pro správu na webu Azure Portal bude využívat nové funkce seskupování a cílení, které už byly oznámeny. Při migraci vašeho stávajícího tenanta do nového prostředí seskupování se provede také vaše migrace do verze Preview nového prostředí pro správu vašeho tenanta. Zatím můžete zjistit další informace o tom, co pro Microsoft Intune na portálu Azure Portal chystáme, v naší [nové dokumentaci](what-is-intune.md).

__Integrace se správou telekomunikačních výdajů ve verzi Public Preview Azure Portal__ <!--747605-->
Ve verzi Preview teď začínáme na webu Azure Portal zavádět integraci se službami TEM (Telecom Expense Management) třetích stran. Pomocí Intune můžete uplatňovat limity na využívání domácích a roamingových dat. Tyto integrace začínáme zavádět s řešením [Saaswedo](http://www.saaswedo.com/). Pokud chcete povolit tuto funkci ve zkušební verzi tenanta, [obraťte se prosím na podporu Microsoftu](get-support.md).

### <a name="new-capabilities"></a>Nové funkce

__Multi-Factor Authentication napříč všemi platformami__ <!--747590-->
Teď můžete vynutit vícefaktorové ověřování (MFA) u vybrané skupiny uživatelů při registraci jejich zařízení se systémem iOS, Android, Windows 8.1+ nebo Windows Phone 8.1+ tak, že na portálu pro správu Azure nakonfigurujete MFA v aplikaci pro registraci Microsoft Intune v Azure Active Directory.

__Možnost omezit registraci mobilního zařízení__ <!--747596-->
Intune přidává nová omezení registrace řídící to, které platformy mobilních zařízení se mohou zaregistrovat. Intune odděluje platformy mobilních zařízení, jako je iOS, macOS, Android, Windows a Windows Mobile.
* Omezení registrace mobilních zařízení neomezuje registraci klienta pro počítače.
* Pouze pro iOS existuje další možnost blokování registrace osobně vlastněných zařízení.

Pokud správce IT neoznačí nová zařízení jako vlastněná podnikem, Intune všechna nová zařízení označí jako osobní. Podrobnosti najdete v [tomto článku](../enrollment/device-enrollment.md).

### <a name="notices"></a>Oznámení

__Multi-Factor Authentication při registraci se přesouvá do Azure Portal__ <!--VSO 750545-->
Dříve by správci při nastavování vícefaktorového ověřování pro registrace Intune přešli do konzoly Intune nebo do konzoly Configuration Manageru (verze dřívější než z října 2016). S touto aktualizovanou funkcí se teď budete pomocí přihlašovacích údajů Intune přihlašovat na [Microsoft Azure Portal](https://manage.windowsazure.com) a nakonfigurujete nastavení MFA pomocí služby Azure AD. Další informace o tom najdete [tady](https://aka.ms/mfa_ad).

__Aplikace Portál společnosti pro Android je teď dostupná v číně__ <!--VSO 658093-->
Publikujeme aplikaci Portál společnosti pro Android pro stahování v Číně. Z důvodu absence Obchod Google Play v Číně musí zařízení s Androidem získávat aplikace z čínských Marketplace aplikací. Aplikace Portál společnosti pro Android bude dostupná ke stažení v těchto obchodech:
* [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
* [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
* [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
* [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

Ke komunikaci se službou Microsoft Intune používá aplikace Portál společnosti pro Android služby Google Play. Vzhledem k tomu, že služby Google Play ještě nejsou v Číně dostupné, může provádění kterékoli z následujících úloh trvat až 8 hodin.

|Konzola správce Intune| Aplikace Portál společnosti Intune pro Android |Web Portál společnosti Intune|
|---|---|---|
|Úplné vymazání| Odebrání vzdáleného zařízení| Odebrání zařízení (místní a vzdálené)|
|selektivní vymazání| Resetování zařízení| Resetování zařízení|
|Nasazení nových nebo aktualizovaných aplikací| Instalace dostupných obchodních aplikací| Resetování hesla zařízení|
|Vzdálené uzamčení|||
|Resetování hesla|||

### <a name="deprecations"></a>Vyřazení

__Firefox už nebude podporovat Silverlight__ <!--VSO TBA-->
Mozilla ve verzi 52 [prohlížeče Firefox](https://www.mozilla.org/firefox) přestává podporovat Silverlight s účinností od března 2017. V důsledku toho se už pomocí Firefoxu ve verzi vyšší než 51 nebudete moct přihlásit ke stávající konzole Intune. Doporučujeme pro přístup ke konzole pro správce používat Internet Explorer 10 nebo 11 nebo [verzi Firefoxu starší než 52](https://ftp.mozilla.org/pub/firefox/releases/). Přechod Intune na Azure Portal umožní podporu celé řady [moderních prohlížečů](/azure/azure-preview-portal-supported-browsers-devices) bez závislosti na Silverlightu.

__Odebrání zásad poštovní schránky mobilních zařízení Exchange Online__ <!--770687-->
Od prosince už správci nebudou moct zobrazit nebo nakonfigurovat zásady poštovní schránky mobilních zařízení Exchange Online (EAS) v konzole Intune. Tato změna se bude pro všechny tenanty Intune zavádět v průběhu prosince a ledna. Všechny stávající zásady zůstanou tak, jak jsou nakonfigurované. Ke konfiguraci nových zásad použijte prostředí Exchange Management Shell. Další informace o tom najdete [tady](https://technet.microsoft.com/library/bb123783%28v=exchg.150%29.aspx).

__Aplikace Intune AV Player, Image Viewer a PDF Viewer se už v Androidu nepodporují.__ <!--747553-->
Od poloviny prosince 2016 už uživatelé nebudou moct dál používat aplikace Intune AV Player, Image Viewer a PDF Viewer. Tyto aplikace nahrazuje aplikace Azure Information Protection. Další informace o aplikaci Azure Information Protection najdete [tady](/information-protection/rms-client/mobile-app-faq).

## <a name="november-2016"></a>Listopad 2016

### <a name="new-capabilities"></a>Nové funkce

__Nový Portál společnosti Microsoft Intune pro zařízení s Windows 10__ Společnost Microsoft vydala novou [aplikaci Portál společnosti Microsoft Intune pro zařízení s Windows 10](https://www.microsoft.com/store/apps/9wzdncrfj3pz). Tato aplikace, která využívá nový univerzální formát Windows 10, poskytne uživatelům aktualizované prostředí, které je identické napříč všemi zařízeními s Windows 10, ať už jsou to počítače, nebo mobilní zařízení, a nabídne přitom stejné funkce, které v současnosti využívají.

Tato nová aplikace také uživatelům umožní využít v zařízeních s Windows 10 další funkce platformy, jako je jednotné přihlašování (SSO) a ověřování na základě certifikátů. Tato aplikace bude dostupná jako upgrade stávající aplikace Portál společnosti Windows 8.1 a Portál společnosti Windows Phone 8.1 a instaluje se z Microsoft Storu. Další podrobnosti najdete na adrese [aka.ms/intunecp_universalapp](https://aka.ms/intunecp_universalapp).

> [!IMPORTANT]
> __Aktualizace v Intune a Androidu for Work__Aplikace Android for Work můžete nasazovat s akcí __Požadované__, ale pokud byly vaše skupiny Intune migrovány do nového prostředí Azure AD, můžete aplikace nasazovat jenom jako __Dostupné__.

__Modul plug-in Cordova sady Intune App SDK teď podporuje mam bez registrace__ . Vývojáři aplikací teď můžou použít modul plug-in Cordova sady Intune App SDK k povolení funkcí MAM bez registrace zařízení ve svých aplikacích založených na Cordova pro Android a iOS/iPadOS. Modul plug-in Cordova sady Intune App SDK najdete [tady](https://github.com/msintuneappsdk/cordova-plugin-ms-intune-mam).

__Komponenta Xamarin sady Intune App SDK teď podporuje mam bez registrace__ . Vývojáři aplikací teď můžou pomocí komponenty Xamarin sady Intune App SDK povolit funkce MAM bez registrace zařízení ve svých aplikacích založených na Xamarin pro Android a iOS/iPadOS. Komponentu Xamarin sady Intune App SDK najdete [tady](https://github.com/msintuneappsdk/intune-app-sdk-xamarin).

### <a name="notices"></a>Oznámení

__Podpisový certifikát Symantec už k nahrání nevyžaduje podepsanou aplikaci Portál společnosti ve Windows Phonu 8__ Nahrání podpisového certifikátu Symantec už nevyžaduje podepsanou aplikaci Portál společnosti ve Windows Phonu 8. Certifikát jde nahrát nezávisle.

### <a name="deprecations"></a>Vyřazení

__Podpora Portálu společnosti ve Windows Phonu 8__ Podpora Portálu společnosti ve Windows Phonu 8 se přestane nabízet. Podpora pro platformy Windows Phone 8 a WinRT se přestala nabízet v říjnu 2016. Podpora pro Portál společnosti ve Windows Phonu 8 se také přestala nabízet v říjnu 2016.


## <a name="see-also"></a>Viz také
Podrobnosti o nedávném vývoji najdete [v tématu Co je nového v Microsoft Intune](whats-new.md) .
