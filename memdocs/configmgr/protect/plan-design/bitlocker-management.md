---
title: Plánování správy nástroje BitLocker
titleSuffix: Configuration Manager
description: Plánování správy nástroj BitLocker Drive Encryption s využitím Configuration Manager
ms.date: 09/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a4d8cda2-bc9b-4fb4-aa0d-23c31b4fc60b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 193189e0e949aefdff15630476a306c1dc4ef2c7
ms.sourcegitcommit: cba06c182646cb6dceef304b35230bf728d5133e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/15/2020
ms.locfileid: "90574527"
---
# <a name="plan-for-bitlocker-management"></a>Plánování správy nástroje BitLocker

*Platí pro: Configuration Manager (Current Branch)*

<!-- 3601034 -->

Počínaje verzí 1910 použijte Configuration Manager ke správě nástroj BitLocker Drive Encryption (BDE) pro místní klienty Windows, které jsou připojené ke službě Active Directory. Poskytuje úplnou správu životního cyklu BitLockeru, která může nahradit použití nástroje Microsoft BitLocker Administration and Monitoring (MBAM).

> [!NOTE]
> Configuration Manager ve výchozím nastavení nepovolí tuto volitelnou funkci. Tuto funkci musíte před použitím povolit. Další informace naleznete v části [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).  

Obecnější informace o nástroji BitLocker najdete v tématu [Přehled nástroje BitLocker](/windows/security/information-protection/bitlocker/bitlocker-overview).

> [!TIP]
> Pokud chcete spravovat šifrování na zařízeních s Windows 10 spravovaných pomocí cloudové služby Microsoft Endpoint Manager, přepněte [ **Endpoint Protection** úlohy](../../comanage/workloads.md#endpoint-protection) do Intune. Další informace o používání Intune najdete v tématu [šifrování Windows](/intune/protect/endpoint-protection-windows-10#windows-encryption).

## <a name="features"></a>Funkce

Configuration Manager poskytuje následující možnosti správy pro nástroj BitLocker Drive Encryption:

### <a name="client-deployment"></a>Nasazení klienta

Nasazení klienta nástroje BitLocker do spravovaných zařízení s Windows s Windows 10 nebo Windows 8.1

### <a name="manage-encryption-policies"></a>Správa zásad šifrování

- Příklad: vyberte šifrování jednotky a sílu šifry, nakonfigurujte zásady pro výjimky uživatelů, nastavení šifrování pevné datové jednotky.

- Určete algoritmy, které zašifrují zařízení, a disky, na které zacílíte šifrování.

- Vynutí uživatele, aby před použitím tohoto zařízení dodržovali nové zásady zabezpečení.

- Přizpůsobte si profil zabezpečení vaší organizace na základě jednotlivých zařízení.

- Když uživatel odemkne jednotku operačního systému, určete, jestli se má odemknout jenom disk s operačním systémem nebo všechny připojené jednotky.

### <a name="compliance-reports"></a>Sestavy dodržování předpisů

Předdefinované sestavy pro:

- Stav šifrování na jeden svazek nebo na jedno zařízení
- Primární uživatel zařízení
- Stav dodržování předpisů
- Důvody pro nedodržování předpisů

### <a name="administration-and-monitoring-website"></a>Web pro správu a monitorování

Umožněte jiným osoby ve vaší organizaci mimo konzolu Configuration Manager, abyste mohli pomáhat s obnovením klíčů, včetně rotace klíčů a další podpory související s BitLockerem. Správci helpdesku můžou například uživatelům pomáhat s obnovením klíče.

### <a name="user-self-service-portal"></a>Samoobslužný portál uživatele

Umožněte uživatelům využít klíč s jedním klíčem k odemknutí zařízení zašifrovaného nástrojem BitLocker. Po použití tohoto klíče se pro zařízení vygeneruje nový klíč.

## <a name="prerequisites"></a>Požadavky

- Klienti v pracovní skupině nebo klienti v nedůvěryhodných doménách nejsou podporováni Azure Active Directoryi. Klient aktuálně musí být připojený k místní službě Active Directory. Tato konfigurace se ověřuje pomocí služby obnovení, aby v úschově klíče.

- K vytvoření zásady správy BitLockeru potřebujete roli **úplného správce** v Configuration Manager.

- Služba obnovení BitLockeru vyžaduje, aby protokol HTTPS zašifroval obnovovací klíče v síti od klienta Configuration Manager do bodu správy. Existují dvě možnosti:

  - HTTPS – povolí web služby IIS v bodu správy, který je hostitelem služby obnovení. Tato možnost se vztahuje pouze na Configuration Manager verze 2002.<!-- 5925660 -->

  - Nakonfigurujte bod správy pro protokol HTTPS. Tato možnost se vztahuje na Configuration Manager verze 1910 nebo 2002.

  Další informace najdete v tématu [šifrování dat pro obnovení](../deploy-use/bitlocker/encrypt-recovery-data.md).

- I když se služba obnovení BitLockeru nainstaluje na bod správy, který používá repliku databáze, klienti nemůžou v úschově obnovovací klíče. Nástroj BitLocker pak jednotku nešifruje. Chcete-li použít službu Recovery Services, potřebujete alespoň jeden bod správy, který není v konfiguraci repliky. Zakažte službu obnovení nástroje BitLocker v jakémkoli bodu správy s replikou databáze.<!-- 7813149 -->

- Chcete-li použít sestavy správy nástroje BitLocker, nainstalujte roli systému lokality bodu služby Reporting Services. Další informace najdete v tématu [Konfigurace vytváření sestav](../../core/servers/manage/configuring-reporting.md).

    > [!NOTE]
    > Aby mohla **Sestava auditu obnovení** fungovat na webu pro správu a monitorování, použijte pouze bod služby Reporting Services v primární lokalitě.

- Chcete-li použít samoobslužný portál nebo web pro správu a monitorování, potřebujete Windows Server, na kterém je spuštěná Internetová informační služba. Můžete znovu použít Configuration Manager systém lokality nebo použít samostatný webový server, který má připojení k serveru databáze lokality. [Pro servery systému lokality použijte podporovanou verzi operačního systému](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md).

    > [!NOTE]
    > Nainstalujte jenom Samoobslužný portál a web pro správu a monitorování s primární databází lokality. V hierarchii nainstalujte tyto weby pro každou primární lokalitu.

- Na webovém serveru, který bude hostitelem samoobslužného portálu, nainstalujte [Microsoft ASP.NET MVC 4,0](/aspnet/mvc/mvc4) a .NET Framework 3,5 před vytvořením hvězdičky v procesu instalace. Další požadované role a funkce Windows serveru se nainstalují automaticky během procesu instalace na portálu.

- Uživatelský účet, který spouští instalační skript portálu, potřebuje práva **správce** systému SQL na serveru databáze lokality. Během procesu instalace skript nastaví práva role přihlášení, uživatel a databáze SQL pro účet počítače webového serveru. Tento uživatelský účet můžete odebrat z role sysadmin po dokončení instalace samoobslužného portálu a webu pro správu a monitorování.

- Správa BitLockeru není podporovaná na virtuálních počítačích (VM) ani na serveru operačních systémech. Z tohoto důvodu některé funkce nemusí fungovat podle očekávání na virtuálních počítačích nebo na serveru operačních systémech. Například u virtuálních počítačů Správa nástroje BitLocker nespustí šifrování na pevných discích virtuálních počítačů. Navíc se pevné jednotky ve virtuálních počítačích můžou zobrazovat jako kompatibilní, i když nejsou zašifrované.

> [!TIP]
> Krok pořadí úkolů **zapnout nástroj BitLocker** standardně zašifruje místo na disku *využité místo* . Správa nástroje BitLocker používá *Úplné šifrování disku* . Nakonfigurujte tento krok pořadí úkolů, aby se povolila možnost **používat úplné šifrování disku**. Další informace najdete v tématu [postup pořadí úkolů – povolení nástroje BitLocker](../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker).

## <a name="next-steps"></a>Další kroky

Před prvním nasazením zásad [šifrovat data obnovení](../deploy-use/bitlocker/encrypt-recovery-data.md) (volitelný požadavek)

[Nasazení klienta pro správu nástroje BitLocker](../deploy-use/bitlocker/deploy-management-agent.md)
