---
title: Přidání webových aplikací do Microsoft Intune
titleSuffix: ''
description: Přečtěte si, jak přidat webové aplikace (aplikace klient-server) do Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5f08752f-0e87-4ad9-a34c-4991b3150775
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5fd0b368eac3e7c883f6e85e812f253707788239
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80325980"
---
# <a name="add-web-apps-to-microsoft-intune"></a>Přidání webových aplikací do Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune podporuje různé typy aplikací, včetně webových. Webová aplikace představuje aplikaci klient-server. Server poskytuje webovou aplikaci, která zahrnuje uživatelské rozhraní, obsah a funkce. Moderní webové hostingové platformy dále běžně nabízejí zabezpečení, vyrovnávání zatížení a další výhody. Webová aplikace se samostatně udržuje na webu. Na tento typ aplikace se odkazuje pomocí Microsoft Intune. Můžete také určit, které skupiny uživatelů mají k této aplikaci přístup. 

Abyste mohli aplikaci spravovat a přiřazovat ji uživatelům, přidejte ji do Intune. 

Intune vytvoří zástupce webové aplikace na zařízení uživatele. Pro zařízení s iOS/iPadOS se na domovskou obrazovku přidá zástupce webové aplikace. Pro zařízení s Androidem pro správu zařízení je zástupce webové aplikace přidaný do widgetu portálu společnosti Intune a pomůcka musí být připnuté ručně uživatelem. V případě zařízení s Windows je zástupce webové aplikace umístěný v nabídce Start.

> [!Note]
> Aby bylo možné spouštět webové aplikace, musí být na zařízení uživatele nainstalován prohlížeč. 
> 
> Pro zařízení s Androidem Enterprise najdete informace v tématu [spravované Google Play webové odkazy](apps-add-android-for-work.md#managed-google-play-web-links).
> 
> V případě zařízení se systémem iOS se nové webové klipy (připnuté webové aplikace) otevřou v Microsoft Edge místo Intune Managed Browser, pokud je to potřeba pro otevření v chráněném prohlížeči. U starších webových klipů pro iOS je nutné tyto webové klipy změnit na místo toho, aby je bylo možné otevřít v Microsoft Edge, Managed Browser.

## <a name="add-a-web-app-to-intune"></a>Přidání webové aplikace do Intune
Pokud chcete přidat aplikaci do Intune v podobě zástupce aplikace na webu, postupujte takto:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > **všechny aplikace** > **Přidat**.
3. V podokně **Vybrat typ aplikace** vyberte v části dostupné **jiné** typy možnost **webový odkaz**.
4. Klikněte na **Vybrat**. Zobrazí se kroky **Přidání aplikace** .
5. Na stránce **informace o aplikaci** přidejte následující informace:
    - **Název**: Zadejte název aplikace, který se zobrazí na Portálu společnosti. 

        > [!NOTE]
        > Pokud po nasazení a instalaci aplikace změníte název aplikace pomocí Intune na portálu Azure Portal, nebude už možné na tuto aplikaci cílit příkazy.

    - **Popis**: Zadejte popis aplikace. Tento popis se uživatelům zobrazí na Portálu společnosti.
    - **Vydavatel**: Zadejte název vydavatele této aplikace.
    - **Adresa URL aplikace**: Zadejte adresu URL webu hostujícího aplikaci, kterou chcete přiřadit.
    - **Kategorie**: Volitelně můžete vybrat jednu nebo několik předdefinovaných kategorií aplikací nebo kategorii, kterou jste vytvořili. Uživatelé tak při procházení Portálu společnosti najdou aplikaci snadněji.
    - **Zobrazit tuto aplikaci jako doporučenou aplikaci v portál společnosti**: tuto možnost vyberte, pokud chcete, aby se sada aplikací zobrazovala na hlavní stránce portálu společnosti, když uživatelé vyhledávají aplikace.
    - **K otevření tohoto odkazu vyžadovat spravovaný prohlížeč**: Tuto možnost vyberte, pokud chcete uživatelům webu nebo webové aplikace přiřadit odkaz, který mohou otevřít v prohlížeči spravovaném v Intune. Tento prohlížeč musí být nainstalovaný na jejich zařízení.
    - **Logo**: Nahrajte ikonu, která se přidruží k aplikaci. Tato ikona se u aplikace zobrazí, když uživatelé procházejí portál společnosti.
6. Kliknutím na tlačítko **Další** zobrazíte stránku **značky oboru** .
7. Klikněte na **Vybrat značky oboru** a volitelně přidejte značky oboru pro aplikaci. Další informace najdete v tématu [použití řízení přístupu na základě role (RBAC) a značek oboru pro distribuci](../fundamentals/scope-tags.md).
8. Kliknutím na tlačítko **Další** zobrazíte stránku **přiřazení** .
9. Vyberte přiřazení skupin pro aplikaci. Další informace najdete v tématu [Přidání skupin pro uspořádání uživatelů a zařízení](../fundamentals/groups-add.md). 
10. Kliknutím na **Další** zobrazte stránku **Revize + vytvořit** . Zkontrolujte hodnoty a nastavení, které jste zadali pro aplikaci.
11. Po dokončení klikněte na **vytvořit** , aby se aplikace přidala do Intune.

    Zobrazí se okno **Přehled** aplikace, kterou jste vytvořili.

> [!Note]
> V současné době je nasazení webových aplikací Intune do zařízení se systémem iOS/iPadOS přidruženo k profilu správy a nelze je odebrat ručně. Na portálu Intune můžete typ nasazení změnit na **Odinstalovat**. V tom případě můžete webovou aplikaci odebrat automaticky. Pokud byste, ještě než změníte přiřazení aplikace na **Odinstalovat**, odebrali nasazení, zůstane webová aplikace trvale v zařízení, dokud v Intune nezrušíte jeho registraci.

Koncoví uživatelé mohou spouštět webové aplikace přímo z aplikace Portál společnosti Windows výběrem webové aplikace a výběrem možnosti **otevřít v prohlížeči**. Publikovaná webová adresa URL se otevře přímo ve webovém prohlížeči. 

## <a name="next-steps"></a>Další kroky

Vytvořená aplikace se zobrazí v seznamu aplikací, kde ji můžete přiřazovat vybraným skupinám. Nápovědu najdete v článku [Přiřazení aplikací do skupin](apps-deploy.md). 
