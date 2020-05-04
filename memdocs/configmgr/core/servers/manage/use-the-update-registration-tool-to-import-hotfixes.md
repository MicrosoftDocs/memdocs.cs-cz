---
title: Nástroj pro registraci aktualizací
titleSuffix: Configuration Manager
description: Zjistěte, kdy a jak používat nástroj pro registraci aktualizací k ručnímu importu aktualizace do konzoly Configuration Manager.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8cc13635-85d6-4b07-a3ec-c42188bc5c74
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 420b13005e8f9ac3d79f7d94398e6aa0ddcc190c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711235"
---
# <a name="use-the-update-registration-tool-to-import-hotfixes-to-configuration-manager"></a>Použijte nástroj pro registraci aktualizací k importu oprav hotfix do Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Některé aktualizace Configuration Manager nejsou z cloudové služby Microsoftu k dispozici a jsou získány pouze mimo IP síť. Příkladem je omezené vydání opravy hotfix, která řeší konkrétní problém.   
Pokud je nutné nainstalovat vzdálenou verzi a název souboru aktualizace nebo opravy hotfix končí příponou **Update. exe**, použijte **Nástroj pro registraci aktualizací** k ručnímu importu aktualizace do konzoly Configuration Manager. Nástroj umožňuje extrahovat a převést balíček aktualizace na server lokality a zaregistrovat aktualizaci v konzole nástroje Configuration Manager.  

 Pokud má soubor opravy hotfix příponu souboru **. exe** (ne **Update. exe**), přečtěte si téma [použití instalačního programu oprav hotfix k instalaci aktualizací pro Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  

> [!NOTE]  
>  V tomto tématu najdete obecné pokyny k instalaci oprav hotfix, které aktualizují Configuration Manager. Podrobnosti o konkrétní aktualizaci nebo opravě hotfix najdete v příslušném článku znalostní báze Knowledge Base (KB) na adrese podpora Microsoftu.  

 **Předpoklady použití nástroje pro registraci aktualizací:**  

-   Pomocí tohoto nástroje se dá nainstalovat jenom aktualizace pro vzdálené aktualizace, které končí příponou **. Update. exe.**  

-   Nástroj je nezávislý na jednotlivých aktualizacích, které získáte přímo od Microsoftu.  

-   Nástroj není závislý na režimu spojovacího bodu služby.  

-   Nástroj musí být spuštěn v počítači, který je hostitelem spojovacího bodu služby.  

-   Počítač, ve kterém se nástroj spustí (počítač se spojovacím bodem služby) musí mít nainstalovanou .NET Framework 4,52.  

-   Účet, který použijete ke spuštění nástroje, musí mít oprávnění **místního správce** v počítači, který je hostitelem spojovacího bodu služby (ve kterém se nástroj spouští).  

-   Účet, který použijete ke spuštění nástroje, musí mít oprávnění k **zápisu** do následující složky v počítači, který je hostitelem spojovacího bodu služby: ** &lt;instalační\>adresář nástroje ConfigMgr \EasySetupPayload\offline**  

### <a name="to-use-the-update-registration-tool"></a>Použití nástroje pro registraci aktualizací  

1. V počítači, který je hostitelem spojovacího bodu služby:  

   -   Otevřete příkazový řádek s oprávněními správce a potom změňte adresáře na umístění, které obsahuje ** &lt;produkt\>-&lt;\>-&lt;\>produktu ID článku znalostní báze-ConfigMgr. Update. exe.**  

2. Zadáním následujícího příkazu spusťte nástroj pro registraci aktualizací:  

   -   **&lt;\>\>Produkt verze-produktu ID\>článku znalostní báze-ConfigMgr. Update. exe-&lt;&lt;**  

   Po registraci se oprava hotfix zobrazí jako nová aktualizace v konzole během 24 hodin.  Proces můžete urychlit:

   - Otevřete konzolu Configuration Manager, přejděte na **Správa** > **aktualizace a údržba**a pak klikněte na **Vyhledat aktualizace**. (Před verzí 1702 se aktualizace a údržba **Administration** > **Cloud Services**.) 

   Nástroj pro registraci aktualizací protokoluje své akce do souboru .log v místním počítači. Soubor protokolu má stejný název jako soubor hotfix. exe a je zapsaný ve složce **% systemroot%/Temp** .  

    Po registraci aktualizace můžete nástroj pro registraci aktualizací zavřít.  

3. Otevřete konzolu Configuration Manager a přejděte do části **Správa** > **aktualizace a údržba**. Importované opravy hotfix jsou teď dostupné k instalaci. (Před verzí 1702 se aktualizace a údržba **Administration** > **Cloud Services**.)

   Informace o instalaci aktualizací najdete v tématu [instalace konzolových aktualizací pro Configuration Manager](../../../core/servers/manage/install-in-console-updates.md)  
