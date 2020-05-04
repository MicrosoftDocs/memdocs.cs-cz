---
title: Úvod do správy aplikací
titleSuffix: Configuration Manager
description: Seznamte se se základními informacemi, které budete potřebovat ke správě a nasazování aplikací v Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d3cd21fe4b1d53ecbb0bc60818405cb795a4f289
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710759"
---
# <a name="introduction-to-application-management-in-configuration-manager"></a>Seznámení se správou aplikací v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

V tomto článku se naučíte základy, než začnete pracovat s Configuration Manager aplikacemi.  

> [!TIP]  
> Pokud jste již obeznámeni s tím, jak spravovat aplikace v Configuration Manager, přeskočte tento článek. Přejděte na vytvoření ukázkové aplikace: [Vytvoření a nasazení aplikace](../get-started/create-and-deploy-an-application.md).  

## <a name="what-is-an-application"></a>Co je aplikace?

I když je *aplikace* *nebo aplikace široce* využívaným termínem Computing, v Configuration Manager znamená něco konkrétního. Představte si aplikaci jako krabici. Toto pole obsahuje jednu nebo více sad instalačních souborů pro softwarový balíček (označované jako *typ nasazení*) a navíc pokyny k nasazení tohoto softwaru.  

Když nasadíte aplikaci do zařízení, **požadavky** rozhodují, který typ nasazení Configuration Manager na zařízení nainstalovat.  

Pomocí aplikace můžete provádět spoustu dalších věcí. O těchto akcích se dozvíte při čtení této příručky. V následujících částech najdete několik konceptů, které budete potřebovat před zahájením dig hlubší:  

### <a name="deployment-type"></a>Typ nasazení

Pokud je *aplikace* pole, pak je *typ nasazení* sada obsahu v poli. Aplikace potřebuje aspoň jeden typ nasazení, protože určuje, jak se má aplikace nainstalovat. Pro konfiguraci jiného obsahu a instalačního programu pro stejnou aplikaci použijte více než jeden typ nasazení.

Vaše společnost má například obchodní aplikaci s názvem Astoria. Vývojáři aplikací poskytují tyto možnosti instalace aplikace:

- Balíček Instalační služba systému Windows pro plnou funkčnost na zařízeních s Windows 10
- Balíček sady App-V pro použití ve farmě serverů Terminálové služby
- Webová aplikace pro mobilní uživatele  

V Configuration Manager vytvoříte jednu aplikaci pro Astoria. Aplikace definuje metadata na nejvyšší úrovni o aplikaci, která je společná pro všechny metody instalace a platformy. Pak vytvoříte tři typy nasazení pro dostupné metody instalace a nasadíte aplikaci pro všechny uživatele. Na základě požadavků a dalších konfigurací na typech nasazení určuje Configuration Manager správnou metodu v každém případu použití.

Další informace najdete v tématu [Vytvoření typů nasazení pro aplikaci](../deploy-use/create-applications.md#bkmk_create-dt).

### <a name="requirements"></a>Požadavky

V předchozích verzích Configuration Manager byste vytvořili kolekci zařízení pro nasazení aplikace na. I když stále můžete vytvořit kolekci, použijte *požadavky* k určení podrobnějších kritérií pro nasazení aplikace.

Například určete, že aplikace může být nainstalována pouze na zařízení s Windows 10. Když nasadíte aplikaci na všechna vaše zařízení, nainstaluje se jenom na zařízení s Windows 10.

Configuration Manager vyhodnotí požadavky, aby bylo možné určit, zda nainstaluje aplikaci a jakýkoli z jejích typů nasazení. Poté určí vhodný typ nasazení, dle kterého bude aplikace nainstalována. Každých 7 dní ve výchozím nastavení klient Configuration Manager znovu vyhodnocuje pravidla požadavků, aby určil dodržování předpisů podle nastavení klienta **naplánovat opakované vyhodnocení nasazení**.

Další informace najdete v tématu [Vytvoření a nasazení](../get-started/create-and-deploy-an-application.md) [požadavků na typ](../deploy-use/create-applications.md#bkmk_dt-require)aplikace a nasazení.

### <a name="global-conditions"></a>Globální podmínky

Při použití požadavků s konkrétním typem nasazení v jedné aplikaci můžete také vytvořit *globální podmínky*. Tyto podmínky jsou knihovnou předdefinovaných požadavků, které můžete použít s libovolným typem aplikace a nasazení. Configuration Manager obsahuje sadu integrovaných globálních podmínek, nebo můžete vytvořit vlastní.

Další informace najdete v tématu [Vytvoření globálních podmínek](../deploy-use/create-global-conditions.md).

### <a name="simulated-deployment"></a>Simulované nasazení

*Simulované nasazení* vyhodnocuje požadavky, metodu detekce a závislosti pro aplikaci. Klient hlásí výsledky, aniž by se skutečně nainstalovala aplikace.

Další informace najdete v tématu [Simulace nasazení aplikace](../deploy-use/simulate-application-deployments.md).  

### <a name="deployment-action"></a>Akce nasazení

*Akce nasazení* určuje, jestli chcete nainstalovat nebo odinstalovat aplikaci, kterou nasazujete. Ne všechny typy nasazení podporují akci odinstalace.

Další informace najdete v tématu [nasazení aplikací](../deploy-use/deploy-applications.md).  

### <a name="deployment-purpose"></a>Účel nasazení

*Účel nasazení* určuje, jestli je aplikace pro nasazení **povinná** nebo **dostupná**:  

- Klient automaticky nainstaluje *požadované* nasazení podle plánu, který jste nastavili. Pokud aplikace není skrytá, může uživatel sledovat jeho stav nasazení. Můžou také pomocí centra softwaru instalovat aplikaci před konečným termínem.  

- Pokud nasadíte aplikaci pro uživatele jako *k dispozici*, uvidí ji v centru softwaru a může na vyžádání požádat.  

Další informace najdete v tématu [nasazení aplikací](../deploy-use/deploy-applications.md).  

### <a name="revisions"></a>Revize

Když provedete *Revize* aplikace nebo typu nasazení, Configuration Manager vytvoří novou verzi aplikace. V konzole Configuration Manager proveďte následující akce:

- Zobrazit historii jednotlivých revizí aplikace
- Zobrazit jeho vlastnosti
- Obnovení předchozí verze aplikace
- Odstraní starou verzi.

Další informace najdete v tématu [aktualizace a vyřazení aplikací](../deploy-use/update-and-retire-applications.md).  

### <a name="detection-method"></a>Metoda detekce

Pomocí *metod detekce* zjistíte, jestli už je v zařízení nainstalovaná aplikace. Pokud metoda detekce indikuje, že je aplikace nainstalovaná, Configuration Manager se nepokusí o její instalaci znovu.

Další informace najdete v tématu [Možnosti metody detekce typu nasazení](../deploy-use/create-applications.md#bkmk_dt-detect).

### <a name="dependencies"></a>Závislosti

*Závislosti* definují jeden nebo více typů nasazení z jiné aplikace, kterou musí klient nainstalovat před instalací tohoto typu nasazení.

Další informace najdete v tématu [závislosti typu nasazení](../deploy-use/create-applications.md#bkmk_dt-depend).  

### <a name="supersedence"></a>Nahrazení

Configuration Manager umožňuje upgradovat nebo nahradit stávající aplikace pomocí vztahu *nahrazování* . Při nahrazování aplikace zadáte nový typ nasazení, který nahradí typ nasazení nahrazené aplikace. Můžete také rozhodnout, zda má být nahrazená aplikace upgradována nebo odinstalována předtím, než klient nainstaluje nahrazující aplikaci.

Další informace najdete v tématu [nahrazování aplikací](../deploy-use/revise-and-supersede-applications.md#application-supersedence).  

### <a name="user-centric-management"></a>Správa zaměřená na uživatele

Configuration Manager aplikace podporují *správu*zaměřenou na uživatele, která umožňuje přidružit konkrétní uživatele k určitým zařízením. Místo toho, abyste si museli pamatovat název zařízení uživatele, nasaďte aplikace pro uživatele a zařízení. Tato funkce vám pomůže zajistit, aby nejdůležitější aplikace byly vždycky dostupné na každé ze zařízení uživatele. Pokud uživatel získá nový počítač, Configuration Manager do zařízení automaticky nainstaluje své aplikace, než se přihlásí.

Další informace najdete v tématu [propojení uživatelů a zařízení pomocí spřažení uživatelských zařízení](../deploy-use/link-users-and-devices-with-user-device-affinity.md).  

### <a name="application-group"></a>Skupina aplikací

Počínaje verzí 1906 vytvořte skupinu aplikací, které můžete odeslat do kolekce uživatelů nebo zařízení jako jediné nasazení. Metadata, která zadáte o skupině aplikací, se zobrazují v centru softwaru jako jediná entita. Aplikace můžete seřadit ve skupině, aby je klient nainstalovaly v určitém pořadí.

Další informace najdete v tématu [Vytvoření skupin aplikací](../deploy-use/create-app-groups.md).

## <a name="what-application-types-can-you-deploy"></a>Jaké typy aplikací můžete nasadit?

Configuration Manager umožňuje nasadit následující typy aplikací:  

- Instalační služba systému Windows (MSI)  

- Balíček aplikace pro Windows a sady prostředků aplikace (appx, appxbundle, msix, msixbundle)  

- Balíček aplikace pro systém Windows v Microsoft Store  

- Instalační program skriptů pro instalační programy třetích stran a obálky skriptů

- Microsoft App-V v4 a V5  

- macOS  

- Pořadí úloh nasazení mimo operační systém pro komplexní aplikace

Při správě zařízení prostřednictvím Configuration Manager [místní správy zařízení](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)navíc můžete spravovat tyto další typy aplikací:  

- Balíček aplikace Windows Phone (XAP)  

- Balíček aplikace Windows Phone v Microsoft Store  

- Instalační služba systému Windows přes MDM (MSI)  

- Webová aplikace

## <a name="state-based-applications"></a>Aplikace na základě stavu  

Configuration Manager aplikace používají monitorování na základě stavu. Můžete sledovat poslední stav nasazení aplikace pro uživatele a zařízení. Stavové zprávy obsahují informace o jednotlivých zařízeních. Například pokud nasadíte aplikaci do kolekce uživatelů, můžete zobrazit stav dodržování předpisů nasazení a účel nasazení v konzole Configuration Manager. Monitorujte nasazení veškerého softwaru z pracovního prostoru **monitorování** v konzole Configuration Manager. Další informace najdete v tématu [monitorování aplikací](../deploy-use/monitor-applications-from-the-console.md).  

Klient Configuration Manager pravidelně přehodnocuje nasazení aplikací. Příklad:  

- Uživatel odinstaluje nasazenou aplikaci. V dalším cyklu vyhodnocení Configuration Manager zjistí, že aplikace není k dispozici. Klient pak aplikaci automaticky znovu nainstaluje.  

- Configuration Manager nenainstaloval aplikaci do zařízení, protože selhala při splnění požadavků. Později se v zařízení provede změna, takže teď splňuje požadavky. Configuration Manager tuto změnu detekuje a klient nainstaluje aplikaci.  

Můžete nastavit interval opakovaného vyhodnocení pro nasazení aplikací. Použijte nastavení klienta **naplánovat opakované vyhodnocení nasazení** ve skupině **nasazení softwaru** . Další informace najdete v tématu [informace o nastavení klienta](../../core/clients/deploy/about-client-settings.md#software-deployment).  

## <a name="get-started-creating-an-application"></a>Začínáme s vytvářením aplikace  

Pokud chcete přejít přímo v a vytvořit aplikaci, najdete postup v článku [Vytvoření a nasazení aplikace](../get-started/create-and-deploy-an-application.md) .  

Pokud jste obeznámeni se základy a hledáte Podrobnější referenční informace o všech dostupných možnostech, začněte [vytvářet aplikace](../deploy-use/create-applications.md).  

## <a name="software-center"></a>Centrum softwaru  

Centrum softwaru je aplikace pro Windows nainstalovaná s klientem Configuration Manager. Použijte ho pro následující akce:  

- Vyhledat a požádat o aplikace nasazené do zařízení nebo uživatele
- Instalace a plánování instalací softwaru
- Zobrazit stav instalace pro aplikace, aktualizace softwaru a operační systémy
- Konfigurace nastavení vzdáleného řízení
- Nastavení řízení spotřeby

Další informace najdete v těchto článcích:  

- [Plánování a konfigurace správy aplikací](../plan-design/plan-for-and-configure-application-management.md)
- [Plánování Centra softwaru](../plan-design/plan-for-software-center.md)
- [Uživatelská příručka Centra softwaru](../../core/understand/software-center.md)

> [!Note]  
> Podpora končí pro role katalogu aplikací s verzí 1910. Další informace najdete v tématu [Odebrání katalogu aplikací](../plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

## <a name="packages-and-programs"></a>Balíčky a programy  

Configuration Manager nadále podporuje balíčky a programy, které se používaly v předchozích verzích produktu.

Další informace najdete v tématu [balíčky a programy](../deploy-use/packages-and-programs.md).  

## <a name="next-steps"></a>Další kroky

Teď, když jste se seznámili se základními koncepty správy aplikací v Configuration Manager, pokračujte v následujících článcích:

- [Vytvoření a nasazení ukázkové aplikace](../get-started/create-and-deploy-an-application.md)
- [Plánování a konfigurace správy aplikací](../plan-design/plan-for-and-configure-application-management.md)
- [Vytváření aplikací](../deploy-use/create-applications.md)
