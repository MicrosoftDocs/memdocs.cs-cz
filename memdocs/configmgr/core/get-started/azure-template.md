---
title: Vytvoření testovacího prostředí v Azure
titleSuffix: Configuration Manager
description: Automatizace vytváření testovacího prostředí pro Configuration Manager Technical Preview nebo laboratoře pro vyhodnocení aktuální větve pomocí šablon Azure
ms.date: 07/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9875c443-19bf-43a0-9203-3a741f305096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ea1965d6cae90808156957be1c9634e4c1631aa8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694521"
---
# <a name="create-a-configuration-manager-lab-in-azure"></a>Vytvoření testovacího prostředí Configuration Manager v Azure

*Platí pro: Configuration Manager (Current Branch, větev Technical Preview)*

<!--3556017-->

Tato příručka popisuje, jak vytvořit Configuration Manager testovací prostředí v Microsoft Azure. Používá šablony Azure ke zjednodušení a automatizaci vytváření testovacího prostředí s využitím prostředků Azure. K dispozici jsou dvě šablony Azure: 

- Šablona Azure Configuration Manager Technical Preview nainstaluje nejnovější verzi Configuration Manager Technical Preview.
- Configuration Manager Current Branch Azure Template nainstaluje vyhodnocení nejnovější verze Configuration Manager aktuální větve. 

Další informace najdete v tématu [Configuration Manager v Azure](../understand/configuration-manager-on-azure.md).



## <a name="prerequisites"></a>Předpoklady

Tento proces vyžaduje předplatné Azure, ve kterém můžete vytvořit následující objekty: 
- Dva Standard_B2s virtuální počítače pro řadič domény, bod správy a distribuční bod.
- Jeden Standard_B2ms virtuální počítač pro server primární lokality a server služby SQL Database.
- Účet úložiště Standard_LRS

> [!Tip]  
> V [cenové kalkulačkě Azure](https://azure.microsoft.com/pricing/calculator/)vám pomůže určit možné náklady.  



## <a name="process"></a>Proces

1. Přejít na [šablonu Configuration Manager Technical Preview](https://azure.microsoft.com/resources/templates/sccm-technicalpreview/) nebo na [šablonu Configuration Manager aktuální větev](https://azure.microsoft.com/resources/templates/sccm-currentbranch/).  

2. Vyberte **nasadit do Azure**, čímž otevřete Azure Portal.  

3. Dokončete šablonu Azure pro rychlý Start s následujícími informacemi:

    - Základy  

        - **Předplatné**: název předplatného, ve kterém se mají virtuální počítače vytvořit.  

        - **Skupina prostředků**: vyberte skupinu prostředků, která se má použít pro tyto virtuální počítače.  

        - **Umístění**: Vyberte datové centrum Azure pro hostování tohoto testovacího prostředí.  

    - Nastavení  

        - **Prefix**: Předpona názvu počítačů. Další informace najdete v tématu [informace o virtuálním počítači Azure](#azure-vm-info).  

        - **Uživatelské jméno správce**: jméno uživatele na virtuálních počítačích s právy správce. Pomocí tohoto uživatele se přihlásíte k virtuálním počítačům.  

        - **Heslo správce**: heslo musí splňovat požadavky na složitost Azure. Další informace najdete v tématu [adminPassword](/rest/api/compute/virtualmachines/createorupdate#osprofile).  

    > [!Important]  
    > Azure vyžaduje následující nastavení. Použijte výchozí hodnoty. Tyto hodnoty neměňte.  
    > 
    > - ** \_ umístění artefaktů**: umístění skriptů pro tuto šablonu <!-- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sccm-technicalpreview/ -->  
    >
    > - ** \_ artefakty umístění lokátoru SAS**: sasToken se vyžaduje pro přístup k umístění artefaktů.  
    > 
    > - **Umístění**: umístění všech prostředků

4. Přečtěte si podmínky a ujednání. Pokud souhlasíte, vyberte Souhlasím **s výše uvedenými podmínkami a ujednáními**. Pak pokračujte výběrem **koupit** . 

Azure ověří nastavení a pak zahájí nasazení. Ověřte stav nasazení ve Azure Portal. 

> [!NOTE]
> Proces může trvat 2-4 hodin. I když Azure Portal zobrazuje úspěšné nasazení, skripty konfigurace budou pořád běžet. Během procesu nerestartujte virtuální počítače.

Chcete-li zobrazit stav konfiguračních skriptů, připojte se k `<prefix>PS1` serveru a Prohlédněte si následující soubor: `%windir%\TEMP\ProvisionScript\PS1.json` . Pokud se zobrazí všechny kroky jako dokončené, proces se provede.

Pokud se chcete připojit k virtuálním počítačům, nejdřív si načtěte z Azure Portal veřejné IP adresy pro každý virtuální počítač. Když se připojíte k virtuálnímu počítači, název domény je `contoso.com` . Použijte přihlašovací údaje, které jste zadali v šabloně nasazení. Další informace najdete v tématu [jak se připojit a přihlásit se k virtuálnímu počítači Azure s Windows](/azure/virtual-machines/windows/connect-logon).



## <a name="azure-vm-info"></a>Informace o virtuálním počítači Azure

Všechny tři virtuální počítače mají následující specifikace:
- 150 GB místa na disku
- Jak veřejné, tak privátní IP adresa. Veřejné IP adresy jsou ve skupině zabezpečení sítě, která umožňuje připojení ke vzdálené ploše jenom na portu TCP 3389. 

Předpona, kterou jste zadali v šabloně nasazení, je předpona názvu virtuálního počítače. Pokud například jako předponu nastavíte "contoso", název počítače řadiče domény je `contosoDC` .


### `<prefix>DC01`

- Řadič domény služby Active Directory
- Standard_B2s, který má dva procesory a 4 GB paměti.
- Windows Server 2019 Datacenter Edition

#### <a name="windows-features-and-roles"></a>Funkce a role Windows
- Active Directory Domain Services (Přidat)
- .NET
- Funkce Remote Differential Compression (RDC)


### `<prefix>PS01`

- Standard_B2ms, který má dva procesory a 8 GB paměti
- Windows Server 2016 Datacenter Edition
- SQL Server
- Windows 10 ADK s Windows PE 
- Configuration Manager primární lokalita

#### <a name="windows-features-and-roles"></a>Funkce a role Windows
- .NET
- Funkce Remote Differential Compression (RDC) 
- Internetová informační služba (IIS)


### `<prefix>DPMP01`

- Standard_B2s, který má dva procesory a 4 GB paměti.
- Windows Server 2019 Datacenter Edition
- Distribuční bod
- Bod správy

#### <a name="windows-features-and-roles"></a>Funkce a role Windows
- .NET
- Funkce Remote Differential Compression (RDC) 
- Internetová informační služba (IIS)
- Služba inteligentního přenosu na pozadí (BITS)

### `<prefix>CL01`

- Pouze pro šablonu hodnocení aktuální větve Configuration Manager
- Windows 10
- Klient Configuration Manager