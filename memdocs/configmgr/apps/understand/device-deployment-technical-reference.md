---
title: Technické informace o nasazení aplikace na kolekce zařízení
titleSuffix: Configuration Manager
description: Řešení potíží s nasazením aplikací do kolekcí zařízení technické reference pro Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 4e62b04d-fe56-42ed-87dc-e673cf061d52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1965029a1933793057dc5768bacb391afd645404
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709758"
---
# <a name="application-deployment-for-device-collections"></a>Nasazení aplikace pro kolekce zařízení

*Platí pro: Configuration Manager (Current Branch)*

Když se aplikace nasadí do kolekce zařízení, zásada se zacílí na všechna zařízení v kolekci bez ohledu na účel nasazení. V tomto článku se dozvíte, jak na klientovi stáhnout zásady a jak se zpracovává nasazení.

> [!TIP]
> Všechny informace, které jsou nezbytné pro kontrolu protokolů klienta, lze získat spuštěním dotazu SQL, na který se odkazuje v části [než začnete](app-deployment-technical-reference.md#before-you-begin) .

## <a name="policy-download"></a>Stažení zásad

Po nastavení zásad pro nasazení aplikace na klienta bude klient stahovat zásady při příštím cyklu cyklického dotazování zásad. Když klient stáhne zásadu, stáhne spolu související zásady společně se zásadami nasazení. Tyto související zásady zahrnují zásady pro aplikaci, typ nasazení, globální podmínky atd. Aktivitu stažení zásad lze sledovat v nástroji **Policyagent. log** v klientovi pomocí jedinečného ID aplikace nebo přiřazení.

<pre><code class="lang-text">Download of policy CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00" completed (DTS Job ID: {AE88E639-0E59-40D7-AAA9-4403AAE6EE82})
Policy state for [CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00"] is currently [Active]
</code></pre>

Po stažení zásad na klienta vytvoří komponenta Scheduler plány pro aktivaci nasazení a vynucení.

## <a name="deployment-activation"></a>Aktivace nasazení

Při aktivaci nasazení je iniciováno vyhodnocení aplikace. Komponenta Scheduler vytvoří plán pro aktivaci přiřazení v čase, který je nakonfigurován v nasazení. Tuto aktivitu lze sledovat v nástroji **Scheduler. log** v klientovi pomocí jedinečného ID přiřazení aplikace.

- Pro **požadovaná** nasazení se vytvoří plán aktivace, ale zpoždění bude trvat až dvě hodiny, aby se zabránilo sporům prostředku na serverech lokality a distribučních bodech. Zpoždění pomáhá zabránit kolizím, protože obsah aplikace může být stažen během hodnocení, pokud je aplikace platná na základě definovaných pravidel požadavků.

    <pre><code class="lang-text">SMSTrigger '15AF8C4000080000' for scheduler '<b>Machine/{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 01:44:00 PM with randomization.
    </code></pre>

- U **dostupných** nasazení se vytvoří plán aktivace, který se aktivuje v dostupném čase nakonfigurovaném v nasazení.

    <pre><code class="lang-text">SMSTrigger '1E4F8C4000080001' for scheduler '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' will fire at 08/15/2019 01:13:33 PM without randomization.
    </code></pre>

Po přijetí časového plánu komponenta Scheduler odešle aktivační zprávu agentu DCM k provedení vyhodnocení aplikace.

<pre><code class="lang-text">Sending message for schedule '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' (Target: 'direct:DCMAgent', Name: '')
</code></pre>

Agent DCM obdrží aktivační zprávu a vytvoří úlohu pro vyhodnocení aplikace.

```text
CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='Activation'><AssignmentID>{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</AssignmentID></CIAssignmentMessage>'
```

## <a name="deployment-enforcement"></a>Vynucení nasazení

Instalace aplikace se iniciuje při vykonání nasazení.

- Pro **požadovaná** nasazení Scheduler vytvoří plán konečného termínu po stažení zásady, aby vynutil aplikaci v konečném termínu nasazení. Plán konečného termínu není ve výchozím nastavení náhodný. Chování při náhodném nastavování pro aktivaci lze nastavit pomocí nastavení klienta pro [vypnutí náhodného termínu](../../core/clients/deploy/about-client-settings.md#disable-deadline-randomization) .

    <pre><code class="lang-text">SMSTrigger '15EF8C4000080000' for scheduler '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 03:05:00 PM without randomization.
    </code></pre>

    V konečném termínu odešle komponenta Scheduleru zprávu o konečném termínu do agenta DCM. 

    <pre><code class="lang-text">Sending message for schedule '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' (Target: 'direct:DCMAgent', Name: '')
    </code></pre>

    Agent DCM obdrží zprávu o konečném termínu a vytvoří úlohu, která aplikaci vynutila.
  
    ```text
    CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='EnforcementDeadline'><AssignmentID>{5F2FA409-C9B2-4100-8BC8-051820311DE1}</AssignmentID></CIAssignmentMessage>'
    ```

    > [!NOTE]
    > Pro nasazení s konečným termínem v minulosti se aplikace aktivuje a vynutila hned stejnou úlohou agenta DCM, která provádí akce vyhodnocení, stažení a instalace.

- U **dostupných** nasazení neexistuje žádný plán konečného termínu, protože k vynucení dojde, když uživatel iniciuje instalaci aplikace z centra softwaru. Když uživatel spustí instalaci, vytvoří se úloha agenta DCM, která provede vyhodnocení aplikace, stažení a instalaci. Tuto aktivitu je možné sledovat v **DCMAgent. log** na klientovi.

## <a name="next-steps"></a>Další kroky

- [Principy klientských komponent nasazení aplikace](client-components-technical-reference.md)
