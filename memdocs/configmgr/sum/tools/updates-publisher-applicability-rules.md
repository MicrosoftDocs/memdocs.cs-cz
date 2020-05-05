---
title: Pravidla použitelnosti
titleSuffix: Configuration Manager
description: Spravovat pravidla použitelnosti pro System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 3cf0c2cd-397a-4622-b11c-961f334fb7d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 53a3aabfe65449723bdb6076486128b76a1a830c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078426"
---
# <a name="manage-applicability-rules-in-updates-publisher"></a>Správa pravidel použitelnosti v nástroji Updates Publisher

*Platí pro: System Center Updates Publisher*

S nástrojem Updates Publisher pravidla použitelnosti definují požadavky, které musí být splněny, než může zařízení nainstalovat aktualizaci. Tato pravidla se taky používají k určení, jestli je v počítači nainstalovaná aktualizace. Pravidlo použitelnosti, které je složité s více částmi, se označuje jako sada pravidel.

Sady aktualizací nepoužívají pravidla použitelnosti.

## <a name="overview-of-applicability-rules"></a>Přehled pravidel použitelnosti
Pravidla použitelnosti můžete spravovat z **pracovního prostoru pravidla**. Když vytvoříte pravidlo, zadáváte jednu nebo více podmínek. Pokud je zadáno více podmínek, můžete nakonfigurovat vztahy mezi podmínkami, aby byly vyhodnocovány sekvenčně nebo sdruženy do logických příkazů **and a** **or** .

Například následuje sada pravidel, která obsahuje tři pravidla. První pravidlo ověří, zda soubor. *MyFile* existuje, a druhá a třetí pravidla ověří, zda je jazyk operačního systému Windows buď angličtina, nebo japonština.

``` Example
And  
  File '\[PROGRAM\_FILES\] \\Microsoft\\MyFile' exists  
  Or  
    Windows Language is English
    Windows Language is Japanese
```

Všechny aktualizace vyžadují aspoň jedno pravidlo použitelnosti. Aktualizace, které importujete, již jsou aplikovány na pravidla použitelnosti a když vytváříte vlastní aktualizace, je nutné do nich přidat jedno nebo více pravidel. Můžete upravit a rozšířit pravidla pro jakékoli aktualizace v aplikaci Publisher Updates Publisher.

Pokud chcete zobrazit pravidla, která jste vytvořili, vyberte v **pracovním prostoru pravidla**pravidlo ze seznamu **Moje uložená pravidla** . Jednotlivé podmínky a logické operace pro toto pravidlo se zobrazí v podokně **pravidla použitelnosti** v konzole nástroje. Pravidla pro aktualizace, která importujete, lze zobrazit a upravit pouze při úpravě této aktualizace.

Pravidla můžete vytvořit na dvou místech v aplikaci Updates Publisher:

-   V **pracovním prostoru pravidla** můžete vytvořit a **Uložit** sady pravidel, které pak můžete použít později. Při úpravách nebo vytváření aktualizace můžete jako **Typ pravidla**vybrat **uložené pravidlo** a pak ho vybrat ze seznamu předem vytvořených sad pravidel.

-   V době, kdy můžete aktualizaci vytvořit nebo upravit, můžete také vytvořit nová pravidla. Pravidla, která tímto způsobem vytvoříte, se neukládají pro budoucí použití.

## <a name="create-applicability-rule"></a>Vytvořit pravidlo použitelnosti
Následující informace jsou podobné způsobu, jakým vytváříte pravidla v [Průvodci vytvořením aktualizace](create-updates-with-updates-publisher.md#use-the-create-update-wizard). Ale na rozdíl od průvodce máte možnost Uložit sady pravidel pro budoucí použití.

1. V **pracovním prostoru pravidla**vyberte **vytvořit** . otevře se průvodce **vytvořením pravidla** .

2. Zadejte název pravidla a potom klikněte na ![nové pravidlo.](media/newrule.png) Otevře se stránka s **pravidlem použitelnosti** , kde můžete nakonfigurovat pravidla.

3. Jako **Typ pravidla** vyberte jednu z následujících možností. Možnosti, které je třeba nakonfigurovat, se liší pro každý typ:

   - **Soubor** – toto pravidlo použijte, pokud požadujete, aby zařízení mělo soubor s vlastnostmi, které splňují jedno nebo více kritérií, která zadáte před použitím této aktualizace.

   - **Registr –** Tento typ slouží k zadání podrobností registru, které musí být přítomné předtím, než se zařízení zaregistruje pro instalaci této aktualizace.

   - **Systém –** Toto pravidlo používá systémové podrobnosti k určení použitelnosti. Můžete si vybrat, jestli se má definovat verze Windows, jazyk Windows, architekturu procesoru, nebo zadat dotaz rozhraní WMI k identifikaci operačního systému zařízení.

   - **Instalační služba systému Windows –** Tento typ pravidla použijte k určení použitelnosti na základě nainstalovaného. MSI nebo Instalační služba systému Windows patch (. MSP). Můžete také určit, zda jsou v rámci požadavku nainstalovány konkrétní součásti nebo funkce.

     > [!IMPORTANT]   
     > Ve spravovaném prostředí unices nemůže Agent web Windows Update rozpoznat instalační balíčky Windows, které jsou nainstalované pro jednotlivé uživatele. Když použijete tento typ pravidla, nakonfigurujete další pravidla použitelnosti, například verze souborů nebo hodnoty klíčů registru, aby balíček Instalační služba systému Windows mohl být správně zjištěn bez ohledu na uživatele nebo na systém.

   - **Uložené pravidlo –** Tato možnost umožňuje najít a použít pravidla, která jste předtím nakonfigurovali a uložili.

4. Podle potřeby pokračujte v přidávání a konfigurování dalších pravidel.

5. Pomocí tlačítek logických operací můžete seřadit a seskupit různá pravidla a vytvořit tak složitější kontroly požadovaných součástí.

6. Po dokončení sady pravidel kliknutím na tlačítko **OK** ji uložte. Sada pravidel se nyní zobrazí v seznamu **Moje uložená pravidla** .

## <a name="edit-applicability-rule-sets"></a>Upravit sady pravidel použitelnosti
Chcete-li upravit pravidlo použitelnosti, v **pracovním prostoru pravidla** vyberte libovolné pravidlo, které je uloženo v seznamu **Moje uložená pravidla** , a pak na pásu karet klikněte na tlačítko **Upravit** . Otevře se průvodce **úpravou pravidla** .

Průvodce **úpravou pravidla** zobrazí aktuální pravidla pro sadu pravidel. Pravidla můžete upravovat stejným způsobem jako při vytváření nových pravidel pomocí průvodce **vytvořením pravidla** . Pomocí tohoto průvodce můžete přejmenovat sadu pravidel, odstranit pravidla, znovu uspořádat pravidla a vztahy nebo přidat nová pravidla.

Až provedete změny, kliknutím na **tlačítko OK** uložte změny a zavřete průvodce.

Další informace o používání Průvodce pravidlo najdete v **kroku 7**, na stránce věnované použitelnosti v [Průvodci vytvořením aktualizace](create-updates-with-updates-publisher.md#use-the-create-update-wizard).

## <a name="delete-applicability-rules"></a>Odstranit pravidla použitelnosti
Pokud chcete odstranit uložené pravidlo použitelnosti, v **pracovním prostoru pravidla** vyberte v seznamu **Moje uložená pravidla** pravidlo nebo sadu pravidel a na pásu karet zvolte **Odstranit** . Tím se odstraní uložené pravidlo nebo sada pravidel z nástroje Updates Publisher.

Chcete-li odstranit pravidlo z konkrétní aktualizace, je nutné [aktualizaci upravit](manage-updates-with-updates-publisher.md#edit-updates-and-bundles).
