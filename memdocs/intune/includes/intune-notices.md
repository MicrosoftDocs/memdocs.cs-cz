---
title: zahrnout soubor
description: zahrnout soubor
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: 0b3af293ebc83c14f85abeb0dbaa38ca5187b267
ms.sourcegitcommit: 6a6a713fc1090e03893d80f4259dc7300fb1d5ff
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/31/2020
ms.locfileid: "80438700"
---
Tato oznámení obsahují důležité informace, které vám pomůžou připravit se na budoucí změny a funkce Intune.

### <a name="microsoft-intune-support-for-windows-10-mobile-ending--3544938--"></a>Microsoft Intune podpora pro Windows 10 Mobile<!--3544938-->
Hlavní podpora Microsoftu pro Windows 10 Mobile skončila v prosinci 2019. Jak je uvedeno v tomto prohlášení o podpoře, uživatelé s Windows 10 Mobile už nebudou mít nárok na příjem nových aktualizací zabezpečení, opravy hotfix bez zabezpečení, bezplatné podpory s asistencí nebo online aktualizace obsahu od Microsoftu. V závislosti na podpoře všech mobilních operačních systémů bude Microsoft Intune nyní koncová podpora obou Portál společnosti pro mobilní aplikace Windows 10 a Windows 10 Mobile v květnu 11. května 2020.

#### <a name="how-does-this-affect-me"></a>Co to pro mě znamená?
Pokud máte zařízení s Windows 10 Mobile nasazená ve vaší organizaci mezi teď a 11. května 2020, můžete registrovat nová zařízení, přidávat nebo odebírat zásady a aplikace nebo aktualizovat nastavení pro správu. Po 11. května zastavíme nové registrace a nakonec odebereme správu Windows 10 Mobile z uživatelského rozhraní Intune. Zařízení už nebudou zaregistrovaná ve službě Intune a odstraníme data zařízení a zásad.  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Jak se mám na tuto změnu připravit?
Můžete si prohlédnout sestavy Intune a zjistit, která zařízení nebo uživatelé to mohou mít vliv. Přejít na **zařízení** > **všechna zařízení** a filtrovat podle OS. Můžete přidat další sloupce, které vám pomůžou identifikovat, kdo ve vaší organizaci má zařízení s Windows 10 Mobile. Zajistěte, aby vaši koncoví uživatelé upgradovali svoje zařízení, nebo aby zařízení nepoužívali pro podnikový přístup.


### <a name="updated-support-statement-for-adobe-acrobat-reader-for-intune-mobile-app--5746776--"></a>Aktualizovaný příkaz Support pro mobilní aplikaci Adobe Acrobat Reader pro Intune<!--5746776-->
V MC188653 jsme na konci srpna sdíleli, že mobilní aplikace Adobe Acrobat Reader pro Intune dosáhla konce životnosti 1. prosince 2019 a že Adobe plánuje v rámci své hlavní aplikace Acrobat Readeru podporovat zásady ochrany aplikací v Intune. Od té doby jsme dostali zpětnou vazbu od zákazníků, kterou jsme potřebovali k tomu, aby bylo možné pokračovat ve povolování IT správců, a koncovým uživatelům začít používat aplikaci Adobe Acrobat Reader pro Intune. Vzhledem k vysokému využití aplikace Adobe Acrobat Reader pro Intune na zařízeních koncových uživatelů a jejich důležitosti v podnikových scénářích chceme zajistit, aby všechny zkušenosti splňovaly požadavky vaší organizace na ochranu aplikací. 

I když ve vašich zásadách stále doporučujeme cílit na obecnou mobilní aplikaci Acrobat Reader, protože mobilní aplikace Acrobat Reader podporuje zásady ochrany aplikací a integruje sadu Intune SDK, bude i nadále podporována aplikace Adobe Acrobat Reader pro Intune. do 31. března 2020. 

#### <a name="how-does-this-affect-me"></a>Co to pro mě znamená?
Tuto zprávu dostáváte, protože naše generování sestav indikuje, že jedna nebo více zásad ve vaší organizaci cílí na aplikaci Adobe Acrobat Reader pro Intune nebo jste dostali předchozí konce ŘÁDKUou komunikaci. 

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Jak se mám na tuto změnu připravit?
Dejte koncovým uživatelům a helpdesku o této změně. K vytvoření kanálu pro otázky související s Intune můžete použít [funkci informace o podpoře portál společnosti](../apps/company-portal-app.md#support-information) .

#### <a name="additional-information"></a>Další informace
https://helpx.adobe.com/acrobat/kb/intune-app-end-of-life.html

### <a name="take-action-use-microsoft-edge-for-your-protected-intune-browser-experience--5728447--"></a>Provést akci: použití Microsoft Edge pro chráněné prostředí Intune Browser<!--5728447-->
Vzhledem k tomu, že jsme provedli sdílení za minulý rok, Microsoft Edge Mobile podporuje stejnou sadu funkcí správy jako Managed Browser a přitom přináší mnohem lepší prostředí pro koncové uživatele. Pro zajištění robustních funkcí poskytovaných Microsoft Edgeem Intune Managed Browser vyřazení z provozu. Od 27. ledna 2020 už Intune nebude podporovat Intune Managed Browser.  

#### <a name="how-does-this-affect-me"></a>Co to pro mě znamená? 
Od 1. února 2020 už nebude Intune Managed Browser k dispozici v Obchod Google Play nebo v obchodě s aplikacemi pro iOS. V tuto chvíli budete mít i nadále na Intune Managed Browser zacílit nové zásady ochrany aplikací, i když noví uživatelé nebudou moct aplikaci Intune Managed Browser stáhnout. V systému iOS se navíc nové webové klipy, které se odešlou do zařízení zaregistrovaného na MDM, otevřou v Microsoft Edge místo Intune Managed Browser.  

Od března 31 2020 se Intune Managed Browser odebere z konzoly Azure. To znamená, že už nebudete moct vytvářet nové zásady pro Intune Managed Browser. Pokud jste nastavili existující zásady Intune Managed Browser, nebudou ovlivněny. Intune Managed Browser se v konzole zobrazí jako obchodní aplikace bez ikony a stávající zásady se budou zobrazovat jako cílené pro aplikaci. V tuto chvíli také odebereme možnost přesměrovat webový obsah do Intune Managed Browser v části Ochrana dat v zásadách ochrany aplikací.  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Jak se mám na tuto změnu připravit? 
K zajištění hladkého přechodu z Intune Managed Browser na Microsoft Edge doporučujeme proaktivně provést následující kroky: 

1. Zaměřte se na Microsoft Edge pro iOS a Android pomocí zásad ochrany aplikací (také označovaných jako MAM) a nastavení konfigurace aplikace. Můžete znovu použít zásady Intune Managed Browser pro Microsoft Edge tím, že tyto existující zásady zacílíte i na Microsoft Edge.  
2. Zajistěte, aby všechny aplikace chráněné MAM ve vašem prostředí měly zásadu ochrany aplikací s nastavením omezit přenos webového obsahu s ostatními aplikacemi nastavenou na prohlížeče spravované zásadami. 
3. Zaměřte se na všechna MAM chráněná nastavením konfigurace spravované aplikace "com. Microsoft. Intune. useEdge" nastavenou na hodnotu true. Počínaje dalším měsícem s vydáním 1911 budete moct provádět kroky 2 a 3 jednoduše tak, že v části Ochrana dat v zásadách ochrany aplikací nastavíte možnost omezit přenos webových obsahu na jiné aplikace. . 

Připravujeme podporu pro webové klipy v iOS a Androidu. Až se tato podpora uvolní, budete muset změnit cílení na existující webové klipy, abyste se ujistili, že se otevřou na Microsoft Edge místo Managed Browser. 

#### <a name="additional-information"></a>Další informace
Další informace najdete v našich dokumentech o [používání Microsoft Edge se zásadami ochrany aplikací](../apps/manage-microsoft-edge.md) , nebo si prohlédněte náš [příspěvek blogu o podpoře](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Use-Microsoft-Edge-for-your-Protected-Intune-Browser-Experience/ba-p/1004269).

### <a name="end-of-support-for-legacy-pc-management"></a>Konec podpory pro správu starších počítačů

Podpora starší verze správy počítačů od 15. října 2020. Upgradujte zařízení na Windows 10 a znovu je zaregistrujte jako zařízení pro správu mobilních zařízení (MDM), abyste je mohli spravovat přes Intune.

[Další informace](https://go.microsoft.com/fwlink/?linkid=2107122)


