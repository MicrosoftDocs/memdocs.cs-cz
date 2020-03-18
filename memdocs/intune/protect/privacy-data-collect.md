---
title: Shromažďování údajů v Intune
titleSuffix: Microsoft Intune
description: Přečtěte si, jak se v Intune shromažďují osobní údaje.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/18/2018
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
ms.openlocfilehash: e986a6dcb598a11a0f2906d6d7be8e2e1abb6aba
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79329119"
---
# <a name="data-collection-in-intune"></a>Shromažďování údajů v Intune

Když si uživatelé zaregistrují svá firemní nebo osobní zařízení pomocí Intune, některé z jejich osobních údajů se shromažďují a sdílí. Intune shromažďuje osobní údaje z těchto zdrojů:

- Využití služby Intune na portálu Azure Portal správcem
- Zařízení koncových uživatelů (při registraci ke správě Intune a v průběhu využívání)
- Účty zákazníků u služeb třetích stran (podle pokynů správce)
- Diagnostické informace a informace o výkonu a použití

Z těchto zdrojů shromažďuje Intune informace, které spadají do těchto tří kategorií: [identifikované](#identified-data), [pseudonymizované](#pseudonymized-data) a [agregované](#aggregated-data) údaje.

> [!NOTE]
> Žádná data shromážděná naší službou neprodávají z jakéhokoli důvodu žádné třetí straně.

## <a name="identified-data"></a>Identifikované údaje

Většina osobních údajů shromážděných službou Intune představuje identifikované údaje. Tato data se vážou k uživateli, zařízení nebo aplikaci a pro správu jako takovou jsou nezbytná. Slouží ke správě zařízení a aplikací uživatele a poskytování služby Intune.

Mezi identifikovaná data shromažďovaná službou Intune patří mimo jiné: 

- Informace o uživateli
  - Jméno vlastníka / zobrazované jméno uživatele (jméno uživatele zaregistrované v Azure, které označuje ID uživatele služby Azure)
  - Hlavní název uživatele nebo e-mailová adresa
  - Identifikátory uživatele třetích stran (např. Apple ID)
- Informace o inventáři hardwaru
  - Název zařízení
  - Výrobce
  - Operační systém
  - Sériové číslo
  - Číslo IMEI
  - IP adresa
  - Wi-Fi MacAddress
  - ICCID
  - Telefonní číslo
- Informace z protokolů auditů včetně dat o následujících aktivitách
  - Spravovat
  - Vytvořit
  - Aktualizace (úpravy)
  - Odstranit
  - Přiřadit
  - Vzdálené úlohy
- Informace o podpoře
  - Kontaktní informace (jméno, telefonní číslo, e-mailová adresa)
  - E-mailové diskuze s podporou Microsoftu a členy produktových týmů nebo týmů zaměřených na zkušenosti uživatelů
- Informace o řízení přístupu (Intune tato data využívá ke správě přístupu k rolím a funkcím pro správu prostřednictvím funkcí, jako je [Řízení přístupu založené na rolích](../fundamentals/role-based-access-control.md).)
  - Statické ověřovače (heslo zákazníka)
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
  - Verze nástroje
  - ID aplikace
  - Velikost
  - Umístění instalace
  - Data inventáře aplikací se shromažďují pouze tehdy, pokud je správce označí jako zařízení vlastněné společností nebo pokud je zapnutá funkce aplikace dodržující předpisy.  
- Zákaznická ID tenantů třetích stran, jako je Apple ID 

## <a name="pseudonymized-data"></a>Pseudonymizované údaje

Pseudonymizované údaje jsou přidružené k jedinečnému identifikátoru (zpravidla systémem vygenerovanému číslu), který jako takový nedokáže identifikovat jednotlivce, ale slouží k poskytování podnikových služeb uživatelům. 

Mezi pseudonymizované údaje shromažďované službou Intune patří mimo jiné: 

- Diagnostické informace a informace o výkonu a použití svázané s uživatelem a/nebo zařízením
  - Počet použití funkce
  - Příkazy zadané funkci
  - Doba odezvy služby
  - Úspěšnost instalací a dalších procesů
  - Chyby aplikace Portál společnosti Intune
  - Identifikátory uživatele a zařízení
  - Identifikátory pro účely reference, korelace a správy 
- Data zařízení nesvázaná se zařízením nebo uživatelem (jsou-li svázaná se zařízením nebo uživatelem, Intune s nimi nakládá jako s identifikovanými údaji)
  - ID zařízení v Intune
  - ID zařízení v Azure Active Directory
  - ID správy zařízení v Intune
  - ID tenanta
  - ID účtu
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

## <a name="aggregated-data"></a>Agregované údaje

Agregované údaje slouží k poskytování a zlepšování služby Intune. 

Mezi agregované údaje shromažďované službou Intune patří mimo jiné: 

- Údaje o využití správcem ze všech tenantů Intune (například ovládací prvky pro správu zvolené při interakci s konzolou správce)
- Informace o účtu tenanta (tyto údaje jsou dostupné v okně Intune)
  - Počet zaregistrovaných zařízení nebo uživatelů
  - Počet identifikovaných platforem zařízení  
  - Počet nainstalovaných zařízení
  - installedDeviceCount: Počet zařízení, na kterých je aplikace nainstalovaná
  - notApplicableDeviceCount: Počet zařízení, na kterých se aplikace nedá použít
  - notInstalledDeviceCount: Počet zařízení, na kterých se aplikace dá použít, ale není nainstalovaná
  - pendingInstallDeviceCount: počet zařízení, pro která je aplikace k dispozici, a čeká na instalaci.

## <a name="next-steps"></a>Další kroky

Přečtěte si další informace o tom, jak služba Intune [ukládá a zpracovává](privacy-data-store-process.md) a [sdílí](privacy-data-secure-share.md) osobní údaje. 
