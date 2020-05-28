---
title: Konfigurace výstrah Endpoint Protection
titleSuffix: Configuration Manager
description: Naučte se konfigurovat výstrahy Endpoint Protection v Configuration Manager.
ms.date: 03/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f504de3e-4caf-455c-80d7-a63f13f4c5d9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5b44147006a9ae4d38d2275a4515d71d61eec55c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074856"
---
#  <a name="configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Konfigurace upozornění pro Endpoint Protection v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

 Ve službě Microsoft Configuration Manager můžete nakonfigurovat výstrahy Endpoint Protection, které upozorní správce na to, že v hierarchii dojde k určitým událostem, jako je infekce malwaru. Oznámení se zobrazují na řídicím panelu Endpoint Protection v konzole Configuration Manager v uzlu **výstrahy** v pracovním prostoru **monitorování** nebo je lze zasílat e-mailem určeným uživatelům.

 Pomocí následujících kroků a doplňkových postupů v tomto tématu můžete konfigurovat výstrahy pro Endpoint Protection v Configuration Manager.

> [!IMPORTANT]
>  Abyste mohli konfigurovat výstrahy Endpoint Protection, musíte mít oprávnění **vyhovět zabezpečení** pro kolekce.

## <a name="steps-to-configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Postup konfigurace výstrah pro Endpoint Protection v Configuration Manager

1.  V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.

2.  V pracovním prostoru **Prostředky a kompatibilita** klikněte na možnost **Kolekce zařízení**.

3.  V seznamu **Kolekce zařízení** vyberte kolekci, pro kterou chcete nakonfigurovat výstrahy, a potom na kartě **Domů** ve skupině **Vlastnosti** klikněte na **Vlastnosti**.

    > [!NOTE]
    >  Výstrahy nelze nakonfigurovat pro kolekce uživatelů.

4.  Na kartě **výstrahy** v dialogovém okně **vlastnosti** _názvu \> kolekce<_ vyberte možnost **Zobrazit tuto kolekci na řídicím panelu Endpoint Protection** , pokud chcete zobrazit podrobnosti o antimalwarových operacích pro tuto kolekci v pracovním prostoru **monitorování** konzoly Configuration Manager.

    > [!NOTE]
    >  Pro kolekci **Všechny systémy** není tato možnost dostupná.

5.  Na kartě **výstrahy** v dialogovém okně **vlastnosti** _názvu \> kolekce<_ klikněte na **Přidat**.

6.  V dialogovém okně **Přidat nové výstrahy kolekce** v části **Generovat výstrahu, když platí tyto podmínky** vyberte výstrahy, které má Configuration Manager generovat při výskytu zadaných událostí Endpoint Protection, a pak klikněte na **OK**.

7.  V seznamu **podmínky** na kartě **výstrahy** vyberte jednotlivé výstrahy Endpoint Protection a pak zadejte následující informace:

    -   **Název výstrahy** – přijměte výchozí název nebo zadejte nový název výstrahy.

    -   **Závažnost výstrahy** – v seznamu vyberte úroveň výstrahy, která se má zobrazit v konzole Configuration Manager.

8.  V závislosti na vybrané výstraze zadejte následující další informace:

    -   **Detekce malwaru** – Tato výstraha se vygeneruje, pokud se na jakémkoli počítači v kolekci, kterou sledujete, zjistí malware. **Prahová hodnota detekce malwaru** Určuje úrovně detekce malwaru, na kterých se vygenerovala Tato výstraha:

        -   **Vysoká – všechny detekce** – výstraha se vygeneruje, když se v zadané kolekci nachází jeden nebo víc počítačů, u kterých se zjistí malware, a to bez ohledu na to, jakou akci klient Endpoint Protection trvá.

        -   **Střední-zjištěná akce, která čeká na vyřízení** – výstraha se vygeneruje, když se v zadané kolekci nachází jeden nebo víc počítačů, u kterých se zjistí malware, a musíte ručně odebrat malware.

        -   **Nízká-nalezen, stále aktivní** – výstraha se vygeneruje, když je v zadané kolekci aspoň jeden počítač, u kterého se malware zjistí a je pořád aktivní.

    -   **Šíření malwaru** – Tato výstraha se vygeneruje, pokud je v zadaném procentu v kolekci, kterou sledujete, zjištěn malware.

        -   **Procento počítačů se zjištěným malwarem** – výstraha se vygeneruje, když procento počítačů s malwarem zjištěným v kolekci překročí zadané procento. Zadejte procento od **1** do **99**.

            > [!NOTE]
            >  Procentuální hodnota je založena na počtu počítačů v kolekci, ale nezahrnuje počítače, které nemají nainstalovaného klienta Configuration Manager. Zahrnuje počítače, na kterých ještě není nainstalovaný klient Endpoint Protection.

    -   **Opakované zjištění malwaru** – Tato výstraha se vygeneruje, pokud je v počítačích v kolekci, kterou sledujete, zjištěn konkrétní malware větší než zadaný počet hodin. Ke konfiguraci této výstrahy zadejte tyto informace:

        -   **Počet zjištění malwaru:** Výstraha se vygeneruje, když se stejný malware zjistí na počítačích v kolekci víckrát, než je zadaný počet. Zadejte číslo od **2** do **32**.

        -   **Interval pro zjišťování (hodin):** Zadejte interval pro zjišťování (v hodinách), ve kterém musí dojít k zadanému počtu zjištění malwaru. Zadejte číslo od **1** do **168**.

    -   **Detekce více instancí malwaru** – Tato výstraha se vygeneruje, pokud se během zadaného počtu hodin v počítačích v kolekci, kterou sledujete, zjistí více než zadaný počet typů malwaru. Ke konfiguraci této výstrahy zadejte tyto informace:

        -   **Počet typů zjištěného malwaru:** Výstraha se vygeneruje, když se na počítačích v kolekci zjistí zadaný počet různých typů malwaru. Zadejte číslo od **2** do **32**.

        -   **Interval pro zjišťování (hodiny):** Zadejte interval zjišťování (v hodinách), ve kterém se musí objevit počet zjištění malwaru. Zadejte číslo od **1** do **168**.

9. Kliknutím na tlačítko **OK** zavřete dialogové okno **vlastnosti** _ \> názvu kolekce<_ .  

## <a name="alert-for-outdated-malware-client"></a>Výstraha pro zastaralého klienta malwaru

Od verze Configuration Manager 1702 můžete nakonfigurovat výstrahu, aby se zajistilo, že Endpoint Protection klienti nebudou zastaralí. Z libovolné kolekce zařízení teď můžete do seznamu přidat sloupce pro následující atributy **verze antimalwarového klienta** a **stav nasazení Endpoint Protection**. V konzole nástroje přejděte například na **prostředky a kompatibilita**  >  **Přehled**  >  **kolekce zařízení**  >  **všechny počítače a klienti serveru**. Klikněte pravým tlačítkem na záhlaví sloupce a vyberte tyto sloupce, které chcete přidat. Chcete-li zjistit výstrahu, zobrazte **výstrahy** v pracovním prostoru **monitorování** . Pokud je na více než 20% spravovaných klientů spuštěná verze antimalwarového softwaru s vypršenou platností, zobrazí se výstraha verze antimalwarového klienta je zastaralá. Tato výstraha se nezobrazuje **Monitoring**na  >  kartě**Přehled** monitorování. Chcete-li aktualizovat antimalwarové klienty s vypršenou platností, povolte aktualizace softwaru pro klienty antimalwaru.

Chcete-li nakonfigurovat procento, ve kterém je výstraha vygenerována, rozbalte položku **sledování**  >  **výstrahy**  >  **všechny výstrahy**, dvakrát klikněte na **antimalwarové klienty zastaralé** a upravte **výstrahu vyvolat, pokud procento spravovaných klientů s neaktuální verzí antimalwarového klienta je větší než** možnost.

> [!div class="button"]
> [Další krok >](endpoint-definition-updates.md)
> 
> [!div class="button"]
> [Zpět >](endpoint-protection-site-role.md)
