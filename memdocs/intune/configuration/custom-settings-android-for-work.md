---
title: Přidání vlastních nastavení do zařízení s Androidem Enterprise v Microsoft Intune – Azure | Microsoft Docs
description: Přidání nebo vytvoření vlastního profilu pro zařízení s Androidem Enterprise v Microsoft Intune
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 4724d6e5-05e5-496c-9af3-b74f083141f8
ms.reviewer: chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 827b5eb8b65aa59212b9ef990def3c5f191baf7c
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79323891"
---
# <a name="use-custom-settings-for-android-enterprise-devices-in-microsoft-intune"></a>Použití vlastních nastavení u zařízení s Androidem Enterprise v Microsoft Intune

Pomocí Microsoft Intune můžete přidat nebo vytvořit vlastní nastavení pro zařízení se systémem Android Enterprise Work Profile pomocí vlastního profilu. Vlastní profily jsou funkcí Intune. Jsou navržené tak, aby bylo možné přidat nastavení a funkce zařízení, které nejsou integrované do Intune.

Vlastní profily pro Android Enterprise používají nastavení OMA-URI (Open Mobile Alliance Uniform Resource Identifier) k ovládání funkcí zařízení s Androidem Enterprise. Nastavení většinou používají výrobci mobilních zařízení k ovládání těchto funkcí.

Intune podporuje následující omezený počet vlastních profilů pro Android Enterprise:

- ./Vendor/MSFT/WiFi/Profile/SSID/Settings: [Vytvoření profilu Wi-Fi s předsdíleným klíčem](wi-fi-profile-shared-key.md) obsahuje několik příkladů.
- ./Vendor/MSFT/VPN/Profile/Name/PackageList: [Vytvoření profilu sítě VPN pro jednotlivé aplikace](android-pulse-secure-per-app-vpn.md) obsahuje několik příkladů.
- ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste: viz [příklad](#example) v tomto článku. Toto nastavení je také k dispozici v uživatelském rozhraní. Další informace najdete v tématu [nastavení zařízení s Androidem Enterprise pro povolení nebo omezení funkcí](device-restrictions-android-for-work.md).

Pokud potřebujete další nastavení, přečtěte si téma [OEMConfig for Android Enterprise](android-oem-configuration-overview.md).

V tomto článku si ukážeme, jak vytvořit vlastní profil pro zařízení s Androidem Enterprise. Najdete zde také příklad na vytvoření vlastního profilu, který blokuje kopírování a vložení.

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.
3. Zadejte následující nastavení:

    - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například **vlastní profil Android Enterprise**.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.
    - **Platforma**: vyberte **Android Enterprise**.
    - **Typ profilu**: vyberte **vlastní**.

4. V nabídce **Vlastní nastavení OMA-URI** vyberte **Přidat**. Zadejte následující nastavení:

    - **Název:** Zadejte jedinečný název pro nastavení OMA-URI, abyste ho snadno našli.
    - **Popis:** Zadejte popis, který nastavení stručně charakterizuje, a další důležité podrobnosti.
    - **OMA-URI:** Zadejte nastavení OMA-URI, které chcete použít.
    - **Datový typ**: vyberte datový typ, který budete používat pro toto nastavení OMA-URI. Možnosti:

      - String
      - Řetězec (soubor XML)
      - Datum a čas
      - Celé číslo
      - Číslo s plovoucí desetinnou čárkou
      - Logická hodnota
      - Base64 (soubor)

    - **Hodnota:** Zadejte datovou hodnotu, kterou chcete přidružit k zadanému nastavení OMA-URI. Hodnota závisí na vybraném datovém typu. Pokud například vyberete položku **Datum a čas**, vyberte hodnotu z ovládacího prvku pro výběr data.

    Po přidání nastavení můžete vybrat **Exportovat**. **Export** vytvoří seznam všech hodnot, které jste přidali do souboru hodnot oddělených čárkou (.csv).

5. Výběrem **OK** uložte změny. Podle potřeby přidejte další nastavení.
6. Po dokončení vyberte **OK** > **vytvořit** a vytvořte profil Intune. Po dokončení se Váš profil zobrazí v seznamu **zařízení – konfigurační profily** .

## <a name="example"></a>Příklad

V tomto příkladu vytvoříte vlastní profil, který na zařízeních s Androidem Enterprise zakazuje kopírovat a vkládat obsah mezi pracovními a osobními aplikacemi.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.
3. Zadejte následující nastavení:

    - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Zadejte například příkaz **Android s blokem s příkazem Kopírovat vložit vlastní profil**.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.
    - **Platforma**: vyberte **Android Enterprise**.
    - **Typ profilu**: vyberte **vlastní**.

4. V nabídce **Vlastní nastavení OMA-URI** vyberte **Přidat**. Zadejte následující nastavení:

    - **Název:** Zadejte třeba `Block copy and paste`.
    - **Popis:** Zadejte třeba `Blocks copy/paste between work and personal apps`.
    - **OMA-URI:** Zadejte `./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste`.
    - **Datový typ**: vyberte **logickou** hodnotu, aby byla hodnota tohoto OMA-URI **true** nebo **false**.
    - **Hodnota**: vyberte **hodnotu true**.

5. Po zadání nastavení byste měli mít podobné prostředí jako na následujícím obrázku:

    ![Blokování kopírování a vkládání v pracovním profilu Androidu](./media/custom-settings-android-for-work/custom-policy-afw-copy-paste.png)

Když tento profil přiřadíte spravovaným zařízením s Androidem Enterprise, bude kopírování a vkládání mezi aplikacemi v pracovních a osobních profilech zablokované.

## <a name="next-steps"></a>Další kroky

Profil je vytvořený, ale zatím se nepoužívá. Dále [Přiřaďte profil](device-profile-assign.md) a [sledujte jeho stav](device-profile-monitor.md).

Vytvořte si [vlastní profil na zařízeních s Androidem](custom-settings-android.md).
