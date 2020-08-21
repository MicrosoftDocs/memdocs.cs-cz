---
title: Technical Preview 1710 | Microsoft Docs
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview verze 1710 pro Configuration Manager.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4706a58-1f11-4eab-b1eb-3d1a0da02d0f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e408bbe7ea88d70c5a9d02368c2d820584cae2b8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694436"
---
# <a name="capabilities-in-technical-preview-1710-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1710 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1710. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview. Před instalací této verze Technical Preview si přečtěte [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md) , abyste se seznámili se všeobecnými požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Známé problémy v této verzi Technical Preview:**
- **Podpora pro Windows 10 verze 1709 (označovaná také jako aktualizace tvůrců v rámci služby Updates)**.  Od této verze Windows Windows Media obsahuje několik edicí. Při konfiguraci pořadí úkolů pro použití balíčku s upgradem operačního systému nebo bitové kopie operačního systému nezapomeňte vybrat [edici, která je podporována pro použití v Configuration Manager](../plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).
- **Aktualizace na novou verzi Preview se nezdařila, pokud máte server lokality v pasivním režimu**. Když spustíte verzi Preview, která má [server primární lokality v pasivním režimu](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), je nutné před tím, než budete moct úspěšně aktualizovat lokalitu Preview na tuto novou verzi Preview, odinstalovat server lokality pasivního režimu. Server lokality v pasivním režimu můžete po dokončení aktualizace znovu nainstalovat.

  Postup odinstalace serveru lokality pasivního režimu:
  1. V konzole nástroje klikněte na **Správa**  >  **Přehled**  >  **Konfigurace**  >  **servery lokality a role systému lokality**a potom vyberte server lokality pasivního režimu.
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

## <a name="improvements-for-deploying-powershell-scripts-from-configuration-manager"></a>Vylepšení pro nasazení skriptů PowerShellu z Configuration Manager
V této verzi teď skripty PowerShellu, které nasadíte, podporují použití následujících vylepšení: 
- **Obory zabezpečení**.  Skripty nyní používají obory zabezpečení k řízení vytváření a spouštění skriptů. To se provádí prostřednictvím přiřazení značek, které reprezentují skupiny uživatelů. Další informace o používání oborů zabezpečení najdete v tématu [Konfigurace správy na základě rolí pro Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).
- **Sledování v reálném čase**. Když monitorete běh skriptu, je nyní v reálném čase jako skript spuštěn.
- **Ověřování parametru**. Každý parametr ve vašem skriptu má dialogové okno **vlastností parametru skriptu** , pomocí kterého můžete přidat ověřování pro tento parametr. Po přidání ověřování byste měli získat chyby, pokud zadáváte hodnotu pro parametr, který nesplňuje jeho ověření.

Nasazení skriptů PowerShellu se poprvé představilo v Technical Preview Technical [preview 1706](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console). Další vylepšení byla poskytována ve verzi [tech preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) a potom ve [verzi Preview 1708](capabilities-in-technical-preview-1708.md#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager).


### <a name="try-it-out"></a>Určitě to udělejte!

Pokud si chcete vyzkoušet použití funkce spustit skripty, přečtěte si téma [Vytvoření a spuštění skriptů](../../apps/deploy-use/create-deploy-scripts.md).



## <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Omezit rozšířená data Windows 10 tak, aby odesílala jenom data relevantní pro Windows Analytics Stav zařízení
<!-- 1356148 -->

V této verzi teď můžete nastavit úroveň shromažďování diagnostických dat Windows 10 na hodnotu **Rozšířené (s omezením)**. Toto nastavení umožňuje získat užitečné informace o zařízeních ve vašem prostředí bez toho, aby zařízení nahlásí všechna data v **Rozšířené** úrovni s Windows 10 verze 1709 nebo novější.

Rozšířená (omezená) úroveň zahrnuje metriky ze základní úrovně a také podmnožinu dat shromážděných ze **zvýšené** úrovně relevantní pro Windows Analytics.


## <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Centrum softwaru už nedeformovaný ikony větší než 250x250  
<!-- 1356194 -->

V této verzi přestane Centrum softwaru derušit ikony, které jsou větší než 250x250. Centrum softwaru tyto ikony vypadá rozmazaně. Nyní můžete nastavit ikonu s rozměry v pixelech až na 512x512 a ta se zobrazí bez zkreslení.

### <a name="try-it-out"></a>Určitě to udělejte!
Přidejte ikonu pro aplikaci v centru softwaru. Pokud ho chcete vyzkoušet, podívejte se na téma [Vytvoření aplikací](../../apps/deploy-use/create-applications.md).


## <a name="check-compliance-from-software-center-for-co-managed-devices"></a>Ověření dodržování předpisů v centru softwaru pro spoluspravovaná zařízení
<!-- 1356374 -->
V této verzi můžou uživatelé pomocí centra softwaru kontrolovat kompatibilitu svých zařízení s Windows 10, a to i v případě, že je podmíněný přístup spravovaný přes Intune. Podrobnosti najdete v tématu [společná správa pro zařízení s Windows 10](./capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices).


## <a name="support-for-exploit-guard"></a>Podpora ochrany před zneužitím
Tato verze přidává podporu pro ochranu před zneužitím v programu Windows Defender. Můžete nakonfigurovat a nasadit zásady, které spravují všechny čtyři součásti ochrany před zneužitím. Mezi tyto komponenty patří:
-   Omezení možností útoku
-   Řízený přístup ke složkám
-   Ochrana Exploit Protection
-   Ochrana sítě

Data dodržování předpisů pro nasazení zásad ochrany proti zneužití jsou k dispozici v rámci konzoly Configuration Manager.

Další informace o ochraně před zneužitím a konkrétních komponent a pravidel najdete v tématu [zneužití ochrany v programu Windows Defender](/windows/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard) v knihovně dokumentace systému Windows.

### <a name="prerequisites"></a>Předpoklady
Spravovaná zařízení musí používat Windows 10 1709: creators Update nebo novější a splňují následující požadavky v závislosti na nakonfigurovaných součástech a pravidlech:

|Součást ochrany před zneužitím |Další požadavky|
|------------------------|------------------------|
| Omezení možností útoku  | Zařízení musí mít povolenou [ochranu v reálném čase v programu Windows Defender AV]( /windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) .  |
| Řízený přístup ke složkám  | Zařízení musí mít povolenou [ochranu v reálném čase v programu Windows Defender AV]( /windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) .   |
| Ochrana Exploit Protection  | Žádné  |
| Ochrana sítě  |  Zařízení musí mít povolenou [ochranu v reálném čase v programu Windows Defender AV]( /windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) .  |

### <a name="create-an-exploit-guard-policy----1355468---"></a>Vytvoření zásady ochrany před zneužitím  <!--1355468 -->
1. V konzole Configuration Manager přejděte na **prostředky a kompatibilita**  >  **Endpoint Protection**a pak klikněte na **zneužití ochrany před zneužitím v programu Windows Defender**.
2. Na kartě **Domů** ve skupině **vytvořit** klikněte na možnost **vytvořit zásadu zneužití**.
3. Na stránce **Obecné** v **průvodci vytvořením položky konfigurace**zadejte název a volitelný popis položky konfigurace.
4. V dalším kroku vyberte součásti zneužití Guard, které chcete s touto zásadou spravovat. Pro každou vybranou součást pak můžete nakonfigurovat další podrobnosti.
   - **Omezení možností útoku:** Nakonfigurujte hrozbu Office, hrozby skriptování a hrozby e-mailů, které chcete zablokovat nebo auditovat. Z tohoto pravidla můžete taky vyloučit konkrétní soubory nebo složky.
   - **Řízený přístup ke složkám:** Nakonfigurujte blokování nebo auditování a pak přidejte aplikace, které tuto zásadu můžou obejít.  Můžete také zadat další složky, které nejsou chráněny ve výchozím nastavení.
   - **Ochrana před zneužitím:**  Zadejte soubor XML, který obsahuje nastavení pro zmírnění zneužití systémových procesů a aplikací. Tato nastavení můžete exportovat z aplikace Security Center v programu Windows Defender na zařízení s Windows 10.
   - **Ochrana sítě:** Nastavení ochrany sítě pro blokování nebo auditování přístupu k podezřelým doménám.
5. Dokončete průvodce a vytvořte zásadu, kterou můžete později nasadit do zařízení.

### <a name="deploy-an-exploit-guard-policy"></a>Nasazení zásady ochrany před zneužitím     
Až vytvoříte zásady ochrany před zneužitím, nasadíte je pomocí Průvodce nasazením zásad ochrany před zneužitím. Provedete to tak, že otevřete konzolu Configuration Manager pro **prostředky a dodržování předpisů**  >  **Endpoint Protection**a potom kliknete na **nasadit zásady ochrany před zneužitím**.

## <a name="limited-support-for-cng-certificates"></a>Omezená podpora pro certifikáty CNG
<!-- 1356191 -->
Od této verze teď můžete používat šablony certifikátů [kryptografické rozhraní API: nové generace (CNG)](/windows/win32/seccng/cng-features) pro následující scénáře:

- Registrace klienta a komunikace s bodem správy HTTPS.   
- Distribuce softwaru a nasazení aplikací s distribučním bodem HTTPS.   
- Nasazení operačního systému.  
- Sada SDK pro zasílání zpráv klienta (s nejnovější aktualizací) a ISV proxy.   
- Konfigurace Brána pro správu cloudu.  

K používání certifikátů CNG musí vaše certifikační autorita (CA) poskytovat šablony certifikátů CNG pro cílové počítače.  Podrobnosti o šabloně se liší v závislosti na scénáři. jsou však požadovány následující vlastnosti:

- Karta **Kompatibilita**

    - **Certifikační autorita** musí být Windows Server 2008 nebo novější. (Doporučuje se Windows Server 2012.)

    - **Příjemce certifikátu** musí být Windows Vista/Server 2008 nebo novější. (Doporučuje se Windows 8/Windows Server 2012.)

- Karta **kryptografie**

    - **Kategorie poskytovatele** musí být **poskytovatelem úložiště klíčů**.  Požadovanou

Pro dosažení nejlepších výsledků doporučujeme sestavit název subjektu z informací služby Active Directory.  Pro **Formát názvu subjektu** použijte název DNS a do alternativního názvu subjektu zadejte název DNS.  V opačném případě je nutné tyto informace zadat, když se zařízení zaregistruje do profilu certifikátu.


## <a name="improved-descriptions-for-pending-computer-restarts-----1356283---"></a>Vylepšené popisy pro probíhající restart počítače   <!--1356283 -->
Ve [verzi Technical preview 1708](capabilities-in-technical-preview-1708.md#restart-computers-from-the-configuration-manager-console)jsme přidali možnost identifikovat zařízení, která čekají na restartování v konzole Configuration Manager.

Od této verze Technical Preview se v konzole nástroje zobrazí další podrobnosti, které obsahují informace o procesu nebo akci, která žádá o restartování.

## <a name="device-guard-policy-changes----1355092---"></a>Změny zásad Device Guard <!-- 1355092 -->
V rámci sestavení 1710 Technical Preview byly provedeny následující tři změny ve vztahu k zásadám ochrany zařízení:

### <a name="device-guard-policies-renamed-to-windows-defender-application-control-policies"></a>Zásady ochrany zařízení se přejmenovaly na zásady řízení aplikací v programu Windows Defender
Zásady ochrany zařízení se přejmenovaly na zásady řízení aplikací v programu Windows Defender. Například **Průvodce vytvořením zásad pro ochranu zařízení** se teď jmenuje **Průvodce vytvořením zásad řízení aplikací v programu Windows Defender**.

### <a name="restart-is-not-required-to-apply-policies"></a>Pro uplatnění zásad není nutné restartovat počítač.
Od Creators Update pro Windows verze 1709 se pro zařízení, která používají novou verzi Windows, nevyžaduje restart, aby mohl použít zásady řízení aplikací v programu Windows Defender.

Výchozím nastavením je restartování.

#### <a name="try-it-out"></a>Určitě to udělejte!  

Pokud chcete restartování vypnout, postupujte takto:

1.  Otevřete Průvodce **vytvořením zásad řízení aplikací v programu Windows Defender** .
2.  Na stránce **Obecné** zrušte zaškrtnutí políčka pro **vykonání restartování zařízení, aby bylo možné tuto zásadu vyhovět pro všechny procesy**.
3.  Klikněte na **Další** , dokud se průvodce nedokončí.

Pro starší verze Windows se stále vynutilo automatizované restartování.

### <a name="automatically-run-software-trusted-by-the-intelligent-security-graph"></a>Automaticky spouštět software důvěryhodný Intelligent Security Graph

Správci mají nyní možnost, aby byla zamčeným zařízením umožněno spouštění důvěryhodného softwaru s dobrou pověstí, jak je určeno Microsoft Intelligent Security Graph (ISG). ISG se skládá z filtru SmartScreen v programu Windows Defender a dalších služeb společnosti Microsoft.

V zařízeních musí být spuštěný filtr SmartScreen v programu Windows Defender, aby byl software důvěryhodný.

#### <a name="try-it-out"></a>Určitě to udělejte!  

Pokud chcete nechat zařízení, které spouští filtr SmartScreen v programu Windows Defender, použít důvěryhodný software, postupujte takto:

1.  Otevřete **Průvodce vytvořením zásad řízení aplikací v programu Windows Defender**.
2.  Na stránce **zahrnutí** zaškrtněte políčko pro **autorizaci softwaru, který je důvěryhodný pro Intelligent Security Graph**.
3.  V poli **důvěryhodné soubory nebo složka** přidejte soubory a složky, které chcete důvěřovat.
4.  Klikněte na **Další** , dokud se průvodce nedokončí.

## <a name="configure-and-deploy-windows-defender-application-guard-policies----1351960---"></a>Konfigurace a nasazení zásad ochrany Application Guard v programu Windows Defender <!-- 1351960 -->

[Ochrana Application Guard v programu Windows Defender](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) je nová funkce systému Windows, která pomáhá chránit uživatele otevřením nedůvěryhodných webů v zabezpečeném izolovaném kontejneru, který není přístupný jiným součástem operačního systému. V této verzi Technical Preview jsme přidali podporu pro konfiguraci této funkce pomocí Configuration Manager nastavení dodržování předpisů, která nakonfigurujete a následně nasadíte do kolekce. Tato funkce bude vydána v Preview pro 64 verzi aktualizace Windows 10 Creator. Pokud chcete tuto funkci nyní otestovat, musíte použít verzi Preview této aktualizace.

### <a name="before-you-start"></a>Než začnete
Aby bylo možné vytvářet a nasazovat zásady ochrany Application Guard v programu Windows Defender, musí být na zařízeních s Windows 10, na která tyto zásady nasazujete, nakonfigurovaná zásada izolace sítě. Další informace najdete v blogovém příspěvku, na který se odkazuje později. Tato funkce funguje jenom s aktuálními sestaveními Windows 10 Insider. K otestování musí být na vašich klientech spuštěné poslední sestavení Windows 10 Insider.

### <a name="try-it-out"></a>Určitě to udělejte!

Pokud chcete pochopit základy ochrany Application Guard v programu Windows Defender, přečtěte si [Blogový příspěvek](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97).

Chcete-li vytvořit zásadu a vyhledat dostupná nastavení:
1. V konzole **Configuration Manager** vyberte **prostředky a kompatibilita**.
2. V pracovním prostoru **prostředky a kompatibilita** vyberte **Přehled**  >  **Endpoint Protection**  >  **ochrana Application Guard v programu Windows Defender**.
3. Na kartě **Domů** ve skupině **vytvořit** klikněte na možnost **vytvořit zásadu Application Guard v programu Windows Defender**.
4. Pomocí příspěvku na blogu jako reference můžete vyhledat a nakonfigurovat dostupná nastavení, abyste mohli tuto funkci vyzkoušet.
5. V této verzi jsme přidali novou stránku definice sítě do průvodce. Zde zadejte podnikovou identitu a definujte hranici vaší podnikové sítě.

    > [!NOTE]
    > Počítače s Windows 10 ukládají na klientovi jenom jeden seznam izolace sítě. V této verzi můžete vytvořit dva různé druhy seznamů izolace sítě (jeden ze systému Windows Information Protection a jeden z ochrany Application Guard v programu Windows Defender) a nasadit je do klienta. Pokud nasadíte obě zásady, musí tyto seznamy izolace sítě odpovídat. Pokud nasadíte seznamy, které se neshodují se stejným klientem, nasazení se nezdaří.

    Další informace o tom, jak zadat definice sítě v dokumentaci [Windows Information Protection], najdete v tématu [Ochrana podnikových dat pomocí Windows Information Protection (NV)](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr).

6. Až skončíte, dokončete průvodce a Nasaďte zásadu na jedno nebo více zařízení s Windows 10.

### <a name="further-reading"></a>Další materiály

Další informace o ochraně Application Guard v programu Windows Defender najdete v [tomto blogovém příspěvku](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Další informace o samostatném režimu ochrany Application Guard v programu Windows Defender najdete v [tomto blogovém příspěvku](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).

## <a name="next-steps"></a>Další kroky
Informace o instalaci nebo aktualizaci větve Technical Preview najdete v tématu [Technical Preview pro Configuration Manager](technical-preview.md).