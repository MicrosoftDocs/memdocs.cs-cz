---
title: Použití cloudových služeb
titleSuffix: Configuration Manager
description: Zřízení cloudových prostředků pro Configuration Manager doplnění místní infrastruktury.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 24fca61e-9cdb-447a-ad7a-f4d2e4fd6704
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e5ea198f944cf44909e54e123889a3f0f29b1db5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699105"
---
# <a name="use-cloud-services-with-configuration-manager"></a>Použití cloudových služeb s nástrojem Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager podporuje několik cloudových možností. Ty můžou doplňovat vaši místní infrastrukturu a můžou vám pomáhat řešit obchodní problémy, jako jsou:  

-   Jak spravovat BYOD (pomocí Intune pro správu mobilních zařízení).  

-   Postup poskytování prostředků obsahu pro izolované klienty nebo prostředky v intranetu, mimo vaši podnikovou bránu firewall (pomocí cloudových distribučních bodů).  

-   Postup horizontálního navýšení kapacity infrastruktury, když není dostupný fyzický hardware, nebo není logicky umístěný tak, aby podporovaly vaše potřeby (pomocí Microsoft Azure virtuálních počítačů).  

I když zřizování cloudových prostředků ještě není potřeba, před nasazením Configuration Manager, může být výhodné tyto možnosti pochopit před tím, než je v plánu návrhu hierarchie příliš daleko. Použití prostředků cloudu vám může ušetřit peníze i čas a zároveň řešit obchodní problémy, které místní infrastruktura nedokáže.  

## <a name="cloud-based-resources-you-can-use-with-configuration-manager"></a>Cloudové prostředky, které můžete používat s Configuration Manager  
 Protože každá možnost má jiné požadavky, prozkoumejte každou z nich podrobněji, abyste porozuměli jedinečným požadavkům, omezením a případným dalším poplatkům za použití.  

-   Informace o cloudových distribučních bodech najdete v tématu [instalace cloudových distribučních bodů](../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md).

-   Další informace o Azure najdete v tématu [co je Azure?](https://azure.microsoft.com/overview/what-is-azure/)

### <a name="azure-virtual-machines-for-cloud-based-infrastructure"></a>Virtuální počítače Azure (pro cloudovou infrastrukturu)  
 Configuration Manager podporuje používání počítačů, které běží na virtuálních počítačích v Azure, stejně jako místní spouštění ve vaší fyzické podnikové síti. Virtuální počítače Azure můžete použít v následujících scénářích:  

-   **Scénář 1:** Na virtuálním počítači můžete spustit Configuration Manager a použít ho ke správě klientů nainstalovaných v jiných virtuálních počítačích.  

-   **Scénář 2:** Na virtuálním počítači můžete spustit Configuration Manager a použít ho ke správě klientů, kteří neběží v Azure.  

-   **Scénář 3:** Ve virtuálních počítačích můžete spouštět různé Configuration Manager role systému lokality a přitom spouštět další role ve fyzické podnikové síti (s odpovídajícím připojením k síti pro komunikaci).  

Stejné požadavky na sítě, operační systémy a požadavky na hardware, které se vztahují k instalaci Configuration Manager ve vaší fyzické podnikové síti, se vztahují také na instalaci Configuration Manager v Azure.  

K používání virtuálních počítačů Azure se vyžaduje předplatné Azure. Poplatky se účtují na základě počtu virtuálních počítačů, které používáte, jejich konfigurace a využívání cloudových prostředků.  

Configuration Manager webů a klientů, které běží na virtuálních počítačích Azure, se navíc vztahují stejné licenční požadavky jako na místní instalace.  

### <a name="azure-services-for-cloud-based-distribution-points"></a>Služby Azure (pro cloudové distribuční body)  
 Službu Azure můžete použít k hostování Configuration Manager distribučního bodu, který se nazývá cloudový distribuční bod. [Cloudový distribuční bod s Configuration Manager můžete použít spolu s](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) místními distribučními body a distribučními body nasazenými na virtuálních počítačích Azure.  

 Tento proces se liší od používání virtuálního počítače Azure, na kterém je nasazená role systému lokality. Cloudové distribuční body:  

-   Spustit jako službu v Azure, ne na virtuálním počítači.  

-   Automatické škálování tak, aby splňovalo zvýšené požadavky na obsah od klientů.  

-   Podpora klientů na internetu a intranetu.  

K hostování distribučních bodů je nutné předplatné Azure. Poplatky se účtují na základě množství dat, která se přenášejí do služby a ze služby.  

### <a name="additional-configuration-manager-capabilities"></a>Další možnosti nástroje Configuration Manager  
 Některé funkce Configuration Manager se můžou připojit ke cloudovým službám, jako jsou:  

-   Windows Server Update Services (WSUS).  

-   Cloud služby Configuration Manager pro stažení aktualizací pro Configuration Manager.  

Tyto další funkce nevyžadují, abyste měli předplatné Azure. Nemusíte nastavovat konkrétní připojení, certifikáty nebo služby v cloudu. Místo toho je automaticky spravuje Configuration Manager za vás. Stačí, abyste zajistili, že příslušné systémy lokalit a zařízení mají přístup k internetovým adresám URL.  

##  <a name="security-for-cloud-based-services"></a><a name="BKMK_CloudSec"></a> Zabezpečení cloudových služeb  
 Configuration Manager používá k zřizování a přístupu k vašemu obsahu v Azure a ke správě služeb, které používáte, certifikáty. Configuration Manager šifruje data, která ukládáte v Azure, ale nezavádí další zabezpečení nebo ovládací prvky dat nad rámec těch, které poskytuje Azure.  

 Další informace najdete v podrobnostech o různých scénářích cloudových prostředků. Seznamte se také s [úvodem do zabezpečení Azure](/azure/security/fundamentals/overview).