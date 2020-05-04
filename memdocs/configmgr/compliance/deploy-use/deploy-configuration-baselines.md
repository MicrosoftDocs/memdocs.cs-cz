---
title: Nasazení standardních hodnot konfigurace
titleSuffix: Configuration Manager
description: Nasaďte standardní hodnoty konfigurace a definujte nasazení standardních hodnot konfigurace a přidejte nebo odeberte standardní hodnoty konfigurace z nasazení.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9be8aaf3-075e-4acd-abd2-7459254e16e2
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 55b559f9b16eabfe2c2096497e6f63816b400803
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712334"
---
# <a name="how-to-deploy-configuration-baselines-in-configuration-manager"></a>Postup nasazení standardních hodnot konfigurace v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Standardní hodnoty konfigurace v Configuration Manager musí být nasazené do jedné nebo více kolekcí uživatelů nebo zařízení před tím, než klientská zařízení v těchto kolekcích budou moci vyhodnotit dodržování standardních hodnot konfigurace.  

Pomocí dialogového okna **Nasadit standardní hodnoty konfigurace** definujte nasazení standardních hodnot konfigurace, což kromě určení plánu vyhodnocení zahrnuje přidání standardních hodnot konfigurace do nasazení nebo jejich odebrání.  

## <a name="deploy-a-configuration-baseline"></a>Nasazení standardních hodnot konfigurace  

1.  V konzole Configuration Manager klikněte na **prostředky a dodržování předpisů** > **Nastavení** > dodržování předpisů**standardní hodnoty konfigurace**.  

3.  V seznamu **Standardní hodnoty konfigurace** vyberte standardní hodnoty konfigurace, které chcete nasadit, a pak na kartě **Domů** ve skupině **Nasazení** klikněte na **Nasadit**.  

4.  V dialogovém okně **Nasadit standardní hodnoty konfigurace** vyberte v seznamu **Dostupné standardní hodnoty konfigurace** standardní hodnoty konfigurace, které chcete nasadit. Kliknutím na **Přidat** je přidejte do seznamu **Vybrané standardní hodnoty konfigurace** .  

    > [!IMPORTANT]  
    >  Pokud změníte položku konfigurace, která byla přidaná do nasazených standardních hodnot konfigurace, u revidované položky se nevyhodnotí dodržování předpisů až do jejího dalšího naplánovaného času hodnocení.  

5.  Zadejte následující doplňkové informace:  

    -   **Napravit pravidla nesplňující požadavky** , je-li to podporováno – automaticky opraví všechna pravidla, která nejsou kompatibilní s rozhraní WMI (Windows Management Instrumentation) (WMI), registr, skripty a všechna nastavení pro mobilní zařízení zaregistrovaná pomocí Configuration Manager.  

    -   **Povolit nápravu mimo okno údržby** – Pokud je pro kolekci, do které nasazujete standardní hodnoty konfigurace, nakonfigurované časové období údržby, povolením této možnosti umožníte nastavení dodržování předpisů napravit hodnotu mimo časové období údržby. Další informace o časových obdobích údržby najdete v tématu [použití časových období](../../core/clients/manage/collections/use-maintenance-windows.md)údržby.  

6.  **Vygenerovat výstrahu** – nakonfiguruje výstrahu, která se vygeneruje, pokud kompatibilita standardních hodnot konfigurace je nižší než zadané procento podle zadaného data a času. Také můžete zvolit, zda chcete zasílat výstrahu do nástroje System Center Operations Manager.  

7.  **Kolekce** – Kliknutím na **Procházet** vyberte kolekci, do které chcete nasadit standardní hodnoty konfigurace.  

8.  **Zadejte plán vyhodnocení shody pro tyto standardní hodnoty konfigurace** Určuje plán, podle kterého budou nasazené standardní hodnoty konfigurace vyhodnocovány na klientských počítačích. Může se jednat o jednoduchý nebo vlastní plán.  

    > [!NOTE]  
    >  Pokud se standardní hodnoty konfigurace nasadí do počítače, vyhodnotí se dodržování předpisů během dvou hodin od naplánovaného času spuštění. Pokud se nasadí pro uživatele, vyhodnotí se dodržování předpisů při přihlášení uživatele.  

9. Kliknutím na tlačítko **OK** zavřete dialogové okno **Nasadit standardní hodnoty konfigurace** a vytvořte nasazení. Další informace o tom, jak monitorovat nasazení, najdete v tématu [monitorování nastavení dodržování předpisů](monitor-compliance-settings.md).  
