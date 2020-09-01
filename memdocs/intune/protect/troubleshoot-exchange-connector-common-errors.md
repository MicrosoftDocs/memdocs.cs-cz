---
title: Řešení běžných chyb pro Intune Exchange Connector
titleSuffix: Microsoft Intune
description: Řešení a řešení běžných chyb pro místní Microsoft Intune Exchange Connector
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cea8981b9fdd16e0d8da9dd36445b8fbdfe3d53f
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193942"
---
# <a name="resolve-common-errors-for-the-intune-exchange-connector"></a>Řešení běžných chyb pro Intune Exchange Connector

Tento článek vám může pomáhat správci Intune vyřešit konkrétní chyby a zprávy týkající se operace Intune Exchange Connectoru.  

## <a name="configuration-failed-and-returned-error-code-0x0000001"></a>Konfigurace se nezdařila a vrátila kód chyby 0x0000001

**Problém**:  
Při pokusu o konfiguraci Microsoft Intune Exchange Connector se zobrazí následující chybová zpráva:

```
   The Microsoft Intune Exchange Connector cannot connect to the Microsoft Exchange server.  
   The following Microsoft Exchange Server address could not be reached <Exchange server Name FQDN>  
   Verify that the FQDN of the exchange server address and credentials that you entered is correct and the server is running. The Microsoft Intune Exchange Connector does not support Exchange server arrays.  
   Error code: 0x0000001  
```

K tomuto problému může dojít, pokud jsou nastavení internetového proxy serveru chybně nakonfigurované.

**Řešení**:  
Konfigurovat nastavení proxy serveru:
1. Obraťte se na správce místní sítě, abyste se ujistili, že je správně nakonfigurované nastavení proxy serveru. 
2. Pomocí příkazu **netsh WinHTTP** Nakonfigurujte proxy server a přidejte požadovaný seznam vyloučení. Příklad:  

   ```
   Netsh winhttp set proxy proxy-server="http=proxy.corp.domain.com" bypass-list"34*.*;134.132.*.*;10.*.*;localhost;*.corp.domain.com;*.staging.domain.com"
   ```

## <a name="configuration-failed-and-returned-error-code-0x000000b"></a>Konfigurace se nezdařila a vrátila kód chyby 0x000000b   

**Problém**:  
Při pokusu o konfiguraci Microsoft Intune Exchange Connector se zobrazí následující chybová zpráva:  

```
   The Microsoft Intune Exchange Connector experienced an error:  
   CertEnroll::CX509PrivateKey::Create: The system cannot find the file specified. 0x80070002 (WIN32: 2  
   ERROR_FILE_NOT_FOUND  
   Error code: 0x000000b  
```
K tomuto problému může dojít, pokud účet, který jste použili k přihlášení do Intune, není účet globálního správce Intune.

**Řešení**:  
Přihlaste se k Intune pomocí účtu, který je globálním správcem, nebo přidejte svůj účet do globální skupiny správců. Další informace najdete v tématu [řízení správy na základě rolí (RBAC) s Microsoft Intune](../fundamentals/role-based-access-control.md).

## <a name="configuration-failed-and-returned-error-code-0x0000006"></a>Konfigurace se nezdařila a vrátila kód chyby 0x0000006

**Problém**:  
Při pokusu o konfiguraci Microsoft Intune Exchange Connector se zobrazí následující chybová zpráva:  

```  
   The Microsoft Intune Exchange Connector cannot connect to Microsoft Intune  
   Verify that you are connected to the Internet, check the Microsoft Intune Service Status, and try to connect again.  
   Error code: 0x00000006  
```  
K této chybě může dojít, pokud proxy server slouží k připojení k Internetu a blokuje provoz do služby Intune. Pokud chcete zjistit, jestli se proxy používá, přejděte na **Ovládací panely**  >  **Možnosti Internetu**, vyberte kartu **připojení** a pak klikněte na **Nastavení místní sítě**.

**Řešení**:  

- **Možnost 1** – odeberte nastavení proxy serveru, aby se počítač mohl připojit k Internetu bez průchodu proxy serverem.  

- **Možnost 2** – Nakonfigurujte proxy server, aby bylo možné komunikovat se službou Intune, jak je uvedeno v [požadavcích Intune Exchange Connectoru](exchange-connector-install.md#intune-exchange-connector-requirements).



## <a name="event-7000-or-7041-microsoft-intune-exchange-connector-service-wont-start"></a>Událost 7000 nebo 7041: Služba Microsoft Intune Exchange Connector se nespustí

**Problém**:  
Nepovedlo se zaregistrovat zařízení s iOS v Intune a vygeneruje se jedna z těchto chybových zpráv:  

```  
   Log Name:      System
   Source:            Service Control Manager
   Date:               <time>
   Task Category: None
   Level:               Error
   Keywords:        Classic
   User:                N/A
   Computer:      <computer>
   Description:
   The Microsoft Intune Exchange Connector Service service failed to start because of the following error:  
   The service did not start because of a logon failure.
```  

```  
   Log Name:      System
   Source:            Service Control Manager
   Date:               <time>
   Event ID:          7041
   Task Category: None
   Level:               Error   
   Keywords:        Classic
   User:                N/A
   Computer:       <computer>
   Description:
   The WIEC service was unable to log on as .\WIEC_USER with the currently configured password because of the following error:
   Logon failure: the user has not been granted the requested logon type at this computer.
   Service: WIEC
   Domain and account: .\WIEC_USER
   This service account does not have the required user right "Log on as a service."  
```
K tomuto problému může dojít, pokud účet **WIEC_User** nemá uživatelské právo **Přihlásit se jako služba** v místních zásadách.

**Řešení**:  
V počítači, na kterém běží Intune Exchange Connector, přiřaďte uživatelské právo **Přihlásit se jako služba** k účtu služby **WIEC_User** . Pokud je počítač uzlem v clusteru, nezapomeňte účtu Clusterové služby na všech uzlech v clusteru přiřadit uživatelské právo *Přihlásit se jako služba* .  

Chcete-li přiřadit uživatelské právo **Přihlásit se jako služba** k účtu služby **WIEC_User** v počítači, postupujte podle následujících kroků:

1. Přihlaste se k počítači jako správce nebo jako člen skupiny Administrators.
2. Spusťte **secpol. msc** a otevřete tak místní zásady zabezpečení.
3. Přejít na **nastavení zabezpečení**  >  **místní zásady**a potom vyberte **přiřazení uživatelských práv**.
4. V pravém podokně klikněte dvakrát na možnost **Přihlásit se jako služba**.
5. Vyberte **Přidat uživatele nebo skupinu**, přidejte **WIEC_USER** k zásadě a pak vyberte **OK** dvakrát.

Pokud byla uživatelská práva **Přihlásit se jako služba** přiřazena **WIEC_User** , ale později byla odebrána, požádejte správce domény, aby určil, zda nastavení zásady skupiny Přepisuje.  

## <a name="next-steps"></a>Další kroky  

Následující článek vám může pomáhat vyřešit konkrétní chyby:
- [Řešení běžných problémů s Intune Exchange Connectorem](troubleshoot-exchange-connector-common-problems.md). Git 

Vyhledejte pomoc od podpory nebo komunity Intune.
- V tématu [získání podpory](../fundamentals/get-support.md) pro používání konzoly Intune můžete pomoct s řešením problému nebo otevřít případ podpory s Microsoftem. 
- Vystavte svůj problém ve [fórech Microsoft Intune](/answers/products/mem).