---
title: Ochrana osobních údajů pro funkce Asset Intelligence zabezpečení
titleSuffix: Configuration Manager
description: Získejte informace o zabezpečení a ochraně osobních údajů pro funkce Asset Intelligence v Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d0c6f7a0-dcae-4e6d-aa28-35d464d97ff7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3cf35b050b110c655ac85e82a7990f9ea2ac3636
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714140"
---
# <a name="security-and-privacy-for-asset-intelligence-in-configuration-manager"></a>Zabezpečení a ochrana osobních údajů pro funkce Asset Intelligence v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Toto téma obsahuje informace o zabezpečení a ochraně osobních údajů pro funkce Asset Intelligence v Configuration Manager.  

##  <a name="security-best-practices-for-asset-intelligence"></a><a name="BKMK_Security_AI"></a> Osvědčené postupy zabezpečení pro funkci Asset Intelligence  
 Při použití funkce Asset Intelligence použijte následující osvědčené postupy zabezpečení:  

|Doporučené zabezpečení|Další informace|  
|----------------------------|----------------------|  
|Při importu souboru s licencí (soubor multilicenčního programu Microsoftu nebo soubor obecné licenční smlouvy) zabezpečte soubor a komunikační kanál.|Pomocí oprávnění systému souborů NTFS zajistěte, že možnost přístupu k souborům s licencí a použití podepisování bloků SMB (Server Message Block) k zajištění integrity dat při přenosu na server lokality během procesu importu mají jenom oprávnění uživatelé.|  
|Při importu souborů s licencí použijte zásadu co nejmenších oprávnění.|K udělení oprávnění Spravovat funkce Asset Intelligence administrativnímu uživateli, který importuje soubory s licencí, použijte správu na základě rolí. Toto oprávnění zahrnuje předdefinovaná role Správce inventáře.|  

##  <a name="privacy-information-for-asset-intelligence"></a><a name="BKMK_Privacy_HardwareInventory"></a> Ochrana osobních údajů pro funkci Asset Intelligence  
 Funkce Asset Intelligence rozšiřuje možnosti inventáře Configuration Manager, aby poskytovaly vyšší úroveň viditelnosti prostředků v podniku. Shromažďování informací funkce Asset Intelligence není povolené automaticky. Můžete změnit typ shromažďovaných informací povolením tříd generování sestav inventáře hardwaru. Další informace najdete v tématu [konfigurace funkce Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Informace funkce Asset Intelligence jsou uloženy v databázi Configuration Manager stejným způsobem jako informace o inventáři. Pokud se klienti připojují k bodům správy pomocí protokolu HTTPS, data jsou při přenosu do bodu správy vždycky šifrovaná. Pokud se klienti připojují pomocí protokolu HTTP, můžete nakonfigurovat, aby byl přenos dat inventáře podepsaný a zašifrovaný. Data inventáře v databázi nejsou uložená v šifrovaném tvaru. Informace se uchovávají v databázi, dokud je úloha správy lokality **Odstranit zastaralou historii inventáře** neodstraní po každých 90 dnech. Můžete provést konfiguraci intervalu odstranění.  

 Funkce Asset Intelligence neodesílá společnosti Microsoft informace o uživatelích a počítačích nebo využívání licence. Můžete zvolit odeslání požadavků System Center Online na kategorizaci, což znamená, že můžete označit jeden nebo několik softwarových titulů, které jsou bez kategorie, a odeslat je do katalogu System Center Online ke zkoumání a kategorizaci. Po odeslání softwarového titulu výzkumníci Microsoftu označí, roztřídí a poté zpřístupní dané znalosti všem zákazníkům, kteří používají online službu. Při odeslání informací do katalogu System Center Online byste si měli být vědomi následujících dopadů na ochranu osobních údajů:  

- Odesílání se týká jenom obecných informací o softwarovém titulu (název, vydavatel a podobně), které vyberte, aby se odesílaly do katalogu System Center Online. Informace o inventáři nejsou v odesílání zahrnuté.  

- Odesílání se nikdy neprovádí automaticky a systém není nastavený na automatizaci tohoto úkolu. Je třeba ručně vybrat a ověřit odeslání každého softwarového titulu.  

- Dialogové okno zobrazí přesně, jaká data se budou odesílat, předtím než se proces odesílání spustí.  

- Informace o licenci se Microsoftu neposílají. Informace o licenci jsou uložené v samostatné oblasti databáze Configuration Manager a nelze je odeslat do společnosti Microsoft.  

- Libovolný odeslaný softwarový titul se stává veřejným v tom smyslu, že znalosti o dané aplikaci a její zatřídění se stávají součástí katalogu System Center Online Asset Intelligence a že je pak jde stáhnout dalšími uživateli katalogu.  

- Zdroj softwarového titulu se v katalogu Asset Intelligence nezaznamená a není dostupný ostatním zákazníkům. Pořád ale musíte ověřovat, že neodesíláte žádné aplikační tituly, které obsahují nějaké soukromé informace.  

- Odeslaná data nelze zrušit.  

  Než nakonfigurujete shromažďování dat funkce Asset Intelligence a rozhodnete, jestli budete odesílat informace do katalogu System Center Online, zvažte požadavky vaší organizace na ochranu osobních údajů.  
