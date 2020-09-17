---
title: Řešení potíží s přístupem k zařízení s Windows 10 do školy nebo práce | Microsoft Intune
description: Vyřešte problémy s přístupem nebo připojením k účtu pro zaregistrovaná zařízení s Windows 10.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/09/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 4ab630b6-47ff-443b-a2a5-be23388bcea7
searchScope:
- User help
ROBOTS: ''
ms.reviewer: amanh
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 268ef3b9931c86a73ccf4e681240e4d2333c8026
ms.sourcegitcommit: 2339c927b6576db8878f34f167a9a45c5dc9f58d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/16/2020
ms.locfileid: "90689391"
---
# <a name="troubleshoot-windows-10-device-access"></a>Řešení potíží s přístupem k zařízení s Windows 10
Tento článek popisuje, jak vyřešit problémy s přístupem k zaregistrovanému zařízení s Windows 10. 

## <a name="check-wi-fi-connection"></a>Ověřit připojení Wi-Fi  

Pro přístup k pracovním nebo školním prostředkům se vyžaduje připojení k síti Wi-Fi. Ověřte, zda jste připojeni k síti Wi-Fi, a pak se pokuste o přístup k prostředkům znovu.  

## <a name="add-work-or-school-account-in-settings-app"></a>Přidat pracovní nebo školní účet v aplikaci nastavení  
Tyto kroky můžete použít k registraci zařízení. Pokud se ale váš účet v aplikaci **Nastavení** nezobrazuje, mnoho toho je potřeba provést znovu.  

1. Otevřete aplikaci **Nastavení**. 
2. Vyberte **Účty**.
3. Tento další krok se liší v závislosti na verzi Windows 10, kterou používáte. 
    * Verze 1607 a novější: vyberte **přístup do práce nebo do školy**.
    * Verze 1511 a starší: vyberte **přístup do práce**.  
4. Ověřte svůj účet. Pokud není v seznamu uveden, přidejte ho kliknutím na tlačítko pro **připojení** a zápis. 
5. Přihlaste se pomocí přihlašovacích údajů svého pracovního nebo školního účtu. 
6. Postupujte podle výzev na obrazovce a dokončete připojení.  
7. Po dokončení se Váš účet přidá jako připojení. Budete mít přístup k prostředkům, které vaše organizace zpřístupňuje.   

## <a name="contact-it-support-for-access-requirements"></a>Kontaktovat IT podporu pro požadavky na přístup  
Pokud vidíte svůj pracovní nebo školní účet uvedený v aplikaci nastavení, vaše zařízení a účet už jsou připojené. Další pomoc s problémy s přístupem vám poskytne pracovník podpory IT. Můžou mít omezení nebo požadavky, které znemožňují přístup k určitým prostředkům.  

## <a name="error-messages"></a>Chybové zprávy  

### <a name="we-couldnt-auto-discover-a-management-endpoint-matching-the-username-entered-please-check-your-username-and-try-again-if-you-know-the-url-to-your-management-endpoint-please-enter-it"></a>Nepovedlo se nám automaticky zjistit koncový bod správy, který odpovídá zadanému uživatelskému jménu. Zkontrolujte prosím své uživatelské jméno a zkuste to znovu. Pokud znáte adresu URL koncového bodu správy, zadejte ji prosím.

**Příčina**: váš účet nešlo ověřit vedle zadané adresy URL (označuje se taky jako koncový bod pro správu).  

#### <a name="resolution"></a>Řešení
1. Zadejte své uživatelské jméno a heslo znovu. 
2. Pokud to pořád nefunguje, obraťte se na pracovníky podpory IT, aby získal správnou adresu URL (například: <code>www.yourcompany.onmicrosoft.com</code> ). 
3. Po zobrazení výzvy zadejte zadanou adresu URL. 

### <a name="it-looks-like-youre-not-connected-make-sure-youre-connected-to-the-network"></a>Vypadá to, že nejste připojení. Ujistěte se, že jste připojení k síti.

**Příčina**: zařízení není připojené k Wi-Fi a připojení k pracovnímu nebo školnímu účtu se vyžaduje.     

#### <a name="resolution"></a>Řešení
1. Na panelu nástrojů nebo nastavení zařízení vyberte ikonu zeměkoule **stav sítě** .
2. Vyberte síť Wi-Fi > **připojit**.  
3. Zkuste svůj účet znovu připojit.  


## <a name="next-steps"></a>Další kroky  

Potřebujete ještě další pomoc? Obraťte se na pracovníky podpory IT. Kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).
