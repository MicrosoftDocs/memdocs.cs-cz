---
title: Soukromí zabezpečení inventáře hardwaru
titleSuffix: Configuration Manager
description: Získejte informace o zabezpečení a ochraně osobních údajů pro inventář hardwaru v Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 62e20d86-db6d-4a1f-b14a-905a9de31698
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a5989c80818ac45bb8dd6a4f768595dbd56b846d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710682"
---
# <a name="security-and-privacy-for-hardware-inventory-in-configuration-manager"></a>Zabezpečení a ochrana osobních údajů pro inventář hardwaru v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Toto téma obsahuje informace o zabezpečení a ochraně osobních údajů pro inventář hardwaru v Configuration Manager.  

##  <a name="security-best-practices-for-hardware-inventory"></a><a name="BKMK_Security_HardwareInventory"></a> Osvědčené postupy zabezpečení pro inventář hardwaru  
 Při shromažďování dat inventáře hardwaru z klientů použijte následující osvědčené postupy zabezpečení:  

|Doporučené zabezpečení|Další informace|  
|----------------------------|----------------------|  
|Podepisujte a šifrujte data inventáře.|Pokud klienti komunikují s body správy pomocí protokolu HTTPS, všechna data, která odesílají, se šifrují pomocí SSL. Nicméně pokud klientské počítače používají ke komunikaci s body správy v intranetu protokol HTTP, data inventáře a shromážděné soubory klienta jde odeslat nepodepsané a nešifrované. Zkontrolujte, že lokalita je nakonfigurovaná tak, aby vyžadovala podepisování a šifrování. Pokud navíc klienti podporují algoritmus SHA-256, vyberte možnost, která SHA-256 vyžaduje.|  
|Nezískávat soubory IDMIF a NOIDMIF v prostředích s vysokými nároky na zabezpečení|Shromažďování souborů IDMIF a NOIDMIF můžete využít k rozšíření kolekce inventáře hardwaru. V případě potřeby Configuration Manager vytvoří nové tabulky nebo upraví existující tabulky v databázi Configuration Manager tak, aby vyhovovaly vlastnostem v souborech IDMIF a NOIDMIF. Configuration Manager ale neověřuje soubory IDMIF a NOIDMIF, takže tyto soubory se dají použít ke změně tabulek, které nechcete měnit. Platná data se můžou přepsat neplatnými daty. Kromě toho je možné přidat velké objemy dat a zpracování těchto dat může způsobit zpoždění ve všech Configuration Manager funkcích. Pokud chcete toto riziko omezit, nakonfigurujte nastavení klienta inventáře hardwaru **Shromáždit soubory MIF** na **Žádné**.|  

### <a name="security-issues-for-hardware-inventory"></a>Problémy se zabezpečením pro inventář hardwaru  
 Shromažďování inventáře zpřístupňuje potenciální ohrožení zabezpečení. Útočníci mohou provádět následující:  

- Odeslat neplatná data, která bod správy přijme, i když je zakázané nastavení klienta inventáře softwaru a shromažďování souborů není povolené.  

- Odeslat nadměrně velké objemy dat v jednom souboru nebo v mnoha souborech, které by mohly způsobit odepření služby.  

- Přístup k informacím o inventáři při přenosu do Configuration Manager.  

  Vzhledem k tomu, že uživatel s oprávněními místního správce může odesílat jakékoli informace jako data inventáře, nepovažujte data inventáře, která jsou shromažďována Configuration Manager autoritativní.  

  Ve výchozím klientském nastavení je inventář hardwaru povolený.  

##  <a name="privacy-information-for-hardware-inventory"></a><a name="BKMK_Privacy_HardwareInventory"></a> Ochrana osobních údajů pro inventář hardwaru  
 Inventář hardwaru umožňuje načíst všechny informace, které jsou uložené v registru a v rozhraní WMI v Configuration Manager klientech. Inventář softwaru umožňuje vyhledat všechny soubory určitého typu nebo shromažďovat všechny zadané soubory z klientů. Funkce Asset Intelligence rozšiřuje možnosti inventáře rozšířením inventáře hardwaru a softwaru a přidáním nové funkce správy licencí.  

 Inventář hardwaru je jako nastavení klienta ve výchozím nastavení povolený a shromažďované informace rozhraní WMI se určují na základě možností, které jste vybrali. Inventář softwaru je ve výchozím povolený, ale soubory se standardně shromažďují. Shromažďování dat funkce Asset Intelligence je automaticky povolené, ale můžete vybrat, které třídy generování sestav inventáře hardwaru jsou povolené.  

 Informace o inventáři se neposílají Microsoftu. Informace o inventáři se ukládají do databáze Configuration Manager. Pokud se klienti připojují k bodům správy pomocí protokolu HTTPS, data inventáře, které posílají do lokality, jsou při přenosu šifrovaná. Pokud se klienti připojují k bodům správy pomocí protokolu HTTP, máte možnost šifrování inventáře povolit. Data inventáře v databázi nejsou uložená v šifrovaném tvaru. Informace se uchovávají v databázi do doby, než je odstraní úlohy údržby lokality **Odstranit zastaralou historii inventáře** nebo **Odstranit zastaralé shromážděné soubory** , a to každých 90 dní. Můžete provést konfiguraci intervalu odstranění.  

 Než začnete konfigurovat inventář hardwaru, inventář softwaru, shromažďování souborů nebo shromažďování dat funkce Asset Intelligence, promyslete si požadavky na ochranu osobních údajů.  
