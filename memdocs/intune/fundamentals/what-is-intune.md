---
title: Co je Microsoft Intune – Azure | Microsoft Docs
description: Přečtěte si, jak Microsoft Intune je komponentou správy mobilních zařízení (MDM) a správy mobilních aplikací (MAM) v řešení Enterprise Mobility + Security a jak vám pomůže chránit podniková data.
keywords: co je Intune
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 06/23/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3b4e778d-ac13-4c23-974f-5122f74626bc
ms.reviewer: pmay
ms.suite: ems
search.appverid: MET150
ms.custom: get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6e8fa8db5e7a960677eeafaf03ca43662da9b8d3
ms.sourcegitcommit: d6cbd1a1c2926064e074e3431471534eb142c905
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/11/2020
ms.locfileid: "90012642"
---
# <a name="microsoft-intune-is-an-mdm-and-mam-provider-for-your-devices"></a>Microsoft Intune je poskytovatel MDM a MAM pro vaše zařízení.

Microsoft Intune je cloudová služba, která se zaměřuje na správu mobilních zařízení (MDM) a správu mobilních aplikací (MAM). Můžete řídit, jak se používají zařízení vaší organizace, včetně mobilních telefonů, tabletů a notebooků. Můžete taky nakonfigurovat konkrétní zásady pro řízení aplikací. Můžete například zabránit posílání e-mailů lidem mimo vaši organizaci. Intune také umožňuje lidem ve vaší organizaci používat jejich osobní zařízení pro školní nebo pracovní práci. V osobních zařízeních Intune pomáhá zajistit, aby data vaší organizace zůstala chráněná a mohla izolovat data organizace od osobních dat.

Intune je součástí [sady Microsoft Enterprise mobility + Securitye (EMS)](https://www.microsoft.com/microsoft-365/enterprise-mobility-security). Intune se integruje s Azure Active Directory (Azure AD), která řídí, kdo má přístup a k čemu mají přístup. Integruje se také s Azure Information Protection pro ochranu dat. Dá se použít s Microsoft 365ovou sadou produktů. Do zařízení můžete například nasadit Microsoft teams, OneNote a jiné aplikace Microsoft 365. Tato funkce umožňuje lidem ve vaší organizaci zvýšit produktivitu na všech svých zařízeních a současně chránit informace vaší organizace pomocí zásad, které vytvoříte.

[![Obrázek architektury Intune](./media/what-is-intune/intunearch_sm.png )](./media/what-is-intune/intunearchitecture.svg#lightbox)

Intune vám umožňuje:

- Vyberte možnost 100% Cloud s Intune nebo se [spoluspravuje](/configmgr/comanage/overview) pomocí Configuration Manager a Intune.
- Nastavte pravidla a nakonfigurujte nastavení na osobních zařízeních a na zařízeních vlastněných organizací pro přístup k datům a sítím.
- Nasaďte a ověřte aplikace na zařízeních – místně a mobilní zařízení.
- Zabezpečte informace společnosti tím, že řídíte způsob přístupu uživatelů k informacím a jejich sdílení.
- Ujistěte se, že zařízení a aplikace vyhovují vašim požadavkům na zabezpečení.

## <a name="manage-devices"></a>Správa zařízení

V Intune můžete zařízení spravovat pomocí přístupu, který je pro vás nejvhodnější. U zařízení vlastněných organizací budete chtít mít oprávnění k úplnému řízení na zařízeních, včetně nastavení, funkcí a zabezpečení. V tomto postupu se zařízení a uživatelé těchto zařízení registrují v Intune. Po registraci obdrží vaše pravidla a nastavení prostřednictvím zásad nakonfigurovaných v Intune. Můžete například nastavit požadavky na heslo a PIN kód, vytvořit připojení k síti VPN, nastavit ochranu před hrozbami a další.

Pro osobní zařízení nebo vlastní zařízení (BYOD) nemusí uživatelé chtít, aby správci organizace měli oprávnění k úplnému řízení. V tomto postupu Poskytněte uživatelům možnosti. Například uživatelé [registrují](../enrollment/device-enrollment.md) svá zařízení, pokud chtějí mít úplný přístup k prostředkům vaší organizace. Nebo pokud mají tito uživatelé přístup jenom k e-mailu nebo Microsoft teams, použijte zásady ochrany aplikací, které pro používání těchto aplikací vyžadují vícefaktorové ověřování (MFA).

Když jsou zařízení zaregistrovaná a spravovaná v Intune, můžou správci:

- Podívejte se na zaregistrovaná zařízení a získejte inventář zařízení, která přistupují k prostředkům organizace.
- Nakonfigurujte zařízení tak, aby splňovala vaše standardy zabezpečení a stavu. Například budete chtít zablokovat zařízení s jailbreakem.
- Nabízení certifikátů do zařízení, aby uživatelé mohli snadno přistupovat k síti Wi-Fi nebo k připojení k síti pomocí sítě VPN.
- Viz sestavy pro uživatele a zařízení, které jsou kompatibilní a které nedodržují předpisy.
- Odebrat data organizace, pokud dojde ke ztrátě, odcizení nebo už nepoužitému zařízení.

**Online prostředky**:

- [Co je registrace zařízení?](../enrollment/device-enrollment.md)

- [Použití funkcí a nastavení v zařízeních pomocí profilů zařízení](../configuration/device-profiles.md)

- [Ochrana zařízení pomocí Microsoft Intune](../protect/device-protect.md)

### <a name="try-the-interactive-guide"></a>Vyzkoušejte interaktivní příručku
Interaktivní příručka pro [správu zařízení pomocí Microsoft Endpoint Manageru](https://mslearn.cloudguides.com/guides/Manage%20devices%20with%20Microsoft%20Endpoint%20Manager) vás provede centrem pro správu Microsoft Endpoint Manageru, který vám ukáže, jak spravovat a chránit mobilní a desktopové aplikace.</br></br>

<div align=”center”>
<iframe allowfullscreen width="95%" height="450" src="https://mslearn.cloudguides.com/guides/Manage%20devices%20with%20Microsoft%20Endpoint%20Manager" frameborder="0" scrolling="no" loading="lazy" importance="low"/></iframe>
</div>

## <a name="manage-apps"></a>Správa aplikací

Správa mobilních aplikací (MAM) v Intune je navržená tak, aby chránila data organizace na úrovni aplikace, včetně vlastních aplikací a aplikací pro Store. Správa aplikací se dá použít na zařízeních vlastněných organizací a na osobních zařízeních.

Když se aplikace spravují v Intune, můžou správci:

- Přidávání a přiřazování mobilních aplikací ke skupinám uživatelů a zařízením, včetně uživatelů v konkrétních skupinách, zařízení v určitých skupinách a dalších.
- Nakonfigurujte aplikace tak, aby se spouštěly nebo spouštěly s povoleným konkrétním nastavením, a aktualizujte existující aplikace, které už jsou v zařízení.
- Podívejte se na sestavy, které aplikace se používají, a sledujte jejich využití.
- Vymažte selektivní vymazání tím, že z aplikací odeberete jenom firemní data.

Jedním ze způsobů, jak Intune zajišťuje zabezpečení mobilních aplikací, je prostřednictvím **[zásad ochrany aplikací](../apps/app-protection-policy.md)**. Zásady ochrany aplikací:

- Využijte Azure AD identity k izolaci firemních dat od osobních dat. Proto jsou osobní údaje izolované od jejich povědomí z organizace. K datům, která se získávají pomocí přihlašovacích údajů organizace, se přidávají další ochrana zabezpečení
- Zabezpečte přístup k osobním zařízením omezením akcí, které mohou uživatelé provádět, například kopírování a vkládání, ukládání a zobrazování.
- Dá se vytvořit a nasadit na zařízeních, která jsou zaregistrovaná v Intune, zaregistrovaná v jiné službě MDM nebo není zaregistrovaná v žádné službě MDM. V zaregistrovaných zařízeních můžou zásady ochrany aplikací přidat další vrstvu ochrany.

Uživatel se například přihlásí k zařízení pomocí svých přihlašovacích údajů organizace. Jejich identita organizace umožňuje přístup k datům, která jsou odepřena své osobní identitě. Jak se používají data organizace, zásady ochrany aplikací řídí způsob ukládání a sdílení dat. Když se uživatelé přihlásí pomocí své osobní identity, tyto samé ochrany se nepoužijí. Tímto způsobem má kontrolu nad daty organizace, zatímco koncoví uživatelé udržují kontrolu a ochranu osobních údajů nad svými osobními údaji.

A můžete Intune použít spolu s ostatními službami v EMS. Tato funkce poskytuje vaší organizaci zabezpečení mobilních aplikací nad rámec toho, co je součástí operačního systému a všech aplikací. Aplikace spravované pomocí EMS mají přístup k širší sadě funkcí mobilní aplikace a ochrany dat.

![Obrázek ukazující úrovně zabezpečení dat správy aplikací](./media/what-is-intune/managing-mobile-apps.png)

## <a name="compliance-and-conditional-access"></a>Dodržování předpisů a podmíněný přístup

Intune se integruje s Azure AD a umožňuje širokou škálu scénářů řízení přístupu. Například vyžadovat, aby mobilní zařízení splňovala standardy organizace definované v Intune, než budete mít přístup k síťovým prostředkům, jako je e-mail nebo SharePoint. Podobně můžete služby uzamknout, aby byly dostupné jenom pro konkrétní sadu mobilních aplikací. Můžete například uzamknout Exchange Online, aby k němu měl přistupovat jenom Outlook nebo Outlook Mobile.

**Online prostředky**:

- [Nastavení pravidel na zařízeních pro povolení přístupu k prostředkům vaší organizace](../protect/device-compliance-get-started.md)

- [Běžné způsoby použití podmíněného přístupu s Intune](../protect/conditional-access-intune-common-ways-use.md)

## <a name="how-to-get-intune"></a>Jak získat Intune

Intune je k dispozici:

- Jako samostatná [Služba Azure](https://go.microsoft.com/fwlink/?linkid=2090973)
- Součástí [Microsoft 365](https://www.microsoft.com/microsoft-365/enterprise-mobility-security/microsoft-intune) a [Microsoft 365 státní správy](https://www.microsoft.com/microsoft-365/government)
- Jako [správu mobilních zařízení v Microsoft 365](https://support.office.com/article/Set-up-Mobile-Device-Management-MDM-in-Office-365-dd892318-bc44-4eb1-af00-9db5430be3cd), která se skládá z některých omezených funkcí Intune

Intune se používá v mnoha odvětvích, včetně [státní správy](/enterprise-mobility-security/solutions/ems-govt-service-description), [vzdělávání](https://www.microsoft.com/en-us/education/intune), veřejného [terminálu nebo vyhrazeného zařízení](../configuration/kiosk-settings.md) pro výrobu a prodej a další.

## <a name="next-steps"></a>Další kroky

- Přečtěte si některé [běžné obchodní problémy, které Intune pomáhá vyřešit](common-scenarios.md).
- Začněte s [30denní zkušební verzí Intune](free-trial-sign-up.md).
- Naplánujte [migraci do Intune](migration-guide.md).
- Pomocí bezplatné zkušební verze nebo předplatného můžete procházet krok [rychlý Start: vytvoření profilu e-mailového zařízení pro iOS](../configuration/quickstart-email-profile.md).