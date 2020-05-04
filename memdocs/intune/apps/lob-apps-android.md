---
title: Přidání obchodní aplikace pro Android do Microsoft Intune
description: Přečtěte si, jak přidat obchodní aplikaci pro Android do Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/23/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 061d793c-c724-4cd9-9240-adb0cbda5661
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0fb8f9e4f779acc9f77327d3fdeee20ae02c6924
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "80324106"
---
# <a name="add-an-android-line-of-business-app-to-microsoft-intune"></a>Přidání obchodní aplikace pro Android do Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Obchodní aplikace (LOB) je aplikace, kterou do Intune přidáte z instalačního souboru aplikace. Tento typ aplikace zpravidla vzniká interně. Intune nainstaluje obchodní aplikaci na zařízení uživatele. 

> [!Note]
> Další informace o obchodních aplikacích a konzole pro vývojáře Google Play najdete v tématu [spravovaná Google Play Private (LOB) publikování aplikací pomocí konzole pro vývojáře Google](apps-add-android-for-work.md?#managed-google-play-private-lob-app-publishing-using-the-google-developer-console). 

> [!Note]
> Zařízení s Androidem for Work najdete v tématu [Přidání spravovaných Google Play aplikací do zařízení s Androidem Enterprise v Intune](apps-add-android-for-work.md). 

## <a name="select-the-app-type"></a>Vyberte typ aplikace.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > **všechny aplikace** > **Přidat**.
3. V podokně **Vybrat typ aplikace** v části **ostatní** typy aplikací vyberte **obchodní aplikace**.
4. Klikněte na **Vybrat**. Zobrazí se kroky **Přidání aplikace** .

## <a name="step-1---app-information"></a>Krok 1 – informace o aplikaci

### <a name="select-the-app-package-file"></a>Vyberte soubor balíčku aplikace.

1. V podokně **Přidat aplikaci** klikněte na **Vybrat soubor balíčku aplikace**. 
2. V podokně **Soubor balíčku aplikace** vyberte tlačítko Procházet. Pak vyberte instalační soubor Androidu s příponou **. apk**.
   Zobrazí se podrobnosti o aplikaci.
3. Až budete hotovi, vyberte **OK** v podokně **soubor balíčku aplikace** a přidejte aplikaci.

### <a name="set-app-information"></a>Nastavení informací o aplikaci

1. Na stránce **informace o aplikaci** přidejte podrobnosti o aplikaci. V závislosti na zvolené aplikaci můžou být některé hodnoty v tomto podokně vyplněné automaticky:
    - **Název**: Zadejte název aplikace, který se zobrazí na portálu společnosti. Ověřte, že názvy všech používaných aplikací jsou jedinečné. Pokud stejný název aplikace existuje dvakrát, zobrazí se na portálu společnosti jen jedna z aplikací.
    - **Popis**: Zadejte popis aplikace. Popis se zobrazí na portálu společnosti.
    - **Vydavatel**: zadejte název vydavatele aplikace.
    - **Minimální operační systém**: V seznamu zvolte minimální verzi operačního systému, na kterou jde aplikaci nainstalovat. Pokud aplikaci přiřadíte k zařízení se starším operačním systémem, nenainstaluje se.
    - **Kategorie**: vyberte jednu nebo více předdefinovaných kategorií aplikací nebo vyberte kategorii, kterou jste vytvořili. Díky kategoriím uživatelé aplikaci při procházení portálu společnosti snadněji najdou.
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

## <a name="step-5-update-a-line-of-business-app"></a>Krok 5: Aktualizace obchodní aplikace

[!INCLUDE [shared-proc-lob-updateapp](../includes/shared-proc-lob-updateapp.md)]

Pokud je na zařízení s Androidem zapnutá možnost **kontrolovat aplikace z externích zdrojů** , uživateli se zobrazí výzva před instalací aktualizace. V opačném případě se aktualizace nainstaluje automaticky.

> [!Note]
> Aby služba Intune úspěšně nasadila nový soubor APK do zařízení, musíte zvýšit hodnotu řetězce `android:versionCode` v souboru AndroidManifest.xml v balíčku APK.

## <a name="next-steps"></a>Další kroky

- Aplikace, kterou jste vytvořili, se zobrazí v seznamu aplikací. Teď ji můžete přiřadit do požadovaných skupin. Nápovědu najdete v článku [Přiřazení aplikací do skupin](apps-deploy.md).

- Zjistěte, jakými způsoby můžete monitorovat vlastnosti a přiřazení aplikace. Viz [Postup monitorování informací a přiřazení aplikace](apps-monitor.md).

- Zjistěte více o kontextu své aplikace v Intune. Viz [Přehled životních cyklů zařízení a aplikací](../fundamentals/device-lifecycle.md).
