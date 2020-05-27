---
title: Registrace zařízení s pracovním profilem Android Enterprise v Intune
titleSuffix: Microsoft Intune
description: Naučte se registrovat zařízení s pracovním profilem Android Enterprise v Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 5/13/2019
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
ms.openlocfilehash: c3da384efb87e5510e64954ed7b1badfb98f6583
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83987509"
---
# <a name="set-up-enrollment-of-android-enterprise-work-profile-devices"></a>Nastavení registrace zařízení s pracovním profilem Android Enterprise

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune vám pomůže nasadit aplikace a nastavení do zařízení se systémem Android Enterprise Work Profile, aby se zajistilo, že pracovní a osobní údaje budou oddělené. Konkrétní podrobnosti o Androidu Enterprise najdete v tématu [požadavky na Android Enterprise](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).

Pokud chcete nastavit správu pracovních profilů pro Android Enterprise, postupujte takto:

1. [Připojte svůj účet tenanta Intune ke svému účtu Android Enterprise](connect-intune-android-enterprise.md).
2. Zadejte nastavení registrace pracovního profilu Android Enterprise. Pracovní profily Android Enterprise jsou [podporované jenom na určitých zařízeních s Androidem](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012%20style=%22target=new_window%22). Každé zařízení, které podporuje pracovní profily Android Enterprise, podporuje také správu Správce zařízení s Androidem. Intune umožňuje určit, jak se mají zařízení, která podporují pracovní profily Android Enterprise, spravovat z [omezení registrace](enrollment-restrictions-set.md).
    - **Blokování**: všechna zařízení s Androidem, včetně zařízení, která podporují pracovní profily Android Enterprise, se zaregistrují jako zařízení s Androidem pro správce zařízení, pokud se nezablokuje i registrace Správce zařízení s Androidem. 
    - **Povolené (výchozí nastavení)**: všechna zařízení, která podporují pracovní profily Android Enterprise, se zaregistrují jako zařízení s Androidem Enterprise Work Profiling. Zařízení s Androidem, které nepodporuje firemní pracovní profily Androidu, se zaregistruje jako zařízení s Androidem pro správce zařízení, pokud není zablokované zápis Správce zařízení s Androidem. 
> [!NOTE]
> Výchozí nastavení **povoleno** platí pro nové klienty od července 2019. U všech předchozích tenantů se neprojeví žádná změna v omezeních registrace a zobrazí se všechny zásady, které nastavily v omezeních registrace. Pro předchozí klienty, u kterých se nikdy nezměnila omezení registrace, bude pro pracovní profily Android Enterprise stále výchozí **blok** .

3. [Sdělte uživatelům, jak mají svá zařízení zaregistrovat](../user-help/enroll-device-android-work-profile.md).  

Pokud chcete zaregistrovat zařízení pomocí firemních pracovních profilů Androidu, ale tato zařízení jsou už zaregistrovaná ve Správci zařízení s Androidem, musí se nejdřív zrušit registrace a pak znovu zaregistrovat.
> [!NOTE]
> Jako správce můžete to provést vzdáleně pomocí funkce **vyřadit z provozu** . Tuto funkci najdete v nabídce Akce po výběru zařízení v okně **všechna zařízení** .

Pokud zaregistrujete zařízení se systémem Android Enterprise Work Profiling pomocí účtu [správce registrace zařízení](device-enrollment-manager-enroll.md) , je k dispozici omezení 10 zařízení, která je možné zaregistrovat pro jednotlivé účty.

Další informace najdete v článku [Data z Intune odesílaná Googlu](../protect/data-intune-sends-to-google.md).

## <a name="next-steps-for-android-enterprise-work-profiles"></a>Další kroky pro pracovní profily Android Enterprise
- [Nasazení aplikací v pracovním profilu Android Enterprise](../apps/apps-add-android-for-work.md)
- [Přidat zásady konfigurace pracovních profilů pro Android Enterprise](../configuration/device-profiles.md)

## <a name="see-also"></a>Viz také

[Konfigurace a řešení potíží se zařízeními s Androidem Enterprise v Microsoft Intune](https://support.microsoft.com/help/4476974)
