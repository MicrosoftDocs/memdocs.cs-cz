---
title: Vyloučit upgrady klientů pro Windows
titleSuffix: Configuration Manager
description: Přečtěte si, jak vyloučit klienty se systémem Windows z části získání upgradu v Configuration Manager.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 58a7741bb628a0c8fb346c8f61b446301b138d80
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715414"
---
# <a name="how-to-exclude-clients-from-upgrade-in-configuration-manager"></a>Jak vyloučit klienty z upgradu v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Můžete vyloučit kolekci klientů z automatické instalace aktualizovaných verzí klientů. Toto vyloučení použijte pro kolekci počítačů, které při upgradu klienta vyžadují větší péči. Klient, který je ve vyloučené kolekci, ignoruje požadavky na instalaci aktualizovaného klientského softwaru.

Toto vyloučení platí pro následující metody:

- Automatický upgrade
- Upgrade na základě aktualizace softwaru
- Přihlašovací skripty
- Zásady skupiny

> [!NOTE]
> I když uživatelské rozhraní uvádí, že klienti nebudou upgradovat prostřednictvím žádné metody, můžete použít dvě metody, pomocí kterých můžete tato nastavení přepsat. K přepsání této konfigurace použijte nabízenou nebo ruční instalaci klienta. Další informace najdete v tématu [Postup upgradu vyloučeného klienta](#bkmk_override).

## <a name="configure-exclusion"></a><a name="bkmk_exclude"></a>Konfigurace vyloučení

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** . Rozbalte položku **Konfigurace lokality**, vyberte uzel **lokality** a pak na pásu karet vyberte **Nastavení hierarchie** .

2. Přepněte na kartu **upgrade klienta** .

3. Vyberte možnost **vyloučení zadaných klientů z upgradu**. Pak vyberte **kolekci vyloučení** , kterou chcete vyloučit. Pro vyloučení můžete vybrat jenom jednu kolekci.

4. Kliknutím na **tlačítko OK** zavřete a uložte konfiguraci.

![Nastavení pro automatické vyloučení upgradu](media/automatic_upgrade_exclusion.png)

Po klientech ve vyloučené zásadě aktualizace se aktualizace klienta neinstalují automaticky. Další informace najdete v tématu [Postup upgradu klientů pro počítače se systémem Windows](upgrade-clients-for-windows-computers.md).

> [!NOTE]
> Vyloučení klienti si pořád stahují a spouštějí CCMSetup, ale neupgradují.

Když odeberete klienta z kolekce Exclude, neprovede se automaticky upgrade na další cyklus automatického upgradu.

## <a name="how-to-upgrade-an-excluded-client"></a><a name="bkmk_override"></a>Postup upgradu vyloučeného klienta

Pokud je zařízení členem kolekce, kterou jste vyloučili z upgradu, můžete klienta upgradovat pomocí jedné z následujících metod:

- **Klientská nabízená instalace**: služba CCMSetup umožňuje klientskou nabízenou instalaci, protože se jedná o přímý záměr. Tato metoda umožňuje upgrade klienta bez jeho odebrání z kolekce nebo odebrání celé kolekce z vyloučení.

- **Ruční instalace klienta**: k ručnímu upgradu vyloučeného klienta použijte následující parametr příkazového řádku CCMSetup: **/IgnoreSkipUpgrade**

    Pokud se pokusíte ručně upgradovat klienta, který je členem vyloučené kolekce, a nepoužívat tento parametr, klient se neupgraduje. Další informace najdete v tématu [Ruční instalace klientů Configuration Manager](../../deploy/deploy-clients-to-windows-computers.md#BKMK_Manual).

## <a name="see-also"></a>Viz také

- [Upgradujte klienty.](upgrade-clients.md)

- [Postup nasazení klientů na počítače s Windows](../../deploy/deploy-clients-to-windows-computers.md)

- [Klient s rozšířenou vzájemnou funkční spoluprací](../../../understand/interoperability-client.md)
