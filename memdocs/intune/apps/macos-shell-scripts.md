---
title: Použití skriptů prostředí v zařízeních macOS v Microsoft Intune | Microsoft Docs
description: Vytváření, přiřazování, sledování a odstraňování potíží s skripty prostředí pro zařízení macOS v Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/30/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c5839154ab0c884e933e8d11055e745d54503433
ms.sourcegitcommit: 8a8378b685a674083bfb9fbc9c0662fb0c7dda97
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/01/2020
ms.locfileid: "82619538"
---
# <a name="use-shell-scripts-on-macos-devices-in-intune-public-preview"></a>Použití skriptů prostředí v zařízeních macOS v Intune (Public Preview)

> [!NOTE]
> Skripty prostředí pro zařízení macOS jsou momentálně ve verzi Preview. Před použitím této funkce si přečtěte seznam [známých problémů ve verzi Preview](macos-shell-scripts.md#known-issues) .

Používejte skripty prostředí pro rozšiřování možností správy zařízení v Intune nad rámec toho, co podporuje operační systém macOS. 

## <a name="prerequisites"></a>Požadavky
Při sestavování skriptů prostředí a jejich přiřazení k zařízením macOS se ujistěte, že jsou splněné následující předpoklady. 
 - Na zařízeních běží macOS 10,12 nebo novější.
 - Zařízení se spravují přes Intune. 
 - Skripty prostředí začínají na `#!` a musí být v platném umístění, například `#!/bin/sh` nebo `#!/usr/bin/env zsh`.
 - Jsou nainstalované překladače příkazového řádku pro příslušné prostředí.

## <a name="important-considerations-before-using-shell-scripts"></a>Důležité informace před použitím skriptů prostředí
 - Skripty prostředí vyžadují, aby byl na zařízení macOS úspěšně nainstalovaný Agent pro správu Microsoft Intune. Další informace najdete v tématu [Agent pro správu Microsoft Intune pro MacOS](macos-shell-scripts.md#microsoft-intune-management-agent-for-macos).
 - Skripty prostředí běží paralelně na zařízeních jako samostatné procesy.
 - Skripty prostředí, které jsou spuštěné jako přihlášený uživatel, se spustí pro všechny aktuálně přihlášené uživatelské účty na zařízení v době spuštění.
 - Koncový uživatel se musí přihlásit k zařízení a spustit skripty spuštěné jako přihlášený uživatel.
 - Oprávnění root user se vyžadují, pokud skript vyžaduje provedení změn, které standardní uživatelský účet nemůže.
 - Skripty prostředí se pokusí spustit častěji než zvolená frekvence skriptu pro určité podmínky, například pokud je disk plný, pokud je umístění úložiště úmyslně poškozeno, pokud je místní mezipaměť smazána nebo pokud se zařízení Mac restartuje.
 
## <a name="create-and-assign-a-shell-script-policy"></a>Vytvoření a přiřazení zásad skriptu prostředí
1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **MacOS** > **Scripts**skripty > **Přidat**.
3. V části **základy**zadejte následující vlastnosti a vyberte **Další**:
   - **Název**: zadejte název skriptu prostředí.
   - **Popis**: zadejte popis skriptu prostředí. Toto nastavení není povinné, ale doporučujeme ho zadat.
4. V **nastavení skriptu**zadejte následující vlastnosti a vyberte **Další**:
   - **Nahrát skript**: přejděte do skriptu prostředí. Velikost souboru skriptu musí být menší než 200 KB.
   - **Spustit skript jako přihlášený uživatel**: vyberte **Ano** a spusťte skript s přihlašovacími údaji uživatele v zařízení. Pokud chcete spustit skript jako kořenový uživatel, vyberte **ne** (výchozí). 
   - **Skrýt oznámení skriptu na zařízeních:** Ve výchozím nastavení se pro každý spuštěný skript zobrazují oznámení skriptu. Koncoví uživatelé uvidí *konfiguraci* oznámení o počítači z Intune na zařízeních MacOS.
   - **Frekvence skriptu:** Vyberte, jak často se má skript spouštět. Pokud chcete spustit skript jenom jednou, vyberte **nenakonfigurované** (výchozí).
   - **Maximální počet pokusů o opakování, pokud se skript nezdařil:** Vyberte, kolikrát se má skript spustit, pokud vrátí nenulový ukončovací kód (nula znamená úspěch). Pokud dojde k chybě skriptu, vyberte možnost **Nenakonfigurováno** (výchozí).
5. V části **značky oboru**Volitelně přidejte značky oboru pro skript a vyberte **Další**. Pomocí značek Scope můžete určit, kdo může v Intune zobrazovat skripty. Úplné podrobnosti o značkách oboru najdete v tématu [použití značek řízení přístupu na základě role a rozsahu pro distribuci IT](../fundamentals/scope-tags.md).
6. Vyberte **přiřazení** > **Vybrat skupiny, které chcete zahrnout**. Zobrazí se existující seznam skupin Azure AD. Vyberte jednu nebo více skupin zařízení, které zahrnují uživatele, jejichž zařízení macOS mají přijmout skript. Zvolte **Vybrat**. Skupiny, které vyberete, se zobrazí v seznamu a budou dostávat vaše zásady pro skripty.
   > [!NOTE]
   > - Skripty prostředí v Intune je možné přiřadit jenom skupinám zabezpečení zařízení Azure AD. Přiřazení skupiny uživatelů se ve verzi Preview nepodporuje. 
   > - Aktualizace přiřazení pro skripty prostředí také aktualizuje přiřazení pro [agenta Microsoft Intune pro správu pro MacOS](macos-shell-scripts.md#microsoft-intune-management-agent-for-macos).
7. V okně **Revize a přidat**se zobrazí souhrn nastavení, které jste nakonfigurovali. Vyberte **Přidat** a uložte skript. Když vyberete **Přidat**, zásada skriptu se nasadí do skupin, které jste zvolili.

Skript, který jste vytvořili, se teď zobrazí v seznamu skriptů. 

## <a name="monitor-a-shell-script-policy"></a>Monitorování zásad skriptů prostředí
Kliknutím na jednu z následujících sestav můžete monitorovat stav spuštění všech přiřazených skriptů pro uživatele a zařízení:
- **Skripty** > **vyberou skript ke sledování** > **stavu zařízení** .
- **Skripty** > **vyberou skript pro sledování** > **stavu uživatele** .

>[!IMPORTANT]
> Bez ohledu na zvolenou **frekvenci skriptu**se stav spuštění skriptu oznamuje jenom při prvním spuštění skriptu. Stav spuštění skriptu není aktualizován při dalších spuštěních. Aktualizované skripty se však považují za nové skripty a stav spuštění bude hlášen znovu.

Po spuštění skriptu vrátí jeden z následujících stavů:
- Stav spuštění skriptu **se nezdařilo** , indikuje, že skript vrátil nenulový ukončovací kód, nebo je skript poškozený. 
- Stav spuštění skriptu **úspěch** indikuje, že skript vrátil nulu jako ukončovací kód. 

## <a name="troubleshoot-macos-shell-script-policies-using-log-collection"></a>Řešení potíží se zásadami skriptů prostředí macOS pomocí shromažďování protokolů

Můžete shromažďovat protokoly zařízení, které vám pomůžou řešit problémy se skripty na zařízeních macOS. 

### <a name="requirements-for-log-collection"></a>Požadavky na shromažďování protokolů
Pro shromáždění protokolů na zařízení macOS jsou vyžadovány následující položky:
- Je nutné zadat úplnou cestu absolutního souboru protokolu.
- Cesty k souborům musí být odděleny pouze pomocí středníku (;).
- Maximální velikost kolekce protokolů k nahrání je 60 MB (komprimovaný) nebo 25 souborů, podle toho, co nastane dřív.
- Mezi typy souborů, které jsou povolené pro shromažďování protokolů, patří následující přípony: *. log,. zip,. gz,. tar,. txt,. XML,. Crash,. RTF.*

#### <a name="collect-device-logs"></a>Shromažďování protokolů zařízení
1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. V sestavě **stav zařízení** nebo **stav uživatele** vyberte zařízení.
3. Vyberte **shromažďovat protokoly**, zadejte cesty ke složkám souborů protokolu oddělené středníkem (;) bez mezer nebo newlines mezi cestami.<br>Například je třeba zapsat více cest jako `/Path/to/logfile1.zip;/Path/to/logfile2.log`. 

   >[!IMPORTANT]
   > Několik cest k souboru protokolu oddělených pomocí čárky, tečky, nového řádku nebo uvozovek s mezerami nebo bez nich bude mít za následek chybu shromažďování protokolů. Mezery se také nepovolují jako oddělovače mezi cestami.

4. Vyberte **OK**. Protokoly se shromažďují při příštím ověření agenta pro správu Intune v zařízení s Intune. K tomuto vrácení se změnami obvykle dochází každých 8 hodin.

   >[!NOTE]
   > 
   > - Shromážděné protokoly se v zařízení šifrují, přenáší a ukládají se do Microsoft Azure úložiště po dobu 30 dnů. Uložené protokoly se dešifrují na vyžádání a stáhnou se pomocí centra pro správu služby Microsoft Endpoint Manager.
   > - Kromě protokolů určených pro správu jsou protokoly agenta pro správu Intune také shromažďovány z těchto složek: `/Library/Logs/Microsoft/Intune` a. `~/Library/Logs/Microsoft/Intune` Názvy souborů protokolu agenta jsou `IntuneMDMDaemon date--time.log` a. `IntuneMDMAgent date--time.log` 
   > - Pokud nějaký soubor zadaný správcem chybí nebo má nesprávnou příponu souboru, najdete tyto názvy souborů uvedené v `LogCollectionInfo.txt`části.     

### <a name="log-collection-errors"></a>Chyby shromažďování protokolů
Shromažďování protokolů nemusí být úspěšné z některého z následujících důvodů uvedených v následující tabulce. Chcete-li tyto chyby vyřešit, postupujte podle kroků pro odstranění problému.

| Kód chyby (Hex) | Kód chyby (prosinec) | Chybová zpráva | Postup odstranění problému |
|------------------|------------------|---------------|-------------------|
| 0X87D300D1 | 2016214834 | Velikost souboru protokolu nemůže být větší než 60 MB. | Zajistěte, aby byly komprimované protokoly menší než 60 MB. |
| 0X87D300D1 | 2016214831 | Zadaná cesta k souboru protokolu musí existovat. Systémová složka uživatele je neplatného umístění pro soubory protokolu. | Ujistěte se, že zadaná cesta k souboru je platná a přístupná. |
| 0X87D300D2 | 2016214830 | Nahrání souboru shromažďování protokolů se nezdařilo z důvodu vypršení platnosti adresy URL pro odeslání. | Opakujte akci **shromáždit protokoly** . |
| 0X87D300D3, 0X87D300D5, 0X87D300D7 | 2016214829, 2016214827, 2016214825 | Nahrání souboru shromažďování protokolů nebylo úspěšné kvůli chybě šifrování. Zkuste odeslat protokol znovu. | Opakujte akci **shromáždit protokoly** . |
| | 2016214828 | Počet souborů protokolu překročil povolený limit 25 souborů. | Najednou se dá shromáždit jenom 25 souborů protokolu. |
| 0X87D300D6 | 2016214826 | Nahrání souboru shromažďování dat se nepovedlo kvůli chybě zip. Zkuste odeslat protokol znovu. | Opakujte akci **shromáždit protokoly** . |
| | 2016214740 | Protokoly nemohly být šifrované, protože nebyly nalezeny komprimované protokoly. | Opakujte akci **shromáždit protokoly** . |
| | 2016214739 | Protokoly byly shromážděny, ale nebyly uloženy. | Opakujte akci **shromáždit protokoly** . |

## <a name="frequently-asked-questions"></a>Nejčastější dotazy
### <a name="why-are-assigned-shell-scripts-not-running-on-the-device"></a>Proč jsou přiřazené skripty prostředí v zařízení nespuštěny?
Může existovat několik důvodů:
* Agent může být muset vrátit se změnami, aby přijímal nové nebo aktualizované skripty. Tento proces vrácení se změnami probíhá každých 8 hodin a liší se od vrácení se změnami MDM. Ujistěte se, že je zařízení spuštěno a připojené k síti pro úspěšné přihlášení agenta a počkejte na vrácení se změnami agenta.
* Agent nemusí být nainstalován. Ověřte, že je agent nainstalovaný `/Library/Intune/Microsoft Intune Agent.app` na zařízení MacOS.
* Agent nemůže být v dobrém stavu. Agent se pokusí o zotavení po dobu 24 hodin, odebrat sám sebe a znovu nainstalovat, pokud jsou skripty prostředí stále přiřazeny.

### <a name="how-frequently-is-script-run-status-reported"></a>Jak často je stav spuštění skriptu hlášeno?
Stav spuštění skriptu se oznamuje konzole pro správu Microsoft Endpoint Manageru hned po dokončení spuštění skriptu. Pokud je naplánováno pravidelné spouštění skriptu v nastavené četnosti, ohlásí stav pouze při prvním spuštění.

### <a name="when-are-shell-scripts-run-again"></a>Kdy se skripty prostředí spouštějí znovu?
Skript se spustí znovu pouze v případě, že je **maximální počet pokusů o opakování skriptu, pokud** je nakonfigurováno nastavení chyby skriptu a při spuštění skriptu dojde k chybě. Pokud je **maximální počet pokusů o opakování skriptu, pokud** není nakonfigurován skript a dojde k selhání skriptu při spuštění, nebude znovu spuštěn a stav spuštění bude hlášen jako **neúspěšný**. 

### <a name="what-intune-role-permissions-are-required-for-shell-scripts"></a>Jaká oprávnění role Intune jsou vyžadována pro skripty prostředí?
Vaše přiřazená role Intune vyžaduje **Konfigurace zařízení** oprávnění k odstraňování, přiřazování, vytváření, aktualizaci nebo čtení skriptů prostředí.

## <a name="microsoft-intune-management-agent-for-macos"></a>Agent pro správu Microsoft Intune pro macOS
 ### <a name="why-is-the-agent-required"></a>Proč je agent vyžadován?
Aby bylo možné Upřesnit možnosti správy zařízení, které nejsou podporovány nativním operačním systémem macOS, je nutné nainstalovat Microsoft Intune agenta pro správu.
 
 ### <a name="how-is-the-agent-installed"></a>Jak je nainstalován agent?
 Na zařízeních macOS spravovaných pomocí Intune se automaticky a tiše nainstaluje agent, kterému přiřadíte aspoň jeden skript prostředí v centru pro správu Microsoft Endpoint Manageru. `/Library/Intune/Microsoft Intune Agent.app` Agent se instaluje v případě potřeby a v aplikacích **vyhledávací** > **aplikace** na zařízeních MacOS se nezobrazuje. Agent se při spuštění `IntuneMdmAgent` na zařízeních MacOS zobrazí jako v **monitorování aktivity** .

### <a name="what-does-the-agent-do"></a>Co agent dělá?
 - Před vrácením se změnami pro příjem skriptů prostředí pro zařízení macOS se agent tiše ověřuje pomocí služeb Intune.
 - Agent obdrží přiřazené skripty prostředí a spustí skripty na základě nakonfigurovaného plánu, pokusů o opakování, nastavení oznámení a dalších nastavení nastavených správcem.
 - Agent kontroluje nové nebo aktualizované skripty se službami Intune obvykle každých 8 hodin. Tato operace vrácení se změnami je nezávislá na vrácení se změnami MDM. 
 
 ### <a name="how-can-i-manually-initiate-an-agent-check-in-from-a-mac"></a>Jak mohu ručně iniciovat agenty vrácení se změnami z počítače Mac?
Na spravovaném počítači Mac s nainstalovaným agentem otevřete **terminál**, spusťte `sudo killall IntuneMdmAgent` příkaz, aby se `IntuneMdmAgent` proces ukončil. `IntuneMdmAgent` Proces se okamžitě restartuje, čímž se zahájí vrácení se změnami do Intune.

Případně můžete provést následující akce:
1. Otevřete > **zobrazení** **monitorování** > aktivit*vybrat **všechny procesy**.* 
2. Vyhledejte procesy s názvem `IntuneMdmAgent`. 
3. Ukončete proces spuštěný pro uživatele **root** . 

> [!NOTE]
> Akce **kontroly nastavení** v portál společnosti a akce **synchronizace** pro zařízení v konzole pro správu služby Microsoft Endpoint Manager iniciují kontrolu MDM a nevynutí vrácení se změnami agenta.

 ### <a name="when-is-the-agent-removed"></a>Kdy je agent odebrán?
 Existuje několik podmínek, které mohou způsobit odebrání agenta ze zařízení, například:
 - Skripty prostředí již nejsou přiřazeny k zařízení. 
 - Zařízení macOS již není spravováno.
 - Agent je ve stavu nezotavitelné po dobu delší než 24 hodin (doba provozu zařízení).

 ### <a name="how-to-turn-off-usage-data-sent-to-microsoft-for-shell-scripts"></a>Jak vypnout data o využití, která se odesílají do Microsoftu pro skripty prostředí?
 Pokud chcete vypnout data o využití posílaná Microsoftu z agenta pro správu Intune, otevřete portál společnosti a vyberte**Předvolby** >  **nabídky** > zrušit*zaškrtnutí políčka Povolit Microsoftu shromažďovat data o využití*. Tato akce vypne data o využití, která jsou posílána jak pro agenta, tak pro Portál společnosti.

## <a name="known-issues"></a>Známé problémy
- **Přiřazení skupiny uživatelů:** Skripty prostředí přiřazené skupinám uživatelů se nevztahují na zařízení. Přiřazení skupiny uživatelů se v tuto chvíli ve verzi Preview nepodporuje. K přiřazení skriptů použijte přiřazení skupiny zařízení.
- **Shromažďovat protokoly:** Akce shromáždit protokoly je viditelná. Ale při pokusu o shromažďování protokolů se zobrazí zpráva "došlo k chybě" a nezachytí protokoly. Shromažďování protokolů není v současné době ve verzi Preview podporováno.
- **Žádný stav spuštění skriptu:** V nepravděpodobném případě, že se na zařízení přijme skript a zařízení přejde do režimu offline, než se nahlásí stav spuštění, zařízení neohlásí stav spuštění skriptu v konzole pro správu.
- **Zpráva o stavu uživatele:** Existuje prázdný problém sestavy. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **monitor**. Stav uživatele zobrazuje prázdnou sestavu.

## <a name="next-steps"></a>Další kroky

- [Vytvoření zásady dodržování předpisů v Microsoft Intune](..\protect\create-compliance-policy.md)
