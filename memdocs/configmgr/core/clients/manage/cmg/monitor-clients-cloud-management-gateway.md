---
title: Monitorovat bránu pro správu cloudu
titleSuffix: Configuration Manager
description: Monitorujte klienty a síťový provoz přes bránu pro správu cloudu (CMG).
ms.date: 06/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b3233dc2f6bd13e56f7555536c95d42a34e01d5e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714224"
---
# <a name="monitor-cloud-management-gateway"></a>Monitorovat bránu pro správu cloudu

*Platí pro: Configuration Manager (Current Branch)*

Po spuštění brány pro správu cloudu (CMG) a připojení klientů přes ni můžete monitorovat klienty a síťový provoz, abyste se ujistili, že víte, jak služba funguje.


## <a name="monitor-clients"></a>Monitorování klientů

Klienti připojení prostřednictvím CMG se zobrazí v konzole Configuration Manager stejným způsobem jako místní klienti. Další informace najdete v tématu [monitorování klientů](../monitor-clients.md).


## <a name="monitor-traffic-in-the-console"></a>Monitorování provozu v konzole nástroje

Monitorujte provoz v CMG pomocí konzoly Configuration Manager:

1. Otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **Brána pro správu cloudu** .  

2. V podokně seznamu vyberte CMG.  

3. Prohlédněte si informace o přenosech v podokně podrobností pro bod připojení CMG a role systému lokality, ke kterým se připojuje. Tyto statistiky znázorňují žádosti klientů přicházející do těchto rolí. Požadavky zahrnují zásady, umístění, registraci, obsah, inventář a oznámení klientů.<!-- SCCMDocs#1208 -->

## <a name="set-up-outbound-traffic-alerts"></a>Nastavení výstrah odchozích přenosů

Výstrahy odchozího provozu vám pomůžou zjistit, kdy síťový provoz přiblíží prahovou hodnotu na 14 dní. Při vytváření CMG můžete nastavit výstrahy provozu. Pokud jste tuto část přeskočili, můžete nastavit upozornění i po spuštění služby. Nastavení výstrah upravte kdykoli.

1. Otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **Brána pro správu cloudu** .  

2. V podokně se seznamem vyberte CMG a pak na pásu karet vyberte **vlastnosti** .  

3. Pro povolení prahové hodnoty a výstrah použijte kartu **výstrahy** . Zadejte prahovou hodnotu pro data z 14 dnů v gigabajtech (GB). Určete také procento prahové hodnoty pro zvýšení počtu různých úrovní výstrahy.  

4. Až to bude hotové, vyberte **OK**.  


## <a name="monitor-logs"></a>Monitorování protokolů

CMG vygeneruje položky v určitém počtu souborů protokolu. Další informace najdete v tématu [protokoly Configuration Manager](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="cloud-management-dashboard"></a>Řídicí panel pro správu cloudu

<!--1358461-->
Od verze 1806 řídicí panel pro správu cloudu poskytuje centralizované zobrazení pro CMG využití. Když je lokalita připojená ke [službě Azure](../../../servers/deploy/configure/azure-services-wizard.md) pro správu cloudu, zobrazuje také data o cloudových uživatelích a zařízeních.  

Následující snímek obrazovky je součástí řídicího panelu pro správu cloudu, který ukazuje dva z dostupných dlaždic:  
![Dlaždice řídicího panelu správy cloudu CMG provoz a aktuální online klienti](media/1358461-cmg-dashboard.png)

V konzole Configuration Manager přejdete do pracovního prostoru **monitorování** . Vyberte uzel **Správa cloudu** a zobrazte dlaždice řídicího panelu.  


## <a name="connection-analyzer"></a>Analyzátor připojení

Počínaje verzí 1806 použijte analyzátor připojení CMG pro ověření v reálném čase pro řešení potíží. Nástroj v konzole kontroluje aktuální stav služby a komunikační kanál prostřednictvím spojovacího bodu CMG k jakýmkoli bodům správy, které povolují přenos CMG.

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** . Rozbalte položku **Cloud Services** a vyberte uzel **Brána pro správu cloudu** .  

2. Vyberte cílovou instanci CMG a pak na pásu karet vyberte **analyzátor připojení** .  

3. V okně analyzátor připojení CMG vyberte jednu z následujících možností, které se mají ověřit u služby:  

     1. **Uživatel Azure AD**: pomocí této možnosti můžete simulovat komunikaci stejným způsobem jako cloudovou identitu uživatele, která se přihlásila k zařízení s Windows 10 připojeným k Azure AD. Klikněte na **Přihlásit** se a bezpečně zadejte přihlašovací údaje pro tento uživatelský účet Azure AD.  

     2. **Certifikát klienta**: pomocí této možnosti můžete simulovat komunikaci, která je stejná jako Configuration Manager klient s [certifikátem ověřování klienta](certificates-for-cloud-management-gateway.md#bkmk_clientauth).  

4. Výběrem **Spustit** spusťte analýzu. Zobrazí se okno analyzátor s výsledky. Výběrem položky zobrazíte další podrobnosti v poli Popis.  


## <a name="stop-cmg-when-it-exceeds-threshold"></a><a name="bkmk_stop"></a>Zastavit CMG, pokud překročí prahovou hodnotu

<!--3735092-->
Počínaje verzí 1902 může Configuration Manager nyní zastavit službu CMG, když celkový přenos dat dosáhne limitu. Pomocí [výstrah](#set-up-outbound-traffic-alerts) můžete aktivovat oznámení v případě, že využití dosáhne varovné nebo kritické úrovně. Tato možnost vypne cloudovou službu, aby vám pomohla snížit případné neočekávané náklady na Azure z důvodu špičky využití.

> [!Important]  
> I když služba není spuštěná, jsou pořád náklady spojené s cloudovou službou. Zastavení služby neeliminuje všechny přidružené náklady na Azure. Pokud chcete odebrat všechny náklady na cloudovou službu, [odeberte CMG](setup-cloud-management-gateway.md#modify-a-cmg).  
>
> Když se služba CMG zastaví, internetoví klienti nebudou moct komunikovat s Configuration Manager.  

Celkový přenos dat (odchozí) zahrnuje data z cloudové služby a účtu úložiště. Tato data pocházejí z následujících toků:

- CMG na klienta  
- CMG do lokality, včetně souborů protokolu CMG  
- Pokud povolíte CMG pro obsah, účet úložiště pro klienta  

Další informace o těchto datových tocích najdete v tématu [porty CMG a tok dat](plan-cloud-management-gateway.md#ports-and-data-flow).

Prahová hodnota pro výstrahu úložiště je oddělená. Tato výstraha monitoruje kapacitu vaší instance služby Azure Storage.

Když vyberete instanci CMG v uzlu **Brána pro správu cloudu** v konzole nástroje, můžete v podokně podrobností zobrazit celkový přenos dat.

Configuration Manager kontroluje prahovou hodnotu každých šest minut. Pokud dojde k náhlému nárůstu využití, Configuration Manager může trvat až šest minut, než zjistí, že překročil prahovou hodnotu, a pak službu zastavte.

### <a name="process-to-stop-the-cloud-service-when-it-exceeds-threshold"></a>Proces zastavení cloudové služby, když překročí prahovou hodnotu

1. [Nastavte výstrahy odchozího provozu](#set-up-outbound-traffic-alerts).  

2. Na kartě **výstrahy** v okně Vlastnosti CMG povolte možnost **zastavit tuto službu v případě překročení kritické prahové hodnoty**.  

K otestování této funkce dočasně snižte jednu z následujících hodnot:  

- **prahová hodnota pro odchozí datové přenosy (GB) za 14 dní**. Výchozí hodnota je `10000`.  

- **Procento prahové hodnoty pro vyvolání kritické výstrahy** Výchozí hodnota je `90`.  
