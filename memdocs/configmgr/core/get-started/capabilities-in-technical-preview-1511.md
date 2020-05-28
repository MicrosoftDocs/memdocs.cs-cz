---
title: Možnosti ve verzi Technical Preview 1511
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview pro Configuration Manager verze 1511.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 69473706-21b3-498b-a67e-670fdc988f0d
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 337b494bdce24463c19dd22ae975af5e99d6d895
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905848"
---
# <a name="capabilities-in-technical-preview-1511-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1511 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1511. Tato verze je základní instalace pro verzi Technical Preview, kterou můžete použít k instalaci nového webu Technical Preview nebo k upgradu ze starší verze Technical Preview.   Před instalací této verze Technical Preview si Projděte úvodní téma, [Technical Preview pro Configuration Manager](technical-preview.md), abyste se seznámili se základními požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.  

V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.  

##  <a name="integration-with-windows-update-for-business-in-windows-10"></a><a name="BKMK_WUfB"></a>Integrace s web Windows Update pro firmy ve Windows 10  
 Configuration Manager teď má možnost odlišit počítač s Windows 10, který je přímo připojený přes web Windows Update pro firmy (WUfB), oproti těm, které jsou připojené ke službě WSUS pro získání aktualizací a upgradů Windows 10.  Pro počítače připojené přes WUfB je možné aktualizace a upgrady spravovat na tempo sady správcem prostřednictvím zásad skupiny nebo zásad správy mobilních zařízení. tyto aktualizace a upgrady je možné nainstalovat přímo z WUfB.    
Pro počítače připojené přes WUfB nebude Configuration Manager moci ohlásit stav dodržování předpisů (včetně aktualizací Windows nebo aktualizací definic). Configuration Manager také nebudou moci na tyto počítače nasadit aktualizace společnosti Microsoft nebo aktualizace třetích stran.  

 **Předpoklady pro tento scénář:**  

-   Windows 10 Desktop pro nebo Windows 10 Enterprise Edition verze 1511 nebo novější  

-   Počítače určené ke správě prostřednictvím [Windows Update for Business](https://docs.microsoft.com/windows/deployment/update/waas-manage-updates-wufb)  

### <a name="try-it-out"></a>Určitě to udělejte!  
 Zkuste dokončit následující úlohu a pak použijte informace o zpětné vazbě v horní části tohoto tématu a sdělte nám, jak se pracovalo:  

1.  Zakažte Agenta Windows Update, aby nemohl skenovat WSUS, pokud byl dřív povolen.   
    Klíč registru **HKEY_LOCAL_MACHINE \software\policies\microsoft\windows\windowsupdate\au\usewsusserver** lze nastavit tak, aby označoval, zda počítač kontroluje službu WSUS nebo web Windows Update.  Pokud je hodnota 2, neprovádí se skenování na serveru WSUS.  

2.  Poznamenejte si nový atribut **UseWUServer**pod uzlem **web Windows Update** v Configuration Manager Průzkumník prostředků.  

3.  Vytvořte kolekci na základě atributu **UseWUServer** pro všechny počítače, které jsou pro aktualizace a upgrady připojené přes WUfB.  

4.  Vytvořte nastavení agenta klienta, které zakazuje pracovní postup aktualizace softwaru, a nasaďte toto nastavení do kolekce počítačů, které jsou připojené přímo k WUfB.  

5.  Počítače, které jsou spravovány přes WUfB, budou ve stavu dodržování předpisů zobrazovat **Neznámý** a nebudou se počítat jako součást celkového procenta dodržování předpisů.  

##  <a name="managing-office-365-proplus-client-update-through-configuration-manager"></a><a name="BKMK_Office365ProPlus"></a>Správa aktualizace klienta Office 365 ProPlus pomocí Configuration Manager  
 Configuration Manager teď má možnost spravovat aktualizace desktopových klientů Office 365 pomocí pracovního postupu Configuration Manager Software Update Management.    
Když společnost Microsoft publikuje novou aktualizaci klienta Office 365 pro stolní počítače do služby Windows Server Update Services (WSUS), Configuration Manager bude moci synchronizovat aktualizaci do katalogu, pokud je aktualizace Office 365 nakonfigurovaná tak, aby byla součástí synchronizace katalogu.  Server lokality Configuration Manager stáhne aktualizace klienta Office 365 a distribuuje balíček do Configuration Manager distribučních bodů.  Klient Configuration Manager pak bude informovat klienty pro stolní počítače Office 365, kde mají získat aktualizace a kdy se má spustit proces instalace aktualizace.  

**Předpoklady pro tento scénář:**  

### <a name="try-it-out"></a>Určitě to udělejte!  
 Zkuste dokončit následující úlohu a pak použijte informace o zpětné vazbě v horní části tohoto tématu a sdělte nám, jak se pracovalo:  

1. Aktualizace sady Office 365 můžete synchronizovat se serverem lokality Configuration Manager a zobrazit je v konzole Configuration Manager.  

2. Aktualizace Office 365 můžete schvalovat a úspěšně nasazovat.  

3. Aktualizace Office 365 můžete stáhnout a úspěšně aktualizovat pro klienty.  

4. Dodržování předpisů pro aktualizace Office 365 můžete ověřit pomocí v konzole monitorování nebo sestavy.  

   Podrobný postup najdete v tématu [Správa aktualizací klientů Office 365 pomocí Configuration Manager Technical Preview](https://docs.microsoft.com/deployoffice/manage-microsoft-365-apps-updates-configuration-manager).  

##  <a name="support-for-sql-server-alwayson-for-highly-available-databases"></a><a name="BKMK_AlwasyOn"></a>Podpora SQL Server AlwaysOn pro vysoce dostupné databáze  
 Configuration Manager teď podporuje používání skupin dostupnosti SQL Server AlwaysOn k hostování databáze lokality.  Když nainstalujete novou lokalitu, můžete nastavit, aby se místo normální instance SQL Server používala Skupina dostupnosti.  

> [!NOTE]  
>  Úspěšná konfigurace a použití skupin dostupnosti vyžaduje, abyste byli obeznámeni s konfigurací SQL Server skupin dostupnosti a spoléhá na dokumentaci a postupy uvedené v knihovně dokumentace SQL Server.  

Mezi procesy vysoké úrovně konfigurace a používání skupin dostupnosti patří:  

1.  Nakonfigurujte skupinu dostupnosti v SQL Server.  

2.  Nainstalujte novou Configuration Manager lokalitu a během instalace nasměrujte lokalitu tak, aby používala skupinu dostupnosti, zadáním koncového bodu skupin.  

**Předpoklady pro tento scénář:**  

-   Vyžaduje verzi SQL Server podporovanou Configuration Manager Technical Preview.  

-   Před instalací nástroje je nutné vytvořit a nakonfigurovat skupinu dostupnosti SQL Server Configuration Manager  

-   Skupina dostupnosti musí mít jednu primární repliku a dál může mít až dvě synchronní sekundární repliky.  

-   Skupina dostupnosti musí mít aspoň jeden koncový bod.  

-   Musíte mít síťové umístění, ke kterému má každý SQL Server ve skupině dostupnosti přístup. Toto umístění používá instalační program při konfiguraci skupiny dostupnosti a po dokončení instalace je možné ho odebrat.  

**Známé problémy této verze:**  

-   Nelze úspěšně přidat nového člena repliky do skupiny dostupnosti, která je již používána jako databáze lokality. Místo toho je nutné lokalitu po přidání nového člena repliky přeinstalovat.  

-   V tomto scénáři může být nutné nainstalovat **nativního klienta SQL Server 2012** ([ze sady SQL Server 2012 Feature Pack](https://www.microsoft.com/download/details.aspx?id=29065)) na serveru bodu správy. Tím zabráníte chybám připojení SQL (které se protokolují v **MP_GetAuth. log** na serveru bodu správy).  

### <a name="try-it-out"></a>Určitě to udělejte!  
Zkuste provést následující úkoly a pak použijte informace o zpětné vazbě v horní části tohoto tématu a sdělte nám, jak se pracovali:  

-   Můžu nainstalovat primární lokalitu, která používá databázový server nakonfigurovaný pro SQL Skupiny dostupnosti AlwaysOn  

-   Převzetí služeb při selhání skupiny dostupnosti SQL AlwaysOn pro novou repliku ve skupině se podařilo a primární lokalita je stále funkční.  

### <a name="configuring-sql-server-alwayson-for-configuration-manager"></a>Konfigurace SQL Server AlwaysOn pro Configuration Manager  
 Pomocí následujících postupů nejprve vytvořte a nakonfigurujte skupinu dostupnosti a pak nainstalujte novou Configuration Manager lokalitu, která používá skupinu dostupnosti.  

#### <a name="to-create-a-sql-server-alwayson-availability-group"></a>Vytvoření skupiny dostupnosti SQL Server AlwaysOn  
Proces [Vytvoření skupiny dostupnosti SQL Server](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server?view=sql-server-ver15) je popsán v knihovně dokumentace SQL Server.  Při vytváření skupiny dostupnosti zajistěte splnění následujících požadavků pro použití s Configuration Manager:  

-   Maximálně tři členy:  

    -   Jedna primární replika a až dvě sekundární repliky  

    -   Sekundární repliky musí být synchronní.  

        > [!TIP]  
        >  Doporučujeme, aby sekundární repliky byly nakonfigurované jen pro čtení. To vám umožní používat sekundární repliku pro funkce, jako je vytváření sestav, a přitom zachovat výkon primární repliky pro operace lokality.  

-   Nejméně jeden koncový bod. Virtuální název tohoto koncového bodu se použije při instalaci Configuration Manager lokality.  

    > [!TIP]  
    >  I když skupina může obsahovat více koncových bodů, Configuration Manager může využít pouze jeden.  

#### <a name="to-install-a-configuration-manager-site-that-uses-the-availability-group"></a>Instalace lokality Configuration Manager, která používá skupinu dostupnosti  
Chcete-li nainstalovat lokalitu, která používá skupinu dostupnosti SQL Server:  

1.  Po zobrazení výzvy Configuration Manager nastavení nahraďte následující:  

    -   **SQL Server název**: zadejte virtuální název koncového bodu, který jste nakonfigurovali při vytváření skupiny dostupnosti. Virtuálním názvem by měl být úplný název DNS, třeba ** &lt; server koncového bodu \> . fabrikam.com**.  

    -   **Instance**: Tato hodnota by měla zůstat prázdná. V této konfiguraci neexistuje žádná instance.  

    -   **Databáze**: zadejte název databáze, kterou jste vytvořili v primární replice skupiny dostupnosti.  

2.  Dále je nutné zadat síťové umístění, ke kterému mají jednotlivé SQL Server ve skupině přístup:  

    -   Účet počítače a účet služby z každého SQL Server vyžadují přístup k tomuto umístění pomocí úplného řízení.  

    -   Toto umístění se používá jenom během instalace a po dokončení instalace se může zrušit jeho sdílení nebo odstranění a lokalita se nainstaluje.  

3.  Po zadání těchto informací dokončete instalaci pomocí normálního procesu a konfigurací.  

##  <a name="service-a--server-cluster"></a><a name="BKMK_ClusterServerUpdates"></a>Obsluha serverového clusteru  
Teď můžete vytvořit kolekci, která obsahuje servery v clusteru, a potom nakonfigurovat nastavení clusteru tak, aby se používala při nasazení aktualizací do clusteru. Můžete řídit procento serverů, které jsou v daný okamžik online, a konfigurovat skripty PowerShellu před nasazením a po nasazení pro spouštění vlastních akcí.  

**Známé problémy této verze:**  

-   Vytváření sestav není k dispozici pro kontrolu stavu nasazení aktualizací softwaru pro clusterové servery.  

-   Možnost pořadí údržby na stránce **Nastavení clusteru** je v této verzi zakázaná a není dostupná.  

### <a name="try-it-out"></a>Určitě to udělejte!  
Zkuste dokončit následující úlohu a pak použijte informace o zpětné vazbě v horní části tohoto tématu a sdělte nám, jak se pracovalo:  

-   Můžu vytvořit kolekci, která představuje cluster serverů. Pro tento test můžete nakonfigurovat, aby vaše pravidla shromažďování členství měla 2 počítače v této kolekci.  

-   Můžu určit, že v každém okamžiku v rámci údržby clusteru může být offline jenom 50% serverů v clusteru. Pomocí ukázkových skriptů v postupu určete skripty před nasazením a po nasazení.  

-   Nasaďte aktualizaci do této kolekce. Zkontrolujte soubory Start. txt a end. txt v C:\Temp a ověřte počáteční a koncové časy nasazení na serverech v clusteru. Další informace najdete v souboru UpdatesDeployment. log.  

#### <a name="to-create-a-collection-for-a-server-cluster"></a>Vytvoření kolekce pro serverový cluster  

1.  [Vytvořte kolekci zařízení](../clients/manage/collections/create-collections.md) , která obsahuje servery v clusteru.  

2.  V pracovním prostoru **prostředky a kompatibilita** klikněte na **kolekce zařízení**, klikněte pravým tlačítkem na kolekci, která obsahuje servery v clusteru, a pak klikněte na **vlastnosti**.  

3.  Na kartě **Obecné** vyberte **všechna zařízení jsou součástí stejného serverového clusteru**a pak klikněte na **Nastavení**.  

4.  Na stránce **Nastavení clusteru** vyberte procento serverů, které lze současně převést do režimu offline, aby byly nainstalovány aktualizace softwaru. Jeden clusterový server může být v čase offline bez ohledu na procento, které zadáte. Při výběru počtu serverů, které se mají v jednom okamžiku vypínat, Configuration Manager se zaokrouhlí. Pokud například zvolíte 51% a v clusteru je 4 servery, 2 servery budou přepnuty do offline režimu.  

5.  Určete, jestli se má použít skript před nasazením (vyprazdňování uzlu) nebo po nasazení (obnovení uzlu).  

    > [!TIP]  
    >  Následují příklady, které můžete použít v části testování pro skripty před nasazením a po nasazení, které zapisují aktuální čas do textového souboru:  
    >   
    >  **Před nasazením**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Po nasazení**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-cluster"></a>Nasazení aktualizací softwaru do serverového clusteru  

1.  [Nasaďte aktualizace softwaru](../../sum/deploy-use/deploy-software-updates.md) do kolekce serverového clusteru.  

2.  [Monitorujte nasazení aktualizace softwaru](../../sum/deploy-use/monitor-software-updates.md).  
