---
title: Nastavení omezení zařízení s Androidem v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na seznam všech nastavení zařízení s Androidem, které můžete v Microsoft Intune ovládat nebo omezit. Tato nastavení můžete použít k ovládání hesla, přístupu ke Google Play, povolení nebo zakázání aplikací, ovládání nastavení prohlížeče, blokování aplikací, zálohování do cloudu Google, ovládání zpráv, hlasového volání, datového roamingu a možností připojení k Wi-Fi nebo prostřednictvím technologie Bluetooth.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/19/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: ayesham, chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a38a7a0e191990871724e217d84c6bd8babb12dc
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332331"
---
# <a name="android-and-samsung-knox-standard-device-restriction-settings-lists-in-intune"></a>Seznamy nastavení omezení zařízení s Androidem a Samsung KNOX standard v Intune

Tento článek ukazuje všechna nastavení omezení zařízení v Microsoft Intune, která můžete nakonfigurovat pro zařízení s Androidem.

>[!TIP]
>Pokud požadovaná nastavení nejsou k dispozici, možná budete moct zařízení nakonfigurovat pomocí [vlastního profilu](custom-settings-android.md).

## <a name="general"></a>Obecné

- **Kamera**: vyberte možnost **blokovat** , pokud chcete zabránit přístupu k fotoaparátu. **Nenakonfigurováno** umožňuje přístup k kameře zařízení.
- **Kopírování a vkládání (jenom Samsung KNOX)** : vyberte **blok** , aby se zabránilo kopírování a vkládání. **Není nakonfigurováno** , umožňuje funkce kopírování a vkládání na zařízení.
- **Sdílení schránky mezi aplikacemi (jenom Samsung KNOX)** : vyberte **blok** , aby se zabránilo použití schránky pro kopírování a vkládání mezi aplikacemi. **Není nakonfigurováno** umožňuje použití schránky ke kopírování a vkládání mezi aplikacemi.
- **Odeslání diagnostických dat (jenom Samsung KNOX)** : výběrem možnosti **blokovat** zabráníte uživateli v odesílání zpráv o chybách ze zařízení. **Není nakonfigurováno** umožňuje uživateli odeslat data.
- **Vymazat (jenom Samsung KNOX)** : umožňuje uživateli na zařízení spustit akci [vymazání](../remote-actions/devices-wipe.md) .
- **Zeměpisná poloha (jenom Samsung KNOX)** : Pokud chcete zakázat používání informací o poloze zařízení, vyberte **blokovat** . **Není nakonfigurováno** , umožňuje zařízení používat informace o poloze.
- **Vypnutí (jenom Samsung KNOX)** : vyberte **blok** , aby se zabránilo uživateli v vypnutí zařízení. Pokud je toto nastavení zakázané, **počet neúspěšných přihlášení před vymazáním nastavení zařízení** nepůjde nastavit a nefunguje. **Nenakonfigurováno** umožňuje uživateli vypnout zařízení.
- **Snímek obrazovky (jenom Samsung KNOX)** : vyberte **blok** pro zabránění snímků obrazovky. **Není nakonfigurováno** umožňuje uživateli zachytit obsah obrazovky jako obrázek.
- **Hlasový asistent (jenom Samsung KNOX)** : Pokud chcete zakázat hlasovou službu S, vyberte možnost **blokovat** . **Není nakonfigurováno** , umožňuje použití hlasové služby a aplikace v zařízení. Toto nastavení se nevztahuje na Bixby nebo hlasového asistenta pro přístupnost, který čte obsah obrazovky nahlas.
- **YouTube (jenom Samsung KNOX)** : Pokud chcete uživatelům zabránit v používání aplikace YouTube, vyberte **blokovat** . Možnost **Nenakonfigurováno** umožňuje použití aplikace YouTube na zařízení.
- **Sdílená zařízení (jenom Samsung KNOX)** : Nakonfigurujte spravované zařízení Samsung KNOX Standard jako sdílené. Pokud je nastavené na **povoleno**, koncoví uživatelé se můžou k zařízení přihlašovat pomocí svých přihlašovacích údajů Azure AD. Zařízení zůstává spravované bez ohledu na to, jestli se používá.</br>Při použití v s profilem certifikátu SCEP Tato funkce umožňuje koncovým uživatelům sdílet zařízení se stejnými aplikacemi pro všechny uživatele. Každý uživatel ale má vlastní certifikát uživatele SCEP. Po odhlášení uživatelů se všechna data aplikací vymažou. Tato funkce je omezená jenom na obchodní aplikace. </br>**Nenakonfigurováno** zabraňuje více koncovým uživatelům přihlásit se k aplikaci Portál společnosti na zařízení pomocí svých přihlašovacích údajů Azure AD.
- **Zablokovat změny data a času (Samsung KNOX)** : Pokud chcete zabránit uživateli ve změně nastavení data a času na zařízení, vyberte **blokovat** . **Není nakonfigurováno** umožňuje uživatelům změnit nastavení data a času.

## <a name="password"></a>Heslo

- **Heslo**: **vyžaduje** , aby koncový uživatel zadal heslo pro přístup k zařízení. **Nenakonfigurováno** umožňuje uživatelům přístup k zařízení bez zadání hesla.

    > [!NOTE]
    > Při registraci MDM zařízení Samsung Knox automaticky vyžadují 4místný číselný kód PIN. Nativní zařízení s Androidem můžou automaticky vyžadovat PIN kód, aby mohl být kompatibilní s podmíněným přístupem.

- **Minimální délka hesla**: zadejte minimální délku hesla, které uživatel musí zadat (mezi 4 a 16 znaky).
- **Maximální počet minut nečinnosti, po kterém se zamkne obrazovka**: zadejte maximální počet minut nečinnosti povolený v zařízení, dokud se obrazovka nezamkne. V zařízení nemůže koncový uživatel nastavit časovou hodnotu větší než nakonfigurovaný čas v profilu. Může ale nastavit kratší časovou hodnotu. Pokud je v profilu nastaveno třeba 15 minut, může koncový uživatel nastavit 5 minut, Koncový uživatel nemůže nastavit hodnotu na 30 minut. 
- **Počet neúspěšných přihlášení před vymazáním zařízení**: zadejte počet povolených neúspěšných přihlášení, než se zařízení vymaže.
- **Vypršení platnosti hesla (dny)** : zadejte počet dní, než bude nutné změnit heslo zařízení.
- **Vyžadovaný typ hesla**: zadejte požadovanou úroveň složitosti hesla a to, jestli se můžou používat biometrická zařízení. Možnosti:
  - **Výchozí ze zařízení**
  - **Biometrika s nízkým zabezpečením**
  - **Aspoň číslice**
  - **Číselná složitá**: opakující se nebo po sobě jdoucí čísla, například "1111" nebo "1234", nejsou povolena. <sup>1</sup>
  - **Aspoň abecední znaky**
  - **Aspoň alfanumerické znaky**
  - **Aspoň alfanumerické se symboly**
- **Zakázat opakované použití předchozích hesel**: zastaví koncovému uživateli vytvoření hesla, které předtím používali.
- **Odemknutí otiskem prstu (jenom Samsung KNOX)** : vyberte **blok** , abyste zabránili použití otisku prstu k odemknutí zařízení. **Není nakonfigurováno** umožňuje uživateli odemknout zařízení pomocí otisku prstu.
- **Smart Lock a jiní agenti**pro určování důvěryhodnosti: vyberte **blok** , aby Smart Lock nebo jiní agenti pro určování důvěryhodnosti zabránili v úpravě nastavení ZAMYKACÍ obrazovky (Samsung KNOX standard 5.0 +). Tato funkce telefonu, která se někdy označuje jako agent pro určování důvěryhodnosti, umožňuje zakázat nebo obejít heslo zamykací obrazovky zařízení, pokud se zařízení nachází v důvěryhodném umístění. Tato funkce se dá použít například v případě, že je zařízení připojené k určitému zařízení Bluetooth nebo když se nachází blízko značky NFC. Pomocí tohoto nastavení můžete uživatelům zabránit v konfiguraci funkce Smart Lock.
- **Šifrování**: vyberte **vyžadovat** , aby byly soubory v zařízení šifrované. Ne všechna zařízení podporují šifrování. Chcete-li použít tuto funkci, postupujte také takto: 
  1. Nastavte **heslo** na **povinné**.
  2. Nastavte **požadovaný typ hesla** **aspoň na číslo**.
  3. Nastavte **minimální délku hesla** aspoň na 4 pro správné hlášení dodržování předpisů pro toto nastavení.

  > [!NOTE]
  > Pokud se vynucují zásady šifrování, zařízení Samsung Knox po uživatelích vyžadují nastavení šestiznakového složitého hesla jako hesla k zařízení.

<sup>1</sup> před přiřazením tohoto nastavení k zařízením nezapomeňte aktualizovat aplikaci Portál společnosti na nejnovější verzi na těchto zařízeních.

Pokud nastavíte **požadovaný typ hesla** na **číselné komplexní**a pak ho přiřadíte k zařízení, na kterém je spuštěná verze androidu starší než 5,0, platí následující chování:

- Pokud Portál společnosti aplikace používá verzi starší než 1704, neaplikují se na zařízení žádné zásady PIN kódu a v centru pro správu Microsoft Endpoint Manageru se zobrazí chyba.
- Pokud aplikace Portál společnosti používá verzi 1704 nebo novější, je možné použít jenom jednoduchý PIN kód. Verze Androidu starší než 5,0 Toto nastavení nepodporují. V centru pro správu Microsoft Endpoint Manageru se nezobrazí žádná chyba.

## <a name="google-play-store"></a>Obchod Google Play

- **Google Play Store (jenom Samsung KNOX)** : Pokud chcete uživatelům zabránit v používání úložiště Google Play, vyberte **blokovat** . **Nenakonfigurováno** umožňuje uživateli přístup k Google Play Storu na zařízení.

## <a name="restricted-apps"></a>Omezené aplikace

Pomocí těchto nastavení můžete na zařízení zakázat nebo zakázat konkrétní aplikace. Tato funkce je podporovaná v zařízeních s Androidem a Samsung KNOX Standard:

- **Zakázané aplikace**: seznam aplikací, které nejsou spravované přes Intune, které nechcete na zařízení nainstalovat. Pokud uživatel z tohoto seznamu nainstaluje aplikaci, budete Intune informovat.
- **Schválené aplikace**: seznam aplikací, které uživatelé můžou instalovat. Aby bylo možné zachovat dodržování předpisů, uživatelé nesmí instalovat jiné aplikace. Aplikace, které spravuje Intune, jsou povolené automaticky.

K přidání aplikace do těchto seznamů můžete:

- **Přidejte** obchod Google Play URL aplikace, kterou chcete. Pokud například chcete přidat aplikaci Vzdálená plocha Microsoft pro Android, zadejte `https://play.google.com/store/apps/details?id=com.microsoft.rdc.android`. Pokud chcete najít adresu URL aplikace, otevřete [Google Play Store](https://play.google.com/store/apps)a vyhledejte aplikaci. Vyhledejte například `Microsoft Remote Desktop Play Store` nebo `Microsoft Planner`. Vyberte aplikaci a zkopírujte adresu URL.
- Importujte soubor CSV s podrobnostmi o aplikaci, včetně adresy URL. Použijte*adresu URL aplikace*< >, <*název aplikace*> < formát*vydavatele aplikace*>. Případně **exportujte** existující seznam obsahující seznam aplikací s omezeným přístupem ve stejném formátu.

> [!IMPORTANT]
> Profily zařízení, které používají nastavení aplikací s omezeným přístupem, se musí přiřadit ke skupinám uživatelů.

## <a name="browser"></a>Prohlížeč

- **Webový prohlížeč (jenom Samsung KNOX)** : vyberte možnost **blokovat** , aby se zabránilo použití výchozího webového prohlížeče na zařízení. **Není nakonfigurováno** , umožňuje používat výchozí webový prohlížeč zařízení.
- **Automatické vyplňování (jenom Samsung KNOX)** : Pokud chcete zabránit automatickému vyplnění textu v prohlížeči, vyberte **blokovat** . **Není nakonfigurováno** umožňuje použít funkci automatického vyplňování webového prohlížeče.
- **Soubory cookie (jenom Samsung KNOX)** : vyberte, jak chcete soubory cookie zpracovávat z webů na zařízení. Možnosti:
  - Povolit
  - Blokovat všechny soubory cookie
  - Povolení souborů cookie z navštívených webů
  - Povoluje soubory cookie z aktuálního webu
- **JavaScript (jenom Samsung KNOX)** : vyberte **blok** , aby se zabránilo spouštění skriptů Java ve webovém prohlížeči. **Není nakonfigurováno** , umožňuje webovému prohlížeči v zařízení spouštět skripty Java.
- **Automaticky otevíraná okna (jenom Samsung KNOX)** : výběrem možnosti **blokovat** zabráníte automaticky otevíraná okna ve webovém prohlížeči. **Nenakonfigurováno** umožňuje automaticky otevíraná okna ve webovém prohlížeči.

## <a name="allow-or-block-apps"></a>Povolení nebo blokování aplikací

Pomocí těchto nastavení můžete na zařízeních se Samsung KNOX standardem zapnout, blokovat nebo skrýt konkrétní aplikace. Skryté aplikace nemůže otevřít nebo spustit uživatel.

Možnosti:

- **Aplikace, které je možné nainstalovat (pouze Samsung Knox Standard)**
- **Aplikace, jejichž spouštění je blokováno (pouze Samsung Knox Standard)**
- **Aplikace, které jsou před uživatelem skryty (pouze Samsung Knox Standard)**

Pro každé nastavení přidejte seznam aplikací. Možnosti:

- **Přidat aplikace podle názvu balíčku**: primárně se používá pro obchodní aplikace. Zadejte název aplikace a název balíčku aplikace.
- **Přidat aplikace podle adresy URL**: zadejte název aplikace a její adresu url do Google Play Storu.
- **Přidat aplikaci pro Store**: vyberte aplikaci ze stávajícího seznamu aplikací, které spravujete v Intune.

## <a name="cloud-and-storage"></a>Cloud a úložiště

- **Zálohování Google (jenom Samsung KNOX)** : Pokud chcete zabránit synchronizaci zařízení s zálohováním na Google, vyberte **blokovat** . **Nenakonfigurováno** umožňuje použití zálohování Google.
- **Automatická synchronizace účtu Google (jenom Samsung KNOX)** : Pokud chcete zabránit funkci automatického synchronizace účtu Google na zařízení, vyberte **blokovat** . **Nenakonfigurováno** umožňuje automatickou synchronizaci nastavení účtu Google.
- **Vyměnitelné úložiště (jenom Samsung KNOX)** : Pokud chcete zabránit tomu, aby zařízení používalo Vyměnitelné úložiště, vyberte **blokovat** . **Nenakonfigurované** : umožňuje zařízení používat Vyměnitelné úložiště, třeba SD kartu.
- **Šifrování na paměťových kartách (jenom Samsung KNOX)** : **vyžaduje** vynutit, aby se paměťové karty musely šifrovat. **Není nakonfigurováno** , umožňuje používat nešifrované paměťové karty. Ne všechna zařízení podporují šifrování paměťové karty. Pokud ho chcete ověřit, obraťte se na výrobce zařízení.

## <a name="cellular-and-connectivity"></a>Mobilní síť a připojení

- **Datový roaming (jenom Samsung KNOX)** : vyberte **blok** , aby se zabránilo datovému roamingu v mobilní síti. Možnost **Nenakonfigurováno** povolí datový roaming, když je zařízení v mobilní síti.
- **Zasílání zpráv SMS a MMS (jenom Samsung KNOX)** : Pokud chcete zabránit textovému zasílání zpráv na zařízení, vyberte **blokovat** . **Není nakonfigurováno** , umožňuje na zařízení používat zprávy SMS a MMS.
- **Hlasové vytáčení (jenom Samsung KNOX)** : Pokud chcete zabránit uživatelům používat funkci hlasového vytáčení na zařízení, vyberte **blokovat** . **Nenakonfigurováno** umožňuje hlasové vytáčení zařízení.
- **Hlasový roaming (jenom Samsung KNOX)** : Pokud chcete zabránit hlasovému roamingu přes mobilní síť, vyberte **blokovat** . Možnost **Nenakonfigurováno** umožňuje hlasový roaming, když je zařízení v mobilní síti.
- **Bluetooth (jenom Samsung KNOX)** : Pokud chcete zabránit použití Bluetooth na zařízení, vyberte **blokovat** . **Není nakonfigurováno** , umožňuje v zařízení používat technologii Bluetooth.
- **NFC (jenom Samsung KNOX)** : vyberte **blok** pro zastavení technologie NFC (Near Field Communication). **Nenakonfigurováno** umožňuje operace, které na podporovaných zařízeních používají bezkontaktní komunikaci.
- **Wi-Fi (jenom Samsung KNOX)** : Pokud chcete zabránit použití Wi-Fi na zařízení, vyberte **blokovat** . Možnost **Nenakonfigurováno** umožňuje použití funkcí Wi-Fi zařízení.
- **Sdílení internetového připojení přes Wi-Fi (jenom Samsung KNOX)** : Pokud chcete zabránit použití internetového připojení přes Wi-Fi na zařízení, vyberte **blokovat** . **Není nakonfigurováno** umožňuje na zařízení používat sdílení Wi-Fi.

## <a name="kiosk"></a>Veřejný terminál

Nastavení platí jen pro zařízení se zabezpečením Samsung Knox Standard a jen pro aplikace, které spravujete přes Intune.

- Přidejte aplikace, které chcete spustit, když je zařízení v celoobrazovkovém režimu. V celoobrazovkovém režimu se spustí jenom aplikace, které přidáte. Nepřidání aplikací neběží. Předem nainstalované prohlížeče se nespouštějí jako aplikace, když je zařízení v celoobrazovkovém režimu. Pokud se vyžaduje prohlížeč, zvažte použití řešení [Managed Browser](../apps/app-configuration-managed-browser.md).

  Možnosti vaší aplikace:

  - **Přidat aplikace podle názvu balíčku**: primárně se používá pro obchodní aplikace. Zadejte název aplikace a název balíčku aplikace.
  - **Přidat aplikace podle adresy URL**: zadejte název aplikace a její adresu url do Google Play Storu.
  - **Přidat aplikaci pro Store**: vyberte aplikaci ze stávajícího seznamu aplikací, které spravujete v Intune.

- **Tlačítko pro režim spánku obrazovky**: vyberte **blok** a zabraňte nebo skryjte tlačítko režimu spánku obrazovky. Možnost **Nenakonfigurováno** umožňuje na zařízení tlačítko probuzení z režimu spánku obrazovky.
- **Tlačítka hlasitosti**: vyberte možnost **blokovat** , pokud chcete uživateli zabránit v úpravách svazku vypnutím tlačítek hlasitosti. Možnost **Nenakonfigurováno** umožňuje použití tlačítek hlasitosti na zařízení.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).

Můžete také vytvořit profily celoobrazovkového pro zařízení s [Androidem Enterprise](device-restrictions-android-for-work.md#dedicated-device-settings) a [Windows 10](kiosk-settings.md) .
