---
title: Plánování místní správy MDM
titleSuffix: Configuration Manager
description: Plánování místní správy mobilních zařízení pro správu mobilních zařízení v Configuration Manager
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5690e4fe003939d00dee1185e6f6551813c346e5
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721847"
---
# <a name="plan-for-on-premises-mdm-in-configuration-manager"></a>Plánování místní správy mobilních zařízení (MDM) v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Při plánování implementace místní správy mobilních zařízení (MDM) v Configuration Manager je potřeba si projít několik klíčových oblastí:

- Podporovaná zařízení a verze operačních systémů
- Požadované role systému lokality
- Zabezpečená komunikace
- Registrace zařízení

> [!IMPORTANT]
> I když se web nebo jakékoli mobilní zařízení nepřipojí k Microsoft Intune, vaše organizace pořád vyžaduje licence Intune, aby mohli tuto funkci používat. Další informace najdete v tématu [Microsoft Intune licencování](https://docs.microsoft.com/intune/fundamentals/licenses).

Než začnete připravovat infrastrukturu Configuration Manager pro zpracování místní správy mobilních zařízení (MDM), vezměte v úvahu následující požadavky.

## <a name="supported-devices"></a><a name="bkmk_devices"></a>Podporovaná zařízení  

Aktuální větev Configuration Manager podporuje registraci v místní správě mobilních zařízení pro zařízení s Windows 10. Tyto typy zařízení primárně zahrnují přenosné počítače, IoT a Surface Hub. Další informace a seznam konkrétních edic najdete v tématu [podporované verze operačních systémů pro klienty a zařízení](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).

## <a name="site-system-roles"></a><a name="bkmk_roles"></a>Role systému lokality

Místní MDM vyžaduje aspoň jednu z následujících rolí systému lokality:

- **Zprostředkující bod registrace**, který podporuje požadavky na registraci.

- **Bod registrace**, který podporuje registraci zařízení.

- **Správa požadované konfigurace** pro doručování zásad. Tato role je variantou bodu správy, ale umožňuje správu mobilních zařízení.

- **Distribuční bod** pro doručování obsahu.

V závislosti na potřebách vaší organizace můžete tyto role nainstalovat na jeden server nebo samostatně na různých serverech.

> [!NOTE]
> Je potřeba nakonfigurovat každou roli, která se používá pro místní MDM, jako koncový bod HTTPS pro komunikaci s důvěryhodnými zařízeními. Další informace najdete v oddílu [Požadovaná důvěryhodná komunikace](#bkmk_trustedComs).

Obecnější informace najdete v tématu [Plánování serverů a rolí systému lokality](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

## <a name="trusted-communications"></a><a name="bkmk_trustedComs"></a>Důvěryhodná komunikace

Místní MDM vyžaduje, abyste povolili role systému lokality pro komunikaci pomocí protokolu HTTPS. V závislosti na vašich potřebách můžete k navázání důvěryhodných připojení mezi servery a zařízeními použít certifikační autoritu (CA) vaší organizace. Jako důvěryhodnou autoritu můžete také použít veřejně dostupnou certifikační autoritu. V obou případech je nutné nakonfigurovat následující certifikáty:

- **Certifikát webového serveru** ve službě IIS na serverech, které jsou hostiteli požadovaných rolí systému lokality. Pokud jeden Server hostuje více rolí systému lokality, budete pro tento server potřebovat jenom jeden certifikát. Pokud je každá role na samostatném serveru, každý server potřebuje samostatný certifikát.

- **Důvěryhodný kořenový certifikát** certifikační autority, který vydává certifikáty webového serveru. Tento kořenový certifikát nainstalujte na všechna zařízení, která se potřebují připojit k rolím systému lokality.

Další informace najdete v tématu [nastavení certifikátů pro důvěryhodnou komunikaci v místní](../get-started/set-up-certificates-on-premises-mdm.md)správě mobilních zařízení (MDM).

## <a name="device-enrollment"></a><a name="bkmk_enrollment"></a>Registrace zařízení

Povolení registrace zařízení pro místní správu mobilních zařízení (MDM):

- Udělení oprávnění uživatelům k registraci prostřednictvím nastavení klienta

- Konfigurace zařízení pro důvěryhodnou komunikaci se servery systému lokality, které jsou hostiteli požadovaných rolí

Jako alternativu k registraci iniciované uživatelem můžete nastavit balíček hromadného zápisu. Tento balíček umožňuje registraci zařízení bez zásahu uživatele. Doručovat balíček do zařízení dřív, než se zřídí pro použití, nebo po jeho absolvování pomocí procesu OOBE.

Další informace najdete v tématu [Nastavení registrace zařízení pro místní](../get-started/set-up-device-enrollment-on-premises-mdm.md)správu mobilních zařízení (MDM).

## <a name="next-step"></a>Další krok

> [!div class="nextstepaction"]
> [Instalace rolí systému lokality](../get-started/install-site-system-roles-for-on-premises-mdm.md)
