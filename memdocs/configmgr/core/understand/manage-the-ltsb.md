---
title: Správa LTSB
titleSuffix: Configuration Manager
description: Rozdíly v správě pro LTSB System Center Configuration Manager.
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8da2887a-fd8e-438c-b926-849c121f7fdf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 86e7579832a5a59c3609d24744eb646e1a4c1fd1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722701"
---
# <a name="manage-the-long-term-servicing-branch-of-configuration-manager"></a>Správa Long Term Servicing Branch Configuration Manager

*Platí pro: System Center Configuration Manager (větev dlouhodobé údržby)*

Pokud používáte LTSB (Long-Term Servicing Branch) System Center Configuration Manager, může vám následující informace pochopit důležité změny, které mají vliv na správu infrastruktury.

Vzhledem k tomu, že LTSB je ekvivalentem Current Branch verze 1606 (s některými výjimkami jako integrace Intune a funkcemi souvisejícími s cloudem), jsou většina úloh, které používáte pro plánování, nasazení, konfiguraci a každodenní správu, stejné.

LTSB například podporuje stejný počet lokalit, typů lokalit, klientů a obecnou infrastrukturu jako Current Branch. Proto použijete pokyny, které najdete v tématech Plánování lokality a hierarchie a návrh Current Branch. Podobně u funkcí s LTSB, které jsou podporovány v obou větvích, jako jsou aktualizace softwaru nebo nasazení operačního systému, použijte pokyny v těchto částech dokumentace Current Branch, které nemají přístup k změnám funkcí zavedeným po verzi 1606 Current Branch.

Následující části obsahují informace o správě nepodobných úloh.

## <a name="updates-and-servicing"></a>Aktualizace a údržba
V LTSB jsou k dispozici pouze důležité aktualizace zabezpečení jako konzolové aktualizace.  

Informace o pravidelných aktualizacích pro následné verze Current Branch jsou viditelné v konzole nástroje, ale nejsou zpřístupněny pro LTSB. Nebudou staženy a nelze je nainstalovat.

K podpoře konzolových aktualizací pro kritické opravy zabezpečení vyžaduje lokalita LTSB použití [spojovacího bodu služby](../servers/deploy/configure/about-the-service-connection-point.md). Tuto roli systému lokality můžete nakonfigurovat v režimu offline nebo online, jak je to pro Current Branch. LTSB shromažďuje a odesílá stejná data telemetrie a využití jako Current Branch.

LTSB podporuje použití instalačního programu oprav hotfix a nástroje pro registraci aktualizací, jak je uvedeno pro Current Branch.

Obecné informace o aktualizacích a údržbě najdete v tématu [aktualizace pro Configuration Manager](../servers/manage/updates.md).


## <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>Změny pro rozšíření lokality a disk CD. Poslední složka
Když spustíte LTSB a rozšíříte samostatnou primární lokalitu pomocí instalace nové lokality centrální správy, je nutné použít instalační program a zdrojové soubory z základního média verze 1606. Pro Current Branch spustíte instalační program a použijete zdrojové soubory z disku CD-ROM. Poslední složka

I když nespouštíte instalační program pro rozšíření lokality z disku CD-ROM. Nejnovější složku, budete nadále používat disk CD. Nejnovější složka pro Site Recovery a pro instalaci nové podřízené primární lokality, pokud byla vaše první lokalita LTSB jako lokalita centrální správy.

Další informace o rozšíření lokality naleznete v tématu [expand a samostatná primární lokalita](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand). Další informace o disku CD. Nejnovější složku, viz [CD. Poslední složka](../servers/manage/the-cd.latest-folder.md)


## <a name="recovery"></a>Obnovení
Při obnovení lokality je nutné obnovit lokalitu nebo databázi lokality do původní větve. Nemůžete obnovit Current Branch databázi lokality do instalace LTSB nebo naopak.
