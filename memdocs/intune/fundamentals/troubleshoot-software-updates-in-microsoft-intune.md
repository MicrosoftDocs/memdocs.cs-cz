---
title: Řešení potíží s aktualizacemi softwaru v Microsoft Intune – Azure | Microsoft Docs
description: Řešte problémy s aktualizacemi softwaru ve službě Microsoft Intune.
keywords: ''
author: Brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/29/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: d17b70f4-17b4-4d89-88fd-70fa4f34fbea
ROBOTS: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 851fea24f101d313dba3426e5d65c60c5f31fdb5
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79330399"
---
# <a name="troubleshoot-software-updates-in-microsoft-intune"></a>Řešení potíží s aktualizacemi softwaru ve službě Microsoft Intune

Pomáhat řešit problémy s aktualizací softwaru v Microsoft Intune. Pokud chcete zobrazit seznam kódů a popisů chyb, přejděte na [kódy chyb agentů aktualizace softwaru v Microsoft Intune](../protect/software-update-agent-error-codes.md).

## <a name="windows-7-devices-with-many-superseded-updates-stop-reporting-to-intune"></a>Zařízení s Windows 7 s mnoha nahrazenými aktualizacemi ukončí vytváření sestav do Intune.

U Microsoft Intune klientů může docházet k jednomu nebo několika z následujících příznaků:

- Zařízení zastavila vytváření sestav do Intune.  
- Zařízení se setkávají s vysokým využitím procesoru.
- Aplikace se při instalaci přes Intune instalují pomalu.
- Microsoft Intune Center se zobrazuje následující chyba: `An error occurred while updating your computer. Error found: Code 0x800705b4`.
- Konzola pro správu Intune > skupiny > všechna zařízení > stav zobrazuje:`One or more agents that are installed on this computer have errors. The information for this computer may not be accurate or up-to-date.`

K tomuto problému může dojít, pokud se nahrazené aktualizace (aktualizace nahrazují jinou aktualizací), které se po delší dobu neodmítly. Během některých procesů, jako je instalace aplikace, systém Windows zkontroluje všechny nahrazené aktualizace tak, aby byly aktualizace a jejich nástupce správně namapované. Pokud je seznam nahrazených aktualizací příliš velký, tato kontrola úlohy může způsobit vysoké využití procesoru z důvodu zatížení a požadovaného času. Tento problém se týká především zařízení se systémem Windows 7 kvůli velkému počtu nahrazených aktualizací, které jsou k dispozici pro systém Windows 7. Novější operační systémy nemusí mít tolik dostupných aktualizací, které se nahrazují, a nemusí být k tomuto problému náchylné.

**Rozlišení**

1. Přihlaste se k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
2. Vyberte **aktualizace softwaru**.
3. Odmítne všechny nahrazené aktualizace, které se mohou vztahovat na systém Windows 7 nebo na aplikace, například systém Microsoft Office, které byly nainstalovány v ovlivněných klientech.
4. Restartujte příslušné klienty.

Pokud používáte systém Windows 7, ujistěte se, že je nainstalována následující aktualizace:[3050265 web Windows Update klient pro systém Windows 7: červen 2015](https://support.microsoft.com/kb/3050265).

## <a name="next-steps"></a>Další kroky

Získejte pomoc [od Microsoftu](get-support.md)nebo využijte [komunitní fóra](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).