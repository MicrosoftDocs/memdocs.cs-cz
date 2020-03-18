---
title: Vytvoření návrhu Microsoft Intune
titleSuffix: Microsoft Intune
description: Tento článek vám pomůže vytvořit a implementovat návrh cloudového řešení Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 3/22/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a8e38e29-f5e3-4a71-a170-d3b1a06e37c6
ms.reviewer: jeffbu, cgerth
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d29294f1d9556f195fe70f0e2cb36cc8c9ddcfba
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79331059"
---
# <a name="create-a-design"></a>Vytvoření návrhu

Návrh Intune vychází z informací, které shromáždíte, a rozhodnutí, která učiníte při čtení jiných [oddílů této příručky](planning-guide.md). Pomůže vám zkombinovat:

- Současné prostředí

- Možnosti nasazení Intune

- Požadavky na identitu u externích závislostí

- Informace o platformě zařízení

- Závazné požadavky  

I když existují minimální požadavky na místní infrastrukturu, plán návrhu je stále užitečný, abyste se ujistili, že máte správné řešení pro správu mobilních zařízení, které splňuje vaše cíle, cíle a požadavky.

Pojďme si projít každou z těchto oblastí podrobněji. 

## <a name="record-your-current-environment"></a>Popis současného prostředí
Kromě toho je běžné mít změny návrhu během fází implementace a testování. Použijte plán návrhu k dokumentaci těchto změn a jejich odůvodnění.

Vaše současné prostředí může ovlivnit rozhodování o návrhu a mělo by být zdokumentováno a popsáno, když činíte jiná rozhodnutí ohledně návrhu Intune. Tady je několik příkladů poznámek o současném prostředí:

- **Identita v cloudu**

  - Používáte DirSync nebo Azure Active Directory (Azure AD) Connect?

  - Je vaše prostředí federované?

  - Je aktivní vícefaktorové ověřování?

- **Prostředí e-mailu**

  - Používáte Exchange? Jedná se o místní nebo cloudové nasazení?

  - Probíhá u vás projekt migrace Exchange do cloudu?

- **Současné řešení správy mobilních zařízení (MDM)**

  - Používáte v současnosti nějaká jiná řešení MDM?

  - Jaká řešení MDM používáte ve scénářích použití firemních zařízení a ve scénářích BYOD?

  - Jaké používáte funkce (například aplikace, nastavení zařízení, konfigurace Wi-Fi)?

  - Jaké platformy zařízení jsou podporované?

  - Jaké skupiny a kolik uživatelů používá řešení MDM?

- **Řešení pro certifikáty**

  - Implementovali jste řešení pro certifikáty?

  - Jaké typy certifikátů používáte?

- **Správa systémů**

  - Jak spravujete počítačové a serverové prostředí?

  - Používáte Microsoft Endpoint Configuration Manager? Používáte platformu pro správu systémů od jiného výrobce?

- **Řešení VPN**

  - Jaké máte řešení VPN?

  - Používáte ho ve scénářích použití firemních zařízení i ve scénářích BYOD?

Při popisu současného prostředí MDM nezapomeňte zaznamenat všechny projekty nebo jakékoli jiné plány, které by mohly vaše prostředí ovlivnit. Následující příklad ukazuje, jak při vytváření návrhu Intune můžete popsat současné prostředí:

| **Oblast řešení** | **Současné prostředí** | **Komentář** |
|---|---|---|
| **Identita** | Azure AD, Azure AD Connect, nefederované, bez MFA | Probíhá projekt, který umožní koncem roku začít používat MFA. |                 
| **Prostředí e-mailu** | Místní Exchange, Exchange Online | V současnosti se místní Exchange migruje na Exchange Online. Už je migrovaných 75 % poštovních schránek. Zbývajících 25 % bude migrováno do začátku pilotního nasazení Intune. |                
| **SharePoint** | Místní SharePoint | Plány přechodu na SharePoint Online neexistují. |  
| **Současné řešení MDM** | Exchange ActiveSync |  |
| **Řešení pro certifikáty** | Microsoft Server 2012 R2, AD Certificate Services | Infrastruktura veřejných klíčů se používá jen pro webové servery. |
| **Správa systému** | Configuration Manager aktuální větev | Chcete prozkoumat řešení spolusprávy |
| **Řešení VPN** | Cisco AnyConnect |  |


Můžete si [stáhnout šablonu výše uvedené tabulky](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) a použít ji k vypracování vlastního plánu návrhu Intune.

## <a name="intune-tenant-location"></a>Umístění tenanta Intune

Pokud máte globální působnost, nezapomeňte při zřizování předplatného služby naplánovat, kde se bude nacházet tenant. Země nebo oblast se definuje při prvním přihlášení k předplatnému Intune a mapování na země nebo oblasti po celém světě, které jsou uvedené níže:

- Severní Amerika

- Evropa, Střední východ a Afrika

- Asie a Tichomoří

>[!IMPORTANT]
> Později není možné změnit zemi nebo oblast a umístění tenanta.

## <a name="external-dependencies"></a>Externí závislosti

Externí závislosti jsou služby a produkty, které jsou oddělené od Intune, ale tato služba je vyžaduje nebo jsou do ní integrované. Je důležité určit požadavky na vnější závislosti a jak je nakonfigurovat. Zde je několik příkladů nejčastějších externích závislostí:

- Identita

- Skupiny uživatelů a zařízení

- Infrastruktura veřejných klíčů (PKI)

V následující části podrobněji prozkoumáme tyto běžné externí závislosti.

### <a name="identity"></a>Identita

Identita představuje způsob identifikace uživatelů, kteří patří do organizace a zaregistrují si zařízení. Intune vyžaduje, aby identitu uživatelů poskytovala služba Azure Active Directory (Azure AD). Pokud tuto službu už používáte, můžete použít svou existující identitu, kterou už máte v cloudu. Doporučeným nástrojem k synchronizaci místních identit uživatelů s cloudovými službami Microsoftu je Azure AD Connect. Pokud vaše organizace už používá Office 365, je důležité, aby služba Intune používala stejné prostředí Azure AD.

Přečtěte si další informace o následujících požadavcích na identitu Intune:

- [Požadavky na identitu](https://docs.microsoft.com/azure/active-directory/understand-azure-identity-solutions)

- [Požadavky na synchronizaci adresáře](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)

- [Požadavky na vícefaktorové ověřování](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud)

### <a name="user-and-device-groups"></a>Skupiny uživatelů a zařízení

Skupiny uživatelů a zařízení určují cíl nasazení včetně zásad, aplikací a profilů. Potřebujete určit, jaké skupiny uživatelů a zařízení budou zapotřebí.

Doporučujeme, abyste všechny skupiny vytvořili v místní službě Active Directory a následně je synchronizovali se službou Azure AD. Přečtěte si další informace o plánování a vytváření skupin uživatelů a zařízení:

- [Plánování skupin uživatelů a zařízení](users-add.md)

- [Vytváření skupin uživatelů a zařízení](groups-add.md)

### <a name="public-key-infrastructure-pki"></a>Infrastruktura veřejných klíčů (PKI)
Infrastruktura veřejných klíčů dodává certifikáty zařízením nebo uživatelům, aby je služba mohla bezpečně ověřit. Intune podporuje infrastrukturu veřejných klíčů Microsoftu. Certifikáty zařízení a uživatele mohou být vydány mobilnímu zařízení, aby byly splněny požadavky na ověřování na základě certifikátů. Před použitím certifikátů musíte určit, jestli je potřebujete, jestli síťová infrastruktura podporuje ověřování na základě certifikátů a jestli se ve stávajícím prostředí momentálně používají certifikáty.

Pokud plánujete, že budete v Intune používat certifikáty s profily VPN, Wi-Fi nebo e-mailu, ověřte, že máte podporovanou [infrastrukturu PKI](../protect/certificates-configure.md) připravenou k vytváření a nasazování profilů certifikátů.

Kromě toho, pokud budou použity profily certifikátů SCEP, je nutné určit, který server bude hostovat funkci služby zápisu síťových zařízení (NDES) a jak bude provedena komunikace.

Další informace pro:

- [Jak konfigurovat profily certifikátů Intune](../protect/certificates-configure.md)

- [Jak konfigurovat infrastrukturu certifikátů pro SCEP](../protect/certificates-scep-configure.md)

- [Jak konfigurovat infrastrukturu certifikátů pro PFX](../protect/certficates-pfx-configure.md)




## <a name="device-platform-considerations"></a>Informace o platformě zařízení

Seznamte se blíže s následujícími aspekty svých zařízení, abyste věděli, jak se správně mají spravovat.

- Podporované platformy zařízení

- Zařízení

- Vlastnictví zařízení

- Hromadný zápis

Pojďme tyto oblasti podrobněji posuzovat.

### <a name="determine-supported-device-platforms"></a>Určení podporovaných platforem zařízení

Při vytváření návrhu potřebujete vědět, jaká zařízení budou v prostředí, a musíte ověřit, jestli je Intune podporuje nebo ne. Intune podporuje platformy iOS/iPadOS, Androidem a Windows.

[Vytvořte seznam zařízení podporovaných službou Intune](supported-devices-browsers.md).

### <a name="devices"></a>Zařízení

Intune slouží ke správě mobilních zařízení. Zabezpečuje firemní data a umožňuje koncovým uživatelům pracovat z více míst. Intune podporuje mnoho platforem zařízení, proto doporučujeme, abyste si povedli dokumentaci zařízení a platforem operačních systémů a verze, které budou v návrhu vaší organizace podporované. Příklad:

| **Platforma zařízení** | **Verze OS** |
|:---:|:---:|
| iOS – iPhone | 10.0+ |                
| iOS – iPad | 10.0+ |               
| Android – Samsung Knox Standard | 4.0+ |
| Tablet s Windows 10 | 10+ |


Můžete si [stáhnout šablonu výše uvedené tabulky](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) a použít ji k vypracování vlastního seznamu zařízení.
### <a name="device-ownership"></a>Vlastnictví zařízení

Intune podporuje jak zařízení vlastněná firmou, tak osobní zařízení. Zařízení se považuje za vlastněné firmou, pokud ho zaregistrujete pomocí některého správce nebo programu pro registraci zařízení. Pokud je například zařízení zaregistrované pomocí Programu registrace zařízení společnosti Apple (DEP – Device Enrollment Program), označí se jako vlastněné firmou a umístí se do skupiny zařízení, která dostává cílené firemní zásady a aplikace.

Další informace o případech použití zařízení vlastněných firmou a zařízení BYOD najdete v [oddílu 3: Určení požadavků scénářů pro případy použití](planning-guide-requirements.md).

### <a name="bulk-enrollment"></a>Hromadný zápis

 V závislosti na platformě můžete zařízení různými způsoby hromadně zaregistrovat. Pokud požadujete hromadnou registraci, napřed [určete, jakým způsobem bude probíhat](../enrollment/device-enrollment.md), a potom tento způsob zapracujte do svého návrhu.

## <a name="feature-requirements"></a>Funkční požadavky

V těchto oddílech si probereme následující funkce a možnosti, které odpovídají požadavkům na váš scénář použití:

- Zásady pro podmínky a ujednání

- Zásady konfigurace

- Profily prostředků

- Aplikace

- zásady dodržování předpisů

- Podmíněný přístup

Pojďme si projít každou z těchto oblastí podrobněji.

### <a name="terms-and-conditions-policies"></a>Zásady pro podmínky a ujednání

[Zásady a ujednání](../enrollment/terms-and-conditions-create.md) slouží k vysvětlení zásad nebo ujednání, která koncový uživatel musí přijmout, aby mohl své zařízení zaregistrovat. Intune podporuje možnost přidat a nasadit u skupin uživatelů různé zásady pro podmínky a ujednání.

Musíte určit, jestli jsou zásady pro podmínky a ujednání potřeba. Pokud tomu tak je, kdo v organizaci odpovídá za poskytování těchto informací. Následující příklad vysvětluje, jak dokumentovat zásadu pro podmínky a ujednání.

| **Název podmínek a ujednání** | **Případ použití** | **Cílová skupina** |
|:---:|:---:|:---:|
| Firemní podmínky a ujednání | Firemní | Firemní uživatelé |                 
| Podmínky a ujednání pro uživatele s vlastním zařízením | UŽIVATELÉ S VLASTNÍM ZAŘÍZENÍM (BYOD) | Uživatelé s vlastním zařízením |                


Můžete si [stáhnout šablonu výše uvedené tabulky](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) a namapovat podmínky a ujednání na své skupiny uživatelů.

### <a name="configuration-policies"></a>Zásady konfigurace

Zásady konfigurace slouží ke správě nastavení a funkcí zabezpečení v zařízení. Při návrhu zásad konfigurace se podívejte na část věnovanou požadavkům pro různé případy použití, kde zjistíte požadovanou konfiguraci zařízení pro Intune. Zdokumentujte nastavení a způsob, jak mají být nakonfigurována. Rovněž zdokumentujte, které skupiny uživatelů nebo zařízení budou jejich cílem.

Měli byste vytvořit alespoň jednu zásadu konfigurace pro každou platformu. V případě potřeby můžete pro každou platformu vytvořit několik zásad konfigurace. Následující příklad ilustruje návrh čtyř různých zásad konfigurace pro různé platformy a scénáře použití.

| **Název zásady** | **Platforma zařízení** | **Nastavení** | **Cílová skupina** |   
|:---:|:---:|:---:|:---:|
| Firemní – iOS | iOS | PIN je povinný, délka 6 znaků, omezené zálohování do cloudu | Firemní zařízení |                                                           
| Firemní – Android | Android | PIN je povinný, délka 6 znaků, omezené zálohování do cloudu | Firemní zařízení |                                                           
| Vlastní zařízení uživatelů – iOS  | iOS | PIN je povinný, délka 4 znaky | Vlastní zařízení uživatelů |
| Vlastní zařízení uživatelů – Android  | Android | PIN je povinný, délka 4 znaky | Vlastní zařízení uživatelů |


Můžete si [stáhnout šablonu výše uvedené tabulky](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) a identifikovat potřeby pro vlastní zásady konfigurace.

### <a name="profiles"></a>Profily

Profily pomáhají koncovému uživateli připojit se k firemním datům. Intune podporuje různé typy profilů. Pokud chcete určit, kdy se budou profily konfigurovat, podívejte se na případy použití a požadavky. Všechny profily zařízení jsou zařazené do kategorií podle typu platformy a měly by být součástí dokumentace k návrhu.

- Profily certifikátů

- Profil Wi-Fi

- Profil VPN

- E-mailový profil

Pojďme si podrobnější přehled o jednotlivých typech profilů.

#### <a name="certificate-profiles"></a>Profily certifikátů

Profily certifikátů umožňují službě Intune vydat certifikát uživateli nebo zařízení. Jaké certifikáty podporuje Intune:

- Protokol SCEP (Simple Certificate Enrollment Protocol)

- Důvěryhodný kořenový certifikát

- Certifikát PFX

Doporučujeme, abyste zdokumentovali, jaké skupiny uživatelů potřebují certifikát, kolik profilů certifikátů potřebujete a kterým skupinám uživatelů je nasadíte.

>[!NOTE]
> Mějte na paměti, že důvěryhodný kořenový certifikát je vyžadován pro profil certifikátu SCEP, proto zajistěte, aby všichni uživatelé, kteří mají profil certifikátu SCEP, získali také důvěryhodný kořenový certifikát. Pokud potřebujete certifikáty SCEP, navrhněte a zdokumentujte, které šablony certifikátů SCEP jsou zapotřebí.

Tady je příklad, jak můžete certifikáty zdokumentovat během návrhu:

| **Typ** | **Název profilu** | **Platforma zařízení** | **Případy použití** |   
|:---:|:---:|:---:|:---:|
| Kořenová CA | Firemní kořenová CA | Android, iOS/iPadOS, Windows Mobile | Firemní zařízení, vlastní zařízení uživatelů  |                                                           
| SCEP | Uživatelský certifikát | Android, iOS/iPadOS, Windows Mobile | Firemní zařízení, vlastní zařízení uživatelů |                                                           


Můžete si [stáhnout šablonu výše uvedené tabulky](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) a identifikovat potřeby pro vlastní profily certifikátů.

#### <a name="wi-fi-profile"></a>Profil Wi-Fi

Profily Wi-Fi se používají k automatickému připojení mobilního zařízení k bezdrátové síti. Intune podporuje nasazení profilů Wi-Fi pro všechny podporované platformy. Přečtěte si další informace o tom, [jak Intune podporuje profily Wi-Fi.](../configuration/wi-fi-settings-configure.md)

Tady je příklad návrhu profilu Wi-Fi:

| **Typ** | **Název profilu** | **Platforma zařízení** | **Případy použití** |
|:---:|:---:|:---:|:---:|
| Wi-Fi | Profil Wi-Fi pro Asii | Android | Firemní zařízení, vlastní zařízení uživatelů, oblast Asie|
| Wi-Fi | Profil Wi-Fi pro Severní Ameriku | Android, iOS/iPadOS, Windows 10 Mobile | Firemní zařízení, vlastní zařízení uživatelů, oblast Severní Amerika |

Můžete si [stáhnout šablonu výše uvedené tabulky](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) a identifikovat potřeby pro vlastní profily Wi-Fi.

#### <a name="vpn-profile"></a>Profil VPN

Profily VPN nabízejí uživatelům bezpečný přístup k síti ze vzdálených míst. Intune podporuje profily VPN nativních mobilních připojení VPN a externích dodavatelů. Další informace o [profilech VPN a dodavatelích podporovaných službou Intune](../configuration/vpn-settings-configure.md).

Tady je příklad, jak dokumentovat návrh profilu VPN.

| **Typ** | **Název profilu** | **Platforma zařízení** | **Případy použití** |
|:---:|:---:|:---:|:---:|
| Síť VPN | Profil VPN Cisco pro jakékoli připojení | Android, iOS/iPadOS, Windows 10 Mobile | Firemní zařízení, vlastní zařízení uživatelů, oblast Severní Amerika a Německo|
| Síť VPN | Pulse Secure | Android | Firemní zařízení, vlastní zařízení uživatelů, oblast Asie |

Můžete si [stáhnout šablonu výše uvedené tabulky](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) a identifikovat potřeby pro vlastní profily VPN.

#### <a name="email-profile"></a>E-mailový profil

E-mailové profily umožňují automatické nastavení e-mailového klienta pomocí informací o připojení a konfigurace e-mailu. Intune podporuje e-mailové profily jen na některých zařízeních. Přečtěte si další informace o [e-mailových profilech a podporovaných platformách](../configuration/email-settings-configure.md).

Tady je příklad, jak dokumentovat návrh e-mailových profilů:

| **Typ** | **Název profilu** | **Platforma zařízení** | **Případy použití** |
|:---:|:---:|:---:|:---:|
| E-mailový profil | E-mailový profil pro iOS | iOS | Firemní – informatik (uživatel s vlastním zařízením) |
| E-mailový profil | E-mailový profil pro Android Knox | Android Knox | UŽIVATELÉ S VLASTNÍM ZAŘÍZENÍM (BYOD) |

Můžete si [stáhnout šablonu výše uvedené tabulky](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) a identifikovat potřeby pro vlastní e-mailové profily.
### <a name="apps"></a>Aplikace

Intune můžete použít k několika způsobům doručování aplikací uživatelům nebo zařízením. Mezi typy aplikací patří instalační aplikace softwaru, aplikace z veřejného obchodu s aplikacemi, externí odkazy nebo spravované aplikace pro iOS. Kromě nasazení individuálních aplikací můžete spravovat a nasazovat také hromadně nakoupené aplikace pořízené prostřednictvím programů hromadného nákupu pro iOS a Windows. Další informace pro:

- [Typy aplikací, které můžete doručovat](../apps/app-management.md)

- [Program iOS VPP (Volume Purchase Program) pro firmy](../apps/vpp-apps-ios.md)

- [Aplikace pro Microsoft Store pro firmy](../apps/windows-store-for-business.md)

#### <a name="app-type-requirements"></a>Požadavky různých typů aplikací

Protože aplikace můžete nasazovat uživatelům a zařízením, doporučujeme, abyste se rozhodli, jaké aplikace budou spravované přes Intune. Při sestavování seznamu se pokuste odpovědět na následující otázky:

- Vyžadují aplikace integraci s cloudovými službami?

- Budou všechny aplikace dostupné uživatelům modelu BYOD?

- Jaké jsou u těchto aplikací možnosti nasazení?

- Potřebuje vaše firma zajistit pro své partnery přístup k datům aplikací SaaS (software jako služba)?

- Vyžadují aplikace přístup k Internetu ze zařízení uživatelů?

- Jsou aplikace veřejně dostupné v obchodu s aplikacemi, nebo jde o vlastní obchodní aplikace?


#### <a name="app-protection-policies"></a>Zásady ochrany aplikace

Zásady ochrany aplikace minimalizují ztrátu dat tím, že definují, jak aplikace spravuje firemní data. Intune podporuje zásady ochrany pro každou aplikaci vytvořenou tak, aby fungovala se správou mobilních aplikací. Při návrhu zásad ochrany aplikací se musíte rozhodnout, jaká omezení chcete uplatnit na firemní data v dané aplikaci. Doporučujeme vám prostudovat, jak [zásady ochrany aplikací](../apps/app-protection-policy.md) fungují. Tady je příklad, jak dokumentovat stávající aplikace a jakou ochranu potřebují.

| **Aplikace** | **Účel** | **Platformy** | **Případ použití** | **Zásada ochrany aplikace** |
|:---:|:---:|:---:|:---:|:---:|
| Outlook Mobile  | K dispozici | iOS | Firemní – vedení | Nelze provést jailbreak, šifrování souborů |                                                         
| Word | K dispozici | iOS/iPadOS, Android – Samsung KNOX, non-KNOX, Windows 10 Mobile | Firemní zařízení, vlastní zařízení uživatelů | Nelze provést jailbreak, šifrování souborů |                                                         


Můžete si [stáhnout šablonu výše uvedené tabulky](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) a identifikovat potřeby pro vlastní zásady ochrany aplikací.
#### <a name="compliance-policies"></a>Zásady slučitelnosti

Zásady dodržování předpisů určují, zda zařízení vyhovuje určitým požadavkům. Služba Intune používá zásady dodržování předpisů k tomu, aby zjistila, jestli zařízení vyhovuje nebo nevyhovuje. Stav dodržování předpisů je pak možné použít k zakázání nebo povolení přístupu k firemním prostředkům. Pokud se vyžaduje podmíněný přístup, doporučujeme navrhnout [zásadu dodržování předpisů pro zařízení](../protect/device-compliance-get-started.md).

Pokud chcete zjistit, kolik zásad dodržování předpisů zařízením potřebujete a jaké skupiny uživatelů jsou cílové, přečtěte si požadavky a případy použití. Navíc se musíte rozhodnout, jak dlouho může být zařízení offline bez vrácení se změnami, než se považuje za nedodržující předpisy.

Tady je příklad návrhu zásad dodržování předpisů:

| **Název zásady** | **Platforma zařízení** | **Nastavení** | **Cílová skupina** |
|:---:|:---:|:---:|:---:|
| zásady dodržování předpisů | iOS/iPadOS, Android – Samsung KNOX, non-KNOX, Windows 10 Mobile | PIN – povinný, nelze provést jailbreak | Firemní zařízení, vlastní zařízení uživatelů |


Můžete si [stáhnout šablonu výše uvedené tabulky](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) a identifikovat potřeby pro vlastní zásady dodržování předpisů.
#### <a name="conditional-access-policies"></a>Zásady podmíněného přístupu

Podmíněný přístup slouží k povolení přístupu k e-mailu a dalším prostředkům společnosti jenom vyhovujícím zařízením. Při řízení přístupu k firemním prostředkům spolupracuje Intune s řešením Enterprise Mobility + Security (EMS). Rozhodněte, jestli požadujete podmíněný přístup a co musí být zabezpečené. Další informace o [podmíněném přístupu](../protect/conditional-access.md).

V případě online přístupu rozhodněte, které platformy a skupiny uživatelů budete cílit podle zásad podmíněného přístupu. Také určete, jestli potřebujete nainstalovat nebo nakonfigurovat konektor Intune pro místní Exchange: 

- [Místní Exchange](../protect/exchange-connector-install.md)

Tady je příklad, jak dokumentovat zásady podmíněného přístupu:

| **Služba** | **Platformy moderního ověřování** | **Základní ověřování** | **Případy použití** |
|:---:|:---:|:---:|:---:|
| Exchange Online | iOS/iPadOS, Android | Blokování nevyhovujících zařízení na platformách podporovaných službou Intune | Firemní zařízení, vlastní zařízení uživatelů |
| SharePoint Online | iOS/iPadOS, Android |  | Firemní zařízení, vlastní zařízení uživatelů |

Můžete [si stáhnout šablonu výše uvedené tabulky](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0) a identifikovat potřeby zásad podmíněného přístupu.

## <a name="next-steps"></a>Další kroky

Další část obsahuje pokyny k [procesu implementace Intune](planning-guide-onboarding.md).
