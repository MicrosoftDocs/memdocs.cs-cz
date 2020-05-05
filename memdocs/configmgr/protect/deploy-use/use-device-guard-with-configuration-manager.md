---
title: Správa řízení aplikací v programu Windows Defender
titleSuffix: Configuration Manager
description: Naučte se používat Configuration Manager ke správě řízení aplikací v programu Windows Defender.
ms.date: 11/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f9aff29d2773c4994272317d5fcd486b83cba8d7
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210175"
---
# <a name="windows-defender-application-control-management-with-configuration-manager"></a>Správa řízení aplikací v programu Windows Defender pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

## <a name="introduction"></a>Úvod
Řízení aplikací v programu Windows Defender je navrženo k ochraně počítačů před malwarem a jiným nedůvěryhodným softwarem. Zabrání spuštění škodlivého kódu tím, že zajistí, že lze spustit pouze schválený kód, který znáte.

Řízení aplikací v programu Windows Defender je softwarová vrstva zabezpečení, která vynutila explicitní seznam softwaru, který může běžet v počítači. Vlastní ovládací prvek aplikace nemá žádné požadavky na hardware nebo firmware. Zásady řízení aplikací nasazené pomocí Configuration Manager umožňují zásadu na počítačích v cílových kolekcích, které splňují požadavky na minimální verzi Windows a SKU uvedené v tomto článku. V případě potřeby lze ochranu na základě hypervisoru zásad řízení aplikací nasazenou prostřednictvím Configuration Manager povolit prostřednictvím Zásady skupiny na hardwaru podporujícím technologii.

Další informace o řízení aplikací v programu Windows Defender najdete v [Průvodci nasazením řízení aplikací v programu Windows Defender](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide).

   > [!NOTE]
   > - Počínaje systémem Windows 10 verze 1709 jsou konfigurovatelné zásady integrity kódu známé jako řízení aplikací v programu Windows Defender.
   > - Od verze Configuration Manager 1710 byly zásady ochrany zařízení přejmenovány na zásady řízení aplikací v programu Windows Defender.

## <a name="using-windows-defender-application-control-with-configuration-manager"></a>Použití řízení aplikací v programu Windows Defender s Configuration Manager

Configuration Manager můžete použít k nasazení zásad řízení aplikací v programu Windows Defender. Tato zásada vám umožní nakonfigurovat režim, ve kterém se řízení aplikací v programu Windows Defender spouští na počítačích v kolekci. 

Můžete nakonfigurovat jeden z následujících režimů:

1. **Vynucení povoleno** – spustit se můžou jenom důvěryhodné spustitelné soubory.
2. **Jenom audit** – povolí spouštění všech spustitelných souborů, ale protokoluje nedůvěryhodné spustitelné soubory, které běží v protokolu událostí místního klienta.

> [!Tip]  
> Tato funkce byla poprvé představena ve verzi 1702 jako [funkce předběžné verze](../../core/servers/manage/pre-release-features.md). Od verze 1906 už není k dispozici funkce předběžného vydání.  

## <a name="what-can-run-when-you-deploy-a-windows-defender-application-control-policy"></a>Co se dá spustit při nasazení zásad řízení aplikací v programu Windows Defender?

Řízení aplikací v programu Windows Defender vám umožní silně řídit, co se dá spouštět na počítačích, které spravujete. Tato funkce může být užitečná pro počítače v oblastech s vysokým zabezpečením, kde je důležité, aby nemohly běžet nežádoucí software.

Když nasadíte zásadu, můžou se spustit následující spustitelné soubory:

- Součásti operačního systému Windows
- Ovladače softwaru pro vývojáře hardwaru (které mají signatury Windows Hardware Quality Labs)
- Aplikace pro Windows Store
- Klient Configuration Manager 
- Veškerý software nasazený prostřednictvím Configuration Manager počítač nainstaloval po zpracování zásad řízení aplikací v programu Windows Defender. 
- Aktualizace součástí systému Windows z:
    - Windows Update
    - web Windows Update pro firmy
    - Windows Server Update Services
    - Configuration Manager
    - Volitelně je software s dobrou pověstí, který je určený Microsoft Intelligent Security Graph (ISG). ISG zahrnuje filtr SmartScreen v programu Windows Defender a další služby Microsoftu. Aby bylo možné tento software důvěřovat, musí mít zařízení spuštěný filtr SmartScreen v programu Windows Defender a Windows 10 verze 1709 nebo novější.

>[!IMPORTANT]
>Tyto položky neobsahují žádný software, který *není integrovaný do* Windows, který automaticky aktualizuje z Internetu nebo aktualizací softwaru třetích stran, ať už jsou nainstalované prostřednictvím kteréhokoli mechanismu aktualizace uvedeného výše, nebo z Internetu. Pouze změny softwaru nasazené, i když je možné spustit klienta Configuration Manager.

## <a name="before-you-start"></a>Než začnete

Než nakonfigurujete nebo nasadíte zásady řízení aplikací v programu Windows Defender, přečtěte si následující informace:

- Správa řízení aplikací v programu Windows Defender je předběžná verze funkce pro Configuration Manager a může se změnit.
- Pokud chcete používat řízení aplikací v programu Windows Defender s Configuration Manager, počítače, které spravujete, musí mít Windows 10 Enterprise verze 1703 nebo novější.
- Po úspěšném zpracování zásady na klientském počítači je Configuration Manager nakonfigurovaný jako spravovaný Instalační program na tomto klientovi. Software, který prostřednictvím něj byl nasazen, je po procesech zásad automaticky důvěryhodný. Software nainstalovaný v Configuration Manager před tím, než se procesy zásad řízení aplikací v programu Windows Defender nebudou automaticky důvěřovat.
- Výchozí plán vyhodnocení dodržování předpisů pro zásady řízení aplikací, který se dá konfigurovat během nasazení, je každý den. Pokud jsou pozorovány problémy při zpracování zásad, může být vhodné nakonfigurovat plán vyhodnocení dodržování předpisů tak, aby byl kratší, například každou hodinu. Tento plán určuje, jak často se klienti při selhání pokoušejí zpracovat zásadu řízení aplikací v programu Windows Defender.
- Bez ohledu na zvolený režim vynucení se při nasazování zásad řízení aplikací v programu Windows Defender nemůžou v klientských počítačích spouštět aplikace HTML s příponou. hta.

## <a name="how-to-create-a-windows-defender-application-control-policy"></a>Postup vytvoření zásad řízení aplikací v programu Windows Defender
1. V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.
2. V pracovním prostoru **prostředky a kompatibilita** rozbalte položku **Endpoint Protection**a potom klikněte na položku **řízení aplikací v programu Windows Defender**.
3. Na kartě **Domů** ve skupině **vytvořit** klikněte na možnost **vytvořit zásadu řízení aplikací**.
4. Na stránce **Obecné** v **Průvodci vytvořením zásad řízení aplikací**zadejte následující nastavení:
    - **Název** – zadejte jedinečný název pro tyto zásady řízení aplikací v programu Windows Defender. 
    - **Popis** – volitelně zadejte popis zásady, který vám pomůže ho identifikovat v konzole Configuration Manager.
    - **Vynutil restart zařízení, aby se tyto zásady mohly vymáhat pro všechny procesy** – po zpracování zásady na KLIENTSKÉm počítači se na straně klienta naplánoval restart podle **nastavení klienta** pro **restartování počítače**.
        - Zařízení se systémem Windows 10 verze 1703 nebo starší se vždy automaticky restartují.
        - Počínaje systémem Windows 10 verze 1709 nebudou aplikace aktuálně spuštěné v zařízení mít pro ně uplatněny nové zásady řízení aplikací, dokud nebudou restartovány. Aplikace spuštěné po použití zásad ale budou dodržovat nové zásady řízení aplikací. 
    - **Režim vynucení** – vyberte jednu z následujících metod vynucení pro řízení aplikací v programu Windows Defender v klientském počítači.
        - **Vynucení povoleno** – povolit spuštění pouze důvěryhodných spustitelných souborů.
        - **Jenom audit** – povolí spouštění všech spustitelných souborů, ale protokoluje nedůvěryhodné spustitelné soubory, které běží v protokolu událostí místního klienta.
5. Na kartě **zahrnutí** v **Průvodci vytvořením zásad řízení aplikací**vyberte, jestli chcete **autorizovat software, který je důvěryhodný pro Intelligent Security Graph**.
6. Klikněte na tlačítko **Přidat** , pokud chcete přidat vztah důvěryhodnosti pro konkrétní soubory nebo složky na počítačích. V dialogovém okně **Přidat důvěryhodný soubor nebo složku** můžete zadat místní soubor nebo cestu ke složce, pro kterou chcete důvěřovat. Můžete také zadat cestu k souboru nebo složce na vzdáleném zařízení, ke kterému máte oprávnění k připojení. Když přidáte vztah důvěryhodnosti pro konkrétní soubory nebo složky v zásadách řízení aplikací v programu Windows Defender, můžete:
    - Překonání problémů s chováním spravované instalační služby
    - Důvěřovat obchodním aplikacím, které se nedají nasadit pomocí Configuration Manager
    - Důvěřujte aplikacím, které jsou součástí bitové kopie nasazení operačního systému. 
8. Kliknutím na tlačítko **Další**dokončete průvodce.

>[!IMPORTANT]
>Zahrnutí důvěryhodných souborů nebo složek je podporováno pouze v klientských počítačích, na kterých běží verze 1706 nebo novější klienta Configuration Manager. Pokud jsou některá pravidla zahrnutí obsažená v zásadách řízení aplikací v programu Windows Defender a tato zásada se pak nasadí do klientského počítače se starší verzí v Configuration Manager klientovi, zásada se nepovede použít. Při upgradu těchto starších klientů se tento problém vyřeší. Zásady, které neobsahují žádná pravidla zahrnutí, mohou být nadále aplikovány na starší verze klienta Configuration Manager.

## <a name="how-to-deploy-a-windows-defender-application-control-policy"></a>Postup nasazení zásad řízení aplikací v programu Windows Defender
1. V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.
2. V pracovním prostoru **prostředky a kompatibilita** rozbalte položku **Endpoint Protection**a potom klikněte na položku **řízení aplikací v programu Windows Defender**.
3. V seznamu zásad vyberte tu, kterou chcete nasadit, a potom na kartě **Domů** ve skupině **nasazení** klikněte na **nasadit zásadu řízení aplikací**.
4. V dialogovém okně **nasadit zásadu řízení aplikací** vyberte kolekci, do které chcete zásady nasadit. Pak nakonfigurujte plán, kdy budou klienti vyhodnocovat zásady. Nakonec vyberte, zda může klient vyhodnotit zásady mimo všechna nakonfigurovaná časová období údržby.
5. Po dokončení klikněte na **OK** , aby se zásady nasadily. 

<!--Reworked article to put this inline while working on VSO 1355092
### Restarting the device after deploying the policy

After the policy is processed on a client PC, a restart is scheduled on that client according to the **Client Settings** for **Computer Restart**. A restart is not required to apply policies, but it is the default. If you want to turn off restarts, follow these steps:

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **General** page, clear the check box for **Enforce a restart of devices so that this policy can be enforced for all processes**.
3. Click **Next** until the wizard completes.-->


## <a name="how-to-monitor-a-windows-defender-application-control-policy"></a>Jak monitorovat zásady řízení aplikací v programu Windows Defender

Informace v článku [monitorování nastavení dodržování předpisů](../../compliance/deploy-use/monitor-compliance-settings.md) vám pomůžou monitorovat, jestli se nasazené zásady použily na všechny počítače správně.

Chcete-li monitorovat zpracování zásad řízení aplikací v programu Windows Defender, použijte následující soubor protokolu na klientských počítačích:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Pokud chcete ověřit, jestli je konkrétní software blokovaný nebo auditováný, podívejte se na následující protokoly událostí místního klienta:

1. Pro blokování a auditování spustitelných souborů > použijte **protokoly aplikací a služeb**operační systém**Microsoft** > **Windows** > –**Integrita** > kódu v**provozu**.
2.  > Pro blokování a auditování souborů Instalační služba systému Windows a skriptu použijte **protokoly aplikací a služeb****Microsoft** > **Windows** > **AppLocker** > **MSI a Script**.

<!--Reworked article to put this inline while working on VSO 1355092
## Automatically let software run if it is trusted by Intelligent Security Graph

You can let locked-down devices run software with a good reputation as determined by the Microsoft Intelligent Security Graph (ISG). The ISG includes [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) and other Microsoft services. The devices must be running Windows Defender SmartScreen for this software to be trusted.

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **Inclusions** page, check the box for **Authorize software that is trusted by the Intelligent Security Graph**.
3. Click **Next** until the wizard completes.
-->


## <a name="security-and-privacy-information-for-windows-defender-application-control"></a>Informace o zabezpečení a ochraně osobních údajů pro řízení aplikací v programu Windows Defender

- V této předběžné verzi nesaďte zásady řízení aplikací v programu Windows Defender s **auditem** režimu vynucení pouze v produkčním prostředí. Tento režim je určený k tomu, aby vám pomohly testovat možnosti jenom v nastavení testovacího prostředí.
- Zařízení, která mají nasazenou zásadu v režimu **jenom pro auditování** nebo **vynucení** , která se nespustila pro vynucování zásad, jsou zranitelná při instalaci nedůvěryhodného softwaru.
V takovém případě může být software nadále povolen i v případě, že se zařízení restartuje nebo obdrží zásadu v režimu **povolených vynucení** .
- Chcete-li zajistit, aby zásady řízení aplikací v programu Windows Defender byly platné, připravte zařízení v testovacím prostředí. Pak Nasaďte zásadu s **povoleným vynucováním** a nakonec restartujte zařízení, než mu udělíte koncovým uživatelům zařízení.
- Nesaďte zásadu s **povoleným vynucením**a pak později Nasaďte zásadu s **auditem jenom** na stejné zařízení. Tato konfigurace může mít za následek neoprávněné spuštění nedůvěryhodného softwaru.
- Když použijete Configuration Manager k povolení řízení aplikací v programu Windows Defender na klientských počítačích, zásada nebrání uživatelům s oprávněními místního správce obejít zásady řízení aplikací nebo jinak spouštět nedůvěryhodný software. 
- Jediným způsobem, jak zabránit uživatelům s oprávněními místního správce zakázat řízení aplikací je nasadit binární zásady se znaménkem. Toto nasazení je možné prostřednictvím Zásady skupiny, ale aktuálně se v Configuration Manager nepodporuje.
- Nastavení Configuration Manager jako spravovaného instalačního programu na klientských počítačích používá zásady AppLockeru. AppLocker se používá pouze k identifikaci spravovaných instalačních programů a veškerá vynucení se provádí pomocí řízení aplikací v programu Windows Defender. 

## <a name="next-steps"></a>Další kroky

 [Správa antimalwarových zásad a nastavení brány firewall](endpoint-antimalware-firewall.md)



