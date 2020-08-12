---
title: Uživatelská prostředí pro nasazení operačního systému
titleSuffix: Configuration Manager
description: Seznamte se s uživatelským prostředím, jako je průběh pořadí úloh a Průvodce médii pro nasazení operačního systému v Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58849e40-30d5-4153-84b3-ca4af3a4f09d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7ad20f80f4727fe18947bed05ded6e7b107fab12
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124080"
---
# <a name="user-experiences-for-os-deployment"></a>Uživatelská prostředí pro nasazení operačního systému

*Platí pro: Configuration Manager (Current Branch)*

Po [nasazení pořadí úkolů](../deploy-use/deploy-a-task-sequence.md)v závislosti na scénáři existují různé způsoby, jak můžou uživatelé s nasazením pracovat. V tomto článku se dozvíte, jak hlavní uživatelské prostředí s nasazeními operačních systémů a jak je můžete nakonfigurovat:

- Uživatelské oznámení centra softwaru pro vysoce působivé nasazení
- Ukázka spouštěcího prostředí PXE
- Průvodce pořadím úloh z média
- Okno průběhu při spuštění pořadí úkolů
- Chybové okno při neúspěchu pořadí úloh

## <a name="software-center"></a>Centrum softwaru

U vysoce ovlivněného nasazení můžete upravit zprávu, kterou Centrum softwaru zobrazuje. Když uživatel otevře nasazení operačního systému v centru softwaru, zobrazí se zpráva podobná následujícímu oknu:

![Přizpůsobené oznámení pořadí úkolů koncovému uživateli z centra softwaru](../media/user-notification-enduser.png)

Další informace o přizpůsobení zprávy v tomto okně najdete v tématu [Vytvoření vlastního oznámení pro nasazení s vysokým rizikem](../deploy-use/manage-task-sequences-to-automate-tasks.md#create-a-custom-notification-for-high-risk-deployments).

Můžete také přizpůsobit název organizace v horní části okna. (Výše uvedený příklad ukazuje výchozí hodnotu `IT Organization` ). Změňte nastavení klienta **název organizace** ve skupině **Počítačový agent** . Další informace najdete v tématu [informace o nastavení klienta](../../core/clients/deploy/about-client-settings.md#computer-agent).

<!--
optional vs required
**Allow user to interact** on required deployment?
-->

Další informace najdete v tématu [použití centra softwaru k nasazení Windows přes síť](../deploy-use/use-software-center-to-deploy-windows-over-the-network.md).

## <a name="pxe"></a>PXE

Různé hardwarové modely mají různé prostředí pro technologii PXE. Aby bylo možné spustit síť, zařízení s rozhraním UEFI obvykle používají `Enter` klíč a zařízení založená na systému BIOS používají `F12` klíč.

Následující příklad ukazuje prostředí PXE technologie Hyper-V Gen1 (BIOS):

![Příklad obrazovky prostředí BIOS PXE z virtuálního počítače s technologií Hyper-V](media/hyperv-pxe.png)

Po úspěšném spuštění zařízení přes PXE se chová podobně jako u spouštěcího média. Další informace najdete v další části [Průvodce pořadím úloh](#task-sequence-wizard).

Další informace najdete v tématu [použití technologie PXE k nasazení Windows přes síť](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

> [!WARNING]
> Pokud používáte nasazení PXE a nakonfigurujete hardware zařízení se síťovým adaptérem jako prvním spouštěcím zařízením, můžou tato zařízení automaticky spustit pořadí úloh nasazení operačního systému bez zásahu uživatele. Ověřování nasazení nespravuje tuto konfiguraci. I když tato konfigurace může zjednodušit proces a omezit interakci s uživatelem, umístí zařízení s větším rizikem na nechtěné obnovení obrazu.

## <a name="task-sequence-wizard"></a>Průvodce pořadím úloh

Když použijete [médium pořadí úkolů](../deploy-use/create-task-sequence-media.md), spustí se Průvodce pořadím úkolů s tímto procesem.

### <a name="welcome-to-the-task-sequence-wizard"></a>Vítá vás Průvodce pořadím úloh.

![Snímek obrazovky s hlavní stránkou Průvodce pořadím úloh](media/welcome-task-sequence-wizard.png)

- Pokud médium chráníte heslem, musí uživatel na této úvodní stránce zadat heslo.

- Pokud chcete zadat statickou IP adresu nebo jiné vlastní nastavení sítě, vyberte **Konfigurovat nastavení sítě** . V opačném případě zařízení ve výchozím nastavení používá protokol DHCP.

- Pokud vaše síť vyžaduje proxy server, vyberte **Konfigurovat nastavení proxy serveru**.

### <a name="select-a-task-sequence-to-run"></a>Vyberte pořadí úloh, které se má spustit.

Pokud nasadíte více než jedno pořadí úloh do zařízení, zobrazí se tato stránka, kde můžete vybrat pořadí úloh. Nezapomeňte použít název a popis pořadí úkolů, které mohou uživatelé pochopit.

![Snímek obrazovky se stránkou výběr pořadí úkolů průvodce pořadím úloh](media/task-sequence-wizard-select.png)

### <a name="edit-task-sequence-variables"></a>Upravit proměnné pořadí úkolů

Pokud některé proměnné pořadí úkolů mají prázdné hodnoty, Průvodce zobrazí stránku pro úpravu hodnot proměnných.

![Snímek obrazovky se stránkou pro úpravy proměnných pořadí úloh v průvodci pořadím úloh](media/task-sequence-wizard-variables.png)

## <a name="prestart-commands"></a>Příkazy před zahájením

Můžete přizpůsobit médium pořadí úloh nebo spouštěcí bitové kopie pro spuštění předspouštěcího příkazu. Před spuštěním pořadí úloh se spustí předspouštěcí příkaz. Následující akce jsou některé z nejběžnějších:

- Vyzvat uživatele k zadání dynamických hodnot, jako je název počítače
- Zadat konfiguraci sítě
- Nastavit spřažení uživatelských zařízení

Předstartovní příkaz je příkazový řádek, který zadáte pomocí skriptu nebo programu. Uživatelské prostředí je pro tento skript nebo program jedinečné.

Další informace najdete v následujících článcích:

- [Příkazy před zahájením pro médium pořadí úkolů](prestart-commands-for-task-sequence-media.md)
- [Správa spouštěcích imagí](../get-started/manage-boot-images.md#customization)
- [Médium pořadí úloh](../deploy-use/create-task-sequence-media.md)

## <a name="task-sequence-progress"></a>Průběh pořadí úkolů

Po spuštění pořadí úkolů se zobrazí okno **průběh instalace** :

![Příklad okna průběhu pořadí úkolů](media/task-sequence-progress.png)

- Toto okno je vždycky nahoře; můžete ho přesunout, ale nemůžete ho zavřít ani minimalizovat.

- Název organizace můžete přizpůsobit v horní části okna. (Výše uvedený příklad ukazuje výchozí hodnotu `IT Organization` ). Změňte nastavení klienta **název organizace** ve skupině **Počítačový agent** . Další informace najdete v tématu [informace o nastavení klienta](../../core/clients/deploy/about-client-settings.md#computer-agent).

    > [!TIP]
    > Pořadí úkolů ukládá tuto hodnotu do proměnné jen pro čtení [_SMSTSOrgName](task-sequence-variables.md#SMSTSOrgName).

- Podnadpis lze přizpůsobit. (Výše uvedený příklad ukazuje výchozí hodnotu, `Running: <task sequence name>` .) Ve vlastnostech pořadí úkolů vyberte možnost pro text oznámení o průběhu **použít vlastní text** . Povoluje se maximálně 255 znaků.

- **Spouští se akce**: první řádek zobrazuje název aktuálního kroku pořadí úkolů. Indikátor průběhu pod ním ukazuje celkové dokončení pořadí úkolů.

- Druhý řádek obsahuje pouze některé kroky, které poskytují podrobnější průběh.

- Proměnnou pořadí úloh [TSDisableProgressUI](task-sequence-variables.md#TSDisableProgressUI) použijte k určení, kdy se v pořadí úkolů zobrazuje průběh.

    Chcete-li zcela zakázat okno průběh, zakažte možnost **Zobrazit průběh pořadí úloh** na stránce **činnost koncového uživatele** v nasazení pořadí úloh.

Počínaje verzí 2002 obsahuje okno průběh pořadí úloh následující vylepšení:<!--5932692-->

- Zobrazuje aktuální číslo kroku, celkový počet kroků a procento dokončení.

- Zvětšením šířky okna získáte více místa, aby bylo možné lépe zobrazit název organizace na jednom řádku.

![Příklad okna průběhu pořadí úkolů](media/2356386-task-sequence-progress.png)

Ve výchozím nastavení používá okno průběh pořadí úloh existující text. Pokud neprovedete žádné změny, bude i nadále fungovat stejně jako verze 1910 a starší. Chcete-li zobrazit nové informace o průběhu, zadejte proměnnou pořadí úloh [TSProgressInfoLevel](task-sequence-variables.md#TSProgressInfoLevel).

Počet a procento dokončení jsou určené pouze pro účely obecné doprovodné materiály. Tyto hodnoty jsou založené na celkovém počtu kroků v pořadí úkolů. V případě složitějšího pořadí úkolů s kroky, které jsou podmíněně spouštěny na základě logiky pořadí úkolů, může být průběh nelineární.

Celkový počet kroků v pořadí úkolů neobsahuje následující položky:

- Skupiny. Tato položka je kontejnerem pro jiné kroky, nikoli pro samotný krok.

- Instance kroku **pořadí úkolů Spustit** . Tento krok je kontejnerem pro další kroky.

- Kroky, které výslovně zakážete. Zakázaný krok neběží během pořadí úkolů.

- Počínaje verzí 2006 nepočítá povolené kroky v zakázané skupině.<!--6448412--> Ve verzi 2002 jsou povolené kroky v zakázané skupině pořád zahrnuté v celkovém počtu.

## <a name="task-sequence-error"></a>Chyba pořadí úloh

Pokud pořadí úkolů neproběhne úspěšně, zobrazí se okno **chyby pořadí úkolů** .

![Příklad okna chyby pořadí úloh](media/task-sequence-error.png)

- Informace hlavičky přizpůsobíte stejně jako okno průběhu pořadí úkolů.

- Zobrazuje název pořadí úkolů, kód chyby a obecnou zprávu pro uživatele. Příklad: `Task sequence: Upgrade to Windows 10 Enterprise has failed with the error code (0x80004005). For more information, contact your system administrator or helpdesk operator.`

- Okno se automaticky zavře po uplynutí časového limitu. Ve výchozím nastavení je tento časový limit 15 minut. Tuto hodnotu můžete přizpůsobit pomocí proměnné pořadí úkolů [SMSTSErrorDialogTimeout](task-sequence-variables.md#SMSTSErrorDialogTimeout).
