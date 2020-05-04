---
title: Zásady ochrany počítačů se systémem Windows
titleSuffix: Microsoft Intune
description: Tyto zásady použijte, aby vám pomohly při zajišťování zabezpečení počítačů s Windows, které jsou spravovány klientským softwarem Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 02/28/2019
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: d081f466-45dd-41d1-ab25-6d974c72a52a
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: 100df6e3e6be4a08e96529b472b766fa424b4a30
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79330895"
---
# <a name="use-policies-to-help-protect-windows-pcs-that-run-the-intune-client-software"></a>Použijte zásady k ochraně počítačů s Windows, na nichž běží klientský software Intune.

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

Microsoft Intune nabízí tři zásady, které pomáhají při zajišťování zabezpečení počítačů s Windows, které jsou spravovány [klientským softwarem Intune](manage-windows-pcs-with-microsoft-intune.md).

## <a name="software-updates"></a>Aktualizace softwaru

Intune umožňuje snadnou [aktualizaci spravovaných počítačů s Windows](keep-windows-pcs-up-to-date-with-software-updates-in-microsoft-intune.md) tím, že vás informuje o dostupných aktualizacích softwaru od Microsoftu i dalších společností. Poté můžete tyto aktualizace schválit nebo odmítnout. Schválené aktualizace budou automaticky nainstalovány na všech příslušných počítačích.

## <a name="windows-firewall"></a>Brána Windows Firewall

Brána Windows Firewall pomáhá chránit počítače s Windows proti hackerům, malwaru a dalším hrozbám. S Intune můžete [spravovat nastavení a funkce pro bránu Windows Firewall](help-protect-windows-pcs-using-windows-firewall-policies-in-microsoft-intune.md) na všech počítačích, které spravujete.

## <a name="endpoint-protection"></a>Funkce Endpoint Protection

Jedna z vašich nejdůležitějších priorit jako správce IT je [udržovat počítače, které spravujete, bez malwaru a virů](help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune.md). Intune se integruje s Endpoint Protection a poskytuje ochranu proti hrozbám malwaru v reálném čase, udržuje aktualizované definiční soubory malwaru a automaticky kontroluje počítače. Endpoint Protection také poskytuje nástroje, které pomáhají se správou a monitorováním malwarových útoků.

## <a name="see-also"></a>Viz také

[Běžné otázky, problémy a řešení se zásadami a profily zařízení](../configuration/device-profile-troubleshoot.md)
