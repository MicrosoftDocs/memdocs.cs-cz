---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 05/28/2019
ms.openlocfilehash: e5c15556a7a8dd91db3ae2c4aa4f9830abc8e430
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724108"
---
## <a name="apply-software-updates-to-an-image"></a><a name="BKMK_OSImagesApplyUpdates"></a>Použití aktualizací softwaru na bitovou kopii

> [!Note]  
> Tato část se vztahuje na **image operačních systémů** i **balíčky s upgradem operačního systému**. K odkazování na soubor bitové kopie systému Windows (WIM) se používá obecný pojem "image". Oba tyto objekty mají soubor WIM, který obsahuje instalační soubory systému Windows. Aktualizace softwaru se vztahují na tyto soubory v obou objektech. Chování tohoto procesu je stejné mezi oběma objekty.  

Každý měsíc jsou pro Image k dispozici nové aktualizace softwaru. Než budete moci použít aktualizace softwaru, budete potřebovat následující požadavky:

- Infrastruktura aktualizací softwaru  
- Aktualizace softwaru byly úspěšně synchronizovány  
- Stažení aktualizací softwaru do knihovny obsahu na serveru lokality  

Další informace najdete v tématu [nasazení aktualizací softwaru](../../../sum/deploy-use/deploy-software-updates.md).  

Použít příslušné aktualizace softwaru na obrázek podle zadaného plánu. Tento proces se někdy nazývá *Údržba offline*. V tomto plánu Configuration Manager aplikuje vybrané aktualizace softwaru na bitovou kopii. Pak může také znovu distribuovat aktualizovanou bitovou kopii do distribučních bodů.

> [!Important]  
> I když můžete vybrat jakoukoli aktualizaci softwaru, která se vztahuje na image na základě verze, DISM může použít jenom určité typy aktualizací pro image. V souboru **OfflineServicingMgr. log** se zobrazí následující položka: `Not applying this update binary, it is not supported`.<!-- SCCMDocs issue 1324 -->

Databáze lokality obsahuje informace o imagi, včetně aktualizací softwaru použitých v době importu. Aktualizace softwaru, které pro bitovou kopii použijete po jejím úvodním přidání, jsou uloženy také v databázi lokality. Když spustíte Průvodce pro použití aktualizací softwaru, načte seznam použitelných aktualizací softwaru, které lokalita ještě pro Image nepoužila. Configuration Manager zkopíruje aktualizace softwaru, které jste vybrali z knihovny obsahu na serveru lokality. Pak použije aktualizace softwaru na bitovou kopii.  

### <a name="servicing-process"></a>Proces údržby

1. V konzole Configuration Manager klikněte na pracovní prostor **softwarová knihovna** , rozbalte možnost **operační systémy**a potom vyberte možnost **bitové kopie operačního systému** nebo **balíčky s upgradem operačního systému**.  

2. Vyberte objekt, pro který chcete použít aktualizace softwaru.  

3. Na pásu karet vyberte **naplánovat aktualizace** a spusťte tak průvodce.  

4. Na stránce **Vybrat aktualizace** vyberte aktualizace softwaru, které se mají použít na bitovou kopii. Zobrazení seznamu aktualizací v průvodci může nějakou dobu trvat. Pomocí **filtru** vyhledejte řetězce v metadatech. Pomocí rozevíracího seznamu **Architektura systému** můžete filtrovat podle **x86**, **x64**nebo **všech**. V seznamu můžete vybrat jednu, mnoho nebo všechny aktualizace. Až budete hotovi s výběrem možnosti aktualizace, vyberte **Další**.  

5. Na stránce **Nastavení plánu** nakonfigurujte následující nastavení a klikněte na tlačítko **Další**.  

    1. **Plán**: Určete plán, kdy má lokalita použít aktualizace softwaru na bitovou kopii.  

    2. **Pokračovat při chybě**: tuto možnost vyberte, pokud chcete v instalaci aktualizací softwaru do image pokračovat, i když dojde k chybě.  

    3. **Aktualizovat distribuční body s imagí**: tuto možnost vyberte, pokud chcete aktualizovat bitovou kopii v distribučních bodech poté, co lokalita nainstaluje aktualizace softwaru.  

6. Dokončete průvodce plánováním aktualizací.  

> [!NOTE]  
> Chcete-li minimalizovat velikost datové části, bude údržba balíčků s upgradem operačního systému a bitových kopií operačního systému odebrána ze starší verze.  

### <a name="servicing-operations"></a>Operace údržby

V konzole Configuration Manager v uzlu **image operačního systému** nebo balíčky s **upgradem operačního systému** přidejte do zobrazení následující sloupce:

- **Datum plánované aktualizace**: Tato vlastnost zobrazuje další plán, který jste definovali.  
- **Stav naplánované aktualizace**: Tato vlastnost zobrazuje stav. Například **úspěch** nebo **v procesu**.  

Vyberte objekt konkrétní obrázek a potom v podokně podrobností přepněte na kartu **stav aktualizace** . Tato karta zobrazuje seznam aktualizací v imagi.

Vyberte objekt konkrétní obrázek a na pásu karet vyberte možnost **vlastnosti** . Karta **nainstalované aktualizace** zobrazuje seznam aktualizací v imagi. Karta **Údržba** je zobrazení aktuálního plánu údržby jen pro čtení a aktualizace, které jste naplánovali použít.

Když je stav **v procesu**, můžete na pásu karet vybrat **zrušit plánované aktualizace** . Tato akce zruší aktivní proces údržby.

Pokud chcete tento proces vyřešit, Prohlédněte si soubory **OfflineServicingMgr. log** a **DISM. log** na serveru lokality. Další informace najdete v tématu [soubory protokolu](../../../core/plan-design/hierarchy/log-files.md).

### <a name="specify-the-drive-for-offline-os-image-servicing"></a><a name="bkmk_servicing-drive"></a>Zadejte jednotku pro obsluhu bitové kopie operačního systému offline

<!--1358924-->

Počínaje verzí 1810 zadejte jednotku, kterou Configuration Manager používá během offline údržby imagí operačního systému. Tento proces může využívat velké množství místa na disku s dočasnými soubory. Tato možnost nabízí flexibilitu při výběru jednotky, která se má použít.

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** . Na pásu karet klikněte na položku **Konfigurovat součásti webu** a vyberte možnost **nasazení operačního systému**.  

2. Na kartě **Offline údržba** Určete možnost, jakou **má místní jednotka používat offline údržbu imagí**.  

Ve výchozím nastavení je toto nastavení **Automatické**. S touto hodnotou Configuration Manager vybere jednotku, na které je nainstalována.

Pokud vyberete jednotku, která na serveru lokality neexistuje, Configuration Manager se chovají stejně, jako byste vybrali možnost **automaticky**.

Během offline údržby Configuration Manager ukládá do složky dočasné soubory `<drive>:\ConfigMgr_OfflineImageServicing`. Také připojí bitovou kopii operačního systému do této složky.

### <a name="optimized-image-servicing"></a><a name="bkmk_resetbase"></a>Optimalizovaná údržba imagí

<!--3555951-->

Počínaje verzí 1902 platí, že při použití aktualizací softwaru pro image operačního systému je k dispozici nová možnost optimalizace výstupu odebráním všech nahrazených aktualizací. Optimalizace na offline údržbu platí jenom pro image s jedním indexem.

Když naplánujete, aby lokalita používala aktualizace softwaru pro image operačního systému, použije nástroj příkazového řádku Obsluha a správa bitových kopií (DISM) pro nasazení systému Windows. Během procesu údržby Tato změna zavádí následující dva další kroky:  

- Spustí nástroj DISM proti připojené offline imagi s parametry `/Cleanup-Image /StartComponentCleanup /ResetBase`. Pokud tento příkaz neproběhne úspěšně, aktuální proces obsluhy se nezdařil. Nepotvrdí žádné změny v imagi.  

- Po Configuration Manager potvrdí změny v imagi a odpojí je od systému souborů, exportuje image do jiného souboru. Tento krok používá parametr `/Export-Image`DISM. Z image se odeberou nepotřebné soubory, což zmenšuje velikost.  

Společnost Microsoft doporučuje, abyste pravidelně použili aktualizace pro offline image. Tuto možnost nemusíte používat při každé změně služby image. Když tento proces provedete každý měsíc, tato nová možnost poskytuje největší přínos v průběhu času. Další informace najdete v tématu [doporučení pro krok instalovat aktualizace softwaru](../../understand/install-software-updates.md#recommendations).

I když tato možnost pomáhá snižovat celkovou velikost bitové kopie, trvá to déle, než proces dokončí. Pomocí Průvodce můžete naplánovat obsluhu během pohodlných časů. Vyžaduje také další úložiště na serveru lokality. Lokalitu můžete přizpůsobit tak, aby používala alternativní umístění. Další informace najdete v tématu [určení jednotky pro obsluhu bitové kopie operačního systému offline](#bkmk_servicing-drive).

#### <a name="process-to-optimize-image-servicing"></a>Postup optimalizace obsluhy imagí

1. Spusťte [proces údržby](#servicing-process).  

2. Na stránce **nastavit plán** vyberte možnost **Odebrání nahrazených aktualizací po aktualizaci obrázku**. Tato možnost není automaticky povolena. Pokud má obrázek více než jeden index, nemůžete použít tuto možnost.  

3. Chcete-li naplánovat obsluhu bitové kopie, dokončete průvodce.  

Ověří a monitorujte proces pomocí **protokolu offlineServicing. log**.
