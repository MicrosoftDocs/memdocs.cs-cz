---
title: Možnosti ve verzi Technical Preview 1610
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview pro Configuration Manager verze 1610.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: cee161747d5c0b462836b7c3a44e1460173b124c
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905664"
---
# <a name="capabilities-in-technical-preview-1610-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1610 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*



V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1610. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview.      Před instalací této verze Technical Preview si Projděte úvodní téma, [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md), abyste se seznámili se základními požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.    


**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  
## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrovat podle velikosti obsahu v pravidlech automatického nasazení
Nyní můžete vyfiltrovat velikost obsahu pro aktualizace softwaru v pravidlech automatického nasazení. Můžete například nastavit filtr **Velikost obsahu (KB)** na **< 2048** , aby bylo možné stahovat pouze aktualizace softwaru, které jsou menší než 2 MB. Použití tohoto filtru zabraňuje automatickému stahování velkých aktualizací softwaru, aby byla lépe podporovaná zjednodušená Údržba Windows, když je omezená šířka pásma sítě. Podrobnosti najdete v tématu [Configuration Manager a zjednodušená Údržba Windows v operačních systémech nižší úrovně](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configuration-manager-and-simplified-windows-servicing-on-down/ba-p/274056).

#### <a name="to-configure-the-content-size-field"></a>Konfigurace pole velikost obsahu
Pokud chcete nakonfigurovat pole **Velikost obsahu (KB)** , na stránce **aktualizace softwaru** v Průvodci vytvořením pravidla automatického nasazení, když vytvoříte pravidlo automatického nasazení, nebo přejít na kartu **aktualizace softwaru** ve vlastnostech pro existující pravidlo automatického nasazení.

![Pole velikost obsahu](media/contentsizefield.png)

## <a name="improved-functionality-for-required-software-dialogs"></a>Vylepšené funkce pro požadované softwarové dialogy
Když uživatel obdrží požadovaný software, z nastavení připomenout **a připomenout:** může vybrat z následujícího rozevíracího seznamu hodnot:
- Později: Určuje, zda jsou oznámení naplánována na základě nastavení oznámení nakonfigurovaného v nastavení agenta klienta.
- Pevná doba: Určuje, zda bude naplánováno zobrazení oznámení po zvoleném čase. Pokud uživatel například vybere 30 minut, oznámení se znovu zobrazí za 30 minut.

![Stránka Počítačový agent v nastavení agenta klienta](media/computeragentsettings.png)

Maximální doba odložení je vždy založena na hodnotách oznámení nakonfigurovaných v nastaveních klientského agenta při každé časové ose nasazení. Pokud je například **konečný termín nasazení delší než 24 hodin, nastavení připomenout uživatele** na stránce Počítačový agent je nakonfigurované na 10 hodin a je více než 24 hodin před konečným termínem při spuštění dialogového okna, uživateli se zobrazí sada možností odložení až po dobu 10 hodin. V rámci blížící se k konečnému termínu se v dialogovém okně zobrazí méně možností, které jsou konzistentní s příslušnými nastaveními klientského agenta pro každou součást časové osy nasazení.

V případě nasazení s vysokým rizikem, jako je například pořadí úkolů, které nasazuje operační systém, se nyní projeví oznámení koncovým uživatelům. Místo dočasného oznámení na hlavním panelu se pokaždé, když se uživateli oznámí, že se vyžaduje údržba nejdůležitějšího softwaru, v počítači uživatele se zobrazí dialogové okno, například následující:

![Požadovaný softwarový dialog](media/requiredsoftwaredialog.png)


Další informace najdete tady:
- [Nastavení pro správu nasazení s vysokým rizikem](../servers/manage/settings-to-manage-high-risk-deployments.md)
- [Postup konfigurace nastavení klienta](../clients/deploy/configure-client-settings.md)

## <a name="deny-previously-approved-application-requests"></a>Odepřít dříve schválené žádosti o aplikace

Jako správce můžete nyní odepřít dříve schválenou žádost o aplikaci. Po odepření nainstalujte tuto aplikaci později, aby ji uživatelé museli znovu odeslat. Při odepření nedojde k odinstalaci aplikace. místo toho vynutí znovu schválení všech nových žádostí o tuto aplikaci od tohoto uživatele. V minulosti byl požadavek na aplikaci k dispozici pouze pro žádosti aplikace, které nebyly schváleny.

#### <a name="try-it-out"></a>Vyzkoušejte si to.
Zamítnutí žádosti schválené pro aplikaci:

1. V konzole Configuration Manager [vytvořte a nasaďte aplikaci](../../apps/deploy-use/create-applications.md) , která vyžaduje schválení.
2. V klientském počítači otevřete Centrum softwaru a odešlete žádost o aplikaci.
3. V konzole Configuration Manager schvalte žádost o aplikaci.
4. Zamítnout schválenou žádost o aplikaci: v konzole Configuration Manager přejděte na **softwarová knihovna**  >  **Přehled**  >  **Application Management**  >  **žádosti o schválení** správy aplikací a vyberte žádost o aplikaci, kterou chcete odepřít.  Na pásu karet klikněte na **Odepřít**.

## <a name="exclude-clients-from-automatic-upgrade"></a>Vyloučit klienty z automatického upgradu
Technical Preview 1610 zavádí nové nastavení, které můžete použít k vyloučení kolekce klientů z automatické instalace aktualizovaných verzí klientů.  To platí pro automatický upgrade i pro jiné metody, jako je upgrade na základě aktualizace softwaru, přihlašovací skripty a zásady skupiny. Tato možnost se dá použít pro kolekci počítačů, které při upgradu klienta vyžadují větší péči. Klient, který je ve vyloučené kolekci, ignoruje požadavky na instalaci aktualizovaného klientského softwaru.

### <a name="configure-exclusion-from-automatic-upgrade"></a>Konfigurace vyloučení z automatického upgradu
Konfigurace vyloučení automatických upgrade:
1. V konzole Configuration Manager otevřete **Nastavení hierarchie** v části **Správa > Konfigurace lokality > lokality**a pak vyberte kartu **upgrade klienta** .
2. Zaškrtněte políčko pro **vyloučení zadaných klientů z upgradu**a potom pro **kolekci vyloučení**vyberte kolekci, kterou chcete vyloučit. Pro vyloučení můžete vybrat jenom jednu kolekci.
3. Kliknutím na tlačítko **OK** zavřete a uložte konfiguraci. Po aktualizaci zásad klienta již klienti ve vyloučené kolekci nebudou automaticky instalovat aktualizace klientského softwaru.

   ![Nastavení pro automatické vyloučení upgradu](media/automatic_upgrade_exclusion.png)

> [!NOTE]
> I když uživatelské rozhraní uvádí, že klienti nebudou upgradováni pomocí žádné metody, existují dvě metody, které můžete použít k přepsání těchto nastavení. K přepsání této konfigurace můžete použít nabízenou instalaci klienta a ruční instalaci klienta. Další podrobnosti najdete v následující části.

### <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>Postup upgradu klienta, který je ve vyloučené kolekci
Pokud je kolekce nakonfigurovaná tak, aby se vyloučila, členové této kolekce můžou mít jenom klientský software upgradovaný jednou ze dvou metod, které přepisují vyloučení:
- **Klientská nabízená instalace** – klientská nabízená instalace můžete použít k upgradu klienta, který je ve vyloučené kolekci. Tato možnost je povolená, protože je považována za záměr správce a umožňuje upgradovat klienty bez odebrání celé kolekce z vyloučení.       
- **Ruční instalace klienta** – klienty, kteří jsou ve vyloučené kolekci, můžete ručně upgradovat, když použijete následující přepínač příkazového řádku s CCMSetup: ***/ignoreskipupgrade*** .

  Pokud se pokusíte ručně upgradovat klienta, který je členem vyloučené kolekce, a tento přepínač Nepoužívat, klient nebude instalovat nový klientský software. Další informace najdete v tématu [Ruční instalace klientů Configuration Manager](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual).

Další informace o metodách instalace klientů najdete v tématu [postup nasazení klientů do počítačů se systémem Windows](../clients/deploy/deploy-clients-to-windows-computers.md).

## <a name="windows-defender-configuration-settings"></a>Konfigurační nastavení Windows Defenderu

Teď můžete nakonfigurovat nastavení klienta Windows Defenderu na počítačích s Windows 10 zaregistrovaných v Intune pomocí položek konfigurace v konzole Configuration Manager.

Konkrétně můžete nakonfigurovat následující nastavení programu Windows Defender:
- Povolit monitorování v reálném čase
- Povolit monitorování chování
- Povolit systém kontroly sítě
- Kontrolovat všechny stahované soubory
- Povolit kontrolu skriptů
- Monitorovat aktivitu souborů a programů
  - Sledované soubory
- Kolik dnů sledovat rozpoznaný malware
- Umožnit přístup k uživatelskému rozhraní klienta
- Naplánovat úplnou kontrolu
  - Naplánovaný den
  - Naplánovaný čas
- Naplánovat každodenní rychlou kontrolu
  - Naplánovaný čas
- Omezit využití CPU% během kontroly prohledávání souborů archivu
- Kontrolovat e-mailové zprávy
- Kontrolovat vyměnitelné jednotky
- Kontrolovat namapované jednotky
- Kontrolovat soubory otevřené z NET shares
- Interval aktualizace signatur
- Povolit cloudovou ochranu
- Vyzvat uživatele k zadání ukázek
- Detekce potenciálně nežádoucích aplikací
- Vyloučené soubory/složky
- Vyloučené přípony souborů
- Vyloučené procesy

> [!NOTE]
> Tato nastavení se dají nakonfigurovat jenom na klientských počítačích s Windows 10 listopad Update (1511) a novějším.

### <a name="try-it-out"></a>Určitě to udělejte!

1. V konzole Configuration Manager, přejít na **prostředky a kompatibilita**  >  **Přehled**  >  **Nastavení dodržování předpisů**  >  **položky konfigurace položky**a vytvořte novou **položku konfigurace**.
2. Zadejte název a potom v části **nastavení pro zařízení spravovaná bez Configuration Manager klienta** vyberte **Windows 8.1 a Windows 10** a klikněte na **Další**.
3. Zajistěte, aby na stránce **podporované platformy** byly vybrány **všechny systémy windows 10 (64 bitů)** a **všechny systémy Windows 10 (32-bit)** , a poté klikněte na tlačítko **Další**.
4. Vyberte skupinu nastavení **programu Windows Defender** a pak klikněte na **Další**.
5. Na této stránce nakonfigurujte požadovaná nastavení a pak klikněte na **Další**.
6. Dokončete průvodce.
7. Přidejte tuto položku konfigurace do standardních hodnot konfigurace a nasaďte tyto standardní hodnoty do počítačů se systémem Windows 10 listopad Update (1511) nebo vyšší.

> [!NOTE]
> Nezapomeňte zaškrtnout políčko **napravit nastavení nesplňující požadavky** při nasazování standardních hodnot konfigurace.

## <a name="request-policy-sync-from-administrator-console"></a>Žádost o synchronizaci zásad z konzoly správce

Teď si můžete vyžádat synchronizaci zásad pro mobilní zařízení z konzoly Configuration Manager, abyste nemuseli žádat o synchronizaci přímo ze samotného zařízení. Informace o stavu žádosti o synchronizaci jsou k dispozici jako nový sloupec v zobrazeních zařízení nazvaný **stav vzdálené synchronizace**. Stav se také zobrazí v dialogovém okně **vlastnosti** pro každé mobilní zařízení v části **data zjišťování** .

### <a name="try-it-out"></a>Určitě to udělejte!

1. V konzole Configuration Manager otevřete přehled **assetů a dodržování předpisů**  >  **Overview** > zařízení.
2. V nabídce **Akce vzdáleného zařízení** vyberte **Odeslat žádost o synchronizaci**.

Synchronizace může trvat pět až deset minut. Všechny změny v zásadách se synchronizují do zařízení. Stav žádosti o synchronizaci můžete sledovat ve sloupci **stav vzdálené synchronizace** v zobrazení **zařízení** nebo v dialogovém okně **vlastnosti** zařízení.

## <a name="additional-security-role-support"></a>Podpora dalších rolí zabezpečení

Kromě úplného správce má teď následující předdefinované role zabezpečení úplný přístup k položkám v uzlu **všechna zařízení ve vlastnictví firmy** , včetně předem **deklarovaných zařízení**, **profilů zápisu iOS**a **profilů zápisu Windows**:
- **Správce inventáře**
- **Správce přístupu k prostředkům společnosti**

Přístup k rolím **analytika** , který je jen pro čtení, je k těmto oblastem konzoly Configuration Manager stále udělen.

## <a name="conditional-access-for-windows-10-vpn-profiles"></a>Podmíněný přístup pro profily sítě VPN s Windows 10

Teď můžete vyžadovat, aby zařízení s Windows 10 zaregistrovaná v Azure Active Directory splňovala předpisy pro přístup k síti VPN přes profily sítě VPN s Windows 10 vytvořená v konzole Configuration Manager. To je možné prostřednictvím zaškrtávacího políčka nový **Povolit podmíněný přístup pro toto připojení k síti VPN** na stránce **metoda ověřování** v Průvodci profilem sítě VPN a vlastností profilu sítě VPN pro profily sítě VPN s Windows 10. Pokud povolíte podmíněný přístup pro profil, můžete také zadat samostatný certifikát pro ověřování pomocí jednotného přihlašování.

## <a name="see-also"></a>Viz také
[Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md)
