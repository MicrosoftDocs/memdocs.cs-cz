---
title: Jak nasadit do pilotního nasazení
titleSuffix: Configuration Manager
description: Návod, jak nasadit do pilotní skupiny pro Desktop Analytics.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b0e939b51c464215ac1d4feea539ceb5677a01a6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723681"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>Jak nasadit do pilotního nasazení pomocí Desktop Analytics

Jednou z výhod funkce Desktop Analytics je pomáhat identifikovat nejmenší sadu zařízení, která poskytují nejširší pokrytí faktorů. Zaměřuje se na faktory, které jsou nejdůležitější pro pilotní nasazení upgradů a aktualizací Windows. Zajištění úspěšnosti pilotního nasazení vám umožní rychleji přesunout a spolehlivě nasadit rozsáhlá nasazení v produkčním prostředí.  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

## <a name="identify-devices"></a>Identifikace zařízení

Prvním krokem je identifikace zařízení, která se mají zahrnout do pilotního projektu. Desktop Analytics doporučuje zařízení na základě hlášených dat a v tomto seznamu můžete zahrnout nebo nahradit zařízení.

1. Přejít na [portál Desktop Analytics](https://aka.ms/desktopanalytics)a ve skupině spravovat vyberte **plány nasazení**.

1. Vyberte plán nasazení.

1. Ve skupině připravit v nabídce plán nasazení vyberte **identifikovat pilotní nasazení**.

Zobrazí se data z Desktop Analytics, které zobrazuje počet zařízení, která doporučuje, včetně optimálního pokrytí. Tento algoritmus je primárně založený na použití důležitých a kritických aplikací a šířce hardwarových konfigurací.

Pro další seznam doporučených zařízení proveďte následující akce:

- **Přidat vše do pilotního nasazení**: Přidá všechna doporučená zařízení do pilotní skupiny.
- **Přidat do pilotního nasazení**: jenom přidat jednotlivá zařízení
- **Nahradit** všechna konkrétní zařízení z pilotního projektu

Při přidávání zařízení z **doporučeného** do **zahrnutého** pilotního seznamu se zvyšuje pokrytí a redundance vašich důležitých a důležitých prostředků v pilotním projektu. Vyšší redundance znamená, že pokryté prostředky mají statisticky velký počet zařízení, která jsou součástí vašeho pilotního projektu.

## <a name="global-pilot"></a><a name="bkmk_GlobalPilot"></a>Globální pilotní nasazení

Můžete také učinit rozhodnutí o tom, které kolekce Configuration Manager zahrnout nebo vyloučit z pilotního nasazení. V nabídce hlavní plocha Analytics klikněte ve skupině globální nastavení na možnost **globální pilotní nasazení**.

Pokud připojíte více Configuration Manager hierarchií ke stejné instanci aplikace Desktop Analytics, zobrazí se zobrazovaný název hierarchie s názvem kolekce v globální pilotní konfiguraci. Tento název je vlastnost **Zobrazovaný název** v připojení Desktop Analytics v konzole Configuration Manager.<!-- 4814075 -->

> [!NOTE]
> Podpora pro více hierarchií vyžaduje Configuration Manager verze 1910 nebo novější.

- Nezahrnovat kolekce, které obsahují více než 20% vašich celkových zaregistrovaných zařízení na Desktop Analytics. Pokud zahrnete velkou kolekci, na portálu se zobrazí upozornění. Můžete zahrnout několik malých kolekcí bez upozornění, ale stále buďte opatrní na počtu zařízení v pilotním projektu. <!-- 6079184 -->

- Chcete-li získat přesné pilotní doporučení pro plány nasazení v konkrétní hierarchii Configuration Manager, zahrňte pouze kolekce z této hierarchie.

### <a name="example"></a>Příklad

- Nakonfigurujete připojení Desktop Analytics v Configuration Manager tak, aby se nacíleno na kolekci **všechny systémy** . Tato akce zapíše všechny klienty do služby.

- Také nakonfigurujete další kolekce pro synchronizaci s desktopovou analýzou:

  - Všichni klienti se systémem Windows 10 (3 000 zařízení)

  - Všechna zařízení IT (200 celkem zařízení, 150 z nichž se spouští Windows 10)

  - Výkonný úřad (20 zařízení)

- V **globálním nastavení pilotu** zahrnete kolekce **všech klientů Windows 10** . Vyloučíte si kolekci **Office pro generálního ředitele** .

- Vytvoříte plán nasazení a jako **cílovou skupinu**vyberete **všechny kolekce IT zařízení** . Tento plán nasazení zamýšlíte jenom pro zařízení v oddělení IT.

- Seznam **zahrnutých pilotních zařízení** obsahuje podmnožinu zařízení, která jsou v **cílové skupině**: **všechna zařízení IT** a *globální seznam* povolených pilotních souborů: **Všichni klienti se systémem Windows 10**. 150 zařízení jsou v tomto seznamu, protože v kolekci **všech IT zařízení** běží pouze 150 zařízení s Windows 10.

- Seznam **dalších doporučených zařízení** obsahuje sadu zařízení z vaší **cílové skupiny** , která poskytuje maximální rozsah a redundanci vašich důležitých prostředků. Funkce Desktop Analytics z tohoto seznamu vyloučí všechna zařízení v globálním seznamu *vyloučení* , který je vaším globálním čepem: generální **ředitel**.

## <a name="address-issues"></a>Problémy s adresou

Pomocí portálu pro Desktop Analytics můžete zkontrolovat všechny nahlášené problémy s prostředky, které můžou zablokovat vaše nasazení. Pak schválí, odmítne nebo upraví navrhovanou opravu. Před zahájením pilotního nasazení musí být všechny položky označeny jako **připravené** nebo **připravené (s nápravou)** .

1. Přejít na [portál Desktop Analytics](https://aka.ms/desktopanalytics)a ve skupině spravovat vyberte **plány nasazení**.  

2. Vyberte plán nasazení.  

3. Ve skupině připravit v nabídce plán nasazení vyberte **připravit pilotní nasazení**.  

4. Na kartě **aplikace** zkontrolujte aplikace, které vyžadují vaše zadání.  

5. Pro každou aplikaci vyberte název aplikace. V podokně informace si Projděte doporučení a vyberte rozhodnutí o upgradu. Pokud se rozhodnete, že jste **nezkontrolovali** nebo **nemůžete**, pak analýza plochy nebude v pilotním nasazení zahrnovat zařízení s touto aplikací. Pokud zvolíte možnost **připraveno (s nápravou)**, můžete pomocí **poznámek k nápravě** zachytit akce, které se mají provést při řešení problému, jako je například *Přeinstalace* nebo *vyhledání Doporučené verze výrobce*.

6. Tuto kontrolu opakujte pro ostatní prostředky.  

Další informace, které vám pomůžou s tímto procesem kontroly, najdete v tématu [vyhodnocení kompatibility](compat-assessment.md).

## <a name="create-software"></a>Vytvořit software

Předtím, než budete moci nasadit systém Windows, nejprve vytvořte softwarové objekty v nástroji Configuration Manager. Další informace najdete v tématu [pořadí úkolů místního upgradu Windows 10](../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md).

## <a name="deploy-to-pilot-devices"></a>Nasazení do pilotních zařízení

Configuration Manager používá data z Desktop Analytics k vytváření kolekcí pro pilotní nasazení a provozní nasazení. Chcete-li zajistit, aby zařízení byla po každé fázi nasazení v pořádku, použijte následující postup k vytvoření fáze nasazení s integrovaným prostředím Desktop Analytics:

1. V konzole Configuration Manager klikněte na **Knihovna softwaru**, rozbalte položku **Údržba Desktop Analytics**a vyberte uzel **plány nasazení** .  

2. Vyberte plán nasazení a na pásu karet vyberte **podrobnosti plánu nasazení** .  

3. Na pásu karet vyberte **vytvořit dvoufázové nasazení** . Tato akce spustí Průvodce vytvořením postupného nasazení.

    > [!Tip]  
    > Pokud chcete vytvořit klasické nasazení pořadí úkolů jenom pro pilotní kolekci, vyberte na dlaždici **stav pilota** možnost **nasadit** . Tato akce spustí Průvodce nasazením softwaru. Další informace naleznete v části [Deploy a task sequence](../osd/deploy-use/deploy-a-task-sequence.md).  

4. Zadejte název nasazení a vyberte pořadí úloh, které se má použít. Pomocí této možnosti můžete **automaticky vytvořit výchozí dvoufázové nasazení**a potom nakonfigurovat následující kolekce:  

    - **První kolekce**: vyhledejte a vyberte **pilotní** kolekci pro tento plán nasazení. Standardní konvence pojmenování pro tuto `<deployment plan name> (Pilot)`kolekci jsou.

    - **Druhá kolekce**: vyhledejte a vyberte **výrobní** kolekci pro tento plán nasazení. Standardní konvence pojmenování pro tuto `<deployment plan name> (Production)`kolekci jsou.

    > [!Note]  
    > Při integraci Desktop Analytics Configuration Manager pro plán nasazení automaticky vytvoří pilotní a produkční kolekce. Než je můžete použít, může trvat i čas, než se tyto kolekce synchronizují. Další informace najdete v tématu [řešení potíží – latence dat](troubleshooting.md#data-latency).<!-- 4984639 -->
    >
    > Tyto kolekce jsou vyhrazené pro zařízení plánu nasazení Desktop Analytics. Ruční změny těchto kolekcí se nepodporují.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Dokončete průvodce pro konfiguraci postupného nasazení. Další informace najdete v tématu [Vytvoření dvoufázové nasazení](../osd/deploy-use/create-phased-deployment-for-task-sequence.md).

    > [!Note]  
    > Výchozí nastavení můžete použít k **automatickému zahájení této fáze po dobu odložení (ve dnech)**. Pro začátek druhé fáze musí být splněna následující kritéria:
    >
    > 1. První fáze dosáhne **procentuálních kritérií úspěšnosti nasazení** pro úspěch. Toto nastavení nakonfigurujete ve dvoufázovém nasazení.
    > 1. Musíte zkontrolovat a učinit rozhodnutí o upgradu v Desktop Analytics a označit důležité a důležité prostředky jako *připravené*. Další informace najdete v tématu [Kontrola prostředků, které potřebují rozhodnutí o upgradu](deploy-prod.md#bkmk_review).
    > 1. Desktop Analytics se synchronizuje s Configuration Managermi kolekcemi všech produkčních zařízení, která splňují kritéria pro *Příprava* .

> [!Important]  
> Tyto kolekce se budou i nadále synchronizovat se změnami členství. Pokud například zjistíte problém s Assetem a označíte ho jako **nemožné**, zařízení s tímto prostředkem již nebudou splňovat kritéria pro *přípravu* . Tato zařízení jsou vyřazena z produkční kolekce nasazení.

## <a name="monitor"></a>Monitorování

### <a name="configuration-manager-console"></a>Konzola nástroje Configuration Manager

Otevřete plán nasazení. Dlaždice **Příprava rozhodnutí o upgradu – celkový stav** poskytuje souhrn stavu plánu nasazení. Tento stav je určen pro pilotní i produkční kolekce. Zařízení mohou patřit do jedné z následujících kategorií:

- **Aktuální**: zařízení se upgradovali na cílovou verzi Windows pro tento plán nasazení.

- **Rozhodnutí o upgradu bylo dokončeno**: jeden z následujících stavů:

  - Zařízení s zajímavosti prostředky, které jsou **připravené** nebo **připravené s nápravou**

  - Stav zařízení je **zablokovaný**, [**nahraďte zařízení**](about-deployment-plans.md#plan-assets) nebo **ho přeinstalujte** .

- **Nezkontrolováno**: zařízení s prostředky zajímavosti **nejsou přezkoumána** nebo **probíhá kontrola** .

Stav zařízení se aktualizuje na dlaždicích stav **pilota** a **stav výroby** s následujícími akcemi:

- Provedete změny v posouzení kompatibility
- Zařízení se upgradují na cílovou verzi Windows.
- Průběh nasazení

Monitorování nasazení Configuration Manager můžete také použít stejně jako jakékoli jiné nasazení pořadí úloh. Další informace najdete v tématu [monitorování nasazení operačního systému](../osd/deploy-use/monitor-operating-system-deployments.md).

### <a name="desktop-analytics-portal"></a>Portál pro Desktop Analytics

Pomocí [portálu pro Desktop Analytics](https://aka.ms/desktopanalytics) můžete zobrazit stav jakéhokoli plánu nasazení. Vyberte plán nasazení a pak vyberte **plán – přehled**.

![Snímek obrazovky s přehledem plánu nasazení v Desktop Analytics](media/deployment-plan-overview.png)

Vyberte dlaždici **pilotního nasazení** . Shrnuje aktuální stav pilotního nasazení. Tato dlaždice také zobrazuje data počtu nespuštěných zařízení, probíhajících, dokončených a vrácených problémů.

Všechna zařízení, která hlásí chyby nebo jiné problémy, jsou uvedena také v oblasti podrobností pilotního nasazení vpravo. Pokud chcete získat podrobnosti o nahlášeném problému, vyberte **zkontrolovat**. Tato akce změní zobrazení na stránku **stavu nasazení** .

Na stránce **stav nasazení** jsou uvedena zařízení v následujících kategoriích:

- Nezahájeno
- Probíhá
- Dokončeno
- Vyžaduje pozornost – zařízení
- Vyžaduje pozornost – problémy

Kategorie **vyžadovat pozornost** zobrazuje stejné informace, ale seřazené jinak.

Pokud chcete získat další podrobnosti o zjištěném problému, vyberte konkrétní seznam v jednom zobrazení.

Jak řešíte tyto problémy s nasazením, řídicí panel dál zobrazuje průběh zařízení. Aktualizuje se, protože zařízení se pohybují od potřeb, aby se **dokončila** **pozornost** .

## <a name="next-steps"></a>Další kroky

Umožněte, aby pilot běžel v průběhu shromažďování provozních dat. Doporučte uživatelům pilotních zařízení testovat aplikace.

Když zkušební nasazení splní vaše kritéria úspěchu, přečtěte si další článek, který nasadí do produkčního prostředí.
> [!div class="nextstepaction"]  
> [Nasazení do produkčního prostředí](deploy-prod.md)  
