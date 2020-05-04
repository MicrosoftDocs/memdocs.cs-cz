---
title: Vytvoření média pořadí úkolů
titleSuffix: Configuration Manager
description: Vytvořte médium pořadí úloh k nasazení operačního systému do cílového počítače v prostředí Configuration Manager.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 87d5df6edee2adba32f1a49b8e867e930386b4df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711025"
---
# <a name="create-task-sequence-media"></a>Vytvoření média pořadí úkolů

*Platí pro: Configuration Manager (Current Branch)*

Médium můžete použít k zachycení image operačního systému z referenčního počítače nebo k nasazení operačního systému do cílového počítače v prostředí Configuration Manager. Vytvořené médium může být disk CD, sada disků DVD nebo jednotka USB Flash.  

K nasazování operačních systémů do cílových počítačů, které nemají připojení k síti nebo mají připojení s malou šířkou pásma pro Configuration Manager web, se používá většinou médium. Médium ale můžete použít také ke spuštění nasazení operačního systému mimo existující operační systém Windows. Tato metoda je užitečná v případě, že neexistuje žádný operační systém, operační systém nefunguje nebo chcete změnit rozdělení pevného disku na oddíly.  

Rozlišujeme následující typy médií pro nasazení: spouštěcí médium, samostatné médium a předzpracované médium. Obsah média se liší v závislosti na typu používaného média. Například samostatné médium obsahuje pořadí úkolů, které nasazuje operační systém. Jiné typy médií načítají pořadí úloh z bodu správy.  

> [!IMPORTANT]  
> Chcete-li vytvořit médium pořadí úkolů, musíte být správcem počítače, ve kterém spouštíte konzolu Configuration Manager. Pokud nejste správcem, budete při spuštění Průvodce vytvořením média pořadí úloh vyzváni k zadání přihlašovacích údajů správce.  


## <a name="capture-media"></a><a name="BKMK_PlanCaptureMedia"></a>Záznamová média

Záznamová média umožňují zaznamenat image operačního systému z referenčního počítače. Záznamové médium obsahuje spouštěcí bitovou kopii, která spouští referenční počítač, a pořadí úkolů, které zachytí image operačního systému.

Další informace o tom, jak vytvářet záznamová média, najdete v tématu [Vytvoření záznamového média](create-capture-media.md).  


## <a name="bootable-media"></a><a name="BKMK_PlanBootableMedia"></a>Spouštěcí médium

Spouštěcí médium obsahuje následující součásti:

- Spouštěcí bitová kopie
- Volitelné [příkazy před zahájením](../understand/prestart-commands-for-task-sequence-media.md) a jejich požadované soubory
- Configuration Manager binárních souborů

Když se cílový počítač spustí, připojí se k síti a načte pořadí úloh, bitovou kopii operačního systému a veškerý další požadovaný obsah ze sítě. Vzhledem k tomu, že pořadí úkolů není na médiu, můžete změnit pořadí úloh nebo obsah, aniž byste museli znovu vytvořit médium.  

> [!IMPORTANT]  
> Balíčky na spouštěcím médiu nejsou šifrovány. Vezměte v úvahu vhodná bezpečnostní opatření, jako je například přidání hesla k médiu, aby se zajistilo, že obsah balíčku bude zabezpečen od neautorizovaných uživatelů.  

Další informace o tom, jak vytvořit spouštěcí médium, najdete v tématu [Vytvoření spouštěcího média](create-bootable-media.md).  


## <a name="prestaged-media"></a><a name="BKMK_PlanPrestagedMedia"></a>Předzpracované médium

Předzpracované médium umožňuje použít spouštěcí médium a bitovou kopii operačního systému na pevný disk před procesem zřizování. Předzpracované médium je soubor bitové kopie systému Windows (WIM). Dá se nainstalovat na holé počítač od výrobce nebo v přípravném centru, které není připojené k produkčnímu Configuration Manager prostředí.  

Předzpracované médium obsahuje spouštěcí bitovou kopii, která se používá ke spuštění cílového počítače a image operačního systému, která se použije pro cílový počítač. Můžete taky v rámci předzpracovaného média určit aplikace, balíčky a ovladače, které mají být součástí. Pořadí úkolů, které nasazuje operační systém, není součástí média. Když nasadíte pořadí úloh používající Předzpracované médium, klient nejprve zkontroluje platný obsah v místní mezipaměti pořadí úloh. Pokud obsah nebyl nalezen nebo byl revidován, klient stáhne obsah z distribučního bodu nebo partnera.  

Předzpracované médium se přenese na pevný disk nového počítače před jeho odesláním koncovému uživateli. Když se počítač poprvé spustí po použití předzpracovaného média, počítač se spustí v systému Windows PE. Připojí se k bodu správy a vyhledá pořadí úkolů, které dokončí proces nasazení operačního systému.  

> [!IMPORTANT]  
> Balíčky na předzpracovaném médiu nejsou šifrovány. Vezměte v úvahu vhodná bezpečnostní opatření, jako je například přidání hesla k médiu, aby se zajistilo, že obsah balíčku bude zabezpečen od neautorizovaných uživatelů.  

Další informace o tom, jak vytvořit předzpracovaná média, najdete v tématu [Vytvoření předzpracovaného média](create-prestaged-media.md).  


## <a name="stand-alone-media"></a><a name="BKMK_PlanStandaloneMedia"></a>Samostatné médium

Samostatné médium obsahuje všechno, co je potřeba k nasazení operačního systému. Tento obsah zahrnuje pořadí úkolů a jakýkoli další požadovaný obsah. Vzhledem k tomu, že všechno, co je potřeba k nasazení operačního systému, je uložené na samostatném médiu, je místo na disku požadované pro samostatné médium větší než u jiných typů médií.  

Další informace o vytvoření samostatného média naleznete v tématu Create a samostatná [média](create-stand-alone-media.md).  


## <a name="considerations-when-using-https"></a>Předpoklady při používání protokolu HTTPS

Když nakonfigurujete body správy a distribuční body na používání protokolu HTTPS, vytvořte spouštěcí médium a předzpracovaná média v primární lokalitě, nikoli v lokalitě centrální správy. Také Vezměte v úvahu následující body, které vám pomůžou určit, jestli se má médium nakonfigurovat jako dynamické nebo založené na webu:  

- Chcete-li konfigurovat médium jako dynamické médium, všechny primární lokality musí mít kořenovou certifikační autoritu (CA) lokality, ze které jste médium vytvořili. Kořenovou certifikační autoritu můžete importovat do všech primárních lokalit v hierarchii.  

- Když primární lokality v hierarchii Configuration Manager používají jiné kořenové certifikační autority, musíte v každé lokalitě použít médium založené na lokalitě.  
