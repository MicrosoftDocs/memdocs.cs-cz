---
title: Nastavení zásad šifrování disků v Intune Endpoint Security | Microsoft Docs
description: Nastavení zásad šifrování disku Endpoint Security pro BitLocker a trezor úložiště v Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: db23ee1742934e8545c03c529d6a05c13cc59f1a
ms.sourcegitcommit: 6ca5e75ed7a6fd2186fbe51c177960004d5ec81f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/19/2020
ms.locfileid: "83633290"
---
# <a name="disk-encryption-policy-settings-for-endpoint-security-in-intune"></a>Nastavení zásad šifrování disku pro zabezpečení koncového bodu v Intune

Podívejte se na nastavení, která můžete nakonfigurovat v části profily pro zásady *šifrování disku* v uzlu Security Endpoint v Intune jako součást [zásad zabezpečení koncového bodu](../protect/endpoint-security-policy.md).

Podporované platformy a profily:

- **MacOS**:
  - Profil: **trezor**
- **Windows 10 a novější**:
  - Profil: **BitLocker**

## <a name="filevault"></a>FileVault

### <a name="encryption"></a>Šifrování

**Povolit trezor úložiště**  
- **Nenakonfigurováno** (*výchozí*)
- **Ano** – povolí šifrování celého disku s použitím XTS-AES 128 with trezoru na zařízeních, na kterých běží MacOS 10,13 a novější. Trezor úložiště je povolený, když se uživatel odhlásí od zařízení.

  Pokud nastavíte *Ano*, můžete nakonfigurovat další nastavení trezoru.

  - Typ obnovovacího **klíče** 
     Pro zařízení se vytvoří klíče pro obnovení *osobních klíčů* . Pro osobní klíč nakonfigurujte následující nastavení:

    - **Střídání osobních obnovovacích klíčů**  
      Určete, jak často se má otočit osobní obnovovací klíč pro zařízení. Můžete vybrat výchozí nastavení **není nakonfigurováno**nebo hodnota **1** až **12** měsíců.
    - **Popis umístění v úschově pro osobní obnovovací klíč**  
      Zadejte krátkou zprávu pro uživatele, která vysvětluje, jak mohou načíst svůj osobní obnovovací klíč. Uživatel uvidí tuto zprávu na přihlašovací obrazovce, když se zobrazí výzva k zadání osobního obnovovacího klíče, pokud je zapomenuté heslo.

  - **Počet povolených pokusů o obejití**  
    Nastaví počet pokusů, které uživatel může ignorovat výzvy k povolení trezoru úložišť, aby se uživatel mohl přihlásit.
    - **Nenakonfigurováno** (*výchozí*) – před povolením dalšího přihlášení je vyžadováno šifrování zařízení.
    - **1** až **10** – povolí uživateli ignorovat výzvu od 1 do 10 před tím, než se v zařízení vyžaduje šifrování.
    - **Bez omezení, vždy** se zobrazí výzva – uživatel bude vyzván k povolení trezoru úložišť, ale šifrování není nikdy vyžadováno.

  - **Povolí odložení, dokud se odhlásí.**  
    - **Nenakonfigurováno** (*výchozí*)
    - **Ano** – odložit výzvu a povolit trezor úložiště, dokud se uživatel odhlásí.  

  - **Zakázat výzvu při odhlášení**  
    Zabrání uživateli zobrazit výzvu, aby povolila trezor úložiště při odhlášení. Pokud je nastavení zakázat, výzva při odhlášení je zakázaná a místo toho se uživateli zobrazí výzva, když se přihlásí.
    - **Nenakonfigurováno** (*výchozí*)
    - **Ano** – zakáže výzvu k povolení trezoru úložišť, který se zobrazí při odhlášení.

## <a name="bitlocker"></a>BitLocker

### <a name="bitlocker--base-settings"></a>BitLocker – základní nastavení

- **Povolení úplného šifrování disku pro operační systém a pevné datové jednotky**  
  CSP: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  Pokud byla jednotka zašifrovaná předtím, než se tato zásada použila, neprovádí se žádná další akce. Pokud metoda šifrování a možnosti odpovídají této zásadě, měla by konfigurace vrátit úspěch. Pokud možnost místní konfigurace BitLockeru neodpovídá těmto zásadám, konfigurace nejspíš vrátí chybu.
  
  Pokud chcete tuto zásadu použít na disk, který je už zašifrovaný, dešifrujte jednotku a znovu použijte zásady MDM. Výchozí nastavení systému Windows není vyžadovat nástroj BitLocker Drive Encryption. V případě služby Azure AD JOIN a registrace účtu Microsoft (MSA) nebo automatického šifrování přihlašovacích údajů se ale může povolit BitLocker na platformě XTS-AES 128-bit Encryption.

  - **Nenakonfigurováno** (*výchozí*) – neprovede se žádné vynucení nástroje BitLocker.
  - **Ano** – vynutilo používání BitLockeru.

- **Vyžadovat šifrování paměťových karet (jenom mobilní zařízení)**  
  CSP: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  Toto nastavení platí pouze pro zařízení se systémem Windows Mobile a Mobile Enterprise SKU.
  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí k výchozímu operačnímu systému, což nepožaduje šifrování paměťové karty.
  - **Ano** – šifrování na paměťových kartách se vyžaduje pro mobilní zařízení.

- **Skrýt výzvu k šifrování třetích stran**  
  CSP: [AllowWarningForOtherDiskEncryption](https://go.microsoft.com/fwlink/?linkid=872525)

  Pokud je BitLocker zapnutý v systému, který už je zašifrovaný pomocí šifrovacího produktu jiného výrobce, může zařízení vykreslit nepoužitelné. Může dojít ke ztrátě dat a možná budete muset přeinstalovat Windows. Důrazně doporučujeme nikdy nepovolit nástroj BitLocker na zařízení, které má nainstalované nebo povolené šifrování třetích stran.

  Ve výchozím nastavení vyzve Průvodce nastavením BitLockeru uživatele k potvrzení, že není zavedeno žádné šifrování třetí strany.

  - **Nenakonfigurováno** (*výchozí*) – Průvodce nastavením BitLockeru zobrazuje upozornění a vyzývá uživatele k potvrzení, že není k dispozici šifrování třetí strany.
  - **Ano** – skryje výzvu Průvodce nastavením BitLockeru od uživatelů.

  Pokud jsou požadovány funkce tichého povolení BitLockeru, musí být upozornění na šifrování třetí strany skryté, protože všechny povinné pracovní postupy pro tiché povolování jsou přerušeny.

  Když nastavíte *Ano*, můžete nakonfigurovat následující nastavení:

  - **Povolit standardním uživatelům povolit šifrování při autopilotu**  
    CSP: [AllowStandardUserEncryption](https://go.microsoft.com/fwlink/?linkid=2114200)
    - **Nenakonfigurováno** (*výchozí*) – během scénářů tichého povolování Azure Active Directory Join (AADJ), uživatelé nemusejí být místními správci, aby mohli BitLocker povolit.
    - **Ano** – nastavení je ponecháno jako výchozí nastavení klienta, což má za účelem povolení nástroje BitLocker vyžadovat přístup místního správce.

    Pro scénáře netichého povolení a autopilotu musí být uživatel místním správcem, aby dokončil Průvodce nastavením BitLockeru.

- **Povolit heslo pro obnovení na základě klienta pro**  
  CSP: [ConfigureRecoveryPasswordRotation](https://go.microsoft.com/fwlink/?linkid=2114201)

  Přidat pracovní účet (AWA, napravo na pracovišti pracoviště) nejsou podporovaná pro rotaci klíčů.
  - **Nenakonfigurováno** (*výchozí*) – klient nebude otáčet klíče pro obnovení nástroje BitLocker.
  - **Disabled** (Zakázáno)
  - **Zařízení připojená k Azure AD**
  - **Zařízení Azure AD a Hybrid-JOINED**

### <a name="bitlocker---fixed-drive-settings"></a>BitLocker – nastavení pevné jednotky

- **Zásady pevné jednotky BitLockeru**  
  [Nastavení Zásady skupiny BitLockeru](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Obnovení pevného disku**  
    CSP: [FixedDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872538)

    Určuje, jakým způsobem se v případě absence požadovaných informací o spouštěcím klíči obnovují pevné datové jednotky chráněné BitLockerem.

    - **Nenakonfigurováno** (*výchozí*) – podporují se výchozí možnosti obnovení včetně agenta obnovování dat (DRA). Koncový uživatel může zadat možnosti obnovení a informace o obnovení nejsou zálohovány do Azure Active Directory.
    - **Konfigurace** – povolí přístup ke konfiguraci různých technik obnovení jednotky.

    Když je nastavena *Konfigurace* , jsou k dispozici následující nastavení:

    - **Vytvoření obnovovacího klíče uživatelem**  
      - **Blokováno** (*výchozí*)
      - **Požadováno**
      - **Povoleno**

    - **Konfigurace balíčku pro obnovení BitLockeru**
      - **Heslo a klíč** (*výchozí*) – zahrňte heslo pro obnovení nástroje BitLocker, které používají správci a uživatelé k odemknutí chráněných jednotek, a balíčky obnovovacích klíčů, které správci používají pro účely obnovování dat, ve službě Active Directory.
      - **Pouze heslo** – balíčky obnovovacího klíče nemusí být v případě potřeby k dispozici.

    - **Vyžadovat, aby zařízení zálohovali informace pro obnovení do Azure AD**
      - **Nenakonfigurováno** (*výchozí*) – povolení BitLockeru se dokončí i v případě, že se zálohování klíčů obnovení do Azure AD nezdaří. Výsledkem může být, že se neukládají žádné informace pro obnovení externě.
      - **Ano** – BitLocker nebude dokončit povolení, dokud se klíče pro obnovení úspěšně neuložily do Azure Active Directory.

    - **Vytváření hesla pro obnovení uživatelem**  
      - **Blokováno** (*výchozí*)
      - **Požadováno**
      - **Povoleno**

    - **Skrýt možnosti obnovení při instalaci nástroje BitLocker**
      - **Nenakonfigurováno** (*výchozí*) – povolí uživateli přístup k dodatečné možnosti obnovení.
      - **Ano** – zablokuje koncovému uživateli možnost výběru dalších možností obnovení, jako je například tisk obnovovacích klíčů během Průvodce nastavením BitLockeru.

    - **Po uložení informací o obnovení povolit nástroj BitLocker**
      - **Nenakonfigurováno** (*výchozí*)  
      - **Ano**

    - **Blokovat použití agenta obnovení dat založeného na certifikátech (DRA)**
      - **Nenakonfigurováno** (*výchozí*) – povolí nastavení použití agenta DRA. Pro nasazení agenta DRA a certifikátů je potřeba, abyste nastavili DRA a Zásady skupiny objekty podnikové infrastruktury veřejných klíčů (PKI).
      - **Ano** – zablokuje možnost použití agenta obnovování dat (DRA) k obnovení jednotek s povoleným bitlockerem.

  - **Blokovat přístup pro zápis na pevné datové jednotky, které nechrání BitLocker**  
    CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    Toto nastavení je k dispozici, když je *zásada pevná jednotka nástroje BitLocker* nastavená na hodnotu *Konfigurovat*.

    - **Nenakonfigurováno** (*výchozí*) – data je možné zapsat na nešifrované pevné jednotky.
    - **Ano** – Windows neumožní zapsat žádná data na pevné jednotky, které nejsou chráněné bitlockerem. Pokud není pevná jednotka zašifrovaná, uživatel bude muset před udělením přístupu pro zápis dokončit průvodce nastavením BitLockeru jednotky.

  - **Konfigurace metody šifrování pro pevné datové jednotky**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  

    Nakonfigurujte metodu šifrování a sílu šifrování pro disky s pevnými datovými jednotkami. *XTS-AES 128-bit* je výchozí metodou šifrování Windows a doporučenou hodnotou.

    - **Nenakonfigurováno** (*výchozí*)
    - **128bit CBC AES**
    - **256bit CBC AES**
    - **128bit XTS AES**
    - **256bit XTS AES**

### <a name="bitlocker---os-drive-settings"></a>BitLocker – nastavení jednotky s operačním systémem

- **Zásada systémové jednotky BitLockeru**  
  CSP: [nastavení zásady skupiny BitLockeru](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **Konfigurace** (*výchozí*)  
  - **Není nakonfigurováno**

  Při nastavení *Konfigurace* můžete nakonfigurovat následující nastavení:

  - **Vyžadováno ověřování po spuštění**  
    CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

    - **Nenakonfigurováno** (*výchozí*)
    - **Ano** – nakonfigurujte dodatečné požadavky na ověření při spuštění systému, včetně použití čipu TPM (Trusted Platform Module) nebo spouštěcího kódu PIN.

    Když nastavíte *Ano* , můžete nakonfigurovat následující nastavení:

    - **Kompatibilní spuštění čipu TPM**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      Doporučuje se pro BitLocker vyžadovat čip TPM. Toto nastavení platí jenom v případě, že nástroj BitLocker už není povolený, ale nemá žádný vliv.

      - **Blokované** (*výchozí*) – BitLocker nepoužívá čip TPM.
      - **Požadovaná** možnost – BitLocker umožňuje jenom v případě, že je čip TPM přítomen a je použitelný.
      - **Povoleno** – BitLocker používá čip TPM, pokud je přítomný.

    - **Kompatibilní spouštěcí PIN kód TPM**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Blokované** (*výchozí*) – zablokuje použití PIN kódu.
      - **Požadováno** – vyžaduje, aby byl k dispozici kód PIN a čip TPM pro zapnutí nástroje BitLocker.
      - **Povoleno** – BitLocker používá čip TPM, pokud je přítomen, a umožňuje, aby byl spouštěcí PIN kód nakonfigurován uživatelem.

      U scénářů s tichým povolením musíte nastavit možnost *zablokovat*. Pokud je potřeba zásah uživatele, neproběhne v tichém režimu povolení (včetně autopilotu) úspěšné.

    - **Kompatibilní spouštěcí klíč TPM**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Blokované** (*výchozí*) – zablokuje použití spouštěcích klíčů.
      - **Požadováno** – vyžaduje, aby byl přítomen spouštěcí klíč a čip TPM, aby bylo možné zapnout nástroj BitLocker.
      - **Povoleno** – BitLocker používá čip TPM, pokud je přítomen, a povoluje spouštěcí klíč (například jednotku USB) k odemknutí jednotek.

      U scénářů s tichým povolením musíte nastavit možnost *zablokovat*. Pokud je potřeba zásah uživatele, neproběhne v tichém režimu povolení (včetně autopilotu) úspěšné.

    - **Kompatibilní spouštěcí klíč a PIN kód TPM**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Blokované** (*výchozí*) – zablokuje použití spouštěcího klíče a kombinace kódů PIN.
      - **Požadováno** – vyžaduje, aby nástroj BitLocker měl spouštěcí klíč a kód PIN, který má být povolen.
      - **Povoleno** – BitLocker používá čip TPM, pokud je přítomný a umožňuje spouštěcí klíč a kombinaci kódů PIN.

      U scénářů s tichým povolením musíte nastavit možnost *zablokovat*. Pokud je potřeba zásah uživatele, neproběhne v tichém režimu povolení (včetně autopilotu) úspěšné.

    - **Zakázat BitLocker na zařízeních, kde TPM není kompatibilní**  
    CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      Pokud není přítomen žádný čip TPM, nástroj BitLocker vyžaduje pro spuštění heslo nebo jednotku USB.

      Toto nastavení platí jenom v případě, že nástroj BitLocker už není povolený, ale nemá žádný vliv.

      - **Nenakonfigurováno** (*výchozí*)
      - **Ano** – zablokuje konfiguraci BitLockeru bez kompatibilního čipu TPM.

    - **Povolit zprávu o obnovení a adresu URL před spuštěním**  
      CSP: konfigurace [SystemDrivesRecoveryMessage](https://go.microsoft.com/fwlink/?linkid=872530)

      - **Nenakonfigurováno** (*výchozí*) – použijte výchozí informace o obnovení před spuštěním nástroje BitLocker.
      - **Ano** – povolí konfiguraci vlastní zprávy pro obnovení před spuštěním a adresu URL, která uživatelům pomůže pochopit, jak najít heslo pro obnovení. Zpráva a adresa URL před spuštěním se uživatelům uvidí, když jsou zamčené z počítače v režimu obnovení.

      Když nastavíte *Ano* , můžete nakonfigurovat následující nastavení:

      - **Zpráva o obnovení před spuštěním**  
        Zadejte vlastní zprávu o obnovení před spuštěním.

      - **Adresa URL pro obnovení před spuštěním**  
        Zadejte vlastní adresu URL pro obnovení před spuštěním.

    - **Obnovení systémové jednotky**  
      CSP: [SystemDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872529)

      - **Nenakonfigurováno** (*výchozí*)  
      - **Konfigurovat** – povolí konfiguraci dalších nastavení.

      Když je nastavena *Konfigurace* , jsou k dispozici následující nastavení:

      - **Vytvoření obnovovacího klíče uživatelem**  
        - **Blokováno** (*výchozí*)
        - **Požadováno**
        - **Povoleno**

      - **Konfigurace balíčku pro obnovení BitLockeru**
        - **Heslo a klíč** (*výchozí*) – zahrňte heslo pro obnovení nástroje BitLocker, které používají správci a uživatelé k odemknutí chráněných jednotek, a balíčky obnovovacích klíčů, které správci používají pro účely obnovování dat, ve službě Active Directory.
        - **Pouze heslo** – balíčky obnovovacího klíče nemusí být v případě potřeby k dispozici.

      - **Vyžadovat, aby zařízení zálohovali informace pro obnovení do Azure AD**
        - **Nenakonfigurováno** (*výchozí*) – povolení BitLockeru se dokončí i v případě, že se zálohování klíčů obnovení do Azure AD nezdaří. Výsledkem může být, že se neukládají žádné informace pro obnovení externě.
        - **Ano** – BitLocker nebude dokončit povolení, dokud se klíče pro obnovení úspěšně neuložily do Azure Active Directory.

      - **Vytváření hesla pro obnovení uživatelem**  
        - **Blokováno** (*výchozí*)
        - **Požadováno**
        - **Povoleno**

      - **Skrýt možnosti obnovení při instalaci nástroje BitLocker**
        - **Nenakonfigurováno** (*výchozí*) – povolí uživateli přístup k dodatečné možnosti obnovení.
        - **Ano** – zablokuje koncovému uživateli možnost výběru dalších možností obnovení, jako je například tisk obnovovacích klíčů během Průvodce nastavením BitLockeru.

      - **Po uložení informací o obnovení povolit nástroj BitLocker**
        - **Nenakonfigurováno** (*výchozí*)  
        - **Ano**

      - **Blokovat použití agenta obnovení dat založeného na certifikátech (DRA)**
        - **Nenakonfigurováno** (*výchozí*) – povolí nastavení použití agenta DRA. Pro nasazení agenta DRA a certifikátů je potřeba, abyste nastavili DRA a Zásady skupiny objekty podnikové infrastruktury veřejných klíčů (PKI).
        - **Ano** – zablokuje možnost použití agenta obnovování dat (DRA) k obnovení jednotek s povoleným bitlockerem.

    - **Minimální délka PIN kódu**  
      CSP: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)

      Zadejte minimální délku spouštěcího PIN kódu, když je během povolování BitLockeru vyžadován čip TPM + PIN. PIN kód musí být dlouhý 4 až 20 číslic.

      Pokud toto nastavení nenakonfigurujete, můžou uživatelé nakonfigurovat spouštěcí PIN kód libovolné délky (mezi 4 a 20 číslicemi).

      Toto nastavení platí jenom v případě, že nástroj BitLocker už není povolený, ale nemá žádný vliv.

  - **Konfigurace metody šifrování pro jednotky operačního systému**  
   CSP: [EncryptionMethodByDriveType]( https://go.microsoft.com/fwlink/?linkid=872526)

    Nakonfigurujte metodu šifrování a sílu šifrování pro jednotky operačního systému. *XTS-AES 128-bit* je výchozí metodou šifrování Windows a doporučenou hodnotou.

    - **Nenakonfigurováno** (*výchozí*)
    - **128bit CBC AES**
    - **256bit CBC AES**
    - **128bit XTS AES**
    - **256bit XTS AES**

### <a name="bitlocker---removable-drive-settings"></a>BitLocker – nastavení jednotky vyměnitelného disku

- **Konfigurace metody šifrování pro jednotky operačního systému**  
  CSP: [nastavení zásady skupiny BitLockeru](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Nenakonfigurováno** (*výchozí*)  
  - **Konfigurace**

  Při nastavení *Konfigurace* můžete nakonfigurovat následující nastavení.

  - **Konfigurace metody šifrování pro vyměnitelné datové jednotky**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)

    Vyberte požadovanou metodu šifrování pro disky vyměnitelných datových jednotek.

    - **Nenakonfigurováno** (*výchozí*)
    - **128bit CBC AES**
    - **256bit CBC AES**
    - **128bit XTS AES**
    - **256bit XTS AES**

  - **Zablokovat přístup pro zápis na vyměnitelné datové jednotky, které nechrání BitLocker**  
    CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

    - **Nenakonfigurováno** (*výchozí*) – data je možné zapsat na nešifrované vyměnitelné jednotky.
    - **Ano** – Windows nepovoluje zápis dat na vyměnitelné jednotky, které nejsou chráněné nástrojem BitLocker. Pokud vložená vyměnitelná jednotka není šifrovaná, musí uživatel dokončit průvodce nastavením BitLockeru před tím, než se udělí přístup pro zápis do jednotky.

    - **Zablokovat přístup pro zápis na vyměnitelné datové jednotky, které nechrání BitLocker**  
      CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

      - **Nenakonfigurováno** (*výchozí*) – lze použít jakoukoli jednotku šifrovanou pomocí BitLockeru.
      - **Ano** – zablokuje přístup k vyměnitelným jednotkám, pokud nebyly zašifrované na počítači, který vlastní vaše organizace.

## <a name="next-steps"></a>Další kroky

[Zásady zabezpečení koncového bodu pro šifrování disků](../protect/endpoint-security-disk-encryption-policy.md)
