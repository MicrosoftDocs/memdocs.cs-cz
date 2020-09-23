---
title: Monitorování stavu řešení Microsoft Tunneling VPN pro Microsoft Intune – Azure | Microsoft Docs
description: Monitoruje stav brány Microsoft Tunnel Gateway, serveru sítě VPN, který běží na systému Linux. Cloudová zařízení od Microsoftu, která spravujete pomocí Intune, můžou mít přístup k místní infrastruktuře.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fd2f584221643c82f07924d96f72fa01c4321b79
ms.sourcegitcommit: 7b4d4bc6ec7d6e551d73fa4320984edef606c63d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/22/2020
ms.locfileid: "91017705"
---
# <a name="monitor-microsoft-tunnel"></a>Monitorování tunelu Microsoft

Po instalaci tunelu Microsoft můžete zobrazit konfiguraci serveru a stav serveru v centru pro správu Microsoft Endpoint Manageru (endpoint.microsoft.com).  

## <a name="use-the-admin-center-ui"></a>Použití uživatelského rozhraní centra pro správu

Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)a pak na *Správa tenanta*  >  *Microsoft Tunnel Gateway*a vyberte kartu **stav** .

Ve verzi Preview zobrazuje stav pouze, zda je server připojen za posledních 5 minut.  Budoucí vylepšení budou přidávat další podrobnosti.

## <a name="use-mst-cli-command-line-tool"></a>Použití nástroje příkazového řádku MST-CLI

K získání informací o serveru tunelu Microsoft použijte nástroj příkazového řádku **MST-CLI** . Tento soubor se přidá na server Linux při instalaci tunelu Microsoft. Nástroj je umístěný na adrese: **/usr/sbin/MST-CLI**.

Další informace a příklady příkazového řádku najdete v tématu [nástroj příkazového řádku MST-CLI pro tunelové propojení Microsoft) (.. /Protect/Microsoft-Tunnel-reference.MD # MST-CLI-Command-line-nástroj-for-Microsoft-Tunnel)

## <a name="next-steps"></a>Další kroky

[Referenční informace k tunelu Microsoft](../protect/microsoft-tunnel-reference.md)
