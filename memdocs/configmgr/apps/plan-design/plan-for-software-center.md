---
title: Plánování Centra softwaru
titleSuffix: Configuration Manager
description: Rozhodněte, jak chcete nakonfigurovat a označit Centrum softwaru, aby mohli uživatelé pracovat s Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c6826794-aa19-469d-ae47-1a0db68a1ff1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5b32fc2de3c945ff2292f119a10d84d982d08677
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127354"
---
# <a name="plan-for-software-center"></a>Plánování Centra softwaru

*Platí pro: Configuration Manager (Current Branch)*

Uživatelé mění nastavení, vyhledávají aplikace a instalují aplikace z centra softwaru. Nainstalujete-li klienta Configuration Manager do zařízení se systémem Windows, aplikace automaticky nainstaluje také centrum softwaru.

Další informace o dalších funkcích centra softwaru najdete v [uživatelské příručce centra softwaru](../../core/understand/software-center.md).  

## <a name="configure-software-center"></a><a name="bkmk_userex"></a>Konfigurace centra softwaru  

Pokud chcete využívat nejnovější funkce centra softwaru, aktualizujte své Configuration Manager weby a klienty na verzi 1906 nebo novější.

> [!IMPORTANT]
> Tato iterativní vylepšení centra softwaru a bodu správy slouží k vyřazení rolí katalogu aplikací.
>
> - Uživatelské prostředí Silverlight není pro aktuální větev verze 1806 podporováno.
> - Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací.
> - Podpora končí pro role katalogu aplikací s verzí 1910.

- Nastavení klienta **používat nové centrum softwaru** ve skupině **Počítačový agent** je ve výchozím nastavení povolené. Předchozí verze centra softwaru už není podporovaná. Další informace najdete v tématu [odebrané a zastaralé funkce](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

- Určete viditelnost odkazu webu Katalog aplikací na kartě **stav instalace** v centru softwaru. Další informace najdete v tématu Nastavení klienta [centra softwaru](../../core/clients/deploy/about-client-settings.md#software-center) .

- Počínaje verzí 1906 můžete přidat až pět vlastních karet do centra softwaru. Další informace najdete v tématu [nastavení klienta centra softwaru](../../core/clients/deploy/about-client-settings.md#software-center). <!--4063773-->

- Uživatelé můžou nakonfigurovat spřažení zařízení a uživatele v centru softwaru. Další informace najdete v tématu [propojení uživatelů a zařízení pomocí spřažení uživatelských zařízení](../deploy-use/link-users-and-devices-with-user-device-affinity.md).

> [!IMPORTANT]
> Pokud chcete využívat nové funkce Configuration Manager, nejdřív aktualizujte klienty na nejnovější verzi. I když se nové funkce zobrazí v konzole Configuration Manager, když aktualizujete lokalitu a konzolu, kompletní scénář nebude funkční, dokud nebude verze klienta zároveň nejnovější.

### <a name="software-center-and-user-available-applications"></a>Centrum softwaru a aplikace dostupné pro uživatele

- Role katalogu aplikací nejsou nutné k zobrazení aplikací dostupných uživatelům v centru softwaru. Toto chování pomáhá snižovat serverovou infrastrukturu potřebnou k doručování aplikací uživatelům. Centrum softwaru spoléhá na to, že bod správy získá tyto informace, což pomáhá lépe škálovat větší prostředí tím, že je přiřadí ke [skupinám hranic](../../core/servers/deploy/configure/boundary-groups.md#management-points).<!--1358309-->

- Uživatelé můžou procházet a instalovat aplikace dostupné pro uživatele na zařízeních, která jsou připojená k Azure Active Directory (Azure AD). Počínaje verzí 2006 můžou aplikace dostupné uživatelům získat na internetových zařízeních připojených k doméně. Další informace najdete v tématu [nasazení aplikací dostupných pro uživatele](../deploy-use/deploy-applications.md#deploy-user-available-applications).

- Od verze 1906 Centrum softwaru komunikuje s bodem správy pro aplikace cílené na uživatele jako dostupné. Katalog aplikací už nepoužívá. Tato změna usnadňuje odebrání katalogu aplikací z lokality nástroje.

- Dříve Centrum softwaru vybralo první bod správy ze seznamu dostupných serverů. Počínaje verzí 1906 používá stejný bod správy, který klient používá. Tato změna umožňuje centru softwaru použít stejný bod správy z přiřazené primární lokality jako klienta.

## <a name="replace-toast-notifications-with-dialog-window"></a><a name="bkmk_impact"></a>Nahradit informační zprávy pomocí dialogového okna

<!--3555947-->
Někdy se uživatelům nezobrazuje zpráva informující o systému Windows o restartování nebo požadovaném nasazení. Pak nevidí prostředí, které připomíná připomenutí k odložení. Toto chování může vést k nedostatečnému uživatelskému prostředí, když klient dosáhne konečného termínu.

Od verze 1902 platí, že když [se vyžadují změny softwaru](#software-changes-are-required) , nebo nasazení [potřebují restartovat](#restart-required), máte možnost použít více rušivých dialogových oken.

### <a name="software-changes-are-required"></a>Jsou vyžadovány změny softwaru

Když [nasadíte aplikaci](../deploy-use/deploy-applications.md) podle potřeby s konečným termínem v budoucnu, na stránce **činnost koncového uživatele** v Průvodci nasazením softwaru vyberte následující možnosti oznámení uživateli:

- **Zobrazit v nástroji Software Center a zobrazit všechna oznámení**
- **Když se vyžadují změny softwaru, zobrazí se uživateli dialogové okno namísto informačního oznámení.**

Konfigurace tohoto nastavení nasazení změní činnost koncového uživatele pro tento scénář.

Z následujících informačních zpráv:

![Informační zpráva oznamující, že jsou požadovány změny softwaru](media/3555947-required-toast.png)  

Do následujícího okna:

![Dialogové okno pro požadované změny softwaru](media/3555947-required-dialog.png)


### <a name="restart-required"></a>Vyžadováno restartování

V okně [restartovat počítač](../../core/clients/deploy/about-client-settings.md#computer-restart) v nastavení klienta Povolte následující možnost: **Pokud nasazení vyžaduje restart, místo oznámení informačního systému se zobrazí dialogové okno s uživatelem**.  

Konfigurace tohoto nastavení klienta změní činnost koncového uživatele pro všechna požadovaná nasazení, která vyžadují restartování následujících typů:

- [Aplikace](../deploy-use/deploy-applications.md)
- [Pořadí úkolů](../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [Aktualizace softwaru](../../sum/deploy-use/deploy-software-updates.md)

Z následujících informačních zpráv:

![Informační zpráva oznamující, že je vyžadováno restartování](media/3555947-restart-toast.png)  

Do následujícího okna:

![Dialogové okno pro restartování počítače](media/3555947-restart-dialog.png)

> [!IMPORTANT]
> V Configuration Manager 1902 se za určitých okolností dialogová okna nebudou nahrazena informačními oznámeními. Pokud chcete tento problém vyřešit, nainstalujte [kumulativní aktualizaci pro Configuration Manager verze 1902](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902). <!--4404715-->

## <a name="brand-software-center"></a>Branding – Centrum softwaru

Změňte vzhled centra softwaru, aby splňoval požadavky vaší organizace na branding. Tato konfigurace pomáhá uživatelům důvěřovat centru softwaru.

### <a name="configure-software-center-branding"></a>Konfigurace brandingu centra softwaru

<!-- 1351224 -->
Přizpůsobte vzhled centra softwaru tím, že přidáte prvky značky vaší organizace a určíte viditelnost karet.

Další informace najdete v následujících článcích:

- Skupina [centra softwaru](../../core/clients/deploy/about-client-settings.md#software-center) nastavení klienta  
- [Postup konfigurace nastavení klienta](../../core/clients/deploy/configure-client-settings.md)  

### <a name="branding-priorities"></a>Priority brandingu

Configuration Manager aplikuje vlastní branding pro Centrum softwaru podle následujících priorit:  

1. Nastavení klienta **centra softwaru** . Další informace najdete v tématu [informace o nastavení klienta](../../core/clients/deploy/about-client-settings.md#software-center).  

2. Nastavení klienta **názvu organizace** ve skupině **Počítačový agent** . Další informace najdete v tématu [informace o nastavení klienta](../../core/clients/deploy/about-client-settings.md#computer-agent).  

#### <a name="application-catalog-branding-priorities"></a>Priority značky Application Catalog

> [!IMPORTANT]
> Uživatelské prostředí programu Silverlight v katalogu aplikací není v aktuální větvi verze 1806 podporováno. Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací. Podpora končí pro role katalogu aplikací s verzí 1910.  

Pokud používáte katalog aplikací, branding se řídí těmito prioritami:  

1. Nastavení klienta **centra softwaru** . Další informace najdete v tématu [informace o nastavení klienta](../../core/clients/deploy/about-client-settings.md#software-center).  

2. *Název organizace* a *Barva* , které zadáte ve vlastnostech bodu webu Katalog aplikací. Další informace najdete v tématu [Možnosti konfigurace pro bod webu Katalog aplikací](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).  

3. Nastavení klienta **názvu organizace** ve skupině **Počítačový agent** . Další informace najdete v tématu [informace o nastavení klienta](../../core/clients/deploy/about-client-settings.md#computer-agent).  

## <a name="see-also"></a>Viz také

- [Uživatelská příručka Centra softwaru](../../core/understand/software-center.md)
- [Plánování a konfigurace správy aplikací](plan-for-and-configure-application-management.md)
