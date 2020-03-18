---
title: Příprava Intune na správu mobilních zařízení
titleSuffix: Microsoft Intune
description: Před migrací do Microsoft Intune vyhodnoťte svoje obchodní a technické požadavky.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 58591442-6606-4f39-a06b-f17a1f25af25
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 46e717478078ab13cc2c8783cdacbde0911e83a5
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331203"
---
# <a name="phase-1-prepare-microsoft-intune-for-mobile-device-management-mdm"></a>Fáze 1: Příprava Microsoft Intune na správu mobilních zařízení (MDM)

Než začneme probírat podrobnosti nastavení Intune, zaměřme se na posouzení požadavků vaší organizace na správu mobilních zařízení. Může být vhodné spustit sestavy aktivních uživatelů v aktuálním zprostředkovateli MDM a identifikovat tak nejdůležitější skupiny uživatelů. Pak můžete začít řešit otázky v části [vyhodnocení požadavků na MDM](migration-guide-prepare.md#assess-mdm-requirements) .

## <a name="assess-mdm-requirements"></a>Vyhodnocení požadavků na MDM

### <a name="what-kinds-of-devices-do-you-need-to-manage"></a>Jaké druhy zařízení potřebujete spravovat?

- Pro které [platformy](supported-devices-browsers.md) potřebujete podporu?

- Jsou zařízení, která potřebujete podporovat, podniková nebo osobní?

- Jaký druh připojení používáte? Wi-Fi, mobilní síť nebo VPN?

### <a name="what-do-your-users-need-to-do-on-managed-devices"></a>Co vaši uživatelé potřebují dělat na spravovaných zařízeních?

- Potřebujete zřizovat aplikace pro koncové uživatele?

- Používáte vlastní obchodní aplikace? Nebo pracujete jen s veřejnými aplikacemi z obchodu?

- Potřebujete zřizovat e-mailové účty?

### <a name="what-kinds-of-users"></a>O jaký druh uživatelů se jedná?

- Kolik uživatelů bude používat jedno zařízení?

- Jaké podmínky použití potřebujete?

  - Zapojte do plánování včas právní oddělení.
  - Jaké lokalizace budou potřeba?

- Jsou uživatelé obeznámeni s technologiemi a IT obecně?

### <a name="what-is-your-device-security-policy"></a>Jaké jsou zásady zabezpečení vašeho zařízení?

- Potřebujete šifrování na úrovni zařízení?

- Jakou délku má vaše aktuální heslo nebo PIN kód k zařízení?

- Potřebujete zakázat některé funkce zařízení nebo omezit určité chování zařízení? Pomocí profilů konfigurace zařízení můžete určovat různá nastavení specifická pro platformu, například:
  - Zakázat fotoaparát
  - Uzamknout zařízení do režimu jedné aplikace<br/>

- Jaký druh ověřování je potřeba podporovat? Pokud potřebujete ověřování na základě certifikátů, jaký druh certifikátů je potřeba poskytovat?
  - Intune můžete poskytovat certifikáty s profily přístupu k prostředkům pro zaregistrovaná zařízení.
  - Jaký typ infrastruktury veřejných klíčů (PKI) potřebujete podporovat?
  <br></br>
- Potřebujete podporovat virtuální privátní síť (VPN) na úrovni zařízení nebo aplikace?

  - Intune může zřídit konfigurace sítě VPN i pro poskytovatele sítí VPN třetích stran.
  <br/><br/>
- Je možné zavést pro některé požadavky dočasné výjimky, aby se zabránilo výpadkům? Nebo musí zařízení s přístupem vždy splňovat všechny požadavky na zabezpečení?

## <a name="next-steps"></a>Další kroky
Přečtete si tyto [případové studie](https://customers.microsoft.com/story/mwh-global-now-part-of-stantec-secures-mobile-devices-with-intune) z různých oborů, abyste získali představu, jak organizace vyhodnotily svoje požadavky na správu mobilních zařízení.

Zkontrolujte [základní nastavení Intune](migration-guide-setup.md).
