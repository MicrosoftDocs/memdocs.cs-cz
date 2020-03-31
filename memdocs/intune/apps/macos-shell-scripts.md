---
title: Použití skriptů prostředí v zařízeních macOS v Microsoft Intune | Microsoft Docs
description: Vytváření, přiřazování, sledování a odstraňování potíží s skripty prostředí pro zařízení macOS v Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/26/2020
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
ms.openlocfilehash: 36936976528b5ea9c3fff1f77ec11223a4e4e63d
ms.sourcegitcommit: e7fb8cf2ffce29548b4a33b2a0c33a3a227c6bc4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/30/2020
ms.locfileid: "80401770"
---
# <a name="use-shell-scripts-on-macos-devices-in-intune-public-preview"></a>Použití skriptů prostředí v zařízeních macOS v Intune (Public Preview)

> [!NOTE]
> Skripty prostředí pro zařízení macOS jsou momentálně ve verzi Preview. Před použitím této funkce si přečtěte seznam [známých problémů ve verzi Preview](macos-shell-scripts.md#known-issues) .

Používejte skripty prostředí pro rozšiřování možností správy zařízení v Intune nad rámec toho, co podporuje operační systém macOS. 

## <a name="prerequisites"></a>Předpoklady
Při sestavování skriptů prostředí a jejich přiřazení k zařízením macOS se ujistěte, že jsou splněné následující předpoklady. 
 - Na zařízeních běží macOS 10,12 nebo novější.
 - Zařízení se spravují přes Intune. 
 - Skripty prostředí začínají na `#!` a musí být v platném umístění, například `#!/bin/sh` nebo `#!/usr/bin/env zsh`.
 - Jsou nainstalované překladače příkazového řádku pro příslušné prostředí.

## <a name="important-considerations-before-using-shell-scripts"></a>Důležité informace před použitím skriptů prostředí
 - Skripty prostředí vyžadují, aby se na zařízení macOS úspěšně nainstaloval agent MDM Microsoft Intune. Další informace najdete v tématu [Microsoft Intune agenta MDM pro MacOS](macos-shell-scripts.md#microsoft-intune-mdm-agent-for-macos).
 - Skripty prostředí běží paralelně na zařízeních jako samostatné procesy.
 - Skripty prostředí, které jsou spuštěné jako přihlášený uživatel, se spustí pro všechny aktuálně přihlášené uživatelské účty na zařízení v době spuštění.
 - Koncový uživatel se musí přihlásit k zařízení a spustit skripty spuštěné jako přihlášený uživatel.
 - Oprávnění root user se vyžadují, pokud skript vyžaduje provedení změn, které standardní uživatelský účet nemůže.
 - Skripty prostředí se pokusí spustit častěji než zvolená frekvence skriptu pro určité podmínky, například pokud je disk plný, pokud je umístění úložiště úmyslně poškozeno, pokud je místní mezipaměť smazána nebo pokud se zařízení Mac restartuje.
 
## <a name="create-and-assign-a-shell-script-policy"></a>Vytvoření a přiřazení zásad skriptu prostředí
1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **macOS** > **skripty** > **Přidat**.
3. V části **základy**zadejte následující vlastnosti a vyberte **Další**:
   - **Název**: zadejte název skriptu prostředí.
   - **Popis**: zadejte popis skriptu prostředí. Toto nastavení není povinné, ale doporučujeme ho zadat.
4. V **nastavení skriptu**zadejte následující vlastnosti a vyberte **Další**:
   - **Nahrát skript**: přejděte do skriptu prostředí. Velikost souboru skriptu musí být menší než 200 KB.
   - **Spustit skript jako přihlášený uživatel**: vyberte **Ano** a spusťte skript s přihlašovacími údaji uživatele v zařízení. Pokud chcete spustit skript jako kořenový uživatel, vyberte **ne** (výchozí). 
5. V části **značky oboru**Volitelně přidejte značky oboru pro skript a vyberte **Další**. Pomocí značek Scope můžete určit, kdo může v Intune zobrazovat skripty. Úplné podrobnosti o značkách oboru najdete v tématu [použití značek řízení přístupu na základě role a rozsahu pro distribuci IT](../fundamentals/scope-tags.md).
6. Vyberte **přiřazení** > **Vybrat skupiny, které chcete zahrnout**. Zobrazí se existující seznam skupin Azure AD. Vyberte jednu nebo více skupin zařízení, které zahrnují uživatele, jejichž zařízení macOS mají přijmout skript. Zvolte **Vybrat**. Skupiny, které vyberete, se zobrazí v seznamu a budou dostávat vaše zásady pro skripty.
   > [!NOTE]
   > - Skripty prostředí v Intune je možné přiřadit jenom skupinám zabezpečení zařízení Azure AD. Přiřazení skupiny uživatelů se ve verzi Preview nepodporuje. 
   > - Aktualizace přiřazení pro skripty prostředí také aktualizuje přiřazení pro [Microsoft Intune agenta MDM pro MacOS](macos-shell-scripts.md#microsoft-intune-mdm-agent-for-macos).
7. V okně **Revize a přidat**se zobrazí souhrn nastavení, které jste nakonfigurovali. Vyberte **Přidat** a uložte skript. Když vyberete **Přidat**, zásada skriptu se nasadí do skupin, které jste zvolili.

Skript, který jste vytvořili, se teď zobrazí v seznamu skriptů. 

## <a name="monitor-a-shell-script-policy"></a>Monitorování zásad skriptů prostředí
Kliknutím na jednu z následujících sestav můžete monitorovat stav spuštění všech přiřazených skriptů pro uživatele a zařízení:
- **Skripty** > **Vybrat skript, který bude monitorovat** **stav zařízení** > 
- **Skripty** > **výběru skriptu pro sledování** **stavu uživatele** > 

>[!IMPORTANT]
> Bez ohledu na zvolenou **frekvenci skriptu**se stav spuštění skriptu oznamuje jenom při prvním spuštění skriptu. Stav spuštění skriptu není aktualizován při dalších spuštěních. Aktualizované skripty se však považují za nové skripty a stav spuštění bude hlášen znovu.

Po spuštění skriptu vrátí jeden z následujících stavů:
- Stav spuštění skriptu **se nezdařilo** , indikuje, že skript vrátil nenulový ukončovací kód, nebo je skript poškozený. 
- Stav spuštění skriptu **úspěch** indikuje, že skript vrátil nulu jako ukončovací kód. 

## <a name="frequently-asked-questions"></a>Nejčastější dotazy
### <a name="why-are-assigned-shell-scripts-not-running-on-the-device"></a>Proč jsou přiřazené skripty prostředí v zařízení nespuštěny?
Může existovat několik důvodů:
* Agent může být muset vrátit se změnami, aby přijímal nové nebo aktualizované skripty. Tento proces vrácení se změnami probíhá každých 8 hodin a liší se od vrácení se změnami MDM. Ujistěte se, že je zařízení spuštěno a připojené k síti pro úspěšné přihlášení agenta a počkejte na vrácení se změnami agenta.
* Agent nemusí být nainstalován. Ověřte, že je agent nainstalovaný na `/Library/Intune/Microsoft Intune Agent.app` na zařízení macOS.
* Agent nemůže být v dobrém stavu. Agent se pokusí o zotavení po dobu 24 hodin, odebrat sám sebe a znovu nainstalovat, pokud jsou skripty prostředí stále přiřazeny.

### <a name="how-frequently-is-script-run-status-reported"></a>Jak často je stav spuštění skriptu hlášeno?
Stav spuštění skriptu se oznamuje konzole pro správu Microsoft Endpoint Manageru hned po dokončení spuštění skriptu. Pokud je naplánováno pravidelné spouštění skriptu v nastavené četnosti, ohlásí stav pouze při prvním spuštění.

### <a name="when-are-shell-scripts-run-again"></a>Kdy se skripty prostředí spouštějí znovu?
Skript se spustí znovu pouze v případě, že je **maximální počet pokusů o opakování skriptu, pokud** je nakonfigurováno nastavení chyby skriptu a při spuštění skriptu dojde k chybě. Pokud je **maximální počet pokusů o opakování skriptu, pokud** není nakonfigurován skript a dojde k selhání skriptu při spuštění, nebude znovu spuštěn a stav spuštění bude hlášen jako **neúspěšný**. 

### <a name="what-intune-role-permissions-are-required-for-shell-scripts"></a>Jaká oprávnění role Intune jsou vyžadována pro skripty prostředí?
Vaše přiřazená role Intune vyžaduje **Konfigurace zařízení** oprávnění k odstraňování, přiřazování, vytváření, aktualizaci nebo čtení skriptů prostředí.

## <a name="microsoft-intune-mdm-agent-for-macos"></a>Microsoft Intune agenta MDM pro macOS
 ### <a name="why-is-the-agent-required"></a>Proč je agent vyžadován?
 Aby bylo možné rozšířit možnosti správy zařízení, které nejsou podporované nativním operačním systémem macOS, je nutné na spravovaných zařízeních macOS nainstalovat agenta MDM. Microsoft Intune
 
 ### <a name="how-is-the-agent-installed"></a>Jak je nainstalován agent?
 Na zařízeních macOS spravovaných pomocí Intune se automaticky a tiše nainstaluje agent, kterému přiřadíte aspoň jeden skript prostředí v centru pro správu Microsoft Endpoint Manageru. Agent se instaluje na `/Library/Intune/Microsoft Intune Agent.app`, pokud je k dispozici, a nezobrazuje se ve **vyhledávači** > **aplikacích** na zařízeních MacOS. Agent se při spuštění na zařízeních macOS zobrazí jako `IntuneMdmAgent` v **monitorování aktivity** .

### <a name="what-does-the-agent-do"></a>Co agent dělá?
 - Před vrácením se změnami pro příjem skriptů prostředí pro zařízení macOS se agent tiše ověřuje pomocí služeb Intune.
 - Agent obdrží přiřazené skripty prostředí a spustí skripty na základě nakonfigurovaného plánu, pokusů o opakování, nastavení oznámení a dalších nastavení nastavených správcem.
 - Agent kontroluje nové nebo aktualizované skripty se službami Intune obvykle každých 8 hodin. Tato operace vrácení se změnami je nezávislá na vrácení se změnami MDM. 

 >[!NOTE]
 > Akce **kontroly nastavení** v portál společnosti vynutí pouze vrácení se změnami MDM. Neexistují žádné ruční akce pro kontrolu agenta.

 ### <a name="when-is-the-agent-removed"></a>Kdy je agent odebrán?
 Existuje několik podmínek, které mohou způsobit odebrání agenta ze zařízení, například:
 - Skripty prostředí již nejsou přiřazeny k zařízení. 
 - Zařízení macOS již není spravováno.
 - Agent je ve stavu nezotavitelné po dobu delší než 24 hodin (doba provozu zařízení).

 ### <a name="how-to-turn-off-usage-data-sent-to-microsoft-for-shell-scripts"></a>Jak vypnout data o využití, která se odesílají do Microsoftu pro skripty prostředí?
 Pokud chcete vypnout data o využití, která se Microsoftu odesílají z agenta Intune MDM, otevřete Portál společnosti a vyberte **nabídka** > **Předvolby** > *zrušte zaškrtnutí políčka Povolit Microsoftu shromažďovat data o využití*. Tím se vypnou data o využití, která se odesílají jak pro agenta Intune MDM, tak pro Portál společnosti.

## <a name="known-issues"></a>Známé problémy
- **Přiřazení skupiny uživatelů:** Skripty prostředí přiřazené skupinám uživatelů se nevztahují na zařízení. Přiřazení skupiny uživatelů se v tuto chvíli ve verzi Preview nepodporuje. K přiřazení skriptů použijte přiřazení skupiny zařízení.
- **Shromažďovat protokoly:** Akce shromáždit protokoly je viditelná. Ale při pokusu o shromažďování protokolů se zobrazí zpráva "došlo k chybě" a nezachytí protokoly. Shromažďování protokolů není v současné době ve verzi Preview podporováno.
- **Žádný stav spuštění skriptu:** V nepravděpodobném případě, že se na zařízení přijme skript a zařízení přejde do režimu offline, než se nahlásí stav spuštění, zařízení neohlásí stav spuštění skriptu v konzole pro správu.
- **Zpráva o stavu uživatele:** Existuje prázdný problém sestavy. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **monitor**. Stav uživatele zobrazuje prázdnou sestavu.

## <a name="next-steps"></a>Další kroky

- [Vytvoření zásady dodržování předpisů v Microsoft Intune](..\protect\create-compliance-policy.md)
