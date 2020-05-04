---
title: Konfigurace portů pro komunikaci klientů
titleSuffix: Configuration Manager
description: Nastavte porty pro komunikaci klientů v Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 406bbdbf-ab4a-4121-a68b-154f96ea14ec
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 30b553bbe2a68ec97e4d5200644a88d09ee5967d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713111"
---
# <a name="how-to-configure-client-communication-ports-in-configuration-manager"></a>Postup konfigurace portů pro komunikaci klientů v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Můžete změnit čísla portů žádosti, která Configuration Manager klienti používají ke komunikaci se systémy lokality, které používají protokol HTTP a HTTPS pro komunikaci. I když je pravděpodobně protokol HTTP nebo HTTPS pro brány firewall již nakonfigurován, klientské oznámení používající protokol HTTP nebo HTTPS vyžaduje větší využití CPU a paměti v počítači bodu správy, než když použijete vlastní číslo portu. Můžete také zadat číslo portu webu, který se má použít, pokud provedete probuzení klientů pomocí tradičních paketů buzení ze spánku.  

 Když zadáte porty požadavků HTTP a HTTPS, můžete zadat výchozí číslo portu i alternativní číslo portu. Klienti automaticky vyzkouší alternativní port po nezdařené komunikaci s výchozím portem. Můžete zadat nastavení pro datovou komunikaci přes protokol HTTP a HTTPS.  

 Výchozí hodnoty pro porty požadavků klientů jsou **80** pro přenosy HTTP a **443** pro přenosy https. Změňte je pouze v případě, že nechcete používat tyto výchozí hodnoty. Typickým scénářem použití vlastních portů je použití vlastního webu ve službě IIS, nikoli výchozího webu. Pokud změníte výchozí čísla portů pro výchozí web ve službě IIS a jiné aplikace používají výchozí web, pravděpodobně selžou.  

> [!IMPORTANT]
>  Neměňte čísla portů v Configuration Manager bez porozumění důsledkům. Příklady:  
> 
> - Pokud změníte čísla portů pro služby žádosti klienta jako konfiguraci lokality a stávající klienti nebudou překonfigurováni tak, aby používali nová čísla portů, budou tito klienti spravováni jako nespravované.  
>   -   Než nakonfigurujete jiné než výchozí číslo portu, ujistěte se, že brány firewall a všechna zařízení v nich mohou tuto konfiguraci podporovat a v případě potřeby je překonfigurujte. Pokud budete spravovat klienty na internetu a změníte výchozí číslo portu HTTPS 443, může tato komunikace zablokovat směrovače a brány firewall na internetu.  

 Aby bylo zajištěno, že klienti nebudou po změně čísel portů požadavků spravováni, musí být klienti nakonfigurováni tak, aby používali nová čísla portů žádosti. Když změníte porty požadavků v primární lokalitě, všechny připojené sekundární lokality automaticky zdědí stejnou konfiguraci portů. Pomocí postupu v tomto tématu Nakonfigurujte porty požadavků v primární lokalitě.  

> [!NOTE]  
>  Informace o tom, jak nakonfigurovat porty požadavků pro klienty na počítačích se systémy Linux a UNIX, najdete v tématu [Konfigurace portů žádostí pro klienta pro Linux a UNIX](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigLnUClientCommuincations).  

 Pokud je lokalita Configuration Manager publikována Active Directory Domain Services, noví a stávající klienti, kteří mají přístup k těmto informacím, budou automaticky nakonfigurováni pomocí nastavení portu lokality a není nutné provádět další akce. Ke klientům, kteří nemohou přistupovat k těmto informacím publikovaným ve službě Active Directory Domain Services, patří klienti pracovní skupiny, klienti z jiné doménové struktury služby Active Directory, klienti nakonfigurovaní pouze jako internetoví klienti a klienti, kteří jsou aktuálně připojeni k internetu. Pokud změníte výchozí čísla portů po instalaci těchto klientů, přeinstalujte je a nainstalujte všechny nové klienty pomocí jedné z následujících metod:  

- Přeinstalujte klienty pomocí Průvodce nabízenou instalací klienta. Klientská nabízená instalace automaticky nakonfiguruje klienty s aktuální konfigurací portů lokality. Další informace o tom, jak používat Průvodce nabízenou instalací klienta, najdete v tématu [Postup instalace Configuration Manager klientů pomocí klientské nabízené](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)instalace.  

- Přeinstalujte klienty pomocí programu CCMSetup. exe a vlastností instalace Client. msi pro CCMHTTPPORT a CCMHTTPSPORT. Další informace o těchto vlastnostech najdete v tématu [informace o vlastnostech instalace klienta](../../../core/clients/deploy/about-client-installation-properties.md).  

- Přeinstalujte klienty pomocí metody, která ve službě Active Directory Domain Services vyhledá vlastnosti instalace klienta nástroje Configuration Manager. Další informace najdete v tématu [o vlastnostech instalace klienta publikovaných na Active Directory Domain Services](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

  K překonfigurování čísel portů pro existující klienty můžete použít také skript PORTSWITCH. VBS, který je součástí instalačního média ve složce SMSSETUP\Tools\PortConfiguration.  

> [!IMPORTANT]  
>  U stávajících a nových klientů, kteří jsou aktuálně připojeni k Internetu, je nutné nakonfigurovat jiná než výchozí čísla portů pomocí vlastností CCMSetup. exe Client. msi pro CCMHTTPPORT a CCMHTTPSPORT.  

 Po změně portů požadavků v lokalitě budou noví klienti, kteří jsou nainstalováni pomocí metody nabízené instalace klienta v rámci lokality, automaticky nakonfigurováni s aktuálními čísly portů pro danou lokalitu.  

#### <a name="to-configure-the-client-communication-port-numbers-for-a-site"></a>Konfigurace čísel portů pro komunikaci klientů pro lokalitu  

1. V konzole Configuration Manager klikněte na možnost **Správa**.  

2. V pracovním prostoru **Správa** rozbalte nabídku **Konfigurace lokality**, klikněte na položku **lokality**a vyberte primární lokalitu, kterou chcete nakonfigurovat.  

3. Na kartě **Domů** klikněte na **vlastnosti**a potom klikněte na kartu **porty** .  

4. Vyberte některou z položek a klikněte na ikonu vlastnosti. zobrazí se dialogové okno **Podrobnosti o portu** .  

5. V dialogovém okně **Podrobnosti o portu** zadejte číslo portu a popis položky a potom klikněte na tlačítko **OK**.  

6. Pokud použijete vlastní název webu **SMSWEB** pro systémy lokality, na kterých je spuštěna služba IIS, vyberte **použít vlastní** Web.  

7. Dialogové okno s vlastnostmi lokality zavřete kliknutím na tlačítko **OK** .  

   Tento postup opakujte u všech primárních lokalit v hierarchii.
