---
title: Upgradovat LTSB na aktuální větev
titleSuffix: Configuration Manager
description: Přečtěte si, jak převést lokalitu dlouhodobého LTSB (Long-Term Servicing Branch) na aktuální pobočku.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b9f79eae1eee29fee33a9a841a303aae55686c55
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722953"
---
# <a name="upgrade-the-long-term-servicing-branch-to-the-current-branch"></a>Upgrade větve dlouhodobé údržby na aktuální větev

*Platí pro: System Center Configuration Manager (větev dlouhodobé údržby)*

V tomto tématu se dozvíte, jak upgradovat (převést) lokalitu a hierarchii, které spouštějí LTSB (Long-Term Servicing Branch) Configuration Manager k Current Branch.

Pokud máte aktuální smlouvu Software Assurance (nebo podobná licenční práva), která vám uděluje práva k používání Current Branch, můžete převést svoji instalaci z LTSB na Current Branch.  Jedná se o jednosměrný převod, protože neexistuje žádná podpora pro převod Current Branchho webu na LTSB.

Pokud máte více lokalit, stačí pouze převést lokalitu nejvyšší úrovně ve vaší hierarchii. Po převedení lokality nejvyšší úrovně:
- Podřízené primární lokality se automaticky převedou.
- Sekundární lokality je nutné ručně aktualizovat v konzole Configuration Manager.

## <a name="run-setup-to-convert-the-long-term-servicing-branch"></a>Spusťte instalační program a převeďte větev dlouhodobé údržby.
V lokalitě nejvyšší úrovně ve vaší hierarchii můžete spustit instalační program Configuration Manager z kvalifikovaného média směrného plánu a vybrat možnost **Údržba lokality**.  Až se zobrazí stránka licencování, vyberte možnost pro Current Branch a dokončete průvodce.

Když se váš web převede na Current Branch, budou k dispozici dříve nedostupné funkce a možnosti k použití.

> [!NOTE]  
> Kvalifikování základního média je médium, které má verzi, která se rovná nebo je vyšší než instalace LTSB.

Například vzhledem k tomu, že LTSB je založen na verzi 1606, nemůžete použít médium standardních hodnot 1511 k převedení na Current Branch. Místo toho spusťte instalaci ze stejného základního média 1606, které jste použili k instalaci webu LTSB, a vyberte možnost licencování pro Current Branch.  Alternativně, pokud byl vydán pozdější základ Current Branch, můžete spustit instalační program z tohoto základního média.

Seznam základních verzí najdete v tématu základní verze **a verze aktualizací** v článku [aktualizace pro Configuration Manager](../servers/manage/updates.md).

## <a name="use-the-configuration-manager-console-to-convert-the-long-term-servicing-branch"></a>Použití konzoly Configuration Manager k převedení dlouhodobé větve údržby
Pokud vaše lokalita používá LTSB, můžete použít následující možnost v konzole Configuration Manager k převedení na Current Branch:

 1. V konzole nástroje klikněte na **Správa** > **Konfigurace** > lokality**lokality**a pak otevřete **Nastavení hierarchie**.  

 2. V **Nastavení hierarchie**přepněte na kartu **licencování** . Vyberte možnost, kterou chcete **převést na Current Branch**, a pak zvolte **použít**.  

Když se váš web převede na Current Branch, budou k dispozici dříve nedostupné funkce a možnosti k použití.
