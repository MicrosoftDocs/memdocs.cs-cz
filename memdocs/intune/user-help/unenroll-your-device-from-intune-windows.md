---
title: Odebrání zařízení s Windows ze systému správy Intune
description: Popisuje postup odebrání zařízení s Windows ze systému správy Intune.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/03/2018
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 018bda65-7238-41f5-b92a-e5f67b7fe085
searchScope:
- User help
ROBOTS: ''
ms.reviewer: jieyang
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 9e9101a46cac488ef8a80858377cbabac8dc7936
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881588"
---
# <a name="remove-your-windows-device-from-management"></a>Odebrání zařízení s Windows ze systému správy

Registrované zařízení s Windows můžete ze systému správy odebrat, pokud už nepotřebujete:  
* Používat zařízení pro práci nebo studium 
* Přistupovat k pracovním nebo školním e-mailům, aplikacím nebo jiným prostředkům

Jakmile registraci zařízení zrušíte, ztratí toto zařízení přístup ke školním nebo pracovním prostředkům. Ze systému správy můžete odebrat následující zařízení s Windows.  
* Zařízení s Windows 10 
* Počítač s Windows 8.1
* Telefon s Windows 8.1
 
Další informace o tom, co se stane, když zařízení odeberete ze systému správy, najdete v tématu s informacemi o tom, [co se stane, když zařízení odeberete z Intune](what-happens-if-you-unenroll-your-device-from-intune-windows.md).  

## <a name="remove-your-windows-10-device"></a>Odebrání zařízení s Windows 10
Provedením následujících kroků odeberete zařízení s Windows 10 ze systému správy.

### <a name="remove-in-company-portal-app-home-page"></a>Odebrání v aplikaci Portál společnosti, **domovská** stránka  

1. Otevřete aplikaci Portál společnosti.
2. Na **domovské stránce** přejděte dolů do části **Moje zařízení**.
3. Vyberte zařízení, které chcete odebrat.
3. V pravém horním rohu aplikace vyberte ikonu **Více**.
4. Vyberte **Odebrat**. 
5. Odebrání zařízení potvrďte výběrem možnosti **Odebrat**.  

### <a name="remove-in-company-portal-app-device-context-menu"></a>Odebrání v aplikaci Portál společnosti, místní nabídka zařízení  

1. Otevřete aplikaci Portál společnosti a přejděte na **Moje zařízení**.

    ![Příklad snímku obrazovky aplikace Portál společnosti pro Windows, domovská stránka, zvýrazněná část Moje zařízení](./media/1809_CheckAccess_Context_Select_Device.png)

2. Kliknutím pravým tlačítkem nebo stisknutím a podržením zařízení otevřete jeho [kontextovou nabídku](https://docs.microsoft.com//windows/uwp/design/controls-and-patterns/menus).  

3. Vyberte **Odebrat**.  

    ![Příklad snímku obrazovky s aplikací Portál společnosti pro Windows, domovská stránka Místní nabídka zařízení se zobrazuje na stránce v části Moje zařízení a zobrazuje akce Přejmenovat, Odebrat a Zkontrolovat přístup.](./media/1809_DeviceContextMenu_Windows_CP.png)  

5. V části potvrzení klikněte na **Další informace** a přečtěte si, jakým způsobem se váš přístup k pracovním a školním prostředkům může změnit. Odebrání zařízení potvrďte výběrem možnosti **Odebrat**.   

     ![Příklad snímku obrazovky s aplikací Portál společnosti pro Windows, domovská stránka Nad zařízením se zobrazí pole Přejmenovat, do kterého uživatel může napsat nový název a může kliknout na Přejmenovat nebo Zrušit.](./media/1808_RemoveDevice_Popup.png)  


### <a name="remove-in-device-settings-app"></a>Odebrání v aplikaci Nastavení zařízení
1. Otevřete aplikaci Nastavení. 
2. Přejděte na **účty**  >  **přístup do práce nebo do školy**.
3. Vyberte připojený účet, který chcete odebrat > **Odpojit**.
4. Odebrání zařízení potvrďte výběrem možnosti **Ano**.

## <a name="remove-your-windows-81-computer"></a>Odebrání počítače s Windows 8.1
Provedením následujících kroků odeberte počítač s Windows 8.1 z Intune.

1. Přejít na **nastavení počítače**  >  **síť**  >  **pracoviště**.
2. V části **Připojení pracovního místa** vyberte **Odejít**.
3. V části **Zapnout správu zařízení** vyberte **Vypnout**.
4. V automaticky otevíraném okně, které se otevře, vyberte **Vypnout**.

## <a name="remove-your-windows-81-phone"></a>Odebrání telefonu s Windows 8.1
Provedením následujících kroků odeberte telefon s Windows 8.1 z Intune.

1. Přejít na **Nastavení**  >  **pracoviště**.
2. Klepněte na pracovní účet, jehož registraci chcete zrušit.
3. V dolní části obrazovky klepněte na **Odstranit**.
4. V dialogovém okně **Odstranit účet** klepněte na **Odstranit**.  
## <a name="removing-your-personal-information-after-removing-the-company-portal"></a>Odebrání osobních údajů po odebrání aplikace Portál společnosti  

Aplikace Portál společnosti ukládá do zařízení s Windows dva druhy dat:

- **Protokoly pro diagnostiku**: Standardní data o aktivitě, která Microsoft shromažďuje. Tato data se automaticky vymažou při odinstalaci aplikace Portál společnosti. Data o aktivitě aplikací jsou například data o tom, jak dlouho byla aplikace otevřena nebo jestli se chybově ukončila.
- **Mezipaměť aplikace**: Podpůrné soubory, které aplikace potřebuje k práci, například ikony a nastavení.

Pokud chcete odstranit uložené protokoly a mezipaměť, proveďte jeden z následujících kroků:

* [Odinstalace aplikace Portál společnosti](https://support.microsoft.com/help/4028003/windows-10-uninstall-apps-and-programs) 

* Resetujte aplikaci Portál společnosti. Otevřete aplikaci **Nastavení** a vyberte > **aplikace**  >  **portál společnosti**  >  **Upřesnit možnosti**  >  **obnovit**. 

Potřebujete ještě další pomoc? Obraťte se na podporu ve vaší společnosti. Kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).
