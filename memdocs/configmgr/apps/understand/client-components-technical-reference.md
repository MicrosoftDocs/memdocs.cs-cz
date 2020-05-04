---
title: Technické informace o klientských součástech nasazení aplikace
titleSuffix: Configuration Manager
description: Klientské součásti používané pro řešení potíží s nasazením aplikace v Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 701a3456-9dd6-4aaa-9c5a-37c1e1773216
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35b54bd5868197d607a15ab1d4759d03968b9892
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709800"
---
# <a name="understanding-application-deployment-client-components"></a>Principy klientských komponent nasazení aplikace

*Platí pro: Configuration Manager (Current Branch)*

Vyhodnocení nasazení aplikace a operace vynucení jsou zpracovávány komponentami agenta DCM a agentem CI na klientovi. Tento článek vysvětluje, jak funguje typická úloha agenta DCM a CI.

## <a name="dcm-agent"></a>Agent DCM

Agent DCM je klientská součást vysoké úrovně zodpovědná za hodnocení položek konfigurace, včetně aplikací. Když se nasazení aktivuje nebo vynutilo, vytvoří se úloha agenta DCM, která načte zásady přiřazení a určí akce, které je potřeba provést. Tato aktivita se dá sledovat v **DCMAgent. log** na klientovi pomocí ID úlohy agenta DCM, který se dá identifikovat tak, že vyhledáte jedinečné ID aplikace.

### <a name="device-deployments"></a>Nasazení zařízení

- Pro **požadovaná** nasazení by DCMAgent. log zobrazila příslušné akce. Tyto akce se mohou lišit v závislosti na tom, zda byl konečný termín nasazení již předán.

    ```text
    # Evaluation Job example:
    DCMAgentJob({A9E850E2-91B0-4122-94FD-D14EDF925AF7}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({4C8A9F6E-390B-450E-B505-B5698DB68EDD}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- Pro **dostupná** nasazení se DCMAgent. log zobrazí, že nasazení `is not mandatory`je. V těchto nasazeních se vyhodnocuje aplikace, ale vynucení se přeskočí, pokud uživatel neinicioval instalaci.

    ```text
    # Evaluation Job example:
    DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 - Assignment:{3AC57DFE-3F87-4C59-930B-B9F57CB41B91} is not mandatory.

    # Enforcement Job (user initiated) example:
    Request to enforce application ConfigMgr Toolkit(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/Application_fc76ef0a-3ab0-4110-8cce-1addc36d0225.3) immediately for target: machine with action(s): Evaluation, Install, Update
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {D331249E-F7DE-481B-A497-8E8B5E7B91C3}

    ```

### <a name="user-deployments"></a>Uživatelská nasazení

- Pro **požadovaná** nasazení by DCMAgent. log zobrazila příslušné akce. Tyto akce se mohou lišit v závislosti na tom, zda byl konečný termín nasazení již předán.

    ```text
    # Evaluation Job example:
    DCMAgentJob({65D9688D-1781-4DA3-B07A-193D481251C6}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({2B0DA272-FC65-4F31-9557-C4D840D650F1}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- Pro **dostupná** nasazení se pro vyhodnocení a vynucení vytvoří úlohy agenta DCM, když uživatel iniciuje instalaci aplikace.

    ```text
    # Evaluation Job example:
    DCMAgentJob({FBB44C84-DB06-41F7-8DC1-D9BA368F0C20}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 - Assignment:{7EA17128-EB4F-448A-88A7-B865E7DA228C} is not mandatory.

    # Enforcement Job example:
    CAppMgmtSDK::EnforceAppPolicy ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98.
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {7936D7F3-24B0-401D-BADD-59EB5B49C2C2}
    ```

## <a name="ci-agent"></a>Agent CI

Agent CI je součást klienta zodpovědná za vyhodnocení a nápravu položek konfigurace. Agent DCM načte zásady přiřazení a vytvoří úlohu pro komponentu služby CI agent, která provede požadované akce. **DCMAgent. log** zaznamenává ID úlohy agenta CI, což je užitečné při sledování aktivity agenta CI v **CIAgent. log** v klientovi.

<pre><code class="lang-text">DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgent::InitiateCIAgentJob - <b>Starting CI Agent Job</b> {57AF6FA1-3482-4469-9881-A63F41D18406} for target: machine. Refer to this CI agent job ID in ciagent.log for more details
</code></pre>

Typická úloha agenta CI projde několika fázemi, které je možné identifikovat filtrováním **CIAgent. log** v ID úlohy agenta ci a pak hledáním `TransitionState`. Některé z klíčových fází pro úlohu agenta CI nasazení aplikace jsou:

- **DownloadingCIs**
  - V průběhu této fáze se stáhnou metadata aplikace nutná k vyhodnocení aplikace. Metadata zahrnují metodu detekce, pravidla požadavků, globální podmínky atd. Tuto aktivitu je možné sledovat v **CIDownloader. log** a **DataTransferService. log**. U **dostupných** nasazení k tomuto procesu dochází během prvního vyhodnocení aplikace. Pro **požadovaná** nasazení ale k tomuto procesu dojde hned po stažení zásady.

- **InvokingSdmMethod**
  - V průběhu této fáze se pomocí metody detekce aplikace kontroluje, jestli je aplikace nainstalovaná, a je určený požadovaný stav. Tuto aktivitu je možné sledovat v **AppDiscovery. log** a **AppIntentEval. log**. Další informace o této fázi najdete v tématu [vyhodnocení aplikace](deployment-evaluation-technical-reference.md).

- **StateDownloadingContents**
  - V průběhu této fáze se v případě potřeby stáhne obsah aplikace. Tato aktivita se dá sledovat v **CAS. log**, **ContentTransferManager. log**, **LocationServices. log**a **DataTransferService. log**. Další informace o této fázi najdete v tématu [Stažení aplikace](deployment-download-technical-reference.md).

- **StateEnforcingCIs**
  - Během této fáze se iniciuje instalace aplikace. Tuto aktivitu je možné sledovat v **AppEnforce. log**. Další informace o této fázi najdete v tématu [instalace aplikace](deployment-install-technical-reference.md).

- **StateEnforcementReporting**
  - Během této fáze je stav instalace aplikace zaznamenán pro vytváření sestav do bodu správy. Tuto aktivitu je možné sledovat v **StateMessage. log**.

I když úloha agenta CI projde všemi fázemi, přeskočí fázi, pokud není vyžadována. Například pro **dostupná** nasazení StateDownloadingContents a fáze StateEnforcingCIs se přeskočí, dokud se uživatel nepokusí nainstalovat aplikaci z centra softwaru. Pro **požadovaná** nasazení ale fáze StateDownloadingContents stáhne obsah aplikace (Pokud je potřeba), když je přiřazení aktivované, ale fáze StateEnforcingCIs se přeskočí, pokud je konečný termín v budoucnosti. Toto chování je možné pozorovat v CIAgent. log filtrováním podle ID úlohy agenta CI a hledáním `Skipping policy`.

```text
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for ContentDownload task since CI action was not requested.
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for Enforce task since CI action was not requested.
```

## <a name="next-steps"></a>Další kroky

- [Vyhodnocení aplikace](deployment-evaluation-technical-reference.md)
- [Stažení aplikace](deployment-download-technical-reference.md)
- [Instalace aplikace](deployment-install-technical-reference.md)
