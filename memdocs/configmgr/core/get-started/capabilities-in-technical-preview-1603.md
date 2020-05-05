---
title: Možnosti ve verzi Technical Preview 1603
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview pro Configuration Manager verze 1603.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5f861b72-9f14-4d17-a512-4a79b660abe6
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 73e3e19df4ce545e4cbb36109da2710e848f1159
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076216"
---
# <a name="capabilities-in-technical-preview-1603-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1603 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1603. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview. Pokud použijete System Center Technical Preview 5, nainstaluje se tato verze jako základní verze Configuration Manager Technical Preview. Před instalací této verze Technical Preview si Projděte úvodní téma, [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md), abyste se seznámili se základními požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.  

 **Známé problémy pro tuto verzi Technical Preview:**  

- Tato verze zahrnuje aktualizace dříve vydaných funkcí, ale nezavádí nové funkce. Pokud jste již dříve upgradovali na 1602 a povolili všechny funkce zahrnuté v 1602, bude stránka funkce v Průvodci aktualizací prázdná.  

- Po aktualizaci serveru lokality na verzi Technical Preview 1603 nebudou klienti moci používat žádné funkce vzdáleného řízení, dokud nebudou aktualizovány také na verzi 1603.  

  **V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  

##  <a name="improvements-to-software-center"></a><a name="BKMK_SC1603"></a>Vylepšení centra softwaru  

### <a name="new-tiled-view-for-apps"></a>Nové zobrazení dlaždic pro aplikace  
 Koncoví uživatelé si teď můžou zvolit mezi seznamem aplikací nebo se zobrazením dlaždic aplikací na kartě **aplikace** v centru softwaru.  

### <a name="select-multiple-updates-in-software-center"></a>Výběr více aktualizací v centru softwaru  
 Na kartě **aktualizace** centra softwaru teď můžete vybrat více aktualizací, nebo vybrat možnost **Aktualizovat vše** a začít instalovat více aktualizací současně.  

##  <a name="improvements-to-remote-control"></a><a name="BKMK_RC1603"></a>Vylepšení vzdáleného řízení  

### <a name="limit-shared-clipboard-access-in-a-remote-control-session"></a>Omezení přístupu ke sdílené schránce v relaci vzdáleného řízení  
 Nyní můžete povolit nové klientské nastavení nástroje Remote Tools **Dotázat se uživatele na oprávnění k přenosu souborů ve sdílené schránce** pro omezení přístupu ke sdílené schránce v relaci vzdáleného řízení.  

 Pokud je tato možnost povolená, musí koncový uživatel, který sdílí vzdálenou relaci, udělit oprávnění prohlížeči této relace předtím, než může prohlížeč přenést soubory z relace do místního počítače přes sdílenou schránku.  

 Tím se pro koncového uživatele přidá vrstva ochrany, jak už dřív bylo uděleno oprávnění k úplnému řízení počítače koncového uživatele, aby bylo možné použít sdílenou schránku k přenosu souborů z relace do místního počítače způsobem, který byl pro koncového uživatele zcela transparentní.  

##  <a name="customize-the-ramdisk-tftp-block-size-and-window-size-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a> Přizpůsobení velikosti bloku a velikosti okna TFTP disku paměti RAM na distribučních bodech s povoleným PXE  
 V 1603 Technical Preview můžete přizpůsobit velikost bloku a velikost okna TFTP disku paměti RAM pro distribuční body s povoleným PXE. Pokud jste svoji síť přizpůsobili, může se stát, že při stahování spouštěcí image dojde k vypršení časového limitu, protože je velikost bloku nebo okna moc velká. Přizpůsobení velikosti bloku a velikosti okna TFTP disku paměti RAM vám umožňuje optimalizovat přenosy dat pomocí protokolu TFTP při použití PXE tak, aby tyto hodnoty odpovídaly konkrétním požadavkům vaší sítě.   
Přizpůsobené nastavení budete muset ve svém prostředí otestovat, abyste zjistili, jaké hodnoty jsou nejvhodnější.  

-   **Velikost bloku TFTP**: Velikost bloku je velikost datových paketů odesílaných serverem do klienta, který stahuje soubor (jak popisuje dokument RFC 2347). Větší velikost bloku umožňuje serveru odesílat menší množství paketů, takže se zkrátí doba odezvy mezi serverem a klientem. Větší bloky ale vedou k fragmentaci paketů, kterou většina klientských implementací PXE nepodporuje.  

-   **Velikost okna TFTP**: Protokol TFTP vyžaduje pro každý odeslaný blok dat paket potvrzení (ACK). Server neodešle další blok v řadě, dokud neobdrží paket ACK k předchozímu bloku. Okna TFTP jsou funkce Služby pro nasazení systému Windows, která umožňuje definovat, kolik datových bloků se vejde do jednoho okna. Server odesílá datové bloky jeden po druhém, dokud není okno zaplněné, a potom klient odešle paket ACK. Zvětšením velikosti tohoto okna se sníží doba prodlevy mezi klientem a serverem a také celková doba potřebná ke stažení spouštěcí image.  

### <a name="try-it-out"></a>Určitě to udělejte!  
 Zkuste provést následující úkoly a pak použijte informace o zpětné vazbě v horní části tohoto tématu a sdělte nám, jak se pracovalo:  

-   Můžu přizpůsobit velikost okna TFTP disku paměti RAM na distribučním bodu s povoleným PXE.  

-   Dá se přizpůsobit velikost bloku TFTP disku RAM v distribučním bodě s povoleným PXE.  

### <a name="to-modify-the-ramdisk-tftp-window-size"></a>Postup úpravy velikosti okna TFTP disku paměti RAM  

- Pokud chcete přizpůsobit velikost okna TFTP disku paměti RAM, přidejte na distribuční body s povoleným PXE následující klíč registru:  

   **Umístění**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  Název: RamDiskTFTPWindowSize  

   **Zadejte**: REG_DWORD  

   **Hodnota**: &lt;přizpůsobená velikost okna\>  

  Výchozí hodnota je 1 (1 datový blok vyplní celé okno).  

### <a name="to-modify-the-ramdisk-tftp-block-size"></a>Postup úpravy velikosti bloku TFTP disku paměti RAM  

- Pokud chcete přizpůsobit velikost okna TFTP disku paměti RAM, přidejte na distribuční body s povoleným PXE následující klíč registru:  

   **Umístění**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  Název: RamDiskTFTPBlockSize  

   **Zadejte**: REG_DWORD  

   **Hodnota**: &lt;velikost přizpůsobeného bloku\>  

  Výchozí hodnota je 4096 (4 tisíce).  
