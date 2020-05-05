---
title: Upgradujte klienty.
titleSuffix: Configuration Manager
description: Získejte informace o tom, jak upgradovat klienty v Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 446c83b5-c292-4e74-ba19-0792ac6b3472
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95e6ebf1544951b71ca2b60615e3e01b27cc0f3b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076675"
---
# <a name="upgrade-clients-in-configuration-manager"></a>Upgrade klientů v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

K upgradu Configuration Manager klientského softwaru na počítačích se systémem Windows, serverech se systémy UNIX a Linux a počítačích Mac můžete použít různé metody. Zde jsou výhody a nevýhody jednotlivých metod.  

> [!TIP]  
>  Pokud provádíte upgrade serverové infrastruktury z předchozí verze nástroje Configuration Manager \(jako je Configuration Manager 2007 nebo System Center 2012 Configuration Manager\), doporučujeme před upgradem klientů provést upgrady serveru včetně instalace všech aktualizací aktuální větve. Tímto způsobem budete mít k dispozici také nejnovější verzi klientského softwaru.  

## <a name="group-policy-installation"></a>Instalace zásad skupiny  
 **Podporované klientské platformy:** Windows  

#### <a name="advantages"></a>Výhody  

- Před upgradem klienta nevyžaduje zjišťování počítačů.  

- Lze ji použít pro nové instalace klientů a pro upgrade.  

- Počítače mohou přečíst vlastnosti instalace klienta, které byly publikovány ve službě Active Directory Domain Services.  

- Nevyžaduje konfiguraci a údržbu účtu instalace pro určený klientský počítač.  

#### <a name="disadvantages"></a>Nevýhody  

- Může způsobit vysokou síťovou komunikaci, pokud upgradujete mnoho klientů.  

- Pokud není schéma služby Active Directory rozšířeno pro Configuration Manager, je nutné použít [nastavení zásady skupiny](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientGP) k přidání vlastností instalace klienta do počítačů ve vaší lokalitě.  


## <a name="logon-script-installation"></a>Instalace skriptu přihlášení  
 **Podporované klientské platformy:** Windows  

#### <a name="advantages"></a>Výhody  

- Nevyžaduje zjišťování počítačů před instalací klienta.  

- Lze ji použít pro nové instalace klientů a pro upgrade.  

- Podporuje používání vlastností příkazového řádku služby CCMSetup.  

#### <a name="disadvantages"></a>Nevýhody  

- Může způsobit vysoký síťový provoz, pokud upgradujete velký počet klientů v krátké době.  

- Upgrade všech klientských počítačů může trvat dlouhou dobu, pokud se uživatelé často nepřihlašují k síti.  

  Další informace najdete v části [Instalace klientů nástroje Configuration Manager pomocí přihlašovacích skriptů](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  

## <a name="manual-installation"></a>Ruční instalace  
 **Podporované klientské platformy:** Windows, UNIX/Linux, Mac OS X  

#### <a name="advantages"></a>Výhody  

- Před upgradem klienta nevyžaduje zjišťování počítačů.  

- Může být užitečná pro účely testování.  

- Podporuje používání vlastností příkazového řádku služby CCMSetup.  

#### <a name="disadvantages"></a>Nevýhody  

- Není automatizovaná, takže je časově náročná.  

  Další informace najdete v následujících tématech:  

- [Ruční instalace klientů nástroje Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

- [Postup upgradu klientů pro servery se systémy Linux a UNIX](../../../../core/clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)  

- [Postup upgradu klientů na počítačích Mac](../../../../core/clients/manage/upgrade/upgrade-clients-on-mac-computers.md)  

## <a name="upgrade-installation-application-management"></a>Instalace upgradu (správa aplikací)  
 **Podporované klientské platformy:** Windows  

> [!NOTE]  
>  Pomocí této metody nemůžete upgradovat klienty Configuration Manager 2007. V tomto scénáři můžete nasadit klienta Configuration Manager jako balíček z lokality Configuration Manager 2007, nebo můžete použít automatický upgrade klienta, který automaticky vytvoří a nasadí balíček obsahující nejnovější verzi klienta.  

#### <a name="advantages"></a>Výhody  

- Podporuje používání vlastností příkazového řádku služby CCMSetup.  

#### <a name="disadvantages"></a>Nevýhody  

- Může způsobit vysoký síťový provoz, pokud distribuujete klienta do rozsáhlých kolekcí.  

- Lze ji použít pouze k upgradu klientského softwaru v počítačích, které byly zjištěny a přiřazeny k lokalitě.  

  Další informace najdete v části [Postup instalace klientů nástroje Configuration Manager pomocí balíčku a programu](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientApp).  

## <a name="automatic-client-upgrade"></a>Automatický upgrade klienta  

> [!NOTE]  
> Dá se použít k upgradu klientů Configuration Manager 2007 na Configuration Manager současných klientů větví. Klient Configuration Manager 2007 se může přiřazovat k webu Configuration Manager, ale nemůže provádět žádné akce Kromě automatického upgradu klienta.  

 **Podporované klientské platformy:** Windows  

#### <a name="advantages"></a>Výhody  

- Z důvodu náhodnosti v zadaném období je pro rozsáhlé upgrady klientů vhodné pouze automatické upgrady. Jiné metody jsou buď příliš pomalé ve velkém měřítku, nebo nemají náhodnost. 

    > [!Note]
    > Pilotní nasazení klientů není pro velkou škálu vhodné, protože se vůbec náhodně nepoužívá.  
- Lze ji použít k automatickému zajištění nejnovější verze klientů v lokalitě.  

- Vyžaduje minimální správu.  

#### <a name="disadvantages"></a>Nevýhody  

- Lze ji použít pouze k upgradu klientského softwaru a nelze ji použít k instalaci nového klienta.  

- Platí pro všechny klienty v hierarchii, kteří jsou přiřazeni k lokalitě. Její rozsah nelze vymezit kolekcí.  

- Omezené možnosti plánování.  

  Další informace najdete v tématu [Postup upgradu klientů pro počítače se systémem Windows](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="client-testing"></a>Testování klienta  
 **Podporované klientské platformy:** Windows  

#### <a name="advantages"></a>Výhody  

- Dá se použít k testování nových verzí klientů v menší předprodukční kolekci.  

- Po dokončení testování budou klienti v předprodukčním prostředí povýšeni na produkční a automaticky upgradováni v rámci Configuration Manager lokality.  

#### <a name="disadvantages"></a>Nevýhody  

- Lze ji použít pouze k upgradu klientského softwaru a nelze ji použít k instalaci nového klienta.  

  [Testování upgradu klienta v předprodukční kolekci](../../../../core/clients/manage/upgrade/test-client-upgrades.md)  
