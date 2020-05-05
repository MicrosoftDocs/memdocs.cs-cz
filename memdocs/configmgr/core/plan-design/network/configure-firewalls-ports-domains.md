---
title: Síťová infrastruktura
titleSuffix: Configuration Manager
description: Nastavte brány firewall, porty a domény pro přípravu na Configuration Manager komunikaci.
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 816b48f7dac3703c1d45fdbc0bf8ad7dc9528caa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719838"
---
# <a name="network-infrastructure-considerations-for-configuration-manager"></a>Požadavky na infrastrukturu sítě pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pro přípravu sítě na podporu Configuration Manager možná budete muset nakonfigurovat některé součásti infrastruktury. Například otevřete porty brány firewall, abyste mohli předat komunikaci, kterou používá Configuration Manager.  

## <a name="ports-and-protocols"></a>Porty a protokoly

Různé funkce Configuration Manager používají různé síťové porty. Některé porty jsou povinné a některé můžete přizpůsobit.

Většina Configuration Manager komunikace používá pro protokol HTTPS běžné porty, jako je port 80 pro protokol HTTP nebo 443. Některé role systému lokality podporují používání vlastních webů a vlastních portů. Další informace najdete v tématu [weby pro servery systému lokality](websites-for-site-system-servers.md).

Než nasadíte Configuration Manager, identifikujte porty, které plánujete použít, a podle potřeby nastavte brány firewall.

Pokud potřebujete změnit port po instalaci Configuration Manager, nezapomeňte aktualizovat brány firewall na zařízeních a síti. Změňte také konfiguraci portu v Configuration Manager.

Další informace najdete v těchto článcích:

- [Postup konfigurace portů pro komunikaci klientů](../../clients/deploy/configure-client-communication-ports.md)
- [Porty používané v Configuration Manager](../hierarchy/ports.md)


## <a name="internet-access-requirements"></a>Požadavky na přístup k internetu

Některé funkce Configuration Manager spoléhají na možnosti připojení k Internetu, které mají plnou funkčnost. Pokud vaše organizace omezuje síťovou komunikaci s Internetem pomocí brány firewall nebo proxy zařízení, ujistěte se, že je nutné povolit požadované koncové body.

Další informace najdete v tématu [požadavky na přístup k Internetu](internet-endpoints.md) .


## <a name="proxy-servers"></a>Proxy servery

Pro různé servery a klienty systému lokality můžete zadat samostatné proxy servery. Tyto konfigurace provedete při instalaci role systému lokality nebo klienta nebo později v případě potřeby změníte.

Další informace najdete v tématu [Podpora proxy serveru](proxy-server-support.md).
