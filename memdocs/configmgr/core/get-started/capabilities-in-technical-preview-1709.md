---
title: Technical Preview 1709
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview verze 1709 pro Configuration Manager.
ms.date: 09/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3ef6bdc-a204-4c4c-a02f-2bd03f35183e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: bedb515c8446e13189fb84644bc0ce7563cc1574
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078766"
---
# <a name="capabilities-in-technical-preview-1709-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1709 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1709. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview. Před instalací této verze Technical Preview si přečtěte [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md) , abyste se seznámili se všeobecnými požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Známé problémy v této verzi Technical Preview:**
- **Aktualizace na verzi preview 1709 se nezdařila, pokud máte server lokality v pasivním režimu**. Pokud spouštíte verzi Preview 1706, 1707 nebo 1708 a máte [server primární lokality v pasivním režimu](capabilities-in-technical-preview-1706.md#site-server-role-high-availability), je nutné nejprve odinstalovat server lokality pasivního režimu, aby bylo možné úspěšně aktualizovat lokalitu verze Preview na verzi 1709. Server lokality v pasivním režimu můžete po spuštění lokality verze 1709 znovu nainstalovat.

  Postup odinstalace serveru lokality pasivního režimu:
  1. V konzole nástroje klikněte na **Správa** > **Přehled** > **Konfigurace** > **servery lokality a role systému lokality**a potom vyberte server lokality pasivního režimu.
  2. V podokně **role systému lokality** klikněte pravým tlačítkem na roli **serveru lokality** a pak zvolte **Odebrat roli**.
  3. Klikněte pravým tlačítkem na server lokality pasivního režimu a zvolte **Odstranit**.
  4. Po odinstalaci serveru lokality na aktivním serveru primární lokality restartujte službu **CONFIGURATION_MANAGER_UPDATE**.


**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  

## <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Vylepšené možnosti profilů VPN v konzole Configuration Manager
<!-- 1313282 -->
V této verzi jsme aktualizovali Průvodce profilem sítě VPN a stránky vlastností, aby se zobrazila nastavení vhodná pro vybranou platformu. Konkrétně:

- Každá platforma má svůj vlastní pracovní postup, což znamená, že nové profily sítě VPN obsahují pouze nastavení podporovaná platformou.
- Stránky **podporované platformy** se nyní zobrazí po stránce **Obecné** .  Nyní si zvolíte platformu před nastavením hodnot vlastností.
- Když je platforma nastavená na **Android**, **Android for Work**nebo **Windows Phone 8,1**, stránka **podporované platformy** není potřeba a není zobrazená.
- Configuration Manager pracovní postup založený na klientech se spojil s pracovními postupy Windows 10 na základě klientů hybridního mobilního zařízení (MDM). podporují stejné nastavení.
- Každý pracovní postup platformy obsahuje jenom nastavení vhodná pro tento pracovní postup.  Například pracovní postup Androidu obsahuje nastavení vhodná pro Android. nastavení vhodná pro iOS nebo Windows 10 Mobile se už nezobrazí v pracovním postupu Android.
- U Windows 8.1 zařízení jsou nastavení spravovaná pomocí Configuration Manager jasně označená.
- Stránka automatické sítě VPN je zastaralá a byla odebrána.

Tyto změny platí pro nové profily sítě VPN.  

Kvůli minimalizaci rizika kompatibility se stávající profily sítě VPN nezměnily.  Když upravujete existující profil, nastavení se zobrazí stejně jako při vytvoření profilu.  

### <a name="try-it-out"></a>Určitě to udělejte!

Pomocí běžného procesu vytvořte nový profil VPN. Všimněte si, že se změnila první stránka v možnostech Průvodce profilem sítě VPN.

1. Přejděte na **prostředky a kompatibilita** > **Přehled** > **Nastavení** > dodržování předpisů > **přístup k prostředkům společnosti****Profily sítě VPN** a pak zvolte **vytvořit profil sítě VPN**.
2. Zadejte název na stránce **Obecné** a v části **Zadejte typ profilu sítě VPN, který chcete vytvořit**, vyberte jednu z následujících možností:

    - Windows 10  
    - Windows 8.1  
    - Windows Phone 8.1  
    - iOS a macOS  
    - Android  
    - Android for Work  

3. Zvolíte-li možnost **Windows 8.1**, máte také možnost **vytvořit nový profil** nebo **Importovat ze souboru**.
4. Dokončete Průvodce vytvořením profilu.

Při výběru různých platforem si všimněte, že se zobrazí pouze nastavení relevantní pro vybranou platformu.

## <a name="co-management-for-windows-10-devices"></a>Spoluspráva pro zařízení s Windows 10    
<!-- 1350871 -->
Mnoho zákazníků chce spravovat zařízení s Windows 10 stejným způsobem jako s tím, jak spravují mobilní zařízení, a to s využitím zjednodušeného cloudového řešení s nižšími náklady. Přechod z tradiční správy na moderní správu ale může být náročný. Od verze 1607 Windows 10 (označované také jako aktualizace pro výročí) můžete připojit zařízení s Windows 10 k místní službě Active Directory (AD) a cloudovou službu Azure AD ve stejnou dobu (hybridní služba Azure AD). Spoluspráva využívá toto vylepšení a umožňuje souběžně spravovat zařízení s Windows 10 pomocí Configuration Manager i Intune. Jedná se o řešení, které poskytuje přechod z tradičního na moderní správu a poskytuje cestu k převedení pomocí dvoufázového přístupu. 

### <a name="prerequisites"></a>Požadavky
Aby bylo možné povolit spolusprávu, je nutné, aby byly splněny následující předpoklady. Existují obecné požadavky a různé požadavky na stávající klienty Configuration Manager a zařízení, která nejsou klienty nástroje.

### <a name="known-issues"></a>Známé problémy
Když vytvoříte zásady spolusprávy, nebudete moct zásady upravovat. Pokud chcete zásadu změnit, odstraňte ji a pak ji znovu vytvořte s nastavením, které potřebujete. 

#### <a name="general-prerequisites"></a>Obecné požadavky
Níže jsou uvedené obecné předpoklady pro povolení spolusprávy:  

- Technical Preview pro Configuration Manager verze 1709
- Azure AD 
- Licence EMS nebo Intune pro všechny uživatele
- Předplatné Intune &#40;autoritu MDM v Intune nastavené na **Intune**&#41;

   > [!Note]  
   > Pokud máte hybridní prostředí MDM (integrovaný v Intune s Configuration Manager), nemůžete povolit spolusprávu.

#### <a name="additional-prerequisites-for-existing-configuration-manager-clients"></a>Další požadavky pro existující klienty Configuration Manager
- Windows 10 verze 1709 (aktualizace Creators Update) a novější
- Připojeno k hybridní službě Azure AD (připojeno k AD a Azure AD)

#### <a name="additional-prerequisites-for-new-windows-10-devices"></a>Další požadavky pro nová zařízení s Windows 10
- Windows 10 verze 1709 (aktualizace Creators Update) a novější
- [Brána pro správu cloudu](../clients/manage/manage-clients-internet.md#cloud-management-gateway) v Configuration Manager

### <a name="workloads-you-can-switch-to-intune"></a>Úlohy, které můžete přepnout do Intune
Po povolení spolusprávy Configuration Manager nadále spravovat všechny úlohy. Jakmile se rozhodnete, že jste připraveni, můžete v Intune začít spravovat dostupné úlohy. V této verzi můžete Intune spravovat následující úlohy.   

#### <a name="compliance-policies"></a>Compliance zásady
Zásady dodržování předpisů definují pravidla a nastavení, která musí zařízení dodržovat, aby se dalo považovat za zařízení, které dodržuje zásady podmíněného přístupu. Zásady dodržování předpisů můžeme používat i k monitorování a opravám problémů s dodržováním předpisů u zařízení, a to nezávisle na podmíněném přístupu.

#### <a name="windows-update-for-business-policies"></a>Zásady web Windows Update pro firmy
Zásady web Windows Update pro firmy umožňují nakonfigurovat zásady odložení pro aktualizace funkcí Windows 10 nebo aktualizace kvality pro zařízení s Windows 10 spravovaná přímo pomocí web Windows Update pro firmy. Podrobnosti najdete v tématu [Konfigurace zásad odložení web Windows Update pro firmy](https://docs.microsoft.com/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).  

### <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Vzdálené akce dostupné v Intune v Azure pro spoluspravovaná zařízení
Pokud je pro spolusprávu povolený zařízení s Windows 10, máte k dispozici následující vzdálené akce z Intune v Azure:  
- [Obnovení továrního nastavení](https://docs.microsoft.com/intune/devices-wipe#wipe)
- [Selektivní vymazání](https://docs.microsoft.com/intune/apps-selective-wipe)
- [Odstranit zařízení](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [Restartování zařízení](https://docs.microsoft.com/intune/device-restart)
- [Nový Start](https://docs.microsoft.com/intune/device-fresh-start)

### <a name="prepare-intune-for-co-management"></a>Příprava Intune pro spolusprávu
Než přepnete úlohy z Configuration Manager do Intune, vytvořte profily a zásady, které v Intune potřebujete, abyste zajistili, že budou vaše zařízení dál chráněná.
V Intune můžete vytvářet objekty, které jsou založené na objektech, které máte v Configuration Manager. Nebo pokud je vaše aktuální strategie založená na starší nebo tradiční správě, můžete si projít krok zpátky a znovu se rozhodnout, jaké zásady a profily budete potřebovat pro moderní správu. Pomocí následujících zdrojů Vytvořte zásady a profily.    
<!-- - [Device compliance policies](https://docs.microsoft.com/intune/compliance-policy-create-windows)  -->
- [Zásady web Windows Update pro firmy](https://docs.microsoft.com/intune/windows-update-for-business-configure)  
- [Konfigurační profily zařízení](https://docs.microsoft.com/intune/device-profile-create)  

### <a name="architectural-overview-for-co-management"></a>Přehled architektury pro spolusprávu
Následující diagram znázorňuje architekturu pro spolusprávu a způsob, jakým se zapadá do stávajících infrastruktur konfigurace a Intune.

![Diagram architektury spolusprávy](./media/co-management-arch-cm1709tp.svg)

### <a name="scenarios-to-enable-co-management"></a>Scénáře, jak povolit spolusprávu  
Spolusprávu můžete povolit pro zařízení s Windows 10 zaregistrovaná v Microsoft Intune a stávající klienti Configuration Manager Windows 10. Výsledkem obou scénářů je, že zařízení s Windows 10 jsou souběžně spravovaná pomocí Configuration Manager a Intune a také připojena k AD a Azure AD.  

#### <a name="devices-enrolled-in-intune"></a>Zařízení zaregistrovaná v Intune  
Když jsou zařízení s Windows 10 registrovaná v Intune, můžete nainstalovat klienta Configuration Manager do zařízení (pomocí konkrétního argumentu příkazového řádku) a připravit tak klienty pro spolusprávu. Pak můžete povolit spolusprávu z konzoly Configuration Manager a začít přesouvat konkrétní úlohy do Intune pro konkrétní zařízení s Windows 10.  

Pro zařízení s Windows 10, která ještě nejsou zaregistrovaná v Intune, můžete k registraci zařízení použít automatickou registraci v Azure. Pro nová zařízení s Windows 10 můžete pomocí automatického pilotního nasazení systému Windows nakonfigurovat funkci out-of-box (OOBE), která zahrnuje automatický zápis, který registruje zařízení v Intune.  

#### <a name="configuration-manager-clients"></a>Configuration Manager klienti
Pokud máte zařízení s Windows 10, která jsou Configuration Manager klienty, můžete tato zařízení zaregistrovat a povolit spolusprávu z konzoly Configuration Manager. Configuration Manager aktivuje automatický zápis do Intune na základě informací o tenantovi Azure AD.  

### <a name="prepare-windows-10-devices-for-co-management"></a>Příprava zařízení s Windows 10 na spolusprávu
Můžete povolit spolusprávu na zařízeních s Windows 10, která jsou připojená ke službě AD a Azure AD a zaregistrovaná v Intune a klientovi v Configuration Manager. Pro nová zařízení s Windows 10 a pro zařízení, která jsou už zaregistrovaná v Intune, nainstalujte klienta Configuration Manager, aby bylo možné ho spravovat společně. U zařízení s Windows 10, která už Configuration Manager klientů, můžete zařízení zaregistrovat v Intune a povolit spolusprávu v konzole Configuration Manager.

#### <a name="command-line-to-install-configuration-manager-client"></a>Příkazový řádek pro instalaci klienta Configuration Manager
Vytvořte aplikaci v Intune pro zařízení s Windows 10, která ještě nejsou Configuration Manager klienty. Při vytváření aplikace v dalších částech použijte následující příkazový řádek:

CCMSetup. msi CCMSETUPCMD = "/MP: &#60;*Adresa URL koncového bodu vzájemného ověření brány pro správu cloudu*&#62;/CCMHOSTNAME =&#60;*URL koncového bodu vzájemného ověření brány pro správu cloudu*&#62; SMSSiteCode =&#60;*SiteCode*&#62; SMSMP = https: &#47;/&#60;*plně kvalifikovaný název domény MP*&#62; AADTENANTID =&#60;*ID TENANTA AAD*&#62; AADTENANTNAME =&#60;*název klienta*&#62; AADCLIENTAPPID =&#60;*Server AppID pro integraci AAD*&#62; AADRESOURCEURI = https: &#47; */&#60;*

Například pokud máte následující hodnoty:

- **Adresa URL koncového bodu vzájemného ověření brány pro správu cloudu**: https:/&#47;contoso.cloudapp.NET/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >Použijte hodnotu **MutualAuthPath** v zobrazení **VProxy_Roles** SQL pro **adresu URL koncového bodu vzájemného ověření brány pro správu cloudu** .

- **Plně kvalifikovaný název domény bodu správy (MP)**: sccmmp.corp.contoso.com    
- **Kód lokality**: ps1    
- **ID tenanta Azure AD**: 72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- **Název tenanta Azure AD**: contoso    
- **ID aplikace klienta Azure AD**: bef323b3-042F-41a6-907A-f9faf0d1XXXX     
- **Identifikátor URI ID prostředku AAD**: ConfigMgrServer    

  > [!Note]    
  > Pro hodnotu **identifikátoru URI ID prostředku AAD** použijte hodnotu **IdentifierUri** , kterou najdete v zobrazení **vSMS_AAD_Application_Ex** SQL.

Použijte následující příkazový řádek:

CCMSetup. msi CCMSETUPCMD = "/MP: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 CCMHOSTNAME = contoso. cloudapp. NET/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode = PS1 SMSMP = https:/&#47;sccmmp.corp.contoso.com AADTENANTID = 72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME = contoso AADCLIENTAPPID = bef323b3-042F-41a6-907a-f9faf0d1XXXX AADRESOURCEURI = https:/&#47;ConfigMgrServer"

> [!Tip]
>Parametry příkazového řádku pro váš web můžete najít pomocí následujících kroků:     
> 1. V konzole Configuration Manager klikněte na **Správa** > **Přehled** > **Cloud Services** > **spoluspráva**.  
> 2. Na kartě Domů ve skupině spravovat vyberte možnost **Konfigurovat spolusprávu** a otevřete tak Průvodce připojování spoluspráva.    
> 3. Na stránce Předplatné klikněte na **Přihlásit** se a přihlaste se k tenantovi Intune a potom klikněte na **Další**.    
> 4. Na stránce zapnout klikněte na **Kopírovat** v části **zařízení zaregistrovaná v Intune** , abyste zkopírovali příkazový řádek do schránky a pak jste příkazový řádek uložili, abyste ho mohli použít v postupu vytvoření aplikace.  
> 5. Kliknutím na tlačítko **Storno** ukončíte průvodce.

#### <a name="new-windows-10-devices"></a>Nová zařízení s Windows 10
Pro nová zařízení s Windows 10 můžete použít službu autopilotu ke konfiguraci nedostatku možnosti, která zahrnuje připojení zařízení ke službě AD a Azure AD, a registraci zařízení v Intune. Pak vytvořte v Intune aplikaci, která nasadí klienta Configuration Manager.  
1. Povolit autopilot pro nová zařízení s Windows 10. Podrobnosti najdete v tématu [Přehled Windows Autopilotu](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).  
2. Nakonfigurujte automatickou registraci v Azure AD, aby se vaše zařízení automaticky zaregistrovala do Intune. Podrobnosti najdete v tématu [registrace zařízení s Windows pro Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).
3. Vytvořte aplikaci v Intune s Configuration Manager klientským balíčkem a nasaďte aplikaci do zařízení s Windows 10, která chcete spoluspravovat. Pomocí [příkazového řádku můžete nainstalovat klienta Configuration Manager](#command-line-to-install-configuration-manager-client) , když projdete kroky pro [instalaci klientů z Internetu pomocí Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure).   

#### <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Zařízení s Windows 10, která nejsou zaregistrovaná v Intune nebo klientovi Configuration Manager
Pro zařízení s Windows 10, která nejsou zaregistrovaná v Intune nebo mají klienta Configuration Manager, můžete k registraci zařízení v Intune použít automatickou registraci. Pak vytvořte v Intune aplikaci, která nasadí klienta Configuration Manager.
1. Nakonfigurujte automatickou registraci v Azure AD, aby se vaše zařízení automaticky zaregistrovala do Intune. Podrobnosti najdete v tématu [registrace zařízení s Windows pro Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  
2. Vytvořte aplikaci v Intune s Configuration Manager klientským balíčkem a nasaďte aplikaci do zařízení s Windows 10, která chcete spoluspravovat. Pomocí [příkazového řádku můžete nainstalovat klienta Configuration Manager](#command-line-to-install-configuration-manager-client) , když projdete kroky pro [instalaci klientů z Internetu pomocí Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure).

#### <a name="windows-10-devices-enrolled-in-intune"></a>Zařízení s Windows 10 zaregistrovaná v Intune
U zařízení s Windows 10, která jsou už zaregistrovaná v Intune, vytvořte v Intune aplikaci, která nasadí klienta Configuration Manager. Pomocí [příkazového řádku můžete nainstalovat klienta Configuration Manager](#command-line-to-install-configuration-manager-client) , když projdete kroky pro [instalaci klientů z Internetu pomocí Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

### <a name="switch-configuration-manager-workloads-to-intune"></a>Přepnutí úloh Configuration Manageru do Intune
V předchozí části jste připravili zařízení s Windows 10 pro spolusprávu. Tato zařízení jsou teď připojená ke službě AD a Azure AD a jsou zaregistrovaná v Intune a musí mít klienta Configuration Manager. Máte pravděpodobně stále zařízení s Windows 10, která jsou připojená ke službě AD a mají klienta Configuration Manager, ale nejsou připojeni k Azure AD nebo zaregistrovali v Intune. Následující postup slouží k povolení spolusprávy, přípravě zbývajících zařízení s Windows 10 (Configuration Manager klientů bez registrace Intune) pro spolusprávu a umožňuje začít přepínat konkrétní Configuration Manager úlohy do Intune.

1. V konzole Configuration Manager klikněte na **Správa** > **Přehled** > **Cloud Services** > **spoluspráva**.    
2. Na kartě Domů ve skupině spravovat vyberte možnost **Konfigurovat spolusprávu** a otevřete tak Průvodce připojování spoluspráva.    
3. Na stránce Předplatné klikněte na **Přihlásit** se a přihlaste se k tenantovi Intune a potom klikněte na **Další**.   
4. Na stránce Příprava nakonfigurujte následující nastavení a potom klikněte na tlačítko **Další**:
    - **Pilotní skupina**: pilotní skupina obsahuje jednu nebo více kolekcí, které vyberete. Tuto skupinu použijte jako součást dvoufázové zavedení spolusprávy. Můžete začít s malým testovacím kolekcí a potom do pilotní skupiny přidat další kolekce při zavádění spolusprávy na více uživatelů a zařízení. Kolekce v pilotní skupině můžete kdykoli změnit z vlastností spolusprávy.
    - **Produkce**: Když vyberete toto nastavení, všechna podporovaná zařízení s Windows 10 jsou povolená pro spolusprávu. Nakonfigurujte **skupinu vyloučení** s jednou nebo více kolekcemi. Zařízení, která jsou členem některé z kolekcí v této skupině, se z použití spolusprávy vylučují. 
5. Na stránce povolení zvolte buď **pilotní nasazení** , nebo **vše** (v závislosti na nastaveních, která jste nakonfigurovali na pracovní stránce) a povolte v Intune automatický zápis, a pak klikněte na **Další**. Když zvolíte **pilotní nasazení**, do Intune se automaticky zaregistrují jenom klienti Configuration Manageru, kteří jsou členy pilotní skupiny. Díky tomu můžete povolit spolusprávu u podmnožiny klientů pro prvotní testování spolusprávy a zavedení spolusprávy pomocí dvoufázového přístupu. 
6. Na stránce úlohy vyberte, jestli se mají přepínat Configuration Manager úlohy, které se mají spravovat přes Intune, a pak klikněte na **Další**. Pomocí posuvníků vyberte, jestli se má úloha přepnout na pilotní skupinu nebo pro všechny klienty Windows 10 (v závislosti na nastaveních, která jste nakonfigurovali na pracovní stránce). 
7. Pokud chcete povolit spolusprávu, dokončete průvodce.  

<!--### Modify your co-management settings
After you enable co-management using the wizard, you can modify your target group and change the workloads that are managed by Configuration Manager and Intune.  
- In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.  
Select the co-management object, and then on the Home tab, click **Properties**. -->   

<!--### Monitor co-management
After you have enabled co-management, you can monitor which devices are managed by Configuration Manager and which are managed by Intune. You can also see which Configuration Manager workloads are managed by which product.-->

## <a name="see-also"></a>Viz také
Informace o instalaci nebo aktualizaci větve Technical Preview najdete v tématu [Technical Preview pro Configuration Manager](technical-preview.md). 
