---
title: Základy správy na základě rolí
titleSuffix: Configuration Manager
description: Správa na základě rolí slouží k řízení přístupu pro správu k Configuration Managerům a objektům, které spravujete.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0a2d6c3f-a4e4-4c19-b087-3caada480de9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 62faf2fd736f9751e8b33e821cb814f527a1197c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722855"
---
# <a name="fundamentals-of-role-based-administration-for-configuration-manager"></a>Základy správy na základě rolí pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

V Configuration Manager používáte správu na základě rolí k zabezpečení přístupu, který je potřeba pro správu Configuration Manager. Také zabezpečený přístup k objektům, které spravujete, jako jsou kolekce, nasazení a lokality. Až porozumíte konceptům představeným v tomto článku, můžete [nakonfigurovat správu na základě rolí pro Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

 Model správy na základě rolí centrálně definuje a spravuje nastavení zabezpečení přístupu ke všem lokalitám a nastavením lokalit v celé hierarchii pomocí následujících položek:  

- *Role zabezpečení* jsou přiřazeny správcům, kteří poskytují uživatelům (nebo skupinám uživatelů) oprávnění k různým objektům Configuration Manager. Například oprávnění k vytvoření nebo změně nastavení klienta.  

- *Obory zabezpečení* slouží k seskupení konkrétních instancí objektů, které správce zodpovídá za správu, jako je například aplikace, která instaluje systém Microsoft Office 2010.  

- *Kolekce* se používají k určení skupin prostředků uživatelů a zařízení, které může administrativní uživatel spravovat.  

  U kombinace rolí zabezpečení, oborů zabezpečení a kolekcí můžete oddělit přiřazení pro správu, která splňují požadavky vaší organizace. Společně definují rozsah správy uživatele, což je to, co tento uživatel může zobrazit a spravovat ve vašem nasazení Configuration Manager.  

## <a name="benefits-of-role-based-administration"></a>Výhody správy na základě rolí  

- Lokality se nepoužívají jako hranice správy.  
- Můžete vytvořit administrativní uživatele pro hierarchii a k nim stačí přiřazovat zabezpečení jenom jednou.  
- Všechna přiřazení zabezpečení se replikují a jsou k dispozici v celé hierarchii.  
- K dispozici jsou předdefinované role zabezpečení, které slouží k přiřazení typických úloh správy. Vytvořte vlastní role zabezpečení pro podporu specifických podnikových požadavků.  
- Uživatelé s právy pro správu uvidí jenom objekty, ke kterým mají oprávnění ke správě.  
- Můžete auditovat akce zabezpečení správy.  

Když navrhujete a implementujete zabezpečení správy pro Configuration Manager, k vytvoření *oboru správy* pro administrativního uživatele použijte následující:  

- [Role zabezpečení](#bkmk_Planroles)  

- [Kolekce](#bkmk_planCol)  

- [Obory zabezpečení](#bkmk_PlanScope)  

 Obor správy řídí objekty, které uživatel s právy pro správu zobrazuje v konzole Configuration Manager, a řídí oprávnění, která má uživatel na těchto objektech. Konfigurace správy na základě rolí se replikují do každé lokality v hierarchii jako globální data a následně se použijí pro všechna připojení správy.  

> [!IMPORTANT]  
> V důsledku zpoždění replikací mezi lokalitami nemusí být lokalita schopna přijímat změny pro správu na základě rolí. Informace o tom, jak monitorovat replikaci databáze mezi lokalitami, najdete v tématu [přenos dat mezi lokalitami](../plan-design/hierarchy/data-transfers-between-sites.md) .  

##  <a name="security-roles"></a><a name="bkmk_Planroles"></a>Role zabezpečení

 Pomocí rolí zabezpečení se správcům udělují oprávnění zabezpečení. Role zabezpečení jsou skupiny oprávnění zabezpečení, která přiřazujete správcům, aby mohli provádět úlohy správy. Tato oprávnění zabezpečení definují akce správy, jež mohou správci provádět, a oprávnění, která jsou udělena pro určité typy objektů. Nejlepší postup z hlediska zabezpečení je přiřazovat role zabezpečení poskytující co nejnižší oprávnění.  

 Configuration Manager má několik předdefinovaných rolí zabezpečení, které podporují typické seskupení úloh správy, a můžete vytvořit vlastní role zabezpečení pro podporu specifických podnikových požadavků. Příklady předdefinovaných rolí zabezpečení:  

- *Úplný správce* udělí všechna oprávnění v Configuration Manager.  

- *Správce prostředků* uděluje oprávnění ke správě funkce Asset Intelligence bodu synchronizace, funkce Asset Intelligence tříd vytváření sestav, inventáře softwaru, inventáře hardwaru a pravidel měření.  

- *Správce aktualizací softwaru* uděluje oprávnění definovat a nasazovat aktualizace softwaru. Administrativní uživatelé, kteří jsou přidruženi k této roli, mohou vytvářet kolekce, skupiny aktualizací softwaru, nasazení a šablony.  

- *Správce zabezpečení* uděluje oprávnění k přidávání a odebírání správců a k přidružení administrativních uživatelů k rolím zabezpečení, kolekcím a oborům zabezpečení. Administrativní uživatelé, kteří jsou přidruženi k této roli, mohou také vytvářet, upravovat a odstraňovat role zabezpečení a jejich přiřazené obory a kolekce zabezpečení.

> [!TIP]  
> V konzole Configuration Manager můžete zobrazit seznam předdefinovaných rolí zabezpečení a vlastních rolí zabezpečení, které vytvoříte, včetně jejich popisu. Chcete-li zobrazit role, v pracovním prostoru **Správa** rozbalte položku **zabezpečení**a pak vyberte možnost **role zabezpečení**.  

 Každá role zabezpečení má určitá oprávnění pro různé typy objektů. Například role zabezpečení *vytváření aplikací* má následující oprávnění pro aplikace: schválit, vytvořit, odstranit, upravit, upravit složku, přesunout objekt, číst, spustit sestavu a nastavit obor zabezpečení.

 Oprávnění pro předdefinované role zabezpečení nemůžete změnit, ale můžete roli zkopírovat, provést změny a pak tyto změny uložit jako novou vlastní roli zabezpečení. Můžete také importovat role zabezpečení, které jste exportovali z jiné hierarchie, například z testovací sítě. Zkontrolujte role zabezpečení a jejich oprávnění, abyste zjistili, jestli budete používat předdefinované role zabezpečení, nebo jestli musíte vytvořit vlastní role zabezpečení.  

### <a name="to-help-you-plan-for-security-roles"></a>Vám může při plánování rolí zabezpečení.  

1. Identifikujte úkoly, které administrativní uživatelé provádějí v Configuration Manager. Tyto úlohy se mohou týkat jedné nebo více skupin úloh správy, například nasazování aplikací a balíčků, nasazování operačních systémů a nastavení pro dodržování předpisů, konfigurace lokalit a zabezpečení, auditování, vzdáleného řízení počítačů a shromažďování dat z inventářů.  

2. Namapujte tyto úlohy správy k jedné či několika předdefinovaným rolím zabezpečení.  

3. Pokud některý z správců provádí úlohy více rolí zabezpečení, přiřaďte těmto správcům více rolí zabezpečení, místo aby se vytvořila nová role zabezpečení, která kombinuje úlohy.  

4. Pokud úkoly, které jste identifikovali, nejsou namapovány na předdefinované role zabezpečení, vytvořte a otestujte nové role zabezpečení.  

Informace o tom, jak vytvořit a nakonfigurovat role zabezpečení pro správu na základě rolí, najdete v tématu [Vytvoření vlastních rolí zabezpečení](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole) a [Konfigurace rolí zabezpečení](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole) v článku [Konfigurace správy na základě rolí pro Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md) .  

##  <a name="collections"></a><a name="bkmk_planCol"></a>Sbírk

 Kolekce určují, jaké prostředky uživatele a počítače může správce prohlížet nebo spravovat. Aby mohli správci například nasadit aplikace nebo spustit vzdálené řízení, musí být přiřazeni k roli zabezpečení, která uděluje přístup ke kolekci obsahující tyto prostředky. Lze vybrat kolekce uživatelů nebo zařízení.  

 Další informace o kolekcích najdete v tématu [Úvod do kolekcí](../../core/clients/manage/collections/introduction-to-collections.md).  

 Před konfigurací správy na základě rolí zkontrolujte, zda je nutné vytvářet nové kolekce z některého z následujících důvodů:  

- Funkční uspořádání. Například samostatné kolekce serverů a pracovních stanic.  
- Zeměpisná poloha. Například samostatné kolekce pro Severní Ameriku a Evropu.  
- Požadavky na zabezpečení a podnikové procesy. Například samostatné kolekce pro produkční a testovací počítače.  
- Organizační uspořádání. Například samostatné kolekce pro jednotlivé obchodní jednotky.  

Informace o tom, jak nakonfigurovat kolekce pro správu na základě rolí, najdete v tématu [konfigurace kolekcí pro správu zabezpečení](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl) v článku [Konfigurace správy na základě rolí pro Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md) .  

## <a name="security-scopes"></a><a name="bkmk_PlanScope"></a>Obory zabezpečení

 Pomocí oborů zabezpečení lze správcům zajistit přístup k zabezpečitelným objektům. Obor zabezpečení je pojmenovaná sada zabezpečitelné objekty, které jsou přiřazeny uživatelům správce jako skupina. Všechny zabezpečitelné objekty je potřeba přiřadit aspoň k jednomu oboru zabezpečení. Configuration Manager má dva předdefinované obory zabezpečení:  

- *Veškerý* integrovaný obor zabezpečení uděluje přístup ke všem oborům. K tomuto oboru zabezpečení nelze přiřazovat objekty.  

- *Výchozí* předdefinovaný obor zabezpečení se ve výchozím nastavení používá pro všechny objekty. Při první instalaci Configuration Manager jsou všechny objekty přiřazeny k tomuto oboru zabezpečení.  

Chcete-li omezit objekty, které smí správci zobrazit a spravovat, je nutné vytvořit a používat vlastní obory zabezpečení. Obory zabezpečení nepodporují hierarchickou strukturu a nelze je vnořovat. Obory zabezpečení mohou obsahovat jeden nebo více typů objektů, které obsahují následující položky:  

- Odběry upozornění  
- Aplikace  
- Spouštěcí image  
- Skupiny hranic  
- Položky konfigurace  
- Vlastní nastavení klienta  
- Distribuční body a skupiny distribučních bodů  
- Balíčky ovladačů
- Složky (počínaje verzí 1906) <!--3600867-->
- Globální podmínky  
- Úlohy migrace
- Bitové kopie operačního systému
- Instalační balíčky operačního systému  
- Balíčky  
- Dotazy  
- Lokality  
- Pravidla distribuce softwaru  
- Skupiny aktualizací softwaru  
- Balíčky aktualizací softwaru  
- Balíčky pořadí úloh  
- Položky a balíčky nastavení zařízení se systémem Windows CE  

Existují také objekty, které nelze zahrnout do oborů zabezpečení, protože jsou zabezpečeny pouze pomocí rolí zabezpečení. Přístup pro správu těchto objektů nelze omezit na podmnožinu dostupných objektů. Můžete mít například správce, který vytvoří skupiny hranic, jež budou použity pro určitou lokalitu. Vzhledem k tomu, že objekt hranice nepodporuje obory zabezpečení, nelze tomuto uživateli přiřadit obor zabezpečení, který poskytuje přístup pouze k hranicím, které mohou být přidruženy k této lokalitě. Vzhledem k tomu, že objekt hranice nelze přidružit k oboru zabezpečení, při přiřazení role zabezpečení, která zahrnuje přístup k objektům hranice uživateli, může tento uživatel přistupovat ke každé hranici v hierarchii.  

Objekty, které nejsou omezeny obory zabezpečení, zahrnují následující položky:  

- Doménové struktury služby Active Directory  
- Administrativní uživatelé  
- Výstrahy  
- Antimalwarové zásady  
- Hranice  
- Přidružení počítačů  
- Výchozí nastavení klienta  
- Šablony nasazení  
- Ovladače zařízení  
- konektor systému Exchange Server  
- Mapování migrace z pracoviště na pracoviště  
- Profily zápisu mobilních zařízení  
- Role zabezpečení  
- Obory zabezpečení  
- Adresy lokalit  
- Role systému lokality  
- Názvy softwaru  
- Aktualizace softwaru  
- Stavové zprávy  
- Spřažení uživatelských zařízení  

Obory zabezpečení vytvořte v případě, že je zapotřebí omezit přístup k samostatným instancím objektů. Příklad:  

- Máte skupinu správců, kteří musejí být schopni zobrazit výrobní aplikace a nikoliv testovací aplikace. Vytvořte jeden obor zabezpečení pro výrobní aplikace a druhý pro testovací aplikace.  

- Různí správci vyžadují různý přístup k některým instancím typu objektu. Například jedna skupina správců vyžaduje k určitým skupinám aktualizací softwaru oprávnění Číst a jiná skupina správců vyžaduje pro jiné skupiny aktualizací softwaru oprávnění Upravit a Odstranit . Vytvořte pro tyto skupiny aktualizací softwaru různé obory zabezpečení.  

Informace o tom, jak nakonfigurovat obory zabezpečení pro správu na základě rolí, najdete v článku [Konfigurace oborů zabezpečení pro objekt](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope) v článku [Konfigurace správy na základě rolí pro Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md) .  

## <a name="next-steps"></a>Další kroky

[Konfigurace správy na základě rolí pro Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
