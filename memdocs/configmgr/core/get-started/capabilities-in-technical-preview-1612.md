---
title: Možnosti ve verzi Technical Preview 1612
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview pro Configuration Manager verze 1612.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bceab2e8-2f05-4a17-9ac8-a7a558670fb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9cd0df25c64c4ca1e0d2ce98de5d2915f7564241
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693025"
---
# <a name="capabilities-in-technical-preview-1612-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1612 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*



V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1612. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview. Před instalací této verze Technical Preview si Projděte úvodní téma, [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md), abyste se seznámili se základními požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.    


**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  

## <a name="the-data-warehouse-service-point"></a>Bod služby datového skladu
Počínaje verzí Technical Preview 1612 vám bod služeb datového skladu umožňuje ukládat a vytvářet sestavy o dlouhodobých historických datech pro nasazení Configuration Manager. To se provádí automatizovanými synchronizacemi z databáze Configuration Manager lokality do databáze datového skladu. Tyto informace jsou pak přístupné z vašeho bodu služby Reporting Services.

Když nainstalujete novou roli systému lokality, ve výchozím nastavení Configuration Manager vytvoří databázi datového skladu na základě SQL Server instance, kterou zadáte. Datový sklad podporuje až 2 TB dat s časovými razítky pro sledování změn.  Ve výchozím nastavení data synchronizovaná z databáze lokality obsahují skupiny dat pro globální data, data lokality, Global_Proxy, cloudová data a databázová zobrazení. Můžete také upravit, co je synchronizované, aby zahrnovalo další tabulky, nebo vyloučit konkrétní tabulky z výchozích replikačních sad.
Synchronizovaná výchozí data obsahují informace o:
- Stav infrastruktury
- Zabezpečení
- Dodržování předpisů
- Malware   
- Nasazení softwaru
- Podrobnosti inventáře (ale historie inventáře není synchronizovaná)

Kromě instalace a konfigurace databáze datového skladu je nainstalována řada nových sestav, abyste mohli snadno vyhledat a ohlásit tato data.

### <a name="data-warehouse-dataflow"></a>Tok dat datového skladu   
![Datawarehouse_flow](./media/datawarehouse.png)

| Krok         | Podrobnosti  |
|:------:|-----------|  
| **1** | Server lokality přenáší a ukládá data v databázi lokality.  |  
| **2** | V závislosti na plánu a konfiguraci získá bod služby datového skladu data z databáze lokality.  |  
| **3** | Bod služeb datového skladu přenáší a ukládá kopii synchronizovaných dat v databázi datového skladu. |  
| **A** | Pomocí předdefinovaných sestav se vytvoří žádost o data, která se předají do bodu služby Reporting Services pomocí SQL Server Reporting Services. |  
| **B** | Většina sestav je pro aktuální informace a tyto požadavky se spouštějí v databázi lokality. |  
| **R** | Když sestava vyžádá historická data pomocí jedné ze sestav s *kategorií* **datového skladu**, požadavek se spustí pro databázi datového skladu.   |  

### <a name="prerequisites-for-the-data-warehouse-service-point-and-database"></a>Předpoklady pro bod služby a databázi datového skladu
- Vaše hierarchie musí mít nainstalovanou roli systému lokality bodu služby Reporting Services.
- Počítač, na který instalujete roli systému lokality, vyžaduje .NET Framework 4.5.2 nebo novější.
- Počítačový účet počítače, na který nainstalujete roli systému lokality, musí mít oprávnění místního správce k počítači, který bude hostovat databázi datového skladu.
- Účet pro správu, který použijete k instalaci role systému lokality, musí být DBO na instanci SQL Server, která bude hostovat databázi datového skladu.  
- Databáze je podporována:
  - S SQL Server 2012 nebo novějším, edice Enterprise nebo Datacenter Edition.
  - Ve výchozí nebo pojmenované instanci
  - V *clusteru SQL Server*. I když by tato konfigurace měla fungovat, neotestovala se a podpora je nejlepší úsilí.
  - Pokud je umístěn společně s databází lokality nebo bodem služby Reporting Services. Doporučujeme však, aby byl nainstalován na samostatném serveru.  
- Účet, který se používá jako *účet bodu služby Reporting Services* , musí mít oprávnění **db_datareader** k databázi datového skladu.  
- Databáze není ve *skupině dostupnosti AlwaysOn SQL Server*podporovaná.

### <a name="install-the-data-warehouse"></a>Instalace datového skladu
Roli systému lokality datového skladu nainstalujete do lokality centrální správy nebo do primární lokality pomocí **Průvodce přidáním rolí systému lokality** nebo **Průvodce vytvořením serveru systému lokality**. Další informace najdete v tématu [Instalace rolí systému lokality](../servers/deploy/configure/install-site-system-roles.md) . Hierarchie podporuje víc instancí této role, ale v každé lokalitě je podporovaná jenom jedna instance.  

Při instalaci role Configuration Manager vytvoří databázi datového skladu pro vás na instanci SQL Server, kterou zadáte. Pokud zadáte název existující databáze (jak byste to provedli, když [přesunete databázi datového skladu do nové SQL Server](#move-the-data-warehouse-database)), Configuration Manager nevytvoří novou databázi, ale místo toho použije vámi zadanou.

#### <a name="configurations-used-during-installation"></a>Konfigurace používané při instalaci
K dokončení instalace role systému lokality použijte následující informace:

Stránka pro **Výběr systémové role** :  
Předtím, než Průvodce zobrazí možnost vybrat a nainstalovat bod služby datový sklad, je nutné nainstalovat bod služby Reporting Services.

**Obecná** stránka: vyžadují se tyto obecné informace:
- **Nastavení databáze Configuration Manager:**   
  - **Název serveru** – zadejte plně kvalifikovaný název domény serveru, který je hostitelem databáze lokality. Pokud nepoužíváte výchozí instanci SQL Server, je nutné zadat instanci za plně kvalifikovaným názvem domény v následujícím formátu: *** &lt; Sqlserver_FQDN>\& lt; Instance_name>***
  - **Název databáze** – zadejte název databáze lokality.
  - **Ověřit** – klikněte na **ověřit** a ujistěte se, že připojení k databázi lokality je úspěšné.
</br></br>
- **Nastavení databáze datového skladu:**
  - **Název serveru** – zadejte plně kvalifikovaný název domény serveru, který je hostitelem bodu služby a databáze datového skladu. Pokud nepoužíváte výchozí instanci SQL Server, je nutné zadat instanci za plně kvalifikovaným názvem domény v následujícím formátu: *** &lt; Sqlserver_FQDN>\& lt; Instance_name>***
  - **Název databáze** – zadejte plně kvalifikovaný název domény pro databázi datového skladu.  Configuration Manager vytvoří databázi s tímto názvem. Pokud zadáte název databáze, který již existuje v instanci systému SQL Server, Configuration Manager použije tuto databázi.
  - **Ověřit** – klikněte na **ověřit** a ujistěte se, že připojení k databázi lokality je úspěšné.

Stránka **Nastavení synchronizace** :   
- **Nastavení dat:**
  - **Replikační skupiny, které se mají synchronizovat** – vyberte skupiny dat, které chcete synchronizovat. Informace o různých typech datových skupin najdete v tématu [replikace databáze](../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep) a **distribuovaná zobrazení** v [přenosech dat mezi lokalitami](../plan-design/hierarchy/data-transfers-between-sites.md).
  - **Tabulky zahrnuté do synchronizace** – zadejte název každé další tabulky, kterou chcete synchronizovat. Pomocí čárky oddělte více tabulek. Tyto tabulky budou kromě vybraných skupin replikace synchronizovány z databáze lokality.
  - **Tabulky vyloučené do synchronizace** – zadejte názvy jednotlivých tabulek z replikačních skupin, které synchronizujete. Tabulky, které zadáte, budou vyloučeny z. Pomocí čárky oddělte více tabulek.
- **Nastavení synchronizace:**
  - **Interval synchronizace (minuty)** – zadejte hodnotu v minutách. Po dosažení intervalu se spustí nová synchronizace. To podporuje rozsah od 60 do 1440 minut (24 hodin).
  - **Plán** – zadejte dny, ve kterých má být synchronizace spuštěna.

**Přístup k bodu hlášení**:   
Po instalaci role datový sklad ověřte, že účet, který se používá jako *účet bodu služby Reporting Services* , má oprávnění **db_datareader** k databázi datového skladu.

#### <a name="troubleshoot-installation-and-data-synchronization"></a>Řešení potíží při instalaci a synchronizaci dat
Pomocí následujících protokolů můžete prozkoumat problémy s instalací bodu služby datového skladu nebo synchronizace dat:
- **DWSSMSI. log** a **DWSSSetup. log**  – pomocí těchto protokolů můžete prozkoumat chyby při instalaci bodu služby datového skladu.
- **Microsoft.ConfigMgrDataWarehouse. log** – pomocí tohoto protokolu můžete prozkoumat synchronizaci dat mezi databází lokality a databází datového skladu.

### <a name="reporting"></a>Vytváření sestav
Po instalaci role systému lokality datového skladu jsou v bodu služby Reporting Services k dispozici následující sestavy s *kategorií* **datového skladu:**

|Sestava                   | Podrobnosti                                  |
|-------------------------|------------------------------------------|
| **Sestava nasazení aplikace** | Zobrazí podrobnosti o nasazení aplikace pro konkrétní aplikaci a počítač.|
| **Sestava Update Compliance Endpoint Protection a softwaru**   | Zobrazí počítače, ve kterých chybí aktualizace softwaru.|
| **Obecná sestava inventáře hardwaru**  | Zobrazení veškerého inventáře hardwaru pro určitý počítač.|
| **Obecná sestava inventáře softwaru**  | Zobrazit všechny inventáře softwaru pro určitý počítač.|
| **Přehled stavu infrastruktury**  |Zobrazuje přehled stavu infrastruktury Configuration Manager.|
| **Seznam zjištěného malwaru**  |Zobrazení malwaru zjištěného v organizaci.|
| **Souhrnná sestava distribuce softwaru** | Shrnutí distribuce softwaru pro konkrétní reklamu a počítač.|

### <a name="move-the-data-warehouse-database"></a>Přesunutí databáze datového skladu
K přesunutí databáze datového skladu do nové SQL Server použijte následující postup:

1. Zkontrolujte aktuální konfiguraci databáze a zaznamenejte podrobnosti konfigurace, včetně:  
   - Skupiny dat, které synchronizujete
   - Tabulky, které zahrnete nebo vyloučíte ze synchronizace       

   Po obnovení databáze na nový server a opětovné instalaci role systému lokality překonfigurujete tyto skupiny dat a tabulky.  

2. K zálohování databáze datového skladu použijte SQL Server Management Studio a pak znovu obnovte tuto databázi na SQL Server na novém počítači, který bude hostovat datový sklad.

   Po obnovení databáze na nový server zajistěte, aby byla přístupová oprávnění k databázi stejná na nové databázi datového skladu, stejně jako v původní databázi datového skladu.

3. K odebrání role systému lokality bodu služby datového skladu z aktuálního serveru použijte konzolu Configuration Manager.

4. Nainstalujte nový bod služby datového skladu a zadejte název nové SQL Server a instance, která je hostitelem databáze datového skladu, kterou jste obnovili.

5. Po instalaci role systému lokality se přesun dokončí.

Můžete zkontrolovat následující protokoly Configuration Manager a potvrdit tak, že byla role systému lokality úspěšně přeinstalována:  
- **DWSSMSI. log** a **DWSSSetup. log**  – pomocí těchto protokolů můžete prozkoumat chyby při instalaci bodu služby datového skladu.
- **Microsoft.ConfigMgrDataWarehouse. log** – pomocí tohoto protokolu můžete prozkoumat synchronizaci dat mezi databází lokality a databází datového skladu.


## <a name="content-library-cleanup-tool"></a>Nástroj pro vyčištění knihovny obsahu
Počínaje verzí Technical Preview 1612 můžete pomocí nového nástroje příkazového řádku (**ContentLibraryCleanup.exe**) odebrat obsah, který už není přidružený k žádnému balíčku nebo aplikaci, z distribučního bodu (osamocený obsah). Tento nástroj se nazývá nástroj pro vyčištění knihovny obsahu.

Tento nástroj ovlivňuje pouze obsah v distribučním bodu, který zadáte při spuštění nástroje, a nemůže odebrat obsah z knihovny obsahu na serveru lokality.

Po instalaci Technical Preview 1612 můžete najít **ContentLibraryCleanup.exe** ve složce *% CM_Installation_Path% \ CD. latest\SMSSETUP\TOOLS\ContentLibraryCleanup \* na serveru lokality Technical Preview.

Nástroj vydaný v této verzi Technical Preview má nahradit starší verze podobných nástrojů vydaných pro dřívější Configuration Manager produkty. I když tato verze nástroje přestane fungovat po 1. březnu 2017, budou nové verze vydávány s budoucími technickými náhledy až do doby, kdy se tento nástroj uvolní jako součást Current Branch, nebo mimo provoz, který je připravený pro vzdálenou verzi.

### <a name="requirements"></a>Požadavky  
- Nástroj lze spustit přímo v počítači, který je hostitelem distribučního bodu, nebo vzdáleně z jiného serveru. Nástroj lze spustit pouze proti jednomu distribučnímu bodu v jednom okamžiku.
- Uživatelský účet, který spouští nástroj, musí mít oprávnění pro správu na základě rolí, která jsou shodná s úplným správcem v hierarchii Configuration Manager.  Nástroj nefunguje, když je uživatelský účet udělen jako člen skupiny zabezpečení systému Windows, který má oprávnění správce s úplnými oprávněními.

### <a name="modes-of-operation"></a>Režimy činností
Nástroj lze spustit ve dvou režimech:
1. **Režim citlivosti**:   
   Pokud nezadáte přepínač **/Delete** , nástroj se spustí v režimu s akcemi a určí obsah, který by se odstranil z distribučního bodu, ale ve skutečnosti neodstraní žádná data.

   - Když se nástroj v tomto režimu spustí, informace o obsahu, který se má odstranit, se automaticky zapisují do souboru protokolu nástroje. Uživateli se nezobrazí výzva k potvrzení všech potenciálních odstranění.
   - Ve výchozím nastavení se soubor protokolu zapisuje do dočasné složky uživatele v počítači, na kterém nástroj spustíte, ale můžete použít přepínač/log pro přesměrování souboru protokolu do jiného umístění.  
   </br>

   Doporučujeme spustit nástroj v tomto režimu a zkontrolovat výsledný soubor protokolu před spuštěním nástroje s přepínačem/DELETE.  

2. **Režim odstranění**: když nástroj spustíte s přepínačem **/Delete** , nástroj se spustí v režimu odstranění.

   - Když se nástroj v tomto režimu spustí, může se z knihovny obsahu distribučního bodu odstranit osamocený obsah, který se nachází v zadaném distribučním bodě.
   -  Před odstraněním každého souboru se uživateli zobrazí výzva k potvrzení, že by se měl soubor odstranit.  Pokud chcete přeskočit další výzvy a odstranit veškerý osamocený obsah, můžete vybrat **Y** pro Ano, **N** nebo **Ano** .  
   </br>

   Doporučujeme, abyste tento nástroj spustili v režimu co-if a zkontrolovali výsledný soubor protokolu ještě předtím, než nástroj spustíte s přepínačem/DELETE.  

Když nástroj pro vyčištění knihovny obsahu běží v obou režimech, automaticky vytvoří protokol s názvem, který obsahuje režim, ve kterém se nástroj spouští, název distribučního bodu, datum a čas operace. Po dokončení nástroje se soubor protokolu automaticky otevře. Ve výchozím nastavení se tento protokol zapíše do **dočasné** složky uživatele v počítači, na kterém jste nástroj spustili. pomocí přepínače příkazového řádku můžete přesměrovat soubor protokolu na jiné místo, včetně síťové sdílené složky.   


### <a name="run-the-tool"></a>Spusťte nástroj.
Spuštění nástroje:
1. Otevřete příkazový řádek pro správu do složky, která obsahuje **ContentLibraryCleanup.exe**.  
2. Dále zadejte příkazový řádek, který obsahuje požadované přepínače příkazového řádku a volitelné přepínače, které chcete použít.

**Známý problém** Při spuštění nástroje může dojít k chybě, která by mohla být vrácena, když dojde k selhání balíčku nebo nasazení, nebo když probíhá:
-  *System. InvalidOperationException: tuto knihovnu obsahu nejde vyčistit hned teď, protože balíček \<packageID> není úplně nainstalovaný.*

**Alternativní řešení:** Žádné. Nástroj nemůže spolehlivě identifikovat osamocené soubory, když probíhá zpracování obsahu nebo se nepovedlo ho nasadit. Nástroj proto nebude umožňovat vyčištění obsahu, dokud tento problém nebude vyřešen.



### <a name="command-line-switches"></a>Přepínače příkazového řádku  
Následující přepínače příkazového řádku je možné použít v libovolném pořadí.   

|Přepínač|Podrobnosti|
|---------|-------|
|**/Delete**  |**Volitelné** </br> Tento přepínač použijte, pokud chcete odstranit obsah z distribučního bodu. Zobrazí se výzva před odstraněním obsahu. </br></br> Pokud tento přepínač nepoužijete, nástroj protokoluje výsledky o tom, jaký obsah by se odstranil, ale neodstraní žádný obsah z distribučního bodu. </br></br> Příklad: ***ContentLibraryCleanup.exe/dp Server1.contoso.com/Delete*** |
| **parametr**       |**Volitelné** </br> Spusťte nástroj v tichém režimu, který potlačí všechny výzvy (například výzvy při odstraňování obsahu), a neotevře soubor protokolu automaticky. </br></br> Příklad: ***ContentLibraryCleanup.exe/q/dp Server1.contoso.com*** |
| **&lt;název plně kvalifikovaného názvu domény distribučního bodu/dp>**  | **Požadováno** </br> Zadejte plně kvalifikovaný název domény (FQDN) distribučního bodu, který chcete vyčistit. </br></br> Příklad:  ***ContentLibraryCleanup.exe/dp Server1.contoso.com***|
| **&lt;>plně kvalifikovaný název domény primární lokality/PS**       | **Volitelné** při čištění obsahu z distribučního bodu v primární lokalitě.</br>**Požadováno** při čištění obsahu z distribučního bodu v sekundární lokalitě. </br></br> Zadejte plně kvalifikovaný název domény primární lokality, do které distribuční bod patří, nebo nadřazeného primárního nadřazeného objektu, pokud je distribuční bod v sekundární lokalitě. </br></br> Příklad: ***ContentLibraryCleanup.exe/dp Server1.contoso.com/ps siteserver1.contoso.com*** |
| **&lt;>kódu pro/SC primární lokalitu**  | **Volitelné** při čištění obsahu z distribučního bodu v primární lokalitě.</br>**Požadováno** při čištění obsahu z distribučního bodu v sekundární lokalitě. </br></br> Zadejte kód lokality primární lokality, ke které distribuční bod patří, nebo nadřazenou primární lokalitu, pokud je distribuční bod v sekundární lokalitě.</br></br> Příklad: ***ContentLibraryCleanup.exe/dp Server1.contoso.com/SC ABC*** |
| **/log \<log file directory>**       |**Volitelné** </br> Zadejte adresář, do kterého se mají umístit soubory protokolu. Může to být místní disk nebo sdílená síťová složka.</br></br> Pokud tento přepínač nepoužijete, soubory protokolu se automaticky umístí do dočasné složky Uživatelé.</br></br> Příklad místní jednotky: ***ContentLibraryCleanup.exe/dp Server1.contoso.com/log C:\Users\Administrator\Desktop*** </br></br>Příklad sdílené síťové složky: ***ContentLibraryCleanup.exe/dp Server1.contoso.com/log \\ &lt; share>\& lt; složka>***|


## <a name="improvements-for-in-console-search"></a>Vylepšení vyhledávání v konzole
Na základě názorů na hlas uživatele jsme do prohledávání v konzole přidali následující vylepšení:
- **Cesta k objektu:**  
  Řada objektů nyní podporuje nový sloupec s názvem **cesta k objektu**.  Při hledání a zahrnutí tohoto sloupce do výsledků zobrazení můžete zobrazit cestu k jednotlivým objektům. Například pokud spustíte hledání aplikací v uzlu aplikace a také prohledáváte v poduzlech, sloupec *cesta objektu* v podokně výsledků zobrazí cestu k jednotlivým vráceným objektům.   

- **Zachování hledaného textu:**  
  Když zadáte text do textového pole Hledat a potom převedete mezi hledáním poduzlu a aktuálního uzlu, text, který zadáte, zůstane zachován a zůstane k dispozici pro nové hledání bez nutnosti jeho opětovného zadání.

- **Zachování vašeho rozhodnutí pro hledání poduzlů:**  
  Možnost, kterou vyberete pro hledání *aktuálního uzlu* nebo *všech podřízených uzlů* , nyní přetrvává při změně uzlu, ve kterém pracujete.   Toto nové chování znamená, že nemusíte při přesunu kolem konzoly trvale vynulovat rozhodnutí.  Ve výchozím nastavení, když otevřete konzolu, možnost bude prohledávat pouze aktuální uzel.

## <a name="prevent-installation-of-an-application-if-a-specified-program-is-running"></a>Zabrání instalaci aplikace, pokud je spuštěný určitý program.
Nyní můžete nakonfigurovat seznam spustitelných souborů (s příponou. exe) ve vlastnostech typu nasazení, které při spuštění zablokují instalaci aplikace. Po pokusu o instalaci se uživatelům zobrazí dialogové okno s výzvou, aby zavřeli procesy blokující instalaci.

### <a name="try-it-out"></a>Vyzkoušet
Konfigurace seznamu spustitelných souborů
1. Na stránce vlastnosti libovolného typu nasazení vyberte kartu **zpracování instalačního programu** .
2. Kliknutím na **Přidat**přidejte do seznamu jeden z dalších spustitelných souborů (například **Edge.exe**).
3. Kliknutím na tlačítko **OK** zavřete dialogové okno Vlastnosti typu nasazení.

Když teď nasadíte tuto aplikaci na uživatele nebo zařízení a spustí se jedna z vámi přidaných spustitelných souborů, zobrazí se mu dialogové okno Centrum softwaru, které jim oznámí, že se instalace nezdařila, protože aplikace je spuštěná.

## <a name="new-windows-hello-for-business-notification-for-end-users"></a>Nové oznámení Windows Hello pro firmy pro koncové uživatele

Nové oznámení Windows 10 informuje koncové uživatele o tom, že musí podniknout další kroky k dokončení nastavení Windows Hello pro firmy (například nastavení PIN kódu).

## <a name="windows-store-for-business-support-in-configuration-manager"></a>Podpora Windows Storu pro firmy v Configuration Manager

Nyní můžete nasadit licencované aplikace online s účelem nasazení **dostupným** z Windows Storu pro firmy do počítačů, na kterých běží klient Configuration Manager.
Další podrobnosti najdete v tématu [Správa aplikací z Windows Storu pro firmy pomocí Configuration Manager](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

Podpora pro tuto funkci je aktuálně dostupná jenom pro počítače, na kterých běží Build Windows 10 RS2 ve verzi Preview.

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Vrátit se na předchozí stránku, když pořadí úkolů dojde k chybě
Při spuštění pořadí úkolů se teď můžete vrátit na předchozí stránku a dojde k selhání. Před touto verzí jste museli pořadí úkolů restartovat, pokud došlo k selhání. Například můžete použít tlačítko **Předchozí** v následujících scénářích:

- Když se počítač spustí v prostředí Windows PE, může se dialogové okno spuštění pořadí úkolů zobrazit předtím, než bude pořadí úkolů k dispozici. Když v tomto scénáři kliknete na další, na poslední stránce pořadí úkolů se zobrazí zpráva, že nejsou k dispozici žádná pořadí úkolů. Nyní můžete kliknutím na tlačítko **Předchozí** Hledat v dostupných pořadích úloh znovu. Tento postup můžete opakovat až do chvíle, kdy je pořadí úkolů k dispozici.
- Když spouštíte pořadí úkolů, ale závislé balíčky obsahu ještě nejsou v distribučních bodech k dispozici, pořadí úkolů se nezdařilo. Nyní můžete distribuovat chybějící obsah (Pokud ještě nebyl distribuován) nebo počkat, až bude obsah k dispozici v distribučních bodech, a potom kliknutím na tlačítko **Předchozí** vyhledáte znovu pořadí úloh pro daný obsah.

## <a name="express-installation-files-support-for-windows-10-updates"></a>Podpora souborů Expresní instalace pro aktualizace Windows 10
Přidali jsme podporu souborů Expresní instalace v Configuration Manager pro aktualizace Windows 10. Když použijete podporovanou verzi Windows 10, můžete teď použít nastavení Configuration Manager ke stažení jenom rozdílů mezi kumulativní aktualizací Windows 10 aktuálního měsíce a aktualizací z předchozího měsíce. V současné době v Configuration Manager Current Branch se každý měsíc stáhne celá kumulativní aktualizace Windows 10 (včetně všech aktualizací z předchozích měsíců). Použití souborů Expresní instalace poskytuje menší soubory ke stažení a rychlejší instalaci u klientů.

> [!IMPORTANT]
> I když je v Configuration Manager dostupná nastavení pro podporu použití souborů Expresní instalace, je tato funkce podporovaná jenom ve Windows 10 verze 1607 s aktualizací agenta web Windows Update, která se dodává s aktualizacemi vydanými 10. ledna 2017 (patch úterý). Další informace o těchto aktualizacích najdete v [článku o podpoře 3213986](https://support.microsoft.com/help/4009938/january-10-2017-kb3213986-os-build-14393-693). Můžete využít výhod souborů Expresní instalace při vydání další sady aktualizací od 14. února 2017. Windows 10 verze 1607 bez aktualizace a předchozí verze nepodporují soubory Expresní instalace.


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates-on-the-server"></a>Povolení stažení souborů Expresní instalace pro aktualizace Windows 10 na serveru
Chcete-li zahájit synchronizaci metadat pro instalační soubory systému Windows 10 Express, je nutné ji povolit ve vlastnostech bodu aktualizace softwaru.
1. V konzole Configuration Manager přejděte na **Správa**  >  **Konfigurace lokality**  >  **lokality**.
2. Vyberte lokalitu centrální správy nebo samostatnou primární lokalitu.
3. Na kartě **Domů** v části **Nastavení** klikněte na **Konfigurovat součásti pracoviště**a potom na možnost **Bod aktualizace softwaru**. Na kartě **soubory aktualizace** vyberte **Stáhnout úplné soubory pro všechny schválené aktualizace a soubory Expresní instalace pro Windows 10**.

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>Povolení podpory pro klienty ke stažení a instalaci souborů Expresní instalace
Pokud chcete povolit podporu souborů Expresní instalace na klientech, musíte povolit soubory Expresní instalace na klientských počítačích v části aktualizace softwaru v nastavení klienta. Tím se vytvoří nový naslouchací proces HTTP, který naslouchá požadavkům na stažení souborů Expresní instalace na portu, který zadáte. Když nasadíte nastavení klienta, abyste tuto funkci mohli na klientovi povolit, zkusíme stáhnout rozdíl mezi kumulativní aktualizací Windows 10 v aktuálním měsíci a aktualizací z předchozího měsíce (na klientech musí běžet verze Windows 10, která podporuje soubory Expresní instalace).
1. Povolte podporu souborů Expresní instalace ve vlastnostech komponenty bodu aktualizace softwaru (předchozí postup).
2. V konzole Configuration Manager přejděte na **Správa**  >  **nastavení klienta**.
3. Vyberte odpovídající nastavení klienta a pak na kartě **Domů** klikněte na **vlastnosti**.
4. Vyberte stránku **aktualizace softwaru** , nakonfigurujte **Ano** pro nastavení **Povolit instalaci expresních aktualizací na** klientech a NAKONFIGURUJTE port používaný naslouchacím programem http na klientovi pro port, který se **používá ke stahování obsahu pro nastavení expresní aktualizace** .


## <a name="odata-endpoint-data-access"></a>Přístup k datům koncového bodu OData

 Configuration Manager nyní poskytuje koncový bod RESTful OData pro přístup k datům Configuration Manager. Koncový bod je kompatibilní s protokolem OData verze 4, který umožňuje nástrojům, jako je Excel a Power BI, snadno přistupovat k datům Configuration Manager prostřednictvím jednoho koncového bodu. Technical Preview 1612 podporuje jenom přístup pro čtení k objektům v Configuration Manager.  

Data, která jsou aktuálně k dispozici v [zprostředkovateli rozhraní WMI Configuration Manager](../../develop/reference/configuration-manager-reference.md) , jsou teď přístupná i k novému koncovému bodu OData RESTful. Sady entit vystavené koncovým bodem OData umožňují vytvořit výčet pro stejná data, která můžete dotazovat pomocí zprostředkovatele rozhraní WMI.

### <a name="try-it-out"></a>Vyzkoušet

Než budete moct použít koncový bod OData, musíte ho pro lokalitu povolit.

1.  Přejít na **Administration**  >  **stránku Správa konfigurace lokality**  >  **lokality**.
2.  Vyberte primární lokalitu a klikněte na **vlastnosti**.
3.  Na kartě Obecné v seznamu vlastností primárního webového serveru klikněte na **Povolit koncový bod REST pro všechny poskytovatele v této lokalitě**a pak klikněte na **OK**.

V oblíbeném prohlížeči dotazů OData Vyzkoušejte dotazy podobné následujícím příkladům pro vrácení různých objektů v Configuration Manager:

| Účel | Dotaz OData |
|---|---|
| Získat všechny kolekce | `http://localhost/CMRestProvider/Collection` |
| Získat kolekci | `http://localhost/CMRestProvider/Collection('SMS00001')`
| Získat nejvyšší 100 zařízení v kolekci | `http://localhost/CMRestProvider/Collection('SMS00001')/Device?$top=100` |
| Získání zařízení s ID prostředku v kolekci | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)` |
| Získat operační systém zařízení v kolekci | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)/OPERATING_SYSTEM` |
| Získat uživatele v kolekci | `http://localhost/CMRestProvider/Collection('SMS00001')/User` |

> [!NOTE]
> Příklady dotazů zobrazených v tabulce používají *localhost* jako název hostitele v adrese URL a lze je použít na počítači, na kterém je spuštěný poskytovatel serveru SMS. Pokud spouštíte dotazy z jiného počítače, nahraďte localhost názvem FQDN serveru s nainstalovaným poskytovatelem serveru SMS.

## <a name="azure-active-directory-onboarding"></a>Azure Active Directory připojování

Při připojování Azure Active Directory (AD) se vytvoří připojení mezi Configuration Manager a Azure Active Directory, které budou používat jiné cloudové služby. Tuto možnost je teď možné použít k vytvoření připojení potřebného pro Brána pro správu cloudu.

Tuto úlohu můžete provést u správce Azure, protože budete potřebovat přihlašovací údaje správce Azure.

#### <a name="to-create-the-connection"></a>Vytvoření připojení:

2. V pracovním prostoru **Správa** vyberte možnost **Cloud Services**  >  **Azure Active Directory**  >  **Přidat Azure Active Directory**.
2. Vyberte **Přihlásit** se a vytvořte připojení ke službě Azure AD.

#### <a name="configuration-manager-client-requirements"></a>Configuration Manager požadavky klienta

K dispozici je několik požadavků na povolení vytváření zásad uživatele v Brána pro správu cloudu.

- Proces zprovoznění služby Azure AD musí být kompletní a klient musí být nejdřív připojený k podnikové síti, aby získal informace o připojení.
- Klienti musí být připojeni k doméně (registrováno ve službě Active Directory) a připojená k doméně (registrovaná v Azure AD).
- Je nutné spustit [zjišťování uživatele služby Active Directory](../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
- Je nutné upravit klienta Configuration Manager, aby povoloval požadavky na zásady uživatele prostřednictvím Internetu, a nasazovat změnu na klienta. Vzhledem k tomu, že tato změna klienta probíhá *na klientském zařízení*, může být nasazena prostřednictvím brána pro správu cloudu, i když jste nedokončili změny konfigurace, které jsou potřeba pro zásady uživatele.
- Váš bod správy musí být nakonfigurovaný tak, aby používal protokol HTTPS k zabezpečení tokenu v síti a musí mít nainstalované rozhraní .NET 4,5.

Po provedení těchto změn konfigurace můžete vytvořit zásadu uživatele a přesunout klienty na Internet a otestovat zásadu. Požadavky na zásady uživatele prostřednictvím Brána pro správu cloudu budou ověřeny pomocí ověřování založeného na tokenech Azure AD.

## <a name="change-to-configuring-multi-factor-authentication-for-device-enrollment"></a>Změna konfigurace služby Multi-Factor Authentication pro registraci zařízení

Teď, když můžete nastavit vícefaktorové ověřování (MFA) pro registraci zařízení v Azure Portal, možnost MFA byla v konzole Configuration Manager odebrána. Další informace o nastavení vícefaktorového ověřování pro registraci najdete [v tomto tématu Microsoft Intune](../../../intune/enrollment/multi-factor-authentication.md).