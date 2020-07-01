---
title: Aktualizace a údržba
titleSuffix: Configuration Manager
description: Seznamte se s konzolovou metodou služby nazvanou aktualizace a údržba, která usnadňuje vyhledání a instalaci doporučených aktualizací.
ms.date: 06/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4f92d95b4e1cc814db72b45cfb92cb989b7767c8
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/01/2020
ms.locfileid: "85591013"
---
# <a name="updates-and-servicing-for-configuration-manager"></a>Aktualizace a údržba pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager používá konzolovou metodu služby nazvanou **aktualizace a údržba**. Tato konzolová metoda usnadňuje vyhledání a instalaci doporučených aktualizací pro vaši infrastrukturu Configuration Manager. Obsluha v konzole je doplněná o vzdálené aktualizace, jako jsou třeba opravy hotfix. Vzdálené aktualizace jsou určené pro zákazníky, kteří potřebují vyřešit problémy, které by mohly být specifické pro jejich prostředí.  

> [!TIP]  
> Výrazy *upgradu*, *aktualizace*a *instalace* se používají k popisu tří samostatných konceptů v Configuration Manager. Další informace o tom, jak se jednotlivé podmínky používají, najdete v tématu věnovaném [upgradu, aktualizaci a instalaci](../../understand/upgrade-update-install.md).  

## <a name="baseline-and-update-versions"></a><a name="bkmk_Baselines"></a> Základní a aktualizované verze  

Nejnovější základní verzi použijte při instalaci nové lokality v nové hierarchii.

- K upgradu ze System Center 2012 Configuration Manager taky použít základní verzi.  

- Po upgradu na Configuration Manager aktuální větev nepoužívejte základní verze, aby zůstaly aktuální. Místo toho je třeba použít [konzolové aktualizace](install-in-console-updates.md) k aktualizaci na nejnovější verzi.  

- Další základní verze jsou vydány pravidelně. Když k instalaci nové hierarchie použijete nejnovější základní verzi, nebudete instalovat zastaralou nebo nepodporovanou verzi Configuration Manager, po které následuje další upgrade vaší infrastruktury, aby se aktualizovaly v aktuálním stavu.  

Po dokončení instalace základní verze jsou další verze Configuration Manageru dostupné jako konzolové aktualizace. Konzolové aktualizace aktualizují vaši infrastrukturu na nejnovější verzi Configuration Manageru.  

- Konzolové aktualizace se instalují, když chcete aktualizovat verzi lokality nejvyšší úrovně.  

- Aktualizace, které nainstalujete na lokalitu centrální správy, se automaticky instalují v podřízených primárních lokalitách. Řízení tohoto časování pomocí časového období údržby v primární lokalitě.  

- Ručně aktualizujte sekundární lokality na novou verzi aktualizace v konzole nástroje.  

Když nainstalujete aktualizaci, uloží aktualizace Instalační soubory pro tuto verzi na server lokality ve složce s názvem **CD. Nejnovější**. Další informace o těchto souborech najdete [na disku CD. Poslední složka](the-cd.latest-folder.md)  

- Použijte soubory z disku CD-ROM. Poslední složka během Site Recovery. I když v hierarchii již neběží základní verze, nainstalujte další lokality pomocí těchto souborů.  

- Instalační soubory nemůžete použít z CD. Nejnovější k instalaci první lokality nové hierarchie nebo k upgradu lokality ze System Center 2012 Configuration Manager.  

### <a name="version-details"></a>Podrobnosti o verzi

Některé aktualizace pro Configuration Manager jsou dostupné jako verze konzolové aktualizace pro stávající infrastrukturu i jako nová základní verze.  

#### <a name="supported-versions"></a>Podporované verze

Následující podporované verze Configuration Manager jsou aktuálně k dispozici jako základní, aktualizace nebo obojí:  

| Verze | Datum dostupnosti | [Datum ukončení podpory](current-branch-versions-supported.md) | Standardní hodnoty | Aktualizace v konzole |  
|-------------|-----------|------------|--------------|------------------------|  
| [**2002**](../../plan-design/changes/whats-new-in-version-2002.md)<br /> (5.00.8968) | 1. dubna 2020 | Od 1. října 2021 | Ano,<sup>[Poznámka: 1](#bkmk_note1)</sup> | Ano |
| [**1910**](../../plan-design/changes/whats-new-in-version-1910.md)<br /> (5.00.8913) | 29. listopadu 2019 | 29. května 2021 | Ne | Ano |
| [**1906**](../../plan-design/changes/whats-new-in-version-1906.md)<br /> (5.00.8853) | 26. července 2019 | 26. ledna 2021 | Ne | Ano |
| [**1902**](../../plan-design/changes/whats-new-in-version-1902.md)<br /> (5.00.8790) | 27. března 2019 | 27. září 2020 | Ano,<sup>[Poznámka: 1](#bkmk_note1)</sup> | Ano |
| [**1810**](../../plan-design/changes/whats-new-in-version-1810.md)<br /> (5.00.8740) | 27. listopadu 2018 | 1. prosince 2020 | Ne | Ano |

**Datum dostupnosti** je, když je uvolněna [úvodní aktualizační kanál](checklist-for-installing-update-2002.md#early-update-ring) . Pokud je aktualizace globálně dostupná, bude na službě Volume License Service Center k dispozici základní médium.

<a name="bkmk_note1"></a>

> [!Note]  
> <sup>**Poznámka 1:**</sup> Základní médium je k dispozici jako součást následujících vydání na [službě Volume License Service Center](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC):
>
> - Microsoft Endpoint ConfigMgr (aktuální větev)
> - System Center Datacenter
> - System Center Standard  
>
> Vyhledejte například VLSC pro `Microsoft Endpoint Configmgr (current branch)` . V seznamu souborů Najděte základní médium a Stáhněte si ho pro tuto verzi.  

#### <a name="historical-versions"></a>Historické verze

V následující tabulce jsou uvedené historické verze Configuration Manager aktuální větev, které nepodporují:

| Verze | Datum dostupnosti | Datum ukončení podpory | Standardní hodnoty | Aktualizace v konzole |  
|-------------|-----------|------------|--------------|------------------------|  
| **1806** <br /> (5.00.8692) | 31. července 2018 | 31. ledna 2020 | Ne | Ano |
| **1802** <br /> (5.00.8634) | 22. března 2018 | 22. září 2019 | Ano | Ano |
| **1710** <br /> (5.00.8577) | 20. listopadu 2017 | 20. května 2019 | Ne | Ano |
| **1706** <br /> (5.00.8540) | 31. července 2017 | 31. července 2018 | Ne | Ano |
| **1702** <br /> (5.00.8498) | 27. března 2017 | 27. března 2018 | Ano | Ano |
| **1610** <br /> (5.00.8458) | 18. listopadu 2016 | 18. listopadu 2017 | Ne | Ano |
| **1606** <br /> (5.00.8412.1000) | 22. července 2016 | 22. července 2017 | Ne | Ano |
| **1606 s KB3186654** <br />5.00.8412.1307) | 12. října 2016 | 12. října 2017 | Ano | Ne |
| **1602** <br /> (5.00.8355) | 11. března 2016 | 11. března 2017 | Ne | Ano |
| **1511** <br /> (5.00.8325) | 8. prosince 2015 | 8. prosince 2016 | Ano | Ne |  

#### <a name="how-to-check-the-version"></a>Jak ověřit verzi

Chcete-li zjistit verzi Configuration Manager webu, v konzole nástroje v levém horním rohu konzoly vyhledejte **informace o Configuration Manager** . V tomto dialogovém okně se zobrazí verze lokality a konzoly.  

> [!Note]  
> Verze konzoly se mírně liší od verze lokality. Podverze konzoly odpovídá verzi Configuration Manager vydané verze. Například v Configuration Manager verze 1802 je počáteční verze lokality 5.0.8634.1000 a počáteční verze konzoly je 5. **1802**. 1082,1700. Čísla Build (1082) a revize (1700) se můžou v budoucích opravách hotfix změnit.

## <a name="in-console-updates-and-servicing"></a><a name="bkmk_inconsole"></a> Konzolové aktualizace a údržba  

Když použijete instalaci Configuration Manager aktuální větve připravené pro produkční prostředí, většina aktualizací je dostupná pomocí kanálu **aktualizace a údržba** . Tato metoda identifikuje, stahuje a zpřístupňuje aktualizace, které se vztahují k aktuální verzi infrastruktury a konfiguraci. Obsahuje jenom ty aktualizace, které společnost Microsoft doporučuje pro všechny zákazníky.

Mezi tyto aktualizace patří:  

- Nové verze, jako je verze 1906, 1910 nebo 2002.

- Aktualizace, které zahrnují nové funkce pro aktuální verzi.

- Opravy hotfix pro vaši verzi Configuration Manager a všechny zákazníky, kteří mají nainstalovat.

    > [!Note]  
    > Od verze 1902 mají teď v konzole opravy hotfix vztahy k nahrazení. Další informace najdete v tématu [nahrazování pro konzoly hotfix v konzole](#bkmk_supersede).

Konzolové aktualizace poskytují zvýšení stability a řeší běžné problémy. Nahrazují typy aktualizací zjištěné pro předchozí verze produktu, jako jsou aktualizace Service Pack, kumulativní aktualizace, opravy hotfix, které platí pro všechny zákazníky a rozšíření pro Microsoft Intune.

Konzolové aktualizace se můžou vztahovat na jeden nebo více následujících systémů:  

- Servery primární lokality a lokality centrální správy  

- Systémové servery lokality a role systémů lokality  

- Instance poskytovatele serveru SMS  

- Konzoly Configuration Manager  

- Configuration Manager klienti  

Configuration Manager zjistí nové aktualizace za vás. Synchronizujte spojovací bod služby Configuration Manager s cloudovou službou Microsoftu a zaznamenali jsme následující chování:  

- Když je spojovací bod služby v režimu online, vaše lokalita se každý den synchronizuje s Microsoftem. Automaticky identifikuje nové aktualizace, které se vztahují k vaší infrastruktuře. Chcete-li stáhnout aktualizace a distribuovatelné soubory, počítač, který je hostitelem role systému lokality spojovacího bodu služby, používá kontext **systému** pro přístup k následujícím internetovým umístěním: go.microsoft.com a download.Microsoft.com. Další informace o dalších umístěních používaných spojovacím bodem služby najdete v tématu [požadavky na přístup k Internetu](../deploy/configure/about-the-service-connection-point.md#bkmk_urls).  

- Když je spojovací bod služby v režimu offline, použijte nástroj pro připojení služby k ruční synchronizaci s cloudem Microsoftu. Další informace najdete v tématu [použití nástroje pro připojení služby](use-the-service-connection-tool.md).  

- Konzolové aktualizace nahrazují nutnost nezávisle vyhledávat a instalovat jednotlivé aktualizace, aktualizace Service Pack a nové funkce.  

- Nainstalujte jenom konzolové aktualizace, které si zvolíte. Při instalaci některých aktualizací můžete vybrat jednotlivé funkce, které chcete povolit a používat. Další informace naleznete v části [Enable optional features from updates](install-in-console-updates.md#bkmk_options).  

Při instalaci konzolové aktualizace dojde k následujícímu procesu:  

- Automaticky spustí kontrolu požadovaných součástí. Tuto kontrolu můžete také ručně spustit před zahájením instalace.  

- Instaluje se v lokalitě nejvyšší úrovně ve vašem prostředí. Tato lokalita je lokalita centrální správy, pokud ji máte. V hierarchii se aktualizace automaticky nainstaluje v primárních lokalitách. Určuje, kdy může každý server primární lokality aktualizovat [službu pomocí okna služby pro servery lokality](service-windows.md).  

- Po aktualizaci serveru lokality se automaticky aktualizují všechny dotčené role systému lokality. Mezi tyto role patří instance poskytovatele služby SMS. Poté, co lokalita nainstaluje aktualizaci, Configuration Manager konzoly také vyzve uživatele konzoly k aktualizaci konzoly.  

- Pokud aktualizace zahrnuje klienta Configuration Manager, nabídne se vám možnost otestovat tuto aktualizaci v předprodukčním prostředí, nebo nainstalovat aktualizaci na všechny klienty hned.  

- Po aktualizaci primární lokality se sekundární lokality neaktualizují automaticky. Místo toho je nutné ručně spustit aktualizaci sekundární lokality.  

> [!NOTE]  
> Configuration Manager aktuální větev, dlouhodobá údržba a větev Technical Preview mají různé verze. Aktualizace, které platí pro jednu větev, nejsou k dispozici jako konzolové aktualizace pro ostatní větve. Další informace o dostupných větvích najdete v tématu [kterou větev Configuration Manager mám použít?](../../understand/which-branch-should-i-use.md).

### <a name="supersedence-for-in-console-hotfixes"></a><a name="bkmk_supersede"></a>Nahrazování pro konzolové opravy hotfix

<!-- 3229613 -->
Od verze 1902 mají teď v konzole opravy hotfix vztahy k nahrazení. Když společnost Microsoft publikuje novou opravu hotfix Configuration Manager, konzola nezobrazí žádné opravy hotfix, které jsou nahrazeny touto novou opravou hotfix. Toto nové chování vám pomůže lépe určit, které opravy hotfix nainstalovat.

### <a name="supersedence-example"></a>Příklad nahrazení

K dispozici jsou tři opravy hotfix: hotfix-A, hotfix-B a hotfix-C. Oprava hotfix-A je nahrazena opravou hotfix-B a oprava hotfix-B je nahrazena opravou hotfix-C.

|Oprava hotfix – A|Oprava hotfix – B|Oprava hotfix-C|Zobrazení v konzole|
|--------|--------|--------|---------------|
|Nenainstalováno|Nenainstalováno|Nenainstalováno|Zobrazit všechny tři opravy hotfix|
|Nainstalovaný|Nainstalovaný|Nenainstalováno|Oprava hotfix-B zobrazí jako nainstalované<br/>Oprava hotfix-C ukáže jako připraveno k instalaci.|
|Nenainstalováno|Nenainstalováno|Nainstalovaný|Oprava hotfix-C zobrazuje jako nainstalované|

## <a name="out-of-band-hotfixes"></a><a name="bkmk_outofband"></a> Nestandardní opravy hotfix  

Některé opravy hotfix mají k dispozici omezené dostupnosti k vyřešení konkrétních problémů. Další opravy hotfix platí pro všechny zákazníky, ale nemůžou se instalovat pomocí konzolové metody. Tyto opravy se doručují samostatně a cloudové služby Microsoftu je nerozpoznávají.  

Při řešení potíží s nasazením Configuration Manager obvykle můžete získat informace o opravách hotfix z oddělení služeb zákaznické podpory společnosti Microsoft, článku znalostní báze podpory společnosti Microsoft nebo [blogu týmu Configuration Manager](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/bg-p/ConfigurationManagerBlog).

Tyto opravy nainstalujete ručně pomocí jedné z následujících dvou metod:  

### <a name="update-registration-tool"></a>Nástroj pro registraci aktualizací

Tento nástroj ručně naimportuje opravu hotfix do konzoly Configuration Manager. Pak nainstalujte aktualizaci jako konzolové aktualizace, které se objevují automaticky.  

Tato metoda se používá pro opravy hotfix, které používají následující strukturu názvů souborů:  
    `<Product>-<product version>-<KB article ID>-ConfigMgr.Update.exe`

Další informace najdete v tématu [použití nástroje pro registraci aktualizací k importu oprav hotfix](use-the-update-registration-tool-to-import-hotfixes.md).  

### <a name="hotfix-installer"></a>Instalační program oprav hotfix

Tento nástroj použijte k ruční instalaci opravy hotfix, která se nedá nainstalovat pomocí konzolové metody.  

Tato metoda se používá pro opravy, které používají následující strukturu názvů souborů:  
    `<Product>-<product version>-<KB article ID>-<platform>-<language>.exe`  

Další informace najdete v tématu [použití instalačního programu oprav hotfix k instalaci aktualizací](use-the-hotfix-installer-to-install-updates.md).  

## <a name="next-steps"></a>Další kroky

Následující články vám pomůžou pochopit, jak najít a nainstalovat různé typy aktualizací pro Configuration Manager:  

- [Instalace konzolových aktualizací](install-in-console-updates.md)  

- [Použití nástroje pro připojení služby](use-the-service-connection-tool.md)  

- [Použití nástroje pro registraci aktualizací k importu oprav hotfix](use-the-update-registration-tool-to-import-hotfixes.md)  

- [Instalace aktualizací pomocí instalačního programu oprav hotfix](use-the-hotfix-installer-to-install-updates.md)  

Další informace o větvi Technical Preview najdete v tématu [Technical Preview](../../get-started/technical-preview.md).
