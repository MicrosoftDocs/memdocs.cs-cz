---
title: Shromažďování údajů v Intune
titleSuffix: Microsoft Intune
description: Přečtěte si, jak se v Intune shromažďují osobní údaje.
keywords: Ochrana osobních údajů, osobní údaje
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d1171740-936d-46a5-af37-f418bd6fa63e
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: bcd7ff1ae51314bc57be2bed39c7fe8ca7114d82
ms.sourcegitcommit: e2deac196e5e79a183aaf8327b606055efcecc82
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076103"
---
# <a name="data-collection-in-intune"></a>Shromažďování údajů v Intune

Když uživatelé zaregistrují svoje firemní nebo osobní zařízení pomocí Intune, Intune shromáždí, zpracuje a sdílí některá osobní data, aby podporovala obchodní operace, spolupracuje se zákazníkem a podporuje službu. Intune shromažďuje osobní údaje z těchto zdrojů:

- Správci používají Intune v centru pro správu Microsoft Endpoint Manager.
- Zařízení koncových uživatelů (při registraci zařízení pro správu Intune a při jejich používání).
- Zákaznické účty na službách třetích stran (pokyny pro správce).
- Diagnostické informace a informace o výkonu a použití

Z těchto zdrojů Intune shromažďuje informace, které spadají do následujících dvou kategorií: [požadováno](#required-data), [volitelné](#optional-data). V každé z kategorií jsou data dále rozdělena podle zákaznických dat, osobních údajů, diagnostických dat a dat generovaných službou. 

> [!NOTE]
> Žádná data shromážděná naší službou neprodávají z jakéhokoli důvodu žádné třetí straně.

## <a name="required-data"></a>Požadovaná data

Data v požadované kategorii se skládají z dat, která jsou nutná k zajištění práce naší služby podle očekávání zákazníka. Většina dat shromažďovaných službou Intune vyžaduje data. Tato data se vážou k uživateli, zařízení nebo aplikaci a pro správu jako takovou jsou nezbytná. Shromážděná data obsahují osobní údaje i data, která nejsou osobní. Osobní údaje zahrnují identifikovatelná data, která mohou přímo identifikovat koncového uživatele nebo pseudonymovaná data pomocí jedinečného identifikátoru generovaného systémem, který slouží k doručování podnikových služeb uživatelům, k podpoře dat a účtů. Neosobní údaje zahrnují metadata systému generovaná službou a informace o organizacích a klientech. Intune také shromažďuje data o řízení přístupu pro správu přístupu k rolím a funkcím pro správu prostřednictvím funkcí, jako je [Access Control na základě rolí](../fundamentals/role-based-access-control.md).

Požadovaná data shromážděná službou Intune můžou zahrnovat, ale nejsou omezená na tyto akce: 

- Údaje uživatele
  - Jméno vlastníka/zobrazení uživatele (název zaregistrovaný v Azure, který identifikoval uživatel AzureUserID)
  - Hlavní název uživatele nebo e-mailová adresa
  - Telefonní číslo
  - Identifikátory uživatele třetích stran (např. Apple ID)
- Informace o inventáři hardwaru
  - Název zařízení
  - Manufacturer
  - Operační systém
  - Sériové číslo
  - Číslo IMEI
  - IP adresa
  - Wi-Fi MacAddress
  - ICCID
- Informace z protokolů auditů včetně dat o následujících aktivitách
  - Správa
  - Vytvořit
  - Aktualizace (úpravy)
  - Odstranit
  - Přiřadit
  - Vzdálené úlohy
- Informace pro získání podpory
  - Kontaktní informace (jméno, telefonní číslo, e-mailová adresa)
  - E-mailové diskuze s podporou Microsoftu a členy produktových týmů nebo týmů zaměřených na zkušenosti uživatelů
- Informace o řízení přístupu 
  - Statické ověřovatele (heslo zákazníka)
  - Klíče osobních údajů pro certifikáty 
- Informace o správci a účtu
  - Jméno a příjmení uživatele s rolí správce
  - Uživatelské jméno správce
  - Hlavní název uživatele (UPN, e-mail)
  - Telefonní číslo
  - E-mailová adresa vlastníka účtu
  - ID služby Active Directory správce IT každého zákazníka
  - Platební údaje pro fakturaci zákazníka
  - Klíč předplatného
- Inventář aplikací, například
  - Název aplikace
  - verze
  - ID aplikace
  - velikost
  - Umístění instalace
  - Data inventáře aplikací se shromažďují pouze tehdy, pokud je správce označí jako zařízení vlastněné společností nebo pokud je zapnutá funkce aplikace dodržující předpisy.  
- ID tenantů zákaznických třetích stran (například Apple ID)
- Data zařízení
  - ID zařízení v Intune
  - ID zařízení v Azure Active Directory
  - ID správy zařízení v Intune
  - ID tenanta
  - Account ID
  - ID zařízení v EAS
  - ID specifická pro konkrétní platformu
  - AppleID pro zařízení s iOS/iPadOS
  - Adresa MAC zařízení s macOS
  - Windows ID zařízení s Windows
- Informace o spravované aplikaci
  - ID spravované aplikace
  - Značka zařízení spravované aplikace
  - ID správy zařízení v Intune
  - ID zařízení v Azure Active Directory
  - Šifrovací klíče
- Údaje o využití správcem ze všech tenantů Intune (například ovládací prvky pro správu zvolené při interakci s konzolou správce)
- Informace o účtu tenanta (tyto údaje jsou dostupné v okně Intune)
  - Počet zaregistrovaných zařízení nebo uživatelů
  - Počet identifikovaných platforem zařízení  
  - Počet nainstalovaných zařízení
  - installedDeviceCount: Počet zařízení, na kterých je aplikace nainstalovaná
  - notApplicableDeviceCount: Počet zařízení, na kterých se aplikace nedá použít
  - notInstalledDeviceCount: Počet zařízení, na kterých se aplikace dá použít, ale není nainstalovaná
  - pendingInstallDeviceCount: počet zařízení, pro která je aplikace k dispozici, a čeká na instalaci.

## <a name="optional-data"></a>Volitelná data

Data v nepovinné kategorii nejsou pro prostředí produktu nebo služby nezbytná. Zákazníci můžou řídit shromažďování nepovinných dat. Intune umožňuje zákazníkům, aby se odhlásili nebo odhlásili volitelné shromažďování dat. Příklady volitelných dat spočívající v tom, že data Intune shromažďujeme pro diagnostiku a telemetrii. Upozorňujeme, že máme přesvědčivé důvody pro to, aby lidé mohli sdílet tato volitelná data, protože vytváří příležitosti pro nové a bohatší prostředí, ale chápeme, že je důležité poskytnout uživatelům možnost provádět tyto volby sami. 

Příklady volitelných diagnostických dat můžou zahrnovat data o využití aplikací, chyby a data o výkonu. Všechna diagnostická data, která Microsoft shromažďuje během používání jakékoli Microsoft 365 aplikací pro podnikové aplikace a služby, je pseudonymně definovaný v normě ISO/IEC 19944:2017 (oddíl 8.3.3).

## <a name="certain-end-user-data-or-content-is-never-collected"></a>Některá data nebo obsah koncového uživatele se nikdy neshromažďují.

Intune neshromažďuje ani neumožňuje správcům zobrazit volání nebo historii procházení webu koncovými uživateli, osobní e-mail, textové zprávy, kontakty, hesla k osobním účtům, události v kalendáři nebo fotky, včetně těch v aplikaci Photo nebo fotoaparátu. Viz [Začínáme s registrací zařízení](../enrollment/device-enrollment.md).

Další informace o datových typech a definicích najdete v tématu [jak Microsoft kategorizuje data pro online služby](https://www.microsoft.com/trust-center/privacy/customer-data-definitions) . 

## <a name="next-steps"></a>Další kroky

Přečtěte si další informace o tom, jak služba Intune [ukládá a zpracovává](privacy-data-store-process.md) a [sdílí](privacy-data-secure-share.md) osobní údaje. 
