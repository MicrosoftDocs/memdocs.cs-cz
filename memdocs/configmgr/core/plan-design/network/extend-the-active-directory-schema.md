---
title: Publikování a schéma služby Active Directory
titleSuffix: Configuration Manager
description: Rozšíříte schéma služby Active Directory pro Configuration Manager, abyste zjednodušili proces nasazení a konfigurace klientů.
ms.date: 09/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc15ee7e-4d0a-4463-ae2c-f72d8d45d65d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3595273d55bf01158691fb46587ac264af16bffa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718760"
---
# <a name="prepare-active-directory-for-site-publishing"></a>Příprava služby Active Directory pro publikování webu

*Platí pro: Configuration Manager (Current Branch)*

Když rozšíříte schéma služby Active Directory pro Configuration Manager, zavedete do služby Active Directory nové struktury, které jsou používány Configuration Manager weby k publikování klíčových informací v zabezpečeném umístění, kde k nim klienti můžou snadno přistupovat.  

Při správě místních klientů je vhodné použít Configuration Manager s rozšířeným schématem služby Active Directory. Rozšířené schéma může zjednodušit proces nasazení a nastavování klientů. Rozšířené schéma také umožňuje klientům efektivně vyhledávat prostředky, jako jsou servery obsahu, a další služby, které poskytují různé Configuration Manager role systému lokality.  

-   Pokud nejste obeznámeni s tím, jaké rozšířené schéma poskytuje nasazení Configuration Manager, můžete si přečíst o [rozšíření schématu pro Configuration Manager](../../../core/plan-design/network/schema-extensions.md) , která vám pomůžou toto rozhodnutí udělat.  

-   Pokud rozšířené schéma nepoužíváte, můžete pro vyhledání služeb a serverů systému lokality nastavit jiné metody, třeba DNS a WINS. Tyto metody umístění služby vyžadují další konfiguraci a nejsou pro klienty upřednostňovanou metodou pro umístění služeb. Další informace najdete v článku [Vysvětlení způsobu, jakým klienti hledají služby a prostředky lokality pro Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

-   Pokud bylo vaše schéma služby Active Directory rozšířeno pro Configuration Manager 2007 nebo System Center 2012 Configuration Manager, pak nemusíte nic dělat. Rozšíření schématu jsou beze změny a budou již zavedena.  

Rozšíření schématu je jednorázová akce pro jakoukoli doménovou strukturu. Pokud chcete rozšířit a pak použít rozšířené schéma služby Active Directory, postupujte podle těchto kroků:  

## <a name="step-1-extend-the-schema"></a>Krok 1. Rozšiřte schéma  
Postup při rozšiřování schématu pro Configuration Manager:  

-   Použijte účet, který je členem skupiny zabezpečení Schema Admins.  

-   Být přihlášený k řadiči domény hlavního serveru schémat.  

-   Spusťte nástroj **souboru ExtADSch. exe** nebo použijte nástroj ldifde příkazového řádku se souborem **ConfigMgr_ad_schema. ldf** . Nástroj i soubor jsou ve složce **SMSSETUP\BIN\X64** na instalačním médiu Configuration Manager.  

#### <a name="option-a-use-extadschexe"></a>Možnost A: Použití nástroje Extadsch.exe  

1.  Spuštěním nástroje **extadsch.exe** přidejte nové třídy a atributy do schématu služby Active Directory.  

    > [!TIP]  
    >  Nástroj spusťte z příkazového řádku, abyste během spuštění viděli zpětnou vazbu.  

2.  Zkontrolujte, jestli bylo rozšíření schématu úspěšné, a to tak, že zkontrolujete souboru ExtADSch. log v kořenovém adresáři systémového disku.  

#### <a name="option-b-use-the-ldif-file"></a>Možnost B: Použijte soubor LDIF  

1.  Upravte soubor **ConfigMgr_ad_schema. ldf** a definujte kořenovou doménu služby Active Directory, kterou chcete zvětšit:  

    -   Nahraďte všechny výskyty textu, **DC = x**v souboru úplným názvem domény, kterou chcete zvětšit.  

    -   Pokud má například úplný název domény, která se má zvětšit, má název widgets.microsoft.com, změňte všechny instance DC = x v souboru na **DC = Widgets, DC = Microsoft, DC = com**.  

2.  K importu obsahu **ConfigMgr_ad_schema souboru. ldf** do Active Directory Domain Services použijte nástroj ldifde příkazového řádku:  

    -   Například následující příkazový řádek importuje rozšíření schématu do Active Directory Domain Services, zapne podrobné protokolování a během procesu importu vytvoří soubor protokolu: **ldifde-i-f ConfigMgr_ad_schema. ldf-v-j &lt;umístění k uložení souboru\>protokolu**.  

3.  Chcete-li ověřit, zda bylo rozšíření schématu úspěšné, zkontrolujte soubor protokolu vytvořený pomocí příkazového řádku použitého v předchozím kroku.  

## <a name="step-2--create-the-system-management-container-and-grant-sites-permissions-to-the-container"></a>Krok 2.  Vytvořte kontejner System Management a udělte kontejneru oprávnění lokalit  
 Po rozbalení schématu je nutné vytvořit kontejner s názvem **System Management** v Active Directory Domain Services (služba AD DS):  

-   Tento kontejner vytvoříte jednou v každé doméně, která má primární nebo sekundární lokalitu, která bude publikovat data do služby Active Directory.  

-   Pro každý kontejner udělíte oprávnění k účtu počítače každého serveru primární a sekundární lokality, který bude publikovat data v této doméně. Každý účet potřebuje **Úplné řízení** kontejneru s pokročilým oprávněním, **použít na**, který se rovná **tomuto objektu a všem následným objektům**.  

#### <a name="to-add-the-container"></a>Přidání kontejneru  

1.  Použijte účet, který má oprávnění **Vytvořit všechny podřízené objekty** na kontejneru **Systém** ve službě Active Directory Domain Services.  

2.  Spusťte nástroj **ADSI Edit** (adsiedit. msc) a připojte se k doméně serveru lokality.  

3.  Vytvoření kontejneru:  

    -   Rozbalte **Domain** &lt;plně kvalifikovaný název\>domény počítače domény, rozbalte &lt;rozlišující název\>, klikněte pravým tlačítkem na **CN = System**, zvolte **Nový**a pak zvolte **objekt**.  

    -   V dialogovém okně **vytvořit objekt** zvolte položku **kontejner**a pak klikněte na tlačítko **Další**.  

    -   Do pole **hodnota** zadejte **System Management**a pak zvolte **Next (další**).  

4.  Přiřazení oprávnění:  

    > [!NOTE]  
    >  Pokud chcete, můžete k přidání oprávnění ke kontejneru použít jiné nástroje, například nástroj pro správu uživatelů a počítačů služby Active Directory (dsa.msc).  

    -   Klikněte pravým tlačítkem na **CN = System Management**a pak zvolte **vlastnosti**.  

    -   Zvolte kartu **zabezpečení** , klikněte na tlačítko **Přidat**a poté přidejte účet počítače serveru lokality s oprávněním **Úplné řízení** .  

    -   Zvolte možnost **Upřesnit**, zvolte účet počítače serveru lokality a pak zvolte možnost **Upravit**.  

    -   V seznamu **použít na** vyberte **Tento objekt a všechny odvozené objekty**.  

5.  Kliknutím na **tlačítko OK** zavřete konzolu a uložte konfiguraci.  

## <a name="step-3-set-up-sites-to-publish-to-active-directory-domain-services"></a>Krok 3. Nastavení lokalit pro publikování na Active Directory Domain Services  
 Po nastavení kontejneru se udělují oprávnění a máte nainstalovanou Configuration Manager primární lokalitu, můžete nastavit, aby tato lokalita publikovala data do služby Active Directory.  

 Další informace o publikování najdete v tématu [publikování dat lokality pro Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md).  
