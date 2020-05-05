---
title: Řešení potíží s nástrojem BitLocker
titleSuffix: Configuration Manager
description: Naučte se řešit problémy se správou BitLockeru v Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 134c5b50-edeb-4d60-aaca-944d26deb9ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ed8e464e0ab7c17e87e3de2bf72aa0dfb0acd071
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723919"
---
# <a name="troubleshoot-bitlocker"></a>Řešení potíží s nástrojem BitLocker

*Platí pro: Configuration Manager (Current Branch)*

Informace v tomto článku vám pomůžou při řešení potíží se správou BitLockeru v Configuration Manager.

## <a name="server-error-in-self-service"></a>Chyba serveru v samoobslužné službě

Při prvním pokusu o otevření samoobslužného portálu (`https://webserver.contoso.com/SelfService`) se zobrazí následující chybová zpráva:

``` error
Configuration Error - Server Error in '/SelfService' Application

Description: An error occurred during the processing of a configuration file required to service this request. Please review the specific error details below and modify your configuration file appropriately.

Parser Error Message: Could not load file or assembly 'System.Web.Mvc, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.
```

Chcete-li tento problém vyřešit, ujistěte se, že jste nainstalovali [předpoklad](../../plan-design/bitlocker-management.md#prerequisites) pro **Microsoft ASP.NET MVC 4,0** na webovém serveru.

## <a name="see-also"></a>Viz také

Další informace o používání protokolů událostí BitLockeru najdete v tématu [protokoly událostí BitLockeru](about-event-logs.md).

Seznam známých chyb a možných příčin položek protokolu událostí najdete v následujících článcích:

- [Protokoly klientských událostí](client-event-logs.md)
- [Protokoly serverových událostí](server-event-logs.md)

Informace o tom, proč klienti hlásí, že nedodržují předpisy zásad správy BitLockeru, najdete v tématu [kódy nekompatibility](non-compliance-codes.md).
