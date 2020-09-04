---
title: Aplikace v Portálu společnosti
titleSuffix: Configuration Manager
description: Poskytněte konzistentní uživatelské prostředí pro spoluspravovaná zařízení, která budou používat aplikaci Portál společnosti.
ms.date: 09/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: how-to
ms.assetid: 26456bb7-f46b-4d8d-bb0b-e3fd9a52fe14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cd49546e49d6964cfe37b0b13e1abe9175f4aa0e
ms.sourcegitcommit: 7b656712cc9340d18211c7754cb99bcaae91b0ca
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/03/2020
ms.locfileid: "89432553"
---
# <a name="use-the-company-portal-app-on-co-managed-devices"></a>Použití aplikace Portál společnosti na spoluspravovaných zařízeních

*Platí pro: Configuration Manager (Current Branch)*

<!--CMADO-3601237,INADO-4297660-->

Počínaje verzí 2006 je Portál společnosti nyní prostředí portálu pro aplikace pro různé platformy pro Microsoft Endpoint Manager. Když nakonfigurujete spoluspravovaná zařízení, aby se taky používala Portál společnosti, můžete na všech zařízeních zajistit konzistentní uživatelské prostředí.

Portál společnosti podporuje následující akce:

- Spusťte aplikaci Portál společnosti v souběžně spravovaných zařízeních a přihlaste se pomocí jednotného přihlašování Azure Active Directory (Azure AD) s jednotným přihlašováním (SSO).
- Zobrazit dostupné a nainstalované aplikace Configuration Manager v Portál společnosti spolu s aplikacemi Intune.
- Nainstalovat dostupné Configuration Manager aplikace z Portál společnosti a získat informace o stavu instalace.

:::image type="content" source="media/3601237-company-portal.png" alt-text="Portál společnosti s aplikací z Configuration Manager" lightbox="media/3601237-company-portal.png":::

Chování Portál společnosti závisí na konfiguraci úloh spolusprávy:

| Úloha | Nastavení | Chování |
|----------|---------|----------|
| Klientské aplikace | **Configuration Manager** | Můžete vidět jenom Configuration Manager klientských aplikacích. |
| Klientské aplikace | **Pilotní nasazení Intune** nebo **Intune** | Můžete vidět Configuration Manager i klientské aplikace Intune. |
| Aplikace pro Office Klikni a spusť | **Configuration Manager** | Můžete zobrazit jenom aplikace Configuration Manager Office Klikni a spusť. |
| Aplikace pro Office Klikni a spusť | **Pilotní nasazení Intune** nebo **Intune** | Vidíte pouze aplikace pro Intune Office Klikni a spusť. |

Další informace najdete v následujících článcích:

- [Diagram pro úlohy aplikací](workloads.md#diagram-for-app-workloads)

- [Postup přepnutí úloh Configuration Manager do Intune](how-to-switch-workloads.md)

## <a name="prerequisites"></a>Požadavky

- Configuration Manager aktuální větve verze 2006 nebo novější <sup>([Viz časté otázky](#bkmk_ver-prereq))</sup>

- Portál společnosti verze aplikace 11.0.8980.0 nebo novější

- Windows 10 verze 1803 nebo novější:

  - Zaregistrováno do [spolusprávy](how-to-enable.md)

  - Přístup k [koncovým bodům Internetu pro Intune](../../intune/fundamentals/intune-endpoints.md)

- Uživatelské účty, které se přihlásí k těmto zařízením, vyžadují následující konfigurace:

  - Identita Azure AD

  - Má přiřazenou licenci Intune.

## <a name="configure-and-deploy"></a>Konfigurace a nasazení

### <a name="configuration-manager-client-settings"></a>Configuration Manager nastavení klienta

Chcete-li zajistit, že uživatelé budou dostávat pouze oznámení od Portál společnosti, nakonfigurujte Configuration Manager nastavení klienta. Ve skupině **Centrum softwaru** nastavení zařízení změňte **Výběr portálu user Portal** na **portál společnosti**.

Další informace o nastavení klienta najdete v následujících článcích:

- [Postup konfigurace nastavení klienta](../core/clients/deploy/configure-client-settings.md)
- [O nastavení klientů](../core/clients/deploy/about-client-settings.md#software-center)

### <a name="deploy-the-company-portal-app"></a>Nasazení aplikace Portál společnosti

- Uživatelé můžou aplikaci Portál společnosti z [Microsoft Store](https://www.microsoft.com/p/company-portal/9wzdncrfj3pz?activetab=pivot:overviewtab)nainstalovat ručně.

- Aby bylo možné aplikaci na spoluspravovaných zařízeních vyžadovat, závisí proces nasazení na stavu úlohy spolusprávy [klientských aplikací](workloads.md#client-apps) :

  - Pokud jsou úlohy klientských aplikací v Configuration Manager, [vytvořte a nasaďte aplikaci pomocí Configuration Manager](../apps/get-started/create-and-deploy-an-application.md). Stáhněte si offline Portál společnosti aplikaci z [Microsoft Store pro firmy](https://www.microsoft.com/business-store).

  - Pokud jsou úlohy klientských aplikací v Intune, můžete je nasadit pomocí Configuration Manager nebo [přidat portál společnosti aplikaci pro Windows 10 pomocí Microsoft Intune](../../intune/apps/store-apps-company-portal-app.md).

Další informace o brandingu Portál společnosti pro vaši organizaci najdete v tématu [přizpůsobení aplikace Portál společnosti Intune](../../intune/apps/company-portal-app.md).

## <a name="use-the-company-portal"></a>Použití Portál společnosti

1. Z nabídky Start spusťte Portál společnosti. Aktuálně přihlášený uživatel se automaticky přihlásí k Portál společnosti na základě jeho identity Azure AD.

1. Vyberte stránku **aplikace** . V seznamu byste měli vidět Configuration Manager aplikace.

1. Vyberte jednu z aplikací nasazených z Configuration Manager.

    - Na kartě **Přehled** se zobrazují podrobnosti o aplikaci, jako je velikost, verze a datum publikování.

    - Pokud chcete zjistit, že Configuration Manager je služba správy pro tuto aplikaci, přepněte na kartu **Další informace** .

    - Pokud chcete aplikaci nainstalovat, vyberte **nainstalovat**. Portál společnosti zobrazuje stav instalace a po dokončení se zobrazí oznámení.

    - Pokud je aplikace už nainstalovaná, vyberte **odinstalovat** , aby se aplikace odebrala.

    - Vyberte tři tečky ( `...` ) pro další akce, například **opravit** a **sdílet**.

        :::image type="content" source="media/3601237-company-portal-app-details.png" alt-text="Configuration Manager aplikace s podrobnostmi Portál společnosti" lightbox="media/3601237-company-portal-app-details.png":::

    - Po instalaci webové aplikace Configuration Manager vyberte nabídku se třemi tečkami a pak vyberte **otevřít v prohlížeči** a spusťte webovou aplikaci.

    - Pokud se Configuration Manager aplikace nedokáže nainstalovat se známým kódem chyby, vyberte odkaz na stav selhání a vyhledejte kód chyby.

Pokud změníte nastavení klienta pro Portál společnosti, když uživatel vybere Configuration Manager oznámení, spustí Portál společnosti. Pokud je oznámení pro scénář, který Portál společnosti nepodporuje, pak se při výběru oznámení spustí Centrum softwaru.

Pokud chcete pomoct řešit problémy s instalací aplikací Configuration Manager, přečtěte si část **podpora &** v tématu portál společnosti. Když použijete možnost **získat nápovědu** , můžete v rámci žádosti odeslat soubory protokolu Configuration Manager.

## <a name="frequently-asked-questions-faq"></a>Nejčastější dotazy

### <a name="im-using-configuration-manager-version-2002-why-is-the-new-company-portal-showing-configuration-manager-apps"></a><a name="bkmk_ver-prereq"></a> Používám Configuration Manager verze 2002, proč je nové Portál společnosti zobrazuje Configuration Manager aplikace?

Portál společnosti verze 11.0.8980.0 nebo novější zobrazuje Configuration Manager nasazené aplikace pro všechny spoluspravované klienty, kteří je používají. Předpokladem je Configuration Manager verze 2006, protože přidává nastavení klienta pro řízení oznámení. Pokud nainstalujete Portál společnosti do spoluspravovaného zařízení starší verze nebo nenakonfigurujete nastavení klienta, uživatelé uvidí oznámení z obou portálů. Toto prostředí může být matoucí pro uživatele.

### <a name="does-company-portal-support-applications-deployed-as-software-updates-from-configuration-manager"></a>Podporuje Portál společnosti aplikace nasazené jako aktualizace softwaru z Configuration Manager?

Yes. Pokud nasadíte aplikaci pomocí funkce aktualizace softwaru, klient je považuje za shodný s tím, že se uživatelské prostředí Portál společnosti nebo centra softwaru.

### <a name="can-users-repair-uninstall-and-update-configuration-manager-apps-in-company-portal"></a>Můžou uživatelé opravovat, odinstalovat a aktualizovat aplikace Configuration Manager v Portál společnosti?

Yes. Pokud nakonfigurujete aplikaci Configuration Manager tak, aby podporovala tyto další akce, Portál společnosti podporuje opravu, odinstalaci a aktualizaci.

## <a name="known-issues"></a>Známé problémy

Následující funkce centra softwaru nejsou aktuálně k dispozici v Portál společnosti:

- Některé informace o aplikaci, například pokud je potřeba restartování nebo odhadovaná doba instalace

- [Skupiny aplikací](../apps/deploy-use/create-app-groups.md)

Další známé problémy:

- Pokud nasadíte stejnou aplikaci z Configuration Manager i Intune, zobrazí se dvakrát v Portál společnosti.

- Při hledání Portál společnosti se aplikace Intune vždycky zobrazí před Configuration Manager aplikace.

## <a name="next-steps"></a>Další kroky

[Postup přepnutí úloh Configuration Manager do Intune](how-to-switch-workloads.md)

[Jak přizpůsobit aplikaci Portál společnosti Intune](../../intune/apps/company-portal-app.md)
