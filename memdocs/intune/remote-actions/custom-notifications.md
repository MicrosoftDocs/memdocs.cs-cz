---
title: Odesílání vlastních oznámení uživatelům pomocí Microsoft Intune
titleSuffix: Microsoft Intune
description: Použití Intune k vytváření a odesílání vlastních nabízených oznámení uživatelům zařízení se systémem iOS/iPadOS a Androidem
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: jinyoon
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0ef8989c9f4de0211a7636c747ff9a01111842f6
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80325312"
---
# <a name="send-custom-notifications-in-intune"></a>Odesílání vlastních oznámení v Intune

Pomocí Microsoft Intune můžete odesílat vlastní oznámení uživatelům spravovaných zařízení se systémem iOS/iPadOS a Androidem. Tyto zprávy se zobrazí jako standardní nabízená oznámení z aplikace Portál společnosti a z aplikace Microsoft Intune na zařízení uživatele, stejně jako oznámení z jiných aplikací na zařízení. Zařízení macOS a Windows nepodporují vlastní oznámení Intune.

Vlastní zprávy s oznámením obsahují krátký nadpis a tělo zprávy o 500 nebo méně znaků. Tyto zprávy lze přizpůsobit pro jakýkoli obecný účel komunikace.

### <a name="what-the-notification-looks-like-on-an-iosipados-device"></a>Jak oznámení vypadá na zařízení se systémem iOS/iPadOS

Pokud máte aplikaci Portál společnosti otevřenou v zařízení se systémem iOS/iPadOS, oznámení se podobá následujícímu snímku obrazovky:

> [!div class="mx-imgBorder"]
> ![Portál společnosti testovací oznámení pro iOS/iPadOS](./media/custom-notifications/105046-1.png)

Pokud je zařízení uzamčené, oznámení se podobá následujícímu snímku obrazovky:

> [!div class="mx-imgBorder"]
> ![uzamčené zařízení iOS/iPadOS test Notification](./media/custom-notifications/105046-2.png)

### <a name="what-the-notification-looks-like-on-an-android-device"></a>Jak oznámení vypadá na zařízení s Androidem

Pokud máte aplikaci Portál společnosti otevřenou na zařízení s Androidem, oznámení se podobá následujícímu snímku obrazovky:

> [!div class="mx-imgBorder"]
> ![zkušebních oznámení pro Android](./media/custom-notifications/105046-3.png)

## <a name="common-scenarios-for-sending-custom-notifications"></a>Běžné scénáře odesílání vlastních oznámení  

- Upozorněte všechny zaměstnance změny v plánu, jako jsou uzávěry při sestavování z důvodu inclement počasí.
- Pošle uživateli oznámení o jednom zařízení, aby mohl sdělit naléhavou žádost, třeba restartování zařízení, aby se instalace aktualizace dokončila.

## <a name="considerations-for-using-custom-notifications"></a>Předpoklady pro používání vlastních oznámení

**Konfigurace zařízení**

- Aby uživatelé mohli přijímat vlastní oznámení, musí mít zařízení nainstalovanou aplikaci Portál společnosti nebo aplikaci Microsoft Intune. Musí mít taky nakonfigurovaná oprávnění, aby mohla aplikace Portál společnosti nebo aplikace Microsoft Intune posílat nabízená oznámení. V případě potřeby se aplikace Portál společnosti a aplikace Microsoft Intune můžou uživatele vyzvat, aby povolili oznámení.
- V Androidu je Služby Google Play požadovaná závislost.
- Zařízení musí být zaregistrované v MDM.

**Oprávnění**:

- Aby bylo možné odesílat oznámení do skupin, váš účet musí mít v Intune následující oprávnění RBAC: > *organizace* **aktualizace**.
- Aby bylo možné odesílat oznámení do zařízení, musí mít váš účet v Intune následující oprávnění RBAC: *vzdálené úlohy* > **odesílají vlastní oznámení**.

**Vytváření oznámení**:
 
- Pokud chcete vytvořit zprávu, použijte účet, ke kterému je přiřazená role Intune, která obsahuje správné oprávnění, jak je popsané v předchozí části *oprávnění* . Postup přiřazení oprávnění uživateli najdete v tématu [přiřazení rolí](../fundamentals/role-based-access-control.md#role-assignments).
- Vlastní oznámení jsou omezená na 50 znaků a zprávy 500-Character.  
- Intune neukládá text z dříve odeslaných vlastních oznámení. Chcete-li znovu odeslat zprávu, je nutné tuto zprávu znovu vytvořit.  
- Do skupin za hodinu můžete poslat až 25 zpráv. Toto omezení je na úrovni tenanta. Toto omezení se nevztahuje na odesílání oznámení jednotlivcům.
- Když odesíláte zprávy do jednotlivých zařízení, můžete do stejného zařízení poslat až 10 zpráv za hodinu.
- Můžete odesílat oznámení uživatelům ve skupinách. Při odesílání oznámení do skupin může každé oznámení směrovat přímo na 25 skupin. Vnořené skupiny se do tohoto součtu nepočítají. Při odesílání oznámení do skupiny se zprávy zaměřují jenom na uživatele ve skupině a odesílají se do každého zařízení s iOS/iPadOS nebo Androidem, které uživatel zaregistroval. Zařízení ve skupině budou při cílení na oznámení ignorována.
- Oznámení můžete odesílat do jediného zařízení. Místo používání skupin vyberte zařízení a pak použijte [akci vzdáleného zařízení](device-management.md#available-device-actions) k odeslání vlastního oznámení.

**Doručení**:

- Intune pošle zprávy do aplikace Portál společnosti uživatelů nebo do aplikace Microsoft Intune, která pak vytvoří nabízené oznámení. Uživatelé nemusí být přihlášeni do aplikace, aby bylo oznámení na zařízení vloženo, ale zařízení musí být zaregistrováno cílovým uživatelem.
- Intune, Portál společnosti aplikace a aplikace Microsoft Intune, nemůžou zaručit doručení vlastního oznámení. Vlastní oznámení se můžou zobrazovat i po několika hodinách, pokud je to u všech, takže by se nemuseli používat pro naléhavé zprávy.
- Vlastní oznamovací zprávy z Intune se na zařízeních zobrazují jako standardní nabízená oznámení. Pokud je aplikace Portál společnosti v zařízení se systémem iOS nebo iPadOS otevřená při přijetí oznámení, zobrazí se v aplikaci oznámení místo jako nabízené oznámení systému.  
- Vlastní oznámení můžete zobrazit na zamykací obrazovce na zařízeních s iOS/iPadOS a Androidem v závislosti na nastavení zařízení.  
- V zařízeních s Androidem můžou mít další aplikace přístup k datům ve vlastních oznámeních. Nepoužívejte je pro citlivou komunikaci.  
- Uživatelé zařízení, kteří se nedávno zaregistrovali, nebo uživatelé, kteří byli odebráni ze skupiny, můžou dál dostávat vlastní oznámení, které se později pošle do této skupiny.  Podobně platí, že pokud přidáte uživatele do skupiny po odeslání vlastního oznámení do skupiny, je možné, že nově přidaná zpráva byla přijata k přijetí dříve odeslané zprávy s oznámením.  

## <a name="send-a-custom-notification-to-groups"></a>Odeslání vlastního oznámení do skupin

1. Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) pomocí účtu, který má oprávnění k vytváření a odesílání oznámení, a přejít na **správu tenanta** > **vlastní oznámení**.  

2. Na kartě základy zadejte následující příkaz a pokračujte výběrem **Další** .  
   - **Title** – zadejte název tohoto oznámení. Názvy jsou omezeny na 50 znaků.  
   - **Tělo** – zadejte zprávu. Zprávy jsou omezené na 500 znaků.

   ![Vytvoření vlastního oznámení](./media/custom-notifications/custom-notifications.png)  

3. Na kartě **přiřazení** vyberte skupiny, kterým chcete poslat toto vlastní oznámení, a pak pokračujte výběrem další. Odeslání oznámení skupině bude cílit jenom na uživatele této skupiny. oznámení bude odesláno do všech zařízení s iOS/iPadOS a Androidem zaregistrovaných tímto uživatelem.

4. Na kartě **Revize + vytvořit** zkontrolujte informace a až budete připraveni odeslat oznámení, vyberte **vytvořit**.  

Intune zpracovává zprávy, které vytvoříte hned. Jediným potvrzením, že se zpráva poslala, je oznámení Intune, které potvrdí, že se poslalo vlastní oznámení.  

![Potvrzení odeslaného oznámení](./media/custom-notifications/notification-sent.png)  

Intune nesleduje vlastní oznámení, která odesíláte, a zařízení neprotokolují příjem mimo centrum oznámení zařízení. Oznámení může být obsaženo v dočasném diagnostickém protokolu, pokud uživatel požaduje podporu v rámci aplikace Portál společnosti nebo Intune.

## <a name="send-a-custom-notification-to-a-single-device"></a>Odeslání vlastního oznámení na jedno zařízení

1. Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) pomocí účtu, který má oprávnění k vytváření a odesílání oznámení, a pak na **zařízení** > **všechna zařízení**.

2. Poklikejte na název spravovaného zařízení, do kterého chcete odeslat oznámení. otevře se stránka s *přehledem* zařízení.

3. Na stránce **Přehled** zařízení vyberte akci **Odeslat vlastní oznámení** a otevřete podokno *Odeslat vlastní* oznámení. Pokud tato možnost není k dispozici, vyberte možnost **...** (tři tečky) v pravém horním rohu stránky a pak vyberte **Odeslat vlastní oznámení**.

4. V podokně **Odeslat vlastní oznámení** zadejte následující podrobnosti zprávy:  

   - **Title** – zadejte název tohoto oznámení. Názvy jsou omezeny na 50 znaků.  
   - **Tělo** – zadejte zprávu. Zprávy jsou omezené na 500 znaků.  

5. Vyberte **Odeslat** a odešlete tak vlastní oznámení do zařízení. Na rozdíl od oznámení, která odesíláte do skupin, nekonfigurujte přiřazení ani před odesláním zprávy zkontrolovat.  

Intune zpracovává zprávu hned. Jediným potvrzením, že zpráva byla odeslána, je oznámení Intune, které obdržíte v konzole nástroje, ve kterém se zobrazí text zprávy, kterou jste odeslali.  

## <a name="receive-a-custom-notification"></a>Přijetí vlastního oznámení

Na zařízení uživatelé uvidí vlastní oznamovací zprávy, které Intune odesílají jako standardní nabízené oznámení z aplikace Portál společnosti nebo z aplikace Microsoft Intune. Tato oznámení jsou podobná nabízeným oznámením, která uživatelé dostanou z jiných aplikací na zařízení.  

Pokud je v zařízeních se systémem iOS/iPadOS po přijetí oznámení otevřená aplikace Portál společnosti, zobrazí se v aplikaci oznámení místo nabízeného oznámení.  

Oznámení zůstane, dokud ho uživatel nezavře.  

## <a name="next-steps"></a>Další kroky

[Správa zařízení](device-management.md)
