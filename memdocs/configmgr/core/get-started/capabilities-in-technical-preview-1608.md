---
title: Možnosti ve verzi Technical Preview 1608
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview pro Configuration Manager verze 1608.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 63e1df5e-637c-4b07-b7ec-95340f43a805
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: fd668760a6b5d1a16cfbb8549063da4f7e8a8b7d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074176"
---
# <a name="capabilities-in-technical-preview-1608-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1608 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1608. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview.      Před instalací této verze Technical Preview si Projděte úvodní téma, [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md), abyste se seznámili se základními požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.    


**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  




##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a>Vylepšení kroku pořadí úkolů Připravit klienta nástroje ConfigMgr pro zaznamenání  
Krok připravit klienta nástroje ConfigMgr teď zcela odebere klienta Configuration Manager, místo aby se odebraly jenom informace o klíči. Když pořadí úkolů nasadí zaznamenanou bitovou kopii operačního systému, nainstaluje se pokaždé Configuration Manager klienta.  


## <a name="improvements-to-software-center"></a>Vylepšení centra softwaru
* Na kartách **aplikace**a **Updates** **operační systémy** centra softwaru se nyní zobrazují informace o tom, jaký software byl nedávno přidán. Čísla v navigačním podokně ukazují, kolik nových částí softwaru je na jednotlivých kartách.
* Uživatelé teď můžou požádat o schválení aplikací a pak zobrazit historii žádostí v zobrazení **podrobností o aplikaci** v centru softwaru. Tlačítko **žádosti** v **podrobnostech o aplikaci** již není přesměrováno na webový katalog aplikací.

## <a name="improvements-to-asset-intelligence"></a>Vylepšení funkce Asset Intelligence
Přidali jsme pole do vlastností softwaru v inventáři, který umožňuje nastavit vztah nadřazenosti a podřízenosti k jinému softwaru. V seznamu software v inventáři pak můžete zobrazit nadřazený software jakéhokoli softwaru a také skrýt veškerý podřízený software.

### <a name="configure-a-parent-to-child-relationship"></a>Konfigurace vztahu nadřízený-podřízený
  1. Pokud chcete nastavit nadřazený software, v uzlu software v inventáři klikněte pravým tlačítkem na položku softwaru v seznamu **software v inventáři** a vyberte **vlastnosti**.
  2. V dialogovém okně, které se otevře, vyberte software, který chcete nastavit jako nadřazený software pro počáteční výběr.

### <a name="filter-the-software-display"></a>Filtrovat displej softwaru
Po definování nadřazených a podřízených vztahů můžete zobrazení filtrovat tak, aby zobrazovalo pouze software, který je nadřazený nebo který nemá žádnou definovanou relaci. Tím se skryje veškerý software, který je nastavený jako podřízený jiný software v inventáři. Postupujte následovně:
   1. Pro panel hledání vyberte možnost **Přidat kritéria** .
   2. Vyberte **nadřazený software** a pak změňte hodnotu kritéria na **prázdnou**a pak klikněte na **Hledat**.

Zobrazení teď zobrazuje jenom nadřazené softwarové položky nebo software, který nemá žádné definované relace. Software, který je pouze podřízeným jiným názvem, se nezobrazí.

## <a name="remote-control-keyboard-translation"></a>Překlad klávesnice pro vzdálené řízení
V minulosti Configuration Manager přenesli klíčovou pozici z umístění prohlížeče do umístění sdílejícího. To bylo problematické při konfiguracích klávesnice, které se lišily od prohlížeče ke sdílejícímu. Například prohlížeč s anglickou klávesnicí by měl napsat "A", ale Francouzská klávesnice sdílejícía poskytne "Q". Měníme výchozí chování tak, aby se samotný znak přenesl z klávesnice prohlížeče na sdílející a co prohlížeč zamýšlí napsat, dorazí na sdílejícího.

Toto chování může být vypnuto prohlížečem, pokud chtějí psát podle uspořádání klávesnice sdílejícího. Chcete-li změnit chování, v **Configuration Manager vzdálené řízení**klikněte na tlačítko **Akce**a vyberte možnost **Povolit překlad klávesnice** pro přenos pozice klíče.

> [!NOTE]
>
> Speciální klíče, například ~! # @ $%, nebudou přeloženy správně.
