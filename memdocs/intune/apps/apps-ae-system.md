---
title: Přidání aplikací pro Android Enterprise System do Microsoft Intune
titleSuffix: ''
description: Přečtěte si, jak přidat aplikace podnikového systému do Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4ee71bdcf45c4dc99b9c6b3eb889ba373ecadca9
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461840"
---
# <a name="add-android-enterprise-system-apps-to-microsoft-intune"></a>Přidání aplikací pro Android Enterprise System do Microsoft Intune

Před přiřazením aplikace k zařízení nebo skupině uživatelů je nejprve potřeba danou aplikaci přidat do Microsoft Intune. Systémové aplikace jsou podporované na zařízeních s Androidem Enterprise. Můžete povolit systémovou aplikaci pro [vyhrazená podniková zařízení s Androidem](../enrollment/android-kiosk-enroll.md), [plně spravovaná zařízení](../enrollment/android-fully-managed-enroll.md)nebo [podnikovou firmu v Androidu, která má vlastní pracovní profil](../enrollment/android-corporate-owned-work-profile-enroll.md).

## <a name="add-the-app"></a>Přidání aplikace

Aplikaci pro Android Enterprise System můžete do Intune přidat z Azure Portal tím, že provedete následující kroky:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace**  >  **všechny aplikace**  >  **Přidat**.
3. V podokně **Vybrat typ aplikace** v části dostupné **jiné** typy vyberte **aplikace pro Android Enterprise System**.
4. Klikněte na **Vybrat**. Zobrazí se kroky **Přidání aplikace** .
Na stránce **informace o aplikaci** přidejte podrobnosti o aplikaci:
    - **Název aplikace**: zadejte název aplikace.
    - **Vydavatel**: zadejte název vydavatele aplikace.  
    - **Název balíčku**: zadejte název balíčku. Intune ověří, jestli je název balíčku platný.
5. Kliknutím na tlačítko **Další** zobrazíte stránku **značky oboru** .
8. Klikněte na **Vybrat značky oboru** a volitelně přidejte značky oboru pro aplikaci. Další informace najdete v tématu [použití řízení přístupu na základě role (RBAC) a značek oboru pro distribuci](../fundamentals/scope-tags.md).
9. Kliknutím na tlačítko **Další** zobrazíte stránku **přiřazení** .
10. Vyberte přiřazení skupin pro aplikaci. Další informace najdete v tématu [Přidání skupin pro uspořádání uživatelů a zařízení](../fundamentals/groups-add.md). 
11. Kliknutím na **Další** zobrazte stránku **Revize + vytvořit** . Zkontrolujte hodnoty a nastavení, které jste zadali pro aplikaci.
12. Po dokončení klikněte na **vytvořit** , aby se aplikace přidala do Intune.

Zobrazí se okno **Přehled** aplikace, kterou jste vytvořili.

> [!NOTE]
> Abyste mohli najít název balíčku aplikace, kterou chcete povolit nebo zakázat, budete muset pracovat s výrobcem OEM vašeho zařízení.

Vytvořená aplikace se zobrazí v seznamu aplikací, kde ji můžete přiřazovat vybraným skupinám. 

Aplikace pro Android Enterprise System umožní nebo zakážou aplikace, které už jsou součástí platformy. Pokud chcete aplikaci povolit, přiřaďte systémovou aplikaci podle **potřeby**. Pokud chcete aplikaci zakázat, přiřaďte systémovou aplikaci jako **odinstalaci**. Systémové aplikace nelze přiřadit uživateli, který je k dispozici.


## <a name="next-steps"></a>Další kroky

- [Přiřazení aplikací skupinám](apps-deploy.md)
