---
title: Podpora pro Windows 10
titleSuffix: Configuration Manager
description: Přečtěte si o verzích Windows 10, které jsou podporované jako klienti nebo pro OSD s Configuration Manager
ms.date: 05/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a67a22f788af39dacb9f3a39e91e0f28444c6988
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879074"
---
# <a name="support-for-windows-10-in-configuration-manager"></a>Podpora pro Windows 10 v Configuration Manager  

*Platí pro: Configuration Manager (Current Branch)*

Přečtěte si o verzích Windows 10, které Configuration Manager podporuje, včetně:

- [Windows 10 jako klient Configuration Manager](#windows-10-as-a-client)
- [Sada Windows Assessment and Deployment Kit (ADK) pro Windows 10](#windows-10-adk)

> [!Tip]
> Sestavení Windows serveru jako klient se podporují stejně jako přidružená verze Windows 10. Například Windows Server 2016 je stejná verze buildu jako Windows 10 LTSB 2016 a Windows Server verze 1803 je stejná verze buildu jako Windows 10 verze 1803.
>
> Další informace o systému Windows Server jako systému lokality najdete v tématu [podporované operační systémy pro Configuration Manager servery systému lokality](supported-operating-systems-for-site-system-servers.md#bkmk_core).

## <a name="windows-10-as-a-client"></a>Windows 10 jako klient

Configuration Manager se pokusí poskytovat podporu jako klienta pro každou novou verzi Windows 10 hned po zpřístupnění. Vzhledem k tomu, že produkty mají samostatné plány vývoje a vydání, podpora, kterou Configuration Manager poskytuje, závisí na tom, kdy budou všechny dostupné.

Configuration Manager verze v matici po [podpoře pro tuto verzi](../../servers/manage/current-branch-versions-supported.md) poklesne. Podobně podpora verzí Windows 10, jako je například Enterprise 2015 LTSB nebo 1511, se z matice odeberou, když jsou odebrané z podpory.

- Nejnovější verze Configuration Manager aktuální větve obdrží aktualizace zabezpečení i důležité aktualizace, které můžou zahrnovat opravy pro problémy s verzemi Windows 10. Když společnost Microsoft vydává novou verzi Configuration Manager aktuální větev, předchozí verze dostávají pouze aktualizace zabezpečení. Další informace najdete v tématu [podpora Configuration Manager aktuální verze větví](../../servers/manage/current-branch-versions-supported.md).  

    > [!Note]  
    > Nejlepším způsobem, jak si udržet aktuálnost s Windows 10, je zůstat aktuální Configuration Manager. Další informace najdete v tématu [Configuration Manager a Windows jako služba](../../understand/configuration-manager-and-windows-as-service.md).  

- Tyto informace doplňují [podporované operační systémy pro klienty a zařízení](supported-operating-systems-for-clients-and-devices.md).  

- Pokud používáte větev dlouhodobé údržby Configuration Manager, přečtěte si téma [podporované konfigurace pro dlouhodobou obsluhu](../../understand/supported-configurations-for-ltsb.md).  

V následující tabulce jsou uvedeny verze systému Windows 10, které lze použít jako klient s různými verzemi nástroje Configuration Manager.

| Verze Windows 10 | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 |
|---------------------|-----|-----|-----|-----|-----|
| **Enterprise 2015 LTSB** <!--10/14/2025-->   | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) |
| **Enterprise 2016 LTSB** <!--10/13/2026-->   | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) |
| **Enterprise LTSC 2019** <!--01/09/2029-->   | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) |
| **1709**<br>(10.0.16299)   <!--10/13/2020-->   | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) |
| **1803**<br>(10.0.17134)   <!--11/10/2020-->   | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) |
| **1809**<br>(10.0.17763)   <!--05/11/2021-->   | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) |
| **1903**<br>(10.0.18362)   <!--12/08/2020-->   | ![Nepodporuje se](media/Red_X.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) |
| **1909**<br>(10.0.18363)   <!--05/10/2022-->   | ![Nepodporuje se](media/Red_X.png) | ![Nepodporuje se](media/Red_X.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) |
| **2004**<br>(10.0.19041)   <!--??/??/2021-->   | ![Nepodporuje se](media/Red_X.png) | ![Nepodporuje se](media/Red_X.png) | ![Nepodporuje se](media/Red_X.png) | ![Nepodporuje se](media/Red_X.png) | ![Podporuje se](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

Další informace o životním cyklu Windows najdete na [listu faktu pro životní cyklus Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet) .

| Klíč |
|--|
| ![](media/green_check.png)Podporovaná podpora  =  **Supported**  |
| ![](media/Red_X.png)Nepodporovaná není podporovaná  =  **Not supported** |

### <a name="windows-10-client-support-notes"></a><a name="bkmk_win10-notes"></a>Poznámky k podpoře klientů s Windows 10

- Podpora pro pololetní verze kanálů Windows 10 zahrnuje tyto edice: Enterprise, pro, vzdělávání a vzdělávání pro.  

- Počínaje verzí 1906 Configuration Manager podporuje Windows 10 pro for Workstation.

- Pro Windows 10 verze 1909 se u média pro nasazení operačního systému zobrazuje verze jako 10.0.18362.418.

### <a name="windows-10-on-arm64"></a><a name="bkmk_arm64"></a>Windows 10 v ARM64

Configuration Manager podporuje klienta na zařízeních s Windows 10 ARM64. Nasazení operačního systému se nepodporuje.<!-- 1353704 -->

Počínaje verzí 2002,<!--5954175--> Platforma **All Windows 10 (ARM64)** je dostupná v seznamu podporovaných verzí operačního systému u objektů s pravidly požadavků nebo seznamy použitelnosti.

> [!NOTE]
> Pokud jste dříve vybrali platformu **Windows 10** na nejvyšší úrovni, tato akce automaticky vybrala **všechny systémy windows 10 (64 bitů)** i **všechny systémy Windows 10 (32-bit)**. Tato nová platforma není automaticky vybraná. Pokud chcete přidat **všechny systémy Windows 10 (ARM64)**, ručně je vyberte v seznamu.

### <a name="support-for-windows-insider"></a><a name="bkmk_WIfB-support"></a>Podpora pro Windows Insider

Počínaje verzí 1906 Configuration Manager můžete [aktualizovat a obsluhovat buildy Windows Insider](../../../sum/get-started/configure-classifications-and-products.md#bkmk_WIfB) . Tato možnost je k dispozici pro naše zákazníky jako pohodlí. I když tato funkce by měla fungovat, je jejich podpora nejlepší. Pokud přestane fungovat, Configuration Manager nemusí vydat opravu hotfix pro tuto funkci.  

Pokud chcete poskytnout zpětnou vazbu ke službě Windows Insider, použijte [Centrum zpětné vazby](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-feedback).

## <a name="windows-10-adk"></a>Windows 10 ADK

Pokud nasazujete operační systémy pomocí Configuration Manager, ADK Windows je požadovaná externí závislost. Další informace najdete v následujících článcích:

- [Požadavky na infrastrukturu pro nasazení operačního systému](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10)

- [Stažení sady Windows ADK pro Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install)

    > [!IMPORTANT]
    > Počínaje systémem Windows 10 verze 1809 je systém Windows PE samostatným instalačním programem. Jinak neexistuje žádný funkční rozdíl.
    >
    > Nezapomeňte si stáhnout balíček **Windows ADK pro Windows 10** a **doplněk Windows PE pro ADK**.

V následující tabulce jsou uvedeny verze ADK Windows 10, které můžete použít s různými verzemi Configuration Manager.

| Verze ADK Windows 10  | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 |
|--------------------|-----|-----|-----|-----|-----|
| **1709**<br>(10.1.16299) | ![Nepodporuje se](media/Red_X.png)   | ![Nepodporuje se](media/Red_X.png) | ![Nepodporuje se](media/Red_X.png) | ![Nepodporuje se](media/Red_X.png) | ![Nepodporuje se](media/Red_X.png) |
| **1803**<br>(10.1.17134) | ![Zpětně kompatibilní](media/blue_compat.png) | ![Zpětně kompatibilní](media/blue_compat.png) | ![Nepodporuje se](media/Red_X.png) | ![Nepodporuje se](media/Red_X.png) | ![Nepodporuje se](media/Red_X.png) |
| **1809**<br>(10.1.17763) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Zpětně kompatibilní](media/blue_compat.png) | ![Zpětně kompatibilní](media/blue_compat.png) | ![Nepodporuje se](media/Red_X.png) |
| **1903**<br>(10.1.18362) | ![Nepodporuje se](media/Red_X.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) | ![Podporuje se](media/green_check.png) |
| **2004**<br>(10.1.19041) | ![Nepodporuje se](media/Red_X.png) | ![Nepodporuje se](media/Red_X.png) | ![Nepodporuje se](media/Red_X.png) | ![Nepodporuje se](media/Red_X.png) | ![Podporuje se](media/green_check.png) |

|Klíč|
|--|
| ![](media/green_check.png)Podporovaná podpora  =  **Supported** <br/> V této tabulce je uvedena pouze podpora systému Windows ADK ve vztahu k verzi Configuration Manager. Microsoft doporučuje používat sadu Windows ADK, která odpovídá verzi Windows, kterou nasazujete. Při nasazení nejnovější verze Windows 10 použijte nejnovější verzi Windows ADK. Nejnovější verze systému Windows ADK může podporovat nasazení starších verzí operačního systému, například Windows 8.1.<!-- SCCMDocs issue 1229 --> Další informace o podpoře součástí Windows ADK najdete v článku [podporované platformy DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) a [požadavky na USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
| ![Zpětně kompatibilní ](media/blue_compat.png)   =  **zpětně** kompatibilní <br/> Tato kombinace není testována, ale měla by fungovat. Podíváme se na známé problémy nebo upozornění. |
| ![](media/Red_X.png)Nepodporovaná není podporovaná  =  **Not supported** |

### <a name="windows-10-adk-support-notes"></a><a name="bkmk_adk-notes"></a>Poznámky k podpoře pro Windows 10 ADK

- Configuration Manager podporuje pouze součásti x86 a amd64 systému Windows 10 ADK. V současné době nepodporuje komponenty ARM nebo ARM64.

- Sestavení Windows serveru mají stejný požadavek Windows ADK jako přidružená verze Windows 10. Například Windows Server 2016 je stejná verze buildu jako Windows 10 LTSB 2016.
