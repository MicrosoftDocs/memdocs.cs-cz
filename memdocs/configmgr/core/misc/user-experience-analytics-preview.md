---
title: Služba Endpoint Analytics Preview
titleSuffix: Configuration Manager
description: Pokyny pro službu Endpoint Analytics Preview
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 00537b90-f6d2-45e9-a9a1-6b3ada466a16
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: e7dbb53833c29aae442eec4ca3c8402b99cde237
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693235"
---
# <a name="endpoint-analytics-preview"></a><a name="bkmk_uea"></a>Služba Endpoint Analytics Preview

> [!Note]  
> Tyto informace se vztahují k funkci ve verzi Preview, která se podstatně změnila předtím, než se komerční verze uvolní. Microsoft neposkytuje žádné záruky, výslovné ani předpokládané, týkající se zde uváděných informací. 
>
> Další informace o změnách služby Endpoint Analytics najdete v tématu [co je nového ve službě Endpoint Analytics](whats-new-endpoint-analytics.md). 

## <a name="endpoint-analytics-overview"></a>Přehled služby Endpoint Analytics

Pro koncové uživatele není běžné, že budou mít dlouhé časy spuštění nebo jiné přerušení. Tato přerušení mohou být způsobena kombinací:

- Starší verze hardwaru
- Konfigurace softwaru, které nejsou optimalizované pro činnost koncového uživatele
- Problémy způsobené změnami a aktualizacemi konfigurace

Tyto problémy a další potíže s činnostmi koncového uživatele jsou trvalé, protože neobsahují mnohem přehled o činnosti koncového uživatele. Obecně platí, že k těmto potížím dochází z pomalého nákladného kanálu, který obvykle neposkytuje jasné informace o tom, co je potřeba optimalizovat. Nepodporují jenom náklady na tyto problémy. Čas strávený s informacemi, které pracovníci stráví problémy, je také nákladný. Problémy s výkonem, spolehlivostí a podporou, které omezují produktivitu uživatelů, můžou mít velký dopad i na spodní linii organizace.

Služba **Endpoint Analytics** je cílem zlepšit produktivitu uživatelů a snížit náklady na podporu tím, že poskytuje přehled o prostředí uživatele. Přehledy umožňují optimalizovat činnost koncového uživatele pomocí proaktivní podpory a detekovat regrese uživatelského prostředí tím, že vyhodnotí dopad změn konfigurace na uživatele.

Tato počáteční verze se zaměřuje na tři věci:

- [**Doporučený software**](#bkmk_uea_rs): doporučení pro zajištění nejlepšího uživatelského prostředí
- [**Proaktivní skriptování při nápravě**](#bkmk_uea_prs): Opravte běžné problémy s podporou před tím, než koncoví uživatelé vyvšimnete problémy.
- [**Spuštění výkonu**](#bkmk_uea_bp): usnadňuje uživatelům přístup k rychlému zprovoznění bez zdlouhavého spouštění a zpoždění přihlášení.

Tato verze je jenom začátek. Nové poznatky pro další klíčové uživatele už brzy využijeme po úvodní verzi. Další informace o změnách služby Endpoint Analytics najdete v tématu [co je nového ve službě Endpoint Analytics](whats-new-endpoint-analytics.md).

## <a name="getting-started"></a><a name="bkmk_uea_prereq"></a>Začínáme

Pokud chcete začít používat službu Endpoint Analytics, ověřte požadavky a potom spusťte shromažďování dat. 

### <a name="technical-prerequisites"></a>Technické požadavky

V této verzi Preview můžete registrovat zařízení prostřednictvím Configuration Manager nebo Microsoft Intune. 

Tato verze Preview vyžaduje k registraci zařízení přes Intune:
- Zařízení zaregistrovaná v Intune s Windows 10
- Přehledy o výkonu po spuštění jsou dostupné jenom pro zařízení, na kterých běží verze 1903 nebo novější z Windows 10 Enterprise (v současné době se nepodporují edice Home a pro) a zařízení musí být připojená k Azure AD nebo připojené k hybridní službě Azure AD. Počítače připojené k pracovišti se v tuto chvíli nepodporují.
- Síťové připojení ze zařízení k veřejnému cloudu Microsoftu. Další informace najdete v tématu [koncové body](#bkmk_uea_endpoints).
- K [zahájení shromažďování dat](#bkmk_uea_start)je nutná [role správce služby Intune](https://docs.microsoft.com/intune/fundamentals/role-based-access-control) .
   - Kliknutím na **Start**souhlasíte s tím, že zákaznická data můžou být uložená mimo umístění, které jste vybrali při zřizování tenanta Microsoft Intune.
   - Po kliknutí na tlačítko **Spustit** pro shromažďování dat mohou data zobrazit další role jen pro čtení.

Tato verze Preview vyžaduje k registraci zařízení přes Configuration Manager:
- Configuration Manager verze 2002 nebo novější
- Klienti upgradovali na verzi 2002 nebo novější.
- [Klient Microsoft Endpoint Manageru](https://docs.microsoft.com/mem/configmgr/tenant-attach/device-sync-actions) se musí připojit s umístěním klienta Azure Severní Amerika (brzy se rozbalíme do dalších oblastí).

Bez ohledu na to, jestli jsou zařízení zaregistrovaná přes Intune nebo Configuration Manager, má [**skriptování proaktivního problému**](#bkmk_uea_prs) následující požadavky:
- Zařízení musí být připojená k Azure AD nebo být připojená k hybridní službě Azure AD a splňovat jednu z následujících podmínek:
- Zařízení s Windows 10 Enterprise, Professional nebo vzdělávací zařízení, které je spravované přes Intune
- [Spoluspravované](../../comanage/overview.md) zařízení s Windows 10 Enterprise verze 1607 nebo novější s [úlohou klientské aplikace](../../comanage/workloads.md#client-apps) odkazovalo na Intune.
- [Spoluspravované](../../comanage/overview.md) zařízení s Windows 10 Enterprise verze 1903 nebo novější s [úlohou klientské aplikace](../../comanage/workloads.md#client-apps) ukazují na Configuration Manager.

### <a name="licensing-prerequisites"></a>Požadavky na licencování

Služba Endpoint Analytics je součástí následujících plánů: 

- [Enterprise mobility + Security E3](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) nebo vyšší
- [Microsoft 365 Enterprise E3](https://www.microsoft.com/en-us/microsoft-365/enterprise?rtc=1) nebo vyšší.

Proaktivní nápravy taky vyžadují jednu z následujících licencí pro spravovaná zařízení:
- Windows 10 Enterprise E3 nebo E5 (zahrnuté ve Microsoft 365 F3, E3 nebo E5)
- Windows 10 školství a3 nebo A5 (zahrnuté do Microsoft 365 a3 nebo A5)
- Přístup k virtuální ploše Windows s přístupem E3 nebo E5

### <a name="permissions"></a>Oprávnění

#### <a name="endpoint-analytics-permissions"></a>Oprávnění pro analýzu koncových bodů

Pro službu Endpoint Analytics se používají následující oprávnění:
- **Přečtěte si** kategorii **Konfigurace zařízení** .
- **Přečtěte si** v kategorii **organizace** . <!--temporary for pp-->
- Oprávnění, která jsou vhodná pro roli uživatele v kategorii služby **Endpoint Analytics** .

Uživatel, který je jen pro čtení, potřebuje jenom oprávnění **ke čtení** v rámci **konfigurací zařízení** i kategorií služby **Endpoint Analytics** . Správce Intune by obvykle potřeboval všechna oprávnění.

#### <a name="proactive-remediations-permissions"></a>Oprávnění proaktivní nápravy

V případě proaktivní nápravy potřebuje uživatel oprávnění odpovídající jejich roli v kategorii **Konfigurace zařízení** .  Oprávnění v kategorii služby **Endpoint Analytics** nejsou potřebná, pokud uživatel používá proaktivní nápravy.


## <a name="start-gathering-data"></a><a name="bkmk_uea_start"></a>Spustit shromažďování dat

1. Přejděte na `https://endpoint.microsoft.com/#blade/Microsoft_Intune_Enrollment/UXAnalyticsMenu`.
1. Klikněte na tlačítko **Start**. Tím se automaticky přiřadí konfigurační profil pro shromažďování údajů o výkonu spouštění ze všech oprávněných zařízení. [Přiřazená zařízení](#bkmk_uea_profile) můžete později změnit. Po restartování může trvat až 24 hodin, než se data o výkonu po spuštění naplní ze zařízení zaregistrovaných v Intune.
   - Další informace o běžných problémech najdete v tématu [řešení potíží s registrací spouštěcího zařízení](#bkmk_uea_enrollment_tshooter).

## <a name="overview-page"></a>Stránka Přehled

Jakmile budou data připravena, všimnete si některých informací na stránce **Přehled** , které jsou podrobněji vysvětleny níže:

- **Skóre uživatelského prostředí** je 50/50 vážený průměr **doporučených výsledků softwaru** a **výkonu při spuštění**. V průběhu času budeme rozšiřovat sadu dílčích skóre.

- Aktuální skóre můžete porovnat s dalšími výsledky nastavením standardních hodnot.
  - Jak je popsáno v části [základní hodnoty](#bkmk_uea_baselines) , je k dispozici vestavěný směrný plán pro *komerční medián* , který vám umožní porovnat s běžným podnikem. Můžete vytvořit nové směrné plány na základě aktuálních metrik, abyste mohli sledovat průběh nebo zobrazit regrese v průběhu času.
   - Pro celkové skóre a dílčí skóre jsou zobrazeny základní značky. Pokud se některá z skóre překročí o více než konfigurovatelné prahové hodnotě z vybraného směrného plánu, zobrazí se skóre červeně a skóre nejvyšší úrovně se označí jako potřeba pozornost.
  - Stav **nedostatečných dat** znamená, že nemáte dostatečná zařízení, která by poskytovala smysluplné skóre. V současnosti vyžadujeme aspoň pět zařízení.

- **Filtry** vám umožní zobrazit skóre pro podmnožinu zařízení nebo uživatelů. Funkce filtru ale v této verzi Preview nejsou povolené.

- **Přehledy a doporučení** jsou seznam s určenými prioritami, který vylepšuje vaše skóre. Tento seznam je filtrován na kontext poduzlu při přechodu na **osvědčené postupy** nebo **doporučený software**.

[![Stránka s přehledem služby Endpoint Analytics](media/overview-page.png)](media/overview-page.png#lightbox)

## <a name="recommended-software"></a><a name="bkmk_uea_rs"></a>Doporučený software

> [!Important]  
> Služba Endpoint Analytics vypočítá skóre **přijetí softwaru** pro všechna vaše zařízení spravovaná přes Intune bez ohledu na to, jestli se zaregistrovala v rámci služby Endpoint Analytics, nebo ne.

Určitý software je známý pro zlepšení činnosti koncového uživatele bez ohledu na metriky stavu nižší úrovně. Například Windows 10 má mnohem vyšší skóre síťového vyvýšení, než je Windows 7. Skóre **přijetí softwaru** je číslo mezi 0 a 100, které představuje vážený průměr zařízení, která nasadila různé doporučený software. Aktuální váha je vyšší pro Windows než pro ostatní metriky, protože uživatelé s nimi pracují častěji. Metriky jsou popsány níže: 

[![Doporučená stránka softwaru pro službu Endpoint Analytics](media/recommended-software.png)](media/recommended-software.png#lightbox)

### <a name="windows-10"></a><a name="bkmk_uea_win10"></a> Windows 10

Windows 10 nabízí lepší uživatelské prostředí než starší verze Windows. Další informace najdete v dokumentu [White paper k TEI](https://vc2prod.blob.core.windows.net/vc-resources/TEIStudies/TEI%20of%20Windows%2010.pdf) .

Tato metrika měří procento zařízení ve Windows 10 oproti starší verzi Windows.

Doporučená akce nápravy pro přesunutí zařízení ze starších verzí Windows je vytvoření plánu nasazení pomocí [Desktop Analytics](../../desktop-analytics/overview.md).

### <a name="autopilot"></a><a name="bkmk_uea_ap"></a>Autopilot

Microsoft autopilot poskytuje jednodušší úvodní prostředí pro počítače s Windows 10, než je nativní prostředí, a to díky omezení počtu obrazovek v prostředí příkazového začátku (OOBE) a poskytování výchozích hodnot pro zajištění, že se zařízení zaměstnanců správně zřídí z továrny nebo když se resetují.

Tato metrika měří procento zařízení s Windows 10, která jsou zaregistrovaná pro autopilotní.

Doporučená akce nápravy je registrace existujících zařízení v rámci autopilotu pomocí [Microsoft Intune](https://docs.microsoft.com/intune/enrollment-autopilot).

### <a name="azure-active-directory"></a><a name="bkmk_uea_aad"></a>Azure Active Directory

Azure Active Directory (Azure AD) poskytuje uživatelům spoustu výhod produktivity, jako je jednotné přihlašování k aplikacím a službám, přihlášení Windows Hello, samoobslužné obnovení nástroje BitLocker a podnikový datový roaming.

Tato metrika měří procento zařízení zaregistrovaných ve službě Azure AD.

Vaše zařízení spravovaná přes Microsoft Intune jsou už registrovaná v Azure AD. K doporučené nápravné akci pro zařízení spravovaná pomocí Configuration Manager je můžete buď [zaregistrovat ve službě Azure AD](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) , nebo je [společně spravovat](../../comanage/overview.md). Společně se správou zařízení se taky zlepšuje skóre správy cloudu.

### <a name="cloud-management"></a><a name="bkmk_uea_intune"></a>Správa cloudu

Microsoft Intune poskytuje uživatelům několik výhod produktivity, včetně povolení přístupu k podnikovým prostředkům, i když jsou mimo podnikovou síť, a eliminuje nutnost zásahu z provozu a výkon Zásady skupiny a výsledkem je lepší prostředí pro koncové uživatele. Tato metrika měří procento počítačů zaregistrovaných v Microsoft Intune. Podívejte se, jak [to Microsoft umožňuje pro naše zaměstnance](https://www.microsoft.com/en-us/itshowcase/managing-windows-10-devices-with-microsoft-intune).

K doporučené nápravné akci pro zařízení spravovaná Configuration Manager, která ještě nejsou zaregistrovaná v Intune, se dají [společně spravovat](../../comanage/overview.md).

### <a name="no-commercial-median"></a><a name="bkmk_uea_np"></a>Žádná komerční medián

Předdefinované základní hodnoty **komerčního mediánu** v současnosti neobsahují metriky pro dílčí skóre uvedená v částech výše.

## <a name="startup-performance"></a><a name="bkmk_uea_bp"></a>Výkon při spuštění

> [!NOTE]
> Pokud nevidíte data o výkonu při spuštění ze všech svých zařízení, přečtěte si téma [řešení potíží s registrací spouštěcího zařízení](#bkmk_uea_enrollment_tshooter).

Skóre výkonu při spuštění pomáhá rychle získat uživatele z elektrického napájení do produktivity bez nutnosti zdlouhavého spouštění a zpoždění přihlášení. **Skóre spuštění** je číslo mezi 0 a 100. Toto skóre je vážený průměr **spouštěcího skóre** a skóre **přihlášení** , které se vypočítávají takto:

- **Skóre spuštění**: na základě času zapnutí přihlášení. Podíváme se na čas posledního spuštění z každého zařízení, s výjimkou fáze aktualizace a pak ho skóre od 0 (špatné) až 100 (výjimečné). Tato skóre jsou Průměrná, protože poskytují celkové skóre spuštění tenanta.
- **Skóre přihlášení**: na základě doby od zadání přihlašovacích údajů, dokud uživatel nezíská přístup k reagující ploše (tzn. že plocha se vykreslila a využití CPU kleslo pod 50% po dobu alespoň 2 sekundy). Podíváme se na poslední čas přihlášení ke každému zařízení, s výjimkou prvních přihlášení nebo přihlášení hned po aktualizaci funkcí a jejich skóre z 0 (špatné) na 100 (výjimečné). Tato skóre jsou Průměrná, protože poskytují celkové skóre spuštění tenanta.

[![Stránka výkonu spuštění služby Endpoint Analytics](media/startup-performance.png)](media/startup-performance.png#lightbox)

### <a name="insights"></a>Insights

Stránka **výkon při spuštění** také nabízí seznam **přehledů a doporučení**, která jsou popsaná v následujících částech:

#### <a name="hard-disk-drives"></a><a name="bkmk_uea_hdd"></a>Jednotky pevného disku

Výkon při spuštění nabízí přehled o počtu zařízení, na kterých je spouštěcí jednotka pevný disk. Jednotky pevného disku obvykle mají za následek trojnásobnou dobu spouštění tři až čtyřikrát delší než jednotky Solid-State. Také nahlásíme očekávané vylepšení spuštění výkonu, které byste získali přesunutím na jednotky SSD (Solid-State Drive).

Kliknutím na Zobrazit zobrazíte seznam zařízení, která mají jednotky pevného disku. Doporučená akce je upgradovat tato zařízení na jednotky Solid-State.

#### <a name="group-policy"></a><a name="bkmk_uea_gp"></a>Zásady skupiny

Výkon při spuštění nabízí přehled o počtu zařízení, která mají prodlevu při spouštění a časy přihlášení způsobené Zásady skupiny. Kliknutím přejdete do zobrazení zařízení. Zobrazení je seřazené podle Zásady skupiny času, takže se můžete podívat na postižená zařízení pro další řešení potíží.

Pokud kliknete na konkrétní zařízení, můžete se podívat na jeho spouštěcí historii a historii přihlášení. Historie vám pomůže určit, jestli se jedná o regresi a kdy k tomu mohlo dojít.

I když existuje spousta článků o tom, jak optimalizovat výkon zásad skupiny, můžete místo toho migrovat na cloudovou správu. Migrace do cloudu umožňuje používat [standardní hodnoty zabezpečení Intune](https://docs.microsoft.com/intune/protect/security-baselines) a již brzy vydaný Nástroj pro analýzu zásad.

#### <a name="slow-boot-and-sign-in-times"></a><a name="bkmk_uea_sb"></a>Pomalé spouštění a časy přihlášení

Výkon při spuštění nabízí přehled o počtu zařízení s pomalým spouštěním nebo podobam přihlášení. Skóre spuštění nebo skóre přihlášení "0" znamená, že je pomalé. Kliknutím přejdete do zobrazení zařízení. Tato zařízení jsou seřazená podle základního času spuštění nebo základního přihlašovacího času, takže se můžete podívat na postižená zařízení pro další řešení potíží.

Pokud kliknete na konkrétní zařízení, můžete se podívat na jeho spouštěcí historii a historii přihlášení. Historie vám pomůže určit, jestli se jednalo o regresi a kdy k tomu mohlo dojít.

### <a name="reporting-tabs"></a>Karty vytváření sestav

Stránka **výkon při spuštění** obsahuje karty pro vytváření sestav, které poskytují podporu pro přehledy, včetně:
1. **Výkon modelu**. Na této kartě se můžete podívat na výkon spuštění a přihlášení podle modelu zařízení, který vám může poznat, jestli jsou problémy s výkonem izolované na konkrétní modely.
1. **Výkon zařízení**. Tato karta poskytuje spouštěcí a přihlašovací metriky pro všechna vaše zařízení. Můžete řadit podle konkrétní metriky (například přihlašování pomocí GP) a zjistit, která zařízení mají pro tuto metriku nejhorších skóre, která vám pomůžou při řešení potíží. Můžete také vyhledat zařízení podle názvu. Pokud kliknete na zařízení, uvidíte jeho historii spouštění a přihlašování, které vám pomůžou zjistit, jestli došlo k nedávné regresi.
1. **Procesy po spuštění**. Tato karta (je-li viditelná; jsme se na to seznámili jenom s tím, jak pořád tuto funkci vyvíjíme) se dozvíte, které procesy mají vliv na fázi přihlášení "čas do reakce na pracovní plochu"; To znamená, že po vygenerování plochy se udržuje procesor nad 50%.

## <a name="proactive-remediations"></a><a name="bkmk_uea_prs"></a>Proaktivní nápravné opravy

Proaktivní nápravné opravy jsou balíčky skriptů, které můžou detekovat a opravovat běžné problémy s podporou na zařízení uživatele dřív, než se problém vyřeší. Tyto opravy mohou pomoci snížit volání podpory. Můžete vytvořit vlastní balíček skriptu nebo nasadit jeden z balíčků skriptu, které jsme napsali a použili v našem prostředí pro omezení lístků podpory.

Každý balíček skriptu se skládá ze skriptu detekce, skriptu pro nápravu a metadat. Přes Intune budete moct tyto balíčky skriptů nasazovat a zobrazovat sestavy jejich efektivity. Aktivně vyvíjíme nové balíčky skriptů a rádi bychom věděli, jak vaše prostředí využívají. Pokud máte jakoukoli zpětnou vazbu k balíčkům skriptu, kontaktujte svůj kontakt na službu Endpoint Analytics ve verzi Preview.

### <a name="get-the-detection-and-remediation-scripts"></a><a name="bkmk_uea_prs_ps1"></a>Získání skriptů pro detekci a nápravu

1. Zkopírujte skripty z dolní části tohoto článku v části [powershellové skripty](#bkmk_uea_ps_scripts) .
    - Soubory skriptu, jejichž názvy začínají `det` na, jsou skripty detekce. Skripty pro `rem`nápravu začínají na.
    - Popis skriptů najdete v [popisech skriptů](#bkmk_uea_scripts).
1. Uložte všechny skripty pomocí zadaného názvu. Název je také v komentářích v horní části každého skriptu.
    - Můžete použít jiný název skriptu, ale neshoduje se s názvem uvedeným v části [popisy skriptů](#bkmk_uea_scripts) .


### <a name="deploying-and-monitoring-scripts"></a><a name="bkmk_uea_prs_deploy"></a>Nasazení a monitorování skriptů
Služba **rozšíření pro správu Microsoft Intune** získá skripty z Intune a spustí je. Skripty se spustí znovu každých 24 hodin. Chcete-li nasadit a monitorovat skripty, postupujte podle následujících pokynů:

1. V konzole nástroje přejdete do uzlu **proaktivní nápravy** .
1. Kliknutím na tlačítko **vytvořit balíček skriptu** vytvořte balíček skriptu.
     [![Stránka proaktivní opravy služby Endpoint Analytics. Vyberte odkaz vytvořit.](media/proactive-remediations-create.png)](media/proactive-remediations-create.png#lightbox)
1. V kroku **základy** dejte balíčku skriptu **název** a volitelně také **Popis**. Pole **vydavatele** lze upravovat, ale ve výchozím nastavení se jedná o název tenanta. **Verzi** nelze upravovat. 
1. V kroku **Nastavení** zkopírujte text ze skriptů, které jste stáhli, do polí pro **vyhledávání** a skripty pro **nápravu** . 
   - Potřebujete odpovídající detekci a skript pro nápravu, aby byl ve stejném balíčku. Skript `Detect_stale_Group_Policies.ps1` detekce například odpovídá skriptu pro `Remediate_stale_GroupPolicies.ps1` nápravu.
       [![Stránka nastavení skriptu proaktivní opravy služby Endpoint Analytics.](media/proactive-remediations-script-settings.png)](media/proactive-remediations-script-settings.png#lightbox)
1. Dokončete možnosti na stránce **Nastavení** s následujícími doporučenými konfiguracemi:
   - **Spustit tento skript pomocí přihlášených přihlašovacích údajů**: Tato akce je závislá na skriptu. Další informace najdete v [popisech skriptů](#bkmk_uea_scripts).
   - **Vymáhat kontrolu podpisu skriptu**: ne
   - **Spustit skript v 64 PowerShellu**: ne
1. Klikněte na **Další** a přiřaďte libovolné **značky oboru** , které potřebujete.
1. V kroku **přiřazení** vyberte skupiny zařízení, do kterých chcete balíček skriptu nasadit.
1. Dokončete krok **zkontrolovat + vytvořit** pro vaše nasazení.
1. V části **vytváření sestav** > **služby Endpoint Analytics – proaktivní nápravy**můžete zobrazit přehled stavu zjišťování a oprav.
       [![Sestava proaktivní nápravy služby Endpoint Analytics, stránku Přehled.](media/proactive-remediations-report-overview.png)](media/proactive-remediations-report-overview.png#lightbox)
1. Kliknutím na **stav zařízení** získáte podrobnosti o stavu jednotlivých zařízení v nasazení.
       [![Stav zařízení proaktivní opravy služby Endpoint Analytics.](media/proactive-remediations-device-status.png)](media/proactive-remediations-device-status.png#lightbox)


## <a name="endpoint-analytics-settings"></a><a name="bkmk_uea_set"></a>Nastavení služby Endpoint Analytics

Na stránce nastavení můžete vybrat **Obecné** nebo **základní**. Každé z těchto nastavení je popsáno níže:

### <a name="general"></a><a name="bkmk_uea_gen"></a>Všeobecně

Na stránce **Obecné** v části **Nastavení** můžete zjistit, jestli je povolená kolekce dat výkonu pro spuštění Intune. Když kliknete na **Start** , povolíte analýzu uživatelského prostředí, automaticky se pro všechna vaše zařízení povolí ve výchozím nastavení. Máte možnost přejít na uzel zásad shromažďování dat Intune a změnit sadu zařízení, na kterých se shromažďují záznamy o spouštění a přihlašování.


#### <a name="intune-data-collection-policy"></a><a name="bkmk_uea_profile"></a>Zásady shromažďování dat v Intune

Pokud chcete toto nastavení přiřadit k podmnožině zařízení, [vytvořte profil](/intune/configuration/device-profile-create#create-the-profile) s následujícími informacemi: 

  - **Název**: zadejte popisný název profilu, jako je například **zásada shromažďování dat Intune** .
   
  - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.
    
  - **Platforma**: Vyberte **Windows 10 a novější**.
   
  - **Typ profilu**: vyberte **sledování stavu systému Windows** .
   
  - Nakonfigurujte **Nastavení**:
   
       - **Sledování stavu**: výběrem **Povolit** Shromážděte informace o událostech ze zařízení s Windows 10.
    
    - **Rozsah**: vyberte **spouštěcí výkon** . 

  - Pomocí [značek oboru](/intune/configuration/device-profile-create#scope-tags) a [pravidel použitelnosti](/intune/configuration/device-profile-create#applicability-rules) můžete profil filtrovat na konkrétní skupiny nebo zařízení ve skupině, které splňují určitá kritéria.

> [!NOTE]
> Pro pokyny ke konfiguraci konektoru Configuration Manager data Connector je k dispozici zástupný symbol. Tato funkce ale není implementovaná v této úvodní privátní verzi Preview.

  [![Stránka Obecné nastavení pro službu Endpoint Analytics](media/settings-general.png)](media/settings-general.png#lightbox)

### <a name="baseline-management"></a><a name="bkmk_uea_baselines"></a>Správa standardních hodnot

Aktuální skóre a dílčí skóre můžete porovnat s ostatními nastavením standardních hodnot.

1. Pro **komerční medián**je k dispozici vestavěný směrný plán, který vám umožní porovnat vaše skóre s běžným podnikem.
1. Můžete vytvořit nové směrné plány na základě aktuálních metrik pro sledování průběhu nebo zobrazení regresí v průběhu času. Klikněte na tlačítko **vytvořit nový** a zadejte název nového směrného plánu. Doporučujeme použít název, který bude obsahovat datum, takže ho můžete snáze vybrat v rozevíracím seznamu na stránkách sestavy.
1. U každého tenanta je povolený limit 100 standardních hodnot. Můžete odstranit staré směrné plány, které už nepotřebujete.
1. Vaše aktuální metrika bude označena červeně a bude se zobrazovat jako znovu, pokud v sestavách spadají pod aktuální standardní hodnoty. Vzhledem k tomu, že je zcela normální metrika, která se pohybuje od dne do dne, můžete nastavit prahovou hodnotu regrese, která má výchozí hodnotu 10%. U této prahové hodnoty jsou metriky označeny jako znovu, pokud se na ně přecházejí více než 10%.

   [![Stránka nastavení směrného plánu služby Endpoint Analytics](media/settings-baseline.png)](media/settings-baseline.png#lightbox)

## <a name="troubleshooting"></a><a name="bkmk_uea_tshoot"></a>Při

Následující části vám pomůžou při řešení problémů, se kterými se můžete setkat.

### <a name="troubleshooting-startup-performance-device-enrollment"></a><a name="bkmk_uea_enrollment_tshooter"></a>Řešení potíží s registrací zařízení výkonu při spuštění

Pokud se na stránce Přehled zobrazuje skóre výkonu při spuštění, které se doprovází proužkovou kartou s informací o tom, že čeká na data, nebo pokud karta výkon zařízení výkonu při spuštění zobrazuje méně zařízení, než očekáváte, je třeba provést několik kroků, které můžete provést při odstraňování problému.

Nejdřív je zde stručný přehled omezení pro shromažďování dat o výkonu při spuštění:
1. Zařízení musí mít Windows 10 verze 1903 nebo novější.
2. Zařízení musí být připojená k Azure AD. V tuto chvíli nepodporujeme zařízení připojená k síti na pracovišti, i když aktivně zkoumáte proveditelnost přidávání této funkce do Windows.
3. Zařízení musí být Windows 10 Enterprise Edition. Windows 10 Home a Professional se v současné době nepodporují, i když aktivně zkoumá proveditelnost přidávání této funkce do Windows.

Všimněte si, že tyto problémy nebudou platit pro data přicházející z nadcházejícího konektoru Configuration Manager. bude moct shromažďovat data ze všech Configuration Manager klientských počítačů bez ohledu na konfiguraci verze, edice nebo adresáře.

V druhém najdete stručný kontrolní seznam pro řešení potíží:
1. Ujistěte se, že máte profil sledování stavu systému Windows, který je zaměřený na všechna zařízení, pro která chcete data o výkonu. Odkaz na tento profil můžete najít na stránce nastavení služby Endpoint Analytics nebo na něj přejít stejným způsobem jako jakýkoli jiný profil Intune. Podívejte se na kartu přiřazení a ujistěte se, že je přiřazená k očekávané sadě zařízení. 
1. Podívá se na to, která zařízení byla úspěšně nakonfigurovaná pro shromažďování dat. Tyto informace můžete zobrazit také na stránce Přehled profilů.  
   - Existuje známý problém, kdy se zákazníkům zobrazí Chyby přiřazení profilu, kde ovlivněná zařízení zobrazují kód chyby `-2016281112 (Remediation failed)`. Aktivně zkoumáme tento problém.
1. Zařízení, která byla úspěšně nakonfigurovaná pro shromažďování dat, se musí po povolení shromažďování dat restartovat a po zobrazení zařízení na kartě výkon zařízení musíte počkat až 24 hodin.
1. Pokud se vaše zařízení úspěšně nakonfigurovalo pro shromažďování dat, později se restartuje a po 24 hodinách ho nevidíte, může to být tím, že se zařízení nemůže dostat do našich koncových bodů kolekce. K tomuto problému může dojít, pokud vaše společnost používá proxy server a koncové body nebyly na proxy serveru povoleny. Další informace najdete v tématu [řešení potíží s koncovými body](#bkmk_uea_endpoints).


### <a name="endpoints"></a><a name="bkmk_uea_endpoints"></a>Bod

Aby bylo možné zaregistrovat zařízení do služby Endpoint Analytics, musí společnosti Microsoft odesílat požadovaná funkční data. Pokud vaše prostředí používá proxy server, použijte tyto informace k tomu, abyste mohli nakonfigurovat proxy server.

Pokud chcete povolit sdílení funkčních dat, nakonfigurujte proxy server tak, aby umožňoval následující koncové body:

> [!Important]  
> V případě ochrany osobních údajů a integrity dat systém Windows při komunikaci s požadovanými koncovými body sdílení dat kontroluje certifikát Microsoft SSL (připnutí certifikátů). Zachycení a kontrola SSL nejsou možné. Pokud chcete použít službu Endpoint Analytics, vylučte tyto koncové body z kontroly SSL.<!-- BUG 4647542 -->

| Koncový bod  | Funkce  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Slouží k odeslání [požadovaných funkčních dat](#bkmk_uea_datacollection) do koncového bodu shromažďování dat Intune. |
| `https://graph.windows.net` | Slouží k automatickému načítání nastavení při připojování hierarchie ke službě Endpoint Analytics (na Configuration Manager role serveru). Další informace najdete v tématu [konfigurace proxy serveru pro server systému lokality](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Slouží k synchronizaci kolekce zařízení a zařízení s nástrojem Endpoint Analytics (pouze v Configuration Manager role serveru). Další informace najdete v tématu [konfigurace proxy serveru pro server systému lokality](../plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |


### <a name="proxy-server-authentication"></a>Ověřování proxy serveru

Pokud vaše organizace používá proxy server ověřování pro přístup k Internetu, ujistěte se, že neblokuje data kvůli ověřování. Pokud váš proxy nepovoluje, aby zařízení odesílala tato data, nebudou se zobrazovat v Desktop Analytics.

#### <a name="bypass-recommended"></a>Nepoužívat (doporučeno)

Nakonfigurujte proxy servery tak, aby nevyžadovaly ověřování proxy serveru pro provoz do koncových bodů sdílení dat. Tato možnost je nejkomplexnější řešení. Funguje pro všechny verze Windows 10.  

#### <a name="user-proxy-authentication"></a>Ověřování proxy uživatelů

Nakonfigurovat zařízení tak, aby používala kontext přihlášeného uživatele pro ověřování proxy serveru. Tato metoda vyžaduje následující konfigurace:

- U zařízení je aktuální aktualizace kvality podporovaná pro podporovanou verzi Windows.

- Nakonfigurujte proxy na úrovni uživatele (proxy WinINET) v **nastavení proxy serveru** v síťové & internetovou skupinu nastavení Windows. Můžete použít také starší ovládací panel Možnosti Internetu.

- Ujistěte se, že uživatelé mají oprávnění k přístupu k koncovým bodům sdílení dat. Tato možnost vyžaduje, aby zařízení měla uživatele konzoly s oprávněními proxy serveru, takže tuto metodu nemůžete použít u zařízení bez periferních zařízení.

> [!IMPORTANT]
> Přístup k ověřování pomocí uživatelského proxy serveru je nekompatibilní s používáním rozšířené ochrany před internetovými útoky v programu Microsoft Defender. Toto chování je způsobeno tím, že toto **DisableEnterpriseAuthProxy** ověřování spoléhá na klíč registru `0`DisableEnterpriseAuthProxy nastavený na, zatímco ATP programu Microsoft Defender vyžaduje, `1`aby byl nastaven na. Další informace najdete v tématu [Konfigurace nastavení připojení počítače a připojení k Internetu v ochraně ATP v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

#### <a name="device-proxy-authentication"></a>Ověřování proxy zařízení

Tento přístup podporuje následující scénáře:

- Zařízení bez přihlášení, pokud se k Internetu přihlašuje nebo uživatelé zařízení nemají přístup k Internetu

- Ověřené proxy servery, které nepoužívají integrované ověřování systému Windows

- Pokud používáte také rozšířenou ochranu před internetovými útoky v programu Microsoft Defender

Tento přístup je nejsložitější, protože vyžaduje následující konfigurace:

- Ujistěte se, že zařízení mají přístup k proxy server prostřednictvím služby WinHTTP v kontextu místního systému. Pro konfiguraci tohoto chování použijte jednu z následujících možností:

  - Příkazový řádek`netsh winhttp set proxy`

  - Protokol WPAD (Web Proxy Auto-Discovery)

  - Transparentní proxy server

  - Nakonfigurujte proxy server WinINET v rámci zařízení pomocí následujících nastavení zásad skupiny: **nastavení proxy serveru na počítač (nikoli na uživatele)** (ProxySettingsPerUser = `1`).

  - Směrované připojení nebo použití překladu síťových adres (NAT)

- Nakonfigurujte proxy servery tak, aby umožňovaly účtům počítačů ve službě Active Directory přístup k koncovým bodům dat. Tato konfigurace vyžaduje, aby proxy servery podporovaly integrované ověřování systému Windows.  


## <a name="frequently-asked-questions"></a><a name="bkmk_uea_faq"></a>Nejčastější dotazy

### <a name="why-are-the-scripts-exiting-with-a-code-of-1"></a>Proč se skripty ukončí s kódem 1?

Skripty se ukončí s kódem 1 k signalizaci Intune, ke kterému by mělo dojít k nápravě. V takovém případě ukončení skriptu detekce s 1 znamená, že je tato náprava potřebná. Mnoho balíčků skriptů, které běží výhradně v CM, může zobrazovat vyhovující předpisy, ale ukončí kód 1. U těchto skriptů se ukončí s kódem 1, který není alarm, ale možná budete chtít ověřit, jestli zařízení správně opraví.

### <a name="why-did-the-update-stale-group-policies-script-return-with-error-0x87d00321"></a>Proč skript aktualizace zastaralých zásad skupiny vrátí chybu 0x87D00321?

0x87D00321 je chyba časového limitu spuštění skriptu. K této chybě obvykle dochází u počítačů, které jsou vzdáleně připojené. Možné zmírnění může být nasazení pouze do dynamické kolekce počítačů s interním připojením k síti.

## <a name="script-descriptions"></a><a name="bkmk_uea_scripts"></a>Popisy skriptů

Tato tabulka zobrazuje názvy skriptů, popisy, detekce, nápravy a konfigurovatelné položky. Soubory skriptu, jejichž názvy začínají `Detect` na, jsou skripty detekce. Skripty pro `Remediate`nápravu začínají na. Tyto skripty můžete zkopírovat z další části tohoto článku.

|Název skriptu|Popis|
|---|---|
|**Aktualizace zastaralých zásad skupiny** </br>`Detect_stale_Group_Policies.ps1` </br> `Remediate_stale_GroupPolicies.ps1`| Zjistí, zda je poslední Zásady skupiny aktualizace větší `7 days` než před.  </br>Upravte prahovou hodnotu pro 7 dní změnou hodnoty pro `$numDays` ve skriptu detekce. </br></br>Oprava probíhá spuštěním `gpupdate /target:computer /force` a`gpupdate /target:user /force`  </br> </br>Může pomoci omezit volání podpory související s připojením k síti při doručování certifikátů a konfigurací prostřednictvím Zásady skupiny. </br> </br> **Spusťte skript pomocí přihlášených přihlašovacích údajů**: Ano|
|**Restartujte službu Office Klikni a spusť.** </br> `Detect_Click_To_Run_Service_State.ps1` </br> `Remediate_Click_To_Run_Service_State.ps1`| Zjišťuje, jestli je služba Klikni a spusť nastavená na automatické spuštění a jestli je služba zastavená. </br> </br> Opraví nastavení služby tak, aby se spouštěla automaticky a spouštěla službu, pokud je zastavená. </br></br> Pomáhá opravovat problémy s tím, že se aplikace Win32 Microsoft 365 pro podnik nespustí, protože je zastavená služba Klikni a spusť. </br> </br> **Spusťte skript s použitím přihlášených přihlašovacích údajů**: ne|
|**Kontrolovat síťové certifikáty** </br>`Detect_Expired_Issuer_Certificates.ps1` </br>`Remediate_Expired_Issuer_Certificates.ps1`|Vyhledá certifikáty vydané certifikační autoritou v osobním úložišti nebo v počítači uživatele, jehož platnost vypršela nebo brzy vyprší. </br> Určete certifikační autoritu změnou hodnoty pro `$strMatch` ve skriptu detekce. Chcete-li `$expiringDays` vyhledat certifikáty s vypršenou platností, zadejte hodnotu 0 pro vyhledání certifikátů s vypršenou platností nebo zadejte jiný počet dní.  </br></br>Oprava vyzvednutím informačního oznámení uživateli. </br> Zadejte hodnoty `$Title` a `$msgText` s názvem a textem zprávy, které mají uživatelé vidět. </br> </br> Upozorňuje uživatele na certifikáty s vypršenou platností, které může být nutné obnovit. </br> </br> **Spusťte skript s použitím přihlášených přihlašovacích údajů**: ne|
|**Vymazat zastaralé certifikáty** </br>`Detect_Expired_User_Certificates.ps1` </br> `Remediate_Expired_User_Certificates.ps1`| Detekuje prošlé certifikáty vydané certifikační autoritou v osobním úložišti aktuálního uživatele. </br> Určete certifikační autoritu změnou hodnoty pro `$certCN` ve skriptu detekce. </br> </br> Opravuje odstraněním certifikátů, jejichž platnost vystavila certifikační autorita z osobního úložiště aktuálního uživatele. </br> Určete certifikační autoritu změnou hodnoty pro `$certCN` ve skriptu pro opravu. </br> </br> Vyhledá a odstraní prošlé certifikáty vydané certifikační autoritou z osobního úložiště aktuálního uživatele. </br> </br> **Spusťte skript pomocí přihlášených přihlašovacích údajů**: Ano|

## <a name="powershell-scripts"></a><a name="bkmk_uea_ps_scripts"></a>PowerShellové skripty

### <a name="detect_stale_group_policiesps1"></a>Detect_stale_Group_Policies. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_stale_Group_Policies.ps1
# Description:     Detect if Group Policy has been updated within number of days
# Notes:           Remediate if "Match", $numDays default value of 7, change as appropriate
#
#=============================================================================================================================

# Define Variables
$numDays = 7

try {
    $gpResult = gpresult /R | Select-String -pattern "Last time Group Policy was applied:" | Select-Object -last 1

    if ($gpResult){
    [int]$lastGPUpdateDays = (New-TimeSpan -Start $lastGPUpdateDate -End (Get-Date)).Days
        if ($lastGPUpdateDays -gt $numDays){
            #We want within last $numDays so we get "Match"
            Write-Host "Match"
            exit 1
        }
        else {
            #Script succeeds but > $numDays since last update so remediate
            #Exit 1 for Intune and "Match" for ConfigMan
            Write-Host "No_Match"
            exit 0
        }
    }
}
catch {
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_stale_grouppoliciesps1"></a>Remediate_stale_GroupPolicies. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_stale_GroupPolicies.ps1
# Description:     This script triggers Group Policy update
# Notes:           No variable substitution needed
#
#=============================================================================================================================

try{
    $compGP = gpupdate /target:computer /force | out-string
    $userGP = gpupdate /target:user /force | out-string
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="detect_click_to_run_service_stateps1"></a>Detect_Click_To_Run_Service_State. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Click_To_Run_Service_State.ps1
# Description:     Detect if Office 16 installed and if "Click to Run Service" is running.
# Notes:           No variable substitution should be necessary
#
#=============================================================================================================================

# Define Variables
$curSvcStat,$svcCTRSvc,$errMsg = "","",""

# Main script
If (-not (Test-Path -Path 'hklm:\Software\Microsoft\Office\16.0')){
    Return "Office 16.0 (or greater) not present on this machine"
    exit 0   
} 

Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
}

Catch{    
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}

If ($curSvcStat -eq "Running"){
    Write-Output $curSvcStat
    exit 0                        
}
Else{
    If($curSvcStat -eq "Stopped"){
    Write-Output $curSvcStat
    exit 1     
    }
}
Else{
    Write-Error "Error: " + $errMsg
    exit 1
}
```

### <a name="remediate_click_to_run_service_stateps1"></a>Remediate_Click_To_Run_Service_State. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Click_To_Run_Service_State.ps1
# Description:     Start the "Click to Run Service" and change its startup type to Automatic
#       Notes:     No variable substitution needed
#
#=============================================================================================================================

# Define Variables
$svcCur = "ClickToRunSvc"
$curSvcStat,$svcCTRSvc,$errMsg = "","",""
$ctr = 0

# Main script
# Make sure nothing has changed since detection, the service exists and is stopped
Try{        
    $svcCTRSvc = Get-Service "ClickToRunSvc"
    $curSvcStat = $svcCTRSvc.Status
    }

Catch{    
    $errMsg = $_.Exception.Message
    }
        
# If the service got started between detection and now (nested if) then return
# If the service got uninstalled or corrupted between detection and now (else) then return the "Error: " + the error
If ($curSvcStat -ne "Stopped"){
    If ($curSvcStat -eq "Running"){
        return
    }
    Else{
        return "Error: " + $errMsg
    }
}

# Service should be there and stopped, change the startup type and start
Try{        
    Set-Service $svcCur -StartupType Automatic
    Start-Service $svcCur
    $svcCTRSvc = Get-Service $svcCur
    $curSvcStat = $svcCTRSvc.Status
        While ($curSvcStat.Equals("Stopped")){
            Start-Sleep -Seconds 5
            ctr++
            if(ctr == 12){
                Return "Service could not be started after 60 seconds"
                break
            }
        }
    }

Catch{    
    $errMsg = $_.Exception.Message
    Return $errMsg
    }

Return $curSvcStat
```

### <a name="detect_expired_issuer_certificatesps1"></a>Detect_Expired_Issuer_Certificates. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_Issuer_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" in either Machine
#                  or User certificate store
# Notes:           Change the value of the variable $strMatch from "CN=<your CA here>" to "CN=..."
#                  For testing purposes the value of the variable $expiringDays can be changed to a positive integer
#                  Don't change the $results variable
#
#=============================================================================================================================

# Define Variables
$results = @()
$expiringDays = 0
$strMatch = "CN=<your CA here>"

try
{
    $results = @(Get-ChildItem -Path Cert:\LocalMachine\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch})
    $results += @(Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays $expiringDays | where {$_.Issuer -match $strMatch}) 
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        #No matching certificates, do not remediate
        Write-Host "No_Match"        
        exit 0
    }   
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_issuer_certificatesps1"></a>Remediate_Expired_Issuer_Certificates. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_Issuer_Certificates.ps1
# Description:     Raise a Toast Notification if expired certificates issued by "CN=..."
#                  to user or machine on the machine where detection script found them. No remediation action besides
#                  the Toast is taken.
# Notes:           Change the values of the variables $Title and $msgText
#
#=============================================================================================================================

## Raise toast to have user contact whoever is specified in the $msgText

# Define Variables
$delExpCert = 0
$Title = "Title"
$msgText = "message"

# Main script
[Windows.UI.Notifications.ToastNotificationManager, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.UI.Notifications.ToastNotification, Windows.UI.Notifications, ContentType = WindowsRuntime] | Out-Null
[Windows.Data.Xml.Dom.XmlDocument, Windows.Data.Xml.Dom.XmlDocument, ContentType = WindowsRuntime] | Out-Null

$APP_ID = '{1AC14E77-02E7-4E5D-B744-2EB1AE5198B7}\WindowsPowerShell\v1.0\powershell.exe'

$template = @"
<toast>
    <visual>
        <binding template="ToastText02">
            <text id="1">$Title</text>
            <text id="2">$msgText</text>
        </binding>
    </visual>
</toast>
"@

$xml = New-Object Windows.Data.Xml.Dom.XmlDocument
$xml.LoadXml($template)
$toast = New-Object Windows.UI.Notifications.ToastNotification $xml
[Windows.UI.Notifications.ToastNotificationManager]::CreateToastNotifier($APP_ID).Show($toast)
```

### <a name="detect_expired_user_certificatesps1"></a>Detect_Expired_User_Certificates. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Detect_Expired_User_Certificates.ps1
# Description:     Detect expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=...".
#                  Don't change $results
#
#=============================================================================================================================

# Define Variables
$results = 0
$certCN = "CN=<your CA here>"

try
{   
    $results = Get-ChildItem -Path Cert:\CurrentUser\My -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)}
    if (($results -ne $null)){
        #Below necessary for Intune as of 10/2019 will only remediate Exit Code 1
        Write-Host "Match"
        Return $results.count
        exit 1
    }
    else{
        Write-Host "No_Match"
        exit 0
    }    
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

### <a name="remediate_expired_user_certificatesps1"></a>Remediate_Expired_User_Certificates. ps1

```powershell
#=============================================================================================================================
#
# Script Name:     Remediate_Expired_User_Certificates.ps1
# Description:     Remove expired certificates issued by "CN=<your CA here>" to User
# Notes:           Change the value of the variable $certCN from "CN=<your CA here>" to "CN=..."
#
#=============================================================================================================================

# Define Variables
$certCN = "CN=<your CA here>"

try
{
    Get-ChildItem -Path cert:\CurrentUser -Recurse -ExpiringInDays 0 | where {$_.Issuer -eq($certCN)} | Remove-Item
    exit 0
}
catch{
    $errMsg = $_.Exception.Message
    Write-Error $errMsg
    exit 1
}
```

## <a name="endpoint-analytics-data-privacy"></a><a name="bkmk_uea_privacy"></a>Data služby Endpoint Analytics – ochrana osobních údajů

### <a name="data-flow"></a>Tok dat

Následující obrázek znázorňuje způsob, jakým jsou povinná funkční data z jednotlivých zařízení přenášena prostřednictvím našich datových služeb, přechodného úložiště a vašeho tenanta. Data procházejí prostřednictvím našich stávajících podnikových kanálů bez spoléhání na diagnostická data Windows.

[![Diagram toku dat zkušeností uživatele](media/dataflow.png)](media/dataflow.png#lightbox)

1. Nakonfigurujte zásady **shromažďování dat Intune** pro zaregistrovaná zařízení. Ve výchozím nastavení se tato zásada při **spuštění** služby Endpoint Analytics přiřadí všem zařízením. Přiřazení můžete ale kdykoli [změnit](#bkmk_uea_set) na podmnožinu zařízení nebo vůbec žádná zařízení.

2. Zařízení odesílají požadovaná funkční data.

    - Pro zařízení Intune s přiřazenou zásadou se data odesílají z rozšíření pro správu Intune. Další informace najdete v tématu [požadavky](#bkmk_uea_prereq).
    - U Configuration Manager spravovaných zařízení můžou data taky přesměrovat do služby Microsoft Endpoint Management prostřednictvím konektoru nástroje ConfigMgr. Konektor nástroje ConfigMgr je připojen ke cloudu. Vyžaduje jenom připojení k tenantovi Intune, ale nezapne spolusprávu.

> [!Note]  
> Data potřebná k výpočtu skóre spouštění pro zařízení se generují během spouštění. V závislosti na nastavení napájení a chování uživatelů může trvat i týdny, než se zařízení správně přiřadilo k zásadě, aby zobrazovalo skóre spouštění v konzole pro správu.  

3. Služba Microsoft Endpoint Management zpracovává data pro každé zařízení a v konzole pro správu zveřejňuje výsledky jednotlivých zařízení i organizačních agregací pomocí rozhraní API pro MS Graph.

Průměrná latence od konce do konce je zhruba 12 hodin a je zavedená v době, kdy bude trvat každodenní zpracování. Všechny ostatní části toku dat jsou téměř v reálném čase.

### <a name="data-collection"></a><a name="bkmk_uea_datacollection"></a>Shromažďování dat

Základní funkce služby Endpoint Analytics v současné době shromažďují informace přidružené k záznamům o výkonu spouštění, které spadají do [identifikovaných](https://docs.microsoft.com/mem/intune/protect/privacy-data-collect#identified-data) a [pseudonymních](https://docs.microsoft.com/mem/intune/protect/privacy-data-collect#pseudonymized-data) kategorií. Jak přidáváme další funkce v průběhu času, shromážděná data se budou podle potřeby lišit. Aktuálně shromažďované hlavní databody:

#### <a name="identified-data"></a>Identifikované údaje

- Informace o inventáři hardwaru
  - **nastavit:** Výrobce zařízení
  - **model:** Model zařízení
  - **deviceClass:** Klasifikace zařízení. Například Desktop, Server nebo mobilní zařízení.
  - **Země:** Nastavení oblasti zařízení
- Inventář aplikací, například
  - **Název:** Systému
  - **Ver:** Verze aktuálního operačního systému.
  
#### <a name="pseudonymized-data"></a>Pseudonymizované údaje

- Diagnostické informace a informace o výkonu a použití svázané s uživatelem a/nebo zařízením
  - **logOnId**
  - **ID_spouštění:** ID spuštění systému
  - **coreBootTimeInMilliseconds:** Čas pro základní spuštění
  - **totalBootTimeInMilliseconds:** Celkový čas spuštění
  - **updateTimeInMilliseconds:** Doba, po kterou se aktualizace operačního systému dokončí
  - **gpLogonDurationInMilliseconds**: čas, kdy se mají zpracovat zásady skupiny
  - **desktopShownDurationInMilliseconds:** Čas, kdy se má načítat plocha (Explorer. exe)
  - **desktopUsableDurationInMilliseconds:** Čas, kdy se má použít Desktop (Explorer. exe)
  - **topProcesses:** Seznam procesů načtených během spouštění s názvem, včetně statistik využití procesoru a podrobností aplikace (název, vydavatel, verze) Například *{\"Process\":\"Svchost\",\"CpuUsage\": 43,\"ProcessFullPath\":\"C:\\\\Windows\\\\system32\\\\Svchost. exe\",\"ProductName\":\"operační systém&reg; &reg; \"Microsoft Windows,\"Vydavatel\":\"Microsoft Corporation\",\"ProductVersion\":\"10.0.18362.1}\"*
- Data zařízení nesvázaná se zařízením nebo uživatelem (jsou-li svázaná se zařízením nebo uživatelem, Intune s nimi nakládá jako s identifikovanými údaji)
  - **ID:** Jedinečné ID zařízení, které používá web Windows Update
  - **LocalId:** Místně definované jedinečné ID pro zařízení. Nejedná se o název zařízení srozumitelně pro čtení. Nejpravděpodobnější s hodnotou uloženou v HKLM\Software\Microsoft\SQMClient\MachineId.
  - **aaddeviceid:** ID zařízení Azure Active Directory
  - **OrgID:** Jedinečný identifikátor GUID reprezentující tenanta Microsoft O365
  
> [!Important]  
> Naše zásady pro zpracování dat jsou popsané v [Microsoft Intune prohlášení o zásadách ochrany osobních údajů](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement). Zákaznická data používáme jenom k poskytování služeb, ke kterým jste se zaregistrovali. Jak je popsáno v procesu připojování, anonymizovatme a agregujeme skóre ze všech zaregistrovaných organizací, aby se směrné plány zachovaly v aktuálním stavu.


### <a name="resources"></a>Zdroje a prostředky

Další informace o souvisejících aspektech ochrany osobních údajů najdete v následujících článcích:

- [Microsoft Intune – prohlášení o zásadách ochrany osobních údajů](https://docs.microsoft.com/legal/intune/microsoft-intune-privacy-statement)
- [Dodržování předpisů pro Windows 10 a ochranu osobních údajů](https://docs.microsoft.com/windows/privacy/windows-10-and-privacy-compliance)
- [Licenční podmínky a dokumentace](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  
- [Zabezpečení a ochrana osobních údajů v Microsoft Azure datových Centre](https://azure.microsoft.com/global-infrastructure/)  
- [Jistota v důvěryhodném cloudu](https://azure.microsoft.com/overview/trusted-cloud/)  
- [Centrum zabezpečení](https://www.microsoft.com/trustcenter)  
