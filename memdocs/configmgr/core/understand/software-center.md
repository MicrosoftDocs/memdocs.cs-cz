---
title: Uživatelská příručka Centra softwaru
titleSuffix: Configuration Manager
description: Seznamte se s funkcemi a funkcemi centra softwaru
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: end-user-help
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: 19b1b56c394fbf71e9117ad12fbe900e6f07e5fb
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715412"
---
# <a name="software-center-user-guide"></a>Uživatelská příručka Centra softwaru

*Platí pro: Configuration Manager (Current Branch)*

Správce IT ve vaší organizaci používá Centrum softwaru k instalaci aplikací, aktualizací softwaru a upgradování oken. Tato uživatelská příručka vysvětluje funkčnost centra softwaru pro uživatele počítače.

Centrum softwaru se automaticky nainstaluje na zařízení s Windows, která spravuje vaše IT organizace. Chcete-li začít, přečtěte si téma [Postup otevření centra softwaru](#bkmk_open).

Obecné poznámky k funkcím centra softwaru:

- Tento článek popisuje nejnovější funkce centra softwaru. Pokud vaše organizace používá starší, ale stále podporovanou verzi centra softwaru, nejsou k dispozici všechny funkce. Pokud chcete získat další informace, obraťte se na správce IT.

- Správce IT může zakázat některé aspekty centra softwaru. Vaše konkrétní prostředí se může lišit.

- Pokud zařízení používá více uživatelů najednou, bude jediným uživatelem s nejnižším ID relace pouze ten, který zobrazí všechna dostupná nasazení v centru softwaru. Například více uživatelů v prostředí vzdálené plochy. Uživatelé s vyššími identifikátory relací nemusí v centru softwaru vidět některá nasazení. Například uživatelé s vyššími identifikátory relací můžou vidět nasazené aplikace, ale ne nasazené balíčky nebo sekvence úloh. Mezitím se uživateli s nejnižším ID relace zobrazí všechny nasazené aplikace, balíčky a sekvence úloh. Karta **Uživatelé** ve Správci úloh systému Windows zobrazuje všechny uživatele a jejich ID relací.

- Správce IT může změnit barvu centra softwaru a přidat logo vaší organizace.

## <a name="how-to-open-software-center"></a><a name="bkmk_open"></a>Postup otevření centra softwaru

Centrum softwaru se automaticky nainstaluje na zařízení s Windows, která spravuje vaše IT organizace. Nejjednodušší způsob, jak spustit Centrum softwaru na počítači s Windows 10, získáte stisknutím klávesy **Start** a zadáním `Software Center` . Možná nebudete muset zadávat celý řetězec pro Windows, abyste našli nejlepší shodu.

:::image type="content" source="media/start-menu-software-center.png" alt-text="Nejlepší shoda v centru softwaru v nabídce Start":::

Pokud chcete přejít do nabídky Start, podívejte se do skupiny **Microsoft Endpoint Manager** pro ikonu **centra softwaru** .

:::image type="content" source="media/microsoft-endpoint-manager-start-menu.png" alt-text="Ikony nabídky Start pro Microsoft Endpoint Manager":::

> [!NOTE]
> Výše uvedená cesta v nabídce Start je určena pro verze od listopadu 2019 (verze 1910) nebo novější. V dřívějších verzích je název složky **Microsoft System Center**.

Pokud v nabídce Start nemůžete najít Centrum softwaru, obraťte se na správce IT.

## <a name="applications"></a>Aplikace

:::image type="content" source="media/software-center-apps.png" alt-text="Karta aplikace centra softwaru" lightbox="media/software-center-apps.png":::

Vyberte kartu **aplikace** (1), chcete-li vyhledat a nainstalovat aplikace, které vám správce IT nasadí nebo tento počítač.

- **All** (2): zobrazí všechny dostupné aplikace, které můžete nainstalovat.

- **Požadováno** (3): správce IT tyto aplikace vynutil. Pokud odinstalujete některou z těchto aplikací, Centrum softwaru je znovu nainstaluje.

- **Filtry** (4): správce IT může vytvářet kategorie aplikací. Pokud je k dispozici, vyberte rozevírací seznam pro filtrování zobrazení pouze pro aplikace v určité kategorii. Výběrem možnost **vše** zobrazíte všechny aplikace.

- **Seřadit podle** (5): přeuspořádat seznam aplikací. Ve výchozím nastavení se tento seznam seřadí podle **nejnovějších**. Nedávno dostupné aplikace se zobrazují s **novým** bannerem, který je viditelný po dobu sedmi dní.

- **Hledání** (6): stále nemůžete najít, co hledáte? Do vyhledávacího pole zadejte klíčová slova, abyste mohli najít!

- Přepnout zobrazení (7): Vyberte ikony pro přepínání mezi zobrazením seznamu a zobrazením dlaždic. Ve výchozím nastavení se seznam aplikace zobrazuje jako grafické dlaždice.

|Ikona|Zobrazení|Description|
|----|----|-----------|
|:::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::|**Režim vícenásobného výběru**|Nainstalujte více než jednu aplikaci současně. Další informace najdete v tématu [Instalace více aplikací](#install-multiple-applications).|
|:::image type="icon" source="media/software-center-apps-list-view.png" border="false":::|**zobrazení seznamu**|V tomto zobrazení se zobrazuje ikona aplikace, název, vydavatel, verze a stav.|
|:::image type="icon" source="media/software-center-apps-tile-view.png" border="false":::|**Zobrazení dlaždic**|Správce IT může ikony přizpůsobit. Pod každou dlaždicí se zobrazí název aplikace, Vydavatel a verze.|

### <a name="install-an-application"></a>Instalace aplikace

Výběrem aplikace v seznamu zobrazíte další informace. Vyberte **nainstalovat** a nainstalujte ji. Pokud je aplikace už nainstalovaná, můžete mít možnost ji **odinstalovat**.

Některé aplikace můžou před instalací vyžadovat schválení.

- Při pokusu o instalaci můžete zadat komentář a potom **požádat o** aplikaci.

  :::image type="content" source="media/software-center-app-approval-request.png" alt-text="Požadavek na instalaci aplikace centra softwaru ke schválení":::

- Centrum softwaru zobrazí historii požadavků a žádost můžete zrušit.

  :::image type="content" source="media/software-center-app-approval-status.png" alt-text="Požaduje se instalace aplikace Centrum softwaru":::

- Když správce vaši žádost schválí, můžete aplikaci nainstalovat. Pokud budete čekat, Centrum softwaru aplikaci automaticky nainstaluje v nepracovní době.

  :::image type="content" source="media/software-center-app-approved.png" alt-text="Schválená instalace aplikace centra softwaru":::

### <a name="install-multiple-applications"></a>Instalace více aplikací

<!-- 1357126 -->
Nainstalujte více než jednu aplikaci současně, místo abyste čekali na dokončení před spuštěním dalšího. Vybrané aplikace musí kvalifikovat:

- Aplikace je viditelná pro vás.
- Aplikace se už nestahuje nebo není nainstalovaná.
- Správce IT nevyžaduje schválení k instalaci aplikace.

Postup instalace více než jedné aplikace v jednom okamžiku:

1. V pravém horním rohu vyberte ikonu vícenásobný výběr::::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::

2. Vyberte dvě nebo víc aplikací, které chcete nainstalovat. Zaškrtněte políčko nalevo od každé aplikace v seznamu.

3. Vyberte tlačítko **Instalovat vybrané** , které chcete spustit.

Aplikace se instalují jako normální, jenom teď po úspěchu.

### <a name="share-an-application"></a>Sdílení aplikace

Pokud chcete sdílet odkaz na konkrétní aplikaci, vyberte po výběru aplikace ikonu **sdílet** v pravém horním rohu::::image type="icon" source="media/software-center-share-app-icon.png" border="false":::

:::image type="content" source="media/software-center-share-app-window.png" alt-text="Sdílení aplikace z centra softwaru":::

**Zkopírujte** řetězec a vložte ho jinde, jako je například e-mailová zpráva. Například, `softwarecenter:SoftwareID=ScopeId_73F3BB5E-5EDC-4928-87BD-4E75EB4BBC34/Application_b9e438aa-f5b5-432c-9b4f-6ebeeb132a5a`. Kdokoli jiný ve vaší organizaci pomocí centra softwaru může pomocí odkazu otevřít stejnou aplikaci.

## <a name="updates"></a>Aktualizace

:::image type="content" source="media/software-center-updates.png" alt-text="Karta aktualizace centra softwaru" lightbox="media/software-center-updates.png":::

Kliknutím na kartu **aktualizace** (1) zobrazíte a nainstalujete aktualizace softwaru, které správce IT nasadí do tohoto počítače.  

- **All** (2): zobrazí všechny aktualizace, které můžete nainstalovat.

- **Požadováno** (3): správce IT tyto aktualizace vynutil.

- **Seřadit podle** (4): přeuspořádat seznam aktualizací. Ve výchozím nastavení se tento seznam seřadí podle **názvu aplikace: a až Z**.

- **Hledání** (5): stále nemůžete najít, co hledáte? Do vyhledávacího pole zadejte klíčová slova, abyste mohli najít!

Pokud chcete nainstalovat aktualizace, vyberte **nainstalovat vše** (6).

Chcete-li nainstalovat pouze konkrétní aktualizace, vyberte ikonu pro přechod do režimu vícenásobného výběru (7)::::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::
Zkontrolujte aktualizace, které chcete nainstalovat, a pak vyberte **nainstalovat vybrané**.

## <a name="operating-systems"></a>Operační systémy

:::image type="content" source="media/software-center-os.png" alt-text="Karta operační systémy centra softwaru" lightbox="media/software-center-os.png":::

Vyberte kartu **operační systémy** (1), chcete-li zobrazit a nainstalovat verze systému Windows, které správce IT nasadí do tohoto počítače.  

- **All** (2): zobrazí všechny verze systému Windows, které můžete nainstalovat.

- **Požadováno** (3): správce IT tyto upgrady vynutil.

- **Seřadit podle** (4): přeuspořádat seznam aktualizací. Ve výchozím nastavení se tento seznam seřadí podle **názvu aplikace: a až Z**.

- **Hledání** (5): stále nemůžete najít, co hledáte? Do vyhledávacího pole zadejte klíčová slova, abyste mohli najít!

## <a name="installation-status"></a>Stav instalace

Kliknutím na kartu **stav instalace** zobrazíte stav aplikací. Můžou se zobrazit tyto stavy:

- **Nainstalováno**: Centrum softwaru již nainstalovalo tuto aplikaci na tento počítač.

- **Stahování**: Centrum softwaru stahuje software, který se má nainstalovat na tento počítač.

- **Nepovedlo se**: Software Center nemohl nainstalovat software.

- **Naplánovaná instalace po**: zobrazuje datum a čas příštího časového období údržby zařízení k instalaci připravovaného softwaru. Okna údržby definuje správce IT.<!--1358131-->

  - Stav lze zobrazit na kartě **vše** a **nadcházející** .

  - Kliknutím na tlačítko **nainstalovat nyní** můžete nainstalovat ještě před časem časového období údržby.

## <a name="device-compliance"></a>Dodržování předpisů zařízení

Pokud chcete zobrazit stav dodržování předpisů tohoto počítače, vyberte kartu **dodržování předpisů zařízením** .

Vyberte možnost **ověřit dodržování předpisů** , pokud chcete vyhodnotit nastavení tohoto zařízení proti zásadám zabezpečení definovaným vaším správcem IT.

## <a name="options"></a>Možnosti

Vyberte kartu **Možnosti** a zobrazte další nastavení pro tento počítač.

### <a name="work-information"></a>Pracovní informace

Určete hodiny, které obvykle pracujete. Správce IT může naplánovat instalace softwaru mimo pracovní dobu. Pro úlohy údržby systému nechte každý den alespoň čtyři hodiny. Správce IT může během pracovní doby instalovat i kritické aplikace a aktualizace softwaru.

- Vyberte nejstarší a poslední hodiny, které použijete pro tento počítač. Ve výchozím nastavení jsou tyto hodnoty od **5:00** do **10:00 odp**.

- Vyberte dny v týdnu, kdy tento počítač obvykle používáte. Ve výchozím nastavení Centrum softwaru vybere pouze pracovní dny.

Určete, zda tento počítač pravidelně používáte k práci. Správce může automaticky instalovat aplikace nebo zpřístupnit další aplikace pro primární počítače.<!--3485366--> Pokud je počítač, který používáte, primární počítač, vyberte možnost **pravidelně používat tento počítač k práci**.

### <a name="power-management"></a>Řízení spotřeby

Správce IT může nastavit zásady řízení spotřeby. Tyto zásady pomůžou vaší organizaci šetřit elektřinu v případě, že se tento počítač nepoužívá.

Chcete-li tomuto počítači vyloučit z těchto zásad, vyberte možnost **Nepoužívat nastavení napájení ze svého IT oddělení na tento počítač**. Ve výchozím nastavení je toto nastavení zakázáno a počítač použije nastavení napájení.

### <a name="computer-maintenance"></a>Údržba počítače

Určete, jak má centrum softwaru použít změny softwaru před konečným termínem.

- **Automaticky nainstalovat nebo odinstalovat požadovaný software a restartovat počítač pouze mimo zadanou pracovní dobu**: Toto nastavení je ve výchozím nastavení zakázáno.

- **Pozastavit aktivity centra softwaru, pokud je počítač v prezentačním režimu**: Toto nastavení je ve výchozím nastavení povoleno.

Po pokyn správce IT vyberte možnost **zásady synchronizace**. Tento počítač kontroluje se servery pro jakékoli nové, třeba aplikace, aktualizace softwaru nebo operační systémy.

### <a name="remote-control"></a>Vzdálené řízení

Zadejte nastavení vzdáleného přístupu a vzdáleného řízení pro váš počítač.

**Použití nastavení vzdáleného přístupu z vašeho oddělení IT**: ve výchozím nastavení definuje vaše IT oddělení nastavení, které vám může pomoct vzdáleně. Další nastavení v této části zobrazují stav nastavení, které definuje vaše IT oddělení. Pokud chcete změnit nastavení, nejdřív tuto možnost vypněte.

- **Povolená úroveň vzdáleného přístupu**
  - **Nepovolit vzdálený přístup**: Správci IT nemůžou vzdáleně získat přístup k tomuto počítači, aby vám pomohl.
  - **Jenom zobrazit**: správce IT může vaši obrazovku vzdáleně zobrazit jenom vy.
  - **Úplné**: správce IT může vzdáleně řídit tento počítač. Toto nastavení je výchozí možností.

- **Povolí vzdálené řízení tohoto počítače správci, když jsem pryč**. Toto nastavení je ve výchozím nastavení nastaveno na **Ano** .

- **Když se správce pokusí o vzdálené řízení tohoto počítače**
  - **Požádat o oprávnění pokaždé**: Toto nastavení je výchozí možnost.
  - **Nežádat o oprávnění**

- **Během vzdáleného řízení zobrazit následující**: Tato vizuální oznámení jsou ve výchozím nastavení povolená, aby vám věděla, že správce vzdáleně přistupuje k zařízení.
  - **Ikona stavu v oznamovací oblasti**
  - **Panel připojení relace na ploše**

- **Přehrát zvuk**: Toto zvukové oznámení vám umožní zjistit, že správce vzdáleně přistupuje k zařízení.
  - **Při zahájení a ukončení relace**: Toto nastavení je výchozí možnost.
  - **Opakovaně během relace**
  - **Nikdy**

## <a name="custom-tabs"></a>Vlastní karty

Správce IT může odebrat výchozí karty nebo přidat další karty do centra softwaru. Vlastní karty jsou pojmenovány vaším správcem a otevřou web, který určuje správce. Například můžete mít kartu s názvem "helpdesk", která otevře web helpdesku vaší organizace. <!--1358132-->

## <a name="more-information-for-it-administrators"></a>Další informace pro správce IT

Pro správce IT jsou k dispozici další informace o tom, jak naplánovat a nakonfigurovat Centrum softwaru v následujících článcích:

- [Plánování Centra softwaru](../../apps/plan-design/plan-for-software-center.md)
- [Nastavení klienta centra softwaru](../clients/deploy/about-client-settings.md#software-center)
- [Oznámení o restartování zařízení](../clients/deploy/device-restart-notifications.md)
- [Úvod do vzdáleného řízení](../clients/manage/remote-control/introduction-to-remote-control.md)
