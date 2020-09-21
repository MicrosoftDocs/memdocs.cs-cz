---
title: Správa zabezpečení koncového bodu v Microsoft Intune | Microsoft Docs
description: Přečtěte si, jak správci zabezpečení můžou pomocí uzlu Security Endpoint spravovat zabezpečení zařízení a opravovat problémy pro zařízení ve službě Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/21/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 8d02f32d11cedae94cc179f6a7bdeba553063c8d
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2020
ms.locfileid: "90815387"
---
# <a name="manage-endpoint-security-in-microsoft-intune"></a>Správa zabezpečení koncového bodu v Microsoft Intune

Jako správce zabezpečení můžete pomocí uzlu *Security Endpoint* v Intune nakonfigurovat zabezpečení zařízení a spravovat úlohy zabezpečení pro zařízení, když jsou tato zařízení v ohrožení. Zásady zabezpečení koncového bodu jsou navržené tak, aby vám pomohly se zaměřit na zabezpečení vašich zařízení a zmírnit rizika. Úlohy, které jsou k dispozici, vám pomůžou identifikovat zařízení, která jsou ohrožená, aby je bylo možné opravit, a obnovit je do stavu kompatibilního nebo vyššího zabezpečení.

Uzel zabezpečení koncového bodu seskupuje nástroje, které jsou k dispozici prostřednictvím Intune, které budete používat k zajištění zabezpečení zařízení:

- **Zkontrolujte stav všech spravovaných zařízení**. Použijte zobrazení [všechna zařízení](#manage-devices) , kde můžete zobrazit dodržování předpisů zařízením z vysoké úrovně. Pak přejděte na konkrétní zařízení, abyste zjistili, které zásady dodržování předpisů nejsou splněné, abyste je mohli vyřešit.

- **Nasaďte standardní hodnoty zabezpečení, které vytvoří konfigurace zabezpečení osvědčených postupů pro zařízení**. Intune zahrnuje [základní hodnoty zabezpečení](#manage-security-baselines) pro zařízení s Windows a rostoucí seznam aplikací, jako je Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) a Microsoft Edge. Směrné plány zabezpečení jsou předem nakonfigurované skupiny nastavení Windows, které vám pomůžou použít známou skupinu nastavení a výchozí hodnoty, které doporučují příslušné bezpečnostní týmy.

- **Spravujte konfigurace zabezpečení na zařízeních prostřednictvím úzce zaměřeného zásad**.  Každá [zásada zabezpečení koncového bodu](#use-policies-to-manage-device-security) se zaměřuje na aspekty zabezpečení zařízení, jako je antivirová ochrana, šifrování disků, brány firewall a několik oblastí, které jsou dostupné prostřednictvím integrace s Microsoft Defender atp.

- **Navažte požadavky na zařízení a uživatele prostřednictvím zásad dodržování předpisů**. Pomocí [zásad dodržování předpisů](../protect/device-compliance-get-started.md)nastavíte pravidla, která musí zařízení a uživatelé splňovat, aby se považovaly za vyhovující. Pravidla můžou zahrnovat verze operačních systémů, požadavky na heslo, úroveň hrozeb zařízení a další.

  Při integraci se [zásadami podmíněného přístupu](#configure-conditional-access) Azure Active Directory (Azure AD) pro vykonání zásad dodržování předpisů můžete používat přístup k podnikovým prostředkům pro spravovaná zařízení i pro zařízení, která ještě nejsou spravovaná.

- **Integrujte Intune s týmem ATP v programu Microsoft Defender**. Díky [integraci s ATP programu Microsoft Defender](#set-up-integration-with-microsoft-defender-atp) získáte přístup k [úlohám zabezpečení](#review-security-tasks-from-microsoft-defender-atp). Úkoly zabezpečení úzce propojují ATP a Intune v programu Microsoft Defender a pomohou vašemu týmu zabezpečení identifikovat zařízení, která jsou ohrožená a mají jistotu, že správci Intune můžou pracovat s podrobnými kroky nápravy.

Následující části tohoto článku popisují různé úlohy, které můžete provádět z uzlu Security Center v centru pro správu, a oprávnění řízení přístupu na základě role (RBAC), která jsou potřeba k jejich použití.

## <a name="manage-devices"></a>Správa zařízení

Uzel zabezpečení koncového bodu obsahuje zobrazení *všechna zařízení* , kde můžete zobrazit seznam všech zařízení z Azure AD, které jsou k dispozici ve službě Microsoft Endpoint Manager.

V tomto zobrazení můžete vybrat zařízení, ve kterých budete moct přejít na Další informace, jako jsou zásady, se kterými zařízení nedodržuje předpisy. Přístup z tohoto zobrazení můžete také použít k nápravě problémů zařízení, včetně restartování zařízení, spuštění vyhledávání malwaru nebo otočení klíčů BitLockeru na zařízení s Windows 10.

Další informace najdete v tématu [Správa zařízení pomocí zabezpečení koncového bodu v Microsoft Intune](../protect/endpoint-security-manage-devices.md).

## <a name="manage-security-baselines"></a>Správa standardních hodnot zabezpečení

Standardní hodnoty zabezpečení v Intune jsou předem nakonfigurované skupiny nastavení, které jsou osvědčenými postupy od příslušných týmů pro zabezpečení Microsoftu pro daný produkt. Intune podporuje standardní hodnoty zabezpečení pro nastavení zařízení s Windows 10, Microsoft Edge, rozšířené ochrany před internetovými útoky v Microsoft Defenderu a další.

Pomocí směrných plánů zabezpečení můžete rychle nasadit konfiguraci *osvědčených postupů* pro nastavení zařízení a aplikací pro ochranu uživatelů a zařízení. Pro zařízení s Windows 10 verze 1809 a novější se podporují standardní hodnoty zabezpečení.

Další informace najdete v tématu [použití směrných plánů zabezpečení ke konfiguraci zařízení s Windows 10 v Intune](../protect/security-baselines.md).

Standardní hodnoty zabezpečení jsou v Intune jedním z několika způsobů konfigurace nastavení na zařízeních. Při správě nastavení je důležité pochopit, jaké jiné metody se ve vašem prostředí používají, aby bylo možné zařízení nakonfigurovat, abyste se vyhnuli konfliktům. Další informace najdete v tématu [předcházení konfliktům zásad](#avoid-policy-conflicts) dále v tomto článku.

## <a name="review-security-tasks-from-microsoft-defender-atp"></a>Kontrola úloh zabezpečení z ochrany ATP v programu Microsoft Defender

Při integraci Intune s rozšířenou ochranou před internetovými útoky v programu Microsoft Defender (Microsoft Defender ATP) můžete zkontrolovat *úlohy zabezpečení* v Intune, které identifikují rizikové zařízení, a poskytnout kroky pro zmírnění tohoto rizika. Pak můžete úlohy použít k hlášení zpět do ATP v programu Microsoft Defender v případě jejich úspěšného zmírnění rizika.

- Váš tým ATP v programu Microsoft Defender určí, která zařízení jsou v ohrožení, a předá tyto informace vašemu týmu Intune jako bezpečnostní úlohu. Po několika kliknutích vytvoří úkol zabezpečení pro Intune, který identifikuje ohrožená zařízení, ohrožení zabezpečení a poskytuje pokyny k tomu, jak toto riziko zmírnit.

- Správci Intune kontrolují úlohy zabezpečení a pak jednají v rámci Intune, aby tyto úkoly opravili. Po omezení nastavili úkol na dokončeno, který tento stav sdělí týmu ATP v programu Microsoft Defender.

Díky bezpečnostním úlohám oba týmy zůstávají v synchronizaci, jako u kterých jsou ohrožená zařízení, a jak a kdy se tato rizika napravují.

Další informace o používání úloh zabezpečení najdete v tématu [použití Intune k nápravě ohrožení zabezpečení identifikovaných v souvislosti s programem Microsoft Defender ATP](../protect/atp-manage-vulnerabilities.md).

## <a name="use-policies-to-manage-device-security"></a>Použití zásad ke správě zabezpečení zařízení

Jako správce zabezpečení použijte zásady zabezpečení, které najdete v části *Správa* v uzlu zabezpečení koncového bodu. Pomocí těchto zásad můžete nakonfigurovat zabezpečení zařízení bez režie navigace nad větším textem a rozsahem nastavení z profilů konfigurace zařízení a standardních hodnot zabezpečení.

![Správa zásad](./media/endpoint-security/endpoint-security-policies.png)

Další informace o používání těchto zásad zabezpečení najdete v tématu [Správa zabezpečení zařízení pomocí zásad zabezpečení koncového bodu](../protect/endpoint-security-policy.md).

Zásady zabezpečení koncového bodu jsou jedním z několika způsobů, jak v Intune konfigurovat nastavení na zařízeních. Při správě nastavení je důležité pochopit, jaké jiné metody se ve vašem prostředí používají, které můžou nakonfigurovat vaše zařízení a vyhnout se konfliktům. Další informace najdete v tématu [předcházení konfliktům zásad](#avoid-policy-conflicts) dále v tomto článku.

V části *Správa* najdete taky zásady *dodržování předpisů zařízením* a *podmíněného přístupu* . Tyto zásady nejsou zaměřené na zásady zabezpečení pro konfiguraci koncových bodů, ale jsou to důležité nástroje pro správu zařízení a přístup k podnikovým prostředkům.

## <a name="use-device-compliance-policy"></a>Použití zásad dodržování předpisů pro zařízení

Pomocí zásad dodržování předpisů pro zařízení navažte podmínky, podle kterých budou zařízení a uživatelé mít povolený přístup k vaší síti a prostředkům společnosti.

[Dostupná nastavení dodržování předpisů](../protect/device-compliance-get-started.md#next-steps) závisí na používané platformě, ale mezi běžná pravidla zásad patří:

- Vyžaduje se, aby zařízení spouštěla minimální nebo konkrétní verzi operačního systému.
- Nastavení požadavků na heslo
- Zadání maximální povolené úrovně pro hrozby zařízení, která je určená ATP Microsoft Defender nebo jiným partnerem ochrany před mobilními hrozbami

Kromě pravidel zásad podporuje zásady dodržování předpisů:

- [Umístění](../protect/use-network-locations.md) , která definujete v Intune. Když použijete umístění se zásadami dodržování předpisů, může zásada zajistit, aby byla zařízení připojená k pracovní síti, aby splňovala předpisy.
- [Akce při nedodržení předpisů](../protect/actions-for-noncompliance.md). Tyto akce jsou časově uspořádané posloupnosti akcí, které je třeba použít u nevyhovujících zařízení. Akce zahrnují odesílání e-mailů nebo oznámení upozorňujících na nedodržení předpisů uživatelů zařízení, vzdálené uzamykání zařízení nebo dokonce vyřazení zařízení, která nedodržují předpisy, a odebrání všech firemních dat, která se na nich mohou nacházet.

Když integruje Intune se [zásadami podmíněného přístupu](#configure-conditional-access) Azure AD, aby vynutila zásady dodržování předpisů, podmíněný přístup může používat data o dodržování předpisů k zajištění přístupu k podnikovým prostředkům pro spravovaná zařízení i ze zařízení, která nespravujete.

Další informace najdete v tématu [Nastavení pravidel na zařízeních pro povolení přístupu k prostředkům ve vaší organizaci pomocí Intune](../protect/device-compliance-get-started.md).

Zásady dodržování předpisů pro zařízení jsou jedním z několika způsobů, jak v Intune konfigurovat nastavení na zařízeních. Při správě nastavení je důležité pochopit, jaké jiné metody se ve vašem prostředí používají, které mohou konfigurovat vaše zařízení a vyhnout se konfliktům. Další informace najdete v tématu [předcházení konfliktům zásad](#avoid-policy-conflicts) dále v tomto článku.

## <a name="configure-conditional-access"></a>Konfigurace podmíněného přístupu

K ochraně svých zařízení a podnikových prostředků můžete použít zásady podmíněného přístupu Azure Active Directory (Azure AD) s Intune.

Intune předává výsledky zásad dodržování předpisů zařízením do služby Azure AD, které pak pomocí zásad podmíněného přístupu vynutily, která zařízení a aplikace budou mít přístup k firemním prostředkům. Zásady podmíněného přístupu můžou pomocí brány získat přístup k zařízením, která nespravuje Intune. Můžete dokonce použít podrobnosti o dodržování předpisů od [partnerů ochrany před mobilními hrozbami](../protect/mobile-threat-defense.md) , které Integrujte s Intune.

Níže jsou uvedené dvě běžné metody použití podmíněného přístupu s Intune:

- **Podmíněný přístup podle zařízení**, aby se k síťovým prostředkům mohlo přistupovat jenom spravovaná a vyhovující zařízení.
- **Podmíněný přístup na základě aplikace**, který využívá zásady ochrany aplikací ke správě přístupu k síťovým prostředkům uživateli na zařízeních, která nespravujete přes Intune.

Další informace o použití podmíněného přístupu v Intune najdete v tématu [informace o podmíněném přístupu a Intune](../protect/conditional-access.md).

## <a name="set-up-integration-with-microsoft-defender-atp"></a>Nastavení integrace s Microsoft Defender ATP

Když integrujete Microsoft Defender ATP s Intune, Vylepšete svou schopnost identifikovat a reagovat na rizika.

I když se může Intune integrovat s několika [partnery ochrany před mobilními hrozbami](../protect/mobile-threat-defense.md), při použití ATP Microsoft Defenderu získáte úzkou integraci mezi Microsoft Defender ATP a Intune s přístupem k možnostem ochrany hlubokých zařízení, včetně těchto:

- Úkoly zabezpečení – bezproblémová komunikace mezi ATP a správci Intune o riziku zařízení, jejich nápravě a potvrzení, že se rizika sníží.
- Zjednodušená registrace pro Microsoft Defender ATP na klientech.
- Používání rizikových signálů zařízení ATP v zásadách dodržování předpisů v Intune.
- Přístup k možnostem *neoprávněné ochrany* .

 Další informace o používání služby Microsoft Defender ATP s Intune najdete v tématu [vymáhání dodržování předpisů pro Microsoft Defender ATP s podmíněným přístupem v Intune](../protect/advanced-threat-protection.md).

## <a name="role-based-access-control-requirements"></a>Požadavky na řízení přístupu na základě rolí

Aby bylo možné spravovat úlohy v uzlu Security Endpoint v centru pro správu služby Microsoft Endpoint Manager, musí účet:

- Mít přiřazenou licenci pro Intune.
- Mít oprávnění řízení přístupu na základě role (RBAC) rovna oprávněním, která poskytuje integrovaná role Intune služby  **Endpoint Security Manager**. Role *Správce zabezpečení koncového bodu* uděluje přístup k centru pro správu služby Microsoft Endpoint Manager. Tuto roli můžou použít jednotlivci, kteří spravují funkce zabezpečení a dodržování předpisů, včetně standardních hodnot zabezpečení, dodržování předpisů zařízením, podmíněného přístupu a ochrany ATP v programu Microsoft Defender.

Další informace najdete v tématu [řízení přístupu na základě role (RBAC) pomocí Microsoft Intune](../fundamentals/role-based-access-control.md)

### <a name="permissions-granted-by-the-endpoint-security-manager-role"></a>Oprávnění udělená rolí *Správce zabezpečení koncového bodu*

Následující seznam oprávnění můžete zobrazit v centru pro správu Microsoft Endpoint Manageru tak, že na stránce **role pro správu tenanta**zadáte  >  **Roles**  >  **vlastnosti všechny role**, pak na **Správce služby Endpoint Security Manager**  >  **Properties**.

**Nastaven**

- **Android for Work**
  - Číst
- **Data auditu**
  - Číst
- **Identifikátory podnikových zařízení**
  - Číst
- **Zásady dodržování předpisů pro zařízení**
  - Přiřadit
  - Vytvořit
  - Odstranit
  - Číst
  - Aktualizace
  - Zobrazení sestav
- **Konfigurace zařízení**
  - Číst
- **Správci registrace zařízení**
  - Číst
- **Sestavy aplikace Endpoint Protection**
  - Číst
- **Registrace programů**
  - Číst zařízení
  - Číst profil
  - Token pro čtení
- **Datový sklad Intune**
  - Číst
- **Spravované aplikace**
  - Číst
- **Spravovaná zařízení**
  - Odstranit
  - Číst
  - Nastavit primárního uživatele
  - Aktualizace
- **Mobilní aplikace**
  - Číst
- **Organizace**
  - Číst
- **PolicySets**
  - Číst
- **Vzdálená pomoc**
  - Číst
- **Vzdálené úlohy**
  - Získat klíč trezoru
  - Zahájit akci Správce konfigurace
  - Microsoft Defender
  - Restartovat hned
  - vzdálené uzamčení
  - Otočit BitLockerKeys (Preview)
  - Otočit klíč trezoru
  - Synchronizovat zařízení
- **Role**
  - Číst
- **Základní nastavení zabezpečení**
  - Přiřadit
  - Vytvořit
  - Odstranit
  - Číst
  - Aktualizace
- **Úlohy zabezpečení**
  - Číst
  - Aktualizace
- **Výdaje na telekomunikaci**
  - Číst
- **Podmínky a ujednání**
  - Číst

## <a name="avoid-policy-conflicts"></a>Vyhnout se konfliktům zásad

Mnohá nastavení, která můžete konfigurovat pro zařízení, můžete spravovat pomocí různých funkcí v Intune. Tyto funkce zahrnují, ale nejsou omezené na:

- Zásady zabezpečení koncového bodu
- Základní nastavení zabezpečení
- Zásady konfigurace zařízení
- Zásady registrace pro Windows 10

Například nastavení zjištěná v zásadách zabezpečení koncového bodu jsou podmnožinou nastavení, která se nacházejí v zásadách *ochrany koncových bodů* a *omezení zařízení* v zásadách konfigurace zařízení a která jsou také spravována prostřednictvím různých standardních hodnot zabezpečení.

Jedním ze způsobů, jak zabránit konfliktům, je nepoužívat jiné směrné plány, instance stejného směrného plánu nebo různé typy a instance zásad pro správu stejných nastavení na zařízení. To vyžaduje plánování, které metody použijete k nasazení konfigurací do různých zařízení. Pokud ke konfiguraci stejného nastavení použijete více metod nebo instancí stejné metody, zajistěte, aby vaše různé metody buď souhlasily, nebo nebyly nasazeny do stejného zařízení.

Pokud dojde ke konfliktům, můžete k identifikaci a řešení zdroje těchto konfliktů použít integrované nástroje Intune. Další informace naleznete v tématu:

- [Řešení potíží se zásadami a profily v Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Monitorování standardních hodnot zabezpečení](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>Další kroky

Konfigurace

- [Základní nastavení zabezpečení](../protect/security-baselines.md)
- [Zásady dodržování předpisů](../protect/device-compliance-get-started.md)
- [Zásady podmíněného přístupu](#configure-conditional-access)
- [Integrace s ATP v programu Microsoft Defender](../protect/advanced-threat-protection.md)
