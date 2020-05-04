---
title: Postupy pro skupiny hranic
titleSuffix: Configuration Manager
description: Nakonfigurujte skupiny hranic tak, aby logicky uspořádaly související síťová umístění s názvem hranice.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1fe22d0-4695-4de0-8bf0-e3475b03cf0e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e8a47522cf59cc211f29c572010f9d3250659e1e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715792"
---
# <a name="how-to-configure-boundary-groups-for-configuration-manager"></a>Postup konfigurace skupin hranic pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek obsahuje postupy pro konfiguraci skupin hranic. Než začnete, ujistěte se, že rozumíte konceptům hraničních skupin. Další informace najdete v tématu [skupiny hranic](boundary-groups.md).



## <a name="create-a-boundary-group"></a><a name="bkmk_create"></a>Vytvořit skupinu hranic  

1.  V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace hierarchie**a vyberte uzel **skupiny hranic** .  

2.  Na kartě **Domů** ve skupině **vytvořit** vyberte **vytvořit skupinu hranic**.  

3.  V dialogovém okně **vytvořit skupinu hranic** na kartě **Obecné** zadejte **název** této skupiny hranic. Volitelně můžete zadat **Popis**.  

4.  Vyberte **OK** , pokud chcete novou skupinu hranic uložit, nebo pokračujte k další části a nakonfigurujte skupinu hranic.  


## <a name="configure-a-boundary-group"></a><a name="bkmk_config"></a>Konfigurace hraniční skupiny  

1.  V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace hierarchie**a vyberte uzel **skupiny hranic** .  

2.  Vyberte skupinu hranic, kterou chcete upravit, a na pásu karet vyberte **vlastnosti** . Tato akce otevře skupinu hranic okno Vlastnosti.  

Nakonfigurujte tahle nastavení:  
- [Přidat nebo odebrat hranice](#bkmk_add)  
- [Konfigurace přiřazení lokality a výběr systémových serverů lokality](#bkmk_references)  
- [Konfigurace nouzového chování](#bkmk_bg-fallback)  
- [Konfigurace možností hraniční skupiny](#bkmk_options)  


### <a name="add-or-remove-boundaries"></a><a name="bkmk_add"></a>Přidat nebo odebrat hranice

Ve skupině hranic okno Vlastnosti použijte kartu **Obecné** a upravte hranice, které jsou členy této skupiny hranic:  

- Chcete-li přidat hranice, vyberte možnost **Přidat**. V okně Přidat hranice zaškrtněte políčko pro jednu nebo více hranic a vyberte **OK**.  

- Pokud chcete hranice odebrat, vyberte hranici v seznamu a vyberte **Odebrat**.  


### <a name="configure-site-assignment-and-select-site-system-servers"></a><a name="bkmk_references"></a>Konfigurace přiřazení lokality a výběr systémových serverů lokality

Pokud chcete upravit přiřazení lokality a přidruženou konfiguraci serveru systému lokality, přepněte na kartu **odkazy** ve skupině hranic okno Vlastnosti.  

- Chcete-li tuto skupinu hranic povolit pro použití klienty pro přiřazení lokality, vyberte možnost **použít tuto skupinu hranic pro přiřazení lokality**. Pak vyberte lokalitu v rozevíracím seznamu **přiřazená lokalita** . Další informace najdete v tématu [přiřazení lokality](boundary-groups.md#site-assignment).  

- Pokud chcete k této skupině hranic přidružit dostupné servery systému lokality, vyberte **Přidat**. Okno Přidat systémy lokality obsahuje pouze servery, které mají podporované role systému lokality. Zaškrtněte políčko pro jeden nebo více serverů a vyberte **OK**. Přidá je jako přiřazené systémové servery lokality pro tuto skupinu hranic.  

    > [!NOTE]  
    >  Můžete vybrat libovolnou kombinaci systémů lokality z libovolné lokality v hierarchii. Vybrané systémy lokalit jsou uvedeny na kartě **systémy lokality** ve vlastnostech každé hranice, která je členem této skupiny hranic.  

- Pokud chcete z této skupiny hranic odebrat server, vyberte server a pak vyberte **Odebrat**.  

    > [!NOTE]  
    >  Chcete-li zastavit používání této skupiny hranic pro přidružení systémů lokality, odeberte všechny servery uvedené jako přidružené systémové servery lokality.  


### <a name="configure-fallback-behavior"></a><a name="bkmk_bg-fallback"></a>Konfigurace nouzového chování

Chcete-li nakonfigurovat nouzové chování, přepněte na kartu **relace** ve skupině hranic okno Vlastnosti.  

- Vytvoření relace s jinou skupinou hranic:  

  - Vyberte **Přidat**. V okně záložní skupiny hranic vyberte skupinu hranic, kterou chcete nakonfigurovat.  

  - Nastavte záložní čas pro následující role systému lokality:  
    - Distribuční bod  
    - Bod aktualizace softwaru  
    - Bod správy  

      > [!Note]  
      > Například otevřete okno Vlastnosti pro skupinu hranic pobočky. V okně záložní skupiny hranic vyberte skupinu hranic hlavní kanceláře. Záložní čas distribučního bodu nastavíte na `20`. Když tuto konfiguraci uložíte, klienti ve skupině hranic pobočky budou po 20 minutách vyhledávat obsah z distribučních bodů v hlavní skupině hranic Office.  

  - Chcete-li zabránit přechodům na určitou skupinu hranic, vyberte skupinu hranic a pak pro typ role systému lokality vyberte **nikdy** nevyužívat. Tato akce může zahrnovat *výchozí skupinu hranic lokality*.  

- Chcete-li upravit konfiguraci existujícího vztahu, vyberte skupinu hranic v seznamu a vyberte možnost **změnit**. Tato akce otevře okno záložní skupiny hranic jenom pro tuto skupinu hranic.  
 
- Chcete-li odebrat relaci, vyberte skupinu hranic v seznamu a vyberte možnost **Odebrat**.  

Další informace najdete v tématu [Fallback](boundary-groups.md#fallback). 


### <a name="configure-boundary-group-options"></a><a name="bkmk_options"></a>Konfigurace možností hraniční skupiny
<!--1356193-->
Od verze 1806 můžete nakonfigurovat další možnosti pro klienty v této skupině hranic, a to tak, že přejdete na kartu **Možnosti** . Další informace najdete v tématu [Možnosti hraniční skupiny pro rovnocenné soubory ke stažení](boundary-groups.md#bkmk_bgoptions).

- **Povolit stahování ze strany partnerů v této skupině hranic**: Tato možnost je ve výchozím nastavení povolená. Bod správy poskytuje klientům seznam umístění obsahu, která obsahují partnerské zdroje.  

    - **Během stahování po straně druhé se používají jenom partnerské uzly ve stejné podsíti**: Toto nastavení závisí na výše uvedeném. Pokud tuto možnost povolíte, bude bod správy obsahovat jenom v seznamu umístění obsahu partnerské zdroje, které jsou ve stejné podsíti jako klient.  


## <a name="configure-a-fallback-site-for-automatic-site-assignment"></a><a name="bkmk_site-fallback"></a>Konfigurace záložní lokality pro automatické přiřazení lokality  

Pokud klienti nejsou ve skupině hranic s přiřazenou lokalitou, přiřaďte je k této lokalitě při jejich instalaci.

1.  V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** .  

2.  Na kartě **Domů** na pásu karet ve skupině **lokality** vyberte **Nastavení hierarchie**.  

3.  Na kartě **Obecné** zaškrtněte políčko pro **použití záložní lokality**. Pak vyberte lokalitu v rozevíracím seznamu **záložní lokalita** .  

4.  Kliknutím na **OK** uložte konfiguraci.  

Další informace najdete v tématu [přiřazení lokality](boundary-groups.md#site-assignment).


## <a name="enable-use-of-preferred-management-points"></a><a name="bkmk_proc-prefer"></a>Povolit použití upřednostňovaných bodů správy  

Další informace najdete v tématu [preferované body správy](boundary-groups.md#bkmk_preferred).

1.  V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** .  

2. Na kartě **Domů** na pásu karet ve skupině **lokality** vyberte **Nastavení hierarchie**.  

3. Na kartě **Obecné** vyberte **Klienti dávají přednost používání bodů správy zadaných ve skupinách hranic**.  

4. Kliknutím na **OK** uložte konfiguraci.  

