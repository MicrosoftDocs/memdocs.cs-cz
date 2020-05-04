---
title: Stažení definic od Microsoftu
titleSuffix: Configuration Manager
description: Naučte se, jak povolit stahování definic Endpoint Protection malwaru z aktualizací Microsoftu pro Configuration Manager.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1f0d8ac635d514e750584126458bfde6b5fc24ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715687"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates"></a>Povolit Endpoint Protection definice malwaru ke stažení z aktualizací Microsoftu

*Platí pro: Configuration Manager (Current Branch)*

Když vyberete stažení aktualizací definic z Microsoft Update, klienti zkontrolují Microsoft Update lokality v intervalu definovaném v části **aktualizace služby Security Intelligence** v dialogovém okně antimalwarové zásady.

 Tato metoda může být užitečná, pokud klient nemá připojení k Configuration Manager lokalitě nebo pokud chcete, aby uživatelé mohli zahájit aktualizace definic.

> [!IMPORTANT]
> - Ke stahování aktualizací definic je potřeba, aby měli klienti přístup k webu Microsoft Update přes internet.
> - Oddíl **aktualizace definic** se přejmenoval na **aktualizace Security Intelligence** začínající v Configuration Manager verze 1902.

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>Stahování definic pomocí Centra společnosti Microsoft pro ochranu před škodlivým softwarem
 Můžete klienty nakonfigurovat tak, aby stahovali aktualizace definic z Centra společnosti Microsoft pro ochranu před škodlivým softwarem. Tuto možnost používají klienti Endpoint Protection ke stahování aktualizací definic, pokud se nedaří stáhnout aktualizace z jiného zdroje. Tato metoda aktualizace může být užitečná v případě, že dojde k potížím s infrastrukturou Configuration Manager, která brání v doručování aktualizací.

> [!IMPORTANT]
>  Ke stahování aktualizací definic je potřeba, aby měli klienti přístup k webu Microsoft Update přes internet.
> 
> 
> [!div class="button"]
> [Další krok >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Zpět >](endpoint-configure-alerts.md)
