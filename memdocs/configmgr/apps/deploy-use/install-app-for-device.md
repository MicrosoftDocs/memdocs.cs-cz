---
title: Instalace aplikací pro zařízení
titleSuffix: Configuration Manager
description: K okamžité instalaci aplikace do zařízení bez kolekce použijte Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c2a71fca-8744-4d72-abf9-9d8c5d2afb00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2a9f0c7d6eb7d8ccc42c5740bdb4b67926f676d8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710220"
---
# <a name="install-applications-for-a-device"></a>Instalace aplikací pro zařízení

<!--4402180-->

Počínaje verzí 1906 můžete v konzole Configuration Manager instalovat aplikace do zařízení v reálném čase. Tato funkce může přispět k omezení nutnosti samostatné kolekce pro každou aplikaci.

## <a name="prerequisites"></a>Požadavky

- Povolit [volitelnou funkci](../../core/servers/manage/install-in-console-updates.md#bkmk_options) **schválit žádosti o aplikace pro uživatele na zařízení**.  

- [Nasaďte aplikaci](deploy-applications.md) jako *dostupnou* pro kolekci zařízení.  

    - Na stránce **nastavení nasazení** v Průvodci nasazením vyberte následující možnost: **Správce musí na zařízení schválit žádost o tuto aplikaci**.  

        > [!Note]  
        > S těmito nastaveními nasazení nejsou klientovi odesílány žádné zásady. Aplikace se v centru softwaru nezobrazí jako k dispozici a uživatel nemůže aplikaci nainstalovat pomocí tohoto nasazení. Až tuto akci použijete k instalaci aplikace, uživatel ji může spustit a zobrazit stav instalace v centru softwaru.

- Váš uživatelský účet potřebuje následující oprávnění:

    - **Aplikace**: číst, schválit

    - **Kolekce**: číst, číst prostředek, upravit prostředek, zobrazit shromážděný soubor

    Tato oprávnění mají například předdefinované role **Správce aplikací** .

> [!TIP]
> V hierarchii počkejte, než se informace o aplikaci a nasazení replikují do primární lokality, ke které je cílový klient přiřazen.<!-- SCCMDocs#2113 -->

## <a name="process"></a>Proces

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte uzel **zařízení** . Vyberte cílové zařízení a pak na pásu karet vyberte akci **instalovat aplikaci** .

1. Vyberte ze seznamu jednu nebo více aplikací. V seznamu se zobrazí pouze aplikace, které již byly nasazeny s požadovaným nastavením.

Tato akce aktivuje instalaci vybraných předem nasazených aplikací na zařízení.

Chcete-li zobrazit stav žádosti o schválení, v pracovním prostoru **softwarová knihovna** rozbalte položku **Správa aplikací**a vyberte uzel **požadavky aplikace** .

V uzlu **nasazení** pracovního prostoru **monitorování** Sledujte instalaci aplikace stejně jako obvyklou.


## <a name="see-also"></a>Viz také

[Schválení aplikací](app-approval.md)
