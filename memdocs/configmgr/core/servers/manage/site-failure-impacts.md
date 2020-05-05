---
title: Dopady selhání lokality
titleSuffix: Configuration Manager
description: Pochopení vlivu různých selhání na Configuration Manager lokalitě.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6f0e08f8-f2e1-4823-90f6-7b1f4341eb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf56aee2e9f73ea8c3c69737c749f2a599e1ac37
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723891"
---
# <a name="site-failure-impacts-in-configuration-manager"></a>Dopad na selhání lokality v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Server lokality a některý z dalších systémů lokality mohou selhat a způsobit ztrátu služeb, které pravidelně poskytují. Pokud nainstalujete více systémů lokality do stejného počítače a tento počítač nebude úspěšný, všechny služby, které tyto systémy lokality pravidelně poskytovaly, již nebudou k dispozici.

Součástí procesu plánování by měl být porozumět dopadu na službu, kterou poskytujete vaší organizaci. Vzhledem k tomu, že každý systém lokality v lokalitě nástroje poskytuje různé funkce, dopad selhání na lokalite se liší v závislosti na roli systému lokality, u které došlo k chybě. 

Využijte [Možnosti vysoké dostupnosti](../deploy/configure/high-availability-options.md) , které vám pomůžou zmírnit selhání jakéhokoli jednoho systému. Také můžete naplánovat a vyzkoušet strategii [zálohování a obnovení](backup-and-recovery.md) , která zkracuje dobu, po kterou služba není k dispozici.

V následujících částech je popsán dopad, pokud zadaný systém lokality není funkční:


### <a name="site-server"></a>Server lokality

- Není možné spravovat žádnou správu lokality. Konzolu nelze připojit k lokalitě nástroje.  

- Bod správy shromažďuje informace o klientovi a ukládá je do mezipaměti, dokud se server lokality nevrátí do online režimu.  

- Uživatelé můžou spouštět existující nasazení a klienti si můžou stáhnout obsah z distribučních bodů.  


### <a name="site-database"></a>Databáze lokality

- Není možné spravovat žádnou správu lokality.  

- Pokud klient Configuration Manager již má přiřazení zásady s novými zásadami a pokud bod správy ukládá do mezipaměti tělo zásady, může klient vytvořit požadavek těla zásad a obdržet odpověď těla zásad. Lokalita ale nemůže obsluhovat žádné nové žádosti o přiřazení zásady.  

- Klienti můžou spouštět nasazení, jenom pokud už tuto zásadu obdrželi a přidružené zdrojové soubory už jsou uložené místně v klientovi.  


### <a name="management-point"></a>Bod správy

- I když můžete vytvořit nová nasazení, klienti je neobdrží, dokud je bod správy online.  

- Klienti stále shromažďují informace o inventáři, měření softwaru a stavu. Tato data ukládají místně, dokud není k dispozici bod správy.  

- Klienti můžou spouštět nasazení, jenom pokud už tuto zásadu obdrželi a přidružené zdrojové soubory už jsou uložené místně v klientovi.  


### <a name="distribution-point"></a>Distribuční bod

- Klienti Configuration Manager mohou spustit nasazení, pouze pokud jsou přidružené zdrojové soubory již místně staženy nebo jsou k dispozici v partnerském zdroji.

