---
title: Kurz – nasazení Windows 10
titleSuffix: Configuration Manager
description: Kurz týkající se použití Desktop Analytics a Configuration Manager k nasazení Windows 10 do pilotní skupiny.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: tutorial
ms.assetid: 3e82cd96-0ce0-474a-a597-d65fceadc95a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: fc4309d3d09cd35c17b23bc46dcb1a28d210aa8e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125742"
---
# <a name="tutorial-deploy-windows-10-to-pilot"></a>Kurz: nasazení Windows 10 do pilotního nasazení

V tomto kurzu se používá Desktop Analytics a Configuration Manager k nasazení Windows 10 do pilotní skupiny. Zvýrazňuje integraci cloudové služby, aby poskytovala přehledy pro nasazení systému Windows s místním produktem. Pomocí Desktop Analytics můžete určit nejlepší zařízení, která se mají vložit do pilotní skupiny. Pak použijte Configuration Manager k získání aktuálního systému Windows.

V tomto kurzu se naučíte:  

> [!div class="checklist"]  
> * Nastavení analýzy desktopových analýz v Azure Portal  
> * Připojit Configuration Manager a nakonfigurovat nastavení zařízení  
> * Vytvoření plánu nasazení Desktop Analytics pro Windows 10  
> * Použití Configuration Manager k nasazení Windows 10 do pilotní skupiny  

Pokud ještě nemáte předplatné Azure, vytvořte si napřed [bezplatný účet](https://azure.microsoft.com/free). Když se správně nakonfiguruje, používání Desktop Analytics nenese žádné náklady na Azure.

Desktop Analytics používá *Log Analytics pracovní prostor* ve vašem předplatném Azure. Pracovní prostor je v podstatě kontejner, který obsahuje informace o účtu a jednoduché konfigurační informace. Další informace najdete v tématu [Správa pracovních prostorů](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json).



## <a name="prerequisites"></a>Požadavky

Než začnete s tímto kurzem, ujistěte se, že máte následující požadavky:  

- Aktivní předplatné Azure s oprávněními [**globálního správce**](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions)  

    Další informace najdete v tématu [požadavky na Desktop Analytics](overview.md#prerequisites).

- Configuration Manager verze 1902 s kumulativní aktualizací (4500571) nebo novější s rolí **úplného správce**  

- Instalační médium pro nejnovější verzi Windows 10

- Aspoň jedno zařízení s Windows 10 s následujícími konfiguracemi:  

    - Windows 10 verze 1709 nebo novější, ale menší než verze instalačních médií, které plánujete použít

    - Nejnovější aktualizace Windows 10 – kumulativní kvalita  

    - Configuration Manager klienta verze 1902 s kumulativní aktualizací (4500571) nebo novější  

- Schválení firmy pro konfiguraci úrovně diagnostických dat Windows na **volitelné (omezené)** na pilotních zařízeních  

    Další informace najdete v tématu [Ochrana osobních údajů Desktop Analytics](privacy.md).

- Síťové připojení ze zařízení k následujícím koncovým bodům Internetu:

    - `https://v10c.events.data.microsoft.com`  
    - `https://settings-win.data.microsoft.com`  
    - `http://adl.windows.com`  
    - `https://watson.telemetry.microsoft.com`  
    - `https://umwatsonc.events.data.microsoft.com`  
    - `https://ceuswatcab01.blob.core.windows.net`  
    - `https://ceuswatcab02.blob.core.windows.net`  
    - `https://eaus2watcab01.blob.core.windows.net`  
    - `https://eaus2watcab02.blob.core.windows.net`  
    - `https://weus2watcab01.blob.core.windows.net`  
    - `https://weus2watcab02.blob.core.windows.net`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://graph.windows.net`(jenom u Configuration Manager role serveru)
    - `https://*.manage.microsoft.com`(jenom u Configuration Manager role serveru)

    Další informace najdete v tématu [Povolení sdílení dat pro desktopovou analýzu](enable-data-sharing.md#endpoints).  

> [!Important]  
> Tyto požadavky jsou pro účely tohoto kurzu. Další informace o obecných požadavcích na Desktop Analytics s Configuration Manager najdete v tématu [požadavky](overview.md#prerequisites).  



## <a name="set-up-desktop-analytics"></a>Nastavení portálu Desktop Analytics

Pomocí tohoto postupu se můžete přihlásit k portálu Analytics a nakonfigurovat ho v předplatném. Tento postup představuje jednorázový proces pro nastavení analýzy plochy pro vaši organizaci.  

1. Otevřete [portál Desktop Analytics](https://aka.ms/desktopanalytics) v Microsoft 365 Správa zařízení jako uživatel s oprávněními **globálního správce** . Vyberte **Spustit**.  

2. Na stránce **přijmout licenční smlouvu** si přečtěte smlouvu o poskytování služeb a vyberte **přijmout**.  

3. Na stránce **potvrďte předplatné** jsou seznam požadovaných opravňujících licencí pro funkce stavu zařízení s Windows v Desktop Analytics. Pokračujte výběrem tlačítka **Další**.  

4. Na stránce **udělení přístupu uživatelům** :

    - **Umožněte službě Desktop Analytics spravovat role adresáře vaším jménem**: Desktop Analytics automaticky přiřadí **vlastníky pracovního prostoru** role **správce pro Desktop Analytics** . Pokud jsou tyto skupiny již **globálním správcem**, nedojde ke změně.  

        Pokud tuto možnost nevyberete, bude aplikace Desktop Analytics stále přidávat uživatele jako členy skupiny zabezpečení. **Globální správce** musí ručně přiřadit roli **správce Desktop Analytics** pro uživatele.  

        Další informace o přiřazení oprávnění role správce v Azure Active Directory a oprávnění přiřazená **správcům Desktop Analytics**najdete v tématu [oprávnění role správce v Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Pro vytváření a správu pracovních prostorů a plánů nasazení v nástroji Desktop Analytics předkonfiguruje skupinu zabezpečení **vlastníci pracovního prostoru** v Azure Active Directory. 

        Pokud chcete do skupiny přidat uživatele, zadejte jejich jméno nebo e-mailovou adresu do části **Zadejte jméno nebo e-mailovou adresu** . Po dokončení vyberte **Další**.

5. Na stránce **nastavte svůj pracovní prostor**:  

    > [!Note]  
    > K dokončení tohoto kroku potřebuje uživatel oprávnění **vlastníka pracovního prostoru** a další přístup k předplatnému Azure a skupině prostředků. Další informace najdete v tématu [předpoklady](overview.md#prerequisites).  

    - Vyberte své předplatné Azure.  

    - Pokud chcete použít existující pracovní prostor pro Desktop Analytics, vyberte ho a pokračujte dalším krokem.  

    - Pokud chcete vytvořit pracovní prostor pro Desktop Analytics, vyberte **Přidat pracovní prostor**.  

        1. Zadejte **název pracovního prostoru**.  

        2. V rozevíracím seznamu vyberte **název předplatného Azure pro tento pracovní prostor**a zvolte předplatné Azure pro tento pracovní prostor.  

        3. **Vytvořit nový** Skupinu prostředků nebo **použijte existující**.  

        4. Vyberte **oblast** ze seznamu a pak vyberte **Přidat**.  

6. Vyberte nový nebo existující pracovní prostor a pak vyberte **nastavit jako pracovní prostor Analytics pro stolní počítače**.  Pak v dialogovém okně **potvrzení a udělení přístupu** vyberte **pokračovat** .  

7. Na kartě nový prohlížeč vyberte účet, který se má použít k přihlášení. Vyberte možnost **souhlasu jménem vaší organizace** a vyberte **přijmout**.  


    > [!Note]  
    > Tímto souhlasem je přiřazení aplikace MALogAnalyticsReader k pracovnímu prostoru role čtecího modulu Log Analytics. Tato role aplikace je vyžadována analýzou plochy. Další informace najdete v tématu [aplikační role MALogAnalyticsReader](troubleshooting.md#bkmk_MALogAnalyticsReader).  

8. Zpátky na stránce **nastavte svůj pracovní prostor**tak, že vyberete **Další**.  

9. Na stránce **Poslední kroky** vyberte **Přejít na Desktop Analytics**. Azure Portal zobrazuje **domovskou** stránku nástroje Desktop Analytics.  



## <a name="connect-configuration-manager"></a>Připojení správce konfigurací

Pomocí tohoto postupu můžete aktualizovat Configuration Manager, připojit se k Desktop Analytics a nakonfigurovat nastavení zařízení. Tento postup je jednorázový proces, který umožňuje připojit vaši hierarchii ke cloudové službě.  

### <a name="update-configuration-manager"></a>Aktualizovat Configuration Manager

Pro podporu integrace s desktopovou analýzou nainstalujte Configuration Manager kumulativní aktualizace 1902 (4500571). Další informace o této aktualizaci najdete v tématu [kumulativní aktualizace pro Configuration Manager aktuální větev verze 1902](https://support.microsoft.com/help/4500571).

1. Aktualizujte lokalitu pomocí kumulativní aktualizace pro verzi 1902. Další informace najdete v tématu [instalace konzolových aktualizací](../core/servers/manage/install-in-console-updates.md).  

2. Aktualizujte klienty. Pro zjednodušení tohoto procesu zvažte použití automatického upgradu klienta. Další informace najdete v tématu [upgrade klientů](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  


### <a name="connect-to-the-service"></a>Připojit ke službě

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **služby Azure** . Na pásu karet vyberte **Konfigurovat služby Azure** .  

2. Na stránce **služby Azure** v Průvodci službami Azure nakonfigurujte následující nastavení:  

    - Zadejte **název** pro objekt v Configuration Manager  

    - Zadejte volitelný **Popis** , který vám usnadní identifikaci služby.  

    - Výběr funkce **Desktop Analytics** ze seznamu dostupných služeb  
  
   Vyberte **Další**.  

3. Na stránce **aplikace** vyberte příslušné **prostředí Azure**. Pak vyberte **Vyhledat** webovou aplikaci.

4. Vyberte **vytvořit** a snadno přidejte aplikaci Azure AD pro připojení Desktop Analytics.

5. V okně **vytvořit serverovou aplikaci** nakonfigurujte následující nastavení:  

    - **Název aplikace**: popisný název aplikace ve službě Azure AD.

    - **Adresa URL domovské stránky**: Tato hodnota není používána Configuration Manager, ale vyžaduje ji služba Azure AD. Ve výchozím nastavení touto hodnotou je `https://ConfigMgrService`.  

    - **Identifikátor URI ID aplikace**: Tato hodnota musí být v TENANTOVI Azure AD jedinečná. Je v přístupovém tokenu, který používá klient Configuration Manager k vyžádání přístupu ke službě. Ve výchozím nastavení touto hodnotou je `https://ConfigMgrService`.  

    - **Období platnosti tajného klíče**: v rozevíracím seznamu vyberte buď **1 rok** , nebo **2 roky** . Výchozí hodnota je jeden rok.  

    Vyberte **Sign in** (Přihlásit se). Po úspěšném ověření v Azure stránka zobrazuje **název tenanta Azure AD** pro referenci.

    > [!Note]  
    > Dokončete tento krok jako **globální správce**. Tyto přihlašovací údaje se Configuration Manager neukládají. Tento uživatel nevyžaduje oprávnění v Configuration Manager a nemusí být stejný účet, který spouští Průvodce službami Azure.  

    Vyberte **OK** a vytvořte webovou aplikaci ve službě Azure AD a zavřete dialogové okno vytvořit serverovou aplikaci. V dialogu aplikace serveru vyberte **OK**. Pak na stránce aplikace v Průvodci službami Azure vyberte **Další** .  

6. Na stránce **diagnostická data** nakonfigurujte následující nastavení:  

    - **Komerční ID**: Tato hodnota by se měla automaticky naplnit ID vaší organizace.  

    - **Windows 10 úroveň diagnostických dat**: vyberte aspoň **volitelné (omezené)** .  

    - **Povolit název zařízení v diagnostických datech**: vyberte **Povolit** .  
  
   Vyberte **Další**. Stránka **dostupné funkce** zobrazuje funkce Desktop Analytics, která je dostupná s nastavením diagnostických dat z předchozí stránky. Vyberte **Další**.  

7. Na stránce **kolekce** nakonfigurujte následující nastavení:  

    - **Zobrazovaný název**: portál Analytics pro stolní počítače zobrazuje toto Configuration Manager připojení pomocí tohoto názvu. Slouží k odlišení různých hierarchií. Například *testovací prostředí* nebo *produkce*.  

    - **Cílová kolekce**: Tato kolekce zahrnuje všechna zařízení, která Configuration Manager nakonfigurují pomocí nastavení komerčního ID a dat diagnostiky. Je to celá sada zařízení, která Configuration Manager se připojují ke službě Desktop Analytics.  

    - **Zařízení v cílové kolekci používají pro odchozí komunikaci uživatelem ověřený proxy server**: ve výchozím nastavení je tato hodnota **ne**. V případě potřeby v prostředí nastavte na **Ano**.  

    - **Vyberte konkrétní kolekce, které se mají synchronizovat s desktopovou analýzou**: Pokud chcete zahrnout další kolekce, vyberte **Přidat** . Tyto kolekce jsou k dispozici na portálu Desktop Analytics pro seskupení s plány nasazení. Nezapomeňte zahrnout pilotní a pilotní kolekce.  

        Tyto kolekce se budou i nadále synchronizovat se změnami členství. Například plán nasazení používá kolekci s pravidlem členství v systému Windows 7. Když se tato zařízení upgradují na Windows 10 a Configuration Manager vyhodnotí členství v kolekci, odfiltrují se tato zařízení z plánu shromažďování a nasazení.  

8. Dokončete průvodce.  

Configuration Manager vytvoří zásadu nastavení pro konfiguraci zařízení v cílové kolekci. Tato zásada zahrnuje nastavení diagnostických dat, která umožňují zařízením odesílat data společnosti Microsoft. Ve výchozím nastavení klienti aktualizují zásady každou hodinu. Po přijetí nového nastavení může trvat několik hodin, než budou data dostupná v Desktop Analytics.

> [!Note]  
> Další informace o těchto nastaveních naleznete v tématu [nastavení systému Windows](enroll-devices.md#windows-settings).  

Monitorujte konfiguraci zařízení pro desktopovou analýzu. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte uzel **Údržba Desktop Analytics** a vyberte řídicí panel **stav připojení** .  

Configuration Manager synchronizuje vaše kolekce do 60 minut od vytvoření připojení. Na portálu Analytics pro stolní počítače přejděte na **Global pilot**a podívejte se na vaše kolekce zařízení Configuration Manager. Na zbývajících částech portálu může trvat dva až tři dny, než se zobrazí kompletní data. Další informace najdete v tématu [latence dat](troubleshooting.md#data-latency).

## <a name="create-a-desktop-analytics-deployment-plan"></a>Vytvoření plánu nasazení Desktop Analytics

Pomocí tohoto postupu můžete vytvořit plán nasazení v Desktop Analytics.

1. Otevřete [portál Desktop Analytics](https://aka.ms/desktopanalytics). Používejte přihlašovací údaje, které mají alespoň oprávnění **přispěvatelé v pracovním prostoru** .  

2. Ve skupině spravovat vyberte **plány nasazení** .  

3. V podokně **plány nasazení** vyberte **vytvořit**.  

4. V podokně **vytvořit plán nasazení** nakonfigurujte následující nastavení:  

    - **Název**: jedinečný název plánu nasazení, například`Windows 10 pilot`  

    - **Produkty a verze**: vyberte verzi Windows 10, kterou chcete nasadit. Microsoft doporučuje vytvářet plány nasazení, které používají nejnovější verzi.

    - **Skupiny zařízení**: vyberte jednu nebo víc skupin na kartě Configuration Manager a pak vyberte **nastavit jako cílové skupiny**. Tyto skupiny jsou kolekce synchronizované z Configuration Manager.  

    - **Pravidla připravenosti**: Tato pravidla vám pomůžou určit, která zařízení jsou opravňující k upgradu. Vyberte **operační systém Windows** a nakonfigurujte následující nastavení:  

        - Tyto **počítače automaticky získávají ovladače z web Windows Update**: výchozí nastavení je **vypnuté**, což se doporučuje při nasazení pomocí Configuration Manager.  

        - **Pro vaše aplikace definujte prahovou hodnotu pro minimální počet instalací**: výchozí nastavení je `2%` . Aplikace, které jsou pod touto prahovou hodnotou, se automaticky nastaví na *počet málo instalací*. Desktop Analytics neověřuje tyto doplňky během pilotního nasazení.  

            Pokud je aplikace nainstalovaná na vyšší procento počítačů, než je tato prahová hodnota, plán nasazení označí aplikaci jako *zajímavosti*. Pak se můžete rozhodnout, že jeho důležitost budete testovat během pilotní fáze.  

    - **Datum dokončení**: vyberte datum, kdy má být systém Windows plně nasazen do všech cílových zařízení.  

5. Vyberte **Vytvořit**. Nový plán se zobrazí v seznamu plánů nasazení během zpracování. Pro urychlení zpracování si vyžádejte aktualizaci dat na vyžádání. Další informace najdete v tématu [Nejčastější dotazy k Desktop Analytics](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

6. Kliknutím na název otevřete plán nasazení.  

7. V nabídce plán nasazení vyberte ve skupině **Příprava** možnost **identifikovat důležitost**.  

    1. Na kartě **aplikace** vyberte možnost Zobrazit pouze **neprověřené** prostředky.  

    2. Vyberte každou aplikaci a pak vyberte **Upravit**. Můžete vybrat více než jednu aplikaci, kterou chcete upravit současně.  

    3. V seznamu **důležitost** vyberte úroveň důležitosti. Pokud chcete, aby aplikace Desktop Analytics ověřila aplikaci v rámci pilotního projektu, vyberte **kritické** nebo **důležité**. Neověřuje aplikace označené jako **nedůležité**. Při přiřazování úrovní důležitosti posuďte informace o [kompatibilitě](compat-assessment.md) a dalších plánech.  

        Při přiřazování úrovní důležitosti můžete také zvolit rozhodnutí o upgradu.  

    4. Po dokončení vyberte **Uložit** .  

8. V nabídce plán nasazení vyberte ve skupině **připravit** možnost **identifikovat pilotní projekt**.  

    1. Přečtěte si doporučené zařízení pro pilotní nasazení.  

    2. Vyberte jednotlivá zařízení a vyberte **Přidat do pilotního nasazení**. Pokud nesouhlasím s doporučením, vyberte **nahradit**.  

        Pokud chcete získat další informace o tom, jak tato doporučení využívá funkce Desktop Analytics, vyberte ikonu informace v pravém horním rohu podokna **určení pilotního projektu** .



## <a name="deploy-windows-10-in-configuration-manager"></a>Nasazení Windows 10 v Configuration Manager

Pomocí tohoto postupu můžete nasadit Windows 10 v Configuration Manager do pilotní skupiny.

- Pokud ho ještě nemáte, [vytvořte nejdřív balíček s upgradem operačního systému pro Windows 10](#bkmk_create-package) .  

- Pokud ho ještě nemáte, [Vytvořte pořadí úkolů upgradu operačního systému pro Windows 10](#bkmk_create-ts) .  

- [Nasazení pořadí úkolů](#bkmk_deploy-ts) pomocí plánu nasazení Desktop Analytics  

- [Instalace pořadí úkolů](#bkmk_install-ts) z centra softwaru na cílovém zařízení  

<!-- 
- [Monitor](#bkmk_monitor-ts) status in Configuration Manager  
 -->

### <a name="create-an-os-upgrade-package-for-windows-10"></a><a name="bkmk_create-package"></a>Vytvoření balíčku pro upgrade operačního systému pro Windows 10

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a potom vyberte uzel **balíčky s upgradem operačního systému** .  

2. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte možnost **Přidat balíček s upgradem operačního systému**. Tato akce spustí Průvodce přidáním upgradu operačního systému.  

3. Na stránce **zdroj dat** zadejte síťovou **cestu** k instalačním zdrojovým souborům balíčku s upgradem operačního systému. Například, `\\server\share\path`.  

    > [!NOTE]  
    > Zdrojové instalační soubory obsahují setup.exe a další soubory a složky pro instalaci operačního systému.  

4. Na stránce **Obecné** zadejte jedinečný **název** balíčku upgradu operačního systému.  

5. Dokončete Průvodce přidáním balíčku s upgradem operačního systému.  

#### <a name="distribute-content"></a>Distribuovat obsah

Dále distribuujte balíček s upgradem operačního systému do distribučních bodů.  

1. V seznamu vyberte balíček s upgradem operačního systému. Na kartě **Domů** na pásu karet ve skupině **nasazení** vyberte možnost **distribuovat obsah**. Otevře se Průvodce distribucí obsahu.  

2. Na stránce **Obecné** ověřte, že uvedený obsah je obsah, který chcete distribuovat, a pak vyberte **Další**.  

3. Na stránce **cíl obsahu** vyberte možnost **Přidat**a zvolte možnost **distribuční bod**. Vyberte existující distribuční bod a pak vyberte **OK**. Po dokončení přidávání umístění obsahu vyberte možnost **Další**.  

4. Dokončete Průvodce distribucí obsahu.  


### <a name="create-an-os-upgrade-task-sequence-for-windows-10"></a><a name="bkmk_create-ts"></a>Vytvoření pořadí úkolů upgradu operačního systému pro Windows 10

1. V konzole Configuration Manager klikněte na pracovní prostor **softwarová knihovna** , rozbalte možnost **operační systémy**a pak vyberte **pořadí úloh**.  

2. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte **vytvořit pořadí úloh**.  

3. Na stránce **vytvořit novou sekvenci úloh** v Průvodci vytvořením pořadí úloh vyberte možnost **upgradovat operační systém z balíčku pro upgrade**a pak vyberte možnost **Další**.  

4. Na stránce **informace o pořadí úloh** zadejte **název pořadí úkolů** , který identifikuje pořadí úkolů.  

5. Na stránce **upgrade operačního systému Windows** zadejte následující nastavení a potom vyberte **Další**:  

    - **Balíček s upgradem**: Zadejte balíček pro upgrade, který obsahuje zdrojové soubory upgradu operačního systému.  

    - **Index edice**: Pokud je v balíčku k dispozici více indexů OS Edition, vyberte požadovaný index edice. Ve výchozím nastavení Průvodce vybere první index.  

    - **Kód Product Key**: zadejte kód Product Key systému Windows pro operační systém, který chcete nainstalovat. Zadejte kódované klíče multilicencí nebo standardní kódy Product Key. Pokud používáte standardní kód Product Key, oddělte každou skupinu o pět znaků pomlčkou (-). Příklad: *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*. Pokud je upgrade pro multilicenční edici, nemusí se kód Product Key vyžadovat.  

        > [!Note]  
        > Tento kód Product Key může být klíč k vícenásobné aktivaci (MAK) nebo obecný multilicenční klíč (GVLK). GVLK se také označuje jako klíč pro nastavení klienta služby správy klíčů (KMS). Další informace najdete v tématu [plánování aktivace multilicence](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Seznam klíčů pro instalaci klienta služby správy klíčů najdete v [příloze a](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) v příručce k aktivaci Windows serveru.

6. Na stránce **Zahrnout aktualizace** vyberte možnost **Další** a neinstalujte žádné aktualizace softwaru.  

7. Na stránce **instalovat aplikace** vyberte možnost **Další** a neinstalujte žádné aplikace.

8. Dokončete Průvodce vytvořením pořadí úloh.  


### <a name="deploy-the-task-sequence-using-the-desktop-analytics-deployment-plan"></a><a name="bkmk_deploy-ts"></a>Nasazení pořadí úkolů pomocí plánu nasazení Desktop Analytics

1. V konzole Configuration Manager klikněte na **Knihovna softwaru**, rozbalte položku **Údržba Desktop Analytics**a vyberte uzel **plány nasazení** .  

2. Vyberte plán nasazení pilotního nasazení Windows 10 a pak na pásu karet vyberte **podrobnosti plánu nasazení** .  

3. Na dlaždici **stav pilotního stavu** zvolte v rozevíracím seznamu **pořadí úloh** a pak vyberte **nasadit**.  

4. Na stránce **Obecné** v nástroji Průvodce nasazením softwaru vyberte možnost **Procházet** vedle pole **software** . Vyberte pořadí úkolů místního upgradu Windows 10 a vyberte **Další**.  

    > [!Note]  
    > Při integraci Desktop Analytics Configuration Manager pro plán nasazení automaticky vytvoří pilotní a produkční kolekce. Než je můžete použít, může trvat i čas, než se tyto kolekce synchronizují. Další informace najdete v tématu [řešení potíží – latence dat](troubleshooting.md#data-latency).<!-- 4984639 -->
    >
    > Tato kolekce je vyhrazena pro zařízení plánu nasazení Desktop Analytics. Ruční změny této kolekce se nepodporují.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Na stránce **obsah** vyberte **Přidat**a potom vyberte **distribuční bod**. Vyberte dostupný distribuční bod pro hostování obsahu instalace a vyberte **OK**. Pak vyberte **Další**.  

6. Na stránce **nastavení nasazení** kliknutím na tlačítko **Další** přijměte výchozí nastavení. (Dostupná instalace)  

7. Kliknutím na tlačítko **Další** na stránce **plánování** přijměte výchozí nastavení. (K dispozici co nejdříve.)  

8. Na stránce **činnost koncového uživatele** výběrem možnosti **Další** přijměte výchozí nastavení. (Zobrazit v centru softwaru a zobrazovat pouze oznámení o restartování počítače.)  

9. Na stránce **výstrahy** výběrem možnosti **Další** přijměte výchozí nastavení.  

10. Dokončete průvodce.  


### <a name="install-the-task-sequence-from-software-center"></a><a name="bkmk_install-ts"></a>Instalace pořadí úkolů z centra softwaru

1. Přihlaste se k zařízení, které je členem plánu pilotního nasazení.  

2. Otevřete **Centrum softwaru** a nainstalujte operační systém, který je k dispozici pro Windows 10.  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>Další kroky

V dalším článku se dozvíte víc o plánech nasazení Desktop Analytics.
> [!div class="nextstepaction"]  
> [Plány nasazení](about-deployment-plans.md)
