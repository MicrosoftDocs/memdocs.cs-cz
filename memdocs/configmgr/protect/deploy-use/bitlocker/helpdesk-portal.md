---
title: Web pro správu a monitorování BitLockeru
titleSuffix: Configuration Manager
description: Jak používat web pro správu a monitorování BitLockeru (portál helpdesk) v Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 81f03922-90f6-4e8f-be65-da64ccb21cf2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 84725ac494e1d9497524303b841207bd05cd3859
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717507"
---
# <a name="bitlocker-administration-and-monitoring-website"></a>Web pro správu a monitorování BitLockeru

*Platí pro: Configuration Manager (Current Branch)*

<!--3601034-->

Web pro správu a monitorování BitLockeru je rozhraní pro správu nástroj BitLocker Drive Encryption. Také se označuje jako portál helpdesku. Tento web slouží ke kontrole sestav, obnovení jednotek uživatelů a správě čipy TPM zařízení.

[![Snímek obrazovky s výchozím webem pro správu a monitorování nástrojem BitLocker](media/bitlocker-helpdesk-website.png)](media/bitlocker-helpdesk-website.png#lightbox)

Než ho budete moct používat, nainstalujte tuto komponentu na webový server. Další informace najdete v tématu [nastavení a vytváření sestav a portálů nástroje BitLocker](setup-websites.md).

Přístup k webu pro správu a monitorování prostřednictvím následující adresy URL:`https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> **Sestavu auditu obnovení** můžete zobrazit na webu Správa a monitorování. Do bodu služby Reporting Services přidáte další sestavy správy nástroje BitLocker. Další informace najdete v tématu [zobrazení sestav nástroje BitLocker](view-reports.md).

## <a name="groups"></a>Skupiny

Pro přístup ke konkrétním oblastem webu pro správu a monitorování musí být váš uživatelský účet v jedné z následujících skupin. Vytvořte tyto skupiny ve službě Active Directory s libovolným požadovaným názvem. Při instalaci tohoto webu zadáte názvy těchto skupin. Další informace najdete v tématu [nastavení a vytváření sestav a portálů nástroje BitLocker](setup-websites.md).

|Skupina|Popis|
|--- |--- |
|Správci oddělení technické podpory nástroje BitLocker|Poskytuje přístup ke všem oblastem webu pro správu a monitorování. Když uživateli pomůžete obnovit své jednotky, zadáte pouze obnovovací klíč, nikoli doménu a uživatelské jméno. Pokud je uživatel členem této skupiny i skupiny uživatelů helpdesku nástroje BitLocker, oprávnění skupiny pro správu přepíší oprávnění skupiny uživatelů.|
|Uživatelé oddělení technické podpory BitLockeru|Poskytuje přístup ke správě oblasti obnovení **čipu TPM** a **jednotky** na webu pro správu a monitorování. Když použijete kteroukoli z těchto oblastí, musíte vyplnit všechna pole včetně názvu domény a účtu uživatele. Pokud je uživatel členem této skupiny i skupiny Helpdesk Helpdesk Admins, oprávnění skupiny správců přepíšou oprávnění skupiny uživatelů.|
|Uživatelé sestav nástroje BitLocker|Poskytuje přístup k oblasti **sestav** na webu pro správu a monitorování.|

## <a name="manage-tpm"></a>Správa čipu TPM

Pokud uživatel zadá nesprávný kód PIN příliš mnohokrát, může zamknout čip TPM. Počet, kolikrát může uživatel zadat nesprávný kód PIN před tím, než se zámky čipu TPM budou lišit od výrobce až po výrobce. Z oblasti **Spravovat čip TPM** na webu pro správu a monitorování získáte přístup k centralizovanému systému dat pro obnovení klíčů.

Další informace o vlastnictví čipu TPM najdete v tématu [Konfigurace MBAM pro v úschověí čipu TPM a ukládání hesel OwnerAuth](https://docs.microsoft.com/microsoft-desktop-optimization-pack/mbam-v25/mbam-25-security-considerations#bkmk-tpm).

> [!NOTE]
> Od verze 1607 Windows 10 neuchovává Windows při zřizování čipu TPM heslo vlastníka čipu TPM.

1. Ve webovém prohlížeči přejdete na web pro správu a monitorování, například `https://webserver.contoso.com/HelpDesk`.

1. V levém podokně vyberte **Spravovat oblast TPM** .

    ![Web pro správu a monitorování nástroje BitLocker Správa stránky TPM](media/bitlocker-admin-manage-tpm.png)

1. Zadejte plně kvalifikovaný název domény pro počítač a název počítače.

1. V případě potřeby zadejte doménu a uživatelské jméno uživatele pro načtení souboru hesla vlastníka čipu TPM.

1. Vyberte jednu z následujících možností z **důvodu vyžádání souboru hesla vlastníka čipu TPM**:

    - Resetovat uzamčení kódu PIN
    - Zapnout čip TPM
    - Vypnout čip TPM
    - Změnit heslo TPM
    - Vymazat čip TPM
    - Ostatní

    Po **odeslání** formuláře webová stránka vrátí jednu z následujících odpovědí:

    - Pokud se nedaří najít odpovídajícího souboru hesla vlastníka čipu TPM, vrátí chybovou zprávu.

    - Soubor hesla vlastníka čipu TPM pro odeslaný počítač

    Po načtení souboru hesla vlastníka čipu TPM se na webu zobrazí heslo vlastníka.

1. Pokud chcete uložit heslo do souboru, vyberte **Uložit**.

1. V oblasti **Spravovat čip TPM** vyberte možnost **resetovat uzamčení čipu TPM** a zadejte soubor hesla vlastníka čipu TPM.

    Uzamčení čipu TPM se resetuje. BitLocker obnoví přístup uživatele k zařízení.

    > [!IMPORTANT]
    > Nesdílejte hodnotu hash čipu TPM ani soubor hesla vlastníka čipu TPM.

## <a name="drive-recovery"></a>Obnovení jednotky

### <a name="recover-a-drive-in-recovery-mode"></a><a name="bkmk_recovery"></a>Obnovení jednotky v režimu obnovení

Jednotky přejde do režimu obnovení v následujících scénářích:

- Uživatel ztratí kód PIN nebo heslo nebo ho zapomene.
- ČIP TPM (Trusted Module Platform) detekuje změny systému BIOS nebo spouštěcích souborů počítače.

Chcete-li získat heslo pro obnovení, použijte oblast **obnovení jednotky** na webu pro správu a monitorování.

> [!IMPORTANT]
> Platnost hesel pro obnovení vyprší po jednom použití. Na jednotkách operačního systému a pevných datových jednotkách se pravidlo jediného použití automaticky použije. Na vyměnitelných jednotkách se použije, když jednotku odeberete a znovu vložíte.

1. Ve webovém prohlížeči přejdete na web pro správu a monitorování, například `https://webserver.contoso.com/HelpDesk`.

1. V levém podokně vyberte oblast **obnovení jednotky** .

    ![Stránka pro obnovení ovladače pro správu a monitorování nástroje BitLocker](media/bitlocker-admin-drive-recovery.png)

1. V případě potřeby zadejte doménu uživatele a uživatelské jméno pro zobrazení informací o obnovení.

1. Pokud chcete zobrazit seznam možných vyhovujících klíčů obnovení, zadejte prvních osm číslic ID obnovení klíče. Pokud chcete získat přesný obnovovací klíč, zadejte celé ID obnovovacího klíče.

1. Jako **důvod pro odemčení jednotky**vyberte jednu z následujících možností:

    - Pořadí spouštění operačního systému se změnilo.
    - Systém BIOS změněn
    - Změněné soubory operačního systému
    - Ztracený spouštěcí klíč
    - Ztracený PIN kód
    - Resetování čipu TPM
    - Ztracené heslo
    - Ztracená karta SmartCard
    - Ostatní

    Po **odeslání** formuláře webová stránka vrátí jednu z následujících odpovědí:

    - Pokud má uživatel více odpovídajících hesel pro obnovení, vrátí více možných shod.

    - Heslo pro obnovení a balíček pro obnovení pro odeslaného uživatele

        > [!NOTE]
        > Pokud obnovujete poškozenou jednotku, možnost balíček pro obnovení poskytne nástroji BitLocker kritické informace, které potřebuje k obnovení jednotky.

    - Pokud nemůže najít vyhovující heslo pro obnovení, vrátí chybovou zprávu.

    Po načtení hesla pro obnovení a balíčku pro obnovení se na webu zobrazí heslo pro obnovení.

1. Chcete-li zkopírovat heslo, vyberte možnost **Kopírovat klíč**. Chcete-li uložit heslo pro obnovení do souboru, vyberte možnost **Uložit**.

Pokud chcete jednotku odemknout, zadejte heslo pro obnovení nebo použijte balíček pro obnovení.

### <a name="recover-a-moved-drive"></a><a name="bkmk_moved"></a>Obnovení přesunuté jednotky

Když přesunete jednotku do nového počítače, protože se liší od čipu TPM, BitLocker nepřijímá předchozí PIN kód. Pro obnovení přesunuté jednotky Získejte ID obnovovacího klíče, které načte heslo pro obnovení.

K obnovení přesunuté jednotky použijte oblast **obnovení jednotky** na webu Správa a monitorování.

1. V počítači s přesunutou jednotkou spusťte počítač v režimu Windows Recovery Environment (WinRE).

1. V rozhraní WinRE nástroj BitLocker považuje přesunutou jednotku operačního systému za pevnou datovou jednotku. BitLocker zobrazuje ID hesla pro obnovení jednotky a vyzve k zadání hesla pro obnovení.

    > [!NOTE]
    > V některých situacích během procesu spuštění vyberte možnost **zapomenutí PIN kódu** , pokud je dostupná možnost. Pak přejděte do režimu obnovení a zobrazte ID obnovovacího klíče.

1. K získání hesla pro obnovení z webu pro správu a monitorování použijte ID obnovovacího klíče. Další informace najdete v tématu [obnovení jednotky v režimu obnovení](#bkmk_recovery).

Pokud jste přesunutou jednotku nakonfigurovali tak, aby používala čip TPM v původním počítači, proveďte následující kroky. V opačném případě je proces obnovení dokončen.

1. Po odemčení jednotky spusťte počítač v režimu WinRE. Otevřete příkazový řádek v WinRE a pomocí `manage-bde` příkazu dešifrujte jednotku. Tento nástroj je jediným způsobem, jak odebrat ochranu pomocí **čipu TPM a PIN kódu** bez původního čipu TPM. Další informace o tomto příkazu najdete v tématu [Manage-bde](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-managebde).

1. Až to bude hotové, spusťte počítač normálně. Configuration Manager vynutila zásadu nástroje BitLocker k šifrování jednotky pomocí čipu TPM a kódu PIN nového počítače.

### <a name="recover-a-corrupted-drive"></a><a name="bkmk_corrupted"></a>Obnovení poškozené jednotky

K získání balíčku obnovovacího klíče z webu pro správu a monitorování použijte ID obnovovacího klíče. Další informace najdete v tématu [obnovení jednotky v režimu obnovení](#bkmk_recovery).

1. Uložte **balíček obnovovacího klíče** do počítače a pak ho zkopírujte do počítače s poškozenou jednotkou.

1. Otevřete příkazový řádek jako správce a zadejte následující příkaz:

    `repair-bde <corrupted drive> <fixed drive> -kp <key package> -rp <recovery password>`

    Nahraďte následující hodnoty:

    - `<corrupted drive>`: Písmeno jednotky poškozené jednotky, například`D:`
    - `<fixed drive>`: Písmeno jednotky dostupné jednotky pevného disku podobné nebo větší velikosti než poškozená jednotka. BitLocker obnoví a přesune data na poškozené jednotce na určenou jednotku. Všechna data na této jednotce jsou přepsána.
    - `<key package>`: Umístění balíčku obnovovacího klíče
    - `<recovery password>`: Přidružené heslo pro obnovení

    Příklad:

    `repair-bde C: D: -kp F:\RecoveryKeyPackage -rp 111111-222222-333333-444444-555555-666666-777777-888888`

Další informace o tomto příkazu najdete v tématu [Repair-BDE](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-repairbde).

## <a name="reports"></a>Sestavy

Web pro správu a monitorování zahrnuje **sestavu audit Recovery**. Další sestavy jsou k dispozici v Configuration Manager bodu služby Reporting Services. Další informace najdete v tématu [zobrazení sestav nástroje BitLocker](view-reports.md).

1. Ve webovém prohlížeči přejdete na web pro správu a monitorování, například `https://webserver.contoso.com/HelpDesk`.

1. V levém podokně vyberte oblast **sestavy** .

1. V horním řádku nabídek vyberte **sestavu audit Recovery**.

Další informace o této sestavě najdete v tématu [Sestava auditu obnovení](view-reports.md#bkmk-audit) .

> [!TIP]
> Chcete-li uložit výsledky sestavy, vyberte možnost **exportovat** na řádku nabídek **sestavy** .
