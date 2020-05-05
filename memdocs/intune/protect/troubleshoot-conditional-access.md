---
title: Řešení potíží s podmíněným přístupem
titleSuffix: Microsoft Intune
description: Co dělat, když uživatelé nebudou mít přístup k prostředkům prostřednictvím podmíněného přístupu Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 5fa59501-5f33-46b7-a5f5-75eeae9f1209
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5d56d3982a036ace198ceae9bf2d01a8c12de6d5
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079140"
---
# <a name="troubleshoot-conditional-access"></a>Řešení potíží s podmíněným přístupem
Tento článek popisuje, co dělat, když se vašim uživatelům nedaří získat přístup k prostředkům chráněným pomocí podmíněného přístupu, nebo když uživatelé mají přístup k chráněným prostředkům, ale měli byste je zablokovat.

Pomocí Intune a podmíněného přístupu můžete chránit přístup ke službám, jako jsou:
- Služby Office 365, jako je Exchange Online, SharePoint Online a Online Skype pro firmy
- Místní Exchange
- Různé další služby

Tato funkce vám umožní zajistit, aby k vašim firemním prostředkům měli přístup jenom zařízení zaregistrovaná v Intune a kompatibilní s pravidly podmíněného přístupu, která jste nastavili v konzole pro správu Intune nebo v Azure Active Directory. 

## <a name="requirements-for-conditional-access"></a>Požadavky na podmíněný přístup

Aby podmíněný přístup fungoval, musí být splněné následující požadavky:

- Zařízení musí být zaregistrované v MDM a spravované přes Intune.

- Uživatel i zařízení musí vyhovovat přiřazeným zásadám dodržování předpisů Intune.

- Uživateli se standardně musí přiřadit zásady dodržování předpisů pro zařízení. To může záviset na konfiguraci nastavení **označení zařízení bez přiřazených zásad dodržování předpisů,** která jsou v**nastavení zásad dodržování** předpisů **zařízením** > v portálu pro správu Intune.

- Pokud uživatel nepoužívá Outlook, ale nativního poštovního klienta daného zařízení, musí být v zařízení aktivovaný protokol Exchange ActiveSync. K tomu dochází automaticky pro zařízení se systémy iOS/iPadOS, Windows Phone a Android Knox.

- Pro místní Exchange musí být váš Intune Exchange Connector správně nakonfigurovaný. Další informace najdete v tématu [Poradce při potížích s Exchange Connectorem v Microsoft Intune](troubleshoot-exchange-connector.md).

- Pro místní Skype musíte nakonfigurovat hybridní moderní ověřování. Podívejte se na [Přehled hybridního moderního ověřování](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview).

Tyto podmínky si můžete prohlédnout u každého zařízení na webu Azure Portal a v inventární sestavě zařízení.

## <a name="devices-appear-compliant-but-users-are-still-blocked"></a>Zařízení se zobrazují jako kompatibilní, ale uživatelé jsou přesto blokovaní

- Ujistěte se, že má uživatel přiřazenou licenci Intune pro správné vyhodnocení dodržování předpisů.

- Zařízení s Androidem, která nejsou v systému KNOX, nebudou udělena přístup, dokud uživatel neklikne na odkaz Začínáme **nyní** v e-mailu o karanténě, který obdrží. To platí i v případě, že uživatel je už zaregistrovaný v Intune. Pokud uživatel neobdrží e-mail s odkazem na telefonu, může k přístupu k e-mailu a jeho přeposlání na e-mailový účet na svém zařízení použít počítač.

- Když se zařízení registruje poprvé, může registrace jeho informací o dodržování předpisů trvat nějakou dobu. Počkejte několik minut a zkuste akci zopakovat.

- V případě zařízení se systémem iOS/iPadOS může stávající e-mailový profil blokovat nasazení e-mailového profilu vytvořeného správcem Intune přiřazeného tomuto uživateli, takže zařízení nedodržuje předpisy. V tomto scénáři aplikace Portál společnosti upozorní uživatele, že nedodržují předpisy z důvodu ručního nakonfigurovaného e-mailového profilu, a vyzve uživatele k odebrání tohoto profilu. Jakmile uživatel odebere stávající e-mailový profil, může se e-mailový profil Intune úspěšně nasadit. Pokud chcete tomuto problému zabránit, upozorněte uživatele, aby na svém zařízení před registrací odebrali všechny stávající e-mailové profily.

- Zařízení se může zablokovat ve stavu dodržování předpisů, takže uživatel nebude muset spustit jiné vrácení se změnami. Pokud máte zařízení v tomto stavu:
  - Ujistěte se, že zařízení používá nejnovější verzi aplikace Portál společnosti.
  - Restartujte zařízení.
  - Podívejte se, jestli problém přetrvává v různých sítích (například mobilní, Wi-Fi atd.).

  Pokud problém trvá, kontaktujte podporu Microsoftu podle pokynů v tématu o [získání podpory pro Microsoft Intune](../fundamentals/get-support.md).

- Některá zařízení s Androidem se můžou zdát šifrovat, ale Portál společnosti aplikace tato zařízení rozpoznává jako nevyhovující. V tomto scénáři se uživateli zobrazí oznámení aplikace Portál společnosti s výzvou k nastavení hesla pro spuštění zařízení. Po klepnutí na oznámení a potvrzení stávajícího PIN kódu nebo hesla zvolte na obrazovce **Zabezpečené spuštění** možnost **Ke spuštění zařízení vyžadovat PIN kód** a pak v aplikaci Portál společnosti klepněte na tlačítko **Zkontrolovat dodržování předpisů** pro toto zařízení. Zařízení by se teď mělo rozpoznat jako zašifrované. 

  > [!NOTE]
  > Někteří výrobci zařízení šifrují svoje zařízení bu pomocí výchozího PIN kódu místo PIN kódu nastaveného uživatelem. V Intune se šifrují šifrování, které používá výchozí PIN kód jako nezabezpečené, a tato zařízení označí jako nedodržující předpisy, dokud uživatel nevytvoří nový, jiný než výchozí PIN kód.

- Zařízení s Androidem, které je zaregistrované a kompatibilní, může být i nadále blokované a při prvním pokusu o přístup k podnikovým prostředkům dostávat karanténní oznámení. Pokud k tomu dojde, zajistěte, aby aplikace Portál společnosti neběžela, a potom vyberte odkaz **Začínáme nyní** v e-mailu o karanténě pro aktivaci vyhodnocení. Toto by mělo být potřeba udělat jenom při prvním povolení podmíněného přístupu.

- Zařízení s Androidem, které je zaregistrováno, může uživateli zobrazit výzvu bez nalezených certifikátů a nebude jim udělen přístup k prostředkům O365. Uživatel musí na zaregistrovaném zařízení povolit možnost *Povolit přístup z prohlížeče* následujícím způsobem:
  1. Otevřete aplikaci Portál společnosti.
  2. Přejděte na stránku Nastavení prostřednictvím tlačítka se třemi tečkami (...) nebo hardwarového tlačítka nabídky.
  3. Vyberte tlačítko *Povolit přístup z prohlížeče* .
  4. V prohlížeči Chrome se odhlásí z Office 365 a restartuje Chrome.  


## <a name="devices-are-blocked-and-no-quarantine-email-is-received"></a>Zařízení jsou blokovaná, ale žádný e-mail o karanténě nepřišel

- Ověřte, jestli se dané zařízení nachází v konzole pro správu Intune jako zařízení Exchange ActiveSync. Pokud není, je pravděpodobné, že se zjišťování zařízení nedaří, pravděpodobně kvůli problému s Exchange Connectorem. Další informace najdete v tématu [řešení potíží s místním Exchange Connectorem v Intune](troubleshoot-exchange-connector.md).

- Než Exchange Connector začne blokovat zařízení, odešle aktivační e-mail (e-mail o karanténě). Pokud je zařízení offline, nemusí aktivační e-mail obdržet. 

- Zkontrolujte, jestli je e-mailový klient na zařízení nakonfigurovaný tak, aby načítal e-maily pomocí metody **Push**, a ne **Poll**. Pokud ano, může to být příčina toho, že uživatel nedostal příslušný e-mail. Přepněte na **dotaz** a podívejte se, jestli zařízení neobdrží e-mail.

## <a name="devices-are-noncompliant-but-users-are-not-blocked"></a>Zařízení nedodržují předpisy, ale uživatelé nejsou blokovaní

- U počítačů s Windows podmíněný přístup blokuje jenom nativní e-mailovou aplikaci, Office 2013 s moderním ověřováním nebo Office 2016. Blokování starších verzí aplikace Outlook nebo všech e-mailových aplikací na počítačích s Windows vyžaduje konfigurace zařízení AAD a Active Directory Federation Services (AD FS) (AD FS) podle [nastavení služby SharePoint Online a Exchange Online pro Azure Active Directory podmíněný přístup](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-no-modern-authentication).

- Pokud se zařízení z Intune selektivně vymaže nebo vyřadí, může mu několik hodin po vyřazení nadále zůstat možnost přístupu. Důvodem je to, že Exchange ukládá přístupová práva do mezipaměti po dobu šesti hodin. Zvažte možnost použití jiných způsobů ochrany dat na vyřazených zařízení v tomto scénáři.

- Pokud je uživateli, kterému je přiřazená licence pro Intune, přihlášený uživatel, který má licenci pro Intune, Surface Hub hromadně zaregistrovaná a DEM zaregistrovaná zařízení s Windows můžou podporovat podmíněný přístup. Pro správné vyhodnocení ale musíte nasadit zásady dodržování předpisů do skupin zařízení (ne do skupin uživatelů).

- Zkontrolujte přiřazení zásad dodržování předpisů a zásad podmíněného přístupu. Pokud uživatel není ve skupině, která je přiřazena k zásadám, nebo je ve skupině, která je vyloučena, uživatel není blokovaný. Dodržování předpisů se kontroluje jenom u zařízení uživatelů, kteří jsou v přiřazené skupině.

## <a name="noncompliant-device-is-not-blocked"></a>Zařízení nevyhovující předpisům není blokované

Pokud zařízení nedodržuje předpisy, ale má i nadále přístup, proveďte následující akce.

- Zkontrolujte cílovou skupinu a skupinu pro vyloučení. Pokud uživatel není ve správné cílové skupině nebo je ve skupině vyloučení, nebude zablokovaný. Vyhovování předpisům se kontroluje jenom u zařízení uživatelů, kteří jsou v cílové skupině.

- Zkontrolujte, že se zařízení zjišťuje. Směřuje Exchange Connector na CAS pro Exchange 2010, zatímco je uživatel na serveru Exchange 2013? V takovém případě pokud je výchozí pravidlo Exchange nastavené na povolení, i když je uživatel v cílové skupině, Intune nemůže vědět o připojení zařízení k Exchangi.

- Kontrola stavu existence a přístupu k zařízení v Exchangi:
  - Pomocí této rutiny PowerShellu získáte seznam všech mobilních zařízení pro poštovní schránku: Get-ActiveSyncDeviceStatistics-Mailbox MBX. Pokud zařízení není v seznamu uvedeno, nepřistupuje k Exchangi.
  
  - Pokud je zařízení uvedené, použijte příkaz Get-CASmailbox-identity: UPN | FL rutina pro získání podrobných informací o jeho stavu přístupu a poskytování těchto informací podpora Microsoftu.

## <a name="next-steps"></a>Další kroky
Pokud vám tyto informace nepomohly, můžete také [získat podporu pro Microsoft Intune](../fundamentals/get-support.md).
