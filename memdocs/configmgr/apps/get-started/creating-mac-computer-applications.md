---
title: Vytváření aplikací pro počítače Mac
titleSuffix: Configuration Manager
description: V této části najdete informace, které je nutné vzít v úvahu při vytváření a nasazování aplikací pro počítače se systémem Mac.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: ab1aecdd-d943-44f5-b0a9-e8fe7439e5d6
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3b734dc6149c1613d986205577b46160d363d31d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075784"
---
# <a name="create-mac-computer-applications-with-configuration-manager"></a>Vytváření aplikací pro počítače Mac pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Při vytváření a nasazování aplikací pro počítače Mac mějte na paměti následující skutečnosti.  

> [!IMPORTANT]  
>  Postupy v tomto tématu se týkají informací o nasazení aplikací do počítačů se systémem Mac, na kterých jste nainstalovali klienta Configuration Manager. Počítače Mac, které jste registrovali v Microsoft Intune, nepodporují nasazení aplikací.  

## <a name="general-considerations"></a>Obecné aspekty  
 Configuration Manager můžete použít k nasazení aplikací do počítačů se systémem Mac, na kterých běží klient Configuration Manager Mac. Postup nasazení softwaru do počítačů se systémem Mac se podobá postupu při nasazení softwaru do počítačů se systémem Windows. Před vytvořením a nasazením aplikací pro počítače se systémem Mac, které jsou spravovány nástrojem Configuration Manager, je však třeba vzít v úvahu následující:  

-   Předtím, než budete moci nasadit balíčky aplikací systému Mac do počítačů se systémem Mac, je nutné použít nástroj **CMAppUtil** na počítači Mac k převedení těchto aplikací do formátu, který lze přečíst Configuration Manager.  

-   Configuration Manager nepodporuje nasazení aplikací systému Mac pro uživatele. Místo toho je třeba provést tato nasazení na zařízení. Podobně pro nasazení aplikací pro systém Mac Configuration Manager nepodporuje možnost **předem nasadit software na primární zařízení uživatele** na stránce **nastavení nasazení** v **Průvodci nasazením softwaru**.  

-   Aplikace systému Mac podporují simulovaná nasazení.  

-   Do počítačů se systémem Mac nelze nasadit aplikace s účelem **K dispozici**.  

-   V počítačích se systémem Mac není podporována možnost odeslání paketů buzení ze spánku při nasazení softwaru.  

-   Počítače Mac nepodporují Background Intelligent Transfer Service (BITS) pro stahování obsahu aplikace. Pokud se stažení aplikace nepovede, restartuje se od začátku.  

-   Configuration Manager nepodporuje globální podmínky při vytváření typů nasazení pro počítače se systémem Mac.  

## <a name="steps-to-create-and-deploy-an-application"></a>Postup vytvoření a nasazení aplikace  
 Následující tabulka uvádí kroky, podrobnosti a informace o vytváření a nasazování aplikací pro počítače se systémem Mac.  


|                                         Krok                                          |                                                                                                             Podrobnosti                                                                                                              |
|---------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|            **Krok 1**: Příprava aplikací pro Mac pro Configuration Manager             | Předtím, než budete moci vytvářet Configuration Manager aplikace ze softwarových balíčků systému Mac, je nutné použít nástroj **CMAppUtil** na počítači Mac k převedení softwaru systému Mac do souboru Configuration Manager<strong>. cmmac</strong> . |
| **Krok 2**: vytvoření Configuration Manager aplikace obsahující software pro systém Mac |                                                                       Pomocí **Průvodce vytvořením aplikace** vytvořte aplikaci pro software počítače Mac.                                                                       |
|             **Krok 3**: vytvoření typu nasazení pro aplikaci pro Mac              |                                                              Tento krok je vyžadován, pouze pokud jste tyto informace automaticky nenaimportovali z aplikace.                                                               |
|                        **Krok 4**: nasazení aplikace pro Mac                         |                                                                          Pomocí **Průvodce nasazením softwaru** Nasaďte aplikaci do počítačů se systémem Mac.                                                                          |
|               **Krok 5**: monitorování nasazení aplikace systému Mac               |                                                                                 Monitorujte úspěšné nasazení aplikace do počítačů se systémem Mac.                                                                                 |

## <a name="supplemental-procedures-to-create-and-deploy-applications-for-mac-computers"></a>Další postupy k vytvoření a nasazení aplikací pro počítače Mac  
 Následující postupy použijte k vytvoření a nasazení aplikací pro počítače se systémem Mac, které jsou spravovány nástrojem Configuration Manager.  

###  <a name="step-1-prepare-mac-applications-for-configuration-manager"></a>Krok 1: Příprava aplikací systému Mac pro nástroj Configuration Manager  
 Proces vytváření a nasazování aplikací Configuration Manager do počítačů se systémem Mac se podobá procesu nasazení pro počítače se systémem Windows. Před vytvořením Configuration Manager aplikací, které obsahují typy nasazení systému Mac, je však nutné připravit aplikace pomocí nástroje **CMAppUtil** . Tento nástroj se stáhne společně s instalačními soubory klienta systému Mac. Nástroj **CMAppUtil** může shromažďovat informace o aplikaci, které zahrnují data o detekci z následujících balíčků systému Mac:  

-   Bitová kopie disku Apple (.dmg)  

-   Soubor metabalíčku (.mpkg)  

-   Balíček instalační služby systému Mac OS X (.pkg)  

-   Aplikace systému Mac OS X (.app)  

Jakmile nástroj **CMAppUtil** shromáždí informace o aplikaci, vytvoří soubor s příponou **.cmmac**. Tento soubor obsahuje instalační soubory pro software systému Mac a informace o metodách detekce, které lze použít k vyhodnocení, zda je aplikace již nainstalovaná. Nástroj**CMAppUtil** může pracovat také se soubory **.dmg** , které obsahují několik aplikací systému Mac, a vytvářet různé typy nasazení pro jednotlivé aplikace.  

1.  Zkopírujte instalační balíček softwaru systému Mac do složky v počítači se systémem Mac, do které jste extrahovali obsah souboru **macclient.dmg** , který jste stáhli ze služby Stažení softwaru společnosti Microsoft.  

2.  Ve stejném počítači se systémem Mac otevřete okno terminálu a přejděte do složky, do které jste extrahovali obsah souboru **macclient.dmg** .  

3.  Přejděte do složky **nástroje** a zadejte následující příkaz příkazového řádku:  

     **./CMAppUtil** *<vlastnosti\>*  

     Řekněme například, že chcete převést obsah souboru bitové kopie disku Apple s názvem **Mysoftware. dmg** , který je uložený ve složce plochy uživatele, do souboru **cmmac** ve stejné složce. Budete také chtít vytvořit soubory **cmmac** pro všechny aplikace, které se nacházejí v souboru bitové kopie disku. Chcete-li provést tuto akci, použijte následující příkazový řádek:  

     **./CMApputil –c /Users/** *<Uživatelské_jméno\>* **/Desktop/MySoftware.dmg -o /Users/** *<Uživatelské_jméno\>* **/Desktop -a**  

    > [!NOTE]  
    >  Název aplikace nemůže být delší než 128 znaků.  

     Chcete-li nakonfigurovat možnosti nástroje **CMAppUtil**, použijte vlastnosti příkazového řádku v následující tabulce:  

    |Vlastnost|Další informace|  
    |--------------|----------------------|  
    |**-h**|Zobrazí dostupné vlastnosti příkazového řádku.|  
    |**-r**|Vytvoří výstup souboru **detection.xml** poskytnutého souboru **.cmmac** do souboru **stdout**. Výstup obsahuje parametry detekce a verzi nástroje **CMAppUtil**, která byla použita k vytvoření souboru **.cmmac**.|  
    |**-c**|Určuje zdrojový soubor, který se má převést.|  
    |**– o**|Určuje výstupní cestu ve spojení s vlastností – c.|  
    |**-a**|Automaticky vytvoří soubory. cmmac ve spojení s vlastností – c pro všechny aplikace a balíčky v souboru bitové kopie disku.|  
    |**-s**|Přeskočí vytvoření souboru **detection.xml** , pokud nejsou nalezeny žádné parametry detekce, a vynutí vytvoření souboru **.cmmac** bez souboru **detection.xml** .|  
    |**-v**|Zobrazí podrobný výstup nástroje **CMAppUtil** spolu s diagnostickými informacemi.|  

4.  Ověřte, že byl v zadané výstupní složce vytvořen soubor **.cmmac** .  

###  <a name="create-a-configuration-manager-application-that-contains-the-mac-software"></a>Vytvoření aplikace Configuration Manager obsahující software pro systém Mac  

Pomocí následujícího postupu můžete vytvořit aplikaci pro počítače se systémem Mac, které jsou spravovány nástrojem Configuration Manager.  

1.  V konzole Configuration Manager vyberte možnost **softwarová knihovna** > aplikace**Správa** > **Applications**aplikací.  

3.  Na kartě **Domů** ve skupině **vytvořit** vyberte možnost **vytvořit aplikaci**.  

4.  Na stránce **Obecné** v nástroji **Průvodce vytvořením aplikace**vyberte možnost **automaticky zjišťovat informace o této aplikaci z instalačních souborů**.  

    > [!NOTE]  
    >  Pokud chcete zadat informace o aplikaci sami, vyberte možnost **ručně zadat informace o aplikaci**. Další informace o tom, jak informace zadat ručně, najdete v tématu [vytváření aplikací pomocí Configuration Manager](../../apps/deploy-use/create-applications.md).  

5.  V rozevíracím seznamu **Typ** vyberte možnost **Mac OS X**.  

6.  Do pole **umístění** zadejte cestu UNC ve tvaru * \\ \\<server\> \\ \> \\<sdílet<název\> * souboru pro instalační soubor aplikace pro systém Mac (soubor **. cmmac** ), který zjistí informace o aplikaci. Případně klikněte na tlačítko **Procházet** a vyhledejte a zadejte umístění instalačního souboru.  

    > [!NOTE]  
    >  Je nutné mít přístup k cestě UNC, která obsahuje aplikaci.  

7.  Zvolte **Další**.  

8.  Na stránce **importovat informace** v nástroji **Průvodce vytvořením aplikace**zkontrolujte informace, které byly naimportovány. V případě potřeby si můžete vybrat možnost **Předchozí** a vrátit se zpátky a opravit případné chyby. Pokračujte kliknutím na tlačítko **Další** .  

9. Na stránce **Obecné informace** v nástroji **Průvodce vytvořením aplikace**zadejte informace o aplikaci, například název aplikace, komentáře, verzi a nepovinný odkaz, který vám může při odkazování aplikace v konzole Configuration Manager.  

    > [!NOTE]  
    >  Pokud byly některé informace o aplikaci dříve získány z instalačních souborů aplikace, mohou být na této stránce již na této stránce.  

10. Klikněte na tlačítko **Další**, na stránce **Souhrn** zkontrolujte informace o aplikaci a pak dokončete **Průvodce vytvořením aplikace**.  

11. Nová aplikace se zobrazí v uzlu **aplikace** konzoly Configuration Manager.  

###  <a name="step-3-create-a-deployment-type-for-the-mac-application"></a>Krok 3: Vytvoření typu nasazení pro aplikaci systému Mac  
 Pomocí následujícího postupu můžete vytvořit typ nasazení pro počítače se systémem Mac, které jsou spravovány nástrojem Configuration Manager.  

> [!NOTE]  
>  Pokud jste automaticky naimportovali informace o aplikaci v **Průvodci vytvořením aplikace**, je možné, že již byl vytvořen typ nasazení pro aplikaci.  

1.  V konzole Configuration Manager vyberte možnost **softwarová knihovna** > aplikace**Správa** > **Applications**aplikací.  

3.  Vyberte aplikaci. Pak na kartě **Domů** ve skupině **aplikace** zvolte možnost **vytvořit typ nasazení** a vytvořte nový typ nasazení pro tuto aplikaci.  

    > [!NOTE]  
    >  **Průvodce vytvořením typu nasazení** můžete také spustit z **Průvodce vytvořením aplikace** a z karty **typy nasazení** dialogového okna *<název\> aplikace* **vlastnosti** .  

4.  Na stránce **Obecné** v nástroji **Průvodce vytvořením typu nasazení**vyberte v rozevíracím seznamu **typ** možnost **Mac OS X**.  

5.  Do pole **umístění** zadejte cestu UNC \\ \\ ve tvaru<\> \\ Server<sdílené složky\> \\<název_souboru\> do instalačního souboru aplikace (soubor **. cmmac** ). Případně klikněte na tlačítko **Procházet** a vyhledejte a zadejte umístění instalačního souboru.  

    > [!NOTE]  
    >  Je nutné mít přístup k cestě UNC, která obsahuje aplikaci.  

6.  Zvolte **Další**.  

7.  Na stránce **Importovat informace** v **Průvodci vytvořením typu nasazení**zkontrolujte naimportované informace. V případě potřeby se kliknutím na tlačítko **Předchozí** vraťte zpět a opravte všechny chyby. Pokračujte výběrem položky **Další**.  

8.  Na stránce **Obecné informace** v **Průvodci vytvořením typu nasazení**zadejte informace o aplikaci, například název aplikace, komentáře a jazyky, ve kterých je typ nasazení dostupný.  

    > [!NOTE]  
    >  Pokud byly některé informace o typu nasazení dříve získány z instalačních souborů aplikace, mohou být na této stránce již na této stránce.  

9. Zvolte **Další**.  

10. Na stránce **požadavky** v **Průvodci vytvořením typu nasazení**můžete zadat podmínky, které je nutné splnit, než bude možné nainstalovat typ nasazení do počítačů se systémem Mac.  

11. Kliknutím na tlačítko **Přidat** otevřete dialogové okno **vytvořit požadavek** a přidejte nový požadavek.  

    > [!NOTE]  
    >  Nové požadavky můžete přidat také na kartě **Požadavky** dialogového okna *<název_typu_nasazení\> – * **Vlastnosti**.  

12. V rozevíracím seznamu **Kategorie** vyberte, že tento požadavek je pro zařízení.  

13. V rozevíracím seznamu **Podmínka** vyberte podmínku, kterou chcete použít k vyhodnocení, jestli počítač Mac splňuje požadavky na instalaci. Obsah tohoto seznamu se liší v závislosti na vybrané kategorii.  

14. V rozevíracím seznamu **operátor** vyberte operátor, který se má použít k porovnání vybrané podmínky se zadanou hodnotou, a vyhodnotí, zda uživatel nebo zařízení splňuje požadavky na instalaci. Dostupné operátory se liší v závislosti na zvolené podmínce.  

15. V poli **hodnota** zadejte hodnoty, které mají být použity s vybranou podmínkou a operátorem, k vyhodnocení, zda uživatel nebo zařízení splňují požadavky na instalaci. Dostupné hodnoty se liší v závislosti na vámi vybrané podmínce a operátoru.

16. Kliknutím na **tlačítko OK** uložte pravidlo požadavku a zavřete dialogové okno **vytvořit požadavek** .  

17. Na stránce **požadavky** v nástroji **Průvodce vytvořením typu nasazení**klikněte na tlačítko **Další**.  

18. Na stránce **Souhrn** v **Průvodci vytvořením typu nasazení**zkontrolujte akce, které má průvodce provést.  V případě potřeby klikněte na tlačítko **Předchozí** , vraťte se zpět a změňte nastavení typu nasazení. Pro vytvoření typu nasazení klikněte na tlačítko **Další** .  

19. Po dokončení stránky **průběh** zkontrolujte provedené akce a potom kliknutím na tlačítko **Zavřít** dokončete **Průvodce vytvořením typu nasazení**.  

20. Pokud jste tohoto průvodce spustili z **Průvodce vytvořením aplikace**, vrátíte se na stránku **typy nasazení** .  

###  <a name="deploy-the-mac-application"></a>Nasazení aplikace pro systém Mac  
 Postup nasazení aplikace do počítačů se systémem Mac je stejný jako postup nasazení aplikace do počítačů se systémem Windows, s výjimkou následujících rozdílů:  

-   Není podporováno nasazení aplikací uživatelům.  

-   Nasazení s účelem **K dispozici** nejsou podporována.  

-   Možnost **předem nasadit software na primární zařízení uživatele** na stránce **nastavení nasazení** v **Průvodci nasazením softwaru** není podporována.  

-   Vzhledem k tomu, že počítače Mac nepodporují Centrum softwaru, je nastavení **oznámení uživateli** na stránce **činnost koncového uživatele** v **Průvodci nasazením softwaru** ignorováno.  

-   V počítačích se systémem Mac není podporována možnost odeslání paketů buzení ze spánku při nasazení softwaru.  

> [!NOTE]  
>  Můžete vytvořit kolekci, která bude obsahovat pouze počítače Mac. Pokud to chcete udělat, vytvořte kolekci, která použije pravidlo dotazu a použijte vzorový dotaz WQL v tématu [Vytvoření dotazů](../../core/servers/manage/create-queries.md) .  

 Další informace najdete v tématu [nasazení aplikací](../../apps/deploy-use/deploy-applications.md).  

###  <a name="step-5-monitor-the-deployment-of-the-mac-application"></a>Krok 5: monitorování nasazení aplikace systému Mac  
 Stejný postup můžete použít k monitorování nasazení aplikací do počítačů se systémem Mac, protože byste mohli monitorovat nasazení aplikací do počítačů se systémem Windows.  

 Další informace najdete v tématu [monitorování aplikací](../deploy-use/monitor-applications-from-the-console.md).  
