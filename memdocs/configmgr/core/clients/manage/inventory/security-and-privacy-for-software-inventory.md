---
title: Ochrana osobních údajů zabezpečení inventáře softwaru
titleSuffix: Configuration Manager
description: Získejte informace o zabezpečení a ochraně osobních údajů pro inventář softwaru v Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8e68e1fb-a8ec-4543-bb8a-cbbaf184a418
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d64fd2ac98996a6a1ccadae78e5f9cc576b55444
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710668"
---
# <a name="security-and-privacy-for-software-inventory-in-configuration-manager"></a>Zabezpečení a ochrana osobních údajů pro inventář softwaru v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Toto téma obsahuje informace o zabezpečení a ochraně osobních údajů pro inventář softwaru v Configuration Manager.  

##  <a name="security-best-practices-for-software-inventory"></a><a name="BKMK_Security_HardwareInventory"></a> Osvědčené postupy zabezpečení pro inventář softwaru  
 Při shromažďování dat inventáře softwaru z klientů použijte následující osvědčené postupy zabezpečení:  

|Doporučené zabezpečení|Další informace|  
|----------------------------|----------------------|  
|Podepisujte a šifrujte data inventáře.|Pokud klienti komunikují s body správy pomocí protokolu HTTPS, všechna data, která odesílají, se šifrují pomocí SSL. Nicméně pokud klientské počítače používají ke komunikaci s body správy v intranetu protokol HTTP, data inventáře a shromážděné soubory klienta jde odeslat nepodepsané a nešifrované. Zkontrolujte, že lokalita je nakonfigurovaná tak, aby vyžadovala podepisování a šifrování. Pokud navíc klienti podporují algoritmus SHA-256, vyberte možnost, která SHA-256 vyžaduje.|  
|Nepoužívejte shromažďování souborů ke shromažďování důležitých souborů nebo citlivých informací.|Configuration Manager inventář softwaru používá všechna práva účtu LocalSystem, který má schopnost shromažďovat kopie důležitých systémových souborů, jako je například registr nebo databáze účtů zabezpečení. Pokud jsou tyto soubory na serveru lokality k dispozici, někdo s oprávněními Číst prostředek nebo oprávněními systému NTFS pro umístění uloženého souboru by mohl analyzovat jejich obsah a pravděpodobně rozpoznat důležité podrobnosti o klientovi, aby mohl ohrozit zabezpečení.|  
|Omezte oprávnění místního správce v klientských počítačích.|Uživatel s oprávněními místního správce může odeslat jako informace o inventáři neplatná data.|  

### <a name="security-issues-for-software-inventory"></a>Problémy se zabezpečením pro inventář softwaru  
 Shromažďování inventáře zpřístupňuje potenciální ohrožení zabezpečení. Útočníci mohou provádět následující:  

- Odeslat neplatná data, která bod správy přijme, i když je zakázané nastavení klienta inventáře softwaru a shromažďování souborů není povolené.  

- Odeslat nadměrně velké objemy dat v jednom souboru nebo v mnoha souborech, které by mohly způsobit odepření služby.  

- Přístup k informacím o inventáři při přenosu do Configuration Manager.  

  Pokud uživatelé vědí, že můžou vytvořit skrytý soubor s názvem **Skpswi.dat** a umístit ho do kořenové složky na pevném disku klienta, aby se vyloučil z inventáře softwaru, nebude možné z takového počítače shromažďovat data inventáře softwaru.  

  Vzhledem k tomu, že uživatel s oprávněními místního správce může odesílat jakékoli informace jako data inventáře, nepovažujte data inventáře, která jsou shromažďována Configuration Manager autoritativní.  

  Ve výchozím klientském nastavení je inventář softwaru povolený.  

##  <a name="privacy-information-for-software-inventory"></a><a name="BKMK_Privacy_HardwareInventory"></a> Ochrana osobních údajů pro inventář softwaru  
 Inventář hardwaru umožňuje načíst všechny informace, které jsou uložené v registru a v rozhraní WMI v Configuration Manager klientech. Inventář softwaru umožňuje vyhledat všechny soubory určitého typu nebo shromažďovat všechny zadané soubory z klientů. Funkce Asset Intelligence rozšiřuje možnosti inventáře rozšířením inventáře hardwaru a softwaru a přidáním nové funkce správy licencí.  

 Inventář hardwaru je jako nastavení klienta ve výchozím nastavení povolený a shromažďované informace rozhraní WMI se určují na základě možností, které jste vybrali. Inventář softwaru je ve výchozím povolený, ale soubory se standardně shromažďují. Shromažďování dat funkce Asset Intelligence je automaticky povolené, ale můžete vybrat, které třídy generování sestav inventáře hardwaru jsou povolené.  

 Informace o inventáři se neposílají Microsoftu. Informace o inventáři se ukládají do databáze Configuration Manager. Pokud se klienti připojují k bodům správy pomocí protokolu HTTPS, data inventáře, které posílají do lokality, jsou při přenosu šifrovaná. Pokud se klienti připojují k bodům správy pomocí protokolu HTTP, máte možnost šifrování inventáře povolit. Data inventáře v databázi nejsou uložená v šifrovaném tvaru. Informace se uchovávají v databázi do doby, než je odstraní úlohy údržby lokality **Odstranit zastaralou historii inventáře** nebo **Odstranit zastaralé shromážděné soubory** , a to každých 90 dní. Můžete provést konfiguraci intervalu odstranění.  

 Než začnete konfigurovat inventář hardwaru, inventář softwaru, shromažďování souborů nebo shromažďování dat funkce Asset Intelligence, promyslete si požadavky na ochranu osobních údajů.  
