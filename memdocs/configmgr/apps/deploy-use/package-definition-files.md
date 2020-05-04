---
title: Definiční soubory balíčků
titleSuffix: Configuration Manager
description: Informace o použití definičních souborů balíčku k vytváření balíčků a programů v nástroji Configuration Manager
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2de963d7-ffb9-43c3-9e1d-fc992b67bebd
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 0d2d0dcad06c18b13b337185ae1feb768a7ee323
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710136"
---
# <a name="package-definition-files"></a>Definiční soubory balíčků

*Platí pro: Configuration Manager (Current Branch)*

Definiční soubory balíčku jsou skripty, které vám pomůžou automatizovat vytváření [balíčků a programů](packages-and-programs.md) v Configuration Manager. Poskytují všechny informace, které Configuration Manager potřebují k vytvoření balíčku a programu, s výjimkou umístění zdrojových souborů balíčku.

## <a name="about-the-package-definition-file-format"></a>O formátu definičního souboru balíčku

Každý definiční soubor balíčku je textový soubor ASCII nebo UTF-8, který používá formát souboru. ini. Obsahuje následující oddíly:  

### <a name="pdf"></a>[PDF]

Tato část identifikuje soubor jako definiční soubor balíčku. Obsahuje tyto informace:  

- **Verze**: Zadejte verzi formátu definičního souboru balíčku, kterou soubor používá. Tato verze odpovídá verzi Configuration Manager, pro kterou byla napsána. Tato položka je povinná.  

### <a name="package-definition"></a>[Definice balíčku]

Zadejte vlastnosti balíčku a programu. Poskytuje tyto informace:  

- **Name** (Název): Název balíčku, maximálně 50 znaků.  

- **Verze** (volitelné): verze balíčku, maximálně 32 znaků.  

- **Ikona** (volitelné): soubor, který obsahuje ikonu, která se má použít pro tento balíček. Když se tato ikona zadá, nahradí výchozí ikonu balíčku v konzole Configuration Manager.

- **Publisher** (Vydavatel): Vydavatel balíčku, maximálně 32 znaků.

- **Language** (Jazyk): Jazyková verze balíčku, maximálně 32 znaků.

- **Komentář** (volitelné): komentář k balíčku, maximálně 127 znaků.

- **ContainsNoFiles**: Tato položka označuje, zda má balíček nějaké zdrojové soubory.  

- **Programy**: programy, které definujete pro tento balíček. Každý název programu odpovídá části **[Program]** v tomto definičním souboru balíčku.  

    Příklad:  

    `Programs=Typical, Custom, Uninstall`  

- **MIFFileName** (Název souboru MIF): Název souboru MIF (Management Information Format), který obsahuje stav balíčku, maximální délka 50 znaků.  

- **MIFName**: název balíčku pro párování souborů MIF, maximálně 50 znaků.  

- **MIFVersion (**: číslo verze balíčku pro párování souborů MIF, maximálně 32 znaků.  

- **Mifpublisher (vydavatel**: Vydavatel softwaru balíčku pro párování souborů MIF, maximálně 32 znaků.  

### <a name="program"></a>[Program]

Do položky **programy** v části **[definice balíčku]** přidejte část [program] pro každý program, který zadáte. Tato část definuje každý program. Jednotlivé oddíly programu obsahují následující informace:  

- **Name** (Název): Název programu, maximálně 50 znaků. Tato položka musí být v rámci balíčku jedinečná.  

- **Ikona** (volitelné): Zadejte soubor, který obsahuje ikonu, která se má použít pro tento program. Tato ikona nahradí výchozí ikonu programu v konzole Configuration Manager. Klient také zobrazí tuto ikonu při nasazení programu do kolekce.

- **Komentář** (volitelné): komentář k programu, maximálně 127 znaků.

- **CommandLine**: Zadejte příkazový řádek pro program, maximálně 127 znaků. Příkaz je relativní vzhledem ke zdrojové složce balíčku.

- **StartIn**: Určete pracovní složku pro program, maximálně 127 znaků. Tato položka může představovat absolutní cestu v klientském počítači nebo cestu, která je relativní vzhledem ke zdrojové složce balíčku.

- **Spustit**: Určete režim programu, ve kterém se program spouští. Můžete zadat hodnotu **Minimized** (Minimalizované), **Maximized** (Maximalizované) nebo **Hidden** (Skryté). Pokud tuto položku nezadáte, program se spustí v normálním režimu.  

- **AfterRunning**: zadejte jakoukoli speciální akci, která nastane po úspěšném dokončení programu. Dostupné jsou možnosti **SMSRestart** (Restart SMS), **ProgramRestart** (Restart programu) a **SMSLogoff** (Odhlášení SMS). Pokud tuto položku nezadáte, program nespustí žádnou zvláštní akci.  

- **EstimatedDiskSpace (odhadované**: zadejte velikost místa na disku, které softwarový program vyžaduje ke spuštění v počítači. Výchozí hodnota je **neznámá**. Hodnotu můžete nastavit jako celé číslo větší nebo rovno nule. Pokud zadáte hodnotu, uveďte také jednotky pro hodnotu.  

    Příklad:  

    `EstimatedDiskSpace=38MB`  

- **EstimatedRunTime (**: zadejte odhadovanou dobu v minutách, po kterou se očekává, že se program spustí v klientském počítači. Výchozí hodnota je **120**. Můžete nastavit hodnotu jako celé číslo větší než nula nebo **neznámá**.  

    Příklad:  

    `EstimatedRunTime=25`  

- **SupportedClients**: Určete procesory a operační systémy, na kterých se tento program spouští. Jednotlivé platformy oddělte čárkami. Pokud tuto položku nezadáte, klient nekontroluje podporované platformy pro tento program.  

- **SupportedClientMinVersionX**, **SupportedClientMaxVersionX**: Zadejte počáteční a koncový rozsah pro čísla verzí operačních systémů, které jsou zadány v položce **SupportedClients** .  

    Příklad:  

    ```INI
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999
    ```  

- **AdditionalProgramRequirements** (volitelné): zadejte další informace nebo požadavky pro klientské počítače, maximálně 127 znaků.

- **CanRunWhen (kdy**: zadejte stav uživatele, který program vyžaduje ke spuštění v klientském počítači. Dostupné jsou hodnoty **UserLoggedOn** (Přihlášený uživatel), **NoUserLoggedOn** (Žádný přihlášený uživatel) a **AnyUserStatus** (Libovolný stav uživatele). Výchozí hodnota je **UserLoggedOn** (Přihlášený uživatel).  

- **UserInputRequired**: Určete, zda program vyžaduje interakci s uživatelem. Dostupné jsou hodnoty **True** (Pravda) a **False** (Nepravda). Výchozí hodnota je **true (pravda**). Tato položka je nastavena na **hodnotu false** , pokud **CanRunWhen (kdy** není nastavena na **UserLoggedOn**.  

- **AdminRightsRequired**: Určete, zda program vyžaduje pověření správce v počítači, který má být spuštěn. Dostupné jsou hodnoty **True** (Pravda) a **False** (Nepravda). Výchozí hodnota je **false (NEPRAVDA**). Tato položka je nastavena na **hodnotu true** , pokud **CanRunWhen (kdy** není nastavena na **UserLoggedOn**.  

- **UseInstallAccount**: Určete, jestli program používá účet instalace klientského softwaru, když běží na klientských počítačích. Ve výchozím nastavení je nastavená hodnota **False** (Nepravda). Pokud je položka **CanRunWhen** (Kdy se může spustit) nastavená na hodnotu **UserLoggedOn** (Přihlášený uživatel), má tato položka také hodnotu **False** (Nepravda).  

- **DriveLetterConnection (**: Určete, zda program vyžaduje připojení písmene jednotky k souborům balíčku v distribučním bodu. Můžete zadat hodnotu **True** (Pravda), nebo **False** (Nepravda). Výchozí hodnota je **false**, což umožňuje programu používat připojení UNC (Universal Naming Convention). Pokud je tato hodnota nastavená na **true**, klient použije další dostupné písmeno jednotky od Z: a pokračuje dál.  

- **SpecifyDrive** (volitelné): zadejte písmeno jednotky, které program vyžaduje pro připojení k souborům balíčku v distribučním bodě. Toto nastavení vynucuje použití zadaného písmene jednotky pro připojení klientů k distribučním bodům.

- **ReconnectDriveAtLogon (**: Určete, zda se počítač znovu připojí k distribučnímu bodu, když se uživatel přihlásí. Dostupné jsou hodnoty **True** (Pravda) a **False** (Nepravda). Výchozí hodnota je **false (NEPRAVDA**).  

- **DependentProgram**: Zadejte program v tomto balíčku, který se musí spustit před aktuálním programem. Tato položka používá formát `DependentProgram=<ProgramName>`, kde `<ProgramName>` je záznam **názvu** pro daný program v definičním souboru balíčku. Pokud nejsou žádné závislé programy, nechte tuto položku prázdnou.  

    Příklady:  

    `DependentProgram=Admin`  
    `DependentProgram=`  

- **Přiřazení**: Určete, jak bude program přiřazen uživatelům. Tato hodnota může být:

    - **FirstUser (**: program spustí pouze prvního uživatele, který se přihlásí ke klientovi.
    - **EveryUser**: každý uživatel, který se přihlásí, spustí program

    Pokud **CanRunWhen (kdy** není nastavená na **UserLoggedOn**, tato položka je nastavená na **FirstUser (**.  

- **Disabled**: Určuje, jestli je možné tento program nasadit do klientů. Dostupné jsou hodnoty **True** (Pravda) a **False** (Nepravda). Výchozí hodnota je **false (NEPRAVDA**).  


## <a name="use-a-package-definition-file"></a>Použít definiční soubor balíčku  

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte položku **Správa aplikací**a vyberte uzel **balíčky** .  

2. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte možnost **vytvořit balíček z definice**.  

3. Na stránce **definice balíčku** v **Průvodci vytvořením balíčku z definice**vyberte existující definiční soubor balíčku. Chcete-li otevřít nový definiční soubor balíčku, vyberte možnost **Procházet**. Když zadáte nový definiční soubor balíčku, vyberte ho v seznamu **definice balíčku** .

4. Na stránce **zdrojové soubory** zadejte informace o požadovaných zdrojových souborech pro balíček a program.  

5. Pokud balíček vyžaduje zdrojové soubory, na stránce **Zdrojová složka** zadejte umístění, ze kterého může lokalita získat zdrojové soubory.  

6. Dokončete průvodce.  


## <a name="see-also"></a>Viz také

[Balíčky a programy](packages-and-programs.md)
