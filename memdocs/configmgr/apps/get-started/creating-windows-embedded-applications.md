---
title: Vytváření aplikací pro Windows Embedded
titleSuffix: Configuration Manager
description: V této části najdete informace, které je nutné vzít v úvahu při vytváření a nasazování aplikací pro zařízení se systémem Windows Embedded.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 16acfd63-0c40-424c-82f4-8c63f7f1c30b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bec9765e5152863bb8b55a0b75f1e5c2fc580550
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710493"
---
# <a name="create-windows-embedded-applications-with-configuration-manager"></a>Vytváření aplikací pro Windows Embedded pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Kromě dalších Configuration Manager požadavků a postupů pro vytváření aplikací musíte při vytváření a nasazování aplikací pro zařízení s Windows Embedded vzít v úvahu taky následující skutečnosti.  

## <a name="general-considerations"></a>Obecné aspekty  

-   Když nasadíte aplikace na zařízení se systémem Windows Embedded, která mají povolený filtr zápisu, můžete určit, jestli se má při nasazení aplikace zakázat filtr zápisu na zařízení. Po nasazení aplikace pak můžete zvolit, že se má filtr zápisu restartovat. Pokud není filtr zápisu zakázán, bude software nasazen do dočasného překrytí. To znamená, že pokud jiné nasazení nevynutí trvalé změny, po restartu zařízení již nebude software nainstalován.  

-   Pokud nasazujete aplikaci na zařízení se systémem Windows Embedded, zkontrolujte, že je zařízení součástí kolekce, která má nakonfigurované okno údržby. Tato funkce umožňuje řídit, kdy je filtr zápisu zakázán a povolen a kdy se zařízení restartuje.  

-   Nastavení, které řídí chování filtru zápisu, je zaškrtávací políčko s názvem **Potvrdit změny v den konečného termínu nebo během okna údržby (vyžaduje restart)**.  

## <a name="tips-for-deploying-applications"></a>Tipy pro nasazení aplikací  

**Místo dostupných aplikací pro zařízení se systémem Windows Embedded s povolenými filtry zápisu použijte požadované aplikace.** Vzhledem k tomu, že uživatelé nemohou instalovat aplikace z centra softwaru na zařízení se systémem Windows Embedded s povolenými filtry zápisu, vždy nasaďte aplikace s účelem nasazení **požadováno** , nikoli k **dispozici** pro tato zařízení. Obvykle se nejedná o problém, protože počítače s operačním systémem Windows Embedded často spouštějí jednu aplikaci, která musí běžet stejným způsobem pro více uživatelů. Tato zařízení jsou proto vysokoúrovňově spravována a uzamčena oddělením IT. Požadované aplikace představují vhodné řešení pro takový scénář.

 Pokud však uživatelé zařízení se systémem Windows Embedded s povolenými filtry zápisu používají více aplikací, informujte je o následujících omezeních:  

-   Uživatelé nemohou instalovat požadovaný software z Centra softwaru.  

-   Uživatelé nemůžou měnit svou pracovní dobu na kartě Možnosti Centra softwaru.  

-   Uživatelé nemohou odložit instalaci požadované aplikace.  

Uživatelé s nízkými právy se navíc během období údržby nemůžou přihlásit, pokud Configuration Manager potvrzování změn instalací a aktualizací softwaru. Během tohoto období se uživatelům zobrazí zpráva s informací, že zařízení není k dispozici z důvodu servisu.  

**Nesaďte aplikace do zařízení se systémem Windows Embedded s povolenými filtry zápisu, pokud aplikace vyžaduje, aby si licenční podmínky přijal uživatel.** Pokud jsou filtry zápisu zakázané, takže Configuration Manager můžou instalovat software do integrovaných zařízení, uživatelé s nízkými právy se k zařízení nemohou přihlásit. Pokud instalace vyžaduje, aby uživatel vyjádřil souhlas s licenčními podmínkami, nebude možné souhlas vyjádřit a instalace se nezdaří. Ověřte, že do zařízení se systémem Windows Embedded nenasazujete software, jehož instalace vyžaduje interakci uživatele. Tyto operační systémy můžete odfiltrovat pomocí seznamu Použitelné platformy.  
