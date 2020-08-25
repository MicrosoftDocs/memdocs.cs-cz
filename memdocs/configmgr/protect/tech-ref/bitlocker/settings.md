---
title: Reference k nastavení BitLockeru
titleSuffix: Configuration Manager
description: Všechna nastavení správy BitLockeru dostupná v Configuration Manager
ms.date: 08/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: reference
ms.assetid: f7ade768-2b2b-4aab-8ee1-73624d03a9c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b52fe5a60899d7e871381d1a34a2360bbe68a36c
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820472"
---
# <a name="bitlocker-settings-reference"></a>Reference k nastavení BitLockeru

*Platí pro: Configuration Manager (Current Branch)*

<!-- 5925683 -->

Zásady správy BitLockeru v Configuration Manager obsahují následující skupiny zásad:

- Nastavení
- Jednotka operačního systému
- Pevná jednotka
- Vyměnitelná jednotka
- Správa klientů

Následující části popisují a navrhují konfigurace pro nastavení v jednotlivých skupinách.

> [!NOTE]
> Tato nastavení jsou založená na verzi Configuration Manager 2002. Verze 1910 neobsahuje všechna tato nastavení.

## <a name="setup"></a>Nastavení

Nastavení na této stránce konfigurují globální možnosti šifrování BitLockeru.

### <a name="drive-encryption-method-and-cipher-strength"></a>Metoda šifrování jednotky a síla šifry

*Navrhovaná konfigurace*: je **povolená** s výchozí nebo vyšší metodou šifrování.

> [!NOTE]
> Stránka vlastnosti **instalace** obsahuje dvě skupiny nastavení pro různé verze systému Windows. V této části jsou popsány obě.

#### <a name="windows-81-devices"></a>Zařízení s Windows 8.1

U Windows 8.1 zařízení povolte možnost **Metoda šifrování jednotky a složitou šifru**a vyberte jednu z následujících metod šifrování:

- AES 128-bit s difuzorem
- AES 256-bit s difuzorem
- AES 128-bit (výchozí)
- AES 256-bit

Další informace o tom, jak vytvořit tuto zásadu v prostředí Windows PowerShell, najdete v článku [New-CMBLEncryptionMethodPolicy](/powershell/module/configurationmanager/new-cmblencryptionmethodpolicy?view=sccm-ps).

#### <a name="windows-10-devices"></a>Zařízení s Windows 10

U zařízení s Windows 10 povolte možnost **Metoda šifrování jednotky a sílu šifrování (Windows 10)**. Pak jednotlivě vyberte jednu z následujících metod šifrování pro jednotky operačního systému, pevné datové jednotky a vyměnitelné datové jednotky:

- AES-CBC 128-bit
- AES-CBC 256-bit
- XTS-AES 128-bit (výchozí)
- XTS-AES 256-bit

> [!TIP]
> BitLocker používá jako šifrovací algoritmus standard AES (Advanced Encryption Standard) s konfigurovatelnou délkou klíče 128 nebo 256 bitů. V zařízeních s Windows 10 podporuje šifrování STANDARDu CBC (Cipher Block Chaining) nebo odcizení šifrovaných textů (XTS).
>
> Pokud potřebujete použít vyměnitelnou jednotku na zařízeních, která nepoužívají Windows 10, použijte AES-CBC.

Další informace o tom, jak vytvořit tuto zásadu v prostředí Windows PowerShell, najdete v článku [New-CMBLEncryptionMethodWithXts](/powershell/module/configurationmanager/new-cmblencryptionmethodwithxts?view=sccm-ps).

#### <a name="general-usage-notes-for-drive-encryption-and-cipher-strength"></a>Obecné poznámky k používání pro šifrování jednotky a složitost šifrování

- Pokud tato nastavení zakážete nebo nenakonfigurujete, BitLocker použije výchozí metodu šifrování.

- Configuration Manager použijí tato nastavení při zapnutí nástroje BitLocker.

- Pokud je jednotka už zašifrovaná nebo probíhá, změna těchto nastavení zásad nemění na zařízení šifrování jednotky.

- Použijete-li výchozí hodnotu, sestava dodržování předpisů počítače nástroje BitLocker může zobrazit sílu šifrování jako **neznámou**. Pokud chcete tento problém obejít, povolte toto nastavení a nastavte explicitní hodnotu složitosti šifrování.

### <a name="prevent-memory-overwrite-on-restart"></a>Zabránit přepsání paměti při restartování

*Navrhovaná konfigurace*: **není nakonfigurované**

Nakonfigurujte tuto zásadu, aby se zlepšil výkon při restartování bez přepsání tajných kódů BitLockeru v paměti při restartování.

Pokud tuto zásadu nenakonfigurujete, BitLocker při restartování počítače odebere jeho tajné klíče z paměti.

Další informace o tom, jak vytvořit tuto zásadu v prostředí Windows PowerShell, najdete v článku [New-CMNoOverwritePolicy](/powershell/module/configurationmanager/new-cmnooverwritepolicy?view=sccm-ps).

### <a name="validate-smart-card-certificate-usage-rule-compliance"></a>Ověřit dodržování předpisů pravidla použití certifikátu čipové karty

*Navrhovaná konfigurace*: **není nakonfigurované**

Nakonfigurujte tuto zásadu tak, aby používala ochranu BitLockerem založenou na certifikátech SmartCard. Pak zadejte **identifikátor objektu**certifikátu.

Pokud tuto zásadu nenakonfigurujete, BitLocker použije k určení certifikátu výchozí identifikátor objektu `1.3.6.1.4.1.311.67.1.1` .

Další informace o tom, jak vytvořit tuto zásadu v prostředí Windows PowerShell, najdete v článku [New-CMScCompliancePolicy](/powershell/module/configurationmanager/new-cmsccompliancepolicy?view=sccm-ps).

### <a name="organization-unique-identifiers"></a>Jedinečné identifikátory organizace

*Navrhovaná konfigurace*: **není nakonfigurované**

Nakonfigurujte tuto zásadu na použití agenta obnovení dat založeného na certifikátu nebo čtečky BitLocker to přejít.

Pokud tuto zásadu nenakonfigurujete, BitLocker nepoužije pole **Identifikace** .

Pokud vaše organizace vyžaduje vyšší míry zabezpečení, nakonfigurujte pole **Identifikace** . Nastavte toto pole na všech cílových zařízeních USB a zarovnejte je s tímto nastavením.

Další informace o tom, jak vytvořit tuto zásadu v prostředí Windows PowerShell, najdete v článku [New-CMUidPolicy](/powershell/module/configurationmanager/new-cmuidpolicy?view=sccm-ps).

## <a name="os-drive"></a>Jednotka operačního systému

Nastavení na této stránce konfigurují nastavení šifrování pro jednotku, na které je nainstalovaný systém Windows.

### <a name="operating-system-drive-encryption-settings"></a>Nastavení šifrování jednotky operačního systému

*Navrhovaná konfigurace*: **povoleno**

Pokud povolíte toto nastavení, uživatel musí chránit jednotku operačního systému a BitLocker zašifruje jednotku. Pokud ho zakážete, uživatel nebude moct chránit jednotku. Pokud tuto zásadu nenakonfigurujete, není ochrana BitLockeru na jednotce operačního systému nutná.

> [!NOTE]
> Pokud je už jednotka zašifrovaná a toto nastavení zakážete, BitLocker dešifruje jednotku.  

Pokud máte zařízení bez [čipu TPM (Trusted Platform Module)](/windows/security/information-protection/tpm/trusted-platform-module-top-node), použijte možnost pro **povolení nástroje BitLocker bez kompatibilního čipu TPM (vyžaduje heslo)**. Toto nastavení umožňuje nástroji BitLocker šifrovat jednotku s operačním systémem i v případě, že zařízení nemá čip TPM. Pokud tuto možnost povolíte, systém Windows vyzve uživatele, aby určil heslo nástroje BitLocker.

V zařízeních s kompatibilním čipem TPM lze při spuštění použít dva typy metod ověřování, aby byla zajištěna ochrana šifrovaných dat. Když se počítač spustí, může použít jenom čip TPM k ověřování, nebo může taky vyžadovat zadání osobního identifikačního čísla (PIN). Nakonfigurujte tahle nastavení:

- **Vyberte ochranu pro jednotku operačního systému**: nakonfigurujte ji tak, aby používala čip TPM a kód PIN, nebo jenom čip TPM.

- **Nakonfigurovat minimální délku PIN kódu pro spuštění**: Pokud POŽADUJETE kód PIN, je tato hodnota nejkratší délka, kterou může uživatel zadat. Uživatel zadá tento kód PIN, když se počítač spustí k odemknutí jednotky. Ve výchozím nastavení je minimální délka kódu PIN `4` .

> [!TIP]
> Pokud pro zajištění vyšší úrovně zabezpečení povolíte zařízení s technologií TPM + PIN, zvažte *zakázání* následujících nastavení zásad skupiny v **System**  >  **Power Management**  >  **nastaveních režimu spánku**nástroje řízení spotřeby systému:
>
> - Při přechodu do režimu spánku (napájení ze sítě) povolí stavy v pohotovostním režimu (S1-S3)
>
> - Při přechodu do režimu spánku (na baterii) zapnout úsporné režimy (S1-S3)

Další informace o tom, jak vytvořit tuto zásadu v prostředí Windows PowerShell, najdete v článku [New-CMBMSOSDEncryptionPolicy](/powershell/module/configurationmanager/new-cmbmsosdencryptionpolicy?view=sccm-ps).

### <a name="allow-enhanced-pins-for-startup"></a>Povolení rozšířených PIN kódů pro spuštění

*Navrhovaná konfigurace*: **není nakonfigurované**

Nakonfigurujte BitLocker tak, aby používal rozšířené spouštěcí PIN kódy. Tyto PIN kódy umožňují použití dalších znaků, například velkých a malých písmen, symbolů, čísel a mezer. Toto nastavení platí při zapnutí nástroje BitLocker.

> [!IMPORTANT]
> Ne všechny počítače můžou podporovat rozšířené PIN kódy v prostředí před spuštěním. Než povolíte jeho použití, vyhodnoťte, jestli jsou zařízení kompatibilní s touto funkcí.

Pokud povolíte toto nastavení, všechny nové spouštěcí kódy nástroje BitLocker umožní uživateli vytvářet rozšířené kódy PIN.

- **Vyžadovat PIN kódy jen pro ASCII**: pomůžou zajistit lepší kompatibilitu kódů PIN s počítači, které omezují typ nebo počet znaků, které můžete zadat v prostředí před spuštěním.

Pokud nastavení této zásady zakážete nebo nenakonfigurujete, BitLocker nepoužije rozšířené PIN kódy.

Další informace o tom, jak vytvořit tuto zásadu v prostředí Windows PowerShell, najdete v článku [New-CMEnhancedPIN](/powershell/module/configurationmanager/new-cmenhancedpin?view=sccm-ps).

### <a name="operating-system-drive-password-policy"></a>Zásady pro hesla jednotky operačního systému

*Navrhovaná konfigurace*: **není nakonfigurované**

Pomocí těchto nastavení můžete nastavit omezení pro hesla pro odemknutí jednotek s operačním systémem chráněných BitLockerem. Pokud povolíte ochrany bez čipu TPM na jednotkách operačního systému, nakonfigurujte následující nastavení:

- **Konfigurace složitosti hesla pro jednotky operačního systému**: Pokud chcete vynutit požadavky na složitost hesla, vyberte **vyžadovat složitost hesla**.

- **Minimální délka hesla pro jednotku operačního systému**: ve výchozím nastavení je minimální délka `8` .

- **Vyžadovat hesla jenom standardu ASCII pro vyměnitelné jednotky operačního systému**

Pokud nastavení této zásady povolíte, můžou uživatelé nakonfigurovat heslo, které splňuje požadavky, které definujete.

Další informace o tom, jak vytvořit tuto zásadu v prostředí Windows PowerShell, najdete v článku [New-CMOSPassphrase](/powershell/module/configurationmanager/new-cmospassphrase?view=sccm-ps).

#### <a name="general-usage-notes-for-os-drive-password-policy"></a>Obecné poznámky k používání pro zásady hesel pro jednotky operačního systému

- Aby tato nastavení požadavků na složitost byla účinná, musí také povolit nastavení zásad skupiny, aby **heslo splňovalo požadavky na složitost** v části **Konfigurace počítače**  >  **Windows Settings**  >  **Security Settings**  >  zásady hesel**Zásady účtů Zásady**pro  >  **hesla**.

- BitLocker toto nastavení vynutil, když ho zapnete, ne při odemčení svazku. BitLocker umožňuje odemknout jednotku s jakýmkoli ochranou, která je na disku k dispozici.

- Pokud používáte zásady skupiny k povolení algoritmů kompatibilních se standardem FIPS pro šifrování, algoritmus hash a podepisování, nemůžete povolit hesla jako ochranu nástrojem BitLocker.

### <a name="reset-platform-validation-data-after-bitlocker-recovery"></a>Resetování dat ověření platformy po obnovení BitLockeru

*Navrhovaná konfigurace*: **není nakonfigurované**

Určuje, zda systém Windows aktualizuje data ověřování platformy při spuštění po obnovení nástroje BitLocker.

Pokud toto nastavení povolíte nebo nenakonfigurujete, systém Windows v této situaci aktualizuje data ověřování platformy.

Pokud nastavení této zásady zakážete, Windows v této situaci neaktualizuje data ověření platformy.

Další informace o tom, jak vytvořit tuto zásadu v prostředí Windows PowerShell, najdete v článku [New-CMTpmAutoResealPolicy](/powershell/module/configurationmanager/new-cmtpmautoresealpolicy?view=sccm-ps).

### <a name="pre-boot-recovery-message-and-url"></a>Zpráva o obnovení před spuštěním a adresa URL

*Navrhovaná konfigurace*: **není nakonfigurované**

Když BitLocker zamkne jednotku operačního systému, pomocí tohoto nastavení můžete zobrazit vlastní zprávu o obnovení nebo adresu URL na obrazovce pro obnovení nástroje BitLocker před spuštěním. Toto nastavení platí jenom pro zařízení s Windows 10.

Pokud povolíte toto nastavení, vyberte jednu z následujících možností pro zprávu o obnovení před spuštěním:

- **Použít výchozí zprávu a adresu URL pro obnovení**: zobrazí na obrazovce pro obnovení nástroje BitLocker před spuštěním výchozí zprávu a adresu URL pro obnovení nástroje BitLocker. Pokud jste dříve nakonfigurovali vlastní zprávu nebo adresu URL pro obnovení, použijte tuto možnost k vrácení výchozí zprávy.

- **Použít vlastní zprávu o obnovení**: zahrňte vlastní zprávu na obrazovce pro obnovení nástroje BitLocker před spuštěním.

  - **Možnost vlastní zprávy o obnovení**: zadejte vlastní zprávu, která se zobrazí. Pokud chcete také zadat adresu URL pro obnovení, zahrňte ji jako součást této vlastní zprávy pro obnovení. Maximální délka řetězce je 32 768 znaků.

- **Použít vlastní adresu URL pro obnovení**: nahraďte výchozí adresu URL zobrazenou na obrazovce pro obnovení nástroje BitLocker před spuštěním.

  - **Možnost vlastní adresy URL pro obnovení**: zadejte adresu URL, která se má zobrazit. Maximální délka řetězce je 32 768 znaků.

> [!NOTE]
> V nástroji Pre-Boot nejsou podporovány všechny znaky a jazyky. Nejprve otestujte vlastní zprávu nebo adresu URL, abyste se ujistili, že se zobrazí správně na obrazovce pro obnovení nástroje BitLocker před spuštěním.

Další informace o tom, jak vytvořit tuto zásadu v prostředí Windows PowerShell, najdete v článku [New-CMPrebootRecoveryInfo](/powershell/module/configurationmanager/new-cmprebootrecoveryinfo?view=sccm-ps).

### <a name="encryption-policy-enforcement-settings-os-drive"></a>Nastavení vynucení zásad šifrování (jednotka operačního systému)

*Navrhovaná konfigurace*: **povoleno**

Nakonfigurujte počet dní, po které mohou uživatelé odložit dodržování předpisů BitLocker pro jednotku operačního systému. **Doba odkladu nedodržení předpisů** začíná, když Configuration Manager nejdřív detekuje jako nedodržující předpisy. Po uplynutí tohoto období odkladu uživatelé nemůžou odložit požadovanou akci nebo požádat o výjimku.

Pokud proces šifrování vyžaduje vstup uživatele, zobrazí se dialogové okno ve Windows, které uživatel nemůže zavřít, dokud nezadá požadované informace. Budoucí oznámení o chybách nebo stavu nebudou mít toto omezení.

Pokud nástroj BitLocker nepožaduje zásah uživatele při přidání ochrany, po uplynutí doby odkladu spustí BitLocker šifrování na pozadí.

Pokud toto nastavení zakážete nebo nenakonfigurujete, Configuration Manager nepožaduje, aby uživatelé dodržovali zásady BitLockeru.

Pokud chcete zásady vymáhat hned, nastavte období odkladu `0` .

Další informace o tom, jak vytvořit tuto zásadu v prostředí Windows PowerShell, najdete v článku [New-CMUseOsEnforcePolicy](/powershell/module/configurationmanager/new-cmuseosenforcepolicy?view=sccm-ps).

## <a name="fixed-drive"></a>Pevná jednotka

Nastavení na této stránce konfigurují šifrování pro další datové jednotky v zařízení.

### <a name="fixed-data-drive-encryption"></a>Šifrování pevné datové jednotky

*Navrhovaná konfigurace*: **povoleno**

Spravujte svůj požadavek na šifrování pevných datových jednotek. Pokud povolíte toto nastavení, nástroj BitLocker vyžaduje, aby uživatelé do ochrany umístili všechny pevné datové jednotky. Pak šifruje datové jednotky.

Pokud tuto zásadu povolíte, povolte možnost automatické odemknutí nebo nastavení zásad pro **hesla pro pevné datové jednotky**.

- **Konfigurovat Automatické odemknutí pevné datové jednotky**: povolí nebo vyžádá BitLocker k automatickému odemknutí jakékoli šifrované datové jednotky. Chcete-li použít automatické odemknutí, nástroj také vyžaduje nástroj BitLocker k šifrování [jednotky operačního systému](#os-drive).

Pokud toto nastavení nenakonfigurujete, nástroj BitLocker nepožaduje, aby uživatelé zavedli pevné datové jednotky v rámci ochrany.

Pokud toto nastavení zakážete, uživatelé nebudou moci vkládat pevné datové jednotky v rámci ochrany nástrojem BitLocker. Pokud tuto zásadu zakážete poté, co BitLocker zašifruje pevné datové jednotky, BitLocker dešifruje pevné datové jednotky.

Další informace o tom, jak vytvořit tuto zásadu v prostředí Windows PowerShell, najdete v článku [New-CMBMSFDVEncryptionPolicy](/powershell/module/configurationmanager/new-cmbmsfdvencryptionpolicy?view=sccm-ps).

### <a name="deny-write-access-to-fixed-drives-not-protected-by-bitlocker"></a>Odepřít přístup pro zápis na pevné jednotky, které nechrání BitLocker

*Navrhovaná konfigurace*: **není nakonfigurované**

Vyžadovat ochranu nástrojem BitLocker pro systém Windows k zápisu dat na pevné jednotky na zařízení. BitLocker tuto zásadu použije, když ji zapnete.

Když zapnete toto nastavení:

- Pokud BitLocker chrání pevnou datovou jednotku, Windows je připojí s oprávněním ke čtení a zápisu.

- Pro jakoukoli pevnou datovou jednotku, kterou BitLocker nechrání, ji Windows připojí jako jen pro čtení.

Pokud toto nastavení nenakonfigurujete, Windows připojí všechny pevné datové jednotky s přístupem pro čtení a zápis.

Další informace o tom, jak vytvořit tuto zásadu v prostředí Windows PowerShell, najdete v článku [New-CMFDVDenyWriteAccessPolicy](/powershell/module/configurationmanager/new-cmfdvdenywriteaccesspolicy?view=sccm-ps).

### <a name="fixed-data-drive-password-policy"></a>Zásady pro hesla pevných datových jednotek

*Navrhovaná konfigurace*: **není nakonfigurované**

Pomocí těchto nastavení můžete nastavit omezení pro hesla pro odemknutí pevných datových jednotek chráněných BitLockerem.

Pokud povolíte toto nastavení, uživatelé můžou nakonfigurovat heslo, které splňuje vaše definované požadavky.

Pro vyšší zabezpečení povolte toto nastavení a pak nakonfigurujte následující nastavení:

- **Vyžadovat heslo pro pevný datový disk**: uživatelé musí zadat heslo k odemknutí pevné datové jednotky chráněné nástrojem BitLocker.

- **Konfigurace složitosti hesla pro pevné datové jednotky**: Pokud chcete vynutit požadavky na složitost hesla, vyberte **vyžadovat složitost hesla**.

- **Minimální délka hesla pro pevný datový disk**: ve výchozím nastavení je minimální délka `8` .

Pokud toto nastavení zakážete, uživatelé nemůžou nakonfigurovat heslo.

Pokud zásada není nakonfigurovaná, BitLocker podporuje hesla s výchozími nastaveními. Výchozí nastavení nezahrnuje požadavky na složitost hesla a vyžadují jenom osm znaků.

Další informace o tom, jak vytvořit tuto zásadu v prostředí Windows PowerShell, najdete v článku [New-CMFDVPassPhrasePolicy](/powershell/module/configurationmanager/new-cmfdvpassphrasepolicy?view=sccm-ps).

#### <a name="general-usage-notes-for-fixed-data-drive-password-policy"></a>Obecné poznámky k používání zásad pro hesla pro pevné datové jednotky

- Aby tato nastavení požadavků na složitost byla účinná, musí také povolit nastavení zásad skupiny, aby **heslo splňovalo požadavky na složitost** v části **Konfigurace počítače**  >  **Windows Settings**  >  **Security Settings**  >  zásady hesel**Zásady účtů Zásady**pro  >  **hesla**.

- BitLocker toto nastavení vynutil, když ho zapnete, ne při odemčení svazku. BitLocker umožňuje odemknout jednotku s jakýmkoli ochranou, která je na disku k dispozici.

- Pokud používáte zásady skupiny k povolení algoritmů kompatibilních se standardem FIPS pro šifrování, algoritmus hash a podepisování, nemůžete povolit hesla jako ochranu nástrojem BitLocker.

### <a name="encryption-policy-enforcement-settings-fixed-data-drive"></a>Nastavení vynucení zásad šifrování (pevná datová jednotka)

*Navrhovaná konfigurace*: **povoleno**

Nakonfigurujte počet dní, po které mohou uživatelé odložit dodržování předpisů BitLockeru pro pevné datové jednotky. **Doba odkladu nedodržení předpisů** začíná, když Configuration Manager nejdřív detekuje pevnou datovou jednotku jako nevyhovující. Nevynucování zásad pevné datové jednotky, dokud není kompatibilní s jednotkou operačního systému. Po uplynutí této lhůty uživatelé nemůžou odložit požadovanou akci nebo požádat o výjimku.

Pokud proces šifrování vyžaduje vstup uživatele, zobrazí se dialogové okno ve Windows, které uživatel nemůže zavřít, dokud nezadá požadované informace. Budoucí oznámení o chybách nebo stavu nebudou mít toto omezení.

Pokud nástroj BitLocker nepožaduje zásah uživatele při přidání ochrany, po uplynutí doby odkladu spustí BitLocker šifrování na pozadí.

Pokud toto nastavení zakážete nebo nenakonfigurujete, Configuration Manager nepožaduje, aby uživatelé dodržovali zásady BitLockeru.

Pokud chcete zásady vymáhat hned, nastavte období odkladu `0` .

Další informace o tom, jak vytvořit tuto zásadu v prostředí Windows PowerShell, najdete v článku [New-CMUseFddEnforcePolicy](/powershell/module/configurationmanager/new-cmusefddenforcepolicy?view=sccm-ps).

## <a name="removable-drive"></a>Vyměnitelná jednotka

Nastavení na této stránce konfigurují šifrování pro vyměnitelné jednotky, jako jsou klíče USB.

### <a name="removable-data-drive-encryption"></a>Šifrování vyměnitelných datových jednotek

*Navrhovaná konfigurace*: **povoleno**

Toto nastavení řídí použití nástroje BitLocker u vyměnitelných jednotek.

- **Povolit uživatelům použít ochranu bitlockerem na vyměnitelných datových jednotkách**: uživatelé můžou zapnout ochranu nástrojem BitLocker pro vyměnitelnou jednotku.

- **Umožněte uživatelům pozastavit a dešifrovat BitLocker na vyměnitelných datových jednotkách**: uživatelé můžou odebrat nebo dočasně pozastavit nástroj BitLocker Drive Encryption z vyměnitelné jednotky.

Pokud povolíte toto nastavení a povolíte uživatelům použít ochranu BitLockerem, bude klient Configuration Manager ukládat informace o obnovení vyměnitelných jednotek do služby obnovení v bodu správy. Toto chování umožňuje uživatelům obnovení jednotky, pokud zapomenou nebo ztratí ochranu (heslo).

Když zapnete toto nastavení:

- Povolit nastavení **zásad hesla pro vyměnitelné datové jednotky**

- *Zakažte* následující nastavení zásad skupiny v **nástroji**  >  pro**přístup k vyměnitelnému úložišti** pro uživatele & konfigurací počítačů:

  - **Všechny třídy vyměnitelného úložiště: Odepřít přístup všem**
  - **Vyměnitelné disky: Odepřít přístup pro zápis**
  - **Vyměnitelné disky: Odepřít přístup pro čtení**

Pokud toto nastavení zakážete, uživatelé nemůžou používat BitLocker na vyměnitelných jednotkách.

Další informace o tom, jak vytvořit tuto zásadu v prostředí Windows PowerShell, najdete v článku [New-CMRDVConfigureBDEPolicy](/powershell/module/configurationmanager/new-cmrdvconfigurebdepolicy?view=sccm-ps).

### <a name="deny-write-access-to-removable-drives-not-protected-by-bitlocker"></a>Odepřít přístup pro zápis na vyměnitelné jednotky, které nejsou chráněné nástrojem BitLocker

*Navrhovaná konfigurace*: **není nakonfigurované**

Vyžadovat ochranu nástrojem BitLocker pro systém Windows k zápisu dat na vyměnitelné jednotky na zařízení. BitLocker tuto zásadu použije, když ji zapnete.

Když zapnete toto nastavení:

- Pokud BitLocker chrání vyměnitelnou jednotku, připojí ji Windows s přístupem pro čtení a zápis.

- Pro libovolnou vyměnitelnou jednotku, kterou BitLocker nechrání, ji Windows připojí jako jen pro čtení.

- Pokud povolíte možnost **Odepřít přístup pro zápis do zařízení nakonfigurovaných v jiné organizaci**, nástroj BitLocker udělí oprávnění k zápisu na vyměnitelné jednotky s identifikačními poli, která se shodují s povolenými identifikačními poli. Tato pole definujte s globálním nastavením **jedinečných identifikátorů organizace** na stránce [Nastavení](#setup) .

Když toto nastavení zakážete nebo nenakonfigurujete, Windows připojí všechny vyměnitelné jednotky s přístupem pro čtení a zápis.

> [!NOTE]
> Toto nastavení můžete přepsat pomocí nastavení zásad skupiny v **systému**  >  **přístup k vyměnitelnému úložišti**. Pokud povolíte nastavení zásad skupiny **Vyměnitelné disky: Odepřít přístup pro zápis**, pak BitLocker ignoruje toto nastavení Configuration Manager.

Další informace o tom, jak vytvořit tuto zásadu v prostředí Windows PowerShell, najdete v článku [New-CMRDVDenyWriteAccessPolicy](/powershell/module/configurationmanager/new-cmrdvdenywriteaccesspolicy?view=sccm-ps).

### <a name="removable-data-drive-password-policy"></a>Zásady hesla pro vyměnitelné datové jednotky

*Navrhovaná konfigurace*: **povoleno**

Pomocí těchto nastavení můžete nastavit omezení pro hesla pro odemknutí vyměnitelných jednotek chráněných BitLockerem.

Pokud povolíte toto nastavení, uživatelé můžou nakonfigurovat heslo, které splňuje vaše definované požadavky.

Pro vyšší zabezpečení povolte toto nastavení a pak nakonfigurujte následující nastavení:

- **Vyžadovat heslo pro vyměnitelnou datovou jednotku**: aby uživatelé mohli odemknout vyměnitelnou jednotku chráněnou bitlockerem, musí zadat heslo.

- **Konfigurace složitosti hesla pro vyměnitelné datové jednotky**: Pokud chcete vynutit požadavky na složitost hesla, vyberte **vyžadovat složitost hesla**.

- **Minimální délka hesla pro vyměnitelnou datovou jednotku**: ve výchozím nastavení je minimální délka `8` .

Pokud toto nastavení zakážete, uživatelé nemůžou nakonfigurovat heslo.

Pokud zásada není nakonfigurovaná, BitLocker podporuje hesla s výchozími nastaveními. Výchozí nastavení nezahrnuje požadavky na složitost hesla a vyžadují jenom osm znaků.

Další informace o tom, jak vytvořit tuto zásadu v prostředí Windows PowerShell, najdete v článku [New-CMRDVPassPhrasePolicy](/powershell/module/configurationmanager/new-cmrdvpassphrasepolicy?view=sccm-ps).

#### <a name="general-usage-notes-for-removable-data-drive-password-policy"></a>Obecné poznámky k používání pro zásady hesel pro vyměnitelné datové jednotky

- Aby tato nastavení požadavků na složitost byla účinná, musí také povolit nastavení zásad skupiny, aby **heslo splňovalo požadavky na složitost** v části **Konfigurace počítače**  >  **Windows Settings**  >  **Security Settings**  >  zásady hesel**Zásady účtů Zásady**pro  >  **hesla**.

- BitLocker toto nastavení vynutil, když ho zapnete, ne při odemčení svazku. BitLocker umožňuje odemknout jednotku s jakýmkoli ochranou, která je na disku k dispozici.

- Pokud používáte zásady skupiny k povolení algoritmů kompatibilních se standardem FIPS pro šifrování, algoritmus hash a podepisování, nemůžete povolit hesla jako ochranu nástrojem BitLocker.

## <a name="client-management"></a>Správa klientů

Nastavení na této stránce konfigurují služby a klienty pro správu nástroje BitLocker.

### <a name="bitlocker-management-services"></a>Služby správy nástroje BitLocker

*Navrhovaná konfigurace*: **povoleno**

Když toto nastavení povolíte, Configuration Manager automaticky a tiše zálohuje informace o obnovení klíčů v databázi lokality. Pokud toto nastavení zakážete nebo nenakonfigurujete, Configuration Manager neuloží informace o obnovení klíče.

- **Vyberte informace pro obnovení BitLockeru k uložení**: Nakonfigurujte službu obnovení klíčů pro zálohování informací pro obnovení BitLockeru. Poskytuje metodu správy pro obnovu dat šifrovaných nástrojem BitLocker, což pomáhá zabránit ztrátě dat kvůli chybějícím klíčovým informacím.

- **Povolí ukládání informací pro obnovení do prostého textu**: bez šifrovacího certifikátu správy BitLockeru pro SQL Server Configuration Manager ukládá informace pro obnovení klíče do prostého textu. Další informace najdete v tématu [šifrování dat pro obnovení](../../deploy-use/bitlocker/encrypt-recovery-data.md).

- **Frekvence stavu kontroly klienta (minuty)**: u nakonfigurované frekvence kontroluje klient zásady ochrany BitLockeru a stav počítače a také zálohuje klíč pro obnovení klienta. Ve výchozím nastavení klient Configuration Manager aktualizuje své informace pro obnovení BitLockeru každých 90 minut.

Další informace o tom, jak tyto zásady vytvořit pomocí Windows PowerShellu, najdete tady:

- [Set-CMBlmPlaintextStorage](/powershell/module/configurationmanager/set-cmblmplaintextstorage?view=sccm-ps)
- [New-CMBMSClientConfigureCheckIntervalPolicy](/powershell/module/configurationmanager/new-cmbmsclientconfigurecheckintervalpolicy?view=sccm-ps)

### <a name="user-exemption-policy"></a>Zásady pro výjimky uživatelů

*Navrhovaná konfigurace*: **není nakonfigurované**

Nakonfigurujte způsob kontaktu pro uživatele, aby si vyžádal výjimku z šifrování BitLockeru.

Pokud nastavení této zásady povolíte, zadejte následující informace:

- **Maximální počet dnů do odložení**: počet dní, po které může uživatel odložit vynucované zásadu. Ve výchozím nastavení je tato hodnota `7` dny (jeden týden).

- **Kontaktní metoda**: Určete, jak můžou uživatelé požádat o výjimku: adresu URL, e-mailovou adresu nebo telefonní číslo.

- **Kontakt**: zadejte adresu URL, e-mailovou adresu nebo telefonní číslo. Když si uživatel vyžádá výjimku z ochrany BitLockerem, zobrazí se dialogové okno Windows s pokyny, jak použít. Configuration Manager neověřuje zadané informace.

  - **Adresa URL**: použijte standardní formát adresy URL, `https://website.domain.tld` . Systém Windows zobrazí adresu URL jako hypertextový odkaz.

  - **E-mailová adresa**: použijte standardní formát e-mailové adresy, `user@domain.tld` . Systém Windows zobrazí adresu jako následující hypertextový odkaz: `mailto:user@domain.tld?subject=Request exemption from BitLocker protection` .

  - **Telefonní číslo**: zadejte číslo, které budou vaši uživatelé volat. Systém Windows zobrazí číslo s následujícím popisem: `Please call <your number> for applying exemption` .

Pokud toto nastavení zakážete nebo nenakonfigurujete, Windows nezobrazí uživatelům pokyny pro žádosti o výjimku.

> [!NOTE]
> BitLocker spravuje výjimky na uživatele, nikoli na počítač. Pokud se ke stejnému počítači přihlašuje více uživatelů a jeden uživatel není nepřístupný, BitLocker zašifruje počítač.

Další informace o tom, jak vytvořit tuto zásadu v prostředí Windows PowerShell, najdete v článku [New-CMBMSUserExemptionPolicy](/powershell/module/configurationmanager/new-cmbmsuserexemptionpolicy?view=sccm-ps).

### <a name="url-for-the-security-policy-link"></a>Adresa URL odkazu na zásady zabezpečení

*Navrhovaná konfigurace*: **povoleno**

Zadejte adresu URL, která se zobrazí uživatelům jako **zásady zabezpečení společnosti** ve Windows. Pomocí tohoto odkazu můžete uživatelům poskytnout informace o požadavcích na šifrování. Zobrazuje se, když BitLocker vyzve uživatele k zašifrování jednotky.

Pokud toto nastavení povolíte, nakonfigurujte **adresu URL odkazu na zásady zabezpečení**.

Pokud toto nastavení zakážete nebo nenakonfigurujete, BitLocker nezobrazuje odkaz zásady zabezpečení.

Další informace o tom, jak vytvořit tuto zásadu v prostředí Windows PowerShell, najdete v článku [New-CMMoreInfoUrlPolicy](/powershell/module/configurationmanager/new-cmmoreinfourlpolicy?view=sccm-ps).

## <a name="next-steps"></a>Další kroky

Pokud k vytvoření těchto objektů zásad používáte Windows PowerShell, použijte rutinu [New-CMBlmSetting](/powershell/module/configurationmanager/new-cmblmsetting?view=sccm-ps) . Tato rutina vytvoří objekt nastavení zásad správy BitLockeru, který obsahuje všechny zadané zásady. K nasazení nastavení zásad do kolekce použijte rutinu [New-CMSettingDeployment](/powershell/module/configurationmanager/new-cmsettingdeployment?view=sccm-ps) .
