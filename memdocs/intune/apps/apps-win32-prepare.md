---
title: Příprava nahrávání aplikace Win32 na Microsoft Intune
titleSuffix: ''
description: Naučte se, jak připravit aplikaci Win32, aby se nahrála do Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 94626b6cc7e9586ff6b9230206c3e57e6b01b86f
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083793"
---
# <a name="prepare-win32-app-content-for-upload"></a>Příprava obsahu aplikace Win32 pro nahrání

Než budete moct přidat aplikaci Win32 do Microsoft Intune, musíte aplikaci připravit pomocí [Nástroje pro přípravu obsahu Microsoft Win32](https://go.microsoft.com/fwlink/?linkid=2065730).

## <a name="prerequisites"></a>Požadavky

Pokud chcete používat správu aplikací Win32, ujistěte se, že splňujete následující kritéria:

- Použijte Windows 10 verze 1607 nebo novější (verze Enterprise, pro a školství).
- Zařízení musí být připojená k Azure Active Directory (Azure AD) a automaticky zaregistrovaná. Rozšíření správy Intune podporuje zařízení, která jsou připojená k Azure AD, připojené k hybridní doméně a zaregistrované zásady skupiny. 
  > [!NOTE]
  > V případě registrace zásad skupiny uživatel používá místní uživatelský účet ke službě Azure AD připojit své zařízení s Windows 10. Uživatel se musí přihlásit k zařízení pomocí svého uživatelského účtu Azure AD a zaregistrovat se v Intune. Intune nainstaluje na zařízení rozšíření pro správu Intune, pokud je skript PowerShellu nebo aplikace Win32 cílené na uživatele nebo zařízení.
- Velikost aplikace systému Windows je omezené na 8 GB na aplikaci.

## <a name="convert-the-win32-app-content"></a>Převod obsahu aplikace Win32

K předběžnému zpracování aplikací pro Windows Classic (Win32) použijte [Nástroj pro přípravu obsahu Win32 od Microsoftu](https://go.microsoft.com/fwlink/?linkid=2065730) . Nástroj převede instalační soubory aplikace do formátu *. intunewin* . Nástroj také detekuje některé atributy, které Intune vyžaduje k určení stavu instalace aplikace. Po použití tohoto nástroje ve složce instalačního programu aplikace budete moct vytvořit aplikaci Win32 v konzole Intune.

> [!IMPORTANT]
> [Nástroj pro přípravu obsahu Microsoft Win32](https://go.microsoft.com/fwlink/?linkid=2065730) zips všechny soubory a podsložky při vytváření souboru *. intunewin* . Ujistěte se, že nástroj pro přípravu obsahu Microsoft Win32 je oddělený od instalačních souborů a složek, takže nezahrnete do souboru *. intunewin* nástroj ani jiné nepotřebné soubory a složky.

[Nástroj pro přípravu obsahu Microsoft Win32](https://go.microsoft.com/fwlink/?linkid=2065730) si můžete stáhnout z GitHubu jako soubor. zip. Soubor zip obsahuje složku s názvem *Microsoft-Win32-Content-PREP-Tool-Master*. Složka obsahuje nástroj pro přípravu, licenci, soubor Readme a poznámky k verzi. 

### <a name="process-flow-to-create-a-intunewin-file"></a>Tok procesu pro vytvoření souboru. intunewin

   <img alt="Flow chart of the process to create a .intunewin file." src="./media/apps-win32-app-management/prepare-win32-app.png" width="700">

### <a name="running-the-microsoft-win32-content-prep-tool"></a>Spuštění nástroje pro přípravu obsahu Microsoft Win32

Pokud spouštíte `IntuneWinAppUtil.exe` z příkazového okna bez parametrů, nástroj vám pomůže zadat požadované parametry krok za krokem. Nebo můžete přidat parametry do příkazu na základě následujících dostupných parametrů příkazového řádku.

### <a name="available-command-line-parameters"></a>Dostupné parametry příkazového řádku 

|    **Parametr příkazového řádku**    |    **Popis**    |
|--------------------------------|------------------------------------------------------------|
|    `-h`     |    Nápověda    |
|    `-c <setup_folder>`     |    Složka pro všechny instalační soubory. Všechny soubory v této složce budou zkomprimovány do souboru *. intunewin* .    |
|    `-s <setup_file>`     |    Instalační soubor (například *setup.exe* nebo *setup.msi*)    |
|    `-o <output_folder>`     |    Výstupní složka pro vygenerovaný soubor *.intunewin*    |
|    `-q`       |    Tichý režim.    |

### <a name="example-commands"></a>Příklady příkazů

|    **Ukázkový příkaz**    |    **Popis**    |
|-------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `IntuneWinAppUtil -h`    |    Tento příkaz zobrazí informace o využití nástroje.    |
|    `IntuneWinAppUtil -c c:\testapp\v1.0 -s c:\testapp\v1.0\setup.exe -o c:\testappoutput\v1.0 -q`    |    Tento příkaz vytvoří soubor *. intunewin* ze zadané zdrojové složky a instalačního souboru. U instalačního souboru MSI tento nástroj načte požadované informace pro Intune. Pokud `-q` je zadaný, příkaz se spustí v tichém režimu. Pokud výstupní soubor již existuje, bude přepsán. I když výstupní složka neexistuje, vytvoří se automaticky.    |

Při generování souboru *. intunewin* uložte všechny soubory, které potřebujete odkazovat do podsložky složky nastavení. Pak použijte relativní cestu k odkazování na konkrétní soubor, který potřebujete. Příklad:

**Zdrojová složka instalačního programu:** *c:\testapp\v1.0*<br>
**Soubor s licencí:** *c:\testapp\v1.0\licenses\license.txt*

Odkaz na soubor *license.txt* pomocí relativní cesty *licenses\license.txt*.

## <a name="next-steps"></a>Další kroky

- [Přidání aplikace Win32 do Microsoft Intune](apps-win32-add.md)
