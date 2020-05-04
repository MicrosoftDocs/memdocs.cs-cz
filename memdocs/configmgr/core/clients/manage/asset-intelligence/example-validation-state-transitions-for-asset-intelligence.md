---
title: Příklad přechodů mezi stavy ověření
titleSuffix: Configuration Manager
description: Podívejte se na příklady přechodů stavu ověření pro funkce Asset Intelligence v Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6230a6e5-a1f6-459b-84f1-07fbde0e70f0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2af9243d6720d5821c641e5c80589457a33b638e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714175"
---
# <a name="example-validation-state-transitions-for-asset-intelligence"></a>Příklady přechodů mezi stavy ověření pro Asset Intelligence

*Platí pro: Configuration Manager (Current Branch)*

Funkce Asset Intelligence stavy ověření v Configuration Manager nejsou statické a mohou se měnit z akcí správy, které jsou potřeba pro ovlivnění dat uložených v katalogu funkce Asset Intelligence. V tomto tématu najdete příklady možných přechodů ke stavu ověření.

##  <a name="uncategorized-catalog-item-is-categorized-by-the-administrative-user"></a><a name="BKMK_UncategorizedIsCategorized"></a> Položka dříve nezařazená do kategorie je administrativním uživatelem zařazena.  

|**Přechod stavu**|**Popis přechodu stavu**|  
|--------------------------|--------------------------------------|  
|**Nezařazeno do kategorie**|Inventarizovaný softwarový titul, který nebyl dříve zařazený do kategorií nástrojem System Center Online nebo který administrativní uživatel zařadil do katalogu Asset Intelligence.|  
|**Nezařazeno do kategorie** na **Definovánouživatelem**|Položka dříve nezařazená do kategorie je administrativním uživatelem zařazena.|  

##  <a name="categorized-catalog-item-is-recategorized-by-the-administrative-user"></a><a name="BKMK_CategorizedIsReCategorized"></a> Položka katalogu zařazená do kategorie je administrativním uživatelem přeřazená do jiné kategorie.  

|**Přechod stavu**|**Popis přechodu stavu**|  
|--------------------------|--------------------------------------|  
|**Ověřeno**|Položka katalogu byla definovaná výzkumníky služby System Center Online a zařazená v katalogu Asset Intelligence.|  
|**Ověřeno** na **Definováno uživatelem**|Ověřená položka katalogu je administrativním uživatelem přeřazená do jiné kategorie.|  

> [!NOTE]  
>  Protože kategorizace informací získaných službou System Center Online je uložená v databázi a nelze ji odstranit, administrativní uživatel se může ke kategorizaci podle služby System Center Online později kdykoli vrátit.  

##  <a name="user-defined-catalog-item-is-recategorized-by-system-center-online"></a><a name="BKMK_UserDefinedIsRecategorized"></a>Uživatelem definovaná položka katalogu je službou System Center Online přeřazená do kategorie  

|**Přechod stavu**|**Popis přechodu stavu**|  
|--------------------------|--------------------------------------|  
|**Nezařazeno do kategorie**|Do katalogu Asset Intelligence byl vložený inventarizovaný softwarový titul, který nebyl předtím zařazený do kategorie službou System Center Online nebo administrativním uživatelem.|  
|**Definováno uživatelem**|Položka dříve nezařazená do kategorie je administrativním uživatelem zařazena.|  
|**Definováno uživatelem** na **Aktualizovatelné**|Uživatelem definovaná položka katalogu byla při následné ruční hromadné aktualizaci katalogu Asset Intelligence službou System Center Online kategorizovaná jinak.<br /><br /> Administrativní uživatel může pomocí dialogového okna **Řešení konfliktů podrobností o softwaru** rozhodnout, jestli chce použít novou kategorizaci, nebo předchozí hodnotu definovanou uživatelem.|  
|**Aktualizovatelné** na **Ověřeno**|Administrativní uživatel v dialogovém okně **Řešení konfliktů podrobností o softwaru** použije novou kategorizaci získanou ze služby System Center Online během předchozí aktualizace katalogu.|  
|– nebo –||  
|**Aktualizovatelné** na **Definováno uživatelem**|Administrativní uživatel v dialogovém okně **Řešení konfliktů podrobností o softwaru** použije předchozí uživatelem definovanou hodnotu.|  

> [!NOTE]  
>  Protože kategorizace informací získaných službou System Center Online je uložená v databázi a nelze ji odstranit, administrativní uživatel se může ke kategorizaci podle služby System Center Online později kdykoli vrátit.  

##  <a name="uncategorized-catalog-item-is-submitted-to-system-center-online-for-categorization"></a><a name="BKMK_UncategorizedIsSubmitted"></a>Položka katalogu Nezařazeno do kategorie se odešle službě System Center Online ke kategorizaci.  

|**Přechod stavu**|**Popis přechodu stavu**|  
|--------------------------|--------------------------------------|  
|**Nezařazeno do kategorie**|Do databáze Asset Intelligence byl vložený inventarizovaný softwarový titul, který nebyl předtím zařazený do kategorie službou System Center Online nebo administrativním uživatelem.|  
|**Nezařazeno do kategorie** na **Čeká**|Položka nezařazená do kategorie se administrativním uživatelem odešle službě System Center Online ke kategorizaci.|  
|**Čeká** na **Ověřeno**|Položka je zařazená do kategorie podle služby System Center Online. Administrativní uživatel naimportuje položku do katalogu Asset Intelligence pomocí hromadné aktualizace katalogu nebo synchronizace katalogu Asset Intelligence. Obě možnosti jsou dostupné při použití Instalace role serveru Bod synchronizace katalogu Asset Intelligence.|  

##  <a name="user-defined-catalog-item-is-submitted-to-system-center-online-for-categorization"></a><a name="BKMK_UserDefinedIsSubmitted"></a>Uživatelem definovaná položka katalogu se odešle službě System Center Online ke kategorizaci.  

|**Přechod stavu**|**Popis přechodu stavu**|  
|--------------------------|--------------------------------------|  
|**Nezařazeno do kategorie**|Do databáze Asset Intelligence byl vložený inventarizovaný softwarový titul, který nebyl předtím zařazený do kategorie službou System Center Online nebo administrativním uživatelem.|  
|**Definováno uživatelem**|Zařadili jste do katalogu dosud nezařazenou položku.|  
|**Definováno uživatelem** na **Čeká**|Odešlete uživatelem definovanou položku katalogu službě System Center Online ke kategorizaci.|  
|**Čeká** na **Aktualizovatelné**|Uživatelem definovaná položka katalogu byla službou System Center Online při následné synchronizaci katalogu kategorizovaná jinak. Pomocí akce **Vyřešit konflikt** můžete rozhodnout, jestli použijete nové kategorizační informace nebo předchozí uživatelem definovanou hodnotu. Další informace o řešení konfliktů najdete v tématu [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  
|**Aktualizovatelné** na **Ověřeno**|Použijete akci **Vyřešit konflikt** a vyberte nové informace o kategorizaci přijatých ze služby System Center Online během předchozí aktualizace katalogu. Další informace o řešení konfliktů najdete v tématu [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  
|– nebo –||  
|**Aktualizovatelné** na **Definováno uživatelem**|Použijete akci **Vyřešit konflikt** a vyberete předchozí hodnotu definovanou uživatelem. Další informace o řešení konfliktů najdete v tématu [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  

> [!NOTE]  
>  Protože kategorizace informací získaných službou System Center Online je uložená v databázi a nelze ji odstranit, můžete se ke kategorizaci podle služby System Center Online později kdykoli vrátit.  
