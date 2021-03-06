---
title: Registrace zařízení s Androidem pomocí Portál společnosti Intune | Microsoft Docs
description: Popisuje, jak zaregistrovat zařízení s Androidem pomocí Portál společnosti Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/27/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 0ed3a002-7533-4001-ae24-e10b64b66620
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: ef1b6c82cae82763dc327f16e35d0e3bc522c3c7
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057466"
---
# <a name="enroll-your-device-with-company-portal"></a>Registrace zařízení pomocí Portál společnosti  
Pokud chcete získat zabezpečený přístup k firemnímu e-mailu, aplikacím a datům, zaregistrujte své osobní nebo firemní zařízení s Androidem. Portál společnosti podporuje zařízení s Androidem, včetně Samsung KNOX, se systémem Android 4,4 a novějším.  
</br>
> [!VIDEO https://www.youtube.com/embed/k0Q_sGLSx6o?rel=0]

> [!NOTE]
> Samsung KNOX je typ zabezpečení, který některá zařízení Samsung využívají k další ochraně mimo rámec toho, co poskytuje nativní Android. Pokud chcete zjistit, jestli máte zařízení Samsung KNOX, > přejít na **Nastavení**  >  **o zařízení**. Pokud se tam uvedená **verze Knox** nezobrazuje, máte nativní zařízení s Androidem.  

## <a name="install-company-portal-app"></a>Instalace aplikace Portál společnosti  
Nainstalujte aplikaci Portál společnosti Intune [z Google Play](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal). Seznam obchodů, které nabízejí aplikaci v Čínské lidové republice, najdete v tématu [instalace portál společnosti aplikace v Čínské lidové republice](install-company-portal-android-china.md) .

1. Klepněte na **Domovská**  >  **Obchod Play**.

2. Vyhledejte **portál společnosti Intune**. Pak klepněte na aplikaci a otevřete ji. 

    ![android-search-company-portal](./media/and-cpinstall-1-search-cp.png)

4. Klepněte na **instalovat**.

5. Po zobrazení výzvy k zadání oprávnění aplikace klepněte na **přijmout**.  

    ![android-accept-company-portal-terms](./media/and-cpinstall-3-cp-accept.png)

## <a name="enroll-device"></a>Registrace zařízení  
Během registrace můžete být požádáni, abyste zvolili kategorii, která nejlépe popisuje způsob používání zařízení. Vaše firemní podpora používá vaši odpověď ke kontrole aplikací, ke kterým máte přístup.  

1. Otevřete aplikaci Portál společnosti a přihlaste se pomocí svého pracovního nebo školního účtu.  

2. Pokud budete vyzváni, abyste přijali podmínky a ujednání vaší organizace, klepněte na **přijmout vše**.  

   ![Příklad obrázku obrazovky Portál společnosti, podmínky, zvýraznění tlačítka přijmout vše](./media/accept-terms-1911.png)  


3. Projděte si informace o tom, co vaše organizace uvidí nebo neuvidí. Pak klepněte na **pokračovat**.


    ![Příklad obrázku Portál společnosti, záleží na obrazovce ochrany osobních údajů a zvýrazníme tlačítko pokračovat.](./media/android-privacy-screen-1911.png)  
4. Přečtěte si, co očekávat v nadcházejících krocích. Pak klepněte na **Další**.  

    ![Příklad obrázku Portál společnosti, co je další obrazovka a zvýrazní se tlačítko Další.](./media/android-whats-next-1911.png)  


5. V závislosti na vaší verzi Androidu se může zobrazit výzva, abyste povolili přístup k určitým částem vašeho zařízení. Tyto výzvy vyžaduje Google a neřídí je Microsoft.  

    Klepněte na možnost **udělit** pro následující oprávnění:  
    * **Povolit portál společnosti, aby mohli provádět a spravovat telefonní hovory**: Toto oprávnění umožňuje vašemu zařízení sdílet číslo IMEI (International Mobile Equipment Identity) s Intune a poskytovatelem správy zařízení ve vaší organizaci. Toto oprávnění je bezpečné. Společnost Microsoft nikdy neprovede ani nespravuje telefonní hovory.  
    * **Umožněte portál společnosti přistupovat ke kontaktům**: Toto oprávnění umožňuje aplikaci Portál společnosti vytvářet, používat a spravovat váš pracovní účet.  Toto oprávnění je bezpečné. Společnost Microsoft nebude nikdy přistupovat k vašim kontaktům. 

    Pokud odepřete oprávnění, zobrazí se při příštím přihlášení k Portál společnosti dotaz znovu. Chcete-li tyto zprávy vypnout, vyberte možnost **příště znovu zobrazit dotaz**. Pokud chcete spravovat oprávnění aplikace, přečtěte si v části nastavení aplikace > **aplikace**  >  **portál společnosti**  >  **oprávnění**  >  **telefon**.  

6. Aktivujte aplikaci Správce zařízení. 

    Portál společnosti potřebuje oprávnění správce zařízení pro bezpečnou správu zařízení. Aktivace aplikace umožňuje, aby vaše organizace identifikovala možné problémy se zabezpečením, jako jsou opakované neúspěšné pokusy o odemknutí zařízení, a odpovídajícím způsobem reagovat.  

    ![Příklad obrázku obrazovky aktivace Správce zařízení – zvýrazní se tlačítko aktivovat.](./media/activate-device-administrator-1911.png)  

> [!NOTE]
> Microsoft neřídí zprávy na této obrazovce. Chápeme, že jeho formulace může vypadat trochu drasticky. Portál společnosti nemůže určit, která omezení a přístup jsou relevantní pro vaši organizaci. Pokud máte dotazy ohledně toho, jak vaše organizace používá aplikaci, obraťte se na pracovníky podpory IT. Pokud chcete najít kontaktní údaje vaší organizace, navštivte [web portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980) .  


7. Vaše zařízení zahájí registraci. Pokud používáte zařízení Samsung KNOX, budete vyzváni, abyste nejdřív zkontrolovali a potvrdili zásady ochrany osobních údajů agenta ELM.   

    ![Příklad obrázku obrazovky zásady ochrany osobních údajů Samsung KNOX, která se zobrazí během registrace.](./media/and-enroll-7-knox-privacy-policy.png)  

8. Na obrazovce **nastavení firemního přístupu** ověřte, že je vaše zařízení zaregistrované. Pak klepněte na **pokračovat**.  

    ![Příklad obrázku Portál společnosti, obrazovka nastavení firemního přístupu, která ukazuje, že je vaše zařízení spravované, je dokončené.](./media/update-settings-1911.png)  

9. Vaše organizace může vyžadovat, abyste aktualizovali nastavení zařízení. Klepnutím na **vyřešit** upravte nastavení. Po dokončení aktualizace nastavení klepněte na **pokračovat**.  

   ![Příklad obrázku Portál společnosti, aktualizace nastavení zařízení, zvýraznění tlačítek vyřešit a pokračovat.](./media/resolve-settings-1911.png)  

10. Po dokončení instalace klepněte na **Hotovo**.    

    ![Příklad obrázku Portál společnosti, obrazovka nastavení firemního přístupu, zobrazení dokončeného nastavení a zvýraznění tlačítka Hotovo.](./media/android-enrollment-done-1911.png) 

## <a name="next-steps"></a>Další kroky  

Než se pokusíte nainstalovat školní nebo pracovní aplikaci, přejdete na **Nastavení**  >  **zabezpečení**a zapněte **neznámé zdroje**. Pokud tuto možnost nezapnete, zobrazí se při pokusu o instalaci aplikace následující zpráva: "instalace blokována. Z důvodů zabezpečení je v zařízení nastavené blokování instalací pro aplikace získané z neznámého zdroje.“ Klepnutím na **Nastavení** ve zprávě můžete přejít přímo k **neznámým zdrojům**.  

> [!Note]
> Pokud vaše organizace používá software pro správu telekomunikačních výdajů (Telecom Expense Management), budete muset před úplnou registrací zařízení provést několik dalších kroků. Další informace najdete [tady](enroll-your-device-with-telecom-expense-management-android.md).

Pokud při pokusu o registraci zařízení do služby Intune dojde k chybě, můžete [Odeslat e-mailovou podporu společnosti](send-logs-to-your-it-admin-by-email-android.md).  

Potřebujete ještě další pomoc? Obraťte se na podporu ve vaší společnosti. Kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).  