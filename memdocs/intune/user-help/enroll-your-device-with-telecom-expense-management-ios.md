---
title: Registrace zařízení s iOSem ve službě TEM (Telecom Expense Management) pomocí Intune
description: Přečtěte si, jak zaregistrovat zařízení s iOSem ve službě TEM (Telecom Expense Management).
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/19/2017
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 6d8c6372-f2ce-4558-8886-1d7c1966699c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: sumitp
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 19ab2f9390875a9c094ede4706952bab8187da2e
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79328159"
---
# <a name="enroll-your-ios-device-in-telecom-expense-management"></a>Registrace zařízení s iOS ve službě TEM (Telecom Expense Management)

Vaše organizace může používat software pro správu telekomunikačních výdajů (TEM – Telecom Expense Management), aby zajistila využívání datových a hlasových tarifů v rámci přijatelných limitů. Po dokončení registrace zařízení budete vyzváni k výběru nejvhodnější kategorie tohoto zařízení.

  ![Snímek obrazovky s výběrem nejvhodnější kategorie pro zařízení s iOS. Zobrazuje výběr firemní nebo osobní registrace.](./media/ios-enroll-10-tem-select-best-category.png)

Po výběru příslušné možnosti dostanete oznámení s pokynem k instalaci aplikace [__Datalert__](https://itunes.apple.com/app/datalert/id771029268?mt=8) z App Storu. Aplikace Datalert umožňuje vaší organizaci měřit využití dat. Pokud má vaše organizace nakonfigurovanou možnost pracovní nebo školní registrace, budete se muset přihlásit pomocí pracovního nebo školního účtu. Pokud taková možnost není povolena, budete muset zadat údaje, jako je vaše telefonní číslo, a ověřit zařízení pomocí kódu, abyste se mohli z aplikace zaregistrovat ve službě Datalert.

  ![Snímek úvodní obrazovky aplikace Datalert se stručným vysvětlením toho, jak vám tato aplikace pomůže využít datový tarif na maximum, a výzvou k přechodu na další obrazovku](./media/ios-enroll-11-tem-datalert-setup.png)

## <a name="enroll-into-datalert-using-your-microsoft-work-or-school-account"></a>Registrace v Datalertu pomocí pracovního nebo školního účtu Microsoft

> [!NOTE]
> Abyste se mohli zaregistrovat tímto způsobem, musíte mít v telefonu nainstalovanou a aktivovanou aplikaci [Microsoft Authenticator](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to).

1. Vyberte __Zaregistrovat se pomocí účtu Microsoft__.

   ![Snímek obrazovky Nastavení v aplikaci Datalert, na které je v horní části zobrazeno pole pro registraci zařízení a v dolní části možnost registrace pomocí účtu Microsoft, pokud máte účet Microsoft Office 365 a předplatné Intune](./media/ios-enroll-11a-tem-datalert-enroll-msft-account.png)

2. Zobrazí se oznámení __Datalert chce otevřít Authenticator__. Vyberte __Otevřít__.

   ![Snímek automaticky otevíraného okna s výzvou, aby uživatel otevřel aplikaci Authenticator na žádost aplikace Datalert](./media/ios-enroll-11b-tem-datalert-open-authenticator.png)

3. Přihlaste se __školním nebo pracovním účtem Microsoft__. Datalert se bude instalovat a po chvíli by se měla instalace dokončit. Po dokončení klepněte na __Dokončit__.

## <a name="enroll-into-datalert-using-your-phone-number"></a>Registrace v Datalertu pomocí telefonního čísla

1. Zadejte telefonní číslo zařízení.

   ![Snímek obrazovky aplikace Datalert s žádostí o telefonní číslo](./media/ios-enroll-12-tem-datalert-phone-number.png)

2. Prostřednictvím SMS zprávy pak dostanete ověřovací kód. Zadejte tento kód a klepněte na __OK__.

   ![Snímek obrazovky aplikace Datalert s žádostí o ověřovací kód v SMS zprávě](./media/ios-enroll-13-tem-datalert-sms.png)

3. Jakmile tento ověřovací kód zadáte, instalace aplikace Datalert se dokončí. Po klepnutí na __Dokončit__ budete moci v aplikaci Datalert monitorovat využití dat.

   ![Snímek obrazovky aplikace Datalert s monitorováním dnešního využití dat](./media/ios-enroll-14-tem-datalert-monitoring-active.png)

Po registraci začnete v aplikaci Datalert sledovat využití dat.

Potřebujete ještě další pomoc? Obraťte se na podporu ve vaší společnosti. Kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).
