---
title: Správa hromadně zakoupených e-knih pro iOS/iPadOS
titleSuffix: Microsoft Intune
description: Zjistěte, jak synchronizovat s Intune knihy zakoupené v rámci multilicenčního programu z obchodu pro iOS a jak následně spravovat a sledovat jejich používání.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/26/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f5617074-2384-4812-b913-dc94f64c0818
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 548174cfa891e832f9392604cca8347493db3dab
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "80323569"
---
# <a name="how-to-manage-iosipados-ebooks-you-purchased-through-a-volume-purchase-program-with-microsoft-intune"></a>Jak spravovat e-knihy pro iOS/iPadOS, které jste koupili prostřednictvím programu hromadného nákupu, pomocí Microsoft Intune


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Program Apple Volume Purchase Program (VPP) umožňuje nakoupit více licencí ke knize, kterou chcete distribuovat uživatelům ve vaší společnosti. Distribuovat je možné knihy z komerčních obchodů nebo obchodů s produkty určenými pro vzdělávání.

Microsoft Intune pomáhá synchronizovat, spravovat a přiřazovat knihy, které jste zakoupili prostřednictvím tohoto programu. Můžete naimportovat informace o licencích z obchodu a sledovat, kolik licencí jste použili.

Postupy při správě knih jsou podobné jako u [správy aplikací VPP](vpp-apps-ios.md).

## <a name="manage-volume-purchased-books-for-ios-devices"></a>Správa knih zakoupených v rámci multilicenčního programu pro zařízení s iOSem
Koupíte si více licencí pro knihy iOS/iPadOS prostřednictvím [Apple Volume purchase program pro firmy](https://www.apple.com/business/vpp/) nebo [Apple Volume purchase program pro vzdělávání](https://volume.itunes.apple.com/us/store). Součástí tohoto procesu je vytvoření účtu Apple VPP na webu Apple a odeslání tokenu Apple VPP do Intune.  Potom je možné synchronizovat informace o nákupu v rámci multilicenčního programu s Intune a sledovat využití knih, které jste tímto způsobem koupili.

## <a name="before-you-start"></a>Než začnete
Než začnete, musíte od společnosti Apple získat token VPP a nahrát ho do svého účtu Intune. Dále:

* Pokud jste už dřív použili token VPP s jiným produktem, musíte pro Intune vygenerovat nový token.
* Tokeny mají platnost jeden rok.
* Ve výchozím nastavení se Intune synchronizuje se službou Apple VPP dvakrát denně. Ruční synchronizaci můžete spustit kdykoli.
* Po naimportování tokenu VPP do Intune neimportujte stejný token do žádného jiného řešení správy zařízení. Pokud byste to udělali, mohli byste ztratit přiřazení licence a uživatelských záznamů.
* Než začnete používat iOS/iPadOS Books s Intune, odeberte všechny existující uživatelské účty VPP vytvořené pomocí jiných dodavatelů správy mobilních zařízení (MDM). V rámci bezpečnostních opatření Intune nesynchronizuje tyto uživatelské účty do Intune. Intune synchronizuje jenom ta data ze služby Apple VPP, která jsou vytvořená pomocí Intune.
* Když přiřadíte knihu k zařízení, musí být v daném zařízení nainstalovaná integrovaná aplikace iBooks. Pokud není, musí koncový uživatel aplikaci přeinstalovat, aby si mohl knihu přečíst. V současné době není možné prostřednictvím Intune obnovit odebrané integrované aplikace.
* Přiřadit je možné jenom knihy z webu Apple Volume Purchase Program. Není možné nahrát a potom přiřadit knihy, které jste vytvořili interně.
* V současné době není možné přiřazovat ke kategoriím koncových uživatelů knihy stejně jako aplikace.
* Po přiřazení knihy už není možné licenci vrátit zpět.
* Když se uživatel s oprávněným zařízením pokusí poprvé o instalaci knihy VPP, musí se před tím, než si bude moct knihu nainstalovat, připojit k programu Apple Volume Purchase. Licence také můžete přiřadit ke skupinám zabezpečení se spravovanými identifikátory Apple ID. V takovém případě nebudou uživatelé po instalaci knihy vyzváni k zadání Apple ID.
* Zařízení musí být zaregistrovaná s přidružením uživatele, protože elektronické knihy je možné přiřadit jenom skupinám uživatelů.   


## <a name="to-get-and-upload-an-apple-vpp-token"></a>Získání a odeslání tokenu Apple VPP

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte možnost konektory **správy** > tenanta**a tokeny** > programu**Apple VPP**.
3. V podokně se seznamem tokenů VPP klikněte na **Vytvořit**.
5. V podokně **Nový token VPP** zadejte tyto informace:
    - **Soubor tokenu VPP** – je potřeba se zaregistrovat v rámci programu Volume Purchase Program for Business nebo Volume Purchase Program for Education. Potom si stáhněte token Apple VPP pro svůj účet a vyberte ho tady.
    - **Apple ID** – zadejte Apple ID účtu přidruženého k multilicenčnímu programu.
    - **Typ účtu VPP** – zvolte jednu z možností: **Obchodní** nebo **Vzdělávání**.
5. Až budete hotoví, klikněte na **Vytvořit**.

Token se zobrazí v podokně se seznamem tokenů.


Data ukládaná společností Apple můžete kdykoli synchronizovat s Intune výběrem položky **Synchronizovat nyní**.

## <a name="to-assign-a-volume-purchased-app"></a>Přiřazení aplikace zakoupené v rámci multilicenčního programu

1. Vyberte **Apps** > **eBooks**aplikace > pro**všechny e-knihy**.
2. V podokně se seznamem knih zvolte knihu, kterou chcete přiřadit, a pak zvolte **...** > **Přiřadit skupiny**.
3. V podokně <*název knihy*> – **Přiřazené skupiny** zvolte **Spravovat** > **Přiřazené skupiny**.
4. Zvolte **Přiřadit skupiny** a pak v podokně **Vybrat skupiny** zvolte skupiny uživatelů Azure AD, ke kterým chcete aplikaci přiřadit. V současné době není dostupná podpora skupin zařízení.
Jako akci přiřazení zvolte **K dispozici** nebo **Povinné**. 
5. Až to budete mít, zvolte **Uložit**.

## <a name="next-steps"></a>Další kroky

Informace, které vám pomůžou při sledování přiřazování knih, najdete v článku [Jak sledovat přiřazení aplikací](apps-monitor.md).






