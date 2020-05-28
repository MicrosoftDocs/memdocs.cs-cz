---
title: Support Center
titleSuffix: Configuration Manager
description: Řešení potíží s Configuration Manager klienty pomocí nástroje Support Center.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c631197d-7daa-4faa-9e22-980cd6d604c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: da2fe2ad66617ffb5ad3058011f111b0aaf9e9ae
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82903915"
---
# <a name="support-center-for-configuration-manager"></a>Support Center pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

<!--1357489-->
Od verze 1810 použijte Support Center pro řešení potíží klienta, zobrazení protokolu v reálném čase nebo pro zachycení stavu Configuration Manager klientského počítače pro pozdější analýzu. Support Center je jedním z nástrojů pro konsolidaci mnoha nástrojů pro odstraňování potíží správců.


## <a name="about"></a>Informace

Support Center se zaměřuje na snížení výzev a frustrace při řešení potíží Configuration Manager klientských počítačích. Když jste dřív pracovali s podporou řešení potíží s Configuration Manager klienty, museli byste ručně shromažďovat soubory protokolů a další informace, které vám pomůžou problém vyřešit. Nechtěně zapomenete zásadní soubor protokolu, což způsobí další souvisejícím problémům správou pro vás a pracovníky podpory, se kterými pracujete.

Pomocí nástroje Support Center můžete zjednodušit možnosti podpory. Umožňuje vám:

- Vytvořte sadu prostředků pro odstraňování potíží (soubor. zip), která obsahuje soubory protokolu klienta Configuration Manager. Pak budete mít jeden soubor, který se odešle pracovníkům podpory.  

- Zobrazuje Configuration Manager soubory protokolů klienta, certifikáty, nastavení registru, výpisy ladění, zásady klienta.  

- Diagnostika inventáře v reálném čase (nahrazuje ContentSpy), zásady (nahradí PolicySpy) a mezipaměť klienta.  

### <a name="support-center-viewer"></a>Support Center Viewer

Support Center zahrnuje Support Center Viewer, nástroj, který pracovníkům podpory umožňuje otevřít sady souborů, které vytvoříte pomocí nástroje Support Center. Kolekce dat v nástroji Support Center shromažďuje a balí protokoly diagnostiky z místního nebo vzdáleného Configuration Manager klienta. Chcete-li zobrazit sady kolekcí dat, použijte aplikaci prohlížeče.

### <a name="support-center-log-file-viewer"></a>Prohlížeč souborů protokolu Support Center

Support Center zahrnuje moderní prohlížeč protokolů. Tento nástroj nahrazuje CMTrace a poskytuje přizpůsobitelné rozhraní s podporou karet a oken ukotvit. Má rychlou prezentační vrstvu a dokáže načíst velké soubory protokolů během několika sekund.

### <a name="support-center-onetrace-preview"></a>Support Center OneTrace (Preview)

<!--3555962-->
Počínaje verzí 1906 je **OneTrace** nový prohlížeč protokolů s nástrojem Support Center. Funguje podobně jako CMTrace, s vylepšeními. Další informace najdete v tématu [Support Center OneTrace](support-center-onetrace.md).

### <a name="powershell-cmdlets"></a>Rutiny prostředí PowerShell

Support Center zahrnuje také [rutiny PowerShellu](https://docs.microsoft.com/powershell/sccm/overview?view=sccm-ps). Pomocí těchto rutin můžete vytvořit vzdálené připojení k jinému Configuration Manager klientovi, nakonfigurovat možnosti shromažďování dat a spustit shromažďování dat.


## <a name="prerequisites"></a>Požadavky

Do serveru nebo klientského počítače, na který nainstalujete Support Center, nainstalujte následující komponenty:

- Verze operačního systému podporovaná nástrojem Configuration Manager. Další informace najdete v tématu [podporované verze operačních systémů pro klienty](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md). Support Center nepodporuje mobilní zařízení.  

- V počítači, na kterém spouštíte nástroje Support Center a jeho komponenty, je vyžadován .NET Framework 4.5.2.  


## <a name="install"></a>Instalace

Na serveru lokality vyhledejte instalační program nástroje Support Center v následující cestě: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi` .

Po instalaci nástroje vyhledejte v nabídce Start ve skupině nástroje **Microsoft System Center** následující položky:  

- Support Center (ConfigMgrSupportCenter. exe)  
- Prohlížeč souborů protokolu Support Center (CMLogViewer. exe)  
- Support Center Viewer (ConfigMgrSupportCenterViewer. exe)  


## <a name="known-issues"></a>Známé problémy

### <a name="you-cant-install-the-latest-version-if-an-older-version-is-already-installed"></a>Nemůžete nainstalovat nejnovější verzi, pokud už je nainstalovaná starší verze.

<!--SCCMDocs-pr issue #3090-->
*Platí pro verze 1810 a 1902.*

Pokud už máte nainstalovanou starší verzi nástroje Support Center, nový instalační program se nezdařil. K tomuto problému dochází z důvodu verze souborů mezi původní verzí a nejnovější verzí. Pokud chcete tento problém obejít, nejdřív odinstalujte starší verzi nástroje Support Center. Pak nainstalujte nejnovější verzi.

### <a name="remote-connections-must-include-computer-name-or-domain-as-part-of-the-user-name"></a>Vzdálená připojení musí jako součást uživatelského jména obsahovat název počítače nebo doménu.

Pokud se připojíte ke vzdálenému klientovi z nástroje Support Center, musíte při navazování připojení zadat název počítače nebo název domény pro uživatelský účet. Pokud používáte zkrácený název počítače nebo název domény (například `.\administrator` ), připojení je úspěšné, ale Support Center neshromažďuje data z klienta.

Chcete-li se tomuto problému vyhnout, použijte následující formáty uživatelských jmen pro připojení ke vzdálenému klientovi:

- `ComputerName\UserName`  
- `DomainName\UserName`  

### <a name="scripted-server-message-block-connections-to-remote-clients-might-require-removal"></a>Připojení blokových zpráv serveru ke vzdáleným klientům může vyžadovat odebrání.

Při připojování ke vzdáleným klientům pomocí rutiny [New-CMMachineConnection](https://go.microsoft.com/fwlink/p/?linkid=390542) prostředí PowerShell vytvoří Support Center připojení SMB (Server Message Block) ke každému vzdálenému klientovi. Po dokončení shromažďování dat tato připojení zachová. Aby nedošlo k překročení maximálního počtu vzdálených připojení pro Windows, pomocí `net use` příkazu Zobrazte aktuálně aktivní sadu vzdálených připojení. Pak zakažte všechna nepotřebná připojení pomocí následujícího příkazu:`net use <connection_name> /d`
kde `<connection_name>` je název vzdáleného připojení.

### <a name="application-deployment-evaluation-cycle-request-isnt-sent-correctly-to-remote-machines"></a>Požadavek na cyklus hodnocení nasazení aplikace není na vzdálených počítačích správně odeslán.

<!--2849356-->
*Platí pro verzi 1810*

Pokud v nástroji Support Center vyberete možnost **vyhodnocení nasazení aplikace** z akce **vyvolání triggeru** na kartě **obsah** , spustí Tato akce úkol, který vyhodnotí nasazené aplikace. Pokud jste připojeni k místnímu klientovi, vyhodnotí se tím nasazení uživatelských aplikací i počítačů. Pokud jste ale připojení ke vzdálenému klientovi, vyhodnocuje jenom nasazení aplikací pro počítače.


## <a name="next-steps"></a>Další kroky

[Rychlý Start pro Support Center](support-center-quickstart.md)
