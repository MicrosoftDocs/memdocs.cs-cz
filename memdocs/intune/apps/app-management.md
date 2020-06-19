---
title: Co je správa aplikací v Microsoft Intune?
titleSuffix: ''
description: Seznamte se s možnostmi správy klientských aplikací podle platformy pro Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/31/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1975a2dc-3a14-4cb9-9afb-e2ba01a1c51b
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 617c6b89bfc52d926e2ddb422c36db39edec6908
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093037"
---
# <a name="what-is-microsoft-intune-app-management"></a>Co je správa aplikací v Microsoft Intune?


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Jako správce IT můžete Microsoft Intune použít ke správě klientských aplikací, které používají pracovníci vaší společnosti. Tato funkce doplňuje správu zařízení a ochranu dat. Jednou z priorit správce je zajistit, aby koncoví uživatelé měli přístup k aplikacím, které potřebují ke své práci. To může být náročné z těchto důvodů:
- Existuje široký sortiment platforem zařízení a typů aplikací.
- Potřebujete spravovat aplikace na firemních zařízeních i na osobních zařízeních uživatelů.
- Musíte zajistit zabezpečení sítě a dat.

Navíc potřebujete přiřazovat a spravovat aplikace na zařízeních, která nejsou zaregistrovaná v Intune.

## <a name="mobile-application-management-mam-basics"></a>Základní informace o správě mobilních aplikací (MAM)

[Správa mobilních aplikací (MAM) Intune](app-lifecycle.md) představuje sadu funkcí Intune pro správu, s kterými můžete publikovat, doručovat, konfigurovat, zabezpečovat, monitorovat a aktualizovat mobilní aplikace pro uživatele.

MAM umožňuje spravovat a chránit data vaší organizace v rámci aplikace. S **mam bez registrace** (MAM-We) je možné spravovat pracovní nebo školní aplikaci, která obsahuje citlivá data, a to téměř na jakémkoli [zařízení](app-management.md#app-management-capabilities-by-platform), včetně osobních zařízení ve scénářích **Přineste si vlastní zařízení** (BYOD). Mnoho kancelářských aplikací, například aplikace Microsoft Office, lze spravovat přes Intune MAM. Podívejte se na oficiální seznam [Microsoft Intune chráněných aplikací](apps-supported-intune-apps.md) , které jsou k dispozici pro veřejné použití.

Intune MAM podporuje dvě konfigurace:
- **MDM+MAM Intune**: Správci IT můžou spravovat aplikace pomocí MAM a zásad ochrany aplikací jenom na zařízeních, která jsou zaregistrovaná ve správě mobilních zařízení (MDM) Intune. Pokud zákazníci chtějí spravovat aplikace pomocí MDM + MAM, měli by používat konzolu Intune na portálu Azure Portal na https://portal.azure.com.
- **MAM bez registrace zařízení:** MAM bez registrace zařízení, neboli MAM-WE, umožňuje správcům IT spravovat aplikace pomocí MAM a zásad ochrany aplikací na zařízeních, která nejsou zaregistrovaná ve správě mobilních zařízení Intune. To znamená, že aplikace je možné spravovat pomocí Intune na zařízeních, která jsou zaregistrovaná u jiných poskytovatelů EMM. Pokud zákazníci chtějí spravovat aplikace pomocí MAM-WE, měli by používat konzolu Intune na portálu Azure Portal na https://portal.azure.com. Aplikace je také možné spravovat pomocí Intune na zařízeních zaregistrovaných pomocí jiných poskytovatelů správy firemních mobilních zařízení (Enterprise Mobility Management (EMM)) nebo na zařízeních vůbec v MDM nezaregistrovaných. Další informace o BYOD a EMS Microsoftu najdete v tématu o [technologických rozhodnutích pro povolení BYOD s Microsoft Enterprise mobility + Security (EMS)](../fundamentals/byod-technology-decisions.md).

## <a name="app-management-capabilities-by-platform"></a>Funkce správy aplikací podle platformy

Intune nabízí celou řadu funkcí, které vám pomůžou dostat požadované aplikace na zařízení, na kterých je chcete spouštět. Následující tabulka nabízí souhrn funkcí správy aplikací.

|  | Android/Android Enterprise | iOS/iPadOS | macOS | Windows 10 | Windows Phone 8.1 |
|-------------------------------------------------------------------------------------|---------|-----|-------|------------|-------------------|
| Přidání a přiřazení aplikací k zařízením a uživatelům | Ano | Ano | Ano | Ano | Ano |
| Přiřazení aplikací k zařízením nezaregistrovaným v Intune | Ano | Ano | Ne | Ne | Ne |
| Určení chování aplikací při spuštění pomocí zásad konfigurace aplikací | Ano | Ano | Ne | Ne | Ne |
| Obnovení aplikací s vypršelou platností pomocí zásad zřizování mobilních aplikací | No | Ano | Ne | Ne | Ne |
| Ochrana firemních dat v aplikacích pomocí zásad ochrany aplikací | Ano | Ano | Ne | Ne <sup>1</sup> | Ne |
| Odebrání pouze firemních dat z nainstalovaných aplikací (selektivní vymazání aplikací) | Ano | Ano | No | Ano | Ano |
| Monitorování přiřazení aplikací | Ano | Ano | Ano | Ano | Ano |
| Přiřazení a sledování aplikací hromadně zakoupených v obchodu s aplikacemi | Ne | Ne | Ne | Ano | Ne |
| Povinná instalace aplikací na zařízení (povinné) <sup>2</sup> | Ano | Ano | Ano | Ano | Ano |
| Nepovinná instalace na zařízení z Portálu společnosti (dostupná instalace) | Ano <sup>3</sup> | Ano | Ano | Ano | Ano |
| Zástupce pro instalaci aplikace na webu (webový odkaz) | Ano <sup>4</sup> | Ano | Ano | Ano | Ano |
| Vlastní (obchodní) aplikace | Ano | Ano | Ano | Ano | Ne |
| Aplikace z obchodu | Ano | Ano | Ne | Ano | Ano |
| Aktualizace aplikací | Ano | Ano | Ne | Ano | Ano |

<sup>1</sup> Při ochraně aplikací na zařízeních s Windows 10 uvažujte o použití funkce [Windows Information Protection](../protect/windows-information-protection-configure.md).<br>
<sup>2</sup> Platí jen pro zařízení spravovaná přes Intune.<br>
<sup>3</sup> Intune podporuje dostupné aplikace ze spravovaného Google Play Storu na zařízeních s Androidem Enterprise.<br>
<sup>4</sup> Intune neposkytuje instalaci zástupce aplikace jako webového odkazu na standardní zařízení s Androidem Enterprise. Podpora webových odkazů je ale k dispozici pro [vyhrazená podniková zařízení s Androidem pro více aplikací](../configuration/device-restrictions-android-for-work.md#device-experience). 


## <a name="get-started"></a>Začínáme

Většinu informací týkajících se aplikací najdete v úloze **aplikace** , ke kterým máte přístup pomocí následujících kroků:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Vyberte **aplikace**.

    ![Podokno úloh aplikace](./media/app-management/apps-workload.png)

Úlohy aplikací poskytují odkazy na přístup k běžným informacím a informacím o aplikaci. 

Horní část navigační nabídky úlohy aplikace poskytuje běžně používané podrobnosti o aplikaci:
- **Přehled**: tuto možnost vyberte, pokud chcete zobrazit název tenanta, autoritu MDM, umístění tenanta, stav účtu, stav instalace aplikace a stav zásad ochrany aplikací.
- **Všechny aplikace**: tuto možnost vyberte, pokud chcete zobrazit seznam všech dostupných aplikací. Z této stránky můžete přidat další aplikace. Kromě toho můžete zobrazit stav jednotlivých aplikací a také to, jestli jsou jednotlivé aplikace přiřazené. Další informace najdete v tématu věnovaném [přidávání aplikací](apps-add.md) a [přiřazování aplikací](apps-deploy.md).
- **Monitorování aplikací**
    - **Licence aplikací**: Tady můžete zobrazit, přiřadit a monitorovat aplikace hromadně zakoupené v obchodech s aplikacemi. Další informace najdete v tématu [aplikace VPP (Volume koupené programy)](vpp-apps-ios.md) a [Microsoft Store pro hromadně zakoupené aplikace](windows-store-for-business.md).
    - **Zjištěné aplikace**: zobrazí aplikace, které byly přiřazeny přes Intune nebo nainstalované na zařízení. Další informace najdete v tématu [zjištěné aplikace Intune](app-discovered-apps.md).
    - **Stav instalace aplikace**: Podívejte se na stav přiřazení aplikace, které jste vytvořili. Další informace najdete v článku [Monitorování informací a přiřazení aplikace pomocí Microsoft Intune](apps-monitor.md#device-and-user-status-graphs).
    - **Stav ochrany aplikací**: Tady můžete zobrazit stav zásad ochrany aplikací pro vámi vybraného uživatele.
- **Podle platformy**: výběrem těchto platforem zobrazíte dostupné aplikace podle platformy.
    - Windows
    - iOS
    - macOS
    - Android
- **Zásada**:
    - **Zásady ochrany aplikací**: Tuto možnost vyberte, pokud chcete aplikaci přidružit nastavení pomáhající chránit firemní data, která tato aplikace používá. Můžete například omezit možnosti komunikace aplikace s jinými aplikacemi nebo vyžadovat, aby uživatel při přístupu k firemní aplikaci zadal PIN kód. Další informace najdete v tématu [Zásady ochrany aplikací](app-protection-policies.md).
    - **Zásady konfigurace aplikací**: Tuto možnost vyberte k poskytování nastavení, která se můžou požadovat, když uživatel spustí aplikaci. Další informace najdete v tématech [zásady konfigurace aplikací](app-configuration-policies-use-ios.md), [zásady konfigurace aplikací pro iOS](app-configuration-policies-use-ios.md)a [zásady konfigurace aplikací pro Android](app-configuration-policies-overview.md).
    - **Zřizovací profily aplikací pro iOS**: Aplikace pro iOS obsahují zřizovací profil a kód, který je podepsaný certifikátem. Když tomuto certifikátu vyprší platnost, není možné aplikaci spustit. Intune poskytuje nástroje pro proaktivní přiřazení nových zásad zřizovacího profilu k zařízením s aplikacemi, kterým brzy vyprší platnost. Další informace najdete v tématu [zřizovací profily aplikací pro iOS](app-provisioning-profile-ios.md).
    - **Doplňkové zásady v režimu S**: tuto možnost vyberte, pokud chcete, aby se ve spravovaných zařízeních v režimu spouštěly další aplikace. Další informace najdete v tématu [doplňkové zásady pro režim S](apps-win32-s-mode.md).
    - **Sady zásad**: tuto možnost vyberte, pokud chcete vytvořit přiřazenou kolekci aplikací, zásad a dalších objektů pro správu, které jste vytvořili. Další informace najdete v tématu [sady zásad](../fundamentals/policy-sets.md).
- **Jiné**:   
    - **Selektivní vymazání aplikace**: Tuto možnost vyberte, pokud chcete odebrat pouze firemní data z vybraného zařízení uživatele. Další informace najdete v tématu [selektivní vymazání aplikace](apps-selective-wipe.md).
    - **Kategorie aplikací**: Tady můžete přidat, připnout a odstranit názvy kategorií aplikací.
    - **Elektronické knihy**: v některých obchodech s aplikacemi máte možnost koupit si pro aplikace nebo knihy, které chcete používat ve vaší společnosti, více licencí. Podrobnosti najdete v tématu [Správa aplikací a knih zakoupených v rámci multilicenčního programu pomocí Microsoft Intune](vpp-apps.md).
- **Nápověda a podpora**: Tady můžete řešit potíže, požádat o podporu nebo zobrazit stav Intune. Další informace najdete v tématu [řešení problémů](../fundamentals/help-desk-operators.md).

### <a name="try-the-interactive-guide"></a>Vyzkoušejte interaktivní příručku
Interaktivní příručka [Spravovat a chránit mobilní a desktopové aplikace Microsoft Endpoint Manager](https://mslearn.cloudguides.com/en-us/guides/Manage%20and%20protect%20mobile%20and%20desktop%20applications%20with%20Microsoft%20Endpoint%20Manager) vás provede centrem pro správu Microsoft Endpoint Manageru, která vám ukáže, jak spravovat zařízení zaregistrovaná v Intune, vymáhat dodržování zásad a chránit data vaší organizace.</br></br>

> [!VIDEO https://mslearn.cloudguides.com/en-us/guides/Manage%20and%20protect%20mobile%20and%20desktop%20applications%20with%20Microsoft%20Endpoint%20Manager]

## <a name="additional-information"></a>Další informace
Následující položky v konzole poskytují funkce související s aplikacemi:
- **Microsoft Store pro firmy**: Tady můžete nastavit integraci do Microsoft Storu pro firmy. Potom můžete zakoupené aplikace synchronizovat s Intune, přiřazovat je a sledovat využití licencí. Další informace najdete v tématu [Microsoft Store pro hromadně zakoupené aplikace](windows-store-for-business.md).
- **Certifikát Windows Enterprise**: Tady můžete použít nebo zobrazit stav certifikátu pro podepisování kódu, který se používá k distribuci obchodních aplikací do spravovaných zařízení s Windows.
- **Certifikát Windows Symantec**: Tady můžete použít nebo zobrazit stav certifikátu Symantec pro podepisování kódu, který je nutný k distribuci souborů appx pro XAP a WP8.x na zařízení s Windows 10 Mobile.
- **Klíče pro instalaci bokem ve Windows**: Přidejte klíč pro instalaci bokem ve Windows, který lze použít k instalaci aplikace přímo do zařízení (místo publikování aplikace a jejího stahování z Windows Storu). Další informace najdete v části [strana načítající aplikaci pro Windows](app-sideload-windows.md).
- **Tokeny programu Apple VPP**: použít a zobrazit licence VPP (Volume purchase program) pro iOS/iPadOS. Další informace najdete v tématu [hromadně zakoupené aplikace pro iOS/iPadOS](vpp-apps-ios.md).
- **Managed Google Play**: spravovaná Google Play je podniková aplikace pro Google Store a výhradně zdroj aplikací pro Android Enterprise. Další informace najdete v tématu [Přidání spravovaných Google Play aplikací do zařízení s Androidem Enterprise pomocí Intune](apps-add-android-for-work.md).
- **Přizpůsobení**: přizpůsobte portál společnosti, abyste mu poskytovali značku vaší společnosti. Další informace najdete v tématu [konfigurace portál společnosti](company-portal-app.md).

Další informace o aplikacích najdete v tématu [Přidání aplikací do Microsoft Intune](../apps/apps-add.md).

## <a name="next-steps"></a>Další kroky

- [Přidání aplikace do Microsoft Intune](apps-add.md)
