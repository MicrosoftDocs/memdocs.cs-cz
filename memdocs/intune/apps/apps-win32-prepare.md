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
ms.openlocfilehash: aaf4f009b25b09500d1a17a8c8a97b5f91e330e2
ms.sourcegitcommit: 54a771f1a632aef5d6bf8c71ce1e2c7823513b52
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/10/2020
ms.locfileid: "90003442"
---
# <a name="prepare-win32-app-content-for-upload"></a>Příprava obsahu aplikace Win32 pro nahrání

Než budete moct přidat aplikaci Win32 do Microsoft Intune, musíte aplikaci připravit pomocí [Nástroje pro přípravu obsahu Microsoft Win32](https://go.microsoft.com/fwlink/?linkid=2065730).

## <a name="prerequisites"></a>Předpoklady

Pokud chcete používat správu aplikací Win32, ujistěte se, že splňujete následující kritéria:

- Windows 10 verze 1607 nebo novější (verze Enterprise, pro a školství)
- Klient Windows 10 musí splňovat tyto předpoklady: 
  - Zařízení musí být připojená k Azure AD a automaticky zaregistrovaná. Rozšíření pro správu Intune podporuje připojení ke službě Azure AD, která je připojená k hybridní doméně, a jsou podporovaná zařízení zaregistrovaná v zásadách skupiny. 
  > [!NOTE]
  > V případě zaregistrovaného scénáře zásad skupiny koncový uživatel použije místní uživatelský účet k AAD připojit své zařízení s Windows 10. Uživatel se musí do zařízení přihlásit pomocí svého uživatelského účtu AAD a zaregistrovat se do Intune. Intune nainstaluje na zařízení rozšíření pro správu Intune, pokud je skript PowerShellu nebo aplikace Win32 cílené na uživatele nebo zařízení.
- Velikost aplikace systému Windows je omezené na 8 GB na aplikaci.

## <a name="convert-the-win32-app-content"></a>Převod obsahu aplikace Win32

K předběžnému zpracování aplikací pro Windows Classic (Win32) použijte [Nástroj pro přípravu obsahu Win32 od Microsoftu](https://go.microsoft.com/fwlink/?linkid=2065730) . Nástroj převede instalační soubory aplikace do formátu *. intunewin* . Nástroj také detekuje některé atributy, které Intune vyžaduje k určení stavu instalace aplikace. Po použití tohoto nástroje ve složce instalačního programu aplikace budete moct vytvořit aplikaci Win32 v konzole Intune.

> [!IMPORTANT]
> [Nástroj pro přípravu obsahu Microsoft Win32](https://go.microsoft.com/fwlink/?linkid=2065730) zips všechny soubory a podsložky při vytváření souboru *. intunewin* . Ujistěte se, že nástroj pro přípravu obsahu Microsoft Win32 je oddělený od instalačních souborů a složek, takže nezahrnete do souboru *. intunewin* nástroj ani jiné nepotřebné soubory a složky.

[Nástroj pro přípravu obsahu Microsoft Win32](https://go.microsoft.com/fwlink/?linkid=2065730) si můžete stáhnout z GitHubu jako soubor zip. Soubor zip obsahuje složku s názvem **Microsoft-Win32-Content-PREP-Tool-Master**. Složka obsahuje nástroj pro přípravu, licenci, soubor Readme a poznámky k verzi. 

### <a name="process-flow-to-create-intunewin-file"></a>Tok procesu pro vytvoření souboru. intunewin

   <img alt="Process flow to create a .intunewin file" src="./media/apps-win32-app-management/prepare-win32-app.png" width="700">

### <a name="run-the-microsoft-win32-content-prep-tool"></a>Spuštění nástroje pro přípravu obsahu Microsoft Win32

Pokud spustíte `IntuneWinAppUtil.exe` z příkazového okna bez parametrů, nástroj vás provede zadáním podrobných parametrů. Nebo můžete přidat parametry do příkazu na základě následujících dostupných parametrů příkazového řádku.

### <a name="available-command-line-parameters"></a>Dostupné parametry příkazového řádku 

|    **Parametr příkazového řádku**    |    **Popis**    |
|--------------------------------|------------------------------------------------------------|
|    `-h`     |    Nápověda    |
|    `-c <setup_folder>`     |    Složka pro všechny instalační soubory. Všechny soubory v této složce budou zkomprimovány do souboru *. intunewin* .    |
|    `-s <setup_file>`     |    Instalační soubor (například *setup.exe* nebo *setup.msi*)    |
|    `-o <output_folder>`     |    Výstupní složka pro vygenerovaný soubor *.intunewin*    |
|    `-q`       |    Tichý režim    |

### <a name="example-commands"></a>Příklady příkazů

|    **Ukázkový příkaz**    |    **Popis**    |
|-------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `IntuneWinAppUtil -h`    |    Tento příkaz zobrazí informace o využití nástroje.    |
|    `IntuneWinAppUtil -c c:\testapp\v1.0 -s c:\testapp\v1.0\setup.exe -o c:\testappoutput\v1.0 -q`    |    Tento příkaz vygeneruje soubor `.intunewin` ze zadané zdrojové složky a instalačního souboru. U instalačního souboru MSI tento nástroj načte požadované informace pro Intune. Pokud zadáte parametr `-q`, příkaz se spustí v tichém režimu a pokud už výstupní soubor existuje, přepíše se. Pokud výstupní složka ještě neexistuje, automaticky se vytvoří.    |

Při generování souboru *. intunewin* uložte všechny soubory, které potřebujete odkazovat do podsložky složky nastavení. Pak použijte relativní cestu k odkazování na konkrétní soubor, který potřebujete. Například:

**Zdrojová složka instalačního programu:** *c:\testapp\v1.0*<br>
**Soubor s licencí:** *c:\testapp\v1.0\licenses\license.txt*

Odkaz na soubor *license.txt* pomocí relativní cesty *licenses\license.txt*.

## <a name="next-steps"></a>Další kroky

- [Přidejte aplikaci Win32 pro Microsoft Intune](apps-win32-add.md).
