---
title: Správa distribučních bodů
titleSuffix: Configuration Manager
description: Pomocí distribučních bodů můžete hostovat obsah, který nasadíte do zařízení a uživatelů.
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d1d93dd446a65fda0b259bb10e0c944780d41059
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347087"
---
# <a name="install-and-configure-distribution-points-in-configuration-manager"></a>Instalace a konfigurace distribučních bodů v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Nainstalujte Configuration Manager distribuční body, které budou hostovat soubory obsahu, které nasadíte do zařízení a uživatelů. Vytvořte skupiny distribučních bodů pro zjednodušení správy distribučních bodů a způsobu distribuce obsahu do distribučních bodů.  

*Nový distribuční bod nainstalujete* pomocí Průvodce instalací nástroje. Další informace najdete v tématu [instalace distribučního bodu](#bkmk_install). Chcete-li *Spravovat vlastnosti stávajícího distribučního bodu*, upravte vlastnosti distribučního bodu. Další informace najdete v tématu [Konfigurace distribučního bodu](#bkmk_configs).

Nakonfigurujte většinu nastavení distribučního bodu pomocí obou metod. Několik nastavení je k dispozici pouze při instalaci nebo úpravách, ale ne v obou těchto případech:  

- Nastavení, která jsou k dispozici pouze při instalaci distribučního bodu:  

    - **Povolení Configuration Manager instalace služby IIS na počítači distribučního bodu**

    - **Konfigurace nastavení místa na jednotce pro distribuční bod**  

- Nastavení, která jsou k dispozici pouze při úpravě vlastností distribučního bodu:  

    - **Správa vztahů skupin distribučních bodů**  

    - **Zobrazit obsah nasazený do distribučního bodu**  

    - **Konfigurace omezení přenosové rychlosti pro přenosy dat do distribučních bodů**  

    - **Konfigurace plánů pro přenos dat do distribučních bodů**  


## <a name="install-a-distribution-point"></a><a name="bkmk_install"></a>Instalace distribučního bodu  

Vyberte server systému lokality jako distribuční bod, aby bylo možné obsah zpřístupnit klientským počítačům. Přiřaďte distribuční bod alespoň jedné [skupině hranic](boundary-groups.md#distribution-points) předtím, než mohou místní klientské počítače použít tento distribuční bod jako umístění zdroje obsahu. Přidejte roli distribučního bodu k novému serveru systému lokality nebo ho přidejte na existující server systému lokality.

### <a name="prerequisites"></a><a name="bkmk_install-prereq"></a>Požadovaný

Při instalaci nového distribučního bodu použijete Průvodce instalací, který vás provede dostupnými nastaveními. Než začnete, vezměte v úvahu následující požadavky:  

- K vytvoření a konfiguraci distribučního bodu je nutné mít následující oprávnění zabezpečení:  

    - **Číst** pro objekt **distribučního bodu**  

    - **Kopírovat do distribučního bodu** pro objekt **distribučního bodu**  

    - **Upravit** pro objekt **lokalita**  

    - **Správa certifikátů pro nasazení operačního systému** pro objekt **lokalita**  

- Nainstalujte Internetová informační služba (IIS) na Windows Server, který je hostitelem distribučního bodu. Když nainstalujete roli systému lokality, Configuration Manager může nainstalovat a nakonfigurovat službu IIS.  

### <a name="procedure-to-install-a-distribution-point"></a><a name="bkmk_install-procedure"></a>Postup instalace distribučního bodu  

Tento postup slouží k přidání nového distribučního bodu. Chcete-li změnit konfiguraci existujícího distribučního bodu, přečtěte si část [Konfigurace distribučního bodu](#bkmk_configs) .  

Začněte s obecným postupem pro [instalaci rolí systému lokality](install-site-system-roles.md). Na stránce **Výběr role systému** v Průvodci vytvořením serveru systému lokality vyberte roli **distribuční bod** . Tato akce přidá do průvodce následující stránky:  

- [Distribuční bod](#bkmk_config-general)
- [Communication](#bkmk_config-comm)
- [Nastavení jednotky](#bkmk_config-drive)
- [Distribuční bod pro vyžádání obsahu](#bkmk_config-pull)
- [Nastavení PXE](#bkmk_config-pxe)
- [Odesílání](#bkmk_config-multicast)
- [Ověření obsahu](#bkmk_config-valid)
- [Skupiny hranic](#bkmk_config-boundary)

> [!Important]  
> Následující nastavení jsou k dispozici pouze při instalaci distribučního bodu:  
>
> - **Povolení Configuration Manager instalace služby IIS na počítači distribučního bodu**  
>
> - **Konfigurace nastavení místa na jednotce pro distribuční bod**  

Další informace o stránkách průvodce, které jsou specifické pro roli distribučního bodu, najdete v části [Konfigurace distribučního bodu](#bkmk_configs) . Pokud například chcete nainstalovat distribuční bod jako [distribuční bod pro vyžádání](#bkmk_config-pull)obsahu, vyberte možnost **Povolit tomuto distribučnímu bodu vyžádání obsahu z jiných distribučních bodů**. Pak proveďte další konfigurace, které vyžadují distribuční body pro vyžádání obsahu.  

Po dokončení Průvodce vytvořením serveru systému lokality přidá lokalita roli distribučního bodu na server systému lokality.  


## <a name="manage-distribution-point-groups"></a><a name="bkmk_manage"></a>Správa skupin distribučních bodů  

Skupiny distribučních bodů poskytují možnost logického seskupování distribučních bodů k distribuci obsahu. Pomocí těchto skupin můžete spravovat a monitorovat obsah z centrálního umístění pro distribuční body, které jsou rozloženy na více lokalitách. Mějte na paměti následující body:

- Přidejte jeden nebo více distribučních bodů ze všech lokalit v hierarchii do skupiny distribučních bodů.  

- Přidat distribuční bod do více než jedné skupiny distribučních bodů.  

- Když distribuujete obsah do skupiny distribučních bodů, Configuration Manager distribuuje obsah do všech distribučních bodů, které jsou členy skupiny.  

- Pokud přidáte distribuční bod do skupiny po počáteční distribuci obsahu, Configuration Manager automaticky distribuuje obsah do nového člena distribučního bodu.  

- Přidružte kolekci ke skupině distribučních bodů. Když distribuujete obsah do této kolekce, Configuration Manager určuje, které skupiny jsou spojeny s kolekcí. Pak distribuuje obsah do všech distribučních bodů, které jsou členy těchto skupin.  

    > [!NOTE]  
    > Pokud po distribuci obsahu do kolekce přiřadíte kolekci k nové skupině distribučních bodů, je nutné obsah znovu distribuovat do kolekce, než bude obsah distribuován do nové skupiny distribučních bodů.  

V dalších oddílech jsou uvedeny postupy pro následující akce správy skupin distribučních bodů:  

- [Vytvoří a nakonfiguruje novou skupinu distribučních bodů.](#bkmk_dpgroup-create)
- [Úprava existující skupiny distribučních bodů](#bkmk_dpgroup-modify)
- [Přidat vybrané distribuční body do existujících skupin distribučních bodů](#bkmk_dpgroup-addexist)

### <a name="procedure-to-create-and-configure-a-new-distribution-point-group"></a><a name="bkmk_dpgroup-create"></a>Postup vytvoření a konfigurace nové skupiny distribučních bodů  

1. V konzole Configuration Manager přejděte do pracovního prostoru **Správa** a vyberte uzel **skupiny distribučních bodů** .  

2. Na pásu karet vyberte **vytvořit skupinu**.  

3. V okně vytvořit novou skupinu distribučních bodů zadejte **název**a volitelně také **Popis** skupiny.  

4. Na kartě **Členové** vyberte **Přidat**.  

5. V okně Přidat distribuční body vyberte jeden nebo více distribučních bodů, které chcete přidat jako členy skupiny. Pak zvolte **OK**.  

6. V případě potřeby přepněte na kartu **kolekce** v okně vytvořit novou skupinu distribučních bodů a vyberte **Přidat**.  

7. V okně vybrat kolekce vyberte kolekce, které chcete přidružit ke skupině distribučních bodů, a pak zvolte **OK**.  

8. V okně vytvořit novou skupinu distribučních bodů vytvořte skupinu kliknutím na **tlačítko OK** .  

#### <a name="create-a-new-group-from-an-existing-distribution-point"></a>Vytvoří novou skupinu z existujícího distribučního bodu.

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** a vyberte uzel **distribuční body** . Vyberte jeden nebo více distribučních bodů, které chcete přidat do nové skupiny distribučních bodů.  

2. Na pásu karet vyberte možnost **Přidat vybrané položky**a pak vyberte možnost **Přidat vybrané položky do nové skupiny distribučních bodů**.  

Tento proces automaticky vyplní kartu **Členové** okna vytvořit novou skupinu distribučních bodů s vybranými servery.

### <a name="procedure-to-modify-an-existing-distribution-point-group"></a><a name="bkmk_dpgroup-modify"></a>Postup úpravy existující skupiny distribučních bodů  

1. V konzole Configuration Manager přejděte do pracovního prostoru **Správa** a vyberte uzel **skupiny distribučních bodů** .  

2. Vyberte existující skupinu distribučních bodů, kterou chcete upravit. Na pásu karet vyberte možnost **vlastnosti**.  

3. Chcete-li přidružit nové kolekce k této skupině, přepněte na kartu **kolekce** a klikněte na tlačítko **Přidat**. Vyberte kolekce a pak zvolte **OK**.  

4. Chcete-li přidat do této skupiny nové distribuční body, přepněte na kartu **Členové** a klikněte na tlačítko **Přidat**. Vyberte distribuční body a klikněte na **tlačítko OK**.  

5. Kliknutím na **tlačítko OK** uložte změny do skupiny distribučních bodů.  

### <a name="procedure-to-add-selected-distribution-points-to-existing-distribution-point-groups"></a><a name="bkmk_dpgroup-addexist"></a>Postup přidání vybraných distribučních bodů do existujících skupin distribučních bodů  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** a vyberte uzel **distribuční body** . Vyberte jeden nebo více distribučních bodů, které chcete přidat do existující skupiny.  

2. Na pásu karet vyberte možnost **Přidat vybrané položky**a pak vyberte možnost **Přidat vybrané položky do existujících skupin distribučních bodů**.  

3. V části **Dostupné skupiny distribučních bodů**vyberte skupiny, do kterých budou vybrané distribuční body přidány jako členové. Pak zvolte **OK**.  


## <a name="reassign-a-distribution-point"></a><a name="bkmk_reassign"></a>Změna přiřazení distribučního bodu

<!-- 1306937 -->

Mnoho zákazníků má velké Configuration Manager infrastruktury a snižuje primární nebo sekundární lokalitu, aby se zjednodušilo jejich prostředí. Pořád potřebují uchovávat distribuční body v pobočkách, aby poskytovaly obsah spravovaným klientům. Tyto distribuční body často obsahují více terabajtů nebo více obsahu. Tento obsah je nákladný v čase a šířka pásma sítě pro distribuci na tyto vzdálené servery.

Tato funkce umožňuje změnit přiřazení distribučního bodu k jiné primární lokalitě bez nutnosti opětovné distribuce obsahu. Tato akce aktualizuje přiřazení systému lokality a uchovává veškerý obsah na serveru. Pokud potřebujete změnit přiřazení více distribučních bodů, nejprve tuto akci proveďte v jednom distribučním bodě. Pak pokračujte dalšími servery po jednom.

> [!IMPORTANT]  
> Cílový server může hostovat pouze roli distribučního bodu. Pokud je server systému lokality hostitelem jiné role serveru Configuration Manager, jako je například bod migrace stavu, nelze změnit přiřazení distribučního bodu. Nemůžete znovu přiřadit distribuční bod cloudu.

Před opětovným přiřazením distribučního bodu přidejte účet počítače cílového serveru lokality do skupiny místních správců na cílovém serveru distribučního bodu.

K opětovnému přiřazení distribučního bodu použijte následující postup:

1. V konzole Configuration Manager se připojte k lokalitě centrální správy.  

2. Otevřete pracovní prostor **Správa** a vyberte uzel **distribuční body** .  

3. Klikněte pravým tlačítkem myši na cílový distribuční bod a vyberte **změnit přiřazení distribučního bodu**.  

4. Vyberte cílový server lokality a kód lokality, pro které chcete změnit přiřazení distribučního bodu.  

Sledujte změnu přiřazení podobně jako při přidávání nové role. Nejjednodušším způsobem je aktualizovat zobrazení konzoly za několik minut. Přidejte do zobrazení sloupec Code (kód lokality). Tato hodnota se změní, když Configuration Manager znovu přiřadí server. Pokud se pokusíte provést jinou akci na cílovém serveru před aktualizací zobrazení konzoly, dojde k chybě "objekt nebyl nalezen". Ujistěte se, že je proces dokončený, a před zahájením jakýchkoli dalších akcí na serveru aktualizujte zobrazení konzoly.

Po opětovném přiřazení distribučního bodu aktualizujte certifikát serveru. Nový server lokality potřebuje tento certifikát znovu zašifrovat pomocí jeho veřejného klíče a uložit ho do databáze lokality. Další informace najdete v tématu **Vytvoření certifikátu podepsaného svým držitelem nebo Import klientského certifikátu infrastruktury veřejných klíčů (PKI) pro nastavení distribučního bodu** na kartě [Obecné](#bkmk_config-general) ve vlastnostech distribučního bodu.

- Pro certifikáty PKI nemusíte vytvářet nový certifikát. Importujte stejné. PFX a zadejte heslo.  

- U certifikátů podepsaných svým držitelem upravte datum nebo čas vypršení platnosti a aktualizujte je.  

- Pokud certifikát neaktualizujete, distribuční bod i nadále obsluhuje obsah, ale následující funkce selžou:  

    - Zprávy o ověření obsahu (Distmgr. log ukazuje, že nemůže dešifrovat certifikát)  

    - Podpora PXE pro klienty  

### <a name="tips"></a>Tipy

- Tuto akci proveďte z lokality centrální správy. Tento postup pomáhá při replikaci do primární lokality.  

- Nedistribuujte obsah na cílový server a pak se ho pokuste znovu přiřadit. Úlohy distribuce obsahu, které se právě zpracovávají, můžou během procesu opětovného přiřazování selhat, ale zkusíme to za normální.  

- Pokud je server také klientem Configuration Manager, nezapomeňte také znovu přiřadit klienta k nové primární lokalitě. Tento krok je zvláště důležitý pro distribuční body pro vyžádání obsahu, které používají součásti klienta ke stahování obsahu.  

- Tento proces odebere distribuční bod z výchozí skupiny hranic staré lokality. Pokud je to nutné, musíte ho do výchozí skupiny hranic nové lokality přidat ručně. Všechna ostatní přiřazení hraničních skupin zůstanou stejná.  


## <a name="maintenance-mode"></a><a name="bkmk_maint"></a>Režim údržby

<!--3555754-->

Počínaje verzí 1902 můžete nastavit distribuční bod v režimu údržby. Povolit režim údržby při instalaci softwarových aktualizací nebo při změnách hardwaru serveru.

I když je distribuční bod v režimu údržby, má následující chování:

- Web do něj nedistribuuje žádný obsah.  

- Body správy nevracejí umístění tohoto distribučního bodu klientům.

- Při aktualizaci lokality se stále aktualizuje distribuční bod v režimu údržby.

- Vlastnosti distribučního bodu jsou jen pro čtení. Nemůžete například změnit certifikát ani přidat skupiny hranic.  

- Všechny naplánované úlohy, jako je ověření obsahu, se pořád spouštějí ve stejném plánu.

Buďte opatrní při povolování režimu údržby ve více než jednom distribučním bodě. Tato akce může způsobit dopad na výkon na vaše jiné distribuční body. V závislosti na konfiguraci skupiny hranic můžou mít klienti prodlouženou dobu stahování nebo nemusí stahovat obsah.

Režim údržby by neměl být dlouhodobým stavem pro jakýkoliv distribuční bod. U všech akcí s dlouhou dobou trvání zvažte nejprve odebrání role distribučního bodu.

> [!NOTE]
> I když je distribuční bod v režimu údržby, neprovádějte následující akce:<!-- SCCMDocs-pr #4699 -->
>
> - Odebrat roli
> - Změna přiřazení distribučního bodu

### <a name="enable-maintenance-mode"></a>Povolení režimu údržby

K umístění distribučního bodu do režimu údržby vyžaduje váš uživatelský účet oprávnění **Upravit** pro třídu **lokalita** . Toto oprávnění mají například **správce infrastruktury** a předdefinované role **správce s úplnými oprávněními** .<!-- SCCMDocs-pr issue #3407 -->

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** .  

2. Vyberte uzel **distribuční body** .  

3. Vyberte cílový distribuční bod a na pásu karet zvolte **Povolit režim údržby** .  

Chcete-li zobrazit aktuální stav distribučních bodů, přidejte do uzlu **distribuční body** v konzole sloupec "režim údržby".

Další informace o automatizaci tohoto procesu pomocí Configuration Manager SDK naleznete v tématu [Metoda SetDPMaintenanceMode ve třídě SMS_DistributionPointInfo](../../../../develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo.md).


## <a name="configure-a-distribution-point"></a><a name="bkmk_configs"></a>Konfigurace distribučního bodu  

Jednotlivé distribuční body podporují celou řadu různých konfigurací. Ne všechny typy distribučních bodů však podporují všechny konfigurace. Cloudové distribuční body například nepodporují nasazení s podporou technologie PXE nebo vícesměrového vysílání. Další informace o konkrétních omezeních najdete v následujících článcích:  

- [Použití distribučního bodu cloudu](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

- [Použití distribučního bodu pro vyžádání obsahu](../../../plan-design/hierarchy/use-a-pull-distribution-point.md)  

V následujících částech jsou popsány konfigurace distribučních bodů při [instalaci nového](#bkmk_install-procedure) nebo [úpravou](#bkmk_change-procedure)některého z existujících:  

- [Obecná nastavení](#bkmk_config-general)
- [Communication](#bkmk_config-comm)
- [Nastavení jednotky](#bkmk_config-drive)
- [Nastavení brány firewall](#bkmk_firewall)
- [Distribuční bod pro vyžádání obsahu](#bkmk_config-pull)
- [Nastavení PXE](#bkmk_config-pxe)
- [Odesílání](#bkmk_config-multicast)
- [Ověření obsahu](#bkmk_config-valid)
- [Skupiny hranic](#bkmk_config-boundary)

#### <a name="procedure-to-change-a-distribution-point"></a><a name="bkmk_change-procedure"></a>Postup změny distribučního bodu

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** a vyberte uzel **distribuční body** .  

2. Vyberte distribuční bod, který chcete konfigurovat. Na pásu karet vyberte možnost **vlastnosti**.  

3. Informace v následujících částech použijte při úpravě vlastností distribučního bodu.  

4. Jakmile provedete požadované změny, kliknutím na **tlačítko OK** uložte nastavení a zavřete vlastnosti distribučního bodu.  

### <a name="general"></a><a name="bkmk_config-general"></a>Všeobecně  

> [!Note]  
> Ve verzi 1902 a novější tato stránka obsahuje další nastavení pro HTTP/HTTPS a certifikáty. Počínaje verzí 1906 jsou tato nastavení nyní na stránce [komunikace](#bkmk_config-comm) .

Následující nastavení jsou na stránce **distribuční bod** v Průvodci vytvořením serveru systému lokality a na kartě **Obecné** v okně vlastnosti distribučního bodu:  

- **Popis**: volitelný popis této role distribučního bodu.  

- V **případě potřeby nainstalujte a NAKONFIGURUJTE IIS pomocí Configuration Manager**: Pokud už není služba IIS na serveru nainstalovaná, Configuration Manager nainstaluje a nakonfiguruje. Configuration Manager vyžaduje službu IIS na všech distribučních bodech. Pokud toto nastavení nevyberou a služba IIS není na serveru nainstalovaná, nejdřív nainstalujte IIS, aby Configuration Manager mohl úspěšně nainstalovat distribuční bod.  

    > [!NOTE]  
    > Tato možnost je pouze na stránce **distribuční bod** v Průvodci vytvořením serveru systému lokality. Je k dispozici pouze při [instalaci nového distribučního bodu](#bkmk_install-procedure).  

- **Povolit a nakonfigurovat službu BranchCache pro tento distribuční bod**: Toto nastavení vyberte, pokud chcete Configuration Manager nakonfigurovat službu Windows BranchCache v serveru distribučního bodu. Další informace najdete v tématu [BranchCache](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

- **Upravit rychlost stahování pro použití nevyužité šířky pásma sítě (Windows LEDBAT)**<!--1358112-->: Počínaje verzí 1806 povolte distribučním bodům použití řízení zahlcení sítě. Další informace najdete v tématu [Windows LEDBAT](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#windows-ledbat). Minimální požadavky na podporu LEDBAT:<!-- SCCMDocs issue 883 -->  

    - Configuration Manager verze 1806 (Obecné vydání)  

        - Windows Server verze 1709 nebo novější  

    - Configuration Manager verze 1806 s kumulativní aktualizací (4462978) nebo novější  

        - Windows Server verze 1709 nebo novější
        - Windows Server 2016 s následujícími aktualizacemi:
           - Kumulativní aktualizace KB4132216, vydané 21. června 2018 nebo pozdější Kumulativní aktualizace.
           - Aktualizace servisního zásobníku KB4284833, vydání 18. května 2018 nebo novější aktualizace zásobníku údržby.

    - Configuration Manager verze 1810 nebo novější:

        - Windows Server verze 1709 nebo novější
        - Windows Server 2016 s následujícími aktualizacemi:
           - Kumulativní aktualizace KB4132216, vydané 21. června 2018 nebo pozdější Kumulativní aktualizace.
           - Aktualizace servisního zásobníku KB4284833, vydání 18. května 2018 nebo novější aktualizace zásobníku údržby.
        - Windows Server 2019  

- **Povolit tento distribuční bod pro připravený obsah**: Toto nastavení umožňuje přidat obsah na server před distribucí softwaru. Protože soubory obsahu jsou již v knihovně obsahu, při distribuci softwaru se nepřenášejí po síti. Další informace najdete v tématu [připravený obsah](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent).  

- **Povolit použití tohoto distribučního bodu jako serveru Microsoft Connected cache**: počínaje verzí 1906 můžete na distribučních bodech nainstalovat server s připojenou mezipamětí společnosti Microsoft. Uložením tohoto obsahu do mezipaměti v místním prostředí můžou vaši klienti těžit z funkce Optimalizace doručení, ale můžete přispět k ochraně WAN Links. Další informace, včetně popisu dalších nastavení, najdete v tématu věnovaném [mezipaměti připojené k Microsoftu v Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md).


### <a name="communication"></a><a name="bkmk_config-comm"></a>Telecommunication

> [!Note]  
> Od verze 1906 jsou následující nastavení na kartě **komunikace** . Ve verzi 1902 a novější se tato nastavení nacházejí na kartě [Obecné](#bkmk_config-general) .

Následující nastavení jsou na stránce **komunikace** v Průvodci vytvořením serveru systému lokality a v okně vlastností distribučního bodu:  

- **Konfigurace způsobu, jakým klientská zařízení komunikují s distribučním bodem**: existují výhody a nevýhody používání **protokolu HTTP** nebo **https**. Další informace najdete v tématu [osvědčené postupy zabezpečení pro správu obsahu](../../../plan-design/hierarchy/security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement).  

- **Povolit klientům připojit se anonymně**: Toto nastavení určuje, zda bude distribuční bod umožňovat anonymní připojení z Configuration Manager klientů do knihovny obsahu.  

<!-- I don't think this applies any more, but commenting instead of removing just in case.
    > [!Important]  
    > If you don't use this setting, apply the changes described in Microsoft Knowledge Base article [2619572](https://support.microsoft.com/help/2619572/) on Windows 7 clients. Otherwise repair of Windows Installer applications can fail.  
    >
    > When you deploy a Windows Installer application, the Configuration Manager client downloads the file to its local cache. The client eventually removes the files after the installation finishes. The Configuration Manager client updates the Windows Installer source list for the application. It sets the content path to the content library on associated distribution points. Later, if you try to repair the application on the device, MSIExec attempts to access the content path by using an anonymous user.  
    >
    > After you install the update on clients and modify the documented registry key, MSIExec accesses the content path by using the signed-in user account.  
 -->

- **Vytvoření certifikátu podepsaného svým držitelem nebo Import klientského certifikátu PKI**: Configuration Manager používá tento certifikát pro následující účely:  

    - Ověřuje distribuční bod pro bod správy před tím, než distribuční bod odešle stavové zprávy.  

    - Pokud **povolíte podporu PXE pro klienty** na stránce **Nastavení PXE** , distribuční bod ji odešle do počítačů, které se spouštějí pomocí technologie PXE. Tyto počítače je pak použijí pro připojení k bodu správy během procesu nasazování operačního systému.  

    Pokud nakonfigurujete všechny body správy v lokalitě pro protokol HTTP, vyberte možnost **Vytvoření certifikátu podepsaného svým držitelem**. Při konfiguraci bodů správy pro protokol HTTPS použijte možnost **Import certifikátu** z PKI.  

    Certifikát naimportujete tak, že přejdete do platného souboru PKCS #12 (Public Key Cryptography Standard). Tento soubor PFX nebo CER má certifikát PKI s následujícími požadavky pro Configuration Manager:  

    - Zamýšlené použití zahrnuje ověřování klientů.  

    - Povolit export privátního klíče  

    > [!TIP]  
    > Pro předmět certifikátu nebo alternativní název předmětu (SAN) se nevztahují žádné zvláštní požadavky. V případě potřeby použijte stejný certifikát pro více distribučních bodů.  

    Další informace o požadavcích na certifikát najdete v tématu [požadavky na certifikát PKI](../../../plan-design/network/pki-certificate-requirements.md).  

    Ukázkové nasazení tohoto certifikátu najdete v části [nasazení klientského certifikátu pro distribuční body](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

### <a name="drive-settings"></a><a name="bkmk_config-drive"></a>Nastavení jednotky  

> [!NOTE]  
> Tyto možnosti jsou k dispozici pouze při instalaci nového distribučního bodu.  

Zadejte nastavení jednotky pro distribuční bod. Nakonfigurujte až dvě diskové jednotky pro knihovnu obsahu a dvě diskové jednotky pro sdílenou složku balíčku. Configuration Manager může použít další jednotky, když první dva dosáhnou nakonfigurované rezervy místa na disku. Stránka **Nastavení jednotky** konfiguruje prioritu pro diskové jednotky a množství volného místa na disku, které zbývá na každé diskové jednotce.  

- **Rezerva místa na disku (MB)**: Tato hodnota určuje množství volného místa na jednotce, než Configuration Manager zvolí jinou jednotku a pokračuje v procesu kopírování na tuto jednotku. Soubory obsahu mohou být rozmístěny na několika jednotkách.  

- **Umístění obsahu**: zadejte umístění pro knihovnu obsahu a sdílenou složku balíčku v tomto distribučním bodě. Ve výchozím nastavení jsou všechna umístění obsahu nastavena na hodnotu **automaticky**. Configuration Manager kopíruje obsah do primárního umístění obsahu, dokud velikost volného místa nedosáhne hodnoty zadané v poli **Rezerva místa na disku (MB)**. Když vyberete možnost **automaticky**, Configuration Manager nastaví primární umístění obsahu na diskovou jednotku s největším místem na disku při instalaci. Nastaví sekundární umístění na diskovou jednotku s největším množstvím volného místa na disku. Když primární a sekundární umístění dosáhnou rezervovaného místa na disku, Configuration Manager vybere jinou dostupnou jednotku s největším množstvím volného místa na disku pro pokračování procesu kopírování.  

> [!Tip]  
> Chcete-li zabránit Configuration Manager instalaci na konkrétní jednotku, vytvořte prázdný soubor s názvem **NO_SMS_ON_DRIVE. SMS** a zkopírujte jej do kořenové složky jednotky před instalací distribučního bodu.  

Další informace najdete v [knihovně obsahu](../../../plan-design/hierarchy/the-content-library.md).

### <a name="firewall-settings"></a><a name="bkmk_firewall"></a>Nastavení brány firewall

Distribuční bod musí mít v bráně Windows Firewall nakonfigurovaná následující příchozí pravidla:

- Rozhraní WMI (Windows Management Instrumentation) (DCOM-In)
- Rozhraní WMI (Windows Management Instrumentation) (WMI-in)

Bez těchto pravidel klienti obdrží při pokusu o stažení obsahu v protokolu DataTransferService. log chybu 0x801901F4.

### <a name="pull-distribution-point"></a><a name="bkmk_config-pull"></a>Distribuční bod pro vyžádání obsahu  

**Povolíte-li tomuto distribučnímu bodu vyžádání obsahu z jiných distribučních bodů**, bude se jednat o distribuční bod pro vyžádání obsahu. Můžete změnit chování, jak distribuční bod získá obsah, který do něj distribuujete. Další informace najdete v tématu [použití distribučního bodu pro vyžádání](../../../plan-design/hierarchy/use-a-pull-distribution-point.md)obsahu.

Pro každý distribuční bod pro vyžádání obsahu, který nakonfigurujete, zadejte jeden nebo více zdrojových distribučních bodů, ze kterých získá obsah:  

- Zvolte možnost **Přidat**a potom vyberte jeden nebo více dostupných distribučních bodů, které mají být zdroje.  

- Prioritu můžete upravit pomocí tlačítek se šipkami. Když distribuční bod pro vyžádání obsahu se pokusí o přenos obsahu, priorita je pořadí, ve kterém kontaktuje zdrojové distribuční body. Nejprve kontaktuje distribuční body s nejnižší hodnotou.  

### <a name="pxe"></a><a name="bkmk_config-pxe"></a>PROTOKOLU  

Určete, zda má být v distribučním bodě povolena technologie PXE. Pomocí technologie PXE můžete spustit nasazení operačního systému na klientech. Další informace o tom, jak používat technologii PXE v Configuration Manager, najdete v tématu [použití technologie PXE k nasazení systému Windows přes síť](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

Pokud povolíte PXE, Configuration Manager nainstaluje službu pro nasazení systému Windows (WDS) na server, pokud je to nutné. WDS je služba, která provádí spouštění pomocí technologie PXE pro instalaci operačních systémů. Po dokončení Průvodce vytvořením distribučního bodu Configuration Manager nainstaluje poskytovatele služby WDS, který používá spouštěcí funkce PXE.

Počínaje verzí 1806 můžete povolit technologii PXE v distribučním bodě bez služby WDS.

Vyberte možnost **Povolení podpory PXE pro klienty**a pak nakonfigurujte následující nastavení:  

> [!Note]  
> V dialogovém okně **Zkontrolujte požadované porty pro PXE** vyberte **Ano** a potvrďte tak, že chcete povolit technologii PXE. Configuration Manager automaticky nakonfiguruje výchozí porty na bráně Windows Firewall. Pokud používáte jinou bránu firewall, nakonfigurujte porty ručně.  
>
> Pokud nainstalujete služby WDS a DHCP na stejný server, nakonfigurujte službu WDS tak, aby naslouchala na jiném portu. Ve výchozím nastavení DHCP naslouchá na stejném portu. Další informace najdete v oddílu [Důležité informace, pokud máte službu WDS i protokol DHCP na stejném serveru](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDSandDHCP).  

- **Povolit tomuto distribučnímu bodu reagovat na příchozí požadavky PXE**: Určete, jestli se má povolit, aby služba WDS reagovala na žádosti služby PXE. Pomocí tohoto nastavení můžete službu povolit nebo zakázat bez odebrání funkce PXE z distribučního bodu.  

- **Povolit podporu neznámých počítačů**: Určete, jestli se má povolit podpora pro počítače, které Configuration Manager nespravují. Další informace najdete v tématu [Příprava pro nasazení do neznámých počítačů](../../../../osd/get-started/prepare-for-unknown-computer-deployments.md).  

- **Povolit respondér technologie PXE bez služby pro nasazení systému Windows**: počínaje verzí 1806 Tato možnost povolí v distribučním bodě respondér technologie PXE, který nevyžaduje službu WDS. Tento respondér PXE podporuje sítě IPv6. Pokud tuto možnost povolíte na distribučním bodu, který už je v prostředí PXE povolený, Configuration Manager pozastaví službu WDS. Pokud tuto možnost zakážete, ale přesto **povolíte podporu PXE pro klienty**, pak distribuční bod POVOLÍ službu WDS znovu.<!--1357580-->  

    > [!Note]  
    > Ve verzi 1810 a starší se nepodporuje použití respondérů PXE bez služby WDS na serverech, na kterých běží taky server DHCP.
    >
    > Pokud v rámci verze 1902 povolíte respondér PXE v distribučním bodě bez služby pro nasazení systému Windows, může být nyní na stejném serveru jako služba DHCP. <!--3734270-->  

- **Vyžadovat heslo, když počítače používají PXE**: k zajištění dalšího zabezpečení pro nasazení PXE zadejte silné heslo.  

- **Spřažení uživatelských zařízení**: Určete, jak má distribuční bod přidružit uživatele k cílovému počítači pro nasazení PXE. Zvolte jednu z následujících možností:  

  - **Povolení spřažení uživatelských zařízení pomocí automatického schválení**: Toto nastavení vyberte, pokud chcete automaticky přidružit uživatele k cílovému počítači bez čekání na schválení.  

  - **Povolení spřažení uživatelských zařízení na základě schválení správce**: Toto nastavení vyberte, pokud chcete před přidružením uživatelů k cílovému počítači počkat na schválení od správce.  

  - **Nepovolit spřažení uživatelských zařízení**: Toto nastavení vyberte, pokud chcete určit, že uživatelé nejsou přidružení k cílovému počítači. Toto nastavení je výchozí.  

    Další informace o spřažení uživatelských zařízení najdete v tématu [propojení uživatelů a zařízení pomocí spřažení uživatelských zařízení](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

- **Síťová rozhraní**: Určete, jestli má distribuční bod odpovídat na požadavky PXE ze všech síťových rozhraní nebo ze specifických síťových rozhraní. Pokud distribuční bod odpoví na konkrétní síťová rozhraní, zadejte adresu MAC pro každé síťové rozhraní.  

    > [!Note]  
    > Při změně síťového rozhraní restartujte službu WDS a ujistěte se, že správně ukládá konfiguraci. Pokud používáte službu respondér technologie PXE ve verzi 1806, restartujte **službu CONFIGMGR PXE Responder Service** (SccmPxe).<!--SCCMDocs issue 642-->  

- **Zadejte zpoždění odezvy serveru PXE (sekundy)**: při použití více serverů PXE určete, jak dlouho by měl tento distribuční bod s povoleným PXE čekat, než odpoví na požadavky počítače. Ve výchozím nastavení bude distribuční bod s povoleným PXE Configuration Manager okamžitě reagovat.  

### <a name="multicast"></a><a name="bkmk_config-multicast"></a>Odesílání  

Určete, zda chcete povolit vícesměrové vysílání v distribučním bodě. Nasazení pomocí vícesměrového vysílání šetří šířku pásma při současném posílání dat na více Configuration Managerch klientů současně. Bez vícesměrového vysílání pošle Server kopii dat každému klientovi přes samostatné připojení. Další informace o použití vícesměrového vysílání pro nasazení operačního systému najdete v tématu [použití vícesměrového vysílání k nasazení Windows přes síť](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).

Pokud povolíte vícesměrové vysílání, Configuration Manager v případě potřeby nainstaluje službu pro nasazení systému Windows (WDS) na server.  

Vyberte možnost **Povolení vícesměrového vysílání pro souběžné odesílání dat na více klientů**a pak nakonfigurujte následující nastavení:  

- **Účet pro připojení vícesměrového vysílání**: zadejte účet, který se má použít při konfiguraci Configuration Manager připojení k databázi pro vícesměrové vysílání. Další informace najdete v tématu [účet pro připojení vícesměrového vysílání](../../../plan-design/hierarchy/accounts.md#multicast-connection-account).  

- **Nastavení adresy vícesměrového vysílání**: Určete IP adresy pro odesílání dat do cílových počítačů. Ve výchozím nastavení získá IP adresu ze serveru DHCP, který je povolený pro distribuci adres vícesměrového vysílání. V závislosti na prostředí sítě můžete určit rozsah IP adres od 239.0.0.0 do 239.255.255.255.  

    > [!IMPORTANT]  
    > IP adresy, které nakonfigurujete, musí být přístupné pro cílové počítače, které požadují bitovou kopii operačního systému. Ověřte, že směrovače a brány firewall umožňují přenos vícesměrového vysílání mezi cílovým počítačem a distribučním bodem.  

- **Rozsah portů UDP pro vícesměrové vysílání**: zadejte rozsah portů UDP, které se používají k odesílání dat do cílových počítačů.  

    > [!IMPORTANT]  
    > Porty UDP musí být přístupné pro cílové počítače, které požadují bitovou kopii operačního systému. Ověřte, že směrovače a brány firewall umožňují přenos vícesměrového vysílání mezi cílovým počítačem a serverem lokality.  

- **Maximální počet klientů**: Určete maximální počet cílových počítačů, které mohou stáhnout bitovou kopii operačního systému z tohoto distribučního bodu.  

- **Povolit naplánované vícesměrové vysílání**: Určete, jak Configuration Manager ovládací prvky, kdy se má do cílových počítačů začít nasazovat operační systémy. Nakonfigurujte tyhle možnosti:  

    - **Zpoždění začátku relace (minuty)**: zadejte dobu v minutách, po kterou Configuration Manager čekat, než odpoví na první žádost o nasazení.  

    - **Minimální velikost relace (klientů)**: Určete, kolik požadavků musí být přijato, než Configuration Manager začne nasazovat operační systém.  

> [!IMPORTANT]  
> Počínaje verzí 1806 můžete povolit a nakonfigurovat vícesměrové vysílání na kartě **vícesměrové vysílání** vlastností distribučního bodu. distribuční bod musí používat službu pro nasazení systému Windows.  
>
> - Pokud **povolíte podporu PXE pro klienty** a **povolíte vícesměrové vysílání pro souběžné odesílání dat na více klientů**, nemůžete **Povolit respondér technologie PXE bez služby pro nasazení systému Windows**.  
>
> - Pokud **povolíte podporu PXE pro klienty** a **povolíte respondér PXE bez služby pro nasazení systému Windows**, nemůžete **Povolit vícesměrové vysílání pro souběžné odesílání dat na více klientů** .  

### <a name="group-relationships"></a><a name="bkmk_config-group"></a>Vztahy skupiny  

> [!NOTE]  
> Tyto možnosti jsou k dispozici pouze v případě, že upravujete vlastnosti dříve nainstalovaného distribučního bodu.  

Spravujte skupiny distribučních bodů, ve kterých je tento distribuční bod členem.  

Chcete-li přidat tento distribuční bod jako člena do existující skupiny distribučních bodů, klikněte na tlačítko **Přidat**. V okně Přidat do skupin distribučních bodů vyberte existující skupinu a pak zvolte **OK**.  

Chcete-li odebrat tento distribuční bod ze skupiny distribučních bodů, vyberte skupinu v seznamu a zvolte možnost **Odebrat**. Při odebrání distribučního bodu ze skupiny distribučních bodů se neodebere žádný obsah z distribučního bodu.

### <a name="content"></a><a name="bkmk_config-content"></a>Sušin  

> [!NOTE]  
> Tyto možnosti jsou k dispozici pouze v případě, že upravujete vlastnosti dříve nainstalovaného distribučního bodu.  

Spravujte obsah, který jste rozšíříte do distribučního bodu. Vyberte ze seznamu balíčků pro nasazení a proveďte následující akce:  

- **Ověřit**: Spusťte proces pro ověření integrity souborů obsahu pro daný software. Chcete-li zobrazit výsledky procesu ověřování obsahu, rozbalte v pracovním prostoru **monitorování** možnost **stav distribuce**a poté zvolte uzel **stav obsahu** . Další informace najdete v tématu [ověření obsahu](deploy-and-manage-content.md#validate-content).  

- **Redistribute**: zkopíruje všechny soubory obsahu pro vybraný software do distribučního bodu a přepíše stávající soubory. Tato akce se obvykle používá k opravě souborů obsahu. Další informace najdete v tématu o opětovné [distribuci obsahu](deploy-and-manage-content.md#redistribute-content).  

- **Odebrat**: Odebere soubory obsahu pro software z distribučního bodu. Další informace najdete v tématu [Odebrání obsahu](deploy-and-manage-content.md#remove-content).  

### <a name="content-validation"></a><a name="bkmk_config-valid"></a>Ověření obsahu  

Nastavte plán pro ověření integrity souborů obsahu v distribučním bodě. Když povolíte ověření obsahu podle plánu, Configuration Manager spustí proces v naplánovaném čase. Ověřuje veškerý obsah v distribučním bodě na základě místní třídy SMS_PackagesInContLib SCCMDP. Můžete také nakonfigurovat prioritu ověření obsahu. Ve výchozím nastavení je priorita nastavena na **nejnižší**. Zvýšení priority může zvýšit využití procesoru a disku na serveru během procesu ověřování, ale mělo by to být rychlejší.

Chcete-li zobrazit výsledky procesu ověřování obsahu, rozbalte v pracovním prostoru **monitorování** možnost **stav distribuce**a poté zvolte uzel **stav obsahu** . Zobrazuje obsah pro každý typ softwaru, například aplikace, balíček aktualizace softwaru a spouštěcí bitovou kopii.  

> [!WARNING]  
> I když zadáte plán ověření obsahu pomocí místního času pro daný počítač, konzola Configuration Manager zobrazuje plán ve standardu UTC.  

Další informace najdete v tématu [ověření obsahu](deploy-and-manage-content.md#validate-content).

### <a name="boundary-groups"></a><a name="bkmk_config-boundary"></a>Skupiny hranic  

Spravujte skupiny hranic, ke kterým přiřadíte tento distribuční bod. Přidejte distribuční bod do alespoň jedné skupiny hranic. Během nasazování obsahu musí být klienti ve skupině hranic přidružené k distribučnímu bodu, aby se tento distribuční bod používal jako umístění zdroje pro obsah.

Konfigurujte *vztahy* hraničních skupin, které definují, kdy a do kterých skupin hranic může klient přejít zpět k hledání obsahu. Další informace najdete v tématu [skupiny hranic](boundary-groups.md).

Zvolte **Přidat** a ze seznamu vyberte existující skupinu hranic.

Chcete-li pro tento distribuční bod vytvořit novou skupinu hranic, klikněte na tlačítko **vytvořit**. Další informace o tom, jak vytvořit a nakonfigurovat skupinu hranic, najdete v tématu [postupy pro skupiny hranic](boundary-group-procedures.md).

Pokud upravujete vlastnosti dříve nainstalovaného distribučního bodu, spravujte možnost pro **zajištění distribuce na vyžádání**. Tato možnost umožňuje Configuration Manager k automatické distribuci obsahu na tento server, když na něj klient vyžádá. Další informace najdete v tématu [distribuce obsahu na vyžádání](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).

### <a name="schedule"></a><a name="bkmk_config-sched"></a>CXL  

> [!NOTE]  
> Tyto možnosti jsou k dispozici pouze v případě, že upravujete vlastnosti dříve nainstalovaného distribučního bodu.
>
> Tato karta je k dispozici pouze v případě, že upravujete vlastnosti distribučního bodu, který je vzdálený od serveru lokality.  

Nakonfigurujte plán, který omezí, kdy Configuration Manager může přenášet data do distribučního bodu. Omezte data podle priority nebo uzavřete připojení pro vybraná časová období.

Chcete-li omezit data, vyberte časové období v mřížce a pak vyberte jedno z následujících nastavení **dostupnosti**:  

- **Otevřít pro všechny priority**: Configuration Manager odesílá data do distribučního bodu bez omezení. Toto nastavení je výchozím nastavením pro všechna časová období.  

- **Povolte střední a vysokou prioritu**: Configuration Manager odesílá do distribučního bodu pouze data se střední a vysokou prioritou.  

- **Povolení pouze vysoké priority**: Configuration Manager odesílá do distribučního bodu pouze data s vysokou prioritou.  

- **Uzavřeno**: Configuration Manager neodesílá žádná data do distribučního bodu.  

Nakonfigurujte **prioritu distribuce** softwaru na kartě **Nastavení distribuce** vlastností softwaru.

> [!IMPORTANT]  
> Plán je založen na časovém pásmu z odesílajícího webu, nikoli v distribučním bodě.  

### <a name="rate-limits"></a><a name="bkmk_config-rate"></a>Omezení přenosové rychlosti  

> [!NOTE]  
> Tyto možnosti jsou k dispozici pouze v případě, že upravujete vlastnosti dříve nainstalovaného distribučního bodu.  
>
> Tato karta je k dispozici pouze v případě, že upravujete vlastnosti distribučního bodu, který je vzdálený od serveru lokality.  

Nakonfigurujte omezení přenosové rychlosti, která řídí šířku pásma sítě, kterou Configuration Manager používá k přenosu obsahu do distribučního bodu. Vybírat můžete z těchto možností:  

- **Neomezené při posílání do tohoto cíle**: Configuration Manager odesílá obsah do distribučního bodu bez omezení přenosové rychlosti. Toto nastavení je výchozí.  

- **Pulse – režim**: Tato možnost určuje velikost datových bloků, které webový server odešle do distribučního bodu. Můžete také určit prodlevu mezi odesíláním jednotlivých bloků dat. Tuto možnost použijte, pokud musíte odesílat data v rámci velmi malé šířky pásma síťového připojení k distribučnímu bodu. Například máte omezení pro posílání 1 KB dat každých pět sekund, bez ohledu na rychlost propojení nebo jeho využití v daném okamžiku.  

- **Omezeno na zadaný maximální počet přenosů za hodinu**: Toto nastavení použijte, pokud chcete, aby lokalita odesílala data do distribučního bodu, a to pomocí pouze procentuální hodnoty času, který nakonfigurujete. Když použijete tuto možnost, Configuration Manager neidentifikuje dostupnou šířku pásma sítě. Místo toho rozdělí čas, který může odesílat data. Server odesílá data po krátkou dobu, po jejímž uplynutí jsou po dobu odeslání dat odesílány. Pokud například nastavíte **omezit dostupnou šířku pásma** na **50%**, Configuration Manager přenáší data po určitou dobu následovanou stejnou dobou, kdy nejsou odesílána žádná data. Skutečná velikost dat nebo velikost datového bloku není spravovaná. Spravuje pouze dobu, během které odesílá data.  
