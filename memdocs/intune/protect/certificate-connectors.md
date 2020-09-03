---
title: Konektory certifikátů C pro Microsoft Intune – Azure | Microsoft Docs
description: Přečtěte si o certifikátech Certificate Connectors pro Simple Certificate Enrollment Protocol (SCEP) nebo PKCS (Public Key Cryptography Standards) a profilů certifikátů s Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9f891e7989ad3f0f8d798dd9a5f0207a19ac5b95
ms.sourcegitcommit: b95eac00a0cd979dc88be953623c51dbdc9327c5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/03/2020
ms.locfileid: "89428878"
---
# <a name="certificate-connectors-for-microsoft-intune"></a>Konektory certifikátů pro Microsoft Intune

Aby bylo možné podporovat používání certifikátů pro ověřování a podepisování a šifrování e-mailů pomocí S/MIME, vyžaduje Intune použití Certificate Connectoru. Certificate Connector je software, který nainstalujete na místní server. Konektor umožňuje zařízením spravovaným v cloudu zřídit certifikáty z místní infrastruktury, jako je vydávající certifikační autorita.

Tento článek popisuje dostupné konektory, jejich životní cyklus, předpoklady pro použití a informace o tom, jak je udržovat v aktuálním stavu.  

## <a name="available-connectors"></a>Dostupné konektory

Pro Intune jsou k dispozici dvě konektory certifikátů. Každá z nich má vlastní použití a požadavky.

### <a name="pfx-certificate-connector-for-microsoft-intune"></a>Konektor certifikátu PFX pro Microsoft Intune

**Certificate Connector Connector** podporuje nasazení certifikátů pro PCKS #12 žádosti o certifikát a zpracovává žádosti o soubory PFX importované do Intune pro šifrování e-mailu s/MIME pro konkrétního uživatele.

> [!TIP]
> Před aktualizací ze srpna pro tento konektor byly žádosti o certifikát PKCS #12 zpracovány *konektorem Intune Certificate Connector*. V případě aktualizace ze srpna byly funkce pro všechny žádosti o certifikát PKCS konsolidovány v *konektoru certifikátů PFX*, který podporuje automatické aktualizace konektoru na nové verze a vyžaduje použití .NET Framework verze 4.7.2.
>
> Funkce konektoru Microsoft Intune není zastaralá a je možné ji dál používat s profily certifikátů PKCS. Pokud ale protokol SCEP nepoužíváte nebo jinak nepožadujete použití NDES, můžete přepnout na konektor certifikátů PFX a odebrat NDES z vašich serverů. 

**Konektor certifikátu PFX**:

- Podporuje několik instancí tohoto konektoru pro každého tenanta Intune. Každá instance konektoru musí být nainstalována na Windows Server a musí mít přístup k privátnímu klíči, který slouží k šifrování hesel nahraných souborů PFX.
- Dá se nainstalovat na stejný server, který je hostitelem instance *konektoru Microsoft Intune*.
- Podporuje [Automatické aktualizace](#automatic-update) nových verzí. Aby bylo možné automaticky instalovat nové verze, musí počítač, který je hostitelem konektoru, kontaktovat **AutoUpdate.msappproxy.NET** na portu **443**. Pokud se konektoru nepovede automaticky aktualizovat, můžete konektor aktualizovat ručně.
- Podporuje odvolání certifikátu (vyžaduje spuštění konektoru verze **6.2008.60.607** nebo novější).
- Má stejné požadavky na síť jako [spravovaná zařízení](../fundamentals/intune-endpoints.md#access-for-managed-devices)

  Další informace najdete v tématu [koncové body sítě pro Microsoft Intune](../fundamentals/intune-endpoints.md)a [požadavky na konfiguraci sítě a šířku pásma Intune](../fundamentals/network-bandwidth-use.md).

**Server Windows, na kterém konektor nainstaluje**:

- Musí používat Windows Server 2012 R2 nebo novější.
- Spusťte rozhraní .NET 4.7.2 Framework.  

**Postup instalace konektoru certifikátů PFX**:

Pokyny k instalaci tohoto konektoru najdete v tématu [stažení, instalace a konfigurace konektoru certifikátů PFX](certficates-pfx-configure.md).

### <a name="microsoft-intune-connector"></a>Konektor Microsoft Intune

**Konektor Microsoft Intune** se někdy označuje jako *Microsoft Intune Certificate Connector*. Tento konektor podporuje nasazení certifikátů, pokud používáte *Simple Certificate Enrollment Protocol* (SCEP) a máte certifikační autoritu (CA) služby AD CS (Active Directory Certificate Services). Tento typ certifikační autority se také označuje jako *certifikační autorita společnosti Microsoft*.

Pokud používáte SCEP s certifikační autoritou Microsoftu, musíte také nakonfigurovat **službu zápisu síťových zařízení** (NDES). Z tohoto důvodu se tento konektor často označuje jako *konektor pro NDES Certificate Connector*.

Pokud používáte [certifikační autoritu třetí strany](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration), nemusíte používat tento konektor a NDES se nevyžaduje.

**Konektor Microsoft Intune**:

- Nainstaluje se na Windows Server, který může také hostovat instanci *konektoru certifikátů PFX*.
- Podporuje až 100 instancí tohoto konektoru na každého tenanta, přičemž každá instance je na samostatném Windows serveru. Pokud používáte více konektorů:
  - Všechny instance *konektoru Microsoft Intune* ve vašem prostředí by měly mít stejnou verzi.
  - Vaše infrastruktura podporuje redundanci a vyrovnávání zatížení, protože kterákoli dostupná instance konektoru může zpracovávat žádosti o certifikát.
- Pro instalaci nové verze konektoru je nutné provést [Ruční aktualizaci](#manual-update) . Ruční aktualizace vyžaduje odinstalaci aktuálního konektoru a instalaci nové verze konektoru. Další akce by se neměly vyžadovat.
- Podporuje režim FIPS ( *Federal Information Processing Standard* ). FIPS se nevyžaduje. Pokud je povolený Standard FIPS, můžete vystavit a odvolat certifikáty.
- Má stejné požadavky na síť jako [spravovaná zařízení](../fundamentals/intune-endpoints.md#access-for-managed-devices).

  Další informace najdete v tématu [koncové body sítě pro Microsoft Intune](../fundamentals/intune-endpoints.md)a [požadavky na konfiguraci sítě a šířku pásma Intune](../fundamentals/network-bandwidth-use.md).

**Server Windows, na kterém konektor nainstaluje**:

- Musí používat Windows Server 2012 R2 nebo novější.
- Spusťte rozhraní .NET 4,5. Když se tento konektor nainstaluje na stejný server jako *konektor certifikátu PFX*, musíte použít .NET 4.7.2 Framework, který je vyžadován konektorem PFX.
- Nemůže se jednat o stejný server, který je hostitelem vydávající certifikační autority (CA).
- Při použití pro SCEP s certifikační autoritou Microsoftu vyžaduje přístup k serveru, na kterém běží NDES. Služba NDES běží na Windows serveru a může běžet na stejném serveru jako tento konektor.

**Když se vyžaduje NDES**:

- [Na serveru, který je hostitelem NDES](/previous-versions/windows/it-pro/windows-server-2003/cc775800(v=ws.10)) , a serveru, který je hostitelem *konektoru Microsoft Intune*, musí být vypnutá konfigurace rozšířeného zabezpečení aplikace Internet Explorer.
- Konektor vyžaduje ke komunikaci se službou NDES další konfigurace. Postupy pro instalaci a konfiguraci služby NDES najdete v postupech pro instalaci *konektoru Microsoft Intune*.

  Další informace o NDES najdete v tématu [pokyny pro službu zápisu síťových zařízení](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v=ws.11)).

**Postup instalace konektoru Microsoft Intune**:

Pokyny k instalaci tohoto konektoru najdete v tématu [Konfigurace infrastruktury pro podporu protokolu SCEP s Intune](certificates-scep-configure.md).

## <a name="connector-lifecycle"></a>Životní cyklus konektoru

Aktualizované verze konektorů certifikátů jsou pravidelně vydané. Oznámení pro nové verze konektoru se zobrazí v části (co je nového) (.. /Fundamentals/whats-new.MD) pro Intune a v části [co je nového pro konektory](#whats-new-for-connectors) na konci tohoto článku.

Při vydání nových verzí je podpora pro předchozí verzi zastaralá s omezeným obdobím odkladu pro jejich pokračující používání. Po uplynutí období odkladu bude podpora pro tuto nepoužívané verze ukončena a může kdykoli přestat fungovat. Doba odkladu je šest měsíců.

Naplánujte aktualizaci konektoru na nejnovější verzi při první příležitosti. Každý konektor má jinou cestu aktualizace:

- **PFX Certificate Connector pro Microsoft Intune** – podporuje automatické aktualizace.
- **Microsoft Intune Connector** – vyžaduje ruční aktualizaci.

### <a name="automatic-update"></a>Automatická aktualizace

Když to podporuje typ konektoru a vaše prostředí, může Intune automaticky aktualizovat konektor na nejnovější verzi, a to krátce po vydání této verze konektoru.  

Pro automatické aktualizace musí server, který je hostitelem konektoru, přistupovat ke **službě Azure Update**:

- Port: **443**
- Koncový bod: **AutoUpdate.msappproxy.NET**

Pokud brány firewall, infrastruktury nebo konfigurace sítě omezují přístup pro automatické aktualizace, vyřešte problémy s blokováním nebo ručně aktualizujte konektor na novou verzi.

### <a name="manual-update"></a>Ruční aktualizace

Postup ruční aktualizace Certificate Connectoru je stejný pro přeinstalaci konektoru.

Certificate Connector můžete ručně aktualizovat i v případě, že podporuje automatické aktualizace. Konektor můžete například ručně aktualizovat, pokud vaše konfigurace sítě blokuje automatickou aktualizaci.  

### <a name="to-reinstall-a-certificate-connector"></a>Přeinstalování Certificate Connectoru

1. V systému Windows Server, který je hostitelem konektoru, odinstalujte konektor pomocí **aplikací a funkcí systému Windows** .

2. Chcete-li nainstalovat novou verzi, postupujte podle pokynů pro instalaci nové verze konektoru. Nezapomeňte při instalaci novější verze konektoru zkontrolovat všechny nové nebo aktualizované požadavky:
   - SCEP: [Konfigurace infrastruktury pro podporu protokolu SCEP s Intune](certificates-scep-configure.md)
   - PKCS: [Stáhněte, nainstalujte a nakonfigurujte Certificate Connector PFX pro Microsoft Intune](certficates-pfx-configure.md)

## <a name="connector-status-and-version"></a>Stav a verze konektoru

V centru pro správu Microsoft Endpoint Manageru můžete vybrat Certificate Connector pro zobrazení informací o jeho stavu a potvrzení jeho verze:

1. Přihlaste se do [centra pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) .

2. Přejdete na konektory **pro správu tenanta**  >  **a tokeny**  >  **certifikátů**.

3. Vyberte konektor pro zobrazení jeho stavu.

Při zobrazení stavu konektoru:

- Zastaralé konektory se zobrazí s **upozorněním**. Po uplynutí šestiměsíční lhůty se upozornění změní na chybu.
- Konektory, které přesahují dobu odkladu, zobrazují chybu. Tyto konektory už nejsou podporované a můžou se kdykoli přestat pracovat.

## <a name="whats-new-for-connectors"></a>Co je nového u konektorů

Aktualizace pro dvě konektory certifikátů jsou vydávány pravidelně. Když aktualizujeme konektor, můžete si přečíst o těchto změnách.

### <a name="pfx-certificate-connector-release-history"></a>Historie verzí konektoru certifikátů PFX

*Konektor certifikátu PFX pro Microsoft Intune* [podporuje automatické aktualizace](#automatic-update).

#### <a name="august-26-2020"></a>26. srpna 2020

**6.2008.60.607 verze** – změny v této verzi:

- Vyžaduje .NET Framework verze 4.7.2
- Nahrazuje použití *konektoru Microsoft Intune* pro použití s profily certifikátů PKCS. *Konektor PFX Certificate Connector* je teď jediným konektorem vyžadovaným pro použití PCKS #12 nebo importovaných certifikátů PFX.
- Přidá podporu pro používání profilů certifikátů PKCS se všemi podporovanými platformami kromě Windows 8.1.
- Přidá podporu pro odvolání certifikátu pro Outlook S/MIME.

#### <a name="november-18-2019"></a>18. listopadu 2019

**Verze: 6.1911.11.602** -změny v této verzi:

- Přidala se podpora S/MIME pro import PFX.  

#### <a name="may-17-2019"></a>17. května 2019

**6.1905.0.404 verze** – změny v této verzi:

- Opravili jsme problém, kdy se stávající certifikáty PFX budou dál zpracovávat, což způsobí, že konektor přestane zpracovávat nové požadavky. 

#### <a name="may-6-2019"></a>6. května 2019

**6.1905.0.402 verze** – změny v této verzi:

- Interval dotazování konektoru se zkracuje z 5 minut na 30 sekund.

#### <a name="april-2-2019"></a>2\. dubna 2019

**6.1904.0.401 verze** – změny v této verzi:

- Tento konektor teď podporuje automatickou aktualizaci.
- Opravili jsme problém, kdy se konektoru nepodaří zaregistrovat se do Intune po přihlášení ke konektoru s globálním účtem správce.

### <a name="microsoft-intune-connector-release-history"></a>Historie vydaných verzí konektoru Microsoft Intune

#### <a name="april-2-2019"></a>2\. dubna 2019

**6.1904.1.0 verze** – změny v této verzi:  

- Opravili jsme problém, kdy se konektoru nepodaří zaregistrovat se do Intune po přihlášení ke konektoru s globálním účtem správce.
- Zahrnuje opravy spolehlivosti při odvolání certifikátu.
- Zahrnuje opravy výkonu, které zvyšují rychlost zpracování požadavků certifikátů PKCS.

## <a name="next-steps"></a>Další kroky

Pro každou platformu, kterou chcete použít, vytvořte profily certifikátů importované pomocí protokolu SCEP, PKCS nebo PKCS. Chcete-li pokračovat, přečtěte si následující články:

- [Konfigurace infrastruktury pro podporu certifikátů SCEP pomocí Intune](certificates-scep-configure.md)  
- [Konfigurace a správa certifikátů PKCS pomocí Intune](certficates-pfx-configure.md)  
- [Vytvoření importovaného profilu certifikátu PKCS](certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)
