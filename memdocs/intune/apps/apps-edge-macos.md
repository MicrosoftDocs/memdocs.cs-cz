---
title: Přidání Microsoft Edge do zařízení macOS pomocí Microsoft Intune
titleSuffix: ''
description: Přečtěte si, jak přidat Microsoft Edge do zařízení macOS pomocí Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/07/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: kellieei
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: c0d9267f989988ae33d56696d424de56a649bca2
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "80900469"
---
# <a name="add-microsoft-edge-to-macos-devices-using-microsoft-intune"></a>Přidání Microsoft Edge do zařízení macOS pomocí Microsoft Intune

Než budete moct nasadit, nakonfigurovat, monitorovat nebo chránit aplikace, musíte je přidat do Intune. Jedním z dostupných [typů aplikací](apps-add.md#app-types-in-microsoft-intune) je Microsoft Edge *verze 77 a novější*. Když vyberete tento typ aplikace v Intune, můžete přiřadit a nainstalovat Microsoft Edge *verze 77 a novější* na zařízení, která spravujete pomocí MacOS. Tento typ aplikace usnadňuje přiřazení Microsoft Edge k macOS zařízením bez nutnosti používat nástroj pro zabalení aplikace macOS. K zajištění bezpečnější a aktuálnosti aplikací je aplikace součástí Microsoft AutoUpdate (MAU).

> [!IMPORTANT]
> Tento typ aplikace nabízí vývojářům a betam kanálům pro macOS. Nasazení je pouze anglické (EN), ale koncoví uživatelé mohou změnit jazyk zobrazení v prohlížeči v části **Nastavení** > **jazyků**. 

> [!NOTE]
> Pro Windows 10 je k dispozici také Microsoft Edge *verze 77 a novější* .

## <a name="prerequisites"></a>Požadavky

- Před instalací Microsoft Edge musí být na zařízení macOS spuštěný macOS 10,12 nebo novější.

## <a name="add-microsoft-edge-to-intune"></a>Přidání Microsoft Edge do Intune

Microsoft Edge verze 77 a novější můžete do Intune přidat pomocí následujících kroků:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > **všechny aplikace** > **Přidat**.
3. V seznamu **Typ aplikace** pod **Microsoft Edge verze 77 a novější**zvolte **MacOS**.

## <a name="configure-app-information"></a>Konfigurace informací o aplikaci
V tomto kroku zadáte informace o tomto nasazení aplikace. Tyto informace vám pomůžou identifikovat aplikaci v Intune a pomáhají uživatelům najít aplikaci na portálu společnosti.

1. Kliknutím na **informace o aplikaci** zobrazíte podokno **informace o aplikaci** .
2. V podokně **informace o aplikaci** zadejte informace o tomto nasazení aplikace. Tyto informace vám pomůžou identifikovat aplikaci v Intune a pomáhají uživatelům najít aplikaci na portálu společnosti.
    - **Název**: zadejte název aplikace, který se zobrazí na portálu společnosti. Ujistěte se, že jsou všechny názvy jedinečné. Pokud stejný název aplikace existuje dvakrát, zobrazí se na portálu společnosti uživatelům jenom jedna z aplikací.
    - **Popis**: Zadejte popis aplikace. Můžete například zobrazit seznam cílových uživatelů v popisu.
    - **Vydavatel**: Jako vydavatel se zobrazí Microsoft.
    - **Kategorie**: volitelně vyberte jednu nebo více předdefinovaných kategorií aplikací nebo kategorii, kterou jste vytvořili. Toto nastavení usnadňuje uživatelům vyhledání aplikace při procházení portálu společnosti.
    - **Zobrazit jako doporučenou aplikaci v portál společnosti**: tuto možnost vyberte, pokud chcete, aby se aplikace zobrazovala na hlavní stránce portálu společnosti, když uživatelé vyhledávají aplikace.
    - **Adresa URL informací**: Volitelně můžete zadat adresu URL webu, který obsahuje informace o této aplikaci. Adresa URL se zobrazí uživatelům na portálu společnosti.
    - **Adresa URL informací o ochraně osobních údajů**: Volitelně zadejte adresu URL webu, který obsahuje informace o ochraně osobních údajů v této aplikaci. Adresa URL se zobrazí uživatelům na portálu společnosti.
    - **Vývojář**: Jako vývojář se zobrazí Microsoft.
    - **Vlastník**: Jako vlastník se zobrazí Microsoft.
    - **Poznámky**: Volitelně zadejte jakékoli poznámky, které chcete k aplikaci přidružit.
3. Vyberte **OK**.

## <a name="configure-microsoft-edge-settings"></a>Konfigurace nastavení Microsoft Edge
V tomto kroku nakonfigurujte možnosti instalace aplikace.

1. V podokně **Přidat aplikaci** vyberte **nastavení aplikace**.
2. V podokně **nastavení aplikace** vyberte v seznamu **kanál** buď **stabilní**, **beta** nebo **vývojové** , abyste určili, ze kterého hraničního kanálu budete aplikaci nasazovat.

    - **Stabilní** kanál je doporučeným kanálem pro široce nasazování v podnikovém prostředí. Aktualizuje se každých šest týdnů, přičemž každá verze zahrnuje vylepšení z verze beta kanálu.
    - **Beta** kanál je nejstabilním prostředím Microsoft Edge Preview a nejlepší volbou pro úplný pilotní nasazení v rámci vaší organizace. V případě hlavních aktualizací každých šest týdnů zahrnuje každá verze tyto učení a vylepšení z vývojového kanálu.
    - **Vývojového** kanálu je připravený na podnikovou zpětnou vazbu ve Windows, Windows serveru a MacOS. Aktualizuje se každý týden a obsahuje nejnovější vylepšení a opravy.

    > [!NOTE]
    > Logo prohlížeče Microsoft Edge se zobrazí spolu s aplikací, když uživatelé procházejí portál společnosti.

3.    Vyberte **OK**.

## <a name="select-scope-tags-optional"></a>Vybrat značky oboru (volitelné)
Pomocí značek Scope můžete určit, kdo může v Intune zobrazit informace o klientské aplikaci. Úplné podrobnosti o značkách oboru najdete v tématu použití značek řízení přístupu na základě role a rozsahu pro distribuci IT.
1.    Vyberte **obor (značky)** > **Přidat**.
2.    Pro vyhledání značek oboru použijte pole **Vybrat** .
3.    Zaškrtněte políčko vedle značek oboru, které chcete této aplikaci přiřadit.
4.    Klikněte na **Vybrat** > **OK**.

## <a name="add-the-app"></a>Přidání aplikace
Po dokončení konfigurace vyberte v podokně **aplikace aplikace** možnost **Přidat** . 

Vytvořená aplikace se zobrazí v seznamu aplikací, kde ji můžete přiřazovat vybraným skupinám. 

> [!NOTE]
> V současné době Apple neposkytuje pro Intune způsob, jak odinstalovat Microsoft Edge na zařízeních macOS.

## <a name="next-steps"></a>Další kroky
- Informace o tom, jak nakonfigurovat Microsoft Edge na zařízeních macOS, najdete v tématu [Konfigurace Microsoft Edge na zařízeních MacOS](https://docs.microsoft.com/deployedge/configure-microsoft-edge-on-mac).
- Informace o zahrnutí a vyloučení přiřazení aplikací ze skupin uživatelů najdete v článku [Zahrnutí a vyloučení přiřazení aplikací](apps-inc-exl-assignments.md).
- [Přiřazení aplikací skupinám](apps-deploy.md)
