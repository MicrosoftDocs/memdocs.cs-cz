---
title: Podpora domén služby Active Directory
titleSuffix: Configuration Manager
description: Seznamte se s požadavky na Configuration Manager systém lokality v doméně služby Active Directory.
ms.date: 10/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ab317597633eb432c73d2999590c1859124ddcfd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709611"
---
# <a name="support-for-active-directory-domains-in-configuration-manager"></a>Podpora domén služby Active Directory v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Všechny systémy lokality Configuration Manager musí být členy podporované domény služby Active Directory. Configuration Manager klientské počítače můžou být členy domény nebo členy pracovní skupiny.  

## <a name="requirements-and-limitations"></a>Požadavky a omezení

- Členství v doméně platí také pro systémy lokality, které podporují internetovou správu klientů v hraniční síti. (Tyto sítě se také označují jako DMZ, zóna demilitarizovaná a monitorovaná podsíť).  

- U počítače, který je hostitelem role systému lokality, není možné měnit následující konfigurace:  

  - Členství v doméně, včetně toho, pokud z domény odeberete systém lokality a pak se znovu připojíte ke stejné doméně.

  - Název domény  

  - Název počítače  

  Před provedením těchto změn Odinstalujte roli systému lokality. Chcete-li tyto změny provést na serveru lokality, nejprve odinstalujte lokalitu. Můžete také zvážit vytvoření [serveru lokality v pasivním režimu](../../servers/deploy/configure/site-server-high-availability.md) , který bude pomáhat spravovat tuto změnu na serveru lokality.

- Configuration Manager podporuje úroveň funkčnosti domény a doménové struktury systému Windows Server 2008 R2 nebo novějšího.<!-- SCCMDocs#1853 -->

## <a name="disjoint-namespace"></a><a name="bkmk_Disjoint"></a> Nesouvislý obor názvů

Můžete nainstalovat Configuration Manager systémy lokality a klienty v doméně s *nesouvislým oborem názvů*.  

V nesouvislém oboru názvů se přípona primárního serveru DNS počítače neshoduje s názvem domény DNS služby Active Directory daného počítače. Pokud název domény pro rozhraní NetBIOS řadiče domény neodpovídá názvu domény DNS služby Active Directory, dojde k jinému nesouvislému scénáři oboru názvů.  

### <a name="disjoint-scenarios"></a>Nesouvislé scénáře

Následující části popisují podporované scénáře pro oddělený obor názvů.  

#### <a name="scenario-1"></a>Scénář 1

Přípona primárního serveru DNS řadiče domény se liší od názvu domény DNS služby Active Directory. Počítače, které jsou členy domény, můžou být buď nesouvislé, nebo souvislé.

Řadič domény je v tomto případě nesouvislý. Počítače, které jsou členy domény, například servery lokality a počítače, můžou mít příponu primárního serveru DNS, která odpovídá buď:

- Přípona primárního serveru DNS řadiče domény
- Název domény DNS služby Active Directory

#### <a name="scenario-2"></a>Scénář 2

Členský počítač v doméně služby Active Directory je nesouvislý, a to i v případě, že řadič domény není nesouvislý.

V tomto scénáři se přípona primárního serveru DNS systému lokality liší od názvu domény DNS služby Active Directory. Přípona primárního serveru DNS řadiče domény je stejná jako název domény DNS služby Active Directory. Členské počítače, které jsou Configuration Manager klienty, můžou mít příponu primárního serveru DNS, která odpovídá buď:

- Přípona primárního serveru DNS nesouvislého serveru systému lokality
- Název domény DNS služby Active Directory

### <a name="configure-disjoint-namespace"></a>Konfigurovat oddělený obor názvů

Pokud chcete počítači dovolit přístup k nesouvislým řadičům domény, změňte atribut **msDS-AllowedDNSSuffixes** Active Directory na kontejneru objektů domény. Přidejte do atributu obě přípony DNS.  

Aby se zajistilo, že *seznam hledání přípon DNS* obsahuje všechny obory názvů DNS v organizaci, nakonfigurujte seznam hledání pro každý počítač v nesouvislé doméně. Do seznamu oborů názvů přidejte následující přípony:

- Přípona primárního serveru DNS řadiče domény
- Název domény DNS
- Jakékoli další obory názvů pro ostatní servery, které Configuration Manager mohou komunikovat s

Pomocí zásad skupiny můžete nakonfigurovat seznam **hledání přípon DNS (Domain Name System)** .  

> [!IMPORTANT]  
> Když odkazujete na počítač v Configuration Manager, zadejte tento počítač pomocí jeho primární přípony DNS. Tato přípona musí odpovídat plně kvalifikovanému názvu domény zaregistrovanému jako atribut **dNSHostName** v doméně služby Active Directory a hlavnímu názvu služby přidruženému k systému.  

## <a name="single-label-domains"></a><a name="bkmk_SLD"></a> Domény s názvem bez přípony

Configuration Manager podporuje systémy lokality a klienty v doméně s názvem bez přípony, pokud jsou splněné následující podmínky:  

- Nakonfigurujte doménu s názvem bez přípony v Active Directory Domain Services s nesouvislým oborem názvů DNS, který má platnou doménu nejvyšší úrovně.  

  **Příklad:** Doména s názvem bez přípony Contoso má nastavený nesouvislý obor názvů na serveru DNS contoso.com. Když zadáte příponu DNS v Configuration Manager pro počítač v doméně contoso, zadáte "Contoso.com", nikoli "contoso".  

- Připojení modelu DCOM (Distributed Component Object Model) mezi servery lokality v systémovém kontextu musí být úspěšné pomocí ověřování protokolem Kerberos.  
