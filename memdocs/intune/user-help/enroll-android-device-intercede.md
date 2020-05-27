---
title: Registrace zařízení s Androidem pomocí Portál společnosti Intune a Intercede
description: Registrace zařízení s Androidem a nastavení odvozeného ověřování přihlašovacích údajů pomocí Intercede.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/17/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: jeyang
ms.suite: ems
ms.custom: intune-enduser
ms.collection: M365-identity-device-management
ms.openlocfilehash: e82d8f27b7ffbce663ee64030a6d933bf1684dc1
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83880607"
---
# <a name="set-up-android-device-with-company-portal-and-intercede"></a>Nastavení zařízení s Androidem pomocí Portál společnosti a Intercede

Zaregistrujte zařízení v aplikaci Portál společnosti Intune, abyste získali zabezpečený mobilní přístup k e-mailům, souborům a aplikacím vaší organizace. Po registraci zařízení se bude *Spravovat*. Vaše organizace může k zařízení přiřadit zásady a aplikace prostřednictvím poskytovatele správy mobilních zařízení (MDM), jako je třeba Intune.

Během registrace nainstalujete také na svém zařízení odvozené přihlašovací údaje. Vaše organizace může vyžadovat použití odvozených přihlašovacích údajů jako metody ověřování při přístupu k prostředkům nebo pro podepisování a šifrování e-mailů.

Je možné, že budete muset nastavit odvozené přihlašovací údaje, pokud použijete čipovou kartu k těmto akcím:

* Přihlaste se do školních nebo pracovních aplikací, Wi-Fi a virtuálních privátních sítí (VPN).
* Podepisování a šifrování pracovních e-mailů pomocí certifikátů S/MIME

V tomto článku provedete následující:

* Zaregistrujte mobilní zařízení s Androidem pomocí Portál společnosti Intune.
* Nastavte čipovou kartu tím, že nainstalujete odvozené přihlašovací údaje od poskytovatele odvozeného pověření vaší organizace, [Intercede](https://www.intercede.com/).  

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
* Nové zařízení nebo zařízení pro obnovení továrního nastavení se systémem Android 7,0 nebo novějším
* Aplikace Microsoft Intune nainstalovaná na vašem zařízení

## <a name="enroll-device"></a>Registrace zařízení  

1. Zapněte nové zařízení nebo zařízení pro obnovení do továrního nastavení.  
2. Na **uvítací** obrazovce vyberte svůj jazyk. Pokud jste dostali pokyn k registraci pomocí kódu QR nebo NFC, postupujte podle níže uvedeného kroku, který odpovídá metodě.  
     * NFC: klepněte na zařízení, které podporuje NFC, na programátorské zařízení se připojte k síti vaší organizace. Postupujte podle pokynů na obrazovce. Až se dostanete na obrazovku s podmínkami služby Chrome, pokračujte krokem 5.  

     * QR kód: dokončení kroků v [zápisu kódu QR](#qr-code-enrollment).  

     Pokud jste se dostali k používání jiné metody, pokračujte krokem 3.    

3. Připojte se k Wi-Fi a klepněte na **Další**. Použijte krok, který odpovídá metodě registrace. 

    * Token: když se dostanete na přihlašovací obrazovku Google, proveďte kroky v části [registrace tokenu](#token-enrollment).  
    * Google Zero Touch: po připojení k Wi-Fi bude vaše zařízení rozpoznatelné vaší organizací. Pokračujte krokem 4 a postupujte podle pokynů na obrazovce, dokud nebude instalace dokončena.    
 
       ![Příklad obrázku obrazovky s podmínkami pro Google, který vidíte, pokud používáte Google Zero Touch, zvýrazňování tlačítka přijmout & pokračovat.](./media/google-zero-touch-intune-app-01.png)   
   
4. Zkontrolujte výrazy Google. Pak klepněte na **přijmout & pokračovat**.  

      ![Příklad obrázku obrazovky podmínek Google, zvýrazňování tlačítka přijmout & pokračování](./media/fully-managed-intune-app-04.png)   

5. Kontrola podmínek služby v Chrome. Pak klepněte na **přijmout & pokračovat**.  

   ![Příklad obrázku obrazovky s podmínkami služby Chrome, zvýraznění tlačítko přijmout & pokračovat](./media/fully-managed-intune-app-06.png)  

6. Na přihlašovací obrazovce klepněte na **možnost přihlašovací možnosti** a pak **se přihlaste z jiného zařízení**. 

7. Zapište si kód na obrazovce.  

8. Přepněte na zařízení s podporou čipové karty a přejděte na webovou adresu, která se zobrazí na obrazovce. 

9. Zadejte kód, který jste dříve zapsali.

   > [!div class="mx-imgBorder"]
   > ![Snímek obrazovky s výzvou Portál společnostiového webu "zadat kód"](./media/enter-code-intercede.png)

10. Vložte čipovou kartu, abyste se přihlásili.  

11. Na přihlašovací obrazovce vyberte svůj pracovní nebo školní účet. Pak přejděte zpátky na mobilní zařízení.

12. V závislosti na požadavcích vaší organizace se může zobrazit výzva k aktualizaci nastavení, jako je třeba zámek nebo šifrování obrazovky. Pokud se zobrazí tyto výzvy, klepněte na **nastavit** a postupujte podle pokynů na obrazovce.  

       ![Příklad obrázku nastavení obrazovky pro práci s telefonem, tlačítko zvýraznění sady](./media/fully-managed-intune-app-10.png)   

13. Pokud chcete na zařízení nainstalovat pracovní aplikace, klepněte na **nainstalovat**. Po dokončení instalace klepněte na **Další**.  

       ![Příklad obrázku nastavení obrazovky pro práci s telefonem, zvýraznění tlačítka pro instalaci](./media/fully-managed-intune-app-11.png)    

14. Klepnutím na **Start** otevřete aplikaci Microsoft Intune. 

    ![Příklad obrázku nastavení obrazovky pro práci s telefonem, zvýraznění tlačítka Start](./media/fully-managed-intune-app-17.png)   
 

15. Vraťte se do aplikace Intune na vašem mobilním zařízení a postupujte podle pokynů na obrazovce, dokud se registrace nedokončila. 

    ![Příklad obrázku nastavení přístupu, registrace obrazovky zařízení, zvýraznění tlačítka Hotovo.](./media/fully-managed-intune-app-19.png)   

16. Pokračujte v části [Nastavení čipové karty](enroll-android-device-intercede.md#set-up-smart-card) v tomto článku a dokončete nastavení zařízení.  

### <a name="qr-code-enrollment"></a>Zápis kódu QR  
V této části provedete kontrolu kódu QR poskytovaného vaší společností.  Až budete hotovi, přesměrujeme vás zpátky na kroky registrace zařízení.     
  
1. Na **úvodní** obrazovce klepněte pětkrát na obrazovku a spusťte nastavení kódu QR.  

   ![Příklad obrázku úvodní obrazovky instalace zařízení, zvýraznění pokynů pro klepnutí na obrazovku](./media/qr-code-intune-app-01.png)  

2. Připojte se k Wi-Fi podle pokynů na obrazovce.  
3. Pokud zařízení nemá skener kódu QR, obrazovky instalačního programu zobrazí průběh instalace skeneru. Počkejte na dokončení instalace.  
4. Po zobrazení výzvy Naskenujte kód QR v registračním profilu, který vám vaše organizace poskytla.  
5. Vraťte se k [registraci zařízení](#enroll-device), krok 4 pro pokračování v instalaci.  

### <a name="token-enrollment"></a>Zápis tokenu  
V této části zadáte svůj token poskytovaný společností. Až budete hotovi, přesměrujeme vás zpátky na kroky registrace zařízení.  

1. Do přihlašovací obrazovky Google v poli **e-mail nebo telefon** zadejte **AFW # Setup**. Pak klepněte na **Další**. 

   ![Příklad obrázku přihlašovací obrazovky Google, který ukazuje, že se do pole zadává nastavení "AFW #".](./media/token-intune-app-01.png)   

2. Vyberte **nainstalovat** pro aplikaci **zásad zařízení s Androidem** . Pokračujte v instalaci. V závislosti na vašem zařízení možná budete muset zkontrolovat a přijmout další podmínky.    

3. Na obrazovce **zaregistrovat toto zařízení** vyberte **Další**.  

4. Vyberte **zadat kód**.  

5. Na obrazovce **Kontrola nebo zadání kódu** zadejte kód, který vám vaše organizace poskytla.  Pak klikněte na **Další**.  

   ![Příklad obrázku skenování nebo zadání kódu obrazovky, zvýraznění tlačítka Další](./media/token-intune-app-04.png)  

6. Vraťte se k [registraci zařízení](#enroll-device), krok 4 pro pokračování v instalaci.

## <a name="set-up-smart-card"></a>Nastavení čipové karty  

1. Po dokončení registrace vám aplikace Intune upozorní, abyste si nastavili čipovou kartu. Klepněte na oznámení. Pokud se vám nezobrazí oznámení, podívejte se na e-mail.

   > [!div class="mx-imgBorder"]
   > ![Příklad snímku obrazovky Portál společnosti nabízeného oznámení na domovské obrazovce zařízení.](./media/action-required-in-app-android.png)

2. Na obrazovce **nastavit čipovou kartu** :

   1. Klepněte na odkaz na pokyny pro instalaci vaší organizace. Pokud vaše organizace neposkytuje další pokyny, pošleme vám tento článek.

   2. Klepněte na **začít**.  

   > [!div class="mx-imgBorder"]
   > ![Příklad obrazovky Portál společnosti nastavení obrazovky pro přístup přes mobilní čipovou kartu](./media/smart-card-open-entrust-android.png)

3. Přepněte na zařízení s podporou čipových karet nebo samoobslužný terminál a otevřete aplikaci MyID. Přihlaste se pomocí svých pracovních přihlašovacích údajů.

4. Vyberte možnost pro vyžádání vašeho ID.

5. Po zobrazení dotazu, který profil chcete použít, vyberte možnost aktivace pomocí mobilního přihlašovacího údaje. Zobrazí se kód QR.  

6. Vraťte se na zařízení s Androidem. Na obrazovce Portál společnosti > **získat kód QR** klepněte na **Další**.

    > [!div class="mx-imgBorder"]
    > ![Příklad obrazovky Portál společnosti získání kódu QR](./media/get-qr-code-entrust-android.png)

7. Pokud se zobrazí výzva, abyste aplikaci Intune povolili používání kamery, klepněte na možnost **Povolení**.

8. Naskenujte obrázek kódu QR, který je na vašem zařízení s podporou čipové karty.

9. Aplikace Intune začne stahovat a instalovat certifikáty potřebné pro přístup k pracovním nebo školním prostředkům. V závislosti na připojení k Internetu může tento proces nějakou dobu trvat. Aplikaci během této doby nezavírejte.

    > [!div class="mx-imgBorder"]
    > ![Příklad obrazovky Portál společnosti "stažení a instalace certifikátů"](./media/install-certificates-entrust-android.png)

10. Po zpracování všech certifikátů počkejte, než aplikace Intune dokončí nastavování vašeho zařízení. Po zobrazení **sady, kterou jste nastavili** , budete mít jistotu, že se instalace dokončí! aplikací.

    > [!div class="mx-imgBorder"]
    > ![Ukázkový snímek obrazovky se všemi nastaveními](./media/all-set-android.png)

## <a name="next-steps"></a>Další kroky

Po dokončení registrace budete mít přístup k pracovním prostředkům, například k e-mailu, Wi-Fi a všem aplikacím, které vaše organizace zpřístupňuje. Další informace o tom, jak získat, vyhledat, nainstalovat a odinstalovat aplikace v Intune, najdete v těchto tématech:

* [Použití spravovaných aplikací na zařízení](use-managed-apps-on-your-device-android.md)  
* [Správa aplikací z Portál společnosti webu](manage-apps-cpweb.md)  

Potřebujete ještě další pomoc? Obraťte se na podporu ve vaší společnosti. Kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).
