---
title: Příprava rolí systému lokality pro OSD
titleSuffix: Configuration Manager
description: Před nasazením operačních systémů v Configuration Manager nakonfigurujte role systému lokality.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d9331ce452e40944e4a9b363773d254a32f2c58
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697479"
---
# <a name="prepare-site-system-roles-for-os-deployments-with-configuration-manager"></a>Příprava rolí systému lokality pro nasazení operačního systému pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Chcete-li nasadit operační systémy v Configuration Manager, nejprve připravte následující role systému lokality, které vyžadují konkrétní konfiguraci a požadavky.



##  <a name="distribution-points"></a><a name="BKMK_DistributionPoints"></a> Distribuční body  

Role systému lokality distribučního bodu hostuje zdrojové soubory pro klienty ke stažení. Tento obsah je pro aplikace, aktualizace softwaru, image operačních systémů, spouštěcí bitové kopie a balíčky ovladačů. Řízení distribuce obsahu pomocí možností šířky pásma, omezování a plánování.  

Je důležité, abyste měli dostatek distribučních bodů na podporu nasazení operačních systémů do počítačů. Je také důležité naplánovat umístění těchto distribučních bodů ve vaší hierarchii. Další informace najdete v tématu [Správa obsahu a infrastruktury obsahu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md). Tento článek obsahuje některé další aspekty plánování pro distribuční body, které jsou specifické pro nasazení operačního systému.  


###  <a name="additional-planning-considerations-for-distribution-points"></a><a name="BKMK_AdditionalPlanning"></a> Další aspekty plánování distribučních bodů  

Následující položky jsou další aspekty plánování, které je potřeba vzít v úvahu pro distribuční body:  

#### <a name="how-can-i-prevent-unwanted-os-deployments"></a>Jak zabráním nechtěným nasazením operačních systémů?  
Configuration Manager nerozlišuje servery lokality od jiných cílových počítačů v kolekci. Pokud nasadíte požadované pořadí úkolů do kolekce, která obsahuje server lokality, pořadí úkolů se spustí stejným způsobem jako jakýkoli jiný počítač v kolekci. Ujistěte se, že nasazení operačního systému používá kolekci, která obsahuje příslušné klienty.  

Spravujte chování při vysoce rizikových nasazeních pořadí úkolů. Vysoce rizikové nasazení je takové nasazení, které se na klientovi instaluje automaticky a u kterého hrozí riziko nechtěných výsledků. Například pořadí úkolů s účelem vyžadovaným pro nasazení operačního systému. Chcete-li snížit riziko nežádoucího nasazení s vysokým rizikem, nakonfigurujte nastavení ověřování nasazení. Další informace najdete v tématu [nastavení pro správu nasazení s vysokým rizikem](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

#### <a name="how-many-computers-can-receive-an-os-image-at-one-time-from-a-single-distribution-point"></a>Kolik počítačů může v jednom okamžiku přijmout image operačního systému z jednoho distribučního bodu?  
Pokud chcete odhadnout, kolik distribučních bodů budete potřebovat, vezměte v úvahu následující proměnné:  
- Rychlost zpracování distribučního bodu
- Rychlost disku distribučního bodu
- Dostupná šířka pásma sítě
- Velikost balíčku bitové kopie   
  
Pokud například nebudete brát v úvahu žádné jiné faktory prostředků serveru, maximální počet počítačů, které mohou zpracovat 4 GB balíčků imagí za hodinu v síti Ethernet s rychlostí 100 MB/s je 11 počítačů.  

`100 megabits/sec = 12.5 megabytes/sec = 750 megabytes/min = 45 gigabytes/hour = 11 images @ 4 GB per image`  

Pokud je nutné nasadit operační systém na určitý počet počítačů v rámci určitého časového rámce, distribuujte bitovou kopii do příslušného počtu distribučních bodů.  

#### <a name="can-i-deploy-an-os-to-a-distribution-point"></a>Můžu nasadit operační systém do distribučního bodu?  
Operační systém můžete nasadit do distribučního bodu, ale bitovou kopii operačního systému je třeba přijmout z jiného distribučního bodu.  


###  <a name="configuring-distribution-points-to-accept-pxe-requests"></a><a name="BKMK_PXEDistributionPoint"></a> Konfigurace distribučních bodů pro příjem požadavků PXE  

K nasazení operačních systémů pro Configuration Manager klientů, kteří vytvářejí požadavky na spouštění pomocí technologie PXE, nakonfigurujte jeden nebo více distribučních bodů pro příjem požadavků PXE. Jakmile nakonfigurujete distribuční bod, odpoví na požadavky na spuštění pomocí technologie PXE a určí příslušnou akci nasazení, která se má provést. Další informace naleznete v části [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).  


###  <a name="customize-the-ramdisk-tftp-block-and-window-sizes-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a> Přizpůsobení velikosti bloku a velikosti okna TFTP disku paměti RAM na distribučních bodech s povoleným PXE  

U distribučních bodů s povoleným PXE můžete přizpůsobit blok a velikost okna TFTP disku RAM. Pokud jste přizpůsobili síť, Velká velikost bloku nebo okna by mohla způsobit, že se stahování spouštěcí image nezdaří s chybou vypršení časového limitu. Vlastní nastavení bloku a velikosti okna TFTP disku paměti RAM vám umožní optimalizovat provoz TFTP při použití technologie PXE, aby splňovala konkrétní požadavky na síť. Pokud chcete zjistit, jakou konfiguraci máte nejúčinnější, otestujte vlastní nastavení ve svém prostředí.  

-   **Velikost bloku TFTP**: velikost bloku je velikost datových paketů odesílaných serverem do klienta, který stahuje soubor. Větší velikost bloku umožňuje serveru odesílat menší množství paketů, takže se zkrátí doba odezvy mezi serverem a klientem. Velikost velkého bloku ale vede k fragmentovaným paketům, což u většiny implementací klientů PXE nepodporuje.  

-   **Velikost okna TFTP**: Protokol TFTP vyžaduje pro každý odeslaný blok dat paket potvrzení (ACK). Server neodešle další blok v řadě, dokud neobdrží paket ACK k předchozímu bloku. Okno TFTP umožňuje definovat, kolik datových bloků trvá vyplnit okno. Server odesílá datové bloky jeden po druhém, dokud není okno zaplněné, a potom klient odešle paket ACK. Pokud zvětšíte velikost okna, sníží se tím počet zpoždění odezvy mezi klientem a serverem a zkrátí se celkový potřebný čas na stažení spouštěcí image.  
  

#### <a name="modify-the-ramdisk-tftp-window-size"></a>Úprava velikosti okna TFTP disku RAM  
Pokud chcete přizpůsobit velikost okna TFTP disku paměti RAM, přidejte na distribuční body s povoleným PXE následující klíč registru:  

- **Umístění**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Název**: RamDiskTFTPWindowSize  
- **Zadejte**: REG_DWORD  
- **Hodnota**: (přizpůsobená velikost okna)  
    - Výchozí hodnota je **1** (jeden datový blok vyplní okno).  

#### <a name="modify-the-ramdisk-tftp-block-size"></a>Úprava velikosti bloku TFTP disku RAM  
Pokud chcete přizpůsobit velikost okna TFTP disku paměti RAM, přidejte na distribuční body s povoleným PXE následující klíč registru:  

- **Umístění**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Název**: RamDiskTFTPBlockSize  
- **Zadejte**: REG_DWORD  
- **Hodnota**: (přizpůsobená velikost bloku)  
    - Výchozí hodnota je **4096**.  

> [!Note]  
> Tyto konfigurace protokolu TFTP podporují obě služby pro nasazení systému Windows i Configuration Manager služby respondéru PXE.  


###  <a name="configure-distribution-points-to-support-multicast"></a><a name="BKMK_DPMulticast"></a> Konfigurace distribučních bodů pro podporu vícesměrového vysílání  

Vícesměrové vysílání je metoda optimalizace sítě. Použijte ji v distribučních bodech, pokud je nejspíš více klientů stahovat stejnou bitovou kopii operačního systému ve stejnou dobu. Při použití vícesměrového vysílání může image operačního systému současně stahovat více počítačů jako vícesměrové vysílání distribučním bodem. Bez vícesměrového vysílání pošle distribučnímu bodu kopii dat pro každého klienta přes samostatné připojení. Další informace najdete v tématu [použití vícesměrového vysílání k nasazení Windows přes síť](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

Před nasazením operačního systému nakonfigurujte distribuční bod tak, aby podporoval vícesměrové vysílání. Další informace najdete v tématu [instalace a konfigurace distribučních bodů](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).



##  <a name="state-migration-point"></a><a name="BKMK_StateMigrationPoints"></a> Bod migrace stavu  

Bod migrace stavu ukládá data o stavu uživatele, která nástroj USMT zachytí na jednom počítači a pak obnoví v jiném počítači. Když však zaznamenáte uživatelské nastavení pro nasazení operačního systému na stejném počítači, jako je například nasazení, při kterém aktualizujete systém Windows v cílovém počítači, můžete zvolit, zda chcete ukládat data do stejného počítače pomocí pevných odkazů nebo použít bod migrace stavu. U některých nasazení počítačů se při vytváření úložiště stavů Configuration Manager automaticky vytvoří přidružení mezi úložištěm stavu a cílovým počítačem. Při plánování bodu migrace stavu Vezměte v úvahu následující faktory:    


### <a name="user-state-size"></a>Velikost stavu uživatele  

Velikost stavu uživatele má přímý vliv na využití místa na disku bodu migrace stavu a na výkon sítě v průběhu migrace. Zvažte velikost stavu uživatele a počet migrovaných počítačů. Zvažte také, která nastavení vyžadují migraci z počítače. Pokud je například složka **dokumenty** již zálohována na server, pak ji pravděpodobně nemusíte migrovat jako součást nasazení bitové kopie. Vyloučením zbytečných migrací se zmenší celková velikost stavu uživatele a sníží se tím vliv na výkon sítě a úložný prostor na disku v bodě migrace stavu.  


### <a name="user-state-migration-tool"></a>Nástroj pro migraci stavu uživatele  

Pokud chcete zachytit a obnovit stav uživatele během nasazování operačních systémů, použijte balíček Nástroj pro migraci uživatelských souborů a nastavení (USMT), který odkazuje na zdrojové soubory nástroje USMT. Configuration Manager automaticky vytvoří tento balíček v konzole Configuration Manager v **Software Library**  >  **balíčku pro správu aplikací**knihovny softwaru  >  **Packages**. Configuration Manager pomocí nástroje USMT 10 zachytí stav uživatele z jednoho operačního systému a pak ho obnoví do jiného. Sada Windows Assessment and Deployment Kit (Windows ADK) pro Windows 10 obsahuje nástroj USMT 10.

Popis různých scénářů migrace pro nástroj USMT 10 najdete v tématu [běžné scénáře migrace](/windows/deployment/usmt/usmt-common-migration-scenarios) v dokumentaci k systému Windows.  


### <a name="retention-policy"></a>Zásady uchovávání informací  

Když konfigurujete bod migrace stavu, zadejte dobu, po kterou se budou uchovávat data o stavu uživatele, který ukládá. Dobu uchovávání dat v bodu migrace stavu ovlivňují dvě okolnosti:  

-   Vliv uložených dat na místo na disku.  

-   Potenciální požadavek na uchování dat po určitou dobu pro případ, kdy by byla nutná jejich opětovná migrace.  
  
  
Migrace stavu probíhá ve dvou fázích: zachytávání dat a obnovení dat. Při zaznamenávání se data stavu uživatele shromáždí a uloží do bodu migrace stavu. Při obnovování dat jsou data o stavu uživatele načtena z bodu migrace stavu a zapsána do cílového počítače. Krok pořadí úkolů **Úložiště stavu uvolnění** následně uvolní uložená data. Uvolnění dat spustí časovač uchovávání. Pokud zvolíte možnost okamžitého odstranění migrovaných dat, data o stavu uživatele se odstraní hned po vydání. Pokud zvolíte možnost uchovávání dat po určitou dobu, data o stavu budou odstraněna, jakmile uplyne příslušná doba od jejich uvolnění. Čím delší dobu uchovávání dat nastavíte, tím více místa na disku budete pravděpodobně potřebovat.  


### <a name="select-drive-to-store-user-state-migration-data"></a>Výběr jednotky pro uložení dat migrace stavu uživatele  

Když konfigurujete bod migrace stavu, určete jednotku na serveru, kam se budou ukládat data migrace stavu uživatele. Při výběru máte k dispozici pevný seznam jednotek. Některé z těchto jednotek však nemusí umožňovat zápis, jako například jednotka CD nebo jednotka, která není sdílena v síti. Některá písmena jednotek nemusí být namapována na žádné jednotky v počítači. Při konfiguraci bodu migrace stavu zadejte zapisovatelnou sdílenou jednotku.  


### <a name="configure-a-state-migration-point"></a>Konfigurace bodu migrace stavu  

Ke konfiguraci bodu migrace stavu k uložení dat o stavu uživatele použijte následující metody:  

-   Použít **Průvodce Vytvořit server lokality** , pomocí nějž vytvoříte nový server lokality pro bod migrace stavu.  

-   Použít **Průvodce Přidat role serveru** , pomocí nějž přidáte na existující server bod migrace stavu.  

Při použití těchto průvodců budete vyzváni k zadání následujících informací pro bod migrace stavu:  

-   Složky, do nichž budou uložena data o stavu uživatele.  

-   Maximální počet klientů, kteří mohou ukládat data v bodě migrace stavu.  

-   Minimální volné místo k ukládání dat o stavu uživatele v bodě migrace stavu.  

-   Zásady smazání role. Buď určete, že data o stavu uživatele se odstraní hned po obnovení na počítači nebo po určitém počtu dní od obnovení uživatelských dat v počítači.  

-   Jestli má bod migrace stavu reagovat jenom na požadavky na obnovení dat stavu uživatele. Když tuto možnost povolíte, nebudete moct použít bod migrace stavu k ukládání dat o stavu uživatele.  

Postup instalace role systému lokality najdete v tématu [Přidání rolí systému lokality](../../core/servers/deploy/configure/add-site-system-roles.md).