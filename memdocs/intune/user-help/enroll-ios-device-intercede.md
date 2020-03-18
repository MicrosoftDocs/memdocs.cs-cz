---
title: Registrace zařízení se systémem iOS nebo iPadOS pomocí Portál společnosti Intune a Intercede
description: Naučte se registrovat zařízení se systémem iOS nebo iPadOS a nastavit odvozené ověřování přihlašovacích údajů pomocí Intercede.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilver
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 1bd216049c5dbda7c044949f9fa39c3b7bd56f9d
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79324755"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-intercede"></a>Nastavení zařízení se systémem iOS nebo iPadOS s využitím Portál společnosti a Intercede

Zaregistrujte zařízení v aplikaci Portál společnosti Intune, abyste získali zabezpečený mobilní přístup k e-mailům, souborům a aplikacím vaší organizace.  Po registraci zařízení se bude *Spravovat*. Vaše organizace může k zařízení přiřadit zásady a aplikace prostřednictvím poskytovatele správy mobilních zařízení (MDM), jako je třeba Intune.  

Během registrace nainstalujete také na svém zařízení odvozené přihlašovací údaje. Vaše organizace může vyžadovat použití odvozených přihlašovacích údajů jako metody ověřování při přístupu k prostředkům nebo pro podepisování a šifrování e-mailů. 

Je možné, že budete muset nastavit odvozené přihlašovací údaje, pokud použijete čipovou kartu k těmto akcím:

* Přihlaste se do školních nebo pracovních aplikací, Wi-Fi a virtuálních privátních sítí (VPN).
* Podepisování a šifrování pracovních e-mailů pomocí certifikátů S/MIME  

V tomto článku budete:  

* Zaregistrujte mobilní zařízení se systémem iOS nebo iPadOS pomocí Portál společnosti Intune.  
* Získejte odvozené přihlašovací údaje od poskytovatele odvozeného pověření vaší organizace, [Intercede](https://www.intercede.com/).   


## <a name="what-are-derived-credentials"></a>Co jsou odvozené přihlašovací údaje?  
Odvozená pověření je certifikát, který je odvozený z vašich přihlašovacích údajů čipové karty a nainstalovaný na vašem zařízení. Poskytuje vzdálený přístup k pracovním prostředkům a zároveň brání neautorizovaným uživatelům v přístupu k citlivým informacím.  

Odvozené přihlašovací údaje se používají pro: 
* Ověřování studentů a zaměstnanců, kteří se přihlásí do školních nebo pracovních aplikací, Wi-Fi a VPN
* Podepisování a šifrování školních nebo pracovních e-mailů pomocí certifikátů S/MIME  

Odvozené přihlašovací údaje jsou implementací pokynů National Institute of Standards and Technology (NIST) pro odvozená pověření PIV (Personal Identity Verification) jako součást speciální publikace (SP) 800-157.  

## <a name="prerequisites"></a>Požadavky

 K dokončení registrace musíte mít:

* Čipová karta, kterou poskytuje vaše škola nebo práce
* Přístup k počítači nebo terminálu samoobslužné služby, kde se můžete přihlásit pomocí čipové karty
* Vaše mobilní zařízení
* V zařízení je nainstalovaná aplikace Portál společnosti Intune pro iOS a iPadOS.


## <a name="enroll-device"></a>Registrace zařízení  
1. Na svém mobilním zařízení otevřete aplikaci Portál společnosti pro iOS/iPadOS a přihlaste se pomocí svého pracovního účtu.  
2. Zapište kód, který se zobrazí na obrazovce.  

    ![Příklad obrázku Portál společnosti aplikace pomocí zprávy a kódu na obrazovce](./media/copy-code-intercede.png)  
1. Přepněte na zařízení s podporou čipové karty a přejděte na https://microsoft.com/devicelogin. 

1. Zadejte kód, který jste dříve zapsali.
 
2. Vložte čipovou kartu, abyste se přihlásili.   

3. Vraťte se do aplikace Portál společnosti na svém mobilním zařízení a postupujte podle pokynů na obrazovce k registraci zařízení.  
4. Po dokončení registrace vás Portál společnosti upozorní, abyste si nastavili čipovou kartu. Klepněte na oznámení. Pokud se vám nezobrazí oznámení, podívejte se na e-mail.   

    ![Příklad snímku obrazovky Portál společnosti nabízeného oznámení na domovské obrazovce zařízení.](./media/action-required-in-app-intercede.png)  

5. Na obrazovce **nastavení mobilního přístupu čipové karty** :  
    a. Klepněte na odkaz na pokyny pro instalaci vaší organizace. Pokud vaše organizace neposkytuje další pokyny, pošleme vám tento článek.  
    b. Klepněte na **začít**.  

    ![Příklad obrazovky Portál společnosti nastavení obrazovky pro přístup přes mobilní čipovou kartu](./media/smart-card-info-intercede.png)  

6. Přepněte na zařízení s podporou čipových karet nebo samoobslužný terminál a otevřete aplikaci MyID. Přihlaste se pomocí svých pracovních přihlašovacích údajů.  
7. Vyberte možnost pro vyžádání vašeho ID. 
8. Po zobrazení dotazu, který profil chcete použít, vyberte možnost aktivace pomocí mobilního přihlašovacího údaje. Zobrazí se kód QR.  
9. Vraťte se do mobilního zařízení. Na obrazovce Portál společnosti > **získat kód QR** klepněte na **pokračovat**.  

    ![Příklad obrazovky Portál společnosti získání kódu QR](./media/get-qr-code-intercede.png) 
 
10. Klepněte na **použít fotoaparát** > **OK**.  

    ![Ukázkový snímek obrazovky Portál společnostiového řádku, který žádá o povolení přístupu ke kameře](./media/allow-cp-camera-access-intercede.png)  

11. Naskenujte obrázek kódu QR, který je na vašem zařízení s podporou čipové karty. 
12. Počkejte, až se Portál společnosti dokončí nastavování vašeho zařízení.  

## <a name="next-steps"></a>Další kroky  
Po dokončení registrace budete mít přístup k pracovním prostředkům, například k e-mailu, Wi-Fi a všem aplikacím, které vaše organizace zpřístupňuje. Další informace o tom, jak získat, vyhledat, nainstalovat a odinstalovat aplikace, najdete v Portál společnosti:

* [Správa aplikací z Portál společnosti webu](manage-apps-cpweb.md)  
* [Použití spravovaných aplikací na zařízení](use-managed-apps-on-your-device-ios.md)  

Potřebujete ještě další pomoc? Obraťte se na podporu ve vaší společnosti. Kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).
