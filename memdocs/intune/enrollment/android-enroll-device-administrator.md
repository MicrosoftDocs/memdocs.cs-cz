---
title: Registrace Správce zařízení s Androidem v Microsoft Intune
titleSuffix: ''
description: Registrace zařízení s Androidem do Intune pomocí registrace Správce zařízení
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/23/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2f4683f3c7a243c6342d5fed99b534767bb943fd
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2020
ms.locfileid: "90815000"
---
# <a name="android-device-administrator-enrollment"></a>Registrace správce zařízení s Androidem

Správce zařízení s Androidem (někdy označovaný jako "starší verze" správy Androidu a vydaný s Androidem 2,2) je způsob, jak spravovat zařízení s Androidem. Vylepšené funkce správy jsou teď ale k dispozici v [Androidu Enterprise](https://www.android.com/enterprise/management/) (vydané s androidem 5,0). V úsilí o přechod na moderní, bohatou a bezpečnější správu zařízení bude Google v nových verzích Androidu snížit podporu Správce zařízení.

Proto doporučujeme, abyste zabránili zaregistrování nových zařízení pomocí procesu Správce zařízení popsaného níže.

Ze stejných důvodů doporučujeme, abyste v případě, že se zařízení aktualizují na Android 10, migrovali zařízení mimo správu Správce zařízení. 

> [!IMPORTANT]
> V oblastech, kde je k dispozici Android Enterprise, Google podporuje pohyb od správy zařízení (DA) tím, že snižuje podporu správy v nových verzích Androidu. Pokud však nejsou k dispozici Android Enterprise nebo GMS, budete chtít použít Správce zařízení a seznámit se s těmito změnami. Další informace najdete v části [je Android Enterprise k dispozici ve své zemi](https://support.google.com/work/android/answer/6270910)?

Pokud se přesto rozhodnete, že mají uživatelé zaregistrovat svoje zařízení s Androidem pomocí správy Správce zařízení, pokračujte k další části.  

Další informace o funkcích pro Android Enterprise v Google najdete v těchto článcích:
- [Pokyny pro migraci ze strany správce zařízení na Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Dokumentace ke službě Google v plánu pro zařazování rozhraní API pro správce zařízení](https://developers.google.com/android/work/device-admin-deprecation)

## <a name="set-up-device-administrator-enrollment"></a>Nastavení registrace Správce zařízení

1. Při přípravě na správu mobilních zařízení musíte nastavit autoritu pro správu mobilních zařízení (MDM) na **Microsoft Intune**. Pokyny k tomu najdete v článku [Nastavení autority MDM](../fundamentals/mdm-authority-set.md). Tato možnost se nastavuje jenom jednou při prvním nastavování Intune pro správu mobilních zařízení.
2. Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) a vyberte > **zařízení**  >  **Android**Android  >  **registrace**  >  **osobní zařízení a zařízení vlastněná společností pomocí oprávnění pro správu**zařízení  >  :**ke správě zařízení použijte Správce zařízení**.
3. [Sdělte uživatelům, jak mají svá zařízení zaregistrovat](../user-help/enroll-device-android-company-portal.md).  

Po registraci můžete začít se správou zařízení uživatelů v Intune včetně [přiřazení zásad dodržování předpisů](../protect/compliance-policy-create-android.md), [správy aplikací](../apps/app-management.md) a dalších úloh.

Informace o dalších uživatelských úkolech najdete v článcích:
- [Materiály o prostředí Microsoft Intune pro koncové uživatele](../fundamentals/end-user-educate.md)
- [Použití zařízení Android s Intune](../user-help/why-enroll-android-device.md)


## <a name="block-device-administrator-enrollment"></a>Zablokovat registraci Správce zařízení
Pokud chcete blokovat zařízení pro správce zařízení s Androidem nebo zablokovat jenom zařízení s Androidem ve vlastnictví zařízení s Androidem, přečtěte si téma [Nastavení omezení typu zařízení](enrollment-restrictions-set.md).


## <a name="next-steps"></a>Další kroky
- [Přiřazení zásad dodržování předpisů](../protect/compliance-policy-create-android.md)
- [Správa aplikací](../apps/app-management.md)