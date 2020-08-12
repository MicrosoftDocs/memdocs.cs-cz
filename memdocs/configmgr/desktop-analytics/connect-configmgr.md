---
title: Připojení správce konfigurací
titleSuffix: Configuration Manager
description: Návod, jak připojit Configuration Manager s desktopovou analýzou
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 7015ab4c180ed56b00149ffbff99c9e5a8112e95
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125997"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>Postup připojení Configuration Manager s desktopovou analýzou

Desktop Analytics je úzce integrovaný s Configuration Manager. Nejdřív se ujistěte, že je lokalita aktuální, aby podporovala nejnovější funkce. Pak vytvořte připojení k Desktop Analytics v Configuration Manager. Nakonec Monitorujte stav připojení.

## <a name="update-the-site"></a><a name="bkmk_hotfix"></a>Aktualizace webu

Nejdřív se ujistěte, že na webu Configuration Manager běží aspoň verze 1902. Další informace najdete v tématu [instalace konzolových aktualizací](../core/servers/manage/install-in-console-updates.md).

Pro podporu integrace s Desktop Analytics je taky potřeba nainstalovat kumulativní aktualizaci 1902 (4500571) verze. Další informace o této aktualizaci najdete v tématu [kumulativní aktualizace pro Configuration Manager aktuální větev verze 1902](https://support.microsoft.com/help/4500571).

1. Aktualizujte lokalitu pomocí kumulativní aktualizace pro verzi 1902. Další informace najdete v tématu [instalace konzolových aktualizací](../core/servers/manage/install-in-console-updates.md).

2. Aktualizujte klienty. Pro zjednodušení tohoto procesu zvažte použití automatického upgradu klienta. Další informace najdete v tématu [upgrade klientů](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).

## <a name="connect-to-the-service"></a><a name="bkmk_connect"></a>Připojit ke službě

> [!TIP]
> Před spuštěním průvodce vytvořte cílovou kolekci uvedenou v kroku 8, protože po jejím spuštění nemůžete vybrat možnost mimo průvodce.

Pomocí tohoto postupu můžete připojit Configuration Manager ke službě Desktop Analytics a nakonfigurovat nastavení zařízení. Tento postup je jednorázový proces, který umožňuje připojit vaši hierarchii ke cloudové službě.

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **služby Azure** . Na pásu karet vyberte **Konfigurovat služby Azure** .

    > [!TIP]
    > Připojte se ke službě přímo z uzlu **údržby Desktop Analytics** . V konzole Configuration Manager klikněte na pracovní prostor **softwarová knihovna** a vyberte uzel **Údržba Desktop Analytics** . V poli *Nový pro Desktop Analytics* vyberte druhý odkaz pro *připojení Configuration Manager ke službě Desktop Analytics*.

2. Na stránce **služby Azure** v Průvodci službami Azure nakonfigurujte následující nastavení:

    - Zadejte **název** objektu v Configuration Manager.

    - Zadejte volitelný **Popis** , který vám usnadní identifikaci služby.

    - V seznamu dostupných služeb vyberte možnost **Analýza plochy** .

   Vyberte **Další**.

3. Na stránce **aplikace** vyberte příslušné **prostředí Azure**. Pak vyberte **Vyhledat** webovou aplikaci.

4. Pokud máte existující aplikaci, kterou chcete pro tuto službu znovu použít, vyberte ji ze seznamu a vyberte **OK**.

5. Ve většině případů můžete vytvořit aplikaci pro připojení Desktop Analytics pomocí tohoto průvodce. Vyberte **Vytvořit**.<!-- 3572123 -->

    > [!TIP]
    > Pokud nemůžete vytvořit aplikaci pomocí tohoto průvodce, můžete aplikaci vytvořit ručně v Azure AD a pak ji naimportovat do Configuration Manager. Další informace najdete v tématu [Vytvoření a import aplikace pro Configuration Manager](troubleshooting.md#create-and-import-app-for-configuration-manager).

6. V okně **vytvořit serverovou aplikaci** nakonfigurujte následující nastavení:

    - **Název aplikace**: popisný název aplikace ve službě Azure AD.

    - **Adresa URL domovské stránky**: Tato hodnota není používána Configuration Manager, ale vyžaduje ji služba Azure AD. Ve výchozím nastavení touto hodnotou je `https://ConfigMgrService`.

    - **Identifikátor URI ID aplikace**: Tato hodnota musí být v TENANTOVI Azure AD jedinečná. Je v přístupovém tokenu, který používá klient Configuration Manager k vyžádání přístupu ke službě. Ve výchozím nastavení touto hodnotou je `https://ConfigMgrService`.

    - **Období platnosti tajného klíče**: v rozevíracím seznamu vyberte buď **1 rok** , nebo **2 roky** . Výchozí hodnota je jeden rok.

    Vyberte **Přihlásit se** . Po úspěšném ověření v Azure stránka zobrazuje **název tenanta Azure AD** pro referenci.

    > [!NOTE]
    > Dokončete tento krok jako **globální správce**. Tyto přihlašovací údaje se Configuration Manager neukládají. Tento uživatel nevyžaduje oprávnění v Configuration Manager a nemusí být stejný účet, který spouští Průvodce službami Azure.

    Vyberte **OK** a vytvořte webovou aplikaci ve službě Azure AD a zavřete dialogové okno vytvořit serverovou aplikaci. V dialogu aplikace serveru vyberte **OK**. Pak na stránce aplikace v Průvodci službami Azure vyberte **Další** .

7. Na stránce **diagnostická data** nakonfigurujte následující nastavení:

    - **Komerční ID**: Tato hodnota by se měla automaticky naplnit ID vaší organizace. Pokud ne, ujistěte se, že je proxy server nakonfigurovaná tak, aby umožňovala všem požadovaným [koncovým bodům](enable-data-sharing.md#endpoints) znovu pokračovat. Případně můžete komerční ID načíst ručně z [portálu Desktop Analytics](monitor-connection-health.md#bkmk_ViewCommercialID).

    - **Úroveň diagnostických dat Windows 10**: vyberte aspoň **požadované**. Další informace najdete v tématu [úrovně diagnostických dat](enable-data-sharing.md#diagnostic-data-levels).

        > [!TIP]
        > V Configuration Manager verze 2002 a starší se tato hodnota nazývala **Basic**.<!-- 7363467 -->

    - **Povolit název zařízení v diagnostických datech**: vyberte **Povolit** .

        > [!NOTE]
        > Počínaje systémem Windows 10 verze 1803 se název zařízení ve výchozím nastavení neposílá společnosti Microsoft. Pokud název zařízení neodešlete, zobrazí se v nástroji Desktop Analytics jako "Neznámý". Díky tomuto chování může být obtížné identifikovat a vyhodnocovat zařízení.

   Vyberte **Další**. Stránka **dostupné funkce** zobrazuje funkce Desktop Analytics, která je dostupná s nastavením diagnostických dat z předchozí stránky. Kliknutím na tlačítko **Další** můžete pokračovat nebo můžete provést změny v **předchozí** .

    ![Příklad stránky dostupné funkce v Průvodci službami Azure](media/available-functionality.png)

<a name="bkmk_Collections"></a>

8. Na stránce **kolekce** nakonfigurujte následující nastavení:

    - **Zobrazovaný název**: portál Analytics pro stolní počítače zobrazuje toto Configuration Manager připojení pomocí tohoto názvu. Použijte ho k odlišení různých hierarchií a k identifikaci kolekcí z oddělených hierarchií. Pomocí podmínek můžete snadno odlišit více hierarchií ve vašem prostředí, například *testovací prostředí* nebo *produkci*.

    - **Cílová kolekce**: Tato kolekce zahrnuje všechna zařízení, která Configuration Manager nakonfigurují pomocí nastavení komerčního ID a dat diagnostiky. Je to celá sada zařízení, která Configuration Manager se připojují ke službě Desktop Analytics.

    - **Zařízení v cílové kolekci používají pro odchozí komunikaci uživatelem ověřený proxy server**: ve výchozím nastavení je tato hodnota **ne**. V případě potřeby v prostředí nastavte na **Ano**.

    - **Vyberte konkrétní kolekce, které se mají synchronizovat s desktopovou analýzou**: Pokud chcete zahrnout další kolekce z hierarchie **cílové kolekce** , vyberte **Přidat** . Tyto kolekce jsou k dispozici na portálu Desktop Analytics pro seskupení s plány nasazení. Nezapomeňte zahrnout pilotní a pilotní kolekce.  <!-- 4097528 -->

        > [!TIP]
        > V okně vybrat kolekce se zobrazí pouze kolekce, které jsou omezeny **cílovou kolekcí**.
        >
        > V následujícím příkladu jako cílovou kolekci vyberete Collection. Když pak přidáte další kolekce, uvidíte Collections, CollectionB a CollectionC. Nelze přidat kolekci.
        >
        > - Kolekce: omezeno kolekcí **všechny systémy**
        >     - CollectionB: omezeno kolekcí
        >         - CollectionC: omezeno na CollectionB
        > - Kolekce: omezeno kolekcí **všech systémů**
        >
        > Pokud chcete spravovat kolekce dostupné na portálu pro Desktop Analytics za účelem seskupení s plány nasazení, v konzole Configuration Manager klikněte na pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **služby Azure** . Vyberte položku přidruženou ke službě Azure **Analytics pro stolní počítače** a aktualizujte nastavení na stránce **kolekce Desktop Analytics** .

        > [!IMPORTANT]
        > Tyto kolekce se budou i nadále synchronizovat se změnami členství. Vaše cílová kolekce například používá kolekci s pravidlem členství systému Windows 7. Když se tato zařízení upgradují na Windows 10 a Configuration Manager vyhodnotí členství v kolekci, odfiltrují se tato zařízení z analýz kolekce a plochy.

9. Dokončete průvodce.

Configuration Manager vytvoří zásadu nastavení pro konfiguraci zařízení v cílové kolekci. Tato zásada zahrnuje nastavení diagnostických dat, která umožňují zařízením odesílat data společnosti Microsoft. Ve výchozím nastavení klienti aktualizují zásady každou hodinu. Po přijetí nového nastavení může trvat několik hodin, než budou data dostupná v Desktop Analytics.

## <a name="monitor-connection-health"></a><a name="bkmk_monitor"></a>Monitorování stavu připojení

Monitorujte konfiguraci zařízení pro desktopovou analýzu. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte uzel **Údržba Desktop Analytics** a vyberte řídicí panel **stav připojení** .

Další informace najdete v tématu [monitorování stavu připojení](monitor-connection-health.md).

Configuration Manager synchronizuje vaše kolekce do 60 minut od vytvoření připojení. Na portálu Analytics pro stolní počítače přejděte na**Global pilot**a podívejte se na vaše kolekce zařízení Configuration Manager.

> [!NOTE]
> Připojení Configuration Manager k Desktop Analytics se spoléhá na spojovací bod služby. Změny této role systému lokality mohou mít vliv na synchronizaci s cloudovou službou. Další informace najdete v tématu [o spojovacím bodu služby](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move).

## <a name="next-steps"></a>Další kroky

Přejděte k dalšímu článku, který zaregistruje zařízení do Desktop Analytics.
> [!div class="nextstepaction"]
> [Registrovat zařízení](enroll-devices.md)
