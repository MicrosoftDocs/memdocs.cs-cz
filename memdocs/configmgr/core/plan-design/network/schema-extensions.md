---
title: Rozšíření schématu
titleSuffix: Configuration Manager
description: Rozšíříte schéma služby Active Directory tak, aby podporovalo Configuration Manager.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 95c13c00-909f-4fbb-bbaa-1eba9d54d8c5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1ace560130e43fd5675b51b6d507e84043c01407
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904073"
---
# <a name="schema-extensions-for-configuration-manager"></a>Rozšíření schématu pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Schéma služby Active Directory můžete roztáhnout tak, aby podporovalo Configuration Manager. Tím se upraví schéma služby Active Directory doménové struktury a přidá se nový kontejner a několik atributů, které Configuration Manager lokality používají k publikování klíčových informací ve službě Active Directory, kde je můžou klienti bezpečně používat. Tyto informace můžou zjednodušit nasazení a konfiguraci klientů a pomáhají klientům vyhledat prostředky lokality, jako jsou servery s nasazeným obsahem, nebo které klientům poskytují různé služby.  

-   Je vhodné, abyste schéma služby Active Directory rozšířili, ale není to nutné.  

Před [rozšířením schématu služby Active Directory](https://docs.microsoft.com/sccm/core/plan-design/network/extend-the-active-directory-schema) byste se měli seznámit se službou Active Directory Domain Services a měli byste také umět [upravit schéma služby Active Directory](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc759402(v=ws.10)).  

## <a name="considerations-for-extending-the-active-directory-schema-for-configuration-manager"></a>Pokyny k rozšíření schématu služby Active Directory pro Configuration Manager  

-   Rozšíření schématu služby Active Directory pro Configuration Manager se nezměnila od těch, které Configuration Manager 2007 a Configuration Manager 2012 použít. Pokud jste schéma už pro některou z těchto verzí rozšířili, nemusíte ho rozšiřovat znovu.  

-   Rozšíření schématu je jednorázová a nevratná akce v celé doménové struktuře.  

-   Schéma může zvětšit jenom uživatel, který je členem skupiny Schema Admins nebo který má delegovaná dostatečná oprávnění ke změně schématu.  

-   I když schéma můžete před Configuration Manager spuštěním nebo po spuštění instalačního programu nástroje roztáhnout, je vhodné schéma před zahájením konfigurace nastavení lokalit a hierarchie ještě před tím, než začnete konfigurovat. Můžete tak zjednodušit řadu pozdějších konfiguračních kroků.  

-   Po roztažení schématu se globální katalog služby Active Directory replikuje v celé doménové struktuře. Proto Naplánujte rozšiřování schématu v případě, že provoz replikace nebude mít nepříznivý vliv na jiné procesy závislé na síti:  

    -   V doménových strukturách systému Windows 2000 způsobí rozšíření schématu úplnou synchronizaci celého globálního katalogu.  

    -   Počínaje doménovými strukturami Windows 2003 se replikují jenom nově přidané atributy.  

**Zařízení a klienti, kteří nepoužívají schéma služby Active Directory:**  

-   Mobilní zařízení spravovaná konektorem systému Exchange Server  

-   Klient pro počítače Mac  

-   Klient pro servery se systémem Linux a UNIX  

-   Mobilní zařízení zaregistrovaná službou Configuration Manager  

-   Mobilní zařízení zaregistrovaná službou Microsoft Intune  

-   Starší klienti pro mobilní zařízení  

-   Klienti systému Windows, kteří jsou nakonfigurováni pro správu pouze internetových klientů  

-   Klienti systému Windows, kteří jsou rozpoznáni Configuration Manager na internetu  

## <a name="capabilities-that-benefit-from-extending-the-schema"></a>Možnosti, které rozšíření schématu vylepšuje  
**Instalace klientského počítače a přiřazení lokality** – když počítač se systémem Windows nainstaluje nového klienta, klient vyhledá Active Directory Domain Services vlastnosti instalace.  

-   **Alternativní řešení:** Pokud schéma nerozšiřujete, použijte k zadání podrobností o konfiguraci, které musí počítače nainstalovat, jednu z následujících možností:  

    -   **Použijte klientskou nabízenou instalaci**. Před použitím metody instalace klienta se ujistěte, že jsou splněné všechny požadavky. Další informace naleznete v části "závislosti metod instalace" v tématu [předpoklady pro nasazení klientů do počítačů se systémem Windows](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md).  

    -   **Nainstalujte klienty ručně** a zadejte vlastnosti instalace klienta pomocí vlastností příkazového řádku instalačního programu CCMSetup. Následující vlastnosti jsou povinné:  

        -   Zadejte bod správy nebo cestu ke zdroji, ze které počítač může stáhnout instalační soubory pomocí vlastnosti CCMSetup **/MP: = &lt; název počítače \> ** nebo **/Source: &lt; cesta ke zdrojovým souborům \> klienta** v příkazovém řádku programu CCMSetup během instalace klienta.  

        -   Zadejte seznam počátečních bodů správy, které bude klient používat, aby ho mohl přiřadit k lokalitě a pak stahovat zásady klienta a nastavení lokality. Použijte k tomu vlastnost SMSMP programu CCMSetup Client.msi.  

    -   **Publikujte bod správy ve službě DNS nebo WINS** a nakonfigurujte klienty, aby používali tuto metodu umístění služby.  

**Konfigurace portů pro komunikaci mezi klientem a serverem** – při instalaci klienta se nakonfigurují informace o portech uložené ve službě Active Directory. Pokud později port pro komunikaci klienta se serverem lokality změníte, klient může toto nové nastavení portu získat od služby Active Directory Domain Services.  

-   **Alternativní řešení:** Pokud schéma nerozšíříte, využijte k poskytnutí nové konfigurace portů pro stávající klienty některou z následujících možností:  

    -   **Přeinstalujte klienty** pomocí možností, které konfigurují nový port.  

    -   **Nasaďte do klientů vlastní skript, který aktualizuje údaje o portech**. Pokud klienti nemůžou komunikovat s lokalitou kvůli změně portu, nemůžete k nasazení tohoto skriptu použít Configuration Manager. Můžete například použít zásady skupiny.  

**Scénáře nasazení obsahu** – když vytvoříte obsah v jedné lokalitě a pak ho nasadíte do jiné lokality v hierarchii, přijímající lokalita musí být schopná ověřit podpis podepsaných dat obsahu. To vyžaduje přístup k veřejnému klíči zdrojové lokality, kde jste data vytvořili. Když rozšíříte schéma služby Active Directory pro Configuration Manager, je veřejný klíč lokality dostupný pro všechny lokality v hierarchii.  

-   **Alternativní řešení:** Pokud schéma nerozšíříte, k výměně informací o bezpečnostních klíčích mezi lokalitami použijte nástroj pro údržbu hierarchie **preinst.exe**.  

     Pokud například plánujete vytvořit obsah v primární lokalitě a nasadit jej do sekundární lokality pod jinou primární lokalitou, musíte buď zvětšit schéma služby Active Directory, aby sekundární lokalita mohla získat veřejný klíč zdrojové primární lokality, nebo použít Preinst. exe ke sdílení klíčů mezi dvěma lokalitami přímo.  

## <a name="active-directory-attributes-and-classes"></a>Třídy a atributy služby Active Directory  
Když rozšíříte schéma pro Configuration Manager, do schématu se přidají následující třídy a atributy, které jsou dostupné pro všechny Configuration Manager lokality v této doménové struktuře služby Active Directory.  

-   Atributy:  

    -   CN = mS-SMS-přiřazení-Site-Code  

    -   CN = mS-SMS – možnosti  

    -   CN = MS-SMS-default-MP  

    -   CN = mS-SMS-Device-Management-Point  

    -   CN = mS-SMS-Health-State  

    -   CN = MS-SMS-MP-Address  

    -   CN = MS-SMS-MP-Name  

    -   CN = MS-SMS-rozsah-IP-High  

    -   CN = MS-SMS-rozsah-IP-nízká  

    -   CN = MS-SMS-roaming – hranice  
        on  

    -   CN = MS-SMS-hranice webu  

    -   CN = MS-SMS-site-Code  

    -   CN = mS-SMS-source-doménová struktura  

    -   CN = mS-SMS-Version  

-   Třídy:  

    -   CN = MS-SMS-Management-Point  

    -   CN = MS-SMS-roaming-hranice-rozsah  

    -   CN = MS-SMS-Server-Locator-Point  

    -   CN = MS-SMS-site  

> [!NOTE]
> 
>  Rozšíření schématu můžou zahrnovat atributy a třídy přenesené z předchozích verzí produktu, které Configuration Manager nepoužívá. Příklad:  
> 
> 
> - Atribut: CN = MS-SMS-site-hranice  
>   -   Třída: CN = MS-SMS-Server-Locator-Point  

Předchozí seznamy můžete ověřit zobrazením **ConfigMgr_ad_schema. Soubor LDF** ze složky **\SMSSETUP\BIN\X64** instalačního média Configuration Manager.  
