---
title: Jak monitorovat zásady ochrany aplikací
titleSuffix: Microsoft Intune
description: Toto téma popisuje, jak monitorovat zásady ochrany aplikací v Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 9b0afb7d-cd4e-4fc6-83e2-3fc0da461d02
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 39551ec60e41a7bc3d6c7f63e16f622b64a5669c
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79326263"
---
# <a name="how-to-monitor-app-protection-policies"></a>Jak monitorovat zásady ochrany aplikací
[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Stav zásad ochrany aplikací, které jste použili pro uživatele, můžete monitorovat v podokně Ochrana aplikací Intune v [Azure Portal](https://portal.azure.com). Kromě toho můžete najít informace o uživatelích ovlivněných zásadami ochrany aplikací, stavu dodržování zásad a všech problémech, se kterými se uživatelé mohou setkat.

Existují tři různá místa, kde můžete monitorovat zásady ochrany aplikací:
- Souhrnné zobrazení
- Podrobné zobrazení
- Zobrazení vytváření sestav

Doba uchování dat ochrany aplikací je 90 dní. Všechny instance aplikace, které se vrátily do služby Intune během posledních 90 dní, jsou součástí sestavy stav ochrany aplikací. *Instance aplikace* je jedinečného uživatele + aplikace a zařízení. 

> [!NOTE]
> Další informace najdete v tématu [Vytvoření a přiřazení zásad ochrany aplikací](app-protection-policies.md).

## <a name="summary-view"></a>Souhrnné zobrazení

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Vyberte **aplikace** > **monitorovat** > **stav ochrany aplikací**.

   ![Snímek obrazovky s dlaždicí souhrnu v podokně Správa mobilních aplikací Intune](./media/app-protection-policies-monitor/app-protection-user-status-summary.png)

- **Přiřazení uživatelé**: celkový počet přiřazených uživatelů ve vaší společnosti, kteří používají aplikaci přidruženou k zásadě v pracovním kontextu a jsou chráněni a licencováni, a také přiřazení nechráněných uživatelů a jejich nelicencovaných uživatelů.
- **Uživatelé označení příznakem**: počet uživatelů, u kterých dochází k problémům s jejich zařízeními. Zařízení s jailbreakem (iOS/iPadOS) a rootem (Android) se hlásí v části **Uživatelé označení příznakem**. Uživatelé se zařízeními, která jsou označená kontrolou ověření identity zařízení Google SafetyNet (Pokud je zapnutá správcem IT), jsou také uvedena zde. 
- **Uživatelé s potenciálně škodlivými aplikacemi**: počet uživatelů, kteří můžou mít v zařízení s Androidem zjištěnou škodlivou aplikaci Google Play chránit. 
- **Stav uživatele pro iOS** a **stav uživatele pro Android**: počet uživatelů, kteří použili aplikaci, která má přiřazenou zásadu v pracovním kontextu pro související platformu. Tyto informace zobrazují počet uživatelů spravovaných zásadou a také počet uživatelů, kteří používají aplikaci, na kterou necílí žádné zásady v pracovním kontextu. Tyto uživatele případně můžete k zásadě přidat.
- **Nejvyšší chráněné aplikace pro iOS/iPadOS** a **špičkové**aplikace pro Android: založené na nejpoužívanějších aplikacích pro iOS/iPadOS a Android zobrazuje tyto informace počet chráněných a nechráněných aplikací podle platformy.
- **Hlavní nakonfigurované aplikace pro iOS/IPadOS bez registrace** a **shora nakonfigurovaných aplikací pro Android bez registrace**: na základě nejpoužívanějších aplikací pro iOS/iPadOS a Android pro neregistrovaná zařízení se v těchto informacích zobrazuje počet nakonfigurovaných aplikací podle platformy (jako v systému, pomocí zásad konfigurace aplikace).

    > [!NOTE]
    > Pokud máte pro každou platformu více zásad, bude se uživatel považovat za spravovaného zásadou, pokud má přiřazenou minimálně jednu zásadu.

## <a name="detailed-view"></a>Podrobné zobrazení
Podrobné zobrazení souhrnu získáte tak, že vyberete dlaždici uživatelé s **příznakem příznaku** a **Uživatelé s potenciálně škodlivými aplikacemi** .

### <a name="flagged-users"></a>Uživatelé označení příznakem
V podrobném přehledu se zobrazí chybová zpráva, otevíraná aplikace v okamžiku chyby, dotčená platforma operačního systému zařízení a časové razítko. Tato chyba je typicky pro zařízení s jailbreakem (iOS/iPadOS) nebo rootem (Android). Uživatelé se zařízeními, která jsou označena příznakem "podmíněné spuštění ověření zařízení SafetyNet", jsou také hlášeny v důsledku ohlášení Google. Aby bylo možné uživatele odebrat ze sestavy, je třeba změnit stav samotného zařízení, které se stane po kontrole další kořenové složky (nebo jailbreaků kontrolu/SafetyNet kontrolu), která musí hlásit pozitivní výsledek. Pokud je zařízení skutečně opraveno, bude při opětovném načtení podokna provedena aktualizace na sestavě uživatelů označených příznakem.

### <a name="users-with-potentially-harmful-apps"></a>Uživatelé s potenciálně škodlivými aplikacemi
Uživatelé se zařízeními, která jsou označená pomocí kontroly podmíněného spuštění **v části vyžadovat kontrolu hrozeb u aplikací** , se zobrazí v kategorii hrozeb, která je hlášena Google. Pokud jsou v sestavě uvedené aplikace, které se nasazují přes Intune, obraťte se na vývojáře aplikace, nebo aplikaci odeberte z přiřazení uživatelům. Podrobné zobrazení ukazuje:

- **Uživatel**: jméno uživatele.
- **ID balíčku aplikace**: Toto je způsob, jakým operační systém Android jedinečně určuje aplikaci.
- **Pokud je aplikace povolená mam**: bez ohledu na to, jestli se aplikace nasazuje prostřednictvím Microsoft Intune. 
- **Kategorie hrozby**: jaká kategorie hrozeb zjištěná společností Google spadá do této aplikace. 
- **E-mail**: e-mail uživatele.
- **Název zařízení**: názvy všech zařízení, která jsou přidružená k účtu uživatele.
- **Časové razítko**: Toto je datum poslední synchronizace, kterou v obchodě s Microsoft Intune v souvislosti s potenciálně škodlivými aplikacemi.

## <a name="reporting-view"></a>Zobrazení vytváření sestav

Stejné sestavy můžete najít v horní části podokna **stav ochrany aplikací** . Pokud chcete zobrazit tyto sestavy, vyberte **aplikace** > **stav ochrany aplikace** > **sestavy**. Podokno **sestavy** obsahuje několik sestav založených na uživateli a aplikaci, včetně následujících:

### <a name="user-report"></a>Sestava uživatele

Můžete vyhledat konkrétního uživatele a zkontrolovat u něj stav dodržování předpisů. V podokně **Vytváření sestav aplikace** se zobrazují následující informace o vybraném uživateli:

- **Ikona**: zobrazuje, jestli je stav aplikace aktuální.
- **Název aplikace**: název aplikace.
- **Název zařízení**: zařízení, která jsou přidružená k účtu uživatele.
- **Typ zařízení**: typ zařízení nebo operačního systému, na kterém zařízení běží.
- **Zásady**: zásady přidružené k aplikaci.
- **Stav**:
  - **Zaregistrováno:** Zásada byla u uživatele nasazena a aplikace byla alespoň jednou použita v pracovním kontextu.
  - **Není zaregistrováno**: zásada byla nasazena uživateli, ale aplikace nebyla od té doby použita v pracovním kontextu.
- **Poslední synchronizace**: čas poslední synchronizace aplikace s Intune.

>[!NOTE]
> Sloupec **Poslední synchronizace** představuje stejnou hodnotu jak v sestavě pro stav uživatele v konzole, tak v [sestavě pro vyexportované. csv](https://docs.microsoft.com/intune/app-protection-policies-monitor#export-app-protection-activities)zásady ochrany aplikací. Rozdíl je krátké zpoždění synchronizace mezi hodnotou ve dvou sestavách.
>
> Čas, na který se odkazuje v poslední synchronizaci, je čas, kdy se naposledy viděla instance aplikace Intune. Když uživatel spustí aplikaci, může u této doby spuštění informovat službu Intune App Protection, v závislosti na tom, kdy se naposledy vrátila. Podívejte [se na časy intervalu opakování při vrácení se změnami zásad ochrany aplikací](app-protection-policy-delivery.md). Pokud uživatel nepoužil tuto konkrétní aplikaci v intervalu Poslední vrácení se změnami (což je obvykle 30 minut z aktivního použití) a spustí aplikaci, pak:
>
> - Zpráva o zásadách ochrany aplikací, kterou lze exportovat. csv, má nejnovější čas do 1 minuty (minimálně) až 30 minut (maximum).
> - Zpráva o stavu uživatele má okamžitý čas.
>
> Představte si například cílového a licencovaného uživatele, který spustí chráněnou aplikaci v 12:00. odp.:
>
> - Pokud se jedná o první přihlášení, znamená to, že uživatel byl předtím odhlášený a nemá k dispozici registraci instancí aplikace v Intune. Jakmile se uživatel přihlásí, uživatel získá novou registraci instance aplikace a může být hned vrácen se změnami (se stejným časovým zpožděním uvedeným dříve pro budoucí vrácení se změnami). Čas poslední synchronizace tedy bude 12:00 odp. v sestavě stav uživatele a 12:01 odp. (nebo 12:30 s nejnovějšími) v sestavě zásad ochrany aplikací.
> - Pokud uživatel právě spouští aplikaci, pak čas poslední synchronizace, který je hlášený, závisí na tom, kdy se uživatel naposledy vrátil.

Pokud chcete zobrazit vytváření sestav pro uživatele, postupujte takto:

1. Chcete-li vybrat uživatele, zvolte dlaždici souhrn **stavu uživatele** .

    ![Snímek obrazovky se souhrnem dlaždice Správa mobilních aplikací Intune](./media/app-protection-policies-monitor/MAM-reporting-6.png)

2. V podokně **vytváření sestav aplikací** zvolte **Vybrat uživatele** a vyhledejte uživatele Azure Active Directory.

    ![Snímek obrazovky s možností vybrat uživatele v podokně vytváření sestav aplikací](./media/app-protection-policies-monitor/MAM-reporting-2.png)

3. Vyberte uživatele ze seznamu. Zobrazí se podrobné informace o konkrétním uživateli a stavu dodržování předpisů.

>[!NOTE]
> Pokud uživatel, kterého jste hledali, nemá nasazené zásady MAM, zobrazí se zpráva, že na uživatele není zacílená žádná zásada MAM.

### <a name="app-report"></a>Sestava aplikace
Můžete hledat podle platformy a aplikace a pak tato sestava poskytne dva různé stavy ochrany aplikací, které můžete vybrat před generováním sestavy. Stav může být **chráněný** nebo **nechráněný**.

  - Stav uživatele pro spravovanou aktivitu MAM (**chráněno**): Tato sestava popisuje aktivity každé spravované aplikace mam na jednotlivých uživatelích. Zobrazuje všechny aplikace, které jsou cílem zásad MAM pro jednotlivé uživatele, a stav každé aplikace, jak se zaregistrované v zásadách MAM. Sestava také zahrnuje stav každé aplikace, která byla cílem zásad MAM, ale nikdy se nevrátila.
  - Stav uživatele pro nespravovanou aktivitu MAM (**Nechráněno**): Tato sestava popisuje aktivity aplikací s podporou mam, které jsou aktuálně nespravované, podle jednotlivých uživatelů. K tomu může dojít z těchto důvodů:
    - Tyto aplikace používá uživatel nebo aplikace, na které aktuálně necílí zásady MAM.
    - Všechny aplikace jsou zaregistrované, ale nejsou u nich použité žádné zásady MAM.

    ![Snímek obrazovky s podoknem vytváření sestav aplikace uživatele s podrobnostmi pro tři aplikace](./media/app-protection-policies-monitor/MAM-reporting-4.png)

### <a name="user-configuration-report"></a>**Sestava konfigurace uživatele**
V závislosti na vybraném uživateli Tato sestava obsahuje podrobnosti o všech konfiguracích aplikace, které uživatel přijal.

### <a name="app-configuration-report"></a>**Sestava konfigurace aplikace**
V závislosti na vybrané platformě a aplikaci Tato sestava obsahuje podrobnosti o tom, kteří uživatelé přijali konfigurace pro vybranou aplikaci.

### <a name="app-learning-report-for-windows-information-protection"></a>Sestava o studiu aplikací pro Windows Information Protection
Tato sestava zobrazuje, které aplikace se pokoušejí o vzájemné hranice zásad.

### <a name="website-learning-for-windows-information-protection"></a>Školení k webu pro Windows Information Protection
Tato sestava ukazuje, které weby se pokoušejí o vzájemné hranice zásad.

## <a name="export-app-protection-activities"></a>Exportovat aktivity ochrany aplikací
Všechny aktivity ochrany aplikací můžete vyexportovat do jediného souboru .csv. To může být užitečné při analýze všech stavů ochrany aplikací hlášených od uživatelů. V **souboru App Protection. CSV se zobrazuje**:
- **Uživatel**: jméno uživatele.
- **E-mail**: e-mail uživatele.
- **Aplikace**: název aplikace.
- **Verze aplikace**: verze aplikace
- **Název zařízení**: názvy všech zařízení, která jsou přidružená k účtu uživatele.
- **Výrobce zařízení**: uvádí výrobce zařízení (pouze Android). 
- **Model zařízení**: v této části je uveden výrobce zařízení (pouze Android). 
- **Verze opravy Androidu**: datum poslední opravy zabezpečení Androidu.
- **ID zařízení AAD**: Tento sloupec se naplní, pokud je zařízení připojené k AAD.
- **ID zařízení MDM**: Tento sloupec se naplní, pokud je zařízení zaregistrované Microsoft Intune MDM.
- **Platforma**: operační systém.
- **Verze platformy**: verze operačního systému.
- **Typ správy**: typ správy na zařízení. Například Android Enterprise, unmanaged nebo MDM.  
- **Stav ochrany aplikací**: Nechráněno nebo chráněno.
- **Zásada**: zásady ochrany aplikací přidružené k aplikaci.
- **Poslední synchronizace**: čas poslední synchronizace aplikace s Microsoft Intune. 
- **Stav dodržování předpisů**: Určuje, jestli je aplikace na zařízení uživatele kompatibilní se všemi zásadami podmíněného přístupu na základě aplikace.  

Pomocí těchto kroků vygenerujte soubor. CSV aplikace App Protection nebo soubor konfigurace aplikace. CSV:

1. V podokně správy mobilních aplikací Intune zvolte **Sestava ochrany aplikací**.

    ![Snímek obrazovky s odkazem ke stažení ochrany aplikace](./media/app-protection-policies-monitor/app-protection-report-csv-2.png)

2. Kliknutím na **tlačítko Ano** sestavu uložíte a pak zvolte možnost **Uložit jako**. Vyberte složku, do které chcete sestavu uložit.

    ![Snímek obrazovky pole pro potvrzení uložení sestavy](./media/app-protection-policies-monitor/app-protection-report-csv-1.png)
   
> [!NOTE]
> Intune poskytuje další pole pro vytváření sestav zařízení, včetně ID registrace aplikace, výrobce Androidu, modelu a verze opravy zabezpečení i modelu iOS/iPadOS. V Intune získáte přístup k těmto polím výběrem možnosti **aplikace** > **stav ochrany aplikace** > **Sestava ochrany aplikací: iOS/iPadOS, Android**. Kromě toho tyto parametry pomůžou nakonfigurovat seznam **povolených** pro výrobce zařízení (Android), seznam **povolených** nastavení pro model zařízení (Android a iOS/iPadOS) a **minimální verzi opravy zabezpečení Androidu** .   
 
## <a name="see-also"></a>Viz také
- [Správa přenosu dat mezi aplikacemi pro iOS/iPadOS](data-transfer-between-apps-manage-ios.md)
- [Co očekávat, když ke správě svojí aplikace pro Android používáte zásady ochrany aplikací](../fundamentals/end-user-mam-apps-android.md)
- [Co očekávat, když je vaše aplikace pro iOS/iPadOS spravovaná zásadami ochrany aplikací](../fundamentals/end-user-mam-apps-ios.md)
