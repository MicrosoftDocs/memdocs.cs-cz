---
title: Vytvoření skupin aplikací
titleSuffix: Configuration Manager
description: Vytvořte skupinu aplikací, které můžete odeslat do kolekce uživatelů nebo zařízení jako jedno nasazení v Configuration Manager.
ms.date: 04/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: e67c691e-62ef-4f43-9cfb-0e957d1e7a5f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f63c52fcd2aaccbfbe04160581318126bc53db12
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643128"
---
# <a name="create-application-groups"></a>Vytvoření skupin aplikací

*Platí pro: Configuration Manager (Current Branch)*

<!--3555907-->

Počínaje verzí 1906 vytvořte skupinu aplikací, které můžete odeslat do kolekce uživatelů nebo zařízení jako jediné nasazení. Metadata, která zadáte o skupině aplikací, se zobrazují v centru softwaru jako jediná entita. Aplikace můžete seřadit ve skupině, aby je klient nainstalovaly v určitém pořadí.

> [!Note]  
> V této verzi Configuration Manager jsou skupiny aplikací součástí předběžné verze. Pokud ho chcete povolit, přečtěte si téma [předběžné verze funkcí](../../core/servers/manage/pre-release-features.md).  

1. V konzole Configuration Manager otevřete pracovní prostor **softwarová knihovna** . Rozbalte možnost **Správa aplikací** a vyberte uzel **Skupina aplikací** .  

1. Ve skupině vytvořit na pásu karet vyberte **vytvořit skupinu aplikací**.

1. Na stránce **Obecné informace** zadejte informace o skupině aplikací.  

1. Na stránce **Centrum softwaru** uveďte informace, které se zobrazí v centru softwaru.  

1. Na stránce **Skupina aplikací** vyberte **Přidat**. Vyberte jednu nebo více aplikací pro tuto skupinu. Přeuspořádat je pomocí akcí **Přesunout nahoru** a **Přesunout dolů** .  

1. Dokončete průvodce.  

Nasaďte skupinu aplikací pomocí stejného procesu jako u aplikace. Další informace najdete v tématu [nasazení aplikací](deploy-applications.md). Počínaje verzí 1910 můžete nasadit skupinu aplikací do kolekce zařízení nebo uživatele.

Po nasazení skupiny:

- Pokud do skupiny přidáte novou aplikaci, je nutné samostatně distribuovat obsah nové aplikace do distribučních bodů.

- Pokud aplikaci upravíte ve skupině aplikací, znovu ji distribuujte.

K řešení potíží s nasazením skupiny aplikací použijte v klientovi následující soubory protokolů:

- **AppGroupHandler. log**
- **AppEnforce.log**
- **SettingsAgent. log**

> [!Important]  
> Nevytvářejte ani nesaďte skupinu aplikací, dokud neaktualizujete celou hierarchii a cílové klienty alespoň na verzi 1906.

### <a name="known-issues"></a>Známé problémy

- *Verze 1906*: aplikace ve skupině můžou obsahovat jenom **Instalační služba systému Windows** nebo typy nasazení **skriptu** .
  - *Verze 1906*: nastavte chování při instalaci typu nasazení k **instalaci systému**.
- Následující možnosti nasazení nemusí fungovat: výstrahy, schválení, dvoufázové nasazení, opravit.
- Nemůžete exportovat ani importovat skupiny aplikací.
- Nezahrnovat do skupin žádné aplikace, které vyžadují restart, jinak může dojít k selhání nasazení skupiny.
- *Verze 1906*: skupinu aplikací nejde nasadit do kolekce uživatelů.
- *Verze 1906*: uživatelé nemůžou **odinstalovat** skupinu aplikací v centru softwaru.
- Pokud odstraníte aplikaci, která je součástí skupiny aplikací, při dalším zobrazení vlastností skupiny aplikací se zobrazí následující upozornění: "nelze načíst informace o všech aplikacích ve skupině". Udělejte jednoduchou změnu ve skupině aplikací a uložte ji. Přidejte například prostor do **komentářů správce**. Když změnu uložíte, odebere ze skupiny odstraněnou aplikaci.<!-- 7099542 -->
