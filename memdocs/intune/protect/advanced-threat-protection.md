---
title: Používání ATP v programu Microsoft Defender v Microsoft Intune – Azure | Microsoft Docs
description: Použijte Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) s Intune, včetně nastavení a konfigurace, zprovoznění zařízení Intune s ATP a pak použijte hodnocení rizik ATP pro zařízení se zásadami dodržování předpisů a zásad podmíněného přístupu v zařízeních k ochraně síťových prostředků.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9f54bf7f281fca65e01d839e926200bc68c49765
ms.sourcegitcommit: 46d4bc4fa73b22ae2a6a17a2d1cc6ec933a50e89
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88663443"
---
# <a name="enforce-compliance-for-microsoft-defender-atp-with-conditional-access-in-intune"></a>Vymáhání dodržování předpisů pro Microsoft Defender ATP pomocí podmíněného přístupu v Intune

Integraci rozšířené ochrany před internetovými útoky v programu Microsoft Defender (Microsoft Defender ATP) můžete integrovat s Microsoft Intune jako řešení ochrany před mobilními hrozbami. Integrace vám může přispět k tomu, abyste zabránili narušení zabezpečení a omezili dopad narušení v rámci organizace.

Ochrana ATP v programu Microsoft Defender spolupracuje se zařízeními se systémem Windows 10 nebo novějším a se zařízeními s Androidem.

Aby bylo úspěšné, budete používat následující konfigurace ve vzájemné součinnosti:

- **Navažte spojení mezi službou Intune a ATP v programu Microsoft Defender**. Toto připojení umožňuje službě Microsoft Defender ATP shromažďovat data o rizikech počítačů z podporovaných zařízení, která spravujete pomocí Intune.
- **Pomocí profilu konfigurace zařízení připojte zařízení s ATP Microsoft Defender**. Připojíte zařízení, abyste je mohli nakonfigurovat tak, aby komunikovala s ATP Microsoft Defender a poskytovali data, která vám pomůžou vyhodnotit jejich úroveň rizika.
- **Pomocí zásad dodržování předpisů pro zařízení nastavte úroveň rizika, které chcete udělit**. Úrovně rizika jsou hlášeny v ochraně ATP v programu Microsoft Defender. Zařízení, která překračují povolenou úroveň rizika, se označují jako nedodržující předpisy.
- **Pomocí zásad podmíněného přístupu** můžete uživatelům zablokovat přístup k podnikovým prostředkům ze zařízení, která nedodržují předpisy.

Při integraci Intune s modulem Microsoft Defender ATP můžete využít výhod programu Microsoft Defender ATPs Threat Management & (TVM) a [pomocí Intune napravit slabiny koncových bodů identifikované systémem TVM](atp-manage-vulnerabilities.md).

## <a name="example-of-using-microsoft-defender-atp-with-intune"></a>Příklad používání služby Microsoft Defender ATP s Intune

Následující příklad vám pomůže vysvětlit, jak tato řešení společně pomáhají chránit vaši organizaci. V tomto příkladu jsou služby Microsoft Defender ATP a Intune už integrované.

Vezměte v úvahu událost, kdy někdo pošle Wordovou přílohu s vloženým škodlivým kódem uživateli v rámci vaší organizace.

- Uživatel přílohu otevře a povolí obsah.
- Spustí se útok se zvýšenými oprávněními a útočník ze vzdáleného počítače má práva správce k zařízení oběti.
- Z tohoto zařízení získá vzdálený přístup i k dalším zařízením uživatele. Toto porušení zabezpečení může mít dopad na celou organizaci.

Ochrana ATP v programu Microsoft Defender může pomáhat vyřešit události zabezpečení, jako je tento scénář.

- V našem příkladu ATP Microsoft Defender detekuje, že zařízení provedlo neobvyklý kód, narazilo na eskalaci s oprávněním procesu, vložil škodlivý kód a vystavilo podezřelé vzdálené prostředí.
- Na základě těchto akcí ze zařízení klasifikuje ATP v programu Microsoft Defender [zařízení jako vysoce rizikové](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity) a obsahuje podrobnou zprávu o podezřelé aktivitě na portálu Microsoft Defender Security Center.

Integraci rozšířené ochrany před internetovými útoky v programu Microsoft Defender (Microsoft Defender ATP) můžete integrovat s Microsoft Intune jako řešení ochrany před mobilními hrozbami. Integrace vám může přispět k tomu, abyste zabránili narušení zabezpečení a omezili dopad narušení v rámci organizace.

Vzhledem k tomu, že máte zásady dodržování předpisů pro zařízení v Intune ke klasifikaci zařízení se *střední* nebo *vysokou* úrovní rizika při nedodržení předpisů, je ohrožené zařízení klasifikované jako nedodržující předpisy. Tato klasifikace umožňuje zásadám podmíněného přístupu vykázat a zablokovat přístup z tohoto zařízení k firemním prostředkům.

U zařízení se systémem Android můžete pomocí zásad Intune upravit konfiguraci ochrany ATP v programu Microsoft Defender v Androidu. Další informace najdete v tématu [ochrana ATP na webu Microsoft Defender ATP](../protect/advanced-threat-protection-manage-android.md).

## <a name="prerequisites"></a>Předpoklady

Pokud chcete používat Microsoft Defender ATP s Intune, ujistěte se, že máte nakonfigurované a připravené k použití:

- Tenant s licencí pro Enterprise Mobility + Security E3 a Windows E5 (nebo Microsoft 365 Enterprise E5)
- Prostředí Microsoft Intune s využitím zařízení s Windows 10 [spravovaných pomocí Intune](../enrollment/windows-enroll.md) nebo zařízení s Androidem, která jsou taky připojená k Azure AD
- Prostředí [ATP v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) , které vám umožní přístup k Security Center programu Microsoft Defender (portál ATP)

> [!NOTE]
> Ochrana ATP v programu Microsoft Defender není podporována zásadami ochrany aplikací pro iOS/iPadOS a Android Intune.

## <a name="next-steps"></a>Další kroky

- Postup připojení ochrany Microsoft Defenderu k Intune, zprovoznění zařízení a konfiguraci zásad podmíněného přístupu najdete v tématu [Konfigurace ATP v programu Microsoft Defender v Intune](../protect/advanced-threat-protection-configure.md).

Další informace najdete v dokumentaci k Intune:

- [Použití úloh zabezpečení se správou ohrožení zabezpečení ATPs k nápravě problémů na zařízeních](atp-manage-vulnerabilities.md)
- [Začínáme se zásadami dodržování předpisů zařízeními](device-compliance-get-started.md)

Další informace najdete v dokumentaci ke službě Microsoft Defender ATP:

- [Podmíněný přístup Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Řídicí panel rizik pro ATP v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)
