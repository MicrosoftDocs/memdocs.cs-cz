---
title: Použití časových období údržby
titleSuffix: Configuration Manager
description: Pomocí oken kolekce a údržby můžete efektivně spravovat klienty v Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6c2128c9e26137c268577e68e5ee12e3a71f8513
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714441"
---
# <a name="how-to-use-maintenance-windows-in-configuration-manager"></a>Použití časových období údržby v systému Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Časové intervaly pro správu a údržbu umožňují definovat čas, kdy se Configuration Manager operace můžou provádět v kolekci zařízení. Časové intervaly pro správu a údržbu vám pomůžou zajistit, aby změny konfigurace klientů probíhaly v obdobích, která neovlivňují produktivitu. Od verze Configuration Manager 1806 uvidí vaši uživatelé, když se jeho další časové období údržby nachází na kartě **stav instalace** v **centru softwaru**. <!--1358131-->

 Následující operace podporují časová období údržby:  

- Nasazení softwaru  

- Nasazení aktualizací softwaru  

- Nasazení a vyhodnocení nastavení dodržování předpisů  

- Nasazení operačního systému  

- Nasazení pořadí úloh  

  Nakonfigurujte časové intervaly pro správu a údržbu pomocí počátečního data, času zahájení a dokončení a způsobu opakování. Maximální doba trvání okna musí být kratší než 24 hodin. Ve výchozím nastavení se restart počítače způsobený nasazením nepovoluje mimo časové období údržby, ale můžete přepsat výchozí. Časová období údržby mají vliv jenom na čas, kdy se program nasazení spustí; aplikace nakonfigurované ke stažení a spuštění místně můžou stahovat obsah mimo okno.  

  Když je klientský počítač členem kolekce zařízení, která má okno údržby, spustí se program nasazení pouze v případě, že maximální povolená doba běhu nepřekročí dobu nakonfigurovanou pro okno. Pokud se spuštění programu nepovede, vygeneruje se výstraha a nasazení se znova spustí v dalším plánovaném časovém období údržby, ve kterém bude dost času.  

## <a name="using-multiple-maintenance-windows"></a>Použití více časových období údržby  
 Když je klientský počítač členem více kolekcí zařízení s časovými intervaly pro správu a údržbu, platí tato pravidla:  

- Pokud se časové intervaly pro správu a údržbu nepřekrývají, jsou považovány za dva nezávislé časové intervaly pro správu.  

- Pokud se časové intervaly pro správu a údržbu překrývají, jsou považovány za jedno okno údržby, včetně časového období zahrnutého v oknech údržby. Pokud například dvě okna, každá hodina v době trvání překrývá o 30 minut, bude efektivní doba trvání časového období údržby 90 minut.  

  Když uživatel zahájí instalaci aplikace z centra softwaru, aplikace se nainstaluje hned, bez ohledu na časové intervaly pro správu a údržbu.  

  Pokud nasazení aplikace s účelem **Požadované** dosáhne konečného termínu mimo pracovní dobu nastavenou uživatelem v Centru softwaru, aplikace se nainstaluje. 

### <a name="how-to-configure-maintenance-windows"></a>Konfigurace časových období údržby  

1.  V konzole Configuration Manager klikněte na **prostředky a kompatibilita**>  **kolekce zařízení**.  

3.  V seznamu **kolekce zařízení** vyberte kolekci. Pro kolekci **všechny systémy** nelze vytvořit časová období údržby.  

4.  Na kartě **Domů** ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  

5.  Na kartě časové intervaly pro **správu a údržbu** dialogového okna ** &lt;vlastnost\> název kolekce** klikněte na ikonu **Nový** .  

6.  Dokončete ** &lt;dialog\> nový plán** .  

7.  Vytvořte výběr z rozevíracího seznamu **použít tento plán** .  

8.  Zvolte **OK** a pak zavřete dialogové okno ** &lt;vlastnosti\> názvu kolekce** .  
 
## <a name="using-powershell"></a><a name="bkmk_powershell"></a>Použití PowerShellu

PowerShell se dá použít ke konfiguraci časových období údržby.  Další informace naleznete v tématu:

* [Set-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmmaintenancewindow)
* [Get-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmmaintenancewindow)
* [New-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmmaintenancewindow)
* [Remove-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmmaintenancewindow)
