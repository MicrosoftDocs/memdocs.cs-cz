---
title: Inventář softwaru
titleSuffix: Configuration Manager
description: Seznámení s inventářem softwaru v Configuration Manager.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 07b6f0108125c97128ddc88b663b0af4dabadbe7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714392"
---
# <a name="introduction-to-software-inventory-in-configuration-manager"></a>Úvod do inventáře softwaru v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pomocí inventáře softwaru můžete shromažďovat informace o souborech v klientských zařízeních. Inventář softwaru může taky shromažďovat soubory z klientských zařízení a ukládat je na serveru lokality. Inventář softwaru se shromáždí po výběru nastavení **Povolit inventář softwaru u klientů** v nastavení klienta. Operaci můžete také naplánovat v nastavení klienta.  

Po povolení inventáře softwaru a klienti spouštějící cyklus inventáře softwaru odesílá klient informace do bodu správy v lokalitě klienta. Bod správy poté přepošle informace o inventáři do serveru Configuration Manager lokality, který ukládá informace v databázi lokality.

 Existuje několik způsobů, jak zobrazit data inventáře softwaru:  

- [Vytváření dotazů](../../../../core/servers/manage/create-queries.md) , které vracejí zařízení se zadanými soubory   

- Vytvořte [kolekce založené na dotazech](../../../../core/clients/manage/collections/introduction-to-collections.md) , které obsahují zařízení se zadanými soubory.   

- [Spuštění sestav](../../../servers/manage/introduction-to-reporting.md) , které poskytují podrobné informace o souborech na zařízeních.

- Použijte [Průzkumník prostředků](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) k prohlédnutí podrobných informací o souborech, které byly v inventáři a shromažďovány z klientských zařízení.   

 Když inventář softwaru běží na klientském zařízení, první sestava představuje úplný inventář. Následné sestavy obsahují pouze informace o rozdílech v inventáři. Server lokality zpracovává rozdílové informace v přijatém pořadí. Pokud chybí rozdílové informace pro klienta, server lokality odmítne další rozdílové informace a nasměruje klienta na spuštění úplného inventáře.  

 Configuration Manager můžou zjišťovat počítače s více operačními systémy, ale vrátí jenom informace o inventáři z operačního systému, který je v době inventarizace aktivní.  
