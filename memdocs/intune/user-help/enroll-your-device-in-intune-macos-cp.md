---
title: Registrace počítače Mac s Portál společnosti Intune | Microsoft Docs
description: Naučte se, jak zaregistrovat svůj počítač Mac v Intune pomocí aplikace Portál společnosti.
keywords: Mac OS X, macOS, OS X
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/18/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 3bb659cc-9b57-4d19-8631-2c26749fa71c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: kakyker
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: fe405b66892ec7777d8d1572b2fb6ab6ce1aaa91
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/19/2020
ms.locfileid: "85094191"
---
# <a name="enroll-your-macos-device-using-the-company-portal-app"></a>Registrace zařízení macOS pomocí aplikace Portál společnosti  

Pokud chcete získat zabezpečený přístup k pracovnímu nebo školnímu e-mailu, souborům a aplikacím, zaregistrujte zařízení macOS pomocí aplikace Portál společnosti Intune.

Organizace obvykle vyžadují, abyste si zařízení zaregistrovali předtím, než budete mít přístup ke speciálním datům. Po registraci zařízení se bude *Spravovat*. Vaše organizace může k zařízení přiřadit zásady a aplikace prostřednictvím poskytovatele správy mobilních zařízení (MDM), jako je třeba Intune. Pokud chcete mít nepřetržitý přístup k pracovním nebo školním informacím na zařízení, musíte zařízení nastavit tak, aby odpovídalo nastavení zásad vaší organizace.  

Tento článek popisuje, jak používat aplikaci Portál společnosti pro macOS k nastavení a údržbě zařízení, abyste splnili požadavky vaší organizace.  


## <a name="what-to-expect-from-the-company-portal-app"></a>Co čekat od aplikace Portál společnosti

Při počáteční instalaci aplikace Portál společnosti vyžaduje, abyste se přihlásili a ověřili ve své organizaci. Portál společnosti pak informuje o všech nastaveních, která potřebujete ke konfiguraci, aby splňovala požadavky vaší organizace. Organizace si například často určují požadavky na minimální a maximální délku hesla, které musíte splnit.    

Po registraci zařízení se Portál společnosti vždycky ujistěte, že je zařízení chráněné podle požadavků vaší organizace. Pokud například nainstalujete aplikaci ze zdroje, který není důvěryhodný, Portál společnosti vás upozorní a může omezit přístup k prostředkům vaší organizace. Zásady ochrany aplikací, jako je tato, jsou běžné. Chcete-li znovu získat přístup, budete pravděpodobně muset aplikaci odinstalovat. 

Pokud po registraci vaše organizace vynutila nový požadavek na zabezpečení, jako je například vícefaktorové ověřování, Portál společnosti vás upozorní. Budete tak mít možnost si nastavení upravit, abyste se zařízením mohli dále pracovat.  

Další informace o registraci najdete v tématu s informacemi o tom, [co se stane, když nainstaluji aplikaci Portál společnosti a zaregistruji zařízení](what-happens-if-you-install-the-Company-Portal-app-and-enroll-your-device-in-intune-macos.md).  

## <a name="get-your-macos-device-managed"></a>Jak spravovat zařízení macOS  
Pomocí následujících kroků zaregistrujete zařízení macOS ve vaší organizaci. Vaše zařízení musí používat macOS 10,12 nebo novější.   

> [!NOTE]
> V průběhu tohoto procesu se může zobrazit výzva, abyste Portál společnosti mohli používat důvěrné informace, které jsou uložené v řetězci klíčů. Tyto výzvy jsou součástí zabezpečení Apple. Po zobrazení výzvy zadejte přihlašovací heslo k řetězci a vyberte možnost **vždy povoleno**. Pokud stisknete klávesu **ENTER** nebo **return** na klávesnici, místo toho se zobrazí výzva k výběru **Povolení**, což může způsobit další výzvy.  

### <a name="install-company-portal-app"></a>Instalace aplikace Portál společnosti  
1. Přejít na [zaregistrovat Mac](https://go.microsoft.com/fwlink/?linkid=853070)  
2. Soubor instalačního programu Portál společnosti. pkg se stáhne. Spusťte instalační program a pokračujte postupem. 
3. Vyjádřit souhlas s licenční smlouvou k softwaru. 
4. Pro instalaci softwaru zadejte heslo zařízení nebo registrovaný otisk prstu.  
5. Otevřete Portál společnosti. 

> [!IMPORTANT]
> Microsoft AutoUpdate se může otevřít a aktualizovat si software Microsoftu. Po instalaci všech aktualizací otevřete aplikaci Portál společnosti. Pro dosažení nejlepšího prostředí pro instalaci nainstalujte nejnovější verze Microsoft AutoUpdate a Portál společnosti.  


### <a name="enroll-your-mac"></a>Registrace počítače Mac  


1. Přihlaste se k Portál společnosti pomocí svého pracovního nebo školního účtu.  
2. Po otevření aplikace vyberte **začít**.  
3. Přečtěte si [, co vaše organizace uvidí a](what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md) neuvidí na zaregistrovaném zařízení. Potom vyberte **Pokračovat**.
4. Na obrazovce **Instalace profilu správy** vyberte **Stáhnout profil**.  

    ![Příklad obrazovky Portál společnosti, obrazovky pro instalaci profilu správy, zvýrazňování výzvy k zadání hesla](./media/install-management-profile-macos-2006.png)   

5. Spustí se Předvolby systému vašeho zařízení.  
    a. Vyberte **nainstalovat** a pak znovu vyberte **nainstalovat** .  
    b. Pokud budete vyzváni k zadání hesla zařízení.   
6. Po instalaci se profil zobrazí v seznamu profily v části **Profil správy**.
    ![Příklad obrazovky Předvolby systému, obrazovka profilu správy, zvýrazňování tlačítka "schválit".](./media/management-profile-approve-macos-2006.png)   
7. Vraťte se na Portál společnosti.    
8. Vaše organizace může vyžadovat, abyste aktualizovali nastavení zařízení. Po dokončení aktualizace nastavení vyberte **Opakovat**.  

    ![Příklad obrazovky Portál společnosti, aktualizace nastavení zařízení, zvýraznění tlačítka opakovat.](./media/update-settings-mac-2006.png)  
9. Po dokončení instalace vyberte **Hotovo**.  


 ## <a name="troubleshooting-and-feedback"></a>Řešení potíží a zpětná vazba   

Pokud při registraci narazíte na problémy, přečtěte si **informace v tématu**  >  **poslat diagnostickou zprávu** a oznamte problém vývojářům aplikací Microsoftu. Tyto informace se používají k vylepšení aplikace. Tyto informace budou také tyto informace používat k vyřešení problému, pokud se na něj pracovník podpory IT dostane, aby vám pomohli.  

Po nahlášení problému společnosti Microsoft můžete odeslat podrobnosti o vašem prostředí vaší osobě podpory IT. Vyberte **Podrobnosti e-mailu**. Zadejte, co jste se setkali v těle e-mailu. Pokud chcete najít e-mailovou adresu pracovníka podpory, přečtěte si v aplikaci Portál společnosti > **kontaktujte**. Nebo se podívejte na [web portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).  
 

Kromě toho tým Microsoft Intune Portál společnosti by chtěl slyšet vaši zpětnou vazbu. Přejít na další **informace**a  >  **poslat zpětnou vazbu** ke sdílení vašich nápadů a nápadů.  

## <a name="unverified-profiles"></a>Neověřené profily  
Když zobrazíte nainstalované profily správy mobilních zařízení (MDM) v **System Preferences**  >  **profilech**systémových předvoleb, můžou se u některých profilů zobrazit neověřený stav. Pokud profil správy zobrazuje ověřený stav, nemusíte se zabývat.  

Právě profil správy definuje připojení kanálu MDM. Dokud se profil správy ověří, všechny ostatní profily doručené počítači prostřednictvím tohoto kanálu zdědí vlastnosti zabezpečení profilu správy.  

## <a name="updating-the-company-portal-app"></a>Aktualizace aplikace Portál společnosti

Aktualizace aplikace Portál společnosti se provádí stejným způsobem jako jakákoli jiná aplikace Office, a to prostřednictvím Microsoft AutoUpdate pro macOS. Přečtěte si další informace o [aktualizaci aplikací Microsoftu pro MacOS](https://support.office.com/article/Check-for-Office-for-Mac-updates-automatically-bfd1e497-c24d-4754-92ab-910a4074d7c1).  

## <a name="next-steps"></a>Další kroky  
Potřebujete ještě další pomoc? Obraťte se na podporu ve vaší společnosti. Kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).  


