---
title: Data z Intune odesílaná Googlu
titleSuffix: Microsoft Intune
description: Seznam dat, která Intune odesílá Googlu
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a5c3bec4-18ed-11e8-accf-0ed5f89f718b
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fa9b8bc49e9c5aaf6337988fd980115beea1200b
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329443"
---
# <a name="data-intune-sends-to-google"></a>Data z Intune odesílaná Googlu

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Pokud se na zařízení povolí správa zařízení s Androidem Enterprise, Microsoft Intune naváže spojení s Googlem a bude s ním sdílet informace o uživateli a o zařízení. Aby mohla služba Microsoft Intune navázat spojení, je napřed nutné vytvořit účet Google.

Následující tabulka uvádí data, která Microsoft Intune odesílá do Googlu, když je na daném zařízení povolená správa zařízení:


| Data odesílaná Googlu | Podrobnosti | Používáno pro | Příklad |
|:---:|:---:|:---:|:---:|
| EnterpriseId | Vytvoří se v Googlu po vytvoření vazby účtu Gmail s Intune. | Primární identifikátor používaný ke komunikaci mezi Intune a Googlem.  Tato komunikace zahrnuje nastavení zásad, správu zařízení a vytvoření nebo zrušení vazby Androidu s Intune. | Jedinečný identifikátor, příklad formátu: LC04eik8a6 |
| Text zásad | Vytvoří se v Intune při ukládání nových zásad aplikací nebo konfigurace. | Přiřazení zásad pro zařízení | Jde o kolekci všech nakonfigurovaných nastavení pro zásady aplikace nebo konfigurace. Může obsahovat informace o zákaznících, pokud se poskytly v rámci zásad, například názvy sítí, názvy aplikací a nastavení pro konkrétní aplikace. |
| Data zařízení | U zařízení pro scénáře s pracovními profily se začíná registrací do Intune. U zařízení pro scénáře se spravovanými zařízeními se začíná registrací v Googlu. | Informace o datech zařízení se posílají mezi Intune a Googlem při různých akcích, například při použití zásad, při správě zařízení a při obecném vykazování. | **Jedinečný identifikátor, který představuje název zařízení.** Příklad: enterprises/LC04ebru7b/devices/3592d971168f9ae4<br>**Jedinečný identifikátor, který představuje uživatelské jméno.** Příklad: Enterprises/LC04ebru7b/users/116838519924207449711<br>**Stav zařízení.** Příklady: Active (Aktivní), Disabled (Zakázáno), Provisioning (Zřizuje se).<br>**Stavy dodržování předpisů.** Příklady: Nastavení není podporováno, chybí požadované aplikace<br>**Informace o softwaru.** Příklady: verze softwaru a úroveň oprav.<br>**Informace o síti.** Příklady: IMEI, MEID, WifiMacAddress<br>**Nastavení zařízení.** Příklady: Informace o úrovních šifrování a o tom, jestli zařízení povoluje neznámé aplikace.<br> Příklad zprávy JSON najdete níže. |
| newPassword | Vytvoří se v Intune. | Resetuje heslo zařízení. | Řetězec představující nové heslo. |
| Uživatel Googlu | Google | Spravuje pracovní profil pro scénáře s pracovními profily (BYOD). | Jedinečný identifikátor, který představuje propojený účet Gmail. Příklad: 114223373813435875042 |
| Data aplikací | Vytvoří se v Intune při ukládání zásad aplikací. |  | Řetězec názvu aplikace. Příklad: app:com.microsoft.windowsintune.companyportal |
| Účet služby Enterprise | Vytvoří se v Googlu na žádost služby Intune. | Používá se u transakcí zahrnujících daného zákazníka pro ověřování mezi Intune a Googlem. | Má několik částí:<br> **Enterprise Id**: Bylo už popsáno.<br>**UPN**: Vygenerovaný hlavní název uživatele (UPN), který se používá při ověřování jménem zákazníka.<br>Příklad: w49d77900526190e26708c31c9e8a0@pfwp-commicrosoftonedfmdm2.google.com.iam.gserviceaccount.com<br>**Key**: Objekt blob s kódováním Base64, který se používá v žádostech o ověření, je uložený jako šifrovaný v této službě a vypadá takto:<br> Jedinečný identifikátor, který představuje klíč zákazníka.<br>Příklad: a70d4d53eefbd781ce7ad6a6495c65eb15e74f1f |


Pokud chcete ukončit používání správy zařízení s Androidem Enterprise v Microsoft Intune a odstranit data, je nutné deaktivovat správu zařízení s Androidem Enterprise v Microsoft Intune a také odstranit váš účet Google. Vyhledejte si v účtu Google postup pro správu účtu.


