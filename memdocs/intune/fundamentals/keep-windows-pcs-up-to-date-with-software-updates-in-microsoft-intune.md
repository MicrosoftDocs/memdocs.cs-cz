---
title: Aktualizace softwaru pro počítače s Windows
titleSuffix: Microsoft Intune
description: Intune pomáhá udržovat spravované počítače aktuální díky zajištění rychlé instalace nejnovějších oprav a aktualizací softwaru.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/01/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid: 48e9c41a-d2de-424e-9610-cfd1ad514210
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9a1a5b291135f5c6d42a47377d14d6d3d4f13411
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332475"
---
# <a name="keep-windows-pcs-up-to-date-with-software-updates-in-microsoft-intune"></a>Udržování počítačů s Windows v aktuálním stavu díky softwarovým aktualizacím v Microsoft Intune

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

> [!NOTE]
> Informace v tomto tématu se vztahují jenom na desktopové systémy Windows, které spravujete jako počítače pomocí softwarového klienta Intune. Pokud chcete spravovat aktualizace pro počítače s Windows zaregistrované jako mobilní zařízení, přečtěte si téma [Správa aktualizací softwaru v Intune](../protect/windows-update-for-business-configure.md).

Microsoft Intune vám může pomoct zabezpečit spravované počítače mnoha způsoby, včetně správy softwarových aktualizací, které udržují počítače v aktuálním stavu, protože zajišťují, že se rychle nainstalují nejnovější opravy a aktualizace.

Pokud jste ještě na svých počítačích nenainstalovali klienta Intune, přečtěte si téma [Instalace klienta na počítači s Windows pomocí Microsoft Intune](install-the-windows-pc-client-with-microsoft-intune.md).

Jakmile jsou nové aktualizace dostupné na webu Microsoft Update nebo jste vytvořili aktualizaci jiného výrobce a tyto aktualizace se dají použít pro spravované počítače, na stránce **Přehled** pracovního prostoru **Aktualizace** se zobrazí oznámení. Po kliknutí na odkaz v tomto oznámení potom můžete provádět různé operace, třeba zobrazit další informace o aktualizaci, přijmout nebo nepřijmout aktualizaci a zobrazit počítače, na které se tato aktualizace bude po schválení instalovat.

> [!IMPORTANT]
> Pracovní prostor **Aktualizace** se v konzole pro správu nezobrazí, dokud nenainstalujete klienta aspoň na jeden počítač, který budete úspěšně spravovat.

Když aktualizace schválíte a nainstalujete, můžete v pracovním prostoru **Aktualizace** konzoly Intune zkontrolovat, jestli byla instalace úspěšná, nebo neúspěšná.

V dalších částech se dozvíte, jak udržovat software na spravovaných počítačích v aktuálním stavu.

## <a name="before-you-start"></a>Než začnete
Než začnete vytvářet a schvalovat aktualizace softwaru, nakonfigurujte a nasaďte zásady na svých počítačích, které určují, kdy a jak se budou aktualizace instalovat.

### <a name="to-configure-update-policy-settings"></a>Konfigurace nastavení zásad aktualizací

1. V [konzole pro správu Microsoft Intune](https://manage.microsoft.com/)vyberte **zásady** &gt; **Přehled** &gt; **Přidat zásadu**.

2. Nakonfigurujte a nasaďte zásady **nastavení agenta Microsoft Intune** pro nastavení aktualizací. Můžete použít doporučená nastavení nebo nastavení upravit. Pokud potřebujete více informací o postupu při vytváření a nasazování zásad, projděte si článek [Běžné úlohy správy počítačů s Windows pomocí počítačového klienta Microsoft Intune](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md).

Následující tabulka zobrazuje hodnoty, které můžete v zásadách konfigurovat, a taky Doporučené hodnoty, které se použijí, pokud zásady neupravíte. Tahle nastavení najdete v části **Aktualizace**.

  |Nastavení zásad|Podrobnosti|
    |------------------|--------------------|
    |**Četnost detekce aktualizací a aplikací (hodiny)** |Určuje, jak často (od 8 do 22 hodin) Intune kontroluje nové aktualizace a aplikace.<br /><br />Doporučená hodnota: **8** hodin.|
    |**Automatizovaná instalace aktualizací a aplikací nebo instalace aktualizací a aplikací s výzvami** |Určuje, jestli se mají aktualizace instalovat automaticky nebo jestli se má před instalací uživateli zobrazit výzva. Kromě toho vám tohle nastavení umožňuje naplánovat instalaci aktualizací a aplikací.<br /><br />**Instalace aktualizací a aplikací automaticky podle plánu** umožňuje instalovat aktualizace a aplikace pomocí určeného plánu.<br /><br />**Používat automatickou údržbu pro počítače se systémem Windows**  jako závislé nastavení zásad určuje, jestli se mají aktualizace a aplikace instalovat při zobrazení okna automatické údržby Windows.<br /><br />**Zobrazit uživateli výzvu k instalaci** vyzývá uživatele k instalaci aktualizací, jakmile jsou připravené.<br /><br />Doporučené hodnoty:<br /><br />Vybraná možnost **Instalovat aktualizace a aplikace automaticky podle plánu**<br /><br />**Naplánovaný den: Každý den**<br /><br />**Naplánovaný čas: 3:00**<br /><br />Vybraná možnost **Používat automatickou údržbu pro počítače se systémem Windows**|
    |**Umožnit okamžitou instalaci aktualizací, které nenaruší běh systému Windows** |Možnost **Povolit** umožňuje instalovat aktualizace hned po stažení s výjimkou aktualizací, které by přerušily nebo restartovaly Windows. Tyto aktualizace se instalují v závislosti na konfiguraci nastavení **Automatizovaná instalace aktualizací nebo instalace aktualizací s výzvami**.<br /><br />Možnost **Nepovolit** umožňuje instalovat aktualizace v závislosti na konfiguraci **Automatizovaná instalace aktualizací a aplikací nebo instalace aktualizací a aplikací s výzvami**.<br /><br />Doporučená hodnota: **Povolit** |
    |**Zpoždění restartu systému Windows po instalaci plánovaných aktualizací a aplikací (minuty)** |Určuje (1 až 30 minut) dobu čekání na restartování Windows po instalaci naplánovaných aktualizací a aplikací.<br /><br />Doporučená hodnota: **15 minut** |
    |**Zpoždění po restartu systému Windows při zahájení instalace dosud neprovedených plánovaných aktualizací nebo aplikací (minuty)** |Určuje (1 až 60 minut), jak dlouho se má čekat na spuštění instalace aktualizací a aplikací po restartování Windows, pokud nebyla nainstalovaná plánovaná aktualizace.<br /><br />Doporučená hodnota: **5 minut**|
    |**Povolit přihlášenému uživateli řídit restart systému Windows po instalaci plánovaných aktualizací a aplikací** |Určuje, jestli může přihlášený uživatel zpozdit restartování Windows (pokud je nastavené **Ano**), nebo jestli se má zobrazit upozornění na automatické restartování Windows (pokud se nastaví **Ne**). Pokud není po dokončení naplánované instalaci aktualizací a aplikací přihlášený žádný uživatel, Windows se v případě potřeby restartuje automaticky. Pokud nastavíte **Ne**, nastaví se ve výchozím nastavení doba před restartování Windows na 5 minut.<br /><br />Doporučená hodnota: **Ano**|
    |**Vyzvat uživatele k restartování Windows při povinných aktualizacích klientského agenta Microsoft Intune** |Určuje, jestli se má přihlášenému uživateli zobrazit výzva k restartování Windows, pokud povinná aktualizace klienta Intune vyžaduje restartování Windows.<br /><br />Doporučená hodnota: **Ano**|
    |**Plán instalace povinných aktualizací klientského agenta Microsoft Intune** |Umožňuje vytvořit plán při instalaci aktualizací klienta.<br /><br />Doporučená hodnota: nenakonfigurováno|
    |**Zpoždění mezi výzvami k restartu systému Windows po instalaci plánovaných aktualizací a aplikací (minuty)** |Určuje, jak často (1 až 1440 v minut) bude uživatel vyzván k restartování Windows při instalaci plánované aktualizace nebo aplikace, která vyžaduje restartování Windows, a uživatel zpozdí restartování.<br /><br />Doporučená hodnota: **30 minut** |

## <a name="update-software-made-by-microsoft"></a>Aktualizace softwaru od Microsoftu
Aktualizace softwaru Microsoftu nevyžaduje ze strany uživatele příliš mnoho zásahů. Než ale začnete, měli byste nakonfigurovat tahle dvě nastavení:

- **Kategorie produktů a klasifikace aktualizací** – definuje kategorie a klasifikace aktualizací, které mají být dostupné pro počítače. Můžete se třeba rozhodnout, že chcete instalovat jen důležité aktualizace Microsoft Office.

- **Pravidla pro automatické schválení** – tahle pravidla umožňují automaticky schválit určené typy aktualizace a snížit vaše režijní náklady na správu. Může se třeba stát, že budete chtít automaticky schvalovat všechny důležité aktualizace softwaru.

Použijte tyto dva postupy, které vám pomůžou s používáním aktualizací softwaru:

### <a name="configure-the-product-categories-and-update-classifications-you-want-to-make-available-to-managed-computers"></a>Konfigurace kategorií produktů a klasifikace aktualizací, které chcete zpřístupnit pro spravované počítače

1. V [konzole pro správu Microsoft Intune](https://manage.microsoft.com/)vyberte **správce** &gt; **aktualizace**.

2. Na stránce **Nastavení služby: Aktualizace** vyberte v seznamu **Kategorie produktů** kategorie aktualizací, které mají být dostupné pro počítače. Ve výchozím nastavení jsou vybrané nejběžnější aktualizace.

    > [!IMPORTANT]
    > Aby počítače získávaly aktualizace schválené správcem, nesmí se nastavení zásady skupiny služby Windows Server Update Services (WSUS) **Určení umístění intranetového serveru služby Microsoft Update** použít na počítače, které jsou zaregistrované v Intune.

3. V seznamu **Klasifikace aktualizací** vyberte třídy aktualizace, která má být dostupná pro spravované počítače. Ve výchozím nastavení jsou opět vybrané nejběžnější možnosti.

4. Požadovaný výběr uložíte kliknutím na **Uložit**.

### <a name="to-configure-automatic-approval-rules-for-software-updates"></a>Konfigurace pravidel automatického schvalování pro aktualizace softwaru

1. V [konzole pro správu Microsoft Intune](https://manage.microsoft.com/)vyberte **správce** &gt; **aktualizace**.

2. V části **Pravidla automatického schvalování** na stránce **Nastavení serveru: Aktualizace** zvolte **Nový**.

3. Na stránce **Obecné** v průvodci vytvořením pravidla automatického schvalování zadejte název a volitelný popis pravidla.

4. Na stránce **Kategorie produktů** vyberte všechny produkty, pro které chcete automaticky schvalovat aktualizace.

5. Na stránce **Klasifikace aktualizací** zadejte klasifikace aktualizací, které se mají automaticky schvalovat.

6. Na stránce **Nasazení** udělejte tohle:

    - Vyberte skupiny počítačů, ve kterých chcete nasadit nové pravidlo, a pak zvolte **Přidat**.

    - Pokud chcete určit termín instalace aktualizací, zaškrtněte políčko **Vynutit konečný termín instalace těchto aktualizací** a pak v seznamu **Konečný termín instalace** vyberte termín instalace.

        > [!NOTE]
        > Pokud zadáte termín instalace, je možné, že budete muset spravovaný počítač po uplynutí intervalu konečného termínu jednou nebo víckrát restartovat.

    - Po dokončení zvolte **Další**.

7. Na stránce **Souhrn** zkontrolujte nastavení pro nové pravidlo a pak zvolte **Dokončit**.

Nové pravidlo najdete v části **Pravidla automatického schvalování** stránky **Nastavení služby: Aktualizace**.

> [!NOTE]
> Vytvořené pravidlo automatického schvalování bude schvalovat jenom budoucí aktualizace, ale nebude automaticky schvalovat dřívější aktualizace, které už v Intune existují. Ke schválení těchto aktualizací musíte spustit pravidlo automatického schvalování.


### <a name="to-edit-run-or-delete-an-automatically-approved-update-rule"></a>Úpravy, spuštění nebo odstranění pravidla automaticky schválené aktualizace

1. V [konzole pro správu Microsoft Intune](https://manage.microsoft.com/)vyberte **správce** &gt; **aktualizace**.

2. V části **Pravidla automatického schvalování** vyberte pravidlo a pak udělejte jednu z těchhle věcí:

    - Chcete-li upravit pravidlo, zvolte možnost **Upravit**a poté změňte parametry pravidla v **Průvodci vytvořením pravidla pro schválení automatického aktualizace**.

    - Pokud chcete pravidlo spustit, zvolte **Spustit vybrané**.

    - Pokud chcete pravidlo odstranit, zvolte **Odstranit**.

        > [!NOTE]
        > Odstranění pravidla nemá vliv na předchozí aktualizace schválené odstraněným pravidlem.

## <a name="update-software-not-made-by-microsoft"></a>Aktualizace jiného softwaru než od Microsoftu
Můžete nasadit aktualizace pro software jiného výrobce než Microsoftu. K tomu můžete použít průvodce **nahráváním aktualizací** , který vám umožňuje nahrát aktualizace do úložiště v cloudu, a pak aktualizaci schválit nebo odmítnout podobně jako u softwaru Microsoftu.

### <a name="to-upload-and-configure-a-third-party-update"></a>Nahrání a konfigurace aktualizace jiného výrobce

1. V [konzole pro správu Microsoft Intune](https://manage.microsoft.com/)vyberte **aktualizace** &gt; **Přehled** &gt; **nahrát**.

2. Na stránce **Soubory aktualizace** vyberte **Procházet** a zvolte instalační soubory potřebné k instalaci balíčku aktualizace. Tímto souborem může být soubor instalační služby Windows (.msi), soubor opravy instalační služby Windows (.msp) nebo soubor programu .exe. Dále můžete přidat libovolné soubory a složky, které jsou ve stejné složce jako instalační soubor.

    Zobrazí se celková velikost vybraných souborů, které chcete nahrát. Tato velikost nezahrnuje velikost nekomprimovaných nebo rozbalených instalačních souborů.

3. Po zadání instalačních souborů se na stránce **Popis aktualizace** zobrazí název, popis a klasifikace informací o softwaru, které služba Intune extrahovala z instalačních souborů softwaru. Můžete vybrat klasifikaci pro označení typu nasazované aktualizace (aktualizace, důležité aktualizace, aktualizace zabezpečení, kumulativní aktualizace nebo aktualizace Service Pack). Až budete hotoví, vyberte **Další**.

4. Na stránce **Požadavky** v průvodci zvolte architekturu (32bitovou verzi, 64bitovou verzi nebo obě) a operační systémy spravovaných počítačů, na které se tato aktualizace použije.

5. Na stránce **Pravidla detekce** nastavte, jak má Intune zjistit, jestli je už aktualizace na spravovaných počítačích dostupná. Pokud použijete výchozí možnost **Použít výchozí pravidla zjišťování**, Intune vždycky nainstaluje balíček aktualizace na každý cílový počítač jednou.

    > [!NOTE]
    > Pokud je zadaným instalačním souborem aktualizace soubor instalační služby Windows nebo soubor .msp, stránka **Pravidla detekce** v průvodci se nezobrazí. Je to proto, že soubory instalační služby Windows a soubory .msp obsahují vlastní pokyny pro zjišťování předchozích instalací aktualizace.

    Výběrem jednoho nebo více pravidel určíte, jestli je aktualizace už nainstalovaná na spravovaných počítačích:

    - **Soubor existuje**.

    - **Kód produktu MSI existuje**.

    - **Klíč registru existuje**.

6. Zadejte veškeré další informace, které jsou třeba ke konfiguraci pravidla zjišťování, například cestu k souboru a jeho název, kód produktu instalační služby Windows nebo klíč registru, a potom zvolte **Další**.

7. Na stránce **Požadavky** v průvodci určete software, který už musí být nainstalovaný před instalací této aktualizace. Můžete zadat **Žádný**a vybrat softwarový balíček, který jste už přidali do služby Intune, která ho spravuje, nebo můžete nastavit některé z těchto pravidel pro popis softwaru:

    - **Soubor existuje**.

    - **Kód produktu MSI existuje**.

    - **Klíč registru existuje**.

8. Zadejte veškeré další informace, které jsou třeba ke konfiguraci pravidla zjišťování, například cestu k souboru a jeho název, kód produktu instalační služby Windows nebo klíč registru, a potom zvolte **Další**.

9. Na stránce **Argumenty příkazového řádku** v průvodci můžete přidáním požadovaných vlastností instalace na příkazový řádek instalace upravit chování instalačního souboru. Některý software třeba podporuje vlastnost **/q**, která umožňuje tichou instalaci. Informace o všech podporovaných argumentech příkazového řádku najdete v dokumentaci k vašemu softwarovému balíčku. Zadejte všechny potřebné argumenty příkazového řádku a pak zvolte **Další**.

    > [!NOTE]
    > Pokud aktualizace nepodporuje tichou instalaci, nemůžete ji pomocí Intune instalovat.

10. Na stránce **Návratové kódy** v průvodci můžete určit, jak se interpretují návratové kódy z instalace aktualizací. Ve výchozím nastavení Intune používá návratové kódy podle oborových standardů k oznámení neúspěšné nebo úspěšné instalace balíčku aktualizace. Zadané návratové kódy:

|Návratový kód|Podrobnosti|
|---------------|------------------|
|**0**|Úspěch|
|**3010**|Restartování proběhlo úspěšně|

11. Všechny neuvedené návratové kódy se považují za chybu.
Některé aktualizace používají pro návratové kódy nestandardní interpretace. V takovém případě můžete zadat své vlastní interpretace návratových kódů.

12. Zadejte nebo upravte požadované návratové kódy a pak zvolte **Další**.

13. Na stránce **Souhrn** v průvodci zkontrolujte akce, které se mají provést, a potom výběrem položky **Nahrát** kroky průvodce dokončete.

Nahraná aktualizace se uloží do vašeho cloudového úložiště Intune. Pokud máte dost volného místa pro nahrání balíčku aktualizace, budete na to během procesu nahrávání upozorněni. Intune může zjistit, jestli máte dost volného místa, až po zahájení nahrávání aktualizace, protože komprimované instalační soubory vyžadují po dekomprimaci víc místa.

Jakmile se aktualizace jiného výrobce nahraje do Intune, zobrazí se v pracovním prostoru **Aktualizace** v podokně **Všechny aktualizace**. Pak budete moct aktualizaci schválit a nasadit. Další informace najdete v následující části „Schválení a zamítnutí aktualizací“.

## <a name="approve-and-decline-updates"></a>Schválení a zamítnutí aktualizací
Jakmile jsou aktualizace připravené k instalaci, zobrazí se o tom zpráva na stránce **Přehled aktualizací** pracovního prostoru **Aktualizace** v části **Stav aktualizace**. Výběrem této zprávy otevřete stránku **Všechny aktualizace** , na které uvidíte, jaké aktualizace jsou připravené ke schválení.

Abyste usnadnili hledání aktualizací, můžete použít seznam **Filtry**. Můžete třeba zobrazit jen aktualizace, které se nepodařilo nainstalovat nebo které byly nahrazené.

Po výběru aktualizace ze seznamu budete moct použít další příkazy, které umožňují spravovat aktualizace a které jsou uvedené v této tabulce:

|Úloha|Podrobnosti|
|--------|--------------------|
|**Zobrazit vlastnosti**|Zobrazí podrobné informace o aktualizaci včetně počtu počítačů, na které se vztahuje.|
|**Upravit**|Používá se jen pro aktualizace jiného výrobce než Microsoftu. Umožňuje upravit vlastnosti aktualizace.|
|**Schválit**|Schválí vybranou aktualizaci a umožní vám nakonfigurovat, do jakých skupin se nasadí. Další informace najdete v postupu **Schválení aktualizací** v tomto tématu.|
|**Odmítnout**|Odebere všechna předchozí schválení aktualizace a skryje aktualizaci z výchozích zobrazení. Kromě toho se odeberou všechna data sestavy pro tuto aktualizaci.<br /><br />Pokud chcete později hledat odmítnuté aktualizace, nastavte filtr na stránce **Všechny aktualizace** na **Odmítnuto**. Tuto aktualizaci pak můžete podle potřeby schválit.<br /><br />Pokud došlo k odmítnutí aktualizace z důvodu vypršení její platnosti ve službě Microsoft Update, nebude možné ji schválit v konzole pro správu Intune.<br /><br />Když odstraníte zásady aktualizací nasazené na počítače, hodnoty nastavení zásad těchto aktualizací se vrátí do výchozího stavu pro operační systém nainstalovaný na počítačích.|
|**Odstranit**|Používá se jen pro aktualizace jiného výrobce než Microsoftu. Odstraní vybranou aktualizaci.|
|**Odeslat**|Spustí průvodce **Nahrát aktualizaci**, který vám umožní nahrát aktualizace jiného výrobce než Microsoftu, které chcete nasadit.|

### <a name="to-approve-updates"></a>Schválení aktualizací

1. V [konzole pro správu Microsoft Intune](https://manage.microsoft.com/)vyberte **aktualizace** &gt; **Přehled** &gt; **nové aktualizace ke schválení**.

    V pracovním prostoru **aktualizace** vyberte **Přehled** &gt; **nové aktualizace ke schválení**.

    > [!NOTE]
    > Odkaz **Nové aktualizace ke schválení** se zobrazí v oblasti **Stav aktualizací** , jen když máte aspoň jeden spravovaný počítač, který vyžaduje schválení aktualizace.

2. Vyberte aktualizaci, kterou chcete schválit, v dolní části stránky se podívejte na její vlastnosti, a potom vyberte možnost **Schválit**. Můžete vybrat víc aktualizací tím, že při výběru jednotlivých položek podržíte stisknutou klávesu **CTRL**.

3. Na stránce **Vybrat skupiny** vyberte skupinu, do které chcete nasadit aktualizace, a vyberte možnost **Přidat**. Až budete s určováním skupin hotoví, zvolte **Další**.

4. Na stránce **Akce nasazení** udělejte pro každou skupinu v seznamu tohle:

    - V seznamu **Schválení** vyberte některou z těchto možností:

        - **Požadovaná instalace** – nainstaluje aktualizaci na počítače v určené skupině.

        - **Neinstalovat** – zobrazí jenom informace o použitelnosti a aktualizaci nenainstaluje.

        - **Dostupná instalace** – uživatel může nainstalovat aplikaci na vyžádání z firemního portálu.

        - **Odinstalovat** – odebere aktualizace z počítačů v cílové skupině.

            > [!IMPORTANT]
            > Aktualizace se odebere, i když ji nenainstalovala služba Intune.

    - V seznamu **Termín** vyberte některou z těchto možností:

        - **Žádný** – označuje, že pro instalaci aktualizace nebyl vynucený žádný termín a uživatelé můžou aktualizaci průběžně odmítat.

        - **Co nejdříve** – nainstaluje aktualizaci na cílové počítače při nejbližší příležitosti.

        - **Vlastní** – určuje datum a čas instalace schválených aktualizací.

        - **Jeden týden**, **Dva týdny**, **Jeden měsíc** – nainstaluje aktualizaci během zadaného časového období.

5. Výběrem možnosti **Dokončit** nastavení uložíte a výběrem možnosti **Zrušit** nastavení zrušíte a vrátíte se k seznamu aktualizací.

    > [!IMPORTANT]
    > Pokud jste pro podřízenou skupinu explicitně nenakonfigurovali akci **Neinstalovat**, **Požadovaná instalace**nebo **Odinstalovat** , zdědí všechny podřízené skupiny akci nakonfigurovanou pro nadřazenou skupinu.

6. Na panelu podrobností v dolní části stránky **Všechny aktualizace** můžete vidět zprávy s připomenutím ohledně aktualizací.


## <a name="see-also"></a>Viz také
[Zásady ochrany počítačů se systémem Windows](policies-to-protect-windows-pcs-in-microsoft-intune.md)
