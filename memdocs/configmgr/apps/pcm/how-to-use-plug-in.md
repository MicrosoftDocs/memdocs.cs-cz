---
title: Jak používat modul plug-in převodu
titleSuffix: Configuration Manager
description: K přizpůsobení procesů analýzy a převodu použijte modul plug-in Správce převodu balíčků.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 83cf156c-36de-483f-a9e6-2e06158f3b20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4ca16ade5f8581cb124df39294c3cfc27627a346
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709877"
---
# <a name="how-to-use-the-package-conversion-manager-plug-in"></a>Jak používat modul plug-in Správce převodu balíčků

*Platí pro: Configuration Manager (Current Branch)*

<!--1357861-->

Modul plug-in Správce převodu balíčků vám pomůže přizpůsobit procesy analýzy a převodu. Chcete-li použít modul plug-in Správce převodu balíčků, zapište spustitelný soubor nebo soubor skriptu, který provede vlastní operace. Pak upravte konfigurační soubor Microsoft. ConfigurationManagement. exe. config, aby se volal spustitelný soubor nebo skript. Nejběžnější jazyky, které se používají k psaní skriptu, jsou VBScript nebo PowerShell.

Modul plug-in Správce převodu balíčku se spustí jednou pro každý balíček. Pokud analyzujete nebo převádíte více balíčků najednou, spustí se modul plug-in Správce převodu balíčku pokaždé, když je spuštěn.

> [!NOTE]  
> Další informace o prvcích Package Conversion Manageru v konfiguračním souboru Configuration Manager najdete v tématu [technické Reference k souboru XML konfigurace modulu plug-in Správce převodu balíčku](plugin-config-xml.md).



## <a name="default-process"></a>Výchozí proces

Ve výchozím nastavení provádí nástroj Package Conversion Manager následující akce:

1.  Přečtěte si balíček Configuration Manager.  

2.  Vytvořte aplikaci z balíčku a přidejte výchozí atributy.  

3.  Analyzujte aplikaci a určete stav připravenosti balíčku.  

4.  V závislosti na operaci Package Conversion Manager proveďte jednu z následujících akcí:  

    - **Analyzovat**: Zobrazte stav připravenosti balíčku v konzole Configuration Manager.  

    - **Convert**: Zapište aplikaci do databáze Configuration Manager.  


## <a name="plug-in-based-process"></a>Proces založený na modulu plug-in 

Když použijete modul plug-in, nástroj Package Conversion Manager provede následující akce:

1.  Přečtěte si balíček Configuration Manager.  

2.  Vytvořte aplikaci z balíčku a přidejte výchozí atributy.  

3.  Převeďte aplikaci na XML. Pak soubor uložte na disk.  

4.  Spusťte skript modulu plug-in a upravte XML aplikace. Další informace najdete v tématu [technické Reference k souboru XML konfigurace modulu plug-in Správce převodu balíčku](plugin-config-xml.md).  

5.  Převeďte XML aplikace do aplikace Configuration Manager.  

6.  Analyzujte aplikaci a určete stav připravenosti balíčku.  

7.  V závislosti na operaci Package Conversion Manager proveďte jednu z následujících akcí:  

    - **Analyzovat**: Zobrazte stav připravenosti balíčku v konzole Configuration Manager.  

    - **Convert**: Zapište aplikaci do Configuration Manager databáze.  



## <a name="see-also"></a>Viz také

[Technické informace o konfiguraci modulu plug-in Správce převodu balíčku pro XML](plugin-config-xml.md)
