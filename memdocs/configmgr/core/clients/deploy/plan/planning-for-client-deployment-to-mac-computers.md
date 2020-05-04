---
title: Plánování nasazení klienta na počítače se systémem Mac
titleSuffix: Configuration Manager
description: Naplánujte nasazení klientů na počítače Mac v Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8d15ae3f-de42-461f-a907-c43873da22d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f231e0681b2a202696b6c719966abf818a9c8e27
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713223"
---
# <a name="planning-for-client-deployment-to-mac-computers-in-configuration-manager"></a>Plánování nasazení klientů na počítače Mac v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Klienta Configuration Manager můžete nainstalovat na počítače Mac, na kterých běží operační systém Mac OS X, a použijte následující možnosti správy:  

- **Inventář hardwaru**  

   Pomocí Configuration Manager inventáře hardwaru můžete shromažďovat informace o hardwaru a nainstalovaných aplikacích na počítačích Mac. Tyto informace se pak dají zobrazit v Průzkumník prostředků v konzole Configuration Manager a používají se k vytváření kolekcí, dotazů a sestav. Další informace najdete v tématu [použití Průzkumník prostředků k zobrazení inventáře hardwaru](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

   Configuration Manager shromažďuje následující informace o hardwaru z počítačů Mac:  

  -   Procesor  

  -   Systém počítače  

  -   Disková jednotka  

  -   Diskový oddíl  

  -   Síťový adaptér  

  -   Operační systém  

  -   Služba  

  -   Proces  

  -   Nainstalovaný software  

  -   Produkt počítačového systému  

  -   Řadič USB  

  -   Zařízení USB  

  -   Jednotka CD  

  -   Grafický adaptér  

  -   Stolní monitor  

  -   Přenosná baterie  

  -   Fyzická paměť  

  -   Tiskárna  

  > [!IMPORTANT]  
  >  Informace o hardwaru shromážděné z počítačů Mac nelze během inventáře hardwaru rozvést.  

- **Nastavení dodržování předpisů**  

   Nastavení dodržování předpisů Configuration Manager můžete použít k zobrazení dodržování předpisů a napravení nastavení Mac OS X předvoleb (. plist). Můžete například vynutili nastavení domovské stránky ve webovém prohlížeči Safari nebo ověřit, že je povolená brána firewall Apple. Pomocí skriptů prostředí můžete také monitorovat a opravovat nastavení v MAC OS X.  

- **Správa aplikací**  

   Configuration Manager mohou nasadit software do počítačů se systémem Mac. Do počítačů se systémem Mac můžete nasadit následující formáty softwaru:  

  -   Bitová kopie disku Apple (. DMG  

  -   Soubor meta Package (. MPKG  

  -   Balíček Instalační služby Mac OS X (. PKG  

  -   Mac OS X aplikace (. APLIKACE  

  Když nainstalujete klienta Configuration Manager do počítačů se systémem Mac, nemůžete použít následující funkce správy, které jsou podporovány klientem Configuration Manager v počítačích se systémem Windows:  

- Klientská nabízená instalace  

- Nasazení operačního systému  

- Aktualizace softwaru  

  > [!NOTE]  
  >  Správu aplikací Configuration Manager můžete použít k nasazení požadovaných Mac OS X aktualizací softwaru do počítačů se systémem Mac. Kromě toho můžete pomocí nastavení dodržování předpisů zajistit, aby počítače měly požadované aktualizace softwaru.  

- Časové intervaly pro správu a údržbu  

- Vzdálené řízení  

- Řízení spotřeby  

- Kontrola a náprava stavu klienta  

  Další informace o instalaci a konfiguraci klienta Configuration Manager Mac najdete v tématu [nasazení klientů na](../../../../core/clients/deploy/deploy-clients-to-macs.md)počítače Mac.
