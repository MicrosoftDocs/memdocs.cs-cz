---
title: Konfigurace řízení spotřeby
titleSuffix: Configuration Manager
description: Nastavte řízení spotřeby v Configuration Manager.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3146c753e2d84001c162c653cc09af654e6a170a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715239"
---
# <a name="configure-power-management-in-configuration-manager"></a>Konfigurace řízení spotřeby v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek vysvětluje, jak nastavit řízení spotřeby v Configuration Manager.

## <a name="enable-and-configure-client-settings"></a>Povolení a konfigurace nastavení klienta

Tento postup nakonfiguruje *výchozí nastavení klienta* pro řízení spotřeby. Platí pro všechny počítače ve vaší hierarchii.

Pokud chcete tato nastavení použít jenom pro některé počítače, vytvořte *vlastní nastavení klienta zařízení*. Pak ji přiřaďte ke kolekci, která obsahuje počítače pro řízení spotřeby. Další informace najdete v tématu [Konfigurace nastavení klienta](../../deploy/configure-client-settings.md).  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , vyberte uzel **nastavení klienta** a vyberte **výchozí nastavení klienta**.

1. Na kartě **Domů** na pásu karet ve skupině **vlastnosti** vyberte možnost **vlastnosti**.  

1. Vyberte skupinu **řízení spotřeby** .  

1. Povolením nastavení klienta **povolíte řízení spotřeby zařízení**.

1. Nakonfigurujte další nastavení klienta, která požadujete. Další informace najdete v tématu [o nastavení klienta – řízení spotřeby](../../deploy/about-client-settings.md#power-management).  

Klienti konfigurují tato nastavení při příštím stažení zásad klienta. Pokud chcete iniciovat načtení zásad pro jednoho klienta, přečtěte si téma [Správa klientů](../manage-clients.md#BKMK_PolicyRetrieval).  

## <a name="exclude-computers"></a>Vyloučit počítače

Vybrané kolekce počítačů můžete vyřadit z řízení spotřeby. Pokud je počítač členem *jakékoli* kolekce, kterou vyloučíte z nastavení řízení spotřeby, nepoužije tento počítač nastavení řízení spotřeby. Toto chování platí i v případě, že je členem jiné kolekce, která nastavení řízení spotřeby používá.  

Počítače můžete chtít z řízení spotřeby vyloučit z následujících důvodů:  

- Vaše pracovní procesy vyžadují nepřetržitě zapnuté počítače.  

- Máte kontrolní kolekci počítačů, u kterých nechcete používat nastavení řízení spotřeby.  

- Některé z počítačů nejsou schopné použít nastavení řízení spotřeby.  

- Chcete z řízení spotřeby vyloučit počítače se systémem Windows Server.  

> [!NOTE]  
> Pokud nakonfigurujete nastavení klienta tak, aby **umožňovalo uživatelům vyloučit jejich zařízení z řízení spotřeby**, uživatelé mohou vyloučit své počítače z řízení spotřeby pomocí centra softwaru.  

Pokud chcete zjistit, které počítače jsou vyloučené z řízení spotřeby, spusťte sestavu **vyloučené počítače**. Další informace o této sestavě najdete v tématu [monitorování a plánování řízení spotřeby](monitor-and-plan-for-power-management.md#BKMK_Excluded).  

> [!IMPORTANT]  
> Vyloučení počítače z řízení spotřeby způsobí, že všechna nastavení napájení se vrátí na původní hodnoty. Není možné vrátit na původní hodnoty jenom jednotlivá nastavení řízení spotřeby.  

### <a name="how-to-exclude-a-collection-of-computers-from-power-management"></a>Vyloučení kolekce počítačů z řízení spotřeby  

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte uzel **kolekce zařízení** .  

1. Vyberte kolekci, kterou chcete vyloučit z řízení spotřeby. Na kartě **Domů** na pásu karet ve skupině **vlastnosti** vyberte možnost **vlastnosti**.  

1. Přepněte na kartu **řízení spotřeby** a v **počítačích v této kolekci vyberte nikdy nepoužívat nastavení řízení spotřeby**.  

## <a name="next-steps"></a>Další kroky

[Vytvoření a použití schémat napájení](create-and-apply-power-plans.md)

[Postupy pro monitorování a plánování řízení spotřeby](monitor-and-plan-for-power-management.md)
