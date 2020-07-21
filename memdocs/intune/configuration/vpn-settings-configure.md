---
title: Přidání nastavení sítě VPN do zařízení v Microsoft Intune – Azure | Microsoft Docs
description: Na zařízeních s Androidem pro správce zařízení, Android Enterprise, iOS, iPadOS, macOS a Windows můžete pomocí integrovaných nastavení vytvořit připojení k virtuální privátní síti (VPN) v Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1916004d8e61239d7de92a77769ee970cc7a3118
ms.sourcegitcommit: d3992eda0b89bf239cea4ec699ed4711c1fb9e15
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/21/2020
ms.locfileid: "86565619"
---
# <a name="create-vpn-profiles-to-connect-to-vpn-servers-in-intune"></a>Vytvoření profilů sítě VPN pro připojení k serverům VPN v Intune

Virtuální privátní sítě (VPN) poskytují uživatelům zabezpečený vzdálený přístup k síti vaší organizace. Zařízení používají profil připojení VPN ke spuštění připojení se serverem VPN. **Profily sítě VPN** v Microsoft Intune přiřazují nastavení sítě VPN pro uživatele a zařízení ve vaší organizaci. Tato nastavení použijte, aby se uživatelé mohli snadno a bezpečně připojit k síti vaší organizace.

Chcete například nakonfigurovat všechna zařízení s iOS/iPadOS s požadovaným nastavením pro připojení ke sdílené složce v síti organizace. Vytvoříte profil sítě VPN, který bude obsahovat tato nastavení. Pak tento profil přiřadíte všem uživatelům, kteří mají zařízení se systémem iOS/iPadOS. Uživatelé uvidí připojení VPN v seznamu dostupných sítí a můžou se připojit s minimálním úsilím.

> [!NOTE]
> [Vlastní zásady konfigurace Intune](custom-settings-configure.md) můžete použít k vytvoření profilů sítě VPN pro následující platformy:
>
> * Android 4 nebo novější
> * Zaregistrovaná zařízení se systémem Windows 8.1 a novějším
> * Windows Phone 8.1 nebo novější
> * Zaregistrovaná zařízení s desktopovým systémem Windows 10
> * Windows 10 Mobile
> * Windows Holographic for Business

## <a name="vpn-connection-types"></a>Typy připojení VPN

Profily VPN můžete vytvářet pomocí následujících typů připojení:

- Automaticky
  - Windows 10

- Check Point Capsule VPN
  - Správce zařízení s Androidem
  - Podnikové pracovní profily Androidu
  - Plně spravovaný podnik s Androidem Enterprise a pracovní profil ve vlastnictví firmy: použití [zásad konfigurace aplikací](../apps/app-configuration-vpn-ae.md)
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- Cisco AnyConnect
  - Správce zařízení s Androidem
  - Podnikové pracovní profily Androidu
  - Plně spravovaný podnik pro Android Enterprise a pracovní profil ve vlastnictví firmy
  - iOS/iPadOS
  - macOS

- Cisco (IPSec)
  - iOS/iPadOS

- Citrix SSO
  - Správce zařízení s Androidem
  - Android Enterprise Working Profiles: použití [zásad konfigurace aplikací](../apps/app-configuration-vpn-ae.md)
  - Plně spravované podnikové pracovní profily pro Android Enterprise a vlastněné společností: použití [zásad konfigurace aplikací](../apps/app-configuration-vpn-ae.md)
  - iOS/iPadOS
  - Windows 10

- Vlastní VPN
  - iOS/iPadOS
  - macOS

  Vytváření vlastních profilů VPN pomocí nastavení URI v [vytvořit profil s vlastním nastavením](custom-settings-configure.md).

- F5 Access
  - Správce zařízení s Androidem
  - Podnikové pracovní profily Androidu
  - Plně spravovaný podnik pro Android Enterprise a pracovní profil ve vlastnictví firmy
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- IKEv2
  - iOS/iPadOS
  - Windows 10

- L2TP
  - Windows 10

- Palo Alto Networks GlobalProtect
  - Android Enterprise Working Profiles: použití [zásad konfigurace aplikací](../apps/app-configuration-vpn-ae.md)
  - Plně spravovaný podnik s Androidem Enterprise a pracovní profil ve vlastnictví firmy: použití [zásad konfigurace aplikací](../apps/app-configuration-vpn-ae.md)
  - iOS/iPadOS
  - Windows 10

- PPTP
  - Windows 10

- Pulse Secure
  - Správce zařízení s Androidem
  - Podnikové pracovní profily Androidu
  - Plně spravovaný podnik pro Android Enterprise a pracovní profil ve vlastnictví firmy
  - iOS/iPadOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- SonicWall Mobile Connect
  - Správce zařízení s Androidem
  - Podnikové pracovní profily Androidu
  - Plně spravovaný podnik pro Android Enterprise a pracovní profil ve vlastnictví firmy
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- Zscaler
  - Android Enterprise Working Profiles: použití [zásad konfigurace aplikací](../apps/app-configuration-vpn-ae.md)
  - Plně spravovaný podnik s Androidem Enterprise a pracovní profil ve vlastnictví firmy: použití [zásad konfigurace aplikací](../apps/app-configuration-vpn-ae.md)
  - iOS/iPadOS

> [!IMPORTANT]
> Před použitím profilů VPN přiřazených nějakému zařízení je nutné nainstalovat příslušnou aplikaci VPN pro profil. Pokud chcete aplikaci přiřadit přes Intune, přečtěte si téma [co je Správa aplikací v Microsoft Intune?](../apps/app-management.md).  

## <a name="create-the-profile"></a>Vytvoření profilu

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Devices**  >  **Konfigurace zařízení profily konfigurace**  >  **vytvořit profil**.
3. Zadejte tyto vlastnosti:

    - **Platforma**: vyberte platformu zařízení. Možnosti:
      - **Správce zařízení s Androidem**
      - **Android Enterprise**  >  **Plně spravovaný, vyhrazený a podnikový pracovní profil**
      - **Android Enterprise**  >  **Pracovní profil**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 a novější**
      - **Windows 8.1 a vyšší**
      - **Windows Phone 8.1**
    - **Profil**: vyberte **VPN**.

4. Vyberte **Vytvořit**.
5. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Dobrým názvem profilu je například **profil sítě VPN pro celou firmu**.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.

6. Vyberte **Další**.
7. Nastavení, která můžete konfigurovat v **nastavení konfigurace**, se liší v závislosti na zvolené platformě. Pro podrobnější nastavení vyberte svou platformu:

    - [Správce zařízení s Androidem](vpn-settings-android.md)
    - [Android Enterprise](vpn-settings-android-enterprise.md)
    - [iOS/iPadOS](vpn-settings-ios.md)
    - [macOS](vpn-settings-macos.md)
    - [Windows 10](vpn-settings-windows-10.md) (včetně Windows holografického pro firmy)
    - [Windows 8.1](vpn-settings-windows-8-1.md)
    - [Windows Phone 8.1](vpn-settings-windows-phone-8-1.md)

8. Vyberte **Další**.
9. V části **značky oboru** (volitelné) přiřaďte značku pro filtrování profilu pro konkrétní IT skupiny, například `US-NC IT Team` nebo `JohnGlenn_ITDepartment` . Další informace o značkách oboru naleznete v tématu [použití značek RBAC a Scope pro distribuci](../fundamentals/scope-tags.md).

    Vyberte **Další**.

10. V části **přiřazení**vyberte uživatele nebo skupiny, které obdrží váš profil. Další informace o přiřazování profilů najdete v tématu [přiřazení profilů uživatelů a zařízení](device-profile-assign.md).

    Vyberte **Další**.

11. V rámci **Revize a vytvoření**zkontrolujte nastavení. Když vyberete **vytvořit**, vaše změny se uloží a profil se přiřadí. Tato zásada se taky zobrazuje v seznamu profily.

## <a name="secure-your-vpn-profiles"></a>Zabezpečení profilů sítě VPN

Profily VPN můžou používat spoustu různých typů připojení a protokoly od různých výrobců. Tato připojení jsou obvykle zabezpečená pomocí následujících metod.

### <a name="certificates"></a>Certifikáty

Při vytváření profilu VPN zvolíte certifikátu SCEP nebo PKCS, který jste předtím vytvořili v Intune. Tento profil se označuje jako certifikát identity. Slouží k ověřování na základě důvěryhodného profilu certifikátu (neboli *kořenového certifikátu*), který vytvoříte, aby bylo možné zařízení uživatele připojit. Tento důvěryhodný certifikát se přiřazuje počítači, který ověřuje připojení VPN. Zpravidla se jedná o server VPN.

Pokud pro profil sítě VPN používáte ověřování pomocí certifikátů, pak nasaďte profil sítě VPN, profil certifikátu a důvěryhodný kořenový profil do stejných skupin. Toto přiřazení zajišťuje, aby každé zařízení rozpoznalo legitimitu vaší certifikační autority.

Další informace o vytváření a používání profilů certifikátů v Intune najdete v tématu [Jak konfigurovat certifikáty pomocí Microsoft Intune](../protect/certificates-configure.md).

> [!NOTE]
> Certifikáty přidané pomocí typu profilu **certifikátu importovaného PKCS** nejsou podporované pro ověřování VPN. Certifikáty přidané pomocí typu profilu **PKCS certifikáty** jsou podporovány pro ověřování sítě VPN.


### <a name="user-name-and-password"></a>Uživatelské jméno a heslo

Uživatel se ověřuje na serveru sítě VPN zadáním uživatelského jména a hesla.

## <a name="next-steps"></a>Další kroky

Když je profil vytvořený, není ještě aktivní. Dále [Přiřaďte profil](device-profile-assign.md) k některým zařízením a [sledujte jeho stav](device-profile-monitor.md).

Můžete také vytvořit a použít sítě VPN pro jednotlivé aplikace v zařízeních s Androidem pro [Správce zařízení/Android Enterprise](android-pulse-secure-per-app-vpn.md) a [iOS/iPadOS](vpn-setting-configure-per-app.md) .
