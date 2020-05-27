---
title: Registrace zařízení se systémem iOS nebo iPadOS pomocí Portál společnosti Intune a Entrust Datacard
description: Registrace zařízení se systémem iOS nebo iPadOS a nastavení odvozeného ověřování přihlašovacích údajů pomocí Entrust Datacard.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilver
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: e24a03f3706256c1d18efb2eaebf520a4312edb1
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881531"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-entrust-datacard"></a>Nastavení zařízení se systémem iOS nebo iPadOS s Portál společnosti a Entrust Datacard

Zaregistrujte zařízení v aplikaci Portál společnosti Intune, abyste získali zabezpečený mobilní přístup k e-mailům, souborům a aplikacím vaší organizace. Po registraci zařízení se bude *Spravovat*. Vaše organizace může k zařízení přiřadit zásady a aplikace prostřednictvím poskytovatele správy mobilních zařízení (MDM), jako je třeba Intune.  

Během registrace nainstalujete také na svém zařízení odvozené přihlašovací údaje. Vaše organizace může vyžadovat použití odvozených přihlašovacích údajů jako metody ověřování při přístupu k prostředkům nebo pro podepisování a šifrování e-mailů. 

Je možné, že budete muset nastavit odvozené přihlašovací údaje, pokud použijete čipovou kartu k těmto akcím:  

* Přihlaste se do školních nebo pracovních aplikací, Wi-Fi a virtuálních privátních sítí (VPN).
* Podepisování a šifrování pracovních e-mailů pomocí certifikátů S/MIME  

V tomto článku provedete následující:  

   * Zaregistrujte mobilní zařízení se systémem iOS nebo iPadOS pomocí Portál společnosti Intune.  
   * Získejte odvozené přihlašovací údaje od zprostředkovatele odvozeného pověření vaší organizace [Entrust Datacard](https://www.entrustdatacard.com/).  

### <a name="what-are-derived-credentials"></a>Co jsou odvozené přihlašovací údaje?  
Odvozená pověření je certifikát, který je odvozený z vašich přihlašovacích údajů čipové karty a nainstalovaný na vašem zařízení. Poskytuje vzdálený přístup k pracovním prostředkům a zároveň brání neautorizovaným uživatelům v přístupu k citlivým informacím.  

Odvozené přihlašovací údaje se používají pro: 
* Ověřování studentů a zaměstnanců, kteří se přihlásí do školních nebo pracovních aplikací, Wi-Fi a VPN
* Podepisování a šifrování školních nebo pracovních e-mailů pomocí certifikátů S/MIME

Odvozené přihlašovací údaje jsou implementací pokynů National Institute of Standards and Technology (NIST) pro odvozená pověření PIV (Personal Identity Verification) jako součást speciální publikace (SP) 800-157.  

## <a name="prerequisites"></a>Požadavky

 K dokončení registrace musíte mít:

* Čipová karta, kterou poskytuje vaše škola nebo práce
* Přístup k počítači nebo veřejnému terminálu, kde se můžete přihlásit pomocí čipové karty
* Vaše mobilní zařízení
* V zařízení je nainstalovaná aplikace Portál společnosti Intune pro iOS a iPadOS.  


## <a name="enroll-device"></a>Registrace zařízení  
1. Na svém mobilním zařízení otevřete aplikaci Portál společnosti pro iOS/iPadOS a přihlaste se pomocí svého pracovního účtu.  

2. Zapište si kód na obrazovce.  

    ![Příklad obrázku Portál společnosti aplikace pomocí zprávy a kódu na obrazovce](./media/copy-code-intercede.png)   

3. Přepněte na zařízení s podporou čipové karty a přejděte na https://microsoft.com/devicelogin . 
4. Zadejte kód, který jste dříve zapsali.  

    ![Ukázkový snímek obrazovky Portál společnostiového webu "zadání kódu".](./media/enter-code-intercede.png)   

5. Vložte čipovou kartu, abyste se přihlásili.   
6. Vraťte se do aplikace Portál společnosti na svém mobilním zařízení a postupujte podle pokynů na obrazovce k registraci zařízení.  
7. Po dokončení registrace vás Portál společnosti upozorní, abyste si nastavili čipovou kartu. Klepněte na oznámení. Pokud se vám nezobrazí oznámení, podívejte se na e-mail.   

    ![Příklad snímku obrazovky Portál společnosti nabízeného oznámení na domovské obrazovce zařízení.](./media/action-required-in-app-intercede.png)  

8. Na obrazovce **nastavení mobilního přístupu čipové karty** :   
    a. Klepněte na odkaz na pokyny pro instalaci vaší organizace. Pokud vaše organizace neposkytuje další pokyny, pošleme vám tento článek.  
    b. Klepněte na **začít**.  

    ![Příklad obrazovky Portál společnosti nastavení obrazovky pro přístup přes mobilní čipovou kartu](./media/smart-card-info-intercede.png)

9. Přepněte na zařízení s podporou čipové karty a otevřete IdentityGuard. 
10. Vyhledejte oblast pro přihlášení inteligentních přihlašovacích údajů a vyberte tlačítko Přihlásit se.  
11. Až se zobrazí výzva k výběru certifikátu, vyberte přihlašovací údaje čipové karty. Pak vyberte **OK**. 
12. Zadejte PIN kód čipové karty.  
13. Zobrazí se výzva k výběru ze seznamu akcí. Vyberte ten, který vám umožní provést registraci pro odvozené mobilní inteligentní přihlašovací údaje. Odkaz nebo tlačítko může znamenat, že **se má zaregistrovat pro odvozené mobilní přihlašovací údaje čipové karty.**  
14. Vyberte, že jste úspěšně stáhli a nainstalovali aplikaci s podporou inteligentních přihlašovacích údajů. Pak pokračujte na další obrazovku.   
15. Zadejte informace o vašich odvozených pověřeních čipové karty.  
    a. Jako název identity zadejte libovolný název, jako je například *svěření odvozeného pověření*.  
    b. V rozevírací nabídce vyberte možnost **pověřit IdentityGudard mobilní inteligentní přihlašovací údaje**.  
    c. Pokračujte na další obrazovku. Pod ním se zobrazí kód QR s číselným heslem.  

16. Vraťte se do mobilního zařízení. Na obrazovce Portál společnosti > **získat kód QR** klepněte na **pokračovat**. 

    ![Příklad obrazovky Portál společnosti získání kódu QR](./media/get-qr-code-intercede.png)  
17. Klepněte na **použít fotoaparát**  >  **OK**.  

    ![Ukázkový snímek obrazovky Portál společnostiového řádku, který žádá o povolení přístupu ke kameře](./media/allow-cp-camera-access-intercede.png)  
18. Naskenujte obrázek kódu QR, který je na vašem zařízení s podporou čipové karty.  
19. Zadejte číselné heslo, které se zobrazí pod kódem QR.  

    ![Ukázkový snímek obrazovky Portál společnosti vyžadování hesla zadejte pole heslo.](./media/enter-password-derived-credentials.png)   

20. Počkejte, až se Portál společnosti dokončí nastavování vašeho zařízení.  


## <a name="next-steps"></a>Další kroky  
Po dokončení registrace budete mít přístup k pracovním prostředkům, například k e-mailu, Wi-Fi a všem aplikacím, které vaše organizace zpřístupňuje. Další informace o tom, jak získat, vyhledat, nainstalovat a odinstalovat aplikace, najdete v Portál společnosti:

* [Správa aplikací z Portál společnosti webu](manage-apps-cpweb.md)  
* [Použití spravovaných aplikací na zařízení](use-managed-apps-on-your-device-ios.md)  

Potřebujete ještě další pomoc? Obraťte se na podporu ve vaší společnosti. Kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).  
