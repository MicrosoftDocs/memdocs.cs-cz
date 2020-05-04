---
title: Vzdálená pomoc mobilních zařízení spravovaných pomocí Intune
description: Pomocí čtyř různých možností můžete vzdáleně pomáhat uživatelům s jejich mobilními zařízeními.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 548f63dcbd1635c106573fda40f8cc7bf312866e
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086266"
---
# <a name="remotely-assist-mobile-devices-managed-by-microsoft-endpoint-manager"></a>Vzdálená pomoc mobilním zařízením spravovaným pomocí Microsoft Endpoint Manageru

K dispozici jsou čtyři možnosti pro vzdálenou správu zařízení spravovaných pomocí Microsoft Endpoint Manageru:

- [Microsoft Teams](https://products.office.com/microsoft-teams/) je centrum pro týmovou práci, kde můžete chatovat, plnit a spolupracovat bez ohledu na to, kde jste.
- [Rychlá pomoc](https://support.microsoft.com/help/4027243/windows-10-solve-pc-problems-with-quick-assist) je aplikace pro Windows 10, která umožňuje dvěma osobám sdílet zařízení přes vzdálené připojení.
- [TeamViewer](https://www.teamviewer.com/) je program třetí strany, který si koupíte samostatně. Poskytuje komplexní sadu vzdáleného přístupu a možností podpory. Integrace Intune a [TeamViewer](teamviewer-support.md) umožňuje vzdálenou podporu pomocí TeamVieweru a konektor se spravuje přímo v Intune.
- [Vzdálené řízení](https://docs.microsoft.com/configmgr/core/clients/manage/remote-control/introduction-to-remote-control) je součástí služby Microsoft Endpoint Configuration Manager. Slouží ke vzdálené správě, poskytování pomoci nebo zobrazení libovolného počítače v pracovní skupině a počítači připojeného k doméně.

| Funkce, platformy, licencování | **Teams** | Rychlý pomocník | TeamViewer (Intune) | Vzdálené řízení (ConfigMgr) |
|:---:|:---:|:---:|:---:|:---:|
| Vzdálené zobrazení a řízení |![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Prostřednictvím |![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)||![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Přenos souborů |![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Přístup správce se zvýšenou úrovní oprávnění |||![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Bezobslužný přístup |||![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Současné vzdálené řízení |![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| Podpora více uživatelů |||![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Vzdálené akce ||![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Podpora přes Internet |![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Vytváření sestav auditu |![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)||![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Podpora pro všechny platformy (Windows, iOS, Android, macOS) |![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)||![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Integrace s Windows 10 – nevyžaduje se žádná další aplikace ||![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| Vyžaduje, aby zařízení byla spoluspravovaná pomocí Configuration Manager a Intune. ||||![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Vyžaduje další licencování\* |![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)||![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|![Značka zaškrtnutí](../enrollment/media/enrollment-method-capab/checkmark.png)|

\*Týmy vyžadují licencování O365 nebo M365. Použití TeamVieweru a Intune vyžaduje licencování z TeamVieweru i Intune. Vzdálené řízení je funkce Configuration Manager a vyžaduje licencování Configuration Manager.
