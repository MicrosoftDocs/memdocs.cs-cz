---
title: Osvědčené postupy pro kolekce
titleSuffix: Configuration Manager
description: Získejte osvědčené postupy pro kolekce v Configuration Manager.
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7e3e7b108ef48b218ee9d6a31064606b40a68fea
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714287"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Osvědčené postupy pro kolekce v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pro kolekce v Configuration Manager použijte následující osvědčené postupy.  

## <a name="dont-use-incremental-updates-with-many-collections"></a><a name="bkmk_incremental"></a>Nepoužívejte přírůstkové aktualizace s mnoha kolekcemi

Při povolení volby **Pro tuto kolekci použijte přírůstkové aktualizace** může tato konfigurace, pokud je povolená pro mnoho kolekcí, způsobit zpoždění při vyhodnocování. Prahová hodnota je přibližně 200 kolekcí ve vaší hierarchii. Přesné číslo závisí na následujících faktorech:  

- Celkový počet kolekcí  

- Frekvence přidávání a měnění nových prostředků v hierarchii  

- Počet klientů v hierarchii  

- Složitost pravidel členství v kolekcích ve vaší hierarchii  

## <a name="maintenance-window-size-for-software-updates"></a>Velikost časového období údržby pro aktualizace softwaru

Můžete nakonfigurovat časové intervaly pro správu a údržbu pro kolekce zařízení a omezit tak dobu, po kterou Configuration Manager můžou na tato zařízení instalovat software. Pokud nakonfigurujete časové intervaly pro správu a údržbu, aby byla příliš malá, klient nebude moci instalovat důležité aktualizace softwaru, což klientovi ponechá zranitelnost vůči útokům, které může aktualizace softwaru zmírnit.

> [!Tip]
> Důležité informace, které je potřeba vzít v úvahu při plánování oken údržby:
>
> - Výchozí maximální doba běhu aktualizace softwaru je 60 minut.
> - Když Configuration Manager vypočítá, jestli se aktualizace může nainstalovat, přidá pět minut do maximální doby běhu pro restartování.
> - Zbývající doba trvání časového období údržby musí být delší než maximální doba běhu aktualizace softwaru plus pět minut.
