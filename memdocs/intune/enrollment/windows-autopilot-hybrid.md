---
title: Registrace pro zařízení připojená k hybridní službě Azure AD – Windows autopilot
titleSuffix: ''
description: Pomocí automatických pilotů Windows Zaregistrujte hybridní zařízení připojená k Azure AD v Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/01/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 8518d8fa-a0de-449d-89b6-8a33fad7b3eb
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: be9a4257fec357c3dc124318fda98807df6c26b7
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093488"
---
# <a name="deploy-hybrid-azure-ad-joined-devices-by-using-intune-and-windows-autopilot"></a>Nasazení hybridních zařízení připojených k Azure AD pomocí Intune a automatického pilotního projektu Windows
Pomocí Intune a Windows autopilotu můžete nastavit zařízení připojená k hybridnímu Azure Active Directory (Azure AD). Pokud to chcete provést, postupujte podle kroků v tomto článku.

## <a name="prerequisites"></a>Požadavky

[Zařízení připojená k hybridní službě Azure AD](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)se úspěšně nakonfigurovala. Ujistěte se, že [jste ověřili registraci zařízení](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains#verify-the-registration) pomocí rutiny Get-MsolDevice.

Zařízení, která chcete zaregistrovat, musí:
- S Windows 10 v1809 nebo novějším.
- Musí mít přístup k Internetu podle [dokumentovaných požadavků na síť Windows autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-requirements#networking-requirements).
- Mít přístup k řadiči domény služby Active Directory, musí být připojený k síti organizace (kde může přeložit záznamy DNS pro doménu AD a řadič domény služby AD) a komunikovat s řadičem domény za účelem ověření uživatele. Připojení VPN se v tuto chvíli nepodporuje.
- Být schopné testovat řadič domény domény, ke které se pokoušíte připojit.
- Pokud používáte proxy server, musí být povolená a nakonfigurovaná možnost nastavení proxy serveru WPAD.
- Absolvujte integrované prostředí (OOBE).
- Použijte typ ověřování, který Azure Active Directory podporuje v OOBE.


## <a name="set-up-windows-10-automatic-enrollment"></a>Nastavení automatické registrace pro Windows 10

1. Přihlaste se k Azure a v levém podokně vyberte **Azure Active Directory**.

   ![Azure Portal](./media/windows-autopilot-hybrid/auto-enroll-azure-main.png)

1. Vyberte **Mobilita (MDM a MAM)**.

   ![Podokno Azure Active Directory](./media/windows-autopilot-hybrid/auto-enroll-mdm.png)

1. Vyberte **Microsoft Intune**.

   ![Podokno mobility (MDM a MAM)](./media/windows-autopilot-hybrid/auto-enroll-intune.png)

1. Ujistěte se, že uživatelé, kteří nasazují zařízení připojená k Azure AD pomocí Intune a Windows, jsou členy skupiny, která je zahrnutá v **oboru uživatelů MDM**.

   ![Podokno konfigurace mobility (MDM a MAM)](./media/windows-autopilot-hybrid/auto-enroll-scope.png)

1. Použijte výchozí hodnoty v polích **adresa url podmínky použití MDM**, **Adresa URL zjišťování MDM**a **Adresa URL dodržování předpisů MDM** a pak vyberte **Uložit**.

## <a name="increase-the-computer-account-limit-in-the-organizational-unit"></a>Zvýšení limitu pro účty počítačů v organizační jednotce

Konektor Intune pro vaši službu Active Directory vytváří počítače registrované autopilotem v místní doméně služby Active Directory. Počítač, který je hostitelem konektoru Intune, musí mít práva k vytváření počítačových objektů v doméně. 

V některých doménách nejsou počítačům udělena práva k vytváření počítačů. Domény navíc mají předdefinované omezení (výchozí hodnota 10), které platí pro všechny uživatele a počítače, které nejsou delegovanými právy k vytváření počítačových objektů. Proto musí být práva delegovaná na počítače, které hostují konektor Intune na organizační jednotce, kde se vytvářejí zařízení připojená k hybridní službě Azure AD.

Organizační jednotka, která má udělena práva k vytváření počítačů, musí odpovídat:
- Organizační jednotka, která je zadána v profilu připojení k doméně.
- Pokud není vybraný žádný profil, název domény počítače pro vaši doménu.

1. Otevřete položku **Uživatelé a počítače služby Active Directory (DSA. msc)**.

1. Klikněte pravým tlačítkem na organizační jednotku, kterou budete používat k vytvoření hybridních počítačů připojených k Azure AD, a pak vyberte **delegovat řízení**.

    ![Příkaz ovládacího prvku Delegate](./media/windows-autopilot-hybrid/delegate-control.png)

1. V průvodci **delegováním řízení** vyberte **Další**  >  **Přidat**  >  **typy objektů**.

1. V podokně **typy objektů** zaškrtněte políčko **počítače** a pak vyberte **OK**.

    ![Podokno typy objektů](./media/windows-autopilot-hybrid/object-types-computers.png)

1. V podokně **Vybrat uživatele, počítače nebo skupiny** v poli **Zadejte názvy objektů k výběru** zadejte název počítače, ve kterém je konektor nainstalovaný.

    ![Podokno vybrat uživatele, počítače nebo skupiny](./media/windows-autopilot-hybrid/enter-object-names.png)

1. Vyberte **Zkontrolovat jména** a ověřte zadání, vyberte **OK**a pak vyberte **Další**.

1. Vyberte **vytvořit vlastní úlohu pro delegování**  >  **Další**.

1. Zaškrtněte políčko **pouze následující objekty ve složce** a potom vyberte **objekty počítače**, **vytvořte vybrané objekty v této složce**a zrušte zaškrtnutí políček **Odstranit vybrané objekty v této** složce.

    ![Podokno typu objektu služby Active Directory](./media/windows-autopilot-hybrid/only-following-objects.png)
    
1. Vyberte **Další**.

1. V části **oprávnění**zaškrtněte políčko **Úplné řízení** .  
    Tato akce vybere všechny ostatní možnosti.

    ![Podokno oprávnění](./media/windows-autopilot-hybrid/full-control.png)

1. Vyberte **Další**a pak vyberte **Dokončit**.

## <a name="install-the-intune-connector"></a>Instalace konektoru Intune

Konektor Intune pro službu Active Directory musí být nainstalovaný na počítači se systémem Windows Server 2016 nebo novějším. Počítač musí mít také přístup k Internetu a ke službě Active Directory. Chcete-li zvýšit rozsah a dostupnost, můžete nainstalovat více konektorů ve vašem prostředí. Doporučujeme nainstalovat konektor na server, na kterém neběží žádné jiné konektory Intune.  Všimněte si, že každý konektor musí být schopný vytvářet objekty počítače v libovolné doméně, kterou chcete podporovat.

Konektor Intune vyžaduje [stejné koncové body jako Intune](../fundamentals/intune-endpoints.md).

1. Vypnout konfiguraci rozšířeného zabezpečení aplikace Internet Explorer. Ve výchozím nastavení má Windows Server zapnutou konfiguraci rozšířeného zabezpečení aplikace Internet Explorer. Pokud se nemůžete přihlásit ke službě Intune Connector pro službu Active Directory, pak pro správce vypněte konfiguraci rozšířeného zabezpečení aplikace Internet Explorer. [Vypnutí konfigurace rozšířeného zabezpečení aplikace Internet Explorer](https://blogs.technet.microsoft.com/chenley/2011/03/10/how-to-turn-off-internet-explorer-enhanced-security-configuration). 
2. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **Windows**  >  **Windows registrace**  >  **Intune Connector pro Active Directory**  >  **Přidat**. 
3. Podle pokynů stáhněte konektor.
4. Otevřete instalační soubor staženého konektoru, *ODJConnectorBootstrapper.exe*pro instalaci konektoru.
5. Na konci instalace vyberte **Konfigurovat**.
6. Vyberte **Přihlásit se**.
7. Zadejte globální správce uživatele nebo přihlašovací údaje role správce Intune.  
   Uživatelský účet musí mít přiřazenou licenci Intune.
8. V části **zařízení**  >  **Windows**  >  **Windows registrace**  >  **konektoru Intune pro Active Directory**a potvrďte, že stav připojení je **aktivní**.

> [!NOTE]
> Po přihlášení ke konektoru může trvat několik minut, než se objeví v [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431). Zobrazuje se jenom v případě, že může úspěšně komunikovat se službou Intune.

### <a name="configure-web-proxy-settings"></a>Konfigurace nastavení webového proxy serveru

Pokud máte ve svém síťovém prostředí webový proxy server, ujistěte se, že konektor Intune pro službu Active Directory funguje správně, a to tak, že odkazuje na [práci se stávajícími místními proxy servery](autopilot-hybrid-connector-proxy.md).


## <a name="create-a-device-group"></a>Vytvoření skupiny zařízení
1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **skupiny**  >  **Nová skupina**.

1. V podokně **Skupina** postupujte takto:

    a. Jako **typ skupiny**vyberte **zabezpečení**.

    b. Zadejte **název skupiny** a **Popis skupiny**.

    c. Vyberte **typ členství**.

1. Pokud jste pro typ členství vybrali možnost **Dynamická zařízení** , vyberte v podokně **Skupina** možnost **Členové dynamického zařízení** a potom v poli **Upřesnit pravidlo** proveďte jednu z následujících akcí:
    - Pokud chcete vytvořit skupinu, která bude obsahovat všechna zařízení s vaším autopilotem, zadejte `(device.devicePhysicalIDs -any _ -contains "[ZTDId]")` .
    - Pole značky skupiny v Intune se mapuje na atribut ČísloObjednávky na zařízeních Azure AD. Pokud chcete vytvořit skupinu, která bude obsahovat všechna vaše zařízení autopilotu s konkrétní značkou skupiny (ČísloObjednávky), musíte zadat:`(device.devicePhysicalIds -any _ -eq "[OrderID]:179887111881")`
    - Pokud chcete vytvořit skupinu, která bude obsahovat všechna vaše zařízení autopilotu s určitým ID nákupní objednávky, zadejte `(device.devicePhysicalIds -any _ -eq "[PurchaseOrderId]:76222342342")` .
    
1. Vyberte **Uložit**.

1. Vyberte **Vytvořit**.  

## <a name="register-your-autopilot-devices"></a>Registrace zařízení Autopilot

Vyberte jeden z následujících způsobů registrace zařízení autopilotu.

### <a name="register-autopilot-devices-that-are-already-enrolled"></a>Registrace zařízení Autopilot, která jsou už zaregistrovaná

1. Vytvořte profil nasazení Autopilotu s možností **Převést všechna cílová zařízení na Autopilot** nastavenou na **Ano**. 
2. Přiřaďte profil ke skupině obsahující členy, které chcete automaticky zaregistrovat pomocí automatického pilotního projektu.

Další informace najdete v tématu [Vytvoření profilu nasazení Autopilotu](enrollment-autopilot.md#create-an-autopilot-deployment-profile).

### <a name="register-autopilot-devices-that-arent-enrolled"></a>Registrace zařízení Autopilot, která nejsou zaregistrovaná

Pokud zařízení ještě nejsou zaregistrovaná, můžete je zaregistrovat sami. Další informace najdete v tématu [Přidání zařízení](enrollment-autopilot.md#add-devices).

### <a name="register-devices-from-an-oem"></a>Registrace zařízení od výrobce OEM

Pokud kupujete nová zařízení, můžou někteří výrobci OEM zaregistrovat tato zařízení za vás. Další informace najdete na [stránce Windows Autopilot](https://aka.ms/WindowsAutopilot).

Po *registraci*zařízení s autopilotem, než se zaregistrují do Intune, se zobrazí na třech místech (s názvy nastavenými na jejich sériová čísla):
- Podokno **zařízení autopilot** v Intune v Azure Portal. Vyberte **registrace zařízení registrace**zařízení se  >  **systémem Windows**  >  **Devices**.
- Podokno **zařízení Azure AD** v Intune v Azure Portal. Vyberte **zařízení**zařízení  >  **Azure AD**.
- Podokno **Azure AD všechna zařízení** v Azure Active Directory v Azure Portal tak, že vyberete **zařízení**  >  **všechna zařízení**.

Po *registraci*zařízení autopilotu se zobrazí na čtyřech místech:
- Podokno **zařízení autopilot** v Intune v Azure Portal. Vyberte **registrace zařízení registrace**zařízení se  >  **systémem Windows**  >  **Devices**.
- Podokno **zařízení Azure AD** v Intune v Azure Portal. Vyberte **zařízení**zařízení  >  **Azure AD**.
- Podokno **všechna zařízení Azure AD** v Azure Active Directory v Azure Portal. Vyberte **zařízení**  >  **všechna zařízení**.
- Podokno **všechna zařízení** v Intune v Azure Portal. Vyberte **zařízení**  >  **všechna zařízení**.

Po registraci zařízení autopilotu se jejich názvy stanou názvem hostitele zařízení. Ve výchozím nastavení začíná název hostitele s *plochou*.


## <a name="create-and-assign-an-autopilot-deployment-profile"></a>Vytvoření a přiřazení profilu nasazení Autopilotu
Profily nasazení Autopilotu slouží ke konfiguraci zařízení s AutoPilotem.

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **Windows**  >  **Windows enrollment**  >  **profily nasazení**registrace Windows Windows  >  **vytvořit profil**.
2. Na stránce **základy** zadejte **název** a volitelný **Popis**.
3. Pokud chcete, aby se všechna zařízení v přiřazených skupinách automaticky převedla na Autopilot, nastavte možnost **Převést všechna cílová zařízení na Autopilot** na **Ano**. Všechna vlastněná podniková zařízení, která nejsou v přiřazených skupinách, se budou registrovat v rámci služby nasazení autopilotu. Zařízení v osobním vlastnictví nebudou převedena na autopilot. Vyřízení registrace trvá 48 hodin. Jakmile bude registrace zařízení zrušena a zařízení bude resetováno, Autopilot ho zaregistruje. Jakmile se zařízení tímto způsobem zaregistruje, nedojde zakázáním této možnosti ani odebráním přiřazení profilu k odebrání zařízení ze služby nasazení Autopilot. [Zařízení musíte odebrat přímo](enrollment-autopilot.md#delete-autopilot-devices).
4. Vyberte **Další**.
5. Na stránce spouštěné při **prvním spuštění počítače (OOBE)** pro **režim nasazení**vyberte možnost **řízeno uživatelem**.
6. V poli **připojit ke službě Azure AD** vyberte možnost **připojené k hybridní službě Azure AD**.
7. Pokud nasazujete zařízení ze sítě organizace s využitím podpory sítě VPN, nastavte možnost **Přeskočit možnosti připojení k doméně** na **Ano**.  Další informace najdete v tématu [režim založený na uživateli pro hybridní Azure Active Directory připojení k síti VPN](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven#user-driven-mode-for-hybrid-azure-active-directory-join-with-VPN-support) .
8. Podle potřeby konfigurujte zbývající možnosti na stránce s **počátečním prostředím (OOBE)** .
9. Vyberte **Další**.
10. Na stránce **značky oboru** vyberte [značky oboru](../fundamentals/scope-tags.md) pro tento profil.
11. Vyberte **Další**.
12. Na stránce **přiřazení** vyberte **možnost vybrat skupiny, které chcete zahrnout** > hledání, a vyberte skupinu zařízení > **Vybrat**.
13. Vyberte **Další**  >  **vytvořit**.

Změna stavu profilu zařízení z *nepřiřazeného* *přiřazení* a nakonec trvá přibližně 15 minut, *než se přiřadí.*

## <a name="optional-turn-on-the-enrollment-status-page"></a>Volitelné Zapnout stránku stavu registrace

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **Windows**  >  **Windows registrace registrace**  >  **stavová stránka**.
1. V podokně **Stránka stavu registrace** vyberte **výchozí**  >  **Nastavení**.
1. V poli **Zobrazit průběh instalace aplikace a profilu** vyberte **Ano**.
1. Nakonfiguruje další možnosti podle potřeby.
1. Vyberte **Uložit**.

## <a name="create-and-assign-a-domain-join-profile"></a>Vytvoření a přiřazení profilu připojení k doméně

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **Konfigurace profily**  >  **vytvořit profil**.
2. Zadejte tyto vlastnosti:
   - **Název**: Zadejte popisný název nového profilu.
   - **Popis**: Zadejte popis profilu.
   - **Platforma**: vyberte **Windows 10 a novější**.
   - **Typ profilu**: vyberte **připojení k doméně (Preview)**.
3. Vyberte **Nastavení**a potom zadejte **předponu názvu počítače**, **název domény**.
4. Volitelné Zadejte **organizační jednotku** (OU) ve [formátu DN](https://docs.microsoft.com/windows/desktop/ad/object-names-and-identities#distinguished-name). Mezi tyto možnosti patří:
   - Poskytněte organizační jednotku, ve které jste delegovani řízení na zařízení s Windows 2016, na kterém je spuštěný konektor Intune.
   - Poskytněte organizační jednotku, ve které jste delegovani řízení ke kořenovým počítačům ve službě Prem Active Directory.
   - Necháte-li toto pole prázdné, bude objekt počítače vytvořen v výchozím kontejneru služby Active Directory (CN = computers, pokud jste [jej nikdy nezměnili](https://support.microsoft.com/en-us/help/324949/redirecting-the-users-and-computers-containers-in-active-directory-dom)).
   
   Tady jsou některé platné příklady:
   - OU = úroveň 1, OU = Level2, DC = contoso, DC = com
   - OU = dolu, DC = contoso, DC = com
   
   Tady je několik příkladů, které nejsou platné:
   - CN = computers, DC = contoso, DC = com (kontejner nemůžete zadat, místo toho nechte tuto hodnotu prázdnou pro použití výchozí hodnoty pro doménu)
   - OU = moje (musíte zadat doménu přes atribut DC =)
     
   > [!NOTE]
   > Kolem hodnoty v **organizační jednotce**nepoužívejte uvozovky.
5. Vyberte **OK**  >  **vytvořit**.  
    Profil se vytvoří a zobrazí se v seznamu.
6. Pokud chcete profil přiřadit, postupujte podle kroků v části [přiřazení profilu zařízení](../configuration/device-profile-assign.md#assign-a-device-profile) a přiřazení profilu ke stejné skupině, kterou používá tento krok [vytvořit skupinu zařízení](windows-autopilot-hybrid.md#create-a-device-group). Případně můžete použít různé skupiny, pokud je potřeba připojovat zařízení k různým doménám nebo organizačním jednotkám.

> [!NOTE]
> Možnosti pojmenování pro automatické pilotní služby Windows pro připojení hybridní služby Azure AD nepodporují proměnné jako% SÉRIOVÉho% a podporují pouze předpony pro název počítače.

## <a name="next-steps"></a>Další kroky

Po konfiguraci Windows Autopilotu si přečtěte, jak tato zařízení spravovat. Další informace najdete v tématu [co je Správa zařízení Microsoft Intune?](../remote-actions/device-management.md).
