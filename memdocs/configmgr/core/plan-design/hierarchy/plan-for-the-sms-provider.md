---
title: Plánování poskytovatele serveru SMS
titleSuffix: Configuration Manager
description: Přečtěte si o roli systému lokality poskytovatele služby SMS v Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c83d0da07474c8b078ee226d249b73f00562e0f5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700159"
---
# <a name="plan-for-the-sms-provider"></a>Plánování poskytovatele serveru SMS

*Platí pro: Configuration Manager (Current Branch)*

Chcete-li spravovat Configuration Manager, použijte konzolu Configuration Manager, která se připojuje k instanci **poskytovatele serveru SMS**. Ve výchozím nastavení se poskytovatel serveru SMS nainstaluje na server lokality při instalaci lokality centrální správy nebo primární lokality.

## <a name="about-the-sms-provider"></a><a name="BKMK_PlanSMSProv"></a> O poskytovateli serveru SMS  

Poskytovatel serveru SMS je poskytovatel rozhraní WMI (Windows Management Instrumentation) (WMI), který přiřazuje databázi Configuration Manager v lokalitě přístup **pro čtení** a **zápis** .  

- Každá lokalita centrální správy a primární lokalita musí mít alespoň jednoho poskytovatele serveru SMS. Podle potřeby můžete nainstalovat další poskytovatele.  

- Skupina zabezpečení **SMS Admins** poskytuje přístup k poskytovateli serveru SMS. Configuration Manager automaticky vytvoří tuto skupinu na serveru lokality a na každém počítači, kde nainstalujete instanci poskytovatele serveru SMS. Další informace najdete v tématu [Správci SMS](accounts.md#sms-admins).  

- Sekundární lokality nepodporují roli poskytovatele služby SMS.  

Configuration Manager uživatelé s právy pro správu používají k přístupu k informacím uloženým v databázi poskytovatele služby SMS. K tomu správci můžou použít konzolu Configuration Manager, Průzkumník prostředků, nástroje a vlastní skripty. Poskytovatel serveru SMS nekomunikuje s klienty Configuration Manager. Když se konzola Configuration Manager připojí k lokalitě, dotazuje rozhraní WMI na serveru lokality, aby vyhledala instanci poskytovatele služby SMS, která se má použít.  

Poskytovatel serveru SMS pomáhá vymáhat zabezpečení Configuration Manager. Vrátí pouze informace o tom, že uživatel konzoly má oprávnění k zobrazení.  

Poskytovatel serveru SMS taky poskytuje přístup k interoperabilitě API přes protokol HTTPS, který se označuje jako **Služba pro správu**. Tento REST API lze použít místo vlastní webové služby pro přístup k informacím z webu. Další informace najdete v tématu [co je služba pro správu?](../../../develop/adminservice/overview.md).

> [!IMPORTANT]  
> Pokud je každá instance poskytovatele serveru SMS pro lokalitu offline, Configuration Manager konzol se nemůže připojit k webu.  

Další informace o tom, jak spravovat poskytovatele služby SMS, najdete v tématu [Správa poskytovatele serveru SMS](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider).  

## <a name="installation-prerequisites"></a>Instalační požadavky  

Aby mohl cílový server podporovat poskytovatele služby SMS, musí splňovat následující požadavky:  

- Ve stejné doméně jako server lokality a systémy lokality databáze lokality  

- Nejde mít roli systému lokality z jiné lokality.  

- Poskytovatel serveru SMS už nemůže mít žádnou lokalitu.  

- Spustit podporovanou verzi operačního systému  

- Minimálně 650 MB volného místa na disku pro podporu součástí ADK Windows Další informace o službě Windows ADK a poskytovateli serveru SMS najdete v tématu [požadavky na nasazení operačního systému](#BKMK_WAIKforSMSProv).  

- REST API [služby správy](../../../develop/adminservice/overview.md) :

  - .NET 4,5 nebo novější

  - Povolit webový server role Windows Server **(IIS)**

    > [!Note]  
    > Každý poskytovatel serveru SMS se pokusí nainstalovat službu správy, která vyžaduje certifikát. Tato služba má závislost na službě IIS pro vázání tohoto certifikátu na port HTTPS 443. Pokud povolíte [Rozšířené protokolu HTTP](enhanced-http.md), lokalita tento certifikát vytvoří pomocí rozhraní API služby IIS. Pokud vaše lokalita používá infrastrukturu veřejných klíčů (PKI), je nutné ručně vytvořit z poskytovatele služby IIS certifikát PKI. Počínaje verzí 2002 lokalita automaticky používá certifikát podepsaný držitelem webu.

## <a name="locations"></a><a name="bkmk_location"></a> Polohy  

Při instalaci lokality automaticky nainstalujete prvního poskytovatele služby SMS pro danou lokalitu. Pro poskytovatele serveru SMS můžete určit kterékoli z následujících podporovaných umístění:  

- Server lokality  

- Server databáze lokality  

- Jiný server, který splňuje [předpoklady pro instalaci](#installation-prerequisites)  

Postup zobrazení umístění každého poskytovatele služby SMS pro danou lokalitu:

1. V konzole Configuration Manager klikněte na pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a pak vyberte uzel **lokality** .  

2. V seznamu vyberte požadovaný web a na pásu karet zvolte **vlastnosti** .  

3. Na kartě **Obecné** ve **vlastnostech**lokality Zobrazte pole **umístění poskytovatele serveru SMS** .  

Všichni poskytovatelé serveru SMS podporují souběžná připojení většího počtu požadavků. Jediným omezením u těchto připojení jsou počet připojení serverů, která jsou dostupná pro Windows, a dostupné prostředky na serveru pro obsluhu požadavků na připojení.  

Po instalaci lokality můžete znovu spustit instalaci Configuration Manager na serveru lokality. Pomocí instalačního programu můžete změnit umístění existujícího poskytovatele služby SMS nebo nainstalovat další poskytovatele serveru SMS v dané lokalitě. Nainstalujte do počítače pouze jednoho poskytovatele služby SMS. Počítač nemůže hostovat poskytovatele služby SMS z více než jedné lokality.  

### <a name="choosing-a-location"></a>Volba umístění

V následujících částech jsou popsány výhody a nevýhody instalace poskytovatele služby SMS na jednotlivých podporovaných umístěních:  

#### <a name="configuration-manager-site-server"></a>Server Configuration Manager lokality

- **Výhody**  

  - Poskytovatel serveru SMS nepoužívá systémové prostředky počítače databáze lokality.  

  - Toto umístění může poskytovat lepší výkon, než poskytovatel serveru SMS umístěný na jiném počítači, než je server lokality nebo počítač databáze lokality.  

- **Nevýhody**  

  - Poskytovatel serveru SMS využívá systémové a síťové prostředky, které je možné vyhradit operacím serveru lokality.  

#### <a name="sql-server-that-hosts-the-site-database"></a>SQL Server, který hostuje databázi lokality

- **Výhody**  

  - Poskytovatel serveru SMS nepoužívá systémové prostředky na serveru lokality.  

  - Toto umístění může poskytovat nejlepší výkon ze všech tří umístění, pokud je k dispozici dostatek serverových prostředků.  

- **Nevýhody**  

  - Poskytovatel serveru SMS využívá systémové a síťové prostředky, které se dají vyhradit operacím databáze lokality.  

  - Pokud je databáze lokality hostována v clusterované instanci SQL Server, nemůžete použít toto umístění.  

#### <a name="computer-other-than-the-site-server-or-site-database-server"></a>Jiný počítač než server lokality nebo Server databáze lokality

- **Výhody**  

  - Poskytovatel serveru SMS nepoužívá systémové prostředky serveru lokality nebo databáze webu.  

  - Tento typ umístění umožňuje nasadit další poskytovatele serveru SMS za účelem poskytnutí vysoké dostupnosti pro připojení.  

- **Nevýhody**  

  - Může dojít ke snížení výkonu poskytovatele služby SMS. K tomuto chování dochází z důvodu další síťové aktivity, kterou musí koordinovat se serverem lokality a počítačem databáze lokality.  

  - Tento server musí být vždycky přístupný pro server databáze lokality a pro všechny počítače s nainstalovanou konzolou Configuration Manager.  

  - Toto umístění může využívat systémové prostředky, které by jinak byly vyhrazené jiným službám.  

## <a name="authentication"></a><a name="bkmk_auth"></a> Přihlašovací

<!--1357013-->
Počínaje verzí 1810 můžete určit minimální úroveň ověřování pro správce pro přístup k Configuration Manager lokalit. Tato funkce vynutila správcům přihlášení k systému Windows s požadovanou úrovní. Platí pro všechny komponenty, které přistupují k poskytovateli serveru SMS. Například konzola Configuration Manager, metody sady SDK a rutiny prostředí Windows PowerShell.

### <a name="configure-authentication"></a>Konfigurace ověřování

Pokud chcete nakonfigurovat toto nastavení, nejdřív se přihlaste k Windows pomocí zamýšlené úrovně ověřování.

> [!Important]  
> Tato konfigurace je nastavení v rámci hierarchie. Než toto nastavení změníte, ujistěte se, že se všichni správci Configuration Manager můžou přihlásit k Windows s požadovanou úrovní ověřování.

Pro konfiguraci tohoto nastavení použijte následující postup:

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** .  

2. Na pásu karet vyberte **Nastavení hierarchie** .  

3. Přepněte na kartu **ověřování** . Vyberte požadovanou [úroveň ověření](#authentication-levels)a pak vyberte **OK**.  

    - Pouze v případě potřeby vyberte možnost **Přidat** a Vylučte konkrétní uživatele nebo skupiny. Další informace naleznete v tématu [vyloučení](#exclusions).  

### <a name="authentication-levels"></a>Úrovně ověřování

K dispozici jsou následující úrovně:

- **Ověřování systému Windows**: vyžadovat ověřování pomocí přihlašovacích údajů domény služby Active Directory. Toto nastavení je předchozí chování a aktuální výchozí nastavení. Při aktualizaci lokality se žádná změna úrovně ověřování nijak nemění.  

- **Ověřování certifikátu**: vyžaduje ověření pomocí platného certifikátu, který vystavila důvěryhodná certifikační autorita PKI. Tento certifikát nekonfigurujte v Configuration Manager. Configuration Manager vyžaduje, aby byl správce přihlášený k Windows pomocí PKI.  

- **Ověřování ve Windows Hello pro firmy**: vyžaduje ověřování pomocí silného dvojúrovňového ověřování, které je vázané na zařízení a používá BIOMETRIKA nebo PIN. Další informace najdete v tématu [Windows Hello pro firmy](/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

### <a name="exclusions"></a>Vyloučení

Na kartě **ověřování** v nastavení hierarchie můžete také vyloučit určité uživatele nebo skupiny. Tuto možnost použijte zřídka. Například když konkrétní uživatelé potřebují přístup ke konzole Configuration Manager, ale nelze ověřit pro systém Windows na požadované úrovni. Může být taky potřeba pro automatizaci nebo služby, které běží v kontextu systémového účtu.

## <a name="about-sms-provider-languages"></a><a name="BKMK_SMSProvLanguages"></a> O jazycích poskytovatele SMS  

Poskytovatel serveru SMS funguje nezávisle na jazyce zobrazení serveru, na který ho nainstalujete.  

Když uživatel s právy pro správu nebo Configuration Manager proces požaduje data pomocí poskytovatele služby SMS, pokusí se tato data vrátit ve formátu, který odpovídá jazyku operačního systému žádajícího počítače.

Způsob, jakým se pokusy o shodu s jazykem, je nepřímý. Poskytovatel serveru SMS nepřeloží informace z jednoho jazyka do druhého. Když vrátí data pro zobrazení v konzole Configuration Manager, závisí jazyk zobrazení dat na zdroji objektu a typu úložiště.  

Když Configuration Manager ukládá data pro objekt v databázi, dostupné jazyky závisí na následujících faktorech:  

- Configuration Manager ukládá objekty, které vytvoří, pomocí podpory pro více jazyků. Ukládá objekt do databáze lokality pomocí jazyků, které nakonfigurujete pro lokalitu při spuštění instalačního programu. Konzola Configuration Manager zobrazí tyto objekty v jazyce zobrazení žádajícího počítače, když je tento jazyk pro objekt k dispozici. Pokud konzola nemůže zobrazit objekt v jazyce zobrazení žádajícího počítače, zobrazí objekt ve výchozím jazyce, což je angličtina.  

- Configuration Manager ukládá objekty, které uživatel s právy pro správu vytvoří, pomocí jazyka, který se použil k vytvoření objektu. Tyto objekty se zobrazí v konzole Configuration Manager ve stejném jazyce. Poskytovatel serveru SMS je nemůže přeložit a nemá k dispozici více jazykových možností.  

## <a name="use-multiple-sms-providers"></a><a name="BKMK_MultiSMSProv"></a> Použití více poskytovatelů serveru SMS  

Po dokončení instalace lokality můžete pro tuto lokalitu nainstalovat další poskytovatele serveru SMS. Chcete-li nainstalovat další poskytovatele serveru SMS, spusťte instalační program Configuration Manager na serveru lokality.

Zvažte instalaci dalších poskytovatelů serveru SMS, pokud platí kterákoli z následujících podmínek:  

- Mnoho správců potřebuje použít konzolu Configuration Manager a současně se připojit k lokalitě.  

- Použijete sadu Configuration Manager SDK nebo jiné produkty, které mohou vést k častým voláním poskytovatele služby SMS.  

- Máte obchodní požadavek na vysokou dostupnost poskytovatele služby SMS.  

Když v lokalitě nainstalujete více poskytovatelů serveru SMS a vyžádáte si žádost o připojení, lokalita náhodně přiřadí každou novou žádost o připojení k používání nainstalovaného poskytovatele služby SMS. Nemůžete zadat poskytovatele služby SMS pro použití s konkrétní relací připojení.  

> [!NOTE]  
> Zvažte výhody a nevýhody jednotlivých umístění poskytovatele služby SMS. Další informace najdete v tématu [umístění](#bkmk_location). Tyto požadavky vyvážit s informacemi, které nemůžete ovládat, který poskytovatel serveru SMS se používá pro každé nové připojení.  

Když poprvé připojíte konzolu Configuration Manager k lokalitě, připojení se dotazuje rozhraní WMI na serveru lokality. Tento dotaz identifikuje instanci poskytovatele serveru SMS, kterou používá konzola nástroje. Tato konkrétní instance poskytovatele služby SMS zůstane používána konzolou nástroje až do ukončení relace. Pokud je relace ukončena, protože server poskytovatele služby SMS není v síti k dispozici, dojde při opětovném připojení konzoly k lokalitě k zopakování počátečního dotazu. Je možné, že lokalita přiřadí stejnou instanci poskytovatele služby SMS, která není k dispozici. Pokud dojde k tomuto chování, pokuste se znovu připojit konzolu, dokud lokalita nevrátí dostupného poskytovatele služby SMS.  

## <a name="about-the-sms-provider-namespace"></a><a name="BKMK_SMSProvNamespace"></a> O oboru názvů poskytovatele služby SMS  

Configuration Manager schéma WMI definuje strukturu poskytovatele služby SMS. Obory názvů schématu popisují umístění dat Configuration Manager v rámci schématu poskytovatele služby SMS. Následující tabulka obsahuje některé běžné obory názvů, které poskytovatel serveru SMS používá:  

|Obor názvů|Popis|  
|---------------|-----------------|  
|`Root\SMS\site_<site code>`|Poskytovatel serveru SMS, který je široce používán konzolou Configuration Manager, Průzkumník prostředků, Configuration Managermi nástroji a skripty.|  
|`Root\SMS\SMS_ProviderLocation`|Umístění počítačů poskytovatele serveru SMS pro lokalitu.|  
|`Root\CIMv2`|Umístění informací o oboru názvů rozhraní WMI v inventáři během inventáře hardwaru a softwaru.|  
|`Root\CCM`|Configuration Manager zásady konfigurace klienta a data klienta.|  
|`Root\CIMv2\SMS`|Umístění tříd generování sestav inventáře, které shromažďuje agent klienta inventáře. Klienti toto nastavení zkompiluje během hodnocení zásad počítače. Tato nastavení jsou založená na konfiguraci nastavení klienta pro daný počítač.|  

## <a name="os-deployment-requirements"></a><a name="BKMK_WAIKforSMSProv"></a> Požadavky na nasazení operačního systému

Počítač, na který nainstalujete instanci poskytovatele serveru SMS, vyžaduje podporovanou verzi sady Windows ADK.  

Další informace o tomto požadavku najdete v tématu [požadavky na infrastrukturu pro nasazení operačního systému](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10) a [podporu pro Windows 10](../configs/support-for-windows-10.md).  

Když spravujete nasazení operačního systému, umožňuje Windows ADK poskytovateli serveru SMS dokončit různé úlohy, jako například:  

- Zobrazení podrobností souboru WIM  

- Přidání souborů ovladače do stávajících spouštěcích bitových kopiích  

- Vytvořit spouštěcí soubory ISO  

Instalace sady Windows ADK může vyžadovat až 650 MB volného místa na disku každého počítače, který instaluje poskytovatele serveru SMS. Tento minimální požadavek na místo na disku je nezbytný pro Configuration Manager k instalaci spouštěcích imagí prostředí Windows PE.  

## <a name="administration-service"></a><a name="bkmk_admin-service"></a> Služba správy

<!--3607711, fka 1321523-->

Poskytovatel serveru SMS poskytuje přístup k vzájemné funkční spolupráci rozhraní API přes připojení HTTPS OData nazývané **službu pro správu**. Tento REST API lze použít místo vlastní webové služby pro přístup k informacím z webu.

Další informace najdete v tématu [co je služba pro správu?](../../../develop/adminservice/overview.md)