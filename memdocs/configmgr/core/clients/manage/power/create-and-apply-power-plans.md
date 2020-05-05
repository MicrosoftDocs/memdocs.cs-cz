---
title: Vytvoření a použití schémat napájení
titleSuffix: Configuration Manager
description: Vytvoření a použití schémat napájení v Configuration Manager.
ms.date: 04/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 738eddaa-52e2-467f-b453-821ef2884d47
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ba5479a4c75d3ab8f91a8439a6799589b93972d0
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076692"
---
# <a name="how-to-create-and-apply-power-plans-in-configuration-manager"></a>Postup vytvoření a použití schémat napájení v nástroji Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Řízení spotřeby v Configuration Manager umožňuje použít schémata napájení, která se dodávají s Configuration Manager, do kolekcí počítačů ve vaší hierarchii nebo vytvářet vlastní schémata napájení. Pomocí postupu v tomto tématu můžete do počítačů zavádět vestavěná nebo vlastní schémata napájení.  

> [!IMPORTANT]  
>  Pro kolekce zařízení můžete použít pouze Configuration Manager schémata napájení.  

 Pokud je počítač členem více kolekcí, z nichž každá používá jiné schéma napájení, provedou se tyto akce:  

- Schéma napájení: Pokud se pro počítač používá víc hodnot nastavení napájení, použije se nejméně omezující hodnota.  

- Čas probuzení: Pokud se pro stolní počítač používá víc časů probuzení, použije se čas nejbližší k půlnoci.  

  Sestava **Počítače s více schématy napájení** slouží k zobrazení všech počítačů, které mají víc schémat napájení. Díky tomu můžete najít počítače, které mají konflikt nastavení napájení. Další informace o sestavách řízení spotřeby najdete v tématu [monitorování a plánování řízení spotřeby](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

> [!IMPORTANT]  
>  Nastavení napájení nakonfigurované pomocí Windows Zásady skupiny přepíše nastavení nakonfigurované pomocí Configuration Manager řízení spotřeby.  

 Pomocí následujícího postupu můžete vytvořit a použít Configuration Manager schéma napájení.  

### <a name="to-create-and-apply-a-power-plan"></a>Vytvoření a použití schématu napájení  

1. V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.  

2. V pracovním prostoru **Prostředky a kompatibilita** klikněte na možnost **Kolekce zařízení**.  

3. V seznamu **Kolekce zařízení** vyberte kolekci, pro kterou chcete řízení spotřeby použít, a potom na kartě **Domů** ve skupině **Vlastnosti** klikněte na možnost **Vlastnosti**.  

4. Na kartě **řízení spotřeby** dialogového okna <em><\>název kolekce</em>–**vlastnosti** vyberte možnost **zadat nastavení řízení spotřeby pro tuto kolekci**.  

   > [!NOTE]  
   >  Můžete také kliknout na **Procházet** a zkopírovat nastavení řízení spotřeby z jedné kolekce do druhé.  

5. Do polí **Začátek** a **Konec** zadejte čas začátku a konce pracovní doby (špičky).  

6. Povolením možnosti **Čas probuzení (stolní počítače)** můžete určit čas, kdy se stolní počítač probudí z režimu spánku nebo hibernace kvůli instalaci plánovaných aktualizací nebo softwaru.  

   > [!IMPORTANT]  
   >  Řízení spotřeby používá interní funkci probuzení systému Windows k probuzení počítače ze spánku nebo hibernace v určitou dobu. Nastavení času probuzení se nepoužívá pro přenosné počítače, aby se zabránilo situaci, kdy by byl počítač probuzený v době, kdy není připojený ke zdroji napájení. Čas probuzení je náhodně posunut a počítače budou probuzené na jednu hodinu od času probuzení.  

7. Když chcete konfigurovat vlastní schéma napájení v pracovní době, vyberte možnost **Vlastní špička (nástroj ConfigMgr)** z rozevíracího seznamu **Schéma pro období špičky** a pak klikněte na tlačítko **Upravit**. Když chcete konfigurovat schéma napájení mimo pracovní dobu, vyberte možnost **Vlastní pro dobu mimo špičku (nástroj ConfigMgr)** z rozevíracího seznamu **Schéma pro dobu mimo špičku** a pak klikněte na tlačítko **Upravit**.  

   > [!NOTE]  
   >  Můžete použít sestavu **Aktivita počítače**, která vám pomůže rozhodnout, jak mají při nasazení do kolekce počítačů vypadat schémata napájení pro pracovní dobu a mimo ni. Další informace najdete v tématu [monitorování a plánování řízení spotřeby](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

    Můžete také vybrat z předdefinovaných schémat napájení **Rovnováha (nástroj ConfigMgr)**, **Vysoký výkon (nástroj ConfigMgr)** a **Úspora energie (nástroj ConfigMgr)** a potom kliknutím na tlačítko **Zobrazit** zobrazit vlastnosti daného  schématu napájení.  

   > [!NOTE]  
   >  Nelze změnit vestavěná schémata napájení.  

8. V dialogovém okně <em><název\>schématu napájení</em>–**vlastnosti** nakonfigurujte následující nastavení:  

   -   **Název:** zadejte název pro toto schéma napájení nebo použijte předvyplněnou hodnotu.  

   -   **Popis:**  zadejte popis pro toto schéma napájení nebo použijte předvyplněnou hodnotu.  

   -   **Zadejte vlastnosti pro toto schéma napájení:** určete vlastnosti schématu. Když chcete vlastnost vypnout, zrušte zaškrtnutí jejího políčka. Informace o dostupných nastaveních najdete v části [Available power management plan settings](#BKMK_Plans) v tomto tématu.  

       > [!IMPORTANT]  
       >  Povolená nastavení se použijí pro počítače při použití schématu napájení. Když zrušíte zaškrtnutí políčka některého nastavení, odpovídající hodnota v klientském počítači se při použití schématu napájení nezmění. Zrušení zaškrtnutí políčka ale neobnoví dané nastavení na původní hodnotu před použitím schématu napájení.  

9. Kliknutím na tlačítko **OK** zavřete dialogové okno <em><název\>schématu napájení</em>–**vlastnosti** .  

10. Kliknutím na tlačítko **OK** zavřete dialogové okno**Nastavení** <em>\>názvu kolekce<</em>a použijete schéma napájení.  

##  <a name="available-power-management-plan-settings"></a><a name="BKMK_Plans"></a> Available power management plan settings  
 Následující tabulka uvádí nastavení řízení spotřeby, která jsou k dispozici v Configuration Manager. Můžete nakonfigurovat samostatná nastavení pro případy, kdy je počítač připojený ke zdroji napájení nebo kdy běží na baterii. V závislosti na použité verzi Windows nemusí být některá nastavení dostupná.  

> [!NOTE]  
>  Nastavení napájení, které nenakonfigurujete, si v klientských počítačích zachová aktuální hodnotu.  

|Název|Popis|  
|----------|-----------------|  
|**Vypnout displej po (minuty)**|Určuje dobu, po kterou musí být počítač neaktivní, aby se vypnul displej. Zadejte hodnotu **0** když nechcete, aby řízení spotřeby vypínalo displej.|  
|**Přejít do režimu spánku po (minuty)**|Určuje dobu, po kterou musí být počítač neaktivní, aby přešel do režimu spánku. Zadejte hodnotu **0** když nechcete, aby řízení spotřeby aktivovalo režim spánku.|  
|**Po probuzení požadovat heslo**|Hodnota **Ano** nebo **ne** určuje, jestli se při přechodu do režimu spánku vyžaduje heslo k odemknutí počítače.|  
|**Akce tlačítka napájení**|Určuje akci, která se provádí při stisknutí tlačítka napájení počítače. Možné hodnoty **nedělají nic**, **režim spánku**, **režim hibernace**a **vypnutí**.|  
|**Tlačítko napájení v nabídce Start**|Určuje akci, která nastane po stisknutí tlačítka napájení v nabídce **Start** počítače. Možné hodnoty jsou v **režimu spánku**, **Hibernace**a **vypnuté**.|  
|**Akce tlačítka režimu spánku**|Určuje akci, která nastane po stisknutí tlačítka **režimu spánku** počítače. Možné hodnoty **nedělají nic**, **režim spánku**, **režim hibernace**a **vypnutí**.|  
|**Akce při zavření krytu**|Určuje akci, která nastane při zavření víka přenosného počítače. Možné hodnoty **nedělají nic**, **režim spánku**, **režim hibernace**a **vypnutí**.|  
|**Vypnout pevný disk po (minuty)**|Určuje dobu v minutách, po kterou musí být pevný disk počítače neaktivní, než bude vypnut. Zadejte hodnotu **0** , pokud nechcete, aby řízení spotřeby vypnulo pevný disk počítače.|  
|**Hibernace po (minuty)**|Určuje dobu, po kterou musí být počítač neaktivní, aby přešel do režimu hibernace. Zadejte hodnotu **0** když nechcete, aby řízení spotřeby aktivovalo režim hibernace.|  
|**Akce při nízkém stavu baterie**|Určuje akci, která nastane, když baterie počítače dosáhne určené úrovně upozornění na nízký stav baterie. Možné hodnoty **nedělají nic**, **režim spánku**, **režim hibernace**a **vypnutí**.|  
|**Akce při kritickém stavu baterie**|Určuje akci, která se provede, když baterie počítače dosáhne určené úrovně upozornění na kritický stav baterie. V případě, že jsou možné hodnoty z **baterie** přejít do režimu **spánku**, **Hibernace**a **vypnutí**. Když se **z elektrické sítě v** případě možných hodnot **neudělá nic**, **režim spánku**, **režim hibernace**a **vypnutí**.|  
|**Povolit hybridní režim spánku**|Výběrem hodnoty **zapnuto** nebo **vypnuto** určíte, zda systém Windows při přechodu do režimu spánku uloží soubor hibernace, který se dá použít k obnovení stavu počítače v případě výpadku napájení, který přešel do režimu spánku.<br /><br /> Hybridní režim spánku je určený pro stolní počítače a ve výchozím nastavení není povolený v přenosných počítačích. Na počítačích s Windows 7 povolení hybridního režimu spánku zakáže funkci režimu hibernace.|  
|**Povolit úsporný režim při akci režimu spánku**|Výběr hodnoty **zapnuto** nebo **vypnuto** umožní počítači být v pohotovostním režimu, což stále spotřebovává určitý výkon, ale umožňuje rychlejší probuzení počítače. Když je toto nastavení **Vypnuto**, může počítač přejít jenom do režimu hibernace nebo se vypnout.|  
|**Požadována nečinnost k přechodu do režimu spánku (%)**|Určuje procento doby nečinnosti celkového času procesoru požadované pro přechod počítače do režimu spánku. U počítačů s Windows 7 je tato hodnota vždycky nastavená na **0**.|  
|**Povolit časovač probuzení systému Windows pro stolní počítače**|Vyberete-li hodnotu **Povolit** nebo **Zakázat** , může funkce řízení spotřeby využít integrovaný časovač systému Windows k probuzení stolního počítače. Když je stolní počítač probuzený pomocí časovače probuzení systému Windows, zůstane ve výchozím nastavení vzhůru po dobu 10 minut, aby bylo dost času pro instalaci případných aktualizací nebo zásad.<br /><br /> Časovače probuzení se nepoužívají pro přenosné počítače, aby se zabránilo situaci, kdy by byl počítač probuzený v době, kdy není připojený ke zdroji napájení.|  
