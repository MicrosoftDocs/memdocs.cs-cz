---
title: Přidání obchodní aplikace pro Windows do Microsoft Intune
titleSuffix: ''
description: Naučte se, jak pomocí Microsoft Intune přidat obchodní aplikaci pro Windows.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f81c5f82-5cfa-4b97-9f73-d6cf77c06896
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5b70f36873200d0adbbc356d9a482cf13cc2ea49
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913320"
---
# <a name="add-a-windows-line-of-business-app-to-microsoft-intune"></a>Přidání obchodní aplikace pro Windows do Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Obchodní aplikace (LOB) je aplikace, kterou přidáte z instalačního souboru aplikace. Tento typ aplikace zpravidla vzniká interně. Následující kroky obsahují pokyny k přidání obchodní aplikace pro Windows do Microsoft Intune.

> [!IMPORTANT]
> Při nasazování aplikací Win32 pomocí instalačního souboru s příponou. msi (zabaleného v souboru. intunewin pomocí nástroje pro přípravu obsahu) zvažte použití [rozšíření pro správu služby Intune](../apps/intune-management-extension.md). Pokud během registrace automatického pilotního nasazení kombinujete instalaci aplikací Win32 a obchodních aplikací, může instalace aplikace selhat.  

## <a name="select-the-app-type"></a>Vyberte typ aplikace.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace**  >  **všechny aplikace**  >  **Přidat**.
3. V podokně **Vybrat typ aplikace** v části **ostatní** typy aplikací vyberte **obchodní aplikace**.
4. Klikněte na **Vybrat**. Zobrazí se kroky **Přidání aplikace** .

## <a name="step-1---app-information"></a>Krok 1 – informace o aplikaci

### <a name="select-the-app-package-file"></a>Vyberte soubor balíčku aplikace.

1. V podokně **Přidat aplikaci** klikněte na **Vybrat soubor balíčku aplikace**. 
2. V podokně **Soubor balíčku aplikace** vyberte tlačítko Procházet. Pak vyberte instalační soubor Windows s příponou **. msi**, **. appx**nebo **. appxbundle**.
   Zobrazí se podrobnosti o aplikaci.

    > [!NOTE]
    > Mezi přípony souborů pro aplikace pro Windows patří soubory **. msi**, **. appx**, **. appxbundle**, **. msix**a **. msixbundle**. Další informace o **. msix**najdete v tématu [dokumentace Msix](/windows/msix/) a [distribuce aplikací msix](/windows/msix/desktop/managing-your-msix-deployment-enterprise).

3. Až budete hotovi, vyberte **OK** v podokně **soubor balíčku aplikace** a přidejte aplikaci.

### <a name="set-app-information"></a>Nastavení informací o aplikaci

1. Na stránce **informace o aplikaci** přidejte podrobnosti o aplikaci. V závislosti na zvolené aplikaci můžou být některé hodnoty v tomto podokně vyplněné automaticky:
    - **Název**: Zadejte název aplikace, který se zobrazí na portálu společnosti. Ověřte, že názvy všech používaných aplikací jsou jedinečné. Pokud stejný název aplikace existuje dvakrát, zobrazí se na portálu společnosti jen jedna z aplikací.
    - **Popis**: Zadejte popis aplikace. Popis se zobrazí na portálu společnosti.
    - **Vydavatel**: zadejte název vydavatele aplikace.
    - **Kontext instalace aplikace**: vyberte kontext instalace, který se má přidružit k této aplikaci. Pro aplikace v duálním režimu vyberte požadovaný kontext pro tuto aplikaci. Pro všechny ostatní aplikace je tato možnost předem vybraná na základě balíčku a nedá se změnit.
    - **Ignorovat verzi aplikace**: Nastavte na **Ano**, pokud aplikaci automaticky aktualizuje její vývojář. Tato možnost platí jen pro mobilní aplikace .msi.
    - **Argumenty příkazového řádku**: Volitelně zadejte jakékoli argumenty příkazového řádku, které chcete použít při spuštění souboru .msi.  Příkladem je **/q**. Nepoužívejte příkaz nebo argumenty příkazu msiexec, například **/i** nebo **/x**, jak se používají automaticky. Další informace najdete v tématu [Možnosti příkazového řádku](/windows/desktop/Msi/command-line-options). Pokud. Soubor MSI potřebuje další možnosti příkazového řádku, které se považují za použití [správy aplikací Win32](app-management.md).
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

Aplikace, kterou jste vytvořili, se nyní zobrazí v seznamu aplikací. V tomto seznamu můžete aplikace přiřadit do vybraných skupin. Nápovědu najdete v článku [Přiřazení aplikací do skupin](apps-deploy.md).

## <a name="update-a-line-of-business-app"></a>Aktualizace obchodní aplikace

[!INCLUDE [shared-proc-lob-updateapp](../includes/shared-proc-lob-updateapp.md)]

   > [!NOTE]
   > Aby služba Intune úspěšně nasadila nový soubor APPX do zařízení, musíte zvýšit hodnotu `Version` řetězce v souboru AppxManifest.xml v balíčku appx.

## <a name="configure-a-self-updating-mobile-msi-app-to-ignore-the-version-check-process"></a>Konfigurace automaticky aktualizované mobilní aplikace MSI na ignorování procesu kontroly verzí

Známou automaticky aktualizovanou mobilní aplikaci MSI můžete nakonfigurovat tak, aby ignorovala proces kontroly verzí.

Některé aplikace založené na instalační službě MSI automaticky aktualizuje vývojář aplikace nebo jinou metodu aktualizace. Pro tyto automaticky aktualizované aplikace MSI můžete v podokně **Informace o aplikaci** nakonfigurovat nastavení **Ignorovat verzi aplikace**. Po přepnutí tohoto nastavení na **Ano** nebude Microsoft Intune vynucovat verzi aplikace instalovanou na klientovi Windows.

Tato možnost je užitečná, když chcete předejít konfliktu časování. Ke konfliktu časování může například dojít, když aplikaci automaticky aktualizuje vývojář aplikace a také Intune. Jak vývojář, tak Intune můžou vynucovat verzi aplikace na klientovi Windows, což způsobí konflikt.

## <a name="next-steps"></a>Další kroky

- Aplikace, kterou jste vytvořili, se zobrazí v seznamu aplikací. Teď ji můžete přiřadit do požadovaných skupin. Nápovědu najdete v článku [Přiřazení aplikací do skupin](apps-deploy.md).

- Zjistěte, jakými způsoby můžete monitorovat vlastnosti a přiřazení aplikace. Viz [Postup monitorování informací a přiřazení aplikace](apps-monitor.md).

- Zjistěte více o kontextu své aplikace v Intune. Podívejte [se na Přehled životního cyklu aplikace v Microsoft Intune](app-lifecycle.md).

- Přečtěte si další informace o aplikacích Win32. Viz [Správa aplikací Win32](apps-win32-app-management.md).