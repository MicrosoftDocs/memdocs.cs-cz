---
title: Odebrání zařízení s iOSem z Intune | Microsoft Docs
description: Popisuje odebrání zařízení s iOSem z Intune
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/02/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 28914db1-3e62-45f5-9632-b0d2a808a44d
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 6b5fe7c97b42c4863fbad8e7341b64fa847b8563
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79324191"
---
# <a name="remove-your-ios-device-from-intune"></a>Odebrání zařízení s iOSem z Intune

Pokud zařízení s iOSem odeberete z Intune, nebude mít přístup k prostředkům společnosti a nepůjde spravovat v Intune.


## <a name="removing-the-device-from-my-devices"></a>Odebrání z vlastních zařízení

K odebrání zařízení z Intune použijte následující postup. Můžete se také podívat na toto video:


1. V aplikaci Portál společnosti klepněte na **Zařízení** a vyberte zařízení, kterému chcete zrušit registraci. Pokud máte jenom jedno zařízení, přejdete po klepnutí na **Zařízení** přímo na stránku s jeho podrobnými informacemi.

2. Vedle možnosti **PŘEJMENOVAT** klepněte na tlačítko s třemi tečkami > **Odebrat zařízení** > **Odebrat**.  

    |![Snímek obrazovky Zařízení v aplikaci Portál společnosti s možnostmi, které se zobrazí po kliknutí uživatele na Odebrat Zobrazí se tlačítka Odebrat zařízení, Obnovení továrního nastavení a Zrušit.](./media/cp_ios_unenroll_after_1804_001.png)|

    |![Snímek obrazovky Zařízení v aplikaci Portál společnosti s možnostmi, které se zobrazí po kliknutí uživatele na Odebrat zařízení Tlačítko Odebrat zvýrazněné červeně a tlačítka Další informace a Zrušit zvýrazněná modře](./media/cp_ios_unenroll_after_1804_002.png)|


    Jakmile zrušíte registraci zařízení v Intune, stane se toto:

    - Vaše zařízení se už nebude zobrazovat v Portál společnosti.

    - Už nemůžete instalovat aplikace z Portál společnosti.

    - Nastavení, která se v zařízení změnila od jeho přidání, například zakázání fotoaparátu/kamery nebo vyžadování určité délky hesla, přestanou platit.

    - Je možné, že již v zařízení nebudete mít přístup k některým prostředkům společnosti, jako jsou sdílené složky nebo interní weby.

    - V zařízení už nemůžete používat firemní aplikace ani data společnosti.

    - Je možné, že se už nebudete moct připojovat k podnikové síti pomocí Wi-Fi nebo virtuální privátní sítě (VPN).

    - E-mailové profily společnosti jsou ze zařízení odebrané.

    - V aplikaci Portál společnosti a na webu se už nebudou zobrazovat zařízení, která jsou nakonfigurovaná jenom pro použití e-mailu.

    - Odinstalují se aplikace. Odeberou se data firemních aplikací.

## <a name="removing-data-collected-by-the-company-portal-app"></a>Odebrání dat shromažďovaných aplikací Portál společnosti

Aplikace Portál společnosti ukládá v zařízení data na třech místech.

- **Protokoly s informacemi**: Standardní data o aktivitě aplikací, která shromažďuje Microsoft, třeba jak dlouho byla aplikace otevřena nebo jestli havarovala, se vymažou automaticky při odebrání zařízení z webu Portál společnosti.

- **Analýza Apple**: Standardní data o havarovaných aplikacích, která shromažďuje Apple. Tyto informace můžete odebrat, jen když zařízení obnovíte zpět do továrního nastavení. Tím vymažete všechny osobní informace. Provedete to tak, že otevřete **Nastavení** > **Obecné** > **obnovit** > **vymazat veškerý obsah a nastavení**.

- **Řetězce klíčů**: Zařízení do řetězců klíčů ukládá hesla a další informace používané k přihlášení. Aplikace Microsoftu sdílejí přihlašovací údaje mezi všemi aplikacemi, které vyvíjí Microsoft a jsou na zařízení, včetně aplikací Microsoft Outlook a Microsoft Authenticator. Stejně jako analýzu Apple můžete tyto informace odebrat jenom vrácením (tj. resetováním) zařízení zpět do továrního nastavení. Tím vymažete všechny osobní informace. Provedete to tak, že otevřete **Nastavení** > **Obecné** > **obnovit** > **vymazat veškerý obsah a nastavení**.


Potřebujete ještě další pomoc? Obraťte se na podporu ve vaší společnosti. Kontaktní údaje najdete na [webu Portál společnosti](https://go.microsoft.com/fwlink/?linkid=2010980).
