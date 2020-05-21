---
title: Správa šifrování disků pomocí zásad zabezpečení Endpoint v Microsoft Intune | Microsoft Docs
description: Nakonfigurujte a nasaďte zásady pro zařízení, která spravujete pomocí zásad šifrování disku Endpoint Security ve službě Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: b988e4ddeb306c7da290c87e8a32fa0571627257
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431309"
---
# <a name="disk-encryption-policy-for-endpoint-security-in-intune"></a>Zásady šifrování disku pro zabezpečení koncového bodu v Intune

Profily šifrování disku Endpoint Security se zaměřují jenom na nastavení, která jsou relevantní pro vestavěnou metodu šifrování zařízení, jako je třeba trezor nebo BitLocker. Díky tomuto zaměření můžou správci zabezpečení spravovat nastavení šifrování disků bez nutnosti přecházet na hostitele nesouvisejícího nastavení.

I když můžete nakonfigurovat stejné nastavení zařízení pomocí profilů *Endpoint Protection* pro konfiguraci zařízení, profily konfigurace zařízení obsahují další kategorie nastavení. Tato další nastavení nejsou v souvislosti s šifrováním disku a mohou zkomplikovat úlohy konfigurace pouze šifrování disku.

Zásady zabezpečení koncového bodu pro zásady šifrování disku najdete v části *Správa* v uzlu **zabezpečení koncového bodu** v [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

## <a name="prerequisites-for-disk-encryption-policy"></a>Předpoklady pro zásady šifrování disků

- **MacOS** -MacOS 10,13 nebo novější
- **Windows** – Windows 10 nebo novější

## <a name="disk-encryption-profiles"></a>Profily šifrování disků

**MacOS profily**:

- **Trezor úložišť** – trezor pro zařízení s MacOS zajišťuje integrované šifrování celého disku.

  Spravujte [Nastavení trezoru](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) MacOS.

  Pokud chcete vytvořit profil trezoru, přečtěte si téma [použití šifrování disku trezoru úložiště pro MacOS](../protect/encrypt-devices-filevault.md).

**Profily Windows 10**:

- **BitLocker** -nástroj BitLocker Drive Encryption je funkce ochrany dat, která se integruje s operačním systémem a řeší hrozby krádeže nebo expozice dat před ztrátou, odcizenými nebo nevhodně vyřazenými počítači.

  Správa [nastavení nástroje BitLocker](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker) pro Windows 10.

  Pokud chcete vytvořit profil BitLockeru, přečtěte si téma [použití šifrování disku nástrojem BitLocker pro Windows 10](../protect/encrypt-devices.md).

## <a name="manage-device-encryption"></a>Správa šifrování zařízení

Po nasazení zásad pro šifrování disku zařízení si přečtěte následující články, kde najdete informace o správě šifrování:

- [Správa nástroje BitLocker](../protect/encrypt-devices.md#manage-bitlocker)
- [Správa trezoru úložišť](../protect/encrypt-devices-filevault.md#manage-filevault)
- [Monitorování šifrování zařízení](../protect/encryption-monitor.md)

## <a name="next-steps"></a>Další kroky

- [Vytvoření profilu trezoru úložiště](../protect/encrypt-devices-filevault.md#create-an-endpoint-security-policy-for-filevault)
- [Postup vytvoření profilu nástroje BitLocker](../protect/encrypt-devices.md#create-an-endpoint-security-policy-for-bitlocker)
