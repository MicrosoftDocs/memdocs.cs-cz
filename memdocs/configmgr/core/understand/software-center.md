---
title: Uživatelská příručka Centra softwaru
titleSuffix: Configuration Manager
description: Seznamte se s funkcemi a funkcemi centra softwaru
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/12/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: c4fa0819bf6427d93adf44a7b6284a8266e3a6a5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722659"
---
# <a name="software-center-user-guide"></a>Uživatelská příručka Centra softwaru

*Platí pro: Configuration Manager (Current Branch)*

Správce IT ve vaší organizaci používá Centrum softwaru k instalaci aplikací, aktualizací softwaru a upgradování oken. Tato uživatelská příručka vysvětluje funkčnost centra softwaru pro uživatele počítače.

Obecné poznámky k funkcím centra softwaru:

- Tento článek popisuje nejnovější funkce centra softwaru. Pokud vaše organizace používá starší, ale stále podporovanou verzi centra softwaru, nejsou k dispozici všechny funkce. Pokud chcete získat další informace, obraťte se na správce IT.

- Správce IT může zakázat některé aspekty centra softwaru. Vaše konkrétní prostředí se může lišit.

- Pokud má zařízení současně více uživatelů, například prostřednictvím několika relací vzdálené plochy, bude uživatel s nejnižším ID relace jediným z nich, aby zobrazil všechna dostupná nasazení v centru softwaru. Uživatelé s vyššími identifikátory relací nemusí v centru softwaru vidět některá nasazení. Například uživatelé s vyššími identifikátory relací můžou vidět nasazené aplikace, ale ne nasazené balíčky nebo sekvence úloh. Mezitím se uživateli s nejnižším ID relace zobrazí všechny nasazené aplikace, balíčky a sekvence úloh.

<!-- - Your IT admin may change the color of Software Center, and add your organization's logo. The images in this article show the default experience. -->

## <a name="how-to-open-software-center"></a><a name="bkmk_open"></a>Postup otevření centra softwaru

Nejjednodušší způsob, jak spustit Centrum softwaru na počítači s Windows 10, získáte stisknutím klávesy **Start** a `Software Center`zadáním. Možná nebudete muset zadávat celý řetězec pro Windows, abyste našli nejlepší shodu.

Pokud přejdete do nabídky Start, podívejte se do části skupina **Microsoft Endpoint Manager** pro ikonu **centra softwaru** .

![Ikony nabídky Start pro Microsoft Endpoint Manager](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> Cesta v nabídce Start se změnila ve verzi 1910. Ve verzi 1906 a starší se jedná o název složky **Microsoft System Center**. Když aktualizujete Configuration Manager na verzi 1910 nebo novější, nezapomeňte aktualizovat jakoukoli interní dokumentaci, kterou udržujete, aby zahrnovala toto nové umístění.

## <a name="applications"></a>Aplikace

Vyberte kartu **aplikace** a vyhledejte a nainstalujte aplikace, které vám správce IT nasadí nebo tento počítač.

- **All**: zobrazí všechny aplikace, které lze nainstalovat.
- **Požadováno**: váš správce IT tyto aplikace vynutil. Pokud odinstalujete některou z těchto aplikací, Centrum softwaru je znovu nainstaluje.
- **Filtry**: správce IT může vytvářet kategorie aplikací. Pokud je k dispozici, vyberte rozevírací seznam pro filtrování zobrazení pouze pro aplikace v určité kategorii. Výběrem možnost **vše** zobrazíte všechny aplikace.
- **Seřadit podle**: přeuspořádat seznam aplikací. Ve výchozím nastavení se tento seznam seřadí podle **nejnovějších**. Nedávno dostupné aplikace jsou uvedené s **novou** značkou, která je viditelná po dobu 7 dnů.
- **Hledání**: stále nemůžete najít, co hledáte? Do vyhledávacího pole zadejte klíčová slova, abyste mohli najít!
- **Přepněte zobrazení**: Vyberte ikony a přepněte zobrazení mezi zobrazením seznamu a zobrazením dlaždic. Ve výchozím nastavení se seznam aplikace zobrazuje jako grafické dlaždice.
    - Dlaždice – zobrazení: správce IT může ikony přizpůsobit. Pod každou dlaždicí se zobrazí název aplikace, Vydavatel a verze.
    - Zobrazení seznamu: v tomto zobrazení se zobrazuje ikona aplikace, název, vydavatel, verze a stav.

### <a name="install-multiple-applications"></a>Instalace více aplikací

<!-- 1357126 -->
Nainstalujte více než jednu aplikaci současně, místo abyste čekali na dokončení před spuštěním dalšího. Ne všechny aplikace jsou kvalifikovány:

- Aplikace je viditelná pro vás.
- Aplikace se už nestahuje nebo není nainstalovaná.
- Správce IT nevyžaduje schválení k instalaci aplikace.

Postup instalace více než jedné aplikace v jednom okamžiku:

1. Pokud chcete v zobrazení seznamu zadat režim vícenásobného výběru, vyberte ikonu vícenásobný výběr. ![Ikona vícenásobného výběru centra softwaru](media/software-center-multi-select-apps.png) v pravém horním rohu.
2. Vyberte dvě nebo víc aplikací, které chcete nainstalovat, a to tak, že vyberete zaškrtávací políčko nalevo od aplikací v seznamu.
3. Vyberte tlačítko **nainstalovat vybrané** .

Aplikace se instalují jako normální, jenom teď po úspěchu.


## <a name="updates"></a>Aktualizace

Kliknutím na kartu **aktualizace** zobrazíte a nainstalujete aktualizace softwaru, které správce IT nasadí do tohoto počítače.  

- **All**: zobrazí všechny aktualizace, které můžete nainstalovat.
- **Požadováno**: váš správce IT tyto aktualizace vynutil.
- **Seřadit podle**: přeuspořádat seznam aktualizací. Ve výchozím nastavení se tento seznam seřadí podle **názvu aplikace: a až Z**.

Chcete-li nainstalovat aktualizace, vyberte možnost **instalovat vše**.

Chcete-li nainstalovat pouze konkrétní aktualizace, vyberte ikonu pro přechod do režimu vícenásobného výběru. Zkontrolujte aktualizace, které chcete nainstalovat, a pak vyberte **nainstalovat vybrané**.


## <a name="operating-systems"></a>Operační systémy

Vyberte kartu **operační systémy** a zobrazte a nainstalujte verze Windows, které správce IT nasadí do tohoto počítače.  

- **All**: zobrazí všechny verze systému Windows, které lze nainstalovat.
- **Požadováno**: váš správce IT tyto upgrady vynutil.
- **Seřadit podle**: přeuspořádat seznam aktualizací. Ve výchozím nastavení se tento seznam seřadí podle **názvu aplikace: a až Z**.


## <a name="installation-status"></a>Stav instalace

Kliknutím na kartu **stav instalace** zobrazíte stav aplikací. Můžou se zobrazit tyto stavy:

- **Nainstalováno**: Centrum softwaru již nainstalovalo tuto aplikaci na tento počítač.
- **Stahování**: Centrum softwaru stahuje software, který se má nainstalovat na tento počítač.
- **Nepovedlo se**: při pokusu o instalaci softwaru došlo v centru softwaru k chybě.
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

- Výběrem rozevíracích seznamů vyberte nejstarší a poslední hodiny, které použijete pro tento počítač. Ve výchozím nastavení jsou tyto hodnoty od **5** do **10 odp** .

- Zaškrtněte políčko vedle dny v týdnu, kdy tento počítač obvykle používáte. Centrum softwaru vybere ve výchozím nastavení dny v týdnu.  

Určete, zda tento počítač pravidelně používáte k práci. Správce může automaticky instalovat aplikace nebo zpřístupnit další aplikace pro primární počítače. <!--3485366-->

- Vyberte možnost **pravidelně používat tento počítač k práci,** Pokud je počítač, který používáte, primární počítač.

### <a name="power-management"></a>Řízení spotřeby

Správce IT může nastavit zásady řízení spotřeby. Tyto zásady pomůžou vaší organizaci šetřit elektřinu v případě, že se tento počítač nepoužívá.

Pokud chcete tomuto počítači vyloučit z těchto zásad, zaškrtněte políčko **Nepoužívat nastavení napájení z oddělení IT na tento počítač**. Toto nastavení je ve výchozím nastavení zakázáno. počítač použije nastavení napájení.

### <a name="computer-maintenance"></a>Údržba počítače

Určete, jak má centrum softwaru použít změny softwaru před konečným termínem.

- **Automaticky nainstalovat nebo odinstalovat požadovaný software a restartovat počítač pouze mimo zadanou pracovní dobu**: Toto nastavení je ve výchozím nastavení zakázáno.
- **Pozastavit aktivity centra softwaru, pokud je počítač v prezentačním režimu**: Toto nastavení je ve výchozím nastavení povoleno.
- **Zásady synchronizace**: Toto tlačítko vyberte, když ho správce IT vydá. Tento počítač kontroluje se servery pro jakékoli nové, třeba aplikace, aktualizace softwaru nebo operační systémy.

### <a name="remote-control"></a>Vzdálené řízení

Zadat nastavení vzdáleného přístupu a vzdáleného řízení pro váš počítač

- **Použití nastavení vzdáleného přístupu z vašeho oddělení IT**: Toto políčko je ve výchozím nastavení zaškrtnuté.
- **Povolená úroveň vzdáleného přístupu**: Vyberte si z následujících 3 možností.
    - **Nepovolit vzdálený přístup**
    - **Jenom zobrazení**
    - **Full**: Tato úroveň je ve výchozím nastavení povolená.
- **Povolí vzdálené řízení tohoto počítače správci, když jsem pryč**. Toto nastavení je ve výchozím nastavení nastaveno na **Ano** .
- **Když se správce pokusí o vzdálené řízení tohoto počítače**: Toto nastavení má dvě možnosti.
    - **Požádat o oprávnění pokaždé**: Tato možnost je ve výchozím nastavení vybraná.
    - **Nežádat o oprávnění**
- **Během vzdáleného řízení zobrazit následující**: obě možnosti jsou ve výchozím nastavení vybrané.
    - **Ikona stavu v oznamovací oblasti**
    - **Panel připojení relace na ploše**
- **Přehrát zvuk**: Toto nastavení má tři možnosti
    - **Při zahájení a ukončení relace**: Toto nastavení je standardně vybrané.
    - **Opakovaně během relace**
    - **Nikdy**

    Další informace najdete v tématu [Úvod do vzdáleného řízení](../clients/manage/remote-control/introduction-to-remote-control.md) .
    

## <a name="custom-tab-in-software-center"></a>Vlastní karta v centru softwaru

Správce IT může přidat další kartu do centra softwaru. Tato karta je pojmenována vaším správcem a vede na web, který určí. Například máte kartu s názvem "helpdesk", která vede na web helpdesku vaší organizace. <!--1358132-->
