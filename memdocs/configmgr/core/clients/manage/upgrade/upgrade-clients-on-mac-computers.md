---
title: Upgrade klientů macOS
titleSuffix: Configuration Manager
description: Upgradujte klienta Configuration Manager v počítačích Mac.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f34d0c9233b4f7384dfc2280dc92334450a785ed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715001"
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-configuration-manager"></a>Postup upgradu klientů na počítačích Mac v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Postupujte podle kroků vysoké úrovně v tomto článku a upgradujte klienta nástroje pro počítače Mac pomocí aplikace Configuration Manager. Můžete si také stáhnout instalační soubor klienta pro systém Mac, zkopírovat ho do sdíleného síťového umístění nebo do místní složky v počítači Mac a pak dát pokyn uživatelům, aby instalaci spustili ručně.  

> [!NOTE]  
> Před provedením těchto kroků se ujistěte, že váš počítač Mac splňuje požadavky. Viz [podporované operační systémy pro počítače Mac](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).  

## <a name="download-the-latest-mac-client"></a>Stáhnout nejnovější verzi klienta pro Mac

Klient pro Mac pro Configuration Manager není dodaný na instalačním médiu Configuration Manager. Stáhněte si ho z webu Microsoft Download Center, [klienta Microsoft Endpoint Configuration Manager-MacOS (64-bit)](https://www.microsoft.com/download/details.aspx?id=100850). Instalační soubory klienta pro systém Mac jsou obsaženy v souboru Instalační služba systému Windows s názvem **ConfigmgrMacClient. msi**.  

## <a name="create-the-mac-client-installation-file"></a>Vytvoření instalačního souboru klienta pro systém Mac

Na počítači, na kterém běží Windows, spusťte **ConfigmgrMacClient. msi**. Tento instalační program rozbalí instalační soubor klienta pro systém Mac s názvem **Macclient. dmg**. Ve výchozím nastavení můžete tento soubor najít v následující složce: **C:\Program Files\Microsoft\System Center Configuration Manager pro klienta Mac**.  

## <a name="extract-the-client-installation-files"></a>Extrakce instalačních souborů klienta

Zkopírujte **Macclient. dmg** do počítače Mac. Připojte soubor Macclient. dmg v macOS a pak zkopírujte obsah do složky v počítači Mac.  

## <a name="create-a-cmmac-file"></a>Vytvoření souboru. cmmac

1. Otevřete složku **nástroje** instalačních souborů klienta pro systém Mac. Pomocí nástroje **CMAppUtil** vytvořte soubor. cmmac z instalačního balíčku klienta. Tento soubor použijete k vytvoření aplikace Configuration Manager.  

2. Zkopírujte nový soubor **CMClient. pkg. cmmac** do umístění v síti, které je k dispozici pro počítač se spuštěnou konzolou Configuration Manager.  

    Další informace najdete v tématu [doplňkové postupy pro vytváření a nasazování aplikací pro počítače](../../../../apps/get-started/creating-mac-computer-applications.md#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers)se systémem Mac.  

## <a name="create-and-deploy-the-app"></a>Vytvoření a nasazení aplikace

1. V konzole Configuration Manager [vytvořte aplikaci](../../../../apps/get-started/creating-mac-computer-applications.md) ze souboru **CMClient. pkg. cmmac** .  

2. [Nasaďte tuto aplikaci](../../../../apps/deploy-use/deploy-applications.md) do počítačů Mac ve vaší hierarchii.  

## <a name="install-the-updated-client"></a>Instalace aktualizovaného klienta

Existující klient Configuration Manager v počítačích se systémem Mac vyzve uživatele k instalaci aktualizace k instalaci. Jakmile uživatelé klienta nainstalují, musí restartovat své počítače Mac.  

Po restartování počítače se automaticky spustí průvodce **zápisem počítače** , který si vyžádá nový certifikát uživatele.

Pokud Configuration Manager registraci nepoužíváte, ale nainstalujete certifikát klienta nezávisle na Configuration Manager, přečtěte si téma [Konfigurace klientů pro použití existujícího certifikátu](#BKMK_UpgradingClient_MachineEnrollment).  

## <a name="configure-clients-to-use-an-existing-certificate"></a><a name="BKMK_UpgradingClient_MachineEnrollment"></a>Konfigurace klientů pro použití existujícího certifikátu

Tento postup slouží k tomu, aby nedošlo ke spuštění Průvodce registrací počítače, a ke konfiguraci upgradovaného klienta na používání existujícího klientského certifikátu.  

1. V konzole Configuration Manager [vytvořte položku konfigurace](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md) typu **Mac OS X**.  

1. Zadejte pro tuto položku konfigurace nastavení typu **Skript**.  

1. Přidejte do nastavení následující skript:  

  ``` Shell
  #!/bin/sh  
  echo "Starting script\n"  
  echo "Changing directory to MAC Client\n"  
  cd /Users/Administrator/Desktop/'MAC Client'/  
  echo "Import root cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
  echo "Using openssl to convert pfx to a crt\n"  
  /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
  echo "Adding trust to root cert\n"  
  /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
  echo "Import client cert\n"  
  /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
  echo "Executing ccmclient with MP\n"  
  sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
  echo "Editing Plist file\n"  
  sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
  echo "Changing directory to CCM\n"  
  cd /Library/'Application Support'/Microsoft/CCM/  
  echo "Making connection to the server\n"  
  sudo open ./CCMClient  
  echo "Ending Script\n"  
  exit  
  ```  

1. Přidejte položku konfigurace do [standardních hodnot konfigurace](../../../../compliance/deploy-use/create-configuration-baselines.md). Pak [Nasaďte standardní hodnoty konfigurace](../../../../compliance/deploy-use/deploy-configuration-baselines.md) do všech počítačů Mac, které instalují certifikát nezávisle na Configuration Manager.  
