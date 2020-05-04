---
title: NEJČASTĚJŠÍ DOTAZY K CMG
titleSuffix: Configuration Manager
description: Tento článek slouží k zodpovězení nejčastějších dotazů týkajících se brány pro správu cloudu.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/05/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: 2bd3824df18ecdf426720a99db8720ef4b678733
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714070"
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>Nejčastější dotazy týkající se brány pro správu cloudu

*Platí pro: Configuration Manager (Current Branch)*

Tento článek obsahuje odpovědi na nejčastější dotazy týkající se brány pro správu cloudu. Další informace najdete v tématu [Plánování brány pro správu cloudu](plan-cloud-management-gateway.md).


## <a name="frequently-asked-questions"></a>Nejčastější dotazy

### <a name="what-certificates-do-i-need"></a>Jaké certifikáty potřebuji?

Podrobnější informace najdete v tématu [certifikáty pro bránu pro správu cloudu](certificates-for-cloud-management-gateway.md).


### <a name="do-i-need-azure-expressroute"></a>Potřebuji Azure ExpressRoute?

Ne. [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) umožňuje rozšiřování místní sítě do cloudu Microsoftu. ExpressRoute nebo jiná taková připojení k virtuální síti se nevyžadují pro Configuration Manager bránu pro správu cloudu. Návrh brány pro správu cloudu umožňuje internetovým klientům komunikovat prostřednictvím služby Azure do místních systémů lokality bez další konfigurace sítě. Další informace najdete v tématu [Plánování brány pro správu cloudu](plan-cloud-management-gateway.md) .

<!-- SCCMDocs#1659 -->

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>Potřebuji zachovat virtuální počítače Azure?

Není nutná žádná údržba. Návrh brány pro správu cloudu používá platformu Azure jako službu (PaaS). Pomocí předplatného, které zadáte, Configuration Manager vytvoří nezbytné virtuální počítače, úložiště a sítě. Azure zabezpečuje a aktualizuje virtuální počítač. Tyto virtuální počítače nejsou součástí vašeho místního prostředí, protože se jedná o případ s infrastrukturou jako službou (IaaS). Brána pro správu cloudu je PaaS, které rozšiřuje vaše Configuration Manager prostředí do cloudu. Další informace najdete v tématu [zabezpečení nasazení PaaS](/azure/security/security-paas-deployments).


### <a name="how-can-i-ensure-service-continuity-during-service-updates"></a>Jak se dá zajistit Kontinuita služeb během aktualizací služby?

Změnou velikosti CMG tak, aby zahrnovala dvě nebo víc instancí, budete automaticky využívat výhod aktualizačních domén v Azure. Podívejte [se, jak aktualizovat cloudovou službu](/azure/cloud-services/cloud-services-update-azure-service).


### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>Již jsem používá IBCM. Když přidám CMG, jak se budou klienti chovat?

Pokud jste již nasadili [internetovou správu klientů](../plan-internet-based-client-management.md) (IBCM), můžete také nasadit bránu pro správu cloudu. Klienti obdrží zásady pro obě služby. Při roamingu na internetu náhodně vyberou a používají jednu z těchto internetových služeb.


### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-ad-tenant-as-the-tenant-associated-with-the-subscription-that-hosts-the-cmg-cloud-service"></a>Musí být uživatelské účty ve stejném tenantovi Azure AD jako tenant přidružený k předplatnému, které hostuje cloudovou službu CMG?
<!--SCCMDocs-pr issue #2873-->
Pokud má vaše prostředí více než jedno předplatné, můžete CMG nasadit do libovolného předplatného, které může hostovat Azure Cloud Services. 

Tato otázka je společná v následujících scénářích:  

- Pokud máte odlišnou testovací a provozní službu Active Directory a prostředí Azure AD, ale jeden, centralizovaný hostující odběr Azure  

- Používání Azure se v různých týmechch rozrostlo organickě.  

Pokud používáte nasazení Správce prostředků, připojte klienta služby Azure AD, který je přidružený k předplatnému. Toto připojení umožňuje Configuration Manager ověřování v Azure pro vytváření, nasazování a správu CMG.  

Pokud používáte ověřování Azure AD pro uživatele a zařízení spravovanou přes CMG, připojte se k němu tenanta Azure AD. Další informace o službách Azure pro správu cloudu najdete v tématu [Konfigurace služeb Azure](../../../servers/deploy/configure/azure-services-wizard.md). Při připojování každého tenanta Azure AD může jeden CMG poskytovat ověřování Azure AD pro více tenantů bez ohledu na umístění hostování.

### <a name="how-does-cmg-affect-my-clients-connected-via-vpn"></a>Jaký vliv má CMG na klienty připojené přes síť VPN?

Cestovní klienti, kteří se připojují k vašemu prostředí prostřednictvím sítě VPN, se běžně zjišťují jako intranetové. Pokusí se připojit k místní infrastruktuře, jako jsou body správy a distribuční body. Někteří zákazníci chtějí mít tyto cestovní klienty spravované prostřednictvím cloudových služeb i v případě připojení prostřednictvím sítě VPN. Počínaje verzí 1902 přidružte CMG k hraniční skupině. Tato akce vynutí, aby tito klienti nepoužívali místní systémy lokality. Další informace najdete v tématu [Konfigurace skupin hranic](setup-cloud-management-gateway.md#configure-boundary-groups).

### <a name="if-i-enable-a-cmg-will-my-clients-only-connect-to-the-cmg-enabled-management-point-when-theyre-connected-to-the-intranet"></a>Pokud povolíte CMG, budou se moji klienti připojovat k bodu správy s povoleným CMG, jenom když jsou připojení k intranetu?

Aby bylo možné zabezpečit citlivý přenos odeslaný přes CMG, buď nakonfigurujte bod správy HTTPS, nebo použijte Rozšířený protokol HTTP.

Pokud se rozhodnete nasadit CMG a používat certifikáty PKI pro komunikaci pomocí protokolu HTTPS v bodu správy s povoleným CMG, vyberte možnost **povolení pouze internetových klientů** ve vlastnostech bodu správy. Toto nastavení zajistí, aby interní klienti dál používali body správy protokolu HTTP ve vašem prostředí.

Pokud používáte rozšířené HTTP, nemusíte konfigurovat toto nastavení. Klienti i nadále používají protokol HTTP při komunikaci přímo s bodem správy s povolenou CMG. Další informace najdete v tématu [Rozšířená http](../../../plan-design/hierarchy/enhanced-http.md).

## <a name="next-steps"></a>Další kroky

- [Plánování brány pro správu cloudu](plan-cloud-management-gateway.md)
- [Instalace brány pro správu cloudu](setup-cloud-management-gateway.md)
- [Certifikáty brány pro správu cloudu](certificates-for-cloud-management-gateway.md)
- [Zabezpečení a ochrana brány pro správu cloudu](security-and-privacy-for-cloud-management-gateway.md)
- [Velikost brány pro správu cloudu a čísla škálování](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)
