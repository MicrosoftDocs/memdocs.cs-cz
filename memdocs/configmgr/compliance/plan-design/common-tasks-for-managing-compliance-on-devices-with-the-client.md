---
title: Běžné úlohy správy dodržování předpisů
titleSuffix: Configuration Manager
description: Další informace o Configuration Manager nastavení dodržování předpisů najdete v některých běžných scénářích.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 5920229331bca8d2a47b0bf1ab663530ef63c51e
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240656"
---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-configuration-manager-client"></a>Běžné úlohy správy dodržování předpisů u zařízení s klientem Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

V tomto článku se seznámíte s používáním Configuration Manager nastavení dodržování předpisů, která vás provedou některými běžnými scénáři, se kterými se můžete setkat.  

 Pokud jste již obeznámeni s nastavením dodržování předpisů, najdete podrobné informace o všech funkcích, které používáte v [položkách konfigurace pro zařízení spravovaná pomocí klienta Configuration Manager](../../compliance/deploy-use/create-configuration-items.md).  

 Než začnete, přečtěte si téma [Začínáme s nastavením dodržování předpisů](../../compliance/get-started/get-started-with-compliance-settings.md) a seznamte se se základy nastavení dodržování předpisů. Přečtěte si téma [plánování a konfigurace nastavení dodržování předpisů](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) pro informace o nezbytných požadavcích.  

## <a name="general-information-for-each-scenario"></a>Obecné informace pro všechny scénáře  
 V každém scénáři vytvoříte položku konfigurace, která provede určitou úlohu. Chcete-li otevřít Průvodce vytvořením položky konfigurace a začít, proveďte následující kroky:  

1.  V konzole Configuration Manager vyberte **Assets and Compliance**  >  položky konfigurace**Nastavení dodržování předpisů**prostředky a kompatibilita  >  **Configuration Items**.  

1.  Na kartě **Domů** ve skupině **vytvořit** vyberte možnost **vytvořit položku konfigurace**.  

1.  Na stránce **Obecné** v Průvodci vytvořením položky konfigurace zobrazené na následujícím snímku obrazovky zadejte název a popis položky konfigurace. Pak zvolte odpovídající typ položky konfigurace pro každý scénář v tomto článku.  

     ![Stránka Obecné v Průvodci vytvořením položky konfigurace](../../mdm/deploy-use/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenario-disable-bluetooth-on-windows-10-devices"></a>Scénář: zakázání Bluetooth na zařízeních s Windows 10

 V tomto scénáři vaše bezpečnostní oddělení určilo, že funkce Bluetooth na zařízeních se dá použít k přenosu citlivých firemních informací mimo společnost. Nedávno jste upgradovali všechny počítače na Windows 10. Rozhodnete se na těchto zařízeních zakázat Bluetooth.  

1. Na stránce **Obecné** v Průvodci vytvořením položky konfigurace vyberte typ položky konfigurace **Windows 10** a pak vyberte **Další**.  

2. Na stránce **Podporované platformy** v průvodci vyberte všechny platformy Windows 10.  

3. Na stránce **nastavení zařízení** vyberte **zařízení**a pak vyberte **Další**.  

4. Na stránce **Zařízení** vyberte u položky **Bluetooth** možnost **Zakázáno**.  

5. Vyberte **Napravit neshodná nastavení** , abyste zajistili použití této změny na všech zařízeních s Windows 10.  

6. Dokončete průvodce pro vytvoření položky konfigurace.  

 Nyní můžete použít informace v tématu [běžné úlohy pro vytváření a nasazování standardních hodnot konfigurace s Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) článkem, které vám pomůžou nasadit konfiguraci, kterou jste vytvořili v zařízeních.  

## <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>Scénář: Opravení nesprávné hodnoty registru na stolních počítačích s Windows

> [!NOTE] 
> V počítačích Mac, na kterých běží klient Configuration Manager, máte dvě možnosti pro vyhodnocení dodržování předpisů:  
> - Vyhodnoťte soubor předvoleb systému Mac OS X (plist).
> - Použijte vlastní skript a vyhodnoťte výsledky vrácené tímto skriptem.  
>
>Další informace najdete v tématu [Vytvoření položek konfigurace pro zařízení Mac OS X spravovaná pomocí klienta Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md).  

 V tomto scénáři zjistíte, že důležitá obchodní aplikace neběží správně na některých spravovaných počítačích s Windows 8.1. Zjistíte, že je klíč registru s názvem **HKEY_LOCAL_MACHINE \Software\woodgrove\lob App\Configuration\Configuration1** na některých počítačích nastavený na hodnotu **0** . Aby obchodní aplikace běžela úspěšně, musí být tato hodnota nastavená na **1**.  

 V tomto postupu vytvoříte položku konfigurace, která sleduje a automaticky opraví všechny nesprávné hodnoty klíčů registru, které jsou nalezeny.  

1. Na stránce **Obecné** v Průvodci vytvořením položky konfigurace vyberte typ položky konfigurace **stolní počítače a servery Windows (vlastní)** a pak vyberte **Další**.  

2. Na stránce **podporované platformy** v průvodci vyberte možnost **Windows 8.1** (aby se zajistilo, že se položka konfigurace vztahuje pouze na ovlivněné počítače).  

3. Na stránce **Nastavení** vyberte možnost **nové** a vytvořte nové nastavení.  

4. Na kartě **Obecné** v dialogovém okně **vytvořit nastavení** nakonfigurujte tato nastavení:  

   -   **Název**  >  **Příklad nastavení**  

   -   **Typ nastavení**  >  **Hodnota registru**  

   -   **Datový typ**  >  **Celé číslo** (protože hodnota obsahuje jenom číslo)  

   -   **Podregistr**  >  **HKEY_LOCAL_MACHINE**  

   -   **Klíč**  >  **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

   -   **Hodnota**  >  **1** (požadovaná hodnota)  

5. Na kartě **pravidla shody** v dialogovém okně **vytvořit nastavení** vyberte **Nový**. V dialogovém okně **vytvořit pravidlo** nakonfigurujte tato nastavení:  

   -   **Název**  >  **Příklad pravidla**  

   -   **Vybraná nastavení** > ověří, jestli je vybrané nastavení **Příklad nastavení**.

   -   **Typ pravidla**  >  **Hodnota**  

   -   **Nastavení musí odpovídat následujícímu pravidlu** > ověřte, zda je název nastavení správný, a nakonfigurujte možnost, aby určovala, že se hodnota nastavení musí rovnat **1**.  

   -   **Napravit pravidla nesplňující požadavky** , je-li to podporováno > zaškrtněte toto políčko, aby se zajistilo, že Configuration Manager resetuje hodnotu klíče registru na správnou hodnotu, pokud je nesprávná.  

6. Dokončete průvodce pro vytvoření položky konfigurace.  

 Nyní můžete použít informace v článku [běžné úlohy pro vytváření a nasazování standardních hodnot konfigurace](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) , které vám pomůžou nasadit konfiguraci, kterou jste vytvořili v zařízeních.  

## <a name="next-steps"></a>Další kroky

[Vytvoření a nasazení standardních hodnot konfigurace](common-tasks-for-creating-and-deploying-configuration-baselines.md)
