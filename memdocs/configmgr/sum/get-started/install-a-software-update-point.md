---
title: Instalace a konfigurace bodu aktualizace softwaru
titleSuffix: Configuration Manager
description: Primární lokality vyžadují bod aktualizace softwaru v lokalitě centrální správy pro vyhodnocení shody aktualizací softwaru a nasazení aktualizací softwaru do klientů.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/16/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b099a645-6434-498f-a408-1d438e394396
ms.openlocfilehash: 1f3ab3c108a7f8481aee84b6df5cd41b4b186246
ms.sourcegitcommit: 6176a7825d6c663faa318a6818b7764bc70f08fc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/17/2020
ms.locfileid: "90718837"
---
# <a name="install-and-configure-a-software-update-point"></a>Instalace a konfigurace bodu aktualizace softwaru  

*Platí pro: Configuration Manager (Current Branch)*


> [!IMPORTANT]  
>  Než nainstalujete roli systému lokality bodu aktualizace softwaru (SUP), je nutné ověřit, že server splňuje požadované závislosti a určuje infrastrukturu bodu aktualizace softwaru v lokalitě. Další informace o plánování aktualizací softwaru a určení infrastruktury bodu aktualizace softwaru najdete v tématu [Plánování aktualizací softwaru](../plan-design/plan-for-software-updates.md).  

 Bod aktualizace softwaru je vyžadován v lokalitě centrální správy a v primárních lokalitách, aby bylo možné vyhodnotit dodržování předpisů aktualizací softwaru a nasazovat aktualizace softwaru na klienty nástroje. Bod aktualizace softwaru je volitelně v sekundárních lokalitách. Na serveru s nainstalovanou službou WSUS musí být vytvořena role systému lokality bodu aktualizace softwaru. Bod aktualizace softwaru se službou WSUS komunikuje za účelem konfigurace nastavení aktualizací softwaru a vyžádání synchronizace metadat aktualizace softwaru. Pokud máte hierarchii Configuration Manager, nainstalujte a nakonfigurujte nejprve bod aktualizace softwaru v lokalitě centrální správy, poté v podřízených primárních lokalitách a volitelně i v sekundárních lokalitách. Máte-li samostatnou primární lokalitu, a ne lokalitu centrální správy, nainstalujte a nakonfigurujte nejprve bod aktualizace softwaru v primární lokalitě a poté volitelně v sekundárních lokalitách. Některá nastavení jsou dostupná pouze při konfiguraci bodu aktualizace softwaru v lokalitě vysoké úrovně. V závislosti na místě instalace bodu aktualizace softwaru existují tři různé možnosti konfigurace.  

> [!IMPORTANT]  
>  V lokalitě můžete instalovat víc bodů aktualizace softwaru. První bod aktualizace softwaru, který nainstalujete, je nakonfigurován jako zdroj synchronizací, který synchronizuje aktualizace ze služby Microsoft Update nebo ze zdroje synchronizací pro odesílání dat. Ostatní body aktualizace softwaru v lokalitě jsou nakonfigurovány jako repliky prvního bodu aktualizace softwaru. Některá nastavení proto nejsou po nainstalování a nakonfigurování prvního bodu aktualizace softwaru k dispozici.  

> [!IMPORTANT]  
>  Instalace role systému lokality bodu aktualizace softwaru na server, který byl nakonfigurován a použit jako samostatný server WSUS, nebo pomocí bodu aktualizace softwaru pro přímou správu klientů služby WSUS, není podporována. Existující servery WSUS se podporují jenom jako nadřazené zdroje synchronizace pro aktivní bod aktualizace softwaru. Viz [synchronizace z umístění nadřazeného zdroje dat](#BKMK_wsussync) .

 Roli systému lokality bodu aktualizace softwaru můžete přidat na existující server systému lokalit nebo vytvořit nový server. Na stránce **Výběr role systému** v **Průvodci vytvořením serveru systému lokality** nebo **Průvodce přidáním rolí systému lokality**v závislosti na tom, zda přidáváte roli systému lokality na nový nebo existující server lokality, vyberte možnost **bod aktualizace softwaru**a poté nakonfigurujte nastavení bodu aktualizace softwaru v průvodci. Nastavení se liší v závislosti na používané verzi Configuration Manager. Další informace o instalaci rolí systému lokality najdete v tématu [Instalace rolí systému lokality](../../core/servers/deploy/configure/install-site-system-roles.md).  

 Následující části podávají informace o nastavení bodu aktualizace softwaru v lokalitě.  

## <a name="proxy-server-settings"></a>Nastavení serveru proxy  
 Nastavení proxy server můžete nakonfigurovat na různých stránkách **Průvodce vytvořením serveru systému lokality** nebo **Průvodce přidáním rolí systému lokality** v závislosti na používané verzi Configuration Manager.  

-   Proveďte konfiguraci serveru proxy a určete, kdy má být server proxy pro aktualizace softwaru používán. Nakonfigurujte tahle nastavení:  

    -   Nakonfigurujte nastavení serveru proxy na stránce **Proxy** průvodce nebo na kartě **Proxy** ve vlastnostech systému lokality. Nastavení proxy server jsou specifická pro systém lokality, což znamená, že všechny role systému lokality používají nastavení proxy server, která zadáte.  

    -   Určete, jestli se má použít proxy server, když Configuration Manager synchronizuje aktualizace softwaru a když stahuje obsah pomocí pravidla automatického nasazení. Na stránce **Nastavení serveru proxy a účtu** průvodce nebo na kartě **Nastavení serveru proxy a účtu** ve vlastnostech bodu aktualizace softwaru nakonfigurujte nastavení serveru proxy bodu aktualizace softwaru.  

        > [!NOTE]  
        >  Nastavení **Při stahování obsahu pomocí pravidel automatického nasazení použít server proxy** je dostupné, ale pro bod aktualizace softwaru v sekundární lokalitě se nepoužívá. Obsah ze stránky Microsoft Update stahuje pouze bod aktualizace softwaru v lokalitě centrální správy a v primární lokalitě.  

> [!IMPORTANT]  
>  K připojení k Internetu a stahování aktualizací softwaru při spuštěných pravidlech automatického nasazení se standardně používá účet **Místní systém** pro server, na kterém je vytvořené pravidlo automatického nasazení. Pokud nemá tento účet přístup k internetu, stažení aktualizací softwaru nebude úspěšné a do souboru ruleengine.log se přidá tento záznam: **Nepodařilo se stáhnout aktualizaci z internetu. Error = 12007**. Pokud nemá účet místního systému přístup k Internetu, nakonfigurujte pověření pro připojení k serveru proxy.  


## <a name="wsus-settings"></a>Nastavení služby WSUS  
 Nastavení služby WSUS musíte nakonfigurovat na různých stránkách **Průvodce vytvořením serveru systému lokality** nebo **Průvodce přidáním rolí systému lokality** v závislosti na používané verzi Configuration Manager a v některých případech pouze ve vlastnostech bodu aktualizace softwaru, označovaného také jako vlastnosti komponenty bodu aktualizace softwaru. Informace v následujících částech slouží ke konfiguraci nastavení služby WSUS.  

### <a name="wsus-port-settings"></a><a name="BKMK_wsusport"></a>Nastavení portu služby WSUS  
 Nastavení portu služby WSUS nakonfigurujete na stránce Bod aktualizace softwaru v průvodci nebo ve vlastnostech bodu aktualizace softwaru. K určení nastavení portu, která se používají službou WSUS, použijte následující postup.  

#### <a name="to-determine-the-port-settings-used-in-iis"></a>Určení nastavení portu používaných ve službě IIS  

 1.  Na serveru služby WSUS otevřete správce služby Internet Information Services (IIS).  

 2.  Rozbalte seznam **Lokality**, klikněte pravým tlačítkem na server služby WSUS a pak klikněte na položku **Upravit vazby**. V dialogovém okně Vazby lokality se ve sloupci **Port** zobrazí hodnoty portů HTTP a HTTPS.


### <a name="configure-ssl-communications-to-wsus"></a>Konfigurace komunikace SSL se službou WSUS  
 Komunikaci SSL můžete nakonfigurovat na stránce průvodce **Obecné** nebo na kartě **Obecné** ve vlastnostech bodu aktualizace softwaru.  

 Další informace o použití protokolu SSL najdete v tématu [rozhodnutí, jestli se má služba WSUS nakonfigurovat tak, aby používala protokol SSL](../plan-design/plan-for-software-updates.md#BKMK_WSUSandSSL) , a [nakonfigurujte bod aktualizace softwaru tak, aby používal protokol TLS/SSL s certifikátem PKI](../get-started/software-update-point-ssl.md).  

### <a name="wsus-server-connection-account"></a>Účet připojení serveru služby WSUS  
 Můžete nastavit účet, který má server lokality používat při připojení do služby WSUS běžící v bodě aktualizace softwaru. Pokud tento účet nenakonfigurujete, používá Configuration Manager k připojení ke službě WSUS účet počítače pro server lokality. Na stránce **Nastavení serveru proxy a účtu** v průvodci nebo na kartě **Nastavení serveru proxy a účtu** ve vlastnostech bodu aktualizace softwaru nakonfigurujte účet pro připojení serveru WSUS.  V závislosti na používané verzi Configuration Manager můžete účet nakonfigurovat na různých místech průvodce.  

 Další informace o účtech Configuration Manager najdete v tématu [použití účtů](../../core/plan-design/hierarchy/accounts.md).  

## <a name="synchronization-source"></a>Zdroj synchronizace  
 Můžete nakonfigurovat nadřazený zdroj synchronizace pro synchronizaci aktualizací softwaru na stránce **zdroj synchronizace** v průvodci nebo na kartě **Nastavení synchronizace** ve vlastnostech komponenty bodu aktualizace softwaru. Možnosti nastavení zdroje synchronizace se podle konkrétní stránky liší.  

 V následující tabulce naleznete možnosti dostupné při konfiguraci bodu aktualizace softwaru v lokalitě.  

|Web|Dostupné možnosti nastavení zdroje synchronizace|  
|----------|----------------------------------------------|  
|- Lokalita centrální správy<br />- Samostatná primární lokalita|- Synchronizovat ze služby Microsoft Update<br />- Synchronizovat z umístění nadřazeného zdroje dat<br />- Nesynchronizovat ze služby Microsoft Update nebo z nadřazeného zdroje dat|  
|- Další body aktualizace softwaru v lokalitě<br />- Podřízená primární lokalita<br />- Sekundární lokalita|- Synchronizovat z umístění nadřazeného zdroje dat|  

 Následující seznam uvádí další informace o jednotlivých možnostech, jež lze použít jako zdroj synchronizace:  

-   **Synchronizovat ze služby Microsoft Update**: Při tomto nastavení se budou synchronizovat metadata aktualizace softwaru ze služby Microsoft Update. Lokalita centrální správy musí mít přístup k internetu, jinak nebude synchronizace úspěšná. Toto nastavení je dostupné pouze při konfiguraci bodu aktualizace softwaru v lokalitě vysoké úrovně.  

    > [!NOTE]  
    >  Pokud je mezi bodem aktualizace softwaru a internetem brána firewall, může být potřeba nakonfigurovat ji tak, aby podporovala porty HTTP a HTTPS použité pro web služby WSUS. Přístup na bráně firewall však můžete také omezit na vybrané domény. Další informace o naplánování brány firewall podporující aktualizace softwaru najdete v tématu [Konfigurace bran firewall](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

-   ** <a name="BKMK_wsussync"></a> Synchronizovat z umístění nadřazeného zdroje dat**: pomocí tohoto nastavení můžete synchronizovat metadata aktualizací softwaru z nadřazeného zdroje synchronizací. Podřízené primární lokality a sekundární lokality budou automaticky nakonfigurovány tak, aby využívaly adresu URL nadřazené lokality pro toto nastavení. Můžete nastavit synchronizaci aktualizací softwaru z existujícího serveru služby WSUS. Zadejte adresu URL, například `https://WSUSServer:8531` , kde 8531 je port, který se používá pro připojení k serveru WSUS.  

-   **Nesynchronizovat ze služby Microsoft Update nebo z nadřazeného zdroje dat**: Při tomto nastavení se budou při odpojení bodu aktualizace softwaru na nejvyšší úrovni od Internetu synchronizovat aktualizace softwaru ručně. Další informace najdete v tématu [Synchronizace aktualizací softwaru z odpojeného bodu aktualizace softwaru](synchronize-software-updates-disconnected.md).  

> [!NOTE]  
>  Pokud je mezi bodem aktualizace softwaru a internetem brána firewall, může být potřeba nakonfigurovat ji tak, aby podporovala porty HTTP a HTTPS použité pro web služby WSUS. Přístup na bráně firewall však můžete také omezit na vybrané domény. Další informace o naplánování brány firewall podporující aktualizace softwaru najdete v tématu [Konfigurace bran firewall](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

 Na stránce **zdroj synchronizace** v průvodci nebo na kartě **Nastavení synchronizace** ve vlastnostech komponenty bodu aktualizace softwaru můžete také nastavit, zda se mají vytvářet události vytváření sestav služby WSUS. Configuration Manager tyto události nepoužívá; Proto budete normálně volit výchozí nastavení **Nevytvářet události vytváření sestav služby WSUS**.  

## <a name="synchronization-schedule"></a>Plán synchronizace  
 Na stránce průvodce **Plán synchronizace** nebo v okně Vlastnosti komponenty bodu aktualizace softwaru nakonfigurujte plán synchronizace. Konfigurace tohoto nastavení se provádí pouze v bodu aktualizace softwaru v lokalitě nejvyšší úrovně.  

 Pokud povolíte plán synchronizace, lze nastavit pravidelný jednoduchý nebo vlastní plán. Při konfiguraci jednoduchého plánu je čas spuštění založen na místním času počítače, na kterém je spuštěna konzola Configuration Manager v době, kdy plán vytvoříte. Když nakonfigurujete čas zahájení pro vlastní plán, bude vycházet z místního času počítače, na kterém je spuštěna konzola Configuration Manager.  

> [!TIP]  
>  Spouštění synchronizace aktualizací softwaru naplánujte pomocí časového rámce, který bude vhodný pro vaše prostředí. Jednou z typických možností je nastavit plán synchronizace aktualizací softwaru na okamžik krátce po vydání pravidelných bezpečnostních aktualizací Microsoft každé druhé úterý v měsíci (tzv. Patch Tuesday). Pokud používáte aktualizace softwaru k distribuci definice aplikace Endpoint Protection a aktualizacím modulů, další z typických možností je nastavit plán synchronizace aktualizací softwaru na každodenní spouštění.  

> [!NOTE]  
>  Pokud nepovolíte synchronizaci aktualizací softwaru podle plánu, můžete je z uzlu **Všechny aktualizace softwaru** nebo **Skupiny aktualizací softwaru** v pracovním prostoru Softwarová knihovna synchronizovat ručně. Další informace najdete v tématu [synchronizace aktualizací softwaru](synchronize-software-updates.md).  

## <a name="supersedence-rules"></a>Pravidla nahrazení  
 Na stránce průvodce **Pravidla nahrazení** nebo na kartě **Pravidla nahrazení** v okně Vlastnosti komponenty bodu aktualizace softwaru nakonfigurujte pravidla nahrazení. Pravidla lze nastavit pouze v lokalitě vysoké úrovně. Od verze Configuration Manager 1810 můžete určit chování pravidel nahrazení pro **aktualizace funkcí** odděleně od **aktualizací bez funkcí**. <!--3098809, 2977644-->

 Na této stránce můžete nastavit, zda má platnost nahrazených aktualizací softwaru okamžitě skončit. Nahrazené aktualizace tak nebudou zahrnuty do nových nasazení a existující nasazení budou označena příznakem, který bude sdělovat, že nahrazené aktualizace softwaru obsahují přinejmenším jednu aktualizaci s vypršenou dobou platnosti. Nebo můžete nastavit dobu před tím, než skončí platnost nahrazené aktualizace softwaru. V takovém případě lze ještě aktualizace po určitou dobu nasadit. Další informace najdete v části [Pravidla nahrazení](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

> [!NOTE]  
>  Stránka průvodce **Pravidla nahrazení** je dostupná až po nakonfigurování prvního bodu aktualizace softwaru v lokalitě. Tato stránka se nezobrazí, pokud nainstalujete další body aktualizace softwaru.  

## <a name="classifications"></a>Klasifikace  
 Na stránce průvodce **klasifikace** nebo na kartě **klasifikace** ve vlastnostech komponenty bodu aktualizace softwaru nakonfigurujte nastavení klasifikací. Další informace o klasifikacích aktualizací softwaru najdete v části [Klasifikace aktualizací](../plan-design/plan-for-software-updates.md#BKMK_UpdateClassifications).  

> [!NOTE]  
>  Stránka průvodce **Klasifikace** je dostupná až po nakonfigurování prvního bodu aktualizace softwaru v lokalitě. Tato stránka se nezobrazí, pokud nainstalujete další body aktualizace softwaru.  

> [!TIP]  
>  Při první instalaci bodu aktualizace softwaru v lokalitě nejvyšší úrovně vymažte všechny klasifikace aktualizací softwaru. Po první synchronizaci aktualizací softwaru nakonfigurujte klasifikace z aktualizovaného seznamu a inicializujte novou synchronizaci. Konfigurace tohoto nastavení se provádí pouze v bodu aktualizace softwaru v lokalitě nejvyšší úrovně.  

## <a name="products"></a>Produkty  
 Proveďte konfiguraci nastavení produktu na stránce **produkty** v průvodci nebo na kartě **produkty** ve vlastnostech komponenty bodu aktualizace softwaru.  

> [!NOTE]  
>  Stránka průvodce **Produkty** je dostupná až po nakonfigurování prvního bodu aktualizace softwaru v lokalitě. Tato stránka se nezobrazí, pokud nainstalujete další body aktualizace softwaru.  

> [!TIP]  
>  Při první instalaci bodu aktualizace softwaru v lokalitě nejvyšší úrovně vymažte všechny produkty. Po první synchronizaci aktualizací softwaru nakonfigurujte produkty z aktualizovaného seznamu a inicializujte novou synchronizaci. Konfigurace tohoto nastavení se provádí pouze v bodu aktualizace softwaru v lokalitě nejvyšší úrovně.  

## <a name="languages"></a>Jazyky  
 Na stránce průvodce **jazyky** nebo na kartě **jazyky** ve vlastnostech komponenty bodu aktualizace softwaru nakonfigurujte nastavení jazyka. Zadejte jazyky, pro něž chcete synchronizovat soubory aktualizace softwaru a souhrnné detaily. Nastavení **souboru aktualizace softwaru** se konfiguruje v každém bodu aktualizace softwaru v hierarchii Configuration Manager. Nastavení **Souhrnné detaily** se konfiguruje jenom v bodě aktualizace softwaru nejvyšší úrovně. Další informace najdete v části [Jazyky](../plan-design/plan-for-software-updates.md#BKMK_UpdateLanguages).  

> [!NOTE]  
>  Stránka průvodce **Jazyky** je dostupná až po nainstalování bodu aktualizace softwaru v lokalitě centrální správy. Jazyky souboru aktualizace softwaru se dají nakonfigurovat v podřízených lokalitách na kartě **Jazyky** v okně Vlastnosti komponenty bodu aktualizace softwaru.  

## <a name="third-party-updates"></a>Aktualizace třetích stran
Od verze Configuration Manager 1802 můžete povolit aktualizace třetích stran pro klienty Configuration Manager. Když ve vlastnostech komponenty SUP povolíte aktualizace softwaru třetích stran, načte soubor SUP podpisový certifikát používaný službou WSUS pro aktualizace třetích stran. Tato možnost není k dispozici během instalace bodu aktualizace softwaru a měla by být nakonfigurována po instalaci aktualizace SUP. Pokud chcete povolit nastavení klienta pro aktualizace jiných výrobců, přečtěte si článek [o nastavení klienta](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates) .

## <a name="next-steps"></a>Další kroky
Nainstalovali jste bod aktualizace softwaru od nejvyšší lokality v hierarchii Configuration Manager. Zopakováním postupů v tomto článku nainstalujete bod aktualizace softwaru v podřízených lokalitách.

Jakmile budete mít nainstalované body aktualizace softwaru, přečtěte si informace o [synchronizaci aktualizací softwaru](synchronize-software-updates.md).
