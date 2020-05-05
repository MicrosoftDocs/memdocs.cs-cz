---
title: Jak uživatelé registrují zařízení
titleSuffix: Configuration Manager
description: Pochopte, jak uživatelé registrují zařízení s místní správou mobilních zařízení (MDM) v Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f80b77d6a25d7af701ded249118e95201bcb9cc1
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722330"
---
# <a name="how-users-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>Jak uživatelé registrují zařízení s místní MDM v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Díky Configuration Manager místní správě mobilních zařízení (MDM) můžou uživatelé zaregistrovat svoje zařízení. Existují dva požadavky:

- Pomocí nastavení klienta udělíte uživateli oprávnění k registraci.

- Na zařízení se nainstaluje požadovaný důvěryhodný kořenový certifikát.

Další informace o nastavení registrace najdete v tématu [Nastavení registrace zařízení pro místní](../get-started/set-up-device-enrollment-on-premises-mdm.md)správu mobilních zařízení (MDM).

## <a name="enroll-windows-10"></a><a name="bkmk_enrollDesk"></a>Zaregistrovat Windows 10

1. V počítači s Windows 10 přejděte na **Nastavení**.

1. Vyberte **účty**a pak vyberte **přístup do práce nebo do školy**.

1. Vyberte **připojit**, zadejte hlavní název uživatele (UPN) a pak vyberte **pokračovat**. Hlavní název uživatele (UPN) může být stejný jako vaše e-mailová adresa, například jdoe@contoso.com.

1. Zadejte plně kvalifikovaný název domény (FQDN) zprostředkujícího bodu registrace a vyberte **pokračovat**.

1. Zadejte heslo a vyberte **Přihlásit**se.

1. Systém Windows nemusí pamatovat přihlašovací údaje pro tuto akci, proto vyberte **Přeskočit**.

Po krátké době se zařízení zaregistruje pomocí Configuration Manager.

## <a name="enroll-windows-10-mobile"></a><a name="bkmk_enrollMob"></a>Zaregistrovat Windows 10 Mobile

1. Na zařízení se systémem Windows 10 Mobile přejděte na **Nastavení**.

1. Vyberte **účty**a pak vybrat **přístup do práce**.

1. Vyberte **Connect** (Připojit).

1. Zadejte hlavní název uživatele (UPN) a plně kvalifikovaný název domény zprostředkujícího bodu registrace. Potom vyberte **Připojit**.

1. Na další obrazovce zadejte hlavní název uživatele (UPN) a heslo a pak vyberte **Přihlásit**se.

Po krátké době se zařízení zaregistruje pomocí Configuration Manager. Vyberte **Done** (Hotovo).

## <a name="verify-enrollment"></a><a name="bkmk_verify"></a>Ověřit registraci

Pomocí konzoly Configuration Manager ověřte, že se zařízení úspěšně zaregistrovala. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte možnost **zařízení**. V seznamu zařízení vyhledejte nebo vyhledejte zaregistrované zařízení.
