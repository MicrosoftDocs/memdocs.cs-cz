---
title: Možnosti ve verzi Technical Preview 1604
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview pro Configuration Manager verze 1604.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 684a5559-9e6e-469b-86ae-e768e9f0c9ac
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1785880af8c7d0d106abfe3eea8ecd390f6ce6b1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074448"
---
# <a name="capabilities-in-technical-preview-1604-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1604 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1604. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview.      Před instalací této verze Technical Preview si Projděte úvodní téma, [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md), abyste se seznámili se základními požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.  

 V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.  

##  <a name="manage-volume-purchased-apps-from-the-windows-store-for-business"></a><a name="BKMK_WindowsVPP"></a>Správa hromadně koupených aplikací z Windows Storu pro firmy  
 [Windows Store pro firmy](https://www.microsoft.com/business-store) je místo, kde můžete najít a zakoupit aplikace pro svou organizaci, a to jednotlivě i na svazku. Když obchod připojíte k Configuration Manager, můžete spravovat hromadně zakoupené aplikace z konzoly Configuration Manager, například:  

-   Seznam zakoupených aplikací můžete synchronizovat s Configuration Manager  

-   Aplikace, které jsou synchronizované, se zobrazí v konzole Configuration Manager a můžete je nasadit stejně jako všechny ostatní aplikace.  

-   Můžete sledovat, kolik licencí je dostupných a kolik se používá v konzole Configuration Manager.  

### <a name="try-it-out"></a>Určitě to udělejte!  

##### <a name="scenario-1-set-up-windows-store-for-business-synchronization"></a>Scénář 1: nastavení synchronizace s Windows Storem pro firmy  

1.  V Azure Active Directory Zaregistrujte Configuration Manager pomocí nástroje pro správu "webová aplikace nebo webové rozhraní API". Tím získáte ID klienta, které budete potřebovat později.  

    1.  V [https://manage.windowsazure.com](https://manage.windowsazure.com)uzlu **služby Active Directory** vyberte svou Azure Active Directory a pak klikněte na **aplikace** > **Přidat**.  

    2.  Klikněte na **Přidat aplikaci, kterou vyvíjí moje organizace**.  

    3.  Zadejte název aplikace, vyberte **Webová aplikace** nebo **webové rozhraní API**a potom klikněte na šipku Další.  

    4.  Zadejte stejnou adresu URL pro **přihlašovací adresu URL** i **identifikátor URI ID aplikace**.  Adresa URL může být libovolná a nemusí se překládat na skutečnou adresu. Můžete například zadat **&lt;https://yourdomain\>/SCCM**.  

    5.  Dokončete průvodce.  

2.  V Azure Active Directory vytvořte klíč klienta pro registrovaný Nástroj pro správu.  

    1.  Zvýrazněte aplikaci, kterou jste právě vytvořili, a klikněte na **Konfigurovat**.  

    2.  V části **klíče**vyberte v seznamu dobu trvání a klikněte na **Uložit**.  Tím se vytvoří nový klíč klienta.  Nevybírejte z této stránky, dokud jste neúspěšně připojili Windows Store pro firmy k Configuration Manager.  

3.  Ve Windows Storu pro firmy nakonfigurujte Configuration Manager jako nástroj pro správu úložiště.  

    1.  Otevřete [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) a přihlaste se, pokud se zobrazí výzva.  

    2.  V případě potřeby přijměte podmínky použití.  

    3.  V části **Nástroje pro správu**klikněte na **Přidat Nástroj pro správu**.  

    4.  V **části Hledat nástroj podle názvu**zadejte název aplikace, kterou jste předtím vytvořili v AAD, a pak klikněte na **Přidat**.  

    5.  Klikněte na tlačítko **aktivovat** vedle aplikace, kterou jste právě naimportovali.  

    6.  V průvodci **Zobrazit offline licencované aplikace** klikněte na **Ano** , pokud chcete umožnit nákup aplikací licencovaných offline.  

4.  Zakupte si aspoň jednu aplikaci z Windows Storu pro firmy.  

5.  V pracovním prostoru **Správa** konzoly Configuration Manager rozbalte položku **Cloud Services**a pak klikněte na možnost **Windows Store pro firmy**.  

6.  Na kartě **Domů** ve skupině **vytvořit** klikněte na **Přidat účet Windows Store pro firmy**.  

7.  Z Azure Active Directory přidejte ID tenanta, ID klienta a klíč klienta a potom průvodce dokončete.  

8.  Až budete hotovi, zobrazí se účet, který jste nakonfigurovali v seznamu **účty Windows Storu pro firmy** v konzole Configuration Manager.  

##### <a name="scenario-2-create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-offline-licensed-app"></a>Scénář 2: vytvoření a nasazení Configuration Manager aplikace z aplikace Windows Store pro firmy s offline licencí  

1.  V pracovním prostoru **softwarová knihovna** konzoly Configuration Manager rozbalte položku **Správa aplikací**a pak klikněte na **informace o licencích pro aplikace ze Storu**.  

2.  Seznam **zakoupených aplikací pro Windows Store pro firmy** zobrazuje seznam aplikací synchronizovaných ze Storu. Zvolte aplikaci, kterou chcete nasadit, a potom na kartě **Domů** ve skupině **vytvořit** klikněte na možnost **vytvořit aplikaci**.  

3.  Vytvoří se Configuration Manager aplikace obsahující aplikaci Windows Store pro firmy. Tuto aplikaci pak můžete nasadit a monitorovat stejně jako jakoukoli jinou aplikaci Configuration Manager.  

##  <a name="improvements-to-microsoft-passport-for-work-management"></a><a name="BKMK_PFW"></a>Vylepšení správy Microsoft Passport for Work  
 Teď můžete nasadit zásady služby Passport for Work na zařízení s Windows 10 připojená k doméně spravovaná klientem Configuration Manager.  

##  <a name="option-for-clients-to-switch-to-a-new-software-update-point"></a><a name="bkmk_switchsup"></a>Možnost, aby klienti přešli na nový bod aktualizace softwaru  
 V 1604 Technical Preview můžete povolit možnost, aby klienti Configuration Manager přepnuli na nový bod aktualizace softwaru, když dojde k problémům s aktivním bodem aktualizace softwaru. Pro tuto možnost musíte mít v primární lokalitě k dispozici více bodů aktualizace softwaru. Tuto možnost povolíte u kolekce zařízení a po povolení této možnosti budou klienti v kolekci hledat jiný bod aktualizace softwaru při příštím skenování, když se klientovi nepodaří úspěšně připojit k aktivnímu bodu aktualizace softwaru. V závislosti na nastavení konfigurace služby WSUS (klasifikace aktualizací, produkty atd.) se při přepnutí na nový bod aktualizace softwaru vygeneruje další síťový provoz. Proto byste měli tuto možnost používat jenom tehdy, když je to nezbytně nutné.  

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>Postup povolení možnosti přepnout body aktualizace softwaru  

1.  V konzole nástroje Configuration Manager přejděte na **Prostředky a kompatibilita > Přehled > Kolekce zařízení**.  

2.  Na kartě **Domů** ve skupině **Kolekce** klikněte na **Klientské oznámení** a poté klikněte na **Přepnout na další bod aktualizace softwaru**.  

> [!NOTE]  
>  Tato možnost je k dispozici pouze na webech s více body aktualizace softwaru.  

##  <a name="client-settings-to-manage-client-cache-settings-and-client-peer-cache"></a><a name="bkmk_peercache"></a>Nastavení klienta pro správu nastavení mezipaměti klienta a sdílené mezipaměti klienta  
 Technical Preview verze 1604 zavádí dvě nová nastavení klienta zařízení, která mají vliv na použití mezipaměti klienta. Oba se dají použít jednotlivě, ale nakonfigurují se na stejný seznam vlastností pro nastavení klienta a kombinaci, která vám pomůžou spravovat nasazení obsahu do klientů ve vzdálených umístěních.  

-   První je **klientská mezipaměť klienta**, integrovaná Configuration Manager řešení pro klienty, aby mohli sdílet obsah s jinými klienty přímo z místní mezipaměti. Aby mohli klienti sdílené mezipaměti sdílet obsah, musí být členy stejné skupiny hranic. Sdílená mezipaměť nenahrazuje použití jiných řešení, jako je BracnchCache, ale funguje i vedle sebe a poskytuje více možností pro rozšíření tradičních řešení pro nasazení obsahu, jako jsou distribuční body.  

     Po nasazení nastavení klienta, které povoluje sdílené mezipaměti do kolekce, mohou členové této kolekce fungovat jako zdroj obsahu rovnocenného pro ostatní klienty v příslušné skupině hranic.  Klient, který se chová jako zdroj obsahu rovnocenného obsahu, odešle seznam dostupného obsahu, který je uložen do mezipaměti do svého bodu správy. Když pak další klient v této skupině hranic požaduje obsah, nabídne se zdroj sdílené mezipaměti jako potenciální zdroj obsahu spolu se všemi distribučními body, které jsou nakonfigurované tak, aby byly rychlé. Klient vybere z tohoto kombinovaného fondu zdrojů obsahu náhodný zdroj obsahu. Klienti budou hledat pouze obsah z distribučního bodu, který je nakonfigurován tak, aby byl pomalý i v případě, že ve skupině hranic nejsou k dispozici žádné rychlé distribuční body nebo zdroje sdílené mezipaměti.  

-   Druhé nové nastavení umožňuje **spravovat velikost mezipaměti** v klientech. Mezipaměť můžete nastavit tak, aby měla maximální velikost v megabajtech a maximální velikost jako procento místa na jednotce klientů.  Klient vynutil nastavení, které se napřed narazí.  

Abyste porozuměli použití sdílené mezipaměti klienta, můžete zobrazit řídicí panel **zdrojů dat klienta** . V konzole nástroje přejdete na **monitorování > stav klienta > zdroje dat klientů**. Tady můžete vybrat časové období, které se má použít na řídicí panel. Pak můžete v zobrazení vybrat skupinu hranic nebo balíček, pro které chcete zobrazit informace. Při prohlížení informací můžete ukazatelem myši na povrchu zobrazit další podrobnosti o různých zdrojích obsahu nebo zásad.  

 K zobrazení shrnutí zdrojů dat klienta pro každou skupinu hranic můžete použít také novou sestavu **zdroje dat klienta – Shrnutí**.   
**Požadavky na použití sdílené mezipaměti:**  

-   Je nutné nakonfigurovat lokalitu s **účtem přístupu k síti** , který má **oprávnění Úplné řízení** ke složce mezipaměti v každém klientovi. Ve výchozím nastavení je to **%windir%\ccmcache**  

-   Klienti můžou přenášet obsah pomocí sdílené mezipaměti jenom v případě, že jsou členy stejné skupiny hranic.  

#### <a name="to-configure-client-peer-cache-client-settings"></a>Konfigurace nastavení klienta sdílené mezipaměti klienta  

1.  Obě nastavení jsou nakonfigurovaná na stejné stránce nastavení klienta. V konzole Configuration Manager klikněte na **správa > nastavení klienta**a pak otevřete objekt nastavení klienta zařízení, který chcete použít. Můžete také změnit výchozí objekt nastavení klienta.  

2.  V seznamu dostupných nastavení vyberte **nastavení mezipaměti klienta**.  

3.  Chcete-li spravovat velikost mezipaměti, nastavte možnost **Konfigurovat velikost mezipaměti klienta** na **hodnotu Ano**. Pak můžete nakonfigurovat maximální velikost mezipaměti pro megabajt a jako procento místa na jednotce klientů.  

4.  Pokud chcete klientům povolit zapojení do sdílené mezipaměti klienta, nastavte **povolit Configuration Manager klienta v úplném operačním systému pro sdílení obsahu** , který se rovná **Ano**. Pak můžete nakonfigurovat porty, které klienti používají, včetně toho, jestli budou používat protokol HTTP nebo HTTPS.  

### <a name="try-it-out"></a>Určitě to udělejte!  
 Zkuste provést následující úkoly a pak použijte informace o zpětné vazbě v horní části tohoto tématu a sdělte nám, jak se pracovalo:  

1.  Upravte nastavení klienta a zadejte novou velikost mezipaměti klienta a potvrďte toto nastavení v klientovi.  

2.  Použití nastavení klienta ke konfiguraci více klientů pro použití sdílené mezipaměti  

3.  Nasaďte obsah do klientů tak, aby někteří nebo většina klientů získali tento obsah z jiného klienta pomocí sdílené mezipaměti.  Zdroj obsahu, který se používá, můžete potvrdit zobrazením nového řídicího panelu.  

    > [!NOTE]  
    >  Chcete-li dokončit tuto úlohu ve verzi Technical Preview a v jednom distribučním bodě, nakonfigurujte distribuční bod tak, aby byl pro síťové umístění všech klientů pomalý. Pak distribuujte obsah do jednoho klienta.  Poté, co klient získá obsah, můžete distribuovat obsah do dalších klientů, kteří by měli najít místní partnerské uzly, které chcete použít jako zdroj obsahu, a teprve potom použít distribuční bod, který je považován za pomalý z umístění klienta.  

##  <a name="support-for-passport-for-work-as-a-ksp"></a><a name="bkmk_passport"></a>Podpora služby Passport for Work jako KSP  
 Configuration Manager umožňuje integraci s Microsoft Passport for Work, což je alternativní metoda pro přihlašování pomocí účtu služby Active Directory nebo Azure Active Directory, která může nahradit hesla, čipové karty a virtuální čipové karty.  
Passport umožňuje používat místo hesla k přihlášení gesto uživatele. Gesto uživatele může být jednoduchý PIN kód, biometrické ověřování jako třeba Windows Hello nebo externí zařízení, jako je třeba čtečka otisků prstů.  

-   Pomocí Configuration Manager můžete řídit, která gesta uživatel může nebo nemůže používat k přihlášení, a ke konfiguraci požadavků na složitost PIN kódu.  

-   Můžete uložit ověřovací certifikáty ve zprostředkovateli úložiště klíčů (KSP) služby Passport for Work.  

Když uživatel vytvoří PIN kód služby Passport, Windows pošle oznámení, které Configuration Manager naslouchá.  Díky tomu mohou Configuration Manager rychle vědět, kteří uživatelé vytvořili PIN kód služby Passport. Configuration Manager potom můžou uživatelům vydat nové certifikáty, pokud se Passport jako poskytovatel úložiště klíčů používá v profilu certifikátu.  

##  <a name="on-premises-device-health-attestation"></a><a name="bkmk_onpremdha"></a>Místní Ověření stavu zařízení  
 Ověření stavu pro zařízení s Windows 10 se teď dá nakonfigurovat tak, aby komunikovala s místní infrastrukturou.  Správci můžou určit, jestli se vytváření sestav provádí prostřednictvím cloudu nebo místních prostředků.  Pokud je pro vytváření sestav Health Attestation vybraný parametr **on-premises** , můžete pro službu zadat identifikátor URI. To umožňuje klientským počítačům bez přístupu k Internetu používat povolení a správu zařízení pomocí ověření stavu.  

#### <a name="enable-health-attestation-for-on-premises-devices"></a>Povolit ověření stavu pro místní zařízení  

1.  V konzole Configuration Manager přejděte na **Správa** > **Přehled** > **nastavení klienta**a pak nastavte použít místní **službu ověření stavu v pořádku** na **Ano**.  

2.  Zadejte **Adresu URL místní služby Ověření stavu** a poté klikněte na **OK**.  

Pokud to chcete vyzkoušet, nakonfigurujte místní službu ověření stavu pomocí nastavení klientského agenta.  

##  <a name="smartlock-setting-for-android-devices"></a><a name="BKMK_Smart"></a>Nastavení inteligentního zámku pro zařízení s Androidem  
 Do položky konfigurace **Android a Samsung KNOX** bylo přidáno nové nastavení, **Povolení inteligentního zámku a dalších agentů** pro správu důvěryhodnosti, které vám umožní řídit funkci inteligentního zámku na kompatibilních zařízeních s Androidem. Tato funkce telefonů, které se někdy říká agenti pro určování důvěryhodnosti, umožňuje zakázat nebo obejít heslo uzamčené obrazovky zařízení, pokud se zařízení nachází v důvěryhodném umístění, třeba pokud je připojené k určitému zařízení Bluetooth nebo když se nachází blízko značky NFC. Pomocí tohoto nastavení můžete koncovým uživatelům zabránit v konfiguraci inteligentního zámku.  
