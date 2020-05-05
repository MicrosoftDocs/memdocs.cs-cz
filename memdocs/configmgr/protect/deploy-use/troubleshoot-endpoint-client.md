---
title: Řešení potíží se službou Endpoint Protection
titleSuffix: Configuration Manager
description: Naučte se řešit problémy s Windows Defenderem a Endpoint Protection.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: efd31eaee987a7e28557cf0601608ca97c914999
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724486"
---
# <a name="troubleshoot-windows-defender-or-endpoint-protection-client"></a>Řešení potíží s programem Windows Defender nebo klientem Endpoint Protection

*Platí pro: Configuration Manager (Current Branch)*

Pokud k problémům v programu Windows Defender nebo Endpoint Protection dochází, použijte k řešení následujících problémů Tento článek:  

- [Aktualizace programu Windows Defender nebo Endpoint Protection](#update-windows-defender-or-endpoint-protection)  
- [Spuštění služby Windows Defender nebo Endpoint Protection](#starting-windows-defender-or-endpoint-protection-service)  
- [Problémy s připojením k internetu](#internet-connection-issues)  
- [Zjištěná hrozba se nedá opravit.](#detected-threat-cant-be-remediated)  

## <a name="update-windows-defender-or-endpoint-protection"></a> Aktualizace programu Windows Defender nebo aplikace Endpoint Protection

### <a name="symptoms"></a>Příznaky

Program Windows Defender nebo Endpoint Protection pracuje automaticky s Microsoft Update, aby se zajistilo aktuálnost definic virů a spywaru.  

Tato část řeší běžné problémy s automatickými aktualizacemi, včetně těchto situací:  

- Zobrazí se chybové zprávy, které oznamují, že se aktualizace nezdařila.  

- Při kontrole aktualizací se zobrazí chybová zpráva s upozorněním, že aktualizace definic virů a spywaru není možné zkontrolovat, stáhnout nebo nainstalovat.  

- I když je zařízení připojené k Internetu, aktualizace se nezdaří.  

- Aktualizace se neinstalují automaticky podle plánu.  

### <a name="causes"></a>Příčiny

Mezi nejběžnější příčiny problémů s aktualizací dochází k problémům s připojením k Internetu. Pokud víte, že je zařízení připojené k Internetu, protože můžete přejít na jiné weby, problém může způsobovat konflikty s nastavením Internetu ve Windows.  

### <a name="options-to-resolve"></a>Možnosti, které se mají vyřešit

#### <a name="step-1-reset-your-internet-settings"></a>Krok 1: resetování nastavení Internetu  

1. Ukončete všechny spuštěné programy, včetně webového prohlížeče.  

    > [!NOTE]  
    > Když resetujete tato nastavení Internetu, může odstranit vaše prohlížeče dočasné soubory, soubory cookie, historii procházení a online hesla. Neodstraní vaše oblíbené položky.  

2. Přejděte do nabídky **Start** a otevřete `inetcpl.cpl`.  

3. Přepněte na kartu **Upřesnit** .  

4. V části **Obnovení nastavení aplikace Internet Explorer**vyberte možnost **resetovat**a pak pro potvrzení vyberte znovu možnost **resetovat** .  

5. Po resetování nastavení vyberte **OK** .

6. Zkuste znovu aktualizovat program Windows Defender.

Pokud se problém nevyřeší, pokračujte k dalšímu kroku.  

#### <a name="step-2-make-sure-that-the-date-and-time-are-set-correctly-on-your-computer"></a>Krok 2: Ujistěte se, že je na vašem počítači správně nastavené datum a čas.  

Pokud chybová zpráva obsahuje kód 0x80072F8F, problém je pravděpodobně způsoben nesprávným nastavením data nebo času ve vašem počítači. Přejděte do nabídky **Start** , vyberte **Nastavení**, vyberte **čas & jazyk**a vyberte **Datum & čas**.

#### <a name="step-3-rename-the-software-distribution-folder-on-your-computer"></a>Krok 3: přejmenování složky distribuce softwaru v počítači  

1. Zastavte službu **web Windows Update** .  

    1. Pokračujte na **Start**a otevřete **Services. msc**.  

    2. Vyberte službu **web Windows Update** . Přejděte do nabídky **Akce** a vyberte **zastavit**.

2. Přejmenujte adresář **SoftwareDistribution** .  

    1. Otevřete příkazový řádek jako správce.  

    2. Zadejte následující příkazy:

        ```cmd
        cd %windir%
        ren SoftwareDistribution SDTemp
        exit
        ```

3. Restartujte službu **web Windows Update** .

    1. Přepněte zpět do okna **služby** .  

    2. Vyberte službu **web Windows Update** . Přejděte do nabídky **Akce** a vyberte **Spustit**.

    3. Zavřete okno Služby.  

#### <a name="step-4-reset-the-microsoft-antivirus-update-engine-on-your-computer"></a>Krok 4: resetování stroje antivirové aktualizace společnosti Microsoft ve vašem počítači  

1. Otevřete příkazový řádek jako správce.

2. Zadejte následující příkazy:

    ```cmd
    cd \

    cd program files\windows defender

    MpCmdRun -RemoveDefinitions -all

    exit
    ```

3. Restartujte počítač.  

4. Zkuste znovu aktualizovat program Windows Defender.

Pokud se problém nevyřeší, pokračujte k dalšímu kroku.  

#### <a name="step-5-manually-install-the-definition-updates"></a>Krok 5: ruční instalace aktualizací definic  

[Ručně stáhněte nejnovější aktualizace](https://www.microsoft.com/en-us/wdsi/defenderupdates).  

#### <a name="step-6-contact-microsoft-support"></a>Krok 6: kontaktujte podporu Microsoftu.  

Pokud tyto kroky problém nevyřeší, obraťte se na podporu Microsoftu. Další informace najdete v tématu [Podpora možností a komunitních prostředků](../../core/understand/find-help.md#BKMK_SupportOptions).  

## <a name="starting-windows-defender-or-endpoint-protection-service"></a>Spuštění služby Windows Defender nebo Endpoint Protection

### <a name="symptom"></a>Příznak

Zobrazí se zpráva s upozorněním, že program **Windows Defender nebo Endpoint Protection nemonitoruje váš počítač, protože služba programu byla zastavena. Měli byste ho restartovat hned teď.**

### <a name="solution"></a>Řešení

#### <a name="step-1-restart-your-computer"></a>Krok 1: restartování počítače

Ukončete všechny aplikace a restartujte počítač.  

#### <a name="step-2-check-the-windows-service"></a>Krok 2: ověření služby systému Windows

1. Pokračujte na **Start**a otevřete **Services. msc**.  

2. Vyberte **službu antivirová ochrana v programu Windows Defender**.  

3. Ujistěte se, že **Typ spouštění** je nastaven na hodnotu **automaticky**.

4. Přejděte do nabídky **Akce** a vyberte **Spustit**.

    1. Pokud tato akce není k dispozici, vyberte **zastavit**. Počkejte, až se služba zastaví, a pak vyberte akci **Spustit** pro restartování služby.  

Poznamenejte si všechny chyby, které se mohou zobrazit během tohoto procesu. [Kontaktujte podpora Microsoftu](../../core/understand/find-help.md#BKMK_SupportOptions) a zadejte informace o chybě.  

#### <a name="step-3-remove-any-third-party-security-programs"></a>Krok 3: odebrání všech programů zabezpečení třetích stran  

> [!NOTE]  
> Některé aplikace zabezpečení nebudou zcela odinstalovány. Možná budete muset stáhnout a spustit čisticí nástroj pro předchozí aplikaci zabezpečení a úplně ho odebrat.  

1. **Spusťte** příkaz **appwiz. cpl**a otevřete ho.  

2. V seznamu nainstalovaných programů odinstalujte všechny programy zabezpečení třetích stran.

3. Restartujte počítač.  

> [!CAUTION]  
> Když odeberete programy zabezpečení, může být počítač nechráněný. Pokud máte potíže s instalací programu Windows Defender po odebrání stávajících programů zabezpečení, obraťte se na [Podpora Microsoftu](https://support.microsoft.com/supportforbusiness/productselection). Vyberte rodinu produktů **zabezpečení** a pak produkt **Windows Defender** .

## <a name="internet-connection-issues"></a>Problémy s připojením k internetu

Aby mohl váš počítač získat nejnovější aktualizace z web Windows Update, připojte ho k Internetu.  

1. **Spusťte** příkaz **ncpa. cpl**a spusťte ho.  

2. Otevřete název připojení a zobrazte **stav**připojení.  

3. Pokud je váš počítač připojený, stav připojení **IPv4** a/nebo **IPv6** je **Internet**.  

4. Pokud se zdá, že váš počítač není připojený k síti, vyberte název připojení a vyberte **diagnostiku tohoto připojení**.

Ukončete všechny spuštěné programy a restartujte počítač.  

## <a name="detected-threat-cant-be-remediated"></a> Zjištěná hrozba se nedá napravit

Když program Windows Defender nebo Endpoint Protection zjistí potenciální hrozbu, pokusí se hrozbu zmírnit tím, že se tato hrozba odstraní do karantény. Tyto hrozby se můžou skrýt v komprimovaném`.zip`archivu () nebo ve sdílené síťové složce.

### <a name="remove-or-scan-the-file"></a>Odebrání nebo kontrola souboru  

- Pokud byla zjištěná hrozba v komprimovaném souboru archivu, přejděte k souboru. Odstraňte soubor nebo ho ručně prověřte. Klikněte na soubor pravým tlačítkem a vyberte **Vyhledat v programu Windows Defender**. Pokud program Windows Defender zjistí v souboru další hrozby, upozorní vás. Pak můžete vybrat příslušnou akci.  

- Pokud se zjištěná hrozba nacházela ve sdílené síťové složce, otevřete sdílenou složku a ručně ji prověřte. Klikněte na soubor pravým tlačítkem a vyberte **Vyhledat v programu Windows Defender**. Pokud program Windows Defender zjistí ve sdílené síťové složce další hrozby, upozorní vás. Pak můžete vybrat příslušnou akci.  

- Pokud si nejste jistí původem souboru, spusťte v počítači úplnou kontrolu. Úplná kontrola může nějakou dobu trvat.  

## <a name="see-also"></a>Viz také

[Endpoint Protection nejčastějších dotazech klienta](endpoint-protection-client-faq.md)

[Nápověda klienta služby Endpoint Protection](endpoint-protection-client-help.md)
