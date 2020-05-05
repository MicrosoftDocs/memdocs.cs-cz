---
title: Protokoly serverových událostí
titleSuffix: Configuration Manager
description: Technické informace o možných položkách serveru BitLocker (MBAM) v protokolu událostí systému Windows
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c3279b7d-654d-444b-bd17-1262894590c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8d49a24b6fea08f12d1fe70c1e0b7415adf98719
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074805"
---
# <a name="server-event-logs"></a>Protokoly serverových událostí

*Platí pro: Configuration Manager (Current Branch)*

<!--3601034-->

Pomocí Prohlížeč událostí Windows můžete zobrazit protokoly událostí pro následující součásti management server BitLockeru v Configuration Manager:

- Služba obnovení v bodu správy
- Samoobslužný portál
- Web pro správu a monitorování

Na serveru, který je hostitelem jedné nebo více těchto součástí, otevřete Prohlížeč událostí. Pak přejdete na **protokoly aplikací a služeb**, **Microsoft**, **Windows**a rozbalte **MBAM-web**. Ve výchozím nastavení jsou k dispozici protokoly událostí pro [správu](#admin) a [provoz](#operational) .

Následující části obsahují zprávy a informace o odstraňování potíží pro ID událostí, ke kterým může docházet pomocí komponent management server BitLockeru.

## <a name="admin"></a>Správce

### <a name="1-webappspnerror"></a>1: WebAppSpnError

U aplikace {název_webu} {Virtualdirector} chybí následující názvy hlavních názvů služby (SPN): {ListOfSpns} zaregistrujte požadované SPN na účtu: {ExecutionAccount}.

Aby bylo úspěšné integrované ověřování systému Windows, musí být nezbytné hlavní názvy služby (SPN). Tato zpráva znamená, že hlavní název služby (SPN) vyžadovaný pro aplikaci není správně nakonfigurovaný. Podrobnosti obsažené v této události by měly poskytovat další informace.

<!-- See "Service Principal Name (SPN)" in MBAM 2.5 Server Prerequisites for Stand-alone and Configuration Manager Integration Topologies for more information. -->

### <a name="100-adminservicerecoverydberror"></a>100: AdminServiceRecoveryDbError

Možné chybové zprávy:

- GetMachineUsers: došlo k chybě při získávání informací o uživateli z databáze.
- GetRecoveryKey: při získávání obnovovacího klíče z databáze došlo k chybě.
- GetRecoveryKey: došlo k chybě při získávání informací o uživateli z databáze.
- GetRecoveryKeyIds: při získávání ID obnovovacích klíčů z databáze došlo k chybě.
- GetTpmHashForUser: při získávání dat hash čipu TPM z databáze obnovení došlo k chybě.
- GetTpmHashForUser: při získávání dat hash čipu TPM z databáze obnovení došlo k chybě.
- QueryDriveRecoveryData: při získávání dat obnovy jednotky z databáze došlo k chybě.
- QueryRecoveryKeyIdsForUser: při získávání ID obnovovacích klíčů z databáze došlo k chybě.
- QueryVolumeUsers: došlo k chybě při získávání informací o uživateli z databáze.

Tato zpráva se zaprotokoluje vždy, když dojde k výjimce při komunikaci s databází pro obnovení. Přečtěte si informace obsažené v trasování pro získání konkrétních podrobností o výjimce.

### <a name="101-adminservicecompliancedberror"></a>101: AdminServiceComplianceDbError

Možné chybové zprávy:

- GetRecoveryKey: při protokolování události auditu do databáze dodržování předpisů došlo k chybě.
- GetRecoveryKeyIds: při protokolování události auditu do databáze dodržování předpisů došlo k chybě.
- GetTpmHashForUser: při protokolování události auditu do databáze dodržování předpisů došlo k chybě.
- QueryRecoveryKeyIdsForUser: při protokolování události auditu do databáze dodržování předpisů došlo k chybě.
- QueryDriveRecoveryData: při protokolování události auditu do databáze dodržování předpisů došlo k chybě.

Tato zpráva se zaznamená, kdykoli při komunikaci s databází dodržování předpisů dojde k výjimce. Přečtěte si informace obsažené v trasování pro získání konkrétních podrobností o výjimce.

### <a name="102-agentservicerecoverydberror"></a>102: AgentServiceRecoveryDbError

Tato zpráva označuje výjimku, pokud se služba pokusí o komunikaci s databází pro obnovení. Přečtěte si zprávu obsaženou v události a získejte konkrétní informace o výjimce.

Ověřte, že účet fondu aplikací MBAM má požadovaná oprávnění pro připojení k databázi pro obnovení.

### <a name="103-agentserviceerror"></a>103: AgentServiceError

Možné chybové zprávy:

- Nelze zjistit účet klientského počítače nebo uživatelský účet migrace dat.

    Pokaždé, když se provede volání `PostKeyRecoveryInfo`metod `IsRecoveryKeyResetRequired`, `CommitRecoveryKeyRest`, a `GetTpmHash` , načte volající kontext pro získání přihlašovacích údajů volajícího. Pokud má volající kontext hodnotu null nebo je prázdný, služba protokoluje tuto zprávu.

- Ověření účtu pro identitu volajícího se nezdařilo.

    Tato zpráva se zaznamená do protokolu, pokud webová metoda očekává, že volající je účet počítače a není. Může to být také způsobeno tím, že webová metoda očekává, že volající je uživatelský účet, a není to uživatelský účet nebo člen účtu skupiny migrace dat.

### <a name="104-statusservicecompliancedbconfigerror"></a>104: StatusServiceComplianceDbConfigError

Připojovací řetězec databáze dodržování předpisů v registru je prázdný.

Tato zpráva se zaprotokoluje vždy, když je připojovací řetězec databáze dodržování předpisů neplatný. Ověřte hodnotu v klíči `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString`registru.

### <a name="105-statusservicecompliancedberror"></a>105: StatusServiceComplianceDbError

Tato chyba označuje, že weby nebo webové služby se nedokázaly připojit k databázi dodržování předpisů. Ověřte, zda se účet fondu aplikací služby IIS může připojit k databázi.

### <a name="106-helpdeskerror"></a>106: HelpdeskError

Známé chyby a možné příčiny:

- Požadavek na adresu URL způsobil vnitřní chybu.

    V aplikaci se vyvolala Neošetřená výjimka pro web pro správu a monitorování (helpdesk). Zkontrolujte položky protokolu v protokolu událostí **správce** a najděte konkrétní výjimku.

- Při získávání informací o kontextu spuštění došlo k chybě. Nelze ověřit registraci hlavního názvu služby (SPN).

    Během operace načítání webu technické podpory kontroluje hlavní název služby (SPN). Pokud chcete ověřit hlavní název služby (SPN), vyžaduje informace o účtu, IIS website a ApplicationVirtualPath, které odpovídají webu helpdesku. Tato chybová zpráva se zaznamená, když některý z těchto atributů není platný nebo chybí.

- Při ověřování registrace hlavního názvu služby (SPN) došlo k chybě.

    Tato zpráva znamená, že při ověřování hlavního názvu služby (SPN) je vyvolána výjimka zabezpečení. Podívejte se na výjimku obsaženou v podrobnostech události.

### <a name="107-selfserviceportalerror"></a>107: SelfServicePortalError

Známé chyby a možné příčiny:

- Při získávání obnovovacího klíče pro uživatele došlo k chybě.

    Označuje, že byla vyvolána Neočekávaná výjimka, když byla vytvořena žádost o načtení obnovovacího klíče. Podívejte se na zprávu výjimky v podrobnostech události. Pokud je trasování povolené v aplikaci helpdesku, přečtěte si téma trasování dat a Získejte podrobné zprávy o výjimkách.

- Při získávání informací o kontextu spuštění došlo k chybě. Nepovedlo se ověřit registraci hlavního názvu služby (SPN).

    Během počáteční operace načítání načte Samoobslužný portál informace o účtu, IIS a ApplicationVirtualPath pro samoobslužný web, který ověřuje hlavní název služby (SPN). Tato chybová zpráva se zaznamená do protokolu, když jeden nebo více těchto atributů není platný.

- Při ověřování registrace hlavního názvu služby (SPN) došlo k chybě. EventDetails: {ExceptionMessage}

    Tato zpráva znamená, že při ověřování hlavního názvu služby byla vyvolána výjimka zabezpečení. Podívejte se na výjimku obsaženou v podrobnostech události.

### <a name="108-domaincontrollererror"></a>108: DomainControllerError

Známé chyby a možné příčiny:

- Při překladu názvu domény {domainname} došlo k chybě. došlo k chybě přidělení paměti.

    K překladu názvu domény volá rozhraní API `DsGetDcName` systému Windows. Tato zpráva se zaznamená do protokolu, `ERROR_NOT_ENOUGH_MEMORY`když toto rozhraní API vrátí, což znamená selhání přidělení paměti.

- Nepovedlo se vyvolat metodu DsGetDcName.

    Tato zpráva znamená, že `DsGetDcName` rozhraní API není na hostiteli k dispozici.

### <a name="109-webapprecoverydberror"></a>109: WebAppRecoveryDbError

Známé chyby a možné příčiny:

- Při čtení konfigurace databáze pro obnovení došlo k chybě. Připojovací řetězec k databázi pro obnovení není nakonfigurován.

    Tato zpráva znamená, že informace o připojovacím řetězci `HKLM\Software\Microsoft\MBAM Server\Web\RecoveryDBConnectionString` databáze obnovení nejsou platné. Ověřte zadanou hodnotu klíče registru.

Pokud se zobrazí některá z následujících zpráv, ověřte, zda pověření fondu aplikací ze serveru služby IIS může vytvořit připojení k databázi obnovení:

- DoesUserHaveMatchingRecoveryKey: při získávání ID obnovovacího klíče pro uživatele došlo k chybě.
- QueryDriveRecoveryData: při získávání dat obnovení jednotky došlo k chybě.
- QueryRecoveryKeyIdsForUser: při získávání ID obnovovacího klíče pro uživatele došlo k chybě.
- Při získávání hodnoty hash hesla čipu TPM z databáze obnovení došlo k chybě.

### <a name="110-webappcompliancedberror"></a>110: WebAppComplianceDbError

Známé chyby a možné příčiny:

- Při čtení konfigurace databáze dodržování předpisů došlo k chybě. Připojovací řetězec k databázi dodržování předpisů není nakonfigurován.

    Tato zpráva znamená, že informace o připojovacím řetězci `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString` databáze dodržování předpisů na je neplatná. Ověřte hodnotu tohoto klíče registru.

Pokud se zobrazí některá z následujících zpráv, ověřte, jestli přihlašovací údaje fondu aplikací ze serveru IIS můžou navázání spojení s databází dodržování předpisů:

- GetRecoveryKeyForCurrentUser: při protokolování události auditu do databáze dodržování předpisů došlo k chybě.
- QueryRecoveryKeyIdsForUser: při protokolování události auditu do databáze dodržování předpisů došlo k chybě.
- QueryRecoveryKeyIdsForUser: při protokolování události auditu do databáze dodržování předpisů došlo k chybě.

### <a name="111-webappdberror"></a>111: WebAppDbError

Tyto chyby označují jednu z následujících dvou podmínek:

- Websites nebo WebServices MBAM se nepodařilo připojit k databázi kompatibility nebo obnovení.
- Účet pro spuštění MBAM websites/WebServices (účet fondu aplikací) nemohl spustit `GetVersion` uloženou proceduru v databázi dodržování předpisů nebo obnovení.

Zpráva obsažená v události obsahuje další podrobnosti o výjimce.

Ověřte, že se účet fondu aplikací může připojit k databázím dodržování předpisů nebo obnovení. Potvrďte, že má oprávnění ke spuštění `GetVersion` uložené procedury.

### <a name="112-webapperror"></a>112: WebAppError

Při ověřování registrace hlavního názvu služby (SPN) došlo k chybě.

Chcete-li ověřit hlavní název služby (SPN), dotazuje se na službu Active Directory, aby získala Seznam mapovaných spouštěcích účtů Také se dotazuje `ApplicationHost.config` na, aby získal vazby webu. Tato chybová zpráva znamená, že nemůže komunikovat se službou Active Directory, nebo nemůže `ApplicationHost.config` soubor načíst.

Ověřte, že účet fondu aplikací má oprávnění k dotazování služby Active Directory `ApplicationHost.config` nebo souboru. Ověřte také položky vazby webu v `ApplicationHost.config` souboru.

## <a name="operational"></a>Funkční

### <a name="4-performancecountererror"></a>4: PerformanceCounterError

Při načítání čítače výkonu došlo k chybě.

Zpráva trasování obsahuje skutečnou zprávu o výjimce, jejíž seznam najdete tady:

- ArgumentNullException: Tato výjimka je vyvolána, pokud je kategorie, čítač nebo instance požadovaného čítače výkonu neplatná.
- System. InvalidOperationException: categoryName je prázdný řetězec (""). counterName je prázdný řetězec ("").
- Požadované nastavení oprávnění ke čtení a zápisu není pro tento čítač platné.
- Zadaná kategorie neexistuje (Pokud je vlastnost readOnly nastavena na hodnotu true).
- Zadaná kategorie není .NET Framework vlastní kategorie (Pokud je jen pro čtení hodnotu false).
- Zadaná kategorie je označená jako více instancí a vyžaduje, aby byl čítač výkonu vytvořen s názvem instance.
- instance je delší než 127 znaků.
- NázevKategorie a counterName byly lokalizovány do různých jazyků.
- System. ComponentModel. Win32Exception: při přístupu k systémovému rozhraní API došlo k chybě.
- System. UnauthorizedAccessException: kód, který se spouští bez oprávnění správce, se pokusil přečíst počítadlo výkonu.

Zpráva v události poskytuje další podrobnosti o výjimce.

V `System.UnauthorizedAccessException`případě nástroje ověřte, zda má účet fondu aplikací přístup k rozhraním API čítače výkonu.

### <a name="200-helpdeskinformation"></a>200: HelpDeskInformation

Aplikace webu pro správu se úspěšně našla a připojila k podporované verzi databáze pro obnovení nebo dodržování předpisů.

Označuje úspěšné připojení k databázi pro obnovení nebo databázi dodržování předpisů z webu helpdesku.

### <a name="201-selfserviceportalinformation"></a>201: SelfServicePortalInformation

Aplikace samoobslužného portálu se úspěšně našla a připojila k podporované verzi databáze pro obnovení nebo dodržování předpisů.

Označuje úspěšné připojení k databázi pro obnovení nebo databázi dodržování předpisů ze samoobslužného portálu.

### <a name="202-webappinformation"></a>202: WebAppInformation

Aplikace má správně zaregistrované hlavní názvy služby.

Indikuje, že hlavní názvy služby (SPN) vyžadované pro web helpdesku jsou správně zaregistrované u spuštěného účtu.

## <a name="see-also"></a>Viz také

Další informace o použití těchto protokolů najdete v tématu [protokoly událostí BitLockeru](about-event-logs.md).

Další informace o řešení potíží najdete v tématu [řešení potíží s nástrojem BitLocker](troubleshoot.md).

Další informace o instalaci těchto webů najdete v tématu [nastavení a vytváření sestav a portálů nástroje BitLocker](../../deploy-use/bitlocker/setup-websites.md).
