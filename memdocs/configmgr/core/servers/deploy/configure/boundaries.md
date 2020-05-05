---
title: Definovat hranice
titleSuffix: Configuration Manager
description: Zjistěte, jak definovat síťová umístění v intranetu, která můžou obsahovat zařízení, která chcete spravovat.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f53088843e0bf42a93c1d959255c7885b07dfe35
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721112"
---
# <a name="define-network-locations-as-boundaries-for-configuration-manager"></a>Definovat síťová umístění jako hranice pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Hranice Configuration Manager jsou umístění v síti obsahující zařízení, která chcete spravovat. Hranice, na které je zařízení zapnuté, je ekvivalentní lokalitě služby Active Directory nebo síťové IP adrese, která je identifikovaná Configuration Manager klientem, který je nainstalovaný v zařízení.
- Můžete ručně vytvořit jednotlivé hranice. Configuration Manager však nepodporuje přímou položku tuto nadsíť jako hranici. Místo toho použijte jako typ hranice rozsah IP adres.
- Metodu [zjišťování doménové struktury služby Active Directory](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) můžete nakonfigurovat tak, aby automaticky zjistila a vytvořila hranice pro každou podsíť protokolu IP a lokalitu služby Active Directory, kterou zjišťuje. Když funkce zjišťování doménové struktury služby Active Directory identifikuje tuto nadsíť, která je přiřazená k lokalitě služby Active Directory, Configuration Manager převede tuto nadsíť na hranici rozsahu IP adres.  

Pro zařízení není Neběžné používat IP adresu, o které správce Configuration Manager neví. Pokud je síťové umístění zařízení nejisté, potvrďte, co zařízení nahlásí jako své umístění pomocí příkazu **ipconfig** na zařízení.  

Když vytvoříte hranici, automaticky získá název podle typu a rozsahu hranice. Tento název není možné změnit. Místo toho můžete zadat popis, který vám usnadní identifikaci hranice v konzole Configuration Manager.  

Každá hranice je k dispozici pro každý web ve vaší hierarchii. Po vytvoření hranice můžete změnit její vlastnosti a provést následující akce:  
- Přidat hranici k jedné nebo k několika skupinám hranic.  
- Změnit typ nebo rozsah hranice.  
- Zobrazením hranic na kartě **Systémy lokality** zobrazíte servery systému lokality přiřazené k hranici (distribuční body, body migrace stavu a body správy).  

## <a name="to-create-a-boundary"></a>Postup při vytvoření hranice  

1.  V konzole Configuration Manager klikněte na **Správa** > **hranice** **Konfigurace** > hierarchie.  

2.  Na kartě **Domů** ve skupině **Vytvořit** klikněte na možnost **Vytvořit Boundary**.  

3.  Na kartě **Obecné** v dialogovém okně Vytvořit hranici můžete zadat přesný **Popis** a označit hranici popisným názvem nebo označením.  

4.  Vyberte **Typ** této hranice:  

    - Pokud zvolíte možnost **Podsíť protokolu IP**, musíte zadat **ID podsítě** této hranice.  
      > [!TIP]  
      > Můžete zadat parametry **Síť** a **Maska podsítě** a parametr **ID podsítě** bude zadán automaticky. Při uložení hranice bude uložena pouze hodnota ID podsítě.  

    - Jestliže zvolíte možnost **Lokalita služby Active Directory**, musíte **Procházet** k lokalitě služby Active Directory v místní doménové struktuře serveru lokality nebo ji zadat přímo.  
        
      - Když u hranice zadáte lokalitu služby Active Directory, bude hranice zahrnovat každou podsíť protokolu IP, která je členem dané lokality služby Active Directory. Pokud se konfigurace lokality služby Active Directory změní ve službě Active Directory, změní se také síťová umístění zahrnutá v této hranici.  

      - U čistě AzureAD klientů nefungují hranice lokalit služby Active Directory. Pokud dojde k místnímu roamingu, nespadají do žádné hranice, pokud jsou definované jenom pomocí lokalit služby Active Directory.

    - Zvolíte-li možnost **IPv6 – předpona**, musíte zadat parametr **Předpona** ve formátu předpony protokolu IPv6.  

    - Při zvolení možnosti **Rozsah IP adres**je nutné zadat parametry **Počáteční IP adresa** a **Koncová adresa IP** , jež budou zahrnovat část podsítě protokolu IP nebo několik podsítí protokolu IP.    

5.  Uložte novou hranici kliknutím na tlačítko **OK** .  

## <a name="to-configure-a-boundary"></a>Postup při konfiguraci hranice  

1.  V konzole Configuration Manager klikněte na **Správa** > **hranice** **Konfigurace** > hierarchie.  

2.  Vyberte hranici, kterou chcete upravit.  

3.  Na kartě **Domů** ve skupině **Vlastnosti** klikněte na možnost **Vlastnosti**.  

4.  V dialogovém okně **Vlastnosti** dané hranice lze na kartě **Obecné** upravit **Popis** nebo **Typ** hranice. Rovněž je možné změnit rozsah hranice úpravou síťových umístění této hranice. Například pro hranici lokality služby Active Directory lze zadat nový název lokality služby Active Directory.  

5.  Na kartě **Systémy lokality** lze zobrazit systémy lokalit, které jsou k této hranici přidruženy. Toto nastavení nelze změnit z vlastností hranice.  

    > [!TIP]  
    > Aby byl systémový server lokality uveden u hranice jako systém lokality, musí být tento systémový server lokality přiřazen jako systémový server lokality alespoň u jedné skupiny hranic zahrnující i tuto hranici. To se nastavuje na kartě **Odkazy** skupiny hranic.  

6.  Na kartě **Skupiny hranic** lze upravit členství této hranice ve skupině hranic:  

    - Chcete-li přidat tuto hranici do jedné nebo několika skupin hranic, klikněte na tlačítko **Přidat**, zaškrtněte políčko u jedné či několika skupin hranic a poté klikněte na tlačítko **OK**.  

    - Pokud chcete tuto hranici ze skupiny hranic odebrat, vyberte skupinu hranic a klikněte na tlačítko **Odebrat**.  

7.  Kliknutím na tlačítko **OK** zavřete vlastnosti hranice a uložte konfiguraci.  
