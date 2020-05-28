---
title: Technical Preview 1708
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview verze 1708 pro Configuration Manager.
ms.date: 08/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3c061ceb-3bdb-4d4f-8c60-344964bd416b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: ab5cc83cc8e7bb51477d84a50f18d4f6b73f286d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721329"
---
# <a name="capabilities-in-technical-preview-1708-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1708 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1708. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview. Před instalací této verze Technical Preview si přečtěte [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md) , abyste se seznámili se všeobecnými požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Známé problémy v této verzi Technical Preview:**
- **Aktualizace na verzi preview 1708 se nezdařila, pokud máte server lokality v pasivním režimu**. Pokud spustíte verzi Preview 1706 nebo 1707 a máte [server primární lokality v pasivním režimu](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), je nutné nejprve odinstalovat server lokality pasivního režimu před tím, než bude možné úspěšně aktualizovat lokalitu Preview na verzi 1708. Server lokality v pasivním režimu můžete po spuštění lokality verze 1708 znovu nainstalovat.

  Postup odinstalace serveru lokality pasivního režimu:
  1. V konzole nástroje klikněte na **Správa**  >  **Přehled**  >  **Konfigurace**  >  **servery lokality a role systému lokality**a potom vyberte server lokality pasivního režimu.
  2. V podokně **role systému lokality** klikněte pravým tlačítkem na roli **serveru lokality** a pak zvolte **Odebrat roli**.
  3. Klikněte pravým tlačítkem na server lokality pasivního režimu a zvolte **Odstranit**.
  4. Po odinstalaci serveru lokality na aktivním serveru primární lokality restartujte službu **CONFIGURATION_MANAGER_UPDATE**.




**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Vylepšení zadávání parametrů skriptu při nasazení skriptů PowerShellu z Configuration Manager
<!-- 1236459 -->

Z Configuration Manager 1706 a vyšší můžete [vytvořit a spustit powershellové skripty z konzoly Configuration Manager](../../apps/deploy-use/create-deploy-scripts.md).

Ve [verzi Technical Preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager)jsme tuto možnost rozšířili tak, aby Configuration Manager četla parametry ze skriptu.

V této verzi Technical Preview jsme rozšířili funkci parametrů skriptu, aby bylo možné zjistit, které parametry jsou povinné a které jsou volitelné, a zobrazí se výzva k jejich zadání.

### <a name="try-it-out"></a>Určitě to udělejte!

1. Při [vytváření a spouštění skriptů PowerShellu z konzoly Configuration Manager](../../apps/deploy-use/create-deploy-scripts.md)postupujte podle pokynů.
2. Na stránce nové **Parametry skriptu** v **Průvodci vytvořením skriptu**zvolte parametr a pak upravte jeho hodnoty.
Průvodce zobrazí seznam parametrů, které jsou povinné a které jsou volitelné.
4. Po dokončení úprav parametrů dokončete průvodce.

Po spuštění skriptu budou použity hodnoty parametrů, které jste nakonfigurovali. Pokud jste nenakonfigurovali povinný parametr, koncový uživatel se vyzve k zadání parametru při spuštění skriptu.

## <a name="management-insights"></a>Přehledy správy
<!-- 1353967 -->
Nyní můžete získat přehled o aktuálním stavu prostředí založeného na analýze dat v databázi lokality. Přehledy vám pomůžou lépe pochopit vaše prostředí a provádět akce na základě přehledu. Projděte si přehledy správy v konzole **Administration**Configuration Manager v části Správa  >  **přehledů**pro  >  **všechny přehledy**. V této verzi jsou nyní k dispozici následující přehledy:

- **Aplikace bez nasazení**: Vypíše aplikace v prostředí, které nemají aktivní nasazení. Díky tomu můžete najít a odstranit nepoužívané aplikace a zjednodušit tak seznam aplikací zobrazených v konzole nástroje.
- **Prázdné kolekce**: vypíše kolekce v prostředí, které nemají žádné členy. Tyto kolekce můžete odstranit, chcete-li zjednodušit seznam kolekcí zobrazených při nasazování objektů, například.


## <a name="restart-computers-from-the-configuration-manager-console"></a>Restartování počítačů z konzoly Configuration Manager   
<!-- 1356283 -->
Od této verze můžete použít konzolu Configuration Manager k identifikaci klientských zařízení, která vyžadují restart, a pak použít akci klientského oznámení k jejich restartování.

Chcete-li identifikovat zařízení, která čekají na restartování, vyhledejte **položky prostředky a kompatibilita**  >  **Devices** a vyberte kolekci se zařízeními, která by mohla vyžadovat restartování. Po výběru kolekce můžete zobrazit stav jednotlivých zařízení v podokně podrobností v novém sloupci s názvem **čeká na restartování**. Každé zařízení má hodnotu **Yes**nebo **No**.

Vytvoření klientského oznámení pro restartování zařízení:
1. Vyhledejte zařízení, které chcete restartovat, v uzlu zařízení v konzole nástroje.
2. Pravým tlačítkem myši klikněte na zařízení, vyberte **klientské oznámení**a pak vyberte **restartovat**. Tím se otevře okno s informacemi o restartování. Kliknutím na **OK** potvrďte požadavek na restartování.

Když klient obdrží oznámení, otevře se okno oznámení **centra softwaru** , které uživatele informuje o restartování. Ve výchozím nastavení dojde k restartování po 90 minutách. Čas restartování můžete upravit konfigurací [nastavení klienta](../clients/deploy/configure-client-settings.md). Nastavení pro chování při restartování najdete na kartě [restart počítače](../clients/deploy/about-client-settings.md#computer-restart) výchozího nastavení.


### <a name="try-it-out"></a>Určitě to udělejte!
Zkuste provést následující úkoly a pak nám poslat **zpětnou vazbu** z karty **Domů** na pásu karet a sdělte nám, jak se pracovalo:
1. Nasaďte aplikaci nebo ji aktualizujte na zařízení, které bude vyžadovat, aby se zařízení restartovalo, aby se dokončila instalace.
2. Vyhledejte zařízení v uzlu prostředky **a kompatibilita**v  >  **Devices** konzole a potvrďte, že se ve sloupci **čeká na restartování** zobrazí **Ano** . Může trvat až 20 minut, než se stav probíhajícího restartování projeví v konzole nástroje.
3. Monitorujte zařízení a potvrďte, že se otevře oznámení centra softwaru a že se zařízení úspěšně restartuje.


## <a name="software-center-customization"></a>Přizpůsobení centra softwaru
<!-- 1351224 -->
Můžete přidat prvky firemního brandingu a zadat viditelnost karet v centru softwaru. Můžete přidat název vaší společnosti v centru softwaru, nastavit motiv barvy konfigurace centra softwaru, nastavit logo společnosti a nastavit viditelné karty pro klientská zařízení.

### <a name="customize-software-center"></a>Přizpůsobení centra softwaru

Postup úpravy centra softwaru:

1. V konzole **Configuration Manager** vyberte možnost **Správa**  >  **nastavení klienta**. Klikněte na požadovanou instanci nastavení klienta.
2. Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.
3. V dialogovém okně **výchozí nastavení** vyberte **Centrum softwaru**.
4. Vyberte **Ano** , pokud chcete **Vybrat nové nastavení a zadat firemní informace** . tím povolíte nastavení přizpůsobení centra softwaru.
5. Zadejte **název vaší společnosti**.
6. Vyberte **barevné schéma pro Centrum softwaru**.
7. Klikněte na **Procházet** a přejděte do svého loga pro Centrum softwaru. Logo musí být JPEG nebo PNG 400 x 100 pixelů s maximální velikostí 750 KB.
8. Vyberte **Ano** , pokud chcete, aby se karty zobrazovaly v centru softwaru pro klientská zařízení. Musí být viditelná aspoň jedna karta:

    -  Povolit kartu aplikace
    -  Povolit kartu aktualizace
    -  Povolit kartu operační systémy
    -  Povolit kartu stav instalace
    -  Povolit kartu dodržování předpisů zařízením
    -  Povolit kartu Možnosti

### <a name="next-steps"></a>Další kroky

Další informace o správě aplikací v Configuration Manager najdete v tématu [Úvod do správy aplikací](../../apps/understand/introduction-to-application-management.md).
