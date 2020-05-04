---
title: Požadavky řízení spotřeby
titleSuffix: Configuration Manager
description: Získejte požadavky na řízení spotřeby v Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a816d333d96dba6cb1c38f6499ccac78e2db8a3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715183"
---
# <a name="prerequisites-for-power-management-in-configuration-manager"></a>Požadavky na řízení spotřeby v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Řízení spotřeby v Configuration Manager má vnější závislosti a závislosti v rámci produktu.  

## <a name="dependencies-external-to-configuration-manager"></a>Vnější závislosti nástroje Configuration Manager  
 Následující tabulka uvádí vnější závislosti Configuration Manager pro použití řízení spotřeby.  

|Závislost|Další informace|  
|----------------|----------------------|  
|Klientské počítače musí být schopné podporovat požadované stavy spotřeby.|Aby bylo možné používat všechny funkce řízení spotřeby, klientské počítače musí být schopné podporovat přechod do režimu spánku nebo hibernace nebo probuzení z režimu spánku nebo hibernace. Pomocí sestavy **Možnosti napájení** můžete určit, jestli počítače můžou podporovat tyto akce. Další informace najdete v tématu [Sestava možností napájení](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) v tématu [monitorování a plánování řízení spotřeby](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).|  

## <a name="configuration-manager-dependencies"></a>Závislosti nástroje Configuration Manager  
 Následující tabulka uvádí závislosti v rámci Configuration Manager pro použití řízení spotřeby.  

|Závislost|Další informace|  
|----------------|----------------------|  
|Před vytvořením a monitorováním schémat napájení musí být povolené řízení spotřeby.|Informace o tom, jak povolit a nakonfigurovat řízení spotřeby, najdete v tématu [Konfigurace řízení spotřeby](../../../../core/clients/manage/power/configuring-power-management.md).|  
|Bod služby Reporting services|Před zobrazením sestav řízení spotřeby musíte konfigurovat bod služby Reporting services. Další informace najdete v tématu [Úvod do vytváření sestav](../../../servers/manage/introduction-to-reporting.md).|  
