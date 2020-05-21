---
title: Registrace zařízení s Androidem pomocí Microsoft Intune App a DISA purebred
description: Přečtěte si, jak zaregistrovat zařízení s Androidem a jak nastavit odvozené ověřování přihlašovacích údajů pomocí DISA purebred.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/15/2020
ms.topic: article
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
ms.openlocfilehash: 9f92a23b117582ef40d236fe257917018431128e
ms.sourcegitcommit: 6ca5e75ed7a6fd2186fbe51c177960004d5ec81f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/19/2020
ms.locfileid: "83633394"
---
# <a name="set-up-android-device-with-the-microsoft-intune-app-and-disa-purebred"></a>Nastavení zařízení s Androidem pomocí aplikace Microsoft Intune a DISA purebred

Zaregistrujte zařízení v aplikaci Microsoft Intune, abyste získali zabezpečený mobilní přístup k e-mailům, souborům a aplikacím vaší organizace. Po registraci zařízení se bude *Spravovat*. Vaše organizace může k zařízení přiřadit zásady a aplikace prostřednictvím poskytovatele správy mobilních zařízení (MDM), jako je třeba Intune.  

Během registrace nainstalujete také na svém zařízení odvozené přihlašovací údaje. Vaše organizace může vyžadovat použití odvozených přihlašovacích údajů jako metody ověřování při přístupu k prostředkům nebo pro podepisování a šifrování e-mailů.

Je možné, že budete muset nastavit odvozené přihlašovací údaje, pokud použijete čipovou kartu k těmto akcím:

* Přihlaste se do školních nebo pracovních aplikací, Wi-Fi a virtuálních privátních sítí (VPN).
* Podepisování a šifrování pracovních e-mailů pomocí certifikátů S/MIME

V tomto článku provedete následující:

* Registrace mobilního zařízení se systémem Android pomocí aplikace Intune
* Nastavte čipovou kartu tím, že nainstalujete odvozené přihlašovací údaje od poskytovatele odvozeného pověření vaší organizace, [DISA purebred](https://public.cyber.mil/pki-pke/purebred/)

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
* Aplikace purebred nainstalovaná na vašem zařízení (aplikace by se měla po instalaci zařízení automaticky nainstalovat. Pokud tomu tak není, obraťte se na pracovníky podpory IT.)

Při instalaci bude také potřeba kontaktovat agenta purebred nebo zástupce.

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

16. Pokračujte v části [Nastavení čipové karty](enroll-android-device-disa-purebred.md#set-up-smart-card) v tomto článku a dokončete nastavení zařízení.  

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

1. Do přihlašovací obrazovky Google v poli **e-mail nebo telefon** zadejte **AFW # Setup**. Klepněte na **Další**. 

   ![Příklad obrázku přihlašovací obrazovky Google, který ukazuje, že se do pole zadává nastavení "AFW #".](./media/token-intune-app-01.png)   

2. Vyberte **nainstalovat** pro aplikaci **zásad zařízení s Androidem** . Pokračujte v instalaci. V závislosti na vašem zařízení možná budete muset zkontrolovat a přijmout další podmínky.    

3. Na obrazovce **zaregistrovat toto zařízení** vyberte **Další**.  

4. Vyberte **zadat kód**.  

5. Na obrazovce **Kontrola nebo zadání kódu** zadejte kód, který vám vaše organizace poskytla.  Pak klikněte na **Další**.  

   ![Příklad obrázku skenování nebo zadání kódu obrazovky, zvýraznění tlačítka Další](./media/token-intune-app-04.png)  

6. Vraťte se k [registraci zařízení](#enroll-device), krok 4 pro pokračování v instalaci.


## <a name="set-up-smart-card"></a>Nastavení čipové karty  

> [!NOTE]
> K provedení těchto kroků se vyžaduje aplikace purebred, která se po registraci automaticky nainstaluje do vašeho zařízení. Pokud ještě nemáte aplikaci ani po krátké době čekání, obraťte se na pracovníky podpory IT.  

1. Po dokončení registrace vám aplikace Intune upozorní, abyste si nastavili čipovou kartu. Klepněte na oznámení. Pokud se vám nezobrazí oznámení, podívejte se na e-mail.

   > [!div class="mx-imgBorder"]
   > ![Snímek obrazovky s nabízeným oznámením aplikace Intune na domovské obrazovce zařízení](./media/action-required-in-app-android.png)

2. Na obrazovce **nastavit čipovou kartu** :

   1. Klepněte na odkaz a Projděte si pokyny pro instalaci vaší organizace. Pokud vaše organizace neposkytuje další pokyny, pošleme vám tento článek.

   2. Klepněte na **začít**.   

   > [!div class="mx-imgBorder"]
   > ![Snímek obrazovky aplikace Intune, nastavení obrazovky čipové karty](./media/smart-card-open-disa-purebred-android.png)

3. Na obrazovce **získat certifikáty** klepněte na **Spustit PUREBRED** a otevřete aplikaci PUREBRED. (Aplikace by měla být na vašem zařízení automaticky nainstalovaná. Pokud ho nemáte, obraťte se na pracovníky podpory.)  

   > [!div class="mx-imgBorder"]
   > ![Snímek obrazovky s výzvou aplikace Intune pro otevření aplikace DISA purebred](./media/open-app-prompt-disa-purbred-android.png)  

4. Aby mohla aplikace purebred správně fungovat, může k tomu potřebovat další oprávnění. Po zobrazení výzvy klepněte na možnost **Povolení** nebo **povolení všech časů** . Pokud chcete získat další informace o tom, proč se tato oprávnění vyžadují, Mluvte s pracovníkem podpory nebo s agentem purebred.  

5. Až budete v aplikaci purebred, můžete pracovat s agentem purebred vaší organizace a stáhnout a nainstalovat certifikáty, které potřebujete pro přístup k pracovním nebo školním prostředkům.

    > [!IMPORTANT]
    > Během tohoto procesu klepněte na tlačítko **OK** nebo **nainstalovat** po zobrazení výzvy. Neměňte názvy certifikačních autorit (CA) ani certifikátů, které jste vyzváni k instalaci.    

6. Po dokončení instalace obdržíte oznámení, že vaše certifikáty jsou připravené. Klepnutím na oznámení se vraťte do aplikace Intune.

    > [!div class="mx-imgBorder"]
    > ![Snímek obrazovky "povolení přístupu k certifikátům"](./media/certificates-ready-prompt-disa-purbred-android.png)

7. Na obrazovce **Povolit přístup k certifikátům** udělíte aplikaci Intune oprávnění pro přístup k odvozeným přihlašovacím údajům, které jste získali z DISA purebred. Tento krok zajistí, že vaše organizace může ověřit vaši identitu, kdykoli budete mít přístup k chráněným pracovním nebo školním prostředkům.  

    1. Klepněte na **Další**.

       > [!div class="mx-imgBorder"]
       > ![Snímek obrazovky s výzvou k zadání certifikátů je připraven](./media/certificates-access-disa-purbred-android.png)

    2. Po zobrazení výzvy k výběru **certifikátu**neměňte výběr. Už je vybraný správný certifikát, stačí jenom klepnout na **Vybrat** nebo **OK**.  

       > [!div class="mx-imgBorder"]
       > ![Snímek obrazovky s výzvou "zvolit certifikát"](./media/choose-certificates-prompt-disa-purbred-android.png)

    3. Vaše odvozené přihlašovací údaje se skládají z více certifikátů, takže se může zobrazit výzva k **výběru certifikátu** několikrát. Opakujte předchozí krok, dokud nebudou zobrazeny žádné další výzvy.  

8. Po zpracování všech certifikátů počkejte, než aplikace Intune dokončí nastavování vašeho zařízení. Po zobrazení **sady, kterou jste nastavili** , budete mít jistotu, že se instalace dokončí! aplikací.  

    > [!div class="mx-imgBorder"]
    > ![Snímek obrazovky se sadou, kterou jste nastavili](./media/all-set-android.png)

## <a name="next-steps"></a>Další kroky

Po dokončení registrace budete mít přístup k pracovním prostředkům, například k e-mailu, Wi-Fi a všem aplikacím, které vaše organizace zpřístupňuje. Další informace o tom, jak získat, vyhledat, nainstalovat a odinstalovat aplikace v Intune, najdete v těchto tématech:

* [Použití spravovaných aplikací na zařízení](use-managed-apps-on-your-device-android.md)  
* [Správa aplikací z Portál společnosti webu](manage-apps-cpweb.md)  


Potřebujete ještě další pomoc? Obraťte se na podporu ve vaší společnosti. Kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).
