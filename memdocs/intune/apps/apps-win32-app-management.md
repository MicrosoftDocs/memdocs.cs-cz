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
ms.openlocfilehash: db28653207d7bf4341d614aeecb769dcc145caaa
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083926"
---
# <a name="win32-app-management-in-microsoft-intune"></a>Správa aplikací Win32 v Microsoft Intune

Microsoft Intune umožňuje funkce správy aplikací Win32. I když je možné, že zákazníci, kteří jsou připojeni k cloudu, používají Configuration Manager koncového bodu Microsoftu pro správu aplikací Win32, budou mít zákazníci s Intune větší možnosti správy pro své obchodní aplikace (LOB) pro Win32. V tomto tématu najdete přehled funkcí správy aplikací Win32 Intune a související informace.

> [!NOTE]
> Tato funkce správy aplikací podporuje jak 32, tak 64 architekturu operačního systému pro aplikace Windows.

> [!IMPORTANT]
> Když nasazujete aplikace Win32, zvažte výhradně použití [rozšíření pro správu služby Intune](../apps/intune-management-extension.md) , zejména v případě, že máte k dispozici instalační program Win32 aplikace s více soubory. Pokud během registrace automatického pilotního nasazení kombinujete instalaci aplikací Win32 a obchodních aplikací, může instalace aplikace selhat. Rozšíření pro správu Intune se nainstaluje automaticky, když se k uživateli nebo zařízení přiřadí skript prostředí PowerShell nebo aplikace Win32.

## <a name="prerequisites"></a>Předpoklady

Pokud chcete používat správu aplikací Win32, ujistěte se, že splňujete následující kritéria:

- Použijte Windows 10 verze 1607 nebo novější (verze Enterprise, pro a školství).
- Zařízení musí být připojená k Azure Active Directory (Azure AD) a automaticky zaregistrovaná. Rozšíření správy Intune podporuje zařízení, která jsou připojená k Azure AD, připojené k hybridní doméně a zaregistrované zásady skupiny. 
  > [!NOTE]
  > V případě registrace zásad skupiny uživatel používá místní uživatelský účet ke službě Azure AD připojit své zařízení s Windows 10. Uživatel se musí přihlásit k zařízení pomocí svého uživatelského účtu Azure AD a zaregistrovat se v Intune. Intune nainstaluje na zařízení rozšíření pro správu Intune, pokud je skript PowerShellu nebo aplikace Win32 cílené na uživatele nebo zařízení.
- Velikost aplikace systému Windows je omezené na 8 GB na aplikaci.

## <a name="prepare-the-win32-app-content-for-upload"></a>Příprava obsahu aplikace Win32 pro nahrání

Než budete moct přidat aplikaci Win32 do Microsoft Intune, musíte aplikaci připravit pomocí nástroje pro přípravu obsahu Microsoft Win32. Nástroj pro přípravu obsahu Microsoft Win32 slouží k předběžnému zpracování aplikací pro Windows Classic (Win32). Nástroj převede instalační soubory aplikace do formátu *. intunewin* . Další informace a kroky najdete v tématu [Příprava obsahu aplikace Win32 pro nahrání](apps-win32-prepare.md). 

## <a name="add-assign-and-monitor-a-win32-app"></a>Přidání, přiřazení a monitorování aplikace Win32

Po [přípravě aplikace Win32 pro nahrání do Intune](apps-win32-prepare.md) pomocí nástroje pro přípravu obsahu Microsoft Win32 můžete aplikaci přidat do Intune. Další informace a postup najdete v tématu [Přidání, přiřazení a monitorování aplikace Win32 v Microsoft Intune](apps-win32-add.md).

## <a name="delivery-optimization"></a>Optimalizace doručení

Klienti se systémem Windows 10 1709 a novějším stáhnou obsah aplikace Intune Win32 pomocí součásti optimalizace doručování v klientovi s Windows 10. Optimalizace doručení poskytuje funkce peer-to-peer, které jsou ve výchozím nastavení zapnuté. 

Můžete nakonfigurovat agenta pro optimalizaci doručení pro stažení obsahu aplikace Win32 v režimu pozadí nebo popředí na základě přiřazení. Optimalizace doručení se dá nakonfigurovat pomocí zásad skupiny a pomocí konfigurace zařízení v Intune. Další informace najdete v tématu [optimalizace doručování pro Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization). 

> [!NOTE]
> Můžete taky nainstalovat server s připojenou mezipamětí Microsoft do distribučních bodů Configuration Manager pro ukládání obsahu aplikace Win32 v Intune. Další informace najdete v tématu věnovaném [mezipaměti připojené k Microsoftu v Configuration Manager](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune).

## <a name="install-required-and-available-apps-on-devices"></a>Instalace požadovaných a dostupných aplikací na zařízení

Uživateli se zobrazí oznámení Windows pro požadovaná a dostupná instalace aplikace. Následující obrázek ukazuje příklad oznámení, ve kterém není instalace aplikace dokončena, dokud se zařízení nerestartuje. 

![Snímek obrazovky s oznámením Windows pro instalaci aplikace](./media/apps-win32-app-management/apps-win32-app-08.png)    

Následující obrázek upozorní uživatele, že se na zařízení provádí změny aplikace.

![Snímek obrazovky s informacemi o tom, že se provádí změny aplikace](./media/apps-win32-app-management/apps-win32-app-09.png)    

Kromě toho aplikace Portál společnosti zobrazuje více zpráv o stavu instalace aplikací pro uživatele. Pro funkce závislosti Win32 platí následující podmínky:
- Aplikaci se nepovedlo nainstalovat. Nevyhověly závislosti definované správcem.
- Aplikace byla úspěšně nainstalována, ale vyžaduje restart.
- Aplikace se právě instaluje, ale vyžaduje restart, aby bylo možné pokračovat.

## <a name="set-win32-app-availability-and-notifications"></a>Nastavení dostupnosti a oznámení aplikace Win32
Můžete nakonfigurovat čas zahájení a konečný termín pro aplikaci Win32. V počátečním čase rozšíření pro správu Intune spustí stažení obsahu aplikace a uloží ho do mezipaměti pro požadovaný záměr. Aplikace se nainstaluje v čase konečného termínu. 

V případě dostupných aplikací se čas spuštění určí při zobrazení aplikace na portálu společnosti a obsah se stáhne, když si uživatel vyžádá aplikaci z portálu společnosti. Můžete také povolit dobu odkladu pro restartování. 

> [!IMPORTANT]
> Nastavení **období odkladu pro restartování** v části **přiřazení** je dostupné jenom v případě, že se **chování zařízení při restartu** v části **program** nastavilo na jednu z následujících možností:
> - **Určení chování na základě návratových kódů**
> - **Intune vynutí povinné restartování zařízení.**

Nastavte dostupnost aplikace na základě data a času požadované aplikace pomocí následujících kroků:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace**  >  **všechny aplikace**.
3. V seznamu **aplikace pro Windows (Win32)** vyberte aplikaci. 
4. V podokně aplikace vyberte **vlastnosti**  >  **Upravit** vedle oddílu **přiřazení** . Pak vyberte **Přidat skupinu** pod **požadovaným** typem přiřazení. 
   
   Všimněte si, že dostupnost aplikace se dá nastavit na základě typu přiřazení. Je možné **zadat typ přiřazení** **, který je** **k dispozici pro zaregistrovaná zařízení**nebo **odinstalovat**.
5. Vyberte skupinu v podokně **Vybrat skupinu** a určete tak, do které skupiny uživatelů se aplikace přiřadí. 

    > [!NOTE]
    > Mezi možnosti **typu přiřazení** patří následující:<br>
    > - **Požadováno**: můžete zvolit **nastavit tuto aplikaci jako povinnou pro všechny uživatele** nebo **nastavit tuto aplikaci jako povinnou na všech zařízeních**.<br>
    > - **K dispozici pro zaregistrovaná zařízení**: můžete vybrat možnost **zpřístupnit tuto aplikaci všem uživatelům se zaregistrovanými zařízeními**.<br>
    > - **Odinstalace**: můžete zvolit možnost **odinstalovat tuto aplikaci pro všechny uživatele** nebo **odinstalovat tuto aplikaci pro všechna zařízení**.

6. Chcete-li upravit možnosti **oznámení koncovým uživatelům** , vyberte možnost **Zobrazit všechna informační oznámení**.
7. V podokně **Upravit přiřazení** nastavte oznámení pro **uživatele Ender** , aby se **zobrazila všechna informační oznámení**. Všimněte si, že můžete nastavit **oznámení koncových uživatelů** a **Zobrazit všechna informační oznámení**, **Zobrazit informační zprávy pro restartování počítače**nebo **Skrýt všechna informační oznámení**.
8. Nastavte **Dostupnost aplikace** na **konkrétní datum a čas** a vyberte datum a čas. Toto datum a čas určují, kdy se aplikace stáhne do zařízení uživatele. 
9. Nastavte **konečný termín instalace aplikace** na **konkrétní datum a čas** a vyberte datum a čas. Toto datum a čas určují, kdy se aplikace nainstaluje na zařízení uživatele. Pokud se pro stejného uživatele nebo zařízení provede více než jedno přiřazení, bude čas konečného termínu instalace aplikace vyzvednut na základě nejdřívějšího možného času.

10. Vyberte **povoleno** v poli **období odkladu pro restartování**. Doba odkladu restartování se spustí hned po dokončení instalace aplikace v zařízení. Pokud je nastavení zakázané, zařízení se může bez upozornění restartovat. 

    Můžete přizpůsobit následující možnosti:
    
    - **Doba odkladu pro restartování zařízení (minuty)**: výchozí hodnota je 1 440 minut (24 hodin). Tato hodnota může být maximálně 2 týdny.
    - **Vyberte, kdy se má zobrazit dialogové okno odpočítávání před restartováním (minuty)**: výchozí hodnota je 15 minut.
    - **Dovolit uživateli odložit oznámení o restartování**: můžete vybrat **Ano** nebo **ne**.
        - **Vyberte dobu opakovaného přiložení (minuty)**: výchozí hodnota je 240 minut (4 hodiny). Hodnota pro odložení nemůže být větší než doba odkladu pro restartování.

11. Vyberte **zkontrolovat a uložit**.

## <a name="notifications-for-win32-apps"></a>Oznámení pro aplikace Win32 
V případě potřeby můžete potlačit zobrazování uživatelských oznámení na přiřazení aplikace. V Intune vyberte **aplikace**  >  **všechny aplikace**  >  *, které*  >  **přiřazení**aplikace  >  **zahrnuje skupiny**. 

> [!NOTE]
> Aplikace Win32 nainstalované prostřednictvím rozšíření pro správu Intune se odinstalují na nezaregistrovaných zařízeních. Správci můžou vyloučení přiřazení použít k tomu, aby nenabídli aplikace Win32 k převedení vlastních zařízení (BYOD).

## <a name="next-steps"></a>Další kroky

- Další informace o přidávání aplikací do Intune najdete v článku [Přidání aplikací do Microsoft Intune](apps-add.md).
