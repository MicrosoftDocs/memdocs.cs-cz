---
title: Průvodce testováním Microsoft Intune App SDK pro Android
description: Průvodce testováním sady Microsoft Intune App SDK pro Android vám pomůže otestovat aplikaci pro Android spravovanou v Intune.
keywords: Sada SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/26/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 4ef8f421-9610-4d34-a464-cc02eb1578a9
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6875dc873d44b77a24fe68f637d9329c9f5e1d9c
ms.sourcegitcommit: 118587ddb31ce26b27801839db9b3b59f1177f0f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/29/2020
ms.locfileid: "84165596"
---
# <a name="microsoft-intune-app-sdk-for-android-testing-guide"></a>Průvodce testováním Microsoft Intune App SDK pro Android

Tento průvodce pomáhá vývojářům testovat aplikace pro Android spravované v Intune.  

## <a name="prerequisite-test-accounts"></a>Požadované zkušební účty
Můžete vytvořit nové účty s předem generovanými daty nebo bez nich. Vytvoření nového účtu:
1. Přejít na web [ukázek ukázek společnosti Microsoft](https://demos.microsoft.com/environments/create/tenant) . 
2. [Nastavte Intune](../fundamentals/setup-steps.md) pro povolení správy mobilních zařízení (MDM).
3. [Vytvořte uživatele](../fundamentals/users-add.md).
4. [Vytvořte skupiny](../fundamentals/groups-add.md).
5. [Přiřaďte licence](../fundamentals/licenses-assign.md) podle potřeby pro vaše testování.


## <a name="azure-portal-policy-configuration"></a>Konfigurace zásad Azure Portal
[Vytvořte a přiřaďte zásady ochrany aplikací](../apps/app-protection-policies.md) v okně [Intune Azure Portal](https://portal.azure.com/?feature.customportal=false#blade/Microsoft_Intune_Apps/MainMenu/14/selectedMenuItem/Overview). V okně Intune můžete také vytvořit a přiřadit [zásady konfigurace aplikace](../apps/app-configuration-policies-overview.md) .

> [!NOTE]
> Pokud vaše aplikace není uvedená v Azure Portal, můžete na ni cílit pomocí zásady výběrem možnosti **Další aplikace** a zadáním názvu balíčku do textového pole.

## <a name="test-cases"></a>Testovací případy

Následující testovací případy poskytují kroky konfigurace a potvrzení. Tyto pokyny vám pomůžou při řešení problémů s aplikacemi pro Android spravovanými přes Intune.

### <a name="required-pin-and-corporate-credentials"></a>Požadované PIN a firemní přihlašovací údaje

Pro přístup k firemním prostředkům můžete vyžadovat PIN kód. Můžete taky vymáhat podnikové ověřování, aby mohli uživatelé používat spravované aplikace. Zde je uveden postup:

1. Nastavte **vyžadovat pro přístup kód PIN** a pro přístup k **Ano** **vyžadovat podnikové přihlašovací údaje** . Další informace najdete v tématu [nastavení zásad ochrany aplikací pro Android v Microsoft Intune](../apps/app-protection-policy-settings-android.md#access-requirements).
2. Potvrďte následující podmínky:
    - Při spuštění aplikace by se měla zobrazit výzva k zadání PIN kódu nebo výrobnímu uživateli, který se použil při registraci s Portál společnosti.
    - Nepovedlo se vytvořit platnou výzvu k přihlášení, protože je k dispozici nesprávně nakonfigurovaný manifest Androidu, konkrétně hodnoty pro integraci knihovny Azure Active Directory Authentication Library (ADAL) (SkipBroker, ClientID a Authority).
    - Chyba při zobrazení výzvy může být způsobena nesprávně integrovanou `MAMActivity` hodnotou. Další informace o najdete `MAMActivity` v tématu [Microsoft Intune App SDK pro Android – příručka pro vývojáře](app-sdk-android.md).

> [!NOTE] 
> Pokud předchozí test nefunguje, následující testy budou pravděpodobně také neúspěšné. Projděte si integraci [sady SDK](app-sdk-android.md#sdk-integration) a [ADAL](app-sdk-android.md#configure-azure-active-directory-authentication-library-adal) .

### <a name="restrict-transferring-and-receiving-data-with-other-apps"></a>Omezení přenosu a příjem dat s jinými aplikacemi
Přenos dat mezi podnikovými spravovanými aplikacemi můžete řídit následujícím způsobem:

1. Nastavte možnost **povoluje aplikaci přenášet data do jiných aplikací** do **aplikací spravovaných podle zásad**.
2. Nastavte **možnost dovolit aplikaci, aby přijímala data z jiných aplikací** do **všech aplikací**. Tyto zásady ovlivňují použití záměrů a poskytovatelů obsahu.
3. Potvrďte následující podmínky:
    - Správné otevření z nespravované aplikace do funkce aplikace.
    - Sdílení obsahu mezi spravovanými aplikacemi je povolené.
    - Sdílení ze spravovaných aplikací do nespravovaných aplikací (například Chrome) je zablokované.

### <a name="restrict-cut-copy-and-paste"></a>Omezit vyjmutí, kopírování a vložení
Systémovou schránku můžete omezit na spravované aplikace následujícím způsobem:

1. Nastavte **Omezit vyjmutí, kopírování a vložení s jinými aplikacemi** do **zásad spravovaných pomocí vložit**.
2. Potvrďte následující podmínky:
    - Kopírování textu z aplikace do nespravované aplikace (například zprávy) je zablokované.

### <a name="prevent-save"></a>Zabránit uložení
Funkci **Uložit jako** můžete řídit následujícím způsobem:

1. Pokud vaše aplikace vyžaduje [Integrované ovládací prvky Uložit jako](app-sdk-android.md#example-determine-if-saving-to-device-or-cloud-storage-is-permitted), nastavte možnost **zakázat možnost Uložit jako** na **Ano**.
2. Potvrďte následující podmínky:
    - Uložení je omezené jenom na vhodná spravovaná umístění.

### <a name="file-encryption"></a>Šifrování souborů
Data na zařízení můžete šifrovat následujícím způsobem:

1. Nastavte **šifrovat data aplikací** na **Ano**.
2. Potvrďte následující podmínky:
    - Normální chování aplikace není ovlivněno.

### <a name="prevent-android-backups"></a>Zakázat zálohování dat v zařízeních s Androidem
Zálohování aplikací můžete řídit následujícím způsobem:

1. Pokud jste nastavili [integrovaná omezení zálohování](app-sdk-android.md#protecting-backup-data), nastavte **Zakázat zálohování Androidu** na **Ano**.
2. Potvrďte následující podmínky:
    - Zálohy jsou omezené.

### <a name="unenrollment"></a>Zrušení registrace
Spravované aplikace můžete vzdáleně vymazat z obsahujícího podnikového e-mailu a dokumentů a osobní údaje se dešifrují, když už se nespravuje. Zde je uveden postup:

1. Z Azure Portal [vydejte vymazání](../apps/apps-selective-wipe.md).
2. Pokud se vaše aplikace neregistruje pro žádné obslužné rutiny vymazání, potvrďte následující podmínky:
    - Dojde k úplnému vymazání aplikace.
3. Pokud se vaše aplikace zaregistrovala pro `WIPE_USER_DATA` nebo `WIPE_USER_AUXILARY_DATA` , potvrďte následující podmínky:
    - Spravovaný obsah se z aplikace odebere. Další informace najdete v tématu [sada Intune App SDK pro Android Developer Guide – selektivní vymazání](app-sdk-android.md#selective-wipe).

### <a name="multi-identity-support"></a>Podpora více identit
Integrace [podpory více identit](app-sdk-android.md#multi-identity-optional) je vysoce riziková změna, kterou je třeba důkladně otestovat. K nejběžnějším problémům dochází kvůli nesprávně nastavování identity (kontext vs. úroveň ohrožení) a sledovacích souborů ( `MAMFileProtectionManager` ).

Minimální, potvrďte, že:

- Zásada **Uložit jako** pro spravované identity funguje správně.
- Omezení kopírování a vkládání se správně vynutila ze spravovaných na osobní.
- Šifrují se jenom data patřící do spravované identity a osobní soubory se nemění.
- Selektivní vymazání během Odregistrace odebírá jenom spravovaná data identity.
- Uživateli se zobrazí výzva k zadání podmíněného spuštění při změně z nespravovaného na spravovaný účet (pouze při prvním).

### <a name="app-configuration-optional"></a>Konfigurace aplikace (volitelné)
Můžete nakonfigurovat chování spravovaných aplikací. Pokud vaše aplikace spotřebovává nastavení konfigurace aplikace, měli byste otestovat, jestli vaše aplikace správně zpracovává všechny hodnoty, které jste (jako správce) mohli nastavit. V Intune můžete vytvářet a přiřazovat [zásady konfigurace aplikací](../apps/app-configuration-policies-overview.md) .

## <a name="next-steps"></a>Další kroky

- [Přidání obchodní aplikace pro Android do Microsoft Intune](../apps/lob-apps-android.md)
