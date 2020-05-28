---
title: Kterou větev mám použít
titleSuffix: Configuration Manager
description: Přečtěte si o rozdílech mezi dostupnými větvemi Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 542069b82ea4c68a48ccc47b79007fd2fa25322a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906009"
---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>Kterou větev nástroje Configuration Manager mám použít?

*Platí pro: Configuration Manager (Current Branch & Technical Preview Branch) & System Center Configuration Manager (dlouhodobá údržba Branch)*

K dispozici jsou tři větve Configuration Manager:

- Aktuální větev
- Long-Term Servicing Branch
- Větev Technical Preview

Tento článek vám může při výběru správné větve použít.

> [!TIP]  
> Všechny lokality v hierarchii musí používat stejnou větev. Nepodporuje hierarchii s různými větvemi v různých lokalitách.

## <a name="current-branch"></a>Aktuální větev

Tato větev je licencovaná pro použití v produkčním prostředí. Tuto větev použijte k získání nejnovějších funkcí a funkcí. Pokud máte jednu z následujících licencí, můžete použít tuto větev:  

- System Center Datacenter
- System Center Standard
- System Center Configuration Manager
- Ekvivalentní práva k předplatnému  

Další informace o možnostech programu Software Assurance a licencování najdete v tématu [licencování a větve pro Configuration Manager](learn-more-editions.md) a [nejčastější dotazy pro Configuration Manager pobočky a licencování](product-and-licensing-faq.md).

Microsoft plánuje vydávat aktualizace pro Configuration Manager aktuální větve několikrát za rok. Každá verze aktualizace zůstane v podpoře po dobu 18 měsíců od data vydání obecné dostupnosti (GA). Technická podpora je poskytována pro celou dobu podpory. Naše struktura podpory je ale dynamická a vyvíjí se ve dvou různých fázích údržby, které závisí na dostupnosti nejnovější aktuální verze větve. (Další informace najdete v tématu [podpora Configuration Manager aktuální verze větví](../servers/manage/current-branch-versions-supported.md). Aktualizace novějších verzí jsou k dispozici jako konzolové aktualizace.

K instalaci aktuální větve jako nového webu použijte [Základní médium](../servers/manage/updates.md#bkmk_Baselines). K upgradu ze System Center 2012 Configuration Manager s aktualizací Service Pack 2 nebo System Center 2012 R2 Configuration Manager s aktualizací Service Pack 1 použijte také základní médium směrného plánu. Přístup k tomuto médiu závisí na tom, jak vaše organizace Configuration Manager licence.

K instalaci nové lokality, která je zkušební edicí aktuální větve, můžete použít také základní médium. Zkušební edice nevyžaduje licenci. Zkušební edici můžete použít po dobu 180 dnů. Podporuje upgrade na licencovanou verzi aktuální větve. Pokud chcete nainstalovat jenom zkušební edici, Získejte ji z [centra hodnocení](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection).

> [!NOTE]
> K instalaci lokalit pro novou hierarchii Configuration Manager použijte základní média. Pokud jste dříve nainstalovali základní verzi, aktualizujte své weby na novou verzi pomocí konzolových aktualizací.  
>
> Lokality, které jsou aktualizované pomocí konzolových aktualizací, mají za následek to, že lokality jsou stejné jako u nové lokality nainstalované pomocí základního média.
>
> Další informace najdete v tématu [aktualizace pro Configuration Manager](../servers/manage/updates.md).  

### <a name="features-of-the-current-branch"></a>Funkce aktuální větve

- Přijímá [konzolové aktualizace](../servers/manage/install-in-console-updates.md) , které zpřístupňují nové funkce pro použití.
- Přijímá konzolové aktualizace, které dodávají opravy zabezpečení a kvality existujícím funkcím.
- V případě potřeby podporuje vzdálené aktualizace. Další informace najdete v tématu [použití nástroje pro registraci aktualizací](../servers/manage/use-the-update-registration-tool-to-import-hotfixes.md) nebo [použití instalačního programu oprav hotfix](../servers/manage/use-the-hotfix-installer-to-install-updates.md).
- Integruje se s cloudovou službou.
- Podporuje [migraci dat](../migration/migrate-data-between-hierarchies.md) do a z jiných Configuration Manager instalací.
- Podporuje upgrade z předchozích verzí Configuration Manager.
- Podporuje instalaci jako zkušební edici, ze které můžete později upgradovat na plně licencovanou instalaci.

Microsoft doporučuje, abyste po vydaných verzích brzo aktualizovali na nejnovější verzi. Před aktualizací na novější verzi můžete počkat až 18 měsíců. Můžete také přeskočit aktualizaci pro instalaci nejnovější dostupné verze. Vzhledem k tomu, že každá verze je kumulativní, Pokud přeskočíte na aktualizaci a nainstalujete nejnovější verzi, získáte přístup ke všem funkcím a vylepšením z předchozích verzí.

Další informace najdete v tématu [Podpora pro aktuální verze větví](../servers/manage/current-branch-versions-supported.md).

### <a name="current-branch-update-options"></a>Možnosti aktualizace aktuální větve

- Díky aktivnímu programu Software Assurance můžete instalovat aktualizace v konzole pro aktuální verze větví.  
- Neexistuje možnost převést aktuální větev na větev Technical Preview. Větve Technical Preview jsou samostatné instalace, které nevyžadují licenci.
- Neexistuje možnost převést svou aktuální větev na LTSB (Long-Term Servicing Branch). Musíte odinstalovat aktuální větev a pak nainstalovat LTSB jako novou instalaci.

## <a name="long-term-servicing-branch"></a>Long-Term Servicing Branch

Tato větev je licencovaná pro použití v produkčním prostředí pro Configuration Manager zákazníky, kteří používají aktuální větev, a mají povolené jejich Configuration Manager program Software Assurance (SA) nebo ekvivalentní práva k předplatnému od 1. října 2016. Další informace o možnostech licencování a programu Software Assurance najdete v tématu [licencování a větve pro Configuration Manager](learn-more-editions.md) a [Nejčastější dotazy týkající se Configuration Manager větví a licencování](product-and-licensing-faq.md).

LTSB je založen na verzi 1606. Tato větev neobdrží aktualizace v konzole, které dodávají nové funkce nebo aktualizují stávající možnosti. K dispozici jsou však důležité opravy zabezpečení. Pokud chcete nainstalovat LTSB, musíte použít [Základní médium](../servers/manage/updates.md#bkmk_Baselines) verze 1606, které získáte v rámci nástroje System Center 2016. Novější základní verze nepodporují instalaci rozhraní LTSB.

Pokud chcete nainstalovat LTSB jako novou lokalitu nebo jako upgrade z podporované lokality System Center 2012 Configuration Manager, použijte [Základní médium](../servers/manage/updates.md#bkmk_Baselines) verze 1606, které získáte v rámci nástroje system Center 2016. Pomocí média směrného plánu můžete nainstalovat novou lokalitu, která používá verzi 1606 aktuální větve, nebo novou lokalitu, která spouští určitou větev dlouhodobé údržby.

> [!TIP]  
> Informace o produktu System Center 2016 najdete v [dokumentaci k nástroji System center 2016](https://docs.microsoft.com/system-center/index). Tato dokumentace také označuje, jak získat produkt System Center 2016, který vyžaduje licenční smlouvu společnosti Microsoft nebo podobná práva.  
>  
> Chcete-li najít Configuration Manager verze 1606 na webu Volume Licensing Service Center (VLSC), klikněte na kartu **Stažení a klíče** [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), vyhledejte `System Center 2016` a potom vyberte buď **System center 2016 Datacenter** nebo **System Center 2016 Standard**.  
>  
> Můžete také získat zkušební edici System Center 2016 z [centra hodnocení](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview).  

### <a name="features-of-the-ltsb"></a>Funkce LTSB

- Přijímá konzolové aktualizace, které poskytují kritické opravy zabezpečení.
- Poskytuje možnost instalace v případě, že platnost vaší smlouvy SA nebo ekvivalentní práva k Configuration Manager vypršela.
- Podporuje upgrade (převod) na aktuální větev, pokud máte aktuální smlouvu SA nebo ekvivalentní práva k Configuration Manager.

### <a name="ltsb-limitations"></a>Omezení LTSB

LTSB je založen na aktuální větvi verze 1606 a má následující omezení:

- LTSB se podporuje po dobu 10 let kritických aktualizací zabezpečení po obecné dostupnosti (říjen 2016), po jejímž uplynutí vyprší podpora pro tuto větev. Další informace o životním cyklu podpory najdete v tématu [Zásady životního cyklu Microsoftu](https://support.microsoft.com/lifecycle).
- Podporuje seznam omezených sad serverových a klientských operačních systémů a souvisejících technologií, jako jsou verze SQL Server. Další informace najdete v tématu [podporované konfigurace pro odloučenou obsluhu](supported-configurations-for-ltsb.md).
- Nepřijímá aktualizace pro nové funkce
- Nepodporuje následující možnosti:
  - Funkce připojené ke cloudu, jako je spoluspráva nebo desktopová analýza
  - Místní správa MDM
  - Řídicí panel údržby Windows 10, plány údržby nebo půlroční kanál Windows 10
  - Budoucí verze Windows 10 LTSB a Windows serveru
  - Funkce Asset Intelligence
  - Všechny funkce předběžné verze

### <a name="ltsb-update-options"></a>Možnosti aktualizace LTSB

- Instalaci LTSB můžete převést na instalaci aktuální větve. Převod na aktuální větev se podporuje před nebo po ukončení podpory pro LTSB.

  Pro převod musíte mít aktivní smlouvu Software Assurance s Microsoftem. Další informace najdete v následujících článcích:

  - [Upgrade větve dlouhodobé údržby na aktuální větev](convert-to-current-branch.md)
  - [Licencování a větve pro Configuration Manager](learn-more-editions.md)
  - [Základní a aktualizační verze](../servers/manage/updates.md#bkmk_Baselines)

- Není k dispozici možnost převést LTSB na větev Technical Preview. Větve Technical Preview jsou samostatné instalace, které nevyžadují licenci.

- Zkušební edici aktuální větve nemůžete upgradovat na instalaci LTSB.

## <a name="technical-preview-branch"></a>Větev Technical Preview

Větev Technical Preview je určena pro použití v testovacím prostředí. Seznamte se s nejnovějšími funkcemi, které jsou vyvíjené pro Configuration Manager, a vyzkoušení. Nepodporuje se v produkčním prostředí a nevyžaduje si licenční smlouvu Software Assurance.

Pokud chcete nainstalovat novou lokalitu, která používá větev Technical Preview, použijte nejnovější [základní média pro větev Technical Preview](../get-started/technical-preview.md#bkmk_install). Po instalaci větve Technical Preview budou nové verze k dispozici jako aktualizace v konzole každý měsíc.

### <a name="features-of-the-technical-preview-branch"></a>Funkce větve Technical Preview

- Na základě poslední základní verze aktuální větve
- Obdrží konzolové aktualizace, které aktualizují vaši instalaci na nejnovější verzi verze Technical Preview.
- Obsahuje nové funkce, které jsou vyvíjené a pro které Microsoft požaduje vaše názory.
- Přijímá aktualizace, které se vztahují jenom na větev Technical Preview.

### <a name="technical-preview-limitations"></a>Omezení Technical Preview

- [Podpora je omezená](../get-started/technical-preview.md#bkmk_reqs), včetně jenom jedné primární lokality a až 10 klientů.  
- Nemůžete upgradovat nebo migrovat na aktuální větev nebo instalaci LTSB.
- Nepodporuje následující chování:
  - Použití migrace k importu nebo exportu dat do jiné instalace Configuration Manager
  - Upgrade z předchozí verze Configuration Manager
  - Nainstalovat jako zkušební edici

Funkce, které jsou poprvé představené ve větvi Technical Preview, se v pozdější aktualizaci často přidávají do aktuální větve. Každá nová verze vaší větve Technical Preview zahrnuje funkce z předchozích větví Technical Preview, a to i po přidání těchto funkcí do aktuální větve.

Další informace najdete v tématu [Technical Preview pro Configuration Manager](../get-started/technical-preview.md).

### <a name="technical-preview-update-options"></a>Možnosti aktualizace Technical Preview

- Můžete nainstalovat libovolnou konzolovou aktualizaci pro novou verzi verze Technical Preview.

- Není k dispozici možnost převést větev Technical Preview na aktuální větev nebo LTSB.

## <a name="identify-your-version-and-branch"></a>Určení vaší verze a větve

### <a name="version"></a>Verze

Chcete-li zjistit verzi webu, v konzole nástroje v levém horním rohu konzoly vyhledejte **informace o Configuration Manager** . V tomto dialogovém okně se zobrazí **verze lokality**. Seznam verzí webů najdete v tématu [základní a aktualizační verze](../servers/manage/updates.md#bkmk_Baselines).

### <a name="branch"></a>Větvení.

Chcete-li potvrdit větev webu, v konzole nástroje klikněte na **Správa**  >  **Konfigurace lokality**  >  **lokality**a otevřete **Nastavení hierarchie**. Pokud je k dispozici aktivní možnost převodu na aktuální větev, lokalita spustí verzi LTSB. Když lokalita spustí aktuální větev, konzola tuto možnost zakáže.

Další informace o různých verzích Configuration Manager najdete v tématu [základní a aktualizační verze](../servers/manage/updates.md#bkmk_Baselines).
