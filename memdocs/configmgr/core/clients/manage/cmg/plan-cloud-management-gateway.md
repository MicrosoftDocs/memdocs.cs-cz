---
title: Plánování brány pro správu cloudu
titleSuffix: Configuration Manager
description: Naplánujte a navrhněte bránu pro správu cloudu (CMG), abyste zjednodušili správu internetových klientů.
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 136e11f97849e5fd8a27d9f83ea1bd44791c492e
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715641"
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Plánování brány pro správu cloudu v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

<!--1101764-->
Brána pro správu cloudu (CMG) poskytuje jednoduchý způsob správy Configuration Manager klientů na internetu. Nasazením CMG jako cloudové služby v Microsoft Azure můžete spravovat tradiční klienty, kteří se přecházejí na Internet bez další místní infrastruktury. Nemusíte také zveřejňovat místní infrastrukturu s internetem.

> [!NOTE]
> Configuration Manager ve výchozím nastavení nepovolí tuto volitelnou funkci. Tuto funkci musíte před použitím povolit. Další informace naleznete v části [Enable optional features from updates](../../../servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

Po vytvoření požadavků se vytváření CMG skládá z následujících tří kroků v konzole Configuration Manager:

1. Nasaďte cloudovou službu CMG do Azure.
2. Přidejte roli spojovacího bodu CMG.
3. Nakonfigurujte role lokality a lokality pro službu.
Po nasazení a konfiguraci budou klienti bezproblémově přistupovat k místním rolím lokality bez ohledu na to, jestli jsou na intranetu nebo na internetu.

Tento článek poskytuje základní informace o CMG, návrhu, jak se ve vašem prostředí hodí, a naplánujte implementaci.

## <a name="scenarios"></a>Scénáře

Existuje několik scénářů, u kterých je CMG užitečné. Níže jsou uvedeny některé z častých scénářů:  

- Spravujte tradiční klienty Windows pomocí identity připojené k doméně služby Active Directory. Mezi tyto klienty patří Windows 8.1 a Windows 10. Používá certifikáty PKI k zabezpečení komunikačního kanálu. Mezi aktivity správy patří:  

  - Aktualizace softwaru a Endpoint Protection
  - Stav inventáře a klienta
  - Nastavení dodržování předpisů
  - Distribuce softwaru do zařízení
  - Pořadí úkolů místního upgradu Windows 10

- Spravujte tradiční klienty Windows 10 pomocí moderní identity, ať už je to hybridní nebo čistě cloudová doména – připojené k Azure Active Directory (Azure AD). Klienti používají Azure AD k ověřování místo certifikátů PKI. Použití Azure AD je jednodušší k nastavení, konfiguraci a údržbě než složitější systémy PKI. Aktivity správy jsou stejné jako první scénář a také:  

  - Distribuce softwaru uživateli  

- Nainstalujte klienta Configuration Manager do zařízení s Windows 10 přes Internet. Použití Azure AD umožňuje zařízení ověřit CMG pro registraci a přiřazení klienta. Klienta můžete nainstalovat ručně nebo pomocí jiné metody distribuce softwaru, například Microsoft Intune.  

- Nové zřizování zařízení s spolusprávou. Při automatickém zápisu stávajících klientů se CMG nevyžaduje pro spolusprávu. Vyžaduje se pro nová zařízení, která zahrnují Windows autopilot, Azure AD, Microsoft Intune a Configuration Manager. Další informace najdete v tématu věnovaném [cestám ke společné správě](../../../../comanage/quickstart-paths.md).

### <a name="specific-use-cases"></a>Konkrétní případy použití

V těchto scénářích mohou být uplatněny následující případy použití konkrétního zařízení:

- Roamingová zařízení, jako jsou laptopy  

- Vzdálená zařízení nebo firemní pobočky, které jsou levnější a efektivnější pro správu přes Internet než přes síť WAN nebo přes síť VPN.  

- Fúze a akvizice, kde může být nejjednodušší připojit zařízení ke službě Azure AD a spravovat je prostřednictvím CMG.  

- Klienti pracovní skupiny. Tato zařízení mohou vyžadovat další konfiguraci, například certifikáty.<!-- SCCMDocs#1925 -->

    Počínaje verzí 2002 Configuration Manager podporuje ověřování na základě tokenů, které může pomáhat se správou vzdálených klientů pracovní skupiny. Další informace najdete v tématu [ověřování založené na tokenech pro CMG](../../deploy/deploy-clients-cmg-token.md).

> [!Important]
> Ve výchozím nastavení všichni klienti obdrží zásady pro CMG a začnou je používat, když se stanou na internetu. V závislosti na scénáři a případu použití, který se vztahuje k vaší organizaci, možná budete muset určit rozsah používání CMG. Další informace najdete v tématu [Povolení použití klientského nastavení brány pro správu cloudu](../../deploy/about-client-settings.md#enable-clients-to-use-a-cloud-management-gateway) v klientech.

## <a name="topology-design"></a>Návrh topologie

### <a name="cmg-components"></a>Součásti CMG

Nasazení a provoz CMG zahrnuje následující komponenty:  

- **Cloudová služba CMG** v Azure ověřuje a přesměruje Configuration Manager požadavky klienta na bod připojení CMG.  

- Role systému lokality **spojovacího bodu CMG** umožňuje konzistentní a vysoce výkonné připojení z místní sítě ke službě CMG v Azure. Publikuje také nastavení do CMG, včetně informací o připojení a nastavení zabezpečení. Bod připojení CMG přesměruje požadavky klienta z CMG do místních rolí podle mapování adres URL.

- Role systému lokality [**spojovacího bodu služby**](../../../servers/deploy/configure/about-the-service-connection-point.md) spouští komponentu Cloud Service Manager, která zpracovává všechny úlohy nasazení CMG. Kromě toho monitoruje a hlásí informace o stavu a protokolování služby z Azure AD. Ujistěte se, že je váš spojovací bod služby v [online režimu](../../../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes).  

- Požadavky klientů služby role systému lokality **bodu správy** na normální.

- Požadavky klientů na službu role systému lokality **bodu aktualizace softwaru** na normální.

    > [!NOTE]
    > Pokyny pro změnu velikosti pro body správy a body aktualizace softwaru se nemění bez ohledu na to, zda jsou místní nebo internetové klienty. Další informace najdete v tématu věnovaném [velikostem a škálováním čísel](../../../plan-design/configs/size-and-scale-numbers.md#management-point).

- **Internetoví klienti** se připojují k CMG pro přístup k místním součástem Configuration Manager.

- CMG používá webovou službu **https založenou na certifikátech** k zabezpečení síťové komunikace s klienty.  

- Internetoví klienti používají **certifikáty PKI nebo Azure AD** k ověřování identity a ověřování.  

- [**Distribuční bod cloudu**](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) poskytuje podle potřeby obsah pro internetové klienty.  

  - CMG může také poskytovat obsah klientům. Tato funkce snižuje nároky na požadované certifikáty a náklady na virtuální počítače Azure. Další informace najdete v tématu [Úprava CMG](setup-cloud-management-gateway.md#modify-a-cmg).<!--1358651-->  

### <a name="azure-resource-manager"></a>Azure Resource Manager

<!-- 1324735 -->
Vytvořte CMG pomocí **nasazení Azure Resource Manager**. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) je moderní platforma pro správu všech prostředků řešení jako jedné entity, která se označuje jako [Skupina prostředků](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). Když nasazujete CMG s Azure Resource Manager, lokalita používá Azure Active Directory (Azure AD) k ověření a vytvoření potřebných cloudových prostředků. Toto moderní nasazení nevyžaduje klasický certifikát pro správu Azure.  

> [!NOTE]
> Tato funkce nepovoluje podporu pro poskytovatele cloudových služeb Azure (CSP). Nasazení CMG s Azure Resource Manager nadále používá klasickou cloudovou službu, kterou CSP nepodporuje. Další informace najdete v tématu [dostupné služby Azure v CSP Azure](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-available-services).

Počínaje verzí 1902 Configuration Manager Azure Resource Manager je jediným mechanismem nasazení pro nové instance brány pro správu cloudu. Existující nasazení budou fungovat i nadále.<!-- 3605704 -->

V Configuration Manager verze 1810 a starší podporuje Průvodce CMG i možnost **nasazení klasické služby** pomocí certifikátu pro správu Azure. Pro zjednodušení nasazení a správy prostředků se doporučuje model nasazení Azure Resource Manager pro všechny nové instance CMG. Pokud je to možné, znovu nasaďte existující instance CMG prostřednictvím Správce prostředků. Další informace najdete v tématu [Úprava CMG](setup-cloud-management-gateway.md#modify-a-cmg).

> [!IMPORTANT]
> Nasazení klasické služby v Azure je zastaralé pro použití v Configuration Manager. Verze 1810 je poslední pro podporu vytváření těchto nasazení Azure. Tato funkce bude odebrána v budoucí verzi Configuration Manager.<!--SCCMDocs-pr issue #2993-->  

### <a name="hierarchy-design"></a>Návrh hierarchie

Vytvořte CMG v lokalitě nejvyšší úrovně ve vaší hierarchii. Pokud se jedná o lokalitu centrální správy, vytvořte body připojení CMG v podřízených primárních lokalitách. Součást cloudového portálu Service Manager je ve spojovacím bodu služby, který je také v lokalitě centrální správy. V případě potřeby může tento návrh sdílet službu v různých primárních lokalitách.

V Azure můžete vytvořit několik služeb CMG a můžete vytvořit několik přípojných bodů CMG. Několik přípojných bodů CMG poskytuje vyrovnávání zatížení klientského provozu z CMG do místních rolí.

Počínaje verzí 1902 můžete přidružit CMG k hraniční skupině. Tato konfigurace umožňuje klientům výchozí nebo záložní CMG pro komunikaci klientů podle [vztahů skupin hranic](../../../servers/deploy/configure/boundary-groups.md). Toto chování je užitečné hlavně v scénářích firemních poboček a VPN. Místo toho můžete směrovat klientský provoz z nákladných i pomalých připojení WAN, aby používal rychlejší služby v Microsoft Azure.<!--3640932-->

> [!NOTE]
> Internetoví klienti nespadají do žádné skupiny hranic.
>
> V Configuration Manager verze 1810 a starší CMG nespadají do žádné skupiny hranic.

Další faktory, jako je třeba počet klientů, které se mají spravovat, mají vliv na návrh CMG. Další informace najdete v tématu [výkon a škálování](#performance-and-scale).

#### <a name="example-1-standalone-primary-site"></a>Příklad 1: samostatná primární lokalita

Společnost Contoso má samostatnou primární lokalitu v místním datacentru v sídle v New York City.

- Vytvářejí CMG v oblasti Východní USA Azure, aby se snížila latence sítě.
- Vytvářejí dva spojovací body CMG, které jsou propojeny s jednou službou CMG.  

Když klienti přecházejí do Internetu, komunikují s CMG v oblasti Východní USA Azure. CMG předává tuto komunikaci prostřednictvím obou přípojných bodů CMG.

#### <a name="example-2-hierarchy"></a>Příklad 2: hierarchie

Čtvrtá káva má lokalitu centrální správy v místním datacentru v Seattlu. Jedna primární lokalita je ve stejném datovém centru a druhá primární lokalita se nachází v hlavní evropské kanceláři v Paříži.

- V lokalitě centrální správy vytvoří služba CMG ve Západní USA oblasti Azure. Škálují počet virtuálních počítačů pro očekávané zatížení cestovních klientů v celé hierarchii.
- V primární lokalitě založené na Seattlu vytvoří bod připojení CMG propojený s jedním CMG.
- V primární lokalitě založené na Paříži vytvoří spojovací bod CMG propojený s jedním CMG.

Když klienti přecházejí do Internetu, komunikují s CMG v oblasti Západní USA Azure. CMG předává tuto komunikaci do spojovacího bodu CMG v primární lokalitě přiřazené klientovi.

> [!TIP]
> Pro účely geografického umístění není nutné nasazovat více než jednu bránu pro správu cloudu. Configuration Manager klient se většinou netýká mírné latence, ke které může dojít u cloudové služby, a to i v případě geograficky vzdálené.

### <a name="test-environments"></a>Testovací prostředí
<!-- SCCMDocs#1225 -->
Mnoho organizací má samostatná prostředí pro produkční, testovací, vývojové nebo kvalitní zajištění. Při plánování nasazení CMG Vezměte v úvahu následující otázky:

- Kolik tenantů Azure AD má vaše organizace?
  - Existuje samostatný tenant pro testování?
  - Jsou identity uživatelů a zařízení ve stejném tenantovi?

- Kolik předplatných je v každém tenantovi?
  - Jsou k dispozici předplatná, která jsou specifická pro testování?

Služba Azure pro **správu cloudu** Configuration Manager podporuje víc klientů. Ke stejnému tenantovi se může připojit více Configuration Manager lokalit. Jedna lokalita může nasadit několik služeb CMG do různých předplatných. Do stejného předplatného může nasadit více lokalit služby CMG Services. Configuration Manager poskytuje flexibilitu v závislosti na vašem prostředí a obchodních požadavcích.

Další informace najdete v následujících nejčastějších dotazech: [účty uživatelů musí být ve stejném Tenantovi Azure AD jako tenant přidružený k předplatnému, které hostuje cloudovou službu CMG?](cloud-management-gateway-faq.md#bkmk_tenant)

## <a name="requirements"></a>Požadavky

- **Předplatné Azure** , které bude HOSTOVAT službu CMG.

    > [!IMPORTANT]
    > CMG nepodporuje předplatné s poskytovatelem Cloud Service (CSP) Azure.<!-- MEMDocs#320 -->

- Váš uživatelský účet musí být ve Configuration Manager správce infrastruktury s **úplnými oprávněními** nebo **správcem infrastruktury** .<!-- SCCMDocs#2146 -->

- **Správce Azure** se musí zúčastnit prvotního vytváření určitých součástí v závislosti na vašem návrhu. To může být stejné jako správce Configuration Manager, nebo oddělení. Pokud se liší, nevyžaduje oprávnění v Configuration Manager.

  - K nasazení CMG potřebujete **vlastníka předplatného** .
  - Pokud chcete web integrovat se službou Azure AD pro nasazení CMG pomocí Azure Resource Manager, budete potřebovat **globální správce** .

- Aspoň jeden místní Windows Server pro hostování **spojovacího bodu CMG**. Tuto roli můžete společně najít pomocí jiných Configuration Manager rolí systému lokality.  

- **Spojovací bod služby** musí být v [online režimu](../../../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes).  

- Integrace se službou **Azure AD** pro nasazení služby pomocí Azure Resource Manager. Další informace najdete v tématu [Konfigurace služeb Azure](../../../servers/deploy/configure/azure-services-wizard.md).  

- [**Ověřovací certifikát serveru**](certificates-for-cloud-management-gateway.md#bkmk_serverauth) pro CMG.  

- V závislosti na verzi operačního systému klienta a modelu ověřování mohou být vyžadovány **Další certifikáty** . Další informace najdete v tématu [certifikáty CMG](certificates-for-cloud-management-gateway.md).  

    Použijete-li možnost lokalita k **použití Configuration Manager generovaných certifikátů pro systémy lokality protokolu HTTP**, může být bod správy http. Další informace najdete v tématu [Rozšířená http](../../../plan-design/hierarchy/enhanced-http.md).

- Pokud používáte metodu nasazení Azure Classic, musíte v Configuration Manager verze 1810 nebo starší použít [**certifikát pro správu Azure**](certificates-for-cloud-management-gateway.md#bkmk_azuremgmt).  

    > [!TIP]  
    > Použijte model nasazení **Azure Resource Manager** . Nevyžaduje tento certifikát pro správu.
    >
    > Metoda klasického nasazení je zastaralá od verze 1810.  

- Klienti musí používat **protokol IPv4**.  

## <a name="specifications"></a>Specifikace

- Všechny verze systému Windows uvedené v [podporovaných operačních systémech pro klienty a zařízení](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) jsou podporovány pro CMG.  

- CMG podporuje pouze role bodu správy a bodu aktualizace softwaru.  

- CMG nepodporuje klienty, kteří komunikují pouze s adresami IPv6.<!--495606-->  

- Body aktualizace softwaru používající nástroj pro vyrovnávání zatížení sítě nefungují s CMG. <!--505311-->  

- CMG nasazení pomocí modelu prostředků Azure nepovolí podporu pro poskytovatele cloudových služeb Azure (CSP). Nasazení CMG s Azure Resource Manager nadále používá klasickou cloudovou službu, kterou CSP nepodporuje. Další informace najdete v tématu [služby Azure dostupné v programu Azure CSP](https://docs.microsoft.com/partner-center/azure-plan-available).

### <a name="support-for-configuration-manager-features"></a>Podpora funkcí Configuration Manager

V následující tabulce jsou uvedeny CMG podpora pro funkce Configuration Manager:

|Funkce  |Podpora  |
|---------|---------|
| Aktualizace softwaru     | ![Podporuje se](media/green_check.png) |
| Ochrana koncového bodu     | ![Podporovaná ](media/green_check.png) <sup> [Poznámka 1](#bkmk_note1)</sup> |
| Inventář hardwaru a softwaru     | ![Podporuje se](media/green_check.png) |
| Stav klienta a oznámení     | ![Podporuje se](media/green_check.png) |
| Spustit skripty     | ![Podporuje se](media/green_check.png) |
| Nastavení dodržování předpisů     | ![Podporuje se](media/green_check.png) |
| Instalace klienta<br>(s integrací Azure AD)     | ![Podporuje se](media/green_check.png) |
| Distribuce softwaru (zaměřená na zařízení)     | ![Podporuje se](media/green_check.png) |
| Distribuce softwaru (vyžaduje se pro uživatele)<br>(s integrací Azure AD)     | ![Podporuje se](media/green_check.png) |
| Distribuce softwaru (cílová a dostupná pro uživatele)<br>([všechny požadavky](../../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices)) | ![Podporuje se](media/green_check.png) |
| Pořadí úkolů místního upgradu Windows 10      | ![Podporuje se](media/green_check.png) |
| Sekvence úloh, které nepoužívají spouštěcí image a jsou nasazené s možností: **před spuštěním pořadí úloh stáhnout veškerý obsah místně**      | ![Podporuje se](media/green_check.png) |
| Sekvence úloh, které nepoužívají spouštěcí bitové kopie  | ![Podporuje se](media/green_check.png) (1910)|
| CMPivot     | ![Podporuje se](media/green_check.png) |
| Jakýkoli jiný scénář pořadí úkolů     | ![Nepodporuje se](media/Red_X.png) |
| Klientská nabízená instalace     | ![Nepodporuje se](media/Red_X.png) |
| Automatické přiřazení lokality     | ![Nepodporuje se](media/Red_X.png) |
| Žádosti o schválení softwaru     | ![Nepodporuje se](media/Red_X.png) |
| Konzola nástroje Configuration Manager     | ![Nepodporuje se](media/Red_X.png) |
| Vzdálené nástroje     | ![Nepodporuje se](media/Red_X.png) |
| Web vytváření sestav     | ![Nepodporuje se](media/Red_X.png) |
| Funkce vzdáleného probuzení Wake on LAN     | ![Nepodporuje se](media/Red_X.png) |
| Klienti se systémem Mac, Linux a UNIX     | ![Nepodporuje se](media/Red_X.png) |
| Sdílená mezipaměť     | ![Nepodporuje se](media/Red_X.png) |
| Místní správa MDM     | ![Nepodporuje se](media/Red_X.png) |
| Správa nástroje BitLocker     | ![Nepodporuje se](media/Red_X.png) |

|Klíč|
|--|
|![Podporuje se](media/green_check.png) = Tato funkce je podporována u CMG pro všechny podporované verze Configuration Manager  |
|![Podporováno ](media/green_check.png) (*YYMM*) = Tato funkce je podporována u CMG počínaje verzí *YYMM* Configuration Manager  |
|![Nepodporuje se](media/Red_X.png) = Tato funkce není u CMG podporována. |

#### <a name="note-1-support-for-endpoint-protection"></a><a name="bkmk_note1"></a>Poznámka 1: podpora pro Endpoint Protection
<!-- 4350561 -->
Aby zařízení připojená k doméně mohla použít zásady ochrany koncových bodů, vyžadují přístup k této doméně. Zařízení s nečastým přístupem k interní síti se můžou setkat s prodlevami při aplikování zásad ochrany koncových bodů. Pokud vyžadujete, aby zařízení ihned po jejich přijetí použili zásady ochrany koncových bodů, vezměte v úvahu jednu z následujících možností:

- Využijte spolusprávu a přepněte [Endpoint Protection úlohy](../../../../comanage/workloads.md#endpoint-protection) do Intune a spravujte [antivirovou ochranu v programu Microsoft Defender](https://docs.microsoft.com/mem/intune/configuration/device-restrictions-windows-10#microsoft-defender-antivirus) z cloudu.

- Použijte [položky konfigurace](../../../../compliance/deploy-use/create-configuration-items.md) namísto nativní funkce [antimalwarových](../../../../protect/deploy-use/endpoint-antimalware-policies.md) zásad, aby se použily zásady ochrany koncových bodů.

## <a name="cost"></a>Náklady

> [!IMPORTANT]  
> Následující informace o nákladech slouží pouze k odhadování účelu. Vaše prostředí může mít jiné proměnné, které mají vliv na celkové náklady na používání CMG.

CMG používá následující komponenty Azure, které se účtují za účet předplatného Azure:

### <a name="virtual-machine"></a>Virtuální počítač

- CMG používá Azure Cloud Services jako službu (PaaS). Tato služba používá virtuální počítače, které účtují výpočetní náklady.  

- CMG používá standardní virtuální počítač a2 v2.  

- Vyberte, kolik instancí virtuálních počítačů podporuje CMG. Jedna je výchozí hodnota a 16 je maximum. Toto číslo se nastaví při vytváření CMG a později se dá změnit, aby se služba mohla podle potřeby škálovat.

- Další informace o tom, kolik virtuálních počítačů potřebujete pro podporu klientů, najdete v tématu [výkon a škálování](#performance-and-scale).

- Podívejte se na [cenové kalkulačky Azure](https://azure.microsoft.com/pricing/calculator/) , které vám pomůžou určit možné náklady.

    > [!NOTE]  
    > Náklady na virtuální počítač se liší podle oblasti.

### <a name="outbound-data-transfer"></a>Přenos odchozích dat

- Poplatky se účtují na základě toku dat z Azure (výstup nebo stažení). Veškerá data toků do Azure jsou volná (příchozí nebo odesílací). CMG data z Azure zahrnují zásady pro klienta, oznámení klientů a odpovědi klientů předané CMG do lokality. Mezi tyto odpovědi patří sestavy inventáře, stavové zprávy a stav dodržování předpisů.  

- I bez jakýchkoli klientů, kteří komunikují s CMG, způsobí některá komunikace na pozadí síťový provoz mezi CMG a místní lokalitou.  

- Zobrazení **odchozích přenosů dat (GB)** v konzole Configuration Manager. Další informace najdete v tématu [monitorování klientů v CMG](monitor-clients-cloud-management-gateway.md).  

- Další informace o cenách najdete v [podrobnostech o cenách šířky pásma Azure](https://azure.microsoft.com/pricing/details/bandwidth/) . Ceny za přenos dat jsou vrstveny. Tím více využijete, tím méně platíte za gigabajt.  

- *Pro účely odhadování*je pro internetové klienty očekáváno přibližně 100-300 MB na klienta za měsíc. Nižší odhad je pro výchozí konfiguraci klienta. Horní odhad je pro účinnější konfiguraci klienta. Vaše skutečné využití se může lišit v závislosti na tom, jak konfigurujete nastavení klienta.  

    > [!NOTE]  
    > Provádění dalších akcí, jako je nasazení aktualizací softwaru nebo aplikací, zvyšuje objem odchozích přenosů dat z Azure.

- Internetoví klienti získají obsah aktualizace softwaru společnosti Microsoft od web Windows Update zdarma. Nedistribuujte balíčky aktualizací pomocí obsahu služby Microsoft Update do distribučního bodu cloudu, jinak můžete účtovat náklady na úložiště a výstup dat.  

- Nespravovaná konfigurace možnosti CMG pro **ověření odvolání klientského certifikátu** může způsobit další provoz od klientů až po CMG. Tento další provoz může zvýšit objem dat Azure pro výstup, což může zvýšit náklady na Azure.<!-- SCCMDocs#1434 --> Další informace najdete v tématu [publikování seznamu odvolaných certifikátů](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

### <a name="content-storage"></a>Úložiště obsahu

- Internetoví klienti získají obsah aktualizace softwaru společnosti Microsoft od web Windows Update zdarma. Nedistribuujte balíčky aktualizací pomocí obsahu služby Microsoft Update do distribučního bodu cloudu, jinak můžete účtovat náklady na úložiště a výstup dat.  

- Pro jakýkoliv jiný nezbytný obsah, jako jsou aplikace nebo aktualizace softwaru třetích stran, musíte distribuovat do cloudového distribučního bodu. V současné době CMG podporuje pouze distribuční bod cloudu pro posílání obsahu klientům.
   - Při použití CMG pro úložiště obsahu se nebude obsah pro aktualizace třetích stran stahovat do klientů, pokud je povolený **rozdílový obsah ke stažení, pokud** je povolené [nastavení klienta](../../deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) dostupné. <!--6598587--> 

- Další informace najdete v tématu náklady na používání [cloudových distribučních bodů](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_cost).  

- CMG může být také distribučním bodem cloudu pro poskytování obsahu klientům. Tato funkce snižuje nároky na požadované certifikáty a náklady na virtuální počítače Azure. Další informace najdete v tématu [Úprava CMG](setup-cloud-management-gateway.md#modify-a-cmg).<!--1358651-->  

- CMG používá místně redundantní úložiště Azure (LRS). Další informace najdete v tématu [místně redundantní úložiště](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs).  

### <a name="other-costs"></a>Další náklady

- Každá cloudová služba má dynamickou IP adresu. Každý jedinečný CMG používá novou dynamickou IP adresu. Přidání dalších virtuálních počítačů na CMG tyto adresy nezvyšuje.  

## <a name="performance-and-scale"></a>Výkon a škálování

Další informace o škále CMG najdete v tématu věnovaném [velikostem a škálováním čísel](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg).

Následující doporučení vám pomohou zlepšit výkon CMG:

- Spojení mezi klientem Configuration Manager a CMGem nezohledňuje oblast. Komunikace klientů je z velké části neovlivněna latencí nebo geografickým oddělením. Pro účely geografické blízkosti není nutné nasazovat víc CMG. Nasaďte CMG v lokalitě nejvyšší úrovně ve vaší hierarchii a přidejte instance pro zvýšení měřítka.

- Pro zajištění vysoké dostupnosti služby vytvořte CMG s alespoň dvěma instancemi CMG a dvěma body připojení CMG pro každý web.  

- Škálujte CMG tak, aby podporoval více klientů přidáním dalších instancí virtuálních počítačů. Nástroj pro vyrovnávání zatížení Azure řídí připojení klientů ke službě.  

- Vytvořte další spojovací body CMG k distribuci zatížení mezi nimi. CMG distribuuje provoz na jeho propojení spojovacími body CMG v kruhovém dotazování.  

- Pokud je CMG s vysokým zatížením s více než podporovaným počtem klientů, stále zpracovává požadavky, ale může dojít ke zpoždění.  

> [!NOTE]
> I když Configuration Manager nemá žádný pevný limit počtu klientů pro bod připojení CMG, má Windows Server výchozí maximální rozsah dynamického portu TCP 16 384. Pokud Configuration Manager lokalita spravuje více než 16 384 klientů s jedním přípojným bodem CMG, je nutné zvýšit limit Windows serveru. Všichni klienti udržují kanál pro oznámení klientů, který obsahuje port otevřený v bodu připojení CMG. Další informace o tom, jak tento limit zvýšit pomocí příkazu netsh, najdete v [článku 929851 podpora Microsoftu](https://support.microsoft.com/help/929851).

## <a name="ports-and-data-flow"></a>Porty a tok dat

Nemusíte otevírat žádné příchozí porty v místní síti. Bod připojení služby a bod připojení CMG zahájí veškerou komunikaci s Azure a CMG. Tyto dvě role systému lokality potřebují vytvořit odchozí připojení ke cloudu Microsoftu. Bod připojení služby nasadí a monitoruje službu v Azure, proto musí být online režim. Bod připojení CMG se připojuje k CMG za účelem správy komunikace mezi CMG a místními rolemi systému lokality.

Následující diagram je základní koncepční datový tok pro CMG:

[![Tok dat CMG](media/cmg-data-flow.png)](media/cmg-data-flow.png#lightbox)

1. Spojovací bod služby se připojuje k Azure přes port HTTPS 443. Ověřuje se pomocí Azure AD nebo certifikátu pro správu Azure. Spojovací bod služby nasadí CMG do Azure. CMG vytvoří cloudovou službu HTTPS pomocí ověřovacího certifikátu serveru.  

2. Bod připojení CMG se připojuje k CMG v Azure prostřednictvím TCP-TLS nebo HTTPS. Obsahuje otevřené připojení a vytváří kanál pro budoucí obousměrnou komunikaci.  

3. Klient se připojí k CMG přes port HTTPS 443. Ověřuje se pomocí služby Azure AD nebo certifikátu pro ověřování klientů.  

    > [!NOTE]
    > Pokud povolíte, aby služba CMG poskytovala obsah nebo používala cloudový distribuční bod, klient se připojí přímo ke službě Azure Blob Storage přes port HTTPS 443. Další informace najdete v tématu [Použití cloudového distribučního bodu](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_dataflow).<!-- SCCMDocs#2332 -->

4. CMG předává komunikaci klienta přes existující připojení k místnímu spojovacímu bodu CMG. Nemusíte otevírat žádné porty brány firewall pro příchozí spojení.  

5. Bod připojení CMG předává komunikaci klienta s místním bodem správy a bodem aktualizace softwaru.  

Další informace o hostování obsahu v Azure najdete v tématu [Použití cloudového distribučního bodu](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_dataflow).

### <a name="required-ports"></a>Požadované porty

V této tabulce jsou uvedené požadované síťové porty a protokoly. *Klient* je zařízení iniciované připojením a vyžaduje odchozí port. *Server* je zařízení, které přijímá připojení, vyžaduje port pro příchozí spojení.

| Klient | Protocol (Protokol) | Port | Server | Description |
|--------|----------|------|--------|-------------|
| Spojovací bod služby | HTTPS | 443 | Azure | Nasazení CMG |
| Bod připojení CMG | TCP-TLS | 10140-10155 | Služba CMG | Upřednostňovaný protokol pro sestavení CMG kanálu <sup> [Poznámka 1](#bkmk_port-note1)</sup> |
| Bod připojení CMG | HTTPS | 443 | Služba CMG | Záložní protokol pro sestavení kanálu CMG jenom na jednu instanci virtuálního počítače <sup> [2. Poznámka 2](#bkmk_port-note2)</sup> |
| Bod připojení CMG | HTTPS | 10124-10139 | Služba CMG | Záložní protokol pro sestavení kanálu CMG do dvou nebo více instancí virtuálních počítačů <sup> [Poznámka 3](#bkmk_port-note3)</sup> |
| Klient | HTTPS | 443 | CMG | Obecná komunikace s klientem |
| Klient | HTTPS | 443 | Blob Storage | Stažení obsahu založeného na cloudu |
| Bod připojení CMG | HTTPS nebo HTTP | 443 nebo 80 | Bod správy | Místní provoz, port závisí na konfiguraci bodu správy. |
| Bod připojení CMG | HTTPS nebo HTTP | 443 nebo 80 | Bod aktualizace softwaru | Místní provoz, port závisí na konfiguraci bodu aktualizace softwaru. |

#### <a name="note-1-cmg-connection-point-tcp-tls-ports"></a><a name="bkmk_port-note1"></a>Poznámka 1: porty připojení CMG spojovacího bodu TCP-TLS

Bod připojení CMG se nejprve pokusí vytvořit dlouhodobé připojení TCP-TLS s každou instancí virtuálního počítače CMG. Připojuje se k první instanci virtuálního počítače na portu 10140. Druhá instance virtuálního počítače používá port 10141 až šestnáct na portu 10155. Připojení TCP-TLS to vykoná nejlépe, ale nepodporuje internetový proxy server. Pokud spojovací bod CMG se nemůže připojit prostřednictvím protokolu TCP-TLS, pak se vrátí k protokolu HTTPS<sup>[Note 2](#bkmk_port-note2)</sup>.

#### <a name="note-2-cmg-connection-point-https-ports-for-one-vm"></a><a name="bkmk_port-note2"></a>Poznámka 2: porty CMG spojovacího bodu připojení pro jeden virtuální počítač

Pokud spojovací bod CMG se nemůže připojit k CMG prostřednictvím TCP-TLS<sup>[Note 1](#bkmk_port-note1)</sup>, připojí se k nástroji Azure Network Load Balancer přes HTTPS 443 pouze pro jednu instanci virtuálního počítače.  

#### <a name="note-3-cmg-connection-point-https-ports-for-two-or-more-vms"></a><a name="bkmk_port-note3"></a>Poznámka 3: porty HTTPS bodu připojení CMG pro dva nebo více virtuálních počítačů

Pokud jsou k dispozici dvě nebo více instancí virtuálních počítačů, spojovací bod CMG používá k první instanci virtuálního počítače protokol HTTPS 10124, nikoli HTTPS 443. Připojí se k druhé instanci virtuálního počítače na HTTPS 10125, až šestnáctě na portu HTTPS 10139.

### <a name="internet-access-requirements"></a>Požadavky na přístup k internetu

Pokud vaše organizace omezuje síťovou komunikaci s Internetem pomocí brány firewall nebo proxy zařízení, je nutné povolit spojovacímu bodu CMG a spojovacímu bodu služby přístup k internetovým koncovým bodům.

Další informace najdete v tématu [požadavky na přístup k Internetu](../../../plan-design/network/internet-endpoints.md#bkmk_cloud).

## <a name="next-steps"></a>Další kroky

- [Certifikáty brány pro správu cloudu](certificates-for-cloud-management-gateway.md)
- [Zabezpečení a ochrana brány pro správu cloudu](security-and-privacy-for-cloud-management-gateway.md)
- [Velikost brány pro správu cloudu a čísla škálování](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)
- [Nejčastější dotazy týkající se brány pro správu cloudu](cloud-management-gateway-faq.md)
- [Instalace brány pro správu cloudu](setup-cloud-management-gateway.md)
