---
title: Konfigurace funkce Asset Intelligence
titleSuffix: Configuration Manager
description: Nastavte funkce Asset Intelligence v Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1a5c89d3fdd82bfa654f806c6931bde2621e714b
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906610"
---
# <a name="configure-asset-intelligence-in-configuration-manager"></a>Konfigurace funkce Asset Intelligence v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Funkce Asset Intelligence inventáře a spravují využívání softwarových licencí.   

## <a name="steps-to-configure-asset-intelligence"></a>Kroky při konfiguraci funkce Asset Intelligence  
   

- **Krok 1**: Pokud chcete shromáždit data inventáře funkce Asset Intelligence sestav, musíte povolit klientského agenta inventáře hardwaru, jak je popsáno v tématu [postup rozšiřování inventáře hardwaru](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).
- **Krok 2**: [Povolení funkce Asset Intelligence třídy generování sestav inventáře hardwaru](#BKMK_EnableAssetIntelligence)  
- **Krok 3**: [instalace bodu synchronizace funkce Asset Intelligence](#BKMK_InstallAssetIntelligenceSynchronizationPoint)
- **Krok 4**: [Povolení auditování událostí úspěšného přihlášení](#BKMK_EnableSuccessLogonEvents)  
- **Krok 5**: [Import informací o softwarových licencích](#BKMK_ImportSoftwareLicenseInformation)  
- **Krok 6**: [konfigurace úloh údržby funkce Asset Intelligence](#BKMK_ConfigureMaintenanceTasks) 


###  <a name="enable-asset-intelligence-hardware-inventory-reporting-classes"></a><a name="BKMK_EnableAssetIntelligence"></a> Enable Asset Intelligence hardware inventory reporting classes  
 Pokud chcete povolit funkce Asset Intelligence v Configuration Managerch lokalitách, musíte povolit jednu nebo více funkce Asset Intelligence tříd generování sestav inventáře hardwaru. Tyto třídy můžete povolit na domovské stránce **Asset Intelligence** nebo ve vlastnostech nastavení klienta v uzlu **Nastavení klienta** v pracovním prostoru **Správa** . Použijte jeden z následujících postupů.  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-the-asset-intelligence-home-page"></a>Povolení třídy generování sestav inventáře hardwaru Asset Intelligence z domovské stránky funkce Asset Intelligence  

1.  V konzole Configuration Manager vyberte **Asset a funkce Asset Intelligence dodržování předpisů**  >  **Asset Intelligence**.  

3.  Na kartě **Domů** ve skupině **funkce Asset Intelligence** vyberte možnost **Upravit třídy inventáře**.   

4.  Chcete-li povolit vytváření sestav funkce Asset Intelligence, vyberte možnost **Povolit všechny funkce Asset Intelligence třídy vytváření zpráv** nebo **Povolit pouze vybrané třídy vytváření zpráv funkce Asset Intelligence**a vyberte alespoň jednu třídu generování sestav ze zobrazených tříd.  

    > [!NOTE]  
    >  Sestavy funkce Asset Intelligence, které závisejí na třídách inventáře hardwaru, které pomocí tohoto postupu povolíte, zobrazují data, až když klienti vyhledají a vrátí inventář hardwaru.  


##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-client-settings-properties"></a>Povolení třídy generování sestav inventáře hardwaru Asset Intelligence z vlastností nastavení klienta  

1.  V konzole Configuration Manager vyberte možnost **Správa**  >   **nastavení klienta**  >  **výchozí nastavení agenta klienta**. Pokud jste vytvořili vlastní nastavení klienta, můžete je místo toho vybrat.  

3.  Na kartě **domů** > **vlastnosti** skupiny a vyberte **vlastnosti**.   

4.  Vyberte **Hardware Inventory**  >  **třídy sady nastavení**inventáře hardwaru. .  

5.  Vyberte možnost **filtrovat podle kategorie**  >  **funkce Asset Intelligence třídy vytváření sestav**. Seznam tříd se obnoví a zobrazí se jenom třídy generování sestav inventáře hardwaru funkce Asset Intelligence.  

6.  Vyberte ze seznamu alespoň jednu třídu pro vytváření sestav.  

    > [!NOTE]  
    >  Sestavy funkce Asset Intelligence, které závisejí na třídách inventáře hardwaru, které pomocí tohoto postupu povolíte, zobrazují data, až když klienti vyhledají a vrátí inventář hardwaru.  
  

###  <a name="install-an-asset-intelligence-synchronization-point"></a><a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> Install an Asset Intelligence Synchronization Point  

Role systému lokality bodu synchronizace funkce Asset Intelligence slouží k připojení Configuration Managerch lokalit ke službě System Center Online za účelem synchronizace informací funkce Asset Intelligence katalogu. Bod synchronizace funkce Asset Intelligence lze nainstalovat pouze v systému lokality umístěném v lokalitě nejvyšší úrovně v hierarchii Configuration Manager a vyžaduje přístup k Internetu pro synchronizaci se službou System Center Online pomocí portu TCP 443.

Bod synchronizace katalogu Asset Intelligence může kromě stažení nových informací katalogu Asset Intelligence taky odeslat do služby System Center Online vlastní informace o softwarových titulech  ke kategorizaci. Microsoft zpracovává všechny nahrané softwarové tituly jako veřejné informace. Zajistěte, aby vlastní softwarové tituly neobsahovaly důvěrné nebo proprietární informace. Další informace o vyžádání kategorizace softwarových titulů najdete v tématu [Request a catalog update for uncategorized software titles](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate).  

##### <a name="to-install-an-asset-intelligence-synchronization-point-site-system-role"></a>Instalace role systému lokality bodu synchronizace katalogu Asset Intelligence  

1.  V konzole Configuration Manager klikněte na možnost **Správa** >  **Konfigurace lokality**  >  **servery a role systému lokality**.  

3.  Přidejte roli systému lokality bodu synchronizace funkce Asset Intelligence k novému nebo existujícímu serveru systému lokality:  

    -  Pro **Nový server systému lokality**: na kartě **Domů** ve skupině **vytvořit** vyberte možnost **vytvořit server systému lokalit** a spusťte průvodce.   

        > [!NOTE]  
        >  Ve výchozím nastavení, když Configuration Manager nainstaluje roli systému lokality, instalační soubory se nainstalují na první dostupnou diskovou jednotku s formátem NTFS, která má nejvíce dostupného volného místa na pevném disku. Chcete-li zabránit Configuration Manager instalaci na konkrétní jednotky, vytvořte prázdný soubor s názvem No_sms_on_drive. SMS a zkopírujte jej do kořenové složky jednotky před tím, než nainstalujete server systému lokality.  

    -  Pro **existující server systému lokality**: vyberte server, na který chcete nainstalovat roli systému lokality bodu synchronizace funkce Asset Intelligence. Po výběru serveru se v podokně podrobností zobrazí seznam rolí systému lokality, které jsou již nainstalovány na serveru.  

         Kliknutím na možnost **Přidat roli systému lokality** na kartě **Domů** ve skupině **Server** spusťte průvodce.  

4.  Dokončete stránku **Obecné** . Pokud bod synchronizace katalogu Asset Intelligence přidáte do existujícího serveru systému lokality, ověřte hodnoty, které už byly nakonfigurované.  

5.  Na stránce **Výběr role systému** vyberte v seznamu dostupných rolí **bod synchronizace funkce Asset Intelligence** .  

6.  Na stránce **nastavení připojení bodu synchronizace funkce Asset Intelligence** klikněte na tlačítko **Další**.  

     Ve výchozím nastavení je položka **Použijte tento bod synchronizace informací o prostředcích** vybraná a nedá se na této stránce konfigurovat. System Center Online přijímá síťový provoz jenom přes port TCP 443, proto na této stránce průvodce nejde nakonfigurovat nastavení **Číslo portu SSL** .  

7.  Volitelně můžete zadat cestu k souboru ověřovacího certifikátu (. pfx) služby System Center Online. Cesta pro certifikát se ale obvykle nezadává, protože certifikát připojení se při instalaci role lokality zřizuje automaticky.  

8.  Na stránce **nastavení proxy serveru** určete, jestli funkce Asset Intelligence bod synchronizace bude při připojování ke službě System Center Online používat proxy server k synchronizaci katalogu a jestli se má použít přihlašovací údaje pro připojení k proxy server.  

    > [!WARNING]  
    >  Pokud se pro připojení ke službě System Center Online vyžaduje proxy server a vyprší platnost hesla účtu nakonfigurovaného pro ověřování proxy serveru, může se taky odstranit certifikát připojení.  

9. Na stránce **Plán synchronizace** zadejte, jestli se má katalog Asset Intelligence synchronizovat podle časového plánu. Pokud povolíte plán synchronizace, určíte taky, jestli se použije jednoduchý nebo vlastní plán. Při plánované synchronizaci se bod synchronizace katalogu Asset Intelligence připojí ke službě System Center Online a načte nejnovější katalog Asset Intelligence. Katalog funkce Asset Intelligence můžete ručně synchronizovat z uzlu funkce Asset Intelligence v konzole Configuration Manager. Postup ruční synchronizace katalogu funkce Asset Intelligence najdete v části [Ruční synchronizace funkce Asset Intelligence katalogu](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog) v tématu [operace pro funkce Asset Intelligence](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).  

10. Dokončete průvodce. 

###  <a name="enable-auditing-of-success-logon-events"></a><a name="BKMK_EnableSuccessLogonEvents"></a> Enable auditing of success logon events  
 Čtyři sestavy Asset Intelligence zobrazují informace získané z protokolů událostí Zabezpečení systému Windows v klientských počítačích. Tady je postup konfigurace přihlašovacích nastavení zásad zabezpečení počítače pro povolení auditování událostí úspěšného přihlášení.  

##### <a name="to-enable-success-logon-event-logging-by-using-a-local-security-policy"></a>Povolení protokolování událostí úspěšného přihlášení pomocí místních zásad zabezpečení  

1.  V Configuration Manager klientském počítači vyberte možnost **Spustit**  >  **Nástroje pro správu**  >  **místní zásady zabezpečení**.  

2.  V dialogovém okně **místní zásady zabezpečení** v části **nastavení zabezpečení**rozbalte **místní zásady**a pak zvolte **zásady auditu**.  

3.  V podokně výsledků dvakrát klikněte na **Auditovat události přihlášení**, ověřte, že je zaškrtnuté políčko **úspěch** , a pak zvolte **OK**.  

##### <a name="to-enable-success-logon-event-logging-by-using-an-active-directory-domain-security-policy"></a>Povolení protokolování událostí úspěšného přihlášení pomocí zásad zabezpečení domény Active Directory  

1.  V počítači s řadičem domény zvolte **Start**, přejděte na **Nástroje pro správu**a pak zvolte **zásady zabezpečení domény**.  

2.  V dialogovém okně **místní zásady zabezpečení** v části **nastavení zabezpečení**rozbalte **místní zásady**a pak zvolte **zásady auditu**.  

3.  V podokně výsledků dvakrát klikněte na **Auditovat události přihlášení**, ověřte, že je zaškrtnuté políčko **úspěch** , a pak zvolte **OK**.  

###  <a name="import-software-license-information"></a><a name="BKMK_ImportSoftwareLicenseInformation"></a> Import software license information  
 Následující části popisují postupy, které je nutné pro import informací o licencování společnosti Microsoft a obecné informace o softwaru do databáze Configuration Manager, pomocí Průvodce importem softwarové licence. Při importu informací o softwarových licencích ze souborů výpisů licencí do databáze lokality účet počítače serveru lokality vyžaduje pro systém souborů NTFS oprávnění **Úplné řízení** ke sdílené složce, která se používá pro import informací o softwarových licencích.  

> [!IMPORTANT]  
>  Když se informace o softwarových licencích naimportují do databáze lokality, stávající informace o softwarových licencí se přepíšou. Ověřte, že soubor informací o softwarových licencích, který používáte v Průvodci importem licencí softwaru, obsahuje kompletní výpis všech nezbytných informací.  

##### <a name="to-import-software-license-information-into-the-asset-intelligence-catalog"></a>Import informací o softwarových licencích do katalogu Asset Intelligence  

1.  V pracovním prostoru prostředky **a kompatibilita** vyberte možnost **funkce Asset Intelligence**.  

2.  Na kartě **Domů** ve skupině **funkce Asset Intelligence** vyberte **importovat licence softwaru**.   

4.  Na stránce **Import** zadejte, jestli importujete soubor programu Microsoft Volume Licensing (MVLS) (.xml nebo .csv) nebo soubor obecné licenční smlouvy (.csv). Další informace o vytvoření souboru obecné licenční smlouvy najdete dál v tomto tématu v části [Create a general license statement information file for import](#BKMK_CreateGeneralLicenseStatement) .  

    > [!WARNING]  
    >  Pokud chcete stáhnout soubor MVLS ve formátu .csv, který můžete naimportovat do katalogu Asset Intelligence, přejděte na web [Microsoft Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx). Pro přístup k těmto informacím musíte mít na tomto webu zaregistrovaný účet. Pokud potřebujete informace, jak získat soubor MVLS ve formátu .xml, musíte kontaktovat zástupce zákazníka Microsoftu.  

5.  Zadejte cestu UNC k souboru výpisu licencí nebo klikněte na **Procházet** a vyberte síťovou sdílenou složku a soubor.  

    > [!NOTE]  
    >  Tato sdílená složka by měla být správně zabezpečená, aby se předešlo neoprávněnému přístupu k souboru s licenčními informacemi, a počítačový účet, ve kterém se spouští průvodce, musí mít ke sdílené složce, která obsahuje soubor importu licencí, oprávnění Úplný přístup.  

6. Dokončete průvodce.  

###  <a name="create-a-general-license-statement-information-file-for-import"></a><a name="BKMK_CreateGeneralLicenseStatement"></a> Create a general license statement information file for import  
 Obecná licenční smlouva se dá do katalogu Asset Intelligence naimportovat taky pomocí ručně vytvořeného souboru importu licencí ve formátu textového souboru s oddělovači (.csv).  

> [!NOTE]  
>  Přestože se údaje vyžadují jenom v polích **Název**, **Vydavatel**, **Verze**a **EffectiveQuantity** , musí být v souboru importu licencí zadaná všechna pole na prvním řádku. Všechna datová pole by se měla zobrazovat ve formátu měsíc/den/rok, třeba 08/04/2008.  

Asset Intelligence páruje produkty, které zadáte v obecné licenční smlouvě, na základě názvu a verze produktu, ale ne názvu vydavatele. V obecné licenční smlouvě musíte použít název produktu, který se přesně shoduje s názvem produktu uloženým v databázi lokality. Funkce Asset Intelligence převezme číslo **EffectiveQuantity** uvedené v obecné licenční smlouvě a porovná počet nainstalovaných produktů nalezených v Configuration Manager inventáři.  

> [!TIP]  
>  Chcete-li získat úplný seznam názvů produktů uložených v databázi lokality Configuration Manager, můžete spustit následující dotaz v databázi lokality: vyberte Productname0 from z v_GS_INSTALLED_SOFTWARE.  

 U produktu můžete uvést přesné verze nebo můžete zadat část verze, třeba jenom hlavní verzi. V následujících příkladech jsou uvedené výsledné shody verzí pro položku verze obecné licenční smlouvy pro konkrétní produkt.  

|Položka obecné licenční smlouvy|Odpovídající položky databáze lokality|  
|-------------------------------------|------------------------------------|  
|Název: "MySoftware", ProductVersion0: "2"|Productname0 from: "Mysoftware"; ProductVersion0: "2.01.1234"<br /><br /> Productname0 from: "MySoftware"; ProductVersion0: "2.02.5678"<br /><br /> Productname0 from: "MySoftware"; ProductVersion0: "2.05.1234"<br /><br /> Productname0 from: "MySoftware"; ProductVersion0: "2.05.5678"<br /><br /> Productname0 from: "MySoftware"; ProductVersion0: "2.05.3579.000"<br /><br /> Productname0 from: "MySoftware"; ProductVersion0: "2.10.1234"|  
|Název: "MySoftware", verze "2,05"|Productname0 from: "MySoftware"; ProductVersion0: "2.05.1234"<br /><br /> Productname0 from: "MySoftware"; ProductVersion0: "2.05.5678"<br /><br /> Productname0 from: "MySoftware"; ProductVersion0: "2.05.3579.000"|  
|Název: "Mysoftware", verze "2"<br /><br /> Název: "Mysoftware", verze "2,05"|Při importu nastala chyba. Když jedné verzi produktu odpovídá víc položek, import se nepovede.|  
  

##### <a name="to-create-a-general-license-statement-import-file-by-using-microsoft-excel"></a>Vytvoření souboru importu obecné licenční smlouvy pomocí Microsoft Excelu  

1.  Otevřete Microsoft Excel a vytvořte novou tabulku.  

2.  Do prvního řádku nové tabulky zadejte všechny názvy datových polí softwarových licencí.  

3.  Do druhého a dalších řádků nové tabulky zadejte příslušné informace o softwarových licencích. Zkontrolujte, že pro každou softwarovou licenci, která se má naimportovat, jsou v dalších řádcích vyplněná všechna povinná datová pole. Název softwarového titulu zadaný do tabulky se musí shodovat se softwarovým titulem, který se pro klientský počítač zobrazuje po spuštění inventarizace hardwaru  v Průzkumníku prostředků.  

4.  Soubor uložte ve formátu. csv.  

5.  Tento soubor .csv zkopírujte do sdílené složky, která se používá pro import informací o softwarových licencích do katalogu Asset Intelligence.  

6.  V konzole Configuration Manager použijte Průvodce importem licencí softwaru k importu nově vytvořeného souboru. csv.  

7.  Spusťte sestavu funkce Asset Intelligence **License 15a-Third party software slaďování** a ověřte, že licenční informace byly úspěšně importovány do katalogu funkce Asset Intelligence.  

> [!NOTE]  
>  Příklad obecného souboru softwarové licence, který můžete použít pro účely testování, najdete v tématu [příklad funkce Asset Intelligence soubor importu obecné licence](../../../../core/clients/manage/asset-intelligence/example-asset-intelligence-general-license-import.md).  

#### <a name="sample-table-to-describe-software-licenses"></a>Ukázková tabulka pro popis softwarových licencí  
 Při vytváření souboru importu obecné licenční smlouvy můžete k popisu softwarových licencí, které se mají naimportovat do katalogu Asset Intelligence, použít informace v následující tabulce.  

|Název sloupce|Datový typ|Vyžadováno|Příklad|  
|-----------------|---------------|--------------|-------------|  
|Name|Až 255 znaků|Ano|Softwarový titul|  
|Publisher|Až 255 znaků|Ano|Vydavatel softwaru|  
|Verze|Až 255 znaků|Ano|Verze softwarového titulu|  
|Jazyk|Až 255 znaků|Ano|Jazyk softwarového titulu|  
|EffectiveQuantity|Celočíselná hodnota|Ano|Počet zakoupených licencí|  
|PONumber|Až 255 znaků|Ne|Informace o objednávce|  
|ResellerName|Až 255 znaků|Ne|Informace o prodejci|  
|DateOfPurchase|Datová hodnota ve formátu MM/DD/RRRR|Ne|Datum zakoupení licence|  
|SupportPurchased|Bitová hodnota|Ne|0 nebo 1: 0 – Ano, 1 – Ne|  
|SupportExpirationDate|Datová hodnota ve formátu MM/DD/RRRR|Ne|Datum ukončení zakoupené podpory|  
|Komentáře|Až 255 znaků|Ne|Volitelné poznámky|  

###  <a name="configure-asset-intelligence-maintenance-tasks"></a><a name="BKMK_ConfigureMaintenanceTasks"></a> Configure Asset Intelligence maintenance tasks  
 Pro funkci Asset Intelligence jsou dostupné následující úlohy údržby:  

-   **Zkontrolovat název aplikace s informacemi o inventáři**: kontroluje, zda je softwarový titul, který je hlášen v inventáři softwaru, odsouhlasen se softwarovým titulem v katalogu funkce Asset Intelligence. Ve výchozím nastavení je tato úloha povolená a naplánovaná pro spuštění v sobotu po 12:00 ráno. a před 5:00 dop. Tato úloha údržby je k dispozici pouze v lokalitě nejvyšší úrovně ve vaší hierarchii Configuration Manager.  

-   **Shrnout nainstalovaná data softwaru**: poskytuje informace, které se zobrazí v pracovním prostoru **prostředky a kompatibilita** v uzlu **software v inventáři** pod uzlem **funkce Asset Intelligence** . Když se úloha spustí, Configuration Manager shromáždí počet všech softwarových titulů v inventáři v primární lokalitě. Ve výchozím nastavení je tato úloha povolená a naplánována na spuštění každý den po 12:00 ráno. a před 5:00 dop. Tato úloha údržby je k dispozici pouze v primárních lokalitách.  

##### <a name="to-configure-asset-intelligence-maintenance-tasks"></a>Konfigurace úloh údržby funkce Asset Intelligence  

1.  V konzole Configuration Manager klikněte na **Správa**  >  **Konfigurace lokality**  >  **lokality**.  

3.  Vyberte lokalitu, na které chcete nakonfigurovat úlohu údržby funkce Asset Intelligence.  

4.  Na kartě **Domů** ve skupině **Nastavení** vyberte **Údržba lokality**. Vyberte úlohu a upravte nastavení kliknutím na **Upravit** . 

    Doporučujeme nastavit časový interval na dobu mimo špičku tohoto webu. Časový interval určuje časové rozpětí, kdy se úloha může spustit. Definuje ho nastavení **Spustit po** a **Nejpozdější čas spuštění** zadané v dialogovém okně **Vlastnosti úlohy** .  

    Úlohu můžete hned spustit, pokud vyberete aktuální den a **Spustit po** nastavíte na čas, který nastane za několik minut.  

7.  Kliknutím na **tlačítko OK** uložte nastavení. Úloha se teď bude spouštět podle zadaného plánu.  

    > [!NOTE]  
    >  Pokud se úloha při prvním pokusu nepodaří spustit, Configuration Manager se pokusí úlohu znovu spustit, dokud se úloha nesplní nebo dokud neuplyne časový interval, ve kterém se úloha mohla spustit.  
