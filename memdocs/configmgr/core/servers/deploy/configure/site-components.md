---
title: Součásti lokality
titleSuffix: Configuration Manager
description: Naučte se konfigurovat součásti lokality, abyste upravili chování rolí systému lokality a vytváření sestav stavu lokality.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a3447e6ac71e9c5441a9e82034ee41eabda59374
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718326"
---
# <a name="site-components-for-configuration-manager"></a>Součásti lokality pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pro každou lokalitu Configuration Manager můžete nakonfigurovat součásti lokality, aby se změnila chování rolí systému lokality a vytváření sestav stavu lokality. Konfigurace součástí lokality se vztahují k lokalitě a ke každé instanci příslušné role systému lokality v lokalitě.  

V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** . Vyberte lokalitu. Ve skupině **Nastavení** na pásu karet vyberte možnost **Konfigurovat součásti webu**. Vyberte jednu z následujících možností:

- [Distribuce softwaru](#software-distribution)  
- [Bod aktualizace softwaru](#software-update-point) 
- [Nasazení operačního systému](#operating-system-deployment)
- [Bod správy](#management-point)  
- [Vytváření stavových zpráv](#status-reporting)  
- [E-mailové oznámení](#email-notification)
- [Vyhodnocení členství kolekce](#bkmk_colleval)


## <a name="about-site-components"></a>Součásti lokality  

 Většina možností pro různé součásti lokality je zřejmá při zobrazení v konzole Configuration Manager. Následující podrobnosti vám ale můžou vysvětlit některé z složitějších konfigurací nebo vás nasměrovat k dalšímu obsahu.  

> [!Note]  
> Dostupné možnosti pro některé součásti se liší bez ohledu na to, jestli vyberete lokalitu centrální správy, primární lokalitu nebo sekundární lokalitu. Některé součásti nejsou k dispozici vůbec pro určité typy webů.  



### <a name="software-distribution"></a>Distribuce softwaru  

#### <a name="content-distribution-settings"></a>Nastavení distribuce obsahu
Na kartě **Obecné** zadejte nastavení, které mění způsob, jakým server lokality přenáší obsah do svých distribučních bodů. Když zvýšíte hodnoty, které používáte pro nastavení souběžných distribucí, budete moct při distribuci softwaru využít větší šířku pásma sítě.  

#### <a name="pull-distribution-point"></a>Distribuční bod pro vyžádání obsahu
Další informace najdete v tématu [použití distribučního bodu pro vyžádání](../../../plan-design/hierarchy/use-a-pull-distribution-point.md)obsahu.

#### <a name="network-access-account"></a>Účet přístupu k síti
Další informace najdete v tématu [účet pro přístup k síti](../../../plan-design/hierarchy/accounts.md#network-access-account).  


### <a name="software-update-point"></a>Bod aktualizace softwaru  

Další informace najdete v tématu [instalace bodu aktualizace softwaru](../../../../sum/get-started/install-a-software-update-point.md).  


### <a name="operating-system-deployment"></a>Nasazení operačního systému

Další informace najdete v tématu [určení jednotky pro obsluhu bitové kopie operačního systému offline](../../../../osd/get-started/manage-operating-system-images.md#bkmk_servicing-drive).


### <a name="management-point"></a>Bod správy  

Na kartě **Obecné** nastavte lokalitu tak, aby publikovala informace o svých bodech správy na Active Directory Domain Services.  

Configuration Manager klienti používají body správy k vyhledání služeb a k nalezení informací o lokalitě, jako je členství ve skupině hranic a možnosti výběru certifikátu PKI. Klienti také používají body správy k nalezení dalších bodů správy v lokalitě a distribučních bodů, ze kterých se má software stáhnout. Body správy také usnadňují klientům dokončení přiřazení lokality a stažení zásad klienta a nahrání informací o klientovi.  

Nejbezpečnější metodou pro vyhledání bodů správy je jejich publikování v Active Directory Domain Services. Tato metoda umístění služby vyžaduje, aby byly splněny následující podmínky:

- Schéma je rozšířené pro Configuration Manager.
- Existuje kontejner **System Management** s příslušnými oprávněními zabezpečení pro server lokality, který se má publikovat do tohoto kontejneru.
- Lokalita Configuration Manager je nastavena pro publikování do Active Directory Domain Services.
- Klienti patří do stejné doménové struktury služby Active Directory jako doménová struktura serveru lokality.  

Když klienti na intranetu nemůžou použít Active Directory Domain Services k nalezení bodů správy, použijte [publikování DNS](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns).  

Obecné informace o umístění služby najdete v tématu [Vysvětlení způsobu, jakým klienti hledají služby a prostředky lokality](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  


#### <a name="publish-selected-intranet-management-points-in-dns"></a>Publikování vybraných intranetových bodů správy v DNS
Tuto možnost zadejte, když klienti na intranetu nemůžou najít body správy z Active Directory Domain Services. Místo toho můžou použít záznam prostředků umístění služby DNS (SRV RR) k nalezení bodu správy v přiřazené lokalitě.  

Aby bylo možné Configuration Manager publikovat intranetové body správy ve službě DNS, musí být splněné všechny následující podmínky:  

-   Vaše servery DNS mají verzi BIND, která je 8.1.2 nebo novější.  

-   Vaše servery DNS se nastavují pro automatické aktualizace a podporují záznamy prostředků umístění služby.  

-   Zadané plně kvalifikované názvy domény (FQDN) pro body správy v Configuration Manager mají záznamy hostitelů (A nebo AAA) ve službě DNS.  

> [!WARNING]  
>  Aby mohli klienti najít body správy publikované ve službě DNS, je nutné přiřadit klienty ke konkrétní lokalitě (místo použití automatického přiřazení lokality). Nastavte tyto klienty tak, aby používaly kód lokality s příponou domény svého bodu správy. Další informace najdete v tématu [vyhledání bodů správy](../../../clients/deploy/assign-clients-to-a-site.md#locating-management-points).  

Pokud klienti Configuration Manager nemůžou k nalezení bodů správy na intranetu používat Active Directory Domain Services ani DNS, používají [službu WINS](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins). První bod správy, který je nainstalovaný pro lokalitu, se automaticky publikuje do služby WINS, když je nastavený tak, aby přijímal připojení klienta HTTP na intranetu.  


### <a name="status-reporting"></a>Vytváření stavových zpráv  

Tato nastavení přímo nastaví úroveň podrobností, která je součástí zprávy o stavu z lokalit a klientů.  


### <a name="email-notification"></a>E-mailové oznámení  

Zadáním podrobností o účtu a e-mailovém serveru povolíte Configuration Manager odesílání e-mailových oznámení pro výstrahy.  

Další informace najdete v tématu [použití výstrah a stavového systému](../../manage/use-alerts-and-the-status-system.md).


### <a name="collection-membership-evaluation"></a><a name="bkmk_colleval"></a>Vyhodnocení členství kolekce  

Pomocí této součásti lze nastavit, jak často se má členství v kolekci přírůstkově vyhodnocovat. Postupná vyhodnocování aktualizují členství kolekce pouze novými nebo změněnými zdroji.  

Další informace najdete v tématu [osvědčené postupy pro kolekce](../../../clients/manage/collections/best-practices-for-collections.md).



##  <a name="use-the-configuration-manager-service-manager-to-manage-site-components"></a><a name="BKMK_ServiceMgr"></a> Použití nástroje Configuration Manager Service Manager pro správu součástí lokality  

Service Manager Configuration Manager můžete použít k řízení Configuration Managerch služeb a k zobrazení stavu libovolné služby Configuration Manager nebo pracovního vlákna. Tyto služby a vlákna se budou souhrnně označovat jako Configuration Manager komponenty. Seznamte se s následujícími prohlášeními o Configuration Managerch součástech:  

-   Komponenty lze spustit v libovolném systému lokality.  

-   Komponenty se spravují stejným způsobem, jako spravujete služby v systému Windows. Můžete spustit, zastavit, pozastavit, obnovit nebo Configuration Manager komponenty pro dotazování.  

Služba Configuration Manager se spustí, když je pro ni něco udělat. Tato akce se obvykle provádí při zápisu konfiguračního souboru do doručené pošty součásti. 


### <a name="use-the-configuration-manager-service-manager"></a>Použití Configuration Manager Service Manager  

1.  V konzole Configuration Manager otevřete pracovní prostor **monitorování** , rozbalte položku **stav systému**a vyberte uzel **Stav součásti** .  

2.  Ve skupině **součástí** na pásu karet vyberte možnost **Start**a poté vyberte možnost **Configuration Manager Service Manager**.  

3.  Když se nástroj Configuration Manager Service Manager otevře, proveďte připojení k lokalitě, kterou chcete spravovat.  

     Pokud nevidíte lokalitu, kterou chcete spravovat, přejděte do nabídky **Web** a vyberte **připojit**. Pak zadejte název serveru lokality správné lokality.  

4.  Rozbalte lokalitu a přejděte na **Součásti** nebo **Servery** podle toho, kde se nachází součásti, které chcete spravovat.  

5.  Na pravém panelu vyberte jednu nebo víc součástí. Pak v nabídce **Komponenta** vyberte možnost **dotaz** a aktualizujte stav vašeho výběru.  

6.  Po aktualizaci stavu komponenty použijte jednu ze čtyř možností založených na akcích v nabídce **Komponenta** a upravte operaci komponenty. Po vyžádání akce musíte pro zobrazení nového stavu komponenty odeslat komponentě dotaz.  

7.  Až skončíte s úpravou provozního stavu komponent, zavřete Configuration Manager Service Manager.  
