---
title: Příprava pro nasazení do neznámých počítačů
titleSuffix: Configuration Manager
description: Naučte se nasazovat operační systémy do počítačů, které nejsou spravované pomocí Configuration Manager ve vašem Configuration Manager prostředí.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9e447e34-0943-49ed-b6ba-3efebf3566c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e79e2ec1d42c7ed0e520b5e117fbac73817511a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724066"
---
# <a name="prepare-for-unknown-computer-deployments-in-configuration-manager"></a>Příprava na nasazení neznámých počítačů v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Informace v tomto tématu použijte k nasazení operačních systémů do neznámých počítačů v prostředí Configuration Manager. Neznámý počítač je počítač, který není spravován nástrojem Configuration Manager. To znamená, že v databázi Configuration Manager není žádný záznam o těchto počítačích. Neznámé počítače zahrnují následující:  

- Počítač, na kterém není nainstalovaný klient Configuration Manager  

- Počítač, který není importován do Configuration Manager  

- Počítač, který nebyl zjištěn nástrojem Configuration Manager  

  Pomocí následujících metod nasazení můžete nasazovat operační systémy na neznámé počítače:  

- [Použití technologie PXE k nasazení Windows přes síť](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)  

- [Nasazení operačního systému pomocí spouštěcího média](../deploy-use/create-bootable-media.md)  

- [Nasazení operačního systému pomocí předzpracovaného média](../deploy-use/create-prestaged-media.md)  

## <a name="unknown-computer-deployment-workflow"></a>Pracovní postup nasazení na neznámý počítač  
 Toto je základní pracovní postup pro nasazení operačního systému na neznámý počítač:  

-   Vyberte objekt neznámého počítače k použití při nasazování. Operační systém můžete nasadit na jeden z objektů neznámých počítačů v kolekci **Všechny neznámé počítače** nebo můžete přidat objekty z kolekce **Všechny neznámé počítače** do jiné kolekce. Configuration Manager poskytuje dva objekty neznámých počítačů v kolekci **všechny neznámé počítače** . Jeden objekt je pro počítače x86 a druhý objekt pro počítače x64.  

    > [!NOTE]  
    >  Objekt **Neznámý počítač x86** je pouze pro počítače, které mají architekturu x86. Objekt **Neznámý počítač x64** je pro počítače, které mají architekturu x86 a x64. Jinými slovy tyto objekty popisují architekturu cílového počítače. Nepopisují operační systém, který chcete nasadit na cílový počítač.  

-   Nakonfigurujte distribuční bod, který má povolenou technologii PXE, nebo vytvořte médium pro podporu nasazení na neznámý počítač.  

-   Nasaďte pořadí úkolů pro nasazení operačního systému.  

## <a name="unknown-computer-installation-process"></a>Proces instalace neznámého počítače  
 Když se počítač poprvé spustí z prostředí PXE nebo z média, Configuration Manager zkontroluje, jestli v databázi Configuration Manager existuje záznam pro tento počítač. Pokud záznam existuje, Configuration Manager pak zkontroluje, zda existují nějaké sekvence úloh nasazené na záznam. Pokud se nejedná o záznam, Configuration Manager zkontroluje, zda jsou v objektu neznámého počítače nasazeny nějaké sekvence úloh. V obou případech Configuration Manager pak provede jednu z následujících akcí:  

- Pokud je k dispozici pořadí úkolů, Configuration Manager vyzve uživatele ke spuštění pořadí úkolů.  

- Pokud existuje požadované pořadí úloh, Configuration Manager automaticky spustí pořadí úloh.  

- Pokud pořadí úkolů není pro tento záznam nasazeno, Configuration Manager vygeneruje chybu, která pro cílový počítač neexistuje žádná nasazená sekvence úloh.  

  Po spuštění neznámého počítače Configuration Manager rozpozná počítač jako nezřízený počítač místo neznámého počítače. To znamená, že tento počítač nyní může obdržet sekvence úloh, které byly nasazeny na objekt neznámého počítače. Nasazená sekvence úloh pak nainstaluje bitovou kopii operačního systému, která musí zahrnovat klienta Configuration Manager.  

  Po instalaci klienta Configuration Manager bude vytvořen záznam pro počítač a počítač bude uveden v příslušné Configuration Manager kolekci. Pokud se počítači nepodařilo nainstalovat bitovou kopii operačního systému nebo klienta Configuration Manager, vytvoří se záznam "Neznámý" pro počítač a počítač se zobrazí v kolekci **všechny systémy** .  

> [!NOTE]  
>  Během instalace bitové kopie operačního systému může sekvence úloh získat z tohoto počítače proměnné z kolekce, ale nikoli proměnné z počítače.  

##  <a name="enabling-unknown-computer-support"></a><a name="BKMK_EnablingUnknown"></a>Povolení podpory neznámého počítače  
 Následující informace můžete použít k povolení podpory neznámých počítačů při nasazení pomocí technologie PXE, spouštěcího média a předzpracovaného média.  

-   **PXE**  

     Zaškrtněte políčko **Povolit podporu neznámých počítačů** na kartě **Technologie PXE** pro distribuční bod, který má povolenou technologii PXE. Další informace najdete v tématu [Konfigurace distribučních bodů pro příjem požadavků PXE](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint).  

-   **Spouštěcí médium**  

     Zaškrtněte políčko **Povolit podporu neznámého počítače** na stránce **Zabezpečení** v Průvodci vytvořením média pořadí úloh. Další informace najdete v tématu [Konfigurace distribučních bodů pro příjem požadavků PXE](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint) a [použití technologie PXE k nasazení Windows přes síť pomocí Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

-   **Předzpracované médium**  

     Zaškrtněte políčko **Povolit podporu neznámého počítače** na stránce **Zabezpečení** v Průvodci vytvořením média pořadí úloh. Další informace najdete v tématu [Vytvoření předzpracovaného média pomocí Configuration Manager](../deploy-use/create-prestaged-media.md).  
