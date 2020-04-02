---
title: Nastavení standardních hodnot zabezpečení Intune pro Microsoft Edge
titleSuffix: Microsoft Intune
description: Nastavení standardních hodnot zabezpečení, které Intune podporuje pro správu prohlížeče Microsoft Edge
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/30/2019
ms.topic: reference
ms.service: microsoft-intune
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6108fc56b978c57bfc70b2bce9911f7901a01a3e
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/02/2020
ms.locfileid: "80551736"
---
# <a name="microsoft-edge-baseline-settings-for-intune"></a>Základní nastavení Microsoft Edge pro Intune

Zobrazení standardních nastavení webového prohlížeče Microsoft Edge, která jsou podporována nástrojem Microsoft Intune. Výchozí nastavení Microsoft Edge představuje doporučenou konfiguraci pro prohlížeče Microsoft Edge a nemusí odpovídat výchozím hodnotám pro jiné standardní hodnoty zabezpečení.

> [!NOTE]
> Základní hodnoty Microsoft Edge jsou v Public Preview. 

## <a name="microsoft-edge"></a>Microsoft Edge

- **Zabránit obcházení výzev filtru SmartScreen v programu Microsoft Defender pro weby**  
  **Výchozí**: povoleno  
  Microsoft Edge CSP: [browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  Nastavení této zásady umožňuje určit, jestli uživatelé můžou potlačit upozornění filtru SmartScreen v programu Microsoft Defender o potenciálně škodlivých webech. 
  - Pokud toto nastavení povolíte, uživatelé nebudou moct ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a jejich pokračování na webu bude zablokováno. 
  - Pokud toto nastavení zakážete nebo nenakonfigurujete, uživatelé můžou ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a pokračovat v lokalitě.

- **Minimální povolená verze SSL**  
  **Výchozí**: povoleno  

  Nastavte minimální podporovanou verzi SSL. Pokud nastavíte tuto zásadu na *nenakonfigurovanou*, Microsoft Edge použije výchozí minimální verzi *TLS 1,0*. Pokud je nastavené na *povoleno*, můžete vybrat minimální verzi z následujících hodnot:

  - TLS 1,0
  - TLS 1,1
  - TLS 1.2

  - **Minimální povolená verze SSL**  
    **Výchozí**: TLS 1,2

- **Zabránit obcházení upozornění filtru SmartScreen v programu Microsoft Defender o souborech ke stažení**  
  **Výchozí**: povoleno  
  Microsoft Edge CSP: [browser/PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  Tato zásada vám umožní určit, jestli můžou uživatelé potlačit upozornění filtru SmartScreen v programu Microsoft Defender o neověřených souborech ke stažení.
  - Pokud tuto zásadu povolíte, uživatelé ve vaší organizaci nemůžou ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a nebudou moct dokončit neověřené soubory ke stažení.
  - Pokud tuto zásadu zakážete nebo nenakonfigurujete, uživatelé můžou ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a dokončit neověřené soubory ke stažení.

- **Povolí uživatelům pokračovat ze stránky s upozorněním SSL.**  
  **Výchozí**: zakázáno  
  Microsoft Edge CSP: [browser/PreventCertErrorOverrides](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  Microsoft Edge zobrazí stránku upozornění, když uživatelé navštíví weby s chybami SSL. Pokud nastavíte tuto zásadu na *povolenou* nebo *nenakonfigurovanou*, můžou uživatelé kliknout na tyto stránky s upozorněními. Pokud je tato zásada *zakázaná*, uživatelé budou mít možnost kliknout na jakoukoli stránku s upozorněním. 

- **Výchozí nastavení Adobe Flash**  
  **Výchozí**: povoleno  
  Microsoft Edge CSP: [browser/AllowFlash](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflash)a [browser/AllowFlashClickToRun](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)  

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
    - Basic
    - Otisk
    - Protokol NTLM *(vybraný ve výchozím nastavení)*
    - Negotiate *(vybráno ve výchozím nastavení)*

- **Povolit ukládání hesel do Správce hesel**  
  **Výchozí**: zakázáno  
  Microsoft Edge CSP: [browser/AllowPasswordManager](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  Povolí Microsoft Edge ukládat hesla uživatelů. 
  - Pokud tuto zásadu povolíte, můžou si uživatelé ukládat svoje hesla na Microsoft Edge. Při příštím návštěvě webu bude Microsoft Edge automaticky zadávat heslo. 
  - Pokud tuto zásadu zakážete, uživatelé nebudou moct ukládat nová hesla, ale můžou dál používat dřív uložená hesla. 
  
  Když nastavíte tuto zásadu na *povolenou* nebo *zakázanou*, uživatelé nemůžou tuto zásadu v Microsoft Edge změnit ani přepsat. 
  
  Pokud tuto možnost nastavíte na *není nakonfigurované*, můžou uživatelé ukládat hesla a tuto funkci vypnout.

- **Kontrola, která rozšíření se nedají nainstalovat**  
  **Výchozí**: povoleno  

  Vypíše konkrétní rozšíření, která uživatelé nemůžou instalovat na Microsoft Edge. Když nasadíte tuto zásadu, všechna rozšíření v tomto seznamu, která byla dříve nainstalována, budou zakázána a uživatel je nebude moci povolit. Odeberete-li položku ze seznamu blokovaných přípon, bude tato přípona automaticky znovu povolena kdekoli, kde byla dříve nainstalována.
  
  Použijte **\*** k blokování všech rozšíření, která nejsou explicitně uvedena v seznamu povolených. Pokud je tato zásada nastavená na *nenakonfigurovaná*, uživatelé můžou nainstalovat jakékoli rozšíření v Microsoft Edge. 
  
  Příklad hodnoty: extension_id1 extension_id2.  
  <br>
  - **ID rozšíření: uživatel by měl mít zakázáno instalovat (nebo * pro všechny).**  
    Vyberte **Přidat** a zadejte další rozšíření. ve výchozím nastavení je vybraná možnost **\*** .

- **Konfigurovat filtr SmartScreen v programu Microsoft Defender**  
  **Výchozí**: povoleno  
  Microsoft Edge CSP: [browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)  
  
  Nastavením této zásady lze nakonfigurovat, zda má být filtr SmartScreen v programu Microsoft Defender zapnut. Filtr SmartScreen v programu Microsoft Defender poskytuje varovné zprávy, které vám pomůžou ochránit uživatele před potenciálními podvodnými zprávami a škodlivým softwarem. 
  
  - Ve výchozím nastavení je filtr SmartScreen v programu Microsoft Defender zapnutý. Pokud povolíte toto nastavení, filtr SmartScreen v programu Microsoft Defender je zapnutý a uživatelé ho nemůžou vypnout.
  - Pokud toto nastavení zakážete, filtr SmartScreen v programu Microsoft Defender je vypnutý a uživatelé ho nemůžou zapnout. 
  - Pokud nastavíte možnost *není nakonfigurované*, uživatelé si můžou vybrat, jestli se má používat filtr SmartScreen v programu Microsoft Defender. 
  
  Tato zásada je dostupná jenom v instancích systému Windows, které jsou připojené k doméně Microsoft Active ředitele, nebo k instancím Windows 10 pro nebo Enterprise zaregistrovaným pro správu zařízení.

- **Povolí hostitelům nativního zasílání zpráv na úrovni uživatele (nainstalované bez oprávnění správce).**  
  **Výchozí**: zakázáno  

  Povoluje instalaci nativních hostitelů zasílání zpráv na úrovni uživatele. 
  - Pokud tuto zásadu zakážete, Microsoft Edge bude používat jenom nativní hostitele zasílání zpráv nainstalované na úrovni systému. Ve výchozím nastavení, pokud tyto zásady nenakonfigurujete, Microsoft Edge povolí použití nativních hostitelů zasílání zpráv na úrovni uživatele.

## <a name="next-steps"></a>Další kroky

- [Další informace o standardních hodnotách zabezpečení](security-baselines.md)
- [Vyhnout se konfliktům](security-baselines.md#avoid-conflicts)
- [Řešení potíží se zásadami a profily v Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
