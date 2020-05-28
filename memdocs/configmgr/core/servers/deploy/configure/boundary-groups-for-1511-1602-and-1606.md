---
title: Skupiny hranic pro 1511, 1602 a 1606
titleSuffix: Configuration Manager
description: Používejte skupiny hranic s Configuration Manager verzí 1511, 1602 a 1606.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dec1e0d7-5864-43a8-9f56-413923b3914e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 09c1b0613d36cd135ff3ac71ac7ec8472ad1e8c4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721105"
---
# <a name="boundary-groups-for-configuration-manager-version-1511-1602-and-1606"></a>Skupiny hranic pro Configuration Manager verze 1511, 1602 a 1606

*Platí pro: Configuration Manager (Current Branch)*
<!-- This topic drops from TOC with the release of version 1706 -->

Informace v tomto tématu se týkají použití skupin hranic s verzemi 1511, 1602 a 1606 Configuration Manager.
Pokud používáte verzi 1610 nebo novější, přečtěte si téma [Konfigurace skupin hranic](boundary-groups.md) pro informace o tom, jak používat přepracované skupiny hranic.  


##  <a name="boundary-groups"></a><a name="BKMK_BoundaryGroups"></a>Skupiny hranic  
 Skupiny hranic se vytvářejí za účelem logického seskupení souvisejících síťových umístění (hranice), aby bylo snazší spravovat infrastrukturu. Než je možné začít skupinu hranic používat, je nutné k ní přiřadit hranice. Klienti používají konfiguraci skupiny hranic pro tyto účely:  

-   Automatické přiřazení lokality  

-   Umístění obsahu  

-   Preferované body správy

    Pokud budete používat upřednostňované body správy, musíte tuto možnost Povolit pro hierarchii a ne z konfigurace skupiny hranic. Další informace najdete v části *Povolení použití upřednostňovaných bodů správy* dále v tomto tématu.  

Při nastavování skupin hranic přidáte jednu nebo více hranic do skupiny hranic. Potom nakonfigurujete další nastavení, která se použijí pro klienty umístěné na těchto hranicích.  

#### <a name="to-create-a-boundary-group"></a>Postup při vytvoření skupiny hranic  

1.  V konzole Configuration Manager vyberte možnost **Správa**  >  **Konfigurace hierarchie**  >   **skupiny hranic**.  

2.  Na kartě **Domů** ve skupině **vytvořit** vyberte možnost **vytvořit skupinu hranic**.  

3.  V dialogovém okně **vytvořit skupinu hranic** klikněte na kartu **Obecné** a zadejte **název** této skupiny hranic.  

4.  Kliknutím na **tlačítko OK** uložte novou skupinu hranic.  

#### <a name="to-set-up-a-boundary-group"></a>Nastavení skupiny hranic  

1.  V konzole Configuration Manager vyberte možnost **Správa**  >  **Konfigurace hierarchie**  >   **skupiny hranic**.  

2.  Vyberte skupinu hranic, kterou chcete změnit.  

3.  Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  

4.  V dialogovém okně **vlastnosti** pro skupinu hranic klikněte na kartu **Obecné** a změňte hranice, které jsou členy této skupiny hranic:  

    -   Chcete-li přidat hranice, zvolte možnost **Přidat**, zaškrtněte políčko u jedné nebo více hranic a klikněte na **tlačítko OK**.  

    -   Pokud chcete hranice odebrat, vyberte hranici a pak zvolte **Odebrat**.  

5.  Na kartě **odkazy** můžete změnit přiřazení lokality a konfiguraci přiřazeného systémového serveru lokality:  

    -   Chcete-li tuto skupinu hranic povolit pro použití klienty pro přiřazení lokality, zaškrtněte políčko pro **použití této skupiny hranic pro přiřazení lokality**a poté vyberte lokalitu v rozevíracím seznamu **přiřazená lokalita** .  

    -   Chcete-li nastavit dostupné servery systému lokality, které jsou přidruženy k této skupině hranic:  

    1.  Zvolte možnost **Přidat**a zaškrtněte políčko u jednoho nebo více serverů. Servery se přidají jako přiřazené systémové servery lokality pro tuto skupinu hranic. Jsou dostupné pouze servery, které mají nainstalovanou podporovanou roli systému lokality.  

        > [!NOTE]  
        >  Můžete vybrat libovolnou kombinaci systémů lokality z libovolné lokality v hierarchii. Vybrané systémy lokalit jsou uvedeny na kartě **Systémy lokality** ve vlastnostech každé hranice, která je členem této skupiny hranic.  

    2.  Pokud chcete z této skupiny hranic odebrat server, zvolte server a pak zvolte **Odebrat**.  

        > [!NOTE]  
        >  Chcete-li zastavit používání této skupiny hranic pro přiřazování systémů lokality, musíte odebrat všechny servery, které jsou uvedeny jako přidružené systémové servery lokality.  

    3.  Chcete-li u této skupiny hranic změnit rychlost síťového připojení pro server systému lokality, zvolte server a pak zvolte možnost **změnit připojení**.  

         Ve výchozím nastavení je rychlost připojení pro každý systém lokality **rychlá**, ale rychlost můžete změnit na **pomalé**. Rychlost připojení k síti a konfigurace nasazení určuje, zda může klient stahovat obsah ze serveru.  

6.  Kliknutím na **tlačítko OK** zavřete vlastnosti skupiny hranic a uložte konfiguraci.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>Přidružení serveru nasazení obsahu nebo bodu správy ke skupině hranic  

1.  V konzole Configuration Manager vyberte možnost **Správa**  >  **Konfigurace hierarchie**  >   **skupiny hranic**.  

2.  Vyberte skupinu hranic, kterou chcete změnit.  

3.  Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  

4.  V dialogovém okně **vlastnosti** pro skupinu hranic klikněte na kartu **odkazy** .  

5.  V části **Vybrat systémové servery lokality**zvolte **Přidat**, zaškrtněte políčko u systémových serverů lokality, které chcete přidružit k této skupině hranic, a pak zvolte **OK**.  

6.  Kliknutím na **tlačítko OK** zavřete dialogové okno a uložte konfiguraci skupiny hranic.  

#### <a name="to-enable-use-of-preferred-management-points"></a>Povolit používání upřednostňované body správy  

1.  V konzole Configuration Manager zvolte **Správa**  >  **Konfigurace lokality**  >  **lokality**a pak na kartě **Domů** vyberte **Nastavení hierarchie**.  

2.  Na kartě **Obecné** v **Nastavení hierarchie**vyberte **Klienti dávají přednost používání bodů správy zadaných ve skupinách hranic**.  

3.  Kliknutím na **tlačítko OK** zavřete dialogové okno a uložte konfiguraci.  

#### <a name="to-set-up-a-fallback-site-for-automatic-site-assignment"></a>Nastavení záložní lokality pro automatické přiřazení lokality  

1. V konzole Configuration Manager klikněte na **Správa**  >  **Konfigurace lokality**  >   **lokality**.  

2. Na kartě **Domů** ve skupině **lokality** klikněte na možnost **Nastavení hierarchie**.  

3. Na kartě **Obecné** zaškrtněte políčko pro **použití záložní lokality**a pak vyberte lokalitu v rozevíracím seznamu **záložní lokalita** .  

4. Kliknutím na **tlačítko OK** konfiguraci uložte.  

   Následující části obsahují další podrobnosti o konfiguraci skupiny hranic.  

###  <a name="about-site-assignment"></a><a name="BKMK_BoundarySiteAssignment"></a> Přiřazení lokality  
 Pro klienty můžete nastavit každou skupinu hranic s přiřazenou lokalitou.  

-   Nově instalovaný klient, který používá automatické přiřazení lokality, se připojí k přiřazené lokalitě skupiny hranic, která má aktuální síťové umístění klienta.  

-   Klient, který je přiřazen k lokalitě, nemění své přiřazení lokality, když klient změní své umístění v síti. Pokud se například klient přenese do nového síťového umístění, které je reprezentované hranicí ve skupině hranic s jiným přiřazením lokality, zůstane přiřazená lokalita klienta nezměněna.  

-   Když služba zjišťování systémových prostředků služby Active Directory zjistí nový zdroj, budou informace o síti tohoto zjištěného zdroje vyhodnoceny vůči hranicím ve skupině hranic. Tento proces přidruží nový zdroj k přiřazené lokalitě určené pro metodu automatické nabízené instalace klienta.  

-   Když je hranice členem několika skupin hranic s různými přiřazenými lokalitami, klienti náhodně vyberou jednu z těchto lokalit.  

-   Změny v přiřazené lokalitě skupiny hranic se vztahují pouze na nové akce přiřazení lokality. Klienti, kteří byli dříve přiřazeni k lokalitě, nevyhodnocují své přiřazení lokality znovu na základě změn konfigurace skupiny hranic (nebo v jejich vlastním umístění v síti).  

Další informace o přiřazení klienta k lokalitě najdete v tématu věnovaném [automatickému přiřazení lokality pro počítače](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) v tématu [přiřazení klientů k lokalitě](../../../../core/clients/deploy/assign-clients-to-a-site.md)nástroje.  

###  <a name="about-content-location"></a><a name="BKMK_BoundaryContentLocation"></a> Umístění obsahu  
 Každou skupinu hranic můžete nastavit s jedním nebo více distribučními body a body migrace stavu a můžete přidružit stejné distribuční body a body migrace stavu k několika skupinám hranic.  

-   **Během distribuce softwaru**si klient vyžádá umístění pro obsah nasazení. Configuration Manager odesílá klientovi seznam distribučních bodů spojených se všemi skupinami hranic, které zahrnují aktuální síťové umístění klienta.  

-   **Během nasazování operačního systému**si klient vyžádá umístění pro odeslání nebo přijetí informací o migraci stavu. Configuration Manager odesílá klientovi seznam bodů migrace stavu přidružených ke každé skupině hranic, která obsahuje aktuální síťové umístění klienta.  

Díky tomuto chování si klient vybere nejbližší server, ze kterého se má přenášet obsah nebo informace o migraci stavu.  

###  <a name="about-preferred-management-points"></a><a name="BKMK_PreferredMP"></a> Upřednostňované body správy  
 Preferované body správy umožňují klientovi identifikovat bod správy, který je přidružený k aktuálnímu umístění v síti (hranice).  

-   Klient se pokusí použít upřednostňovaný bod správy z přiřazené lokality před tím, než použije bod správy z jeho přiřazené lokality, který není nastaven jako upřednostňovaný.  

-   Pokud chcete tuto možnost použít, musíte ji povolit pro hierarchii a nastavit skupiny hranic v jednotlivých primárních lokalitách, aby zahrnovaly body správy, které by měly být přidružené k hranicím přidruženým této skupině hranic.  

-   Když jsou nastaveny preferované body správy a klient organizuje svůj seznam bodů správy, umístí klient upřednostňované body správy na začátek seznamu přiřazených bodů správy, který zahrnuje všechny body správy z lokality přiřazené klientovi.  

> [!NOTE]  
>  Při roamingu klienta, například když se přenosný počítač přenáší do vzdáleného umístění kanceláře a mění jeho umístění v síti, může použít bod správy (nebo proxy bod správy) z místní lokality v jeho novém umístění, než se pokusí použít bod správy z jeho přiřazené lokality (která obsahuje upřednostňované body správy).  Další informace najdete v tématu [Vysvětlení způsobu, jakým klienti hledají služby a prostředky lokality pro Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) .  

###  <a name="about-overlapping-boundaries"></a><a name="BKMK_BoundaryOverlap"></a> Překrývající se hranice  
 Configuration Manager podporuje konfigurace překrývajících se hranic pro umístění obsahu:  

-   **Když klient požádá o obsah**a síťové umístění klienta patří do několika skupin hranic, Configuration Manager odesílá klientovi seznam všech distribučních bodů, které mají obsah.  

-   **Když klient požádá server o odeslání nebo přijetí informací o stavu migrace**a umístění klientské sítě patří do několika skupin hranic, Configuration Manager odešle klientovi seznam všech bodů migrace stavu přidružených ke skupině hranic, která obsahuje aktuální síťové umístění klienta.  

Díky tomuto chování si klient vybere nejbližší server, ze kterého se má přenášet obsah nebo informace o migraci stavu.  

###  <a name="about-network-connection-speed"></a><a name="BKMK_BoudnaryNetworkSpeed"></a> Rychlost síťového připojení  
 Pro každý server systému lokality ve skupině hranic můžete nastavit rychlost síťového připojení. Toto nastavení platí pro klienty, kteří se připojují k systému lokality na základě konfigurace této skupiny hranic. Stejný server systému lokality může mít nastavenou jinou rychlost připojení v různých skupinách hranic.  

 Ve výchozím nastavení je rychlost síťového připojení nastavená na hodnotu **rychlá**, ale můžete ji změnit na **pomalé**. Rychlost síťového připojení a konfigurace nasazení kontrolují, zda může klient stahovat obsah z distribučního bodu, pokud je klient v přidružené skupině hranic.  

 Další informace o tom, jak konfigurace rychlosti síťového připojení ovlivňuje získávání obsahu klienty, najdete v tématu [scénáře umístění zdroje obsahu](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  
