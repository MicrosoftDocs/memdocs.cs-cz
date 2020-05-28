---
title: Monitorování stavu
titleSuffix: Configuration Manager
description: Přečtěte si informace o tom, jak monitorování stavu funguje v Desktop Analytics.
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 119f787f15b8c907d0c760a12b973ca984f4348c
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268534"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>Monitorování stavu v Desktop Analytics

Když [nasadíte aktualizaci do produkčního prostředí](deploy-prod.md), pomocí nástroje Desktop Analytics můžete monitorovat stav svých zařízení. Tento článek podrobně popisuje, jak funguje sledování stavu.

Další informace o tom, jak tuto funkci používat, najdete v tématu [monitorování stavu aktualizovaných zařízení](deploy-prod.md#bkmk_monitor).

![Snímek obrazovky se stránkou monitorování stavu Desktop Analytics](media/monitor-health.png)

> [!NOTE]  
> Desktop Analytics shromažďuje jenom data o stavu ze zařízení, která poskytují data o využití, která může použít jako jmenovatel. To znamená, že neobsahují zařízení s Windows 7 a Windows 10, která nemají nastavená na sdílení diagnostických dat na rozšířené (omezené) úrovni. Pokud je více než 10% zařízení s Windows 10 nastavené na sdílení diagnostických dat na jiných úrovních než rozšířené (omezené), zobrazí se na stránce **sledování stavu** upozornění v oblasti banner.  

Pokud chcete zobrazit další informace o konkrétní aplikaci, vyberte ji v seznamu.

## <a name="apps"></a>Aplikace

### <a name="health-status-factors"></a>Faktory stavu

![Faktory stavu pro aplikaci v oblasti analýzy pro stolní počítače](media/monitor-health-status-factors.png)

Desktop Analytics monitoruje následující faktory stavu pro aplikace:

- **% Zařízení s chybami**: za poslední dva týdny počet zařízení, ve kterých došlo k chybě této konkrétní aplikace, dělený počtem zařízení, na kterých se aplikace používala. Toto zobrazení vám umožní zjistit, jestli se v nové verzi operačního systému zvýšila nebo snížila stabilita aplikace. Aplikace Desktop Analytics vypočítá toto procento pro následující sady:  

  - **Po aktualizaci**: zařízení, která se aktualizovaly na cílovou verzi operačního systému zadanou v plánu nasazení. Aby bylo možné snížit počet prostředků s nedostatečnými daty, bude tato data shromažďovat aplikace Desktop Analytics pro všechna vaše aktualizovaná zařízení. Tato sada zahrnuje zařízení, která nejsou v plánu nasazení.  

  - **Před aktualizací**: zařízení, která jsou ve verzi operačního systému starší než zadaná v plánu nasazení. Tento seznam nezahrnuje zařízení s Windows 7.  

  - **Komerční Průměrná**hodnota: Průměrná (průměrná) Chyba v rámci všech komerčních zařízení. Tento průměr se vypočítává napříč *všemi* verzemi aplikace. Pokud vaše verze zobrazuje míru chyb nad komerčním průměrem, může být k dispozici více stabilní verze.  

- **% Relací s chybami**: podobá se předchozímu, ale počítá procento relací s chybami za poslední dva týdny.  

Aby bylo možné určit stav aplikace, Analytics pro stolní počítače vyžaduje data minimálně na 20 zařízeních. V opačném případě oznamuje **nedostatečné množství dat** pro aplikaci. Služba vypočítá stav na základě *míry selhání relace* z těchto zařízení. Rychlost selhání zařízení se poskytuje jenom pro informace. Nepoužívá se při výpočtu stavu.

### <a name="usage"></a>Využití

<!-- 5533890 -->

- **Aktivní zařízení**: Tato hodnota je počet zařízení, ve kterých uživatel spustil vybranou aplikaci během posledních dvou týdnů. Vychází ze zařízení ve vybraném plánu nasazení, na kterých běží cílová verze Windows 10.

- **Relace**: Tato hodnota představuje celkový počet pokusů, kolikrát uživatel spustil vybranou aplikaci na cílové verzi Windows.

### <a name="additional-tabs"></a>Další karty

V dolní části stránky s podrobnostmi o aplikaci vám můžou pomoct tyto tři karty:

- **Další verze**: seznam alternativních verzí této aplikace. U každé verze zobrazuje relativní změny v rámci vaší organizace a komerční průměr. Pokud najdete novější verzi aplikace s nižší mírou havárie, může vám aktualizace aplikace pomáhat.  

    Také ukazuje, jestli má verze rozšířené přehledy. Další informace najdete v tématu [posouzení kompatibility](compat-assessment.md).  

- **Hlavní problémy**: seznam nejčastějších identifikátorů selhání podle počtu instancí. ID chyby identifikuje trasování zásobníku přidružené k chybě. Toto ID můžete použít při volání podpory od dodavatele aplikace.  

- **Nedávné havárie**: seznam zařízení, ve kterých nedávno došlo k chybě aplikace. Můžete filtrovat podle ID selhání a dalších kritérií. Tyto informace slouží k řešení tohoto problému shromažďováním protokolů nebo pokusy o opravy na konkrétních zařízeních před tím, než se pokusíte o širší nasazení.  

Pokud zjistíte vážnou regresi stavu, kterou nemůžete opravit, změňte **rozhodnutí o upgradu** aplikace na **neschopen**. Tato akce zabrání budoucímu nasazení aktualizace do zařízení s tímto Assetem.

## <a name="see-also"></a>Viz také

- [Posouzení kompatibility v Desktop Analytics](compat-assessment.md)  

- [Nasazení do produkčního prostředí s využitím Desktop Analytics](deploy-prod.md)  
