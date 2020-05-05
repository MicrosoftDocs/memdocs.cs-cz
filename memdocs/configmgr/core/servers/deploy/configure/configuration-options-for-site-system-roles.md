---
title: Možnosti role systému lokality
titleSuffix: Configuration Manager
description: Podrobnosti o Configuration Manager rolích systému lokality, které nejsou nutně vysvětlující, najdete v tomto článku.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9dfe9e0cb2ecefc636c67cf127e596fd1ad2bfa4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721084"
---
# <a name="configuration-options-for-site-system-roles-in-configuration-manager"></a>Možnosti konfigurace pro role systému lokality v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Většina možností konfigurace pro Configuration Manager role systému lokality je vysvětlená nebo se v průvodci nebo dialogová okna vysvětlují, když je nakonfigurujete. Následující části vysvětlují role systému lokality, jejichž nastavení může vyžadovat další informace.  


## <a name="application-catalog-website-point"></a><a name="BKMK_ApplicationCatalog_Website"></a>Bod webu Katalog aplikací  

> [!Important]
> Uživatelské prostředí programu Silverlight v katalogu aplikací není v aktuální větvi verze 1806 podporováno. Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací. Podpora končí pro role katalogu aplikací s verzí 1910.  
>
> Další informace najdete v těchto článcích:
>
> - [Konfigurace centra softwaru](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Odebrané a zastaralé funkce](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Další informace o tom, jak nastavit bod webu Katalog aplikací, najdete v tématu [plánování a konfigurace správy aplikací](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  


## <a name="application-catalog-web-service-point"></a><a name="BKMK_ApplicationCatalog_WebService"></a>Bod webové služby Katalog aplikací  

> [!Important]
> Uživatelské prostředí programu Silverlight v katalogu aplikací není v aktuální větvi verze 1806 podporováno. Počínaje verzí 1906 aktualizované klienty automaticky používají bod správy pro nasazení aplikací, které jsou k dispozici pro uživatele. Nemůžete také instalovat nové role katalogu aplikací. Podpora končí pro role katalogu aplikací s verzí 1910.  
>
> Další informace najdete v těchto článcích:
>
> - [Konfigurace centra softwaru](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Odebrané a zastaralé funkce](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Další informace o tom, jak nastavit bod služeb webu Katalog aplikací, najdete v tématu [plánování a konfigurace správy aplikací](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  


## <a name="certificate-registration-point"></a><a name="BKMK_CertificateRegistrationPoint"></a>Bod registrace certifikátu  

Další informace o tom, jak nastavit bod registrace certifikátu, najdete v tématu [Úvod do profilů certifikátů](../../../../protect/deploy-use/introduction-to-certificate-profiles.md).  


## <a name="distribution-point"></a><a name="BKMK_Distribution_Point"></a>Distribuční bod  

Další informace o tom, jak nastavit distribuční bod pro nasazení obsahu, najdete v tématu [Správa obsahu a infrastruktury obsahu](manage-content-and-content-infrastructure.md).  

Další informace o nastavení distribučního bodu pro nasazení PXE najdete v tématu [použití technologie PXE pro nasazení systému Windows přes síť](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

Další informace o nastavení distribučního bodu pro nasazení pomocí vícesměrového vysílání najdete v tématu [použití vícesměrového vysílání k nasazení Windows přes síť](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

### <a name="install-and-configure-iis-if-required-by-configuration-manager"></a>V případě potřeby nainstalujte a nakonfigurujte IIS pomocí Configuration Manager

Tuto možnost vyberte, pokud chcete Configuration Manager nainstalovat a nastavit službu IIS v systému lokality, pokud ještě není nainstalovaná. Služba IIS musí být nainstalována na všech distribučních bodech a je nutné vybrat toto nastavení, aby bylo možné pokračovat v průvodci.  

### <a name="site-system-installation-account"></a>Účet instalace systému lokality

U distribučních bodů, které jsou nainstalovány na serveru lokality, je pro použití jako účet instalace systému lokality podporován pouze počítačový účet serveru lokality. Další informace najdete v tématu [účty](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).  


## <a name="enrollment-point"></a><a name="BKMK_Enrollment_Point"></a>Bod registrace  

Body registrace se používají k instalaci počítačů macOS a registraci zařízení, která spravujete pomocí místní správy mobilních zařízení. Další informace najdete v těchto článcích:  

- [Postup nasazení klientů na počítače Mac](../../../clients/deploy/deploy-clients-to-macs.md)  

- [Jak uživatelé registrují zařízení pomocí místní správy MDM](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

### <a name="allowed-connections"></a>Povolená připojení

Nastavení HTTPS se vybere automaticky a vyžaduje certifikát PKI na serveru pro ověřování serverů zprostředkujícího bodu registrace a šifrování dat přes SSL. Další informace najdete v tématu [požadavky na certifikát PKI](../../../plan-design/network/pki-certificate-requirements.md).  

Příklad nasazení certifikátu serveru a informace o jeho konfiguraci ve službě IIS najdete v části [Nasazení certifikátu webového serveru pro systémy lokality, na kterých běží IIS](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  


## <a name="enrollment-proxy-point"></a><a name="BKMK_Enrollment_Proxy_Point"></a>Zprostředkující bod registrace  

Další informace o tom, jak nastavit zprostředkující bod registrace pro mobilní zařízení, najdete v tématu [jak uživatelé registrují zařízení pomocí místní](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)správy mobilních zařízení (MDM).  

### <a name="client-connections"></a>Připojení klientů

Nastavení HTTPS se vybere automaticky. Vyžaduje následující certifikáty PKI na serveru:

- Pro ověřování serverů pro mobilní zařízení a počítače Mac, které zaregistrujete pomocí Configuration Manager
- Pro šifrování dat přes SSL (Secure Sockets Layer) (SSL)

Další informace o požadavcích na certifikát najdete v tématu [požadavky na certifikát PKI](../../../plan-design/network/pki-certificate-requirements.md).  

Příklad nasazení certifikátu serveru a informace o jeho konfiguraci ve službě IIS najdete v části [Nasazení certifikátu webového serveru pro systémy lokality, na kterých běží IIS](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  


## <a name="fallback-status-point"></a><a name="BKMK_Fallback_Status_Point"></a>Bod záložního stavu  

### <a name="number-of-state-messages-and-throttle-interval-in-seconds"></a>Počet stavových zpráv a interval omezení (v sekundách)

Výchozí nastavení pro tyto možnosti jsou 10 000 zpráv o stavu a 3 600 sekund pro interval omezení. Tato nastavení jsou ve většině případů dostačující, možná je budete muset změnit, pokud jsou splněné obě následující podmínky:  

- Bod záložního stavu akceptuje připojení pouze z intranetu.  

- Použijete bod záložního stavu během zavádění nasazení klienta pro mnoho počítačů.  

V tomto scénáři může průběžný Stream stavových zpráv vytvořit nevyřízené položky zpráv o stavu, které způsobují vysoké využití procesoru na serveru lokality po dobu trvalého období. Kromě toho se v konzole Configuration Manager a v sestavách nasazení klientů nemusí zobrazovat aktuální informace o nasazení klienta.  

Tato nastavení záložního stavového bodu jsou navržená tak, aby se vytvořila pro stavové zprávy, které se generují během nasazování klienta. Nastavení nejsou určena pro problémy s komunikací klientů, například když se klienti na Internetu nemohou připojit k internetovému bodu správy. Protože záložní stavový bod nemůže použít tato nastavení pouze pro stavové zprávy, které jsou generovány během nasazování klienta, nekonfigurujte tato nastavení, pokud záložní stavový bod akceptuje připojení z Internetu.  

Každý počítač, který úspěšně nainstaloval klienta Configuration Manager, odesílá do záložního stavového bodu tyto čtyři stavové zprávy:  

- Nasazení klienta bylo spuštěno.  

- Nasazení klienta se podařilo.  

- Přiřazení klienta bylo spuštěno.  

- Přiřazení klienta bylo úspěšné.  

Počítače, které nelze nainstalovat nebo které přiřazují Configuration Manager klienta odesílají další zprávy o stavu.  

Pokud například nasadíte klienta Configuration Manager do počítačů 20 000, může nasazení odesílat zprávy o stavu 80 000 do záložního stavového bodu. Vzhledem k tomu, že výchozí konfigurace omezování 10 000 umožňuje odesílat zprávy o stavu pro použití náhradní lokality do záložního stavového bodu každých 3 600 sekund (1 hodina), stavové zprávy mohou být nevyhlášeny do bodu záložního stavu. Zvažte také dostupnou šířku pásma sítě mezi záložním stavovým bodem a serverem lokality a výpočetní silou serveru lokality, aby bylo možné zpracovat mnoho stavových zpráv.  

Chcete-li zabránit těmto problémům, zvažte zvýšení počtu stavových zpráv a snížení intervalu omezení.  

Obnovte hodnoty omezení pro bod stavu pro použití náhradní lokality, pokud je splněna některá z následujících podmínek:  

- Vypočítáte, že aktuální hodnoty omezení jsou vyšší než požadované pro zpracování stavových zpráv ze záložního stavového bodu.  

- Zjistíte, že aktuální nastavení omezení vytváří vysoké využití procesoru na serveru lokality.  

Neměňte nastavení pro nastavení omezení záložního stavového bodu, pokud nerozumíte důsledkům. Když například zvýšíte nastavení omezení na vysoká, může se využití procesoru na serveru lokality zvýšit na vysokou, což zpomaluje všechny operace v lokalitě.  
