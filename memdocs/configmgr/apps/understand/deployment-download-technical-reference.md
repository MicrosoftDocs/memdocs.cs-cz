---
title: Technické informace o stažení aplikace
titleSuffix: Configuration Manager
description: Řešení potíží s technickou referencí ke stažení aplikací pro Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 41c29a07-9bf6-4ec4-b3f2-1c05e001eff7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: effa8115a5023a8e0611f6bc4245a101b3a47e38
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709807"
---
# <a name="application-download-in-configuration-manager"></a>Stažení aplikace v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Než budete pokračovat, přečtěte si prosím [klientské komponenty nasazení aplikace](client-components-technical-reference.md) , abyste porozuměli zpracování úloh DCM a CI agent.

## <a name="download-initiation"></a>Zahájení stahování

Stažení obsahu aplikace je iniciováno komponentou agenta CI v klientovi během fáze **StateDownloadingContents** . Tento proces je stejný, bez ohledu na to, jestli je aplikace nasazená na kolekci zařízení nebo na kolekci uživatelů.

- Pro **dostupná** nasazení se obsah aplikace stáhne, když uživatel zahájí instalaci aplikace z centra softwaru.
- Pro **požadovaná** nasazení se obsah aplikace stáhne, když se aktivuje přiřazení, a po vyhodnocení se aplikace zjistí. Informace o tom, kdy se přiřazení aktivuje, najdete v článcích [nasazení aplikace do kolekcí zařízení](device-deployment-technical-reference.md) nebo [nasazení aplikací do kolekcí uživatelů](user-deployment-technical-reference.md) .

Když Agent CI zahájí stahování obsahu, vytvoří úlohu, která je zpracována součástí Správce úloh CI. Správce úloh CI pak zahájí stahování obsahu. Tuto aktivitu lze sledovat v **CITaskMgr. log** pomocí jedinečného ID typu nasazení.

<pre><code class="lang-text"><b>Initiating task ContentDownload</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {53EA65C2-D596-4215-83E4-F7007B78E18C}
</code></pre>

## <a name="distribution-point-location"></a>Umístění distribučního bodu

Všechny úlohy stahování jsou zpracovávány komponentou pro přístup k obsahu, která zodpovídá za správu mezipaměti klienta. Po vytvoření úlohy stažení zkontroluje komponenta Content Access, zda je obsah již v mezipaměti klienta k dispozici. Pokud není obsah k dispozici, vytvoří požadavek na umístění, kde získá seznam distribučních bodů, ze kterých lze získat obsah. Tuto aktivitu je možné sledovat v **certifikačních autoritách CAS. log** a **LocationServices. log** v klientovi pomocí jedinečného ID obsahu.

```text
Requesting locations synchronously for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 with priority Foreground
ContentLocationRequest : <Request XML Body>
Reply Message Body : <Reply XML Body>
```

> [!IMPORTANT]
> I když součást Locationing Service zpracovává požadavky na umístění, přímo nepožaduje umístění z bodu správy. Všechny požadavky na bod správy obvykle přecházejí do součásti pro zasílání zpráv CCM, která se zaznamená do **CcmMessaging. log**.

Adresa XML odpovědi umístění obsahuje seznam distribučních bodů na základě skupiny hranic klienta. Tento seznam se analyzuje a uchovává v rozhraní WMI na klientovi podle [priority zdroje obsahu](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#content-source-priority). Tato aktivita se dá zobrazit v **ContentTransferManager. log**pomocí jedinečného ID obsahu a hledání `Persisted location`. 

Pokud kód XML odpovědi umístění neobsahuje žádné distribuční body, zobrazí `Received empty location update` se **ContentTransferManager. log** a klient může při stahování aplikace zablokovat 0%. Tato odpověď se obvykle může vyskytnout z důvodu problémů s konfigurací skupiny hranic. Další informace najdete v tématu [selhání stahování](../deploy-use/troubleshoot-application-deployment.md#download-failures).

## <a name="content-download"></a>Stažení obsahu

Po získání umístění distribučního bodu vytvoří součást Content Access úlohu přenosu obsahu. Tato aktivita se dá sledovat v **CAS. log** pomocí jedinečného ID obsahu.

<pre><code class="lang-text">Submitted CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> to download Content <b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b> under context System
</code></pre>

Správce přenosu obsahu pak vytvoří úlohu služby Přenos dat pro stažení obsahu. Tuto aktivitu je možné sledovat v **ContentTransferManager. log** v klientovi pomocí jedinečného ID obsahu.

<pre><code class="lang-text">CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> (corresponding DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>) started download from '<Distribution Point URL>/<b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b>' for full content download.
</code></pre>

> [!NOTE]
> Tato položka protokolu se dá použít k identifikaci ID úlohy CTM a DTS, která se dá použít ke sledování průběhu přenosu obsahu v **ContentTransferManager. log** a **DataTransferService. log** .

Služba Přenos dat provádí stahování obsahu aplikace vytvořením úlohy Background Intelligent Transfer Service (BITS) a čekáním na dokončení stahování. Tuto aktivitu je možné sledovat v **DataTransferService. log** v klientovi pomocí ID úlohy DTS získaného z **ContentTransferService. log**.

<pre><code class="lang-text">Starting BITS job '{40263E01-2EDD-462F-ABBA-A5E892CB9229}' for DTS job '<b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>' under user 'S-1-5-18'.
DTSJob <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> in state 'DownloadingData'.
DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> has completed
</code></pre>

Po dokončení stahování se dokončí oznámení součásti Content Access. Komponenta pro přístup k obsahu potom ověří stažený obsah, aby se zajistilo, že se obsah během stahování nezměnil. Tato aktivita se dá sledovat v **CAS. log** pomocí jedinečného ID obsahu.

```text
Hash verification succeeded for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 downloaded under context System
```

Až se obsah ověří, agent CI obdrží oznámení o dokončení úlohy a úloha agenta CI se přesune do další fáze.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateDownloadingContents</b>)
</code></pre>

## <a name="next-steps"></a>Další kroky

- [Instalace aplikace](deployment-install-technical-reference.md)
