---
title: Správce přenosu balíčků
titleSuffix: Configuration Manager
description: Pochopení způsobu, jakým správce přenosu balíčků v Configuration Manager přenáší obsah ze serveru lokality do vzdálených distribučních bodů.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3359f254-dd48-42b7-9eab-c92a3417e3fb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b450c45342793b89d41a2d96b8a7340939899093
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722449"
---
# <a name="package-transfer-manager-in-configuration-manager"></a>Správce přenosu balíčků v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

V Configuration Manager lokalitě je správcem přenosu balíčků součást služby SMS_Executive, která spravuje přenos obsahu z počítače serveru lokality do vzdálených distribučních bodů v lokalitě. (Vzdálený distribuční bod je jeden, který se nenachází na počítači serveru lokality.) Správce přenosu balíčků nepodporuje konfigurace správcem, ale princip jeho fungování vám může pomoci při plánování infrastruktury správy obsahu. Můžete vám taky vyřešit problémy s distribucí obsahu.


Když distribuujete obsah do jednoho nebo více vzdálených distribučních bodů v lokalitě, **Správce distribuce** vytvoří úlohu přenosu obsahu. Pak upozorní správce přenosu balíčků na primárních a sekundárních serverech lokalit, aby přenesl obsah do vzdálených distribučních bodů.

 Správce přenosu balíčků protokoluje své akce do souboru **Pkgxfermgr. log** na serveru lokality. Soubor protokolu je jediné místo, kde můžete zobrazit aktivity správce přenosu balíčků.  

> [!NOTE]  
>  V předchozích verzích Configuration Manager spravuje správce distribuce přenos obsahu do vzdáleného distribučního bodu. Správce distribuce také spravuje přenos obsahu mezi lokalitami. Správce distribuce v Configuration Manager nadále spravuje přenos obsahu mezi dvěma lokalitami. Správce přenosu balíčků teď ale spravuje přenos obsahu do velkého počtu distribučních bodů. To pomáhá zvýšit celkový výkon nasazení obsahu mezi lokalitami i distribučními body v rámci lokality.  

Pro přenos obsahu do standardního distribučního bodu funguje správce přenosu balíčků stejně jako správce distribuce funguje v předchozích verzích Configuration Manager. To znamená, že aktivně spravuje přenos souborů do každého vzdáleného distribučního bodu. Pokud však chcete distribuovat obsah do distribučního bodu pro vyžádání obsahu, správce přenosu balíčků upozorní distribuční bod pro vyžádání obsahu, že obsah je k dispozici. Distribuční bod pro vyžádání obsahu pak převezme proces přenosu.  

Následující informace popisují, jak správce přenosu balíčků spravuje přenos obsahu do standardních distribučních bodů a do distribučních bodů nakonfigurovaných jako distribuční body pro vyžádání obsahu:
1.  **Správce nasadí obsah do jednoho nebo více distribučních bodů v lokalitě.**  

    -   **Standardní distribuční bod:** Správce distribuce vytvoří úlohu přenosu obsahu pro tento obsah.  

    -   **Distribuční bod pro vyžádání obsahu:** Správce distribuce vytvoří úlohu přenosu obsahu pro tento obsah.  

2.  **Správce distribuce spouští předběžné kontroly.**  

    -   **Standardní distribuční bod:** Správce distribuce spustí základní kontrolu, aby potvrdil, že každý distribuční bod je připraven přijmout obsah. Po této kontrole správce distribuce upozorní správce přenosu balíčků, aby zahájil přenos obsahu do distribučního bodu.  

    -   **Distribuční bod pro vyžádání obsahu:** Správce distribuce spustí správce přenosu balíčků, který poté oznámí distribučnímu bodu pro vyžádání obsahu, že je k dispozici nová úloha přenosu obsahu. Správce distribuce nekontroluje stav vzdálených distribučních bodů, které jsou distribučními body pro vyžádání obsahu, protože každý distribuční bod pro vyžádání obsahu spravuje vlastní přenos obsahu.  

3.  **Správce přenosu balíčků připraví přenos obsahu.**  

    -   **Standardní distribuční bod:** Správce přenosu balíčků prověřuje ukládání obsahu jediné instance každého zadaného vzdáleného distribučního bodu. Účelem této funkce je identifikovat všechny soubory, které jsou již v tomto distribučním bodě. Pak správce přenosu balíčků zařadí do fronty pro přenos pouze těch souborů, které ještě nejsou přítomné.  

        > [!NOTE]  
        >  Chcete-li zkopírovat každý soubor v distribuci do distribučního bodu, i když jsou soubory již přítomny v ukládání jediné instance distribučního bodu, použijte akci znovu **distribuovat** pro obsah.  

    -   **Distribuční bod pro vyžádání obsahu:** Pro každý distribuční bod pro vyžádání obsahu v distribuci zkontroluje správce přenosu balíčků zdrojové distribuční body distribučních bodů pro vyžádání obsahu, aby bylo možné potvrdit, zda je obsah k dispozici.  

        -   Pokud je obsah k dispozici alespoň v jednom zdrojovém distribučním bodě, správce přenosu balíčků pošle oznámení do tohoto distribučního bodu pro vyžádání obsahu. Oznámení směruje tento distribuční bod za účelem zahájení procesu přenosu obsahu. Oznámení zahrnuje názvy souborů a velikosti, atributy a hodnoty hash.  

        -   Pokud obsah ještě není k dispozici, správce přenosu balíčku nepošle oznámení do distribučního bodu. Místo toho opakuje kontrolu každých 20 minut, dokud nebude obsah k dispozici. Až bude obsah k dispozici, správce přenosu balíčků odešle oznámení do tohoto distribučního bodu pro vyžádání obsahu.  

        > [!NOTE]  
        >  Aby distribuční bod pro vyžádání obsahu kopíroval každý soubor v distribuci do distribučního bodu, a to i v případě, že jsou soubory již přítomny v ukládání jediné instance distribučního bodu pro vyžádání obsahu, použijte pro obsah akci znovu **distribuovat** .  

4.  **Obsah začíná přenosem.**  

    -   **Standardní distribuční bod:** Správce přenosu balíčků zkopíruje soubory do každého vzdáleného distribučního bodu. Během přenosu do standardního distribučního bodu:  

        -   Ve výchozím nastavení může správce přenosu balíčků současně zpracovávat tři jedinečné balíčky a paralelně je distribuovat do pěti distribučních bodů. Souhrnně se nazývají **Nastavení souběžné distribuce**. Chcete-li nastavit souběžnou distribuci, v části **vlastnosti součásti distribuce softwaru** pro každou lokalitu nástroje přejdete na kartu **Obecné** .  

        -   Správce přenosu balíčků používá pro účely přenosu obsahu do tohoto distribučního bodu konfigurace plánování a šířky pásma sítě v každém distribučním bodě. Chcete-li nakonfigurovat tato nastavení, přejděte ve **vlastnostech** každého vzdáleného distribučního bodu na kartu **plány** a **omezení přenosové rychlosti** . Další informace najdete v tématu [Správa obsahu a infrastruktury obsahu pro Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    -   **Distribuční bod pro vyžádání obsahu:** Když distribuční bod pro vyžádání obsahu obdrží soubor oznámení, distribuční bod zahájí proces přenosu obsahu. Proces přenosu se spouští nezávisle na každém distribučním bodu pro vyžádání obsahu:  

        1.   Distribuce pro vyžádání obsahu identifikuje soubory v distribuci obsahu, které ještě nejsou v úložišti jediné instance, a připraví stažení tohoto obsahu z jednoho ze svých zdrojových distribučních bodů.  

        2.   Dále bude distribuční bod pro vyžádání obsahu kontrolovat u každého ze zdrojových distribučních bodů v pořadí, dokud nenajde zdrojový distribuční bod s dostupným obsahem. Když distribuční bod pro vyžádání obsahu identifikuje zdrojový distribuční bod s obsahem, zahájí stahování tohoto obsahu.  

        > [!NOTE]  
        >  Proces stažení obsahu distribučním bodem pro vyžádání obsahu je stejný jako používaný klienty Configuration Manager. Pro přenos obsahu pomocí distribučního bodu pro vyžádání obsahu se nepoužijí nastavení souběžného přenosu. Možnosti plánování a omezování, které nakonfigurujete pro standardní distribuční body, se nepoužívají buď.  

5.  **Přenos obsahu je dokončený.**  

    -   **Standardní distribuční bod:** Až správce přenosu balíčků dokončí přenos souborů do každého určeného vzdáleného distribučního bodu, ověří hodnotu hash obsahu v distribučním bodě. Pak oznámí správci distribuce, že distribuce je dokončena.  

    -   **Distribuční bod pro vyžádání obsahu:** Poté, co distribuční bod pro vyžádání obsahu dokončí stahování obsahu, ověří distribuční bod hodnotu hash obsahu. Poté odešle stavovou zprávu do bodu správy lokality, aby označovala úspěch. Pokud po 60 minutách není tento stav přijatý, správce přenosu balíčků se znovu probudí. Kontroluje s distribučním bodem pro vyžádání obsahu, aby potvrdil, zda distribuční bod pro vyžádání obsahu stáhl obsah. Pokud probíhá stahování obsahu, správce přenosu balíčku přejde do režimu spánku pro jiné 60 minut, než se znovu vrátí s distribučním bodem pro vyžádání obsahu. Cyklus pokračuje, dokud distribuční bod pro vyžádání obsahu nedokončí přenos obsahu.  
