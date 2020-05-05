---
title: Konfigurace zjišťování
titleSuffix: Configuration Manager
description: Nakonfigurujte metody zjišťování tak, aby vyhledaly prostředky, které se mají spravovat ze sítě, Active Directory a Azure Active Directory.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3bd03cb15ae1633d8ddfc8c2f26a741d2679b083
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721042"
---
# <a name="configure-discovery-methods-for-configuration-manager"></a>Konfigurace metod zjišťování pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Nakonfigurujte metody zjišťování tak, aby vyhledaly prostředky, které se mají spravovat ze sítě, Active Directory a Azure Active Directory (Azure AD). Nejprve povolte a pak nakonfigurujte každou metodu, kterou chcete použít pro hledání v prostředí. Metodu můžete také zakázat pomocí stejného postupu, který použijete k jeho povolení. Jedinou výjimkou z tohoto procesu je zjišťování prezenčního signálu a zjišťování serveru:  

- Ve výchozím nastavení je **zjišťování prezenčního signálu** již povolené při instalaci Configuration Manager primární lokality. Je nastavené tak, aby běžely podle plánu Basic. Nechejte zjišťování prezenčního signálu povolené. Zajišťuje, aby záznamy dat zjišťování (DDR) pro zařízení byly aktuální. Další informace o zjišťování prezenčního signálu najdete v tématu [o zjišťování prezenčního signálu](about-discovery-methods.md#bkmk_aboutHeartbeat).  

- **Zjišťování serveru** je metoda automatického zjišťování. Vyhledá počítače, které používáte jako systémy lokality. Nemůžete ho nakonfigurovat ani zakázat.  


## <a name="active-directory-forest-discovery"></a><a name="BKMK_ConfigADForestDisc"></a>Zjišťování doménové struktury služby Active Directory  

Chcete-li dokončit konfiguraci zjišťování doménové struktury služby Active Directory, nakonfigurujte nastavení v následujících umístěních konzoly Configuration Manager:  

- V uzlu **metody zjišťování** :

  - Povolte tuto metodu zjišťování.  

  - Nastavte plán cyklického dotazování.  

  - Vyberte, jestli zjišťování automaticky vytvoří hranice pro lokality a podsítě služby Active Directory, které zjistí.  

- V uzlu **doménové struktury služby Active Directory** :

  - Přidejte doménové struktury, které chcete zjišťovat.  

  - Povolte zjišťování lokalit a podsítí služby Active Directory v této doménové struktuře.  

  - Nakonfigurujte nastavení, která umožní webům Configuration Manager publikovat informace o lokalitě v doménové struktuře.  

  - Přiřaďte účet, který se má používat jako účet doménové struktury služby Active Directory pro každou doménovou strukturu.  

Pomocí následujících postupů můžete povolit zjišťování doménové struktury služby Active Directory a nakonfigurovat jednotlivé doménové struktury pro použití se zjišťováním doménových struktur služby Active Directory.  

### <a name="configure-active-directory-forest-discovery"></a>Konfigurace zjišťování doménové struktury služby Active Directory  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace hierarchie**a vyberte uzel **metody zjišťování** .  

2. Vyberte metodu zjišťování doménové struktury služby Active Directory pro lokalitu, u které chcete zjišťování nakonfigurovat.  

3. Na kartě **Domů** na pásu karet vyberte možnost **vlastnosti**.  

4. Na kartě **Obecné** ve vlastnostech nakonfigurujte následující nastavení:  

    - Povolte metodu zjišťování.

    - Zadejte možnosti pro vytvoření hranic lokality pro zjištěná umístění.  

    - Zadejte plán, kdy se má zjišťování spouštět.  

5. Kliknutím na **OK** uložte konfiguraci.  

### <a name="configure-a-forest-for-active-directory-forest-discovery"></a>Konfigurace doménové struktury pro zjišťování doménových struktur služby Active Directory  

1. V pracovním prostoru **Správa** rozbalte položku **Konfigurace hierarchie**a vyberte uzel **doménové struktury služby Active Directory** . Jestliže bylo předtím spuštěno zjišťování doménové struktury služby Active Directory, v podokně výsledků uvidíte všechny zjištěné doménové struktury. Když se tato metoda zjišťování spustí, zjistí místní doménovou strukturu a všechny důvěryhodné doménové struktury. Ručně přidejte nedůvěryhodné doménové struktury.  

    - Chcete-li nakonfigurovat dříve zjištěnou doménovou strukturu, vyberte doménovou strukturu v podokně výsledků. Na pásu karet vyberte **vlastnosti** a otevřete vlastnosti doménové struktury.

    - Pokud chcete konfigurovat novou doménovou strukturu, která není uvedená, na kartě **Domů** ve skupině **vytvořit** vyberte **Přidat doménovou strukturu**. Tato akce otevře dialogové okno **Přidat doménové struktury** .

2. Na kartě **Obecné** dokončete konfigurace pro doménovou strukturu, které chcete zjišťovat, a zadejte **účet doménové struktury služby Active Directory**. Další informace o tomto účtu najdete v tématu [účty](../../../plan-design/hierarchy/accounts.md#active-directory-forest-account).  

    > [!NOTE]  
    > Zjišťování doménové struktury služby Active Directory vyžaduje pro zjišťování a publikování na nedůvěryhodných doménových strukturách globální účet. Pokud nepoužíváte účet počítače serveru lokality, můžete vybrat pouze globální účet.  

3. Pokud plánujete, aby lokality publikovaly data lokality do této doménové struktury, na kartě **publikování** dokončete konfigurace pro publikování do této doménové struktury.  

    > [!NOTE]  
    > Pokud umožníte webům publikovat do doménové struktury, rozšíříte schéma služby Active Directory této doménové struktury pro Configuration Manager. Účet doménové struktury služby Active Directory musí mít oprávnění k úplnému řízení kontejneru systému v této doménové struktuře.  

4. Kliknutím na **OK** uložte konfiguraci.  


## <a name="active-directory-discovery-for-computers-users-or-groups"></a><a name="BKMK_ConfigADDiscGeneral"></a>Zjišťování služby Active Directory pro počítače, uživatele nebo skupiny  

Chcete-li nakonfigurovat zjišťování počítačů, uživatelů nebo skupin, začněte s těmito běžnými kroky:

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace hierarchie**a vyberte uzel **metody zjišťování** .  

2. Vyberte metodu pro lokalitu, u které chcete zjišťování nakonfigurovat.  

3. Na kartě **Domů** na pásu karet vyberte možnost **vlastnosti**.  

4. Na kartě **Obecné** ve vlastnostech zaškrtněte políčko pro povolení zjišťování. Nebo můžete zjišťování nakonfigurovat hned a pak se vrátit k povolení zjišťování později.  

Pak použijte informace v následujících částech ke konfiguraci konkrétních metod zjišťování:  

- [Zjišťování skupiny aktivního adresáře](#bkmk_config-adgd)  

- [Zjišťování systému aktivního adresáře](#bkmk_config-adgd)  

- [Zjišťování uživatele Active Directory](#bkmk_config-adud)  

> [!NOTE]  
> Informace v této části se nevztahují na zjišťování doménové struktury služby Active Directory.  

I když je každá z těchto metod zjišťování nezávislá na ostatních, sdílí podobné možnosti. Další informace o těchto možnostech konfigurace najdete v tématu [sdílené možnosti pro zjišťování skupin, systémů a uživatelů](about-discovery-methods.md#bkmk_shared).  

> [!WARNING]  
> Cyklické dotazování služby Active Directory podle každé z těchto metod zjišťování může způsobit výrazné zatížení sítě. Zvažte možnost naplánovat každou metodu zjišťování tak, aby běžela v době, kdy tento síťový provoz nepříznivě neovlivní firemní použití vaší sítě.  

### <a name="configure-active-directory-group-discovery"></a><a name="bkmk_config-adgd"></a>Konfigurace zjišťování skupin služby Active Directory  

1. Na kartě **Obecné** ve okno Vlastnosti zjišťování skupin služby Active Directory vyberte **Přidat** a nakonfigurujte rozsah vyhledávání. Vyberte buď **skupiny** , nebo **umístění**. Pak v dialogovém okně **Přidat skupiny** nebo **Přidat umístění služby Active Directory** dokončete následující konfigurace:  

    1. Zadejte **název** pro tento rozsah vyhledávání.  

    2. Zadejte **doména služby Active Directory** nebo **umístění** pro hledání:  

        - Pokud jste zvolili **skupiny**, určete jednu nebo více skupin služby Active Directory, které chcete zjišťovat.  

        - Pokud jste zvolili možnost **umístění**, zadejte kontejner služby Active Directory jako umístění, které chcete zjistit. Pro toto umístění můžete také povolit rekurzivní hledání podřízených kontejnerů služby Active Directory.  

    3. Zadejte **účet zjišťování skupiny služby Active Directory** , který lokalita používá k vyhledání tohoto oboru zjišťování. Další informace najdete v tématu [účty](../../../plan-design/hierarchy/accounts.md#active-directory-group-discovery-account).  

    4. Vyberte **OK** a uložte konfiguraci oboru zjišťování.  

2. Opakujte předchozí kroky pro každý další rozsah zjišťování, který chcete definovat.  

3. Na kartě **plán cyklického dotazování** nakonfigurujte plán cyklického dotazování plného zjišťování i zjišťování rozdílů.

4. Na kartě **Možnosti** nakonfigurujte nastavení pro odfiltrování nebo vyloučení zastaralých záznamů počítačů ze zjišťování. Také nakonfigurujte zjišťování členství distribučních skupin.  

    > [!NOTE]  
    > Ve výchozím nastavení zjišťování skupin služby Active Directory zjišťuje pouze členství ve skupinách zabezpečení.  

5. Kliknutím na **OK** uložte konfiguraci.  

### <a name="configure-active-directory-system-discovery"></a><a name="bkmk_config-adsd"></a>Konfigurace zjišťování systému služby Active Directory  

1. Na kartě **Obecné** v okno Vlastnosti zjišťování systémových souborů služby Active Directory vyberte ikonu **Nová** ![ikona nové](media/Disc_new_Icon.gif) a zadejte nový kontejner služby Active Directory. V dialogovém okně **kontejner služby Active Directory** dokončete následující konfigurace:  

    1. Zadejte nebo vyhledejte umístění pro **cestu**. Tato hodnota představuje platnou cestu protokolu LDAP ke kontejneru nebo organizační jednotce (OU). Tento web se dotazuje na tuto cestu k prostředkům. Například `LDAP://CN=Computers,DC=contoso,DC=com`.  

    2. Zadejte možnosti, které mění chování hledání:  

        - **Zjistit objekty ve skupinách služby Active Directory**: lokalita také prohlíží členství skupin v této cestě.  

        - **Rekurzivní hledání podřízených kontejnerů služby Active Directory**: Pokud povolíte tuto možnost, lokalita vyhledá další kontejnery nebo organizační jednotky ve výše uvedené cestě. Pokud tuto možnost zakážete, vyhledá web pouze prostředky v konkrétní cestě.  

          Počínaje verzí 1806 vyberte subkontejnery, které mají být vyloučeny z tohoto rekurzivního vyhledávání. Tato možnost pomáhá snížit počet zjištěných objektů. Vyberte **Přidat** a vyberte kontejnery v rámci výše uvedené cesty. V dialogovém okně vybrat nový kontejner vyberte podřízený kontejner, který se má vyloučit. Kliknutím na **OK** zavřete dialogové okno vybrat nový kontejner.<!--1358143-->

          > [!Tip]  
          > Seznam kontejnerů služby Active Directory v rámci zjišťování systémových součástí služby Active Directory okno Vlastnosti obsahuje sloupec **vyloučení**. Když vyberete kontejnery, které se mají vyloučit, tato hodnota je **Yes (Ano**).  

    3. Pro každé umístění zadejte účet, který chcete použít jako **účet zjišťování služby Active Directory**. Další informace najdete v tématu [účty](../../../plan-design/hierarchy/accounts.md#active-directory-system-discovery-account).  

        > [!TIP]  
        > Pro každé zadané umístění můžete nakonfigurovat sadu možností zjišťování a jedinečný účet zjišťování služby Active Directory.  

    4. Výběrem **OK** uložte konfiguraci kontejneru služby Active Directory.  

2. Na kartě **plán cyklického dotazování** nakonfigurujte plán cyklického dotazování plného zjišťování i zjišťování rozdílů.  

3. Na kartě **atributy služby Active Directory** nakonfigurujte další atributy služby Active Directory pro počítače, které chcete zjišťovat. Tato karta obsahuje seznam výchozích atributů objektu.  

    > [!Tip]  
    > Vaše organizace například používá atribut **Description** v účtu počítače ve službě Active Directory. Vyberte **vlastní**a přidejte `Description` jako vlastní atribut. Po spuštění této metody zjišťování se tento atribut zobrazí na kartě Vlastnosti zařízení v konzole Configuration Manager.<!--513948-->  

4. Na kartě **Možnosti** nakonfigurujte nastavení pro odfiltrování nebo vyloučení zastaralých záznamů počítačů ze zjišťování.  

5. Kliknutím na **OK** uložte konfiguraci.  

### <a name="configure-active-directory-user-discovery"></a><a name="bkmk_config-adud"></a>Konfigurace zjišťování uživatelů služby Active Directory  

1. Na kartě **Obecné** ve okno Vlastnosti zjišťování uživatelů služby Active Directory vyberte novou ikonu **Nová** ikona ![](media/Disc_new_Icon.gif) a zadejte nový kontejner služby Active Directory. V dialogovém okně **kontejner služby Active Directory** dokončete následující konfigurace:  

    1. Zadejte jedno nebo více umístění, která chcete vyhledat.  

    2. Pro každé umístění zadejte možnosti, které mění chování hledání.  

    3. Pro každé umístění zadejte účet, který chcete použít jako **účet zjišťování služby Active Directory**. Další informace najdete v tématu [účty](../../../plan-design/hierarchy/accounts.md#active-directory-user-discovery-account).  

        > [!NOTE]  
        > Pro každé zadané umístění můžete nakonfigurovat jedinečnou sadu možností zjišťování a jedinečný účet zjišťování služby Active Directory.  

    4. Výběrem **OK** uložte konfiguraci kontejneru služby Active Directory.  

2. Na kartě **plán cyklického dotazování** nakonfigurujte plán cyklického dotazování plného zjišťování i zjišťování rozdílů.  

3. Na kartě **atributy služby Active Directory** nakonfigurujte další atributy služby Active Directory pro počítače, které chcete zjišťovat. Tato karta obsahuje seznam výchozích atributů objektu.  

4. Kliknutím na **OK** uložte konfiguraci.  


## <a name="azure-ad-user-discovery"></a><a name="azureaadisc"></a>Zjišťování uživatelů Azure AD

Zjišťování uživatelů Azure AD není povolené nebo není nakonfigurované jako jiné metody zjišťování. Nakonfigurujte ho při připojování Configuration Manager lokality do služby Azure AD.

Další informace najdete v tématu [zjišťování uživatelů Azure AD](about-discovery-methods.md#azureaddisc).

### <a name="prerequisites"></a>Požadavky

Pokud chcete tuto metodu zjišťování povolit a nakonfigurovat, [nakonfigurujte služby Azure](azure-services-wizard.md) pro **správu cloudu**.

Pokud k *Vytvoření* aplikace Azure použijete Configuration Manager, nakonfiguruje se aplikace s potřebnými oprávněními.

Pokud vytvoříte aplikaci v Azure jako první a pak ji *naimportujete* do Configuration Manager, musíte aplikaci ručně nakonfigurovat. Tato konfigurace zahrnuje udělení oprávnění aplikace serveru pro čtení dat adresáře.

1. Otevřete [Azure Portal](https://portal.azure.com) jako uživatel s oprávněními *globálního správce* . Přejít na **Azure Active Directory**a vyberte **Registrace aplikací**. V případě potřeby přepněte na **všechny aplikace** .

1. Vyberte cílovou aplikaci.

1. V nabídce **Správa** vyberte **oprávnění rozhraní API**.  

    1. Na panelu **oprávnění rozhraní API** vyberte **Přidat oprávnění**.  

    2. V panelu **oprávnění rozhraní API** přepněte na **rozhraní API, které moje organizace používá**.  

    3. Vyhledejte a vyberte rozhraní **Microsoft Graph** API.  

        > [!Tip]
        > Ve verzi 1810 a starší použijte rozhraní **Azure Active Directory Graph** API.

    4. Vyberte skupinu **oprávnění aplikace** . Rozbalte položku **adresář**a vyberte **adresář. Read. All**.  

    5. Vyberte **Přidat oprávnění**.  

1. Na panelu **oprávnění rozhraní API** v části **souhlas udělení** souhlasu vyberte **udělit souhlas správce...**. Vyberte **Ano**.  

### <a name="configure-azure-ad-user-discovery"></a>Konfigurace zjišťování uživatelů Azure AD

Při konfiguraci služby **Cloud Management** Azure:

- Na stránce **zjišťování** v průvodci vyberte možnost pro **Povolení Azure Active Directory zjišťování uživatelů**.
- Vyberte **Nastavení**.
- V dialogovém okně nastavení zjišťování uživatelů služby Azure AD nakonfigurujte plán, kdy proběhne zjišťování. Můžete také povolit zjišťování rozdílů, které kontroluje pouze nové nebo změněné účty v Azure AD.

> [!Note]  
> Pokud je uživatel federované nebo synchronizovanou identitou, musíte použít Configuration Manager [zjišťování uživatelů služby Active Directory](about-discovery-methods.md#bkmk_aboutUser) a taky zjišťování uživatelů Azure AD. Další informace o hybridních identitách najdete v tématu [definice strategie přijetí hybridní identity](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->


## <a name="azure-ad-user-group-discovery"></a><a name="bkmk_azuregroupdisco"></a>Zjišťování skupin uživatelů Azure AD

<!--3611956-->
> [!Tip]  
> Tato funkce byla poprvé představena ve verzi 1906 jako [funkce předběžné verze](../../manage/pre-release-features.md). Od verze 2002 už není k dispozici funkce předběžného vydání.  

Můžete zjistit skupiny uživatelů a členy těchto skupin z Azure AD. Když lokalita najde uživatele ve skupinách Azure AD, které předtím neodhalili, přidá je jako nové uživatelské prostředky v Configuration Manager. Záznam prostředku skupiny uživatelů se vytvoří, když je skupina skupinou zabezpečení.

### <a name="prerequisites"></a>Požadavky

- [Služba Azure](azure-services-wizard.md) pro správu cloudu
- Oprávnění ke čtení a hledání skupin Azure AD

### <a name="limitations"></a>Omezení

Zjišťování rozdílů pro zjišťování skupin uživatelů Azure AD je aktuálně zakázané.

### <a name="log-files"></a>Soubory protokolů

Pro řešení potíží použijte protokol SMS_AZUREAD_DISCOVERY_AGENT. log. Tento protokol se taky sdílí se zjišťováním uživatelů Azure AD. Další informace najdete v tématu [soubory protokolu](../../../plan-design/hierarchy/log-files.md#BKMK_ServerLogs).

### <a name="enable-azure-ad-user-group-discovery"></a>Povolit zjišťování skupin uživatelů Azure AD

Postup povolení zjišťování na stávající službě Azure **pro správu cloudu** :

1. V pracovním prostoru **Správa** rozbalte položku **Cloud Services**a pak vyberte uzel **služby Azure** .
1. Vyberte jednu z vašich služeb Azure a pak na pásu karet vyberte **vlastnosti** .
1. Na kartě **zjišťování** zaškrtněte políčko pro **povolení zjišťování skupin Azure Active Directory**a pak vyberte **Nastavení**.
1. Na kartě **obory vyhledávání** vyberte **Přidat** .
    - **Plán cyklického dotazování** můžete upravit na druhé kartě.
1. Vyberte jednu nebo více skupin uživatelů. Můžete **Hledat** podle názvu a zvolit, jestli chcete zobrazit **jenom skupiny zabezpečení**.
    - Po prvním výběru **hledání** budete vyzváni k přihlášení k Azure.
1. Po dokončení výběru skupin vyberte **OK** .
1. Po dokončení zjišťování můžete procházet skupiny uživatelů Azure AD v uzlu **Uživatelé** .

Pokud chcete povolit zjišťování při konfiguraci nové služby **Cloud managementu** Azure:

- Na stránce **zjišťování** v průvodci vyberte možnost pro **povolení zjišťování skupin Azure Active Directory**.
- Vyberte **Nastavení**.
- V dialogovém okně nastavení zjišťování skupin služby Azure AD nakonfigurujte rozsah vyhledávání a plán, kdy se má zjišťování provést.


## <a name="heartbeat-discovery"></a><a name="BKMK_ConfigHBDisc"></a>Zjišťování prezenčního signálu

Configuration Manager povoluje metodu zjišťování prezenčního signálu při instalaci primární lokality. Pokud chcete použít výchozí plán každých 7 dní, neexistuje žádná další konfigurace. V opačném případě stačí nakonfigurovat plán, jak často klienti odesílají záznam dat zjišťování prezenčního signálu do bodu správy.  

> [!NOTE]  
> Pokud povolíte klientskou nabízenou instalaci a úlohu údržby lokality pro možnost **Vymazat instalaci** ve stejné lokalitě, nastavte plán zjišťování prezenčního signálu na méně, než je období opětovného **zjišťování klienta** v úloze údržby lokality **Vymazat příznak instalace** . Další informace o úlohách údržby lokality najdete v tématu [úlohy údržby](../../manage/maintenance-tasks.md).  

### <a name="configure-the-heartbeat-discovery-schedule"></a>Konfigurovat plán zjišťování prezenčního signálu  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace hierarchie**a vyberte uzel **metody zjišťování** .  

2. Vyberte metodu **zjišťování prezenčního signálu** pro lokalitu, u které chcete nakonfigurovat zjišťování prezenčního signálu.  

3. Na kartě **Domů** na pásu karet vyberte možnost **vlastnosti**.  

4. Nastavte četnost, s jakou klienti odesílají záznam dat zjišťování prezenčního signálu. Pak kliknutím na **OK** konfiguraci uložte.  


<a name="BKMK_AboutConfigNetworkDisc"></a>

## <a name="network-discovery"></a><a name="BKMK_ConfigNetworkDisc"></a>Zjišťování sítě  

Před konfigurací zjišťování sítě je třeba pochopit následující témata:  

- Dostupné úrovně zjišťování sítě  

- Dostupné možnosti zjišťování sítě  

- Omezení zjišťování sítě v síti  

Další informace najdete v tématu [o zjišťování sítě](about-discovery-methods.md#bkmk_aboutNetwork).  

Následující části obsahují informace o běžných konfiguracích pro zjišťování sítě. Jednu nebo více těchto konfigurací můžete nakonfigurovat pro použití během stejného spuštění zjišťování. Pokud používáte více konfigurací, naplánujte interakce, které mohou ovlivnit výsledky zjišťování.  

Například zjistíte všechna zařízení SNMP (Simple Network Management Protocol), která používají konkrétní název komunity SNMP. Pro stejné spuštění zjišťování zakažte zjišťování v konkrétní podsíti. Když je zjišťování spuštěno, zjišťování sítě nezjistí zařízení SNMP se zadaným názvem komunity v podsíti, kterou jste zakázali.  

### <a name="determine-your-network-topology"></a><a name="BKMK_DetermineNetTopology"></a>Určení síťové topologie  

K namapování sítě můžete použít zjišťování pouze topologie. Tento druh zjišťování neodhalí potenciální klienty. Zjišťování jenom topologie sítě spoléhá na SNMP.  

Při mapování topologie sítě nakonfigurujte **maximální segmenty směrování** na kartě **SNMP** v dialogovém okně **Vlastnosti zjišťování sítě** . Jenom pár segmentů směrování může posloužit k řízení šířky pásma sítě, která se používá při spuštění zjišťování. Když zjistíte více vaší sítě, zvyšte počet směrování, abyste získali lepší porozumění síťové topologii.  

Po pochopení síťové topologie nakonfigurujte další vlastnosti pro zjišťování sítě. Tyto vlastnosti usnadňují zjišťování potenciálních klientů a jejich operačních systémů. Také nakonfigurujte zjišťování sítě tak, aby se omezily síťové segmenty, které může prohledávat.  

Další informace najdete v tématu [určení síťové topologie](#bkmk_proc-top) .

### <a name="network-discovery-search-options"></a>Možnosti vyhledávání zjišťování sítě

Configuration Manager podporuje následující metody vyhledávání v síti:

- [Omezení vyhledávání pomocí podsítí](#BKMK_LimitBySubnet)
- [Vyhledat konkrétní doménu](#BKMK_SearchByDomain)
- [Omezení prohledávání pomocí názvů komunit SNMP](#BKMK_LimitBySNMPname)
- [Prohledat konkrétní server DHCP](#BKMK_SearchByDHCP)

#### <a name="limit-searches-by-using-subnets"></a><a name="BKMK_LimitBySubnet"></a>Omezení vyhledávání pomocí podsítí  

Funkci zjišťování sítě můžete nakonfigurovat tak, aby prohledala konkrétní podsítě během spuštění zjišťování. Ve výchozím nastavení zjišťování sítě vyhledává podsíť serveru, na kterém je zjišťování spuštěno. Všechny další podsítě, které nakonfigurujete a povolíte, se vztahují jenom na možnosti vyhledávání SNMP a DHCP. Když funkce zjišťování sítě prohledává domény, není omezena konfigurací podsítí.  

Pokud zadáte jednu nebo více podsítí na kartě **podsítě** v dialogovém okně **Vlastnosti zjišťování sítě** , prohledají pouze podsítě, které označíte jako **povolené**.  

Když podsíť zakážete, lokalita ji vyloučí ze zjišťování a platí následující podmínky:  

- Dotazy založené na protokolu SNMP nejsou v podsíti spuštěné.  

- Servery DHCP neodpovídají seznamu prostředků umístěných v podsíti.  

- Dotazy založené na doméně můžou zjišťovat prostředky, které se nacházejí v podsíti.  

#### <a name="search-a-specific-domain"></a><a name="BKMK_SearchByDomain"></a>Vyhledat konkrétní doménu  

Funkci zjišťování sítě můžete nakonfigurovat tak, aby prohledala určitou doménu nebo sadu domén během spuštění zjišťování. Ve výchozím nastavení zjišťování sítě vyhledává místní doménu serveru, na kterém je zjišťování spuštěno.  

Pokud zadáte jednu nebo více domén na kartě **domény** v dialogovém okně **Vlastnosti zjišťování sítě** , prohledají se pouze domény, které označíte jako **povolené**.  

Když doménu zakážete, lokalita ji vyloučí ze zjišťování a platí následující podmínky:  

- Zjišťování sítě nedotazuje řadiče domény v dané doméně.  

- Dotazy založené na protokolu SNMP můžou být pořád spuštěné v podsítích v doméně.  

- Servery DHCP stále můžou odpovídat seznamu prostředků umístěných v doméně.  

#### <a name="limit-searches-by-using-snmp-community-names"></a><a name="BKMK_LimitBySNMPname"></a>Omezení prohledávání pomocí názvů komunit SNMP  

Funkci zjišťování sítě můžete nakonfigurovat tak, aby během spuštění zjišťování prohledala konkrétní komunitu nebo sadu komunit SNMP. Ve výchozím nastavení metoda konfiguruje název **veřejné** komunity.  

Funkce zjišťování sítě používá názvy komunit k získání přístupu k směrovačům, které jsou zařízeními SNMP. Směrovač může poskytovat zjišťování sítě s informacemi o jiných směrovačích a podsítích, které jsou propojeny s prvním směrovačem.  

> [!NOTE]  
> Názvy komunit SNMP se podobají heslům. Zjišťování sítě může získat informace jenom ze zařízení SNMP, pro které jste zadali název komunity. Každé zařízení SNMP může mít svůj vlastní název komunity, ale často je stejný název komunity sdílený mezi několika zařízeními. Kromě toho většina zařízení SNMP má výchozí název komunity **veřejné**. Ale některé organizace odstraňují název **veřejné** komunity ze svých zařízení jako bezpečnostní opatření.  

Pokud zahrnete více komunit SNMP na kartě **SNMP** v dialogovém okně **Vlastnosti zjišťování sítě** , vyhledá je v pořadí, ve kterém jsou zobrazené. Ujistěte se, že se nejčastěji používané názvy nacházejí v horní části seznamu. Tato konfigurace pomáhá minimalizovat síťový provoz, který lokalita generuje při pokusu o kontaktování zařízení pomocí různých názvů.

> [!NOTE]  
> Společně s použitím názvu komunity SNMP můžete zadat IP adresu nebo název překladu konkrétního zařízení SNMP. Tuto akci provedete na kartě **zařízení SNMP** v dialogovém okně **Vlastnosti zjišťování sítě** .  

#### <a name="search-a-specific-dhcp-server"></a><a name="BKMK_SearchByDHCP"></a>Prohledat konkrétní server DHCP  

Funkci zjišťování sítě můžete nakonfigurovat tak, aby při spuštění zjišťování používala konkrétní server DHCP nebo víc serverů pro zjišťování klientů DHCP.  

Zjišťování sítě vyhledává každý server DHCP, který zadáte, na kartě **DHCP** v dialogovém okně **Vlastnosti zjišťování sítě** . Pokud server, na kterém je spuštěno zjišťování, zapůjčení jeho IP adresy ze serveru DHCP, můžete nakonfigurovat zjišťování pro hledání tohoto serveru DHCP. Toto chování povolte s možností **Zahrnout server DHCP, na který je server lokality nakonfigurován, aby jej bylo možné použít**.  

> [!NOTE]  
> Aby bylo možné úspěšně nakonfigurovat server DHCP při zjišťování sítě, musí vaše prostředí podporovat protokol IPv4. Funkci zjišťování sítě nelze nakonfigurovat tak, aby používala server DHCP v nativním prostředí IPv6.  

### <a name="how-to-configure-network-discovery"></a><a name="BKMK_HowToConfigNetDisc"></a>Postup konfigurace zjišťování sítě  

Následující postupy použijte k prvnímu zjištění pouze síťové topologie a potom ke konfiguraci zjišťování sítě pro zjištění potenciálních klientů pomocí jedné nebo více dostupných možností zjišťování sítě.  

#### <a name="how-to-determine-your-network-topology"></a><a name="bkmk_proc-top"></a>Jak zjistit topologii sítě  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace hierarchie**a vyberte uzel **metody zjišťování** .  

2. Vyberte metodu **zjišťování sítě** pro lokalitu, u které chcete zjistit síťové prostředky.  

3. Na kartě **Domů** na pásu karet vyberte možnost **vlastnosti**.  

    - Na kartě **Obecné** vyberte možnost **Povolit zjišťování sítě**. Pak vyberte možnost **topologie** z **typu možností zjišťování** .  

    - Na kartě **podsítě** vyberte možnost **Hledat místní podsítě** .  

      > [!TIP]  
      > Pokud znáte konkrétní podsítě, které tvoří vaši síť, zrušte zaškrtnutí políčka **prohledávat místní podsítě** . Pak vyberte ikonu **Nová** ikona ![nová](media/Disc_new_Icon.gif)a přidejte konkrétní podsítě, které chcete vyhledat. V případě rozsáhlých sítí můžete v jednom okamžiku vyhledávat pouze jednu nebo dvě podsítě, abyste minimalizovali využití šířky pásma sítě.  

    - Na kartě **domény** vyberte možnost **hledání v místní doméně**.  

    - Na kartě **SNMP** vyberte možnost z rozevíracího seznamu **maximální počet směrování** . Tato možnost určuje, kolik sítí směrování směrovačů může v rámci mapování topologie trvat.  

      > [!TIP]  
      > Při prvním mapování síťové topologie nakonfigurujte jenom několik směrování směrovače, aby se minimalizovalo používání šířky pásma sítě.  

4. Na kartě **plán** vyberte ikonu **Nová** ikona ![nové](media/Disc_new_Icon.gif)a nastavte plán pro spuštění zjišťování.  

    > [!NOTE]  
    > Nemůžete přiřadit jinou konfiguraci zjišťování pro samostatné plány zjišťování sítě. Pokaždé, když se zjišťování sítě spustí, použije se aktuální konfigurace zjišťování.  

5. Vyberte **OK** , aby se konfigurace přijímala. Zjišťování sítě běží v naplánovaném čase.  

#### <a name="how-to-configure-network-discovery"></a><a name="bkmk_proc-config"></a>Postup konfigurace zjišťování sítě  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace hierarchie**a vyberte uzel **metody zjišťování** .  

2. Vyberte metodu **zjišťování sítě** pro lokalitu, u které chcete zjistit síťové prostředky.  

3. Na kartě **Domů** na pásu karet vyberte možnost **vlastnosti**.  

4. Na kartě **Obecné** vyberte možnost **Povolit zjišťování sítě**.  

    - Vyberte z **typu možností zjišťování** typ zjišťování, který chcete spustit.  

    - Povolením možnosti **pomalé sítě** pro Configuration Manager provádět automatické úpravy pro sítě s malou šířkou pásma.  

5. Chcete-li nakonfigurovat zjišťování pro prohledávání podsítí, přepněte na kartu **podsítě** . Pak nakonfigurujte jednu nebo více z následujících možností:  

    - Pokud chcete spustit zjišťování v podsítích, které jsou místní pro počítač, na kterém se spouští zjišťování, povolte možnost **Hledat v místních podsítích**.  

    - Pokud chcete vyhledat konkrétní podsíť, ujistěte se, že je podsíť uvedená v části **podsítě k hledání** a jestli má **povolenou**hodnotu **hledání** :  

      1. Pokud není podsíť uvedená, ![ **vyberte novou ikonu** nová ikona](media/Disc_new_Icon.gif). V dialogovém okně **nové přiřazení podsítě** zadejte informace o **podsíti** a **masce** a pak vyberte **OK**. Ve výchozím nastavení je pro vyhledávání povolena nová podsíť.  

      2. Chcete-li změnit hodnotu **hledání** v uvedené podsíti, vyberte ji v seznamu. Pak vyberte ikonu **přepínání** , aby se přepnula hodnota mezi **zakázaným** a **povoleným**.  

6. Chcete-li nakonfigurovat zjišťování pro hledání domén, přepněte na kartu **domény** . Pak nakonfigurujte jednu nebo více z následujících možností:  

    - Chcete-li spustit funkci zjišťování v doméně počítače, ve kterém je zjišťování spuštěno, povolte možnost **hledání místní domény**.  

    - Pokud chcete vyhledat konkrétní doménu, ujistěte se, že je doména uvedená v části **domény** a že má **povolenou**hodnotu **hledání** :  

      1. Pokud není doména uvedená, vyberte ikonu **Nová** ![ikona](media/Disc_new_Icon.gif). V dialogovém okně **vlastnosti domény** zadejte informace o **doméně** a pak vyberte **OK**. Ve výchozím nastavení je pro prohledávání povolena nová doména.  

      2. Chcete-li změnit hodnotu **hledání** v uvedené doméně, vyberte ji v seznamu. Pak vyberte ikonu **přepínání** , aby se přepnula hodnota mezi **zakázaným** a **povoleným**.  

7. Chcete-li nakonfigurovat zjišťování pro hledání konkrétních názvů komunit SNMP pro zařízení SNMP, přepněte na kartu **SNMP** . Pak nakonfigurujte jednu nebo více z následujících možností:  

    - Chcete-li přidat název komunity SNMP do seznamu **názvů komunity SNMP**, vyberte ikonu **Nová** ikona ![nové](media/Disc_new_Icon.gif). V dialogovém okně **nový název komunity SNMP** zadejte **název** komunity SNMP a pak vyberte **OK**.  

    - Pokud chcete odebrat název komunity SNMP, vyberte název komunity a pak ![vyberte ikonu](media/Disc_delete_Icon.gif) **Odstranit ikona odstranit** .  

    - Pokud chcete upravit pořadí hledání názvů komunit SNMP, vyberte ze seznamu název komunity. Pak vyberte ikonu přesunout **položku nahoru** ikona ![](media/Disc_moveUp_Icon.gif) přesunout nahoru nebo ikonu ![](media/Disc_moveDown_Icon.gif) **přesunout položku dolů** ikona přesunout dolů. Při spuštění zjišťování se názvy komunit prohledávají v pořadí shora dolů. 

    - Chcete-li nakonfigurovat maximální počet směrování směrovače pro použití vyhledáváním SNMP, vyberte počet směrování z rozevíracího seznamu **maximální počet směrování** .  

8. Chcete-li nakonfigurovat zařízení SNMP, přepněte na kartu **zařízení SNMP** . Pokud zařízení není uvedené, vyberte ikonu **Nová** ikona ![nový](media/Disc_new_Icon.gif). V dialogovém okně **nové zařízení SNMP** zadejte IP adresu nebo název zařízení SNMP a pak vyberte **OK**.  

    > [!NOTE]  
    > Pokud zadáte název zařízení, Configuration Manager musí být schopný přeložit název pro rozhraní NetBIOS na IP adresu.  

9. Chcete-li nakonfigurovat zjišťování pro dotazování na konkrétní servery DHCP, přepněte na kartu **DHCP** . Pak nakonfigurujte jednu nebo více z následujících možností:  

    - Chcete-li zadat dotaz na server DHCP v počítači, na kterém je spuštěno zjišťování, povolte možnost **vždy použít server DHCP serveru lokality**.  

      > [!NOTE]  
      > Chcete-li použít tuto možnost, server musí zapůjčovat svou IP adresu ze serveru DHCP a nemůže používat statickou IP adresu.  

    - Pokud chcete zadat dotaz na konkrétní server DHCP, **New** vyberte ikonu ![nová ikona](media/Disc_new_Icon.gif)nový. V dialogovém okně **Nový server DHCP** Určete IP adresu nebo název serveru DHCP a pak vyberte **OK**.  

      > [!NOTE]  
      > Pokud zadáte název serveru, Configuration Manager musí být schopný přeložit název pro rozhraní NetBIOS na IP adresu.  

10. Pokud chcete nakonfigurovat, kdy se má zjišťování spustit, přepněte na kartu **plán** . Pak vyberte **novou** ikonu Nová ![ikona](media/Disc_new_Icon.gif) a nastavte plán pro spuštění zjišťování sítě. Můžete nakonfigurovat více opakovaných plánů a vícenásobné plány bez opakování.  

    > [!NOTE]  
    > Pokud karta **plán** zobrazuje více než jeden plán současně, bude zjišťování sítě spuštěno pro všechny plány, jak jsou nakonfigurovány v době uvedené v plánu. Toto chování platí také pro opakující se plány.  

11. Kliknutím na **OK** uložte své konfigurace.  

### <a name="how-to-verify-that-network-discovery-has-finished"></a><a name="BKMK_HowToVerifyNetDisc"></a>Jak ověřit, že se dokončilo zjišťování sítě  

Čas, kdy se zjišťování sítě potřebuje dokončit, se může lišit v závislosti na jednom nebo několika následujících faktorech:  

- Velikost vaší sítě  

- Topologie vaší sítě  

- Maximální počet směrování, které jsou nakonfigurované pro hledání směrovačů v síti  

- Typ zjišťování, který se spouští  

Funkce zjišťování sítě nevytváří zprávy upozorňující na jejich dokončení. K ověření, kdy bylo zjišťování dokončeno, použijte následující postup:  

1. V konzole Configuration Manager přejdete do pracovního prostoru **monitorování** . Rozbalte položku **stav systému**a pak vyberte uzel **dotazy stavových zpráv** .  

2. Vyberte dotaz **všechny stavové zprávy** .  

3. Na kartě **Domů** na pásu karet ve skupině **dotazy stavových zpráv** vyberte **Zobrazit zprávy**.  

4. V okně všechny stavové zprávy vyberte hodnotu z rozevíracího seznamu **vybrat datum a čas** , který obsahuje informace o tom, jak dlouho proběhlo zjišťování. Pak vyberte **OK** a otevřete tak **Configuration Manager Prohlížeč stavových zpráv**.  

    > [!TIP]  
    > Můžete také použít možnost **zadat datum a čas** a vybrat konkrétní datum a čas, kdy jste zjišťování spustili. Tato možnost je užitečná, když jste spustili zjišťování sítě v daném datu a chcete načíst zprávy pouze z daného data.  

5. Chcete-li ověřit, zda bylo zjišťování sítě dokončeno, vyhledejte stavovou zprávu s následujícími podrobnostmi:  

    - ID zprávy: **502**  

    - Součást: **SMS_NETWORK_DISCOVERY**  

    - Popis: **Tato součást byla zastavena** .  

    Pokud tato stavová zpráva není k dispozici, zjišťování sítě nebylo dokončeno.  

6. Chcete-li ověřit, zda bylo zjišťování sítě spuštěno, vyhledejte stavovou zprávu s následujícími podrobnostmi:  

    - ID zprávy: **500**  

    - Součást: **SMS_NETWORK_DISCOVERY**  

    - Popis: **Tato součást je spuštěná** .  

    Tato informace ověřuje, zda bylo zjišťování sítě spuštěno. Pokud tyto informace nejsou k dispozici, proveďte znovu plánování zjišťování sítě.  
