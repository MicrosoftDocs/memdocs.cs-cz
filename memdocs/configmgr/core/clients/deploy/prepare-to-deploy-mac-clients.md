---
title: Příprava na nasazení klienta na počítače Mac
titleSuffix: Configuration Manager
description: Úlohy konfigurace před nasazením klienta Configuration Manager do počítače Mac.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8d0968a61be4e450bb145b309f61de0d6c212549
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713993"
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>Příprava na nasazení klientského softwaru na počítače Mac

*Platí pro: Configuration Manager (Current Branch)*

Postupujte podle těchto kroků a ujistěte se, že jste připraveni [nasadit klienta Configuration Manager do počítačů se systémem Mac](deploy-clients-to-macs.md).



## <a name="mac-prerequisites"></a>Požadavky na Mac

Instalační balíček klienta pro systém Mac není dodáván s Configuration Manager médium. Stáhněte si **klienty pro další operační systémy** z [webu Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkID=525184).  

Seznam podporovaných verzí najdete v tématu [podporované operační systémy pro klienty a zařízení](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).



## <a name="certificate-requirements"></a>Požadavky na certifikáty

Instalace a Správa klientů pro počítače Mac vyžaduje certifikáty infrastruktury veřejných klíčů (PKI). Certifikáty PKI zabezpečují komunikaci mezi počítači Mac a lokalitou Configuration Manager pomocí vzájemného ověřování a šifrovaných přenosů dat. Configuration Manager může vyžádat a nainstalovat klientský certifikát uživatele. Používá certifikační služby s certifikační autoritou rozlehlé sítě a bod registrace Configuration Manager a zprostředkující bod registrace. Můžete si taky vyžádat a nainstalovat certifikát počítače nezávisle na Configuration Manager. Tento certifikát musí splňovat Configuration Manager požadavky na certifikát.  

Configuration Manager klienti se systémem Mac vždy kontrolují odvolání certifikátů. Tuto funkci nelze zakázat.  

Pokud klienti se systémem Mac nemůžou najít seznam odvolaných certifikátů (CRL), nemůžou se připojit k Configuration Managerm systémům lokality. Zvláště u klientů se systémem Mac v jiné doménové struktuře jako vydávající certifikační autorita ověřte návrh seznamu odvolaných certifikátů. Ujistěte se, že klienti se systémem Mac můžou vyhledat a stáhnout seznam odvolaných certifikátů.  

Před instalací klienta Configuration Manager do počítače Mac rozhodněte, jak nainstalovat certifikát klienta:  

-   Použijte Configuration Manager registraci pomocí [nástroje CMEnroll](deploy-clients-to-macs.md#client-and-certificate-automation-with-cmenroll). Proces registrace nepodporuje automatické obnovení certifikátu. Před vypršením platnosti certifikátu znovu zaregistrujte počítače Mac.  

-   [Použijte žádost o certifikát a metodu instalace, která je nezávislá na Configuration Manager](deploy-clients-to-macs.md#bkmk_external).  

Další informace o požadavcích na certifikát klienta Mac najdete v tématu [požadavky na certifikát PKI pro Configuration Manager](../../plan-design/network/pki-certificate-requirements.md).  

Klienti se systémem Mac se automaticky přiřazují do Configuration Manager lokality, která je spravuje. Klienti se systémem Mac se instalují jenom jako internetoví klienti, a to i v případě, že je komunikace omezená na intranet. Tato konfigurace znamená, že komunikuje s internetovými body správy a distribučními body v jim přiřazené lokalitě. Počítače Mac nekomunikují se systémy lokality mimo přiřazenou lokalitu.  

> [!IMPORTANT]  
>  Klienta Configuration Manager pro macOS nelze použít pro připojení k bodu správy, který je nakonfigurován pro použití [repliky databáze](../../servers/deploy/configure/database-replicas-for-management-points.md).  



## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Nasazení certifikátu webového serveru na servery systému lokality  

Pokud tyto systémy lokalit nástroje nemají, Nasaďte certifikát webového serveru na počítače, které mají tyto role systému lokality:  

-   Bod správy  

-   Distribuční bod  

-   Bod registrace  

-   Zprostředkující bod registrace  

Certifikát webového serveru musí obsahovat internetový plně kvalifikovaný název domény, který je určený ve vlastnostech systému lokality. Server nemusí být přístupný z Internetu pro podporu počítačů Mac. Pokud nepotřebujete internetovou správu klientů, můžete zadat hodnotu intranetového plně kvalifikovaného názvu domény pro internetový plně kvalifikovaný název domény.  

Zadejte hodnotu internetového plně kvalifikovaného názvu domény systému lokality v certifikátu webového serveru pro bod správy, distribuční bod a zprostředkující bod registrace.

Další informace o ukázkovém nasazení najdete v části [Nasazení certifikátu webového serveru pro systémy lokality, které spouští službu IIS](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  



## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Nasazení certifikátu ověřování klienta na servery systému lokality  

Pokud tyto systémy lokalit nástroje nemají, Nasaďte certifikát ověřování klienta na počítače, které jsou hostiteli těchto rolí systému lokality:  

-   Bod správy  

-   Distribuční bod  

Ukázkové nasazení, které vytváří a instaluje certifikát klienta pro body správy, najdete v části [Nasazení certifikátu klienta pro počítače se systémem Windows](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).  

Ukázkové nasazení, které vytváří a instaluje klientský certifikát pro distribuční body, najdete v části [nasazení klientského certifikátu pro distribuční](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012)body.  

> [!IMPORTANT]  
>  Chcete-li nasadit klienta nástroje do zařízení se systémem macOS Sierra, musí být správně nakonfigurován název subjektu certifikátu bodu správy. Použijte například plně kvalifikovaný název domény serveru bodu správy.  



## <a name="prepare-the-client-certificate-template-for-macs"></a>Příprava šablony certifikátu klienta pro počítače Mac  

Šablona certifikátu musí mít oprávnění **ke čtení** a **zápisu** pro uživatelský účet, který registruje certifikát v počítači Mac.  

Další informace najdete v tématu [Nasazení certifikátu klienta pro počítače Mac](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1).  



## <a name="configure-the-management-point-and-distribution-point"></a>Konfigurace bodu správy a distribučního bodu  

Proveďte konfiguraci bodů správy u následujících možností:  

-   HTTPS  

-   Umožňuje připojení klientů z Internetu. Tato hodnota konfigurace je nezbytná pro správu počítačů Mac. Neznamená to ale, že servery systému lokality musí být dostupné z Internetu.  

-   Povolit používání tohoto bodu správy mobilními zařízení a počítači Mac  

Distribuční body nejsou vyžadovány k instalaci klienta pro systém Mac. Pokud chcete po instalaci klienta nasadit software do těchto počítačů, nakonfigurujte distribuční body tak, aby umožňovaly připojení klientů z Internetu.  


### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>Konfigurace bodů správy a distribučních bodů pro podporu počítačů Mac  

Než začnete s tímto postupem, nezapomeňte nakonfigurovat bod správy a distribuční bod pomocí internetového plně kvalifikovaného názvu domény. Pokud tyto servery nepodporují internetovou správu klientů, zadejte plně kvalifikovaný název domény intranetu jako hodnotu internetového plně kvalifikovaného názvu domény.

Role systému lokality musí být v primární lokalitě.  

1.  V konzole Configuration Manager klikněte na pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **servery a role systému lokality** . Pak vyberte server, který má správné role systému lokality.  

2.  V podokně podrobností vyberte roli **bodu správy** a na pásu karet vyberte **vlastnosti** . V okně **Vlastnosti bodu správy** nakonfigurujte tyto možnosti:  

    1.  Vyberte **https**.  

    2.  Vyberte možnost **povolí připojení pouze internetových klientů** nebo **povolte připojení intranetového a internetového klienta**. Tyto možnosti vyžadují internetový nebo intranetový plně kvalifikovaný název domény.  

    3.  Vyberte možnost **Povolte mobilním zařízením a počítačům Mac používat tento bod správy**.  

    4. Uložte tuto konfiguraci výběrem tlačítka **OK**.  

3.  V podokně podrobností uzlu role serveru a systému lokality vyberte roli **distribučního bodu** a na pásu karet vyberte **vlastnosti** . V okně **vlastnosti distribučního bodu** nakonfigurujte tyto možnosti:  

    -   Vyberte **https**.  

    -   Vyberte možnost **povolí připojení pouze internetových klientů** nebo **povolte připojení intranetového a internetového klienta**. Tyto možnosti vyžadují internetový nebo intranetový plně kvalifikovaný název domény.  

    -   Zvolte **importovat certifikát**, přejděte do souboru certifikátu distribučního bodu exportovaného klienta a pak zadejte heslo.  

4.  Tento postup opakujte pro všechny body správy a distribuční body v primárních lokalitách, které spravují počítače Mac.  



## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Konfigurace zprostředkujícího bodu registrace a bodu registrace  

Nainstalujte obě role do stejné lokality. Nemusíte je instalovat na stejný server systému lokality nebo do stejné doménové struktury služby Active Directory.  

Další informace o umístění role systému lokality a důležitých informacích najdete v tématu [role systému lokality](../../plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles).  

Chcete-li přidat role systému lokality pro podporu počítačů se systémem Mac, přečtěte si téma [Instalace rolí systému lokality](../../servers/deploy/configure/install-site-system-roles.md).

Na stránce **Výběr role systému** vyberte **zprostředkující bod registrace** a **bod zápisu** ze seznamu dostupných rolí.  



## <a name="install-the-reporting-services-point"></a>Instalace bodu služby Reporting Services  

Další informace najdete v tématu [instalace bodu služby Reporting Services](../../servers/manage/configuring-reporting.md).  



## <a name="next-steps"></a>Další kroky

[Nasazení klienta Configuration Manager do počítačů se systémem Mac](deploy-clients-to-macs.md)  
