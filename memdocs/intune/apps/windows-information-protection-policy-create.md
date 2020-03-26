---
title: Zásady ochrany aplikací pro Windows Information Protection (NV)
titleSuffix: Microsoft Intune
description: Vytvoření a nasazení zásad Windows Information Protection (NV) pomocí Microsoft Intune
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/25/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 4e3627bd-a9fd-49bc-b95e-9b7532f0ed55
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 88e26a023b745e96926b9611d7bcab41faac261c
ms.sourcegitcommit: fe7484e86ec8a109fa5f54fe9cceef8aac94bd9f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/26/2020
ms.locfileid: "80274723"
---
# <a name="create-and-deploy-windows-information-protection-wip-policy-with-intune"></a>Vytvoření a nasazení zásad Windows Information Protection (NV) pomocí Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Zásady pro Windows Information Protection (nedokončené výroby) s aplikacemi pro Windows 10 můžete použít k ochraně aplikací bez registrace zařízení.

## <a name="before-you-begin"></a>Před zahájením

Musíte porozumět několika konceptům při přidání zásady WIP:

### <a name="list-of-allowed-and-exempt-apps"></a>Seznamy povolených aplikací a aplikací s výjimkou

- **Chráněné aplikace**: Jedná se o aplikace, které musí tuto zásadu dodržovat.

- **Aplikace s výjimkou:** Tyto aplikace mají z této zásady výjimku a můžou k podnikovým datům přistupovat bez omezení.

### <a name="types-of-apps"></a>Typy aplikací

- **Doporučené aplikace:** Předvyplněný seznam aplikací (většinou Microsoft Office), které můžete snadno importovat do zásady.
- **Aplikace pro Store:** Do zásad můžete přidat libovolnou aplikaci z Microsoft Storu.
- **Desktopové aplikace Windows:** Do zásad můžete přidat libovolné tradiční desktopové aplikace Windows (např. soubory typu exe nebo dll).

## <a name="prerequisites"></a>Požadavky

Než budete moct vytvořit zásady nedokončené výroby, musíte nakonfigurovat poskytovatele MAM. Přečtěte si další informace o tom, [jak nakonfigurovat poskytovatele MAM u Intune](app-protection-policies-configure-windows-10.md).  

> [!IMPORTANT]
> WIP nepodporuje víc identit. Vždy může existovat jenom jedna spravovaná identita. Další informace o možnostech a omezeních nedokončené výroby najdete v tématu [Ochrana podnikových dat pomocí Information Protection Windows (NV)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip).

Navíc musíte mít následující licenci a aktualizaci:

- Licence [Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium)
- [Windows Creators Update](https://blogs.windows.com/windowsexperience/2017/04/11/how-to-get-the-windows-10-creators-update/#o61bC2PdrHslHG5J.97)





## <a name="to-add-a-wip-policy"></a>Přidání zásady WIP

Pokud už máte v organizaci nastavenou službu Intune, můžete vytvořit zásadu specifickou pro WIP.

> [!TIP]  
> Související informace o vytváření zásad WIP pro Intune, včetně dostupných nastavení a postupů jejich konfigurace, najdete v tématu o [vytvoření zásad WIP (Windows Information Protection) s MAM pomocí webu Azure Portal pro Microsoft Intune](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-mam-intune-azure) v knihovně dokumentace k zabezpečení systému Windows. 


1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > **zásady ochrany aplikací** > **vytvořit zásadu**.
3. Přidejte následující hodnoty:
    - **Název:** Zadejte název nové zásady (povinné).
    - **Popis:** Volitelně zadejte popis.
    - **Platforma:** Jako podporovanou platformu pro vaši zásadu nedokončené výroby vyberte **Windows 10** .
    - **Stav registrace:** Jako stav registrace pro vaši zásadu zvolte **Bez registrace**.
4. Zvolte **Vytvořit**. Zásada se vytvoří a zobrazí se v tabulce v podokně **Zásady ochrany aplikací** .

## <a name="to-add-recommended-apps-to-your-protected-apps-list"></a>Přidání doporučených aplikací do seznamu chráněných aplikací

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > **Zásady ochrany aplikací**.
3. V podokně **Zásady ochrany aplikací** vyberte zásadu, kterou chcete upravit. Zobrazí se podokno **Intune App Protection** .
4. V podokně **Intune App Protection** vyberte **chráněné aplikace** . Otevře se podokno **chráněné aplikace** , ve kterém se zobrazí všechny aplikace, které už jsou v seznamu pro tuto zásadu ochrany aplikací uvedené.
5. Vyberte **Přidat aplikace**. Informace v části **Přidat aplikace** zobrazí filtrovaný seznam aplikací. Seznam v horní části podokna vám umožní změnit filtr seznamu.
6. Otevřete každou aplikaci, které chcete povolit přístup k podnikovým datům.
7. Klikněte na tlačítko **OK**. V podokně **chráněné aplikace** se aktualizuje zobrazení všech vybraných aplikací.
8. Klikněte na **Uložit**.

## <a name="add-a-store-app-to-your-protected-apps-list"></a>Přidání aplikace ze Storu do seznamu chráněných aplikací

**Přidání aplikace ze Storu**

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > **Zásady ochrany aplikací**.
3. V podokně **Zásady ochrany aplikací** vyberte zásadu, kterou chcete upravit. Zobrazí se podokno **Intune App Protection** .
4. V podokně **Intune App Protection** vyberte **chráněné aplikace** . Otevře se podokno **chráněné aplikace** , ve kterém se zobrazí všechny aplikace, které už jsou v seznamu pro tuto zásadu ochrany aplikací uvedené.
5. Vyberte **Přidat aplikace**. Informace v části **Přidat aplikace** zobrazí filtrovaný seznam aplikací. Seznam v horní části podokna vám umožní změnit filtr seznamu.
6. Ze seznamu vyberte **Aplikace pro Store**.
7. Zadejte hodnoty pro **Název**, **Vydavatel**, **Název produktu** a **Akce**. Nezapomeňte nastavit hodnotu **Akce** na **Povolit**, aby měla aplikace přístup k podnikovým datům.
9. Klikněte na tlačítko **OK**. V podokně **chráněné aplikace** se aktualizuje zobrazení všech vybraných aplikací.
10. Klikněte na **Uložit**.

## <a name="add-a-desktop-app-to-your-protected-apps-list"></a>Přidání desktopové aplikace do seznamu chráněných aplikací

**Přidání desktopové aplikace**
1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > **Zásady ochrany aplikací**.
3. V podokně **Zásady ochrany aplikací** vyberte zásadu, kterou chcete upravit. Zobrazí se podokno **Intune App Protection** .
4. V podokně **Intune App Protection** vyberte **chráněné aplikace** . Otevře se podokno **chráněné aplikace** , ve kterém se zobrazí všechny aplikace, které už jsou v seznamu pro tuto zásadu ochrany aplikací uvedené.
5. Vyberte **Přidat aplikace**. Informace v části **Přidat aplikace** zobrazí filtrovaný seznam aplikací. Seznam v horní části podokna vám umožní změnit filtr seznamu.
6. Ze seznamu vyberte **Desktopové aplikace**.
7. Zadejte hodnoty pro **Název**, **Vydavatel**, **Název produktu**, **Soubor**, **Minimální verze**, **Maximální verze** a **Akce**. Nezapomeňte nastavit hodnotu **Akce** na **Povolit**, aby měla aplikace přístup k podnikovým datům.
9. Klikněte na tlačítko **OK**. V podokně **chráněné aplikace** se aktualizuje zobrazení všech vybraných aplikací.
10. Klikněte na **Uložit**.

## <a name="wip-learning"></a>Kurzy k WIP
Po přidání aplikací, které chcete chránit pomocí WIP, je potřeba použít režim ochrany prostřednictvím **Kurzů k WIP**.

### <a name="before-you-begin"></a>Před zahájením

Kurzy k WIP jsou sestava umožňující monitorovat vaše aplikace podporující WIP a neznámé aplikace v rámci WIP. Neznámé aplikace jsou aplikace, které nenasadilo IT oddělení vaší organizace. Můžete je ze sestavy vyexportovat a přidat do zásad WIP. Zabráníte tak přerušení produktivity po dobu, než vynutíte WIP v režimu Blokovat.

<!-- 1631908 -->
Kromě zobrazování informací o aplikacích s podporou WIP můžete zobrazit souhrn zařízení, která sdílí pracovní data s weby. Pomocí těchto informací můžete určit, které weby by se měly přidat do zásad WIP pro skupiny a uživatele. Souhrn zobrazuje adresy URL webů, ke kterým mají přístup aplikace podporující WIP.

Když pracujete s aplikacemi podporujícími WIP a s neznámými aplikacemi v rámci WIP, doporučujeme začít s režimem **Tiché** nebo **Povolit potlačení** a u malé skupiny ověřit, jestli máte v seznamu chráněných aplikací správné aplikace. Až budete hotovi, můžete režim změnit na konečnou zásadu vynucení **Blokovat**.

### <a name="what-are-the-protection-modes"></a>Co jsou režimy ochrany?

#### <a name="block"></a>Blokování
WIP hledá nepatřičné postupy sdílení dat a zabrání uživateli dokončit akci. K blokovaným akcím může patřit sdílení mezi podnikově nechráněnými aplikacemi a sdílení podnikových dat mezi dalšími lidmi a zařízeními mimo vaši organizaci.

#### <a name="allow-overrides"></a>Povolit potlačení
WIP hledá nepatřičné sdílení dat, a pokud uživatelé udělají něco potenciálně nebezpečného, upozorní je na to. Uživatel ale může v tomto režimu zásady potlačit a data sdílet. Akce se v takovém případě zaznamená do protokolu auditu.

#### <a name="silent"></a>Tiché
WIP běží bez upozorňování s protokolováním nepatřičného sdílení dat. Neblokuje nic, co by v režimu Povolit potlačení vyžadovalo interakci uživatele. Nepovolené akce, jako jsou nepatřičné pokusy aplikací o přístup k síťovému prostředku nebo k datům chráněným pomocí WIP, budou ale zastaveny.

#### <a name="off-not-recommended"></a>Vypnuto (nedoporučuje se)
WIP je vypnuté a nepomáhá chránit nebo auditovat data.

Když WIP vypnete, proběhne pokus o dešifrování všech souborů označených přes WIP na místně připojených jednotkách. Mějte na paměti, že po opětovném zapnutí WIP se předchozí informace o šifrování a zásadách znovu automaticky nepoužijí.

### <a name="add-a-protection-mode"></a>Přidání režimu ochrany

1. V podokně **zásada aplikace** zvolte název zásady a pak zvolte **požadovaná nastavení**.

    ![Snímek obrazovky s podoknem výukového režimu](./media/windows-information-protection-policy-create/learning-mode-sc1.png)

1. Vyberte nastavení a potom zvolte **Uložit**.

### <a name="use-wip-learning"></a>Použití Kurzů k WIP

1. Otevřete portál [Azure Portal](https://portal.azure.com). Zvolte **Všechny služby**. Do filtru textového pole zadejte **Intune**.

3. Vyberte **Intune** > **aplikace**.

4. Zvolte **Stav ochrany aplikace** > **Sestavy** > **Kurz k Windows Information Protection**.  

    Jakmile se tyto aplikace objeví v sestavě protokolování Kurzy k WIP, můžete je přidat do zásad ochrany aplikací.

## <a name="allow-windows-search-indexer-to-search-encrypted-items"></a>Povolit Windows Search Indexeru prohledávat šifrované položky
Tato zásada povolí nebo zakáže indexování položek. Souvisí s Windows Search Indexerem a určuje, jestli se mají indexovat šifrované položky, třeba chráněné soubory Windows Information Protection (WIP).

Tato zásada ochrany aplikací se nachází v zásadách Windows Information Protection v části **Upřesnit nastavení**. Zásady ochrany aplikací musí být nastavené pro platformu *Windows 10* a možnost **Stav registrace** musí být nastavená na hodnotu **S registrací**.

Pokud je tato zásada povolená, chráněné položky WIP se indexují a metadata o nich se ukládají do nešifrovaného umístění. Součástí metadat jsou takové položky jako cesta k souboru a datum změny.

Pokud je tato zásada zakázaná, chráněné položky WIP se neindexují a ve výsledcích v Cortaně nebo v Průzkumníkovi souborů se nezobrazují. Pokud se v zařízení nachází mnoho souborů médií chráněných WIP, může to mít také dopad na výkon fotografií a aplikací Groove.

## <a name="add-encrypted-file-extensions"></a>Přidat přípony šifrovaných souborů

Kromě nastavení možnosti **Povolit Windows Search Indexeru prohledávat šifrované položky** můžete zadat seznam přípon souborů. Při kopírování ze sdílené složky SMB (Server Message Block) v rámci hranic firmy definovaných seznamem síťových umístění se soubory s těmito příponami budou šifrovat. Když se tato zásada nezadá, použije se stávající chování automatického šifrování. Pokud se tato zásada nakonfiguruje, budou se šifrovat jenom soubory, které mají přípony uvedené v seznamu.

## <a name="deploy-your-wip-app-protection-policy"></a>Nasazení zásady ochrany aplikací WIP

> [!IMPORTANT]
> Následující informace platí pro WIP bez registrace zařízení.

<!---not sure why you need the Important note. Isn't this what the topic is about? app protection w/o enrollment?--->

Když jste vytvořili zásadu ochrany aplikací WIP, potřebujete ji nasadit ve vaší organizaci s použitím MAM.

1. V podokně **zásady aplikace** vyberte nově vytvořenou zásadu ochrany aplikací, vyberte **skupiny uživatelů** > **Přidat skupinu uživatelů**.

    Seznam skupin uživatelů, ze kterých se ve vašem Azure Active Directory skládá všechny skupiny zabezpečení, se otevře v podokně **Přidat skupinu uživatelů** .

2. Zvolte skupinu, u které chcete zásadu použít, a kliknutím na **Vybrat** zásadu nasaďte.

## <a name="next-steps"></a>Další kroky

Další informace o službě Windows Information Protection najdete v tématu [Ochrana podnikových dat pomocí služby Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip).
