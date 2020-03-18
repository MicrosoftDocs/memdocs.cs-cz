---
title: Kontrola přístupu k zařízení | Microsoft Docs
description: Zkontrolujte přístup k zařízení, abyste zjistili, jestli vaše zařízení odpovídá požadavkům a je schopné přistupovat k pracovním nebo školním prostředkům.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/05/2018
ms.topic: article
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: f99a159a776e95c2f7ff8045a802b0c686672c9a
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79328291"
---
# <a name="check-access-from-company-portal-app-for-windows"></a>Kontrola přístupu z aplikace Portál společnosti pro Windows

Ověřte, že vaše zařízení má přístup k pracovním nebo školním prostředkům. 

Organizace vynucují požadavky &ndash; jako jsou třeba šifrování a omezení hesel, aby zajistily, že k jejich datům budou přistupovat pouze zabezpečená a důvěryhodná zařízení. Spravovaná zařízení musí splňovat a udržovat tyto požadavky, aby mohla přistupovat k prostředkům organizace.

Akce **Zkontrolovat přístup** vyhodnotí nastavení vašeho zařízení a jeho stav přístupu. Stránka **Detaily zařízení** obsahuje seznam nastavení, která musíte upravit, abyste znovu získali přístup. 

Proveďte kroky uvedené v tomto článku, abyste zkontrolovali přístup z aplikace Portál společnosti pro Windows.  

## <a name="check-access-from-device-details-page"></a>Kontrola přístupu ze stránky Detaily zařízení  
1. Otevřete aplikaci Portál společnosti pro Windows a přejděte na **Moje zařízení**.  

    ![Příklad snímku obrazovky aplikace Portál společnosti pro Windows, domovská stránka, zvýrazněná část Moje zařízení](./media/1809_CheckAccess_Context_Select_Device.png)  
2. Vyberte zařízení.  
3. Na stránce **Detaily zařízení** vyberte **Zkontrolovat přístup**. Aplikace synchronizuje vaše zařízení s aktuálními požadavky vaší organizace a provede kontrolu, kterou ověří, že jim vaše zařízení odpovídá. Tato kontrola může trvat několik minut.  

    ![Příklad snímku obrazovky aplikace Portál společnosti pro Windows, stránka Detaily zařízení, zvýrazněné tlačítko Zkontrolovat přístup](./media/1809_CheckAccess_Checking_Status.png) 

4. Podívejte se na aktualizaci stavu. Ukáže, že vaše zařízení **může přistupovat k prostředkům vaší organizace** nebo **nemůže přistupovat k prostředkům vaší organizace**.  

   ![Příklad snímku obrazovky aplikace Portál společnosti pro Windows, stránka Detaily zařízení, zvýrazněná část Stav](./media/1809_CheckAccess_Device_details_status1.png)  
   
5. Pokud vaše zařízení nemůže přistupovat k prostředkům, přejděte na upozornění v horní části stránky. Kliknutím na **Více** rozbalíte jeho podrobnosti. Kliknutím na **Méně** je sbalíte.  

    ![Příklad snímku obrazovky aplikace Portál společnosti pro Windows, stránka Detaily zařízení, zvýrazněné upozornění v horní části stránky](./media/1809_CheckAccess_Device_details_alert1.png)  

6. Tam, kde je to možné, zpráva zobrazuje odkazy na další pomoc a nápravné akce. Vyberte jednu nebo více z těchto možností a začněte s odstraňováním potíží. Akce řešení problémů, synchronizace a kontaktování &ndash;popsané níže&ndash; se zobrazují pouze při použití Portálu společnosti na ovlivněném zařízení.  

     * Odkaz **Jak to vyřešit** otevře relevantní článek nápovědy, pokud je k dispozici.  
     * Odkaz **Vyřešit** vás přesměruje na nastavení na vašem zařízení.  
     * Odkaz **Synchronizovat** vyhodnotí zařízení, aby se ověřilo, že odpovídá požadavkům vaší organizace.  
     * **Kontaktovat IT** vás přesměruje na kontaktní údaje vašeho IT týmu.   
 
6. Jakmile nastavení aktualizujete, klikněte na **Zkontrolovat přístup**, abyste potvrdili stav vašeho zařízení.  

    ![Příklad snímku obrazovky aplikace Portál společnosti pro Windows, stránka Detaily zařízení, zvýrazněná část Stav](./media/1809_CheckAccess_Device_details_status1.png)  

## <a name="check-access-from-device-context-menu"></a>Kontrola přístupu z místní nabídky zařízení  
1. Otevřete aplikaci Portál společnosti pro Windows a přejděte na **Moje zařízení**.  

    ![Příklad snímku obrazovky aplikace Portál společnosti pro Windows, domovská stránka, zvýrazněná část Moje zařízení](./media/1809_CheckAccess_Context_Select_Device.png)  

2. Klikněte pravým tlačítkem myši nebo stiskněte a podržte zařízení, aby se otevřela jeho [místní nabídka](https://docs.microsoft.com//windows/uwp/design/controls-and-patterns/menus).  

    ![Příklad snímku obrazovky s aplikací Portál společnosti pro Windows, domovská stránka Místní nabídka zařízení se zobrazuje na stránce v části Moje zařízení a zobrazuje akce Přejmenovat, Odebrat a Zkontrolovat přístup.](./media/1809_DeviceContextMenu_Windows_CP.png)  
3. Vyberte **Zkontrolovat přístup**. Aplikace synchronizuje vaše zařízení s aktuálními požadavky vaší organizace a provede kontrolu, kterou ověří, že jim vaše zařízení odpovídá. Tato kontrola může trvat několik minut.  
 
4. Pod zařízením se zobrazuje zpráva oznamující, že zařízení **může přistupovat k prostředkům společnosti** nebo **nemůže přistupovat k prostředkům společnosti**. 

    ![Příklad snímku obrazovky aplikace Portál společnosti pro Windows, stránka Detaily zařízení, zvýrazněná část Stav](./media/1809_CheckAccess_Context_Menu_Alert2.png) 

5. Pokud zařízení přistupovat k prostředkům nemůže, vyberte ho.  
6. Na stránce **Detaily zařízení** přejděte na oznámení v horní části stránky. Kliknutím na **Více** rozbalíte jeho podrobnosti. Kliknutím na **Méně** je sbalíte.  

    ![Příklad snímku obrazovky aplikace Portál společnosti pro Windows, stránka Detaily zařízení, zvýrazněné upozornění v horní části stránky](./media/1809_CheckAccess_Device_details_alert1.png)  

6. Tam, kde je to možné, zpráva zobrazuje odkazy na další pomoc a nápravné akce. Vyberte jednu nebo více z těchto možností a začněte s odstraňováním potíží. Akce řešení problémů, synchronizace a kontaktování &ndash;popsané níže&ndash; se zobrazují pouze při použití Portálu společnosti na ovlivněném zařízení.  

     * Odkaz **Jak to vyřešit** otevře relevantní článek nápovědy, pokud je k dispozici.  
     * Odkaz **Vyřešit** vás přesměruje na nastavení na vašem zařízení.  
     * Odkaz **Synchronizovat** vyhodnotí zařízení, aby se ověřilo, že odpovídá požadavkům vaší organizace.  
     * **Kontaktovat IT** vás přesměruje na kontaktní údaje vašeho IT týmu.    

7. Jakmile nastavení aktualizujete, klikněte na **Zkontrolovat přístup** v dolní části stránky.  

    ![Příklad snímku obrazovky aplikace Portál společnosti pro Windows, stránka Detaily zařízení, zvýrazněná akce Zkontrolovat přístup](./media/1809_CheckAccess_Device_details_button.png) 


Potřebujete další pomoc? Kontaktní informace na firemní podporu najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).
