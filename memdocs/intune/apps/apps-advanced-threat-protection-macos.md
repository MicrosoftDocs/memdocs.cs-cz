---
title: Přidání ATP Microsoft Defenderu do zařízení macOS pomocí Microsoft Intune
titleSuffix: ''
description: Přečtěte si, jak přidat ATP Microsoft Defenderu do zařízení macOS pomocí Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/21/2020
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
ms.openlocfilehash: 8707b938231e682fe1cd165c207cca8e575950d4
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80324657"
---
# <a name="add-microsoft-defender-atp-to-macos-devices-using-microsoft-intune"></a>Přidání ATP Microsoft Defenderu do zařízení macOS pomocí Microsoft Intune

Než budete moct nasadit, nakonfigurovat, monitorovat nebo chránit aplikace, musíte je přidat do Intune. Jedním z dostupných [typů aplikací](apps-add.md#app-types-in-microsoft-intune) je program Microsoft Defender Advanced Threat Protection (ATP). Když vyberete tento typ aplikace v Intune, můžete přiřadit a nainstalovat ATP Microsoft Defenderu na zařízení, která spravujete pomocí macOS. Tento typ aplikace usnadňuje přiřazení ATP programu Microsoft Defender k macOS zařízením bez nutnosti používat nástroj pro zabalení aplikace macOS. K zajištění bezpečnější a aktuálnosti aplikací je aplikace součástí Microsoft AutoUpdate (MAU).

## <a name="prerequisites"></a>Požadavky
- Na zařízení macOS musí být spuštěný macOS 10,13 nebo novější.
- Zařízení macOS musí mít minimálně 650 MB místa na disku.
- Nasaďte rozšíření jádra do Intune. Další informace najdete v tématu [Přidání rozšíření jádra MacOS do Intune](../configuration/kernel-extensions-overview-macos.md).

> [!IMPORTANT]
> Rozšíření jádra se dá automaticky schválit jenom v případě, že se nachází na zařízení před instalací aplikace Microsoft Defender ATP. Jinak se uživatelům zobrazí zpráva "rozšíření systému je blokované" na počítači Mac a musí toto rozšíření schválit tak, že přejde na **Předvolby zabezpečení** nebo **Předvolby systému** > **zabezpečení & ochrany osobních údajů** a potom vyberte **Povolit**. Další informace najdete v tématu [řešení potíží s rozšířením jádra v programu Microsoft Defender ATP pro Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/mac-support-kext).

## <a name="add-microsoft-defender-atp-to-intune"></a>Přidání ATP Microsoft Defenderu do Intune
Do Intune můžete přidat ATP programu Microsoft Defender pomocí následujících kroků:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > **všechny aplikace** > **Přidat**.
3. V seznamu **Typ aplikace** v oblasti **ATP v programu Microsoft Defender**vyberte možnost **MacOS**.

## <a name="configure-app-information"></a>Konfigurace informací o aplikaci
V tomto kroku zadáte informace o tomto nasazení aplikace. Tyto informace vám pomůžou identifikovat aplikaci v Intune a pomáhají uživatelům najít aplikaci na portálu společnosti.

1. Kliknutím na **informace o aplikaci** zobrazíte podokno **informace o aplikaci** .
2. V podokně **informace o aplikaci** zadejte informace o tomto nasazení aplikace. Tyto informace vám pomůžou identifikovat aplikaci v Intune a pomáhají uživatelům najít aplikaci na portálu společnosti.
    - **Název**: zadejte název aplikace, který se zobrazí na portálu společnosti. Ujistěte se, že jsou všechny názvy jedinečné. Pokud stejný název aplikace existuje dvakrát, zobrazí se na portálu společnosti uživatelům jenom jedna z aplikací.
    - **Popis**: Zadejte popis aplikace. Můžete například zobrazit seznam cílových uživatelů v popisu.
    - **Vydavatel**: Jako vydavatel se zobrazí Microsoft.
    - **Kategorie**: Můžete vybrat jednu nebo několik předdefinovaných kategorií nebo kategorii, kterou jste vytvořili. Toto nastavení usnadňuje uživatelům vyhledání aplikace při procházení portálu společnosti.
    - **Zobrazit jako doporučenou aplikaci v portál společnosti**: tuto možnost vyberte, pokud chcete, aby se aplikace zobrazovala na hlavní stránce portálu společnosti, když uživatelé vyhledávají aplikace.
    - **Adresa URL informací**: Volitelně můžete zadat adresu URL webu, který obsahuje informace o této aplikaci. Adresa URL se zobrazí uživatelům na portálu společnosti.
    - **Adresa URL informací o ochraně osobních údajů**: Volitelně zadejte adresu URL webu, který obsahuje informace o ochraně osobních údajů v této aplikaci. Adresa URL se zobrazí uživatelům na portálu společnosti.
    - **Vývojář**: Jako vývojář se zobrazí Microsoft.
    - **Vlastník**: Jako vlastník se zobrazí Microsoft.
    - **Poznámky**: Volitelně zadejte jakékoli poznámky, které chcete k aplikaci přidružit.
3. Vyberte **OK**.

## <a name="select-scope-tags-optional"></a>Vybrat značky oboru (volitelné)
Pomocí značek Scope můžete určit, kdo může v Intune zobrazit informace o klientské aplikaci. Úplné podrobnosti o značkách oboru najdete v tématu použití značek řízení přístupu na základě role a rozsahu pro distribuci IT.
1.    Vyberte **obor (značky)**  > **Přidat**.
2.    Pro vyhledání značek oboru použijte pole **Vybrat** .
3.    Zaškrtněte políčko vedle značek oboru, které chcete této aplikaci přiřadit.
4.    Klikněte na **vybrat** > **OK**.

## <a name="add-the-app"></a>Přidání aplikace
Po dokončení konfigurace vyberte v podokně **aplikace aplikace** možnost **Přidat** . 

Vytvořená aplikace se zobrazí v seznamu aplikací, kde ji můžete přiřazovat vybraným skupinám. 

> [!NOTE]
> V současné době Apple neposkytuje pro Intune způsob, jak odinstalovat Microsoft Defender ATP na zařízeních macOS.

## <a name="next-steps"></a>Další kroky
- Informace o tom, jak nakonfigurovat Microsoft Defender ATP na zařízeních macOS, najdete v tématu [Konfigurace ATP programu Microsoft Defender na zařízeních MacOS](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/mac-preferences).
- Informace o zahrnutí a vyloučení přiřazení aplikací ze skupin uživatelů najdete v článku [Zahrnutí a vyloučení přiřazení aplikací](apps-inc-exl-assignments.md).
- [Přiřazení aplikací skupinám](apps-deploy.md)

