---
title: Přidání a přiřazení spravovaných aplikací Google Play k zařízením s Androidem Enterprise
titleSuffix: Microsoft Intune
description: Naučte se synchronizovat a přiřadit aplikace zařízením s Androidem Enterprise ze spravovaného Google Play Storu.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2f6c06bf-e29a-4715-937b-1d2c7cf663d4
ms.reviewer: chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1b9cd6d0292c07b2f1a987efba6d1ad9f8d81d99
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989562"
---
# <a name="add-managed-google-play-apps-to-android-enterprise-devices-with-intune"></a>Přidání spravovaných aplikací Google Play do zařízení s Androidem Enterprise pomocí Intune

Managed Google Play je podniková aplikace v obchodě Google a výhradně zdroj aplikací pro Android Enterprise. Intune můžete použít k orchestraci nasazení aplikací prostřednictvím spravovaných Google Play pro jakýkoli scénář Androidu Enterprise (včetně pracovního profilu, vyhrazeného a plně spravovaného zápisu). Způsob přidávání spravovaných aplikací Google Play do Intune se liší od způsobu, jakým se aplikace pro Android přidávají pro jiné než Android Enterprise. Aplikace pro Store, obchodní aplikace a webové aplikace se schvalují nebo přidají do spravovaných Google Play a pak se synchronizují do Intune tak, aby se zobrazovaly v seznamu klientských aplikací. Jakmile se zobrazí v seznamu seznam klientských aplikací, můžete spravovat přiřazení jakékoli spravované Google Play aplikace stejně jako jakoukoli jinou aplikaci.

Abychom vám usnadnili konfiguraci a používání správy Android Enterprise managementu, po připojení vašeho tenanta Intune ke spravovaným Google Play Intune do konzoly pro správu Intune automaticky přidá čtyři běžné aplikace související s podnikovým prostředím Android. Tyto čtyři aplikace jsou následující:

- **[Microsoft Intune](https://play.google.com/store/apps/details?id=com.microsoft.intune)** – používá se pro plně spravované scénáře pro Android Enterprise. Tato aplikace se automaticky nainstaluje do plně spravovaných zařízení během procesu registrace zařízení.
- **[Microsoft Authenticator](https://play.google.com/store/apps/details?id=com.azure.authenticator)** – vám pomůže se přihlašovat k vašim účtům, pokud použijete dvojúrovňové ověřování. Tato aplikace se automaticky nainstaluje do plně spravovaných zařízení během procesu registrace zařízení.
- **[Portál společnosti Intune](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal)** – používá se pro scénáře zásad ochrany aplikací (App) a Android Enterprise Work Profile. Tato aplikace se automaticky nainstaluje do plně spravovaných zařízení během procesu registrace zařízení.
- **[Spravovaná Domovská obrazovka](https://play.google.com/store/apps/details?id=com.microsoft.launcher.enterprise)** – používá se pro veřejné terminály s více aplikacemi pro Android Enterprise. Správci IT by měli vytvořit přiřazení pro instalaci této aplikace na vyhrazená zařízení, která se budou používat ve scénářích veřejného terminálu s více aplikacemi.

>[!NOTE]
>Když koncový uživatel zaregistruje svoje zařízení s plnou správou pro Android Enterprise, Portál společnosti Intune aplikace se automaticky nainstaluje a ikona aplikace může být viditelná pro koncového uživatele. Pokud se koncový uživatel pokusí spustit aplikaci Portál společnosti Intune, koncový uživatel se přesměruje do aplikace Microsoft Intune a ikona Portál společnosti aplikace bude následně skrytá.

## <a name="before-you-start"></a>Než začnete
- Ujistěte se, že jste klienta Intune připojili ke spravovaným Google Play.  Další informace najdete v tématu [připojení účtu Intune ke spravovanému účtu Google Play](../enrollment/connect-intune-android-enterprise.md).
- Pokud máte v úmyslu registrovat zařízení pracovního profilu, ujistěte se, že jste nakonfigurovali pracovní profily Intune a Android pro společné fungování v rámci úlohy **registrace zařízení** Azure Portal. Další informace najdete v tématu [Registrace zařízení s Androidem](../enrollment/android-work-profile-enroll.md).

>[!NOTE]
>Při práci s Microsoft Intune doporučujeme používat prohlížeč Microsoft Edge nebo Google Chrome.

## <a name="managed-google-play-app-types"></a>Spravované typy aplikací Google Play
Existují tři typy aplikací, které jsou k dispozici se spravovanými Google Play:

- **Spravované Google Play ukládají** aplikace veřejné pro aplikace, které jsou všeobecně dostupné v obchod Play. Spravujte tyto aplikace v Intune tak, že přejdete na aplikace, které chcete spravovat, schválíte je a pak je synchronizujete do Intune.
- **Spravovaná Google Play soukromá aplikace** – jedná se o obchodní aplikace publikované do spravovaných Google Play správci Intune.  Tyto aplikace jsou soukromé a jsou k dispozici pouze pro vašeho tenanta Intune. To je způsob, jakým se spravují a nasazují obchodní aplikace se spravovanými Google Play a Androidem Enterprise.
- **Spravované Google Play webový odkaz** – webové odkazy s ikonami definovanými správcem IT, které se nasazují na zařízení s Androidem Enterprise. Zobrazují se na zařízeních v seznamu aplikací v zařízení stejně jako běžné aplikace.

## <a name="managed-google-play-store-apps"></a>Spravované aplikace Google Play Storu
Existují dva způsoby procházení a schvalování spravovaných aplikací pro Google Play Store pomocí Intune:

1. Přímo v konzole Intune – procházení a schvalování aplikací ze Storu v zobrazení hostovaném v Intune. Otevře se přímo v konzole Intune a nevyžaduje opětovné ověření pomocí jiného účtu.
1. V konzole spravovaného Google Play – můžete volitelně otevřít konzolu spravované Google Play přímo a schválit aplikace. Další informace najdete v tématu [synchronizace spravované aplikace Google Play s Intune](apps-add-android-for-work.md#sync-a-managed-google-play-app-with-intune) .  K tomu je potřeba samostatné přihlášení pomocí účtu, který jste použili k připojení tenanta Intune ke spravovaným Google Play.

### <a name="add-a-managed-google-play-store-app-directly-in-the-intune-console"></a>Přidání spravované aplikace Google Play Storu přímo do konzoly Intune

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace**  >  **všechny aplikace**  >  **Přidat**.
3. V podokně **Vybrat typ aplikace** v části dostupné typy **aplikací pro Store** vyberte **Managed Google Play App**.
4. Klikněte na **Vybrat**. Zobrazí se **spravované Google Play** App Store.

    > [!NOTE]
    > Aby bylo možné procházet spravované aplikace Google Play Storu, musí být váš účet tenanta Intune připojený k vašemu účtu Android Enterprise. Další informace najdete v tématu [připojení účtu Intune ke spravovanému účtu Google Play](../enrollment/connect-intune-android-enterprise.md).

5. Výběrem aplikace zobrazíte podrobnosti o aplikaci.
6. Na stránce, na které se aplikace zobrazuje, klikněte na **schválit**. Otevře se okno s žádostí, abyste této aplikaci udělili oprávnění k provádění různých operací.
7. Pokud chcete přijmout oprávnění aplikace a pokračovat, vyberte **Schválit**.
8. Vyberte **zachovat schválené, když aplikace požaduje nová oprávnění** na kartě **Nastavení schvalování** a pak klikněte na **Hotovo**. 

    > [!IMPORTANT]
    > Pokud tuto možnost nevyberete, budete muset ručně schválit všechna nová oprávnění, pokud vývojář aplikace publikuje aktualizaci. To způsobí, že se instalace a aktualizace aplikace zastaví, dokud nebudou oprávnění schválena. Z tohoto důvodu se doporučuje vybrat možnost pro automatické schválení nových oprávnění. 

9. Klikněte na **Vybrat** a vyberte aplikaci.
10. V horní části okna klikněte na **synchronizovat** , aby se aplikace synchronizoval se službou Managed Google Play Service.
11. Kliknutím na **aktualizovat** můžete seznam aplikací aktualizovat a zobrazit nově přidanou aplikaci.

### <a name="add-a-managed-google-play-store-app-in-the-managed-google-play-console-alternative"></a>Přidání spravované aplikace Google Play Storu v konzole spravovaného Google Play (alternativně)
Pokud dáváte přednost synchronizaci spravované aplikace Google Play s Intune místo přímého přidávání pomocí Intune, použijte následující postup.

> [!IMPORTANT]
> Níže uvedené informace jsou alternativní metodou přidání spravované aplikace Google Play pomocí Intune, jak je popsáno výše.

1. Přejděte na [spravovaný obchod Google Play](https://play.google.com/work). Přihlaste se pomocí stejného účtu, který jste použili ke konfiguraci připojení mezi Intune a Androidem Enterprise.
2. Vyhledejte a vyberte v obchodě aplikaci, kterou chcete přiřadit pomocí Intune.
3. Na stránce, na které se aplikace zobrazuje, klikněte na **schválit**.  
    Na tomto příkladu jsme zvolili Microsoft Excel.

    ![Tlačítko Schválit ve spravovaném obchodu Google Play](./media/apps-add-android-for-work/approve.png)

   Otevře se okno s žádostí, abyste této aplikaci udělili oprávnění k provádění různých operací.

4. Pokud chcete přijmout oprávnění aplikace a pokračovat, vyberte **Schválit**.

    ![Na tlačítko Schválit pro oprávnění aplikace](./media/apps-add-android-for-work/approve-app-permissions.png)

5. Vyberte způsob zpracovávání nových žádostí oprávnění aplikace a potom zvolte **Uložit**.

    ![Možnosti zpracovávání nových žádostí oprávnění aplikace](./media/apps-add-android-for-work/approve-app-settings.png)

    Aplikace se schválí a zobrazí v konzole pro správu. V dalším kroku můžete [synchronizovat aplikaci pracovní profil pro Android s Intune](apps-add-android-for-work.md#sync-a-managed-google-play-app-with-intune).

## <a name="managed-google-play-private-lob-apps"></a>Spravované Google Play soukromé aplikace (LOB)

Existují dva způsoby, jak přidat obchodní aplikace do spravovaných Google Play:

1. Přímo v konzole Intune – díky tomu můžete přidat obchodní aplikace tím, že v Intune odešlete jenom APK a název aplikace. Tato metoda nevyžaduje, abyste měli účet vývojáře Google a nemuseli platit poplatek za jeho registraci v Google jako vývojář.  Tato metoda je jednodušší a má výrazně omezený počet kroků a zpřístupňuje obchodní aplikace pro správu v pouhých deseti minutách.
1. V konzole pro vývojáře Google Play – Pokud máte účet pro vývojáře Google nebo chcete nakonfigurovat pokročilé funkce distribuce, které jsou dostupné jenom v konzole pro vývojáře Google Play (jako je přidání dalších obrazovek s dalšími aplikacemi), můžete použít [konzolu pro vývojáře Google Play](https://play.google.com/apps/publish). 

### <a name="managed-google-play-private-lob-app-publishing-directly-in-the-intune-console"></a>Spravované Google Play privátních aplikací (LOB) přímo v konzole Intune

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace**  >  **všechny aplikace**  >  **Přidat**.
3. V podokně **Vybrat typ aplikace** v části dostupné typy **aplikací pro Store** vyberte **Managed Google Play App**.
4. Klikněte na **Vybrat**. V Intune se zobrazuje **spravované Google Play** App Store.
5. V okně Google Play vyberte **soukromé aplikace** (vedle ikony *zámku* ). 
6. Kliknutím na tlačítko **"+"** v pravém dolním rohu přidejte novou aplikaci.
7. Přidejte **název** aplikace a klikněte na **nahrát APK** přidat balíček aplikace APK.
8. Klikněte na **Vytvořit**.
9. Pokud jste dokončili přidávání aplikací, zavřete podokno spravované Google Play.
10. V podokně **aplikace aplikace** klikněte na **synchronizovat** a synchronizujte se se službou Managed Google Play Service. 

    > [!NOTE]
    > Synchronizace privátních aplikací může trvat několik minut, než se synchronizuje. Pokud se aplikace při prvním provedení synchronizace nezobrazí, počkejte pár minut a zahajte novou synchronizaci.

Další informace o spravovaných Google Play privátních aplikacích včetně nejčastějších dotazů najdete v článku podpora Google:https://support.google.com/googleplay/work/answer/9146439

>[!IMPORTANT]
>Privátní aplikace přidané pomocí této metody se nikdy nedají zveřejnit. Tuto možnost publikování použijte jenom v případě, že jste si jisti, že tato aplikace bude vždycky soukromá pro vaši organizaci.

### <a name="managed-google-play-private-lob-app-publishing-using-the-google-developer-console"></a>Spravované Google Play privátních aplikací (LOB) pro publikování pomocí vývojářské konzoly Google

1. Přihlaste se ke [konzole pro vývojáře Google Play](https://play.google.com/apps/publish) pomocí stejného účtu, který jste použili ke konfiguraci připojení mezi Intune a Androidem Enterprise.  
    Pokud se přihlašujete poprvé, musíte se zaregistrovat a zaplatit poplatek, abyste se stali členy programu pro vývojáře Google.
2. V této konzole zvolte **Přidat novou aplikaci**.
3. Informace o vaší aplikaci nahrajete a zadáte stejným způsobem jako při publikování jakékoli jiné aplikace v obchodě Google Play. Musíte ale vybrat **Zpřístupnit tuto aplikaci pouze pro moji organizaci (<*název organizace*>)**.

    Tato operace zpřístupní aplikaci ve vaší organizaci. Nebude dostupná ve veřejném obchodu Google Play.

    Další informace o nahrávání a publikování aplikací pro Android najdete v [nápovědě ke konzole pro vývojáře Google](https://support.google.com/googleplay/android-developer/answer/113469).
4. Po publikování aplikace se přihlaste ke [spravovanému Google Play Storu](https://play.google.com/work) pomocí stejného účtu, který jste použili ke konfiguraci připojení mezi Intune a Androidem Enterprise.
5. Ověřte si, že se v uzlu **Aplikace** tohoto obchodu zobrazuje aplikace, kterou jste publikovali.  
    Synchronizace s Intune bude automaticky schválená.

## <a name="managed-google-play-web-links"></a>Spravované Google Play webové odkazy

Spravované Google Play webové odkazy se můžou instalovat a spravovat stejně jako jiné aplikace pro Android. Když se na zařízení nainstaluje, zobrazí se v seznamu aplikací daného uživatele spolu s dalšími aplikacemi, které nainstaloval. Po klepnutí se spustí v prohlížeči zařízení.

Webové odkazy se otevřou pomocí Microsoft Edge nebo jakékoli jiné aplikace prohlížeče, kterou si zvolíte k nasazení. Nezapomeňte nasadit aspoň jednu aplikaci v prohlížeči do zařízení, aby se webové odkazy daly správně otevřít. Všechny možnosti **zobrazení** dostupné pro webové odkazy (celá obrazovka, samostatné a minimální uživatelské rozhraní) ale budou fungovat jenom s prohlížečem Chrome. 

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace**  >  **všechny aplikace**  >  **Přidat**.
3. V podokně **Vybrat typ aplikace** v části dostupné typy **aplikací pro Store** vyberte **Managed Google Play App**.
4. Klikněte na **Vybrat**. V Intune se zobrazuje **spravované Google Play** App Store.
5. V okně Google Play vyberte **Web Apps** (vedle ikony *zeměkoule* ).
6. Kliknutím na tlačítko **"+"** v pravém dolním rohu přidejte novou aplikaci.
7. Přidejte **název**aplikace, **adresu URL**webové aplikace, vyberte, jak se má aplikace zobrazit, a vyberte ikonu aplikace.
8. Klikněte na **Vytvořit**.
9. Pokud jste dokončili přidávání aplikací, zavřete podokno spravované Google Play.
10. V podokně **aplikace aplikace** klikněte na **synchronizovat** a synchronizujte se se službou Managed Google Play Service. 

    > [!NOTE]
    > Aby bylo možné synchronizovat webové aplikace, může trvat několik minut. Pokud se aplikace při prvním provedení synchronizace nezobrazí, počkejte pár minut a zahajte novou synchronizaci.

## <a name="sync-a-managed-google-play-app-with-intune"></a>Synchronizace aplikace ze spravovaného obchodu Google Play s Intune

Pokud jste aplikaci schválili ze Storu a nevidíte ji v úloze **aplikace** , vynuťte okamžitou synchronizaci následujícím způsobem:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Vyberte **aplikace**  >  konektory**pro správu tenanta**  >  **a tokeny**  >  **spravované Google Play**.
5. V podokně **Spravovaný obchod Google Play** zvolte **Aktualizovat**.  
    Stránka aktualizuje čas a stav poslední synchronizace.
6. V centru pro správu Microsoft Endpoint Manageru vyberte **aplikace**  >  **všechny aplikace**.  
    Zobrazí se nově dostupná aplikace ze spravovaného obchodu Google Play.

## <a name="assigning-a-managed-google-play-app-to-android-enterprise-work-profile-devices"></a>Přiřazení spravované aplikace Google Play k zařízením s pracovním profilem v systému Android Enterprise

Když se aplikace zobrazí v uzlu **licence aplikace** podokna úloh **aplikace** , můžete [ji přiřadit stejně jako jakoukoli jinou aplikaci](/mem/intune/apps/apps-deploy) , a to tak, že aplikaci přiřadíte skupinám uživatelů.

Po přiřazení aplikace je nainstalovaná (nebo dostupná pro instalaci) na zařízeních uživatelů, na které jste cíleni. Uživatel zařízení nebude požádán o schválení instalace. Další informace o zařízeních s pracovním profilem Android Enterprise najdete v tématu [Nastavení registrace zařízení s pracovním profilem v Androidu Enterprise](../enrollment/android-work-profile-enroll.md). 

> [!NOTE] 
> Pouze aplikace, které byly přiřazeny, se zobrazí ve spravovaném Google Play Storu pro koncového uživatele. V takovém případě se jedná o klíčový krok, který může správce provést při nastavování aplikací se spravovanými Google Play.

## <a name="assigning-a-managed-google-play-app-to-android-enterprise-fully-managed-devices"></a>Přiřazení spravované aplikace Google Play k zařízením s plně spravovaným systémem Android Enterprise

[Zařízení se systémem Android Enterprise standarded](../enrollment/android-fully-managed-enroll.md) jsou zařízení vlastněná společností, která jsou přidružená k jednomu uživateli a používána výhradně pro práci a nikoli pro osobní použití. Uživatelé na plně spravovaných zařízeních můžou z spravované aplikace Google Play na svém zařízení získat své dostupné firemní aplikace.

Ve výchozím nastavení zařízení s plně spravovaným podnikem v Androidu neumožní zaměstnancům instalovat žádné aplikace, které organizace neschválila. Zaměstnanci také nebudou moci odebrat žádné nainstalované aplikace proti zásadám. Pokud chcete, aby uživatelé měli přístup k úplnému Google Play Storu pro instalaci aplikací, a ne jenom přístup ke schváleným aplikacím ve spravovaném Google Play Storu, můžete nastavit možnost **Povolení přístupu ke všem aplikacím v Google Play Storu** . **Allow** S tímto nastavením může uživatel přistupovat ke všem aplikacím v Google Play Storu pomocí svého podnikového účtu, ale nákupy můžou být omezené. Omezení počtu omezení nákupu můžete odebrat tak, že uživatelům na zařízení přidáte nové účty. Tím umožníte, aby koncoví uživatelé měli možnost nakupovat aplikace z Google Play Storu pomocí osobních účtů a provádět nákupy v aplikaci. Další informace najdete v tématu [nastavení zařízení s Androidem Enterprise a povolení nebo omezení funkcí v Intune](../configuration/device-restrictions-android-for-work.md). 

> [!NOTE]
> Aplikace Microsoft Intune, aplikace Microsoft Authenticator a aplikace Portál společnosti budou v průběhu připojování nainstalovány jako požadované aplikace do všech plně spravovaných zařízení. Automatické instalace těchto aplikací poskytuje podporu podmíněného přístupu a Microsoft Intune uživatelé aplikací můžou zobrazit a vyřešit problémy s dodržováním předpisů. 

## <a name="manage-android-enterprise-app-permissions"></a>Správa oprávnění pro podnikovou aplikaci Android
Android Enterprise vyžaduje, abyste před synchronizací s Intune schválili aplikace ve webové konzoli spravované Google Play a přiřadili je uživatelům. Vzhledem k tomu, že Android Enterprise umožňuje bez tichého a automatického vkládání aplikací do zařízení uživatelů, musíte přijmout oprávnění aplikace jménem všech uživatelů. Uživatelé neuvidí při instalaci žádná oprávnění aplikací, takže je důležité, abyste těmto oprávněním porozuměli.

Když vývojář aplikace aktualizuje oprávnění v nové verzi aplikace, nejsou tato oprávnění přijata automaticky, i když jste dřívější oprávnění schválili. Zařízení s předchozí verzí aplikace ji mohou dál používat. Dokud ale oprávnění neschválíte, nebude se aplikace upgradovat. Na zařízení, ve kterých tato aplikace není nainstalovaná, nejde aplikace nainstalovat, dokud neschválíte její nová oprávnění. 

### <a name="update-app-permissions"></a>Aktualizace oprávnění aplikace

Pravidelně navštěvujte spravovanou konzolu Google Play a kontrolujte nová oprávnění. Obchod Google Play můžete nastavit tak, aby byl vám nebo jiným uživatelům zaslán e-mail, pokud bude schválená aplikace vyžadovat nová oprávnění. Pokud přiřadíte aplikaci a zjistíte, že není na zařízeních nainstalovaná, zkontrolujte tímto způsobem nová oprávnění:

1. Přejděte na [Google Play](https://play.google.com/work).
2. Přihlaste se pod účtem Google, který jste použili k publikování a schválení aplikací.
3. Vyberte kartu **Aktualizace** a zkontrolujte, jestli některé aplikace nevyžadují aktualizaci.  
    Všechny zde uvedené aplikace vyžadují nová oprávnění a nepřiřadí se, dokud nebudou použita.

Případně ale můžete obchod Google Play nastavit tak, aby automaticky schvaloval nová oprávnění pro každou z aplikací.

## <a name="additional-managed-google-play-app-reporting-for-android-enterprise-work-profile-devices"></a>Další spravované Google Play vytváření sestav aplikací pro zařízení s Androidem Enterprise Work Profile

U spravovaných aplikací Google Play nasazených do zařízení se systémem Android Enterprise Work profilů můžete zobrazit stav a číslo verze aplikace nainstalované na zařízení pomocí Intune. 

## <a name="working-with-managed-google-play-closed-testing-tracks"></a>Práce s ukončenými testovacími běhy spravované Google Play

Neprodukční verzi spravované aplikace Google Play můžete distribuovat do zařízení zaregistrovaných ve scénáři Android Enterprise (**Enterprise Work Profile**, **plně spravované**a **vyhrazené**), aby bylo možné provádět testování. V Intune můžete zjistit, jestli aplikace obsahuje předprodukční zkušební záznam buildu, který je na něj publikovaný, a taky umožnit přiřazení této stopy ke skupinám uživatelů AAD nebo skupinám zařízení. Pracovní postup přiřazení produkční verze ke skupině, která aktuálně existuje, je stejný jako při přiřazování neprodukčního kanálu. Po nasazení bude stav instalace každé stopy odpovídat číslu verze stopy ve spravovaném Google Play. Další informace najdete v tématu [o ukončených testovacích běhů Google Play pro předběžné verze testování aplikace](https://support.google.com/googleplay/android-developer/answer/3131213).

## <a name="delete-managed-google-play-apps"></a>Odstranit spravované aplikace Google Play
V případě potřeby můžete z Microsoft Intune odstranit spravované aplikace Google Play. Pokud chcete odstranit spravovanou aplikaci Google Play, otevřete Microsoft Intune v Azure Portal a vyberte **aplikace**  >  **všechny aplikace**. V seznamu aplikace vyberte tři tečky (...) napravo od spravované aplikace Google Play a pak v zobrazeném seznamu vyberte **Odstranit** . Při odstranění spravované aplikace Google Play ze seznamu aplikací se spravovaná aplikace Google Play automaticky neschválí.

> [!NOTE]
> Pokud je aplikace neschválená nebo Odstraněná ze spravovaného úložiště Google Play, nebude odebrána ze seznamu klientských aplikací Intune. To vám umožní pořád cílit zásady odinstalace na uživatele, i když je aplikace neschválená.
> 
> Pokud chcete vypnout registraci a správu Androidu Enterprise, přečtěte si téma [Odpojení účtu správce Android Enterprise](../enrollment/connect-intune-android-enterprise.md#disconnect-your-android-enterprise-administrative-account).

## <a name="android-enterprise-system-apps"></a>Systémové aplikace typu Android Enterprise

Můžete povolit aplikaci pro Android Enterprise pro [Podniková vyhrazená zařízení s Androidem](../enrollment/android-kiosk-enroll.md) nebo [plně spravovaná zařízení](../enrollment/android-fully-managed-enroll.md). Další informace o přidání aplikace pro Android Enterprise System najdete v tématu [Přidání aplikací pro Android Enterprise System pro Microsoft Intune](apps-ae-system.md).

## <a name="next-steps"></a>Další kroky

- [Přiřazení aplikací skupinám](apps-deploy.md)
