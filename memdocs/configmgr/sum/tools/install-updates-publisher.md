---
title: Nainstalovat Updates Publisher
titleSuffix: Configuration Manager
description: Instalace System Center Updates Publisher ve vašem prostředí
ms.date: 08/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: ab5cda93-b67c-4aa5-904d-7b63ce790aa0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2f83e7207207496d69342a2322909e972ada5676
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720370"
---
# <a name="install-updates-publisher"></a>Nainstalovat Updates Publisher

*Platí pro: System Center Updates Publisher*

Informace v těchto článcích vám pomůžou stáhnout, nainstalovat a nastavit vydavatele aktualizací pro použití s prostředím Configuration Manager.

## <a name="prerequisites-and-limitations"></a>Požadavky a omezení
System Center Updates Publisher lze použít pouze s Configuration Manager. Není určený pro použití se samostatnými hierarchiemi služby WSUS.

V následujících částech jsou popsány požadavky pro instalaci a používání nástroje Updates Publisher a omezení nebo známých problémů jeho použití.  

### <a name="operating-systems"></a>Operační systémy
Nainstalujte a spusťte Updates Publisher v 64 edicích těchto operačních systémů. Neexistují žádné minimální požadavky kumulativní aktualizace nebo aktualizace Service Pack.

-   Windows Server 2016 (Standard, Datacenter)
-   Windows Server 2012 R2 (Standard, Datacenter)
-   Windows 10 (pro, vzdělávání, vzdělávání pro firmy)
-   Windows 8.1 (Professional, Enterprise)

### <a name="prerequisites"></a>Požadavky
V počítači, který spouští nástroje Updates Publisher, jsou vyžadovány následující požadavky.

-   **64 bitový operační systém**: počítač, na který instalujete Updates Publisher, musí mít spuštěný 64 operační systém.
-   **WSUS 6,2 nebo novější**:
    -   V systému Windows Server nainstalujte výchozí konzolu pro správu, aby splňovala tento požadavek.
    -   Pro Windows 10 a Windows 8.1 nainstalujte [Nástroje pro vzdálenou správu serveru (RSAT) pro operační systémy Windows](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems). Tím se nainstaluje potřebná podpora pro použití nástroje Updates Publisher (*rozhraní API a rutin prostředí PowerShell*a *konzoly pro správu uživatelského rozhraní*).
-   **Oprávnění**:
    -   Instalace: místní správce
    -   Většina operací: místní uživatel
    -   Publikování nebo operace zahrnující službu WSUS: člen skupiny Správci služby WSUS na serveru WSUS.

### <a name="supported-languages"></a>Podporované jazyky
Publisher Updates je k dispozici pouze v angličtině, ale může spravovat aktualizace pro jiné jazyky. Podpora jazyků závisí na úloze, jako je publikování, vytváření nebo úpravy aktualizací.

Při exportu nebo publikování aktualizací zobrazí Vydavatel aktualizace název a Popis aktualizace softwaru na základě národního prostředí počítače, ve kterém je nainstalován program Updates Publisher.

Například vytvoříte aktualizaci softwaru s názvem v angličtině a španělštině.

-   Pokud vytvoříte aktualizaci na počítači, jehož národní prostředí je anglické, ve výchozím nastavení se zobrazí nadpis a popis v angličtině.
-   Pokud tuto aktualizaci exportujete nebo publikujete na počítači, jehož národní prostředí je španělština, v tomto počítači byste viděli nadpis a popis v španělštině.

### <a name="publishing"></a>Publikování
Když publikujete aktualizace softwaru, můžete zadat jazyk binárního souboru aktualizace softwaru. Můžete také určit, že binární soubor je jazykově neutrální. Podporují se tyto jazyky:

-   Arabština
-   Čínština (Hongkong – zvláštní správní oblast ČLR)
-   Čínština (tradiční)
-   Čínština (zjednodušená)
-   Čeština
-   Dánština
-   Nizozemština
-   Angličtina
-   Finština
-   Francouzština
-   Němčina
-   Řečtina
-   Hebrejština
-   Maďarština
-   Italština
-   Japonština
-   Korejština
-   Norština
-   Polština
-   Portugalština
-   Portugalština (Brazílie)
-   Ruština
-   Španělština
-   Švédština
-   Turečtina

### <a name="software-update-titles-and-descriptions"></a>Nadpisy a popisy aktualizace softwaru
Následující jazyky jsou podporovány pro názvy a popisy aktualizací softwaru.

-   Čínština (tradiční)
-   Čínština (zjednodušená)
-   Angličtina
-   Francouzština
-   Němčina
-   Italština
-   Japonština
-   Korejština
-   Portugalština (Brazílie)
-   Ruština
-   Španělština

## <a name="install-updates-publisher"></a>Nainstalovat Updates Publisher
Stáhněte si soubor **UpdatesPubliser. msi** pro instalaci System Center Updates Publisher z webu [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=55543).

Chcete-li nainstalovat nástroje Updates Publisher, spusťte **UpdatesPublisher. msi** na počítači, který splňuje *požadavky*. Instalační program vytvoří následující složku, která bude obsahovat soubory nezbytné ke spuštění nástroje Updates Publisher:%PROGRAMFILES%\Microsoft\UpdatesPublisher *.

Vzhledem k tomu, že tato složka obsahuje všechny soubory, které jsou nezbytné k použití nástroje Updates Publisher, můžete zkopírovat složku a její obsah do nového umístění nebo počítače a potom použít nástroje Updates Publisher z tohoto umístění. Nové umístění nebo počítač musí ale splňovat požadavky na spuštění nástroje Updates Publisher.

Po dokončení instalace spusťte **UpdatesPublisher. exe** ze složky *UpdatesPublisher* a spusťte nástroje Updates Publisher.

## <a name="next-steps"></a>Další kroky
 Po instalaci nástroje Updates Publisher doporučujeme [nakonfigurovat možnosti](updates-publisher-options.md) pro aplikaci Updates Publisher. Než budete moci použít některé funkce nástroje Updates Publisher, je nutné nakonfigurovat některé možnosti.

 Pokud ale chcete použít výchozí hodnoty a neplánujete nasadit aktualizace na server aktualizací nebo na spravovaná zařízení, můžete přejít přímo na [správu katalogů aktualizací softwaru](updates-publisher-catalogs.md)nebo [vytvořit aktualizace softwaru](create-updates-with-updates-publisher.md) a vytvořit vlastní katalogy aktualizací.
