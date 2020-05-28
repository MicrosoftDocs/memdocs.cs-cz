---
title: Možnosti ve verzi Technical Preview 1601
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview pro Configuration Manager verze 1601.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aae1cf2f-2c04-4f68-a03a-f4a925433c09
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ed3f53b6e2e9557def20fc459dfcf4641b0e396d
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905831"
---
# <a name="capabilities-in-technical-preview-1601-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1601 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1601. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview.      Před instalací této verze Technical Preview si Projděte úvodní téma, [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md), abyste se seznámili se základními požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.  

 **Známé problémy pro tuto verzi Technical Preview:**  

-   Když spravujete **Možnosti aktualizace klienta** za účelem zvýšení úrovně předprodukčního klienta na produkční, zobrazí se v textu zaškrtávacího políčka verze klienta nula (0) místo skutečného čísla sestavení klienta. Správná verze předprodukčního klienta se zobrazuje na povrchu nad touto možností a je verze klienta povýšená na produkční, když vyberete tuto možnost.  

-   Když aktualizujete na Technical Preview 1601 a zvolíte test klienta Configuration Manager v předprodukční kolekci, balíček klienta pro kolekci se neupgraduje. Tento problém se týká jenom Technical Preview 1601.  

     Pokud chcete tyto problémy vyřešit, proveďte jeden z následujících kroků:  

    -   Spusťte následující skript SQL v databázi primární lokality:  

        ``` SQL
        DECLARE @PilotingPkgID NVARCHAR(8)  

        SELECT @PilotingPkgID = PilotingPackageID FROM ClientDeploymentSettings  

        MERGE INTO PkgServers_G AS T  
        USING (  
            SELECT @PilotingPkgID AS PkgID, NALPath, SiteCode, SiteName, SourceSite, RefreshTrigger, UpdateMask, [Action]  
            FROM PkgServers_G WHERE PkgID IN (SELECT UpgradePackageID FROM ClientDeploymentSettings)  
            ) AS S  
        ON T.PkgID = S.PkgID and T.NALPath = S.NALPath  

        WHEN NOT MATCHED THEN  
            INSERT (PkgID, NALPATH, SiteCode, SiteName, SourceSite, LastRefresh, RefreshTrigger, UpdateMask, [Action])  
            VALUES (S.PkgID, S.NALPath, S.SiteCode, S.SiteName, S.SourceSite, GetUTCDate(), S.RefreshTrigger, S.UpdateMask, S.[Action])  
        ;  

        ```  

    -   Přidejte novou roli systému lokality distribučního bodu k vašemu testovacímu webu. Nový distribuční bod provede upgrade předprodukční kolekce pomocí nového balíčku klienta.  

**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  

##  <a name="improvements-to-microsoft-intune-integration"></a><a name="bkmk_hybrid1"></a>Vylepšení integrace Microsoft Intune  
V 1601 Technical Preview jsme doplnili podporu pro následující funkce:  

### <a name="improvements-to-conditional-access"></a>Vylepšení podmíněného přístupu  

-   **Podpora podmíněného přístupu pro počítače, které jsou spravované pomocí Configuration Manager**  

     Teď můžete nastavit zásady podmíněného přístupu pro počítače spravované pomocí Configuration Manager, které budou vyžadovat, aby počítače byly kompatibilní se zásadami dodržování předpisů, aby mohli přistupovat ke službám Exchange Online a SharePoint Online.  Díky této nové funkci můžete také zaregistrovat počítače se službou Azure AD prostřednictvím zásad dodržování předpisů a monitorovat a vykazovat jejich registraci v Azure AD.  

    > [!NOTE]  
    >  Podmíněný přístup ještě není ve Windows 10 podporovaný.  

    Pro použití této funkce je potřeba splnit následující požadavky:  

    -   Azure Active Directory Premium předplatné a synchronizaci služby ADFS.  

    -   Odběr služby Microsoft Intune. Microsoft Intune předplatné je potřeba nakonfigurovat v konzole Configuration Manager.  

    -   [Předpoklady pro automatickou registraci služby Azure AD](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    Pokud chcete použít tuto možnost, musíte v Configuration Manager vytvořit zásadu dodržování předpisů s konkrétními pravidly, která jsou popsaná níže, a nastavit zásadu podmíněného přístupu v konzole Intune.  Aby bylo zajištěno, že přístup je povolen pouze pro vyhovující počítače, je nutné nastavit možnost požadavky na počítač s Windows na **zařízení musí splňovat předpisy** . Níže jsou uvedené pravidla zásad dodržování předpisů, která platí pro počítače spravované pomocí Configuration Manager.  

    -   **Vyžadovat registraci ve službě Azure Active Directory:** Toto pravidlo zkontroluje, jestli je zařízení uživatele na pracovišti připojené ke službě Azure AD, a pokud ne, zařízení se automaticky zaregistruje ve službě Azure AD. Automatická registrace se podporuje jenom v systému Windows 8.1. Na počítače se systémem Windows 7 nasaďte pro provedení automatické registrace instalační službu MSI. Další informace najdete [tady](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    -   **Všechny požadované aktualizace jsou nainstalované s konečným termínem starším než určitý počet dnů:** Toto pravidlo zkontroluje, jestli má zařízení uživatele všechny požadované aktualizace (zadané v pravidle **požadované automatické aktualizace** ) v rámci konečného termínu a poskytnuté lhůty, a automaticky nainstaluje všechny požadované aktualizace, které čekají na vyřízení.  

    -   **Vyžadovat šifrování jednotky nástrojem BitLocker:** Tato kontrolu vám umožní zjistit, jestli je primární jednotka (například C: \\ ) v zařízení šifrovaná bitlockerem. Pokud šifrování nástrojem Bitlocker není na primární jednotce povolené, zařízení má blokovaný přístup k e-mailu a službě SharePoint Services.  

    -   **Vyžadovat antimalware:** Tato část kontroluje, zda je povolen a spuštěn antimalwarový software (pouze System Center Endpoint Protection nebo Windows Defender).  
         Pokud není povolený, bude přístup k k e-mailu a službě SharePoint Services blokovaný.  

    Koncoví uživatelé, kteří jsou zablokovaný v důsledku nedodržování předpisů, budou zobrazovat informace o dodržování předpisů v centru softwaru a iniciují nové vyhodnocení zásad, když dojde k nápravě problémů s dodržováním předpisů.  

-   **Podmíněný přístup se službou ověření stavu** Nyní můžete omezit přístup k e-mailu a službám 0365 na základě stavu zařízení, jak je uvedeno ve službě Health Attestation.  Zařízení spravovaná pomocí Intune jsou navíc obsažena v sestavách stavu zařízení.  

    Do konzoly nástroje Configuration Manager bylo přidáno nové pravidlo dodržování předpisů, které umožňuje určit, jestli se mají zařízení povolit nebo zablokovat přístup na základě jejich stavu.  Chcete-li vytvořit toto pravidlo, otevřete **Průvodce vytvořením zásad dodržování předpisů**a přidejte nové pravidlo.  Vyberte pro podmínku **službu Health Attestation hlášenou jako stav** a nastavte hodnotu na **true**.  Tím se zajistí, že budou mít přístup k firemním prostředkům jenom zařízení, která jsou hlášená jako v pořádku. Podrobnosti o službě ověření stavu a o tom, jak se v Intune hlásí stav zařízení, najdete v tématu [ověření stavu zařízení](capabilities-in-technical-preview-1512.md#bkmk_devicehealth).  

-   **Nová nastavení zásad dodržování předpisů:** Nová nastavení zásad dodržování předpisů usnadňují vylepšení zabezpečení a ochrany v zařízeních, která se používají pro přístup k firemnímu e-mailu a službě SharePoint:  

    -   **Vyžadovat automatické aktualizace:** Můžete vyžadovat, aby zařízení s Windows 8.1 nebo novějším umožňovala automatickou instalaci aktualizací, a také určit třídu aktualizací, které jsou nainstalovány.  Můžete vybrat možnost: instalovat pouze aktualizace označené jako důležité nebo nainstalovat všechny doporučené aktualizace.  

         Pokud chcete vytvořit pravidlo pro automatické aktualizace, otevřete **Průvodce vytvořením zásad dodržování předpisů**a přidejte nové pravidlo.  Jako podmínku vyberte **minimální klasifikace požadovaných aktualizací** a nastavte hodnotu na jednu z dostupných hodnot: **žádné**, **Doporučené**a **důležité**.  

        -   **Žádné:** Aktualizace se neinstalují automaticky.  

        -   **Doporučené:** Nainstalují se všechny doporučené aktualizace.  

        -   **Důležité informace:** Jsou nainstalovány pouze aktualizace klasifikované jako důležité.  

    -   **Vyžadovat heslo k odemknutí mobilních zařízení:** Pokud je toto nastavení nastaveno na **Ano**, musí koncoví uživatelé zadat heslo, aby mohli získat přístup ke svému zařízení.  

         Pokud chcete vytvořit pravidlo pro heslo k odemknutí mobilních zařízení, otevřete **Průvodce vytvořením zásad dodržování předpisů**a přidejte nové pravidlo. Vyberte **vyžadovat heslo k odemknutí nečinného zařízení** jako podmínky a nastavte hodnotu na **true**.  

    -   **Počet minut nečinnosti před vyžadováním hesla:**  Určuje dobu nečinnosti, než uživatel musí znovu zadat heslo.  

         Chcete-li vytvořit toto pravidlo, otevřete **Průvodce vytvořením zásad dodržování předpisů**a přidejte nové pravidlo. **Vyberte počet minut nečinnosti před vyžadováním hesla** jako podmínku a nastavte hodnotu na jednu z dostupných možností: 1 minuta, 5 minut, 15 minut, 30 minut, 1 hodina.  

-   **Přepsání výchozího pravidla – vždy povoluje zaregistrovaná zařízení s předpisy a kompatibilní s Intune pro přístup k místnímu Exchangi:**  

     Když zaškrtnete tuto možnost, zařízení, která jsou zaregistrovaná v Intune a vyhovují zásadám dodržování předpisů, budou mít povolený přístup k místnímu Exchangi. Toto pravidlo přepíše výchozí pravidlo. to znamená, že i když nastavíte výchozí pravidlo pro karanténu nebo blokování přístupu, zaregistrovaná zařízení splňující předpisy budou mít pořád přístup k místnímu Exchangi.  
     Toto nastavení použijte, pokud chcete, aby zaregistrovaná zařízení splňující předpisy měla vždycky přístup k e-mailu prostřednictvím místního Exchange.  

     Tato podpora je podporovaná na následujících platformách: Windows Phone 8 a novější, iOS 6 a novější. Android 4,0 a novější, Samsung KNOX Standard 4,0 nebo novější.  

     Pokud chcete tuto možnost použít, přejděte na stránku **Obecné** v **Průvodci konfigurací zásad podmíněného přístupu** pro místní Exchange.  

##  <a name="client-online-status"></a><a name="bkmk_clientStatus"></a>Online stav klienta  
Od verze Technical Preview 1601 můžete na první pohled zjistit, jestli je klient online nebo offline v konzole Configuration Manager. Díky aktualizovaným ikonám a sloupcům v seznamech zařízení konzoly můžete posoudit stav klientů ve vašem prostředí a identifikovat problematické oblasti a další problémy, které by mohly vyžadovat vaši pozornost.  

Klient je online, pokud je aktuálně připojen k roli systému lokality bodu správy Configuration Manager. Pokud bod správy přijímá zprávy typu příkazového testu z klienta, je jeho stav online. Pokud Správa neobdrží zprávu po dobu 5 minut, stav klienta se změní na offline.  

### <a name="icons-for-client-status"></a>Ikony stavu klienta  

|||  
|-|-|  
|![ikona online stavu pro klienty](media/online-status-icon.png)|Klient je online.|  
|![ikona offline stavu pro klienty](media/offline-status-icon.png)|Klient je offline.|  
|![ikona neznámého stavu pro klienty](media/unknown-status-icon.png)|Stav klienta není známý.|  

### <a name="prerequisites"></a>Požadavky  
 Online stav klienta nemá žádné požadavky. Můžete ji začít používat hned po instalaci Configuration Manager Technical Preview 1601.  

### <a name="limitations"></a>Omezení  
 Online stav klienta je k dispozici pouze pro počítače se systémem Windows s nainstalovaným klientem Configuration Manager. Online stav klienta není podporován pro počítače Mac, počítače se systémem Linux nebo UNIX ani pro zařízení spravovaná pomocí \- místní správy mobilních zařízení.  

### <a name="to-view-client-online-status"></a>Zobrazení online stavu klienta  

1. V konzole Configuration Manager, přečtěte si **Přehled prostředků a dodržování předpisů > > zařízení**.  

2. Klikněte pravým tlačítkem na záhlaví sloupce a potom klikněte na jedno z polí online stav klienta a přidejte ho do zobrazení zařízení. Pole jsou  

   -   **Online stav zařízení** udává, jestli je klient aktuálně online nebo offline.  

   -   **Poslední online čas** indikuje, kdy se online stav klienta změnil z offline na online.  

   -   **Poslední čas v režimu offline** udává, kdy se stav změní z online na offline.  

   Chcete-li zobrazit nedávné změny stavu klienta, aktualizujte konzolu.  

##  <a name="improvements-to-application-management"></a><a name="bkmk_appmgmt1601"></a>Vylepšení správy aplikací  
 V 1601 Technical Preview jsme přidali podporu pro následující funkce:  

### <a name="manage-volume-purchased-apps-for-ios-devices"></a>Správa hromadně koupených aplikací pro zařízení s iOS  
 Některé App Story umožňují pro aplikace, které chcete spouštět ve vaší společnosti, nakoupit víc licencí. Můžete tak snížit administrativní režii při sledování několika kopií koupených aplikací.  

 Configuration Manager teď vám pomůže spravovat aplikace, které jste koupili prostřednictvím takového programu, importováním licenčních informací z App Storu a sledováním, kolik licencí jste už použili.  


### <a name="ios---app-configuration-for-applicationsbr-hybrid"></a>iOS – konfigurace aplikací pro aplikace<br />Hybridní  
 Některé aplikace pro iOS podporují předběžnou konfiguraci nastavení, jako je třeba server nebo databáze, ke kterým by se aplikace měla připojit. Configuration Manager teď podporuje nasazení zásad konfigurace aplikací do zařízení, které uživateli umožňuje aplikaci používat hned, aniž by museli tyto informace znát. Vývojáři musí tuto funkci povolit ve svých aplikacích.  

 Omezený počet veřejně vydaných aplikací, které aktuálně podporují předběžnou konfiguraci nastavení; můžete mít také interní vyvíjené obchodní aplikace, které je podporují.  

#### <a name="prerequisites-for-this-scenario"></a>Předpoklady pro tento scénář  

-   Pro Configuration Manager je nutné přidat předplatné Microsoft Intune.  

-   Do předplatného Intune musíte přidat platný certifikát Apple APNs.  

-   Musíte mít nasazenou aplikaci pro iOS, která podporuje konfiguraci aplikace.  

#### <a name="try-it-out"></a>Určitě to udělejte!  
 Po splnění výše uvedených požadavků musíte vytvořit aplikaci Configuration Manager, která používá typ nasazení iOS. Aplikace, kterou použijete, musí podporovat konfiguraci aplikace. Informace o konkrétních položkách (páry název/hodnota) najdete v dokumentaci dodavatele aplikace, kterou můžete nakonfigurovat.  

 Pak přidružíte zásady konfigurace aplikací k typu nasazení iOS během nasazování aplikace. Zásadu můžete nasadit taky z uzlu **zásady konfigurace aplikace** , která je zacílená na existující aplikaci a kolekci.  

 Zkuste provést následující úkoly a pak použijte informace o zpětné vazbě v horní části tohoto tématu a sdělte nám, jak se pracovali:  

-   Pokud máte aplikaci pro iOS, která podporuje konfiguraci aplikací, přečtěte si v dokumentaci dodavatele aplikace, kde najdete dvojice název a hodnota, které musíte zadat pro konfiguraci aplikace.  

-   Spusťte průvodce **vytvořením zásad konfigurace aplikace** . Na stránce **zásady pro iOS** v průvodci zkuste přidat dvojice název a hodnota, které jste našli v dokumentaci dodavatele aplikace, nebo můžete importovat soubor XML, který obsahuje požadované hodnoty.  

-   V průvodci **nasazením softwaru** na stránce **zásady konfigurace aplikací** přidružte zásadu konfigurace aplikace, kterou jste vytvořili s kompatibilním typem nasazení, z aplikace.  

##  <a name="improvements-to-compliance-settings"></a><a name="bkmk_compliance1601"></a>Vylepšení nastavení dodržování předpisů  
 V 1601 Technical Preview jsme přidali podporu pro následující funkce:  

### <a name="microsoft-edge-browser-settings"></a>Nastavení prohlížeče Microsoft Edge  
 Do **Windows 8.1 a položky konfigurace Windows 10** se přidalo nové nastavení prohlížeče Microsoft Edge (nastavení platí jenom pro zařízení s Windows 10).  

 Chcete-li zobrazit nová nastavení, vyberte možnost **Microsoft Edge** na stránce **nastavení zařízení** položky konfigurace v průvodci **vytvořením položky konfigurace** .  

 Další informace najdete v tématu [Vytvoření položek konfigurace pro Windows 8.1 a zařízení s Windows 10 spravovaná bez klienta Configuration Manager](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="compliance-settings-for-windows-10-team-devices"></a>Nastavení dodržování předpisů pro zařízení s Windows 10 Team  
 Pomocí těchto nových nastavení dodržování předpisů můžete nakonfigurovat zařízení s Windows 10 Team, například Surface Hub zařízení.  

 Pokud chcete nová nastavení zobrazit, vyberte **Windows 10 Team** na stránce **nastavení zařízení** položky konfigurace v průvodci **vytvořením položky konfigurace** .  

 Další informace najdete v tématu [Vytvoření položek konfigurace pro Windows 8.1 a zařízení s Windows 10 spravovaná bez klienta Configuration Manager](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="android---kiosk-mode-for-samsung-knox-standardbr-hybrid"></a>Android – celoobrazovkový režim pro Samsung KNOX Standard<br />Hybridní  
 Celoobrazovkový režim umožňuje uzamknout zařízení a povolit fungování jenom některých funkcí. Můžete třeba povolit, aby v zařízení běžela jenom jedna vámi určená spravovaná aplikace, nebo můžete zakázat tlačítka hlasitosti na zařízení. Tato nastavení se dají používat pro ukázkový model zařízení nebo zařízení, které může provádět jenom jednu funkci, jako je třeba zařízení POS. Tato nastavení nejsou k dispozici pro zařízení Samsung KNOX standard v položkách konfigurace **Windows 8.1 a Windows 10** (nastavení platí jenom pro zařízení s Windows 10).  

 Pokud chcete nová nastavení zobrazit, vyberte možnost **celoobrazovkový režim – Samsung KNOX** na stránce **nastavení zařízení** položky konfigurace v průvodci **vytvořením položky konfigurace** .  

 Další informace najdete v tématu [Vytvoření položek konfigurace pro Windows 8.1 a zařízení s Windows 10 spravovaná bez klienta Configuration Manager](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  
