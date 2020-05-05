---
title: Jak zavřít účet
titleSuffix: Configuration Manager
description: Jak odebrat desktopovou analýzu z účtu Azure
ms.date: 10/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 6e7d2850-b0af-497e-bbc1-bfc2a7420a7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e1d031588100f3930bf5bf25970f544b91017d77
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722519"
---
# <a name="how-to-close-your-account"></a>Jak zavřít účet

Pokud ve svém prostředí nastavíte analýzu stolního počítače a pak se rozhodnete ji odebrat, pomocí tohoto postupu uzavřete svůj účet.

## <a name="prerequisites"></a>Požadavky

Účet v Azure Portal může zavřít nebo znovu aktivovat pouze **globální správce** .

## <a name="process-to-offboard"></a>Proces do odpojení

1. Otevřete [portál Desktop Analytics](https://aka.ms/desktopanalytics) v Microsoft 365 Správa zařízení jako uživatel s rolí **globálního správce** .

1. V nabídce **globální nastavení** vyberte **připojené služby**. V části registrace zařízení vyberte možnost **odpojení**.

1. Pokud se rozhodnete pokračovat, váš účet je uzavřený.

> [!Important]
> Pokračujte pouze ve zbývající části tohoto článku po 90 dnech, nebo pokud znovu neaktivujete.
>
> Pokud chcete účet úplně zavřít, aniž byste čekali na 90 dní, nejdřív [resetujte](account-reset.md) účet.

## <a name="reactivate"></a>Znovu aktivovat

V příštích 90 dnech se všem správcům z vaší organizace, kteří přistupují k portálu pro Desktop Analytics, zobrazí oznámení, že jste se rozhodli odpojení.

Globální správce může účet znovu aktivovat během 90 dnů. Pokud chcete obnovit aplikaci Desktop Analytics pro vaši organizaci, vyberte možnost **vrácení zpět**.

## <a name="delete-the-solution"></a>Odstranit řešení

> [!Warning]
> Pokračujte pouze ve zbývající části tohoto článku po 90 dnech, nebo pokud znovu neaktivujete. Pokud tyto další komponenty odstraníte a odpojíte, nezkuste znovu aktivovat.

1. Přihlaste se k [Azure Portal](https://portal.azure.com) jako uživatel s rolí **globálního správce** .

1. Vyhledejte v části **všechny prostředky** název pracovního prostoru Desktop Analytics. Toto je název, který jste vytvořili při registraci ke službě.

1. Odstraňte `Microsoft365Analytics(YourWorkspaceName)` **řešení**typu.

Data služby Desktop Analytics se odkládají na základě zásad uchovávání dat v pracovním prostoru. Můžete dál používat jiná řešení ve stejném pracovním prostoru.

> [!Important]  
> Pokud používáte Log Analytics pracovní prostor s jinými řešeními, neodstraňujte pracovní prostor.

## <a name="remove-user-and-app-access"></a>Odebrání přístupu uživatele a aplikace

1. Přihlaste se k [Azure Portal](https://portal.azure.com) jako uživatel s rolí **globálního správce** . Přejít na **Azure Active Directory**.

1. V části **role a správci**vyhledejte roli **správce Desktop Analytics** . Odeberte jeho členy.

1. V části **skupiny**odeberte členy následujících skupin:

    - **Správci klientů M365 Analytics (vlastníci Log Analytics)**
    - **Správci klientů M365 Analytics (Log Analytics přispěvatelé)**

1. V části **podnikové aplikace**odstraňte nebo Odvolejte přístupová oprávnění pro následující aplikace:

    - `MaLogAnalyticsReader`

    - Aplikace ConfigMgr. Pokud chcete najít název této aplikace, otevřete konzolu Configuration Manager. V pracovním prostoru **Správa** rozbalte položku **Cloud Services**a vyberte uzel **služby Azure** . Otevřete vlastnosti služby **Desktop Analytics** a přepněte na kartu **aplikace** . **Webová aplikace** je tato aplikace Azure.

        > [!Important]  
        > Než provedete změny této aplikace ve službě Azure AD, ujistěte se, že ji nepoužíváte s jinou službou v Configuration Manager.

## <a name="disconnect-configuration-manager"></a>Odpojit Configuration Manager

1. Otevřete konzolu Configuration Manager jako uživatel s rolí **úplného správce** .

1. V pracovním prostoru **Správa** rozbalte položku **Cloud Services**a vyberte uzel **služby Azure** .

1. Odstraňte službu Desktop Analytics.

### <a name="delete-collections-for-the-pilot-and-production-deployments"></a>Odstranění kolekcí pro pilotní nasazení a produkční nasazení

1. V konzole Configuration Manager v pracovním prostoru **prostředky a kompatibilita** vyberte **kolekce zařízení** .

1. Odstraňte všechny kolekce, které už nepoužíváte. Ve výchozím nastavení se kolekce nacházejí ve složce **plány nasazení** .  

## <a name="reconfigure-clients"></a>Změna konfigurace klientů

### <a name="unenroll-devices"></a>Zrušit registraci zařízení

V zaregistrovaných zařízeních odeberte hodnotu CommercialID z následujících klíčů registru Windows:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Konfigurace diagnostických dat Windows

Pokud nechcete, aby zařízení pokračovala v posílání diagnostických dat:

- Windows 10: Nastavte úroveň diagnostických dat na **zabezpečení**
- Windows 7 SP1 nebo 8,1: zakázání **klíče pro přihlášení k komerčním datům**

Tyto hodnoty nastavte pomocí jedné z následujících metod:

- Zásady skupiny v části **Konfigurace** > **šablony pro správu** > kolekce dat**součásti** > systému Windows**a buildy Preview**
- Správa mobilních zařízení (MDM), například [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

Další informace najdete v tématu [Konfigurace diagnostických dat Windows ve vaší organizaci](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization).

> [!NOTE]  
> Když tyto změny použijete, zařízení okamžitě zastaví odesílání diagnostických dat. Společnost Microsoft může trvat 24-48 hodin, než přestane zpracovávat přehledy pro váš pracovní prostor. Společnost Microsoft odstraní tato data ze svých cloudových služeb do 30 dnů nebo i rychleji.
