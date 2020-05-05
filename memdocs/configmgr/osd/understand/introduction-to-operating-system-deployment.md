---
title: Úvod k nasazení operačního systému
titleSuffix: Configuration Manager
description: Seznamte se s koncepty ještě před nasazením operačních systémů v prostředí Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d9a1c545-8301-492c-832f-2c108ff93c77
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d53ab2221e3ee936f9b09592a7c7b383b200c928
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720384"
---
# <a name="introduction-to-operating-system-deployment-in-configuration-manager"></a>Seznámení s nasazením operačního systému v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pomocí Configuration Manager můžete nasazovat operační systémy mnoha různými způsoby. Informace v této části vám povysvětlí, jak nasadit operační systémy a automatizovat úlohy. 

##  <a name="the-operating-system-deployment-process"></a><a name="BKMK_OSDeploymentProcess"></a>Proces nasazení operačního systému  
 Configuration Manager poskytuje několik metod, které můžete použít k nasazení operačního systému. Bez ohledu na konkrétní metodu nasazení, kterou zvolíte, je potřeba provést několik akcí:  

-   Identifikujte ovladače zařízení systému Windows potřebné ke spuštění spouštěcí image nebo k instalaci image operačního systému, které musíte nasadit.  

-   Identifikujte spouštěcí bitovou kopii, kterou chcete použít ke spuštění cílového počítače.  

-   Zaznamenejte image operačního systému, kterou chcete nasadit, pomocí pořadí úkolů. Případně můžete použít výchozí image operačního systému.  

-   Distribuujte spouštěcí bitovou kopii, bitovou kopii operačního systému a veškerý související obsah do distribučního bodu.  

-   Vytvořte pořadí úkolů obsahující kroky nasazení spouštěcí image a image operačního systému.  

-   Nasaďte pořadí úkolů do kolekce počítačů.  

-   Sledujte nasazení.  

##  <a name="operating-system-deployment-scenarios"></a><a name="BKMK_OSDScenarios"></a>Scénáře nasazení operačního systému  
 V Configuration Manager existuje mnoho scénářů nasazení operačního systému, které si můžete vybrat v závislosti na vašem prostředí a účelu instalace operačního systému.  Můžete třeba rozdělit existující počítač na oddíly a naformátovat ho pomocí nové verze Windows nebo aktualizovat Windows na nejnovější verzi. Pro usnadnění určení metody nasazení, která vyhovuje vašim potřebám, si Projděte [scénáře nasazení podnikových operačních systémů](../deploy-use/scenarios-to-deploy-enterprise-operating-systems.md).  Můžete si vybrat z těchto scénářů nasazení operačního systému:  

-   [Upgrade systému Windows na nejnovější verzi](../deploy-use/upgrade-windows-to-the-latest-version.md)  

-   [Aktualizace existujícího počítače na novou verzi Windows](../deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalace nové verze Windows do nového počítače (holý počítač)](../deploy-use/install-new-windows-version-new-computer-bare-metal.md)  

-   [Nahrazení existujícího počítače a nastavení přenosu](../deploy-use/replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="methods-to-deploy-operating-systems"></a><a name="BKMK_OSDMethods"></a>Metody nasazení operačních systémů  
 Existuje několik metod, které lze použít k nasazení operačních systémů pro Configuration Manager klientských počítačů.  

- **Nasazení inicializovaná technologií PXE**: Při nasazení inicializovaném technologií PXE si klientské počítače vyžádají nasazení prostřednictvím sítě. Při této metodě nasazení jsou bitová kopie operačního systému a spouštěcí bitová kopie systému Windows PE odeslány do distribučního bodu, jehož konfigurace akceptuje žádosti o spuštění pomocí technologie PXE. Další informace najdete v tématu [použití technologie PXE pro nasazení Windows přes síť s Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

- **Zpřístupnění operačních systémů v Centru softwaru**: Můžete nasadit operační systém a zpřístupnit ho v Centru softwaru. Klienti Configuration Manager můžou zahájit instalaci operačního systému z centra softwaru. Další informace najdete v tématu [nahrazení existujícího počítače a nastavení přenosů](../deploy-use/replace-an-existing-computer-and-transfer-settings.md).  

- **Nasazení pomocí vícesměrového vysílání**: Nasazení pomocí vícesměrového vysílání šetří šířku pásma sítě, protože odesílá data současně několika klientům (neodesílá jednotlivým klientům kopii dat prostřednictvím samostatného připojení). Při této metodě nasazení je bitová kopie operačního systému odeslána do distribučního bodu. Distribuční bod nasadí bitovou kopii na vyžádání klientského počítače. Další informace najdete v tématu [použití vícesměrového vysílání k nasazení Windows přes síť](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

- **Nasazení ze spouštěcího média**: Při nasazení ze spouštěcího média můžete nasadit operační systém při spuštění cílového počítače. Cílový počítač při spuštění získá pořadí úloh, bitovou kopii operačního systému a další vyžadovaný obsah ze sítě. Protože obsah není uložen na médiu, můžete ho aktualizovat bez nutnosti nového vytváření média. Další informace najdete v tématu [Vytvoření spouštěcího média](../deploy-use/create-bootable-media.md).  

- **Nasazení ze samostatného média**: Při nasazení ze samostatného média můžete nasadit operační systém za těchto podmínek:  

  - V prostředích, v nichž není praktické kopírovat bitovou kopii operačního systému nebo další velké balíčky prostřednictvím sítě.  

  - V prostředích bez připojení k síti nebo se síťovým připojením s malou šířkou pásma.  

    Další informace najdete v tématu [vytvoření samostatného média](../deploy-use/create-stand-alone-media.md).  

- **Nasazení z předzpracovaného média**: Při nasazení z předzpracovaného média můžete nasadit operační systém na počítač, který není úplně zřízený. Předzpracované médium je soubor ve formátu WIM (Windows Imaging Format), který se dá nainstalovat na holý počítač výrobce nebo v přípravném centru podniku, které není připojené k Configuration Managermu prostředí.  

   Později v prostředí Configuration Manager se počítač spustí pomocí spouštěcí image, která je k dispozici na médiu, a potom se připojí k bodu správy lokality pro dostupná pořadí úkolů, která dokončí proces stahování. Tato metoda nasazení snižuje objem síťového přenosu, protože bitová kopie a spouštěcí bitová kopie operačního systému jsou již uloženy v cílovém počítači. Můžete určit aplikace, balíčky a balíčky ovladačů, které mají být součástí předzpracovaného média. Další informace najdete v tématu [Vytvoření předzpracovaného média](../deploy-use/create-prestaged-media.md).  

##  <a name="boot-images"></a><a name="BKMK_BootImages"></a>Spouštěcí bitové kopie  
 Spouštěcí bitová kopie v Configuration Manager je image prostředí Windows PE (WinPE), která se používá při nasazení operačního systému. Spouštěcí image slouží ke spuštění počítače v prostředí WinPE, což je minimální operační systém s omezenými komponentami a službami, který připraví cílový počítač na instalaci Windows. Configuration Manager poskytuje dvě spouštěcí image: jednu pro podporu platforem x86 a druhou pro podporu platforem x64. Ty se považují za výchozí spouštěcí image. Spouštěcí bitové kopie, které vytvoříte a přidáte do Configuration Manager, se považují za vlastní image. Výchozí spouštěcí image se dají při aktualizaci Configuration Manager automaticky nahradit. Další informace o spouštěcích imagích najdete v tématu [Správa spouštěcích imagí](../get-started/manage-boot-images.md).  

##  <a name="operating--system-images"></a><a name="BKMK_OSImages"></a>Bitové kopie operačního systému  
 Image operačního systému v Configuration Manageru se ukládají ve formátu WIM (Windows Imaging) a představují zkomprimovanou kolekci referenčních souborů a složek, které jsou potřebné k úspěšné instalaci a konfiguraci operačního systému na počítači. Ve všech scénářích nasazení operačního systému musíte vybrat image operačního systému. Můžete použít výchozí image operačního systému nebo sestavit image operačního systému z referenčního počítače, který nakonfigurujete. Další informace najdete v tématu [Správa imagí operačního systému](../get-started/manage-operating-system-images.md).  

##  <a name="operating-system-upgrade-packages"></a><a name="BKMK_OSUpgradePackages"></a>Balíčky s upgradem operačního systému  
 Balíčky s upgradem operačního systému se používají k upgradu operačního systému. Jedná se o nasazení operačního systému inicializovaná při spuštění. Balíčky s upgradem operačního systému se importují do Configuration Manager z disku DVD nebo z připojeného souboru ISO. Další informace najdete v tématu [Správa balíčků s upgradem operačního systému](../get-started/manage-operating-system-upgrade-packages.md).  

##  <a name="media-to-deploy-operating-systems"></a><a name="BKMK_OSDMedia"></a>Média pro nasazení operačních systémů  
 Vytvořit lze několik druhů médií, která slouží k nasazení operačních systémů. Patří mezi ně záznamová média, která se používají k záznamu bitových kopií operačního systému, a dále samostatná, předzpracovaná a spouštěcí média, sloužící k nasazení operačního systému. Pomocí médií můžete nasadit operační systémy v počítačích, které nemají připojení k síti nebo mají připojení s malou šířkou pásma k vaší Configuration Manager lokalitě. Další informace o tom, jak používat média, najdete v tématu [Vytvoření média pořadí úkolů](../deploy-use/create-task-sequence-media.md).  

##  <a name="device-drivers"></a><a name="BKMK_DeviceDrivers"></a>Ovladače zařízení  
 Do cílových počítačů je možné nainstalovat ovladače zařízení, aniž by byly součástí nasazované bitové kopie operačního systému. Configuration Manager poskytuje katalog ovladačů, který obsahuje odkazy na všechny ovladače zařízení, které naimportujete do Configuration Manager. Katalog ovladačů se nachází v pracovním prostoru **Softwarová knihovna** a tvoří ho dva uzly: **Ovladače** a **Balíčky ovladačů**. Uzel **Ovladače** obsahuje seznam všech ovladačů, které jste do katalogu ovladačů importovali. Tento uzel můžete využít k zjištění podrobností o jednotlivých importovaných ovladačích, ke změně přiřazení balíčku ovladačů nebo spouštěcí bitové kopie, k povolení nebo zakázání ovladače atd. Další informace najdete v tématu [Správa ovladačů](../get-started/manage-drivers.md).  

##  <a name="save-and-restore-user-state"></a><a name="BKMK_OSDUserState"></a>Uložení a obnovení stavu uživatele  
 Při nasazení operačního systému můžete uložit stav uživatele z cílového počítače, nasadit operační systém a po nasazení operačního systému stav uživatele opět obnovit. Tento proces se obvykle používá při instalaci operačního systému na Configuration Manager klientský počítač.  

 Informace o stavu uživatele se zaznamenávají a obnovují pomocí pořadí úloh. Jakmile je informace o stavu uživatele zaznamenána, může být uložena jedním z těchto způsobů:  

- Data o stavu uživatele můžete uložit vzdáleně nakonfigurováním bodu migrace stavu. Pořadí úloh Zachytit odešle data do bodu migrace stavu. Po nasazení operačního systému pořadí úloh Obnovit data načte a obnoví v cílovém počítači stav uživatele.  

- Data o stavu uživatele můžete uložit místně v určené složce. Při tomto scénáři pořadí úloh Zachytit zkopíruje uživatelská data do konkrétní složky v cílovém počítači. Po nasazení operačního systému pořadí úloh Obnovit uživatelská data z tohoto umístění načte.  

- Můžete zadat pevné odkazy, které budou sloužit k obnovení uživatelských dat do původního umístění. Při tomto scénáři zůstávají data o stavu uživatele při odebrání starého operačního systému na disku. Po nasazení operačního systému pořadí úloh Obnovit použije pevné odkazy k obnovení dat o stavu uživatele do původního umístění.  

  Další informace najdete v informacích o [správě stavu uživatele](../get-started/manage-user-state.md).  

##  <a name="deploy-to-unknown-computers"></a><a name="BKMK_UnknownComputer"></a>Nasazení na neznámé počítače  
 Operační systém můžete nasadit do počítačů, které nejsou spravovány nástrojem Configuration Manager. V databázi Configuration Manager není žádný záznam o těchto počítačích. Tyto počítače se označují jako neznámé. Neznámé počítače zahrnují následující:  

- Počítač, na kterém není nainstalovaný klient Configuration Manager  

- Počítač, který není importován do Configuration Manager  

- Počítač, který není zjištěn nástrojem Configuration Manager  

  Další informace najdete v tématu [Příprava pro nasazení do neznámých počítačů](../get-started/prepare-for-unknown-computer-deployments.md).  

##  <a name="associate-users-with-a-computer"></a><a name="BKMK_UDA"></a>Přidružení uživatelů k počítači  
 Při nasazování operačního systému můžete přidružit uživatele k cílovému počítači, a umožnit tak spřažení uživatelských zařízení. Pokud přidružíte uživatele k cílovému počítači, může správce později provádět akce na jakémkoli počítači přidruženém tomuto uživateli, jako je nasazení aplikace do počítače konkrétního uživatele. Pokud však nasazujete operační systém, nelze ho nasadit do počítače konkrétního uživatele. Další informace najdete v tématu [přidružení uživatelů k cílovému počítači](../get-started/associate-users-with-a-destination-computer.md).  

##  <a name="use-task-sequences-to-automate-steps"></a><a name="BKMK_TaskSequences"></a>Automatizace kroků pomocí pořadí úkolů  
 Pořadí úkolů můžete vytvořit k provádění nejrůznějších úloh v prostředí Configuration Manager. Akce vykonávané pořadím úloh definují jednotlivé kroky pořadí úloh. Po spuštění pořadí úloh jsou na úrovni příkazového řádku prováděny akce jednotlivých kroků bez nutnosti zásahu uživatele. Pořadí úkolů můžete použít k těmto účelům:  

-   [Vytvoření pořadí úkolů pro instalaci operačního systému](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md)  

-   [Vytvoření pořadí úloh pro jiná nasazení než nasazení operačních systémů](../deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)  

-   [Vytvoření pořadí úloh pro zachycení operačního systému](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)  

-   [Vytvoření pořadí úkolů pro zachycení a obnovení stavu uživatele](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)  

-   [Vytvoření vlastního pořadí úkolů](../deploy-use/create-a-custom-task-sequence.md)  
