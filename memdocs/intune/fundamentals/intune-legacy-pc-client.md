---
title: Starší verze klienta Intune pro počítače a Intune v Azure
description: Co potřebujete zvážit při používání Intune v Azure ke správě zařízení s Windows ve vaší organizaci.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/15/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid: 1f104923-12df-453c-9c20-942ef65a0945
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 41b5b4116359864c4d1251515d29005b9d9af425
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82077933"
---
# <a name="intune-on-azure-console-and-legacy-intune-pc-client"></a>Intune v konzole Azure a starší verze klienta Intune pro počítače

Intune využívá architekturu aplikační služby SaaS založenou na Azure. Azure poskytuje významná vylepšení ve škálování, kapacitě a výkonu. Tato možnost nabízí vylepšené prostředí pro správu Intune a optimalizované pracovní postupy v Azure Portal. 

Pokud ke správě zařízení s Windows ve vaší organizaci používáte Intune v Azure, vezměte v úvahu následující body:

## <a name="manage-windows-10-devices-by-using-mdm"></a>Správa zařízení s Windows 10 pomocí MDM

Doporučujeme vám použít [Mobile Device Management (MDM) ke správě zařízení s Windows 10](../configuration/device-restrictions-windows-10.md) místo starší verze klienta Intune v osobním počítači. Funkce správy Windows 10 pomocí MDM je k dispozici v Intune na portálu Azure Portal. Správa Windows 10 MDM poskytuje mnoho nových funkcí správy a zabezpečení, které nejsou k dispozici ve starší verzi klienta Intune v osobním počítači.

## <a name="legacy-pc-client-features-are-only-available-in-the-silverlight-console"></a>Funkce starší verze klienta v osobním počítači jsou dostupné jenom v konzole Silverlight.

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

Pracovní postupy správy klienta Intune v osobním počítači používají [konzolu pro správu Intune založenou na technologii Silverlight](https://manage.microsoft.com/), což má následující důsledky:

- Pro všechny úkoly správy bez skupin s využitím klienta Intune v osobním počítači musíte používat konzolu Silverlight.
- Při správě skupin je nutné použít [Intune na portálu Azure Portal](https://portal.azure.com/). Tento požadavek existuje, protože nyní Intune místo starší verze skupin Intune používá skupiny Azure AD. 

Z důvodu přepnutí do skupin Azure AD se mírně změnily filtrování "na základě skupin" v zobrazení řídicího panelu konzoly Silverlight. Pokud chcete filtrovat v aktualizovaném uživatelském rozhraní Silverlight, postupujte takto:

1. Vyberte zobrazení.
2. V okně **Filtry** zadejte název skupiny, podle které chcete filtrovat, a stiskněte Enter. Vyfiltruje se zobrazení seznamu zařízení v dané skupině.

   ![Vstupní rozevírací seznam filtru s vybraným None](./media/intune-legacy-pc-client/image01.png)


## <a name="continue-to-manage-windows-7-by-using-intune-pc-client"></a>Správa Windows 7 i nadále pomocí klienta Intune v osobním počítači

V případě systému Windows 7, který nejde spravovat pomocí MDM, budeme dál podporovat stávající možnosti klientských počítačů Intune jenom v konzole Silverlight. Zvažte přechod na správu MDM při upgradu na Windows 10.

## <a name="mdm-capabilities"></a>Funkce MDM

Podrobné porovnání možností klienta v osobním počítači a MDM najdete v tématu [Porovnání správy počítačů s Windows jako osobních počítačů nebo jako mobilních zařízení](pc-management-comparison.md). Aktualizace MDM budou nadále přinášet nové možnosti správy zařízení s Windows 10 zaregistrovaných v MDM včetně vyhodnocení možnosti pro aplikace Win 32. Podívejte se, [co je nového](whats-new.md) pro nejnovější doplňky pro vydání služby.

## <a name="switch-from-pc-client-to-mdm"></a>Přechod z klienta v počítači na MDM

Pokud chcete ve správě zařízení s Windows 10 přejít z klienta Intune v osobním počítači na správu pomocí MDM, postupujte takto:

1. V konzole Silverlight proveďte **selektivní vymazání**, abyste zrušili registraci zařízení klienta v osobním počítači.
  ![Místní nabídka upozornění s vybraným přepínačem selektivního vymazání zařízení](./media/intune-legacy-pc-client/image02.png)
2. Zařízení znovu zaregistrujte pomocí [MDM (nebo Azure AD Join)](../enrollment/windows-enroll.md).

## <a name="next-steps"></a>Další kroky
[Registrace zařízení s Windows](../enrollment/windows-enroll.md)
