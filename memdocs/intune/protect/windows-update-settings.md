---
title: Nastavení aktualizace Windows pro firmy pro Microsoft Intune – Azure | Microsoft Docs
description: Nastavení WUfB pro zařízení s Windows 10, která můžete nasadit pomocí Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: aiwang
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: ba826620d1589d081f683e3b4c807115c4a137ae
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/25/2020
ms.locfileid: "88819707"
---
# <a name="windows-update-settings-for-intune"></a>Nastavení služby Windows Update pro Intune  

Prohlédněte si nastavení aktualizace Windows 10, která můžete [Konfigurovat a spravovat](windows-update-for-business-configure.md) pomocí Microsoft Intune.  

Když konfigurujete nastavení pro aktualizační kanály Windows 10 v Intune, konfigurujete nastavení web Windows Update. Pokud má nastavení Windows Update závislost na verzi Windows 10, zaznamená se závislost na verzi v podrobnostech nastavení.  

## <a name="update-settings"></a>Aktualizace nastavení  

Nastavení aktualizace řídí, co se bude stahovat a kdy se zařízení stáhne. Další informace o chování jednotlivých nastaveních najdete v referenční dokumentaci k systému Windows.  

- **Kanál pro údržbu**  
  **Výchozí**: půlroční kanál  
  Web Windows Update CSP: [Update/BranchReadinessLevel](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-branchreadinesslevel)  

  Nastavte kanál (větev), ze kterého zařízení přijímá aktualizace systému Windows. Různé kanály můžou před doručením aktualizací používat odlišná období odložení.  

  Například *půlroční kanál* má odložení po dobu šesti měsíců. Pokud použijete tento kanál bez dalších odložení z tohoto základního nastavení, zařízení nainstaluje aktualizaci po dobu šesti měsíců po jejím vydání.  

  Podporované kanály pro aktualizace:  

  - Půlroční kanál  
  - Půlroční kanál (cílený)  
  - Windows Insider – rychlá  
  - Windows Insider – pomalé  
  - Windows Insider – Release  

  Když vyberete kanál Insider, Intune automaticky nakonfiguruje nastavení služby Windows Update [Update/ManagePreviewBuilds](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-managepreviewbuilds) , aby se Build Insider mohl pracovat.  


  > [!IMPORTANT]  
  > Počínaje systémem Windows verze 1903 je použití *pololetního kanálu (cílené)* (SAC-T) vyřazeno. Při této změně se SAC – T sloučí s *půlročním kanálem*. Pokud chcete získat další informace o této změně a o tom, jak má vliv na web Windows Update pro firmy, přečtěte si Blogový příspěvek ve Windows pro IT specialisty [web Windows Update pro firmy a vyřazení konzoly SAC – T](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/Windows-Update-for-Business-and-the-retirement-of-SAC-T/ba-p/339523).  
 
- **Aktualizace produktů Microsoftu**  
  **Výchozí**: povolení  
  Web Windows Update CSP: [Update/AllowMUUpdateService](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-allowmuupdateservice)

  - **Povolení** – vyberte možnost *umožňuje* vyhledávat aktualizace aplikací z Microsoft Update.  
  - **Blok-výběr** bloku, který zabrání v kontrole aktualizací aplikace.  

- **Ovladače pro Windows**  
  **Výchozí**: povolení  
  Web Windows Update CSP: [Update/ExcludeWUDriversInQualityUpdate](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-excludewudriversinqualityupdate)  

  - **Povoleno** – zaškrtněte políčko *povoleno* zahrnout web Windows Update ovladače během aktualizací.  
  - **Blok-výběr** bloku, který zabrání v kontrole ovladačů.  

- **Doba odložení aktualizace kvality (ve dnech)**  
  **Výchozí hodnota**: 0  
  Web Windows Update CSP: [Update/DeferQualityUpdatesPeriodInDays](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-deferqualityupdatesperiodindays)  

  Zadejte počet dní od 0 do 30, pro které se odložit aktualizace kvality. Toto období je kromě všech období odložení, které je součástí zvoleného kanálu služby. Doba odložení začíná, když zařízení obdrží zásady.  

  Aktualizace kvality jsou obvykle opravy a vylepšení stávajících funkcí systému Windows.  

- **Doba odložení aktualizace funkcí (ve dnech)**  
  **Výchozí hodnota**: 0  
  Web Windows Update CSP: [Update/PauseFeatureUpdatesPeriodInDays](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-deferfeatureupdatesperiodindays)  

  Zadejte počet dní, po které se mají odložit aktualizace funkcí. Toto období je kromě všech období odložení, které je součástí zvoleného kanálu služby. Doba odložení začíná, když zařízení obdrží zásady.  

  Podporované období odložení:  

  - *Windows verze 1709 a novější* -0 až 365 dní  
  
  Aktualizace funkcí jsou zpravidla nové funkce pro Windows.  

- **Nastavit období odinstalace aktualizací funkcí (2 – 60 dní)**  
  **Výchozí**: 10  
  Web Windows Update CSP: [Update/ConfigureFeatureUpdateUninstallPeriod](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-configurefeatureupdateuninstallperiod)  

  Nakonfigurujte čas, po kterém se aktualizace funkcí nedají odinstalovat.  

  Po uplynutí této doby se ze zařízení odeberou předchozí aktualizace a nebude už možné ji odinstalovat na předchozí verzi aktualizace.  

  Představte si například aktualizační kanál s dobou odinstalace aktualizace funkcí o 20 dní. Po 25 dnech se rozhodnete vrátit nejnovější aktualizaci funkcí a použít možnost odinstalace.  Zařízení, na která se nainstalovala aktualizace funkcí víc než 20 dní, ji nemůžou odinstalovat, protože v rámci údržby odebrala potřebné bity. Zařízení, u kterých se tato funkce nainstalovala jenom do 19 dnů, ale můžou aktualizaci odinstalovat, jenom když se úspěšně zaregistrují, aby se před tím, než je doba odinstalace odinstalovala.  

## <a name="user-experience-settings"></a>Nastavení uživatelského prostředí  

Nastavení uživatelského prostředí řídí činnost koncového uživatele při restartu a připomenutích zařízení. Další informace o chování jednotlivých nastaveních najdete v dokumentaci k web Windows Update CSP.  

- **Chování automatické aktualizace**  
  **Výchozí**: automaticky instalovat v době údržby  
  Web Windows Update CSP: [Update/AllowAutoUpdate](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-allowautoupdate)  

  Vyberte, jak se mají nainstalovat automatické aktualizace, a v případě potřeby i po restartování zařízení.  

  Podporované možnosti:  

  - **Upozorňovat na stažení** – před stažením aktualizace upozorněte uživatele. Uživatelé si můžou stáhnout a nainstalovat aktualizace.  

  - Automaticky **nainstalovat v době údržby** – aktualizace se automaticky stahují a pak se během automatické údržby instalují, když se zařízení nepoužívá nebo neběží při napájení z baterie. Po restartování počítače se uživatelům zobrazí výzva k restartování po dobu až sedmi dnů a pak se restartování vynutí.  

    Tato možnost po instalaci aktualizace může zařízení restartovat automaticky. Pomocí nastavení **aktivní hodiny** můžete definovat období, během kterého jsou automatické restartování blokované:  

    - **Začátek aktivních hodin** – zadejte počáteční čas pro potlačení restartování z důvodu instalace aktualizací.  
      **Výchozí**: 8 dop.  
      Web Windows Update CSP: [Update/ActiveHoursStart](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-activehoursstart)  
  
    - **Aktivní hodiny končí** – zadejte čas ukončení pro potlačení restartování kvůli instalaci aktualizací.  
      **Výchozí**: 5 odp.  
      Web Windows Update CSP: [Update/ActiveHoursEnd](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-activehoursend)  

  - Automaticky **nainstalovat a restartovat v době údržby** – aktualizace se automaticky stahují a pak se nainstalují během automatické údržby, když se zařízení nepoužívá nebo se spouští při napájení z baterie. Pokud je vyžadováno restartování, zařízení se restartuje, když se nepoužívá. (Toto je výchozí nastavení pro nespravovaná zařízení.)  

    Tato možnost po instalaci aktualizace může zařízení restartovat automaticky. Použití nastavení **aktivní hodiny** není popsané v nastavení web Windows Update, ale používá se v Intune k definování období, během kterého se zablokuje automatické restartování:  

    - **Začátek aktivních hodin** – zadejte počáteční čas pro potlačení restartování z důvodu instalace aktualizací.  
      **Výchozí**: 8 dop.  
      Web Windows Update CSP: [Update/ActiveHoursStart](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-activehoursstart)  
  
    - **Aktivní hodiny končí** – zadejte čas ukončení pro potlačení restartování kvůli instalaci aktualizací.  
      **Výchozí**: 5 odp.  
      Web Windows Update CSP: [Update/ActiveHoursEnd](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-activehoursend)  

  - **Automaticky nainstalovat a restartovat v naplánovaném čase** – zadejte den a čas instalace. Je-li tento parametr zadán, bude instalace spuštěna 3. den a následuje 15 minut odpočítávání za účelem restartu. Přihlášené používání může zpozdit odpočítávání a restartování.   
  Web Windows Update CSP: [Update/AllowAutoUpdate](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-allowautoupdate)  

    Tato možnost podporuje další nastavení.  

    - **Frekvence automatického chování** – pomocí tohoto nastavení můžete naplánovat instalaci aktualizací, včetně týdne, dne a času.  
      **Výchozí**: každý týden

    - **Den plánované instalace** – určete, ke kterému dni v týdnu chcete nainstalovat aktualizace.  
      **Výchozí**: každý den  

    - **Čas plánované instalace** – zadejte denní dobu, kdy se mají aktualizace instalovat.  
      **Výchozí**: 3 dop.  

  - Automaticky **nainstalovat a restartovat bez ovládacího prvku pro koncové uživatele** – aktualizace se automaticky stahují a pak se nainstalují během automatické údržby, když se zařízení nepoužívá nebo neběží na napájení z baterie. Pokud je vyžadováno restartování, zařízení se restartuje, když se nepoužívá. Tato možnost nastaví podokno ovládacího prvku koncoví uživatelé na jen pro čtení.  

  - **Obnovit výchozí** – obnoví původní nastavení automatické aktualizace na počítačích s Windows 10, na kterých běží aktualizace z října 2018 nebo novější.  


- **Restartovat kontroly**  
  **Výchozí**: povolení  
  Web Windows Update CSP: [Update/SetEDURestart](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-setedurestart)  

  Pokud tyto kontroly chcete přeskočit, zvolte **Přeskočit**. 
  
  Toto nastavení má různé výsledky v závislosti na verzi Windows pro zařízení:  
 
  - *Windows verze 1709 a novější* – během aktivní hodiny se pro aktualizace nespouštějí následující procesy: kontrola, stažení, instalace a restartování. Po aktivní hodině se procesy aktualizace spouštějí a můžou zařízení probudit z režimu spánku, prohledávat, stahovat, instalovat a restartovat zařízení, pokud se kontrolují baterie a kontrolují napájení. 

- **Zablokovat uživateli pozastavit aktualizace Windows**  
  **Výchozí**: povolení  
  Web Windows Update CSP: [Update/SetDisablePauseUXAccess](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-setdisablepauseuxaccess)  

  - **Povolení** – povolí uživatelům zařízení pozastavit instalaci aktualizace.  
  - **Blok** – zabraňuje uživatelům zařízení pozastavit instalaci aktualizace.  

- **Zablokovat uživateli kontrolu aktualizací Windows**  
  **Výchozí**: povolení  
  Web Windows Update CSP: [Update/SetDisableUXWUAccess](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-setdisableuxwuaccess) 

  - **Povolení** – umožní uživatelům zařízení použít web Windows Update prohledávání k vyhledání a stažení aktualizací a instalaci funkcí.
  - **Blok** – zabraňuje uživatelům zařízení v přístupu k web Windows Update kontrole, stahování aktualizací a instalaci funkcí.  

- **Pro zavření oznámení o restartování vyžadovat schválení uživatele**  
  **Výchozí**: Nenakonfigurováno  
  Web Windows Update CSP: [Update/AutoRestartRequiredNotificationDismissal](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-autorestartrequirednotificationdismissal)
  
  - **Žádné** automatické odhlašování po 25 sekundách.
  - **Ano** – vyžaduje vynechávání uživatele.
   
- **Připomenout uživatele před vyžadováním automatického restartování s připomenutím přeskočit (hodiny)**  
  **Výchozí**: 4  
  Web Windows Update CSP: [Update/ScheduleRestartWarning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-schedulerestartwarning)  

  Určete, jak dlouho předem má automatické restartování zobrazovat oznámení přeskočit uživateli zařízení o tomto restartování. Jsou podporovány hodnoty **2**, **4**, **8**, **12**a **24** hodin.  
  
  Když výchozí hodnota zrušíte, toto nastavení se *nenakonfigurovalo*.  

- **Připomenout uživatele před vyžadováním automatického restartování s trvalým připomenutím (minuty)**  
  **Výchozí**: 15  
  Web Windows Update CSP: [Update/ScheduleImminentRestartWarning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-scheduleimminentrestartwarning)  

  Zadejte, jak dlouho předem bude automatické restartování pro uživatele zařízení o tomto restartování zobrazovat upozornění bez přeskočit. Jsou podporovány hodnoty **15**, **30** a **60** minut.  

  Když výchozí hodnota zrušíte, toto nastavení se *nenakonfigurovalo*.  

- **Změna úrovně oznámení aktualizace**  
  **Výchozí**: použít výchozí oznámení web Windows Update  
  Web Windows Update CSP: [Update/UpdateNotificationLevel](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-updatenotificationlevel)
  
  Určete, jakou úroveň oznámení web Windows Update uživatelé uvidí. Toto nastavení neurčuje, jak a kdy se aktualizace stahují a instalují.  

  Podporované možnosti:
  - **Není nakonfigurováno**
  - **Použít výchozí oznámení web Windows Update**
  - **Vypnout všechna oznámení s výjimkou upozornění na restartování**
  - **Vypnout všechna oznámení, včetně upozornění na restartování**  

- **Použít nastavení termínu**  
  **Výchozí**: Nenakonfigurováno  
 
  Umožňuje uživateli použít nastavení termínu.  

  - **Není nakonfigurováno**
  - **Povolit**

  Pokud je nastaveno na hodnotu *povoleno*, můžete pro termíny nakonfigurovat následující nastavení:

  - **Konečný termín pro aktualizace funkcí**  
    **Výchozí**: *Nenakonfigurováno*  
    Web Windows Update CSP: [Update/ConfigureDeadlineForFeatureUpdates](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-configuredeadlineforfeatureupdates)  

    Určuje počet dní, po které má uživatel, než se aktualizace funkcí na svých zařízeních nainstalují automaticky (2-30).

  - **Konečný termín pro aktualizace kvality**  
    **Výchozí**: *Nenakonfigurováno*  
    Web Windows Update CSP: [Update/ConfigureDeadlineForQualityUpdates](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-configuredeadlineforqualityupdates)

    Určuje počet dní, po které má uživatel k automatické instalaci aktualizací kvality na svých zařízeních (2-30).

  - **Období odkladu**  
    **Výchozí**: *není nakonfigurované* web Windows Update CSP: [Update/ConfigureDeadlineGracePeriod]( https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-configuredeadlinegraceperiod)

    Určuje minimální počet dnů po termínu, do kterého proběhne automatické restartování (0-7).

  - **Automatický restart před konečným termínem**  
    **Výchozí**: Ano web Windows Update CSP: [Update/ConfigureDeadlineNoAutoReboot](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-configuredeadlinenoautoreboot)

    Určuje, jestli se má zařízení před konečným termínem automaticky restartovat.
    - **Ano**
    - **Ne**

### <a name="delivery-optimization-download-mode"></a>Režim stažení Optimalizace doručení  

Optimalizace doručení již není konfigurována jako součást aktualizačního kanálu Windows 10 v části aktualizace softwaru. Optimalizace doručování se teď nastavuje prostřednictvím konfigurace zařízení. Předchozí konfigurace ale zůstanou v konzole k dispozici. Tyto předchozí konfigurace můžete odebrat tak, že je upravíte, aby *nebyly nakonfigurované*, ale nelze je jinak upravovat. 

Aby nedocházelo ke konfliktům mezi novou a starou zásadou, přečtěte si téma [Odebrání optimalizace doručování z aktualizačních kanálů Windows 10](../configuration/delivery-optimization-windows.md#remove-delivery-optimization-from-windows-10-update-rings) a přesunutí nastavení do profilu Optimalizace doručení.
