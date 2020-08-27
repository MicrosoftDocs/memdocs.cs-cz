---
title: Kategorizace zařízení do skupin v Intune
titleSuffix: Microsoft Intune
description: Zjistěte, jak můžete pomocí kategorizace zařízení do skupin zajistit snadnější správu.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7b668c37-40b9-4c69-8334-5d8344e78c24
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: e6dae19e466d3d0e88ae07d1c82a63b098439632
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908611"
---
# <a name="categorize-devices-into-groups"></a>Zařazení zařízení do skupin

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Abyste usnadnili správu zařízení, můžete použít kategorie zařízení Microsoft Intune k automatickému přidávání zařízení do skupin na základě kategorií, které definujete.

Pro kategorie zařízení se používá následující pracovní postup:
1. Vytvořte kategorie, z kterých si uživatelé při registraci svého zařízení můžou vybrat.
2. Když uživatelé zařízení se systémem iOS/iPadOS a Androidem registrují zařízení, musí zvolit kategorii ze seznamu nakonfigurovaných kategorií. K přiřazení kategorie zařízení s Windows musí uživatelé použít web Portálu společnosti.
3. Do těchto skupin pak můžete nasadit zásady a aplikace.

Kategorie zařízení můžete vytvořit zcela podle svých potřeb. Příklad:
- Zařízení POS
- Předváděcí zařízení
- Sales
- Účetnictví
- Manager

## <a name="how-to-configure-device-categories"></a>Jak konfigurovat kategorie zařízení

### <a name="step-1-create-device-categories-on-the-intune-blade-of-the-azure-portal"></a>Krok 1: Vytvoření kategorií zařízení v okně Intune na portálu Azure Portal
1. Přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)a vyberte **zařízení**  >  **kategorie zařízení**.
2. Na stránce **Kategorie zařízení** zvolte **Vytvořit**, abyste mohli přidat novou kategorii.
3. V okně **Vytvořit kategorii zařízení** zadejte **název** nové kategorie a případně i její **popis**.
4. Po dokončení vyberte **Vytvořit**. Novou kategorii uvidíte v seznamu kategorií.

Název kategorie zařízení použijete při vytváření skupin zabezpečení Azure Active Directory (Azure AD) v kroku 2.

### <a name="step-2-create-azure-active-directory-security-groups"></a>Krok 2: Vytvoření skupin zabezpečení Azure Active Directory
V tomto kroku vytvoříte na webu Azure Portal dynamické skupiny na základě kategorie zařízení a názvu kategorie zařízení.

Pokud chcete pokračovat, přečtěte si v dokumentaci služby Azure AD téma [Vytváření rozšířených pravidel pomocí atributů](/azure/active-directory/users-groups-roles/groups-dynamic-membership#using-attributes-to-create-rules-for-device-objects).

S využitím informací v tomto oddílu můžete vytvořit skupinu zařízení s rozšířeným pravidlem využívajícím atribut **deviceCategory**. Příklad: **device.deviceCategory -eq** "*název kategorie zařízení, který jste získali z portálu Azure Portal*"

Až nakonfigurujete skupiny zařízení, bude se uživatelům při registrování jejich zařízení zobrazovat seznam nakonfigurovaných kategorií. Až si zvolí kategorii a dokončí registraci, přidá se jejich zařízení do skupiny zabezpečení Active Directory, která odpovídá zvolené kategorii.

### <a name="view-the-categories-of-devices-that-you-manage"></a>Zobrazení kategorií zařízení, která spravujete

1. Přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)a vyberte **zařízení**  >  **všechna zařízení**.

2. V seznamu zařízení zkontrolujte sloupec **Kategorie zařízení**.

Pokud sloupec **kategorie zařízení** není zobrazený, použijte **Columns**možnost  >  **Category**  >  **použít**kategorii sloupce.

### <a name="change-the-category-of-a-device"></a>Změna kategorie zařízení

1. Přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431), vyberte **zařízení**  >  **všechna zařízení** > vyberte zařízení, které chcete > **vlastností**.
2. V dalším okně můžete pro vybrané zařízení změnit nastavení **Kategorie zařízení** na kterýkoliv z názvů kategorií, které jste dříve nakonfigurovali.

## <a name="after-you-configure-device-groups"></a>Po konfiguraci skupin zařízení

Když uživatelé zařízení se systémem iOS/iPadOS a Androidem registrují svá zařízení, musí zvolit kategorii ze seznamu nakonfigurovaných kategorií. Jakmile zvolí kategorii a dokončí registraci, jejich zařízení se přidá do skupiny zařízení Intune nebo do skupiny zabezpečení Active Directory, která odpovídá zvolené kategorii.

Uživatelé s Windows musí k výběru kategorie použít web Portál společnosti.

Bez ohledu na platformu můžou uživatelé po registraci zařízení vždycky použít stránku portal.manage.microsoft.com. Požádejte uživatele, ať přejdou na web Portál společnosti a na něm do části **Moje zařízení**. Na této stránce můžou zvolit zaregistrované zařízení a pak vybrat kategorii.

Když vyberete kategorii, přidá se zařízení automaticky k příslušné vámi vytvořené skupině. Pokud se zařízení už zaregistrovalo předtím, než jste nakonfigurovali kategorie, uživateli se oznámení o něm zobrazí na webu Portál společnosti. To umožňuje uživateli, aby při příštím přístupu k aplikaci Portál společnosti v systému iOS/iPadOS nebo Android vybrala kategorii.

## <a name="further-information"></a>Další informace
- Kategorii zařízení můžete upravit na portálu Azure Portal, ale musíte ručně aktualizovat všechny skupiny zabezpečení Azure AD, které na tuto kategorii odkazují.

- Pokud některou kategorii odstraníte, zobrazí se u všech zařízení, která jsou do ní zařazená, hodnota **Nepřiřazeno**.