---
title: Data JAMF pro odesílá do Intune.
titleSuffix: Microsoft Intune
description: Projděte si seznam dat, která Jamf pro odesílá do Microsoft Intune při integraci Jamf pro pro správu počítačů Mac s Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/16/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: elocholi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e9b943ca03f54a976061c19f4ce60a94283640c0
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79329439"
---
# <a name="data-jamf-pro-sends-to-intune"></a>Data, která Jamf Pro odesílaná do Intune

Pokud ke správě počítačů Mac koncových uživatelů s Intune používáte [Jamf pro](https://www.jamf.com) , zachytí Jamf pro informace o inventáři spravovaných zařízení MacOS. 

## <a name="data"></a>Data  
Seznam dat, která Jamf pro sdílí s Intune, najdete v [příloze: informace o inventáři sdílené pomocí Microsoft Intune](https://docs.jamf.com/technical-papers/jamf-pro/microsoft-intune/10.9.0/Appendix__Inventory_Information_Shared_with_Microsoft_Intune.html) v technické dokumentaci k Jamf pro. 

<!--  
Jamf Pro reports the following information to Intune:  

* Device Azure AD ID
* JAMF Inventory State (inventory state of a computer checked in with Jamf Pro within the last 24 hours)
* OS Version
* User Azure AD ID
* Encrypted (FileVault 2)
* Gatekeeper Status
* Password: minimum number of character sets
* Password expiration (days)
* Password Type - simple, alphanumeric, or unknown
* Prevent Auto Login
* Required Passcode Length
* Password: number of previous passwords to prevent reuse
* System Integrity Protection
* Last Check-In Time
* Architecture Type
* Available RAM Slots
* Battery Capacity
* Boot ROM
* Bus Speed
* Cache Size
* Device Name
* Domain Join
* Jamf ID
* MAC address
* Make
* Model
* Model Identifier
* NIC Speed
* Number of Cores
* Number of Processors
* OS
* Platform
* Processor Speed
* Processor Type
* Secondary MAC Address
* Serial Number
* SMC Version
* Total RAM
* UDID
* User Email
--> 

<!-- 
You can remove a Jamf-managed device from the Intune console by selecting **Delete** in the **All devices** view. Bulk device deletion can be enabled by selecting multiple devices and clicking **Delete**.
-->

## <a name="next-steps"></a>Další kroky
Získejte informace o tom, jak [Odebrat Jamf zařízení spravované v dokumentaci pro Jamf pro](https://www.jamf.com/jamf-nation/articles/80/unmanaging-computers-while-preserving-their-inventory-information). Pro další pomoc si můžete také [poJamf podporu](https://www.jamf.com/support/) a pokaždé, když zadáte lístek podpory. 

