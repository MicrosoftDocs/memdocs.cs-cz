---
title: 'Vytvoření položek konfigurace pro Mac spravované na straně klienta '
titleSuffix: Configuration Manager
description: Pomocí položky konfigurace Configuration Manager Mac OS X můžete spravovat nastavení pro Mac OS X zařízení.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 722d5bf5-bedc-4dfc-b324-6eeb773874e9
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 9323fc3c1203d20c77af1f2fd27cee0a377e8d68
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240078"
---
# <a name="create-configuration-items-for-mac-os-x-devices"></a>Vytvoření položek konfigurace pro zařízení Mac OS X
Pomocí položky konfigurace Configuration Manager **Mac OS X (vlastní)** můžete spravovat nastavení pro Mac OS X zařízení, která spravuje klient Configuration Manager.  
  
Mac OS X operační systém používá k ukládání nastavení aplikace soubory seznamu vlastností (. plist). Použijte nastavení dodržování předpisů k vyhodnocení a nápravě nastavení v souboru seznamu vlastností. Nastavení Mac OS X můžete spravovat i tak, že napíšete skript prostředí, který vrátí hodnotu, kterou můžete vyhodnotit a opravit pro dodržování předpisů.  
  
## <a name="create-a-custom-mac-os-x-configuration-item"></a>Vytvoření vlastní položky konfigurace Mac OS X  
  
1. V konzole Configuration Manager vyberte **prostředky a kompatibilita**.  
  
2. V pracovním prostoru **prostředky a kompatibilita** rozbalte **Nastavení dodržování předpisů**a pak vyberte **položky konfigurace**.  
  
3. Na kartě **Domů** ve skupině **vytvořit** vyberte možnost **vytvořit položku konfigurace**.  
  
4. Na stránce **Obecné** v průvodci **vytvořením položky konfigurace** zadejte název a volitelný popis položky konfigurace.  
  
5. V části **Zadejte typ položky konfigurace, který chcete vytvořit** vyberte **Mac OS X (vlastní)**.  
  
6. Pokud vytvoříte a přiřadíte kategorie, které vám pomůžou při hledání a filtrování položek konfigurace v konzole Configuration Manager, vyberte **kategorie**.  
  
7. Na stránce průvodce **Podporované platformy** vyberte konkrétní verze Mac OS X, které vyhodnotí položku konfigurace.  
  
8. Na stránce **Nastavení** v průvodci přidejte nová nastavení, která se vyhodnocují pro dodržování předpisů na počítačích Mac. Výběrem **nové** otevřete dialogové okno **vytvořit nastavení** .  
  
9. V dialogovém okně **Vytvořit nastavení** zadejte jedinečný název a popis nastavení.  
  
10. Zvolte **Typ nastavení** , který chcete, a potom zadejte požadované informace:  
  
    -   **Předvolby – Mac OS X**  
  
        -   **ID aplikace**: Zadejte ID aplikace souboru seznamu vlastností, ze kterého chcete vyhodnotit shodu klíče.  
  
             Pokud například chcete upravit nastavení pro webový prohlížeč Safari, můžete použít soubor **com.apple.Safari.plist**.  
  
        -   **Klíč**: zadejte název klíče, který chcete vyhodnotit pro dodržování předpisů na počítačích Mac. Použijte následující syntaxi: */<adresář\>/<název klíče\>*.  
  
            > [!IMPORTANT]  
            >  V názvu klíče se rozlišují velká a malá písmena a nebudou vyhodnoceny, pokud se liší od názvu klíče v počítači Mac. Po zadání názvu klíče navíc nemůžete tento název upravit. Pokud potřebujete název klíče upravit, odstraňte nastavení a potom ho vytvořte znovu.  
  
    -   **Skript**  
  
        -   **Skript zjišťování**: vyberte **Přidat skript**a potom zadejte skript prostředí pro vyhodnocení nastavení na počítači Mac pro dodržování předpisů. Pomocí příkazu **echo** v skriptu prostředí vrátíte hodnoty, které se Configuration Manager pro dodržování předpisů. Configuration Manager používá výsledky vrácené v **stdout** k vyhodnocení dodržování předpisů.  
  
            > [!IMPORTANT]  
            >  Do skriptu zjišťování nezahrnujte příkaz **restart** . Vzhledem k tomu, že se skript zjišťování spustí při každém restartování klienta, způsobí to, že se počítač Mac bude nepřetržitě restartovat.  
  
        -   Skript napravení **(volitelný)**: Volitelně můžete vybrat **Přidat skript**a potom zadat skript prostředí, který se používá k nápravě nekompatibilních nastavení nalezených na klientských počítačích Mac.  
  
            > [!IMPORTANT]  
            >  Abyste se ujistili, že nezavádíte formátovací znaky, které počítač Mac nemůže interpretovat, nepoužívejte příkaz Kopírovat a vložit. Místo toho zadejte skript.  
  
11. Vyberte **datový typ**, což je formát, ve kterém podmínka vrátí data, než se použije k vyhodnocení nastavení.  
  
    > [!NOTE]  
    >  Datový typ **Plovoucí desetinná čárka** podporuje za desetinnou čárkou pouze 3 číslice.  
    >   
    >  Configuration Manager nepodporuje použití **logického** datového typu pro nastavení skriptu položky konfigurace počítače Mac. Místo toho nastavte datový typ na **celé číslo**a ujistěte se, že skript vrací celočíselnou hodnotu.  
  
12. Výběrem **OK** uložte nastavení a zavřete dialogové okno **vytvořit nastavení** . Pak pokračujte v přidávání tolika nastavení, kolik budete potřebovat.  
  
13. Na stránce **pravidla dodržování předpisů** v průvodci určete podmínky, které definují dodržování předpisů u položky konfigurace. Před vyhodnocením dodržování předpisů musí mít nastavení alespoň jedno pravidlo dodržování předpisů. Pokud chcete přidat nové pravidlo, vyberte **Nový** .  
  
14. V dialogovém okně **Vytvořit pravidlo** zadejte následující údaje:  
  
    -   **Název**: zadejte název pravidla dodržování předpisů.  
  
    -   **Popis**: zadejte popis pravidla dodržování předpisů.  
  
    -   **Vybrané nastavení**: kliknutím na **Procházet** otevřete dialogové okno **Vybrat nastavení** . Vyberte nastavení, pro které chcete definovat pravidlo, nebo vyberte **nové nastavení**. Po dokončení klikněte na **Vybrat**.  
  
        > [!TIP]  
        >  Můžete také vybrat **vlastnosti** a zobrazit informace o aktuálně vybraném nastavení.  
  
    -   **Typ pravidla**: Vyberte typ pravidla dodržování předpisů, který chcete použít:  
  
        -   **Hodnota**: Vytvořte pravidlo, které porovnává hodnotu vrácenou položkou konfigurace s vámi zadanou hodnotou.  
  
        -   **Existenční**: Vytvořte pravidlo, které vyhodnotí nastavení v závislosti na tom, jestli na zařízení existuje.  
  
    -   Pro typ pravidla **Hodnota** zadejte následující informace:  
  
        -   **Nastavení musí odpovídat následujícímu pravidlu**: vyberte operátor a hodnotu, která bude vyhodnocená z hlediska dodržování předpisů s vybraným nastavením. Můžete použít následující operátory:  
  
            -   **Je rovno**  
  
            -   **Není rovno**  
  
            -   **Větší než**  
  
            -   **Menší než**  
  
            -   **Jednotlivých**  
  
            -   **Je větší než nebo rovno**  
  
            -   **Je menší než nebo rovno**  
  
            -   **Jedna z**: v textovém poli zadejte jednu položku na každý řádek.  
  
            -   **Žádné z**: v textovém poli zadejte jednu položku na každý řádek.  
  
        -   **Napravit pravidla nesplňující požadavky**, je-li to podporováno: tuto možnost vyberte, pokud chcete Configuration Manager automaticky napravit pravidla nesplňující požadavky.  
  
            > [!IMPORTANT]  
            >  Napravit pravidla nedodržující předpisy můžete pouze v případě, že je operátor pravidla nastavený na **Rovná se**.  
  
        -   **Pokud není nalezena instance tohoto nastavení, nahlásit neshodu**: položka konfigurace nahlásí neshodu v případě, že toto nastavení není v počítači Mac nalezeno.  
  
        -   **Závažnost neshody pro sestavy**: Zadejte úroveň závažnosti oznámenou v případě, že toto pravidlo dodržování předpisů selhává. K dispozici jsou následující úrovně závažnosti:  
  
            -   **Žádné**: počítače, které nesplní toto pravidlo dodržování předpisů, nehlásí pro sestavy Configuration Manager žádné závažnost selhání.  
  
            -   **Informace**: počítače, které nesplní toto pravidlo dodržování předpisů, nahlásí u sestav Configuration Manager závažnost selhání typu **informace** .  
  
            -   **Upozornění**: počítače, které nesplní toto pravidlo dodržování předpisů, nahlásí u sestav Configuration Manager závažnost selhání typu **Upozornění** .  
  
            -   **Kritické**: počítače, které nesplní toto pravidlo dodržování předpisů, nahlásí u sestav Configuration Manager závažnost selhání typu **kritické** .  
  
            -   **Kritické s událostí**: počítače, které nesplní toto pravidlo dodržování předpisů, nahlásí u sestav Configuration Manager závažnost selhání typu **kritické** . Klientský počítač se systémem Mac také zaznamená tuto úroveň závažnosti.  
  
    -   Pro typ pravidla **Existenční** zadejte následující informace:  
  
        -   Vyberte jednu z těchto akcí:  
  
            -   **Nastavení musí existovat na klientských zařízeních**  
  
            -   **Nastavení nesmí existovat na klientských zařízeních**  
  
        -   **Závažnost neshody pro sestavy**: Zadejte úroveň závažnosti, která se oznamuje, pokud toto pravidlo dodržování předpisů selhává. K dispozici jsou následující úrovně závažnosti:  
  
            -   **Žádné**: počítače, které nesplní toto pravidlo dodržování předpisů, nehlásí pro sestavy Configuration Manager žádné závažnost selhání.  
  
            -   **Informace**: počítače, které nesplní toto pravidlo dodržování předpisů, nahlásí u sestav Configuration Manager závažnost selhání typu **informace** .  
  
            -   **Upozornění**: počítače, které nesplní toto pravidlo dodržování předpisů, nahlásí u sestav Configuration Manager závažnost selhání typu **Upozornění** .  
  
            -   **Kritické**: počítače, které nesplní toto pravidlo dodržování předpisů, nahlásí u sestav Configuration Manager závažnost selhání typu **kritické** .  
  
            -   **Kritické s událostí**: počítače, které nesplní toto pravidlo dodržování předpisů, nahlásí u sestav Configuration Manager závažnost selhání typu **kritické** . Klientský počítač se systémem Mac také zaznamená tuto úroveň závažnosti.  
  
        > [!NOTE]  
        >  Zobrazené možnosti se můžou lišit v závislosti na typu nastavení, pro které konfigurujete pravidlo.  
  
15. Kliknutím na **tlačítko OK** zavřete dialogové okno **vytvořit pravidlo** .  
  
16. Na stránce **Souhrn** potvrďte nastavení pro novou položku konfigurace. Potom dokončete průvodce.  
  
Podívejte se na novou položku konfigurace v uzlu **položky konfigurace** pracovního prostoru **prostředky a kompatibilita** .  
  
Pokud teď chcete přidat tuto položku konfigurace do standardních hodnot konfigurace, přečtěte si téma [Vytvoření standardních hodnot konfigurace](../../compliance/deploy-use/create-configuration-baselines.md).  
  
## <a name="next-steps"></a>Další kroky

 [Položky konfigurace pro zařízení spravovaná pomocí klienta Configuration Manager](../../compliance/deploy-use/create-configuration-items.md)
