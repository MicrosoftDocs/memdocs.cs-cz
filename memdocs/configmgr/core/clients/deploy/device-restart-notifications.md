---
title: Oznámení o restartování zařízení
titleSuffix: Configuration Manager
description: Restartujte chování oznámení pro různá nastavení klienta v Configuration Manager.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5b6d383b2d5904f4d31fff5f549127dc21c39f29
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713391"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Oznámení o restartování zařízení v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Oznámení, která uživatel obdrží pro čekání na restartování zařízení, se můžou lišit v závislosti na [nastaveních klienta restartování počítače](about-client-settings.md#computer-restart) a na používané verzi Configuration Manager. Tento článek pomáhá správcům určit, jaké uživatelské prostředí slouží pro nedokončená oznámení o restartování zařízení.

>[!NOTE]
> - Tento článek se zaměřuje na nastavení klienta nalezené v Configuration Manager verze 1902 a verze 1906.


## <a name="deployment-types-for-restart-notifications"></a>Typy nasazení pro oznámení o restartování

[Nastavení klienta restartovat počítač](about-client-settings.md#computer-restart) změní uživatelské prostředí pro všechna požadovaná nasazení, která vyžadují restartování následujících typů:

- [Aplikace](../../../apps/deploy-use/deploy-applications.md)
- [Pořadí úkolů](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Aktualizace softwaru](../../../sum/deploy-use/deploy-software-updates.md)

## <a name="restart-notification-types"></a>Typy oznámení o restartování

Pokud je vyžadováno restartování, koncovému uživateli se zobrazí oznámení o nadcházejícím restartování. Existují čtyři obecná oznámení, která uživatelé mohou obdržet:

**Informační zpráva oznamující** , že je potřeba restartovat počítač. Informace v oznámení informační zprávy se můžou lišit v závislosti na verzi Configuration Manager, kterou používáte. Tento typ oznámení je nativní pro operační systém Windows a pomocí tohoto typu oznámení můžete také vidět software třetí strany.

![Informační zpráva o čekání na restartování](media/3555947-restart-toast.png)

Oznámení centra softwaru s možností odložení, která zobrazuje zbývající čas před vysazením restartování. Tato zpráva se může lišit v závislosti na vaší verzi Configuration Manager.

![Čeká na restartování oznámení centra softwaru s tlačítkem pro odložení](media/3976435-snooze-restart-countdown.png)

Konečné oznámení o odpočítávání centra softwaru, které uživatel nemůže zavřít. Tlačítko pro odložení je zobrazeno šedě.

![Oznámení o konečném odpočítávání centra softwaru](media/3976435-final-restart-countdown.png)

Pokud uživatel proaktivně nainstaluje požadovaný software, který vyžaduje restart před konečným termínem, uvidí jiné oznámení. K následujícímu oznámení dojde, pokud nastavení činnost koncového uživatele umožňuje oznámení a nepoužíváte pro nasazení oznámení informační zprávy. Další informace o konfiguraci těchto nastavení najdete v tématu [nasazení nastavení **uživatelského prostředí** ](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) a [oznámení uživatelů pro požadovaná nasazení](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

![Oznámení o proaktivním nainstalovaném softwaru](media/3976435-proactive-user-restart-notification.png)

- Pokud nepoužíváte informační zprávy, bude dialog pro software označený jako **dostupný** podobný aktivnímu nainstalovanému softwaru.

  - U **dostupného** softwaru oznámení nemá konečný termín pro restartování a uživatel může zvolit vlastní interval odložení. Další informace najdete v tématu [nastavení schválení](../../../apps/deploy-use/deploy-applications.md#bkmk_approval).

    ![Software označený jako "dostupný" nemá konečný termín pro restartování v oznámení.](media/3555947-deployment-marked-available-restart.png)

## <a name="device-restart-notifications-in-version-1902"></a>Oznámení o restartování zařízení ve verzi 1902

<!--3555947-->
Někdy se uživatelům nezobrazuje zpráva informující o systému Windows o restartování nebo požadovaném nasazení. Pak nevidí prostředí, které připomíná připomenutí k odložení. Toto chování může vést k nedostatečnému uživatelskému prostředí, když klient dosáhne konečného termínu.

Od verze 1902 platí, že když se vyžadují změny softwaru, nebo nasazení potřebují restartovat, máte možnost použít více rušivých dialogových oken.

V okně [restartovat počítač](about-client-settings.md#computer-restart) v nastavení klienta Povolte následující možnost: **Pokud nasazení vyžaduje restart, místo oznámení informačního systému se zobrazí dialogové okno s uživatelem**.  

Konfigurace tohoto nastavení klienta změní činnost koncového uživatele pro všechna požadovaná nasazení, která vyžadují restart ze zpráv oznámení:

![Informační zpráva oznamující, že je vyžadováno restartování](media/3555947-restart-toast-initial.png)  

Do dialogového okna více rušivého centra softwaru:

![Dialogové okno pro restartování počítače](media/3976435-proactive-user-restart-notification.png)

Pokud uživatel po instalaci nerestartoval své zařízení, obdrží oznámení jako připomenutí. Toto dočasné připomenutí se uživateli zobrazí na základě nastavení klienta: **Zobrazit dočasné oznámení uživateli, které udává interval před odhlášením uživatele nebo restartováním počítače (minuty)**. Toto nastavení je celkový čas, po který musí uživatel restartovat počítač, než bude vynucen restart.

- Dočasné oznámení při použití oznámení informačních zpráv:

  ![Informační zpráva o čekání na restartování](media/3555947-restart-toast.png)

- Dočasné oznámení při použití dialogového okna Centrum softwaru, nikoli informační zprávy:

  ![Čeká na restartování oznámení centra softwaru s tlačítkem pro odložení](media/3555947-1902-hide-notification.png)

Pokud se uživatel po dočasném oznámení nerestartuje, bude mu přiděleno konečné oznámení o odpočítávání, které nepůjde zavřít. Čas, kdy se zobrazí konečné oznámení, je založen na nastavení klienta: **zobrazí dialogové okno, které uživatel nemůže zavřít, který zobrazí interval odpočítávání před odhlášením uživatele nebo restartování počítače (minuty)**. Pokud je například nastavení 60, pak hodina před restartováním, zobrazí se konečné oznámení uživateli:

![Oznámení o konečném odpočítávání centra softwaru](media/3555947-1902-final-countdown.png)

Následující nastavení musí být kratší než v době trvání, než má nejkratší [okno údržby](../manage/collections/use-maintenance-windows.md) , které se pro počítač použije:

- **Zobrazit dočasné oznámení uživateli, které udává interval před odhlášením uživatele nebo restartováním počítače (minuty)**
- **Zobrazí dialogové okno, které uživatel nemůže zavřít, který zobrazuje interval odpočítávání před odhlášením uživatele nebo restartování počítače (minuty).**

> [!IMPORTANT]
> V Configuration Manager 1902 se za určitých okolností dialogová okna nebudou nahrazena informačními oznámeními. Pokud chcete tento problém vyřešit, nainstalujte [kumulativní aktualizaci pro Configuration Manager verze 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="device-restart-notifications-starting-in-version-1906"></a>Oznámení o restartování zařízení od verze 1906
<!--3976435-->
Někteří správci upřednostňují časté oznámení o restartování a krátký časový rámec, který umožňuje odložené restartování. Jiní správci umožňují uživatelům odložit restartování po delší dobu a chtít, aby se uživatelům zobrazilo oznámení o nedokončeném restartování. Configuration Manager verze 1906 poskytuje správci větší kontrolu nad časováním a četností oznámení o restartování. V 1906 byly zavedeny následující položky, které správcům poskytují větší kontrolu:

- **Zadejte dobu opakovaného přiložení pro odpočítávání oznámení restartování počítače (minuty)** , které se přidalo do [nastavení klienta restartovat počítač](about-client-settings.md#computer-restart).
- Maximální hodnota pro **zobrazení dočasného oznámení uživateli, které udává interval před odhlášením uživatele nebo restartováním počítače (minuty)** od 1440 minut (24 hodin) do 20160 minut (dva týdny).
- Uživateli se v oznámení o restartu nezobrazuje indikátor průběhu, dokud bude nedokončené restartování méně než 24 hodin.

### <a name="notifications-when-required-software-is-installed-at-or-after-the-deadline"></a>Oznámení v případě, že je požadovaný software nainstalován v nebo po konečném termínu

Pokud je požadovaný software nainstalovaný v nebo po konečném termínu, uživatelé uvidí oznámení v závislosti na nastaveních klienta, která jste vybrali.

Pokud nastavení **, když nasazení vyžaduje restart, zobrazí uživateli dialogové okno místo oznámení informační** zpráva je nastaveno na:

- **Žádná** oznámení se používají až po dosažení konečného oznámení o odpočítávání.
- **Ano** – zobrazuje se oznámení centra softwaru.
  - Pokud je restartování delší než 24 hodin, zobrazí se odhadovaný čas restartování. Časování tohoto oznámení je založené na nastavení: **zobrazí pro uživatele dočasné oznámení, které určuje interval před odhlášením uživatele nebo restartováním počítače (minuty)**.

     ![Doba restartu je víc než 24 hodin.](media/3976435-notification-greater-than-24-hours.png)

  - Pokud je restartování méně než 24 hodin pryč, zobrazí se indikátor průběhu. Časování tohoto oznámení je založené na nastavení: **Zobrazit pro uživatele dočasné oznámení, které označuje interval před odhlášením uživatele nebo restartováním počítače (minuty)** .

     ![Čas restartování je pryč méně než 24 hodin.](media/3976435-notification-less-than-24-hours.png)

Pokud uživatel vybere tlačítko pro **odložení** , dojde k dalšímu dočasnému oznámení po uplynutí doby pro odložení, za předpokladu, že ještě nedosáhli konečného odpočítávání. Časování dalšího oznámení je založené na nastavení: **Zadejte dobu odložení pro odpočítávání oznámení restartování počítače (hodiny)**. Pokud uživatel vybere příkaz **připomenout** a interval odložení bude jedna hodina, bude uživatel znovu upozorněn za 60 minut za předpokladu, že ještě nedosáhl konečné odpočítávání.

Po dosažení konečného odpočítávání je uživateli přiděleno oznámení, které nelze zavřít. Indikátor průběhu je červený a uživatel se nemůže **připomenout**znovu.

![Konečné odpočítávání oznámení centra softwaru ve verzi 1906](media/3976435-1906-final-restart-countdown.png)

### <a name="the-user-proactively-installs-before-the-deadline"></a>Uživatel provede proaktivní instalaci před konečným termínem.

Pokud uživatel proaktivně nainstaluje požadovaný software, který vyžaduje restart před konečným termínem, uvidí jiné oznámení. Další informace o konfiguraci těchto nastavení najdete v tématu [nasazení nastavení **uživatelského prostředí** ](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) a [oznámení uživatelů pro požadovaná nasazení](../../../apps/deploy-use/deploy-applications.md#bkmk_notify). 

K následujícímu oznámení dojde, pokud nastavení činnost koncového uživatele umožňuje oznámení a nepoužíváte pro nasazení oznámení informační zprávy:

![Oznámení o proaktivním nainstalovaném softwaru](media/3976435-proactive-user-restart-notification.png)

Jakmile je dosaženo konečného termínu pro software, budou oznámení v případě, že je [vyžadován požadovaný software, nainstalován v nebo po následování chování konečného termínu](#notifications-when-required-software-is-installed-at-or-after-the-deadline) .

## <a name="log-files"></a>Soubory protokolů

Pro řešení potíží s restartováním zařízení použijte protokol **RebootCoordinator. log** a **SCNotify. log** . V závislosti na použitém typu nasazení možná budete muset použít taky další [soubory protokolů](../../plan-design/hierarchy/log-files.md) klienta.

## <a name="next-steps"></a>Další kroky

- [Úvod do správy aplikací](../../../apps/understand/introduction-to-application-management.md)
- [Úvod k nasazení operačního systému](../../../osd/understand/introduction-to-operating-system-deployment.md)
- [Úvod ke správě aktualizací softwaru](../../../sum/understand/software-updates-introduction.md)
