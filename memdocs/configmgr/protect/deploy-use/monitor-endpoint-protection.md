---
title: Monitorování stavu služby Endpoint Protection
titleSuffix: Configuration Manager
description: Přečtěte si, jak monitorovat Endpoint Protection ve vaší hierarchii Configuration Manager.
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f4a1335c-bb3d-493e-a124-83a32a107dc8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 18bbbfc6486a1e5a784603e6725629d966f6c11a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722274"
---
# <a name="how-to-monitor-endpoint-protection-status"></a>Jak monitorovat stav Endpoint Protection

*Platí pro: Configuration Manager (Current Branch)*

Endpoint Protection v hierarchii Microsoft Configuration Manager můžete monitorovat pomocí uzlu **stav Endpoint Protection** pod položkou **zabezpečení** v pracovním prostoru **monitorování** , uzlu **Endpoint Protection** v pracovním prostoru **prostředky a kompatibilita** a pomocí sestav.  

##  <a name="how-to-monitor-endpoint-protection-by-using-the-endpoint-protection-status-node"></a><a name="BKMK_1"></a>Postup monitorování Endpoint Protection pomocí uzlu stav Endpoint Protection  

1. V konzole Configuration Manager klikněte na **monitorování**.  

2. V pracovním prostoru **monitorování** rozbalte **zabezpečení** a pak klikněte na **Endpoint Protection stav**.  

3. V seznamu **kolekce** vyberte kolekci, pro kterou chcete zobrazit informace o stavu.  

   > [!IMPORTANT]
   >  Kolekce jsou k dispozici pro výběr v následujících případech:  
   > 
   > - Když vyberete možnost **Zobrazit tuto kolekci na řídicím panelu Endpoint Protection** na kartě **výstrahy** v dialogovém okně**vlastnosti** <em>názvu\>kolekce<</em>.  
   >   -   Když do kolekce nasadíte Endpoint Protection antimalwarové zásady.  
   >   -   Když povolíte a nasadíte Endpoint Protection nastavení klienta do kolekce.  

4. Projděte si informace, které se zobrazí v částech **stav zabezpečení** a **provozní stav** . Kliknutím na libovolný stavový odkaz můžete vytvořit dočasnou kolekci v uzlu **Zařízení** v pracovním prostoru **Prostředky a kompatibilita**. Dočasná kolekce obsahuje počítače s vybraným stavem.  

   > [!IMPORTANT]  
   >  Informace, které se zobrazují v uzlu **stav Endpoint Protection** , jsou založené na posledních datech, která byla shrnuta z databáze Configuration Manager a nemusí být aktuální. Pokud chcete načíst nejnovější data, na kartě **Domů** klikněte na **Spustit shrnutí** nebo klikněte na **Naplánovat shrnutí** a upravte interval shrnutí.  

##  <a name="how-to-monitor-endpoint-protection-in-the-assets-and-compliance-workspace"></a><a name="BKMK_2"></a>Postup monitorování Endpoint Protection v pracovním prostoru prostředky a kompatibilita  

1.  V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.  

2.  V pracovním prostoru **prostředky a kompatibilita** proveďte jednu z následujících akcí:  

    -   Klikněte na **Zařízení**. V seznamu **Zařízení** vyberte počítač, a poté klikněte na kartu **Podrobnosti o malwaru** .  

    -   Klikněte na **kolekce zařízení**. V seznamu **Kolekce zařízení** vyberte kolekci obsahující počítač, který chcete monitorovat, a poté na kartě **Domů** ve skupině **Kolekce** klikněte na **Zobrazit členy**.  

3.  V seznamu *<název\> kolekce* vyberte počítač a pak klikněte na kartu **Podrobnosti o malwaru** .  

##  <a name="how-to-monitor-endpoint-protection-by-using-reports"></a><a name="BKMK_3"></a>Jak monitorovat Endpoint Protection pomocí sestav  
 Následující sestavy vám pomůžou zobrazit informace o Endpoint Protection ve vaší hierarchii. Pomocí těchto sestav můžete také řešit problémy s Endpoint Protection. Další informace o tom, jak nakonfigurovat vytváření sestav v Configuration Manager, najdete v tématu [Úvod do vytváření sestav](../../core/servers/manage/introduction-to-reporting.md) a [souborů protokolů](../../core/plan-design/hierarchy/log-files.md). Sestavy Endpoint Protection jsou ve složce Endpoint Protection.  

|Název sestavy|Popis|  
|-----------------|-----------------|  
|**Sestava o antimalwarové aktivitě**|Zobrazuje přehled antimalwarových aktivit pro konkrétní kolekci.|  
|**Nakažené počítače**|Zobrazuje seznam počítačů, ve kterých byla zjištěná zadaná hrozba.|  
|**Nejohroženější uživatelé podle hrozeb**|Zobrazuje seznam uživatelů s největším počtem zjištěných hrozeb.|  
|**Seznam hrozeb pro uživatele**|Zobrazuje seznam hrozeb zjištěných pro zadaný uživatelský účet.|  

## <a name="malware-alert-levels"></a>Úrovně výstrah malwaru  
 Pomocí následující tabulky Identifikujte různé Endpoint Protection úrovně výstrah, které se mohou zobrazit v sestavách nebo v konzole Configuration Manager.  

|Úroveň výstrahy|Popis|  
|-----------------|-----------------|  
|**Failed**|Endpoint Protection se nepovedlo opravit malware. Podrobnosti o chybě najdete v protokolech.<br /><br /> **Poznámka:** Seznam souborů protokolu Configuration Manager a Endpoint Protection najdete v části "Endpoint Protection" v tématu [soubory protokolu](../../core/plan-design/hierarchy/log-files.md) .|  
|**Odebráno**|Endpoint Protection úspěšně odebral malware.|  
|**V karanténě**|Endpoint Protection přesunula malware do zabezpečeného umístění a zabránila jeho spuštění, dokud ho neodeberete nebo nepovolíte jeho spuštění.|  
|**Vyčištěno**|Malware se z nakaženého souboru vyčistil.|  
|**Povoleno**|Uživatel s právy pro správu se rozhodl povolit spuštění softwaru, který obsahuje malware.|  
|**Žádná akce**|Endpoint Protection neprováděla žádnou akci s malwarem. Tato situace může nastat, když se počítač po zjištění malwaru restartuje a malware už se nedetekuje, třeba když se mapovaná síťová jednotka, na které byl malware zjištěný, po restartování počítače už nepřipojí.|  
|**Blokováno**|Endpoint Protection zablokovala spuštění malwaru. Tato situace může nastat, když se zjistí, že malware je obsažený v procesu v počítači.|
