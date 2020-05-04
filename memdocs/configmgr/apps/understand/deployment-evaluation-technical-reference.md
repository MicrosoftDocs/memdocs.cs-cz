---
title: Technické informace o vyhodnocení aplikace
titleSuffix: Configuration Manager
description: Řešení potíží s technickou referencí k vyhodnocení aplikací pro Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a7035223-d7bd-47b4-896f-08de3416a4eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fdeec54489adfc0d2a5cceb99c7e7587ce1a41ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709793"
---
# <a name="application-deployment-evaluation"></a>Vyhodnocení nasazení aplikace

*Platí pro: Configuration Manager (Current Branch)*

Než budete pokračovat, přečtěte si prosím [klientské komponenty nasazení aplikace](client-components-technical-reference.md) , abyste porozuměli zpracování úloh DCM a CI agent.

Vyhodnocení aplikace provádí agent DCM a komponenty agenta CI při aktivaci nasazení. Informace o tom, kdy se přiřazení aktivuje, najdete v článcích [nasazení aplikace do kolekcí zařízení](device-deployment-technical-reference.md) nebo [nasazení aplikací do kolekcí uživatelů](user-deployment-technical-reference.md) .

## <a name="application-detection-and-evaluation"></a>Detekce a vyhodnocení aplikace

Vyhodnocení aplikace se provádí během fáze **InvokingSdmMethod** úlohy agenta CI. Tato fáze je tam, kde klient vyhodnocuje metodu detekce definovanou pro aplikaci k určení, jestli je aplikace na zařízení nainstalovaná. Tuto aktivitu lze sledovat v **AppDiscovery. log** pomocí jedinečného ID typu nasazení nebo názvu typu nasazení.

```text
Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ Did not detect app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
```

> [!NOTE]
> Výše uvedený příklad ukazuje detekci pro aplikaci MSI, kde je zjišťování provedeno, pomocí kontroly, zda je v zařízení nainstalován kód produktu MSI. Pro aplikace, které používají alternativní metody zjišťování, se ke kontrole, jestli je aplikace nainstalovaná, používá příslušná metoda detekce.

V dalším kroku klient vyhodnotí požadovaný stav aplikace na základě účelu nasazení. Tento krok zahrnuje také zjištění, zda má aplikace nějaké závislosti nebo pravidla nahrazení, která by měla být pro aplikaci dodržena. Tuto aktivitu je možné sledovat v **AppIntentEval. log** pomocí jedinečného ID typu aplikace a nasazení.

<pre><code class="lang-text"># Available Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Available</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Required Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Installed</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Requirement Rules Not Met

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = NotApplicable, ResolvedState = None</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]
</code></pre>

V položce protokolu výše uvádí **aktuální stav** , zda je v zařízení aktuálně nainstalovaná aplikace. **Použitelnost** označuje, zda je aplikace platná na základě definovaných pravidel požadavků. **ResolvedState** určuje požadovaný stav aplikace na základě účelu nasazení.

> [!TIP]
> Pomocí [Nástroje pro monitorování nasazení](../../core/support/deployment-monitoring-tool.md) zobrazte stav aplikace, stav použitelnosti a porušení požadavků.

## <a name="next-steps"></a>Další kroky

- [Stažení aplikace](deployment-download-technical-reference.md)
