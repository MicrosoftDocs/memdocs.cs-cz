---
title: nastavení dodržování předpisů pro zařízení macOS v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na seznam všech nastavení, která můžete použít při nastavování dodržování předpisů pro zařízení macOS v Microsoft Intune. Vyžadovat ochranu před integritou systému od společnosti Apple, nastavit omezení hesla, vyžadovat bránu firewall, dovolit server gatekeeper a další.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/22/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 210ec5ea6acc2d0ce91a93c83991b630a6fdbb4d
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329679"
---
# <a name="macos-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>nastavení macOS a označení zařízení jako kompatibilních nebo nekompatibilních s použitím Intune

Tento článek obsahuje seznam a popis různých nastavení dodržování předpisů, která můžete nakonfigurovat na zařízeních macOS v Intune. Jako součást řešení správy mobilních zařízení (MDM) pomocí těchto nastavení můžete nastavit minimální nebo maximální verzi operačního systému, nastavit vypršení platnosti hesla a další.

Tato funkce platí pro:

- macOS

Jako správce Intune můžete pomocí těchto nastavení dodržování předpisů ochránit prostředky vaší organizace. Další informace o zásadách dodržování předpisů a o tom, co dělají, najdete v tématu [Začínáme s dodržováním předpisů pro zařízení](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte zásadu dodržování předpisů](create-compliance-policy.md#create-the-policy). U možnosti **Platforma** vyberte **macOS**.

## <a name="device-health"></a>Stav zařízení

- **Vyžadovat ochranu integrity systému**:  
  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Vyžadovat** – vyžaduje, aby zařízení MacOS měla [ochranu integrity systému](https://support.apple.com/HT204899) (otevře web společnosti Apple) povolenou.  

## <a name="device-properties"></a>Vlastnosti zařízení

- **Minimální požadovaný operační systém**:  
  Pokud zařízení nesplňuje požadavek na minimální verzi operačního systému, nahlásí se jako nevyhovující. Zobrazí se odkaz s informacemi, jak upgradovat. Uživatel zařízení si může upgradovat svoje zařízení. Pak mají přístup k prostředkům organizace.

- **Maximální povolená verze operačního systému**:  
  Pokud zařízení používá verzi operačního systému, která je novější než verze v pravidle, bude přístup k prostředkům organizace blokovaný. Uživateli zařízení se zobrazí výzva, aby kontaktoval správce IT. Zařízení nemá přístup k prostředkům organizace, dokud se nezmění pravidlo, které povoluje verzi operačního systému.

- **Minimální verze buildu operačního systému**:  
  Když Apple publikuje aktualizace zabezpečení, číslo sestavení se obvykle aktualizuje, nikoli verze operačního systému. Pomocí této funkce lze zadat číslo minimální povolenou sestavení na zařízení.

- **Maximální verze buildu operačního systému**:  
  Když Apple publikuje aktualizace zabezpečení, číslo sestavení se obvykle aktualizuje, nikoli verze operačního systému. Pomocí této funkce lze zadat maximální povolené sestavení číslo na zařízení.

## <a name="system-security-settings"></a>Systémové nastavení zabezpečení

### <a name="password"></a>Heslo

- **Vyžadovat heslo k odemknutí mobilních zařízení**:  
  - **Nenakonfigurováno** (*výchozí*)
  - **Vyžadovat** Uživatelé musí zadat heslo, aby mohli získat přístup ke svému zařízení.

- **Jednoduchá hesla**:  
  - **Nenakonfigurováno** (*výchozí*) – uživatelé můžou vytvářet hesla, která jsou jednoduchá jako **1234** nebo **1111**.
  - **Blok** – uživatelé nemůžou vytvářet jednoduchá hesla, třeba **1234** nebo **1111**.

- **Minimální délka hesla**:  
  Zadejte minimální počet číslic nebo znaků, které musí heslo obsahovat.

- **Typ hesla**: Zvolte, jestli má heslo obsahovat pouze **číselné** znaky, nebo jestli má obsahovat kombinaci čísel a dalších znaků (**alfanumerické**).

- **Počet nealfanumerických znaků v hesle**:  
  Zadejte minimální počet speciálních znaků, například `&`, `#`, `%`, `!`a tak dále, které musí být v hesle.

  Po nastavení vyššího čísla bude uživatel muset vytvořit složitější heslo.

- **Maximální počet minut nečinnosti před vyžadováním hesla**:  
  Zadejte dobu nečinnosti, než uživatel musí znovu zadat heslo.

- **Vypršení platnosti hesla (dny)** :  
  Vyberte počet dní, po jejichž uplynutí vyprší platnost hesla, a musí vytvořit nové.

- **Počet předchozích hesel, která zabrání opakovanému použití**:  
  Zadejte počet dříve použitých hesel, která se nedají použít.
> [!IMPORTANT]
> Když se požadavek na heslo na zařízení s macOS změní, projeví se to až při příští změně hesla uživatelem. Pokud třeba nastavíte omezení délky hesla na osm číslic a zařízení s macOS má aktuálně šestičíselné heslo, bude zařízení dál splňovat předpisy až do doby, kdy uživatel heslo na zařízení aktualizuje.

### <a name="encryption"></a>Šifrování

- **Šifrování datového úložiště na zařízení**:  
  - **Nenakonfigurováno** (*výchozí*)
  - **Vyžadovat** *– použít k* šifrování úložiště dat na vašich zařízeních.

### <a name="device-security"></a>Zabezpečení zařízení

Firewall chrání zařízení před neoprávněným přístupem do sítě. Pomocí firewallu můžete ovládat připojení pro jednotlivé aplikace. 

- **Brána firewall**:  
  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení vypne bránu firewall a síťový provoz je povolen (není zablokovaný).
  - **Povolit** – pomocí *Povolit* můžete chránit zařízení před neoprávněným přístupem. Aktivace této funkce vám umožní zpracovávat příchozí internetová připojení a používat neviditelný režim. 

- **Příchozí připojení**:  
  - **Nenakonfigurováno** (*výchozí*) – povolí příchozí připojení a sdílení služeb.
  - **Blok** – zablokuje všechna příchozí síťová připojení s výjimkou připojení požadovaných pro základní internetové služby, jako jsou DHCP, Bonjour a IPSec. Toto nastavení také blokuje všechny služby sdílení, včetně sdílení obrazovky, vzdáleného přístupu, sdílení hudby v iTunes a dalších.  

- **Neviditelný režim**:  
  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení ponechá neviditelný režim vypnutý.
  - **Povolit** – zapnout režim utajení, který zabrání zařízením v reakci na požadavky na zjišťování, které se dají uživatelům se zlými úmysly udělat. Při aktivaci této možnosti bude zařízení oprávněným aplikacím dále odpovídat na příchozí požadavky.  

### <a name="gatekeeper"></a>Gatekeeper

Další informace najdete v tématu [gatekeeper na MacOS](https://support.apple.com/HT202491) (Otevírá web společnosti Apple).

**Povolit aplikace stažené z těchto míst**: Povolí instalaci podporovaných aplikací na vaše zařízení z různých umístění. Možnosti umístění:

- **Nenakonfigurováno** (*výchozí*) – možnost serveru gatekeeper nemá žádný vliv na dodržování předpisů nebo nedodržování předpisů.  
- **Mac App Store** – nainstalujte jenom aplikace pro Mac App Store. Aplikace jiných výrobců ani identifikovaných vývojářů nelze nainstalovat. Pokud uživatel vybere Gatekeeper pro instalaci aplikací z umístění mimo Mac App Store, považuje se zařízení za nevyhovující předpisům.
- **Mac App Store a identifikování vývojáři** – nainstalujte aplikace pro Mac App Store a od identifikovaných vývojářů. macOS zkontroluje identitu vývojářů a provede několik dalších kontrol, aby ověřil integritu aplikace. Pokud uživatel vybere Gatekeeper pro instalaci aplikací z umístění mimo tyto možnosti, považuje se zařízení za nevyhovující předpisům.
- **Odkudkoli** – aplikace můžete instalovat odkudkoli a jakýmkoli vývojářem. Jedná se o nejméně bezpečnou možnost.
 

## <a name="next-steps"></a>Další kroky

- [Přidejte akce pro zařízení nedodržující předpisy](actions-for-noncompliance.md) a [použijte značky oboru k filtrování zásad](../fundamentals/scope-tags.md).
- [Monitorujte zásady dodržování předpisů](compliance-policy-monitor.md).
- Podívejte se na [nastavení zásad dodržování předpisů pro](compliance-policy-create-ios.md) zařízení s iOS.