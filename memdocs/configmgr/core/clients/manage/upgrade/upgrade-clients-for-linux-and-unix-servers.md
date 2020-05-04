---
title: Upgrade klientů Linux a UNIX
titleSuffix: Configuration Manager
description: Upgrade klienta na serveru se systémem Linux nebo UNIX v Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7d2bb377-1005-4a55-bd1f-b80a6d0b22e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f71a36dff92f888d595538ff2fd483d7c212358f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715393"
---
# <a name="how-to-upgrade-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Postup upgradu klientů pro servery se systémy Linux a UNIX v nástroji Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

> [!Important]  
> Počínaje verzí 1902 Configuration Manager nepodporuje klienty se systémy Linux a UNIX. 
> 
> Zvažte Microsoft Azure správu pro správu serverů se systémem Linux. Řešení Azure mají rozsáhlou podporu pro Linux, která ve většině případů překračuje Configuration Manager funkce, včetně ucelené správy oprav pro Linux.

Verzi klienta pro Linux a UNIX v počítači můžete upgradovat na novější verzi klienta a nemusíte přitom aktuálního klienta odinstalovat. Pokud to chcete udělat, nainstalujte do počítače nový instalační balíček klienta a použijte vlastnost příkazového řádku **-keepdb** . Když se klient pro Linux a UNIX nainstaluje, přepíše stávající klientská data novými soubory. Vlastnost příkazového řádku **-keepdb** ale přesměruje proces instalace tak, aby zachoval jedinečný identifikátor klientů (GUID), místní databázi informací a úložiště certifikátů. Tyto informace se potom využijí novou klientskou instalací.  

 Představte si třeba, že máte počítač RHEL5 x64, ve kterém se spouští klient z původního vydání klienta Configuration Manageru pro Linux a UNIX. Pokud chcete tohoto klienta upgradovat na verzi klienta z kumulativní aktualizace 1, ručně spuštěním **instalačního** skriptu nainstalujete příslušný balíček klienta z kumulativní aktualizace 1 s přidáním přepínače příkazového řádku **-keepdb** . Podívejte se na následující příklad příkazového řádku:  

`./install -mp <hostname\> -sitecode <code\> -keepdb ccm-Universal-x64.<build\>.tar`  



## <a name="how-to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Použití nasazení softwaru k upgradu klientů na serverech s Linuxem a UNIXem  
 Pomocí nasazení softwaru můžete upgradovat klienta pro Linux a UNIX na novou verzi. Klient Configuration Manager ale nemůže přímo spustit instalační skript pro instalaci nového klienta, protože instalace nového klienta musí nejdřív odinstalovat aktuálního klienta. Tato akce způsobí ukončení procesu Configuration Manager klienta, který spouští instalační skript před zahájením instalace nového klienta. Chcete-li úspěšně použít nasazení softwaru pro instalaci nového klienta, je třeba naplánovat, aby se instalace spouštěla v budoucím čase a aby ji bylo možné spustit pomocí možností plánování integrovaných v operačním systému.  

 K prvnímu zkopírování souborů pro nový instalační balíček klienta do klientského počítače použijte nasazení softwaru. Pak nasaďte a spusťte skript pro naplánování procesu instalace klienta. Skript k odložení svého spuštění používá integrovaný příkaz **v** operačním systému. Po spuštění skriptu je jeho operace spravována klientským operačním systémem, nikoli klientem Configuration Manager v počítači. Toto chování umožňuje příkazovému řádku, který skript volá, aby nejdřív odinstaloval klienta Configuration Manager a pak nainstaloval nového klienta. Tyto akce dokončí proces upgradu klienta v počítači se systémem Linux nebo UNIX. Po dokončení upgradu zůstane upgradovaný klient spravovaný pomocí Configuration Manager.  

 Následující postup vám pomůže nakonfigurovat nasazení softwaru pro upgrade klienta pro Linux a UNIX. Následující kroky a příklady upgradují počítač RHEL5 x64, ve kterém je spuštěná počáteční verze klienta, na klientskou verzi kumulativní aktualizace 1.  

#### <a name="to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Použití nasazení softwaru k upgradu klientů na serverech s Linuxem a UNIXem  

1. Zkopírujte instalační balíček nového klienta do počítače, na kterém je spuštěný klient nástroje Configuration Manager, a proveďte upgrade.  

    Instalační balíček klienta můžete umístit například do následujícího umístění v klientském počítači a nainstalovat skript pro kumulativní aktualizaci 1: **/TMP/patch**  

2. Vytvořte skript pro správu upgradu klienta Configuration Manager. Pak umístěte kopii skriptu do stejné složky v klientském počítači jako instalační soubory klienta z kroku 1.  

    Skript nevyžaduje konkrétní název. Musí obsahovat příkazové řádky, které jsou dostatečné pro použití instalačních souborů klienta z místní složky v klientském počítači a k instalaci instalačního balíčku klienta pomocí vlastnosti příkazového řádku **-keepdb** . Pomocí vlastnosti příkazového řádku **-keepdb** Udržujte jedinečný identifikátor aktuálního klienta, který chcete použít pro nového klienta, kterého instalujete.  

    Vytvořte například skript s názvem **upgrade.sh** , který obsahuje následující řádky:  

   ```  
   #!/bin/sh  
   #  
   /tmp/PATCH/install -sitecode <code> -mp <hostname> -keepdb /tmp/PATCH/ccm-Universal-x64.<build>.tar  

   ```  

    Pak ho zkopírujte do složky **/TMP/patch** v klientském počítači.

3. Pomocí nasazení softwaru klienta nechte každého klienta použít integrovaný počítačový příkaz **at** ke spuštění skriptu **upgrade.sh** (s krátkou prodlevou před spuštěním).  

    Ke spuštění skriptu například použijte následující příkazový řádek: on **-f/TMP/upgrade.sh-m Now + 5 minut**  

   Když klient úspěšně naplánuje spuštění skriptu **upgrade.sh** , odešle stavovou zprávu s informací, že nasazení softwaru se úspěšně dokončilo. Vlastní instalaci klienta ale pak po nastavené prodlevě spravuje počítač. Po dokončení upgradu klienta ověřte instalaci kontrolou souboru **/var/opt/microsoft/scxcm.log** v klientském počítači. Ověřte, že je klient nainstalován a komunikuje s lokalitou, zobrazením podrobností o klientovi v uzlu **zařízení** v pracovním prostoru prostředky **a kompatibilita** v konzole Configuration Manager.  
