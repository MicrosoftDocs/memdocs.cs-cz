---
title: Auditování změn a událostí v Microsoft Intune – Azure | Microsoft Docs
description: Přečtěte si, jak kontrolovat protokoly auditu se zaznamenanými aktivitami Microsoft Intune.
keywords: ''
ms.author: dougeby
author: dougeby
manager: dougeby
ms.date: 03/18/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6ee841cc-5694-4ba1-8f66-1d58edec30a4
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 923a7c192121530d84ca2034b2ca8a4be3cc32d6
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990759"
---
# <a name="use-audit-logs-to-track-and-monitor-events-in-microsoft-intune"></a>Sledování a monitorování událostí v Microsoft Intune pomocí protokolů auditu

Protokoly auditu obsahují záznam aktivit, které generují změnu v Microsoft Intune. Vytváření, aktualizace (úpravy), odstraňování, přiřazování a vzdálené akce všechny události vytváření auditu, které můžou správci zkontrolovat pro většinu úloh Intune. Ve výchozím nastavení je auditování povolené pro všechny zákazníky. Tuto funkci nelze zakázat.

> [!NOTE]
> Události auditu se zahájily zaznamenáváním do vydání funkce prosince 2017. Předchozí události nejsou k dispozici.

## <a name="who-can-access-the-data"></a>Kdo má přístup k datům?

Protokoly auditu mohou kontrolovat uživatelé s tímto oprávněním:

- Globální správce
- Správce služby Intune
- Správci přiřazení k roli Intune s **Audit data**  -  oprávněním**ke čtení dat pro** audit

## <a name="audit-logs-for-intune-workloads"></a>Protokoly auditu pro úlohy Intune

Protokoly auditu můžete zkontrolovat ve skupině monitorování pro každou úlohu Intune:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **Tenant administration**  >  **protokoly auditu**správy tenanta.
3. Pokud chcete filtrovat výsledky, vyberte **filtrovat** a upřesněte výsledky pomocí následujících možností.
    - **Kategorie**: například **dodržování předpisů**, **zařízení**a **role**.
    - **Aktivita**: níže uvedené možnosti jsou omezeny možností vybranými v **kategorii kategorie**.
    - **Rozsah dat**: můžete vybrat protokoly pro předchozí měsíc, týden nebo den.
4. Zvolte **Použít**.
4. Kliknutím na položku v seznamu zobrazíte podrobnosti o aktivitě.

## <a name="route-logs-to-azure-monitor"></a>Směrování protokolů do Azure Monitor

Protokoly auditu a provozní protokoly je také možné směrovat na Azure Monitor. V **protokolech auditu**vyberte **nastavení exportovat data**:

![Export dat protokolu do služby Azure monitor výběrem možnosti Exportovat data v Intune](./media/monitor-audit-logs/audit-logs-export-data-settings.png)

> [!NOTE]
> Další informace o této funkci a o požadavcích na jejich použití najdete v tématu [odeslání dat protokolu do úložiště, centra událostí nebo Log Analytics](review-logs-using-azure-monitor.md).

> [!NOTE]
> **Iniciované uživatelem (actor)** obsahuje informace o tom, kdo úlohu spustil a kde byla spuštěna. Pokud například spustíte aktivitu v Intune v Azure Portal, **aplikace** vždy vypíše seznam **Microsoft Intune portálu** a **ID aplikace** vždy používá stejný identifikátor GUID.
>
> V části **cíle (y)** je uveden seznam více cílů a vlastností, které byly změněny.  

## <a name="use-graph-api-to-retrieve-audit-events"></a>Použití rozhraní API služby Graph k načtení událostí auditu

Podrobnosti o používání rozhraní Graph API k získání až jednoho roku událostí auditu najdete v článku [auditEvents](https://docs.microsoft.com/graph/api/intune-auditing-auditevent-list?view=graph-rest-1.0).

## <a name="next-steps"></a>Další kroky

[Odešlete data protokolu do úložiště, centra událostí nebo Log Analytics](review-logs-using-azure-monitor.md).

[Kontrola protokolů ochrany klientských aplikací](../apps/app-protection-policy-settings-log.md).
