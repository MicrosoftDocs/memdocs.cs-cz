---
title: Prostředky v Desktop Analytics
titleSuffix: Configuration Manager
description: Přečtěte si o zařízeních, ovladačích a aplikacích v Desktop Analytics.
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe1338781cbb16a8485de050a294e34e487a2ecc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722547"
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

Nakonfigurujte **důležitost** aplikací nastavením jedné z následujících kategorií:

- Kritická
- Důležité
- Ignorovat
- Nerevidováno
- Není důležité<!-- 3587232 -->

Vyberte aplikaci ze seznamu a vyberte **Upravit**. Tato akce zobrazí podrobnosti o aplikaci. Vyberte rozevírací nabídku **důležitost** a nastavte hodnotu. Můžete také přiřadit **vlastníka**. Pokud provedete nějaké změny, vyberte **Uložit**.

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a><a name="bkmk_plan-autoapp" />Automatické rozhodnutí o upgradu pro systém a aplikace ze Storu

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

V plánu nasazení můžete také nastavit **rozhodnutí o upgradu**. Další informace najdete v tématu [plánování prostředků](about-deployment-plans.md#plan-assets) .

### <a name="usage"></a>Využití

<!-- 5533890 -->

- **Celkový počet instalací**: Tato hodnota je počet instalací vybrané aplikace na všech zařízeních zaregistrovaných na Desktop Analytics.

- **Procento instalace**: Tato hodnota je procento instalací vybrané aplikace na celkový počet zařízení zaregistrovaných pro stolní analýzu.

- **Zařízení spustila tuto aplikaci za posledních 30 dnů**: Tato hodnota je počet zařízení, ve kterých uživatel spustil vybranou aplikaci. Zahrnuje jenom zařízení, která nahlásila využití v posledních 30 dnech. Tento počet se nachází ve všech vašich zařízeních zaregistrovaných pomocí stolních analýz, které běží na libovolné verzi Windows 10. Je možné, že tento počet se může u plánu nasazení lišit.

## <a name="next-steps"></a>Další kroky

- [Další informace o plánech nasazení Desktop Analytics](about-deployment-plans.md)  

- [Další informace o aktualizacích zabezpečení a funkcí](about-updates.md)  

- [Posouzení kompatibility v Desktop Analytics](compat-assessment.md)  
