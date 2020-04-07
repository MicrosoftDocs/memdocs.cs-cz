---
title: Zobrazení podrobností o zařízeních v Microsoft Intune – Azure | Microsoft Docs
description: Zobrazte si podrobnosti o zařízení, včetně operačních systémů, místa v úložišti, výrobce a modelu. Microsoft Intune v Azure vám umožňuje získat seznam nainstalovaných aplikací, zkontrolovat zásady dodržování předpisů a nastavit TeamViewer. Jedná se o podobný princip jako při zobrazení inventáře zařízení, která spravujete.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: e71c6bdb-d75c-404f-8e38-24a663be81c2
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed5ff548d28a5bc973c43c84861b9b256b41a203
ms.sourcegitcommit: e17fc618d4c56c38a65c489b73ba27baa133ee7b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/06/2020
ms.locfileid: "80696291"
---
# <a name="see-device-details-in-intune"></a>Zobrazení podrobností o zařízení v Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Funkce **Zařízení** poskytuje další podrobnosti o zařízení, která spravujete, včetně jejich hardwaru a nainstalovaných aplikací.

V tomto článku se dozvíte, jak si můžete zobrazit všechna zařízení a jejich vlastnosti na portálu Azure Portal.

## <a name="view-the-device-details"></a>Zobrazení podrobností o zařízení

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Vyberte **Zařízení** > **Všechna zařízení** > výběrem zařízení uvedeného v seznamu otevřete podrobné informace o něm:

   - **Přehled** zobrazuje název zařízení a uvádí některé klíčové vlastnosti zařízení, například to, jestli jde o osobní nebo firemní zařízení, sériové číslo, primární uživatel a další. Na zařízení můžete provést následující akce:
      - [Vyřadit](devices-wipe.md#retire)
      - [Vymazání](devices-wipe.md#wipe)
      - [Odstranit](devices-wipe.md#delete-devices-from-the-intune-portal)
      - [Vzdálené uzamčení](device-remote-lock.md)
      - [Synchronizovat](device-sync.md)
      - [Resetovat heslo](device-passcode-reset.md)
      - [Restartovat](device-restart.md) (jenom Windows)
      - [Začít znovu](device-fresh-start.md) (jenom Windows)
      - [Resetování autopilotu](/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset) (jenom Windows)
      - [Rychlá kontrola](../configuration/device-restrictions-windows-10.md) (jenom Windows 10)
      - [Úplná kontrola](../configuration/device-restrictions-windows-10.md) (jenom Windows 10)
      - Aktualizace funkce Security Intelligence v programu Windows Defender
      - [Střídání klíčů BitLockeru](https://docs.microsoft.com/mem/intune/protect/encrypt-devices#to-rotate-the-bitlocker-recovery-key)
      - [Přejmenování zařízení](device-rename.md)
      - [Nová relace vzdálené pomoci](https://docs.microsoft.com/mem/intune/remote-actions/teamviewer-support)
   - Pomocí **vlastností** můžete zařízení přiřadit [kategorii, kterou vytvoříte](../enrollment/device-group-mapping.md), a upravit jeho vlastnictví na osobní nebo podnikové.
   - **Hardware** obsahuje mnoho podrobností o zařízení, jako je ID zařízení, operační systém a verze, prostor úložiště a další podrobnosti.
   - V části **Zjištěné aplikace** se zobrazuje seznam všech nainstalovaných aplikací, které služba Intune v zařízení našla, včetně jejich verzí. Další informace najdete v tématu [zjištěné aplikace Intune](../apps/app-discovered-apps.md).
   - V části **Dodržování předpisů zařízení** najdete všechny přiřazené zásady dodržování předpisů a informaci, jestli je zařízení splňuje.
   - Část **Konfigurace zařízení** obsahuje všechny zásady konfigurace přiřazené zařízení a informaci, jestli byly zásady úspěšné.
   - **Konfigurace aplikace** 
   - **Konfigurace zabezpečení koncového bodu**
   - **Klíče pro obnovení** zobrazují dostupné klíče BitLockeru pro zařízení.
   - **Spravované aplikace** zobrazí seznam všech spravovaných aplikací, které Intune nakonfigurovali a nasadily do zařízení. 

## <a name="hardware-device-details"></a>Podrobnosti o hardwarovém zařízení
V závislosti na tom, jaký dopravce zařízení používá, se nemusí shromažďovat všechny podrobnosti.

> [!Note]  
> Inventář hardwaru a softwaru se ve službě Intune aktualizuje každých 7 dní.

|Údaj|Popis|Platforma| 
|--------------|----------------------|----|  
|Název|Název zařízení|Windows, iOS|
|Název správy|Název zařízení používaný jenom v konzole. Změnou tohoto názvu nedojde ke změně názvu v zařízení.|Windows, iOS|
|UDID|Jedinečný identifikátor zařízení|Windows, iOS|
|ID zařízení Intune|Globálně jedinečný identifikátor, který jednoznačně identifikuje zařízení|Windows, iOS|
|Sériové číslo|Sériové číslo zařízení od výrobce|Windows, iOS|
|Sdílené zařízení|Pokud **Ano**, je zařízení sdílené více než jedním uživatelem|Windows, iOS|
|Registrace schválená uživatelem|Pokud **Ano**, zařízení má k registraci schváleného uživatelem, které umožňuje správcům spravovat určitá nastavení zabezpečení na zařízení.|Windows, iOS|
|Operační systém|Operační systém používaný v zařízení|Windows, iOS|
|Verze operačního systému|Verze operačního systému v zařízení.|Windows, iOS|
|Jazyk operačního systému|Jazyk nastavený pro operační systému v zařízení|Windows, iOS|
|Číslo buildu|Číslo sestavení operačního systému.|Android|
|Úroveň opravy zabezpečení|Úroveň opravy zabezpečení pro zařízení.|Android|
|Celkové místo v úložišti|Celkové místo úložiště v zařízení (v gigabajtech)|Windows, iOS|
|Volné místo úložiště|Nevyužité místo úložiště v zařízení (v gigabajtech)|Windows, iOS|
|IMEI|Mezinárodní identita mobilního zařízení|Windows, iOS/iPadOS, Android|
|MEID|Identifikátor mobilního zařízení|Windows, iOS/iPadOS, Android|
|Výrobce|Výrobce zařízení|Windows, iOS/iPadOS, Android|
|Model|Model zařízení|Windows, iOS/iPadOS, Android|
|Telefonní číslo|Telefonní číslo přidružené k zařízení|Windows, iOS/iPadOS, Android *|
|Poskytovatel služeb pro odběratele|Bezdrátový operátor zařízení|Windows, iOS/iPadOS, Android|
|Mobilní technologie|Rádiový systém používaný zařízením|Windows, iOS/iPadOS, Android|
|Wi-Fi MAC|Adresa MAC zařízení|Windows, iOS/iPadOS, Android|
|ICCID|Identifikátor karty s integrovaným obvodem, což je jedinečné identifikační číslo SIM karty|Windows, iOS/iPadOS, Android|
|Datum zápisu|Datum a čas, kdy se zařízení zaregistrovalo v Intune|Windows, iOS/iPadOS, Android|
|Poslední kontakt|Datum a čas posledního připojení zařízení k Intune|Windows, iOS/iPadOS, Android|
|Kód pro obejití zámku aktivace|Kód, který lze použít k zakázání zámku aktivace.|iOS|
|Registrované v Azure AD|Pokud **Ano**, zařízení je registrované v Azure Active Directory|Windows, iOS/iPadOS, Android|
|Intune je zaregistrované.|Pokud **Ano**, zařízení je zaregistrované v Intune.|Windows, iOS/iPadOS, Android|
|Dodržování předpisů|Stav dodržování předpisů zařízení|Windows, iOS/iPadOS, Android|
|EAS aktivované|Pokud **Ano**, pak je zařízení synchronizované s poštovní schránkou Exchange|Windows, iOS/iPadOS, Android|
|ID aktivace EAS|Identifikátor protokolu Exchange ActiveSync zařízení|Windows, iOS/iPadOS, Android|
|Pod dohledem|Pokud **Ano**, mají správci nad zařízením lepší kontrolu|Windows, iOS/iPadOS, Android|
|Šifrované|Pokud **Ano**, jsou data uložená v zařízení šifrovaná|Windows, iOS/iPadOS, Android|

> [!Note]  
> Telefonní číslo není v inventáři na vyhrazených nebo plně spravovaných zařízeních s Androidem Enterprise.

## <a name="next-steps"></a>Další kroky
Podívejte se, jaké další akce [správy zařízení](device-management.md) můžete provádět pomocí Intune.
