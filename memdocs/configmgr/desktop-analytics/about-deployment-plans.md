---
title: Plány nasazení v Desktop Analytics
titleSuffix: Configuration Manager
description: Přečtěte si o plánech nasazení v Desktop Analytics.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c14eb9127b096f7fc4e4680735867913ea877f54
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722533"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>O plánech nasazení v Desktop Analytics

Desktop Analytics shromažďuje a analyzuje data o zařízeních, aplikacích a ovladačích ve vaší organizaci. Na základě této analýzy a vašeho vstupu můžete službu použít k vytvoření plánů nasazení pro Windows 10. Plány nasazení mají následující funkce:  

- Automaticky doporučit, která zařízení se mají zahrnout do pilotních nasazení  

- Identifikace problémů s kompatibilitou a navrhování rizik  

- Vyhodnotit stav nasazení před, během a po aktualizacích  

- Sledování průběhu nasazení  

V rámci plánu nasazení provedete následující akce:  

- Definice verzí Windows 10, které chcete nasadit  

- Vyberte skupiny zařízení, do kterých chcete nasadit.  

- Vytvořit pravidla připravenosti pro nasazení  

- Definování důležitosti vašich aplikací  

- Výběr pilotních zařízení na základě automatických doporučení  

- Rozhodněte se, jak opravit problémy s aplikacemi na základě doporučení z Desktop Analytics.  

Ve výchozím nastavení Desktop Analytics aktualizuje data plánu nasazení každý den. Všechny změny, které provedete v rámci plánu nasazení, jako je například přiřazení důležitosti aplikaci nebo volba zařízení, které se má zahrnout do pilotního projektu, trvá až 24 hodin. Pokud chcete tento proces urychlit, požádejte o aktualizaci dat na vyžádání. Další informace najdete v tématu [Nejčastější dotazy k Desktop Analytics](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

Po připojení Desktop Analytics k Configuration Manager vyberte kolekce v plánech nasazení. Tato integrace pak umožní nasadit Windows do kolekce na základě dat z Desktop Analytics.



## <a name="readiness-rules"></a>Pravidla připravenosti

V plánech nasazení jsou k dispozici následující pravidla připravenosti:

- Zda zařízení automaticky obdrží ovladače od web Windows Update. Pokud zařízení obdrží aktualizace ovladačů od web Windows Update, budou všechny problémy s ovladači identifikované jako součást hodnocení připravenosti automaticky označeny jako **připravené**.  

- Prahová hodnota počtu instalací pro aplikace pro Windows Pokud je aplikace nainstalovaná na vyšší procento počítačů, než je tato prahová hodnota, plán nasazení označí aplikaci jako **zajímavosti**. Tato značka znamená, že se můžete rozhodnout, jak důležité je aplikace testovat v průběhu pilotní fáze.  


## <a name="plan-assets"></a>Plánování prostředků

<!-- 4670224 -->

I když oblast [assetů](about-assets.md) také zobrazuje zařízení a aplikace, zahrnuje oblast **plánování prostředků** v rámci konkrétního plánu nasazení další informace.

### <a name="devices"></a>Zařízení

Projděte si **rozhodnutí o upgradu Windows** pro každé zařízení v plánu nasazení.

Rozhodnutí o inovaci systému Windows, které **nahrazuje zařízení** , může být z jednoho z následujících důvodů:

- Nepovedlo se ověřit kontrolu požadovaného procesoru Windows 10. Další informace najdete v tématu [minimální požadavky na hardware](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview#31-processor).
- Má blok systému BIOS
- Nemá dostatek paměti.
- Součást důležitá pro spouštění v systému má blokovaný ovladač.
- Konkrétní značka a model nejde upgradovat.
- Existuje komponenta třídy zobrazení s blokem ovladače, který má všechny následující atributy:
    - Nepřepisujete
    - V nové verzi operačního systému není žádný ovladač.
    - Ještě není na web Windows Update
- V systému, který blokuje upgrade, je jiná komponenta Plug-and-Play.
- Je k dispozici bezdrátová komponenta, která používá ovladač Emulovaný na XP.
- Síťová součást s aktivním připojením ztratí svůj ovladač. Jinými slovy, po upgradu by mohlo dojít ke ztrátě připojení k síti.

Rozhodnutí o **opětovné instalaci** Windows Upgrade znamená, že upgrade bude vyžadovat přeinstalaci, a to na rozdíl od místního upgradu. 

**Blokované** rozhodnutí o upgradu systému Windows může být způsobeno následujícími důvody:

- Nastavili jste rozhodnutí o upgradu jednoho nebo více prostředků na hodnotu **neschopen**.

- Data inventáře pro toto zařízení jsou neúplná a Desktop Analytics nemůže provádět úplné posouzení kompatibility.

### <a name="apps"></a>Aplikace

Nastavte **rozhodnutí o upgradu** a **důležitost** této aplikace v tomto plánu nasazení. Další informace najdete v tématu [vytvoření plánů nasazení](create-deployment-plans.md).

V podrobnostech o aplikaci můžete zobrazit také následující informace: doporučení, rizikové faktory kompatibility a známé problémy společnosti Microsoft. Tyto informace vám pomůžou při nastavování **rozhodnutí o upgradu**. Další informace najdete v tématu [posouzení kompatibility](compat-assessment.md).

Aplikace, které Desktop Analytics zobrazuje jako *zajímavosti* , jsou založené na prahové hodnotě nízkého počtu instalací pro pravidla připravenosti plánu nasazení. Další informace najdete v tématu [pravidla připravenosti](create-deployment-plans.md#readiness-rules).

   > [!Tip]
   > Další informace o kategorii nedůležité aplikace najdete v tématu věnovaném [automatickému upgradu pro systém a aplikace ze Storu](about-assets.md#bkmk_plan-autoapp). <!-- 3587232 -->


### <a name="drivers"></a>Ovladače

Podívejte se na seznam ovladačů, které jsou součástí tohoto plánu nasazení. Nastavte **rozhodnutí o upgradu**, Projděte si doporučení Microsoftu a Prohlédněte si rizikové faktory kompatibility.


## <a name="importance"></a>Důležitost

Jako součást plánu nasazení nastavte *důležitost* aplikací. Desktop Analytics detekuje tyto aplikace jako nainstalované na cílových zařízeních. Toto nastavení pomáhá analýzám stolních počítačů určit, která zařízení obsahuje ve fázi pilotního nasazení.

Pokud je aplikace nainstalovaná na méně než 2% cílových zařízení, označí se za **nízký počet instalací**. Výchozí hodnota je dvě procenta. Prahovou hodnotu v nastavení připravenosti můžete upravit z 0% na 10%. Funkce Desktop Analytics tyto aplikace automaticky označí jako **připravené k upgradu**.  

Pro aplikace vyberte důležitost **kritické**, **důležité**nebo **nedůležité**. Pokud označíte jednu jako kritickou nebo důležitou, zahrnuje Analytics pro stolní počítače v pilotním nasazení některá zařízení s touto aplikací. Služba zahrnuje v pilotním nasazení více instancí kritické aplikace. Pokud aplikaci označíte jako nedůležitou, bude ji sada Desktop Analytics automaticky nastavit tak, aby byla **připravena k upgradu**.



## <a name="pilot-devices"></a>Pilotní zařízení

Desktop Analytics kombinuje vaše důležité informace s globálním nastavením pilotního nasazení. Pak vytvoří doporučení, která zařízení by měla být součástí pilotního nasazení. Doporučené pilotní nasazení zahrnuje zařízení s různými hardwarovými konfiguracemi a jednu nebo více instancí všech důležitých a důležitých aplikací. Pokud je aplikace označená jako kritická, služba v pilotním programu doporučuje více zařízení s touto aplikací.



## <a name="deployment-plans-in-configuration-manager"></a>Plány nasazení v Configuration Manager

Po vytvoření plánu nasazení použijte Configuration Manager k nasazení produktů. Po zahájení nasazení monitoruje Desktop Analytics nasazení na základě nastavení v plánu.


## <a name="next-steps"></a>Další kroky

- [Další informace o prostředcích Desktop Analytics](about-assets.md): zařízení, ovladače a aplikace  

- [Další informace o aktualizacích zabezpečení a funkcí](about-updates.md)  

- [Vytvoření plánu nasazení](create-deployment-plans.md)  
