---
title: Novinka ve verzi 1602
titleSuffix: Configuration Manager
description: Získejte podrobnosti o změnách a nových funkcích zavedených ve verzi 1602 Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4021eca1-adfb-4e5a-adee-159263c29637
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9a54ee5fb427f276ec755e748513b178d0c026ab
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698567"
---
# <a name="what39s-new-in-version-1602-of-configuration-manager"></a>Co&#39;s novinkou ve verzi 1602 Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*


Aktualizace 1602 pro Configuration Manager je k dispozici pouze v rámci konzoly aktualizace pro dříve nainstalované lokality, které používají verzi 1511. Verze 1511 je počáteční základní verze, kterou použijete k instalaci nových lokalit Configuration Manager.  


> [!TIP]  
> Přečtěte si další informace:  
>   
> - [Instalace nových lokalit](../../servers/deploy/install/prepare-to-install-sites.md) (pomocí základní verze, jako je 1511)  
> - [Instalace aktualizací v lokalitách](../../servers/manage/updates.md) (například aktualizace 1602)  

 Následující části obsahují podrobné informace o změnách a nových funkcích, které jsou představené ve verzi 1602 Configuration Manager.  

## <a name="site-infrastructure"></a>Infrastruktura webu  

###  <a name="in-place-upgrade-the-operating-system-of-site-servers-that-run-windows-server-2008-r2"></a><a name="bkmk_UpgradeOS"></a> Místní upgrade operačního systému serverů lokality, na kterých běží Windows Server 2008 R2  
 Configuration Manager weby, na kterých běží verze 1602 nebo novější, podporují místní upgrade operačního systému serverů lokality ze systému Windows Server 2008 R2 na Windows Server 2012 R2.  

> [!WARNING]  
>  Před provedením upgradu na Windows Server 2012 R2 je nutné ze serveru odinstalovat službu WSUS 3.2.  
>   
>  Další informace o tomto důležitém kroku najdete v části "nové a změněné funkce" v tématu [přehled Windows Server Update Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345(v=ws.11)#new-and-changed-functionality).  

 Chcete-li upgradovat server, použijte postupy upgradu systému Windows Server 2012 R2. Po upgradu nemusíte spouštět obnovení serveru lokality Configuration Manager. Postupy upgradu najdete v tématu [Možnosti upgradu pro Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11)) v dokumentaci k systému Windows Server.  

###  <a name="sql-server-alwayson-availability-groups"></a><a name="bkmk_AOAG"></a> SQL Server skupiny dostupnosti AlwaysOn  
 Použijte SQL Server skupiny dostupnosti AlwaysOn k hostování databáze lokality v primárních lokalitách a lokalitu centrální správy jako řešení zotavení po havárii s vysokou dostupností.  

 Podrobnosti najdete v tématu [SQL Server AlwaysOn pro databázi lokality s vysokou dostupností pro Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

## <a name="operating-system-deployment"></a>Nasazení operačního systému  

### <a name="windows-10-servicing"></a>Údržba Windows 10  
 V Configuration Manager verze 1602 se přidala následující vylepšení pro obsluhu Windows 10:  

-   K dispozici jsou nové možnosti filtru pro plány údržby, které vám umožňují filtrovat podle **jazyka**, **povinného**a **názvu**. Do daného nasazení se přidají jenom upgrady, které odpovídají zadaným kritériím.  

-   Když pro synchronizaci aktualizací softwaru vyberete klasifikaci **upgrady** , zobrazí se upozornění. Toto upozornění vám umožní zjistit, že se vyžaduje [oprava hotfix 3095113](https://support.microsoft.com/kb/3095113) for Windows Server Update Services (WSUS) 4,0 předtím, než budete moct úspěšně synchronizovat aktualizace softwaru, a aby Údržba Windows 10 fungovala správně. Z varovné zprávy můžete přejít na příslušný článek znalostní báze Knowledge Base.  

-   Dostupné upgrady Windows 10 se teď zobrazují jenom v uzlu aktualizace Windows **10**  \  pro**všechny systémy Windows** 10 konzoly Configuration Manager. Tyto aktualizace se už nezobrazují v uzlu aktualizace **softwaru**  \  **všechny aktualizace softwaru** v konzole nástroje.  

-   Plán údržby se považuje za vysoce rizikové nasazení a v okně **Vybrat kolekci** se zobrazují pouze vlastní kolekce, které splňují nastavení ověřování nasazení nakonfigurovaná ve vlastnostech lokality. Další informace najdete v tématu [nastavení pro správu nasazení s vysokým rizikem pro Configuration Manager](../../servers/manage/settings-to-manage-high-risk-deployments.md).  

-   Uživatelé, kteří spouštějí balíček s upgradem Windows 10, teď obdrží zprávu, že budou upgradovat svůj operační systém.  

## <a name="application-management"></a>Správa aplikací  

### <a name="ios-app-configuration-policies"></a>Zásady konfigurace aplikací pro iOS  
 Zásady konfigurace aplikací Configuration Manager slouží k poskytnutí nastavení, která se můžou požadovat, když uživatel spustí aplikaci pro iOS. Aplikace může například vyžadovat, aby uživatel určil vlastní číslo portu, jazyk, nastavení zabezpečení nebo nastavení brandingu (například logo společnosti). Pokud jsou tato nastavení nesprávně zadaná, může to zvýšit zatížení vašeho helpdesku a také zpomalit přijímání nových aplikací.  

 Zásady konfigurace aplikací vám pomůžou tyto problémy eliminovat tím, že vám umožní nasadit tato nastavení pro uživatele v zásadách před spuštěním aplikace. Nastavení je pak zadáno automaticky a uživatel nemusí provádět žádnou akci.

### <a name="manage-volume-purchased-ios-apps"></a>Správa hromadně zakoupených aplikací pro iOS  
 Configuration Manager vám může pomáhat s nasazením a správou aplikací, které jste koupili v hromadném využití programu Apple Volume purchase program (VPP). Configuration Manager importuje informace o licencích z App Storu a sleduje, kolik licencí jste už použili.  


### <a name="automatic-creation-of-office-mobile-apps"></a>Automatické vytváření mobilních aplikací Office  
 Když aktualizujete na verzi 1602 z 1511, Configuration Manager automaticky vytvoří následující systém Microsoft Office mobilní aplikace pro Android a iOS:  

-   Microsoft Word  

-   Microsoft Excel  

-   Microsoft PowerPoint  

-   Microsoft OneDrive  

-   Microsoft OneNote (jenom iOS)  

-   Microsoft Outlook  

Tyto aplikace se nacházejí v uzlu **aplikace** konzoly Configuration Manager.  

 Další informace o nasazení aplikací najdete v tématu [nasazení aplikací pomocí Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

## <a name="software-updates"></a>Aktualizace softwaru  

### <a name="manage-office-365-client-updates"></a>Správa aktualizací klienta Office 365  
 Configuration Manager má možnost spravovat aktualizace klientů Office 365 pomocí pracovního postupu správy softwarových aktualizací. Další informace najdete v tématu [Správa aktualizací Office 365 ProPlus pomocí Configuration Manager](../../../sum/deploy-use/manage-office-365-proplus-updates.md).  

## <a name="compliance-settings"></a>Nastavení dodržování předpisů  

### <a name="compliance-settings-for-devices-running-windows-10-team"></a>Nastavení dodržování předpisů pro zařízení s Windows 10 Team  
 Do položky konfigurace **Windows 8.1 a Windows 10** se přidala nová nastavení. Tato nastavení vám pomůžou řídit zařízení s Windows 10 Team, jako je Surface Hub zařízení.  

 Podrobnosti najdete v tématu [Vytvoření položek konfigurace pro Windows 8.1 a zařízení s Windows 10 spravovaná bez klienta Configuration Manager](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="kiosk-mode-settings-for-android-samsung-knox-standard-devices"></a>Nastavení celoobrazovkového režimu pro zařízení se systémem Android Samsung KNOX Standard  
 Celoobrazovkový režim umožňuje uzamknout zařízení, aby fungovaly jenom některé funkce. Můžete třeba povolit, aby v zařízení běžela jenom jedna vámi určená spravovaná aplikace, nebo můžete na zařízení zakázat tlačítka hlasitosti. Tato nastavení se dají používat pro ukázkový model zařízení nebo pro zařízení, které je vyhrazené jenom pro jednu funkci, jako je třeba zařízení POS. V Configuration Manager teď můžete zadat nastavení celoobrazovkového režimu pro zařízení se zabezpečením Samsung KNOX Standard.  


## <a name="conditional-access"></a>Podmíněný přístup  

### <a name="conditional-access-for-pcs-managed-by-configuration-manager"></a>Podmíněný přístup pro počítače spravované pomocí Configuration Manager  
 Před tímto vydáním jste mohli nastavit podmíněný přístup k počítači, ale počítač byl buď zaregistrován v Intune, nebo musí být počítač připojený k doméně. Od aktualizace 1602 se podporuje podmíněný přístup pro počítače spravované pomocí Configuration Manager. Pro počítače, které jsou spravované pomocí Configuration Manager, můžete omezit přístup k Exchangi Online a SharePointu Online jenom na zařízení, která jsou kompatibilní se zásadami dodržování předpisů, které jste nastavili.  


### <a name="restricting-access-based-on-the-health-of-devices"></a>Omezení přístupu na základě stavu zařízení  
 Nyní můžete omezit přístup k e-mailu a službám Office 365 na základě stavu zařízení, jak je uvedeno ve službě Health Attestation. Zařízení spravovaná pomocí Intune jsou navíc obsažená v sestavách stavu zařízení.  

 Konzola Configuration Manager obsahuje nové pravidlo dodržování předpisů, které umožňuje určit, jestli se mají zařízení povolit nebo zablokovat přístup na základě jejich stavu. Podrobnosti o službě ověření stavu a o tom, jak se v Intune hlásí stav zařízení, najdete v tématu [ověření stavu pro Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### <a name="new-compliance-policy-rules"></a>Nová pravidla zásad dodržování předpisů  
 Byla přidána nová pravidla zásad dodržování předpisů, jako jsou automatické aktualizace a vyžadování hesla k odemknutí zařízení, aby se podporovaly lepší požadavky na zabezpečení.


### <a name="make-sure-enrolled-and-compliant-devices-always-have-access-to-exchange-on-premises"></a>Zajistěte, aby zaregistrovaná zařízení splňující předpisy měla vždycky přístup k místnímu Exchangi.  
 Když zaškrtnete tuto možnost, zařízení, která jsou zaregistrovaná v Intune a vyhovují zásadám dodržování předpisů, mají povolený přístup k místnímu Exchangi: **přepsání výchozího pravidla – vždy povolit zaregistrovaným a kompatibilním zařízením Intune přístup k místnímu Exchangi:**. Toto pravidlo je k dispozici na  **stránce Obecné** v **Průvodci konfigurací zásad podmíněného přístupu** pro místní Exchange.

 Toto pravidlo přepíše výchozí pravidlo. to znamená, že i když nastavíte výchozí pravidlo pro karanténu nebo blokování přístupu, zaregistrovaná zařízení splňující předpisy budou mít pořád přístup k místnímu Exchangi. Toto nastavení použijte, pokud chcete, aby zaregistrovaná zařízení splňující předpisy měla vždycky přístup k e-mailu prostřednictvím místního Exchange.   

 Podrobný návod najdete v tématu [Správa přístupu k e-mailu](../../../mdm/understand/what-happened-to-hybrid.md).  

## <a name="client-management"></a>Správa klientů  

### <a name="client-online-status"></a>Online stav klienta  
 Nový stav pro klienty je k dispozici pro monitorování, pokud je počítač online nebo ne. Počítač se považuje za online, pokud je připojený ke svému přiřazenému bodu správy. Pro indikaci, že je počítač online, klient odesílá do bodu správy zprávy typu příkazového testu. Pokud bod správy neobdrží zprávu po 5 minutách, klient bude považován za offline.  

 Podrobnosti najdete v tématu [Postup monitorování klientů](../../../core/clients/manage/monitor-clients.md).  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Aktualizovat počítač PC a zásady uživatele z centra softwaru  
 Nová možnost, **zásada synchronizace**, byla přidána do stránky **Možnosti**  >  **Údržba počítače** v centru softwaru, která způsobí, že počítač aktualizuje svůj Configuration Manager počítač a zásady uživatele.  

### <a name="software-center-branding-changes"></a>Změny brandingu centra softwaru  
 Můžete změnit barvu, název organizace a ikonu, která se zobrazí v centru softwaru. Tato nastavení se aplikují podle následujících pravidel:  

- Pokud není nainstalovaná role serveru lokality bodu webu katalogu aplikací, Centrum softwaru zobrazí název organizace uvedený v nastavení klienta **Počítačový agent** nazvaný **název organizace zobrazený v centru softwaru**.  

- Pokud je nainstalovaná role serveru lokality bodu webu katalogu aplikací, Centrum softwaru zobrazí název organizace a barvu určenou ve vlastnostech role serveru lokality bodu webu katalogu aplikací.  

- Pokud je předplatné Microsoft Intune nakonfigurované a připojené k Configuration Manager prostředí, Centrum softwaru zobrazí název organizace, barvu a logo společnosti zadané ve vlastnostech předplatného Intune.  

### <a name="health-attestation"></a>Ověření stavu  
 Správci mohou zobrazit stav Ověření stavu zařízení s Windows 10 v konzole nástroje Configuration Manager. To je k dispozici pro Configuration Manager a také Configuration Manager s Microsoft Intune. Ověření stavu zařízení umožňuje správcům zajistit, že klientské počítače mají následující důvěryhodné konfigurace systému BIOS, čipu TPM a spouštěcího softwaru:  

-   Antimalware s raným spuštěním  

-   BitLocker  

-   Zabezpečené spouštění  

-   Integrita kódu  

Podrobnosti najdete v tématu [ověření stavu pro Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### <a name="improvements-to-endpoint-protection-antimalware-settings"></a>Vylepšení Endpoint Protection antimalwarových nastavení  
 1602 přidá do Endpoint Protection antimalwarových zásad pro Windows Defender následující nová nastavení:  

-   Ochrana v reálném čase: zablokuje si potenciálně nežádoucí aplikace při stažení před instalací.  

-   Nastavení prohledávání: kontrolovat namapované síťové jednotky během úplného prohledávání.  

-   Nastavení automatického odesílání ukázkových souborů:  

     Antimalwarový stroj může vyžadovat, aby se Microsoftu odeslaly ukázky souborů k další analýze. Ve výchozím nastavení se před odesláním takových ukázek vždycky dotáže. Správci teď můžou spravovat následující nastavení pro konfiguraci tohoto chování:  

    -   Upřesnit: umožňuje povolit automatické odesílání ukázkových souborů, které Microsoftu pomůže určit, jestli jsou některé zjištěné položky škodlivé.  

    -   Upřesnit: umožní uživatelům změnit nastavení automatického odesílání ukázkových souborů.  

    V části "nastavení vyloučení" antimalwarové zásady služby Endpoint Protection pak existující nastavení **vyloučit soubory a složky** teď umožňuje vyloučit zařízení.  

Podrobnosti najdete v tématu [Vytvoření a nasazení antimalwarových zásad pro Endpoint Protection](../../../protect/deploy-use/endpoint-antimalware-policies.md).  

## <a name="mobile-device-management"></a>Správa mobilních zařízení  

### <a name="ios-activation-lock"></a>Zámek aktivace pro iOS  
 Configuration Manager vám může pomáhat spravovat Zámek aktivace pro iOS, což je funkce aplikace Najít iPhone pro zařízení s iOS 7,1 a novějším. Zámek aktivace se povolí automaticky, když se na zařízení používá aplikace Najít iPhone. Když je tato funkce povolená, musí se zadat Apple ID a heslo uživatele, aby bylo možné:  

-   Vypnout funkci Najít iPhone  

-   Vymaže zařízení.  

-   Znovu aktivujte zařízení.  

Configuration Manager může požádat o stav Zámek aktivace jak na zařízení pod dohledem, tak i na zařízeních, která používají systém iOS 7,1 nebo novější. V případě zařízení pod dohledem Configuration Manager může získat kód pro obejití Zámek aktivace a přímo ho vydat do zařízení.  

### <a name="monitor-terms-and-conditions-deployments"></a>Monitorování nasazení podmínek a ujednání  
 Můžete monitorovat nasazení podmínek a ujednání v konzole Configuration Manager.  

 V seznamu nasazení vyberte nasazení podmínek a ujednání. V oblasti souhrnu se zobrazí následující statistiky:  

-   **Kompatibilní**: uživatelé přijali nejnovější verzi podmínek a ujednání.  

-   **Chyba**  

-   **Nedodržující předpisy**: uživatelé přijali verzi podmínek a ujednání, ale ne nejnovější verzi.  

-   **Neznámé**: uživatelé nikdy nepřijali podmínky a ujednání, včetně těch, kteří nemají zaregistrované zařízení.