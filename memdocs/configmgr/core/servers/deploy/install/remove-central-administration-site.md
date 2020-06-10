---
title: Odebrání certifikačních autorit
titleSuffix: Configuration Manager
description: Odeberte lokalitu centrální správy (CAS), aby se zjednodušila Configuration Manager infrastruktura pro jednu samostatnou primární lokalitu.
ms.date: 06/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 16975644-8dfa-4f22-b45a-c54a9250dbd2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 237c326c4420aec13ad6c9ca9b07d9f5304b6945
ms.sourcegitcommit: 52dd59bdbad07b414db9e4209da0f4c957cf5d6e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/09/2020
ms.locfileid: "84613977"
---
# <a name="remove-the-central-administration-site"></a>Odebrat lokalitu centrální správy

*Platí pro: Configuration Manager (Current Branch)*

<!-- 3607277 -->

Pokud se v rámci verze 2002 skládá hierarchie z lokality centrální správy (CAS) a jedné podřízené primární lokality, můžete certifikační autority odebrat. Tato akce zjednodušuje infrastrukturu Configuration Manager pro jednu samostatnou primární lokalitu. Odstraňuje složitosti replikace typu Site-to-site a zaměřuje úlohy správy na jednu lokalitu.

> [!IMPORTANT]
> V této verzi Configuration Manager je tato funkce předběžná a není povolená ve výchozím nastavení. Je aktuálně k dispozici pro zákazníky s Microsoft Premier.
>
> Pokud chcete tuto funkci povolit, požádejte o pomoc správce svého technického účtu.
>
> - TAM otevře poradní případ, který bude používat vaše hodiny na webu Microsoft Premier.
> - Nemůžete změnit závažnost případu.
> - Podpora Microsoftu pomůže těmto poradenským případům během normální pracovní doby v týdnu.

## <a name="plan"></a>Plánování

- Hierarchie musí obsahovat certifikační autority a jednu podřízenou primární lokalitu. Primární lokalita může obsahovat sekundární lokality. Pokud chcete z hierarchie odebrat další podřízené primární lokality, Projděte si kroky plánování a požadavky pro [odinstalaci primární lokality](uninstall-sites-and-hierarchies.md#bkmk_primary).

- Ujistěte se, že vaše podřízená primární lokalita splňuje požadavky na velikost a škálování pro [samostatnou primární lokalitu](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_pri).

- Přesuňte nebo vyřaďte role webu na CAS, s výjimkou spojovacího bodu služby a bodu aktualizace softwaru. Configuration Manager při odebírání certifikačních autorit zpracovává tyto dvě role.

  Následující role jsou nejběžnější v certifikačních autoritách, které je třeba vyřadit nebo přesunout do primární lokality:

  - funkce Asset Intelligence bod synchronizace
  - Bod ochrany koncového bodu Endpoint Protection
  - Bod služby Reporting services
  - Bod služby datového skladu
  - Brána pro správu cloudu (CMG)

    > [!NOTE]
    > Pokud jste povolili CMG pro obsah, naplánujte znovu distribuci obsahu po opětovném vytvoření CMG v primární lokalitě.<!-- 6608659 -->

- Vypnout distribuovaná zobrazení

- Configuration Manager automaticky zpracovává umístění zdrojů balíčku pro integrované balíčky, jako je například klient Configuration Manager. Zkontrolujte všechna ostatní umístění zdroje obsahu, abyste se ujistili, že nepoužívají sdílenou složku na certifikačních autoritách.

- Zastavte všechny aktivní úlohy migrace a odeberte všechny konfigurace pro migraci. Další informace najdete v tématu [zastavení aktivní migrace z jiné hierarchie](prerequisites-for-installing-sites.md#stop-active-migration-from-another-hierarchy).

- Pokud používáte pravidla automatického nasazení pro aktualizace softwaru, vytvořte je znovu v podřízené primární lokalitě.

- Pokud ke správě [aktualizací softwaru třetích stran](../../../../sum/deploy-use/third-party-software-updates.md)používáte Configuration Manager nebo System Center Updates Publisher, exportujte podpisový certifikát služby WSUS z bodu aktualizace softwaru na certifikačních autoritách.

  - Před odebráním certifikačních autorit počkejte na termíny všech požadovaných nasazení aktualizací softwaru třetích stran. Klienti před stažením obsahu pro požadovaná nasazení a při změně bodu aktualizace softwaru mění hodnotu hash obsahu pomocí *místního publikování* aktualizací softwaru. (Toto chování nemá vliv na jiné typy obsahu, pouze místní publikování aktualizací softwaru třetích stran.) Pokud odeberete certifikační autority s těmito požadovanými nasazeními, dojde k jejich selhání u klientů s chybou neshody hodnoty hash.

- Projděte si software jiného výrobce, který může mít závislost na certifikačních autoritách.

## <a name="prerequisites"></a>Požadavky

- Administrativní uživatel, který spouští Configuration Manager instalační program, potřebuje následující bezpečnostní oprávnění:

  - Práva místního **správce** na serveru CAS

  - Pokud je databázový server CAS vzdálený od serveru lokality, oprávnění místního **správce** k serveru databáze vzdálené lokality pro certifikační autority.

  - Oprávnění **sysadmin** v databázi lokality CAS

  - Oprávnění místního **správce** na serveru primární lokality

  - Pokud je server databáze primární lokality vzdálený od primárního serveru lokality, oprávnění místního **správce** k serveru databáze vzdálené lokality pro primární lokalitu.

  - Oprávnění **sysadmin** v databázi primární lokality

  - Role zabezpečení **správce infrastruktury** nebo správce s **úplnými oprávněními** na certifikačních autoritách a primárních lokalitách

- V hierarchii je pouze jedna podřízená primární lokalita. Další informace najdete v tématu [odinstalace primární lokality](uninstall-sites-and-hierarchies.md#bkmk_primary).

## <a name="process"></a>Proces

1. Spusťte instalaci Configuration Manager na serveru CAS pomocí jedné z následujících metod:

    - V nabídce **Start** vyberte **Configuration Manager nastavení**.

    - V adresáři pro *instalační médium*Configuration Manager otevřete `\SMSSETUP\BIN\X64\setup.exe` . Ujistěte se, že je tato verze stejná jako verze lokality.

    - V adresáři, ve kterém je *nainstalováno*Configuration Manager, otevřete `\BIN\X64\setup.exe` .

1. Přečtěte si informace na stránce **než začnete** .

1. Na stránce **Začínáme** vyberte možnost **provést údržbu lokality nebo resetovat tuto lokalitu**.

1. Na stránce **Údržba webového serveru** vyberte možnost **odebrat lokalitu centrální správy**. <!-- or is it still "delete"? -->

1. Na stránce **překonfigurování stávajících rolí systému lokality** :

    - **Bod připojení služby**: zadejte plně kvalifikovaný název domény systému lokality v primární lokalitě pro hostování této požadované role. Další informace najdete v tématu [o spojovacím bodu služby](../configure/about-the-service-connection-point.md).

    - **Bod aktualizace softwaru**: Vyberte existující bod aktualizace softwaru v primární lokalitě. Instalační program nakonfiguruje tento bod aktualizace softwaru, aby synchronizoval stejnou konfiguraci CAS.

    Instalační program zkontroluje, zda zadané servery splňují požadavky. Pokud budete připraveni pokračovat, vyberte **zahájit instalaci** .

Pokud dojde k problému s instalací, použijte průvodce a opakujte proces.

Po dokončení instalace obnoví primární lokalitu. Další informace najdete v tématu [spuštění resetování lokality](../../manage/modify-your-infrastructure.md#bkmk_reset).

## <a name="monitor-and-verify"></a>Monitorování a ověření

Během procesu instalace zkontrolujte tyto protokoly:

- `C:\ConfigMgrSetup.log`na serveru CAS

- **hman. log** v adresáři protokolu Configuration Manager v serveru primární lokality

K vizualizaci změn v hierarchii použijte uzel **hierarchie lokality** v pracovním prostoru **monitorování** . Například následující obrázek znázorňuje porovnání a po porovnání **nesmělí abyste** CAS, **Haw** primární lokality a sekundární lokality **VWT** :

| Před  | Po   |
|---------|---------|
|![Příklad zobrazení hierarchie lokality pro certifikační autority, primární lokalitu a sekundární lokalitu](media/3607277-cas-primary-secondary.png)|![Příklad zobrazení hierarchie lokality v primární lokalitě a sekundární lokalitě](media/3607277-primary-secondary.png)|

## <a name="post-setup-tasks"></a>Úkoly po instalaci

Po odebrání certifikačních autorit si Projděte následující kroky, které se vztahují na vaše prostředí.

- Ručně odeberte účet počítače serveru CAS z místní skupiny primární lokality.

- Důvěryhodný kořenový klíč se změnil, což může vyžadovat další akce:

  - Aktualizujte spouštěcí image nasazení operačního systému tak, aby obsahovaly nejnovější binární soubory Configuration Manager.

  - Znovu vytvořte [médium pro nasazení operačního systému](../../../../osd/deploy-use/create-task-sequence-media.md).

- Pokud připojíte Configuration Manager s [Azure monitor](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm?context=configmgr/core/context/core-context), musíte resetovat připojení. Prvním krokem při řešení potíží je [obnovení tajného klíče](../configure/azure-services-wizard.md#bkmk_renew). Pokud se tím problém nevyřeší, vytvořte připojení znovu.<!-- 5584635 -->

- Pokud v části verze 2002 povolíte synchronizaci ovladačů Surface, překonfigurujte tuto funkci po odebrání certifikačních autorit. Další informace najdete v tématu [ovladače Microsoft Surface a aktualizace firmwaru](../../../../sum/deploy-use/surface-drivers.md).<!-- 5728727 -->

- Pokud spravujete aktualizace softwaru třetích stran:

  1. Exportujte podpisový certifikát služby WSUS z bodu aktualizace softwaru na CAS (Pokud jste to ještě neudělali).

  1. Před vytvořením nových nasazení odeberte aktualizaci z existujících nasazení a balíčků aktualizací softwaru.

  1. Chcete-li obnovit metadata aktualizace softwaru do použitelného stavu, znovu synchronizujte odebírané katalogy. Můžete také počkat, až se Configuration Manager automaticky znovu synchronizuje.

  1. Spusťte nebo počkejte, až se běžný proces synchronizace aktualizace softwaru aktualizuje Configuration Manager s aktuálním stavem ze služby WSUS. Volitelně můžete použít rutiny prostředí PowerShell SCUP nebo WSUS k odstranění a čtení aktualizací.

  1. Znovu publikujte obsah pro aktualizace, které je třeba nasadit.
