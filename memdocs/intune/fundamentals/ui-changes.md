---
title: Kde v Azure najdu svoje funkce Intune?
titleSuffix: Microsoft Intune
description: Tento článek vám pomůže najít funkce Microsoft Intune na portálu Azure Portal.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 1/4/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 809d9d76-20f8-4329-9e18-cd7d4946a9af
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5ff2898f97bbef4cba0d14d4810a503d613cff18
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82077916"
---
# <a name="where-did-my-intune-feature-go-in-azure"></a>Kde v Azure najdu svoje funkce Intune?
Při přesunu Intune do portálu Azure Portal jsme využili příležitost uspořádat některé úlohy logičtěji. Každé vylepšení ale přichází za cenu toho, že je potřeba se s novým uspořádáním seznámit. Tato referenční příručka je určena uživatelům, kteří znají dobře Intune na klasickém portálu a zajímá je, jak s Intune pracovat na webu Azure Portal. Pokud tento článek nepopisuje funkci, kterou se pokoušíte najít, ponechte na konci článku komentář, abychom ho mohli aktualizovat.
## <a name="quick-reference-guide"></a>Stručná referenční příručka

|Funkce |Cesta na klasickém portálu|Cesta v Intune na Azure Portalu|
|------------|---------------|---------------|
|Program registrace zařízení (DEP)[jenom iOS]|Správce > Správa mobilních zařízení > iOS > Program registrace zařízení|[Registrace zařízení > Registrace Apple > Token Programu registrace](#where-did-apple-dep-go) |
|Program registrace zařízení (DEP)[jenom iOS]| Správce > Správa mobilních zařízení > iOS a Mac OS X > Program registrace zařízení |[Registrace zařízení > Registrace Apple > Sériová čísla programu registrace](#where-did-apple-dep-go) |
|Pravidla registrace |Správce > Správa mobilních zařízení > Pravidla registrace|[Registrace zařízení > Omezení registrace](#where-did-enrollment-rules-go) |
|Skupiny podle sériového čísla iOSu |Skupiny > Všechna zařízení > Firemní předregistrovaná zařízení > Podle sériového čísla iOS|[Registrace zařízení > Registrace Apple > Sériová čísla programu registrace](#where-did-corporate-pre-enrolled-devices-go) |
|Skupiny podle sériového čísla iOSu |Skupiny > Všechna zařízení > Firemní předregistrovaná zařízení > Podle sériového čísla iOS| [Registrace zařízení > Registrace Apple > Sériová čísla AC](#where-did-corporate-pre-enrolled-devices-go)|
|Skupiny podle IMEI (všechny platformy)| Skupiny > Všechna zařízení > Firemní předregistrovaná zařízení > Podle IMEI (všechny platformy) | [Registrace zařízení > Identifikátory podnikových zařízení ](#by-imei-all-platforms)|
| Profil Registrace podnikového zařízení| Zásady > Registrace podnikového zařízení | [Registrace zařízení > Registrace Apple > Profily Programu registrace](#where-did-corporate-pre-enrolled-devices-go) |
| Profil Registrace podnikového zařízení | Zásady > Registrace podnikového zařízení | [Registrace zařízení > Registrace Apple > Profily AC](#where-did-corporate-pre-enrolled-devices-go) |
| Android for Work | Správce > Správa mobilních zařízení > Android for Work | Registrace zařízení > Registrace Androidu |
| Podmínky a ujednání | Zásady > Podmínky a ujednání | Registrace zařízení > Podmínky a ujednání |
Nastavení Portálu společnosti|Správce > Portál společnosti|**Správa** > Mobilní aplikace<br> **Nastavení** > Značky Portálu společnosti


## <a name="where-do-i-manage-groups"></a>Kde můžu spravovat skupiny?
Intune na Azure Portalu používá ke správě skupin službu [Azure Active Directory (AD)](https://docs.microsoft.com/azure/active-directory/active-directory-groups-create-azure-portal).

## <a name="where-did-enrollment-rules-go"></a>Kde najdu pravidla registrace?
Na klasickém portálu jste mohli nastavit pravidla, která řídí registraci mobilních a dalších moderních zařízení s Windows a macOS do MDM.

![Obrázek klasických pravidel registrace mobilních zařízení](./media/ui-changes/01-classic-rules.png)

Tato pravidla platila bez výjimky pro všechny uživatele ve vašem účtu Intune. Na webu Azure Portal jsou místo těchto pravidel dva různé typy zásad: omezení typu zařízení a omezení limitů počtů zařízení.

![Obrázek omezení registrace mobilních zařízení v Azure](./media/ui-changes/02-azure-enroll-restrictions.png)

Výchozí omezení limitu počtu zařízení odpovídá limitu pro registraci zařízení na klasickém portálu.

![Obrázek omezení počtů zařízení v Azure](./media/ui-changes/03-azure-device-limit.png)

Výchozí omezení typu zařízení odpovídá na klasickém portálu omezením platformy.

![Obrázek omezení typu zařízení v Azure](./media/ui-changes/04-azure-platform-restrictions.png)

Možnost povolit nebo zablokovat zařízení v osobním vlastnictví se teď spravuje v rámci konfigurace platforem omezení typu zařízení.

![Obrázek nastavení blokování osobních zařízení v Azure](./media/ui-changes/05-azure-personal-block.png)

Nové možnosti omezení se přidají jenom do portálu Azure Portal.

## <a name="where-did-my-conditional-access-policies-go"></a>Kde se zásady podmíněného přístupu přecházejí?
Jakmile se tenant migruje do Azure Portal, budou zásady podmíněného přístupu vašeho tenanta i nadále vynutily. Z Intune na webu Azure Portal je ale nemůžete prohlížet ani upravovat.

Pokud chcete zobrazit a změnit zásady podmíněného přístupu z Azure Portal, bude nutné odebrat staré zásady z portálu Classic. A potom je znovu vytvořit na webu Azure Portal. Další informace o migraci zásad podmíněného přístupu najdete v tématu [migrace klasických zásad na webu Azure Portal](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-migration). 

## <a name="where-did-my-compliance-policies-go"></a>Kde jsou moje zásady dodržování předpisů?
Po migraci tenanta na web Azure Portal zůstávají zásady dodržování předpisů tenanta nadále v platnosti. Z Intune na webu Azure Portal je ale nemůžete prohlížet ani upravovat.

Pokud chcete zásady dodržování předpisů zobrazovat a měnit na webu Azure Portal, musíte staré zásady odebrat z klasického portálu. A potom je znovu vytvořit na webu Azure Portal. Další informace o zásadách dodržování předpisů pro zařízení najdete v článku o tom, [jak začít používat zásady dodržování předpisů pro zařízení v Intune](../protect/device-compliance-get-started.md). 

## <a name="where-did-apple-dep-go"></a>Kde najdu Program registrace zařízení (DEP) Apple?
Na klasickém portálu můžete nastavit integraci Intune s Program registrace zařízení společnosti Apple a ručně vyžádat synchronizaci se službou společnosti Apple:

![Obrázek klasického tokenu DEP](./media/ui-changes/06-classic-dep-token.png)

Na portálu Azure Portal můžete Program registrace zařízení Apple nastavit stejným postupem jako v klasickém Intune:

![Obrázek tokenu DEP v Azure](./media/ui-changes/07-azure-dep-token.png)

Možnost **Synchronizovat** na klasickém portálu se ale přesunula do pracovního postupu správy sériových čísel, protože se tam zobrazí výsledky ruční synchronizace:

![Obrázek synchronizace DEP v Azure](./media/ui-changes/08-azure-dep-sync.png)

## <a name="where-did-corporate-pre-enrolled-devices-go"></a>Kde najdu firemní předregistrovaná zařízení?
### <a name="by-ios-serial-number"></a>Podle sériového čísla iOSu
Na klasickém portálu můžete zařízení s iOSem registrovat prostřednictvím Programu registrace zařízení (DEP) Apple a Apple Configuratoru. Obě metody nabízejí předregistraci zařízení podle sériového čísla a zahrnují přiřazení speciálních profilů Registrace podnikového zařízení. Ještě před registrací můžete přiřazení profilu registrace spravovat prostřednictvím skupiny zařízení **Firemní předregistrované zařízení podle sériového čísla iOS**:

![Obrázek klasických sériových čísel Apple](./media/ui-changes/09-classic-apple-serials.png)

Tam najdete sériová čísla pro registraci pomocí DEP Apple i Apple Configuratoru v jednom seznamu. Abychom omezili neshody při přiřazení profilů (profil DEP přiřazený sériovému číslu AC a naopak), rozdělili jsme sériová čísla na portálu Apple Portal do dvou seznamů:

**Sériová čísla**
![DEP obrázek sériových čísel DEP v Azure](./media/ui-changes/10-azure-dep-serials.png)

**Sériová čísla**
![Apple Configuratoru obrázek sériových čísel Apple Configuratoru v Azure](./media/ui-changes/11-azure-ac-serials.png)

### <a name="by-imei-all-platforms"></a>Podle IMEI (všechny platformy)

Na klasickém portálu můžete předem vytvořit seznam čísel IMEI zařízení, která se při registraci do Intune označí jako firemní:

![Obrázek klasického seznamu čísel IMEI](./media/ui-changes/12-classic-corp-imei.png)

Na Azure Portalu musíte stejné číslo IMEI nahrát do seznamu identifikátorů podnikových zařízení pomocí textového souboru s oddělovači (CSV). Nový portál nepodporuje ruční zadání čísel IMEI:

![Obrázek seznamu čísel IMEI v Azure](./media/ui-changes/13-azure-corp-imei.png)

Intune na portálu Azure Portal je připravený na budoucnost díky podpoře jiných typů identifikátorů kromě IMEI, ale aktuálně umožňuje předběžné seznamy jenom čísel IMEI.

## <a name="where-did-corporate-device-enrollment-profiles-go"></a>Kde najdu profily registrace podnikového zařízení?
Pokud chcete registrovat zařízení s iOSem prostřednictvím Programu registrace zařízení (DEP) Apple nebo pomocí Apple Configuratoru, musíte zadat profil registrace podnikového zařízení, kterému se má zařízení přiřadit. Na klasickém portálu se vytváření a správa těchto profilů prováděla v jednom seznamu:

![Obrázek klasických profilů registrace zařízení](./media/ui-changes/14-classic-corp-profiles.png)

Tento seznam ukazuje profily povolené pro použití s Programem registrace zařízení (DEP) Apple (**DEP zapnuto**) a profil povolený jenom pro použití s Apple Configuratorem (**DEP vypnuto**).

Abychom omezili možnost záměny obou typů profilů a potenciální nesprávná přiřazení (profil DEP přiřazený zařízením Configuratoru a naopak), oddělili jsme tvorbu a správu profilů programu registrace (podporují Program registrace zařízení Apple i Apple School Manager) a profilů Apple Configuratoru:

**Profily DEP obrázek**
![DEP Azure](./media/ui-changes/15-azure-dep-profiles.png)

**Profily Apple Configuratoru**
obrázek profilů Apple Configuratoru![v Azure](./media/ui-changes/16-azure-ac-profiles.png)
