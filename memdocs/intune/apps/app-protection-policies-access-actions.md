---
title: Vymazání dat pomocí akcí podmíněného spuštění zásad ochrany aplikací
titleSuffix: Microsoft Intune
description: Naučte se selektivně vymazat data pomocí zásad ochrany aplikací s podmíněnými spouštěcími akcemi v Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f5ca557e-a8e1-4720-b06e-837c4f0bc3ca
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b4e3f058e1edef4833959868201c120de93ff85c
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79326299"
---
# <a name="selectively-wipe-data-using-app-protection-policy-conditional-launch-actions-in-intune"></a>Selektivní vymazání dat pomocí zásad ochrany aplikací s podmíněnými spouštěcími akcemi v Intune

Pomocí zásad ochrany aplikací můžete v Intune nakonfigurovat nastavení, která koncovým uživatelům zablokují přístup k podnikové aplikaci nebo účtu. Tato nastavení se zaměřují na přemístění dat a požadavky na přístup, které vaše organizace stanovila například pro zařízení s jailbreakem a minimální verze operačního systému.
 
S využitím těchto nastavení můžete explicitně vymazat podniková data ze zařízení koncového uživatele jako akci, která se má provést při nedodržení předpisů. U některých nastavení budete moci nakonfigurovat více akcí (například zablokování přístupu a vymazání dat) na základě různých zadaných hodnot.

## <a name="create-an-app-protection-policy-using-conditional-launch-actions"></a>Vytvoření zásady ochrany aplikací pomocí podmíněných spouštěcích akcí

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **aplikace** > **Zásady ochrany aplikací**.
3. Klikněte na **vytvořit zásadu** a vyberte platformu zařízení pro vaše zásady. 
4. Kliknutím na **Konfigurovat požadovaná nastavení** zobrazíte seznam dostupných nastavení, která se mají pro tuto zásadu konfigurovat. 
5. Posunutím dolů v podokně nastavení se zobrazí část s názvem **podmíněné spuštění** s upravitelnou tabulkou.

    ![Snímek obrazovky akcí přístupu ochrany aplikací v Intune](./media/app-protection-policies-access-actions/apps-selective-wipe-access-actions01.png)

6. Vyberte **Nastavení** a do sloupce **Hodnota** zadejte hodnotu, kterou uživatelé musí splnit, aby se přihlásili k firemní aplikaci. 
7. Ve sloupci **Akce** vyberte akci, která se má provést, pokud uživatelé nesplňují požadavky. V některých případech lze pro jedno nastavení nakonfigurovat více akcí. Další informace najdete v tématu [Vytvoření a přiřazení zásad ochrany aplikací](app-protection-policies.md).

## <a name="policy-settings"></a>Nastavení zásad 

Tabulka s nastavením zásad ochrany aplikací obsahuje sloupce **Nastavení**, **Hodnota** a **Akce**.

### <a name="ios-policy-settings"></a>Nastavení zásad pro iOS
Pro iOS/iPadOS budete moct nakonfigurovat akce pro následující nastavení pomocí rozevíracího seznamu **Nastavení** :
- Maximální počet pokusů o zadání PIN kódu
- Offline období odkladu
- Zařízení s jailbreakem nebo rootem
- Minimální verze operačního systému
- Minimální verze aplikace
- Minimální verze sady SDK
- Modely zařízení
- Maximální povolená úroveň hrozby pro zařízení

Pokud chcete použít nastavení **modelů zařízení** , zadejte středníkem oddělený seznam identifikátorů modelů iOS/iPadOS. U těchto hodnot se nerozlišují velká a malá písmena. Kromě v Intune vytváření sestav pro vstup modelů zařízení můžete najít identifikátor modelu iOS/iPadOS ve sloupci Typ zařízení v [dokumentaci podpory HockeyApp](https://support.hockeyapp.net/kb/client-integration-ios-mac-os-x-tvos/ios-device-types) nebo v tomto [úložišti GitHub třetí strany](https://gist.github.com/adamawolf/3048717).<br>
Příklad zadání: *iPhone5,2;iPhone5,3*

Na zařízeních koncových uživatelů by klient Intune provedl akci založenou na jednoduché shodě řetězců modelu zařízení zadaných v okně Intune pro zásady ochrany aplikací. Párování zcela závisí na tom, co zařízení ohlásí. Jako správci IT vám doporučujeme toto nastavení otestovat na zařízeních od různých výrobcích a na různých modelech zařízení u malé skupiny uživatelů, abyste si ověřili, že se nastavení chová, jak má. Výchozí hodnotou je **Nenakonfigurováno**.<br>
Nastavte jednu z následujících akcí: 
- Povolit zadané (blokovat nezadané)
- Povolit zadané (vymazat nezadané)

**Co se stane, když správce IT zapíše jiný seznam identifikátorů modelů pro iOS/iPadOS mezi zásadami, které jsou určené pro stejné aplikace pro stejného uživatele Intune?**<br>
Pokud mezi dvěma zásadami ochrany aplikací dojde ke konfliktu nakonfigurovaných hodnot, Intune obvykle zvolí nejvíce omezující přístup. Proto bude výsledná zásada odesílaná do cílové aplikace otevřené cílovým uživatelem Intune průsečík identifikátorů modelů iOS/iPadOS v *zásadách a* a *zásadě B* , které cílí na kombinaci stejné aplikace/uživatele. *Zásada A* například určuje iPhone5,2;iPhone5,3 a *Zásada B* určuje iPhone5,3. Výsledná zásada, která se uplatní u příslušného uživatele, na kterého cílí současně *Zásada A* i *Zásada B*, bude iPhone5,3. 

### <a name="android-policy-settings"></a>Nastavení zásad pro Android

Pro Android budete moci pomocí rozevíracího seznamu **Nastavení** nakonfigurovat akce pro následující nastavení:
- Maximální počet pokusů o zadání PIN kódu
- Offline období odkladu
- Zařízení s jailbreakem nebo rootem
- Minimální verze operačního systému
- Minimální verze aplikace
- Minimální verze opravy
- Výrobci zařízení
- Ověření zařízení SafetyNet
- Vyžadovat kontrolu hrozeb u aplikací
- Minimální verze Portál společnosti
- Maximální povolená úroveň hrozby pro zařízení

Pomocí **Minimální verze portál společnosti**můžete zadat konkrétní minimální verzi portál společnosti, která se vynutila na zařízení koncového uživatele. Toto nastavení podmíněného spuštění umožňuje nastavit hodnoty pro **blokování přístupu**, **vymazání dat**a **Upozornění** jako na možné akce, když se jednotlivá hodnota nesplní. Možné formáty této hodnoty se řídí vzorem *[hlavní]. [ Vedlejší]* , *[hlavní]. [ Vedlejší]. [Build]* nebo *[hlavní]. [ Vedlejší]. [Build]. [Revize]* . Vzhledem k tomu, že někteří koncoví uživatelé nemusí preferovat vynucenou aktualizaci aplikací na místě, může být při konfiguraci tohoto nastavení ideální možnost upozornění. Obchod Google Play je dobrým úkolem, který odesílá jenom rozdílové bajty pro aktualizace aplikací, ale může to být i velké množství dat, které uživatel nemusí použít, pokud se v době aktualizace data používají. Vynucení aktualizace a stažení aktualizované aplikace může vést k neočekávaným poplatkům za data v době aktualizace. Nastavení **Minimální verze portál společnosti** , pokud je nakonfigurováno, bude mít vliv na každého koncového uživatele, který získá 5.0.4560.0 verze portál společnosti a jakékoli budoucí verze portál společnosti. Toto nastavení nebude mít žádný vliv na uživatele, kteří používají verzi Portál společnosti, která je starší než verze, ve které byla tato funkce vydána. Koncoví uživatelé, kteří používají automatické aktualizace aplikace na jejich zařízení, nejspíš neuvidí žádná dialogová okna této funkce, protože budou pravděpodobně na nejnovější verzi Portál společnosti. Toto nastavení platí jenom pro Android s ochranou aplikací pro zapsaná a neregistrovaná zařízení.

Pokud chcete použít nastavení **Výrobci zařízení**, zadejte seznam výrobců zařízení s Androidem oddělených středníkem. U těchto hodnot se nerozlišují velká a malá písmena. Kromě vytváření sestav služby Intune můžete v nastavení zařízení najít výrobce Androidu zařízení. <br>
Příklad zadání: *Výrobce A;Výrobce B* 

>[!NOTE]
> Toto je několik obvyklých výrobců hlášených ze zařízení používajících Intune, které lze použít pro zadání: Asus; Blackberry; Bq; Gionee; Google; Hmd global; Htc; Huawei; Infinix; Kyocera; Lemobile; Lenovo; Lge; Motorola; Oneplus; Oppo; Samsung; Sharp; Sony; Tecno; Vivo; Vodafone; Xiaomi; Zte; Zuk.

Na zařízeních koncových uživatelů by klient Intune provedl akci založenou na jednoduché shodě řetězců modelu zařízení zadaných v okně Intune pro zásady ochrany aplikací. Párování zcela závisí na tom, co zařízení ohlásí. Jako správci IT vám doporučujeme toto nastavení otestovat na zařízeních od různých výrobcích a na různých modelech zařízení u malé skupiny uživatelů, abyste si ověřili, že se nastavení chová, jak má. Výchozí hodnotou je **Nenakonfigurováno**.<br>
Nastavte jednu z následujících akcí: 
- Povolit zadané (blokovat nezadané)
- Povolit zadané (vymazat nezadané)

**Co se stane, když správce zadá seznam výrobců zařízení s Androidem, který se v různých zásadách pro stejné aplikace pro stejného uživatele Intune liší?**<br>
Pokud mezi dvěma zásadami ochrany aplikací dojde ke konfliktu nakonfigurovaných hodnot, Intune obvykle zvolí nejvíce omezující přístup. Výsledná zásada odeslaná do cílové aplikace, kterou otevírá cílový uživatel Intune, by tedy byla průsečíkem výrobců zařízení s Androidem uvedených v seznamu v *Zásadě A* a *Zásadě B*, které cílí na stejnou kombinaci aplikace a uživatele. *Zásada A* například určuje Google;Samsung a *Zásada B* určuje Google. Výsledná zásada, která se uplatní u příslušného uživatele Intune, na kterého cílí současně *Zásada A* i *Zásada B*, bude Google. 

### <a name="additional-settings-and-actions"></a>Další nastavení a akce 

Pokud má nastavení **Vyžadovat pro přístup PIN kód** hodnotu **Ano**, bude mít tabulka standardně vyplněné řádky **Offline období odkladu** a **Maximální počet pokusů o zadání PIN kódu**.
 
Pokud chcete konfigurovat některé nastavení, vyberte ho v rozevíracím seznamu ve sloupci **Nastavení**. Po výběru nastavení se na stejném řádku zpřístupní upravitelné textové pole ve sloupci **Hodnota**, pokud je potřeba nastavit hodnotu. Zároveň se zpřístupní rozevírací seznam ve sloupci **Akce** se sadou podmíněně spuštěných akcí použitelných pro dané nastavení. 

Následující seznam obsahuje nejčastější akce:
- **Blokovat přístup** – zablokuje koncovému uživateli přístup k podnikové aplikaci.
- **Vymazat data** – vymaže ze zařízení koncového uživatele podniková data.
- **Upozornit** – zobrazí koncovému uživateli dialogové okno s upozorněním.

V některých případech, jako u nastavení **Minimální verze operačního systému**, můžete nakonfigurovat, aby se provedly všechny použitelné akce na základě různých čísel verzí. 

![Snímek obrazovky s akcemi přístupu aplikace App Protection – minimální verze operačního systému](./media/app-protection-policies-access-actions/apps-selective-wipe-access-actions05.png)

Jakmile je nastavení plně nakonfigurované, objeví se řádek v zobrazení jen pro čtení a bude možné ho kdykoli upravit. Ve sloupci **Nastavení** bude u tohoto řádku dostupný rozevírací seznam pro výběr. Nastavení, která už jsou nakonfigurovaná a neumožňují více akcí, nebudou v tomto rozevíracím seznamu dostupná k výběru.

## <a name="next-steps"></a>Další kroky

Další informace o zásadách ochrany aplikací v Intune zjistíte zde:
- [Vytvoření a přiřazení zásad ochrany aplikací](app-protection-policies.md)
- [nastavení zásad ochrany aplikací pro iOS/iPadOS](app-protection-policy-settings-ios.md)
- [Nastavení zásad ochrany aplikací pro Android v Microsoft Intune](app-protection-policy-settings-android.md) 
