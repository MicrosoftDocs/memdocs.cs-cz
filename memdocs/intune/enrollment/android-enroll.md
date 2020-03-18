---
title: Registrace zařízení s Androidem v Intune
titleSuffix: Microsoft Intune
description: Přečtěte si, jak zaregistrovat zařízení s Androidem v Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 7/23/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f276d98c-b077-452a-8835-41919d674db5
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d3d179af4a531134a543b070e5e70731231eda2c
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325487"
---
# <a name="enroll-android-devices"></a>Registrace zařízení s Androidem

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Jako správce Intune můžete zařízení s Androidem registrovat následujícími způsoby:
- Android Enterprise (nabízí sadu možností registrace, které uživatelům poskytují nejaktuálnější a zabezpečené funkce):
    - [**Pracovní profil Android Enterprise**](android-work-profile-enroll.md): pro osobní zařízení udělená oprávnění pro přístup k podnikovým datům. Správci můžou spravovat pracovní účty, aplikace a data. Osobní údaje na zařízení jsou oddělené od pracovních dat a správci neovládají osobní nastavení ani data. 
    - [**Vyhrazená podniková**](android-kiosk-enroll.md)platforma pro Android: pro zařízení vlastněná společností, jako je digitální podpis, tisk lístku nebo Správa inventáře. Správci omezí použití zařízení na omezenou sadu aplikací a webových odkazů. Uživatelé zároveň nemůžou na tomto zařízení přidávat jiné aplikace ani provádět jiné akce.
    - [**Plně spravovaná platforma Android Enterprise**](android-fully-managed-enroll.md): pro samostatná zařízení vlastněná společností, která slouží výhradně pro práci a nikoli pro osobní použití. Správci můžou spravovat celé zařízení a vynutilit ovládací prvky zásad nedostupné pro pracovní profily. 
- [**Správce zařízení s Androidem**](android-enroll-device-administrator.md), včetně zařízení se zabezpečením Samsung KNOX Standard a [zařízení Zebra](../configuration/android-zebra-mx-overview.md). 

## <a name="prerequisites"></a>Požadavky

Při přípravě na správu mobilních zařízení musíte nastavit autoritu pro správu mobilních zařízení (MDM) na **Microsoft Intune**. Pokyny k tomu najdete v článku [Nastavení autority MDM](../fundamentals/mdm-authority-set.md). Tato možnost se nastavuje jenom jednou při prvním nastavování Intune pro správu mobilních zařízení.

Pro zařízení vyráběná technologiemi Zebra může být potřeba udělit Portál společnosti dodatečná oprávnění v závislosti na možnostech konkrétního zařízení. [Rozšíření mobility na zařízeních Zebra](../configuration/android-zebra-mx-overview.md) obsahují další podrobnosti.

Pro zařízení se zabezpečením Samsung KNOX Standard jsou k dispozici [Další požadavky](android-samsung-knox-mobile-enroll.md).

## <a name="next-steps"></a>Další kroky

- [Nastavení registrace pracovních profilů pro Android Enterprise](android-work-profile-enroll.md)
- [Nastavení registrace zařízení se systémem Android Enterprise vyhrazené](android-kiosk-enroll.md)
- [Nastavení plně spravovaných registrů pro Android Enterprise](android-fully-managed-enroll.md)
- [Nastavení registrace Správce zařízení s Androidem](android-enroll-device-administrator.md)

