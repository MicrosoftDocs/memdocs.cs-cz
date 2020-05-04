---
title: Služby a příkazy klientské součásti systému UNIX/Linux
titleSuffix: Configuration Manager
description: Přečtěte si o službách komponent a příkazech v klientech se systémy Linux a UNIX v Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de564595ce51a336b5f11d4050928fa812269601
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713342"
---
# <a name="linux-and-unix-clients-component-services-and-commands-for-configuration-manager"></a>Služby a příkazy klientů se systémy Linux a UNIX pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

> [!Important]  
> Počínaje verzí 1902 Configuration Manager nepodporuje klienty se systémy Linux a UNIX. 
> 
> Zvažte Microsoft Azure správu pro správu serverů se systémem Linux. Řešení Azure mají rozsáhlou podporu pro Linux, která ve většině případů překračuje Configuration Manager funkce, včetně ucelené správy oprav pro Linux.


 Následující tabulka určuje služby komponent klienta klienta Configuration Manager pro systémy Linux a UNIX.  

|Název souboru|Další informace|  
|---------------|----------------------|  
|ccmexec.bin|Tato služba je podobná službě službě ccmexc u klienta se systémem Windows. Zodpovídá za veškerou komunikaci s Configuration Manager rolemi systému lokality a také komunikuje se službou omiserver. bin ke shromáždění inventáře hardwaru z místního počítače.<br /><br /> Seznam podporovaných argumentů příkazového řádku získáte spuštěním příkazu.`ccmexec -h`|  
|omiserver.bin|Tato služba je server CIM. Server CIM poskytuje rozhraní pro připojitelné softwarové moduly nazývané poskytovatelé. Poskytovatelé komunikují s prostředky počítače se systémem Linux a UNIX a shromažďují data inventáře hardwaru. Například **poskytovatel procesů** pro počítače se systémem Linux shromažďuje data související s procesy operačního systému Linux.|  

 Následující tabulky uvádějí příkazy, které můžete použít ke spuštění, zastavení nebo restartování služeb klienta (ccmexec.bin a omiserver.bin) v každé verzi systému Linux nebo UNIX. Při spuštění nebo zastavení služby ccmexec se služba omiserver taky spustí nebo zastaví.  

|Operační systém|Příkazy|  
|----------------------|--------------|  
|Universal Agent<br /><br /> RHEL 4 a SLES 9|Čína`/etc/init d/ccmexecd start`<br /><br /> Stop:`/etc/init d/ccmexecd stop`<br /><br /> Službu`/etc/init d/ccmexecd restart`|  
|Solaris 9|Čína`/etc/init d/ccmexecd start`<br /><br /> Stop:`/etc/init d/ccmexecd stop`<br /><br /> Službu`/etc/init d/ccmexecd restart`|  
|Solaris 10|Spuštění:<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> Zastavení:<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|Solaris 11|Spuštění:<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> Zastavení:<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|AIX|Spuštění:<br /><br /> `startsrc -s omiserver`<br /><br /> `startsrc -s ccmexec`<br /><br /> Zastavení:<br /><br /> `stopsrc -s ccmexec`<br /><br /> `stopsrc -s omiserver`|  
|HP-UX|Čína`/sbin/init.d/ccmexecd start`<br /><br /> Stop:`/sbin/init.d/ccmexecd stop`<br /><br /> Službu`/sbin/init.d/ccmexecd restart`|  
