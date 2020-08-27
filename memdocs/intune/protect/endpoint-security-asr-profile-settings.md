---
title: Nastavení omezení plochy pro útok na zabezpečení koncového bodu Intune | Microsoft Docs
description: Nastavení zásad omezení pro omezení zabezpečení koncového bodu v Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/11/2020
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
ms.openlocfilehash: a2b404e1741c93a6dbf5023f394f3b9528020617
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913456"
---
# <a name="attack-surface-reduction-policy-settings-for-endpoint-security-in-intune"></a>Nastavení zásad pro omezení možností útoku pro zabezpečení koncového bodu v Intune

Podívejte se na nastavení, která můžete nakonfigurovat v části profily pro zásady *omezení možností útoku* v uzlu zabezpečení koncového bodu služby Intune jako součást [zásad zabezpečení koncového bodu](../protect/endpoint-security-policy.md).

Podporované platformy a profily:

- **Windows 10 a novější**:
  - Profil: **izolace aplikace a prohlížeče**
  - Profil: **ochrana webu**
  - Profil: **řízení aplikací**
  - Profil: **pravidla pro omezení možností útoku**
  - Profil: **ovládací prvek zařízení**
  - Profil: **zneužití ochrany**

## <a name="app-and-browser-isolation-profile"></a>Profil izolace aplikace a prohlížeče

### <a name="app-and-browser-isolation"></a>Izolace aplikací a prohlížečů

- **Zapnout ochranu Application Guard pro Edge (možnosti)**  
  CSP: [AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)

  - **Nenakonfigurováno** (*výchozí*)
  - **Povoleno pro funkci Edge** -Application Guard otevře neschválené weby v kontejneru procházení virtualizovaného pomocí technologie Hyper-V.

  Když je nastavená možnost *Povolit pro Edge*, jsou k dispozici následující nastavení:
  
  - **Chování schránky**  
    CSP: [ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    Vyberte, které akce kopírování a vkládání jsou povoleny v místním počítači a ve virtuálním prohlížeči ochrany Application Guard.
    - **Nenakonfigurováno** (*výchozí*)
    - **Blokovat kopírování a vkládání mezi počítačem a prohlížečem**
    - **Povoluje kopírování a vkládání jenom z prohlížeče na počítač.**
    - **Povolí kopírování a vkládání jenom z počítačů do prohlížeče.**
    - **Povolí kopírování a vkládání mezi počítačem a prohlížečem.**

  - **Zablokovat externí obsah od nepodnikových lokalit, které byly schváleny**  
    CSP: [BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **Nenakonfigurováno** (*výchozí*)
    - **Ano** – zablokuje načítání obsahu z neschválených webů.

  - **Shromažďovat protokoly pro události, ke kterým dojde v relaci procházení ochrany Application Guard**  
    CSP: [AuditApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872418)

    - **Nenakonfigurováno** (*výchozí*)
    - **Ano** – shromáždí protokoly pro události, ke kterým dojde v rámci virtuální relace procházení ochrany Application Guard.

  - **Povolí ukládání dat prohlížeče generovaných uživatelem.**  
    CSP: [AllowPersistence](https://go.microsoft.com/fwlink/?linkid=872419)

    - **Nenakonfigurováno** (*výchozí*)
    - **Ano** – povolí ukládání uživatelských dat, která se vytvoří během virtuální relace procházení ochrany Application Guard. Mezi příklady uživatelských dat patří hesla, oblíbené položky a soubory cookie.

  - **Povolit hardwarovou akceleraci grafiky**  
    CSP: [AllowVirtualGPU](https://go.microsoft.com/fwlink/?linkid=872420)

    - **Nenakonfigurováno** (*výchozí*)
    - **Ano** – v rámci relace virtuálního procházení ochrany Application Guard použijte virtuální grafický procesor, abyste rychleji načetli weby náročné na grafiku.

  - **Dovolit uživatelům stahovat soubory na hostitele**  
    CSP: [SaveFilesToHost](https://go.microsoft.com/fwlink/?linkid=872421)

    - **Nenakonfigurováno** (*výchozí*)
    - **Ano** – umožní uživatelům stahovat soubory z virtualizovaného prohlížeče do hostitelského operačního systému.

- **Ochrana Application Guard povoluje tisk na místních tiskárnách**  

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano** – povolí tisk na místních tiskárnách.

- **Ochrana Application Guard povoluje tisk na síťových tiskárnách**  

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano** – povoluje tisk tisku na síťové tiskárny.

- **Ochrana Application Guard povoluje tisk do PDF**  

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano**– povoluje tisk tisku do PDF.

- **Ochrana Application Guard povoluje tisk do XPS**  

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano** – povolí tisk tisku do XPS.

- **Zásady izolace sítě systému Windows**  
  
  - **Nenakonfigurováno** (*výchozí*)
  - **Ano** – nakonfigurujte zásady izolace sítě systému Windows.  
  
  Pokud nastavíte *Ano*, můžete nakonfigurovat následující nastavení.

  - **Rozsahy IP adres**  
    Rozbalte rozevírací seznam, vyberte **Přidat**a potom zadejte *nižší adresu* a pak *horní adresu*.

  - **Cloudové prostředky**  
    Rozbalte rozevírací seznam, vyberte možnost **Přidat**a poté zadejte *IP adresu nebo plně kvalifikovaný název domény* a *proxy server*.

  - **Síťové domény**  
   Rozbalte rozevírací seznam, vyberte **Přidat**a pak zadejte *síťové domény*.

  - **Proxy servery**  
    Rozbalte rozevírací seznam, vyberte **Přidat**a pak zadejte *proxy servery*.

  - **Interní proxy servery**  
    Rozbalte rozevírací seznam, vyberte **Přidat**a pak zadejte *interní proxy servery*.

  - **Neutrální prostředky**  
    Rozbalte rozevírací seznam, vyberte **Přidat**a pak zadejte *neutrální prostředky*.

  - **Zakázat automatickou detekci dalších podnikových proxy serverů**  
    - **Nenakonfigurováno** (*výchozí*)
    - **Ano** – zakáže automatickou detekci dalších podnikových proxy serverů.

  - **Zakázat automatickou detekci dalších podnikových IP adres**  
    - **Nenakonfigurováno** (*výchozí*)
    - **Ano** – zakáže automatickou detekci dalších PODNIKových IP adres.

## <a name="web-protection-profile"></a>Profil webové ochrany

### <a name="web-protection"></a>Ochrana webu

- **Povolit ochranu sítě**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího systému Windows, který je zakázaný.
  - **Definováno uživatelem**
  - **Povolit** – Ochrana sítě je povolená pro všechny uživatele systému.
  - **Režim auditu** – uživatelé nejsou zablokovaných z nebezpečných domén a místo toho se vyvolají události Windows.

- **Vyžadovat filtr SmartScreen pro Microsoft Edge**  
  CSP: [browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **Ano** – pomocí filtru SmartScreen ochráníte uživatele před potenciálními podvodnými zprávami a škodlivým softwarem.
  - **Nenakonfigurováno** (*výchozí*)

- **Blokovat přístup ke škodlivému webu**  
  CSP: [browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **Ano** – zablokuje uživatelům ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a zablokuje jejich přesun na web.
  - **Nenakonfigurováno** (*výchozí*)

- **Blokovat stahování neověřených souborů**  
  CSP: [browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **Ano** – zablokuje uživatelům ignorovat upozornění filtru SmartScreen v programu Microsoft Defender a zablokuje stahování neověřených souborů.
  - **Nenakonfigurováno** (*výchozí*)

## <a name="application-control-profile"></a>Profil řízení aplikací

### <a name="microsoft-defender-application-control"></a>Řízení aplikací v programu Microsoft Defender

- **Řízení aplikací v aplikaci Locker**  
  CSP: [AppLocker](/windows/client-management/mdm/applocker-csp)

  - **Nenakonfigurováno** (*výchozí*)
  - **Vynutilit komponenty a aplikace ze Storu**
  - **Komponenty auditu a aplikace pro Store**
  - **Vynutilit komponenty, aplikace pro Store a Smartlocker**
  - **Auditovat komponenty, aplikace pro Store a Smartlocker**
   

- **Zablokovat uživatelům ignorovat upozornění filtru SmartScreen**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

  - **Nenakonfigurováno** (*výchozí*) – uživatelé můžou ignorovat upozornění filtru SmartScreen pro soubory a škodlivé aplikace.
  - **Ano** – filtr SmartScreen je povolen a uživatelé nemohou obejít upozornění na soubory nebo škodlivé aplikace.

- **Zapnout filtr Windows SmartScreen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **Nenakonfigurováno** (*výchozí*) – vrátí nastavení výchozí nastavení systému Windows, které povoluje filtr SmartScreen, ale uživatelé můžou toto nastavení změnit. Chcete-li zakázat filtr SmartScreen, použijte vlastní identifikátor URI.
  - **Ano** – vynutilo použití filtru SmartScreen pro všechny uživatele.

## <a name="attack-surface-reduction-rules-profile"></a>Profil pravidel pro omezení možností útoku

### <a name="attack-surface-reduction-rules"></a>Pravidla pro omezení možností útoku

- **Blokovat odcizení přihlašovacích údajů ze subsystému místního úřadu zabezpečení systému Windows (lsass.exe)**  
  <!-- Defender ATP security baseline, Device configuration Endpoint protection profile -->
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=874499)

  Toto pravidlo pro omezení možností útoku (ASR) se řídí pomocí tohoto identifikátoru GUID: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - **Definováno uživatelem**
  - **Povolit** – pokusy o odcizení přihlašovacích údajů prostřednictvím lsass.exe jsou blokované.
  - **Režim auditu** – uživatelé nejsou zablokovaných z nebezpečných domén a místo toho se vyvolají události Windows.

- **Blokovat Adobe Reader v vytváření podřízených procesů**  
  [Omezení ploch útoku pomocí pravidel pro omezení možností útoku](https://go.microsoft.com/fwlink/?linkid=853979)
  
  Toto pravidlo ASR se ovládá pomocí následujícího identifikátoru GUID: 7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c
  - **Nenakonfigurováno** (*výchozí*) – obnoví se výchozí nastavení systému Windows, není blokováno vytváření podřízených procesů.
  - **Definováno uživatelem**
  - **Povolit** – Adobe Reader je blokováno při vytváření podřízených procesů.
  - **Režim auditu** – místo blokování podřízených procesů jsou vyvolány události systému Windows.

- **Blokovat aplikacím Office vkládání kódu do jiných procesů**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=872974)

  Toto pravidlo ASR se ovládá pomocí následujícího identifikátoru GUID: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - **Blokové** aplikace sady Office zablokují vkládání kódu do jiných procesů.
  - **Režim auditu** – místo blokování se vyvolají události systému Windows.

- **Blokovat aplikacím Office vytváření spustitelného obsahu**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=872975)

  Toto pravidlo ASR se řídí pomocí následujícího identifikátoru GUID: 3B576869-A4EC-4529-8536-B80A7769E899
  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - **Blokování** aplikací pro Office je zablokované pro vytváření spustitelného obsahu.
  - **Režim auditu** – místo blokování se vyvolají události systému Windows.

- **Zablokovat všechny aplikace Office z vytváření podřízených procesů**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=872976)

  Toto pravidlo ASR se ovládá pomocí následujícího identifikátoru GUID: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - **Blokování** aplikací pro Office je zablokované pro vytváření podřízených procesů.
  - **Režim auditu** – místo blokování se vyvolají události systému Windows.

- **Blokování volání Win32 API z makra Office**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=872977)

  Toto pravidlo ASR se řídí pomocí následujícího identifikátoru GUID: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - **Blok**  -makro sady Office je blokováno pomocí Win32 API volání.
  - **Režim auditu** – místo blokování se vyvolají události systému Windows.

- **Blokování aplikací pro komunikaci Office z vytváření podřízených procesů**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=874499)  

  Toto pravidlo ASR se řídí pomocí následujícího identifikátoru GUID: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **Nenakonfigurováno** (*výchozí*) – obnoví se výchozí nastavení systému Windows, které neblokuje vytváření podřízených procesů.
  - **Definováno uživatelem**
  - **Povolit** – komunikační aplikace Office se blokují při vytváření podřízených procesů.
  - **Režim auditu** – místo blokování podřízených procesů jsou vyvolány události systému Windows.

- **Zablokovat provádění potenciálně zablokovaných skriptů (js/vbs/PS)**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=872978)

  Toto pravidlo ASR se ovládá pomocí následujícího identifikátoru GUID: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - **Blok** -Defender blokuje provádění zadefinovaných skriptů.
  - **Režim auditu** – místo blokování se vyvolají události systému Windows.

- **Blokování spouštění staženého spustitelného obsahu pomocí JavaScriptu nebo VBScript**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=872979)

   Toto pravidlo ASR se ovládá pomocí následujícího identifikátoru GUID: D3E037E1-3EB8-44C8-A917-57927947596D
  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - **Blok** -Defender blokuje soubory JavaScript nebo VBScript, které byly staženy z Internetu ze spouštění.
  - **Režim auditu** – místo blokování se vyvolají události systému Windows.

- **Blokovat vytváření procesů, které pocházejí z příkazů PSExec a WMI**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=874500)

  Toto pravidlo ASR se ovládá pomocí následujícího identifikátoru GUID: d1e49aac-8F56-4280-b9ba-993a6d77406c
  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - Vytváření **blokových** procesů pomocí příkazů PsExec nebo WMI je blokováno.
  - **Režim auditu** – místo blokování se vyvolají události systému Windows.

- **Zablokovat nedůvěryhodné a nepodepsané procesy, které se spouštějí z USB**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=874502)

  Toto pravidlo ASR se ovládá pomocí následujícího identifikátoru GUID: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - **Zablokují** se nedůvěryhodné a nepodepsané procesy, které se SPOUŠTĚJÍ z USB jednotky.
  - **Režim auditu** – místo blokování se vyvolají události systému Windows.

- **Zablokovat spouštění spustitelných souborů, pokud nesplňují kritéria prevalence, stáří nebo seznamu důvěryhodných souborů**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=874503)

  Toto pravidlo ASR se řídí pomocí následujícího identifikátoru GUID: 01443614-cd74-433a-b99e-2ecdc07bfc25e
  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - **Blok**
  - **Režim auditu** – místo blokování se vyvolají události systému Windows.

- **Blokovat stahování spustitelného obsahu z e-mailu a klientů webové pošty**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=872980)

  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - **Blokování** spustitelného obsahu z e-mailu a klientů webové pošty je blokované.
  - **Režim auditu** – místo blokování se vyvolají události systému Windows.

- **Použití rozšířené ochrany proti ransomwarem**  
   [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=874504)

  Toto pravidlo ASR se řídí pomocí následujícího identifikátoru GUID: c1db55ab-c21a-4637-bb3f-a12568109d35
  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení systému Windows, které je vypnuté.
  - **Definováno uživatelem**
  - **Povolení**
  - **Režim auditu** – místo blokování se vyvolají události Windows.

- **Povolit ochranu složky**  
  CSP: [EnableControlledFolderAccess](https://go.microsoft.com/fwlink/?linkid=872614)

  - **Nenakonfigurováno** (*výchozí*) – Toto nastavení se vrátí do výchozího, což není zablokované čtení nebo zápisy.
  - **Povolit** – pro nedůvěryhodné aplikace se v programu Defender pokusy o změnu nebo odstranění souborů v chráněných složkách nebo zápis do sektorů disku. Defender automaticky určuje, které aplikace mohou být důvěryhodné. Případně můžete definovat vlastní seznam důvěryhodných aplikací.
  - **Režim auditu** – události systému Windows jsou vyvolány, když se nedůvěryhodné aplikace přistupují ke složkám řízeným přístupem, ale žádné bloky se neuplatňují.
  - **Blokovat úpravu disku** – zablokují se jenom pokusy o zápis do sektorů disku.
  - **Auditovat úpravu disku** – jsou vyvolány události Windows namísto blokování pokusů o zápis do sektorů disku.
  
- **Vyloučit soubory a cesty z pravidel pro omezení možností útoku**  
  CSP: [AttackSurfaceReductionOnlyExclusions](https://go.microsoft.com/fwlink/?linkid=872981)

  Rozbalte rozevírací seznam a pak vyberte **Přidat** a definujte **cestu** k souboru nebo složce, které se mají vyloučit z pravidel pro omezení možností útoku.

## <a name="device-control-profile"></a>Řídicí profil zařízení

### <a name="device-control"></a>Řízení zařízení

- **Instalace hardwarových zařízení podle identifikátorů zařízení**  
  [PreventInstallationOfMatchingDeviceIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  Toto nastavení umožňuje určit seznam technologie Plug and Play ID hardwaru a kompatibilní ID pro zařízení, na která systém Windows znemožňuje instalaci. Nastavení této zásady má přednost před jinými nastaveními zásad, která umožňují systému Windows nainstalovat zařízení.  Pokud nastavení této zásady povolíte na vzdáleném počítači, nastavení zásad bude mít vliv na přesměrování zadaných zařízení z klienta vzdálené plochy na server vzdálené plochy.

  - **Není nakonfigurováno**
  - **Povolit instalaci hardwarového zařízení** – zařízení je možné nainstalovat a aktualizovat tak, aby byla povolená nebo zabrání jiným nastavením zásad.
  - **Blokovat instalaci hardwarového zařízení** (*výchozí*) – systému Windows se znemožní nainstalovat zařízení, jehož ID hardwaru nebo kompatibilní ID se zobrazí v seznamu, který definujete.

  Pokud je nastavená možnost *blokovat instalaci hardwarového zařízení* , můžete nakonfigurovat následující nastavení:

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

- **Kontrolovat vyměnitelné jednotky při úplné kontrole**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946)

  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení klienta, které kontroluje vyměnitelné jednotky, ale uživatel může tuto kontrolu zakázat.
  - **Ano** – při úplné kontrole se prohledají vyměnitelné jednotky (například jednotky USB Flash).

- **Zablokovat přímý přístup do paměti**  
  CSP: [DataProtection/AllowDirectMemoryAccess](https://go.microsoft.com/fwlink/?linkid=2067031)

  Nastavení této zásady se vynutilo jenom v případě, že je povolené BitLocker nebo šifrování zařízení.

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano** – zablokuje přímý přístup do paměti (DMA) pro všechny bezplatných portů PCI pro příjem dat, dokud se uživatel do Windows nepřihlásí. Jakmile se uživatel přihlásí, systém Windows zobrazí zařízení PCI připojená k portům plug-in hostitele. Pokaždé, když uživatel zamkne počítač, je přímý přístup do zásuvky na konektorech PCI bez podřízených zařízení blokovaný, dokud se uživatel znovu nepřipojí. Zařízení, která už byla ve výčtu v době, kdy byl počítač odemčený, budou dál fungovat, dokud nebude odpojená.

- **Výčet externích zařízení nekompatibilních s režimem ochrany DMA v jádře**  
  CSP: [DmaGuard/DeviceEnumerationPolicy](/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  Tato zásada může poskytovat další zabezpečení proti externímu zařízení podporujícím technologii DMA. Umožňuje lepší kontrolu nad výčtem externích zařízení s technologií DMA, která nejsou kompatibilní s přemapováním DMA/izolací paměti zařízení a sandboxing.

  Tato zásada se projeví jenom v případě, že je ochrana DMA pro jádro podporovaná a povolená systémovým firmwarem. Ochrana pomocí rozhraní DMA pro jádro je funkce platformy, kterou musí systém podporovat v době výroby. Pokud chcete zjistit, jestli systém podporuje ochranu před nejenom jádrem, na stránce Souhrn v MSINFO32.exe ověřte pole ochrana jádra DMA.

  - **Nenakonfigurováno** – (*výchozí*)
  - **Blokovat vše**
  - **Povolení všech**

- **Blokovat připojení Bluetooth**  
  CSP: [Bluetooth/AllowDiscoverableMode](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano** – zablokuje připojení Bluetooth k zařízení a.

- **Blokování zjistitelnosti Bluetooth**  
  CSP: [Bluetooth/AllowDiscoverableMode](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano** – zabrání zařízení, aby bylo zjistitelné jinými zařízeními podporujícími technologii Bluetooth.

- **Zablokovat předběžné párování Bluetooth**  
  CSP: [Bluetooth/AllowPrepairing](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowprepairing)

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano** – zabraňuje automatickému párování specifických zařízení Bluetooth s hostitelským zařízením.

- **Blokovat reklamu přes Bluetooth**  
  CSP: [Bluetooth/AllowAdvertising](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano** – zabrání zařízení v posílání reklamy Bluetooth.  

- **Blokování blízkých připojení Bluetooth**  
  CSP: [Bluetooth/AllowPromptedProximalConnections](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections) zablokovat uživatelům používání páru SWIFT a dalších scénářů založených na blízkosti

  - **Nenakonfigurováno** (*výchozí*)
  - **Ano** – zabrání uživateli v použití páru SWIFT a dalších scénářů založených na blízkosti.  

  [Zprostředkovatel kryptografických služeb Bluetooth/AllowPromptedProximalConnections](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections)

- **Povolené služby Bluetooth**  
  CSP: [Bluetooth/ServicesAllowedList](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-servicesallowedlist).  
  Další informace o seznamu služeb najdete v tématu [Průvodce využitím ServicesAllowedList](/windows/client-management/mdm/policy-csp-bluetooth#servicesallowedlist-usage-guide) .

  - **Přidat** – zadejte povolené služby a profily Bluetooth jako šestnáctkové řetězce, například `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}` .
  - **Import** – importujte soubor. csv, který obsahuje seznam služeb a profilů Bluetooth, jako šestnáctkové řetězce, například `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`

## <a name="exploit-protection-profile"></a>Profil ochrany před zneužitím

### <a name="exploit-protection"></a>Ochrana Exploit Protection

- **Nahrát XML**  
  CSP: [ExploitProtectionSettings](https://go.microsoft.com/fwlink/?linkid=2067035)

  Umožňuje správci IT nabízet konfiguraci, která představuje požadované možnosti zmírnění systému a aplikace pro všechna zařízení v organizaci. Konfigurace je reprezentovaná souborem XML. Ochrana před zneužitím může chránit zařízení před malwarem, který využívá zneužití k rozšíření a nakazit. Pomocí aplikace zabezpečení systému Windows nebo PowerShellu vytvoříte sadu zmírnění hrozeb (označované jako konfigurace). Tuto konfiguraci pak můžete exportovat jako soubor XML a sdílet ho s více počítači ve vaší síti, aby všichni měli stejnou sadu nastavení pro zmírnění rizik. Existující konfigurační soubor XML nástroje EMET můžete také převést a importovat do konfiguračního souboru XML ochrany před zneužitím.

  Zvolte **možnost vybrat soubor XML**, zadejte XML filet upload a pak klikněte na **Vybrat**.
  - **Nenakonfigurováno** (*výchozí*)
  - **Ano**

- **Zablokuje uživatelům úpravy rozhraní zneužití ochrany před zneužitím.**  
  CSP: [DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **Nenakonfigurováno** (*výchozí*) – místní uživatelé mohou provádět změny v oblasti nastavení ochrany před zneužitím.
  - **Ano** – zabrání uživatelům v provádění změn v oblasti nastavení ochrany před zneužitím v Security Center programu Microsoft Defender.

## <a name="next-steps"></a>Další kroky

[Zásady zabezpečení služby Endpoint pro ASR](../protect/endpoint-security-asr-policy.md)