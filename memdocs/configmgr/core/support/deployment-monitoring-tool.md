---
title: Nástroj pro monitorování nasazení
titleSuffix: Configuration Manager
description: Pomocí nástroje pro monitorování nasazení můžete řešit potíže s nasazením softwaru v klientovi Configuration Manager.
ms.date: 09/24/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9edc214f-f405-456d-80df-8adcc2a5428d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5a27e96cf69ab01b58910ae02fc732940eda8a04
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723373"
---
# <a name="deployment-monitoring-tool"></a>Nástroj pro monitorování nasazení

*Platí pro: Configuration Manager (Current Branch)*

Nástroj pro monitorování nasazení je jedním z [Configuration Manager nástrojů](tools.md). Jedná se o grafické uživatelské rozhraní navržené pro pomoc při řešení potíží s nasazením aplikace, aktualizace softwaru a standardních hodnot konfigurace v klientovi Configuration Manager. Nástroj je jen pro čtení, protože nemění žádný stav klienta. Můžete ho bezpečně použít k diagnostice běžných scénářů nasazení.


## <a name="features"></a>Funkce

- Spusťte ji jako správce a vyřešte potíže s nasazeními v místním klientovi.  

- Řešení potíží s nasazeními na vzdáleném klientovi. Spusťte nástroj a připojte se ke vzdálenému počítači jako správce.  

- Exportujte do XML veškerá data shromážděná v nástroji. Sdílejte soubor XML s ostatními a použijte ho jako běžnou platformu pro komunikaci s nasazeními.  

- Importujte dříve exportovaná data do jiného počítače a použijte je ke spuštění nástroje v režimu offline.   


## <a name="usage"></a>Využití

Nástroj pro monitorování nasazení podporuje pouze grafické uživatelské rozhraní. Chcete-li spustit nástroj, spusťte **DeploymentMonitoringTool. exe** jako správce. Existují tři zobrazení:  

- **Vlastnosti klienta**: seznam užitečných atributů zařízení a klienta Configuration Manager. Toto zobrazení je výchozí.   

- **Nasazení**: Zobrazte všechna aktuálně cílená nasazení. V podokně výsledků vyberte nasazení a zobrazte další informace v podokně podrobností.  

- **Všechny aktualizace**: Zobrazit všechny aktualizace softwaru a jejich stav.  

Chcete-li kopírovat data v jakémkoli zobrazení, vyberte buňku a stiskněte klávesu **CTRL** + **C**.


### <a name="actions-menu"></a>Nabídka akce

V nabídce **Akce** jsou k dispozici následující akce:  

- **Připojit ke vzdálenému počítači**: vyberte počítač, ke kterému se chcete připojit. Pokud nezadáte uživatelské jméno a heslo, použije se aktuální přihlašovací údaje. Kliknutím na **Uložit** se připojte ke vzdálenému počítači.  

- **Exportovat data**: vyberte soubor, do kterého chcete zapisovat data, a klikněte na **Uložit**. Použijte exportovaný soubor XML pro vzdálené řešení potíží v jiném počítači.  

- **Importovat data**: vyberte soubor, který chcete importovat do nástroje.  

- **Zobrazit protokol**: otevře přidružený soubor protokolu v závislosti na zobrazení:  
    - Vlastnosti klienta:`\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Nasazení`\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Všechny aktualizace:`C:\Windows\WindowsUpdate.log`



## <a name="see-also"></a>Viz také

- [Nasazení aplikací](../../apps/deploy-use/deploy-applications.md)
- [Nasazení aktualizací softwaru](../../sum/deploy-use/deploy-software-updates.md)
- [Nasazení standardních hodnot konfigurace](../../compliance/deploy-use/deploy-configuration-baselines.md)
