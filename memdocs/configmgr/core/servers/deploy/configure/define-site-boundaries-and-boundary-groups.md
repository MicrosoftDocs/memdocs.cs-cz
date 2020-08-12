---
title: Použití hranic a skupin hranic
titleSuffix: Configuration Manager
description: Pomocí hranic a skupin hranic definujte síťová umístění a přístupné systémy lokality pro zařízení, která spravujete.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 385dc1b2f542c964b52515e755a9202ee951bc5c
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126371"
---
# <a name="define-site-boundaries-and-boundary-groups"></a>Definice hranic lokality a skupin hranic

*Platí pro: Configuration Manager (Current Branch)*

*Hranice* v Configuration Manager definují síťová umístění v intranetu. Mezi tato umístění patří zařízení, která chcete spravovat. *Skupiny hranic* jsou logické skupiny hranic, které nakonfigurujete.

Hierarchie může obsahovat libovolný počet skupin hranic. Každá skupina hranic může obsahovat libovolnou kombinaci těchto typů hranic:  

- Podsíť protokolu IP  
- název lokality služby Active Directory,  
- Předpona IPv6  
- Rozsah IP adres  
- VPN (počínaje verzí 2006)

Klienti v intranetu vyhodnotí svoje aktuální umístění v síti a potom pomocí těchto informací identifikují skupiny hranic, ke kterým patří.  

Klienti použijí skupiny hranic k:  

- **Najít přiřazenou lokalitu:** Skupiny hranic umožňují klientům vyhledat primární lokalitu pro přiřazení klienta. Toto chování se označuje také jako *Automatické přiřazení lokality*.  

- **Najděte některé role systému lokality, které můžou použít:** Přidružte skupinu hranic k určitým rolím systému lokality. Lokalita pak klientům poskytne seznam systémů lokality ve skupině hranic. Klienti používají tyto systémy lokality k akcím, jako je hledání obsahu nebo blízkého bodu správy.  

Klienti, kteří jsou na internetu nebo nakonfigurované jako pouze internetoví klienti, nepoužívají informace o hranicích. Tito klienti nemůžou použít automatické přiřazení lokality. Mohou stahovat obsah z internetového distribučního bodu ze své přiřazené lokality nebo z cloudového distribučního bodu.  

Počínaje verzí 1902 můžete přidružit bránu pro správu cloudu (CMG) k hraniční skupině. Další informace najdete v tématu [Návrh hierarchie CMG](../../../clients/manage/cmg/plan-cloud-management-gateway.md#hierarchy-design).<!--3640932-->


## <a name="recommendations"></a><a name="BKMK_BoundaryBestPractices"></a>Doporučit

### <a name="use-a-mix-of-the-fewest-boundaries-that-meet-your-needs"></a>Používejte kombinaci nejmenších hranic, které vyhovují vašim potřebám.

Použijte libovolný typ nebo typy hranic, které si zvolíte pro vaše prostředí. Chcete-li zjednodušit úlohy správy, použijte typy hranic, které vám umožní použít nejnižší počet hranic, které můžete.

### <a name="avoid-overlapping-boundaries-for-automatic-site-assignment"></a>Nepoužívejte překrývající se hranice pro automatické přiřazení lokality

I když každá skupina hranic podporuje přiřazení lokality i odkaz na systém lokality, vytvoří samostatnou sadu skupin hranic, které se použijí jenom pro přiřazení lokality. Ujistěte se, že každá hranice ve skupině hranic není členem jiné skupiny hranic s jiným přiřazením lokality.

- Jedna hranice může být zahrnutá ve víc skupinách hranic.  

- Každá skupina hranic může být pro přiřazení lokality přidružená k jiné primární lokalitě.  

- Pro hranici, která je členem dvou různých skupin hranic s různými přiřazeními lokalit, klienti náhodně vyberou lokalitu, ke které se připojí. Toto chování nemusí být pro lokalitu, ke které se má klient připojit. Tato konfigurace se nazývá *překrývající se hranice*.  

    Překrývající se hranice nejsou problémem pro umístění obsahu. Může to být užitečná konfigurace, která poskytuje klientům další zdroje nebo umístění obsahu, které můžou používat.  


## <a name="next-steps"></a>Další kroky

- [Definovat síťová umístění jako hranice](boundaries.md)

- [Konfigurace skupin hranic](boundary-groups.md)
