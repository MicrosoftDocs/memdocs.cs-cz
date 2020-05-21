---
title: Nastavení zásad antivirové ochrany Windows 10 pro antivirovou ochranu v programu Microsoft Defender pro Intune | Microsoft Docs
description: Podívejte se na seznam nastavení v profilu antivirové ochrany Microsoft Defenderu pro Windows 10. Tato nastavení můžete nakonfigurovat jako součást zásad ochrany před viry v zabezpečení koncového bodu v Microsoft Intune.
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
ms.openlocfilehash: be850b2351de138ddacb087b2acf198e164dcd67
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83430098"
---
# <a name="settings-for-windows-10-microsoft-defender-antivirus-policy-in-microsoft-intune"></a>Nastavení pro zásady antivirové ochrany v Microsoft Defenderu pro Windows 10 v Microsoft Intune

Podívejte se na nastavení zásad ochrany antivirovým programem Endpoint Security, která můžete nakonfigurovat pro antivirový profil Microsoft Defender pro Windows 10 v Microsoft Intune jako součást [zásady zabezpečení koncového bodu](../protect/endpoint-security-policy.md).

## <a name="cloud-protection"></a>Ochrana cloudu

- **Zapnutí ochrany poskytované cloudem**  
  CSP: [AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Ve výchozím nastavení Defender v zařízeních s Windows 10 Desktop odesílá společnosti Microsoft informace o případných problémech, které najde. Microsoft analyzuje tyto informace, aby se dozvěděly Další informace o problémech, které se týkají vás a dalších zákazníků, a nabízí Vylepšená řešení.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému.
  - **Ne** – nastavení je zakázané. Uživatelé zařízení nemůžou toto nastavení změnit.
  - **Ano** – ochrana Doručená v cloudu je zapnutá.  Uživatelé zařízení nemůžou toto nastavení změnit.

- **Úroveň ochrany v cloudu**  
  CSP: [CloudBlockLevel](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Nakonfigurujte, jak agresivní antivirová antivirová ochrana blokuje a kontroluje podezřelé soubory.
  - **Nenakonfigurováno** (*výchozí*) – výchozí úroveň blokování v programu Defender.
  - **Vysoce** agresivní blokování neznámých během optimalizace výkonu klienta, což zahrnuje větší šanci falešně pozitivních hodnot.
  - **Vysoké plus** – neznámy neznámé a používají další ochranné míry, které by mohly mít vliv na výkon klienta.
  - **Nulová tolerance** – zablokuje všechny neznámé spustitelné soubory.

- **Rozšířený časový limit pro Cloud Defenderu v sekundách**  
  CSP: [CloudExtendedTimeout](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Antivirová ochrana automaticky blokuje podezřelé soubory po dobu 10 sekund, takže může zkontrolovat soubory v cloudu a ujistit se, že jsou bezpečné. Pomocí tohoto nastavení můžete tomuto časovému limitu přidat až 50 dalších sekund.

## <a name="microsoft-defender-antivirus-exclusions"></a>Vyloučení antivirové ochrany v programu Microsoft Defender

Pro každé nastavení v této skupině můžete rozbalit nastavení, vybrat **Přidat**a zadat hodnotu vyloučení.

- **Procesy v programu Defender k vyloučení**  
  CSP: [ExcludedProcesses](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)

  Určuje seznam souborů otevřených procesy, které se mají ignorovat během kontroly. Samotný proces není při kontrole vyloučený.

- **Přípony souborů, které se mají vyloučit z kontrol a ochrany v reálném čase**  
  CSP: [ExcludedExtensions](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)

  Zadejte seznam přípon typu souboru, které mají být při kontrole ignorovány.

- **Soubory a složky Defenderu k vyloučení**  
  CSP: [ExcludedPaths](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

  Zadejte seznam souborů a cest k adresářům, které se mají ignorovat během kontroly.

## <a name="real-time-protection"></a>Ochrana v reálném čase

- **Zapnout ochranu v reálném čase**  
  CSP: [AllowRealtimeMonitoring](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  K použití funkcí monitorování v reálném čase vyžaduje program Defender na zařízeních s Windows 10 Desktop.
  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího nastavení systému.
  - **Ne** – nastavení je zakázané. Uživatelé zařízení nemůžou toto nastavení změnit.
  - **Ano** – vynutilo používání monitorování v reálném čase. Uživatelé zařízení nemůžou toto nastavení změnit.

- **Povolit při ochraně přístupu**  
  CSP: [AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935)

  Nakonfigurujte nepřetržitě aktivní antivirovou ochranu, a to na rozdíl od na vyžádání.

  - **Nenakonfigurováno** (*výchozí*) – Tato zásada nemění stav tohoto nastavení v zařízení. Stávající stav zařízení zůstane beze změny.
  - **No** – zablokuje ochranu přístupu na zařízeních. Uživatelé zařízení nemůžou toto nastavení změnit.
  - Na zařízeních je aktivní ochrana přístupu na úrovni **Ano** .

- **Monitorování příchozích a odchozích souborů**  
  CSP: [Defender/RealTimeScanDirection](https://go.microsoft.com/fwlink/?linkid=2113943)

  Konfigurací tohoto nastavení určíte, která aktivita souborů a programů systému souborů NTFS bude monitorována.
  - **Monitorovat všechny soubory** (*výchozí*)
  - **Monitorovat jenom příchozí soubory**
  - **Monitorovat jenom odchozí soubory**

- **Zapnout monitorování chování**  
  CSP: [AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048)

  Ve výchozím nastavení používá Defender na zařízeních s Windows 10 Desktop funkce monitorování chování.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému.
  - **Ne** – nastavení je zakázané. Uživatelé zařízení nemůžou toto nastavení změnit.
  - **Ano** – vynutilo používání monitorování chování v reálném čase. Uživatelé zařízení nemůžou toto nastavení změnit.

- **Zapnout ochranu sítě**  
  CSP: [EnableNetworkProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  Chraňte uživatele zařízení pomocí libovolné aplikace v přístupu k podvodným podvodům, webům pro zneužití a škodlivému obsahu na internetu. Ochrana zahrnuje prevenci prohlížeče třetích stran v připojení k nebezpečným webům.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému.
  - **Ne** – nastavení je zakázané. Uživatelé zařízení nemůžou toto nastavení změnit.
  - **Ano** – Ochrana sítě je zapnutá. Uživatelé zařízení nemůžou toto nastavení změnit.

- **Prohledat všechny stažené soubory a přílohy**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939)

  Nakonfigurujte Defender tak, aby kontroloval všechny stažené soubory a přílohy.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému.
  - **Ne** – nastavení je zakázané. Uživatelé zařízení nemůžou toto nastavení změnit.
  - **Ano** – Defender vyhledá všechny stažené soubory a přílohy. Uživatelé zařízení nemůžou toto nastavení změnit.

- **Kontrolovat skripty, které se používají v prohlížečích Microsoftu**  
  CSP: [AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054)

  Nakonfigurujte Defender tak, aby kontroloval skripty.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému.
  - **Ne** – nastavení je zakázané. Uživatelé zařízení nemůžou toto nastavení změnit.
  - **Ano** – Defender prohledává skripty. Uživatelé zařízení nemůžou toto nastavení změnit.

- **Prohledat síťové soubory**  
  CSP: [AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&)

  Nakonfigurujte Defender pro kontrolu síťových souborů.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému.
  - **Ne** – nastavení je zakázané. Uživatelé zařízení nemůžou toto nastavení změnit.
  - **Ano** – zapněte kontrolu síťových souborů. Uživatelé zařízení nemůžou toto nastavení změnit.

- **Kontrolovat e-maily**  
  CSP: [AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  Nakonfigurujte Defender pro kontrolu příchozích e-mailů.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému.
  - **Ne** – nastavení je zakázané. Uživatelé zařízení nemůžou toto nastavení změnit.
  - **Ano** – zapněte kontrolu e-mailů. Uživatelé zařízení nemůžou toto nastavení změnit.

## <a name="remediation"></a>Odstranění rizika

- **Počet dní (0-90) pro udržení malwaru v karanténě**  
  CSP: [DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055)

  Zadejte počet dní od nuly do 90, po který systém ukládá položky v karanténě, než se automaticky odebere. Hodnota nula zachovává položky v karanténě a automaticky je neodstraní.

- **Předložit souhlas s ukázkami**  

  - **Nenakonfigurováno** (*výchozí*)
  - **Posílat bezpečné vzorky automaticky**
  - **Vždycky se zeptat**
  - **Nikdy Neodesílat**
  - **Posílat všechny vzorky automaticky**

- **Akce, která se má provést u potenciálně nežádoucích aplikací**  
  CSP: [PUAProtection](https://go.microsoft.com/fwlink/?linkid=2114051)

  Zadejte úroveň detekce potenciálně nežádoucích aplikací (PUAs). Program Defender upozorní uživatele, když se stahuje potenciálně nežádoucí software nebo se pokouší o instalaci na zařízení.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému, což je PUA ochrana.
  - **Zakázat**
  - **Povolit** – zjištěné položky jsou blokované a zobrazují se v historii spolu s dalšími hrozbami.
  - **Režim auditování** – Defender detekuje potenciálně nežádoucí aplikace, ale neprovede žádnou akci. Můžete zkontrolovat informace o aplikacích, které Defender přijal, pomocí hledání událostí, které vytvořil Defender v Prohlížeč událostí.

- **Akce zjištěných hrozeb**  
  CSP: [ThreatSeverityDefaultAction](https://go.microsoft.com/fwlink/?linkid=2113938)

  Zadejte akci, kterou Defender provede u zjištěného malwaru na základě úrovně hrozby malwaru.
  
  Defender klasifikuje malware, který detekuje, jako jednu z následujících úrovní závažnosti:
  - **Nízká závažnost**
  - **Střední závažnost**
  - **Vysoká závažnost**
  - **Závažná závažnost**

  Pro každou úroveň zadejte akci, která se má provést. Výchozí hodnota pro každou úroveň závažnosti není *nakonfigurovaná*.

  - **Není nakonfigurováno**
  - **Vyčistit** – služba se pokusí o obnovení souborů a pokusit se o jejich dezinfekci.
  - **Karanténa** – přesune soubory do karantény.
  - **Odebrat** – odebere soubory ze zařízení.
  - **Povolit** – povolí soubor a nepřijímá další akce.
  - **Definováno uživatelem** – uživatel zařízení provede rozhodnutí, které akce má provést.
  - **Blok** – zablokuje spuštění souboru.

## <a name="scan"></a>Skenování

- **Prohledat archivní soubory**  
  CSP: [AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047)

  Nakonfigurujte Defender pro kontrolu souborů archivu, jako jsou soubory ZIP nebo CAB.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení klienta, ve kterém se má kontrolovat archivované soubory, ale uživatel ho může zakázat.
Další informace
  - Archivy **žádného** souboru nejsou prohledávány. Uživatelé zařízení nemůžou toto nastavení změnit.
  - **Ano** – povolí kontroly souborů archivu. Uživatelé zařízení nemůžou toto nastavení změnit.

- **Pro naplánovaná prohledávání použít nízkou prioritu procesoru**  
  CSP: [EnableLowCPUPriority](https://go.microsoft.com/fwlink/?linkid=2113944)

  Nakonfigurujte prioritu procesoru pro naplánovaná prohledávání.
  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího systému, ve kterém se neprovádí žádné změny priority procesoru.
  - **Ne** – nastavení je zakázané. Uživatelé zařízení nemůžou toto nastavení změnit.
  - **Ano** – nízká priorita procesoru bude použita během naplánovaných kontrol. Uživatelé zařízení nemůžou toto nastavení změnit.

- **Zakázat úplné prověřování při zachytávání**  
  CSP: [DisableCatchupFullScan](https://go.microsoft.com/fwlink/?linkid=2114042)

  Konfigurace zachytávání kontrol pro plánované úplné prověřování. Kontrola, která je zachytávání, se spustí, protože se vynechala pravidelná Naplánovaná kontrola. Obvykle se Tato naplánovaná prohledávání neprojeví, protože počítač byl v naplánovaném čase vypnutý.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího klienta, což znamená, že se má povolit zachytávání kontrol pro úplnou kontrolu, ale uživatel je může vypnout.
  - **Ne** – nastavení je zakázané. Uživatelé zařízení nemůžou toto nastavení změnit.
  - **Ano** – vynutily se kontroly pro plánované úplné kontroly a uživatel je nemůže zakázat. Pokud je počítač offline po dvou po sobě jdoucích plánovaných kontrolách, spustí se při příštím přihlášení k počítači, když se někdo znovu přihlašuje. Pokud není nakonfigurovaná žádná Naplánovaná kontrola, nebudete moct spustit žádnou kontrolu. Uživatelé zařízení nemůžou toto nastavení změnit.

- **Zakázat rychlé prověřování zjištění nového stavu**  
  CSP: [DisableCatchupQuickScan](https://go.microsoft.com/fwlink/?linkid=2113941)

  Konfigurace zachytávání kontrol pro plánované rychlé prověřování. Kontrola, která je zachytávání, se spustí, protože se vynechala pravidelná Naplánovaná kontrola. Obvykle se Tato naplánovaná prohledávání neprojeví, protože počítač byl v naplánovaném čase vypnutý.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení klienta, které umožní rychlé kontroly, ale uživatel je může vypnout.
  - **Ne** – nastavení je zakázané. Uživatelé zařízení nemůžou toto nastavení změnit.
  - **Ano** – vynutily se kontroly pro plánované rychlé kontroly a uživatel je nemůže zakázat. Pokud je počítač offline po dvou po sobě jdoucích plánovaných kontrolách, spustí se při příštím přihlášení k počítači, když se někdo znovu přihlašuje. Pokud není nakonfigurovaná žádná Naplánovaná kontrola, nebudete moct spustit žádnou kontrolu. Uživatelé zařízení nemůžou toto nastavení změnit.

- **Limit využití procesoru na kontrolu**  
  CSP: [AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046)

  Zadejte jako procento od nuly do 100, což je průměrný faktor zatížení procesoru pro hledání v programu Defender.

- **Při úplné kontrole kontrolovat namapované síťové jednotky**  
  CSP: [AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945)

  Nakonfigurujte Defender pro kontrolu mapovaných síťových jednotek.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému, což zakáže kontrolu mapovaných síťových jednotek.
  - **Ne** – nastavení je zakázané. Uživatelé zařízení nemůžou toto nastavení změnit.
  - **Ano** – povolí kontroly mapovaných síťových jednotek. Uživatelé zařízení nemůžou toto nastavení změnit.

- **Spustit každodenní rychlou kontrolu v**  
  CSP: [ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053)

  Vyberte denní dobu, po kterou se spustí rychlé prověřování v Defenderu.
  Ve výchozím nastavení to není **nakonfigurované** .

- **Typ kontroly**  
  CSP: [ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045)

  Vyberte typ kontroly, který Defender spustí.

  - **Nenakonfigurováno** (*výchozí*)
  - **Rychlá kontrola**
  - **Úplná kontrola**

- **Den v týdnu, kdy se má spustit Naplánovaná kontrola**  
  - **Nenakonfigurováno** (*výchozí*)

- **Denní doba spuštění naplánované kontroly**  
  - **Nenakonfigurováno** (*výchozí*)

- **Před spuštěním kontroly vyhledat aktualizace podpisů**  
  - **Nenakonfigurováno** (*výchozí*)
  - **Ne**
  - **Ano**

## <a name="updates"></a>Aktualizace

- **Zadejte, jak často (0-24 hodin) se mají kontrolovat aktualizace služby Security Intelligence.**  
  CSP: [SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936)

  Zadejte interval od nuly do 24 (v hodinách), který se používá ke kontrole podpisů. Nulová hodnota nemá za následek kontrolu nových podpisů. Hodnota 2 bude kontrolovat každé dvě hodiny atd.

## <a name="user-experience"></a>Uživatelské prostředí

- **Povolení přístupu uživatele k aplikaci Microsoft Defender**  
  CSP: [AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043)  

  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení klienta, ve kterém se uživatelské rozhraní a oznámení povolují.
  - **Ne** – uživatelské rozhraní (UI) programu Defender je nedostupné a nepřístupné oznámení se nepoužívá.
  - **Ano**

