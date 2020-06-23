---
title: Hromadný zápis pro Windows 10
titleSuffix: Microsoft Intune
description: Vytvoření balíčku hromadné registrace pro Microsoft Intune
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 5/21/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1f39c02a-8d8a-4911-b4e1-e8d014dbce95
ms.reviewer: spshumwa
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7894e2648b58b1afd313250dc9724f117fe6c93a
ms.sourcegitcommit: 79ffc8afed164c408db6994806d71f64d1fc0b8f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/23/2020
ms.locfileid: "85216531"
---
# <a name="bulk-enrollment-for-windows-devices"></a>Hromadná registrace pro zařízení s Windows

Jako správce můžete k Azure Active Directory a Intune připojit větší počet zařízení s Windows. Hromadnou registraci zařízení pro vašeho tenanta Azure AD zahájíte vytvořením zřizovacího balíčku pomocí aplikace Windows Configuration Designer (WCD). Při aplikování zřizovacího balíčku na zařízení ve vlastnictví firmy se tato zařízení připojí k vašemu tenantovi Azure AD a zaregistrují v systému správy pomocí Intune. Po použití balíčku je připraveno pro uživatele Azure AD, aby se přihlásili.

Uživatelé Azure AD jsou na těchto zařízeních standardními uživateli a obdrží přiřazené zásady Intune a požadované aplikace. Zařízení s Windows, která jsou zaregistrovaná v Intune pomocí hromadné registrace Windows, můžou k instalaci dostupných aplikací použít aplikaci Portál společnosti. 

## <a name="prerequisites-for-windows-devices-bulk-enrollment"></a>Předpoklady pro hromadnou registraci zařízení s Windows

- Zařízení s Windows 10 Creator Update (Build 1709) nebo novější
- [Automatická registrace Windows](windows-enroll.md#enable-windows-10-automatic-enrollment)

## <a name="create-a-provisioning-package"></a>Vytvoření zřizovacího balíčku

1. Stáhněte si [Windows Configuration Designer (WCD)](https://www.microsoft.com/p/windows-configuration-designer/9nblggh4tx22) z Microsoft Storu.
   ![Snímek obrazovky s aplikací Windows Configuration Designer ve Storu](./media/windows-bulk-enroll/bulk-enroll-store.png)

2. Otevřete aplikaci **Windows Configuration Designer** a vyberte **Provision desktop devices** (Zřídit počítačová zařízení).
   ![Snímek obrazovky s výběrem možnosti Provision desktop devices ve Windows Configuration Designeru](./media/windows-bulk-enroll/bulk-enroll-select.png)

3. Otevře se okno **New project** (Nový projekt), kde zadáte tyto údaje:
   - **Name** (Název) – název vašeho projektu
   - **Project folder** (Složka projektu) – místo pro ukládání projektu
   - **Description** (Popis) – volitelný popis projektu ![Snímek obrazovky se zadáním názvu, složky projektu a popisu v aplikaci Windows Configuration Designer](./media/windows-bulk-enroll/bulk-enroll-name.png)

4. Zadejte jedinečný název pro zařízení. Názvy můžou zahrnovat sériové číslo (% SERIAL%). nebo náhodnou sadu znaků. Volitelně můžete také zadat kód Product Key, pokud provádíte upgrade edice Windows, nakonfigurovat zařízení pro sdílené používání a odebrat předinstalovaný software.
   
   ![Snímek obrazovky se zadáním názvu kódu Product Key v aplikaci Windows Configuration Designer](./media/windows-bulk-enroll/bulk-enroll-device.png)

5. Volitelně můžete nakonfigurovat síť Wi-Fi, ke které se zařízení připojí při prvním spuštění.  Pokud síťová zařízení nejsou nakonfigurovaná, musí být při prvním spuštění zařízení připojeno ke kabelové síti.
   ![Snímek obrazovky s povolením Wi-Fi včetně SSID sítě a typu sítě v aplikaci Windows Configuration Designer](./media/windows-bulk-enroll/bulk-enroll-network.png)

6. Vyberte **Enroll in Azure AD** (Zaregistrovat v Azure AD), zadejte datum **Bulk Token Expiry** (Vypršení platnosti hromadného tokenu) a pak vyberte **Get Bulk Token** (Získat hromadný token).
   ![Snímek obrazovky se správou účtů v aplikaci Windows Configuration Designer](./media/windows-bulk-enroll/bulk-enroll-account.png)

7. Zadejte přihlašovací údaje k Azure AD, abyste získali hromadný token.
   ![Snímek obrazovky s přihlášením do aplikace Windows Configuration Designer](./media/windows-bulk-enroll/bulk-enroll-cred.png)

8. V části **použít tento účet všude na této stránce zařízení** vyberte **jenom tuto aplikaci**.

9. Když se **Bulk Token** (Hromadný token) úspěšně načte, klikněte na **Next** (Další).

10. Volitelně můžete **Add applications** (Přidat aplikace) a **Add certificates** (Přidat certifikáty). Tyto aplikace a certifikáty se zřídí v zařízení.

11. Volitelně můžete zřizovací balíček ochránit heslem.  Klikněte na **Vytvořit**.
    ![Snímek obrazovky s ochranou balíčku v aplikaci Windows Configuration Designer](./media/windows-bulk-enroll/bulk-enroll-create.png)

## <a name="provision-devices"></a>Zřízení zařízení

1. Najděte zřizovací balíček v umístění, které jste zadali v **Project folder** (Složka projektu) v aplikaci.

2. Vyberte způsob použití zřizovacího balíčku pro zařízení.  Zřizovací balíček se dá do zařízení aplikovat jedním z těchto způsobů:
   - Zřizovací balíček umístěte do jednotky USB a vložte jednotku USB do zařízení, které chcete hromadně zaregistrovat, a použijte ho při počáteční instalaci.
   - Zřizovací balíček umístěte do síťové složky a nainstalujte ho po počáteční instalaci.

   Podrobné pokyny k aplikování zřizovacího balíčku najdete v článku o [aplikování zřizovacího balíčku](https://technet.microsoft.com/itpro/windows/configure/provisioning-apply-package).

3. Po použití balíčku se zařízení za minutu automaticky restartuje.
   ![Snímek obrazovky se zadáním názvu, složky projektu a popisu v aplikaci Windows Configuration Designer](./media/windows-bulk-enroll/bulk-enroll-add.png)

4. Po restartu se zařízení připojí k Azure Active Directory a zaregistruje v Microsoft Intune.

## <a name="troubleshooting-windows-bulk-enrollment"></a>Řešení potíží s hromadnou registrací zařízení s Windows

### <a name="provisioning-issues"></a>Problémy se zřizováním
Zřizování se má používat na nových zařízeních s Windows. Selhání zřizování může vyžadovat vymazání zařízení nebo obnovení zařízení ze spouštěcí image. Tyto příklady popisují některé důvody pro selhání zřizování:

- Zřizovací balíček snažící se připojit k doméně Active Directory nebo tenantovi Azure Active Directory, který nevytváří místní účet, může způsobit, že bude zařízení nedostupné, pokud proces připojení k doméně selže kvůli chybějícímu připojení k síti.
- Skripty spouštěné zřizovacím balíčkem se spouštějí v kontextu systému. Tyto skripty mohou v zařízení libovolně měnit systém souborů i jeho konfiguraci. Škodlivý nebo chybný skript by mohl zařízení uvést do stavu, který jde obnovit jen pomocí obnovení z image nebo vymazání.

Můžete zjistit, jestli je nastavení v balíčku úspěšné nebo neúspěšné, v přihlašování Správce služby **zřizování-Diagnostika – poskytovatel** Prohlížeč událostí.

### <a name="bulk-enrollment-with-wi-fi"></a>Hromadná registrace přes Wi-Fi 

Pokud nepoužíváte otevřenou síť, musíte k inicializaci připojení použít [certifikáty na úrovni zařízení](../protect/certificates-configure.md) . Hromadně zaregistrovaná zařízení se nedají použít pro uživatelem cílené certifikáty pro přístup k síti. 

### <a name="conditional-access"></a>Podmíněný přístup
Podmíněný přístup není k dispozici pro zařízení s Windows zaregistrovaná pomocí hromadné registrace.
