---
title: Stránka stavu tenanta Microsoft Intune
titleSuffix: Microsoft Intune
description: Pomocí stránky stav tenanta Intune můžete zobrazit důležité podrobnosti o tenantovi, aniž byste museli opustit portál Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/05/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 7954a686-25dc-4fce-b395-324816f46d3b
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 99a34167f8616c6bbf2e441628de0d73aba080c3
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79330495"
---
# <a name="use-the-intune-tenant-status-page"></a>Použití stránky stavu tenanta Intune
Stránka stav tenanta Microsoft Intune je centralizované centrum, kde si můžete zobrazit aktuální a důležité podrobnosti o vašem tenantovi. Podrobnosti zahrnují dostupnost a používání licencí, stav konektoru a důležitou komunikaci týkající se služby Intune.  

Pokud chcete zobrazit řídicí panel, přihlaste se k [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) a pak vyberte **stav tenanta**.  *Stav tenanta* se zobrazí v části **pomoc a podpora**.  

Stránka je rozdělena na tři karty:

## <a name="tenant-details"></a>Podrobnosti o tenantovi
Podrobnosti o tenantovi poskytují informace o vašem tenantovi. Podívejte se na podrobnosti, jako je název tenanta a umístění, autorita MDM a číslo verze služby tenanta. Číslo vydání služby je odkaz, který otevře článek *co je nového v Intune* v dokumentaci Microsoftu. V části *co je nového*si můžete přečíst o nejnovějších funkcích a aktualizacích služby Intune.  

Na této kartě najdete také základní informace o dostupných licencích a počtu uživatelů, kteří jsou přiřazeni. Licence pro zařízení nejsou zobrazeny.

## <a name="connector-status"></a>Stav konektoru
Stav konektoru je jediné umístění, ve kterém můžete zkontrolovat stav všech dostupných konektorů pro Intune.  

Konektory jsou:
- **Připojení, která nakonfigurujete pro externí služby**. Například služba *Apple Volume purchase program* nebo služba *Windows autopilot* .  Stav tohoto typu konektoru je založený na poslední úspěšné synchronizaci.
- **Certifikáty nebo přihlašovací údaje, které jsou vyžadovány pro připojení k externí nespravované službě**, jako jsou certifikáty APNs ( *Apple Push Notification Services* ). Stav tohoto typu konektoru je založený na časovém razítku vypršení certifikátu nebo přihlašovacích údajů.  

Když otevřete kartu *stav konektoru* , všechny konektory, které nejsou v pořádku, se zobrazí v horní části seznamu. Dále jsou konektory s upozorněními a pak seznam konektorů v pořádku. Konektory, které jste ještě nenakonfigurovali *, se zobrazí jako poslední*.

Pokud je k dispozici více než jeden konektor libovolného typu, je stav souhrn pro všechny tyto stejné konektory. Nejnižší dobrý stav jakéhokoli konektoru se používá jako stav pro skupinu.  

**Stav konektoru:**
- **Není v pořádku**
  - Platnost certifikátu nebo přihlašovacích údajů vypršela.
  - Poslední synchronizace proběhla před třemi nebo více dny.
- **Upozornění**
  - Platnost certifikátu nebo přihlašovacích údajů vyprší do sedmi dnů.
  - Poslední synchronizace proběhla před víc než jedním dnem.
- **V pořádku**
  - Platnost certifikátu nebo přihlašovacích údajů nevyprší během příštích sedmi dnů.
  - Poslední synchronizace byla před méně než 1 dnem.  

Když vyberete konektor ze seznamu, portál zobrazí stránku portálu, která je relevantní pro daný konektor. Na stránce konektory si můžete zobrazit stav dříve nakonfigurovaných konektorů nebo vybrat možnosti pro přidání nebo vytvoření nového konektoru tohoto typu.

Pokud například vyberete konektor **Datum vypršení platnosti VPP** , otevře se stránka **tokeny programu Volume koupené pro iOS** , kde můžete zobrazit další podrobnosti o tomto konektoru. Můžete také vytvořit novou konfiguraci nebo upravit a opravit problémy s existujícím.

## <a name="service-health-dashboard"></a>Řídicí panel stavu služby  
Na řídicím panelu stavu služby můžete zobrazit podrobnosti o *incidentech služby* , které mají vliv na vašeho tenanta, a *novinky Intune* , které poskytují informace o aktualizacích a plánovaných změnách.

### <a name="intune-service-health"></a>Service Health Intune
Zobrazte si podrobnosti o aktivních incidentech a poradcích, aniž byste museli přecházet na řídicí panel Microsoft 365 Service Health nebo Centrum zpráv, jak je umístěno v [centru pro správu Microsoft 365](https://admin.microsoft.com). Zobrazí se pouze incidenty, které mají vliv na vašeho tenanta.  

Po výběru incidentu se podrobnosti o incidentu zobrazí přímo na stránce Stav tenanta. Pokud chcete zobrazit minulé poradce a incidenty, vyberte **zobrazit minulé incidenty/poradci**. Otevře se centrum pro správu Microsoft 365, kde můžete zobrazit upozornění a incidenty za posledních 30 dní pro vašeho tenanta.  

Pokud chcete zobrazit informace o *Service Health Intune*, váš účet musí mít roli **globálního správce** nebo **Správce služby** v Azure Active Directory nebo v centru pro správu Microsoft 365. Pokud chcete přiřadit tato oprávnění, přihlaste se k [centru pro správu Microsoft 365](https://admin.microsoft.com) s oprávněními globálního správce. Vyberte **uživatelé > aktivní uživatelé**a pak vyberte účet, který vyžaduje přístup. Vyberte **Upravit** pro role, vyberte *Správce služby* nebo *globální správce*a pak **uložte** úpravy, abyste přidělili oprávnění.  

Předvolby komunikace pro Service Health Intune můžete nastavit jenom prostřednictvím centra pro správu Microsoft 365.

### <a name="intune-news"></a>Novinky Intune  
Prohlédněte si informační komunikaci z týmu služby Intune, aniž byste museli přejít do centra zpráv Office. Mezi komunikace patří zprávy o změnách, ke kterým nedávno došlo ve službě Intune, nebo na způsobu, jakým je váš tenant.  

Ve výchozím nastavení se zobrazuje 10 nejaktuálnějších a aktivních zpráv. Chcete-li zobrazit starší zprávy, vyberte možnost **zobrazit minulé zprávy** a otevřete *Centrum zpráv* v centru pro správu Microsoft 365.  

Pokud chcete zobrazit informace o zprávách Intune, váš účet musí mít roli **globálního správce** nebo **správce služeb** v Azure Active Directory nebo roli **Čtenář centra zpráv** v centru pro správu Microsoft 365.  Pokud chcete toto oprávnění přiřadit, přihlaste se k [centru pro správu Microsoft 365](https://admin.microsoft.com) s oprávněními správce. Vyberte **uživatelé > aktivní uživatelé**a pak vyberte účet, který vyžaduje přístup. Vyberte **Upravit** pro *role*, vyberte *týmy komunikace správce*a potom **uložte** vaši úpravu pro přiřazení oprávnění.  

Předvolby komunikace pro zprávy Intune můžete nastavit jenom prostřednictvím centra pro správu Microsoft 365.
