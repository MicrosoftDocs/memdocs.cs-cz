---
title: Scénář s asistencí – nasazení Microsoft Edge pro mobilní zařízení
titleSuffix: Microsoft Intune
description: Přečtěte si informace o scénáři s průvodcem nasazení Microsoft Edge pro mobilní zařízení z portálu pro správu Microsoft 365.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7eb352e73a88f8da8eb927400b5db86356c10363
ms.sourcegitcommit: 9a700a72735f9a316bdb51c44f86f9cc3bfb7be2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/21/2020
ms.locfileid: "83764148"
---
# <a name="guided-scenario---deploy-microsoft-edge-for-mobile"></a>Scénář s asistencí – nasazení Microsoft Edge pro mobilní zařízení

Podle tohoto [Průvodce](guided-scenarios-overview.md)můžete aplikaci Microsoft Edge přiřadit uživatelům na zařízeních s iOS/IPadOS nebo Androidem ve vaší organizaci. Přiřazení této aplikace umožní uživatelům plynule procházet obsah pomocí podnikových zařízení.

Microsoft Edge umožňuje uživatelům vyjímat zbytečný web s integrovanými funkcemi, které jim pomůžou konsolidovat, organizovat a spravovat pracovní obsah. Uživatelé zařízení se systémem iOS/iPadOS a Androidem, kteří se přihlásí pomocí svých podnikových účtů služby Azure AD v aplikaci Microsoft Edge, uvidí svůj prohlížeč předem načtený s **oblíbenými položkami** na pracovišti a vámi definovanými filtry webu.

> [!NOTE]
> Pokud jste zablokované uživatelům zablokovali registraci zařízení se systémem iOS nebo iPadOS nebo Androidem, tento scénář nepovolí registraci a uživatelé budou muset pro sebe nainstalovat Edge.
Následující funkce Microsoft Edge Enterprise, které jsou povolené zásadami Intune, zahrnují:

- **Dual-identity** – uživatelé můžou pro procházení přidat jak pracovní účet, tak i osobní účet. Mezi těmito dvěma identitami se dokončí oddělení, které se podobá architektuře a prostředí v aplikacích Office 365 a Outlook. Správci Intune budou moct nastavit požadované zásady pro chráněné prostředí pro procházení v rámci pracovního účtu.
- **Integrace zásad ochrany aplikací Intune** – správci teď můžou cílit na zásady ochrany aplikací na Microsoft Edge, včetně ovládacího prvku pro vyjmutí, kopírování a vložení, zabránění zachycení obrazovky a zajištění, aby se odkazy vybrané uživatelem otevíraly jenom v jiných spravovaných aplikacích.
- **Integrace služby Azure Application proxy** – správci můžou řídit přístup k aplikacím SaaS a webovým aplikacím, což pomáhá zajistit, aby se aplikace založené na prohlížeči spouštěly jenom v zabezpečeném prohlížeči Microsoft Edge, ať už se koncoví uživatelé připojují z podnikové sítě nebo se připojí z Internetu.
- **Zástupci spravovaných oblíbených položek a domovské stránky** – pro usnadnění přístupu můžou správci nastavit adresy URL tak, aby se zobrazovaly v části Oblíbené, pokud jsou koncoví uživatelé ve firemním kontextu. Správci můžou nastavit zástupce domovské stránky, který se zobrazí jako primární zástupce, když firemní uživatel otevře novou stránku nebo novou kartu v Microsoft Edge.

## <a name="prerequisites"></a>Požadavky

- [Nastavení autority MDM na Intune](mdm-authority-set.md#set-mdm-authority-to-intune) – nastavení autority správy mobilních zařízení (MDM) určuje způsob správy zařízení. Jako správce IT musíte nastavit autoritu MDM, aby uživatelé mohli registrovat zařízení pro správu.
- Potřebná oprávnění správce Intune:
  - Spravované aplikace – čtení, vytváření, odstraňování a přiřazování oprávnění
  - Mobilní aplikace – čtení, vytváření a přiřazování oprávnění
  - Nastavení zásad čtení, vytváření a přiřazování oprávnění
  - Oprávnění číst, aktualizovat v organizaci

## <a name="step-1---introduction"></a>Krok 1 – Úvod

Pomocí průvodce **nasazením Microsoft Edge pro mobilní** prostředí nastavíte základní nasazení Microsoft Edge pro vybranou skupinu uživatelů iOS/IPadOS a Androidem. Toto nasazení implementuje zástupce s **duální identitou** a **spravované oblíbené položky a domovské stránky**. Zařízení zaregistrovaná vybranými uživateli navíc budou automaticky mít aplikaci Microsoft Edge nainstalovanou Intune. K této automatické instalaci dojde u všech typů registrace řízených uživatelem, mezi které patří:

- registrace zařízení se systémem iOS/iPadOS prostřednictvím aplikace Portál společnosti
- registrace spřažení uživatele pro iOS/iPadOS prostřednictvím Apple Business Manageru
- Starší registrace Androidu prostřednictvím aplikace Portál společnosti

Tento scénář s asistencí automaticky povolí zobrazení **MyApp** v oblíbených položkách Microsoft Edge a nakonfiguruje prohlížeč se stejným brandingem, který jste nastavili pro aplikaci Portál společnosti Intune.

### <a name="what-you-will-need-to-continue"></a>Co budete potřebovat k pokračování

Požádáme vás o oblíbené položky na pracovišti, které uživatelé potřebují, a filtry, které požadujete pro procházení webu. Než budete pokračovat, ujistěte se, že jste dokončili následující úlohy:

- Přidejte uživatele do skupin Azure AD. Další informace najdete v tématu [Vytvoření základní skupiny a přidání členů pomocí Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=2102458).
- Registrace zařízení s iOS/iPadOS nebo Androidem v Intune Další informace najdete v tématu [registrace zařízení](https://go.microsoft.com/fwlink/?linkid=2102547).
- Shromážděte seznam oblíbených položek na pracovišti, které se dají přidat do Microsoft Edge.
- Shromážděte seznam filtrů webů, které se vynutily v Microsoft Edge.

## <a name="step-2---basics"></a>Krok 2 – základy

V tomto kroku musíte zadat název a popis pro nové zásady Microsoft Edge. Na tyto zásady se dá později odkazovat, pokud potřebujete změnit přiřazení a konfigurace. Průvodce s asistencí přidá a přiřadí aplikaci Microsoft Edge iOS/iPadOS pro vaše zařízení s iOS/iPadOS a aplikaci Microsoft Edge pro Android pro vaše zařízení s Androidem. V tomto kroku se taky pro tyto aplikace vytvoří zásady konfigurace.

## <a name="step-3---configuration"></a>Krok 3 – konfigurace

V tomto kroku se ve scénáři s asistencí nakonfiguruje Microsoft Edge, aby zobrazoval všechny ostatní aplikace přiřazené uživatelům prostřednictvím Intune a sdílel stejné značky jako aplikace Microsoft Intune Portál společnosti. Microsoft Edge můžete dále konfigurovat pomocí **adresy URL zástupce domovské stránky**, seznamu **spravovaných záložek**a seznamu **blokovaných adres URL**. **Adresa URL zástupce domovské stránky** se zobrazí uživatelům jako první ikony pod panelem hledání, když otevřou novou kartu v Microsoft Edge na svém zařízení. **Spravované záložky** jsou seznam oblíbených adres URL, které mají vaši uživatelé k dispozici při používání Microsoft Edge v jejich pracovním kontextu. **Blokované adresy URL** určují weby, které jsou pro vaše uživatele blokované v pracovním kontextu. Všechny ostatní weby budou povoleny.

## <a name="step-4---assignments"></a>Krok 4 – přiřazení

V tomto kroku můžete vybrat skupiny uživatelů, pro které chcete použít Microsoft Edge Mobile nakonfigurovaný pro práci. Microsoft Edge se taky nainstaluje na všechna zařízení s iOS/iPadOS a Androidem zaregistrovaná těmito uživateli.

## <a name="step-5---review--create"></a>Krok 5 – přezkoumání a vytvoření

Poslední krok vám umožní zkontrolovat souhrn nastavení, která jste nakonfigurovali. Po zkontrolování výběru klikněte na **vytvořit** a dokončete scénář s asistencí. 

> [!NOTE]
> Získání Konfigurace Edge může trvat až 12 hodin. Další informace najdete v tématu [zásady konfigurace aplikací pro Microsoft Intune](../apps/app-configuration-policies-overview.md).

> [!IMPORTANT]
> Po dokončení průvodce se zobrazí souhrn. Prostředky uvedené v souhrnu můžete upravit později, ale Tabulka zobrazující tyto prostředky se neuloží.

## <a name="next-steps"></a>Další kroky

- Nastavením integrace zásad ochrany aplikací Intune Zvyšte zabezpečení používání Microsoft Edge. Další informace najdete v tématu [Zásady ochrany aplikací pro Microsoft Edge](../apps/manage-microsoft-edge.md#application-protection-policies-for-microsoft-edge).
- Pokud máte Intranetové servery, které chcete zahrnout, prozkoumejte ochranu přístupu pomocí integrace služby Azure Application proxy. Další informace najdete v tématu [Konfigurace nastavení proxy aplikací pro Microsoft Edge](../apps/manage-microsoft-edge.md#configure-application-proxy-settings-for-microsoft-edge).

