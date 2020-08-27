---
title: Zásady dodržování předpisů pro zařízení Jamf
titleSuffix: Microsoft Intune
description: K usnadnění zabezpečení zařízení spravovaných Jamf Microsoft Intune použijte zásady dodržování předpisů Azure Active Directory podmíněný přístup.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c87fd2bd-7f53-4f1b-b985-c34f2d85a7bc
ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 08586879f3523d1188f18e2d7024f32fae83febc
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911195"
---
# <a name="enforce-compliance-on-macs-managed-with-jamf-pro"></a>Vynucení dodržování předpisů v počítačích Mac spravovaných aplikací Jamf Pro

Při integraci Jamf pro s Intune můžete pomocí zásad podmíněného přístupu vymáhat dodržování předpisů na vašich zařízeních Mac pomocí požadavků vaší organizace. Tento článek vám pomůže s následujícími úlohami:  

- Vytvořte zásady podmíněného přístupu.
- Nakonfigurujte Jamf pro pro nasazení aplikace Portál společnosti Intune do zařízení, která spravujete pomocí Jamf.
- Nakonfigurujte zařízení, která se registrují ve službě Azure AD, když se uživatel zařízení přihlásí k aplikaci Portál společnosti, kterou začínají v aplikaci samoobslužné aplikace Jamf. Registrace zařízení vytváří identitu ve službě Azure AD, která umožňuje vyhodnotit zařízení na základě zásad podmíněného přístupu pro přístup k prostředkům společnosti.  
 
Postupy v tomto článku vyžadují přístup ke konzolám Intune i Jamf pro.
Intune podporuje dvě metody pro integraci Jamf pro, které nakonfigurujete samostatně z postupů v tomto článku:

- Doporučené: [Použití cloudového konektoru Jamf k integraci Jamf pro s Intune](conditional-access-jamf-cloud-connector.md)
- [Ruční konfigurace integrace služby Jamf pro s Intune](conditional-access-integrate-jamf.md)

## <a name="set-up-device-compliance-policies-in-intune"></a>Nastavení zásad dodržování předpisů pro zařízení v Intune

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Devices**  >  **zásady dodržování předpisů**pro zařízení. Pokud používáte dříve vytvořenou zásadu, vyberte tuto zásadu v konzole nástroje a pak se pokuste přejít k dalšímu kroku tohoto postupu. Pokud chcete vytvořit novou zásadu, vyberte **vytvořit zásadu** a pak zadejte podrobnosti zásady s *platformou* **MacOS**. Nakonfigurujte *Nastavení* a *Akce při nedodržení předpisů* , aby splňovaly požadavky vaší organizace, a pak vyberte **vytvořit** a zásadu uložte.

3. V podokně *Přehled* zásad vyberte **přiřazení**. Pomocí dostupných možností můžete nakonfigurovat, které Azure Active Directory (Azure AD) a skupiny zabezpečení obdrží tyto zásady. **Integrace Jamf s Intune nepodporuje zásady dodržování předpisů, které cílí na skupiny zařízení.**

> [!NOTE]
> Integrace Jamf s Intune podporuje jenom skupiny uživatelů AAD. Zásady dodržování předpisů zařízením, které cílí na skupiny zařízení, se nepoužijí.

4. Když vyberete **Save (Uložit**), zásada se nasadí uživatelům.  

Zásady, které nasadíte, cílí na zařízení, která používají přiřazení uživatelé. Tato zařízení se vyhodnocují pro dodržování předpisů. Vyhovující zařízení jsou označená jako vyhovující pro nastavení "*požadovat, aby zařízení bylo*ve službě Azure AD označené jako vyhovující".  

> [!NOTE]
> Intune v zájmu dodržování předpisů vyžaduje úplné šifrování disků.

## <a name="deploy-the-company-portal-app-for-macos-in-jamf-pro"></a>Nasazení aplikace Portál společnosti pro macOS v Jamf Pro

Vytvořte zásadu v Jamf pro pro nasazení Portál společnosti Intune. Tato zásada nasadí aplikaci Portál společnosti tak, aby byla dostupná v samoobslužné službě Jamf. Před vytvořením zásad v Jamf pro můžete vytvořit tuto zásadu pro uživatele k registraci zařízení ve službě Azure AD.  

K provedení následujícího postupu potřebujete přístup k zařízení macOS a portálu Jamf pro. 

### <a name="to-deploy-the-company-portal-app"></a>Nasazení aplikace Portál společnosti  

1. Na zařízení macOS si stáhněte, ale neinstalujte aktuální verzi [aplikace Portál společnosti pro MacOS](https://go.microsoft.com/fwlink/?linkid=862280). Potřebujete jenom kopii aplikace, abyste mohli aplikaci nahrát do Jamf pro.  

2. Otevřete Jamf pro a pokračujte na **balíčky pro správu počítače**  >  **Packages**.

3. Vytvořte nový balíček pomocí aplikace Portál společnosti pro macOS a pak vyberte **Uložit**.

4. Otevřete **Computers**  >  **zásady**počítače a pak vyberte **Nový**.

5. Nakonfigurujte nastavení zásad pomocí datové části **General** (Obecné). Měli byste nastavit:
   - Trigger: Vyberte **Enrollment Complete** (Registrace dokončena) a **Recurring Check-in** (Opakované vrácení se změnami).
   - Execution Frequency (Četnost spuštění): Vyberte **Once per computer** (Jednou na počítač).

6. Vyberte datovou část **Packages (Balíčky)** klikněte na **Configure (Konfigurovat)**.

7. Kliknutím na **Add (Přidat)** vyberte balíček pomocí aplikace Portál společnosti.

8. V místní nabídce **Akce** vyberte **instalovat** .
9. Nakonfigurujte nastavení balíčku.

10. Vyberte kartu **obor** a určete, na kterých počítačích by se měla aplikace Portál společnosti nainstalovat. Vyberte **Uložit**. Zásada se spustí v oboru zařízení při příštím výskytu vybrané aktivační události v počítači a splní se kritéria v datové části **General** .

## <a name="create-a-policy-in-jamf-pro-to-have-users-register-their-devices-with-azure-active-directory"></a>Vytvoření zásad v Jamf Pro, které donutí uživatele zaregistrovat zařízení ve službě Azure Active Directory  

Po [nasazení portál společnosti](conditional-access-assign-jamf.md#deploy-the-company-portal-app-for-macos-in-jamf-pro) pro MacOS prostřednictvím samoobslužné služby Jamf pro můžete vytvořit zásadu Jamf pro, která zaregistruje zařízení uživatele ve službě Azure AD. 

Registrace zařízení vyžaduje, aby uživatel zařízení v rámci samoobslužné služby Jamf ručně vybral aplikaci Portál společnosti Intune. Doporučujeme, abyste se [koncovým uživatelům kontaktovali](../fundamentals/end-user-educate.md) prostřednictvím e-mailu, oznámení Jamf pro nebo jakékoli jiné metody, kterou vaše organizace používá k tomu, aby tato akce mohla dokončit, aby se jejich zařízení zaregistrovalo. 

> [!WARNING]
> Ruční spuštění aplikace Portál společnosti (například ze složek aplikace nebo soubory ke stažení) nebude zařízení registrovat. Pokud uživatel zařízení spustí Portál společnosti ručně, zobrazí se upozornění **"AccountNotOnboarded"**.

### <a name="to-create-the-registration-policy"></a>Vytvoření zásad registrace  

1. V Jamf pro vyhledejte **Computers**  >  **zásady**počítače a vytvořte novou zásadu pro registraci zařízení.

2. Nakonfigurujte datovou část **Microsoft Intune Integration** (Integrace Microsoft Intune) včetně frekvence aktivační události a spouštění.

3. Vyberte kartu **obor** a pak nastavte obor zásady na všechna cílová zařízení.

4. Vyberte kartu **Samoobslužná služba** , která zpřístupní zásadu v samoobslužné službě Jamf. Zahrňte zásadu v kategorii **Device Compliance (Dodržování předpisů zařízením)**. Klikněte na **Uložit**.

## <a name="validate-intune-and-jamf-integration"></a>Ověření integrace Intune a Jamf  

Pomocí konzoly Jamf pro potvrďte, že komunikace mezi Jamf pro a Microsoft Intune je úspěšná. 

- V Jamf pro, přejít na **Nastavení**  >  **Globální správa**  >  **Microsoft Intune integrace**a pak vyberte **test**.

    Konzola zobrazí zprávu s úspěšným nebo neúspěšným připojením.  

Pokud selže test připojení z konzoly Jamf pro, zkontrolujte konfiguraci Jamf. 


## <a name="removing-a-jamf-managed-device-from-intune"></a>Odebrání zařízení spravovaného prostřednictvím Jamf z Intune

Pokud chcete odebrat zařízení spravované přes Jamf, otevřete centrum pro správu Microsoft Endpoint Manageru a vyberte **zařízení**  >  **všechna zařízení**, vyberte zařízení a pak vyberte **Odstranit**.  Hromadné odstranění zařízení se dá povolit výběrem více zařízení a kliknutím na **Odstranit**.

Získejte informace o tom, jak [Odebrat Jamf zařízení spravované v dokumentaci pro Jamf pro](https://www.jamf.com/jamf-nation/articles/80/unmanaging-computers-while-preserving-their-inventory-information). Pro další pomoc si můžete také [poJamf podporu](https://www.jamf.com/support/) a pokaždé, když zadáte lístek podpory. 

## <a name="next-steps"></a>Další kroky

- [Podmíněný přístup v Azure Active Directory](/azure/active-directory/active-directory-conditional-access-azure-portal)
- [Začínáme s podmíněným přístupem v Azure Active Directory](/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)