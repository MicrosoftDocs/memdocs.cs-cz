---
title: Co je Configuration Manager?
titleSuffix: Configuration Manager
description: Seznamte se se základy služby Microsoft Endpoint Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 78b9175c10d4389623bfa08ac7895df200944a13
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722729"
---
# <a name="what-is-configuration-manager"></a>Co je Configuration Manager?

*Platí pro: Configuration Manager (Current Branch)*

Počínaje verzí 1910 je teď Configuration Manager součástí Microsoft Endpoint Manageru.

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Endpoint Manager je integrované řešení pro správu všech vašich zařízení. Společnost Microsoft spolupracuje Configuration Manager a Intune, a to bez složité migrace a s zjednodušenou správou licencí. Nadále Využijte své stávající investice Configuration Manager a využijte výkon cloudu Microsoftu podle vlastního tempa.

Následující řešení pro správu Microsoft jsou teď součástí značky **Microsoft Endpoint Manageru** :

- [Configuration Manager](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [Desktop Analytics](../../desktop-analytics/overview.md)
- [Autopilot](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)
- Další funkce v [konzole správce správy zařízení](https://go.microsoft.com/fwlink/?linkid=2109094)

Další informace najdete v tématu [Microsoft Endpoint Configuration Manager – Nejčastější dotazy](microsoft-endpoint-manager-faq.md).

## <a name="introduction"></a>Úvod

Configuration Manager vám pomůžou s následujícími činnostmi správy systému:

- Zvýšení produktivity a efektivity IT tím, že se omezí ruční úlohy a umožní vám soustředit se na projekty s vysokými hodnotami.  
- Maximalizujte investice na hardware a software.  
- Poskytování správného softwaru ve správný čas díky zvýšení produktivity uživatelů.  

Configuration Manager vám pomůže doručovat efektivnější IT služby tím, že umožňují:

- Zabezpečené a škálovatelné nasazení aplikací, aktualizací softwaru a operačních systémů.
- Akce v reálném čase na spravovaných zařízeních.
- Cloudové analýzy a správa pro místní a Internetová zařízení.
- Správa nastavení dodržování předpisů.  
- Komplexní správa serverů, stolních počítačů a přenosných počítačů.

Configuration Manager rozšiřuje a funguje společně s mnoha technologiemi a řešeními Microsoftu. Například Configuration Manager integrace s:  

- Microsoft Intune pro souběžnou správu široké škály platforem mobilních zařízení
- Microsoft Azure hostování cloudových služeb za účelem rozšiřování služeb správy
- Služba WSUS (Windows Server Update Services) pro správu aktualizací softwaru
- Certifikační služba
- Exchange Server a Exchange Online
- Zásady skupiny
- DNS
- Sada Windows Automated Deployment Kit (Windows ADK) a Nástroj pro migraci uživatelských souborů a nastavení (USMT)
- Služba pro nasazení systému Windows (WDS)
- Funkce Vzdálená plocha a Vzdálená pomoc

Configuration Manager také používá:  

- Active Directory Domain Services a Azure Active Directory pro zabezpečení, umístění služeb, konfiguraci a zjišťování uživatelů a zařízení, která chcete spravovat.  
- Microsoft SQL Server jako distribuovaná databáze správy změn a integruje se se službou SQL Server Reporting Services (SSRS) k vytváření sestav pro monitorování a sledování aktivit správy.  
- Role systému lokality, které rozšiřuje funkce správy a využívají webové služby Internetová informační služba (IIS).
- Optimalizace doručování, Windows s nízkým zpožděním na pozadí (LEDBAT), Background Intelligent Transfer Service (BITS), BranchCache a další technologie pro ukládání do sdílené mezipaměti, které vám pomůžou spravovat obsah ve vašich sítích a mezi zařízeními.

Aby bylo možné Configuration Manager v produkčním prostředí, důkladně Naplánujte a otestujte funkce správy. Configuration Manager je výkonná aplikace pro správu s možností ovlivnění všech počítačů ve vaší organizaci. Když nasadíte a spravujete Configuration Manager s pečlivým naplánováním a zvážením vašich obchodních požadavků, Configuration Manager můžou snížit režijní náklady na správu a celkové náklady na vlastnictví.  

## <a name="user-interfaces"></a>Uživatelská rozhraní

### <a name="the-configuration-manager-console"></a><a name="BKMK_Console"></a>Konzola Configuration Manager

Po instalaci Configuration Manager použijte konzolu Configuration Manager ke konfiguraci lokalit a klientů a ke spouštění a monitorování úkolů správy. Tato konzola je hlavním bodem správy a umožňuje správu více lokalit.  

Konzolu Configuration Manager můžete nainstalovat do dalších počítačů a omezit přístup a omezit, kteří uživatelé s právy pro správu uvidí v konzole nástroje pomocí Configuration Manager správy na základě rolí.  

Další informace najdete v tématu [použití konzoly Configuration Manager](../servers/manage/admin-console.md).

### <a name="software-center"></a><a name="BKMK_ApplicationCatalog"></a>Centrum softwaru

**Centrum softwaru** je aplikace, která je nainstalována při instalaci klienta Configuration Manager do zařízení se systémem Windows. Uživatelé používají Centrum softwaru k vyžádání a instalaci softwaru, který nasazujete. Centrum softwaru umožňuje uživatelům provádět tyto akce:  

- Vyhledat a nainstalovat aplikace, aktualizace softwaru a nové verze operačního systému
- Zobrazit historii žádostí o software
- Zobrazení dodržování zásad vaší organizace v zařízeních

V centru softwaru můžete také zobrazit vlastní karty, které budou splňovat další obchodní požadavky.

Další informace najdete v [uživatelské příručce k centru softwaru](software-center.md).

## <a name="next-steps"></a>Další kroky

Než nainstalujete Configuration Manager, Seznamte se se základními pojmy a pojmy:

- Pokud jste obeznámeni s nástrojem System Center 2012 Configuration Manager, přečtěte si téma [co se změnilo ze služby System center 2012 Configuration Manager](../plan-design/changes/what-has-changed-from-configuration-manager-2012.md).

- Podrobný technický přehled Configuration Manager najdete v tématu [základy Configuration Manager](fundamentals.md).

Pokud jste obeznámeni se základními koncepty, použijte tuto knihovnu dokumentace, která vám umožní úspěšně nasadit a používat Configuration Manager. Začněte s následujícími články:

- [Funkce a možnosti Configuration Manager](../plan-design/changes/features-and-capabilities.md)  
- [Výběr řešení správy zařízení](../plan-design/choose-a-device-management-solution.md)  
- [Vyhodnotit Configuration Manager vytvořením vlastního testovacího prostředí](../get-started/set-up-your-lab.md)
- [Najít nápovědu k použití Configuration Manager](find-help.md)  
