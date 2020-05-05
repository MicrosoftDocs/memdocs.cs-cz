---
title: Zásady ochrany aplikací pro rozšíření
titleSuffix: Microsoft Intune
description: Toto téma popisuje zásady ochrany aplikací (APP) pro rozšíření.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/06/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1dce45d0ad8d44d09345ebfe3fcd358b34a104d6
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078375"
---
# <a name="protecting-application-extensions"></a>Ochrana rozšíření aplikace

Tento článek popisuje zásady ochrany aplikací pro rozšíření v Microsoft Intune.

## <a name="add-ins-for-outlook-app"></a>Doplňky pro aplikaci Outlook

Doplňky Outlooku umožňují integrovat oblíbené aplikace s e-mailovým klientem. Doplňky pro Outlook jsou k dispozici na webu, ve Windows, na Macu a v Outlooku pro Android a iOS/iPadOS. Zásady ochrany aplikací Intune APP SDK a Intune nezahrnují podporu pro správu doplňků pro Outlook, ale existují i jiné způsoby, jak omezit jejich používání. Vzhledem k tomu, že se doplňky spravují přes Microsoft Exchange, budou uživatelé moct sdílet data a zprávy v rámci Outlooku a nespravovaných aplikací doplňků (pokud nemají doplňky vypnuté na Exchangi).

Pokud chcete svým koncovým uživatelům používání a instalaci doplňků Outlooku zakázat (bude to mít vliv na všechny klienty Outlooku), musíte v rolích v Centru pro správu Exchange provést následující změny:

- Pokud chcete uživatelům zabránit v instalaci doplňků z Office Storu, odeberte jim roli My Marketplace (Moje tržiště).
- Pokud chcete uživatelům zabránit v instalaci doplňků bokem (mimo Store), odeberte jim roli My Custom Apps (Moje vlastní aplikace).
- Pokud chcete uživatelům zabránit v instalaci všech doplňků, odeberte jim jak roli My Custom Apps, tak roli My Marketplace.

Tyto pokyny se vztahují na Office 365, Exchange 2016 a Exchange 2013 napříč Outlookem na webu, v systémech Windows, Mac a na mobilních zařízeních.

- Další informace o [doplňcích pro Outlook](https://technet.microsoft.com/library/jj943753(v=exchg.150).aspx).
- Přečtěte si další informace o tom [jak určit, kteří správci a uživatelé můžou instalovat a spravovat doplňky pro aplikaci Outlook](https://technet.microsoft.com/library/jj943754(v=exchg.150).aspx).

## <a name="linkedin-account-connections-for-microsoft-apps"></a>Připojení účtů LinkedIn pro aplikace Microsoft

Připojení účtů LinkedIn umožňuje uživatelům zobrazit informace veřejného profilu sítě LinkedIn v určitých aplikacích Microsoft. Ve výchozím nastavení si uživatelé mohou zvolit připojení svého účtu LinkedIn a pracovního nebo školního účtu Microsoft, aby se mohli podívat na další informace profilu sítě LinkedIn. 

> [!NOTE]
> Integrace LinkedIn je momentálně nedostupná pro zákazníky ze státní správy USA a pro organizace s poštovními schránkami Exchange Online v Austrálii, Číně, Francii, Indii, Japonsku, Jižní Koreji, Jihoafrické republice, Kanadě, Německu a Spojeném království.

Sada Intune SDK ani zásady služby Intune App Protection nepodporují správu připojených účtů LinkedIn, ale existují jiné způsoby, jak tyto účty spravovat. Připojení účtů LinkedIn můžete zakázat pro celou organizaci, nebo je můžete povolit pro vybrané skupiny uživatelů ve vaší organizaci. Tato nastavení ovlivňují připojení LinkedIn ve všech aplikacích Office 365 na všech platformách (webové, mobilní a desktopové). Můžete:

- Povolte nebo zakažte připojení účtů LinkedIn pro tenanta na portálu Azure Portal. 
- Povolte nebo zakažte připojení účtů LinkedIn pro aplikace Office 2016 ve vaší organizaci pomocí zásad skupiny.

Pokud je integrace LinkedIn pro vašeho tenanta povolena, mají uživatelé ve vaší organizaci při připojení svých účtů LinkedIn a pracovních nebo školních účtů Microsoft dvě možnosti: 

- Mohou udělit oprávnění ke sdílení dat mezi oběma účty. To znamená, že mohou udělit oprávnění svému účtu LinkedIn sdílet data s pracovním nebo školním účtem Microsoft a naopak. Data sdílená s LinkedIn opouští online služby. 
- Mohou udělit oprávnění ke sdílení dat pouze ze svého účtu LinkedIn do pracovního nebo školního účtu Microsoft.

Pokud uživatel souhlasí se sdílením dat mezi účty stejně jako u doplňků Office, integrace LinkedIn používá existující rozhraní Microsoft Graph API. Integrace LinkedIn používá pouze podmnožinu rozhraní API dostupných pro doplňky Office a podporuje různá vyloučení.


|Oprávnění Microsoft Graph  |Popis  |
|---------|---------|
|Oprávnění ke čtení pro možnost [Lidé](https://developer.microsoft.com/graph/docs/concepts/permissions_reference#people-permissions)     |Umožňuje aplikaci přístup k seznamu osob se skóre, které jsou pro přihlášeného uživatele relevantní. Seznam může obsahovat místní kontakty, kontakty ze sociálních sítí nebo adresáře vaší organizace a osoby z posledních komunikací (například z e-mailu nebo Skypu).         |
|Oprávnění ke čtení pro možnost [Kalendáře](https://developer.microsoft.com/graph/docs/concepts/permissions_reference#calendars-permissions)     |Umožňuje aplikaci přístup k událostem v uživatelských kalendářích. Zahrnuje schůzky v kalendářích přihlášených uživatelů, jejich časy, umístění a účastníky.         |
|Oprávnění ke čtení pro možnost [Profil uživatele](https://developer.microsoft.com/graph/docs/concepts/permissions_reference#user-permissions)     |Umožňuje uživatelům přihlásit se k aplikaci a aplikaci umožňuje přístup k profilu přihlášených uživatelů. Také aplikaci umožňuje přístup k základním informacím o společnosti u přihlášených uživatelů.         |
|Předplatná     |Tento rozsah se zatím nepoužívá a není proto dostupný. Zahrnuje předplatná, která organizace uživatele poskytuje aplikacím a službám Microsoft, například Office 365.         |
|Insights     |Tento rozsah se zatím nepoužívá a není proto dostupný. Zahrnuje zájmy přidružené k účtu přihlášeného uživatele podle toho, jak uživatel používá služby Microsoft.         |

### <a name="learn-more"></a>Další informace

- Přečtěte si o [informacích a funkcích LinkedIn v aplikacích Microsoft](https://go.microsoft.com/fwlink/?linkid=850740).
- Přečtěte si o možnosti připojení účtů LinkedIn na [stránce roadmapy Office 365](https://products.office.com/en-US/business/office-365-roadmap?filters=%26freeformsearch=linkedin#abc). 
- Přečtěte si o [konfiguraci připojení účtů LinkedIn](https://docs.microsoft.com/azure/active-directory/linkedin-integration).
- Další informace o datech, která jsou sdílená mezi uživateli LinkedIn a pracovními nebo školními účty uživatelů, najdete [v tématu LinkedIn v aplikacích Microsoftu ve vaší práci nebo ve škole](https://www.linkedin.com/help/linkedin/answer/84077).

