---
title: Konfigurace vzdáleného řízení
titleSuffix: Configuration Manager
description: Nastavte vzdálené řízení v Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 78f74a9659a011defd50e6ab0e9e1cfe85eec16b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076726"
---
# <a name="configuring-remote-control-in-configuration-manager"></a>Konfigurace vzdáleného řízení v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

 Tento postup popisuje konfiguraci výchozího nastavení klienta pro vzdálené řízení. Tato nastavení se vztahují na všechny počítače ve vaší hierarchii. Pokud chcete toto nastavení použít jenom pro některé počítače, přiřaďte do kolekce, která obsahuje tyto počítače, vlastní nastavení klienta zařízení. Další informace najdete v tématu [Konfigurace nastavení klienta](../../../../core/clients/deploy/configure-client-settings.md). 

Pokud chcete použít vzdálenou pomoc nebo vzdálenou plochu, musí být nainstalovaná a nakonfigurovaná na počítači, na kterém běží Konzola Configuration Manager. Další informace o instalaci a konfiguraci funkce Vzdálená pomoc nebo Vzdálená plocha najdete v dokumentaci k Windows.  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>Povolení vzdáleného řízení a konfigurace nastavení klienta  

1. V konzole Configuration Manager vyberte možnost **Správa** > **Nastavení** > klienta**výchozí nastavení klienta**.  

2. Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  

3. V dialogovém okně **výchozí** vyberte položku **vzdálené nástroje**.  

4. Nakonfigurujte nastavení klienta vzdálené řízení, Vzdálená pomoc a Vzdálená plocha. Seznam nastavení klienta vzdálených nástrojů, která můžete konfigurovat, najdete v tématu [Remote Tools](../../../../core/clients/deploy/about-client-settings.md#remote-tools).  

   Můžete změnit název společnosti, který se zobrazí v dialogovém okně **Vzdálené řízení ConfigMgr** konfigurováním hodnoty pro **Název organizace zobrazený v Centru softwaru** v nastavení klienta **Počítačový agent**.  

   Při příštím stažení zásad klienta se klientské počítače nakonfigurují tímto nastavením. Pokud chcete iniciovat načtení zásad pro jednoho klienta, přečtěte si téma [Správa klientů](../../../../core/clients/manage/manage-clients.md).  

#### <a name="enable-keyboard-translation"></a>Povolit překlad klávesnice

Ve výchozím nastavení Configuration Manager přenáší klíčovou pozici z umístění prohlížeče do umístění sdílejícího. To může představovat problém pro konfigurace klávesnice, které se liší od prohlížeče k sdílejícímu. Například prohlížeč s anglickou klávesnicí by měl napsat "A", ale Francouzská klávesnice sdílejícía poskytne "Q". Nyní máte možnost nakonfigurovat vzdálené řízení tak, aby se samotný znak přenesl z klávesnice prohlížeče na sdílející a co prohlížeč zamýšlí napsat, dorazí na sdílejícího.

Chcete-li zapnout překlad klávesnice, vyberte v **Configuration Manager vzdálené řízení**možnost **Akce**a vyberte možnost **Povolit překlad klávesnice** pro přenos pozice klíče.

> [!NOTE]
>
> Speciální klíče, například ~! # @ $%, nebudou přeloženy správně.


## <a name="keyboard-shortcuts-for-the-remote-control-viewer"></a>Klávesové zkratky pro prohlížeč vzdáleného řízení

|Klávesová zkratka|Popis|  
|-----------------------|-----------------|  
|Alt+Page Up|Přepne mezi spuštěnými programy zleva doprava.|  
|Alt+Page Down|Přepne mezi spuštěnými programy zprava doleva.|  
|Alt+Insert|Přepne mezi spuštěnými programy v pořadí, v jakém byly spuštěné.|  
|Alt+Home|Zobrazí nabídku **Start** .|  
|Ctrl+Alt+End|Zobrazí dialogové okno Zabezpečení systému Windows (Ctrl+Alt+Del).|  
|Alt+Delete|Zobrazí nabídku Windows.|  
|Ctrl+Alt+symbol mínus (na numerické klávesnici)|Zkopíruje aktivní okno místního počítače do schránky vzdáleného počítače.|  
|Ctrl+Alt+symbol plus (na numerické klávesnici)|Zkopíruje celou oblast okna místního počítače do schránky vzdáleného počítače.|  
