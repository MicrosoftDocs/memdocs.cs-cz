---
title: Zásady ochrany aplikací a pracovní profily v Microsoft Intune – Azure | Microsoft Docs
description: Pokud se rozhodnete používat zásady ochrany aplikací nebo pracovní profily pro osobní nebo BYOD zařízení se systémem Android Enterprise v Microsoft Intune, podívejte se na rozdíly a specialisty a nevýhody. Porovnáním rozdílů a funkcí, které se budou používat v zásadách ochrany aplikací bez registrace (APP-WE) a Android Enterprise Working Profiles.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/13/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: ea67d432f3f418b4ecc592462d93e7d4da3676f6
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79327407"
---
# <a name="application-protection-policies-and-work-profiles-on-android-enterprise-devices-in-intune"></a>Zásady ochrany aplikací a pracovní profily na zařízeních s Androidem Enterprise v Intune

V mnoha organizacích jsou správci vyzváni k ochraně prostředků a dat na různých zařízeních. Jedna z těchto výzev chrání prostředky pro uživatele pomocí osobních zařízení s Androidem Enterprise, označovaných také jako vlastní zařízení (BYOD). Microsoft Intune podporuje dva scénáře nasazení Androidu pro vlastní zařízení (BYOD):

- Zásady ochrany aplikací bez registrace (APP-WE)
- Podnikové pracovní profily Androidu

Scénáře nasazení v rámci aplikace a a Androidu pro nasazení pracovních profilů zahrnují následující klíčové funkce, které jsou důležité pro BYOD prostředí:

1. **Ochrana a oddělení dat spravovaných organizací**: obě řešení chrání data organizace tím, že vynucuje ovládací prvky ochrany před únikem informací (DLP) na data spravovaná organizací. Tyto ochrany zabraňují náhodnému úniku chráněných dat, jako je například koncový uživatel náhodně ho sdílí s osobní aplikací nebo účtem. Slouží také k tomu, aby se zajistilo, že zařízení, které přistupuje k datům, je v pořádku a není ohroženo.

2. **Ochrana osobních údajů koncového uživatele**: App-We a Android Enterprise Worker oddělují obsah koncových uživatelů na zařízení a data spravovaná správcem správy mobilních zařízení (MDM). V obou scénářích vynutili správci IT zásady, jako je ověřování pouze kódem PIN pro aplikace nebo identity spravované organizací. Správci IT nemohou číst, přistupovat ani mazat data, která jsou vlastněná nebo řízená koncovými uživateli.

Bez ohledu na to, jestli pro nasazení BYOD zvolíte pracovní profily APP-WE nebo Android Enterprise, záleží na vašich požadavcích a obchodních potřebách. Cílem tohoto článku je poskytnout pokyny, které vám pomůžou při rozhodování.

## <a name="about-intune-app-protection-policies"></a>Informace o zásadách ochrany aplikací Intune

Zásady ochrany aplikací Intune (aplikace) jsou zásady ochrany dat cílené na uživatele. Zásady používají ochranu před únikem informací na úrovni aplikace. APLIKACE Intune vyžaduje, aby vývojáři aplikací povolili funkce aplikací v aplikacích, které vytvořili.

Jednotlivé aplikace pro Android jsou aplikacím povoleny v několika ohledech:

1. **Nativně integrovaná do aplikací Microsoft First stran**: systém Microsoft Office aplikace pro Android a výběr dalších aplikací Microsoftu, které jsou součástí integrovaného předdefinovaného aplikace Intune. Tyto aplikace Office, jako jsou Word, OneDrive, Outlook atd., nevyžadují žádné další přizpůsobení, abyste mohli aplikovat zásady. Tyto aplikace můžou instalovat koncoví uživatelé přímo z Obchod Google Play.

2. **Integrováno do buildů aplikací vývojáři, kteří používají Intune SDK**: vývojáři aplikací mohou INTEGROVAt sadu Intune SDK do zdrojového kódu a znovu kompilovat své aplikace, aby podporovaly funkce zásad aplikací Intune.

3. **Zabalené pomocí nástroje pro zabalení aplikace Intune**: někteří zákazníci zkompiluje aplikace pro Android (. Soubor APK) bez přístupu ke zdrojovému kódu. Bez zdrojového kódu nemůže vývojář integrovat se sadou Intune SDK. Bez SDK nemůžou povolit svoji aplikaci pro zásady aplikací. Vývojář musí aplikaci upravit nebo Recode, aby podporovala zásady aplikací.

    Intune vám umožní využít nástroj pro **zabalení aplikace** pro existující aplikace pro Android (kopírují) a vytvoří aplikaci, která rozpoznává zásady pro aplikace.

    Další informace o tomto nástroji najdete v tématu [Příprava obchodních aplikací na zásady ochrany aplikací](../developer/apps-prepare-mobile-application-management.md).

Pokud chcete zobrazit seznam aplikací povolených pro aplikaci, přečtěte si téma [spravované aplikace s bohatou sadou zásad ochrany mobilních aplikací](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).

## <a name="deployment-scenarios"></a>Scénáře nasazení

Tato část popisuje důležité charakteristiky scénářů nasazení pracovních profilů pro aplikace a Android Enterprise.

### <a name="app-we"></a>APP-WE

APLIKACE – nasazení (zásady ochrany aplikací bez registrace) definuje zásady pro aplikace, ne zařízení. V tomto scénáři zařízení obvykle nejsou zaregistrovaná nebo spravovaná autoritou MDM, jako je třeba Intune. Aby mohli správci chránit aplikace a přistupovat k datům organizace, používají aplikace spravované aplikací a pro tyto aplikace platí zásady ochrany dat.

Tato funkce platí pro:

- Android 4,4 a novější

> [!TIP]
> Další informace najdete v tématu [co jsou zásady ochrany aplikací?](app-protection-policy.md).

Scénáře pro aplikace jsou pro koncové uživatele, kteří na svých zařízeních chtějí malé organizační nároky a nechtějí se registrovat v MDM. Jako správce je stále potřeba chránit vaše data. Tato zařízení nejsou spravovaná. Běžné úlohy a funkce MDM, jako je Wi-Fi, VPN zařízení a Správa certifikátů, nejsou součástí tohoto scénáře nasazení.

### <a name="android-enterprise-work-profiles"></a>Podnikové pracovní profily Androidu

Pracovní profily jsou základním scénářem nasazení Android Enterprise a jediným scénářem, který je zaměřený na BYOD případy použití. Pracovní profil je samostatný oddíl vytvořený na úrovni operačního systému Android, který se dá spravovat přes Intune.

Tato funkce platí pro:

- Zařízení s Androidem 5,0 a novějším s Google Mobile Services

Pracovní profil obsahuje následující funkce:

- **Tradiční funkce MDM**: Klíčové možnosti MDM, jako je například Správa životního cyklu aplikací pomocí spravovaného Google Play, jsou k dispozici v jakémkoli scénáři Android Enterprise. Spravovaná Google Play poskytuje robustní prostředí pro instalaci a aktualizaci aplikací bez zásahu uživatele. Může taky zaručovat nastavení konfigurace aplikací do organizačních aplikací. Také nevyžaduje, aby koncoví uživatelé povolili instalace z neznámých zdrojů. Další běžné aktivity MDM, jako je například nasazení certifikátů, konfigurace Wi-Fi/VPN a nastavení hesla zařízení, jsou k dispozici v pracovních profilech.

- Ochrana **před únikem informací na hranici pracovního profilu**: například App-We, může vyhovět zásadám ochrany dat. S pracovním profilem se zásady ochrany před únikem informací vynutily na úrovni pracovního profilu, ne na úrovni aplikace. Například ochrana kopírování/vkládání se vynutila nastavením aplikace použitým pro aplikaci nebo vynutil pracovní profil. Po nasazení aplikace do pracovního profilu můžou správci pozastavit ochranu kopírováním a vkládáním do pracovního profilu tím, že tuto zásadu vypíná na úrovni aplikace.

## <a name="tips-to-optimize-the-work-profile-experience"></a>Tipy k optimalizaci prostředí pracovních profilů

### <a name="when-to-use-app-within-work-profiles"></a>Kdy použít aplikaci v pracovních profilech

APLIKACE Intune a pracovní profily představují doplňkové technologie, které se dají použít společně nebo samostatně. V rámci architektury vynutila obě řešení zásady v různých vrstvách – aplikace na jednotlivých vrstvách aplikace a pracovní profil ve vrstvě profilace. Nasazení aplikací spravovaných zásadou aplikace do aplikace v pracovním profilu je platný a podporovaný scénář. Pokud chcete používat aplikaci, pracovní profily nebo kombinaci, záleží na vašich požadavcích na ochranu před únikem informací.

Pracovní profily a aplikace doplňují všechna ostatní nastavení tím, že poskytují dodatečné pokrytí v případě, že jeden profil nesplňuje požadavky vaší organizace na ochranu dat. Například pracovní profily neposkytují nativně ovládací prvky pro omezení aplikace na ukládání do nedůvěryhodného umístění úložiště v cloudu. Tato funkce zahrnuje aplikaci. Můžete se rozhodnout, že ochrana před únikem informací, která je k dispozici výhradně v pracovním profilu, je dostatečná a zvolte možnost Nepoužívat aplikaci. Případně můžete vyžadovat ochranu z kombinace těchto dvou.

### <a name="suppress-app-policy-for-work-profiles"></a>Potlačit zásady aplikací pro pracovní profily

Možná budete muset podporovat jednotlivé uživatele, kteří mají více zařízení nespravovaných zařízeními ve scénáři APP-WE a spravovaná zařízení s pracovními profily.

Vyžadujete například, aby koncoví uživatelé při otevírání pracovní aplikace zadali kód PIN. V závislosti na zařízení jsou funkce PIN zpracovávány aplikací nebo pracovním profilem. Pro zařízení, která jsou v aplikaci, se chování kódem PIN na spuštění vynutilo aplikací. Pro zařízení pracovních profilů můžete použít PIN kód zařízení nebo pracovního profilu, který vynutil operační systém. Pro dosažení tohoto scénáře nakonfigurujte nastavení aplikace tak, aby se *nepři* nasazení aplikace do pracovního profilu neprojevila. Pokud ho nenastavíte tímto způsobem, koncový uživatel se zobrazí výzva k zadání PIN kódu zařízení a znovu ve vrstvě aplikace.

### <a name="control-multi-identity-behavior-in-work-profiles"></a>Řízení chování více identit v pracovních profilech

Aplikace Office, jako je například Outlook a OneDrive, mají chování s více identitami. V rámci jedné instance aplikace může koncový uživatel přidat připojení k více jedinečným účtům nebo umístěním cloudového úložiště. V rámci aplikace lze data získaná z těchto umístění oddělit nebo sloučit. A uživatel může kontext přepnout mezi osobními identitami (user@outlook.com) a identitami organizace (user@contoso.com).

Pokud používáte pracovní profily, možná budete chtít zakázat toto chování s více identitami. Když ho zakážete, budou se s označením instance aplikace v pracovním profilu moct konfigurovat jenom s identitou organizace. Použijte nastavení konfigurace aplikace povolených účtů pro podporu aplikací Office pro Android.

Další informace najdete v tématu [nasazení aplikace Outlook pro iOS/iPadOS a nastavení konfigurace aplikací pro Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune).

## <a name="when-to-use-intune-app"></a>Kdy použít aplikaci Intune

K dispozici je několik scénářů pro podnikovou mobilitu, kde je použití aplikace Intune nejlepší doporučení.

### <a name="older-devices-running-android-44-51-are-being-used"></a>Používají se starší zařízení se systémem Android 4.4-5.1.

V oficiálním případě všechny zařízení s Androidem 5,0 nebo vyšší s Google Mobile Services podporuje pracovní profily a v takovém případě mají nárok na správu. Některá zařízení s Androidem 5,0 a 5,1 však někteří výrobci OEM nepodporují pracovní profily.

Pokud používáte verze, které nepodporují pracovní profily, a k zajištění ochrany před únikem informací organizace na zařízeních, musíte použít funkce aplikace Intune.

### <a name="no-mdm-no-enrollment-google-services-are-unavailable"></a>Žádná MDM, žádné registrace, služby Google nejsou k dispozici

Někteří zákazníci nepotřebují žádnou formu správy zařízení, včetně správy pracovních profilů, a to z různých důvodů:

- Důvody právního a ručení
- Pro zajištění konzistence uživatelského prostředí
- Prostředí zařízení s Androidem je vysoce heterogenní
- Neexistují žádné možnosti připojení ke službám Google, které se vyžadují pro správu pracovních profilů.

Například zákazníci, kteří mají nebo mají uživatele v Číně, nemůžou používat správu zařízení s Androidem, protože jsou blokované služby Google. V takovém případě použijte k ochraně před únikem informací aplikaci Intune.

## <a name="summary"></a>Souhrn

V Intune jsou pro váš program pro Android BYOD k dispozici obě pracovní profily APP-WE i Android Enterprise. Pokud chcete zvolit APP-WE nebo pracovní profily, záleží na vašich firmách a požadavcích na použití. V souhrnu použijte pracovní profily, pokud potřebujete aktivity MDM na spravovaných zařízeních, jako je nasazení certifikátů, nabízení aplikace atd. Použijte APP-WE, pokud nechcete nebo nemůžete spravovat zařízení a používáte jenom aplikace s podporou aplikací Intune.

## <a name="next-steps"></a>Další kroky
[Začněte používat zásady ochrany aplikací](app-protection-policy.md)nebo [svoje zařízení zaregistrovat](../enrollment/android-enroll.md).
