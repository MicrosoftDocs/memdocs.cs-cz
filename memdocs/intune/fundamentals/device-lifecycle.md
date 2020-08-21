---
title: Přehled životního cyklu Microsoft Intune MDM
description: Zjistěte, jak vám pomůže Intune spravovat zařízení prostřednictvím jejich životního cyklu od registrace přes konfiguraci až po závěrečné vyřazení.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/04/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0c8d60a4a943ba2af9ea99f9eb887a9b77a49fcf
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693501"
---
# <a name="overview-of-the-microsoft-intune-mobile-device-management-mdm-lifecycle"></a>Přehled životního cyklu správy mobilních zařízení (MDM) v Microsoft Intune

Všechna zařízení, která spravujete, mají *životní cyklus*. Intune vám může pomoci při správě tohoto životního cyklu od registrace přes konfiguraci a ochranu až po vyřazení zařízení, když už nebude potřeba. Tady je příklad: iPad zakoupený vaší společností nejdřív musí být zaregistrovaný s vaším účtem Microsoft Intune, aby ho vaše společnost mohla spravovat. pak je potřeba nakonfigurovat míru vaší společnosti; pak je nutné chránit data, která jsou na něm uložena uživatelem. a konečně, pokud už tento iPad nepotřebujete, musíte na něm [vyřadit nebo vymazat](https://docs.microsoft.com/mem/intune/remote-actions/devices-wipe) všechna citlivá data.

![Životní cyklus zařízení](./media/device-lifecycle/device-lifecycle.png "životní cyklus zařízení v Intune")

## <a name="enroll"></a>Registrace

Dnešní strategie správy mobilních zařízení (MDM) se týkají nejrůznějších telefonů, tabletů a počítačů (iOS/iPadOS, Android, Windows a Mac OS X). Pokud potřebujete mít možnost spravovat zařízení, což se často stává třeba u zařízení vlastněných společností, prvním krokem je [nastavení registrace zařízení](../enrollment/device-enrollment.md). Počítače s Windows můžete také spravovat buď tak, že je zaregistrujete v Intune (MDM), nebo do nich [nainstalujete klientský software Intune](manage-windows-pcs-with-microsoft-intune.md).

## <a name="configure"></a>Konfigurace

Registrace zařízení je jenom první krok. Pokud chcete využívat všechno, co Intune nabízí, a zajistit u zařízení zabezpečení a dodržování standardů společnosti, můžete si vybrat z široké nabídky zásad. Ty vám umožní nastavit skoro každý aspekt fungování spravovaných zařízení. Mají třeba uživatelé na zařízeních, která obsahují firemní data, používat heslo? Můžete to vyžadovat. Máte podnikovou síť Wi-Fi? Můžete ji automaticky nakonfigurovat. Tady je přehled typů dostupných možností konfigurace:

- [**Konfigurace zařízení**](../configuration/device-profiles.md). Tyto zásady umožňují nastavit způsob fungování funkcí a možností zařízení, která spravujete. Můžete například vyžadovat použití hesla na telefonech s Androidem nebo zakázat používání kamery na iPhonu.
- [**Přístup k prostředkům společnosti**](../configuration/device-profiles.md). Pokud umožníte uživatelům přistupovat k pracovním dokumentům z osobních zařízení, může to znamenat určité výzvy. Jak třeba zajistíte, aby byla všechna zařízení, která potřebují přístup k firemním e-mailům, správně nakonfigurovaná? Jak zajistíte, aby mohli uživatelé získat přístup do podnikové sítě pomocí připojení VPN, aniž by museli znát složitá nastavení? Intune vám může pomoct tyto překážky překonat díky automatické konfiguraci, která spravovaným zařízením umožní přístup k běžným prostředkům společnosti.
- [**Zásady správy počítačů s Windows (s klientským softwarem Intune)**](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md) I když vám nejvíc možností správy zařízení přinese registrace počítačů s Windows do Intune, Intune dál podporuje správu počítačů s Windows pomocí klientského softwaru Intune. Pokud potřebujete informace o některých úlohách, které můžete s počítači provádět, začněte tady.

## <a name="protect"></a>Ochrana

V moderním světě informačních technologií představuje ochrana zařízení proti neoprávněnému přístupu jeden z vašich nejdůležitějších úkolů. Kromě položek v kroku **Konfigurace** životního cyklu zařízení Intune poskytuje tyto možnosti, které pomáhají chránit spravovaná zařízení proti neoprávněnému přístupu nebo nebezpečným útokům:

- [**Multi-Factor Authentication**](../enrollment/multi-factor-authentication.md). Přidáním další úrovně ověřování k přihlašování uživatelů můžete přispět k ještě lepšímu zabezpečení zařízení. Mnoho zařízení podporuje vícefaktorové ověřování, které před povolením přístupu uživatelů vyžaduje druhou úroveň ověření, například prostřednictvím telefonního hovoru nebo textové zprávy.
- [**Nastavení Windows Hello pro firmy**](../protect/windows-hello.md) Nastavení Windows Hello pro firmy je alternativní metoda přihlašování, která umožňuje uživatelům používat k přihlášení *gesto*, třeba otisk prstu nebo Windows Hello, takže nemusí zadávat heslo.
- [**Zásady ochrany počítačů se systémem Windows (s klientským softwarem Intune)**](policies-to-protect-windows-pcs-in-microsoft-intune.md). Pokud spravujete počítače s Windows pomocí klientského softwaru Intune, jsou dostupné zásady, které vám umožňují řídit na spravovaných počítačích s Windows nastavení služby Endpoint Protection, aktualizací softwaru a brány Windows Firewall.

## <a name="retire"></a>Vyřazení

Když dojde ke ztrátě nebo odcizení zařízení, když je potřeba zařízení vyměnit nebo když se uživatelé přesunou na jinou pracovní pozici, je většinou vhodné zařízení [vyřadit nebo vymazat](../remote-actions/device-management.md). To můžete udělat několika způsoby, třeba zařízení resetovat, odebrat ho ze zprávy nebo z něj vymazat firemní data.

## <a name="next-steps"></a>Další kroky

- Další informace o [správě zařízení v Microsoft Intune](../remote-actions/device-management.md)
