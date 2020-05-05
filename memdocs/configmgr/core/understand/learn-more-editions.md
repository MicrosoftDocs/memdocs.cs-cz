---
title: Licencování a větve
titleSuffix: Configuration Manager
description: Seznamte se s licenčními požadavky pro možnosti instalace dostupné s Configuration Manager
ms.date: 06/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 495b87ae-41a4-49ba-abe2-d4f7d22ac0d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f18ed2180f1d526e2afa4872e8fa9018c7e18721
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722708"
---
# <a name="licensing-and-branches-for-configuration-manager"></a>Licencování a větve pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch), & System Center Configuration Manager (dlouhodobá údržba Branch)*

V tomto článku se dozvíte o licenčních požadavcích na možnosti instalace dostupné v Configuration Manager. Tyto možnosti instalace zahrnují následující větve:

- Aktuální větev
- LTSB (Long-Term Servicing Branch)
- Instalace pro zkušební verzi aktuální větve
- Větev Technical Preview

## <a name="licensing-overview"></a>Přehled licencování

Zákazníci s aktivním softwarem Software Assurance (SA) na základě licencí Configuration Manager nebo s ekvivalentními právy k předplatnému od 1. října 2016 mají práva k použití verze Configuration Manager 1606 z října 2016. Zákazníci s právy k Configuration Manager od 1. října 2016 budou při instalaci najít dvě licencované možnosti: aktuální větev a dlouhodobá obsluha větve (LTSB).

Kompletní podmínky a ujednání pro produkty, které zakoupíte prostřednictvím multilicenčních programů Microsoftu, najdete v tématu [licenční podmínky a dokumentace](https://go.microsoft.com/fwlink/?LinkId=800052).


## <a name="licensed-branches"></a>Licencované větve

Tento článek se odkazuje na smlouvu Software Assurance nebo na ekvivalentní práva k předplatnému. Tato licenční smlouva Microsoft uděluje práva k instalaci a používání Configuration Manager.

### <a name="current-branch"></a>Aktuální větev

Aktuální větev vyžaduje aktivní smlouvu Software Assurance nebo ekvivalentní práva k Configuration Manager. Další informace najdete v tématu [Software Assurance a Current Branch](#software-assurance-and-the-current-branch).

Tato větev je podporovaná pro použití v produkčních prostředích, která chtějí získávat pravidelné aktualizace kvality a funkcí od Microsoftu. Poskytuje přístup k používání všech funkcí a vylepšení.

Od verze 1710 se každá verze aktualizace stále bude podporovat po dobu 18 měsíců od jejího obecného data vydání. Další informace najdete v tématu [podpora Configuration Manager aktuální verze větví](../servers/manage/current-branch-versions-supported.md).

### <a name="long-term-servicing-branch-ltsb"></a>LTSB (Long-Term Servicing Branch)

LTSB vyžaduje aktuální smlouvu Software Assurance s Microsoftem od 1. října 2016. Další informace najdete v tématu [Software Assurance a LTSB](#software-assurance-and-the-ltsb).

Tato větev se podporuje pro použití v produkčních prostředích. Je určená pro zákazníky, kteří mají právo programu Software Assurance (SA) nebo ekvivalentní předplatné Configuration Manager vypršení platnosti od 1. října 2016. Tato větev je v porovnání s Current Branch omezená.

Důležité aktualizace zabezpečení pro Configuration Manager jsou k dispozici pro tuto větev, ale nejsou k dispozici žádné nové funkce.

### <a name="evaluation-installation-of-the-current-branch"></a>Instalace pro zkušební verzi aktuální větve

Zkušební verze nevyžaduje smlouvu Software Assurance s Microsoftem. [Zkušební](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) verze jsou vždycky aktuální branou a můžete je použít po dobu 180 dnů.

Instalaci zkušební verze můžete upgradovat na úplnou instalaci aktuální větve. Nemůžete upgradovat instalaci zkušební verze na dlouhodobou obsluhu.

### <a name="technical-preview-branch"></a>Větev Technical Preview

[Větev Technical Preview](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) je také k dispozici. Tato větev je omezené sestavení Configuration Manager, které umožňuje vyzkoušet nové funkce. Technical Preview nainstalujete pomocí jiného média než licencovaných verzí. Další informace najdete v tématu [Technical Preview](../get-started/technical-preview.md).


## <a name="software-assurance-agreements"></a>Smlouvy Software Assurance

Stav programu Software Assurance na licencích Configuration Manager nebo ekvivalentních práv k předplatnému od 1. října 2016 určuje větev, kterou můžete nainstalovat a používat.

### <a name="software-assurance-and-the-current-branch"></a>Software Assurance a aktuální větev

Práva k použití Configuration Manager aktuální větvi může poskytnout:

- **System Center:** Zákazníci s aktivním zabezpečením SA na počítačích se systémem System Center Standard nebo Datacenter můžou instalovat a používat možnost aktuální větve Configuration Manager.

- **System Center Configuration Manager:** Zákazníci s aktivním zabezpečením SA na licencích Configuration Manager nebo s ekvivalentními právy k předplatnému můžou nainstalovat a používat možnost aktuální větve Configuration Manager.

Pokud máte aktivní SA pro Configuration Manager licence nebo ekvivalentní práva k předplatnému od 1. října 2016:

- Můžete nainstalovat a používat aktuální větev.
- Pokud povolíte přidružení zabezpečení nebo předplatnému, musíte odinstalovat aktuální větev.

### <a name="software-assurance-and-the-ltsb"></a>Software Assurance a LTSB

Pokud máte aktivní SA pro Configuration Manager licence nebo ekvivalentní práva k předplatnému od 1. října 2016:

- Můžete nainstalovat a používat LTSB. Zákazníci, kteří mají trvalá práva k Configuration Manager nebo kteří můžou své přidružení nebo předplatnému předplatit, mohou nainstalovat verzi Configuration Manager LTSB, která je aktuální v době trvání platnosti.

LTSB je založen na aktuální větvi verze 1606 a má následující omezení:

- Neexistuje žádná podpora pro převod aktuální větve na LTSB. Pokud aktuálně máte lokalitu aktuální pobočky, musíte nainstalovat LTSB jako novou lokalitu.  

- LTSB nepodporuje všechny funkce aktuální větve. Další informace najdete v tématu [Úvod do větve dlouhodobé údržby](introduction-to-the-ltsb.md). Mezi tato omezení patří omezená sada funkcí, omezené možnosti upgradu a samostatný životní cyklus podpory produktu.  

### <a name="software-assurance-expiration-date"></a>Datum vypršení platnosti Software Assurance

2016 od verze 1606 základního média verze pro Configuration Manager můžete zadat datum vypršení platnosti vaší smlouvy Software Assurance. **Datum vypršení platnosti Software Assurance** je volitelnou hodnotou pro pohodlné připomenutí. Přidejte ho při spuštění Configuration Manager instalaci nebo později v konzole Configuration Manager.

> [!NOTE]
> Microsoft neověřuje datum vypršení platnosti, které zadáte, a nepoužívá toto datum pro ověření licence. Použijte ji jako připomenutí data vypršení platnosti. Tato hodnota je užitečná, když Configuration Manager pravidelně kontroluje nové aktualizace softwaru, které jsou k dispozici online. Váš stav licence Software Assurance by měl být aktuální, aby měl nárok na použití těchto dalších aktualizací.

#### <a name="to-specify-the-software-assurance-expiration-date"></a>Zadání data vypršení platnosti Software Assurance

- Když spouštíte instalaci z Configuration Manager média, zadejte hodnotu na stránce **kód Product Key** Průvodce instalací nástroje.

- V konzole Configuration Manager v **Nastavení hierarchie**zadejte hodnotu na kartě **licencování** .


## <a name="licensing-resources"></a>Prostředky licencování

Další informace o licencování produktu najdete v následujících zdrojích informací.

### <a name="microsoft-volume-licensing-service-center-vlsc"></a>Microsoft Volume Licensing Service Center (VLSC)

- [Přehled VLSC](https://www.microsoft.com/Licensing/existing-customer/vlsc-training-and-resources.aspx)

- [Podmínky produktu multilicenčního programu společnosti Microsoft](https://go.microsoft.com/fwlink/?LinkId=800052)

- Zákazníci s multilicencí můžou získat souhrn svých licencí z [centra služby Volume License Service](https://www.microsoft.com/Licensing/servicecenter/default.aspx). Přejděte do nabídky **licence** a vyberte **Souhrn licencí**.

### <a name="vlsc-videos"></a>Videa VLSC

- Výuková videa o tom, jak VLSC funguje, najdete v tématu [Microsoft Volume Licensing Service Center Training and Resources](https://www.microsoft.com/licensing/existing-customer/vlsc-training-and-resources) a v tématu **How to video**.

- [Kde vyhledat aktivní smlouvu Software Assurance](https://www.microsoft.com/showcase/video.aspx?uuid=fe1846cb-1d26-49fc-b064-57b25dcc31a0) (od 43 sekund)  

- [Jak získat oprávnění pro VLSC](https://www.microsoft.com/showcase/video.aspx?uuid=ac4ed1ca-d0a9-43cd-89fa-74ccb555dec4). Můžete delegovat oprávnění ke čtení a zápisu VLSC ostatním lidem ve vaší organizaci.
