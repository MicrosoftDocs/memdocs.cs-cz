---
title: Rozšiřování a migrace místního serveru na Microsoft Azure
titleSuffix: Configuration Manager
description: Přečtěte si, jak pomocí nástroje pro migraci programově vytvořit virtuální počítače Azure pro Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1c975c5e-efd1-4d47-a315-39ccb32633dc
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4d5f0c9127cc5c5819368eb0454d7bc63546ccc1
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699496"
---
# <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>Rozšiřování a migrace místního serveru na Microsoft Azure

*Platí pro: Configuration Manager (Current Branch)*


Tento nástroj, který je představený ve verzi 1910, vám pomůže programově vytvářet virtuální počítače Azure pro Configuration Manager. <!--3556022--> Může se nainstalovat s výchozími nastaveními role lokality, jako je pasivní server lokality, body správy a distribuční body. Jakmile ověříte nové role, použijte je jako další systémy lokality pro zajištění vysoké dostupnosti. Můžete také odebrat roli místního systému lokality a zachovat jenom roli virtuálních počítačů Azure.

## <a name="prerequisites"></a>Předpoklady

- Předplatné Azure

- Virtuální síť Azure s bránou ExpressRoute

<!-- - A standalone primary site. A hierarchy with a central administration site isn't currently supported. can comment this out because TP only supports a standalone primary!-->

- Váš uživatelský účet musí být Configuration Manager **úplný správce** a mít práva správce na primárním serveru lokality.

- Chcete-li přidat pasivní server, musí primární lokalita splňovat [požadavky na vysokou dostupnost serveru lokality](../servers/deploy/configure/site-server-high-availability.md#prerequisites). Například vyžaduje [knihovnu vzdáleného obsahu](../plan-design/hierarchy/the-content-library.md#bkmk_remote).

### <a name="required-azure-permissions"></a>Vyžadovaná oprávnění Azure

Při spuštění nástroje budete potřebovat následující oprávnění v Azure:
<!--5789222-->
Microsoft. Resources/Subscriptions/resourceGroups/Read <br>
Microsoft. Resources/Subscriptions/resourceGroups/Write <br>
Microsoft. Resources/nasazení/čtení <br>
Microsoft. Resources/nasazení/zápis <br>
Microsoft. Resources/nasazení/ověření/akce <br>
Microsoft. COMPUTE/virtualMachines/Extensions/Read <br>
Microsoft. COMPUTE/virtualMachines/Extensions/Write <br>
Microsoft. COMPUTE/virtualMachines/Read <br>
Microsoft. COMPUTE/virtualMachines/Write <br>
Microsoft. Network/virtualNetworks/Read <br>
Microsoft. Network/virtualNetworks/podsítí/čtení <br>
Microsoft. Network/virtualNetworks/subnets/JOIN/Action <br>
Microsoft. Network/networkInterfaces/Read <br>
Microsoft. Network/networkInterfaces/Write <br>
Microsoft. Network/networkInterfaces/JOIN/Action <br>
Microsoft. Network/networkSecurityGroups/Write <br>
Microsoft. Network/networkSecurityGroups/Read <br>
Microsoft. Network/networkSecurityGroups/JOIN/Action <br>
Microsoft. Storage/storageAccounts/Write <br>
Microsoft. Storage/storageAccounts/Read <br>
Microsoft. Storage/storageAccounts/klíče listkey/Action <br>
Microsoft. Storage/storageAccounts/listServiceSas/Action <br>
Microsoft. Storage/storageAccounts/blobServices/Containers/Write <br>
Microsoft. Storage/storageAccounts/blobServices/Containers/Read <br>
Trezor Microsoft. a trezory/nasazení/akce <br>
Trezor Microsoft. a trezory/čtení <br>


Další informace o oprávněních a přiřazování rolích najdete v tématu [Správa přístupu k prostředkům Azure pomocí RBAC](/azure/role-based-access-control/role-assignments-portal).

## <a name="run-the-tool"></a>Spusťte nástroj.

1. Přihlaste se k serveru primární lokality a spusťte následující nástroj v instalačním adresáři Configuration Manager: `Cd.Latest\SMSSETUP\TOOLS\ExtendMigrateToAzure\ExtendMigrateToAzure.exe`

1. Zkontrolujte informace na kartě **Obecné** a pak přejděte na kartu **informace o Azure** .

1. Na kartě  **informace o Azure** zvolte **prostředí Azure**a pak se **přihlaste**.

    > [!TIP]
    > Možná budete muset přidat `https://*.microsoft.com` do seznamu důvěryhodných webů pro správné přihlášení.

    [![Karta informace o Azure v nástroji pro rozšiřování a migraci](./media/3556022-azure-information-tab.png)](./media/3556022-azure-information-tab.png#lightbox)

1. Po přihlášení vyberte své **ID předplatného** a **virtuální síť**. Nástroj uvádí jenom sítě s bránou ExpressRoute.

## <a name="site-server-high-availability"></a>Vysoká dostupnost serveru lokality

1. Na kartě **Vysoká dostupnost serveru lokality** zaškrtněte políčko **zaškrtněte** , pokud chcete vyhodnotit připravenost svého webu.

    Pokud některá z kontrol selže, vyberte **Další podrobnosti** , abyste zjistili, jak problém vyřešit. Další informace o těchto požadavcích najdete v tématu [Vysoká dostupnost serveru lokality](../servers/deploy/configure/site-server-high-availability.md#prerequisites).

2. Pokud chcete server lokality rozšíříte nebo migrujete do Azure, vyberte **vytvořit server lokality v Azure**. Pak vyplňte následující pole:

    |Název|Popis|
    |---|---|
    |**Předplatné**|Jen pro čtení. Zobrazuje název a ID předplatného.|
    |**Skupina prostředků**| Zobrazí seznam dostupných skupin prostředků. Pokud potřebujete vytvořit novou skupinu prostředků, použijte [Azure Portal](https://portal.azure.com)a pak tento nástroj znovu spusťte.|
    |**Umístění**| Jen pro čtení. Určeno umístěním vaší virtuální sítě|
    |**Velikost virtuálního počítače**|Vyberte velikost, která se přizpůsobí vašim úlohám. Společnost Microsoft doporučuje **Standard_DS3_v2**.|
    |**Operační systém**|Jen pro čtení. Nástroj používá systém Windows Server 2019.|
    |**Typ disku**|Jen pro čtení. Nástroj používá SSD úrovně Premium k dosažení nejlepšího výkonu.|
    |**Virtuální síť**|Jen pro čtení.|
    |**Podsíť**|Vyberte podsíť, která se má použít. Pokud potřebujete vytvořit novou podsíť, použijte [Azure Portal](https://portal.azure.com).|
    |**Název počítače**|Zadejte název virtuálního počítače pasivního serveru webu v Azure. Je to stejný název, který se zobrazuje v [Azure Portal](https://portal.azure.com).|
    |**Uživatelské jméno místního správce**|Zadejte jméno místního administrativního uživatele, který virtuální počítač Azure vytvoří, než se připojí k doméně.|
    |**Heslo místního správce**|Heslo místního administrativního uživatele. Pokud chcete chránit heslo během nasazování Azure, uložte heslo jako tajný kód v [Azure Key Vault](/azure/key-vault/key-vault-overview). Pak použijte odkaz zde. V případě potřeby vytvořte nový z [Azure Portal](https://portal.azure.com).|
    |**Plně kvalifikovaný název domény**|Plně kvalifikovaný název domény, ke které se má připojit doména služby Active Directory Ve výchozím nastavení nástroj získá tuto hodnotu z vašeho aktuálního počítače.|
    |**Uživatelské jméno domény**|Jméno uživatele domény s povoleným připojením k doméně Nástroj ve výchozím nastavení používá název aktuálně přihlášeného uživatele.|
    |**Heslo domény**|Heslo uživatele domény, který se má připojit k doméně Nástroj ji ověří po výběru možností **Start**. Pokud chcete chránit heslo během nasazování Azure, uložte heslo jako tajný kód v [Azure Key Vault](/azure/key-vault/key-vault-overview). Pak použijte odkaz zde. V případě potřeby vytvořte nový z [Azure Portal](https://portal.azure.com).|
    |**IP adresa DNS domény**|Slouží k připojení k doméně. Nástroj ve výchozím nastavení používá aktuální službu DNS z vašeho aktuálního počítače.|
    |**Typ**|Jen pro čtení. Jako typ se zobrazí *pasivní server lokality* .|

    > [!IMPORTANT]
    > Ve výchozím nastavení jsou virtuální počítače nastavené na hodnotu **ne** pro **použití existující licence na Windows Server**. Pokud chcete využívat své místní licence k Windows serveru se Software Assurance, nakonfigurujte toto nastavení v [Azure Portal](https://portal.azure.com) po zřízení virtuálních počítačů. Další informace najdete v tématu [zvýhodněné hybridní využití Azure pro Windows Server](/windows-server/get-started/azure-hybrid-benefit).

1. Pokud chcete začít zřídit virtuální počítač Azure, vyberte **Spustit**. Pokud chcete monitorovat stav nasazení, přejděte v nástroji na kartu **nasazení na portálu Azure** . Chcete-li získat nejnovější stav, vyberte možnost **aktualizovat stav nasazení**.

    > [!TIP]
    > Můžete také použít [Azure Portal](https://portal.azure.com) ke kontrole stavu, hledání chyb a určení možných oprav.

1. Až se nasazení dokončí, přejdete na SQL servery a udělíte oprávnění k novému virtuálnímu počítači Azure. Další informace najdete v tématu [Vysoká dostupnost serveru lokality – předpoklady](../servers/deploy/configure/site-server-high-availability.md#prerequisites).

1. Pokud chcete přidat virtuální počítač Azure jako server lokality v pasivním režimu, vyberte **Přidat server lokality v pasivním režimu**.

1. Jakmile lokalita přidá server lokality v pasivním režimu, karta **Vysoká dostupnost serveru lokality** zobrazí stav.

   [![Pasivní server lokality přidaný na kartu vysoká dostupnost serveru lokality](./media/3556022-site-server-passive-mode.png)](./media/3556022-site-server-passive-mode.png#lightbox)

1. Pak na kartě nasazení na webu [Azure](#bkmk_deploy-azure) dokončete nasazení.

## <a name="site-database"></a>Databáze lokality

Tento nástroj aktuálně nemá žádné úlohy pro migraci databáze z místního prostředí do Azure. Můžete zvolit přesun databáze z místního SQL serveru do virtuálního počítače Azure SQL Server. Tento nástroj obsahuje následující články na kartě **databáze lokality** , které vám pomůžou:

- [Zálohování a obnovení databáze](../servers/manage/backup-and-recovery.md)
- [Nakonfigurujte SQL Always On a Umožněte replikaci dat.](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup)
- [Migrace databáze SQL do virtuálního počítače Azure SQL Server](/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)

## <a name="site-system-roles"></a>Role systému lokality

1. Přepněte na kartu **role systému lokality** . Pokud chcete zřídit novou roli systému lokality s výchozími nastaveními, vyberte **vytvořit novou**. Můžete zřídit role, jako je bod správy, distribuční bod a bod aktualizace softwaru. Ne všechny role jsou aktuálně k dispozici v nástroji.

    [![Karta role systému lokality v nástroji Extended and migruje](./media/3556022-site-system-roles-tab.png)](./media/3556022-site-system-roles-tab.png#lightbox)

1. V okně zřizování vyplňte pole a zřiďte virtuální počítač role webu v Azure. Tyto podrobnosti se podobají výše uvedenému seznamu pro server lokality.

1. Pokud chcete začít zřídit virtuální počítač Azure, vyberte **Spustit**. Pokud chcete monitorovat stav nasazení, přejděte v nástroji na kartu **nasazení na portálu Azure** . Chcete-li získat nejnovější stav, vyberte možnost **aktualizovat stav nasazení**.

    > [!TIP]
    > Můžete také použít [Azure Portal](https://portal.azure.com) ke kontrole stavu, hledání chyb a určení možných oprav.

1. Opakujte tento postup pro přidání dalších rolí systému lokality.

1. Pak na kartě nasazení na webu [Azure](#bkmk_deploy-azure) dokončete nasazení.

1. Po dokončení nasazení přejdete do konzoly Configuration Manager, abyste provedli další změny role lokality.

## <a name="deployments-in-azure"></a><a name="bkmk_deploy-azure"></a> Nasazení v Azure

1. Jakmile Azure vytvoří virtuální počítač, přejděte v nástroji na kartu **nasazení na portálu Azure** . Vyberte **nasadit** a nakonfigurujte roli s výchozím nastavením.

1. Výběrem **Spustit** spusťte powershellový skript.

    [![Nasazení rolí lokality spuštěním generovaného skriptu PowerShellu](./media/3556022-run-powershell-script-deployment.png)](./media/3556022-run-powershell-script-deployment.png#lightbox)

1. Opakujte tento postup pro konfiguraci dalších rolí.

## <a name="add-site-roles-to-an-existing-virtual-machine-deployment"></a><a name="bkmk_add_role"></a> Přidání rolí webu do existujícího nasazení virtuálního počítače
<!--5665775, 6307931-->
Počínaje verzí 2002 Configuration Manager nástroj Extended and migruje on-premises web do Microsoft Azure Tool podporuje zřizování více rolí systému lokality na jednom virtuálním počítači Azure. Po dokončení počátečního nasazení virtuálního počítače Azure můžete přidat role systému lokality. Chcete-li přidat novou roli k existujícímu virtuálnímu počítači, proveďte následující kroky:
1. Na kartě **nasazení na platformě Azure** klikněte na nasazení virtuálního počítače, které má stav **dokončeno** .
1. Kliknutím na tlačítko **vytvořit nové** přidejte další roli k virtuálnímu počítači.


## <a name="next-steps"></a>Další kroky

Zkontrolujte změny v [Azure Portal](https://portal.azure.com)