---
title: Akce a možnosti Intune podporované při registraci uživatele Apple
titleSuffix: Microsoft Intune
description: Zjistěte, které akce a možnosti Intune se podporují při registraci uživatele Apple.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 2/14/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: aa78178f6649e0199aa2de96bac2725ba55208ae
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331531"
---
# <a name="intune-actions-and-options-supported-with-apple-user-enrollment"></a>Akce a možnosti Intune podporované při registraci uživatele Apple

Zápis uživatele podporuje podmnožinu možností správy zařízení. Pokud se pro zařízení registrace uživatele použije už existující konfigurační profil, na toto zařízení se použijí jenom nastavení podporovaná zápisem uživatele.

> [!NOTE]
> Podpora registrace uživatelů společnosti Apple v Intune je momentálně ve verzi Preview pro iOS a iPadOS.

## <a name="password-settings"></a>Nastavení hesla

Pokud nakonfigurujete nastavení hesla na zařízeních pro zápis uživatelů, nastavení **jednoduchého hesla** se automaticky nastaví na **blokování**a VYnutil se kód PIN pro číslice 6.

Například nakonfigurujete nastavení **vypršení platnosti hesla** a tuto zásadu nahrajete do zařízení zaregistrovaných uživatelem. V zařízeních dojde k následujícímu:
- Nastavení **vypršení platnosti hesla** je ignorováno.
- Jednoduchá hesla, například `111111` nebo `123456`, nejsou povolena.
- Je vynutil kód PIN pro číslice 6.

## <a name="administrator-remote-device-actions-and-options"></a>Akce a možnosti vzdáleného zařízení pro správu
Správci můžou na zařízeních pro zápis uživatelů provádět následující akce a možnosti:
- Vyřadit
- Odstranit
- Vzdálené uzamčení
- Synchronizovat

Všechny ostatní akce nejsou podporovány.

## <a name="end-user-actions"></a>Akce koncového uživatele
Na zařízeních pro zápis uživatelů můžou koncoví uživatelé provádět tyto akce na svých zařízeních z Portál společnosti aplikace a webu:
- Změňte. Tato akce se vztahuje pouze na uživatelské jméno v rámci Portál společnosti. Zařízení nebude plně přejmenováno mimo tento kontext.
- Odebrat
- Vzdálené uzamčení
- Stav kontroly

## <a name="app-deployment-options"></a>Možnosti nasazení aplikace
Na zařízeních pro zápis uživatelů se dají nasadit následující typy aplikací:
- Uživatelem licencované aplikace plánu pro plánování multilicencí (VPP) včetně vlastních aplikací
- Obchodní aplikace (LOB)
- Webové aplikace

## <a name="other-supported-options"></a>Další podporované možnosti

V Intune se podporují následující možnosti pro zařízení zaregistrovaná pomocí registrace uživatele Apple:
- SÍŤ VPN pro jednotlivé aplikace Tato podpora vyloučí domény Safari, protože zápis uživatele nepodporuje konfiguraci nastavení Safari.
- Wi-Fi 
- Odebrání podnikové aplikace při zrušení registrace
- Detekce jailbreaků

Podporovaná jsou tato omezení:
- Zobrazení firemních dokumentů v nespravovaných aplikacích
- Zobrazení nefiremních dokumentů v podnikových aplikacích
- Povolení čtení nespravovaných aplikací ze spravovaných účtů kontaktů
- Přetažení jako nespravovaného cíle
- Požadované šifrované zálohování
- Synchronizace spravovaných aplikací do cloudu
- Přístup k řídicímu centru při uzamčeném zařízení
- Přístup k centru oznámení, když je zařízení uzamčené
- Zobrazení dnes, když je zařízení uzamčené
- Blokovat snímky obrazovky
- Blokovat zálohování podnikových knih
- Blokovat synchronizaci metadat v podnikovém adresáři
- Vyžadovat šifrované zálohování
- Vyžadovat sledovat detekci zápěstí
- Zablokovat Siri
- Zablokovat Siri, když je zařízení uzamčené
- Vyžadovat upozornění na podvod Safari
- Blokovat odeslání diagnostiky do Applu


## <a name="options-not-supported"></a>Možnosti nejsou podporovány.
V zařízeních zaregistrovaných pomocí zápisu uživatelů nejsou podporovány následující možnosti. Pokud tyto možnosti potřebujete, podívejte se na registraci zařízení u zařízení vlastněných osobně nebo na automatický zápis zařízení pro podniková zařízení.
- Shromážděte inventář aplikací pro aplikace mimo spravovaný svazek APFS.
- Shromažďování inventáře certifikátů a zřizovacích profilů mimo spravovaný svazek APFS
- Shromážděte UDID a další identifikátory trvalého zařízení.
- Registrace uživatele pro každé zaregistrované zařízení podporuje jedinečné ID registrace, ale toto ID po zrušení registrace nezachovají.
- Následující funkce Intune se kvůli tomuto omezení nepodporují:
- Profily uživatelů SCEP s formátem názvu subjektu sériového čísla.
- SÍŤ VPN na úrovni zařízení.
- Nasazení aplikace VPP licencované pro zařízení
- Nainstalujte aplikace z App Storu jako spravované aplikace.
- Řízení MDM pro aplikace mimo spravovaný svazek APFS
- Zásady ochrany aplikací se pro tyto aplikace stále použijí. Nebudete ale moct převzít správu ani nasadit spravované verze těchto aplikací, pokud je uživatel ze zařízení neodstraní.
- Akce, konfigurace, nastavení a příkazy vyžadující dohled. 


## <a name="known-issues-in-preview"></a>Známé problémy ve verzi Preview
- Odvolání licence VPP: oznámení, že licence byla odvolána, se nezobrazí. Aktuální chování je, že odvolání je úspěšné, ale koncový uživatel není upozorněn. 
- Vytváření sestav aplikací VPP: v sestavě umístěné v klientských aplikacích > aplikace > [název aplikace] > stav instalace zařízení, aplikace VPP nasazené do zařízení zaregistrovaných uživateli se hlásí jako neúspěšná, i když se aplikace úspěšně nasadila do zařízení. 
- Vytváření sestav aplikací: u typů aplikací nepodporovaných při zápisu uživatelů mohou sestavy poskytnout nepodstatné chybové zprávy. 
- Portál společnosti App Experience: uživatelům se zobrazí všechny aplikace, které jsou jí cílené, bez ohledu na to, jestli jsou tyto typy aplikací podporované pro zařízení zaregistrovaná uživatelem. 
- Portál společnosti App Experience: uživatelům se zobrazí stejný text, který označuje, co můžou organizace zobrazit pro registraci uživatelů a zařízení, pokud správce přizpůsobil text, který indikuje, co organizace neuvidí.


## <a name="next-steps"></a>Další kroky

[Nastavení registrace uživatelů pro iOS/iPadOS a iPadOS](ios-user-enrollment.md)
