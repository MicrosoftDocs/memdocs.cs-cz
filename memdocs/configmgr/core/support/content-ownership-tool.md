---
title: Nástroj pro vlastnictví obsahu
titleSuffix: Configuration Manager
description: Vlastnictví osamocených balíčků v Configuration Manager můžete změnit pomocí nástroje pro vlastnictví obsahu.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 753d2681-ea72-4f47-94d1-ac10188d9d5b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee1a24a93bb71178af3a4cfbba2a406bdd958d19
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723387"
---
# <a name="content-ownership-tool"></a>Nástroj pro vlastnictví obsahu

*Platí pro: Configuration Manager (Current Branch)*

Nástroj pro vlastnictví obsahu je jedním z [nástrojů Configuration Manager](tools.md). Změní vlastnictví osamocených balíčků v Configuration Manager. Osamocené balíčky nemají vlastnící server lokality. Balíčky můžou být osamocené odebráním serveru lokality, zatímco pořád vlastní tento server lokality.

Nástroj pro vlastnictví obsahu spusťte na jakémkoli webovém serveru v hierarchii Configuration Manager. Přihlaste se jako uživatel s právy pro správu s dostatečnými oprávněními k balíčku.  

> [!Tip]  
> Pomocí **ContentLibraryCleanup. exe** v `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` můžete *Odebrat* osamocený obsah z distribučního bodu. Další informace najdete v tématu [Nástroj pro vyčištění knihovny obsahu](../plan-design/hierarchy/content-library-cleanup-tool.md).  



## <a name="features"></a>Funkce

- Zobrazit všechny osamocené balíčky  

- Zobrazit všechny balíčky, i když nejsou osamocené  

- Zobrazení stavu připojení k lokalitě  

- Filtrovat balíčky podle názvu, kódu webu nebo typu balíčku  

- Seřadit podle libovolného zobrazeného sloupce  

- Změna přiřazení jednoho nebo více balíčků s jednou akcí  

- Zobrazit průběh aktivity převodu vlastnictví  



## <a name="usage"></a>Využití

Spusťte nástroj **ContentOwnershipTool. exe** a spusťte nástroj. Oprávnění místního správce na počítači není nutné ke spuštění tohoto nástroje.

Neexistují žádné parametry příkazového řádku.

> [!Important]   
> Tento nástroj změní vlastnictví osamoceného balíčku. Samotný balíček se nepřesouvá z distribučního bodu, ve kterém je uložený. Tato změna vlastnictví nezpůsobí aktualizaci balíčku v distribučních bodech. Také nezpůsobí, aby klienti znovu vyhodnotili zásady pro nasazení balíčku. Po změně vlastnictví se ujistěte, že nový server lokality má přístup ke zdrojovým souborům. Musí mít alespoň oprávnění **ke čtení** pro zdrojové soubory každého balíčku. 



## <a name="see-also"></a>Viz také

- [Základní koncepty správy obsahu](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [Knihovna obsahu](../plan-design/hierarchy/the-content-library.md)
