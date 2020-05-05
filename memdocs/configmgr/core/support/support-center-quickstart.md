---
title: Rychlý Start pro Support Center
titleSuffix: Configuration Manager
description: Rychle Zachyťte stav klienta Configuration Manager pro řešení potíží.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5cb41e2b-4c79-4da9-a432-ff869c0870f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c8c43fe1dbca9155bf9b554a2554c652b1482583
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723114"
---
# <a name="support-center-quickstart-guide"></a>Průvodce rychlým startem pro Support Center

*Platí pro: Configuration Manager (Current Branch)*

Support Center nabízí výkonné možnosti, včetně řešení potíží a prohlížení protokolů v reálném čase. Můžete ji také použít během několika minut k zachycení stavu Configuration Managerho klientského počítače. Tato možnost zahrnuje přístup ke vzdáleným klientům.

Vytvořte kompletní soubor *sady prostředků pro řešení potíží* (. zip), který zachytí stav klienta. Sada neobsahuje pouze soubory protokolu. Může zahrnovat i další typy dat, jako jsou nastavení registru a konfigurace klientů. Poskytněte sadě pracovníkovi podpory, který využívá Support Center Viewer.



## <a name="prerequisites"></a>Požadavky

- Práva místního správce pro klienta Configuration Manager  

- Instalační program nástroje Support Center. Tento soubor je na serveru lokality na adrese `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`. Další informace najdete v tématu [Support Center – Install](support-center.md#install).  



## <a name="step-1-create-a-data-bundle-on-a-local-client"></a>Krok 1: vytvoření datové sady v místním klientovi

1.  Nainstalujte si Support Center na klienta Configuration Manager.  

2.  Přejděte do nabídky **Start** , ve skupině **Microsoft System Center** vyberte **Support Center**.  

3.  Na kartě Domů na pásu karet vyberte **shromažďovat vybraná data**. Support Center standardně shromažďuje jenom minimální datovou sadu: soubory protokolů, konfiguraci klienta a operační systém.  

4.  Uložte soubor sady prostředků řešení potíží (. zip) do složky v počítači. Ve výchozím nastavení je název souboru podobný následujícímu příkladu: `Support_c885cdfed3c7482bba4f9e662978ec07.zip`.  



## <a name="step-2-view-the-data-bundle-using-support-center-viewer"></a>Krok 2: zobrazení sady dat pomocí Support Center Vieweru

1.  Spusťte **nástroj Support Center Viewer**. Tato akce může nastat v jakémkoli počítači, na kterém je nainstalovaný Support Center.  

2.  Vyberte **otevřít sadu prostředků**, přejděte k souboru sady a vyberte **otevřít**.  

3.  Po zpracování souboru nástrojem Support Center Viewer přepněte na každou dostupnou kartu. zobrazí se typy dat, které nástroj Support Center shromáždí ve výchozím nastavení:  

    - **Konfigurace**  

        - Configuration Manager konfigurace klienta  

        - Operační systém  

        - Počítač  

        - Služby  

        - Síťové adaptéry  

    - **Protokoly**: zvolte jednu nebo více položek v seznamu a vyberte **otevřít**. Tato akce otevře vybrané soubory protokolu v log Vieweru. Pomocí této funkce můžete vyhledat kódy chyb a použít rozšířené filtry, které vám pomůžou rychleji analyzovat soubory protokolů.  



## <a name="collect-more-data"></a>Shromažďování dalších dat

Kromě těchto základních funkcí podporuje Support Center také nejrůznější informace o stavu klienta. Otevřete **Centrum pro podporu** a vyberte **shromáždit všechna data**. Tento proces obvykle trvá několik minut i v novějších počítačích. Support Center shromažďuje následující dodatečná data:

- **Zásady**: Configuration Manager nastavení zásad, včetně požadované konfigurace zásad a skutečné konfigurace zásad  

- **Certifikáty**: informace o veřejném klíči pro klientské certifikáty. Support Center neshromažďuje privátní klíče certifikátu.  

- **Registr klienta**: shromažďuje informace o konfiguraci klienta z registru. Support Center shromažďuje jenom informace o Configuration Manager registru.  

- **WMI klienta**: informace o konfiguraci klienta z rozhraní WMI. Support Center neshromažďuje zásady klienta.  

- **Řešení potíží**: data pro řešení potíží v reálném čase, která vám pomůžou diagnostikovat běžné problémy klienta se službou Active Directory, body správy, sítí, přiřazením zásad a registrací.  

- **Výpisy ladění**: Proveďte ladění výpisu ladění klienta a souvisejících procesů. Výpisy ladění můžou být velké. Tuto možnost povolte jenom v případě, že chcete řešit problémy s výkonem klienta.  

