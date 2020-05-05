---
title: Příprava instalace lokalit
titleSuffix: Configuration Manager
description: Pokud plánujete instalaci více lokalit Configuration Manager, přečtěte si tyto informace, které vám pomůžou ušetřit čas a vyhnout se chybám.
ms.date: 09/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 87c1713f9903cf704e484c49f7e720e6f0bd3e4a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718179"
---
# <a name="prepare-to-install-configuration-manager-sites"></a>Příprava na instalaci Configuration Managerch lokalit

*Platí pro: Configuration Manager (Current Branch)*

Pro přípravu úspěšného nasazení jednoho nebo více Configuration Manager lokalit se seznamte s podrobnostmi v tomto článku. Pomocí těchto kroků můžete ušetřit čas během instalace více webů a pomáhat zabránit nepotřebným krokům, které by mohly vést k přeinstalování jedné nebo více lokalit.

> [!TIP]
> Při správě Configuration Manager infrastruktury lokalit a hierarchie se používají výrazy *upgradu*, *aktualizace*a *instalace* , které popisují tři samostatné koncepty. Informace o tom, jak se jednotlivé podmínky používají, najdete v tématu věnovaném [upgradu, aktualizaci a instalaci](../../../understand/upgrade-update-install.md).

## <a name="options-for-installing-different-types-of-sites"></a><a name="bkmk_options"></a>Možnosti instalace různých typů lokalit
Když nainstalujete novou lokalitu Configuration Manager, verze zdrojových souborů, které můžete použít, závisí na verzi lokalit, které jsou již v hierarchii (pokud existuje). Metody instalace, které můžete použít, závisí na typu lokality, kterou chcete nainstalovat.  

Před instalací lokality nástroje se ujistěte, že jste naplánovali hierarchii a rozumíte typu lokality, kterou chcete nainstalovat. Další informace najdete v tématu [Návrh hierarchie lokalit](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).


### <a name="first-site"></a>První lokalita
První lokalita, kterou nainstalujete v hierarchii, bude buď samostatná primární lokalita nebo lokalita centrální správy.

**Instalační médium**: Chcete-li nainstalovat lokalitu centrální správy nebo samostatnou primární lokalitu jako první lokalitu v nové hierarchii, je nutné [použít základní verzi](../../../../core/servers/manage/updates.md#bkmk_Baselines) Configuration Manager. Neinstalujte první lokalitu nové hierarchie pomocí aktualizovaných zdrojových souborů z [disku CD-ROM. Poslední složka](../../../../core/servers/manage/the-cd.latest-folder.md) libovolného webu

**Metoda instalace**: libovolný typ lokality můžete nainstalovat pomocí [Průvodce instalací Configuration Manager](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md), nebo můžete nakonfigurovat skript pro použití s [instalací skriptu spouštěného na příkazovém řádku](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).


### <a name="additional-sites"></a>Další lokality
Po instalaci počáteční lokality můžete kdykoli přidat další lokality. Pro přidávání lokalit máte tyto možnosti (až do [podporovaných limitů](../../../../core/plan-design/configs/size-and-scale-numbers.md)):

|Lokalita, kterou máte|Další typ lokality, kterou můžete nainstalovat|
|---|---|
|Lokalita centrální správy|Podřízená primární lokalita|
|Podřízená primární lokalita|Sekundární lokalita|
|Samostatná primární lokalita|Sekundární lokalita (můžete rozbalit primární lokalitu, která převede samostatnou primární lokalitu na podřízenou primární lokalitu).|

**Instalační médium**: Když nainstalujete lokalitu centrální správy pro rozšíření samostatné primární lokality nebo pokud v existující hierarchii nainstalujete novou podřízenou primární lokalitu, musíte použít instalační média (která obsahuje zdrojové soubory), která odpovídá verzi existující lokality nebo lokality.

> [!IMPORTANT]
> Pokud jste nainstalovali konzolové aktualizace, které změnily verzi dříve nainstalovaných webů, nepoužívejte původní instalační médium. Místo toho v tomto scénáři použijte zdrojové soubory z [disku CD-ROM. Poslední složka](../../../../core/servers/manage/the-cd.latest-folder.md) aktualizované lokality. Configuration Manager vyžaduje, abyste použili zdrojové soubory, které odpovídají verzi existující lokality, ke které se vaše lokalita bude připojovat.

Sekundární lokalita musí být nainstalována z konzoly Configuration Manager. Tímto způsobem jsou sekundární lokality vždy nainstalovány pomocí zdrojových souborů z nadřazené primární lokality.

**Metoda instalace**: metoda, kterou použijete k instalaci dalších lokalit, závisí na typu lokality, kterou chcete nainstalovat.
- **Přidat lokalitu centrální správy**: k instalaci nové lokality centrální správy jako nadřazené lokality do existující samostatné primární lokality můžete použít průvodce instalací Configuration Manager nebo skriptový příkazový řádek. Další informace najdete v tématu [rozšíření samostatné primární lokality](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand).
- **Přidat podřízenou primární lokalitu**: pomocí Průvodce instalací nástroje Configuration Manager nebo pomocí instalace příkazového řádku můžete přidat podřízenou primární lokalitu pod lokalitu centrální správy.
- **Přidat sekundární lokalitu**: pomocí konzoly Configuration Manager nainstalujte sekundární lokalitu jako podřízenou lokalitu pod primární lokalitou. Jiné metody nejsou podporovány pro přidávání sekundárních lokalit.

## <a name="common-tasks-to-complete-before-starting-an-installation"></a><a name="bkmk_tasks"></a>Běžné úlohy, které je potřeba dokončit před zahájením instalace
- **Pochopení topologie hierarchie, kterou použijete pro nasazení**    
Další informace najdete v tématu [Návrh hierarchie lokalit pro Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

- **Příprava a konfigurace jednotlivých serverů pro splnění požadavků a podporovaných konfigurací pro použití s Configuration Manager**         
Další informace najdete v tématu [Požadované součásti lokality a systému lokality](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

- **Instalace a konfigurace SQL Server pro hostování databáze lokality**     
Další informace najdete v tématu [podpora verzí SQL Server pro Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

- **Příprava síťového prostředí na podporu Configuration Manager**      
Další informace najdete v tématu [Konfigurace bran firewall, portů a domén pro přípravu na Configuration Manager](../../../../core/plan-design/network/configure-firewalls-ports-domains.md).  

- **Pokud budete používat infrastrukturu veřejných klíčů (PKI), připravte svoji infrastrukturu a certifikáty.**      
Další informace najdete v tématu [požadavky na certifikát PKI pro Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).

- **Nainstalujte nejnovější aktualizace zabezpečení na počítačích, které budete používat jako servery lokality nebo servery systému lokality, a v případě potřeby je znovu spusťte.**

## <a name="about-site-names-and-site-codes"></a><a name="bkmk_sitecodes"></a>O názvech webů a kódech lokalit
Kódy lokalit a názvy lokalit slouží k identifikaci a správě lokalit v hierarchii Configuration Manager. V konzole Configuration Manager se kód lokality a název lokality &lt;zobrazují ve formátu*názvu* \> lokality *kódu*\> - &lt;lokality. Každý kód lokality, který používáte ve vaší hierarchii, musí být jedinečný. Je-li schéma služby Active Directory rozšířeno pro Configuration Manager a vaše weby publikují data, musí být kódy lokalit používané v doménové struktuře služby Active Directory jedinečné, i když jsou používány v jiné hierarchii Configuration Manager nebo pokud byly použity v předchozích Configuration Manager instalacích. Před nasazením hierarchie nezapomeňte pečlivě naplánovat kódy a názvy lokalit.

### <a name="specify-a-site-code-and-site-name"></a>Zadejte kód lokality a název lokality
Když spustíte instalační program Configuration Manager, zobrazí se výzva k zadání kódu lokality a názvu lokality pro lokalitu centrální správy a pro každou primární lokalitu a instalaci sekundární lokality. Kód lokality musí jednoznačně identifikovat každou lokalitu v hierarchii. Vzhledem k tomu, že se kód lokality používá v názvech složek, nikdy pro kód lokality nepoužívejte následující názvy, které zahrnují názvy rezervované pro Configuration Manager a Windows:
- POMOCNÉ
- PŘ
- NUL
- PRN
- SMS
- ENV <!--SCCMDocs-1871 and 5399453-->

> [!NOTE]
> Instalační program Configuration Manager neověřuje, zda se kód lokality již nepoužívá.

Pokud chcete pro web zadat kód lokality, když spouštíte Configuration Manager instalační program, musíte zadat tři alfanumerické znaky. V kódu lokality jsou povoleny *pouze písmena a* až *Z* a čísla *0* až *9*v libovolné kombinaci. Posloupnost písmen nebo číslic nemá žádný vliv na komunikaci mezi lokalitami. Například není nutné pojmenovat primární lokalitu *ABC* a sekundární lokalitu *def*.

Název webu je identifikátor popisného názvu webu. Můžete použít pouze znaky *A* až *z*, *a* až *z*, *0* až *9*a spojovník (*-*) v názvech webů.

> [!IMPORTANT]
> Změna kódu lokality nebo názvu lokality po instalaci lokality není podporována.

### <a name="reuse-a-site-code"></a>Opětovné použití kódu lokality
Kódy lokality nelze použít více než jednou v hierarchii Configuration Manager pro lokalitu centrální správy nebo pro primární lokalitu, a to i v případě, že původní lokalita a kód lokality byly odinstalovány. Pokud kód lokality znovu použijete, riskujete, že v hierarchii jsou konflikty ID objektů. Můžete použít kód lokality pro sekundární lokalitu, pokud se tato sekundární lokalita a kód lokality již nepoužívají ve vaší Configuration Manager hierarchii nebo v doménové struktuře služby Active Directory.

## <a name="limits-and-restrictions-for-installed-sites"></a>Omezení a omezení pro nainstalované lokality
Než nainstalujete lokalitu nástroje, je důležité pochopit následující omezení, která platí pro lokality a hierarchie lokality:
- Po spuštění instalace nemůžete změnit následující vlastnosti lokality bez odinstalování lokality a pak ji znovu nainstalovat pomocí nových hodnot:  
  - Instalační adresář programových souborů  
  - Kód lokality  
  - Popis webu  
- Pokud vaše hierarchie obsahuje lokalitu centrální správy:  
  - Configuration Manager nepodporuje přesunutí podřízené primární lokality mimo hierarchii, aby bylo možné vytvořit samostatnou primární lokalitu nebo ji připojit k jiné hierarchii. Místo toho odinstalujte podřízenou primární lokalitu a pak ji znovu nainstalujte jako novou samostatnou primární lokalitu nebo jako podřízenou lokalitu centrální lokality pro správu v jiné hierarchii.  


## <a name="optional-steps-before-running-setup"></a><a name="bkmk_optionalsteps"></a>Volitelné kroky před spuštěním instalačního programu
**Ruční spuštění nástroje pro [stažení instalačního programu](../../../../core/servers/deploy/install/setup-downloader.md)**

Chcete-li stáhnout aktualizované instalační soubory pro Configuration Manager, můžete spustit nástroj pro stažení instalačního programu. Pokud počítač, kde spustíte instalační program, není připojen k Internetu, nebo pokud očekáváte instalaci více serverů lokality, zvažte použití nástroje pro stažení instalačního programu, který stáhne požadované aktualizace instalačního programu. Tady jsou další informace:
- Ve výchozím nastavení se instalační program připojí k Internetu a stáhne aktualizované instalační soubory.
- Ve výchozím nastavení jsou soubory uloženy ve složce Redist.
- Instalaci můžete nasměrovat do umístění v síti, kde jste předtím uložili kopii těchto souborů.

**Ruční spuštění [kontroly požadovaných součástí](../../../../core/servers/deploy/install/prerequisite-checker.md)**

Chcete-li identifikovat a opravit problémy před spuštěním instalačního programu pro instalaci lokality a před instalací role systému lokality na server, můžete spustit kontrolu požadovaných součástí. Kontrola požadovaných součástí pomáhá zajistit, že počítač splňuje požadavky na hostování lokality nebo role systému lokality. Tady jsou další informace:
- Ve výchozím nastavení spustí instalační program kontrolu požadovaných součástí.
- Pokud dojde k chybám, instalace se zastaví, dokud se problém nevyřeší.

**Identifikace volitelných portů**

Můžete identifikovat volitelné porty pro systémy lokality a klienty, kteří se mají použít. Tady jsou další informace:
- Systémy lokality a klienti standardně používají předdefinované porty ke komunikaci.
- Během instalace můžete nakonfigurovat alternativní porty.

Další informace najdete v tématu [použité porty](../../../../core/plan-design/hierarchy/ports.md).
