---
title: Zásady pro aplikace Office
titleSuffix: Microsoft Intune
description: Pochopení zásad, které jsou k dispozici pro aplikace Office
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: ca558b40ad3d006aa764819a0fbccc16a03fd0e2
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/10/2020
ms.locfileid: "89644010"
---
# <a name="policies-for-office-apps"></a>Zásady pro aplikace Office

Intune poskytuje zásady určené konkrétně pro aplikace systém Microsoft Office. Můžete vybrat konkrétní možnosti pro vytvoření zásad správy mobilních aplikací pro mobilní aplikace Office, které se připojují ke službě Microsoft 365 Services. K dispozici je celá řada zásad pro aplikace Office, které můžete přidat do Microsoft Intune a použít u skupin koncových uživatelů.

Mezi příklady některých zásad aplikace Office stačí následující:
- Microsoft Word: vypnutí *chráněného zobrazení pro přílohy otevřené z Outlooku*
- Microsoft Visio: *blokování spouštění maker v souborech Office z Internetu*
- Microsoft Project: *Povolení důvěryhodných umístění v síti*
- Microsoft Publisher: *úroveň zabezpečení automatizace vydavatele*
- Microsoft PowerPoint: vypnutí *chráněného zobrazení pro přílohy otevřené z Outlooku*

> [!NOTE]
> Když zvolíte, že se mají nakonfigurovat jednotlivé konkrétní zásady aplikace, poskytnou se další podrobnosti o zásadách. Seznam zásad Office můžete filtrovat tak, aby se rychle vybraly Doporučené zásady **standardních hodnot zabezpečení** .

Přístup k místním poštovním schránkám systému Exchange můžete chránit také vytvořením zásad ochrany aplikací Intune pro Outlook pro iOS/iPadOS a Androidem s povoleným hybridním moderním ověřováním. Než tuto funkci použijete, musíte splnit požadavky na používání služby zásady cloudu Office. Zásady ochrany aplikací se nepodporují pro jiné aplikace, které se připojují k místním službám Exchange nebo SharePoint. Související informace najdete v tématu [Přehled služby zásady cloudu Office pro aplikace Microsoft 365 pro podniky](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service).

## <a name="prerequisites"></a>Požadavky

Musíte splňovat požadavky na použití zásad pro aplikace Office. Další informace najdete v tématu [požadavky na používání služby zásady cloudu Office](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service#requirements-for-using-the-office-cloud-policy-service).

## <a name="to-add-an-office-app-policy"></a>Přidání zásady aplikace pro Office

Po nastavení Intune pro vaši organizaci můžete vytvořit zásady aplikace pro Office.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Apps**  >  **zásady aplikací pro aplikace Office**  >  **vytvořit**.
3. Přidejte následující hodnoty:
    - **Název:** Zadejte název nové zásady (povinné).
    - **Popis:** Volitelně zadejte popis.
    - **Vyberte typ:** Vyberte, jak se tato konfigurace zásady použije.
    - **Vybrat skupinu:** Vyberte skupinu pro tuto konfiguraci zásad.
    - **Konfigurace zásad:** Vyberte zásadu Office, kterou chcete použít. Zadaný seznam můžete seřadit podle zásad, platformy, aplikace, doporučení a stavu.
4. Vyberte **Vytvořit**. Zásada se vytvoří a zobrazí se v tabulce v podokně **Konfigurace zásad** .

   > [!TIP]
   > Podokno **Konfigurace zásad** poskytuje **stav** pro každou zásadu.

## <a name="additional-information"></a>Další informace

- [Přehled služby cloudové zásady Office pro aplikace Microsoft 365 pro podniky](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service)
- [Použití nastavení zásad ke správě řízení ochrany osobních údajů pro aplikace Microsoft 365 pro podniky](https://docs.microsoft.com/deployoffice/privacy/manage-privacy-controls)
- [Použití předvoleb ke správě řízení ochrany osobních údajů pro systém Office pro Mac](https://docs.microsoft.com/deployoffice/privacy/mac-privacy-preferences)
- [Použití předvoleb ke správě řízení ochrany osobních údajů pro Office na zařízeních s iOS](https://docs.microsoft.com/deployoffice/privacy/ios-privacy-preferences)
- [Použití nastavení zásad ke správě řízení ochrany osobních údajů pro Office na zařízeních s Androidem](https://docs.microsoft.com/deployoffice/privacy/android-privacy-controls)

## <a name="next-steps"></a>Další kroky

- [Monitorování informací a přiřazení aplikace pomocí Microsoft Intune](apps-monitor.md)