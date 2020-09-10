---
title: Správa aplikací Win32 v Microsoft Intune
titleSuffix: ''
description: Naučte se spravovat aplikace Win32 pomocí Microsoft Intune. Toto téma poskytuje přehled funkcí pro doručování a správu aplikací Intune Win32.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: efdc196b-38f3-4678-ae16-cdec4303f8d2
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: contperfq1
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6579f5137abd20e564616bf1ef6188fc7b5a5009
ms.sourcegitcommit: 54a771f1a632aef5d6bf8c71ce1e2c7823513b52
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/10/2020
ms.locfileid: "90003001"
---
# <a name="win32-app-management-in-microsoft-intune"></a>Správa aplikací Win32 v Microsoft Intune

Microsoft Intune umožňuje funkce správy aplikací Win32. Přestože zákazníci připojení ke cloudu mohou pro správu aplikací Win32 používat nástroj Configuration Manager, zákazníci, kteří používají pouze Intune, mají širší možnosti správy svých obchodních aplikací Win32. V tomto tématu najdete přehled funkcí správy aplikací Win32 Intune a související informace.

> [!NOTE]
> Tato funkce správy aplikací podporuje jak 32, tak 64 architekturu operačního systému pro aplikace Windows.

> [!IMPORTANT]
> Při nasazování aplikací Win32 zvažte výhradně použití přístupu [rozšíření správy Intune](../apps/intune-management-extension.md) , zejména v případě, že máte k dispozici instalační program aplikace pro více souborů Win32. Pokud během registrace automatického pilotního nasazení kombinujete instalaci aplikací Win32 a obchodních aplikací, může instalace aplikace selhat. Rozšíření pro správu Intune se nainstaluje automaticky, když se k uživateli nebo zařízení přiřadí skript prostředí PowerShell nebo aplikace Win32.

## <a name="prerequisites"></a>Předpoklady

Pokud chcete používat správu aplikací Win32, ujistěte se, že splňujete následující kritéria:

- Windows 10 verze 1607 nebo novější (verze Enterprise, pro a školství)
- Klient Windows 10 musí splňovat tyto předpoklady: 
  - Zařízení musí být připojená k Azure AD a automaticky zaregistrovaná. Rozšíření pro správu Intune podporuje připojení ke službě Azure AD, která je připojená k hybridní doméně, a jsou podporovaná zařízení zaregistrovaná v zásadách skupiny. 
  > [!NOTE]
  > V případě zaregistrovaného scénáře zásad skupiny koncový uživatel použije místní uživatelský účet k AAD připojit své zařízení s Windows 10. Uživatel se musí do zařízení přihlásit pomocí svého uživatelského účtu AAD a zaregistrovat se do Intune. Intune nainstaluje na zařízení rozšíření pro správu Intune, pokud je skript PowerShellu nebo aplikace Win32 cílené na uživatele nebo zařízení.
- Velikost aplikace systému Windows je omezené na 8 GB na aplikaci.

## <a name="prepare-the-win32-app-content-for-upload"></a>Příprava obsahu aplikace Win32 pro nahrání

Než budete moct přidat aplikaci Win32 do Microsoft Intune, musíte aplikaci připravit pomocí nástroje pro přípravu obsahu Microsoft Win32. Pomocí nástroje pro přípravu obsahu Win32 předběžného zpracování aplikací pro Windows Classic (Win32). Nástroj převede instalační soubory aplikace do formátu *. intunewin* . Další informace a kroky najdete v tématu [Příprava obsahu aplikace Win32 pro nahrání](apps-win32-prepare.md). 

## <a name="add-assign-and-monitor-a-win32-app"></a>Přidání, přiřazení a monitorování aplikace Win32

Po [přípravě aplikace Win32, která se má nahrát do Intune](apps-win32-prepare.md) pomocí nástroje pro přípravu obsahu Microsoft Win32, můžete aplikaci přidat do Intune. Další informace a postup najdete v tématu [Přidání, přiřazení a monitorování aplikace Win32 v Microsoft Intune](apps-win32-add.md).

## <a name="delivery-optimization"></a>Optimalizace doručení

Windows 10 1709 a novější klienti stáhnou obsah aplikace Intune Win32 pomocí součásti optimalizace doručování v klientovi s Windows 10. Optimalizace doručení poskytuje funkce peer-to-peer, které jsou ve výchozím nastavení zapnuté. Můžete nakonfigurovat agenta pro optimalizaci doručení ke stažení obsahu aplikace Win32 buď v režimu pozadí, nebo v režimu popředí na základě přiřazení. Optimalizace doručení se dá nakonfigurovat pomocí zásad skupiny a pomocí konfigurace zařízení v Intune. Další informace najdete v tématu [optimalizace doručování pro Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization). 

> [!NOTE]
> Můžete taky nainstalovat server s připojenou mezipamětí Microsoft do distribučních bodů Configuration Manager pro ukládání obsahu aplikace Win32 v Intune. Další informace najdete v tématu věnovaném [podpoře aplikací pro Intune Win32 v Configuration Manager](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune).

## <a name="install-required-and-available-apps-on-devices"></a>Instalace požadovaných a dostupných aplikací na zařízení

Koncový uživatel uvidí informační zprávy systému Windows pro požadované a dostupné instalace aplikací. Na následujícím obrázku je znázorněna ukázková informační zpráva, že instalace aplikace se nedokončí, dokud se zařízení nerestartuje. 

![Snímek obrazovky s oznámeními informačních zpráv systému Windows pro instalaci aplikace](./media/apps-win32-app-management/apps-win32-app-08.png)    

Následující obrázek upozorní koncového uživatele, že se na zařízení provádí změny aplikace.

![Snímek obrazovky oznamující uživateli, že probíhají změny aplikace](./media/apps-win32-app-management/apps-win32-app-09.png)    

Kromě toho aplikace Portál společnosti zobrazuje další zprávy o stavu instalace aplikací koncovým uživatelům. Pro funkce závislosti Win32 platí následující podmínky:
- Aplikaci se nepovedlo nainstalovat. Nevyhověly závislosti definované správcem.
- Aplikace byla úspěšně nainstalována, ale vyžaduje restart.
- Aplikace se právě instaluje, ale vyžaduje restart, aby bylo možné pokračovat.

## <a name="set-win32-app-availability-and-notifications"></a>Nastavení dostupnosti a oznámení aplikace Win32
Můžete nakonfigurovat čas zahájení a konečný termín pro aplikaci Win32. V počátečním čase rozšíření pro správu Intune spustí stažení obsahu aplikace a uloží je do mezipaměti pro požadovaný záměr. Aplikace se nainstaluje v čase konečného termínu. V případě dostupných aplikací se čas spuštění určí při zobrazení aplikace v Portál společnosti a obsah se stáhne, když koncový uživatel požádá aplikaci z Portál společnosti. Navíc můžete povolit dobu odkladu pro restartování. 

> [!IMPORTANT]
> Nastavení **období odkladu pro restartování** v části **přiřazení** je dostupné, jenom když je **chování zařízení** v části **program** nastavené na jednu z následujících možností:
> - **Určení chování na základě návratových kódů**
> - **Intune vynutí povinné restartování zařízení.**

Nastavte dostupnost aplikace na základě data a času požadované aplikace pomocí následujících kroků:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace**  >  **všechny aplikace**.
3. Vyberte ze seznamu existující **aplikaci pro Windows (Win32)** . 
4. V podokně aplikace vyberte **vlastnosti**  >  **Upravit** vedle oddílu **přiřazení** > **přidejte skupinu** pod **požadovaný** typ přiřazení. 
   Všimněte si, že dostupnost aplikace se dá nastavit na základě typu přiřazení. **Typ přiřazení** může být **povinný**, **dostupný pro zaregistrovaná zařízení**nebo **odinstalovat**.
5. Vyberte skupinu v podokně **Vybrat skupinu** a určete tak, do které skupiny uživatelů se aplikace přiřadí. 

    > [!NOTE]
    > Mezi možnosti **typu přiřazení** patří následující:<br>
    > - **Požadováno**: tuto aplikaci si můžete **nastavit jako povinnou pro všechny uživatele** nebo **nastavit tuto aplikaci jako povinnou na všech zařízeních**.<br>
    > - **K dispozici pro zaregistrovaná zařízení**: tuto aplikaci můžete nastavit tak, aby byla **dostupná pro všechny uživatele s registrovanými zařízeními**.<br>
    > - **Odinstalace**: můžete si vybrat možnost ***odinstalovat tuto aplikaci pro všechny uživatele** nebo **odinstalovat tuto aplikaci pro všechna zařízení**.

6. Chcete-li upravit možnosti **oznámení koncovým uživatelům** , vyberte možnost **Zobrazit všechna informační oznámení**.
7. V podokně **Upravit přiřazení** nastavte **oznámení pro uživatele Ender** , aby se **zobrazila všechna informační oznámení**. Všimněte si, že můžete nastavit **oznámení koncových uživatelů** a **Zobrazit všechna informační oznámení**, **Zobrazit informační zprávy pro restartování počítače**nebo **Skrýt všechna informační oznámení**.
8. Nastavte **Dostupnost aplikace** na **konkrétní datum a čas** a vyberte datum a čas. Toto datum a čas určuje, kdy se aplikace stáhne do zařízení koncových uživatelů. 
9. Nastavte **konečný termín instalace aplikace** na **konkrétní datum a čas** a vyberte datum a čas. Toto datum a čas určuje, kdy se aplikace nainstaluje na koncové uživatele. Pokud se pro stejného uživatele nebo zařízení provede více než jedno přiřazení, bude čas konečného termínu instalace aplikace vyzvednut na základě nejdřívějšího možného času.

10. Klikněte na **povoleno** vedle **období odkladu pro restartování**. Doba odkladu restartování se spustí hned po dokončení instalace aplikace na zařízení. Když je tato možnost zakázaná, může se zařízení bez upozornění restartovat. <br>Můžete přizpůsobit následující možnosti:
    - **Doba odkladu pro restartování zařízení (minuty)**: výchozí hodnota je 1440 minut (24 hodin). Tato hodnota může být maximálně 2 týdny.
    - **Vyberte, kdy se má zobrazit dialogové okno odpočítávání před restartováním (minuty)**: výchozí hodnota je 15 minut.
    - **Dovolit uživateli odložit oznámení o restartování**: můžete vybrat **Ano** nebo **ne**.
        - **Vyberte dobu opakovaného přiložení (minuty)**: výchozí hodnota je 240 minut (4 hodiny). Hodnota pro odložení nemůže být delší než doba odkladu pro restartování.

11. Klikněte na tlačítko **zkontrolovat a uložit**.

## <a name="toast-notifications-for-win32-apps"></a>Oznámení informačních zpráv pro aplikace Win32 
V případě potřeby můžete potlačit zobrazování oznámení informační zprávy koncového uživatele na přiřazení aplikace. V Intune vyberte **aplikace**  >  **všechny aplikace** > vyberte **přiřazení**> aplikace  >  **Zahrnout skupiny**. 

> [!NOTE]
> Rozšíření pro správu Intune nainstalované aplikace Win32 se odinstalují na nezaregistrovaných zařízeních. Správci můžou využít vyloučení přiřazení, aby nenabízeli aplikacím Win32 možnost BYOD zařízení.

## <a name="next-steps"></a>Další kroky

- Další informace o přidávání aplikací do Intune najdete v článku [Přidání aplikací do Microsoft Intune](apps-add.md).
