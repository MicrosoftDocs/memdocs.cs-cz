---
title: Konfigurace stavu klienta
titleSuffix: Configuration Manager
description: V Configuration Manager vyberte nastavení stavu klienta.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5bb77e1e9f55919a03368d549946ee4dd1cda58a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713573"
---
# <a name="how-to-configure-client-status-in-configuration-manager"></a>Postup konfigurace stavu klienta v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Než budete moci monitorovat Configuration Manager stav klienta a opravit nalezené problémy, je nutné nakonfigurovat lokalitu tak, aby určovala parametry používané k označení klientů jako neaktivních, a nakonfigurovat možnosti, které vás upozorní, pokud aktivita klienta klesne pod určenou prahovou hodnotu. Můžete také zakázat možnost automaticky oprava všechny problémy, které najde stav klienta.  

##  <a name="to-configure-client-status"></a><a name="BKMK_1"></a>Konfigurace stavu klienta  

1.  V konzole Configuration Manager klikněte na **monitorování**.  

2.  V pracovním prostoru **monitorování** klikněte na **stav klienta**a pak na kartě **Domů** ve skupině **stav klienta** klikněte na **Nastavení stavu klienta**.  

3.  V dialogovém okně **Vlastnosti nastavení stavu klienta** zadejte následující hodnoty pro určení aktivity klienta:  

    > [!NOTE]  
    >  Pokud není splněno žádné nastavení, bude klient označen jako neaktivní.  

    -   **Požadavky na zásady klienta v průběhu následujících dnů:** Zadejte počet dnů od doby, kdy klient požádal o zásady. Aktuální hodnota činí **7** dní.  

    -   **Zjišťování prezenčního signálu v průběhu následujících dnů:** Zadejte počet dnů od doby, kdy klientský počítač odeslal do databáze lokality záznam zjišťování prezenčního signálu. Aktuální hodnota činí **7** dní.  

    -   **Inventář hardwaru v průběhu následujících dnů:** Zadejte počet dnů od doby, kdy klientský počítač odeslal do databáze lokality záznam inventáře hardwaru. Aktuální hodnota činí **7** dní.  

    -   **Inventář softwaru v průběhu následujících dnů:** Zadejte počet dnů od doby, kdy klientský počítač odeslal do databáze lokality záznam inventáře softwaru. Aktuální hodnota činí **7** dní.  

    -   **Stavové zprávy v průběhu následujících dnů:** Zadejte počet dnů od doby, kdy klientský počítač odeslal do databáze lokality stavové zprávy. Aktuální hodnota činí **7** dní.  

4.  V dialogovém okně **Vlastnosti nastavení stavu klienta** zadejte následující hodnotu, abyste zjistili, jak dlouho se uchovávají data historie stavu klienta:  

    -   **Uchovat historii stavu klienta po následující počet dnů:** Určete, jak dlouho má historie stavu klienta zůstat v databázi lokality. Výchozí hodnota je **31** dní.  

5.  Kliknutím na tlačítko **OK** uložte vlastnosti a zavřete dialogové okno **Vlastnosti nastavení stavu klienta** .  

##  <a name="to-configure-the-schedule-for-client-status"></a><a name="BKMK_Schedule"></a>Postup konfigurace plánu pro stav klienta  

1.  V konzole Configuration Manager klikněte na **monitorování**.  

2.  V pracovním prostoru **monitorování** klikněte na **stav klienta**a potom na kartě **Domů** ve skupině **stav klienta** klikněte na položku **naplánovat aktualizaci stavu klienta**.  

3.  V dialogovém okně **aktualizace stavu klienta naplánovat** nastavte interval, ve kterém chcete aktualizovat stav klienta, a klikněte na tlačítko OK.  

    > [!NOTE]  
    >  Když změníte plán aktualizací stavu klienta, aktualizace se projeví až po další plánované aktualizaci stavu klienta (pro dříve nakonfigurovaný plán).  

##  <a name="to-configure-alerts-for-client-status"></a><a name="BKMK_2"></a>Konfigurace výstrah pro stav klienta  

1. V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.  

2. V pracovním prostoru **Prostředky a kompatibilita** klikněte na možnost **Kolekce zařízení**.  

3. V seznamu **Kolekce zařízení** vyberte kolekci, pro kterou chcete nakonfigurovat výstrahy, a poté na kartě **Domů** ve skupině **Vlastnosti** klikněte na možnost **Vlastnosti**.  

   > [!NOTE]  
   >  Výstrahy nelze nakonfigurovat pro kolekce uživatelů.  

4. Na kartě **výstrahy** v dialogovém okně**vlastnosti** <em> &lt;názvu\>kolekce</em>klikněte na tlačítko **Přidat**.  

   > [!NOTE]  
   >  Karta **Výstrahy** je viditelná jen v případě, že role zabezpečení, k níž jste přidruženi, má oprávnění pro výstrahy.  

5. V dialogovém okně **Přidat nové výstrahy kolekce** vyberte výstrahy, jež mají být vygenerovány, když prahové hodnoty stavu klienta klesnou pod zadanou hodnotu, a poté klikněte na tlačítko **OK**.  

6. V seznamu **Podmínky** na kartě **Výstrahy** vyberte jednotlivé výstrahy stavu klienta a zadejte následující informace.  

   -   **Název výstrahy** – přijměte výchozí název nebo zadejte nový název výstrahy.  

   -   **Závažnost výstrahy** – v rozevíracím seznamu vyberte úroveň výstrahy, která se zobrazí v konzole Configuration Manager.  

   -   **Vyvolat výstrahu** – zadejte procento prahové hodnoty pro výstrahu.  

7. Kliknutím na tlačítko **OK** zavřete dialogové okno**vlastnosti** <em> &lt;názvu\>kolekce</em>.  

##  <a name="to-exclude-computers-from-automatic-remediation"></a><a name="BKMK_3"></a>Vyloučení počítačů z automatické nápravy  

1. Otevřete Editor registru v klientském počítači, pro který chcete zakázat automatickou nápravu.  

   > [!WARNING]  
   >  Pokud používáte Editor registru nesprávně, může dojít k vážným problémům, které by mohly vyžadovat přeinstalaci operačního systému. Společnost Microsoft nemůže zaručit, že budete schopni vyřešit problémy vzniklé z nesprávného použití Editoru registru. Editor registru používáte na vlastní nebezpečí.  

2. Přejděte na **HKEY_LOCAL_MACHINE \software\microsoft\ccm\ccmeval\notifyonly**.  

3. Pro tento klíč registru zadejte jednu z následujících hodnot:  

   -   **True** – klientský počítač nebude automaticky opravovat žádné nalezené problémy. V pracovním prostoru **monitorování** však budete upozorněni na případné potíže s tímto klientem.  

   -   **False** – klientský počítač bude automaticky opravovat problémy při jejich nalezení a v pracovním prostoru **monitorování** budete upozorněni. Toto je výchozí nastavení.  

4. Zavřete editor registru.  

   Můžete taky nainstalovat klienty pomocí vlastnosti instalace CCMSetup **NotifyOnly** , aby se vyloučily z automatické nápravy. Další informace o této vlastnosti instalace klienta najdete v tématu [informace o vlastnostech instalace klienta](../../../core/clients/deploy/about-client-installation-properties.md).  
