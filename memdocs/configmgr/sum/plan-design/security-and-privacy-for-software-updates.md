---
title: Zabezpečení a ochrana osobních údajů pro aktualizace softwaru
titleSuffix: Configuration Manager
description: Použijte tyto osvědčené postupy pro zabezpečení aktualizací softwaru a Naučte se, jak Configuration Manager zpracovává informace o ochraně osobních údajů.
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 41d6d5d8-ba84-4efb-b105-4d1eed239824
author: mestew
ms.author: mstewart
ms.openlocfilehash: 5c7a1ac5e88aa669ae1d5e6bb9333e1f54fb5980
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724003"
---
# <a name="security-and-privacy-for-software-updates-in-configuration-manager"></a>Zabezpečení a ochrana osobních údajů pro aktualizace softwaru v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Toto téma obsahuje informace o zabezpečení a ochraně osobních údajů pro aktualizace softwaru v nástroji Configuration Manager.  

##  <a name="security-best-practices-for-software-updates"></a><a name="BKMK_Security_HardwareInventory"></a> Osvědčené postupy zabezpečení pro aktualizace softwaru  
 Při nasazování aktualizací softwaru do klientů používejte následující osvědčené postupy zabezpečení:  

-   Neměňte výchozí oprávnění u balíčků aktualizací softwaru.  

     Výchozí oprávnění je u balíčků aktualizací softwaru nastaveno na úroveň **Úplné řízení** pro správce a na úroveň **Číst** pro uživatele. Změna těchto oprávnění může případnému útočníkovi umožnit přidání, odebrání nebo odstranění aktualizací softwaru.  

-   Zajistěte řízení přístupu k umístění pro stahování aktualizací softwaru.  

     Účty počítačů poskytovatele služby SMS, serveru lokality a správce, který bude skutečně stahovat aktualizace softwaru do umístění pro stahování, vyžadují pro toto umístění úroveň přístupu **Zapisovat** . Omezením přístupu k umístění pro stahování snížíte riziko manipulace se zdrojovými soubory aktualizací softwaru v tomto umístění ze strany případných útočníků.  

     Pokud používáte jako umístění pro stahování sdílenou složku UNC, zabezpečte dále síťový kanál protokolem IPsec nebo podepisováním SMB. Zabráníte tak možné manipulaci se zdrojovými soubory aktualizací softwaru při jejich přenosu v síti.  

-   Při vyhodnocování časů nasazení používejte světový čas (UTC).  

     Pokud místo světového času použijete místní čas, uživatelé by teoreticky mohli oddalovat instalaci aktualizací softwaru změnou časového pásma ve svých počítačích.  

-   Povolte protokol SSL u služby WSUS a použijte osvědčené postupy zabezpečení služby WSUS (Windows Server Update Services).  

     Identifikujte a dodržujte osvědčené postupy zabezpečení pro verzi služby WSUS, kterou používáte s Configuration Manager.  

    > [!IMPORTANT]  
    >  Pokud nastavíte bod aktualizace softwaru, aby při komunikaci se serverem služby WSUS používal protokol SSL, musíte na serveru služby WSUS nastavit virtuální kořeny pro protokol SSL.  

-   Zapněte kontrolu seznamu CRL.  

     Ve výchozím nastavení Configuration Manager nekontroluje seznam odvolaných certifikátů (CRL), aby ověřil podpis na aktualizacích softwaru před jejich nasazením do počítačů. Kontrola seznamu CRL pokaždé, když je certifikát použit, poskytuje lepší zabezpečení proti použití certifikátu, který byl zrušen, ale představuje zpoždění připojení a má za následek další zpracování na počítači provádějícím kontrolu seznamu CRL.  

     Další informace o tom, jak povolit kontrolu CRL pro aktualizace softwaru, najdete v tématu [Jak povolit kontrolu CRL pro aktualizace softwaru](../get-started/manage-settings-for-software-updates.md#crl-checking-for-software-updates).  

-   Nastavte službu WSUS, aby používala vlastní web.  

     Při instalaci služby WSUS v bodě aktualizace softwaru je možné použít existující výchozí web služby IIS nebo vytvořit vlastní web služby WSUS. Vytvořte vlastní web pro server WSUS, aby služba IIS byla hostitelem služeb WSUS ve vyhrazeném virtuálním webu místo sdílení stejného webu, který používají jiné systémy lokality Configuration Manager nebo jiné aplikace.  

     Další informace naleznete v části [Configure WSUS to use a custom web site](plan-for-software-updates.md#BKMK_CustomWebSite).  

##  <a name="privacy-information-for-software-updates"></a><a name="BKMK_Privacy_HardwareInventory"></a>Informace o ochraně osobních údajů pro aktualizace softwaru  
 Aktualizace softwaru prohledávají klientské počítače a zjišťují, jaké aktualizace softwaru potřebujete. Tyto informace pak odesílají zpět do databáze lokality. Během procesu aktualizace softwaru Configuration Manager může přenášet informace mezi klienty a servery, které identifikují počítač a účty přihlášení.  

 Configuration Manager udržuje informace o stavu procesu nasazení softwaru. Informace nejsou při přenosu a uchovávání šifrovány. Informace o stavu jsou uloženy v databázi Configuration Manager a jsou odstraněny úlohami údržby databáze. Žádné informace o stavu nejsou odesílány společnosti Microsoft.  

 Použití Configuration Manager aktualizací softwaru k instalaci aktualizací softwaru do klientských počítačů může podléhat licenčním podmínkám pro tyto aktualizace, které jsou oddělené od licenčních podmínek k softwaru pro Configuration Manager. Před instalací aktualizací softwaru pomocí Configuration Manager vždy přečtěte licenční podmínky pro software a souhlasím s nimi.  

 Configuration Manager ve výchozím nastavení neimplementuje aktualizace softwaru a před shromažďováním informací vyžaduje několik kroků konfigurace.  

 Před konfigurací aktualizací softwaru zvažte své požadavky na ochranu osobních údajů.  
