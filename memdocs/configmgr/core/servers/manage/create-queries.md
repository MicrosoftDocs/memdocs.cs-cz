---
title: Vytváření dotazů
titleSuffix: Configuration Manager
description: Objevte, jak vytvářet a importovat dotazy v Configuration Manager. Obsahuje příklady dotazů a tipů.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 63f815394414167ad4f887c5970538eab22c931a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906149"
---
# <a name="create-queries-in-configuration-manager"></a>Vytváření dotazů v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek popisuje, jak vytvářet a importovat dotazy v Configuration Manager.  

##  <a name="create-a-query"></a><a name="BKMK_Create"></a>Vytvoření dotazu  
 Pomocí tohoto postupu můžete vytvořit dotaz v Configuration Manager.  

1.  V konzole Configuration Manager vyberte **monitorování**.  

2.  V pracovním prostoru **monitorování** vyberte **dotazy**. Na kartě **Domů** ve skupině **vytvořit** vyberte možnost **vytvořit dotaz**.  

3.  Na kartě **Obecné** v **Průvodci vytvořením dotazu**zadejte jedinečný název a volitelně také komentář pro dotaz.  

4.  Pokud chcete importovat existující dotaz, který chcete použít jako základ pro nový dotaz, vyberte možnost **importovat příkaz dotazu**. V dialogovém okně **Procházet dotaz** vyberte dotaz, který chcete importovat, a pak vyberte **OK**.  

5.  V seznamu **typ objektu** vyberte typ objektu, který má dotaz vrátit. Tato tabulka popisuje některé příklady typů objektů, které můžete hledat:  

    |typ objektu|Description|  
    |-----------------|-----------------|  
    |**Systémový prostředek**|Slouží k vyhledání typických systémových atributů, jako je například název NetBIOS zařízení, verze klienta, IP adresa klienta a informace Active Directory Domain Services.|  
    |**Prostředek User**|Slouží k vyhledání typických uživatelských informací, jako jsou uživatelská jména, názvy skupin uživatelů a názvy skupin zabezpečení.|  
    |**Nasazení**|Slouží k vyhledání typických atributů nasazení, například názvu nasazení, plánu a kolekce, do které byl nasazen.|  

6.  Výběrem **příkazu Upravit dotaz** otevřete &lt; \> dialogové okno **vlastnosti příkazu** pro název dotazu.  

7.  Na kartě **Obecné** v &lt; \> dialogovém okně **vlastnosti příkazu** názvu dotazu Určete atributy, které dotaz vrátí a jak se mají zobrazovat. Kliknutím na ikonu **Nový** přidáte nový atribut. Můžete také vybrat možnost **Zobrazit jazyk dotazu** a zadat nebo upravit dotaz přímo v jazyk WQL (WMI Query Language) (WQL). Příklady dotazů WMI najdete v části Příklady [dotazů WQL](#BKMK_Example) v tomto článku.  

    > [!TIP]  
    > K vytvoření vlastních dotazů WQL můžete použít následující referenční dokumentaci:  
    >   
    > -   [WQL (SQL pro WMI)](https://docs.microsoft.com/windows/win32/wmisdk/wql-sql-for-wmi)  
    > -   [Klauzule WHERE](https://docs.microsoft.com/windows/win32/wmisdk/where-clause)  
    > -   [Operátory WQL](https://docs.microsoft.com/windows/win32/wmisdk/wql-operators)  

8.  Na kartě **kritéria** v &lt; \> dialogovém okně **vlastnosti příkazu** názvu dotazu zadejte kritéria, která slouží k upřesnění výsledků dotazu. Můžete například vracet pouze prostředky, které mají kód lokality **XYZ**. Pro dotaz můžete nakonfigurovat víc kritérií.  

    > [!IMPORTANT]  
    > Pokud vytvoříte dotaz neobsahující žádná kritéria, dotaz vrátí všechna zařízení v kolekci **Všechny systémy** .  

9. Na kartě **spojení** v &lt; \> dialogovém okně **vlastnosti příkazu** názvu dotazu můžete kombinovat data ze dvou různých atributů do výsledků dotazu. I když Configuration Manager automaticky vytvoří spojení s dotazy, když pro výsledek dotazu vyberete jiné atributy, karta **spojení** poskytuje pokročilejší možnosti. Configuration Manager podporuje tyto třídy atributů:  

    |Typ spojení|Description|  
    |---------------|-----------------|  
    |Vnitřní|Zobrazí pouze vyhovující výsledky. Vždy používají spojení, která jsou vytvořena automaticky.|  
    |Left|Zobrazí všechny výsledky pro základní atribut a jenom odpovídající výsledky pro spojovaný atribut.|  
    |Vpravo|Zobrazí všechny výsledky pro atribut JOIN a pouze vyhovující výsledky pro základní atribut.|  
    |Do bloku|Zobrazí všechny výsledky pro základní atribut i pro atribut JOIN.|  

     Další informace o tom, jak používat operace JOIN, najdete v dokumentaci k SQL Server.  

10. Kliknutím na **tlačítko OK** zavřete &lt; \> dialogové okno **vlastnosti příkazu** pro název dotazu.  

11. Na kartě **Obecné** v **Průvodci vytvořením dotazu**určete, že výsledky dotazu nejsou omezeny na členy kolekce, že jsou omezeny na členy zadané kolekce nebo že se při každém spuštění dotazu zobrazí výzva pro kolekci.  

12. Dokončením průvodce vytvořte nový dotaz. Nový dotaz se zobrazí v uzlu **dotazy** v pracovním prostoru **monitorování** .  

##  <a name="import-a-query"></a><a name="BKMK_Import"></a>Importovat dotaz  
 Pomocí tohoto postupu můžete importovat dotaz do Configuration Manager. Informace o tom, jak exportovat dotazy, najdete v tématu [Správa dotazů](../../../core/servers/manage/manage-queries.md).  

1.  V konzole Configuration Manager vyberte **monitorování**.  

2.  V pracovním prostoru **monitorování** vyberte **dotazy**. Na kartě **Domů** ve skupině **vytvořit** vyberte možnost **importovat objekty**.  

3.  Na stránce **název souboru MOF** v **Průvodci importem objektů**vyberte **Procházet** a vyberte soubor formát MOF (Managed Object Format) (MOF) obsahující dotaz, který chcete naimportovat.  

4.  Zkontrolujte informace o dotazu, který chcete naimportovat, a pak dokončete průvodce. Nový dotaz se zobrazí v uzlu **dotazy** v pracovním prostoru **monitorování** .  

##  <a name="example-wql-queries"></a><a name="BKMK_Example"></a> Example WQL queries

Tato část obsahuje příklad dotazů jazyka WQL, které můžete použít ve vaší hierarchii nebo upravit pro jiné účely. Chcete-li použít tyto dotazy, vyberte možnost **Zobrazit jazyk dotazu** v dialogovém okně **vlastnosti příkazu dotazu** . Pak zkopírujte a vložte dotaz do pole **příkaz dotazu** .  

> [!TIP]  
> Můžete použít zástupný znak `%` místo libovolného řetězce znaků. Například `%Visio%` vrátí systém Microsoft Office Visio 2010.  

### <a name="computers-that-run-windows-10"></a>Počítače se systémem Windows 10

Následující dotaz vrátí název NetBIOS a verzi operačního systému všech počítačů s Windows 7.  

``` WQL
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from
SMS_R_System where
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 10%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>Počítače s nainstalovaným určitým softwarovým balíčkem  

Následující dotaz vrátí název NetBIOS a název softwarového balíčku všech počítačů, které mají nainstalovaný konkrétní softwarový balíček. Tento příklad vrátí všechny počítače s nainstalovanou verzí aplikace Microsoft Visio. Nahraďte `Microsoft%Visio%` softwarovým balíčkem, pro který chcete zadat dotaz.  

> [!TIP]  
> Tento dotaz vyhledává softwarový balíček podle názvů, které se zobrazují v seznamu programů v Ovládacích panelech Windows.  

``` WQL
select SMS_R_System.NetbiosName,
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =
SMS_R_System.ResourceId where
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "Microsoft%Visio%"  
```  

### <a name="computers-in-a-specific-active-directory-domain-services-organizational-unit"></a>Počítače v určité Active Directory Domain Services organizační jednotce

Použijte následující dotaz, který vrátí název NetBIOS a název organizační jednotky (OU) pro všechny počítače v zadané organizační jednotce. Nahraďte text `OU Name` názvem organizační jednotky, pro kterou chcete zadat dotaz.  

``` WQL
select SMS_R_System.NetbiosName,
SMS_R_System.SystemOUName from
SMS_R_System where
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>Počítače s určitým názvem NetBIOS

Následující dotaz vrátí název NetBIOS všech počítačů, které začínají určitým řetězcem znaků. V tomto příkladu dotaz vrátí všechny počítače s názvem NetBIOS, který začíná na `ABC` .  

``` WQL
select SMS_R_System.NetbiosName from
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="devices-of-a-specific-type"></a><a name="BKMK_DeviceType"></a> Zařízení určitého typu

Typy zařízení jsou uložené v databázi Configuration Manager pod třídou prostředků **sms_r_system** a názvem atributu **AgentEdition**. Pomocí tohoto dotazu můžete načíst jenom zařízení, která odpovídají edici agenta typu zařízení, kterou zadáte:  

``` WQL
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

Pro ID zařízení použijte jednu z těchto hodnot &lt; \> :  

|Typ zařízení|Hodnota AgentEdition|  
|-----------------|---------------------------|  
|Stolní nebo přenosný počítač s Windows|0|  
|Zařízení s Windows využívající procesor ARM (se systémem Windows RT)|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|telefon se systémem Windows|4|  
|Počítač Mac|5|  
|Windows CE|6|  
|Windows Embedded|7|  
|Systém Intel na čipu|12|  
|Servery Unix a Linux|13|  
|Microsoft HoloLens (MDM)|15|
|Microsoft Surface Hub (MDM)|16|

> [!NOTE]
> Hodnoty, které nejsou uvedeny v této tabulce, jsou přidruženy k zařízením, která již nejsou podporována.

<!-- removed with hybrid EOL
|iOS|8|  
|iPad|9|  
|iPod touch|10|  
|Android|11|  
|Apple macOS (MDM)|14|
|Android for Work|17|
 -->

Pokud například chcete vracet pouze počítače se systémem Mac, použijte tento dotaz:  

``` WQL
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="next-steps"></a>Další kroky

[Správa dotazů](manage-queries.md)
