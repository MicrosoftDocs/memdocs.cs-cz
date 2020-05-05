---
title: Správa aplikací pro místní správu mobilních zařízení (MDM)
titleSuffix: Configuration Manager
description: Spravujte aplikace pro místní správu mobilních zařízení (MDM) v Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 693f661f2a2db59335ec8e463842a0ad03c977f3
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721910"
---
# <a name="manage-apps-for-on-premises-mdm-in-configuration-manager"></a>Správa aplikací pro místní MDM v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Když spravujete zařízení pomocí Configuration Manager místní správy mobilních zařízení (MDM), můžete spravovat následující typy aplikací:

- Balíček aplikace systému Windows Phone (soubor .xap)
- Balíček aplikací systému Windows Phone (ve skladu systému Windows Phone)
- Instalační služba systému Windows pomocí MDM
- Webová aplikace

Obecnější informace o správě Configuration Manager aplikací a typů nasazení najdete v tématu [úlohy správy pro Configuration Manager aplikace](../../apps/deploy-use/management-tasks-applications.md).

## <a name="create-windows-phone-application"></a><a name="bkmk_winphone"></a>Vytvoření aplikace Windows Phone

Configuration Manager aplikace má jeden nebo více typů nasazení. Typ nasazení zahrnuje instalační soubory a informace, které jsou nutné k nasazení softwaru do zařízení. Typ nasazení má taky pravidla, která určují, kdy a jak se má software nasadit.

Obecné kroky pro vytvoření aplikace a typů nasazení naleznete v tématu Create a [Application](../../apps/deploy-use/create-applications.md#bkmk_create).

Configuration Manager podporuje následující typy souborů aplikací pro zařízení se systémem Windows Mobile:

|Typ zařízení|Podporované typy souborů|
|-----------------|---------------------|
|Windows Phone 8|XAP|
|Windows Phone 8.1|XAP, AppX, appxbundle|
|Windows 10 Mobile|XAP, AppX, appxbundle|

Nasaďte aplikace Windows Phone jako **dostupné** nebo **povinné**. K odinstalaci aplikací taky použijte nasazení.

## <a name="deploy-and-monitor-apps"></a>Nasazení a monitorování aplikací

Nasaďte a monitorujte aplikace pro mobilní zařízení v Configuration Manager stejným způsobem jako u jiných zařízení, jako jsou stolní počítače a servery. Další informace najdete v těchto článcích:

- [Nasazení aplikací](../../apps/deploy-use/deploy-applications.md)
- [Monitorování aplikací](../../apps/deploy-use/monitor-applications-from-the-console.md)

Zkontrolujte následující omezení specifická pro mobilní zařízení:

- Zařízení zaregistrovaná v MDM nepodporují simulovaná nasazení, uživatelské prostředí ani nastavení plánování.

- Nepřidávejte do jedné aplikace více než 100 lokálních hodnot. Tato akce zabrání instalaci aplikace do zařízení.

## <a name="next-step"></a>Další krok

Chcete-li provést změny, odinstalovat nebo nahradit nasazenou aplikaci novou aplikací, můžete ji spravovat stejně jako jakoukoli aplikaci v Configuration Manager. Další informace najdete v tématu [aktualizace a vyřazení aplikací](../../apps/deploy-use/update-and-retire-applications.md).
