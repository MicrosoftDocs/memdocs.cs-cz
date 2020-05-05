---
title: Monitorování profilů e-mailu, Wi-Fi a VPN
titleSuffix: Configuration Manager
description: Naučte se monitorovat stav dodržování předpisů pro profily e-mailu, Wi-Fi a VPN v Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e2315b8b-98bc-40e1-8ef9-bfb5e69ab109
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 59e372641c303e77f0d88e655bb917660c9e677c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724493"
---
# <a name="monitor-email-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Sledujte profily e-mailu, Wi-Fi a VPN v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Po nasazení Configuration Manager e-mailu, Wi-Fi nebo VPN profily uživatelům ve vaší hierarchii můžete pomocí následujících postupů monitorovat stav kompatibility profilu:  

-   [Postup zobrazení výsledků dodržování předpisů v konzole Configuration Manager](#BKMK_console)  

-   [Postup zobrazení výsledků dodržování předpisů pomocí sestav](#BKMK_Reports)  

##  <a name="how-to-view-compliance-results-in-the-configuration-manager-console"></a><a name="BKMK_console"></a>Postup zobrazení výsledků dodržování předpisů v konzole Configuration Manager  
 Tento postup slouží k zobrazení podrobností o kompatibilitě nasazených profilů v konzole Configuration Manager.  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Chcete-li zobrazit výsledky kontroly kompatibility v konzole nástroje Configuration Manager:  

1.  V konzole Configuration Manager klikněte na **monitorování**.  

2.  V pracovním prostoru **Sledování** klikněte na možnost **Nasazení**.  

3.  V seznamu **nasazení** vyberte nasazení profilu, pro které chcete zkontrolovat informace o kompatibilitě.  

4.  Na hlavní stránce můžete zkontrolovat souhrnné informace o kompatibilitě nasazení profilu. Chcete-li zobrazit podrobnější informace, vyberte nasazení profilu a potom na kartě **Domů** ve skupině **nasazení** kliknutím na možnost **Zobrazit stav** otevřete stránku **stav nasazení** .  

     Na stránce **Stav nasazení** naleznete následující karty:  

    -   **Vyhovující předpisům:** Zobrazuje kompatibilitu profilu podle počtu ovlivněných prostředků. Dvojitým kliknutím na pravidlo můžete vytvořit dočasný uzel v uzlu **Uživatelé** v pracovním prostoru **Prostředky a kompatibilita** , který bude obsahovat všechny uživatele, kteří jsou kompatibilní s tímto profilem. V podokně **Podrobnosti o aktivech** jsou zobrazeni uživatelé, kteří jsou kompatibilní s profilem. Dvakrát klikněte na uživatele v seznamu a zobrazte další informace.  

        > [!IMPORTANT]  
        >  Pokud se profil nedá použít v klientském zařízení, nebude hodnocen. je však vrácen jako kompatibilní.  

    -   **Chyba:** Zobrazuje seznam všech chyb pro vybrané nasazení profilu podle počtu ovlivněných prostředků. Dvojitým kliknutím na pravidlo můžete vytvořit dočasný uzel v uzlu **Uživatelé** v pracovním prostoru **Prostředky a kompatibilita** , který bude obsahovat všechny uživatele, kteří vytvořili chyby s tímto profilem. Po výběru uživatele se v podokně **Podrobnosti o aktivech** zobrazí uživatelé, na které se vztahuje vybraný problém. Dvakrát klikněte na uživatele v seznamu a zobrazte další informace o problému.  

    -   **Nekompatibilní:** Zobrazí seznam všech pravidel nesplňujících požadavky v rámci profilu, který je založený na počtu ovlivněných prostředků. Dvojitým kliknutím na pravidlo můžete vytvořit dočasný uzel v uzlu **Uživatelé** v pracovním prostoru **Prostředky a kompatibilita** , který bude obsahovat všechny uživatele, kteří jsou nekompatibilní s tímto profilem. Po výběru uživatele se v podokně **Podrobnosti o aktivech** zobrazí uživatelé, na které se vztahuje vybraný problém. Dvakrát klikněte na uživatele v seznamu a zobrazte další informace o problému.  

    -   **Neznámý:** Zobrazí seznam všech uživatelů, u kterých nebyla nahlášena kompatibilita pro vybrané nasazení profilu, spolu s aktuálním stavem klienta pro daná zařízení.  

5.  Na stránce **stav nasazení** můžete zobrazit podrobné informace o kompatibilitě nasazeného profilu. V uzlu **Nasazení** se vytvoří dočasný uzel, který vám znovu pomůže rychle najít tyto informace.  

##  <a name="how-to-view-compliance-results-by-using-reports"></a><a name="BKMK_Reports"></a> How to View Compliance Results by Using Reports  
 Nastavení dodržování předpisů, které zahrnuje profily v Configuration Manager, zahrnuje také řadu předdefinovaných sestav, které umožňují monitorovat informace o profilech. Tyto sestavy obsahují kategorii sestav **Správa nastavení a kompatibility**.  

> [!IMPORTANT]  
>  Je nutné použít zástupný znak (%). znak při použití parametrů **Filtr zařízení** a **Filtr uživatelů** v sestavách nastavení dodržování předpisů.  

 Další informace o tom, jak nakonfigurovat vytváření sestav v Configuration Manager, najdete v tématu [Úvod do vytváření sestav](../../core/servers/manage/introduction-to-reporting.md).  
