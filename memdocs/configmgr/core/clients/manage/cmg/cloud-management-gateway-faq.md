---
title: NEJČASTĚJŠÍ DOTAZY K CMG
titleSuffix: Configuration Manager
description: Tento článek slouží k zodpovězení nejčastějších dotazů týkajících se brány pro správu cloudu.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: ecc91168cc90af58c40903ea3d288eeaa82be7a0
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502234"
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

### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-ad-tenant-as-the-tenant-associated-with-the-subscription-that-hosts-the-cmg-cloud-service"></a><a name="bkmk_tenant"></a>Musí být uživatelské účty ve stejném tenantovi Azure AD jako tenant přidružený k předplatnému, které hostuje cloudovou službu CMG?
<!--SCCMDocs-pr issue #2873-->
Ne, CMG můžete nasadit do libovolného předplatného, které může hostovat Azure Cloud Services.

Postup při objasnění podmínek:

- _Tenant_ je adresář uživatelských účtů a registrací aplikací. Jeden tenant může mít několik předplatných.
- _Předplatné_ odděluje fakturace, prostředky a služby. Je přidružen k jednomu klientovi.

Tato otázka je společná v následujících scénářích:  

- Pokud máte odlišnou testovací a provozní službu Active Directory a prostředí Azure AD, ale jedno, centralizované předplatné hostování Azure.

- Používání Azure se v různých týmechch rozrostlo organickě.

Pokud používáte nasazení Správce prostředků, připojte klienta služby Azure AD, který je přidružený k předplatnému. Toto připojení umožňuje Configuration Manager ověřování v Azure pro vytváření, nasazování a správu CMG.  

Pokud používáte ověřování Azure AD pro uživatele a zařízení spravovanou přes CMG, připojte se k němu tenanta Azure AD. Další informace o službách Azure pro správu cloudu najdete v tématu [Konfigurace služeb Azure](../../../servers/deploy/configure/azure-services-wizard.md). Při připojování každého tenanta Azure AD může jeden CMG poskytovat ověřování Azure AD pro více tenantů bez ohledu na umístění hostování.

#### <a name="example-1-one-tenant-with-multiple-subscriptions"></a>Příklad 1: jeden tenant s několika předplatnými

Identity uživatelů, registrace zařízení a registrace aplikací jsou všechny ve stejném tenantovi. Můžete si vybrat, které předplatné používá CMG. Můžete nasadit několik služeb CMG z jedné lokality do samostatných předplatných. Lokalita má relaci 1:1 s klientem. Rozhodnete, které odběry se mají použít, a to z různých důvodů, jako je fakturace nebo logické oddělení.

#### <a name="example-2-multiple-tenants"></a>Příklad 2: více tenantů

Jinými slovy, vaše prostředí má více než jednu službu Azure AD. Pokud potřebujete podporovat identitu uživatelů a zařízení v obou klientech, musíte lokalitu připojit ke každému tenantovi. Tento proces vyžaduje účet správce z každého tenanta, aby se v tomto tenantovi vytvořily registrace aplikací. Jedna lokalita pak může hostovat služby CMG Services ve více klientech. CMG můžete vytvořit v jakémkoli dostupném předplatném v obou klientech. Zařízení, která jsou připojená nebo Hybrid připojená k Azure AD, můžou používat CMG.

Pokud jsou identity uživatelů a zařízení v jednom tenantovi, ale předplatné CMG je v jiném tenantovi, musíte lokalitu připojit ke klientům. Technicky, klientská aplikace není potřebná pro druhého tenanta, který má pouze službu CMG. Klientská aplikace poskytuje pouze ověřování uživatelů a zařízení pro klienty, kteří používají službu CMG.<!-- SCCMDocs#1902 -->

### <a name="how-does-cmg-affect-my-clients-connected-via-vpn"></a>Jaký vliv má CMG na klienty připojené přes síť VPN?

Cestovní klienti, kteří se připojují k vašemu prostředí prostřednictvím sítě VPN, se běžně zjišťují jako intranetové. Pokusí se připojit k místní infrastruktuře, jako jsou body správy a distribuční body. Někteří zákazníci chtějí mít tyto cestovní klienty spravované prostřednictvím cloudových služeb i v případě připojení prostřednictvím sítě VPN. Počínaje verzí 1902 přidružte CMG k hraniční skupině. Tato akce vynutí, aby tito klienti nepoužívali místní systémy lokality. Další informace najdete v tématu [Konfigurace skupin hranic](setup-cloud-management-gateway.md#configure-boundary-groups).

### <a name="if-i-enable-a-cmg-will-my-clients-only-connect-to-the-cmg-enabled-management-point-when-theyre-connected-to-the-intranet"></a>Pokud povolíte CMG, budou se moji klienti připojovat k bodu správy s povoleným CMG, jenom když jsou připojení k intranetu?

Aby bylo možné zabezpečit citlivý přenos odeslaný přes CMG, buď nakonfigurujte bod správy HTTPS, nebo použijte Rozšířený protokol HTTP.

Pokud se rozhodnete nasadit CMG a používat certifikáty PKI pro komunikaci pomocí protokolu HTTPS v bodu správy s povoleným CMG, vyberte možnost **povolení pouze internetových klientů** ve vlastnostech bodu správy. Toto nastavení zajistí, aby interní klienti dál používali body správy protokolu HTTP ve vašem prostředí.

Pokud používáte rozšířené HTTP, nemusíte konfigurovat toto nastavení. Klienti i nadále používají protokol HTTP při komunikaci přímo s bodem správy s povolenou CMG. Další informace najdete v tématu [Rozšířená http](../../../plan-design/hierarchy/enhanced-http.md).

### <a name="what-are-the-differences-with-client-authentication-between-azure-ad-and-certificates"></a>Jaké jsou rozdíly mezi ověřováním klientů mezi Azure AD a certifikáty?
<!-- MEMDocs#277 -->
Pro zařízení, která se mají ověřit ve službě CMG, můžete použít certifikát služby Azure AD nebo [certifikát pro ověřování klientů](certificates-for-cloud-management-gateway.md#bkmk_clientauth) .

Pokud spravujete tradiční klienty se systémem Windows s identitou připojenou k doméně služby Active Directory, potřebují k zabezpečení komunikačního kanálu certifikáty PKI. Tito klienti můžou zahrnovat Windows 8.1 a Windows 10. Můžete použít všechny funkce podporované CMG, ale distribuce softwaru je omezená jenom na zařízení. Nainstalujte klienta Configuration Manager předtím, než se zařízení přemístí do Internetu, nebo verze 2002 nebo novější, použijte ověřování pomocí tokenu.

Můžete také spravovat klienty Windows 10 s moderní identitou, a to buď z hybridních, nebo čistě cloudových domén – připojených k Azure AD. Klienti používají Azure AD k ověřování místo certifikátů PKI. Použití Azure AD je jednodušší k nastavení, konfiguraci a údržbě než složitější systémy PKI. Můžete provádět všechny stejné aktivity správy a distribuci softwaru uživateli. Umožňuje taky další metody instalace klienta na vzdáleném zařízení.

Microsoft doporučuje připojit zařízení k Azure AD. Internetová zařízení můžou pomocí Azure AD ověřit pomocí Configuration Manager. Také umožňuje scénářům zařízení i uživatele, zda je zařízení na internetu nebo připojeno k interní síti. Další informace najdete v tématu [instalace a registrace klienta pomocí Azure AD identity](../../deploy/deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).

## <a name="next-steps"></a>Další kroky

- [Plánování brány pro správu cloudu](plan-cloud-management-gateway.md)
- [Instalace brány pro správu cloudu](setup-cloud-management-gateway.md)
- [Certifikáty brány pro správu cloudu](certificates-for-cloud-management-gateway.md)
- [Zabezpečení a ochrana brány pro správu cloudu](security-and-privacy-for-cloud-management-gateway.md)
- [Velikost brány pro správu cloudu a čísla škálování](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)
