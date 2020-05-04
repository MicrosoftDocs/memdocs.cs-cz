---
title: Kontrolní seznam správce pro řízení spotřeby
titleSuffix: Configuration Manager
description: Pomocí kontrolního seznamu Správce vám pomůžete naplánovat a implementovat řízení spotřeby v Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 94e42cbe-9df8-4228-a04e-0ad7626180ca
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 039ebf73fba9850b8479bfabab6ab928b7d6f2df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715281"
---
# <a name="administrator-checklist-for-power-management-in-configuration-manager"></a>Kontrolní seznam správce pro řízení spotřeby v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento kontrolní seznam správce poskytuje doporučené kroky pro použití Configuration Manager řízení spotřeby ve vaší organizaci.  

## <a name="configuring-power-management"></a>Konfigurování řízení spotřeby  
 Pomocí těchto kroků můžete nakonfigurovat svou hierarchii pro shromažďování informací o řízení spotřeby z klientských počítačů.  

> [!IMPORTANT]  
>  Nepoužívejte na počítače v hierarchii schémata napájení, dokud jste neshromáždili a nezanalyzovali data napájení z klientských počítačů. Pokud použijete nové nastavení řízení spotřeby pro počítače bez dřívějšího prozkoumání stávajícího nastavení, může to vést ke zvýšení spotřeby energie.  

|Úkol|Podrobnosti|  
|----------|-------------|  
|Seznamte se s koncepty řízení spotřeby v knihovně dokumentace Configuration Manager.|Viz [Úvod do řízení spotřeby](introduction-to-power-management.md).|  
|Seznamte se s požadavky řízení spotřeby v knihovně dokumentace Configuration Manager.|Viz [předpoklady pro řízení spotřeby](prerequisites-for-power-management.md).|  
|Přečtěte si informace o osvědčených postupech pro řízení spotřeby.|Podívejte se [na osvědčené postupy pro řízení spotřeby](best-practices-for-power-management.md).|  
|Nakonfigurujte své kolekce pro správu spotřeby energie z počítačů ve vašem prostředí.|Použijte **kolekci pro vytváření sestav základních dat**, **kolekci pro vytváření sestav základních dat**, **kolekci počítačů neschopných řízení spotřeby**, kolekce **počítačů, do kterých se budou používat schémata napájení**, kolekce počítačů, **do kterých**se budou používat schémata napájení, a kolekce počítačů se **spuštěným systémem Windows Server** , které vám pomůžou spravovat nastavení napájení pro počítače ve vaší hierarchii. Můžete vytvořit více kolekcí a použít pro jednotlivé kolekce různá schémata napájení.|  
|Povolte řízení spotřeby.|Před zahájením používání musíte řízení spotřeby povolit a konfigurovat požadovaná nastavení klienta. Další informace najdete v tématu [Konfigurace řízení spotřeby](configuring-power-management.md).|  
|Shromážděte informace o řízení spotřeby z klientských počítačů.|Data řízení spotřeby hlásí klienti prostřednictvím Configuration Manager inventáře hardwaru. V závislosti na plánu inventáře hardwaru, který jste nakonfigurovali, může trvat nějakou dobu, než se načte inventář ze všech klientských počítačů.|  

## <a name="monitoring-and-planning-phase"></a>Fáze monitorování a plánování  

|Úkol|Podrobnosti|  
|----------|-------------|  
|Spusťte sestavu **Aktivita počítače**.|Sestava **Aktivita počítače** zobrazí graf s informacemi o aktivitě monitorů, počítačů a uživatelů pro zadanou kolekci v zadaném období. Tato sestava obsahuje odkaz na sestavu **Podrobnosti o aktivitě počítače**, která zobrazuje funkce režimu spánku a probuzení z režimu spánku u počítačů v zadané kolekci. Další informace najdete v tématu [monitorování a plánování řízení spotřeby](monitor-and-plan-for-power-management.md).|  
|Spusťte sestavu **Spotřeba energie** nebo **Spotřeba energie na den**.|Sestavy **Spotřeba energie** a **Spotřeba energie na den** zobrazí celkovou měsíční spotřebu energie v kilowatthodinách (kWh) pro zadanou kolekci za zadané časové období. Další informace najdete v tématu [monitorování a plánování řízení spotřeby](monitor-and-plan-for-power-management.md).|  
|Spusťte sestavu **ekologický dopad** nebo **ekologický dopad na den**.|Sestavy **Ekologický dopad** a **Ekologický dopad na den** zobrazí graf emisí oxidu uhličitého (CO2) ušetřených zadanou kolekcí v zadaném časovém období. Další informace najdete v tématu [monitorování a plánování řízení spotřeby](monitor-and-plan-for-power-management.md).|  
|Spusťte sestavu **Náklady na energii** nebo **Náklady na energii za den**.|Sestavy **Náklady na energii** a **Náklady na energii na den** zobrazí celkové náklady na energii během zadaného časového období. Další informace najdete v tématu [monitorování a plánování řízení spotřeby](monitor-and-plan-for-power-management.md).|  
|Spusťte sestavu **Možnosti napájení**.|Sestava **Možnosti napájení** zobrazí možnosti řízení spotřeby u počítačů v zadané kolekci. Další informace najdete v tématu [monitorování a plánování řízení spotřeby](monitor-and-plan-for-power-management.md).|  
|Spusťte sestavu **Nastavení napájení**.|Sestava **Nastavení napájení** zobrazí souhrnný seznam aktuálních nastavení napájení, které používají počítače v zadané kolekci. Další informace najdete v tématu [monitorování a plánování řízení spotřeby](monitor-and-plan-for-power-management.md).|  
|Vylučte všechny požadované kolekce počítačů z řízení spotřeby.|Viz [Konfigurace řízení spotřeby](configuring-power-management.md).|  

> [!IMPORTANT]  
>  Nezapomeňte uložit informace ze sestav řízení spotřeby vytvořených během fáze monitorování a plánování. Můžete porovnat tato data s informacemi řízení spotřeby generovanými během fáze vynucování a dodržování předpisů, což vám pomůže vyhodnotit spotřebu, náklady na energie a úspory ekologických dopadů plynoucí z použití schématu napájení na počítače ve vaší hierarchii.  

## <a name="enforcement-phase"></a>Fáze vynucení  

|Úkol|Podrobnosti|  
|----------|-------------|  
|Vyberte existující schémata napájení nebo vytvořte nová schémata napájení pro kolekce počítačů ve vaší organizaci.|Přečtěte si téma [Vytvoření a použití schémat napájení](create-and-apply-power-plans.md).|  
|Použijte tato schémata napájení na počítače.|Přečtěte si téma [Vytvoření a použití schémat napájení](create-and-apply-power-plans.md).|  

## <a name="compliance-phase"></a>Fáze dodržování předpisů  

|Úkol|Podrobnosti|  
|----------|-------------|  
|Spusťte sestavu **Aktivita počítače**.|Sestava **Aktivita počítače** zobrazí graf s informacemi o aktivitě monitorů, počítačů a uživatelů pro zadanou kolekci v zadaném období. Tato sestava obsahuje odkaz na sestavu **Podrobnosti o aktivitě počítače**, která zobrazuje funkce režimu spánku a probuzení z režimu spánku u počítačů v zadané kolekci. Další informace najdete v tématu [monitorování a plánování řízení spotřeby](monitor-and-plan-for-power-management.md).|  
|Spusťte sestavu **Spotřeba energie** nebo **Spotřeba energie na den**.|Sestavy **Spotřeba energie** a **Spotřeba energie na den** zobrazí celkovou měsíční spotřebu energie v kilowatthodinách (kWh) pro zadanou kolekci za zadané časové období. Další informace najdete v tématu [monitorování a plánování řízení spotřeby](monitor-and-plan-for-power-management.md).|  
|Spusťte sestavu **Ekologický dopad** nebo **Ekologický dopad na den**.|Sestavy **Ekologický dopad** a **Ekologický dopad na den** zobrazí graf emisí oxidu uhličitého (CO2) ušetřených zadanou kolekcí v zadaném časovém období. Další informace najdete v tématu [monitorování a plánování řízení spotřeby](monitor-and-plan-for-power-management.md).|  
|Spusťte sestavu **Náklady na energii** nebo **Náklady na energii za den**.|Sestavy **Náklady na energii** a **Náklady na energii na den** zobrazí celkové náklady na energii během zadaného časového období. Další informace najdete v tématu [monitorování a plánování řízení spotřeby](monitor-and-plan-for-power-management.md).|  

## <a name="troubleshooting"></a>Řešení potíží  

|Úkol|Podrobnosti|  
|----------|-------------|  
|Pokud počítače ve vaší hierarchii nepřešly do režimu spánku nebo hibernace, spusťte sestavu **Sestava režimu spánku** a zobrazte možné příčiny.|**Sestava režimu spánku** zobrazí seznam běžných příčin, které počítačům zabránily v přechodu do režimu spánku nebo hibernace, a počet počítačů ovlivněných jednotlivými příčinami v zadaném období. Další informace najdete v tématu [monitorování a plánování řízení spotřeby](monitor-and-plan-for-power-management.md).|  
|Pokud se pro počítač používá víc schémat napájení, použije se nejméně omezující schéma napájení. Spusťte sestavu **Počítače s více schématy napájení** a zobrazte počítače, pro které se používá víc schémat napájení.|Viz **počítače s více schématy napájení** v tématu [monitorování a plánování řízení spotřeby](monitor-and-plan-for-power-management.md).|  
