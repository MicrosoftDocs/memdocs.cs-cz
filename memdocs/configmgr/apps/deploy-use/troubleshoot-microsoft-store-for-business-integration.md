---
title: Řešení potíží s integrací MSfB
titleSuffix: Configuration Manager
description: Poskytuje návrhy a řešení pro řešení některých nejběžnějších problémů s Microsoft Store pro podnikání a integraci vzdělávání.
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 09929057-ecf2-4d49-aee0-709916932b14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 694083bbce34b9e1b62f77a1d18cf79663704b2a
ms.sourcegitcommit: af8a3efd361a7f3fa6e98e5126dfb1391966ff76
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/24/2020
ms.locfileid: "82149094"
---
# <a name="troubleshoot-the-microsoft-store-for-business-and-education-integration-with-configuration-manager"></a>Řešení potíží s Microsoft Store pro podnikání a vzdělávání pomocí Configuration Manager

Tento článek obsahuje klíčové tipy a opravy pro některé z nejdůležitějších problémů, které můžete mít v rámci integrace Microsoft Store for Business a vzdělávání (MSfB) s Configuration Manager.

Další informace o používání Microsoft Store pro firmy a vzdělávání s Configuration Manager najdete v tématu [Správa aplikací z Microsoft Store pro firmy a vzdělávání pomocí Configuration Manager](manage-apps-from-the-windows-store-for-business.md).

## <a name="monitor"></a>Monitorování

### <a name="component-status"></a>Stav součásti

V konzole Configuration Manager otevřete pracovní prostor **monitorování** , rozbalte položku **stav systému**a vyberte uzel **Stav součásti** . Stav monitorování následujících součástí:

- SMS_BUSINESS_APP_PROCESS_MANAGER
- SMS_CLOUDCONNECTION

### <a name="sync-status"></a>Stav synchronizace

V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **Microsoft Store pro firmy** . Zkontroluje sloupec **Stav poslední synchronizace** .

### <a name="view-synchronized-apps"></a>Zobrazení synchronizovaných aplikací

V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte položku **Správa aplikací**a vyberte možnost **informace o licencích pro uzel aplikace Store** .


## <a name="log-files"></a>Soubory protokolů

### <a name="wsfbsyncworkerlog"></a>WSfBSyncWorker. log

Tento soubor protokolu je umístěný ve spojovacím bodu služby v části `\Logs` v instalačním adresáři Configuration Manager. Zaznamenává informace o komunikaci s cloudovou službou. Tyto informace zahrnují metadata, ikony, balíčky a načtení souboru s licencí.

Pokud chcete změnit úroveň protokolu, změňte `LoggingLevel` hodnotu na `0` v klíči `HKLM\SOFTWARE\Microsoft\SMS\Tracing\SMS_CLOUDCONNECTION` registru. Další informace najdete v tématu [Konfigurace možností protokolování](../../core/plan-design/hierarchy/about-log-files.md#bkmk_reg-site).

### <a name="sms_cloudconnectionlog"></a>SMS_CLOUDCONNECTION. log

Tento soubor protokolu je umístěný ve spojovacím bodu služby v části `\Logs` v instalačním adresáři Configuration Manager. Pokud služba WSfBSyncWorker není spuštěná nebo se opakovaně spouští a zastavuje, zkontrolujte položky v tomto souboru protokolu.

> [!NOTE]
> Tento soubor protokolu je sdílen s jinými funkcemi.

### <a name="businessappprocessworkerlog"></a>BusinessAppProcessWorker. log

Tento soubor protokolu je umístěný na serveru lokality pro lokalitu nejvyšší úrovně v hierarchii. `\Logs` Je to v instalačním adresáři Configuration Manager. Zaznamenává informace o následujících procesech:

- Vloží informace o metadatech synchronizovaných součástí BusinessAppProcessWorker do databáze.
- Zpracovat soubory v`\InstallDir\inboxes\businessappprocess.box`

### <a name="sms_business_app_process_managerlog"></a>SMS_BUSINESS_APP_PROCESS_MANAGER. log

Tento soubor protokolu je umístěný na serveru lokality pro lokalitu nejvyšší úrovně v hierarchii. `\Logs` Je to v instalačním adresáři Configuration Manager. Pokud služba BusinessAppProcessWorker není spuštěná nebo se opakovaně spouští a zastavuje, zkontrolujte položky v tomto souboru protokolu.



## <a name="last-sync-failed"></a>Poslední synchronizace se nezdařila.

Pokud se stav poslední synchronizace *nezdařil*, začněte kontrolou následujících [souborů protokolu](#log-files) a Identifikujte tak příznak:

- WSfbSyncWorker. log
- SMS_CLOUDCONNECTION. log

Pak se podívejte do jednoho z následujících částí, kde najdete běžné problémy:

- [Chyba autorizace](#bkmk_fail-symptom1)
- [Tajný klíč je neplatný.](#bkmk_fail-symptom2)
- [Chyba při získávání tokenu aplikace](#bkmk_fail-symptom3)
- [Umístění obsahu neexistuje nebo má nesprávná oprávnění.](#bkmk_fail-symptom4)
- [Při vytváření požadavku HTTP při volání metody GET došlo k chybě.](#bkmk_fail-symptom5)
- [Do vyrovnávací paměti nelze zapsat více bajtů.](#bkmk_fail-symptom6)

### <a name="authorization-error"></a><a name="bkmk_fail-symptom1"></a>Chyba autorizace

#### <a name="cause"></a>Příčina

K tomuto problému může dojít, pokud nakonfigurovaná aplikace Azure Active Directory (Azure AD) nemá oprávnění ke správě Microsoft Store pro firmy a vzdělávání tohoto tenanta.

#### <a name="workaround"></a>Alternativní řešení

1. Přihlaste se jako správce na Microsoft Store pro firmy nebo na portál pro vzdělávání.
1. Přejít na **Nastavení**a vyberte **Nástroje pro správu**.
1. Pokud aplikace není v seznamu uvedena, vyberte **Přidat Nástroj pro správu**. Pak hledejte podle názvu a vyberte aplikaci Azure AD přidruženou ke stejnému ClientID jako Configuration Manager.
1. Pokud se stav nezobrazuje jako **aktivní**, vyberte v části **Akce** možnost **aktivovat** .
1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **Microsoft Store pro firmy** . Proveďte synchronizaci s úložištěm nebo počkejte, než dojde k dalšímu intervalu synchronizace.

> [!Tip]
> Zjištění ClientID v Configuration Manager:
>
> 1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **Azure Active Directory Tennts** .
> 1. Vyberte tenanta, kterého používáte pro integraci Microsoft Store pro firmy a vzdělávání.
> 1. V podokně výsledků Najděte aplikaci, která odpovídá, a podívejte se na sloupec **ID klienta** .

### <a name="the-secret-key-is-invalid"></a><a name="bkmk_fail-symptom2"></a>Tajný klíč je neplatný.

#### <a name="cause"></a>Příčina

K tomuto problému může dojít, pokud vypršela platnost tajného klíče v aplikaci Azure AD pro účely konfigurace Microsoft Store pro firmy a vzdělávání.

#### <a name="resolution"></a>Řešení

Obnovte tajný klíč pro aplikaci Azure AD. Další informace najdete v tématu [obnovení tajného klíče](../../core/servers/deploy/configure/azure-services-wizard.md#bkmk_renew).

### <a name="error-getting-application-token"></a><a name="bkmk_fail-symptom3"></a>Chyba při získávání tokenu aplikace

#### <a name="cause"></a>Příčina

K tomuto problému může dojít, pokud už připojená aplikace ve službě Azure AD neexistuje.

#### <a name="resolution"></a>Řešení

Odstraňte a znovu vytvořte připojení k Microsoft Store pro firmy a vzdělávání.

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **Microsoft Store pro firmy** .
1. Vyberte existující připojení.
1. Na pásu karet vyberte **Odstranit** .

Pak znovu vytvořte připojení. Další informace najdete v těchto článcích:

- [Konfigurace služeb Azure](../../core/servers/deploy/configure/azure-services-wizard.md)
- [Nastavení Microsoft Store pro obchodní a školní synchronizaci](manage-apps-from-the-windows-store-for-business.md#bkmk_setup)

### <a name="content-location-doesnt-exist-or-incorrect-permissions"></a><a name="bkmk_fail-symptom4"></a>Umístění obsahu neexistuje nebo má nesprávná oprávnění.

#### <a name="cause"></a>Příčina

Když nastavíte Microsoft Store pro obchodní a vzdělávací připojení, zadáte sdílenou síťovou složku pro ukládání synchronizovaného obsahu. K tomuto problému může dojít, pokud tato sdílená složka neexistuje nebo má nesprávná oprávnění. Účet počítače pro spojovací bod služby by měl být vlastníkem tohoto adresáře a všech podadresářů.<!-- memdocs#146 --> Pokud tomu tak není, zobrazí se chybová zpráva podobná následující chybě:

```
Failed to download package d788cc1b-ab00-bb5f-1548-f2dfe717583b-X86-Arm for product 9WZDNCRFJ3PS\0015.
System.IO.IOException: This security ID may not be assigned as the owner of this object.
```

Pokud se chcete podívat na umístění, které jste nakonfigurovali:

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **Microsoft Store pro firmy** .

1. Vyberte účet a otevřete jeho **vlastnosti**.

1. Přepněte na kartu **Konfigurace** . Nastavení **umístění** zobrazuje síťovou cestu pro ukládání obsahu aplikace staženého z Microsoft Store pro firmy a vzdělávání.

#### <a name="workaround"></a>Alternativní řešení

1. Pokud ještě neexistuje, vytvořte sdílenou složku.

1. Ověřte oprávnění systému souborů NTFS ve složce a oprávnění ke sdílené síťové složce. Udělte účtu počítače oprávnění **ke čtení** a **zápisu** spojovacího bodu služby.

Pokud chcete změnit konfiguraci umístění, odstraňte a znovu vytvořte připojení k novému umístění obsahu.

### <a name="error-occurred-making-http-request-calling-get-method"></a><a name="bkmk_fail-symptom5"></a>Při vytváření požadavku HTTP při volání metody GET došlo k chybě.

#### <a name="cause"></a>Příčina

K tomuto problému může dojít, pokud synchronizace aplikací ze Storu trvala tak dlouho, že adresa URL obsahu vypršela.

#### <a name="workaround"></a>Alternativní řešení

Zkusit znovu proces synchronizace

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **Microsoft Store pro firmy** .
1. Vyberte připojení. Na pásu karet vyberte **synchronizovat z Microsoft Store pro firmy**.

V každém okamžiku byste měli pokračovat dál. Může to trvat několik opakování v závislosti na následujících faktorech:

- Počet offline aplikací
- Velikost balíčků
- Rychlost sítě

Při každém pokusu by se měla zobrazit chyba méně času. Pokud se počet chyb nesníží, dojde k dalšímu problému.

### <a name="cannot-write-more-bytes-to-the-buffer"></a><a name="bkmk_fail-symptom6"></a>Do vyrovnávací paměti nelze zapsat více bajtů.

#### <a name="cause"></a>Příčina

K tomuto problému může dojít, pokud je balíček aplikace větší než 500 MB. Configuration Manager podporuje pouze automatickou synchronizaci offline aplikací s balíčky menšími než 500 MB.

#### <a name="workaround"></a>Alternativní řešení

Tyto aplikace nemůžete automaticky synchronizovat, ale můžete si stáhnout obsah a ručně vytvořit aplikaci:

1. Získat ID neúspěšné aplikace z následujícího řádku v **WSfbSynWorker. log**:

    `Error(s) syncing or downloading application <ApplicationID> from the Microsoft Store for Business.`

1. Přihlaste se jako správce na Microsoft Store pro firmy nebo na portál pro vzdělávání. Najde stránku pro tuto aplikaci.

    > [!Tip]
    > Adresa URL stránky je podobná:`https://businessstore.microsoft.com/en-us/store/p/app/ApplicationID`

    1. Vyberte **offline**, pokud už není vybraný. Pak vyberte **Spravovat**.

    1. Vytvořte samostatnou složku ve sdílené složce obsahu aplikace pro všechny podporované platformy.

    1. Stáhněte balíček do složky Package.

    1. Stáhněte si soubor `.bin` s kódovanými licenčními soubory do složky balíčku.

    1. Stáhněte všechny požadované architektury do složky balíčku.

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte položku **Správa aplikací**a vyberte uzel **aplikace** .

1. [Vytvořte aplikaci](create-applications.md)a ručně určete informace o aplikaci.

    1. Vytvořte typ nasazení pro každou podporovanou platformu, kterou jste předtím stáhli.

    1. Typ: **balíček aplikace systému Windows\*(. appx \*,. appxbundle)**

    1. Zadejte appx/appxbundle pro skutečný balíček aplikace, ne požadovaný balíček závislostí.

Na stránce finální **informace o importu** potvrďte následující podrobnosti:

- **Soubor s licencí:** Určuje `.bin` soubor. Tento licenční soubor je nutný pro offline aplikace.
- **Závislosti aplikace systému Windows:** Ověřte, zda jsou pro tento balíček staženy všechny požadované závislosti.


## <a name="sync-doesnt-run"></a>Synchronizace neběží.

Tato část se zabývá následujícími problémy synchronizace:

- Proces synchronizace se spouští ručně, ale neběží.
- Lokalita se automaticky nesynchronizuje každý den

Začněte kontrolou následujících [souborů protokolu](#log-files) a Identifikujte příznak:

- BusinessAppProcessWorker. log
- SMS_BUSINESS_APP_PROCESS_MANAGER. log
- WsfbSyncWorker. log
- SMS_CLOUDCONNECTION. log

Pak se podívejte do jednoho z následujících částí, kde najdete běžné problémy:

- [Ruční synchronizace se nespustí.](#bkmk_sync-symptom1)
- [Automatická denní synchronizace se nespustí a v SMS_BUSINESS_APP_PROCESS_MANAGER. log se vypíná počet pracovních procesů.](#bkmk_sync-symptom2)

### <a name="manual-sync-doesnt-start"></a><a name="bkmk_sync-symptom1"></a>Ruční synchronizace se nespustí.

#### <a name="cause"></a>Příčina

K tomuto problému může dojít, Pokud zahájíte synchronizaci za méně než 10 minut po předchozí synchronizaci. Nemůžete synchronizovat častěji než každých 10 minut.

#### <a name="resolution"></a>Řešení

Před zahájením další synchronizace počkejte aspoň 10 minut.

### <a name="automatic-daily-sync-doesnt-run-and-shutting-down--workers-error-in-sms_business_app_process_managerlog"></a><a name="bkmk_sync-symptom2"></a>Automatická denní synchronizace se nespustí a v SMS_BUSINESS_APP_PROCESS_MANAGER. log se vypíná počet pracovních procesů.

#### <a name="cause"></a>Příčina

K tomuto problému může dojít, pokud komponenta SMS_BUSINESS_APP_PROCESS_MANAGER zastaví vlákno WsfbSyncWorker. Chyba může určit buď `2` pracovní procesy `4` , nebo.

#### <a name="workaround"></a>Alternativní řešení

Restartujte službu **SMS_Executive** .

Pokud tuto hlavní službu nemůžete restartovat, zastavte obě součásti s pracovními procesy MSfB a pak spusťte obě tyto možnosti:

1. Otevřete registr systému Windows na serveru, na kterém je spuštěn spojovací bod služby.

1. Přejděte na `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_CLOUDCONNECTION`.

    1. Nastavte požadovanou operaci na **zastavení**.

    1. Aktualizace pro ověření aktuálního stavu = **Zastaveno**.

1. Přejděte na `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_BUSINESS_APP_PROCESS_MANAGER`.

    1. Nastavte požadovanou operaci na **zastavení**.

    1. Aktualizace pro ověření aktuálního stavu = **Zastaveno**.

1. V **SMS_CLOUDCONNECTION**nastavte požadovanou operaci na **Start**.

1. V **SMS_BUSINESS_APP_PROCESS_MANAGER**nastavte požadovanou operaci na **Start**.


## <a name="language-related-issues"></a>Problémy související s jazykem

Tato část obsahuje následující běžné problémy:

- [Změny výběru jazyka nejsou aplikovány](#bkmk_lang-symptom1)
- [Ne všechny vybrané jazyky jsou k dispozici pro všechny informace o licenci.](#bkmk_lang-symptom2)

### <a name="language-selection-changes-arent-applied"></a><a name="bkmk_lang-symptom1"></a>Změny výběru jazyka nejsou aplikovány

#### <a name="cause"></a>Příčina

K tomuto problému může dojít, pokud je výběr jazyka uložen do mezipaměti a není vymazán po změně hodnot vlastností.

#### <a name="workaround"></a>Alternativní řešení

Chcete-li tento problém vyřešit, restartujte službu **SMS_Executive** .

### <a name="not-all-selected-languages-are-present-for-all-license-information"></a><a name="bkmk_lang-symptom2"></a>Ne všechny vybrané jazyky jsou k dispozici pro všechny informace o licenci.

#### <a name="cause"></a>Příčina

K tomuto problému může dojít, pokud informace o licencích aplikace Microsoft Store for Business a školství neobsahují lokalizovaná data pro zadaný jazyk.

#### <a name="workaround"></a>Alternativní řešení

Ručně přidejte chybějící jazyky pro vytvořené aplikace.


## <a name="offline-applications"></a>Offline aplikace

Tato část obsahuje následující běžné problémy:

- [Nepodařilo se vytvořit offline aplikaci, protože obsah nelze ověřit.](#bkmk_off-symptom1)
- [Nepodařilo se nainstalovat aplikaci vytvořenou z offline informací o licenci.](#bkmk_off-symptom2)

### <a name="fail-to-create-offline-application-because-content-cant-be-verified"></a><a name="bkmk_off-symptom1"></a>Nepodařilo se vytvořit offline aplikaci, protože obsah nelze ověřit.

#### <a name="cause"></a>Příčina

K tomuto problému může dojít, pokud je synchronizovaný obsah pro offline aplikaci poškozený nebo změněný.

#### <a name="workaround"></a>Alternativní řešení

Spusťte novou synchronizaci. Po dokončení synchronizace by se měla ověřit a stáhnout všechny nesprávné soubory obsahu.

### <a name="fail-to-install-application-created-from-offline-license-information"></a><a name="bkmk_off-symptom2"></a>Nepodařilo se nainstalovat aplikaci vytvořenou z offline informací o licenci.

#### <a name="cause"></a>Příčina

K tomuto problému může dojít, pokud nasadíte aplikaci na klienta s verzí Windows 10 starší než verze 1511. Licencované aplikace offline z Microsoft Store pro firmy a vzdělávání se podporují jenom ve Windows 10 verze 1511 a novějších.

#### <a name="resolution"></a>Řešení

Nainstalujte nejnovější verzi Windows 10.


## <a name="next-steps"></a>Další kroky

Další nápovědu najdete v tématu [hledání pomoci při použití Configuration Manager](../../core/understand/find-help.md).
