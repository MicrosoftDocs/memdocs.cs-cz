---
title: Požadavky na profily sítí Wi-Fi a VPN
titleSuffix: Configuration Manager
description: Přečtěte si o požadavcích na správu profilů sítě Wi-Fi a profilů sítě VPN v Configuration Manager
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9e7a557bab6b41be6e6335e3aa2744e8627d285b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722127"
---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Předpoklady pro profily Wi-Fi a VPN v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Profily Wi-Fi a VPN v Configuration Manager mají závislosti pouze v rámci produktu.

Abyste mohli spravovat nastavení přístupu k prostředkům společnosti, jako jsou například profily certifikátů, profily sítě Wi-Fi a profily sítě VPN, potřebujete následující oprávnění zabezpečení:  

- Zobrazení a správa výstrah a sestav pro Wi-Fi a profily: **vytvořit**, **Odstranit**, **Upravit**, **Upravit sestavu**, **číst**a **Spustit sestavu** pro objekt **výstrahy** .  

- Vytvoření a Správa profilů certifikátů: vytvořit **zásady**, **Upravit sestavu**, **číst**a **Spustit sestavu** pro objekt **Profil certifikátu** .  

- Správa nasazení profilů sítě Wi-Fi, certifikátu a sítě VPN: **nasadit zásady konfigurace**, **upravit výstrahu stavu klienta**, **číst**a **číst prostředek** pro objekt **kolekce** .  

- Správa všech zásad konfigurace: **vytvořit**, **Odstranit**, **Upravit**, **číst**a **nastavit obor zabezpečení** pro objekt **zásady konfigurace** .  

- Spuštění dotazů souvisejících s profily sítě Wi-Fi a VPN: oprávnění **číst** pro objekt **dotaz** .  

- Zobrazení informací o profilech sítě Wi-Fi a VPN v konzole Configuration Manager: oprávnění **číst** pro objekt **lokalita** .  

- Zobrazení stavových zpráv pro profily sítě Wi-Fi a VPN: oprávnění **číst** pro objekt **stavové zprávy** .  

- Vytvoření a změna profilu certifikátu důvěryhodné certifikační autority: oprávnění vytvořit **zásady**, **Upravit sestavu**, **číst**a **Spustit sestavu** pro objekt **Profil certifikátu důvěryhodné certifikační autority** .  

- Vytvoření a správa profilů sítě VPN: **Vytvořit zásady**, **Upravit sestavu**, **Číst** a **Spustit sestavu** pro objekt **Profil sítě VPN**.  

- Vytvoření a správa profilů sítě Wi-Fi: **Vytvořit zásady**, **Upravit sestavu**, **Číst** a **Spustit sestavu** pro objekt **Profil sítě Wi-Fi**.  

Tato oprávnění, která jsou nutná ke správě profilů sítě Wi-Fi v Configuration Manager, zahrnují role zabezpečení **Správce přístupu k prostředkům společnosti** . Další informace najdete v tématu [Konfigurace zabezpečení](../../core/plan-design/security/configure-security.md).
