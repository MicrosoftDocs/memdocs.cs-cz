---
title: Weby pro systémy lokality
titleSuffix: Configuration Manager
description: Seznamte se s výchozími a vlastními weby pro servery systému lokality v Configuration Manager.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 681f0893-e83b-476e-9ec0-a5dc7c9deeb6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 344ba7f6a6b0ee7683c3ac7661338f01be601a10
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718690"
---
# <a name="websites-for-site-system-servers-in-configuration-manager"></a>Weby pro servery systému lokality v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Několik Configuration Manager rolí systému lokality vyžaduje použití Microsoft Internetová informační služba (IIS) a k hostování služeb systému lokality používá výchozí web služby IIS. Pokud je nutné spustit další webové aplikace na stejném serveru a nastavení nejsou kompatibilní s Configuration Manager, zvažte použití vlastního webu pro Configuration Manager.  

> [!TIP]  
>  Osvědčeným postupem zabezpečení je vyhradit server pro Configuration Manager systémy lokality, které vyžadují službu IIS. Pokud spouštíte jiné aplikace v Configuration Managerm systému lokality, zvýšíte tak plochu pro útok na daný počítač.  




##  <a name="what-to-know-before-choosing-to-use-custom-websites"></a><a name="BKMK_What2Know"></a>Co potřebujete znát, než se rozhodnete používat vlastní weby  
 Ve výchozím nastavení role systému lokality používají **Výchozí webový server** ve službě IIS. Tato funkce se nastaví automaticky při instalaci role systému lokality. V primárních lokalitách ale můžete místo toho použít vlastní weby. Při použití vlastních webů:  

-   Vlastní weby jsou povolené pro celou lokalitu, ne pro jednotlivé servery nebo role systému lokality.  

-   V primárních lokalitách musí být každý počítač, který bude hostitelem příslušné role systému lokality, nastaven s vlastním webem s názvem **SMSWEB**. Dokud nevytvoříte tento web a nakonfigurujete role systému lokality na tomto počítači pro použití vlastního webu, klienti nemusí být schopni komunikovat s rolemi systému lokality v tomto počítači.  

-   Vzhledem k tomu, že sekundární lokality jsou automaticky nastaveny pro použití vlastního webu, když je nastavena jejich primární Nadřazená lokalita, je nutné také vytvořit vlastní weby ve službě IIS na každém sekundárním serveru systému lokality, který vyžaduje službu IIS.  


  **Požadavky pro použití vlastních webů:**  

 Před povolením možnosti používat vlastní weby v lokalitě:  

-   Vytvořte vlastní web s názvem **SMSWEB** ve službě IIS na každém serveru systému lokality, který vyžaduje službu IIS. Je potřeba to udělat v primární lokalitě a všech podřízených sekundárních lokalitách.  

-   Nastavte vlastní web tak, aby odpovídal na stejný port, který jste nastavili pro Configuration Manager komunikaci klientů (port požadavku klienta).  

-   Pro všechny vlastní nebo výchozí weby, které používají vlastní složku, umístěte kopii výchozího typu dokumentu, který použijete v kořenové složce, která je hostitelem webu. Například na počítači se systémem Windows Server 2008 R2, který má výchozí konfigurace, je **soubor Iisstart. htm** jedním z několika výchozích typů dokumentů, které jsou k dispozici. Tento soubor najdete v kořenovém adresáři výchozího webu a potom do kořenové složky, která hostuje vlastní web SMSWEB, umístěte kopii tohoto souboru (nebo kopii výchozího typu používaného dokumentu). Další informace o výchozích typech dokumentů najdete v tématu [výchozí &lt;dokument\> defaultDocument pro službu IIS](https://www.iis.net/configreference/system.webserver/defaultdocument).  

**Informace o požadavcích služby IIS:**
**následující role systému lokality vyžadují službu IIS a web pro hostování služeb systému lokality:**  

-   Bod služeb webu Katalog aplikací  

-   Bod webu Katalog aplikací  

-   Distribuční bod  

-   Bod registrace  

-   Zprostředkující bod registrace  

-   Bod záložního stavu  

-   Bod správy  

-   Bod aktualizace softwaru  

-   Bod migrace stavu  

Další rozhodnutí:  

-   Pokud má primární lokalita povolené vlastní weby, klienti přiřazení k této lokalitě budou přesměrováni tak, aby komunikovali s vlastními weby, a ne s výchozími weby na příslušných serverech systému lokality.  

-   Pokud používáte vlastní weby pro jednu primární lokalitu, zvažte použití vlastních webů pro všechny primární lokality ve vaší hierarchii, abyste zajistili, že se klienti budou moct úspěšně pohybovat v rámci hierarchie. (O roamingu mluvíme, pokud se klientský počítač přesune do nového segmentu sítě, který spravuje jiná lokalita. Roaming může ovlivnit prostředky, ke kterým může klient přistupovat místně, a ne přes připojení WAN.  

-   Role systému lokality, které používají službu IIS, ale nepřijmou připojení klientů, jako je bod služby Reporting Services, používají také web SMSWEB namísto výchozího webu.  

-   Vlastní weby vyžadují, abyste přiřadili čísla portů, která se liší od těch, které používá výchozí web počítače. Výchozí web a vlastní web se nedají spouštět současně, pokud se oba weby snaží používat stejné porty TCP/IP.  

-   Porty TCP/IP, které jste nastavili ve službě IIS pro vlastní web, se musí shodovat s porty požadavků klientů pro danou lokalitu.  

## <a name="switch-between-default-and-custom-websites"></a>Přepínání mezi výchozími a vlastními weby  
I když můžete zaškrtnout nebo zrušit políčko pro použití vlastních webů v primární lokalitě kdykoliv (Toto pole je na kartě Obecné ve vlastnostech lokality), před provedením této změny je pečlivě naplánujte. Při změně této konfigurace se musí všechny příslušné role systému lokality v primární lokalitě a podřízených sekundárních lokalitách odinstalovat a potom znovu nainstalovat:  

Tyto role se **přeinstalují automaticky**:  

-   Bod správy  

-   Distribuční bod  

-   Bod aktualizace softwaru  

-   Bod záložního stavu  

-   Bod migrace stavu  

Tyto role se musí **přeinstalovat ručně**:  

-   Bod služeb webu Katalog aplikací  

-   Bod webu Katalog aplikací  

-   Bod registrace  

-   Zprostředkující bod registrace  

Dále:  

-   Když změníte výchozí web na použití vlastního webu, Configuration Manager neodebere staré virtuální adresáře. Chcete-li odebrat soubory, které Configuration Manager použity, je nutné ručně odstranit virtuální adresáře, které byly vytvořeny pod výchozím webem.  

-   Změníte-li lokalitu, aby používala vlastní weby, musí být klienti, kteří jsou již přiřazeni k lokalitě, překonfigurováni tak, aby používali nové porty požadavků klientů pro vlastní weby. Přečtěte si téma [Konfigurace portů pro komunikaci klientů](../../../core/clients/deploy/configure-client-communication-ports.md).  

## <a name="set-up-custom-websites"></a>Nastavení vlastních webů  
Protože se postup vytvoření vlastního webu liší pro jednotlivé verze operačního systému, vyhledejte přesné kroky v dokumentaci ke svému operačnímu systému. Tam, kde je to možné, použijte následující informace:  

-   Název webu musí být: **SMSWEB**.  

-   Při nastavování protokolu HTTPS je nutné před uložením konfigurace zadat certifikát SSL.  

-   Po vytvoření vlastního webu odeberte vlastní porty webu, které používáte, z jiných webů ve službě IIS:  

    1.  Upravte **vazby** ostatních webů tak, aby se odebraly porty, které odpovídají názvům, které jsou přiřazené webu **SMSWEB** .  

    2.  Spusťte web **SMSWEB** .  

    3.  Restartujte službu **SMS_SITE_COMPONENT_MANAGER** na serveru lokality.  
