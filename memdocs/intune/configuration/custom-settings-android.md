---
title: Přidání vlastního nastavení do zařízení s Androidem v Microsoft Intune – Azure | Microsoft Docs
description: Přidejte nebo vytvořte vlastní profil pro zařízení s Androidem k vytvoření profilu Wi-Fi s předsdíleným klíčem, vytvoření profilu sítě VPN pro jednotlivé aplikace nebo povolení/blokování aplikací pro zařízení se Samsung Knox Standard v Microsoft Intune
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 494b3892-916e-4b40-9b67-61adec889bdf
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 43107ce98ee1c9d002b07470c224b2291819069b
ms.sourcegitcommit: 397ec824f1368dcf06c3870c89f52347852062bd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/23/2020
ms.locfileid: "85264103"
---
# <a name="use-custom-settings-for-android-devices-in-microsoft-intune"></a>Použití vlastních nastavení u zařízení s Androidem v Microsoft Intune

V Microsoft Intune můžete použít vlastní profil k přidání nebo vytvoření vlastního nastavení pro zařízení s Androidem. Vlastní profily jsou funkcí Intune. Jsou navržené tak, aby bylo možné přidat nastavení a funkce zařízení, které nejsou integrované do Intune.

Vlastní profily Androidu používají nastavení OMA-URI (Open Mobile Alliance Uniform Resource Identifier) ke konfiguraci různých funkcí zařízení s Androidem. Nastavení většinou používají výrobci mobilních zařízení k ovládání těchto funkcí.

Pomocí vlastního profilu můžete nakonfigurovat a přiřadit následující nastavení Androidu. Intune má v sobě integrovaná následující nastavení:

- [Vytvoření profilu Wi-Fi s předsdíleným klíčem](/intune/wi-fi-profile-shared-key)
- [Vytvoření profilu sítě VPN pro jednotlivé aplikace](/intune/android-pulse-secure-per-app-vpn)
- [Povolení a blokování aplikací pro zařízení se Samsung Knox Standard](/intune/samsung-knox-apps-allow-block)
- [Konfigurace webové ochrany v Rozšířené ochraně před internetovými útoky v programu Microsoft Defender pro Android](../protect/advanced-threat-protection.md#configure-web-protection-on-devices-that-run-android)

>[!IMPORTANT]
> Vlastní profil můžeme použít jenom ke konfiguraci uvedených nastavení. Zařízení s Androidem nezveřejňují úplný seznam nastavení OMA-URI, která můžete konfigurovat. Pokud chcete vidět další nastavení, pak pro ně hlasujte na [webu Intune Uservoice](https://microsoftintune.uservoice.com/forums/291681-ideas).

V tomto článku si ukážeme, jak vytvořit vlastní profil pro zařízení s Androidem.

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.
3. Zadejte následující nastavení:

    - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například **vlastní profil Android**.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.
    - **Platforma**: vyberte **Android**.
    - **Typ profilu**: vyberte **vlastní**.

4. V nabídce **Vlastní nastavení OMA-URI** vyberte **Přidat**. Zadejte následující nastavení:

    - **Název:** Zadejte jedinečný název pro nastavení OMA-URI, abyste ho snadno našli.
    - **Popis:** Zadejte popis, který nastavení stručně charakterizuje, a další důležité podrobnosti.
    - **OMA-URI:** Zadejte nastavení OMA-URI, které chcete použít.
    - **Datový typ**: vyberte datový typ, který budete používat pro toto nastavení OMA-URI. Možnosti:

      - Řetězec
      - Řetězec (soubor XML)
      - Datum a čas
      - Integer
      - Plovoucí desetinná čárka
      - Logická hodnota
      - Base64 (soubor)

    - **Hodnota:** Zadejte datovou hodnotu, kterou chcete přidružit k zadanému nastavení OMA-URI. Hodnota závisí na vybraném datovém typu. Pokud například vyberete položku **Datum a čas**, vyberte hodnotu z ovládacího prvku pro výběr data.

    Po přidání nastavení můžete vybrat **Exportovat**. **Export** vytvoří seznam všech hodnot, které jste přidali do souboru hodnot oddělených čárkou (.csv).

5. Výběrem **OK** uložte změny. Podle potřeby přidejte další nastavení.
6. Po dokončení vyberte **OK**  >  **vytvořit** a vytvořte profil Intune. Po dokončení se Váš profil zobrazí v seznamu **zařízení – konfigurační profily** .

## <a name="next-steps"></a>Další kroky

Profil je vytvořený, ale zatím se nepoužívá. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).

Vytvořte si [vlastní profil na zařízeních s Androidem Enterprise](custom-settings-android-for-work.md).
