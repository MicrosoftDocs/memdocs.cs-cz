---
title: Vytváření a spouštění skriptů
titleSuffix: Configuration Manager
description: Vytvářejte a spouštějte skripty PowerShellu na klientských zařízeních.
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: db3a673d99efc40bd6fa0da7930c66c648136e03
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695353"
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Vytvoření a spuštění PowerShellových skriptů z konzoly Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

<!--1236459-->
Configuration Manager má integrovanou schopnost spouštět skripty prostředí PowerShell. Prostředí PowerShell přináší výhody vytváření sofistikovaných automatizovaných skriptů, které jsou srozumitelné a sdílené s větší komunitou. Tyto skripty zjednodušují vytváření vlastních nástrojů pro správu softwaru a umožňují rychle provádět rutinní úkoly, což vám umožní rychleji a častěji pracovat s velkými úlohami.  

> [!Note]  
> Configuration Manager ve výchozím nastavení nepovolí tuto volitelnou funkci. Tuto funkci musíte před použitím povolit. Další informace naleznete v části [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  


Díky této integraci v Configuration Manager můžete pomocí funkce *spustit skripty* provádět následující akce:

- Vytvořte a upravte skripty pro použití s Configuration Manager.
- Spravujte využití skriptů prostřednictvím rolí a oborů zabezpečení. 
- Spouštějte skripty na kolekcích nebo individuálních místních spravovaných počítačích s Windows.
- Získejte rychlé agregované výsledky skriptů z klientských zařízení.
- Monitorujte provádění skriptu a zobrazte výsledky generování sestav z výstupu skriptu.

> [!WARNING]
> - S ohledem na výkon skriptů vám připomeneme, že budete mít k disměrnému a opatrní na jejich použití. Sestavili jsme další bezpečnostní opatření, která vám pomůžou. oddělené role a obory. Ujistěte se, že před spuštěním ověříte přesnost skriptů a potvrďte, že pocházejí z důvěryhodného zdroje, aby nedocházelo k neúmyslnému spuštění skriptu. Je třeba mít na starosti rozšířené znaky nebo jiné zmatení a informovat o zabezpečení skriptů. [Další informace o zabezpečení PowerShellových skriptů](learn-script-security.md)
> - Určitý antimalwarový software může nechtěně aktivovat události proti Configuration Manager spuštění skriptů nebo funkcí CMPivot. Doporučuje se vyloučit%windir%\CCM\ScriptStore, aby antimalwarový software mohl spouštět tyto funkce bez rušivých zásahů.

## <a name="prerequisites"></a>Předpoklady

- Aby bylo možné spouštět skripty prostředí PowerShell, musí být v klientovi spuštěný PowerShell verze 3,0 nebo novější. Pokud ale skript, který spustíte, obsahuje funkčnost z novější verze prostředí PowerShell, musí klient, na kterém spouštíte skript, používat tuto verzi PowerShellu.
- Aby bylo možné spouštět skripty, Configuration Manager klienti musí spustit klienta z verze 1706 nebo novější.
- Chcete-li použít skripty, musíte být členem příslušné role zabezpečení Configuration Manager.
- Import a vytváření skriptů – váš účet musí mít oprávnění **Create** pro **skripty SMS**.
- Chcete-li schválit nebo zamítnout skripty – váš účet musí mít oprávnění **schvalovat** pro **skripty SMS**.
- Chcete-li spustit skripty – váš účet musí mít oprávnění ke **spuštění skriptu** pro **kolekce**.

Další informace o Configuration Manager rolích zabezpečení:</br>
[Obory zabezpečení pro skripty pro spuštění](#security-scopes)</br>
[Role zabezpečení pro skripty pro spuštění](#bkmk_ScriptRoles)</br>
[Základy správy na základě rolí](../../core/understand/fundamentals-of-role-based-administration.md).

## <a name="limitations"></a>Omezení

Spustit skripty v současné době podporují:

- Skriptovací jazyky: PowerShell
- Typy parametrů: celé číslo, řetězec a seznam.


>[!WARNING]
>Počítejte s tím, že při použití parametrů se otevře plocha oblasti pro potenciální riziko útoku prostřednictvím injektáže prostředí PowerShell. Existují různé způsoby, jak zmírnit a pracovat, jako je například použití regulárních výrazů k ověření vstupu parametru nebo použití předdefinovaných parametrů. Běžným osvědčeným postupem není zahrnutí tajných kódů do skriptů PowerShellu (žádná hesla atd.). [Další informace o zabezpečení PowerShellových skriptů](learn-script-security.md) <!--There are external tools available to validate your PowerShell scripts such as the [PowerShell Injection Hunter](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) tool. -->


## <a name="run-script-authors-and-approvers"></a>Spustit autory skriptů a schvalovatele

Spouštění skriptů používá koncept *autorů skriptů* a *schvalovatelů skriptů* jako samostatné role pro implementaci a provádění skriptu. Oddělení rolí autora a schvalovatele umožňuje důležité kontrolu výkonného nástroje, který spouští skripty. K dispozici je další role *spouštěče skriptu* , která umožňuje spouštění skriptů, ale ne vytváření nebo schvalování skriptů. Viz téma [Vytvoření rolí zabezpečení pro skripty](#bkmk_ScriptRoles).

### <a name="scripts-roles-control"></a>Ovládací prvek role skriptů

Ve výchozím nastavení uživatelé nemůžou schválit vytvořený skript. Vzhledem k tomu, že jsou skripty výkonné, všestranné a potenciálně nasazené na mnoho zařízení, můžete jednotlivé role oddělit mezi osobu, která tento skript vytvoří, a osoba, která skript schválí. Tyto role poskytují další úroveň zabezpečení před spuštěním skriptu bez dohledu. Je možné vypnout sekundární schválení pro snadné testování.

### <a name="approve-or-deny-a-script"></a>Schválení nebo zamítnutí skriptu

Aby bylo možné skripty spustit, musí být nejprve schváleny rolí *schvalovatele skriptu* . Postup schválení skriptu:

1. V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.
2. V pracovním prostoru **softwarová knihovna** klikněte na **skripty**.
3. V seznamu **skript** vyberte skript, který chcete schválit nebo odepřít, a potom na kartě **Domů** ve skupině **skript** klikněte na **schválit/odepřít**.
4. V dialogovém okně **schválení nebo odepření skriptu** vyberte **schválit**nebo **Odepřít** pro skript. Volitelně můžete zadat komentář k vašemu rozhodnutí.  Pokud skript odepřete, nejde ho spustit na klientských zařízeních. <br>
![Schválení skriptu](./media/run-scripts/RS-approval.png)
1. Dokončete průvodce. V seznamu **skriptů** se zobrazí změna sloupce **stav schválení** v závislosti na akci, kterou jste udělali.

### <a name="allow-users-to-approve-their-own-scripts"></a>Povolit uživatelům schvalovat své vlastní skripty

Toto schválení se primárně používá pro testovací fázi vývoje skriptů.

1. V konzole Configuration Manager klikněte na možnost **Správa**.
2. V pracovním prostoru **Správa** rozbalte nabídku **Konfigurace webu**a klikněte na položku **Weby**.
3. V seznamu lokality vyberte lokalitu a pak na kartě **Domů** ve skupině **lokality** klikněte na **Nastavení hierarchie**.
4. Na kartě **Obecné** v dialogovém okně **Vlastnosti nastavení hierarchie** zrušte zaškrtnutí políčka **autoři skriptů vyžadují další schvalovatele skriptu**.

>[!IMPORTANT]
>Jako osvědčený postup byste neměli povolit autorovi skriptu schvalovat své vlastní skripty. Mělo by být povoleno pouze v nastavení testovacího prostředí. Pečlivě zvažte potenciální dopad na změnu tohoto nastavení v produkčním prostředí.

## <a name="security-scopes"></a>Obory zabezpečení
  
Spouštění skriptů používá rozsahy zabezpečení, existující funkce Configuration Manager, pro řízení vytváření a spouštění skriptů pomocí přiřazování značek, které reprezentují skupiny uživatelů. Další informace o používání oborů zabezpečení najdete v tématu [Konfigurace správy na základě rolí pro Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="create-security-roles-for-scripts"></a><a name="bkmk_ScriptRoles"></a> Vytváření rolí zabezpečení pro skripty
Tři role zabezpečení používané ke spouštění skriptů nejsou ve výchozím nastavení ve Configuration Manager vytvořeny. Pokud chcete vytvořit spouštěče skriptů, autory skriptů a role schvalovatelů skriptů, postupujte podle kroků uvedených výše.

1. V konzole Configuration Manager, přejít na **Správa**  > **Security**  > **role zabezpečení** zabezpečení
2. Klikněte pravým tlačítkem na roli a pak klikněte na **Kopírovat**. Role, kterou kopírujete, má již přiřazená oprávnění. Ujistěte se, že jste provedli pouze oprávnění, která potřebujete. 
3. Zadejte **název** vlastní role a její **Popis**. 
4. Přiřaďte roli zabezpečení níže uvedeným oprávněním.  

### <a name="security-role-permissions"></a>Oprávnění role zabezpečení  

**Název role**: spouštěče skriptů  
- **Popis**: Tato oprávnění umožňují, aby tato role spouštěla pouze skripty, které byly dříve vytvořeny a schváleny jinými rolemi.  
- **Oprávnění:** Zajistěte, aby byla tato hodnota nastavena na **hodnotu Ano**.  

|Kategorie|Oprávnění|Stav|
|---|---|---|
|Kolekce|Spustit skript|Ano|
|Web|Číst|Ano|
|Skripty SMS|Číst|Ano|


**Název role**: autoři skriptů  
- **Popis**: Tato oprávnění umožňují této roli vytvářet skripty, ale nemůžou je schvalovat ani spouštět.  
- **Oprávnění**: Ujistěte se, že jsou nastavená následující oprávnění.
 
|Kategorie|Oprávnění|Stav|
|---|---|---|
|Kolekce|Spustit skript|Ne|
|Web|Číst|Ano|
|Skripty SMS|Vytvořit|Ano|
|Skripty SMS|Číst|Ano|
|Skripty SMS|Odstranit|Ano|
|Skripty SMS|Modify|Ano|


**Název role**: schvalovatelé skriptů  
- **Popis**: Tato oprávnění umožňují této roli schvalovat skripty, ale nemůžou je vytvářet ani spouštět.  
- **Oprávnění:** Ujistěte se, že jsou nastavená následující oprávnění.  

|Kategorie|Oprávnění|Stav|
|---|---|---|
|Kolekce|Spustit skript|Ne|
|Web|Číst|Ano|
|Skripty SMS|Číst|Ano|
|Skripty SMS|Schválení|Ano|
|Skripty SMS|Modify|Ano|

     
**Příklad oprávnění ke skriptům SMS pro roli autoři skriptů**  

 ![Příklad oprávnění ke skriptům SMS pro roli autoři skriptů](./media/run-scripts/script_authors_permissions.png)


## <a name="create-a-script"></a>Vytvoření skriptu

1. V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.
2. V pracovním prostoru **softwarová knihovna** klikněte na **skripty**.
3. Na kartě **Domů** ve skupině **vytvořit** klikněte na možnost **vytvořit skript**.
4. Na stránce **skript** v Průvodci vytvořením **skriptu** nakonfigurujte následující nastavení:
    - **Název skriptu** – zadejte název skriptu. I když můžete vytvořit více skriptů se stejným názvem a pomocí duplicitních názvů poznáte, že budete chtít najít skript, který potřebujete, v konzole Configuration Manager.
    - **Skriptovací jazyk** – v současné době se podporují jenom skripty PowerShellu.
    - **Import** – importujte powershellový skript do konzoly nástroje. Skript se zobrazí v poli **skript** .
    - **Vymazat** – Odebere aktuální skript z pole skriptu.
    - **Skript** – zobrazí aktuálně importovaný skript. Skript v tomto poli můžete podle potřeby upravit.
5. Dokončete průvodce. Nový skript se zobrazí v seznamu **skriptů** se stavem **čekání na schválení**. Než budete moct spustit tento skript na klientských zařízeních, musíte ho schválit. 

> [!IMPORTANT]
> Vyhněte se skriptování restartování zařízení nebo restartování agenta Configuration Manager při použití funkce spustit skripty. To by mohlo vést k průběžnému restartování stavu. V případě potřeby jsou k dispozici vylepšení funkce klientského oznámení, která umožňují restartování zařízení. [Sloupec čeká na restartování](../../core/clients/manage/manage-clients.md#restart-clients) může přispět k identifikaci zařízení, která vyžadují restart. 
> <!--SMS503978  -->

## <a name="script-parameters"></a>Parametry skriptu

Přidáním parametrů do skriptu získáte větší flexibilitu vaší práce. Můžete zahrnout až 10 parametrů. Následující text popisuje aktuální schopnost funkce spouštět skripty s parametry skriptu pro; *String*, *celočíselné* datové typy. K dispozici jsou také seznamy předdefinovaných hodnot. Pokud váš skript obsahuje nepodporované datové typy, zobrazí se upozornění.

V dialogovém okně **vytvořit skript** klikněte v části **skript**na **Parametry skriptu** .

Každý z parametrů vašeho skriptu má vlastní dialog pro přidání dalších podrobností a ověření. Pokud je ve skriptu výchozí parametr, zobrazí se jeho výčet v uživatelském rozhraní parametru a můžete ho nastavit. Configuration Manager nepřepíše výchozí hodnotu, protože nikdy neupraví skript přímo. Můžete si to představit jako "předem vyplněné navrhované hodnoty", které jsou k dispozici v uživatelském rozhraní, ale Configuration Manager neposkytují přístup k "výchozím" hodnotám v době běhu. To lze vyřešit úpravou skriptu, aby byly správné výchozí hodnoty. <!--17694323-->

>[!IMPORTANT]
> Hodnoty parametrů nemůžou obsahovat jednoduchou uvozovku. </br></br>
> Došlo k známému problému, kdy hodnoty parametrů, které obsahují nebo jsou uzavřeny v jednoduchých uvozovkách, nejsou správně předány do skriptu. Při zadávání výchozích hodnot parametrů, které obsahují mezeru ve skriptu, použijte místo toho dvojité uvozovky. Při zadávání výchozích hodnot parametrů během vytváření nebo provádění **skriptu**není nutné mít výchozí hodnotu v obou nebo jednoduchých uvozovkách bez ohledu na to, zda hodnota obsahuje mezeru nebo ne.

### <a name="parameter-validation"></a>Ověřování parametrů

Každý parametr ve vašem skriptu má dialogové okno **vlastností parametru skriptu** , pomocí kterého můžete přidat ověřování pro tento parametr. Po přidání ověřování byste měli získat chyby, pokud zadáváte hodnotu pro parametr, který nesplňuje jeho ověření.

#### <a name="example-firstname"></a>Příklad: *FirstName*

V tomto příkladu je možné nastavit vlastnosti řetězcového parametru, *FirstName*.

![Parametry skriptu – řetězec](./media/run-scripts/RS-parameters-string.png)


Část ověření dialogového okna **vlastností parametru skriptu** obsahuje následující pole pro vaše použití:

- **Minimální délka** – minimální počet znaků pole *FirstName* .
- **Maximální délka**– maximální počet znaků pole *FirstName*
- **RegEx** *Regulární výraz*je krátký. Další informace o použití regulárního výrazu naleznete v další části s *použitím ověření regulárního výrazu*.
- **Vlastní chyba** – užitečné pro přidání vlastní chybové zprávy, která nahrazuje jakékoli chybové zprávy ověřování systému.

#### <a name="using-regular-expression-validation"></a>Ověřování pomocí regulárního výrazu

Regulární výraz je kompaktní forma programování pro kontrolu řetězce znaků proti zakódovanému ověření. Například můžete vyhledat absenci znakového písmena v poli *FirstName* tak, že umístíte `[^A-Z]` do pole *Regex* .

.NET Framework je podporováno zpracování regulárního výrazu pro tento dialog. Pokyny k používání regulárních výrazů naleznete v tématu [regulární výraz .NET](/dotnet/standard/base-types/regular-expressions) a [Jazyk regulárních výrazů](/dotnet/standard/base-types/regular-expression-language-quick-reference).


## <a name="script-examples"></a>Příklady skriptu

Tady je několik příkladů, které ilustrují skripty, které můžete chtít použít s touto funkcí.

### <a name="create-a-new-folder-and-file"></a>Vytvoří novou složku a soubor.

Tento skript vytvoří novou složku a soubor v rámci složky s ohledem na zadání pojmenování.

``` PowerShell
Param(
[Parameter(Mandatory=$True)]
[string]$FolderName,
[Parameter(Mandatory=$True)]
[string]$FileName
)

New-Item $FolderName -type directory
New-Item $FileName -type file
```

### <a name="get-os-version"></a>Získat verzi operačního systému

Tento skript používá rozhraní WMI k dotazování počítače na jeho verzi operačního systému.

``` PowerShell
Write-Output (Get-WmiObject -Class Win32_operatingSystem).Caption
```

## <a name="edit-or-copy-powershell-scripts"></a><a name="bkmk_psedit"></a> Úpravy nebo kopírování skriptů PowerShellu
<!--3705507-->
*(Zavedeno s verzí 1902)*  
Můžete **Upravit** nebo **zkopírovat** existující skript prostředí PowerShell, který se používá s funkcí **spustit skripty** . Místo opětovného vytváření skriptu, který potřebujete změnit, ho teď můžete přímo upravit. Obě akce používají stejné možnosti průvodce jako při vytváření nového skriptu. Při úpravách nebo kopírování skriptu Configuration Manager neuchovává stav schválení.

> [!Tip]  
> Neupravujte skript, který je aktivně spuštěný na klientech. Nespustí se tak původní skript a z těchto klientů možná nezískáte zamýšlené výsledky.  

### <a name="edit-a-script"></a>Úprava skriptu

1. V pracovním prostoru **softwarová knihovna** otevřete uzel **skripty** .
1. Vyberte skript, který chcete upravit, a pak na pásu karet klikněte na **Upravit** . 
1. Změňte nebo znovu naimportujte skript na stránce **Podrobnosti skriptu** .
1. Kliknutím na **Další** zobrazíte **Souhrn** a po dokončení úprav budete moct **Zavřít** .

### <a name="copy-a-script"></a>Kopírování skriptu

1. V pracovním prostoru **softwarová knihovna** otevřete uzel **skripty** .
1. Vyberte skript, který chcete zkopírovat, a pak klikněte na tlačítko **Kopírovat** na pásu karet.
1. Přejmenujte skript do pole **název skriptu** a proveďte další úpravy, které byste mohli potřebovat.
1. Kliknutím na **Další** zobrazíte **Souhrn** a po dokončení úprav budete moct **Zavřít** .


## <a name="run-a-script"></a>Spuštění skriptu

Po schválení skriptu je možné ho spustit na jednom zařízení nebo v kolekci. Po spuštění skriptu se rychle spustí v systému s vysokou prioritou, který je časovým limitem v průběhu jedné hodiny. Výsledky skriptu se pak vrátí pomocí systému stavových zpráv.

Výběr kolekce cílů pro váš skript:

1. V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.
2. V pracovním prostoru Prostředky a kompatibilita klikněte na možnost **Kolekce zařízení**.
3. V seznamu **kolekce zařízení** klikněte na kolekci zařízení, na kterých chcete skript spustit.
4. Vyberte kolekci, kterou jste vybrali, a klikněte na **Spustit skript**.
5. Na stránce **skript** v průvodci **spuštěním skriptu** vyberte ze seznamu skript. Zobrazují se jenom schválené skripty.
6. Klikněte na **Další**a pak dokončete průvodce.

> [!IMPORTANT]
> Pokud se skript nespustí, například v případě, že je cílové zařízení během jednoho hodiny vypnuté, musíte ho spustit znovu.

### <a name="target-machine-execution"></a>Provedení cílového počítače

Skript se spustí jako *systémový* nebo *počítačový* účet na cílových klientech. Tento účet má omezený přístup k síti. Každý přístup ke vzdáleným systémům a umístěním pomocí skriptu se musí zřídit odpovídajícím způsobem.

## <a name="script-monitoring"></a>Monitorování skriptů

Po zahájení spuštění skriptu na kolekci zařízení použijte následující postup k monitorování operace. Můžete sledovat skript v reálném čase, když se spustí, a později se vrátit ke stavu a výsledkům pro dané spuštění skriptu spuštění. Data stavu skriptu se vyčistí v rámci [úlohy Odstranit zastaralou správu operací klienta](../../core/servers/manage/reference-for-maintenance-tasks.md) nebo odstranění skriptu.<br>

![Sledování skriptů – stav spuštění skriptu](./media/run-scripts/RS-monitoring-three-bar.png)

1. V konzole Configuration Manager klikněte na **monitorování**.
2. V pracovním prostoru **monitorování** klikněte na **stav skriptu**.
3. V seznamu **stav skriptu** zobrazíte výsledky pro každý skript, který jste spustili v klientských zařízeních. Kód ukončení skriptu **0** obecně znamená, že skript byl úspěšně spuštěn.

 
   ![Sledování skriptů – zkrácený skript](./media/run-scripts/Script-monitoring-truncated.png)

## <a name="script-output"></a>Výstup skriptu

Výstup vráceného skriptu klienta pomocí formátování JSON, protože výsledky skriptu převede do rutiny [ConvertTo-JSON](/powershell/module/microsoft.powershell.utility/convertto-json) . Formát JSON konzistentně vrátí čitelný výstup skriptu. Pro skripty, které nevracejí objekty jako výstup, rutina ConvertTo-JSON převede výstup na jednoduchý řetězec, který vrátí klient místo JSON.  

- Skripty, které získají Neznámý výsledek nebo kde byl klient offline, se nezobrazí v grafech nebo sadě dat. <!--507179-->
- Vyhněte se vrácení výstupu velkých skriptů, protože se zkrátí na 4 KB. <!--508488-->
- Převeďte objekt enum na řetězcovou hodnotu ve skriptech, aby byly správně zobrazeny ve formátu JSON. <!--508377-->

   ![Převést objekt enum na hodnotu Sting](./media/run-scripts/enum-tostring-JSON.png)

Podrobný výstup skriptu můžete zobrazit v nezpracovaném nebo strukturovaném formátu JSON. Toto formátování usnadňuje čtení a analýzu výstupu. Pokud skript vrátí platný text ve formátu JSON nebo ho můžete převést na JSON pomocí rutiny prostředí PowerShell [ConvertTo-JSON](/powershell/module/microsoft.powershell.utility/convertto-json) a pak zobrazit podrobný výstup buď jako **výstup JSON** , nebo jako **nezpracovaný výstup**. V opačném případě je jediným z možností **výstup skriptu**.

### <a name="example-script-output-is-convertible-to-valid-json"></a>Příklad: výstup skriptu je převoditelný na platný formát JSON.

Systému `$PSVersionTable.PSVersion`  

``` Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

### <a name="example-script-output-isnt-valid-json"></a>Příklad: výstup skriptu není platný formát JSON.

Systému `Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

``` Output
Microsoft Windows 10 Enterprise
```

## <a name="log-files"></a>Soubory protokolu

- Na straně klienta ve výchozím nastavení v C:\Windows\CCM\logs:  
  - **Skripty. log**  
  - **CcmMessaging.log**  

- V MP ve výchozím nastavení v C:\ SMS_CCM \Logs.:
  - **MP_RelayMsgMgr. log**  

- Na serveru lokality ve výchozím nastavení C:\Program Files\Configuration Manager\Logs:
  - **SMS_Message_Processing_Engine. log**

## <a name="see-also"></a>Viz také

- [Konfigurace správy na základě rolí pro Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [Základy správy na základě rolí](../../core/understand/fundamentals-of-role-based-administration.md)