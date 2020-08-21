---
title: Posouzení kompatibility
titleSuffix: Configuration Manager
description: Přečtěte si o vyhodnocení kompatibility pro aplikace a ovladače pro Windows v Desktop Analytics.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: c9268514b43f4f728d3fff4715d4d71308a712f3
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699071"
---
# <a name="compatibility-assessment-in-desktop-analytics"></a>Posouzení kompatibility v Desktop Analytics

Posouzení upgradu v předchozích řešeních bylo obecné, například: nutná pozornost nebo oprava k dispozici. Neposkytuje žádný vizuální indikátor pro určení priorit aplikací nebo ovladačů s problémy nebo přehledy upgradu. Funkce Desktop Analytics nahrazuje tuto funkci **riziku kompatibility**. Desktop Analytics zobrazuje posouzení pro aplikace pouze v zobrazení nasazení pro scénář před upgradem. Kategorizují aplikace založené na Insights, které Microsoft získá z počítačů zahrnutých v aktuálním plánu nasazení.

Desktop Analytics používá následující kategorie posouzení kompatibility:

- **Nízká**: Služba nenalezla žádné signály k uvedení této aplikace na riziko pro upgrade Windows. Bude nejspíš pracovat na cílovém operačním systému tak, jak je.

- **Střední**: analýza znamená, že aplikace může mít postižené funkce, i když náprava je pravděpodobně možná.

- **Vysoká**: aplikace je skoro v průběhu upgradu nebo po ní téměř neúspěšná. Může to být potřeba k nápravě.

- **Neznámé**: aplikace se nehodnotila. Neexistují žádné další přehledy, jako je například *MS známé problémy* nebo *připravené pro Windows*.

V seznamu prostředků aplikací nebo ovladačů v plánu nasazení uvidíte tuto hodnotu pro každý Asset ve sloupci **rizika kompatibility** .

## <a name="app-risk-assessment"></a>Posouzení rizika aplikace

![Diagram zdrojů vyhodnocování rizik aplikace](media/app-risk-assessment-sources.png)

K dispozici je několik zdrojů, které Desktop Analytics používá k vygenerování hodnocení hodnocení pro aplikace:

- [Známé problémy společnosti Microsoft](#microsoft-known-issues)
- [Připraveno pro Windows](#ready-for-windows)
- [Rozšířené přehledy](#advanced-insights)

Posouzení pro každý zdroj v aplikaci můžete najít v části Desktop Analytics. V seznamu prostředků aplikace v plánu nasazení vyberte jednotlivou aplikaci a otevřete její informační podokno s vlastnostmi. Uvidíte celkové doporučení a úroveň posouzení. V části **rizikové faktory kompatibility** se zobrazují podrobnosti o těchto hodnoceních.

> [!TIP]
> Pokud podokno podrobností aplikace nezobrazuje posouzení kompatibility, může to být způsobeno tím, že je nastavení **Podrobnosti verze aplikace** vypnuté. Ve výchozím nastavení je vypnutá a kombinuje všechny verze aplikací se stejným názvem a vydavatelem. Služba stále vyhodnotila rizika kompatibility pro každou verzi. Pokud chcete zobrazit vyhodnocení rizik kompatibility konkrétní verze aplikace, zapněte si **Podrobnosti o verzích aplikací** . Další informace najdete v tématu [plánování prostředků](about-deployment-plans.md#plan-assets).

## <a name="microsoft-known-issues"></a>Známé problémy společnosti Microsoft

Pro všechny známé problémy se v databázi pro desktopovou analýzu prohlíží databáze Microsoft App Compatibility. Tato databáze používá k určení všech stávajících bloků kompatibility pro veřejně dostupné aplikace od Microsoftu nebo jiných vydavatelů. Tato kontroly platí pouze pro cílový operační systém pro vybraný plán nasazení.

V podokně vlastností aplikace se zobrazí následující problémy jako **MS známé problémy**:

### <a name="asset-is-removed-during-upgrade"></a>Během upgradu se odebral prostředek.

V systému Windows byly zjištěny problémy s kompatibilitou s aplikací nebo ovladačem. Asset nebude migrován na novou verzi operačního systému. K pokračování upgradu není nutná žádná akce. Nainstalujte do nové verze operačního systému kompatibilní verzi aplikace nebo ovladače.

<!-- 3594545 -->
Systém Windows může tyto prostředky částečně nebo zcela odebrat:

- Úplné odebrání: Instalační program systému Windows zcela odebere aplikaci nebo ovladač ze zařízení během upgradu.
- Částečné odebrání: Instalační program systému Windows částečně odebere ze zařízení aplikaci nebo ovladač. Až budete upgradovat Windows, musíte ho ručně odinstalovat.

V obou případech může uživatel po upgradu Windows použít aplikaci nebo hardware, který je k ovladači přidružený.

Pokud se chcete podívat na toto doporučení na portálu Desktop Analytics:

1. V plánu nasazení vyberte **připravit pilotní**nasazení.
1. Vyberte kartu **aplikace** .
1. Vyberte aplikaci a potom v bočním podokně zobrazte faktory rizika kompatibility a doporučení.

[![Snímek obrazovky s doporučením Asset Analytics na portálu pro Desktop Analytics](media/3594545-app-removed.png)](media/3594545-app-removed.png#lightbox)

### <a name="blocking-upgrade"></a>Blokování upgradu

Systém Windows zjistil blokující problémy a nemůže aplikaci odebrat během upgradu. Nemusí fungovat na nové verzi operačního systému. Před upgradem aplikaci odeberte. Přeinstalujte ji a otestujte ji na nové verzi operačního systému.

### <a name="blocking-upgrade-but-can-be-reinstalled-after-upgrading"></a>Blokování upgradu, ale po upgradu se dá přeinstalovat.

Aplikace je kompatibilní s novou verzí operačního systému, ale nemigruje se. Před upgradem systému Windows aplikaci odeberte. Znovu ji nainstalujte na novou verzi operačního systému.

### <a name="blocking-upgrade-update-application-to-newest-version"></a>Blokování upgradu, aktualizace aplikace na nejnovější verzi

Existující verze aplikace není kompatibilní s novou verzí operačního systému a nebude migrována. K dispozici je kompatibilní verze aplikace. Před upgradem aplikaci aktualizujte.

### <a name="disk-encryption-blocking-upgrade"></a>Upgrade blokování šifrování disku

Funkce šifrování aplikace zablokují upgrade. Před upgradem systému Windows zakažte funkci šifrování a po upgradu ji povolte.

### <a name="does-not-work-with-new-os-but-wont-block-upgrade"></a>Nefunguje s novým operačním systémem, ale neblokuje upgrade

Aplikace není kompatibilní s novou verzí operačního systému, ale neblokuje upgrade. K pokračování upgradu není nutná žádná akce. Nainstalujte kompatibilní verzi aplikace na novou verzi operačního systému.

### <a name="does-not-work-with-new-os-and-will-block-upgrade"></a>Nefunguje s novým operačním systémem a bude blokovat upgrade

Aplikace není kompatibilní s novou verzí operačního systému a zablokuje upgrade. Před upgradem aplikaci odeberte. Je možné, že je k dispozici kompatibilní verze aplikace.

### <a name="evaluate-application-on-new-os"></a>Zhodnotit aplikaci pro nový operační systém

Systém Windows provede migraci aplikace, ale zjistila problémy, které mohou ovlivnit výkon aplikace v nové verzi operačního systému. K pokračování upgradu není nutná žádná akce. Otestujte aplikaci na nové verzi operačního systému.

### <a name="may-block-upgrade-test-application"></a>Může blokovat upgrade, testovací aplikaci

Systém Windows zjistil problémy, které mohou narušit upgrade, ale vyžadují další šetření. Otestuje chování aplikace během upgradu. Pokud se upgrade zablokuje, odeberte ho před upgradem. Pak ji znovu nainstalujte a otestujte v nové verzi operačního systému.

### <a name="multiple"></a>Několik

Aplikace má vliv na více problémů. Vyberte **dotaz** pro zobrazení podrobností o problémech zjištěných systémem Windows.

### <a name="reinstall-application-after-upgrading"></a>Po upgradu přeinstalovat aplikaci

Aplikace je kompatibilní s novou verzí operačního systému, ale po upgradu systému Windows ji musíte znovu nainstalovat. Proces upgradu odebere aplikaci. K pokračování upgradu není nutná žádná akce. Přeinstalujte aplikaci na novou verzi operačního systému.

### <a name="safeguards"></a>Ochrana

<!-- 5746559 -->

Data o kompatibilitě Windows klasifikují některé aplikace a ovladače s *ochranou*, což může způsobit, že aktualizace Windows 10 selže nebo se vrátí zpět. Může se také upgradovat systém Windows, ale aplikace nebo ovladač se odebere. Pomocí nástroje Desktop Analytics teď můžete tato ochranná opatření identifikovat předem, abyste mohli prostředek napravit před nasazením aktualizace.

1. Na portálu Desktop Analytics vyberte plán nasazení.

1. V nabídce vyberte **plán assetů** a přepněte na kartu **aplikace** .

1. Filtrováním sloupce název zobrazíte položky s hodnotami, které obsahují slovo `Safeguard` . Kliknutím na výsledek zobrazíte další informace.

    > [!NOTE]
    > Tato položka není skutečnou aplikací, která je nainstalovaná na vašich zařízeních. Je to zástupný symbol, který vám usnadní identifikaci aplikací nebo ovladačů ve vašem prostředí pomocí značky kompatibility s ochranou.

1. V části doporučení kliknutím na odkaz zobrazíte *Další informace*. Tento odkaz otevře web Windows s aktuálním seznamem aplikací nebo ovladačů se značkou zabezpečení.

1. Porovnejte aktuální publikovaný seznam se seznamem prostředků ve vašem prostředí. Opravte všechny potenciálně problematické aplikace nebo ovladače tak, že aktualizujete na kompatibilní verzi.

[![Snímek obrazovky s ochranou aplikace v Desktop Analytics](media/5746559-safeguards.png)](media/5746559-safeguards.png#lightbox)

## <a name="ready-for-windows"></a>Připraveno pro Windows

Stav přijetí je založený na informacích z komerčních zařízení, která sdílejí data s Microsoftem. Stav je integrován s příkazy podpory od dodavatelů softwaru.

Desktop Analytics poskytuje stav přijetí pro každou verzi assetu, která se nachází v komerčních zařízeních. Tento stav nezahrnuje data ze zařízení uživatelů nebo zařízení, která nesdílejí data. Stav nemusí být zástupcem míry přijetí ve všech zařízeních s Windows 10.

Možné kategorie:

- **Vysoce přijato**: Tato aplikace nainstalovala aspoň 100 000 komerční zařízení s Windows 10.

- **Přijato**: Tato aplikace nainstalovala aspoň 10 000 komerční zařízení s Windows 10.

- **Nedostatečná data**: příliš málo komerčních zařízení s Windows 10 nesdílí informace pro tuto aplikaci, aby mohla společnost Microsoft zařazovat své přijetí.

- **Vývojář kontaktu**: v této verzi aplikace může dojít k problémům s kompatibilitou. Společnost Microsoft doporučuje kontaktovat poskytovatele softwaru a získat další informace.

- **Neznámé**: k dispozici nejsou žádné informace pro tuto verzi této aplikace. Informace mohou být k dispozici pro jiné verze aplikace.

### <a name="support-statement"></a>Příkaz support

Pokud poskytovatel softwaru podporuje jednu nebo více verzí této aplikace ve Windows 10, zobrazí se v podokně Vlastnosti aplikace tento příkaz. V části rizikové faktory kompatibility se podívejte na **příkaz Support (podpora**).

## <a name="advanced-insights"></a>Rozšířené přehledy

Pomocí těchto dalších přehledů můžete také detekovat problémy s nástrojem Desktop Analytics:

### <a name="adopted-version-available"></a>Přijatá verze je k dispozici.

Existuje jiná verze této aplikace, kterou vysoce přijali jiní zákazníci. Tento signál používá data o přijetí z ekosystému systému Windows. Pokud existují nějaké blokující upgrady s aktuální verzí, zvažte místo toho nasazení alternativní verze. Pokud chcete najít alternativní verze přijaté aplikace, přečtěte si téma stav aplikace v části příprava výroby.

### <a name="driver-dependency"></a>Závislost ovladače

Aplikace závisí na ovladači. Desktop Analytics doporučuje aplikaci pro pilotní testování, aby zjistila jakékoli regrese. Pokud máte nějaké problémy, kontaktujte vydavatele, aby požádal o verzi kompatibilní s Windows 10.

### <a name="additional-insights"></a>Další přehledy

<!-- 4021225 -->
Když aktualizujete Configuration Manager lokalitu a klienty na verzi 1906, klienti také nahlásí tyto další přehledy, když je úroveň diagnostických dat nastavena na hodnotu rozšířené omezení:

> [!Important]  
> Pokud chcete plně využít nové funkce Configuration Manager, po aktualizaci lokality aktualizujte také klienty na nejnovější verzi. Tento scénář není funkční, dokud nebude verze klienta zároveň nejnovější.

#### <a name="16-bit-apps"></a>16bitové aplikace

Odeberte všechny 16bitové komponenty z aplikací a nahraďte je pomocí 32 a 64 bitů ekvivalentů. Další informace najdete v tématu [Windows Vista a Windows Server 2008 Developer Story: Kompatibilita aplikací kuchařka](/previous-versions/aa480152\(v=msdn.10\)).

Druhou možností je povolit počítač se systémem NT Virtual DOS (NTVDM) pro podporu Windows 10.

#### <a name="requires-admin-privileges"></a>Vyžaduje oprávnění správce.

Aplikace vyžaduje, aby uživatel měl přístup správce k zařízení. Pro tyto aplikace použijte manifest aplikace, který vyžaduje oprávnění správce. Další informace najdete v tématu [Vytvoření a vložení manifestu aplikace](/previous-versions/bb756929\(v=msdn.10\)).

Desktop Analytics doporučuje aplikaci pro pilotní testování, aby zjistila jakékoli regrese.

#### <a name="java-dependency"></a>Závislost Java

Mnoho aplikací Java spoléhá na samostatně instalované Java Runtime Environment (JRE). I když starší verze JRE můžou i nadále fungovat ve Windows 10, podporuje Oracle jenom nejnovější verze JRE. Použití staršího nepodporovaného JRE může mít ohrožení zabezpečení. Ověřte, že vaše aplikace běží na nejnovějších verzích JRE.

#### <a name="not-dpi-aware"></a>Nepodporující rozlišení DPI

Aplikace může zobrazit problémy s pokročilými rozlišeními obrazovky ve Windows 10. Použijte manifest aplikace, abyste se vyhnuli jakýmkoli problémům s rozlišením vysoké úrovně DPI. Další informace najdete v tématu [manifesty aplikací](/windows/desktop/SbsCs/application-manifests).

Desktop Analytics doporučuje aplikaci pro pilotní testování, aby zjistila jakékoli regrese.

#### <a name="silverlight-framework"></a>Rozhraní Silverlight

Microsoft doporučuje, aby aplikace nezaložené na prohlížeči nepoužívaly technologii Silverlight. Datum ukončení podpory pro Silverlight 5 je říjnu 2021.

Většina současných webových prohlížečů nepodporuje Silverlight.

| Prohlížeč | Podpora |
|---------|---------|
| Google Chrome | Konec podpory: září 2015 |
| Firefox | Konec podpory: březen 2017 |
| Microsoft Edge | Není dostupný žádný modul plug-in. |

Desktop Analytics doporučuje aplikaci pro pilotní testování, aby zjistila jakékoli regrese.

#### <a name="net-framework-1011"></a>.NET Framework 1.0/1.1

Verze .NET Framework 1,0 není ve Windows 10 podporovaná. Verze 1,1 není kompatibilní s Windows 10. Pokud je aplikace od vydavatele třetí strany, obraťte se na dodavatele, aby požádal o verzi kompatibilní s Windows 10. V opačném případě znovu sevývojte aplikaci tak, aby používala podporovanou verzi rozhraní .NET.

#### <a name="net-framework-2030"></a>.NET Framework 2.0/3.0

Rozhraní .NET 2,0 a 3,5 jsou podporovaná ve Windows 10. Možná budete muset povolit funkci Windows. Další informace najdete v tématu [instalace .NET Framework 3,5 ve Windows 10](/dotnet/framework/install/dotnet-35-windows-10).

#### <a name="ui-access"></a>Přístup k uživatelskému rozhraní

Aplikace s přístupem k UŽIVATELSKÉmu rozhraní můžou obejít úroveň řízení uživatelského rozhraní a řídit tak vstup do oken s vyšším oprávněním na ploše. Toto nastavení použijte jenom pro aplikace technologie usnadnění uživatelského rozhraní.

Pokud v aplikaci nepoužíváte funkce přístupnosti, nastavte příznak přístup k uživatelskému rozhraní v manifestu aplikace na hodnotu NEPRAVDA. Další informace najdete v tématu [Vytvoření a vložení manifestu aplikace](/previous-versions/bb756929\(v=msdn.10\)).

Desktop Analytics doporučuje aplikaci pro pilotní testování, aby zjistila jakékoli regrese.

## <a name="driver-risk-assessment"></a>Posouzení rizika ovladače

Desktop Analytics také obsahuje seznam a skupiny podle dostupnosti všech ovladačů, které nebudou migrovány na verzi operačního systému.

Posouzení můžete najít na ovladači v části Desktop Analytics. V seznamu prostředků ovladače v plánu nasazení vyberte jednotlivý ovladač a otevřete jeho podokno s informačním panelem vlastností. Uvidíte celkové doporučení a úroveň posouzení. V části **rizikové faktory kompatibility** se zobrazují podrobnosti o těchto hodnoceních.

| Dostupnost ovladače | Je vyžadována akce? | Význam | Pokyny |
|---------------------|------------------|---------------|----------|
| K dispozici v krabicích | Ne, jenom pro povědomí | Aktuálně nainstalovaná verze aplikace nebo ovladače nebude migrována na novou verzi operačního systému. Kompatibilní verze je nainstalována s novou verzí operačního systému. | K pokračování upgradu není nutná žádná akce. |
| Importovat z web Windows Update | Ano | Aktuálně nainstalovaná verze ovladače nebude migrována na novou verzi operačního systému. Kompatibilní verze je k dispozici z web Windows Update. | Pokud počítač automaticky obdrží aktualizace z web Windows Update, není vyžadována žádná akce. V opačném případě importujte nový ovladač z web Windows Update po upgradu Windows. |
| K dispozici v krabicích a z web Windows Update | Ano | Aktuálně nainstalovaná verze ovladače nebude migrována na novou verzi operačního systému. I když je během upgradu nainstalován nový ovladač, je k dispozici novější verze z web Windows Update. | Pokud počítač automaticky obdrží aktualizace z web Windows Update, není vyžadována žádná akce. V opačném případě importujte nový ovladač z web Windows Update po upgradu Windows. |
| Obraťte se na dodavatele. | Ano | Ovladač nebude migrován na novou verzi operačního systému a Desktop Analytics nemůže najít kompatibilní verzi. | V případě řešení se poraďte se nezávislým dodavatelem hardwaru (IHV), který vyrábí ovladač, nebo výrobcem OEM (Original Equipment Manufacturer), který toto zařízení poskytl. |

## <a name="see-also"></a>Viz také:

Zvýhodnění centra FastTrack pro Windows 10 poskytuje přístup k **zajištění přístupu k desktopové aplikaci**. Tato výhoda je nová služba určená k řešení problémů s Windows 10 a Microsoft 365 aplikacemi pro zajištění kompatibility s podnikovou sítí. Další informace najdete v tématu [zajištění pro desktopovou aplikaci](/fasttrack/win-10-desktop-app-assure).