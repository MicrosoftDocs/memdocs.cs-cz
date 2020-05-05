---
title: Profily sítě VPN
titleSuffix: Configuration Manager
description: Naučte se používat profily sítě VPN v Configuration Manager k nasazení nastavení VPN pro uživatele ve vaší organizaci.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9463d857599e676da6267313df575c8881436f93
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722253"
---
# <a name="vpn-profiles-in-configuration-manager"></a>Profily sítě VPN v nástroji Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

<!--1283610-->
K nasazení nastavení VPN pro uživatele ve vaší organizaci použijte profily sítě VPN v Configuration Manager. Nasazením těchto nastavení zjednodušíte koncovým uživatelům připojování k prostředkům v síti společnosti.  

Například chcete nakonfigurovat všechna zařízení s Windows 10 s nastavením požadovaným pro připojení ke sdílené složce v interní síti. Vytvořte profil sítě VPN s nastavením potřebným pro připojení k interní síti. Pak tento profil nasaďte všem uživatelům, kteří mají zařízení s Windows 10. Tito uživatelé uvidí připojení VPN v seznamu dostupných sítí a můžou se připojit s malým úsilím.

Když vytváříte profil sítě VPN, můžete zahrnout řadu nastavení zabezpečení. Tato nastavení zahrnují certifikáty pro ověření serveru a klienta, které zřídíte pomocí Configuration Manager profily certifikátů. Další informace najdete v tématu [profily certifikátů](introduction-to-certificate-profiles.md).

> [!Note]
> Configuration Manager ve výchozím nastavení nepovolí tuto volitelnou funkci. Tuto funkci musíte před použitím povolit. Další informace naleznete v části [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

## <a name="supported-platforms"></a>Podporované platformy

Následující tabulka popisuje profily sítě VPN, které můžete nakonfigurovat pro různé platformy zařízení.

|Typ připojení|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|
|---------------|-----------|----------|--------------|----------|
|**Pulse Secure**|Ano|Ne|Ano|Ano|
|**F5 Edge Client**|Ano|Ne|Ano|Ano|
|**Dell SonicWALL Mobile Connect**|Ano|Ne|Ano|Ano|
|**Kontrolní bod – mobilní síť VPN**|Ano|Ne|Ano|Ano|
|**Protokol SSL společnosti Microsoft (SSTP)**|Ano|Ano|Ano|Ne|
|**Automaticky pomocí technologie Microsoft**|Ano|Ano|Ano|Ne|
|**IKEv2**|Ano|Ano|Ano|Ne|
|**PPTP**|Ano|Ano|Ano|Ne|
|**L2TP**|Ano|Ano|Ano|Ne|

## <a name="next-step"></a>Další krok

> [!div class="nextstepaction"]
> [Postup vytvoření profilů sítě VPN](create-vpn-profiles.md)

## <a name="see-also"></a>Viz také

- [Požadavky na profily sítě VPN](../plan-design/prerequisites-for-wifi-vpn-profiles.md)

- [Zabezpečení a ochrana osobních údajů pro profily sítě VPN](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
