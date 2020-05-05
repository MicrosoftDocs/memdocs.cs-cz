---
title: Podpora kódování Unicode a ASCII
titleSuffix: Configuration Manager
description: Přečtěte si o podpoře znaků Unicode a ASCII v Configuration Managerch objektech.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bdec799-905f-48bc-aed5-2d92134739e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7bd3dad5f0ef24074ac8c8e6d2edf01d5641b541
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717549"
---
# <a name="unicode-and-ascii-support-in-configuration-manager"></a>Podpora kódování Unicode a ASCII v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager vytváří většinu objektů pomocí znaků Unicode. Nicméně několik objektů podporuje pouze znaky ASCII, nebo mají jiná omezení.  

## <a name="objects-that-use-ascii-characters"></a><a name="BKMK_ASCIIchar"></a>Objekty používající znaky ASCII

Při vytváření následujících objektů Configuration Manager podporuje pouze znakovou sadu ASCII:  

- Kód lokality  

- Všechny názvy počítačů serveru systému lokality  

- Následující účty Configuration Manager:  

    > [!NOTE]  
    > Tyto účty podporují znaky ASCII a ru znaky na webu, který běží v ruštině.  

    - Účet klientské nabízené instalace  

    - Účet připojení databáze bodu správy  

    - Účet přístupu k síti  

    - Účet pro přístup k balíčku  

    - Účet standardního odesílatele  

    - Účet instalace systému lokality  

    - Účet pro připojení k bodu aktualizace softwaru  

    - Účet proxy server bodu aktualizace softwaru  

    > [!NOTE]  
    > Účty, které zadáte pro správu na základě rolí, podporují kódování Unicode.  
    >
    > Účet bodu služby Reporting Services podporuje kódování Unicode s výjimkou ru znaků.  

- Plně kvalifikovaný název domény (FQDN) pro servery lokality a systémy lokality  

- Instalační cesta pro Configuration Manager  

- Názvy instancí SQL Server  

- Cesta pro následující role systému lokality:  

    - Bod registrace  

    - Zprostředkující bod registrace  

    - Bod služby Reporting services  

    - Bod migrace stavu  

- Cesta pro následující složky:  

    - Složka, ve které jsou uložena data migrace stavu klienta  

    - Složka, která obsahuje sestavy Configuration Manager  

    - Složka, ve které je uložena záloha Configuration Manager  

    - Složka, ve které jsou uloženy zdrojové instalační soubory pro instalaci lokality  

    - Složka, ve které jsou uloženy požadované soubory ke stažení pro použití instalačním programem  

- Cesta pro následující objekty:  

    - Web služby IIS  

    - Instalační cesta virtuální aplikace  

    - Název virtuální aplikace  

- Názvy souborů ISO spouštěcího média  


## <a name="additional-limitations"></a><a name="BKMK_OtherCharLimitations"></a>Další omezení

Následují další omezení pro podporované znakové sady a jazykové verze:  

- Configuration Manager nepodporuje změnu národního prostředí počítače serveru lokality.  

- Podniková certifikační autorita (CA) nepodporuje názvy klientských počítačů, které používají dvoubajtové znakové sady (DBCS). Názvy klientských počítačů, které můžete použít, jsou omezeny omezením infrastruktury veřejných klíčů ve znakové sadě IA5. Configuration Manager nepodporuje názvy certifikačních autorit ani hodnoty názvu subjektu, které používají sadu DBCS.  


## <a name="objects-that-arent-localized"></a><a name="BKMK_LangNonLocalize"></a>Objekty, které nejsou lokalizovány

Databáze Configuration Manager podporuje kódování Unicode pro většinu objektů, které ukládá. Pokud je to možné, zobrazí tyto informace v jazyce operačního systému, který se shoduje s národním prostředím počítače. Pro klientské rozhraní nebo Configuration Manager konzolu pro zobrazení informací v jazyce operačního systému počítače musí národní prostředí počítače odpovídat jazyku klienta nebo serveru, který nainstalujete v lokalitě nástroje.  

Několik objektů Configuration Manager nepodporuje kódování Unicode. Jsou uloženy v databázi pomocí ASCII nebo mají další jazyková omezení. Tyto informace se vždy zobrazují pomocí znakové sady ASCII nebo v jazyce, který byl použit při vytváření objektu.  
