---
title: Oznámení konzoly Configuration Manager
titleSuffix: Configuration Manager
description: Přečtěte si o oznámeních z konzoly Configuration Manager.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a0d709fa-c4f8-46e1-b432-582cc293be35
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 12ec788fdf19ec72e954f5a9f229a5a3f95a4610
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129624"
---
# <a name="configuration-manager-console-notifications"></a>Oznámení konzoly Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

<!--3556016, fka 1318035-->
Počínaje verzí 1902 Configuration Manager konzola Configuration Manager upozorní na konkrétní události, ke kterým dojde. U Configuration Managerch webů můžete nakonfigurovat některá oznámení o událostech.

- Nekonfigurovatelná oznámení o událostech:
   - Když je k dispozici aktualizace pro Configuration Manager sebe sama
   - V případě, že dojde k událostem životního cyklu a údržby v prostředí
- Konfigurovatelné oznamování událostí:
   - [Nekritické změny stavu lokality](#bkmk_noncrit)
   - [Zprávy od Microsoftu](#bkmk_msft) (počínaje verzí 2006)

Toto oznámení je pruhem v horní části okna konzoly pod pás karet. Nahrazuje předchozí prostředí, když Configuration Manager aktualizace k dispozici. Tato oznámení v konzole stále zobrazují důležité informace, ale nebrání v práci v konzole nástroje. Nemůžete zavřít kritická oznámení. Konzola zobrazí všechna oznámení v nové oblasti oznámení v záhlaví.

![Oznamovací pruh a příznak v konzole](./media/1318035-notify-eval-version-expired.png)

## <a name="configure-a-site-to-show-non-critical-notifications"></a><a name="bkmk_noncrit"></a>Nakonfigurovat lokalitu, aby zobrazovala Nekritická oznámení

Každou lokalitu můžete nakonfigurovat tak, aby zobrazovala Nekritická oznámení ve vlastnostech lokality.

1. V pracovním prostoru **Správa** rozbalte nabídku **Konfigurace lokality**a pak vyberte uzel **lokality** .
1. Vyberte lokalitu, kterou chcete nakonfigurovat pro Nekritická oznámení.
1. Na pásu karet vyberte možnost **vlastnosti**.
1. Na kartě **výstrahy** vyberte možnost **Povolení oznámení konzoly pro nekritické změny stavu lokality**.
   - Pokud povolíte toto nastavení, všichni uživatelé konzoly uvidí upozornění na kritická, varovná a informační oznámení. Standardně je toto nastavení povolené.  
   - Pokud toto nastavení zakážete, budou se uživatelům konzoly zobrazovat jenom kritická oznámení.  

Většina oznámení konzoly je vázaná na jednu relaci. Konzola vyhodnocuje dotazy, když je uživatel spustí. Chcete-li zobrazit změny v oznámeních, restartujte konzolu. Pokud uživatel zahodí nekritické oznámení, znovu se upozorní, jakmile se konzola restartuje, pokud je stále k dispozici.

Následující oznámení se znovu vyhodnotí každých pět minut:

- Lokalita je v režimu údržby.  
- Lokalita je v režimu obnovení.  
- Lokalita je v režimu upgradu.  

Oznámení se řídí oprávněními pro správu na základě rolí. Pokud například uživatel nemá oprávnění k zobrazení Configuration Manager aktualizace, neuvidí tato oznámení.

Některá oznámení mají související akci. Pokud se například verze konzoly neshoduje s verzí lokality, vyberte **nainstalovat novou verzi konzoly**. Tato akce spustí instalační program konzoly.

Pokud nakonfigurujete služby Azure na Cloud – připojíte se k lokalitě, počínaje verzí 2006, zobrazí se oznámení s akcí [obnovení tajného klíče](../deploy/configure/azure-services-wizard.md#bkmk_renew).<!--6386392--> Lokalita vyhodnocuje stav následujících výstrah jednou za hodinu:

- Brzo vyprší platnost jednoho nebo více tajných klíčů aplikací Azure AD.
- Platnost jednoho nebo více tajných klíčů aplikace Azure AD vypršela.

Pro větev Technical Preview platí následující oznámení:  

- Zkušební verze spadá do 30 dnů od vypršení platnosti (upozornění): aktuální datum spadá do 30 dnů od data vypršení platnosti zkušební verze.  
- Platnost zkušební verze vypršela (kritická): aktuální datum následuje po datu vypršení platnosti zkušební verze.  
- Neshoda verzí konzoly (kritická): verze konzoly neodpovídá verzi lokality.  
- Je k dispozici upgrade lokality (upozornění): je k dispozici nový balíček aktualizace.  

Další informace a pomoc při řešení potíží najdete v souboru **SmsAdminUI. log** v počítači konzoly. Ve výchozím nastavení se tento soubor protokolu nachází v následující cestě: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\AdminUILog\SmsAdminUI.log` .

## <a name="configure-a-site-to-receive-messages-from-microsoft"></a><a name="bkmk_msft"></a>Konfigurace lokality pro příjem zpráv od Microsoftu
 <!--3953121-->

Počínaje verzí 2006 můžete zvolit příjem oznámení od Microsoftu v konzole Configuration Manager. Tato oznámení vám pomůžou udržovat informace o nových nebo aktualizovaných funkcích, změnách Configuration Manager a připojených službách a problémech, které vyžadují nápravu.

### <a name="configure-notification-settings-for-microsoft-messages"></a>Konfigurace nastavení oznámení pro zprávy Microsoftu

1. Přejděte na **Správa**  >  **Konfigurace lokality**  >  **lokality**.
1. Klikněte pravým tlačítkem na lokalitu a vyberte **vlastnosti**.
1. Na kartě **výstrahy** Povolte oznámení výběrem možnosti **přijímat zprávy od společnosti Microsoft**. Můžete zrušit výběr některého z následujících oznámení, pokud jim nepřejete přijímat tyto zprávy:  
   - **Zabránit/opravit**: známé problémy, které mají vliv na vaši organizaci, což může vyžadovat provedení akce.
   - **Plánování změn**: změny Configuration Manager, které mohou vyžadovat, abyste provedli akci.
   - **Průběžně:** informují o nových nebo aktualizovaných funkcích, které jsou k dispozici.

     [![Oznámení z možností Microsoftu ve vlastnostech webu](./media/3953121-microsoft-notifications.png)](./media/3953121-microsoft-notifications.png#lightbox)



## <a name="next-steps"></a>Další kroky

- [Použití konzoly](admin-console.md)
- [Tipy pro konzolu](admin-console-tips.md)
- [Funkce pro usnadnění přístupu](../../understand/accessibility-features.md)
