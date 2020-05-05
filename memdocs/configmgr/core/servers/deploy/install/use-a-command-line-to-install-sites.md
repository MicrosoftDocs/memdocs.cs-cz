---
title: Instalace z příkazového řádku
titleSuffix: Configuration Manager
description: Zjistěte, jak spustit instalaci Configuration Manager na příkazovém řádku pro celou řadu instalací lokality.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c46e7f4dde0fb4719daf0f5c1f1293f627063f2a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717955"
---
# <a name="use-a-command-line-to-install-configuration-manager-sites"></a>Instalace Configuration Managerch lokalit pomocí příkazového řádku

*Platí pro: Configuration Manager (Current Branch)*

 Můžete spustit instalaci Configuration Manager na příkazovém řádku a nainstalovat celou řadu typů webů.

## <a name="supported-tasks-for-command-line-installations"></a>Podporované úlohy pro instalace na příkazovém řádku
 Tato metoda spuštění instalačního programu podporuje následující úlohy instalace lokality a údržby lokality:

- **Instalace lokality centrální správy nebo primární lokality z příkazového řádku**  
  Zobrazit [Možnosti příkazového řádku pro instalaci](../../../../core/servers/deploy/install/command-line-options-for-setup.md)

- **Upravte jazyky používané v lokalitě centrální správy nebo v primární lokalitě.**  
   Pokud chcete upravit jazyky, které jsou nainstalované v lokalitě, z příkazového řádku (včetně jazyků pro mobilní zařízení), musíte:  

  - Spusťte instalaci ze ** &lt;ConfigMgrInstallationPath\>\Bin\X64** na serveru lokality,
  - Použijte možnost příkazového řádku **/MANAGELANGS** .
  - Zadejte soubor skriptu jazyka, který určuje jazyky, které chcete přidat nebo odebrat.  

    Použijte například následující syntaxi příkazu: **setupwpf. exe/MANAGELANGS &lt;Language Script File\> **  

    Pokud chcete vytvořit soubor skriptu jazyka, použijte informace v části [Možnosti příkazového řádku ke správě jazyků](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang) .  

- **Použití souboru instalačního skriptu pro bezobslužné instalace lokality nebo Site Recovery**  
   Instalaci můžete spustit z příkazového řádku pomocí instalačního skriptu a spuštěním bezobslužné instalace lokality. Tuto možnost můžete použít také k obnovení lokality.    

   Postup použití skriptu s instalačním programem:  

  - Spusťte instalační program s příkazovým řádkem-Option **/Script** a zadejte soubor skriptu.  

  - Soubor skriptu musí být nakonfigurovaný s požadovanými klíči a hodnotami.  

    Pro bezobslužnou instalaci lokality centrální správy nebo primární lokality musí mít soubor skriptu tyto oddíly:  

  - Identifikace    
  - Možnosti    
  - MožnostiKonfSQL    
    -   Hierarchyoptions Pokud    
  - CloudConnectorOptions   

    Chcete-li obnovit lokalitu, je třeba zahrnout také následující části souboru skriptu:  

  - Identifikace  
  - Obnovení

Další informace najdete v tématu [bezobslužné obnovení lokality pro Configuration Manager](../../manage/unattended-recovery.md).  

Seznam klíčů a hodnot pro použití v souboru skriptu bezobslužné instalace najdete v tématu [klíče souborů skriptu bezobslužné instalace](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended).  

## <a name="about-the-command-line-script-file"></a>O souboru skriptu příkazového řádku  
 Pro bezobslužné instalace Configuration Manager můžete instalační program spustit pomocí možnosti příkazového řádku **/Script**a zadat soubor skriptu, který obsahuje možnosti instalace. Následující úkoly jsou podporovány pomocí této metody:  

-   Instalace lokality centrální správy  
-   Instalace primární lokality  
-   Instalace konzoly nástroje Configuration Manager  
-   Obnovení lokality  

> [!NOTE]  
>  Soubor skriptu bezobslužné instalace nemůžete použít k upgradu zkušební lokality na licencovanou instalaci Configuration Manager.  

### <a name="the-cdlatest-key-name"></a>Název klíče CDLatest
Když použijete médium z disku CD-ROM. Poslední složka, ve které se spustí instalace s použitím skriptu pro tyto čtyři možnosti instalace, musí váš skript zahrnovat klíč **CDLatest** s hodnotou **1**:
- Instalace nové lokality centrální správy
- Nainstalovat novou primární lokalitu
- Obnovení lokality centrální správy
- Obnovení primární lokality

Tato hodnota není podporována pro použití s instalačním médiem, které získáte na webu Microsoft Volume License.
Informace o tom, jak používat tento název klíče v souboru skriptu, najdete v tématu [Možnosti příkazového řádku](command-line-options-for-setup.md) .



### <a name="create-the-script"></a>Vytvoření skriptu
Instalační skript se automaticky vytvoří při [spuštění instalačního programu pro instalaci lokality pomocí uživatelského rozhraní](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  Když potvrdíte nastavení na stránce **Souhrn** v průvodci, dojde k následujícímu:  

-   Instalační program vytvoří skript **%TEMP%\ConfigMgrAutoSave.ini**.  Tento soubor můžete přejmenovat předtím, než ho použijete, ale musí si zachovat příponu souboru. ini.  
-   Skript bezobslužné instalace obsahuje nastavení, která jste vybrali v průvodci.  
-   Po vytvoření skriptu můžete upravit skript pro instalaci dalších lokalit ve vaší hierarchii.  
-   Pak můžete pomocí tohoto skriptu provést bezobslužnou instalaci Configuration Manager.  

Tento soubor skriptu obsahuje stejné informace, k jejichž zadání vyzve Průvodce instalací nástroje, s tím rozdílem, že neexistuje žádné výchozí nastavení.   
Je nutné zadat všechny hodnoty klíčů pro instalaci, které se vztahují na typ instalace, kterou používáte.   

Když instalační program vytvoří skript bezobslužné instalace, naplní hodnotu kódu Product Key, kterou zadáte během instalace. Může to být platný kód Product Key nebo **Eval** při instalaci zkušební verze nástroje Configuration Manager. Hodnota kódu Product Key ve skriptu je naplněná, aby bylo možné dokončit kontrolu požadovaných součástí.   

Když instalační program spustí aktuální instalaci lokality, vytvoří se automaticky vytvořený skript, aby se znovu vymazala hodnota kódu Product Key ve skriptu, který vytvoří. Před použitím skriptu pro bezobslužnou instalaci nové lokality můžete upravit skript tak, aby poskytoval platný kód Product Key, nebo zadat zkušební instalaci Configuration Manager.  

### <a name="section-names-key-names-and-values"></a>Názvy oddílů, názvy klíčů a hodnoty
Skript obsahuje názvy částí, názvy klíčů a hodnoty. Všimněte si následujících informací:
-   Požadované názvy klíčů oddílů se liší v závislosti na typu instalace, který zadáváte do skriptů.
-   Pořadí klíčů v částech a pořadí částí v souboru není důležité.     
-   U klíčů se nerozlišují velká a malá písmena.  
-   Když zadáte hodnoty pro klíče, musí za názvem klíče následovat znak rovná se (=) a hodnota klíče.    

> [!TIP]  
>  Kompletní sadu možností najdete v tématu [Možnosti příkazového řádku pro instalační program a skripty](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  

## <a name="use-the-script-setup-command-line-option"></a>Použití možnosti příkazového řádku pro nastavení/SCRIPT

-   Je nutné použít soubor skriptu instalace a zadat název souboru za parametrem příkazového řádku pro nastavení **/Script** . Všimněte si následujících informací:   
    -   Název souboru musí mít příponu názvu souboru **. ini** .  
    -   Když odkazujete na soubor skriptu instalace z příkazového řádku, musíte zadat úplnou cestu k souboru. Například pokud se inicializační soubor instalace nazývá Setup. ini a je uložen ve složce C:\Setup, zadejte do příkazového řádku: **Setup/Script c:\Setup\Setup.ini**.  

-   Účet, který spouští instalační program, musí mít v počítači práva **správce** . Když spouštíte instalaci pomocí bezobslužného skriptu, otevřete okno příkazového řádku pomocí možnosti **Spustit jako správce** .   
