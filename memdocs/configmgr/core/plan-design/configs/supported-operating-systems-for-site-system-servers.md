---
title: " Podporované servery systému lokality"
titleSuffix: Configuration Manager
description: Zjistěte, které verze systému Windows můžete použít k hostování Configuration Manager lokality nebo role systému lokality.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cc58ae7f7b5629319d239f9c48b5c6572fb28116
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711585"
---
# <a name="supported-operating-systems-for-configuration-manager-site-system-servers"></a>Podporované operační systémy pro servery systému lokality Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek podrobně popisuje verze systému Windows, které můžete použít k hostování Configuration Manager lokality nebo role systému lokality.

Informace v tomto článku použijte spolu s informacemi v následujících článcích:

- [Doporučený hardware pro nástroj Configuration Manager](recommended-hardware.md)
- [Požadavky lokality a systému lokality pro Configuration Manager](site-and-site-system-prerequisites.md)
- [Dimenzování a škálování nástroje Configuration Manager](size-and-scale-numbers.md)

## <a name="windows-server-2019"></a><a name="bkmk_2019"></a>Windows Server 2019

*Platí pro Windows Server 2019: Standard a Datacenter.* 

Počínaje verzí 1810 je tato verze operačního systému podporovaná pro následující role:

#### <a name="site-servers"></a>Servery lokalit

- Lokalita centrální správy  
- Primární lokalita  
- Sekundární lokalita  

#### <a name="site-system-servers"></a>Servery systému lokality

- Bod služeb webu Katalog aplikací  
- Bod webu Katalog aplikací  
- Bod synchronizace katalogu Asset Intelligence  
- Bod registrace certifikátu  
- Bod připojení brány pro správu cloudu  
- Bod služby datového skladu  
- Poznámka k distribučnímu bodu <sup> [1](#bkmk_note1)</sup>  
- Bod ochrany koncového bodu Endpoint Protection  
- Bod registrace  
- Zprostředkující bod registrace  
- Bod záložního stavu  
- Bod správy
- Bod služby Reporting services  
- Spojovací bod služby  
- Server databáze lokality – <sup> [Poznámka 2](#bkmk_note2)</sup>  
- SMS_Provider  
- Bod aktualizace softwaru  
- Bod migrace stavu

## <a name="windows-server-2016"></a><a name="bkmk_2016"></a>Windows Server 2016

*Platí pro Windows Server 2016: Standard a Datacenter.*

Tato verze operačního systému je podporovaná pro následující role:

#### <a name="site-servers"></a>Servery lokalit

- Lokalita centrální správy  
- Primární lokalita  
- Sekundární lokalita  

#### <a name="site-system-servers"></a>Servery systému lokality

- Bod služeb webu Katalog aplikací  
- Bod webu Katalog aplikací  
- Bod synchronizace katalogu Asset Intelligence  
- Bod registrace certifikátu  
- Bod připojení brány pro správu cloudu  
- Bod služby datového skladu  
- Poznámka k distribučnímu bodu <sup> [1](#bkmk_note1)</sup>  
- Bod ochrany koncového bodu Endpoint Protection  
- Bod registrace  
- Zprostředkující bod registrace  
- Bod záložního stavu  
- Bod správy
- Bod služby Reporting services  
- Spojovací bod služby  
- Server databáze lokality – <sup> [Poznámka 2](#bkmk_note2)</sup>  
- SMS_Provider  
- Bod aktualizace softwaru  
- Bod migrace stavu

## <a name="windows-storage-server-2016"></a><a name="bkmk_stor2016"></a>Windows Storage Server 2016

#### <a name="site-system-server"></a>Server systému lokality

- Poznámka k distribučnímu bodu <sup> [1](#bkmk_note1)</sup>  

## <a name="windows-server-2012-r2"></a><a name="bkmk_2012r2"></a>Windows Server 2012 R2

*Platí pro Windows Server 2012 R2: Standard a Datacenter.*

#### <a name="site-servers"></a>Servery lokalit

- Lokalita centrální správy  
- Primární lokalita  
- Sekundární lokalita  

#### <a name="site-system-servers"></a>Servery systému lokality

- Bod služeb webu Katalog aplikací  
- Bod webu Katalog aplikací  
- Bod synchronizace katalogu Asset Intelligence  
- Bod registrace certifikátu  
- Bod připojení brány pro správu cloudu  
- Bod služby datového skladu  
- Poznámka k distribučnímu bodu <sup> [1](#bkmk_note1)</sup>  
- Bod ochrany koncového bodu Endpoint Protection  
- Bod registrace  
- Zprostředkující bod registrace  
- Bod záložního stavu  
- Bod správy
- Bod služby Reporting services  
- Spojovací bod služby  
- Server databáze lokality – <sup> [Poznámka 2](#bkmk_note2)</sup>  
- SMS_Provider  
- Bod aktualizace softwaru  
- Bod migrace stavu  

## <a name="windows-server-2012"></a><a name="bkmk_2012"></a>Windows Server 2012  

*Platí pro Windows Server 2012: Standard a Datacenter.*

#### <a name="site-servers"></a>Servery lokalit

- Lokalita centrální správy  
- Primární lokalita  
- Sekundární lokalita  

#### <a name="site-system-servers"></a>Servery systému lokality

- Bod služeb webu Katalog aplikací  
- Bod webu Katalog aplikací  
- Bod synchronizace katalogu Asset Intelligence  
- Bod registrace certifikátu  
- Bod připojení brány pro správu cloudu  
- Bod služby datového skladu  
- Poznámka k distribučnímu bodu <sup> [1](#bkmk_note1)</sup>  
- Bod ochrany koncového bodu Endpoint Protection  
- Bod registrace  
- Zprostředkující bod registrace  
- Bod záložního stavu  
- Bod správy
- Bod služby Reporting services  
- Spojovací bod služby  
- Server databáze lokality – <sup> [Poznámka 2](#bkmk_note2)</sup>  
- SMS_Provider  
- Bod aktualizace softwaru  
- Bod migrace stavu  

## <a name="client-os-versions"></a><a name="bkmk_client"></a>Verze operačního systému klienta

Následující verze operačního systému klienta jsou podporovány pro použití jako **distribuční bod** <sup>[Poznámka 1](#bkmk_note1)</sup>:  

- Windows 10 (x86, x64): pro a Enterprise

    Další informace o podporovaných verzích sestavení najdete v tématu [Podpora pro Windows 10](support-for-windows-10.md).

- Windows 8.1 (x86, x64): Professional a Enterprise

Tato podpora má následující omezení:  

- Distribuční body v tomto operačním systému nepodporují technologii PXE ani vícesměrové vysílání s výchozí službou pro nasazení systému Windows. Počínaje verzí 1806 můžete pomocí technologie PXE povolit distribuční bod v tomto operačním systému s možností **Povolit respondér technologie PXE bez služby pro nasazení systému Windows**. Další informace najdete v tématu [instalace a konfigurace distribučních bodů](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).  

## <a name="server-core-installations"></a><a name="bkmk_core"></a>Instalace jádra serveru

Instalace jádra serveru z následujících verzí operačního systému serveru se podporuje pro použití jako **distribuční bod**:

- Windows Server 2019 (počínaje Configuration Manager verze 1810)  
- Windows Server verze 1809 (počínaje Configuration Manager, verze 1810)  
- Windows Server verze 1803 (počínaje Configuration Manager, verze 1802)  
- Windows Server verze 1709 (počínaje Configuration Manager, verze 1710)  
- Windows Server 2016  
- Windows Server 2012 R2  
- Windows Server 2012  

Tato podpora má následující omezení:  

- Distribuční body v tomto operačním systému nepodporují technologii PXE ani vícesměrové vysílání s výchozí službou pro nasazení systému Windows. Počínaje verzí 1806 můžete pomocí technologie PXE povolit distribuční bod v tomto operačním systému s možností **Povolit respondér technologie PXE bez služby pro nasazení systému Windows**. Další informace najdete v tématu [instalace a konfigurace distribučních bodů](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).  

## <a name="general-notes"></a>Obecné poznámky

### <a name="note-1-distribution-points"></a><a name="bkmk_note1"></a>Poznámka 1: distribuční body

Distribuční body podporují několik různých konfigurací, které mají různé požadavky. V některých případech tyto konfigurace podporují instalaci nejen na serverech, ale i v klientských operačních systémech. Další informace najdete v tématu [Správa obsahu a infrastruktury obsahu](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="note-2-site-database-servers"></a><a name="bkmk_note2"></a>Poznámka 2: servery databáze lokality

Servery databáze lokality se nepodporují na řadiči domény jen pro čtení (RODC). Další informace najdete v podpora Microsoftu článku: [při instalaci SQL Server na řadič domény se můžete setkat s problémy](https://support.microsoft.com/help/2032911). 

Na žádném řadiči domény navíc nejsou podporované servery sekundární lokality.  
