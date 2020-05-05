---
title: Monitorování profilů certifikátů
titleSuffix: Configuration Manager
description: Naučte se monitorovat stav dodržování předpisů Configuration Manager profily certifikátů.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 98feaa06-64b1-4e86-a122-93017c97cd4f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee1f43e113aa91f75c09bd264e8b3bc2704220a8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722295"
---
# <a name="how-to-monitor-certificate-profiles-in-configuration-manager"></a>Jak monitorovat profily certifikátů v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*


##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Zobrazení výsledků dodržování předpisů v konzole Configuration Manager  

K monitorování dodržování předpisů certifikátu SCEP nepoužívejte konzolu, ale použijte [sestavy](#view-compliance-results-by-using-reports). 

1. V konzole Configuration Manager vyberte možnost **monitorování**>  **nasazení**.  

2. Vyberte nasazení profilu certifikátu, které vás zajímá.  

3. Projděte si souhrnné informace o kompatibilitě certifikátů na hlavní stránce. Podrobnější informace získáte tak, že vyberete profil certifikátu a potom na kartě **Domů** ve skupině **nasazení** vyberete možnost **Zobrazit stav** a otevřete stránku **stav nasazení** .  

    Na stránce **Stav nasazení** naleznete následující karty:  

   -   **Kompatibilní:** Zobrazuje kompatibilitu profilu certifikátu podle počtu ovlivněných prostředků. Pokud dvakrát kliknete na pravidlo, můžete pod uzlem **Uživatelé** v pracovním prostoru **Prostředky a kompatibilita** vytvořit dočasný uzel. Tento uzel obsahuje všechny uživatele, kteří jsou kompatibilní s profilem certifikátu. Také v podokně **Podrobnosti o aktivech** jsou zobrazeni uživatelé kompatibilní s tímto profilem. Poklikáním na uživatele v seznamu zobrazíte další informace.  

       > [!IMPORTANT]  
       >  Jestliže se profil certifikátu ke klientskému zařízení nevztahuje, nebude hodnocen. Nicméně bude vrácen jako kompatibilní.  

   -   **Chyba:** Zobrazuje seznam všech chyb pro vybrané nasazení profilu certifikátu podle počtu ovlivněných prostředků. Chcete-li vytvořit dočasný uzel pod uzlem **Uživatelé** pracovního prostoru **Prostředky a kompatibilita** , můžete dvakrát kliknout na pravidlo. Tento uzel obsahuje všechny uživatele, u nichž s tímto profilem vznikly chyby. Po výběru uživatele se v podokně **Podrobnosti o aktivech** zobrazí uživatelé, na které se vztahuje vybraný problém. Poklikáním na uživatele v seznamu zobrazíte další informace.  

   -   **Nekompatibilní:** Zobrazuje seznam všech pravidel nesplňujících požadavky v rámci profilu certifikátu podle počtu ovlivněných prostředků. Chcete-li vytvořit dočasný uzel pod uzlem **Uživatelé** pracovního prostoru **Prostředky a kompatibilita** , můžete dvakrát kliknout na pravidlo. Tento uzel obsahuje všechny uživatele, kteří nejsou kompatibilní s tímto profilem. Po výběru uživatele se v podokně **Podrobnosti o aktivech** zobrazí uživatelé, na které se vztahuje vybraný problém. Dvakrát klikněte na uživatele v seznamu a zobrazte další informace o problému.  

   -   **Neznámé:** Zobrazuje seznam všech uživatelů, u kterých nebyla nahlášená kompatibilita pro vybrané nasazení profilu certifikátu, spolu s aktuálním stavem klienta pro daná zařízení.  

4. Na stránce **stav nasazení** si přečtěte podrobné informace o kompatibilitě nasazeného profilu certifikátu. V uzlu **Nasazení** se vytvoří dočasný uzel, který vám znovu pomůže rychle najít tyto informace.  

    Stav zápisu certifikátu je zobrazen ve formě čísla. Následující tabulka vysvětluje význam jednotlivých čísel:  


   | Stav registrace |                                                                                                                   Popis                                                                                                                   |
   |-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |    0x00000001     |                                                                                         Zápis byl úspěšný a certifikát byl vydán.                                                                                          |
   |    0x00000002     |                                                                    Žádost byla odeslána a zápis čeká na dokončení, nebo žádost byla vydána vzdáleně.                                                                    |
   |    0x00000004     |                                                                                                          Zápis musí být odložen.                                                                                                           |
   |    0x00000010     |                                                                                                               Došlo k chybě.                                                                                                                |
   |    0x00000020     |                                                                                                        Stav zápisu není znám.                                                                                                        |
   |    0x00000040     | Informace o stavu byly vynechány. K této chybě může dojít, pokud<https://msdn.microsoft.com/windows/ms721572>je v hypertextovém odkazu "," _security_certification_authority_gly "certifikační autorita" "\l" neplatná nebo nebyla vybrána pro monitorování. |
   |    0x00000100     |                                                                                                           Zápis byl zamítnut.                                                                                                           |

##  <a name="view-compliance-results-by-using-reports"></a>Zobrazení výsledků dodržování předpisů pomocí sestav

Nastavení dodržování předpisů v Configuration Manager obsahují předdefinované sestavy, pomocí kterých můžete monitorovat informace o profilech certifikátů. Tyto sestavy obsahují kategorii sestav **Správa nastavení a kompatibility**.  

> [!IMPORTANT]  
>  Při použití parametrů **Filtr zařízení** a **Filtr uživatelů** v sestavách pro nastavení kompatibility je nutné použít zástupný znak (%).  

Pokud chcete monitorovat dodržování předpisů certifikátu SCEP, použijte tyto sestavy certifikátů v uzlu sestavy **přístup k prostředkům společnosti**:  

-   Historie vystavování certifikátů  
-   Seznam prostředků s certifikáty s blížícím se datem konce platnosti  
-   Seznam prostředků podle stavu vystavení certifikátu  



 Další informace o tom, jak nakonfigurovat vytváření sestav v Configuration Manager, najdete v tématu [Úvod do vytváření sestav](../../core/servers/manage/introduction-to-reporting.md).  
