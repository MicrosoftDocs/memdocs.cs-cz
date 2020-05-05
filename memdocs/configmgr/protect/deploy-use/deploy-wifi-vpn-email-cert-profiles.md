---
title: Nasazování profilů přístupu k prostředkům
titleSuffix: Configuration Manager
description: Naučte se nasazovat profily sítě Wi-Fi, VPN a certifikátů v Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0272c50429973cc3e15c295303b91593075ebe01
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724514"
---
# <a name="deploy-resource-access-profiles-in-configuration-manager"></a>Nasazení profilů přístupu k prostředkům v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Po vytvoření jednoho z následujících profilů přístupu k prostředkům ho nasaďte do jedné nebo více kolekcí:

- [Wi-Fi](create-wifi-profiles.md)
- [VPN](create-vpn-profiles.md)
- [Certifikát](create-certificate-profiles.md)

Když nasadíte tyto profily, zadáte cílovou kolekci a určíte, jak často bude klient vyhodnocovat kompatibilitu s profilem.  

## <a name="deploy-a-profile"></a>Nasazení profilu

1. V konzole Configuration Manager přejdete do pracovního prostoru **prostředky a kompatibilita** . Rozbalte **Nastavení dodržování předpisů**, rozbalte **přístup k prostředkům společnosti**a pak zvolte vhodný uzel profilu. Například profily sítě **Wi-Fi**.

1. V seznamu profilů vyberte profil, který chcete nasadit. Pak na kartě **Domů** na pásu karet ve skupině **nasazení** vyberte **nasadit**.  

1. V okně Nasadit profil zadejte následující informace:  

    - **Kolekce**: vyberte kolekci, do které chcete nasadit profil.

    - **Generovat upozornění**: tuto možnost povolte, pokud chcete nakonfigurovat výstrahu. Lokalita tuto výstrahu vygeneruje, pokud je kompatibilní s profilem nižší než zadané procento podle zadaného data a času. Můžete také vybrat, zda chcete odeslat výstrahu System Center Operations Manager.

    - **Náhodné zpoždění (hodiny)**: pro profily certifikátů, které obsahují nastavení Simple Certificate ENROLLMENT Protocol (SCEP), zadejte zpoždění, aby nedocházelo k nadměrnému zpracování v rámci služby zápisu síťových zařízení (NDES). Výchozí hodnota je `64` hodiny.  

    - **Zadejte plán vyhodnocení shody pro tuto... Profil**: Určete, jak často má klient vyhodnotit dodržování předpisů pro tento profil. Vyberte **jednoduchý plán** nebo nakonfigurujte **vlastní plán**. Ve výchozím nastavení je jednoduchý plán jednou `12` za hodinu.

1. Výběrem **OK** zavřete okno a vytvořte nasazení.

## <a name="delete-a-deployment"></a>Odstranění nasazení

Pokud chcete nasazení odstranit, vyberte ho ze seznamu. V podokně podrobností přepněte na kartu **nasazení** . Vyberte nasazení a pak na pásu karet na kartě **nasazení** vyberte **Odstranit**.

> [!IMPORTANT]
> Když odeberete nasazení profilu sítě VPN, Configuration Manager neodebere profil sítě VPN ze systému Windows. Pokud chcete odebrat profil ze zařízení, ručně ho odeberte.

## <a name="next-steps"></a>Další kroky

[Monitorování profilů sítě Wi-Fi a VPN](monitor-wifi-email-vpn-profiles.md)

[Monitorování profilů certifikátů](monitor-certificate-profiles.md)
