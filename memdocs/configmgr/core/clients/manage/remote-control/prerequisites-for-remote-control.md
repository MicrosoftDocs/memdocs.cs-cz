---
title: Požadavky na vzdálené řízení
titleSuffix: Configuration Manager
description: Získejte předpoklady pro vzdálené řízení v Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f19f8799dd90fc61c0bfeeee1dc60125ba491fef
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715113"
---
# <a name="prerequisites-for-remote-control-in-configuration-manager"></a>Předpoklady pro vzdálené řízení v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Vzdálené řízení v Configuration Manager má vnější závislosti a závislosti v rámci produktu.  

## <a name="dependencies-external-to-configuration-manager"></a>Vnější závislosti nástroje Configuration Manager  

|Závislost|Další informace|  
|----------------|----------------------|  
|Ovladač videokarty počítače|Zkontrolujte, zda je v klientských počítačích nainstalovaný nejaktuálnější ovladač videokarty, aby se zajistil optimální výkon vzdáleného řízení.|  

 Zařízení, která používají systém Windows Embedded for Point of Service (POS) a Windows Fundamentals pro starší počítače, nepodporují prohlížeč vzdáleného řízení, ale podporují klienta vzdáleného řízení.  

 Configuration Manager vzdálené řízení nelze použít pro vzdálenou správu klientských počítačů, které používají Systems Management Server 2003 nebo Configuration Manager 2007.  

> [!NOTE]  
>  Pro vzdálené řízení nejsou požadované  žádné služby Windows jako vnější závislosti.  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>Podporované operační systémy pro prohlížeč vzdáleného řízení  
Prohlížeč vzdáleného řízení je podporován ve všech operačních systémech podporovaných konzolou Configuration Manager. Informace najdete v tématu [podporované konfigurace pro Configuration Manager konzolách](../../../../core/plan-design/configs/supported-operating-systems-consoles.md).   

## <a name="configuration-manager-dependencies"></a>Závislosti nástroje Configuration Manager  

|Závislost|Další informace|  
|----------------|----------------------|  
|Musí být povolené vzdálené řízení pro klienty|Ve výchozím nastavení není vzdálené řízení povolené při instalaci Configuration Manager. Informace o tom, jak povolit a nakonfigurovat vzdálené řízení, najdete v tématu [Konfigurace vzdáleného řízení](../../../../core/clients/manage/remote-control/configuring-remote-control.md).|  
|Bod služby Reporting services|Před spuštěním sestav pro vzdálené řízení musí být nainstalovaná role systému lokality bodu služby Reporting Services. Další informace najdete v tématu [Úvod do vytváření sestav](../../../servers/manage/introduction-to-reporting.md).|  
|Oprávnění zabezpečení pro správu vzdáleného řízení|Pro přístup k prostředkům kolekce a k zahájení relace vzdáleného řízení z konzoly Configuration Manager: oprávnění **číst**, **číst prostředek**a **vzdálené řízení** pro objekt **kolekce** .<br /><br /> Role zabezpečení **operátor nástrojů pro vzdálenou** správu zahrnuje tato oprávnění, která jsou nutná ke správě vzdáleného řízení v Configuration Manager.<br /><br /> Další informace najdete v tématu [Konfigurace správy na základě rolí pro Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).<br /><br /> Kromě toho musí být povoleným divákům uděleno oprávnění k používání vzdáleného řízení přidáním těchto uživatelů do seznamu **povolených prohlížečů vzdáleného řízení a vzdálené pomoci** v nastavení klienta **Remote Tools** .
