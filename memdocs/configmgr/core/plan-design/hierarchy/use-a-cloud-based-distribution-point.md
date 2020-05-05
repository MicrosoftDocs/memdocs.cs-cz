---
title: Distribuční bod cloudu
titleSuffix: Configuration Manager
description: Plánování a návrh distribuce obsahu softwaru prostřednictvím Microsoft Azure s distribučními body cloudu v Configuration Manager.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7a14b79a9e7fd91b6470836b4271a669725065bd
ms.sourcegitcommit: 568f8f8c19fafdd0f4352d0682f1ca7a4d665d25
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/22/2020
ms.locfileid: "81771174"
---
# <a name="use-a-cloud-distribution-point-in-configuration-manager"></a>Použití distribučního bodu cloudu v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

> [!Important]  
> Implementace pro sdílení obsahu z Azure se změnila. Pomocí brány pro správu cloudu s povoleným obsahem povolte, aby služba **CMG mohla fungovat jako distribuční bod cloudu a poskytovala obsah z Azure Storage**. Další informace najdete v tématu [Úprava CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg).
>
> V budoucnu nebudete moci vytvořit tradiční distribuční bod cloudu. Další informace najdete v tématu [odebrané a zastaralé funkce](../changes/deprecated/removed-and-deprecated-cmfeatures.md).

Distribuční bod cloudu je Configuration Manager distribuční bod, jehož hostitelem je platforma jako služba (PaaS) v Microsoft Azure. Tato služba podporuje následující scénáře:  

- Poskytování obsahu softwaru pro internetové klienty bez další místní infrastruktury  

- Cloud – povolení systému distribuce obsahu  

- Snižte potřebu tradičních distribučních bodů  

Tento článek vám pomůže získat informace o distribučním bodu cloudu, naplánovat jeho použití a navrhnout implementaci. Obsahuje následující oddíly:

- [Funkce a výhody](#bkmk_features)
- [Návrh topologie](#bkmk_topology)
- [Požadavky](#bkmk_requirements)
- [Specifikace](#bkmk_spec)
- [Náklady](#bkmk_cost)
- [Výkon a škálování](#bkmk_perf)
- [Porty a tok dat](#bkmk_dataflow)
- [Certifikáty](#bkmk_certs)
- [Nejčastější dotazy](#bkmk_faq)


## <a name="features-and-benefits"></a><a name="bkmk_features"></a>Funkce a výhody

### <a name="features"></a>Funkce

Distribuční bod cloudu podporuje několik funkcí, které jsou také nabízeny místními distribučními body:  

- Správa distribučních bodů cloudu individuálně nebo jako členové skupin distribučních bodů  

- Použití distribučního bodu cloudu jako záložního umístění obsahu  

- Podporuje intranetové i internetové klienty.  

### <a name="benefits"></a>Výhody

Distribuční bod cloudu přináší následující další výhody:  

- Lokalita šifruje obsah před odesláním do distribučního bodu cloudu v Azure.  

- Pokud chcete splnit měnící se požadavky na požadavky na obsah od klientů, proveďte ruční škálování cloudové služby v Azure. Tato akce nevyžaduje, abyste nainstalovali a zřídili další distribuční body v Configuration Manager.  

- Podporuje stahování obsahu od klientů nakonfigurovaných pro jiné technologie obsahu, jako je Windows BranchCache a alternativní poskytovatelé obsahu.  

- Počínaje verzí 1806 použijte distribuční body cloudu jako umístění zdroje pro distribuční body pro vyžádání obsahu.  


## <a name="topology-design"></a><a name="bkmk_topology"></a>Návrh topologie

Nasazení a provoz distribučního bodu cloudu zahrnuje následující součásti:  

- **Cloudová služba** v Azure. Lokalita distribuuje obsah do této služby, která ho ukládá do cloudového úložiště Azure. Bod správy poskytuje klientům toto umístění obsahu v seznamu dostupných zdrojů podle potřeby.  

- Požadavky klienta role systému lokality **bodu správy** na normální.  

    - Místní klienti obvykle používají místní bod správy.  

    - Internetoví klienti buď používají [bránu pro správu cloudu](../../clients/manage/cmg/plan-cloud-management-gateway.md), nebo [internetový bod správy](../../clients/manage/plan-internet-based-client-management.md).  

- Distribuční bod cloudu používá webovou službu **https založenou na certifikátech** , která usnadňuje zabezpečení síťové komunikace s klienty. Klienti musí důvěřovat tomuto certifikátu.  

### <a name="azure-resource-manager"></a>Azure Resource Manager

<!--1322209-->
Počínaje verzí 1806 vytvořte distribuční bod cloudu pomocí **nasazení Azure Resource Manager**. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) je moderní platforma pro správu všech prostředků řešení jako jedné entity, která se označuje jako [Skupina prostředků](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). Při nasazování cloudového distribučního bodu s Azure Resource Manager lokalita používá Azure Active Directory (Azure AD) k ověření a vytvoření potřebných cloudových prostředků. Toto moderní nasazení nevyžaduje klasický certifikát pro správu Azure.  

> [!Note]  
> Tato funkce nepovoluje podporu pro poskytovatele cloudových služeb Azure (CSP). Nasazení distribučního bodu cloudu pomocí Azure Resource Manager nadále používá klasickou cloudovou službu, kterou CSP nepodporuje. Další informace najdete v tématu [dostupné služby Azure v CSP Azure](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

Počínaje verzí 1902 Configuration Manager Azure Resource Manager je jediným mechanismem nasazení pro nové instance distribučního bodu cloudu. Existující nasazení budou fungovat i nadále.<!-- 3605704 -->

V Configuration Manager verze 1810 a starší podporuje Průvodce distribučním bodem cloudu i možnost **nasazení klasické služby** pomocí certifikátu pro správu Azure. Pro zjednodušení nasazení a správy prostředků použijte model nasazení Azure Resource Manager pro všechny nové distribuční body cloudu. Pokud je to možné, znovu nasaďte existující cloudové distribuční body prostřednictvím Správce prostředků.

> [!Important]  
> Počínaje verzí 1810 je nasazení klasické služby v Azure zastaralé pro použití v Configuration Manager. Tato verze je poslední, aby podporovala vytváření těchto nasazení Azure. Tato funkce bude odebrána v budoucí verzi Configuration Manager.<!--SCCMDocs-pr issue #2993-->  

Configuration Manager nemigruje stávající klasické cloudové distribuční body do modelu nasazení Azure Resource Manager. Pomocí Azure Resource Manager nasazení vytvořte nové distribuční body cloudu a pak odeberte klasické cloudové distribuční body.

### <a name="hierarchy-design"></a>Návrh hierarchie

Místo vytvoření distribučního bodu cloudu závisí na tom, kteří klienti potřebují k obsahu přistupovat. Počínaje verzí 1806 jsou k dispozici tři typy distribučních bodů cloudu:  

- Nasazení Azure Resource Manager: Tento typ vytvořte v primární lokalitě nebo lokalitě centrální správy.  

- Nasazení klasické služby: Tento typ vytvořte pouze v primární lokalitě.  

- Brána pro správu cloudu může také poskytovat obsah klientům. Tato funkce snižuje nároky na požadované certifikáty a náklady na virtuální počítače Azure. Další informace najdete v tématu [Plánování brány pro správu cloudu](../../clients/manage/cmg/plan-cloud-management-gateway.md).<!--1358651-->  

Pokud chcete zjistit, jestli se mají do skupin hranic zahrnout distribuční body cloudu, vezměte v úvahu následující chování:  

- Internetoví klienti nespoléhají na skupiny hranic. Používají jenom internetové distribuční body nebo cloudové distribuční body. Pokud k obsluhování těchto typů klientů používáte pouze distribuční body cloudu, pak je nemusíte zahrnout do skupin hranic.  

- Pokud chcete, aby klienti ve vaší interní síti používali distribuční bod cloudu, musí být ve stejné skupině hranic jako klienti. Klienti nastavují prioritu distribučních bodů cloudu jako poslední v seznamu zdrojů obsahu, protože jsou spojené s stažením obsahu mimo Azure. Cloudový distribuční bod se obvykle používá jako záložní zdroj pro intranetové klienty. Pokud chcete vytvořit návrh cloudu, pak Navrhněte skupiny hranic tak, aby splňovaly tento obchodní požadavek. Další informace najdete v tématu [Konfigurace skupin hranic](../../servers/deploy/configure/boundary-groups.md).  

I když nainstalujete distribuční body cloudu v konkrétních oblastech Azure, klienti si nevědí o oblastech Azure. Náhodně si vyberou distribuční bod cloudu. Pokud nainstalujete distribuční body cloudu do několika oblastí a klient obdrží více než jednu položku v seznamu umístění obsahu, klient nemusí používat distribuční bod cloudu ze stejné oblasti Azure.  

### <a name="backup-and-recovery"></a>Backup a obnovení  

Při použití distribučního bodu cloudu ve vaší hierarchii vám při plánování zálohování a obnovení použijte následující informace:  

- Když použijete úlohu údržby **Zálohovat server webu** , Configuration Manager automaticky zahrnuje konfigurace distribučního bodu cloudu.  

- Zálohujte a uložte kopii ověřovacího certifikátu serveru. Pokud používáte nasazení klasické služby v Azure, zálohujte a uložte kopii certifikátu pro správu Azure. Když obnovíte Configuration Manager primární lokalitu na jiný server, musíte znovu naimportovat certifikáty.  


## <a name="requirements"></a><a name="bkmk_requirements"></a>Požadavků

- K hostování služby potřebujete **předplatné Azure** .  

    - **Správce Azure** se musí zúčastnit prvotního vytváření určitých součástí v závislosti na vašem návrhu. Tento uživatel nevyžaduje oprávnění v Configuration Manager.  

- Webový server vyžaduje **přístup k Internetu** pro nasazení a správu cloudové služby.  

- Při použití metody nasazení **Azure Resource Manager** můžete integrovat Configuration Manager se službou [Azure AD](../../servers/deploy/configure/azure-services-wizard.md) pro **správu cloudu**. *Zjišťování uživatelů* služby Azure AD není vyžadováno.  

- **Certifikát ověřování serveru**. Další informace najdete v části [certifikáty](#bkmk_certs) níže.  

    - K omezení složitosti použijte poskytovatele veřejného certifikátu pro ověřovací certifikát serverů. Když to uděláte, budete pro klienty potřebovat také **alias DNS CNAME** , aby bylo možné přeložit název cloudové služby.  

- V Configuration Manager verze 1810 nebo starší, pokud používáte metodu nasazení Azure Classic, potřebujete **certifikát pro správu Azure**. Další informace najdete v části [certifikáty](#bkmk_certs) níže.  

    > [!TIP]  
    > Počínaje verzí 1806 Configuration Manager použijte model nasazení **Azure Resource Manager** . Nevyžaduje tento certifikát pro správu.  
    >
    > Metoda klasického nasazení je zastaralá od verze 1810.  

- Nastavte nastavení klienta, **povolte přístup ke cloudovým distribučním bodům**, na **ano** ve skupině **Cloud Services** . Ve výchozím nastavení je tato hodnota nastavena na **Ne**.  

- Klientská zařízení vyžadují **připojení k Internetu**a musí používat **protokol IPv4**.  


## <a name="specifications"></a><a name="bkmk_spec"></a>Tématech

- Distribuční bod cloudu podporuje všechny verze systému Windows, které jsou uvedeny v části [podporované operační systémy pro klienty a zařízení](../configs/supported-operating-systems-for-clients-and-devices.md).  

- Správce distribuuje následující typy podporovaného softwarového obsahu:  
  - Aplikace
  - Balíčky
  - Balíčky s upgradem operačního systému
  - Aktualizace softwaru třetích stran  

    > [!Important]  
    > - I když konzola Configuration Manager neblokuje distribuci aktualizací softwaru Microsoftu do cloudového distribučního bodu, platíte za Azure náklady na ukládání obsahu, který klienti nepoužívají. Internetoví klienti vždy získávají obsah aktualizace softwaru společnosti Microsoft z cloudové služby Microsoft Update. Nedistribuujte aktualizace softwaru od Microsoftu do cloudového distribučního bodu.
    > - Při použití CMG pro úložiště obsahu se nebude obsah pro aktualizace třetích stran stahovat do klientů, pokud je povolený **rozdílový obsah ke stažení, pokud** je povolené [nastavení klienta](../../clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) dostupné. <!--6598587--> 

- Počínaje verzí 1806 nakonfigurujte distribuční bod pro vyžádání obsahu tak, aby jako zdroj používal distribuční bod cloudu. Další informace najdete v tématu [zdrojové distribuční body](use-a-pull-distribution-point.md#about-source-distribution-points).<!--1321554-->  

### <a name="deployment-settings"></a>Nastavení nasazení

- Když nasadíte pořadí úkolů s možností **stahovat obsah místně v případě potřeby spuštěním pořadí úloh**, bod správy neobsahuje distribuční bod cloudu jako umístění obsahu. Nasaďte pořadí úkolů s možností **stahovat veškerý obsah místně před spuštěním pořadí úkolů** , aby klienti mohli používat distribuční bod cloudu.  

- Distribuční bod cloudu nepodporuje nasazení balíčků s možností **Spustit program z distribučního bodu**. Pomocí možnosti nasazení můžete **Stáhnout obsah z distribučního bodu a spustit místně**.  

### <a name="limitations"></a>Omezení  

- Distribuční bod cloudu nelze použít pro nasazení pomocí technologie PXE nebo vícesměrového vysílání.  

- Distribuční bod cloudu nepodporuje aplikace streamování sady App-V.  

- Nemůžete [připravit obsah](manage-network-bandwidth.md#BKMK_PrestagingContent) v cloudovém distribučním bodě. Správce distribuce primární lokality, která spravuje distribuční bod cloudu, přenáší veškerý obsah.  

- Distribuční bod cloudu nelze konfigurovat jako distribuční bod pro vyžádání obsahu.  


## <a name="cost"></a><a name="bkmk_cost"></a>Ze

<!--501018-->
> [!IMPORTANT]  
> Následující informace o nákladech slouží pouze k odhadování účelu. Vaše prostředí může mít jiné proměnné, které mají vliv na celkové náklady na používání cloudového distribučního bodu.  

Configuration Manager obsahují následující možnosti, které vám pomůžou řídit náklady a monitorovat přístup k datům:  

- Řízení a monitorování množství obsahu uloženého v cloudové službě. Další informace najdete v tématu [monitorování distribučních bodů cloudu](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor).  

- Nakonfigurujte Configuration Manager, aby vás upozornily na to, že prahové hodnoty pro stahování klientů splňují nebo překračují měsíční limity. Další informace najdete v tématu [výstrahy prahové hodnoty přenosu dat](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_alerts).

- Chcete-li snížit počet přenosů dat z distribučních bodů cloudu klienty, použijte jednu z následujících technologií pro ukládání do mezipaměti.  
  - Configuration Manager sdílené mezipaměti
  - Služba BranchCache systému Windows
  - Optimalizace doručování Windows 10  

    Další informace najdete v tématu [základní koncepty správy obsahu](fundamental-concepts-for-content-management.md).  

### <a name="components"></a>Komponenty

Distribuční bod cloudu používá následující součásti Azure, které se účtují za účet předplatného Azure:  

> [!Tip]  
> Od verze 1806 může Brána pro správu cloudu taky poskytovat obsah klientům. Tato funkce snižuje náklady sloučením virtuálních počítačů Azure. Další informace najdete v tématu [náklady na bránu pro správu cloudu](../../clients/manage/cmg/plan-cloud-management-gateway.md#cost).  

#### <a name="virtual-machine"></a>Virtuální počítač

- Distribuční bod cloudu používá jako službu PaaS (Platform as a Service) Azure Cloud Services. Tato služba používá virtuální počítače, které účtují výpočetní náklady.  

- Každá služba distribučního bodu cloudu používá dva standardní virtuální počítače a0.  

- Podívejte se na [cenové kalkulačky Azure](https://azure.microsoft.com/pricing/calculator/) , které vám pomůžou určit možné náklady.

    > [!NOTE]  
    > Náklady na virtuální počítač se liší podle oblasti.

#### <a name="outbound-data-transfer"></a>Přenos odchozích dat

- Všechny toky dat do Azure jsou bezplatné (příchozí nebo odeslaný). Distribuce obsahu z lokality do distribučního bodu cloudu se odesílá do Azure.  

- Poplatky se účtují na základě toku dat z Azure (výstup nebo stažení). Tok dat distribučního bodu cloudu z Azure se skládá z softwarového obsahu, který klienti stahují.  

- Další informace najdete v tématu [monitorování distribučních bodů cloudu](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor).  

- Další informace o cenách najdete v [podrobnostech o cenách šířky pásma Azure](https://azure.microsoft.com/pricing/details/bandwidth/) . Ceny za přenos dat jsou vrstveny. Tím více využijete, tím méně platíte za gigabajt.  

#### <a name="content-storage"></a>Úložiště obsahu

- Internetoví klienti získají zdarma obsah aktualizace softwaru společnosti Microsoft z cloudové služby Microsoft Update. Nedistribuujte balíčky nasazení aktualizace softwaru s aktualizacemi softwaru Microsoftu do distribučního bodu cloudu. V opačném případě budete mít náklady na úložiště dat pro obsah, který klienti nikdy nepoužívají.  

- Distribuční body cloudu využívají v závislosti na modelu nasazení následující standardní úložiště objektů BLOB:  

    - Nasazení Azure Resource Manager používá místně redundantní úložiště Azure (LRS). Tato změna snižuje náklady na účet úložiště. Klasické nasazení nepoužívá další funkce GRS. Další informace najdete v tématu [místně redundantní úložiště](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs).  

    - Klasické nasazení s Configuration Manager verze 1810 nebo starší používá geograficky redundantní úložiště Azure (GRS). Další informace najdete v tématu [geograficky redundantní úložiště](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs).  

#### <a name="other-costs"></a>Další náklady

- Každá cloudová služba má dynamickou IP adresu. Každý z různých distribučních bodů cloudu používá novou dynamickou IP adresu. Přidání dalších virtuálních počítačů na cloudovou službu tyto adresy nezvyšuje.  


## <a name="ports-and-data-flow"></a><a name="bkmk_dataflow"></a>Porty a tok dat

Pro cloudový distribuční bod existují dva primární datové toky:  

- Webový server se připojí k Azure a nastaví službu distribučního bodu cloudu.  

- Klient se připojí k distribučnímu bodu cloudu, aby mohl stáhnout obsah.  

### <a name="site-server-to-azure"></a>Webový server do Azure

Nemusíte otevírat žádné příchozí porty v místní síti. Server lokality iniciuje veškerou komunikaci s Azure a cloudovým distribučním bodem pro nasazení, aktualizaci a správu cloudové služby. Server lokality potřebuje vytvořit odchozí připojení ke cloudu Microsoftu. Tato akce je stejná jako instalace role systému lokality distribučního bodu v určité lokalitě.  

### <a name="client-to-cloud-distribution-point"></a>Klient do cloudového distribučního bodu

Nemusíte otevírat žádné příchozí porty v místní síti. Internetoví klienti komunikují přímo se službou Azure. Klienti ve vaší interní síti, kteří používají distribuční bod cloudu, se musí připojit ke cloudu Microsoftu.

Další informace o prioritě umístění obsahu a o tom, kdy intranetové klienty používají distribuční bod cloudu, najdete v tématu [Priorita zdroje obsahu](fundamental-concepts-for-content-management.md#content-source-priority).

Když klient použije distribuční bod cloudu jako umístění obsahu:  

1. Bod správy dává klientovi přístupový token společně se seznamem zdrojů obsahu. Tento token je platný po dobu 24 hodin a poskytuje klientovi přístup k distribučnímu bodu cloudu.  

2. Bod správy reaguje na požadavek na umístění klienta s **plně kvalifikovaným názvem domény** cloudového distribučního bodu. Tato vlastnost je stejná jako běžný název ověřovacího certifikátu serveru.  

    Pokud používáte název domény, například WallaceFalls.contoso.com, klient se nejprve pokusí přeložit tento plně kvalifikovaný název domény. Pokud chcete, aby klienti mohli přeložit název služby Azure, třeba: WallaceFalls.cloudapp.net, budete potřebovat alias CNAME v internetové službě DNS s přístupem k Internetu.  

3. Klient dále přeloží název služby Azure, například WallaceFalls.cloudapp.net, na platnou IP adresu. Tato odpověď by měla být zpracována DNS Azure.  

4. Klient se připojí k distribučnímu bodu cloudu. Azure vyrovnává zatížení připojení k jedné z instancí virtuálních počítačů. Klient se sám ověřuje pomocí přístupového tokenu.  

5. Distribuční bod cloudu ověřuje přístupový token klienta a pak klientovi poskytuje přesné umístění obsahu ve službě Azure Storage.  

6. Pokud klient důvěřuje ověřovacímu certifikátu serveru distribučního bodu cloudu, připojí se ke službě Azure Storage a stáhne obsah.


## <a name="performance-and-scale"></a><a name="bkmk_perf"></a>Výkon a škálování

<!--494872-->

Stejně jako u všech návrhů distribučních bodů Vezměte v úvahu následující faktory:  

- Počet souběžných připojení klientů
- Velikost obsahu, který stahují klienti
- Doba, po kterou je možné splnit vaše podnikové požadavky

V závislosti na [návrhu topologie](#bkmk_topology)mají klienti možnost mít pro libovolný obsah více než jeden distribuční bod cloudu, a to přirozeně náhodně náhodně v těchto cloudových službách. Pokud distribuujete jenom určitý obsah do jednoho cloudového distribučního bodu a velký počet klientů se pokusí stáhnout tento obsah ve stejnou chvíli, tato aktivita zajistí vyšší zatížení tohoto jednoho cloudového distribučního bodu. Přidání dalšího distribučního bodu cloudu zahrnuje také samostatnou službu Azure Storage. Další informace o tom, jak klient komunikuje s komponentami distribučního bodu cloudu a stahuje obsah, najdete v tématu [porty a tok dat](#bkmk_dataflow).  

Distribuční bod cloudu používá dva virtuální počítače Azure jako front-end pro Azure Storage. Toto výchozí nasazení splňuje většinu potřeb zákazníků. V některých extrémních případech s velkým počtem souběžných připojení klientů (například 150 000 klientů) nedokáže zpracování virtuálních počítačů Azure udržovat požadavky klientů na kapacitu. Nemůžete změnit velikost virtuálních počítačů Azure používaných pro cloudový distribuční bod. I když nemůžete nakonfigurovat počet instancí virtuálních počítačů pro distribuční bod cloudu v Configuration Manager v případě potřeby překonfigurujte cloudovou službu v Azure Portal. Buď ručně přidejte více instancí virtuálních počítačů, nebo nakonfigurujte službu tak, aby se automaticky škálovat.

> [!Important]  
> Když aktualizujete Configuration Manager, lokalita znovu nasadí cloudovou službu. Pokud v Azure Portal ručně překonfigurujete cloudovou službu, počet instancí se obnoví na výchozí hodnotu dvě.  

Služba Azure Storage podporuje pro jeden soubor 500 požadavků za sekundu. Testování výkonu jednoho cloudového distribučního bodu, který podporuje distribuci jednoho souboru 100 MB na 50 000 klientů za 24 hodin.<!--512106-->  


## <a name="certificates"></a><a name="bkmk_certs"></a>Certifikáty  

V závislosti na návrhu distribučního bodu cloudu budete potřebovat jeden nebo více digitálních certifikátů.  

### <a name="general-information"></a>Obecné informace

<!--SCCMDocs issue #779-->
Certifikáty pro distribuční body cloudu podporují následující konfigurace:  

- Délka bitového klíče 4096

- Certifikáty verze 3. Další informace najdete v tématu [Přehled certifikátů CNG](../network/cng-certificates-overview.md).  

- Počínaje verzí 1802 se při konfiguraci systému Windows pomocí následujících zásad: **Kryptografie systému: pro šifrování, generování hodnot hash a podepisování použít algoritmy kompatibilní se standardem FIPS**  

- Od verze 1802 se podpora TLS 1,2. Další informace najdete v tématu [technické informace o ovládacích prvcích kryptografie](../security/cryptographic-controls-technical-reference.md#about-ssl-vulnerabilities).  

### <a name="server-authentication-certificate"></a>Ověřovací certifikát serverů

*Tento certifikát je vyžadován pro všechna nasazení distribučních bodů cloudu.*

Další informace najdete v tématu [ověřovací certifikát serveru CMG](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_serverauth)a v následujících pododdílech, podle potřeby:  

- CMG důvěryhodný kořenový certifikát pro klienty
- Certifikát ověřování serveru vydaný veřejným poskytovatelem
- Certifikát ověřování serveru vydaný z podnikové infrastruktury veřejných klíčů

Distribuční bod cloudu používá tento typ certifikátu stejným způsobem jako brána pro správu cloudu. Klienti musí také důvěřovat tomuto certifikátu. Microsoft doporučuje použít certifikát vydaný veřejným poskytovatelem, aby se snížila složitost.

Pokud nepoužíváte certifikát se zástupnými znaky, nepoužívejte stejný certifikát znovu. Každá instance distribučního bodu cloudu a brány pro správu cloudu vyžaduje jedinečný certifikát ověřování serveru.

Další informace o vytváření tohoto certifikátu z PKI najdete v tématu [Nasazení certifikátu služby pro cloudové distribuční body](../network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012).  

### <a name="azure-management-certificate"></a>Certifikát pro správu Azure

*Tento certifikát je nutný pro nasazení v klasickém provozu. Nevyžaduje se pro Azure Resource Manager nasazení.*

> [!Important]  
> Počínaje verzí 1806 Configuration Manager použijte model nasazení **Azure Resource Manager** . Nevyžaduje tento certifikát pro správu.  
>
> Metoda klasického nasazení je zastaralá od verze 1810.  
>
> Počínaje verzí 1902 Configuration Manager Azure Resource Manager je jediným mechanismem nasazení pro nové instance distribučního bodu cloudu. Tento certifikát se nevyžaduje v Configuration Manager verze 1902 nebo novější.<!-- 3605704 -->

Pokud používáte metodu nasazení Azure Classic s Configuration Manager verze 1810 nebo starší, potřebujete **certifikát pro správu Azure**. Další informace najdete v části [certifikát pro správu Azure](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_azuremgmt) v článku certifikáty brány pro správu cloudu. Server lokality Configuration Manager používá tento certifikát k ověřování pomocí Azure k vytvoření a správě klasického nasazení.  

Pro snížení složitosti použijte stejný certifikát pro správu Azure pro všechna nasazení Classic cloudových distribučních bodů a bran pro správu cloudu napříč všemi předplatnými Azure a všemi Configuration Manager lokalitami.


## <a name="frequently-asked-questions-faq"></a><a name="bkmk_faq"></a>Nejčastější dotazy – Nejčastější dotazy

### <a name="does-a-client-need-a-certificate-to-download-content-from-a-cloud-distribution-point"></a>Potřebuje klient certifikát ke stažení obsahu z distribučního bodu cloudu?

Certifikát ověřování klienta není povinný. Klient musí důvěřovat ověřovacímu certifikátu serveru, který používá cloudový distribuční bod. Pokud je tento certifikát vydaný poskytovatelem veřejného certifikátu, pak většina zařízení s Windows už pro tyto poskytovatele zahrnuje důvěryhodné kořenové certifikáty. Pokud jste vystavili certifikát pro ověřování serveru z infrastruktury veřejných klíčů vaší organizace, musí si klienti důvěřovat vydaným certifikátům v celém řetězci. Tento řetěz zahrnuje kořenovou certifikační autoritu a všechny zprostředkující certifikační autority. V závislosti na návrhu infrastruktury veřejných klíčů může tento certifikát zavádět další složitost nasazení cloudového distribučního bodu. Aby se zabránilo této složitosti, společnost Microsoft doporučuje použít poskytovatele veřejného certifikátu, kterému již klienti důvěřují.  

### <a name="can-my-on-premises-clients-use-a-cloud-distribution-point"></a>Můžou místní klienti používat distribuční bod cloudu?

Ano. Pokud chcete, aby klienti ve vaší interní síti používali distribuční bod cloudu, musí být ve stejné skupině hranic jako klienti. Klienti nastavují prioritu distribučních bodů cloudu jako poslední v seznamu zdrojů obsahu, protože jsou spojené s stažením obsahu mimo Azure. Cloudový distribuční bod se proto obvykle používá jako záložní zdroj pro intranetové klienty. Pokud chcete vytvořit návrh cloudu, proveďte odpovídajícím způsobem návrh skupin hranic. Další informace najdete v tématu [Konfigurace skupin hranic](../../servers/deploy/configure/boundary-groups.md).  

### <a name="do-i-need-azure-expressroute"></a>Potřebuji Azure ExpressRoute?

[Azure ExpressRoute](/azure/expressroute/expressroute-introduction) umožňuje rozšiřování místní sítě do cloudu Microsoftu. ExpressRoute nebo jiná taková připojení k virtuální síti se pro distribuční bod cloudu Configuration Manager nevyžadují.  

Pokud vaše organizace používá ExpressRoute, izolujte předplatné Azure pro distribuční bod cloudu z předplatného, které používá ExpressRoute. Tato konfigurace zajišťuje, že distribuční bod cloudu není náhodně připojen tímto způsobem.  

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>Potřebuji zachovat virtuální počítače Azure?

Není nutná žádná údržba. Návrh distribučního bodu cloudu používá platformu Azure jako službu (PaaS). Pomocí předplatného, které zadáte, Configuration Manager vytvoří nezbytné virtuální počítače, úložiště a sítě. Azure zabezpečuje a aktualizuje virtuální počítače. Tyto virtuální počítače nejsou součástí vašeho místního prostředí, protože se jedná o případ s infrastrukturou jako službou (IaaS). Cloudový distribuční bod je PaaS, který rozšiřuje vaše Configuration Manager prostředí do cloudu. Další informace najdete v tématu [výhody zabezpečení pro model cloudové služby PaaS](https://docs.microsoft.com/azure/security/security-paas-deployments#security-advantages-of-a-paas-cloud-service-model).  

### <a name="does-the-cloud-distribution-point-use-azure-cdn"></a>Používá distribuční bod cloudu Azure CDN?

Azure Content Delivery Network (CDN) je globální řešení pro rychlé doručování obsahu s vysokou šířkou pásma díky ukládání obsahu do mezipaměti v strategicky umístěných fyzických uzlech po celém světě. Další informace najdete v tématu [co je Azure CDN?](https://docs.microsoft.com/azure/cdn/cdn-overview).

Distribuční bod cloudu Configuration Manager v tuto chvíli nepodporuje Azure CDN.


## <a name="next-steps"></a>Další kroky

[Instalace distribučních bodů cloudu](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)
