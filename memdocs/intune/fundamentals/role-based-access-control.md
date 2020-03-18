---
title: Řízení přístupu na základě role (RBAC) s Microsoft Intune
description: Přečtěte si, jak vám umožňuje řídit, kdo může provádět akce a provádět změny v Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/22/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ca3de752-3caa-46a4-b4ed-ee9012ccae8e
ms.reviewer: pjain
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: b01f9444cf70c447c916d3d0a550a8cf46efc28a
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79330659"
---
# <a name="role-based-access-control-rbac-with-microsoft-intune"></a>Řízení přístupu na základě role (RBAC) s Microsoft Intune

Řízení přístupu na základě role (RBAC) pomáhá spravovat, kdo má přístup k prostředkům vaší organizace a co s těmito prostředky může dělat.  [Přiřazením rolí](assign-role.md) uživatelům Intune můžete omezit to, co můžou zobrazit a změnit. Každá role má sadu oprávnění, která určují, co můžou uživatelé s touto rolí používat a měnit v rámci vaší organizace.

Abyste mohli vytvářet, upravovat nebo přiřazovat role, váš účet musí mít ve službě Azure AD jedno z těchto oprávnění:
- **Globální správce**
- **Správce služby Intune** (označovaný také jako **správce Intune**)

Pokud potřebujete Rady a návrhy týkající se RBAC v Intune, můžete si vyzkoušet tuto řadu pěti videí, která prezentují příklady a návody: [1](https://www.youtube.com/watch?v=5deXLMLcnKY), [2](https://www.youtube.com/watch?v=38dnMBLuxbQ), [3](https://www.youtube.com/watch?v=6vqg9cAkMbY), [4](https://www.youtube.com/watch?v=5yOLajFFMHE), [5](https://www.youtube.com/watch?v=P5DDvsSF4Wk).

## <a name="roles"></a>Role
Role definuje sadu oprávnění udělených uživatelům přiřazeným k této roli.
Můžete použít jak předdefinované, tak i vlastní role. Předdefinované role se týkají některých běžných scénářů Intune. Můžete [vytvořit vlastní role](create-custom-role.md) s přesnou sadou oprávnění, která potřebujete. Několik rolí Azure Active Directory má oprávnění k Intune.
Pokud chcete zobrazit roli, vyberte **role > ** **Intune** > **všechny role** > vyberte roli. Zobrazí se následující stránky:

- **Vlastnosti**: značky název, popis, typ, přiřazení a obor pro roli. 
- **Oprávnění**: vypíše dlouhou sadu přepínačů definujících, jaká oprávnění role má.
- **Přiřazení**: seznam [přiřazení rolí]( assign-role.md) definujících, kteří uživatelé mají přístup k jakým uživatelům nebo zařízením. Role může mít více přiřazení a uživatel může být v několika přiřazeních.

### <a name="built-in-roles"></a>Předdefinované role
Předdefinované role můžete přiřadit skupinám bez další konfigurace. Nemůžete odstranit ani upravit název, popis, typ ani oprávnění předdefinované role.

- **Operátor helpdesku**: Provádí vzdálené úlohy u uživatelů a zařízení a může uživatelům a zařízením přiřazovat aplikace nebo zásady.
- **Správce zásad a profilů**: spravuje zásady dodržování předpisů, konfigurační profily, registrace Apple, identifikátory podnikových zařízení a směrné plány zabezpečení.
- **Operátor s oprávněními pouze ke čtení**: Zobrazuje informace o uživatelích, zařízeních, registraci, konfiguraci a aplikacích. Nejde dělat změny v Intune.
- **Správce aplikací**: Spravuje mobilní a spravované aplikace, může číst informace o zařízeních a zobrazit konfigurační profily zařízení.
- **Správce role Intune**: spravuje vlastní role Intune a přidává přiřazení pro předdefinované role Intune. Je to jediná role Intune, která může přiřazovat oprávnění správcům.
- **Školní správce**: spravuje zařízení s Windows 10 v [Intune for Education](introduction-intune-education.md).
- **Endpoint Security Manager**: spravuje funkce zabezpečení a dodržování předpisů, jako jsou například standardní hodnoty zabezpečení, dodržování předpisů zařízením, podmíněný přístup a ATP v programu Microsoft Defender.

### <a name="custom-roles"></a>Vlastní role
Můžete vytvořit vlastní role s vlastními oprávněními. Další informace o vlastních rolích najdete v tématu [Vytvoření vlastní role](create-custom-role.md).

### <a name="azure-active-directory-roles-with-intune-access"></a>Azure Active Directory role s přístupem k Intune
| Role Azure Active Directory | Všechna data Intune | Data auditu Intune |
| --- | :---: | :---: |
| Globální správce | Čtení a zápis | Čtení a zápis |
| Správce služby Intune | Čtení a zápis | Čtení a zápis |
| Správce podmíněného přístupu | Žádné | Žádné |
| Správce zabezpečení | Jen pro čtení (úplná oprávnění správce pro uzel Security Endpoint Security) | Jen pro čtení |
| Operátor zabezpečení | Jen pro čtení | Jen pro čtení |
| Čtenář zabezpečení | Jen pro čtení | Jen pro čtení |
| Správce dodržování předpisů | Žádné | Jen pro čtení |
| Správce dat dodržování předpisů | Žádné | Jen pro čtení |
| Globální čtenář | Jen pro čtení | Jen pro čtení |

> [!TIP]
> Intune také ukazuje tři rozšíření Azure AD: **Uživatelé**, **skupiny**a **podmíněný přístup**, které se řídí pomocí Azure AD RBAC. **Správce uživatelských účtů** navíc provádí jenom aktivity uživatele nebo skupiny AAD a nemá úplná oprávnění provádět všechny aktivity v Intune. Další informace najdete v tématu [RBAC s Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles).
### <a name="roles-created-in-the-intune-classic-portal"></a>Role vytvořené na klasickém portálu Intune
Z klasického portálu Intune se do Intune na Azure Portalu migrují jenom **správci služeb** Intune s úplnými oprávněními. Musíte znovu přiřadit role **správců služby** Intune s přístupem "jen pro čtení" nebo "helpdesk" do rolí Intune v Azure Portal a odebrat je z portálu Classic.
> [!IMPORTANT]
> Pokud budou vaši správci dál potřebovat přístup ke správě počítačů pomocí Intune, může být potřeba zachovat přístup správce služby Intune na klasickém portálu.

## <a name="role-assignments"></a>Přiřazení rolí
Přiřazení role definuje:

- kteří uživatelé jsou přiřazeni k roli
- prostředky, které uvidí
- Jaké prostředky mohou změnit.

Uživatelům můžete přiřadit vlastní i předdefinované role. Uživatel musí mít licenci Intune, aby mu byla přiřazena role Intune.
Pokud chcete zobrazit přiřazení role, vyberte **role** > **Intune** > **všechny role** > vyberte roli > vyberte přiřazení. Zobrazí se následující stránky:

- **Properties (vlastnosti**): název, popis, role, členy, obory a značky přiřazení.
- **Členové**: všichni uživatelé v uvedených skupinách zabezpečení Azure mají oprávnění ke správě uživatelů nebo zařízení, která jsou uvedená v oboru (skupiny).
- **Rozsah (skupiny)** : všichni uživatelé/zařízení v těchto skupinách zabezpečení Azure je můžou spravovat uživatelé v rámci členů.
- **[Scope (značky)](scope-tags.md)** : uživatelé v členech můžou zobrazit prostředky, které mají stejné značky oboru.

### <a name="multiple-role-assignments"></a>Přiřazení více rolí
Pokud má uživatel více než jedno přiřazení rolí, oprávnění a značky oboru, přiřazení těchto rolí se rozšiřuje na různé objekty následujícím způsobem:

- Přiřazení oprávnění a značek oboru platí jenom pro objekty (jako jsou zásady nebo aplikace) v oboru přiřazení této role (skupiny). Přiřadit oprávnění a značky oboru se nevztahují na objekty v jiných přiřazeních rolí, pokud jiné přiřazení je výslovně neudělí.
- Další oprávnění (například vytváření, čtení, aktualizace, odstranění) a značky oboru se vztahují na všechny objekty stejného typu (jako jsou všechny zásady nebo všechny aplikace) v libovolném přiřazení uživatele.
- Značky oprávnění a oboru pro objekty různých typů (jako jsou zásady nebo aplikace) se nevztahují na sebe navzájem. Oprávnění ke čtení pro zásady například neposkytuje oprávnění ke čtení pro aplikace v přiřazení uživatele.

## <a name="next-steps"></a>Další kroky
- [Přiřazení role uživateli](assign-role.md)
- [Vytvoření vlastní role](create-custom-role.md)
