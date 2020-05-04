---
title: Auditovat využití vzdáleného řízení
titleSuffix: Configuration Manager
description: Auditovat použití vzdáleného řízení v Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5c975e69-0cc0-4afd-b7fb-b7182162a933
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2cda087867f3ebbd6695a0f4d368bbe2c5e06664
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715162"
---
# <a name="how-to-audit-remote-control-usage-in-configuration-manager"></a>Jak auditovat využití vzdáleného řízení v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pomocí sestav Configuration Manager můžete zobrazit informace o auditování pro vzdálené řízení.  

 Další informace o tom, jak nakonfigurovat vytváření sestav v Configuration Manager, najdete v tématu [Úvod do vytváření sestav](../../../servers/manage/introduction-to-reporting.md).  

 V kategorii **Stavové zprávy – audit**jsou dostupné tyto dvě sestavy:  

-   **Vzdálené řízení – všechny počítače vzdáleně řízené určitým uživatelem** – zobrazí shrnutí aktivity vzdáleného řízení, kterou určitý uživatel inicioval.  

-   **Vzdálené řízení – informace o veškerém vzdáleném řízení** – zobrazí souhrn stavových zpráv o vzdáleném řízení klientských počítačů.  

### <a name="to-run-the-report-remote-control---all-computers-remote-controlled-by-a-specific-user"></a>Spuštění sestavy vzdálené řízení – všechny počítače vzdáleně řízené určitým uživatelem  

1.  V konzole Configuration Manager klikněte na **monitorování**.  

2.  V pracovním prostoru **Sledování** rozbalte možnost **Generování sestav**a pak klikněte na položku **Sestavy**.  

3.  V uzlu **Sestavy** kliknutím na sloupec **Kategorie** seřaďte sestavy, abyste mezi nimi snáze našli kategorii **Stavové zprávy - Audit**.  

4.  Vyberte sestavu **Vzdálené řízení – všechny počítače vzdáleně řízené určitým uživatelem**a pak na kartě **Domů** klikněte v části **Skupina sestav**na tlačítko **Spustit**.  

5.  V seznamu **Uživatelské jméno** v sestavě **Vzdálené řízení – všechny počítače vzdáleně řízené určitým uživatelem**určete uživatele, pro kterého chcete informace auditu shromáždit, a klikněte na **Zobrazit sestavu**.  

6.  Až si sestavu prohlédnete, zavřete její okno.  

### <a name="to-run-the-report-remote-control---all-remote-control-information"></a>Spuštění sestavy vzdálené řízení – informace o veškerém vzdáleném řízení  

1.  V konzole Configuration Manager klikněte na **monitorování**.  

2.  V pracovním prostoru **Sledování** rozbalte možnost **Generování sestav**a pak klikněte na položku **Sestavy**.  

3.  V uzlu **Sestavy** kliknutím na sloupec **Kategorie** seřaďte sestavy, abyste mezi nimi snáze našli kategorii **Stavové zprávy - Audit**.  

4.  Vyberte sestavu **Vzdálené řízení – informace o veškerém vzdáleném řízení**a pak na kartě **Domů** kliknutím v části **Skupina sestav**na tlačítko **Spustit** otevřete okno sestavy **Vzdálené řízení – informace o veškerém vzdáleném řízení** .  

5.  Až si sestavu prohlédnete, zavřete její okno.  
