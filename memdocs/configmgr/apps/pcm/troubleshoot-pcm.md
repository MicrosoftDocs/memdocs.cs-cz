---
title: Řešení potíží s nástrojem Package Conversion Manager
titleSuffix: Configuration Manager
description: Naučte se řešit problémy s nástrojem Package Conversion Manager v Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cb616925-bb94-4b7c-a867-b3d95aef4d5e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05110714d3aa8ca48ff9384f0116338b0092fde1
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83877626"
---
# <a name="troubleshoot-package-conversion-manager"></a>Řešení potíží s nástrojem Package Conversion Manager

*Platí pro: Configuration Manager (Current Branch)*

<!--1357861-->

Informace v tomto článku vám pomůžou při řešení potíží při použití Správce převodu balíčků.



## <a name="sms-provider"></a>SMS Provider

Package Conversion Manager používá poskytovatele služby SMS. Další informace najdete v tématu [plánování poskytovatele serveru SMS](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).

Pokud poskytovatel serveru SMS nepracuje správně, konzola Configuration Manager včetně balíčku pro převod balíčku nefunguje.



## <a name="package-readiness"></a>Připravenost balíčku

Před převodem balíčku na aplikaci Analyzujte balíček pomocí funkce **analyzovat** Package Conversion Manager. Po analýze přidejte do uzlu **balíčky** konzoly Configuration Manager sloupec **připravenosti** . Seznam balíčků zobrazuje jeden z následujících stavů připravenosti balíčku analyze:

- **Automaticky**: balíček je možné přímo převést pomocí funkce **Convert** .      

  > [!NOTE]  
  > Automatický převod nepřevede dotazy WQL do požadavků aplikace. Tyto dotazy můžete převést pomocí procesu **opravit a převést** .  

- **Ruční**: balíček potřebuje nějaké dodatky nebo změny, aby ho bylo možné převést pomocí funkce **opravit a převést** .  

- **Nelze použít**: balíček není vhodný pro převod. Buď opravte všechny problémy s balíčkem, nebo ho nasaďte jako balíček.  

- **Chyba**: balíček obsahuje chyby. Před analýzou a převodem můžete tyto chyby opravit ručně.  

Podokno podrobností uzlu **balíčky** v konzole Configuration Manager zobrazuje všechny problémy s připraveností. Vyberte balíček a potom v podokně podrobností vyberte kartu **Souhrn** .



## <a name="log-files"></a>Soubory protokolů

### <a name="enable-logging"></a>Povolit protokolování

Pokud povolíte protokolování pro Package Conversion Manager, protokoluje všechny jeho akce, výjimky a chyby.

Chcete-li povolit protokolování této součásti v Configuration Manager, upravte soubor **Microsoft. ConfigurationManagement. exe. config**. Ve výchozím nastavení je tento konfigurační soubor umístěný v následující cestě:  
`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`  

> [!IMPORTANT]
> Počínaje verzí 1910 se tato cesta změnila na použití `Microsoft Endpoint Manager` složky. Ujistěte se, že nepoužíváte starší verzi souboru, která může existovat v jiné složce.

Do prvku **System. Diagnostics** po posledním elementu **sources** vložte následující **přepínače** a **Trace** XML Elements:

``` XML
</sources>

    <switches>
      <add name="PcmLogging" value="3"/>
    </switches>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <add name="PcmTraceListener" type="Microsoft.ConfigurationManagement.UserCentric.Logging.RolloverLogTraceListener, Microsoft.ConfigurationManagement.UserCentric.Logging" initializeData="%UserProfile%\AppData\Local\Temp\PcmTrace.log"/>
      </listeners>
    </trace>

</system.diagnostics>
```

Tato ukázka používá soubor **PCMTrace. log**. Tento protokol je v počítači se spuštěnou konzolou Configuration Manager v následující cestě:  
`%UserProfile%\AppData\Local\Temp`

Chcete-li nakonfigurovat úroveň podrobností, změňte nastavení sledovacího přepínače **PcmLogging** . Nastavte tuto hodnotu na čtyři úrovně podrobností, od nejméně podrobných ( `1` ) až po nejpodrobnější ( `4` ).


### <a name="smsprovlog"></a>SMSProv.log

V některých situacích se informace týkající se řešení potíží s procesem převodu balíčku nacházejí v souboru **Smsprov. log** . Tento soubor zachycuje informace od poskytovatele serveru SMS Configuration Manager.

Ve výchozím nastavení se tento soubor protokolu nachází na Configuration Manager serveru lokality v následující cestě:  
`C:\Program Files\Microsoft Configuration Manager\Logs`

Pokud se zobrazí některá z následujících chybových zpráv, soubor **Smsprov. log** může obsahovat relevantní informace pro řešení potíží:

- `The SMS Provider reported an error`

- `Generic Failure`

Tyto chybové zprávy obvykle označují, že došlo k chybě na serveru lokality a že informace o chybě nebyly odeslány do konzoly Configuration Manager.

Další informace najdete v tématu [technické informace o chybových zprávách správce převodu balíčků](error-messages.md).



## <a name="changing-package-attributes-after-analysis"></a>Změna atributů balíčku po analýze

Po analýze balíčku a má stav připravenosti **Automatické** nebo **Ruční**, může proces převodu selhat, pokud změníte kterýkoli z relevantních atributů.

Například analyzujete balíček a jeho stav připravenosti je **Automatický**. Potom do balíčku přidáte další program. Převod balíčku se nemusí zdařit.

Pokud potřebujete provést změny balíčku po analýze, znovu spusťte analýzu před převodem. 



## <a name="see-also"></a>Viz také

[Technické informace o chybových zprávách správce převodu balíčků](error-messages.md)
