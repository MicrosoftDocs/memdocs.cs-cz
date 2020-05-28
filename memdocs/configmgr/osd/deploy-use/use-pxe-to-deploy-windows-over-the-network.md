---
title: Použití technologie PXE pro OSD přes síť
titleSuffix: Configuration Manager
description: Pomocí nasazení operačního systému inicializovaného technologií PXE aktualizujte operační systém počítače nebo nainstalujte novou verzi Windows do nového počítače.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11045ff31dc3832ac97d62f491561b3cf989813c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079344"
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-configuration-manager"></a>Použití technologie PXE pro nasazení Windows přes síť s Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Nasazení operačních systémů spouštěné pomocí technologie PXE (Preboot eXecution Environment) ve službě Configuration Manager umožňují klientům vyžádat a nasazovat operační systémy přes síť. V tomto scénáři nasazení odešlete bitovou kopii operačního systému a spouštěcí bitové kopie do distribučního bodu s povoleným PXE.

> [!NOTE]  
> Když vytvoříte nasazení operačního systému, které cílí jenom na počítače s x64 BIOS, musí být na distribučním bodu dostupná spouštěcí bitová kopie x64 i Bitová spouštěcí kopie x86.

Nasazení operačního systému inicializované technologií PXE můžete použít v následujících scénářích:

- [Aktualizace existujícího počítače na novou verzi Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Instalace nové verze Windows do nového počítače (holý počítač)](install-new-windows-version-new-computer-bare-metal.md)  

Proveďte kroky v jednom ze scénářů nasazení operačního systému a potom použijte části v tomto článku k přípravě na nasazení inicializovaná technologií PXE.

> [!WARNING]
> Pokud používáte nasazení PXE a nakonfigurujete hardware zařízení se síťovým adaptérem jako prvním spouštěcím zařízením, můžou tato zařízení automaticky spustit pořadí úloh nasazení operačního systému bez zásahu uživatele. Ověřování nasazení nespravuje tuto konfiguraci. I když tato konfigurace může zjednodušit proces a omezit interakci s uživatelem, umístí zařízení s větším rizikem na nechtěné obnovení obrazu.

## <a name="configure-at-least-one-distribution-point-to-accept-pxe-requests"></a><a name="BKMK_Configure"></a> Konfigurace nejmíň jednoho distribučního bodu pro příjem požadavků PXE

K nasazení operačních systémů pro Configuration Manager klientů, kteří vytvářejí požadavky na spouštění PXE, je nutné nakonfigurovat jeden nebo více distribučních bodů, aby přijímaly požadavky PXE. Jakmile nakonfigurujete distribuční bod, odpoví na požadavky na spuštění pomocí technologie PXE a určí příslušnou akci nasazení, která se má provést. Další informace naleznete v části [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).  

> [!NOTE]  
> Při konfiguraci jednoho distribučního bodu s povoleným PXE pro podporu více podsítí není podporováno použití možností DHCP. Nakonfigurujte pomocníky IP adres na směrovačích, aby byly požadavky PXE předávány do distribučních bodů s povoleným PXE.
>
> Ve verzi 1810 není podporované používat respondér technologie PXE bez služby WDS na serverech, na kterých běží taky server DHCP.
>
> Pokud v rámci verze 1902 povolíte respondér PXE v distribučním bodě bez služby pro nasazení systému Windows, může být nyní na stejném serveru jako služba DHCP.<!--3734270, SCCMDocs-pr #3416--> Přidejte následující nastavení pro podporu této konfigurace:  
>
> - Nastavte hodnotu DWord **DoNotListenOnDhcpPort** na `1` následující klíč registru: `HKLM\Software\Microsoft\SMS\DP` .
> - Nastavte možnost DHCP 60 na `PXEClient` .  
> - Restartujte služby SCCMPXE a DHCP na serveru.  

## <a name="prepare-a-pxe-enabled-boot-image"></a>Příprava spouštěcí image s povolenou technologií PXE

Chcete-li použít technologii PXE k nasazení operačního systému, je nutné, aby byly spouštěcí bitové kopie s povoleným PXE x86 i x64 distribuovány do jednoho nebo více distribučních bodů s povoleným PXE. Pomocí těchto informací povolte technologii PXE ve spouštěcí imagi a tuto spouštěcí image distribuujte do distribučních bodů:

- Pokud chcete povolit technologii PXE ve spouštěcí imagi, vyberte možnost **nasadit tuto bitovou spouštěcí kopii z distribučního bodu s povoleným PXE** na kartě **zdroj dat** ve vlastnostech spouštěcí bitové kopie.

- Pokud změníte vlastnosti spouštěcí bitové kopie, aktualizujte a znovu Distribuujte spouštěcí bitovou kopii do distribučních bodů. Další informace najdete v části [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

## <a name="manage-duplicate-hardware-identifiers"></a>Správa duplicitních identifikátorů hardwaru

Configuration Manager může rozpoznat více počítačů jako stejné zařízení, pokud mají duplicitní atributy SMBIOS, nebo použijete sdílený síťový adaptér. Tyto problémy zmírnit tím, že v nastavení hierarchie nařídíte duplicitní identifikátory hardwaru. Další informace najdete v tématu [Správa duplicitních identifikátorů hardwaru](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers).

## <a name="create-an-exclusion-list-for-pxe-deployments"></a><a name="BKMK_PXEExclusionList"></a> Vytvoření seznamu vyloučení pro nasazení PXE

> [!Note]  
> V některých případech může být snazší proces [správy duplicitních identifikátorů hardwaru](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers) .<!-- SCCMDocs issue 802 -->
>
> Chování každého z nich může v některých scénářích způsobit různé výsledky. Seznam vyloučení nikdy nespustí klienta s uvedenou adresou MAC bez ohledu na to, co.
>
> Seznam duplicitních ID nepoužívá adresu MAC k vyhledání zásad pořadí úkolů pro klienta. Pokud se shoduje s ID SMBIOS nebo pokud existují zásady pořadí úkolů pro neznámé počítače, klient se pořád spustí.

Pokud nasazujete operační systémy pomocí technologie PXE, můžete v každém distribučním bodě vytvořit seznam vyloučení. Přidejte adresy MAC do seznamu vyloučení počítačů, které má distribuční bod ignorovat. Uvedené počítače neobdrží pořadí úkolů nasazení, které Configuration Manager používá pro nasazení PXE.

### <a name="process-to-create-the-exclusion-list"></a>Postup vytvoření seznamu vyloučení

1. V distribučním bodě s povoleným PXE vytvořte textový soubor. Název tohoto textového souboru může být například **pxeExceptions.txt**.  

2. Použijte Editor prostého textu, například Poznámkový blok, a přidejte adresy MAC počítačů, které má distribuční bod s povoleným PXE ignorovat. Hodnoty adres MAC oddělujte dvojtečkami a každou adresu zadejte na samostatný řádek. Příklad: `01:23:45:67:89:ab`  

3. Uložte tento textový soubor do systémového serveru lokality distribučního bodu s povoleným PXE. Textový soubor může být uložený v jakémkoli umístění na serveru.  

4. Pokud chcete vytvořit klíč registru **MACIgnoreListFile** , upravte registr distribučního bodu s povoleným PXE. Přidejte hodnotu řetězce pro celou cestu k textovému souboru na serveru systému lokality distribučního bodu s povoleným PXE. Použijte následující cestu registru:  

    `HKLM\Software\Microsoft\SMS\DP`  

    > [!WARNING]  
    > Používáte-li Editor registru nesprávně, může dojít k vážným problémům, které mohou vyžadovat přeinstalaci systému Windows. Společnost Microsoft nemůže zaručit, že můžete vyřešit problémy, které jsou výsledkem nesprávného použití Editoru registru. Editor registru používáte na vlastní nebezpečí.  

5. Po provedení této změny registru restartujte službu WDS nebo službu PXE Responder Service. Nemusíte restartovat server.<!--512129-->  

## <a name="ramdisk-tftp-block-size-and-window-size"></a><a name="BKMK_RamDiskTFTP"></a>Velikost bloku a velikost okna TFTP disku RAM

U distribučních bodů s povoleným PXE můžete přizpůsobit blok a velikost okna TFTP disku RAM. Pokud jste přizpůsobili síť, Velká velikost bloku nebo okna by mohla způsobit, že se stahování spouštěcí image nezdaří s chybou vypršení časového limitu. Vlastní nastavení bloku a velikosti okna TFTP disku paměti RAM vám umožní optimalizovat provoz TFTP při použití technologie PXE, aby splňovala konkrétní požadavky na síť. Pokud chcete zjistit, jakou konfiguraci máte nejúčinnější, otestujte vlastní nastavení ve svém prostředí. Další informace najdete v tématu [přizpůsobení velikosti bloku a velikosti okna TFTP disku paměti RAM na distribučních bodech s povoleným PXE](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="configure-deployment-settings"></a>Konfigurace nastavení nasazení

Pokud chcete použít nasazení operačního systému inicializované technologií PXE, nakonfigurujte nasazení tak, aby byl operační systém dostupný pro požadavky na spouštění pomocí technologie PXE. Na kartě **nastavení nasazení** ve vlastnostech nasazení nakonfigurujte dostupné operační systémy. Pro nastavení **zpřístupnit pro následující** vyberte jednu z následujících možností:

- Configuration Manager klienty, média a technologie PXE

- Pouze média a technologie PXE

- Pouze média a technologie PXE (skryté)

## <a name="option-82-during-pxe-dhcp-handshake"></a>Možnost 82 během ověřování PXE DHCP
Počínaje verzí 1906 se při signalizaci PXE DHCP bez služby WDS podporuje možnost 82 za metodou handshake PXE DHCP. Pokud je vyžadována možnost 82, nezapomeňte použít respondér technologie PXE bez služby WDS. Možnost 82 není u služby WDS podporována.

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> Nasazení pořadí úkolů

Nasaďte operační systém do cílové kolekce. Další informace naleznete v části [Deploy a task sequence](deploy-a-task-sequence.md). Při nasazování operačních systémů pomocí technologie PXE můžete nakonfigurovat, jestli má být nasazení požadované, nebo dostupné.

- **Požadované nasazení**: požadovaná nasazení využívají technologii PXE bez zásahu uživatele. Uživatel nemůže obejít spouštění pomocí technologie PXE. Pokud však uživatel spouštění PXE zruší, než distribuční bod odpoví, operační systém nebude nasazen.

- **Dostupné nasazení**: dostupná nasazení vyžadují, aby byl uživatel přítomen v cílovém počítači. Aby bylo možné pokračovat v procesu spouštění PXE, musí uživatel stisknout klávesu **F12** . Pokud není k dispozici uživatel pro stisknutí klávesy **F12**, počítač se spustí do aktuálního operačního systému nebo z dalšího dostupného spouštěcího zařízení.

Požadované nasazení PXE můžete znovu nasadit tak, že zrušíte stav posledního nasazení PXE přiřazeného ke kolekci Configuration Manager nebo počítači. Další informace o akci **Vymazat požadovaná nasazení PXE** najdete v tématu [Správa klientů](../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode) nebo [Správa kolekcí](../../core/clients/manage/collections/manage-collections.md#bkmk_device). Tato akce resetuje stav tohoto nasazení a znovu nainstaluje nejnovější požadovaná nasazení.

> [!IMPORTANT]  
> Protokol PXE není zabezpečený. Ujistěte se, že se server PXE a klient PXE nacházejí v fyzicky zabezpečené síti, například v datovém centru, aby se zabránilo neoprávněnému přístupu k webu.

## <a name="how-the-boot-image-is-selected-for-pxe"></a>Způsob výběru spouštěcí bitové kopie pro technologii PXE

Když se klient spustí s technologií PXE, Configuration Manager poskytne klientovi spouštěcí image, která se má použít. Configuration Manager používá spouštěcí bitovou kopii s přesnou shodou architektury. Pokud není k dispozici spouštěcí image s přesnou architekturou, Configuration Manager používá spouštěcí bitovou kopii s kompatibilní architekturou.

Následující seznam uvádí podrobnosti o tom, jak je vybraná spouštěcí image pro klienty spouštěné pomocí technologie PXE:  

1. Configuration Manager vyhledá v databázi lokality záznam systému, který odpovídá adrese MAC nebo SMBIOS klienta, který se pokouší spustit.  

    > [!NOTE]  
    > Pokud se počítač, který je přiřazený k lokalitě, spustí v prostředí PXE pro jinou lokalitu, zásady nejsou pro tento počítač viditelné. Například pokud je klient již přiřazen k lokalitě A, bod správy a distribuční bod pro lokalitu B nebudou mít přístup k zásadám z lokality A. Klient nástroje se nepodařilo spustit pomocí technologie PXE.  

2. Configuration Manager vyhledá pořadí úloh nasazená na záznam systému, který najdete v kroku 1.  

3. V seznamu pořadí úloh nalezených v kroku 2 Configuration Manager vyhledá spouštěcí bitovou kopii, která odpovídá architektuře klienta, který se pokouší spustit. Pokud se najde spouštěcí image se stejnou architekturou, použije se tato spouštěcí image.  

    Pokud nalezne více než jednu spouštěcí image, použije *nejvyšší* nebo poslední ID nasazení pořadí úkolů. V případě hierarchie více lokalit by měl lokalita s *vyšším* písmenem přednost před porovnáváním řetězců. Pokud se například oba shodují, je v rámci nasazení z webu AAA vybráno staré nasazení z lokality ZZZ.<!-- SCCMDocs issue 877 -->  

4. Pokud se spouštěcí image nenajde se stejnou architekturou, Configuration Manager vyhledá spouštěcí image, která je kompatibilní s architekturou klienta. Vyhledá v seznamu pořadí úloh, které najdete v kroku 2. Třeba 64 klient systému BIOS/MBR je kompatibilní s 32 bitovou spouštěcí imagí a 64 bitových kopií. 32 klient BIOS/MBR je kompatibilní s pouze 32 bitových spouštěcích kopií. Klienti UEFI jsou kompatibilní jenom s architekturou pro porovnání. 64 klient UEFI je kompatibilní jenom s 64 bitovou spouštěcí kopií a klient UEFI s 32 je kompatibilní 32 jenom s 16bitovými bitovými spouštěcími kopiemi.
