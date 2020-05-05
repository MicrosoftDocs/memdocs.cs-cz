---
title: Správa aktualizací Windows 10 Express
titleSuffix: Configuration Manager
description: Configuration Manager podporuje soubory Expresní instalace pro Windows 10, které poskytují menší soubory ke stažení a rychlejší instalaci u klientů.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/02/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.openlocfilehash: 4093eafe9f8a337ce322165a529f630a759b365f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718641"
---
# <a name="manage-express-installation-files-for-windows-10-updates"></a>Správa souborů Expresní instalace pro aktualizace Windows 10

Configuration Manager podporuje soubory Expresní instalace pro aktualizace Windows 10. Nakonfigurujte klienta tak, aby stahoval jenom změny v rámci kumulativní aktualizace kvality Windows 10 s Windows 10 a aktualizace z předchozího měsíce. Bez souborů Expresní instalace si Configuration Manager klienti stáhnou každý měsíc úplnou kumulativní aktualizaci Windows 10, včetně všech aktualizací z předchozích měsíců. Použití souborů Expresní instalace poskytuje menší soubory ke stažení a rychlejší instalaci u klientů.

Informace o tom, jak používat Configuration Manager ke správě obsahu aktualizace pro aktuálnost s Windows 10, najdete v tématu [optimalizace doručování aktualizací Windows 10](optimize-windows-10-update-delivery.md).  


> [!IMPORTANT]  
> Podpora klientů s operačním systémem je k dispozici ve Windows 10 verze 1607 s aktualizací agenta web Windows Update. Tato aktualizace je součástí aktualizací vydaných 11. dubna 2017. Další informace o těchto aktualizacích najdete v [článku o podpoře 4015217](https://support.microsoft.com/kb/4015217). Budoucí aktualizace využijí expresní pro menší soubory ke stažení. Předchozí verze Windows 10 a Windows 10 verze 1607 bez této aktualizace nepodporují soubory Expresní instalace.  


## <a name="enable-the-site-to-download-express-installation-files-for-windows-10-updates"></a>Povolit webovému serveru stažení souborů Expresní instalace pro aktualizace Windows 10
Pokud chcete zahájit synchronizaci metadat pro instalační soubory Windows 10 Express, povolte ji ve vlastnostech bodu aktualizace softwaru.  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** .  

2. Vyberte lokalitu centrální správy nebo samostatnou primární lokalitu.  

3. Na pásu karet klikněte na položku **Konfigurovat součásti webu**a poté klikněte na možnost **bod aktualizace softwaru**. Přepněte na kartu **soubory aktualizace** a vyberte **Stáhnout úplné soubory pro všechny schválené aktualizace a soubory Expresní instalace pro Windows 10**.

> [!NOTE]    
> Komponentu bodu aktualizace softwaru nelze nakonfigurovat tak, aby stahoval *pouze* expresní aktualizace.  Lokalita stáhne Kromě úplných souborů i soubory rychlé instalace. Tím se zvyšuje množství obsahu uloženého v knihovně obsahu a distribuované do a uložené v distribučních bodech.

> [!Tip]  
> Chcete-li určit skutečné místo na disku, které je používáno souborem, zkontrolujte vlastnost **Velikost na disku** souboru. Vlastnost Size na disku by měla být výrazně menší než hodnota Size. Další informace najdete v tématu [Nejčastější dotazy k optimalizaci doručování aktualizací Windows 10](optimize-windows-10-update-delivery.md#bkmk_faq).  


## <a name="enable-clients-to-download-and-install-express-installation-files"></a>Povolit klientům stahovat a instalovat soubory Expresní instalace
Pokud chcete povolit podporu souborů Expresní instalace na klientech, povolte soubory rychlé instalace ve skupině **aktualizace softwaru** nastavení klienta. Toto nastavení vytvoří nový naslouchací proces HTTP, který naslouchá požadavkům na stažení souborů Expresní instalace na portu, který zadáte.

> [!NOTE]    
> Toto je místní port, který klienti používají k naslouchání požadavkům na optimalizaci doručení nebo Background Intelligent Transfer Service (BITS) ke stažení expresního obsahu z distribučního bodu. Tento port nemusíte otevírat na firewallech, protože veškerý provoz je v místním počítači.  

Po nasazení nastavení klienta pro povolení této funkce v klientovi se pokusí stáhnout rozdíl mezi kumulativní aktualizací Windows 10 a aktualizací z předchozího měsíce v aktuálním měsíci. Klienti musí používat verzi Windows 10, která podporuje soubory Expresní instalace.  

1. Povolte podporu souborů Expresní instalace ve vlastnostech komponenty bodu aktualizace softwaru (předchozí postup).  

2. V konzole Configuration Manager otevřete pracovní prostor **Správa** a vyberte **nastavení klienta**.  

3. Vyberte odpovídající nastavení klienta a klikněte na pásu karet na **vlastnosti** .  

4. Vyberte skupinu **aktualizace softwaru** . Nastavte na **Ano** , pokud chcete na **klientech povolit instalaci expresních aktualizací**. Nakonfigurujte **port používaný ke stahování obsahu pro expresní aktualizace** s portem použitým naslouchacím procesem protokolu HTTP na klientovi.
    - Ve verzi 1902 se **port používaný ke stahování obsahu pro expresní aktualizace** změnil na **port, který klienti používají pro příjem požadavků na rozdílový obsah**.

## <a name="next-steps"></a>Další kroky

[Nasazení aktualizací softwaru](deploy-software-updates.md)