---
title: Metody registrace zařízení s Windows v Intune
titleSuffix: Microsoft Intune
description: Seznamte se s různými způsoby, jak můžete zaregistrovat zařízení s Windows v Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: ''
ms.openlocfilehash: a6b45cef3cc13357638753efd5b8179c5ce41f6c
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/21/2020
ms.locfileid: "80085699"
---
# <a name="intune-enrollment-methods-for-windows-devices"></a>Metody registrace zařízení s Windows v Intune

Aby bylo možné spravovat zařízení v Intune, musí být zařízení nejprve zaregistrovaná ve službě Intune. Pro správu Intune je možné zaregistrovat jak osobní vlastnictví, tak i zařízení vlastněná firmou. 

Existují dva způsoby, jak získat zařízení zaregistrovaná v Intune:
- Uživatelé můžou své počítače s Windows sami zaregistrovat 
- Správci můžou nakonfigurovat zásady, aby vynutily automatický zápis bez nutnosti zásahu uživatele.

## <a name="user-self-enrollment-in-intune"></a>Samoobslužná registrace uživatelů v Intune

Uživatelé můžou svoje zařízení s Windows sami zaregistrovat pomocí kterékoli z těchto metod:

- [Přineste si vlastní zařízení (BYOD)](https://docs.microsoft.com/mem/intune/user-help/enroll-windows-10-device): uživatelé si zaregistrují svá zařízení v osobním vlastnictví tím, že se z **Nastavení** zařízení připojí **pracovní a školní** účet. Tento proces:
  - Zaregistruje zařízení Azure Active Directory, aby získalo přístup k firemním prostředkům, jako je e-mail.
  - Zaregistruje zařízení v Intune jako zařízení s osobním vlastnictvím (BYOD).
Pokud správce nakonfiguroval automatický zápis (dostupný s předplatnými Azure AD Premium), musí jenom zadat svoje přihlašovací údaje jenom jednou. V opačném případě se bude muset registrovat samostatně jenom přes registraci MDM a znovu zadat přihlašovací údaje.  
- **Registrace jenom pro MDM** umožňuje uživatelům zaregistrovat stávající pracovní skupinu, službu Active Directory nebo počítač připojený ke službě Azure Active Directory do Intune. Uživatelé se registrují z nastavení v existujícím počítači s Windows. Tato metoda se nedoporučuje, protože neregistruje zařízení do Azure Active Directory. Také zabraňuje použití funkcí, jako je například podmíněný přístup.
- [Připojení Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/user-help/user-help-join-device-on-network) – připojí zařízení k Azure Active Directory a umožní uživatelům přihlašovat se k Windows pomocí svých přihlašovacích údajů Azure AD. Pokud je povolený automatický zápis, zařízení se automaticky zaregistruje v Intune. Výhodou automatického zápisu je proces jednoho kroku pro uživatele. V opačném případě se bude muset registrovat samostatně jenom přes registraci MDM a znovu zadat přihlašovací údaje. Uživatelé tento způsob zapisují buď při počátečním nastavení systému Windows, nebo v nastavení. Zařízení je v Intune označené jako zařízení vlastněné společností.
- Automatický [pilot](enrollment-autopilot.md) – automatizuje připojení k Azure AD a zapisuje do Intune nová zařízení vlastněná společností. Tato metoda zjednodušuje integrované prostředí a odstraňuje nutnost použít na zařízení vlastní image operačního systému. Když správci používají Intune ke správě zařízení autopilotu, můžou po registraci spravovat zásady, profily, aplikace a další.  Existují čtyři typy nasazení autopilotu: [režim samoobslužného nasazování](https://docs.microsoft.com/windows/deployment/windows-autopilot/self-deploying) (pro veřejné terminály, digitální podpis nebo sdílené zařízení), [režim řízený uživatelem](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) (pro tradiční uživatele), [White šetrnější](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove) umožňuje partnerům nebo pracovníkům IT, aby předem zřídit počítač s Windows 10, aby byl plně nakonfigurovaný a připravený pro přípravu a [autopilot pro stávající zařízení](https://docs.microsoft.com/windows/deployment/windows-autopilot/existing-devices) vám umožní snadno nasadit nejnovější verzi Windows 10 na stávající zařízení.

## <a name="administrator-based-enrollment-in-intune"></a>Registrace na základě správce v Intune

Správci mohou nastavit následující metody registrace, které nevyžadují zásah uživatele:

- [Připojení k hybridní službě Azure AD](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy) umožňuje správcům nakonfigurovat zásady skupiny služby Active Directory tak, aby automaticky zaregistrovaly zařízení, která jsou připojená k hybridní službě Azure AD
- [Configuration Manager spoluspráva](https://docs.microsoft.com/configmgr/comanage/overview) umožňuje správcům zaregistrovat svá existující Configuration Manager spravovaná zařízení do Intune a získat tak duální výhody Intune a Configuration Manager.
- [Správce registrace zařízení](device-enrollment-manager-enroll.md) (DEM) je zvláštní účet služby. Účty DEM mají oprávnění, která oprávněným uživatelům umožňuje registrovat a spravovat více zařízení vlastněných společností. Tyto typy zařízení se hodí například pro aplikace POS a jednoúčelové aplikace, ale nehodí se pro uživatele, kteří potřebují přístup k e-mailu nebo k prostředkům společnosti. Tato metoda nepovoluje použití funkcí, jako je například podmíněný přístup. 
- [Hromadný zápis](windows-bulk-enroll.md) umožňuje oprávněnému uživateli připojit velký počet nových zařízení vlastněných společností Azure Active Directory a Intune. Zřizovací balíček vytvoříte pomocí aplikace Windows Configuration Designer (WCD). Pak pomocí média USB během počátečního prostředí Windows OOBE nebo z existujícího počítače s Windows nainstalujete zřizovací balíček, aby se zařízení automaticky zaregistrovala do Intune. Tato metoda nepovoluje použití podmíněného přístupu.
- [Registrace zařízení s Windows IoT Core](https://docs.microsoft.com/windows/iot-core/manage-your-device/intunedeviceenrollment) se provádí pomocí řídicího panelu Windows IoT Core k přípravě zařízení a následnému vytvoření zřizovacího balíčku pomocí nástroje Windows Configuration Designer. Když pak při počátečním spuštění použijete médium karty SD, nainstaluje zřizovací balíček, aby se zařízení automaticky zaregistrovala do Intune.

## <a name="next-steps"></a>Další kroky

[Seznamte se s možnostmi metod registrace Windows](enrollment-method-capab.md)
