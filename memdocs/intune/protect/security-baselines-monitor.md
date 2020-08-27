---
title: Ověření úspěšného nebo neúspěšného směrného plánu zabezpečení v Microsoft Intune – Azure | Microsoft Docs
description: Při nasazení standardních hodnot zabezpečení pro uživatele a zařízení v Microsoft Intune MDM se podívejte na stav Chyba, konflikt a úspěch. Podívejte se, jak řešit potíže s používáním klientských protokolů a funkce sestav v Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1ccf9801c7a5977485c6c1864a69be2e46a4af55
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914867"
---
# <a name="monitor-security-baselines-and-profiles-in-microsoft-intune"></a>Sledujte standardní hodnoty a profily zabezpečení v Microsoft Intune

Intune nabízí několik možností monitorování standardních hodnot zabezpečení. Další možnosti:

- Sledujte základní hodnoty zabezpečení a všechna zařízení, která se shodují (nebo se neshodují) s doporučenými hodnotami.
- Monitorujte profil standardních hodnot zabezpečení, který se týká vašich uživatelů a zařízení.
- Podívejte se, jak se nastavení z vybraného profilu nastaví na vybrané zařízení.

Můžete si také prohlédnout *Konfigurace zabezpečení koncového bodu* , které se vztahují na jednotlivá zařízení, která zahrnují standardní hodnoty zabezpečení.

Tento článek vás provede těmito možnostmi monitorování.

[Směrné plány zabezpečení v Intune](security-baselines.md) poskytují další podrobnosti o funkci směrného plánu zabezpečení v Microsoft Intune.

## <a name="monitor-the-baseline-and-your-devices"></a>Monitorování standardních hodnot a zařízení

Při sledování směrného plánu získáte přehled o stavu zabezpečení vašich zařízení na základě doporučení Microsoftu. Pokud si chcete zobrazit tyto přehledy, přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431), klikněte na směrné plány zabezpečení služby **Endpoint Security**  >  **Security baselines** a vyberte typ standardních hodnot zabezpečení, jako je *základní hodnota zabezpečení MDM*. Pak v podokně *profil* vyberte instanci profilu, pro kterou chcete zobrazit podrobnosti. Otevře se okno *vlastnosti* profilů, kde můžete vybrat libovolnou sestavu profilu z části *monitorování* . 

Po prvním přiřazení směrného plánu trvá zobrazení dat až 24 hodin. Pozdější změny se projeví až po šesti hodinách.

Při přechodu k sestavám a zařízením jsou k dispozici různé podrobnosti.

<!-- UI is changing, unclear how yet: 


- **Device view** – A summary of how many devices are in each status category for the baseline.
- **Per-category** - A view that displays each category in the baseline and includes the percentage of devices for each status group for each baseline category.

Each device is represented by one of the following statuses (used in the *device* view and also the *per-category* views):

- **Matches baseline** - All the settings in the baseline match the recommended settings.
- **Does not match baseline** - One or more settings in the baseline were modified from their default values in the original baseline. The default values in each security baseline are the recommended values for that baseline.

  > [!NOTE]
  > When you create or edit a baseline profile, any change that is made to a default value or configuration setting causes a *Does not match baseline* status to occur. For help to determine the settings that were changed, contact Microsoft Support. 

- **Misconfigured** - At least one setting isn't correctly configured. This status means that the setting is in a conflict, error, or pending state.
- **Not applicable** - At least one setting isn't applicable and isn't applied.

### Device view

The Overview pane displays a chart-based summary of how many devices have a specific status for the baseline; **Security baseline posture for assigned Windows 10 devices**.

![Check the status of the devices](./media/security-baselines-monitor/overview.png)

When a device has different status from different categories in the baseline, the device is represented by a single status. The status that represents the device is taken from the following order of precedence: **Misconfigured**, **Does not match baseline**, **Not applicable**, **Matches baseline**.

For example, if a device has a setting that's classified as *misconfigured* and one or more settings that are classified as *Does not match baseline*, the device is classified as *Misconfigured*.

You can click on the chart to drill through and view a list of devices with various statuses. You can then select individual devices from that list to view details about individual devices. For example:

- Select **Device configuration** > Select the profile with an Error state:

  ![View the status of a profile](./media/security-baselines-monitor/device-configuration-profile-list.png)

- Select the Error profile. A list of all settings in the profile, and their state is shown. Now, you can scroll to find the setting causing the error:

  ![See the setting causing the error](./media/security-baselines-monitor/profile-with-error-status.png)

Use this reporting to see any settings in a profile that are causing an issue. Also get more details of policies and profiles deployed to devices.

> [!NOTE]
> When a property is set to **Not configured** in the baseline, the setting is ignored, and no restrictions are enforced. The property isn't shown in any reporting.

### Per category view

The Overview pane displays a per-category chart for the baseline named **Security baseline posture by category**.  This view displays each category from the baseline, and identifies the percentage of devices that fall into a status classification for each of those categories.

![Per-Category view of status](./media/security-baselines-monitor/monitor-baseline-per-category.png)

Status for **Matches baseline** doesn't display until 100% of devices report that status for the category.

You can sort the by-category view by each column, by selecting up-down arrow icon at the top of the column.
-->

## <a name="monitor-the-profile"></a>Monitorování profilu

Monitorování profilu poskytuje přehled o stavu nasazení vašich zařízení, ale ne stav zabezpečení na základě základních doporučení.

1. V Intune vyberte **standardní hodnoty zabezpečení** > výběrem směrného plánu otevřete jeho podokno *profily* .

<!-- More churn  
2. Select a profile. In **Overview**, the image shows how many devices and users have this profile assigned:

   ![See how many devices and users are assigned the security baselines profile](./media/security-baselines-monitor/existing-profile-overview.png)
--> 
3. V části **Spravovat**  >  **vlastnosti**se zobrazí seznam všech nastavení ve standardních hodnotách. Můžete také změnit kterékoli z těchto nastavení:

   ![Zobrazit a aktualizovat nastavení v profilu standardních hodnot zabezpečení](./media/security-baselines-monitor/manage-settings.png)

4. V okně **monitor**můžete zobrazit stav nasazení profilu na jednotlivých zařízeních, stav pro každého uživatele a stav každého nastavení ve standardních hodnotách:

   ![Zobrazit různé možnosti monitorování pro profil standardních hodnot zabezpečení](./media/security-baselines-monitor/monitor-status-options.png)

## <a name="view-settings-from-profiles-that-apply-to-a-device"></a>Zobrazit nastavení z profilů, které se vztahují k zařízení

Můžete vybrat profil pro standardní hodnoty zabezpečení a přejít k podrobnostem a zobrazit si seznam nastavení z tohoto profilu, která se vztahují na jednotlivá zařízení.  Pokud chcete tento seznam zobrazit, Projděte si základní hodnoty zabezpečení **Endpoint**Security.  >  **Security baselines**  >  *Vyberte typ standardních hodnot*zabezpečení,  >  *Vyberte profil, ve kterém chcete zobrazit*  >  **stav zařízení**. Seznam můžete zobrazit také tak, že kliknete na **zabezpečení koncového bodu**  >  **všechna zařízení**  >  *Vybrat*  >  **Konfigurace zabezpečení koncového bodu**zařízení  >  *Vybrat základní verzi*.

Po výběru zařízení se v centru pro správu Microsoft Endpoint Manageru zobrazí seznam nastavení z tohoto profilu, včetně kategorie, ze které se nastavení nachází, a stavu konfigurace na zařízení. Stavy konfigurace obsahují tyto hodnoty:

- **Úspěch** – nastavení zařízení odpovídá hodnotě nakonfigurované v profilu. Toto je výchozí nastavení a doporučená hodnota nebo vlastní hodnota zadaná správcem při konfiguraci profilu.
- **Konflikt** – nastavení je v konfliktu s jinou zásadou, obsahuje chybu nebo čeká na aktualizaci.
- **Nelze použít** – nastavení není profilem použito.

> [!NOTE]
> Hodnoty stavu pro nastavení se aktualizují v budoucí verzi, aby bylo možné získat podrobnější informace.

## <a name="view-endpoint-security-configurations-per-device"></a>Zobrazit konfigurace zabezpečení Endpoint na zařízení

Podívejte se na podrobnosti o konfiguracích zabezpečení, které se vztahují na jednotlivá zařízení, která vám pomůžou izolovat nesprávně nakonfigurované nastavení.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. V části **zařízení**  >  **všechna zařízení** a vyberte zařízení, které chcete zobrazit.

3. V kategorii *monitor* vyberte možnost **Konfigurace zabezpečení koncového bodu** a zobrazte seznam konfigurací zabezpečení, které se vztahují k danému zařízení.

4. Můžete vybrat konfiguraci zabezpečení koncového bodu pro přechod k podrobnostem a zobrazit další podrobnosti o vyhodnocení této konfigurace zabezpečení na zařízení.

## <a name="troubleshoot-using-per-setting-status"></a>Řešení potíží s použitím stavu podle nastavení

Nasadili jste základní úroveň zabezpečení, ale stav nasazení zobrazuje chybu. Následující kroky vám poskytnou pokyny k řešení této chyby.

1. V Intune vyberte **standardní hodnoty zabezpečení** > vyberte **profily**> směrného plánu.

2. Vyberte profil > pod položkou **monitorovat**  >  **stav podle nastavení**.

3. V tabulce jsou uvedena všechna nastavení a stav jednotlivých nastavení. Pokud chcete zobrazit nastavení, které způsobuje chybu, vyberte sloupec **Chyba** nebo sloupec **konfliktů** .

### <a name="mdm-diagnostic-information"></a>Diagnostické informace MDM

Nyní znáte problematické nastavení. V dalším kroku zjistíte, proč toto nastavení způsobuje chybu nebo konflikt.

Na zařízeních s Windows 10 je k dispozici integrovaná sestava diagnostické informace MDM. Tato sestava obsahuje výchozí hodnoty, aktuální hodnoty, seznam těchto zásad, informace o tom, jestli se nasadí do zařízení nebo uživatele, a další. Tato sestava vám pomůže zjistit, proč nastavení způsobuje konflikt nebo chybu.

1. V zařízení přejděte na **Nastavení**  >  **účty**  >  **přístup do práce nebo do školy**.

2. Vyberte účet > **informace**  >  **Upřesnit diagnostickou sestavu**  >  **vytvořit sestavu**.

3. Vyberte **exportovat**a vygenerovaný soubor otevřete.

4. V sestavě vyhledejte nastavení chyba nebo konflikt v různých částech sestavy.

  Podívejte se například na oddíl **zaregistrované zdrojové konfigurace a cílové prostředky** nebo na oddíl **nespravované zásady** . Můžete získat představu o tom, proč způsobuje chybu nebo konflikt.

[Diagnostika selhání MDM ve Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10) poskytuje další informace o této předdefinované sestavě.

> [!TIP]
>
> - Některá nastavení také uvádějí identifikátor GUID. Tento identifikátor GUID můžete vyhledat v místním registru (Regedit) pro všechny hodnoty sady.
> - Protokoly Prohlížeč událostí mohou také obsahovat informace o problémech s problematickým nastavením (**Event viewer**  >  **protokoly aplikací a služeb**v prohlížeči událostí  >  **Microsoft**  >  **Windows**  >  **DeviceManagement-Enterprise-Diagnostics-Provider**  >  **admin**).

## <a name="next-steps"></a>Další kroky

- [Další informace o standardních hodnotách zabezpečení](security-baselines.md)
- [Vyhnout se konfliktům](security-baselines.md#avoid-conflicts)
- [Sledování profilů zařízení](../configuration/device-profile-monitor.md) 
- [Běžné problémy a jejich řešení](../configuration/device-profile-troubleshoot.md).
- [Řešení potíží se zásadami a profily v Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)