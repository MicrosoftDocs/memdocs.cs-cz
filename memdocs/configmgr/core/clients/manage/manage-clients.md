---
title: Správa klientů
titleSuffix: Configuration Manager
description: Naučte se spravovat klienty v Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7b9111e3be82424425561e0a664fee955d73ee63
ms.sourcegitcommit: 1e04fcd0d6c43897cf3993f705d8947cc9be2c25
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/02/2020
ms.locfileid: "84270816"
---
# <a name="how-to-manage-clients-in-configuration-manager"></a>Správa klientů v nástroji Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Když se klient Configuration Manager nainstaluje do zařízení a úspěšně se přiřadí k lokalitě, zobrazí se zařízení v pracovním prostoru **prostředky a kompatibilita** v uzlu **zařízení** a v jedné nebo více kolekcích v uzlu **kolekce zařízení** . Vyberte zařízení nebo kolekci a potom spusťte operace správy. Existují však i další způsoby správy klienta, které mohou zahrnovat jiné pracovní prostory v konzole nástroje, nebo úlohy mimo konzolu nástroje.  

> [!NOTE]  
> Pokud nainstalujete klienta Configuration Manager, ale ještě nebyl úspěšně přiřazen k lokalitě nástroje, nemusí se zobrazit v konzole nástroje. Poté, co se klient přiřadí k lokalitě, aktualizuje členství kolekce a pak aktualizuje zobrazení konzoly.  
>
> Zařízení se může v konzole zobrazit i v případě, že není nainstalován klient Configuration Manager. K tomuto chování dochází, pokud lokalita zjistí zařízení, ale klient není nainstalován a přiřazen.
>
> Mobilní zařízení spravovaná pomocí [konektoru systému Exchange Server](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md) nebo místní správy mobilních zařízení ( [MDM](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) ) neinstalují klienta Configuration Manager.  
>
> Chcete-li spravovat zařízení z konzoly nástroje, pomocí sloupce **klient** v uzlu **zařízení** určete, zda je nainstalován klient nástroje.  

## <a name="manage-clients-from-the-devices-node"></a><a name="BKMK_ManagingClients_DevicesNode"></a>Správa klientů z uzlu **zařízení**  

V závislosti na typu zařízení nemusí být některé z těchto možností k dispozici.  

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte uzel **zařízení** .  

2. Vyberte jedno nebo více zařízení a pak na pásu karet vyberte jednu z těchto úloh správy klientů. Můžete také kliknout pravým tlačítkem na zařízení.)  

### <a name="import-user-device-affinity"></a>Importovat spřažení uživatelského zařízení

Nakonfigurujte přidružení uživatelů a zařízení, abyste mohli efektivně nasazovat software uživatelům.  

Další informace najdete v tématu [propojení uživatelů a zařízení pomocí spřažení uživatelských zařízení](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

### <a name="import-computer-information"></a>Importovat informace o počítači

Spusťte **Průvodce importem informací o počítači** pro import informací o novém počítači do databáze Configuration Manager. Můžete importovat více počítačů pomocí souboru nebo zadat informace pro jeden počítač.

### <a name="add-selected-items"></a>Přidat vybrané položky

Poskytuje následující možnosti:

- **Přidat vybrané položky do existující kolekce zařízení**: otevře dialogové okno **Vybrat kolekci** . Vyberte kolekci, do které chcete přidat toto zařízení. Zařízení je součástí této kolekce pomocí **přímého** pravidla členství.  

- **Přidat vybrané položky do nové kolekce zařízení**: otevře **Průvodce vytvořením kolekce zařízení** , kde můžete vytvořit novou kolekci. Vybraná kolekce je zahrnutá v této kolekci pomocí **přímého** pravidla členství.  

Další informace najdete v tématu [vytváření kolekcí](collections/create-collections.md).

### <a name="install-client"></a>Nainstalovat klienta

Otevře **Průvodce instalací klienta**. Tento průvodce používá nabízenou instalaci klienta k instalaci nebo přeinstalaci klienta Configuration Manager na vybraném zařízení.

> [!TIP]  
> Existuje mnoho různých způsobů, jak nainstalovat klienta Configuration Manager. I když Průvodce klientskou nabízenou instalací nabízí z konzoly pohodlnou metodu instalace klienta, tato metoda má mnoho závislostí a není vhodná pro všechna prostředí. Další informace o závislostech najdete v tématu [předpoklady pro nasazení klientů do počítačů se systémem Windows](../deploy/prerequisites-for-deploying-clients-to-windows-computers.md#client-push-installation). Další informace o dalších metodách instalace klientů najdete v tématu [metody instalace klientů](../deploy/plan/client-installation-methods.md).

Další informace najdete v tématu [instalace Configuration Manager klientů pomocí klientské nabízené instalace](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).

### <a name="run-script"></a>Spuštění skriptu

Otevře průvodce **spuštěním skriptu** , ve kterém se spustí skript PowerShellu na vybraném zařízení.

Další informace najdete v tématu [vytváření a spouštění skriptů PowerShellu](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="install-application"></a>Instalovat aplikaci

Nainstalujte aplikaci do zařízení v reálném čase. Tato funkce může přispět k omezení nutnosti samostatné kolekce pro každou aplikaci.

Další informace najdete v tématu [instalace aplikací pro zařízení](../../../apps/deploy-use/install-app-for-device.md).

### <a name="reassign-site"></a>Opětovné přiřazení lokality

Opětovně přiřaďte jednoho nebo více klientů, včetně spravovaných mobilních zařízení, k jiné primární lokalitě v hierarchii. Můžete kdykoli znovu přiřadit klienty nebo vybrat více než jednu, aby bylo možné je znovu přiřadit hromadnému přiřazení.  

### <a name="client-settings---resultant-client-settings"></a>Nastavení klienta – výsledná nastavení klienta

Když nasadíte více nastavení klienta na stejné zařízení, stanovení priorit a kombinace nastavení je složité. Tuto možnost použijte, pokud chcete zobrazit výslednou sadu nastavení klienta nasazených na toto zařízení.

Další informace najdete v tématu [Konfigurace nastavení klienta](../deploy/configure-client-settings.md).

### <a name="start"></a>Spustit

- Spusťte **Průzkumník prostředků** pro zobrazení informací o inventáři hardwaru a softwaru z klienta systému Windows. Další informace najdete v následujících článcích:

  - [Použití Průzkumníka prostředků k zobrazení inventáře hardwaru](inventory/use-resource-explorer-to-view-hardware-inventory.md)

  - [Použití Průzkumníka prostředků k zobrazení inventáře softwaru](inventory/use-resource-explorer-to-view-software-inventory.md)

- Vzdáleně spravovat zařízení pomocí **vzdáleného řízení**, **vzdálené pomoci**nebo **klienta vzdálené plochy**. Další informace najdete v tématu [Postup při vzdálené správě klientského počítače se systémem Windows](remote-control/remotely-administer-a-windows-client-computer.md).

### <a name="approve"></a>Schválení

Pokud klient komunikuje se systémy lokality pomocí protokolu HTTP a certifikátu podepsaného svým držitelem, je nutné tyto klienty schválit, aby je identifikoval jako důvěryhodné počítače. Konfigurace lokality ve výchozím nastavení automaticky schválí klienty ze stejné doménové struktury služby Active Directory, důvěryhodných doménových struktur a připojených Azure Active Directory (Azure AD).<!-- MEMDocs#318 -->. Toto výchozí chování znamená, že nemusíte ručně schvalovat každého klienta. Ručně schvalte počítače v pracovní skupině, kterým důvěřujete, a všechny jiné neschválené počítače, kterým důvěřujete.

> [!IMPORTANT]  
> I když některé funkce správy mohou fungovat pro neschválené klienty, jedná se o nepodporovaný scénář pro Configuration Manager.  

Nemusíte schvalovat klienty, kteří vždy komunikují se systémy lokality pomocí protokolu HTTPS, nebo klienti, kteří používají certifikát PKI při komunikaci se systémy lokality pomocí protokolu HTTP. Tito klienti vytvářejí důvěru pomocí certifikátů PKI.

### <a name="block-or-unblock"></a>Blokovat nebo odblokovat

Zablokuje klienta, kterému již nadále nedůvěřujete. Blokování brání klientovi v přijetí zásad a zabrání systému lokality v komunikaci s klientem.  

> [!IMPORTANT]  
> Blokování klienta zabrání klientovi pouze v komunikaci s Configuration Manager systémy lokality. Nebrání komunikaci s jinými zařízeními. Pokud klient komunikuje se systémy lokality pomocí protokolu HTTP místo protokolu HTTPS, dochází k některým omezením zabezpečení.  

Můžete také odblokovat blokovaného klienta.

Další informace najdete v tématu [Určení možnosti blokování klientů](../deploy/plan/determine-whether-to-block-clients.md).

<!-- Change Category is a hybrid action -->

### <a name="clear-required-pxe-deployments"></a>Vymazat požadovaná nasazení PXE

Požadované nasazení PXE můžete znovu nasadit tak, že zrušíte stav posledního nasazení PXE přiřazeného ke kolekci Configuration Manager nebo počítači. Tato akce resetuje stav tohoto nasazení a znovu nainstaluje nejnovější požadovaná nasazení.

Další informace najdete v tématu [použití technologie PXE k nasazení Windows přes síť](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

### <a name="client-notification"></a>Klientské oznámení

Další informace najdete v tématu [oznámení klienta](client-notification.md#client-notification).

### <a name="endpoint-protection"></a>Funkce Endpoint Protection

Další informace najdete v tématu [oznámení klienta](client-notification.md#endpoint-protection).

### <a name="edit-primary-users"></a>Upravit primární uživatele

Zobrazit uživatele tohoto zařízení za posledních 90 dní nebo zadat primární uživatele tohoto zařízení.

Další informace najdete v tématu [propojení uživatelů a zařízení pomocí spřažení uživatelských zařízení](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

### <a name="wipe-a-mobile-device"></a>Vymazání mobilního zařízení

Můžete vymazat mobilní zařízení, která podporují příkaz vymazání. Tato akce trvale odstraní všechna data v mobilním zařízení, včetně osobních nastavení a osobních údajů. Tato akce obvykle obnoví mobilní zařízení na výchozí hodnoty z výroby. Vymažte mobilní zařízení, pokud již není důvěryhodné. Například pokud dojde ke ztrátě nebo odcizení zařízení.  

> [!TIP]  
> Další informace o tom, jak mobilní zařízení zpracovává příkaz pro vzdálené vymazání, najdete v dokumentaci od výrobce.  

Často se jedná o prodlevu, dokud mobilní zařízení neobdrží příkaz vymazání:  

- Pokud je mobilní zařízení zaregistrované pomocí Configuration Manager, klient obdrží příkaz, když stáhne své zásady klienta.

- Pokud je mobilní zařízení spravováno konektorem systému Exchange Server, obdrží příkaz při synchronizaci se serverem Exchange.  

Pokud chcete monitorovat, kdy zařízení obdrží příkaz vymazání, použijte sloupec **stav vymazání** . Dokud zařízení neodešle potvrzení o vymazání Configuration Manager, můžete zrušit příkaz vymazání.  

### <a name="retire-a-mobile-device"></a>Vyřazení mobilního zařízení

Možnost **vyřadit** je podporovaná jenom na mobilních zařízeních zaregistrovaných pomocí místní správy mobilních zařízení (MDM).  

Další informace najdete v tématu [Chraňte svá data pomocí vzdáleného vymazání, vzdáleného zámku nebo resetování hesla](../../../mdm/deploy-use/wipe-lock-reset-devices.md).

### <a name="change-ownership"></a>Změnit vlastnictví

Pokud zařízení není připojené k doméně a nemá nainstalovaného klienta Configuration Manager, použijte tuto možnost ke změně vlastnictví na **Společnost** nebo **osobní**.  

Tuto hodnotu můžete použít v požadavcích aplikace pro řízení nasazení a pro kontrolu nad tím, kolik inventáře se bude shromažďovat ze zařízení uživatelů.  

Je možné, že budete muset přidat do zobrazení sloupec **vlastník zařízení** tak, že kliknete pravým tlačítkem na záhlaví kteréhokoli sloupce a vyberete ho.

### <a name="delete"></a>Odstranit

> [!WARNING]  
> Neodstraňujte klienta, pokud chcete odinstalovat klienta Configuration Manager nebo jej odebrat z kolekce.  

Akce **Odstranit** ručně odstraní záznam klienta z databáze Configuration Manager. Tuto akci použijte pouze k vyřešení problému. Pokud odstraníte objekt, ale klient je stále nainstalován a komunikuje s lokalitou, funkce zjišťování prezenčního signálu znovu vytvoří záznam klienta. Znovu se zobrazí v konzole Configuration Manager, i když bude ztracena historie klienta a jakékoli předchozí asociace.  
> [!NOTE]  
> Když odstraníte klienta mobilního zařízení, který byl zaregistrován nástrojem Configuration Manager, tato akce také odvolá vydaný certifikát PKI. Tento certifikát je poté zamítnut bodem správy, i když služba IIS nekontroluje seznam odvolaných certifikátů (CRL).
>
> Certifikáty u starších verzí klientů mobilních zařízení nejsou v případě odstranění těchto klientů odvolány.

Chcete-li odinstalovat klienta, přečtěte si téma [odinstalace klienta Configuration Manager](#BKMK_UninstalClient).  

Chcete-li přiřadit klienta k nové primární lokalitě, přečtěte si téma [přiřazení klientů k lokalitě](../deploy/assign-clients-to-a-site.md).

Chcete-li odebrat klienta z kolekce, překonfigurujte vlastnosti kolekce. Další informace najdete v tématu [Správa kolekcí](collections/manage-collections.md).

### <a name="refresh"></a>Aktualizovat

Aktualizujte zobrazení konzoly s nejnovějšími daty v databázi. Například pokud se zařízení zobrazuje v seznamu ze zjišťování, ale nezobrazuje se jako nainstalované. Po instalaci klienta nástroje a zajistěte, aby byl přiřazen k lokalitě, vyberte **aktualizovat**.

### <a name="properties"></a>Vlastnosti

Zobrazit data zjišťování a nasazení cílená pro klienta.

Můžete také nakonfigurovat proměnné, které pořadí úloh použijí k nasazení operačního systému do zařízení. Další informace najdete v [sevytváření proměnných pořadí úkolů pro zařízení a kolekce](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-coll-var).


## <a name="manage-clients-from-the-device-collections-node"></a><a name="BKMK_ManagingClients_DeviceCollectionsNode"></a>Správa klientů z uzlu **kolekce zařízení**

Mnohé z úloh, které jsou k dispozici pro zařízení v uzlu **zařízení** , jsou také k dispozici v kolekcích. Konzola automaticky použije operaci na všechna oprávněná zařízení v kolekci. Tato akce v celé kolekci vytvoří další síťové pakety a zvýší využití procesoru na serveru lokality.  

Před spuštěním úloh na úrovni kolekce zvažte následující otázky. Po spuštění nemůžete úlohu zastavit z konzoly.

- Kolik zařízení je v kolekci?
- Jsou zařízení připojená k síťovým připojením s malou šířkou pásma?
- Jak dlouho je potřeba, aby se tato úloha dokončila pro všechna zařízení?

Další informace najdete v tématu [Správa kolekcí](collections/manage-collections.md).


## <a name="restart-clients"></a>Restartovat klienty

Použijte konzolu Configuration Manager k identifikaci klientů, kteří vyžadují restart. Pak použijte akci klientského oznámení a restartujte ji.

> [!Tip]
> Povolte automatický upgrade klienta, abyste klientům zachovali aktuálnost s menší námahou. Další informace najdete v tématu [o automatickém upgradu klienta](upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate).

Chcete-li identifikovat zařízení, která čekají na restartování, v konzole Configuration Manager klikněte na pracovní prostor **prostředky a kompatibilita** a vyberte uzel **zařízení** . Pak zobrazte stav pro každé zařízení v podokně podrobností v novém sloupci s názvem **čeká na restartování**. Každé zařízení má jednu nebo více z následujících hodnot:

- **Ne**: nečeká se na restartování
- **Configuration Manager**: Tato hodnota pochází z komponenty koordinátora restart klienta (RebootCoordinator. log).
- **Přejmenování souboru**: Tato hodnota pochází z Windows Reporting s probíhající operací přejmenování souboru (HKLM\SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations).
- **Web Windows Update**: Tato hodnota pochází z agenta web Windows Update a vytváření sestav, který čeká na restartování, se vyžaduje pro jednu nebo více aktualizací (HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired).
- **Přidat nebo odebrat funkci**: Tato hodnota pochází z obsluhy založené na komponentách systému Windows vytváření sestav při přidávání nebo odebírání funkcí Windows vyžaduje restart (Servicing\Reboot na základě HKLM\Software\Microsoft\Windows\CurrentVersion\Component).

### <a name="create-the-client-notification-to-restart-a-device"></a>Vytvoření klientského oznámení pro restartování zařízení

1. Vyberte zařízení, které chcete restartovat v rámci kolekce v uzlu **kolekce zařízení** v konzole nástroje.
2. Na pásu karet vyberte možnost **klientské oznámení**a pak vyberte možnost **restartovat**. Otevře se okno s informacemi o restartování. Kliknutím na **OK** potvrďte požadavek na restartování.

Když klient obdrží oznámení, otevře se okno oznámení **centra softwaru** , které uživatele informuje o restartování. Ve výchozím nastavení dojde k restartování po 90 minutách. Čas restartování můžete upravit konfigurací [nastavení klienta](../deploy/configure-client-settings.md). Nastavení pro chování při restartování najdete na kartě [restart počítače](../deploy/about-client-settings.md#computer-restart) výchozího nastavení.


## <a name="configure-the-client-cache"></a><a name="BKMK_ClientCache"></a>Konfigurace mezipaměti klienta

Mezipaměť klienta ukládá do mezipaměti dočasné soubory pro klienty, kteří instalují aplikace a programy. Aktualizace softwaru také používají mezipaměť klienta, ale vždy se pokusí o stažení do mezipaměti bez ohledu na nastavení velikosti. Nakonfigurujte nastavení mezipaměti, například velikost a umístění, při ruční instalaci klienta nástroje, když použijete nabízenou instalaci klienta nebo po instalaci.

Velikost složky mezipaměti můžete zadat pomocí nastavení klienta v konzole Configuration Manager. Další informace najdete v tématu [nastavení mezipaměti klienta](../deploy/about-client-settings.md#client-cache-settings).

Výchozí umístění mezipaměti klienta Configuration Manager je `%windir%\ccmcache` a výchozí místo na disku je 5120 MB.  

> [!IMPORTANT]  
> Nešifrovat složku používanou pro mezipaměť klienta. Configuration Manager nemůže stáhnout obsah do zašifrované složky.  

### <a name="about-the-client-cache"></a>O mezipaměti klienta  

Klient Configuration Manager stáhne obsah pro požadovaný software krátce po přijetí nasazení, ale čeká na jeho spuštění až do naplánovaného času nasazení. V naplánovaném čase klient Configuration Manager zkontroluje, zda je obsah v mezipaměti k dispozici. Pokud je obsah v mezipaměti a jedná se o správnou verzi, klient použije obsah uložený v mezipaměti. Pokud se požadovaná verze změny obsahu nebo pokud klient odstraní obsah, aby uvolnil místo pro jiný balíček, klient stáhne obsah do mezipaměti znovu.  

Pokud se klient pokusí stáhnout obsah pro program nebo aplikaci, která je větší než velikost mezipaměti, nasazení se nezdařilo z důvodu nedostatečné velikosti mezipaměti. Klient generuje stavovou zprávu 10050 pro nedostatečnou velikost mezipaměti. Pokud velikost mezipaměti později zvětšíte, výsledek je následující:  

- Požadovaný program: klient se automaticky znovu nepokouší stáhnout obsah. Znovu nasaďte balíček a program do klienta.  
- Požadovaná aplikace: klient se automaticky pokusí stáhnout obsah při stahování zásad klienta.  

Pokud se klient pokusí stáhnout balíček, který je menší než velikost mezipaměti, ale mezipaměť je plná, všechna *požadovaná* nasazení budou pokračovat až do:

- K dispozici je místo v mezipaměti.
- Doba stahování vypršela.
- Počet opakování dosáhne svého limitu.

Pokud později zvětšíte velikost mezipaměti, klient se pokusí stáhnout balíček znovu během intervalu příštího opakování. Klient se pokusí stáhnout obsah každé čtyři hodiny, dokud nezkusí o 18 časů.  

Obsah uložený v mezipaměti není automaticky odstraněn. Zůstane v mezipaměti alespoň jeden den po použití tohoto obsahu klientem. Pokud nakonfigurujete vlastnosti balíčku s možností zachovat obsah v mezipaměti klienta, klient je automaticky neodstraní. Pokud je místo mezipaměti používáno balíčky, které byly staženy během posledních 24 hodin, a klient musí stáhnout nové balíčky, buď zvětšete velikost mezipaměti, nebo vyberte možnost odstranění trvalého obsahu mezipaměti.  

Pomocí následujících postupů lze nakonfigurovat mezipaměť klienta během ruční instalace klienta, nebo až když je klient nainstalován.  

### <a name="configure-the-cache-during-manual-client-installation"></a>Konfigurace mezipaměti během ruční instalace klienta  

Ze zdrojového umístění instalace spusťte příkaz CCMSetup.exe a zadejte následující požadované vlastnosti oddělené mezerami:  

- DISABLECACHEOPT  

  - SMSCACHEDIR  

  - SMSCACHEFLAGS  

  - SMSCACHESIZE  

    > [!NOTE]
    > Místo SMSCACHESIZE použijte nastavení velikosti mezipaměti dostupné v **nastavení klienta** v konzole Configuration Manager. Další informace najdete v tématu [nastavení mezipaměti klienta](../deploy/about-client-settings.md#client-cache-settings).

Další informace o tom, jak používat tyto vlastnosti příkazového řádku pro CCMSetup. exe, najdete v tématu [informace o vlastnostech instalace klienta](../deploy/about-client-installation-properties.md).

### <a name="configure-the-cache-during-client-push-installation"></a>Konfigurace mezipaměti během nabízené instalace klienta  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** .  

2. Vyberte příslušný web. Na kartě **Domů** na pásu karet ve skupině **Nastavení** vyberte **nastavení instalace klienta**a zvolte možnost **klientská nabízená instalace**. Přepněte na kartu **vlastnosti instalace** .  

3. Zadejte následující vlastnosti oddělené mezerami:  

   - DISABLECACHEOPT  

   - SMSCACHEDIR  

   - SMSCACHEFLAGS  

   - SMSCACHESIZE  

     > [!NOTE]
     > Místo SMSCACHESIZE použijte nastavení velikosti mezipaměti dostupné v **nastavení klienta** v konzole Configuration Manager. Další informace najdete v tématu [nastavení mezipaměti klienta](../deploy/about-client-settings.md#client-cache-settings).

     Další informace o tom, jak používat tyto vlastnosti příkazového řádku pro CCMSetup. exe, najdete v tématu [informace o vlastnostech instalace klienta](../deploy/about-client-installation-properties.md).  

### <a name="configure-the-cache-on-the-client-computer"></a>Konfigurace mezipaměti v klientském počítači  

1. V klientském počítači otevřete ovládací panel **Configuration Manager** .  

2. Přepněte na kartu **cache (mezipaměť** ). Nastavte vlastnosti prostor a umístění. Výchozí umístění je `%windir%\ccmcache` .  

3. Chcete-li odstranit soubory ve složce mezipaměti, vyberte možnost **Odstranit soubory**.  

### <a name="configure-client-cache-size-in-client-settings"></a>Konfigurace velikosti mezipaměti klienta v nastavení klienta

Upravte velikost mezipaměti klienta bez nutnosti přeinstalovat klienta. Použijte nastavení velikosti mezipaměti dostupné v **nastavení klienta** v konzole Configuration Manager. Další informace najdete v tématu [nastavení mezipaměti klienta](../deploy/about-client-settings.md#client-cache-settings).


## <a name="uninstall-the-client"></a><a name="BKMK_UninstalClient"></a>Odinstalace klienta

Z počítače můžete odinstalovat Configuration Manager klientský software pomocí nástroje **CCMSetup. exe** s vlastností **/Uninstall** . Spusťte program CCMSetup. exe v samostatném počítači z příkazového řádku nebo nasaďte balíček pro odinstalaci klienta pro kolekci počítačů.  

> [!NOTE]  
> Klienta Configuration Manager nelze odinstalovat z mobilního zařízení. Pokud je nutné odebrat klienta Configuration Manager z mobilního zařízení, je nutné zařízení vymazat, čímž dojde k odstranění všech dat v mobilním zařízení.  

1. Otevřete příkazový řádek systému Windows jako správce. Změňte složku na umístění, ve kterém je umístěn program CCMSetup. exe, například:`cd %windir%\ccmsetup`

2. Spusťte následující příkaz:`CCMSetup.exe /uninstall`

> [!TIP]  
> Proces odinstalace zobrazí na obrazovce žádné výsledky. Postup pro ověření úspěšného odinstalace klienta najdete v následujícím souboru protokolu:`%windir%\ccmsetup\logs\CCMSetup.log`  
>
> Pokud potřebujete počkat na dokončení procesu odinstalace ještě předtím, než budete dělat něco jiného, spusťte `Wait-Process CCMSetup` v PowerShellu. Tento příkaz může pozastavit skript, dokud proces CCMSetup nedokončí.


## <a name="manage-conflicting-records"></a><a name="BKMK_ConflictingRecords"></a>Správa konfliktních záznamů

Configuration Manager používá hardwarový identifikátor k pokusu o identifikaci klientů, kteří mohou být duplicitní a upozorňuje vás na konfliktní záznamy. Pokud například přeinstalujete počítač, hardwarový identifikátor by byl stejný, ale identifikátor GUID, který používá Configuration Manager, může být změněn.  

Configuration Manager automaticky řeší konflikty pomocí ověřování systému Windows účtu počítače nebo certifikátu PKI z důvěryhodného zdroje. Když Configuration Manager nedokáže vyřešit konflikt duplicitních identifikátorů hardwaru, nastavení hierarchie Určuje chování.

### <a name="change-the-hierarchy-setting-for-managing-conflicting-records"></a>Změna nastavení hierarchie pro správu konfliktních záznamů  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** .

1. Na pásu karet vyberte **Nastavení hierarchie**.

1. Přepněte na kartu **schválení klienta a konfliktní záznamy** a vyberte jednu z následujících možností:

    - **Automaticky vyřešit konfliktní záznamy**
    - **Ruční řešení konfliktních záznamů**

### <a name="manually-resolve-conflicting-records"></a>Ruční řešení konfliktních záznamů  

1. V konzole Configuration Manager otevřete pracovní prostor **monitorování** , rozbalte položku **stav systému**a vyberte uzel **konfliktní záznamy** .  

1. Vyberte jeden nebo více konfliktních záznamů a pak zvolte **konfliktní záznam**.  

1. Vyberte jednu z následujících možností:  

    - **Sloučení**: spojí nově zjištěný záznam s existujícím záznamem klienta.  

    - **Novinka**: vytvořte nový záznam pro konfliktní záznam klienta.  

    - **Block**: vytvoří nový záznam pro konfliktní záznam klienta, ale označí jej jako blokovaný.  


## <a name="manage-duplicate-hardware-identifiers"></a>Správa duplicitních identifikátorů hardwaru

Můžete zadat seznam identifikátorů hardwaru, které Configuration Manager ignorovat pro spouštění pomocí technologie PXE a registraci klienta. Tento seznam pomáhá řešit dva běžné problémy:

1. Mnoho nových zařízení nezahrnuje port připojení k síti Ethernet. Technici používají adaptér USB-to-Ethernet k navázání kabelového připojení pro účely nasazení operačního systému. Tyto adaptéry se často sdílejí z důvodu nákladů a obecné použitelnosti. Lokalita používá adresu MAC tohoto adaptéru k identifikaci zařízení. Proto se adaptér znovu používá bez dalších akcí správce mezi jednotlivými nasazeními. Pokud chcete použít adaptér v tomto scénáři, vylučte jeho adresu MAC.

2. I když by měl být atribut SMBIOS jedinečný, některá speciální hardwarová zařízení mají duplicitní identifikátory. Vylučte tento duplicitní identifikátor a spoléhá se na jedinečnou adresu MAC každého zařízení.

Pomocí následujícího postupu přidejte identifikátory hardwaru pro Configuration Manager ignorovat:

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** .

2. Na kartě **Domů** na pásu karet ve skupině **lokality** klikněte na možnost **Nastavení hierarchie**.

3. Přepněte na kartu **schválení klienta a konfliktní záznamy** . Pokud chcete přidat nové identifikátory hardwaru, vyberte v části **duplicitní identifikátory hardwaru** možnost **Přidat** .

> [!TIP]
> Počínaje verzí 1910 použijte k automatizaci správy duplicitních identifikátorů hardwaru následující rutiny PowerShellu:<!-- 4852819 -->
>
> - New-CMDuplicateHardwareIdGuid
> - Remove-CMDuplicateHardwareIdGuid
> - New-CMDuplicateHardwareIdMacAddress
> - Remove-CMDuplicateHardwareIdMacAddress


## <a name="start-policy-retrieval"></a><a name="BKMK_PolicyRetrieval"></a>Spustit načtení zásad

Klient Configuration Manager stáhne své zásady klienta podle plánu, který nakonfigurujete jako klientské nastavení. Můžete také spustit načítání zásad na vyžádání z klienta. Například pro účely řešení potíží nebo testování.  

- [Klientské oznámení](#bkmk_policy-notify)
- [Ovládací panel klienta](#bkmk_policy-manual)
- [Support Center](#bkmk_policy-support)
- [Skript](#bkmk_policy-script)

### <a name="start-client-policy-retrieval-with-client-notification"></a><a name="bkmk_policy-notify"></a>Spuštění načtení zásad klienta s klientským oznámením  

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte možnost **zařízení**.  

1. Vyberte zařízení, pro které chcete zásady stáhnout. Na kartě **Domů** na pásu karet ve skupině **zařízení** vyberte možnost **klientské oznámení**a pak zvolte možnost **Stáhnout zásady počítače**.  

    > [!NOTE]  
    > Pomocí klientského oznámení můžete také spustit načtení zásad pro všechna zařízení v kolekci.  

### <a name="start-client-policy-retrieval-from-the-configuration-manager-client-control-panel"></a><a name="bkmk_policy-manual"></a>Spuštění načtení zásad klienta z Configuration Manager ovládacích panelů klienta

1. Otevřete ovládací panely **Configuration Manager** v počítači.  

2. Přepněte na kartu **Akce** . výběrem možnosti obnovení **zásad počítače & cyklus vyhodnocení** spusťte zásadu počítače a pak vyberte **Spustit nyní**.  

3. Kliknutím na **tlačítko OK** potvrďte výzvu.  

4. Předchozí kroky opakujte pro všechny další akce. Například **cyklus načítání zásad uživatele & cyklus vyhodnocení** pro nastavení klienta uživatele.  

### <a name="start-client-policy-retrieval-with-support-center"></a><a name="bkmk_policy-support"></a>Spuštění načtení zásad klienta pomocí programu Support Center

Pro vyžádání a zobrazení zásad klienta použijte Support Center. Další informace najdete v tématu [Support Center – reference](../../support/support-center-ui-reference.md#bkmk_support-policy).

### <a name="start-client-policy-retrieval-by-script"></a><a name="bkmk_policy-script"></a>Spuštění načtení zásad klienta pomocí skriptu  

1. Otevřete Editor skriptu, například Poznámkový blok nebo Integrované skriptovací prostředí (ISE) v prostředí Windows PowerShell.  

2. Zkopírujte a vložte následující vzorový kód PowerShellu<!-- SCCMDocs#1591 --> do souboru:  

    ```PowerShell
    $trigger = "{00000000-0000-0000-0000-000000000021}"
    Invoke-WmiMethod -Namespace root\ccm -Class sms_client -Name TriggerSchedule $trigger
    ```  

    > [!TIP]
    > Další informace o ID plánů najdete v tématu [ID zpráv](../../support/send-schedule-tool.md#bkmk_sendschedule-guids).

3. Uložte soubor s příponou. ps1.  

4. Spusťte skript na klientovi.
