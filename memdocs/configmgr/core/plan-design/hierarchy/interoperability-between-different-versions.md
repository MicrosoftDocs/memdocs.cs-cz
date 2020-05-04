---
title: Vzájemná funkční spolupráce mezi verzemi
titleSuffix: Configuration Manager
description: Zjistěte, jak se vyhnout konfliktům mezi více Configuration Manager hierarchií ve stejné síti.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d8d5eeeeafa775514bb46fa0906f22572343611d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713083"
---
# <a name="interoperability-between-different-versions-of-configuration-manager"></a>Vzájemná funkční spolupráce mezi různými verzemi Configuration Manageru

*Platí pro: Configuration Manager (Current Branch)*

Ve stejné síti můžete nainstalovat a provozovat víc nezávislých hierarchií Configuration Manager. Protože však různé hierarchie Configuration Manager nespolupracují mimo proces migrace, vyžaduje Každá hierarchie konfigurace, které zabrání konfliktům mezi nimi. Kromě toho můžete vytvořit určité konfigurace, které pomůžou prostředkům, které spravujete, pracovat se systémy lokality ze správné hierarchie.  

## <a name="interoperability-between-current-branch-and-earlier-versions"></a><a name="BKMK_SupConfigInterop"></a>Interoperabilita mezi aktuální větví a staršími verzemi  

Lokality různých verzí nemohou koexistovat ve stejné Configuration Manager hierarchii. Jediné výjimky jsou během procesu následujících scénářů upgradu:

- Z verze System Center 2012 Configuration Manager do Configuration Manager aktuální větev
- Z jedné Configuration Manager aktuální verze větve do novější verze pomocí konzolových aktualizací

Configuration Manager lokalitu aktuální větve a hierarchii můžete nasadit vedle existující lokality nástroje System Center 2012 Configuration Manager nebo hierarchie. Naplánujte, aby se klientům z jedné verze zabránilo v pokusu o připojení k lokalitě z jiné verze.

Pokud například dvě nebo více Configuration Manager hierarchií mají [překrývající se hranice](../../servers/deploy/configure/boundary-groups.md#overlapping-boundaries) , které zahrnují stejná síťová umístění, přiřaďte každého nového klienta k určité lokalitě místo použití automatického přiřazení lokality. Další informace najdete v tématu [přiřazení klientů k lokalitě](../../clients/deploy/assign-clients-to-a-site.md).  

Kromě toho nemůžete nainstalovat klienta nástroje ze System Center 2012 Configuration Manager do počítače, který hostuje roli systému lokality z Configuration Manager aktuální větev. Do počítače, který hostuje roli systému lokality ze služby System Center 2012 Configuration Manager, nemůžete také nainstalovat Configuration Manager klienta aktuální větve.  

Následující klienti a připojení nejsou podporováni:  

- Jakákoli verze počítačového klienta System Center 2012 Configuration Manager nebo starší verze  

- Jakýkoli klient správy zařízení nástroje System Center 2012 Configuration Manager nebo dřívější verze  

- Klient správy zařízení systém Windows CE Platform Builder (libovolná verze)  

- Připojení k síti VPN technologie System Center Mobile Device Manager  

### <a name="client-site-assignment-considerations"></a><a name="BKMK_SupConfigSiteAssignment"></a> Důležití informace o přiřazování klientů k lokalitám  

Configuration Manager klientech se dají přiřadit jenom k jedné primární lokalitě. Pokud jsou splněné všechny následující podmínky, nemůžete předpovědět skutečné přiřazení lokality klienta:

- Pomocí automatického přiřazení lokality můžete přiřadit klienty k lokalitě během instalace klienta.
- Víc než jedna skupina hranic obsahuje stejnou hranici.
- Skupiny hranic mají různé přiřazené lokality.

Pokud se hranice překrývají napříč více Configuration Manager lokalitami a hierarchiemi, nemusí být klienti přiřazeni k lokalitě, kterou jste očekávali, nebo se k lokalitě nemusí přiřadit vůbec.  

Configuration Manager klienti aktuální větve kontrolují verzi lokality předtím, než dokončí přiřazení lokality. Pokud se hranice lokality překrývají, nemůžete přiřadit klienty k lokalitě s předchozí verzí. Starší verze nástroje System Center 2012 Configuration Manager pravděpodobně nebudou nesprávně přiřazeny k novějším Configuration Managermu webu aktuální pobočky.  

Chcete-li zabránit tomu, aby se klienti z neúmyslného přiřazení k nesprávné lokalitě, když se překrývají hranice dvou hierarchií, nakonfigurujte parametry instalace klienta, aby bylo možné přiřadit klienty k určité lokalitě.  

## <a name="configuration-manager-limitations-in-a-mixed-version-hierarchy"></a><a name="bkmk_mixed"></a>Omezení Configuration Manager v hierarchii se smíšenými verzemi  

Když upgradujete Configuration Manager aktuální hierarchie větví, dojde k nějakým časům, kdy různé lokality budou mít různé verze. Například je třeba nejprve upgradovat lokalitu centrální správy. Z důvodu oken údržby lokality neprovedete upgrade primárních lokalit do pozdějšího data a času.  

Když různé lokality v jedné hierarchii používají různé verze, některé funkce nejsou k dispozici. Toto chování může mít vliv na to, jak spravovat Configuration Manager objekty v konzole Configuration Manager a jaké funkce jsou k dispozici pro klienty. Funkce z novější verze Configuration Manager nejsou obvykle dostupné v lokalitách nebo klientům, kteří používají nižší verzi aktualizace Service Pack.  

### <a name="network-access-account"></a>Účet přístupu k síti

Upgradujete lokalitu centrální správy na Configuration Manager aktuální větev. Podrobnosti o účtu přístupu k síti si můžete zobrazit z konzoly Configuration Manager, která je připojená k této aktualizované lokalitě. Nezobrazuje podrobnosti o účtu na webech, na kterých pořád běží System Center 2012 Configuration Manager.

Po upgradu primární lokality na stejnou verzi jako lokalita centrální správy jsou podrobnosti o účtu viditelné v konzole nástroje.

Stejné chování platí při aktualizaci mezi verzemi Configuration Manager.

### <a name="boot-images-for-os-deployment"></a>Spouštěcí bitové kopie pro nasazení operačního systému

#### <a name="when-upgrading-from-system-center-2012-configuration-manager-to-configuration-manager-current-branch"></a>Při upgradu z verze System Center 2012 Configuration Manager na Configuration Manager aktuální větev

Když lokalita nejvyšší úrovně v hierarchii upgraduje na Configuration Manager aktuální větev, automaticky aktualizuje výchozí spouštěcí image tak, aby používala sadu Windows Assessment and Deployment Kit (ADK) verze 10. Tyto spouštěcí image použijte jenom pro nasazení do klientů v Configuration Manager aktuální pobočky. Další informace najdete v tématu [plánování interoperability nasazení operačního systému](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md).

#### <a name="when-upgrading-between-configuration-manager-current-branch-versions"></a>Při upgradu mezi Configuration Manager aktuálními verzemi větví

Pokud nové verze nástroje Configuration Manager neaktualizují verzi ADK systému Windows, která se používá, nebude to mít žádný vliv na spouštěcí bitové kopie.

### <a name="new-task-sequence-steps"></a>Nové kroky pořadí úkolů

Když vytvoříte pořadí úkolů s krokem představeným v jedné verzi Configuration Manager, která není k dispozici v dřívější verzi, může dojít k následujícím problémům:

- Pokud se pokusíte upravit pořadí úkolů z lokality, na které běží předchozí verze Configuration Manager, dojde k chybě.

- Pořadí úkolů se nespustí na počítači, na kterém je spuštěná předchozí verze klienta Configuration Manager.

### <a name="client-to-down-level-management-point-communications"></a>Komunikace klienta s bodem správy nižší úrovně

Klient Configuration Manager, který komunikuje s bodem správy z lokality používající nižší verzi, než má klient, může používat pouze funkce, které verze Configuration Manager nižší úrovně podporuje. Například pokud nasadíte obsah z Configuration Manager lokality aktuální větve, která byla nedávno upgradována na klienta nástroje, který komunikuje s bodem správy, který dosud nebyl upgradován na tuto verzi, nemůže tento klient použít nové funkce z nejnovější verze.

### <a name="package-and-task-sequence-deployments-to-legacy-clients"></a>Nasazení balíčků a pořadí úkolů do starších verzí klientů

<!-- SCCMDocs-pr issue #3493 -->

Počínaje verzí 1902 nemůžete nasadit balíček nebo pořadí úloh do klienta verze 5,7730 nebo starší. Pokud chcete toto omezení obejít, upgradujte klienta na novější verzi.

## <a name="software-updates"></a>Aktualizace softwaru

### <a name="orchestration-groups"></a>Skupiny orchestrace

Skupiny Orchestration, představené ve verzi 2002, se nedají použít v hierarchii se smíšenými verzemi. <!--SCCMDocs-pr issue ##5056, 6389000-->

## <a name="interoperability-for-the-configuration-manager-console"></a><a name="BKMK_ConsoleInterop"></a>Interoperabilita pro konzolu Configuration Manager  

Tato část obsahuje informace o použití konzoly Configuration Manager v prostředí, které obsahuje kombinaci Configuration Manager verzí.  

### <a name="an-environment-with-both-system-center-2012-configuration-manager-and-configuration-manager-current-branch"></a>Prostředí s nástrojem System Center 2012 Configuration Manager a Configuration Manager aktuální větví

Aby bylo možné spravovat Configuration Manager lokalitu nástroje, konzola i lokalita, ke které se konzola připojuje, musí používat stejnou verzi Configuration Manager. Například nemůžete použít konzolu nástroje System Center 2012 Configuration Manager ke správě Configuration Manager aktuální pobočky nebo jiným způsobem.

Instalace konzoly nástroje System Center 2012 Configuration Manager a konzoly Configuration Manager aktuální větve ve stejném počítači není podporována.

### <a name="an-environment-with-multiple-versions-of-configuration-manager"></a>Prostředí s několika verzemi Configuration Manager

Configuration Manager aktuální větev nepodporuje instalaci více než jedné konzoly Configuration Manager v počítači. Chcete-li použít více konzol, které jsou specifické pro různé verze Configuration Manager, nainstalujte různé konzoly na samostatné počítače.

Během procesu aktualizace lokalit v hierarchii nástroje na novou verzi můžete připojit konzolu k lokalitě, která používá novější verzi, a zobrazit informace o ostatních lokalitách v této hierarchii. Tato konfigurace se ale nedoporučuje. Je možné, že rozdíly mezi verzí konzoly a verzí Configuration Manager lokality můžou způsobit problémy s daty. Některé funkce, které jsou k dispozici v nejnovější verzi produktu, nebudou v konzole k dispozici.

Při použití konzoly s verzí, která neodpovídá verzi lokality, není Správa lokality podporována. To může způsobit ztrátu dat a může ohrozit váš web. Například není podporováno použití konzoly z verze 1610 ke správě lokality, na které běží verze 1606.
