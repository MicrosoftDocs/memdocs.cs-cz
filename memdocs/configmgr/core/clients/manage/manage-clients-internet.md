---
title: Správa klientů na internetu
titleSuffix: Configuration Manager
description: Přečtěte si o správě klientů pomocí brány pro správu cloudu a internetové správy klientů v Configuration Manager.
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2840b30bee20d2fa73531b07c095e028979f6274
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715590"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Správa klientů na internetu pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Většinou v Configuration Manager je většina spravovaných počítačů a serverů fyzicky ve stejné interní síti jako servery systému lokality, které provádějí funkce správy. Můžete ale spravovat klienty mimo vaši interní síť, když jsou připojeni k Internetu. Tato možnost nevyžaduje, aby se klienti připojovali přes VPN, aby dosáhli serverů systému lokality.

Configuration Manager poskytuje dva způsoby, jak spravovat klienty připojené k Internetu:

- Brána pro správu cloudu

- Internetová správa klientů

> [!NOTE]
> Pro jednu lokalitu můžete mít kombinaci obou služeb. Pokud zařízení získá zásady z lokality pro IBCM i CMG, pak je mezi nimi náhodně přesměruje pro komunikaci. Jediným mechanismem, který je k dispozici pro řízení komunikace, je ověření klienta. Například pokud klient připojený k Azure AD nedůvěřuje ověřovacímu certifikátu serveru internetového bodu správy, může použít pouze CMG. Pokud klient připojený k doméně nedůvěřuje ověřovacímu certifikátu serveru CMG, může použít pouze internetový bod správy.<!-- SCCMDocs#1541 -->

## <a name="cloud-management-gateway"></a>Brána pro správu cloudu

Brána pro správu cloudu poskytuje správu internetových klientů. Používá kombinaci Microsoft Azure cloudové služby a místní roli systému lokality, která komunikuje s touto službou. Internetoví klienti používají cloudovou službu ke komunikaci s místními Configuration Manager.

### <a name="cmg-advantages"></a>Výhody CMG

- Nevyžadují se žádné další místní investice do infrastruktury.  

- Nevystavuje místní infrastrukturu pro Internet.  

- Cloudové virtuální počítače, které spouštějí službu, jsou plně spravovány Azure a nevyžadují žádnou údržbu.  

- Snadné nastavení a konfigurace v konzole Configuration Manager.  

### <a name="cmg-disadvantages"></a>CMG nevýhody  

- Náklady na předplatné cloudu  

- Data správy odesílaná prostřednictvím cloudové služby.  

Další informace najdete v tématu [Plánování brány pro správu cloudu](cmg/plan-cloud-management-gateway.md).  

## <a name="internet-based-client-management"></a>Internetová správa klientů

Tato metoda spoléhá na internetové servery webového serveru, ke kterým klienti přímo komunikují za účelem správy. Vyžaduje, aby klienti a systémové servery lokality byly nakonfigurovány pro internetovou správu klientů (IBCM).

### <a name="ibcm-advantages"></a>Výhody IBCM

- Žádná závislost cloudové služby.  

- S cloudovým předplatným nejsou spojené žádné další náklady.  

- Úplné řízení serverů a rolí poskytujících službu.  

### <a name="ibcm-disadvantages"></a>IBCM nevýhody

- Vyžadovat další investice do infrastruktury.  

- Režie a provozní náklady na další infrastrukturu.  

- Infrastruktura musí být zveřejněná pro Internet.  

Další informace najdete v tématu [plánování internetové správy klientů](plan-internet-based-client-management.md).  
