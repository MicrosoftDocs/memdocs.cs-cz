---
title: Cluster SQL Server
titleSuffix: Configuration Manager
description: Hostování Configuration Manager databáze lokality pomocí SQL Serverho clusteru
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 90e4c0dfd2b55ec5acf943cd591ba45c719a68ff
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607512"
---
# <a name="use-a-sql-server-cluster-for-the-site-database"></a>Použít cluster SQL Server pro databázi lokality

*Platí pro: Configuration Manager (Current Branch)*

Cluster s podporou převzetí služeb při selhání SQL Server můžete použít k hostování databáze Configuration Manager lokality. Cluster poskytuje podporu převzetí služeb při selhání a zvyšuje spolehlivost databáze lokality. Neposkytuje ale další výhody zpracování nebo vyrovnávání zatížení. Kromě toho cluster SQL Server s podporou převzetí služeb při selhání používá sdílené úložiště a představuje jediný bod selhání. Může dojít ke snížení výkonu, protože server lokality musí najít aktivní uzel SQL Server clusteru předtím, než se připojí k databázi lokality.  

> [!IMPORTANT]  
> Úspěšná instalace SQL Serverch clusterů spoléhá na dokumentaci a postupy uvedené v knihovně dokumentace SQL Server.  


Než nainstalujete Configuration Manager, připravte cluster SQL Server tak, aby podporoval Configuration Manager. Další informace najdete v tématu [Příprava clusterované instance SQL Server](#bkmk_prepare).

Během Configuration Manager instalace se modul Windows služba Stínová kopie svazku Writer nainstaluje do každého uzlu fyzického počítače clusteru systému Microsoft Windows Server. Tato služba podporuje úlohu údržby **Zálohovat server webu** .  

Po instalaci lokality Configuration Manager kontroluje změny v uzlu clusteru každou hodinu. Configuration Manager automaticky spravuje všechny nalezené změny, které mají vliv na instalaci komponenty. Například převzetí služeb při selhání uzlu nebo přidání nového uzlu do clusteru SQL Server.  



## <a name="supported-options"></a>Podporované možnosti

Pro SQL Server clustery s podporou převzetí služeb při selhání používané jako databáze lokality jsou podporovány následující možnosti:

- Cluster s jednou instancí  

- Konfigurace s víc instancemi  

- Víc aktivních uzlů  

- Pojmenované i výchozí instance  



## <a name="prerequisites"></a>Požadavky

Pamatujte na následující požadavky:  

- Databáze lokality musí být od serveru lokality vzdálená. Cluster nemůže obsahovat server systému lokality.  

    > [!Note]  
    > Počínaje verzí 1810 nebude proces instalace Configuration Manager nadále blokovat instalaci role serveru lokality do počítače s rolí systému Windows pro clustering s podporou převzetí služeb při selhání. Dříve se nám nepovedlo společně najít databázi lokality na serveru lokality. Díky této změně můžete vytvořit vysoce dostupnou lokalitu s menším počtem serverů pomocí clusteru SQL a serveru lokality v pasivním režimu. Další informace najdete v tématu [Možnosti vysoké dostupnosti](high-availability-options.md). <!--3607761, fka 1359132-->  

- Přidejte účet počítače serveru lokality do skupiny místní **Správci** každého serveru v clusteru.  

- Pro podporu ověřování protokolem Kerberos povolte komunikační protokol sítě **TCP/IP** pro síťové připojení každého uzlu SQL Server clusteru. Protokol **pojmenovaných kanálů** není povinný, ale dá se použít k řešení problémů s ověřováním protokolu Kerberos. Nastavení síťového protokolu se konfigurují v **SQL Server Configuration Manager**v části **SQL Server konfigurace sítě**.  

- Při použití SQL Serverho clusteru pro databázi lokality jsou k dispozici konkrétní požadavky na certifikáty. Další informace najdete v následujících článcích:
  - [Instalace certifikátu v konfiguraci clusteru s podporou převzetí služeb při selhání pro SQL Server](/sql/database-engine/configure-windows/manage-certificates#provision-failover-cluster-cert)
  - [Požadavky na certifikát PKI pro nástroj Configuration Manager](../../../plan-design/network/pki-certificate-requirements.md#BKMK_PKIcertificates_for_servers)

  > [!NOTE]
  > Pokud certifikát v SQL nechcete předem zřídit, Configuration Manager vytvoří a zřídí certifikát podepsaný svým držitelem pro SQL.<!-- 7099499 -->

## <a name="limitations"></a>Omezení

Vezměte v úvahu následující omezení:  


### <a name="installation-and-configuration"></a>Instalace a konfigurace

- Sekundární lokality nemůžou používat cluster SQL Server.  

- Když zadáte cluster SQL Server, možnost určit jiné než výchozí umístění souborů pro databázi lokality není k dispozici.  


### <a name="sms-provider"></a>poskytovatele serveru SMS

Nemůžete nainstalovat instanci poskytovatele služby SMS na cluster SQL Server. Také se nepodporuje na počítači, který běží jako clusterovaný SQL Server uzel.  


### <a name="data-replication-options"></a>Možnosti replikace dat

Pokud používáte **distribuovaná zobrazení**, nemůžete použít cluster SQL Server k hostování databáze lokality.  


### <a name="backup-and-recovery"></a>Backup a obnovení

Configuration Manager nepodporuje zálohování Data Protection Manager (DPM) pro SQL Server cluster, který používá pojmenovanou instanci. Podporuje zálohování DPM na SQL Serverm clusteru, který používá výchozí instanci SQL Server.  



## <a name="prepare-a-clustered-sql-server-instance"></a><a name="bkmk_prepare"></a> Příprava clusterované instance SQL Server  

Tady jsou hlavní úlohy, které je potřeba dokončit pro přípravu databáze lokality:

- Vytvořte virtuální cluster SQL Serveru pro hostování databáze lokality ve stávajícím prostředí clusteru Windows Serveru. Konkrétní kroky pro instalaci a nastavení clusteru SQL Server naleznete v dokumentaci týkající se vaší verze SQL Server. Další informace najdete v tématu [Vytvoření nového clusteru s podporou převzetí služeb při selhání SQL Server](/sql/sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup).  

- Na každém počítači v clusteru SQL Server umístěte soubor do kořenové složky každé jednotky, kde nechcete, aby Configuration Manager instalovat součásti lokality. Pojmenujte soubor `NO_SMS_ON_DRIVE.SMS`. Ve výchozím nastavení Configuration Manager nainstaluje některé součásti na každý fyzický uzel, aby bylo možné podporovat operace, jako je zálohování.  

- Přidejte účet počítače serveru lokality do skupiny místní **Správci** každého počítače uzlu clusteru se systémem Windows Server.  

- V instanci Virtual SQL Server přiřaďte roli **sysadmin** SQL Server k uživatelskému účtu, který spouští Configuration Manager instalace.  


### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>Instalace nové lokality pomocí clusterovaného SQL Serveru  

Chcete-li nainstalovat lokalitu, která používá clusterovanou databázi lokality, spusťte Configuration Manager nastavení po běžném procesu pro instalaci lokality s následující změnou:  

- Na stránce **Informace o databázi** zadejte název virtuální instance clusteru SQL Serveru, která bude hostovat databázi lokality. Virtuální instance nahradí název počítače, na kterém běží SQL Server.  

    > [!IMPORTANT]  
    > Když zadáte název instance virtuálního SQL Server clusteru, nezadávejte název virtuálního Windows serveru vytvořeného clusterem Windows serveru. Pokud použijete název virtuálního Windows serveru, databáze lokality se nainstaluje na místní pevný disk aktivního uzlu clusteru Windows serveru. To znemožňuje úspěšné převzetí služeb při selhání v případě, že tento uzel selže.