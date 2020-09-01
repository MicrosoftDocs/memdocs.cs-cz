---
title: Nastavení zásad antivirové ochrany Windows 10 z antivirové ochrany v programu Microsoft Defender pro zařízení připojená k tenantovi | Microsoft Docs
description: Podívejte se na seznam nastavení v profilu antivirového programu Microsoft Defender pro zařízení s Windows 10 spravovaná pomocí Configuration Manager. Tato nastavení můžete nakonfigurovat jako součást zásad ochrany před viry v Endpoint Security v Microsoft Intune po nakonfigurování připojení tenanta pro Configuration Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
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
ms.openlocfilehash: 3bb1d4806271ab40c60f0ad419e4e708d36bbc97
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194119"
---
# <a name="settings-for-microsoft-defender-antivirus-policy-for-tenant-attached-devices-in-microsoft-intune"></a>Nastavení pro zásady antivirové ochrany v programu Microsoft Defender pro zařízení připojená klientovi v Microsoft Intune

Umožňuje zobrazit nastavení antivirové ochrany v programu Microsoft Defender, která můžete spravovat pomocí profilu **Microsoft Defender Antivirus Policy (ConfigMgr)** z Intune. Profil je k dispozici při konfiguraci [zásad antivirové ochrany koncového bodu zabezpečení](../protect/endpoint-security-antivirus-policy.md)služby Intune a tato zásada se nasadí do zařízení, která spravujete pomocí nástroje Configuration Manager, když jste nakonfigurovali scénář [připojení klienta](../protect/tenant-attach-intune.md) .

## <a name="cloud-protection"></a>Ochrana cloudu

- **Zapnutí ochrany poskytované cloudem**  
  CSP: [AllowCloudProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Ve výchozím nastavení Defender v zařízeních s Windows 10 Desktop odesílá společnosti Microsoft informace o případných problémech, které najde. Microsoft analyzuje tyto informace, aby se dozvěděly Další informace o problémech, které se týkají vás a dalších zákazníků, a nabízí Vylepšená řešení.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému.
  - **Není povoleno.** Vypne služba Microsoft Active Protection Service.
  - **Povolené.**  Zapne služba Microsoft Active Protection Service.

- **Úroveň ochrany v cloudu**  
  CSP: [CloudBlockLevel](/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Nakonfigurujte, jak agresivní antivirová antivirová ochrana blokuje a kontroluje podezřelé soubory.
  - **Nenakonfigurováno** (*výchozí*) – výchozí úroveň blokování v programu Defender.
  - **Vysoce** agresivní blokování neznámých během optimalizace výkonu klienta, což zahrnuje větší šanci falešně pozitivních hodnot.
  - **Vysoké plus** – neznámy neznámé a používají další ochranné míry, které by mohly mít vliv na výkon klienta.
  - **Nulová tolerance** – zablokuje všechny neznámé spustitelné soubory.

- **Rozšířený časový limit pro Cloud Defenderu v sekundách**  
  CSP: [CloudExtendedTimeout](/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Antivirová ochrana automaticky blokuje podezřelé soubory po dobu 10 sekund, takže může zkontrolovat soubory v cloudu a ujistit se, že jsou bezpečné. Pomocí tohoto nastavení můžete tomuto časovému limitu přidat až 50 dalších sekund.

## <a name="microsoft-defender-antivirus-exclusions"></a>Vyloučení antivirové ochrany v programu Microsoft Defender

Pro každé nastavení v této skupině můžete rozbalit nastavení, vybrat **Přidat**a zadat hodnotu vyloučení.

- **Procesy v programu Defender k vyloučení**  
  CSP: [ExcludedProcesses](/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)

  Určuje seznam souborů otevřených procesy, které se mají ignorovat během kontroly. Samotný proces není při kontrole vyloučený.

- **Přípony souborů, které se mají vyloučit z kontrol a ochrany v reálném čase**  
  CSP: [ExcludedExtensions](/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)

  Zadejte seznam přípon typu souboru, které mají být při kontrole ignorovány.

- **Soubory a složky Defenderu k vyloučení**  
  CSP: [ExcludedPaths](/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

  Zadejte seznam souborů a cest k adresářům, které se mají ignorovat během kontroly.

## <a name="real-time-protection"></a>Ochrana v reálném čase

- **Zapnout ochranu v reálném čase**  
  CSP: [AllowRealtimeMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  K použití funkcí monitorování v reálném čase vyžaduje program Defender na zařízeních s Windows 10 Desktop.
  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího nastavení systému.
  - **Není povoleno.** Vypne službu monitorování v reálném čase.
  - **Povolené.** Zapne a spustí službu monitorování v reálném čase.

- **Povolit při ochraně přístupu**  
  CSP: [AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935)

  Nakonfigurujte nepřetržitě aktivní antivirovou ochranu, a to na rozdíl od na vyžádání.

  - **Nenakonfigurováno** (*výchozí*) – Tato zásada nemění stav tohoto nastavení v zařízení. Stávající stav zařízení zůstane beze změny.
  - **Není povoleno.** Vypne službu monitorování v reálném čase.
  - **Povolené.**

- **Monitorování příchozích a odchozích souborů**  
  CSP: [Defender/RealTimeScanDirection](https://go.microsoft.com/fwlink/?linkid=2113943)

  Konfigurací tohoto nastavení určíte, která aktivita souborů a programů systému souborů NTFS bude monitorována.
  - **Monitorovat všechny soubory (obousměrně)** (*výchozí*)
  - **Monitorovat příchozí soubory.**
  - **Monitorujte odchozí soubory.**

- **Zapnout monitorování chování**  
  CSP: [AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048)

  Ve výchozím nastavení používá Defender na zařízeních s Windows 10 Desktop funkce monitorování chování.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému.
  - **Není povoleno.** Vypne monitorování chování.
  - **Povolené.** Zapne monitorování chování v reálném čase.

- **Povolení systému ochrany před vniknutím**  
  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému.
  - **Není povoleno.**
  - **Povolené.**

- **Prohledat všechny stažené soubory a přílohy**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939)

  Nakonfigurujte Defender tak, aby kontroloval všechny stažené soubory a přílohy.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému.
  - **Není povoleno.**
  - **Povolené.**

- **Kontrolovat skripty, které se používají v prohlížečích Microsoftu**  
  CSP: [AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054)

  Nakonfigurujte Defender tak, aby kontroloval skripty.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému.
  - **Není povoleno.**
  - **Povolené.**

- **Prohledat síťové soubory**  
  CSP: [AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&)

  Nakonfigurujte Defender pro kontrolu síťových souborů.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému.
  - **Není povoleno.** Vypne prohledávání síťových souborů.
  - **Povolené.** Prohledá síťové soubory.

- **Kontrolovat e-maily**  
  CSP: [AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  Nakonfigurujte Defender pro kontrolu příchozích e-mailů.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému.
  - **Není povoleno.** Vypne kontrolu e-mailů.
  - **Povolené.** Zapne kontrolu e-mailů.

## <a name="remediation"></a>Náprava

- **Počet dní (0-90) pro udržení malwaru v karanténě**  
  CSP: [DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055)

  Zadejte počet dní od nuly do 90, po který systém ukládá položky v karanténě, než se automaticky odebere. Hodnota nula zachovává položky v karanténě a automaticky je neodstraní.

- **Předložit souhlas s ukázkami**  

  - **Nenakonfigurováno** (*výchozí*)
  - **Vždycky se zeptat.**
  - **Posílat bezpečné vzorky automaticky**
  - **Nikdy Neodesílat.**
  - **Posílat všechny vzorky automaticky**

- **Akce, která se má provést u potenciálně nežádoucích aplikací**  
  CSP: [PUAProtection](https://go.microsoft.com/fwlink/?linkid=2114051)

  Zadejte úroveň detekce potenciálně nežádoucích aplikací (PUAs). Program Defender upozorní uživatele, když se stahuje potenciálně nežádoucí software nebo se pokouší o instalaci na zařízení.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému, což je PUA ochrana.
  - **PUA Protection.** Program Windows Defender nebude chránit před potenciálně nežádoucími aplikacemi.
  - **PUA ochranu.** Zjištěné položky jsou blokované. Budou se zobrazovat v historii spolu s dalšími hrozbami.
  - **Režim auditování.** Defender detekuje potenciálně nežádoucí aplikace, ale neprovede žádnou akci. Můžete zkontrolovat informace o aplikacích, které Defender přijal, pomocí hledání událostí, které vytvořil Defender v Prohlížeč událostí.

- **Před vyčištěním počítačů vytvořit bod obnovení systému**  
  - **Ano** (*výchozí*)
  - **Ne**
  - **Není nakonfigurováno**

- **Akce zjištěných hrozeb**  
  CSP: [ThreatSeverityDefaultAction](https://go.microsoft.com/fwlink/?linkid=2113938)

  Zadejte akci, kterou Defender provede u zjištěného malwaru na základě úrovně hrozby malwaru.
  
  Defender klasifikuje malware, který detekuje, jako jednu z následujících úrovní závažnosti:
  - **Nízká hrozba**
  - **Střední hrozba**
  - **Vysoká hrozba**
  - **Závažná hrozba**

  Pro každou úroveň zadejte akci, která se má provést. Výchozí hodnota pro každou úroveň závažnosti není *nakonfigurovaná*.

  - **Nenakonfigurováno** (*výchozí*)
  - **Vyčistit** – služba se pokusí o obnovení souborů a pokusit se o jejich dezinfekci.
  - **Karanténa** – přesune soubory do karantény.
  - **Odebrat** – odebere soubory ze zařízení.
  - **Povolit** – povolí soubor a nepřijímá další akce.
  - **Definováno uživatelem** – uživatel zařízení provede rozhodnutí, které akce má provést.
  - **Blok** – zablokuje spuštění souboru.

## <a name="scan"></a>Prohledávání

- **Prohledat archivní soubory**  
  CSP: [AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047)

  Nakonfigurujte Defender pro kontrolu souborů archivu, jako jsou soubory ZIP nebo CAB.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení klienta, ve kterém se má kontrolovat archivované soubory, ale uživatel může kontrolu zakázat.
Další informace
  - **Nepovolené** Vypne kontrolu archivovaných souborů.
  - **Povolené.** Vyhledá archivní soubory.

- **Povolit nízkou prioritu procesoru pro naplánovaná prohledávání**  
  CSP: [EnableLowCPUPriority](https://go.microsoft.com/fwlink/?linkid=2113944)

  Nakonfigurujte prioritu procesoru pro naplánovaná prohledávání.
  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího systému, ve kterém se neprovádí žádné změny priority procesoru.
  - **Zakázáno**
  - **Povoleno**

- **Zakázat úplné prověřování při zachytávání**  
  CSP: [DisableCatchupFullScan](https://go.microsoft.com/fwlink/?linkid=2114042)

  Konfigurace zachytávání kontrol pro plánované úplné prověřování. Kontrola zachytávání je kontrola, která se spustí, protože se vynechala pravidelná Naplánovaná kontrola. Obvykle se Tato naplánovaná prohledávání neprojeví, protože počítač byl v naplánovaném čase vypnutý.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího klienta, což znamená, že se má povolit zachytávání kontrol pro úplnou kontrolu, ale uživatel je může vypnout.
  - **Zakázáno**
  - **Povoleno**

- **Zakázat rychlé prověřování zjištění nového stavu**  
  CSP: [DisableCatchupQuickScan](https://go.microsoft.com/fwlink/?linkid=2113941)

  Konfigurace zachytávání kontrol pro plánované rychlé prověřování. Kontrola zachytávání je kontrola, která se spustí, protože se vynechala pravidelná Naplánovaná kontrola. Obvykle se Tato naplánovaná prohledávání neprojeví, protože počítač byl v naplánovaném čase vypnutý.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se vrátí do výchozího nastavení klienta, které umožní rychlé kontroly, ale uživatel je může vypnout.
  - **Zakázáno**
  - **Povoleno**

- **Limit využití procesoru (0-100 procent) na jednu kontrolu**  
  CSP: [AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046)

  Zadejte jako procento od nuly do 100, což je průměrný faktor zatížení procesoru pro hledání v programu Defender.

- **Povolit skenování mapovaných síťových jednotek během úplného prohledávání**  
  CSP: [AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945)

  Nakonfigurujte Defender pro kontrolu mapovaných síťových jednotek.

  - **Nenakonfigurováno** (*výchozí*) – nastavení se obnoví do výchozího systému, což zakáže kontrolu mapovaných síťových jednotek.
  - **Není povoleno.** Zakáže kontrolu mapovaných síťových jednotek.
  - **Povolené.** Kontroluje namapované síťové jednotky.

- **Spustit každodenní rychlou kontrolu v**  
  CSP: [ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053)

  Vyberte denní dobu, po kterou se spustí rychlé prověřování v Defenderu.
  Ve výchozím nastavení není tato možnost **nakonfigurovaná** .

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
  - **Zakázáno**
  - **Povoleno**

- **Náhodně přeskupit časy zahájení naplánovaných prohledávání a aktualizace Security Intelligence**  
  -**Nenakonfigurováno** (*výchozí*) –**Ano** 
  - **ne**

- **Kontrolovat vyměnitelné jednotky při úplné kontrole**
  - **Nenakonfigurováno** (*výchozí*)
  - **Není povoleno.** Vypne kontrolu vyměnitelných jednotek.
  - **Povolené.** Vyhledá vyměnitelné jednotky.

## <a name="updates"></a>Aktualizace

- **Zadejte, jak často (0-24 hodin) se mají kontrolovat aktualizace služby Security Intelligence.**  
  CSP: [SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936)

  Zadejte interval od nuly do 24 (v hodinách), který se používá ke kontrole podpisů. Nulová hodnota nemá za následek kontrolu nových podpisů. Hodnota 2 bude kontrolovat každé dvě hodiny atd.

- **Pořadí záložní aktualizace podpisů (zařízení)**

- **Podpis – aktualizace zdrojů sdílených složek (zařízení)**

- **Umístění Security Intelligence (zařízení)**  

## <a name="user-experience"></a>Uživatelské prostředí

- **Zablokovat přístup uživatelů k aplikaci Microsoft Defender**  
  - **Nenakonfigurováno** (*výchozí*)
  - **Není povoleno.** Zabrání uživatelům v přístupu k uživatelskému rozhraní.
  - **Povolené.** Umožňuje uživatelům přístup k uživatelskému rozhraní.

- **Zobrazit zprávy s oznámeními v klientském počítači, když uživatel potřebuje spustit úplnou kontrolu, aktualizovat Security Intelligence nebo spustit program Windows Defender Offline**  
  - **Nenakonfigurováno** (*výchozí*)
  - **Ano**
  - **Ne**

- **Zakázat uživatelské rozhraní klienta**  
  - **Nenakonfigurováno** (*výchozí*)
  - **Ano**
  - **Ne**

- **Dovolit uživatelům zobrazení úplných výsledků historie**
  - **Nenakonfigurováno** (*výchozí*)
  - **Ano**
  - **Ne**