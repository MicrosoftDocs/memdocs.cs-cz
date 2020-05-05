---
title: Content Library Cleanup Tool
titleSuffix: Configuration Manager
description: Pomocí nástroje pro vyčištění knihovny obsahu můžete odebrat osamocený obsah, který už není přidružený k nasazení Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b1b415d5c24800f003f730426216ac7cf190a4f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720216"
---
# <a name="content-library-cleanup-tool"></a>Content Library Cleanup Tool

*Platí pro: Configuration Manager (Current Branch)*

Pomocí nástroje příkazového řádku pro vyčištění knihovny obsahu můžete odebrat obsah, který už není přidružený k žádnému balíčku nebo aplikaci v distribučním bodě. Tento typ obsahu se nazývá *osamocený obsah*. Tento nástroj nahrazuje starší verze podobných nástrojů vydaných pro dřívější Configuration Manager produkty.  

Nástroj má vliv pouze na obsah v distribučním bodu, který zadáte při spuštění nástroje. Nástroj nemůže odebrat obsah z knihovny obsahu na serveru lokality.

Vyhledejte **ContentLibraryCleanup. exe** `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` na serveru lokality.



## <a name="requirements"></a>Požadavky  

- Spouštějte nástroj pouze proti jednomu distribučnímu bodu v jednom okamžiku.  

- Spusťte ji přímo v počítači, který je hostitelem distribučního bodu, nebo vzdáleně z jiného počítače.  

- Uživatelský účet, který spouští nástroj, musí mít oprávnění stejné jako role zabezpečení **správce s úplnými** oprávněními v Configuration Manager.  



## <a name="modes-of-operation"></a>Režimy činností

Spusťte nástroj v následujících dvou režimech: [co-if](#what-if-mode) a [Delete](#delete-mode).

> [!Tip]  
> Začněte s režimem *citlivostní* operace. Až budete s výsledky spokojeni, spusťte nástroj v režimu *odstranění* .  


### <a name="what-if-mode"></a>Režim citlivosti   

Pokud `/delete` parametr nezadáte, nástroj se spustí v režimu s akcemi. Tento režim identifikuje obsah, který by se odstranil z distribučního bodu.

- Při spuštění v tomto režimu Nástroj neodstraní žádná data.  

- Nástroj zapisuje do souboru protokolu informace o obsahu, který by odstranil. Nebudete vyzváni k potvrzení všech potenciálních odstranění.  


### <a name="delete-mode"></a>Režim odstranění   

Když nástroj spustíte s `/delete` parametrem, nástroj se spustí v režimu odstranění.

- Při spuštění v tomto režimu lze odstranit osamocený obsah, který vyhledá v zadaném distribučním bodě, z knihovny obsahu distribučního bodu.  

- Před odstraněním každého souboru potvrďte, že ho má nástroj odstranit. Pokud chcete přeskočit další výzvy a odstranit veškerý osamocený obsah, vyberte **Y** pro Ano, **N** pro ne nebo **Ano všem** .  


### <a name="log-file"></a>Soubor protokolu

Když je nástroj spuštěn v obou režimech, automaticky vytvoří protokol. Pojmenuje soubor protokolu s následujícími informacemi: 
- Režim, ve kterém se nástroj spouští  
- Název distribučního bodu  
- Datum a čas operace  

Po dokončení nástroje se automaticky otevře soubor protokolu v systému Windows. 

Nástroj ve výchozím nastavení zapíše soubor protokolu do dočasné složky uživatelského účtu, který nástroj spouští. Toto umístění je v počítači, na kterém jste spustili nástroj, který není vždy cílem nástroje. Použijte `/log` parametr pro přesměrování souboru protokolu do jiného umístění, včetně síťové sdílené složky.



## <a name="run-the-tool"></a>Spusťte nástroj.

Spuštění nástroje: 

1. Otevřete příkazový řádek jako správce. Změňte adresář na složku, která obsahuje **ContentLibraryCleanup. exe**.  

2. Zadejte příkazový řádek, který obsahuje požadované [parametry příkazového řádku](#bkmk_params)a všechny volitelné parametry, které chcete použít.



## <a name="command-line-parameters"></a><a name="bkmk_params"></a>Parametry příkazového řádku  

Tyto parametry příkazového řádku použijte v libovolném pořadí.   

### <a name="required-parameters"></a>Požadované parametry

|Parametr|Podrobnosti|
|---------|-------|
| `/dp <distribution point FQDN>`  | Zadejte plně kvalifikovaný název domény (FQDN) distribučního bodu, který se má vyčistit. |
| `/ps <primary site FQDN>` | *Vyžadováno* pouze při čištění obsahu z distribučního bodu v sekundární lokalitě. Nástroj se připojí k nadřazené primární lokalitě a spustí dotazy pro poskytovatele služby SMS. Tyto dotazy umožňují nástroji určit, jaký obsah by měl být na distribučním bodu. Pak může identifikovat osamocený obsah, který se má odebrat. Toto připojení k nadřazené primární lokalitě musí být vytvořeno pro distribuční body v sekundární lokalitě, protože požadované podrobnosti nejsou k dispozici přímo ze sekundární lokality.|
| `/sc <primary site code>`  | *Vyžadováno* pouze při čištění obsahu z distribučního bodu v sekundární lokalitě. Zadejte kód lokality nadřazené primární lokality. |

#### <a name="example-scan-and-log-what-content-it-would-delete-what-if"></a>Příklad: prohledávání a protokolování obsahu, který by odstranil (co-if)
`ContentLibraryCleanup.exe /dp server1.contoso.com`

#### <a name="example-scan-and-log-content-for-a-dp-at-a-secondary-site"></a>Příklad: prohledávání a protokolování obsahu pro DP v sekundární lokalitě
`ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com /sc ABC` 


### <a name="optional-parameters"></a>Volitelné parametry

|Parametr|Podrobnosti|
|---------|-------|
|`/delete`| Tento parametr použijte, pokud jste připraveni odstranit obsah z distribučního bodu. Před odstraněním obsahu se zobrazí výzva. </br></br> Pokud tento parametr nepoužijete, Nástroj zaznamená výsledky, které obsah odstraní. Bez tohoto parametru se ve skutečnosti neodstraní žádný obsah z distribučního bodu. |
| `/q` | Tento parametr spustí nástroj v tichém režimu, který potlačí všechny výzvy. Tyto výzvy budou zahrnovat při odstraňování obsahu. Také automaticky neotevře soubor protokolu. |
| `/ps <primary site FQDN>` | Volitelné pouze při čištění obsahu z distribučního bodu v primární lokalitě. Zadejte plně kvalifikovaný název domény primární lokality, do které distribuční bod patří. |
| `/sc <primary site code>` | Volitelné pouze při čištění obsahu z distribučního bodu v primární lokalitě. Zadejte kód lokality primární lokality, do které distribuční bod patří. |
| `/log <log file directory>` | Zadejte umístění, do kterého nástroj zapisuje soubor protokolu. Toto umístění může být místní jednotka nebo sdílená síťová složka.</br></br> Pokud tento parametr nepoužijete, nástroj umístí soubor protokolu do dočasného adresáře uživatele v počítači, na kterém je nástroj spuštěný.|

#### <a name="example-delete-content"></a>Příklad: odstranění obsahu 
`ContentLibraryCleanup.exe /dp server1.contoso.com /delete`

#### <a name="example-delete-content-without-prompts"></a>Příklad: odstranění obsahu bez výzvy
`ContentLibraryCleanup.exe /q /dp server1.contoso.com /delete` 

#### <a name="example-log-to-local-drive"></a>Příklad: přihlášení na místní disk
`ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop` 

#### <a name="example-log-to-network-share"></a>Příklad: log do síťové sdílené složky
`ContentLibraryCleanup.exe /dp server1.contoso.com /log \\server\share`


### <a name="known-issue"></a>Známý problém

Pokud se nějaký balíček nebo nasazení nezdařil nebo probíhá, může nástroj vrátit následující chybu:`System.InvalidOperationException: This content library cannot be cleaned up right now because package <packageID> is not fully installed.`

Pro tento problém neexistuje žádné alternativní řešení. Nástroj nemůže spolehlivě identifikovat osamocené soubory, když probíhá zpracování obsahu nebo se jeho nasazení nepovedlo. Nástroj nebude umožňovat vyčištění obsahu, dokud tento problém nevyřešíte.
