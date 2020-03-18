---
title: Běžné zprávy Endpoint Protection v Microsoft Intune – Azure | Microsoft Docs
description: Přečtěte si téma běžné zprávy a možné řešení při používání a řešení potíží s aplikací Endpoint Protection a programem Microsoft Defender v Microsoft Intune.
keywords: ''
author: Brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/13/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: e31df2d2-bb1b-491b-9a71-04e0b18829c1
ROBOTS: ''
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 16b7cc65ae043fb48b7f500bfcd65195c7ff7561
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79330435"
---
# <a name="endpoint-protection-issues-and-possible-solutions-in-microsoft-intune"></a>Problémy s ochranou koncového bodu a možná řešení v Microsoft Intune

Tento článek obsahuje seznam a popis potenciálních příčin a řešení některých chyb a upozornění. Tyto informace vám pomůžou při řešení problémů při použití aplikace Endpoint Protection.

## <a name="microsoft-defender-error-codes"></a>Kódy chyb programu Microsoft Defender

Zkontrolujte protokoly událostí a chybové kódy, abyste mohli [řešit problémy s antivirovým programem Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/troubleshoot-windows-defender-antivirus).

## <a name="common-intune-errors-and-possible-resolutions"></a>Běžné chyby služby Intune a možná řešení

### <a name="endpoint-protection-engine-unavailable"></a>Modul služby Endpoint Protection není k dispozici.

**Možná příčina**: modul ochrany koncového bodu Intune je poškozený nebo odstraněný.

**Možná řešení**:

- Pokud je Endpoint Protection poškozený nebo se neaktualizuje, aktualizujte nebo přeinstalujte program.
- Vynutit okamžitou aktualizaci. V klientském programu Endpoint Protection (případně na hlavním panelu) vyberte **aktualizovat**.
- V Ovládacích panelech > programy vyberte **Microsoft Intune Endpoint Protection Agent**. Odinstalujte aplikaci.
- Při další synchronizaci aktualizací zjistí program Microsoft Online Management Update Manager chybějící program a v další naplánované době pro instalace ho nainstaluje znova.

### <a name="features-are-disabled"></a>Funkce jsou zakázané.

Může se zobrazit zpráva, že některé funkce jsou zakázané. K těmto zprávám může dojít, pokud správce nevypne službu Intune Endpoint Protection nebo Microsoft Defender pomocí konfiguračního profilu. Nebo je zakázaný koncovým uživatelem na zařízení. Možné zprávy:

`Endpoint Protection disabled`  
`Real-time protection disabled`  
`Download scanning disabled`  
`File and program activity monitoring disabled`  
`Behavior monitoring disabled`  
`Script scanning disabled`  
`Network Inspection System disabled`  

**Možná řešení**: Povolte tyto funkce. Pokyny najdete v těchto tématech:

- [Přidat nastavení ochrany koncových bodů](../protect/endpoint-protection-configure.md)
- [Antivirová ochrana v programu Microsoft Defender](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus)
- [Koncoví uživatelé: zapněte ochranu v reálném čase, abyste měli přístup k prostředkům společnosti.](../user-help/turn-on-defender-windows.md)

### <a name="malware-definitions-out-of-date"></a>Definice malwaru nejsou aktuální

Tento stav ukazuje, kdy jsou definice malwaru na zařízení zastaraly o 14 dní nebo víc. Zpráva může například Ukázat, že zařízení je odpojené od Internetu, nebo jsou definice malwaru zastaralé.

**Možná řešení**: Pokud jsou definice malwaru zastaralé, aktualizujte definice pomocí [antivirové ochrany v programu Microsoft Defender](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus).

### <a name="full-scan-overdue-or-quick-scan-overdue"></a>Zpožděna úplná kontrola nebo zpožděna Rychlá kontrola

Po dobu 14 dnů se úplná kontrola nebo Rychlá kontrola nedokončila. K tomuto scénáři může dojít, pokud se zařízení během úplné kontroly restartuje.

**Možná řešení**: Pokud je kontrola zpožděná, můžete spustit jednorázovou kontrolu nebo naplánovat opakující se kontroly. Viz [antivirová ochrana v programu Microsoft Defender](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus).

### <a name="another-endpoint-protection-application-running"></a>Je spuštěna jiná aplikace ochrany koncových bodů.

Je spuštěná jiná aplikace ochrany koncových bodů a zařízení je v pořádku.

**Možná řešení**: Pokud je nainstalovaná jiná aplikace ochrany koncových bodů a Intune tuto aplikaci detekuje, může se stát, že se zařízení nestabilní.

## <a name="next-steps"></a>Další kroky

Získejte pomoc [od Microsoftu](get-support.md)nebo využijte [komunitní fóra](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).
