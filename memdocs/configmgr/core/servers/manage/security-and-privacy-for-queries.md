---
title: Zabezpečení a ochrana osobních údajů pro dotazy
titleSuffix: Configuration Manager
description: Osvědčené postupy pro zabezpečení a ochranu osobních údajů při dotazování na informace z databáze lokality.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 882eedd1be029d5824fbd5d26a3f08d8f8f0021d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714609"
---
# <a name="security-and-privacy-for-queries-in-configuration-manager"></a>Zabezpečení a ochrana osobních údajů pro dotazy v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Dotazy v Configuration Manager umožňují načíst informace z databáze lokality podle kritérií, která zadáte. Configuration Manager shromažďuje informace o databázi lokality během standardní operace. Například pomocí informací, které jsou shromážděny během zjišťování nebo inventarizace, můžete nakonfigurovat dotaz k identifikaci zařízení, která splňují zadaná kritéria.  

 Další informace o dotazech najdete v tématu [Úvod do dotazů](../../../core/servers/manage/introduction-to-queries.md). Osvědčené postupy zabezpečení a ochrana osobních údajů týkající se Configuration Manager operací, které shromažďují data, která můžete načíst pomocí dotazů, najdete v tématu [zabezpečení a ochrana osobních údajů pro Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Osvědčené postupy zabezpečení pro dotazy

 Tento osvědčený postup zabezpečení použijte pro dotazy.  

|Doporučené zabezpečení|Další informace|  
|----------------------------|----------------------|  
|Pokud exportujete nebo importujete dotaz, který je uložený v umístění v síti, Zabezpečte umístění a síťový kanál.|Omezte přístup k síťové složce neoprávněným uživatelům.<br /><br /> Použijte podepisování SMB (Server Message Block) nebo protokol Internet Protocol Security (IPsec) mezi umístěním v síti a serverem lokality, abyste zabránili útočníkovi v manipulaci s daty dotazu před jejich importem.|  

## <a name="next-steps"></a>Další kroky
  
[Zabezpečení a ochrana osobních údajů v nástroji Configuration Manager](../../../core/plan-design/security/security-and-privacy.md)
