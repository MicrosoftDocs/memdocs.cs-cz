---
title: Vlastní profil VPN pro jednotlivé aplikace pro Android v Microsoft Intune – Azure | Microsoft Docs
description: Naučte se vytvořit profil sítě VPN pro jednotlivé aplikace pro zařízení s Androidem, která spravuje Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d035ebf5-85f4-4001-a249-75d24325061a
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d58ab666929e1e28cab4e19f2e2cec668f428452
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "80083877"
---
# <a name="use-a-microsoft-intune-custom-profile-to-create-a-per-app-vpn-profile-for-android-devices"></a>K vytvoření profilu VPN pro aplikaci pro zařízení s Androidem můžete použít vlastní profil Microsoft Intune.

Pro zařízení s Androidem verze 5.0 a novější spravovaná pomocí Intune můžete vytvořit profil VPN pro jednotlivé aplikace. Nejdříve vytvoříte profil VPN, který používá typ připojení Pulse Secure nebo Citrix. Potom vytvoříte vlastní zásadu konfigurace, která přidruží tento profil ke konkrétním aplikacím.

> [!NOTE]
> Pokud chcete používat síť VPN pro jednotlivé aplikace na zařízeních s Androidem Enterprise, můžete použít i tyto kroky. Doporučuje se ale použít [zásady konfigurace aplikací](../apps/app-configuration-policies-use-android.md) pro klientská aplikace VPN.

Po přiřazení zásad pro skupiny zařízení nebo uživatelů Android by uživatelé měli spustit klienta VPN Pulse Secure nebo Citrix. Klient VPN pak umožní jenom provoz ze zadaných aplikací na používání otevřeného připojení VPN.

> [!NOTE]
>
> Pro tento profil se podporují jenom připojení Pulse Secure a Citrix.

## <a name="step-1-create-a-vpn-profile"></a>Krok 1: Vytvoření profilu sítě VPN

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Konfigurace zařízení** > **profily** > konfigurace**vytvořit profil**.
3. Zadejte tyto vlastnosti:

    - **Platforma**: vyberte **Správce zařízení s Androidem**.
    - **Profil**: vyberte **VPN**.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například **profil VPN pro aplikaci pro zařízení s Androidem pro celou firmu**.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.
7. V **nastavení konfigurace**nakonfigurujte požadovaná nastavení v profilu:

    - [Nastavení sítě VPN pro zařízení s Androidem pro správce](vpn-settings-android.md)

    Poznamenejte si hodnotu **název připojení** , kterou zadáte při vytváření profilu sítě VPN. Tento název je potřeba v dalším kroku. V tomto příkladu je název připojení **MyAppVpnProfile**.

8. Vyberte **Další**a pokračujte v vytváření profilu. Další informace najdete v tématu [Vytvoření profilu sítě VPN](vpn-settings-configure.md#create-the-profile).

## <a name="step-2-create-a-custom-configuration-policy"></a>Krok 2: Vytvoření vlastní zásady konfigurace

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Konfigurace zařízení** > **profily** > konfigurace**vytvořit profil**.
3. Zadejte tyto vlastnosti:

    - **Název**: zadejte popisný název vlastního profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například **vlastní profil VPN OMA-URI pro celou firmu**.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.
    - **Platforma**: vyberte **Správce zařízení s Androidem**.
    - **Typ profilu**: vyberte **vlastní**.

4. Vyberte **Nastavení** > **Konfigurovat**.
5. V podokně **Vlastní nastavení OMA-URI** zvolte **Přidat**.
    - **Název**: zadejte název vašeho nastavení.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.
    - **OMA-URI**: zadejte `./Vendor/MSFT/VPN/Profile/*Name*/PackageList`, kde *název* je název připojení, které jste si poznamenali v kroku 1. V tomto příkladu je `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/PackageList`řetězec.
    - **Datový typ**: zadejte **řetězec**.
    - **Hodnota**: zadejte středníkem oddělený seznam balíčků, které chcete přidružit k profilu. Například pokud chcete, aby připojení k síti VPN používal Excel a prohlížeč Google Chrome, zadejte `com.microsoft.office.excel;com.android.chrome`.

    > [!div class="mx-imgBorder"]
    >![Příklad vlastních zásad sítě VPN pro správce zařízení s Androidem](./media/android-pulse-secure-per-app-vpn/android_per_app_vpn_oma_uri.png)

### <a name="set-your-app-list-to-blacklist-or-whitelist-optional"></a>Nastavení seznamu aplikací jako zakázaných nebo povolených (volitelné)

Pomocí hodnoty **zakázané** zadejte seznam aplikací, které *nemůžou* používat připojení VPN. Všechny ostatní aplikace se připojují prostřednictvím VPN. Nebo pomocí hodnoty seznamu **povolených** adres zadejte seznam aplikací, které *můžou* používat připojení VPN. Aplikace, které nejsou v seznamu, se nepřipojují prostřednictvím sítě VPN.

1. V podokně **Vlastní nastavení OMA-URI** zvolte **Přidat**.
2. Zadejte název nastavení.
3. Do pole **OMA-URI**zadejte `./Vendor/MSFT/VPN/Profile/*Name*/Mode`, kde *název* je název profilu VPN, který jste si poznamenali v kroku 1. V našem příkladu je `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/Mode`řetězec.
4. Do **datového typu**zadejte **řetězec**.
5. Do pole **Hodnota** zadejte **BLACKLIST** nebo **WHITELIST**.

## <a name="step-3-assign-both-policies"></a>Krok 3: Přiřazení obou zásad

[Přiřaďte oba profily zařízení](device-profile-assign.md) požadovaným uživatelům nebo zařízením.

## <a name="next-steps"></a>Další kroky

- Seznam všech nastavení sítě VPN pro správce zařízení s Androidem najdete v tématu [nastavení zařízení s Androidem konfigurace sítě VPN](vpn-settings-android.md).
- Další informace o nastavení sítě VPN a Intune najdete v tématu [Konfigurace nastavení sítě VPN v Microsoft Intune](vpn-settings-configure.md).
