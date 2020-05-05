---
title: Instalovat aktualizace softwaru
titleSuffix: Configuration Manager
description: 'Doporučení pro použití kroku pořadí úkolů: instalovat aktualizace softwaru v Configuration Manager.'
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 72d1ccd5-3763-4f88-9273-e1a73e8f4286
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6528e979222bc6ecea2a57a003ff5266b5c096c5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719992"
---
# <a name="install-software-updates"></a>Instalovat aktualizace softwaru

*Platí pro: Configuration Manager (Current Branch)*

Krok **instalovat aktualizace softwaru** se běžně používá v Configuration Manager pořadí úkolů. Při instalaci nebo aktualizaci operačního systému aktivuje komponenty aktualizace softwaru, aby kontrolovaly a nasadily aktualizace. Tento krok může u některých zákazníků způsobit problémy, třeba dlouhé prodlevy při vypršení časového limitu nebo nezmeškaných aktualizacích. Informace v tomto článku vám pomůžou zmírnit problémy, které se týkají tohoto kroku, a pro lepší řešení potíží, když dojde k chybě.

Další informace o tomto kroku najdete v tématu [instalace aktualizací softwaru](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) .



## <a name="recommendations"></a>Doporučení

Chcete-li tomuto procesu zajistit úspěch, použijte následující doporučení:

- [Použití offline údržby](#use-offline-servicing)
- [Jeden index](#single-index)
- [Zmenšit velikost obrázku](#bkmk_resetbase)

### <a name="use-offline-servicing"></a>Použití offline údržby

Pomocí Configuration Manager pravidelně instalovat příslušné aktualizace softwaru do souborů imagí. V tomto postupu pak dojde k omezení počtu aktualizací, které je potřeba nainstalovat během pořadí úkolů.

Další informace najdete v tématu [použití aktualizací softwaru pro obrázek](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates).

### <a name="single-index"></a>Jeden index

Mnoho souborů imagí obsahuje několik indexů, například pro různé edice systému Windows. Zmenšete soubor obrázku na jeden index, který požadujete. Tento postup zkracuje dobu, po kterou se mají v imagi použít aktualizace softwaru. Také umožňuje další doporučení zmenšit velikost obrázku.

Počínaje verzí 1902 tento proces Automatizujte při přidání image operačního systému do lokality. Další informace najdete v tématu [Přidání image operačního systému](../get-started/manage-operating-system-images.md#BKMK_AddOSImages).<!--3719699-->

### <a name="reduce-image-size"></a><a name="bkmk_resetbase"></a>Zmenšit velikost obrázku

Při použití aktualizací softwaru na bitovou kopii optimalizuje výstup odebráním jakýchkoli nahrazených aktualizací. Použijte nástroj příkazového řádku DISM, například:

``` Command
dism /Mount-Image /ImageFile:C:\Data\install.wim /MountDir:C:\Mountdir
dism /Image:C:\Mountdir /Cleanup-Image /StartComponentCleanup /ResetBase
dism /Unmount-Image /MountDir:C:\Mountdir /Commit  
```

Počínaje verzí 1902 je k dispozici nová možnost automatizace tohoto procesu. Další informace najdete v tématu [optimalizovaná údržba imagí](../get-started/manage-operating-system-images.md#bkmk_resetbase).<!--3555951-->


## <a name="image-engineering-decisions"></a>Rozhodnutí o inženýrech obrázků

Při návrhu procesu vytváření bitových kopií je k dispozici několik možností, které mohou mít vliv na instalaci aktualizací softwaru:

- [Pravidelně znovu zachytit image](#bkmk_goldimage)  
- [Použití offline údržby](#bkmk_offline)  
- [Použít pouze výchozí obrázek](#bkmk_installwim)

### <a name="periodically-recapture-the-image"></a><a name="bkmk_goldimage"></a>Pravidelně znovu zachytit image

Máte automatizovaný proces automatického zachycení vlastní image operačního systému v pravidelných intervalech. Toto pořadí úloh zachycení nainstaluje nejnovější aktualizace softwaru. Tyto aktualizace můžou zahrnovat kumulativní, nekumulativní a další důležité aktualizace, jako je například aktualizace služby Servicing (cestou nadřazené). Pořadí úkolů nasazení nainstaluje další aktualizace od zachytávání.

Další informace o tomto procesu najdete v tématu [Vytvoření pořadí úkolů pro zachycení operačního systému](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).

#### <a name="advantages"></a>Výhody

- Méně aktualizací, které se mají použít v době nasazení na klienta, které šetří čas a šířku pásma během nasazování
- Méně aktualizací, které se zabývat tím, že způsobují restart
- Přizpůsobená image pro organizaci
- Méně proměnných v době nasazení

#### <a name="disadvantages"></a>Nevýhody

- Čas k vytvoření a zachycení obrázku, i když je převážně automatizovaná
- Čas pro distribuci image do distribučních bodů, který se může zobrazit jako výpadek pro aktivní nasazení
- Doba testování prostřednictvím předprodukčních prostředí může být delší než cyklus oprav operačního systému, který může mít nepodstatný aktualizovaný obraz.


### <a name="use-offline-servicing"></a><a name="bkmk_offline"></a>Použití offline údržby

Naplánujte Configuration Manager pro použití aktualizací softwaru pro image.

Další informace najdete v tématu [použití aktualizací softwaru pro obrázek](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates).

#### <a name="advantages"></a>Výhody

- Méně aktualizací, které se mají použít v době nasazení na klienta, které šetří čas a šířku pásma během nasazování
- Méně aktualizací, které se zabývat tím, že způsobují restart
- V lokalitě můžete naplánovat proces údržby.

#### <a name="disadvantages"></a>Nevýhody

- Ruční výběr aktualizací
- Čas pro distribuci image do distribučních bodů se zvýšil.
- Podporuje pouze aktualizace založené na modelu CBS. Nejde použít aktualizace Office.

> [!Tip]  
> Výběr aktualizací softwaru můžete automatizovat pomocí prostředí PowerShell. Seznam aktualizací získáte pomocí rutiny [Get-CMSoftwareUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmsoftwareupdate?view=sccm-ps) . Pak pomocí rutiny [New-CMOperatingSystemImageUpdateSchedule](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmoperatingsystemimageupdateschedule?view=sccm-ps) vytvořte plán údržby offline. Následující příklad ukazuje jednu metodu pro automatizaci této akce:
>
> ```PowerShell
> # Get the OS image
> $Win10Image = Get-CMOperatingSystemImage -Name "Windows 10 Enterprise"
>
> # Get the latest cumulative update for Windows 10 1809
> $OSBuild = "1809"
> $LatestUpdate = Get-CMSoftwareUpdate -Fast | Where {$_.LocalizedDisplayName -Like "*Cumulative Update for Windows 10 Version $OSBuild for x64*" -and $_.LocalizedDisplayName -notlike "*Dynamic*"} | Sort-Object ArticleID -Descending | Select -First 1
> Write-Host "Latest update for Windows 10 build" $OSBuild "is" $LatestUpdate.LocalizedDisplayName
>
> # Create a new update schedule to apply the latest update
> New-CMOperatingSystemImageUpdateSchedule -Name $Win10Image.Name -SoftwareUpdate $LatestUpdate -RunNow -ContinueOnError $True
> ```


### <a name="use-default-image-only"></a><a name="bkmk_installwim"></a>Použít pouze výchozí obrázek

V pořadí úloh nasazení použijte výchozí soubor bitové kopie Windows Install. wim.

#### <a name="advantages"></a>Výhody

- Známý dobrý zdroj, který snižuje riziko poškození obrázku jako možného problému
- Eliminuje změny obrázku jako možný problém.

#### <a name="disadvantages"></a>Nevýhody

- Potenciál pro velký objem aktualizací během nasazení
- Zvýšení doby nasazení pro každé zařízení
- Nemusí mít potřebná přizpůsobení, vyžaduje přizpůsobení dalších kroků pořadí úkolů.



## <a name="flowchart"></a>Vývojový diagram

Tento diagram vývojového diagramu znázorňuje proces, když zahrnete krok instalovat aktualizace softwaru v pořadí úkolů.

[Zobrazit diagram v plné velikosti](media/ts-step-install-software-updates.svg)

![Diagram vývojového diagramu pro krok pořadí úkolů instalovat aktualizace softwaru](media/ts-step-install-software-updates.svg)  

1. **Proces začíná na klientovi**: pořadí úkolů spuštěné v klientovi zahrnuje krok instalovat aktualizace softwaru.
2. **Kompilovat a vyhodnocovat zásady**: klient zkompiluje všechny zásady aktualizace softwaru do oboru názvů WMI RequestedConfigs. (CIAgent. log)
3. *Je tato instance poprvé volána?*  
    1. **Ano**: Přejít na **úplnou kontrolu**  
    2. **Ne**: *jedná se o krok nakonfigurovaný s možností [vyhodnotit aktualizace softwaru z výsledků kontroly v mezipaměti](task-sequence-steps.md#evaluate-software-updates-from-cached-scan-results)?*
        1. **Ano**: Přejít na **kontrolu z mezipaměti výsledků**
        2. **Ne**: Přejít na **úplnou kontrolu**
4. Proces kontroly: úplná kontrola nebo skenování z výsledků v mezipaměti s paralelním procesem monitorování.
    1. **Úplná kontrola**: modul pořadí úloh volá agenta aktualizace softwaru prostřednictvím rozhraní API pro kontrolu aktualizací a provede *úplnou* kontrolu. (WUAHandler. log, ScanAgent. log)  
        1. **Kontrola součtu agenta-úplné**: normální proces skenování prostřednictvím agenta web Windows Update (WUA), který komunikuje s bodem aktualizace softwaru, na kterém běží služba WSUS. Do místního úložiště aktualizací přidá všechny příslušné aktualizace. (WindowsUpdate. log, UpdateStore. log)
    2. **Skenovat z výsledků uložených v mezipaměti**: modul pořadí úkolů volá agenta aktualizace softwaru prostřednictvím rozhraní API pro kontrolu aktualizací, aby kontroloval metadata uložená v mezipaměti. (WUAHandler. log, ScanAgent. log)
        1. **Sum-prověřování agentů – v mezipaměti**: Agent web Windows Update (WUA) kontroluje aktualizace již uložené v mezipaměti místního úložiště aktualizací. (WindowsUpdate. log, UpdateStore. log)
    3. **Spustit časovač prohledávání**: modul pořadí úkolů spustí časovač a počká. (K tomuto procesu dochází paralelně s úplnou kontrolou nebo kontrolou z procesu výsledků uložených v mezipaměti.)
        1. **Monitorování**: modul pořadí úloh monitoruje agenta součtu na stav.
        2. *Co je odpověď od agenta SUM?*
            - **Probíhá**: má časovač dosaženou hodnotu v proměnné pořadí úkolů [SMSTSSoftwareUpdateScanTimeout](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)? (Výchozí 1 hodina)
                - **Ano**: krok se nezdařil.
                - **Ne**: Přejít na **monitorování**
            - Nezdařilo se: krok se **nepovedlo**provést.
            - **Dokončeno**: Přejít na **seznam výpisů aktualizací**
5. **Seznam aktualizací výčtu**: Agent Sum vypíše seznam aktualizací vrácených prohledáním, určení, které jsou k dispozici nebo povinně.
6. *Existují v seznamu výsledků kontroly nějaké aktualizace?*
    - **Ano**: přejít k **instalaci aktualizací**
    - **Ne**: nic se nedá nainstalovat, krok se úspěšně dokončí.
7. Proces nasazení: proces instalace aktualizací proběhne paralelně s procesem monitorování nasazení.
    1. **Nainstalovat aktualizace**: modul pořadí úloh volá agenta Sum prostřednictvím rozhraní API pro nasazení aktualizací, aby nainstaloval všechny dostupné nebo jenom povinné aktualizace. Toto chování je založené na konfiguraci kroku, bez ohledu na to, zda jste vybrali možnost **požadováno k instalaci – povinné aktualizace softwaru** nebo **jsou k dispozici pro instalaci – všechny aktualizace softwaru**. Toto chování můžete také určit pomocí proměnné [SMSInstallUpdateTarget](task-sequence-variables.md#SMSInstallUpdateTarget) .
        1. **Instalace agenta Sum**: běžný proces instalace využívající existující seznam aktualizací, který se stahuje standardním obsahem. Nainstalujte aktualizaci prostřednictvím agenta web Windows Update (WUA). (UpdatesDeployment. log; UpdatesHandler. log; WuaHandler. log, WindowsUpdate. log)
    2. **Spustit časovač nasazení a zobrazit průběh**: modul pořadí úkolů spouští časovač instalace, zobrazuje dílčí postup v uživatelském rozhraní průběhu procesu TS v 10% intervalech a čeká.
        1. **Monitorování**: modul pořadí úkolů se dotáže agenta součtu na stav.
        2. *Co je odpověď od agenta SUM?*
            - **Probíhá**: *proces instalace byl pro 8 hodin neaktivní?*
                - **Ano**: krok se nezdařil.
                - **Ne**: Přejít na **monitorování**
            - Nezdařilo se: krok se **nepovedlo**provést.
            - **Dokončeno**: Přejít na *je krok nakonfigurovaný s možností **vyhodnotit aktualizace softwaru z výsledků kontroly v mezipaměti**?*


### <a name="timeouts"></a>Časové limity

Diagram obsahuje dvě proměnné časového limitu, které se vztahují k tomuto kroku. Existují další standardní časovače z jiných komponent, které mohou mít vliv na tento proces.

- Časový limit kontroly aktualizace: 1 hodina (souboru Smsts. log)  
- Časový limit požadavku na umístění: 1 hodina (LocationServices. log, CAS. log)  
- Časový limit stahování obsahu: 1 hodina (DTS. log)  
- Časový limit neaktivního distribučního bodu: 1 hodina (LocationServices. log, CAS. log)  
- Celkový časový limit instalace celkem: 8 hodin (souboru Smsts. log)  



## <a name="troubleshooting"></a>Řešení potíží

Následující zdroje informací a další informace vám pomůžou při řešení problémů s tímto krokem:

- Ujistěte se, že vaše nasazení aktualizací softwaru cílí na stejnou kolekci jako nasazení pořadí úkolů.  

- Nezapomeňte zahrnout body aktualizace softwaru do skupin hranic. Další informace najdete v tomto [článku Podpora Microsoftu](https://support.microsoft.com/help/4041012/1702-clients-do-not-get-software-updates-from-configuration-manager).  

- Pomoc při odstraňování potíží s procesem správy aktualizací softwaru najdete v tématu [řešení potíží se softwarem Update Management](https://support.microsoft.com/help/10680/software-update-management-troubleshooting-in-configuration-manager).  

- Chcete-li zvýšit celkový výkon, zmenšete velikost katalogu aktualizací softwaru. Příklad:  

    - Odeberte zbytečné klasifikace, produkty a jazyky. Další informace najdete v tématu [Konfigurace klasifikací a produktů k synchronizaci](../../sum/get-started/configure-classifications-and-products.md).  

    - Reindexujte databázi lokality a znovu sestavte statistiku. Další informace najdete na stránce [dokumentace k výkonu Configuration Manager a škálování](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e)na stránce.  

    - Odmítněte nepotřebné aktualizace, například:
        - Nahrazeno (počínaje verzí 1810, Configuration Manager tuto akci za vás. Další informace najdete v tématu [chování vyčištění služby WSUS počínaje verzí 1810](../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-behavior-starting-in-version-1810).)
        - Itanium
        - Beta
        - Další verze
        - ARM
        - Verze Windows, které nasazujete
