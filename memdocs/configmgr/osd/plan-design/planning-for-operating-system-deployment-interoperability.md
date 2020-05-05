---
title: Interoperabilita nasazení operačního systému
titleSuffix: Configuration Manager
description: Pokud různé Configuration Manager weby v jedné hierarchii používají různé verze, můžete pochopit problémy s interoperabilitou.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5931c43f0f8513ea1819e00f4eac7ecfd35dc717
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723548"
---
# <a name="plan-for-os-deployment-interoperability"></a>Plánování interoperability nasazení operačního systému

*Platí pro: Configuration Manager (Current Branch)*

Pokud různé Configuration Manager weby v jedné hierarchii používají různé verze, některé funkce Configuration Manager nejsou k dispozici. Funkce z novější verze Configuration Manager nejsou obvykle dostupné v lokalitách nebo klientech, kteří používají nižší verzi. Další informace najdete v tématu [vzájemná funkční spolupráce mezi různými verzemi Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  


## <a name="objects"></a>Objekty

Při upgradu lokality nejvyšší úrovně ve vaší hierarchii a dalších lokalit v hierarchii Vezměte v úvahu následující objekty Configuration Manager s nižší verzí:  

### <a name="client-installation-package"></a>Instalační balíček klienta  

- Zdroj výchozího instalačního balíčku klienta je automaticky upgradován. Všechny distribuční body v hierarchii se aktualizují pomocí nového instalačního balíčku klienta. K tomuto chování dochází i v distribučních bodech v lokalitách v hierarchii, které mají nižší verzi.  

- Nemůžete přiřadit nové verze klientům lokalitám, které jste ještě neupgradovali na novou verzi. Přiřazení je blokováno v bodu správy.  

### <a name="boot-images"></a>Spouštěcí image  

- Při upgradu lokality nejvyšší úrovně na nejnovější verzi Configuration Manager automaticky aktualizuje výchozí spouštěcí image (x86 a x64). Tato aktualizace používá Windows ADK pro Windows 10, která zahrnuje Windows PE 10. Soubory, které jsou přidruženy k výchozím spouštěcím bitovým kopiím, jsou aktualizovány pomocí nejnovější Configuration Manager verze souborů. Lokalita nebude automaticky aktualizovat vlastní spouštěcí image. Je potřeba ručně aktualizovat vlastní spouštěcí image, které zahrnují starší verze prostředí Windows PE.  

- Pokud vaše hierarchie lokality obsahuje lokality s různými verzemi Configuration Manager, vyhněte se použití dynamického média. Místo toho použijte médium založené na lokalitě pro kontaktování určitého bodu správy. Po aktualizaci všech lokalit na stejnou verzi Configuration Manager můžete znovu použít dynamické médium.

- Ověřte, že jsou k disConfiguration Manager nejnovější bitové spouštěcí kopie, včetně vlastních nastavení. Pak aktualizujte všechny distribuční body v nových verzích na nové verzi pomocí nejnovější verze nových spouštěcích imagí.  

### <a name="user-state-migration-tool-usmt"></a>Nástroj pro migraci stavu uživatele (USMT)  

Když upgradujete lokalitu nejvyšší úrovně na nejnovější verzi Configuration Manager, automaticky aktualizuje výchozí balíček USMT na nejnovější verzi. Neaktualizuje automaticky žádné vlastní balíčky nástroje USMT. Tyto balíčky budete muset aktualizovat ručně.  

### <a name="new-task-sequence-steps"></a>Nové kroky pořadí úkolů  

Nové kroky pořadí úloh jsou pravidelně zavedeny s novými verzemi Configuration Manager. Když nasadíte pořadí úkolů s novým krokem na starší klienty, krok pořadí úkolů se nezdařil. Než nasadíte pořadí úkolů s novým krokem, ujistěte se, že jsou klienti v cílové kolekci aktualizovaní na novou verzi.  

### <a name="os-deployment-media"></a>Média pro nasazení operačního systému  

Pokud je lokalita aktualizována na novou verzi, aktualizujte všechna média pomocí nového balíčku Configuration Manager klienta. Mezi tyto typy médií patří spouštěcí, zachytává, předzpracovaná a samostatná.

### <a name="third-party-extensions-to-os-deployment"></a>Rozšíření pro nasazení operačního systému od jiných výrobců  

Máte-li rozšíření pro nasazení operačního systému od jiných výrobců a máte různé verze Configuration Managerch webů nebo Configuration Manager klientů, může dojít k problémům s rozšířeními.  


## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>Nejnovější verze Configuration Manager lokalit ve smíšené hierarchii  

Když upgradujete lokalitu na nejnovější verzi Configuration Manager, sekvence úloh, které odkazují na výchozí instalační balíček klienta, automaticky spustí nasazení nejnovější verze Configuration Manager klienta.

Pořadí úkolů, která odkazují na vlastní instalační balíček klienta, budou pokračovat v nasazování verze klienta, která je obsažena v tomto vlastním balíčku. Vlastní balíčky nejspíš obsahují starší verzi Configuration Manager klienta. Aby se zabránilo chybám při nasazování pořadí úloh, aktualizujte všechny vlastní instalační balíčky klienta na nejnovější verzi.

Když nakonfigurujete pořadí úkolů pro použití vlastního instalačního balíčku klienta, proveďte jednu z následujících akcí:

- Aktualizujte krok pořadí úkolů tak, aby používal nejnovější verzi Configuration Manager instalačního balíčku klienta.
- Aktualizace vlastního balíčku pro použití nejnovějšího Configuration Manager zdroje instalace klienta

> [!IMPORTANT]  
> Nesaďte pořadí úkolů, které odkazuje na nejnovější Configuration Manager instalační balíček klienta na klienty ve starší Configuration Manager lokalitě. Když se klienti přiřazení k síti starší verze Configuration Manager upgradují na nejnovější verzi klienta Configuration Manager, Configuration Manager zablokuje přiřazení ke starší Configuration Manager lokalitě. Tito klienti již nejsou přiřazeni k žádné lokalitě. Dokud ručně nepřiřazujete klienta k nejnovější Configuration Manager lokalitě nebo přeinstalujete starší verzi Configuration Manager klienta v počítači, tito klienti nejsou spravováni.


## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>Starší verze Configuration Manager ve smíšené hierarchii  

Když upgradujete lokalitu centrální správy na nejnovější verzi Configuration Manager, ujistěte se, že pořadí úloh nasazení operačního systému nenechávají tyto klienty v nespravovaném stavu. Například pokud nasadíte klienta na starší Configuration Manager lokalitu, kterou jste dosud neupgradovali na nejnovější verzi Configuration Manager.

Vytvořte kopii pořadí úkolů, které použijete k nasazení na klienty v nejnovější verzi Configuration Manager lokality. Pak upravte pořadí úkolů, abyste ho mohli nasadit na klienty na starší Configuration Manager lokalitě. Nakonfigurujte pořadí úkolů tak, aby odkazovalo na vlastní instalační balíček klienta, který používá starší Configuration Manager zdroj instalace klienta. Pokud ještě nemáte vlastní instalační balíček klienta, který odkazuje na starší zdroj instalace klienta Configuration Manager, vytvořte ho ručně.  

> [!Important]  
> Počínaje verzí 1902 nemůžete nasadit balíček nebo pořadí úloh do klienta verze 5,7730 nebo starší. Pokud chcete toto omezení obejít, upgradujte klienta na novější verzi.<!-- SCCMDocs-pr issue #3493 -->
