---
title: Zabezpečení a ochrana osobních údajů pro nastavení dodržování předpisů
titleSuffix: Configuration Manager
description: Seznamte se s osvědčenými postupy zabezpečení pro nastavení dodržování předpisů v Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1c409244-6778-4970-a99c-d2508c9cf62b
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 5021a88966c6c57a3b49a907e14bbe06e28286ff
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240637"
---
# <a name="security-and-privacy-for-compliance-settings-in-configuration-manager"></a>Zabezpečení a ochrana osobních údajů pro nastavení dodržování předpisů v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*


## <a name="security-best-practices-for-compliance-settings"></a>Osvědčené postupy zabezpečení pro nastavení dodržování předpisů  

|Doporučené zabezpečení|Další informace|  
|----------------------------|----------------------|  
|Nemonitorujte citlivá data.|Pokud chcete zamezit úniku citlivých informací, nekonfigurujte položky konfigurace pro monitorování potenciálně citlivých informací.|  
|Nekonfigurujte pravidla dodržování předpisů, která využívají data, jež by mohla být upravena koncovými uživateli.|Pokud vytvoříte pravidla dodržování předpisů na základě dat, která mohou uživatelé změnit, jako je například nastavení konfigurace v registru, výsledky kontroly dodržování předpisů nebudou spolehlivé.|  
|Importujte balíčky konfigurace Microsoft System Center a další konfigurační data z externích zdrojů jenom v případě, že mají platný digitální podpis od důvěryhodného vydavatele.|Publikovaná konfigurační data je možné digitálně podepsat, abyste mohli ověřit zdroj publikování a ujistit se, že s daty nikdo nemanipuloval. Když ověření pomocí digitálního podpisu selže, zobrazí se varování a dotaz, jestli chcete pokračovat v importu. Když nemůžete ověřit zdroj a integritu dat, neimportujte nepodepsaná data.|  
|Implementujte řízení přístupu, čímž ochráníte referenčního počítače.|Ujistěte se, že pokud administrativní uživatel konfiguruje registr nebo nastavení systému souborů tím, že najde referenční počítač procházením, nebyl referenční počítač ohrožen.|  
|Při procházení k referenčnímu počítači zabezpečte komunikační kanál.|Chcete-li zabránit manipulaci s daty při jejich přenosu po síti, použijte protokol Internet Protocol Security (IPsec) nebo SMB (Server Message Block) mezi počítačem, který spouští konzolu Configuration Manager a referenčním počítačem.|  
|Omezte a monitorujte administrativní uživatele, kterým je udělená role zabezpečení Správce nastavení dodržování předpisů.|Administrativní uživatelé, kteří mají roli **Správce nastavení dodržování předpisů** můžou nasadit položky konfigurace do všech zařízení a pro všechny uživatele v hierarchii. Položky konfigurace můžou být velmi silné a umožňují například spouštění skriptů nebo úpravy registru.|  

## <a name="privacy-information-for-compliance-settings"></a>Ochrana osobních údajů pro nastavení dodržování předpisů  
 Nastavení dodržování předpisů slouží k vyhodnocení, jestli jsou kompatibilní s položky konfigurace, které nasadíte ve standardních hodnotách konfigurace klientských zařízení. Některá nastavení se mohou automaticky opravit, když nejsou v souladu. Informace o dodržování předpisů se z bodu správy odešlou na server lokality a uloží se do databáze lokality. Data jsou zašifrována, když je zařízení zasílají do místa správy, ale v databázi lokality nejsou uložena v zašifrovaném formátu. Informace jsou uchovány v databázi, dokud je úloha správy lokality **Odstranit starší data správy konfigurací** neodstraní po každých 90 dnech. Můžete provést konfiguraci intervalu odstranění. Informace o shodě nejsou zaslány do společnosti Microsoft.  

 Ve výchozím nastavení zařízení nevyhodnocují nastavení dodržování předpisů. Kromě toho musíte konfigurovat položky konfigurace a standardní hodnoty konfigurace a nasadit je do zařízení.  
