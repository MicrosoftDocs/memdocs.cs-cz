---
title: Zjednodušení správy počítačů s Windows pomocí zásad
titleSuffix: Microsoft Intune
description: Popisuje zásady správy počítačů s Windows a nastavení pro Microsoft Intune Center.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/01/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: f0afda7e-f4c3-4bcd-b4bf-4304103cf73e
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: 275939c4c97b25f7e9b2ab179a7491d47801e48e
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79330239"
---
# <a name="use-policies-to-simplify-windows-pc-management"></a>Zjednodušení správy počítačů s Windows pomocí zásad

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

Při správě počítačů s Windows pomocí klienta softwaru Intune můžete použít jenom ty zásady, které jsou v konzole správce Intune uvedené v zásadách **Správa počítače**. Všechny ostatní zásady uvedené v konzole správce jsou určené jenom pro mobilní zařízení. Pomocí zásad **Správa počítače** můžete konfigurovat nastavení centra Microsoft Intune Center, řídit aktualizace počítačů a konfigurovat na počítačích bránu Windows Firewall.

![Šablony zásad pro počítače s Windows](./media/use-policies-to-simplify-windows-pc-management/pc_policy_template.png)

## <a name="manage-the-microsoft-intune-center"></a>Správa centra Microsoft Intune Center
Klientský software Intune se uživatelům zobrazí jako **Microsoft Intune Center**. Microsoft Intune Center uživatelům umožňuje:

- Získávat aplikace z portálu společnosti

- Kontrolovat aktualizace

- Spravovat Microsoft Intune Endpoint Protection

- Žádat o vzdálenou pomoc

Microsoft Intune Center se nainstaluje na všech spravovaných počítačích. V zásadách Intune můžete nakonfigurovat následující nastavení, která se uživatelům zobrazí v centru Microsoft Intune Center:

|Nastavení zásad|Podrobnosti|
|------------------|--------------------|
|**Název**|Jméno správce, který spravuje příslušný počítač<br />Maximální délka: 40 znaků|
|**Telefonní číslo**|Telefonní číslo správce, který spravuje příslušný počítač<br />Maximální délka: 20 znaků|
|**E-mailová adresa**|Emailová adresa správce, který spravuje příslušný počítač<br />Maximální délka: 40 znaků|
|**Název webu**|Název vašeho webu pro podporu uživatelů<br />>Maximální délka: 40 znaků|
|**Adresa URL webu**|Adresa URL vašeho webu podpory<br />Maximální délka: 150 znaků|
|**Poznámky**|Poznámka, která se zobrazuje uživatelům<br />Maximální délka: 120 znaků|

Informace o zásadách a nastaveních, které můžete konfigurovat pro počítače s Windows, najdete v následujících zdrojích:

- [Udržování počítačů s Windows v aktuálním stavu díky softwarovým aktualizacím v Microsoft Intune](keep-windows-pcs-up-to-date-with-software-updates-in-microsoft-intune.md) – Tyto zásady nutí spravované počítače vyhledávat a stahovat aktualizace softwaru od Microsoftu a třetích stran. Tyto aktualizace nezahrnují upgrady operačního systému (třeba z upgrade z Windows 7 na Windows 10 nebo upgrade starší verze Windows 10 na verzi novější).

- [Pomoc se zabezpečením počítačů s Windows pomocí služby Endpoint Protection pro Microsoft Intune](help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune.md) – Tato nastavení zahrnují plány kontrol a akce, které se mají provést při zjištění malwaru.

- [Pomoc při ochraně počítačů s Windows pomocí zásad brány Windows Firewall v Microsoft Intune](help-protect-windows-pcs-using-windows-firewall-policies-in-microsoft-intune.md) – Tyto zásady zjednodušují správu nastavení brány Windows Firewall na spravovaných počítačích.

## <a name="see-also"></a>Viz také

[Běžné úlohy správy počítačů s Windows pomocí klientského softwaru Intune](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)
