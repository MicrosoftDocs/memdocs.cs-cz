---
title: Metody zjišťování
titleSuffix: Configuration Manager
description: Seznamte se s dostupnými metodami zjišťování k vyhledání zařízení v síti, ze služby Active Directory nebo Azure Active Directory.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ed931751-18f2-4230-a09e-a0a329fbfa1c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: af35d5a941d5fd9bde2f87c8fb700b9d85e10b00
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078647"
---
# <a name="about-discovery-methods-for-configuration-manager"></a>O metodách zjišťování pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Metody zjišťování Configuration Manager najít různá zařízení v síti, zařízení a uživatele ze služby Active Directory nebo uživatele z Azure Active Directory (Azure AD). Chcete-li efektivně používat metodu zjišťování, měli byste porozumět dostupným konfiguracím a omezením.  



##  <a name="active-directory-forest-discovery"></a><a name="bkmk_aboutForest"></a>Zjišťování doménové struktury služby Active Directory  
 **Konfigurovatelné:** Ano  

 **Povoleno ve výchozím nastavení:** Ne  

 **Účty** , které můžete použít ke spuštění této metody:  

-   **Účet zjišťování doménové struktury služby Active Directory** (definovaný uživatelem)  

-   **Účet počítače** serveru lokality  

Na rozdíl od jiných metod zjišťování služby Active Directory nezjistí zjišťování doménových struktur služby Active Directory prostředky, které můžete spravovat. Místo toho tato metoda zjistí umístění v síti, která jsou nakonfigurovaná ve službě Active Directory. Může převést tato umístění na hranice pro použití v celé vaší hierarchii.  

Když se tato metoda spustí, vyhledá místní doménovou strukturu služby Active Directory, každou důvěryhodnou doménovou strukturu a každou další doménovou strukturu, kterou nakonfigurujete v uzlu **doménové struktury služby Active Directory** konzoly Configuration Manager.  

Zjišťování doménové struktury služby Active Directory můžete použít k těmto akcím:  

-   Vyhledejte lokality a podsítě služby Active Directory a pak vytvořte Configuration Manager hranice na základě těchto umístění v síti.  

-   Identifikujte sítě, které jsou přiřazeny k lokalitě služby Active Directory. Převeďte jednotlivé tuto nadsíťy na hranici rozsahu IP adres.  

-   Publikování do Active Directory Domain Services (služba AD DS) v doménové struktuře, pokud je povoleno publikování v této doménové struktuře. Zadaný účet doménové struktury služby Active Directory musí mít oprávnění k této doménové struktuře.  

Zjišťování doménové struktury služby Active Directory můžete spravovat v konzole Configuration Manager. Přejdete do pracovního prostoru **Správa** a rozbalte možnost **Konfigurace hierarchie**.   

-   **Metody zjišťování**: povolí spuštění zjišťování doménové struktury služby Active Directory v lokalitě nejvyšší úrovně ve vaší hierarchii. Můžete také zadat jednoduchý plán pro spuštění zjišťování. Nakonfigurujte ji tak, aby automaticky vytvářela hranice z podsítí protokolu IP a lokalit služby Active Directory, které zjistí. Zjišťování doménové struktury služby Active Directory nelze spustit v podřízené primární lokalitě nebo v sekundární lokalitě.  

-   **Doménové struktury služby Active Directory**: Nakonfigurujte další doménové struktury, které chcete zjišťovat, určete jednotlivé účty doménové struktury služby Active Directory a nakonfigurujte publikování pro každou doménovou strukturu. Monitorujte proces zjišťování. Přidejte podsítě protokolu IP a lokality služby Active Directory jako hranice Configuration Manager a členy skupin hranic.  

Chcete-li konfigurovat publikování pro doménové struktury služby Active Directory pro každou lokalitu v hierarchii, Připojte konzolu Configuration Manager k lokalitě nejvyšší úrovně ve vaší hierarchii. Karta **publikování** v dialogovém okně **vlastnosti** lokality služby Active Directory může zobrazit pouze aktuální lokalitu a její podřízené lokality. Pokud je pro doménovou strukturu povoleno publikování a schéma této doménové struktury je pro Configuration Manager rozšířené, budou pro každou lokalitu, která je povolená k publikování do této doménové struktury služby Active Directory, publikovány následující informace:  

-    **SMS –&lt;>kódu lokality**

-   **SMS-MP-&lt;kód lokality> –&lt;název systémového serveru lokality>**  

-   **SMS-SLP-&lt;kód lokality> –&lt;název systémového serveru lokality>**  

-   **SMS-&lt;kód lokality> –&lt;název lokality služby Active Directory nebo podsíť>**  

> [!NOTE]  
>  Sekundární lokality vždy používají k publikování pro službu Active Directory účet počítače serveru sekundární lokality. Pokud chcete, aby sekundární lokality publikovaly do služby Active Directory, ujistěte se, že účet počítače serveru sekundární lokality má oprávnění pro publikování do služby Active Directory. Sekundární lokalita nemůže publikovat data do nedůvěryhodné doménové struktury.  

> [!CAUTION]  
>  Když zrušíte kontrolu možnosti publikování lokality do doménové struktury služby Active Directory, všechny dříve publikované informace pro tuto lokalitu, včetně dostupných rolí systému lokality, se z Active Directory odeberou.  

Akce zjišťování doménové struktury služby Active Directory se zaznamenávají v následujících protokolech:  

-   Všechny akce s výjimkou akcí souvisejících s publikováním se zaznamenávají do souboru **ADForestDisc. log** ve složce ** &lt;InstallationPath> \Logs.** na serveru lokality.  

-   Akce publikování zjišťování doménové struktury služby Active Directory se zaznamenávají do souborů **hman. log** a **Sitecomp. log** ve složce ** &lt;InstallationPath> \Logs.** na serveru lokality.  

Další informace o tom, jak nakonfigurovat tuto metodu zjišťování, najdete v tématu [Konfigurace metod zjišťování](configure-discovery-methods.md#BKMK_ConfigADForestDisc).  



##  <a name="active-directory-group-discovery"></a><a name="bkmk_aboutGroup"></a>Zjišťování skupiny služby Active Directory  
**Konfigurovatelné:** Ano  

**Povoleno ve výchozím nastavení:** Ne  

**Účty** , které můžete použít ke spuštění této metody:  

-   **Účet zjišťování skupiny služby Active Directory** (definovaný uživatelem)  

-   **Účet počítače** serveru lokality  

> [!TIP]  
>  Kromě informací v této části najdete další informace v tématu [běžné funkce skupiny služby Active Directory, systému a zjišťování uživatelů](#bkmk_shared).  

Tuto metodu použijte k vyhledání Active Directory Domain Services k identifikaci:  

-   Místní, globální a univerzální skupiny zabezpečení.  

-   Členství ve skupinách.  

-   Omezené informace o členských počítačích a uživatelích skupiny, a to i v případě, že jiná metoda zjišťování tyto počítače a uživatele předtím nezjistila.  

Tato metoda zjišťování je určena k identifikaci skupin a skupin vztahů členů skupin. Ve výchozím nastavení jsou zjištěny pouze skupiny zabezpečení. Pokud chcete také vyhledat členství v distribučních skupinách, musíte zaškrtnout políčko pro možnost **zjistit členství v distribučních skupinách** na kartě **Možnosti** v dialogovém okně **Vlastnosti zjišťování skupiny služby Active Directory** .  

Funkce zjišťování skupiny služby Active Directory nepodporuje rozšířené atributy služby Active Directory, které lze identifikovat pomocí zjišťování systému služby Active Directory nebo zjišťování uživatelů služby Active Directory. Vzhledem k tomu, že tato metoda zjišťování není optimalizovaná pro zjišťování prostředků počítače a uživatele, zvažte spuštění této metody zjišťování po spuštění zjišťování systému služby Active Directory a zjišťování uživatelů služby Active Directory. Tato metoda je způsobena tím, že tato metoda vytvoří úplný záznam dat zjišťování (DDR) pro skupiny, ale pouze omezené DDR pro počítače a uživatele, kteří jsou členy skupin.  

Můžete nakonfigurovat následující rozsahy zjišťování, které řídí, jak tato metoda vyhledává informace:  

-   **Umístění**: použijte umístění, pokud chcete prohledávat jeden nebo více kontejnerů služby Active Directory. Tato možnost oboru podporuje rekurzivní hledání zadaných kontejnerů služby Active Directory. Tento proces prohledá všechny podřízené kontejnery v kontejneru, který zadáte. Pokračuje, dokud nebudou nalezeny žádné další podřízené kontejnery.  

-   **Skupiny**: použijte skupiny, pokud chcete prohledávat jednu nebo více konkrétních skupin služby Active Directory. **Doména služby Active Directory** můžete nakonfigurovat tak, aby používala výchozí doménu a doménovou strukturu, nebo omezit hledání na jednotlivé řadiče domény. Kromě toho můžete zadat jednu nebo více skupin, které chcete vyhledat. Pokud nezadáte aspoň jednu skupinu, prohledávají se všechny skupiny, které se nacházejí v zadaném umístění **doména služby Active Directory** .  

> [!CAUTION]  
>  Při konfiguraci rozsahu vyhledávání vyberte pouze skupiny, které je třeba zjistit. Toto doporučení je způsobeno tím, že funkce zjišťování skupiny služby Active Directory se pokusí zjistit každého člena skupiny v rozsahu zjišťování. Zjišťování velkých skupin může vyžadovat rozsáhlé využití šířky pásma a prostředků služby Active Directory.  

> [!NOTE]  
>  Než budete moci vytvořit kolekce založené na rozšířených atributech služby Active Directory a zajistit přesné výsledky zjišťování pro počítače a uživatele, spusťte zjišťování systémových dat služby Active Directory nebo zjišťování uživatelů služby Active Directory v závislosti na tom, co chcete zjistit.  

Akce pro zjišťování skupiny služby Active Directory se zaznamenávají do souboru **adsgdis. log** ve složce ** &lt;InstallationPath\>\Logs.** na serveru lokality.  

Další informace o tom, jak nakonfigurovat tuto metodu zjišťování, najdete v tématu [Konfigurace metod zjišťování](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral).  



##  <a name="active-directory-system-discovery"></a><a name="bkmk_aboutSystem"></a>Zjišťování systému služby Active Directory  
**Konfigurovatelné:** Ano  

**Povoleno ve výchozím nastavení:** Ne  

**Účty** , které můžete použít ke spuštění této metody:  

-   **Účet zjišťování systému služby Active Directory** (definovaný uživatelem)  

-   **Účet počítače** serveru lokality  

> [!TIP]  
>  Kromě informací v této části najdete další informace v tématu [běžné funkce skupiny služby Active Directory, systému a zjišťování uživatelů](#bkmk_shared).  

Pomocí této metody zjišťování můžete vyhledat zadaná Active Directory Domain Services umístění pro prostředky počítače, které se dají použít k vytváření kolekcí a dotazů. Klienta Configuration Manager můžete nainstalovat také na zjištěné zařízení pomocí klientské nabízené instalace.  

Ve výchozím nastavení tato metoda zjišťuje základní informace o počítači, včetně následujících atributů:  

-   Název počítače  

-   Operační systém a verze  

-   Název kontejneru služby Active Directory  

-   IP adresa  

-   Lokalita Active Directory  

-   Časové razítko posledního přihlášení  

Aby bylo možné úspěšně vytvořit záznam DDR pro počítač, musí být zjišťování systému služby Active Directory schopno identifikovat účet počítače a potom úspěšně přeložit název počítače na IP adresu.  

V dialogovém okně **Vlastnosti zjišťování systémových součástí služby Active Directory** můžete na kartě **atributy služby Active Directory** Zobrazit úplný seznam výchozích atributů objektů, které zjistí. Můžete také nakonfigurovat metodu pro zjišťování dalších (rozšířených) atributů.  

Akce pro zjišťování systému služby Active Directory se zaznamenávají do souboru **Adsysdis. log** ve složce ** &lt;InstallationPath\>\Logs.** na serveru lokality.  

Další informace o tom, jak nakonfigurovat tuto metodu zjišťování, najdete v tématu [Konfigurace metod zjišťování](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral).  



##  <a name="active-directory-user-discovery"></a><a name="bkmk_aboutUser"></a>Zjišťování uživatelů služby Active Directory  
**Konfigurovatelné:** Ano  

**Povoleno ve výchozím nastavení:** Ne  

**Účty** , které můžete použít ke spuštění této metody:  

-   **Účet zjišťování uživatelů služby Active Directory** (definovaný uživatelem)  

-   **Účet počítače** serveru lokality  

> [!TIP]  
>  Kromě informací v této části najdete další informace v tématu [běžné funkce skupiny služby Active Directory, systému a zjišťování uživatelů](#bkmk_shared).  

Tato metoda zjišťování slouží k vyhledávání Active Directory Domain Services k identifikaci uživatelských účtů a přidružených atributů. Ve výchozím nastavení tato metoda zjišťuje základní informace o uživatelském účtu, včetně následujících atributů:  

-   Uživatelské jméno  

-   Jedinečné uživatelské jméno (včetně názvu domény)  

-   Domain (Doména)  

-   Názvy kontejnerů služby Active Directory  

V dialogovém okně **Vlastnosti zjišťování uživatelů služby Active Directory** můžete na kartě **atributy služby Active Directory** Zobrazit úplný výchozí seznam atributů objektů, které zjišťuje. Můžete také nakonfigurovat metodu pro zjišťování dalších (rozšířených) atributů.

Akce zjišťování uživatelů služby Active Directory se zaznamenávají do souboru **adusrdis. log** ve složce ** &lt;\>InstallationPath \Logs.** na serveru lokality.  

Další informace o tom, jak nakonfigurovat tuto metodu zjišťování, najdete v tématu [Konfigurace metod zjišťování](configure-discovery-methods.md#BKMK_ConfigADDiscGeneral).  



## <a name="azure-active-directory-user-discovery"></a><a name="azureaddisc"></a>Azure Active Directory zjišťování uživatelů

Pomocí služby Azure Active Directory (Azure AD) zjišťování uživatelů můžete hledat v předplatném Azure AD pro uživatele s moderní cloudovou identitou. Zjišťování uživatelů služby Azure AD může najít následující atributy:

- Objektu
- displayName
- pošta
- mailNickname
- onPremisesSecurityIdentifier
- userPrincipalName (Hlavní název uživatele)
- AAD tenantID
- onPremisesDomainName
- onPremisesSamAccountName
- onPremisesDistinguishedName

Tato metoda podporuje úplnou a rozdílovou synchronizaci atributů uživatele ze služby Azure AD. Tyto informace se pak dají použít na souběžných datech zjišťování, která shromáždíte z jiných metod zjišťování.

Akce zjišťování uživatelů Azure AD se zaznamenávají do souboru **SMS_AZUREAD_DISCOVERY_AGENT. log** na serveru lokality nejvyšší úrovně v hierarchii.

Pokud chcete nakonfigurovat zjišťování uživatelů Azure AD, přečtěte si téma [Konfigurace služeb Azure](azure-services-wizard.md) pro správu cloudu. Informace o tom, jak nakonfigurovat tuto metodu zjišťování, najdete v tématu [Konfigurace zjišťování uživatelů Azure AD](configure-discovery-methods.md#azureaadisc).

## <a name="azure-active-directory-user-group-discovery"></a><a name="bkmk_azuregroupdisco"></a>Azure Active Directory zjišťování skupiny uživatelů
<!--3611956-->
*(Zavedeno jako [Předběžná verze funkce](../../manage/pre-release-features.md) verze 1906)*

Můžete zjistit skupiny uživatelů a členy těchto skupin z Azure Active Directory (Azure AD). Zjišťování skupin uživatelů Azure AD může najít následující atributy:

- Objektu
- displayName
- mailNickname
- onPremisesSecurityIdentifier
- AAD tenantID

Akce zjišťování skupin uživatelů Azure AD se zaznamenávají do souboru **SMS_AZUREAD_DISCOVERY_AGENT. log** na serveru lokality nejvyšší úrovně v hierarchii. Informace o tom, jak nakonfigurovat tuto metodu zjišťování, najdete v tématu [Konfigurace zjišťování skupin uživatelů Azure AD](configure-discovery-methods.md#bkmk_azuregroupdisco).

##  <a name="heartbeat-discovery"></a><a name="bkmk_aboutHeartbeat"></a>Zjišťování prezenčního signálu  
**Konfigurovatelné:** Ano  

**Povoleno ve výchozím nastavení:** Ano  

**Účty** , které můžete použít ke spuštění této metody:  

-   **Účet počítače** serveru lokality  

Zjišťování prezenčního signálu se liší od jiných metod zjišťování Configuration Manager. Ve výchozím nastavení je povolen a spouští se v každém klientském počítači (místo na serveru lokality) k vytvoření DDR. V případě klientů mobilních zařízení je tento záznam DDR vytvořen bodem správy, který používá klient mobilního zařízení. Chcete-li zajistit udržování záznamu databáze Configuration Manager klientů, nepovolujte zjišťování prezenčního signálu. Kromě udržování záznamu v databázi může tato metoda vynutit zjišťování počítače jako nového záznamu prostředku. Může také znovu naplnit záznam databáze počítače, který byl odstraněn z databáze.  

Zjišťování prezenčního signálu běží podle plánu nakonfigurovaného pro všechny klienty v hierarchii. Výchozí plán zjišťování prezenčního signálu je nastaven na každých 7 dní. Pokud změníte interval zjišťování prezenčního signálu, ujistěte se, že je spuštěn častěji než úloha údržby lokality **Odstranit stará data zjišťování**. Tento úkol vymaže z databáze lokality neaktivní záznamy klientů. V primárních lokalitách můžete nakonfigurovat úlohu **Odstranit zastaralá data zjišťování** . 

Zjišťování prezenčního signálu můžete také ručně vyvolat pro konkrétního klienta. Spusťte **cyklus shromažďování dat zjišťování** na kartě **akce** ovládacího panelu Configuration Manager klienta.  

Když je zjišťování prezenčního signálu spuštěné, vytvoří se záznam DDR, který obsahuje aktuální informace o klientovi. Klient pak tento malý soubor (přibližně o velikosti 1 KB) zkopíruje do bodu správy, aby jej mohla primární lokalita zpracovat. Soubor obsahuje následující informace:  

-   Síťové umístění  

-   Název pro rozhraní NetBIOS  

-   Verze agenta klienta  

-   Podrobnosti provozního stavu  

Zjišťování prezenčního signálu je jedinou metodou zjišťování, která poskytuje podrobné informace o stavu instalace klienta. Tím se aktualizuje atribut klienta systémového prostředku, aby se nastavila hodnota rovna hodnotě **Ano**.  

> [!NOTE]  
>  I když je zjišťování prezenčního signálu zakázané, záznamy DDR se ještě vytvoří a odešlou pro aktivní klienty mobilních zařízení. Tím se zajistí, že úkol, který má **Odstranit zastaralá data zjišťování** , nebude mít vliv na aktivní mobilní zařízení. Když úloha **Odstranit zastaralá data zjišťování** odstraní záznam databáze pro mobilní zařízení, odvolá také certifikát zařízení. Tato akce blokuje připojení mobilního zařízení k bodům správy.  

Akce zjišťování prezenčního signálu se zaznamenávají do těchto umístění:  

-   U klientských počítačů se akce zjišťování prezenčního signálu zaznamenávají v klientovi v souboru **InventoryAgent. log** ve složce *%Windir%\CCM\Logs* .  

-   U klientů mobilních zařízení se akce zjišťování prezenčního signálu zaznamenávají do souboru **DMPRP. log** ve složce *% Program Files%\CCM\Logs* bodu správy, kterou používá klient mobilního zařízení.  

Další informace o tom, jak nakonfigurovat tuto metodu zjišťování, najdete v tématu [Konfigurace metod zjišťování](configure-discovery-methods.md#BKMK_ConfigHBDisc).  



##  <a name="network-discovery"></a><a name="bkmk_aboutNetwork"></a>Zjišťování sítě  
**Konfigurovatelné:** Ano  

**Povoleno ve výchozím nastavení:** Ne  

**Účty** , které můžete použít ke spuštění této metody:  

-   **Účet počítače** serveru lokality  

Tuto metodu použijte, chcete-li zjistit topologii vaší sítě a vyhledat zařízení v síti s IP adresou. Zjišťování sítě vyhledá v síti prostředky s povoleným protokolem IP pomocí dotazu na následující entity: 
- Servery, na kterých běží implementace DHCP od Microsoftu
- Mezipaměť protokolu ARP (Address Resolution Protocol) ve směrovačích sítě
- Zařízení s podporou protokolu SNMP
- Domény služby Active Directory  

Než budete moci použít zjišťování sítě, je nutné určit *úroveň* zjišťování, které se má spustit. Také nakonfigurujete jeden nebo více mechanismů zjišťování, které umožní zjišťování sítě Dotázat se na síťové segmenty nebo zařízení. Můžete také nakonfigurovat nastavení, která umožňují řídit akce zjišťování v síti. Nakonec definujete jeden nebo více plánů pro spuštění zjišťování sítě.  

Aby tato metoda úspěšně zjistila prostředek, zjišťování sítě musí identifikovat IP adresu a masku podsítě daného prostředku. K identifikaci masky podsítě objektu slouží následující metody:  

-   **Mezipaměť protokolu ARP směrovače:** Funkce zjišťování sítě se dotazuje mezipaměti protokolu ARP směrovače, aby se vyhledaly informace o podsíti. Data v mezipaměti protokolu ARP směrovače mají obvykle krátký čas do provozu. Proto když funkce zjišťování sítě dotazuje mezipaměť protokolu ARP, mezipaměť protokolu ARP již nemusí mít informace o požadovaném objektu.  

-   **Protokol DHCP:** Funkce zjišťování sítě se dotazuje na každý server DHCP, který zadáte, abyste zjistili zařízení, pro která server DHCP poskytoval zapůjčení. Funkce zjišťování sítě podporuje pouze servery DHCP, na kterých běží implementace DHCP od společnosti Microsoft.  

-   **Zařízení SNMP:** Zjišťování sítě se může přímo dotazovat na zařízení SNMP. Aby zjišťování sítě mohlo dotazovat se na zařízení, musí mít nainstalovaného místního agenta SNMP. Nakonfigurujte také funkci zjišťování sítě tak, aby používala název komunity, kterou používá Agent SNMP.  

Když zjišťování identifikuje objekt s podporou IP adres a může určit masku podsítě objektu, vytvoří pro tento objekt záznam DDR. Vzhledem k tomu, že různé typy zařízení se připojují k síti, zjišťování sítě zjišťuje prostředky, které nepodporují klienta Configuration Manager. Například zařízení, která se dají zjistit, ale nejsou spravovaná, zahrnují tiskárny a směrovače.  

Zjišťování sítě může vracet několik atributů jako součást záznamu zjišťování, který vytvoří. K těmto atributům patří:  

-   Název pro rozhraní NetBIOS  

-   IP adresy  

-   Doména prostředků  

-   Systémové role  

-   Název komunity SNMP  

-   Adresy MAC  

Aktivita zjišťování sítě je zaznamenána v souboru **Netdisc. log** v * &lt;InstallationPath\>\Logs.* na serveru lokality, který spouští funkci zjišťování.  

 Další informace o tom, jak nakonfigurovat tuto metodu zjišťování, najdete v tématu [Konfigurace metod zjišťování](configure-discovery-methods.md#BKMK_ConfigNetworkDisc).  

> [!NOTE]  
>  Složité sítě a připojení s nízkou šířkou pásma můžou způsobit pomalý chod zjišťování sítě a vygenerování významného síťového provozu. Osvědčeným postupem je spustit zjišťování sítě pouze v případě, že jiné metody zjišťování nemůžou najít prostředky, které je třeba zjistit. Zjišťování sítě můžete například použít, pokud potřebujete zjistit počítače pracovní skupiny. Jiné metody zjišťování nezjišťují počítače v pracovní skupině.  

###  <a name="levels-of-network-discovery"></a><a name="BKMK_NetDiscLevels"></a>Úrovně zjišťování sítě  
Při konfiguraci zjišťování sítě zadáte jednu ze tří úrovní zjišťování:  

|Úroveň zjišťování|Podrobnosti|  
|------------------------|-------------|  
|Topologie|Tato úroveň zjišťuje směrovače a podsítě, ale neidentifikuje masku podsítě pro objekty.|  
|Topologie a klient|Kromě topologie Tato úroveň zjišťuje potenciální klienty, jako jsou počítače, a prostředky, jako jsou tiskárny a směrovače. Tato úroveň zjišťování se pokusí identifikovat masku podsítě objektů, které najde.|  
|Topologie, klient a operační systém klienta|Kromě topologie a potenciálních klientů se tato úroveň pokusí zjistit název a verzi operačního systému počítače. Tato úroveň používá volání prohlížeče Windows a sítě Windows.|  

 U každé přírůstkové úrovně zjišťování sítě zvyšuje jeho činnost a využití šířky pásma sítě. Zvažte síťový provoz, který se může vygenerovat předtím, než povolíte všechny aspekty zjišťování sítě.  

 Například při prvním použití zjišťování sítě můžete začít pouze s úrovní topologie k identifikaci síťové infrastruktury. Pak znovu nakonfigurujte zjišťování sítě, aby bylo možné zjišťovat objekty a jejich operační systémy. Můžete také nakonfigurovat nastavení, které omezí zjišťování sítě na konkrétní rozsah segmentů sítě. Tímto způsobem můžete zjistit objekty v síťových umístěních, která potřebujete, a vyhnout se zbytečnému síťovému provozu. Tento proces také umožňuje zjišťovat objekty z hraničních směrovačů nebo mimo vaši síť.  

###  <a name="network-discovery-options"></a><a name="BKMK_NetDiscOptions"></a>Možnosti zjišťování sítě  
Pokud chcete zjišťování sítě povolit hledání zařízení s podporou IP adres, nakonfigurujte jednu nebo více těchto možností.  

> [!NOTE]  
>  Zjišťování sítě běží v kontextu účtu počítače serveru lokality, na kterém je zjišťování spuštěno. Pokud účet počítače nemá oprávnění k nedůvěryhodné doméně, konfigurace domén a serverů DHCP může nepodařit zjistit prostředky.  

#### <a name="dhcp"></a>DHCP  

Zadejte každý server DHCP, který má funkce zjišťování sítě dotazovat. (Zjišťování sítě podporuje jenom servery DHCP, na kterých běží implementace DHCP od Microsoftu.)  

-   Zjišťování sítě načte informace pomocí vzdálených volání procedur do databáze na serveru DHCP.  

-   Zjišťování sítě se může dotazovat na 32 a 64 servery DHCP pro seznam zařízení, která jsou zaregistrovaná na každém serveru.  

-   Aby funkce zjišťování sítě úspěšně provedla dotaz na server DHCP, účet počítače serveru, na kterém je zjišťování spuštěno, musí být členem skupiny DHCP Users na serveru DHCP. Tato úroveň přístupu například existuje, pokud je splněn jeden z následujících příkazů:  

    -   Zadaný server DHCP je serverem DHCP serveru, na kterém je zjišťování spuštěno.  

    -   Počítač, který spouští funkci zjišťování a server DHCP, je ve stejné doméně.  

    -   Mezi počítačem, na kterém je spuštěno zjišťování a server DHCP, existuje obousměrný vztah důvěryhodnosti.  

    -   Webový server je členem skupiny DHCP Users.  

-   Když zjišťování sítě vytvoří výčet serveru DHCP, nikdy nezjistí statické IP adresy. Funkce zjišťování sítě nenalezne IP adresy, které jsou součástí vyloučeného rozsahu IP adres na serveru DHCP. Nezjišťují taky IP adresy, které jsou rezervované pro ruční přiřazení.  

#### <a name="domains"></a>Domény  

Zadejte každou doménu, kterou má zjišťování sítě dotazovat.  

-   Účet počítače serveru lokality, který spouští zjišťování, musí mít oprávnění ke čtení řadičů domény v každé zadané doméně.  

-   Pokud chcete zjišťovat počítače z místní domény, musíte povolit službu prohledávání počítačů aspoň na jednom počítači. Tento počítač musí být ve stejné podsíti jako server lokality, na kterém je spuštěno zjišťování sítě.  

-   Funkce zjišťování sítě může vyhledat libovolný počítač, který můžete zobrazit ze serveru lokality při procházení sítě.  

-   Zjišťování sítě načte IP adresu. Pak použije požadavek na odezvu protokolu ICMP (Internet Control Message Protocol) k otestování každého nalezeného zařízení. Příkaz k zadání **příkazu k odeslání**  

#### <a name="snmp-devices"></a>Zařízení SNMP  

Zadejte každé zařízení SNMP, které má funkce zjišťování sítě dotazovat.  

-   Funkce zjišťování sítě načte hodnotu ipNetToMediaTable z libovolného zařízení SNMP, které reaguje na dotaz. Tato hodnota vrátí pole IP adres, které jsou klientskými počítači nebo jinými prostředky, jako jsou tiskárny, směrovače nebo jiná zařízení s podporou IP adres.  

-   K dotazování na zařízení musíte zadat IP adresu nebo název NetBIOS zařízení.  

-   Nakonfigurujte zjišťování sítě tak, aby používalo název komunity zařízení, nebo zařízení odmítne dotaz založený na protokolu SNMP.  


###  <a name="limiting-network-discovery"></a><a name="BKMK_LimitNetDisc"></a>Omezení zjišťování sítě  
Když funkce zjišťování sítě dotazuje zařízení SNMP na hraniční síti, může identifikovat informace o podsítích a zařízeních SNMP, která jsou mimo vaši bezprostřední síť. Pomocí následujících informací můžete omezit zjišťování sítě konfigurací zařízení SNMP, se kterými může zjišťování komunikovat, a zadáním segmentů sítě pro dotazování.  

#### <a name="subnets"></a>Podsítě  

Nakonfigurujte podsítě, které funkce zjišťování sítě použije při použití možností SNMP a DHCP. Tyto dvě možnosti prohledají pouze povolené podsítě.  

Požadavek DHCP může například vracet zařízení z umístění v celé síti. Pokud chcete zjistit pouze zařízení v konkrétní podsíti, zadejte a povolte tuto konkrétní podsíť na kartě **podsítě** v dialogovém okně **Vlastnosti zjišťování sítě** . Když zadáte a povolíte podsítě, omezíte budoucí úlohy zjišťování DHCP a SNMP na tyto podsítě.  

> [!NOTE]  
>  Konfigurace podsítí neomezují objekty, které možnost zjišťování **domén** zjišťuje.  

#### <a name="snmp-community-names"></a>Názvy komunit SNMP  

Pokud chcete zjišťování sítě povolit úspěšné dotazování na zařízení SNMP, nakonfigurujte zjišťování sítě pomocí názvu komunity zařízení. Pokud zjišťování sítě není nakonfigurováno pomocí názvu komunity zařízení SNMP, zařízení tento dotaz odmítne.  

#### <a name="maximum-hops"></a>Maximální počet segmentů směrování  

Když nakonfigurujete maximální počet segmentů směrování směrovačů, omezíte počet segmentů sítě a směrovačů, které může funkce zjišťování sítě využít k dotazování pomocí protokolu SNMP.  

Počet nakonfigurovaného směrování omezuje počet dalších zařízení a segmentů sítě, které může funkce zjišťování sítě dotazovat.  

Například zjišťování pouze topologie s přesměrováním směrovače **0** (nula) zjistí podsíť, ve které se nachází původní server. Zahrnuje všechny směrovače v této podsíti.  

Následující diagram znázorňuje, co najde jenom dotaz zjišťování sítě jenom topologie, když běží na serveru 1 s určeným počtem 0 skoků směrovače: podsíť D a směrovač 1.  

 ![Obrázek zjišťování s nulovým skokem směrovače](media/Disc-0.gif)  

 Následující diagram znázorňuje, co najde topologie a dotaz na zjišťování sítě klienta, když běží na serveru 1 s určeným počtem 0 skoků směrovače: podsíť D a směrovač 1 a všechny potenciální klienty v podsíti D.  

 ![Obrázek zjišťování s jedním skokem směrovače](media/Disc-1.gif)  

 Chcete-li získat lepší představu o tom, jak další segmenty směrování můžou zvýšit počet zjištěných síťových prostředků, zvažte následující síť:  

 ![Obrázek zjišťování se dvěma odkazy směrovače](media/Disc-2.gif)  

 Spuštění zjišťování sítě pouze topologie ze serveru 1 s jedním směrováním směrovače zjistí následující entity:  

-   Směrovač 1 a podsíť 10.1.10.0 (našlo se s nulovými segmenty směrování)  

-   Podsítě 10.1.20.0 a 10.1.30.0, podsíť a a směrovač 2 (našlo se při prvním směrování)  

> [!WARNING]  
>  Každé zvýšení počtu směrování směrovačů může výrazně zvýšit počet zjistitelných prostředků a zvýšit šířku pásma sítě, kterou používá zjišťování sítě.  



##  <a name="server-discovery"></a><a name="bkmk_aboutServer"></a>Zjišťování serveru  
**Konfigurovatelné:** Ne  

Kromě uživatelsky konfigurovatelné metody zjišťování Configuration Manager používá proces s názvem **zjišťování serveru** (SMS_WINNT_SERVER_DISCOVERY_AGENT). Tato metoda zjišťování vytváří záznamy prostředků pro počítače, které jsou systémy lokality, například počítač, který je nakonfigurován jako bod správy.  



##  <a name="common-features-of-active-directory-group-discovery-system-discovery-and-user-discovery"></a><a name="bkmk_shared"></a>Běžné funkce zjišťování skupiny služby Active Directory, zjišťování systému a zjišťování uživatelů  
V této části najdete informace o funkcích, které jsou běžné pro následující metody zjišťování:  

-   Zjišťování skupiny aktivního adresáře  

-   Zjišťování systému aktivního adresáře  

-   Zjišťování uživatele Active Directory  

> [!NOTE]  
>  Informace v této části se nevztahují na zjišťování doménové struktury služby Active Directory.  

Tyto tři metody zjišťování jsou v konfiguraci a provozu podobné. Můžou zjišťovat počítače, uživatele a informace o členství prostředků ve skupině, které jsou uložené v Active Directory Domain Services. Proces zjišťování je spravován agentem zjišťování. Agent běží na serveru lokality v každé lokalitě, kde je zjišťování nakonfigurované na spouštění. Každou z těchto metod zjišťování můžete nakonfigurovat tak, aby jako instance umístění v místní doménové struktuře nebo ve vzdálených doménových strukturách hledala jedno nebo několik umístění služby Active Directory.  

Když zjišťování vyhledá prostředky v nedůvěryhodné doménové struktuře, musí být agent zjišťování schopný vyřešit následující postup, aby bylo úspěšné:  

-   Aby bylo možné zjistit prostředek počítače pomocí zjišťování systémových prostředků služby Active Directory, musí být agent zjišťování schopný přeložit plně kvalifikovaný název domény prostředku. Pokud se plně kvalifikovaný název domény nedá přeložit, pokusí se prostředek přeložit podle názvu NetBIOS.  

-   Chcete-li zjistit prostředek uživatele nebo skupiny pomocí zjišťování uživatelů služby Active Directory nebo zjišťování skupiny služby Active Directory, musí být agent zjišťování schopný přeložit plně kvalifikovaný název domény pro název řadiče domény, který zadáte pro umístění služby Active Directory.  

Pro každé umístění, které zadáte, můžete nakonfigurovat jednotlivé možnosti hledání, jako je povolení rekurzivního vyhledávání podřízených kontejnerů služby Active Directory. Můžete také nakonfigurovat jedinečný účet, který bude použit při hledání daného umístění. Tento účet poskytuje flexibilitu při konfiguraci metody zjišťování v jedné lokalitě pro hledání více umístění služby Active Directory ve více doménových strukturách. Nemusíte konfigurovat jeden účet, který má oprávnění pro všechna umístění.  

Pokud se každá z těchto tří metod zjišťování spustí v určité lokalitě, server lokality Configuration Manager v této lokalitě kontaktuje nejbližší řadič domény v zadané doménové struktuře služby Active Directory za účelem vyhledání prostředků služby Active Directory. Doména a doménová struktura může být v libovolném podporovaném režimu služby Active Directory. Účet, který přiřadíte do každé instance umístění, musí mít oprávnění ke **čtení** pro zadaná umístění služby Active Directory.

Zjišťování vyhledá objekty v zadaném umístění a poté se pokusí shromáždit informace o těchto objektech. Záznam DDR se vytvoří, když je možné identifikovat dostatečné informace o prostředku. Požadované informace se liší v závislosti na použité metodě zjišťování.  

Pokud nakonfigurujete stejnou metodu zjišťování, aby běžela na různých Configuration Managerch lokalitách, aby bylo možné využít dotazování na místní servery služby Active Directory, můžete každou lokalitu nakonfigurovat s jedinečnou sadou možností zjišťování. Vzhledem k tomu, že jsou data zjišťování sdílena s každou lokalitou v hierarchii, je třeba se překrývat mezi těmito konfiguracemi a efektivně tak odhalit jednotlivé prostředky.

U menších prostředí zvažte spuštění jednotlivých metod zjišťování pouze v jedné lokalitě v hierarchii. Tato konfigurace snižuje režijní náklady na správu a možnost různých akcí zjišťování pro opakované zjišťování stejných prostředků. Když minimalizujete počet lokalit, na kterých zjišťování spouštíte, zmenšíte celkovou šířku pásma sítě, kterou zjišťování používá. Můžete také snížit celkový počet záznamů DDR, které jsou vytvořeny a které musí být zpracovány vašimi servery lokality.  

Mnohé z konfigurací metod zjišťování jsou vysvětlivekné. Následující části obsahují další informace o možnostech zjišťování, které mohou vyžadovat další informace před jejich konfigurací.  

K dispozici jsou následující možnosti pro použití s více metodami zjišťování služby Active Directory:  

-   [Zjišťování rozdílů](#bkmk_delta)  

-   [Filtrování zastaralých záznamů počítačů podle přihlášení k doméně](#bkmk_stalelogon)  

-   [Filtrovat zastaralé záznamy podle hesla počítače](#bkmk_stalepassword)  

-   [Hledat přizpůsobené atributy služby Active Directory](#bkmk_customAD)  


###  <a name="delta-discovery"></a><a name="bkmk_delta"></a>Zjišťování rozdílů  
K dispozici pro:  

-   Zjišťování skupiny aktivního adresáře  

-   Zjišťování systému aktivního adresáře  

-   Zjišťování uživatele Active Directory  

Zjišťování rozdílů není nezávislou metodou zjišťování, ale k dispozici je možnost pro příslušné metody zjišťování. Zjišťování rozdílů prohledává specifické atributy služby Active Directory pro změny, které byly provedeny od posledního plného cyklu zjišťování příslušné metody zjišťování. Změny atributů se odesílají do databáze Configuration Manager, aby se aktualizoval záznam zjišťování prostředku.  

Ve výchozím nastavení běží rozdílové zjišťování v průběhu pěti minut. Tento plán je mnohem častější než běžný plán pro plný cyklus zjišťování. Tento častý cyklus je možný, protože rozdílové zjišťování používá méně serveru lokality a síťových prostředků než plný cyklus zjišťování. Když použijete zjišťování rozdílů, můžete snížit četnost plného cyklu zjišťování pro tuto metodu zjišťování.  

Níže jsou uvedené nejběžnější změny, které zjišťování rozdílů detekuje:  

-   Nové počítače nebo uživatelé přidaní do služby Active Directory  

-   Změny v základních informacích o počítači a uživateli  

-   Nové počítače nebo uživatelé přidaní do skupiny  

-   Počítače nebo uživatelé odebraní ze skupiny  

-   Změny objektů systémové skupiny  

I když zjišťování rozdílů dokáže detekovat nové prostředky a změny členství ve skupinách, nemůže zjistit, kdy byl prostředek odstraněn ze služby Active Directory. Záznamy DDR vytvořené pomocí zjišťování rozdílů jsou zpracovány podobně jako záznamy DDR, které jsou vytvářeny plným cyklem zjišťování.  

Zjišťování rozdílů konfigurujete na kartě **plán cyklického dotazování** ve vlastnostech pro každou metodu zjišťování.  


###  <a name="filter-stale-computer-records-by-domain-logon"></a><a name="bkmk_stalelogon"></a>Filtrování zastaralých záznamů počítačů podle přihlášení k doméně  
K dispozici pro:  

-   Zjišťování skupiny aktivního adresáře  

-   Zjišťování systému aktivního adresáře  

Zjišťování můžete nakonfigurovat tak, aby vyloučilo počítače se záznamem zastaralý počítač. Toto vyloučení vychází z posledního přihlášení počítače k doméně. Pokud je tato možnost povolena, funkce zjišťování systému služby Active Directory vyhodnocuje každý počítač, který identifikuje. Zjišťování skupiny služby Active Directory vyhodnocuje každý počítač, který je členem skupiny, která je zjištěna.  

Chcete-li použít tuto možnost:  

-   Počítače musí být nakonfigurovány tak, aby aktualizovaly atribut **lastLogonTimestamp** v Active Directory Domain Services.  

-   Úroveň funkčnosti domény služby Active Directory musí být nastavená na Windows Server 2003 nebo novější.  

Pokud konfigurujete čas po posledním přihlášení, které chcete použít pro toto nastavení, vezměte v úvahu interval replikace mezi řadiči domény.  

Filtrování se konfiguruje na kartě **možnost** v dialogových oknech **Vlastnosti zjišťování systémových systémů služby Active Directory** a **Vlastnosti zjišťování skupiny služby Active Directory** . Vyberte, **zda chcete zjišťovat pouze počítače, které se přihlásily k doméně v daném časovém období**.  

> [!WARNING]  
>  Když tento filtr nakonfigurujete a **filtrujete zastaralé záznamy podle hesla počítače**, funkce zjišťování nezahrnuje počítače, které splňují kritéria některého z filtrů.  


###  <a name="filter-stale-records-by-computer-password"></a><a name="bkmk_stalepassword"></a>Filtrovat zastaralé záznamy podle hesla počítače  
K dispozici pro:  

-   Zjišťování skupiny aktivního adresáře  

-   Zjišťování systému aktivního adresáře  

Zjišťování můžete nakonfigurovat tak, aby vyloučilo počítače se záznamem zastaralý počítač. Toto vyloučení vychází z poslední aktualizace hesla účtu počítače v počítači. Pokud je tato možnost povolena, funkce zjišťování systému služby Active Directory vyhodnocuje každý počítač, který identifikuje. Zjišťování skupiny služby Active Directory vyhodnocuje každý počítač, který je členem skupiny, která je zjištěna.  

Chcete-li použít tuto možnost:  

-   Počítače musí být nakonfigurovány tak, aby aktualizovaly atribut **pwdLastSet** v Active Directory Domain Services.  

Při konfiguraci této možnosti zvažte interval aktualizace tohoto atributu. Zvažte také interval replikace mezi řadiči domény.  

Filtrování se konfiguruje na kartě **možnost** v dialogových oknech **Vlastnosti zjišťování systémových systémů služby Active Directory** a **Vlastnosti zjišťování skupiny služby Active Directory** . Vyberte, **zda chcete zjišťovat pouze počítače, které v daném časovém období aktualizovaly heslo účtu počítače**.  

> [!WARNING]  
>  Když tento filtr nakonfigurujete a **filtrujete zastaralé záznamy podle přihlášení k doméně**, funkce zjišťování nezahrnuje počítače, které splňují kritéria obou filtrů.  


###  <a name="search-customized-active-directory-attributes"></a><a name="bkmk_customAD"></a>Hledat přizpůsobené atributy služby Active Directory  
 K dispozici pro:  

-   Zjišťování systému aktivního adresáře  

-   Zjišťování uživatele Active Directory  

Každá metoda zjišťování podporuje jedinečný seznam atributů služby Active Directory, které mohou být zjištěny.  

Seznam přizpůsobených atributů můžete zobrazit a nakonfigurovat na kartě **atributy služby Active Directory** ve **vlastnostech zjišťování systému služby Active** Directory a v dialogových oknech **Vlastnosti zjišťování uživatelů služby Active Directory** .  
