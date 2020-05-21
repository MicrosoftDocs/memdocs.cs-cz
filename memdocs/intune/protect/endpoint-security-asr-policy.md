---
title: Správa nastavení omezení možností útoku pomocí zásad zabezpečení koncového bodu v Microsoft Intune | Microsoft Docs
description: Konfigurace a nasazení zásad pro zařízení, která spravujete pomocí nastavení zásad omezení možností zabezpečení Endpoint Security v Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 20c8cc73e8037c0f394547b64d562cf75271240c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431241"
---
# <a name="attack-surface-reduction-policy-for-endpoint-security-in-intune"></a>Zásady omezení možností útoku pro zabezpečení koncového bodu v Intune

Když se antivirová ochrana v programu Defender používá v zařízeních s Windows 10, můžete pro snížení počtu možností útoku použít zásady zabezpečení koncového bodu služby Intune a spravovat tato nastavení pro vaše zařízení.

Zásady omezení možností útoku snižují prostory útoku tím, že minimalizují místa, kde je vaše organizace zranitelná vůči týká kybernetických hrozeb a útokům. Další informace najdete v tématu [Přehled snížení prostoru pro útoky]( https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-attack-surface-reduction) v dokumentaci k Windows Threat Protection.

V uzlu **zabezpečení koncového** bodu v [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431)vyhledejte zásady zabezpečení koncového bodu pro omezení *možností* útoku. Každý *profil* pro omezení možností útoku spravuje nastavení pro určitou oblast zařízení s Windows 10.

Zobrazit [nastavení pro omezení profilů útoků na plochu](../protect/endpoint-security-asr-profile-settings.md).

## <a name="prerequisites-for-attack-surface-reduction-profiles"></a>Předpoklady pro omezení profilů možností útoku

- Windows 10 nebo novější
- Antivirová ochrana v programu Defender musí být primární antivirový program na zařízení.

## <a name="attack-surface-reduction-profiles"></a>Profily pro omezení možností útoku

**Profily Windows 10**:

- **Izolace aplikací a prohlížečů** – Spravujte nastavení pro ochranu Application Guard v programu Windows Defender (Application Guard) jako součást ATP programu Defender. Ochrana Application Guard pomáhá zabránit starým a nově vznikajícím útokům a může izolovat podnikové lokality jako nedůvěryhodné při definování, které lokality, cloudové prostředky a interní sítě jsou důvěryhodné.

  Další informace najdete v tématu [Application Guard](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview) v dokumentaci ke službě Microsoft Defender atp.

- **Webová ochrana** – nastavení, která můžete spravovat pro webovou ochranu v ATP v programu Microsoft Defender konfigurace ochrany sítě pro zabezpečení vašich počítačů před webovými hrozbami. Díky integraci s Microsoft Edgem a oblíbenými prohlížeči třetích stran, jako je Chrome a Firefox, Webová ochrana zastavuje webové hrozby bez webového proxy serveru a může chránit počítače i v době, kdy jsou nebo jsou v místním prostředí. Ochrana webu přestane mít přístup k:
  - Weby útoku phishing
  - Vektory malwaru
  - Zneužití webů
  - Nedůvěryhodné nebo nízké reputace webů
  - Weby, které jste zablokovali ve svém vlastním seznamu ukazatelů.

  Další informace najdete v tématu [Webová ochrana](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) v dokumentaci ke službě Microsoft Defender atp.

- **Řízení aplikací** – nastavení řízení aplikací může pomáhat zmírnit bezpečnostní hrozby tím, že omezí aplikace, které můžou uživatelé spouštět, a kód, který běží v jádru systému (jádro). Spravujte nastavení, které může blokovat nepodepsané skripty a MSIs, a omezit prostředí Windows PowerShell tak, aby běželo v režimu omezeného jazyka.

  Další informace najdete v tématu [řízení aplikací](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) v dokumentaci ke službě Microsoft Defender atp.

- **Pravidla pro omezení možností útoku** – nakonfigurujte nastavení pro pravidla pro omezení možností útoku, která cílí na chování, která malwarová a škodlivá aplikace obvykle používají pro nainfikování počítačů, včetně těchto:
  - Spustitelné soubory a skripty používané v aplikacích Office nebo ve webové poště, které se pokoušejí stáhnout nebo spustit soubory
  - Zmatené nebo jinak podezřelé skripty
  - Chování, které aplikace většinou nespouštějí během běžné každodenní práce, které snižují prostor pro útok, znamená, že by útočníki nabízeli méně způsobů, jak provádět útoky.

  Další informace najdete v tématu [pravidla pro omezení možností útoku](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction) v dokumentaci ke službě Microsoft Defender atp.

- **Řízení zařízení** – s nastavením pro řízení zařízení můžete nakonfigurovat zařízení pro vrstvený přístup k zabezpečení vyměnitelných médií. Ochrana ATP v programu Microsoft Defender poskytuje několik funkcí monitorování a kontroly, které zabraňují hrozbám v neautorizovaných periferních zařízeních narušit vaše zařízení.

  Další informace najdete v tématu [postup řízení zařízení USB a dalších vyměnitelných médií pomocí ATP v programu Microsoft Defender](https://docs.microsoft.com/windows/security/threat-protection/device-control/control-usb-devices-using-intune) v dokumentaci ke službě Microsoft Defender atp.

- **Zneužití ochrany** – nastavení ochrany před zneužitím můžou přispět k ochraně proti malwaru, který využívá zneužití k nainfikování zařízení a dvojstránky. Ochrana před zneužitím se skládá z několika rizik, která se dají použít buď pro operační systém, nebo pro jednotlivé aplikace.

  Další informace najdete v tématu [Povolení ochrany před zneužitím](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) v dokumentaci ke službě Microsoft Defender atp.

## <a name="next-steps"></a>Další kroky

[Konfigurace zásad zabezpečení koncového bodu](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
