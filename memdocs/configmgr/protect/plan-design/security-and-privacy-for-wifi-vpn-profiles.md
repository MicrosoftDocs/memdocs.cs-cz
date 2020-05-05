---
title: Zabezpečení a ochrana osobních údajů profilů Wi-Fi a VPN
titleSuffix: Configuration Manager
description: Přečtěte si o doporučeních zabezpečení pro správu profilů Wi-Fi a VPN pro zařízení v Configuration Manager.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a6f444e35e16a3b42414fdc6fbee50687cf76f2f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722064"
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Zabezpečení a ochrana osobních údajů pro profily Wi-Fi a VPN v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

## <a name="security-recommendations"></a>Doporučení zabezpečení

Při správě profilů Wi-Fi a VPN pro zařízení použijte následující osvědčené postupy zabezpečení.

### <a name="choose-the-most-secure-options-that-your-wi-fi-and-vpn-infrastructure-and-client-operating-systems-can-support"></a>Vyberte nejbezpečnější možnosti, které vaše infrastruktura Wi-Fi a VPN a klientské operační systémy můžou podporovat.

Profily Wi-Fi a VPN poskytují pohodlný způsob, jak centrálně distribuovat a spravovat nastavení Wi-Fi a VPN, která už vaše zařízení podporují. Configuration Manager nepřidává funkce Wi-Fi nebo VPN. Identifikujte, implementujte a sledujte veškerá doporučení zabezpečení pro vaše zařízení a infrastrukturu.

## <a name="privacy-information"></a>Informace o ochraně osobních údajů

Profily Wi-Fi a VPN můžete použít ke konfiguraci klientských zařízení pro připojení k serverům Wi-Fi a VPN. Pak použijte Configuration Manager k vyhodnocení, jestli budou tato zařízení po použití profilů kompatibilní. Bod správy odešle serveru lokality informace o kompatibilitě a informace se uloží v databázi lokality. Informace jsou zašifrovány, když je zařízení odesílá do bodu správy, ale v databázi lokality nejsou uložena v zašifrovaném formátu. Databáze uchová informace, dokud nejsou odstraněny úlohou údržby lokality **Odstranit stará data správy konfigurací** . Výchozí interval odstranění je 90 dnů, ale můžete jej změnit. Informace o kompatibilitě nejsou odesílány společnosti Microsoft.

Ve výchozím nastavení zařízení nevyhodnocují profily sítě Wi-Fi a VPN. Kromě toho musíte nakonfigurovat profily a pak je nasadit na uživatele.  

Před konfigurací profilů sítě Wi-Fi nebo VPN zvažte své požadavky na ochranu osobních údajů.  
