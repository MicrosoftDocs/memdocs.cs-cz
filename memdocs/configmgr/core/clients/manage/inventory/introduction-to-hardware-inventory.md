---
title: 'Inventář hardwaru '
titleSuffix: Configuration Manager
description: Seznámení s inventářem hardwaru v Configuration Manager.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7baf6bad80fbccb698278602c519f3a75b8a4b5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714406"
---
# <a name="introduction-to-hardware-inventory-in-configuration-manager"></a>Úvod do inventáře hardwaru v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Inventář hardwaru v nástroji Configuration Manager slouží ke shromažďování informací o konfiguraci hardwaru klientských zařízení ve vaší organizaci. Chcete-li shromáždit inventář hardwaru, je nutné vybrat nastavení **Povolit inventář hardwaru u klientů** v nastavení klienta.  

 Po povolení inventáře hardwaru a spuštění cyklu inventáře hardwaru klient pošle informace do bodu správy v lokalitě klienta. Bod správy poté přesměruje informace o inventáři na Server Configuration Manager lokality, který ukládá informace o inventáři do databáze lokality. Inventář hardwaru běží na klientech podle plánu, který určíte v nastavení klienta.  
## <a name="view-hardware-inventory"></a>Zobrazit inventář hardwaru 

 K zobrazení dat inventáře hardwaru, které Configuration Manager shromažďuje, můžete použít několik metod:  

- [Vytvořte dotazy, které vrátí zařízení, která jsou založená na konkrétní hardwarové konfiguraci](../../../../core/servers/manage/introduction-to-queries.md).  

- [Vytváření kolekcí založených na dotazech, které jsou založeny na konkrétní hardwarové konfiguraci](../../../../core/clients/manage/collections/introduction-to-collections.md). Členství v kolekcích založených na dotazech se budou automaticky aktualizovat podle plánu. Kolekce můžete použít pro několik úloh, včetně nasazení softwaru.

- [Spouštění sestav, které zobrazují konkrétní podrobnosti o konfiguracích hardwaru ve vaší organizaci](../../../servers/manage/introduction-to-reporting.md).

- [Pomocí Průzkumník prostředků](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) můžete zobrazit podrobné informace o inventáři hardwaru shromážděného z klientských zařízení.

Když inventář hardwaru běží na klientském zařízení, první data inventáře, která klient odešle, obsahují vždy úplný inventář. Další data inventáře obsahují jenom informace o rozdílovém inventáři. Server lokality zpracovává informace o rozdílovém inventáři v přijatém pořadí. Pokud chybí rozdílové informace pro klienta, server lokality odmítne další rozdílové informace a nasměruje klienta, aby spustil úplný cyklus inventarizace.  

 Configuration Manager poskytuje omezené podpory pro počítače s více operačními systémy. Configuration Manager mohou zjišťovat počítače s více operačními systémy, ale vrací informace o inventáři pouze z operačního systému, který je aktivní při spuštění cyklu inventarizace.  

> [!NOTE]  
>  Informace o používání inventáře hardwaru u klientů se systémy Linux a UNIX najdete v tématu [inventář hardwaru pro Linux a UNIX](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  

## <a name="extending-configuration-manager-hardware-inventory"></a>Rozšíření inventáře hardwaru pomocí nástroje Configuration Manager  
 Kromě integrovaného inventáře hardwaru v Configuration Manager můžete k rozšíření inventáře hardwaru použít taky jednu z těchto metod:  

- Povolte, zakažte, přidejte a odeberte třídy inventáře pro inventář hardwaru z konzoly Configuration Manager.  
- Soubory NOIDMIF můžete použít ke shromažďování informací o klientských zařízeních, která nemůžou být v inventáři Configuration Manager. Můžete například chtít shromažďovat pro zařízení informace o evidenčním čísle, které existuje jenom jako štítek na zařízení. Soubor NOIDMIF se automaticky přidruží klientskému zařízení, ze kterého byl shromážděný.  
- Soubory IDMIF můžete použít ke shromažďování informací o prostředcích, které nejsou přidružené k Configuration Manager klientovi, například projektory, kopírky a síťové tiskárny.


## <a name="next-steps"></a>Další kroky
Další informace o použití těchto metod pro rozšiřování Configuration Manager inventáře hardwaru najdete v tématu [Konfigurace inventáře hardwaru](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
