---
title: Instalace ochrany před mobilními hrozbami na mobilní zařízení
description: Zjistěte, jaké jsou aplikace ochrany před mobilními hrozbami a jak ji nastavit.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/20/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser, contperfq1
ms.collection: ''
ms.openlocfilehash: 9ac83ce840d4a43de98791d6b116bb373a018a7d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914187"
---
# <a name="install-mobile-threat-defense-app"></a>Instalace aplikace Mobile Threat Defense  

> [!TIP]
> Na trhu je k dispozici celá řada aplikací MTD. Vaše organizace by vám měla sdělit, která z nich se má použít. Pokud se zobrazí výzva k instalaci aplikace MTD a nebudete okamžitě přesměrováni na nastavení nebo instalaci aplikace, požádejte o pomoc pracovníka podpory IT.  

V rámci požadavků na zabezpečení vaší organizace může být nutné nainstalovat aplikaci pro dodavatele ochrany před mobilními hrozbami (MTD). Tento typ aplikace detekuje a upozorňuje na hrozby na vašem zařízení, jako jsou podezřelé aplikace, sítě nebo ohrožení zabezpečení operačního systému.  

Pokud nemáte požadovanou aplikaci MTD, budete mít k vašemu pracovnímu nebo školnímu účtu zablokované přihlášení k chráněným, spravovaným aplikacím (jako je Microsoft Excel nebo OneDrive). V tomto článku se dozvíte, [jak nastavit aplikaci MTD](set-up-mobile-threat-defense.md#set-up-mtd-app) a získat přístup.    

## <a name="mtd-apps-for-ios"></a>Aplikace MTD pro iOS
Na zařízeních s iOS se běžně používají tyto aplikace MTD. Výběrem aplikace otevřete její výpis v App Storu.   

* [Lookout for Work](https://go.microsoft.com/fwlink/?linkid=2139367)
* [Symantec Endpoint Protection (SEP) – mobilní zařízení](https://go.microsoft.com/fwlink/?linkid=2139141)
* [Sandblast Mobile Protect](https://go.microsoft.com/fwlink/?linkid=2139231)
* [Zimperium zIPS](https://go.microsoft.com/fwlink/?linkid=2139232)


## <a name="mtd-apps-for-android"></a>Aplikace MTD pro Android 
Na zařízeních s Androidem se běžně používají tyto aplikace MTD. Výběrem aplikace otevřete její výpis v Google Play.  

* [Lookout for Work](https://go.microsoft.com/fwlink/?linkid=2139453)
* [Symantec Endpoint Protection (SEP) – mobilní zařízení](https://go.microsoft.com/fwlink/?linkid=2139454)
* [Sandblast Mobile Protect](https://go.microsoft.com/fwlink/?linkid=2139455)
* [Zimperium mobilní IP adresy (zIPS)](https://go.microsoft.com/fwlink/?linkid=2139142)  


## <a name="information-your-organization-can-see"></a>Informace, které vaše organizace uvidí   

Vaše organizace nemůže v osobních aplikacích zobrazit žádná data, jako jsou texty, e-maily a obrázky. Aplikace MTD oznamuje informace o vašich aplikacích, jako je název a verze, do vaší organizace. Skutečné informace hlášené v závislosti na dodavateli MTD, které vaše společnost používá. Vaše organizace může zobrazit tyto informace:   

* Název aplikace  
* ID aplikace: jedinečný název, který identifikuje aplikaci v Google Play.  
* Verze aplikace a krátké číslo verze: specifická čísla vydání pro aplikaci.  
* Sada prostředků aplikace a dynamická velikost: velikost místa, které aplikace v zařízení používá. 


## <a name="set-up-mtd-app"></a>Nastavení aplikace pro MTD 
Když se přihlásíte k chráněné aplikaci, zobrazí se výzva k instalaci aplikace MTD. Dokončete instalaci podle pokynů na obrazovce a získejte přístup k chráněné aplikaci. 

Další kontext najdete v pokynech pro [iOS](set-up-mobile-threat-defense.md#ios-setup) nebo [Android](set-up-mobile-threat-defense.md#android-setup) v této části. Tyto kroky jsou doplněny a nejsou určeny k nahrazení pokynů zobrazených na obrazovce. 

Pokud se zobrazí výzva k instalaci aplikace MTD, ale nejste si jistí, která z nich se má nainstalovat, požádejte o pomoc pracovníka podpory IT.  

### <a name="device-registration"></a>Registrace zařízení  
Registrace zařízení je nutná k potvrzení vaší identity a připojení školního nebo pracovního účtu k vašemu zařízení. Pokud zařízení není zaregistrované, po dokončení instalace aplikace MTD vás automaticky provedete těmito kroky na obrazovce.   

Další informace o registraci zařízení najdete v tématu [registrace osobního zařízení v síti vaší organizace](/azure/active-directory/user-help/user-help-register-device-on-network).  

### <a name="ios-setup"></a>instalace iOS  
Tyto kroky začínají na obrazovce **získat přístup** , která se zobrazí po přihlášení k chráněné aplikaci.  

1. Na obrazovce **získat přístup** postupujte podle pokynů k instalaci aplikace MTD, kterou vyžaduje vaše organizace.   
2. Vraťte se na obrazovku **získat přístup** a vyberte **otevřít**.  
3. Aplikace MTD požaduje oprávnění k otevření Microsoft Authenticator. Vyberte **Otevřít**. 
4. Vyberte svůj pracovní účet a přihlaste se. 
5. Počkejte, než aplikace MTD zkontroluje bezpečnostní hrozby ve vašem zařízení. 
6. Vraťte se do školy nebo pracovní aplikace, ke které jste se pokusili získat přístup. V tomto okamžiku může vaše organizace zobrazit výzvu ke konfiguraci dalších požadavků na zabezpečení aplikací, například vytvoření kódu PIN.   
7. Teď byste měli mít přístup k aplikaci. Pokud jste stále zablokovali:  
    * Na obrazovce **získat přístup** vyberte možnost znovu **ověřit**.  
    * Vraťte se do aplikace MTD a vyhledejte existující hrozby. Dokončete doporučený postup a vyřešte hrozbu a získejte přístup.    

### <a name="android-setup"></a>Nastavení pro Android 
Tyto kroky začínají na obrazovce **získat přístup** , která se zobrazí po přihlášení k chráněné aplikaci.  

1. Na obrazovce **získat přístup** postupujte podle pokynů k instalaci aplikace MTD, kterou vyžaduje vaše organizace.  
2. Vraťte se na obrazovku **získat přístup** a vyberte **otevřít**.  
3. Aplikace MTD žádá o vaše oprávnění pro přístup k určitým oblastem vašeho zařízení, takže by měla být. Aby tato aplikace fungovala správně, je nutné, abyste **povolili** přístup ke kontaktům. Požadovaná oprávnění se budou lišit v závislosti na MTD dodavatelích.  
4. Vyberte svůj pracovní účet a přihlaste se.  
5. Počkejte, než aplikace MTD zkontroluje bezpečnostní hrozby ve vašem zařízení.  
6. Vraťte se do školy nebo pracovní aplikace, ke které jste se pokusili získat přístup. V tomto okamžiku může vaše organizace zobrazit výzvu ke konfiguraci dalších požadavků na zabezpečení aplikací, například vytvoření kódu PIN.  
7. Teď byste měli mít přístup k aplikaci. Pokud jste stále zablokovali:  
    * Na obrazovce **získat přístup** vyberte možnost znovu **ověřit**.  
    * Vraťte se do aplikace MTD a vyhledejte existující hrozby. Dokončete doporučený postup a vyřešte hrozbu a získejte přístup.  


## <a name="resolving-a-threat"></a>Řešení hrozby
Pokud se zjistí hrozba, která překročí definovanou úroveň hrozby vaší organizace, bude vaše organizace:  
   
* Blokovat přístup: blokuje používání chráněných aplikací vaší organizace při přihlášení ke svému pracovnímu nebo školnímu účtu.  
* Vymazání dat: odstraní vaše pracovní nebo školní data z jedné nebo více chráněných aplikací vaší organizace.  

Řešení hrozby a opětovné získání přístupu k chráněným aplikacím:  

1. Otevřete na svém zařízení aplikaci MTD.     
2. Přečtěte si podrobnosti o hrozbách v aplikaci, které vysvětlují, jak může hrozba ovlivnit vaše zařízení, pokud je ponecháno nevyřešené a jak ho vyřešit. 
3. Až v zařízení provedete požadované změny, vraťte se do aplikace MTD a spusťte novou kontrolu. Opakujte tyto kroky, dokud nebudou vyřešeny všechny hrozby. Synchronizace změn ve vaší organizaci může trvat několik minut. Jakmile se tyto změny synchronizují, znovu získáte přístup k chráněné aplikaci. 

## <a name="get-support"></a>Získání podpory
Pokud chcete najít kontaktní údaje vaší organizace, navštivte [web portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980) . Požádejte je, aby vám pomohli:

* Určení používané aplikace MTD  
* Instalace  
* Neúspěšná instalace  
* Zjišťování a řešení hrozby  
* Odinstalace aplikace MTD   
 

### <a name="share-app-logs-with-it-support"></a>Sdílení protokolů aplikace s podporou IT  
Můžete také odeslat protokoly aplikací vaší osobě podpory IT a poskytnout jim další kontext o nezdařené instalaci.  
* Uživatelé Androidu: [nahrání a odeslání e-mailů protokolů](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android) z portál společnosti.   

* Uživatelé zařízení s iOS: [načítají a odesílají protokoly](https://docs.microsoft.com/intune/apps/manage-microsoft-edge#use-microsoft-edge-to-access-managed-app-logs) z Microsoft Edge pro iOS.  


## <a name="next-steps"></a>Další kroky  

V následujících článcích najdete další informace o tom, jak spravované aplikace fungují, jak je získat a jak rozpoznat, že ji používáte.  

* [Použití spravovaných aplikací na zařízení s Androidem](use-managed-apps-on-your-device-android.md)
* [Použití spravovaných aplikací na zařízení s iOSem](use-managed-apps-on-your-device-ios.md)  

Potřebujete ještě další pomoc? Obraťte se na podporu ve vaší společnosti. Kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).

