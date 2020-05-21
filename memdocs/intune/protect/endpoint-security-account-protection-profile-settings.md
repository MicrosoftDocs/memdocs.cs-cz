---
title: Nastavení zásad ochrany účtu zabezpečení koncového bodu služby Intune | Microsoft Docs
description: Nastavení zásad ochrany účtů zabezpečení koncových bodů v Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
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
ms.openlocfilehash: f4e67c434af9eb7f88c3e7d3997ef7c7d829c860
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431409"
---
# <a name="account-protection-policy-settings-for-endpoint-security-in-intune"></a>Nastavení zásad ochrany účtů pro zabezpečení koncových bodů v Intune

Podívejte se na nastavení, která můžete nakonfigurovat v části profily pro zásady *ochrany účtů* v uzlu zabezpečení koncového bodu služby Intune jako součást [zásady zabezpečení koncového bodu](../protect/endpoint-security-policy.md).

Podporované platformy a profily:

- **Windows 10 a novější**:
  - Profil: **ochrana účtů** *(Preview)*


## <a name="account-protection-profile"></a>Profil ochrany účtů

### <a name="account-protection"></a>Ochrana účtu

- **Blokovat Windows Hello pro firmy**

  Windows Hello pro firmy je alternativní metoda pro přihlašování do systému Windows tím, že nahrazujete hesla, čipové karty a virtuální čipové karty.
  - **Nenakonfigurováno** (*výchozí*) – zařízení zřídí Windows Hello pro firmy.
  - **Zakázané** – zařízení zřídí Windows Hello pro firmy.
  - **Povoleno** – zařízení nezřídí Windows Hello pro firmy pro žádného uživatele.
  
- **Povolení použití bezpečnostních klíčů pro přihlášení**

  Povolte klíč zabezpečení Windows Hello jako přihlašovací údaje pro všechny počítače v tenantovi.
  - **Nenakonfigurováno** (*výchozí*)
  - **Ano**

- **Zapnout ochranu Credential Guard**  
  [CSP: [] DeviceGuard](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard k zajištění ochrany používá hypervisor Windows. Credential Guard vyžaduje hardwarovou podporu pro zabezpečené spouštění a ochranu DMA. Toto nastavení je úspěšné jenom na zařízeních, která splňují hardwarové požadavky.
  - **Nenakonfigurováno** (*výchozí*) – zakáže použití Credential Guard, což je výchozí nastavení systému Windows.
  - **Povolit s uzamčením UEFI** – povolí ochranu přihlašovacích údajů a zablokuje, aby se vypnula, protože je nutné ručně vymazat konfiguraci rozhraní UEFI.
  - **Povolit bez zámku UEFI** – povolí ochranu přihlašovacích údajů a povolí, aby bylo vypnuté bez fyzického přístupu k počítači.

## <a name="next-steps"></a>Další kroky

[Zásady zabezpečení koncového bodu pro ochranu účtu](../protect/endpoint-security-account-protection-policy.md)
