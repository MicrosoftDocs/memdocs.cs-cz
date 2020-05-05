---
title: Možnosti ve verzi Technical Preview 1704
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview pro Configuration Manager verze 1704.
ms.date: 04/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e318e705-20f2-417d-8cde-7dfe661b2fa7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c24b9a6e4f6f123e0456b9f1337a7c3b19ab6962
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721406"
---
# <a name="capabilities-in-technical-preview-1704-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1704 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1704. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview. Před instalací této verze Technical Preview si Projděte úvodní téma, [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md), abyste se seznámili se základními požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.    


**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  

## <a name="configure-android-apps-with-app-configuration-policies"></a>Konfigurace aplikací pro Android pomocí zásad konfigurace aplikací
Zásady konfigurace aplikací v Configuration Manager můžete použít k distribuci nastavení, která se můžou požadovat, když uživatel spustí aplikaci na zařízeních s Androidem for Work. Zásady konfigurace aplikací pro Android jsou dostupné jenom v zařízeních s Androidem for Work a platí pro schválené aplikace z obchodu Play for Work.

### <a name="try-it-out"></a>Vyzkoušejte si to.                 

V konzole Configuration Manager vyberte možnost **softwarová knihovna** > **aplikace Správa** > aplikací**zásady konfigurace** a klikněte na **vytvořit zásadu konfigurace aplikace**. Na stránce **Obecné** v průvodci teď můžete **Vybrat typ zásady konfigurace**. Zadejte platformu, na kterou cílí zásady konfigurace aplikace: **zásady konfigurace pro aplikace pro Android for Work**. Pak můžete **zadat páry název-hodnota** nebo **Vyhledat soubor JSON seznamu vlastností**. Nové zásady konfigurace aplikací se zobrazí v pracovním prostoru **softwarová knihovna** v uzlu **zásady konfigurace aplikace** . Pokud chcete přidružit zásady konfigurace aplikace k nasazení aplikace pro Android for Work, nasaďte aplikaci obvyklým způsobem pomocí postupu v tématu [nasazení aplikací](../../apps/deploy-use/deploy-applications.md) .

## <a name="hardware-inventory-collects-secure-boot-information"></a>Inventář hardwaru shromažďuje informace o zabezpečeném spuštění.
Inventář hardwaru nyní shromažďuje informace o tom, zda je na klientech povoleno zabezpečené spouštění. Tyto informace jsou uloženy ve třídě **SMS_Firmware** (představené ve verzi 1702) a jsou ve výchozím nastavení povoleny v inventáři hardwaru. Další informace o inventáři hardwaru najdete v tématu [Konfigurace inventáře hardwaru](../clients/manage/inventory/configure-hardware-inventory.md).

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Přidání podřízených sekvencí úloh do pořadí úkolů
V této verzi můžete přidat nový krok pořadí úloh, který spustí jiné pořadí úkolů, které vytvoří vztah nadřazenosti/podřízenosti mezi pořadím úkolů. To vám umožní vytvořit další modulární pořadí úloh, která můžete znovu použít.  

Při přidávání podřízeného pořadí úloh do pořadí úloh Vezměte v úvahu následující:

- Sekvence nadřazených a podřízených úloh jsou efektivně zkombinovány do jediné zásady, kterou klient spustí.
- Přidání podřízeného pořadí úkolů, které je nadřazené jiné sekvenci úloh, není podporované.
- Prostředí je globální. Pokud je například proměnná nastavena nadřazeným pořadím úloh a následně změněna podřízeným pořadím úkolů, proměnná zůstane přesunuta do popředí. Podobně pokud podřízené pořadí úkolů vytvoří novou proměnnou, je tato proměnná k dispozici pro zbývající kroky v nadřazeném pořadí úkolů.
- Stavové zprávy jsou posílány na normální pro jednu operaci pořadí úkolů.
- Pořadí úkolů zapisují položky do souboru souboru Smsts. log s novými položkami protokolu, které se při spuštění podřízeného pořadí úkolů vymažou.
- V Technical Preview pro Configuration Manager verze 1704, pokud podřízená pořadí úloh odkazují na libovolný balíček a spouštíte nadřazené pořadí úkolů z centra softwaru, klient nenalezne obsah balíčku, když je spuštěno podřízené pořadí úkolů. V tomto scénáři je nutné spustit pořadí úloh z média (spouštěcí médium, technologie PXE atd.).  

    Pokud podřízené pořadí úkolů používá kroky, jako je **příkazový řádek Run** (bez odkazu na balíček), **Format**, **BitLocker**atd., pak se pořadí úkolů úspěšně spustí z centra softwaru.

### <a name="to-add-a-child-task-sequence-to-a-task-sequence"></a>Přidání podřízeného pořadí úloh do pořadí úloh
1. V editoru pořadí úloh klikněte na tlačítko **Přidat**, vyberte možnost **Obecné**a klikněte na možnost **Spustit pořadí úloh**.
2. Kliknutím na **Procházet** vyberte podřízené pořadí úkolů.  

## <a name="reload-boot-images-with-current-windows-pe-version"></a>Opětovné načtení spouštěcích imagí s aktuální verzí prostředí Windows PE
Když spouštíte **distribuční body aktualizace** na vybrané spouštěcí imagi, můžete si teď zvolit, že se má v spouštěcí imagi znovu načíst nejnovější verze prostředí Windows PE (z instalačního adresáře Windows ADK). Na stránce **Obecné** v průvodci najdete informace o verzi Windows ADK nainstalované na serveru lokality, verzi Windows ADK, ze které se používalo prostředí Windows PE ve spouštěcí imagi, a verzi klienta Configuration Manager. Tyto informace můžete použít k určení toho, jestli se spouštěcí image má znovu načíst. Při prohlížení spouštěcích imagí v uzlu **spouštěcí bitové kopie** se přidal také nový sloupec (**verze klienta**), abyste věděli, jaká verze Configuration Manager klient používá.

### <a name="to-reload-a-boot-image-with-the-current-windows-pe-version"></a>Opětovné načtení spouštěcí bitové kopie s aktuální verzí prostředí Windows PE

1. V konzole Configuration Manager v části **softwarová knihovna** > **spouštěcí bitové kopie****operačních systémů** > .
2. Vyberte spouštěcí bitovou kopii a klikněte na **Aktualizovat distribuční body**.
3. Na stránce **Obecné** v průvodci vyberte možnost **znovu načíst spouštěcí bitovou kopii pomocí aktuální verze prostředí Windows PE z nainstalované sady Windows ADK**.

## <a name="improvements-to-operating-system-deployment"></a>Vylepšení nasazení operačního systému
Provedli jsme následující vylepšení nasazení operačního systému, což bylo výsledkem vašich názorů na hlas uživatele.

- [Nový sloupec **verze operačního** systému pro bitové kopie operačních systémů](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17558407-add-a-column-to-the-operating-system-images-node-f): Přidali jsme nový sloupec s názvem **verze operačního** systému, který zobrazí verzi operačního systému pro bitovou kopii při zobrazení informací v uzlech balíčky s upgradem **operačního systému** a **upgrady operačního systému** . Pouze verze prvního indexu v. Zobrazí se soubor WIM. Chcete-li zkontrolovat verze operačního systému pro jiné indexy, klikněte na kartu **Podrobnosti** pro obrázek.

- Efektivnější [protokolování v souboru Smsts. log](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16791919-stop-filling-smsts-log-with-useless): od této verze už nepoužíváme zápis položek do souboru souboru Smsts. log CCM_CIVersionInfo. PolicyID informace. Před touto verzí může být s těmito informacemi spousta záznamů, což mělo těžko najít v souboru protokolu další relevantní informace.
