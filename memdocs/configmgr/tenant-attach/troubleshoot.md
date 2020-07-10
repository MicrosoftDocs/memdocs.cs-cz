---
title: Řešení potíží s připojením klienta a akcemi zařízení
titleSuffix: Configuration Manager
description: Řešení potíží s připojením klienta a akcemi zařízení pro Configuration Manager
ms.date: 07/07/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 44c2eb8a-3ccc-471f-838b-55d7971bb79e
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 67daa42fa6a8c107e7563302ccbcf8d7b2b4f69f
ms.sourcegitcommit: 3806a1850813b7a179d703e002bcc5c7eb1cb621
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/09/2020
ms.locfileid: "86210745"
---
# <a name="troubleshooting-tenant-attach-and-device-actions"></a>Řešení potíží s připojením klienta a akcemi zařízení

*Platí pro: Configuration Manager (Current Branch)*

Počínaje Configuration Manager 2002 se klienti Configuration Manager můžou synchronizovat s centrem pro správu Microsoft Endpoint Manageru. Některé akce klienta můžete spustit z centra pro správu Microsoft Endpoint Manageru u synchronizovaných klientů.

K dispozici jsou tyto akce:
- Synchronizovat zásady počítače
- Synchronizovat zásady uživatele
- Cyklus hodnocení aplikace


[![Přehled zařízení v centru pro správu služby Microsoft Endpoint Manager](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)
  
Když správce spustí akci z centra pro správu služby Microsoft Endpoint Manager, požadavek na oznámení se přesměruje na Configuration Manager lokalita a z lokality do klienta.

## <a name="configuration-manager-components"></a>Configuration Manager komponenty

- **SMS_SERVICE_CONNECTOR**: používá pracovní proces oznámení brány ke zpracování oznámení z centra pro správu služby Microsoft Endpoint Manager.
- **SMS_NOTIFICATION_SERVER**: načte oznámení a vytvoří klientské oznámení.
- **BgbAgent**: klient získá úlohu a spustí požadovanou akci.

## <a name="sms_service_connector"></a>SMS_SERVICE_CONNECTOR

Když se v centru pro správu Microsoft Endpoint Manager iniciuje akce, zpracovává se žádost **CMGatewayNotificationWorker. log** .  

```text
Received new notification. Validating basic notification details...
Validating device action message content...
Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
```
 
1. Z centra pro správu Microsoft Endpoint Manageru se přijalo oznámení.

   ```text
   Received new notification. Validating basic notification details..
   ```

1. Akce uživatelů a zařízení jsou ověřeny.

   ```text
   Validating device action message content... 
   Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
   ```

1. Vzdálená úloha se přepošle na SMS_NOTIFICATION_SERVER.

    ```text
   Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
    ```


## <a name="sms_notification_server"></a>SMS_NOTIFICATION_SERVER

Po odeslání zprávy do SMS_NOTIFICATION_SERVER je úloha odeslána z bodu správy do odpovídajícího klienta. Uvidíte níže v **BgbServer. log**, který je v bodu správy:

```text
Get one push message from database.
Starting to send push task (PushID: 7 TaskID: 8 TaskGUID: A43DD1B3-A006-4604-B012-5529380B3B6F TaskType: 1 TaskParam: ) to 1 clients  with throttling (strategy: 1 param: 42)
```

## <a name="bgbagent"></a>BgbAgent

Poslední krok probíhá na klientovi a může se zobrazit v **CcmNotificationAgent. log**. Po přijetí úkolu vyžádá Plánovač, aby provedl akci. Po provedení akce se zobrazí potvrzovací zpráva:

```text
Receive task from server with pushid=7, taskid=8, taskguid=A43DD1B3-A006-4604-B012-5529380B3B6F, tasktype=1 and taskParam=

Send Task response message <BgbResponseMessage TimeStamp="2020-01-21T15:43:43Z"><PushID>8</PushID><TaskID>9</TaskID><ReturnCode>1</ReturnCode></BgbResponseMessage> successfully.
```

## <a name="common-issues"></a>Běžné problémy

### <a name="unauthorized-to-perform-client-action"></a><a name="bkmk_noauth"></a>Neautorizováno k provedení akce klienta

Pokud správce nemá v Configuration Manager požadovaná oprávnění, zobrazí se `Unauthorized` odpověď v **protokolu CMGatewayNotificationWorker. log**.

```text
Received new notification. Validating basic notification details..
Validating device action message content...
Unauthorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID: 3a1e89e6-e190-4615-9d38-a208b0eb1c78
```  

Ujistěte se, že uživatel, který spustil akci z centra pro správu Microsoft Endpoint Manageru, má požadovaná oprávnění na Configuration Manager lokalitě. Další informace najdete v tématu [připojení požadavků klienta služby Microsoft Endpoint Manager](device-sync-actions.md#prerequisites).


## <a name="next-steps"></a>Další kroky

[Řešení potíží s podrobnostmi](troubleshoot-client-details.md) 
 klienta nástroje ConfigMgr [Umožněte spolusprávu](../comanage/overview.md) a získejte další možnosti cloudu, jako je podmíněný přístup.
