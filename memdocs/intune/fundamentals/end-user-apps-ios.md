---
title: Jak uživatelé iOS/iPadOS získávají své aplikace
description: Metody zpřístupnění aplikací pro iOS/iPadOS koncovým uživatelům
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7e3135c1-df26-48c9-aa4c-cdab6168897a
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 957c63c760dcc576ab30bb85440d52833307818d
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79326863"
---
# <a name="how-your-iosipados-users-get-their-apps"></a>Jak uživatelé iOS/iPadOS získávají své aplikace

Tyto informace slouží k pochopení toho, jak a kde koncoví uživatelé získávají aplikace, které distribuujete pomocí Microsoft Intune.

**Požadované aplikace** – aplikace, které jsou vyžadované správcem a které se instalují na zařízení s nutností minimálního zásahu ze strany uživatele (v závislosti na platformě).

**Dostupné aplikace** – aplikace, které jsou v seznamu aplikace Portál společnosti a které si uživatel může volitelně nainstalovat.

**Spravované aplikace** – aplikace, které jde spravovat pomocí zásad a které jsou „zabalené“ službou Intune nebo sestavené pomocí sady Intune App SDK. Tyto aplikace je možné spravovat pomocí služby Intune a je na ně možné aplikovat zásady ochrany aplikací.

**Nespravované aplikace**– aplikace, které uživatelé můžou stahovat z App Storu pro iOS/iPadOS, které nejsou integrované se sadou Intune App SDK. Intune nemá žádnou kontrolu nad distribucí, správou nebo selektivním vymazáním těchto aplikací.  

Zaregistrovaní uživatelé můžou používat aplikace po klepnutí na následující dlaždice na obrazovce Aplikace v aplikaci Portál společnosti:

- **Všechny aplikace** zobrazí seznam všech aplikací na kartě VŠE na [webu Portál společnosti](https://portal.manage.microsoft.com).

- Po klepnutí na **Vybrané aplikace** se uživatelům zobrazí na webu Portál společnosti karta VYBRANÉ.

- **Kategorie** odkazují na webu Portál společnosti na kartu KATEGORIE.

![Obrazovka aplikací na Portálu společnosti pro iOS](./media/end-user-apps-ios/ios-cp-app-main-apps-screen.png)

Další informace o přidávání aplikací najdete v článku [Přidání aplikací do Microsoft Intune](../apps/apps-add.md).

## <a name="app-management-takeover"></a>Převzetí správy aplikací
Pokud je už aplikace nainstalovaná na zařízení koncového uživatele, zařízení s iOS/iPadOS zobrazí výstrahu, která umožňuje správu aplikace ve vaší organizaci. Koncový uživatel musí organizaci dovolit, aby před použitím konfigurace aplikace na spravovaném zařízení převzala správu aplikace. Pokud uživatel výstrahu zruší, bude se tato výstraha pravidelně zobrazovat, dokud bude zařízení spravované a přiřadíte aplikaci.  


![Obrázek výstrahy změny správy aplikace, která zobrazuje možnosti zrušení a Správa](./media/end-user-apps-ios/intune-app-management-confirmation-2002.png)

## <a name="see-also"></a>Viz také  

[Jak uživatelé s Androidem získávají svoje aplikace](end-user-apps-android.md)

[Jak uživatelé s Windows získávají svoje aplikace](end-user-apps-windows.md)
