---
title: Plánování služby Endpoint Protection
titleSuffix: Configuration Manager
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 7610bbd3-a67f-4a09-8115-e35d40d43b42
author: mestew
ms.author: mstewart
manager: dougeby
description: Plánování antimalwarových zásad a zabezpečení brány Windows Firewall
ms.openlocfilehash: 2e3904b7b7232e92fd4a246d2e0519ef32fb67f6
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606831"
---
# <a name="planning-for-endpoint-protection-in-configuration-manager"></a>Plánování pro Endpoint Protection v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*


Endpoint Protection v Configuration Manager vám umožní spravovat antimalwarové zásady a zabezpečení brány Windows Firewall pro klientské počítače ve vaší hierarchii Configuration Manager.  

> [!IMPORTANT]  
>  Abyste mohli spravovat klienty ve vaší Configuration Manager hierarchii, musíte mít licenci, aby používala Endpoint Protection.  

Pokud používáte Endpoint Protection s Configuration Manager, máte následující výhody:  

-   Konfigurace antimalwarových zásad, nastavení brány Windows Firewall a Správa rozšířené ochrany před internetovými útoky v programu Microsoft Defender na vybrané skupiny počítačů  

-   Pomocí Configuration Manager aktualizace softwaru si stáhněte nejnovější soubory antimalwarových definic, aby byly klientské počítače pořád aktuální.  

-   Můžete odesílat e-mailová oznámení, používat sledování v rámci konzoly a zobrazovat sestavy, aby měli správci průběžné informace o malwaru zjištěném na klientských počítačích.  

Počítače s Windows 10 nevyžadují žádné další klienty pro správu ochrany koncových bodů. Na Windows 8.1 a starších počítačích Endpoint Protection nainstaluje kromě klienta Configuration Manager i svého vlastního klienta. Klient aplikace Endpoint Protection nabízí tyto možnosti:  

-   Zjišťování a náprava malwaru a spywaru  

-   Zjišťování a náprava rootkitů  

-   Vyhodnocení kritických ohrožení zabezpečení a automatické aktualizace definic a stroje  

-   Zjišťování ohrožení zabezpečení sítě pomocí aplikace Systém kontroly sítě  

-   Integrace se službou Cloud Protection pro hlášení malwaru společnosti Microsoft. Když se připojíte k této službě, program Windows Defender nebo klient Endpoint Protection může stáhnout nejnovější definice z centra ochrany před malwarem, pokud se v počítači zjistí neidentifikovaný malware.  

> [!NOTE]  
>  Klienta Endpoint Protection můžete nainstalovat na server se spuštěnou technologií Hyper-V a na hostované virtuální počítače s podporovanými operačními systémy. Aby nedocházelo k nadměrnému využití procesoru, Endpoint Protection akcí mají vestavěnou náhodnou prodlevu, aby se služby nespouštěly současně.  

  Endpoint Protection v Configuration Manager vám navíc umožní spravovat nastavení brány Windows Firewall v konzole Configuration Manager.  

 [Příklad scénáře: použití nástroje System Center Endpoint Protection k ochraně počítačů před malwarem](../deploy-use/scenarios-endpoint-protection.md) ukazuje, jak můžete konfigurovat a spravovat Endpoint Protection a bránu Windows Firewall.  

## <a name="managing-malware-with-endpoint-protection"></a>Správa malwaru pomocí aplikace Endpoint Protection  

Endpoint Protection v Configuration Manager umožňuje vytvářet antimalwarové zásady, které obsahují nastavení pro Endpoint Protection konfigurace klientů. Pak můžete tyto antimalwarové zásady nasadit do klientských počítačů a monitorovat je v uzlu **stav Endpoint Protection** v pracovním prostoru **monitorování** nebo pomocí sestav Configuration Manager.  

 Další informace:  

-   [Vytvoření a nasazení antimalwarových zásad pro Endpoint Protection](../deploy-use/endpoint-antimalware-policies.md) – vytváření, nasazování a sledování antimalwarových zásad se seznamem nastavení, která můžete nakonfigurovat  

-   [Monitorujte Endpoint Protection](../deploy-use/monitor-endpoint-protection.md) – monitorování sestav aktivit, nakažených klientských počítačů a další.   

-   [Správa antimalwarových zásad a nastavení brány firewall pro Endpoint Protection](../deploy-use/endpoint-antimalware-firewall.md) – můžete změnit prioritu zásad pro [antimalware](../deploy-use/endpoint-antimalware-firewall.md#manage-antimalware-policies) nebo [bránu firewall](../deploy-use/endpoint-antimalware-firewall.md#manage-windows-firewall-policies), [opravit malware nalezený v klientských počítačích](../deploy-use/endpoint-antimalware-firewall.md#remediate-detected-malware)a další úlohy.

## <a name="managing-windows-firewall-with-endpoint-protection"></a>Správa brány Windows Firewall pomocí aplikace Endpoint Protection  
 Endpoint Protection v Configuration Manager poskytuje základní správu brány Windows Firewall v klientských počítačích. Pro každý profil sítě můžete nakonfigurovat tato nastavení:  

-   Povolení nebo zákaz brány Windows Firewall  

-   Blokování příchozích připojení včetně těch, která se nachází na seznamu povolených programů  

-   Upozornění uživateli, když brána Windows Firewall zablokuje nový program  

> [!NOTE]  
>  Aplikace Endpoint Protection podporuje jenom správu brány Windows Firewall.  

  Další informace o tom, jak vytvořit a nasadit zásady brány Windows Firewall pro Endpoint Protection, najdete v tématu [Postup vytvoření a nasazení zásad brány Windows Firewall pro Endpoint Protection](../deploy-use/create-windows-firewall-policies.md).  

## <a name="microsoft-defender-advanced-threat-protection"></a>Rozšířená ochrana před internetovými útoky v programu Microsoft Defender

Počínaje verzí 1606 Configuration Manager (Current Branch) může Endpoint Protection spravovat a monitorovat rozšířenou ochranu před internetovými útoky v programu Microsoft Defender, dříve označované jako ochrana ATP v programu Windows Defender. Microsoft Defender ATP je služba, která podnikům pomůže odhalit, prozkoumat a reagovat na pokročilé útoky v jejich sítích. Viz [Rozšířená ochrana před internetovými útoky v programu Microsoft Defender](../deploy-use/defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Pracovní postup aplikace Endpoint Protection  
 Následující diagram vám pomůže pochopit pracovní postup, který implementuje Endpoint Protection ve vaší Configuration Manager hierarchii.  

 ![Pracovní postup aplikace Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Klient aplikace Endpoint Protection pro počítače Mac a servery se systémem Linux  
 System Center zahrnuje klienta Endpoint Protection pro Linux a pro počítače Mac. Tito klienti nejsou dodávány s Configuration Manager. místo toho je nutné stáhnout následující produkty z [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).  

> [!IMPORTANT]  
>  Ke stažení instalačních souborů aplikace Endpoint Protection pro Linux a počítače Mac potřebujete multilicenci od Microsoftu.  

 Tyto produkty se nedají spravovat z konzoly nástroje Configuration Manager. S instalačními soubory se ale dodává sada Management Pack nástroje System Center Operations Manager, která umožňuje spravovat klienta pro Linux pomocí nástroje Operations Manager.  

 Další informace o tom, jak nainstalovat a spravovat klienty aplikace Endpoint Protection pro Linux a počítače Mac, najdete v dokumentaci dodávané s těmito produkty, která se nachází ve složce **Documentation** .

## <a name="best-practices-for-endpoint-protection-in-configuration-manager"></a>Doporučené postupy pro řešení Endpoint Protection v nástroji Configuration Manager  
 Používejte následující doporučené postupy pro řešení Endpoint Protection v nástroji System Center 2012 Configuration Manager.  

### <a name="configure-custom-client-settings-for-endpoint-protection"></a>Konfigurace vlastních nastavení klienta pro bod Endpoint Protection  
 Když konfigurujete nastavení klienta pro Endpoint Protection, nepoužívejte výchozí nastavení klienta, protože tato nastavení platí pro všechny počítače ve vaší hierarchii. Místo toho nakonfigurujte vlastní nastavení klienta a přiřaďte je kolekcím počítačů ve vaší hierarchii.  

 Při konfiguraci vlastních nastavení klienta můžete provést následující:  

-   Přizpůsobit antimalwarová nastavení a nastavení zabezpečení pro různé části vaší organizace.  
-   Před nasazením do celé hierarchie otestujte účinky spuštění Endpoint Protection v malých skupinách počítačů.  
-   V průběhu času přidejte do kolekce další klienty pro fázi nasazení Endpoint Protection klienta.  

### <a name="distributing-definition-updates-by-using-software-updates"></a>Distribuce aktualizací definic pomocí aktualizací softwaru  
 Pokud používáte Configuration Manager aktualizace softwaru k distribuci aktualizací definic, zvažte umístění aktualizací definic do balíčku, který neobsahuje jiné aktualizace softwaru. Tím se zmenší velikost balíčku aktualizací definic, což umožňuje urychlit replikaci do distribučních bodů.
