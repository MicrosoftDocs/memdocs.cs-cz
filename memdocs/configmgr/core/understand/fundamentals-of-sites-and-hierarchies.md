---
title: Základy lokalit a hierarchií
titleSuffix: Configuration Manager
description: Získejte základní informace o Configuration Manager lokalitách a hierarchiích.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4db1e15f-e832-4cf9-be33-d3971e635a55
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 04ed22436d750572fed8ce898c5ed3a23b71f239
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722813"
---
# <a name="fundamentals-of-sites-and-hierarchies-for-configuration-manager"></a>Základy lokalit a hierarchií pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Nasazení Configuration Manager musí být nainstalováno v doméně služby Active Directory. Základem tohoto nasazení je jeden nebo více Configuration Managerch lokalit, které tvoří hierarchii lokalit. Typ a umístění instalovaných lokalit poskytují možnost vertikálně navýšit kapacitu (rozšířit) v případě potřeby vaše nasazení, a poskytují klíčové služby spravovaným uživatelům a zařízením, bez ohledu na to, zda se jedná o jednu lokalitu nebo hierarchii více lokalit.

## <a name="hierarchies-of-sites"></a>Hierarchie lokalit
Při první instalaci Configuration Manager určí první Configuration Manager Server, který nainstalujete, rozsah vaší hierarchie. První lokalita Configuration Manager je základem, ze kterého budete spravovat zařízení a uživatele v podniku. Tato první lokalita musí být buď lokalita centrální správy nebo samostatná primární lokalita.  

 *Lokalita centrální správy* je vhodná pro rozsáhlá nasazení, poskytuje centrální bod správy a poskytuje flexibilitu při podpoře zařízení, která jsou distribuována v globální síťové infrastruktuře. Po instalaci lokality centrální správy budete muset nainstalovat jednu nebo několik primárních lokalit jako podřízených lokalit. Tato konfigurace je nezbytná, protože lokalita centrální správy přímo nepodporuje správu zařízení, což je funkce primární lokality. Lokalita centrální správy podporuje několik podřízených primárních lokalit. Podřízené primární lokality slouží k přímé správě zařízení a k řízení šířky pásma sítě, pokud jsou spravovaná zařízení v různých geografických umístěních.  

 *Samostatná primární lokalita* je vhodná pro menší nasazení a dá se použít ke správě zařízení bez nutnosti instalovat další lokality. I když samostatná primární lokalita může omezit velikost vašeho nasazení, podporuje scénář pozdějšího rozšíření vaší hierarchie instalací nové lokality centrální správy. V tomto scénáři rozšíření lokality se vaše samostatná primární lokalita stávají podřízenou primární lokalitou a pak můžete nainstalovat další podřízené primární lokality pod novou lokalitu centrální správy. Pak můžete rozšířit počáteční nasazení pro budoucí růst vašeho podniku.  

> [!TIP]  
>  Samostatná primární lokalita a podřízená primární lokalita jsou ve skutečnosti stejným typem lokality: primární lokalita. Rozdíl v názvu vychází ze vztahu v rámci hierarchie, který vzniká, pokud používáte lokalitu centrální správy. Tento vztah hierarchie může také omezit instalaci některých rolí systému lokality, které zvyšují funkčnost Configuration Manager. K tomuto omezení rolí dochází, protože některé role systému lokality lze instalovat pouze v lokalitě nejvyšší úrovně v hierarchii, lokalitě centrální správy nebo samostatné primární lokalitě.  

 Po instalaci první lokality můžete nainstalovat další lokality. Pokud byla první lokalita lokalitou centrální správy, můžete nainstalovat jednu nebo více podřízených primárních lokalit. Po instalaci primární lokality (samostatné nebo podřízené primární) můžete nainstalovat jednu nebo více sekundárních lokalit.  

 *Sekundární lokalitu* lze nainstalovat pouze jako podřízenou lokalitu primární lokality. Tento typ lokality rozšiřuje rozsah primární lokality tak, aby byla možná správa zařízení v umístěních s pomalým síťovým připojením k primární lokalitě. I když sekundární lokalita rozšiřuje primární lokalitu, primární lokalita spravuje všechny klienty. Sekundární lokalita poskytuje podporu pro zařízení ve vzdáleném umístění. Poskytuje podporu komprimací a následnou správou přenosů informací v síti, které odesíláte (nasazujete) klientům a které klienti odesílají zpět do lokality.  

 Na následujících schématech je znázorněno několik příkladů návrhů lokalit.  

 ![Příklady hierarchie](media/Hierarchy_examples.png)  

 Další informace najdete v následujících tématech:  

-   [Úvod do nástroje Configuration Manager](../../core/understand/introduction.md)  

-   [Návrh hierarchie lokalit pro Configuration Manager](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)  

-   [Nainstalovat Configuration Manager lokality](../servers/deploy/install/installing-sites.md)  

## <a name="site-system-servers-and-site-system-roles"></a>Servery systému lokality a role systému lokality  
 Každá Configuration Manager lokality nainstaluje *role systému lokality* , které podporují operace správy. Následující role jsou nainstalovány ve výchozím nastavení, když instalujete lokalitu nástroje:

-   Role serveru lokality je přiřazena k počítači, do kterého instalujete lokalitu nástroje.

-   Role serveru databáze lokality je přiřazena k SQL Server, která je hostitelem databáze lokality.

Jiné role systému lokality jsou volitelné a používají se pouze v případě, že chcete používat funkce, které jsou aktivní v roli systému lokality. Jakýkoli počítač, který je hostitelem role systému lokality, je označován jako server systému lokality.  

 Pro menší nasazení Configuration Manager můžete zpočátku spustit všechny role systému lokality přímo na počítači serveru lokality. Poté, co vaše spravované prostředí potřebuje růst, můžete nainstalovat další servery systému lokality, které budou hostovat další role systému lokality, aby se zlepšila efektivita webu pro poskytování služeb pro více zařízení.  

 Informace o různých rolích systému lokality najdete v tématu [role systému lokality](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) v tématu [Plánování serverů systému lokality a rolí systému lokality pro Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

## <a name="publishing-site-information-to-active-directory-domain-services"></a>Publikování informací o lokalitě ve službě AD DS (Active Directory Domain Services)  
 Chcete-li zjednodušit správu Configuration Manager, můžete roztáhnout schéma služby Active Directory tak, aby podporovalo podrobnosti, které jsou používány Configuration Manager a potom weby publikují své klíčové informace do Active Directory Domain Services (služba AD DS). Počítače, které chcete spravovat, můžou bezpečně načítat informace týkající se webu z důvěryhodného zdroje služba AD DS. Informace, které mohou klienti načítat, identifikují dostupné lokality, servery systému lokality a služby, které tyto servery systému lokality poskytují.  

 *Rozšíření schématu služby Active Directory* se provádí jenom jednou pro každou doménovou strukturu a dá se provést před nebo po instalaci Configuration Manager.   Když rozšíříte schéma, musíte vytvořit nový kontejner služby Active Directory s názvem System Management v každé doméně. Kontejner obsahuje Configuration Manager web, který bude publikovat data pro klienty, které chcete najít. Další informace najdete v tématu [Příprava služby Active Directory pro publikování lokality](../../core/plan-design/network/extend-the-active-directory-schema.md).  

 *Publikování dat webu* zlepšuje zabezpečení vaší Configuration Manager hierarchie a snižuje administrativní režii, ale není vyžadováno pro základní funkce Configuration Manager.  
