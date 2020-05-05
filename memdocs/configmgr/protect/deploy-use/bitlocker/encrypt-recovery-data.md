---
title: Šifrování dat pro obnovení
titleSuffix: Configuration Manager
description: Šifrujte klíče pro obnovení BitLockeru, balíčky pro obnovení a hodnoty hash hesel TPM napříč sítí a v databázi Configuration Manager.
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 1ee6541a-e243-43ea-be16-d0349f7f0c6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79f50cf4b0d241df2fc8d12dc46c833af278bd5a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724437"
---
# <a name="encrypt-recovery-data"></a>Šifrování dat pro obnovení

*Platí pro: Configuration Manager (Current Branch)*

<!--3601034-->

Při vytváření zásad správy BitLockeru Configuration Manager nasadí službu obnovení do bodu správy. Pokud **nakonfigurujete služby správy nástroje BitLocker**na stránce **Správa klienta** v zásadách správy nástroje BitLocker, klient zálohuje informace o obnovení klíčů do databáze lokality. Tyto informace zahrnují klíče pro obnovení nástroje BitLocker, balíčky pro obnovení a hodnoty hash hesel TPM. Když jsou uživatelé uzamčeni z chráněného zařízení, můžete tyto informace využít k tomu, aby jim usnadnili obnovení přístupu k zařízení.

S ohledem na citlivou povahu těchto informací je nutné chránit je v následujících situacích:

- Configuration Manager vyžaduje připojení HTTPS mezi klientem a službou obnovení k šifrování dat při přenosu přes síť. Existují dvě možnosti:

  - HTTPS – povolí web IIS v bodu správy, který hostuje službu obnovení, a ne celou roli bodu správy. Tato možnost se vztahuje pouze na Configuration Manager verze 2002.<!-- 5925660 -->

  - Nakonfigurujte bod správy pro protokol HTTPS. Ve vlastnostech bodu správy musí být nastavení **připojení klientů** **https**. Tato možnost se vztahuje na Configuration Manager verze 1910 nebo 2002.

    > [!NOTE]
    > V současné době nepodporuje rozšířené požadavky HTTP.

- Zvažte také šifrování těchto dat při ukládání do databáze lokality. Můžete použít SQL Server šifrování na úrovni buněk s vlastním certifikátem.

    Pokud nechcete vytvořit šifrovací certifikát pro správu BitLockeru, přihlaste se k ukládání dat pro obnovení do prostého textu. Když vytváříte zásadu správy BitLockeru, povolte možnost **Povolit ukládání informací pro obnovení do prostého textu**.

    > [!NOTE]
    > Další vrstvou zabezpečení je šifrování celé databáze lokality. Pokud povolíte šifrování v databázi, neexistují žádné funkční problémy v Configuration Manager.
    >
    > Zašifrujte s opatrností, zejména ve velkých prostředích. V závislosti na vámi šifrovaných tabulkách a verzi SQL můžete všimnout až 25% snížení výkonu. Aktualizujte své plány zálohování a obnovení, abyste mohli úspěšně obnovit šifrovaná data.

## <a name="certificate-requirements"></a>Požadavky na certifikáty

### <a name="https-server-authentication-certificate"></a>Ověřovací certifikát serveru HTTPS

<!--5925660-->

V Configuration Manager aktuální větve verze 1910 pro integraci služby obnovení nástroje BitLocker, kterou jste měli v rámci protokolu HTTPS – povolte bod správy. Připojení HTTPS je nezbytné k šifrování obnovovacích klíčů v síti od klienta Configuration Manager do bodu správy. Konfigurace bodu správy a všech klientů pro protokol HTTPS může být pro mnoho zákazníků náročné.

Počínaje verzí 2002 je požadavek HTTPS určen pro web IIS, který je hostitelem služby obnovení, nikoli celou roli bodu správy. Tato změna zmírnit požadavky na certifikát a stále zašifruje obnovovací klíče při přenosu.

Nyní může být vlastnost **připojení klienta** bodu správy **http** nebo **https**. Pokud je bod správy nakonfigurován pro **protokol HTTP**, aby podporoval službu obnovení nástroje BitLocker:

1. Získejte certifikát ověřování serveru. Připojte certifikát k webu služby IIS v bodu správy, který je hostitelem služby obnovení nástroje BitLocker.

2. Nakonfigurujte, aby klienti důvěřovali ověřovacímu certifikátu serveru. Existují dvě metody, jak tento vztah důvěryhodnosti provést:

    - Použijte certifikát od poskytovatele veřejného a globálně důvěryhodného certifikátu. Například mimo jiné, DigiCert, Thawte nebo VeriSign. Mezi tyto poskytovatele patří mezi klienty Windows důvěryhodné kořenové certifikační autority (CA). Pomocí ověřovacího certifikátu serveru, který je vydaný jedním z těchto poskytovatelů, by se klienti měli automaticky důvěřovat.

    - Použijte certifikát vydaný certifikační autoritou z infrastruktury veřejných klíčů vaší organizace. Většina implementací infrastruktury veřejných klíčů přidávají klientům Windows důvěryhodné kořenové certifikační autority. Například používání služby Active Directory Certificate Services se zásadami skupiny. Pokud vydáte certifikát pro ověření serveru od certifikační autority, které vaši klienti automaticky nedůvěřují, přidejte do klientů důvěryhodný kořenový certifikát certifikační autority.

> [!TIP]
> Pouze klienti, kteří potřebují komunikovat se službou Recovery Services, jsou klienti, u kterých chcete cílit na zásadu správy nástroje BitLocker a které obsahují pravidlo **správy klienta** .

Na straně klienta použijte k řešení potíží s tímto připojením **protokol BitLockerManagementHandler. log** . V případě připojení ke službě Recovery Services se v protokolu zobrazuje adresa URL, kterou klient používá. Vyhledejte položku, která začíná na `Checking for Recovery Service at`.

> [!NOTE]
> Pokud má lokalita více než jeden bod správy, povolte protokol HTTPS u všech bodů správy v lokalitě, pomocí kterých může klient spravovaný pomocí nástroje BitLocker potenciálně komunikovat. Pokud bod správy HTTPS není k dispozici, může klient převzít služby při selhání do bodu správy protokolu HTTP a pak selže v úschově obnovovacího klíče.
>
> Toto doporučení platí pro obě možnosti: Povolte bod správy pro protokol HTTPS nebo povolte web IIS, který je hostitelem služby obnovení v bodu správy.

### <a name="sql-encryption-certificate"></a>Certifikát pro šifrování SQL

Tento certifikát použijte k povolení SQL Server šifrování na úrovni buněk pro data obnovení nástroje BitLocker. Pomocí vlastního procesu můžete vytvořit a nasadit šifrovací certifikát pro správu nástroje BitLocker, pokud splňuje následující požadavky:

- Název šifrovacího certifikátu správy BitLockeru musí být `BitLockerManagement_CERT`.

- Zašifrujte tento certifikát pomocí hlavního klíče databáze.

- Následující uživatelé SQL potřebují pro certifikát oprávnění k **řízení** :
  - RecoveryAndHardwareCore
  - RecoveryAndHardwareRead
  - RecoveryAndHardwareWrite

- Nasaďte stejný certifikát do každé databáze lokality ve vaší hierarchii.

- Vytvořte certifikát s nejnovější verzí SQL Server ve vašem prostředí. Příklad:
  - Certifikáty vytvořené pomocí SQL Server 2016 nebo novější jsou kompatibilní s SQL Server 2014 nebo starším.
  - Certifikáty vytvořené pomocí SQL Server 2014 nebo starší nejsou kompatibilní s SQL Server 2016 nebo novějším.

## <a name="example-scripts"></a>Ukázkové skripty

Tyto skripty SQL jsou příklady pro vytvoření a nasazení šifrovacího certifikátu správy BitLockeru v databázi lokality Configuration Manager.

### <a name="create-certificate"></a>Vytvořit certifikát

Tento ukázkový skript provádí následující akce:

- Vytvoří certifikát.
- Nastaví oprávnění.
- Vytvoří hlavní klíč databáze.

Než použijete tento skript v produkčním prostředí, změňte následující hodnoty:

- Název databáze webu (`CM_ABC`)
- Heslo pro vytvoření hlavního klíče (`MyMasterKeyPassword`)
- Datum vypršení platnosti certifikátu`20391022`()

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN
    CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
    WITH SUBJECT = 'BitLocker Management',
    EXPIRY_DATE = '20391022'

    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="back-up-certificate"></a>Zálohovat certifikát

Tento ukázkový skript zálohuje certifikát. Když certifikát uložíte do souboru, můžete ho [obnovit](#restore-certificate) do jiných databází lokality v hierarchii.

Než použijete tento skript v produkčním prostředí, změňte následující hodnoty:

- Název databáze webu (`CM_ABC`)
- Cesta k souboru a název`C:\BitLockerManagement_CERT_KEY`()
- Exportovat heslo klíče (`MyExportKeyPassword`)

``` SQL
USE CM_ABC
BACKUP CERTIFICATE BitLockerManagement_CERT TO FILE = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        ENCRYPTION BY PASSWORD = 'MyExportKeyPassword')
```

> [!IMPORTANT]
> Exportovaný soubor certifikátu a přidružené heslo uložte do zabezpečeného umístění.

### <a name="restore-certificate"></a>Obnovit certifikát

Tento ukázkový skript obnoví certifikát ze souboru. Tento postup použijte k nasazení certifikátu, který jste vytvořili v jiné databázi lokality.

Než použijete tento skript v produkčním prostředí, změňte následující hodnoty:

- Název databáze webu (`CM_ABC`)
- Heslo hlavního klíče (`MyMasterKeyPassword`)
- Cesta k souboru a název`C:\BitLockerManagement_CERT_KEY`()
- Exportovat heslo klíče (`MyExportKeyPassword`)

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN

CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
FROM FILE  = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        DECRYPTION BY PASSWORD = 'MyExportKeyPassword')

GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="verify-certificate"></a>Ověřit certifikát

Pomocí tohoto skriptu SQL ověřte, zda SQL úspěšně vytvořil certifikát s požadovanými oprávněními.

``` SQL
USE CM_ABC
declare @count int
select @count = count(distinct u.name) from sys.database_principals u
join sys.database_permissions p on p.grantee_principal_id = u.principal_id or p.grantor_principal_id = u.principal_id
join sys.certificates c on c.certificate_id = p.major_id
where u.name in('RecoveryAndHardwareCore', 'RecoveryAndHardwareRead', 'RecoveryAndHardwareWrite') and
c.name = 'BitLockerManagement_CERT' and p.permission_name like 'CONTROL'
if(@count >= 3) select 1
else select 0
```

Pokud je certifikát platný, skript vrátí hodnotu `1`.

## <a name="see-also"></a>Viz také

Další informace o těchto příkazech SQL najdete v následujících článcích:

- [SQL Server a šifrovací klíče databáze](https://docs.microsoft.com/sql/relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine)
- [Vytvořit certifikát](https://docs.microsoft.com/sql/t-sql/statements/create-certificate-transact-sql)
- [Záložní certifikát](https://docs.microsoft.com/sql/t-sql/statements/backup-certificate-transact-sql)
- [Vytvořit hlavní klíč](https://docs.microsoft.com/sql/t-sql/statements/create-master-key-transact-sql)
- [Záložní hlavní klíč](https://docs.microsoft.com/sql/t-sql/statements/backup-master-key-transact-sql)
- [Udělení oprávnění k certifikátu](https://docs.microsoft.com/sql/t-sql/statements/grant-certificate-permissions-transact-sql)
