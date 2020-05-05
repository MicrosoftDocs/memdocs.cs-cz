---
title: Internetová správa klientů
titleSuffix: Configuration Manager
description: Vytvořte plán pro správu internetových klientů v Configuration Manager.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f7054c75643c6ffa37decba74f9fe85831728985
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587213"
---
# <a name="plan-for-internet-based-client-management-in-configuration-manager"></a>Plánování internetové správy klientů v systému Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Použijte internetovou správu klientů (IBCM) ke správě Configuration Manager klientů, když nejsou připojení k vaší interní síti. Výhody použití IBCM:

- Úplné řízení serverů a rolí poskytujících službu
- Žádná závislost cloudové služby
- Nemusí vyžadovat virtuální privátní síť (VPN)
- Všechny náklady jsou spojené s místní službou.

Vzhledem k vyšším požadavkům na zabezpečení pro správu klientských počítačů ve veřejné síti IBCM vyžaduje použití certifikátů PKI. Tato konfigurace zajišťuje, že připojení jsou ověřována nezávislou autoritou. Když klienti a servery lokality IBCM odesílají data, jsou šifrovaná a zabezpečená.  

## <a name="client-communications"></a>Komunikace s klientem

Následující role systému lokality v primárních lokalitách podporují připojení od klientů, kteří jsou v nedůvěryhodných umístěních:

> [!NOTE]
> I když se IBCM primárně zaměřuje na internetový scénář, stejné chování se vztahuje na klienty v nedůvěryhodné doménové struktuře služby Active Directory. Sekundární lokality nepodporují připojení klientů z nedůvěryhodných umístění.

- Bod registrace certifikátu pro modul zásad Configuration Manager (NDES)

- Distribuční bod

- Cloudový distribuční bod

- Zprostředkující bod registrace

- Bod záložního stavu

- Bod správy

- Bod aktualizace softwaru

> [!NOTE]
> Pro role katalogu aplikací s verzí 1910 byla ukončena podpora. Další informace najdete v tématu [Odebrání katalogu aplikací](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat). Pro Configuration Manager verze 1906 a starší, které stále podporují, může bod webu Katalog aplikací přijímat připojení z internetových klientů.

### <a name="about-internet-facing-site-systems"></a>Systémy internetových serverů

Neexistuje žádný požadavek na vztah důvěryhodnosti mezi doménovou strukturou klienta a serverem systému lokality. Pokud však doménová struktura, která obsahuje internetové systémy lokality, důvěřuje doménové struktuře obsahující uživatelské účty, tato konfigurace podporuje uživatelské zásady pro zařízení v Internetu, pokud povolíte nastavení klienta **zásady klienta** **Povolit žádosti o zásady uživatele od internetových klientů**.

Například následující konfigurace ilustruje, kdy IBCM podporuje uživatelské zásady pro zařízení v Internetu:

- Internetový bod správy je v hraniční síti. Tato síť má také řadič domény jen pro čtení k ověření uživatele. Brána firewall mezi hraničními a interními sítěmi umožňuje pakety služby Active Directory.

- Uživatelský účet je v doménové struktuře založené na intranetu. Internetový bod správy je v hraniční struktuře založené na hraniční síti. Hraniční struktura důvěřuje interní doménové struktuře. Brána firewall mezi hraničními a interními sítěmi povoluje ověřovací pakety.

- Uživatelský účet a internetový bod správy jsou v doménové struktuře založené na intranetu. Bod správy publikujete na Internet pomocí webové proxy server.

### <a name="use-a-web-proxy-server"></a>Použití webové proxy server

Internetové systémy lokality můžete umístit do intranetu, když je publikujete na Internet pomocí webové proxy server. Tyto systémy lokality konfigurujte pro klientská připojení pouze z Internetu, nebo připojení klientů z Internetu a intranetu. Pokud používáte web proxy server, můžete ho nakonfigurovat pro přemostění SSL (Secure Sockets Layer) (SSL) do tunelového propojení SSL nebo SSL.

#### <a name="ssl-bridging-to-ssl"></a>Přemostění SSL do SSL

Přemostění SSL do SSL je doporučená a bezpečnější konfigurace, protože používá ukončení protokolu SSL s ověřením. Ověřuje klientské počítače pomocí ověřování počítače. Mobilní zařízení, která zapíšete pomocí Configuration Manager, nepodporují přemostění SSL.

Při ukončení SSL u proxy serveru kontroluje pakety z Internetu, než je přepošle interní síti. Proxy ověří připojení z klienta, ukončí ho a pak otevře nové ověřené připojení k internetovým systémům lokality. Když Configuration Manager klienti používají proxy server, klient bezpečně obsahuje svou identitu (GUID) v datové části paketu. Bod správy nebere v úvahu, že proxy server je klient. Configuration Manager nepodporuje přemostění s protokolem HTTP na HTTPS nebo z HTTPS na HTTP.

> [!NOTE]
> Configuration Manager nepodporuje nastavování konfigurací přemostění SSL od jiných dodavatelů. Například Citrix NetScaler nebo F5 BIG-IP. Pokud chcete nakonfigurovat použití s Configuration Manager, obraťte se na dodavatele zařízení.

#### <a name="tunneling"></a>Tunelové propojení

Pokud váš webový proxy server nepodporuje požadavky na přemostění SSL, Configuration Manager podporuje také tunelování SSL. Tunelové propojení SSL můžete použít také k podpoře mobilních zařízení zaregistrovaných ve službě Configuration Manager. Jedná se o méně bezpečnou možnost, protože proxy předávají pakety SSL z Internetu do systémů lokality bez ukončení protokolu SSL. Proxy nekontroluje pakety pro škodlivý obsah. Pokud používáte tunelové připojení protokolu SSL, neexistují žádné požadavky na certifikáty proxy webového serveru.

## <a name="plan-for-internet-based-clients"></a>Plánování internetových klientů

Rozhodněte, jestli chcete nakonfigurovat internetové klienty pro správu na intranetu i internetu, nebo jenom na internetovou správu klientů. Tuto možnost správy můžete nakonfigurovat pouze při instalaci klienta. Pokud ho chcete později změnit, přeinstalujte klienta.

> [!NOTE]
> Pokud nakonfigurujete bod správy pro podporu internetových klientů, klienti, kteří se k tomuto bodu správy připojí, se budou moci připojit k Internetu, když budou příště aktualizovat seznam dostupných bodů správy.
>
> Konfiguraci pouze internetové správy klientů nemusíte omezovat na Internet. Můžete ho také použít na intranetu.

Klienti, u kterých nakonfigurujete jenom internetovou správu, komunikují pouze se systémy lokality, které nakonfigurujete pro připojení klientů z Internetu. Tuto konfiguraci použijte v následujících případech:

- U počítačů, u kterých víte, že se nikdy nepřipojíte k intranetu. Například počítače prodejního bodu ve vzdálených umístěních.
- Omezení komunikace klientů pouze s protokolem HTTPS. Například pro podporu brány firewall a omezených zásad zabezpečení.
- Když nainstalujete internetové systémy lokality do hraniční sítě a chcete tyto servery spravovat jako Configuration Manager klienty.

> [!NOTE]
> Chcete-li spravovat klienty pracovní skupiny na internetu, nainstalujte je jako pouze Internet.
>
> Když nakonfigurujete mobilní zařízení na použití internetového bodu správy, automaticky se nakonfiguruje jenom jako Internet.

Můžete nakonfigurovat ostatní klienty pro správu internetových klientů i intranetu. Když zjistí změnu sítě, automaticky přepnou mezi IBCM a intranetovou správou klientů. Pokud tito klienti mohou vyhledat a připojit se k bodu správy, který podporuje připojení klientů v intranetu, budou tito klienti spravováni jako klienti v intranetu. Intranetové klienty mají plnou funkčnost Configuration Manager. Pokud klienti nemůžou najít nebo se připojit k bodu správy, který podporuje připojení klientů v intranetu, pokusí se připojit k internetovému bodu správy. Pokud tato akce proběhne úspěšně, budou tito klienti spravováni internetovými systémy lokality v přiřazené lokalitě.

Výhodou automatického přepínání je, že klienti můžou používat všechny funkce, když se připojí k intranetu, a získají základní správu, když jsou na internetu. Stahování obsahu, které začíná na internetu, může bezproblémově pokračovat na intranetu a druhý způsob.

## <a name="prerequisites"></a>Požadavky

IBCM v Configuration Manager má následující závislosti:

- Klienti vyžadují připojení k Internetu. Configuration Manager používá stávající připojení k Internetu v zařízení. Mobilní zařízení musí mít přímé připojení k Internetu. Úplnými klientskými počítači může být přímé připojení k Internetu nebo připojení pomocí proxy webového serveru.

- Systémy lokality, které podporují IBCM, vyžadují připojení k Internetu a musí se nacházet v doméně služby Active Directory. Internetové systémy lokality nevyžadují důvěryhodný vztah s doménovou strukturou služby Active Directory serveru lokality. Pokud však internetový bod správy může ověřit uživatele pomocí ověřování systému Windows, podporuje zásady uživatele. Pokud ověřování systému Windows neproběhne úspěšně, podporuje pouze zásady zařízení.

    > [!NOTE]
    > Pokud chcete podporovat zásady uživatele, ve skupině **zásad klienta** povolte taky následující nastavení klienta:
    >
    > - **Povolit zásady uživatele u klientských počítačů**
    > - **Povolit žádosti o zásady uživatele od internetových klientů**  

- Infrastruktura veřejných klíčů (PKI) pro nasazení a správu požadovaných certifikátů pro internetové klienty a servery systému lokality. Další informace najdete v tématu [požadavky na certifikát PKI](../../plan-design/network/pki-certificate-requirements.md).

- Zaregistrujte veřejné položky hostitele DNS pro plně kvalifikované názvy domén (FQDN) pro všechny systémy lokality, které podporují IBCM.

### <a name="client-communication-requirements"></a>Požadavky na komunikaci klienta

Použité brány firewall nebo proxy servery musí umožňovat komunikaci klienta s internetovými systémy lokality:

- Podpora HTTP 1.1  

- Umožňuje obsah typu HTTP přílohy MIME s více částmi (více částí / smíšená a aplikace / osminásobný proud)  

#### <a name="verbs"></a>Příkazy

Pro role webového serveru systému lokality Povolte následující příkazy:

| Role | Příkazy |
|------|-------|
| Bod správy | – HEAD<br>-CCM_POST<br>-BITS_POST<br>– GET<br>-PROPFIND |
| Distribuční bod | – HEAD<br>– GET<br>-PROPFIND |
| Bod záložního stavu | POST |
| Bod webu Katalog aplikací | – POST<br>– ZÍSKAT |

#### <a name="http-headers"></a>Hlavičky protokolu HTTP

Pro role webového serveru systému lokality Povolte následující hlavičky protokolu HTTP:

| Role | Hlavičky protokolu HTTP |
|------|--------------|
| Bod správy | Oblasti<br>- CCMClientID:<br>- CCMClientIDSignature:<br>- CCMClientTimestamp:<br>- CCMClientTimestampsSignature: |
| Distribuční bod | Rozsah: |

Podobné požadavky na komunikaci při použití bodu aktualizace softwaru pro připojení klientů z internetu najdete v dokumentaci ke službě Windows Server Update Services (WSUS).

## <a name="unsupported-features"></a>Nepodporované funkce

Ne všechny funkce správy klientů jsou vhodné pro Internet. Configuration Manager nepodporuje některé funkce pro klienty na internetu. Tyto nepodporované funkce se obvykle spoléhají na Active Directory Domain Services nebo nejsou vhodné pro veřejnou síť.

Následující funkce nejsou podporované, když spravujete klienty na internetu pomocí IBCM:

- Nasazení klientů prostřednictvím Internetu, jako je například nabízená instalace klienta a nasazení klienta na základě aktualizace softwaru. Použijte ruční instalaci klienta.

- Automatické přiřazení lokality

- Funkce Wake-on-LAN

- Nasazení operačního systému. Můžete ale nasadit pořadí úloh, která neimplementují operační systém.

- Vzdálené řízení

- Nasazení softwaru pro uživatele. Tato funkce se spoléhá na katalog aplikací, který je zastaralý.

- Roaming klienta. Roaming umožňuje klientům vždy nalézt nejbližší distribuční body pro stahování obsahu. Klienti bez deterministického výběru jednoho z internetových systémů lokality bez ohledu na šířku pásma nebo fyzického umístění.

Když nakonfigurujete bod aktualizace softwaru tak, aby přijímal připojení z Internetu, internetoví klienti vždy prohledají v tomto bodu aktualizace softwaru, aby zjistili, které aktualizace softwaru jsou nutné. Pokud jsou tito klienti připojeni k Internetu, pokusí se nejprve stáhnout softwarové aktualizace z Microsoft Update, nikoli z internetového distribučního bodu. Pokud toto chování neproběhne úspěšně, pokusí se stáhnout požadované softwarové aktualizace z internetového distribučního bodu.

> [!TIP]
> Klient Configuration Manager automaticky určí, zda je na intranetu nebo Internetu. Pokud klient může kontaktovat řadič domény nebo místní bod správy, nastaví jeho typ připojení na "aktuálně *intranet*". V opačném případě se přepne na "aktuálně *Internet*" a komunikuje se systémy lokality, které jsou přiřazené ke své lokalitě.
