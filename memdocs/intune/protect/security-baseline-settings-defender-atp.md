---
title: Nastavení standardních hodnot zabezpečení v Intune pro rozšířenou ochranu před internetovými útoky v programu Microsoft Defender
titleSuffix: Microsoft Intune
description: Nastavení standardních hodnot zabezpečení, které Intune podporuje pro správu rozšířené ochrany před internetovými útoky v programu Microsoft Defender
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
zone_pivot_groups: atp-baseline-versions
ms.openlocfilehash: d29240dcbcbbcd5a4399dbfb3648c2a6df47764c
ms.sourcegitcommit: 46d4bc4fa73b22ae2a6a17a2d1cc6ec933a50e89
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88663425"
---
<!-- Pivots in use: 
::: zone pivot="atp-april-2020"
::: zone-end

::: zone pivot="atp-march-2020"
::: zone-end

::: zone pivot="atp-march-2020,atp-april-2020"
::: zone-end
-->

# <a name="microsoft-defender-advanced-threat-protection-baseline-settings-for-intune"></a>Základní nastavení pro Intune v programu Microsoft Defender Advanced Threat Protection

Zobrazit základní nastavení nástroje Microsoft Defender Advanced Threat Protection, která jsou podporována nástrojem Microsoft Intune. Výchozí hodnoty standardních hodnot rozšířené ochrany před internetovými útoky (ATP) znázorňují doporučenou konfiguraci ATP a nemusí odpovídat výchozím hodnotám pro jiné standardní hodnoty zabezpečení.

::: zone pivot="atp-april-2020"

Podrobnosti v tomto článku se týkají verze 4 standardních hodnot ATP v programu Microsoft Defender, který byl vydán 21. dubna 2020. Chcete-li zjistit, co se změnilo v této verzi směrného plánu z předchozích verzí, použijte akci [Porovnat směrné plány](../protect/security-baselines.md#compare-baseline-versions) , která je k dispozici při prohlížení podokna *verze* pro tento směrný plán.

::: zone-end
::: zone pivot="atp-march-2020"

Podrobnosti v tomto článku se týkají verze 3 standardních hodnot ATP v programu Microsoft Defender, který byl vydán 1. března 2020. Chcete-li zjistit, co se změnilo v této verzi směrného plánu z předchozích verzí, použijte akci [Porovnat směrné plány](../protect/security-baselines.md#compare-baseline-versions) , která je k dispozici při prohlížení podokna *verze* pro tento směrný plán.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"


Směrný plán rozšířené ochrany před internetovými útoky v programu Microsoft Defender je dostupný, když vaše prostředí splňuje požadavky na používání [rozšířené ochrany před internetovými útoky v programu Microsoft Defender](advanced-threat-protection.md#prerequisites).

Tato standardní hodnota je optimalizovaná pro fyzická zařízení a v tuto chvíli se nedoporučuje používat na virtuálních počítačích (VM) nebo koncových bodech VDI. Určitá nastavení standardních hodnot můžou mít vliv na vzdálené interaktivní relace ve virtualizovaných prostředích. Další informace najdete v dokumentaci k Windows v tématu [zvýšení dodržování předpisů pro základní hodnoty zabezpečení služby Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) .


## <a name="application-guard"></a>Ochrana Application Guard

Další informace najdete v tématu [WINDOWSDEFENDERAPPLICATIONGUARD CSP](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp) v dokumentaci k systému Windows.  

Při používání Microsoft Edge Aplikace Microsoft Defender Application Guard chrání vaše prostředí od webů, které nedůvěřují vaší organizaci. Když uživatelé navštíví weby, které nejsou uvedené ve vaší izolované síti, lokality se otevřou v rámci virtuální relace procházení technologie Hyper-V. Důvěryhodné lokality jsou definovány pomocí hranice sítě.  

- **Zapnout ochranu Application Guard pro Edge (možnosti)**  
  CSP: [Nastavení/AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)
  
  - **Povoleno pro Edge** (*výchozí*) – Application Guard otevírá neschválené weby v kontejneru procházení virtualizované technologie Hyper-V.
  - **Nenakonfigurováno** – v zařízení se otevře žádná lokalita (důvěryhodná a nedůvěryhodná) a ne v virtualizovaném kontejneru.  
  
  Když nastavíte možnost *Povolit pro Edge*, můžete nakonfigurovat *blokování externího obsahu od neschválených webů* a chování ve *schránce*od jiných organizací.

  - **Zablokovat externí obsah od nepodnikových lokalit, které byly schváleny**  
    CSP: [Nastavení/BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **Ano** (*výchozí*) – zablokuje načítání obsahu z neschválených webů.
    - **Nenakonfigurováno** – na zařízení můžou být otevřené nepodnikové weby.

  - **Chování schránky**  
    CSP: [Nastavení/ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    Vyberte, které akce kopírování a vkládání jsou povolené mezi místním počítačem a virtuálním prohlížečem Application Guard. Vaše možnosti jsou:
    - **Není nakonfigurováno**  
    - **Zablokovat kopírování a vkládání mezi počítačem a prohlížečem** (*výchozí*) – zablokuje obojí. Data se nemůžou přenášet mezi počítačem a virtuálním prohlížečem.
    - **Povolení kopírování a vkládání z prohlížeče pouze do počítačů** – data nelze přenést z počítače do virtuálního prohlížeče.
    - **Povolení kopírování a vkládání z počítače jenom do prohlížeče** – data se nemůžou přenášet z virtuálního prohlížeče na hostitelský počítač.
    - **Povoluje kopírování a vkládání mezi počítačem a prohlížečem** – neexistuje žádný blok pro obsah.

- **Zásady izolace sítě systému Windows**  
  CSP: [zásady CSP – NetworkIsolation](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-networkisolation)

  Zadejte seznam *domén sítě*, což jsou podnikové prostředky hostované v cloudu, které Application Guard považuje za podnikové lokality.
  - **Konfigurace** (*výchozí*)
  - **Není nakonfigurováno**

  Po nastavení *Konfigurace* můžete definovat *síťové domény*.

  - **Síťové domény**  
    Vyberte **Přidat** a zadejte domény, rozsahy IP adres a síťové hranice. Ve výchozím nastavení je *SecurityCenter.Windows.com* nakonfigurovaný.

## <a name="bitlocker"></a>BitLocker

Další informace najdete v dokumentaci k Windows v části [nastavení zásady skupiny BitLockeru](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings) .

- **Vyžadovat šifrování paměťových karet (jenom mobilní zařízení)**  
  CSP: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  Toto nastavení platí pouze pro zařízení se systémem Windows Mobile a Mobile Enterprise SKU.
  - **Ano** (*výchozí*) – pro mobilní zařízení se vyžadují šifrování u paměťových karet.
  - **Nenakonfigurováno** – nastavení se vrátí k VÝCHOZÍmu operačnímu systému, což nepožaduje šifrování paměťové karty.

  > [!NOTE]
  > Podpora pro [Windows 10 Mobile](https://support.microsoft.com/help/4485197/windows-10-mobile-end-of-support-faq) a [Windows Phone 8,1](https://support.microsoft.com/help/4036480/windows-phone-8-1-end-of-support-faq) skončila v srpnu 2020.

- **Povolení úplného šifrování disku pro operační systém a pevné datové jednotky**  
  CSP: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  Pokud byla jednotka zašifrovaná předtím, než se tato zásada použila, neprovádí se žádná další akce. Pokud metoda šifrování a možnosti odpovídají této zásadě, měla by konfigurace vrátit úspěch. Pokud možnost místní konfigurace BitLockeru neodpovídá těmto zásadám, konfigurace nejspíš vrátí chybu.
  
  Pokud chcete tuto zásadu použít na disk, který je už zašifrovaný, dešifrujte jednotku a znovu použijte zásady MDM. Výchozí nastavení systému Windows není vyžadovat nástroj BitLocker Drive Encryption, ale při připojení ke službě Azure AD a automatickém šifrování účtu Microsoft (MSA) se může povolit BitLocker při použití šifrování XTS-AES 128-bit.

  - **Ano** (*výchozí*) – vynutilo použití BitLockeru.
  - **Nenakonfigurováno** – žádné vynucení BitLockeru neproběhne.

- **Zásada systémové jednotky BitLockeru**  
  [Nastavení Zásady skupiny BitLockeru](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **Konfigurace** (*výchozí*)
  - **Není nakonfigurováno**

  Po nastavení *Konfigurace*můžete nakonfigurovat *metodu šifrování pro jednotky operačního systému*.

  - **Konfigurace metody šifrování pro jednotky operačního systému**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Toto nastavení je k dispozici, když je *zásada systémové jednotky nástroje BitLocker* nastavena na hodnotu *Konfigurovat*.  

    Nakonfigurujte metodu šifrování a sílu šifrování pro systémové jednotky.  *XTS-AES 128-bit* je výchozí metodou šifrování Windows a doporučenou hodnotou.

    - **Nenakonfigurováno** (*výchozí*)
    - **128bit CBC AES**
    - **256bit CBC AES**
    - **128bit XTS AES**
    - **256bit XTS AES**

- **Zásady pevné jednotky BitLockeru**  
  [Nastavení Zásady skupiny BitLockeru](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Konfigurace** (*výchozí*)
  - **Není nakonfigurováno**

  Když nastavíte *konfiguraci*, můžete nakonfigurovat *přístup zablokování na pevné datové jednotky, které nechrání BitLocker* , a *nakonfigurovat metodu šifrování pro pevné datové jednotky*.

  - **Blokovat přístup pro zápis na pevné datové jednotky, které nechrání BitLocker**  
    CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    Toto nastavení je k dispozici, když je *zásada pevná jednotka nástroje BitLocker* nastavená na hodnotu *Konfigurovat*.

    - **Nenakonfigurováno** (*výchozí*) – data je možné zapsat na nešifrované pevné jednotky.
    - **Ano** – Windows nebude umožňovat zápis jakýchkoli dat na pevné jednotky, které nejsou chráněné bitlockerem. Pokud pevná jednotka není šifrovaná, bude uživatel muset před udělením přístupu pro zápis dokončit průvodce nastavením BitLockeru jednotky.

  - **Konfigurace metody šifrování pro pevné datové jednotky**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Toto nastavení je k dispozici, když je *zásada pevná jednotka nástroje BitLocker* nastavená na hodnotu *Konfigurovat*.

    Nakonfigurujte metodu šifrování a sílu šifrování pro disky s pevnými datovými jednotkami. *XTS-AES 128-bit* je výchozí metodou šifrování Windows a doporučenou hodnotou.

    - **Nenakonfigurováno** (*výchozí*)
    - **128bit CBC AES**
    - **256bit CBC AES**
    - **128bit XTS AES**
    - **256bit XTS AES**

- **Zásada pro vyměnitelné jednotky BitLockeru**  
  [Nastavení Zásady skupiny BitLockeru](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Konfigurace** (*výchozí*)
  - **Není nakonfigurováno**

  Po nastavení *Konfigurace*můžete nakonfigurovat *metodu šifrování pro vyměnitelné datové jednotky* a *zablokovat přístup pro zápis na vyměnitelné datové jednotky, které nechrání BitLocker*.

  - **Konfigurace metody šifrování pro vyměnitelné datové jednotky**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Toto nastavení je dostupné, když je *zásada vyměnitelné jednotky BitLockeru* nastavená na *Konfigurovat*.

    Nakonfigurujte metodu šifrování a sílu šifrování pro disky vyměnitelných datových jednotek. *XTS-AES 128-bit* je výchozí metodou šifrování Windows a doporučenou hodnotou.

    - **Není nakonfigurováno**
    - **128bit CBC AES**
    - **AES 256BIT CBC** (*výchozí*)
    - **128bit XTS AES**
    - **256bit XTS AES**

  - **Zablokovat přístup pro zápis na vyměnitelné datové jednotky, které nechrání BitLocker**  
    CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)  
    Toto nastavení je dostupné, když je *zásada vyměnitelné jednotky BitLockeru* nastavená na *Konfigurovat*.

    - **Nenakonfigurováno** (*výchozí*) – data je možné zapsat na nešifrované vyměnitelné jednotky.  
    - **Ano** – Windows neumožní zapsat žádná data na vyměnitelné jednotky, které nejsou chráněné bitlockerem. Pokud není vyměnitelná jednotka šifrovaná, musí uživatel před udělením přístupu pro zápis dokončit průvodce nastavením BitLockeru jednotky.

## <a name="browser"></a>Prohlížeč

- **Vyžadovat filtr SmartScreen pro Microsoft Edge**  
  CSP: [browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **Ano** (*výchozí*) – pomocí filtru SmartScreen ochráníte uživatele před potenciálními podvodnými zprávami a škodlivým softwarem.
  - **Není nakonfigurováno**

- **Blokovat přístup ke škodlivému webu**  
  CSP: [browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **Ano** (*výchozí*) – zablokuje uživatelům ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a zablokuje jejich přesun na web.
  - **Není nakonfigurováno**

- **Blokovat stahování neověřených souborů**  
  CSP: [browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **Ano** (*výchozí*) – zablokuje uživatelům ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a zablokuje stahování neověřených souborů.
  - **Není nakonfigurováno**

## <a name="data-protection"></a>Ochrana dat

- **Zablokovat přímý přístup do paměti**  
  CSP: [DataProtection/AllowDirectMemoryAccess](https://go.microsoft.com/fwlink/?linkid=2067031)  

  Nastavení této zásady se vynutilo jenom v případě, že je povolené BitLocker nebo šifrování zařízení.

  - **Ano** (*výchozí*) – zablokuje přímý přístup do paměti (DMA) pro všechny horké porty PCI pro příjem po dobu, kdy se uživatel do Windows přihlásí. Jakmile se uživatel přihlásí, systém Windows zobrazí zařízení PCI připojená k portům plug-in hostitele. Pokaždé, když uživatel zamkne počítač, je přímý přístup do zásuvky na konektorech PCI bez podřízených zařízení blokovaný, dokud se uživatel znovu nepřipojí. Zařízení, která už jsou ve výčtu, když se počítač odemkne, bude dál fungovat, dokud nebude odpojený.
  - **Není nakonfigurováno**

## <a name="device-guard"></a>Ochrana zařízení  

- **Zapnout ochranu Credential Guard**  
  CSP: [DeviceGuard/ConfigureSystemGuardLaunch](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard používá hypervisor Windows k poskytování ochrany, která vyžaduje ochranu pomocí zabezpečeného spouštění a ochrany DMA, což vyžaduje splnění požadavků na hardware.

  - **Nenakonfigurováno** – zakažte použití Credential Guard, což je výchozí nastavení systému Windows.
  - **Povolit s zámkem UEFI** (*výchozí*) – povolí ochranu přihlašovacích údajů a neumožní její vzdálené zakázání, protože konfiguraci rozhraní UEFI trvalá musí být ručně smazána.
  - **Povolit bez zámku UEFI** – povolí ochranu přihlašovacích údajů a povolí, aby bylo vypnuté bez fyzického přístupu k počítači.

## <a name="device-installation"></a>Instalace zařízení

- **Instalace hardwarových zařízení podle identifikátorů zařízení**  
  [DeviceInstallation/PreventInstallationOfMatchingDeviceIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  Toto nastavení zásad umožňuje zadat seznam technologie Plug and Play ID hardwaru a kompatibilní ID pro zařízení, na která systém Windows znemožňuje instalaci. Nastavení této zásady má přednost před jinými nastaveními zásad, která umožňují systému Windows nainstalovat zařízení.  Pokud nastavení této zásady povolíte na vzdáleném počítači, nastavení zásad bude mít vliv na přesměrování zadaných zařízení z klienta vzdálené plochy na server vzdálené plochy.

  - **Není nakonfigurováno**
  - **Povolit instalaci hardwarového zařízení** – zařízení je možné nainstalovat a aktualizovat tak, aby byla povolená nebo zabrání jiným nastavením zásad.
  - **Blokovat instalaci hardwarového zařízení** (*výchozí*) – systému Windows se znemožní nainstalovat zařízení, jehož ID hardwaru nebo kompatibilní ID se zobrazí v seznamu, který definujete.

  Pokud je nastavená možnost *blokovat instalaci hardwarového zařízení* , můžete nakonfigurovat *Odebrání odpovídající hardwarových zařízení* a *identifikátorů hardwarových zařízení, které jsou blokované*.

  - **Odebrat shodná hardwarová zařízení**

    Toto nastavení je dostupné, jenom když je *Instalace hardwarového zařízení podle identifikátorů zařízení* nastavená tak, aby *blokovala instalaci hardwarového zařízení*.
    - **Ano**
    - **Není nakonfigurováno**

  - **Blokované identifikátory hardwarových zařízení**  
    
    Toto nastavení je dostupné, jenom když je *Instalace hardwarového zařízení podle identifikátorů zařízení* nastavená tak, aby *blokovala instalaci hardwarového zařízení*.

    Vyberte **Přidat**a pak zadejte identifikátor hardwarového zařízení, který chcete blokovat.

- **Instalace hardwarových zařízení pomocí tříd instalace**  
  CSP: [DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses](https://go.microsoft.com/fwlink/?linkid=2067048)  
  
  Nastavení této zásady umožňuje zadat seznam globálně jedinečných identifikátorů (GUID) třídy nastavení zařízení pro ovladače zařízení, které systém Windows znemožňuje nainstalovat. Nastavení této zásady má přednost před jinými nastaveními zásad, která umožňují systému Windows nainstalovat zařízení. Pokud nastavení této zásady povolíte na vzdáleném počítači, nastavení zásad bude mít vliv na přesměrování zadaných zařízení z klienta vzdálené plochy na server vzdálené plochy.

  - **Není nakonfigurováno**
  - **Povolit instalaci hardwarového zařízení** – systém Windows může nainstalovat a aktualizovat zařízení podle povolených nebo zabránících jiným nastavením zásad.
  - **Zablokovat instalaci hardwarového zařízení** (*výchozí*) – systém Windows znemožní instalaci zařízení, jejichž identifikátory GUID třídy nastavení se zobrazí v seznamu, který definujete.

  Pokud je nastavená možnost *blokovat instalaci hardwarového zařízení* , můžete nakonfigurovat *Odebrání odpovídající hardwarových zařízení* a *identifikátorů hardwarových zařízení, které jsou blokované*.

  - **Odebrat shodná hardwarová zařízení**

    Toto nastavení je dostupné, jenom když je *Instalace hardwarového zařízení podle identifikátorů zařízení* nastavená tak, aby *blokovala instalaci hardwarového zařízení*.
    - **Ano**
    - **Není nakonfigurováno**

  - **Blokované identifikátory hardwarových zařízení**

    Toto nastavení je dostupné, jenom když je *Instalace hardwarového zařízení podle identifikátorů zařízení* nastavená tak, aby *blokovala instalaci hardwarového zařízení*.

    Vyberte **Přidat**a pak zadejte identifikátor hardwarového zařízení, který chcete blokovat.

## <a name="dma-guard"></a>Ochrana DMA

- **Výčet externích zařízení nekompatibilních s režimem ochrany DMA v jádře**  
  CSP: [DmaGuard/DeviceEnumerationPolicy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  Tato zásada může poskytovat další zabezpečení proti externímu zařízení podporujícím technologii DMA. Umožňuje lepší kontrolu nad výčtem externích zařízení s technologií DMA, která nejsou kompatibilní s přemapováním DMA/izolací paměti zařízení a sandboxing.
  
  Tato zásada se projeví jenom v případě, že je ochrana DMA pro jádro podporovaná a povolená systémovým firmwarem. Ochrana pomocí rozhraní DMA pro jádro je funkce platformy, kterou musí systém podporovat v době výroby. Pokud chcete zjistit, jestli systém podporuje ochranu před nejenom jádrem, na stránce Souhrn v MSINFO32.exe ověřte pole ochrana jádra DMA.

  - **Nenakonfigurováno** – (*výchozí*)
  - **Blokovat vše**
  - **Povolení všech**

## <a name="endpoint-detection-and-response"></a>Zjištění a odpověď koncového bodu

Další informace o následujících nastaveních najdete v tématu [WindowsAdvancedThreatProtection](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp) CSP v dokumentaci k systému Windows.

- **Sdílení ukázky pro všechny soubory**  
  CSP: [Configuration/SampleSharing](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Vrátí nebo nastaví parametr konfigurace sdílení ukázky rozšířené ochrany před internetovými útoky v programu Microsoft Defender.  
  
  - **Ano** (*výchozí*)
  - **Není nakonfigurováno**

- **Urychlení četnosti vytváření sestav telemetrie**  
  CSP: [Configuration/TelemetryReportingFrequency](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Urychlení generování sestav telemetrie rozšířené ochrany před internetovými útoky v programu Microsoft Defender  

  - **Ano** (*výchozí*)
  - **Není nakonfigurováno**

## <a name="firewall"></a>Firewall

Další informace najdete v dokumentaci k Windows v tématu [zprostředkovatel CSP brány firewall](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) .

- **Zakázat stavovou protokol FTP (File Transfer Protocol) (FTP)**  
  CSP: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)  

  - **Ano** (*výchozí*)
  - **Nenakonfigurováno** – brána firewall bude používat protokol FTP pro kontrolu a filtrování sekundárních síťových připojení, což by mohlo způsobit ignorování pravidel brány firewall.

- **Počet sekund, po které může být přidružení zabezpečení nečinné, než se odstraní**  
CSP: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  Zadejte, jak dlouho se přidružení zabezpečení uchovávají po skončení síťového provozu. Pokud není nakonfigurováno, systém odstraní přidružení zabezpečení poté, co je nečinné po *300* sekund (výchozí nastavení).
  
  Číslo musí být od **300** do **3600** sekund.

- **Kódování předsdíleného klíče**  
  CSP: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

   Pokud nepotřebujete UTF-8, předsdílené klíče se zpočátku zakódují pomocí kódování UTF-8. Pak uživatelé zařízení můžou zvolit jinou metodu kódování.

  - **Není nakonfigurováno**
  - **Žádný**
  - **UTF8** (*výchozí*)

- **Ověření seznamu odvolaných certifikátů (CRL)**  
  CSP: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

  Určete, jak se vynutilo ověřování seznamu odvolaných certifikátů (CRL).  

  - **Nenakonfigurováno** (*výchozí*)-ověření seznamu CRL je zakázané.
  - **Žádný**
  - **Byl**
  - **Vyžadovat**

- **Řízení front paketů**  
  CSP: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  Určete, jak se má pro daný software na straně příjmu Povolit šifrované přijímání a prostý text před scénářem brány IPsec pro tunelové připojení. Toto nastavení zajistí, aby bylo zachováno pořadí paketů.

  - **Nenakonfigurováno** (*výchozí*) – služba Packet Queuing vrátí do výchozího nastavení klienta, což je zakázané.
  - **Zakázáno**
  - **Příchozí fronta**
  - **Odchozí fronta**
  - **Zařadit do fronty**

- **Profil brány firewall Private**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067041)

  - **Konfigurace** (*výchozí*)
  - **Není nakonfigurováno**

  Po nastavení *Konfigurace*můžete nakonfigurovat následující další nastavení.

  - **Blokovaná příchozí připojení**  
    CSP: [/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Vyžadují se jednosměrové odpovědi na všesměrová vysílání vícesměrového vysílání.**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Je vyžadován neviditelný režim.**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Vyžadují se odchozí připojení.**  
    CSP: [/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Blokovaná příchozí oznámení**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Globální pravidla portů ze sloučených zásad skupiny**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Zakázaný neviditelný režim**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Povolená brána firewall**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Není nakonfigurováno**
    - **Blokované**
    - **Povoleno** (*výchozí*)

  - **Pravidla autorizovaných aplikací ze zásad skupiny nejsou sloučena.**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Pravidla zabezpečení připojení ze zásad skupiny nejsou sloučena.**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Vyžaduje se příchozí provoz**  
    CSP: [/Shielded](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Pravidla zásad ze zásad skupiny nejsou sloučena.**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

- **Veřejný profil brány firewall**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067143)

  - **Konfigurace** (*výchozí*)
  - **Není nakonfigurováno**

  Po nastavení *Konfigurace*můžete nakonfigurovat následující další nastavení.

  - **Blokovaná příchozí připojení**  
    CSP: [/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Vyžadují se jednosměrové odpovědi na všesměrová vysílání vícesměrového vysílání.**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Je vyžadován neviditelný režim.**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Vyžadují se odchozí připojení.**  
    CSP: [/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Pravidla autorizovaných aplikací ze zásad skupiny nejsou sloučena.**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Blokovaná příchozí oznámení**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Globální pravidla portů ze sloučených zásad skupiny**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Zakázaný neviditelný režim**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Povolená brána firewall**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Není nakonfigurováno**
    - **Blokované**
    - **Povoleno** (*výchozí*)

  - **Pravidla zabezpečení připojení ze zásad skupiny nejsou sloučena.**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Vyžaduje se příchozí provoz**  
    CSP: [/Shielded](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Pravidla zásad ze zásad skupiny nejsou sloučena.**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

- **Doména profilu brány firewall**  
  CSP: [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2066796)

  - **Vyžadují se jednosměrové odpovědi na všesměrová vysílání vícesměrového vysílání.**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

  - **Pravidla autorizovaných aplikací ze zásad skupiny nejsou sloučena.**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**  

  - **Blokovaná příchozí oznámení**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Globální pravidla portů ze sloučených zásad skupiny**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Zakázaný neviditelný režim**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Povolená brána firewall**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Není nakonfigurováno**
    - **Blokované**
    - **Povoleno** (*výchozí*)

  - **Pravidla zabezpečení připojení ze zásad skupiny nejsou sloučena.**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

  - **Pravidla zásad ze zásad skupiny nejsou sloučena.**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Ano** (*výchozí*)
    - **Není nakonfigurováno**

## <a name="microsoft-defender"></a>Microsoft Defender

- **Spustit každodenní rychlou kontrolu v**  
  CSP: [Defender/ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053&clcid=0x409)
  
   Nakonfigurujte čas, kdy se každodenní Rychlá kontrola spouští. Ve výchozím nastavení je spuštění skenování nastaveno na **2 dop**.

- **Čas zahájení naplánované kontroly**  
  
  Ve výchozím nastavení je tato hodnota nastavená na **2 dop**.

- **Konfigurace nízké priority procesoru pro naplánovaná prohledávání**  
  CSP: [Defender/EnableLowCPUPriority](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority)  

  -**Ano** (*výchozí*)
  - **Není nakonfigurováno**

- **Blokování aplikací pro komunikaci Office z vytváření podřízených procesů**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=874499)  

  Toto pravidlo ASR se řídí pomocí následujícího identifikátoru GUID: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **Nenakonfigurováno** – obnoví se výchozí nastavení systému Windows, které neblokuje vytváření podřízených procesů.
  - **Definováno uživatelem**
  - **Povolit** (*výchozí*) – komunikační aplikace Office jsou blokované pro vytváření podřízených procesů.
  - **Režim auditu** – místo blokování podřízených procesů jsou vyvolány události systému Windows.

- **Blokovat Adobe Reader v vytváření podřízených procesů**  
  [Omezení ploch útoku pomocí pravidel pro omezení možností útoku](https://go.microsoft.com/fwlink/?linkid=853979)  

  - **Nenakonfigurováno** – obnoví se výchozí nastavení systému Windows, není blokováno vytváření podřízených procesů.
  - **Definováno uživatelem**
  - **Povolit** (*výchozí*) – Adobe Reader se zablokuje při vytváření podřízených procesů.
  - **Režim auditu** – místo blokování podřízených procesů jsou vyvolány události systému Windows.

- **Kontrolovat příchozí e-mailové zprávy**  
  CSP: [Defender/AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052&clcid=0x409)

  - **Ano** (*výchozí*) – prohledají se e-mailové poštovní schránky a poštovní soubory, například PST, dbx, mnx, MIME a BinHex.
  - **Nenakonfigurováno** – nastavení se vrátí k výchozímu nastavení klienta e-mailových souborů, které nejsou prohledávány.

- **Zapnout ochranu v reálném čase**  
  CSP: [Defender/AllowRealtimeMonitoring](https://go.microsoft.com/fwlink/?linkid=2114050&clcid=0x409)

  - **Ano** (*výchozí*) – vynutilo se monitorování v reálném čase a uživatel ho nemůže zakázat.
  - **Nenakonfigurováno** – nastavení se vrátí do výchozího nastavení klienta, které je zapnuté, ale uživatel ho může změnit. Pokud chcete zakázat monitorování v reálném čase, použijte vlastní identifikátor URI.

- **Počet dní (0-90) pro udržení malwaru v karanténě**  
  CSP: [Defender/DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055&clcid=0x409)

  Nakonfigurujte počet dní, po které se mají položky uchovávat ve složce karantény, než se odeberou. Výchozí hodnota je nula (**0**), což vede k tomu, že se soubory v karanténě nikdy neodstraňují.

- **Plán kontroly systémových úloh Defenderu**  
  CSP: [Defender/ScheduleScanDay](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)

  Naplánujte, který den v Defenderu prohledává zařízení. Ve výchozím nastavení je vyhledávání **definováno uživatelem** , ale může být nastaveno *na každý den v týdnu*nebo na možnost *bez naplánovaného prohledávání*.

- **Dodatečné množství času (0-50 sekund) pro prodloužení časového limitu ochrany cloudu**  
  CSP: [Defender/CloudExtendedTimeout](https://go.microsoft.com/fwlink/?linkid=2113940&clcid=0x409)

  Antivirová ochrana automaticky blokuje podezřelé soubory po dobu 10 sekund, takže může zkontrolovat soubory v cloudu a ujistit se, že jsou bezpečné. Pomocí tohoto nastavení můžete tomuto časovému limitu přidat až 50 dalších sekund.  Ve výchozím nastavení je časový limit nastaven na hodnotu nula (**0**).

- **Při úplné kontrole kontrolovat namapované síťové jednotky**  
  CSP: [Defender/AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945&clcid=0x409)

  - **Ano** (*výchozí*) – při úplné kontrole jsou zahrnuty mapované síťové jednotky.
  - **Nenakonfigurováno** – klient se vrátí k výchozímu, což zakáže kontrolu mapovaných síťových jednotek.

- **Zapnout ochranu sítě**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939&clcid=0x409)
  
  - **Ano** (*výchozí*) – blokování škodlivých přenosů zjištěných signaturami ve službě systém kontroly sítě (NIS).
  - **Není nakonfigurováno**

- **Prohledat všechny stažené soubory a přílohy**  
  CSP: [Defender/AllowIOAVProtection](https://go.microsoft.com/fwlink/?linkid=2113934&clcid=0x409)

  - **Ano** (*výchozí*) – prohledají se všechny stažené soubory a přílohy. Nastavení se vrátí do výchozího nastavení klienta, které je zapnuté, ale uživatel ho může změnit. Pokud chcete toto nastavení zakázat, použijte vlastní identifikátor URI.
  - **Nenakonfigurováno** – nastavení se vrátí do výchozího nastavení klienta, které je zapnuté, ale uživatel ho může změnit. Pokud chcete toto nastavení zakázat, použijte vlastní identifikátor URI.

::: zone-end
::: zone pivot="atp-april-2020"

- **Blokovat ochranu přístupu**  
  CSP: [Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **Ano**
  - **Nenakonfigurováno** (*výchozí*)

::: zone-end
::: zone pivot="atp-march-2020"

- **Blokovat ochranu přístupu**  
  CSP: [Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **Ano** (*výchozí*)
  - **Není nakonfigurováno**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Kontrolovat skripty v prohlížeči**  
  CSP: [Defender/AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054&clcid=0x409)

  - **Ano** (*výchozí*) – vynutila se funkce kontroly skriptů v programu Microsoft Defender a uživatel je nemůže vypnout.
  - **Nenakonfigurováno** – nastavení se vrátí do výchozího nastavení klienta, což znamená povolit kontrolu skriptů, ale uživatel ho může vypnout.

- **Zablokovat přístup uživatelů k aplikaci Microsoft Defender**  
  CSP: [Defender/AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043&clcid=0x409)

  - **Ano** (*výchozí*) – uživatelské rozhraní (UI) programu Microsoft Defender je nedostupné a oznámení jsou překvapena
  - **Není nakonfigurováno** Pokud nastavíte Ano, uživatelské rozhraní (UI) programu Windows Defender nebude dostupné a oznámení budou překvapena. Pokud je nastavené na Nenakonfigurováno, nastavení se vrátí do výchozího nastavení klienta, ve kterém bude uživatelské rozhraní a oznámení povolené.

- **Maximální povolené využití CPU (0-100 procent) na jednu kontrolu**  
  CSP: [Defender/AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046&clcid=0x409)

  Zadejte procento maximálního počtu PROCESORů, které se má pro kontrolu použít. Výchozí hodnota je **50**.

- **Typ kontroly**  
  CSP: [Defender/ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045&clcid=0x409)

  - **Definováno uživatelem**
  - **Zakázáno**
  - **Rychlá kontrola** (*výchozí*)
  - **Úplná kontrola**

- **Zadejte, jak často (0-24 hodin) se mají kontrolovat aktualizace služby Security Intelligence.**  
  CSP: [Defender/SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936&clcid=0x409)

  Určete, jak často se mají kontrolovat aktualizované podpisy v hodinách. Například hodnota 1 bude kontrolovat každou hodinu. Hodnota 2 bude kontrolovat každé dvě hodiny atd.

  Pokud není definovaná žádná hodnota, zařízení použije výchozí nastavení klienta na **8** hodin.

- **Souhlas s odesláním ukázky v programu Defender**  
  CSP: [Defender/SubmitSamplesConsent](https://go.microsoft.com/fwlink/?linkid=2067131)

  Kontroluje, jestli se na úrovni souhlasu uživatele v programu Microsoft Defender odesílají data. Pokud je požadovaný souhlas již udělen, Microsoft Defender je odešle. Pokud ne (a pokud si uživatel není nikdy požádán), uživatelské rozhraní se spustí, aby požádalo o souhlas uživatele (při nastavení ochrany před odesláním *cloudu* na *Ano*).

  - **Posílat bezpečné vzorky automaticky** (*výchozí*)
  - **Vždycky se zeptat**
  - **Nikdy Neodesílat**
  - **Posílat všechny vzorky automaticky**

- **Úroveň ochrany v cloudu**  
  CSP: [CloudBlockLevel](https://go.microsoft.com/fwlink/?linkid=2113942)

  Nakonfigurujte, jak agresivní antivirová antivirová ochrana blokuje a kontroluje podezřelé soubory.
  - **Nenakonfigurováno** (*výchozí*) – výchozí úroveň blokování v programu Defender.
  - **Vysoce** agresivní blokování neznámých během optimalizace výkonu klienta, což zahrnuje větší šanci falešně pozitivních hodnot.
  - **Vysoké plus** – neznámy neznámé a používají další ochranné míry, které by mohly mít vliv na výkon klienta.
  - **Nulová tolerance** – zablokuje všechny neznámé spustitelné soubory.

- **Prohledat archivní soubory**  
  CSP: [Defender/AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047&clcid=0x409)

  - **Ano** (*výchozí*) – vynutila se kontrola souborů archivu, jako jsou soubory ZIP nebo CAB.
  - **Nenakonfigurováno** – nastavení se vrátí zpátky do výchozího nastavení klienta, což znamená skenování archivovaných souborů, ale uživatel může kontrolu zakázat.

- **Zapnout monitorování chování**  
  CSP: [Defender/AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048&clcid=0x409)

  - **Ano** (*výchozí*) – vynutilo se monitorování chování a uživatel ho nemůže zakázat.
  - **Nenakonfigurováno** – nastavení se vrátí do výchozího nastavení klienta, které je zapnuté, ale uživatel ho může změnit. Pokud chcete zakázat monitorování v reálném čase, použijte vlastní identifikátor URI.
  
- **Kontrolovat vyměnitelné jednotky při úplné kontrole**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946&clcid=0x409)

  - **Ano** (*výchozí*) – při úplné kontrole se prohledají vyměnitelné jednotky (například jednotky USB Flash).
  - **Nenakonfigurováno** – nastavení se vrátí do výchozího nastavení klienta, které kontroluje vyměnitelné jednotky, ale uživatel může tuto kontrolu zakázat.
  
- **Prohledat síťové soubory**  
  CSP: [Defender/AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&clcid=0x409)

  - **Ano** (*výchozí*) – Microsoft Defender prohledává síťové soubory.
  - **Nenakonfigurováno** – klient se vrátí k výchozímu, což zakáže kontrolu síťových souborů.
  
- **Akce potenciálně nežádoucí aplikace v Defenderu**  
  CSP: [Defender/PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

  Zadejte úroveň detekce potenciálně nežádoucích aplikací (PUAs). Program Defender upozorní uživatele, když se stahuje potenciálně nežádoucí software nebo se pokouší o instalaci na zařízení.
  - **Výchozí ze zařízení**
  - **Blok** (*výchozí*) – zjištěné položky jsou blokované a zobrazují se v historii spolu s dalšími hrozbami.
  - **Audit** -Defender detekuje potenciálně nežádoucí aplikace, ale neprovede žádnou akci. Můžete zkontrolovat informace o aplikacích, které Defender přijal, pomocí hledání událostí, které vytvořil Defender v Prohlížeč událostí.

- **Zapnutí ochrany poskytované cloudem**  
  CSP: [AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Ve výchozím nastavení Defender v zařízeních s Windows 10 Desktop odesílá společnosti Microsoft informace o případných problémech, které najde. Microsoft analyzuje tyto informace, aby se dozvěděly Další informace o problémech, které se týkají vás a dalších zákazníků, a nabízí Vylepšená řešení.

  - **Ano** (*výchozí*) – je zapnutá ochrana s doručováním cloudu.  Uživatelé zařízení nemůžou toto nastavení změnit.
  - **Nenakonfigurováno**  – nastavení se obnoví do výchozího nastavení systému.

- **Blokovat aplikacím Office vkládání kódu do jiných procesů**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=872974)

  Toto pravidlo ASR se ovládá pomocí následujícího identifikátoru GUID: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **Nenakonfigurováno** – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - **Blok** (*výchozí*) – aplikace Office jsou blokované pro vkládání kódu do jiných procesů.
  - **Režim auditu** – místo blokování se vyvolají události systému Windows.

- **Blokovat aplikacím Office vytváření spustitelného obsahu**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=872975)

  Toto pravidlo ASR se řídí pomocí následujícího identifikátoru GUID: 3B576869-A4EC-4529-8536-B80A7769E899
  - **Nenakonfigurováno** – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - **Blok** (*výchozí*) – aplikace Office jsou blokované z vytváření spustitelného obsahu.
  - **Režim auditu** – místo blokování se vyvolají události systému Windows.
  
- **Blokování spouštění staženého spustitelného obsahu pomocí JavaScriptu nebo VBScript**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=872979)

   Toto pravidlo ASR se ovládá pomocí následujícího identifikátoru GUID: D3E037E1-3EB8-44C8-A917-57927947596D
  - **Nenakonfigurováno** – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - **Blok** (*výchozí*) – Defender blokuje soubory JavaScript nebo VBScript stažené z Internetu ze spouštění.
  - **Režim auditu** – místo blokování se vyvolají události systému Windows.
  
- **Povolit ochranu sítě**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **Nenakonfigurováno** – nastavení se vrátí k výchozímu systému Windows, který je zakázaný.
  - **Definováno uživatelem**
  - **Povolit** – Ochrana sítě je povolená pro všechny uživatele systému.
  - **Režim auditování** (*výchozí*) – uživatelé nejsou zablokovaných z nebezpečných domén a místo toho se vyvolají události Windows.

- **Zablokovat nedůvěryhodné a nepodepsané procesy, které se spouštějí z USB**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=874502)

  Toto pravidlo ASR se ovládá pomocí následujícího identifikátoru GUID: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **Nenakonfigurováno** – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - **Blokovat** (*výchozí*) – nedůvěryhodné a nepodepsané procesy, které se spouštějí z USB jednotky, jsou blokovány.
  - **Režim auditu** – místo blokování se vyvolají události systému Windows.

- **Blokovat odcizení přihlašovacích údajů ze subsystému místního úřadu zabezpečení systému Windows (lsass.exe)**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=874499)

  Toto pravidlo ASR se ovládá pomocí následujícího identifikátoru GUID: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **Nenakonfigurováno** – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - **Definováno uživatelem**
  - **Povolit** (*výchozí*) – pokusy o odcizení přihlašovacích údajů prostřednictvím lsass.exe jsou blokované.
  - **Režim auditu** – uživatelé nejsou zablokovaných z nebezpečných domén a místo toho se vyvolají události Windows.

- **Blokovat stahování spustitelného obsahu z e-mailu a klientů webové pošty**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=872980)

  - **Nenakonfigurováno** – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - **Blokovat** (*výchozí*) – spustitelný obsah stažený z e-mailu a klientů webmailu je blokovaný.
  - **Režim auditu** – místo blokování se vyvolají události systému Windows.

- **Zablokovat všechny aplikace Office z vytváření podřízených procesů**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=872976)

  Toto pravidlo ASR se ovládá pomocí následujícího identifikátoru GUID: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **Nenakonfigurováno** – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - **Blok** (*výchozí*)
  - **Režim auditu** – místo blokování se vyvolají události systému Windows.

- **Zablokovat provádění potenciálně zablokovaných skriptů (js/vbs/PS)**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=872978)

  Toto pravidlo ASR se ovládá pomocí následujícího identifikátoru GUID: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **Nenakonfigurováno** – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - **Blok** (*výchozí*) – Defender bude blokovat provádění zavedených skriptů.
  - **Režim auditu** – místo blokování se vyvolají události systému Windows.

- **Blokování volání Win32 API z makra Office**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=872977)

  Toto pravidlo ASR se řídí pomocí následujícího identifikátoru GUID: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **Nenakonfigurováno** – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - **Blok** (*výchozí*) – pro makro Office se zablokuje použití volání Win32 API.
  - **Režim auditu** – místo blokování se vyvolají události systému Windows.

## <a name="microsoft-defender-security-center"></a>Security Center programu Microsoft Defender

- **Zablokuje uživatelům úpravy rozhraní zneužití ochrany před zneužitím.**  
  CSP: [WindowsDefenderSecurityCenter/DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **Ano** (*výchozí*) – zabrání uživatelům v provádění změn v oblasti nastavení ochrany před zneužitím v programu Microsoft Defender Security Center.
  - **Nenakonfigurováno** – místní uživatelé mohou provádět změny v oblasti nastavení ochrany před zneužitím.

## <a name="smart-screen"></a>Inteligentní obrazovka

- **Zablokovat uživatelům ignorovat upozornění filtru SmartScreen**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

   Toto nastavení vyžaduje, aby se nastavení zapnout filtr SmartScreen pro Windows nastavilo na Ano.
  - **Ano** (*výchozí*) – filtr SmartScreen je povolen a uživatelé nemohou obejít upozornění na soubory nebo škodlivé aplikace.
  - **Nenakonfigurováno** – uživatelé můžou ignorovat upozornění filtru SmartScreen pro soubory a škodlivé aplikace.

- **Vyžadovat pouze aplikace ze Storu**  

  - **Ano** (*výchozí*)
  - **Není nakonfigurováno**

- **Zapnout filtr Windows SmartScreen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **Ano** (*výchozí*) – vynutilo použití filtru SmartScreen pro všechny uživatele.
  - **Nenakonfigurováno** – vrátí nastavení do výchozího nastavení systému Windows, což znamená Povolit filtr SmartScreen, ale uživatelé můžou toto nastavení změnit. Chcete-li zakázat filtr SmartScreen, použijte vlastní identifikátor URI.

## <a name="windows-hello-for-business"></a>Windows Hello pro firmy

Další informace najdete v tématu [PASSPORTFORWORK CSP](https://docs.microsoft.com/windows/client-management/mdm/passportforwork-csp) v dokumentaci k systému Windows.

- **Blokovat Windows Hello pro firmy**  

   Windows Hello pro firmy je alternativní metoda pro přihlašování do systému Windows tím, že nahrazujete hesla, čipové karty a virtuální čipové karty.

  - **Nenakonfigurováno** – zařízení, která používají Windows Hello pro firmy, je ve výchozím nastavení Windows.
  - **Zakázáno** (*výchozí*) – zařízení zřídí Windows Hello pro firmy.
  - **Povoleno** – zařízení nezřídí pro žádného uživatele Windows Hello pro firmy.

  Pokud je nastavené na *zakázáno*, můžete nakonfigurovat následující nastavení:

  - **Malá písmena v PIN kódu**  
    - **Není povoleno**
    - **Požadováno**
    - **Povoleno** (*výchozí*)

  - **Speciální znaky v PIN kódu**
    - **Není povoleno**
    - **Požadováno**
    - **Povoleno** (*výchozí*)

  - **Velká písmena v PIN kódu**
    - **Není povoleno**
    - **Požadováno**
    - **Povoleno** (*výchozí*)

::: zone-end

## <a name="next-steps"></a>Další kroky

- [Další informace o standardních hodnotách zabezpečení](security-baselines.md)
- [Vyhnout se konfliktům](security-baselines.md#avoid-conflicts)
- [Řešení potíží se zásadami a profily v Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)