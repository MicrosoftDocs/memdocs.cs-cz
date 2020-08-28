---
title: Microsoft Endpoint Manager – přehled – Azure | Microsoft Docs
description: Správce koncových bodů zahrnuje Intune, Configuration Manager, spolusprávu, Desktop Analytics, Windows autopilot a centrum pro správu ke správě všech zařízení, včetně místních.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/21/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: ''
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0d638cb382aa7abe8859648192837601c86f22ce
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996550"
---
# <a name="microsoft-endpoint-manager-overview"></a>Přehled k produktu Microsoft Endpoint Manager

Microsoft Endpoint Manager pomáhá zajistit moderní pracoviště a moderní správu, aby vaše data byla zabezpečená v cloudu i v místním prostředí. Správce koncových bodů zahrnuje služby a nástroje, které používáte ke správě a monitorování mobilních zařízení, stolních počítačů, virtuálních počítačů, integrovaných zařízení a serverů.

Správce koncových bodů kombinuje služby, které můžete znát a již používat, včetně Microsoft Intune, Configuration Manager, analýzy stolních počítačů, spolusprávy a Windows autopilotu. Tyto služby jsou součástí Microsoft 365 stacku, které vám pomůžou zabezpečit přístup, chránit data a reagovat a spravovat rizika.

Začněte sledováním následujících dvou minut od Brada Anderson, což je Microsoft Corporate viceprezident pro Microsoft 365:

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## <a name="what-you-get"></a>Co získáte

Správce koncových bodů zahrnuje následující služby:

- **Microsoft Intune**: intune 100 je cloudová správa mobilních zařízení (MDM) a Správa mobilních aplikací (MAM) pro vaše aplikace a zařízení. Umožňuje vám řídit funkce a nastavení na zařízeních se systémem Android, Android Enterprise, iOS/iPadOS, macOS a Windows 10. Integruje se s ostatními službami, včetně Azure Active Directory (AD), služby pro ochranu před mobilními hrozbami, šablon ADMX, Win32 a vlastních obchodních aplikací a dalších.

  Pokud máte místní infrastrukturu, jako je Exchange nebo Active Directory, jsou k dispozici také konektory Intune:

  - **Konektor Intune pro Active Directory** přidává položky do místní domény služby Active Directory pro počítače, které se registrují pomocí automatického pilotního projektu Windows. Další informace najdete v tématu [nasazení hybridních zařízení připojených k Azure AD](./autopilot/windows-autopilot-hybrid.md).
  - **Intune Certificate Connector** zpracovává žádosti o certifikát ze zařízení, která používají certifikáty k ověřování a šifrování S/MIME e-mailu. Další informace najdete v tématu [použití certifikátů k ověřování](./intune/protect/certificates-configure.md).

  Jako součást Správce koncových bodů můžete pomocí Intune vytvářet a kontrolovat dodržování předpisů a nasazovat aplikace, funkce a nastavení do zařízení pomocí cloudu.

  Další informace najdete v tématu [co je Microsoft Intune](/intune/fundamentals/what-is-intune).

- **Configuration Manager**: Configuration Manager je místní řešení pro správu, ve kterém můžete spravovat stolní počítače, servery a přenosné počítače, které jsou ve vaší síti nebo na internetu. V cloudu můžete povolit integraci s Intune, Azure Active Directory (AD), ATP Microsoft Defender a dalšími Cloud Services. Pomocí Configuration Manager můžete nasazovat aplikace, aktualizace softwaru a operační systémy. Můžete také monitorovat dodržování předpisů, dotazování a působit na klienty v reálném čase a mnohem víc.

  Jako součást Správce koncových bodů můžete dál používat Configuration Manager, jak budete mít vždycky. Pokud jste připraveni přesunout některé úkoly do cloudu, zvažte spolupráci v rámci [spolusprávy](/configmgr/comanage/).

  Další informace najdete v tématu [co je Configuration Manager?](/configmgr/core/understand/introduction).

- **Spoluspráva**: spoluspráva kombinuje vaše stávající místní Configuration Manager investice do cloudu s využitím Intune a dalších cloudových služeb Microsoft 365. Zvolíte, jestli Configuration Manager nebo Intune je autorita pro správu pro sedm různých skupin úloh.

  V rámci správce koncových bodů používá společná Správa funkce cloudu, včetně podmíněného přístupu. Některé úkoly se udržují v místním prostředí a při spouštění dalších úloh v cloudu s Intune.

  Další informace najdete v tématu [co je spoluspráva?](/configmgr/comanage/overview).

- **Plocha Analytics**: Desktop Analytics je cloudová služba, která se integruje s Configuration Manager. Poskytuje přehled a inteligentní informace, které vám pomohou při rozhodování o připravenosti na aktualizace svých klientů s Windows. Služba kombinuje data z vaší organizace s daty agregovanými z milionů zařízení připojených ke cloudu Microsoftu. Poskytuje informace o aktualizacích zabezpečení, aplikacích a zařízeních ve vaší organizaci a identifikuje problémy s kompatibilitou aplikací a ovladačů. Vytvoření pilotního projektu pro zařízení s největší pravděpodobně poskytuje nejlepší přehledy pro prostředky v rámci vaší organizace.

  Jako součást Správce koncových bodů můžete využívat přehledy cloudových analýz na ploše, které udržují zařízení s Windows 10 aktuální.

  Další informace najdete v tématu [co je Desktop Analytics?](/configmgr/desktop-analytics/overview).

- **Windows autopilot**: Windows autopilot nastaví a předem nakonfiguruje nová zařízení, která se připravují k použití. Je navržený tak, aby zjednodušil životní cyklus zařízení s Windows, a to i pro koncové uživatele, od počátečního nasazení po skončení životnosti.

  Jako součást Správce koncových bodů použijte k předkonfigurování zařízení a automatické registraci zařízení v Intune nástroj autopilot. Můžete také integrovat autopilot pomocí Configuration Manager a spolusprávy pro složitější konfigurace zařízení (ve verzi Preview).

  Další informace najdete v tématu [Přehled Windows autopilotu](/windows/deployment/windows-autopilot/windows-autopilot) a [registrace zařízení s Windows v Intune](./autopilot/enrollment-autopilot.md).

- **Azure Active Directory (AD)**: služba Endpoint Manager používá službu Azure AD k identifikaci zařízení, uživatelů, skupin a služby Multi-Factor Authentication (MFA). **Azure AD Premium**, což může být dodatečné náklady, obsahuje [Další funkce](https://azure.microsoft.com/pricing/details/active-directory/) , které vám pomůžou chránit zařízení, aplikace a data, včetně dynamických skupin, automatického zápisu a podmíněného přístupu.

  Další informace najdete v tématech [Přidání uživatelů](./intune/fundamentals/users-add.md), [Nastavení automatického zápisu](./intune/enrollment/windows-enroll.md)a [o podmíněném přístupu](./intune/protect/conditional-access.md).

- **Centrum pro správu Správce koncových bodů**: [Centrum pro správu](https://go.microsoft.com/fwlink/?linkid=2109431) je jedním zastaveným webem, který umožňuje vytvářet zásady a spravovat vaše zařízení. Připojuje se k jiným klíčovým službám pro správu zařízení, včetně skupin, zabezpečení, podmíněného přístupu a vytváření sestav. Toto centrum pro správu také zobrazuje zařízení spravovaná pomocí Configuration Manager a Intune (ve verzi Preview).

## <a name="choose-whats-right-for-you"></a>Zvolit, co je pro vás nejvhodnější

Existuje několik způsobů, jak určit, co je pro vaši organizaci správné. Vaše další kroky závisí na tom, co vaše organizace dělá. Zvažte, co se snažíte dosáhnout.

Příklad:

- Pokud neustále zřizujete nová zařízení, začněte s Windows autopilotem.
- Pokud přidáte pravidla a nastavení řízení pro uživatele, aplikace a zařízení, začněte s Intune.
- Pokud aktuálně používáte Configuration Manager k nasazování aplikací a chcete používat podmíněný přístup na základě požadavků na zabezpečení, začněte spolusprávou.
- Pokud aktuálně používáte Configuration Manager a zodpovídáte za udržování aktuálnosti zařízení s Windows 10, začněte s desktopovou analýzou.
- Pokud začínáte s MDM a MAM, můžete použít šablony ADMX k řízení nastavení Office, Microsoft Edge a Windows a začít s Intune.

Správce koncových bodů si taky můžete představit ve třech částech: cloudové, místní a cloudová a místní:

- **Cloud**: všechna data jsou uložená v Azure. A žádná další datová centra. Tento přístup vám dává výhody cloudu a výhody zabezpečení Azure.

- **Místní**: Pokud máte místní infrastrukturu, která zahrnuje Configuration Manager nebo není připravená na používání cloudu, můžete zachovat stávající systémy.

- **Cloud**a místní: řada prostředí je smíšená a používá přístup k cloudovým připojením. To znamená, že používají kombinaci cloudu a místního prostředí. Pro nová zařízení používejte k přístupu a ochraně dat výhody Intune. Pokud používáte Configuration Manager, připojte se ke cloudu pro další funkce a analýzy. Pokud chcete přesunout některé úlohy do cloudu, je vhodná možnost spoluspráva.

## <a name="what-you-need-to-get-started"></a>Co potřebujete, než začnete

Microsoft Endpoint Manager je platforma řešení, která sjednocuje několik technologií. Nejedná se o novou licenci. Služby jsou licencovány na základě podmínek jejich jednotlivých licencí. Další informace najdete v [licenčních podmínkách k produktu](https://www.microsoft.com/licensing/product-licensing/products).

Pokud v tuto chvíli používáte Configuration Manager, získáte také Microsoft Intune ke společné správě zařízení s Windows. Pro jiné platformy, jako je iOS/iPadOS a Android, budete potřebovat samostatnou licenci Intune.

Ve většině scénářů může být Microsoft 365 nejlepší volbou, protože vám nabízí správce koncových bodů a Office. Další informace najdete v tématu [Microsoft 365](https://www.microsoft.com/licensing/product-licensing/microsoft-365-enterprise).

## <a name="next-steps"></a>Další kroky

[Využijte výkon cloudových informací, abyste je zjednodušili a urychlili a přešli na moderní pracovní plochu.](https://www.microsoft.com/microsoft-365/blog/2019/11/04/use-the-power-of-cloud-intelligence-to-simplify-and-accelerate-it-and-the-move-to-a-modern-workplace/)

[Microsoft Endpoint Manager](https://www.microsoft.com/microsoft-365/microsoft-endpoint-manager)

[Kurz: Seznámení se se službou Intune v Microsoft Endpoint Manageru](/intune/fundamentals/tutorial-walkthrough-endpoint-manager)

[Co je Microsoft 365? naučit se modul](/learn/modules/what-is-m365/index)