---
title: Doporučení pro řízení spotřeby
titleSuffix: Configuration Manager
description: Přečtěte si doporučení Microsoftu pro řízení spotřeby v Configuration Manager.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 02cfb32f9187ca5a0ae0ad70ffcb4b85db8afb1b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715260"
---
# <a name="recommendations-for-power-management-in-configuration-manager"></a>Doporučení pro řízení spotřeby v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pro řízení spotřeby v Configuration Manager použijte následující doporučení.  

## <a name="monitor-at-a-representative-time"></a>Monitorování v reprezentativním čase

Monitorovací fáze řízení spotřeby poskytuje následující informace z počítačů ve vaší organizaci:

- Spotřeba energie
- Aktivita
- Možnosti řízení spotřeby
- Dopad na životní prostředí

Vyberte reprezentativní čas pro monitorování zařízení. Například monitorování během veřejné dovolené neposkytuje realistickou sestavu o využití výkonu počítače.

## <a name="create-a-control-collection"></a>Vytvoření kolekce ovládacích prvků

Vytvořte dvě kolekce počítačů, které vám pomohou monitorovat účinky použití schémat napájení na počítače. První kolekce by měla obsahovat většinu počítačů, u kterých chcete použít nastavení napájení. *Kolekce ovládacích prvků* by měla obsahovat zbývající počítače. Použijte požadované schéma řízení spotřeby na první kolekci. Pak spusťte sestavy, abyste porovnali dopad mezi oběma kolekcemi.  

## <a name="run-reports-before-you-apply-a-plan"></a>Spouštění sestav před použitím plánu

Než použijete schéma řízení spotřeby na kolekci počítačů, spusťte sestavu **nastavení napájení** . Tato sestava vám pomůže pochopit nastavení řízení spotřeby, která jsou už nakonfigurovaná na počítačích v kolekci. Pokud pro počítače použijete nové nastavení řízení spotřeby bez předchozího prozkoumání stávajícího nastavení, může to zvýšit spotřebu energie.  

## <a name="exclude-servers"></a>Vyloučit servery

Řízení spotřeby pro počítače, na kterých běží Windows Server, se nepodporuje. Přidejte servery do kolekce a vylučte z řízení spotřeby.  

> [!NOTE]
> I když Configuration Manager nepodporuje řízení spotřeby Windows serveru, stále shromažďuje data o využití spotřeby pro účely analýzy a vytváření sestav.

## <a name="exclude-other-computers"></a>Vyloučení dalších počítačů

Pokud máte počítače, které nechcete spravovat pomocí řízení spotřeby, přidejte tyto počítače do kolekce vyloučení.  

Je možné, že budete chtít vyloučit z řízení spotřeby následující typy počítačů:

- Počítače, které musí zůstat zapnuté.  

- Počítače, ke kterým se uživatelé potřebují připojit vzdáleně.  

- Počítače, které nemůžou používat řízení spotřeby.  

- Počítače, které mají roli distribučního bodu systému lokality.  

- Veřejné počítače, například veřejné počítače, informační displeje nebo monitorovací konzoly, kde musí být počítač a monitor vždy zapnuté.  

Další informace najdete v tématu [Konfigurace řízení spotřeby](configuring-power-management.md).  

## <a name="apply-power-plans-to-a-test-collection"></a>Použití schémat napájení pro testovací kolekci

Vždycky testujte účinek použití schématu řízení spotřeby na testovací kolekci počítačů, než schéma napájení použijete na větší kolekci počítačů.  

Když počítač vyloučíte z řízení spotřeby, všechna nastavení napájení se vrátí na původní hodnoty. U jednotlivých nastavení napájení nemůžete obnovit původní hodnoty.  

## <a name="apply-power-plan-settings-individually"></a>Použijte nastavení schématu napájení jednotlivě

Sledujte účinek použití každého nastavení napájení před tím, než použijete další. Tento proces zajistí, že každé nastavení má požadovaný efekt. Další informace o nastavení schématu napájení najdete v tématu [dostupná nastavení plánu řízení spotřeby](create-and-apply-power-plans.md#BKMK_Plans).  

## <a name="regularly-monitor-computers-for-multiple-power-plans"></a>Pravidelně monitorujte počítače pro více schémat napájení.

Řízení spotřeby obsahuje sestavu, která zobrazuje počítače, které mají více než jedno schéma napájení: **počítače s více schématy napájení**.

Pokud je počítač členem více kolekcí, z nichž každá používá jiná schémata napájení, platí následující chování:  

- **Schéma napájení**: Pokud u počítače použijete více hodnot nastavení napájení, použije se nejméně omezující hodnota.  

- **Čas probuzení**: Pokud pro stolní počítač použijete více časů probuzení, použije se čas nejbližší k půlnoci.  

Další informace najdete v tématu [počítače s více schématy napájení](monitor-and-plan-for-power-management.md#BKMK_Multiple).  

## <a name="save-or-export-power-management-information"></a>Uložit nebo exportovat informace o řízení spotřeby

Pokud spouštíte sestavy během fáze monitorování a dodržování předpisů, uložte nebo exportujte výsledky. Ponechte data pro pozdější porovnání v případě, Configuration Manager později data odebrat.  

Configuration Manager udržuje v databázi lokality následující informace o řízení spotřeby:

- Informace o řízení spotřeby využívané denními sestavami: 31 dní

- Informace o řízení spotřeby využívané měsíčními sestavami: 13 měsíců
