---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 06/29/2020
ms.openlocfilehash: 26bfbe7b7cabef8c8dee56077b924b69c4c5886a
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590524"
---
### <a name="azure-ad-authentication-doesnt-work"></a><a name="ki_auth"></a>Ověřování Azure AD nefunguje
<!--7569264-->
Používání služby tokenu zabezpečení Azure Active Directory (Azure AD) Configuration Manager nefunguje. **CCM_STS. log** v bodu správy obsahuje záznam podobný následující chybě: `ProcessRequest - Exception: System.IO.FileLoadException: Could not load file or assembly 'System.IdentityModel.Tokens.JWT.` obsahuje také HRESULT 0x80131040.

Další příznakem jsou problémy s bránou pro správu cloudu (CMG). Pokud spustíte nástroj CMG Connection Analyzer, při testování kanálu CMG pro bod správy dojde k následující chybě:`Failed to get ConfigMgr token with Azure AD token. Status code is '500' and status description is 'CMGConnector_InternalServerError'.`

Příčinou tohoto problému je nesoulad verzí s podpůrnou knihovnou.

Pokud chcete tento problém obejít, zkopírujte **System.IdentityModel.Tokens.JWT.dll** ze složky \bin\X64 instalačního adresáře na serveru lokality do složky SMS_CCM \ CCM_STS \Bin v bodu správy.
