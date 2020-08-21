---
title: Podpora funkcí Windows
titleSuffix: Configuration Manager
description: Seznamte se s funkcemi pro Windows a sítě, které Configuration Manager podporuje.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4f9266668a488b6331857bf860d874a48161fcd0
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700210"
---
# <a name="support-for-windows-features-and-networks-in-configuration-manager"></a>Podpora funkcí a sítí Windows v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek popisuje podporu Configuration Manager běžných funkcí pro Windows a sítě.  

## <a name="branchcache"></a><a name="bkmk_branchcache"></a> Služba  

Použijte Windows BranchCache s Configuration Manager, když ho povolíte v distribučních bodech, a nakonfigurujte klienty tak, aby ho používali v režimu distribuované mezipaměti.

Nakonfigurujte nastavení služby BranchCache pro typ nasazení pro aplikace, nasazení pro balíček a pro pořadí úkolů. Počínaje verzí 1802 je ve výchozím nastavení povolená služba BranchCache.

Když se splní požadavky na BranchCache, tato funkce umožní klientům ve vzdálených umístěních získat obsah od místních klientů, kteří mají aktuální mezipaměť obsahu.  

Pokud například první klient s povolenou službou BranchCache požaduje obsah z distribučního bodu, který je nakonfigurovaný jako server BranchCache, klient stáhne a uloží obsah do mezipaměti. Tento obsah je poté zpřístupněn klientům ve stejné podsíti, která požadovala tento obsah.

Tito klienti také obsah uloží do mezipaměti. Ostatní klienti ve stejné podsíti nemusí stahovat obsah z distribučního bodu. Obsah je distribuován mezi několik klientů pro budoucí přenosy.  

### <a name="requirements-to-support-branchcache-with-configuration-manager"></a>Požadavky na podporu služby BranchCache pomocí Configuration Manager

#### <a name="configure-distribution-points"></a>Konfigurace distribučních bodů

Přidejte funkci **Windows BranchCache** na server systému lokality, který je nakonfigurovaný jako distribuční bod.

- Distribuční body na serverech, které jsou nakonfigurovány pro podporu služby BranchCache, nevyžadují žádnou další konfiguraci.
- Nelze přidat službu Windows BranchCache do cloudového distribučního bodu. Cloudové distribuční body podporují stahování obsahu klienty konfigurovanými pro službu Windows BranchCache.  

#### <a name="configure-clients"></a>Konfigurace klientů

- Klienti, kteří můžou podporovat BranchCache, musí být nakonfigurované pro režim distribuované mezipaměti BranchCache.  
- Aby bylo možné podporovat službu BranchCache, musí být u nastavení klienta služby BITS povolena nastavení operačního systému.  

Informace najdete v tématu [Konfigurace klientů pro službu BranchCache](/windows/deployment/update/waas-branchcache#configure-clients-for-branchcache) v dokumentaci k systému Windows.

Configuration Manager všechny podporované verze Windows podporují službu BranchCache ve výchozím nastavení.

Další informace najdete v tématu Služba [BranchCache pro systém Windows](/windows-server/networking/branchcache/branchcache) v dokumentaci k Windows serveru.  

## <a name="computers-in-workgroups"></a><a name="bkmk_Workgroups"></a> Počítače v pracovních skupinách  

Configuration Manager poskytuje podporu pro klienty v pracovních skupinách.  

- Configuration Manager podporuje přesun klienta z pracovní skupiny do domény nebo z domény do pracovní skupiny. Další informace najdete v tématu [instalace klientů Configuration Manager do počítačů v pracovní skupině](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup).  

> [!NOTE]
> I když jsou klienti v pracovních skupinách podporováni, všechny systémy lokalit musí být členy podporované domény služby Active Directory.  

## <a name="data-deduplication"></a><a name="bkmmk_datadedup"></a> Odstranění duplicitních dat

Configuration Manager podporuje použití odstranění duplicitních dat s distribučními body v systému Windows Server 2012 nebo novějším.

> [!IMPORTANT]  
> Svazek, který je hostitelem zdrojových souborů balíčku, nelze označit pro odstranění duplicitních dat. Toto omezení je způsobeno tím, že odstranění duplicitních dat používá spojovací body. Configuration Manager nepodporuje použití umístění zdroje obsahu se soubory uloženými v bodech rozboru.  

Další informace najdete v následujících příspěvcích:

- [Configuration Manager distribuční body a odstranění duplicitních dat Windows serveru 2012](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configuration-manager-distribution-points-and-windows-server/ba-p/273385) na blogu týmu Configuration Manager

- [Přehled odstranění duplicitních dat](/windows-server/storage/data-deduplication/overview) v dokumentaci k Windows serveru

## <a name="directaccess"></a><a name="bkmk_DA"></a> DirectAccess  

Configuration Manager podporuje funkci DirectAccess pro komunikaci mezi klienty a systémy serveru lokality.  

- Po splnění všech požadavků pro technologii DirectAccess umožňuje Configuration Manager klientům na internetu komunikovat s přiřazenou lokalitou, jako kdyby byla na intranetu.  

- U akcí iniciované serverem, jako je třeba vzdálené řízení a klientská nabízená instalace, musí iniciující počítač používat protokol IPv6. Tento protokol musí být podporovaný na všech používaných síťových zařízeních.  

Configuration Manager nepodporuje u technologie DirectAccess následující funkce:  

- Nasazení operačního systému

- Komunikace mezi Configuration Manager lokalitami  

- Komunikace mezi Configuration Managermi servery systému lokality v rámci lokality  

## <a name="dual-boot-computers"></a><a name="bkmk_dualboot"></a> Počítače s více operačními systémy  

Configuration Manager nemůže spravovat více než jeden operační systém v jednom počítači. Pokud je v počítači k dispozici více než jeden operační systém, upravte metody zjišťování lokality a instalace klienta, aby se zajistilo, že je klient Configuration Manager nainstalován pouze v operačním systému, který má být spravován.  

## <a name="ipv6"></a><a name="bkmk_IPv6"></a> Protokolů  

Kromě Internet Protocol verze 4 (IPv4) Configuration Manager podporuje Internet Protocol verze 6 (IPv6), s následujícími výjimkami:  

|Funkce| Výjimka z podpory protokolu IPv6|  
|--------------|-------------------------------|  
|Cloudové distribuční body|K podpoře Microsoft Azure a cloudových distribučních bodů je nutný protokol IPv4.|  
|Brána pro správu cloudu|K podpoře Microsoft Azure a brány pro správu cloudu je vyžadován protokol IPv4.|  
|Mobilní zařízení zaregistrovaná službou Microsoft Intune a konektorem Microsoft Service Connector|K podpoře mobilních zařízení zaregistrovaných nástrojem Microsoft Intune a konektorem Microsoft Service Connector je vyžadován protokol IPv4.|  
|Zjištění sítě|Ke konfiguraci serveru DHCP pro hledání v rámci zjišťování sítě je nutný protokol IPv4.|  
|Nasazení operačního systému|Ve verzi 1802 a starší se k podpoře nasazení operačního systému vyžaduje protokol IPv4.  </br> </br> Počínaje verzí 1806 povolte respondér technologie PXE v distribučním bodě bez služby pro nasazení systému Windows. Tato nová služba respondérů PXE podporuje protokol IPv6. Další aspekty funkce nasazení operačního systému, jako je například zachytávání nebo nastavení statických IP adres během pořadí úkolů, budou vyžadovat protokol IPv4. |  
|Komunikace s proxy probuzením|K podpoře klientských balíčků proxy probuzení je nutný protokol IPv4.|  
|Windows CE|K podpoře Configuration Manager klienta na systém Windows CE zařízeních je vyžadován protokol IPv4.|  

## <a name="network-address-translation"></a><a name="bkmk_NAT"></a> Překlad síťových adres  

Překlad síťových adres (NAT) není v Configuration Manager podporován, pokud lokalita nepodporuje klienty, kteří jsou na internetu, a klient zjistí, že je připojen k Internetu. Další informace o internetové správě klientů najdete v tématu [Plánování správy internetových klientů](../../clients/manage/plan-internet-based-client-management.md).  

## <a name="specialized-storage-technology"></a><a name="bkmk_storage"></a> Specializovaná technologie úložiště  

Configuration Manager funguje s veškerým hardwarem, který je v seznamu kompatibilního hardwaru systému Windows certifikovaný pro verzi operačního systému, na kterém je nainstalovaná součást Configuration Manager.

Role serveru lokality vyžadují systém souborů NTFS, aby Configuration Manager mohl nastavit oprávnění k adresářům a souborům. Configuration Manager předpokládá, že má kompletní vlastnictví logické jednotky. Systémy lokality, které běží na různých počítačích, nemůžou sdílet logický oddíl na jakékoli technologii úložiště. Každý počítač ale může v jednom fyzickém oddílu sdíleného paměťového zařízení používat samostatnou logickou oblast.  

### <a name="support-considerations"></a>Požadavky na podporu

- **Síť SAN (Storage Area**Network): síť SAN (Storage Area Network) je podporovaná, když se k svazku hostovanému v síti SAN připojí podporovaný Server s Windows.  

- **Úložiště jedné instance**: Configuration Manager nepodporuje konfiguraci balíčku distribučního bodu a složek podpisů ve svazku s povolenou funkcí SIS (Single Instance Storage).  

     Kromě toho není podpora mezipaměti klienta Configuration Manager podporována na svazku s povolenou funkcí SIS.  

- **Vyměnitelná disková jednotka**: Configuration Manager nepodporuje instalaci Configuration Manager systémů lokality nebo klientů na vyměnitelnou diskovou jednotku.