---
title: Skupiny Intune Classic na portálu Azure Portal
titleSuffix: Microsoft Intune
description: Seznamte se s novinkami ve skupinách na portálu Azure Portal pro Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/31/2019
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 323f384d-8a76-4adc-999b-e508d641bfa1
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 82834dc3a7fc60292228acbd62c7c6a8b8a94ee3
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909784"
---
# <a name="microsoft-intune-classic-groups-in-the-azure-portal"></a>Skupiny Microsoft Intune Classic na portálu Azure Portal

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Vyslyšeli jsme vaše názory a změnili jsme způsob práce se skupinami v Microsoft Intune.
Pokud Intune používáte z portálu Azure Portal, pak se vaše skupiny Intune migrovaly do skupin zabezpečení Azure Active Directory.

Výhoda pro vás spočívá v tom, že teď používáte stejné prostředí skupin ve všech aplikacích Enterprise Mobility + Security a Azure AD. Kromě toho můžete použít rozhraní API prostředí PowerShell a Graph a tuto novou funkci si rozšířit a přizpůsobit.

Skupiny zabezpečení služby Azure AD podporují všechny typy nasazení Intune pro uživatele i zařízení. Kromě toho můžete používat dynamické skupiny Azure AD, které se automaticky aktualizují na základě atributů, které zadáte. Můžete například vytvořit skupinu zařízení se systémem iOS 9. Vždy, když se zařízení se systémem iOS 9 zaregistruje, zobrazí se toto zařízení automaticky v dynamické skupině.

## <a name="what-is-not-available"></a>Co není dostupné?

Některé možnosti skupin Intune, které jste dříve možná používali, nejsou v Azure AD dostupné:

- Nejsou už dostupné skupiny Intune **Neseskupení uživatelé** a **Neseskupená zařízení**.
- Možnost **Vyloučit konkrétní členy** ze skupiny na portálu Azure Portal neexistuje. Toto chování ale můžete nahradit pomocí skupiny zabezpečení Azure AD s rozšířenými pravidly. Pokud například chcete vytvořit pokročilé pravidlo, které do skupiny zabezpečení zahrne všechny pracovníky vašeho prodejního oddělení, ale vynechá všechny skupiny, které mají v názvu slovo „Asistent“, můžete použít toto rozšířené pravidlo:

  `(user.department -eq "Sales") -and -not (user.jobTitle -contains "Assistant")`.
- Skupina **Všechna zařízení spravovaná prostřednictvím protokolu Exchange ActiveSync** v klasické konzole Intune se do služby Azure AD nemigrovala. K informacím o zařízeních spravovaných přes EAS však stále máte přístup z portálu Azure Portal.

## <a name="how-to-get-started"></a>Jak začít?

- Přečtěte si následující témata, kde najdete další informace o skupinách zabezpečení služby Azure AD a jak fungují:
  - [Správa přístupu k prostředkům pomocí skupin Azure Active Directory](/azure/active-directory/fundamentals/active-directory-manage-groups).
  - [Správa skupin v Azure Active Directory](/azure/active-directory/fundamentals/active-directory-groups-create-azure-portal).
  - [Vytváření rozšířených pravidel pomocí atributů](/azure/active-directory/users-groups-roles/groups-dynamic-membership)
- Všechny správce, kteří potřebují vytvářet skupiny, je potřeba přidat do role Azure AD **Správce služby Intune**. Role správce služby Azure AD nemá oprávnění **Spravovat skupinu**.
- Pokud vaše skupiny Intune použily možnost **Vyloučit konkrétní členy**, rozhodněte se, jestli chcete tyto skupiny znovu vytvořit bez vyloučení nebo jestli potřebujete rozšířená pravidla, abyste vyhověli potřebám firmy.


## <a name="what-happened-to-intune-groups"></a>Co se stalo se skupinami Intune?
Při migraci skupin z Azure Portalu do Intune na Azure Portalu se použijí následující pravidla:

| Skupiny v Intune|Skupiny ve službě Azure AD|
|-----------------------------------------------------------------------|-------------------------------------------------------------|
|Statická skupina uživatelů|Statická skupina zabezpečení Azure AD|
|Dynamická skupina uživatelů|Statické skupiny zabezpečení služby Azure AD s hierarchií skupiny zabezpečení služby Azure AD|
|Statická skupina zařízení|Statická skupina zabezpečení Azure AD|
|Dynamická skupina zařízení|Dynamická skupina zabezpečení Azure AD|
|Skupina s podmínkou zahrnutí|Statická skupina zabezpečení Azure AD obsahující všechny statické nebo dynamické členy z podmínky zahrnutí v Intune|
|Skupina s podmínkou vyloučení|Nemigruje se.|
|Předdefinované skupiny:<br>- **Všichni uživatelé**<br>- **Neseskupení uživatelé**<br>- **Všechna zařízení**<br>- **Neseskupená zařízení**<br>- **Všechny počítače**<br>- **Všechna mobilní zařízení**<br>- **Všechna zařízení spravovaná systémem MDM**<br>- **Všechna zařízení spravovaná systémem EAS**|Skupiny zabezpečení služby Azure AD|

## <a name="group-hierarchy"></a>Hierarchie skupin

V konzole Intune měly všechny skupiny nadřazenou skupinu. Skupiny mohly obsahovat jenom členy ze svojí nadřazené skupiny. V Azure AD můžou podřízené skupiny obsahovat členy, které nejsou v jejich nadřazené skupině.

## <a name="group-attributes"></a>Atributy skupin
Atributy jsou vlastnosti zařízení, které se dají použít při definování skupin. Tato tabulka popisuje, jak se kritéria přesouvají do skupin zabezpečení služby Azure AD.

| Atribut v Intune|Atribut v Azure AD|
|-----------------------------------------------------------------------|-------------------------------------------------------------|
|Atribut OU (organizační jednotky) pro skupiny zařízení|Atribut OU pro dynamické skupiny.|
|Atribut názvu domény pro skupiny zařízení|Atribut názvu domény pro dynamické skupiny.|
|Skupina zabezpečení jako atribut pro skupiny uživatelů|Skupiny nemohou být atributy v dynamických dotazech služby Azure AD. Dynamické skupiny můžou obsahovat jenom atributy specifické pro uživatele nebo zařízení.|
|Atribut Manager pro skupiny uživatelů|Rozšířené pravidlo pro atribut *manager* v dynamických skupinách|
|Všichni uživatelé z nadřazené skupiny uživatelů|Statická skupina s touto skupinou jako členem|
|Všechna mobilní zařízení z nadřazené skupiny zařízení|Statická skupina s touto skupinou jako členem|
|Veškerá mobilní zařízení spravovaná přes Intune|Atribut typu správy s typem MDM jako s hodnotou pro dynamickou skupinu|
|Vnořené skupiny v rámci statických skupin |Vnořené skupiny v rámci statických skupin|
|Vnořené skupiny v rámci dynamických skupin|Dynamická skupina s jednou úrovní vnoření|

## <a name="what-happens-to-policies-and-apps-you-previously-deployed"></a>Co se stane se zásadami a aplikacemi, které jste už nasadili?

Zásady a aplikace jsou i nadále nasazené do skupin, stejně jako dříve. Tyto skupiny teď ale budete spravovat z Azure Portalu, ne z konzoly Intune.