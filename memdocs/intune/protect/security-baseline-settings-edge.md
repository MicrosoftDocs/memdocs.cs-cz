---
title: Nastavení standardních hodnot zabezpečení Intune pro Microsoft Edge
titleSuffix: Microsoft Intune
description: Nastavení standardních hodnot zabezpečení, které Intune podporuje pro správu prohlížeče Microsoft Edge
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
zone_pivot_groups: edge-baseline-versions
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed235acefe62b7c432351273d1defe9db89f0f60
ms.sourcegitcommit: 7b4d4bc6ec7d6e551d73fa4320984edef606c63d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "91008375"
---
<!-- Pivots in use: 
::: zone pivot="edge-october-2019"
::: zone-end

::: zone pivot="edge-april-2020"
::: zone-end

::: zone pivot="edge-october-2019,edge-april-2020"
::: zone-end
-->

# <a name="microsoft-edge-baseline-settings-for-intune"></a>Základní nastavení Microsoft Edge pro Intune

Zobrazení standardních nastavení webového prohlížeče Microsoft Edge, která jsou podporována nástrojem Microsoft Intune. Výchozí nastavení Microsoft Edge představuje doporučenou konfiguraci pro prohlížeče Microsoft Edge a nemusí odpovídat výchozím hodnotám pro jiné standardní hodnoty zabezpečení.

::: zone pivot="edge-october-2019"

> [!NOTE]
> Směrný plán Microsoft Edge pro říjen 2019 je v Public Preview.

Chcete-li aktualizovat profil standardních hodnot zabezpečení na nejnovější verzi tohoto směrného plánu, přečtěte si téma [Změna základní verze profilu](../protect/security-baselines.md#change-the-baseline-version-for-a-profile).

::: zone-end
::: zone pivot="edge-april-2020"

**Směrný plán Microsoft Edge pro duben 2020 (Edge verze 80)**  
Tato verze standardních hodnot zabezpečení nahrazuje předchozí verze. Profily, které byly vytvořeny před dostupností této základní verze:

- Jsou nyní jen pro čtení. Tyto profily můžete nadále používat, ale nemůžete je upravovat, abyste změnili jejich konfiguraci.
- Dá se aktualizovat na nejnovější verzi. Po aktualizaci aktuální základní verze můžete upravit profil a upravit nastavení.

Chcete-li zjistit, co se změnilo v této verzi směrného plánu z předchozích verzí, použijte akci [Porovnat směrné plány](../protect/security-baselines.md#compare-baseline-versions) , která je k dispozici při prohlížení podokna *verze* pro tento směrný plán. Nezapomeňte vybrat verzi směrného plánu, kterou chcete zobrazit.

Chcete-li aktualizovat profil standardních hodnot zabezpečení na nejnovější verzi tohoto směrného plánu, přečtěte si téma [Změna základní verze profilu](../protect/security-baselines.md#change-the-baseline-version-for-a-profile).


::: zone-end
::: zone pivot="edge-october-2019,edge-april-2020"

## <a name="microsoft-edge"></a>Microsoft Edge

::: zone-end
::: zone pivot="edge-april-2020"

- **Podporovaná schémata ověřování**  
  Určuje, která schémata ověřování HTTP jsou podporovaná. Zásady můžete nakonfigurovat pomocí těchto hodnot: *Basic*, *Digest*, *NTLM*a *Negotiate*. Více hodnot oddělte čárkami. Pokud tuto zásadu nenakonfigurujete, použijí se všechna čtyři schémata.

  - **Povolené** (*výchozí*) – používají se schémata, která jste vybrali.
  - **Zakázáno**
  - **Nenakonfigurováno** – používají se všechna čtyři schémata.
  
  Pokud je nastavené na *povoleno* , můžete nakonfigurovat následující nastavení, ve kterém můžete vybrat, které ověřování se má použít:

  - **Podporovaná schémata ověřování**  
    Vyberte z následujících možností:
    - **Basic**
    - **Otisk**
    - **Protokol NTLM** *(vybraný ve výchozím nastavení)*
    - **Negotiate** *(vybráno ve výchozím nastavení)*

- **Výchozí nastavení Adobe Flash**  
  CSP: [browser/AllowFlash](/windows/client-management/mdm/policy-csp-browser#browser-allowflash)a [browser/AllowFlashClickToRun](/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)

  Povolte přístup k následujícímu nastavení, kde můžete nakonfigurovat chování pro spuštění modulu plug-in Adobe Flash.  

  - **Povoleno** (*výchozí*)
  - **Zakázáno**
  - **Není nakonfigurováno**

  Pokud je nastavené na *povoleno* , můžete nakonfigurovat následující nastavení.

  - **Výchozí nastavení Adobe Flash**

    - **Blokovat modul plug-in Adobe Flash** (*výchozí*) – blokovat Adobe Flash na všech webech
    - **Kliknutím spustíte přehrávání** – Adobe Flash se spustí, ale uživatel musí vybrat možnost jeho spuštění.

- **Kontrola, která rozšíření se nedají nainstalovat**  
  Povolí použití seznamu, který určuje rozšíření, která uživatelé nemůžou instalovat na Microsoft Edge. Když se seznam používá, všechna nastavení v seznamu, která byla dříve nainstalována, jsou zakázána a uživatel je nemůže povolit. Odeberete-li položku ze seznamu blokovaných přípon, bude tato přípona automaticky znovu povolena kdekoli, kde byla dříve nainstalována.

  - **Povoleno** (*výchozí*) – povolí blokování rozšíření pomocí seznamu.
  - **Zakázáno**
  - **Nenakonfigurováno** – uživatelé můžou instalovat jakékoli rozšíření v Microsoft Edge.
  
  Pokud je nastavené na *povoleno*, můžete nakonfigurovat následující nastavení definující seznam rozšíření, která mají být zablokovaná.

  - **ID rozšíření: uživatel by měl mít zakázáno instalovat (nebo * pro všechny).**

    Vyberte **Přidat** a zadejte další rozšíření. **\*** je vybráno ve výchozím nastavení.

- **Povolí hostitelům nativního zasílání zpráv na úrovni uživatele (nainstalované bez oprávnění správce).**  
  Povoluje instalaci nativních hostitelů zasílání zpráv na úrovni uživatele.

  - **Povoleno**
  - **Zakázáno** (*výchozí*) – Microsoft Edge používá pouze nativní hostitele zasílání zpráv nainstalované na úrovni systému.
  - **Nenakonfigurováno** – Microsoft Edge umožňuje používat nativní hostitele zasílání zpráv na úrovni uživatele.

- **Povolit ukládání hesel do Správce hesel**  
  Microsoft Edge CSP: [browser/AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  Povolí Microsoft Edge ukládat hesla uživatelů.

  - **Povoleno** – uživatelé můžou ukládat hesla na Microsoft Edge. Při příštím návštěvě webu bude Microsoft Edge automaticky zadávat heslo. Uživatelé nemůžou tuto zásadu v Microsoft Edge změnit ani přepsat.
  - **Zakázáno** (*výchozí*) – uživatelé nemůžou ukládat nová hesla, ale můžou dál používat dřív uložená hesla. Uživatelé nemůžou tuto zásadu v Microsoft Edge změnit ani přepsat.
  - **Nenakonfigurováno** – uživatelé můžou ukládat hesla a tuto funkci vypnout.

- **Zabránit obcházení výzev filtru SmartScreen v programu Microsoft Defender pro weby**  
  CSP: [browser/PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  Rozhodněte, jestli uživatelé můžou potlačit upozornění filtru SmartScreen v programu Microsoft Defender o potenciálně škodlivých webech.

  - **Povoleno** (*výchozí*) – uživatelé nemůžou ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a jejich pokračování na webu bude zablokováno.
  - **Zakázáno** – uživatelé můžou ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a pokračovat v lokalitě.
  - **Není nakonfigurováno** Uživatelé můžou ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a pokračovat v lokalitě.

- **Zabránit obcházení upozornění filtru SmartScreen v programu Microsoft Defender o souborech ke stažení**  
  CSP: [browser/PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  Určete, jestli můžou uživatelé potlačit upozornění filtru SmartScreen v programu Microsoft Defender o neověřených souborech ke stažení.

  - **Povoleno** (*výchozí*) – uživatelé nemůžou ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a brání v dokončení neověřených stahování.
  - **Zakázáno** – uživatelé můžou ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a dokončit neověřené soubory ke stažení.
  - **Nenakonfigurováno** – uživatelé můžou ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a dokončit neověřené soubory ke stažení.

- **Povolit izolaci lokality pro každou lokalitu**  
  Nakonfigurujte izolaci lokality, aby se uživatelům zabránilo ve zrušení výchozího chování izolace všech lokalit.
  
  - **Povoleno** (*výchozí*) – uživatelé nemohou odhlásit výchozí chování, kde každá lokalita běží ve vlastním procesu.
  - **Zakázáno** – uživatelé můžou odhlásit izolaci webu. Izolace webu není vypnutá.
  - **Nenakonfigurováno** – uživatelé můžou odhlásit izolaci lokality. Izolace webu není vypnutá.

  Microsoft Edge podporuje taky zásady [IsolateOrigins](/deployedge/microsoft-edge-policies#isolateorigins) , které můžou izolovat další, jemnější navýšení zdroje.  Intune nepodporuje konfiguraci zásad IsolateOrigins.
  
- **Konfigurovat filtr SmartScreen v programu Microsoft Defender**  
  CSP: [browser/AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)  
  
  Filtr SmartScreen v programu Microsoft Defender poskytuje varovné zprávy, které usnadňují ochranu uživatelů před potenciálními podvodnými zprávami a škodlivým softwarem. Ve výchozím nastavení je filtr SmartScreen v programu Microsoft Defender zapnutý.
  
  - **Povoleno** (*výchozí*) – filtr SmartScreen v programu Microsoft Defender je zapnutý a uživatelé ho nemůžou vypnout.
  - **Zakázáno** – filtr SmartScreen v programu Microsoft Defender je vypnutý a uživatelé ho nemůžou zapnout.
  - **Není nakonfigurováno**  Uživatelé si můžou vybrat, jestli se má používat filtr SmartScreen v programu Microsoft Defender.

  Tato zásada je dostupná jenom v instancích systému Windows, které jsou připojené k doméně Microsoft Active ředitele, nebo k instancím Windows 10 pro nebo Enterprise zaregistrovaným pro správu zařízení.

- **Konfigurace filtru SmartScreen v programu Microsoft Defender pro blokování potenciálně nežádoucích aplikací**  
    Nakonfigurujte chování filtru SmartScreen v programu Microsoft Defender pro blokování potenciálně nežádoucích aplikací. Filtr SmartScreen v programu Microsoft Defender může poskytovat varovné zprávy, které vám pomůžou chránit uživatele před adwarem, mince dolování hlásí, bundleware a dalšími aplikacemi s nízkou pověstí, které jsou hostovány na webech. Blokování potenciálně nežádoucích aplikací ve filtru SmartScreen v programu Microsoft Defender je ve výchozím nastavení vypnuté.

  - **Povoleno** (*výchozí*) – potenciálně nežádoucí aplikace jsou blokované.
  - **Zakázané** – potenciálně nežádoucí aplikace nejsou blokované.
  - **Nenakonfigurováno** – uživatelé můžou zvolit, jestli se má v filtru SmartScreen v programu Microsoft Defender použít blokování potenciálně nežádoucích aplikací.

  Tato zásada je dostupná jenom v instancích systému Windows, které jsou připojené k doméně Microsoft Active ředitele, nebo k instancím Windows 10 pro nebo Enterprise zaregistrovaným pro správu zařízení.

- **Povolí uživatelům pokračovat ze stránky s upozorněním SSL.**  
   CSP: [browser/PreventCertErrorOverrides](/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  Microsoft Edge zobrazí stránku upozornění, když uživatelé navštíví weby s chybami SSL.
  - **Povoleno** – uživatelé můžou kliknout na stránky s upozorněními.
  - **Zakázáno** (*výchozí*) – uživatelům se zablokuje kliknutí na stránku s upozorněním.
  - **Nenakonfigurováno** – uživatelé můžou kliknout na tyto stránky s upozorněními.

- **Minimální povolená verze SSL**  
  Povolte možnost nastavit minimální podporovanou verzi SSL.

  - **Povoleno** (*výchozí*) – povolí přístup k dalšímu nastavení, kde ZAdáte minimální verzi TLS, která se má použít.
  - **Zakázáno**
  - **Nenakonfigurováno** – Microsoft Edge používá výchozí minimální verzi *TLS 1,0*.

  Pokud je nastavené na *povoleno*, můžete TLS nakonfigurovat pomocí následujícího nastavení.

  - **Minimální povolená verze SSL** Nastavte minimální verzi TLS, která se má použít. Microsoft Edge nebude používat žádnou verzi SSL/TLS, která je nižší než zadaná verze.
    - **TLS 1,0**
    - **TLS 1.1**
    - **TLS 1,2** (*výchozí*)

::: zone-end

::: zone pivot="edge-october-2019"

- **Zabránit obcházení výzev filtru SmartScreen v programu Microsoft Defender pro weby**  
  **Výchozí**: povoleno  
  Microsoft Edge CSP: [browser/PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  Nastavení této zásady umožňuje určit, jestli uživatelé můžou potlačit upozornění filtru SmartScreen v programu Microsoft Defender o potenciálně škodlivých webech. 
  - Pokud toto nastavení povolíte, uživatelé nebudou moct ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a jejich pokračování na webu bude zablokováno. 
  - Pokud toto nastavení zakážete nebo nenakonfigurujete, uživatelé můžou ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a pokračovat v lokalitě.

- **Minimální povolená verze SSL**  
  **Výchozí**: povoleno  

  Nastavte minimální podporovanou verzi SSL. Pokud nastavíte tuto zásadu na *nenakonfigurovanou*, Microsoft Edge použije výchozí minimální verzi *TLS 1,0*. Pokud je nastavené na *povoleno*, můžete vybrat minimální verzi z následujících hodnot:

  - TLS 1.0
  - TLS 1.1
  - TLS 1.2

  - **Minimální povolená verze SSL**  
    **Výchozí**: TLS 1,2

- **Zabránit obcházení upozornění filtru SmartScreen v programu Microsoft Defender o souborech ke stažení**  
  **Výchozí**: povoleno  
  Microsoft Edge CSP: [browser/PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  Tato zásada vám umožní určit, jestli můžou uživatelé potlačit upozornění filtru SmartScreen v programu Microsoft Defender o neověřených souborech ke stažení.
  - Pokud tuto zásadu povolíte, uživatelé ve vaší organizaci nemůžou ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a nebudou moct dokončit neověřené soubory ke stažení.
  - Pokud tuto zásadu zakážete nebo nenakonfigurujete, uživatelé můžou ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a dokončit neověřené soubory ke stažení.

- **Povolí uživatelům pokračovat ze stránky s upozorněním SSL.**  
  **Výchozí**: zakázáno  
  Microsoft Edge CSP: [browser/PreventCertErrorOverrides](/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  Microsoft Edge zobrazí stránku upozornění, když uživatelé navštíví weby s chybami SSL. Pokud nastavíte tuto zásadu na *povolenou* nebo *nenakonfigurovanou*, můžou uživatelé kliknout na tyto stránky s upozorněními. Pokud je tato zásada *zakázaná*, uživatelé budou mít možnost kliknout na jakoukoli stránku s upozorněním. 

- **Výchozí nastavení Adobe Flash**  
  **Výchozí**: povoleno  
  Microsoft Edge CSP: [browser/AllowFlash](/windows/client-management/mdm/policy-csp-browser#browser-allowflash)a [browser/AllowFlashClickToRun](/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)  

  Určuje, jestli weby, které nejsou pokryté ' PluginsAllowedForUrls ' nebo ' PluginsBlockedForUrls ', můžou automaticky spustit modul plug-in Adobe Flash. 

  - Vyberte ' BlockPlugins ' pro blokování Adobe Flash na všech webech
  - Vyberte ' ClickToPlay ', pokud chcete, aby aplikace Adobe Flash běžela, ale vyžadovala uživateli kliknutí na zástupný symbol pro jeho spuštění.
  
  V každém případě mají zásady "PluginsAllowedForUrls" a "PluginsBlockedForUrls" přednost před "DefaultPluginsSetting". Automatické přehrávání je povoleno pouze pro domény výslovně uvedené v zásadách ' PluginsAllowedForUrls '. 
   Pokud chcete povolit automatické přehrávání pro všechny weby, zvažte přidání http://* a https://* do tohoto seznamu.

  - Pokud nastavíte tuto zásadu na *není nakonfigurované*, může uživatel toto nastavení změnit ručně. * 2 = zablokovat modul plug-in Adobe Flash * 3 = kliknutím zahrajete předchozí sadu možností "1" povolení-vše, ale tato funkce je nyní zpracována pouze zásadami ' PluginsAllowedForUrls '. Existující zásady používající ' 1 ' budou fungovat v režimu kliknutí na přehrávání.  

  - **Výchozí nastavení Adobe Flash**  
    **Výchozí**: blokovat modul plug-in Adobe Flash

- **Povolit izolaci lokality pro každou lokalitu**  
  **Výchozí**: povoleno  

  Zásadu ' SitePerProcess ' lze použít k tomu, aby se uživatelé nemohli odcházet na výchozím chování izolace všech lokalit. Zásady IsolateOrigins můžete použít také k izolaci dalších, jemnějších zdrojů.

  - Pokud je tato zásada nastavená na *povoleno*, uživatelé se nebudou moci odhlásit z výchozího chování, kde každá lokalita běží ve vlastním procesu. 
  - Pokud použijete možnost *zakázáno* nebo *není nakonfigurováno*, uživatel může odhlásit izolaci webu. (Například pomocí položky "zakázat izolaci lokality" v edge://flags.) Když zásadu zakážete nebo nenakonfigurujete, nevypne se izolace lokality.

- **Podporovaná schémata ověřování**  
  **Výchozí**: povoleno  

  Určuje, která schémata ověřování HTTP jsou podporovaná. Zásady můžete nakonfigurovat pomocí těchto hodnot: "Basic", "Digest", "NTLM" a "Negotiate". Více hodnot oddělte čárkami. Pokud tuto zásadu nenakonfigurujete, použijí se všechna čtyři schémata.

  - **Podporovaná schémata ověřování**  
    Vyberte z následujících možností:
    - Základní
    - Otisk
    - Protokol NTLM *(vybraný ve výchozím nastavení)*
    - Negotiate *(vybráno ve výchozím nastavení)*

- **Povolit ukládání hesel do Správce hesel**  
  **Výchozí**: zakázáno  
  Microsoft Edge CSP: [browser/AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  Povolí Microsoft Edge ukládat hesla uživatelů.
  - Pokud tuto zásadu povolíte, můžou si uživatelé ukládat svoje hesla na Microsoft Edge. Při příštím návštěvě webu bude Microsoft Edge automaticky zadávat heslo.
  - Pokud tuto zásadu zakážete, uživatelé nebudou moct ukládat nová hesla, ale můžou dál používat dřív uložená hesla.
  
  Když nastavíte tuto zásadu na *povolenou* nebo *zakázanou*, uživatelé nemůžou tuto zásadu v Microsoft Edge změnit ani přepsat.
  
  Pokud tuto možnost nastavíte na *není nakonfigurované*, můžou uživatelé ukládat hesla a tuto funkci vypnout.

- **Kontrola, která rozšíření se nedají nainstalovat**  
  **Výchozí**: povoleno  

  Vypíše konkrétní rozšíření, která uživatelé nemůžou instalovat na Microsoft Edge. Když nasadíte tuto zásadu, všechna rozšíření v tomto seznamu, která byla dříve nainstalována, budou zakázána a uživatel je nebude moci povolit. Odeberete-li položku ze seznamu blokovaných přípon, bude tato přípona automaticky znovu povolena kdekoli, kde byla dříve nainstalována.
  
  Slouží **\*** k blokování všech rozšíření, která nejsou explicitně uvedena v seznamu povolených. Pokud je tato zásada nastavená na *nenakonfigurovaná*, uživatelé můžou nainstalovat jakékoli rozšíření v Microsoft Edge.
  
  Příklad hodnoty: extension_id1 extension_id2.  
  <br>
  - **ID rozšíření: uživatel by měl mít zakázáno instalovat (nebo * pro všechny).**  
    Vyberte **Přidat** a zadejte další rozšíření. **\*** je vybráno ve výchozím nastavení.

- **Konfigurovat filtr SmartScreen v programu Microsoft Defender**  
  **Výchozí**: povoleno  
  Microsoft Edge CSP: [browser/AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

  Nastavením této zásady lze nakonfigurovat, zda má být filtr SmartScreen v programu Microsoft Defender zapnut. Filtr SmartScreen v programu Microsoft Defender poskytuje varovné zprávy, které vám pomůžou ochránit uživatele před potenciálními podvodnými zprávami a škodlivým softwarem.
  
  - Ve výchozím nastavení je filtr SmartScreen v programu Microsoft Defender zapnutý. Pokud povolíte toto nastavení, filtr SmartScreen v programu Microsoft Defender je zapnutý a uživatelé ho nemůžou vypnout.
  - Pokud toto nastavení zakážete, filtr SmartScreen v programu Microsoft Defender je vypnutý a uživatelé ho nemůžou zapnout.
  - Pokud nastavíte možnost *není nakonfigurované*, uživatelé si můžou vybrat, jestli se má používat filtr SmartScreen v programu Microsoft Defender.
  
  Tato zásada je dostupná jenom v instancích systému Windows, které jsou připojené k doméně Microsoft Active ředitele, nebo k instancím Windows 10 pro nebo Enterprise zaregistrovaným pro správu zařízení.

- **Povolí hostitelům nativního zasílání zpráv na úrovni uživatele (nainstalované bez oprávnění správce).**  
  **Výchozí**: zakázáno

  Povoluje instalaci nativních hostitelů zasílání zpráv na úrovni uživatele. 
  - Pokud tuto zásadu zakážete, Microsoft Edge bude používat jenom nativní hostitele zasílání zpráv nainstalované na úrovni systému. Ve výchozím nastavení, pokud tyto zásady nenakonfigurujete, Microsoft Edge povolí použití nativních hostitelů zasílání zpráv na úrovni uživatele.

::: zone-end

## <a name="next-steps"></a>Další kroky

- [Další informace o standardních hodnotách zabezpečení](security-baselines.md)
- [Vyhnout se konfliktům](security-baselines.md#avoid-conflicts)
- [Řešení potíží se zásadami a profily v Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)