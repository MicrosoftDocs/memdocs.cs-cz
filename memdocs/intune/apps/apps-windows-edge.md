---
title: Přidejte Microsoft Edge pro Windows 10 a Microsoft Intune
titleSuffix: ''
description: Přečtěte si o přidání Microsoft Edge pro Windows k Microsoft Intune.
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
ms.openlocfilehash: 64cb05d6e031cfe08789d6b7c923d9e489d0e433
ms.sourcegitcommit: 0e62655fef7afa7b034ac11d5f31a2a48bf758cb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/29/2020
ms.locfileid: "82254312"
---
# <a name="add-microsoft-edge-for-windows-10-to-microsoft-intune"></a>Přidejte Microsoft Edge pro Windows 10 a Microsoft Intune

Než budete moct nasadit, nakonfigurovat, monitorovat nebo chránit aplikace, musíte je přidat do Intune. Jedním z dostupných [typů aplikací](apps-add.md#app-types-in-microsoft-intune) je Microsoft Edge *verze 77 a novější*. Když vyberete tento typ aplikace v Intune, můžete přiřadit a nainstalovat Microsoft Edge *verze 77 a novější* na zařízení, která spravujete, na kterých běží Windows 10.

> [!IMPORTANT]
> Tento typ aplikace nabízí stabilní, beta a vývojové kanály pro Windows 10. Nasazení je pouze anglické (EN), ale koncoví uživatelé mohou změnit jazyk zobrazení v prohlížeči v části **Nastavení** > **jazyků**. Microsoft Edge je aplikace Win32 nainstalovaná v kontextu systému a jako architektury (aplikace x86 v operačním systému x86 a x64 v operačním systému x64). Intune zjistí všechny existující instalace Microsoft Edge. Pokud je nainstalován v uživatelském kontextu, bude instalace systému přepsána. Pokud je nainstalován v kontextu systému, je nahlášena úspěch instalace. Automatické aktualizace Microsoft Edge jsou navíc ve výchozím nastavení **zapnuté** .

> [!NOTE]
> Pro macOS je k dispozici také Microsoft Edge *verze 77 a novější* .
>
> Nemůžete použít integrované nasazení aplikace Microsoft Edge pro počítače připojení k síti na pracovišti. Integrované nasazení aplikací vyžaduje rozšíření pro správu Intune, které existuje jenom pro zařízení připojená k AAD. Verzi Microsoft Edge *77 a novější* můžete nasadit pomocí souboru *. msi* nahraného do **aplikací**. Přečtěte si téma [Přidání obchodní aplikace pro Windows do Microsoft Intune](lob-apps-windows.md).

## <a name="prerequisites"></a>Požadavky

- Windows 10 verze 1709 nebo novější.
- Všechny předinstalované verze Microsoft Edge *verze 77 a novější* pro všechny kanály v uživatelském kontextu budou přepsány s hranou nainstalovanými v kontextu systému.

## <a name="configure-the-app-in-intune"></a>Konfigurace aplikace v Intune

Microsoft Edge verze 77 a novější můžete do Intune přidat pomocí následujících kroků:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > **všechny aplikace** > **Přidat**.
3. V seznamu **Typ aplikace** pod **Microsoft Edge verze 77 a novější**vyberte **Windows 10**.

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

## <a name="configure-app-settings"></a>Konfigurace nastavení aplikace
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
Po dokončení konfigurace aplikace vyberte v podokně **aplikace aplikace** možnost **Přidat** . 

Vytvořená aplikace se zobrazí v seznamu aplikací, kde ji můžete přiřazovat vybraným skupinám. 

> [!NOTE]
> Pokud zrušíte přiřazení Microsoft Edge, v tuto chvíli zůstane v zařízení.

## <a name="uninstall-the-app"></a>Odinstalace aplikace

Pokud potřebujete odinstalovat Microsoft Edge ze zařízení uživatele, použijte následující postup.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > **všechny aplikace** > *Microsoft Edge* aplikace > **přiřazení** > **Přidat skupinu**.
3. V podokně **Přidat skupinu** vyberte **odinstalovat**.

    > [!NOTE]
    > Aplikace se odinstaluje ze zařízení ve vybraných skupinách, pokud Intune předtím instaloval aplikaci do zařízení prostřednictvím **dostupného pro zaregistrovaná zařízení** nebo **požadované** přiřazení pomocí stejného nasazení.
4. Vyberte možnost **zahrnuté skupiny** a vyberte skupiny uživatelů, na které se vztahuje přiřazení této aplikace.
5. Vyberte skupiny, u kterých chcete použít přiřazení odinstalace.
6. V podokně **Vybrat skupiny** klikněte na **Vybrat** .
7. Nastavte přiřazení kliknutím na **OK** v podokně **přiřazení** .
8. Pokud se rozhodnete některé skupiny uživatelů vyloučit, aby nebyly přiřazením aplikace ovlivněné, klikněte na **Vyloučit skupiny**.
9. Pokud jste se rozhodli některé skupiny vyloučit, ve **Vybrat skupiny** zvolte **Vybrat**.
10. V podokně **Přidat skupinu** vyberte **OK** .
11. V podokně **přiřazení** aplikace vyberte **Uložit** .

> [!IMPORTANT]
> Aby se aplikace úspěšně odinstalovala, nezapomeňte odebrat členy nebo přiřazení skupiny pro instalaci, než je přiřadíte k odinstalování. Pokud je skupina přiřazena k instalaci aplikace i k odinstalaci aplikace, aplikace zůstane a nebude odebrána.

## <a name="troubleshooting"></a>Řešení potíží
**Microsoft Edge verze 77 a novější pro Windows 10:**<br>
Intune používá rozšíření pro správu Intune ke stažení a nasazení instalačního programu Microsoft Edge na přiřazená zařízení s Windows 10 a pak sdělí nastavení nasazení k instalačnímu programu Microsoft Edge, který stáhne a nainstaluje prohlížeč Microsoft Edge přímo ze sítě CDN. Odkažte na [požadavky pro rozšíření pro správu Intune](intune-management-extension.md#prerequisites)a osvědčené postupy, které jsou uvedené v části přístup ke službě Azure Update a CDN, aby bylo zajištěno, že konfigurace sítě umožní přístup k těmto umístěním pro zařízení s Windows 10. Chcete-li kromě toho dovolit přístup k instalačním souborům ze sítě CDN pro instalaci prohlížeče, je nutné povolený přístup k koncovým bodům web Windows Update. Další informace najdete v tématu [Správa koncových bodů připojení pro Windows 10, verze 1809 – web Windows Update](https://docs.microsoft.com/windows/privacy/manage-windows-1809-endpoints#windows-update) a [koncových bodů sítě pro Microsoft Intune](../fundamentals/intune-endpoints.md).

## <a name="next-steps"></a>Další kroky
- [Přiřazení aplikací skupinám](apps-deploy.md)
