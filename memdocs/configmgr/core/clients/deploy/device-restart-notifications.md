---
title: Oznámení o restartování zařízení
titleSuffix: Configuration Manager
description: Restartujte chování oznámení pro různá nastavení klienta v Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: feb9f4206df65ee34228577a9e589ddd1be72870
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127239"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Oznámení o restartování zařízení v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Oznámení, která uživatel obdrží pro čekání na restartování zařízení, se může lišit v závislosti na [nastaveních klienta restartování počítače](#client-settings) a na používané verzi Configuration Manager. Tento článek vám pomůže nakonfigurovat činnost koncového uživatele pro nedokončená oznámení o restartování zařízení.

## <a name="deployment-types-for-restart-notifications"></a>Typy nasazení pro oznámení o restartování

[Nastavení klienta restartovat počítač](#client-settings) změní uživatelské prostředí pro všechna požadovaná nasazení, která vyžadují restartování následujících typů:

- [Aplikace](../../../apps/deploy-use/deploy-applications.md)
- [Pořadí úkolů](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Aktualizace softwaru](../../../sum/deploy-use/deploy-software-updates.md)

## <a name="restart-notification-types"></a>Typy oznámení o restartování

Když zařízení vyžaduje restart, klient zobrazí koncovému uživateli oznámení o nadcházejícím restartování.

### <a name="toast-notification"></a>Informační oznámení

Informační zpráva systému Windows informuje uživatele o tom, že zařízení musí restartovat. Informace v oznámení informační zprávy se můžou lišit v závislosti na verzi Configuration Manager, kterou používáte. Tento typ oznámení je nativní pro operační systém Windows. Pomocí tohoto typu oznámení můžete také vidět software třetí strany.

:::image type="content" source="media/3555947-restart-toast.png" alt-text="Informační zpráva o čekání na restartování":::

### <a name="software-center-notification-with-snooze"></a>Oznámení centra softwaru s odložením

Centrum softwaru zobrazuje oznámení s možností odložení a zbývající čas před tím, než zařízení vynutí restartování. Tato zpráva se může lišit v závislosti na vaší verzi Configuration Manager.

:::image type="content" source="media/3976435-snooze-restart-countdown.png" alt-text="Čeká na restartování oznámení centra softwaru s tlačítkem pro odložení":::

### <a name="software-center-final-countdown-notification"></a>Oznámení o konečném odpočítávání centra softwaru

Centrum softwaru zobrazí toto konečné oznámení o odpočítávání, které uživatel nemůže zavřít nebo odložit.

:::image type="content" source="media/3976435-final-restart-countdown.png" alt-text="Oznámení o konečném odpočítávání centra softwaru":::

Počínaje verzí 1906 se uživateli v oznámení o restartu nezobrazuje indikátor průběhu, dokud nebude čekat na restartování před méně než 24 hodinami.

### <a name="software-center-notification-before-deadline"></a>Oznámení centra softwaru před konečným termínem

Pokud uživatel proaktivně nainstaluje požadovaný software před konečný termín a vyžaduje restart, uvidí jiné oznámení. K následujícímu oznámení dojde, pokud nastavení činnost koncového uživatele umožňuje oznámení a nepoužíváte pro nasazení oznámení informační zprávy. Další informace o konfiguraci těchto nastavení najdete v tématu [nasazení nastavení **uživatelského prostředí** ](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) a [oznámení uživatelů pro požadovaná nasazení](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

:::image type="content" source="media/3976435-proactive-user-restart-notification.png" alt-text="Oznámení o proaktivním nainstalovaném softwaru":::

#### <a name="available-apps"></a>Dostupné aplikace

Pokud nepoužíváte informační zprávy, bude dialog pro software označený jako **dostupný** podobný aktivnímu nainstalovanému softwaru. U **dostupného** softwaru oznámení nemá konečný termín pro restartování a uživatel může zvolit vlastní interval odložení. Další informace najdete v tématu [nastavení schválení](../../../apps/deploy-use/deploy-applications.md#bkmk_approval).

:::image type="content" source="media/3555947-deployment-marked-available-restart.png" alt-text="Dostupný software nemá konečný termín pro restartování v oznámení.":::

### <a name="software-center-notification-of-required-restart"></a>Oznámení centra softwaru o povinném restartování

<!--3601213-->

Počínaje verzí 2006 můžete nakonfigurovat nastavení klienta, aby se zabránilo automatickému restartování zařízení, když to nasazení vyžaduje. Když požadované nasazení potřebuje, aby se zařízení restartovalo, ale zakážete nastavení klienta **Configuration Manager může vynutit restartování zařízení**, zobrazí se následující oznámení:

:::image type="content" source="media/3601213-restart-your-computer.png" alt-text="Oznámení centra softwaru pro restartování počítače":::

Pokud toto **oznámení** odhlásíte, bude se znovu zobrazovat na základě způsobu konfigurace frekvence oznámení připomenutí restartování. Zařízení se nerestartuje, dokud nevyberete **restart** nebo ručně nerestartujete Windows.

> [!NOTE]
> Ve výchozím nastavení může Configuration Manager i nadále Vynutit restartování zařízení.

## <a name="client-settings"></a>Nastavení klienta

Chcete-li řídit chování při restartování klienta, nakonfigurujte následující nastavení klienta zařízení ve skupině **restartovat počítač** . Další informace najdete v tématu [Konfigurace nastavení klienta](configure-client-settings.md).

### <a name="configuration-manager-can-force-a-device-to-restart"></a>Configuration Manager může vynutit restartování zařízení

<!--3601213-->

Počínaje verzí 2006 můžete nakonfigurovat nastavení klienta, aby se zabránilo automatickému restartování zařízení, když to nasazení vyžaduje. Configuration Manager toto nastavení povolí ve výchozím nastavení.

> [!IMPORTANT]
> Toto nastavení klienta se vztahuje na všechna nasazení aplikace, aktualizace softwaru a balíčky na zařízení. Dokud uživatel ručně nerestartuje zařízení:
>
> - Aktualizace softwaru a revize aplikací se nemusí úplně nainstalovat.
> - Další instalace softwaru nemusí nastat

Když toto nastavení zakážete, nemůžete zadat množství času po uplynutí konečného termínu, kdy se zařízení restartuje, nebo se uživateli zobrazí konečné oznámení o odpočítávání.

> [!NOTE]
> Pokud chcete plně využít nové funkce Configuration Manager, po aktualizaci lokality aktualizujte také klienty na nejnovější verzi. I když se nové funkce zobrazí v konzole Configuration Manager, když aktualizujete lokalitu a konzolu, kompletní scénář nebude funkční, dokud nebude verze klienta zároveň nejnovější.

### <a name="specify-the-amount-of-time-after-the-deadline-before-a-device-gets-restarted-minutes"></a>Zadejte čas po uplynutí konečného termínu, než se zařízení restartuje (minuty).

Toto nastavení musí být kratší než doba trvání, než je u počítače použito nejkratší časové období údržby. Další informace o časových obdobích údržby najdete v tématu [použití časových období](../manage/collections/use-maintenance-windows.md)údržby.

Výchozí hodnota je 90 minut. Počínaje verzí 1906 se maximální hodnota zvýšila ze 1440 minut (24 hodin) na 20160 minut (dva týdny).

> [!NOTE]
> Toto nastavení dříve **znamenalo zobrazit dočasné oznámení uživateli, které udává interval před odhlášením uživatele nebo restartováním počítače (minuty)**.

### <a name="specify-the-amount-of-time-that-a-user-is-presented-a-final-countdown-notification-before-a-device-gets-restarted-minutes"></a>Zadejte dobu, po kterou se uživateli zobrazí konečné oznámení o odpočítávání, než se zařízení restartuje (minuty).

Toto nastavení musí být kratší než doba trvání, než je u počítače použito nejkratší časové období údržby. Další informace o časových obdobích údržby najdete v tématu [použití časových období](../manage/collections/use-maintenance-windows.md)údržby.

Výchozí hodnota je 15 minut.

> [!NOTE]
> Toto nastavení dříve vyvolalo **zobrazení dialogového okna, které uživatel nemůže zavřít, který zobrazuje interval odpočítávání před odhlášením uživatele nebo restartování počítače (minuty)**.

### <a name="specify-the-frequency-of-reminder-notifications-presented-to-the-user-after-the-deadline-before-a-device-gets-restarted-minutes"></a>Zadejte frekvenci oznámení připomenutí, která se uživateli zobrazí po uplynutí konečného termínu, než se zařízení restartuje (minuty).
<!--3976435-->
_Počínaje verzí 1906_

Tato hodnota trvání frekvence by měla být menší než hodnota **určující dobu, po jejímž uplynutí se zařízení restartuje (minuty)** minus hodnota **určující dobu, po kterou se uživateli zobrazí konečné oznámení o odpočítávání, než se zařízení restartuje (minuty)**. V opačném případě oznámení připomenutí nebudou fungovat.

Výchozí hodnota je 240 minut.

> [!NOTE]
> Toto nastavení dříve vyvolalo **zadání doby přiložení pro oznámení odpočítávání restartování počítače (minuty)**.

### <a name="when-a-deployment-requires-a-restart-show-a-dialog-window-to-the-user-instead-of-a-toast-notification"></a>Pokud nasazení vyžaduje restart, zobrazí se uživateli dialogové okno namísto informačního oznámení.
<!--3555947-->
Od verze 1902 se konfigurace tohoto nastavení změní na **Ano** . tím se uživatelské prostředí přizpůsobuje na více rušivých. Toto nastavení platí pro všechna nasazení aplikací, pořadí úloh a aktualizace softwaru. Další informace najdete v tématu [plánování centra softwaru](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact).

> [!IMPORTANT]
> V Configuration Manager 1902 se za určitých okolností dialogová okna nebudou nahrazena informačními oznámeními. Pokud chcete tento problém vyřešit, nainstalujte [kumulativní aktualizaci pro Configuration Manager verze 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="device-restart-notifications-version-1906"></a>Oznámení o restartování zařízení (verze 1906)
<!--3976435-->
Někteří zákazníci upřednostňují časté oznámení o restartování a umožňují uživatelům krátkou dobu odložení. Ostatní umožňují uživatelům odložit restartování po delší dobu a uživatelům, kteří čekají na restartování, upozorňovat i zřídka. Od verze Configuration Manager 1906 máte větší kontrolu nad časováním a četností oznámení o restartování.

### <a name="install-required-software-at-or-after-the-deadline"></a>Nainstalovat požadovaný software na konečný termín nebo za něj

Pokud je požadovaný software nainstalovaný v nebo po konečném termínu, uživatelé uvidí oznámení v závislosti na nastaveních klienta, která jste vybrali.

Pokud nastavení **, když nasazení vyžaduje restart, zobrazí uživateli dialogové okno místo oznámení informační** zpráva je nastaveno na:

- **Ne**: systém Windows zobrazuje informační zprávy, dokud nasazení nedosáhne konečného oznámení o odpočítávání.

- **Ano**: Centrum softwaru zobrazuje oznámení:

  - Pokud je restartování delší než 24 hodin, zobrazí se odhadované doba restartování. Časování tohoto oznámení je založené na nastavení: **Zadejte dobu, po jejímž uplynutí se zařízení restartuje (minuty)**.

    :::image type="content" source="media/3976435-notification-greater-than-24-hours.png" alt-text="Doba restartu je víc než 24 hodin.":::

  - Pokud je restartování kratší než 24 hodin, zobrazí se indikátor průběhu. Časování tohoto oznámení je založené na nastavení: **Zadejte dobu, po jejímž uplynutí se zařízení restartuje (minuty)**.

    :::image type="content" source="media/3976435-notification-less-than-24-hours.png" alt-text="Čas restartování je pryč méně než 24 hodin.":::

Pokud uživatel vybere **připomenout**znovu, další dočasné oznámení se zobrazí po uplynutí doby odložení. Toto chování předpokládá, že ještě nedosáhla konečného odpočítávání. Časování dalšího oznámení je založené na nastavení: **Určete četnost oznámení připomenutí prezentovaných uživateli, po uplynutí konečného termínu, než se zařízení restartuje (minuty)**. Pokud uživatel vybere **připomenout**znovu a váš interval odložení bude jedna hodina, Centrum softwaru ho znovu upozorní uživatele za 60 minut. Toto chování předpokládá, že ještě nedosáhla konečného odpočítávání.

Po dosažení konečného odpočítávání v centru softwaru se uživateli zobrazí oznámení, že se nemůžou zavřít. Indikátor průběhu je červený a uživatel ho nemůže **připomenout** odložit.

:::image type="content" source="media/3976435-1906-final-restart-countdown.png" alt-text="Konečné odpočítávání oznámení centra softwaru ve verzi 1906":::

### <a name="proactively-install-required-software-before-the-deadline"></a>Proaktivní instalace požadovaného softwaru před konečným termínem

Pokud uživatel proaktivně nainstaluje požadovaný software, který potřebuje restartovat před konečným termínem, uvidí jiné oznámení. Další informace o konfiguraci těchto nastavení najdete v tématu [nasazení nastavení **uživatelského prostředí** ](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux) a [oznámení uživatelů pro požadovaná nasazení](../../../apps/deploy-use/deploy-applications.md#bkmk_notify).

K následujícímu oznámení dojde, pokud nastavení činnost koncového uživatele umožňuje oznámení a nepoužíváte pro nasazení oznámení informační zprávy:

:::image type="content" source="media/3976435-proactive-user-restart-notification.png" alt-text="Oznámení o proaktivním nainstalovaném softwaru":::

Jakmile nasazení dosáhne svého konečného termínu, Centrum softwaru bude postupovat podle pokynů k [instalaci požadovaného softwaru do nebo po termínu](#install-required-software-at-or-after-the-deadline).

## <a name="example-configurations"></a>Příklady konfigurací

Následující příklady popisují, jak nakonfigurovat nastavení klienta, aby bylo dosaženo konkrétního chování.

### <a name="reminders-are-off"></a>Připomenutí jsou vypnutá.

| Nastavení | Hodnota |
|---------|---------|
|Zadejte čas po uplynutí konečného termínu, než se zařízení restartuje (minuty).|180|
|Zadejte dobu, po kterou se uživateli zobrazí konečné oznámení o odpočítávání, než se zařízení restartuje (minuty).|60|
|Zadejte frekvenci oznámení připomenutí, která se uživateli zobrazí po uplynutí konečného termínu, než se zařízení restartuje (minuty).|240|
|Pokud nasazení vyžaduje restart, zobrazí se uživateli dialogové okno namísto informačního oznámení.|Ne|

Zařízení se po uplynutí konečného termínu nasazení restartuje tři hodiny (**180** minut). Po jedné hodině (**60** minut) před restartováním se uživateli zobrazí odpočítávání, že se nemůže zavřít ani znovu připomenout. První oznámení o připomenutí je nastavené na začátek čtyř hodin (**240** minut) po uplynutí konečného termínu, který následuje po restartování. Takže se uživateli nezobrazí žádná připomenutí.

### <a name="low-reminder-frequency"></a>Frekvence nízkého připomenutí

| Nastavení | Hodnota |
|---------|---------|
|Zadejte čas po uplynutí konečného termínu, než se zařízení restartuje (minuty).|7200|
|Zadejte dobu, po kterou se uživateli zobrazí konečné oznámení o odpočítávání, než se zařízení restartuje (minuty).|120|
|Zadejte frekvenci oznámení připomenutí, která se uživateli zobrazí po uplynutí konečného termínu, než se zařízení restartuje (minuty).|900|
|Pokud nasazení vyžaduje restart, zobrazí se uživateli dialogové okno namísto informačního oznámení.|Ano|

Zařízení se restartuje 5 dní (**7200** minut) po uplynutí konečného termínu nasazení. Dvě hodiny (**120** minut) před tím, než se restartuje, uživatel uvidí odpočítávání, že se nemůžou zavřít ani znovu připomenout. Tato konfigurace umožňuje zobrazit připomenutí () 118 hodin ( `(7200 - 120) / 60` ). 15 hodin (**900** minut) po uplynutí konečného termínu zobrazí Centrum softwaru první připomenutí. Zobrazuje maximálně šest dalších připomenutí každých 15 hodin (**900 minut**). Uživatel uvidí připomenutí jako okno na obrazovce, místo upozornění, které se během několika sekund zmizí.

### <a name="high-reminder-frequency"></a>Frekvence vysokého připomenutí

| Nastavení | Hodnota |
|---------|---------|
|Zadejte čas po uplynutí konečného termínu, než se zařízení restartuje (minuty).|2880|
|Zadejte dobu, po kterou se uživateli zobrazí konečné oznámení o odpočítávání, než se zařízení restartuje (minuty).|60|
|Zadejte frekvenci oznámení připomenutí, která se uživateli zobrazí po uplynutí konečného termínu, než se zařízení restartuje (minuty).|30|
|Pokud nasazení vyžaduje restart, zobrazí se uživateli dialogové okno namísto informačního oznámení.|Ano|

Zařízení se restartuje dva dny (**2880** minut) po uplynutí konečného termínu nasazení. Po jedné hodině (**60** minut) před restartováním se uživateli zobrazí odpočítávání, že se nemůže zavřít ani znovu připomenout. Tato konfigurace umožňuje zobrazit připomenutí () 47 hodin ( `(2880 - 60) / 60` ). **30** minut po uplynutí konečného termínu zobrazí Centrum softwaru první připomenutí. Zobrazuje se maximálně 92 dalších připomenutí každých **30 minut**. Uživatel uvidí připomenutí jako okno na obrazovce, místo upozornění, které se během několika sekund zmizí.

## <a name="device-restart-notifications-version-1902"></a>Oznámení o restartování zařízení (verze 1902)

<!--3555947-->
Někdy se uživatelům nezobrazuje zpráva informující o systému Windows o restartování nebo požadovaném nasazení. Pak nevidí prostředí, které připomíná připomenutí k odložení. Toto chování může vést k nedostatečnému uživatelskému prostředí, když klient dosáhne konečného termínu.

Od verze 1902 platí, že když se vyžadují změny softwaru, nebo nasazení potřebují restartovat, máte možnost použít více rušivých dialogových oken.

V okně [restartovat počítač](#client-settings) v nastavení klienta Povolte následující možnost: **Pokud nasazení vyžaduje restart, místo oznámení informačního systému se zobrazí dialogové okno s uživatelem**.  

Konfigurace tohoto nastavení klienta změní činnost koncového uživatele pro všechna požadovaná nasazení, která vyžadují restart ze zpráv oznámení:

:::image type="content" source="media/3555947-restart-toast-initial.png" alt-text="Informační zpráva oznamující, že je vyžadováno restartování":::

Do dialogového okna více rušivého centra softwaru:

:::image type="content" source="media/3976435-proactive-user-restart-notification.png" alt-text="Dialogové okno pro restartování počítače":::

Pokud uživatel po instalaci nerestartoval své zařízení, obdrží oznámení jako připomenutí. Toto dočasné připomenutí se uživateli zobrazí na základě nastavení klienta: **Zobrazit dočasné oznámení uživateli, které udává interval před odhlášením uživatele nebo restartováním počítače (minuty)**. Toto nastavení je celkový čas, po který musí uživatel restartovat počítač, než bude vynucen restart.

- Dočasné oznámení při použití oznámení informačních zpráv:

    :::image type="content" source="media/3555947-restart-toast.png" alt-text="Informační zpráva o čekání na restartování":::

- Dočasné oznámení při použití dialogového okna Centrum softwaru, nikoli informační zprávy:

    :::image type="content" source="media/3555947-1902-hide-notification.png" alt-text="Čeká na restartování oznámení centra softwaru s tlačítkem pro odložení":::

Pokud se uživatel po dočasném oznámení nerestartuje, bude mu přiděleno konečné oznámení o odpočítávání, které nepůjde zavřít. Čas, kdy se zobrazí konečné oznámení, je založen na nastavení klienta: **zobrazí dialogové okno, které uživatel nemůže zavřít, který zobrazí interval odpočítávání před odhlášením uživatele nebo restartování počítače (minuty)**. Pokud je například nastavení 60, pak hodina před restartováním, zobrazí se konečné oznámení uživateli:

:::image type="content" source="media/3555947-1902-final-countdown.png" alt-text="Oznámení o konečném odpočítávání centra softwaru":::

Následující nastavení musí být kratší než v době trvání, než má nejkratší [okno údržby](../manage/collections/use-maintenance-windows.md) , které se pro počítač použije:

- **Zobrazit dočasné oznámení uživateli, které udává interval před odhlášením uživatele nebo restartováním počítače (minuty)**
- **Zobrazí dialogové okno, které uživatel nemůže zavřít, který zobrazuje interval odpočítávání před odhlášením uživatele nebo restartování počítače (minuty).**

> [!IMPORTANT]
> V Configuration Manager 1902 se za určitých okolností dialogová okna nebudou nahrazena informačními oznámeními. Pokud chcete tento problém vyřešit, nainstalujte [kumulativní aktualizaci pro Configuration Manager verze 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="log-files"></a>Soubory protokolu

Pokud chcete řešit potíže s restartováním zařízení, použijte soubory **RebootCoordinator. log** a **SCNotify. log** v klientovi. Na základě konkrétního typu nasazení budete možná muset použít i další [soubory protokolů](../../plan-design/hierarchy/log-files.md)klienta.

## <a name="next-steps"></a>Další kroky

- [Postup konfigurace nastavení klienta](configure-client-settings.md)
- [Nastavení **uživatelského prostředí** nasazení aplikace](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)
- [Oznámení uživatelů pro požadovaná nasazení aplikací](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)
