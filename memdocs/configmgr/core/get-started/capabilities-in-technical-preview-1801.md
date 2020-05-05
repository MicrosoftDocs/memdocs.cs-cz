---
title: Technical Preview 1801 | Microsoft Docs
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview verze 1801 pro Configuration Manager.
ms.date: 01/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5a352ae0-355f-4fcf-b863-fb0654f51c52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e1e83126748596d9d631caa85506f7b236bf4a76
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074210"
---
# <a name="capabilities-in-technical-preview-1801-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1801 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1801. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview. 

Před instalací této verze Technical Preview si přečtěte [Technical Preview for Configuration Manager](technical-preview.md) . V tomto článku se seznámíte s obecnými požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Známé problémy v této verzi Technical Preview:**
- **Aktualizace na novou verzi Preview se nezdařila, pokud máte server lokality v pasivním režimu**. Pokud máte [server primární lokality v pasivním režimu](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), je nutné před aktualizací na tuto novou verzi Preview odinstalovat server lokality pasivního režimu. Server lokality v pasivním režimu můžete po dokončení aktualizace znovu nainstalovat.

  Postup odinstalace serveru lokality pasivního režimu:
  1. V konzole Configuration Manager klikněte na **Správa** > **Přehled** > **Konfigurace** > **servery lokality a role systému lokality**a potom vyberte server lokality pasivního režimu.
  2. V podokně **role systému lokality** klikněte pravým tlačítkem na roli **serveru lokality** a pak zvolte **Odebrat roli**.
  3. Klikněte pravým tlačítkem na server lokality pasivního režimu a zvolte **Odstranit**.
  4. Po odinstalaci serveru lokality na aktivním serveru primární lokality restartujte službu **CONFIGURATION_MANAGER_UPDATE**.
  <!--sms 489412-->


**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.
 -  Task 1
 -  Task 2              
-->



## <a name="create-phased-deployments"></a>Vytvořit dvoufázové nasazení
<!-- 1357405 -->
Postupná nasazení automatizují koordinované, sekvenční zavedení softwaru bez vytváření více nasazení. V této verzi Technical Preview se Průvodce vytvořením fáze nasazení dá dokončit pro pořadí úkolů v konzole pro správu. Nasazení ale nejsou vytvořená. 

### <a name="try-it-out"></a>Určitě to udělejte!  
  Zkuste úkoly dokončit. Potom můžete poslat **zpětnou vazbu** na kartě **Domů** na pásu karet, abychom věděli, jak pracovali.
 
**Vytvoření postupného nasazení pro pořadí úkolů** </br>
1. V pracovním prostoru **softwarová knihovna** rozbalte možnost **operační systémy**a vyberte **pořadí úloh**.
2. Klikněte pravým tlačítkem na existující pořadí úloh a vyberte **vytvořit dvoufázové nasazení**. 
3. Na kartě **Obecné** udělte postupné nasazení název, popis (volitelné) a vyberte **automaticky vytvořit výchozí pilotní a produkční fáze**. 
4. Naplňte **pilotní kolekce** a pole **produkční kolekce** . Vyberte **Další**.
5. Na kartě **Nastavení** vyberte jednu možnost pro každé nastavení plánování a po dokončení vyberte **Další** . 
6. Na kartě **fáze** v případě potřeby upravte jakoukoli fázi a potom klikněte na tlačítko **Další**.
7. Potvrďte svoje výběry na kartě **Souhrn** a pokračujte kliknutím na tlačítko **Další** .

## <a name="co-management-reporting"></a>Sestavy spolusprávy
<!-- 1356648 -->
Pokud používáte možnosti [spolusprávy](../../comanage/overview.md) , můžete nyní zobrazit řídicí panel s informacemi o spolusprávě ve vašem prostředí. V konzole Configuration Manager přejděte do pracovního prostoru **monitorování** , rozbalte položku **upgrade Readiness**a vyberte řídicí panel **spolusprávy** . Řídicí panel obsahuje tyto dlaždice:
- **Spoluspravovaná zařízení**: procento zařízení ve vašem prostředí, které jste povolili pro spolusprávu.
- **Distribuce operačního systému**: rozpis operačních systémů (OS) podle verze. Tento graf používá následující seskupení:
  - Windows 7 & 8. x
  - Windows 10 nižší než 1709
  - Windows 10 1709 a novější
    > [!NOTE] 
    > Windows 10, verze 1709 a novější, je předpokladem pro spolusprávu
- **Stav spolusprávy**: rozpis úspěšnosti nebo selhání zařízení v následujících kategoriích:
   - Úspěch, připojeno k hybridní službě Azure AD
   - Úspěch, připojeno k Azure AD
   - Chyba: automatický zápis se nezdařil
- **Přechod úlohy**: pruhový graf zobrazující počet zařízení, která jste přešli na Microsoft Intune pro tři dostupné úlohy: 
   - Zásady dodržování předpisů
   - Přístup k prostředkům
   - web Windows Update pro firmy

### <a name="prerequisites"></a>Požadavky
- Počítač, který spouští konzolu Configuration Manager, vyžaduje aplikaci Internet Explorer 9 nebo novější.



## <a name="improvements-to-automatic-deployment-rule-evaluation-schedule"></a>Vylepšení plánu vyhodnocení pravidla automatického nasazení
<!-- 1357133 -->
V závislosti na vašem [uživatelském hlasovém názoru](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8819518-software-update-patch-tuesday-scheduling)teď můžete naplánovat vyhodnocení pravidla automatického nasazení (ADR), které se má posunout od základního dne. Například posun dvou dnů od druhého úterý v měsíci vyhodnotí pravidlo ve čtvrtek. 

### <a name="try-it-out"></a>Určitě to udělejte!  
 Zkuste úkoly dokončit. Potom můžete poslat **zpětnou vazbu** na kartě **Domů** na pásu karet, abychom věděli, jak pracovali. <br/>

**Vytvoření vlastního plánu, který vyhodnotí a přiloží posun od základního dne** </br>
1.  V pracovním prostoru **softwarová knihovna** rozbalte možnost **aktualizace softwaru**a vyberte možnost **pravidla automatického nasazení**.
2. Klikněte pravým tlačítkem na **pravidla automatického nasazení** a vyberte **vytvořit pravidlo automatického nasazení**. 
3. Podle pokynů dokončete karty **Obecné**, **nastavení nasazení**a **aktualizace softwaru** . 
4. Na kartě **Plán vyhodnocení** vyberte **Spustit pravidlo podle plánu** a **Přizpůsobte**si ho.
5. Pro vlastní plán vyberte **měsíčně** a vložte do něj základní den, například druhé úterý. 
6. Zaškrtněte **tlačítko** **posun (dny)** a počet dní pro posun po dokončení.  
7. Dokončete **Průvodce vytvořením pravidla automatického nasazení**. 



## <a name="reassign-distribution-point"></a>Změna přiřazení distribučního bodu
<!-- 1306937 -->
Mnoho zákazníků má velké Configuration Manager infrastruktury a snižuje primární nebo sekundární lokalitu, aby se zjednodušilo jejich prostředí. Pořád potřebují uchovávat distribuční body v pobočkách, aby poskytovaly obsah spravovaným klientům. Tyto distribuční body často obsahují více terabajtů nebo více obsahu. Tento obsah je nákladný v čase a šířka pásma sítě pro distribuci na tyto vzdálené servery. 

Tato funkce umožňuje změnit přiřazení distribučního bodu k jiné primární lokalitě bez nutnosti opětovné distribuce obsahu. Tato akce aktualizuje přiřazení systému lokality a uchovává veškerý obsah na serveru. Pokud potřebujete změnit přiřazení více distribučních bodů, nejprve tuto akci proveďte v jednom distribučním bodě a pak pokračujte v dalších serverech po jednom.

> [!IMPORTANT]
> Systémový server lokality může hostovat pouze roli distribučního bodu. Pokud je server systému lokality hostitelem jiné role serveru Configuration Manager, jako je například bod migrace stavu, nelze změnit přiřazení distribučního bodu. Nemůžete znovu přiřadit distribuční bod cloudu. 

Tato možnost není v této verzi funkční kvůli limitu Technical Preview pro jednu primární lokalitu. Vezměte v úvahu scénář a pak na kartě **Domů** na pásu karet poslat **zpětnou vazbu** týkající se možností této akce.
1. V konzole Configuration Manager otevřete pracovní prostor **Správa** a vyberte uzel **distribuční body** .
2. Klikněte pravým tlačítkem myši na cílový distribuční bod a vyberte **změnit přiřazení distribučního bodu**. 
  ![Změna přiřazení distribučního bodu](media/1306937-reassign-dp.png)
3. Vyberte server lokality a kód lokality, pro které chcete změnit přiřazení distribučního bodu. 
  ![Vybrat server lokality](media/1306937-select-site.png)



## <a name="improvements-to-hardware-inventory"></a>Vylepšení inventáře hardwaru
<!-- 1357389 -->
U nově přidaných tříd se pro vlastnosti inventáře hardwaru, které nejsou klíče, dají zadat délky řetězců větší než 255 znaků.

### <a name="try-it-out"></a>Určitě to udělejte!  
Zkuste úkoly dokončit. Potom můžete poslat **zpětnou vazbu** na kartě **Domů** na pásu karet, abychom věděli, jak pracovali.<br/>

1. V pracovním prostoru **Správa** klikněte na **nastavení klienta** zvýraznit nastavení klientského zařízení, které chcete upravit, klikněte pravým tlačítkem myši a vyberte možnost **vlastnosti**. 
2. Vyberte **inventář hardwaru**a pak **nastavte třídy**a **Přidat**.
3. Klikněte na tlačítko **připojit** .
4. Do pole **název počítače**zadejte **obor názvů rozhraní WMI**a v případě potřeby vyberte možnost **rekurzivní** . V případě potřeby zadejte přihlašovací údaje pro připojení. Kliknutím na **připojit** Zobrazte třídy oboru názvů.
5. Vyberte novou třídu a pak klikněte na **Upravit**.
6. Změňte **délku** nejméně jedné vlastnosti, která je řetězcem, který je jiný než klíč, aby byla větší než 255. Klikněte na tlačítko **OK**. 
7. Zajistěte, aby byla upravená vlastnost pro **Přidat třídu inventáře hardwaru** vybrána, a klikněte na tlačítko **OK**. 
8. Shromážděte inventář hardwaru s nově přidanou třídou, která obsahuje vlastnost větší než 255 znaků. 



## <a name="improvements-to-client-settings-for-software-center"></a>Vylepšení nastavení klienta pro Centrum softwaru
<!-- 1351224 & 1355146 -->
V této verzi Technical Preview byly vylepšení pro přizpůsobení centra softwaru v rámci nastavení klienta k dispozici. 

1. Nastavení klienta pro Centrum softwaru teď má tlačítko **přizpůsobit** .
2. Přidala se náhled, který ukazuje, jak vypadá banner centra softwaru.<!--1351224-->
    - Pokud není vybrané žádné logo, zobrazí náhled text a barvu názvu společnosti.
    - Pokud je vybrané logo, zobrazí náhled logo a text názvu společnosti.  
3.  **Skrýt neschválené aplikace v centru softwaru** je nové nastavení pro Centrum softwaru. Když je tato možnost povolená, aplikace dostupné pro uživatele, které vyžadují schválení, jsou v centru softwaru skryté.<!--1355146-->

### <a name="try-it-out"></a>Určitě to udělejte!  
 Zkuste úkoly dokončit. Potom můžete poslat **zpětnou vazbu** na kartě **Domů** na pásu karet, abychom věděli, jak pracovali.

1. V pracovním prostoru **Správa** klikněte na **nastavení klienta**. Vyberte nastavení klientského zařízení, které chcete upravit. Klikněte na něj pravým tlačítkem a pak vyberte **vlastnosti** a **Centrum softwaru**.
2.  Klikněte na tlačítko **přizpůsobit** . Vyzkoušejte si různá nastavení přizpůsobení včetně verze Preview.
3. Povolte nastavení **Skrýt neschválené aplikace v centru softwaru**. Sledujte změny v centru softwaru. 



## <a name="new-settings-for-windows-defender-application-guard"></a>Nová nastavení pro ochranu Application Guard v programu Windows Defender
<!-- 1356256 -->
Pro zařízení s Windows 10 verze 1709 a novější jsou k dispozici dvě nová nastavení interakce hostitelů pro [ochranu Application Guard v programu Windows Defender](../../protect/deploy-use/create-deploy-application-guard-policy.md). 
1. Webům lze udělit přístup k virtuálnímu grafickému procesoru hostitele. 
2. Soubory stažené v kontejneru lze zachovat na hostiteli. </br>



## <a name="improvements-to-run-scripts"></a>Vylepšení spouštění skriptů
<!-- 1236459 -->
Funkce [ **spustit skripty** ](../../apps/deploy-use/create-deploy-scripts.md) teď umožňuje importovat a spouštět podepsané skripty PowerShellu. 
- Aby se zajistila integrita skriptu, musí být naimportovány podepsané skripty místo použití kopírování/vkládání. 
- Importované podepsané skripty nelze po importu upravovat.
    
>[!IMPORTANT]
>V této verzi Technical Preview existují dvě dočasná omezení.
>- Skripty lze importovat pouze do funkce spustit skripty a nelze je upravovat přímo z konzoly nástroje.
>- Skripty importované s kódováním, které není Unicode, se můžou v konzole zobrazovat nesprávně. Skript se pořád spustí jako původně zapsaný.





## <a name="next-steps"></a>Další kroky
Informace o instalaci nebo aktualizaci větve Technical Preview najdete v tématu [Technical Preview pro Configuration Manager](technical-preview.md).    
