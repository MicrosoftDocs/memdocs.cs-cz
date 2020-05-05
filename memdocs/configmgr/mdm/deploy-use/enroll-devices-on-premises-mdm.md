---
title: Registrace zařízení pro místní správu MDM
titleSuffix: Configuration Manager
description: Přečtěte si o metodách registrace zařízení pro místní správu mobilních zařízení (MDM) v Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1ca7f792bb6b419dd1d20d495bdb53bc7c2be506
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720671"
---
# <a name="enroll-devices-for-on-premises-mdm-in-configuration-manager"></a>Registrace zařízení pro místní MDM v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pokud chcete spravovat zařízení pomocí Configuration Manager místní správy mobilních zařízení (MDM), musíte je nejdřív zaregistrovat. Pak Configuration Manager můžou komunikovat se zařízeními pro úlohy správy. Configuration Manager poskytuje dvě metody registrace zařízení:

- **Zápis uživatele**: Uživatelé spouštějí proces registrace na svém zařízení. Aby registrace uživatele proběhla úspěšně, nainstalujte certifikát důvěryhodného kořenového certifikátu do zařízení a zajistěte uživateli registraci v nastavení klienta. Pokud chcete zařízení zaregistrovat, musí uživatel zadat jenom svoje přihlašovací údaje.

    Další informace najdete v tématu [jak uživatelé registrují zařízení](user-enroll-devices-on-premises-mdm.md).

- **Hromadná registrace**: uživatel zařízení nespustí registraci. V Configuration Manager vytvoříte balíček hromadného zápisu. Když ho otevřete na zařízení, balíček poskytne informace potřebné k registraci zařízení.

    Další informace najdete v tématu [jak hromadně registrovat zařízení](bulk-enroll-devices-on-premises-mdm.md).

Další informace o verzích operačních systémů, které Configuration Manager podporuje pro registraci zařízení v místní MDM, najdete v části [podporované konfigurace](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).
