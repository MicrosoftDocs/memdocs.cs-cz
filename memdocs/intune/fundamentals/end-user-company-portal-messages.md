---
title: Zprávy Portálu společnosti, které se můžou uživatelům zobrazit na zařízeních
titleSuffix: Microsoft Intune
description: Vysvětlení různých zpráv, které se můžou koncovým uživatelům zobrazit v aplikaci Portál společnosti
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/09/2017
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3df993aa-48c5-4799-b68d-c85fe4f7b02c
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 91c79ae7ca7fc70c361fba0a7ad6becf8d035b5a
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79332611"
---
# <a name="help-end-users-understand-company-portal-app-messages"></a>Vysvětlení zpráv aplikace Portál společnosti pro koncové uživatele

> [!NOTE]
> Následující informace se vztahují jenom na zařízení s Androidem 6.0 + a iOS 10 +.

Tady najdete vysvětlení různých zpráv, které se můžou koncovým uživatelům zobrazit v aplikaci Portál společnosti. Tyto zprávy aplikace se běžně zobrazují v různých okamžicích procesu registrace. Zjistěte, kde se tyto zprávy objevují, co znamenají a co se stane, když uživatel přístup zamítne. Také se dozvíte, jak zprávy nejlépe vysvětlit uživatelům.

- __Povolit pro Portál společnosti telefonování a správu telefonních hovorů?__
- __Povolit pro Portál společnosti přístup k fotkám, médiím a souborům ve vašem zařízení?__

> [!NOTE]
> Žádná data shromážděná naší službou neprodávají z jakéhokoli důvodu žádné třetí straně.

## <a name="allow-company-portal-to-make-and-manage-phone-calls"></a>Povolit pro Portál společnosti telefonování a správu telefonních hovorů?

### <a name="where-it-appears"></a>Místo zobrazení

Zpráva **Povolit pro Portál společnosti telefonování a správu telefonních hovorů?** se zobrazí, když uživatel během registrace svého zařízení klepne v aplikaci Portál společnosti na možnost **Zaregistrovat**.

### <a name="what-it-means"></a>Význam

Přijetím této výzvy uživatel umožní, aby se telefonní číslo a číslo IMEI jeho zařízení odeslala do služby Intune. Tyto údaje se objeví v konzole pro správu na stránce __Hardware__.

> [!NOTE]
> **Aplikace Portál společnosti nikdy netelefonuje ani nespravuje telefonní hovory!** Text zprávy je pod kontrolu Googlu a nejde ho změnit.

Stránku **Hardware** zobrazíte tak, že přejdete na **Skupiny** > **Všechna mobilní zařízení** > **Zařízení**. Vyberte zařízení uživatele a pak přejít na **Zobrazit vlastnosti** > **hardware**.

### <a name="what-happens-if-users-deny-access"></a>Co se stane, když uživatel přístup zamítne

Pokud uživatel přístup zamítne, může aplikaci Portál společnosti dál používat a zaregistrovat své zařízení. Na stránce __Hardware__ v konzole pro správu ale bude telefonní číslo a číslo IMEI zařízení prázdné. Při druhém přihlášení k aplikaci Portál společnosti po zamítnutí přístupu se ve zprávě zobrazí zaškrtávací políčko **Příště se už neptat**, takže uživatel může zobrazování této výzvy zastavit.

Pokud uživatel povolí přístup, ale později ho zamítne, zobrazí se tato zpráva při přihlášení k aplikaci Portál společnosti, které následuje po registraci zařízení.

Pokud se uživatel později rozhodne povolit přístup, může přejít na **Nastavení** > **aplikace** > **portál společnosti** > **oprávnění** > **telefon**a zapnout ho.

### <a name="how-to-explain-this-to-your-users"></a>Jak to vysvětlit uživatelům

Nasměrujte uživatele na článek [Registrace zařízení s Androidem v Intune](../user-help/enroll-device-android-company-portal.md), kde najdou další informace.

## <a name="allow-company-portal-to-access-your-contacts"></a>Povolit pro Portál společnosti přístup k vašim kontaktům?

### <a name="where-it-appears"></a>Místo zobrazení

Zpráva **Povolit pro Portál společnosti přístup k vašim kontaktům?** se zobrazí, když uživatel během registrace svého zařízení klepne v aplikaci Portál společnosti na možnost **Zaregistrovat**.

### <a name="what-it-means"></a>Význam

Přijetím této výzvy uživatel umožní, aby služba Intune vytvořila pracovní účet a spravovala identitu služby Azure Active Directory, která je pro uživatele registrovaná na tomto zařízení.

> [!NOTE]
> **Společnost Microsoft nebude nikdy přistupovat k vašim kontaktům!** Text zprávy je pod kontrolu Googlu a nejde ho změnit.

### <a name="what-happens-if-users-deny-access"></a>Co se stane, když uživatel přístup zamítne

Pokud uživatel přístup zamítne, nebude zařízení v Intune zaregistrováno a nebude možné ho spravovat. Při druhém přihlášení k aplikaci Portál společnosti po zamítnutí přístupu se ve zprávě zobrazí zaškrtávací políčko **Příště se už neptat**, takže uživatel může zobrazování této výzvy zastavit.

Pokud uživatel povolí přístup, ale později ho zamítne, zobrazí se tato zpráva při přihlášení k aplikaci Portál společnosti, které následuje po registraci zařízení.

Pokud se uživatel později rozhodne povolit přístup, může přejít na **Nastavení** > **aplikace** > **portál společnosti** > **oprávnění** > **telefon**a zapnout ho.

### <a name="how-to-explain-this-to-your-users"></a>Jak to vysvětlit uživatelům

Nasměrujte uživatele na článek [Registrace zařízení s Androidem v Intune](../user-help/enroll-device-android-company-portal.md), kde najdou další informace.  

## <a name="allow-company-portal-to-access-photos-media-and-files-on-your-device"></a>Povolit pro Portál společnosti přístup k fotkám, médiím a souborům ve vašem zařízení?

### <a name="where-it-appears"></a>Místo zobrazení

Zpráva **Povolit pro Portál společnosti přístup k fotkám, médiím a souborům ve vašem zařízení?** se zobrazí, když uživatel klepnutím na **Odeslat data** odešle protokoly svému správci IT.

### <a name="what-it-means"></a>Význam

Přijetím této výzvy umožní uživatel zápis datových protokolů na SD kartu zařízení. Také se tím umožní přesun těchto protokolů pomocí USB kabelu.   

> [!NOTE]
> **Aplikace Portál společnosti nikdy nemá přístup k fotografiím, médiím a souborům uživatelů.** Text zprávy je pod kontrolu Googlu a nejde ho změnit.

### <a name="what-happens-if-users-deny-access"></a>Co se stane, když uživatel přístup zamítne

Pokud uživatel přístup zamítne, může pořád odesílat datové protokoly e-mailem, ale tyto protokoly se nezkopírují na SD kartu zařízení.

Při druhém přihlášení k aplikaci Portál společnosti po odepření přístupu se ve zprávě zobrazí zaškrtávací políčko **Příště se už neptat**, takže uživatel může určit, že se tato zpráva už nebude zobrazovat. Pokud uživatel povolí přístup, ale později ho zamítne, zobrazí se tato zpráva při příštím pokusu o odeslání protokolů. Pokud se ale uživatel později rozhodne povolit přístup, může přejít na **Nastavení** > **aplikace** > **portál společnosti** > **oprávnění** > **úložiště**a toto oprávnění zapnout.


### <a name="how-to-explain-this-to-your-users"></a>Jak to vysvětlit uživatelům

Nasměrujte uživatele na článek [Odeslání protokolů správci IT e-mailem](../user-help/send-logs-to-your-it-admin-by-email-android.md). 

## <a name="your-company-support-needs-to-give-you-access-to-company-resources"></a>Podpora vaší společnosti vám musí udělit přístup k prostředkům společnosti

### <a name="where-it-appears"></a>Místo zobrazení

Pokud jste aplikaci Portál společnosti nepřidali na seznam **Povolených aplikací** nebo **Aplikací s výjimkou** a uživatel se pokusí přihlásit, přihlášení selže. Zobrazí se tato zpráva:

> **Podpora vaší společnosti vám musí udělit přístup k prostředkům společnosti**  
> Vaše společnost k ochraně vašeho zařízení používá zásady Windows Information Protection. Podpora společnosti musí Portálu společnosti povolit k těmto prostředkům přístup.

### <a name="what-it-means"></a>Význam

Přidejte Portál společnosti do seznamu **povolených aplikací** nebo **aplikací s výjimkou** v zásadách ochrany aplikací pro Windows Information Protection (NV). Další informace najdete v článku [Vytvoření a nasazení zásady ochrany aplikací WIP (Windows Information Protection) u Intune](../apps/windows-information-protection-policy-create.md).

## <a name="approve-a-iosipados-company-app-line-of-business-app-on-your-iosipados-device"></a>Schválení aplikace společnosti pro iOS/iPadOS (obchodní aplikace) na zařízení se systémem iOS/iPadOS 

### <a name="where-it-appears"></a>Místo zobrazení

aplikace pro iOS vyvinuté ve vaší organizaci, které nejsou dostupné v obchodě s aplikacemi, nejsou ve výchozím nastavení důvěryhodné pro vaše zařízení. Když tyto aplikace nainstalujete pomocí Portál společnosti a spustíte aplikaci, zobrazí se následující zpráva:

![zpráva aplikace pro iOS – nedůvěryhodný vývojář pro podniky](./media/end-user-company-portal-messages/end-user-company-portal-messages-01.png)

### <a name="what-it-means"></a>Význam

Tato zpráva znamená, že budete muset změnit nastavení zařízení s iOS/iPadOS a schválit a nainstalovat aplikaci vyvinutou vaší společností na zařízení s iOS/iPadOS.

Když tyto aplikace nainstalujete pomocí Portál společnosti a aplikaci spustíte, po stažení proveďte následující kroky, abyste aplikaci schválili:

1. Po spuštění nainstalované firemní aplikace (obchodní aplikace) se zobrazí zpráva "nedůvěryhodná verze Enterprise Developer". <br>
   Stiskněte **Zrušit**.
2. Přejděte na **Nastavení** > **Obecné** > **Správa zařízení**.

   ![uživatelské rozhraní zařízení s iOS – Správa zařízení](./media/end-user-company-portal-messages/end-user-company-portal-messages-02.png)

3. Vyberte možnost **profil** > správy**podniková aplikace**.
4. Vyberte název vývojáře.
5. Stiskněte klávesu **Trust _název vývojáře_**.
6. Potvrďte aplikaci tak, že v místní zprávě pro instalaci aplikace vyberete **důvěřovat** .

   ![uživatelské rozhraní zařízení s iOS – důvěryhodná zpráva aplikace](./media/end-user-company-portal-messages/end-user-company-portal-messages-03.png)

    Měli byste být schopni spustit a používat podnikovou aplikaci.


## <a name="see-also"></a>Viz také
[Co říct koncovým uživatelům o používání služby Intune](end-user-educate.md)
