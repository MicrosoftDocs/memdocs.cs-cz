---
title: Instalace konektoru Exchange Connector
titleSuffix: Configuration Manager
description: Nainstalujte a nakonfigurujte Exchange Connector pro Configuration Manager pro správu mobilních zařízení přes ActiveSync.
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: e179e30a-a1fc-461e-8087-ff3a55803450
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e0db550369ca2d81f42a25e68960b5f8f27be168
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700476"
---
# <a name="install-and-configure-the-exchange-connector"></a>Instalace a konfigurace softwaru Exchange Connector

*Platí pro: Configuration Manager (Current Branch)*

Pomocí tohoto postupu nainstalujete a nakonfigurujete konektor systému Exchange Server pro správu mobilních zařízení. Configuration Manager podporuje jenom jeden konektor v organizaci Exchange.

Před instalací konektoru serveru Exchange Server pro Configuration Manager ověřte, zda máte požadovaná oprávnění a verze. Další informace najdete v tématu [Správa zařízení pomocí Exchange a Configuration Manager](manage-mobile-devices-with-exchange-activesync.md#prerequisites).

## <a name="exchange-connection-account"></a>Účet připojení systému Exchange

Určete, který účet se připojí k serveru Exchange Client Access za účelem správy mobilních zařízení. Účet může být účet počítače serveru lokality nebo účet uživatele systému Windows.

Pak nakonfigurujte tento účet ve skupině rolí Exchange a spusťte následující rutiny Exchange serveru:

- **Clear-ActiveSyncDevice**  

- **Get-ActiveSyncDevice**  

- **Get-ActiveSyncDeviceAccessRule**  

- **Get-ActiveSyncDeviceStatistics**  

- **Get-ActiveSyncMailboxPolicy**  

- **Get-ActiveSyncOrganizationSettings**  

- **Get-ExchangeServer**  

- **Získat poštovní schránku**

- **Get-Recipient**  

- **Set-ADServerSettings**  

- **Set-ActiveSyncDeviceAccessRule**  

- **Set-ActiveSyncMailboxPolicy**  

- **Set-CASMailbox**  

- **New-ActiveSyncDeviceAccessRule**  

- **New-ActiveSyncMailboxPolicy**  

- **Remove-ActiveSyncDevice**  

- **Get-CasMailbox**  

- **Získat uživatele**  

- **Set-ActiveSyncOrganizationSettings**  

Následující role správy systému Exchange Server zahrnují tyto rutiny:

- Správa příjemců
- Správa organizace jen pro zobrazení
- Správa serveru

Další informace najdete v tématu [Principy skupin rolí správy](/exchange/understanding-management-role-groups-exchange-2013-help) v dokumentaci k systému Exchange Server 2013.

> [!TIP]  
> Pokud se pokusíte nainstalovat nebo použít konektor systému Exchange Server bez požadovaných rutin, zobrazí se v souboru EasDisc. log na počítači serveru lokality následující chyba: `Invoking cmdlet <cmdlet> failed` .

## <a name="install-the-connector"></a>Instalace konektoru

1. V konzole Configuration Manager klikněte na pracovní prostor **Správa** , rozbalte **Konfigurace hierarchie**a potom vyberte **konektory systému Exchange Server**.

1. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte možnost **Přidat Exchange Server**.

1. Na stránce **Obecné** v Průvodci přidáním serveru Exchange vyberte jednu z prostředí Exchange serveru:

    - **Místní Exchange Server**: zadejte jeden server nebo pole serveru Client Access pro každou lokalitu služby Active Directory.

        Pokud je server nebo pole v režimu offline, Configuration Manager se pokusí zjistit Server Client Access, který se má použít. Pokud se to nepovede, Configuration Manager se vrátí k používání serveru poštovních schránek, aby se navázáno připojení k serveru Client Access. Při opakovaném pokusu o připojení zaznamená následující upozornění do souboru EasDisc. log na počítači serveru lokality: `Failed to open runspace for site <site_name>` .

    - **Hostovaný Exchange Server**: zadejte adresu serveru vašeho prostředí Exchange Online.

    Pak vyberte primární lokalitu, ke které se má konektor systému Exchange Server spustit.

1. Na stránce **účet** zadejte účet, který se má připojit k serveru Exchange. Další informace najdete v tématu [účet pro připojení k systému Exchange](#exchange-connection-account).

1. Na stránce **zjišťování** nakonfigurujte plán synchronizace a pravidla pro hledání zařízení.

1. Na stránce **Nastavení** nakonfigurujte nastavení mobilních zařízení v následujících skupinách:

    - **Obecné**
    - **Heslo**
    - **Správa e-mailů**
    - **Zabezpečení**
    - **Aplikace**

    Další informace najdete v tématu [nastavení Exchange Connectoru](manage-mobile-devices-with-exchange-activesync.md#policies).

    Pokud zapisujete i mobilní zařízení pomocí Configuration Manager místní správy mobilních zařízení ( [MDM](../understand/manage-mobile-devices-with-on-premises-infrastructure.md)), povolte možnost **Povolit externí správu mobilních zařízení**. Toto nastavení umožňuje, aby tato mobilní zařízení pokračovala v doručování e-mailů ze serveru Exchange, až je Configuration Manager zaregistrovali.

1. Dokončete průvodce.

## <a name="verify-and-monitor"></a>Ověřit a monitorovat

Ověřte instalaci konektoru systému Exchange Server se stavovým zprávou a soubory protokolu:

- Potvrďte, že Správce součástí lokality úspěšně nainstaloval konektor serveru Exchange Server. Vyhledejte zprávu ID stavu **1015** ze součásti **SMS_EXCHANGE_CONNECTOR** .

    Instalace může selhat, pokud je zadaný server pro klientský přístup v režimu offline. Pokud Configuration Manager nemůže konektor úspěšně nainstalovat, Configuration Manager se znovu pokusí o instalaci každých 60 minut. Stále se bude opakovat, dokud se instalace nepodaří nebo neodeberete konektor serveru Exchange Server.

- Na počítači serveru lokality zkontrolujte **protokol Sitecomp. log** pro následující položku: `Component SMS_EXCHANGE_CONNECTOR flagged for installation` . Pak protokoluje úspěšnou instalaci s následujícím textem: `STATMSG: ID=1015` .

Po dokončení instalace monitorujte mobilní zařízení, která jsou nalezena a spravována konektorem. Zobrazení kolekcí mobilních zařízení a používání sestav pro mobilní zařízení.

> [!NOTE]  
> Configuration Manager generuje názvy pro mobilní zařízení, která najde. Používá*typ zařízení*formát *uživatelského jména*_. Například **jdoe_WindowsPhone**. Pokud má uživatel více než jedno mobilní zařízení, které má stejný typ zařízení, Configuration Manager zobrazí pro tato mobilní zařízení stejný název v konzole a v sestavách.  

## <a name="see-also"></a>Viz také:

- [Porty používané klienty konfigurace a systémy lokality](../../core/plan-design/hierarchy/ports.md#BKMK_PortsExchangeConnectorHosted)
- [Podpora proxy serveru](../../core/plan-design/network/proxy-server-support.md#site-system-roles-that-use-a-proxy)
- [Doporučení zabezpečení pro mobilní zařízení](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#bkmk_mobile)
- [Informace o ochraně osobních údajů pro mobilní zařízení spravovaná pomocí konektoru systému Exchange Server](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#BKMK_Privacy_ExchangeConnector)