---
title: Desktop Analytics
titleSuffix: Configuration Manager
description: Přehled služby Desktop Analytics integrované s Configuration Manager.
ms.date: 03/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: b280661c4de9282d3907b7d480477fc67f6a8dc5
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/24/2020
ms.locfileid: "83824060"
---
# <a name="what-is-desktop-analytics"></a>Co je Desktop Analytics?

Desktop Analytics je cloudová služba, která se integruje s Configuration Manager. Služba poskytuje přehled a inteligentní informace, které vám pomohou s rozhodováním o připravenosti na aktualizace svých klientů s Windows. Kombinuje data z vaší organizace s daty agregovanými z milionů zařízení připojených ke cloudovým službám Microsoftu.

Použití aplikace Desktop Analytics s Configuration Manager:  

- Vytvoření inventáře aplikací běžících ve vaší organizaci  

- Posouzení kompatibility aplikací s nejnovějšími aktualizacemi funkcí Windows 10  

- Identifikujte problémy s kompatibilitou a získejte návrhy na zmírnění na základě cloudových dat s podporou cloudu  

- Vytváření pilotních skupin, které reprezentují celou aplikaci a ovladače v rámci minimální sady zařízení  

- Nasazení Windows 10 do pilotního nasazení a zařízení spravovaných výrobou  

![Snímek obrazovky domovské stránky Desktop Analytics v Azure Portal](media/portal-home.png)

Následující video je relace z Ignite 2019, která obsahuje další informace o Desktop Analytics:

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3085]

[Využití desktopových analýz a Configuration Manager ke snížení celkových nákladů na vlastnictví Windows prostřednictvím přehledů na základě dat pro správu, údržbu a podporu](https://myignite.techcommunity.microsoft.com/sessions/81689?source=sessions)

Přeskočte na 10:00 pro podrobnou ukázku.

> [!Note]  
> Desktop Analytics je následníkem Windows Analytics, který vychází z 31. ledna 2020.
>
> Schopnosti služby Windows Analytics jsou kombinovány ve službě Desktop Analytics. Desktop Analytics je taky úzce integrovaný s Configuration Manager. Další informace najdete v tématu [Nejčastější dotazy pro zákazníky s Windows Analytics](faq.md#existing-windows-analytics-customers).

## <a name="benefits"></a>Výhody

Mnohé zákazníky mají problémy s tím, že se s Windows 10 dostávají a zabývají aktuálními. Primární výzvou testuje aplikace. Tento proces je obvykle ruční. Pro správce IT a vlastníky aplikací je časově náročné, aby mohli průběžně analyzovat stávající aplikace. Pak opravte všechny problémy, které vznikají.

Desktop Analytics nabízí následující výhody:

- **Inventář zařízení a softwaru**: inventarizace klíčových faktorů, jako jsou aplikace a verze Windows.  

- **Identifikace pilotního projektu**: identifikace nejmenší sady zařízení, která poskytují nejširší pokrytí faktorů. Zaměřuje se na faktory, které jsou nejdůležitější pro pilotní nasazení upgradů a aktualizací Windows. Zajištění úspěšnosti pilotního nasazení vám umožní rychleji a bez obav pokračovat v jejich širším nasazení v produkčním prostředí.  

- **Identifikace problému**: pomocí agregovaných tržních dat spolu s daty z vašeho prostředí předpovídá možné problémy s tím, že se budou v systému Windows získávat a předávat aktuální údaje. Pak navrhuje možná omezení rizik.  

- **Configuration Manager Integration**: Cloud služby – umožňuje vaši stávající místní infrastrukturu. Tato data a analýza použijte k nasazení a správě Windows na svých zařízeních.  

## <a name="prerequisites"></a>Požadavky

Pokud chcete použít desktopovou analýzu, ujistěte se, že vaše prostředí splňuje následující požadavky.

### <a name="technical"></a>Technické

- Aktivní globální předplatné Azure s oprávněními [globálního správce](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions) . [Účty Microsoft](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts) se nepodporují.  

    > [!Important]  
    > Služba Desktop Analytics v současnosti vyžaduje, abyste nasadili službu Office 365 v tenantovi Azure AD. To v budoucnu nebude mít žádný požadavek.

    - Oprávnění **vlastníka pracovního prostoru** k **Nastavení pracovního prostoru**a následujících rolí:  

      - Role [**správce pro Desktop Analytics**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions) .

      - [**Log Analytics Přispěvatel**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor) a [**Správce přístupu uživatelů**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) ve skupině prostředků, aby používaly existující pracovní prostor nebo vytvořil nový pracovní prostor v existující skupině prostředků.

      - Oprávnění [**vlastníka**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner)nebo [**Přispěvatel**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) a [**Správce přístupu uživatele**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) k předplatnému k vytvoření pracovního prostoru v nové skupině prostředků.  

    - Pokud chcete mít přístup k portálu po registraci, budete potřebovat:

      - Role a [**vlastník**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) [**správce stolního počítače**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions) , nebo oprávnění [**přispěvatele**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) u skupiny prostředků, ve které se pracovní prostor vytvořil.

- Configuration Manager verze 1902 s kumulativní aktualizací (4500571) nebo novější. Další informace najdete v tématu [aktualizace Configuration Manager](connect-configmgr.md#bkmk_hotfix).  

    - Role [**úplného správce**](../core/understand/fundamentals-of-role-based-administration.md#bkmk_Planroles) v Configuration Manager  

    > [!NOTE]
    > Funkce Desktop Analytics podporuje vytváření sestav několika hierarchií Configuration Manager do jednoho tenanta služby Azure AD.<!-- 4814075 --> Pokud máte ve svém prostředí více hierarchií, máte následující možnosti:
    >
    > - Používejte odlišná komerční ID a klienty Azure AD.
    > - Nakonfigurujte obě hierarchie tak, aby používaly stejné komerční ID ke sdílení instance Azure AD tenant a Desktop Analytics. Pro připojení jednotlivých hierarchií použijte [různé aplikace](connect-configmgr.md#bkmk_connect) . Může trvat až 30 dnů od odpojení hiearchy, aby se změny projevily na portálu. 

- Zařízení se systémem Windows 7, Windows 8.1 nebo Windows 10  

    - Nainstalujte nejnovější aktualizace. Další informace najdete v tématu [aktualizace zařízení](enroll-devices.md#update-devices).  

    - Zařízení musí mít také klienta Configuration Manager, verze 1902 s kumulativní aktualizací (4500571) nebo novější. Další informace najdete v tématu [aktualizace Configuration Manager](connect-configmgr.md#bkmk_hotfix).  

    > [!Note]  
    > Desktop Analytics nepodporuje upgrady na kanál pro dlouhodobé obsluhy Windows 10 (LTSC). Další informace najdete v tématu [Přehled služby Windows as](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).
    >
    > Desktop Analytics je navržený tak, aby nejlépe podporoval scénář místního upgradu. Pokud potřebujete provést významné změny, jako je například z 32-bitové architektury na 64, použijte scénář pro vytváření imagí. Přehledy Desktop Analytics jsou v těchto scénářích nasazení klasického operačního systému stále důležité, ale můžete ignorovat konkrétní pokyny pro upgrade na místě. Další informace najdete v tématu [scénáře nasazení podnikových operačních systémů pomocí Configuration Manager](../osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems.md).

- Diagnostická data systému Windows. Další informace najdete v následujících článcích:  

    - [Úrovně diagnostických dat](enable-data-sharing.md#diagnostic-data-levels)  

    - [Ochrana osobních údajů Desktop Analytics](privacy.md)  

- Síťové připojení ze zařízení k veřejnému cloudu Microsoftu. Další informace najdete v tématu [Povolení sdílení dat](enable-data-sharing.md) .  

> [!Important]
> Microsoft má silné závazky na poskytování nástrojů a prostředků, které vám povedou kontrolu nad vaším soukromím. V důsledku toho společnost Microsoft neshromažďuje následující data ze zařízení umístěných v zemích Evropské země (EHP a Švýcarsko):
>
> - Diagnostická data Windows ze zařízení Windows 8.1
> - Data o využití aplikací pro Windows 7

### <a name="licensing-and-costs"></a>Licencování a náklady

- Aktivní globální předplatné Azure.

    > [!NOTE]
    > Většina odpovídajících předplatných pro Configuration Manager taky zahrnuje Azure AD. Příklad najdete v tématu [plány Microsoft 365](https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans) a [Enterprise mobility + Security licencování](https://www.microsoft.com/licensing/product-licensing/enterprise-mobility-security).

- Zařízení zaregistrovaná v Desktop Analytics potřebují platnou licenci Configuration Manager. Další informace najdete v tématu [Configuration Manager licencování](../core/understand/product-and-licensing-faq.md).

- Uživatelé zařízení potřebují jednu z následujících licencí:

  - Windows 10 Enterprise E3 nebo E5 (zahrnuté ve Microsoft 365 F3, E3 nebo E5)

  - Windows 10 školství a3 nebo A5 (zahrnuté do Microsoft 365 a3 nebo A5)

  - Přístup k virtuální ploše Windows s přístupem E3 nebo E5  

> [!NOTE]
> Kromě nákladů na tyto licenční předplatné se za použití Desktop Analytics v Azure Log Analytics neúčtují žádné další poplatky. Datové typy ingestované na Desktop Analytics jsou bezplatné a účtují se veškeré Log Analytics a poplatky za uchování dat. Jako nefakturovatelné datové typy nepodléhají tato data ani Log Analytics dennímu limitu pro přijímání dat. Další informace najdete v tématu [Log Analytics využití a náklady](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage).

## <a name="next-steps"></a>Další kroky

Následující kurz nabízí podrobný průvodce Začínáme s desktopovou analýzou a Configuration Manager:
  
> [!div class="nextstepaction"]
> [Pilotní nasazení Windows 10](tutorial-windows10.md)
