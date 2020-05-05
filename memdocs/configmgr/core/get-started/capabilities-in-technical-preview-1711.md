---
title: Technical Preview 1711 | Microsoft Docs
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview verze 1711 pro Configuration Manager.
ms.date: 11/17/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e68dc12-6776-437a-9138-45cd7d4bf9cf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e6f8ed1562392899b46a082bf8f64872c7e1b67d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721287"
---
# <a name="capabilities-in-technical-preview-1711-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1711 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1711. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview. Před instalací této verze Technical Preview si přečtěte [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md) , abyste se seznámili se všeobecnými požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Známé problémy v této verzi Technical Preview:**
- **Podpora pro Windows 10 verze 1709 (označovaná také jako aktualizace tvůrců v rámci služby Updates)**.  Od této verze Windows Windows Media obsahuje několik edicí. Při konfiguraci pořadí úkolů pro použití balíčku s upgradem operačního systému nebo bitové kopie operačního systému nezapomeňte vybrat [edici, která je podporována pro použití v Configuration Manager](../plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).
- **Aktualizace na novou verzi Preview se nezdařila, pokud máte server lokality v pasivním režimu**. Když spustíte verzi Preview, která má [server primární lokality v pasivním režimu](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), je nutné před tím, než budete moct úspěšně aktualizovat lokalitu Preview na tuto novou verzi Preview, odinstalovat server lokality pasivního režimu. Server lokality v pasivním režimu můžete po dokončení aktualizace znovu nainstalovat.

  Postup odinstalace serveru lokality pasivního režimu:
  1. V konzole nástroje klikněte na **Správa** > **Přehled** > **Konfigurace** > **servery lokality a role systému lokality**a potom vyberte server lokality pasivního režimu.
  2. V podokně **role systému lokality** klikněte pravým tlačítkem na roli **serveru lokality** a pak zvolte **Odebrat roli**.
  3. Klikněte pravým tlačítkem na server lokality pasivního režimu a zvolte **Odstranit**.
  4. Po odinstalaci serveru lokality na aktivním serveru primární lokality restartujte službu **CONFIGURATION_MANAGER_UPDATE**.

**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-to-run-task-sequence"></a>Vylepšení spuštění pořadí úloh
<!-- 1261338 -->

V této verzi Technical Preview se vylepšit krok spuštění pořadí úkolů. Mezi vylepšení patří následující položky:

- Podpora všech scénářů nasazení operačního systému z centra softwaru, technologie PXE a médií.
- Vylepšení akcí konzoly, jako je kopírování, import, export a upozornění při odstraňování objektu.
- Podpora pro průvodce **vytvořením připraveného obsahu** .
- Integrace s ověřováním nasazení.
- Krok pořadí úkolů spustit se teď dá použít na více úrovních pořadí úkolů, nikoli jenom na jeden vztah nadřazený-podřízený. Vztahy na více úrovních zvyšují složitost, proto používejte s opatrností. U těchto vztahů se pořád kontroluje cyklické odkazy.

### <a name="try-it-out"></a>Určitě to udělejte!  

Zkuste provést následující úkoly a pak nám poslat **zpětnou vazbu** z karty **Domů** na pásu karet a sdělte nám, jak se pracovalo:

1. V editoru pořadí úloh klikněte na tlačítko **Přidat**, vyberte možnost **Obecné**a klikněte na možnost **Spustit pořadí úloh**.
2. Kliknutím na **Procházet** vyberte podřízené pořadí úkolů.

## <a name="allow-user-interaction-when-installing-an-application----1356976---"></a>Při instalaci aplikace povolte interakci s uživatelem. <!-- 1356976 -->

V této verzi Preview můžete koncovému uživateli dovolit, aby při spuštění pořadí úkolů komunikoval s instalací aplikace. Například spusťte proces instalace, který vyzve koncového uživatele k zadání různých možností. Některé instalační programy aplikace nemůžou mít netiché výzvy pro uživatele nebo proces instalace může vyžadovat konkrétní hodnoty konfigurace známé jenom pro uživatele. Tato funkce umožňuje zvládnout tyto scénáře instalace.

### <a name="try-it-out"></a>Určitě to udělejte!

Zkuste dokončit následující úkoly a potom poslat **zpětnou vazbu** z karty **Domů** na pásu karet a sdělte nám, jak se pracovalo:

1.  Vytvoří nebo upraví aplikaci. Další informace najdete v tématu [vytváření aplikací pomocí Configuration Manager](../../apps/deploy-use/create-applications.md).

    a. Vyberte kartu **činnost koncového uživatele** ve **vlastnostech Instalační služba systému Windows\*(soubor MSI)**.

    b. Pro **chování instalace**vyberte **instalovat pro systém** .

    c. Vyberte **, zda je uživatel přihlášen** pro **požadavek na přihlášení**.

    d. Pro **viditelnost instalačního programu**vyberte **normální** . Můžete vybrat ze tří možností: **minimalizované**, **normální**nebo **maximalizované**.

    e. Zaškrtněte políčko **povolí uživatelům interakci s instalací programu** .

2.  Vytvořte nebo upravte pořadí úkolů pro instalaci aplikace pomocí kroku **instalovat aplikaci** . Další informace najdete v tématu [instalace aplikace](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication) v [krocích pořadí úkolů](../../osd/understand/task-sequence-steps.md).

    a. Pořadí úkolů pro vytváření imagí za krokem nastavení a Configuration Manager.

    b. Pořadí úkolů místního upgradu ve skupině po zpracování.

3.  Nasaďte pořadí úkolů do klienta.
4.  Nainstalujte pořadí úkolů z centra softwaru.

Během procesu pořadí úkolů se na cílovém zařízení koncového uživatele zobrazí rozhraní instalace aplikace. Průběh pořadí úkolů se pozastaví, dokud koncový uživatel nedokončí pracovní postup instalace aplikace.

### <a name="install-using-the-wizard"></a>Instalace pomocí Průvodce

Tuto funkci můžete také použít při nasazování aplikace pomocí průvodce.

1. Vytvoří nebo upraví aplikaci.
2. Nasaďte aplikaci na klienta.
3. Nainstalujte aplikaci z centra softwaru. Mělo by se zobrazit rozhraní instalace aplikace. Koncový uživatel by měl postupovat podle Průvodce instalací aplikace a aplikace bude úspěšně nainstalována.




<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Další kroky
Informace o instalaci nebo aktualizaci větve Technical Preview najdete v tématu [Technical Preview pro Configuration Manager](technical-preview.md).    
