---
title: Endpoint Protection definice malwaru
titleSuffix: Configuration Manager
description: Naučte se konfigurovat Configuration Manager aktualizace softwaru pro doručení aktualizací definic do klientských počítačů.
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3b9c4027-a98b-406b-935c-ccabcfe713df
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c0b734fe2a63373e8fd1af9abe77cde7f52b6824
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126081"
---
# <a name="use-configuration-manager-to-deliver-definition-updates"></a>Doručovat aktualizace definic pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager aktualizace softwaru můžete nakonfigurovat tak, aby automaticky poskytovaly aktualizace definic do klientských počítačů. Než začnete vytvářet pravidla automatického nasazení, nezapomeňte nakonfigurovat Configuration Manager aktualizace softwaru. Další informace najdete v tématu [Úvod do aktualizací softwaru](../../sum/understand/software-updates-introduction.md).

> [!NOTE]
> Tato procedura je specifická pro Endpoint Protection. Obecnější informace o pravidlech automatického nasazení najdete v tématu [automatické nasazení aktualizací softwaru](../../sum/deploy-use/automatically-deploy-software-updates.md).

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** . Rozbalte položku **aktualizace softwaru**a pak vyberte možnost **pravidla automatického nasazení**.

1. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte **vytvořit pravidlo automatického nasazení**.

1. Na stránce **Obecné** v **Průvodci vytvořením pravidla automatického nasazení**zadejte následující informace:

    - **Název:** Zadejte jedinečný název pravidla automatického nasazení.

    - **Kolekce**: vyberte kolekci zařízení, do které chcete nasadit aktualizace definic.

        > [!NOTE]
        > Aktualizace definic se nedají nasadit do kolekce uživatelů.

1. Vyberte **Přidat do existující skupiny aktualizací softwaru**.

1. **Po spuštění tohoto pravidla vyberte Povolit nasazení**.

1. Na stránce **nastavení nasazení** v průvodci pro **úroveň podrobností**vyberte **pouze chybové zprávy**.

    > [!NOTE]
    > Když vyberete **pouze chybové zprávy**, dojde k omezení počtu stavových zpráv, které nasazení definice odesílá. Tato konfigurace pomáhá snižovat zpracování CPU na serverech Configuration Manager.

1. Na stránce **aktualizace softwaru** :

    1. Vyberte filtr **aktualizace vlastností klasifikace** . V seznamu **kritéria hledání** vyberte **<položky, které chcete najít\>**.

        V okně **kritéria hledání** vyberte **aktualizace definic**a pak vyberte **OK**.

    1. Vyberte filtr vlastností **produktu** . V seznamu **kritéria hledání** vyberte **<položky, které chcete najít\>**.

        V okně **kritéria vyhledávání** vyberte možnost **System Center Endpoint Protection** pro Windows 8.1 a starší nebo **Windows Defender** pro Windows 10 a novější a pak vyberte **OK**.

    > [!NOTE]
    > Volitelně můžete odfiltrovat nahrazené aktualizace. Vyberte filtr **nahrazených** vlastností. V seznamu **kritéria hledání** vyberte **<položky, které chcete najít\>**. V okně **kritéria hledání** vyberte **ne**a pak vyberte **OK**.

1. Na stránce **Plán vyhodnocení** v průvodci vyberte **Spustit pravidlo po jakékoli synchronizaci bodu aktualizace softwaru**.

1. Na stránce **Plán nasazení** v průvodci konfigurujte následující nastavení:

    - **Čas na základě**: Pokud chcete, aby všichni klienti instalovali nejnovější definice ve stejnou dobu, vyberte možnost **UTC**. Skutečná doba instalace se bude lišit v rozmezí dvou hodin.

    - **Čas dostupnosti softwaru**: zadejte čas dostupnosti pro nasazení, které toto pravidlo vytvoří. Zadaný čas musí být aspoň hodinu po spuštění pravidla automatického nasazení. Tato konfigurace zajistí, aby měl obsah dost času na replikaci do distribučních bodů. Některé aktualizace definic můžou také obsahovat aktualizace antimalwarového stroje, které můžou do distribučních bodů putovat delší dobu.

    - **Konečný termín instalace:** Vyberte možnost **Co nejdříve**.

        > [!NOTE]
        > Konečné termíny aktualizace softwaru se liší v průběhu dvou hodin. Toto chování brání všem klientům v žádosti o aktualizaci ve stejnou dobu.

1. Na stránce **činnost koncového uživatele** průvodce v části **oznámení uživateli**vyberte možnost **Skrýt v nástroji Software Center a všech oznámeních**. V této konfiguraci se aktualizace definic tiše instalují.

1. V průvodci na stránce **balíček pro nasazení** vyberte existující balíček pro nasazení nebo vytvořte nový.

    > [!NOTE]
    > Zvažte umístění aktualizací definic do balíčku, který neobsahuje jiné aktualizace softwaru. Tato strategie zajistí menší velikost balíčku aktualizací definic, což umožňuje urychlit replikaci do distribučních bodů.

1. Pokud vytvoříte nový balíček pro nasazení, na stránce **distribuční body** v průvodci vyberte jeden nebo více distribučních bodů. Lokalita zkopíruje obsah tohoto balíčku do těchto distribučních bodů.

1. Na stránce **umístění pro stahování** vyberte možnost **stáhnout softwarové aktualizace z Internetu**.

1. Na stránce **Výběr jazyka** vyberte všechny jazykové verze aktualizací, které chcete stáhnout.

1. Na stránce **Nastavení stahování** vyberte chování při stahování nezbytných aktualizací softwaru.

1. Dokončete průvodce.

Ověřte, zda se v uzlu **pravidla automatického nasazení** konzoly Configuration Manager zobrazuje nové pravidlo.

> [!div class="nextstepaction"]
> [Vytvoření a nasazení antimalwarových zásad](endpoint-antimalware-policies.md)
