---
title: Nastavení přístupu zařízení s iOSem k prostředkům společnosti | Microsoft Docs
description: Popisuje, jak začít spravovat zařízení s iOSem pomocí Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/18/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 6eeec7aa-1b07-4ce3-894c-13e09b89bdd4
searchScope:
- User help
ROBOTS: ''
ms.reviewer: tisilv
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 49e598f370669ed55688af6e6a570a932b5bf9d3
ms.sourcegitcommit: 3ff33493c3f93bf06fdc942d30958a2a4ad03529
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/24/2020
ms.locfileid: "82137962"
---
# <a name="set-up-ios-device-access-to-your-company-resources"></a>Nastavení přístupu zařízení s iOSem k prostředkům společnosti  

Zaregistrujte si zařízení s iOSem pomocí aplikace Portál společnosti v Intune a získejte zabezpečený přístup k e-mailům, souborům a aplikacím vaší organizace.

Po registraci zařízení se bude *Spravovat*. Vaše organizace může k zařízení přiřadit zásady a aplikace prostřednictvím poskytovatele správy mobilních zařízení (MDM), jako je třeba Intune.  

> [!NOTE]
> Žádná data shromážděná naší službou neprodávají z jakéhokoli důvodu žádné třetí straně.  

Pokud chcete zachovat přístup k pracovním nebo školním informacím ze zařízení, budete muset nakonfigurovat zařízení tak, aby odpovídalo preferovanému nastavení vaší organizace. Tento článek popisuje, jak použít Portál společnosti k registraci zařízení a udržování požadavků na nastavení vaší organizace.  
</br>
> [!VIDEO https://www.youtube.com/embed/mJyv6YcHi7c?rel=0]

> [!NOTE]
> Pokud jste se pokusili přistoupit k podnikovému e-mailu v aplikaci Pošta a zobrazila se vám výzva ke správě vašeho zařízení, jste na správném místě. Podle pokynů uvedených níže získáte přístup ke svému e-mailu a dalším prostředkům společnosti na zařízení s iOSem.  


## <a name="what-to-expect-from-the-company-portal-app"></a>Co čekat od aplikace Portál společnosti  

### <a name="security"></a>Zabezpečení  
Při počátečním nastavení vás aplikace požádá, abyste se ve vaší organizaci ověřili. Potom vás informuje o všech nastaveních, která musíte aktualizovat. Organizace si například často určují požadavky na minimální a maximální délku hesla, které musíte splnit.

### <a name="protection"></a>Ochrana  
Po registraci zařízení bude aplikace Portál společnosti i nadále kontrolovat, že je chráněno. Pokud si například nainstalujete aplikaci z nedůvěryhodného zdroje, upozorní vás a dokonce vám může i odvolat přístup k firemním datům. Tento druh zásad je v organizacích společný a často vyžaduje, abyste před tím, než budete moct znovu získat přístup, odinstalovali nedůvěryhodnou aplikaci.  

### <a name="setting-notifications"></a>Nastavení oznámení  
Pokud po registraci vaše organizace vynucuje nový požadavek na zabezpečení (například vícefaktorové ověřování), aplikace Portál společnosti vás o něm informuje. Budete tak mít možnost si nastavení upravit, abyste se zařízením mohli dále pracovat.  

Další informace o registraci najdete v tématu s informacemi o tom, [co se stane, když nainstaluji aplikaci Portál společnosti a zaregistruji zařízení](https://docs.microsoft.com//mem/intune/user-help/what-happens-if-you-install-the-company-portal-app-and-enroll-your-device-in-intune-ios).  

## <a name="enroll-your-ios-device"></a>Registrace zařízení s iOSem  

Pokud si chcete stáhnout a nainstalovat [aplikaci Portál společnosti Intune](install-and-sign-in-to-the-intune-company-portal-app-ios.md) do svého zařízení, přejdete do obchodu App Store. Budete také muset udržovat připojení Wi-Fi a mít přístup k Safari během registrace. 

Pozastavení aplikace po dobu delší než několik minut může způsobit ukončení nebo ukončení instalace aplikace. Pokud k tomu dojde, otevřete aplikaci Portál společnosti a zkuste to znovu.  

1. Otevřete Portál společnosti a přihlaste se pomocí svého pracovního nebo školního účtu.  

2. Po zobrazení výzvy k přijetí oznámení Portál společnosti klepněte na možnost **povolení.** Portál společnosti používá oznámení k upozornění, pokud například potřebujete aktualizovat nastavení zařízení.  

3. Na obrazovce **nastavit přístup** vyberte **začít.**   

    ![Příklad obrazovky Portál společnosti a obrazovky "nastavit přístup".](./media/ios-enrollment-checklist-1909.PNG)  

4. Zobrazí se obrazovka **Vybrat typ zařízení a registrace** a zobrazí výzvu k zadání typu zařízení.  
    * Klepněte na **(organizace) Toto zařízení vlastní** , pokud jste si dostali zařízení z vaší organizace. Potom přejděte na [zabezpečení celé zařízení](#secure-entire-device) v tomto článku a dokončete instalaci.  
    * Pokud používáte osobní zařízení, které jste napravili z domova, klepněte na **Toto zařízení** . Pak pokračujte na další krok.  

    Pokud tuto obrazovku nevidíte, přejděte k nastavení [zabezpečit celé zařízení](#secure-entire-device) a dokončete instalaci.  
    
    ![Příklad obrazovky Portál společnosti, obrazovky "vybrat zařízení a typ registrace", možnosti typu zařízení.](./media/ios-device-type-1909.PNG)  


5. Vyberte způsob ochrany dat v zařízení po jeho registraci.  
    * Pokud chcete zabezpečit všechny aplikace a data v zařízení, klepněte na **zabezpečit celé zařízení** . Pak pokračujte v nastavení [zabezpečení celého zařízení](enroll-your-device-in-intune-ios.md#secure-entire-device) .
    * Klepněte na **zabezpečené pracovní aplikace a data jenom** k zabezpečení aplikací a dat, ke kterým přistupujete pomocí svého pracovního účtu. Pak přejdete k [zabezpečeným aplikacím a datům souvisejícím s prací](enroll-your-device-in-intune-ios.md#secure-work-related-apps-and-data).  

    ![Příklad obrazovky Portál společnosti, "vybrat zařízení a typ registrace", možnosti typu registrace.](./media/ios-enrollment-type-1909.PNG)  


### <a name="secure-entire-device"></a>Zabezpečit celé zařízení  

1. Na obrazovce **Správa a ochrana osobních údajů** v zařízení si přečtěte seznam informací o zařízení, které vaše organizace může a neuvidí. Pak klepněte na **pokračovat**.  


 > [!IMPORTANT]
> Tyto další kroky a obrazovky se budou lišit v závislosti na verzi iOS. Postupujte podle kroků pro verzi iOS. 

2. Safari otevře web Portál společnosti na vašem zařízení. Po zobrazení výzvy ke stažení konfiguračního profilu klepněte na možnost **Povolení**. Pokud se nacházíte na zařízení se systémem:  
    * iOS 12,2 a novější: po dokončení stahování klepněte na **Zavřít**. Pak pokračujte krokem 3.  
    * iOS 12,1 a starší: po dokončení stahování budete automaticky přesměrováni do aplikace nastavení. Přejděte ke kroku 4.  
 
    Pokud omylem klepnete na **Ignorovat**, aktualizujte stránku. Zobrazí se výzva k otevření aplikace Portál společnosti. Až to budete mít, klepněte **znovu na Stáhnout**.

  > [!NOTE]
  > Je nutné nainstalovat profil pro správu, jak je popsáno v následujících krocích během 8 minut od stažení. Pokud to neuděláte, profil se odebere a bude nutné restartovat registraci.  

3. Po zobrazení výzvy k otevření Portál společnosti klepněte na **otevřít**. Přečtěte si informace na obrazovce **Instalace profilu správy** .  

4. Přejdete do aplikace nastavení a klepnete na **zaregistrovat < název organizace >** nebo **Stáhnout profil**.  

    ![Příklad snímku obrazovky aplikace nastavení, registrace v možnosti organizace](./media/enroll-in-organization-ios-1909.PNG)  

   Pokud se nezobrazí žádné možnosti, jděte do **obecných** > **profilů &**> **Profil správy**správy zařízení. Pokud se vám stále nezobrazuje profil správy, budete ho muset stáhnout znovu.  

5. Klepněte na **instalovat**.  
    
6. Zadejte heslo zařízení. Pak klepněte na **instalovat**.    

7. Další obrazovka má standardní systémové upozornění týkající se správy zařízení. Pokud chcete pokračovat v instalaci, klepněte na **instalovat**. Pokud se zobrazí výzva k důvěřování vzdálené správě, klepněte na **důvěřovat**.  

8. Po dokončení instalace klepněte na **Hotovo**. Pokud chcete ověřit, že se profil nainstaloval, klikněte na **profily & nastavení správy zařízení** . Měl by se zobrazit profil uvedený v části **Správa mobilních zařízení**.   

    ![Příklad obrazovky nastavení aplikace, profily & nastavení správy zařízení, zobrazení profilu správy.](./media/ios-12-cp-enroll-1904.PNG)  

9. Vraťte se do aplikace Portál společnosti. Portál společnosti se začne synchronizovat a nastavit vaše zařízení. Portál společnosti vás může zobrazit výzva k aktualizaci dalších nastavení zařízení. Pokud k tomu klepne, klepněte na **pokračovat**.  

10. Poznáte, že je instalace dokončena, když všechny položky v seznamu zobrazí zelenou značku zaškrtnutí. Klepněte na **Hotovo**.   

> [!Note]
> Pokud vaše organizace sleduje omezení hlasu a dat nebo poskytuje zařízení vlastněná společností, může být potřeba provést několik dalších kroků. Pokud se zobrazí výzva k instalaci aplikace **Datalert** , přečtěte si téma [registrace zařízení ve správě telekomunikačních výdajů](enroll-your-device-with-telecom-expense-management-ios.md). Pokud je vaše organizace součástí Program registrace zařízení společnosti Apple, přečtěte si, [jak zaregistrovat zařízení vlastněné společností](enroll-your-device-dep-ios.md).  

### <a name="secure-work-related-apps-and-data"></a>Zabezpečení aplikací a dat souvisejících s prací  
1. Zobrazí se obrazovka pro **stažení Microsoft Authenticator** (Pokud už máte ověřovací data, tato obrazovka se nezobrazí, takže přejděte ke kroku 2).  
    1. Klepněte na **stáhnout z App Storu**.
    2. Po otevření App Storu se aplikace nainstaluje. 
    3. Vraťte se do Portál společnosti a klepněte na **pokračovat**.    
    
   Po instalaci Microsoft Authenticator nebudete muset provádět žádné další akce s aplikací. Stačí, abyste na svém zařízení nacházeli. 

   ![Příklad obrazovky Portál společnosti a obrazovky "stáhnout Microsoft Authenticator".](./media/download-ms-authenticator-1909.PNG)  

2. Na obrazovce **Správa a ochrana osobních údajů** v zařízení si přečtěte seznam informací o zařízení, které vaše organizace může a neuvidí. Pak klepněte na **pokračovat**.  


 > [!IMPORTANT]
> Tyto další kroky a obrazovky se budou lišit v závislosti na verzi iOS. Postupujte podle kroků pro verzi iOS. 

3. Safari otevře web Portál společnosti na vašem zařízení. Po zobrazení výzvy ke stažení konfiguračního profilu klepněte na možnost **Povolení**. Pokud se nacházíte na zařízení se systémem:  
    * iOS 12,2 a novější: po dokončení stahování klepněte na **Zavřít**. Pak pokračujte krokem 4.  
    * iOS 12,1 a starší: po dokončení stahování budete automaticky přesměrováni do aplikace nastavení. Přejděte na krok 5.  
 
    Pokud omylem klepnete na **Ignorovat**, aktualizujte stránku. Zobrazí se výzva k otevření aplikace Portál společnosti. Z aplikace můžete znovu klepnout na **Stáhnout**.

  > [!NOTE]
  > Je nutné nainstalovat profil pro správu, jak je popsáno v následujících krocích během 8 minut od stažení. Pokud to neuděláte, profil se odebere a bude nutné restartovat registraci.  

4. Po zobrazení výzvy k otevření Portál společnosti klepněte na **otevřít**. Přečtěte si informace na obrazovce **Instalace profilu správy** . 

5. Přejdete do aplikace nastavení a klepnete na **zaregistrovat < název organizace >** nebo **Stáhnout profil**.  

    ![Příklad snímku obrazovky aplikace nastavení, registrace v možnosti organizace](./media/enroll-in-organization-ios-1909.PNG)  

   Pokud se nezobrazí žádné možnosti, jděte do **obecných** > **profilů &**> **Profil správy**správy zařízení. Pokud se vám stále nezobrazuje profil správy, budete ho muset stáhnout znovu.   


6. Na obrazovce **registrace uživatele** klepněte na **Registrovat iPhone**.  

    ![Ukázkový snímek obrazovky aplikace nastavení, obrazovka registrace uživatele a zvýraznění tlačítka zapsat](./media/user-enrollment-information-1909.PNG)  

7. Zadejte heslo zařízení. Pak klepněte na **instalovat**.  

8. Na **přihlašovací** obrazovce zadejte heslo pro vaše spravované Apple ID. Ve většině případů budou tyto přihlašovací údaje stejné jako při přihlášení k pracovnímu nebo školnímu účtu, pokud vám vaše organizace neposkytla jinou sadu přihlašovacích údajů. 
9. Klepněte na **Přihlásit se**.  
10. Na obrazovce se krátce po instalaci profilu zobrazí zpráva o úspěchu. Pokud chcete ověřit, že se profil nainstaloval, klikněte na **profily & nastavení správy zařízení** . Měl by se zobrazit profil uvedený v části **Správa mobilních zařízení.**  

    ![Příklad obrazovky nastavení aplikace, profily & nastavení správy zařízení, zobrazení profilu správy.](./media/ios-12-cp-enroll-1904.PNG)  

11. Vraťte se do aplikace Portál společnosti. Portál společnosti se začne synchronizovat a nastavit vaše zařízení. Portál společnosti vás může zobrazit výzva k aktualizaci dalších nastavení zařízení. Pokud k tomu klepne, klepněte na **pokračovat**.    

12. Poznáte, že je instalace dokončena, když všechny položky v seznamu zobrazí zelenou značku zaškrtnutí. Klepněte na **Hotovo**.  

## <a name="it-administrator-support"></a>Podpora správce IT  
Pokud jste správcem IT a máte potíže s registrací zařízení, přečtěte si téma řešení potíží s registrací [zařízení s iOS v Microsoft Intune](https://support.microsoft.com/en-us/help/4039809). V tomto článku jsou uvedené běžné chyby, jejich příčiny a kroky, jak je vyřešit.  

## <a name="next-steps"></a>Další kroky  
Najděte aplikace, které vám pomůžou při práci nebo ve škole. Seznamte se s tím, [jak jsou aplikace zpřístupněny](use-managed-apps-on-your-device-ios.md) prostřednictvím portál společnosti.  

Potřebujete ještě další pomoc? Obraťte se na svou firemní podporu. Kontaktní informace správce najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).  
