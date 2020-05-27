---
title: Ochrana zařízení pomocí Microsoft Intune
titleSuffix: Microsoft Intune
description: Přečtěte si o některých způsobech, kterými vám Intune může pomoct chránit vaše zařízení před neoprávněným přístupem a dalšími hrozbami.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/19/2018
ms.topic: overview
ms.subservice: protect
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 95a1833dc518ad4cbc663ac006bb7c72ef2e627e
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989698"
---
# <a name="protect-devices-with-microsoft-intune"></a>Ochrana zařízení pomocí Microsoft Intune

Microsoft Intune pomáhá chránit vámi spravovaná zařízení i data, která jsou na nich uložená.

## <a name="device-configuration"></a>Konfigurace zařízení
[Zásady konfigurace](../configuration/device-profiles.md) Intune vám pomůžou chránit a konfigurovat zařízení tím, že se řídí velké množství nastavení a funkcí. Příklad:

- Na zařízení můžete omezit používání hardwarových funkcí, jako je fotoaparát nebo Bluetooth.
- Můžete nakonfigurovat, které aplikace splňují či nesplňují vaše požadavky. Když se nainstaluje aplikace nesplňující požadavky, dostanete upozornění (a některé platformy instalaci přímo zablokují).

## <a name="reset-passcodes-when-users-are-locked-out-of-their-devices"></a>Resetování přístupových kódů v případě, že se uživatelé nemůžou přihlásit k zařízení
Vzhledem k tomu, že prvním krokem při ochraně dat společnosti na mobilních zařízeních je vyžadování hesla pro použití zařízení, je někdy nutné [Resetovat heslo](../remote-actions/device-passcode-reset.md) nebo s tím zaměstnanci pomoci odebráním hesla nebo nastavením dočasného hesla vzdáleně. Pokud dojde ke ztrátě nebo odcizení zařízení, můžete ho také [vzdáleně uzamknout](../remote-actions/device-remote-lock.md).

## <a name="retire-devices-and-remove-data"></a>Vyřazení zařízení a odebrání dat
Pokud je potřeba [odebrat zařízení ze správy Intune](../remote-actions/devices-wipe.md) (třeba když uživatel odejde z organizace nebo dojde ke ztrátě či odcizení zařízení), pravděpodobně budete chtít ze zařízení odebrat data. S Intune můžete firemní data uchovat v bezpečí hned několika způsoby.

## <a name="require-devices-to-be-compliant"></a>Nastavení požadavků pro zařízení
Intune obsahuje [zásady dodržování předpisů](device-compliance-get-started.md), s jejichž pomocí můžete vyhodnotit, jaká zařízení nesplňují vámi stanovené požadavky (v některých případech můžete stav i napravit). Můžete si třeba nechat hlásit:
- zařízení s jailbreakem iOS/iPadOS
- Šifrovaná nebo nešifrovaná zařízení
- Stav zařízení s Windows 10 (podle Služby pro ověření stavu)

## <a name="protect-apps-and-the-data-they-use"></a>Ochrana aplikací a jimi využívaných dat
Intune poskytuje celou řadu funkcí, které usnadňují ochranu aplikací a jejich dat. Zásady správy mobilních aplikací například můžou:
- Zabránit zálohování dat z chráněné aplikace
- Zakázat kopírování a vkládání do ostatních aplikací
- Požadovat PIN pro přístup k aplikaci – další informace najdete v tématu [Ochrana dat a aplikací pomocí Microsoft Intune](../apps/app-protection-policy.md)

## <a name="add-an-additional-layer-of-protection-to-devices"></a>Přidání další vrstvy ochrany do zařízení
[Multi-Factor Authentication (MFA)](../enrollment/multi-factor-authentication.md) představuje bezpečnější způsob ověřování uživatelů zařízení v síti.  Pokud se používá služba MFA, uživatelé musí potvrdit svou identitu i jinak než jen pomocí svého uživatelského jména a hesla – prostřednictvím telefonního hovoru nebo SMS zprávy.

## <a name="control-windows-hello-for-business-settings-on-windows-devices"></a>Nastavení Windows Hello pro firmy na zařízeních s Windows
Intune umožňuje integraci se službou [Windows Hello pro firmy](windows-hello.md). Tato alternativní metoda pro přihlašování do systému Windows 10 a novějších pomocí účtu služby Active Directory nebo Azure Active Directory nahrazuje heslo, čipovou kartu nebo virtuální čipovou kartu.

## <a name="disable-activation-lock-on-ios-devices"></a>Zakázat Zámek aktivace na zařízeních s iOS
Zámek aktivace je funkce, která pomáhá chránit zařízení uživatelů. Tato funkce vyžaduje, aby uživatelé před vymazáním nebo opětovnou aktivací zařízení zadali své Apple ID a heslo. Tato funkce ale může vést k problémům, pokud třeba uživatel odejde ze společnosti, aniž by ze zařízení zámek odebral. [Zakázat iOS/iPadOS zámek aktivace](../remote-actions/device-activation-lock-disable.md) může pomáhat odebráním zámku ze zařízení se systémem iOS/iPadOS, která vám umožní znovu přidělit nebo vymazat.

## <a name="next-steps"></a>Další kroky

Přečtěte si další informace o [ochraně před mobilním hrozbami](mobile-threat-defense.md).
