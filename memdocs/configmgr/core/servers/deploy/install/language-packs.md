---
title: Jazykové sady
titleSuffix: Configuration Manager
description: Přečtěte si o podpoře jazyků dostupné v Configuration Manager.
ms.date: 06/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ec5581567925ee57300274e50288058e06d80ec0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718186"
---
# <a name="language-packs-in-configuration-manager"></a>Jazykové sady v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek poskytuje technické podrobnosti o podpoře jazyků v Configuration Manager. Servery lokalit a klienti se Configuration Manager považují za jazykově neutrální. Přidání podpory pro jazyky zobrazení instalací **jazykových sad serveru** nebo **jazykových sad klienta** v lokalitě centrální správy a v primárních lokalitách. V rámci procesu instalace lokality vyberete jazyky serveru a klienta, které se budou podporovat v lokalitě, od dostupných souborů jazykové sady.
 
Nainstalujte několik jazyků do každé lokality. Stačí jenom nainstalovat používané jazyky.  

- Každá lokalita podporuje několik jazyků pro Configuration Manager konzoly.  

- Přidejte podporu pouze pro jazyky klienta, které chcete podporovat, instalací jednotlivých jazykových sad klienta v každé lokalitě.  

Když instalujete podporu pro jazyk, který odpovídá následujícím součástem:  

- Jazyk zobrazení počítače: konzola Configuration Manager a uživatelské rozhraní klienta, které běží na tomto počítači, zobrazuje informace v tomto jazyce.  

- Jazykové předvolby používané webovým prohlížečem počítače: připojení k webovým informacím, včetně katalogu aplikací nebo SQL Server Reporting Services, se zobrazí v daném jazyce.  


Když spustíte instalační program Configuration Manager, stáhne se soubory jazykové sady jako součást požadavků a distribuovatelných souborů. Ke stažení těchto souborů před spuštěním instalace můžete použít také nástroj pro stažení [instalačního programu](setup-downloader.md) .   



## <a name="server-languages"></a>Jazyky serveru  

Pomocí následující tabulky namapujte ID národního prostředí na jazyk, který chcete podporovat na serverech. Další informace o ID národních prostředí najdete v tématu [ID národního prostředí přiřazené společností Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=252609).  

|Jazyk serveru|ID národního prostředí (LCID)|Kód se třemi písmeny|  
|---------------------|------------------------|-----------------------|  
|Angličtina (výchozí)|0409|ENU|  
|Čínština (zjednodušená)|0804|CHS|  
|Čínština (tradiční, Tchaj-wan)|0404|CHT|  
|Čeština|0405|CSY|  
|Nizozemština – Nizozemsko|0413|NLD|  
|Francouzština|040c|FRA|  
|Němčina|0407|DEU|  
|Maďarština|040e|HUN|  
|Italština – Itálie|0410|ITA|  
|Japonština|0411|JPN|  
|Korejština|0412|KOR|  
|Polština|0415|PLK|  
|Portugalština – Brazílie|0416|PTB|  
|Portugalština – Portugalsko|0816|PTG|  
|Ruština|0419|RUS|  
|Španělština – Španělsko|0c0a|ESN|  
|Švédština|041d|SVE|  
|Turečtina|041f|TRK|  



## <a name="client-languages"></a>Jazyky klienta  

Pomocí následující tabulky namapujte ID národního prostředí na jazyk, který chcete podporovat na klientských počítačích. Další informace o ID národních prostředí najdete v tématu [ID národního prostředí přiřazené společností Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=252609).  

|Jazyk klienta|ID národního prostředí (LCID)|Kód se třemi písmeny|  
|---------------------|------------------------|-----------------------|  
|Angličtina (výchozí)|0409|CZE|  
|Čínština – zjednodušená|0804|CHS|  
|Čínština (tradiční, Tchaj-wan)|0404|CHT|  
|Čeština|0405|CSY|  
|Dánština|0406|DAN|  
|Nizozemština – Nizozemsko|0413|NLD|  
|Finština|040b|FIN|  
|Francouzština|040c|FRA|  
|Němčina|0407|DEU|  
|Řečtina|0408|ELL|  
|Maďarština|040e|HUN|  
|Italština – Itálie|0410|ITA|  
|Japonština|0411|JPN|  
|Korejština|0412|KOR|  
|Norština|0414|NOR|  
|Polština|0415|PLK|  
|Portugalština (Brazílie)|0416|PTB|  
|portugalština (Portugalsko)|0816|PTG|  
|Ruština|0419|RUS|  
|Španělština – Španělsko|0c0a|ESN|  
|Švédština|041d|SVE|  
|Turečtina|041f|TRK|  


### <a name="mobile-device-client-languages"></a>Jazyky klienta mobilního zařízení  
Když přidáte podporu pro jazyky mobilních zařízení, budou zahrnuty všechny podporované jazyky klientů mobilních zařízení. Nemůžete vybrat jednotlivé jazykové sady pro podporu mobilních zařízení.  



## <a name="identify-installed-language-packs"></a>Identifikace nainstalovaných jazykových sad  
Chcete-li určit jazykové sady, které jsou nainstalovány v počítači, na kterém je spuštěn klient Configuration Manager, vyhledejte ID národního prostředí (LCID) nainstalovaných jazykových sad v registru počítače. Tyto informace jsou k dispozici v následující cestě k registru:  

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs`  

Přizpůsobení inventáře hardwaru pro shromažďování těchto informací. Pak vytvořte vlastní sestavu pro zobrazení podrobností o jazyce. Další informace o shromažďování vlastního inventáře hardwaru najdete v tématu [Konfigurace inventáře hardwaru](../../../clients/manage/inventory/configure-hardware-inventory.md). Další informace najdete v tématu [vytváření sestav](../../manage/operations-and-maintenance-for-reporting.md#create-reports).
