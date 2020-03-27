---
title: Použití řízení přístupu na základě role (RBAC) a značek oboru pro distribuci v Intune | Microsoft Docs
description: Pomocí značek oboru můžete filtrovat konfigurační profily pro konkrétní role.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/06/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.technology: ''
ms.assetid: a21d3039-f2ed-4f43-b6fa-d00c071edbc4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: eea973ec936ce41578754cb1a68d1b9128895b76
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80326687"
---
# <a name="use-role-based-access-control-rbac-and-scope-tags-for-distributed-it"></a>Použití řízení přístupu na základě role (RBAC) a značek oboru pro distribuci

Pomocí značek řízení přístupu založených na rolích a oborech můžete zajistit, aby měli oprávnění správce správný přístup a viditelnost správných objektů Intune. Role určují, kteří správci mají přístup k objektům. Značky oboru určují, které objekty můžou správci vidět.

Řekněme například, že regionální správce Office v Seattlu má roli správce zásad a profilace. Chcete, aby tento správce mohl zobrazovat a spravovat pouze profily a zásady, které se vztahují pouze na zařízení v Seattlu. K nastavení tohoto přístupu byste měli:

1. Vytvořte značku oboru s názvem Seattle.
2. Vytvořte přiřazení role pro roli Správce profilů a s těmito zásadami: 
    - Členové (skupiny) = skupina zabezpečení s názvem Praha IT Admins. Všichni správci v této skupině budou mít oprávnění ke správě zásad a profilů pro uživatele nebo zařízení v oboru (skupiny).
    - Scope (skupiny) = skupina zabezpečení s názvem uživatelé v Seattlu. Všichni uživatelé nebo zařízení v této skupině můžou mít svoje profily a zásady spravované správci v členech (skupinách). 
    - Scope (značky) = Seattle. Správci v členovi (skupinách) můžou vidět objekty Intune, které mají také značku oboru Seattle.
3. Přidejte značku oboru Seattle k zásadám a profilům, ke kterým chcete, aby správci členové (skupiny) měli přístup.
4. Přidejte značku oboru Seattle do zařízení, která mají být viditelná pro správce v členech (skupinách). 

## <a name="default-scope-tag"></a>Výchozí značka oboru
Výchozí značka oboru je automaticky přidána do všech netagovaných objektů, které podporují značky oboru.

Výchozí funkce značky oboru je podobná funkci obory zabezpečení ve službě Microsoft Endpoint Configuration Manager. 

## <a name="to-create-a-scope-tag"></a>Vytvoření značky oboru

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **Správa tenanta** > **role** > **oboru (značky)**  > **vytvořit**.
2. Na stránce **základy** zadejte **název** a volitelný **Popis**. Vyberte **Další**.
3. Na stránce **přiřazení** vyberte skupiny obsahující zařízení, kterým chcete přiřadit tuto značku oboru. Vyberte **Další**.
4. Na stránce **Revize + vytvořit** klikněte na **vytvořit**.

## <a name="to-assign-a-scope-tag-to-a-role"></a>Přiřazení značky oboru k roli

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte možnost **Správa tenanta** > **role** > **všechny role** > vyberte role > **přiřazení** > **přiřadit**.
2. Na stránce **základy** zadejte název a **Popis** **přiřazení** . Vyberte **Další**.
3. Na stránce **skupiny pro správu** zvolte **Vybrat skupiny, které se mají zahrnout**, a vyberte skupiny, které chcete použít jako součást tohoto přiřazení. Uživatelé v této skupině budou mít oprávnění ke správě uživatelů nebo zařízení v oboru (skupiny). Vyberte **Další**.

    ![Snímek obrazovky s vybranými skupinami členů](./media/scope-tags/select-member-groups.png)

4. Na stránce **skupiny oborů** vyberte jednu z následujících možností pro **přiřazení k**
    - **Vybrané skupiny**: vyberte skupiny obsahující uživatele/deivces, které chcete spravovat. Všichni uživatelé nebo zařízení ve vybraných skupinách budou spravováni uživateli ve skupinách pro správu.
    - **Všichni uživatelé**: všichni uživatelé můžou být spravováni uživateli ve skupinách pro správu.
    - **Všechna zařízení**: všechna zařízení můžou spravovat uživatelé ve skupinách pro správu.
    - **Všichni uživatelé a všechna zařízení**: uživatelé můžou spravovat všichni uživatelé a zařízení ve skupinách pro správu.

5. Klikněte na **Další**.
6. Na stránce **značky oboru** vyberte značky, které chcete přidat do této role. Uživatelé ve skupinách pro správu budou mít přístup k objektům Intune, které mají také stejnou značku oboru. Roli můžete přiřadit maximálně 100 značek oboru.
7. Kliknutím na tlačítko **Další** přejdete na stránku **Revize + vytvořit** a pak vyberte **vytvořit**.

## <a name="assign-scope-tags-to-other-objects"></a>Přiřadit značky oboru jiným objektům

Pro objekty, které podporují značky oboru, se značky oboru obvykle zobrazují v části **vlastnosti**. Pokud například chcete přiřadit značku oboru ke konfiguračnímu profilu, postupujte takto:

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení** > **konfigurační profily** > zvolit profil.

2. Zvolte **vlastnosti** > **rozsah (značky)**  > **upravit** > **Vyberte značky oboru** > vyberte značky, které chcete přidat do profilu. Objektu můžete přiřadit maximálně 100 značek rozsahu.
4. Zvolte **možnost vybrat** > **Revize a uložit**.

## <a name="scope-tag-details"></a>Podrobnosti o značce oboru
Při práci s štítky oboru si pamatujte tyto podrobnosti: 

- Pokud má tenant více verzí tohoto objektu (například přiřazení rolí nebo aplikace), můžete přiřadit značky oboru k typu objektu Intune.
  Následující objekty Intune jsou výjimkou tohoto pravidla a aktuálně nepodporují značky oboru:
    - Profily ESP Windows
    - Kategorie zařízení
    - Omezení registrace
    - Identifikátory zařízení Corp
    - Zařízení autopilotu
    - Umístění dodržování předpisů pro zařízení
    - Zařízení Jamf
- Aplikace VPP a e-knihy přidružené k tokenu VPP dědí značky oboru přiřazené k přidruženému tokenu VPP.
- Zařízení Program registrace zařízení (DEP) a profily DEP přidružené k tomuto tokenu DEP dědí značky oboru přiřazené k přidruženému tokenu DEP.
- Když správce vytvoří v Intune objekt, všechny značky oboru přiřazené tomuto správci se automaticky přiřadí k novému objektu.
- Pro role Azure Active Directory se nepoužívá nastavení RBAC pro Intune. Role Správci služby Intune a globální Správci proto mají úplný přístup správce k Intune bez ohledu na to, jaké obory mají.
- Pokud přiřazení role nemá žádnou značku oboru, může správce IT Zobrazit všechny objekty na základě oprávnění správců IT. Správci, kteří nemají značky oboru v podstatě mají všechny značky oboru.
- Můžete přiřadit pouze značku oboru, kterou máte v přiřazení role.
- Můžete cílit jenom na skupiny, které jsou uvedené v oboru (skupiny) přiřazení role.
- Pokud máte ke své roli přiřazenou značku oboru, nemůžete odstranit všechny značky oboru v objektu Intune. Vyžaduje se aspoň jedna značka oboru.

## <a name="next-steps"></a>Další kroky

Přečtěte si, jak se značky oboru chovají, když existuje [více přiřazení rolí](role-based-access-control.md#multiple-role-assignments).
Spravujte [role](role-based-access-control.md) a [profily](../configuration/device-profile-assign.md).


