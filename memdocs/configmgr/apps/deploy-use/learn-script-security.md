---
title: Další informace o zabezpečení PowerShellových skriptů
titleSuffix: Configuration Manager
description: Materiály, které vám pomůžou získat informace o zabezpečení PowerShellového skriptu.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: a0bd093d-67a5-4f74-bf79-dd604889f5ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6b519d60be094bb7c39f738d04322009b36a409f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075859"
---
# <a name="learn-more-about-powershell-script-security"></a>Další informace o zabezpečení PowerShellových skriptů

*Platí pro: Configuration Manager (Current Branch)*

Zodpovídá za správce při ověřování navržených prostředí PowerShell a parametrů prostředí PowerShell ve svém prostředí. Tady je několik užitečných prostředků, které vám pomůžou informovat správce o výkonu PowerShellu a potenciálních rizikových plochách. Důvodem je to, aby se zmírnily potenciální rizikové plochy a povolovaly se používat bezpečné skripty.

## <a name="powershell-script-security"></a>Zabezpečení skriptů PowerShellu
Integrovaná do skriptů pro spuštění je funkce pro vizuální kontrolu a schvalování skriptů, které se vyžadují ke spuštění v prostředí. Správci by si měli být vědomi, že skripty prostředí PowerShell můžou mít neoprávněný skript: skript, který je škodlivý a obtížné detekovat vizuální kontrolu během procesu schvalování skriptu. Osvědčeným postupem je použití určitých kontrolních nástrojů, a to ještě při vizuálním prohlížení skriptů PowerShellu, pomůže detekovat podezřelé problémy se skripty. Tyto nástroje nemůžou vždy určit záměr autora prostředí PowerShell, aby mohl dostat pozornost na podezřelý skript. Nástroje ale budou vyžadovat, aby správce mohl posoudit, jestli se jedná o škodlivou nebo záměrné syntaxi skriptu.

## <a name="recommendations"></a>Doporučení
- Seznamte se s osvědčenými postupy zabezpečení PowerShellu pomocí různých odkazů, které jsou odkazovány níže.
- **Podepište své skripty**: jinou metodou pro zachování zabezpečení skriptů je jejich prověřené a podepsání před jejich importem pro použití.
- Neukládejte tajné klíče (například hesla) ve skriptech PowerShellu a přečtěte si další informace o zpracování tajných kódů.


## <a name="general-information-about-powershell-security-best-practices"></a>Obecné informace o osvědčených postupech zabezpečení PowerShellu

Tato kolekce odkazů se rozhodla dát správcům Configuration Manager výchozí bod pro získání informací o osvědčených postupech zabezpečení skriptu PowerShellu.  

[Seznámení s osvědčenými postupy zabezpečení PowerShellu](https://blogs.msdn.microsoft.com/powershell/2013/12/16/powershell-security-best-practices/ )

[Osvědčené postupy zabezpečení PowerShellu v PowerPointu](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/74/metablogapi/1055.PowerShell-Security-Best-Practices_3CA24C32.pptx)

<iframe src="https://channel9.msdn.com/Events/Blue-Hat-Security-Briefings/BlueHat-Security-Briefings-Fall-2013-Sessions/PowerShell-Best-Practices/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

[Ochrana proti útokům na PowerShell, blog týmu PowerShellu](https://blogs.msdn.microsoft.com/powershell/2017/10/23/defending-against-powershell-attacks/)

[Ochrana před útoky pomocí PowerShellu na Twitter, z Microsoft PowerShellu a poradce zabezpečení Holmes Novák](https://twitter.com/Lee_Holmes/status/922462821081694208)

[Ochrana před vkládáním škodlivého kódu](https://blogs.msdn.microsoft.com/powershell/2006/11/22/protecting-against-malicious-code-injection/)

[PowerShell s modrým týmem, popisuje protokolování hloubkového bloku skriptu, protokolování chráněných událostí, antimalwarové kontroly rozhraní API pro generování zabezpečeného kódu.](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)

[Pro Windows 10 je k dispozici rozhraní API pro rozhraní prověřování proti malwaru](https://cloudblogs.microsoft.com/microsoftsecure/2015/06/09/windows-10-to-offer-application-developers-new-malware-defenses/?source=mmpc)

## <a name="powershell-parameters-security"></a>Zabezpečení parametrů PowerShellu
Předávání parametrů je způsob, jak mít flexibilitu s vašimi skripty a odložit rozhodnutí do doby spuštění. Otevře se také další rizikový povrch. Osvědčené postupy pro prevenci škodlivých parametrů nebo injektáže skriptu jsou:

- Povoluje použití předem definovaných parametrů.
- K ověření povolených parametrů použijte funkci regulárního výrazu.
    - Příklad: Pokud je povolen pouze určitý rozsah hodnot, použijte regulární výraz pro kontrolu pouze těch znaků nebo hodnot, které mohou být v rozsahu.
    - Ověřování parametrů vám může zabránit uživatelům, kteří chtějí používat určité znaky, jako jsou například uvozovky. Mějte na paměti, že existuje několik typů uvozovek, takže použití regulárních výrazů k ověření, které znaky, které jste určili, je často snazší než pokus o definování všech vstupů, které nejsou přípustné.
- Využijte modul PowerShellu ["injektáže Hunterem"](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) v Galerie prostředí PowerShell.
    - Může se jednat o falešně pozitivních hodnot, aby bylo možné zjistit, zda se jedná o skutečný problém nebo ne. 
- Microsoft Visual Studio má analyzátor skriptu, který může pomoct s kontrolou syntaxe PowerShellu.
- Toto video s názvem "DEF CON 25-Novák Holmes-Get $pwnd: proútočit na systém Windows Server" obsahuje přehled typů problémů, které lze zabezpečit proti (obzvláště v části 12:20 až 17:50):    <iframe width="560" height="315" src="https://www.youtube.com/embed/ahxMOAAani8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## <a name="environment-recommendations"></a>Doporučení pro prostředí
Obecná doporučení pro správce PowerShellu
1. Nasaďte nejnovější verzi PowerShellu, jako je verze 5 nebo vyšší, která je integrovaná do Windows 10. Alternativně můžete nasadit rozhraní [Windows Management Framework](https://www.microsoft.com/download/details.aspx?id=54616). 
2. Povolte a Shromážděte protokoly prostředí PowerShell, volitelně včetně protokolování chráněných událostí. Tyto protokoly zahrňte do pracovních postupů pro vaše podpisy, lovecké a reakce na incidenty.
3. Implementujte dostatečně velkou správu systémů s vysokými hodnotami, abyste vyloučili nebo omezili přístup správce k těmto systémům.
4. Nasazením zásad řízení aplikací v programu Windows Defender umožníte předběžně schváleným úlohám správy používání celé možnosti jazyka PowerShellu a omezení interaktivního a neschváleného použití na omezené podmnožinu jazyka PowerShellu.
5. Nasaďte Windows 10 a poskytněte poskytovateli antivirového programu úplný přístup k veškerému obsahu (včetně vygenerovaného obsahu nebo deaktivace za běhu) zpracovávaných hostiteli Windows scripters, včetně PowerShellu.
