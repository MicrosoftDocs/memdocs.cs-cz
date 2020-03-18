---
title: Kurz – návod Intune v Azure Portal
titleSuffix: Microsoft Intune
description: V tomto kurzu provedete Microsoft Intune, abyste lépe pochopili, jak provádět úlohy.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/06/2019
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: e892d8a3-7f74-498c-98d5-e968a8fbb049
Customer intent: As an Intune admin, I want to learn where to find the different features in Intune.
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 22910604d19aecb37adef2452d01d46c1435f7ef
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79330299"
---
# <a name="tutorial-walkthrough-of-microsoft-intune-in-the-azure-portal"></a>Kurz: návod Microsoft Intune v Azure Portal

[Azure](https://docs.microsoft.com/learn/modules/welcome-to-azure) obsahuje více než 100 služeb, které vám pomůžou s nejrůznějšími scénáři a možnostmi cloud computingu. Microsoft Intune je jedna z několika služeb dostupných v Azure. Intune vám pomůže zajistit, aby zařízení, aplikace a data vaší společnosti splňovaly požadavky na zabezpečení vaší společnosti. Máte kontrolu nad tím, které požadavky je potřeba zkontrolovat a co se stane, když tyto požadavky nebudou splněné. [Azure Portal](https://portal.azure.com) je místo, kde najdete službu Microsoft Intune. Porozumění funkcím dostupným v Intune vám pomůže dosáhnout různých úloh správy mobilních zařízení (MDM) a správy mobilních aplikací (MAM).

V tomto kurzu se naučíte:
> [!div class="checklist"]
> * Microsoft Intune prohlídky
> * Nakonfigurovat Azure Portal

Pokud nemáte předplatné Intune, [Zaregistrujte si bezplatný zkušební účet](free-trial-sign-up.md).

## <a name="prerequisites"></a>Požadavky
Než budete nastavovat Microsoft Intune, projděte si následující požadavky:

- [Podporované operační systémy a prohlížeče](supported-devices-browsers.md) 
- [Požadavky týkající se konfigurace sítě a šířky pásma](network-bandwidth-use.md)

## <a name="sign-up-for-a-microsoft-intune-free-trial"></a>Registrace bezplatné zkušební verze Microsoft Intune

Intune si můžete zdarma vyzkoušet. Zkušební doba je 30 dní. Pokud už máte svůj pracovní nebo školní účet, **přihlaste se** s jeho použitím a přidejte Intune k svému předplatnému. Jinak si můžete [zaregistrovat bezplatný zkušební účet](free-trial-sign-up.md) , abyste mohli používat Intune pro vaši organizaci.

> [!IMPORTANT]
> Když si zaregistrujete nový účet, nebude možné s ním kombinovat stávající pracovní nebo školní účet.

## <a name="tour-microsoft-intune"></a>Microsoft Intune prohlídky

Pomocí následujících kroků můžete lépe pochopit Intune v Azure Portal. Po dokončení prohlídky budete mít lepší informace o některých hlavních oblastech Intune.

1. Otevřete prohlížeč a přihlaste se k [portálu Intune](https://aka.ms/intuneportal). Pokud s Intune začínáte, použijte bezplatné zkušební předplatné.

    ![Snímek obrazovky Microsoft Intuneového portálu](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-01.png)

    Když v Azure otevřete Intune nebo jakoukoli jinou službu, tato služba se zobrazí v podokně. Mezi první úlohy, které můžete v Intune použít, patří **zařízení**, **klientské aplikace**, **Uživatelé**a **skupiny**. Úlohou je pouze podoblast služby. Po výběru úlohy se toto podokno otevře jako plná stránka. Ostatní podokna se při otevření dostanou na pravé straně podokna a blízkoou se odhalí předchozí podokno. Podokno se také označuje jako okno. 

    Ve výchozím nastavení se při otevření Intune zobrazí podokno **Přehled** . Toto podokno poskytuje celkový vizuální snímek přiřazení zařízení a stavu dodržování předpisů a také stav instalace aplikace.

2. V [Intune](https://aka.ms/intuneportal)vyberte **registrace zařízení** a zobrazte podrobnosti o zaregistrovaných zařízeních v tenantovi Intune. Pokud začínáte s novým klientem Intune, zatím nebudete mít žádná zaregistrovaná zařízení. 

    ![Snímek obrazovky s podoknem registrace zařízení](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-02.png)
    
    Intune umožňuje spravovat zařízení a aplikace vašich zaměstnanců, včetně toho, jak přistupují k firemním datům. Aby bylo možné použít tuto službu správy mobilních zařízení (MDM), musí být zařízení nejprve zaregistrovaná v Intune. Když je zařízení zaregistrované, vystaví se mu certifikát MDM. Tento certifikát slouží ke komunikaci se službou Intune. 

    Existuje několik způsobů, jak zaregistrovat zařízení zaměstnanců do Intune. Každá metoda závisí na vlastnictví zařízení (osobní nebo firemní), typu zařízení (iOS/iPadOS, Windows, Android) a požadavcích na správu (resetování, spřažení, uzamykání). Abyste ale mohli povolit registraci zařízení, musíte si nastavit infrastrukturu Intune. Registrace zařízení vyžaduje zejména [nastavení autority MDM](mdm-authority-set.md). Další informace o tom, jak připravit prostředí Intune (tenanta), najdete v tématu [Nastavení Intune](setup-steps.md). Jakmile budete mít tenanta Intune připravený, můžete zaregistrovat zařízení. Další informace o registraci zařízení najdete v článku [Co je registrace zařízení?](../enrollment/device-enrollment.md)

3. V [Intune](https://aka.ms/intuneportal)vyberte **dodržování předpisů zařízením** , abyste zobrazili podrobnosti o dodržování předpisů pro zařízení spravovaná pomocí Intune. Zobrazí se podrobnosti podobné následujícímu obrázku.

    ![Snímek obrazovky s podoknem dodržování předpisů zařízením](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-03.png)
    
    Požadavky na dodržování předpisů jsou v podstatě pravidla, jako třeba vyžadování PIN kódu zařízení nebo vyžadování šifrování zařízení. Zásady dodržování předpisů pro zařízení definují pravidla a nastavení, která musí zařízení dodržovat, aby se dalo považovat za vyhovující. Pokud chcete použít dodržování předpisů zařízením, musíte mít:
    - Předplatné Intune a Azure Active Directory (Azure AD) Premium
    - Zařízení, na kterých běží podporovaná platforma
    - Zařízení musí být zaregistrovaná v Intune.
    - Zařízení, která jsou zaregistrovaná jednomu uživateli nebo žádnému primárnímu uživateli.
    
    Další informace najdete v tématu [Začínáme se zásadami dodržování předpisů zařízením v Intune](../protect/device-compliance-get-started.md).

4. V [Intune](https://aka.ms/intuneportal)vyberte **Konfigurace zařízení** , aby se zobrazily podrobnosti o profilech zařízení v Intune.

    ![Snímek obrazovky s podoknem konfigurace zařízení](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-04.png)
    
    Intune obsahuje nastavení a funkce, které můžete různým zařízením v organizaci povolit nebo zakázat. Tato nastavení a funkce se přidají do části "konfigurační profily". Můžete vytvářet profily pro různá zařízení a různé platformy, včetně iOS/iPadOS, Androidu a Windows. Pak můžete použít Intune k aplikování profilu na zařízení ve vaší organizaci.   

    Další informace o konfiguraci zařízení najdete v tématu [použití nastavení funkcí v zařízeních pomocí profilů zařízení v Microsoft Intune](../configuration/device-profiles.md).

5. V [Intune](https://aka.ms/intuneportal)vyberte **zařízení** a zobrazí se podrobnosti o zaregistrovaných zařízeních tenanta Intune. Pokud začínáte s novým zařazení Intune, zatím nebudete mít žádná zaregistrovaná zařízení.

    ![Snímek obrazovky s podoknem registrace zařízení](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-05.png)

    V podokně **zařízení** najdete podrobné informace o zaregistrovaných zařízeních vašeho tenanta. Kliknutím na **všechna zařízení** můžete zobrazit seznam zařízení pro vašeho tenanta Intune.

6. V [Intune](https://aka.ms/intuneportal)vyberte **klientské aplikace** pro zobrazení stavu instalace aplikace.

    ![Snímek obrazovky s podoknem klientských aplikací](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-06.png)

    Jako správce IT můžete Microsoft Intune použít ke správě klientských aplikací, které používají pracovníci vaší společnosti. Tato funkce doplňuje správu zařízení a ochranu dat. Jednou z priorit správce je zajistit, aby koncoví uživatelé měli přístup k aplikacím, které potřebují ke své práci. Navíc potřebujete přiřazovat a spravovat aplikace na zařízeních, která nejsou zaregistrovaná v Intune. Intune nabízí celou řadu funkcí, které vám pomůžou zajistit, aby na požadovaných zařízeních byly potřebné aplikace. Další informace o přidávání a přiřazování aplikací najdete v tématu [Přidání aplikací do Microsoft Intune](../apps/apps-add.md) a [přiřazení aplikací do skupin pomocí Microsoft Intune](../apps/apps-deploy.md).

7. V [Intune](https://aka.ms/intuneportal)vyberte **podmíněný přístup** , abyste zobrazili podrobnosti o zásadách přístupu.

    ![Snímek obrazovky s podoknem podmíněného přístupu](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-07.png)

    Podmíněný přístup označuje způsoby, kterými můžete řídit zařízení a aplikace, které se můžou připojovat k e-mailu a prostředkům společnosti. Další informace o podmíněném přístupu založeném na zařízeních a aplikacích a o běžných scénářích použití podmíněného přístupu v Intune najdete v tématu [co je podmíněný přístup?](../protect/conditional-access.md) .

8. V [Intune](https://aka.ms/intuneportal)vyberte **Uživatelé** a zobrazte si podrobnosti o uživatelích, které jste zahrnuli do Intune. Tito uživatelé jsou zaměstnanci vaší společnosti.

    ![Snímek obrazovky s podoknem uživatelé](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-08.png)

    Můžete přidat uživatele přímo do Intune nebo synchronizovat uživatele z místní služby Active Directory. Po přidání můžou uživatelé zaregistrovat zařízení a přistupovat k prostředkům společnosti. Taky můžete uživatelům poskytnout další oprávnění k přístupu k Intune. Další informace najdete v tématech [Přidání uživatelů a udělení oprávnění pro správu do Intune](users-add.md).

9. V [Intune](https://aka.ms/intuneportal)vyberte **skupiny** , abyste zobrazili podrobnosti o skupinách Azure Active Directory (Azure AD), které jsou zahrnuté v Intune. Jako správce Intune můžete skupiny používat ke správě zařízení a uživatelů.

    ![Snímek obrazovky s podoknem skupiny](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-09.png)

    Skupiny můžete nastavit tak, aby vyhovovaly potřebám vaší organizace. Vytvořte skupiny, které uživatele nebo zařízení uspořádají podle zeměpisné polohy, oddělení nebo vlastností hardwaru. Skupiny použijte ke spravování úloh se škálováním. Můžete například nastavit zásady pro mnoho uživatelů nebo nasazovat aplikace do sady zařízení. Další informace o skupinách najdete v tématu [Přidání skupin pro uspořádání uživatelů a zařízení](groups-add.md).

10. V [Intune](https://aka.ms/intuneportal)zvolte pomoc **a podpora a** požádejte o pomoc. Jako správce IT můžete použít možnost **pomoc a podpora** k vyhledávání a zobrazení řešení a také k podávání lístku on-line Support pro Intune. 

    ![Snímek obrazovky s podoknem pomoc a podpora](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-10.png)

    Pokud chcete vytvořit lístek podpory, váš účet musí být přiřazený jako role správce v Azure Active Directory. Role správců zahrnují správce **Intune**, **globálního správce**a **Správce služeb**. Další informace najdete v tématu [Jak získat podporu pro Microsoft Intune](get-support.md).

11. V [Intune](https://aka.ms/intuneportal)vyberte **stav tenanta** , abyste zobrazili podrobnosti o tenantovi Intune.

    ![Snímek obrazovky s podoknem stavu tenanta](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-11.png)

    Podrobnosti o stavu tenanta zahrnují stav konektoru, stav služby Intune a novinky Intune. Pokud se s vaším klientem nebo Intune vlastní nějaké problémy, najdete podrobnosti v podokně **stav tenanta** . Další informace najdete v tématu [stav tenanta Intune](tenant-status.md).

12. V [Intune](https://aka.ms/intuneportal)vyberte **řešení potíží** , abyste se mohli dostat k zástupci tipů pro odstraňování potíží, žádosti o podporu nebo kontrolu stavu Intune. Tyto informace jsou specifické pro vámi zvoleného uživatele Intune.

    ![Snímek obrazovky s podoknem Poradce při potížích](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-12.png)

Další informace o řešení potíží v Intune najdete v tématu [použití portálu pro řešení potíží pro pomoc uživatelům ve vaší společnosti](help-desk-operators.md).

## <a name="configure-the-azure-portal"></a>Nakonfigurovat Azure Portal

Azure umožňuje přizpůsobit a nakonfigurovat zobrazení portálu.

### <a name="change-the-sidebar"></a>Změnit postranní panel

**Boční panel** na levé straně portálu Azure Portal zobrazuje seznam všech dostupných služeb Azure. Výchozí zobrazení tohoto kompletního seznamu se dá změnit, abyste neustále měli na očích služby, které jsou pro vás nejdůležitější. V níže uvedeném příkladu si přidáte službu Intune na začátek seznamu.

![Hledání služby Microsoft Intune v seznamu Další služby](./media/tutorial-walkthrough-intune-portal/azure-add-intune1.png)

1. Na bočním panelu na levé straně stránky vyberte **Všechny služby**.
2. V poli filtru vyhledejte **Intune**.
3. Výběrem **hvězdičky** přidáte Intune na konec seznamu svých oblíbených služeb.
4. Najeďte na službu Intune myší. Vyberte a přetáhněte Intune pomocí **tří svislých teček** na pravé straně názvu služby.

### <a name="change-the-dashboard"></a>Změna řídicího panelu

Výchozí cílovou stránkou je **řídicí panel**. Na této stránce si dlaždice přizpůsobíte tak, aby zobrazovaly informace, které jsou pro vás nejdůležitější.

![Obrázek obecného nového řídicího panelu. Znázorňuje řídicí panel se všemi službami nalevo a hlavní řídicí panel uprostřed. Tlačítka pro změnu řídicího panelu se nacházejí nahoře společně s dlaždicemi, které nabízejí přístup ke všem prostředkům, výukovým kurzům, stavu služby a Azure Marketpace.](./media/tutorial-walkthrough-intune-portal/azure-default-dashboard.png)

Pokud chcete současný řídicí panel změnit, vyberte tlačítko **Upravit řídicí panel**. Pokud výchozí řídicí panel nechcete změnit, můžete také vytvořit **Nový řídicí panel**. Vytvořením nového řídicího panelu získáte prázdný privátní řídicí panel s **galerií dlaždic**, který umožňuje přidání a uspořádání dlaždic. Dlaždice můžete najít podle **obecné** kategorie, **typu**, pomocí **hledání** a prostřednictvím **skupiny prostředků** nebo **značky**.

Přímo na řídicí panel přidáte dlaždice tak, že zvolíte jakékoli tlačítko se **třemi tečkami** a vyberete **Připnout na řídicí panel**.

![Detail oblasti Uživatelé a skupiny > Všechny skupiny v Intune, kde je v pravém horním rohu skupiny vidět možnost Připnout na řídicí panel](./media/tutorial-walkthrough-intune-portal/azure-pin-to-dashboard.png)

Tato možnost bude užitečnější, až si do Intune přidáte další obsah, jako jsou skupiny a uživatelé.

## <a name="next-steps"></a>Další kroky

Pokud chcete rychle pracovat na Microsoft Intune, přečtěte si první nastavení bezplatného účtu Intune a Projděte si rychlý Start k Intune.

> [!div class="nextstepaction"]
> [Rychlý Start: Vyzkoušejte si Microsoft Intune zdarma](free-trial-sign-up.md)
