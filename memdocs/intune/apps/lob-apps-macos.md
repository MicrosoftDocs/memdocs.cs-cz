---
title: Přidání obchodních aplikací pro macOS do Microsoft Intune
titleSuffix: ''
description: Přečtěte si, jak přidat macOS obchodní aplikace do Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/31/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ef8008ac-8b85-4bfc-86ac-1f9fcbd3db76
ms.reviewer: aiwang
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6dad4dffba0efadcca0ea5eb7d61960bec1b3f8e
ms.sourcegitcommit: 0907ee1137773f0482b1d2b9bb344e206d05aede
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/01/2020
ms.locfileid: "80536839"
---
# <a name="how-to-add-macos-line-of-business-lob-apps-to-microsoft-intune"></a>Přidání obchodních aplikací pro macOS do Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Informace v tomto článku vám pomůžou přidat do Microsoft Intune obchodní aplikace pro macOS. Než budete moct obchodní soubor nahrát do Microsoft Intune, musíte si stáhnout externí nástroj pro předběžné zpracování souborů *.pkg*. Předběžné zpracování souborů *.pkg* se musí provést v zařízení s macOS.

> [!NOTE]
> Od vydání verze macOS Catalina 10,15 se před přidáním vašich aplikací do Intune ujistěte, že jsou vaše obchodní aplikace macOS notarized. Pokud vývojáři vašich obchodních aplikací nenotarize své aplikace, aplikace se nespustí na zařízeních macOS vašich uživatelů. Další informace o tom, jak zjistit, jestli je aplikace notarized, najdete v článku [Notarize své aplikace MacOS pro přípravu na MacOS Catalina](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Notarizing-your-macOS-apps-to-prepare-for-macOS/ba-p/808579).

> [!NOTE]
> Uživatelé zařízení s macOS můžou odebrat některé integrované aplikace pro macOS, třeba aplikace Akcie a Mapy, ale není možné tyto aplikace s použitím Intune znovu nasadit. Když koncoví uživatelé tyto aplikace odstraní, musí přejít do App Storu a znovu si je ručně nainstalovat.

## <a name="before-your-start"></a>Než začnete

Musíte si stáhnout externí nástroj, označit stažený nástroj jako spustitelný soubor a předem zpracovat soubory *. pkg* pomocí nástroje, abyste mohli nahrát svůj obchodní soubor do Microsoft Intune. Předběžné zpracování souborů *.pkg* se musí provést v zařízení s macOS. Pomocí nástroje Intune App Wrapping Tool pro Mac umožněte správu aplikací pro Mac pomocí Microsoft Intune.

> [!IMPORTANT]
> Soubor *. pkg* musí být podepsán pomocí certifikátu instalační program ID pro vývojáře získaný z účtu Apple Developer. K nahrání obchodních aplikací pro macOS do Microsoft Intune je možné použít jenom soubory *.pkg*. Převod jiných formátů, například z *.dmg* na *.pkg*, není podporovaný.
>

1. Stáhněte si [Nástroj pro zabalení aplikace Intune pro Mac](https://github.com/msintuneappsdk/intune-app-wrapping-tool-mac).

    > [!NOTE]
    > **Intune App Wrapping Tool pro Mac** se musí spustit v počítači s macOS. 

2. Označte stažený nástroj jako spustitelný soubor:
   - Spusťte aplikaci Terminal.
   - Změňte adresář na umístění, kde se nachází `IntuneAppUtil`.
   - Spusťte následující příkaz, který nastaví spustitelný soubor nástroje:<br> 
       `chmod +x IntuneAppUtil`

3. Pomocí příkazu `IntuneAppUtil` v **Intune App Wrapping Tool pro Mac** zabalte soubor obchodní aplikace *.pkg* ze souboru *.intunemac*.<br>

    Tady jsou vzorové příkazy pro Microsoft Intune App Wrapping Tool pro macOS:
    > [!IMPORTANT]
    > Před spuštěním příkazů `IntuneAppUtil` zajistěte, aby `<source_file>` argumentu neobsahuje mezery.

    - `IntuneAppUtil -h`<br>
    Tento příkaz zobrazí informace o využití nástroje.
    
    - `IntuneAppUtil -c <source_file> -o <output_directory_path> [-v]`<br>
    Tento příkaz zalomí soubor aplikace LOB *. pkg* , který je součástí `<source_file>`, do souboru *. intunemac* se stejným názvem a umístí ho do složky, na kterou odkazuje `<output_directory_path>`.
    
    - `IntuneAppUtil -r <filename.intunemac> [-v]`<br>
    Tento příkaz extrahuje zjištěné parametry a verze vytvořeného souboru *.intunemac*.

## <a name="select-the-app-type"></a>Vyberte typ aplikace.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > **všechny aplikace** > **Přidat**.
3. V podokně **Vybrat typ aplikace** v části **ostatní** typy aplikací vyberte **obchodní aplikace**.
4. Klikněte na **Vybrat**. Zobrazí se kroky **Přidání aplikace** .

## <a name="step-1---app-information"></a>Krok 1 – informace o aplikaci

### <a name="select-the-app-package-file"></a>Vyberte soubor balíčku aplikace.

1. V podokně **Přidat aplikaci** klikněte na **Vybrat soubor balíčku aplikace**. 
2. V podokně **Soubor balíčku aplikace** vyberte tlačítko Procházet. Pak vyberte instalační soubor macOS s příponou *. intunemac*.
   Zobrazí se podrobnosti o aplikaci.
3. Až budete hotovi, vyberte **OK** v podokně **soubor balíčku aplikace** a přidejte aplikaci.

### <a name="set-app-information"></a>Nastavení informací o aplikaci

1. Na stránce **informace o aplikaci** přidejte podrobnosti o aplikaci. V závislosti na zvolené aplikaci můžou být některé hodnoty v tomto podokně vyplněné automaticky:
    - **Název**: Zadejte název aplikace, který se zobrazí na portálu společnosti. Ověřte, že názvy všech používaných aplikací jsou jedinečné. Pokud stejný název aplikace existuje dvakrát, zobrazí se na portálu společnosti jen jedna z aplikací.
    - **Popis**: Zadejte popis aplikace. Popis se zobrazí na portálu společnosti.
    - **Vydavatel**: Zadejte název vydavatele aplikace.
    - **Minimální operační systém**: V seznamu zvolte minimální verzi operačního systému, na kterou jde aplikaci nainstalovat. Pokud aplikaci přiřadíte k zařízení se starším operačním systémem, nenainstaluje se.
    - **Kategorie**: Vyberte jednu nebo několik předdefinovaných kategorií aplikací nebo kategorii, kterou jste si vytvořili sami. Díky kategoriím uživatelé aplikaci při procházení portálu společnosti snadněji najdou.
    - **Zobrazit tuto aplikaci jako doporučenou aplikaci v portál společnosti**: když uživatelé vyhledávají aplikace, zobrazí se na hlavní stránce portálu společnosti výrazně.
    - **Adresa URL informací**: Volitelně můžete zadat adresu URL webu, který obsahuje informace o této aplikaci. Adresa URL se zobrazí na portálu společnosti.
    - **Adresa URL informací o ochraně osobních údajů**: Volitelně zadejte adresu URL webu, který obsahuje informace o ochraně osobních údajů v této aplikaci. Adresa URL se zobrazí na portálu společnosti.
    - **Vývojář**: Volitelně zadejte jméno vývojáře aplikace.
    - **Vlastník**: Volitelně zadejte jméno vlastníka aplikace. Zadat můžete například **Personální oddělení**.
    - **Poznámky**: Zadejte jakékoli poznámky, které chcete k aplikaci přidružit.
    - **Logo**: Nahrajte ikonu, která se k aplikaci přidruží. Tato ikona se u aplikace zobrazí, když uživatelé procházejí portál společnosti.
2. Kliknutím na tlačítko **Další** zobrazíte stránku **značky oboru** .

## <a name="step-2---select-scope-tags-optional"></a>Krok 2 – výběr značek oboru (volitelné)

Pomocí značek Scope můžete určit, kdo může v Intune zobrazit informace o klientské aplikaci. Úplné podrobnosti o značkách oboru najdete v tématu [použití značek řízení přístupu na základě role a rozsahu pro distribuci IT](../fundamentals/scope-tags.md).

1. Klikněte na **Vybrat značky oboru** a volitelně přidejte značky oboru pro aplikaci. 
2. Kliknutím na tlačítko **Další** zobrazíte stránku **přiřazení** .

## <a name="step-3---assignments"></a>Krok 3 – přiřazení

1. Vyberte **požadované**, **dostupné pro zaregistrovaná zařízení**nebo **odinstalujte** přiřazení skupin pro aplikaci. Další informace najdete v tématech [Přidání skupin pro uspořádání uživatelů a zařízení](../fundamentals/groups-add.md) a [přiřazení aplikací do skupin pomocí Microsoft Intune](apps-deploy.md).
2. Kliknutím na **Další** zobrazte stránku **Revize + vytvořit** . 

## <a name="step-4---review--create"></a>Krok 4 – přezkoumání a vytvoření

1. Zkontrolujte hodnoty a nastavení, které jste zadali pro aplikaci.
2. Po dokončení klikněte na **vytvořit** , aby se aplikace přidala do Intune.

    Zobrazí se okno **Přehled** pro obchodní aplikaci.

Vytvořená aplikace se zobrazí v seznamu aplikací, kde ji můžete přiřadit ke zvoleným skupinám. Nápovědu najdete v článku [Přiřazení aplikací do skupin](apps-deploy.md).

> [!NOTE]
> Pokud soubor *.pkg* obsahuje více aplikací nebo instalačních programů aplikací, pak Microsoft Intune ohlásí, že je *aplikace* úspěšně nainstalovaná, jenom když se v zařízení zjistí všechny nainstalované aplikace.

## <a name="update-a-line-of-business-app"></a>Aktualizace obchodní aplikace

[!INCLUDE [shared-proc-lob-updateapp](../includes/shared-proc-lob-updateapp.md)]

> [!NOTE]
> Aby služba Intune úspěšně nasadila nový soubor *.pkg* do zařízení, musíte zvýšit hodnotu řetězců `version` a `CFBundleVersion` balíčku v souboru *packageinfo* v balíčku *.pkg*.

## <a name="next-steps"></a>Další kroky

- Aplikace, kterou jste vytvořili, se zobrazí v seznamu aplikací. Nyní ji můžete přiřadit do požadované skupiny. Nápovědu najdete v článku [Přiřazení aplikací do skupin](apps-deploy.md).

- Zjistěte, jakými způsoby můžete monitorovat vlastnosti a přiřazení aplikace. Další informace najdete v tématu [Postup monitorování informací a přiřazení aplikace](apps-monitor.md).

- Zjistěte více o kontextu své aplikace v Intune. Další informace najdete v tématu [Přehled životních cyklů zařízení a aplikací](../fundamentals/device-lifecycle.md).
