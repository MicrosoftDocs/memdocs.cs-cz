---
title: Velikost a škálování
titleSuffix: Configuration Manager
description: Určete počet rolí systému lokality a lokalit, které budete potřebovat pro podporu zařízení ve vašem prostředí.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0d8057d61ebaaa8a545d21b31331faec1c04884e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126694"
---
# <a name="size-and-scale-numbers-for-configuration-manager"></a>Dimenzování a škálování nástroje Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Každé nasazení Configuration Manager má maximální počet webů, rolí systému lokality a zařízení, která může podporovat. Tato čísla se liší v závislosti na struktuře hierarchie, typu a počtu lokalit, které používáte, a rolím systému lokality, které nasadíte. Informace v tomto článku vám pomůžou určit počet rolí systému lokality a lokalit, které potřebujete k podpoře zařízení, která chcete spravovat.

Další informace najdete v následujících článcích:

- [Doporučený hardware](recommended-hardware.md)
- [Podporované operační systémy pro servery systému lokality](supported-operating-systems-for-site-system-servers.md)  
- [Podporované operační systémy pro klienty a zařízení](supported-operating-systems-for-clients-and-devices.md)
- [Požadavky na lokality a systémy lokalit](site-and-site-system-prerequisites.md)

Tato čísla podpory jsou založená na použití doporučeného hardwaru pro Configuration Manager. Jsou také založeny na výchozích nastaveních pro všechny dostupné Configuration Manager funkce. Pokud nepoužíváte doporučený hardware nebo používáte více agresivních vlastních nastavení, výkon systémů lokality může být degradován. Systémy lokality nemusí splňovat uvedené úrovně podpory. (Příklad účinnějšího nastavení klienta je provoz hardwaru nebo softwaru častěji než výchozí hodnota každých 7 dní.)

## <a name="site-types"></a><a name="bkmk_SiteSystemScale"></a>Typy lokalit  

### <a name="central-administration-site"></a>Lokalita centrální správy  

- Lokalita centrální správy podporuje až 25 podřízených primárních lokalit.  

### <a name="primary-site"></a>Primární lokalita  

- Každá primární lokalita podporuje až 250 sekundárních lokalit.  

- Počet sekundárních lokalit na primární lokalitu vychází z nepřetržitě propojených a spolehlivých připojení WAN (Wide Area Network). Pro umístění, která mají méně než 500 klientů, zvažte místo sekundární lokality distribuční bod.  

  Informace o počtu klientů a zařízení, které může primární lokalita podporovat, najdete v tématu [čísla klientů pro lokality a hierarchie](#bkmk_clientnumbers).  

### <a name="secondary-site"></a>Sekundární lokalita  

- Sekundární lokality nepodporují podřízené lokality.  

## <a name="site-system-roles"></a><a name="bkmk_roles"></a>Role systému lokality

### <a name="application-catalog-web-service-point"></a>Bod webové služby Katalog aplikací  

> [!Important]
> Uživatelské prostředí programu Silverlight v katalogu aplikací není v aktuální větvi verze 1806 podporováno. Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací. Podpora končí pro role katalogu aplikací s verzí 1910.  
>
> Další informace najdete v následujících článcích:
>
> - [Konfigurace centra softwaru](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Odebrané a zastaralé funkce](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- V primárních lokalitách můžete nainstalovat více instancí bodu webové služby katalogu aplikací.  

### <a name="application-catalog-website-point"></a>Bod webu Katalog aplikací  

> [!Important]
> Uživatelské prostředí programu Silverlight v katalogu aplikací není v aktuální větvi verze 1806 podporováno. Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací. Podpora končí pro role katalogu aplikací s verzí 1910.  
>
> Další informace najdete v následujících článcích:
>
> - [Konfigurace centra softwaru](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Odebrané a zastaralé funkce](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- V primárních lokalitách můžete nainstalovat více instancí bodu webu Katalog aplikací.  

### <a name="cloud-management-gateway"></a><a name="bkmk_cmg"></a>Brána pro správu cloudu

- V primárních lokalitách nebo v lokalitě centrální správy můžete nainstalovat více instancí brány pro správu cloudu (CMG).  

    > [!Tip]  
    > V hierarchii vytvořte CMG v lokalitě centrální správy.  

  - Jedna CMG podporuje jednu až 16 instancí virtuálních počítačů v cloudové službě Azure.  

  - Každá instance virtuálního počítače CMG podporuje 6 000 současných připojení klientů. Pokud je CMG při vysokém zatížení v důsledku více než podporovaného počtu klientů, stále zpracovává požadavky, ale může dojít ke zpoždění.  

Další informace najdete v tématu CMG [Performance and Scale](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale) .

### <a name="cloud-management-gateway-connection-point"></a>Bod připojení brány pro správu cloudu

- V primárních lokalitách můžete nainstalovat více instancí spojovacího bodu CMG.  

- Jeden bod připojení CMG může podporovat CMG s až čtyřmi instancemi virtuálních počítačů. Pokud má CMG více než čtyři instance virtuálních počítačů, přidejte druhý spojovací bod CMG pro vyrovnávání zatížení. CMG s 16 instancemi virtuálních počítačů by se měly propojit se čtyřmi spojovacími body CMG.

Další informace najdete v tématu CMG [Performance and Scale](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale) .

> [!NOTE]
> Pokud zvažujete požadavky na hardware pro bod připojení CMG, přečtěte si téma [doporučený hardware pro vzdálené servery systému lokality](recommended-hardware.md#bkmk_RemoteSiteSystem).<!-- SCCMDocs#2276 -->

### <a name="distribution-point"></a>Distribuční bod  

- Distribuční body na lokalitu:  

  - Každá primární a sekundární lokalita podporuje až 250 distribučních bodů.  

  - Každá primární a sekundární lokalita podporuje až 2000 dalších distribučních bodů nakonfigurovaných jako distribuční body pro vyžádání obsahu. Jedna primární lokalita **například**podporuje 2250 distribučních bodů, pokud je 2000 těchto distribučních bodů nakonfigurován jako distribuční body pro vyžádání obsahu.  

  - Každý distribuční bod podporuje připojení od až 4 000 klientů.  

  - Distribuční bod pro vyžádání obsahu funguje jako klient, když přistupuje k obsahu ze zdrojového distribučního bodu.  

- Každá primární lokalita podporuje součet až 5 000 distribučních bodů. Tato celková hodnota zahrnuje všechny distribuční body v primární lokalitě a všechny distribuční body, které patří do podřízených sekundárních lokalit primární lokality.  

- Každý distribuční bod podporuje kombinovaný součet až 10 000 balíčků a aplikací.  

> [!WARNING]  
> Skutečný počet klientů, které může podporovat jeden distribuční bod, závisí na rychlosti sítě a konfiguraci hardwaru serveru.  
>
> Počet distribučních bodů pro vyžádání obsahu, které může podporovat jeden zdrojový distribuční bod, závisí podobně na rychlosti sítě a konfiguraci hardwaru zdrojového distribučního bodu. Ale toto číslo je ovlivněno také množstvím obsahu, který jste nasadili. To proto, že na rozdíl od klientů, kteří obvykle přistupují k obsahu v různých časech během nasazení, všechny požadavky na distribuční body pro vyžádání obsahu jsou ve stejnou dobu. Distribuční body pro vyžádání obsahu mohou vyžadovat veškerý dostupný obsah, nikoli pouze obsah, který je pro ně použitelný. Při vysokém zatížení na zdrojovém distribučním bodu může dojít k neočekávaným zpožděním při distribuci obsahu do cílových distribučních bodů.  

### <a name="fallback-status-point"></a>Bod záložního stavu  

- Každý bod stavu pro použití náhradní lokality může podporovat až 100 000 klientů.  

### <a name="management-point"></a>Bod správy  

- Každá primární lokalita podporuje až 15 bodů správy.  

    > [!TIP]  
    > Neinstalujte body správy na serverech, které jsou v případě pomalého připojení ze serveru primární lokality nebo serveru databáze lokality.  

- Každá sekundární lokalita podporuje jeden bod správy, který musí být nainstalován na serveru sekundární lokality.  

Informace o počtu klientů a zařízení, které může bod správy podporovat, najdete v části [body správy](#bkmk_mp) .  

> [!NOTE]
> Pokud povolíte, aby bod správy podporoval [bránu pro správu cloudu](../../clients/manage/cmg/plan-cloud-management-gateway.md), klientské požadavky na internetové služby se budou na normální úrovni. Pokyny pro změnu velikosti bodu správy se nemění bez ohledu na to, jestli místní nebo internetové klienty IT služby.

### <a name="software-update-point"></a>Bod aktualizace softwaru  

Jako základ použijte následující doporučení. Tato základní hodnota vám pomůže určit informace pro plánování kapacity aktualizací softwaru, které je vhodné pro vaši organizaci. Skutečné požadavky na kapacitu se mohou lišit od doporučení uvedených v tomto článku v závislosti na následujících kritériích:

- Vaše konkrétní síťové prostředí
- Hardware, který slouží k hostování systému lokality bodu aktualizace softwaru
- Počet spravovaných klientů
- Ostatní role systému lokality nainstalované na serveru  

> [!NOTE]
> Pokud povolíte, aby bod aktualizace softwaru podporoval [bránu pro správu cloudu](../../clients/manage/cmg/plan-cloud-management-gateway.md), klientské požadavky na internetové služby jsou na normální. Pokyny pro změnu velikosti bodu aktualizace softwaru se nemění bez ohledu na to, jestli místní nebo internetové klienty IT služby.

#### <a name="capacity-planning-for-the-software-update-point"></a><a name="BKMK_SUMCapacity"></a> Plánování kapacity pro bod aktualizace softwaru  

Počet podporovaných klientů závisí na verzi služby Windows Server Update Services (WSUS), která běží v bodě aktualizace softwaru. Záleží taky na tom, jestli role systému lokality bodu aktualizace softwaru existuje s jinou rolí systému lokality:  

- Bod aktualizace softwaru může podporovat až 25 000 klientů, pokud služba WSUS běží na serveru bodu aktualizace softwaru a bod aktualizace softwaru existuje s jinou rolí systému lokality.  

- Bod aktualizace softwaru může podporovat až 150 000 klientů, pokud vzdálený server splňuje požadavky služby WSUS, služba WSUS se používá s Configuration Manager a Vy nakonfigurujete následující nastavení:

  Fondy aplikací IIS:

  - Zvyšte hodnotu nastavení WsusPool Queue Length na 2000
  - Zvyšte limit soukromé paměti nastavení WsusPool nebo nastavte na 0 (neomezeno). Pokud je například výchozí omezení 1 843 200 KB, zvyšte ho na 7 372 800. Další informace najdete v [příspěvku blogu týmu podpory Configuration Manager](https://www.phoenixtekk.com/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors/).  

    Další informace o požadavcích na hardware pro bod aktualizace softwaru najdete v tématu [doporučený hardware pro systémy lokality](recommended-hardware.md#bkmk_ScaleSieSystems).  

#### <a name="capacity-planning-for-software-updates-objects"></a><a name="bkmk_sum-capacity-obj"></a>Plánování kapacity pro objekty aktualizací softwaru  

K plánování objektů aktualizací softwaru použijte následující informace o kapacitě:  

- **Omezení 1000 aktualizací softwaru v nasazení** – omezte počet aktualizací softwaru na 1000 pro každé nasazení aktualizace softwaru. Když vytváříte pravidlo automatického nasazení (ADR), zadejte kritéria, která omezují počet aktualizací softwaru. Pokud zadaná kritéria vrátí více než 1000 aktualizací softwaru, pravidla automatického nasazení se nezdařila. Pomocí uzlu **pravidla automatického nasazení** v konzole Configuration Manager ověřte stav služby ADR. Když ručně nasadíte aktualizace softwaru, nevybírejte více než 1000 aktualizací k nasazení.  

  Také omezte počet aktualizací softwaru na 1000 v směrném plánu konfigurace. Další informace najdete v tématu [Vytvoření standardních hodnot konfigurace](../../../compliance/deploy-use/create-configuration-baselines.md).

- **Omezení 580 oborů zabezpečení pro pravidla automatického nasazení** -<!--ado 4962928-->
Omezte počet oborů zabezpečení pro pravidla automatického nasazení (pravidla automatického nasazení) na hodnotu menší než 580. Při vytváření pravidla automatického nasazení se přidají automaticky obory zabezpečení, které k nim mají přístup. Pokud je nastavené více než 580 oborů zabezpečení, pravidla automatického nasazení se nezdaří a v protokolu RuleEngine. log se zaznamená chyba.

### <a name="sms-provider"></a>poskytovatele serveru SMS

<!-- SCCMDocs#1958 -->

Každá instance poskytovatele služby SMS podporuje současná připojení z více požadavků. Jediným omezením u těchto připojení jsou počet připojení serverů, která jsou dostupná pro Windows, a dostupné prostředky na serveru pro obsluhu požadavků na připojení.

Další informace najdete v tématu [plánování poskytovatele serveru SMS](../hierarchy/plan-for-the-sms-provider.md).

Služba správy je REST API na všech instancích poskytovatele služby SMS. Podporuje až 5 000 požadavků za sekundu a 200 požadavků na IP adresu klienta.

## <a name="client-numbers-for-sites-and-hierarchies"></a><a name="bkmk_clientnumbers"></a>Čísla klientů pro lokality a hierarchie

Pomocí následujících informací určete, kolik klientů a které typy klientů můžete podporovat v lokalitě nebo v hierarchii.  

### <a name="hierarchy-with-a-central-administration-site"></a><a name="bkmk_cas"></a>Hierarchie s lokalitou centrální správy

Lokalita centrální správy podporuje celkový počet zařízení, která zahrnují počet zařízení uvedených pro následující tři skupiny:  

- 700 000 počítačů se systémem Windows. Viz také podpora [integrovaných zařízení](#embedded).

- 25 000 zařízení se systémem Mac a systém Windows CE 7,0  

- 100 000 zařízení, která spravujete pomocí místní správy mobilních zařízení (MDM)

V hierarchii můžete například podporovat 700 000 stolních počítačů, až 25 000 Mac a systém Windows CE 7,0 zařízení a až 100 000 zařízení spravovaná místní správou MDM. Tato hierarchie podporuje celkem 825 000 zařízení.

> [!IMPORTANT]  
> V hierarchii, kde lokalita centrální správy používá edici Standard SQL Server, podporuje tato hierarchie maximálně 50 000 počítačů a zařízení. Aby bylo možné podporovat více než 50 000 počítačů a zařízení, je nutné použít SQL Server edice Enterprise. Tento požadavek se vztahuje pouze na lokalitu centrální správy. Neplatí pro samostatnou primární lokalitu nebo podřízenou primární lokalitu. Edice SQL Server, kterou používáte pro primární lokalitu, neomezuje svoji kapacitu na podporu zadaného počtu klientů.

Edice SQL Server používaná v samostatné primární lokalitě neomezuje kapacitu tohoto webu na podporu až po stanovený počet klientů.  

### <a name="child-primary-site"></a><a name="bkmk_chipri"></a>Podřízená primární lokalita

Každá podřízená primární lokalita v hierarchii s lokalitou centrální správy podporuje následující počet klientů:  

- 150 000 Celkový počet klientů a zařízení, která nejsou omezená na konkrétní skupinu nebo typ, pokud podpora nepřekračuje počet podporovaný v hierarchii. Viz také podpora [integrovaných zařízení](#embedded).

Například primární lokalita podporuje zařízení se systémem 25 000 Mac a systém Windows CE 7,0. Toto číslo je omezení pro hierarchii. Tato primární lokalita pak může podporovat další 125 000 stolní počítače. Celkový počet podporovaných zařízení pro podřízenou primární lokalitu je maximální podporovaný limit 150 000.

### <a name="stand-alone-primary-site"></a><a name="bkmk_pri"></a>Samostatná primární lokalita

Samostatná primární lokalita podporuje následující počet zařízení:  

- 175 000 Celkový počet klientů a zařízení, které nepřekročí:  

  - 150 000 stolních počítačů (počítače se systémem Windows, Linux a UNIX). Viz také podpora [integrovaných zařízení](#embedded).

  - 25 000 zařízení se systémem Mac a systém Windows CE 7,0

  - 50 000 zařízení, která spravujete pomocí místní správy mobilních zařízení (MDM)  

Například samostatná primární lokalita, která podporuje 150 000 stolních počítačů a 10 000 Mac, může podporovat jenom další 15 000 mobilní zařízení, která spravuje místní MDM.

### <a name="primary-sites-and-windows-embedded-devices"></a><a name="embedded"></a>Primární lokality a zařízení se systémem Windows Embedded

Primární lokality podporují zařízení se systémem Windows Embedded, která mají povolený filtr zápisu na základě souborů (FBWF). Když vložená zařízení nemají povolené filtry zápisu, může primární lokalita podporovat několik integrovaných zařízení až do povoleného počtu zařízení pro tuto lokalitu. Pokud mají vložená zařízení povolené FBWF nebo sjednocené filtry zápisu (UWF), může primární lokalita podporovat maximálně 10 000 zařízení se systémem Windows Embedded. Tato zařízení musí být nakonfigurovaná s výjimkami uvedenými v důležité poznámce, které najdete v části [Plánování nasazení klienta na zařízení se systémem Windows Embedded](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md). Primární lokalita podporuje jenom 3 000 zařízení se systémem Windows Embedded, která mají povolený EWF a která nejsou pro tyto výjimky nakonfigurované.

### <a name="secondary-sites"></a><a name="bkmk_sec"></a>Sekundární lokality

Sekundární lokality podporují následující počet zařízení:  

- 15 000 stolních počítačů (počítače se systémem Windows, Linux a UNIX)  

### <a name="management-points"></a><a name="bkmk_mp"></a>Body správy

Každý bod správy může podporovat následující počet zařízení:  

- 25 000 Celkový počet klientů a zařízení, které nepřekročí:  

  - 25 000 stolních počítačů (počítače se systémem Windows, Linux a UNIX)  

  - Jedna z následujících (nikoli obě):  

    - 10 000 zařízení, která jsou spravovaná pomocí místní správy mobilních zařízení (MDM)  

    - 10 000 zařízení, na kterých běží klienti Mac a systém Windows CE 7,0
