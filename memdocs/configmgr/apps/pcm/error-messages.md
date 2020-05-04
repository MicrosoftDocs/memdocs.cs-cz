---
title: Chybové zprávy
titleSuffix: Configuration Manager
description: Přečtěte si o chybových zprávách ze Správce převodu balíčků.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0d3cf6e1-b295-4b05-821d-e9f57c74ca14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4d4a2fa66dc1c4a8af3b3f7f16c67d58edebb5fa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709884"
---
# <a name="technical-reference-for-package-conversion-manager-error-messages"></a>Technické informace o chybových zprávách správce převodu balíčků

*Platí pro: Configuration Manager (Current Branch)*

<!--1357861-->

Tento článek popisuje chybové zprávy, které Package Conversion Manager zobrazí. Obsahuje taky možné příčiny chyby a metody, jak chybu opravit. Package Conversion Manager protokoluje chybové zprávy v **PCMTrace. log**. Další informace, včetně toho, jak řídit úroveň podrobností, najdete v tématu [soubory protokolu](troubleshoot-pcm.md#log-files).


#### <a name="application-creation-failed-with-the-following-exception"></a>Aplikaci se nepovedlo vytvořit, došlo k následující výjimce:

Během odesílání objektu aplikace na Server Configuration Manager došlo k zadané výjimce.

Zkontrolujte vaše oprávnění v Configuration Manager, ověřte připojení a pak to zkuste znovu. Pokud tyto akce problém nevyřeší, Projděte si soubor **PCMtrace. log** (s úrovní podrobností 4) a **Smsprov. log**.


#### <a name="conversion-error--applies-to-a-package-transform-status"></a>Chyba převodu – platí pro stav transformace balíčku

Při převodu balíčku došlo k obecné výjimce. Podívejte se do souboru **PCMtrace. log** (úroveň podrobností 4).

Zkontrolujte oprávnění uživatele pro sdílenou síťovou složku (zdroj dat balíčku), ověřte připojení a pak to zkuste znovu. Pokud tyto akce problém nevyřeší, Projděte si soubor **PCMtrace. log** (s úrovní podrobností 4).


#### <a name="did-not-find-a-converted-package-and-its-resultant-application-in-the-workflow-outputs"></a>V výstupech pracovního postupu se nenašel převedený balíček a jeho výsledná aplikace.
Aplikace (převedený balíček/program) se odstranila.

Upravte závislý balíček/program a ujistěte se, že existuje závislý balíček nebo program.


#### <a name="objects-were-not-created-successfully"></a>Objekty se úspěšně nevytvořily.
Existuje několik možných příčin.

Zkontrolujte vaše oprávnění v Configuration Manager, ověřte připojení a pak to zkuste znovu. Pokud tyto akce problém nevyřeší, Projděte si soubor **PCMtrace. log** (s úrovní podrobností 4) a soubor **Smsprov. log** .


#### <a name="please-close-the-wizard-and-resolve-any-issues-with-the-selected-package-see-pcmtracelog-for-more-details"></a>Zavřete prosím průvodce a vyřešte všechny problémy s vybraným balíčkem. Další podrobnosti najdete v tématu PCMTrace. log.
Existuje několik možných příčin.

Zkontrolujte vaše oprávnění v Configuration Manager, ověřte připojení a pak to zkuste znovu. Pokud tyto akce problém nevyřeší, Projděte si soubor **PCMtrace. log** (s úrovní podrobností 4) a soubor **Smsprov. log** .


#### <a name="some-deployment-types-are-missing-detection-methods-all-deployment-types-must-have-detection-methods"></a>U některých typů nasazení chybí metody detekce. Všechny typy nasazení musí mít metody detekce.
V programu chybí metody detekce.

Přidejte jednu nebo více metod detekce během procesu **opravit a převést** .


#### <a name="there-was-an-error-preparing-the-package-for-conversion"></a>Při přípravě balíčku pro převod došlo k chybě.
Existuje několik možných příčin.

Zkontrolujte vaše oprávnění v Configuration Manager, ověřte připojení a pak to zkuste znovu. Pokud tyto akce problém nevyřeší, Projděte si soubor **PCMtrace. log** (s úrovní podrobností 4) a soubor **Smsprov. log** .


