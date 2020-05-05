---
title: Technical Preview 1803
titleSuffix: Configuration Manager
description: Seznamte se s novými funkcemi dostupnými v Configuration Manager Technical Preview verze 1803.
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 56dc4b07-5aa4-43e2-9be8-d26ae5ff5613
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: bb8224df3ccbb086ca0c83d08f29522cf3289c32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719040"
---
# <a name="capabilities-in-technical-preview-1803-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1803 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1803. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Technical Preview. 

Před instalací této aktualizace si přečtěte článek [Technical Preview](technical-preview.md) . V tomto článku se seznámíte s obecnými požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->


</br>

**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  



 
## <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Distribuční body pro vyžádání obsahu podporují distribuční body cloudu jako zdroj  
<!--1321554-->
Mnoho zákazníků používá [distribuční body pro vyžádání](../plan-design/hierarchy/use-a-pull-distribution-point.md) obsahu ve vzdálených nebo firemních pobočkách, které stahují obsah ze zdrojového distribučního bodu v síti WAN. Pokud vaše vzdálené pobočky mají lepší připojení k Internetu nebo chcete snížit zatížení připojení WAN, teď můžete jako zdroj použít [distribuční bod cloudu](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) v Microsoft Azure. Když přidáte zdroj na kartě **distribuční bod pro vyžádání** obsahu vlastností distribučního bodu, všechny distribuční body cloudu v lokalitě jsou nyní uvedeny jako dostupné distribuční body. Chování obou rolí systému lokality zůstane stejné jako v opačném případě. 

### <a name="prerequisites"></a>Požadavky
- Distribuční bod pro vyžádání obsahu potřebuje přístup k Internetu, aby mohl komunikovat s Microsoft Azure.
- Obsah musí být distribuován do zdrojového cloudového distribučního bodu.

> [!Note]  
> Tato funkce se za vaše předplatné Azure účtuje za ukládání dat a odchozí přenos z sítě. Další informace najdete v tématu [náklady na používání cloudové distribuce](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_cost).



## <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>Částečná podpora stahování ve sdílené mezipaměti klienta pro omezení využití sítě WAN
<!--1357346-->
Zdroje sdílené mezipaměti klienta teď můžou rozdělit obsah na části. Tyto části minimalizují přenos v síti, aby se snížilo využití sítě WAN. Bod správy poskytuje podrobnější sledování částí obsahu. Pokusí se odstranit více než jedno stažení stejného obsahu pro jednu skupinu hranic. 

### <a name="example-scenario"></a>Ukázkový scénář
Contoso má jednu primární lokalitu se dvěma skupinami hranic: ústředí (sídel) a firemní pobočky. Mezi skupinami hranic existuje záložní vztah mezi 30 minutami. Bod správy a distribuční bod pro lokalitu nástroje jsou pouze na hranici sídel. Umístění pobočky nemá žádný místní distribuční bod. Dva ze čtyř klientů na pobočce jsou nakonfigurováni jako zdroje sdílené mezipaměti. 

![Diagram konfigurace sítě, jak je popsáno v ukázkovém scénáři](media/1357346-peer-cache-source-parts.png)

1. Cílíte na nasazení s využitím obsahu na všechny čtyři klienty na pobočce. Obsah jste rozšíříte pouze do distribučního bodu.
2. Client3 a Client4 nemají pro nasazení místní zdroj. Bod správy instruuje klienty, aby čekali 30 minut, než se vrátí do skupiny vzdálených hranic.
3. KLIENT1 (PCS1) je prvním zdrojem sdílené mezipaměti, který aktualizuje zásady pomocí bodu správy. Vzhledem k tomu, že je tento klient povolen jako zdroj sdílené mezipaměti, bod správy ho instruuje, aby ihned zahájil stahování části A z distribučního bodu.  
4. Když počítač KLIENT2 (PCS2) kontaktuje bod správy, protože součást A již ještě není dokončena, bod správy ji vydá pokyn, aby hned zahájil stahování části B z distribučního bodu.
5. PCS1 dokončí stahování části a a okamžitě se upozorní na bod správy. V případě, že část B již probíhá, ale ještě není dokončena, bod správy ji instruuje, aby zahájil stahování části C z distribučního bodu.
6. PCS2 dokončí stahování části B a okamžitě se upozorní na bod správy. Bod správy dá pokyn ke spuštění stahování části D z distribučního bodu. 
7. PCS1 dokončí stahování části C a okamžitě se upozorní na bod správy. Bod správy je informuje o tom, že ze vzdáleného distribučního bodu nejsou k dispozici žádné další části. Bod správy dá pokyn ke stažení části B od svého místního partnera PCS2.
8. Tento proces pokračuje, dokud oba zdroje sdílené mezipaměti klienta všechny části navzájem navzájem. Bod správy určuje prioritu částí ze vzdáleného distribučního bodu před tím, než dáte pokyn pro zdroje sdílené mezipaměti, aby stahoval součásti z místních partnerských uzlů. 
9. Client3 je první k aktualizaci zásad po vypršení platnosti záložního období 30 minut. Nyní se vrátí s bodem správy, který informuje klienta o nových místních zdrojích. Místo stažení obsahu z distribučního bodu v síti WAN stáhne obsah v plném rozsahu z jednoho ze zdrojů sdílené mezipaměti klienta. Klienti mají prioritu místních partnerských zdrojů. 

> [!Note]  
> Pokud je počet zdrojů sdílené mezipaměti klienta větší než počet částí obsahu, pak bod správy vydá další zdroje sdílené mezipaměti, aby čekal na záložní použití jako normálního klienta. 


### <a name="try-it-out"></a>Určitě to udělejte!
 Zkuste úkoly dokončit. Potom můžete poslat **zpětnou vazbu** na kartě **Domů** na pásu karet, abychom věděli, jak pracovali.

1. Nastavte [skupiny hranic](../servers/deploy/configure/boundary-groups.md) a [zdroje sdílené mezipaměti](../plan-design/hierarchy/client-peer-cache.md) na normální.
2. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte možnost **lokality**. Na pásu karet klikněte na **Nastavení hierarchie** . 
3. Na kartě **Obecné** povolte možnost **Konfigurace zdrojů sdílené mezipaměti klienta pro rozdělení obsahu na části**. 
4. Vytvořte požadované nasazení s obsahem.  

   > [!Note]  
   > Tato funkce funguje pouze v případě, že klient stáhne obsah na pozadí, například s požadovaným nasazením. Stahování na vyžádání, například když uživatel nainstaluje dostupné nasazení v centru softwaru, se chová jako obvykle.  

1. Pokud se chcete podívat, jak se stahují obsah v částech, Prohlédněte si soubor **ContentTransferManager. log** ve zdroji sdílené mezipaměti klienta a **MP_Location. log** v bodu správy.  
 



## <a name="maintenance-windows-in-software-center"></a>Okna údržby v centru softwaru
<!--1358131-->
Centrum softwaru teď zobrazí další naplánované časové období údržby. Na kartě stav instalace přepněte zobrazení ze všech na nadcházející. Zobrazuje časový rozsah a seznam naplánovaných nasazení. Seznam je prázdný, pokud nejsou k dispozici žádná budoucí časová období údržby. 

![Centrum softwaru zobrazující seznam nadcházejících nasazení na kartě stav instalace](media/1358131-software-center-maintenance-windows.png)


## <a name="custom-tab-for-webpage-in-software-center"></a>Vlastní karta pro webovou stránku v centru softwaru
<!--1358132-->
Nyní můžete vytvořit přizpůsobenou kartu pro otevření webové stránky v centru softwaru. Tato funkce umožňuje zobrazit obsah koncovým uživatelům konzistentním a spolehlivým způsobem. Následující seznam obsahuje několik příkladů:
- Kontaktujte IT: informace o tom, jak kontaktovat oddělení IT ve vaší organizaci
- IT Support Center: samoobslužné akce, jako je hledání ve znalostní bázi nebo otevření lístku podpory.
- Dokumentace pro koncové uživatele: články pro uživatele ve vaší organizaci na různých tématech, jako je například použití aplikací nebo upgrade na systém Windows 10.


### <a name="try-it-out"></a>Určitě to udělejte!
 Zkuste úkoly dokončit. Potom můžete poslat **zpětnou vazbu** na kartě **Domů** na pásu karet, abychom věděli, jak pracovali.

1. V konzole Configuration Manager v pracovním prostoru **Správa** v uzlu **nastavení klienta** otevřete výchozí zásady **nastavení klienta** .
2. Vyberte skupinu **Centrum softwaru** .
3. V **Nastavení centra softwaru**klikněte na **přizpůsobit**.
4. Přepněte na kartu **karty** .
5. Povolte možnost **zadat vlastní kartu pro Centrum softwaru**.
    1. Zadejte název do textového pole **název karty** . Tento název se zobrazí uživateli v centru softwaru.
    2. Do textového pole **Adresa URL obsahu** zadejte platnou adresu URL. Tato adresa URL je obsah, který Centrum softwaru zobrazí, když na tuto kartu uživatel klikne.

> [!Tip]  
> Centrum softwaru používá součásti aplikace Internet Explorer pro vykreslování webové stránky.

## <a name="enable-third-party-software-update-support-on-clients"></a>Povolit podporu aktualizací softwaru třetích stran na klientech

Nyní můžete povolit konfiguraci Configuration Manager klientů pro aktualizace softwaru třetích stran. Když pro vlastnosti komponenty SUP **povolíte aktualizace softwaru třetích stran** , NAČTE soubor SUP podpisový certifikát používaný službou WSUS pro aktualizace třetích stran. <!--1357605-->

Výběr možnosti **Povolit aktualizace softwaru třetích stran** v nastavení klienta provede následující akce: 
- V klientovi nastaví zásadu pro možnost "povolení podepsaných aktualizací pro intranetové služby Microsoft Update". 
- Nainstaluje podpisový certifikát do úložiště důvěryhodných vydavatelů na klientovi. 

### <a name="try-it-out"></a>Určitě to udělejte!
 Zkuste úkoly dokončit. Potom můžete poslat **zpětnou vazbu** na kartě **Domů** na pásu karet, abychom věděli, jak pracovali.

1. V lokalitě na nejvyšší úrovni v hierarchii Configuration Manager klikněte na uzel **Správa** , rozbalte položku **Konfigurace lokality**a pak na **lokality**.
2. Pravým tlačítkem myši klikněte na server lokality na nejvyšší úrovni a vyberte možnost **Konfigurovat součásti webu** a potom **bod aktualizace softwaru**.
3. Klikněte na kartu **aktualizace třetích stran** a zaškrtněte políčko **Povolit aktualizace softwaru třetích stran**.
4. Otevřete **nastavení klienta** a pokračujte na nastavení pro **aktualizace softwaru**.
5. Ujistěte se, že **možnost povolit aktualizace softwaru třetích stran** je nastavená na **Ano**.

## <a name="enable-copypaste-of-asset-details-from-monitoring-views"></a>Povolit kopírování a vkládání podrobností assetů ze zobrazení monitorování
V důsledku [zpětné vazby uživatele](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20234866-allow-us-to-copy-information-out-of-the-asset-det) můžete nyní povolit funkce kopírování a vkládání v podokně Podrobnosti o aktivech v zobrazeních monitorování stavu nasazení a distribuce.  <!--1357552-->

## <a name="scap-extensions"></a>Rozšíření SCAP
Předběžná verze rozšíření SCAP je k dispozici na disku CD. poslední složka v části SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi. Tato předběžná verze rozšíření SCAP se dá nainstalovat na všechny aktuálně podporované verze Configuration Manager aktuální větve a LTSB 1606.



## <a name="next-steps"></a>Další kroky
Informace o instalaci nebo aktualizaci větve Technical Preview najdete v tématu [Technical Preview pro Configuration Manager](technical-preview.md).    
