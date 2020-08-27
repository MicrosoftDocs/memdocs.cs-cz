---
title: Správa zařízení v Microsoft 365
description: Součástí Microsoft 365 Enterprise je Microsoft Intune. Podívejte se, jak Intune zajišťuje správu mobilních zařízení a správu mobilních aplikací pro vaši organizaci. Čtení běžných scénářů a použití Intune k nasazení Microsoft 365 ve vašem prostředí.
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/24/2020
ms.topic: overview
audience: microsoft-business
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.technology: ''
ms.assetid: 0649d310-43a7-4b01-85d2-da255d03e1da
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: microsoft-intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: d2b7deb7d3c09a41a16b1ebf3da26075f0cc70eb
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915343"
---
# <a name="device-management-overview"></a>Přehled správy zařízení

Klíčovým úkolem každého správce je chránit a zabezpečovat prostředky a data organizace na zařízeních uživatelů v jejich organizaci. Tato úloha je **Správa zařízení**. Uživatelé přijímají a odesílají e-maily z osobních účtů, procházejí weby z domova a z restaurací a instalují aplikace a hry. Tito uživatelé jsou také zaměstnanci a studenti. Na svých zařízeních chtějí přistupovat k pracovním a školním prostředkům, jako je e-mail a OneNote, a přistupovat k nim rychle. Jako správce je vaším cílem chránit tyto prostředky a poskytovat uživatelům snadný přístup pro celou řadu zařízení, a to vše současně.

Správa zařízení umožňuje organizacím chránit a zabezpečovat své prostředky a data a z různých zařízení.

Díky poskytovateli správy zařízení může organizace zajistit, aby přístup k proprietárním informacím měli jenom oprávnění lidé a zařízení. Podobně se uživatelé zařízení můžou rozpracovat na práci s pracovními daty z telefonu, protože ví, že jejich zařízení splňuje požadavky organizace na zabezpečení. Jako zástupci organizace si možná kladete otázku: **Jaký produkt máme k ochraně našich prostředků použít?**

Odpověď je [Microsoft Intune](what-is-intune.md). Intune nabízí správu mobilních zařízení (MDM) a správu mobilních aplikací (MAM). K hlavním úlohám řešení MDM nebo MAM patří:

- Podporují nejrůznější mobilní prostředí a bezpečně spravují zařízení s iOS/iPadOS, Androidem, Windows a macOS.
- Ujistěte se, že zařízení a aplikace vyhovují požadavkům na zabezpečení vaší organizace.
- Vytvořte zásady, které pomůžou zabezpečit data vaší organizace v bezpečí na zařízeních vlastněných organizací a osobním zařízením.
- Použití jediného unifikovaného mobilního řešení k vynucení těchto zásad a usnadnění správy zařízení, aplikací, uživatelů a skupin
- Chraňte své firemní informace tím, že vám pomohou řídit způsob, jakým vaše zaměstnanci přistupují k datům a sdílí je.

Intune je součástí Microsoft Azure, Microsoft 365 a integruje se s Azure Active Directory (Azure AD). Azure AD pomáhá řídit, kdo má přístup a k čemu má přístup.

## <a name="microsoft-intune"></a>Microsoft Intune

Řada organizací, například Microsoft, používá Intune k zabezpečení vlastnických dat, ke kterým uživatelé přistupují ze svých firemních a osobních mobilních zařízení. Intune zahrnuje zásady konfigurace zařízení a aplikací, zásady aktualizace softwaru a stavy instalace (grafy, tabulky a sestavy), které vám pomůžou zabezpečit a monitorovat přístup k datům.

Je běžné, že lidé mají několik zařízení, která používají různé platformy. Zaměstnanec může například pro práci používat Surface Pro a pro soukromé účely mobilní zařízení s Androidem. A je běžné, že tato osoba z obou uvedených zařízení přistupuje k prostředkům organizace, jako jsou například Microsoft Outlook a SharePoint.

S Intune můžete spravovat víc zařízení na osobu a na různých platformách, které se na jednotlivých zařízeních spouštějí, včetně iOS/iPadOS, macOS, Androidu a Windows. Intune odděluje zásady a nastavení podle platformy zařízení. Proto je snadné spravovat a zobrazovat zařízení konkrétní platformy.

**[Typické scénáře](common-scenarios.md)** jsou výborným zdrojem informací o tom, jak se v Intune řeší běžné situace při práci s mobilními zařízeními. Najdete zde scénáře pro tyto oblasti:  

- Ochrana e-mailu pomocí místního Exchange
- Bezpečný přístup k Office 365
- Použití osobních zařízení pro přístup k prostředkům organizace

Další informace o Intune najdete v tématu [co je Intune](what-is-intune.md).

## <a name="co-management"></a>Spoluspráva

Mnoho organizací používá místní Configuration Manager ke správě zařízení, včetně stolních počítačů a serverů. K Microsoft Intune můžete v cloudu připojit místní Configuration Manager. Když se připojíte ke cloudu, získáte výhody Intune a cloudu, včetně [podmíněného přístupu](../../configmgr/comanage/quickstart-conditional-access.md), [spouštění vzdálených akcí](../../configmgr/comanage/quickstart-remote-actions.md), [používání Windows autopilotu](../../configmgr/comanage/quickstart-autopilot.md)a dalších.

[Microsoft Endpoint Manager](../../endpoint-manager-overview.md) je platforma řešení, která sjednocuje několik služeb. Zahrnuje [Microsoft Intune](what-is-intune.md) pro cloudovou správu zařízení a [Configuration Manager + Intune](../../configmgr/comanage/overview.md) pro správu zařízení pomocí cloudu.

Pokud používáte Configuration Manager a jste připraveni přesunout některé úkoly do cloudu, pak je spoluspráva vaše odpověď.

Další informace o připojení Configuration Manager ke cloudu najdete v tématu [co je spoluspráva](../../configmgr/comanage/overview.md).

## <a name="integration-with-secure-and-protect-services"></a>Integrace se službami zabezpečení a ochrany

Hlavní úlohou řešení správy zařízení je poskytování zabezpečení a ochrany. Intune k plnění této úlohy skvěle využívá integraci s dalšími službami. Příklad:

- **Microsoft 365** je hlavní komponentou pro zjednodušení běžných úloh IT. V centru pro správu Microsoft 365 vytváříte uživatele a spravujete skupiny. Získáte také přístup k dalším službám, jako je například Intune, Azure AD a další.

  Vytvořte například skupinu zařízení se systémem iOS/iPadOS v Microsoft 365. Pak pomocí Intune zařaďte zásady do skupiny zařízení se systémem iOS/iPadOS, které se zaměřují na funkce iOS/iPadOS, jako je například přístup k obchodu s aplikacemi, zálohování na iCloud, použití webového filtru společnosti Apple a další.

- **Windows Defender** obsahuje mnoho funkcí zabezpečení, které usnadňují ochranu zařízení s Windows 10. Při společném použití Intune a programu Windows Defender můžete například:

  - Povolit, aby [filtr SmartScreen v programu Windows Defender](../protect/endpoint-protection-windows-10.md) hledal podezřelou aktivitu souborů a aplikací na mobilních zařízeních
  - Použití [rozšířené ochrany před internetovými útoky v programu Microsoft Defender (ATP)](../protect/advanced-threat-protection.md) k ochraně před narušením zabezpečení mobilních zařízení. A můžete tak omezit dopad porušení zabezpečení tím, že zablokujete uživatele z firemních prostředků.

- **Podmíněný přístup** je funkce Azure Active Directory a v Intune se v tomto případě integruje. Pomocí [podmíněného přístupu](../protect/conditional-access.md)zajistěte, aby přístup k e-mailu, SharePointu a dalším aplikacím umožňoval jenom vyhovující zařízení.

## <a name="choose-the-device-management-solution-thats-right-for-you"></a>Výběr správného řešení pro správu zařízení

Existuje několik způsobů přístupu ke správě zařízení. Nejdřív můžete spravovat různé aspekty zařízení pomocí funkcí integrovaných do Intune. Tento přístup se nazývá **Správa mobilních zařízení (MDM)**. Uživatelé si zaregistrují svá zařízení a používají certifikáty ke komunikaci s Intune. Jako správce IT můžete nabízet aplikace na zařízeních, omezovat zařízení na konkrétní operační systém, blokovat osobní zařízení a další. Pokud dojde ke ztrátě nebo odcizení zařízení, můžete také odebrat všechna data ze zařízení.

U druhého způsobu spravujete aplikace na zařízeních. Tento přístup se nazývá **Správa mobilních aplikací (MAM)**. Uživatelé můžou k přístupu k prostředkům organizace používat svoje osobní zařízení. Při otevření aplikace, jako je e-mail nebo SharePoint, se uživatelům zobrazí výzva k dalšímu ověření. Pokud dojde ke ztrátě nebo odcizení zařízení, můžete odebrat všechna firemní data z aplikací spravovaných pomocí Intune.

Můžete také použít společně kombinaci [MDM a MAM](byod-technology-decisions.md).

Při nastavení Intune se také rozhodujete, jestli ke správě zařízení budete používat výhradně Azure Portal, nebo společně Intune a Microsoft 365. [Migrace správy mobilních zařízení do Intune v Azure Portal](https://www.microsoft.com/itshowcase/Article/Content/1042/Migrating-mobile-device-management-to-Intune-in-the-Azure-portal) je Případová studie Microsoftu. V takovém případě si prostudujte, jak Microsoft IT zvolí moderní přístup k správě zařízení, a přečtěte si získané lekce.

## <a name="simplify-it-tasks-using-the-device-management-admin-center"></a>Zjednodušení IT úloh pomocí centra pro správu správy zařízení

[Centrum pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) je jedním z důvodů, jak spravovat a provádět úlohy pro vaše mobilní zařízení. Tento pracovní prostor zahrnuje služby používané pro správu zařízení, včetně Intune a Azure Active Directory, a také správu klientských aplikací.

V centru pro správu správy zařízení můžete:

- [Registrovat zařízení](../enrollment/device-enrollment.md)
- [Nastavit dodržování předpisů zařízením](../protect/device-compliance-get-started.md)
- [Správa zařízení](../remote-actions/device-management.md)
- [Správa aplikací](../apps/app-management.md)  
- [E-knihy pro iOS](../apps/vpp-ebooks-ios.md)  
- [Instalace konektoru Exchange On-Premises Connector](../protect/exchange-connector-install.md)  
- [Správa rolí](role-based-access-control.md)  
- Správa aktualizací softwaru
  - [Správa aktualizací Windows 10](../protect/windows-update-for-business-configure.md)  
  - [Správa aktualizací pro iOS/iPadOS](../protect/software-updates-ios.md)  
- [Azure Active Directory](/azure/active-directory)  
- [Správa uživatelů](/azure/active-directory/fundamentals/add-users-azure-active-directory)
- [Správa skupin a členů](/azure/active-directory/fundamentals/active-directory-manage-groups)
- [Odstraňování potíží](help-desk-operators.md)

## <a name="next-steps"></a>Další kroky

Až budete připraveni začít s řešením MDM nebo MAM, Projděte si jednotlivé kroky k nastavení Intune, registraci zařízení a zahájení vytváření zásad. [Správa mobilních zařízení pro Microsoft 365](/microsoft-365/enterprise/mobility-infrastructure) je také skvělým prostředkem.