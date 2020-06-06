---
title: Konfigurace obsahu předběžné mezipaměti
titleSuffix: Configuration Manager
description: Přečtěte si, jak můžou klienti stahovat obsah nasazení operačního systému, než uživatel nainstaluje pořadí úkolů.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9d1e8252-99e3-48aa-bfa5-0cf4cd6637b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ec465f3dee33ca311aec120e74a2994a81a90ec9
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455221"
---
# <a name="configure-pre-cache-content-for-task-sequences"></a>Konfigurace obsahu před ukládáním do mezipaměti pro pořadí úloh

*Platí pro: Configuration Manager (Current Branch)*

<!--1021244-->
Funkce pre-cache pro dostupná nasazení pořadí úkolů umožňuje klientům stáhnout relevantní obsah předtím, než uživatel nainstaluje pořadí úkolů. Klient může předukládat obsah do mezipaměti pro pořadí úloh, která provádějí [upgrade operačního systému](create-a-task-sequence-to-upgrade-an-operating-system.md) nebo [instalaci image operačního systému](create-a-task-sequence-to-install-an-operating-system.md).

> [!Note]  
> Ve výchozím nastavení ve verzi 1910 Configuration Manager tuto funkci povolí. Verze 1906 nebo starší Configuration Manager ve výchozím nastavení tuto volitelnou funkci nepovoluje. Tuto funkci musíte před použitím povolit. Další informace naleznete v části [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

Například stačí pouze jedno místní upgradované pořadí úkolů pro všechny uživatele a mít mnoho architektur a jazyků. V předchozích verzích se obsah začne stahovat, když uživatel nainstaluje dostupné nasazení pořadí úkolů z centra softwaru. Tato prodleva přidá další čas před tím, než bude instalace připravena k zahájení. Veškerý obsah, na který se odkazuje v pořadí úkolů, se stáhne. Tento obsah zahrnuje balíček s upgradem operačního systému pro všechny jazyky a architektury. Pokud má každý balíček s upgradem velikost přibližně 3 GB, je celkový obsah velmi velký.

Obsah předběžného ukládání do mezipaměti umožňuje klientovi stahovat jenom příslušný obsah a veškerý další odkazovaný obsah hned po přijetí nasazení. Když uživatel klikne na **instalovat** v centru softwaru, obsah je připravený. Instalace se spustí rychle, protože obsah je na místním pevném disku.

V Configuration Manager verze 1902 a starší se toto chování vztahuje pouze na *balíček s upgradem operačního systému*. Tento balíček je jediným obsahem, na kterém zadáte odpovídající architekturu nebo jazyk. Pokud například pořadí úkolů odkazuje také na více balíčků ovladačů, klient je stáhne. Modul pořadí úloh vyhodnocuje podmínky kroků při spuštění pořadí úloh, nikoli předem. Klient nástroje používá značky ve vlastnostech balíčku k určení obsahu, který se má předem ukládat do mezipaměti.

Počínaje verzí 1906,<!--4224642--> pro snížení spotřeby šířky pásma následujících typů obsahu můžete použít předukládání do mezipaměti.

- Balíčky s upgradem operačního systému
- Image operačního systému
- Balíčky ovladačů
- Balíčky

## <a name="configure-pre-caching"></a>Konfigurace před ukládáním do mezipaměti

Existují tři kroky ke konfiguraci funkce pre-cache:

1. [Vytvoření a konfigurace balíčků](#bkmk_createpkg)
2. [Vytvoření pořadí úkolů s podmíněnými kroky](#bkmk_createts)
3. [Nasadit pořadí úloh a povolit předběžné ukládání do mezipaměti](#bkmk_deploy)


### <a name="1-create-and-configure-the-packages"></a><a name="bkmk_createpkg"></a>1. vytvoření a konfigurace balíčků

Klient vyhodnotí atributy balíčků a určí, který obsah se stáhne během předběžného ukládání do mezipaměti.  

#### <a name="os-upgrade-package"></a>Balíček s upgradem operačního systému

Vytvořte [balíčky pro upgrade operačního systému](../get-started/manage-operating-system-upgrade-packages.md) pro konkrétní architektury a jazyky. Určete **architekturu** a **jazyk** na kartě **zdroj dat** jejích vlastností.

#### <a name="os-image"></a>Bitová kopie operačního systému

Vytváření [imagí operačních systémů](../get-started/manage-operating-system-images.md) pro konkrétní architektury a jazyky. Určete **architekturu** a **jazyk** na kartě **zdroj dat** jejích vlastností.

#### <a name="driver-package"></a>Balíček ovladačů

Vytvořte [balíčky ovladačů](../get-started/manage-drivers.md#BKMK_ManagingDriverPackages) pro konkrétní hardwarové modely. Na kartě **Obecné** v jeho vlastnostech zadejte **model** .

Aby bylo možné určit, který balíček ovladače se stáhne během předběžného ukládání do mezipaměti, klient vyhodnotí model proti vlastnosti **Name** třídy **Win32_ComputerSystemProduct** WMI.

> [!TIP]
> Samotný dotaz používá `LIKE` příkaz se zástupnými znaky: `select * from win32_computersystemproduct where name like "%yourstring%"` . Například pokud zadáte `Surface` jako model, dotaz odpovídá všem modelům, které obsahují tento řetězec.<!-- 6315551 -->

#### <a name="package"></a>Balíček

Vytvořte [balíčky](../../apps/deploy-use/packages-and-programs.md) pro konkrétní architektury a jazyky. Určete **architekturu** a **jazyk** na kartě **Obecné** vlastností.


### <a name="2-create-a-task-sequence"></a><a name="bkmk_createts"></a>2. Vytvoření pořadí úloh

Vytvořte pořadí úkolů s podmíněnými kroky pro různé jazyky a architektury nebo různé hardwarové modely pro balíčky ovladačů.

|Obsah|Krok|
|---------|---------|
|Balíček s upgradem operačního systému|[Upgrade operačního systému](../understand/task-sequence-steps.md#BKMK_UpgradeOS)|
|Bitová kopie operačního systému|[Použít bitovou kopii operačního systému](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)|
|Balíček ovladačů|[Použít balíček ovladače](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage)|
|Balíček|[Instalovat balíček](../understand/task-sequence-steps.md#BKMK_InstallPackage)|

Například následující krok **upgradu operačního systému** používá anglickou verzi:  

![Editor pořadí úloh znázorňující více kroků upgradu operačního systému pro CSY, DEU a JPN](../media/precacheproperties2.png)

![Editor pořadí úloh, karta možnosti a zobrazení dotazu rozhraní WMI v jazyce WQL pro národní prostředí a OSArchitecture](../media/precacheoptions2.png)  

> [!Tip]
> Následující dotaz rozhraní WMI doporučujeme pro anglickou verzi operačního systému (USA) a architekturu 64:
>
> ```WMI
> SELECT * FROM Win32_OperatingSystem WHERE OSArchitecture LIKE '%64%' AND OSLanguage='1033'
> ```
>
> Nejdřív přidejte jazyk tak, že vyberete podmínku **jazyka operačního systému** . Pak upravte dotaz rozhraní WMI tak, aby zahrnoval klauzuli Architecture.

### <a name="3-deploy-the-task-sequence"></a><a name="bkmk_deploy"></a>3. nasazení pořadí úkolů

[Nasaďte pořadí úkolů](deploy-a-task-sequence.md). Pro funkci před ukládáním do mezipaměti nakonfigurujte následující nastavení:  

- Na kartě **Obecné** vyberte **předem stáhnout obsah pro toto pořadí úloh**.  

- Na kartě **nastavení nasazení** nakonfigurujte pořadí úkolů jako **dostupné**.  

- Na kartě **plánování** vyberte aktuálně vybraný čas pro nastavení a **naplánujte, kdy bude toto nasazení k dispozici**. Klient spustí předběžné ukládání obsahu do mezipaměti v době dostupnosti nasazení. Když cílový klient obdrží tuto zásadu, je dostupný čas v minulosti, takže se stahování před ukládáním do mezipaměti začne hned. Pokud klient obdrží tuto zásadu, ale dostupný čas je v budoucnu, klient nezačne ukládat obsah do mezipaměti, dokud nedojde k dostupnému času.  

- Na kartě **distribuční body** nakonfigurujte nastavení **možností nasazení** . Pokud obsah není předem uložen do mezipaměti, než uživatel spustí instalaci, klient použije tato nastavení.  

    > [!Important]  
    > V případě pořadí úkolů, které nainstaluje bitovou kopii operačního systému, nepoužívejte možnost nasazení ke **stahování obsahu místně, pokud to vyžaduje běžící pořadí úloh**. Když pořadí úkolů vymaže disk dříve, než použije bitovou kopii operačního systému, odebere mezipaměť klienta. Vzhledem k tomu, že je obsah pryč, pořadí úkolů se nezdařilo.<!-- SCCMDocs-PR #1338 --> Tyto možnosti nasazení jsou dynamické na základě dalších možností, které jste vybrali pro nasazení. Další informace naleznete v části [Deploy a task sequence](deploy-a-task-sequence.md#bkmk_deploy-options).<!-- MEMDocs#328, SCCMDocs#2114 -->

## <a name="user-experience"></a>Uživatelské prostředí

- Když klient obdrží zásadu nasazení, začne obsah předem ukládat do mezipaměti po dostupném čase nasazení. Tento obsah zahrnuje všechny odkazované balíčky, ale pouze balíček s upgradem operačního systému, který odpovídá architektuře a atributům jazyka v balíčku.  

- Když klient zpřístupní nasazení pro uživatele, zobrazí se oznámení upozorňující uživatele na nové nasazení. Teď je pořadí úkolů zobrazené v centru softwaru. Uživatel může přejít do centra softwaru a kliknutím na tlačítko **nainstalovat** spustit instalaci.  

- Pokud klient nemá plně uložený obsah do mezipaměti, když ho uživatel nainstaluje, pak klient použije nastavení, které zadáte na kartě **možnost nasazení** v nasazení.  

## <a name="see-also"></a>Viz také

- [Vytvoření pořadí úkolů pro upgrade operačního systému](create-a-task-sequence-to-upgrade-an-operating-system.md)
- [Scénář upgradu Windows na nejnovější verzi](upgrade-windows-to-the-latest-version.md)
