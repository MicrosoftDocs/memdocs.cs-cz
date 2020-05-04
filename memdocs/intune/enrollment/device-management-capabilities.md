---
title: Možnosti správy zařízení v Microsoft Intune
description: Přečtěte si toto téma a zjistěte, jak vám může Intune pomoct spravovat zaregistrovaná zařízení.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/16/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ROBOTS: NOINDEX,NOFOLLOW
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2dea6d5af4356526c2df1b23d47fb468c6213e0c
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "79331591"
---
# <a name="enrolled-device-management-capabilities-of-microsoft-intune"></a>Možnosti správy zaregistrovaných zařízení v Microsoft Intune

Microsoft Intune umožňuje spravovat řadu zařízení tím, že je *zaregistruje*. Některé typy zařízení můžete zaregistrovat sami, nebo je můžou zaregistrovat uživatelé pomocí aplikace *Portál společnosti*. Registrace umožňuje procházet a instalovat aplikace, zajistěte, aby jejich zařízení vyhovovala podnikovým zásadám a kontaktovalo IT oddělení IT.

Tento článek obsahuje úplný seznam funkcí, které získáte po registraci zařízení.

Správa, inventarizace, nasazování aplikací, zřizování a vyřazení z provozu se procházejí prostřednictvím Intune v Azure Portal.

Uživatelé získají přístup k portálu společnosti, odkud můžou instalovat aplikace a registrovat a odebírat zařízení a odkud můžou snadno kontaktovat IT oddělení nebo technickou podporu.



## <a name="device-security-and-configuration"></a>Konfigurace a zabezpečení zařízení

|Schopnost|Podrobnosti|Další informace|
|--------------|-----------|--------------------|
|Zásady konfigurace<br><br>Vlastní zásady| Umožňují spravovat množství nastavení a funkcí na mobilních zařízeních ve vaší organizaci. Můžete třeba vyžadovat heslo, omezit počet neúspěšných pokusů o přihlášení, určit dobu, po které se uzamkne obrazovka zařízení, nastavit dobu platnosti hesla a zabránit nastavení už použitých hesel. Můžete také řídit použití funkcí hardwaru a softwaru, jako je třeba fotoaparát zařízení nebo webový prohlížeč.<br><br>Vlastní zásady použijte v případě, že zásady konfigurace neobsahují nastavení, které požadujete. Pro zařízení s iOS/iPadOS můžete importovat nastavení, která jste exportovali z nástroje Apple Configuratoru. Pro další zařízení můžete pomocí nastavení OMA-URI (Open Mobile Alliance Uniform Resource Identifier) nakonfigurovat nastavení a funkce v zařízení.|[Správa nastavení a funkcí na zařízeních pomocí zásad Microsoft Intune](../protect/device-compliance-get-started.md)|
|Vzdálené vymazání, Vzdálené uzamčení a Resetování hesla|V případě ztráty nebo odcizení zařízení je možné vymazat citlivá data. Zařízení můžete třeba vzdáleně uzamknout, obnovit do továrního nastavení nebo vymazat jenom firemní data.<br><br>Můžete resetovat hesla, když uživatelé ztratí přístup ke svým zařízením, uzamknout ztracená nebo odcizená zařízení nebo z takových zařízení dokonce vymazat data.|Chraňte svá zařízení pomocí [vzdáleného zámku](../remote-actions/device-remote-lock.md) a [resetování hesla](../remote-actions/device-passcode-reset.md) .|
|Celoobrazovkový režim|Umožňuje uzamknout určité funkce mobilních zařízení, třeba snímek obrazovky a vypínač. Umožňuje taky omezit zařízení tak, aby v nich mohla běžet jenom jedna vámi určená aplikace. |[Nastavení zásad konfigurace pro iOS v Microsoft Intune](../configuration/device-restrictions-ios.md)|
|Obnovení nastavení AutoPilot|Odešle úlohu na zařízení, aby se proces resetování spouštěl vzdáleně, aby nemuseli pracovníci IT nebo jiní správci navštěvovat jednotlivé počítače, aby mohli tento proces spustit. Když se na zařízení používá resetování autopilotního projektu, primární uživatel zařízení se odebere. Další uživatel, který se přihlásí po obnovení, se nastaví jako primární uživatel.|[Resetování vzdáleného Windows autopilotu](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)|

## <a name="app-management"></a>Správa aplikací

|Schopnost|Podrobnosti|Další informace|
|--------------|-----------|--------------------|
|Správa a nasazení aplikací|Poskytuje řadu nástrojů, které vám pomůžou spravovat mobilní aplikace v průběhu jejich životního cyklu, včetně nasazení aplikací z instalačních souborů a obchodů s aplikacemi, podrobného sledování stavu aplikací a jejich odebrání.|[Nasazení aplikací v Microsoft Intune](../apps/apps-deploy.md)|
|Kompatibilní a nekompatibilní aplikace|Umožňuje určit seznam kompatibilních aplikací (které uživatelé můžou nainstalovat) a nekompatibilních aplikací (které uživatelé nainstalovat nesmí).|[Nastavení zásad pro iOS v Microsoft Intune](../configuration/device-restrictions-ios.md)|
|Správa mobilních aplikací|Konfiguruje omezení pro aplikace pomocí správy mobilních aplikací jak pro zařízení, která spravujete v Intune, tak pro zařízení, která Intune nespravuje. Můžete zvýšit zabezpečení firemních dat omezením operací, jako je kopírování a vkládání, externí zálohování dat a přenos dat mezi aplikacemi.|[Konfigurace a nasazení zásad správy mobilních aplikací v konzole Microsoft Intune](../developer/app-wrapper-prepare-android.md)|
|Konfigurace mobilních aplikací pro iOS|Pomocí zásad konfigurace mobilních aplikací poskytuje nastavení pro aplikace pro iOS/iPadOS, které se můžou požadovat, když uživatel spustí aplikaci. Aplikace může například vyžadovat, aby uživatel zadal číslo portu nebo přihlašovací informace. Můžete zjednodušit konfiguraci aplikace a snížit počet volání podpory.|[Konfigurace aplikací pro iOS/iPadOS pomocí zásad konfigurace mobilních aplikací v Microsoft Intune](../apps/app-configuration-policies-use-ios.md)|
|profily zřizování mobilních aplikací pro iOS/iPadOS|Pomůže vám nasadit zřizovací profily pro aplikace iOS/iPadOS, které se blíží vypršení platnosti. |[Použití mobilních zásad zřizovacích profilů pro iOS/iPadOS k zabránění vypršení platnosti vašich aplikací](../apps/app-provisioning-profile-ios.md)|
|Spravovaný prohlížeč|Konfiguruje zásady spravovaného prohlížeče pro kontrolu nad weby, které uživatelé můžou navštěvovat. Pro spravovaný prohlížeč můžete taky použít zásady správy mobilních aplikací.|[Správa přístupu k Internetu pomocí zásad spravovaného prohlížeče pomocí Microsoft Intune](../apps/app-configuration-managed-browser.md)|
|Windows Hello pro firmy|Umožňuje integraci se službou Microsoft Hello pro firmy. Tato alternativní metoda pro přihlašování do Windows 10 pomocí místní služby Active Directory nebo Azure Active Directory může nahradit hesla, čipové karty a virtuální čipové karty.|[Řízení nastavení Windows Hello pro firmy na zařízeních pomocí Microsoft Intune](../protect/windows-hello.md)|
|Hromadně zakoupené aplikace|Pomůže spravovat aplikace, které jste koupili prostřednictvím programu hromadného nákupu, importováním licenčních informací z App Storu, sledováním, kolik licencí jste už použili, a zabráněním instalace více aplikací, než na kolik máte licence.|[Správa hromadně koupených aplikací v Microsoft Intune](../apps/vpp-apps.md)|

## <a name="company-resource-access"></a>Přístup k prostředkům společnosti

|Schopnost|Podrobnosti|Další informace|
|--------------|-----------|--------------------|
|Profily certifikátů|Vytvoří a nasadí profily důvěryhodných certifikátů a certifikáty protokolu SCEP (Simple Certificate Enrollment Protocol), které se dají použít k zabezpečení a ověření profilů sítí Wi-Fi, VPN a e-mailu.|[Zabezpečení přístupu k prostředkům pomocí profilů certifikátů v Microsoft Intune](../protect/certificates-configure.md)|
|Profily sítě Wi-Fi|Nasadí uživatelům nastavení bezdrátových sítí. Nasazením těchto nastavení minimalizujete úsilí uživatelů potřebné k připojení k firemní síti.|[Připojení Wi-Fi v Microsoft Intune](../configuration/wi-fi-settings-configure.md)|
|E-mailové profily.|Vytvoří a nasadí nastavení e-mailu na zařízení, aby uživatelé měli přístup k podnikovému e-mailu na svých osobních zařízeních, aniž by jejich součást musela mít.|[Konfigurace přístupu k firemnímu e-mailu pomocí e-mailových profilů v Microsoft Intune](../configuration/email-settings-configure.md)|
|Profily sítě VPN|Nasadí nastavení sítě VPN pro uživatele a zařízení ve vaší organizaci. Nasazením těchto nastavení zjednodušíte uživatelům připojování k prostředkům v síti společnosti.|[Připojení VPN v Microsoft Intune](../configuration/device-profiles.md#vpn)|
|Zásady podmíněného přístupu|Spravuje přístup k e-mailu Microsoft Exchange a službám SharePoint Online ze zařízení, která nespravuje Intune.|[Omezení přístupu k e-mailu a SharePointu pomocí Microsoft Intune](../protect/app-based-conditional-access-intune.md)|

## <a name="next-steps"></a>Další kroky

[Podívejte se na seznam zařízení, která můžete spravovat](../remote-actions/device-management.md).
