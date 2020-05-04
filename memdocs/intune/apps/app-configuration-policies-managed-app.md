---
title: Zásady konfigurace aplikací pro spravované aplikace bez registrace zařízení
titleSuffix: Microsoft Intune
description: Přečtěte si, jak nakonfigurovat zásady pro spravované aplikace bez registrace zařízení.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/23/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: E61C1618-79D0-41A1-B61F-4123FB6672FC
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9729fa1fb89f31606c35d61773c224693e7da3c1
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "80323470"
---
# <a name="add-app-configuration-policies-for-managed-apps-without-device-enrollment"></a>Přidání zásad konfigurace aplikací pro spravované aplikace bez registrace zařízení

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Zásady konfigurace aplikací můžete používat se spravovanými aplikacemi, které podporují sadu Intune App SDK, i na nezaregistrovaných zařízeních. 

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2.  > Vyberte zásady **Apps** > **Konfigurace aplikací**aplikace**Přidat** > **spravované aplikace**.
3. Na stránce **základy** nastavte následující podrobnosti:
    - **Name (název**): název profilu, který se zobrazí v Azure Portal.
    - **Popis**: popis profilu, který se zobrazí v Azure Portal.
    - **Typ registrace zařízení**: je vybraná možnost spravované aplikace.
4. Zvolte **Vybrat veřejné aplikace** nebo **zvolte vlastní aplikace** a zvolte aplikaci, kterou chcete konfigurovat. Ze seznamu vyberte některou z aplikací, kterou jste schválili a synchronizovali s Intune.
5. Kliknutím na **Další** zobrazte stránku **Nastavení** .
6. Pro každé nastavení konfigurace podporované aplikací zadejte **název** a **hodnotu**. 

   Aplikace s povolenou sadou Intune App SDK podporují konfigurace v párech klíč-hodnota. Nahlédněte do dokumentace k jednotlivým aplikacím, kde zjistíte, které konfigurace klíč-hodnota se podporují. Připomínáme, že můžete používat tokeny, které se budou dynamicky plnit daty generovanými aplikací. Další informace najdete v tématu [konfigurační hodnoty pro používání tokenů](app-configuration-policies-managed-app.md#configuration-values-for-using-tokens). Informace o nastavení zásad konfigurace aplikace Outlook pro iOS/iPadOS najdete v tématu [Správa konfigurace aplikací pro iOS/iPadOS pomocí Microsoft Intune](https://technet.microsoft.com/library/mt813789(v=exchg.150).aspx).

    Pokud chcete konfiguraci odstranit, zvolte tři tečky (**…**) a vyberte **Odstranit**.  

7. Kliknutím na tlačítko **Další** zobrazíte stránku **přiřazení** .
8. Klikněte na **Vybrat skupiny, které chcete zahrnout**.
9. V podokně **Vybrat skupiny, které se mají zahrnout** vyberte skupinu a klikněte na **Vybrat**.
10. Klikněte na možnost **Vybrat skupiny, které se vyloučí** a zobrazte tak související podokno.
11. Vyberte skupiny, které chcete vyloučit, a potom klikněte na **Vybrat**.

    >[!NOTE]
    >Pokud přidáváte skupinu a pro daný typ přiřazení už byla zahrnuta jakákoliv jiná skupina, je pro ostatní typy zahrnutí přiřazení předem vybraná a není ji možné změnit. Tato použitá skupina se tedy nedá použít jako vyloučená skupina.

12. Kliknutím na **Další** zobrazte stránku **Revize + vytvořit** .
13. Kliknutím na **vytvořit** přidejte zásady konfigurace aplikací do Intune.

## <a name="configuration-values-for-using-tokens"></a>Hodnoty konfigurace pro používání tokenů

Intune může určité tokeny vygenerovat a odeslat je do spravované aplikace. Pokud třeba konfigurace aplikace umožňuje používat nastavení e-mailu, můžete pomocí tokenu přidat dynamický e-mail. Do pole **Název** zadejte název, který aplikace očekává, a potom do pole **Hodnota** zadejte `\{\{mail\}\}`.

Intune podporuje v nastavení konfigurace následující typy tokenů. Jiné vlastní dvojice klíč/hodnota nejsou podporované.

- \{\{userprincipalname\}\} – například John@contoso.com.
- \{\{mail\}\} – například John@contoso.com.
- \{\{partialupn\}\} – například John.
- \{\{accountid\}\} – například fc0dc142-71d8-4b12-bbea-bae2a8514c81.
- \{\{userid\}\} – například 3ec2c00f-b125-4519-acf0-302ac3761822.
- \{\{username\}\} – například John Doe.
- \{\{PrimarySMTPAddress\}\} – například testuser@ad.domain.com.

> [!Note]  
> Znaky \{\{ a \}\} se používají jenom pro typy tokenů a nesmí se používat pro jiné účely.

## <a name="next-steps"></a>Další kroky

Pokračujte s [přiřazením](apps-deploy.md) a [sledováním](apps-monitor.md) aplikace jako obvykle.
