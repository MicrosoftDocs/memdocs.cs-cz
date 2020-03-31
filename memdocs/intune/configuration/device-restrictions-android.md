---
title: Nastavení omezení zařízení s Androidem v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na seznam všech nastavení Správce zařízení s Androidem, která můžete řídit a omezit v Microsoft Intune. Tato nastavení můžete použít k ovládání hesla, přístupu ke Google Play, povolení nebo zakázání aplikací, ovládání nastavení prohlížeče, blokování aplikací, zálohování do cloudu Google, ovládání zpráv, hlasového volání, datového roamingu a možností připojení k Wi-Fi nebo prostřednictvím technologie Bluetooth.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: chmaguir, chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4afc27680c464f67756340ebcb0958887ae6f795
ms.sourcegitcommit: e2877d21dfd70c4029c247275fa2b38e76bd22b8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80407874"
---
# <a name="android-and-samsung-knox-standard-device-restriction-settings-lists-in-intune"></a>Seznamy nastavení omezení zařízení s Androidem a Samsung KNOX standard v Intune

Tento článek ukazuje všechna nastavení omezení zařízení v Microsoft Intune, která můžete nakonfigurovat pro zařízení s Androidem.

>[!TIP]
>Pokud požadovaná nastavení nejsou k dispozici, možná budete moct zařízení nakonfigurovat pomocí [vlastního profilu](custom-settings-android.md).

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte profil konfigurace zařízení](device-restrictions-configure.md).

## <a name="general"></a>Obecné

- **Kamera**: **Block** zabrání přístupu k fotoaparátu zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat přístup k kameře zařízení.

  Intune spravuje jenom přístup k kameře zařízení. Nemá přístup k obrázkům a videím.

- **Kopírování a vkládání (jenom Samsung KNOX)** : **blok** zabraňuje kopírování a vkládání. **Není nakonfigurováno** , umožňuje funkce kopírování a vkládání na zařízeních.
- **Sdílení schránky mezi aplikacemi (jenom Samsung KNOX)** : **blok** zabraňuje použití schránky ke kopírování a vkládání mezi aplikacemi. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém na zařízeních dovolit funkce kopírování a vkládání.
- **Odeslání diagnostických dat (jenom Samsung KNOX)** : **blokování** brání uživatelům v odesílání zpráv o chybách ze zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit data odeslat.
- **Vymazání (jenom Samsung KNOX)** : umožňuje uživatelům spouštět na zařízeních akci [vymazání](../remote-actions/devices-wipe.md) . Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.
- **Geografická poloha (jenom Samsung KNOX)** : **blokování** zakáže zařízením používat informace o poloze. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zařízení použít k používání informací o poloze.
- **Vypnutí (jenom Samsung KNOX)** : **blok** zabraňuje uživatelům v vypínání zařízení. Zabrání také tomu, aby byl **počet neúspěšných přihlášení, než** se nakonfiguruje nastavení zařízení a bude fungovat. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům způsobit vypnutí zařízení.
- **Snímek obrazovky (jenom Samsung KNOX)** : **blokování** zabraňuje snímekům obrazovky. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům umožnit zachytit obsah obrazovky v podobě obrázku.
- **Hlasový asistent (jenom Samsung KNOX)** : **blok** zakáže hlasovou službu S. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém používat hlasovou službu S a aplikaci na zařízeních. Toto nastavení se nevztahuje na Bixby nebo hlasového asistenta pro přístupnost, který čte obsah obrazovky nahlas.
- **YouTube (jenom Samsung KNOX)** : **blok** zabraňuje uživatelům v používání aplikace YouTube. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém použít aplikaci YouTube na zařízeních.
- **Sdílená zařízení (jenom Samsung KNOX)** : Nakonfigurujte spravované zařízení Samsung KNOX Standard jako sdílené. Při této možnosti je **možné** uživatelům přihlašovat se pomocí svých přihlašovacích údajů služby Azure AD ze zařízení. Zařízení zůstávají spravovaná bez ohledu na to, jestli se používají.

  Při použití v s profilem certifikátu SCEP umožňuje tato funkce uživatelům sdílet zařízení se stejnými aplikacemi pro všechny uživatele. Každý uživatel ale má vlastní certifikát uživatele SCEP. Po odhlášení uživatelů se všechna data aplikací vymažou. Tato funkce je omezená jenom na obchodní aplikace.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit více uživatelům v přihlašování k aplikaci Portál společnosti na zařízeních s použitím svých přihlašovacích údajů Azure AD.
- **Zablokovat změny data a času (Samsung KNOX)** : **blok** znemožní uživatelům měnit nastavení data a času na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit změnit nastavení data a času.

## <a name="password"></a>Heslo

- **Heslo**: **vyžaduje** , aby uživatelé zadali heslo pro přístup k zařízením. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit přístup k zařízením bez zadání hesla.

    > [!NOTE]
    > Při registraci MDM zařízení Samsung Knox automaticky vyžadují 4místný číselný kód PIN. Nativní zařízení s Androidem můžou automaticky vyžadovat PIN kód, aby mohl být kompatibilní s podmíněným přístupem.

- **Minimální délka hesla**: zadejte minimální počet požadovaných znaků od 4-16. Zadejte například `6` pro vyžadování alespoň šesti čísel nebo znaků v délce hesla.
- **Maximální počet minut nečinnosti, po kterém se zamkne obrazovka**: zadejte dobu, po kterou musí být zařízení nečinné, než se automaticky uzamkne obrazovka. Zadejte například `5` pro uzamčení zařízení po 5 minutách nečinnosti. Když je hodnota prázdná nebo nastavená na **nenakonfigurovaná**, Intune se nezmění ani neaktualizuje.

  V zařízení uživatelé nemůžou nastavit časovou hodnotu větší než nakonfigurovanou dobu v profilu. Uživatelé můžou nastavit nižší časovou hodnotu. Pokud je například profil nastavený na `15` minut, můžou uživatelé nastavit hodnotu na 5 minut. Uživatelé nemůžou hodnotu nastavit na 30 minut.

- **Počet neúspěšných přihlášení před vymazáním zařízení**: zadejte počet chybných hesel povolených před vymazáním zařízení, od 4-11. `0` (nula) může zakázat funkci vymazání zařízení. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje.
- **Vypršení platnosti hesla (dny)** : zadejte počet dní, než bude nutné změnit heslo zařízení, od 1-365. Zadejte například `90` vypršení platnosti hesla po 90 dnech. Po vypršení platnosti hesla se uživatelům zobrazí výzva k vytvoření nového hesla. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje.
- **Vyžadovaný typ hesla**: zadejte požadovanou úroveň složitosti hesla a to, jestli se můžou používat biometrická zařízení. Možnosti:
  - **Výchozí ze zařízení**
  - **Biometrika s nízkou úrovní zabezpečení**: [silný vs. slabý biometrika](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (otevře web v Androidu)
  - **Aspoň číslice**: obsahuje číselné znaky, například `123456789`.
  - **Číselná složitá**: opakující se nebo po sobě jdoucí čísla, například "1111" nebo "1234", nejsou povolena. Před přiřazením tohoto nastavení k zařízením nezapomeňte aktualizovat aplikaci Portál společnosti na nejnovější verzi na těchto zařízeních.

    Když nastavíte **číselnou složitost**a přiřadíte nastavení k zařízením s verzí Androidu starší než 5,0, platí následující chování:

    - Pokud Portál společnosti aplikace používá verzi starší než 1704, na zařízení se nevztahují žádné zásady pro PIN a v centru pro správu Microsoft Endpoint Manageru se zobrazí chyba.
    - Pokud aplikace Portál společnosti používá verzi 1704 nebo novější, je možné použít jenom jednoduchý PIN kód. Verze Androidu starší než 5,0 Toto nastavení nepodporuje. V centru pro správu Microsoft Endpoint Manageru se nezobrazí žádná chyba.

  - **Aspoň abecední**znaky: obsahuje písmena v abecedě. Čísla a symboly nejsou požadovány.
  - **Aspoň alfanumerické**znaky: obsahuje velká písmena, malá písmena a číslice.
  - **Aspoň alfanumerické se symboly**: obsahuje velká písmena, malá písmena, číslice, interpunkční znaménka a symboly.

- **Zakázat opakované použití předchozích hesel**: pomocí tohoto nastavení můžete uživatelům zabránit ve vytváření hesel, která používali dřív. Zadejte počet dříve použitých hesel, která se nedají použít, od 1-24. Zadejte například `5`, takže uživatelé nemůžou nastavit nové heslo nebo některá z předchozích čtyř hesel. Pokud je hodnota prázdná, Intune se nezmění ani neaktualizuje.
- **Odemknutí otiskem prstu (jenom Samsung KNOX)** : **blok** zabraňuje použití otisku prstu k odemknutí zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit, aby zařízení odemkli pomocí otisku prstu.
- **Smart Lock a jiní agenti**pro určování důvěryhodnosti: **blok** brání Smart Lock nebo jiným agentům pro určování důvěryhodnosti v nastavení zamykací obrazovky. Pokud je zařízení v důvěryhodném umístění, pak tato funkce, označovaná také jako agent pro určování důvěryhodnosti, umožňuje zakázat nebo obejít heslo zamykací obrazovky zařízení. Tuto funkci můžete například použít, když jsou zařízení připojená k určitému zařízení Bluetooth nebo když jsou zařízení blízko značky NFC. Pomocí tohoto nastavení můžete uživatelům zabránit v konfiguraci funkce Smart Lock.

  Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení.

  Toto nastavení platí pro:

  - Samsung KNOX standard 5.0 +

- **Šifrování**: vyberte **vyžadovat** , aby byly soubory v zařízení šifrované. Ne všechna zařízení podporují šifrování. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Pokud chcete nakonfigurovat toto nastavení a správně ohlásit dodržování předpisů, nakonfigurujte taky:
  1. **Heslo**: nastavte na **vyžadovat**.
  2. **Požadovaný typ hesla**: nastavte **aspoň na číslo**.
  3. **Minimální délka hesla**: nastavte aspoň `4`.

  > [!NOTE]
  > Pokud se vynucují zásady šifrování, zařízení Samsung Knox po uživatelích vyžadují nastavení šestiznakového složitého hesla jako hesla k zařízení.

## <a name="google-play-store"></a>Obchod Google Play

- **Google Play Store (jenom Samsung KNOX)** : **blok** zabraňuje uživatelům v používání úložiště Google Play. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit přístup k Google Play Storu na zařízeních.

## <a name="restricted-apps"></a>Omezené aplikace

Pomocí těchto nastavení můžete na zařízeních zapnout nebo zakázat konkrétní aplikace. Tato funkce je podporovaná v zařízeních s Androidem a Samsung KNOX Standard.

- **Nenakonfigurováno** (výchozí): Intune toto nastavení nemění ani neaktualizuje.
- **Zakázané aplikace**: seznam aplikací (nespravovaných pomocí Intune), které uživatelé nemůžou instalovat a spouštět. Pokud uživatel z tohoto seznamu nainstaluje aplikaci, budete Intune informovat.
- **Schválené aplikace**: seznam aplikací, které můžou uživatelé instalovat. Aby bylo možné zachovat dodržování předpisů, uživatelé nesmí instalovat jiné aplikace.  Aplikace spravované přes Intune se automaticky povolují, včetně aplikace Portál společnosti.
- **Seznam aplikací**: **Přidat** aplikaci:
  - **ID sady prostředků aplikace**: Zadejte ID sady prostředků aplikace.
  - **Adresa URL obchodu s aplikacemi**: zadejte adresu URL obchod Google Play aplikace, kterou chcete. Pokud například chcete přidat aplikaci Vzdálená plocha Microsoft pro Android, zadejte `https://play.google.com/store/apps/details?id=com.microsoft.rdc.android`.

    Pokud chcete najít adresu URL aplikace, otevřete [Google Play Store](https://play.google.com/store/apps)a vyhledejte aplikaci. Vyhledejte například `Microsoft Remote Desktop Play Store` nebo `Microsoft Planner`. Vyberte aplikaci a zkopírujte adresu URL.
  
  - **Název aplikace**: zadejte název, který chcete. Tento název se zobrazí uživatelům.
  - **Vydavatel** (volitelné): zadejte vydavatele aplikace, například `Microsoft`.

Můžete také **naimportovat** soubor CSV s podrobnostmi o aplikaci, včetně adresy URL. Použijte*adresu URL aplikace*< >, <*název aplikace*> < formát*vydavatele aplikace*>. Případně **exportujte** existující seznam obsahující seznam aplikací s omezeným přístupem ve stejném formátu.

> [!IMPORTANT]
> Profily zařízení, které používají nastavení aplikací s omezeným přístupem, se musí přiřadit ke skupinám uživatelů, nikoli ke skupinám zařízení.

## <a name="browser"></a>Prohlížeč

- **Webový prohlížeč (jenom Samsung KNOX)** : **blokování** zabraňuje použití výchozího webového prohlížeče na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém používat výchozí webový prohlížeč zařízení.
- Automatické **vyplňování (jenom Samsung KNOX)** : **blok** znemožní automatickému vyplňování textu v prohlížeči. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat automatické vyplňování.
- **Soubory cookie (jenom Samsung KNOX)** : vyberte, jak se mají zpracovávat soubory cookie z webů na zařízeních. Možnosti:
  - Povolit
  - Blokovat všechny soubory cookie
  - Povolení souborů cookie z navštívených webů
  - Povoluje soubory cookie z aktuálního webu
- **JavaScript (jenom Samsung KNOX)** : **blok** zabraňuje spuštění JavaScriptu v prohlížeči. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém tyto skripty dovolit.
- **Automaticky otevíraná okna (jenom Samsung KNOX)** : **blok** zapne blokování automaticky otevíraných oken, aby se zabránilo automaticky otevíraná okna ve webovém prohlížeči. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat automaticky otevíraná okna.

## <a name="allow-or-block-apps"></a>Povolení nebo blokování aplikací

Pomocí těchto nastavení můžete na zařízeních se Samsung KNOX standardem zapnout, blokovat nebo skrýt konkrétní aplikace. Skryté aplikace nemohou být otevřeny nebo spuštěny uživateli.

Možnosti:

- **Aplikace, které je možné nainstalovat (jenom Samsung KNOX Standard)** : Přidejte aplikace, které můžou uživatelé instalovat. Uživatelé nemůžou instalovat aplikace, které nejsou v seznamu.
- **Blokované aplikace od spuštění (jenom Samsung KNOX Standard)** : zadejte aplikace, které uživatelé nemůžou na svém zařízení spustit.
- **Aplikace skryté od uživatele (jenom Samsung KNOX Standard)** : zadejte aplikace, které jsou na zařízeních skryté. Uživatelé nemůžou tyto aplikace vyhledat ani spustit.

Pro každé nastavení přidejte své aplikace:

- **Přidat aplikace podle názvu balíčku**: zadejte název aplikace a název balíčku aplikace. Primárně se používá pro obchodní aplikace. 
- **Přidat aplikace podle adresy URL**: zadejte název aplikace a její adresu url do Google Play Storu.
- **Přidat aplikaci pro Store**: vyberte aplikaci ze stávajícího seznamu aplikací, které spravujete v Intune.

## <a name="cloud-and-storage"></a>Cloud a úložiště

- **Záloha Google (jenom Samsung KNOX)** : **blokovat** brání tomu, aby se zařízení synchronizoval se zálohováním na Google. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém používat zálohování Google.
- **Automatická synchronizace účtu Google (jenom Samsung KNOX)** : **blok** zabraňuje funkci automatické synchronizace účtu Google na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat automatickou synchronizaci nastavení účtu Google.
- **Vyměnitelné úložiště (jenom Samsung KNOX)** : **blokovat** zabrání zařízením používat Vyměnitelné úložiště. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zařízení umožňovat použití vyměnitelného úložiště, jako je třeba karta SD.
- **Šifrování na paměťových kartách (jenom Samsung KNOX)** : **vyžaduje** vynutit, aby se paměťové karty musely šifrovat. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat použití nešifrovaných paměťových karet. Ne všechna zařízení podporují šifrování paměťové karty. Pokud ho chcete ověřit, obraťte se na výrobce zařízení.

## <a name="cellular-and-connectivity"></a>Mobilní síť a připojení

- **Datový roaming (jenom Samsung KNOX)** : **blokovat** zabrání datovým roamingu v mobilní síti. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat datový roaming.
- **Zasílání zpráv SMS a MMS (jenom Samsung KNOX)** : **blokování** brání textovému zasílání zpráv na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat použití SMS a MMS zpráv.
- **Hlasové vytáčení (jenom Samsung KNOX)** : **blok** zabraňuje uživatelům používat funkci hlasového vytáčení na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat hlasové vytáčení.
- **Hlasový roaming (jenom Samsung KNOX)** : **blok** zabraňuje hlasovému roamingu přes mobilní síť. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat hlasový roaming.
- **Bluetooth (jenom Samsung KNOX)** : **blok** zabraňuje použití Bluetooth na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat použití Bluetooth.
- **NFC (jenom Samsung KNOX)** : **blok** zakáže operace, které na zařízeních, které ji podporují, používají technologii NFC (bezkontaktní komunikace). Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat operace NFC.
- **Wi-Fi (jenom Samsung KNOX)** : **blok** zabraňuje použití Wi-Fi na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat použití Wi-Fi.
- **Sdílení internetového připojení přes Wi-Fi (jenom Samsung KNOX)** : **blok** zabraňuje použití internetového připojení Wi-Fi na zařízeních. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém umožňovat použití internetového připojení přes Wi-Fi.

## <a name="kiosk"></a>Kiosk

Nastavení platí jen pro zařízení se zabezpečením Samsung Knox Standard a jen pro aplikace, které spravujete přes Intune.

- Přidejte aplikace, které chcete spustit, když je zařízení v celoobrazovkovém režimu. V celoobrazovkovém režimu se spustí jenom aplikace, které přidáte. Nepřidání aplikací neběží. Předem nainstalované prohlížeče se nespouštějí jako aplikace, když je zařízení v celoobrazovkovém režimu. Pokud se vyžaduje prohlížeč, zvažte použití řešení [Managed Browser](../apps/app-configuration-managed-browser.md).

  Možnosti vaší aplikace:

  - **Přidat aplikace podle názvu balíčku**: primárně se používá pro obchodní aplikace. Zadejte název aplikace a název balíčku aplikace.
  - **Přidat aplikace podle adresy URL**: zadejte název aplikace a její adresu url do Google Play Storu.
  - **Přidat aplikaci pro Store**: vyberte aplikaci ze stávajícího seznamu aplikací, které spravujete v Intune.

- **Tlačítko režimu spánku obrazovky**: **blok** zabraňuje nebo skrývá tlačítko režimu spánku obrazovky. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém na zařízeních zapnout tlačítko probuzení z režimu spánku obrazovky.
- **Tlačítka hlasitosti**: **blok** zabraňuje uživatelům v úpravách svazku tím, že zakáže tlačítka hlasitosti. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém použít na zařízeních tlačítka hlasitosti.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).

Můžete také vytvořit profily celoobrazovkového pro zařízení s [Androidem Enterprise](device-restrictions-android-for-work.md#dedicated-devices) a [Windows 10](kiosk-settings.md) .
