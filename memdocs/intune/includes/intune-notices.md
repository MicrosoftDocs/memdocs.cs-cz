---
title: zahrnout soubor
description: zahrnout soubor
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: fbf352c3bccfb17efc35e34a2a822b6bbbcc215d
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/28/2020
ms.locfileid: "82183040"
---
Tato oznámení obsahují důležité informace, které vám pomůžou připravit se na budoucí změny a funkce Intune.

### <a name="microsoft-intune-support-for-windows-10-mobile-ending--3544938--"></a>Microsoft Intune podpora pro Windows 10 Mobile<!--3544938-->
Hlavní podpora Microsoftu pro Windows 10 Mobile skončila v prosinci 2019. Jak je uvedeno v tomto prohlášení o podpoře, uživatelé s Windows 10 Mobile už nebudou mít nárok na příjem nových aktualizací zabezpečení, opravy hotfix bez zabezpečení, bezplatné podpory s asistencí nebo online aktualizace obsahu od Microsoftu. V závislosti na podpoře všech mobilních operačních systémů se Microsoft Intune nyní ukončí podpora obou Portál společnosti pro mobilní aplikace Windows 10 a Windows 10 Mobile na 10. srpna 2020.

#### <a name="how-does-this-affect-me"></a>Co to pro mě znamená?
Pokud máte zařízení s Windows 10 Mobile nasazená ve vaší organizaci mezi teď a 10. srpna 2020, můžete registrovat nová zařízení, přidávat nebo odebírat zásady a aplikace nebo aktualizovat nastavení pro správu. Po 10. srpna zastavíme nové registrace a nakonec odebereme správu Windows 10 Mobile z uživatelského rozhraní Intune. Zařízení už nebudou zaregistrovaná ve službě Intune a odstraníme data zařízení a zásad.  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Jak se mám na tuto změnu připravit?
Můžete si prohlédnout sestavy Intune a zjistit, která zařízení nebo uživatelé to mohou mít vliv. Přejít na **zařízení** > **všechna zařízení** a filtrovat podle operačního systému. Můžete přidat další sloupce, které vám pomůžou identifikovat, kdo ve vaší organizaci má zařízení s Windows 10 Mobile. Zajistěte, aby vaši koncoví uživatelé upgradovali svoje zařízení, nebo aby zařízení nepoužívali pro podnikový přístup.


### <a name="end-of-support-for-legacy-pc-management"></a>Konec podpory pro správu starších počítačů

Podpora starší verze správy počítačů od 15. října 2020. Upgradujte zařízení na Windows 10 a znovu je zaregistrujte jako zařízení pro správu mobilních zařízení (MDM), abyste je mohli spravovat přes Intune.

[Další informace](https://go.microsoft.com/fwlink/?linkid=2107122)


### <a name="decreasing-support-for-android-device-administrator--5857738--"></a>Snížení podpory pro správce zařízení s Androidem<!--5857738-->
Správce zařízení s Androidem (někdy označovaný jako "starší verze" správy Androidu a vydaný s Androidem 2,2) je způsob, jak spravovat zařízení s Androidem. Vylepšené funkce správy jsou teď ale k dispozici v [Androidu Enterprise](../enrollment/connect-intune-android-enterprise.md) (vydané s androidem 5,0). V úsilí o přechod na moderní, bohatou a bezpečnější správu zařízení bude Google v nových verzích Androidu snížit podporu Správce zařízení.

#### <a name="how-does-this-affect-me"></a>Co to pro mě znamená?
Vzhledem k těmto změnám od společnosti Google budou mít uživatelé Intune tyto možnosti:  
- Intune bude moct poskytovat úplnou podporu pro zařízení s Androidem spravovaná pomocí Správce zařízení s Androidem 10 nebo novějším prostřednictvím nástroje Q2 CY2020. Zařízení spravovaná správcem zařízení, na kterých běží Android 10 nebo novější, se nebudou moct zcela spravovat. Zvláště ovlivněná zařízení nebudou dostávat nové požadavky na heslo.
    - V tomto období nebude mít vliv na zařízení Samsung KNOX, protože prostřednictvím integrace Intune s platformou Knox je zajištěná Rozšířená podpora. Získáte tak více času k naplánování přechodu mimo správu správy zařízení.    
- Zařízení s Androidem spravovaná správcem zařízení, která zůstávají ve verzích Androidu pod Androidem 10, nebudou ovlivněná a můžou se dál spravovat pomocí Správce zařízení.    
- Pro všechna zařízení s Androidem 10 nebo novějším má Google možnost agentů správy zařízení, jako je Portál společnosti získat přístup k informacím o identifikátoru zařízení. Toto omezení má vliv na následující funkce Intune po aktualizaci zařízení na Android 10 nebo novější:  
    - Řízení přístupu k síti pro VPN už nebude fungovat.   
    - Identifikace zařízení jako vlastněných společností pomocí IMEI nebo sériového čísla nebude automaticky označovat zařízení jako ve vlastnictví firmy.  
    - IMEI a sériové číslo se už nebudou zobrazovat správcům IT v Intune. 
        > [!NOTE]
        > To má vliv jenom na zařízení spravovaná správcem zařízení s Androidem 10 a novějším a nemá vliv na zařízení spravovaná jako Android Enterprise. 

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Jak se mám na tuto změnu připravit?
Abyste se vyhnuli omezení funkčnosti přicházejícím se do třetího CY2020, doporučujeme následující:
- Nepřidávejte nová zařízení do správy Správce zařízení.
- Pokud se očekává, že zařízení obdrží aktualizaci pro Android 10, migruje ji ze správy správců zařízení na zásady pro Android Enterprise Management a/nebo ochranu aplikací.

#### <a name="additional-information"></a>Další informace
- [Pokyny pro migraci ze strany správce zařízení na Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Dokumentace ke službě Google v plánu pro zařazování rozhraní API pro správce zařízení](https://developers.google.com/android/work/device-admin-deprecation)