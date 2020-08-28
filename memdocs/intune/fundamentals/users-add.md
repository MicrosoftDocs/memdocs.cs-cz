---
title: Přidání uživatelů a udělení oprávnění
titleSuffix: Microsoft Intune
description: Synchronizace místních uživatelů s Azure AD a udělení správci oprávnění ke správě předplatného Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/28/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6e9ec662-465b-4ed4-94c1-cff0fe18f126
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 56d632da8480e0beedac7f086928638633dbe49c
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996312"
---
# <a name="add-users-and-grant-administrative-permission-to-intune"></a>Přidání uživatelů a udělení oprávnění pro správu v Intune

Jako správce můžete uživatele přidat přímo nebo je synchronizovat z místní služby Active Directory. Po přidání můžou uživatelé zaregistrovat zařízení a přistupovat k prostředkům společnosti. Můžete také uživatelům udělit další oprávnění včetně oprávnění *globálního správce* a *správce služeb*.

## <a name="add-users-to-intune"></a>Přidání uživatelů do Intune

Do svého předplatného Intune můžete ručně přidat uživatele pomocí [centra pro správu Microsoft 365](https://admin.microsoft.com) nebo [Azure Portal](https://portal.azure.com/#blade/Microsoft_Intune_DeviceSettings/ExtensionLandingBlade/overview). Správce může upravovat uživatelské účty a přiřazovat licence Intune. Licence můžete přiřadit buď v centru pro správu Microsoft 365, nebo v Azure Portal Intune. Další informace o použití centra pro správu Microsoft 365 najdete v tématu [Přidání uživatelů jednotlivě nebo hromadně do centra pro správu Microsoft 365](https://support.office.com/article/Add-users-individually-or-in-bulk-to-Office-365-Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec).

### <a name="add-intune-users-in-the-microsoft-365-admin-center"></a>Přidání uživatelů Intune v centru pro správu Microsoft 365

1. Přihlaste se k [Microsoft 365 centra pro správu](https://admin.microsoft.com) pomocí účtu globálního správce nebo správce správy uživatelů.
2. V nabídce Microsoft 365 vyberte **správce**.
3. V Centru pro správu vyberte **Přidat uživatele**.

   ![Snímek obrazovky sekce Přidat uživatele](./media/users-add/office-add-user.png)

4. Uveďte následující údaje o uživateli:
   - **Jméno**
   - **Příjmení**
   - **Zobrazovaný název**
   - **Uživatelské jméno** – hlavní název uživatele (UPN) uložený v Azure Active Directory a používaný pro přístup ke službě
   - **Umístění**
   - **Kontaktní informace** (nepovinné)
   - **Heslo** – automaticky vygenerované nebo vytvořené

     ![Snímek obrazovky sekce nového uživatele](./media/users-add/office-add-user-details.png)

5. Přiřaďte uživatelskou licenci pro Intune. Vyberte možnost **Licence na produkty** a vyberte licenci na produkt. Je potřeba licence zahrnující Intune.
6. Zvolte **Přidat** a vytvořte tak nového uživatele.

### <a name="add-intune-users-in-the-azure-portal"></a>Přidání uživatelů Intune na Azure Portalu

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **Uživatelé**  >  **Všichni uživatelé**.
2. V Centru pro správu vyberte **Nový uživatel**.
3. Uveďte následující údaje o uživateli:
   - **Name**
   - **Uživatelské jméno** – nové jméno na portálu Azure Active Directory ![Snímek obrazovky přidání jména a uživatelského jména](./media/users-add/intune-add-user-info.png) Pokračujte výběrem **OK**.
4. Volitelně můžete zadat následující vlastnosti uživatele:
   - **Profil** – údaje týkající se práce včetně **pracovní pozice** a **oddělení**
   - **Skupiny** – vyberte skupiny, které chcete pro uživatele přidat
   - **Role adresáře** – přidělte uživateli oprávnění správce včetně role správce služeb Intune.

   Vyberte **Vytvořit** a přidejte tak nového uživatele do Intune.
5. Vyberte **Profil** a potom pro nového uživatele vyberte **Místo využívání**. Místo využívání je nutné zadat, abyste mohli přiřadit novému uživateli licenci Intune. Pokračujte možností **Uložit**.
    ![Snímek obrazovky místa využívání](./media/users-add/intune-add-user-loc.png)
6. Vyberte **Licence**. Potom zvolte **Přiřadit** a přiřaďte tomuto uživateli licenci Intune. Licence Intune je nutná pro registraci zařízení a přístup k prostředkům společnosti. Vyberte **Produkty**, zvolte typ licence, **Vybrat** a potom **Přiřadit**.

## <a name="grant-admin-permissions"></a>Udělení oprávnění správce

Až budete mít k předplatnému Intune přidané další uživatele, doporučujeme, abyste několika uživatelům přidělili oprávnění správce.  Oprávnění správce přidělíte takto:

### <a name="give-admin-permissions-in-microsoft-365"></a>Udělení oprávnění správce v Microsoft 365

1. Přihlaste se k [centru pro správu Microsoft 365](https://admin.microsoft.com) pomocí účtu globálního správce.
2. V nabídce Microsoft 365 vyberte **správce**.
3. V Centru pro správu zvolte **Aktivní uživatele** a pak vyberte uživatele, kterému chcete udělit oprávnění správce.

4. Ve sloupci **Role** zvolte **Upravit**.

    ![Snímek obrazovky uživatele Správce](./media/users-add/office-assign-roles-open.png)

5. Ze seznamu dostupných rolí vyberte oprávnění správce, které chcete udělit.
![Snímek obrazovky přiřazení rolí](./media/users-add/office-assign-roles.png)
6. Klikněte na tlačítko **Uložit**.

### <a name="give-admin-permissions-in-the-azure-portal"></a>Udělení oprávnění správce na Azure Portalu

1. Přihlaste se k [Azure Portalu](https://portal.azure.com) pomocí účtu globálního správce.
2. Na Azure Portalu zvolte **Uživatel** a pak vyberte uživatele, kterému chcete udělit oprávnění správce.
3. Vyberte **Role adresáře** a pak vyberte oprávnění.
  ![Snímek obrazovky Role adresáře](./media/users-add/add-intune-directory-role.png)
4. Klikněte na tlačítko **Uložit**.

### <a name="types-of-administrators"></a>Typy správců

Přiřazení jednoho nebo více oprávnění správce uživatelům. Tato oprávnění definují, v jakém rozsahu můžou uživatelé provádět správu a úlohy. Oprávnění správce jsou obvyklá v rámci různých cloudových služeb Microsoftu a některé služby nemusí některá oprávnění podporovat. V centru pro správu Azure Portal a Microsoft 365 je seznam omezených rolí správce, které Intune nepoužívá. Oprávnění správce pro Intune zahrnují tyto možnosti:

- **Globální správce** – (Microsoft 365 a Intune) přistupuje ke všem funkcím pro správu v Intune. Ve výchozím nastavení se osoba, která se zaregistruje do Intune, stal globálním správcem. Globální správci jsou jedinými správci, kteří můžou přiřazovat další role správců. V organizaci můžete mít více než jednoho globálního správce. Jako osvědčený postup doporučujeme, aby tuto roli mělo jenom pár lidí ve vaší společnosti, aby se minimalizovala rizika, která by mohla ohrozit vaši firmu.
- **Správce hesel** – (Microsoft 365 a Intune) může resetovat hesla, spravovat žádosti o služby a monitorovat stav služby. Správci hesel můžou resetovat hesla jenom uživatelům.
- **Správce služeb** – (Microsoft 365 a Intune) otevírá žádosti o podporu u Microsoftu a prohlíží řídicí panel služeb a Centrum zpráv. Mají oprávnění pouze pro zobrazení s výjimkou otevření lístků podpory a jejich čtení.
- **Správce fakturace** – (Microsoft 365 a Intune) umožňuje nákupy, spravovat předplatná, spravovat lístky podpory a monitorovat stav služby.
- **Správce uživatelů** – (Microsoft 365 a Intune) může resetovat hesla, sledovat stav služeb, přidávat a odstraňovat uživatelské účty a spravovat žádosti o služby. Správce správy uživatelů nemůže odstranit globálního správce, vytvářet další role správců ani resetovat hesla jiných správců.
- **Správce služby Intune** – všechna oprávnění globálního správce Intune s výjimkou oprávnění k vytvoření správců s možnostmi **Role adresáře**.

Účet, který se používá k vytvoření vašeho předplatného Microsoft Intune, je globální správce. Pro každodenní úlohy se nedoporučuje používat globálního správce. Pro přístup k Intune na portálu Azure Portal sice správce nepotřebuje licenci Intune, ale k provádění určitých úloh správy, jako je třeba nastavení konektoru služby Exchange, se licence Intune vyžaduje.

Pokud chcete získat přístup k centru pro správu Microsoft 365, váš účet musí mít **povolenou** sadu pro přihlášení. Na Azure Portalu nastavte v oblasti **Profil** volbu **Zablokovat přihlášení** na **Ne**, čímž povolíte přístup. Tento stav je něco jiného než vlastnictví licence k předplatnému. Ve výchozím nastavení jsou všechny uživatelské účty nastavené na **Povoleno**. Uživatelé bez oprávnění správce můžou použít Centrum pro správu Microsoft 365 k resetování hesel Intune.

## <a name="sync-active-directory-and-add-users-to-intune"></a>Synchronizace služby Active Directory a přidání uživatelů do Intune

Můžete nakonfigurovat synchronizaci adresářů, aby se importovaly uživatelské účty z vaší místní služby Active Directory do Microsoft Azure Active Directory (Azure AD), což zahrnuje uživatele Intune. Když máte místní službu Active Directory připojenou ke všem vašim službám založeným na Azure Active Directory, správa identity uživatele se tím zjednodušuje. Můžete taky nakonfigurovat funkce jednotného přihlašování, aby se prostředí ověřování pro vaše uživatele zjednodušilo a zpřehlednilo. Propojením stejného [tenanta Azure AD](/azure/active-directory/hybrid/whatis-hybrid-identity) s více službami se uživatelské účty, které jste předtím synchronizovali, stanou dostupnými pro všechny cloudové služby.

### <a name="how-to-sync-on-premises-users-with-azure-ad"></a>Synchronizace místních uživatelů s Azure AD

Jediný nástroj potřebný k synchronizaci uživatelských účtů s Azure AD je [Průvodce Azure AD Connectem](https://www.microsoft.com/download/details.aspx?id=47594). Průvodce Azure AD Connectem je nástroj, který vás zjednodušeně provede připojením místní infrastruktury identit ke cloudu. Vyberte topologii a potřeby (jeden nebo více adresářů, synchronizaci hodnoty hash, předávací ověřování nebo federaci). Průvodce nasadí a nakonfiguruje všechny komponenty potřebné ke zprovoznění a spuštění vašeho připojení. Včetně služeb synchronizace, Active Directory Federation Services (AD FS) a modulu Azure AD PowerShell.

> [!TIP]
> Azure AD Connect zahrnuje funkce, které byly dříve vydány jako DirSync a Azure AD Sync. Přečtěte si další informace o [integraci adresáře](/previous-versions/azure/azure-services/jj573653(v=azure.100)). Informace o synchronizaci uživatelských účtů z místního adresáře do Azure AD najdete v tématu [Podobnosti mezi službou Active Directory a Azure AD](/previous-versions/azure/azure-services/dn518177(v=azure.100)).