---
title: Vytvoření položek konfigurace pro Windows
titleSuffix: Configuration Manager
description: Vytvořte položky konfigurace pro správu nastavení pro počítače s Windows 10 pomocí místní správy mobilních zařízení (MDM) v Configuration Manager.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 23e1e4dc-623a-4521-ad04-ae9482927097
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1987ba504630ab1d4b23cdb54710f0cbaa3db28a
ms.sourcegitcommit: 7f542c97ac55bbd329f5befda97d671213c24e9a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/08/2020
ms.locfileid: "84506244"
---
# <a name="create-configuration-items-for-windows-devices-with-on-premises-mdm-in-configuration-manager"></a>Vytvoření položek konfigurace pro zařízení s Windows s místní správou MDM v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pomocí položky konfigurace Configuration Manager **Windows 8.1 a Windows 10** můžete spravovat nastavení pro zařízení s Windows, která spravujete pomocí místní správy mobilních zařízení (MDM).

Obecnější informace o nastavení dodržování předpisů v Configuration Manager najdete v následujících článcích:

- [Začínáme s nastavením dodržování předpisů](../../compliance/get-started/get-started-with-compliance-settings.md)

- [Plánování a konfigurace nastavení dodržování předpisů](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)

## <a name="create-a-configuration-item"></a>Vytvoření položky konfigurace

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** , rozbalte položku **Nastavení dodržování předpisů**a potom vyberte uzel **položky konfigurace** .

1. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte možnost **vytvořit položku konfigurace**.

1. Na stránce **Obecné** v **Průvodci vytvořením položky konfigurace**zadejte následující informace:

    - **Název**: jedinečný název, který identifikuje tuto položku konfigurace.

    - **Popis**: volitelný popis, který poskytne další informace o jeho použití.

    - V části **nastavení pro zařízení spravovaná *bez* klienta Configuration Manager**vyberte **Windows 8.1 a Windows 10**.

    - **Kategorie**: můžete vytvořit a přiřadit kategorie, které vám pomohou při hledání a filtrování položek konfigurace v konzole Configuration Manager.

1. Na stránce **podporované platformy** v průvodci vyberte konkrétní platformy Windows pro vyhodnocení této položky konfigurace.

1. Na stránce **nastavení zařízení** vyberte skupiny nastavení, které chcete konfigurovat. Další informace o dostupných nastaveních najdete v tématu informace o [Nastavení](#bkmk_setref).

    > [!TIP]
    > Pokud není uvedené požadované nastavení, vyberte možnost **Konfigurace dalších nastavení, která nejsou ve skupinách výchozích nastavení**. Tato možnost přidá do průvodce stránku **Další nastavení** .

1. Na každé stránce nastavení nakonfigurujte potřebná nastavení. Pokud je nastavení podporuje, můžete také **napravit nevyhovující nastavení**. Pokud zařízení vyhodnotí nastavení jako nedodržující tuto položku konfigurace, opraví nastavení tak, aby vyhovovalo.

    Pro každou skupinu nastavení můžete také nakonfigurovat závažnost, kterou hlásí, když nastavení nedodržuje předpisy. Vyberte jednu z následujících hodnot pro možnost **závažnost neshody pro sestavy** :

    - **Žádné**: zařízení, které nesplní toto pravidlo dodržování předpisů, nehlásí pro sestavy Configuration Manager žádné závažnost selhání.

    - **Informace**

    - **Upozornění**

    - **Kritické**

    - **Kritické s událostí**: zařízení, které nesplní toto pravidlo dodržování předpisů, nahlásí u sestav Configuration Manager závažnost selhání typu **kritické** . Také protokoluje stav nedodržující předpisy jako událost systému Windows v protokolu událostí aplikace.

1. Na stránce průvodce **použitelnost platformy** zkontrolujte nastavení, která nejsou kompatibilní s vybranými podporovanými platformami. Vraťte se a odeberte tato nastavení, změňte platformy podpory nebo pokračujte.

    > [!IMPORTANT]
    > Zařízení nevyhodnocují shodu nepodporovaných nastavení.

1. Dokončete průvodce.

Novou položku konfigurace můžete zobrazit v uzlu **Položky konfigurace** pracovního prostoru **Prostředky a kompatibilita** .

## <a name="settings-reference"></a><a name="bkmk_setref"></a>Odkaz nastavení  

Následující části obsahují podrobnosti o konkrétních nastaveních dostupných v jednotlivých skupinách. Tato nastavení nakonfigurujte na stránce **nastavení zařízení** **Průvodce vytvořením položky konfigurace** pro **Windows 8.1 a zařízení s Windows 10** spravovaná *bez* klienta Configuration Manager.

### <a name="password"></a>Heslo

Tato nastavení platí jenom pro zařízení s Windows 10 a novějším.

- **Vyžadovat nastavení hesla na zařízeních**: vyžadovat heslo na podporovaných zařízeních.
- **Minimální délka hesla (ve znacích)**: minimální délka hesla.
- **Vypršení platnosti hesla během dnů**: počet dní, než uživatel musí změnit heslo.
- **Počet zapamatovaných hesel**: zabraňuje opakovanému použití dřív použitých hesel.
- **Počet neúspěšných pokusů o přihlášení před vymazáním zařízení**: Pokud tento počet pokusů o přihlášení selže, zařízení MDM ho vymaže.
- **Doba nečinnosti před uzamčením zařízení**: zadejte dobu, po kterou může být zařízení nečinné, než bude uzamčené. Zařízení je nečinné, když není žádný uživatelský vstup.
- **Složitost hesla**: zvolte, jestli můžete zadat číselný kód PIN, například `1234` , nebo jestli musíte zadat silné heslo.
  - **Počet složitých znakových sad vyžadovaných v hesle**: Pokud je složitost hesla **silná**, vyberte, kolik typů znaků heslo vyžaduje: velká písmena, malá písmena, číslice nebo symboly. Ve výchozím nastavení je tato hodnota `2` .
- **Odeslat PIN obnovení hesla na Exchange Server**

### <a name="device"></a>Zařízení

- **Snímek obrazovky**: Povolením tohoto nastavení umožníte uživateli pořídit obrazovku zařízení. (Pouze Windows 10)
- **Odeslání diagnostických dat**: Toto nastavení povolte, pokud chcete povolit diagnostická data Windows pro analýzy. (Pouze Windows 8.1)
- **Povolit odeslání diagnostických dat (Windows 10)**: Nastavte úroveň diagnostických dat Windows pro analýzy: Disable, Basic, Enhanced nebo Full. (Pouze Windows 10)
- **Zeměpisná poloha**: Toto nastavení povolte, pokud chcete, aby zařízení používalo informace o službách zjišťování polohy. (Pouze Windows 10)
- **Zkopírování a vložení**: Povolením tohoto nastavení můžete přenášet data mezi aplikacemi pomocí kopírování a vkládání. (Pouze Windows 10)
- **Obnovení továrního**nastavení: Toto nastavení povolte, pokud chcete, aby uživatel obnovil původní nastavení zařízení. (Pouze Windows 10)
- **Bluetooth**: povolí nebo zakáže použití funkce Bluetooth zařízení.
- **Zjistitelný režim Bluetooth**: povolí nebo zakáže, aby se zařízení zjistilo v jiných zařízeních Bluetooth. (Pouze Windows 10)
- **Inzerce Bluetooth**: povolí nebo zakáže používání reklamy přes Bluetooth. (Pouze Windows 10)
- **Záznam hlasu**: povolí nebo zakáže použití funkcí záznamu hlasu na zařízení. (Pouze Windows 10)
- **Cortana**: povolí nebo zakáže použití hlasového asistenta Cortany. (Pouze Windows 10)
- **Oznámení centra akcí**: povolí nebo zakáže podokno oznámení ve Windows 10. (Pouze Windows 10)
- **Změny nastavení oblasti (jenom desktopové aplikace)**: povolí nebo zakáže uživateli měnit místní nastavení na zařízení.
- **Změny nastavení napájení a režimu spánku (jenom desktopové aplikace)**: povolí nebo zakáže uživateli měnit nastavení napájení a režimu spánku na zařízení.
- **Změny nastavení jazyka (jenom desktopové verze)**: povolí nebo zakáže uživateli změnit nastavení jazyka v zařízení.
- **Změna systémového času**: povolí nebo zakáže uživateli změnit datum a čas zařízení.
- **Úprava názvu zařízení**: povolí nebo zakáže uživateli změnit název zařízení.

### <a name="email-management"></a>Správa e-mailů

Tato nastavení jsou pro zařízení s Windows 8.1 a Windows 10.  

- **E-mail protokolu POP a IMAP**: povolí nebo zakáže připojení k e-mailovým účtům, které používají standardy pop a IMAP.
- **Maximální doba, po kterou se má zachovat e-mail**: jak dlouho se má zachovat e-mail před tím, než server odstraní.
- **Povolené formáty zpráv**: Určete, jestli jsou e-maily **prostým textem** nebo **HTML a prostým textem**.
- **Maximální velikost pro emaily s prostým textem (automaticky stažené)**: Nastavte maximální velikost e-mailů s prostým textem, když se stáhnou automaticky.
- **Maximální velikost e-mailu ve formátu HTML (automaticky stažené)**: Nastavte maximální velikost e-mailů HTML při jejich automatickém stažení.
- **Maximální velikost přílohy (automaticky stažené)**: Nastavte maximální velikost příloh e-mailů, které se stáhnou automaticky.
- **Synchronizace kalendáře**: povolí nebo zakáže synchronizaci kalendářů se zařízením.
- **Vlastní e-mailový účet**: povolí nebo zakáže použití e-mailového účtu, který není v organizaci na zařízení.
- **Nastavit účet Microsoft jako volitelný v aplikaci Windows pošta**: tuto možnost povolte, pokud nepožadujete účet Microsoft ve Windows mailu.

### <a name="store"></a>Store

Tato nastavení platí jenom pro zařízení s Windows 10 a novějším.

- **Obchod s aplikacemi**: povolí nebo zakáže přístup k Microsoft Store na zařízení.
- **Zadejte heslo pro přístup do obchodu s aplikacemi**: tuto možnost povolte, pokud chcete, aby uživatelé zadali heslo pro přístup k aplikaci Microsoft Store.
- **Nákupy v aplikaci**: povolí nebo zakáže uživatelům vytvářet nákupy v aplikaci.
- **Spuštění aplikace pocházející ze Storu**: zakáže všechny aplikace, které byly na zařízení předem nainstalované, nebo nainstalované z Microsoft Store.
- Automaticky **aktualizovat aplikace ze Storu**: povolí nebo zakáže aplikace nainstalované z Microsoft Store k automatické aktualizaci.
- **Nainstalovat aplikace na systémovou jednotku**: povolí nebo zakáže zařízení instalovat aplikace na systémovou jednotku, což je obvykle `C:` jednotka.
- **Nainstalovat data aplikací na systémový svazek**: tuto možnost povolte, pokud chcete, aby aplikace ukládaly data na systémovou jednotku.
- **Použít pouze privátní úložiště**: vyžaduje, aby uživatelé stáhli aplikace z vašeho privátního úložiště.
- Záznam ze **hry**: zakázání zaznamenávání a vysílání her ve Windows

### <a name="browser"></a>Prohlížeč

Tato nastavení jsou pro zařízení s Windows 8.1 a Windows 10.

- **Povolení webového prohlížeče**: povolí nebo zakáže použití webového prohlížeče na zařízení.
- Automatické **vyplňování**: povoluje nebo zakazuje změnu nastavení automatického dokončování v prohlížeči.
- **Aktivní skriptování**: povolí nebo zakáže, jestli prohlížeč může spouštět skripty, například skripty ActiveX.
- **Moduly plug-in**: povolí nebo zakáže přidávání modulů plug-in do Internet Exploreru.
- **Blokování automaticky otevíraných oken**: povolí nebo zakáže blokování automaticky otevíraných oken v prohlížeči.
- **Soubory cookie**: povoluje nebo zakazuje ukládání souborů cookie do zařízení.
- **Upozornění na podvod**: povolí nebo zakáže upozornění na potenciální podvodné weby.

### <a name="internet-explorer"></a>Internet Explorer

Tato nastavení jsou pro zařízení s Windows 8.1 a Windows 10.

- **Vždy odesílat hlavičku do Not Track**: povolit nebo zakázat odesílání informací o procházení webům třetích stran.
- **Zóna zabezpečení intranetu**: povolí nebo zakáže přiřazení úrovně zabezpečení k zóně zabezpečení intranetu.
- **Úroveň zabezpečení pro zónu Internetu**: Nastavte úroveň zabezpečení pro zónu Internetu: vysoká, střední-vysoká nebo střední.
- **Úroveň zabezpečení pro zónu intranetu**: Nastavte úroveň zabezpečení pro zónu intranetu: vysoká, střední-vysoká, střední, střední, nízká nebo nízká.
- **Úroveň zabezpečení pro zónu důvěryhodných lokalit**: Nastavte úroveň zabezpečení pro zónu důvěryhodných lokalit: vysoká, střední-vysoká, střední, střední, nízká nebo nízká.
- **Úroveň zabezpečení pro zónu lokalit s omezeným přístupem**: Nastavte úroveň zabezpečení pro zónu lokalit s omezeným přístupem: vysoká.
- **Obory názvů pro zónu intranetu**: Nakonfigurujte weby tak, aby se přidaly nebo odebraly ze zóny intranetu.
- **Přejít na intranetový web pro použití jediného slova**: povolí nebo zakáže, aby Internet Explorer automaticky přešel na intranetový web, pokud uživatel zadá platný název lokality bez předchozího protokolu, například `https://` .
- **Možnost nabídky podnikového režimu**: umožňuje uživatelům aktivovat a deaktivovat podnikový režim z nabídky **nástroje** Internet Exploreru.
  - **Umístění sestavy protokolování (URL)**: Pokud je aktivní režim rozlehlé sítě, zadejte adresu URL pro protokolování navštívených webů.
- **Umístění seznamu webů podnikového režimu (URL)**: Pokud je aktivní podnikový režim, zadejte seznam webů, které ho používají.

### <a name="cloud"></a>Cloud

Tato nastavení jsou pro zařízení s Windows 8.1 a Windows 10.

- **Synchronizace nastavení**: povoluje nebo zakazuje synchronizaci nastavení mezi zařízeními.
- **Synchronizace přihlašovacích údajů**: povolí nebo zakáže synchronizaci přihlašovacích údajů mezi zařízeními.
- **Účet Microsoft**: Toto nastavení povolte, pokud chcete povolit použití účet Microsoft na zařízení.
- **Synchronizace nastavení přes připojení účtovaná podle objemu dat**: povolí nebo zakáže synchronizaci nastavení při měření síťového připojení.

### <a name="security"></a>Zabezpečení

- **Nepodepsaná instalace souboru**: umožňuje, kdo může nainstalovat nepodepsaný soubor. (Pouze Windows 10)
- **Nepodepsané aplikace**: povolí nebo zakáže instalaci nepodepsaných aplikací. (Pouze Windows 10)
- **Zasílání zpráv SMS a MMS**: povolí nebo zakáže protokoly textových zpráv na zařízení. (Pouze Windows 10)
- **Vyměnitelné úložiště**: povolí nebo zakáže použití vyměnitelného úložiště, třeba SD karty. (Pouze Windows 10)
- **Kamera**: povolí nebo zakáže použití kamery zařízení. (Pouze Windows 10)
- **Bezkontaktní komunikace (NFC)**: povolí nebo zakáže komunikaci pomocí NFC. (Pouze Windows 10)
- **Režim ochrany před krádeží**: povolí nebo zakáže použití režimu AntiTheft pro Windows 10. (Pouze Windows 10)
- **Povolení připojení USB**: povolí nebo zakáže ostatním zařízením, aby se připojovala k tomuto zařízení pomocí připojení USB. (Pouze Windows 10)
- **Profil sítě VPN systému Windows RT**: zřídí profil sítě VPN pro zařízení se systémem Windows RT (pouze Windows 8.1)

### <a name="peak-synchronization"></a>Synchronizace ve špičce

Tato nastavení platí jenom pro zařízení s Windows 10 a novějším.

- **Zadejte dobu špičky**: Nastavte dobu špičky a dny v týdnu pro synchronizaci mobilního zařízení.
- **Četnost synchronizace ve špičce**: Nakonfigurujte, jak často dochází k synchronizaci během špičky.
- **Četnost synchronizace mimo špičku**: Nakonfigurujte, jak často dochází k synchronizaci mimo dobu špičky.

### <a name="roaming"></a>Roaming

- **Správa zařízení při roamingu**: povolí nebo zakáže Configuration Manager správě zařízení při roamingu. (Pouze Windows 10)
- **Stahování softwaru při roamingu**: povolí nebo zakáže stahování aplikací a softwaru při roamingu. (Pouze Windows 10)
- **Stažení e-mailu při roamingu**: povolí nebo zakáže stahování e-mailů při roamingu. (Pouze Windows 10)
- **Roaming dat**: povolí nebo zakáže roaming mezi sítěmi při přístupu k datům.
- **VPN v mobilní**síti: povolí nebo zakáže zařízení používat připojení VPN při připojení k mobilní síti. (Pouze Windows 10)
- **Roaming VPN v mobilní**síti: povolí nebo zakáže zařízení používat připojení VPN při roamingu v mobilní síti. (Pouze Windows 10)

### <a name="encryption"></a>Šifrování

- **Šifrování paměťové karty**: nastavte zapnuto, pokud chcete, aby uživatel zašifroval všechny paměťové karty použité v zařízení. (Pouze Windows 10)
- **Šifrování souborů v zařízení**: nastaveno na k šifrování souborů uložených v zařízení.
- **Vyžadovat podepisování e-mailů**: uživatel musí před odesláním digitálně podepsat e-maily.
  - **Podpisový algoritmus**: vyberte algoritmus pro podpisové e-maily: Default, SHA nebo MD5.
- **Vyžadovat šifrování e-mailu**: uživatel musí před odesláním šifrovat e-maily.
  - **Šifrovací algoritmus**: vyberte algoritmus pro šifrování e-mailů: výchozí, Triple DES, des, RC2 128-bit, RC2 64-bit, RC2 40-bit

### <a name="wireless-communications"></a>Bezdrátová komunikace

Tato nastavení platí jenom pro zařízení s Windows 10 a novějším.

- **Bezdrátové připojení k síti**: povolí nebo zakáže schopnost Wi-Fi zařízení.
- **Sdílení internetového připojení přes Wi-Fi**: umožní uživateli používat zařízení jako mobilní hotspot.
- Pokud je to možné, přesměrujte **data na Wi-Fi**: Povolte zařízení používat připojení Wi-Fi co nejvíce.
- **Vytváření sestav Wi-Fi hotspotů**: povolí zařízení odesílat informace o připojeních Wi-Fi, aby uživatel mohl zjistit okolní připojení.
- **Ruční konfigurace Wi-Fi**: povolí uživateli ruční konfiguraci bezdrátových připojení.

#### <a name="configured-wireless-network-connections"></a>Konfigurovaná bezdrátová síťová připojení

1. Na stránce **Konfigurovat nastavení bezdrátové komunikace mobilního zařízení** vyberte **Přidat**.

1. V okně **bezdrátové připojení k síti** zadejte následující informace o bezdrátovém připojení, které se má zřídit na mobilních zařízeních:

    - **Název sítě (SSID)**: zadejte název sítě Wi-Fi.
    - **Síťové připojení**: vyberte možnost **Internet** nebo **práce**.
    - **Ověřování**: Vyberte metodu ověřování pro bezdrátové připojení:
        - **Otevřít**
        - **Shared**
        - **WPA**
        - **WPA-PSK**
        - **WPA2**
        - **WPA2-PSK**
    - **Šifrování dat**: Vyberte metodu šifrování, kterou toto připojení používá. Dostupné hodnoty se mění v závislosti na vybrané metodě **ověřování** :
        - **Disabled** (Zakázáno)
        - **WEP**
        - **TKIP**
        - **AES**
    - **Index klíče**: Pokud nastavíte **šifrování dat** na **WEP**, vyberte index klíče od **1** do **4**.
    - **Tato síť se připojuje k Internetu**: Zadejte nastavení proxy serveru a umožněte tak mobilním zařízením v bezdrátové síti připojit se k Internetu.
        - **Nastavení proxy serveru**: Nakonfigurujte nastavení **serveru** a **portu** pro proxy servery **http**, **WAP**a **Sockets** .
    - **Nastavení 802.1 x**:
        - **Povolit 802.1 x přístup k síti**: Zabezpečte připojení zadáním typu EAP.
        - **Typ protokolu EAP**: vyberte jeden z následujících ověřovacích protokolů:
            - **PEAP**
            - **Karta SmartCard nebo certifikát**

### <a name="certificates"></a>Certifikáty

Importujte certifikáty pro instalaci na mobilních zařízeních.

Vyberte **importovat**a pak zadejte následující hodnoty:

- **Soubor certifikátu**: vyhledejte a vyberte soubor certifikátu (**. cer**), který chcete importovat.
- **Cílové úložiště**: vyberte aspoň jedno z následujících úložišť certifikátů:
  - **Zobrazuje**
  - **CA**
  - **Normální**
  - **Privilegovaný**
  - **Certifikát SPC**
  - **Partnerský uzel**
- **Role**: Pokud vyberete úložiště certifikátů certifikát **SPC** (Software Publisher Certificate), vyberte roli, kterou chcete přidružit k certifikátu:
  - **Mobilní operátor**
  - **Manager**
  - **Uživatel byl ověřen**
  - **Správce IT**
  - **Uživatel nebyl ověřen**
  - **Důvěryhodný zřizovací server**

### <a name="system-security"></a>Zabezpečení systému

- **Řízení uživatelských účtů**: nakonfiguruje chování nástroje řízení uživatelských účtů systému Windows na zařízení.
- **Síťová brána firewall**: vyžaduje, aby systém Windows povolil vestavěnou bránu firewall. (Windows 8.1)
- **Aktualizace**: Nakonfigurujte chování aktualizací softwaru Windows. (Windows 8.1)
  - **Minimální klasifikace aktualizací**: vyberte minimální klasifikaci aktualizací, které se mají stáhnout a nainstalovat: **žádné**, **důležité**nebo **Doporučené**.
- **Aktualizace (Windows 10)**: Konfigurace chování Windows Software Updates. (Pouze Windows 10)
  - **Den instalace**: vyberte naplánovaný den, kdy zařízení automaticky nainstaluje aktualizace a restarty. (Pouze Windows 10)
  - **Čas instalace**: vyberte naplánovaný čas, kdy zařízení automaticky nainstaluje aktualizace a restarty. (Pouze Windows 10)
- **SmartScreen**: povolení nebo zákaz automatické obrazovky Windows
- **Antivirová ochrana**: vyžaduje, aby systém Windows měl antivirový software.
- **Signatury antivirové ochrany jsou aktuální**: vyžaduje, aby byly soubory signatur antivirové ochrany aktuální.
- **Zobrazení oznámení na zamykací obrazovce**: povolí nebo zakáže oznámení, která se mají zobrazit na zamykací obrazovce.
- **Předběžné verze funkcí**: umožňuje nakonfigurovat, jestli zařízení přijímá předběžné verze nastavení a funkce. (Pouze Windows 10)
- **Ruční instalace kořenového certifikátu**: povolí nebo zakáže uživateli ruční instalaci kořenového certifikátu, který umožňuje důvěryhodnost pro jakýkoli certifikát vydaný tímto kořenem. (Pouze Windows 10)
- **Povolení ručního zrušení registrace**: povolí nebo zakáže uživateli zrušit registraci zařízení v místní správě mobilních zařízení pomocí Configuration Manager.

### <a name="windows-server-work-folders"></a>Pracovní složky Windows Serveru

Tato nastavení jsou pro zařízení s Windows 8.1 a Windows 10.

- **Adresa URL pracovních složek**: zadejte umístění pracovní složky Windows serveru, ke které se uživatelé můžou připojit ze svého zařízení.

### <a name="allowed-and-blocked-apps-list"></a>Seznam povolených a blokovaných aplikací

Tato nastavení platí jenom pro zařízení s Windows Phone, která Configuration Manager místní MDM nepodporuje. Další informace najdete v tématu [co se stalo se hybridem?](../understand/what-happened-to-hybrid.md).

### <a name="windows-10-team"></a>Windows 10 Team

Tato nastavení platí jenom pro zařízení s Windows 10 Team.

- **Dovolit automatické probuzení obrazovky, když senzory zjišťují někoho v místnosti**: povolí nebo zakáže automatické probuzení zařízení, když jeho Senzor detekuje někoho v místnosti.
- **Vyžadovat kód PIN pro bezdrátovou projekci**: povolí nebo zakáže, jestli musíte zadat PIN kód, než se může jiné zařízení připojit bezdrátově pro projekci.
- Časové **období údržby**: Toto nastavení povolte, pokud chcete, aby se při instalaci a restartování zařízení mohl aktualizovat okno.
  - **Čas spuštění**: nastavte čas zahájení časového intervalu pro správu a údržbu.
  - **Doba trvání (hodiny)**: nastavte délku v hodinách časového období údržby.
- **Azure Operational Insights**: povolí [službě Azure Operational Insights](https://azure.microsoft.com/resources/videos/azure-operational-insights-overview/) shromažďovat, ukládat a analyzovat data souborů protokolu ze zařízení s Windows 10 Team.
  - **ID pracovního prostoru**: Zadejte platné ID pracovního prostoru.
  - **Klíč pracovního prostoru**: Zadejte klíč pro přidružený pracovní prostor.
- **Bezdrátová projekce Miracast**: umožňuje zařízením s podporou Miracast povolit projekt pro toto zařízení s Windows 10 Team.
  - **Kanál Miracast**: vyberte kanál Miracast k obsahu projektu.
- **Informace o schůzce zobrazené na úvodní obrazovce**: Vyberte typ informací, které se zařízení zobrazí na dlaždici **schůzky** na **úvodní** obrazovce:
  - **Zobrazit jenom organizátora a čas**
  - **Zobrazit organizátora, čas a předmět (u privátních schůzek je předmět skrytý)**
- **Adresa URL obrázku pozadí zamykací obrazovky**: zadejte adresu URL pro zobrazení vlastního pozadí na **úvodní** obrazovce zařízení s Windows 10 Team. Spusťte adresu URL `https://` a použijte formát PNG.

### <a name="windows-information-protection"></a>Windows Information Protection  

Další informace o tom, jak nakonfigurovat ochranu podnikových dat pomocí Configuration Manager, najdete v tématu [Ochrana podnikových dat pomocí Windows Information Protection (NV)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip).

### <a name="microsoft-edge-legacy"></a>Microsoft Edge starší verze

Tato nastavení platí jenom pro zařízení s Windows 10 a novějším.  

- **Povolit návrhy hledání na adresním řádku**: umožňuje vyhledávacímu webu navrhovat při zadávání vyhledávacích frází lokality.
- **Povolit do Not Track**: informujte weby, které nechcete, aby sledovaly vaši návštěvu.
- **Povolit filtr SmartScreen**: Ověřte, že stažené soubory neobsahují škodlivý kód.
- **Povolí automaticky otevíraná**okna: konfigurovat automaticky otevíraná okna prohlížeče.
- **Povoluje soubory cookie**: umožňuje nakonfigurovat použití souborů cookie.
- **Povolit automatické vyplňování**: umožní prohlížeči automaticky vyplnit formuláře uloženými informacemi, jako je jméno, adresa a telefon.
- **Povolit správce hesel**: umožňuje prohlížeči ukládat a spravovat hesla pro weby.
- **Vývojářské nástroje**: povolí nebo zakáže funkci vývojářských nástrojů Edge.
- **Rozšíření**: povoluje nebo zakazuje rozšíření Edge.
- **Procházení InPrivate**: povolí nebo zakáže procházení InPrivate, které neukládá historii ani soubory cookie.
- **IP adresa WebRTC localhost**: povolí nebo zakáže IP adresu místního hostitele zařízení, která se zobrazí, když uživatel provede telefonní hovory pomocí protokolu Web RTC.
- **Blokovat přístup ke stránce About: Flags**: povolí nebo zakáže uživateli přístup na `about:flags` stránku, která obsahuje vývojáře a experimentální nastavení.
- **Přepsání výzvy SmartScreen pro soubory**: povolí nebo zakáže uživateli obejít upozornění filtru SmartScreen týkající se stahování potenciálně škodlivých souborů.
- **Přepsání výzvy SmartScreen**: povolí nebo zakáže uživateli obejít upozornění filtru SmartScreen na potenciálně škodlivé weby.
- **Adresa URL prvního spuštění**: Zadejte web, který se zobrazí, když uživatel poprvé otevře okraj.

### <a name="windows-defender-antivirus"></a>Antivirová ochrana v programu Windows Defender

Tato nastavení platí jenom pro zařízení s Windows 10 a novějším.

- **Povolit monitorování v reálném čase**: Povolit kontrolu malwaru, spywaru a dalšího nežádoucího softwaru v reálném čase.
- **Povolení monitorování chování**: Defender kontroluje určité známé vzorce podezřelé aktivity na zařízeních.
- **Povolit systém kontroly sítě**: systém kontroly sítě (NIS) pomáhá chránit zařízení před zneužitím prostřednictvím sítě. Používá signatury známých slabých míst z Centra Microsoftu pro ochranu koncových bodů ke zjištění a blokování škodlivého síťového provozu.
- **Kontrolovat všechna stahování**: Defender kontroluje všechny soubory, které jste stáhli z Internetu.
- **Povolení kontroly skriptů**: Defender kontroluje skripty, které se používají v Internet Exploreru.
- **Monitorovat aktivitu souborů a programů**: Defender sleduje aktivitu souborů a programů na zařízeních.
  - **Monitorovaných souborů**: Vyberte typ souborů, které se mají monitorovat: vše, příchozí nebo odchozí.
- Počet **dní pro sledování vyřešeného malwaru**: Defender pokračuje v sledování vyřešeného malwaru po zadaný počet dnů. Pak můžete ručně ověřit dříve zasažená zařízení. Pokud nastavíte počet dní na 0, malware zůstane ve složce karanténa a automaticky se neodebere. Maximální hodnota je 90.
- **Povolení přístupu k uživatelskému rozhraní klienta**: Určuje, jestli se má skrýt uživatelské rozhraní Defenderu pro uživatele. Když toto nastavení změníte, projeví se při příštím restartování zařízení.
- **Naplánovat kontrolu systému**: zvolte úplnou nebo rychlou kontrolu, ke které dochází pravidelně v den a čas, který vyberete:
  - **Naplánovaný den**: vyberte naplánovaný den, kdy má Defender spustit kontrolu.
  - **Naplánovaný čas**: vyberte naplánovaný čas, kdy má Defender spustit kontrolu.
- **Naplánovat každodenní rychlou kontrolu**: vyberte naplánovaný čas, kdy Defender spouští rychlou kontrolu každý den.
- **Omezit využití procesoru při kontrole**: nastavte procento procesoru, který může Defender využít při spuštění kontroly. Zadejte hodnotu od 1 do 100.
- **Kontrolovat archivní soubory**: Defender prohledává Komprimované archivy, jako jsou soubory. zip nebo. cab.
- **Kontrolovat e-mailové zprávy**: Defender kontroluje e-mailové zprávy při jejich doručování do zařízení.
- **Kontrolovat vyměnitelné jednotky**: Defender vyhledává vyměnitelné jednotky, jako jsou USB hole.
- **Kontrolovat namapované jednotky**: Defender kontroluje jednotky, které jsou namapované na sdílené síťové složky. Například `H:` je namapován na osobní disk uživatele. Pokud jsou soubory na disku jen pro čtení, Defender nemůže odebrat žádný malware, který tam najde.
- **Kontrolovat soubory otevřené ze síťových sdílených složek**: Defender prohledává soubory, když je uživatel otevře ze sdílené síťové cesty. Například, `\\server\share\file.doc`. Pokud je soubor sdílené složky jen pro čtení, Defender nemůže odebrat nalezený malware.
- **Interval aktualizace signatur**: vyberte časový interval, po kterém program Defender kontroluje nové soubory signatur.
- **Povolit cloudovou ochranu**: Defender používá Microsoft Cloud k získávání informací o aktivitě malwaru a umožňuje funkcím, jako je například blok, na první pohled.
- **Vyzvat uživatele k odeslání vzorků**: vyberte chování pro Defender, kdy mohou soubory vyžadovat další analýzu. Defender může například automaticky odeslat soubory do Microsoftu a zjistit, jestli jsou škodlivé.
- **Detekce potenciálně nežádoucích aplikací**: chrání zařízení před spuštěním softwaru, který je klasifikován Defenderem jako potenciálně nežádoucí. Můžete chránit před těmito aplikacemi nebo použít režim auditu k hlášení, že uživatel nainstaluje potenciálně nežádoucí aplikaci.
- **Vyloučení souborů a složek**: do seznamu vyloučení přidejte jeden nebo více souborů a složek. Příkladem je `C:\Path` nebo `%ProgramFiles%\Path\filename.exe`. Defender nezahrnuje tyto soubory a složky v reálném čase nebo v naplánovaných kontrolách.
- **Vyloučení přípony souboru**: do seznamu vyloučení přidejte jednu nebo více přípon souborů. Příkladem je `java` nebo `exe`. Defender neobsahuje žádné soubory s těmito příponami v reálném čase nebo v plánovaných kontrolách.
- **Vyloučení procesů**: přidejte konkrétní procesy do seznamu vyloučení. Například, `C:\path\myproc.exe`. Tento typ vyloučení podporuje pouze následující rozšíření: `exe` , `com` nebo `scr` . Defender nezahrnuje tyto procesy v reálném čase nebo v plánovaných kontrolách.

### <a name="additional-settings"></a>Další nastavení

Pokud v průvodci na stránce **nastavení zařízení** vyberete možnost **Konfigurace dalších nastavení, která nejsou ve skupinách výchozích nastavení**, nakonfigurujte tato nastavení pomocí této stránky **Další nastavení** . Vyberte **Přidat** a potom vyberte ze seznamu dostupných nastavení mobilních zařízení. Zvolte **možnost vybrat** , pokud chcete upravit předdefinované nastavení, nebo **vytvořte nastavení** pro vytvoření vlastního hodnoty registru nebo nastavení OMA URI.

## <a name="next-steps"></a>Další kroky

[Monitorování nastavení dodržování předpisů](../../compliance/deploy-use/monitor-compliance-settings.md)
