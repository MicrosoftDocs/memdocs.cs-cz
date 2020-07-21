---
title: Rozhraní API k zaregistrování certifikačních autorit třetích stran
titleSuffix: Microsoft Intune
description: Přidejte nebo integrujte řešení GitHubu SCEP pro externí certifikační autority (CA), abyste mohli vydávat zařízením v Microsoft Intune certifikáty SCEP. Toto řešení zahrnuje rozhraní API jazyka Java a C#, která provádí ověřování, odesílají oznámení o úspěchu a neúspěchu do Intune a při komunikaci s Intune používají objekt pro vytváření soketu SSL. Taky se můžete podívat na přehled kroků k testování konfigurace certifikační autority SCEP.
keywords: ''
author: Brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/06/2018
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 16b212bde0f46861b8acb1470588b784c6f2a7fb
ms.sourcegitcommit: d3992eda0b89bf239cea4ec699ed4711c1fb9e15
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/21/2020
ms.locfileid: "86565661"
---
# <a name="use-apis-to-add-third-party-cas-for-scep-to-intune"></a>Použití rozhraní API k přidání externích certifikačních autorit pro SCEP do Intune

V Microsoft Intune můžete přidat externí certifikační autority (CA) a nechat je vystavovat a ověřovat certifikáty pomocí protokolu SCEP (Simple Certificate Enrollment Protocol). Článek o [přidání externí certifikační autority](certificate-authority-add-scep-overview.md) obsahuje základní informace o této funkci a popisuje úlohy správce v Intune.

Existují i úlohy pro vývojáře používající open-source knihovnu, kterou Microsoft publikoval na GitHub.com. Tato knihovna obsahuju rozhraní API, které:

- ověří heslo SCEP dynamicky vygenerované službou Intune,
- upozorní Intune na certifikáty vytvořené na zařízeních odesílajících žádosti protokolu SCEP.

Pomocí tohoto rozhraní API se váš externí server SCEP integruje s řešením pro správu Intune SCEP pro zařízení MDM. Knihovna odděluje od uživatelů aspekty, jako je ověřování, umístění služby nebo rozhraní ODATA Intune Service API.

## <a name="scep-management-solution"></a>Řešení pro správu SCEP

![Způsob integrace externí certifikační autority SCEP s Microsoft Intune](./media/scep-libraries-apis/scep-certificate-vendor-integration.png)

Správci pomocí Intune vytvoří profily SCEP a potom tyto profily přiřadí zařízením MDM. Profily SCEP zahrnují například tyto parametry:

- adresa URL serveru SCEP
- důvěryhodný kořenový certifikát certifikační autority
- atributy certifikátu a další

Zařízením, která se vrátí se změnami do služby Intune, se přiřadí profil SCEP a pak se pomocí těchto parametrů nakonfigurují. Intune vytvoří dynamicky generovanou výzvu heslem SCEP a pak ji přiřadí k zařízení.

Tato výzva obsahuje:

- Dynamicky generovanou výzvu heslem
- Podrobnosti o parametrech očekávaných v žádosti o podepsání certifikátu, kterou zařízení vydává serveru SCEP
- Dobu vypršení platnosti výzvy

Intune tyto informace zašifruje, podepíše zašifrovaný objekt blob a potom tyto podrobnosti zabalí do výzvy heslem SCEP.

Zařízení, která kontaktují server SCEP kvůli vyžádání certifikátu, potom tuto výzvu heslem SCEP předají. Server SCEP odešle žádost o podepsání certifikátu a šifrovanou výzvu heslem SCEP do Intune k ověření.  Aby server SCEP certifikát do zařízení vydal, musí výzva heslem a žádost o podepsání certifikátu projít ověřením. Po ověření výzvy SCEP proběhnou následující kontroly:


- Ověří se podpis zašifrovaného objektu blob.
- Ověří se, že nevypršela platnost výzvy.
- Ověří se, že daný profil stále cílí na dané zařízení.
- Ověří se, že vlastnosti certifikátu požadované zařízením v žádosti o podepsání certifikátu odpovídají očekávaným hodnotám.

Řešení pro správu SCEP obsahuje také generování sestav. Správce může získat informace o stavu nasazení profilu SCEP a o certifikátech vydaných zařízením.

## <a name="integrate-with-intune"></a>Integrace s Intune

Kód pro integrování knihovny se službou Intune SCEP je k dispozici ke stažení v [úložišti GitHub Microsoft/Intune-Resource-Access](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/CsrValidation).

Integrování knihovny do vašich produktů se provádí následovně. K dokončení toho postupu musíte umět pracovat s úložišti GitHub a vytvářet řešení a projekty v sadě Visual Studio.

1. Zaregistrujte si příjímání oznámení z úložiště.
2. Uložiště naklonujte nebo stáhněte.
3. Přejděte na požadovanou implementaci knihovny ve složce `\src\CsrValidation` (https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/CsrValidation).
4. Knihovnu sestavte podle pokynů v souboru README.
5. Zahrňte knihovnu do projektu, který vytvoří váš server SCEP.
6. Na server SCEP proveďte následující úlohy:

   - Umožněte správci nakonfigurovat [identifikátor aplikace Azure, klíč aplikace Azure a ID tenanta](#onboard-scep-server-in-azure) (v tomto článku), které knihovna používá k ověřování. Správci by měli mít možnost klíč aplikace Azure aktualizovat.
   - Identifikujte žádosti SCEP, které obsahují heslo SCEP vygenerované v Intune.
   - K ověření hesel SCEP vygenerovaných v Intune použijte knihovnu **rozhraní API pro ověření požadavku**.
   - Použijte knihovnu rozhraní API pro oznámení, abyste Intune informovali o certifikátech vydaných pro požadavky SCEP, které mají hesla SCEP vygenerovaná v Intune. Informujte Intune také o chybách, které mohou při zpracování těchto požadavků SCEP nastat.
   - Zkontrolujte, že server protokoluje dostatek informací, aby správci mohli řešit potíže.

7. Dokončete [testování integrace](#integration-testing) (v tomto článku) a vyřešte případné problémy.
8. Poskytněte zákazníkovi písemné pokyny vysvětlující:

   - způsob nasazení serveru SCEP na web Azure Portal,
   - způsob získání identifikátoru aplikace Azure a klíče aplikace Azure, které jsou potřeba ke konfiguraci knihovny.

### <a name="onboard-scep-server-in-azure"></a>Nasazení serveru SCEP v Azure

K ověření ve službě Intune potřebuje server SCEP ID aplikace Azure, klíč aplikace Azure a ID tenanta. Server SCEP vyžaduje ještě oprávnění pro přístup k rozhraní Intune API.

K získání těchto dat se správce serveru SCEP musí přihlásit k webu Azure Portal, zaregistrovat aplikaci, poskytnout aplikaci oprávnění k **ověření výzvy rozhraní Microsoft Intune API nebo SCEP** a vytvořit pro danou aplikaci klíč. Potom si bude moct ID aplikace, její klíč a ID tenanta stáhnout.

Pokyny k registraci aplikace a získání ID a klíčů najdete v tématu o [použití webu Azure Portal k vytvoření aplikace a instančního objektu AAD pro přístup k prostředkům](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal).

### <a name="java-library-api"></a>Rozhraní API knihovny Java

Knihovna Java se implementuje jako projekt Maven, který své závislosti získává při sestavení. Rozhraní API se implementuje pod oborem názvů `com.microsoft.intune.scepvalidation` třídy `IntuneScepServiceClient`.

#### <a name="intunescepserviceclient-class"></a>Třída IntuneScepServiceClient

Třída `IntuneScepServiceClient` obsahuje metody používané službou SCEP k ověřování hesel SCEP, informování Intune o vytvořených certifikátech a vypisování případných chyb.

##### <a name="intunescepserviceclient-constructor"></a>Konstruktor IntuneScepServiceClient

**Podpis**:

```java
IntuneScepServiceClient(
    Properties configProperties)
```

**Popis**:

Vytvoří instanci a nakonfiguruje objekt `IntuneScepServiceClient`.

**Parametry**:

- **configProperties** – objekt vlastnosti obsahující informace o konfiguraci klienta

Konfigurace musí obsahovat následující vlastnosti:

- AAD_APP_ID="ID aplikace Azure získané během procesu nasazení"
- AAD_APP_KEY="klíč aplikace Azure získaný během procesu nasazení"
- TENANT="ID tenanta získané během procesu nasazení."
- PROVIDER_NAME_AND_VERSION="informace sloužící k identifikaci produktu a jeho verze"

Pokud vaše řešení vyžaduje proxy (s ověřováním nebo bez něj), přidejte následující vlastnosti:

- PROXY_HOST="Hostitel, který hostuje proxy."
- PROXY_PORT="Port, na kterém proxy naslouchá."
- PROXY_USER="Uživatelské jméno, které se použije, pokud proxy používá základní ověřování."
- PROXY_PASS="Heslo, které se použije, pokud proxy používá základní ověřování."

**Vyvolá**:

- **IllegalArgumentException** – vyvoláno, pokud je konstruktor proveden bez správného objektu vlastnosti.

> [!IMPORTANT]
> Doporučujeme vytvořit instanci této třídy a použít ji ke zpracování více žádostí protokolu SCEP. Sníží se tím režie, protože do mezipaměti ukládá ověřovací tokeny a informace o umístění služby.

**Poznámky k zabezpečení**  
Implementátor serveru SCEP musí chránit data zadaná do vlastností konfigurace, která se ukládají do úložiště, aby nedošlo k manipulaci nebo zpřístupnění informací. K zabezpečení informací se doporučuje použití vhodných seznamů řízení přístupu a vhodného šifrování.

##### <a name="validaterequest-method"></a>Metoda ValidateRequest

**Podpis**:

```java
void ValidateRequest(
    String transactionId,
    String certificateRequest)
```

**Popis**:

Ověřuje žádosti o certifikáty SCEP.

**Parametry**:

- **transactionId** – ID transakce SCEP
- **certificateRequest** -kódování PKCS #10 pro žádost o certifikát kódování Base64 jako řetězec

**Vyvolá**:

- **IllegalArgumentException** – vyvolána při volání s neplatným parametrem
- **IntuneScepServiceException** – vyvolána, pokud se zjistí, že žádost o certifikát není platná
- **Výjimka** – vyvolala se v případě, že došlo k neočekávané chybě.

> [!IMPORTANT]
> Výjimky vyvolané touto metodou by měl server zaprotokolovat. Všimněte si, že vlastnosti `IntuneScepServiceException` mají podrobné informace o tom, proč se ověření žádosti o certifikát nezdařilo.

**Poznámky k zabezpečení**:

- Pokud tato metoda vyvolá výjimku, server SCEP **nesmí** klientovi certifikát vydat.
- Chyby při ověřování žádosti o certifikát SCEP mohou značit potíže v infrastruktuře Intune. Nebo mohou znamenat, že se certifikát snaží získat útočník.

##### <a name="sendsuccessnotification-method"></a>Metoda SendSuccessNotification

**Podpis**:

```java
void SendSuccessNotification(
    String transactionId,
    String certificateRequest,
    String certThumbprint,
    String certSerialNumber,
    String certExpirationDate,
    String certIssuingAuthority)
```

**Popis**:

Upozorní Intune, že se jako součást zpracování požadavku SCEP vytvořil certifikát.

**Parametry**:

- **transactionId** – ID transakce SCEP
- **certificateRequest** -kódování PKCS #10 pro žádost o certifikát kódování Base64 jako řetězec
- **certThumprint** -SHA1 – hash kryptografický otisk zřízeného certifikátu
- **certSerialNumber** – sériové číslo zřízeného certifikátu
- **certExpirationDate** – datum vypršení platnosti zřízeného certifikátu. Řetězec datum a čas by měl být ve formátu webového času UTC (YYYY-MM-DDThh:mm:ss.sssTZD) podle normy ISO 8601.
- **certIssuingAuthority** – název autority, která certifikát vystavila

**Vyvolá**:

- **IllegalArgumentException** – vyvolána při volání s neplatným parametrem
- **IntuneScepServiceException** – vyvolána, pokud se zjistí, že žádost o certifikát není platná
- **Výjimka** – vyvolala se v případě, že došlo k neočekávané chybě.

> [!IMPORTANT]
> Výjimky vyvolané touto metodou by měl server zaprotokolovat. Všimněte si, že vlastnosti `IntuneScepServiceException` mají podrobné informace o tom, proč se ověření žádosti o certifikát nezdařilo.

**Poznámky k zabezpečení**:

- Pokud tato metoda vyvolá výjimku, server SCEP **nesmí** klientovi certifikát vydat.
- Chyby při ověřování žádosti o certifikát SCEP mohou značit potíže v infrastruktuře Intune. Nebo mohou znamenat, že se certifikát snaží získat útočník.

##### <a name="sendfailurenotification-method"></a>Metoda SendFailureNotification

**Podpis**:

```java
void SendFailureNotification(
    String transactionId,
    String certificateRequest,
    long  hResult,
    String errorDescription)
```

**Popis**:

Upozorní Intune, že při zpracování požadavku SCEP došlo k chybě. Tato metoda by se u výjimek vyvolaných metodami této třídy neměla vyvolávat.

**Parametry**:

- **transactionId** – ID transakce SCEP
- **certificateRequest** -kódování PKCS #10 pro žádost o certifikát kódování Base64 jako řetězec
- **hResult** – kód chyby Win32, který nejlépe popisuje chybu, ke které došlo. Viz [kódy chyb Win32](https://msdn.microsoft.com/library/cc231199.aspx).
- **errorDescription** – popis zjištěné chyby

**Vyvolá**:

- **IllegalArgumentException** – vyvolána při volání s neplatným parametrem
- **IntuneScepServiceException** – vyvolána, pokud se zjistí, že žádost o certifikát není platná
- **Výjimka** – vyvolala se v případě, že došlo k neočekávané chybě.

> [!IMPORTANT]
> Výjimky vyvolané touto metodou by měl server zaprotokolovat. Všimněte si, že vlastnosti `IntuneScepServiceException` mají podrobné informace o tom, proč se ověření žádosti o certifikát nezdařilo.

**Poznámky k zabezpečení**:

- Pokud tato metoda vyvolá výjimku, server SCEP **nesmí** klientovi certifikát vydat.
- Chyby při ověřování žádosti o certifikát SCEP mohou značit potíže v infrastruktuře Intune. Nebo mohou znamenat, že se certifikát snaží získat útočník.

##### <a name="setsslsocketfactory-method"></a>Metoda SetSslSocketFactory

**Podpis**:

```java
void SetSslSocketFactory(
    SSLSocketFactory factory)
```

**Popis**:

Pomocí této metody můžete informovat klienta, že při komunikaci s Intune musí používat zadaný objekt pro vytváření soketu SSL (místo výchozího).

**Parametry**:

- **Factory** – objekt pro vytváření soketů SSL, který by měl klient používat pro požadavky HTTPS

**Vyvolá**:

- **IllegalArgumentException** – vyvolána při volání s neplatným parametrem

> [!NOTE]
> Pokud se vyžaduje objekt pro vytváření soketu SSL, musí být nastavený před spuštěním ostatních metod této třídy.

## <a name="integration-testing"></a>Testování integrace

Ověřování a testování správné integrace vašeho řešení s Intune je nezbytné. Následující seznam uvádí přehled všech kroků:

1. Nastavte [zkušební účet Intune](../fundamentals/account-sign-up.md).
2. Nasaďte [server SCEP na webu Azure Portal](#onboard-scep-server-in-azure) (v tomto článku).
3. [Nakonfigurujte server SCEP](certificates-scep-configure.md) pomocí ID a klíčů vytvořených při nasazení serveru SCEP.
4. [Zaregistrujte zařízení](../enrollment/device-enrollment.md), abyste v [matici testování scénářů](https://github.com/Microsoft/Intune-Resource-Access/blob/develop/src/CsrValidation/doc/TestMatrix.csv) otestovali dané scénáře.
5. [Vytvořte profil důvěryhodných kořenových certifikátů](certificates-scep-configure.md) pro otestování certifikační autority.
6. Vytvořte profily SCEP, abyste v [matici testování scénářů](https://github.com/Microsoft/Intune-Resource-Access/blob/develop/src/CsrValidation/doc/TestMatrix.csv) otestovali uvedené scénáře.
7. [Přiřaďte profily](../configuration/device-profile-assign.md) uživatelům, kteří svá zařízení zaregistrovali.
8. Počkejte, než se zařízení s Intune synchronizují, nebo je [synchronizujte ručně](../remote-actions/device-sync.md).
9. Zkontrolujte, že profily důvěryhodných kořenových certifikátů a profily SCEP [jsou na daných zařízeních nasazené](../configuration/device-profile-monitor.md).
10. Zkontrolujte, že jsou důvěryhodné kořenové certifikáty nainstalované na všech zařízeních.
11. Zkontrolujte, že certifikáty SCEP pro přiřazené profily jsou nainstalované na všech zařízeních.
12. Zkontrolujte, že vlastnosti nainstalovaných certifikátů odpovídají vlastnostem nastaveným v profilu SCEP.
13. Zkontrolujte, že vydané certifikáty jsou v konzole Intune uvedené správně.

## <a name="see-also"></a>Viz také

- [Přidání přehledu externích certifikačních autorit](certificate-authority-add-scep-overview.md)
- [Nastavení Intune](../fundamentals/setup-steps.md)
- [Registrace zařízení](../enrollment/device-enrollment.md)
- [Vytvoření profilu certifikátu SCEP](certificates-profile-scep.md) (v tomto scénáři se nastavení Microsoft NDES Serveru ani Connectoru nepoužívá)
