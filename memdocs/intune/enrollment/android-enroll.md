---
title: Registrace zařízení s Androidem v Intune
titleSuffix: Microsoft Intune
description: Přečtěte si, jak zaregistrovat zařízení s Androidem v Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 7/23/2019
ms.topic: overview
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
ms.openlocfilehash: b2a948b99abed1f2f7cb988016d047e5d1a86c11
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2020
ms.locfileid: "90814983"
---
# <a name="enroll-android-devices"></a>Registrace zařízení s Androidem

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Jako správce Intune můžete zařízení s Androidem registrovat následujícími způsoby:
- Android Enterprise (nabízí sadu možností registrace, které uživatelům poskytují nejaktuálnější a zabezpečené funkce):
    - [**Pracovní profil Android Enterprise**](android-work-profile-enroll.md): pro osobní zařízení udělená oprávnění pro přístup k podnikovým datům. Správci můžou spravovat pracovní účty, aplikace a data. Osobní údaje na zařízení jsou oddělené od pracovních dat a správci neovládají osobní nastavení ani data. 
    - [**Vyhrazená podniková**](android-kiosk-enroll.md)platforma pro Android: pro zařízení vlastněná společností, jako je digitální podpis, tisk lístku nebo Správa inventáře. Správci omezí použití zařízení na omezenou sadu aplikací a webových odkazů. Uživatelé zároveň nemůžou na tomto zařízení přidávat jiné aplikace ani provádět jiné akce.
    - [**Plně spravovaná platforma Android Enterprise**](android-fully-managed-enroll.md): pro samostatná zařízení vlastněná společností, která slouží výhradně pro práci a nikoli pro osobní použití. Správci můžou spravovat celé zařízení a vynutilit ovládací prvky zásad nedostupné pro pracovní profily.
    - [**Android Enterprise – vlastněný s pracovním profilem**](android-corporate-owned-work-profile-enroll.md): pro samostatná zařízení vlastněná společností, která jsou určená pro podnikové a osobní použití.
- [**Správce zařízení s Androidem**](android-enroll-device-administrator.md), včetně zařízení se zabezpečením Samsung KNOX Standard a [zařízení Zebra](../configuration/android-zebra-mx-overview.md). V oblastech, kde je k dispozici Android Enterprise, Google podporuje pohyb od správy zařízení (DA) tím, že snižuje podporu správy v nových verzích Androidu. Pokud však nejsou k dispozici Android Enterprise nebo GMS, budete chtít použít Správce zařízení a seznámit se s těmito změnami. Další informace najdete v části [je Android Enterprise k dispozici ve své zemi](https://support.google.com/work/android/answer/6270910)?

## <a name="prerequisites"></a>Požadavky

Při přípravě na správu mobilních zařízení musíte nastavit autoritu pro správu mobilních zařízení (MDM) na **Microsoft Intune**. Pokyny k tomu najdete v článku [Nastavení autority MDM](../fundamentals/mdm-authority-set.md). Tato možnost se nastavuje jenom jednou při prvním nastavování Intune pro správu mobilních zařízení.

V případě Androidu Enterprise se podívejte na následující článek podpory od společnosti Google a ujistěte se, že je Android Enterprise k dispozici ve vaší zemi nebo oblasti: https://support.google.com/work/android/answer/6270910

Pro zařízení vyráběná technologiemi Zebra může být potřeba udělit Portál společnosti dodatečná oprávnění v závislosti na možnostech konkrétního zařízení. [Rozšíření mobility na zařízeních Zebra](../configuration/android-zebra-mx-overview.md) obsahují další podrobnosti.

Pro zařízení se zabezpečením Samsung KNOX Standard jsou k dispozici [Další požadavky](android-samsung-knox-mobile-enroll.md).

## <a name="next-steps"></a>Další kroky

- [Nastavení registrace pracovních profilů pro Android Enterprise](android-work-profile-enroll.md)
- [Nastavení registrace zařízení se systémem Android Enterprise vyhrazené](android-kiosk-enroll.md)
- [Nastavení plně spravovaných registrů pro Android Enterprise](android-fully-managed-enroll.md)
- [Nastavení registrace Správce zařízení s Androidem](android-enroll-device-administrator.md)

