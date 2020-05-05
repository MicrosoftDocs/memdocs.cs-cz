---
title: Kódy nedodržování předpisů
titleSuffix: Configuration Manager
description: Technické informace o možných kódech z klienta Configuration Manager, který nedodržuje zásady BitLockeru
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6c28fa29-fc97-49ef-9fc3-cb062bdba908
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e8ee130929605f8087eb7fbef55e8a27618c3aed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722050"
---
# <a name="non-compliance-codes"></a>Kódy nedodržování předpisů

*Platí pro: Configuration Manager (Current Branch)*

<!--3601034-->

Rozhraní WMI na klientovi poskytuje následující kódy, které nedodržují předpisy. Popisuje také důvody, proč konkrétní zařízení hlásí nedodržující předpisy.

Existují různé způsoby, jak zobrazit rozhraní WMI. Například použijte následující příkaz prostředí PowerShell:

``` PowerShell
(Get-WmiObject -Class mbam_Volume -Namespace root\microsoft\mbam).ReasonsForNoncompliance
```

> [!TIP]
> Pokud je zařízení v souladu s předpisy, tento příkaz nevrátí žádnou hodnotu.
>
> Můžete také zaškrtnout `Compliant` atribut této třídy, což znamená `1` , že zařízení dodržuje předpisy.

|Kód nekompatibility|Důvod pro nedodržování předpisů|
|--- |--- |
|0|Síla šifry není AES 256.|
|1|Zásady BitLockeru vyžadují, aby byl tento svazek zašifrovaný, ale ne.|
|2|Zásada BitLockeru vyžaduje, aby tento svazek *nebyl* zašifrovaný, ale je.|
|3|Zásada BitLockeru vyžaduje, aby tento svazek používal ochranu čipem TPM, ale ne.|
|4|Zásada BitLockeru vyžaduje, aby tento svazek používal ochranu pomocí čipu TPM a PIN kódu, ale ne.|
|5|Zásada nástroje BitLocker nepovoluje, aby zařízení, která nejsou TPM, mohla hlásit kompatibilní.|
|6|Svazek má ochranu čipem TPM, ale čip TPM není viditelný.|
|7|Zásada BitLockeru vyžaduje, aby tento svazek používal ochranu heslem, ale ten ho nemá.|
|8|Zásada BitLockeru vyžaduje, aby *Tento svazek* nepoužíval ochranu heslem, ale ten ho obsahuje.|
|9|Zásada BitLockeru vyžaduje, aby tento svazek používal ochranu pomocí automatického odemknutí, ale ten ho nemá.|
|10|Zásada BitLockeru vyžaduje, aby *Tento svazek* nepoužíval ochranu pomocí automatického odemknutí, ale ten ho obsahuje.|
|11|BitLocker detekuje konflikt zásad, který brání tomu, aby nahlásí tento svazek jako vyhovující.|
|12|Systémový svazek je nutný k zašifrování svazku operačního systému, ale není k dispozici.|
|13|Ochrana svazku je pozastavena.|
|14|Ochrana pomocí automatického odemknutí je nebezpečná, pokud není svazek operačního systému zašifrovaný.|
|15|Zásada vyžaduje minimální šifrováním sílu XTS-AES-128, skutečná síla šifrováním je slabší.|
|16|Zásada vyžaduje minimální šifrováním sílu XTS-AES-256, skutečná síla šifrováním je slabší.|
