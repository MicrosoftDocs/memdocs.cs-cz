---
title: Řešení problémů s konektorem Exchange
titleSuffix: Microsoft Intune
description: Naučte se řešit potíže s místním Intune Exchange Connectorem.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: a7e3c742-295b-40bb-9afa-17f243062500
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3e7f9c984b81bbe98269b0123371d8097d960ffb
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462129"
---
# <a name="troubleshoot-the-intune-exchange-connector"></a>Řešení potíží s Intune Exchange Connectorem

Tento článek popisuje, jak řešit problémy související s Intune Exchange Connectorem.

> [!IMPORTANT]
>
> Od 1. července 2020 se podpora pro Exchange Connector zastaralá a nahrazuje ji pomocí [hybridního moderního ověřování](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview) Exchange (HMA) a možnost přidat konektor Exchange Connector do Intune se odebere.
>
> Zákazníci, kteří dřív nakonfigurovali a používali Exchange Connector, budou mít i nadále podporu konektoru.


## <a name="before-you-start"></a>Než začnete

Než začnete řešit potíže s Exchange Connectorem v Intune, shromážděte některé základní informace, abyste pracovali na Solid Foundation. Tento přístup vám může pomáhat lépe pochopit povahu problému a rychleji ho vyřešit.

- Ověřte, že váš proces splňuje požadavky na instalaci. Viz [nastavení místního Intune Exchange Connectoru](exchange-connector-install.md).
- Ověřte, že váš účet má oprávnění správce Exchange i Intune.
- Poznamenejte si text zpráva o úplné a přesné chybě, podrobnosti a místo, kde se zpráva zobrazuje.
- Určete, kdy problém začal: 
  - Nastavování konektoru poprvé? 
  - Pracoval konektor správně a pak selže?
  - Pokud fungovalo, k jakým změnám došlo v prostředí Intune, prostředí Exchange nebo na počítači, na kterém běží konektorový software?
- Co je Autorita MDM?
- Jakou verzi Exchange používáte?

### <a name="use-powershell-to-get-more-data-on-exchange-connector-issues"></a>Použití PowerShellu k získání dalších informací o problémech s Exchange Connectorem

- Pokud chcete získat seznam všech mobilních zařízení pro poštovní schránku, použijte`Get-ActiveSyncDeviceStatistics -mailbox mbx`
- Chcete-li získat seznam adres SMTP pro poštovní schránku, použijte`Get-Mailbox -Identity user | select emailaddresses | fl`
- Podrobné informace o stavu přístupu k zařízení získáte pomocí`Get-CASMailbox <upn> | fl`

## <a name="review-the-connector-configuration"></a>Kontrola konfigurace konektoru

Zkontrolujte [požadavky na místní Exchange Connector](exchange-connector-install.md#intune-exchange-connector-requirements) , abyste se ujistili, že vaše prostředí a konektor jsou správně nakonfigurované. 

### <a name="general-considerations-for-the-connector"></a>Obecné požadavky konektoru

- Ujistěte se, že brána firewall a proxy servery umožňují komunikaci mezi serverem, který je hostitelem Intune Exchange Connectoru a službou Intune.

- Počítač, který je hostitelem Intune Exchange Connectoru a server Exchange Client Access (CAS), by měl být připojený k doméně a ve stejné síti LAN. Ujistěte se, že se pro účet, který používá Intune Exchange Connector, přidají požadovaná oprávnění.

- Účet oznámení slouží k načtení nastavení *Konfigurace* . Další informace o Autodisover v systému Exchange najdete v tématu [Služba automatické konfigurace v systému Exchange Server](https://docs.microsoft.com/exchange/architecture/client-access/autodiscover?view=exchserver-2016).

- Intune Exchange Connector pošle požadavek na adresu URL služby EWS pomocí přihlašovacích údajů účtu oznámení k odeslání e-mailových zpráv s oznámením s odkazem *Začínáme* (k registraci v Intune). Použití odkazu *Začínáme* k registraci je požadavkem na zařízení s Androidem, která nejsou Knox. Jinak budou tato zařízení blokovaná podmíněným přístupem.

### <a name="common-issues-for-connector-configurations"></a>Běžné problémy s konfiguracemi konektorů

- **Oprávnění účtu**: v dialogovém okně Microsoft Intune Exchange Connector se ujistěte, že jste zadali uživatelský účet, který má příslušná oprávnění ke spouštění [požadovaných rutin prostředí Windows PowerShell Exchange](exchange-connector-install.md#exchange-cmdlet-requirements).
- **E-mailové zprávy s oznámením**: Povolit oznámení a zadat účet oznámení.
- **Synchronizace serveru pro klientský přístup**: při konfiguraci softwaru Exchange Connector zadejte certifikační autority, které mají nejnižší možnou latenci sítě pro server, který je hostitelem konektoru Exchange. Latence komunikace mezi certifikačními autoritami a Exchange Connectorem může zpozdit zjišťování zařízení, zejména pokud používáte vyhrazené Exchange Online.
- **Plán synchronizace**: uživatel s nově zaregistrovaným zařízením se může zpozdit o přístup, dokud se konektor Exchange nesynchronizuje s CERTIFIKAČNÍmi autoritami Exchange. Úplná synchronizace probíhá jednou denně a rozdílová (rychlá) synchronizace probíhá několikrát denně. Pokud chcete minimalizovat zpoždění, můžete [ručně vynutit rychlou synchronizaci nebo úplnou synchronizaci](exchange-connector-install.md#manually-force-a-quick-sync-or-full-sync).

## <a name="next-steps"></a>Další kroky
Následující články vám pomůžou vyřešit běžné problémy a konkrétní chyby:

- [Řešení běžných problémů s Intune Exchange Connectorem](troubleshoot-exchange-connector-common-problems.md)
- [Řešení běžných chyb pro Intune Exchange Connector](troubleshoot-exchange-connector-common-errors.md)

Vyhledejte pomoc od podpory nebo komunity Intune:

- V tématu [získání podpory](../fundamentals/get-support.md) pro používání konzoly Intune můžete pomoct s řešením problému nebo otevřít případ podpory s Microsoftem. 
- Vystavte svůj problém ve [fórech Microsoft Intune](https://social.technet.microsoft.com/Forums/en-US/home?forum=microsoftintuneprod).  
