---
title: 'Správa stavu uživatele '
titleSuffix: Configuration Manager
description: Configuration Manager používá Nástroj pro migraci uživatelských souborů a nastavení k zachycení a obnovení dat o stavu uživatele ve scénářích nasazení operačního systému.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d8d5c345-1e91-410b-b8a9-0170dcfa846e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 70c15fb3a108b22ffacad69d6a67bef3b2d29952
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724073"
---
# <a name="manage-user-state-in-configuration-manager"></a>Správa stavu uživatele v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pořadí úloh Configuration Manager můžete použít k zaznamenání a obnovení dat o stavu uživatele ve scénářích nasazení operačního systému, kde chcete zachovat stav uživatele v aktuálním operačním systému. Příklad:  

- Nasazení, při kterých chcete zaznamenat stav uživatele v jednom počítači a obnovit tento stav v jiném.  

- Aktualizujte nasazení, ve kterém chcete zachytit a obnovit stav uživatele na stejném počítači.  

Configuration Manager používá Nástroj pro migraci uživatelských souborů a nastavení (USMT) 10,0 ke správě migrace dat o stavu uživatele ze zdrojového počítače do cílového počítače po dokončení instalace operačního systému. Další informace o běžných scénářích migrace pomocí Nástroje pro migraci stavu uživatele (USMT) 10.0 najdete v tématu  [Běžné scénáře migrace](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios).

Následující části vám pomůžou zachytit a obnovit data uživatelů.

## <a name="store-user-state-data"></a><a name="BKMK_StoringUserData"></a>Uložení dat o stavu uživatele

 Při zaznamenání stavu stavu uživatele můžete uložit data stavu uživatele na cílový počítač nebo do bodu migrace stavu. Chcete-li uložit stav uživatele v bodě migrace stavu uživatele, je nutné použít Configuration Manager Server systému lokality, který je hostitelem role systému lokality bodu migrace stavu. Chcete-li uložit stav uživatele v cílovém počítači, je třeba nakonfigurovat pořadí úloh tak, aby pomocí odkazů uložilo data v místním počítači.

> [!NOTE]
> Odkazům, které slouží k místnímu uložení stavu uživatele, se říká pevné odkazy. Pevné odkazy jsou funkcí Nástroje pro migraci stavu uživatele (USMT) 10.0, která v počítači vyhledá uživatelské soubory a nastavení a potom vytvoří adresář pevných odkazů na tyto soubory. Po nasazení nového operačního systému slouží pevné odkazy k obnově dat uživatele.

> [!IMPORTANT]
> K uložení dat o stavu uživatele však nelze současně použít bod migrace stavu a pevné odkazy.

Jakmile je informace o stavu uživatele zaznamenána, může být uložena jedním z těchto způsobů:  

- Data o stavu uživatele můžete uložit vzdáleně nakonfigurováním bodu migrace stavu. Pořadí úkolů **zaznamenat** odešle data do bodu migrace stavu. Po nasazení operačního systému pořadí úloh **obnovit** data načte a obnoví stav uživatele v cílovém počítači.  

- Data o stavu uživatele můžete uložit místně v určené složce. V tomto scénáři pořadí úkolů **zaznamenat** zkopíruje data uživatele do určitého umístění v cílovém počítači. Po nasazení operačního systému pořadí úkolů **obnovit** načte uživatelská data z tohoto umístění.  

- Můžete zadat pevné odkazy, které budou sloužit k obnovení uživatelských dat do původního umístění. Při tomto scénáři zůstávají data o stavu uživatele při odebrání starého operačního systému na disku. Potom po nasazení nového operačního systému pořadí úkolů **Obnovit** na základě pevných odkazů obnoví data stavu uživatele v původním umístění.  

### <a name="store-user-data-on-a-state-migration-point"></a><a name="BKMK_UserDataSMP"></a>Uložení dat uživatele do bodu migrace stavu

 Pokud chcete uložit data stavu uživatele do bodu migrace stavu, postupujte takto:  

1. Podle postupu v kroku[Configure a state migration point](#BKMK_StateMigrationPoint) uložte data stavu uživatele.  

1. Podle postupu v kroku[Create a computer association](#BKMK_ComputerAssociation) vytvořte přidružení mezi zdrojovým a cílovým počítačem. Toto přiřazení musí být vytvořeno ještě před zaznamenáním stavu uživatele ve zdrojovém počítači.  

1. [Vytvořte pořadí úkolů pro zachycení a obnovení stavu uživatele](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). Konkrétně je potřeba přidat následující kroky pořadí úkolů pro zaznamenání dat uživatele z počítače, Uložit Datum uživatele do bodu migrace stavu a obnovit data uživatelů na počítač:  

    - [Request State Store](../understand/task-sequence-steps.md#BKMK_RequestStateStore) – pro vyžádání přístupu k bodu migrace stavu při zaznamenávání stavu z počítače nebo obnovování stavu v počítači.  

    - [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState) – pro zaznamenání a uložení dat stavu uživatele do bodu migrace stavu.  

    - [Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState) – pro obnovení stavu uživatele v cílovém počítači načtením dat z bodu migrace stavu uživatele.  

    - [Release State Store](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) – upozorní bod migrace stavu, že se akce zaznamenání nebo obnovení dokončila.  

### <a name="store-user-data-locally"></a><a name="BKMK_UserDataDestination"></a>Místní uložení dat uživatele

 Pokud chcete uložit data stavu uživatele místně, postupujte takto:  

- [Vytvořte pořadí úkolů pro zachycení a obnovení stavu uživatele](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). Konkrétně je potřeba přidat následující kroky pořadí úkolů pro zaznamenání dat uživatele z počítače a obnovení dat uživatelů do počítače pomocí pevných odkazů.

  - [Capture User State](../understand/task-sequence-steps.md#BKMK_CaptureUserState) – pro zaznamenání a uložení dat stavu uživatele do místní složky pomocí pevných odkazů.  

  - [Restore User State](../understand/task-sequence-steps.md#BKMK_RestoreUserState) – pro obnovení stavu uživatele na cílovém počítači načtením dat pomocí pevných odkazů.  

    > [!NOTE]
    > Data o stavu uživatele, na něž pevné odkazy odkazují, zůstávají v počítači i poté, co pořadí úloh odstraní starý operační systém. Jedná se o data sloužící k obnově stavu uživatele po nasazení nového operačního systému.  

## <a name="configure-a-state-migration-point"></a><a name="BKMK_StateMigrationPoint"></a>Konfigurace bodu migrace stavu

Bod migrace stavu uchovává data o stavu uživatele zaznamenaná v jednom počítači a následně obnovovaná v jiném počítači. Pokud ale zaznamenáváte uživatelské nastavení pro nasazení operačního systému na stejném počítači, třeba pro nasazení, při kterém obnovíte operační systém cílového počítače, můžete data uložit na stejný počítač (pomocí pevných odkazů) nebo do bodu migrace stavu. U některých nasazení počítačů se při vytváření úložiště stavů Configuration Manager automaticky vytvoří přidružení mezi úložištěm stavu a cílovým počítačem. Ke konfiguraci bodu migrace stavu k uložení dat o stavu uživatele můžete použít následující metody:  

- Použít **Průvodce Vytvořit server lokality** , pomocí nějž vytvoříte nový server lokality pro bod migrace stavu.  

- Použít **Průvodce Přidat role serveru** , pomocí nějž přidáte na existující server bod migrace stavu.  

  Při použití těchto průvodců budete vyzváni, abyste zadali následující informace o bodu migrace stavu:  

- Složky, do nichž budou uložena data o stavu uživatele.  

- Maximální počet klientů, kteří mohou ukládat data v bodě migrace stavu.  

- Minimální volné místo k ukládání dat o stavu uživatele v bodě migrace stavu.  

- Zásady smazání role. Můžete určit, zda mají být data o stavu uživatele smazána okamžitě po obnovení v počítači, nebo až po určitém počtu dní od obnovení uživatelských dat v počítači.  

- Jestli má bod migrace stavu reagovat jenom na požadavky na obnovení dat stavu uživatele. Pokud povolíte tuto možnost, nebude možné využívat bod migrace stavu k ukládání dat o stavu uživatele.  

  Další informace o bodu migrace stavu a pokyny k jeho konfiguraci najdete v tématu [State migration point](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

## <a name="create-a-computer-association"></a><a name="BKMK_ComputerAssociation"></a>Vytvořit přidružení počítače

Vytvořte přidružení počítačů, které určuje vztah mezi zdrojovým počítačem a cílovým počítačem při instalaci operačního systému na nový hardware, když chcete zaznamenat a obnovit nastavení dat uživatele. Zdrojový počítač je existující počítač, který Configuration Manager spravuje. Pokud nasazujete nový operační systém do cílového počítače, obsahuje zdrojový počítač stav uživatele, který je přenášen do cílového počítače.  

> [!NOTE]  
> Není podporováno vytváření přidružení počítače mezi počítači umístěnými v Configuration Manager nadřazené lokalitě s počítači umístěnými v podřízené lokalitě. Přidružení počítačů jsou specifická pro konkrétní lokality a nereplikují se.  

### <a name="to-create-a-computer-association"></a>Vytvoření přiřazení počítačů

1. V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.  

1. V pracovním prostoru **Prostředky a kompatibilita** klikněte na možnost **Migrace stavu uživatele**.  

1. Na kartě **Domů** ve skupině **Vytvořit** klikněte na možnost **Vytvořit přiřazení počítače**.  

1. Na kartě **Přidružení počítače** v dialogovém okně **Vlastnosti přidružení počítače** zadejte zdrojový počítač, z nějž má být zaznamenán stav uživatele, a cílový počítač, v němž mají být data o stavu uživatele obnovena.  

1. Na kartě **Uživatelské účty** zadejte uživatelské účty, které mají být přeneseny do cílového počítače. Nastavte následující možnosti:  

    - **Uchovejte a obnovte všechny uživatelské účty**: Toto nastavení zaznamená a obnoví všechny uživatelské účty. Pomocí tohoto nastavení lze vytvořit několik přiřazení k jednomu zdrojovému počítači.  

    - **Uchovejte všechny uživatelské účty a obnovte zadané účty**: Toto nastavení zaznamená všechny uživatelské účty ve zdrojovém počítači, ale v cílovém počítači obnoví pouze zadané účty. Toto nastavení lze navíc využít, pokud chcete vytvořit několik přiřazení pro jeden zdrojový počítač.  

    - **Uchovejte a obnovte zadané uživatelské účty**: Toto nastavení zaznamená a obnoví jenom zadané uživatelské účty. Při tomto nastavení nelze vytvořit více přiřazení k jednomu zdrojovému počítači.  

## <a name="restore-user-state-data-when-an-operating-system-deployment-fails"></a><a name="BKMK_MigrationFails"></a>Obnovení dat o stavu uživatele v případě, že dojde k chybě nasazení operačního systému

Pokud se nasazení operačního systému nezdaří, pomocí funkce LoadState Nástroje pro migraci stavu uživatele (USMT) 10.0 načtěte data stavu uživatele, která se zaznamenala v průběhu nasazení. Patří sem data uložená v bodu migrace stavu nebo data uložená lokálně na cílovém počítači. Další informace o této funkci USMT naleznete v části [LoadState Syntax](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax).
