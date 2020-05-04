---
title: Vyhodnotit v testovacím prostředí
titleSuffix: Configuration Manager
description: Vytvořte testovací prostředí pro vyhodnocení Configuration Manager pro použití ve vaší organizaci.
ms.date: 02/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dd238319ba064f57911eee58e1299e17a2ce5b60
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713839"
---
# <a name="evaluate-configuration-manager-by-building-your-own-lab-environment"></a>Vyhodnotit Configuration Manager vytvořením vlastního testovacího prostředí

*Platí pro: Configuration Manager (Current Branch)*

 Naučte se, jak vytvořit testovací prostředí pro vyhodnocení Configuration Manager pro použití ve vaší organizaci.  

 Configuration Manager je komplexní a výkonný nástroj pro správu uživatelů, zařízení a softwaru. Je vhodné důkladně vyhodnotit Configuration Manager před úplným nasazením, abyste mohli Marry koncepční porozumění s praktickými cvičeními.  

 Tato příručka je primárně určena správcům, kteří vyhodnocují použití Configuration Manager v podnikových prostředích:  

-   Správci, kteří chtějí mít řešení plně spravovat počítače, servery a mobilní zařízení  

-   Správci v oborech s vysokou úrovní zabezpečení, kteří vyžadují zabezpečení místní správy zařízení s flexibilitou cloudové správy zařízení  

-   Správci, kteří chtějí spravovat škálování své místní architektury serveru  

## <a name="what-this-lab-does"></a>Co toto testovací prostředí nabízí  
 Hlavním cílem vytvoření tohoto testovacího prostředí je poskytnout vám obecné znalosti, jak začít pracovat s Configuration Manager a vylepšit své porozumění Configuration Manager. Projděte si urychlené sestavení aktuální verze Configuration Manager pomocí dvou serverů:  

-   Ten, který je hostitelem služby Active Directory, řadiče domény a serveru DNS.  

-   Ten, který je hostitelem Configuration Manager a všechny přidružené SQL Server součásti  

Klientské počítače jsou nainstalované v rámci technologie Hyper-V. Samotné testovací prostředí se dá také spustit jako plně virtualizovaný systém na jednom serveru.  

## <a name="what-this-lab-does-not-do"></a>Co toto testovací prostředí nenabízí  
 Tato laboratoř vás neprovede všemi Configuration Manager scénáři. Není navržena tak, aby se ihned migrovali do aktivního prostředí.  

 Když sestavíte tuto testovací prostředí, získáte funkční prostředí, ve kterém můžete pracovat. Toto prostředí ale nebude optimalizované pro faktory, jako je výkon systému, Správa místa na pevném disku a SQL Server úložiště.  

##  <a name="recommended-reading-before-you-build-the-lab"></a><a name="BKMK_EvalRec"></a>Doporučené čtení před sestavením testovacího prostředí  
 K dispozici je spousta obsahu v [dokumentaci pro Configuration Manager](https://docs.microsoft.com/sccm/). Než začnete sestavovat testovací prostředí, doporučujeme, abyste si přečetli následující témata z této knihovny:  

-   Naučte se základní koncepty týkající se konzoly Configuration Manager, portálů pro koncové uživatele a ukázkových scénářů v části [Úvod do Configuration Manager](../../core/understand/introduction.md).  

-   Přečtěte si o hlavních možnostech správy Configuration Manager v části [funkce a možnosti Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md).  

-   Podpořit své znalosti [základy Configuration Manager](../../core/understand/fundamentals.md).  

-   Zjistěte důležitost rolí zabezpečení v tématu [základy správy na základě rolí pro Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   Seznamte se se správou obsahu v [konceptech správy obsahu](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   Naučte se, jak úspěšně podporovat každodenní úkoly v rámci nasazení, v tématu [Vysvětlení způsobu, jakým klienti hledají služby a prostředky lokality pro Configuration Manager](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  
