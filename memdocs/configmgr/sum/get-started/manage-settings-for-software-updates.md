---
title: Správa nastavení pro aktualizace softwaru
titleSuffix: Configuration Manager
description: Přečtěte si o nastaveních klienta, která jsou vhodná pro aktualizace softwaru ve vaší lokalitě po instalaci bodu aktualizace softwaru.
ms.date: 03/30/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 0d484c1a-e903-4bff-9e9b-e452c62e38a8
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 0a2a45ff866ea02aacc83c42109c8cba4020ed4e
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906797"
---
#  <a name="manage-settings-for-software-updates"></a><a name="BKMK_ManageSUSettings"></a>Správa nastavení pro aktualizace softwaru  

*Platí pro: Configuration Manager (Current Branch)*

Po synchronizaci aktualizací softwaru v nástroji Configuration Manager nakonfigurujte a ověřte nastavení v následujících oddílech.

##  <a name="client-settings-for-software-updates"></a><a name="BKMK_ClientSettings"></a> Nastavení klienta pro aktualizace softwaru  
Po instalaci bodu aktualizace softwaru jsou aktualizace softwaru na klientech povolené ve výchozím nastavení a položky nastavení na stránce **Aktualizace softwaru** v nastaveních klienta mají výchozí hodnoty. Nastavení klienta se používá v rámci lokality a má vliv na to, kdy jsou aktualizace softwaru kontrolovány na dodržování předpisů a jak a kdy jsou aktualizace softwaru nainstalovány v klientských počítačích. Před nasazením aktualizací softwaru ověřte, zda jsou nastavení klienta vhodná pro aktualizace softwaru ve vaší lokalitě.  

> [!IMPORTANT]  
>  Nastavení **Povolit aktualizace softwaru na klientských počítačích** je ve výchozím nastavení povolené. Pokud toto nastavení zrušíte, Configuration Manager odebere existující zásady nasazení z klienta.  

Informace o konfiguraci nastavení klienta najdete v tématu [Konfigurace nastavení klienta](../../core/clients/deploy/configure-client-settings.md).  

Další informace o nastavení klienta najdete v tématu [informace o nastavení klienta](../../core/clients/deploy/about-client-settings.md).  

##  <a name="group-policy-settings-for-software-updates"></a><a name="BKMK_GroupPolicy"></a>Nastavení zásad skupiny pro aktualizace softwaru  
Agent webu Windows Update používá na klientských počítačích určitá nastavení zásad skupiny k připojení ke službě WSUS, která běží v bodu aktualizace softwaru. Tato nastavení zásady skupiny se také používají k úspěšnému zjištění shody aktualizací softwaru a k automatické aktualizování aktualizací softwaru a agenta webu Windows Update.

### <a name="specify-intranet-microsoft-update-service-location-local-policy"></a>Místní zásada Určit umístění intranetového serveru služby Microsoft Update  
Když je pro lokalitu vytvořený bod aktualizace softwaru, klienti obdrží zásadu počítače, která poskytuje název serveru bodu aktualizace softwaru a konfiguruje místní zásadu **Určit umístění intranetového serveru služby Microsoft Update** na počítači. Agent WUA načte název serveru určený v nastavení **Nastavení intranetové aktualizační služby pro zjišťování aktualizací** a potom se spojí s tímto serverem při zjišťování shody aktualizací softwaru. Pokud se pro položku **Určit umístění intranetového serveru služby Microsoft Update** vytvoří zásada domény, přepíše místní zásadu a agent WUA se může připojit k jinému serveru, než je bod aktualizace softwaru. Pokud k tomu dojde, může klient vyhledat shodu aktualizace softwaru na základě různých produktů, klasifikací a jazyků. Proto byste neměli konfigurovat zásadu služby Active Directory pro klientské počítače.  

### <a name="allow-signed-content-from-intranet-microsoft-update-service-location-group-policy"></a>Zásada skupiny Povolit podepsaný obsah z umístění intranetové služby Microsoft Update  
Nastavení zásady skupiny **Povolit podepsané aktualizace z umístění intranetové služby Microsoft Update** musíte povolit předtím, než agent WUA na počítačích vyhledá aktualizace softwaru, které vytvořil a publikoval nástroj System Center Updates Publisher. Když je toto nastavení zásady povolené, agent WUA přijme aktualizace softwaru přijaté z intranetového umístění, pokud jsou aktualizace softwaru podepsané v úložišti certifikátů **Důvěryhodní vydavatelé** na místním počítači. Další informace o nastaveních zásad skupiny požadovaných pro nástroj Updates Publisher najdete v [knihovně dokumentace nástroje Updates Publisher 2011](https://docs.microsoft.com/previous-versions/system-center/updates-publisher-2011/hh134742(v=technet.10)).  

### <a name="automatic-updates-configuration"></a>Konfigurace automatických aktualizací  
Automatické aktualizace umožňují přijetí aktualizací zabezpečení a dalších důležitých stahovaných souborů na klientských počítačích. Automatické aktualizace se konfigurují prostřednictvím nastavení zásad skupiny **Konfigurovat automatické aktualizace** nebo nabídky Ovládací panely místního počítače. Když je položka Automatické aktualizace povolena, klientské počítače obdrží oznámení a v závislosti na nakonfigurovaných nastaveních si tyto počítače stáhnout a nainstalují potřebné aktualizace. Když jsou Automatické aktualizace umístěny společně s aktualizacemi softwaru, může každý klientský počítač zobrazit ikony oznámení a místní kontextová oznámení pro stejnou aktualizaci. Je-li požadováno restartování, může každý klientský počítač zobrazit dialogové okno restartování pro stejnou aktualizaci.  

### <a name="self-update"></a>Samoaktualizace  
Když je na klientském počítači povolena Automatická aktualizace, agent WUA automaticky provede samoaktualizaci vždy, když je dostupná nová verze nebo když se vyskytnou problémy se součástí agenta WUA. Když Automatické aktualizace nejsou nakonfigurovány nebo jsou zakázány a klientské počítače mají dřívější verzi agenta WUA, musí být na nich spuštěn instalační soubor agenta WUA.  

## <a name="software-updates-properties"></a>Vlastnosti aktualizací softwaru
Vlastnosti aktualizací softwaru poskytují informace o aktualizacích softwaru a přiřazeném obsahu. Tyto vlastnosti lze rovněž použít ke konfiguraci nastavení pro aktualizace softwaru. Když otevřete vlastnosti pro více aktualizací softwaru, zobrazí se pouze karty **Maximální doba běhu** a **Vlastní závažnost** .   

Pomocí následujícího postupu můžete otevřít vlastnosti aktualizací softwaru.  

#### <a name="to-open-software-update-properties"></a>Otevření vlastností aktualizací softwaru  

1. V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  
2. V pracovním prostoru Softwarová knihovna rozbalte možnost **Aktualizace softwaru** a klikněte na položku **Všechny aktualizace softwaru**.  
3. Vyberte alespoň jednu aktualizaci softwaru a poté na kartě **Domů** klikněte na položku **Vlastnosti** ve skupině **Vlastnosti** .  

   > [!NOTE]  
   >  V uzlu **všechny aktualizace softwaru** Configuration Manager zobrazí pouze aktualizace softwaru s klasifikací **kritické** a **zabezpečení** , které byly vydány v posledních 30 dnech.  

###  <a name="review-software-updates-information"></a><a name="BKMK_SoftwareUpdatesInformation"></a>Kontrola informací o aktualizacích softwaru  
Ve vlastnostech aktualizací softwaru můžete zkontrolovat podrobné informace o aktualizaci softwaru. Podrobné informace se nezobrazí, pokud vyberete více než jednu aktualizaci softwaru. Následující části popisují informace, které jsou dostupné pro vybranou aktualizaci softwaru.  

####  <a name="software-update-details"></a><a name="BKMK_SoftwareUpdateDetails"></a> Podrobnosti o aktualizacích softwaru  
Na kartě **Podrobnosti o aktualizaci** můžete zobrazit následující souhrnné informace o vybrané aktualizaci softwaru:  

- **ID bulletinu:** Určuje ID bulletinu, které je přidružené k aktualizacím zabezpečení softwaru. Podrobnosti o bulletinech zabezpečení najdete na stránce s ID bulletinu na webové stránce [centra Microsoft Security Response](https://portal.msrc.microsoft.com/) .  

> [!NOTE]
> Způsob, jakým se mění aktualizace zabezpečení dokumentů společnosti Microsoft. Předchozí model použil webové stránky bulletin zabezpečení a obsahoval čísla ID bulletinu zabezpečení (například MS16-XXX) jako bod otáčení. Tato forma dokumentace k aktualizaci zabezpečení, včetně čísel ID bulletinů, se vyřadí a nahrazuje se průvodcem aktualizací zabezpečení. Místo ID bulletinů se nová příručka Překlopí na čísla ID ohrožení zabezpečení a čísla ID článků v KB. Další informace najdete v nejčastějších dotazech k [aktualizaci zabezpečení](https://www.microsoft.com/msrc/faqs-security-update-guide).


- **ID článku:** Určuje ID článku pro aktualizaci softwaru. Vybraný článek poskytuje podrobnější informace o aktualizaci softwaru a problému, který daná aktualizace softwaru opravuje či zmírňuje.  

- **Datum revize:** Určuje datum poslední úpravy aktualizace softwaru.  

- **Maximální hodnocení závažnosti:** Určuje pro aktualizaci softwaru hodnocení závažnosti definované dodavatelem.  

- **Popis:** Poskytuje přehled toho, co aktualizace softwaru opravuje nebo zlepšuje.  

- **Použitelné jazyky:** Zobrazuje seznam jazyků, na které se aktualizace softwaru vztahuje.  

- **Ovlivněné produkty:** Zobrazuje seznam produktů, na které se aktualizace softwaru vztahuje.  

####  <a name="content-information"></a><a name="BKMK_ContentInformation"></a> Informace o obsahu  
Na kartě **Informace o obsahu** jsou zobrazeny následující informace o obsahu, který je přiřazen k vybrané aktualizaci softwaru:  

-   **ID obsahu:** Určuje ID obsahu pro aktualizaci softwaru.  

-   **Staženo**: Určuje, zda Configuration Manager stáhla soubory aktualizace softwaru.  

-   **Jazyk:** Určuje jazyky pro aktualizaci softwaru.  

-   **Zdrojová cesta:** Určuje cestu ke zdrojovým souborům aktualizace softwaru.  

-   **Velikost (MB):** Určuje velikost zdrojových souborů aktualizace softwaru.  

####  <a name="custom-bundle-information"></a><a name="BKMK_CustomBundleInformation"></a> Informace o vlastním balíčku  
Na kartě **Informace o vlastním balíčku** naleznete informace o vlastním balíčku pro aktualizaci softwaru. Když vybraná aktualizace softwaru obsahuje přibalené aktualizace softwaru, jež jsou obsaženy v souboru aktualizace softwaru, zobrazí se tyto aktualizace v části **Informace o balíčku** . Na této kartě nejsou zobrazeny přibalené aktualizace softwaru, které jsou zobrazeny na kartě **Informace o obsahu**, jako jsou například soubory aktualizací pro různé jazyky.  

####  <a name="supersedence-information"></a><a name="BKMK_SupersedenceInformation"></a> Informace o nahrazení  
Na kartě **Informace o nahrazení** jsou zobrazeny následující informace o nahrazení pro aktualizaci softwaru:  

- **Tato aktualizace byla nahrazena následujícími aktualizacemi:** Určuje aktualizace softwaru, které nahrazují tuto aktualizaci. To znamená, že uvedené aktualizace jsou novější. Ve většině případů nasadíte jednu z aktualizací softwaru, která nahrazuje danou aktualizaci softwaru. Aktualizace softwaru, které jsou zobrazeny v tomto seznamu, obsahují hypertextové odkazy na webové stránky, jež poskytují další informace o aktualizacích softwaru. Když tato aktualizace není nahrazena, zobrazí se položka **Žádné** .  

- **Tato aktualizace nahrazuje následující aktualizace:** Určuje aktualizace softwaru, které tato aktualizace softwaru nahrazuje. To znamená, že tato aktualizace softwaru je novější. Ve většině případů nasadíte tuto aktualizaci softwaru, aby nahradila starší aktualizace softwaru. Aktualizace softwaru, které jsou zobrazeny v tomto seznamu, obsahují hypertextové odkazy na webové stránky, jež poskytují další informace o aktualizacích softwaru. Pokud tato aktualizace nenahrazuje žádnou jinou aktualizaci, zobrazí se položka **Žádná**.  

###  <a name="configure-software-updates-settings"></a><a name="BKMK_SoftwareUpdatesSettings"></a> Konfigurace nastavení aktualizací softwaru  
Ve vlastnostech můžete nakonfigurovat nastavení aktualizace softwaru pro jednu nebo více aktualizací softwaru. Většinu nastavení aktualizací softwaru můžete nakonfigurovat pouze v lokalitě centrální správy nebo samostatné primární lokalitě. Následující části vám pomohou nakonfigurovat nastavení pro aktualizace softwaru.  

####  <a name="set-maximum-run-time"></a><a name="BKMK_SetMaxRunTime"></a> Nastavení maximální doby běhu  
Na kartě **Maximální doba běhu** můžete nastavit maximální dobu, která je vymezena pro dokončení aktualizace softwaru na klientských počítačích. Pokud bude aktualizace trvat déle, než je hodnota maximální doby běhu, Configuration Manager vytvoří stavovou zprávu a zastaví monitorování nasazení aktualizací softwaru. Toto nastavení lze upravit pouze v lokalitě centrální správy nebo samostatné primární lokalitě.  

Configuration Manager používá toto nastavení také k určení, jestli se má zahájit instalace aktualizace softwaru v nakonfigurovaném časovém období údržby. Pokud je hodnota maximální doby běhu větší než dostupný zbývající čas v časovém období údržby, odloží se instalace aktualizací softwaru až do zahájení dalšího časového období údržby. Když mají být na klientský počítač s nakonfigurovaným časovým obdobím údržby nainstalováno více aktualizací softwaru (časový rámec), nejprve se nainstaluje aktualizace softwaru s nejnižší maximální dobou běhu, následně se nainstaluje aktualizace softwaru s další maximální dobou běhu v pořadí a tak dále. Než klient nainstaluje všechny aktualizace softwaru, ověří, zda dostupné časové období údržby poskytne dostatek času k instalaci aktualizace softwaru. Poté, co je zahájena instalace aktualizace softwaru, bude se v instalaci pokračovat dokonce i v případě, že instalace překročí konec časového období údržby. Další informace o časových obdobích údržby najdete v [časových intervalech](../../core/clients/manage/collections/use-maintenance-windows.md)pro správu a údržbu.  

Na kartě **Maximální doba běhu** můžete zobrazit a nakonfigurovat následující nastavení:  

- **Maximální doba spuštění**: Určuje maximální počet minut vyhrazených pro dokončení instalace aktualizace softwaru před tím, než instalace přestane být monitorována nástrojem Configuration Manager. Toto nastavení se rovněž používá k určení faktu, zda zbývá dostatek času k instalaci aktualizace, než skončí časové období údržby. Výchozí nastavení je 60 minut pro aktualizace Service Pack. U ostatních typů aktualizací softwaru je výchozí hodnota 10 minut, pokud jste provedli novou instalaci Configuration Manager verze 1511 nebo vyšší a 5 minut, když upgradujete z předchozí verze. Hodnoty mohou být v rozsahu 5 až 9 999 minut.  

> [!IMPORTANT]  
>  Nezapomeňte nastavit hodnotu maximální doby běhu menší než nakonfigurované časové období údržby nebo prodloužit časový interval pro správu a údržbu na hodnotu vyšší, než je maximální doba běhu. Jinak nebude instalace aktualizace softwaru nikdy zahájena.  

####  <a name="set-custom-severity"></a><a name="BKMK_SetCustomSeverity"></a> Nastavení vlastní závažnosti  
Ve vlastnostech aktualizace softwaru je možné pomocí karty **Vlastní závažnost** konfigurovat vlastní hodnoty závažnosti pro aktualizace softwaru. To může být užitečné, pokud předem definované hodnoty závažnosti nevyhovují vašim požadavkům. Vlastní hodnoty jsou uvedené ve sloupci **Vlastní závažnost** v konzole Configuration Manager. Aktualizace softwaru lze seřadit dle definovaných vlastních hodnot závažnosti a také je možné vytvořit dotazy a sestavy, pomocí kterých lze tyto hodnoty filtrovat. Toto nastavení lze upravit pouze v lokalitě centrální správy nebo v samostatné primární lokalitě.  

Na kartě **Vlastní závažnost** lze konfigurovat následující nastavení.  

- **Vlastní závažnost:** Slouží k nastavení vlastní hodnoty závažnosti pro aktualizace softwaru. Ze seznamu vyberte možnost **Kritická**, **Důležitá**, **Střední**nebo **Nízká** . Ve výchozím nastavení je vlastní hodnota závažnosti prázdná.

## <a name="crl-checking-for-software-updates"></a>Kontrola CRL pro aktualizace softwaru
Ve výchozím nastavení se seznam odvolaných certifikátů (CRL) nekontroluje při ověřování signatury Configuration Manager aktualizací softwaru. Kontrola seznamu CRL pokaždé, když je certifikát použit, poskytuje lepší zabezpečení proti použití certifikátu, který byl zrušen, ale představuje zpoždění připojení a má za následek další zpracování na počítači provádějícím kontrolu seznamu CRL.  

V případě použití musí být Kontrola CRL povolena v Configuration Manager konzolách, které zpracovávají aktualizace softwaru.  

#### <a name="to-enable-crl-checking"></a>Povolení kontroly seznamu CRL  
Na počítači provádějícím kontrolu seznamu CRL z disku DVD s produktem spusťte následující příkaz z příkazového řádku: **\SMSSETUP\BIN\X64 \\ ** < *Language* > **\UpdDwnldCfg.exe/checkrevocation**.  

Například pro angličtinu (US) spusťte **\SMSSETUP\BIN\X64\00000409\UpdDwnldCfg.exe/checkrevocation**  
