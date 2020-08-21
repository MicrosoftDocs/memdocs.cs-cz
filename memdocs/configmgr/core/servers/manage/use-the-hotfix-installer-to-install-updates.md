---
title: Instalační program oprav hotfix
titleSuffix: Configuration Manager
description: Zjistěte, kdy a jak nainstalovat aktualizace prostřednictvím instalačního programu oprav hotfix pro Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f3058277-c597-4dac-86d1-41b6f7e62b36
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8c5cc09b7c2723a5dbdd1030cb0053ae75b1ff22
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699462"
---
# <a name="use-the-hotfix-installer-to-install-updates-for-configuration-manager"></a>Instalace aktualizací pro Configuration Manager pomocí instalačního programu oprav hotfix

*Platí pro: Configuration Manager (Current Branch)*

Některé aktualizace Configuration Manager nejsou z cloudové služby Microsoftu k dispozici a jsou získány pouze mimo IP síť. Příkladem je omezené vydání opravy hotfix, která řeší konkrétní problém.   
Pokud musíte nainstalovat aktualizaci (nebo opravu hotfix), kterou jste obdrželi od společnosti Microsoft, a tato aktualizace má název souboru, který končí příponou **. exe** (ne **update.exe**), použijte instalační program oprav hotfix, který je součástí tohoto stažení opravy hotfix, a nainstalujte aktualizaci přímo na Configuration Manager Server lokality.  

Pokud má soubor opravy hotfix příponu souboru **.update.exe** , přečtěte si téma [použití nástroje pro registraci aktualizací k importu oprav hotfix do Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md).  

> [!NOTE]  
> V tomto tématu najdete obecné pokyny k instalaci oprav hotfix, které aktualizují Configuration Manager. Podrobnosti o konkrétní aktualizaci naleznete v příslušném článku ve znalostní bázi Knowledge Base (KB) na webu podpory společnosti Microsoft.  

##  <a name="overview-of-hotfixes-for-configuration-manager"></a><a name="bkmk_Overview"></a> Přehled oprav hotfix pro Configuration Manager  
Opravy hotfix pro Configuration Manager jsou podobné těm pro ostatní produkty Microsoftu, jako je například SQL Server, obsahují buď jednu jednotlivou opravu, nebo sadu prostředků (souhrn oprav) a jsou popsané v článku znalostní báze Microsoft Knowledge Base.  

Jednotlivé aktualizace obsahují jednu aktualizaci zaměřenou na konkrétní verzi Configuration Manager.  
Sady aktualizací obsahují víc aktualizací pro konkrétní verzi Configuration Manager.  
Pokud je oprava sadou, nemůžete z této sady instalovat jednotlivé aktualizace.  

Pokud ale plánujete vytvořit nasazení k instalaci aktualizací do dalších počítačů, musíte sadu aktualizací nainstalovat na server lokality centrální správy nebo na server primární lokality.  

Při spuštění sady aktualizací se stane toto:  

- Ze sady aktualizací se extrahují aktualizační soubory pro všechny příslušné komponenty.  

- Spustí se průvodce, který vás provede procesem konfigurace aktualizací a možnostmi nasazení pro aktualizace.  

- Po dokončení průvodce se aktualizace ze sady, které se vztahují k danému serveru lokality, nainstalují na server lokality.  

Průvodce také vytvoří nasazení, která můžete použít k instalaci aktualizací do dalších počítačů. Můžete nasadit aktualizace pro další počítače pomocí podporované metody nasazení, jako je balíček nasazení softwaru nebo Microsoft System Center Updates Publisher 2011.  

Když spustíte průvodce, vytvoří se soubor **.cab** na serveru lokality pro použití s nástrojem Updates Publisher 2011. Volitelně můžete nakonfigurovat průvodce tak, aby vytvořil také jeden nebo více balíčků pro nasazení softwaru. Tato nasazení můžete použít k instalaci aktualizací do součástí, například klientů nebo konzolu Configuration Manager. Aktualizace můžete nainstalovat také ručně na počítačích, které nepoužívají klienta Configuration Manager.  

Následující tři skupiny v Configuration Manager lze aktualizovat:  

- Configuration Manager role serveru, mezi které patří:  

  - Lokalita centrální správy  

  - Primární lokalita  

  - Sekundární lokalita  

  - Vzdálený poskytovatel služby SMS  

- Konzola nástroje Configuration Manager  

- Klient Configuration Manager  

> [!NOTE]  
> **Aktualizace rolí systému lokality** (včetně aktualizací databáze lokality a cloudových distribučních bodů) se instalují jako součást aktualizace pro servery lokality a služby nástrojem Site Component Manager.  
>   
> Aktualizace distribučních bodů pro vyžádání obsahu je však služba distribuována správcem distribuce místo správce součástí lokality.  

Každá sada aktualizací pro Configuration Manager je samorozbalovací soubor. exe (SFX), který obsahuje soubory potřebné k instalaci aktualizace pro příslušné součásti Configuration Manager. Soubor SFX obvykle obsahuje následující soubory:  

|Soubor|Podrobnosti|  
|----------|-------------|  
|&lt;Verze produktu \> -QFE-KB – &lt; ID článku KB \> - &lt; platforma \> - &lt; Language \> . exe|Toto je aktualizační soubor. Příkazový řádek tohoto souboru je řízen souborem Updatesetup.exe.<br /><br /> Příklad:<br />CM1511RTM-QFE-KB123456-X64-ENU.exe|  
|Updatesetup.exe|Tato schránka .msi řídí instalaci sady aktualizací.<br /><br /> Po spuštění aktualizace zjistí soubor Updatesetup.exe jazyk zobrazení v počítači, v němž je spuštěn. Výchozím jazykem rozhraní aktualizace je angličtina. Pokud je však podporován jazyk zobrazení nastavený v počítači, zobrazí se uživatelské rozhraní v místním jazyce počítače.|  
|License_&lt;jazyk\>.rtf|V případě potřeby obsahuje aktualizace jeden nebo více souborů s licencemi v podporovaných jazycích.|  
|&lt;Produkt&typ aktualizace> – &lt; verze produktu \> - &lt; ID článku znalostní báze Knowledge Base \> - &lt; \> . msp|Pokud se aktualizace vztahuje na Configuration Manager konzolu nebo klienty, obsahuje sada aktualizací samostatné soubory Instalační služba systému Windows opravy (. msp).<br /><br /> Příklad:<br /><br /> **Aktualizace konzoly nástroje Configuration Manager:** ConfigMgr1511-AdminUI-KB1234567-i386.msp<br /><br /> **Aktualizace klienta:** ConfigMgr1511-client-KB1234567-i386. msp<br />ConfigMgr1511-client-KB1234567-x64. msp|  

Sada aktualizací standardně zaznamenává svou činnost do souboru .log na serveru lokality. Soubor protokolu má stejný název jako sada aktualizací a je zapsaný ve složce **%SystemRoot%/Temp** .  

Jakmile spustíte sadu aktualizací, extrahuje soubor se stejným názvem, jako je název sady aktualizací, do dočasné složky v počítači a poté spustí program Updatesetup.exe. Updatesetup.exe spustí aktualizaci softwaru pro Configuration Manager v &lt; \> &lt; Průvodci číslo verze KB produktu \> .  

V případě rozsahu aktualizace vytvoří průvodce řadu složek v rámci instalační složky Configuration Manager na serveru lokality. Struktura složek má následující podobu:   
** \\ \\ &lt; Název serveru \> \ SMS_ &lt; kód lokality \> \HotFix \\ &lt; KB \> \\ &lt; typ aktualizace \> \\ &lt; platforma \> **.  

Podrobnosti o složkách v této struktuře naleznete v následující tabulce:  

|Název složky|Další informace|  
|-----------------|----------------------|  
|&lt;Název serveru\>|Název serveru lokality, kde spouštíte sadu aktualizací.|  
|&lt;Kód SMS_ lokality\>|Toto je název sdílené složky Configuration Manager instalační složky.|  
|&lt;Číslo KB\>|ID článku k této sadě aktualizací ve znalostní bázi Knowledge Base.|  
|&lt;Typ aktualizace\>|Jedná se o typy aktualizací Configuration Manager. Průvodce vytvoří samostatnou složku pro každý typ aktualizace obsažené v sadě aktualizací. Názvy složek reprezentují typy aktualizací. Jsou to tyto:<br /><br /> **Server**: obsahuje aktualizace serverů lokality, serverů databáze lokality a počítačů, v nichž je spuštěný poskytovatel serveru SMS.<br /><br /> **Klient**: obsahuje aktualizace klienta Configuration Manager.<br /><br /> **AdminConsole**: obsahuje aktualizace konzoly Configuration Manager.<br /><br /> Kromě výše uvedených typů aktualizací vytvoří průvodce složku s názvem **SCUP**. Tato složka nezastupuje žádný typ aktualizace, ale obsahuje soubor .cab pro Updates Publisher.|  
|&lt;Platforma\>|Složka specifická pro konkrétní platformu. Obsahuje aktualizační soubory specifické pro daný typ procesoru.  Mezi tyto složky patří:<br /><br />– x64<br /><br /> – I386|  

##  <a name="how-to-install-updates"></a><a name="bkmk_Install"></a> Postup instalace aktualizací  
Chcete-li instalovat aktualizace, je třeba nejprve nainstalovat sadu aplikací na server lokality. Instalujete-li sadu aktualizací, spustí se průvodce instalací pro tuto aktualizaci. Průvodce provede následující úlohy:  

- Extrahuje aktualizační soubory  

- Pomůže vám nakonfigurovat nasazení  

- Nainstaluje příslušné aktualizace do součástí serveru místního počítače  

Po instalaci sady aktualizací na server lokality můžete aktualizovat další součásti pro Configuration Manager. Následující tabulka popisuje aktualizační úlohy pro různé součásti:  

|Součást|Pokyny|  
|---------------|------------------|  
|Server lokality|Nasazení aktualizací na vzdálený server lokality (pokud jste nezvolili instalaci sady aktualizací přímo na tento vzdálený server lokality).|  
|Databáze lokality|U vzdálených serverů lokality nasazení aktualizací serveru, které obsahují aktualizaci databáze lokality (pokud neinstalujete sadu aktualizací přímo na tento vzdálený server lokality).|  
|Konzola nástroje Configuration Manager|Po počáteční instalaci konzoly Configuration Manager můžete nainstalovat aktualizace pro konzolu Configuration Manager na každém počítači, na kterém je spuštěna konzola nástroje. Instalační soubory konzoly Configuration Manager nelze změnit tak, aby se aktualizace nainstalovaly během úvodní instalace konzoly nástroje.|  
|Vzdálený poskytovatel služby SMS|Instalace aktualizací pro všechny instance poskytovatele služby SMS, který se spouští v jiných počítačích, než je server lokality, do nějž jste nainstalovali sadu aktualizací.|  
|Configuration Manager klienti|Po počáteční instalaci klienta Configuration Manager můžete nainstalovat aktualizace pro klienta Configuration Manager na každý počítač, na kterém je spuštěný klient nástroje.|  

> [!NOTE]  
> Aktualizace lze nasadit pouze do počítačů, v nichž je spuštěn klient Configuration Manager.  

Pokud přeinstalujete klienta, Configuration Manager konzolu nebo poskytovatele služby SMS, je nutné přeinstalovat také aktualizace těchto součástí.  

Informace v následujících částech použijte k instalaci aktualizací do každé součásti pro Configuration Manager.  

###  <a name="update-servers"></a><a name="bkmk_servers"></a> Aktualizovat servery  
Aktualizace serverů mohou obsahovat aktualizace **lokalit**, **site database**a počítačů, v nichž se spouští instance **poskytovatele serveru SMS**:  

####  <a name="update-a-site"></a><a name="bkmk_site"></a> Aktualizace webu  
Chcete-li aktualizovat lokalitu Configuration Manager, můžete nainstalovat sadu aktualizací přímo na server lokality, nebo můžete aktualizace nasadit na server lokality po instalaci sady aktualizací do jiné lokality.  

Pokud instalujete aktualizaci na server lokality, proces instalace aktualizací řídí ostatní akce, které jsou vyžadovány k použití aktualizace, jako je např. aktualizace rolí systému lokality. Výjimkou je databáze lokality. Následující část obsahuje informace o aktualizaci databáze lokality.  

####  <a name="update-a-site-database"></a><a name="bkmk_database"></a> Aktualizace databáze lokality  
Chcete-li aktualizovat databázi lokality, proces instalace spustí soubor s názvem **Update. SQL** v databázi lokality. Proces aktualizace lze nakonfigurovat tak, aby byla databáze lokality aktualizována automaticky, nebo můžete databázi lokality aktualizovat později ručně.  

**Automatická aktualizace databáze lokality**  

Při instalaci sady aktualizací na server lokality můžete zvolit automatickou aktualizaci databáze lokality při instalaci aktualizace serveru. Toto rozhodnutí se vztahuje pouze na server lokality, kde instalujete sadu aktualizací a nevztahuje se na nasazení vytvořená k instalaci aktualizací na vzdálené servery lokality.  

> [!NOTE]  
> Pokud se rozhodnete aktualizovat databázi lokality automaticky, proces aktualizuje databázi bez ohledu na to, zda je databáze umístěna na serveru lokality nebo na vzdáleném počítači.  

> [!IMPORTANT]  
> Před aktualizací databáze lokality vytvořte zálohu databáze lokality. Aktualizaci databáze lokality nelze odinstalovat. Informace o tom, jak vytvořit zálohu pro Configuration Manager, najdete v tématu [zálohování a obnovení pro Configuration Manager](backup-and-recovery.md).  

**Ruční aktualizace databáze lokality**  

Pokud se rozhodnete, že nechcete automaticky aktualizovat databázi lokality při instalaci sady aktualizací na server lokality, aktualizace serveru neupraví databázi na serveru lokality, kde je spuštěná sada aktualizací. Nicméně nasazení, která používají balíček vytvořený pro nasazení softwaru nebo která instalují, vždy aktualizují databázi lokality.  

> [!WARNING]  
> Pokud aktualizace obsahuje aktualizace webového serveru i databáze lokality, aktualizace nebude funkční, dokud se aktualizace nedokončí jak pro server lokality, tak pro databázi lokality. Dokud se aktualizace nepoužije pro databázi lokality, lokalita je v nepodporovaném stavu.  

**Ruční aktualizace databáze lokality:**  

1.  Na serveru lokality zastavte službu SMS_SITE_COMPONENT_MANAGER a potom zastavte službu SMS_EXECUTIVE.  

2.  Zavřete konzolu Configuration Manager.  

3.  V databázi této lokality spusťte skript aktualizace s názvem **Update. SQL** . Informace o tom, jak spustit skript pro aktualizaci databáze SQL Server, najdete v dokumentaci k verzi SQL Server, kterou používáte pro server databáze lokality.  

4.  Restartujte služby, které jste zastavili v předchozích krocích.  

5.  Po instalaci sady aktualizací extrahuje **Update. SQL** do následujícího umístění na serveru lokality: ** \\ \\ &lt; název serveru \> \ SMS_ &lt; kód lokality \> \HotFix \\ &lt; KB číslo \> \Update.SQL**  

####  <a name="update-a-computer-that-runs-the-sms-provider"></a><a name="bkmk_provider"></a> Aktualizace počítače, na kterém je spuštěný poskytovatel serveru SMS  
Po instalaci sady aktualizací obsahující aktualizace poskytovatele serveru SMS musíte aktualizaci nasadit do každého počítače, na kterém je spuštěný poskytovatel serveru SMS. Jedinou výjimku představuje instance poskytovatele serveru SMS dříve instalovaná na serveru lokality, kde sadu aktualizací instalujete. Místní instance poskytovatele serveru SMS na serveru lokality je aktualizována při instalaci sady aktualizací.  

Pokud poskytovatele služby SMS z počítače odeberete a znovu nainstalujete, musíte znovu nainstalovat aktualizaci poskytovatele služby SMS v tomto počítači.  

###  <a name="update-clients"></a><a name="BKMK_clients"></a> Aktualizace klientů  
Při instalaci aktualizace, která obsahuje aktualizace pro klienta Configuration Manager, se zobrazí možnost automaticky upgradovat klienty pomocí instalace aktualizací nebo ručně upgradovat klienty později. Další informace o automatickém upgradu klientů najdete v tématu [Postup upgradu klientů pro počítače s Windows](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

Aktualizace můžete nasadit pomocí nástroje Updates Publisher nebo pomocí balíčku nasazení softwaru. Aktualizace jednotlivých klientů můžete taky nainstalovat ručně. Další informace o použití nasazení k instalaci aktualizací naleznete v části [Nasazení aktualizací pro Configuration Manager](#BKMK_Deploy) v tomto tématu.  

> [!IMPORTANT]  
> Když instalujete aktualizace pro klienty a sada aktualizací obsahuje aktualizace pro servery, nezapomeňte nainstalovat také aktualizace serveru v primární lokalitě, ke které jsou klienti přiřazení.  

Chcete-li ručně nainstalovat aktualizaci klienta, u každého klienta Configuration Manager musíte spustit **Msiexec.exe** a odkazovat na soubor. msp s aktualizací klienta pro konkrétní platformu.  

Pro aktualizaci klienta můžete například použít následující příkazový řádek. Tento příkaz spustí v klientském počítači program Msiexec s odkazem na soubor. msp, který byla extrahována ze sady aktualizací na serveru lokality: **msiexec.exe/p \\ \\ &lt; název_serveru \> \ SMS_ &lt; SiteCode \> \HotFix \\ &lt; KB number \> \Client \\ &lt; Platform \> \\ &lt; MSP \> /l \* v &lt; logfile \> REINSTALLMODE = Mous REINSTALL = ALL**  

###  <a name="update-configuration-manager-consoles"></a><a name="BKMK_console"></a> Aktualizace Configuration Managerch konzol  
Chcete-li aktualizovat konzolu Configuration Manager, je nutné nainstalovat aktualizaci na počítač, který spouští konzolu po dokončení instalace konzoly.  

> [!IMPORTANT]  
> Když nainstalujete aktualizace pro konzolu Configuration Manager a sada aktualizací obsahuje aktualizace pro servery, nezapomeňte taky nainstalovat aktualizace serveru na lokalitu, kterou používáte s konzolou Configuration Manager.  

Pokud počítač, který aktualizujete, spustí klienta Configuration Manager:  

- Můžete použít nasazení k instalaci aktualizace. Další informace o použití nasazení k instalaci aktualizací naleznete v části [Nasazení aktualizací pro Configuration Manager](#BKMK_Deploy) v tomto tématu.  

- Pokud jste přihlášeni přímo ke klientskému počítači, můžete instalaci spustit interaktivně.  

- Aktualizaci můžete nainstalovat ručně do jednotlivých počítačů. Chcete-li ručně nainstalovat aktualizaci konzoly Configuration Manager, můžete na každém počítači, který spouští konzolu Configuration Manager, spustit Msiexec.exe a odkazovat na soubor. msp s aktualizací konzoly Configuration Manager.  

Pomocí následujícího příkazového řádku můžete například aktualizovat Configuration Manager konzolu. Tento příkaz spustí v počítači program Msiexec s odkazem na soubor. msp, který byla extrahována ze sady aktualizací na serveru lokality: **msiexec.exe/p \\ \\ &lt; název_serveru \> \ SMS_ &lt; SiteCode \> \HotFix \\ &lt; KB číslo \> \AdminConsole \\ &lt; Platform \> \\ &lt; MSP \> /l \* v &lt; logfile \> REINSTALLMODE = Mous REINSTALL = ALL**  

##  <a name="deploy-updates-for-configuration-manager"></a><a name="BKMK_Deploy"></a> Nasazení aktualizací pro Configuration Manager  
Po instalaci sady aktualizací na server lokality můžete použít jednu z následujících tří metod k nasazení aktualizací do dalších počítačů.  

###  <a name="use-updates-publisher-2011-to-install-updates"></a><a name="BKMK_DeploySCUP"></a> Pomocí Updates Publisher 2011 nainstalujte aktualizace.  
Když nainstalujete sadu aktualizací na server lokality, Průvodce instalací vytvoří soubor katalogu pro nástroj Updates Publisher, který můžete použít k nasazení aktualizací do příslušných počítačů. Průvodce tento katalog vytvoří vždy, i když vyberete možnost **Použít balíček a program k nasazení této aktualizace**.  

Katalog pro aktualizace Publisher je pojmenován **SCUPCatalog.cab** a najdete ho v následujícím umístění na počítači, kde je spuštěná sada aktualizací: ** \\ \\ &lt; servername \> \ SMS_ &lt; SiteCode \> \HotFix \\ &lt; KB number \>\SCUP\SCUPCatalog.cab**  

> [!IMPORTANT]  
> Vzhledem k tomu, že je soubor SCUPCatalog.cab vytvořen pomocí cest, které jsou specifické pro server lokality, kde je sada aktualizací nainstalována, nelze ji použít na jiných serverech lokality.  

Po dokončení průvodce můžete katalog importovat do nástroje Updates Publisher a potom k nasazení aktualizací použít Configuration Manager aktualizace softwaru. Informace o nástroji Updates Publisher najdete v tématu [Updates publisher 2011](/previous-versions/system-center/updates-publisher-2011/hh134742(v=technet.10)).  

Následující postup použijte k importu souboru SCUPCatalog.cab do nástroje Updates Publisher a publikování aktualizací.  

##### <a name="to-import-the-updates-to-updates-publisher-2011"></a>Import aktualizací do nástroje Updates Publisher 2011  

1.  Spusťte konzolu nástroje Updates Publisher a klikněte na **importovat**.  

2.  Na stránce **typ importu** v Průvodci importem katalogu aktualizací softwaru vyberte možnost **zadat cestu ke katalogu, který chcete importovat**, a pak zadejte soubor SCUPCatalog.cab.  

3.  Klikněte na tlačítko **Další**a potom znovu klikněte na tlačítko **Další** .  

4.  V dialogovém okně **Upozornění zabezpečení – ověření katalogu** klikněte na **přijmout**. Po dokončení průvodce zavřete.  

5.  V konzole nástroje Updates Publisher vyberte aktualizaci, kterou chcete nasadit, a potom klikněte na **publikovat**.  

6.  Na stránce **Možnosti publikování** v Průvodci publikováním aktualizací softwaru vyberte možnost **celý obsah**a klikněte na tlačítko **Další**.  

7.  Dokončete průvodce, aby se aktualizace publikovaly.  

###  <a name="use-software-deployment-to-install-updates"></a><a name="BKMK_DeploySWDist"></a> Použití nasazení softwaru k instalaci aktualizací  
Když nainstalujete sadu aktualizací na server primární lokality nebo lokality centrální správy, můžete nakonfigurovat Průvodce instalací, aby vytvořil balíčky aktualizací pro nasazení softwaru. Jednotlivé balíčky pak můžete nasadit do kolekce počítačů, které chcete aktualizovat.  

Chcete-li vytvořit balíček nasazení softwaru, na stránce průvodce **Konfigurovat nasazení aktualizace softwaru** zaškrtněte políčko pro každý typ balíčku aktualizací, který chcete aktualizovat. Dostupné typy mohou zahrnovat servery, Configuration Manager konzolu a klienty. Pro každý vybraný typ aktualizace bude vytvořen samostatný balíček.  

> [!NOTE]  
> Balíček pro servery obsahuje aktualizace pro následující komponenty:  
>   
> - Server lokality  
> - poskytovatele serveru SMS  
> - Databáze lokality  

Následně v průvodci na stránce **Metoda konfigurace nasazení aktualizace softwaru** vyberte možnost **Použiji distribuci softwaru**. Tento výběr nastaví Průvodce tak, aby vytvořil balíčky pro nasazení softwaru.  

Po dokončení průvodce můžete zobrazit balíčky, které vytvoří v konzole Configuration Manager v uzlu **balíčky** v pracovním prostoru **softwarová knihovna** . Pak můžete použít svůj standardní proces k nasazení softwarových balíčků do Configuration Manager klientů. Když balíček běží na klientovi, nainstaluje aktualizace na příslušné součásti Configuration Manager v klientském počítači.  

Informace o tom, jak nasadit balíčky do klientů Configuration Manager, najdete v tématu [balíčky a programy](../../../apps/deploy-use/packages-and-programs.md).  

###  <a name="create-collections-for-deploying-updates-to-configuration-manager"></a><a name="BKMK_DeployCollections"></a> Vytváření kolekcí pro nasazování aktualizací do Configuration Manager  
Můžete nasadit konkrétní aktualizace pro příslušné klienty. Následující informace vám pomohou při vytváření kolekcí zařízení pro různé součásti pro Configuration Manager.  

|Součást Configuration Manager|Pokyny|  
|----------------------------------------|------------------|  
|Server lokality centrální správy|Vytvořte přímý dotaz členství a přidejte počítač serveru lokality centrální správy.|  
|Všechny servery primární lokality|Vytvořte přímý dotaz členství a přidejte všechny počítače serverů primární lokality.|  
|Všechny servery sekundární lokality|Vytvořte přímý dotaz členství a přidejte všechny počítače serverů sekundární lokality.|  
|Všichni klienti x86|Vytvořte kolekci s následujícími kritérii dotazu:<br /><br /> **Vyberte \* z SMS_R_System SMS_G_System_SYSTEM vnitřního spojení na SMS_G_System_SYSTEM. ResourceID = SMS_R_System. ResourceId, kde SMS_G_System_SYSTEM.SystemType = "počítač založený na platformě x86"**|  
|Všichni klienti x64|Vytvořte kolekci s následujícími kritérii dotazu:<br /><br /> **Vyberte \* z SMS_R_System SMS_G_System_SYSTEM vnitřního spojení na SMS_G_System_SYSTEM. ResourceID = SMS_R_System. ResourceId, kde SMS_G_System_SYSTEM.SystemType = "počítač s procesorem x64"**|  
|Všechny počítače, na kterých běží Konzola Configuration Manager|Vytvořte přímý dotaz členství a přidejte všechny počítače.|  
|Vzdálené počítače používající instanci poskytovatele služby SMS|Vytvořte přímý dotaz členství a přidejte všechny počítače.|  

> [!NOTE]  
> Chcete-li aktualizovat databázi lokality, nasaďte aktualizaci na server příslušné lokality.  

Informace o vytváření kolekcí najdete v tématu [vytváření kolekcí](../../../core/clients/manage/collections/create-collections.md).