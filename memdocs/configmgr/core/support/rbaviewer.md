---
title: Nástroj pro správu na základě rolí
titleSuffix: Configuration Manager
description: Pomocí nástroje pro správu a auditování na základě rolí můžete modelovat a auditovat role a obory zabezpečení v Configuration Manager.
ms.date: 07/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6372ff17-7f56-4d7b-a21b-87fb8bdd6d3a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4cf9d4d3f9d1b2f439d2e87d41cc280e7af0805a
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/10/2020
ms.locfileid: "86239704"
---
# <a name="role-based-administration-and-auditing-tool"></a>Nástroj pro správu a auditování na základě rolí

*Platí pro: Configuration Manager (Current Branch)*

Nástroj pro správu a auditování na základě rolí je jedním z [Configuration Manager nástrojů](tools.md). Tento nástroj použijte pro následující úlohy:

- Modelování rolí zabezpečení s konkrétními oprávněními  

- Audit rozsahů zabezpečení a rolí zabezpečení, které jiní uživatelé mají



## <a name="requirements"></a>Požadavky

- Spusťte ji na stejném počítači jako Configuration Manager Server lokality. 

- Máte správce s **úplnými oprávněními**, **analytik jen pro čtení**nebo role **Správce zabezpečení** .  

- Přiřaďte svůj účet k oboru zabezpečení **vše** a všem kolekcím.  

- (*Volitelné*) K analýze zabezpečení složky sestav musíte mít přístup k SQL.  

- (*Volitelné*) Chcete-li analyzovat podrobné procházení sestav, spusťte tento nástroj na systémovém serveru lokality s rolí bodu hlášení.



## <a name="procedures"></a>Procedury


### <a name="model-permissions-for-a-new-role"></a>Oprávnění modelu pro novou roli

K modelování oprávnění k nové roli, kterou chcete vytvořit, použijte následující postup: 

1. Spusťte **RBAViewer.exe**.  

2. Vyberte základní role zabezpečení, na kterých chcete vytvořit, nebo začněte z prázdné sady oprávnění. Vyberte nezbytná oprávnění.  

3. Kliknutím na **analyzovat** zobrazíte uživatelské rozhraní, které tato vlastní role uvidí.  

    > [!Note]  
    > Pokud chcete zjistit, jestli existuje stávající role zabezpečení, která splňuje vaše požadavky, přepněte na kartu **podobnost** .  

4. Kliknutím na **exportovat** uložte roli jako soubor XML. Pak ho importujte do konzoly Configuration Manager. Další informace najdete v tématu [Vytvoření vlastních rolí zabezpečení](../servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).


### <a name="audit-existing-security-scopes"></a>Auditovat existující obory zabezpečení

Pomocí následujícího postupu můžete auditovat všechny existující administrativní uživatele, kolekce a obory zabezpečení v Configuration Manager:

1. Spusťte **RBAViewer.exe**.  

2. Na panelu nástrojů vyberte tlačítko **audit RBA** .  

    1. Chcete-li zobrazit relace omezené na kolekci ve stromovém zobrazení, přepněte na kartu **Souhrn kolekce** .  

    2. Chcete-li zobrazit objekty přiřazené k roli zabezpečení, přepněte na kartu **Souhrn oboru** .  


### <a name="audit-a-specific-user"></a>Auditovat určitého uživatele

Pomocí následujícího postupu můžete auditovat konfiguraci správy na základě rolí pro konkrétního uživatele:

1. Spusťte **RBAViewer.exe**.  

2. Na panelu nástrojů vyberte tlačítko **Spustit jako** .  

3. Zadejte konkrétní uživatelské jméno a ověřte oprávnění pro tento účet.  

4. Tento nástroj zobrazí role zabezpečení přiřazené uživateli nebo skupině zabezpečení, do které uživatel patří. Zobrazuje také objekty, které může tento uživatel zobrazit, a akce, které mohou provádět v konzole nástroje.  



## <a name="see-also"></a>Viz také

- [Základy správy na základě rolí](../understand/fundamentals-of-role-based-administration.md)
- [Konfigurace správy na základě rolí](../servers/deploy/configure/configure-role-based-administration.md)
