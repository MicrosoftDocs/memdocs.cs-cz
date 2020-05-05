---
title: Cloud připojující se spolusprávou
titleSuffix: Configuration Manager
description: Spoluspráva nabízí okamžitou hodnotu, když ji povolíte.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 8d878443-90e7-46e4-9cd3-99e2a19b2ad0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5ca960ddd6a4057da10341063f0b14a7f1d104d1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075808"
---
# <a name="cloud-connecting-with-co-management"></a>Cloud připojující se spolusprávou

![Banner řady Blastoff](media/blastoff-banner.png)

Spoluspráva přidává do stávajícího nasazení Configuration Manager nové funkce, a to beze změny, jak už pracujete. Když povolíte spolusprávu, okamžitě začnete využívání z cloudu. Tuto hodnotu můžete použít pro svou stávající infrastrukturu a procesy správy.

V této sérii rychlých startech spolusprávy si přečtěte, jak můžete rychle řídit novou hodnotu správy. Spoluspráva je sestavená tak, aby vytvořila funkce a nástroje, které můžete použít hned teď.

V následujícím videu společnost Microsoft místopředseda brada Anderson zavádí tuto řadu spolusprávy:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Cloud-Connecting-with-Co-Management/player]

| Okamžitá hodnota | Začínáme |
|-----------------|-----------------|
| - [Podmíněný přístup](#bkmk_ca)<br> - [Vzdálené akce z Intune](#bkmk_remote)<br> - [Stav klienta](#bkmk_client-health)<br> - [Hybridní služba Azure AD](#bkmk_hybrid-aad)<br> - [Windows autopilot](#bkmk_autopilot) | - [Cesty ke spolusprávě](#bkmk_paths)<br> - [Nastavení hybridní služby Azure AD](#bkmk_setup-hybrid-aad)<br> - [Upgrade na Windows 10](#bkmk_upgrade-win10)<br> - [Získat pomoc z FastTrack](#bkmk_fasttrack) |

## <a name="immediate-value"></a>Okamžitá hodnota

| | | |
|-|-|-|
| <a name="bkmk_ca"></a>**Podmíněný přístup s dodržováním předpisů zařízením** | Řízení přístupu uživatelů k podnikovým prostředkům na základě pravidel dodržování předpisů z Intune | [![Miniatura videa podmíněného přístupu](media/thumbnail-conditional-access.png)](quickstart-conditional-access.md) |
| <a name="bkmk_remote"></a>**Vzdálené akce z Intune** | Spouštějte vzdálené akce z Intune pro spoluspravovaná zařízení. Například vymazání a resetování zařízení a údržba registrace a účtu | [![Miniatura videa vzdálených akcí](media/thumbnail-remote-action.png)](quickstart-remote-actions.md) |
| <a name="bkmk_client-health"></a>**Configuration Manager stav klienta** | Udržujte si přehled o Configuration Manager stav klienta z Intune na Azure Portal | [![Miniatura videa o stavu klienta](media/thumbnail-client-health.png)](quickstart-client-health.md) |
| <a name="bkmk_hybrid-aad"></a>**Azure Active Directory (Azure AD)** | Pomocí Azure AD můžete využívat lepší produktivitu uživatelů a zabezpečení vašich prostředků v cloudových i Prem prostředích. | [![Miniatura hybridního videa služby Azure AD](media/thumbnail-azure-ad.png)](quickstart-hybrid-aad.md) |
| <a name="bkmk_autopilot"></a>**Windows autopilot** | Omezte čas, prostředky a složitost spojené s nasazením, správou a vyřazením nebo vyřazením zařízení. Tento autopilot také pro koncové uživatele vytvoří lepší prostředí. | [![Miniatura videa o programu Windows autopilot](media/thumbnail-autopilot.png)](quickstart-autopilot.md) |

## <a name="getting-started"></a>Začínáme

Pokud chcete povolit spolusprávu, začněte tady a odblokujte technické obavy, které máte.

| | | |
|-|-|-|
| <a name="bkmk_paths"></a>**Cesty ke spolusprávě** | Existují dva základní způsoby, jak můžete nastavit spolusprávu a je důležité pochopit požadavky na jednotlivé cesty.  Každá cesta vyžaduje určitou kombinaci služby Azure AD, ConfigMgr, Intune a klienta Windows. | [![Miniatura snímku cest spolusprávy](media/thumbnail-paths.png)](quickstart-paths.md) |
| <a name="bkmk_setup-hybrid-aad"></a>**Nastavení hybridní služby Azure AD** | Pokud má vaše prostředí v současnosti zařízení s Windows 10 připojená k doméně, nastavte hybridní službu Azure AD, aby bylo možné povolit spolusprávu. | [![Miniatura nastavení hybridního videa pro Azure AD](media/thumbnail-setup-azure-ad.png)](quickstart-setup-hybrid-aad.md) |
| <a name="bkmk_upgrade-win10"></a>**Upgrade na Windows 10** | Pro spolusprávu se vyžaduje Windows 10 verze 1709 nebo novější. | [![Miniatura upgradu videa s Windows 10](media/thumbnail-upgrade-win10.png)](quickstart-upgrade-win10.md) |
| <a name="bkmk_fasttrack"></a>**Získat pomoc z FastTrack** | Organizace FastTrack je velkou skupinou techniků Microsoftu, kteří se specializují na pomoc všem typům organizací, které nasazují Microsoft 365 aplikace, včetně nastavení spolusprávy. | [![Miniatura videa FastTrack](media/thumbnail-fasttrack.png)](quickstart-fasttrack.md) |
