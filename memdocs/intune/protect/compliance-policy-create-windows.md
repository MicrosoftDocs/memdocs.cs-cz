---
title: Nastavení dodržování předpisů pro Windows 10 v Microsoft Intune – Azure | Microsoft Docs
description: Podívejte se na seznam všech nastavení, která můžete použít při nastavování dodržování předpisů pro zařízení s Windows 10, Windows holografickými a Surface Hub v Microsoft Intune. Podívejte se na dodržování předpisů pro minimální a maximální operační systém, nastavte omezení a délku hesla, vyhledejte řešení partnerů pro ochranu proti virům (AV), povolte šifrování u úložiště dat a další.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 20d3f3967fa77ab90229915afc8b05043004b125
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909342"
---
# <a name="windows-10-and-later-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Nastavení Windows 10 a novějších označení zařízení jako kompatibilních nebo nekompatibilních s Intune

Tento článek obsahuje seznam a popis různých nastavení dodržování předpisů, která můžete konfigurovat v zařízeních s Windows 10 a novějším v Intune. Jako součást řešení správy mobilních zařízení (MDM) použijte Tato nastavení k vyžadování nástroje BitLocker, nastavení minimálního a maximálního operačního systému, nastavení úrovně rizika pomocí rozšířené ochrany před internetovými útoky v programu Microsoft Defender (ATP) a dalších.

Tato funkce platí pro:

- Windows 10 a novější
- Windows Holographic for Business
- Surface Hub

Jako správce Intune můžete pomocí těchto nastavení dodržování předpisů ochránit prostředky vaší organizace. Další informace o zásadách dodržování předpisů a o tom, co dělají, najdete v tématu [Začínáme s dodržováním předpisů pro zařízení](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Než začnete

[Vytvořte zásady dodržování předpisů](create-compliance-policy.md#create-the-policy). V části **platforma**vyberte **Windows 10 a novější**.

## <a name="device-health"></a>Stav zařízení

### <a name="windows-health-attestation-service-evaluation-rules"></a>Pravidla pro vyhodnocení služby ověření stavu systému Windows

- **Vyžadovat nástroj BitLocker**:  
   Windows BitLocker Drive Encryption šifruje všechna data uložená na svazku operačního systému Windows. BitLocker používá čip TPM (Trusted Platform Module) k ochraně operačního systému Windows a uživatelských dat. Pomáhá také ověřit, že počítač není úmyslně poškozen, a to ani v případě, že je jeho levý bezobslužný, ztracený nebo odcizený. Pokud je počítač vybavený kompatibilním čipem TPM, nástroj BitLocker pomocí čipu TPM uzamkne šifrovací klíče, které chrání data. K těmto klíčům proto nelze přistupovat, dokud čip TPM neověří stav počítače.  

  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Vyžadovat** – zařízení může chránit data uložená na disku před neoprávněným přístupem, když je systém vypnutý nebo v režimu hibernace.
  
  [Zařízení HealthAttestation CSP – BitLockerStatus](/windows/client-management/mdm/healthattestation-csp)

- **Vyžadovat, aby na zařízení bylo povolené zabezpečené spouštění**:  
  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Vyžadovat** – systém je nucen spouštět do důvěryhodného stavu výroby. Základní komponenty, které se používají ke spouštění počítače, musí mít správné kryptografické podpisy, které jsou důvěryhodné pro organizaci, která zařízení vyrobila. Firmware UEFI nejdříve ověří podpis a až potom povolí spuštění počítače. Pokud jsou nějaké soubory úmyslně poškozeny, což přeruší svůj podpis, systém se nespustí.

  > [!NOTE]
  > U některých zařízení s čipem TPM 1,2 a 2,0 je nastavení **vyžadovat, aby bylo povolené zabezpečené spuštění na zařízení** . Pokud zařízení nepodporují TPM 2.0 nebo novější, zobrazí se v Intune stav zásady jako **nevyhovující**. Další informace o podporovaných verzích najdete v tématu  [ověření stavu zařízení](/windows/security/information-protection/tpm/trusted-platform-module-overview#device-health-attestation).

- **Vyžadovat integritu kódu**:  
  Integrita kódu je funkce, která ověřuje integritu ovladače nebo systémového souboru pokaždé, když je načten do paměti.
  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Vyžadovat** – vyžaduje integritu kódu, která detekuje, jestli se do jádra nenačítá nepodepsaný ovladač nebo systémový soubor. Také zjistí, zda je systémový soubor změněn škodlivým softwarem nebo spuštěn pomocí uživatelského účtu s oprávněními správce.

Další zdroje informací:

- Podrobnosti o tom, jak služba ověření stavu funguje, najdete v tématu [poskytovatel CSP služby Health Attestation](/windows/client-management/mdm/healthattestation-csp).
- [Tip podpory: použití nastavení ověření stavu zařízení jako součást zásad dodržování předpisů v Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Using-Device-Health-Attestation-Settings-as-Part-of/ba-p/282643).

## <a name="device-properties"></a>Vlastnosti zařízení

### <a name="operating-system-version"></a>Verze operačního systému

- **Minimální verze operačního systému**:  
  Zadejte minimální povolenou verzi ve formátu **čísla major.minor.Build.cu** . Správnou hodnotu získáte, když otevřete příkazový řádek a zadáte `ver`. Příkaz `ver` vrátí verzi v následujícím formátu:

  `Microsoft Windows [Version 10.0.17134.1]`

  Pokud má zařízení starší verzi, než je zadaná verze operačního systému, nahlásí se jako nedodržující předpisy. Zobrazí se odkaz s informacemi, jak upgradovat. Koncový uživatel si může upgradovat svoje zařízení. Po upgradu budou mít přístup k prostředkům společnosti.

- **Maximální verze OS**:  
  Zadejte maximální povolenou verzi v **číselném formátu hlavní_verze. podverze. Build. Revision** . Správnou hodnotu získáte, když otevřete příkazový řádek a zadáte `ver`. Příkaz `ver` vrátí verzi v následujícím formátu:

  `Microsoft Windows [Version 10.0.17134.1]`

  Pokud zařízení používá verzi operačního systému, která je novější než zadaná verze, bude přístup k prostředkům organizace blokovaný. Koncovému uživateli se zobrazí výzva, aby kontaktoval správce IT. Zařízení nemá přístup k prostředkům organizace, dokud se nezmění pravidlo, které umožňuje verzi operačního systému.

- **Minimální požadovaný operační systém pro mobilní zařízení**:  
  Zadejte minimální povolenou verzi ve formátu hlavní. podverze. sestavení.

  Pokud má zařízení starší verzi operačního systému, kterou zadáte, nahlásí se jako nedodržující předpisy. Zobrazí se odkaz s informacemi, jak upgradovat. Koncový uživatel si může upgradovat svoje zařízení. Po upgradu budou mít přístup k prostředkům společnosti.

- **Maximální požadovaný operační systém pro mobilní zařízení**:  
  Zadejte maximální povolenou verzi v hlavní číslo. podverze. sestavení.

  Pokud zařízení používá verzi operačního systému, která je novější než zadaná verze, bude přístup k prostředkům organizace blokovaný. Koncovému uživateli se zobrazí výzva, aby kontaktoval správce IT. Zařízení nemá přístup k prostředkům organizace, dokud se nezmění pravidlo, které umožňuje verzi operačního systému.

- **Platná sestavení operačního systému**:  
  Zadejte rozsah pro přijatelné verze operačních systémů, včetně minimální a maximální hodnoty. Seznam vyhovujících čísel buildů operačních systémů také můžete **exportovat** do textového souboru CSV s oddělovači.

## <a name="configuration-manager-compliance"></a>Configuration Manager dodržování předpisů

Platí jenom pro spoluspravovaná zařízení s Windows 10 a novějším. Zařízení jenom v Intune vracejí stav není k dispozici.

- **Vyžadovat Configuration Manager dodržování předpisů zařízením**:  
  - **Nenakonfigurováno** (*výchozí*) – Intune nekontroluje žádné nastavení Configuration Manager pro dodržování předpisů.
  - **Vyžadovat** – vyžaduje, aby všechna nastavení (konfigurační položky) v Configuration Manager splňovala předpisy.

    Můžete například vyžadovat, aby v zařízeních byly nainstalované všechny aktualizace softwaru. V Configuration Manager má tento požadavek stav nainstalováno. Pokud jsou některé programy v zařízení v neznámém stavu, zařízení nedodržuje předpisy v Intune.

  > [!NOTE]
  > V případě, že je úloha dodržování předpisů pro spolusprávu nastavená na *Configuration Manager*, je třeba použít pouze **dodržování předpisů zařízením od Configuration Manager** . Když použijete toto nastavení s úlohou kompatibility nastavenou na *Intune*, může to ovlivnit celkové hodnocení dodržování předpisů.

## <a name="system-security"></a>Zabezpečení systému

### <a name="password"></a>Heslo

- **Vyžadovat heslo k odemknutí mobilních zařízení**:  
  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení není vyhodnoceno pro dodržování předpisů nebo nedodržování předpisů.
  - **Vyžadovat** – uživatelé musí zadat heslo, aby mohli získat přístup ke svému zařízení. 

- **Jednoduchá hesla**:  
  - **Nenakonfigurováno** (*výchozí*) – uživatelé můžou vytvářet jednoduchá hesla, například **1234** nebo **1111**.
  - **Blok** – uživatelé nemůžou vytvářet jednoduchá hesla, třeba **1234** nebo **1111**.

- **Typ hesla**:  
  Vyberte požadovaný typ hesla nebo PIN kódu. Možnosti:
  - **Výchozí nastavení zařízení** (*výchozí*) – vyžadovat heslo, číselný kód PIN nebo alfanumerický kód PIN
  - **Číselná** – vyžaduje heslo nebo číselný PIN kód.
  - **Alfanumerické** – vyžaduje heslo, nebo alfanumerický kód PIN.  
  
  Pokud je nastaveno na *alfanumerické*, jsou k dispozici následující nastavení:  
  - **Složitost hesla**:  
    Možnosti:
    - **Vyžadovat číslice a malá písmena** (*výchozí*)
    - **Vyžadovat číslice, malá písmena a velká písmena**
    - **Vyžadovat číslice, malá písmena, Velká písmena a speciální znaky**

    > [!TIP]
    > Alfanumerické zásady hesel můžou být složité. Doporučujeme správcům, aby si přečetli CSP pro další informace:
    >
    > - [CSP DeviceLock/AlphanumericDevicePasswordRequired](/windows/client-management/mdm/policy-csp-devicelock#devicelock-alphanumericdevicepasswordrequired)
    > - [CSP DeviceLock/MinDevicePasswordComplexCharacters](/windows/client-management/mdm/policy-csp-devicelock#devicelock-mindevicepasswordcomplexcharacters)

- **Minimální délka hesla**:  
  Zadejte minimální počet číslic nebo znaků, které musí heslo obsahovat.

- **Maximální počet minut nečinnosti před vyžadováním hesla**:  
  Zadejte dobu nečinnosti, než uživatel musí znovu zadat heslo.

- **Vypršení platnosti hesla (dny)**:  
  Zadejte počet dní do vypršení platnosti hesla a musí vytvořit nové, od 1-730.

- **Počet předchozích hesel, která zabrání opakovanému použití**:  
  Zadejte počet dříve použitých hesel, která se nedají použít.

- **Vyžadovat heslo při návratu zařízení ze stavu nečinnosti (mobilní a holografická)**:  
  - **Nenakonfigurováno** (*výchozí*)
  - **Vyžadovat** – vyžaduje, aby uživatelé zařízení zadali heslo pokaždé, když se zařízení vrátí ze stavu nečinnosti.

  > [!IMPORTANT]
  > Když se požadavek na heslo změní na plochu Windows, uživatelé budou mít vliv na jeho příštím přihlášení, protože to znamená, že zařízení přestane být aktivní. Uživatelům s hesly, kteří splňují požadavky, se stále zobrazí výzva ke změně hesla.

### <a name="encryption"></a>Šifrování

- **Šifrování datového úložiště na zařízení**:  
  Toto nastavení se vztahuje na všechny jednotky na zařízení.
  - **Nenakonfigurováno** (*výchozí*)
  - **Vyžadovat** *– použít k* šifrování úložiště dat na vašich zařízeních.
  
   [DeviceStatus CSP – DeviceStatus/dodržování předpisů/EncryptionCompliance](/windows/client-management/mdm/devicestatus-csp)

  > [!NOTE]
  > Nastavení **Šifrování datového úložiště na zařízení** kontroluje obecnou přítomnost šifrování v zařízení. Pokud chcete nastavení šifrování zkontrolovat důkladněji, použijte možnost **Vyžadovat BitLocker**, která k ověření stavu BitLockeru na úrovni čipu TPM používá službu Ověření stavu zařízení s Windows.

### <a name="device-security"></a>Zabezpečení zařízení  

- **Brána firewall**:  
  - **Nenakonfigurováno** (*výchozí*) – Intune neřídí firewall v programu Microsoft Defender ani nemění stávající nastavení.
  - **Vyžadovat** – zapnout firewall v programu Microsoft Defender a zabránit uživatelům v jeho vypnutí.

  [Zprostředkovatel CSP brány firewall](/windows/client-management/mdm/firewall-csp)

  > [!NOTE]
  > Pokud se zařízení hned po restartování synchronizuje nebo hned synchronizuje probuzení z režimu spánku, toto nastavení se může hlásit jako **Chyba**. Tento scénář nemusí mít vliv na celkový stav dodržování předpisů zařízením. Pokud chcete znovu vyhodnotit stav dodržování předpisů, proveďte ruční [synchronizaci zařízení](../user-help/sync-your-device-manually-windows.md).

- **Čip TPM (Trusted Platform Module)**:  
  - **Nenakonfigurováno** (*výchozí*) – Intune nekontroluje u zařízení verzi čipu TPM.
  - **Vyžadovat** – Intune kontroluje dodržování předpisů ve verzi čipu TPM. Zařízení splňuje předpisy, pokud je verze čipu TPM větší než **0** (nula). Zařízení nedodržuje předpisy, pokud na zařízení není verze TPM.

  [DeviceStatus CSP – DeviceStatus/TPM/SpecificationVersion](/windows/client-management/mdm/devicestatus-csp)
  
- **Antivirová ochrana**:  
  - **Nenakonfigurováno** (*výchozí*) – Intune nekontroluje žádná antivirová řešení nainstalovaná na zařízení.
  - **Vyžadovat** – kontroluje dodržování předpisů pomocí antivirových řešení, která jsou zaregistrovaná ve [Windows Security Center](https://blogs.windows.com/windowsexperience/2017/01/23/introducing-windows-defender-security-center/), jako je Symantec a Microsoft Defender.

  [DeviceStatus CSP – DeviceStatus/Antivirus/status](/windows/client-management/mdm/devicestatus-csp)

- **Antispywarový**program:  
  - **Nenakonfigurováno** (*výchozí*) – Intune nekontroluje žádná antispywarová řešení nainstalovaná na zařízení.
  - **Vyžadovat** – kontroluje dodržování předpisů pomocí antispywarových řešení, která jsou zaregistrovaná ve [Windows Security Center](https://blogs.windows.com/windowsexperience/2017/01/23/introducing-windows-defender-security-center/), jako je Symantec a Microsoft Defender.

  [DeviceStatus CSP – DeviceStatus/antispywarový/status](/windows/client-management/mdm/devicestatus-csp)

### <a name="defender"></a>Defender

*S Windows 10 Desktop podporuje následující nastavení dodržování předpisů.*

- **Antimalware v programu Microsoft Defender**:  
  - **Nenakonfigurováno** (*výchozí*) – Intune neřídí službu ani nemění stávající nastavení.
  - **Vyžadovat** – zapnout službu Microsoft Defender anti-malware a zabránit uživatelům v jejich vypnutí.

- **Minimální verze antimalwaru v programu Microsoft Defender**:  
  Zadejte minimální povolenou verzi služby Microsoft Defender anti-malware. Zadejte například `4.11.0.0`. Pokud je ponecháno prázdné, bude možné použít jakoukoli verzi služby Microsoft Defender anti-malware.

  *Ve výchozím nastavení není nakonfigurována žádná verze*.

- **Microsoft Defender antimalwar Security –** přehledy v aktuálním stavu:  
  Řídí aktualizace ochrany proti virům a hrozbám zabezpečení systému Windows na zařízeních.
  - **Nenakonfigurováno** (*výchozí*) – Intune neuplatňuje žádné požadavky.
  - **Vyžadovat** – vynuťte aktuálnost Microsoft Defender Security Intelligence.

  [Defender CSP – Defender/Health/SignatureOutOfDate CSP](/windows/client-management/mdm/defender-csp)
  
  Další informace najdete v článku [aktualizace Security Intelligence pro antivirovou ochranu v programu Microsoft Defender a další antimalware Microsoftu](https://www.microsoft.com/en-us/wdsi/defenderupdates).

- **Ochrana v reálném čase**:  
  - **Nenakonfigurováno** (*výchozí*) – Intune neřídí tuto funkci ani nemění stávající nastavení.
  - **Vyžaduje** – zapněte ochranu v reálném čase, která kontroluje malware, spyware a další nežádoucí software.  

  [Zásady CSP – Defender/AllowRealtimeMonitoring CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

## <a name="microsoft-defender-atp"></a>Microsoft Defender ATP

### <a name="microsoft-defender-advanced-threat-protection-rules"></a>Pravidla rozšířené ochrany před internetovými útoky v programu Microsoft Defender

- **Vyžadovat, aby zařízení bylo na nebo pod hodnocením rizika počítače**:  
  Toto nastavení použijte, pokud chcete jako podmínku dodržování předpisů převzít vyhodnocení rizik ze služeb ochrany před hrozbami. Vyberte maximální povolenou úroveň hrozby:
  - **Nenakonfigurováno** (*výchozí*)  
  - **Clear** – Tato možnost je nejbezpečnější, protože zařízení nemůže mít žádné hrozby. Pokud se zjistí, že zařízení má jakoukoli úroveň hrozeb, vyhodnotí se jako nedodržující předpisy.
  - **Nízká** – zařízení se vyhodnotí jako vyhovující, pokud jsou přítomny jenom hrozby nízké úrovně. Jakákoliv vyšší úroveň zařízení zařadí do stavu nedodržující předpisy.
  - **Střední** – zařízení se vyhodnotí jako vyhovující, pokud jsou stávající hrozby v zařízení na nízké nebo střední úrovni. Pokud se zjistí, že zařízení bude mít hrozby vysoké úrovně, je zjištěno, že nedodržuje předpisy.
  - **Vysoká** – Tato možnost je nejméně bezpečná a umožňuje všechny úrovně hrozeb. Může být užitečná, pokud toto řešení používáte jen ke generování sestav.
  
  Informace o nastavení ochrany ATP Microsoft Defenderu (Rozšířená ochrana před internetovými útoky) jako služby ochrany před hrozbami najdete v tématu [Povolení ATP Microsoft Defenderu s podmíněným přístupem](advanced-threat-protection.md).

## <a name="windows-holographic-for-business"></a>Windows Holographic for Business

Windows Holographic for Business používá platformu **Windows 10 a novější**. Windows Holographic for Business podporuje následující nastavení:

- **Zabezpečení systému**  >  **Šifrování**  >  **Šifrování datového úložiště na zařízení**.

Pokud chcete ověřit šifrování u zařízení Microsoft HoloLens, přečtěte si článek [Ověření šifrování zařízení](/hololens/security-encryption-data-protection).

## <a name="surface-hub"></a>Surface Hub

Surface Hub používá platformu **Windows 10 a novější**. Centra Surface jsou podporovaná pro dodržování předpisů i pro podmíněný přístup. Pokud chcete tyto funkce na Surface Hub povolit, doporučujeme [Povolit automatickou registraci Windows 10](../enrollment/windows-enroll.md) v Intune (vyžaduje Azure Active Directory (Azure AD)) a cílit na Surface Hub zařízení jako na skupiny zařízení. Rozbočovače Surface musí být připojená k Azure AD pro dodržování předpisů a podmíněný přístup pro práci.

Pokyny najdete v tématu [Nastavení registrace pro zařízení s Windows](../enrollment/windows-enroll.md).

## <a name="next-steps"></a>Další kroky

- [Přidejte akce pro zařízení nedodržující předpisy](actions-for-noncompliance.md) a [použijte značky oboru k filtrování zásad](../fundamentals/scope-tags.md).
- [Monitorujte zásady dodržování předpisů](compliance-policy-monitor.md).
- Podívejte se na [nastavení zásad dodržování předpisů pro zařízení Windows 8.1](compliance-policy-create-windows-8-1.md) .