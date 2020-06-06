---
title: Nasazení správy nástroje BitLocker
titleSuffix: Configuration Manager
description: Nasazení agenta pro správu nástroje BitLocker pro Configuration Manager klientů a služby obnovení do bodů správy
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 39aa0558-742c-4171-81bc-9b1e6707f4ea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e33ba8df84239b4a438ff0c526bb255c5b7d0052
ms.sourcegitcommit: e618ea7cb864635c838b672bc71a1e926bf7c047
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2020
ms.locfileid: "84458147"
---
# <a name="deploy-bitlocker-management"></a>Nasazení správy nástroje BitLocker

*Platí pro: Configuration Manager (Current Branch)*

<!--3601034-->

Správa BitLockeru v Configuration Manager zahrnuje tyto komponenty:

- **Agent správy BitLockeru**: Configuration Manager povolí tohoto agenta na zařízení, když [vytvoříte zásadu](#create-a-policy) a [nasadíte ji do kolekce](#deploy-a-policy).

- **Služba obnovení**: součást serveru, která přijímá data obnovení nástroje BitLocker od klientů. Další informace najdete v tématu [Služba Recovery Services](#recovery-service).

Před vytvořením a nasazením zásad správy BitLockeru postupujte takto:

- Kontrola [požadavků](../../plan-design/bitlocker-management.md#prerequisites)

- V případě potřeby [Zašifrujte klíče pro obnovení](encrypt-recovery-data.md) v databázi lokality.

## <a name="create-a-policy"></a>Vytvoření zásad

Když tuto zásadu vytvoříte a nasadíte, povolí klient Configuration Manager v zařízení agenta pro správu BitLockeru.

> [!NOTE]
> K vytvoření zásady správy BitLockeru potřebujete roli **úplného správce** v Configuration Manager.

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** , rozbalte položku **Endpoint Protection**a vyberte uzel **Správa nástroje BitLocker** .

1. Na pásu karet vyberte **vytvořit zásadu řízení správy nástroje BitLocker**.

1. Na stránce **Obecné** zadejte název a volitelný popis. Vyberte komponenty, které chcete povolit na klientech s touto zásadou:  

    - **Jednotka operačního systému**: umožňuje řídit, jestli je jednotka operačního systému zašifrovaná.

    - **Pevná jednotka**: Správa šifrování dalších datových jednotek v zařízení

    - **Vyměnitelná jednotka**: Správa šifrování pro jednotky, které můžete odebrat ze zařízení, jako je USB klíč

    - **Správa klientů**: Správa služby obnovení klíčů zálohování nástroj BitLocker Drive Encryption informací o obnovení  

1. Na stránce **instalace** nakonfigurujte následující globální nastavení pro nástroj BitLocker Drive Encryption:

    > [!NOTE]
    > Configuration Manager tato nastavení platí, když povolíte BitLocker. Pokud je jednotka už zašifrovaná nebo probíhá, změna těchto nastavení zásad nemění na zařízení šifrování jednotky.
    >
    > Pokud tato nastavení zakážete nebo nenakonfigurujete, BitLocker použije výchozí metodu šifrování (AES 128-bit).

    - U zařízení Windows 8.1 Povolte možnost **Metoda šifrování jednotky a sílu šifrování**. Pak vyberte metodu šifrování.

    - U zařízení s Windows 10 povolte možnost **Metoda šifrování jednotky a sílu šifrování (Windows 10)**. Pak jednotlivě vyberte metodu šifrování pro jednotky operačního systému, pevné datové jednotky a vyměnitelné datové jednotky.

    Další informace o těchto a dalších nastaveních na této stránce najdete v tématu [Nastavení reference –](../../tech-ref/bitlocker/settings.md#setup)nastavení.

1. Na stránce **jednotka operačního systému** zadejte následující nastavení:  

    - **Nastavení šifrování jednotky operačního systému**: Pokud povolíte toto nastavení, uživatel bude chránit jednotku operačního systému a BitLocker zašifruje jednotku. Pokud ho zakážete, uživatel nebude moct chránit jednotku.  

    V zařízeních s kompatibilním čipem TPM lze při spuštění použít dva typy metod ověřování, aby byla zajištěna ochrana šifrovaných dat. Když se počítač spustí, může použít jenom čip TPM k ověřování, nebo může taky vyžadovat zadání osobního identifikačního čísla (PIN). Nakonfigurujte tahle nastavení:

    - **Vyberte ochranu pro jednotku operačního systému**: nakonfigurujte ji tak, aby používala čip TPM a kód PIN, nebo jenom čip TPM.

    - **Nakonfigurovat minimální délku PIN kódu pro spuštění**: Pokud POŽADUJETE kód PIN, je tato hodnota nejkratší délka, kterou může uživatel zadat. Uživatel zadá tento kód PIN, když se počítač spustí k odemknutí jednotky. Ve výchozím nastavení je minimální délka kódu PIN `4` .

    Další informace o těchto a dalších nastaveních na této stránce najdete v tématu [nastavení referenčního operačního systému na jednotce s operačním systémem](../../tech-ref/bitlocker/settings.md#os-drive).

1. Na stránce **pevný disk** zadejte následující nastavení:

    - **Šifrování pevné datové jednotky**: Pokud povolíte toto nastavení, nástroj BitLocker vyžaduje, aby uživatelé do ochrany umístili všechny pevné datové jednotky. Pak šifruje datové jednotky. Pokud tuto zásadu povolíte, povolte možnost automatické odemknutí nebo nastavení zásad pro **hesla pro pevné datové jednotky**.

    - **Konfigurovat Automatické odemknutí pevné datové jednotky**: povolí nebo vyžádá BitLocker k automatickému odemknutí jakékoli šifrované datové jednotky. Chcete-li použít automatické odemknutí, nástroj také vyžaduje nástroj BitLocker k šifrování jednotky operačního systému.

    Další informace o těchto a dalších nastaveních na této stránce najdete v části [Nastavení reference-pevná jednotka](../../tech-ref/bitlocker/settings.md#fixed-drive).

1. Na stránce **vyměnitelná jednotka** určete následující nastavení:

    - **Šifrování vyměnitelných datových jednotek**: Pokud povolíte toto nastavení a povolíte uživatelům použít ochranu bitlockerem, klient Configuration Manager uloží informace o obnovení vyměnitelných jednotek do služby obnovení v bodu správy. Toto chování umožňuje uživatelům obnovení jednotky, pokud zapomenou nebo ztratí ochranu (heslo).

    - **Povolit uživatelům použít ochranu bitlockerem na vyměnitelných datových jednotkách**: uživatelé můžou zapnout ochranu nástrojem BitLocker pro vyměnitelnou jednotku.

    - **Zásada pro vyměnitelné datové jednotky**: Tato nastavení použijte k nastavení omezení pro hesla pro odemknutí vyměnitelných jednotek chráněných bitlockerem.

    Další informace o těchto a dalších nastaveních na této stránce najdete v části [Nastavení odkazy – vyměnitelná jednotka](../../tech-ref/bitlocker/settings.md#removable-drive).

1. Na stránce **Správa klienta** zadejte následující nastavení:

    > [!IMPORTANT]
    > Pokud nemáte bod správy s webem podporujícím protokol HTTPS, toto nastavení nekonfigurujte. Další informace najdete v tématu [Služba Recovery Services](#recovery-service).

    - **Konfigurace služby správy BitLockeru**: Pokud povolíte toto nastavení, Configuration Manager automaticky a tiše zálohuje informace o obnovení klíčů v databázi lokality. Pokud toto nastavení zakážete nebo nenakonfigurujete, Configuration Manager neuloží informace o obnovení klíče.

        - **Vyberte informace pro obnovení BitLockeru k uložení**: Nakonfigurujte je tak, aby používaly heslo pro obnovení a balíček klíčů, nebo jenom heslo pro obnovení.

        - **Povolí ukládání informací pro obnovení do prostého textu**: bez šifrovacího certifikátu pro správu nástroje BitLocker Configuration Manager ukládá informace pro obnovení klíče do prostého textu. Další informace najdete v tématu [šifrování dat pro obnovení](encrypt-recovery-data.md).

    Další informace o těchto a dalších nastaveních na této stránce najdete v tématu [Nastavení reference – Správa klientů](../../tech-ref/bitlocker/settings.md#client-management).

1. Dokončete průvodce.

Chcete-li změnit nastavení existující zásady, vyberte ji v seznamu a vyberte možnost **vlastnosti**.

Když vytvoříte více než jednu zásadu, můžete nakonfigurovat jejich relativní prioritu. Pokud nasadíte do klienta více zásad, použije se k určení jeho nastavení hodnota priority.

## <a name="deploy-a-policy"></a>Nasazení zásady

1. Vyberte existující zásadu v uzlu **Správa nástroje BitLocker** . Na pásu karet vyberte **nasadit**.

1. Jako cíl nasazení vyberte kolekci zařízení.

1. Pokud chcete, aby zařízení mohl kdykoli šifrovat nebo dešifrovat jednotky, vyberte možnost pro **Povolení nápravy mimo časové období údržby**. Pokud má kolekce nějaké časové intervaly pro správu a údržbu, pořád tuto zásadu BitLockeru opraví.

1. Nakonfigurujte **jednoduchý** nebo **vlastní** plán. Klient vyhodnotí své dodržování předpisů na základě nastavení určeného v plánu.

1. Vyberte **OK** a Nasaďte zásadu.

Můžete vytvořit více nasazení stejné zásady. Chcete-li zobrazit další informace o každém nasazení, vyberte zásadu v uzlu **Správa nástroje BitLocker** a potom v podokně podrobností přepněte na kartu **nasazení** .

## <a name="monitor"></a>Monitorování

V podokně podrobností uzlu **Správa BitLockeru** si prohlédněte statistiku základního dodržování předpisů týkající se nasazení zásad:

- Počet dodržování předpisů
- Počet selhání
- Počet nedodržení předpisů

Přepněte na kartu **nasazení** , aby se zobrazilo procento dodržování předpisů a doporučená akce. Vyberte nasazení a pak na pásu karet vyberte **Zobrazit stav**. Tato akce přepne zobrazení do pracovního prostoru **monitorování** , uzel **nasazení** . Podobně jako u nasazení jiných nasazení zásad konfigurace uvidíte v tomto zobrazení podrobnější stav dodržování předpisů.

Informace o tom, proč klienti hlásí, že nedodržují předpisy zásad správy BitLockeru, najdete v tématu [kódy nekompatibility](../../tech-ref/bitlocker/non-compliance-codes.md).

Další informace o řešení potíží najdete v tématu [řešení potíží s nástrojem BitLocker](../../tech-ref/bitlocker/troubleshoot.md).

K monitorování a odstraňování potíží použijte následující protokoly:

### <a name="client-logs"></a>Protokoly klienta

- Protokol událostí MBAM: ve Windows Prohlížeč událostí přejděte do části aplikace a služby > Microsoft > Windows > MBAM.  Další informace najdete v tématu [protokoly událostí BitLockeru](../../tech-ref/bitlocker/about-event-logs.md) a [protokoly událostí klienta](../../tech-ref/bitlocker/client-event-logs.md).

- **BitlockerMangementHandler. log** v cestě klientských protokolů `%WINDIR%\CCM\Logs` ve výchozím nastavení

### <a name="management-point-logs-recovery-service"></a>Protokoly bodu správy (služba obnovení)

- Protokol událostí služby Recovery Services: v Prohlížeč událostí Windows přejděte do části aplikace a služby > Microsoft > Windows > MBAM-Web. Další informace najdete v tématu [protokoly událostí BitLockeru](../../tech-ref/bitlocker/about-event-logs.md) a [protokoly událostí serveru](../../tech-ref/bitlocker/server-event-logs.md).

- Protokoly trasování služby obnovení:`<Default IIS Web Root>\Microsoft BitLocker Management Solution\Logs\Recovery And Hardware Service\trace*.etl`

## <a name="recovery-service"></a>Služba obnovení

Služba obnovení BitLockeru je součást serveru, která přijímá data obnovení nástroje BitLocker od klientů Configuration Manager. Lokalita nasadí službu obnovení při vytváření zásad správy BitLockeru. Configuration Manager automaticky nainstaluje službu obnovení do každého bodu správy pomocí webu s podporou protokolu HTTPS.

Configuration Manager ukládá informace o obnovení do databáze lokality. Bez šifrovacího certifikátu pro správu nástroje BitLocker Configuration Manager ukládá informace o obnovení klíče do prostého textu.

Další informace najdete v tématu [šifrování dat pro obnovení](encrypt-recovery-data.md).

## <a name="migration-considerations"></a>Posouzení migrace

Pokud aktuálně používáte nástroj Microsoft BitLocker Administration and Monitoring (MBAM), můžete plynule migrovat správu na Configuration Manager. Když nasadíte zásady správy BitLockeru v Configuration Manager, klienti automaticky odesílají klíče a balíčky pro obnovení do služby Configuration Manager Recovery Services.

> [!IMPORTANT]
> Pokud provádíte migraci ze samostatného MBAMu na Configuration Manager správu BitLockeru a potřebujete existující funkce samostatného MBAM, nepoužívejte samostatné servery MBAM nebo komponenty se správou nástroje BitLocker Configuration Manager. Pokud tyto servery znovu použijete, samostatné MBAM přestane fungovat, když Configuration Manager Správa BitLockeru nainstaluje své komponenty na tyto servery. Nespouštějte skript MBAMWebSiteInstaller. ps1 a nastavte portály BitLocker na samostatné servery MBAM. Při nastavování Configuration Manager správy BitLockeru použijte samostatné servery.

### <a name="group-policy"></a>Zásady skupiny

- Nastavení správy BitLockeru jsou plně kompatibilní s nastavením zásad skupiny MBAM. Pokud zařízení dostanou nastavení zásad skupiny i zásady Configuration Manager, nakonfigurujte je tak, aby odpovídaly.

- Configuration Manager neimplementuje všechna nastavení zásad skupiny MBAM. Pokud v zásadách skupiny nakonfigurujete další nastavení, agent pro správu BitLockeru na Configuration Manager klientech respektují tato nastavení.

### <a name="tpm-password-hash"></a>Hodnota hash hesla TPM

- Předchozí klienti MBAM neodesílají hodnotu hash hesla TPM do Configuration Manager. Klient odešle hodnotu hash hesla čipu TPM pouze jednou.

- Pokud potřebujete tyto informace migrovat do služby Configuration Manager Recovery Services, vymažte na zařízení čip TPM. Po restartování odešle služba obnovení novou hodnotu hash hesla čipu TPM.

### <a name="re-encryption"></a>Opětovné šifrování

Configuration Manager nešifruje jednotky, které jsou již chráněny pomocí nástroj BitLocker Drive Encryption. Pokud nasadíte zásadu správy BitLockeru, která neodpovídá aktuální ochraně jednotky, ohlásí se jako nedodržující předpisy. Jednotka je pořád chráněná.

Například jste použili MBAM k zašifrování jednotky bez ochrany kódem PIN, ale zásady Configuration Manager vyžadují PIN kód. Tato jednotka není kompatibilní se zásadami, a to i v případě, že je jednotka zašifrovaná.

Pokud chcete tento problém obejít, nejdřív na zařízení zakažte nástroj BitLocker. Pak nasaďte novou zásadu s novým nastavením.

## <a name="co-management-and-intune"></a>Společná správa a Intune

<!-- SCCMDocs#2321 -->

Obslužná rutina klienta Configuration Manager pro BitLocker se spolupracuje. Pokud je zařízení spoluspravované a přepnete [Endpoint Protection úlohy](../../../comanage/workloads.md#endpoint-protection) do Intune, bude klient Configuration Manager ignorovat zásady BitLockeru. Zařízení získá zásady šifrování Windows z Intune.

Když přepnete autority pro správu šifrování, naplánujte [opakované šifrování](#re-encryption).

Další informace o správě nástroje BitLocker s Intune najdete v následujících článcích:

- [Použití šifrování zařízení s Intune](../../../../intune/protect/encrypt-devices.md)
- [Řešení potíží se zásadami BitLockeru v Microsoft Intune](../../../../intune/protect/troubleshoot-bitlocker-policies.md)

## <a name="next-steps"></a>Další kroky

[Nastavení a vytváření sestav a portálů nástroje BitLocker](setup-websites.md)
