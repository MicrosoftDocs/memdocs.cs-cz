---
title: Nástroj pro stažení instalačního programu
titleSuffix: Configuration Manager
description: Přečtěte si o této samostatné aplikaci, která je navržená tak, aby instalace lokality používala aktuální verze instalačních souborů klíčů.
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2fa1899f8e7dc14812f9f9ecf889350a153b2d25
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718074"
---
# <a name="setup-downloader-for-configuration-manager"></a>Stažení instalačního programu pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Než spustíte instalační program pro instalaci nebo upgrade lokality Configuration Manager, můžete použít samostatnou aplikaci pro stažení instalačního programu z verze Configuration Manager, kterou chcete nainstalovat, abyste stáhli aktualizované instalační soubory.  

Pomocí aktualizovaných instalačních souborů zajistíte, aby instalace lokality používala aktuální verze instalačních souborů klíčů. V oveview:   
-   Když ke stahování souborů před spuštěním instalačního programu použijete nástroj pro stažení instalačního programu, určíte složku, která bude obsahovat soubory.  
-   Účet, který použijete ke spuštění nástroje pro stažení instalačního programu, musí mít oprávnění **Úplné řízení** ke složce pro stahování.  
-   Když spustíte instalační program pro instalaci nebo upgrade lokality, můžete ji nasměrovat na použití této místní kopie souborů, které jste stáhli dříve. Tím se zabrání tomu, aby se při instalaci nebo upgradu lokality při spuštění instalace nebo upgradu lokality muselo připojit se k Microsoftu.  
-   Pro následné instalace nebo upgrady lokality můžete použít stejnou místní kopii instalačních souborů.  

Nástroj pro stažení instalačního programu stáhne následující typy souborů:  
-   Požadované distribuovatelné soubory  
-   Jazykové sady  
-   Nejnovější aktualizace produktu pro instalaci  

Ke spuštění nástroje pro stažení instalačního programu máte dvě možnosti:
- Spuštění aplikace s uživatelským rozhraním
- Pro možnosti příkazového řádku spusťte aplikaci na příkazovém řádku.


## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a>Spuštění nástroje pro stažení instalačního programu s uživatelským rozhraním  

1.  V počítači s přístupem k Internetu spusťte Průzkumníka Windows a přejděte na ** &lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**.  

2.  Chcete-li spustit nástroj pro stažení instalačního programu, poklikejte na **setupdl. exe**.   

3. Zadejte cestu ke složce, která bude hostovat aktualizované instalační soubory, a klikněte na tlačítko **Stáhnout**. Nástroj pro stažení instalačního programu ověří soubory, které se aktuálně nacházejí ve složce pro stahování. Stahuje pouze soubory, které chybějí nebo jsou novější než stávající soubory. Nástroj pro stažení instalačního programu vytváří podsložky pro stažené jazyky a další požadované podsložky.  

4.  Chcete-li zkontrolovat výsledky stahování, otevřete soubor **ConfigMgrSetup. log** v kořenovém adresáři jednotky C.  .  

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a>Spuštění nástroje pro stažení instalačního programu z příkazového řádku  

1.  V okně příkazového řádku přejdete na ** &lt; *Configuration Manager \SMSSETUP\BIN\X64 instalační médium*\>**.   

2.  Chcete-li spustit nástroj pro stažení instalačního programu, spusťte **setupdl. exe**.

    Pomocí nástroje **setupdl. exe**můžete použít následující možnosti příkazového řádku:   

    -   **/Verify**: pomocí této možnosti ověříte soubory ve složce pro stahování, které obsahují jazykové soubory. Seznam zastaralých souborů najdete v souboru ConfigMgrSetup. log v kořenovém adresáři jednotky C. Při použití této možnosti se nestahují žádné soubory.  

    -   **/VERIFYLANG**: pomocí této možnosti ověříte jazykové soubory ve složce pro stahování. Seznam zastaralých jazykových souborů najdete v souboru ConfigMgrSetup. log v kořenovém adresáři jednotky C.

    -   **/Lang**: tuto možnost použijte, pokud chcete stáhnout pouze jazykové soubory do složky pro stahování.  

    -   **/NOUI**: tuto možnost použijte, pokud chcete spustit nástroj pro stažení instalačního programu bez zobrazení uživatelského rozhraní. Když použijete tuto možnost, musíte zadat cestu pro **stažení** jako součást příkazu na příkazovém řádku.  

    -   DownloadPath: můžete zadat cestu ke složce pro stahování, chcete-li automaticky spustit proces ověření nebo stažení. ** &lt;\>** Pokud použijete možnost **/NOUI** , musíte zadat cestu pro stažení. Pokud nezadáte cestu pro stahování, je nutné zadat cestu při spuštění nástroje pro stažení instalačního programu. Nástroj pro stažení instalačního programu vytvoří složku, pokud neexistuje.  

    Příklady příkazů:

    -   **setupdl &lt;DownloadPath\>**  

        -   Nástroj pro stažení instalačního programu se spustí, ověří soubory v zadané složce pro stahování a pak stáhne jenom soubory, které chybí nebo které mají novější verze než existující soubory.     

    -   **setupdl/VERIFY &lt;DownloadPath\>**  

        -   Stažení instalačního programu spustí a ověří soubory v zadané složce pro stahování.  

    -   **setupdl/NOUI &lt;DownloadPath\>**  

        -   Nástroj pro stažení instalačního programu se spustí, ověří soubory v zadané složce pro stahování a pak stáhne jenom soubory, které chybějí nebo jsou novější než stávající soubory.  

    -   **setupdl/LANG &lt;DownloadPath\>**  

        -   Nástroj pro stažení instalačního programu se spustí, ověří jazykové soubory v zadané složce pro stahování a pak stáhne jenom jazykové soubory, které chybějí nebo jsou novější než stávající soubory.  

    -   **setupdl/VERIFY**  

        -   Spustí se nástroj pro stažení instalačního programu a pak musíte zadat cestu ke složce pro stahování. Když potom kliknete na **ověřit**, nástroj pro stažení instalačního programu ověří soubory ve složce pro stahování.  

3.  Chcete-li zkontrolovat výsledky stahování, otevřete soubor **ConfigMgrSetup. log** v kořenovém adresáři jednotky C.

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a>Kopírování souborů pro stažení instalačního programu do jiného počítače

1. V Průzkumníku Windows použijte jedno z následujících umístění:

    - **&lt;Configuration Manager instalační média> \SMSSETUP\BIN\X64**
    - **&lt;Configuration Manager cesta instalace> \BIN\X64**
    
1. Zkopírujte následující soubory do stejné cílové složky na druhém počítači:
    
    - **setupdl. exe**
    - **. \\jazyk>\\setupdlres &lt;. dll**
      - Tento soubor je v podsložce pro jazyk instalace. Například angličtina je v `00000409` podsložce.

    Například cílové složky na vašem zařízení by měly vypadat takto:
    - C:\ConfigManInstall\setupdl.exe
    - C:\ConfigManInstall\00000409\setupdlres.dll

1. Spusťte nástroj pro stažení instalačního programu z počítače pomocí [uživatelského rozhraní](#bkmk_ui) nebo [příkazového řádku](#bkmk_cmd)popsaného v částech výše.
