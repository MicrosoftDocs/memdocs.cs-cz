---
title: Přehled certifikátů CNG
titleSuffix: Configuration Manager
description: Přečtěte si o podpoře certifikátů kryptografických služeb nové generace (CNG) pro Configuration Manager klienty a servery.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dba904ae-7c44-46db-ae63-999b9821cb46
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 191325d05ccc23a4f07d8b39f7927c2b2e543f41
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692651"
---
# <a name="cng-certificates-overview"></a>Přehled certifikátů CNG
<!-- 1356191 --> 

Configuration Manager má omezené podpory pro certifikáty Cryptography: Next Generation (CNG). Klienti služby Configuration Manager můžou používat certifikát ověřování klientů PKI s privátním klíčem v CNG (klíč úložiště klíčů). S podporou KSP Configuration Manager klienti podporují privátní klíč založený na hardwaru, jako je například KSP čipu TPM pro certifikáty ověřování klientů PKI.

## <a name="supported-scenarios"></a>Podporované scénáře
Šablony certifikátů [kryptografických rozhraní API nové generace (CNG)](/windows/win32/seccng/cng-features) můžete použít pro následující scénáře:

- Registrace a komunikace klienta s bodem správy HTTPS   
- Distribuce softwaru a nasazení aplikací s distribučním bodem HTTPS   
- Nasazení operačního systému  
- Sada SDK pro zasílání zpráv klienta (s nejnovější aktualizací) a ISV proxy   
- Konfigurace Brána pro správu cloudu  

Počínaje verzí 1802 použijte certifikáty CNG pro následující role serveru s podporou protokolu HTTPS: <!-- 1357314 -->   
- Bod správy
- Distribuční bod
- Bod aktualizace softwaru
- Bod migrace stavu     

Počínaje verzí 1806 použijte certifikáty CNG pro následující role serveru s podporou protokolu HTTPS:

- Bod registrace certifikátu, včetně serveru NDES, s modulem zásad Configuration Manager <!--1357314-->

> [!NOTE]
> CNG je zpětně kompatibilní s kryptografickým rozhraním API (CAPI). Certifikáty rozhraní CAPI jsou nadále podporovány i v případě, že je na klientovi povolena podpora CNG.

## <a name="unsupported-scenarios"></a>Nepodporované scénáře

V současné době nejsou podporovány následující scénáře:

- Následující role serveru nejsou funkční, když jsou nainstalovány v režimu HTTPS s certifikátem CNG vázaným na web v Internetová informační služba (IIS): 
    - Webová služba Application Catalog
    - Web katalogu aplikací
    - Bod registrace  
    - Zprostředkující bod registrace  

- Centrum softwaru nezobrazuje aplikace a balíčky jako dostupné, které jsou nasazené do kolekcí skupin uživatelů nebo uživatelů.

- Vytvoření distribučního bodu cloudu pomocí certifikátů CNG

- Pokud modul zásad NDES používá pro ověřování klientů certifikát CNG, komunikace s bodem registrace certifikátu se nezdařila. 
    - To se podporuje od verze Configuration Manager 1806.

- Pokud při vytváření média pořadí úloh zadáte certifikát CNG, průvodce se nedokáže vytvořit spouštěcí médium.
    - To se podporuje od verze Configuration Manager 1806.

## <a name="to-use-cng-certificates"></a>Používání certifikátů CNG

K používání certifikátů CNG musí vaše certifikační autorita (CA) poskytovat šablony certifikátů CNG pro cílové počítače. Podrobnosti o šabloně se liší v závislosti na scénáři. jsou však požadovány následující vlastnosti:

- Karta **Kompatibilita**

    - **Certifikační autorita** musí být Windows Server 2008 nebo novější. (Doporučuje se Windows Server 2012.)

    - **Příjemce certifikátu** musí být Windows Vista/Server 2008 nebo novější. (Doporučuje se Windows 8/Windows Server 2012.)

- Karta **kryptografie**

    - **Kategorie poskytovatele** musí být **poskytovatelem úložiště klíčů**. požadovanou
    - **Požadavek musí používat jednoho z následujících zprostředkovatelů:** musí být **poskytovatelem úložiště klíčů od Microsoftu**. 

> [!NOTE]
> Požadavky na vaše prostředí nebo organizaci se můžou lišit. Obraťte se na svého odborníka PKI. Důležitým bodem, který je třeba zvážit, je, že šablona certifikátu musí používat poskytovatele úložiště klíčů k využití CNG.

Pro dosažení nejlepších výsledků doporučujeme sestavit název subjektu z informací služby Active Directory. Pro **Formát názvu subjektu** použijte název DNS a do alternativního názvu subjektu zadejte název DNS. V opačném případě je nutné poskytnout tyto informace, když se zařízení zaregistruje do profilu certifikátu.