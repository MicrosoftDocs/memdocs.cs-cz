---
title: Nástroj pro resetování aktualizací
titleSuffix: Configuration Manager
description: Použijte nástroj pro obnovení aktualizací pro konzolové aktualizace pro Configuration Manager.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 25fa89d6-7e47-45a6-8f4e-70b77560fba6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b4aa67280c879d6f7feaf549ac7f13ba0136ca91
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720748"
---
# <a name="update-reset-tool"></a>Nástroj pro resetování aktualizací

*Platí pro: Configuration Manager (Current Branch)*  


Počínaje verzí 1706, Configuration Manager primárními lokalitami a lokalitami centrální správy zahrnuje nástroj pro resetování aktualizací Configuration Manager **CMUpdateReset. exe**. Pomocí tohoto nástroje můžete opravit problémy, pokud mají aktualizace v konzole problémy při stahování nebo replikaci. Nástroj se nachází ve složce ***\CD.latest\SMSSETUP\TOOLS*** serveru lokality.

Tento nástroj můžete použít u libovolné verze aktuální větve, která zůstane v rámci podpory.

Tento nástroj použijte v případě, že [Konzola aktualizace](install-in-console-updates.md) není ještě nainstalována a je ve stavu selhání. Neúspěšný stav znamená, že stahování aktualizace probíhá, ale zablokovala nebo přebírá příliš dlouhou dobu. Dlouhá doba se považuje za hodiny delší než historická očekávání pro aktualizační balíčky podobné velikosti. Může se také jednat o selhání při replikaci aktualizace do podřízených primárních lokalit.  

Když nástroj spustíte, spustí se s aktualizací, kterou určíte. Ve výchozím nastavení Nástroj neodstraní úspěšně nainstalované nebo stažené aktualizace.  

### <a name="prerequisites"></a>Požadavky
Účet, který použijete ke spuštění nástroje, vyžaduje následující oprávnění:
- Oprávnění **ke čtení** a **zápisu** do databáze lokality centrální správy a do každé primární lokality ve vaší hierarchii. Chcete-li nastavit tato oprávnění, můžete přidat uživatelský účet jako člena **db_datawriter** a **db_datareader** [pevné databázové role](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) v databázi Configuration Manager jednotlivých lokalit. Nástroj nekomunikuje se sekundárními lokalitami.
- **Místní správce** v lokalitě nejvyšší úrovně ve vaší hierarchii.
- **Místní správce** na počítači, který je hostitelem spojovacího bodu služby.

Potřebujete GUID balíčku aktualizací, který chcete obnovit. Získání identifikátoru GUID:
  1.   V konzole nástroje přejdete na **Správa**  >  **aktualizace a údržba**.
  2.   V podokně zobrazení klikněte pravým tlačítkem myši na záhlaví jednoho ze sloupců (například **stav**) a pak vyberte možnost **identifikátor GUID balíčku** pro přidání tohoto sloupce do zobrazení.
  3.   Sloupec teď zobrazuje identifikátor GUID balíčku aktualizace.

> [!TIP]  
> Chcete-li zkopírovat identifikátor GUID, vyberte řádek balíčku aktualizací, který chcete obnovit, a potom pomocí kombinace kláves CTRL + C tento řádek zkopírujte. Pokud vložíte zkopírovaný výběr do textového editoru, můžete zkopírovat pouze identifikátor GUID, který se použije jako parametr příkazového řádku při spuštění nástroje.

### <a name="run-the-tool"></a>Spusťte nástroj.    
Nástroj musí být spuštěn v lokalitě nejvyšší úrovně v hierarchii.

Při spuštění nástroje použijte parametry příkazového řádku k zadání:
- SQL Server v lokalitě nejvyšší úrovně v hierarchii.
- Název databáze lokality v lokalitě nejvyšší úrovně.
- Identifikátor GUID balíčku aktualizací, který chcete obnovit.

Na základě stavu aktualizace nástroj identifikuje další servery, které potřebuje k přístupu.   

Pokud je balíček aktualizace ve stavu *po stažení* , nástroj nevyčistit balíček. Jako možnost můžete vynutit odebrání úspěšného stažení aktualizace pomocí parametru vynutit odstranění (viz parametry příkazového řádku dále v tomto tématu).

Po spuštění nástroje:
- Pokud byl balíček odstraněn, restartujte službu SMS_Executive v lokalitě nejvyšší úrovně. Pak zkontrolujte aktualizace, abyste mohli balíček znovu stáhnout.
- Pokud se balíček neodstranil, nemusíte provádět žádnou akci. Aktualizace se znovu inicializuje a pak restartuje replikaci nebo instalaci.

**Parametry příkazového řádku:**  


|                        Parametr                         |                                                       Description                                                        |
|----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **-S &lt; plně kvalifikovaný název domény SQL Server vaší lokality nejvyšší úrovně>** | *Požadováno* <br> Zadejte plně kvalifikovaný název domény SQL Server, který je hostitelem databáze lokality pro lokalitu nejvyšší úrovně ve vaší hierarchii. |
|                **-D &lt; název databáze>**                 |                          *Požadováno* <br> Zadejte název databáze v lokalitě nejvyšší úrovně.                          |
|                 **-P &lt;>identifikátor GUID balíčku**                 |                        *Požadováno* <br> Zadejte identifikátor GUID balíčku aktualizací, který chcete obnovit.                        |
|           **-I &lt; SQL Server název instance>**           |                    *Volitelné* <br> Identifikujte instanci SQL Server, která je hostitelem databáze lokality.                     |
|                       **-FDELETE**                       |                       *Volitelné* <br> Vynutit odstranění úspěšně staženého balíčku aktualizace.                        |

**4.6**  
V typickém scénáři chcete obnovit aktualizaci, která má problémy se stahováním. Plně kvalifikovaný název domény SQL serveru je *Server1.fabrikam.com*, databáze lokality je *CM_XYZ*a identifikátor GUID balíčku je *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Spustíte: ***CMUpdateReset. exe-S Server1.fabrikam.com-D CM_XYZ-P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

V extrémním scénáři chcete vynutit odstranění problematického balíčku aktualizace. Plně kvalifikovaný název domény SQL serveru je *Server1.fabrikam.com*, databáze lokality je *CM_XYZ*a identifikátor GUID balíčku je *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Spustíte: ***CMUpdateReset. exe-FDELETE-S Server1.fabrikam.com-D CM_XYZ-P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***
