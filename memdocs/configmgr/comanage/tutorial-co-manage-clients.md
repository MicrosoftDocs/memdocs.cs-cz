---
title: Kurz&#58; povolení spolusprávy pro stávající klienty
titleSuffix: Configuration Manager
description: Nakonfigurujte spolusprávu pomocí Microsoft Intune, když už zařízení s Windows 10 spravujete pomocí Configuration Manager.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 918df2cded3fad48352fff6a2617b1133540c0eb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712425"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>Kurz: povolení spolusprávy pro stávající klienty Configuration Manager

Společně se správou můžete zajistit, aby se při správě počítačů ve vaší organizaci používaly Configuration Manager. Ve stejnou chvíli budete investovat do cloudu prostřednictvím použití Intune pro zabezpečení a moderní zřizování.  

V tomto kurzu nastavíte spolusprávu zařízení s Windows 10, která jsou už zaregistrovaná v Configuration Manager. Tento kurz začíná místním prostředím, které už používáte Configuration Manager ke správě zařízení s Windows 10.

Tento kurz použijte v těchto případech:  

- Máte místní službu Active Directory, ke které se můžete připojit Azure Active Directory (Azure AD) v hybridní konfiguraci služby Azure AD.

  Pokud nemůžete nasadit hybridní Azure Active Directory (AD), která se připojí k místní službě AD pomocí Azure AD, doporučujeme vám náš doprovodný kurz, který [umožní spolusprávu pro nová internetová zařízení s Windows 10](tutorial-co-manage-new-devices.md).
- Máte existující Configuration Manager klienty, ke kterým se chcete připojit ke cloudu.

**V tomto kurzu provedete tyto kroky:**  
> [!div class="checklist"]
> * Kontrola požadavků pro Azure a místní prostředí
> * Nastavení hybridní služby Azure AD  
> * Konfigurace agentů Configuration Manager klientů k registraci ve službě Azure AD  
> * Konfigurace Intune pro automatické registrace zařízení  
> * Povolit spolusprávu v Configuration Manager  

## <a name="prerequisites"></a>Požadavky  

### <a name="azure-services-and-environment"></a>Služby a prostředí Azure

- Předplatné Azure ([bezplatná zkušební verze](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Odběr služby Microsoft Intune
  > [!TIP]  
  > Předplatné Enterprise Mobility + Security (EMS) zahrnuje Azure Active Directory Premium i Microsoft Intune. Předplatné EMS ([bezplatná zkušební verze](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial))  

Pokud ve vašem prostředí ještě neexistují, budete během tohoto kurzu:

- Nakonfigurujte [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-select-installation) mezi vaší místní službou Active Directory a vaším klientem Azure Active Directory (AD).

> [!TIP]
> Už nemusíte kupovat a přiřazovat k vašim uživatelům jednotlivé licence Intune ani EMS. Další informace najdete v tématu [Nejčastější dotazy k produktu a licencování](../core/understand/product-and-licensing-faq.md#bkmk_mem).

### <a name="on-premises-infrastructure"></a>Místní infrastruktura

- [Podporovaná verze](../core/servers/manage/updates.md#supported-versions) Configuration Manager aktuální větve
- Autorita správy mobilních zařízení (MDM) musí být nastavená na Intune.  

### <a name="permissions"></a>Oprávnění

V celém tomto kurzu použijte následující oprávnění k dokončení úkolů:

- Účet, který je *globálním správcem* v Azure Active Directory (Azure AD) 
- Účet, který je *správcem domény* v místní infrastruktuře  
- Účet, který je *úplný správce* pro *všechny* obory v Configuration Manager

## <a name="set-up-hybrid-azure-ad"></a>Nastavení hybridní služby Azure AD

Když nastavíte hybridní službu Azure AD, opravdu nastavujete integraci místní služby AD se službou Azure AD pomocí Azure AD Connect a služby AD FS (Active Directory federovaným Services). Po úspěšné konfiguraci se vaši pracovníci můžou bezproblémově přihlašovat k externím systémům pomocí místních přihlašovacích údajů služby AD.

> [!IMPORTANT]  
> Tento kurz popisuje holé procesy pro nastavení hybridní služby Azure AD pro spravovanou doménu. Doporučujeme, abyste se s tímto procesem seznámili a Nespoléháte se na tento kurz, který vám pomůže pochopit a nasazovat hybridní službu Azure AD.
>
> Další informace o hybridní službě Azure AD najdete v následujících článcích v dokumentaci k Azure Active Directory:
>
> - [Plánování implementace připojení ke službě Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)
> - [Plánování implementace připojení k hybridní službě Azure AD](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)
> - [Řízení připojení vašich zařízení k hybridní službě Azure AD](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-control)
> - [Konfigurace připojení k hybridní službě Azure AD pro federované domény](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  

### <a name="set-up-azure-ad-connect"></a>Nastavit Azure AD Connect

Hybridní služba Azure AD vyžaduje konfiguraci Azure AD Connect pro udržování účtů počítačů v místní službě Active Directory (AD) a objekt zařízení v Azure AD v synchronizaci.

Azure AD Connect od verze 1.1.819.0 nabízí průvodce konfigurací hybridního připojení k Azure AD. Použití tohoto průvodce zjednodušuje proces konfigurace.  

Pokud chcete nakonfigurovat Azure AD Connect, budete potřebovat přihlašovací údaje globálního správce služby Azure AD.  

> [!TIP]  
> Následující postup by se neměl považovat za autoritativní pro nastavení Azure AD Connect, ale tady se poskytuje, aby se zjednodušila konfigurace spolusprávy mezi Intune a Configuration Manager. Autoritativní obsah v tomto a souvisejícím postupu pro nastavení služby Azure AD najdete v tématu [Konfigurace hybridního připojení k Azure AD pro spravované domény](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) v dokumentaci k Azure AD.  

#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>Konfigurace připojení k hybridní službě Azure AD pomocí Azure AD Connect

1. Získejte a nainstalujte [nejnovější verzi Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 nebo novější).  
2. Spusťte Azure AD Connect a pak vyberte **Konfigurovat**.
3. Na stránce **další úlohy** vyberte **Konfigurovat možnosti zařízení**a pak vyberte **Další**.
4. Na stránce **Přehled** vyberte **Další**.
5. Na stránce **připojit ke službě Azure AD** zadejte přihlašovací údaje globálního správce služby Azure AD.
6. Na stránce **Možnosti zařízení** vyberte **Konfigurovat hybridní připojení k Azure AD**a pak vyberte **Další**.
7. Na stránce **operační systémy zařízení** vyberte operační systémy používané zařízeními v prostředí služby Active Directory a pak vyberte **Další**.  

   Můžete vybrat možnost pro podporu zařízení připojených k doméně starší verze systému Windows, ale mějte na paměti, že společná správa zařízení je podporována pouze pro systém Windows 10.
8. Na stránce **spojovací bod** služby pro každou místní doménovou strukturu, kterou chcete Azure AD Connect ke konfiguraci spojovacího bodu služby (SCP), proveďte následující kroky a potom vyberte **Další**:  
   1. Vyberte doménovou strukturu.  
   2. Vyberte ověřovací službu.  Pokud máte federované domény, vyberte AD FS Server, pokud vaše organizace nemá výhradně klienty s Windows 10 a že jste nakonfigurovali synchronizaci počítačů a zařízení nebo pokud vaše organizace používá [SeamlessSSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso).  
   3. Klikněte na **Přidat** a zadejte přihlašovací údaje podnikového správce.  
9. Pokud máte spravovanou doménu, přeskočte tento krok.  

   Na stránce **Konfigurace federace** zadejte přihlašovací údaje správce AD FS a pak vyberte **Další**.
10. Na stránce **připraveno ke konfiguraci** vyberte **Konfigurovat**.
11. Na stránce **Konfigurace byla dokončena** vyberte možnost **ukončit**.

Pokud dochází k problémům s dokončením hybridního připojení služby Azure AD pro zařízení s Windows připojená k doméně, přečtěte si téma [řešení potíží s hybridním připojením k Azure AD pro Windows](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current)

## <a name="configure-client-settings-to-direct-clients-to-register-with-azure-ad"></a>Konfigurace nastavení klienta pro směrování klientů k registraci ve službě Azure AD

Pomocí nastavení klienta nakonfigurujete klienty Configuration Manager k automatické registraci ve službě Azure AD.  

1. Otevřete okno > **Správa** >  **konzoly Configuration Manager****Přehled** > **nastavení klienta**a pak upravte **výchozí nastavení klienta**.  

2. Vyberte **Cloud Services**.  

3. Na stránce **výchozí nastavení** nastavte možnost **automaticky registrovat nová zařízení s Windows 10 připojená k doméně pomocí Azure Active Directory** na **hodnotu Ano**.  

4. Uložte tuto konfiguraci výběrem tlačítka **OK**.  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>Konfigurace automatického zápisu zařízení do Intune

V dalším kroku nastavíme automatickou registraci zařízení v Intune. Díky automatické registraci se zařízení, která spravujete, Configuration Manager automaticky zaregistrují v Intune.

Automatický zápis taky umožňuje uživatelům zaregistrovat svoje zařízení s Windows 10 do Intune. Zařízení se registrují, když uživatel přidá svůj pracovní účet do svého zařízení v osobním vlastnictví nebo když je zařízení vlastněné společností připojené k Azure Active Directory.  

1. Přihlaste se [k Azure Portal](https://portal.azure.com/) a vyberte**Microsoft Intune** **Azure Active Directory** > **mobility (MDM a mam)** > .  

2. Nakonfigurujte **obor uživatele MDM**. Určete jednu z následujících možností pro konfiguraci zařízení uživatelů, která jsou spravovaná nástrojem Microsoft Intune a přijměte výchozí hodnoty pro hodnoty URL.  

   - **Některé**: vyberte **skupiny** , které můžou automaticky registrovat svoje zařízení s Windows 10.  

   - **Vše**: všichni uživatelé můžou automaticky zaregistrovat svá zařízení s Windows 10.

   - **Žádné**: zakázat automatickou registraci MDM

   > [!IMPORTANT]  
   > Pokud u skupiny povolíte jak **obor uživatele MAM**, tak i automatickou registraci MDM (**obor uživatele MDM**), povolí se jenom MAM. Pro uživatele v této skupině se při připojení osobního zařízení k síti na pracovišti přidá jenom Správa mobilních aplikací (MAM). Zařízení nejsou automaticky zaregistrovaná do MDM.  

3. Kliknutím na **Uložit** dokončete konfiguraci automatického zápisu.  

4. Vraťte se k **mobilitě (MDM a mam)** a pak vyberte **Microsoft Intune registrace**.  

    > [!NOTE]
    > Někteří klienti nemusí mít tyto možnosti nakonfigurovány.<!-- SCCMDocs#1230 -->
    >
    > **Microsoft Intune** je způsob konfigurace aplikace MDM pro službu Azure AD. **Registrace Microsoft Intune** je konkrétní aplikace služby Azure AD, která se vytvoří při použití zásad služby Multi-Factor Authentication pro registraci zařízení s iOS a Androidem. Další informace najdete v tématu [vyžadování služby Multi-Factor Authentication pro registraci zařízení v Intune](https://docs.microsoft.com/intune/enrollment/multi-factor-authentication).

5. Pro možnost obor uživatele MDM vyberte **vše**a pak ho **uložte**.  

## <a name="enable-co-management-in-configuration-manager"></a>Povolit spolusprávu v Configuration Manager

Když máte na začátku hybridní konfigurace a Configuration Manager klienta Azure AD, jste připraveni překlopit přepínač a povolit spolusprávu zařízení s Windows 10.  

> [!TIP]
> - Pokud povolíte spolusprávu, přiřadíte kolekci jako *pilotní skupinu*. Jedná se o skupinu, která obsahuje malý počet klientů pro otestování konfigurací spolusprávy. Před zahájením postupu doporučujeme vytvořit vhodnou kolekci. Pak můžete tuto kolekci vybrat bez ukončení postupu.
> - Configuration Manager počínaje verzí 1906 je možné, že budete potřebovat více kolekcí, protože pro každou úlohu můžete přiřadit jinou *pilotní skupinu* .

### <a name="enable-co-management-starting-in-version-1906"></a>Povolit spolusprávu počínaje verzí 1906

Pokud chcete povolit spolusprávu od verze Configuration Manager 1906, postupujte podle následujících pokynů:

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>Povolit spolusprávu ve verzi 1902 a novější

Pokud chcete povolit spolusprávu pro Configuration Manager verze 1902 a starší, postupujte podle následujících pokynů:

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="next-steps"></a>Další kroky

- Kontrola stavu souběžně spravovaných zařízení pomocí [řídicího panelu spolusprávy](how-to-monitor.md)
- Začněte získávat [okamžitou hodnotu](quickstarts.md#immediate-value) ze spolusprávy
- Použití pravidel dodržování předpisů [podmíněného přístupu](quickstart-conditional-access.md) a Intune ke správě přístupu uživatelů k podnikovým prostředkům
