---
title: Nasazení Windows to – přejít
titleSuffix: Configuration Manager
description: Naučte se, jak zřídit Windows to in v Configuration Manager k vytvoření pracovního prostoru Windows to přejít, který se spouští z externího disku.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 8eed50f5-80a4-422e-8aa6-a7ccb2171475
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3cf735dfa2dd73ed39a24c2d674a966acddf05a
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125113"
---
# <a name="deploy-windows-to-go-with-configuration-manager"></a>Nasazení Windows to-přejít pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

V tomto tématu najdete postup, jak zajistit, aby Windows to přešel do Configuration Manager. Windows To Go je funkce Enterprise systému Windows 8, která umožňuje vytvořit pracovní prostor Windows To Go, který lze spustit z externího disku připojeného přes USB v počítačích splňujících požadavky systémů Windows 7 nebo Windows 8 na certifikaci, a to bez ohledu na to, jaký operační systém je v počítači používán. Pracovní prostory Windows To Go mohou využívat stejnou bitovou kopii, kterou podniky využívají pro své stolní počítače a notebooky, a lze je spravovat stejným způsobem.  

 Další informace o funkci Windows to přejít najdete v tématu [Přehled funkcí Windows to přejít](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh831833(v=ws.11)).  

## <a name="provision-windows-to-go"></a>Zřízení funkce Windows To Go  
 Windows To Go je operační systém uložený na externím disku připojovaným přes USB. Zřízení disku Windows To Go je podobné jako zřízení ostatních nasazení operačního systému. Protože je však funkce Windows To Go navržena jako vysoce mobilní řešení pro konkrétního uživatele, postup při zřízení těchto disků se v některých ohledech liší.  

 Na nejvyšší úrovni je Windows To Go dvoufázové nasazení, umožňující nakonfigurovat zařízení Windows To Go a obsah připravený pro nasazení operačního systému. Můžete to dosáhnout s minimálním dopadem na uživatele a omezit prostoje pro počítač uživatele. Po předpřipravení počítače je třeba provést proces zřízení, a zajistit tak, že bude uživatel moci počítač používat. Proces zřízení je podobný procesu nasazení aktuálního operačního systému. Následující přehled uvádí obecný postup přípravy obsahu a zřízení funkce Windows To Go:  

1.  [Požadavky na zřízení Windows to – přejít](#BKMK_Prereqs)  

2.  [Vytvoření předzpracovaného média](#BKMK_CreatePrestagedMedia)  

3.  [Vytvoření balíčku Windows To Go Creator](#BKMK_CreatePackage)  

4.  [Aktualizace pořadí úkolů za účelem zapnutí nástroje BitLocker pro funkci Windows To Go](#BKMK_UpdateTaskSequence)  

5.  [Nasazení balíčku Windows to, Creator a pořadí úkolů](#BKMK_Deployments)  

6.  [Uživatel spustí program Windows to Směřuj Creator.](#BKMK_UserExperience)  

7.  [Configuration Manager konfigurace a fáze jednotky Windows to Drive](#BKMK_ConfigureStageDrive)  

8.  [Přihlášení uživatele k systému Windows 8](#BKMK_UserLogsIn)  

###  <a name="prerequisites-to-provision-windows-to-go"></a><a name="BKMK_Prereqs"></a> Požadavky na zřízení funkce Windows To Go  
 Než začnete se systémem Windows to přejít, je nutné provést následující kroky v Configuration Manager:  

-   **Distribuce spouštěcí image do distribučního bodu:**  

     Než vytvoříte předzpracované médium, je třeba distribuovat spouštěcí bitovou kopii do distribučního bodu.  

    > [!NOTE]  
    >  Spouštěcí bitové kopie slouží k instalaci operačního systému do cílových počítačů v prostředí Configuration Manager. Obsahují verzi systému PE, který nainstaluje operační systém a všechny požadované doplňkové ovladače zařízení. Configuration Manager poskytuje dvě spouštěcí image: jednu pro podporu platforem x86 a druhou pro podporu platforem x64. Vytvořit ale můžete také vlastní spouštěcí bitové kopie. Další informace najdete v tématu [Správa spouštěcích imagí](../get-started/manage-boot-images.md).  

-   **Distribuce image operačního systému Windows 8 do distribučního bodu**  

     Než vytvoříte předzpracované médium, je třeba distribuovat do distribučního bodu bitovou kopii operačního systému Windows 8.  

    > [!NOTE]  
    >  Bitové kopie operačního systému jsou soubory ve formátu .WIM, reprezentující zkomprimovanou kolekci referenčních souborů a složek, které jsou vyžadovány k úspěšné instalaci a konfiguraci operačního systému v počítači. Další informace najdete v tématu [Správa imagí operačního systému](../get-started/manage-operating-system-images.md).  

-   **Vytvoření pořadí úloh k nasazení systému Windows 8**  

     Při vytváření předzpracovaného média je třeba vytvořit pořadí úloh pro nasazení systému Windows 8, na něž budete odkazovat. Další informace najdete v tématu [Správa pořadí úkolů pro automatizaci úloh](manage-task-sequences-to-automate-tasks.md).  

###  <a name="create-prestaged-media"></a><a name="BKMK_CreatePrestagedMedia"></a>Vytvoření předzpracovaného média  
 Předzpracované médium obsahuje spouštěcí bitovou kopii sloužící ke spuštění cílového počítače a bitové kopie operačního systému, který bude v cílovém počítači nasazen. Počítač lze spustit pomocí spouštěcí bitové kopie na předzpracovaném médiu. Počítač pak může spustit existující pořadí úloh k nasazení operačního systému a nainstalovat kompletní nasazení operačního systému. Pořadí úloh, které operační systém nasadí, není obsaženo na médiu.  

 Ve fázi přípravy obsahu můžete přidat k imagi a spouštěcí imagi operačního systému další obsah, jako např. aplikace nebo ovladače zařízení. Tím se snižuje čas potřebný k nasazení operačního systému, ale také objem síťového přenosu, protože obsah je již uložen na disku.  

 K vytvoření předzpracovaného média použijte následující postup.  

#### <a name="to-create-prestaged-media"></a>Vytvoření předzpracovaného média  

1. V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  

2. V pracovním prostoru **softwarová knihovna** rozbalte možnost **operační systémy**a klikněte na položku **pořadí úloh**.  

3. Na kartě **Domů** ve skupině **Vytvoření** kliknutím na možnost **Vytvoření médií sekvence úlohy** spusťte průvodce vytvořením médií sekvence úlohy.  

4. Na stránce **Výběr typu média** zadejte následující informace a klikněte na tlačítko **Další**.  

   -   Vyberte položku **Předzpracované médium**.  

   -   Chcete-li spustit nasazení funkcí Windows To Go bez interakce s uživatelem, zvolte možnost **Povolit bezobslužné nasazení operačního systému** .  

       > [!IMPORTANT]  
       >  Pokud použijete tuto možnost spolu s vlastní proměnnou SMSTSPreferredAdvertID (viz dále v tomto postupu), nebude vyžadována žádná interakce s uživatelem, a pokud počítač nalezne disk Windows To Go, automaticky spustí nasazení funkcí Windows To Go. Pokud je médium konfigurováno k ochraně heslem, bude uživatel pouze vyzván k zadání hesla. Pokud použijete nastavení **Povolit bezobslužné nasazení operačního systému** bez proměnné SMSTSPreferredAdvertID, dojde při nasazení pořadí úloh k chybě.  

5. Na stránce **Správa média** zadejte následující informace a klikněte na tlačítko **Další**.  

   -   Zvolte možnost **Dynamická média** , pokud chcete, aby řídicí místo přesměrovalo média do jiného řídicího místa v závislosti na umístění klienta v hranicích lokality.  

   -   Zvolte možnost **Média lokality** , pokud chcete, aby média byla ve spojení pouze s určeným řídicím místem.  

6. Na stránce **Vlastnosti média**  zadejte následující informace a klikněte na tlačítko **Další**.  

   -   **Vytvořil**: Zadejte, kdo médium vytvořil.  

   -   **Verze**: Zadejte číslo verze média.  

   -   **Komentář**: Zadejte unikátní popis, k čemu médium slouží.  

   -   **Mediální soubor**: Zadejte název výstupních souborů a cestu ke složce, ve které se uloží. Průvodce uloží výstupní soubory do tohoto umístění. Příklad: ** \\ \servername\folder\outputfile.wim**  

7. Na stránce **Zabezpečení** zadejte následující informace a klikněte na tlačítko **Další**.  

   -   Vyberte možnost **Povolit podporu neznámých počítačů** , aby médium mohlo nasadit operační systém do počítače, který není spravován nástrojem Configuration Manager. V databázi Configuration Manager není žádný záznam o těchto počítačích. Neznámé počítače zahrnují následující:  

       -   Počítač, na kterém není nainstalovaný klient Configuration Manager  

       -   Počítač, který není importován do Configuration Manager  

       -   Počítač, který není zjištěn nástrojem Configuration Manager  

   -   Chcete-li médium ochránit před neoprávněným přístupem, nastavte možnost **Chránit médium heslem** a zadejte silné heslo. Pokud zadáte heslo, musí uživatel k použití předzpracovaného média zadat toto heslo.  

       > [!IMPORTANT]  
       >  Ke zvýšení ochrany předzpracovaného média doporučujeme vždy nastavit heslo.  

       > [!NOTE]  
       >  Pokud je předzpracované médium chráněno heslem, bude uživatel vyzván k zadání hesla i v případě, že je pro médium nastavena možnost **Povolit bezobslužné nasazení operačního systému** .  

   -   Pro komunikace HTTP vyberte možnost **Vytvoření certifikátu médií podepsaného svým držitelem**a pak určete datum počátku a ukončení platnosti certifikátu.  

   -   Pro komunikace HTTPS vyberte možnost **Import certifikátu PKI**a pak určete certifikát, který chcete importovat a jeho heslo.  

        Další informace o tomto klientském certifikátu, který se používá pro spouštěcí image, najdete v tématu [požadavky na certifikát PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

   -   **Spřažení zařízení a uživatele**: pro podporu správy zaměřené na uživatele v Configuration Manager určete, jak chcete, aby média spojila uživatele s cílovým počítačem. Další informace o tom, jak nasazení operačního systému podporuje spřažení uživatelských zařízení, najdete v tématu [přidružení uživatelů k cílovému počítači](../get-started/associate-users-with-a-destination-computer.md).  

       -   Vyberte možnost **Povolení spřažení zařízení uživatele prostřednictvím automatického schválení** , pokud chcete, aby média automaticky spojovala uživatele s cílovým počítačem. Tato funkce je založena na akcích sekvence úlohy, která nasazuje operační systém. V tomto scénáři vytváří sekvence úlohy vzájemný vztah mezi určenými uživateli a cílovým počítačem při nasazování operačního systému do cílového počítače.  

       -   Vyberte možnost **Povolení spřažení zařízení uživatele čekající na schválení správcem** , pokud chcete, aby média spojila uživatele s cílovým počítačem po udělení schválení. Tato funkce je založena na rozsahu sekvence úlohy, která nasazuje operační systém. V tomto scénáři vytváří sekvence úlohy vzájemný vztah mezi určenými uživateli a cílovým počítačem, ale čeká na schválení administrátorem předtím, než je operační systém nasazen.  

       -   Vyberte možnost **Zákaz spřažení zařízení uživatele** , pokud nechcete, aby média spojila uživatele s cílovým počítačem. V tomto scénáři sekvence úlohy nespojí uživatele s cílovým počítačem při nasazení operačního systému.  

8. Na stránce **Pořadí úloh** zadejte pořadí úloh pro systém Windows 8, které jste vytvořili v předchozí části.  

9. Na stránce **Bootovací obrázek** určete následující data a pak klikněte na tlačítko **Další**.  

    > [!IMPORTANT]  
    >  Architektura distribuovaného bootovacího obrázku musí odpovídat architektuře cílového počítače. Například cílový počítač x64 může bootovat a spustit bootovací obrázek x86 nebo x64. Ale cílový počítač x86 může bootovat a spustit pouze bootovací obrázek x86. U certifikovaných počítačů se systémem Windows 8 v režimu EFI musí být použita spouštěcí bitová kopie x64.  

    -   **Spouštěcí bitová kopie**: Zadejte spouštěcí image, pomocí které se má spustit cílový počítač.  

    -   **Distribuční bod**: Zadejte distribuční bod, který je hostitelem spouštěcí image. Průvodce získá bootovací obrázek z distribučního místa a uloží jej do médií.  

        > [!NOTE]  
        >  Administrativní uživatel musí mít k obsahu spouštěcí bitové kopie v distribučním bodu oprávnění **Číst** . Další informace najdete v tématu [účet pro přístup k balíčku](../../core/plan-design/hierarchy/accounts.md#package-access-account).  

    -   Pokud jste na stránce **Správa média** v tomto průvodci zvolili možnost **Médium webového serveru** , v poli **Bod správy** zadejte bod správy z primární lokality.  

    -   Pokud jste na stránce **Správa média** v tomto průvodci zvolili možnost **Dynamické médium** , v poli **Přidružené body správy** zadejte body správy primární lokality, které mají být použity, a priority pro prvotní komunikaci.  

10. Na stránce **Bitové kopie** zadejte následující informace a klikněte na tlačítko **Další**.  

    -   **Balíček bitové kopie**: Zadejte balíček obsahující image operačního systému Windows 8.  

    -   **Index bitové kopie**: Zadejte, která image se má nasadit, když balíček obsahuje víc imagí operačního systému.  

    -   **Distribuční bod**: Zadejte distribuční bod, který je hostitelem balíčku image operačního systému. Průvodce získá bitovou kopii operačního systému z distribučního bodu a zapíše ji na médium.  

        > [!NOTE]  
        >  Administrativní uživatel musí mít k obsahu bitové kopie operačního systému v distribučním bodu oprávnění **Číst** . Další informace najdete v tématu [účet pro přístup k balíčku](../../core/plan-design/hierarchy/accounts.md#package-access-account).  

11. Na stránce **Vybrat aplikaci** zvolte aplikace, které chcete zahrnout do souboru média, a klikněte na tlačítko **Další**.  

12. Na stránce **Vyberte balíček** zvolte další balíčky, které chcete zahrnout do souboru média, a klikněte na tlačítko **Další**.  

13. Na stránce **Vybrat balíček ovladače** zvolte balíček ovladačů, který chcete zahrnout do souboru média, a klikněte na tlačítko **Další**.  

14. Na stránce **Distribuční body** vyberte jeden nebo více distribučních bodů, které obsahují obsah požadovaný pořadím úloh a klikněte na tlačítko **Další**.  

15. Na stránce **Vlastní nastavení** určete následující data a pak klikněte na tlačítko **Další**.  

    - **Proměnné**: Určete proměnné, které pořadí úkolů používá k nasazení operačního systému. Pokud chcete automaticky zvolit nasazení funkcí Windows To Go, použijte u funkce Windows To Go proměnnou SMSTSPreferredAdvertID ve tvaru:  

       SMSTSPreferredAdvertID = {*DeploymentID*}, kde DeploymentID je identifikátor ID nasazení přidružený k pořadí úloh, které bude použito v procesu zřízení pro disk Windows To Go.  

      > [!TIP]  
      >  Pokud použijete tuto proměnnou spolu s pořadím úloh nastaveným na bezobslužné nasazení (viz dříve v tomto postupu), nebude vyžadována žádná interakce s uživatelem, a pokud počítač nalezne disk Windows To Go, automaticky spustí nasazení funkcí Windows To Go. Pokud je médium konfigurováno k ochraně heslem, bude uživatel pouze vyzván k zadání hesla.  

    - **Příkazy před zahájením**: Určete veškeré příkazy, které chcete spustit předtím, než se spustí pořadí úkolů. Předstartovní příkazy mohou být skripty nebo spustitelné soubory, které mohou komunikovat s uživatelem v systému Windows PE před spuštěním pořadí úloh za účelem instalace operačního systému. K nasazení funkcí Windows To Go nastavte tyto možnosti:  

      - **OSDBitLockerPIN**: Nástroj BitLocker pro Windows To Go vyžaduje heslo. Chcete-li nastavit heslo nástroje BitLocker pro disk Windows To Go, nastavte jako součást předstartovního příkazu proměnnou **OSDBitLockerPIN** .  

        > [!WARNING]  
        >  Pokud je pro nástroj BitLocker povoleno přístupové heslo, uživatel bude muset zadat heslo vždy, když se počítač pokusí spustit disk Windows To Go.  

      - **SMSTSUDAUsers**: Udává primárního uživatele cílového počítače. Tuto proměnnou použijte v případě, že chcete shromažďovat jména uživatelů, která lze poté využít k přiřazení uživatele k zařízení. Další informace najdete v tématu [přidružení uživatelů k cílovému počítači](../get-started/associate-users-with-a-destination-computer.md).  

        > [!TIP]  
        >  Chcete-li získávat jména uživatelů, můžete jako součást předstartovního příkazu vytvořit vstupní pole, do nějž uživatel zadá své uživatelské jméno, a poté nastavit proměnnou s touto hodnotou. Do souboru skriptu předstartovního příkazu můžete vložit například následující řádky:  
        >   
        >  `UserID = inputbox("Enter Username" ,"Enter your username:","",400,0)`  
        >   
        >  `env("SMSTSUDAUsers") = UserID`  

        Další informace o tom, jak vytvořit soubor skriptu, který se použije jako Předstartovní příkaz, najdete v tématu [příkazy před zahájením pro médium pořadí úloh](../understand/prestart-commands-for-task-sequence-media.md).  

16. Dokončete průvodce.  

    > [!NOTE]  
    >  Vytvoření souboru předzpracovaného média průvodcem může chvíli trvat.  

###  <a name="create-a-windows-to-go-creator-package"></a><a name="BKMK_CreatePackage"></a>Vytvoření balíčku Windows to do programu Creator  
 Jako součást nasazení funkcí Windows To Go je třeba vytvořit balíček k nasazení souboru předzpracovaného média. Balíček musí obsahovat nástroj, jímž se konfiguruje disk Windows To Go a který rozbalí předzpracované médium na disk. K vytvoření balíčku Windows To Go Creator postupujte podle následujícího popisu.  

#### <a name="to-create-the-windows-to-go-creator-package"></a>Vytvoření balíčku Windows To Go Creator  

1. Na serveru, na němž mají být umístěny soubory balíčku Windows To Go Creator, vytvořte pro zdrojové soubory balíčku zdrojovou složku.  

   > [!NOTE]  
   >  Účet počítače serveru lokality musí mít ke zdrojové složce oprávnění **Číst** .  

2. Zkopírujte soubor předzpracovaného média, který jste vytvořili v části [Create prestaged media](#BKMK_CreatePrestagedMedia) , do zdrojové složky balíčku.  

3. Do zdrojové složky balíčku zkopírujte nástroj Windows To Go Creator (WTGCreator.exe). Nástroj Creator je k dispozici na všech serverech primární lokality v následujícím umístění: <*ConfigMgrInstallationFolder*> \OSD\Tools\WTG\Creator.  

4. Pomocí Průvodce vytvořením balíčku a programu vytvořte balíček a program.  

5. V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  

6. V pracovním prostoru **Softwarová knihovna** rozbalte možnost **Správa aplikací**a klikněte na položku **Balíčky**.  

7. Na kartě **Domů** ve skupině **Vytvořit** klikněte na možnost **Vytvořit balíček**.  

8. Na stránce **Balíček** zadejte název a popis balíčku. Například zadejte **Windows to přejít** pro název balíčku a zadejte **balíček pro konfiguraci jednotky Windows To přejděte pomocí Configuration Manager** pro popis balíčku.  

9. Zvolte možnost **Tento balíček obsahuje zdrojové soubory**, zadejte cestu ke zdrojové složce balíčku, který jste vytvořili v kroku 1, a klikněte na tlačítko **Další**.  

10. Na stránce **Typ programu** zvolte možnost **Standardní program**a klikněte na tlačítko **Další**.  

11. Na stránce **Standardní program** zadejte následující informace:  

    -   **Název**: Zadejte název programu. Jako název programu můžete zadat třeba **Creator** .  

    -   **Příkazový řádek**: Zadejte **WTGCreator.exe /wim:PrestageName.wim**, kde PrestageName je název předem připraveného souboru, který jste vytvořili a zkopírovali do zdrojové složky balíčku nástroje Windows To Go Creator.  

         Volitelně můžete nastavit tyto možnosti:  

        -   **enableBootRedirect**: možnost příkazového řádku, která povolí přesměrování při spuštění pomocí funkce Windows To Go. Pokud nastavíte tuto možnost, počítač spustí operační systém z disku USB bez nutnosti změny pořadí spouštění ve firmwaru počítače nebo nechá uživatele během spuštění počítače vybrat ze seznamu možností spouštění. Pokud je nalezen disk Windows To Go, počítač spustí operační systém z tohoto disku.  

    -   **Spustit**: Pokud chcete, aby se program spustil podle výchozího nastavení systému a programu, vyberte **Normální** .  

    -   **Program lze spustit**: Určete, jestli se program může spustit, jenom když je přihlášený uživatel.  

    -   **Režim spuštění**: Určete, jestli se program spustí s oprávněním přihlášeného uživatele nebo s oprávněním správce. Nástroj Windows To Go Creator vyžaduje ke spuštění zvýšenou úroveň oprávnění.  

    -   Nastavte možnost **Povolit uživatelům zobrazení a interakci s instalací programu**a klikněte na tlačítko **Další**.  

12. Na stránce Požadavky zadejte následující informace:  

    - **Požadavky na platformu**: Zvolte platformy Windows 8, ve kterých se má povolit zřizování.  

    - **Odhadované místo na disku**: Určete velikost zdrojové složky balíčku pro nástroj Windows To Go Creator.  

    - **Maximální povolená době běhu (v minutách)**: Určete maximální dobu, po kterou se očekává spuštění programu v klientském počítači. Ve výchozím nastavení je tato hodnota nastavena na 120 minut.  

      > [!IMPORTANT]  
      >  Pokud používáte časové intervaly pro správu a údržbu pro kolekce, ve které tento program běží, může vzniknout konflikt, pokud je **Maximální povolená doba běhu** delší než plánovaný časový interval pro správu a údržbu. Pokud je maximální doba běhu nastavena na možnost **Neznámá**, spustí se během časového intervalu pro správu a údržbu, ale bude pokračovat, dokud neskončí nebo neselže po zavření časového intervalu pro správu a údržbu. Pokud nastavíte maximální dobu běhu na určitou dobu (nikoli možnost Neznámá), která překračuje délku kteréhokoli dostupného časového intervalu pro správu a údržbu, daný program se nespustí.  

      > [!NOTE]  
      >  Pokud je hodnota nastavená na **Neznámý**, Configuration Manager nastaví maximální povolenou dobu běhu na 12 hodin (720 minut).  

      > [!NOTE]  
      >  Pokud je maximální doba běhu (nastavená uživatelem nebo jako výchozí hodnota) překročena, Configuration Manager zastaví program, pokud je vybrána možnost **Spustit s právy správce** a možnost **Zobrazit uživatelům zobrazení a interakci s instalací programu** není vybrána na stránce **standardní program** .  

      Klikněte na **Další** a dokončete průvodce.  

###  <a name="update-the-task-sequence-to-enable-bitlocker-for-windows-to-go"></a><a name="BKMK_UpdateTaskSequence"></a>Aktualizace pořadí úkolů za účelem zapnutí nástroje BitLocker pro systém Windows to přejít  
 Systém Windows To Go slouží k zapnutí nástroje BitLocker na externí spustitelné jednotce bez použití TPM. Proto je třeba ke konfiguraci nástroje BitLocker na jednotce se systémem Windows To Go použít samostatný nástroj. Chcete-li nástroj BitLocker zapnout, je třeba do pořadí úloh přidat akci za krok **Nastavit systém Windows a nástroj ConfigMgr** .  

> [!NOTE]  
>  Nástroj BitLocker pro systém Windows To Go vyžaduje heslo. V kroku [Create prestaged media](#BKMK_CreatePrestagedMedia) nastavte heslo jako součást předstartovního příkazu pomocí proměnné OSDBitLockerPIN.  

 Pomocí následujícího postupu aktualizuje pořadí úloh systému Windows 8, čímž zapnete nástroj BitLocker pro systém Windows To Go.  

#### <a name="to-update-the-windows-8-task-sequence-to-enable-bitlocker"></a>Aktualizace pořadí úloh systému Windows 8 za účelem zapnutí nástroje BitLocker  

1.  V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  

2.  V pracovním prostoru **Softwarová knihovna** rozbalte možnost **Správa aplikací**a klikněte na položku **Balíčky**.  

3.  Na kartě **Domů** ve skupině **Vytvořit** klikněte na možnost **Vytvořit balíček**.  

4.  Na stránce **Balíček** zadejte název a popis balíčku. Jako název balíčku zadejte třeba **BitLocker for Windows To Go** a jako jeho popis použijte **Package to update BitLocker for Windows To Go** .  

5.  Vyberte možnost **Tento balíček obsahuje zdrojové soubory**, zadejte umístění nástroje BitLocker pro systém Windows To Go a poté klikněte na tlačítko **Další**. Nástroj BitLocker je k dispozici na jakémkoli serveru Configuration Manager primární lokality v následujícím umístění: <*ConfigMgrInstallationFolder*> \OSD\Tools\WTG\BitLocker\  

6.  Na stránce **Typ programu** vyberte možnost **Nevytvářet program**.  

7.  Klikněte na **Další** a dokončete průvodce.  

8.  V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  

9. V pracovním prostoru **softwarová knihovna** rozbalte možnost **operační systémy**a klikněte na položku **pořadí úloh**.  

10. Vyberte pořadí úloh systému Windows 8, na kterou odkazujete v předzpracovaném médiu.  

11. Na kartě **Domů** ve skupině **Pořadí úloh** klikněte na možnost **Upravit**.  

12. Klikněte na krok **Nastavit systém Windows a nástroj ConfigMgr** , poté na možnost **Přidat**, **Obecné**a nakonec možnost **Spustit příkazový řádek**. Krok Spustit příkazový řádek bude přidán za krok Nastavit systém Windows a nástroj ConfigMgr.  

13. Na kartě **Vlastnosti** v kroku **Spustit příkazový řádek** přidejte následující informace:  

    1.  **Název**: Zadejte název pro příkazový řádek, třeba **Enable BitLocker for Windows To Go**.  

    2.  **Příkazový řádek**: i386\osdbitlocker_wtg.exe/Enable/pwd: < *none&#124;AD*>  

         Parametry:  

        -   /PWD: <None&#124;AD> – zadejte režim obnovení hesla nástroje BitLocker. Tento parametr je povinný při použití parametru /Enable na příkazovém řádku.  

             Vyberte možnost **AD**, chcete-li konfigurovat šifrování jednotky nástroje BitLocker pro zálohování informací o obnovení pro jednotky chráněné nástrojem BitLocker do služeb Active Directory Domain Services (AD DS). Zálohování hesel obnovení pro jednotky chráněné nástrojem BitLocker umožňují uživatelům s právy správce obnovit jednotku, je-li uzamčena. Díky tomu lze zajistit, že šifrovaná data patřící podniku jsou oprávněným uživatelům vždy dostupná. Pokud zadáte možnost **Žádné**, uživatel odpovídá za pořízení kopie hesla nebo klíče pro obnovení. Pokud uživatel tuto informaci ztratí nebo odmítne jednotku před odchodem z organizace dešifrovat, uživatelé s právy uživatele nebudou moci k jednotce jednoduše přistupovat.  

        -   /Wait: <TRUE&#124;FALSE> – určete, zda pořadí úloh čeká na dokončení šifrování, než bude dokončeno.  

    3.  Vyberte možnost **Balíček**a poté vyberte balíček, který jste vytvořili na začátku tohoto postupu.  

    4.  Na kartě **Možnosti** přidejte následující podmínky:  

        -   Podmínka = proměnná pořadí úloh  

        -   Proměnná = _SMSTSWTG  

        -   Podmínka = Rovno  

        -   Hodnota = True  

    > [!NOTE]  
    >  Krok **Zapnout nástroj BitLocker** , který obvykle následuje po kroku nového příkazového řádku, se nepoužívá k zapnutí nástroje BitLocker pro systém Windows To Go. Tento krok je však možné ponechat v pořadí úloh, aby bylo možné použít nasazení systému Windows 8, která jednotku systému Windows To Go nepoužívají.  

###  <a name="deploy-the-windows-to-go-creator-package-and-task-sequence"></a><a name="BKMK_Deployments"></a> Nasazení balíčku Windows To Go Creator a pořadí úkolů  
 Windows To Go je proces hybridního nasazení. Proto je třeba nasadit balíček Windows To Go Creator a pořadí úloh pro systém Windows 8. Následujícím postupem lze proces nasazení dokončit.  

#### <a name="to-deploy-the-windows-to-go-creator-package"></a>Nasazení balíčku Windows To Go Creator  

1.  V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  

2.  V pracovním prostoru **Softwarová knihovna** rozbalte možnost **Správa aplikací**a klikněte na položku **Balíčky**.  

3.  Vyberte balíček Windows To Go, který jste vytvořili v kroku [Vytvoření balíčku Windows To Go Creator](#BKMK_CreatePackage) .  

4.  Na kartě **Domů** ve skupině **Nasazení** klikněte na možnost **Nasadit**.  

5.  Na stránce **Obecné** určete následující nastavení:  

    1.  **Software**: Ověřte, jestli je vybraný balíček Windows To Go.  

    2.  **Kolekce**: Kliknutím na možnost **Procházet** vyberte kolekci, do které chcete balíček Windows To Go nasadit.  

    3.  **Použít výchozí skupiny distribučních bodů přidružené k této kolekci**: Tuto možnost vyberte, pokud chcete uložit obsah balíčku do výchozí skupiny distribučních bodů kolekce. Pokud jste vybranou kolekci nepřiřadili ke skupině distribučních bodů, tato možnost nebude k dispozici.  

6.  Na stránce **Obsah** klikněte na tlačítko **Přidat** a poté vyberte distribuční body nebo skupiny distribučních bodů, do kterých chcete nasadit obsah přiřazený k tomuto balíčku a programu.  

7.  Na stránce **Nastavení nasazení** vyberte možnost **K dispozici** pro typ nasazení a poté klikněte na tlačítko **Další**.  

8.  Na stránce **Plánování**nastavte, kdy má být tento balíček a program nasazen nebo zpřístupněn klientským zařízením.  

     Možnosti na této stránce se budou lišit v závislosti na nastavení akce nasazení **K dispozici** nebo **Požadováno**.  

9. Na stránce **Plánování**upravte následující nastavení a poté klikněte na tlačítko **Další**.  

    1.  **Naplánovat, kdy bude toto nasazení k dispozici**: Zadejte datum a čas, kdy bude balíček a program dostupný pro spuštění na cílovém počítači. Pokud vyberete možnost **UTC**, toto nastavení zajistí, že balíček a program bude k dispozici pro několik cílových počítačů současně spíše než v různou dobu, dle místního času na cílových počítačích.  

    2.  **Naplánovat, kdy toto nasazení vyprší**: Zadejte datum a čas, kdy bude platnost balíčku a programu v cílovém počítači vyprší. Pokud vyberete možnost **UTC**, toto nastavení zajistí, že pořadí úloh vyprší na několika cílových počítačích současně spíše než v různou dobu, dle místního času na cílových počítačích.  

10. Na stránce **Činnost koncového uživatele** v průvodci zadejte následující informace:  

    -   **Instalace softwaru**: Umožňuje instalaci softwaru mimo nakonfigurovaná časová období údržby.  

    -   **Restart systému (pokud je to nutné pro dokončení instalace)**: Umožňuje restartovat zařízení mimo nakonfigurovaná časová období údržby, pokud to vyžaduje instalace softwaru.  

    -   **Zařízení se systémem Windows Embedded**:  Při nasazení balíčků a programů do zařízení se systémem Windows Embedded s povolenými filtry zápisu můžete vybrat instalaci balíčků a programů v dočasném překrytí a pozdější použití změn, nebo použití změn při dokončení instalace nebo během časového období údržby. Pokud provedete změny v termínu instalace nebo během otevření okna údržby, je nutné provést restart (změny se na zařízení zachovají).  

11. Na stránce **Distribuční body** zadejte následující informace:  

    -   **Možnosti nasazení** : Vyberte **Stáhnout obsah z distribučního bodu a spustit místně**.  

    -   **Povolit klientům sdílet obsah s ostatními klienty ve stejné podsíti**: Tuto možnost vyberte, pokud chcete snížit zatížení sítě tím, že klientům povolíte stahovat obsah z jiných klientů v síti, kteří už obsah stáhli a uložili do mezipaměti. Tato možnost využívá funkci Windows BranchCache a lze ji použít v počítačích s operačním systémem Windows Vista SP2 nebo novějším.  

    -   **Povolit klientům používat náhradní umístění zdroje obsahu**: Určete, jestli klienti můžou jako umístění zdroje obsahu používat jiný než upřednostňovaný distribuční bod, když obsah není v upřednostňovaném distribučním bodě dostupný.  

12. Dokončete průvodce.  

#### <a name="to-deploy-the-windows-8-task-sequence"></a>Nasazení pořadí úloh systému Windows 8  

1.  V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  

2.  V pracovním prostoru **softwarová knihovna** rozbalte možnost **operační systémy**a klikněte na položku **pořadí úloh**.  

3.  Vyberte pořadí úloh systému Windows 8 vytvořené v kroku [Prerequisites to provision Windows To Go](#BKMK_Prereqs) .  

4.  Na kartě **Domů** ve skupině **Nasazení** klikněte na možnost **Nasadit**.  

5.  Na stránce **Obecné** určete následující nastavení:  

    1.  **Pořadí úkolů**: Ověřte, jestli je vybrané pořadí úkolů systému Windows 8.  

    2.  **Kolekce**: Kliknutím na **Procházet** vyberte kolekci, která zahrnuje všechna zařízení, pro které uživatel mohl zřídit funkci Windows To Go.  

        > [!IMPORTANT]  
        >  Pokud předzpracované médium, které jste vytvořili v části [Create prestaged media](#BKMK_CreatePrestagedMedia) , používá proměnnou SMSTSPreferredAdvertID, je možné pořadí úloh nasadit do kolekce **Všechny systémy** a určit nastavení **Pouze systém Windows PE (skryté)** na stránce **Obsah** . Protože pořadí úloh je skryté, bude k dispozici pouze pro médium.  

    3.  **Použít výchozí skupiny distribučních bodů přidružené k této kolekci**: Tuto možnost vyberte, pokud chcete uložit obsah balíčku do výchozí skupiny distribučních bodů kolekce. Pokud jste vybranou kolekci nepřiřadili ke skupině distribučních bodů, tato možnost nebude k dispozici.  

6.  Na stránce **Nastavení nasazení** upravte následující nastavení a poté klikněte na tlačítko **Další**.  

    -   **Účel**: Vyberte možnost **K dispozici**. Pokud nasadíte pořadí úloh pro uživatele, uživatel uvidí zveřejněné pořadí úloh v katalogu aplikací a může si je vyžádat. Pokud nasadíte pořadí úloh do zařízení, uživatel uvidí pořadí úloh v centru softwaru a může je na požádání nainstalovat.  

    -   **Zpřístupnit pro následující**: Určete, jestli je pořadí úkolů dostupné pro Configuration Manager klienty, média nebo technologii PXE.  

        > [!IMPORTANT]  
        >  Nastavení **Pouze média a technologie PXE (skryté)** pro automatické nasazení pořadí úloh. Vyberte možnost **Povolit bezobslužné nasazení operačního systému** a nastavte proměnnou SMSTSPreferredAdvertID jako součást předzpracovaného média, aby počítač automaticky spouštěl nasazení nástroje Windows To Go bez zásahu uživatele, pokud detekuje jednotku Windows To Go. Další informace o těchto nastaveních předzpracovaných médií najdete v části [Create prestaged media](#BKMK_CreatePrestagedMedia) .  

7.  Na stránce **Plánování** upravte následující nastavení a poté klikněte na tlačítko **Další**.  

    1.  **Naplánovat, kdy bude toto nasazení k dispozici**: Zadejte datum a čas, kdy bude pořadí úkolů dostupné pro spuštění na cílovém počítači. Pokud vyberete možnost **UTC**, toto nastavení zajistí, že pořadí úloh bude k dispozici na několika cílových počítačích současně spíše než v různou dobu, dle místního času na cílových počítačích.  

    2.  **Naplánovat, kdy toto nasazení vyprší**: Zadejte datum a čas, kdy vyprší platnost pořadí úkolů na cílovém počítači. Pokud vyberete možnost **UTC**, toto nastavení zajistí, že pořadí úloh vyprší na několika cílových počítačích současně spíše než v různou dobu, dle místního času na cílových počítačích.  

8.  Na stránce **Činnost koncového uživatele** zadejte následující informace:  

    -   **Zobrazit průběh pořadí úloh**: Určete, jestli Configuration Manager klient zobrazuje průběh pořadí úkolů.  

    -   **Instalace softwaru**: Určete, jestli uživatel může software instalovat po naplánovaném čase mimo nakonfigurovaná časová období údržby.  

    -   **Restart systému (pokud je to nutné pro dokončení instalace)**: Umožňuje restartovat zařízení mimo nakonfigurovaná časová období údržby, pokud to vyžaduje instalace softwaru.  

    -   **Zařízení se systémem Windows Embedded**:  Při nasazení balíčků a programů do zařízení se systémem Windows Embedded s povolenými filtry zápisu můžete vybrat instalaci balíčků a programů v dočasném překrytí a pozdější použití změn, nebo použití změn při dokončení instalace nebo během časového období údržby. Pokud provedete změny v termínu instalace nebo během otevření okna údržby, je nutné provést restart (změny se na zařízení zachovají).  

    -   **Internetoví klienti**: Určete, jestli se pořadí úkolů může spustit v internetovém klientovi. V tomto nastavení nejsou podporovány činnosti, které instalují software, například operační systém. Tuto možnost použijte pouze pro obecná pořadí úloh založená na skriptu, která slouží k provádění operací v běžném operačním systému.  

9. Na stránce **Výstrahy** určete nastavení upozorňování pro toto nasazení pořadí úloh a poté klikněte na tlačítko **Další**.  

10. Na stránce **Distribuční body** určete následující data a poté klikněte na tlačítko **Další**.  

    -   **Možnosti nasazení**: Vyberte **Pokud to vyžaduje spuštění pořadí úkolů, stáhnout veškerý obsah místně**.  

    -   **Není-li místní distribuční bod k dispozici, použijte vzdálený distribuční bod**: Určete, jestli klienti můžou ke stažení obsahu, který vyžaduje pořadí úkolů, používat distribuční body v pomalých a nespolehlivých sítích.  

    -   **Umožňuje klientům používat náhradní umístění zdroje obsahu**:
        - *Před verzí 1610*můžete zaškrtnout políčko umožnit záložní umístění zdroje pro obsah, aby se klienti mimo tyto skupiny hranic mohli vracet a používat distribuční bod jako umístění zdroje obsahu, pokud nejsou k dispozici žádné jiné distribuční body.
        - *Počínaje verzí 1610*již nemůžete konfigurovat **záložní umístění zdroje pro obsah**.  Místo toho můžete nakonfigurovat vztahy mezi skupinami hranic, které určují, kdy může klient začít vyhledávat další skupiny hranic pro platné umístění zdroje obsahu. 

11. Dokončete průvodce.  

###  <a name="user-runs-the-windows-to-go-creator"></a><a name="BKMK_UserExperience"></a> Spuštění nástroje Windows To Go Creator uživatelem  
 Po nasazení balíčku Windows To Go a pořadí úloh systému Windows 8 bude uživatelům k dispozici nástroj Windows To Go Creator. Uživatel může přejít do katalogu softwaru nebo centra softwaru, pokud byl nástroj Windows To Go Creator nasazen do zařízení, a spustit program Windows To Go Creator. Po stažení balíčku nástroje Creator se na hlavním panelu úloh zobrazí blikající ikona. Když uživatel na ikonu klikne, zobrazí se dialogové okno pro výběr jednotky Windows To Go pro zajišťování (pokud není použita možnost příkazového řádku /drive). Pokud tato jednotka nesplňuje požadavky nástroje Windows To Go nebo pokud na jednotce není dostatek volného místa pro instalaci bitové kopie, program Creator zobrazí chybové hlášení. Uživatel může ověřit jednotku a bitovou kopii, která bude použita, na stránce potvrzení. Během konfigurace a předzpracování obsahu nástrojem Creator na jednotce Windows To Go se zobrazuje dialogové okno průběhu. Po dokončení předzpracování nástroj Creator zobrazí výzvu k restartování počítače, aby bylo možné jednotku Windows To Go spustit.  

> [!NOTE]  
>  Pokud jste nepovolili přesměrování spuštění v rámci příkazového řádku pro program Creator v části [Create a Windows To Go Creator package](#BKMK_CreatePackage) , uživatel může být požádán o ruční spuštění jednotky Windows To Go při každém restartu systému.  

###  <a name="configuration-manager-configures-and-stages-the-windows-to-go-drive"></a><a name="BKMK_ConfigureStageDrive"></a> Konfigurace a zpracování jednotky Windows To Go nástrojem Configuration Manager  
 Po restartu počítače z jednotky Windows To Go se jednotka spustí v systému Windows PE a připojí se k bodu správy, aby bylo možné získat zásadu pro dokončení nasazení operačního systému. Configuration Manager konfiguraci a fázi jednotky. Po Configuration Manager fázi jednotky může uživatel počítač restartovat, aby se proces zajišťování dokončí (například pro připojení k doméně nebo instalace aplikací). Tento proces je pro všechna předzpracovaná média stejný.  

###  <a name="user-logs-in-to-windows-8"></a><a name="BKMK_UserLogsIn"></a>Přihlášení uživatele k systému Windows 8  
 Po dokončení procesu zřízení Configuration Manager se uživatel může přihlásit k operačnímu systému a zobrazí se zamykací obrazovka systému Windows 8.  
