---
title: Nastavení konektoru Microsoft Intune Exchange
titleSuffix: Microsoft Intune
description: Pomocí on-premises Intune Exchange Connector můžete spravovat přístup zařízení k poštovním schránkám Exchange na základě registrace v Intune a Exchange ActiveSync (EAS).
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a0376ea1-eb13-4f13-84da-7fd92d8cd63c
ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e646ce40acaa156910f516c475cd6b0885989941
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462183"
---
# <a name="set-up-the-on-premises-intune-exchange-connector"></a>Nastavení místního Intune Exchange Connectoru

> [!IMPORTANT]
> Informace v tomto článku se vztahují na zákazníky, kteří jsou podporováni pro použití konektoru Exchange.
>
> Od 1. července 2020 se podpora pro Exchange Connector zastaralá a nahrazuje ji pomocí [hybridního moderního ověřování](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview) Exchange (HMA).  Pokud máte ve svém prostředí nastavený Exchange Connector, zůstane klient Intune pro jeho použití podporovaný a vy budete mít přístup k uživatelskému rozhraní, které podporuje jeho konfiguraci. Můžete dál používat konektor nebo nakonfigurovat HMA a pak konektor odinstalovat.
>
>Použití paměti HMA nevyžaduje instalaci Intune a použití konektoru Exchange. Díky této změně se uživatelské rozhraní pro konfiguraci a správu Exchange Connectoru pro Intune odebralo z centra pro správu Microsoft Endpoint Manageru, pokud už nepoužíváte Exchange Connector s vaším předplatným.

Aby se chránil přístup k Exchangi, Intune spoléhá na místní komponentu, která se označuje jako konektor Microsoft Intune Exchange. Tento konektor se také označuje jako *konektor Exchange ActiveSync On-Premises Connector* v některých umístěních konzoly Intune.

> [!IMPORTANT]
> V Intune se odebere podpora funkce konektoru On-Premises Connector ze služby Intune počínaje verzí 2007 (červenec). Stávající zákazníci s aktivním konektorem budou v tuto chvíli moci pokračovat s aktuálními funkcemi. Noví zákazníci a stávající zákazníci, kteří nemají aktivní konektor, už nebudou moct vytvářet nové konektory ani spravovat zařízení Exchange ActiveSync (EAS) z Intune. Pro tyto klienty Microsoft doporučuje používat [hybridní moderní ověřování Exchange (HMA)](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview) k ochraně přístupu k místnímu Exchangi. HMA umožňuje Intune App Protection zásady (označované také jako MAM) a podmíněný přístup prostřednictvím Outlook Mobile pro místní Exchange.

Informace v tomto článku vám pomůžou nainstalovat a monitorovat konektor Intune Exchange Connector. Konektor se [zásadami podmíněného přístupu](conditional-access-exchange-create.md) můžete použít k povolení nebo blokování přístupu k místním poštovním schránkám Exchange.

Konektor se nainstaluje a spustí na místním hardwaru. Zjišťuje zařízení, která se připojují k Exchangi, a komunikuje informace o zařízení do služby Intune. Konektor povolí nebo zablokuje zařízení na základě toho, jestli jsou zařízení zaregistrovaná a kompatibilní. Tato komunikace používá protokol HTTPS.

Když se zařízení pokusí získat přístup k místnímu Exchange serveru, Exchange Connector mapuje záznamy Exchange ActiveSync (EAS) na Exchange serveru na záznamy Intune, aby se ujistili, že se zařízení zaregistruje v Intune a vyhovuje zásadám vašeho zařízení. V závislosti na zásadách podmíněného přístupu se může zařízení povolit nebo zablokovat. Další informace najdete v tématu [co jsou běžné způsoby použití podmíněného přístupu s Intune](conditional-access-intune-common-ways-use.md) .

Operace *zjišťování* i *povolování i blokování* jsou prováděny pomocí standardních rutin prostředí Exchange PowerShell. Tyto operace používají účet služby, který je k dispozici při počáteční instalaci softwaru Exchange Connector.

Intune podporuje instalaci více konektorů Intune Exchange pro každé předplatné. Pokud máte více než jednu místní organizaci Exchange, můžete pro každý z nich nastavit samostatný konektor. Pro každou organizaci Exchange se ale dá nainstalovat jenom jeden konektor.  

Při nastavování připojení, které Intune umožňuje komunikaci s místním Exchange serverem, postupujte podle těchto obecných kroků:

1. Stáhněte si konektor On-Premises Connector z portálu Intune.
2. Nainstalujte a nakonfigurujte Exchange Connector na počítači v místní organizaci Exchange.
3. Ověřte připojení k Exchangi.
4. Tento postup opakujte pro každou další organizaci Exchange, kterou chcete připojit k Intune.

## <a name="how-conditional-access-for-exchange-on-premises-works"></a>Jak podmíněný přístup pro místní Exchange funguje

Podmíněný přístup pro místní Exchange funguje jinak než zásady založené na podmíněném přístupu Azure. Intune Exchange On-Premises Connector nainstalujete k přímé interakci se systémem Exchange Server. Konektor Intune Exchange si vyžádá všechny záznamy Exchange Active Sync (EAS), které existují na serveru Exchange, aby Intune mohl tyto záznamy EAS namapovat na záznamy zařízení Intune. Tyto záznamy jsou zařízení zaregistrovaná a rozpoznaná službou Intune. Tento proces povolí nebo zablokuje přístup k e-mailu.

Pokud je záznam EAS nový a Intune o něm není vědět, Intune vydá rutinu (příkaz-let), která přesměruje Exchange Server, aby blokoval přístup k e-mailu. Níže najdete další podrobnosti o tom, jak tento proces funguje:

> [!div class="mx-imgBorder"]
> ![Vývojový diagram místního Exchange s podmíněným přístupem](./media/exchange-connector-install/ca-intune-common-ways-1.png)

1. Uživatel se pokusí o přístup k podnikovému e-mailu, který je hostovaný na místním Exchangi 2010 SP1 nebo novějším.

2. Pokud zařízení nespravuje Intune, bude přístup k e-mailu blokovaný. Intune pošle klientovi EAS oznámení o blokování.

3. EAS obdrží oznámení o zablokování, přesune zařízení do karantény a odešle e-mail o karanténě s kroky k nápravě, které obsahují odkazy, aby uživatelé mohli svá zařízení zaregistrovat.

4. Provede se proces připojení k pracovišti, který je prvním krokem k tomu, aby se zařízení spravovalo pomocí Intune.

5. Zařízení se zaregistruje v Intune.

6. Intune namapuje záznam EAS na záznam zařízení a uloží stav dodržování předpisů zařízením.

7. ID klienta EAS se zaregistruje prostřednictvím procesu registrace zařízení Azure AD. Tím se vytvoří vztah mezi záznamem zařízení v Intune a ID klienta EAS.

8. Registrace zařízení Azure AD uloží informace o stavu zařízení.

9. Pokud uživatel splňuje zásady podmíněného přístupu, Intune vydá rutinu prostřednictvím Intune Exchange Connectoru, která umožňuje synchronizaci poštovní schránky.

10. Server Exchange odešle oznámení klientovi EAS, aby uživatel získal přístup k e-mailu.

## <a name="intune-exchange-connector-requirements"></a>Požadavky Intune Exchange Connectoru

Pokud se chcete připojit k Exchangi, potřebujete účet, který má licenci Intune, kterou může konektor používat. Účet určíte při instalaci konektoru.  

V následující tabulce jsou uvedené požadavky na počítač, na který nainstalujete Intune Exchange Connector.  

|  Požadavek  |   Další informace     |
|---------------|------------------------|
|  Operační systémy        | Intune podporuje Intune Exchange Connector na počítači, na kterém běží libovolná edice Windows serveru 2008 SP2 64-bit, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 nebo Windows Server 2016.<br /><br />Konektor není podporován v žádné instalaci jádra serveru.  |
| Microsoft Exchange          | Místní konektory vyžadují Microsoft Exchange 2010 SP3 nebo novější, nebo starší Exchange Online Dedicated. Pokud chcete zjistit, jestli je vaše prostředí Exchange Online Dedicated v *nové* nebo *starší* konfiguraci, kontaktujte svého správce účtů. |
| Autorita pro správu mobilních zařízení           | [Nastavte autoritu pro správu mobilních zařízení na Intune](../fundamentals/mdm-authority-set.md). |
| Hardware              | Počítač, na který nainstaluje konektor, musí mít minimálně 1,6GHz procesor s 2 GB paměti RAM a 10 GB volného místa na disku. |
|  Synchronizace se službou Active Directory             | Před použitím konektoru k připojení Intune k serveru Exchange [nastavte synchronizaci služby Active Directory](../fundamentals/users-add.md). Místní uživatelé a skupiny zabezpečení se musí synchronizovat s vaší instancí Azure Active Directory. |
| Další software         | Počítač, který je hostitelem konektoru, musí mít úplnou instalaci Microsoft .NET Framework 4,5 a Windows PowerShell 2,0. |
| Síť               | Počítač, na který instalujete konektor, musí být v doméně, která má vztah důvěryhodnosti s doménou, která hostuje server Exchange.<br /><br />Nakonfigurujte počítač tak, aby umožňoval přístup ke službě Intune přes brány firewall a proxy servery přes porty 80 a 443. Intune tyto domény používá: <br> – manage.microsoft.com <br> - \*manage.microsoft.com<br> - \*. manage.microsoft.com <br><br> Intune Exchange Connector komunikuje s následujícími službami: <br> – Služba Intune: port HTTPS 443 <br> – Exchange Client Access Server (CAS): port služby WinRM 443<br> – Exchange # 443<br> – Webové služby Exchange (EWS) 443  |

### <a name="exchange-cmdlet-requirements"></a>Požadavky rutin systému Exchange

Vytvořte uživatelský účet služby Active Directory pro Intune Exchange Connector. Tento účet musí mít oprávnění ke spuštění následujících rutin Windows PowerShellu pro Exchange:  

- `Get-ActiveSyncOrganizationSettings`, `Set-ActiveSyncOrganizationSettings`
- `Get-CasMailbox`, `Set-CasMailbox`
- `Get-ActiveSyncMailboxPolicy`, `Set-ActiveSyncMailboxPolicy`, `New-ActiveSyncMailboxPolicy`, `Remove-ActiveSyncMailboxPolicy`
- `Get-ActiveSyncDeviceAccessRule`, `Set-ActiveSyncDeviceAccessRule`, `New-ActiveSyncDeviceAccessRule`, `Remove-ActiveSyncDeviceAccessRule`
- `Get-ActiveSyncDeviceStatistics`
- `Get-ActiveSyncDevice`
- `Get-ExchangeServer`
- `Get-ActiveSyncDeviceClass`
- `Get-Recipient`
- `Clear-ActiveSyncDevice`, `Remove-ActiveSyncDevice`
- `Set-ADServerSettings`
- `Get-Command`

## <a name="download-the-installation-package"></a>Stažení instalačního balíčku

Na Windows serveru, který může podporovat Intune Exchange Connector:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).  Použijte účet, který je správcem místního Exchange serveru a který má licenci k používání Exchange serveru.

2. Vyberte možnost **Správce klienta**  >  **přístup k Exchangi**.

3. V části **Nastavení**zvolte **Exchange ActiveSync On-Premises Connector** a pak vyberte **Přidat**.

   > [!div class="mx-imgBorder"]
   > ![Přidání konektoru On-Premises Exchange ActiveSync](./media/exchange-connector-install/add-connector.png)

4. Na stránce **Přidat konektor** vyberte **Stáhnout konektor On-Premises Connector**. Intune Exchange Connector je v komprimované složce (. zip), která se dá otevřít nebo Uložit. V dialogovém okně **Stažení souboru** klikněte na **Uložit** a uložte komprimovanou složku do zabezpečeného umístění.

## <a name="install-and-configure-the-intune-exchange-connector"></a>Instalace a konfigurace Intune Exchange Connectoru

Pomocí těchto kroků nainstalujete Intune Exchange Connector. Pokud máte více organizací Exchange, opakujte postup u každého konektoru Exchange, který chcete nastavit.

1. V podporovaném operačním systému pro Intune Exchange Connector extrahujte soubory z **Exchange_Connector_Setup.zip** do zabezpečeného umístění.
   > [!IMPORTANT]
   > Soubory, které jsou ve složce *Exchange_Connector_Setup* , nemusíte přejmenovat ani přesouvat. Tyto změny by způsobily selhání instalace konektoru.

2. Po extrahování souborů otevřete extrahovanou složku a dvojím kliknutím na **Exchange_Connector_Setup.exe** instalaci konektoru nainstalujte.

   > [!IMPORTANT]
   > Pokud cílová složka není v zabezpečeném umístění, po dokončení instalace místních konektorů odstraňte soubor certifikátu *MicrosoftIntune. accountcert* .

3. V dialogovém okně **Microsoft Intune Exchange Connector** vyberte **On-premises Microsoft Exchange Server** nebo **Hostovaný Microsoft Exchange Server**.

   ![Obrázek znázorňující, kde vybrat typ Exchange Serveru](./media/exchange-connector-install/intune-sa-exchange-connector-config.png)

   V případě místního serveru Exchange zadejte název serveru nebo plně kvalifikovaný název domény serveru Exchange, který je hostitelem role **Server pro klientský přístup**.

   U hostovaného serveru Exchange zadejte adresu serveru Exchange. Adresu URL hostovaného serveru Exchange najdete takto:

   1. Otevřete Outlook pro Office 365.

   2. Vyberte **?** v levém horním rohu a pak vyberte **o**.

   3. Najděte hodnotu **Externí nastavení POP**.

   4. Vyberte **Proxy server** a zadejte nastavení proxy serveru pro svůj hostovaný server Exchange.

       1. Vyberte **Používat proxy server při synchronizaci informací mobilních zařízení**.

       1. Zadejte **název proxy serveru** a **číslo portu** pro přístup na server.

       1. Pokud jsou pro přístup k proxy server vyžadovány přihlašovací údaje uživatele, vyberte **použít pověření pro připojení k proxy server**. Zadejte **doménu\uživatele** a **heslo**.

       1. Vyberte **OK**.

4. Do polí **uživatel (doména \ Uživatel)** a **heslo** zadejte přihlašovací údaje pro připojení k serveru Exchange. Účet, který zadáte, musí mít licenci k používání Intune.

5. Zadejte přihlašovací údaje pro odesílání oznámení do poštovní schránky Exchange serveru uživatele. Tento uživatel může být vyhrazený jenom pro oznámení. Uživatel oznámení potřebuje poštovní schránku Exchange k odesílání oznámení e-mailem. Tato oznámení můžete nakonfigurovat pomocí zásad podmíněného přístupu v Intune.

   Ujistěte se, že je služba Automatická konfigurace a webové služby systému Exchange nakonfigurované na certifikačních autoritách Exchange. Další informace najdete v tématu [Server pro klientský přístup](https://technet.microsoft.com/library/dd298114.aspx).

6. Do pole **heslo** zadejte heslo pro tento účet, aby měl Intune přístup k systému Exchange Server.

   > [!NOTE]
   > Účet, pomocí kterého se přihlašujete ke klientovi, musí být aspoň Správce služby Intune. Bez tohoto účtu správce obdržíte neúspěšné připojení s chybou "vzdálený server vrátil chybu: (400) chybný požadavek.

7. Zvolte **Připojit**.

   > [!NOTE]
   > Konfigurace připojení může trvat několik minut.

V průběhu konfigurace konektor Exchange Connector ukládá vaše nastavení proxy serveru, aby mohl mít přístup k Internetu. Pokud se vaše nastavení proxy serveru změní, překonfigurujte Exchange Connector tak, aby na konektoru Exchange použili aktualizované nastavení proxy serveru.

Jakmile Exchange Connector nastaví připojení, mobilní zařízení přidružená k uživatelům spravovaným systémem Exchange budou automaticky synchronizována a přidána do konektoru Exchange. Dokončení této synchronizace může chvíli trvat.

> [!NOTE]
> Pokud nainstalujete Intune Exchange Connector a později potřebujete odstranit připojení k Exchangi, musíte konektor odinstalovat z počítače, na kterém je nainstalovaný.

## <a name="install-connectors-for-multiple-exchange-organizations"></a>Instalace konektorů pro více organizací Exchange

Intune podporuje několik konektorů Intune Exchange pro každé předplatné. U tenanta s více organizacemi Exchange můžete pro každou organizaci Exchange nastavit jenom jeden konektor.

Chcete-li nainstalovat konektory pro připojení k více organizacím systému Exchange, Stáhněte složku. zip jednou. Pro každý konektor, který nainstalujete, znovu použijte stejné soubory ke stažení. Pro každý další konektor použijte postup v předchozí části k extrakci a spuštění instalačního programu na serveru v organizaci Exchange.

Každá organizace Exchange, která se připojuje k Intune, podporuje vysokou dostupnost, monitorování a ruční synchronizaci. Tyto funkce jsou popsány v následujících částech.

## <a name="on-premises-intune-exchange-connector-high-availability-support"></a>Podpora vysoké dostupnosti místní služby Intune Exchange Connector  

U konektoru On-Premises Connector to znamená, že pokud CAS serveru Exchange, kterou konektor používá, nebude k dispozici, konektor může pro tuto organizaci Exchange přejít na jiné certifikační autority. Exchange Connector sám nepodporuje vysokou dostupnost. Pokud se konektoru nepovede, neexistuje žádné automatické převzetí služeb při selhání a musíte [nainstalovat nový konektor](#reinstall-the-intune-exchange-connector) , aby se neúspěšný konektor nahradil.

Pro převzetí služeb při selhání konektor pomocí zadaných certifikačních autorit vytvoří úspěšné připojení k Exchangi. Pak zjistí další servery CAS pro tuto organizaci Exchange. Toto zjišťování umožňuje konektoru převzít služby při selhání jiné certifikační autority, pokud je k dispozici, dokud nebudou primární CA k dispozici.

Ve výchozím nastavení je povoleno zjišťování dalších servery CAS. Pokud potřebujete vypnout převzetí služeb při selhání:

1. Na serveru, na kterém je nainstalovaný Exchange Connector, navštivte ** % *Složka ProgramData*% \ Microsoft\Windows Intune Exchange Connector**.

2. V textovém editoru otevřete soubor **OnPremisesExchangeConnectorServiceConfiguration.xml**.

3. Změňte ** \<IsCasFailoverEnabled> *hodnotu true* \</IsCasFailoverEnabled> ** na ** \<IsCasFailoverEnabled> *false*false \</IsCasFailoverEnabled> **.

## <a name="performance-tune-the-exchange-connector-optional"></a>Výkon – ladění Exchange Connectoru (volitelné)

Když Exchange ActiveSync podporuje 5 000 nebo více zařízení, můžete nakonfigurovat volitelné nastavení pro zlepšení výkonu konektoru. Můžete zvýšit výkon tím, že povolíte serveru Exchange používat více instancí prostředí PowerShellového místa pro spuštění.

Než tuto změnu provedete, ujistěte se, že účet, který používáte ke spuštění Exchange Connectoru, se nepoužije pro jiné účely správy Exchange. Účet systému Exchange má omezený počet mezer za běhu a konektor bude používat většinu z nich.

Ladění výkonu není vhodné pro konektory, které běží na starším nebo pomalejším hardwaru.

Zlepšení výkonu konektoru Exchange Connector:

1. Na serveru, na kterém je nainstalovaný konektor, otevřete instalační adresář konektoru.  Výchozí umístění je *C:\ProgramData\Microsoft\Windows Intune Exchange Connector*.

2. Upravte soubor *OnPremisesExchangeConnectorServiceConfiguration.xml*.

3. Vyhledejte **EnableParallelCommandSupport** a nastavte hodnotu na **true**:

   \<EnableParallelCommandSupport>true\</EnableParallelCommandSupport>

4. Uložte soubor a pak restartujte službu Microsoft Intune Exchange Connector.

## <a name="reinstall-the-intune-exchange-connector"></a>Opětovná instalace Intune Exchange Connectoru

Možná budete muset přeinstalovat konektor Intune Exchange. Vzhledem k tomu, že se ke každé organizaci Exchange může připojit jenom jeden konektor, pokud pro organizaci nainstalujete druhý konektor, nový konektor, který nainstalujete, nahradí původní konektor.

1. Pokud chcete nainstalovat nový konektor, postupujte podle pokynů v části [instalace a konfigurace konektoru Exchange](#install-and-configure-the-intune-exchange-connector) .

2. Po zobrazení výzvy vyberte **nahradit** a nainstalujte nový konektor.
   ![Upozornění konfigurace k nahrazení konektoru](./media/exchange-connector-install/prompt-to-replace.png)

3. Pokračujte postupem v části [instalace a konfigurace konektoru Intune Exchange](#install-and-configure-the-intune-exchange-connector) a znovu se přihlaste k Intune.

4. V posledním okně vyberte **Zavřít** a dokončete instalaci.
   ![Dokončení instalace](./media/exchange-connector-install/successful-reinstall.png)

## <a name="monitor-an-exchange-connector"></a>Monitorování konektoru softwaru Exchange

Po úspěšné konfiguraci softwaru Exchange Connector můžete zobrazit stav připojení a poslední úspěšný pokus o synchronizaci:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte možnost **Správce klienta**  >  **přístup k Exchangi**.

3. Vyberte **Exchange ActiveSync On-Premises Connector**a pak vyberte konektor, který chcete zobrazit.

4. Konzola zobrazí podrobnosti o konektoru, který jste vybrali, kde můžete zobrazit **stav** a datum a čas poslední úspěšné synchronizace.

Kromě stavu v konzole můžete použít [Management Pack System Center Operations Manager pro Exchange Connector a Intune](https://www.microsoft.com/download/details.aspx?id=55990&751be11f-ede8-5a0c-058c-2ee190a24fa6=True&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True&fa43d42b-25b5-4a42-fe9b-1634f450f5ee=True). Management Pack nabízí různé způsoby, jak monitorovat Exchange Connector, pokud potřebujete řešit problémy.

## <a name="manually-force-a-quick-sync-or-full-sync"></a>Ruční vynucení rychlé synchronizace nebo úplné synchronizace

Intune Exchange Connector automaticky synchronizuje záznamy zařízení EAS a Intune. Pokud se stav dodržování předpisů změní na zařízení, proces automatické synchronizace pravidelně aktualizuje záznamy, aby bylo možné zablokovat nebo povolit přístup k zařízení.

- **Rychlá synchronizace** probíhá pravidelně, několikrát za den. Rychlá synchronizace načte informace o zařízení pro uživatele s licencí na Intune a na místní Exchange, které jsou cílené na podmíněný přístup a které se od poslední synchronizace změnily.

- **Úplná synchronizace** probíhá ve výchozím nastavení jednou denně. Úplná synchronizace načte informace o zařízení pro všechny uživatele licencované pro Intune a místní Exchange, na které cílí podmíněný přístup. Úplná synchronizace také načte informace Exchange serveru a zajistí, že konfigurace, kterou Intune určí v Azure Portal, bude aktualizována na serveru Exchange.

Konektor můžete vynutit ke spuštění synchronizace pomocí možností **rychlá synchronizace** nebo **úplné synchronizace** na řídicím panelu Intune:

   1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

   2. Vyberte **klienta Správa tenanta**  >  **Exchange**  >   **ActiveSync On-Premises Connector**.

   3. Vyberte konektor, který chcete synchronizovat, a pak zvolte Rychlá synchronizace nebo Úplná synchronizace.

   > [!div class="mx-imgBorder"]
   > ![Příklad snímku obrazovky s podrobnostmi konektoru](./media/exchange-connector-install/connector-details.png)

## <a name="next-steps"></a>Další kroky

Vytvořte [zásady podmíněného přístupu pro místní Exchange servery](conditional-access-exchange-create.md).
