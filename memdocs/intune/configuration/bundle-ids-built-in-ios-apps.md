---
title: ID sady pro iOS/iPadOS pro integrované aplikace v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Podívejte se na seznam ID sad pro integrované aplikace pro iOS a iPadOS. Pomocí těchto ID sady prostředků explicitně povolte aplikace v konfiguračních profilech zařízení a zásadách v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c7de0b978c24f28988c62854a249505a0598db95
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "80084083"
---
# <a name="bundle-ids-for-built-in-ios-and-ipados-apps-you-can-use-in-intune"></a>ID sady prostředků pro integrované aplikace pro iOS a iPadOS, které můžete použít v Intune

Když konfigurujete funkce na zařízeních s iOS/iPadOS, můžete taky přidat integrované aplikace na zařízení se systémem iOS/iPadOS. Tento článek obsahuje seznam ID sady prostředků některých běžných integrovaných aplikací pro iOS a iPadOS. Pokud chcete najít ID sady prostředků jiných aplikací, obraťte se na dodavatele softwaru. Viz seznam [identifikátorů ID sady iOS/IPadOS](https://support.apple.com/guide/mdm/ios-bundle-ids-mdm90f60c1ce/web) společnosti Apple (otevře web společnosti Apple).

## <a name="bundle-ids"></a>ID sady prostředků

| ID sady prostředků                   | Název aplikace     | Vydavatel |
|-----------------------------|--------------|-----------|
| com.apple.AppStore          | App Store    | Apple     |
| com. Apple. Store. Jolly       | Apple Store  | Apple     |
| com.apple.calculator        | Kalkulačka   | Apple     |
| com.apple.mobilecal         | Kalendář     | Apple     |
| com.apple.camera            | Camera       | Apple     |
| com.apple.mobiletimer       | Clock        | Apple     |
| com. Apple. klipy             | Klip        | Apple     |
| com.apple.compass           | Kompas      | Apple     |
| com.apple.MobileAddressBook | Kontakty     | Apple     |
| com.apple.facetime          | FaceTime     | Apple     |
| com. Apple. DocumentsApp      | Soubory        | Apple     |
| com.apple.mobileme.fmf1     | Najít přátele | Apple     |
| com.apple.mobileme.fmip1    | Najít iPhone  | Apple     |
| com.apple.gamecenter        | Herní centrum  | Apple     |
| com.apple.mobilegarageband  | GarageBand   | Apple     |
| com.apple.Health            | Stav       | Apple     |
| com. Apple. Home              | Domů         | Apple     |
| com.apple.iBooks            | iBooks       | Apple     |
| com. Apple. iMovie            | iMovie       | Apple     |
| com. Apple. itunesconnect. Mobile | Připojení iTunes | Apple |
| com.apple.MobileStore       | iTunes Store | Apple     |
| com.apple.itunesu           | iTunes U     | Apple     |
| com.apple.Keynote           | Keynote      | Apple     |
| com.apple.mobilemail        | Pošta         | Apple     |
| com.apple.Maps              | Maps         | Apple     |
| com. Apple. Measure           | Measure      | Apple     |
| com.apple.MobileSMS         | Zprávy     | Apple     |
| com.apple.Music             | Hudba        | Apple     |
| com.apple.news              | Novinky         | Apple     |
| com.apple.mobilenotes       | Poznámky        | Apple     |
| com.apple.Numbers           | Čísla      | Apple     |
| com.apple.Pages             | Stránky        | Apple     |
| com. Apple. mobilephone       | Telefon        | Apple     |
| com.apple.Photo-Booth       | Photo Booth  | Apple     |
| com.apple.mobileslideshow   | Fotky       | Apple     |
| com.apple.podcasts          | Podcasty     | Apple     |
| com.apple.reminders         | Připomínky    | Apple     |
| com.apple.mobilesafari      | Safari       | Apple     |
| com.apple.Preferences       | Nastavení     | Apple     |
| com. Apple. Shortcuts         | Zástupci    | Apple     |
| com. Apple. SiriViewService   | Siri         | Apple     |
| com.apple.stocks            | Stocks       | Apple     |
| com.apple.tips              | Tipy         | Apple     |
| com.apple.tv                | TV           | Apple     |
| com.apple.videos            | Videa       | Apple     |
| com.apple.VoiceMemos        | Diktafon   | Apple     |
| com.apple.Passbook          | Wallet       | Apple     |
| com.apple.Bridge            | Watch        | Apple     |
| com.apple.weather           | Weather      | Apple     |

## <a name="next-steps"></a>Další kroky

Pomocí těchto ID sady prostředků můžete nakonfigurovat [funkce zařízení](ios-device-features-settings.md) a [Povolit nebo omezit některá nastavení](device-restrictions-ios.md) zařízení s iOS/iPadOS.
