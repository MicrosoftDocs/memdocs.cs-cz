---
title: Vytváření aplikací pro servery Linux a UNIX
titleSuffix: Configuration Manager
description: V této části najdete informace, které je potřeba vzít v úvahu při vytváření a nasazování aplikací pro zařízení se systémy Linux a UNIX.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 79cd131a-1a24-4751-87c8-7f275e45d847
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3f5d0cfb930e6d1b8cf4cd6dfb0eabfa38ddab16
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075774"
---
# <a name="create-linux-and-unix-server-applications-with-configuration-manager"></a>Vytváření aplikací serveru pro Linux a UNIX pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

> [!Important]  
> Počínaje verzí 1902 Configuration Manager nepodporuje klienty se systémy Linux a UNIX. 
> 
> Zvažte Microsoft Azure správu pro správu serverů se systémem Linux. Řešení Azure mají rozsáhlou podporu pro Linux, která ve většině případů překračuje Configuration Manager funkce, včetně ucelené správy oprav pro Linux.

Při vytváření a nasazování aplikací pro počítače se systémem Linux a UNIX Vezměte v úvahu následující skutečnosti.  

## <a name="general-considerations"></a>Obecné aspekty  
 Klient Configuration Manager pro systémy Linux a UNIX podporuje **nasazení softwaru využívající balíčky a programy**. Configuration Manager aplikace nemůžete nasadit do počítačů se systémy Linux a UNIX.  

 Mezi možnosti nasazení softwaru pro Linux a UNIX patří:  

-   Instalace softwaru pro servery se systémy Linux a UNIX, včetně následujících funkcí:  

    -   Nasazení nového softwaru  

    -   Aktualizace softwaru pro programy, které jsou již v počítači  

    -   Opravy operačního systému  

-   Nativní příkazy pro systémy Linux a UNIX a skripty umístěné na serverech se systémy Linux a UNIX  

-   Nasazení omezená na operační systémy, které zadáte, když vyberete možnost program **pouze na zadaných klientských platformách**

-   Časové intervaly pro správu a údržbu k řízení při instalaci softwaru

-   Stavové zprávy o nasazení pro monitorování nasazení  

-   Možnost klienta omezit využití sítě při stahování softwaru z distribučního bodu  

### <a name="differences-between-deploying-to-linux-and-unix-computers-and-deploying-to-windows-devices"></a>Rozdíly mezi nasazením na počítače se systémy Linux a UNIX a nasazením na zařízení s Windows
Hlavní rozdíly mezi nasazením balíčků a programů na počítače se systémy Linux a UNIX a nasazením balíčků a programů na zařízení s Windows jsou následující:  

|Konfigurace|Podrobnosti|  
|-------------------|-------------|  
|Používejte pouze konfigurace určené pro počítače a nepoužívejte konfigurace určené pro uživatele.|Klient Configuration Manager pro systémy Linux a UNIX nepodporuje konfigurace určené pro uživatele.|  
|Nakonfigurujte programy ke stažení softwaru z distribučního bodu a spusťte programy z místní mezipaměti klienta.|Klient Configuration Manager pro systémy Linux a UNIX nepodporuje spouštění softwaru z distribučního bodu. Místo toho je nutné nakonfigurovat software ke stažení do klienta a pak nainstalovat.<br /><br /> Ve výchozím nastavení platí, že jakmile klient nástroje pro Linux a UNIX nainstaluje software, bude tento software z mezipaměti klienta odstraněn. Balíčky, které jsou nakonfigurované s **trvalým obsahem v mezipaměti klienta** , ale nejsou z klienta odstraněny a zůstanou v mezipaměti klienta i po instalaci softwaru.<br /><br /> Klient pro systémy Linux a UNIX nepodporuje konfigurace mezipaměti klienta a maximální velikost mezipaměti klienta je omezena pouze volným místem na disku klientského počítače.|  
|Konfigurace účtu přístupu k síti pro přístup k distribučním bodům|Počítače se systémy Linux a UNIX jsou koncipovány jako počítače do skupiny. Chcete-li získat přístup k balíčkům z distribučního bodu v Configuration Manager doméně serveru lokality, je nutné nakonfigurovat účet přístupu k síti pro lokalitu. Tento účet musí být zadán jako vlastnost komponenty distribuce softwaru a nakonfigurován ještě před nasazením softwaru.<br /><br /> Pro každou lokalitu můžete nakonfigurovat více účtů přístupu k síti. Klient pro systém Linux a UNIX může využívat všechny tyto účty, které nastavíte jako účty přístupu k síti.<br /><br /> Další informace najdete v tématu [součásti lokality pro Configuration Manager](../../core/servers/deploy/configure/site-components.md).|  

 Balíčky a programy lze nasadit do kolekcí, které obsahují pouze klienty se systémy Linux nebo UNIX, nebo je můžete nasadit do kolekcí obsahujících kombinaci různých typů klientů, jako je **Kolekce všech systémů**. Klienti, kteří nejsou systémy Linux a UNIX, ale nebudou instalovat software nebo nahlásit selhání.  

 Když klient Configuration Manager pro systémy Linux a UNIX obdrží a spustí nasazení, vygeneruje stavové zprávy. Tyto stavové zprávy můžete zobrazit v konzole Configuration Manager nebo pomocí sestav, které monitorují stav nasazení.  

 Informace o tom, jak používat balíčky a programy, najdete v tématu [balíčky a programy](../../apps/deploy-use/packages-and-programs.md).  

##  <a name="configure-packages-programs-and-deployments-for-linux-and-unix-servers"></a>Konfigurace balíčků, programů a nasazení pro servery se systémy Linux a UNIX  
 Balíčky a programy můžete vytvářet a nasazovat pomocí dostupných výchozích možností v konzole Configuration Manager. Klient nevyžaduje žádné jedinečné konfigurace.  

 Informace v následujících částech slouží ke konfiguraci balíčků a programů a nasazení.  

### <a name="packages-and-programs"></a>Balíčky a programy  
 Chcete-li vytvořit balíček a program pro server se systémem Linux nebo UNIX, použijte **Průvodce vytvořením balíčku a programu** z konzoly Configuration Manager. Klient pro systémy Linux a UNIX podporuje většinu nastavení balíčků a programů. Některé nastavení však není podporováno. Když vytváříte nebo konfigurujete balíček a program, vezměte v úvahu následující body:  

-   Zahrňte typy souborů, které jsou podporovány cílovými počítači.  

-   Definujte příkazové řádky, které jsou vhodné pro použití v cílovém počítači.  

-   Pamatujte, že nastavení pro interakci s uživateli nejsou podporovaná.  

V následující tabulce jsou uvedeny vlastnosti pro balíčky a programy, které nejsou podporované:  

|Vlastnost balíčku a programu|Chování|Další informace|  
|----------------------------------|--------------|----------------------|  
|Nastavení sdílené složky balíčků:<br /><br /> -Všechny možnosti|Vygeneruje se chyba a instalace softwaru se nezdařila.|Klient tuto konfiguraci nepodporuje. Klient místo toho musí software stáhnout pomocí protokolu HTTP nebo HTTPS a poté spustit příkazový řádek z místní mezipaměti.|  
|Nastavení aktualizace balíčků:<br /><br /> -Odpojit uživatele od distribučních bodů|Nastavení je ignorováno|Klient tuto konfiguraci nepodporuje.|  
|Nastavení nasazení operačního systému:<br /><br /> -Všechny možnosti|Nastavení je ignorováno|Klient tuto konfiguraci nepodporuje.|  
|Vytváření sestav:<br /><br /> – Pro párování stavových souborů MIF používat vlastnosti balíčku<br /><br /> – Pro párování stavových souborů MIF používat tato pole|Nastavení je ignorováno|Klient nepodporuje používání stavových souborů MIF.|  
|**Spusťte**:<br /><br /> -Všechny možnosti|Nastavení je ignorováno|Klient vždy spouští balíčky bez uživatelského rozhraní.<br /><br /> Klient ignoruje veškeré nastavení pod položkou Spustit.|  
|Po spuštění:<br /><br />-Configuration Manager restartuje počítač.<br /><br /> – Program řídí restart.<br /><br /> -Configuration Manager odhlásí uživatele|Vygeneruje se chyba a instalace softwaru se nezdařila.|Nastavení restartování systému a nastavení pro konkrétní uživatele nejsou podporovaná.<br /><br /> Pokud se používá jakékoli nastavení jiné než **Není zapotřebí žádná akce** , klient vygeneruje chybu a v instalaci softwaru pokračuje bez jakékoli akce.|  
|Program lze spustit:<br /><br /> – Jenom když je přihlášený uživatel|Vygeneruje se chyba a instalace softwaru se nezdařila.|Nastavení specifické pro uživatele se nepodporuje.<br /><br /> Pokud je nastavena tato možnost, klient vygeneruje chybu a instalace softwaru selže.<br /><br /> Ostatní možnosti jsou ignorovány a instalace softwaru bude pokračovat.|  
|Režim spuštění:<br /><br /> -Spustit s uživatelskými právy|Nastavení je ignorováno|Nastavení specifické pro uživatele se nepodporuje.<br /><br /> Klient však podporuje konfiguraci běžící s právy správce.<br /><br /> Když zadáte **příkaz Spustit s právy správce**, klient Configuration Manager použije své kořenové přihlašovací údaje.<br /><br /> Toto nastavení nevygeneruje chybu ani záznam v protokolu. Místo toho se instalace softwaru nezdařila, pokud klient vygeneruje chybu pro požadovanou konfiguraci **programu lze spustit** = **pouze v případě, že je uživatel přihlášen**.|  
|Umožněte uživatelům zobrazení a interakci s instalací programu.|Nastavení je ignorováno|Nastavení specifické pro uživatele se nepodporuje.<br /><br /> Toto nastavení je ignorováno a instalace softwaru bude pokračovat.|  
|Režim jednotky:<br /><br /> -Všechny možnosti|Nastavení je ignorováno|Toto nastavení není podporováno, protože obsah je vždy stažen do klienta a spuštěn místně.|  
|Nejprve spustit jiný program|Vygeneruje se chyba a instalace softwaru se nezdařila.|Rekurzivní instalace programu není podporována.<br /><br /> Pokud je program nakonfigurován tak, aby nejprve spustil jiný program, instalace softwaru se nezdařila a instalace jiného programu nebude spuštěna.|  
|Když je tento program přiřazen počítači:<br /><br /> -Spustit jednou pro každého uživatele, který se přihlásí|Nastavení je ignorováno|Nastavení specifické pro uživatele se nepodporuje.<br /><br /> Klient však podporuje konfiguraci spuštěnou jednou pro počítač.<br /><br /> Toto nastavení nevygeneruje chybu ani záznam v protokolu, protože chyba a záznam v protokolu jsou již vytvořeny pro požadovanou konfiguraci **programu lze spustit** = **pouze v případě, že je uživatel přihlášen**.|  
|Potlačit oznámení programu|Nastavení je ignorováno|Klient neimplementuje uživatelské rozhraní.<br /><br /> Pokud je vybraná tato konfigurace, bude ignorována a instalace softwaru bude pokračovat.|  
|Zakázat tento program v počítačích, kde je nasazen|Nastavení je ignorováno|Toto nastavení není podporováno a nemá vliv na instalaci softwaru.|  
|Povolí instalaci tohoto programu z pořadí úloh instalace balíčku bez nasazení.||Klient nepodporuje pořadí úloh.<br /><br /> Toto nastavení není podporováno a nemá vliv na instalaci softwaru.|  
|Instalační služba systému Windows:<br /><br /> -Všechny možnosti|Nastavení je ignorováno|Klient nepodporuje Instalační služba systému Windows soubory ani nastavení.|  
|Režim údržby nástroje OpsMgr:<br /><br /> -Všechny možnosti|Nastavení je ignorováno|Klient tuto konfiguraci nepodporuje.|  

### <a name="deploy-software-to-a-linux-or-unix-server"></a>Nasazení softwaru na server se systémem Linux nebo UNIX
 Chcete-li nasadit software na server se systémem Linux nebo UNIX pomocí balíčku a programu, můžete použít **Průvodce nasazením softwaru** z konzoly Configuration Manager. Klient nástroje pro systémy Linux a UNIX podporuje většinu nastavení nasazení. Některá nastavení se ale nepodporují. Při nasazení softwaru Vezměte v úvahu následující body:  

- Balíček zřiďte alespoň v jednom distribučním bodu, který je přidružený ke skupině hranic, která je nakonfigurovaná pro umístění obsahu.  

- Klient pro systémy Linux a UNIX, který obdrží toto nasazení, musí mít přístup k distribučnímu bodu ze svého umístění v síti.  

- Klient pro systémy Linux a UNIX stáhne balíček z distribučního bodu a spustí program v místním počítači.  

- Klient pro Linux a UNIX nemůže stahovat balíčky ze sdílených složek. Stahují balíčky z distribučních bodů s povoleným IIS, které podporují protokol HTTP nebo HTTPS.  

  V následující tabulce jsou uvedeny vlastnosti pro nasazení, která nejsou podporovaná:  

|Vlastnost nasazení|Chování|Další informace|  
|-------------------------|--------------|----------------------|  
|Nastavení nasazení – účel:<br /><br /> – K dispozici<br /><br /> – Požadováno|Nastavení je ignorováno|Nastavení specifické pro uživatele se nepodporuje.<br /><br /> Klient však podporuje nastavení **požadováno**, které vynutilo naplánovanou dobu instalace, ale nepodporuje ruční instalaci před tímto naplánovaným časem.|  
|Odeslat pakety pro probuzení|Nastavení je ignorováno|Klient tuto konfiguraci nepodporuje.|  
|Plán přiřazení:<br /><br /> – Přihlásit se<br /><br /> – Odhlásit se|Vygeneruje se chyba a instalace softwaru se nezdařila.|Nastavení specifické pro uživatele se nepodporuje.<br /><br /> Klient však podporuje nastavení **Co nejdříve**.|  
|Nastavení upozorňování:<br /><br /> – Umožní uživatelům spustit program nezávisle na přiřazení.|Nastavení je ignorováno|Klient neimplementuje uživatelské rozhraní.|  
|Když je dosaženo plánovaného času přiřazení, povolit provedení následujících akcí mimo časový interval pro správu a údržbu:<br /><br /> -Restart systému (Pokud je to nutné pro dokončení instalace)|Je vygenerována chyba|Klient nepodporuje restartování systému.|  
|Nastavení nasazení pro rychlé sítě (LAN):<br /><br /> -Spustit program z distribučního bodu|Vygeneruje se chyba a instalace softwaru se nezdařila.|Klient nemůže spustit software z distribučního bodu a před spuštěním musí program stáhnout.|  
|Nastavení nasazení pro pomalou či nespolehlivou mez sítě nebo záložní umístění zdroje pro obsah:<br /><br /> – Umožní klientům sdílet obsah s ostatními klienty ve stejné podsíti.|Nastavení je ignorováno|Klient nepodporuje sdílení obsahu mezi partnerskými uzly.|  

 Další informace o umístění obsahu najdete v tématu [Správa obsahu a infrastruktury obsahu pro Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 Další informace o tom, jak vytvořit nasazení, najdete v tématu [nasazení aplikací](../../apps/deploy-use/deploy-applications.md).  

##  <a name="manage-network-bandwidth-for-software-downloads-from-distribution-points"></a> Správa šířky pásma sítě pro stahování softwaru z distribučních bodů  
 Klient se systémem Linux a UNIX podporuje řízení šířky pásma sítě při stahování softwaru z distribučního bodu.  

 Klient nástroje používá nastavení služby inteligentního přenosu na pozadí (BITS), které nakonfigurujete jako nastavení klienta v Configuration Manager, ale neimplementuje službu BITS. K omezení využití šířky pásma sítě místo toho řídí velikost bloku požadavků protokolu HTTP a prodlevu mezi bloky při stahování softwaru.  

 Chcete-li nakonfigurovat klienta k využití řízení šířky pásma sítě, nastavte možnost **Inteligentní přenos na pozadí** a použijte nastavení na klientský počítač. Aby bylo možné použít ovládací prvky šířky pásma, musí klient přijmout nastavení klienta pro **Inteligentní přenos na pozadí** s následujícími nastaveními nakonfigurovanými na **Ano**:  

- **Omezit maximální šířku pásma sítě pro přenosy na pozadí BITS**  

  Pro službu Background Intelligent Transfer (BITS) podporuje klient tuto konfiguraci:  

  -   **Čas zahájení omezovacího okna**  

  -   **Čas ukončení omezovacího okna**  

  -   **Maximální přenosová rychlost během omezovacího okna (kB/s)**  

  -   **Maximální přenosová rychlost mimo omezovací okno (Kbps)**  

Následující nastavení služby Background Intelligent Transfer není podporováno a klienti pro systémy Linux a UNIX ho budou ignorovat:  

- **Povolit stažení ze serveru BITS mimo omezovací okno**  

  Je-li stahování softwaru do klienta z distribučního bodu přerušeno, klient pro systémy Linux a UNIX neobnoví stahování. Místo toho se spustí stahování celého softwarového balíčku.  

##  <a name="configure-operations-for-software-deployments"></a>Konfigurace operací pro nasazení softwaru  
 Podobně jako u klienta Windows klient Configuration Manager pro systémy Linux a UNIX při dotazování a kontrolách nových zásad zjistí nová nasazení softwaru. Frekvence, s níž klient vyhledává nové zásady, závisí na nastavení klienta. Ke stanovení okamžiku, kdy bude software nasazen, můžete nastavit časové intervaly pro správu a údržbu.  

 Nasazení softwaru na servery se systémy Linux a UNIX můžete nastavit pomocí vlastností balíčků, programů a nasazení.  

 Když klient obdrží zásady pro nasazení, odešle stavovou zprávu. Odesílá také stavové zprávy, když spustí instalaci softwaru a když se instalace dokončí nebo dojde k chybě.  

 Programy pro nasazení softwaru se spouštějí s přihlašovacími údaji, které klient Configuration Manager pro systémy Linux a UNIX spouští s nástrojem. Ukončovací kód programového příkazu slouží ke stanovení úspěšného či neúspěšného dokončení. Ukončovací kód 0 (nula) označuje úspěšné dokončení. Pokud je úroveň protokolu nastavena na hodnoty INFO nebo TRACE, je spolu s ním zkopírován do souboru protokolu také záznam **stdout** (standardní výstupní proud) a **stderr** (standardní chybový proud).  

> [!TIP]  
>  Pokud je nasazovaný software umístěn ve sdílené složce NFS (Network File System), k níž má server se systémem Linux nebo UNIX přístup, není nutné využívat ke stažení balíčku distribuční bod. Při vytváření balíčku nezaškrtávejte políčko **Tento balíček obsahuje zdrojové soubory**. Při konfiguraci programu pak zadejte příslušný příkazový řádek k přímému přístupu k balíčku v přípojném bodě NFS.  
