---
title: Windows Autopilot se spolusprávou
titleSuffix: Configuration Manager
description: Pomocí nástroje Windows autopilot pro spolusprávu v Configuration Manager můžete zjednodušit nastavení nových zařízení s Windows 10.
ms.date: 07/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: e3e3c97f-5945-49ab-a622-9f6fe6b9737e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f77cb76e3cfd9c932a6f3789f98e5616cdaa27eb
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546429"
---
# <a name="windows-autopilot-with-co-management"></a>Windows Autopilot se spolusprávou

Přijímání nových zařízení s Windows 10 je skvělé. Nicméně může trvat nějakou dobu, než se nakonfigurují všechna nastavení a aplikace, abyste mohli být produktivní. Spoluspráva řeší tento problém zřizování zařízení pomocí automatického pilotního projektu Windows.

Tento autopilot nabízí pro vás i uživatele zjednodušené prostředí v následujících situacích:
- Nastavení a Předkonfigurace nových zařízení s Windows 10  
- Resetování, recyklace a obnovení stávajících zařízení  

Proces autopilotu zkracuje čas, prostředky a složitost spojené s nasazením, správou a vyřazením zařízení. Zároveň je prostředí pro vaše uživatele zjednodušené a snadné při prvním spuštění.

Windows autopilot podporuje několik scénářů, z nichž všechny jsou maximalizovány společně s spolusprávou:

- Uživatelé můžou řídit vlastní nasazení nových zařízení do služby Active Directory s využitím hybridního připojení k Azure AD nebo Azure Active Directory (Azure AD).  

- Můžete nastavit samoobslužné nasazení nových nasazení zařízení do služby Azure AD pro sdílená zařízení a veřejné terminály.  

- S Windows autopilotem pro stávající zařízení použijte Configuration Manager k migraci stávajícího zařízení ze systému Windows 7 a služby Active Directory do systému Windows 10 a Azure AD.  

V následujícím videu vedoucí program Danny Guillory a hlavní správce programu Andrew blog projednávají a demonstrační Windows autopilot s spolusprávou:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Windows-Autopilot-with-Co-Management/player]



## <a name="benefits"></a>Výhody

Pokud používáte spolusprávu a autopilotní společně, ujistěte se, že nová zařízení, která vstupují do vaší sítě, skončí ve stejném stavu správy. V tomto nastavení jsou zařízení zaregistrovaná v Intune a musí mít klienta Configuration Manager.  Umožňuje používat nový model zřizování Windows 10 a pomáhá eliminovat nutnost vytvářet, udržovat a aktualizovat vlastní image operačního systému. 

Ve všech těchto scénářích můžete automaticky [Povolit spolusprávu](how-to-prepare-Win10.md) pomocí Intune. Tato automatizace pomáhá procesu zřizování a průběžné správě zařízení.

Díky autopilotu se nemusíte starat o image a ovladače. Zaměřte se na zřizování zařízení díky tomuto automatizovanému procesu pomocí Intune a Configuration Manager prostřednictvím spolusprávy.


V tuto chvíli vám může pomoci použití spolusprávy a automatického pilotního nasazení:

#### <a name="reduce-time-costs-and-complexity"></a>Snížení času, nákladů a složitosti
Windows autopilot používá verzi Windows 10 optimalizovanou pro výrobce OEM, která je v zařízení předinstalována. Tato konfigurace ukládá organizacím úsilí, abyste zachovali vlastní image a ovladače pro každý model používaného zařízení. Namísto obnovování imagí zařízení Transformujte existující instalaci Windows 10 na stav "připraveno pro účely podnikání". Aplikuje nastavení a zásady, nainstaluje aplikace a změní edici Windows 10. Například upgrade z Windows 10 pro na Windows 10 Enterprise, abyste mohli podporovat pokročilé funkce.

#### <a name="improve-the-user-experience"></a>Vylepšení uživatelského prostředí
Nejlepší uživatelské prostředí způsobuje nejnižší přerušení a pomůže vám se vrátit k zaměření na jejich práci. Windows autopilot nabízí jednoduchý přístup, který uživatelům pomůže rychle nastavit pomocí několika jednoduchých kliknutí a jejich přihlašovacích údajů Azure AD. V mnoha organizacích s velkým polem vzdálených zaměstnanců použijte k dodávání nových zařízení přímo od výrobce Windows autopilot.

#### <a name="use-autopilot-and-configuration-manager-to-migrate-existing-windows-7-devices-to-windows-10"></a>Použití autopilotu a Configuration Manager k migraci stávajících zařízení se systémem Windows 7 do Windows 10
Pomocí nástroje Windows autopilot pro existující zařízení vytvoříte konfigurační soubor a nasadíte ho pomocí Configuration Manager pořadí úkolů. Tento proces snadno migruje stávající zařízení ze systému Windows 7 na Windows 10. Použijete podpisovou image Windows 10 v Configuration Manager a pak ji použijete na stávající zařízení s Windows 7 s konfigurací autopilotu. Když uživatel zařízení spustí, použije proces zprovoznění řízený uživatelem pomocí automatického pilotního nasazení.

Tady jsou kroky pro autopilot pro existující zařízení:

![Přehled procesu pro Windows autopilot pro existující zařízení](media/autopilot-for-existing-devices.png)

1. Nasazení zásad skupiny pro přesměrování známých složek na OneDrive
2. Generovat konfigurační soubor autopilotu
3. Nasazení pořadí úkolů pro upgrade na Windows 10
4. Počítač s Windows 10 se při prvním spuštění prochází prostřednictvím autopilotu.

#### <a name="modernizing-device-provisioning-for-all-types-of-workers"></a>Zřizování zařízení modernizaci pro všechny typy pracovních procesů
Pomocí automatického pilotního nasazení teď můžete poskytnout bezplatná nasazení operačního systému pro Unmanned zařízení nebo sdílená zařízení pomocí režimu samoobslužného nasazování. Toto nastavení vyhovuje potřebám všech vašich různých typů pracovníků. Funkce resetování Windows autopilotu navíc zajišťuje, že opětovné zřízení zařízení pro nového uživatele je jednoduché a snadné. Tento proces zjednodušuje, co je tradičně obtížná úloha, když máte sezónní nebo smluvní pracovní procesy. 



## <a name="case-study"></a>Případová studie

Německý logistická a železniční dopravní společnost Schenker používá k zvýšení produktivity zaměstnanců a uvolnění IT týmů, aby na každodenních úkolech podpory pracovali. DATABÁZE Schenker se přesunula z tradičních imagí a nahradila ji prostřednictvím zřizování přes Cloud. Nyní používají Azure AD – připojení a Intune, aby bylo možné rychle začít pracovat s novými zařízeními. 

Místo toho, aby se jejich vzdálené pracovní procesy vyčistily do umístění se službami IT, používá DB Schenker nyní Windows autopiloting. Dodávají své pracovníky hardwaru přímo od výrobce do své místní kanceláře. Pracovní proces připojí nové zařízení k Internetu a přihlásí se pomocí svých přihlašovacích údajů Azure AD. Zařízení se pak připojí k aplikacím a službám, které Schenker IT oddělení DB přiřadí k individuálnímu profilu uživatele.

Další informace najdete v tématu [globální logistická jednotka, která je v ní zaměstnanci s moderními digitálními pracovišti](https://customers.microsoft.com/story/db-schenker-travel-transportation-windows-10).



## <a name="value-proposition"></a>Pozice hodnoty

Vytvořte si ve své organizaci uspokojivý zážitek tím, že vytvoříte lepší uživatelské prostředí pro uživatele. Pomocí programu Windows autopilot můžete zvýšit náklady. Uvolněte čas a Zaměřte se na další projekty, abyste mohli zvýšit hodnotu a dopad vaší organizace.



## <a name="configure"></a>Konfigurace

Další informace najdete v následujících článcích:

[Vytváření profilů Windows autopilotu pomocí Intune](https://docs.microsoft.com/intune/enrollment-autopilot)

[Windows Autopilot pro existující zařízení](../../autopilot/existing-devices.md)
