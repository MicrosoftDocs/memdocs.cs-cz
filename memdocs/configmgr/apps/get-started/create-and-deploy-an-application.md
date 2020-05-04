---
title: Vytvoření a nasazení aplikace
titleSuffix: Configuration Manager
description: Vytvořte a nasaďte aplikaci, která obsahuje obchodní aplikaci, a Naučte se efektivně spravovat aplikace.
ms.date: 07/19/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 3bd1e487-ea18-43c1-b7c3-acbd9b86d429
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: b2d2a3465aebf66db37722629991078093abaaa7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710507"
---
# <a name="create-and-deploy-an-application-with-configuration-manager"></a>Vytvoření a nasazení aplikace pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

V tomto tématu přejdete přímo do části a vytvoříte aplikaci pomocí Configuration Manager. V tomto příkladu vytvoříte a nasadíte aplikaci, která obsahuje obchodní aplikaci pro počítače s Windows nazvanou **contoso. msi**, kterou je třeba nainstalovat na všechny počítače s Windows 10 ve vaší společnosti. V takovém případě se naučíte spoustu věcí, ke kterým můžete efektivně spravovat aplikace.  

 Tento postup je navržený tak, aby vám poskytl přehled o tom, jak vytvářet a nasazovat aplikace Configuration Manager. Nezabývá se však všemi možnostmi konfigurace nebo vytvořením a nasazením aplikací pro jiné platformy.  

 Konkrétní podrobnosti, které jsou relevantní pro jednotlivé platformy, najdete v jednom z následujících témat:  

- [Vytváření aplikací pro Windows](creating-windows-applications.md)
- [Vytváření aplikací pro Windows Phone](../../mdm/deploy-use/management-tasks-applications.md#bkmk_winphone)
- [Vytváření aplikací pro počítače Mac](creating-mac-computer-applications.md)
- [Vytváření aplikací pro servery Linux a UNIX](creating-linux-and-unix-server-applications.md)
- [Vytváření aplikací pro Windows Embedded](creating-windows-embedded-applications.md)


Pokud jste již obeznámeni s Configuration Manager aplikacemi, můžete toto téma přeskočit. Můžete ale chtít si projít téma [Create Applications](../../apps/deploy-use/create-applications.md) , kde najdete informace o všech možnostech, které jsou k dispozici při vytváření a nasazování aplikací.  

## <a name="before-you-start"></a>Než začnete  

Ujistěte se, že jste si přečetli informace v tématu [Úvod do správy aplikací](../understand/introduction-to-application-management.md) , abyste měli připravený web k instalaci aplikací a pochopení terminologie používané v tomto tématu.  

 Také se ujistěte, že jsou instalační soubory pro aplikaci **contoso. msi** v dostupném umístění v síti.  

## <a name="create-the-configuration-manager-application"></a>Vytvoření aplikace nástroje Configuration Manager  

### <a name="to-start-the-create-application-wizard-and-create-the-application"></a>Spuštění Průvodce vytvořením aplikace a vytvoření aplikace  

1. V konzole Configuration Manager vyberte možnost **softwarová knihovna** > aplikace**Správa** > **Applications**aplikací.  

2. Na kartě **Domů** ve skupině **vytvořit** vyberte možnost **vytvořit aplikaci**.  

3. Na stránce **Obecné** v nástroji **Průvodce vytvořením aplikace**vyberte možnost **automaticky zjišťovat informace o této aplikaci z instalačních souborů**. Tím se předem naplní některé informace v průvodci informacemi, které se extrahují ze souboru instalace. msi. Pak zadejte následující informace:  

   - **Typ**: vyberte **Instalační služba systému Windows (\*soubor. msi)**.  

   - **Umístění**: zadejte umístění (nebo zvolte **Procházet** a vyberte umístění) instalačního souboru **contoso. msi**. Všimněte si, že umístění musí být zadané ve formátu * \\\Server\Share\File* , kde se Configuration Manager najít instalační soubory.  

   Skončíte s něčím, co vypadá jako na následujícím snímku obrazovky:  

   ![Stránka Obecné Průvodce správou aplikací](media/App-management-wizard-general-page.png)  

4. Zvolte **Další**. Na stránce **importovat informace** se zobrazí některé informace o aplikaci a všechny související soubory, které byly naimportovány do Configuration Manager. Až budete hotovi, klikněte znovu na **Další** .  

5. Na stránce **Obecné informace** můžete zadávat další informace o aplikaci, které vám pomůžou je seřadit a vyhledat v konzole Configuration Manager.  

    Kromě toho vám pole **instalační program** umožní určit úplný příkazový řádek, který se použije k instalaci aplikace do počítačů. Tuto možnost můžete upravit a přidat tak vlastní vlastnosti (například **/q** pro bezobslužnou instalaci).  

   > [!TIP]  
   > Některá pole na této stránce průvodce se můžou vyplnit automaticky při importu instalačních souborů aplikace.  

    Nakonec se zobrazí obrazovka, která bude vypadat podobně jako na následujícím snímku obrazovky:  

    ![Stránka Obecné informace Průvodce správou aplikací](media/App-management-wizard-general-information-page.png)  

6. Zvolte **Další**. Na stránce Souhrn můžete potvrdit nastavení aplikace a potom průvodce Dokončit.  

   Tím je vytváření aplikace hotové. Pokud ji chcete najít, v pracovním prostoru **softwarová knihovna** rozbalte možnost **Správa aplikací**a pak zvolte možnost **aplikace**. V našem příkladě se zobrazí:  

   ![Grafika finální aplikace](media/Final-app-graphic.png)  

## <a name="examine-the-properties-of-the-application-and-its-deployment-type"></a>Podívejte se na vlastnosti aplikace a na její typ nasazení.  

Teď, když jste vytvořili aplikaci, můžete v případě potřeby Upřesnit nastavení aplikace. Chcete-li se podívat na vlastnosti aplikace, vyberte aplikaci a poté na kartě **Domů** ve skupině **vlastnosti** zvolte možnost **vlastnosti**.  

 V dialogovém okně **<\> – vlastnosti aplikace Contoso** se zobrazí mnoho položek, které můžete nakonfigurovat pro upřesnění chování aplikace. Podrobnosti o všech nastaveních, která můžete konfigurovat, najdete v tématu věnovaném [vytváření aplikací](../../apps/deploy-use/create-applications.md). Pro účely tohoto příkladu budeme měnit jenom některé vlastnosti týkající se typu nasazení aplikace.  

 Vyberte kartu **typy nasazení** > typ nasazení **aplikace Contoso** > **Upravit**.

Zobrazí se dialogové okno podobné následujícímu:  

![Stránka vlastností aplikace pro správu aplikací](media/App-management-app-properties-page.png)  

## <a name="add-a-requirement-to-the-deployment-type"></a>Přidání požadavku k typu nasazení

 Požadavky určují podmínky, které je nutné splnit, než bude možné nainstalovat aplikaci do klientského zařízení.  Můžete si vybrat z předdefinovaných požadavků, nebo můžete vytvořit svoje vlastní. V tomto příkladu přidáte požadavek, který bude aplikace nainstalována pouze na počítače se systémem Windows 10.  

1. Na stránce vlastnosti typu nasazení, kterou jste právě otevřeli, klikněte na kartu **požadavky** .  

2. Kliknutím na tlačítko **Přidat** otevřete dialogové okno **vytvořit požadavek** .  

3. V dialogovém okně **Vytvořit požadavek** zadejte následující údaje:  

    - **Kategorie**: **zařízení**  

    - **Podmínka**: **operační systém**  

    - **Typ pravidla**: **hodnota**  

    - **Operátor**: **jedna z**  

    - Ze seznamu operačních systémů vyberte **Windows 10**.  

    Zobrazí se dialogové okno, které vypadá takto:  

    ![Stránka požadavky na správu aplikací](media/App-management-requirements-page.png)  

4. Kliknutím na **tlačítko OK** zavřete každou otevřenou stránku vlastností. Pak se vraťte do seznamu **aplikace** v konzole Configuration Manager.  

> [!TIP]  
> Požadavky mohou přispět ke snížení počtu potřebných kolekcí Configuration Manager. Protože jste právě určili, že se aplikace dá nainstalovat jenom na počítače s Windows 10, můžete ji později nasadit do kolekce, která obsahuje počítače, na kterých běží spousta různých operačních systémů. Ale aplikace se nainstaluje jenom na počítače s Windows 10.

## <a name="add-the-application-content-to-a-distribution-point"></a>Přidání obsahu aplikace do distribučního bodu  

V dalším kroku nasazení aplikace do počítačů se ujistěte, že se obsah aplikace zkopíroval do distribučního bodu. Počítače mají přístup k distribučnímu bodu pro instalaci aplikace.  

> [!TIP]  
> Další informace o distribučních bodech a správě obsahu v Configuration Manager najdete v tématu [Správa obsahu a infrastruktury obsahu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).

1. V konzole Configuration Manager vyberte možnost **softwarová knihovna**.  

2. V pracovním prostoru **softwarová knihovna** rozbalte položku **aplikace**. Pak v seznamu aplikací vyberte **aplikaci Contoso** , kterou jste vytvořili.  

3. Na kartě **Domů** ve skupině **nasazení** klikněte na možnost **distribuovat obsah**.  

4. Na stránce **Obecné** v **Průvodci distribucí obsahu**zkontrolujte, že je název aplikace správný, a klikněte na tlačítko **Další**.  

5. Na stránce **obsah** zkontrolujte informace, které budou zkopírovány do distribučního bodu, a klikněte na tlačítko **Další**.  

6. Na stránce **cíl obsahu** zvolte možnost **Přidat** a vyberte jeden nebo více distribučních bodů nebo skupin distribučních bodů, na které chcete nainstalovat obsah aplikace.  

7. Dokončete průvodce.  

Obsah aplikace se úspěšně zkopíroval do distribučního bodu v pracovním prostoru **monitorování** v části stav **distribuce** > stav**obsahu**.  

## <a name="deploy-the-application"></a>Nasazení aplikace  

V dalším kroku nasaďte aplikaci do kolekce zařízení ve vaší hierarchii. V tomto příkladu nasadíte aplikaci do kolekce zařízení **všechny systémy** .  

> [!TIP]  
> Pamatujte, že aplikace bude instalovat jenom počítače s Windows 10 z důvodu požadavků, které jste předtím vybrali.

1. V konzole Configuration Manager vyberte možnost **softwarová knihovna** > aplikace**Správa** > **Applications**aplikací.  

2. V seznamu aplikací vyberte aplikaci, kterou jste vytvořili dříve (**aplikace Contoso**), a potom na kartě **Domů** ve skupině **nasazení** zvolte **nasadit**.  

3. Na stránce **Obecné** v nástroji **Průvodce nasazením softwaru**vyberte možnost **Procházet** a vyberte kolekci zařízení **všechny systémy** .  

4. Na stránce **obsah** ověřte, zda je vybrán distribuční bod, ze kterého chcete nainstalovat aplikaci počítače.  

5. Na stránce **nastavení nasazení** se ujistěte, že je akce nasazení nastavená na **nainstalovat**a že je účel nasazení nastavený na **požadováno**.  

    > [!TIP]  
    > Nastavením účelu nasazení na **požadováno**se ujistěte, že je aplikace nainstalovaná na počítačích, které splňují požadavky, které jste nastavili. Pokud tuto možnost nastavíte na hodnotu **Dostupné**, uživatelé budou moct aplikaci nainstalovat na vyžádání z Centra softwaru.

6. Na stránce **Plánování** můžete nastavit, kdy se má aplikace nainstalovat. V tomto příkladu vyberte **Co nejdříve po času dostupnosti**.  

7. Na stránce **činnost koncového uživatele** se kliknutím na tlačítko **Další** přijměte výchozí hodnoty.  

8. Dokončete průvodce.  

K zobrazení stavu nasazení aplikace použijte informace v následujícím tématu **sledování aplikace** .  

## <a name="monitor-the-application"></a>Monitorování aplikace

 V této části se můžete rychle podívat na stav nasazení aplikace, kterou jste právě nasadili.  

### <a name="to-review-the-deployment-status"></a>Kontrola stavu nasazení  

1. V konzole Configuration Manager vyberte možnost **monitorování** > **nasazení**.  

2. Ze seznamu nasazení vyberte položku **Aplikace Contoso**.  

3. Na kartě **Domů** ve skupině **nasazení** vyberte možnost **Zobrazit stav**.  

4. Výběrem jedné z následujících karet zobrazíte další aktualizace stavu nasazení aplikace:  

    - **Úspěch**: aplikace je úspěšně nainstalovaná na uvedených počítačích.  

    - **Probíhá**: aplikace ještě nebyla dokončena při instalaci.  

    - **Chyba**: při instalaci aplikace na uvedené počítače došlo k chybě. Zobrazí se také další informace o chybě.  

    - **Požadavky nejsou splněny**: na označených zařízeních nebyl proveden žádný pokus o instalaci, protože nesplňovaly požadavky, které jste nakonfigurovali (v tomto příkladu, protože neběží ve Windows 10).  

    - **Neznámé**: Configuration Manager nemohl ohlásit stav nasazení. Zkuste to znovu později.  

> [!TIP]  
> Existuje několik způsobů, jak můžete monitorovat nasazení aplikací. Úplné podrobnosti najdete v tématu [monitorování aplikací](../deploy-use/monitor-applications-from-the-console.md).

## <a name="end-user-experience"></a>Prostředí koncového uživatele  

Uživatelům, kteří mají počítače spravované nástrojem Configuration Manager a systémem Windows 10, se zobrazí zpráva s oznámením, že musí nainstalovat aplikaci Contoso. Po přijetí instalace se aplikace nainstaluje.  

Configuration Manager počínaje verzí 1906 **je nový software k dispozici** oznámení, že pro danou aplikaci a revizi se pro uživatele zobrazí jenom jednou. Uživatel se už nebude zobrazovat oznámení pokaždé, když se přihlásí. Pro aplikaci uvidí jenom další oznámení, pokud se aplikace změnila nebo byla znovu nasazena.

## <a name="next-steps"></a>Další kroky

[Monitorování aplikací](../deploy-use/monitor-applications-from-the-console.md)
