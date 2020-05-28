---
title: Nasadit obsah
titleSuffix: Configuration Manager
description: Po instalaci distribučních bodů pro Configuration Manager můžete začít nasazovat obsah do těchto umístění.
ms.date: 05/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d50dcca0-4419-449d-a487-73abcadf328f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df26fe91f009a1a4f5d3c5a4f4adb5fe45bbd245
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343146"
---
# <a name="deploy-and-manage-content-for-configuration-manager"></a>Nasazení a Správa obsahu pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Po instalaci distribučních bodů pro Configuration Manager můžete začít s nasazením obsahu. Obvykle se přenosy obsahu do distribučních bodů v síti, ale i další možnosti, jak získat obsah do distribučních bodů, existují. Po přenosu obsahu do distribučního bodu můžete aktualizovat, znovu distribuovat, odebrat a ověřit obsah v distribučních bodech.  

##  <a name="distribute-content"></a><a name="bkmk_distribute"></a>Distribuovat obsah  
Obvykle distribuujete obsah do distribučních bodů tak, aby byl dostupný pro klientské počítače. (Výjimkou je tato výjimka při použití distribuce obsahu na vyžádání pro konkrétní nasazení.) Když distribuujete obsah, Configuration Manager ukládá soubory obsahu do balíčku a potom balíček distribuuje do distribučního bodu. Obsah balíčku se načte z knihovny obsahu serveru lokality. Typy obsahu, které můžete distribuovat, zahrnují:  

- Typy nasazení aplikace  

- Balíčky  

- Balíčky pro nasazení  

- Balíčky ovladačů  

- Bitové kopie operačního systému  

- Instalační programy operačního systému  

- Spouštěcí image  

- Pořadí úloh  

Když vytvoříte balíček, který obsahuje zdrojové soubory, například typ nasazení aplikace nebo balíček nasazení, lokalita, ve které balíček vytvoříte, se bude vlastníkem lokality pro zdroj obsahu balíčku. Configuration Manager zkopíruje zdrojové soubory z cesty zdrojových souborů, které zadáte pro objekt do knihovny obsahu na serveru lokality, který vlastní zdroj obsahu balíčku.  Pak Configuration Manager replikuje informace do dalších lokalit. (Další informace o tomto tématu najdete v [knihovně obsahu](../../../../core/plan-design/hierarchy/the-content-library.md) .)  

K distribuci obsahu do distribučních bodů použijte následující postup.  

#### <a name="to-distribute-content-on-distribution-points"></a>Distribuce obsahu do distribučních bodů  

1.  V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  

2.  V pracovním prostoru **softwarová knihovna** vyberte jeden z následujících kroků pro typ obsahu, který chcete distribuovat:  

    - **Aplikace**: rozbalte položku aplikace **pro správu aplikací**  >  **Applications**a potom vyberte aplikace, které chcete distribuovat.  

    - **Balíčky**: rozbalte položku balíčky **pro správu aplikací**  >   **Packages**a potom vyberte balíčky, které chcete distribuovat.  

    - **Balíčky pro nasazení**: rozbalte balíčky pro nasazení **aktualizací softwaru**  >   **Deployment Packages**a potom vyberte balíčky pro nasazení, které chcete distribuovat.  

    - **Balíčky ovladačů**: rozbalte **Operating Systems**  >   **balíčky ovladačů**operačních systémů a pak vyberte balíčky ovladačů, které chcete distribuovat.  

    - **Bitové kopie operačního systému**: **rozbalte**  >   **image operačního systému**a potom vyberte image operačního systému, které chcete distribuovat.  

    - **Instalační programy operačního systému**: rozbalte položku **operační systémy**  >  **instalační programy operačního systému**a pak vyberte instalační programy operačního systému, které chcete distribuovat.  

    - **Spouštěcí bitové kopie**: rozbalte **Operating Systems**  >   **spouštěcí bitové kopie**operačních systémů a pak vyberte spouštěcí bitové kopie, které chcete distribuovat.  

    - **Pořadí úloh**: rozbalte **Operating Systems**  >   **pořadí úloh**operační systémy a potom vyberte pořadí úkolů, které chcete distribuovat. Přestože pořadí úloh neobsahují obsah, mají přidružené závislosti obsahu, které jsou distribuovány.  

      > [!NOTE]  
      > Pokud upravíte pořadí úloh, musíte znovu distribuovat obsah.  

3.  Na kartě **Domů** ve skupině **Nasazení** klikněte na možnost **Distribuovat obsah**. Otevře se Průvodce distribucí obsahu.  

4.  Na stránce **Obecné** ověřte, že uvedený obsah je obsah, který chcete distribuovat, vyberte, jestli chcete, aby Configuration Manager detekovat závislosti obsahu, které jsou přidružené k vybranému obsahu, a přidejte závislosti do distribuce a pak klikněte na **Další**.  

    > [!NOTE]  
    > Máte možnost konfigurovat **závislosti přidruženého obsahu a přidat je do tohoto nastavení distribuce** pouze pro typ obsahu aplikace. Configuration Manager automaticky nakonfiguruje toto nastavení pro pořadí úloh a nedá se změnit.  

5.  Na kartě **obsah** (Pokud se zobrazí) ověřte, zda je uvedený obsah obsahem, který chcete distribuovat, a poté klikněte na tlačítko **Další**.  

    > [!NOTE]  
    > Stránka **obsah** se zobrazí pouze v případě, že je vybrána možnost **detekovat závislosti přidruženého obsahu a přidat je do tohoto nastavení distribuce** na stránce **Obecné** v průvodci.  

6.  Na stránce **cíl obsahu** klikněte na tlačítko **Přidat**, vyberte jednu z následujících možností a pak postupujte podle příslušného kroku:  

    - **Kolekce**: Vyberte kolekce **uživatelů** nebo **kolekce zařízení**, klikněte na kolekci spojenou s jednou nebo více skupinami distribučních bodů a pak klikněte na **OK**.  

        > [!NOTE]  
        > Zobrazí se pouze kolekce, které jsou přidruženy ke skupině distribučních bodů. Další informace o přidružení kolekcí ke skupinám distribučních bodů najdete v tématu [Správa skupin distribučních](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) bodů v tématu [instalace a konfigurace distribučních bodů pro Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) .  

    - **Distribuční bod**: Vyberte existující distribuční bod a klikněte na tlačítko **OK**. Distribuční body, které dříve obdržely obsah, se nezobrazí.  

    - **Skupina distribučních bodů**: Vyberte existující skupinu distribučních bodů a klikněte na tlačítko **OK**. Skupiny distribučních bodů, které dříve obdržely obsah, se nezobrazí.  

    Po dokončení přidávání umístění obsahu klikněte na tlačítko **Další**.  

7.  Než budete pokračovat, na stránce **Souhrn** zkontrolujte nastavení distribuce. Chcete-li distribuovat obsah do vybraných míst, klikněte na tlačítko **Další**.  

8.  Stránka **průběh** zobrazuje průběh distribuce.  

9. Stránka **potvrzení** zobrazuje, zda byl obsah úspěšně přiřazen k bodům. Informace o monitorování distribuce obsahu najdete v tématu [monitorování obsahu distribuovaného pomocí Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

##  <a name="use-prestaged-content"></a><a name="bkmk_prestage"></a>Použití připraveného obsahu  
Soubory obsahu můžete připravit pro aplikace a typy balíčků:  

- V konzole Configuration Manager vyberte požadovaný obsah a pak pomocí **Průvodce vytvořením souboru připraveného obsahu** vytvořte komprimovaný soubor připraveného obsahu, který obsahuje soubory a související metadata pro obsah, který jste vybrali.  

- Pak můžete ručně importovat obsah serveru lokality, sekundární lokality nebo distribučního bodu.  

- Když importujete soubor připraveného obsahu na server lokality, soubory obsahu se přidají do knihovny obsahu na serveru lokality a potom se zaregistrují v databázi serveru lokality.  

- Když importujete soubor připraveného obsahu do distribučního bodu, soubory obsahu se přidají do knihovny obsahu v distribučním bodě a na server lokality se pošle stavová zpráva, která lokalitu informuje o tom, že obsah je k dispozici v distribučním bodě.  

**Omezení a požadavky pro připravený obsah:**  

- **Pokud je distribuční bod umístěn na serveru lokality**, nepovolujte distribuční bod pro připravený obsah. Místo toho použijte postup v tématu [Příprava obsahu v distribučním bodě na serveru lokality](#bkmk_dpsiteserver).  

- **Pokud je distribuční bod konfigurován jako distribuční bod pro vyžádání**obsahu, nepovolujte distribuční bod pro připravený obsah. Konfigurace připraveného obsahu pro distribuční bod přepisuje konfiguraci distribučního bodu pro vyžádání obsahu. Distribuční bod pro vyžádání obsahu, který je konfigurován pro připravený obsah, nezískává obsah ze zdrojového distribučního bodu a nepřijímá obsah ze serveru lokality.  

- Aby bylo **možné připravit obsah na distribuční bod, musí být knihovna obsahu vytvořena na distribučním bodu**. Před přístupným obsahem do distribučního bodu distribuujte obsah přes síť alespoň jednou.  

- Když připravujete **obsah pro balíček s dlouhou zdrojovou cestou balíčku** (například více než 140 znaků), nástroj příkazového řádku rozbalit obsah se nemusí podařit úspěšně extrahovat obsah pro tento balíček do knihovny obsahu.  

Informace o tom, jak připravit soubory obsahu, najdete v tématu *připravený obsah* v tématu [Správa šířky pásma sítě pro správu obsahu](../../../plan-design/hierarchy/manage-network-bandwidth.md) .  

K přednastavení obsahu použijte následující části.  

###  <a name="step-1-create-a-prestaged-content-file"></a><a name="BKMK_CreatePrestagedContentFile"></a>Krok 1: vytvoření souboru připraveného obsahu  
Můžete vytvořit komprimovaný soubor připraveného obsahu, který obsahuje soubory a související metadata pro obsah, který vyberete v konzole Configuration Manager. Pomocí následujícího postupu můžete vytvořit soubor připraveného obsahu.  

##### <a name="to-create-a-prestaged-content-file"></a>Vytvoření souboru připraveného obsahu  

1.  V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  

2.  V pracovním prostoru **softwarová knihovna** vyberte jeden z následujících kroků pro typ obsahu, který chcete připravit:  

    - **Aplikace**: rozbalte možnost **Správa aplikací**, klikněte na **aplikace**a potom vyberte aplikace, které chcete připravit.  

    - **Balíčky**: rozbalte možnost **Správa aplikací**, klikněte na **balíčky**a potom vyberte balíčky, které chcete připravit.  

    - **Balíčky ovladačů**: rozbalte možnost **operační systémy**, klikněte na **balíčky ovladačů**a pak vyberte balíčky ovladačů, které chcete připravit.  

    - **Bitové kopie operačního systému**: rozbalte možnost **operační systémy**, klikněte na **bitové kopie operačního systému**a potom vyberte image operačního systému, které chcete připravit.  

    - **Instalační programy operačního systému**: rozbalte možnost **operační systémy**, klikněte na **instalační programy operačního systému**a pak vyberte instalační programy operačního systému, které chcete připravit.  

    - **Spouštěcí bitové kopie**: rozbalte možnost **operační systémy**, klikněte na **spouštěcí bitové kopie**a pak vyberte spouštěcí bitové kopie, které chcete připravit.  

    - **Pořadí úloh**: rozbalte možnost **operační systémy**, klikněte na možnost **pořadí úloh**a pak vyberte pořadí úloh, které chcete připravit.  

3.  Na kartě **Domů** ve skupině **nasazení** klikněte na možnost **vytvořit soubor připraveného obsahu**. Spustí se Průvodce vytvořením souboru připraveného obsahu.  

    > [!NOTE]  
    > **Pro aplikace:** Na kartě **Domů** ve skupině **aplikace** klikněte na možnost **vytvořit soubor připraveného obsahu**.  
    >   
    > **Pro balíčky:** Na kartě **Domů** ve &lt; skupině> *aktualizace* klikněte na možnost **vytvořit soubor připraveného obsahu**.  

4.  Na stránce **Obecné** klikněte na tlačítko **Procházet**, zvolte umístění souboru připraveného obsahu, zadejte název souboru a potom klikněte na tlačítko **Uložit**. Tento soubor připraveného obsahu můžete použít na serverech primární lokality, serverech sekundární lokality nebo distribučních bodech pro import obsahu a metadat.  

5.  Pro aplikace vyberte **exportovat všechny závislosti** , aby Configuration Manager zjistila a přidala závislosti přidružené k aplikaci do souboru připraveného obsahu. Toto nastavení je ve výchozím nastavení vybráno.  

6.  V části **Komentáře správce**zadejte volitelné komentáře k souboru připraveného obsahu a potom klikněte na tlačítko **Další**.  

7.  Na stránce **obsah** ověřte, zda je uvedený obsah obsahem, který chcete přidat do souboru připraveného obsahu, a poté klikněte na tlačítko **Další**.  

8.  Na stránce **umístění obsahu** určete distribuční body, ze kterých mají být načteny soubory obsahu pro soubor připraveného obsahu. Můžete vybrat více než jeden distribuční bod pro načtení obsahu. Distribuční body jsou uvedeny v části umístění obsahu. Sloupec **obsah** zobrazuje, kolik vybraných balíčků nebo aplikací je dostupných v každém distribučním bodě. Configuration Manager začíná prvním distribučním bodem v seznamu, aby se načetl vybraný obsah, a pak se přesune seznam za účelem získání zbývajícího obsahu požadovaného pro soubor připraveného obsahu. Chcete-li změnit pořadí priorit distribučních bodů **, klikněte na tlačítko nahoru nebo** **dolů.** Pokud distribuční body v seznamu neobsahují veškerý vybraný obsah, je nutné přidat distribuční body do seznamu, který obsahuje obsah, nebo ukončit průvodce, distribuovat obsah do alespoň jednoho distribučního bodu a pak restartovat průvodce.  

9. Na stránce **Souhrn** potvrďte podrobnosti. Můžete přejít zpět na předchozí stránky a provést změny. Klikněte na tlačítko **Další** a vytvořte soubor připraveného obsahu.  

10. Stránka **průběh** zobrazuje obsah, který se přidává do souboru připraveného obsahu.  

11. Na stránce **dokončení** ověřte, zda byl soubor připraveného obsahu úspěšně vytvořen, a poté klikněte na tlačítko **Zavřít**.  

###  <a name="step-2-assign-the-content-to-distribution-points"></a><a name="BKMK_AssignContentToDistributionPoint"></a>Krok 2: přiřazení obsahu do distribučních bodů  
 Po přípravě souboru obsahu přiřaďte obsah do distribučních bodů.  

> [!NOTE]  
> Použijete-li soubor připraveného obsahu k obnovení knihovny obsahu na serveru lokality a není nutné připravovat soubory obsahu v distribučním bodě, můžete tento postup přeskočit.  

 K přiřazení obsahu v souboru připraveného obsahu do distribučních bodů použijte následující postup.  

> [!IMPORTANT]  
> Ověřte, zda jsou distribuční body, které chcete připravit, konfigurovány jako připravené distribuční body nebo zda je obsah distribuován do distribučních bodů pomocí sítě.  

##### <a name="to-assign-the-content-to-distribution-points"></a>Přiřazení obsahu do distribučních bodů  

1.  V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  

2.  V pracovním prostoru **softwarová knihovna** vyberte jeden z následujících kroků pro typ obsahu, který jste vybrali při vytváření souboru připraveného obsahu:  

    - **Aplikace**: rozbalte možnost **Správa aplikací**, klikněte na **aplikace**a potom vyberte aplikace, které jste připravili.  

    - **Balíčky**: rozbalte možnost **Správa aplikací**, klikněte na **balíčky**a potom vyberte balíčky, které jste připravili.  

    - **Balíčky pro nasazení**: rozbalte možnost **aktualizace softwaru**, klikněte na **balíčky pro nasazení**a potom vyberte balíčky pro nasazení, které jste připravili.  

    - **Balíčky ovladačů**: rozbalte možnost **operační systémy**, klikněte na **balíčky ovladačů**a pak vyberte balíčky ovladačů, které jste připravili.  

    - **Bitové kopie operačního systému**: rozbalte možnost **operační systémy**, klikněte na **bitové kopie operačního systému**a pak vyberte bitové kopie operačního systému, které jste připravili.  

    - **Instalační programy operačního systému**: rozbalte možnost **operační systémy**, klikněte na **instalační programy operačního systému**a pak vyberte instalační programy operačního systému, které jste připravili.  

    - **Spouštěcí bitové kopie**: rozbalte možnost **operační systémy**, klikněte na **spouštěcí bitové kopie**a pak vyberte spouštěcí bitové kopie, které jste připravili.  

3.  Na kartě **Domů** ve skupině **Nasazení** klikněte na možnost **Distribuovat obsah**. Otevře se Průvodce distribucí obsahu.  

4.  Na stránce **Obecné** ověřte, že je zobrazený obsah, který jste připravili, vyberte, jestli chcete, Configuration Manager zjišťovat závislosti obsahu, které jsou přidružené k vybranému obsahu, a přidejte závislosti do distribuce a pak klikněte na **Další**.  

    > [!NOTE]  
    > Máte možnost konfigurovat **závislosti přidruženého obsahu a přidat je do tohoto nastavení distribuce** pouze pro typ obsahu aplikace. Configuration Manager automaticky nakonfiguruje toto nastavení pro pořadí úloh a nedá se změnit.  

5.  V případě zobrazení na stránce **obsah** ověřte, zda je uvedený obsah obsahem, který chcete distribuovat, a poté klikněte na tlačítko **Další**.  

    > [!NOTE]  
    > Stránka **obsah** se zobrazí pouze v případě, že je vybrána možnost **detekovat závislosti přidruženého obsahu a přidat je do tohoto nastavení distribuce** na stránce **Obecné** v průvodci.  

6.  Na stránce **cíl obsahu** klikněte na tlačítko **Přidat**, vyberte jednu z následujících možností, která zahrnuje distribuční body, které mají být předem připravené, a pak postupujte podle příslušného kroku:  

    - **Kolekce**: Vyberte kolekce **uživatelů** nebo **kolekce zařízení**, klikněte na kolekci spojenou s jednou nebo více skupinami distribučních bodů a pak klikněte na **OK**.  

      > [!NOTE]  
      > Zobrazí se pouze kolekce, které jsou přidruženy ke skupině distribučních bodů.  Další informace najdete v tématu [Správa skupin distribučních bodů](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) v tématu [instalace a konfigurace distribučních bodů pro Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) .  

    - **Distribuční bod**: Vyberte existující distribuční bod a klikněte na tlačítko **OK**. Distribuční body, které dříve obdržely obsah, se nezobrazí.  

    - **Skupina distribučních bodů**: Vyberte existující skupinu distribučních bodů a klikněte na tlačítko **OK**. Skupiny distribučních bodů, které dříve obdržely obsah, se nezobrazí.  

    Po dokončení přidávání umístění obsahu klikněte na tlačítko **Další**.  

7.  Než budete pokračovat, na stránce **Souhrn** zkontrolujte nastavení distribuce. Chcete-li distribuovat obsah do vybraných míst, klikněte na tlačítko **Další**.  

8.  Stránka **průběh** zobrazuje průběh distribuce.  

9. Stránka **potvrzení** zobrazuje, zda byl obsah úspěšně přiřazen do distribučních bodů. Informace o monitorování distribuce obsahu najdete v tématu [monitorování obsahu distribuovaného pomocí Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

###  <a name="step-3-extract-the-content-from-the-prestaged-content-file"></a><a name="BKMK_ExportContentFromPrestagedContentFile"></a>Krok 3: extrakce obsahu ze souboru připraveného obsahu  
Po vytvoření souboru připraveného obsahu a přiřazení obsahu do distribučních bodů můžete extrahovat soubory obsahu do knihovny obsahu na serveru lokality nebo v distribučním bodě. Obvykle jste zkopírovali soubor připraveného obsahu na přenosné jednotky, jako je například jednotka USB, nebo jste vypáleni obsah na médium, jako je DVD, a máte k dispozici v umístění serveru lokality nebo distribučního bodu, který vyžaduje obsah.  

Pomocí následujícího postupu můžete ručně exportovat soubory obsahu ze souboru připraveného obsahu pomocí nástroje příkazového řádku rozbalit obsah.  

> [!IMPORTANT]  
> Když spustíte nástroj příkazového řádku rozbalit obsah, nástroj vytvoří dočasný soubor při vytváření souboru připraveného obsahu. Pak se soubor zkopíruje do cílové složky a dočasný soubor se odstraní. Musíte mít dostatek místa na disku pro tento dočasný soubor, jinak se proces nezdařil. Dočasný soubor se vytvoří v následujícím umístění:  
>   
> - Dočasný soubor se vytvoří ve stejné složce, kterou zadáte jako cílovou složku pro soubor připraveného obsahu.  

> [!IMPORTANT]  
> Uživatel, který spouští nástroj příkazového řádku rozbalit obsah, musí mít v počítači, ze kterého extrahujete připravený obsah, oprávnění **správce** .  

##### <a name="to-extract-the-content-files-from-the-prestaged-content-file"></a>Extrakce souborů obsahu ze souboru připraveného obsahu  

1.  Zkopírujte soubor připraveného obsahu do počítače, ze kterého chcete extrahovat obsah.  

2.  Zkopírujte nástroj příkazového řádku rozbalit obsah z &lt; *ConfigMgrInstallationPath*> \\ &lt;>*platformy* \Bin do počítače, ze kterého chcete soubor připraveného obsahu extrahovat.  

3.  Otevřete příkazový řádek a přejděte do umístění složky souboru připraveného obsahu a rozbalte nástroj obsah.  

    > [!NOTE]  
    > Jeden nebo více souborů připraveného obsahu můžete extrahovat na server lokality, sekundární server lokality nebo distribuční bod.  

4.  Zadejte **extractcontent/p:** &lt; *příkaz* > **\\** &lt; *PrestagedFileName* >  **/s** pro import jednoho souboru.  

    Zadejte **extractcontent/p:** &lt; *příkaz* >  **/s** pro import všech předzpracovaných souborů v zadané složce.  

    Například zadejte **extractcontent/p: D:\PrestagedFiles\MyPrestagedFile.pkgx/s** `D:\PrestagedFiles\` , kde je příkaz, `MyPrestagedFile.pkgx` je název předzpracovaného souboru a `/S` informují Configuration Manager k extrakci pouze souborů obsahu, které jsou novější, než je aktuálně na distribučním bodu.  

    Když extrahujete soubor připraveného obsahu na server lokality, soubory obsahu se přidají do knihovny obsahu na serveru lokality a pak se dostupnost obsahu zaregistruje v databázi serveru lokality. Pokud exportujete soubor připraveného obsahu do distribučního bodu, soubory obsahu budou přidány do knihovny obsahu v distribučním bodě, distribuční bod odešle stavovou zprávu nadřazenému serveru primární lokality a pak bude dostupnost obsahu registrována v databázi lokality.  

    > [!IMPORTANT]  
    > V následujícím scénáři je nutné aktualizovat obsah, který jste extrahovali ze souboru připraveného obsahu, když je obsah aktualizován na novou verzi:  
    >   
    >  1.  Vytvoříte soubor připraveného obsahu pro verzi 1 balíčku.  
    >  2.  Aktualizujete zdrojové soubory balíčku pomocí verze 2.  
    >  3.  Extrahujte soubor připraveného obsahu (verze 1 balíčku) do distribučního bodu.  
    >   
    > Configuration Manager automaticky distribuuje balíček verze 2 do distribučního bodu. Je nutné vytvořit nový soubor připraveného obsahu, který obsahuje novou verzi souboru, a poté extrahovat obsah, aktualizovat distribuční bod pro distribuci souborů, které se změnily, nebo znovu distribuovat všechny soubory v balíčku.  

###  <a name="how-to-prestage-content-on-a-distribution-point-on-a-site-server"></a><a name="bkmk_dpsiteserver"></a>Příprava obsahu v distribučním bodě na serveru lokality  
Pokud je distribuční bod nainstalován na serveru lokality nástroje, je nutné k úspěšné přípravě obsahu použít následující postup. Důvodem je to, že soubory obsahu jsou již v knihovně obsahu.  

Pokud distribuční bod není povolen pro předzpracovaný obsah nebo když distribuční bod není umístěn na serveru lokality, přečtěte si část [použití připraveného obsahu](#bkmk_prestage) v tomto tématu.  

##### <a name="to-prestage-content-on-distribution-points-located-on-a-site-server"></a>Příprava obsahu v distribučních bodech nacházejících se na serveru lokality  

1.  Pomocí následujících kroků ověřte, že distribuční bod není povolen pro připravený obsah.  

    1.  V konzole Configuration Manager klikněte na možnost **Správa**.  

    2.  V pracovním prostoru **Správa** klikněte na možnost **distribuční body**a poté vyberte distribuční bod, který je umístěn na serveru lokality.  

    3.  Na kartě **Domů** ve skupině **Vlastnosti** klikněte na možnost **Vlastnosti**.  

    4.  Na kartě **Obecné** ověřte, zda není zaškrtnuto políčko **Povolit tento distribuční bod pro připravený obsah** .  

2.  Vytvořte soubor připraveného obsahu pomocí [kroku 1: vytvoření souboru připraveného obsahu](#BKMK_CreatePrestagedContentFile) v tomto tématu.  

3.  Přiřaďte obsah distribučnímu bodu pomocí [kroku 2: přiřazení obsahu do distribučních bodů](#BKMK_AssignContentToDistributionPoint) v tomto tématu.  

4.  Na serveru lokality rozbalte obsah ze souboru připraveného obsahu pomocí [kroku 3: extrakce obsahu ze souboru připraveného obsahu](#BKMK_ExportContentFromPrestagedContentFile) v tomto tématu.  

    > [!NOTE]  
    > Pokud je distribuční bod v sekundární lokalitě, počkejte aspoň 10 minut a pak pomocí Configuration Manager konzolu, která je připojená k nadřazené primární lokalitě, přiřaďte obsah do distribučního bodu v sekundární lokalitě.  

##  <a name="manage-the-content-you-have-distributed"></a><a name="bkmk_manage"></a>Správa distribuovaného obsahu  
Pro správu obsahu máte následující možnosti:  
- [Aktualizovat obsah](#update-content)
- [Znovu distribuovat obsah](#redistribute-content)
- [Odebrat obsah](#remove-content)
- [ověřit obsah](#validate-content)

### <a name="update-content"></a>Aktualizovat obsah
Pokud je umístění zdrojových souborů pro nasazení Aktualizováno přidáním nových souborů nebo nahrazením existujících souborů novější verzí, můžete aktualizovat soubory obsahu v distribučních bodech pomocí akce **Aktualizovat distribuční body** nebo **Aktualizovat obsah** :  
- Soubory obsahu se zkopírují z původního zdrojového umístění balíčku do knihovny obsahu v lokalitě, která vlastní zdroj obsahu balíčku.
- Verze balíčku se zvýší.  
- Každá instance knihovny obsahu na serverech lokality a v distribučních bodech aktualizuje pouze soubory, které se změnily.  

> [!WARNING]  
> Verze balíčku pro aplikace je vždy 1. Když aktualizujete obsah pro typ nasazení aplikace, Configuration Manager vytvoří nové ID obsahu pro typ nasazení a balíček odkazuje na nové ID obsahu.  

#### <a name="to-update-content-on-distribution-points"></a>Aktualizace obsahu v distribučních bodech  

1.  V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  

2.  V pracovním prostoru **softwarová knihovna** vyberte jeden z následujících kroků pro typ obsahu, který chcete distribuovat:  

    - **Aplikace**: rozbalte položku aplikace **pro správu aplikací**  >  **Applications**a potom vyberte aplikace, které chcete distribuovat. Klikněte na kartu **typy nasazení** a potom vyberte typ nasazení, který chcete aktualizovat.  

    - **Balíčky**: rozbalte položku balíčky **pro správu aplikací**  >  **Packages**a potom vyberte balíčky, které chcete aktualizovat.  

    - **Balíčky pro nasazení**: rozbalte balíčky pro nasazení **aktualizací softwaru**  >  **Deployment Packages**a potom vyberte balíčky pro nasazení, které chcete aktualizovat.  

    - **Balíčky ovladačů**: rozbalte **Operating Systems**  >  **balíčky ovladačů**operačních systémů a pak vyberte balíčky ovladačů, které chcete aktualizovat.  

    - **Bitové kopie operačního systému**: **rozbalte**  >  **image operačního systému**a potom vyberte image operačního systému, které chcete aktualizovat.  

    - **Instalační programy operačního systému**: rozbalte položku **operační systémy**  >  **instalační programy operačního systému**a pak vyberte instalační programy operačního systému, které chcete aktualizovat.  

    - **Spouštěcí bitové kopie**: rozbalte **Operating Systems**  >   **spouštěcí bitové kopie**operačních systémů a pak vyberte spouštěcí bitové kopie, které chcete aktualizovat.  

3.  Na kartě **Domů** ve skupině **nasazení** klikněte na možnost **Aktualizovat distribuční body**a potom kliknutím na tlačítko **OK** potvrďte, že chcete aktualizovat obsah.  

    > [!NOTE]  
    > Chcete-li aktualizovat obsah pro aplikace, klikněte na kartu **typy nasazení** , klikněte pravým tlačítkem myši na typ nasazení, klikněte na příkaz **Aktualizovat obsah**a potom kliknutím na tlačítko **OK** potvrďte, že chcete aktualizovat obsah.  

    > [!NOTE]  
    > Když aktualizujete obsah pro spouštěcí bitové kopie, otevře se Průvodce správou distribučního bodu. Zkontrolujte informace na stránce **Souhrn** a pak dokončete průvodce, aby se obsah aktualizoval.  

### <a name="redistribute-content"></a>Znovu distribuovat obsah
Balíček můžete znovu distribuovat a kopírovat tak všechny soubory obsahu v balíčku do distribučních bodů nebo skupin distribučních bodů a přepsat tak stávající soubory.  

Tato operace slouží k opravě souborů obsahu v balíčku nebo k opětovnému odeslání obsahu, když počáteční distribuce nebude úspěšná. Balíček můžete znovu distribuovat z:  

- Vlastnosti balíčku  
- Vlastnosti distribučního bodu  
- Vlastnosti skupiny distribučních bodů.  


#### <a name="to-redistribute-content-from-package-properties"></a>Opětovné distribuce obsahu z vlastností balíčku  

1.  V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  

2.  V pracovním prostoru **softwarová knihovna** vyberte jeden z následujících kroků pro typ obsahu, který chcete distribuovat:  

    - **Aplikace**: rozbalte položku aplikace **pro správu aplikací**  >   **Applications**a potom vyberte aplikaci, kterou chcete znovu distribuovat.  

    - **Balíčky**: rozbalte položku balíčky **pro správu aplikací**  >  **Packages**a pak vyberte balíček, který chcete znovu distribuovat.  

    - **Balíčky pro nasazení**: rozbalte balíčky pro nasazení **aktualizací softwaru**  >   **Deployment Packages**a potom vyberte balíček pro nasazení, který chcete znovu distribuovat.  

    - **Balíčky ovladačů**: rozbalte **Operating Systems**  >  **balíčky ovladačů**operačních systémů a pak vyberte balíček ovladačů, který chcete znovu distribuovat.  

    - **Bitové kopie operačního systému**: **rozbalte**  >  možnost**bitové kopie operačního systému**a pak vyberte bitovou kopii operačního systému, kterou chcete znovu distribuovat.  

    - **Instalační programy operačního systému**: rozbalte položku **operační systémy**  >  **instalační programy operačního systému**a potom vyberte instalační program operačního systému, který chcete znovu distribuovat.  

    - **Spouštěcí bitové kopie**: rozbalte spouštěcí bitové kopie **operačních systémů**  >   **Boot Images**a pak vyberte spouštěcí bitovou kopii, kterou chcete znovu distribuovat.  

3.  Na kartě **Domů** ve skupině **Vlastnosti** klikněte na možnost **Vlastnosti**.  

4.  Klikněte na kartu **umístění obsahu** , vyberte distribuční bod nebo skupinu distribučních bodů, ve kterých chcete znovu distribuovat obsah, klikněte na položku znovu **distribuovat**a poté klikněte na tlačítko **OK**.  

#### <a name="to-redistribute-content-from-distribution-point-properties"></a>Opětovná distribuce obsahu z vlastností distribučního bodu  

1.  V konzole Configuration Manager klikněte na možnost **Správa**.  

2.  V pracovním prostoru **Správa** klikněte na možnost **distribuční body**a poté vyberte distribuční bod, ve kterém chcete znovu distribuovat obsah.  

3.  Na kartě **Domů** ve skupině **Vlastnosti** klikněte na možnost **Vlastnosti**.  

4.  Klikněte na kartu **obsah** , vyberte obsah, který chcete znovu distribuovat, klikněte na položku znovu **distribuovat**a poté klikněte na tlačítko **OK**.  

#### <a name="to-redistribute-content-from-distribution-point-group-properties"></a>Opětovná distribuce obsahu z vlastností skupiny distribučních bodů  

1.  V konzole Configuration Manager klikněte na možnost **Správa**.  

2.  V pracovním prostoru **Správa** klikněte na možnost **skupiny distribučních bodů**a pak vyberte skupinu distribučních bodů, ve které chcete znovu distribuovat obsah.  

3.  Na kartě **Domů** ve skupině **Vlastnosti** klikněte na možnost **Vlastnosti**.  

4.  Klikněte na kartu **obsah** , vyberte obsah, který chcete znovu distribuovat, klikněte na položku znovu **distribuovat**a poté klikněte na tlačítko **OK**.  

    > [!IMPORTANT]  
    > Obsah v balíčku je znovu distribuován do všech distribučních bodů ve skupině distribučních bodů.  


#### <a name="use-the-sdk-to-force-replication-of-content"></a>Vynutit replikaci obsahu pomocí sady SDK
Pomocí metody třídy **RetryContentReplication** rozhraní WMI (Windows Management Instrumentation) (WMI) z SDK Configuration Manager můžete vynutit, aby správce distribuce mohl kopírovat obsah ze zdrojového umístění do knihovny obsahu.  

Tuto metodu použijte pouze k vynucení replikace, pokud je nutné znovu distribuovat obsah po problémech s normální replikací obsahu (obvykle potvrzené použitím uzlu monitorování konzoly).   

Další informace o této možnosti sady SDK naleznete v tématu [Metoda RetryContentReplication ve třídě SMS_CM_UpdatePackages](../../../../develop/reference/sum/retrycontentreplication-method-in-class-sms_cm_updatepackages.md).

### <a name="remove-content"></a>Odebrat obsah
Pokud již nepotřebujete obsah v distribučních bodech, můžete odebrat soubory obsahu v distribučním bodě.  

- Vlastnosti balíčku  
- Vlastnosti distribučního bodu  
- Vlastnosti skupiny distribučních bodů.  

Pokud je však obsah přidružen k jinému balíčku, který byl distribuován do stejného distribučního bodu, nelze obsah odebrat.  

#### <a name="to-remove-package-content-files-from-distribution-points"></a>Odebrání souborů obsahu balíčku z distribučních bodů  

1.  V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  

2.  V pracovním prostoru **softwarová knihovna** vyberte jeden z následujících kroků pro typ obsahu, který chcete odstranit:  

    - **Aplikace**: rozbalte položku aplikace **pro správu aplikací**  >  **Applications**a potom vyberte aplikaci, kterou chcete odebrat.  

    - **Balíčky**: rozbalte položku balíčky **pro správu aplikací**  >  **Packages**a pak vyberte balíček, který chcete odebrat.  

    - **Balíčky pro nasazení**: rozbalte balíčky pro nasazení **aktualizací softwaru**  >  **Deployment Packages**a potom vyberte balíček pro nasazení, který chcete odebrat.  

    - **Balíčky ovladačů**: rozbalte **Operating Systems**  >  **balíčky ovladačů**operačních systémů a pak vyberte balíček ovladačů, který chcete odebrat.  

    - **Bitové kopie operačního systému**: **rozbalte**  >  **bitové kopie operačního systému**a pak vyberte bitovou kopii operačního systému, kterou chcete odebrat.  

    - **Instalační programy operačního systému**: rozbalte položku **operační systémy**  >  **instalační programy operačního systému**a pak vyberte instalační program operačního systému, který chcete odebrat.  

    - **Spouštěcí bitové kopie**: rozbalte spouštěcí bitové kopie **operačních systémů**  >  **Boot Images**a pak vyberte spouštěcí bitovou kopii, kterou chcete odebrat.  

3.  Na kartě **Domů** ve skupině **Vlastnosti** klikněte na možnost **Vlastnosti**.  

4.  Klikněte na kartu **umístění obsahu** , vyberte distribuční bod nebo skupinu distribučních bodů, ze kterých chcete odebrat obsah, klikněte na tlačítko **Odebrat**a poté klikněte na tlačítko **OK**.  

#### <a name="to-remove-package-content-from-distribution-point-properties"></a>Odebrání obsahu balíčku z vlastností distribučního bodu  

1.  V konzole Configuration Manager klikněte na možnost **Správa**.  

2.  V pracovním prostoru **Správa** klikněte na možnost **distribuční body**a poté vyberte distribuční bod, ve kterém chcete odstranit obsah.  

3.  Na kartě **Domů** ve skupině **Vlastnosti** klikněte na možnost **Vlastnosti**.  

4.  Klikněte na kartu **obsah** , vyberte obsah, který chcete odebrat, klikněte na tlačítko **Odebrat**a pak klikněte na tlačítko **OK**.  

#### <a name="to-remove-content-from-distribution-point-group-properties"></a>Odebrání obsahu z vlastností skupiny distribučních bodů  

1.  V konzole Configuration Manager klikněte na možnost **Správa**.  

2.  V pracovním prostoru **Správa** klikněte na možnost **skupiny distribučních bodů**a pak vyberte skupinu distribučních bodů, ve které chcete odebrat obsah.  

3.  Na kartě **Domů** ve skupině **Vlastnosti** klikněte na možnost **Vlastnosti**.  

4.  Klikněte na kartu **obsah** , vyberte obsah, který chcete odebrat, klikněte na tlačítko **Odebrat**a pak klikněte na tlačítko **OK**.  


### <a name="validate-content"></a>Ověřit obsah
Proces ověřování obsahu ověřuje integritu souborů obsahu v distribučních bodech. Povolíte ověření obsahu podle plánu nebo můžete ručně zahájit ověřování obsahu z vlastností distribučních bodů a balíčků.  

Při spuštění procesu ověřování obsahu Configuration Manager ověří soubory obsahu v distribučních bodech, a pokud je hodnota hash souboru pro soubory v distribučním bodě neočekávaná, Configuration Manager vytvoří stavovou zprávu, kterou můžete zkontrolovat v pracovním prostoru **monitorování** .  

Další informace o konfiguraci plánu ověřování obsahu najdete v tématu [Konfigurace distribučních bodů](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs) v tématu [instalace a konfigurace distribučních bodů pro Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) .  


#### <a name="to-initiate-content-validation-for-all-content-on-a-distribution-point"></a>Zahájení ověřování obsahu pro veškerý obsah v distribučním bodě  

1.  V konzole Configuration Manager klikněte na možnost **Správa**.  

2.  V pracovním prostoru **Správa** klikněte na možnost **distribuční body**a poté vyberte distribuční bod, ve kterém chcete ověřit obsah.  

3.  Na kartě **Domů** ve skupině **Vlastnosti** klikněte na možnost **Vlastnosti**.  

4.  Na kartě **obsah** vyberte balíček, ve kterém chcete ověřit obsah, klikněte na tlačítko **ověřit**, klikněte na tlačítko **OK**a potom klikněte na tlačítko **OK**. Proces ověření obsahu inicializuje balíček v distribučním bodě.  

5.  Chcete-li zobrazit výsledky procesu ověřování obsahu, rozbalte v pracovním prostoru **monitorování** možnost **stav distribuce**a klikněte na uzel **stav obsahu** . Zobrazí se obsah pro každý typ balíčku (například aplikace, balíček aktualizace softwaru a spouštěcí bitová kopie). Další informace o monitorování stavu obsahu najdete v tématu [monitorování obsahu distribuovaného pomocí Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

#### <a name="to-initiate-content-validation-for-a-package"></a>Zahájení ověřování obsahu pro balíček  

1.  V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  

2.  V pracovním prostoru **softwarová knihovna** vyberte jeden z následujících kroků pro typ obsahu, který chcete ověřit:  

    - **Aplikace**: rozbalte položku aplikace **pro správu aplikací**  >  **Applications**a potom vyberte aplikaci, kterou chcete ověřit.  

    - **Balíčky**: rozbalte položku balíčky **pro správu aplikací**  >  **Packages**a pak vyberte balíček, který chcete ověřit.  

    - **Balíčky pro nasazení**: rozbalte balíčky pro nasazení **aktualizací softwaru**  >  **Deployment Packages**a potom vyberte balíček pro nasazení, který chcete ověřit.  

    - **Balíčky ovladačů**: rozbalte **Operating Systems**  >  **balíčky ovladačů**operačních systémů a pak vyberte balíček ovladačů, který chcete ověřit.  

    - **Bitové kopie operačního systému**: **rozbalte**  >  **bitové kopie operačního systému**a pak vyberte bitovou kopii operačního systému, kterou chcete ověřit.  

    - **Instalační programy operačního systému**: rozbalte položku **operační systémy**  >   **instalační programy operačního systému**a potom vyberte instalační program operačního systému, který chcete ověřit.  

    - **Spouštěcí bitové kopie**: rozbalte spouštěcí bitové kopie **operačních systémů**  >  **Boot Images**a pak vyberte spouštěcí bitovou kopii, kterou chcete připravit.  

3.  Na kartě **Domů** ve skupině **Vlastnosti** klikněte na možnost **Vlastnosti**.  

4.  Na kartě **umístění obsahu** vyberte distribuční bod nebo skupinu distribučních bodů, ve kterých chcete ověřit obsah, klikněte na tlačítko **ověřit**, klikněte na tlačítko **OK**a potom klikněte na tlačítko **OK**. Proces ověřování obsahu spustí obsah ve vybraném distribučním bodě nebo skupině distribučních bodů.  

5.  Chcete-li zobrazit výsledky procesu ověřování obsahu, rozbalte v pracovním prostoru **monitorování** možnost **stav distribuce**a klikněte na uzel **stav obsahu** . Zobrazí se obsah pro každý typ balíčku (například aplikace, balíček aktualizace softwaru a spouštěcí bitová kopie). Další informace o sledování stavu obsahu najdete v tématu [monitorování obsahu distribuovaného pomocí Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  
