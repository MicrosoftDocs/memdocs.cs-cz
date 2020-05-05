---
title: Výběr řešení správy zařízení
titleSuffix: Configuration Manager
description: Seznamte se s řešeními, která Microsoft nabízí pro správu počítačů, serverů a zařízení.
ms.date: 01/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d36e29f0f915c0f2a35070c667525853e5981564
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719264"
---
# <a name="choose-a-device-management-solution"></a>Výběr řešení správy zařízení

Microsoft nabízí různá řešení pro správu počítačů, serverů a zařízení. Tato řešení jsou k dispozici místně, v cloudu nebo v kombinaci obou. Vyberte řešení, které je nejvhodnější pro obchodní požadavky vaší organizace. Založte rozhodnutí na platformách zařízení, které potřebujete ke správě, a o funkcích správy, které potřebujete.

## <a name="overview"></a>Přehled

K dispozici je několik řešení Microsoftu, která by mohla fungovat nejlépe v různých scénářích. Nemusíte volit jenom jeden.

- Pro malou organizaci může být vhodným nástrojem jako centrum pro správu systému Windows.
- Pro správu svých zařízení používá Configuration Manager přibližně 75% IT organizací.
- Microsoft Azure poskytuje různá řešení v cloudu nebo v místním prostředí s Azure Stack, která primárně cílí na správu serveru.
- Microsoft Intune poskytuje cloudovou správu klientů.
- Pomocí spolusprávy můžete kombinovat Configuration Manager a Intune.

Následující tabulku vám pomůžou porovnat tyto technologie pro správu:

|  | Výhradně cloudový | Připojeno ke cloudu | Lokálně | Propojení |
|---------|---------|---------|---------|---------|
| **Hostitel Hyper-V** | Neuvedeno | -Azure Stack<br/> – Centrum pro správu Windows<br/> -Virtual Machine Manager | -Azure Stack<br/> – Centrum pro správu Windows<br/> -Virtual Machine Manager | -Azure Stack<br/> – Centrum pro správu Windows<br/> -Virtual Machine Manager |
| **Windows Server** | – Správa Azure<br/> -Configuration Manager | – Správa Azure<br/> -Configuration Manager | – Správa Azure<br/> -Configuration Manager | Configuration Manager |
| **Server Linux** | Správa Azure | Správa Azure | Správa Azure |  |
| **Windows 10** | – Intune<br/> -Configuration Manager | – Intune<br/> -Configuration Manager | – Intune<br/> -Configuration Manager | Configuration Manager |
| **Windows 7 nebo 8,1** | Configuration Manager | Configuration Manager | Configuration Manager | Configuration Manager |
| **Windows Virtual Desktop** | Configuration Manager | Neuvedeno | Neuvedeno | Neuvedeno |

Další informace najdete v těchto článcích:

- [Co je Azure Stack?](https://docs.microsoft.com/azure-stack/operator/azure-stack-overview)
- [Co je centrum pro správu Windows?](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/what-is)
- [Co je nástroj Virtual Machine Manager?](https://docs.microsoft.com/system-center/vmm/overview)
- [Produkty pro správu Azure](https://docs.microsoft.com/azure/)
- [Co je Windows Virtual Desktop?](https://docs.microsoft.com/azure/virtual-desktop/overview)

Další informace o Configuration Manager a řešeních Intune najdete v další části.

## <a name="client-management"></a>Správa klientů

V této části se porovnávají následující čtyři řešení pro správu klientů:

- [Klient Configuration Manager](#bkmk_sccm)
- [Místní správa mobilních zařízení (MDM) s Configuration Manager](#bkmk_opmdm)
- [Spoluspráva pomocí Microsoft Intune](#bkmk_comanage)
- [Microsoft Exchange](#bkmk_opmdm)

Tato řešení můžete použít samostatně nebo v kombinaci s jinými. Například použijte přístup pro správu na základě klientů ke správě počítačů a serverů ve vaší organizaci a ke správě internetových přenosných počítačů používejte spolusprávu. Kombinací přístupů tímto způsobem můžete pokrýt všechny požadavky na správu zařízení.  

K dispozici jsou také dvě tabulky, které porovnávají řešení pro správu následujícími faktory:

- [Porovnání podle podporovaných platforem](#bkmk_comp1)
- [Porovnání funkcí správy](#bkmk_comp2)

### <a name="configuration-manager-client"></a><a name="bkmk_sccm"></a>Klient Configuration Manager  

Tato možnost vyžaduje instalaci klienta Configuration Manager v zařízeních. Poskytuje nejvíc funkcí pro správu počítačů, serverů a dalších zařízení ve vašem prostředí.

Další informace najdete v tématu [metody instalace klientů](../clients/deploy/plan/client-installation-methods.md).  

### <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a>Místní MDM  

Tato možnost používá možnosti správy zařízení, které jsou součástí Windows 10. I když není tak plně vybavená jako správa na základě klientů, místní MDM poskytuje jednodušší přístup ke správě. Pro správu zařízení používá místní Configuration Manager prostředky.  

Další informace najdete v tématu [Správa mobilních zařízení s místní infrastrukturou](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

### <a name="co-management-with-microsoft-intune"></a><a name="bkmk_comanage"></a>Spoluspráva pomocí Microsoft Intune

Spoluspráva je jedním z hlavních způsobů, jak připojit stávající nasazení Configuration Manager ke cloudu Microsoft 365. Umožňuje souběžně spravovat zařízení s Windows 10 pomocí Configuration Manager i Microsoft Intune. Spoluspráva umožňuje cloudově připojit stávající investice do Configuration Manager přidáním nových funkcí.

Další informace najdete v tématu [co je spoluspráva?](../../comanage/overview.md).  

### <a name="microsoft-exchange"></a><a name="bkmk_exchange"></a>Microsoft Exchange  

Tato možnost používá konektor systému Exchange Server k připojení více serverů Exchange k Configuration Manager. Slouží k centralizaci správy zařízení, která se můžou připojit k Exchange ActiveSync. Funkce správy mobilních zařízení systému Exchange můžete nakonfigurovat z konzoly Configuration Manager. Příklady funkcí zahrnují vzdálené vymazání zařízení a řízení nastavení pro více serverů Exchange.

Další informace najdete v tématu [Správa mobilních zařízení pomocí Configuration Manager a Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="compare-solutions-by-supported-platforms"></a><a name="bkmk_comp1"></a>Porovnání řešení podle podporovaných platforem  

|Platforma|Klient Configuration Manager|Místní správa MDM|Configuration Manager se systémem Exchange| Intune |
|--------|----------------------------|---------------|-----------------------------------|--------|
|Android| | |Ano| Ano |
|iOS| | |Ano| Ano |
|Mac OS X|Ano| |Ano| Ano |
|Windows 10|Ano|Ano|Ano| Ano |
|Windows 10 Mobile| |Ano|Ano| Ano |
|Windows (předchozí verze)|Ano| |Ano|  |
|Windows Server|Ano| |Ano|  |
|Windows Embedded|Ano| | |  |

Úplný seznam podporovaných platforem najdete v následujících článcích:

- [Podporované operační systémy pro klienty a zařízení pro Configuration Manager](configs/supported-operating-systems-for-clients-and-devices.md)
- [Konfigurace podporované v Intune](https://docs.microsoft.com/intune/supported-devices-browsers)

Microsoft doporučuje používat Intune ke správě zařízení se systémem Android, iOS a Windows 10 Mobile. Další informace najdete v tématu [co je Microsoft Intune?](https://docs.microsoft.com/intune/what-is-intune).

### <a name="compare-solutions-by-management-functionality"></a><a name="bkmk_comp2"></a>Porovnání řešení podle funkcí správy  

|Funkce správy|Klient Configuration Manager|Místní správa MDM|Configuration Manager se systémem Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Vzájemné ověřování založené na certifikátech|Ano|Ano| |
|Instalace klienta|Ano| | |
|Podpora přes Internet|Ano| | |
|Zjišťování|Ano| |Ano|
|Inventář hardwaru|Ano|Ano|Ano|
|Inventář softwaru|Ano| |Ano|
|Nastavení|Ano|Ano|Ano|
|Nasazení softwaru|Ano|Ano| |
|Správa aktualizací softwaru|Ano| | |
|Nasazení operačního systému|Ano| | |
|Blokovat z Configuration Manager|Ano|Ano| |
|Karanténa a blokování ze systému Exchange Server (a Configuration Manager)| | |Ano|
|Vzdálené vymazání| |Ano|Ano|
