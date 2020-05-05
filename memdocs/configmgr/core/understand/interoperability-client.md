---
title: Klient s rozšířenou vzájemnou funkční spoluprací
titleSuffix: Configuration Manager
description: Přečtěte si, jak používat rozšířeného klienta vzájemné funkční spolupráce pro dlouhodobou podporu statického Configuration Managerho klienta s aktuální branou.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 61296321251be45cfa0449a3e4f21ba79a024753
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722778"
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Použití Configuration Manager klientského softwaru pro rozšířenou interoperabilitu s budoucími verzemi Current Branch lokality

*Platí pro: Configuration Manager (Current Branch)*  

Obchodní požadavky možná neumožňují pravidelně aktualizovat klienta Configuration Manager na některých zařízeních. Například je třeba postupovat podle zásad správy změn nebo je zařízení klíčové. Podle těchto potřeb nainstalujte nového klienta pro dlouhodobé použití označovaný jako rozšířený klient vzájemné spolupráce (EIC). EIC použijte jenom pro konkrétní zařízení, která se nedají často aktualizovat, jako jsou veřejná zařízení nebo zařízení v prodeji. Pro většinu klientů používejte i nadále [Automatický upgrade klienta](../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate) .

## <a name="how-it-works"></a>Jak to funguje

Když nainstalujete novou [konzolovou aktualizaci](../servers/manage/install-in-console-updates.md) pro Configuration Manager, klienti nástroje automaticky aktualizují svůj klientský software, aby mohli používat tyto nové funkce. V tomto scénáři se pořád aktualizujete na aktuální větev přijímání nových funkcí a aktualizací. Většina zařízení aktualizuje Configuration Manager klientský software pomocí každé aktualizace verze, kterou nainstalujete. Nicméně v podmnožině důležitých systémů, které nechcete dostávat aktualizace klientského softwaru, nainstalujete rozšířenou spolupráci klienta. Tito klienti neinstalují nový klientský software, dokud do nich explicitně nenainstalujete novou verzi klientského softwaru.

## <a name="supported-versions"></a>Podporované verze

V následující tabulce jsou uvedeny verze Configuration Manager klienta, které jsou podporovány pro tento scénář:

| Verze | Datum dostupnosti | Datum ukončení podpory |
|---------|---------|---------|
| 1902<br/>5.00.8790 | 27. března 2019 | Starší než 27. března 2021 |
| 1802<br/>5.00.8634 | 1. května 2018 | Ne dříve než 1. května 2020 |
| 1606<br/>5.00.8412 | 18. listopadu 2016 | 1. května 2019 |

> [!TIP]  
> EIC se podporuje aspoň na dva roky od data vydání. Další informace o datech vydání najdete v tématu [podpora Configuration Manager aktuální verze větví](../servers/manage/current-branch-versions-supported.md).  

Naplánujte aktualizaci rozšířeného klienta interoperability na zařízeních, která spravujete v rámci aktuální větve před tím, než vyprší podpora pro klienta. Provedete to tak, že si stáhnete novou verzi klienta od Microsoftu a potom tento aktualizovaný klientský software nasadíte do zařízení, která používají aktuálního rozšířeného klienta v rámci interoperability.

## <a name="how-to-use-the-eic"></a>Jak používat EIC

1. Přidejte tato zařízení do kolekce a vylučte tuto kolekci z automatických upgradů klienta. Další informace najdete v tématu [jak vyloučit klienty z upgradu](../clients/manage/upgrade/exclude-clients-windows.md).  

1. Získejte podporovanou verzi EIC ze `\SMSSETUP\Client` složky instalačního média aktualizace Configuration Manager. Ujistěte se, že kopírujete celý obsah složky.  

    > [!TIP]  
    > Chcete-li najít Configuration Manager média na webu [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC), klikněte na kartu **soubory ke stažení a klíče** , vyhledejte `System Center Config`a vyberte možnost **System Center Configuration správce (aktuální větev)**.

1. Ručně nainstalujte EIC do těchto zařízení. Další informace najdete v tématu [Ruční instalace klienta](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual).  

    > [!Important]  
    > Při upgradu klientů verze 1606 na verzi 1802 použijte možnost CCMSETUP **/AlwaysExcludeUpgrade: true**. V opačném případě může klient od bodu správy získat zásadu k automatickému upgradu před zásadou vyloučení.  

## <a name="limitations"></a>Omezení

- Aktualizace rozšířeného klientského softwaru vzájemné funkční spolupráce nejsou k dispozici pomocí konzolových aktualizací. Další informace o tom, jak aktualizovat EIC, najdete v tématu [Postup upgradu vyloučeného klienta](../clients/manage/upgrade/exclude-clients-windows.md#bkmk_override).  

- EIC podporuje pouze následující funkce:  

  - Aktualizace softwaru  
  - Inventář hardwaru a softwaru
  - Balíčky a programy

## <a name="next-steps"></a>Další kroky

[Vyloučení klientů z upgradu](../clients/manage/upgrade/exclude-clients-windows.md)

Informace o tom, jak se ujistit, že klienti jsou na zařízeních, která chcete nainstalovat správně, najdete v tématu [Postup monitorování klientů](../clients/manage/monitor-clients.md).
