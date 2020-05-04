---
title: Kurz – návod Intune ve Správci Microsoft Endpoint Manager
titleSuffix: Microsoft Intune
description: V tomto kurzu provedete Microsoft Intune v centru pro správu Microsoft Endpoint Manageru, abyste lépe pochopili, jak provádět úlohy.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/06/2019
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
Customer intent: As an Intune admin, I want to learn where to find the different features in Intune from the Microsoft Endpoint Manager admin center.
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 81ea88bc72e6bcd52dbfe51cb4fa12803605de18
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79330387"
---
# <a name="tutorial-walkthrough-intune-in-microsoft-endpoint-manager"></a>Kurz: Seznámení se se službou Intune v Microsoft Endpoint Manageru

[Azure](https://docs.microsoft.com/learn/modules/welcome-to-azure) obsahuje více než 100 služeb, které vám pomůžou s nejrůznějšími scénáři a možnostmi cloud computingu. Microsoft Intune je jedna z několika služeb dostupných v Azure. Intune vám pomůže zajistit, aby zařízení, aplikace a data vaší společnosti splňovaly požadavky na zabezpečení vaší společnosti. Máte kontrolu nad tím, které požadavky je potřeba zkontrolovat a co se stane, když tyto požadavky nebudou splněné. [Centrum pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) je místo, kde můžete najít službu Microsoft Intune a další nastavení související s správou zařízení. Porozumění funkcím dostupným v Intune vám pomůže dosáhnout různých úloh správy mobilních zařízení (MDM) a správy mobilních aplikací (MAM).

> [!NOTE]
> Microsoft Endpoint Manager je jediná integrovaná platforma pro správu koncových bodů pro správu všech vašich koncových bodů. Toto centrum pro správu Microsoft Endpoint Manageru integruje nástroj ConfigMgr a Microsoft Intune.

V tomto kurzu provedete následující:
> [!div class="checklist"]
> * Prohlídka centra pro správu Microsoft Endpoint Manageru
> * Přizpůsobení zobrazení centra pro správu Microsoft Endpoint Manageru

Pokud nemáte předplatné Intune, [Zaregistrujte si bezplatný zkušební účet](free-trial-sign-up.md).

## <a name="prerequisites"></a>Požadavky
Než budete nastavovat Microsoft Intune, projděte si následující požadavky:

- [Podporované operační systémy a prohlížeče](supported-devices-browsers.md)
- [Požadavky týkající se konfigurace sítě a šířky pásma](network-bandwidth-use.md)

## <a name="sign-up-for-a-microsoft-intune-free-trial"></a>Registrace bezplatné zkušební verze Microsoft Intune

Intune si můžete zdarma vyzkoušet. Zkušební doba je 30 dní. Pokud už máte svůj pracovní nebo školní účet, **přihlaste se** s jeho použitím a přidejte Intune k svému předplatnému. Jinak si můžete [zaregistrovat bezplatný zkušební účet](free-trial-sign-up.md) , abyste mohli používat Intune pro vaši organizaci.

> [!IMPORTANT]
> Když si zaregistrujete nový účet, nebude možné s ním kombinovat stávající pracovní nebo školní účet.

## <a name="tour-microsoft-intune-in-the-microsoft-endpoint-manager-admin-center"></a>Microsoft Intune prohlídky v centru pro správu Microsoft Endpoint Manageru

Pomocí následujících kroků můžete lépe pochopit Intune v centru pro správu Microsoft Endpoint Manager. Po dokončení prohlídky budete mít lepší informace o některých hlavních oblastech Intune.

1. Otevřete prohlížeč a přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431). Pokud s Intune začínáte, použijte bezplatné zkušební předplatné.

    ![Snímek obrazovky s centrem pro správu Microsoft Endpoint Manager – Domovská stránka](./media/tutorial-walkthrough-endpoint-manager/tutorial-walkthrough-mem-01.png)

    Když otevřete Microsoft Endpoint Manager nebo jakoukoli jinou službu v Azure, služba se zobrazí v podokně. Mezi první úlohy, které můžete v Intune použít, patří **zařízení**, **aplikace**, **Uživatelé**a **skupiny**. Úlohou je pouze podoblast služby. Po výběru úlohy se toto podokno otevře jako plná stránka. Ostatní podokna se při otevření dostanou na pravé straně podokna a blízkoou se odhalí předchozí podokno. 

    Když ve výchozím nastavení otevřete Microsoft Endpoint Manager, zobrazí se podokno **domovské stránky** . Toto podokno poskytuje celkový vizuální snímek stavu tenanta a stavu dodržování předpisů a také další užitečné související odkazy.

2. V navigačním podokně vyberte **řídicí panel** , abyste zobrazili celkové podrobnosti o zařízeních a klientech aplikace v tenantovi Intune. Pokud začínáte s novým klientem Intune, zatím nebudete mít žádná zaregistrovaná zařízení. 

    ![Snímek obrazovky centra pro správu Microsoft Endpoint Manageru – řídicí panel](./media/tutorial-walkthrough-endpoint-manager/tutorial-walkthrough-mem-02.png)
    
    Intune umožňuje spravovat zařízení a aplikace vašich zaměstnanců, včetně toho, jak přistupují k firemním datům. Aby bylo možné použít tuto službu správy mobilních zařízení (MDM), musí být zařízení nejprve zaregistrovaná v Intune. Když je zařízení zaregistrované, vystaví se mu certifikát MDM. Tento certifikát slouží ke komunikaci se službou Intune. 

    Existuje několik způsobů, jak zaregistrovat zařízení zaměstnanců do Intune. Každá metoda závisí na vlastnictví zařízení (osobní nebo firemní), typu zařízení (iOS/iPadOS, Windows, Android) a požadavcích na správu (resetování, spřažení, uzamykání). Abyste ale mohli povolit registraci zařízení, musíte si nastavit infrastrukturu Intune. Registrace zařízení vyžaduje zejména [nastavení autority MDM](mdm-authority-set.md). Další informace o tom, jak připravit prostředí Intune (tenanta), najdete v tématu [Nastavení Intune](setup-steps.md). Jakmile budete mít tenanta Intune připravený, můžete zaregistrovat zařízení. Další informace o registraci zařízení najdete v článku [Co je registrace zařízení?](../enrollment/device-enrollment.md)

3. V navigačním podokně vyberte **zařízení** a zobrazí se podrobnosti o zaregistrovaných zařízeních v tenantovi Intune. 

    > [!TIP]
    > Pokud jste v Azure Portal dříve použili Intune, zjistili jste výše uvedené podrobnosti v Azure Portal tak, že se přihlásíte k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) a vyberete **zařízení**.

    Podokno **Přehled zařízení** obsahuje několik karet, které umožňují zobrazit souhrn následujících stavů a výstrah:
    - **Stav registrace** – Projděte si podrobnosti o zařízeních zaregistrovaných v Intune podle platforem a selhání registrace.
    - **Výstrahy registrace** – další podrobnosti o nepřiřazených zařízeních podle platformy najdete v podrobnostech. 
    - **Stav dodržování předpisů** – zkontrolujte stav dodržování předpisů na základě zařízení, zásad, nastavení, hrozeb a ochrany. Toto podokno navíc nabízí seznam zařízení bez zásad dodržování předpisů.
    - **Stav konfigurace** – zkontrolujte stav konfigurace profilů zařízení a také nasazení profilu. 
    - **Stav aktualizace softwaru** – zobrazí vizuál stavu nasazení pro všechna zařízení a pro všechny uživatele.

    ![Snímek obrazovky centra pro správu Microsoft Endpoint Manageru – zařízení](./media/tutorial-walkthrough-endpoint-manager/tutorial-walkthrough-mem-03.png)

4. V podokně **zařízení – přehled** vyberte **zásady dodržování předpisů** a zobrazte podrobnosti o kompatibilitě pro zařízení spravovaná službou Intune. Zobrazí se podrobnosti podobné následujícímu obrázku.

    ![Snímek obrazovky centra pro správu služby Microsoft Endpoint Manager – zásady dodržování předpisů](./media/tutorial-walkthrough-endpoint-manager/tutorial-walkthrough-mem-04.png)
    
    > [!TIP]
    > Pokud jste v Azure Portal dříve použili Intune, zjistili jste výše uvedené podrobnosti v Azure Portal, když se přihlásíte k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) a vyberete **dodržování předpisů pro zařízení**.

    Požadavky na dodržování předpisů jsou v podstatě pravidla, jako třeba vyžadování PIN kódu zařízení nebo vyžadování šifrování zařízení. Zásady dodržování předpisů pro zařízení definují pravidla a nastavení, která musí zařízení dodržovat, aby se dalo považovat za vyhovující. Pokud chcete použít dodržování předpisů zařízením, musíte mít:
    - Předplatné Intune a Azure Active Directory (Azure AD) Premium
    - Zařízení, na kterých běží podporovaná platforma
    - Zařízení musí být zaregistrovaná v Intune.
    - Zařízení, která jsou zaregistrovaná jednomu uživateli nebo žádnému primárnímu uživateli.
    
    Další informace najdete v tématu [Začínáme se zásadami dodržování předpisů zařízením v Intune](../protect/device-compliance-get-started.md).

5. V podokně **zařízení – přehled** vyberte **podmíněný přístup** a zobrazte podrobnosti o zásadách přístupu.

    ![Snímek obrazovky centra pro správu Microsoft Endpoint Manager – podmíněný přístup](./media/tutorial-walkthrough-endpoint-manager/tutorial-walkthrough-mem-05.png)

    > [!TIP]
    > Pokud jste v Azure Portal dříve použili Intune, zjistili jste výše uvedené podrobnosti v Azure Portal, když se přihlásíte k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) a vyberete **podmíněný přístup**.

    Podmíněný přístup označuje způsoby, kterými můžete řídit zařízení a aplikace, které se můžou připojovat k e-mailu a prostředkům společnosti. Další informace o podmíněném přístupu založeném na zařízeních a aplikacích a o běžných scénářích použití podmíněného přístupu v Intune najdete v tématu [co je podmíněný přístup?](../protect/conditional-access.md) .

6. V navigačním podokně vyberte možnost**profily konfigurací** **zařízení** > a zobrazte podrobnosti o profilech zařízení v Intune.

    ![Snímek obrazovky centra pro správu služby Microsoft Endpoint Manager – konfigurační profily](./media/tutorial-walkthrough-endpoint-manager/tutorial-walkthrough-mem-06.png)
    
    > [!TIP]
    > Pokud jste v Azure Portal dříve použili Intune, zjistili jste výše uvedené podrobnosti v Azure Portal tak, že se přihlásíte k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) a vyberete **Konfigurace zařízení**.

    Intune obsahuje nastavení a funkce, které můžete různým zařízením v organizaci povolit nebo zakázat. Tato nastavení a funkce se přidají do části "konfigurační profily". Můžete vytvářet profily pro různá zařízení a různé platformy, včetně iOS/iPadOS, Androidu, macOS a Windows. Pak můžete použít Intune k aplikování profilu na zařízení ve vaší organizaci.   

    Další informace o konfiguraci zařízení najdete v tématu [použití nastavení funkcí v zařízeních pomocí profilů zařízení v Microsoft Intune](../configuration/device-profiles.md).

7. V navigačním podokně vyberte **zařízení** > **všechna zařízení** a zobrazte podrobnosti o zaregistrovaných zařízeních klienta Intune. Pokud začínáte s novým zařazení Intune, zatím nebudete mít žádná zaregistrovaná zařízení.

    ![Snímek obrazovky s centrem pro správu Microsoft Endpoint Manageru – všechna zařízení](./media/tutorial-walkthrough-endpoint-manager/tutorial-walkthrough-mem-07.png)

    Tento seznam zařízení zobrazuje podrobné informace o kompatibilitě, verzi operačního systému a datu posledního vrácení se změnami.

    > [!TIP]
    > Pokud jste v Azure Portal dříve použili Intune, zjistili jste výše uvedené podrobnosti v Azure Portal tak, že se přihlásíte k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) a vyberete **zařízení** > **všechna zařízení**.
 
8. V navigačním podokně vyberte **aplikace** , abyste zobrazili přehled o stavu aplikace. V tomto podokně se zobrazuje stav instalace aplikace na základě následujících karet:

    > [!TIP]
    > Pokud jste v Azure Portal dříve použili Intune, zjistili jste výše uvedené podrobnosti v Azure Portal tak, že se přihlásíte k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) a vyberete **klientské aplikace**.

    Podokno s **přehledem aplikací** obsahuje dvě karty, které umožňují zobrazit souhrn následujících stavů:
    - **Stav instalace** – Prohlédněte si hlavní chyby instalace zařízení a také aplikace s chybami při instalaci.  
    - **Stav zásad ochrany aplikací** – informace o přiřazených uživatelích ke zásadám ochrany aplikací a také uživatelům označených příznakem

    ![Snímek obrazovky centra pro správu Microsoft Endpoint Manageru – aplikace](./media/tutorial-walkthrough-endpoint-manager/tutorial-walkthrough-mem-08.png)

    Jako správce IT můžete Microsoft Intune použít ke správě klientských aplikací, které používají pracovníci vaší společnosti. Tato funkce doplňuje správu zařízení a ochranu dat. Jednou z priorit správce je zajistit, aby koncoví uživatelé měli přístup k aplikacím, které potřebují ke své práci. Navíc potřebujete přiřazovat a spravovat aplikace na zařízeních, která nejsou zaregistrovaná v Intune. Intune nabízí celou řadu funkcí, které vám pomůžou zajistit, aby na požadovaných zařízeních byly potřebné aplikace. 

    > [!NOTE]
    > V podokně s **přehledem aplikací** jsou taky informace o stavu tenanta a účtu.

    Další informace o přidávání a přiřazování aplikací najdete v tématu [Přidání aplikací do Microsoft Intune](../apps/apps-add.md) a [přiřazení aplikací do skupin pomocí Microsoft Intune](../apps/apps-deploy.md).

9. V podokně **aplikace – přehled** vyberte **všechny aplikace** , abyste viděli seznam aplikací přidaných do Intune.

    > [!TIP]
    > Pokud jste v Azure Portal dříve použili Intune, zjistili jste výše uvedené podrobnosti v Azure Portal tak, že se přihlásíte [k Intune](https://go.microsoft.com/fwlink/?linkid=2090973) a vyberete**aplikace**pro **klientské aplikace** > .

    Do Intune můžete přidat různé typy aplikací, které jsou založené na platformě. Po přidání aplikace ji můžete přiřadit ke skupinám uživatelů. 

    ![Snímek obrazovky s centrem pro správu Microsoft Endpoint Manageru – všechny aplikace](./media/tutorial-walkthrough-endpoint-manager/tutorial-walkthrough-mem-09.png)

    Další informace najdete v článku [Přidání aplikací do Microsoft Intune](../apps/apps-add.md).

10. V navigačním podokně vyberte **Uživatelé** a zobrazte si podrobnosti o uživatelích, které jste zahrnuli do Intune. Tito uživatelé jsou zaměstnanci vaší společnosti.

    ![Snímek obrazovky s centrem pro správu Microsoft Endpoint Manager – uživatelé](./media/tutorial-walkthrough-endpoint-manager/tutorial-walkthrough-mem-10.png)

    > [!TIP]
    > Pokud jste v Azure Portal dříve použili Intune, zjistili jste výše uvedené podrobnosti v Azure Portal tak, že se přihlásíte k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) a vyberete **Uživatelé**.

    Můžete přidat uživatele přímo do Intune nebo synchronizovat uživatele z místní služby Active Directory. Po přidání můžou uživatelé zaregistrovat zařízení a přistupovat k prostředkům společnosti. Taky můžete uživatelům poskytnout další oprávnění k přístupu k Intune. Další informace najdete v tématech [Přidání uživatelů a udělení oprávnění pro správu do Intune](users-add.md).

11. V navigačním podokně vyberte **skupiny** a zobrazte podrobnosti o skupinách Azure Active Directory (Azure AD), které jsou zahrnuté v Intune. Jako správce Intune můžete skupiny používat ke správě zařízení a uživatelů.

    ![Snímek obrazovky centra pro správu Microsoft Endpoint Manageru – skupiny](./media/tutorial-walkthrough-endpoint-manager/tutorial-walkthrough-mem-11.png)

    > [!TIP]
    > Pokud jste v Azure Portal dříve použili Intune, zjistili jste výše uvedené podrobnosti v Azure Portal tak, že se přihlásíte k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) a vyberete **skupiny**.

    Skupiny můžete nastavit tak, aby vyhovovaly potřebám vaší organizace. Vytvořte skupiny, které uživatele nebo zařízení uspořádají podle zeměpisné polohy, oddělení nebo vlastností hardwaru. Skupiny použijte ke spravování úloh se škálováním. Můžete například nastavit zásady pro mnoho uživatelů nebo nasazovat aplikace do sady zařízení. Další informace o skupinách najdete v tématu [Přidání skupin pro uspořádání uživatelů a zařízení](groups-add.md).

12. V navigačním podokně vyberte **Správa tenanta** , abyste zobrazili podrobnosti o tenantovi Intune.

    > [!TIP]
    > Pokud jste v Azure Portal dříve použili Intune, zjistili jste výše uvedené podrobnosti v Azure Portal tak, že se přihlásíte k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) a vyberete **stav tenanta**.

    **Správce tenanta – podokno stav tenanta** poskytuje karty pro **Podrobnosti o tenantovi**, **stav konektoru**a **řídicí panel stavu služby**. Pokud se u vašeho tenanta nebo samotného Intune vyskytnou nějaké problémy, najdete podrobnosti dostupné v tomto podokně.

    ![Snímek obrazovky centra pro správu služby Microsoft Endpoint Manager – stav tenanta](./media/tutorial-walkthrough-endpoint-manager/tutorial-walkthrough-mem-12.png)

    Další informace najdete v tématu [stav tenanta Intune](tenant-status.md).

13. V navigačním podokně vyberte **řešení potíží +** > **řešení** potíží a ověřte podrobnosti o stavu konkrétního uživatele. 

    > [!TIP]
    > Pokud jste v Azure Portal dříve použili Intune, zjistili jste výše uvedené podrobnosti v Azure Portal tak, že se přihlásíte k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) a vyberete **řešení potíží**.

    V rozevíracím seznamu **přiřazení** se můžete rozhodnout pro zobrazení cílových přiřazení klientských aplikací, zásad, aktualizačních kroužků a omezení registrace. Kromě toho toto podokno poskytuje podrobnosti o zařízení, stavu ochrany aplikací a selhání registrace pro konkrétního uživatele.

    ![Snímek obrazovky centra pro správu Microsoft Endpoint Manageru – řešení potíží](./media/tutorial-walkthrough-endpoint-manager/tutorial-walkthrough-mem-13.png)

    Další informace o řešení potíží v Intune najdete v tématu [použití portálu pro řešení potíží pro pomoc uživatelům ve vaší společnosti](help-desk-operators.md).

14. V navigačním podokně vyberte možnost **Poradce při potížích + podpora** > **a podpora a** požádejte o pomoc.

    > [!TIP]
    > Pokud jste v Azure Portal dříve použili Intune, zjistili jste výše uvedené podrobnosti v Azure Portal tak, že se přihlásíte k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) a vyberete možnost **pomoc a podpora**.

    Jako správce IT můžete použít možnost **pomoc a podpora** k vyhledávání a zobrazení řešení a také k podávání lístku on-line Support pro Intune.

    ![Snímek obrazovky centra pro správu Microsoft Endpoint Manageru – pomoc a podpora](./media/tutorial-walkthrough-endpoint-manager/tutorial-walkthrough-mem-14.png)

    Pokud chcete vytvořit lístek podpory, váš účet musí být přiřazený jako role správce v Azure Active Directory. Role správců zahrnují správce **Intune**, **globálního správce**a **Správce služeb**.

    Další informace najdete v tématu [Jak získat podporu pro Microsoft Intune](get-support.md).

15. V navigačním podokně vyberte **Poradce při potížích** > a ve**scénářích s asistencí** pro zobrazení dostupných scénářů s asistencí Intune.

    Scénář s asistencí je přizpůsobený sled kroků, které jsou na začátku celého případu použití. Běžné scénáře jsou založené na roli, kterou správce, uživatel nebo zařízení hraje ve vaší organizaci. Tyto role obvykle vyžadují kolekci pečlivě Orchestrované profily, nastavení, aplikace a kontroly zabezpečení, které poskytují nejlepší uživatelské prostředí a zabezpečení.

    Pokud nejste obeznámeni se všemi kroky a prostředky potřebnými k implementaci konkrétního scénáře Intune, můžete použít jako výchozí bod scénáře s asistencí.

    ![Snímek obrazovky s centrem pro správu služby Microsoft Endpoint Manager – řízené scénáře](./media/tutorial-walkthrough-endpoint-manager/tutorial-walkthrough-mem-15.png)

    Další informace o scénářích s průvodcem najdete v článku [Přehled scénářů](guided-scenarios-overview.md).

## <a name="configure-the-microsoft-endpoint-manager-admin-center"></a>Konfigurace centra pro správu Microsoft Endpoint Manageru

Azure umožňuje přizpůsobit a nakonfigurovat zobrazení portálu.

### <a name="change-the-dashboard"></a>Změna řídicího panelu

**Řídicí panel** , který zobrazuje celkové podrobnosti o zařízeních a klientech aplikace v tenantovi Intune. Řídicí panely poskytují způsob, jak vytvořit prioritní a uspořádané zobrazení v centru pro správu služby Microsoft Endpoint Manager. Řídicí panely slouží jako pracovní prostor, kde můžete rychle spouštět úlohy pro každodenní operace a monitorovat prostředky. Můžete například vytvářet vlastní řídicí panely založené na projektech, úkolech nebo rolích uživatelů. Centrum pro správu Microsoft Endpoint Manageru poskytuje výchozí řídicí panel jako výchozí bod. Můžete upravit výchozí řídicí panel, vytvořit a přizpůsobit další řídicí panely a publikovat a sdílet řídicí panely, které je zpřístupní ostatním uživatelům. 

   ![Snímek obrazovky centra pro správu Microsoft Endpoint Manageru – řídicí panel](./media/tutorial-walkthrough-endpoint-manager/tutorial-walkthrough-mem-16.png)

Chcete-li upravit aktuální řídicí panel, vyberte možnost **Upravit**. Pokud výchozí řídicí panel nechcete změnit, můžete také vytvořit **Nový řídicí panel**. Vytvořením nového řídicího panelu získáte prázdný privátní řídicí panel s **galerií dlaždic**, který umožňuje přidání a uspořádání dlaždic. Můžete najít dlaždice podle typu kategorie nebo prostředku. Můžete také vyhledat konkrétní dlaždice. Vyberte **Můj řídicí panel** a vyberte libovolný ze stávajících vlastních řídicích panelů.

### <a name="change-the-portal-settings"></a>Změna nastavení portálu

Centrum pro správu Microsoft Endpoint Manageru můžete přizpůsobit tak, že vyberete výchozí zobrazení, motiv, dobu časového limitu přihlašovacích údajů a také nastavení jazyka a oblasti.

   <img alt="Screenshot of the Microsoft Endpoint Manager admin center - Portal settings" src="./media/tutorial-walkthrough-endpoint-manager/tutorial-walkthrough-mem-17.png" width="250">

## <a name="next-steps"></a>Další kroky

Pokud chcete rychle pracovat na Microsoft Intune, přečtěte si první nastavení bezplatného účtu Intune a Projděte si rychlý Start k Intune.

> [!div class="nextstepaction"]
> [Rychlý start: Bezplatné vyzkoušení Microsoft Intune](free-trial-sign-up.md)
