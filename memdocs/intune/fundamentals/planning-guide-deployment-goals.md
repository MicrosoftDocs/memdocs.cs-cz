---
title: Vymezení cílů, úkolů a problémů při nasazení
titleSuffix: Microsoft Intune
description: Tento článek pomáhá vymezit cíle, úkoly a problémy spojené s cloudovou implementací Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 24cf9d97-db39-4b95-a664-4aa2e33edb87
ms.reviewer: jeffbu, cgerth
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9ff60d5823d7b249e4648b5858ff5ab2dcd5935a
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331055"
---
# <a name="determine-deployment-goals-objectives-and-challenges"></a>Vymezení cílů, úkolů a problémů při nasazení

Dobrý plán nasazení začíná identifikací cílů, úkolů a potenciálních problémů spojených s nasazením řešení v organizaci. Pojďme se na jednotlivé oblasti podívat podrobněji.

## <a name="deployment-goals"></a>Cíle nasazení

Cíle nasazení jsou dlouhodobé výsledky, kterých chcete nasazením Intune v organizaci dosáhnout. Tady je několik příkladů takových cílů, včetně jejich popisu a obchodní hodnoty.

- **Integrace s Office 365 a podpora použití mobilních aplikací Office**

  - **Popis:** Zajištění úzké integrace Office 365 a použití mobilních aplikací Office, včetně jejich ochrany.

  - **Obchodní hodnota:** Zabezpečené a vylepšené uživatelské prostředí, které umožňuje uživatelům používat známé a oblíbené aplikace.

- **Zpřístupnění interních firemních služeb na mobilních zařízeních**

  - **Popis:** Umožní zaměstnancům, aby byli produktivní všude, kde potřebují pracovat, a s libovolným zařízením, které je pro ně nejvhodnější. Projekt má zajistit mobilní produktivitu a bezpečný přístup k firemním datům.

  - **Obchodní hodnota:** Umožní zaměstnancům, aby byli aktivní a mohli pracovat odkudkoliv. Podnikům zase nabízí větší konkurenceschopnost a hodnotnější pracovní prostředí.

- **Zajištění ochrany dat v mobilních zařízeních**

  - **Popis:** Pokud jsou data uložená v mobilním zařízení, musí být chráněna proti poškození, náhodné ztrátě nebo sdílení.

  - **Obchodní hodnota:** Ochrana dat je nezbytným předpokladem zachování konkurenceschopnosti, který organizaci umožňuje zacházet s klienty a jejich daty co nejopatrněji.

- **Snižování nákladů**

  - **Popis:** Pokud je to možné, snižuje projekt náklady na nasazení a provoz.

  - **Obchodní hodnota:** Efektivní využití prostředků umožňuje podnikům investovat do jiných oblastí, zachovat si konkurenceschopnost a poskytovat lepší služby klientům.

## <a name="deployment-objectives"></a>Úkoly nasazení

Úkoly nasazení jsou akce, které musí organizace provést, aby dosáhla cílů nasazení Intune. Tady jsou některé příklady úkolů při nasazení, včetně způsobu jejich plnění.

- **Snížení počtu řešení pro správu zařízení**

  - **Implementace:** Sjednocení do jediného řešení pro správu mobilních zařízení Microsoft Intune, které chrání firemní data v aplikacích a zařízeních.

- **Zajištění zabezpečeného přístup k Exchangi a SharePointu Online**

  - **Implementace:** Použijte podmíněný přístup pro Exchange a SharePoint Online.

- **Zabránění ukládání nebo přeposílání firemních dat v mobilním zařízení jiným než firemním službám**

  - **Implementace:** Použít zásady ochrany aplikací v Intune pro Microsoft Office a obchodní aplikace.

- **Zajistit možnost vymazání firemních dat ze zařízení**

  - **Implementace:** Registrace zařízení do Intune. V případě potřeby si tím zajistíte možnost vzdáleného vymazání firemních dat a prostředků.

## <a name="deployment-challenges"></a>Aspekty nasazení

Problémy při nasazení mají pro organizaci nejvyšší prioritu, protože mohou negativně ovlivnit nasazení. Někdy souvisejí s minulými problémy z předchozích projektů, kterým byste se chtěli vyhnout, nebo s novými problémy, které se týkají současného nasazení. Tady jsou příklady problémů při nasazení Intune spolu s možnostmi, jak je zmírnit.

- Při úvodním stanovení rozsahu projektu se nepřihlédlo k připravenosti podpory a zkušenostem koncových uživatelů. To vede k nedostatečnému osvojení koncovými uživateli a k problémům s podporou v organizaci.

  - **Zmírnění dopadů:** Začlenit školení podpory. Doplnit plán nasazení o ověření zkušeností koncových uživatelů prostřednictvím měřítek úspěšnosti.

- Nedostatek jasně definovaných cílů a měřítek úspěšnosti vede k nedefinovatelným výsledkům. Při vzniku problémů se organizace může dostat do situace, kdy na ně reaguje dodatečně.

  - **Zmírnění dopadů:** Definujte cíle a metriky úspěšnosti už na začátku projektu a použijte tyto údaje, abyste podpořili další zaváděcí fáze. Zajistěte, aby cíle vyhovovaly pravidlu SMART (Specific = konkrétní, Measurable = měřitelné, Attainable = dosažitelné, Realistic = reálné a Timely = včas). V každé fázi naplánujte měření cílů, abyste zajistili průběh projektu podle plánu.

- Opomenete vytvořit , ověřit a důsledně sdílet jasný návrh přidané hodnoty, který zajistí podporu celé organizace. Častým důsledkem je omezené osvojení a nedostatečná návratnost investic (ROI).

  - **Zmírnění dopadů:** Pravděpodobně se už nemůžete dočkat, až projekt zahájíte. Přesto se napřed ujistěte, že máte jasně definované cíle a úkoly. Ty pak uvádějte na všech propagačních akcích a školeních, abyste pomohli uživatelům pochopit, proč organizace vybrala Intune.

## <a name="next-steps"></a>Další kroky

Po identifikaci cílů, úkolů a možných problémů při nasazení můžete přejít k další části, kterou je [identifikace scénářů použití](planning-guide-scenarios.md).
