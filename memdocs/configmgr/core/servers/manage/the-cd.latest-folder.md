---
title: Složka CD.Latest
titleSuffix: Configuration Manager
description: Přečtěte si o procesu, který doručuje aktualizace produktu v konzole Configuration Manager.
ms.date: 03/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 577bfd865ad3872c386384c3bba95cb009ef83ec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720510"
---
# <a name="the-cdlatest-folder-for-configuration-manager"></a>Disk CD. Poslední složka pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager má proces pro doručování aktualizací do produktu v konzole Configuration Manager. Pro podporu této nové metody aktualizace Configuration Manager se vytvoří nová složka s názvem **CD. Nejnovější**. Tato složka obsahuje kopii instalačních souborů Configuration Manager pro aktualizovanou verzi vaší lokality.  

Disk CD. Složka nejnovější obsahuje složku s názvem **Redist**, která obsahuje redistribuovatelné soubory, které instalační program stáhne a použije. Tyto soubory odpovídají verzi souborů nástroje Configuration Manager nalezených v této složce CD.Latest. Pokud spouštíte instalační program ze složky CD.Latest, musíte použít soubory odpovídající dané verzi instalačního programu. Můžete buď nasměrovat instalační program, aby stahoval nové a aktuální soubory od společnosti Microsoft, nebo přímo instalační program, aby používal soubory ze složky Redist, která je součástí disku CD. Poslední složka

Základní média neobsahují složku pro **redistribuci** . Lokalita nevytvoří složku Redist, dokud nenainstalujete konzolovou aktualizaci. Mezitím použijte složku Redist, kterou jste použili při instalaci lokalit ze základního média.  

> [!TIP]  
> Ujistěte se, že redistribuovatelné soubory, které používáte, jsou aktuální. Pokud jste dosud nestáhli redistribuovatelné soubory, naplánujte, aby instalační program provedl od společnosti Microsoft.   

Následující scénáře vytvoří nebo aktualizují disk CD. Poslední složka v lokalitě centrální správy nebo na serveru primární lokality:  

- Když nainstalujete aktualizaci nebo opravu hotfix v konzole Configuration Manager, lokalita vytvoří nebo aktualizuje složku v instalační složce Configuration Manager.  

- Když spustíte integrovanou úlohu zálohování Configuration Manager, lokalita vytvoří nebo aktualizuje složku pod určeným umístěním zálohovací složky.  

- Když nainstalujete novou lokalitu pomocí základního média, lokalita vytvoří disk CD. Poslední složka


## <a name="supported-scenarios"></a>Podporované scénáře

Zdrojové soubory z disku CD-ROM. Nejnovější složka je podporována v následujících scénářích:  

### <a name="backup-and-recovery"></a>Backup a obnovení
Chcete-li obnovit lokalitu, použijte zdrojové soubory z disku CD-ROM. Nejnovější složku, která odpovídá vašemu webu. Když spustíte zálohování lokality pomocí předdefinované úlohy zálohování lokality, pak z disku CD. Nejnovější složka je součástí zálohy.

- Při přeinstalaci lokality v rámci obnovení lokality lokalitu nainstalujete ze složky CD.Latest obsažené v záloze. Tato akce nainstaluje lokalitu pomocí verzí souborů, které odpovídají záloze lokality a databázi lokality.  

    - Pokud nemáte přístup ke správnému disku CD. Nejnovější verzi složky, Získejte disk CD. Nejnovější složku se správnými verzemi souborů instalací lokality do testovacího prostředí. Pak aktualizujte lokalitu tak, aby odpovídala verzi, kterou chcete obnovit.  

    - Pokud nemáte správný disk CD. Nejnovější složku a její obsah jsou k dispozici, nemůžete obnovit lokalitu. V takovém případě je potřeba lokalitu přeinstalovat.  

- Pokud nemáte disk CD. Poslední složka, ale má funkční podřízenou primární lokalitu nebo lokalitu centrální správy, můžete tuto lokalitu použít jako referenční lokalitu pro obnovení lokality.  

### <a name="install-a-child-primary-site"></a>Nainstalovat podřízenou primární lokalitu
Pokud chcete nainstalovat novou podřízenou primární lokalitu pod lokalitou centrální správy, která má nainstalovanou jednu nebo více konzolových aktualizací, použijte instalační program a zdrojové soubory z disku CD-ROM. Poslední složka z centrální lokality pro správu. Tento proces používá zdrojové instalační soubory, které odpovídají verzi lokality centrální správy. Další informace najdete v tématu [Instalace lokalit pomocí Průvodce instalací](../deploy/install/use-the-setup-wizard-to-install-sites.md)nástroje.  

### <a name="expand-a-stand-alone-primary-site"></a>Rozšíření samostatné primární lokality
Když rozbalíte samostatnou primární lokalitu pomocí instalace nové lokality centrální správy, použijte instalační program a zdrojové soubory z disku CD-ROM. Poslední složka z primární lokality. Tento proces používá zdrojové instalační soubory, které odpovídají verzi primární lokality. Další informace najdete v tématu [rozšíření samostatné primární lokality](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand).

### <a name="install-a-secondary-site"></a>Instalace sekundární lokality
<!-- SCCMDocs-pr issue #3164 -->
Pokud chcete nainstalovat novou sekundární lokalitu pod primární lokalitou, která má nainstalovanou jednu nebo více konzolových aktualizací, použijte zdrojové soubory z disku CD-ROM. Poslední složka z primární lokality. 

Další informace najdete v tématu [instalace sekundární lokality](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary). 


## <a name="unsupported-scenarios"></a>Nepodporované scénáře

Aktualizovaný disk CD. Nejnovější zdrojové soubory nejsou podporovány pro:  

- Instalaci nové lokality nové hierarchie  
- Upgrade lokality Microsoft System Center 2012 Configuration Manager na Configuration Manager aktuální větev
- Instalace klientů Configuration Manager
- Instalace konzol Configuration Manager
