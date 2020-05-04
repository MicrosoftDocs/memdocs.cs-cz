---
title: Vlastnosti instalace klienta ve službě Active Directory
titleSuffix: Configuration Manager
description: Publikování Configuration Manager vlastností instalace klienta do Active Directory Domain Services.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 101d7d4d-92db-419d-b2ae-3c1c1dea68e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49b2edf7234e53c3fc03542f803933463190e8c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712068"
---
# <a name="about-client-installation-properties-published-to-active-directory-domain-services"></a>Vlastnosti instalace klienta publikované ve službě Active Directory Domain Services

*Platí pro: Configuration Manager (Current Branch)*

Když rozšíříte schéma služby Active Directory pro Configuration Manager a lokalita je publikována v Active Directory Domain Services, je mnoho vlastností instalace klienta Publikováno na Active Directory Domain Services. Pokud počítač dokáže tyto vlastnosti instalace klienta vyhledat, může je použít během Configuration Manager nasazení klienta.  

 Použití služby AD DS (Active Directory Domain Services) k publikování vlastností instalace klienta má následující výhody:  

-   Klientské instalace na základě bodu aktualizace softwaru a instalace klienta Zásady skupiny nevyžadují, aby byly v každém počítači nastavené parametry instalačního programu.  

-   Protože jsou tyto informace generovány automaticky, je omezeno riziko lidské chyby související s ručním zadáváním vlastností instalace.  

> [!NOTE]  
>  Další informace o rozšíření schématu služby Active Directory pro Configuration Manager a o tom, jak publikovat lokalitu, najdete v tématu [rozšíření schématu pro Configuration Manager](../../plan-design/network/schema-extensions.md).  

## <a name="client-installation-properties-published-to-active-directory-domain-services"></a>Vlastnosti instalace klienta publikované na Active Directory Domain Services  
Následuje seznam vlastností instalace klienta. Další informace o jednotlivých položkách uvedených níže najdete v tématu [informace o vlastnostech instalace klienta](../../../core/clients/deploy/about-client-installation-properties.md).  

- Kód Configuration Manager lokality.  

- Podpisový certifikát serveru lokality  

- Důvěryhodný kořenový klíč  

- Porty pro komunikaci klienta pro protokol HTTP a HTTPS  

- Bod záložního stavu. Pokud má lokalita více bodů záložního stavu, publikuje se do Active Directory Domain Services jenom první nainstalovaná verze.  

- Nastavení indikující, že klient musí komunikovat pouze pomocí protokolu HTTPS.  

- Nastavení související s certifikáty PKI:  

  -   Možnost použití certifikátu PKI klienta  

  -   Kritéria výběru certifikátu pro výběr. To může být nutné, protože klient má více než jeden platný certifikát PKI, který lze použít pro Configuration Manager.  

  -   Nastavení určující, který certifikát bude použit, pokud má klient více platných certifikátů po dokončení procesu výběru certifikátu.  

  -   Seznam vydavatelů certifikátů, který obsahuje seznam důvěryhodných kořenových certifikátů CA.  

- Vlastnosti instalace Client.msi, které jsou zadány na kartě **Klient** v dialogovém okně **Vlastnosti klientské nabízené instalace** .

Instalace klienta (CCMSetup) používá vlastnosti, které jsou publikovány do Active Directory Domain Services pouze v případě, že nejsou zadány žádné jiné vlastnosti pomocí některého z následujících postupů:  

-   Metoda ruční instalace (popsaná dále v tomto článku)

-   Metoda instalace Zásady skupiny (popsaná dále v tomto článku)

> [!NOTE]  
>  Vlastnosti instalace klienta se používají k instalaci klienta nástroje. Po instalaci klienta a jeho úspěšném přiřazení k Configuration Manager může být tato vlastnost přepsána novým nastavením ze své přiřazené lokality.  

 Pomocí podrobností v následujících částech určíte, které Configuration Manager metody instalace klienta používají Active Directory Domain Services k získání vlastností instalace klienta.  

## <a name="client-push-installation"></a>Klientská nabízená instalace  
 Klientská nabízená instalace nepoužije službu AD DS (Active Directory Domain Services) k získání vlastností instalace.  

 Místo toho můžete zadat vlastnosti instalace klienta na kartě **vlastnosti instalace** v dialogovém okně **Vlastnosti klientské nabízené instalace** . Tyto možnosti nastavení lokality související s klientem jsou uloženy v souboru, který klient během instalace přečte.  

> [!NOTE]  
>  Nemusíte zadávat žádné vlastnosti služby CCMSetup pro klientskou nabízenou instalaci, bod záložního stavu nebo důvěryhodný kořenový klíč na kartě **vlastnosti instalace** . Tato nastavení jsou klientům automaticky dodávána při jejich instalaci pomocí klientské nabízené instalace.
Kromě vlastností Client. msi podporuje CCMSetup následující parametry:/forcereboot,/skipprereq,/Logon,/BITSPriority,/downloadtimeout,/forceinstall.

 Všechny vlastnosti, které zadáte na kartě **vlastnosti instalace** , se publikují do Active Directory Domain Services, pokud je web publikovaný na Active Directory Domain Services. Tato nastavení jsou přečtena instalacemi klienta v případě spuštění služby CCMSetup bez vlastností instalace.  

## <a name="software-update-point-based-installation"></a>Instalace aktualizace softwaru z bodu  
 Metoda instalace aktualizace softwaru z bodu nepodporuje přidání vlastností instalace do příkazového řádku služby CCMSetup.  

 Pokud nebyly v klientském počítači zajištěny žádné vlastnosti příkazového řádku pomocí zásad skupiny, služba CCMSetup vyhledá vlastnosti instalace ve službě AD DS (Active Directory Domain Services).  

## <a name="group-policy-installation"></a>Instalace zásad skupiny  
 Metoda instalace zásad skupiny nepodporuje přidání vlastností instalace do příkazového řádku služby CCMSetup.  

 Pokud nebyly v klientském počítači zajištěny žádné vlastnosti příkazového řádku, služba CCMSetup vyhledá vlastnosti instalace ve službě AD DS (Active Directory Domain Services).  

## <a name="manual-installation"></a>Ruční instalace  
 CCMSetup vyhledává Active Directory Domain Services pro vlastnosti instalace za následujících podmínek:  

-   Po příkazu CCMSetup.exe nejsou určeny žádné vlastnosti příkazového řádku.  

-   Prostřednictvím zásad skupiny nebyl počítač opatřen žádnými vlastnostmi instalace.  

## <a name="logon-script-installation"></a>Instalace skriptu přihlášení  
 CCMSetup vyhledává Active Directory Domain Services pro vlastnosti instalace za následujících podmínek:  

-   Po příkazu CCMSetup.exe nejsou určeny žádné vlastnosti příkazového řádku.  

-   Prostřednictvím zásad skupiny nebyl počítač opatřen žádnými vlastnostmi instalace.  

## <a name="software-distribution-installation"></a>Instalace distribuce softwaru  
 CCMSetup vyhledává Active Directory Domain Services pro vlastnosti instalace za následujících podmínek:  

-   Po příkazu CCMSetup.exe nejsou určeny žádné vlastnosti příkazového řádku.  

-   Prostřednictvím zásad skupiny nebyl počítač opatřen žádnými vlastnostmi instalace.  

## <a name="installations-for-clients-that-cannot-access-active-directory-domain-services"></a>Instalace klientů, kteří nemají přístup k Active Directory Domain Services  
Tyto klientské počítače nemohou číst nebo přistupovat k publikovaným vlastnostem instalace z Active Directory Domain Services.

 Mezi tyto klienty patří:  

-   Počítače v pracovní skupině.  

-   Klienti přiřazení k Configuration Manager lokalitě, která není publikována v Active Directory Domain Services.  

-   Klienti, kteří jsou nainstalováni, když jsou připojeni k Internetu.  
