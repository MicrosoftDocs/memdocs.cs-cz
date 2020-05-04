---
title: Správa klientů na internetu
titleSuffix: Configuration Manager
description: Přečtěte si o správě klientů pomocí brány pro správu cloudu a internetové správy klientů v Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c00d480b993498c5fa27e2a4d91a5f2a3bc130ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710626"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Správa klientů na internetu pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Většinou v Configuration Manager je většina spravovaných počítačů a serverů fyzicky ve stejné interní síti jako servery systému lokality, které provádějí funkce správy. Můžete ale spravovat klienty mimo vaši interní síť, když jsou připojeni k Internetu. Tato možnost nevyžaduje, aby se klienti připojovali přes VPN, aby dosáhli serverů systému lokality.

Configuration Manager poskytuje dva způsoby, jak spravovat klienty připojené k Internetu:

-   Brána pro správu cloudu

-   Internetová správa klientů


## <a name="cloud-management-gateway"></a>Brána pro správu cloudu

Brána pro správu cloudu poskytuje správu internetových klientů. Používá kombinaci Microsoft Azure cloudové služby a novou roli systému lokality, která komunikuje s touto službou. Internetoví klienti používají cloudovou službu ke komunikaci s místními Configuration Manager.

#### <a name="advantages"></a>Výhody  

-   Nevyžadují se žádné další místní investice do infrastruktury.  

-   Nevystavuje místní infrastrukturu pro Internet.  

-   Cloudové virtuální počítače, které spouštějí službu, jsou plně spravovány Azure a nevyžadují žádnou údržbu.  

-   Snadné nastavení a konfigurace v konzole Configuration Manager.  

#### <a name="disadvantages"></a>Nevýhody  

-   Náklady na předplatné cloudu  

-   Data správy odesílaná prostřednictvím cloudové služby.  

Další informace najdete v tématu [Plánování brány pro správu cloudu](cmg/plan-cloud-management-gateway.md).  



## <a name="internet-based-client-management"></a>Internetová správa klientů

Tato metoda spoléhá na internetové servery webového serveru, na které klienti komunikují z důvodů správy. Vyžaduje, aby byly klienti a servery systému lokality nakonfigurované pro internetovou správu.

#### <a name="advantages"></a>Výhody  

-   Žádná závislost cloudové služby.  

-   S cloudovým předplatným nejsou spojené žádné další náklady.  

-   Úplné řízení serverů a rolí poskytujících službu.  

#### <a name="disadvantages"></a>Nevýhody  

-   Vyžadovat další investice do infrastruktury.  

-   Režie a provozní náklady na další infrastrukturu.  

-   Infrastruktura musí být zveřejněná pro Internet.  

Další informace najdete v tématu [plánování internetové správy klientů](plan-internet-based-client-management.md).  
