---
title: Technické informace o instalaci aplikace
titleSuffix: Configuration Manager
description: Řešení potíží s technickou referencí k instalaci aplikací Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 2af4f9c3-16b8-4691-a59d-aea6241d288e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 13c96e9ad4f0608084d87bed3973221730cb2d5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709779"
---
# <a name="application-installation"></a>Instalace aplikace

*Platí pro: Configuration Manager (Current Branch)*

Než budete pokračovat, přečtěte si prosím [klientské komponenty nasazení aplikace](client-components-technical-reference.md) , abyste porozuměli zpracování úloh DCM a CI agent.

Instalace aplikace je prováděna komponentou agenta DCM a agentem CI při vykonání nasazení. Doba vynucení se liší pro dostupná a požadovaná nasazení. Informace o tom, kdy se přiřazení vynutilo, najdete v článcích [nasazení aplikace do kolekcí zařízení](device-deployment-technical-reference.md) nebo [nasazení aplikací do kolekcí uživatelů](user-deployment-technical-reference.md) .

## <a name="enforcement-initiation"></a>Iniciace vynucení

Instalace aplikace je iniciována komponentou agenta CI v klientovi během fáze **StateEnforcingCIs** . Tento proces je stejný, bez ohledu na to, jestli je aplikace nasazená na kolekci zařízení nebo na kolekci uživatelů.

- U **dostupných** nasazení se aplikace nainstaluje, když uživatel zahájí instalaci aplikace z centra softwaru.
- Pro **požadovaná** nasazení se aplikace nainstaluje v konečném termínu nasazení. Uživatel ale může zahájit instalaci z centra softwaru před konečným termínem.

Když Agent CI inicializuje instalaci aplikace, vytvoří úlohu, která je zpracována součástí Správce úloh CI. Správce úloh CI pak zahájí instalaci. Tuto aktivitu lze sledovat v **CITaskMgr. log** pomocí jedinečného ID typu nasazení.

<pre><code class="lang-text"><b>Initiating task Enforce</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {9BC3154A-98F1-4595-A967-173D536A3F94}
Initiated application enforcement. : CITask(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2..Install.Enforce)
</code></pre>

## <a name="application-enforcement"></a>Vynucování aplikace

Po zahájení vynucování aplikace klient provede detekci aplikace znovu, aby zajistil, že aplikace ještě není nainstalovaná. Jakmile zjistíte, že aplikace není nainstalovaná, je spuštěna instalace aplikace. Tuto aktivitu lze sledovat v **AppEnforce. log** v klientovi pomocí jedinečného ID typu nasazení.

```text
+++ Starting Install enforcement for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" ApplicationDeliveryType - ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision - 2, ContentPath - C:\WINDOWS\ccmcache\2, Execution Context - System
    Executing Command line: "C:\WINDOWS\system32\msiexec.exe" /i "ConfigMgrTools.msi" /q /qn with user context
    Process 7292 terminated with exitcode: 0
Status is switching to Success
```

## <a name="installation-verification"></a>Ověření instalace

Po instalaci aplikace se znovu použije metoda detekce aplikace, aby se zajistilo, že se aplikace zjistila jako nainstalovaná.

<pre><code class="lang-text">Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ <b>Discovered MSI application</b> [AppDT Id: ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision: 2, MSI Product code: {4FFF7ECC-CCF7-4530-B938-E7812BB91186}, MSI Product version: ]
++++++ <b>App enforcement completed</b> (3 seconds) for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" [ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44], Revision: 2, User SID: ] ++++++
</code></pre>

Po dokončení vynucení obdrží agent CI oznámení o dokončení úlohy a úloha agenta CI přejde do další fáze.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateEnforcingCIs</b>)
</code></pre>

## <a name="next-steps"></a>Další kroky

[Řešení potíží s nasazením aplikací](../deploy-use/troubleshoot-application-deployment.md)
