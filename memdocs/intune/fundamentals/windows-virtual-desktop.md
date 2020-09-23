---
title: Použití virtuálního počítače s Windows s Microsoft Intune
titleSuffix: ''
description: Pokyny k používání služby Virtual Desktop systému Windows s Microsoft Intune
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 9/22/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: madakeva
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 64594332514004fbf75dfb1a86f1b0f346a336c9
ms.sourcegitcommit: 7b4d4bc6ec7d6e551d73fa4320984edef606c63d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "91017707"
---
# <a name="using-windows-virtual-desktop-with-intune"></a>Použití virtuálního klienta Windows s Intune

[Virtuální klient Windows](https://docs.microsoft.com/azure/virtual-desktop/)   je služba virtualizace plochy a aplikací, která běží na Microsoft Azure.Umožňuje koncovým uživatelům bezpečně se připojit k celé ploše z libovolného zařízení. Pomocí Microsoft Intune můžete po registraci zabezpečit a spravovat virtuální počítače virtuálních počítačů s Windows pomocí zásad a aplikací ve velkém měřítku. 

## <a name="prerequisites"></a>Požadavky 

V současné době Intune podporuje virtuální počítače virtuálních počítačů s Windows, které jsou: 

- Se systémem Windows 10 Enterprise verze 1809 nebo novější.
- [Služba Azure AD je připojená k hybridní službě Azure AD](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan).
- Nastavte si jako [osobní vzdálené plochy](https://docs.microsoft.com/azure/virtual-desktop/configure-host-pool-personal-desktop-assignment-type) v Azure. 
- Zaregistrované v Intune jedním z následujících způsobů: 
    - Nakonfigurujte [Zásady skupiny služby Active Directory](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy) tak, aby automaticky zaregistrovaly zařízení, která jsou připojená k hybridní službě Azure AD.
    - [Configuration Manager spolusprávy](https://docs.microsoft.com/configmgr/comanage/overview).
    - [Samoobslužná registrace uživatele prostřednictvím služby Azure AD JOIN](../enrollment/windows-enrollment-methods.md#user-self-enrollment-in-intune).

Další informace o licenčních požadavcích na virtuální počítače s Windows najdete v tématu [co je to virtuální počítač s Windows?](https://docs.microsoft.com/azure/virtual-desktop/overview#requirements).

Intune zpracovává osobní virtuální počítače s virtuálními počítači s Windows stejně jako fyzické desktopy Windows 10 Enterprise. Toto ošetření vám umožní používat některé ze stávajících konfigurací a zabezpečit virtuální počítače pomocí zásad dodržování předpisů a podmíněného přístupu. Správa služby Intune není závislá na správě virtuálních počítačů s Windows stejného virtuálního počítače nebo ke kolizi. 

## <a name="limitations"></a>Omezení

Při správě vzdálených klientů Windows 10 Enterprise se Pamatujte na určitá omezení: 

### <a name="configuration"></a>Konfigurace

Všechna omezení virtuálních počítačů uvedená v v [používání virtuálních počítačů s Windows 10](windows-10-virtual-machines.md) se vztahují také na virtuální počítače virtuálních počítačů s Windows.

Následující profily se v současné době navíc nepodporují:
- [Připojení k doméně](../configuration/device-profiles.md#domain-join)
- [Wi-Fi](../configuration/device-profiles.md#wi-fi)

Ujistěte se, že [zásady RemoteDesktopServices/AllowUsersToConnectRemotely](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-allowuserstoconnectremotely) nejsou zakázané.

### <a name="remote-actions"></a>Vzdálené akce

Následující vzdálené akce zařízení s Windows 10 se nepodporují/doporučují pro virtuální počítače virtuálních počítačů s Windows:

- Resetování autopilotu
- Střídání klíčů BitLockeru
- Začít znovu
- vzdálené uzamčení
- Resetování hesla
- Vymazání

### <a name="retirement"></a>Vyřazení

Při odstraňování virtuálních počítačů z Azure zůstanou v Intune osamocené záznamy o zařízeních. Automaticky se [vyčistí](../remote-actions/devices-wipe.md#automatically-delete-devices-with-cleanup-rules) podle pravidel čištění nakonfigurovaných pro tenanta.

### <a name="windows-10-enterprise-multi-session"></a>Více relací Windows 10 Enterprise

Intune v současné době nepodporuje správu víc relací Windows 10 Enterprise.

## <a name="next-steps"></a>Další kroky

[Přečtěte si další informace o virtuálních plochách Windows](https://docs.microsoft.com/azure/virtual-desktop/).