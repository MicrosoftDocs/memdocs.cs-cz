---
title: 'Instalace lokality pomocí základního média 1606 '
titleSuffix: Configuration Manager
description: Nainstalujte nebo upgradujte na LTSB pro System Center Configuration Manager.
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d70611aff329f48c8223a47dfa238e5a4559972
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722799"
---
# <a name="install-and-upgrade-with-the-version-1606-baseline-media"></a>Instalace a upgrade pomocí základního média verze 1606

*Platí pro: System Center Configuration Manager (větev dlouhodobé údržby)*

Když spouštíte instalaci z základního média verze 1606 pro Configuration Manager, můžete nainstalovat System Center Configuration Manager webu s dlouhou dobou údržby.

Základní médium je k dispozici na disku DVD jako součást softwaru Microsoft System Center 2016 nebo z System Center Configuration Manageré dlouhodobé větve údržby verze 1606. Další informace o základních médiích najdete v tématu [základní a aktualizační verze](../servers/manage/updates.md#bkmk_Baselines).


Když použijete základní médium verze 1606, lokalita, kterou nainstalujete nebo upgradujete na, je:
- *Current Branch lokalita* , která je shodná s lokalitou, která byla poprvé nainstalována pomocí základního média 1511, a poté aktualizována na verzi 1606 1606 a kumulativní oprava-KB3186654.
- *Lokalita LTSB* , která je rovnocenná lokalitě Current Branch, na které běží verze 1606, a 1606 opravy hotfix Rollup-KB3186654. Základní médium již obsahuje kumulativní opravu hotfix.  LTSB ale nepodporuje všechny funkce a možnosti, které jsou k dispozici v Current Branch, jak je popsáno v [úvodu ke větvi dlouhodobé údržby System Center Configuration Manager](introduction-to-the-ltsb.md).

Pokud nejste obeznámeni s různými větvemi Configuration Manager, přečtěte si informace [o tom, kterou větev Configuration Manager mám použít](which-branch-should-i-use.md).




## <a name="changes-to-setup-with-the-1606-baseline-media"></a>Změny nastavení pomocí multimediálního základního média 1606
Základní médium 1606 obsahuje následující změny instalačního programu pro Configuration Manager.

### <a name="branch-and-edition"></a>Větev a edice
Když spustíte instalaci, zobrazí se vám stránka licencování, kde můžete vybrat větev Configuration Manager, kterou chcete nainstalovat. Jako licencovanou instalaci můžete zvolit buď Current Branch, nebo LTSB, nebo můžete zvolit zkušební edici Current Branch jako nelicencovanou instalaci.

Další informace najdete v tématu [licencování a větve pro Configuration Manager](learn-more-editions.md).

### <a name="software-assurance-expiration"></a>Doba platnosti Software Assurance
Během instalace máte možnost zadat hodnotu **data vypršení platnosti Software Assurance** . Toto je volitelná hodnota, kterou můžete zadat jako pohodlné připomenutí.

> [!NOTE]
> Microsoft neověřuje datum vypršení platnosti, které jste zadali, a nepoužije toto datum pro ověření licence.  Místo toho ho můžete použít jako připomenutí data vypršení platnosti. To je užitečné, protože Configuration Manager pravidelně kontroluje nové aktualizace softwaru, které jsou k dispozici online, a stav licence Software Assurance by měl být aktuální, aby mohl používat tyto další aktualizace.    

- Hodnotu data můžete zadat na stránce **kód Product Key** Průvodce instalací při spuštění instalačního programu ze základního média Configuration Manager verze 1606.
- Toto datum můžete také zadat tak, že v konzole Configuration Manager vyberete **Nastavení hierarchie vlastnosti** > **licencování** .

Další informace najdete v tématu "smlouvy Software Assurance" v části [licencování a větve pro Configuration Manager](learn-more-editions.md).


### <a name="additional-pre-upgrade-configurations"></a>Další konfigurace před upgradem
Před zahájením upgradu System Center 2012 Configuration Manager do LTSB musíte provést následující další kroky jako součást kontrolního seznamu před upgradem.  
Odinstalujte role systému lokality, které LTSB nepodporuje:
- Bod synchronizace katalogu Asset Intelligence
- Konektor služby Microsoft Intune
- Cloudové distribuční body

Další informace najdete v tématu [upgrade na Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md).


### <a name="new-scripted-installation-options"></a>Nové možnosti instalace pomocí skriptů
Základní klíčové médium verze 1606 podporuje nový klíč souboru skriptu bezobslužné instalace pro skriptované instalace nové lokality nejvyšší úrovně. To platí pro instalaci nové samostatné primární lokality nebo přidání lokality centrální správy jako součást scénáře rozšíření lokality.

Při použití bezobslužného skriptu k instalaci licencované větve musíte do oddílu možnosti vašeho skriptu přidat následující část názvy klíčů a hodnoty. Tyto hodnoty nemusíte používat k skriptu instalace zkušební edice Current Branch:  

 **SABranchOptions**
- **Název klíče: SAActive**
  - Hodnoty: 0 nebo 1.  
  - Podrobnosti: 0 nainstaluje nelicencovanou zkušební verzi Current Branch a 1 nainstaluje licencovanou verzi.   

- **CurrentBranch**
  - Hodnoty: 0 nebo 1.  
  - Podrobnosti: 0 nainstaluje větev dlouhodobé údržby a 1 nainstaluje Current Branch.  

Například pro instalaci licencované Current Branch edice byste použili:

**Název klíče: SABranchOptions**
- **SAActive = 1**
- **CurrentBranch = 1**


> [!IMPORTANT]  
> **SABranchOptions** funguje jenom s instalačním programem ze základního média. Neplatí při spuštění instalačního programu z disku CD-ROM. Nejnovější složku webu, který jste dříve nainstalovali pomocí základního média verze 1606.
>
> **SABranchOptions** se nevztahuje na skriptované upgrady z nástroje System Center 2012 Configuration Manager a vždy vede Current Branch.

Další informace najdete v tématu [použití příkazového řádku pro instalaci Configuration Managerch lokalit](../servers/deploy/install/use-a-command-line-to-install-sites.md).


## <a name="install-a-new-site"></a>Nainstalovat novou lokalitu
Pokud k instalaci nové lokality obou větví použijete základní médium 1606, použijte postupy pro plánování, přípravu a instalaci, které jsou popsané v tématu [Instalace lokalit Configuration Manager](../servers/deploy/install/installing-sites.md) , s přidáním následujících požadavků pro instalaci:

- Během instalace musíte zvolit větev Configuration Manager, kterou chcete nainstalovat, a můžete zadat podrobnosti o vaší smlouvě Software Assurance.
- Všechny lokality ve stejné hierarchii musí spouštět stejnou větev. Není podporováno, aby hierarchie se směsí LTSB a Current Branch v různých lokalitách.
- Nová skriptovaná instalace. Další informace najdete v části nové možnosti instalace pomocí skriptů výše v tomto článku.

## <a name="expand-a-stand-alone-primary-site"></a>Rozšíření samostatné primární lokality
Můžete rozšířit samostatnou primární lokalitu, která spouští rozhraní LTSB.  Tento proces se neliší od použití pro lokalitu Current Branch s jednou výstrahou:

- Při instalaci nové lokality centrální správy je nutné použít instalaci z původního zdrojového média, které jste použili k instalaci webu LTSB. Spuštění instalačního programu z disku CD-ROM. Poslední složka pro tento scénář není podporována.

Další informace o rozšíření lokality naleznete v části "rozšíření samostatné primární lokality" v tématu [instalace lokality pomocí Průvodce instalací nástroje](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md).

## <a name="upgrade-from-system-center-2012-configuration-manager"></a>Upgrade ze System Center 2012 Configuration Manager
Při upgradu z nástroje System Center 2012 Configuration Manager použijte plánování, přípravu a postupy lokality, jak je popsáno v tématu [upgrade na Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md) , ale s následujícími změnami:

**Upgradujte na Current Branch:**
- Během instalace musíte zvolit Current Branch a můžete zadat podrobnosti o smlouvě Software Assurance.
- Nová skriptovaná instalace. Další informace najdete v části nové možnosti instalace pomocí skriptů výše v tomto článku.

**Upgradujte na LTSB:**  
- Další kroky, které je potřeba provést v kontrolním seznamu před upgradem.
- Během instalace musíte zvolit LTSB a můžete zadat podrobnosti o smlouvě Software Assurance.
- Můžete upgradovat jenom lokalitu, na které běží System Center 2012 Configuration Manager s aktualizací Service Pack 1, System Center 2012 Configuration Manager s aktualizací Service Pack 2, System Center 2012 R2 Configuration Manager s aktualizací Service Pack 1 nebo System Center 2012 R2 Configuration Manager bez aktualizace Service Pack.

### <a name="in-place-upgrade-paths-for-the-1606-baseline-media"></a>Cesty k místnímu upgradu pro médium 1606 směrného plánu
Pomocí základního média 1606 můžete upgradovat následující verze na licencovanou verzi Configuration Manager:
- System Center 2012 R2 Configuration Manager s aktualizací Service Pack 1
- System Center 2012 R2 Configuration Manager bez aktualizace Service Pack (vyžaduje použití základního média pro verzi 1606, které bylo znovu vydány 15. prosince 2016.)
- System Center 2012 Configuration Manager s aktualizací Service Pack 2
- System Center 2012 Configuration Manager s aktualizací Service Pack 1 (vyžaduje použití základního média pro verzi 1606, které bylo znovu vydány 15. prosince 2016.)


Tato média můžete také použít k upgradu nelicencované zkušební edice Current Branch na plně licencovanou verzi Current Branch.

Toto médium nepodporuje upgrade:
- Další verze System Center 2012 Configuration Manager.
- Configuration Manager 2007 nebo starší.
- Release Candidate instalace Configuration Manager.

## <a name="about-the-cdlatest-folder-and-the-ltsb"></a>O disku CD. Poslední složka a LTSB
Níže jsou uvedena omezení pro použití média, které Configuration Manager vytvoří na disku CD. Poslední složka na serveru lokality. Tato omezení platí pro lokality, na kterých běží LTSB:

Média na disku CD-ROM. Nejnovější složka je podporována pro:
- Site Recovery.
- Údržba lokality.
- Instalace dalších podřízených primárních lokalit.

Média na disku CD-ROM. Nejnovější složka není podporována pro:  
- Instalace lokality centrální správy jako součásti scénáře rozšíření lokality.

Další informace najdete [na disku CD. Poslední složka](../servers/manage/the-cd.latest-folder.md)

## <a name="backup-recovery-and-site-maintenance-for-the-ltsb"></a>Zálohování, obnovení a Údržba lokality pro LTSB
K zálohování, obnovení nebo spuštění údržby lokality na webu, na kterém běží LTSB, použijte pokyny a postupy [pro zálohování a obnovení pro Configuration Manager](../servers/manage/backup-and-recovery.md).  

Pomocí instalačního programu Configuration Manager z disku CD-ROM. Poslední složka zálohy vašeho webu LTSB.
