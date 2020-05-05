---
title: Funkce a možnosti
titleSuffix: Configuration Manager
description: Přečtěte si o hlavních možnostech správy Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5cdd0a9497f07d80813aca5dc169c4d61944e85d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722372"
---
# <a name="features-and-capabilities-of-configuration-manager"></a>Funkce a možnosti Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek shrnuje hlavní funkce správy Configuration Manager. Každá z těchto funkcí má své vlastní požadavky a jejich použití může mít vliv na návrh a implementaci vaší Configuration Manager hierarchie. Pokud například chcete nasadit aktualizace softwaru do zařízení v hierarchii, budete potřebovat roli systému lokality bodu aktualizace softwaru.  

Další informace o tom, jak naplánovat a nainstalovat Configuration Manager pro podporu těchto možností správy ve vašem prostředí, najdete v článku [Příprava na Configuration Manager](../get-ready.md).  

## <a name="co-management"></a>Spoluspráva

Spoluspráva je jedním z hlavních způsobů, jak připojit stávající nasazení Configuration Manager ke cloudu Microsoft 365. Umožňuje souběžně spravovat zařízení s Windows 10 pomocí Configuration Manager i Microsoft Intune. Spoluspráva umožňuje cloudově připojit stávající investice do Configuration Manager přidáním nových funkcí, jako je podmíněný přístup. Další informace najdete v tématu [co je společná správa](../../../comanage/overview.md)?.

## <a name="desktop-analytics"></a>Desktop Analytics

Desktop Analytics je cloudová služba, která se integruje s Configuration Manager. Služba poskytuje přehled a inteligentní informace, které vám pomohou s rozhodováním o připravenosti na aktualizace svých klientů s Windows. Kombinuje data z vaší organizace s daty agregovanými z milionů zařízení připojených ke cloudovým službám Microsoftu. Další informace najdete v tématu [co je Desktop Analytics](../../../desktop-analytics/overview.md)?

## <a name="cloud-attached-management"></a>Správa s připojením ke cloudu

Internetové klienty můžete spravovat pomocí funkcí, jako je brána pro správu cloudu, cloudové distribuční body a Azure Active Directory.

Další informace najdete v těchto článcích:

- [Správa klientů na internetu](../../clients/manage/manage-clients-internet.md)
- [Plán pro Azure AD](../security/plan-for-security.md#bkmk_planazuread)
- [Služby Azure](../../servers/deploy/configure/azure-services-wizard.md)

## <a name="real-time-management"></a>Správa v reálném čase

Použijte CMPivot k okamžitému dotazování online zařízení a pak filtrujte a Seskupujte data pro hlubší poznatky. Ke správě a nasazování skriptů prostředí Windows PowerShell pro klienty taky použijte konzolu Configuration Manager. Další informace najdete v tématu [CMPivot](../../servers/manage/cmpivot.md) a [vytváření a spouštění skriptů PowerShellu](../../../apps/deploy-use/create-deploy-scripts.md).

## <a name="application-management"></a>Správa aplikací

Pomáhá vytvářet, spravovat, nasazovat a monitorovat aplikace do různých různých zařízení, která spravujete. Nasaďte, aktualizujte a spravujte Office 365 z konzoly Configuration Manager. Kromě toho Configuration Manager integrovat s Microsoft Store pro firmy a vzdělávání a dodávat cloudové aplikace. Další informace najdete v tématu [Úvod do správy aplikací](../../../apps/understand/introduction-to-application-management.md).

## <a name="os-deployment"></a>Nasazení operačního systému

Nasaďte místní upgrade Windows 10 nebo Zachyťte a nasaďte image operačních systémů. Nasazení image může používat PXE, vícesměrové vysílání nebo spouštěcí média. Může také pomoci znovu nasadit stávající zařízení pomocí nástroje Windows autopilot. Další informace najdete v tématu [Úvod do nasazení operačního systému](../../../osd/understand/introduction-to-operating-system-deployment.md).  

## <a name="software-updates"></a>Aktualizace softwaru

Spravujte, nasaďte a sledujte aktualizace softwaru v organizaci. Integrujte s optimalizací doručení Windows a dalšími technologiemi pro ukládání do mezipaměti, které vám pomůžou řídit využití sítě. Další informace najdete v tématu [Úvod do aktualizací softwaru](../../../sum/understand/software-updates-introduction.md).  

## <a name="company-resource-access"></a>Přístup k prostředkům společnosti

Umožňuje uživatelům ve vaší organizaci přístup k datům a aplikacím ze vzdálených umístění. Tato funkce zahrnuje profily Wi-Fi, VPN, e-mailu a certifikátů. Další informace najdete v tématu [Ochrana dat a infrastruktury lokality](../../../protect/understand/protect-data-and-site-infrastructure.md).

## <a name="compliance-settings"></a>Nastavení dodržování předpisů

Pomáhá vyhodnocovat, sledovat a opravovat kompatibilitu konfigurace klientských zařízení v organizaci. Kromě toho můžete pomocí nastavení dodržování předpisů nakonfigurovat řadu funkcí a nastavení zabezpečení na zařízeních, která spravujete. Další informace najdete v tématu [zajištění dodržování předpisů zařízením](../../../compliance/understand/ensure-device-compliance.md).  

## <a name="endpoint-protection"></a>Funkce Endpoint Protection

Poskytuje zabezpečení, ochranu proti malwaru a správu brány Windows Firewall pro počítače ve vaší organizaci. Tato oblast zahrnuje správu a integraci s následujícími funkcemi Windows Defender Suite:

- Antivirová ochrana v programu Windows Defender
- Rozšířená ochrana před internetovými útoky v programu Microsoft Defender
- Ochrana Exploit Guard v programu Windows Defender
- Ochrana Application Guard v programu Windows Defender
- Řízení aplikací programu Windows Defender
- Firewall v programu Windows Defender

Další informace najdete v tématu [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).  

## <a name="inventory"></a>Inventarizace

Pomáhá identifikovat a monitorovat prostředky.

### <a name="hardware-inventory"></a>Inventář hardwaru

Shromažďuje podrobné informace o hardwaru zařízení ve vaší organizaci. Další informace najdete v tématu [Úvod do inventáře hardwaru](../../clients/manage/inventory/introduction-to-hardware-inventory.md).  

### <a name="software-inventory"></a>Inventář softwaru

Shromažďuje a hlásí informace o souborech uložených v klientských počítačích ve vaší organizaci. Další informace najdete v tématu [Úvod do inventáře softwaru](../../clients/manage/inventory/introduction-to-software-inventory.md).  

### <a name="asset-intelligence"></a>Funkce Asset Intelligence

Poskytuje nástroje pro shromažďování dat inventáře a monitorování využití softwarových licencí ve vaší organizaci. Další informace najdete v tématu [Úvod do funkce Asset Intelligence](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

## <a name="on-premises-mobile-device-management"></a>Místní správa mobilních zařízení

Umožňuje registrovat a spravovat zařízení pomocí místní infrastruktury Configuration Manager s funkcemi správy integrovanými do platforem zařízení. (Typická Správa používá samostatně nainstalovaného klienta Configuration Manager.) Tato funkce aktuálně podporuje správu zařízení se systémy Windows 10 Enterprise a Windows 10 Mobile. Další informace najdete v tématu [Správa mobilních zařízení s místní infrastrukturou](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

## <a name="power-management"></a>Řízení spotřeby

Spravujte a sledujte spotřebu energie klientských počítačů v organizaci. Nakonfigurujte schémata napájení a pomocí funkce Wake-on-LAN proveďte údržbu mimo pracovní dobu. Další informace najdete v tématu [Úvod do řízení spotřeby](../../clients/manage/power/introduction-to-power-management.md).  

## <a name="remote-control"></a>Vzdálené řízení

Poskytuje nástroje pro vzdálenou správu klientských počítačů z konzoly Configuration Manager. Další informace najdete v tématu [Úvod do vzdáleného řízení](../../clients/manage/remote-control/introduction-to-remote-control.md).  

## <a name="reporting"></a>Generování sestav

Pomocí rozšířených možností vytváření sestav SQL Server Reporting Services z konzoly Configuration Manager. Tato funkce poskytuje stovky výchozích sestav. Další informace najdete v tématu [Úvod do vytváření sestav](../../servers/manage/introduction-to-reporting.md).  

## <a name="software-metering"></a>Monitorování míry využití softwaru

Monitorování a shromažďování dat o využití softwaru od klientů Configuration Manager. Tato data můžete použít k určení, zda se software používá po instalaci. Další informace najdete v tématu [monitorování využití aplikací pomocí monitorování míry využívání softwaru](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  
