---
title: Prostředky v Desktop Analytics
titleSuffix: Configuration Manager
description: Přečtěte si o zařízeních, ovladačích a aplikacích v Desktop Analytics.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: f87c4cc1bcbe8039acb5876dc8e26ac597f12e59
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107302"
---
# <a name="assets-in-desktop-analytics"></a>Prostředky v Desktop Analytics

Jakmile zařízení nahlásí data do Desktop Analytics, poskytne inventář těchto prostředků:

- Zařízení
- Nainstalované aplikace  

Na portálu služby vyberte **assets (prostředky** ) v nabídce Analytics pro stolní počítače.

## <a name="devices"></a>Zařízení

Karta **zařízení** zobrazuje klíčové informace o všech zařízeních ve vaší organizaci, které zaregistrujete do služby Desktop Analytics. Můžete řadit podle libovolného sloupce nebo filtru pro konkrétní hodnoty.

> [!NOTE]  
> Pokud řídicí panel neoznamuje počet zařízení, která očekáváte pro vaše prostředí, přečtěte si téma [řešení potíží s desktopovou analýzou](troubleshooting.md).  

V plánu nasazení je k dispozici více podrobností o zařízeních. Další informace najdete v tématu [plánování prostředků](about-deployment-plans.md#plan-assets) .

## <a name="apps"></a>Aplikace

Karta **aplikace** zobrazuje všechny nainstalované aplikace, které služba detekuje na vašich zařízeních s Windows.

Aplikace **zajímavosti** se instalují na více než 2% zaregistrovaných zařízení.

Nastavení **Podrobnosti verzí aplikace** je ve výchozím nastavení vypnuté, takže tato karta kombinuje všechny verze aplikací se stejným názvem a vydavatelem.<!-- 5542186 --> Výchozí chování pomáhá snížit celkový počet aplikací, které vidíte, což pomáhá snižovat vaše úsilí při přidávání poznámek k aplikacím. Toto nastavení se projeví i v počtu aplikací na dlaždici **aplikace zajímavosti** . Například místo výpisu stovek instancí Microsoft Edge existuje jedna instance pro všechny verze. Pro všechny verze můžete udělat rozhodnutí jednou. Pokud potřebujete rozhodnout o konkrétních verzích aplikace, zapněte toto nastavení. Toto nastavení můžete nakonfigurovat i při práci s plánem nasazení. Další informace najdete v tématu [plánování prostředků](about-deployment-plans.md#plan-assets).

Vyberte aplikaci ze seznamu a vyberte **Upravit**. Tato akce zobrazí podrobnosti o aplikaci. Vyberte rozevírací nabídku **důležitost** a nastavte hodnotu. Můžete také přiřadit **vlastníka**. Pokud provedete nějaké změny, vyberte **Uložit**.

Nakonfigurujte **důležitost** aplikací nastavením jedné z následujících kategorií:

- Kritické
- Důležité
- Ignorovat
- Nerevidováno
- Není důležité<!-- 3587232 -->

Pokud je nastavení **Podrobnosti verze aplikace** vypnuté, zobrazí se v podokně podrobností aplikace počet verzí aplikací a jazyků, které kombinuje. Pokud všechny změny v podrobnostech aplikace uložíte, platí pro všechny verze. Nastavte například **důležitost** nebo **vlastník**. Některé hodnoty zobrazí "vícenásobné", což znamená, že ve všech verzích není jedna konzistentní hodnota.

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a><a name="bkmk_plan-autoapp"> </a> Automatické rozhodnutí o upgradu pro systém a aplikace ze Storu

<!-- 3587232 -->
Určení **důležitosti** a **rozhodnutí o upgradu** je klíčové pro všechny aplikace zajímavosti v pracovním postupu Desktop Analytics. Aby bylo možné snížit úsilí při přidávání poznámek k těmto aplikacím, určité typy aplikací jsou automaticky označeny jako *nedůležité*. Rozhodnutí o upgradu plánu nasazení pro tyto aplikace je také označeno jako *připravené*. Následující aplikace jsou kompatibilní a měly by po upgradu Windows i nadále fungovat:

- Systémové aplikace a komponenty publikované Microsoftem

- Aplikace spravované a aktualizované z Microsoft Store

> [!TIP]
> Spravujte vstupy pro libovolnou aplikaci na globální úrovni nebo na plán nasazení.
>
> 1. Na portálu Analytics pro stolní počítače vyberte v nabídce **Spravovat** položku **assety**. Pak vyberte **aplikace**.
>
> 2. Ke správě těchto kategorií aplikací použijte sloupce **typ** a **kategorie** :
>
>    - Pro aplikace ze Storu, **typ** filtru jako **moderní**
>    - Pro systémové aplikace, filtrovat **kategorii** jako **proces na pozadí** nebo **součást systému Windows**

V plánu nasazení můžete také nastavit **rozhodnutí o upgradu**. Další informace najdete v tématu [plánování prostředků](about-deployment-plans.md#plan-assets).

### <a name="usage"></a>Využití

<!-- 5533890 -->

- **Celkový počet instalací**: Tato hodnota je počet instalací vybrané aplikace na všech zařízeních zaregistrovaných na Desktop Analytics.

- **Procento instalace**: Tato hodnota je procento instalací vybrané aplikace na celkový počet zařízení zaregistrovaných pro stolní analýzu.

- **Zařízení spustila tuto aplikaci za posledních 30 dnů**: Tato hodnota je počet zařízení, ve kterých uživatel spustil vybranou aplikaci. Zahrnuje jenom zařízení, která nahlásila využití v posledních 30 dnech. Tento počet se nachází ve všech vašich zařízeních zaregistrovaných pomocí stolních analýz, které běží na libovolné verzi Windows 10. Je možné, že tento počet se může u plánu nasazení lišit.

## <a name="next-steps"></a>Další kroky

- [Další informace o plánech nasazení Desktop Analytics](about-deployment-plans.md)  

- [Další informace o aktualizacích zabezpečení a funkcí](about-updates.md)  

- [Posouzení kompatibility v Desktop Analytics](compat-assessment.md)  
