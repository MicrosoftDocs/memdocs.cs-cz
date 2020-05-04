---
title: Blokování klientů
titleSuffix: Configuration Manager
description: Zablokuje klientský přístup k zabezpečení systému pomocí Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 54ef5fbb-521d-4ca5-a1c5-61e6f538d71e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b01fd7944d8a6ab726712f6ebeb4cb5374896072
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713237"
---
# <a name="determine-whether-to-block-clients-in-configuration-manager"></a>Určete, jestli se mají blokovat klienti v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pokud klientský počítač nebo mobilní zařízení klienta již nejsou důvěryhodné, můžete klienta blokovat v konzole nástroje System Center 2012 Configuration Manager. Zablokované klienty jsou odmítnuté infrastrukturou Configuration Manager, aby nemohly komunikovat se systémy lokality ke stažení zásad, odeslání dat inventáře nebo odesílání stavových zpráv.  

 Spíše než ze sekundární lokality nebo lokality centrální správy je nutné klienta blokovat a odblokovat z jeho přiřazené lokality.  

> [!IMPORTANT]  
>  I když blokování v Configuration Manager může pomáhat zabezpečit lokalitu Configuration Manager, nespoléhá se na tuto funkci, pokud chcete lokalitu chránit před nedůvěryhodnými počítači nebo mobilními zařízeními, pokud klientům umožníte komunikovat se systémy lokality pomocí protokolu HTTP, protože blokovaný klient by se mohl znovu připojit k lokalitě pomocí nového certifikátu podepsaného svým držitelem a ID hardwaru. Místo toho použijte funkci blokování k blokování ztracených nebo ohrožených spouštěcích médií, která používáte k nasazení operačních systémů, a pokud systémy lokality přijmou připojení klienta pomocí protokolu HTTPS.  

 Klienty, kteří přistupují k lokalitě pomocí certifikátu ISV Proxy, nejde blokovat. Další informace o certifikátu ISV proxy najdete v sadě Configuration Manager Software Development Kit (SDK).  

 Pokud vaše systémy lokality přijímají připojení klienta pomocí protokolu HTTPS a vaše infrastruktura veřejných klíčů (PKI) podporuje seznam odvolaných certifikátů (CRL), vždycky je třeba zajistit, aby odvolané certifikáty byly první linií obrany před potenciálně ohroženými certifikáty. Blokování klientů v Configuration Manager nabízí druhou linii obrany ochrany vaší hierarchie.  

##  <a name="considerations-for-blocking-clients"></a><a name="BKMK_Block_vs_CRL"></a> Aspekty týkající se blokování klientů  

-   Tato možnost je dostupná pro připojení klientů pomocí protokolu HTTP a HTTPS, ale při připojení klientů k systémům lokality pomocí protokolu HTTP má omezené zabezpečení.  

-   Configuration Manager administrativních uživatelů má oprávnění blokovat klienta a akce se provádí v konzole Configuration Manager.  

-   Komunikace klienta je odmítnuta pouze z hierarchie Configuration Manager.  

    > [!NOTE]  
    >  Stejný klient by se mohl zaregistrovat v jiné hierarchii Configuration Manager.  

-   Klient je okamžitě zablokován z Configuration Manager webu.  

-   Pomáhá chránit systémy lokality před potenciálně ohroženými počítači a mobilními zařízeními.  

## <a name="considerations-for-using-certificate-revocation"></a>Aspekty týkající se použití odvolání certifikátu  

-   Tato možnost je dostupná pro připojení klientů s Windows pomocí protokolu HTTPS, pokud infrastruktura veřejných klíčů podporuje seznam odvolaných certifikátů (CRL).  

     Klienti Mac vždycky provedou kontrolu seznamu CRL a tuto funkčnost nejde zakázat.  

     I když klienti mobilních zařízení nepoužívají seznamy odvolaných certifikátů ke kontrole certifikátů pro systémy lokality, jejich certifikáty mohou být odvolány a zkontrolovány Configuration Manager.  

-   Správci infrastruktury veřejných klíčů mají oprávnění odvolat certifikát a akce se provádí mimo konzolu Configuration Manager.  

-   Komunikace klienta může být odmítnutá v jakémkoli počítači nebo mobilním zařízení vyžadujícím tento certifikát klienta.  

-   Mezi odvoláním certifikátu a stažením změněného seznamu odvolaných certifikátů (CRL) systémy lokality pravděpodobně nastane prodleva.  

-   V případě nasazení velkého počtu certifikátů PKI může tato prodleva trvat jeden i víc dnů. Třeba ve službě AD DS (Active Directory Certificate Services) je výchozí doba vypršení platnosti jeden týden v případě úplného seznamu CRL a jeden den v případě rozdílového seznamu CRL.  

-   Pomáhá chránit systémy a klienty lokality před potenciálně ohroženými počítači a mobilními zařízeními.  

    > [!NOTE]  
    >  Systémy lokality používající službu IIS jde dál chránit před neznámými klienty konfigurací seznamu důvěryhodných certifikátů (CTL) ve službě IIS.  
