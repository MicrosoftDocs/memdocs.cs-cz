---
title: Podporované konfigurace
titleSuffix: Configuration Manager
description: Identifikujte konfigurace a požadavky klíčů, abyste mohli plánovat, nasazovat a udržovat funkční Configuration Manager nasazení.
ms.date: 10/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 09618acc1c0950c3eaae79cca59fcf71dc7ef61e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709569"
---
# <a name="supported-configurations-for-configuration-manager"></a>Podporované konfigurace pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Jako místní řešení Configuration Manager využívá vaše servery, klienty, konfigurace sítě a další produkty, jako je Microsoft Intune, SQL Server a Azure.

Informace v těchto tématech a následující témata jsou nezbytné pro pomoc s identifikací konfigurací klíčů, požadavků a omezení, abyste mohli plánovat, nasazovat a udržovat funkční Configuration Manager nasazení.  Tyto informace jsou specifické pro infrastrukturu Configuration Manager lokalit, hierarchií a spravovaných zařízeních.

Pokud funkce Configuration Manager nebo schopnost vyžaduje konkrétnější konfigurace, jsou tyto informace součástí dokumentace k jednotlivým funkcím a jsou doplňující k obecnější podrobnostem o konfiguraci.  

 Produkty a technologie, které jsou popsány v následujících tématech, jsou podporovány nástrojem Configuration Manager. Jejich zahrnutí do tohoto obsahu ale neznamená rozšíření podpory pro jakýkoli produkt nad rámec životního cyklu podpory tohoto produktu. Produkty, které přesahují životní cyklus podpory, se nepodporují pro použití s Configuration Manager, včetně všech produktů, které jsou zahrnuté v programu [Extended Security Updates (EVJ)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) . Další informace o životních cyklech podpory společnosti Microsoft najdete na webu [o fázích životního cyklu podpory společnosti Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=208270) . Další informace o rozšířených aktualizacích zabezpečení v Configuration Manager najdete v tématu [podporované verze operačních systémů pro klienty a zařízení pro Configuration Manager](supported-operating-systems-for-clients-and-devices.md#bkmk_ESU).

> [!NOTE]  
>  Informace o zásadách životního cyklu podpory Microsoftu najdete na webu Nejčastější dotazy k zásadám životního cyklu podpora Microsoftu v tématu [Podpora Microsoftu zásady životního cyklu](https://go.microsoft.com/fwlink/p/?LinkId=31976).  

 Produkty a verze produktů, které nejsou uvedené v následujících tématech, se navíc v Configuration Manager nepodporují, pokud nejsou ohlášeny na [blogu Enterprise mobility and Security blog](https://blogs.technet.microsoft.com/enterprisemobility/).  V některých případech předá obsah tohoto blogu aktualizaci této části dokumentace.


-  [Dimenzování a škálování](../../../core/plan-design/configs/size-and-scale-numbers.md)  
Přečtěte si, kolik lokalit, rolí systému lokality na lokalitách a klientů nebo zařízení je podporováno v různých návrzích hierarchie pro Configuration Manager.

-  [Požadavky na lokality a systémy lokalit](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Seznamte se s konfiguracemi, které jsou potřeba na Windows serveru pro podporu různých typů lokalit a rolí systému lokality.

-  [Podporované operační systémy pro servery systému lokality](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
Informace o tom, které operační systémy můžete použít jako server lokality nebo server systému lokality.

-  [Podporované operační systémy pro klienty a zařízení](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)  
Přečtěte si o tom, které operační systémy můžete spravovat pomocí Configuration Manager, včetně Windows, Windows Embedded, Linux a UNIX, Mac a mobilních zařízení.

-  [Podporované operační systémy pro konzolu](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
Informace o tom, které operační systémy mohou hostovat konzolu Configuration Manager, aby poskytovaly bod přístupu ke správě nasazení.  

-  [Podpora verzí SQL Serveru](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
Informace o tom, které verze SQL Server mohou hostovat databázi lokality a databázi vytváření sestav, a také o požadovaných konfiguracích a volitelných konfiguracích, které můžete použít.

-  [Možnosti vysoké dostupnosti](../../servers/deploy/configure/high-availability-options.md)  
Přečtěte si o možnostech, které můžete implementovat při navrhování prostředí, aby se zajistila vysoká úroveň dostupné služby pro nasazení Configuration Manager.

-  [Doporučený hardware](../../../core/plan-design/configs/recommended-hardware.md)  
Seznamte se s pokyny, které vám pomůžou identifikovat správný hardware a konfigurace pro hostování Configuration Managerch lokalit a klíčových služeb.

-  [Podpora domén služby Active Directory](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
Přečtěte si o podporovaných konfiguracích domény služby Active Directory, které Configuration Manager vyžaduje a podporuje.

-  [Podpora pro funkce Windows a sítě](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
Přečtěte si o podporovaných technologiích Windows (například BranchCache a odstranění duplicitních dat) a o omezeních jejich použití pomocí Configuration Manager.

-  [Podpora virtualizovaných prostředí](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
Přečtěte si další informace o tom, jak používat podporované technologie virtuálních počítačů.
