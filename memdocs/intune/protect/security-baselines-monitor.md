---
title: Ověření úspěšného nebo neúspěšného směrného plánu zabezpečení v Microsoft Intune – Azure | Microsoft Docs
description: Při nasazení standardních hodnot zabezpečení pro uživatele a zařízení v Microsoft Intune MDM se podívejte na stav Chyba, konflikt a úspěch. Podívejte se, jak řešit potíže s používáním klientských protokolů a funkce sestav v Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/21/2020
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
ms.openlocfilehash: 6623afcce55c6598ed69fdb78d35235e0fd39dc5
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2020
ms.locfileid: "90815357"
---
# <a name="monitor-security-baselines-and-profiles-in-microsoft-intune"></a>Sledujte standardní hodnoty a profily zabezpečení v Microsoft Intune

Intune poskytuje několik možností pro sledování standardních hodnot zabezpečení. Další možnosti:

- Sledujte základní hodnoty zabezpečení a všechna zařízení, která se shodují (nebo se neshodují) s doporučenými hodnotami.
- Monitorujte profil standardních hodnot zabezpečení, který se týká vašich uživatelů a zařízení.
- Podívejte se, jak se nastavení z vybraného profilu nastaví na vybrané zařízení.

Můžete si také prohlédnout *Konfigurace zabezpečení koncového bodu* , které se vztahují na jednotlivá zařízení, která zahrnují standardní hodnoty zabezpečení.

Další informace o této funkci najdete v tématu [základní hodnoty zabezpečení v Intune](security-baselines.md).

## <a name="monitor-the-baseline-and-your-devices"></a>Monitorování standardních hodnot a zařízení

Při sledování směrného plánu získáte přehled o stavu zabezpečení vašich zařízení na základě doporučení Microsoftu. Pokud si chcete zobrazit tyto přehledy, přihlaste se do [centra pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431), klikněte na směrné plány zabezpečení služby **Endpoint Security**  >  **Security baselines** a vyberte typ standardních hodnot zabezpečení, jako je *základní hodnota zabezpečení MDM*. Potom v podokně *verze* vyberte instanci profilu, pro kterou chcete zobrazit podrobnosti, a otevřete její podokno *přehledu* . 

V podokně *Přehled* se zobrazí dvě zobrazení stavu pro vybraný směrný plán:

- **Stav tabulka standardních hodnot zabezpečení** – tento graf zobrazuje nejdůležitější podrobnosti o stavu zařízení pro základní verzi. Dostupné podrobnosti:
  - **Odpovídá výchozímu směrnému plánu** – tento stav určuje, kdy se konfigurace zařízení shoduje s výchozí (neupravenou) konfigurací standardních hodnot.
  - **Odpovídá vlastnímu nastavení** – tento stav identifikuje, kdy konfigurace zařízení odpovídá přizpůsobené verzi směrného plánu, který jste nasadili. 
  - **Nesprávně nakonfigurovaný** – tento stav představuje souhrn, který reprezentuje tři stavové stavy ze zařízení: *Chyba*, *čeká*nebo *konflikt*. Tyto samostatné stavy jsou k dispozici v jiných zobrazeních, jako je například *standardní hodnota zabezpečení stav podle kategorie*, zobrazení seznamu, které se zobrazí pod tímto grafem.
  - **Netýká** se – tento stav představuje zařízení, které tyto zásady nemůžou přijmout. Například zásada aktualizuje nastavení specifické pro nejnovější verzi Windows, ale zařízení používá starší (starší) verzi, která toto nastavení nepodporuje. 

- **Základní hodnota zabezpečení stav podle kategorie** – zobrazení seznamu, které zobrazuje stav zařízení podle kategorie. V tomto zobrazení seznamu jsou k dispozici stejné podrobnosti jako *stav graf zabezpečení standardních hodnot* . Místo chybných *konfigurací* se ale zobrazí tři sloupce stavu stav, který je nesprávně nakonfigurovaný:

  - **Chyba**: zásadu se nepovedlo použít. Tato zpráva se obvykle zobrazí s chybovým kódem, který odkazuje na vysvětlení.
  - **Konflikt**: pro stejné zařízení se aplikují dvě nastavení a Intune ho nedokáže rozřadit do konfliktu. Správce by měl provést kontrolu.
  - **Čeká na vyřízení**: zařízení ještě není zaregistrované v Intune, aby bylo možné tyto zásady přijmout.
 
Když přejdete na dva předchozí zobrazení, můžete zobrazit následující podrobnosti o stavu nastavení a zobrazeních seznamu stavů zařízení:

- **Úspěch**: zásada se použije.
- **Chyba**: zásadu se nepovedlo použít. Tato zpráva se obvykle zobrazí s chybovým kódem, který odkazuje na vysvětlení.
- **Konflikt**: pro stejné zařízení se aplikují dvě nastavení a Intune ho nedokáže rozřadit do konfliktu. Správce by měl provést kontrolu.
- **Čeká na vyřízení**: zařízení ještě není zaregistrované v Intune, aby bylo možné tyto zásady přijmout.
- **Nedá se použít**: zařízení nemůže tuto zásadu přijmout. Například zásada aktualizuje nastavení specifické pro nejnovější verzi Windows, ale zařízení používá starší (starší) verzi, která toto nastavení nepodporuje.

V zobrazení *verze* můžete vybrat **stav zařízení**. V zobrazení stav zařízení se zobrazí seznam zařízení, která obdrží tyto standardní hodnoty, a obsahuje následující podrobnosti:
- *Hlavní název uživatele* – zobrazuje profil uživatele přidružený ke směrnému plánu na zařízení. 
- *Zabezpečení standardních hodnot stav* – v tomto sloupci se zobrazuje stav zařízení:
  - **Úspěch**: zásada se použije.
  - **Chyba**: zásadu se nepovedlo použít. Tato zpráva se obvykle zobrazí s chybovým kódem, který odkazuje na vysvětlení.
  - **Konflikt**: pro stejné zařízení se aplikují dvě nastavení a Intune ho nedokáže rozřadit do konfliktu. Správce by měl provést kontrolu.
  - **Čeká na vyřízení**: zařízení ještě není zaregistrované v Intune, aby bylo možné tyto zásady přijmout.
  - **Nedá se použít**: zařízení nemůže tuto zásadu přijmout. Například zásada aktualizuje nastavení specifické pro nejnovější verzi Windows, ale zařízení používá starší (starší) verzi, která toto nastavení nepodporuje.
- *Poslední vrácení se změnami* – při posledním přijetí stavu ze zařízení.

> [!TIP]  
> Po prvním přiřazení směrného plánu trvá zobrazení dat až 24 hodin. Pozdější změny se projeví až po šesti hodinách.

## <a name="monitor-the-profile"></a>Monitorování profilu

Monitorování profilu poskytuje přehled o stavu nasazení vašich zařízení, ale ne stav zabezpečení na základě základních doporučení.

1. V Intune vyberte **Endpoint security**  >  **standardní hodnoty zabezpečení**Endpoint Security, *Vyberte typ standardních hodnot zabezpečení, jako je například směrný plán zabezpečení MDM*  >  *Vyberte instanci těchto vlastností směrného plánu*  >  **Properties**.

2. Ve *vlastnostech* směrného plánu rozbalte **Nastavení** pro procházení a zobrazte všechny kategorie nastavení a jednotlivá nastavení ve standardních hodnotách, včetně jejich konfigurace pro tuto instanci směrného plánu.

   ![Obrázek obrazovky znázorňující zobrazení nastavení](./media/security-baselines-monitor/manage-settings.png)

3. Pomocí možností **monitorování** můžete zobrazit stav nasazení profilu na jednotlivých zařízeních, stav pro každého uživatele a stav nastavení z instance směrného plánu:

   ![Zobrazit různé možnosti monitorování pro profil standardních hodnot zabezpečení](./media/security-baselines-monitor/monitor-status-options.png)

## <a name="resolve-conflicts-for-security-baselines"></a>Řešení konfliktů pro standardní hodnoty zabezpečení

Pokud chcete vyřešit konflikt nebo chybu nastavení v profilech standardních hodnot zabezpečení nebo zásadách zabezpečení koncového bodu, Prohlédněte si **konfiguraci zabezpečení koncového bodu** zařízení.  Toto zobrazení založené na zařízení vám pomůže zjistit, kde profily a zásady obsahují nastavení, která zastavují stav konflikt nebo chyba. 

Informace o konfliktních nastaveních a chybách můžete získat pomocí dvou cest v centru pro správu Microsoft Endpoint Manageru:

- Zabezpečení koncového **bodu**  >  **Standardní hodnoty zabezpečení**  >  *Vyberte typ*  >  směrného plánu. **Profily**  >  *Vyberte instanci*  >  standardních hodnot. **Stav zařízení**  >  Konfigurace zabezpečení koncového **bodu**  >  *nastavení, které zobrazuje konflikty nebo chyby*.
- **Zařízení**  >  *Vyberte zařízení*  >  . Konfigurace zabezpečení koncového **bodu**  >  *Vyberte profil nebo směrný plán*  >  . *Vyberte nastavení ze seznamu nastavení, které zobrazuje konflikty nebo chyby*.

V zobrazení **Konfigurace zabezpečení koncového bodu** zařízení Intune zobrazuje každý základní profil a zásadu z zabezpečení koncového bodu, které je přiřazené k tomuto zařízení. Toto zobrazení také identifikuje přidružený hlavní název uživatele pro každou položku a stav profilu standardních hodnot nebo zásad. Profil nebo zásada se můžou v zařízení objevit několikrát, jednou pro každý jiný hlavní název uživatele, který je k němu přidružený. 

<!-- pending
The **Baseline status** represents the worst available status from any applicable setting in that profile or policy. For example, if on the device a single setting from a profile is found to be in conflict while the rest of the baselines’ settings are successful, the *Baseline status* is set to *Conflict*. 

The available status from best to worst:

- **Success** - The setting on the device matches the value as configured in the profile, and there are no conflicting configurations. This is either a default and recommended value, or a custom value specified by an administrator when the profile was configured.
- **Error** - The profile and settings failed to apply.
- **Conflict** - The setting conflicts with another instance of the setting from another policy, has an error, or is pending an update. This setting isn’t sent to the device until the conflict is resolved.
--> 

### <a name="drill-in-to-identify-and-resolve-conflicts"></a>Procházení k identifikaci a řešení konfliktů

1. Při prohlížení konfigurace zabezpečení koncového bodu v zařízení vyberte profil, který chcete zobrazit, a získejte další informace o problému, který má za následek konflikt nebo stav chyby.

   Když přejdete k podrobnostem, Intune zobrazí seznam nastavení pro tento profil, který obsahuje všechna nastavení, která nebyla nastavena jako *nenakonfigurovaná*, a stav tohoto nastavení. Zobrazení lze uspořádat podle kategorie, názvu nastavení nebo stavu. Pokud filtrujete stav, můžete se rychle zaměřit jenom na nastavení, která mají chybu nebo konflikt.  

2. Pokud chcete zobrazit podrobnosti o konkrétním nastavení, vyberte ho a otevřete tak podokno **Podrobnosti nastavení** . V tomto podokně se zobrazí:
   - Nastavení – název nastavení.
   - State – stav nastavení na zařízení. 
   - Zdrojový profil – Toto je seznam každého profilu zabezpečení koncového bodu nebo standardní hodnoty zabezpečení, který konfiguruje stejné nastavení, ale s jinou hodnotou.

   > [!TIP]  
   > Na rozdíl od konfiguračních profilů zařízení neposkytují profily zabezpečení Endpoint kódy chyb ani související podrobnosti.

3. Chcete-li znovu nakonfigurovat konfliktní profily, vyberte záznam ze seznamu **Profil zdroje** a otevřete tak zobrazení konfigurace těchto profilů. V zobrazení konfigurace profilu můžete zkontrolovat a upravit nastavení v tomto profilu pro odstranění konfliktu.

## <a name="view-settings-from-profiles-that-apply-to-a-device"></a>Zobrazit nastavení z profilů, které se vztahují k zařízení

Můžete vybrat profil pro standardní hodnoty zabezpečení a přejít k podrobnostem a zobrazit si seznam nastavení z tohoto profilu, která se vztahují na jednotlivá zařízení.  Pokud chcete tento seznam zobrazit, Projděte si základní hodnoty zabezpečení **Endpoint**Security.  >  **Security baselines**  >  *Vyberte typ standardních hodnot*zabezpečení,  >  *Vyberte profil, ve kterém chcete zobrazit*  >  **stav zařízení**. Seznam můžete zobrazit také tak, že kliknete na **zabezpečení koncového bodu**  >  **všechna zařízení**  >  *Vybrat*  >  **Konfigurace zabezpečení koncového bodu**zařízení  >  *Vybrat základní verzi*.

Po výběru zařízení se v centru pro správu Microsoft Endpoint Manageru zobrazí seznam nastavení z tohoto profilu, který obsahuje kategorii, ze které se nastavení nachází, a stav konfigurace na zařízení. Stavy konfigurace obsahují tyto hodnoty:

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


