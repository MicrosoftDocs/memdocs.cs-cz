---
title: Řešení potíží s tipy pro nasazení aplikací
titleSuffix: Configuration Manager
description: Tipy pro řešení problémů s nasazením aplikací v Configuration Manager
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4e8b46a3-3e11-475f-a4d7-6bf9ddf14145
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4723a85c55a2a5f7a4fbd0a99a14fbf31e7511c6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710584"
---
# <a name="troubleshooting-tips-for-application-deployments"></a>Tipy pro řešení potíží s nasazením aplikací

*Platí pro: Configuration Manager (Current Branch)*

Typické problémy s nasazením aplikací spadají do jedné z následujících kategorií:

- Selhání stahování aplikace

- Dodržování předpisů při nasazení aplikace zablokovalo 0%.

Pokud se setkáte s jedním z těchto problémů, Tento článek popisuje některé kroky, které můžete použít k řešení potíží. Další podrobné řešení potíží najdete v tématu [řešení potíží s technickými referencemi k nasazení aplikací](../understand/app-deployment-technical-reference.md).


## <a name="download-failures"></a>Neúspěšné stahování

Selhání stahování aplikací zahrnuje následující problémy:

- Klient se zablokuje stažením aplikace.

- Klientovi se nepodařilo stáhnout obsah aplikace.

- Klient se při stahování aplikace zablokuje na 0%.

První věc, kterou je třeba kontrolovat při selhání stahování aplikace, je pro chybějící nebo nesprávně nakonfigurované hranice a skupiny hranic. Například pokud je klient na intranetu a není nakonfigurovaný pro správu jenom internetových klientů, jeho síťové umístění musí být v nakonfigurované hranici. Aby mohl klient stahovat obsah, musí být k této hranici přiřazena také hraniční skupina. Další informace najdete v tématu [definice hranic lokality a skupin hranic](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).

Pokud nemůžete konfigurovat hranici pro klienta, nebo pokud konkrétní skupina hranic nemůže být členem jiné skupiny hranic:

1. V konzole Configuration Manager otevřete vlastnosti **typu nasazení**.  

1. Přepněte na kartu **obsah** .

1. V části pro použití distribučního bodu ze sousední skupiny hranic nebo výchozí skupiny hranic lokality změňte **Možnosti nasazení** tak, aby **stahoval obsah z distribučního bodu, a spusťte místně**. (Ve výchozím nastavení toto nastavení **nestahuje obsah**.)

Pokud klient nemůže stáhnout obsah aplikace, zajistěte, aby byl distribuován do distribučního bodu. Pokud chcete tuto konfiguraci ověřit, pomocí funkcí v konzole monitorujte distribuci obsahu do distribučních bodů. Další informace najdete v tématu [monitorování šířeného obsahu](../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  


## <a name="compliance-stuck-at-0"></a>Dodržování předpisů je zablokované na 0%.

Pokud je Kompatibilita nasazení aplikace 0%, ověřte stav nasazení aplikace v pracovním prostoru **monitorování** v uzlu **nasazení** .

- **Probíhá**: klient se může zablokovat [stahování obsahu](#download-failures) .

- **Chyba**: Další informace o tom, jak tento problém vyřešit, najdete v tomto blogovém příspěvku: [tipy a triky: jak provést akci s prostředky, které nahlásí selhání nasazení.](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/Tips-and-Tricks-How-to-Take-Action-on-Assets-That-Report-a/ba-p/273019)

- **Neznámé**: Tento stav obvykle znamená, že klient neobdržel zásady. Ručně aktualizujte zásady klienta a zjistěte, jestli je klient obdrží. Další informace najdete v tématu [spuštění načtení zásad pro klienta Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).
  
Pokud tyto akce problém nevyřeší, Projděte si stav klienta. Může docházet k hlubšímu problému s klientem. Další informace najdete v tématu [monitorování klientů](../../core/clients/manage/monitor-clients.md).


## <a name="next-steps"></a>Další kroky

- [Monitorování aplikací](monitor-applications-from-the-console.md)
- [Nasazení aplikací](deploy-applications.md)
- [Úlohy správy pro aplikace](management-tasks-applications.md)
- [Řešení potíží s technickými referencemi k nasazení aplikace](../understand/app-deployment-technical-reference.md)
