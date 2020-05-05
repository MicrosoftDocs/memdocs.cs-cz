---
title: Příkazy před zahájením pro médium pořadí úkolů
titleSuffix: Configuration Manager
description: Vytvořte skript, který chcete použít pro předspouštěcí příkaz, distribuujte obsah přidružený k předspouštěcímu příkazu a nakonfigurujte předspouštěcí příkaz v médiu.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ccc9f652-2953-4c38-8a90-c799484105ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9dd921d58e6ef777017af3e2eb24dbf4bd611fab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717458"
---
# <a name="prestart-commands-for-task-sequence-media-in-configuration-manager"></a>Příkazy před zahájením pro médium pořadí úloh v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Můžete vytvořit předspouštěcí příkaz v Configuration Manager pro použití se spouštěcím médiem, samostatným médiem a předzpracovaným médiem. Předspouštěcí příkaz je skript nebo spustitelný soubor, který je spuštěn před výběrem sekvence úloh a může komunikovat s uživatelem v systému Windows PE. Předspouštěcí příkaz může vyzvat uživatele k zadání informací a jejich uložení do prostředí sekvence úloh nebo vyzvat proměnnou sekvence úloh k zadání informací. Když se spouští cílový počítač, příkazový řádek je spuštěn před stažením zásad z bodu správy. Následující postupy použijte k vytvoření skriptu, který chcete použít pro předspouštěcí příkaz, distribuujte obsah přidružený k předspouštěcímu příkazu a nakonfigurujte předspouštěcí příkaz v médiu.  

## <a name="create-a-script-file-to-use-for-the-prestart-command"></a>Vytvoření souboru skriptu k použití pro příkaz před zahájením  
 Proměnné pořadí úloh se můžou při provádění pořadí úloh načíst a zapsat pomocí objektu COM Microsoft.SMS.TSEnvironment. Následující příklad ilustruje soubor skriptu v jazyce Visual Basic, který se dotazuje proměnné sekvence úloh _SMSTSLogPath k získání aktuálního umístění protokolu. Skript zároveň nastaví vlastní proměnnou.  

``` VBScript
dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")  
dim logPath  
' You can query the environment to get an existing variable.  
logPath = env("_SMSTSLogPath")  
' You can also set a variable in the OSD environment.  
env("MyCustomVariable") = "varname"  
```  

## <a name="create-a-package-for-the-script-file-and-distribute-the-content"></a>Vytvoření balíčku pro soubor skriptu a distribuování obsahu  
 Když vytvoříte skript nebo spustitelný soubor pro předspouštěcí příkaz, musíte vytvořit zdroj balíčku, který bude hostitelem souborů pro tento skript nebo spustitelný soubor, vytvořit balíček pro soubory (není potřeba žádný program) a pak distribuovat obsah do distribučního bodu.  

 Další informace o vytváření balíčku najdete v tématu [balíčky a programy](../../apps/deploy-use/packages-and-programs.md).  

 Další informace o distribuci obsahu najdete v tématu [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

## <a name="configure-the-prestart-command-in-media"></a>Nakonfigurování předspouštěcího příkazu v médiu  
 Předspouštěcí příkaz můžete nakonfigurovat v nástroji Průvodce vytvořením média sekvence úloh pro samostatné médium, spouštěcí médium nebo předzpracované médium. Další informace o typech médií najdete v tématu [Vytvoření média pořadí úkolů](../deploy-use/create-task-sequence-media.md). K vytvoření předspouštěcího příkazu v médiu použijte následující postup.  

#### <a name="to-create-a-prestart-command-in-media"></a>Vytvoření předspouštěcího příkazu v médiu  

1.  V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  

2.  V pracovním prostoru **softwarová knihovna** rozbalte možnost **operační systémy**a klikněte na položku **pořadí úloh**.  

3.  Na kartě **Domů** ve skupině **Vytvoření** kliknutím na možnost **Vytvoření médií sekvence úlohy** spusťte průvodce vytvořením médií sekvence úlohy.  

4.  Na stránce **Vybrat typ média** vyberte možnost **Samostatné médium**, **Spouštěcí médium**nebo **Předzpracované médium**a pak klikněte na tlačítko **Další**.  

5.  V průvodci přejděte na stránku **Vlastní nastavení** . Další informace o konfigurování dalších stránek v průvodci najdete v tématu [Vytvoření média pořadí úkolů](../deploy-use/create-task-sequence-media.md).  

6.  Na stránce **Vlastní nastavení** určete následující data a pak klikněte na tlačítko **Další**.  

    -   Vyberte možnost **Povolit předspouštěcí příkaz**.  

    -   Do textového pole **Příkazový řádek** zadejte skript nebo spustitelný soubor, který jste vytvořili pro předspouštěcí příkaz.  

        > [!IMPORTANT]  
        >  Pomocí příkazu **cmd/c <\> příkazu před zahájením** zadejte příkaz před zahájením. Pokud byste například použili TSScript.vbs jako název vašeho skriptu příkazu před zahájením, zadali byste na příkazový řádek text **cmd /C TSScript.vbs** . Kde možnost **cmd /C** otevírá nové interpretační okno příkazu systému Windows a používá proměnnou prostředí pro cestu k vyhledání skriptu příkazu před zahájením nebo spustitelného souboru. Také můžete zadat úplnou cestu k předspouštěcímu příkazu, ale písmeno diskové jednotky může být jiné na počítačích s jinými konfiguracemi diskových jednotek.  

    -   Vyberte možnost **Zahrnout soubory pro předspouštěcí příkaz**.  

    -   Klikněte na možnost **Nastavit** k vybrání balíčku, který je přidružený k souborům předspouštěcích příkazů.  

    -   Klikněte na tlačítko **Procházet** k výběru distribučního bodu, který je hostitelem obsahu předspouštěcího příkazu.  

7.  Dokončete průvodce.  
