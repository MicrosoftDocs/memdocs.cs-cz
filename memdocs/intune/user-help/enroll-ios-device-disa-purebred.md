---
title: Registrace zařízení se systémem iOS nebo iPadOS pomocí Portál společnosti Intune a DISA purebred
description: Naučte se registrovat zařízení se systémem iOS nebo iPadOS a nastavit odvozené ověřování přihlašovacích údajů s DISA purebred.
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
ms.openlocfilehash: 50330bbdc61eeeada022c44f4d1f2f68b31f19a4
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881555"
---
# <a name="set-up-ios-or-ipados-device-with-company-portal-and-disa-purebred"></a>Nastavení zařízení se systémem iOS nebo iPadOS pomocí Portál společnosti a DISA purebred  

Zaregistrujte zařízení v aplikaci Portál společnosti Intune, abyste získali zabezpečený mobilní přístup k e-mailům, souborům a aplikacím vaší organizace. Po registraci zařízení se bude *Spravovat*. Vaše organizace může k zařízení přiřadit zásady a aplikace prostřednictvím poskytovatele správy mobilních zařízení (MDM), jako je třeba Intune.  

Během registrace nainstalujete také na svém zařízení odvozené přihlašovací údaje. Vaše organizace může vyžadovat použití odvozených přihlašovacích údajů jako metody ověřování při přístupu k prostředkům nebo pro podepisování a šifrování e-mailů. 

Je možné, že budete muset nastavit odvozené přihlašovací údaje, pokud použijete čipovou kartu k těmto akcím:

* Přihlaste se do školních nebo pracovních aplikací, Wi-Fi a virtuálních privátních sítí (VPN).
* Podepisování a šifrování pracovních e-mailů pomocí certifikátů S/MIME  

V tomto článku provedete následující:  

   * Zaregistrujte mobilní zařízení se systémem iOS nebo iPadOS pomocí Portál společnosti Intune.  
   * Získejte odvozené přihlašovací údaje od poskytovatele odvozeného pověření vaší organizace, DISA purebred: https: \/ /Cyber.mil/PKI-PKE/purebred/.  

## <a name="what-are-derived-credentials"></a>Co jsou odvozené přihlašovací údaje?  
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

Při instalaci bude také potřeba kontaktovat agenta purebred nebo zástupce.      

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
    a. Klepněte na odkaz na pokyny pro nastavení vaší organizace. Pokud vaše organizace neposkytuje další pokyny, pošleme vám tento článek.  
    b. Kliknutím na **otevřít** otevřete aplikaci purebred.  

    ![Příklad obrazovky Portál společnosti nastavení obrazovky pro přístup přes mobilní čipovou kartu](./media/smart-card-open-disa-purebred.png)  
9. Až se zobrazí výzva, aby Portál společnosti otevřela aplikaci pro registraci purebred, vyberte **otevřít**.   

    ![Ukázkový snímek obrazovky Portál společnosti výzvy k otevření aplikace purebred v DISA](./media/open-app-prompt-disa-purbred.png)  
10. Když aplikace funguje, spolupracujte s agentem purebred vaší organizace a nakonfigurujte a Stáhněte si konfigurační profil pro předběžné registrace purebred.   
11. V části nastavení aplikace > **Obecné**  >  **profily &**  >  **instalovat profil** zařízení a klepněte na **instalovat**.  
12. Zadejte heslo zařízení.  
13. Nainstalujte profil. Pro spuštění instalace možná budete muset klepnout na **nainstalovat** více než jednou. 
14. Vraťte se do registrační aplikace purebred. Pokračujte podle pokynů agenta purebred.  
 
15. Až stáhnete konfigurační profil, v části nastavení aplikace > **Obecné**  >  **profily &**  >  **instalovat profil** zařízení a klepněte na **instalovat**.   
16.  Zadejte heslo zařízení.
17. Nainstalujte profil. Pro spuštění instalace možná budete muset klepnout na **nainstalovat** více než jednou. 
18. Po dokončení instalace se vraťte do aplikace Portál společnosti.  
19.  Na obrazovce **nastavení mobilního přístupu k čipové kartě** klepněte na **pokračovat**.  

20. Na obrazovce **Import certifikátů** načtěte a importujte odvozené přihlašovací údaje, které jste získali z DISA purebred.  

    a. Klepněte na **pokračovat**.   

    ![Ukázkový snímek obrazovky Portál společnosti nastavit import certifikátů](./media/import-certificate-disa-purebred.png)  
    b. Přejděte na umístění pro **procházení**jednotky iCloud  >  **Locations** a klepněte na **Další umístění**.  

    ![Příklad obrazovky iCloud Drive, procházení nabídky Procházet Další místa možnost.](./media/icloud-drive-more-locations.png)  
    c. Klepněte na přepínač a povolte tak **řetěz purebred klíčů**.  

    ![Ukázkový snímek obrazovky iCloud Drive, zobrazení procházení a zvýraznění, že je povolený přepínač řetězení klíčů purebred](./media/icloud-drive-enable-purebred-keychain.png)   

    d. Klepněte na **balíček přihlašovacích údajů purebred**.  

    ![Ukázkový snímek obrazovky s iOS s možností balíčku s volitelným přihlašovacími údaji purebred](./media/purebred-credential-package.png)  
    f. Zobrazí se seznam certifikátů. Vyberte jednu a potom klepněte na **Importovat klíč**.  

    ![Příklad snímku obrazovky seznamu volitelných certifikátů, u kterých je už vybraný.](./media/import-purebred-keychain.png) 
21. Vraťte se do aplikace Portál společnosti a počkejte, až se Portál společnosti dokončí nastavování vašeho zařízení.   

## <a name="next-steps"></a>Další kroky  
Po dokončení registrace budete mít přístup k pracovním prostředkům, například k e-mailu, Wi-Fi a všem aplikacím, které vaše organizace zpřístupňuje. Další informace o tom, jak získat, vyhledat, nainstalovat a odinstalovat aplikace, najdete v Portál společnosti:

* [Správa aplikací z Portál společnosti webu](manage-apps-cpweb.md)  
* [Použití spravovaných aplikací na zařízení](use-managed-apps-on-your-device-ios.md)  

Potřebujete ještě další pomoc? Obraťte se na podporu ve vaší společnosti. Kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).
