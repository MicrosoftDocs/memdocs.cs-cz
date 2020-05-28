---
title: Technical Preview 1707
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview verze 1707 pro Configuration Manager.
ms.date: 08/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cb405ba0-8792-4ab7-988b-2f835f3a9550
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4ddae3e4c4cf31cb05376bfa437d722f16652fad
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721315"
---
# <a name="capabilities-in-technical-preview-1707-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1707 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1707. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview. Před instalací této verze Technical Preview si přečtěte [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md) , abyste se seznámili se všeobecnými požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Známé problémy v této verzi Technical Preview:**
- **Aktualizace na verzi preview 1707 se nezdařila, pokud máte server lokality v pasivním režimu**. Pokud spustíte verzi Preview 1706 a máte [server primární lokality v pasivním režimu](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), je nutné nejprve odinstalovat server lokality pasivního režimu před tím, než bude možné úspěšně aktualizovat lokalitu Preview na verzi 1707. Server lokality v pasivním režimu můžete po spuštění lokality verze 1707 znovu nainstalovat.

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

## <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Podpora souborů Expresní instalace v klientu sdílené mezipaměti pro Windows 10 a Office 365
<!-- 1352486 -->
Od této verze sdílená mezipaměť podporuje distribuci souborů Expresní instalace obsahu pro Windows 10 a souborů aktualizací pro Office 365. Nevyžadují se žádné další konfigurace.

## <a name="surface-device-dashboard"></a>Řídicí panel zařízení Surface
<!--1355788-->
Řídicí panel zařízení Surface poskytuje informace o zařízeních Surface, která se nacházejí ve vašem prostředí. V konzole nástroje přejdete na **monitorování**  >  **Surface zařízení**. Můžete zobrazit následující:
- procento povrchů
- procento modelů Surface
- pět hlavních verzí operačního systému

Úplný seznam zařízení zobrazíte kliknutím na část v grafu **modely Surface** .  

## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Konfigurace a nasazení zásad ochrany Application Guard v programu Windows Defender
<!-- 1351960 -->

[Ochrana Application Guard v programu Windows Defender](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) je nová funkce systému Windows, která pomáhá chránit uživatele otevřením nedůvěryhodných webů v zabezpečeném izolovaném kontejneru, který není přístupný jiným součástem operačního systému. V této verzi Technical Preview jsme přidali podporu pro konfiguraci této funkce pomocí Configuration Manager nastavení dodržování předpisů, která nakonfigurujete a následně nasadíte do kolekce. Tato funkce bude vydávána ve verzi Preview verze 64 aktualizace pro tvůrce (kódový název: RS3) ve Windows 10. Pokud chcete tuto funkci nyní otestovat, musíte použít verzi Preview této aktualizace.

### <a name="before-you-start"></a>Než začnete

Aby bylo možné vytvářet a nasazovat zásady ochrany Application Guard v programu Windows Defender, musí být na zařízeních s Windows 10, na která tyto zásady nasazujete, nakonfigurovaná zásada izolace sítě. Další podrobnosti najdete v [tomto blogovém příspěvku](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Tato funkce funguje jenom s aktuálními sestaveními Windows 10 Insider. K otestování musí být na vašich klientech spuštěné poslední sestavení Windows 10 Insider.

### <a name="try-it-out"></a>Určitě to udělejte!

#### <a name="to-create-a-policy-and-to-browse-the-available-settings"></a>Chcete-li vytvořit zásadu a vyhledat dostupná nastavení:

1. V konzole Configuration Manager vyberte **prostředky a kompatibilita**.
2. V pracovním prostoru **prostředky a kompatibilita** vyberte **Přehled**  >  **Endpoint Protection**  >  **ochrana Application Guard v programu Windows Defender**.
3. Na kartě **Domů** ve skupině **vytvořit** klikněte na možnost **vytvořit zásadu Application Guard v programu Windows Defender**.
4. Pomocí příspěvku na blogu jako reference můžete vyhledat a nakonfigurovat dostupná nastavení, abyste mohli tuto funkci vyzkoušet.
5. V této verzi jsme přidali novou stránku **definice sítě** do průvodce. Na této stránce zadejte podnikovou identitu a definujte hranici vaší podnikové sítě.<br>Počítače s Windows 10 ukládají na klientovi jenom jeden seznam izolace sítě. V této verzi můžete vytvořit dva různé druhy seznamů izolace sítě (jeden ze systému Windows Information Protection a jeden z ochrany Application Guard v programu Windows Defender) a nasadit je do klienta. Pokud nasadíte obě zásady, musí tyto seznamy izolace sítě odpovídat. Pokud nasadíte seznamy, které se neshodují se stejným klientem, nasazení se nezdaří.
Další informace o tom, jak zadat definice sítě, najdete v [dokumentaci k Windows Information Protection](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr).

6. Až skončíte, dokončete průvodce a Nasaďte zásadu na jedno nebo více zařízení s Windows 10.

### <a name="further-reading"></a>Další čtení
Další informace o ochraně Application Guard v programu Windows Defender najdete v [tomto blogovém příspěvku](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Další informace o samostatném režimu ochrany Application Guard v programu Windows Defender najdete v [tomto blogovém příspěvku](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).

## <a name="add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Přidání parametrů při nasazení skriptů PowerShellu z Configuration Manager

<!-- 1236459 --->

V poslední verzi Technical Preview jsme zavedli novou funkci, která umožňuje [vytvářet a spouštět skripty PowerShellu z konzoly Configuration Manager](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console).
V této verzi Technical Preview jsme tuto možnost rozšířili. Configuration Manager nyní přečte skript prostředí PowerShell a zobrazí všechny parametry v Průvodci vytvořením skriptu. V průvodci můžete uvést hodnotu pro parametr, který se použije při spuštění skriptu. Případně můžete tento parametr nechat prázdné. Pokud to uděláte, budete muset při spuštění skriptu uvést hodnotu parametru.
V této verzi Technical Preview je nutné dodat všechny parametry, které skript vyžaduje. V budoucí verzi plánujeme zadat parametry skriptu jako volitelné.

### <a name="try-it-out"></a>Určitě to udělejte!

1. Při [vytváření a spouštění skriptů PowerShellu z konzoly Configuration Manager](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console)postupujte podle pokynů.
2. Na stránce nové **Parametry skriptu** v **Průvodci vytvořením skriptu**zvolte parametr a pak klikněte na **Upravit**.
3. Zadejte hodnotu parametru pro vybraný parametr a pak klikněte na tlačítko **OK**.
4. Dokončete průvodce.

Po spuštění skriptu budou použity hodnoty parametrů, které jste nakonfigurovali.
