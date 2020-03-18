---
title: Scénář s asistencí – zabezpečené systém Microsoft Office mobilní aplikace
titleSuffix: Microsoft Intune
description: Přečtěte si informace o scénáři s průvodcem nasazení zabezpečených systém Microsoft Office mobilních aplikací z portálu pro správu Microsoft 365 zařízení.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/06/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7aabc09e276c723e9aeaed4ec8eb3dd4c0332b4e
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332531"
---
# <a name="guided-scenario---secure-microsoft-office-mobile-apps"></a>Scénář s asistencí – zabezpečené systém Microsoft Office mobilní aplikace

Podle tohoto průvodce na portálu pro správu zařízení můžete povolit základní ochranu aplikací Intune na zařízeních s iOS/iPadOS a Androidem.

Ochrana aplikace, kterou povolíte, vynutila následující akce:

- Zašifrujte pracovní soubory.
- Pro přístup k pracovním souborům vyžadovat PIN kód.
- Vyžadovat, aby se PIN kód resetoval po pěti neúspěšných pokusech.
- Blokuje zálohování pracovních souborů v iTunes, iCloud nebo v zálohovacích službách Androidu.  
- Vyžadovat, aby se pracovní soubory uložily jenom na OneDrive nebo SharePoint.
- Zabraňte chráněným aplikacím v načítání pracovních souborů na zařízeních s jailbreakem nebo rootem.
- Zablokovat přístup k pracovním souborům, pokud je zařízení po dobu 720 minut v režimu offline.
- Pokud je zařízení po dobu 90 dnů offline, odeberte pracovní soubory.

## <a name="background"></a>Podrobnosti

Mobilní aplikace Office a Microsoft Edge pro mobilní zařízení podporují duální identitu. Duální identita umožňuje aplikacím spravovat pracovní soubory odděleně od osobních souborů. 

![Obrázek podnikových dat versus osobních údajů](./media/guided-scenarios-office-mobile/guided-scenarios-office-mobile-01.png)

[Zásady ochrany aplikací Intune](../apps/app-protection-policy.md) vám pomůžou chránit pracovní soubory na zařízeních, která jsou zaregistrovaná v Intune. Zásady ochrany aplikací můžete použít také u zařízení vlastněných zaměstnanci, která nejsou zaregistrovaná ke správě v Intune. V takovém případě, i když vaše společnost zařízení nespravuje, je stále nutné zajistit, aby byly pracovní soubory a prostředky chráněné.

Pomocí zásad ochrany aplikací můžete uživatelům zabránit v ukládání pracovních souborů v nechráněných umístěních. Můžete také zamezit přesunu dat do jiných aplikací, které nejsou chráněné zásadami ochrany aplikací. Mezi nastavení zásad ochrany aplikací patří:

- Zásady přemístění dat, jako jsou **ukládání kopií org data**, a **omezení vyjmutí, kopírování a vložení**.
- Nastavení zásad přístupu, které vyžaduje pro přístup jednoduchý kód PIN a zablokuje spouštění spravovaných aplikací na zařízeních s jailbreakem nebo rootem.

Podmíněný přístup založený na aplikaci a správa klientských aplikací přidávají další vrstvu zabezpečení. Zajišťují, aby přístup k Exchangi Online a dalším službám Office 365 měly jenom klientské aplikace, které podporují řešení Intune s jeho zásadami ochrany aplikací.

Pokud povolíte přístup k Exchangi Online jenom aplikaci Microsoft Outlook, můžete zablokovat integrované e-mailové aplikace v iOS/iPadOS a Androidu. Kromě toho můžete blokovat aplikace, které nemají zásady ochrany aplikací Intune použité pro přístup k SharePointu Online.

V tomto příkladu použil správce zásady ochrany aplikací u aplikace Outlook a následné pravidlo podmíněného přístupu. To přidá Outlook na seznam schválených aplikací, které lze využít k přístupu k firemnímu e-mailu.

![Tok procesu podmíněného přístupu aplikace Outlook](./media/guided-scenarios-office-mobile/guided-scenarios-office-mobile-02.png)

## <a name="prerequisites"></a>Požadavky

Budete potřebovat následující oprávnění správce Intune:

- Spravované aplikace – čtení, vytváření, odstraňování a přiřazování oprávnění
- Nastavení zásad čtení, vytváření a přiřazování oprávnění
- Oprávnění ke čtení z organizace

## <a name="step-1---introduction"></a>Krok 1 – Úvod

Po použití scénáře s průvodcem **Intune App Protection** se vyhnete sdílení nebo nevracení dat mimo vaši organizaci. 

Přiřazení uživatelé s iOS/iPadOS a Androidem musí při každém otevření aplikace Office zadat kód PIN. Po 5 neúspěšných pokusech o zadání PIN kódu musí uživatelé resetovat PIN kód. Pokud už potřebujete PIN zařízení, nebudou mít uživatelé vliv na to.

### <a name="what-you-will-need-to-continue"></a>Co budete potřebovat k pokračování

Požádáme vás o aplikace, které uživatelé potřebují, a to, co je potřeba pro přístup k nim. Ujistěte se, že máte užitečné následující informace:

- Seznam aplikací Office schválených pro podnikové použití
- Jakékoli požadavky na PIN kód pro spouštění schválených aplikací na nespravovaných zařízeních.

## <a name="step-2---basics"></a>Krok 2 – základy

V tomto kroku musíte zadat **předponu** a **Popis** pro nové zásady ochrany aplikací. Při přidávání **předpony**se aktualizují podrobnosti související s prostředky, které vytvoří průvodce vytvořeným procesem. Tyto podrobnosti usnadňují vyhledání zásad později, pokud potřebujete změnit přiřazení a konfiguraci.

> [!TIP]
> Vezměte v úvahu informace o prostředcích, které se vytvoří, abyste na ně mohli odkazovat později.

## <a name="step-3---apps"></a>Krok 3 – aplikace

Abychom vám pomohli začít, tento scénář s asistencí předem vybírá následující mobilní aplikace pro ochranu na zařízeních s iOS/iPadOS a Androidem:

- Microsoft Excel
- Microsoft Word
- Microsoft Teams
- Microsoft Edge
- Microsoft PowerPoint
- Microsoft Outlook
- Microsoft OneDrive

Tento scénář s asistencí také nakonfiguruje tyto aplikace na otevřené webové vazby v Microsoft Edge, aby bylo zajištěno, že pracovní pracoviště budou otevřena v chráněném prohlížeči.

Upravte seznam aplikací spravovaných podle zásad, které chcete chránit. Přidat nebo odebrat aplikace z tohoto seznamu.

Po výběru aplikací klikněte na tlačítko **Další**.

## <a name="step-4---configuration"></a>Krok 4 – konfigurace

V tomto kroku musíte nakonfigurovat požadavky pro přístup k firemním souborům a e-mailům v těchto aplikacích a jejich sdílení. Ve výchozím nastavení mohou uživatelé ukládat data do účtů OneDrive a SharePoint vaší organizace.

| Nastavení | Popis | Výchozí hodnota |
|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
| Typ kódu PIN | Číselné kódy PIN se skládají ze všech čísel. Hesla se skládají z alfanumerických znaků a speciálních znaků.  Pro konfiguraci typu "heslo" v systému iOS/iPadOS je nutné, aby měla aplikace sadu Intune SDK verze 7.1.12 nebo vyšší. Číselný typ nemá žádné omezení, pokud se jedná o verzi sady Intune SDK. | Číselné |
| Vyberte minimální délku PIN kódu. | Určuje minimální počet číslic v posloupnosti kódu PIN. | 6 |
| Znovu ověřit požadavky na přístup po (minuty neaktivity) | Pokud je aplikace spravovaná zásadou neaktivní po dobu delší, než je zadaný počet minut nečinnosti, aplikace se vyzve k zadání požadavků na přístup (tj. Připnutí, nastavení podmíněného spuštění), které se má po spuštění aplikace znovu ověřit. | 30 |
| Tisk organizačních dat | Pokud je zablokovaná, aplikace nemůže tisknout chráněná data. | Blokování |
| Otevření odkazů aplikací spravovaných zásadou v nespravovaných prohlížečích | Pokud je zablokované, musí se odkazy na aplikace spravované podle zásad otevřít ve spravovaném prohlížeči. | Blokování |
| Kopírování dat do nespravovaných aplikací | Pokud je blokované, spravovaná data zůstanou ve spravovaných aplikacích. | Povolit |

## <a name="step-5---assignments"></a>Krok 5 – přiřazení

V tomto kroku můžete vybrat skupiny uživatelů, které chcete zahrnout, abyste měli jistotu, že mají přístup k firemním datům. Ochrana aplikací se přiřazuje uživatelům, nikoli zařízením, takže firemní data budou zabezpečená bez ohledu na použité zařízení a stav registrace.

Uživatelé, kteří nemají přiřazené zásady ochrany aplikací a nastavení podmíněného přístupu, budou moct ukládat data z jejich podnikového profilu do osobních aplikací a nonmanged místní úložiště na svých mobilních zařízeních. Můžou se také připojit k podnikovým datovým službám, jako je Microsoft Exchange, s osobními aplikacemi.

## <a name="step-6---review--create"></a>Krok 6 – Kontrola a vytvoření

Poslední krok vám umožní zkontrolovat souhrn nastavení, která jste nakonfigurovali. Po zkontrolování výběru klikněte na **vytvořit** a dokončete scénář s asistencí. Po dokončení průvodce se zobrazí tabulka prostředků. Tyto prostředky můžete upravit později. když ale necháte souhrnné zobrazení, tabulka se neuloží.

> [!IMPORTANT]
> Po dokončení průvodce se zobrazí souhrn. Prostředky uvedené v souhrnu můžete upravit později, ale Tabulka zobrazující tyto prostředky se neuloží.

## <a name="next-steps"></a>Další kroky

- Tím, že uživatelům přiřadíte zásady podmíněného přístupu na základě aplikace, aby chránili cloudové služby před odesláním pracovních souborů nechráněným aplikacím, Vylepšili jsme zabezpečení pracovních souborů. Další informace najdete v tématu [nastavení zásad podmíněného přístupu na základě aplikace v Intune](../protect/app-based-conditional-access-intune-create.md).
