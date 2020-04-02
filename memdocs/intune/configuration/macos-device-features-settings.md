---
title: nastavení funkcí zařízení macOS v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na nastavení pro konfiguraci zařízení macOS pro Protisk a přizpůsobení okna přihlášení k zobrazení nebo skrytí tlačítek napájení v Microsoft Intune. Podívejte se na postup, jak získat IP adresu, cestu a nastavení portu tiskového serveru v síti. Pomocí těchto nastavení můžete nakonfigurovat funkce zařízení macOS v profilu konfigurace zařízení.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/25/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker; annovich
ms.suite: ems
search.appverid: ''
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7c6c8b9d964355b1c08756fc2026a87e30bc7297
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/02/2020
ms.locfileid: "80551508"
---
# <a name="macos-device-feature-settings-in-intune"></a>nastavení funkcí zařízení macOS v Intune

Intune obsahuje vestavěná nastavení pro přizpůsobení funkcí na zařízeních macOS. Správci můžou například přidat tiskárny pro průchozí tisk, zvolit způsob, jakým se uživatelé přihlásí, konfigurovat řízení spotřeby, používat ověřování pomocí jednotného přihlašování a další.

Pomocí těchto funkcí můžete řídit zařízení macOS jako součást řešení správy mobilních zařízení (MDM).

Tento článek uvádí tato nastavení a popisuje, co jednotlivé nastavení dělá. V této části najdete taky postup pro získání IP adresy, cesty a portu pro tiskárny pro práci na tiskárně pomocí Terminálové aplikace (emulátor). Další informace o funkcích zařízení najdete v pro [Přidání nastavení funkcí zařízení s iOS/iPadOS nebo MacOS](device-features-configure.md).

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte profil konfigurace zařízení MacOS](device-features-configure.md).

> [!NOTE]
> Tato nastavení platí pro různé typy registrace s některými nastaveními, která platí pro všechny možnosti registrace. Další informace o různých typech registrace najdete v tématu [registrace MacOS](../enrollment/macos-enroll.md).

## <a name="airprint"></a>AirPrint

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Nastavení platí pro: registrace zařízení a automatický zápis zařízení

- **IP adresa**: zadejte adresu IPv4 nebo IPv6 tiskárny. Pokud k identifikaci tiskáren používáte názvy hostitelů, můžete získat IP adresu pomocí příkazového testu tiskárny v aplikaci Terminal. Další podrobnosti najdete v článku [získání IP adresy a cesty](#get-the-ip-address-and-path) (v tomto článku).
- **Cesta**: zadejte cestu k tiskárně. Cesta je obvykle `ipp/print` pro tiskárny v síti. Další podrobnosti najdete v článku [získání IP adresy a cesty](#get-the-ip-address-and-path) (v tomto článku).
- **Port** (iOS 11.0 +, iPadOS 13.0 +): zadejte port naslouchání cíle přenosu. Pokud necháte tuto vlastnost prázdnou, použije se při tisku výchozí port.
- **TLS** (iOS 11.0 +, iPadOS 13.0 +): Pokud chcete zabezpečit připojení přes tisk přes TLS (Transport Layer Security), vyberte **Povolit** .

- **Přidat** Server pro Protisk. Můžete přidat spoustu tiskových serverů.

Můžete taky **importovat** textový soubor s oddělovači (. csv), který obsahuje seznam tiskáren pro průchozí tisk. Po přidání tiskáren pro tisk do Intune můžete také **exportovat** tento seznam.

### <a name="get-the-ip-address-and-path"></a>Získat IP adresu a cestu

Chcete-li přidat servery s modulem pro tisk, budete potřebovat IP adresu tiskárny, cestu k prostředku a port. Následující kroky ukazují, jak tyto informace získat.

1. Na Macu, který je připojený ke stejné místní síti (podsíti) jako tiskárny pro Protisk, otevřete **terminál** (z **/aplikace/Utility**).
2. V aplikaci Terminal App zadejte `ippfind`a vyberte Enter.

    Poznamenejte si informace o tiskárně. Například může vracet něco podobného jako `ipp://myprinter.local.:631/ipp/port1`. První část je název tiskárny. Poslední část (`ipp/port1`) je cesta prostředku.

3. Do terminálu zadejte `ping myprinter.local`a vyberte Enter.

   Poznamenejte si IP adresu. Například může vracet něco podobného jako `PING myprinter.local (10.50.25.21)`.

4. Použijte hodnoty IP adresy a prostředku cesty. V tomto příkladu je `10.50.25.21`IP adresa a cesta k prostředku je `/ipp/port1`.

## <a name="login-items"></a>Přihlašovací položky

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **Soubory, složky a vlastní aplikace**: **přidejte** cestu k souboru, složce, vlastní aplikaci nebo systémové aplikaci, kterou chcete otevřít, když se uživatelé přihlásí ke svým zařízením. Systémové aplikace nebo aplikace sestavené nebo přizpůsobené pro vaši organizaci jsou obvykle ve složce `Applications` s cestou podobnou `/Applications/AppName.app`. 

  Můžete přidat mnoho souborů, složek a aplikací. Zadejte například:  
  
  - `/Applications/Calculator.app`
  - `/Applications`
  - `/Applications/Microsoft Office/root/Office16/winword.exe`
  - `/Users/UserName/music/itunes.app`
  
  Při přidávání libovolné aplikace, složky nebo souboru Nezapomeňte zadat správnou cestu. Ne všechny položky jsou ve složce `Applications`. Pokud uživatel přesune položku z jednoho umístění do jiného, pak se cesta změní. Tato přesunutá položka nebude otevřena, když se uživatel přihlásí.

- **Skrýt z konfigurace uživatele**: při **skrytí** se aplikace nezobrazuje v seznamu Uživatelé & skupiny přihlášení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení OS zobrazuje položku, kterou spustíte při přihlášení, v seznamu Uživatelé & skupiny přihlášení skupin s možností skrýt nezaškrtnuto.

  > [!NOTE]
  > Toto nastavení se zapojí všem zákazníkům za několik dalších týdnů.

## <a name="login-window"></a>Přihlašovací okno

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Nastavení platí pro: registrace zařízení a automatický zápis zařízení

#### <a name="window-layout"></a>Rozložení okna

- **Zobrazit další informace v řádku nabídek**: když je vybraná časová oblast na řádku **nabídek, možnost** Zobrazit zobrazí název hostitele a verzi MacOS. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí tyto informace na řádku nabídek zobrazit.
- **Banner**: zadejte zprávu, která se zobrazí na přihlašovací obrazovce na zařízeních. Zadejte například informace o vaší organizaci, uvítací zprávu, ztracené a zjištěné informace atd.
- **Vyberte formát přihlášení**: vyberte, jak se uživatelé přihlašují k zařízením. Možnosti:
  - **Vyzvat k zadání uživatelského jména a hesla** (výchozí): vyžaduje, aby uživatelé zadali uživatelské jméno a heslo.
  - **Seznam všech uživatelů, výzva k zadání hesla**: vyžaduje, aby uživatelé vybrali své uživatelské jméno ze seznamu uživatelů a pak zadali heslo. Také konfigurovat:

    - **Místní uživatelé**: **Skrýt** nezobrazuje místní uživatelské účty v seznamu uživatelů, které mohou zahrnovat účty Standard a admin. Zobrazují se jenom účty uživatelů sítě a systému. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém v seznamu uživatelů zobrazovat místní uživatelské účty.
    - **Mobilní účty**: **Skrýt** nezobrazuje mobilní účty v seznamu uživatelů. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazit mobilní účty v seznamu uživatelů. Některé mobilní účty se můžou zobrazovat jako síťoví uživatelé.
    - **Uživatelé sítě**: výběrem **Zobrazit zobrazíte** seznam uživatelů v síti v seznamu uživatelů. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí v seznamu uživatelů zobrazovat síťové uživatelské účty.
    - **Uživatelé s oprávněními**správce: **Skrýt** v seznamu uživatelů nezobrazují uživatelské účty správců. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazit uživatelské účty správce v seznamu uživatelů.
    - **Jiní uživatelé**: výběrem **Zobrazit** můžete v seznamu uživatelů vybrat **Další seznam.** Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí v seznamu uživatelů zobrazovat jiné uživatelské účty.

#### <a name="login-screen-power-settings"></a>Nastavení napájení přihlašovací obrazovky

- **Tlačítko vypnout**: **Skrýt** na přihlašovací obrazovce nezobrazuje tlačítko vypnout. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazit tlačítko vypnout.
- **Tlačítko restartovat**: **Skrýt** na přihlašovací obrazovce nezobrazuje tlačítko restartovat. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazit tlačítko restartovat.
- **Tlačítko režimu spánku**: **Skrýt** nezobrazuje na přihlašovací obrazovce tlačítko režimu spánku. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zobrazit tlačítko režimu spánku.

#### <a name="other"></a>Další

- **Zakázat přihlášení uživatele z konzoly**: **Disable zakáže** a skryje příkaz MacOS, který se používá pro přihlášení. V případě typických uživatelů toto nastavení **zakažte** . Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit, aby se přihlásili pomocí příkazového řádku macOS. Chcete-li přejít do režimu konzoly, uživatelé zadají `>console` do pole uživatelské jméno a musí se ověřit v okně konzoly.

#### <a name="apple-menu"></a>Nabídka Apple

Až se uživatelé přihlásí k zařízením, následující nastavení budou mít vliv na to, co můžou dělat.

- **Zakázat možnost vypnout**: **Zakázat** umožňuje uživatelům vybrat možnost **vypnutí** po přihlášení uživatele. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit, aby na zařízeních vybrali položku nabídky pro **vypnutí** .
- **Zakázat restart**: **Disable** znemožní uživatelům vybrat možnost **restartování** po přihlášení uživatele. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit vybrat položku nabídky **restartovat** na zařízeních.
- **Zakázat**vypnutí: **Zakázat** umožňuje uživatelům **vybrat možnost vypnutí** po přihlášení uživatele. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit vybrat položku nabídky **napájení** v zařízeních.
- **Zakázat možnost Odhlásit** se (MacOS 10,13 a novější): **Disable** znemožní uživatelům vybrat možnost **Odhlásit** se po přihlášení uživatele. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit vybrat položku nabídky **Odhlásit** se na zařízeních.
- **Zakázat zamykací obrazovku** (MacOS 10,13 a novější): možnost **Zakázat** znemožní uživatelům vybrat možnost **zamykací obrazovky** po přihlášení uživatele. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům dovolit vybrat položku nabídky **zamykací obrazovka** na zařízeních.

## <a name="single-sign-on-app-extension"></a>Rozšíření aplikace s jednotným přihlašováním

Tato funkce platí pro:

- macOS 10,15 a novější

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace 

- **Typ rozšíření aplikace jednotného přihlašování**: Vyberte typ rozšíření aplikace jednotného přihlašování. Možnosti:

  - **Nenakonfigurováno**: rozšíření aplikací se nepoužívají. Pokud chcete rozšíření aplikace zakázat, přepněte typ rozšíření aplikace jednotného přihlašování na **Nenakonfigurováno**.
  - **Přesměrování**: k použití jednotného přihlašování s moderními toky ověřování použijte obecné a přizpůsobitelné rozšíření aplikace pro přesměrování. Ujistěte se, že znáte rozšíření a ID týmu pro rozšíření aplikace vaší organizace.
  - **Přihlašovací údaje**: pomocí obecného rozšíření aplikace s přizpůsobitelnou přihlašovacími údaji můžete používat jednotné přihlašování s toky ověřování typu Challenge a Response. Ujistěte se, že znáte ID rozšíření a ID týmu pro rozšíření aplikace jednotného přihlašování ve vaší organizaci.  
  - **Kerberos**: použijte integrované rozšíření protokolu Kerberos společnosti Apple, které je součástí macOS Catalina 10,15 a novějších. Tato možnost je verze rozšíření **přihlašovacích údajů** specifická pro Kerberos.

  > [!TIP]
  > Pomocí typů **přesměrování** a **přihlašovacích údajů** přidáte vlastní hodnoty konfigurace, které budou předávány prostřednictvím rozšíření. Pokud používáte **přihlašovací údaje**, zvažte použití integrovaného nastavení konfigurace poskytovaného společností Apple v typu **Kerberos** .

- **ID rozšíření** (přesměrování a přihlašovací údaje): zadejte identifikátor sady prostředků, který identifikuje vaše rozšíření aplikace jednotného přihlašování, například `com.apple.ssoexample`.
- **ID týmu** (přesměrování a přihlašovací údaje): zadejte identifikátor týmu rozšíření aplikace jednotného přihlašování. Identifikátor týmu je alfanumerický řetězec (čísla a písmena), který vygenerovala společnost Apple, například `ABCDE12345`. 

  [Najděte své ID týmu](https://help.apple.com/developer-account/#/dev55c3c710c) (otevře se webová stránka společnosti Apple), kde najdete další informace.

- **Sféra** (přihlašovací údaje a Kerberos): zadejte název sféry ověřování. Název sféry by měl být velkými písmeny, například `CONTOSO.COM`. Název vaší sféry je typicky stejný jako název vaší domény DNS, ale jenom na velká písmena.

- **Domény** (přihlašovací údaje a Kerberos): zadejte doménu nebo názvy hostitelů pro weby, které se dají ověřit pomocí jednotného přihlašování. Pokud je váš web například `mysite.contoso.com`, `mysite` je název hostitele a `contoso.com` je název domény. Když se uživatelé připojí k některé z těchto webů, aplikace App Extension zpracuje výzvu ověřování. Toto ověřování umožňuje uživatelům k přihlášení použít ID obličeje, dotykové ID nebo Apple PINCODE/přístupový kód.

  - Všechny domény v profilech služby Intune, které mají rozšíření pro aplikace jednotného přihlašování, musí být jedinečné. Doménu nemůžete opakovat v žádném profilu rozšíření aplikace pro přihlášení, i když používáte různé typy rozšíření aplikace jednotného přihlašování.
  - U těchto domén se nerozlišují velká a malá písmena.

- **Adresy URL** (pouze přesměrované): zadejte PŘEDPONY adresy URL vašich zprostředkovatelů identity, na jejichž základě rozšíření pro přesměrování aplikace používá jednotné přihlašování. Když budou uživatelé přesměrováni na tyto adresy URL, rozšíření aplikace jednotného přihlašování se zasáhne a zobrazí výzvu k přihlášení SSO.

  - Všechny adresy URL v profilech rozšíření aplikace jednotného přihlašování Intune musí být jedinečné. Doménu nejde opakovat v žádném profilu rozšíření aplikace jednotného přihlašování, a to ani v případě, že používáte různé typy rozšíření aplikace jednotného přihlašování.
  - Adresy URL musí začínat na http://nebo https://.

- **Další konfigurace** (přesměrování a přihlašovací údaje): zadejte další data specifická pro rozšíření, která chcete předat rozšíření aplikace jednotného přihlašování:
  - **Klíč**: zadejte název položky, kterou chcete přidat, například `user name`.
  - **Typ**: zadejte typ dat. Možnosti:

    - Řetězec
    - Boolean: v **hodnotě konfigurace**zadejte `True` nebo `False`.
    - Integer: v **hodnotě konfigurace**zadejte číslo.
    
  - **Hodnota**: zadejte data.
  
  - **Přidat**: vyberte, pokud chcete přidat konfigurační klíče.

- **Použití řetězce klíčů** (jenom Kerberos): vyberte **blok** , aby se zabránilo ukládání a ukládání hesel do řetězce klíčů. Pokud je blokováno, uživatelé nebudou vyzváni k uložení hesla a po vypršení platnosti lístku protokolu Kerberos je nutné znovu zadat heslo. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém ukládat hesla a uložit je do řetězce klíčů. Uživatelům se po vypršení platnosti lístku nezobrazí výzva k zadání hesla.
- **ID obličeje, dotykové ID nebo heslo** (jenom Kerberos): **vyžaduje** , aby uživatelé při aktualizaci lístku Kerberos zadali své ID a dotykové jméno a heslo zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí vyžadovat, aby uživatelé pomocí biometrika nebo hesla zařízení aktualizovali lístek protokolu Kerberos. Pokud je **použití řetězce klíčů** blokované, pak toto nastavení neplatí.
- **Výchozí sféra** (pouze Kerberos): Chcete-li nastavit hodnotu **sféry** , kterou jste zadali jako výchozí sféru, vyberte možnost **Povolit** . Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí nastavit výchozí sféru.

  > [!TIP]
  > - Toto nastavení **Povolte** , pokud konfigurujete více rozšíření aplikace pro jednotné přihlašování pomocí protokolu Kerberos ve vaší organizaci.
  > - Toto nastavení **Povolte** , pokud používáte více sfér. Nastaví hodnotu **sféry** , kterou jste zadali jako výchozí sféru.
  > - Pokud máte pouze jednu sféru, ponechte ji **nenakonfigurovanou** (výchozí).

- **Automatická konfigurace** (jenom Kerberos): Pokud je nastavená na **blokovat**, nebude rozšíření protokolu Kerberos automaticky používat LDAP a DNS k určení jeho názvu lokality Active Directory. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém způsobit, že rozšíření automaticky nalezne název lokality služby Active Directory.
- **Změny hesla** (jenom Kerberos): **blok** znemožní uživatelům měnit hesla, která používají pro přihlášení k doménám, které jste zadali. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém způsobit změny hesla.  
- **Synchronizace hesel** (jenom Kerberos): Pokud chcete synchronizovat místní hesla uživatelů do Azure AD, vyberte **Povolit** . Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zakázat synchronizaci hesel do služby Azure AD. Toto nastavení použijte jako alternativu nebo zálohu k jednotnému přihlašování. Toto nastavení nefunguje, pokud jsou uživatelé přihlášení pomocí mobilního účtu Apple.
- **Složitost hesla služby Active Directory systému Windows Server** (pouze Kerberos): vyberte možnost **vyžadovat** , pokud chcete vynutit uživatelská hesla pro splnění požadavků na složitost hesla služby Active Directory. Další informace najdete v tématu [heslo musí splňovat požadavky na složitost](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements). Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí vyžadovat, aby uživatelé splnili požadavky na heslo služby Active Directory.
- **Minimální délka hesla** (jenom Kerberos): zadejte minimální počet znaků, které můžou vytvářet hesla uživatelů. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí pro uživatele vymáhat minimální délku hesla.
- **Omezení opakovaného použití hesla** (jenom Kerberos): zadejte počet nových hesel, od 1-24, které se musí použít, až bude možné znovu použít předchozí heslo v doméně. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí vynutilit omezení opakovaného použití hesla.
- **Minimální stáří hesla** (pouze Kerberos): zadejte počet dní, po které musí být heslo v doméně použito, než je může uživatel změnit. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení operační systém nemusí vyhovět minimálnímu stáří hesla, aby bylo možné je změnit.
- **Oznámení vypršení platnosti hesla** (jenom Kerberos): zadejte počet dní, než heslo vyprší, uživatelé obdrží oznámení o vypršení platnosti hesla. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém používat `15` dnů.
- **Vypršení platnosti hesla** (pouze Kerberos): zadejte počet dní, než bude nutné změnit heslo zařízení. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém nikdy vypršení platnosti hesel.
- **Adresa URL pro změnu hesla** (jenom Kerberos): zadejte adresu URL, která se otevře, když uživatelé spustí změnu hesla protokolu Kerberos.
- **Hlavní název** (jenom Kerberos): zadejte uživatelské jméno objektu zabezpečení protokolu Kerberos. Nemusíte zahrnovat název sféry. Například v `user@contoso.com``user` je hlavní název a `contoso.com` je název sféry.

  > [!TIP]
  > - Můžete také použít proměnné v hlavním názvu zadáním složených závorek `{{ }}`. Chcete-li například zobrazit uživatelské jméno, zadejte `Username: {{username}}`. 
  > - Buďte ale opatrní s náhradou proměnných, protože proměnné nejsou v uživatelském rozhraní ověřené a rozlišují velká a malá písmena. Nezapomeňte zadat správné informace.
  
- **Kód lokality služby Active Directory** (pouze Kerberos): zadejte název lokality služby Active Directory, kterou má rozšíření protokolu Kerberos použít. Tuto hodnotu pravděpodobně nebudete muset měnit, protože rozšíření protokolu Kerberos může automaticky najít kód lokality služby Active Directory.
- **Název mezipaměti** (jenom Kerberos): zadejte název obecné služby zabezpečení (GSS) mezipaměti protokolu Kerberos. Tuto hodnotu pravděpodobně nemusíte nastavovat.  
- **Zpráva požadavky na heslo** (jenom Kerberos): zadejte textovou verzi požadavků na heslo vaší organizace, které se zobrazují uživatelům. Zpráva se zobrazí, pokud nepožadujete požadavky na složitost hesla služby Active Directory nebo nezadáte minimální délku hesla.  
- **ID sady prostředků aplikace** (jenom Kerberos): **přidejte** identifikátory sady prostředků aplikace, které by měly na svých zařízeních používat jednotné přihlašování. Těmto aplikacím je udělen přístup k lístku pro udělení lístku protokolu Kerberos a ověřovacímu lístku. Aplikace také ověřují uživatele pro služby, kterým má oprávnění k přístupu.
- **Mapování sféry domény** (jenom Kerberos): **přidejte** přípony DNS domény, které by se měly namapovat do vaší sféry. Toto nastavení použijte, pokud názvy DNS hostitelů neodpovídají názvu sféry. Pravděpodobně nemusíte vytvářet vlastní mapování domén na sféru.
- **PKINIT certifikát** (jenom Kerberos): **Vyberte** certifikát kryptografie s veřejným klíčem pro počáteční ověřování (PKINIT), který se dá použít pro ověřování protokolem Kerberos. Můžete si vybrat z certifikátů [PKCS](../protect/certficates-pfx-configure.md) nebo [SCEP](../protect/certificates-scep-configure.md) , které jste přidali v Intune. Další informace o certifikátech najdete v tématu [použití certifikátů k ověřování v Microsoft Intune](../protect/certificates-configure.md).

## <a name="associated-domains"></a>Přidružené domény

V Intune můžete:

- Přidejte mnoho přidružení aplikace k doméně.
- Přidružte mnoho domén ke stejné aplikaci.

Tato funkce platí pro:

- macOS 10,15 a novější

### <a name="settings-apply-to-all-enrollment-types"></a>Nastavení platí pro: všechny typy registrace

- **ID aplikace**: zadejte identifikátor aplikace, který se má přidružit k webu. Identifikátor aplikace zahrnuje ID týmu a ID sady: `TeamID.BundleID`.

  ID týmu je alfanumerické znaky (písmena a čísla) vygenerované společností Apple pro vývojáře aplikací, například `ABCDE12345`. [Vyhledejte své ID týmu](https://help.apple.com/developer-account/#/dev55c3c710c) (otevře web společnosti Apple) obsahuje další informace.

  ID sady prostředků jednoznačně identifikuje aplikaci a obvykle je ve formátu zpětného zápisu názvů domén. Například ID sady Finder je `com.apple.finder`. Pokud chcete najít ID sady, použijte AppleScript v terminálu:

  `osascript -e 'id of app "ExampleApp"'`

- **Doména**: zadejte doménu webu, kterou chcete přidružit k aplikaci. Doména zahrnuje typ služby a plně kvalifikovaný název hostitele, například `webcredentials: www.contoso.com`.

  Všechny subdomény přidružené domény můžete vyhledat zadáním `*.` (zástupný znak hvězdička a tečka) před začátkem domény. Období je povinné. Přesné domény mají vyšší prioritu než u domén se zástupnými znaky. Modely z nadřazených domén se tedy shodují, *Pokud* se shoda nenajde v plně kvalifikované subdoméně.

  Typ služby může být:

  - **authsrv**: rozšíření aplikace s jednotným přihlašováním
  - **applink**: Universal Link
  - **webcredentials**: Automatické vyplňování hesel

- **Přidat**: vyberte, pokud chcete přidat své aplikace a přidružené domény.

> [!TIP]
> Pokud chcete řešit potíže, v zařízení macOS otevřete **Předvolby systému** > **profily**. Ověřte, že profil, který jste vytvořili, je v seznamu profily zařízení. Pokud je v seznamu uveden, ujistěte se, že je **Konfigurace přidružených domén** v profilu a obsahuje správné ID aplikace a domény.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).

Funkce zařízení můžete nakonfigurovat také v systému [iOS/iPadOS](ios-device-features-settings.md).
