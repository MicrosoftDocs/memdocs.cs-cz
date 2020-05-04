---
title: 'Rychlý start: Vytvoření skupiny pro správu uživatelů'
titleSuffix: Microsoft Intune
description: V tomto rychlém startu použijete Microsoft Intune k vytvoření skupiny ze stávajících uživatelů.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/17/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 723f4b4e-3090-4811-84ff-6af652abea5a
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d7adb23f4709bf3ead07a01cb00d1b38fcb23c40
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79330807"
---
# <a name="quickstart-create-a-group-to-manage-users"></a>Rychlý start: Vytvoření skupiny pro správu uživatelů

V tomto rychlém startu použijete Intune k vytvoření skupiny ze stávajících uživatelů. Skupiny se používají ke správě uživatelů a řídí přístup zaměstnanců k firemním prostředkům. Tyto prostředky mohou být částí firemního intranetu nebo může jít o externí prostředky, jako jsou weby SharePointu, aplikace SaaS nebo webové aplikace.

Pokud nemáte předplatné Intune, [Zaregistrujte si bezplatný zkušební účet](free-trial-sign-up.md).

>[!NOTE]
>V Intune máte v konzole pohodlně k dispozici předem vytvořené skupiny **Všichni uživatelé** a **Všechna zařízení** s integrovanými optimalizacemi.

## <a name="prerequisites"></a>Požadavky

- Předplatné Microsoft Intune – [zaregistrujte si bezplatný zkušební účet](../fundamentals/free-trial-sign-up.md).
- K dokončení tohoto rychlého startu potřebujete [vytvořit uživatele](quickstart-create-user.md).

## <a name="sign-in-to-intune-in-the-microsoft-endpoint-manager"></a>Přihlášení k Intune ve službě Microsoft Endpoint Manager

Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) jako [globální správce nebo správce služby Intune](users-add.md#types-of-administrators). Pokud jste vytvořili zkušební předplatné Intune, účet, z něhož jste toto předplatné vytvořili, je globálním správcem.

## <a name="create-a-group"></a>Vytvoření skupiny

Vytvoříte skupinu, kterou použijete později v tomto seriálu rychlých startů. Vytvoření skupiny:

1. Po otevření **Microsoft Endpoint Manageru**vyberte **skupiny** > **Nová skupina**.
2. V rozevíracím seznamu **Typ skupiny** vyberte **Zabezpečení**.
3. Do pole **název skupiny** zadejte název nové skupiny (například **testery contoso**).
4. Přidejte **Popis skupiny** .
5. **Typ členství** nastavte na **Přiřazeno**. 
6. V části **Členové**vyberte odkaz a přidejte v seznamu jednoho nebo více členů skupiny.

    ![Snímek obrazovky s vytvořením skupiny v Microsoft Intune](./media/quickstart-create-group/quickstart-use-groups-01.png)

7. Klikněte na **Vybrat** > **vytvořit**.

Po úspěšném vytvoření se skupina zobrazí v seznamu **Všechny skupiny**. 

## <a name="next-steps"></a>Další kroky

V tomto rychlém startu jste použili Intune k vytvoření skupiny ze stávajících uživatelů. Další informace o přidávání skupin do Intune najdete v článku [Přidání skupin pro uspořádání uživatelů a zařízení](groups-add.md).

Pokud chcete postupovat podle této série rychlých startů Intune, pokračujte k dalšímu rychlému startu.

> [!div class="nextstepaction"]
> [Rychlý start: Nastavení automatické registrace zařízení s Windows 10](../enrollment/quickstart-setup-auto-enrollment.md)
