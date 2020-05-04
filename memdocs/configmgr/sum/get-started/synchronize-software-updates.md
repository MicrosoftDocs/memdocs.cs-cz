---
title: Správa synchronizace aktualizací softwaru
titleSuffix: Configuration Manager
description: Pomocí těchto kroků můžete naplánovat synchronizaci aktualizací softwaru, ručně spustit synchronizaci aktualizací softwaru a monitorovat synchronizaci aktualizací softwaru.
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: ea8698c4-9df5-4cf5-8b62-ab93115b4769
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: d1b47965fa5cc36b0c0eb6d47c2214d1dceb8ee8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712677"
---
#  <a name="synchronize-software-updates"></a><a name="BKMK_SUMSync"></a>Synchronizovat aktualizace softwaru

*Platí pro: Configuration Manager (Current Branch)*

 Synchronizace aktualizací softwaru v Configuration Manager je proces načítání metadat aktualizace softwaru, která splňují kritéria, která nakonfigurujete. To zahrnuje konkrétní produkty, klasifikace a jazyky. Obvykle bod aktualizace softwaru v lokalitě centrální správy nebo v samostatné primární lokalitě načítá metadata z Microsoft Update. Lokalita nejvyšší úrovně pak odešle požadavek na synchronizaci na jiné lokality. Když lokalita obdrží požadavek na synchronizaci z nadřazené lokality, bod aktualizace softwaru pro lokalitu načte metadata aktualizace softwaru z nadřazeného [zdroje synchronizací](../plan-design/plan-for-software-updates.md#BKMK_SyncSource). Další informace o procesu synchronizace aktualizací softwaru najdete v tématu [synchronizace aktualizací softwaru](../understand/software-updates-introduction.md#BKMK_Synchronization).

Synchronizaci aktualizací softwaru můžete nakonfigurovat tak, aby běžela podle plánu ve vlastnostech bodu aktualizace softwaru v lokalitě nejvyšší úrovně. Po konfiguraci plánu synchronizace obvykle v rámci běžných operací nebudete plán měnit. Synchronizaci aktualizací softwaru však můžete v případě potřeby zahájit ručně.

  > [!NOTE]  
  >  Aby bylo možné synchronizovat aktualizace softwaru, musí být body aktualizace softwaru připojeny k nadřazenému zdroji synchronizace. Pokud bod aktualizace softwaru není k nadřazenému zdroji připojen, můžete k synchronizaci aktualizací softwaru použít metodu exportu a importu. Další informace najdete v tématu [Synchronizace aktualizací softwaru z odpojeného bodu aktualizace softwaru](synchronize-software-updates-disconnected.md).  

## <a name="schedule-software-updates-synchronization"></a>Naplánovat synchronizaci aktualizací softwaru
Když nakonfigurujete plán pro synchronizaci aktualizací softwaru, bod aktualizace softwaru nejvyšší úrovně spustí synchronizaci s Microsoft Update v naplánovaném datu a času. Vlastní plán umožňuje synchronizovat aktualizace softwaru v datu a čase, kdy jsou požadavky na server služby Windows Server Update Services (WSUS), server lokality a síť nízké. Můžete například nastavit plán tak, aby se aktualizace softwaru synchronizovaly každý týden v 2:00. Během plánované synchronizace jsou do databáze lokality vloženy všechny změny metadat aktualizací softwaru od poslední plánované synchronizace. Zahrnují metadata nových aktualizací softwaru nebo metadata, která byla změněna, odebrána nebo jejichž platnost vypršela.

Pomocí následujících postupů v lokalitě nejvyšší úrovně Naplánujte synchronizaci aktualizací softwaru.  

#### <a name="to-schedule-software-updates-synchronization"></a>Naplánování synchronizace aktualizací softwaru  

  1.  V konzole Configuration Manager klikněte na možnost **Správa**.  

  2.  V pracovním prostoru Správa rozbalte nabídku **Konfigurace webu**a klikněte na položku **Weby**.  

  3.  V podokně výsledků klikněte na lokalitu centrální správy nebo na samostatnou primární lokalitu.  

  4.  Na kartě **Domů** v části **Nastavení** rozbalte položku **Konfigurovat součásti pracoviště**a potom klikněte na **Bod aktualizace softwaru**.  

  5.  V dialogovém okně Vlastnosti komponenty bodu aktualizace softwaru vyberte možnost **Povolit synchronizaci s plánem**a potom určete plán synchronizace.  

## <a name="manually-start-software-updates-synchronization"></a>Ruční spuštění synchronizace aktualizací softwaru
Můžete ručně zahájit synchronizaci aktualizací softwaru v lokalitě nejvyšší úrovně v konzole Configuration Manager v uzlu **všechny aktualizace softwaru** v pracovním prostoru **softwarová knihovna** .  

Pro ruční zahájení synchronizace aktualizací softwaru použijte následující postupy v lokalitě nejvyšší úrovně.  

#### <a name="to-manually-start-software-updates-synchronization"></a>Ruční spuštění synchronizace aktualizací softwaru  

1. V konzole Configuration Manager, která je připojená k lokalitě centrální správy nebo samostatné primární lokalitě klikněte na možnost **softwarová knihovna**.  

2. V pracovním prostoru Softwarová knihovna rozbalte možnost **Aktualizace softwaru** a klikněte na **Všechny aktualizace softwaru** nebo **Skupiny aktualizací softwaru**.  

3. Na kartě **Domů** v části **Vytvořit** klikněte na **Synchronizovat softwarové aktualizace**. Kliknutím na tlačítko **Ano** v dialogovém okně potvrďte, že chcete proces synchronizace zahájit.  

   Po zahájení procesu synchronizace v bodě aktualizace softwaru můžete monitorovat proces synchronizace z konzoly Configuration Manager pro všechny body aktualizace softwaru ve vaší hierarchii. Pomocí následujícího postupu monitorujte proces synchronizace aktualizací softwaru.  


## <a name="monitor-software-updates-synchronization"></a>Monitorování synchronizace aktualizací softwaru
Po zahájení procesu synchronizace můžete použít konzolu Configuration Manager k monitorování procesu pro všechny body aktualizace softwaru ve vaší hierarchii. Pomocí následujícího postupu monitorujte proces synchronizace aktualizací softwaru. Další informace o monitorování aktualizací softwaru, včetně procesu synchronizace, najdete v tématu [monitorování aktualizací softwaru](../deploy-use/monitor-software-updates.md).

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Monitorování procesu synchronizace aktualizací softwaru  

1. V konzole Configuration Manager klikněte na **monitorování**.  

2. V pracovním prostoru **monitorování** klikněte na **stav synchronizace bodu aktualizace softwaru**.  

   Body aktualizace softwaru ve vaší hierarchii Configuration Manager se zobrazí v podokně výsledků. Z tohoto hlediska můžete sledovat stav synchronizace všech míst aktualizace softwaru. Podrobnější informace o procesu synchronizace najdete v souboru wsyncmgr.log, který se nachází na jednotlivých serverech lokality v umístění <*instalační_cesta_ConfigMgru*>\Logs.  

## <a name="import-updates-from-the-microsoft-update-catalog"></a>Import aktualizací z katalogu Microsoft Update

Bod aktualizace softwaru nejvyšší úrovně používá službu WSUS k získání informací o aktualizacích softwaru od Microsoftu do Configuration Manager. V některých případech možná budete potřebovat aktualizaci, která se automaticky nesynchronizuje do WSUS pro vybrané produkty a klasifikace, ale je dostupná v [katalogu Microsoft Update](https://catalog.update.microsoft.com). Aktualizace, které se automaticky nesynchronizují do služby WSUS, jsou obvykle určeny k řešení vysoce specifických problémů. Pokud je aktualizace v katalogu dostupná, můžete ji importovat do služby WSUS. Pak ho můžete synchronizovat do Configuration Manager a nasadit jako jakoukoli jinou aktualizaci.

### <a name="to-import-an-update-from-the-microsoft-update-catalog"></a>Import aktualizace z katalogu Microsoft Update

1. Otevřete konzolu pro správu služby WSUS a připojte ji k serveru WSUS nejvyšší úrovně ve vaší hierarchii.
   - Pokud Internet Explorer není výchozím webovým prohlížečem počítače, dočasně ho nastavte jako výchozí.
2. Klikněte na **aktualizace** nebo na název serveru WSUS. 
3. V podokně **Akce** vyberte **Importovat aktualizace...** tím otevřete okno prohlížeče pro [katalog Microsoft Update](https://catalog.update.microsoft.com).
   ![V konzole WSUS vyberte Importovat aktualizace.](media/wsus-console-import-updates.png)
4. Pokud se zobrazí výzva, nainstalujte ovládací prvek ActiveX katalogu Microsoft Update. Pro import aktualizací do služby WSUS musí být nainstalován ovládací prvek. 
5. V okně prohlížeče vyhledejte aktualizaci, kterou chcete. Kliknutím na tlačítko **Přidat*** ho přidáte do košíku.
6. Klikněte na **Zobrazit košík**. Ujistěte se, že je vybraná možnost **importovat přímo do Windows Server Update Services** . Pak klikněte na **importovat**.
    ![Import aktualizace z katalogu do služby WSUS](./media/import-catalog-update-into-wsus.png)
7. Po dokončení importu klikněte v okně prohlížeče na **Zavřít** .
     - V případě potřeby obnovte výchozí prohlížeč.
8. Synchronizujte Configuration Manager bod aktualizace softwaru.


## <a name="next-steps"></a>Další kroky
Po první synchronizaci aktualizací softwaru nebo po dostupných nových klasifikací nebo dostupných produktech musíte [nakonfigurovat nové klasifikace a produkty](configure-classifications-and-products.md) pro synchronizaci aktualizací softwaru s novými kritérii.

Po synchronizaci aktualizací softwaru s požadovanými kritérii [Spravujte nastavení pro aktualizace softwaru](manage-settings-for-software-updates.md).  
