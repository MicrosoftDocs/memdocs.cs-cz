---
title: Podpora proxy serveru
titleSuffix: Configuration Manager
description: Přečtěte si, jak Configuration Manager servery systému lokality používají proxy servery.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5581214dd786bdefd29d0e4d2626de536ad26ace
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718711"
---
# <a name="proxy-server-support-in-configuration-manager"></a>Podpora proxy serveru v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Některé Configuration Manager servery systému lokality vyžadují připojení k Internetu. Pokud vaše prostředí vyžaduje internetový provoz pro použití proxy server, nakonfigurujte tyto role systému lokality tak, aby používaly proxy server.  

- Počítač, který je hostitelem serveru systému lokality, podporuje jednu konfiguraci proxy server. Všechny role systému lokality v tomto počítači sdílejí stejnou konfiguraci proxy serveru. Pokud potřebujete samostatné proxy servery pro různé role nebo instance role, umístěte tyto role na samostatné servery systému lokality.  

- Když konfigurujete nové nastavení proxy server pro server systému lokality, který už má konfiguraci proxy server, původní konfigurace se přepíše.  

- Ve výchozím nastavení připojení k proxy serveru používají **systémový** účet počítače, který je hostitelem role systému lokality.  

- Pokud se účet počítače nedá ověřit, může server systému lokality ukládat přihlašovací údaje uživatele, aby se mohl připojit k proxy server. Tyto přihlašovací údaje jsou **proxy server účet systému lokality**.  

## <a name="site-system-roles-that-use-a-proxy"></a>Role systému lokality, které používají proxy server

Následující role systému lokality se připojují k Internetu a v případě potřeby můžou použít proxy server:  

### <a name="asset-intelligence-synchronization-point"></a>Bod synchronizace katalogu Asset Intelligence

Tato role systému lokality se připojuje k Microsoftu a používá konfiguraci proxy server v počítači, který je hostitelem bodu synchronizace funkce Asset Intelligence.  

### <a name="cloud-distribution-point"></a>Distribuční bod cloudu

Role distribučního bodu cloudu běží v Microsoft Azure. Tuto roli systému lokality nenakonfigurujete pro použití proxy serveru. Nastavte konfiguraci proxy serveru na serveru primární lokality, který spravuje distribuční bod cloudu.  

Pro tuto konfiguraci server primární lokality:  

- Aby bylo možné nastavit, monitorovat a distribuovat obsah do distribučního bodu cloudu, musí být schopný se připojit k Microsoft Azure.  

- Ve výchozím nastavení používá k vytvoření připojení **systémový** účet počítače. V případě potřeby může také použít účet proxy server systému lokality.  

- Používá rozhraní API webového prohlížeče Windows.  

### <a name="distribution-point"></a>Distribuční bod

<!-- 5856396 -->

Pokud v aplikaci verze 2002 povolíte Configuration Manager distribuční bod pro internetovou mezipaměť připojenou od Microsoftu, může komunikovat neověřenou proxy server pro přístup k Internetu. Další informace najdete v tématu [mezipaměť Microsoft připojené k síti](../hierarchy/microsoft-connected-cache.md).

### <a name="exchange-server-connector"></a>konektor systému Exchange Server

Tato role systému lokality se připojuje k systému Exchange Server. Používá konfiguraci proxy server v počítači, který je hostitelem konektoru systému Exchange Server.  

### <a name="service-connection-point"></a>Spojovací bod služby

Tato role systému lokality se připojuje ke cloudové službě Configuration Manager a stahuje aktualizace verze pro Configuration Manager. Používá proxy server nakonfigurované na počítači, který je hostitelem spojovacího bodu služby.  

### <a name="software-update-point"></a>Bod aktualizace softwaru

Tato role systému lokality používá proxy server, když se připojuje k Microsoft Update ke stažení oprav a synchronizaci informací o aktualizacích. Stejně jako u každé jiné role systému lokality nejprve nakonfigurujte nastavení proxy serveru systému lokality. Pak nakonfigurujte následující možnosti, které jsou specifické pro bod aktualizace softwaru:  

- **Použít proxy server při synchronizaci softwarových aktualizací.**  

- **Použít proxy server při stahování obsahu pomocí pravidel automatického nasazení.**  

    > [!NOTE]
    > I když je k dispozici použití, není toto nastavení používáno body aktualizace softwaru v sekundárních lokalitách.  

Tato nastavení jsou na kartě **nastavení serveru proxy a účtu** ve vlastnostech bodu aktualizace softwaru.  

> [!NOTE]
> Ve výchozím nastavení platí, že při spuštění pravidel automatického nasazení se pro připojení k Internetu a stahování aktualizací softwaru používá **systémový** účet na serveru lokality, ve kterém se vytvořilo pravidlo automatického nasazení. Případně nakonfigurujte a použijte účet proxy server systému lokality. 
>
> Pokud tento účet nemůže získat přístup k Internetu, aktualizace softwaru se nepodařilo stáhnout. Do **protokolu RuleEngine. log**se zaprotokoluje následující položka:  
> `Failed to download the update from internet. Error = 12007.`  

## <a name="other-features-that-use-the-proxy-for-a-site-system-server"></a><a name="bkmk_other"></a>Další funkce, které používají proxy server pro server systému lokality

*(Představené ve verzi 2002)*

Počínaje verzí 2002 Configuration Manager následující funkce používají proxy server, který je hostitelem role [spojovacího bodu služby](#service-connection-point) : <!--5913817-->

- [Zjišťování uživatelů Azure Active Directory (Azure AD)](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)
- [Zjišťování skupin uživatelů Azure AD](../../servers/deploy/configure/about-discovery-methods.md#bkmk_azuregroupdisco)
- [Synchronizace výsledků členství kolekce do skupin Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)

## <a name="configure-the-proxy-for-a-site-system-server"></a>Konfigurace proxy serveru pro server systému lokality  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** . Rozbalte položku **Konfigurace lokality**a pak vyberte uzel **servery a role systému lokality** .  

2. Vyberte server systému lokality, který chcete upravit. V podokně podrobností klikněte pravým tlačítkem myši na roli **systému lokality** a vyberte možnost **vlastnosti**.  

3. V okně Vlastnosti systému lokality přepněte na kartu **proxy** . nakonfigurujte následující nastavení proxy serveru:  

    - **Při synchronizaci informací z Internetu použít proxy server**: tuto možnost vyberte, pokud chcete serveru systému lokality povolit použití proxy server.  

    - **Název proxy serveru**: zadejte název hostitele nebo plně kvalifikovaný název domény proxy server ve vašem prostředí.  

    - **Port**: Zadejte síťový port, na kterém se má komunikovat s proxy server. Ve výchozím nastavení používá port **80**.  

    - **Použijte přihlašovací údaje pro připojení k proxy server**: mnoho proxy serverů vyžaduje ověření uživatele. Ve výchozím nastavení používá systémový server lokality svůj počítačový účet pro připojení k proxy server. V případě potřeby tuto možnost povolte, klikněte na tlačítko **nastavit**a zvolte **existující účet** nebo zadejte **nový účet**. Tyto přihlašovací údaje jsou **proxy server účet systému lokality**.  Další informace najdete v tématu [účty používané v Configuration Manager](../hierarchy/accounts.md).  

4. Kliknutím na **tlačítko OK** uložte novou konfiguraci proxy server.  
