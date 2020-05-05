---
title: Instalace distribučních bodů cloudu
titleSuffix: Configuration Manager
description: Pomocí těchto kroků můžete nastavit distribuční bod cloudu v Configuration Manager.
ms.date: 09/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 30cd61240b09f821d8b18c37e6accc7450f35817
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718844"
---
# <a name="install-a-cloud-distribution-point-for-configuration-manager"></a>Instalace distribučního bodu cloudu pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

> [!Important]  
> Implementace pro sdílení obsahu z Azure se změnila. Pomocí brány pro správu cloudu s povoleným obsahem povolte, aby služba **CMG mohla fungovat jako distribuční bod cloudu a poskytovala obsah z Azure Storage**. Další informace najdete v tématu [Úprava CMG](../../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg).
>
> V budoucnu nebudete moci vytvořit tradiční distribuční bod cloudu. Další informace najdete v tématu [odebrané a zastaralé funkce](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

Tento článek podrobně popisuje kroky pro instalaci cloudového distribučního bodu Configuration Manager v Microsoft Azure. Obsahuje následující oddíly:

- [Před zahájením](#bkmk_before)
- [Nastavení](#bkmk_setup)
- [Konfigurace služby DNS](#bkmk_dns)
- [Nastavení proxy serveru lokality](#bkmk_proxy)
- [Distribuce obsahu a konfigurace klientů](#bkmk_client)
- [Správa a monitorování](#bkmk_monitor)
- [Úprava](#bkmk_modify)
- [Pokročilé řešení potíží](#bkmk_tshoot)


## <a name="before-you-begin"></a><a name="bkmk_before"></a>Než začnete

Začněte tím, že si přečtete článek [použití distribučního bodu cloudu](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md). Tento článek vám pomůže s plánováním a návrhem distribučních bodů cloudu.

Pomocí následujícího kontrolního seznamu se ujistěte, že máte potřebné informace a předpoklady pro vytvoření cloudového distribučního bodu:  

- Webový server se může připojit k Azure. Pokud vaše síť používá proxy server, [nakonfigurujte roli systému lokality](#bkmk_proxy).  

- **Prostředí Azure** , které se má použít. Například veřejný cloud Azure nebo Cloud pro státní správu Azure USA.  

- Od verze 1806 a *Doporučené*použijte **nasazení Azure Resource Manager**. Musí být přitom splněny následující požadavky:<!--1322209-->  

    - Integrace s [Azure Active Directory](azure-services-wizard.md) pro **správu cloudu**. Zjišťování uživatelů služby Azure AD není vyžadováno.  

    - **ID předplatného**Azure.  

    - **Skupina prostředků**Azure.  

    - **Účet správce předplatného** musí být přihlášený během průvodce.  

- **Certifikát ověřování serveru**, vyexportovaný jako. Soubor PFX.  

- Globálně jedinečný **název služby** pro cloudový distribuční bod.  

    > [!TIP]  
    > Před vyžádáním ověřovacího certifikátu serveru, který používá tento název služby, potvrďte, že požadovaný název domény Azure je jedinečný. Například *WallaceFalls.CloudApp.NET*.
    >
    > 1. Přihlaste se k webu [Azure Portal](https://portal.azure.com).
    > 1. Vyberte **všechny prostředky**a pak vyberte **Přidat**.
    > 1. Vyhledejte **cloudovou službu**. Vyberte **Vytvořit**.
    > 1. Do pole **název DNS** zadejte požadovanou předponu, například *WallaceFalls*. Rozhraní odráží, zda je název domény k dispozici nebo již používá jiná služba.
    >
    > Nevytvářejte službu na portálu, stačí pomocí tohoto procesu ověřit dostupnost názvu.

- **Oblast** Azure pro toto nasazení.  

- Pokud stále potřebujete použít **nasazení služby Azure Classic** v Configuration Manager verze 1810 nebo starší, budete potřebovat následující požadavky:  

    > [!Important]  
    > Od verze 1810 jsou nasazení klasických služeb v Azure v Configuration Manager zastaralá. Začněte používat Azure Resource Manager nasazení pro cloudový distribuční bod. Další informace najdete v tématu [Azure Resource Manager](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#azure-resource-manager).  
    >
    > Počínaje verzí 1902 Configuration Manager Azure Resource Manager je jediným mechanismem nasazení pro nové instance distribučního bodu cloudu.<!-- 3605704 -->

    - **ID předplatného**Azure.  

    - **Certifikát pro správu**Azure, který je exportovaný jako obojí. CER a. Soubory PFX. Správce předplatného Azure musí přidat. Certifikát pro správu CER k předplatnému v [Azure Portal](https://portal.azure.com).  

### <a name="branchcache"></a>Služba BranchCache

Pokud chcete distribučnímu bodu cloudu povolit používání služby Windows BranchCache, nainstalujte funkci BranchCache na server lokality.<!-- SCCMDocs-pr#4054 -->

- Pokud má server lokality místní roli systému lokality distribučního bodu, nakonfigurujte možnost ve vlastnostech této role tak, aby **povolovala a nakonfigurovala službu BranchCache**. Další informace najdete v tématu [Konfigurace distribučního bodu](install-and-configure-distribution-points.md#bkmk_config-general).

- Pokud server lokality nemá roli distribučního bodu, nainstalujte funkci BranchCache do systému Windows. Další informace najdete v tématu [Instalace funkce BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/deploy/install-the-branchcache-feature).

Pokud jste už distribuci obsahu do distribučního bodu cloudu a potom se rozhodnete povolit službu BranchCache, nainstalujte tuto funkci. Pak obsah znovu distribuujte do distribučního bodu cloudu.

> [!NOTE]  
> Pokud máte v Configuration Manager verze 1810 a starší, pokud máte více než jeden distribuční bod cloudu, musíte ručně nastavit přístupové heslo klíče BranchCache. Další informace najdete v článku [Podpora Microsoftu KB 4458143](https://support.microsoft.com/help/4458143).

## <a name="set-up"></a><a name="bkmk_setup"></a>Nastavit  

Tento postup proveďte na webu, který bude hostitelem tohoto distribučního bodu cloudu, který je stanovený vaším [návrhem](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_topology).  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte možnost **cloudové distribuční body**. Na pásu karet vyberte **Vytvořit cloudový distribuční bod**.  

2. Na stránce **Obecné** v Průvodci vytvořením distribučního bodu cloudu nakonfigurujte následující nastavení:  

    1. Nejdřív zadejte **prostředí Azure**.  

    2. Od verze 1806 a *Doporučené*vyberte jako metodu nasazení **Azure Resource Manager nasazení** . Vyberte **Přihlásit** se a proveďte ověření pomocí účtu správce předplatného Azure. Průvodce automaticky vyplní zbývající pole z informací uložených během předpokladu integrace služby Azure AD. Pokud vlastníte více předplatných, vyberte **ID předplatného** požadovaného předplatného, které chcete použít.  

    > [!Note]  
    > Od verze 1810 jsou nasazení klasických služeb v Azure v Configuration Manager zastaralá.
    >
    > Pokud potřebujete použít klasické nasazení služby, vyberte tuto možnost na této stránce. Nejdřív zadejte své **ID předplatného**Azure. Pak vyberte **Procházet** a vyberte. Soubor PFX pro certifikát správy Azure.  

3. Vyberte **Další**. Počkejte, než lokalita otestuje připojení k Azure.  

4. Na stránce **Nastavení** zadejte následující nastavení a potom vyberte **Další**:  

    - **Oblast**: Vyberte oblast Azure, ve které chcete distribuční bod cloudu vytvořit.  

    - **Skupina prostředků** (jenom Azure Resource Manager Metoda nasazení)  

        - **Použít existující**: v rozevíracím seznamu vyberte existující skupinu prostředků.  

        - **Vytvořit nový**: zadejte nový název skupiny prostředků, který se má vytvořit v předplatném Azure.  

    - **Primární lokalita**: Vyberte primární lokalitu pro distribuci obsahu do tohoto distribučního bodu.

    - **Soubor certifikátu**: vyberte **Procházet** a vyberte. Soubor PFX pro certifikát ověřování serveru distribučního bodu cloudu Běžný název z tohoto certifikátu naplní požadovaná pole **plně kvalifikovaného názvu domény služby** a **názvu služby** .  

        > [!NOTE]  
        > Certifikát ověřování serveru distribučního bodu cloudu podporuje zástupné znaky. Pokud používáte certifikát se zástupným znakem, nahraďte hvězdičku (`*`) v poli **plně kvalifikovaný název domény služby** požadovaným názvem hostitele pro danou službu.  

5. Na stránce **výstrahy** nastavte kvóty úložiště, kvóty přenosů a v jakém procentu těchto kvót chcete generovat výstrahy Configuration Manager. Pak vyberte **Další**.  

6. Dokončete průvodce.  

### <a name="monitor-installation"></a>Monitorovat instalaci  

Lokalita začne vytvářet novou hostovanou službu pro cloudový distribuční bod. Po ukončení průvodce Sledujte průběh instalace distribučního bodu cloudu v konzole Configuration Manager. Také monitorujte soubor **CloudMgr. log** na primárním serveru lokality. V případě potřeby Sledujte zřízení cloudové služby v Azure Portal.  

> [!NOTE]  
> Zřízení nového distribučního bodu v Azure může trvat až 30 minut. Soubor **CloudMgr. log** opakuje následující zprávu, dokud se nezřídí účet úložiště:  
> `Waiting for check if container exists. Will check again in 10 seconds`  
> Jakmile zřídí účet úložiště, služba se vytvoří a nakonfiguruje.  

### <a name="verify-installation"></a>Ověřit instalaci

Pomocí následujících metod ověřte, zda je instalace distribučního bodu cloudu dokončena:  

- V konzole Configuration Manager otevřete pracovní prostor **Správa** . Rozbalte položku **Cloud Services**a vyberte uzel **distribuční body cloudu** . V seznamu vyhledejte nový distribuční bod cloudu. Sloupec stav by měl být **připravený**.  

- V konzole Configuration Manager přejdete do pracovního prostoru **monitorování** . Rozbalte položku **stav systému**a vyberte uzel **Stav součásti** . Zobrazte všechny zprávy ze součásti **SMS_CLOUD_SERVICES_MANAGER** a vyhledejte stavovou zprávu ID **9409**.  

- V případě potřeby přejdete na Azure Portal. **Nasazení** pro distribuční bod cloudu zobrazuje stav **připraveno**.  


## <a name="configure-dns"></a><a name="bkmk_dns"></a>Konfigurace DNS  

Aby mohli klienti používat cloudový distribuční bod, musí být schopni přeložit název distribučního bodu cloudu na IP adresu, kterou spravuje Azure. Bod správy poskytuje těmto **názvům plně kvalifikovaný název domény** cloudového distribučního bodu. Distribuční bod cloudu existuje v Azure jako **název služby**. Tyto hodnoty najdete na kartě **Nastavení** ve vlastnostech distribučního bodu cloudu.

> [!Note]  
> Uzel **distribučních bodů cloudu** v konzole nástroje zahrnuje sloupec s názvem **Služba**, ale ve skutečnosti se zobrazuje hodnota **plně kvalifikovaného názvu domény služby** . Chcete-li zobrazit obě hodnoty, otevřete **vlastnosti** distribučního bodu cloudu a přepněte na kartu **Nastavení** .  

<!-- Remove based on feedback from RoYork
If you issue the server authentication certificate from your PKI, you may directly specify the Azure **Service name**. For example, `WallaceFalls.cloudapp.net`. When you specify this certificate in the Create Cloud Distribution Point Wizard, both the **Service FQDN** and **Service name** properties are the same. In this scenario, you don't need to configure DNS. The name that clients receive from the management point is the same name as the service in Azure.  
-->

Běžný název certifikátu ověřování serveru by měl obsahovat název domény. Tento název se vyžaduje, když si koupíte certifikát od veřejného poskytovatele. Doporučuje se při vydávání tohoto certifikátu z infrastruktury veřejných klíčů. Například, `WallaceFalls.contoso.com`. Při zadání tohoto certifikátu v Průvodci vytvořením distribučního bodu cloudu naplní běžný název vlastnost **plně kvalifikovaný název domény služby** (`WallaceFalls.contoso.com`). **Název služby** má stejný název hostitele (`WallaceFalls`) a připojí ho k názvu domény Azure. `cloudapp.net` V tomto scénáři musí klienti přeložit **plně kvalifikovaný název domény služby** domény (`WallaceFalls.contoso.com`) na **název služby** Azure (`WallaceFalls.cloudapp.net`). Vytvořte alias CNAME pro mapování těchto názvů.

### <a name="create-cname-alias"></a>Vytvořit alias CNAME

Vytvořte záznam kanonického názvu (CNAME) ve veřejné službě DNS s přístupem k Internetu vaší organizace. Tento záznam vytvoří alias pro vlastnost **plně kvalifikovaného názvu domény služby** distribučního bodu cloudu, kterou klienti obdrží, do **názvu služby**Azure. Například vytvořte nový záznam CNAME pro `WallaceFalls.contoso.com` `WallaceFalls.cloudapp.net`.  

### <a name="client-name-resolution-process"></a>Proces překladu názvů klientů

Následující postup ukazuje, jak klient řeší název distribučního bodu cloudu:  

1. Klient získá **plně kvalifikovaný název domény** distribučního bodu cloudu v seznamu zdrojů obsahu. Například, `WallaceFalls.contoso.com`.  

2. Dotazuje se na DNS, který vyřeší plně kvalifikovaný název domény služby pomocí aliasu CNAME pro **název služby**Azure. Například, `WallaceFalls.cloudapp.net`.  

3. Znovu se dotazuje na DNS, čímž se přeloží název služby Azure na veřejnou IP adresu Azure.  

4. Klient používá tuto IP adresu k zahájení komunikace s cloudovým distribučním bodem.  

5. Distribuční bod cloudu prezentuje certifikát ověřování serveru klientovi. Klient používá k ověření řetězec důvěryhodného certifikátu.  


## <a name="set-up-site-server-proxy"></a><a name="bkmk_proxy"></a>Nastavení proxy serveru lokality  

Server primární lokality, který spravuje distribuční bod cloudu, musí komunikovat s Azure. Pokud vaše organizace používá proxy server k řízení přístupu k Internetu, nakonfigurujte server primární lokality tak, aby používal tento proxy server.  

Další informace najdete v tématu [Podpora proxy serveru](../../../plan-design/network/proxy-server-support.md).  


## <a name="distribute-content-and-configure-clients"></a><a name="bkmk_client"></a>Distribuce obsahu a konfigurace klientů

Distribuujte obsah do distribučního bodu cloudu, který je stejný jako jakýkoli jiný místní distribuční bod. Bod správy neobsahuje distribuční bod cloudu v seznamu umístění obsahu, pokud nemá obsah, který klienti požadují. Další informace najdete v tématu [distribuce a Správa obsahu](deploy-and-manage-content.md).

Správa distribučního bodu cloudu, který je stejný jako jakýkoli jiný místní distribuční bod. Tyto akce zahrnují přiřazení do skupiny distribučních bodů a správu balíčků obsahu. Další informace najdete v tématu [instalace a konfigurace distribučních bodů](install-and-configure-distribution-points.md).

Výchozí nastavení klienta automaticky umožní klientům používat distribuční body cloudu. Pomocí následujícího nastavení klienta můžete řídit přístup ke všem distribučním bodům cloudu ve vaší hierarchii:  

- Ve skupině **Nastavení cloudu** upravte nastavení **Povolení přístupu ke cloudovým distribučním bodům**.  

    - Ve výchozím nastavení je toto nastavení nastaveno na **Ano**.  

    - Toto nastavení upravte a nasaďte pro uživatele i zařízení.  


## <a name="manage-and-monitor"></a><a name="bkmk_monitor"></a>Správa a monitorování  

Monitorujte obsah, který distribuujete do distribučního bodu cloudu, stejně jako u ostatních místních distribučních bodů. Další informace najdete v tématu [monitorování obsahu](monitor-content-you-have-distributed.md).

### <a name="alerts"></a><a name="bkmk_alerts"></a>Generoval  

Configuration Manager pravidelně kontroluje službu Azure. Pokud služba není aktivní nebo pokud dojde k problémům s odběrem nebo certifikátem, Configuration Manager vyvolá výstrahu.

Nakonfigurujte prahové hodnoty pro množství dat, která chcete uložit v distribučním bodě cloudu, a množství dat, které klienti stáhnou z distribučního bodu. Použijte výstrahy pro tyto prahové hodnoty, které vám pomohou určit, kdy se má cloudová služba zastavit nebo odstranit, upravit obsah uložený v distribučním bodě cloudu nebo změnit klienty, kteří můžou službu používat.

- **Prahová hodnota pro výstrahu úložiště**: prahová hodnota pro výstrahu úložiště nastaví horní limit v GB na množství dat nebo obsahu, které chcete uložit v cloudovém distribučním bodě. Ve výchozím nastavení je tato prahová hodnota 2 000 GB. Configuration Manager generuje upozornění a kritické výstrahy, když zbývající volné místo dosáhne úrovně, které zadáte. Ve výchozím nastavení se tyto výstrahy vyskytují v 50% a 90% prahové hodnoty.  

- **Prahová hodnota pro výstrahu měsíčního přenosu**: prahová hodnota pro výstrahu měsíčního přenosu vám pomůže monitorovat množství obsahu, které se přenáší z distribučního bodu na klienty po dobu 30 dnů. Ve výchozím nastavení je tato prahová hodnota 10 000 GB. Lokalita vyvolává upozornění a kritické výstrahy, když přenosy dosáhnou hodnot, které definujete. Ve výchozím nastavení se tyto výstrahy vyskytují v 50% a 90% prahové hodnoty.  

    > [!IMPORTANT]  
    > Configuration Manager monitoruje přenos dat, ale nezastaví přenos dat nad rámec zadané prahové hodnoty pro výstrahu přenosu.  

Zadejte prahové hodnoty pro každý cloudový distribuční bod během instalace nebo použijte kartu **výstrahy** vlastností distribučního bodu cloudu.  

> [!NOTE]  
> Výstrahy cloudového distribučního bodu závisí na statistikách využití z Azure, což může trvat až 24 hodin, než budou k dispozici. Další informace o Analýza úložiště pro Azure najdete v tématu [Analýza úložiště](https://docs.microsoft.com/rest/api/storageservices/storage-analytics).  

V hodinovém cyklu primární lokalita, která monitoruje distribuční bod cloudu, stáhne data transakcí z Azure. Tato data transakcí ukládá do `CloudDP-<ServiceName>.log` souboru na serveru lokality. Configuration Manager pak tyto informace vyhodnotí proti kvótám úložiště a přenosu pro každý cloudový distribuční bod. Když přenos dat dosáhne nebo překročí zadaný svazek pro upozornění nebo kritické výstrahy, Configuration Manager vygeneruje příslušnou výstrahu.  

> [!WARNING]  
> Vzhledem k tomu, že lokalita stahuje informace o přenosech dat z Azure každou hodinu, může použití přesáhnout upozornění nebo kritickou prahovou hodnotu, než Configuration Manager bude mít přístup k datům a vyvolá výstrahu.  


## <a name="modify"></a><a name="bkmk_modify"></a>Upravíte

Zobrazit informace vysoké úrovně distribučního bodu v uzlu **distribuční body cloudu** v části **Cloud Services** v pracovním prostoru **Správa** konzoly Configuration Manager. Vyberte distribuční bod a vyberte **vlastnosti** . zobrazí se další podrobnosti.  

Při úpravě vlastností distribučního bodu cloudu jsou na následujících kartách vložená nastavení pro úpravy:  

#### <a name="settings"></a>Nastavení

- **Popis**  

- **Soubor certifikátu**: předtím, než vyprší platnost certifikátu ověřování serveru, vydejte nový certifikát se stejným běžným názvem. Pak sem přidejte nový certifikát, který chcete použít ke spuštění služby. V případě vypršení platnosti certifikátu nebudou klienti důvěřovat a používat službu.  

#### <a name="alerts"></a>Výstrahy

Upravte prahové hodnoty dat pro úložiště a výstrahy měsíčního přenosu.  

#### <a name="content"></a>Obsah

Umožňuje spravovat obsah stejný jako u místního distribučního bodu.  

### <a name="redeploy-the-service"></a>Opětovné nasazení služby

Důležitější změny, například následující konfigurace, vyžadují opětovné nasazení služby:

- Klasický způsob nasazení Azure Resource Manager
- Předplatné
- Název služby
- Privátní infrastruktura veřejných klíčů
- Oblast Azure

Pokud máte v klasické metodě nasazení existující cloudový distribuční bod, počínaje verzí 1806, je nutné nasadit nový distribuční bod cloudu, aby bylo možné použít Azure Resource Manager metodu nasazení. Existují dvě možnosti:

- Pokud chcete znovu použít stejný název služby:  

    1. Nejprve odstraňte klasický cloudový distribuční bod. Pokud není k dispozici jiný distribuční bod cloudu, klienti nebudou moci získat obsah.  

    2. Vytvořte nový distribuční bod cloudu pomocí Správce prostředků nasazení. Znovu použijte stejný ověřovací certifikát serveru.  

    3. Distribuujte potřebný obsah balíčku softwaru do nového cloudového distribučního bodu.  

- Pokud chcete použít nový název služby:  

    1. Vytvořte nový distribuční bod cloudu pomocí Správce prostředků nasazení. Použijte nový ověřovací certifikát serveru.  

    2. Distribuujte potřebný obsah balíčku softwaru do nového cloudového distribučního bodu.  

    3. Odstraňte klasický cloudový distribuční bod.

> [!Tip]  
> Chcete-li zjistit aktuální model nasazení distribučního bodu cloudu:<!--SCCMDocs issue #611-->  
>
> 1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **distribuční body cloudu** .  
> 2. Přidejte atribut **modelu nasazení** jako sloupec do zobrazení seznamu. Pro nasazení Správce prostředků je tento atribut **Azure Resource Manager**.  

### <a name="stop-or-start-the-cloud-service-on-demand"></a>Zastavení nebo spuštění cloudové služby na vyžádání

Zastavit distribuční bod cloudu kdykoli v konzole Configuration Manager. Tato akce okamžitě zabrání klientům stahovat další obsah ze služby. Chcete-li obnovit přístup pro klienty, restartujte cloudovou službu z konzoly Configuration Manager. Například zastavte cloudovou službu, když dosáhne prahové hodnoty dat.  

Když zastavíte distribuční bod cloudu, cloudová služba neodstraní obsah z účtu úložiště. Zároveň nebrání serveru lokality v přenosu dalšího obsahu do distribučního bodu cloudu. Bod správy stále vrátí distribuční bod cloudu klientům jako platný zdroj obsahu.

K zastavení cloudového distribučního bodu použijte následující postup:  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** . Rozbalte položku **Cloud Services**a vyberte uzel **distribuční body cloudu** .  

2. Vyberte distribuční bod cloudu. Pokud chcete zastavit cloudovou službu, která běží v Azure, vyberte na pásu karet **Zastavit službu** .  

3. Vyberte možnost **Spustit službu** pro restartování distribučního bodu cloudu.  

### <a name="delete-a-cloud-distribution-point"></a>Odstranit distribuční bod cloudu

Chcete-li odinstalovat distribuční bod cloudu, vyberte distribuční bod v konzole Configuration Manager a pak vyberte možnost **Odstranit**.  

Když odstraníte distribuční bod cloudu z hierarchie nástroje, Configuration Manager odebere obsah z cloudové služby v Azure.

Ruční odebráním všech komponent v Azure dojde k nekonzistenci systému. Tento stav opouští osamocené informace a může dojít k neočekávanému chování.


## <a name="advanced-troubleshooting"></a><a name="bkmk_tshoot"></a>Pokročilé řešení potíží

Pokud potřebujete shromáždit diagnostické protokolování z virtuálních počítačů Azure, abyste mohli řešit problémy s distribučním bodem cloudu, použijte následující ukázku PowerShellu k povolení rozšíření služby pro toto předplatné:<!--514275-->  

``` PowerShell
# Change these variables for your Azure environment. The current values are provided as examples. You can find the values for these from the Azure portal.
$storage_name="4780E38368358502‬‭23C071" # The name of the storage account that goes with the CloudDP
$key="3jSyvMssuTyAyj5jWHKtf2bV5JF^aDN%z%2g*RImGK8R4vcu3PE07!P7CKTbZhT1Sxd3l^t69R8Cpsdl1xhlhZtl" # The storage access key from the Storage Account view
$service_name="4780E38368358502‬‭23C071" # The name of the cloud service for the CloudDP, which for a Cloud DP is the same as the storage name
$azureSubscriptionName="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription name the tenant is using
$subscriptionId="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription ID the tenant is using

# This variable is the path to the config file on the local computer.
$public_config="F:\PowerShellDiagFile\diagnostics.wadcfgx"

# These variables are for the Azure management certificate. Install it in the Current User certificate store on the system running this script.
$thumbprint="dac9024f54d8f6df94935fb1732638ca6ad77c13" # The thumbprint of the Azure management certificate
$mycert = Get-Item cert:\\CurrentUser\My\$thumbprint

Set-AzureSubscription -SubscriptionName $azureSubscriptionName -SubscriptionId $subscriptionId -Certificate $mycert

Select-AzureSubscription $azureSubscriptionName

Set-AzureServiceDiagnosticsExtension -StorageAccountName $storage_name -StorageAccountKey $key -DiagnosticsConfigurationPath $public_config –ServiceName $service_name -Slot 'Production' -Verbose
```

Následující ukázka je příkladem souboru **Diagnostics. wadcfgx** , na který se odkazuje v proměnné **public_config** ve výše uvedeném skriptu PowerShellu. Další informace najdete v tématu [schéma konfigurace rozšíření Azure Diagnostics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics-schema).  

``` XML
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
      <Directories scheduledTransferPeriod="PT1M">
        <IISLogs containerName ="wad-iis-logfiles" />
        <FailedRequestLogs containerName ="wad-failedrequestlogs" />
      </Directories>
      <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Application!*" />
      </WindowsEventLog>
      <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Information" />
      <CrashDumps dumpType="Full">
        <CrashDumpConfiguration processName="WaAppAgent.exe" />
        <CrashDumpConfiguration processName="WaIISHost.exe" />
        <CrashDumpConfiguration processName="WindowsAzureGuestAgent.exe" />
        <CrashDumpConfiguration processName="WaWorkerHost.exe" />
        <CrashDumpConfiguration processName="DiagnosticsAgent.exe" />
        <CrashDumpConfiguration processName="w3wp.exe" />
      </CrashDumps>
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      </PerformanceCounters>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```
