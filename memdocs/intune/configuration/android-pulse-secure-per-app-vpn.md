---
title: Vlastní profil VPN pro jednotlivé aplikace pro Android
titleSuffix: Microsoft Intune
description: Zjistěte, jak pro zařízení s Androidem spravovaná pomocí Microsoft Intune vytvořit profil VPN pro aplikaci.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/21/2019
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
ms.openlocfilehash: 9fbcf60d3707097a323a05bf36d2cfe3902d5214
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325607"
---
# <a name="use-a-microsoft-intune-custom-profile-to-create-a-per-app-vpn-profile-for-android-devices"></a>K vytvoření profilu VPN pro aplikaci pro zařízení s Androidem můžete použít vlastní profil Microsoft Intune.

Pro zařízení s Androidem verze 5.0 a novější spravovaná pomocí Intune můžete vytvořit profil VPN pro jednotlivé aplikace. Nejdříve vytvoříte profil VPN, který používá typ připojení Pulse Secure nebo Citrix. Potom vytvoříte vlastní zásadu konfigurace, která přidruží tento profil ke konkrétním aplikacím.

> [!NOTE]
> Pokud chcete používat síť VPN pro jednotlivé aplikace na zařízeních s Androidem Enterprise, můžete použít i tyto kroky. Doporučuje se ale použít [zásady konfigurace aplikací](../apps/app-configuration-policies-use-android.md) pro klientská aplikace VPN.

Po přiřazení zásad pro skupiny zařízení nebo uživatelů Android by uživatelé měli spustit klienta VPN Pulse Secure nebo Citrix. Klient VPN pak umožní provoz jenom z určených aplikací, které budou moct používat otevřené připojení VPN.

> [!NOTE]
>
> Pro tento profil se podporují jenom připojení Pulse Secure a Citrix.

## <a name="step-1-create-a-vpn-profile"></a>Krok 1: Vytvoření profilu sítě VPN

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.
3. Zadejte následující vlastnosti:

    - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například **profil VPN pro aplikaci pro Android pro celou firmu**.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.
    - **Platforma**: vyberte **Android**.
    - **Typ profilu**: vyberte **VPN**.

4. Zvolte **Nastavení** > **Konfigurovat**. Pak nakonfigurujte profil sítě VPN. Další informace najdete v tématu [Konfigurace nastavení sítě VPN](vpn-settings-configure.md) a [nastavení sítě VPN v Intune pro zařízení s Androidem](vpn-settings-android.md).

Poznamenejte si hodnotu **Název připojení**, kterou zadáváte při vytváření profilu VPN. Tento název bude potřeba v dalším kroku. Příklad: **profil_VPN_pro_moje_aplikace**.

## <a name="step-2-create-a-custom-configuration-policy"></a>Krok 2: Vytvoření vlastní zásady konfigurace

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **konfiguračních profilech** > **vytvořit profil**.
3. Zadejte následující vlastnosti:

    - **Název**: zadejte popisný název vlastního profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například **vlastní profil VPN OMA-URI pro celou firmu**.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.
    - **Platforma**: vyberte **Android**.
    - **Typ profilu**: vyberte **vlastní**.

4. Zvolte **Nastavení** > **Konfigurovat**.
5. V podokně **Vlastní nastavení OMA-URI** zvolte **Přidat**.
    - **Název**: zadejte název vašeho nastavení.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.
    - **OMA-URI**: zadejte `./Vendor/MSFT/VPN/Profile/*Name*/PackageList`, kde *název* je název připojení, které jste si poznamenali v kroku 1. V tomto příkladu je řetězec `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/PackageList`.
    - **Datový typ**: zadejte **řetězec**.
    - **Hodnota**: zadejte středníkem oddělený seznam balíčků, které chcete přidružit k profilu. Například pokud chcete, aby připojení k síti VPN používal Excel a prohlížeč Google Chrome, zadejte `com.microsoft.office.excel;com.android.chrome`.

![Příklad vlastní zásady VPN pro aplikaci pro Android](./media/android-pulse-secure-per-app-vpn/android_per_app_vpn_oma_uri.png)

### <a name="set-your-app-list-to-blacklist-or-whitelist-optional"></a>Nastavení seznamu aplikací jako zakázaných nebo povolených (volitelné)

Pomocí hodnoty **zakázané** zadejte seznam aplikací, které *nemůžou* používat připojení VPN. Všechny ostatní aplikace se připojují prostřednictvím VPN. Nebo pomocí hodnoty seznamu **povolených** adres zadejte seznam aplikací, které *můžou* používat připojení VPN. Aplikace, které nejsou v seznamu, se nepřipojují prostřednictvím sítě VPN.

1. V podokně **Vlastní nastavení OMA-URI** zvolte **Přidat**.
2. Zadejte název nastavení.
3. Do pole **OMA-URI**zadejte `./Vendor/MSFT/VPN/Profile/*Name*/Mode`, kde *název* je název profilu VPN, který jste si poznamenali v kroku 1. V našem příkladu je řetězec `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/Mode`.
4. Do **datového typu**zadejte **řetězec**.
5. Do pole **Hodnota** zadejte **BLACKLIST** nebo **WHITELIST**.

## <a name="step-3-assign-both-policies"></a>Krok 3: Přiřazení obou zásad

[Přiřaďte oba profily zařízení](device-profile-assign.md) požadovaným uživatelům nebo zařízením.
