---
title: Návod – vytvoření šablony pro správu v Microsoft Intune – Azure | Microsoft Docs
description: Tento kurz nebo návod používá Microsoft Intune ke konfiguraci šablon Office, Windows a Microsoft Edge ADMX na Windows 10 a novějších zařízeních.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/31/2020
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 41a2dce895761053e482fe029e4599819a099ac6
ms.sourcegitcommit: 0e62655fef7afa7b034ac11d5f31a2a48bf758cb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/29/2020
ms.locfileid: "82254856"
---
# <a name="tutorial-use-the-cloud-to-configure-group-policy-on-windows-10-devices-with-admx-templates-and-microsoft-intune"></a>Kurz: použití cloudu ke konfiguraci zásad skupiny na zařízeních s Windows 10 s šablonami ADMX a Microsoft Intune

> [!NOTE]
> Tento kurz byl vytvořen jako technický workshop pro Microsoft Ignite. Obsahuje více požadavků než typických kurzů, které porovnávají používání a konfiguraci zásad ADMX v Intune a místním prostředí.

Šablony pro správu zásad skupiny, označované taky jako šablony ADMX, obsahují nastavení, která můžete nakonfigurovat na zařízeních s Windows 10, včetně počítačů. Nastavení šablony ADMX jsou k dispozici pro různé služby. Tato nastavení používá poskytovatelé správy mobilních zařízení (MDM), včetně Microsoft Intune. Můžete například zapnout návrhy designu v aplikaci PowerPoint, nastavit domovskou stránku v Microsoft Edge, blokovat ovládací prvky ActiveX v aplikaci Internet Explorer a další.

Šablony ADMX jsou k dispozici pro následující služby:

- **Microsoft Edge**: Stáhněte si [soubor zásad Microsoft Edge](https://www.microsoftedgeinsider.com/en-us/enterprise).
- **Office**: Stáhněte [se na Microsoft 365 aplikace, Office 2019 a Office 2016](https://www.microsoft.com/download/details.aspx?id=49030).
- **Windows**: integrovaný v operačním systému Windows 10.

Další informace o zásadách pro ADMX najdete v tématu [Principy zásad zálohovaných v ADMX](https://docs.microsoft.com/windows/client-management/mdm/understanding-admx-backed-policies).

Tyto šablony jsou integrované pro Microsoft Intune a jsou dostupné jako profily **šablon pro správu** . V tomto profilu nakonfigurujete nastavení, která chcete zahrnout, a potom tento profil přiřadíte k vašim zařízením.

V tomto kurzu provedete následující:

> [!div class="checklist"]
> * Zavedli jsme do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431).
> * Vytváření skupin uživatelů a vytváření skupin zařízení.
> * Porovnejte nastavení v Intune s místními nastaveními ADMX.
> * Vytvořte různé šablony pro správu a nakonfigurujte nastavení, která cílí na různé skupiny.

Na konci tohoto testovacího prostředí budete mít přehled o tom, jak začít používat Intune a Microsoft 365 ke správě uživatelů a nasazovat šablony pro správu.

Tato funkce platí pro:

- Windows 10 verze 1709 a novější

## <a name="prerequisites"></a>Požadavky

- Předplatné Microsoft 365 E3 nebo E5, které zahrnuje Intune a Azure Active Directory (AD) Premium. Pokud nemáte předplatné E3 nebo E5, [zkuste to zdarma](https://docs.microsoft.com/office365/admin/try-or-buy-microsoft-365?view=o365-worldwide).

  Další informace o tom, co se dostanete s různými licencemi Microsoft 365, najdete v tématu věnovaném [transformaci vaší organizace pomocí Microsoft 365](https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans).

- Microsoft Intune je nakonfigurovaný jako **Autorita MDM pro Intune**. Další informace najdete v tématu [Nastavení autority pro správu mobilních zařízení](../fundamentals/mdm-authority-set.md).

  > [!div class="mx-imgBorder"]
  > ![Nastavte autoritu MDM tak, aby ve stavu tenanta Microsoft Intune.](./media/tutorial-walkthrough-administrative-templates/tenant-status.png)

- Místní řadič domény služby Active Directory (DC):

  1. Zkopírujte následující šablony Office a Microsoft Edge do [centrálního úložiště (složka SYSVOL)](https://support.microsoft.com/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra):

      - [Šablony pro správu Office](https://www.microsoft.com/download/details.aspx?id=49030)
      - [Šablony pro správu Microsoft Edge > soubor zásad](https://www.microsoftedgeinsider.com/en-us/enterprise)

  2. Vytvořte zásady skupiny, abyste tyto šablony nastavili na počítač s Windows 10 Enterprise Administrator ve stejné doméně jako řadič domény. V tomto kurzu:

      - Zásady skupiny, které jsme vytvořili pomocí těchto šablon, se nazývají **OfficeandEdge**. Tento název se zobrazí v obrázcích.
      - Počítač správce Windows 10 Enterprise, který používáme, se označuje jako **počítač pro správu**.

      V některých organizacích má správce domény dva účty:  
        - Typický pracovní účet domény
        - Jiný účet správce domény, který se používá jenom pro úlohy správce domény, třeba pro zásady skupiny

      Účelem tohoto **počítače správce** je, aby se správci přihlásili pomocí účtu správce domény a měli přístup k nástrojům navrženým pro správu zásad skupiny.

- V tomto **počítači pro správu**:

  - Přihlaste se pomocí účtu správce domény.

  - Instalace **nástrojů pro správu RSAT: Zásady skupiny Management**:

    1. Otevřete okno **Nastavení** **aplikace >** > **volitelné funkce** > **Přidat funkci**.
    2.  > Vyberte **RSAT: Instalace nástrojů pro správu Zásady skupiny**.**Install**

        Počkejte, než systém Windows nainstaluje funkci. Po dokončení se zobrazí v aplikaci **Nástroje pro správu systému Windows** .

        > [!div class="mx-imgBorder"]
        > ![Aplikace nástrojů pro správu systému Windows, včetně aplikace pro správu Zásady skupiny](./media/tutorial-walkthrough-administrative-templates/windows-administrative-tools-app.png)

  - Ujistěte se, že máte oprávnění k přístupu k Internetu a oprávnění správce k předplatnému Microsoft 365, které zahrnuje centrum pro správu Správce koncových bodů.

## <a name="open-the-endpoint-manager-admin-center"></a>Otevřete centrum pro správu Správce koncových bodů.

1. Otevřete webový prohlížeč Chromu, například Microsoft Edge verze 77 nebo novější.
2. Přejít do [centra pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). Přihlaste se s následujícím účtem:

    **Uživatel**: zadejte účet správce předplatného tenanta Microsoft 365.  
    **Heslo**: zadejte jeho heslo.

Toto centrum pro správu se zaměřuje na správu zařízení a zahrnuje služby Azure, jako je Azure AD a Intune. Možná neuvidíte **Azure Active Directory** a branding **Intune** , ale budete je používat.

Centrum pro správu Správce koncových bodů můžete otevřít taky z [centra pro správu Microsoft 365](https://admin.microsoft.com):

1. Přejít na [https://admin.microsoft.com](https://admin.microsoft.com).
2. Přihlaste se pomocí účtu správce předplatného Microsoft 365 tenanta.
3. V **části centra pro správu**vyberte **všechna centra** > **pro správu koncový bod správa koncových bodů**. Otevře se centrum pro správu Správce koncových bodů.

    > [!div class="mx-imgBorder"]
    > ![Zobrazit všechna centra pro správu v centru pro správu Microsoft 365](./media/tutorial-walkthrough-administrative-templates/microsoft365-admin-centers.png)

## <a name="create-groups-and-add-users"></a>Vytváření skupin a přidávání uživatelů

Místní zásady se používají v LSDOU pořadí – místní, lokalita, doména a organizační jednotka (OU). V této hierarchii zásady organizační jednotky přepíšou místní zásady, zásady domény přepíšou zásady lokality atd.

V Intune se zásady aplikují na uživatele a skupiny, které vytvoříte. Neexistuje hierarchie. Pokud dvě zásady aktualizují stejné nastavení, pak se toto nastavení zobrazí jako konflikt. Pokud jsou v konfliktu dvě zásady dodržování předpisů, uplatní se nejvíce omezující zásada. Pokud dojde ke konfliktu dvou konfiguračních profilů, nastavení se nepoužije. Další informace najdete v tématu [běžné otázky, problémy a řešení pro zásady a profily zařízení](device-profile-troubleshoot.md#if-multiple-policies-are-assigned-to-the-same-user-or-device-how-do-i-know-which-settings-gets-applied).

V těchto dalších krocích vytvoříte skupiny zabezpečení a do těchto skupin přidáte uživatele. Uživatele můžete přidat do více skupin. Například je běžné, že uživatel má více zařízení, jako je například Surface pro práci, a mobilní zařízení s Androidem pro osobní. A je normální pro uživatele, kteří mají přístup k prostředkům organizace z těchto více zařízení.

1. V centru pro správu Správce koncových bodů vyberte **skupiny** > **Nová skupina**.

2. Zadejte následující nastavení:

    - **Typ skupiny**: vyberte **zabezpečení**.
    - **Název skupiny**: zadejte **všechna zařízení se systémem Windows 10 student**.
    - **Typ členství**: vyberte **přiřazeno**.

3. Vyberte **členy**a přidejte některá zařízení.

    Přidávání zařízení je volitelné. Cílem je postup vytváření skupin a pochopení způsobu přidávání zařízení. Pokud tento kurz používáte v produkčním prostředí, měli byste vědět, co děláte.

4. **Výběrem** > **vytvořit** uložte změny.

    Nezobrazuje se vaše skupina? Vyberte **aktualizovat**.

5. Vyberte **Nová skupina**a zadejte následující nastavení:

    - **Typ skupiny**: vyberte **zabezpečení**.
    - **Název skupiny**: zadejte **všechna zařízení se systémem Windows**.
    - **Typ členství**: vyberte **dynamické zařízení**.
    - **Dynamické členy zařízení**: vyberte **Přidat dynamický dotaz**a nakonfigurujte dotaz:

        - **Vlastnost**: vyberte **deviceOSType**.
        - **Operátor**: vyberte **Equals**.
        - **Hodnota**: zadejte **Windows**.

        1. Vyberte **přidat výraz**. Výraz je zobrazen v **syntaxi pravidla**:

            > [!div class="mx-imgBorder"]
            > ![Vytvoření dynamického dotazu a Přidání výrazu v Microsoft Intune šabloně pro správu](./media/tutorial-walkthrough-administrative-templates/dynamic-group-query.png)

            Když uživatelé nebo zařízení splňují zadaná kritéria, automaticky se přidají do dynamických skupin. V tomto příkladu se zařízení automaticky přidají do této skupiny, když je operační systém Windows. Pokud tento kurz používáte v produkčním prostředí, buďte opatrní. Cílem je postupovat při vytváření dynamických skupin.

        2. **Uložením** > uložte změny, které jste**vytvořili** .

6. Vytvořte skupinu **všichni učitelé** s následujícím nastavením:

    - **Typ skupiny**: vyberte **zabezpečení**.
    - **Název skupiny**: zadejte **všechny učitele**.
    - **Typ členství**: vyberte možnost **dynamický uživatel**.
    - **Dynamické členy uživatele**: vyberte **Přidat dynamický dotaz**a nakonfigurujte dotaz:

      - **Vlastnost**: vyberte **oddělení**.
      - **Operátor**: vyberte **Equals**.
      - **Hodnota**: zadejte **učitele**.

        1. Vyberte **přidat výraz**. Váš výraz je zobrazen v **syntaxi pravidla**.

            Když uživatelé nebo zařízení splňují zadaná kritéria, automaticky se přidají do dynamických skupin. V tomto příkladu se uživatelé automaticky přidají do této skupiny, když jsou jejich oddělení učitelé. Po přidání uživatelů do vaší organizace můžete zadat oddělení a další vlastnosti. Pokud tento kurz používáte v produkčním prostředí, buďte opatrní. Cílem je postupovat při vytváření dynamických skupin.

        2. **Uložením** > uložte změny, které jste**vytvořili** .

### <a name="talking-points"></a>Body konverzace

- Dynamické skupiny jsou funkce v Azure AD Premium. Pokud nemáte Azure AD Premium, máte licenci jenom k vytváření přiřazených skupin. Další informace o dynamických skupinách najdete v těchto tématech:

  - [Dynamické členství ve skupině v Azure Active Directory (část 1)](https://blogs.technet.microsoft.com/pauljones/2017/08/28/dynamic-group-membership-in-azure-active-directory-part-1/)
  - [Dynamické členství ve skupině v Azure Active Directory (část 2)](https://blogs.technet.microsoft.com/pauljones/2017/08/29/dynamic-group-membership-in-azure-active-directory-part-2/)

- Azure AD Premium zahrnuje další služby, které se běžně používají při správě aplikací a zařízení, včetně služby [Multi-Factor Authentication (MFA)](https://docs.microsoft.com/azure/active-directory/authentication/concept-mfa-howitworks) a [podmíněného přístupu](https://docs.microsoft.com/azure/active-directory/conditional-access/overview).

- Mnoho správců žádá o použití skupin uživatelů a kdy použít skupiny zařízení. Nějaké pokyny najdete v tématu [skupiny uživatelů a skupiny zařízení](device-profile-assign.md#user-groups-vs-device-groups).

- Pamatujte, že uživatel může patřit do více skupin. Vezměte v úvahu některé z ostatních dynamických skupin uživatelů a zařízení, které můžete vytvořit, například:

  - Všichni studenti
  - Všechna zařízení s Androidem
  - Všechna zařízení s iOS/iPadOS
  - Marketing
  - Personální oddělení
  - Všichni zaměstnanci Charlotte
  - Všichni zaměstnanci Redmond
  - Západní pobřeží správců IT
  - Správci IT východní pobřeží

Vytvoření uživatelé a skupiny se také zobrazují v [centru pro správu Microsoft 365](https://admin.microsoft.com), v Azure Portal Azure AD v a [Microsoft Intune v Azure Portal](https://go.microsoft.com/fwlink/?linkid=2090973). Můžete vytvářet a spravovat skupiny ve všech oblastech pro předplatné tenanta. **Pokud je vaším cílem Správa zařízení, použijte [Centrum pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)**.

### <a name="review-group-membership"></a>Kontrola členství ve skupinách

1. V centru pro správu Správce koncových bodů vyberte **uživatelé** > vyberte jméno existujícího uživatele.

    > [!div class="mx-imgBorder"]
    > ![V centru pro správu Správce koncových bodů vyberte uživatelé.](./media/tutorial-walkthrough-administrative-templates/select-users-endpoint-manager-admin-center.png)

2. Projděte si některé informace, které můžete přidat nebo změnit. Podívejte se například na vlastnosti, které můžete konfigurovat, jako je například název úlohy, oddělení, město, umístění kanceláře a další. Tyto vlastnosti můžete použít ve svých dynamických dotazech při vytváření dynamických skupin.
3. Pokud chcete zobrazit členství tohoto uživatele, vyberte **skupiny** . Uživatele můžete také odebrat ze skupiny.
4. Výběrem některých z dalších možností zobrazíte další informace a to, co můžete dělat. Podívejte se například na přiřazenou licenci, zařízení uživatele a další.

### <a name="what-did-i-just-do"></a>Co mám dělat?

V centru pro správu Správce koncových bodů jste vytvořili nové skupiny zabezpečení a přidali do těchto skupin existující uživatele a zařízení. Tyto skupiny použijeme v pozdějších krocích tohoto kurzu.

## <a name="create-a-template-in-intune"></a>Vytvoření šablony v Intune

V této části vytvoříme v Intune šablonu pro správu, podíváme se na některá nastavení ve **správě Zásady skupiny**a porovnáte stejné nastavení v Intune. Cílem je Ukázat nastavení v zásadách skupiny a zobrazit stejné nastavení v Intune.

1. V centru pro správu Správce koncových bodů vyberte **zařízení** > **Konfigurace profily** > **vytvořit profil**.
2. Zadejte tyto vlastnosti:

    - **Platforma**: vyberte **Windows 10 a novější**.
    - **Profil**: vyberte **šablony pro správu**.

3. Vyberte **Vytvořit**.
4. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte popisný název profilu. Své profily pojmenujte, abyste je později mohli snadno identifikovat. Například zadejte **šablonu pro správu – zařízení s Windows 10 student**.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.

5. Vyberte **Další**.
6. V **nastavení konfigurace**platí nastavení pro zařízení (**Konfigurace počítače**) a nastavení platí pro uživatele (**Konfigurace uživatele**):

    > [!div class="mx-imgBorder"]
    > ![Použití nastavení šablony ADMX pro uživatele a zařízení ve Správci služby Microsoft Intune Endpoint Manager](./media/tutorial-walkthrough-administrative-templates/administrative-templates-choose-computer-user-configuration.png)

7. Rozbalte položku **Konfigurace** > počítače**Microsoft Edge** > vyberte **nastavení filtru SmartScreen**. Všimněte si cesty k zásadám a všech dostupných nastavení:

    > [!div class="mx-imgBorder"]
    > ![Viz nastavení zásad SmartScreen pro Microsoft Edge v šablonách ADMX v Microsoft Intune](./media/tutorial-walkthrough-administrative-templates/computer-configuration-microsoft-edge-smartscreen-path.png)

8. Do Hledat zadejte **Download (stáhnout**). Všimněte si, že nastavení zásad jsou filtrovaná:

    > [!div class="mx-imgBorder"]
    > ![Filtrování nastavení zásad SmartScreen v Microsoft Edge v Microsoft Intune šabloně ADMX](./media/tutorial-walkthrough-administrative-templates/computer-configuration-microsoft-edge-smartscreen-search-download.png)

### <a name="open-group-policy-management"></a>Otevřít správu Zásady skupiny

V této části uvádíme zásadu v Intune a odpovídající zásady v Editor pro správu zásad skupiny.

#### <a name="compare-a-device-policy"></a>Porovnání zásad zařízení

1. V **počítači pro správu**otevřete aplikaci **Zásady skupiny Management** .

    Tato aplikace se nainstaluje pomocí **nástrojů pro vzdálenou správu serveru: Zásady skupiny nástroje pro správu**, což je volitelná funkce, kterou nainstalujete do systému Windows. [Požadavky](#prerequisites) (v tomto článku) obsahují seznam kroků, které je potřeba nainstalovat.

2. Rozbalte **domény** > vyberte doménu. Vyberte například **contoso.NET**.
3. Klikněte pravým tlačítkem na zásady **OfficeandEdge** > **Upravit**. Otevře se aplikace Editor pro správu zásad skupiny.

    > [!div class="mx-imgBorder"]
    > ![Klikněte pravým tlačítkem na zásady skupiny Office a Microsoft Edge ADMX a vyberte Upravit.](./media/tutorial-walkthrough-administrative-templates/open-group-policy-management.png)

    **OfficeandEdge** je zásada skupiny, která zahrnuje šablony Office a Microsoft Edge ADMX. Tato zásada je popsaná v tématu [požadavky](#prerequisites) (v tomto článku).

4. Rozbalte položku**zásady** >  **Konfigurace** > počítače**šablony pro správu** > **přizpůsobení****ovládacích panelů** > . Všimněte si dostupných nastavení.

    > [!div class="mx-imgBorder"]
    > ![Rozbalte položku Konfigurace počítače v Editor pro správu zásad skupiny a pokračujte na přizpůsobení.](./media/tutorial-walkthrough-administrative-templates/open-group-policy-management-editor-admx-policy.png)

    Poklikejte na **zabránit povolování kamery zamykací obrazovky**a podívejte se na dostupné možnosti:

    > [!div class="mx-imgBorder"]
    > ![Podívejte se na možnosti nastavení konfigurace počítače v zásadách skupiny.](./media/tutorial-walkthrough-administrative-templates/prevent-enabling-lock-screen-camera-admx-policy.png)

5. V centru pro správu Správce koncových bodů můžete přejít na šablonu **správce – šablona zařízení s Windows 10 Students** .
6. Vyberte možnost**přizpůsobení**v**ovládacím panelu** >  **Konfigurace** > počítače. Všimněte si dostupných nastavení:

    > [!div class="mx-imgBorder"]
    > ![Cesta nastavení zásad přizpůsobení v Microsoft Intune](./media/tutorial-walkthrough-administrative-templates/computer-configuration-control-panel-personalization-path.png)

    Typ nastavení je **zařízení**a cesta je **/Control Panel nebo individuální nastavení**. Tato cesta se podobá tomu, co jste se v Editor pro správu zásad skupiny právě viděli. Pokud otevřete nastavení **zabránit povolování kamery zamykací obrazovky** , uvidíte stejné možnosti, které **nejsou nakonfigurované**, **povolené**a **zakázané** , a vidíte v Editor pro správu zásad skupiny.

#### <a name="compare-a-user-policy"></a>Porovnání zásad uživatele

1. V šabloně správce vyberte **Konfigurace** > počítače**všechna nastavení**a vyhledejte **procházení InPrivate**. Všimněte si cesty.

    Proveďte stejnou **konfiguraci uživatele**. Vyberte **všechna nastavení**a vyhledejte **procházení InPrivate**.

2. V **Editor pro správu zásad skupiny**vyhledejte nastavení odpovídajícího uživatele a zařízení:

    - Zařízení: rozbalte**zásady** >  **Konfigurace** > počítače**šablony pro správu** > **součásti** > systému Windows**Ochrana osobních údajů** > pro**Internet Explorer** > **vypnout procházení InPrivate**.
    - Uživatel: rozbalte**zásady** >  **Konfigurace** > uživatelů**šablony pro správu** > **součásti** > systému Windows**Ochrana osobních údajů** > pro**Internet Explorer** > **vypnout procházení InPrivate**.

    > [!div class="mx-imgBorder"]
    > ![Vypnutí procházení InPrivate v Internet Exploreru pomocí šablony ADMX](./media/tutorial-walkthrough-administrative-templates/group-policy-turn-off-inprivate-browsing.png)

> [!TIP]
> Chcete-li zobrazit integrované zásady systému Windows, můžete použít také příkaz GPEdit (**Upravit aplikaci zásad skupiny** ).

#### <a name="compare-an-edge-policy"></a>Porovnání hraničních zásad

1. V centru pro správu Správce koncových bodů můžete přejít na šablonu **správce – šablona zařízení s Windows 10 Students** .
2. Rozbalte položku **Konfigurace** > počítače**Microsoft Edge** > **po spuštění, Domovská stránka a nová karta**. Všimněte si dostupných nastavení.

    Proveďte stejnou **konfiguraci uživatele**.

3. V Editor pro správu zásad skupiny Najděte tato nastavení:

    - Zařízení: rozbalte**zásady** >  **Konfigurace** > počítače**šablony pro správu** > úvodní stránky**Microsoft Edge** > **, Domovská stránka a nová karta**.
    - Uživatel: rozbalte položku**zásady** >  **Konfigurace** > uživatele**šablony pro správu** > **úvodní, domovskou stránku a novou stránku karty** **Microsoft Edge** > .

### <a name="what-did-i-just-do"></a>Co mám dělat?

Vytvořili jste šablonu pro správu v Intune. V této šabloně jsme se vyhledali v některých nastaveních ADMX a prohlédli jsme se se stejnými nastaveními ADMX při správě Zásady skupiny.

## <a name="add-settings-to-the-students-admin-template"></a>Přidat nastavení do šablony pro správce studentů

V této šabloně nakonfigurujeme některá nastavení aplikace Internet Explorer tak, aby byla zamčená zařízení sdílená více studenty.

1. V **šabloně pro správu – zařízení s Windows 10 studenty**, rozbalte položku **Konfigurace počítače**, vyberte **všechna nastavení**a vyhledejte vypnout **procházení InPrivate**:

    > [!div class="mx-imgBorder"]
    > ![Vypnutí zásad zařízení pro procházení InPrivate v šabloně pro správu v Microsoft Intune](./media/tutorial-walkthrough-administrative-templates/turn-off-inprivate-browsing-administrative-template.png)

2. Vyberte nastavení **procházení InPrivate** . V tomto okně si všimněte popisu a hodnot, které můžete nastavit. Tyto možnosti jsou podobné tomu, co vidíte v zásadách skupiny.
3. Kliknutím na možnost **povoleno** > **OK** uložte změny.
4. Také nakonfigurujte následující nastavení aplikace Internet Explorer. Nezapomeňte vybrat **OK** , aby se změny uložily.

    - **Povolení přetahování nebo kopírování a vkládání souborů**
      - **Typ**: zařízení
      - **Cesta**: \Windows Windows\internet Explorer\Internet Control Panel\Security Page\Internet Zone
      - **Hodnota**: zakázáno

    - **Zabránit ignorování chyb certifikátu**
      - **Typ**: zařízení
      - **Cesta**: ovládací panel \Windows Windows\Internet Explorer\Internet
      - **Hodnota**: povoleno

    - **Zakázat změnu nastavení domovské stránky**
      - **Typ**: uživatel
      - **Cesta**: \Windows Windows\Internet Explorer
      - **Hodnota**: povoleno
      - **Domovská stránka**: zadejte adresu URL, například `contoso.com`.

5. Vymažte vyhledávací filtr. Všimněte si, že nastavení, které jste nakonfigurovali, jsou uvedená v horní části:

    > [!div class="mx-imgBorder"]
    > ![Nakonfigurovaná nastavení jsou uvedená v horní části Microsoft Intune](./media/tutorial-walkthrough-administrative-templates/configured-settings-administrative-template.png)

### <a name="assign-your-template"></a>Přiřazení šablony

1. V šabloně vyberte **Další** , dokud se nedostanete k **přiřazení**. Zvolte **Vybrat skupiny, které se mají zahrnout**:

    > [!div class="mx-imgBorder"]
    > ![V seznamu profily konfigurace zařízení v Microsoft Intune vyberte profil šablony pro správu.](./media/tutorial-walkthrough-administrative-templates/filter-administrative-template-device-configuration-profiles-list.png)

2. Zobrazí se seznam existujících uživatelů a skupin. Vyberte skupinu **všechna zařízení s Windows 10 Students** , kterou jste vytvořili dříve, > **Vybrat**.

    Pokud tento kurz používáte v produkčním prostředí, zvažte přidání prázdných skupin. Cílem je postup přiřazení šablony.

3. Vyberte **Další**. V rámci **Revize + vytvořit**vyberte **vytvořit** a uložte změny.

Jakmile se profil uloží, vztahuje se na zařízení při vrácení se změnami pomocí Intune. Pokud jsou zařízení připojená k Internetu, může k ní dojít hned. Další informace o časech aktualizace zásad najdete v tématu [Jak dlouho trvá, než zařízení dostanou zásady, profil nebo aplikaci po jejich přiřazení](device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

Při přiřazování striktních nebo omezujících zásad a profilů se Neblokujte sami. Zvažte vytvoření skupiny, která je vyloučená z vašich zásad a profilů. Nápad je mít přístup k řešení potíží. Monitorujte tuto skupinu, abyste potvrdili, že se používá jako zamýšlená.

### <a name="what-did-i-just-do"></a>Co mám dělat?

V centru pro správu Správce koncových bodů jste vytvořili profil konfigurace zařízení v šabloně pro správu a tento profil jste přiřadili do skupiny, kterou jste vytvořili.

## <a name="create-a-onedrive-template"></a>Vytvoření šablony OneDrivu

V této části vytvoříte v Intune šablonu správce OneDrivu, abyste mohli řídit některá nastavení. Tato konkrétní nastavení se volí, protože je běžně používají organizace.

1. Vytvořte další profil (konfigurace**zařízení** > **profily** > **vytvořit profil**).

2. Zadejte tyto vlastnosti:

    - **Platforma**: vyberte **Windows 10 a novější**.
    - **Profil**: vyberte **šablony pro správu**.

3. Vyberte **Vytvořit**.
4. V části **základy**zadejte následující vlastnosti:

    - **Název**: zadejte **šablonu správce – zásady OneDrivu, které se vztahují na všechny uživatele Windows 10**.
    - **Popis**: Zadejte popis profilu. Toto nastavení není povinné, ale doporučujeme ho zadat.

5. Vyberte **Další**.
6. V **nastavení konfigurace**nakonfigurujte následující nastavení. Nezapomeňte vybrat **OK** , aby se změny uložily.:

    - **Computer configuration** > **Všechna nastavení**konfigurace počítače:
      - **Tiché přihlášení uživatelů do synchronizačního klienta OneDrivu s přihlašovacími údaji Windows**
        - **Typ**: zařízení
        - **Hodnota**: povoleno
      - **Použití souborů OneDrive na vyžádání**
        - **Typ**: zařízení
        - **Hodnota**: povoleno

    - **User configuration** > **Všechna nastavení**konfigurace uživatele:
      - **Zabránit uživatelům v synchronizaci osobních účtů OneDrivu**
        - **Typ**: uživatel
        - **Hodnota**: povoleno

Vaše nastavení vypadá podobně jako u následujících nastavení:

> [!div class="mx-imgBorder"]
> ![Vytvoření šablony pro správu OneDrivu v Microsoft Intune](./media/tutorial-walkthrough-administrative-templates/one-drive-administrative-template.png)

Další informace o nastavení klienta OneDrive najdete v tématu [použití zásady skupiny k řízení nastavení synchronizace klienta OneDrive](https://docs.microsoft.com/onedrive/use-group-policy).

### <a name="assign-your-template"></a>Přiřazení šablony

1. V šabloně vyberte **Další** , dokud se nedostanete k **přiřazení**. Zvolte **Vybrat skupiny, které se mají zahrnout**:
2. Zobrazí se seznam existujících uživatelů a skupin. Vyberte skupinu **všechna zařízení se systémem Windows** , kterou jste vytvořili dříve, > **Vybrat**.

    Pokud tento kurz používáte v produkčním prostředí, zvažte přidání prázdných skupin. Cílem je postup přiřazení šablony.

3. Vyberte **Další**. V rámci **Revize + vytvořit**vyberte **vytvořit** a uložte změny.

V tuto chvíli jste vytvořili některé šablony pro správu a přiřadili je skupinám, které jste vytvořili. Dalším krokem je vytvoření šablony pro správu pomocí prostředí Windows PowerShell a rozhraní Microsoft Graph API pro Intune.

## <a name="optional-create-a-policy-using-powershell-and-graph-api"></a>Volitelné: vytvoření zásady pomocí PowerShellu a Graph API

Tato část používá následující zdroje informací. Tyto prostředky nainstalujeme v této části.

- [Sada Intune PowerShell SDK](https://github.com/microsoft/Intune-PowerShell-SDK)
- [Rozhraní API pro Microsoft Graph pro Intune](https://docs.microsoft.com/graph/api/resources/intune-graph-overview?view=graph-rest-1.0)

1. V **počítači pro správu**otevřete **Windows PowerShell** jako správce:

    1. Do vyhledávacího panelu zadejte **PowerShell**.
    2. Klikněte pravým tlačítkem na **Windows PowerShell** > **Spustit jako správce**.

    > [!div class="mx-imgBorder"]
    > ![Spusťte prostředí Windows PowerShell jako správce.](./media/tutorial-walkthrough-administrative-templates/run-windows-powershell-administrator.png)

2. Získejte a nastavte zásady spouštění.

    1. Napište`get-ExecutionPolicy`

        Zapište, co je nastaveno na, což může být **omezeno**. Po dokončení kurzu ho nastavte zpátky na původní hodnotu.

    2. Napište`Set-ExecutionPolicy -ExecutionPolicy Unrestricted`

    3. Pokud `Y` ho chcete změnit, zadejte.

    Zásady spouštění prostředí PowerShell pomáhají zabránit spouštění škodlivých skriptů. Další informace najdete v tématu [o zásadách spouštění](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_execution_policies).

3. Napište`Install-Module -Name Microsoft.Graph.Intune`

    Zadejte `Y` IF:

    - Výzva k instalaci zprostředkovatele NuGet
    - Výzva k instalaci modulů z nedůvěryhodného úložiště

    Dokončení může trvat několik minut. Po dokončení se zobrazí výzva podobná následujícímu dotazu:

    > [!div class="mx-imgBorder"]
    > ![Windows PowerShell – výzva po instalaci modulu](./media/tutorial-walkthrough-administrative-templates/powershell-prompt.png)

4. Ve webovém prohlížeči přejdete na [https://github.com/Microsoft/Intune-PowerShell-SDK/releases](https://github.com/Microsoft/Intune-PowerShell-SDK/releases)adresu a vyberte soubor **Intune-PowerShell-SDK_v6. zip** .

    1. Vyberte **Uložit jako**a vyberte složku, kterou si pamatujete. `c:\psscripts`je dobrá volba.
    2. Otevřete složku, klikněte pravým tlačítkem na soubor. zip > **extrahování všech** > **extrakcí**. Struktura složek vypadá podobně jako v následující složce:

        > [!div class="mx-imgBorder"]
        > ![Struktura složky sady Intune PowerShell SDK po extrakci](./media/tutorial-walkthrough-administrative-templates/psscripts-directory.png)

5. Na kartě **zobrazení** zkontrolujte **přípony názvů souborů**:

    > [!div class="mx-imgBorder"]
    > ![Na kartě zobrazení v Průzkumníkovi vyberte přípony názvů souborů.](./media/tutorial-walkthrough-administrative-templates/file-names-extension.png)

6. Ve složce a přejít na `c:\psscripts\Intune-PowerShell-SDK_v6.1907.00921.0001\drop\outputs\build\Release\net471`. Klikněte pravým tlačítkem na všechny knihovny DLL. > **vlastnosti** > **odblokovat**.

    > [!div class="mx-imgBorder"]
    > ![Odblokovat knihovny DLL](./media/tutorial-walkthrough-administrative-templates/unblock-dll.png)

7. V aplikaci **Windows PowerShell** zadejte:

    ```powershell
    Import-Module c:\psscripts\Intune-PowerShell-SDK_v6.1907.00921.0001\drop\outputs\build\Release\net471\Microsoft.Graph.Intune.psd1
    ```

    Pokud `R` se zobrazí výzva ke spuštění z nedůvěryhodného vydavatele, zadejte.

8. Šablony pro správu Intune používají beta verzi grafu:

    1. Napište`Update-MSGraphEnvironment -SchemaVersion 'beta'`

    2. Napište`Connect-MSGraph -AdminConsent`

    3. Po zobrazení výzvy se přihlaste pomocí stejného účtu správce Microsoft 365. Tyto rutiny vytvářejí zásady ve vaší organizaci tenanta.

        **Uživatel**: zadejte účet správce předplatného tenanta Microsoft 365.  
        **Heslo**: zadejte jeho heslo.

    4. Vyberte **Přijmout**.

9. Vytvořte konfigurační profil konfigurace **testu** . Zadejte:

    ```powershell
    $configuration = Invoke-MSGraphRequest -Url https://graph.microsoft.com/beta/deviceManagement/groupPolicyConfigurations -Content '{"displayName":"Test Configuration","description":"A test configuration created through PS"}' -HttpMethod POST
    ```

    Po úspěšném provedení těchto rutin se vytvoří profil. Potvrďte to tak, že přejdete do centra pro správu Správce koncových bodů > **konfigurační profily**. Váš profil **Konfigurace testu** by měl být uveden.

10. Získejte všechna SettingDefinitions. Zadejte:

    ```powershell
    $settingDefinitions = Invoke-MSGraphRequest -Url https://graph.microsoft.com/beta/deviceManagement/groupPolicyDefinitions -HttpMethod GET
    ```

11. Najděte ID definice pomocí zobrazovaného názvu nastavení. Zadejte:

    ```powershell
    $desiredSettingDefinition = $settingDefinitions.value | ? {$_.DisplayName -Match "Silently sign in users to the OneDrive sync client with their Windows credentials"}
    ```

12. Nakonfigurujte nastavení. Zadejte:

    ```powershell
    $configuredSetting = Invoke-MSGraphRequest -Url "https://graph.microsoft.com/beta/deviceManagement/groupPolicyConfigurations('$($configuration.id)')/definitionValues" -Content ("{""enabled"":""true"",""configurationType"":""policy"",""definition@odata.bind"":""https://graph.microsoft.com/beta/deviceManagement/groupPolicyDefinitions('$($desiredSettingDefinition.id)')""}") -HttpMethod POST
    ```

    ```powershell
    Invoke-MSGraphRequest -Url "https://graph.microsoft.com/beta/deviceManagement/groupPolicyConfigurations('$($configuration.id)')/definitionValues('$($configuredSetting.id)')" -Content ("{""enabled"":""false""}") -HttpMethod PATCH
    ```

    ```powershell
    $configuredSetting = Invoke-MSGraphRequest -Url "https://graph.microsoft.com/beta/deviceManagement/groupPolicyConfigurations('$($configuration.id)')/definitionValues('$($configuredSetting.id)')" -HttpMethod GET
    ```

### <a name="see-your-policy"></a>Zobrazit vaše zásady

1. V centru pro správu Správce koncových bodů >**aktualizujte** **konfigurační profily** > .
2. Vyberte profil **Konfigurace testu** > **Nastavení**.
3. V rozevíracím seznamu vyberte možnost **všechny produkty**.

V případě, že je nakonfigurované nastavení **přihlašovacích údajů pro Windows, uvidíte uživatele v tichém režimu přihlášení k synchronizačnímu klientovi OneDrive** .

## <a name="policy-best-practices"></a>Osvědčené postupy pro zásady

Při vytváření zásad a profilů v Intune je potřeba vzít v úvahu několik doporučení a osvědčených postupů. Další informace najdete v tématu [osvědčené postupy pro zásady a profily](device-profile-create.md#recommendations).

## <a name="clean-up-resources"></a>Vyčištění prostředků

Pokud už je nepotřebujete, můžete:

- Odstraňte skupiny, které jste vytvořili:

  - **Všechna zařízení se systémem Windows 10 student**
  - **Všechna zařízení s Windows**
  - **Všichni učitelé**

- Odstraňte vytvořené šablony pro správu:

  - **Šablona správce – zařízení s Windows 10 student**
  - **Šablona správce – zásady OneDrivu, které se vztahují na všechny uživatele Windows 10**
  - **Konfigurace testu**

- Nastavte zásady spouštění prostředí Windows PowerShell zpátky na původní hodnotu. Následující příklad nastaví zásady spouštění na omezení:

  ```powershell
  Set-ExecutionPolicy -ExecutionPolicy Restricted
  ```

## <a name="next-steps"></a>Další kroky

V tomto kurzu se seznámíte s [centrem pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431), pomocí Tvůrce dotazů můžete vytvářet dynamické skupiny a v Intune vytvářet šablony pro správu, které slouží ke konfiguraci [Nastavení ADMX](https://docs.microsoft.com/windows/client-management/mdm/understanding-admx-backed-policies). V Intune jste také porovnali používání šablon ADMX místně a v cloudu. Jako bonus jste k vytvoření šablony pro správu použili rutiny prostředí PowerShell.

Další informace o šablonách pro správu v Intune najdete v těchto tématech:

> [!div class="nextstepaction"]
> [Použití šablon Windows 10 ke konfiguraci nastavení zásad skupiny v Intune](administrative-templates-windows.md)
