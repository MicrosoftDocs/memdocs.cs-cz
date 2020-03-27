---
title: Registrace zařízení pomocí Windows Autopilotu
titleSuffix: Microsoft Intune
description: Zjistěte, jak registrovat zařízení s Windows 10 pomocí Windows Autopilotu.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/23/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a2dc5594-a373-48dc-ba3d-27aff0c3f944
ms.reviewer: spshumwa
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b6512aa01a55a3a1ed949b634b97eb891e9459a9
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80327129"
---
# <a name="enroll-windows-devices-in-intune-by-using-the-windows-autopilot"></a>Registrace zařízení s Windows v Intune pomocí Windows Autopilot  
Windows Autopilot usnadňuje registraci zařízení v Intune. Vytváření a udržování přizpůsobených imagí operačního systému je proces, který zabere hodně času. Další čas můžete také strávit aplikováním těchto vlastních imagí operačního systému na nová zařízení, abyste je připravili k použití, než je předáte koncovým uživatelům. S Microsoft Intune a Autopilotem můžete nová zařízení koncovým uživatelům poskytovat, aniž by bylo nutné vlastní image operačního systému vytvářet, udržovat a aplikovat na zařízení. Když zařízení s Autopilotem spravujete pomocí Intune, můžete v zařízeních po registraci spravovat zásady, profily, aplikace a mnoho dalšího. Přehled výhod, scénáře a požadavky najdete v [přehledu Windows Autopilotu](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot).

Existují čtyři typy nasazení autopilotu:

- [Režim automatického nasazení](https://docs.microsoft.com/windows/deployment/windows-autopilot/self-deploying) pro veřejné terminály, digitální podpisy nebo sdílené zařízení
- [Bílá šetrnější](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove) umožňuje partnerům nebo pracovníkům IT předem zřídit počítač s Windows 10, aby byl plně nakonfigurovaný a připravený pro podnik.
- [Autopilot pro stávající zařízení](https://docs.microsoft.com/windows/deployment/windows-autopilot/existing-devices) umožňuje snadno nasadit nejnovější verzi Windows 10 na vaše stávající zařízení.
- [Režim řízený uživatelem](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) pro tradiční uživatele.

## <a name="prerequisites"></a>Požadavky

- [Předplatné Intune](../fundamentals/licenses.md)
- [Povolená automatická registrace pro Windows](windows-enroll.md#enable-windows-10-automatic-enrollment)
- [Předplatné Azure Active Directory Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) <!--&#40;[trial subscription](https://go.microsoft.com/fwlink/?LinkID=816845)&#41;-->

## <a name="how-to-get-the-csv-for-import-in-intune"></a>Jak získat sdílený svazek clusteru pro import v Intune

Další informace najdete v tématu Principy rutiny prostředí PowerShell.

- [Get-WindowsAutoPilotInfo](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo)

## <a name="add-devices"></a>Přidání zařízení

Zařízení Windows Autopilot můžete přidat importováním souboru CSV s jejich informacemi.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení** > **Windows** > **Windows** > **zařízení** (v části **Windows autopilot Deployment program** > **Import**.

    ![Snímek obrazovky se zařízeními Windows Autopilot](./media/enrollment-autopilot/autopilot-import-device.png)

2. V části **Přidat zařízení Windows AutoPilot** přejděte na soubor CSV se seznamem zařízení, která chcete přidat. Soubor CSV by měl zobrazovat sériová čísla, ID produktů Windows, hodnoty hash hardwaru, volitelné značky skupin a volitelného přiřazeného uživatele. V seznamu můžete mít až 500 řádků. Informace o tom, jak získat informace o zařízení, najdete v tématu [Přidání zařízení do Windows autopilotu](https://docs.microsoft.com/windows/deployment/windows-autopilot/add-devices#device-identification). Použijte formát záhlaví a čáry zobrazený níže:

    `Device Serial Number,Windows Product ID,Hardware Hash,Group Tag,Assigned User`</br>
    `<serialNumber>,<ProductID>,<hardwareHash>,<optionalGroupTag>,<optionalAssignedUser>`

    ![Snímek obrazovky s přidáním zařízení Windows Autopilot](./media/enrollment-autopilot/autopilot-import-device2.png)

    >[!IMPORTANT]
    > Pokud k přiřazení uživatele použijete nahrávání sdíleného svazku clusteru, ujistěte se, že přiřadíte platné hlavní názvy uživatelů (UPN). Pokud přiřadíte neplatný hlavní název uživatele (UPN) (nesprávné uživatelské jméno), může být zařízení nedostupné, dokud neodeberete neplatné přiřazení. Během nahrávání sdíleného svazku clusteru je jediným ověřováním, které jsme provedli ve sloupci **přiřazený uživatel** , kontrola platnosti názvu domény. Nemůžeme provést individuální ověření UPN, abyste se ujistili, že přiřazujete stávajícího nebo správného uživatele.

3. Pomocí **Importovat** zahajte import informací o zařízeních. Import může trvat několik minut.

4. Po dokončení importu vyberte **zařízení** > **Windows** ** > systému Windows > ** **zařízení** (v části **Windows autopilot Deployment program** > **Sync**. Zobrazí se zpráva, že synchronizace probíhá. Dokončení procesu může trvat několik minut v závislosti na tom, kolik zařízení se synchronizuje.

5. Aktualizováním zobrazení zobrazte nová zařízení.

## <a name="create-an-autopilot-device-group"></a>Vytvořit skupinu zařízení Autopilot

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **skupiny** > **Nová skupina**.
2. V okně **Skupina**:
    1. Pro **Typ skupiny** zvolte **Zabezpečení**.
    2. Zadejte **Název skupiny** a **Popis skupiny**.
    3. Pro **Typ členství** zvolte buď **Přiřazené** nebo **Dynamické zařízení**.
3. Pokud jste v předchozím kroku pro **Typ členství** vybrali **Přiřazené**, potom v okně **Skupina** zvolte **Členové** a přidejte do skupiny zařízení Autopilot.
    Zařízení Autopilot, která ještě nejsou zaregistrovaná, jsou zařízení, jejichž název se rovná sériovému číslu zařízení.
4. Pokud jste výše pro **Typ členství** zvolili **Dynamické zařízení**, potom v okně **Skupina** zvolte **Členové s dynamickými zařízeními** a do pole **Pokročilé pravidlo** zadejte některý z následujících kódů. Tato pravidla shromažďují jenom zařízení s autopilotem, protože cílí na atributy, které mají jenom zařízení s autopilotem. Vytváření skupin založených na autopilotních atributech nezaručuje, že zařízení zahrnutá do skupiny jsou ve skutečnosti zaregistrovaná do automatického pilotního projektu.
    - Pokud chcete vytvořit skupinu, která zahrnuje všechna vaše zařízení autopilota, zadejte: `(device.devicePhysicalIDs -any _ -contains "[ZTDId]")`
    - Pole značky skupiny v Intune se mapuje na atribut ČísloObjednávky na zařízeních Azure AD. Pokud chcete vytvořit skupinu, která bude obsahovat všechna vaše zařízení autopilotu s konkrétní značkou skupiny (ČísloObjednávky pro zařízení Azure AD), musíte zadat: `(device.devicePhysicalIds -any _ -eq "[OrderID]:179887111881")`
    - Pokud chcete vytvořit skupinu, která obsahuje všechna vaše zařízení Autopilot s konkrétním ID nákupní objednávky, zadejte: `(device.devicePhysicalIds -any _ -eq "[PurchaseOrderId]:76222342342")`
    
    Po přidání kódu do pole **Pokročilé pravidlo** zvolte **Uložit**.
5. Zvolte **Vytvořit**.  

## <a name="create-an-autopilot-deployment-profile"></a>Vytvořit profil nasazení Autopilotu
Profily nasazení Autopilotu slouží ke konfiguraci zařízení s AutoPilotem. Můžete vytvořit až 350 profilů na každého tenanta.
1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení** > **Windows** > **Windows** > **profily nasazení profily** > **vytvořit profil**.
2. Na stránce **základy** zadejte **název** a volitelný **Popis**.

    ![Snímek stránky základy](./media/enrollment-autopilot/create-profile-basics.png)

3. Pokud chcete, aby se všechna zařízení v přiřazených skupinách automaticky převedla na Autopilot, nastavte možnost **Převést všechna cílová zařízení na Autopilot** na **Ano**. Všechna vlastněná podniková zařízení, která nejsou v přiřazených skupinách, se budou registrovat v rámci služby nasazení autopilotu. Zařízení v osobním vlastnictví nebudou převedena na autopilot. Vyřízení registrace trvá 48 hodin. Jakmile bude registrace zařízení zrušena a zařízení bude resetováno, Autopilot ho zaregistruje. Jakmile se zařízení tímto způsobem zaregistruje, nedojde zakázáním této možnosti ani odebráním přiřazení profilu k odebrání zařízení ze služby nasazení Autopilot. [Zařízení musíte odebrat přímo](enrollment-autopilot.md#delete-autopilot-devices).
4. Vyberte **Další**.
5. Na stránce spouštěné při **prvním spuštění počítače (OOBE)** pro **režim nasazení**vyberte jednu z těchto dvou možností:
    - **Řízení uživatelem**: Zařízení s tímto profilem se přidruží k uživateli, který zařízení registruje. Při registraci zařízení se musí zadat přihlašovací údaje uživatele.
    - **Samoobslužné nasazování (Preview)** : (vyžaduje zařízení s Windows 10, verze 1809 nebo novější), která s tímto profilem nejsou přidružená k uživateli, který registruje zařízení. Při registraci zařízení se nevyžadují přihlašovací údaje uživatele. Pokud k zařízení není přidružený žádný uživatel, zásady dodržování předpisů na základě uživatele se na něj nevztahují. Při použití režimu samostatného nasazení se použijí jenom zásady dodržování předpisů, které cílí na toto zařízení.

    ![Snímek obrazovky se stránkou OOBE](./media/enrollment-autopilot/create-profile-outofbox.png)

   > [!NOTE]
   > Vybrané režimy nasazení aktuálně nepodporují možnosti, které se zobrazují šedě nebo jsou vystínované.

6. V poli **Připojit k Azure AD jako** zvolte **Připojeno k Azure AD**.
7. Nakonfigurujte tyhle možnosti:
    - **Licenční smlouva s koncovým uživatelem (EULA)** : (Windows 10 verze 1709 nebo novější) Vyberte, jestli se má uživatelům zobrazit EULA.
    - **Nastavení ochrany osobních údajů**: Vyberte, jestli se mají uživatelům zobrazit nastavení ochrany osobních údajů.
    >[!IMPORTANT]
    >Výchozí hodnota pro nastavení diagnostických dat se liší mezi verzemi systému Windows. U zařízení s Windows 10 verze 1903 je výchozí hodnota nastavená na úplné během nastavování předem připraveného prostředí. Další informace najdete v tématu [diagnostická data Windows](https://docs.microsoft.com/windows/privacy/windows-diagnostic-data) . <br>
    
    - **Skrýt změnu možností účtu (vyžaduje Windows 10 verze 1809 nebo novější)** : Pokud chcete zabránit tomu, aby se možnosti změny účtu zobrazovaly na stránce pro přihlášení a na chybové stránky domény, vyberte **Skrýt** . Tato možnost vyžaduje, [aby v Azure Active Directory byla nakonfigurována funkce Branding společnosti](https://docs.microsoft.com/azure/active-directory/fundamentals/customize-branding).
    - **Typ uživatelského účtu**: Vyberte typ účtu uživatele (**Správce** nebo **Standardní** uživatel). Umožníme uživateli připojit se k zařízení jako místní správce přidáním do místní skupiny správců. Nepovolujeme uživatele jako výchozího správce na zařízení.
    - **Povolit White šetrnější OOBE** (vyžaduje Windows 10 verze 1903 nebo novější; [další fyzické požadavky](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove#prerequisites)): Pokud chcete povolit podporu bílé šetrnější, vyberte **Ano** .
    - **Použít šablonu názvu zařízení** (vyžaduje Windows 10, verze 1809 nebo novější a typ připojení Azure AD): Pokud chcete vytvořit šablonu, která se použije při pojmenování zařízení během registrace, klikněte na **Ano** . Názvy musí být maximálně 15 znaků dlouhé a mohou obsahovat písmena, číslice a pomlčky. Nemohou být ale tvořené jen číslicemi. Pomocí [makra %SERIAL%](https://docs.microsoft.com/windows/client-management/mdm/accounts-csp) můžete přidat sériové číslo specifické pro určitý hardware. Nebo můžete použít [makro %RAND:x%](https://docs.microsoft.com/windows/client-management/mdm/accounts-csp), které přidá náhodný řetězec číslic (x značí počet přidaných číslic). V [profilu připojení k doméně](windows-autopilot-hybrid.md#create-and-assign-a-domain-join-profile)můžete zadat jenom předběžnou opravu pro hybridní zařízení. 
    - **Jazyk (oblast)** \*: Zvolte jazyk, který chcete použít pro dané zařízení. Tato možnost je k dispozici, jen pokud jste si pro **Režim nasazení** zvolili **Nasazení sebou samým**.
    - **Automaticky konfigurovat\*klávesnice** : Pokud je vybraná možnost **jazyk (oblast)** , můžete stránku výběr klávesnice přeskočit kliknutím na **tlačítko Ano** . Tato možnost je k dispozici, jen pokud jste si pro **Režim nasazení** zvolili **Nasazení sebou samým**.
8. Vyberte **Další**.
9. Na stránce **značky oboru** můžete volitelně přidat značky oboru, které chcete použít pro tento profil. Další informace o značkách oboru najdete v tématu [použití značek řízení přístupu na základě role a rozsahu pro distribuci IT](../fundamentals/scope-tags.md).
10. Vyberte **Další**.
11. Na stránce **přiřazení** vyberte **vybrané skupiny** pro **přiřazení**.

    ![Snímek obrazovky se stránkou přiřazení](./media/enrollment-autopilot/create-profile-assignments.png)

12. Zvolte **Vybrat skupiny, které se mají zahrnout**, a zvolte skupiny, které chcete zahrnout do tohoto profilu.
13. Pokud chcete vyloučit jakékoli skupiny, zvolte **Vybrat skupiny, které se mají vyloučit**, a zvolte skupiny, které chcete vyloučit.
14. Vyberte **Další**.
15. Na stránce **Revize + vytvořit** vyberte **vytvořit** a vytvořte profil.

    ![Snímek obrazovky se stránkou Revize](./media/enrollment-autopilot/create-profile-review.png)

> [!NOTE]
> Intune bude pravidelně kontrolovat nová zařízení v přiřazených skupinách a pak začít proces přiřazování profilů těmto zařízením. Dokončení tohoto procesu může trvat několik minut. Před nasazením zařízení se ujistěte, že tento proces byl dokončen.  V části **zařízení** ** >  > Windows se** můžete **zaregistrovat > ** **zařízení** (v části **program Windows autopilot Deployment** , kde byste měli vidět změnu stavu profilu z "Nepřiřazeno" na "přiřazení" a nakonec na "přiřazeno".

## <a name="edit-an-autopilot-deployment-profile"></a>Úprava profilu nasazení Autopilotu
Po vytvoření profilu nasazení Autopilotu můžete některé části profilu nasazení upravit.   

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení** > **Windows** > **Windows** > **profily nasazení**.
2. Vyberte profil, který chcete upravit.
3. Vyberte **vlastnosti** vlevo a změňte název nebo popis profilu nasazení. Po provedení změn klikněte na **Uložit**.
5. Pokud chcete provést změny nastavení softwaru spuštěného při prvním zapnutí zařízení, klikněte na **Nastavení**. Po provedení změn klikněte na **Uložit**.

> [!NOTE]
> Změny profilu se použijí na zařízeních, která jsou přiřazena k tomuto profilu. Aktualizovaný profil se ale nepoužije na zařízení, které je už v Intune zaregistrované, dokud se zařízení neresetuje a znovu nezaregistruje.

## <a name="edit-autopilot-device-attributes"></a>Upravit atributy zařízení autopilotu
Po nahrání zařízení s autopilotem můžete upravit určité atributy zařízení.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení** > **Windows** > **Windows** > **zařízení** (v části **program Windows autopilot Deployment**.
2. Vyberte zařízení, které chcete upravit.
3. V podokně na pravé straně obrazovky můžete upravit název zařízení, značku skupiny nebo popisný název uživatele (Pokud jste přiřadili uživatele).
4. Vyberte **Uložit**.

> [!NOTE]
> Názvy zařízení je možné nakonfigurovat pro všechna zařízení, ale v hybridních nasazeních připojených k Azure AD se ignorují. Název zařízení se pořád nachází z profilu připojení k doméně pro hybridní zařízení Azure AD.

## <a name="alerts-for-windows-autopilot-unassigned-devices-----163236---"></a>Výstrahy pro zařízení s nepřiřazeným autopilotem Windows autopilot  <!-- 163236 -->  

Upozornění zobrazí, kolik zařízení programu Autopilot nemá profily nasazení Autopilotu. Na základě informací v upozornění můžete vytvořit profily a přiřadit je potřebným zařízením. Když na upozornění kliknete, zobrazí se úplný seznam zařízení Windows Autopilotu a podrobné informace o zařízeních.

Pokud chcete zobrazit výstrahy pro Nepřiřazená zařízení, [v centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení** > **Přehled** > **výstrahy registrace** > **Nepřiřazená zařízení**.  

## <a name="autopilot-deployments-report"></a>Sestava nasazení autopilotu
Můžete si Zobrazit podrobnosti o každém zařízení nasazeném pomocí Windows autopilotu.
Sestavu zobrazíte tak, že přejdete do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431), zvolíte **zařízení** > **monitorovat** > **nasazení autopilotu**.
Data jsou k dispozici po dobu 30 dnů od nasazení.

Tato sestava je ve verzi Preview. Záznamy nasazení zařízení se aktuálně spouštějí jenom novými událostmi registrace v Intune. To znamená, že tato sestava neodebere jakékoli nasazení, které neaktivuje nový zápis Intune. To zahrnuje jakýkoliv typ resetování, který zachovává registraci, a uživatelskou část s bílým šetrnějšíem autopilotu.

## <a name="assign-a-user-to-a-specific-autopilot-device"></a>Přiřazení uživatele ke konkrétnímu zařízení Autopilot

K zařízení Autopilot můžete přiřadit uživatele. Díky přiřazení se během instalace systému Windows uživatel předem vyplní na přihlašovací stránce s [firemním brandingem](https://docs.microsoft.com/azure/active-directory/fundamentals/customize-branding) ze služby Azure Active Directory. Také můžete nastavit vlastní uvítací název. Ten se předem nevyplňuje, ani neupravuje přihlašování ve Windows. Způsobem popsaným níže lze přiřadit jen uživatele s licencí pro službu Intune.

Požadavky: Azure Active Directory Portál společnosti byl nakonfigurován a Windows 10 verze 1809 nebo novější.

> [!NOTE]
> Pokud používáte službu AD FS, přiřazení uživatele ke konkrétnímu zařízení s autopilotem nefunguje.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení** > **Windows** > **Windows** > **zařízení** (v části **program Windows autopilot Deployment** > vyberte zařízení > **přiřadit uživatele**.

    ![Snímek obrazovky s možností Přiřadit uživatele](./media/enrollment-autopilot/assign-user.png)

2. Vyberte uživatele Azure s licencí pro používání služby Intune a zvolte **Vybrat**.

    ![Snímek obrazovky s vybraným uživatelem](./media/enrollment-autopilot/select-user.png)

3. V poli **Jednoduchý název** zadejte jednoduchý popisný název, nebo přijměte výchozí návrh. Tento řetězec je popisný název, který se zobrazí, když se uživatel přihlásí během instalace systému Windows.

    ![Snímek obrazovky s popisným názvem](./media/enrollment-autopilot/friendly-name.png)

4. Vyberte **OK**.


## <a name="delete-autopilot-devices"></a>Odstranění zařízení Autopilot

Můžete odstranit zařízení Windows autopilot, která nejsou zaregistrovaná v Intune:

- Odstraňte zařízení z Windows autopilotu na **zařízeních** > **windows** > **Windows** > **Devices** (v části **program pro nasazení Windows autopilotu**. Vyberte zařízení, která chcete odstranit, a pak zvolte **Odstranit**. Dokončení odstraňování zařízení Windows autopilotu může trvat několik minut.

Úplné odebrání zařízení z vašeho tenanta vyžaduje, abyste odstranili zařízení Intune, zařízení Azure Active Directory a záznamy zařízení Windows autopilot. To se dá udělat z Intune:

1. Pokud jsou zařízení zaregistrovaná v Intune, musíte je nejdřív [Odstranit v okně Intune všechna zařízení](../remote-actions/devices-wipe.md#delete-devices-from-the-azure-active-directory-portal).

2. Odstraňte zařízení v zařízeních **Azure Active Directory v zařízeních > ** **zařízeních Azure AD**.

3. Odstraňte zařízení z Windows autopilotu na **zařízeních** > **windows** > **Windows** > **Devices** (v části **program Windows autopilot Deployment** >. Vyberte zařízení, která chcete odstranit, a pak zvolte **Odstranit**. Dokončení odstraňování zařízení Windows autopilotu může trvat několik minut.

## <a name="using-autopilot-in-other-portals"></a>Použití Autopilotu na jiných portálech
Pokud nemáte zájem o správu mobilních zařízení, můžete Autopilot používat na jiných portálech. I když je používání na jiných portálech možné, doporučujeme ke správě nasazení Autopilotu používat jenom Intune. Pokud používáte Intune a jiný portál, nemůže Intune:  

- Zobrazit změny v profilech vytvořených v Intune, ale upravených na jiném portálu
- Synchronizovat profily vytvořené na jiném portálu
- Zobrazit změny v přiřazeních profilu provedených na jiném portálu
- Synchronizovat přiřazení profilu provedená na jiném portálu
- Zobrazit změny v seznamu zařízení, které byly provedeny na jiném portálu

## <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot pro existující zařízení

Zařízení s Windows můžete seskupit podle ID korelátoru, pokud se registrují s použitím [Autopilotu pro existující zařízení](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) v nástroji Configuration Manager. ID korelátoru je parametr konfiguračního souboru Autopilotu. [Atribut enrollmentProfileName zařízení služby Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices) se automaticky nastaví tak, aby odpovídal nastavení OfflineAutopilotprofile-\<ID korelátoru\>. Umožní se tím, aby se vytvořily libovolné dynamické skupiny Azure AD na základě ID korelátoru pomocí atributu enrollmentprofileName.

>[!WARNING] 
> ID korelátoru není v Intune přednastavené, takže zařízení může ohlásit libovolné ID korelátoru. Pokud uživatel vytvoří ID korelace, které odpovídá autopilotu nebo názvu profilu Apple ADE, zařízení se přidá do jakékoli dynamické skupiny zařízení Azure AD na základě atributu enrollmentProfileName. Pokud se chcete tomuto konfliktu vyhnout:
> - Vytvářejte pravidla dynamických skupin vždy tak, aby se porovnávala *celá* hodnota atributu enrollmentProfileName.
> - Nikdy Nejmenujte autopilot nebo profily Apple ADE začínající na "OfflineAutopilotprofile-".

## <a name="next-steps"></a>Další kroky
Po konfiguraci Windows Autopilotu pro registrovaná zařízení s Windows 10 zjistěte, jak taková zařízení spravovat. Další informace najdete v článku [Co je správa zařízení v Microsoft Intune](../remote-actions/device-management.md).
