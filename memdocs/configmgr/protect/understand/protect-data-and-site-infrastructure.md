---
title: Ochrana dat a infrastruktury lokality
titleSuffix: Configuration Manager
description: Přečtěte si, jak chránit prostředky vaší organizace před expozicí nebo škodlivým útokem pomocí Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 2117f786-d521-4790-9e8d-ec096c63c9d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 381f9d190b1d73bbbab6142fd9587e881d0870ce
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723912"
---
# <a name="protect-data-and-site-infrastructure"></a>Ochrana dat a infrastruktury lokality

*Platí pro: Configuration Manager (Current Branch)*

Chcete, aby vaši uživatelé měli zabezpečený přístup k prostředkům vaší organizace. Chraňte svoji infrastrukturu i vaše data před expozicí nebo škodlivým útokem. K povolení přístupu a ochraně prostředků vaší organizace použijte Configuration Manager.  

- [Endpoint Protection](../deploy-use/endpoint-protection.md) vám umožní spravovat následující zásady programu Microsoft Defender pro klientské počítače:

  - Antimalwarový program Microsoft Defender
  - Firewall v programu Microsoft Defender
  - Rozšířená ochrana před internetovými útoky v programu Microsoft Defender
  - Ochrana před zneužitím programu Microsoft Defender
  - Ochrana Application Guard v programu Microsoft Defender
  - Řízení aplikací v programu Microsoft Defender

  > [!TIP]
  > Pokud chcete spravovat službu Endpoint Protection na spoluspravovaných zařízeních s Windows 10 pomocí cloudové služby Microsoft Endpoint Manager, přepněte [ **Endpoint Protection** úlohy](../../comanage/workloads.md#endpoint-protection) do Intune. Další informace najdete v tématu [Endpoint Protection pro Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).

- Chraňte data uložená na místních klientech Windows pomocí nástroj BitLocker Drive Encryption (BDE). Configuration Manager poskytuje úplnou správu životního cyklu BitLockeru, která může nahradit použití nástroje Microsoft BitLocker Administration and Monitoring (MBAM). Další informace najdete v tématu [Plánování správy BitLockeru](../plan-design/bitlocker-management.md).

- Místo tradičních hesel můžete povolit alternativní metody přihlašování na zařízeních s Windows 10 pomocí Windows Hello pro firmy. Další informace najdete v tématu [nastavení Windows Hello pro firmy](../deploy-use/windows-hello-for-business-settings.md).

- Umožněte uživatelům připojení k prostředkům tím, že povolíte připojení k síti VPN pomocí profilů VPN, a minimalizujte tak úsilí uživatelů. Další informace najdete v tématu [Profily sítě VPN](../deploy-use/vpn-profiles.md).  

- Profily Wi-Fi poskytují sadu nástrojů a prostředků, které vám pomůžou spravovat nastavení bezdrátové sítě na zařízeních ve vaší organizaci. Nasazením těchto nastavení minimalizujete úsilí, které koncoví uživatelé potřebují pro připojení k bezdrátovým sítím. Další informace najdete v tématu [Profily sítě Wi-Fi](../deploy-use/create-wifi-profiles.md).  

- Zřídí zařízení s certifikáty, které uživatelé potřebují k připojení k prostředkům. Další informace najdete v tématu [profily certifikátů](../deploy-use/introduction-to-certificate-profiles.md).  
