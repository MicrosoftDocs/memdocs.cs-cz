---
title: Metody instalace klienta
titleSuffix: Configuration Manager
description: Přečtěte si informace o metodách instalace klienta Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d5f238ddb0e2c28a51cdad8dc7347f872227535
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713307"
---
# <a name="client-installation-methods-in-configuration-manager"></a>Metody instalace klienta v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

K instalaci Configuration Managerho klientského softwaru můžete použít různé metody. Použijte jednu metodu nebo kombinaci metod. Tento článek popisuje jednotlivé metody, takže můžete zjistit, které z nich nejlépe vyhovuje vaší organizaci.  

## <a name="client-push-installation"></a>Klientská nabízená instalace  

**Podporovaná klientská platforma**: Windows  

#### <a name="advantages"></a>Výhody  

-   Lze ji použít k instalaci klienta do jednoho počítače, kolekce počítačů nebo do výsledků dotazu.  

-   Lze ji použít k automatické instalaci klienta do všech zjištěných počítačů.  

-   Automaticky použije vlastnosti instalace klienta definované na kartě **Klient** v dialogovém okně **Vlastnosti klientské nabízené instalace**.  

#### <a name="disadvantages"></a>Nevýhody  

-   Při nabízení do rozsáhlých kolekcí může způsobit intenzivní síťový provoz.  

-   Lze ji použít pouze v počítačích, které byly zjištěny Configuration Manager.  

-   Nelze ji použít k instalaci klientů v pracovní skupině.  

-   Je nutné zadat účet klientské nabízené instalace, který má oprávnění správce pro určený klientský počítač.  

-   Brána Windows Firewall musí být nakonfigurovaná s výjimkami na klientských počítačích.   

-   Nemůžete zrušit nabízenou instalaci klienta. Configuration Manager se pokusí nainstalovat klienta do všech zjištěných prostředků. Opakuje všechny chyby po dobu až sedmi dnů.  

Další informace najdete v tématu [instalace klientů pomocí klientské nabízené instalace](../deploy-clients-to-windows-computers.md#BKMK_ClientPush).  



## <a name="software-update-point-based-installation"></a>Instalace aktualizace softwaru z bodu  

**Podporovaná klientská platforma**: Windows  

#### <a name="advantages"></a>Výhody  

-   Může použít existující infrastrukturu aktualizací softwaru ke správě klientského softwaru.  

-   Pokud je nastavení Windows Server Update Services (WSUS) a zásad skupiny v Active Directory Domain Services správně nakonfigurované, může klientský software automaticky nainstalovat na nové počítače.  

-   Nepožaduje, aby byly zjištěny počítače, aby bylo možné nainstalovat klienta.  

-   Počítače mohou přečíst vlastnosti instalace klienta, které byly publikovány ve službě Active Directory Domain Services.  

-   Pokud se klient odebere, tato metoda ho znovu nainstaluje.  

-   Nevyžaduje konfiguraci a údržbu účtu instalace pro určený klientský počítač.  

#### <a name="disadvantages"></a>Nevýhody  

-   Požadovanou součástí je funkční infrastruktura aktualizací softwaru.  

-   Musí používat stejný server pro instalaci klienta a aktualizace softwaru. Tento server se musí nacházet v primární lokalitě.  

-   Chcete-li nainstalovat nové klienty, je nutné nakonfigurovat objekt zásad skupiny v Active Directory Domain Services s aktivním bodem a portem aktualizace softwaru klienta.  

-   Pokud není schéma služby Active Directory rozšířeno pro Configuration Manager, je nutné pomocí nastavení zásad skupiny zřídit počítače s vlastnostmi instalace klienta.  

Další informace najdete v tématu [instalace klientů pomocí instalace na základě aktualizace softwaru](../deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  



## <a name="group-policy-installation"></a>Instalace zásad skupiny  

**Podporovaná klientská platforma**: Windows  

#### <a name="advantages"></a>Výhody  

-   Nepožaduje, aby byly zjištěny počítače, aby bylo možné nainstalovat klienta.  

-   Lze ji použít pro nové instalace klientů a pro upgrade.  

-   Počítače mohou přečíst vlastnosti instalace klienta, které byly publikovány ve službě Active Directory Domain Services.  

-   Nevyžaduje konfiguraci a údržbu účtu instalace pro určený klientský počítač.  

#### <a name="disadvantages"></a>Nevýhody  

-   Pokud se instaluje velký počet klientů, může to způsobit velký síťový provoz.  

-   Pokud není schéma služby Active Directory rozšířeno pro Configuration Manager, je nutné použít nastavení zásad skupiny k přidání vlastností instalace klienta do počítačů ve vaší lokalitě.  

Další informace najdete v tématu [Postup instalace klientů pomocí zásad skupiny](../deploy-clients-to-windows-computers.md#BKMK_ClientGP).  



## <a name="logon-script-installation"></a>Instalace skriptu přihlášení  

**Podporovaná klientská platforma**: Windows  

#### <a name="advantages"></a>Výhody  

-   Nepožaduje, aby byly zjištěny počítače, aby bylo možné nainstalovat klienta.  

-   Podporuje používání vlastností příkazového řádku služby CCMSetup.  

#### <a name="disadvantages"></a>Nevýhody  

-   Pokud se v krátkém časovém intervalu instaluje velký počet klientů, může to způsobit velký síťový provoz.  

-   Pokud se uživatelé často přihlašují k síti, může instalace na všech klientských počítačích trvat dlouhou dobu.  

Další informace najdete v tématu [instalace klientů pomocí přihlašovacích skriptů](../deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  



## <a name="manual-installation"></a>Ruční instalace  

**Podporované klientské platformy**: Windows, UNIX/Linux, Mac OS X  

#### <a name="advantages"></a>Výhody  

-   Nepožaduje, aby byly zjištěny počítače, aby bylo možné nainstalovat klienta.  

-   Může být užitečná pro účely testování.  

-   Podporuje používání vlastností příkazového řádku služby CCMSetup.  

#### <a name="disadvantages"></a>Nevýhody  

-   Není automatizovaná, takže je časově náročná.  

Další informace o tom, jak ručně nainstalovat klienta na jednotlivé platformy, najdete v následujících článcích:  

-   [Postup nasazení klientů na počítače s Windows](../deploy-clients-to-windows-computers.md#BKMK_Manual)  

-   [Nasazení klientů na servery se systémy UNIX a Linux](../deploy-clients-to-unix-and-linux-servers.md)  

-   [Postup nasazení klientů na počítače Mac](../deploy-clients-to-macs.md)  



## <a name="microsoft-intune-mdm-installation"></a>Instalace Microsoft Intune MDM

**Podporované klientské platformy**: Windows 10

#### <a name="advantages"></a>Výhody  

-   Nepožaduje, aby byly zjištěny počítače, aby bylo možné nainstalovat klienta.  

-   Nevyžaduje konfiguraci a údržbu účtu instalace pro určený klientský počítač.  

-   Může používat moderní ověřování s Azure Active Directory.  

-   Může nainstalovat a přiřadit počítače na internetu.  

-   Může automatizovat s automatickým pilotním nasazením Windows a Microsoft Intune pro spolusprávu.  

#### <a name="disadvantages"></a>Nevýhody  

-   Vyžaduje další technologie mimo Configuration Manager.  

-   Vyžaduje, aby zařízení mělo přístup k Internetu, a to i v případě, že není k dispozici na internetu.  

Další informace najdete v těchto článcích:  

-   [Instalace klientů na zařízení s Windows spravovaná pomocí Intune MDM](../deploy-clients-to-windows-computers.md#bkmk_mdm)  

-   [Instalace a přiřazení Configuration Manager klientů s Windows 10, kteří používají Azure AD k ověřování](../deploy-clients-cmg-azure.md)  

