---
title: Řešení běžných potíží s Intune Exchange Connectorem
titleSuffix: Microsoft Intune
description: Řešení potíží a řešení běžných potíží s místními Microsoft Intune Exchange Connector.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/06/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b1ed3cd24c05586bd5dc9d9a2443a33ffcdc2a48
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914799"
---
# <a name="resolve-common-problems-with-the-intune-exchange-connector"></a>Řešení běžných problémů s Intune Exchange Connectorem
 
Tento článek vám může pomáhat správci Intune vyřešit běžné problémy s provozem Intune Exchange Connectoru.

Než začnete řešit potíže, přečtěte si téma [Poradce při potížích s místním Exchange Connectorem Intune](troubleshoot-exchange-connector.md) , kde najdete základní informace o tomto konektoru. Projděte si také běžné problémy s konfigurací konektoru.

## <a name="an-exchange-activesync-device-isnt-discovered-from-exchange"></a>Nezjistilo se zařízení Exchange ActiveSync ze systému Exchange.

Pokud se zařízení Exchange ActiveSync nezjistí ze serveru Exchange, [sledujte aktivitu Exchange Connector](exchange-connector-install.md#on-premises-intune-exchange-connector-high-availability-support) a zjistěte, jestli se konektor Exchange Connector synchronizuje s Exchange serverem. Pokud se vám od připojení zařízení nestalo žádná synchronizace, Shromážděte protokoly synchronizace a připojte je k žádosti o podporu. Pokud se po připojení zařízení úspěšně dokončila Úplná synchronizace nebo rychlá synchronizace, podívejte se na následující problémy:

- Ujistěte se, že uživatelé mají licenci Intune. V takovém případě Exchange Connector nezjistí jejich zařízení.

- Pokud je primární adresa SMTP uživatele odlišná od hlavního názvu uživatele (UPN) v Azure Active Directory (Azure AD), Exchange Connector nezjistí žádná zařízení pro tohoto uživatele. Tento problém vyřešíte tím, že opravíte primární adresu SMTP.

- Pokud ve vašem prostředí máte servery poštovních schránek Exchange 2010 i Exchange 2013, doporučujeme, abyste odkazovali na Exchange Connector na Exchange 2013 Server pro přístup klienta (CAS). Pokud je Exchange Connector nastavený tak, aby komunikoval s certifikačními autoritami Exchange 2010, Exchange Connector nezjistí žádná zařízení uživatele na Exchangi 2013.

- V případě vyhrazeného prostředí Exchange Online je nutné při počátečním nastavení nasměrovat konektor Exchange na servery Exchange 2013 CAS (nikoli CAS Exchange 2010). Konektor bude při provádění rutin PowerShellu komunikovat jenom s CAS Exchange 2013.

## <a name="problems-with-the-notification-email-message"></a>Problémy s e-mailovou zprávou s oznámením

Aby bylo možné podporovat podmíněný přístup k místním poštovním schránkám na zařízeních, která nepoužívají Android KNOX, zajistěte, aby se registrace do Intune spouštěla z e-mailové zprávy "Začínáme nyní", kterou odesílá Intune Exchange Connector. Při spuštění registrace ze zprávy se zajistí, že zařízení bude přijímat jedinečné ActiveSyncID napříč všemi platformami (Exchange, Azure AD, Intune).

Uživatel pravděpodobně neobdrží e-mailovou zprávu s oznámením z těchto důvodů:

- Účet oznámení byl nastaven nesprávně.
- Automatická konfigurace pro účet oznámení se nezdařila.
- Požadavek webové služby Exchange (EWS) k odeslání e-mailové zprávy se nezdařil.

V následujících částech najdete řešení potíží s e-mailovými oznámeními.

### <a name="check-the-notification-account-that-retrieves-autodiscover-settings"></a>Ověřte účet oznámení, který načte nastavení automatické konfigurace.

1. Ujistěte se, že je služba automatické konfigurace a EWS nakonfigurovaná ve službách Exchange Client Access. Další informace najdete v tématu [služby pro klientský přístup](/Exchange/architecture/client-access/client-access) a [Služba automatické konfigurace v systému Exchange Server](/Exchange/architecture/client-access/autodiscover?view=exchserver-2019).

2. Ověřte, že váš účet oznámení splňuje následující požadavky:

   - Účet má aktivní poštovní schránku, která je hostovaná na místním serveru Exchange.

   - Hlavní název uživatele (UPN) účtu se shoduje s adresou SMTP.

3. Automatická konfigurace vyžaduje server DNS, který má záznam DNS pro **Autodiscover.SMTPdomain.com** (například Autodiscover.contoso.com), který odkazuje na server Exchange Client Access. Chcete-li vyhledat záznam, zadejte plně kvalifikovaný název domény místo *Autodiscover.SMTPdomain.com* a postupujte podle následujících kroků:

   1. Na příkazovém řádku zadejte příkaz *nslookup*.

   2. Zadejte *Autodiscover.SMTPdomain.com*. Výstup by měl vypadat podobně jako na následujícím obrázku: ![ výsledky nslookup](./media/troubleshoot-exchange-connector-common-problems/nslookup-results.png
      )

   Službu Automatická konfigurace můžete také otestovat z Internetu na adrese https://testconnectivity.microsoft.com . Nebo ho testujte z místní domény pomocí nástroje Microsoft Connectivity Analyzer. Další informace najdete v tématu [Nástroj Microsoft Connectivity Analyzer](/previous-versions/office/exchange-remote-connectivity/jj851141(v=exchg.80)).


### <a name="check-autodiscover"></a>Ověřit automatické konfigurace

Pokud se automatická konfigurace nezdařila, zkuste provést následující kroky:

1. [Nakonfigurujte platný záznam DNS konfigurace](/previous-versions/exchange-server/exchange-150/mt473798(v=exchg.150)).

2. V konfiguračním souboru Intune Exchange Connectoru pevně zakódovat adresu URL služby EWS:

   1. Určete adresu URL EWS. Výchozí adresa URL služby EWS pro Exchange je `https://<mailServerFQDN>/ews/exchange.asmx` , ale adresa URL se může lišit. Obraťte se na správce Exchange a ověřte správnou adresu URL vašeho prostředí.

   2. Upravte soubor *OnPremisesExchangeConnectorServiceConfiguration.xml* . Ve výchozím nastavení se soubor nachází v *%ProgramData%\Microsoft\Windows Intune Exchange Connectoru* na počítači, na kterém běží konektor Exchange Connector. Otevřete soubor v textovém editoru a pak změňte následující řádek tak, aby odrážel adresu URL služby EWS pro vaše prostředí: `<ExchangeWebServiceURL>https://<YourExchangeHOST>/EWS/Exchange.asmx</ExchangeWebServiceURL>`

3. Uložte soubor a restartujte počítač nebo restartujte službu Microsoft Intune Exchange Connector.

>[!NOTE]
> V této konfiguraci Intune Exchange Connector přestane používat funkci automatického připojení a místo toho se připojí přímo k adrese URL EWS.

## <a name="next-steps"></a>Další kroky

Pokud potřebujete nápovědu s konkrétními chybami, zkuste [vyřešit běžné chyby pro Intune Exchange Connector](troubleshoot-exchange-connector-common-errors.md).

Pokud chcete získat podporu nebo získat pomoc od komunity Intune:

- V tématu [získání podpory](../fundamentals/get-support.md) pro používání konzoly Intune můžete vyřešit potíže nebo otevřít případ podpory s Microsoftem.
- Vystavte svůj problém ve [fórech Microsoft Intune](https://social.technet.microsoft.com/Forums/home?forum=microsoftintuneprod).