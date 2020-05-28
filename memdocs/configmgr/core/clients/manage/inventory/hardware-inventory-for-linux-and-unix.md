---
title: Inventář hardwaru pro Linux a UNIX
titleSuffix: Configuration Manager
description: Přečtěte si, jak používat inventář hardwaru pro Linux a UNIX v Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1026d616-2a20-4fb2-8604-d331763937f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 84f4b822475111352c5dcf23f4868a1fa43ec3a7
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906271"
---
# <a name="hardware-inventory-for-linux-and-unix-in-configuration-manager"></a>Inventář hardwaru pro Linux a UNIX v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

> [!Important]  
> Počínaje verzí 1902 Configuration Manager nepodporuje klienty se systémy Linux a UNIX. 
> 
> Zvažte Microsoft Azure správu pro správu serverů se systémem Linux. Řešení Azure mají rozsáhlou podporu pro Linux, která ve většině případů překračuje Configuration Manager funkce, včetně ucelené správy oprav pro Linux.

Klient Configuration Manager pro systémy Linux a UNIX podporuje inventář hardwaru. Po shromáždění inventáře hardwaru můžete spustit zobrazení inventáře v Průzkumníku prostředků nebo v sestavách Configuration Manager a použít tyto informace k vytvoření dotazů a kolekcí, které umožňují následující operace:  

- Nasazení softwaru  

- Vynucení časových období údržby  

- Nasazení vlastního nastavení klienta  

Inventář hardwaru pro servery se systémy Linux a UNIX používá server s podporou standardu model CIM (Common Information Model) (CIM). Server CIM běží jako softwarová služba (nebo proces démon) a poskytuje infrastrukturu správy, která je založená na standardech DMTF (Distributed Management Task Force). Server CIM poskytuje podobné funkce jako infrastruktura Windows Management Infrastructure (WMI) CIM, která je dostupná v počítačích s Windows.  

Počínaje kumulativní aktualizací 1 klient pro Linux a UNIX používá open source **omiserver** verze 1.0.6 z **otevřené skupiny**. (Před kumulativní aktualizací 1 klienta jako server CIM používal **nanowbem** .)  

Server CIM se nainstaluje jako součást klienta pro Linux a UNIX. Klient pro systémy Linux a UNIX komunikuje přímo se serverem CIM a nepoužívá rozhraní WS-MAN serveru CIM. Při instalaci klienta je port WS-MAN na serveru CIM zablokovaný. Společnost Microsoft vyvinula server CIM, který je teď dostupný jako open source prostřednictvím projektu infrastruktury OMI (Open Management Infrastructure). Další informace o projektu OMI najdete na webu [The Open Group](https://www.opengroup.org/) .  

Inventář hardwaru na serverech se systémem Linux a UNIX funguje tak, že mapuje existující třídy a vlastnosti WMI Win32 na ekvivalentní třídy a vlastnosti pro servery Linux a UNIX. Toto mapování tříd a vlastností 1:1 umožňuje integraci inventáře hardwaru se systémem Linux a UNIX s Configuration Manager. Data inventáře ze serverů se systémem Linux a UNIX se zobrazí spolu s inventářem z počítačů se systémem Windows v konzole Configuration Manager a sestavách. Toto chování přináší konzistentní heterogenní prostředí pro správu.  

> [!TIP]  
>  K identifikaci různých serverů se systémem Linux a UNIX v dotazech a kolekcích můžete použít hodnotu **Popisek** pro třídu **Operační systém** .  

##  <a name="configuring-hardware-inventory-for-linux-and-unix-servers"></a><a name="BKMK_ConfigHardwareforLnU"></a> Konfigurace inventáře hardwaru pro servery se systémem Linux a UNIX  
 Pokud chcete konfigurovat inventář hardwaru, můžete použít výchozí nastavení klienta nebo si můžete vytvořit vlastní nastavení. Když použijete vlastní nastavení klientského zařízení, můžete nakonfigurovat třídy a vlastnosti, které chcete shromažďovat jenom ze serverů se systémy Linux a UNIX. Můžete taky zadat vlastní plány, kdy se ze serverů se systémem Linux a UNIX budou shromažďovat úplné a rozdílové inventáře.  

 Klient pro Linux a UNIX podporuje následující třídy inventáře dat které jsou dostupné na serverech se systémem Linux a UNIX:  

- Win32_BIOS  

- Win32_ComputerSystem  

- Win32_DiskDrive  

- Win32_DiskPartition  

- Win32_NetworkAdapter  

- Win32_NetworkAdapterConfiguration  

- Win32_OperatingSystem  

- Win32_Process  

- Win32_Service  

- Win32Reg_AddRemovePrograms  

- SMS_LogicalDisk  

- SMS_Processor  

Pro počítače se systémy Linux a UNIX nejsou v Configuration Manager povoleny všechny vlastnosti pro tyto třídy inventáře.  

##  <a name="operations-for-hardware-inventory"></a><a name="BKMK_OperationsforHardwareforLnU"></a> Operace pro inventář hardwaru  
 Když ze serverů se systémem Linux a UNIX získáte inventář hardwaru, můžete tyto informace zobrazit a použít stejným způsobem jako inventář shromážděný z ostatních počítačů:  

- K zobrazení podrobných informací o inventáři hardwaru shromážděných ze serverů se systémem Linux a UNIX můžete použít Průzkumníka prostředků.  

- Můžete vytvářet dotazy na základě konkrétních hardwarových konfigurací.  

- Na základě dotazů můžete vytvářet kolekce založené na určité konfiguraci hardwaru.  

- Můžete spouštět sestavy, které zobrazí konkrétní podrobnosti o konfiguracích hardwaru.  

Inventář hardwaru se na serveru se systémem Linux nebo UNIX spouští podle plánu, který konfigurujete v nastavení klienta. Ve výchozím nastavení je tento plán každých 7 dní. Klient pro systémy Linux a UNIX podporuje cykly úplného inventáře i cykly rozdílového inventáře.  

Klienta na serveru se systémem Linux nebo UNIX můžete taky vyzvat k okamžitému spuštění inventáře hardwaru. Chcete-li spustit inventář hardwaru, spusťte v klientovi přihlašovací údaje uživatele **root** a spuštěním následujícího příkazu spusťte cyklus inventarizace hardwaru:`/opt/microsoft/configmgr/bin/ccmexec -rs hinv`  

Akce pro inventář hardwaru se zadávají do souboru protokolu klienta **scxcm.log**.  

##  <a name="how-to-use-open-management-infrastructure-to-create-custom-hardware-inventory"></a><a name="BKMK_CustomHINVforLinux"></a> Použití infrastruktury Open Management Infrastructure k vytvoření vlastního inventáře hardwaru  
 Klient pro Linux a UNIX podporuje vlastní inventář hardwaru, který můžete vytvořit pomocí infrastruktury OMI (Open Management Infrastructure). K tomu použijte následující postup:  

1.  Vytvořte vlastního poskytovatele inventáře pomocí zdroje OMI.  

2.  Nakonfigurujte počítače, aby při vytváření sestav inventáře používaly nového poskytovatele.  

3.  Povolit Configuration Manager podpoře nového poskytovatele  

###  <a name="create-a-custom-hardware-inventory-provider-for-linux-and-unix-computers"></a><a name="BKMK_LinuxProvider"></a> Vytvoření vlastního poskytovatele inventáře hardwaru pro počítače se systémem Linux a UNIX:  
 Chcete-li vytvořit vlastního poskytovatele inventáře hardwaru pro klienta Configuration Manager pro systémy Linux a UNIX, použijte **OMI source-v. 1.0.6** a postupujte podle pokynů v průvodci OMI Začínáme. Tento proces zahrnuje vytvoření souboru MOF (Managed Object Format), který definuje schéma nového poskytovatele. Později naimportujte soubor MOF do Configuration Manager, abyste mohli povolit podporu nové vlastní třídy inventáře.  

 OMI Source – v.1.0.6 i úvodní příručka k OMI jsou dostupné ke stažení na webu [The Open Group](https://github.com/microsoft/omi/blob/master/README.md) . Tyto soubory ke stažení najdete na webu OpenGroup.org na kartě **Documents** na webové stránce [Open Management Infrastructure (OMI)](https://collaboration.opengroup.org/omi/).  

###  <a name="configure-each-computer-that-runs-linux-or-unix-with-the-custom-hardware-inventory-provider"></a><a name="BKMK_AddProvidertoLinux"></a> Pro všechny počítače se systémem Linux nebo UNIX nakonfigurujte vlastního poskytovatele inventáře hardwaru:  
 Když vytvoříte vlastního poskytovatele inventáře hardwaru, musíte zkopírovat soubor knihovny poskytovatele a zaregistrovat ho ve všech počítačích s inventářem, který chcete zjistit.  

1.  Zkopírujte soubor knihovny poskytovatele do všech počítačů se systémem Linux a UNIX, ze kterých chcete shromáždit inventář. Název knihovny poskytovatele se podobá následujícímu názvu: **XYZ_MyProvider.**  

2.  Dál musíte ve všech počítačích se systémem Linux a UNIX zaregistrovat soubor knihovny poskytovatele pomocí serveru OMI. Server OMI se nainstaluje do počítače při instalaci klienta Configuration Manager pro systémy Linux a UNIX, ale musíte ručně zaregistrovat vlastní poskytovatele. K registraci poskytovatele použijte tento příkazový řádek:`/opt/microsoft/omi/bin/omireg XYZ_MyProvider.so`  

3.  Až dokončíte registraci nového poskytovatele, otestujte ho pomocí nástroje **omicli** . Nástroj **omicli** se instaluje do každého počítače se systémem Linux a UNIX při instalaci klienta Configuration Manager pro systémy Linux a UNIX. Když třeba vytvoříte poskytovatele s názvem **XYZ_MyProvider** , spusťte v počítači tento příkaz: **/opt/microsoft/omi/bin/omicli ei root/cimv2 XYZ_MyProvider**  

     Informace o **omicli** a a testování vlastních poskytovatelů najdete v úvodní příručce k OMI.  

> [!TIP]  
>  K nasazení vlastních poskytovatelů a jejich registraci v jednotlivých klientských počítačích se systémem Linux a UNIX použijte distribuci softwaru.  

###  <a name="enable-the-new-inventory-class-in-configuration-manager"></a><a name="BKMK_AddLinuxProvidertoCM"></a> V Configuration Manageru povolte novou třídu inventáře:  
 Předtím, než Configuration Manager může ohlásit inventář, který oznámil nový poskytovatel na počítačích se systémem Linux a UNIX, musíte naimportovat soubor formát MOF (Managed Object Format) (MOF), který definuje schéma vlastního poskytovatele.  

 Postup importu vlastního souboru MOF do Configuration Manager najdete v tématu [Postup konfigurace inventáře hardwaru](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
