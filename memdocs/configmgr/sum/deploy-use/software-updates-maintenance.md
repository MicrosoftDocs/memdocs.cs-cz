---
title: Údržba aktualizací softwaru
titleSuffix: Configuration Manager
description: Pokud chcete zachovat aktualizace v Configuration Manager, můžete naplánovat úlohu čištění služby WSUS, nebo ji můžete spustit ručně.
author: mestew
ms.date: 12/17/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 560b432bb90f99207fd15bc07e7aff98ffd59ebf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719782"
---
# <a name="software-updates-maintenance"></a>Údržba aktualizací softwaru

*Platí pro: Configuration Manager (Current Branch)*

Úlohy čištění služby WSUS můžete naplánovat a spustit z konzoly Configuration Manager ve vlastnostech komponenty bodu aktualizace softwaru. Když nejprve vyberete, že se má spustit úloha čištění služby WSUS, bude spuštěna po další synchronizaci aktualizací softwaru.  

## <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>Postup plánování a spuštění úlohy čištění služby WSUS

Naplánujte úlohu čištění služby WSUS spuštěním následujících kroků:

1. V konzole Configuration Manager přejděte do části **Správa** > **Přehled** > **Konfigurace** > **lokality lokality.**
2. Vyberte lokalitu v horní části vaší Configuration Manager hierarchie.

3. Ve skupině **Nastavení** klikněte na **Konfigurovat součásti pracoviště** a potom kliknutím na **Bod aktualizace softwaru** otevřete vlastnosti součásti bodu softwarové aktualizace.  

4. Zkontrolujte **chování nahrazování**. V případě potřeby upravte chování.

   ![snímek obrazovky chování nahrazování](media/supersedence-behavior.png)

5. Klikněte na kartu **pravidla nahrazení** , vyberte **Spustit Průvodce vyčištěním služby WSUS**. Ve verzi 1806 je možnost přejmenována na **spuštění služby WSUS Cleanup po synchronizaci**.

6. Klikněte na **OK** (Pokud používáte verzi 1806), klikněte na **Zavřít** .

## <a name="wsus-cleanup-behavior-in-version-1802-and-earlier"></a>Chování vyčištění služby WSUS ve verzi 1802 a starší

Před Configuration Manager verzí 1806 spustí možnost vyčištění služby WSUS následující položku:

- Možnost **aktualizace s vypršenou platností** z Průvodce vyčištěním služby WSUS je pouze na serveru služby WSUS v lokalitě nejvyšší úrovně.

  ![Snímek obrazovky pro vyčištění aktualizace služby WSUS vypršel](media/wsus-cleanup-expired.PNG)

- Vyčištění položek konfigurace aktualizace softwaru v Configuration Manager databáze probíhá každých 7 dní a z konzoly nástroje odebere nepotřebné aktualizace.
  - Tento proces vyčištění nebude odebírat aktualizace s vypršenou platností z konzoly Configuration Manager, pokud jsou aktuálně nasazeny.

V databázi WSUS nejvyšší úrovně a všech ostatních databázích služby WSUS v prostředí je stále potřeba další údržba. Další informace a pokyny najdete v článku [kompletní příručka k údržbě Microsoft WSUS a Configuration Manager SUP](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) v příspěvku na blogu.

## <a name="wsus-cleanup-behavior-starting-in-version-1806"></a>Chování vyčištění služby WSUS počínaje verzí 1806

Počínaje verzí 1806 se k možnosti vyčištění služby WSUS dochází po každé synchronizaci a následující položky čištění:
<!--1357898 -->

- Možnost **aktualizace s vypršenou platností** pro servery WSUS v certifikačních autoritách a primárních lokalitách.
  - Servery WSUS pro sekundární lokality nespouštějí službu WSUS Cleanup pro aktualizace s vypršenou platností.
- Configuration Manager vytvoří ze své databáze seznam nahrazených aktualizací. Seznam je založen na chování nahrazení ve vlastnostech komponenty bodu aktualizace softwaru.
  - V konzole Configuration Manager vypršela platnost položek konfigurace aktualizace, které splňují kritéria pro chování nahrazování.
  - Aktualizace jsou odmítnuty ve službě WSUS pro certifikační autority a primární lokality, ale ne pro sekundární lokality.
- Vyčištění položek konfigurace aktualizace softwaru v Configuration Manager databáze probíhá každých 7 dní a z konzoly nástroje odebere nepotřebné aktualizace.
  - Tento proces vyčištění nebude odebírat aktualizace s vypršenou platností z konzoly Configuration Manager, pokud jsou aktuálně nasazeny.

> [!NOTE]
> "Měsíce, které se mají počkat před uplynutím nahrazené aktualizace", vycházejí z datum vytvoření nahrazující aktualizace. Pokud například použijete pro toto nastavení 2 měsíce, budou aktualizace, které byly nahrazeny, odmítnuty ve službě WSUS a jejichž platnost vypršela, Configuration Manager, když je aktualizace převádějící na 2 měsíce stará.

Veškerá údržba služby WSUS je nutné spustit ručně na databázích služby WSUS sekundární lokality. Následující možnosti **Průvodce vyčištěním serveru WSUS** nejsou spuštěny v CERTIFIKAČNÍch autoritách a primárních lokalitách:

- Nepoužívané aktualizace a revize aktualizací
- Počítače, které nekontaktují Server
- Nepotřebné soubory aktualizace

  Další informace a pokyny najdete v článku [kompletní příručka k údržbě Microsoft WSUS a Configuration Manager SUP](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) v příspěvku na blogu.

## <a name="wsus-cleanup-behavior-starting-in-version-1810"></a>Chování vyčištění služby WSUS počínaje verzí 1810

Počínaje verzí 1810 můžete zadat pravidla nahrazení pro aktualizace funkcí odděleně od aktualizací bez funkcí ve vlastnostech komponenty bodu aktualizace softwaru. Možnost vyčištění služby WSUS probíhá po každé synchronizaci a provede následující položky vyčištění:
<!--2839349,3098809, 2977644-->

- Možnost **aktualizace s vypršenou platností** pro servery WSUS v certifikačních autoritách, primárních a sekundárních lokalitách.
- Configuration Manager vytvoří ze své databáze seznam nahrazených aktualizací. Seznam je založen na chování nahrazení ve vlastnostech komponenty bodu aktualizace softwaru.
  - V konzole Configuration Manager vypršela platnost položek konfigurace aktualizace, které splňují kritéria pro chování nahrazování.
  - Aktualizace jsou odmítnuty ve službě WSUS pro certifikační autority, primární a sekundární lokality.
- Vyčištění položek konfigurace aktualizace softwaru v Configuration Manager databáze probíhá každých 7 dní a z konzoly nástroje odebere nepotřebné aktualizace.
  - Tento proces vyčištění nebude odebírat aktualizace s vypršenou platností z konzoly Configuration Manager, pokud jsou aktuálně nasazeny.

> [!NOTE]
> "Měsíce, které se mají počkat před uplynutím nahrazené aktualizace", vycházejí z datum vytvoření nahrazující aktualizace. Pokud například použijete pro toto nastavení 2 měsíce, budou aktualizace, které byly nahrazeny, odmítnuty ve službě WSUS a jejichž platnost vypršela, Configuration Manager, když je aktualizace převádějící na 2 měsíce stará.

Následující možnosti **Průvodce vyčištěním serveru WSUS** nejsou spuštěny na serverech CA, primárních a sekundárních lokalitách:

- Nepoužívané aktualizace a revize aktualizací
- Počítače, které nekontaktují Server
- Nepotřebné soubory aktualizace

  Další informace a pokyny najdete v článku [kompletní příručka k údržbě Microsoft WSUS a Configuration Manager SUP](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) v příspěvku na blogu.

## <a name="wsus-cleanup-starting-in-version-1906"></a>Vyčištění služby WSUS počínaje verzí 1906
<!--41101009-->

 Máte další úlohy údržby služby WSUS, které mohou Configuration Manager spustit za účelem zachování zdravých bodů aktualizace softwaru. Kromě odmítnutí aktualizací s vypršenou platností ve službě WSUS může Configuration Manager přidat neclusterované indexy do databází WSUS a odebrat zastaralé aktualizace z databází služby WSUS. Údržba služby WSUS probíhá po každé synchronizaci.

### <a name="decline-expired-updates-in-wsus-according-to-supersedence-rules"></a>Odmítnout aktualizace s vypršenou platností ve službě WSUS podle pravidel nahrazení

Klesající aktualizace ve službě WSUS zvyšují výkon odebráním těchto aktualizací z katalogů odesílaných klientům. Odmítnutí aktualizací, které Configuration Manager označuje jako nahrazené, dále minimalizuje katalogy a zlepší výkon.

1. V konzole Configuration Manager přejděte do části **Správa** > **Přehled** > **Konfigurace** > **lokality lokality.**
2. Vyberte lokalitu v horní části vaší Configuration Manager hierarchie.
3. Ve skupině **Nastavení** klikněte na Konfigurovat součásti pracoviště a potom kliknutím na **Bod aktualizace softwaru** otevřete vlastnosti součásti bodu softwarové aktualizace.
4. Na kartě **Údržba služby WSUS** vyberte v **závislosti na pravidlech nahrazení možnost odmítnout aktualizace s vypršenou platností ve službě WSUS**.

### <a name="add-non-clustered-indexes-to-the-wsus-database-to-improve-wsus-cleanup-performance"></a>Přidání neclusterovaných indexů do databáze WSUS za účelem zlepšení výkonu služby WSUS pro vyčištění

Přidání neclusterovaných indexů zvyšuje výkon vyčištění služby WSUS, který Configuration Manager.

1. V konzole Configuration Manager přejděte do části **Správa** > **Přehled** > **Konfigurace** > **lokality lokality.**
2. Vyberte lokalitu v horní části vaší Configuration Manager hierarchie.
3. Ve skupině **Nastavení** klikněte na Konfigurovat součásti pracoviště a potom kliknutím na **Bod aktualizace softwaru** otevřete vlastnosti součásti bodu softwarové aktualizace.
4. Na kartě **Údržba služby WSUS** vyberte **Přidat neseskupené indexy do databáze WSUS**.
5. V každém SUSDB, který používá Configuration Manager, se indexy přidávají do následujících tabulek:
   - tbLocalizedPropertyForRevision
   - tbRevisionSupersedesUpdate

#### <a name="sql-permissions-for-creating-indexes"></a>Oprávnění SQL pro vytváření indexů

Pokud je databáze WSUS na vzdáleném SQL serveru, možná budete muset přidat oprávnění v SQL a vytvořit indexy. Účet použitý pro připojení k databázi WSUS a vytváření indexů se může lišit. Pokud [ve vlastnostech bodu aktualizace softwaru zadáte účet pro připojení k serveru WSUS](../get-started/install-a-software-update-point.md#wsus-server-connection-account), ujistěte se, že účet pro připojení má oprávnění SQL. Pokud nezadáte účet pro připojení k serveru WSUS, účet počítače serveru lokality potřebuje oprávnění SQL.

- Vytvoření indexu vyžaduje `ALTER` oprávnění pro tabulku nebo zobrazení. Účet musí být členem `sysadmin` pevné role serveru nebo s `db_ddladmin` `db_owner` pevnými databázovými rolemi. Další informace o vytváření a indexování a oprávněních najdete v tématu [Create index (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-index-transact-sql?view=sql-server-2017#permissions).
- Účtu `CONNECT SQL` musí být uděleno oprávnění serveru. Další informace najdete v tématu [udělení oprávnění serveru (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql?view=sql-server-2017).

> [!NOTE]  
>  Pokud je databáze služby WSUS na vzdáleném serveru SQL Server pomocí jiného než výchozího portu, indexy pravděpodobně nebudou přidány. Pro tento scénář můžete vytvořit [alias serveru pomocí SQL Server Configuration Manager](https://docs.microsoft.com/sql/database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client?view=sql-server-2017) . Po přidání aliasu a Configuration Manager může vytvořit připojení k databázi WSUS, budou přidány indexy.

### <a name="remove-obsolete-updates-from-the-wsus-database"></a>Odebrat zastaralé aktualizace z databáze WSUS

Zastaralé aktualizace jsou nepoužívané aktualizace a revize aktualizací v databázi WSUS. Obecně řečeno, aktualizace se považuje za zastaralou, jakmile už není v [katalogu Microsoft Update](https://www.catalog.update.microsoft.com/) a nevyžaduje jiné aktualizace jako součást nebo závislost.

1. V konzole Configuration Manager přejděte do části **Správa** > **Přehled** > **Konfigurace** > **lokality lokality.**
2. Vyberte lokalitu v horní části vaší Configuration Manager hierarchie.
3. Ve skupině **Nastavení** klikněte na Konfigurovat součásti pracoviště a potom kliknutím na **Bod aktualizace softwaru** otevřete vlastnosti součásti bodu softwarové aktualizace.
4. Na kartě **Údržba služby WSUS** vyberte možnost **Odebrat zastaralé aktualizace z databáze WSUS**.
   - Zastaralá odebrání aktualizace bude povoleno spouštět po dobu maximálně 30 minut, než bude zastavena. Spustí se znovu, až se objeví další synchronizace.  

#### <a name="sql-permissions-for-removing-obsolete-updates"></a>Oprávnění SQL pro odebrání zastaralých aktualizací

Pokud je databáze WSUS na vzdáleném SQL serveru, účet počítače serveru lokality potřebuje následující oprávnění SQL:

- Pevné `db_datareader` databázové `db_datawriter` role a. Další informace najdete v tématu [role na úrovni databáze](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles?view=sql-server-2017#fixed-database-roles).
- Oprávnění `CONNECT SQL` serveru musí být uděleno účtu počítače webového serveru. Další informace najdete v tématu [udělení oprávnění serveru (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql?view=sql-server-2017).

#### <a name="wsus-cleanup-wizard"></a>Průvodce vyčištěním služby WSUS

Počínaje verzí 1906 se následující možnosti **Průvodce vyčištěním serveru WSUS** nespouštějí v CERTIFIKAČNÍch autoritách, primárních a sekundárních lokalitách:

- Počítače, které nekontaktují Server
- Nepotřebné soubory aktualizace

  Další informace a pokyny najdete v článku [kompletní příručka k údržbě Microsoft WSUS a Configuration Manager SUP](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) v příspěvku na blogu.


### <a name="known-issues-for-version-1906"></a>Známé problémy verze 1906

Představte si následující scénář:
<!--5418148-->
- Používáte Configuration Manager verze 1906
- Máte vzdálené body aktualizace softwaru pomocí interní databáze Windows.
- Ve **vlastnostech komponenty bodu aktualizace softwaru**máte k dispozici některou z následujících možností na kartě **Údržba služby WSUS** :
   - Přidání neclusterovaných indexů do databáze WSUS
   - Odebrat zastaralé aktualizace z databáze WSUS

V tomto scénáři Configuration Manager není možné provést výše uvedené úlohy údržby služby WSUS pro body aktualizací vzdáleného softwaru pomocí interní databáze Windows. K tomuto problému dochází, protože interní databáze Windows neumožňuje vzdálená připojení. Na serveru lokality se `WSyncMgr.log` zobrazí následující chyby:

```text
Indexing Failed. Could not connect to SUSDB.
SqlException thrown while connect to SUSDB in Server: <SUP.CONTOSO.COM>. Error Message: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server)
...
Could not Delete Obselete Updates because ConfigManager could not connect to SUSDB: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server) UpdateServer: <SUP.CONTOSO.COM>
```

Pokud chcete tento problém obejít, můžete automatizaci údržby služby WSUS pro body vzdálené aktualizace softwaru automatizovat pomocí interní databáze Windows. Další informace a podrobné pokyny najdete [v kompletní příručce k údržbě Microsoft WSUS a Configuration Manager SUP](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint).

## <a name="updates-cleanup-log-entries"></a>Aktualizuje položky protokolu vyčištění.

Toto vyčištění můžete ověřit kontrolou protokolu souboru wsyncmgr. log pro následující položky:

- Po zobrazení této položky protokolu dojde k odmítnutí nahrazených aktualizací ve službě WSUS:`Cleanup processed <number> total updates and declined <number>`
- Po zobrazení této položky se spustí vyčištění služby WSUS:`Calling WSUS Cleanup.`
- Po zobrazení této položky se dokončí vyčištění služby WSUS pro aktualizace s vypršenou platností:`Successfully completed WSUS Cleanup.`
- Po zobrazení této položky se spustí vyčištění Configuration Manager položky konfigurace s vypršenou platností:`Deleting old expired updates...`
- Po zobrazení této položky se dokončí vyčištění položek konfigurace Configuration Manager vypršela platnost.`Deleted <number> expired updates total`
