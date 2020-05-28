---
title: Nástroj pro stažení instalačního programu
titleSuffix: Configuration Manager
description: Pomocí samostatného nástroje si stáhněte aktuální verze instalačních souborů klíčů pro instalaci.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2da8aed5cfe4a478010165445094f1fce4627d9a
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428839"
---
# <a name="setup-downloader-for-configuration-manager"></a>Stažení instalačního programu pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Před spuštěním instalačního programu Configuration Manager pro instalaci nebo upgrade lokality můžete použít samostatný nástroj pro stažení instalačního programu ke stažení aktualizovaných instalačních souborů. Spusťte nástroj z verze Configuration Manager, kterou chcete nainstalovat. Pomocí aktualizovaných instalačních souborů zajistěte, aby instalace lokality používala aktuální verze instalačních souborů klíčů.

Když použijete nástroj pro stažení instalačního programu, určíte složku, která bude obsahovat soubory. Účet, který použijete ke spuštění nástroje, musí mít oprávnění **Úplné řízení** ke složce pro stahování. Když spustíte instalační program pro instalaci nebo upgrade lokality, můžete zadat tuto místní kopii souborů, které jste stáhli dříve. Toto chování zabraňuje instalačnímu programu v připojení k Microsoftu při spuštění instalace nebo upgradu lokality. Můžete použít stejnou místní kopii instalačních souborů pro jiné instalace lokality nebo upgrady stejné verze.

Nástroj pro stažení instalačního programu stáhne následující typy souborů:

- Požadované distribuovatelné soubory
- Jazykové sady
- Nejnovější aktualizace produktu pro instalaci

Ke spuštění nástroje pro stažení instalačního programu máte dvě možnosti:

- Spuštění aplikace s uživatelským rozhraním
- Spuštění aplikace na příkazovém řádku pro další možnosti příkazového řádku

Pokud vaše organizace omezuje síťovou komunikaci s Internetem pomocí brány firewall nebo proxy zařízení, je nutné povolit nástroji přístup k internetovým koncovým bodům. Zařízení, ve kterém spustíte nástroj, vyžaduje přístup k Internetu, který je stejný jako spojovací bod služby. Další informace najdete v tématu [požadavky na přístup k Internetu](../../../plan-design/network/internet-endpoints.md#bkmk_scp).<!-- SCCMDocs#677 -->

## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a>Spuštění nástroje pro stažení instalačního programu s uživatelským rozhraním

1. V počítači, který má přístup k Internetu, přejděte na instalační médium pro verzi Configuration Manager, kterou chcete nainstalovat.

1. V podsložce **SMSSETUP\BIN\X64** spusťte **setupdl. exe**.

1. Zadejte cestu ke složce, do které chcete uložit aktualizované instalační soubory, a pak vyberte **Stáhnout**. Nástroj pro stažení instalačního programu ověří soubory, které se aktuálně nacházejí ve složce pro stahování. Stahuje pouze soubory, které chybějí nebo jsou novější než stávající soubory. Vytváří podsložky pro stažené jazyky a další požadované součásti.

1. Chcete-li zkontrolovat výsledky stahování, přečtěte si téma **C:\ConfigMgrSetup.log**.

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a>Spuštění nástroje pro stažení instalačního programu z příkazového řádku

1. Otevřete příkazový řádek a změňte adresář na instalační médium pro verzi Configuration Manager, kterou chcete nainstalovat.

1. Změňte adresář na podsložku **SMSSETUP\BIN\X64** a spusťte **setupdl. exe** s nezbytnými možnostmi.

1. Chcete-li zkontrolovat výsledky stahování, přečtěte si téma **C:\ConfigMgrSetup.log**.

### <a name="command-line-options"></a>Možnosti příkazového řádku

Pomocí nástroje **setupdl. exe**můžete použít následující možnosti příkazového řádku:

- **/Verify**: Ověřte soubory ve složce pro stahování, které obsahují jazykové soubory. Seznam zastaralých souborů najdete v **C:\ConfigMgrSetup.log**. Když použijete tuto možnost, nestahují žádné soubory.

- **/VERIFYLANG**: Ověřte pouze jazykové soubory ve složce pro stahování. Seznam zastaralých jazykových souborů najdete v **C:\ConfigMgrSetup.log**.

- **/Lang**: stáhnout jenom jazykové soubory do složky pro stahování.

- **/NOUI**: Spusťte nástroj pro stažení instalačního programu bez uživatelského rozhraní. Když použijete tuto možnost, je nutná **cesta pro stažení** .

- **Cesta ke stažení**: Pokud chcete automaticky spustit proces ověření nebo stahování, zadejte cestu ke složce pro stahování. Když použijete možnost **/NOUI** , cesta ke stažení je povinná. Pokud cestu pro stažení nezadáte, nástroj pro stažení instalačního programu vás vyzve k zadání cesty. Pokud složka neexistuje, nástroj pro stažení instalačního programu ji vytvoří.

### <a name="example-commands"></a>Příklady příkazů

#### <a name="example-1"></a>Příklad 1

Nástroj pro stažení instalačního programu ověří soubory v zadané složce pro stahování a pak stáhne soubory.

`setupdl.exe C:\Download`

#### <a name="example-2"></a>Příklad 2

Nástroj pro stažení instalačního programu ověří pouze soubory v zadané složce pro stahování.

`setupdl.exe /VERIFY C:\Download`

#### <a name="example-3"></a>Příklad 3

Nástroj pro stažení instalačního programu ověří soubory v zadané složce pro stahování a pak stáhne soubory. Nástroj nezobrazuje žádné uživatelské rozhraní.

`setupdl.exe /NOUI C:\Download`

#### <a name="example-4"></a>Příklad 4

Nástroj pro stažení instalačního programu ověří jazykové soubory v zadané složce pro stahování a pak stáhne pouze jazykové soubory.

`setupdl.exe /LANG C:\Download`

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a>Kopírování souborů pro stažení instalačního programu do jiného počítače

1. V Průzkumníku Windows použijte jedno z následujících umístění:

    - **&lt;Configuration Manager instalační média> \SMSSETUP\BIN\X64**

    - **&lt;Configuration Manager cesta instalace> \BIN\X64**

1. Zkopírujte následující soubory do stejné cílové složky na druhém počítači:

    - **setupdl. exe**

    - **.\\&lt; jazyk > \\ setupdlres. dll**

        > [!NOTE]
        > Tento soubor je v podsložce pro jazyk instalace. Například angličtina je v `00000409` podsložce.

    Cílové složky v zařízení by měly vypadat jako v následujícím příkladu:

    - `C:\ConfigManInstall\setupdl.exe`

    - `C:\ConfigManInstall\00000409\setupdlres.dll`

1. Spusťte nástroj pro stažení instalačního programu z cílového počítače. Použijte buď [uživatelské rozhraní](#bkmk_ui) , nebo příkazový [řádek](#bkmk_cmd).
