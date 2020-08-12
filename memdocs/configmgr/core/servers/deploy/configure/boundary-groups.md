---
title: Konfigurace skupin hranic
titleSuffix: Configuration Manager
description: Pomáhat klientům najít systémy lokality pomocí skupin hranic k logické organizaci Příbuzná síťová umístění s názvem hranice
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7a925c29b5d186f3ca6f320741f5ca602b0bbb79
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128388"
---
# <a name="configure-boundary-groups-for-configuration-manager"></a>Konfigurace skupin hranic pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pomocí skupin hranic v Configuration Manager logicky uspořádejte související síťová umístění ([hranice](boundaries.md)), aby bylo snazší spravovat infrastrukturu. Než skupinu hranic použijete, přiřaďte hranice skupinám hranic.

Ve výchozím nastavení Configuration Manager vytvoří výchozí skupinu hranic lokality v každé lokalitě.

Ke konfiguraci skupin hranic přidružte hranice (síťová umístění) a role systému lokality, jako jsou distribuční body, ke skupině hranic. Tato konfigurace pomáhá přidružit klienty k systémovým serverům lokality, jako jsou distribuční body, které se nacházejí poblíž klientů v síti.

Pokud chcete zvýšit dostupnost serverů na širší rozsah síťových umístění, přiřaďte stejnou hranici a stejný server do více než jedné skupiny hranic.

Klienti používají hraniční skupinu pro:  

- Automatické přiřazení lokality  
- K vyhledání serveru systému lokality, který může poskytovat službu, včetně:

  - Distribuční body pro umístění obsahu  
  - Body aktualizace softwaru  
  - Body migrace stavu  

    > [!NOTE]
    > Bod migrace stavu nepoužívá záložní relace. Další informace najdete v tématu [Fallback](#fallback).

  - Preferované body správy  

    > [!NOTE]  
    > Pokud používáte preferované body správy, povolte tuto možnost pro hierarchii, nikoli z konfigurace skupiny hranic. Další informace najdete v tématu [Povolení použití upřednostňovaných bodů správy](boundary-group-procedures.md#bkmk_proc-prefer).  

  - Brána pro správu cloudu (počínaje verzí 1902)

## <a name="boundary-groups-and-relationships"></a>Skupiny hranic a vztahy

Pro každou skupinu hranic ve vaší hierarchii můžete přiřadit:

- Jedna nebo více hranic. **Aktuální** skupina hranic klienta je síťové umístění, které je definováno jako hranice přiřazené určité skupině hranic. Klient může mít více než jednu aktuální skupinu hranic.  

- Jedna nebo více rolí systému lokality. Klienti můžou vždycky používat role přidružené ke své aktuální skupině hranic. V závislosti na dalších konfiguracích můžou použít role v dalších skupinách hranic.  

Pro každou skupinu hranic, kterou vytvoříte, můžete nakonfigurovat jednosměrný odkaz na jinou skupinu hranic. Odkaz se nazývá **vztah**. Skupiny hranic, se kterými propojíte, se nazývají **sousední** skupiny hranic. Hraniční skupina může mít víc než jednu relaci, z nichž každá má určitou sousední skupinu hranic.

Když se klientovi nepovede najít dostupný systém lokality v aktuální skupině hranic, určí konfigurace každého vztahu, kdy začne hledat sousední skupinu hranic. Toto hledání dalších skupin se nazývá **Fallback**.

Další informace najdete v následujících postupech:  

- [Vytvořit skupinu hranic](boundary-group-procedures.md#bkmk_create)  
- [Konfigurace hraniční skupiny](boundary-group-procedures.md#bkmk_config)  

### <a name="show-boundary-groups-for-devices"></a><a name="bkmk_show-boundary"></a>Zobrazit skupiny hranic pro zařízení

<!--6521835-->

Počínaje verzí 2002 můžete zobrazit skupiny hranic pro konkrétní zařízení, abyste lépe identifikovali a vypomohli chování zařízení pomocí skupin hranic. V uzlu **zařízení** nebo při zobrazení členů **kolekce zařízení**přidejte do zobrazení seznamu nové sloupce **hraničních skupin** .

- Pokud je zařízení ve více než jedné skupině hranic, je tato hodnota čárkami oddělený seznam názvů skupin hranic.

- Data se aktualizují, když klient vytvoří požadavek na umístění na lokalitu, nebo maximálně každých 24 hodin.

- Pokud je klient roaming a není členem skupiny hranic, hodnota je prázdná.

> [!NOTE]
> Tyto informace jsou data lokality a jsou k dispozici pouze v primárních lokalitách. Pokud připojíte Configuration Manager k lokalitě centrální správy, nezobrazí se hodnota tohoto sloupce.

## <a name="fallback"></a>Záložní volba

Aby nedocházelo k problémům, když klienti nemůžou najít dostupný systém lokality v aktuální skupině hranic, definujte vztah mezi skupinami hranic pro nouzové chování. Možnost Fallback umožňuje klientovi rozšířit své hledání na další skupiny hranic a najít dostupný systém lokality.

Relace jsou nakonfigurovány na kartě **relace** vlastností hraniční skupiny. Když konfigurujete relaci, definujete odkaz na sousední skupinu hranic. Pro každý typ podporované role systému lokality nakonfigurujte nezávislé nastavení pro přechod na sousední skupinu hranic. Další informace najdete v tématu [Konfigurace nouzového chování](boundary-group-procedures.md#bkmk_bg-fallback).

Pokud například nakonfigurujete relaci na určitou skupinu hranic, nastavte záložní distribuční body po 20 minutách. Výchozí hodnota je 120 minut pro rozsáhlejší příklad, viz [Příklad použití skupin hranic](#example-of-using-boundary-groups).

Pokud se klientovi v aktuální skupině hranic nenajde dostupná role systému lokality, klient použije záložní čas v minutách. Tato záložní doba určuje, kdy klient začne hledat dostupný systém lokality přidružený ke sousední skupině hranic.  

Když klient nemůže najít dostupný systém lokality, začne hledat umístění ze sousedních hraničních skupin. Díky tomuto chování se zvyšuje fond dostupných systémů lokality. Konfigurace skupin hranic a jejich vztahů definuje použití tohoto fondu dostupných systémů lokality u klienta.

- Skupina hranic může mít více než jeden vztah. V této konfiguraci můžete pro každý typ systému lokality nakonfigurovat náhradní síť na různé sousední sítě, které se budou vyskytovat po různých časových obdobích.  

- Klienti se vrátí do hraniční skupiny, která je přímým sousedem aktuální skupiny hranic.  

- Když je klient členem více než jedné skupiny hranic, definuje svou aktuální skupinu hranic jako sjednocení všech skupin hranic. Klient se vrátí k sousedům kterékoli z těchto původních hraničních skupin.  

> [!NOTE]
> Role bodu migrace stavu nepoužívá záložní relace. Pokud přidáte jak role bodu migrace stavu, tak i distribučních bodů na stejný server systému lokality, nekonfigurujte pro skupinu hranic zálohu. Pokud pro distribuční bod potřebujete použít náhradní skupinu hranic, přidejte roli bod migrace stavu na jiný server systému lokality.<!-- 2838807 -->

### <a name="the-default-site-boundary-group"></a>Výchozí skupina hranic lokality

Můžete vytvořit vlastní skupiny hranic a každá lokalita má výchozí skupinu hranic lokality, kterou Configuration Manager vytvoří. Tato skupina má název **Default-site-hranice-Group &lt; SiteCode>**. Například skupina pro web ABC by se jmenovala **Default-site-hranice-Group &lt; ABC>**.

Pro každou skupinu hranic, kterou vytvoříte, Configuration Manager automaticky vytvoří implicitní odkaz na každou výchozí skupinu hranic lokality v hierarchii.  

- Implicitní odkaz je výchozí záložní možnost z aktuální skupiny hranic do výchozí skupiny hranic lokality. Výchozí čas Fallback je 120 minut.  

- Pro klienty, kteří nejsou v hranici přidružené k žádné skupině hranic: k identifikaci platných rolí systému lokality použijte výchozí skupinu hranic lokality z přiřazené lokality.  

Chcete-li spravovat zálohu na výchozí skupinu hranic lokality:  

- Otevřete vlastnosti výchozí skupiny hranic a změňte hodnoty na kartě **výchozí chování** . změny, které zde provedete, platí pro *všechny* implicitní odkazy na tuto skupinu hranic. Když nakonfigurujete explicitní odkaz na tuto výchozí skupinu hranic lokality z jiné skupiny hranic, přepíšete tato výchozí nastavení.  

- Otevřete vlastnosti vlastní skupiny hranic. Změňte hodnoty pro explicitní propojení na výchozí skupinu hranic lokality. Pokud pro záložní nebo záložní zálohu nastavíte novou dobu v minutách, tato změna ovlivní pouze odkaz, který konfigurujete. Konfigurace explicitního propojení přepíše nastavení na kartě **výchozí chování** výchozí skupiny hranic lokality.  

## <a name="site-assignment"></a>Přiřazení lokality  

V každé skupině hranic můžete nakonfigurovat přiřazenou lokalitu pro klienty.  

- Nově instalovaný klient, který používá automatické přiřazení lokality, se připojí k přiřazené lokalitě skupiny hranic, která obsahuje aktuální síťové umístění klienta.  

- Po přiřazení k lokalitě klient při změně svého umístění v síti nezmění své přiřazení lokality. Například klient se bude pohybovat do nového síťového umístění. Toto umístění je hranicí ve skupině hranic s jiným přiřazením lokality. Lokalita přiřazená klientovi se nemění.  

- Když zjišťování systémových prostředků služby Active Directory zjistí nový prostředek, vyhodnotí informace o síti pro daný prostředek oproti hranicím ve skupinách hranic. Tento proces přidruží nový zdroj k přiřazené lokalitě určené pro metodu automatické nabízené instalace klienta.  

- Když je hranice členem více skupin hranic s různými přiřazenými lokalitami, klienti náhodně vyberou jednu z těchto lokalit.  

- Změny v přiřazené lokalitě skupiny hranic se vztahují pouze na nové akce přiřazení lokality. Klienti, kteří dříve přiřazeni k lokalitě, nevyhodnocují znovu své přiřazení lokality na základě změn v konfiguraci skupiny hranic (nebo v jejich vlastním umístění v síti).  

Další informace o přiřazení lokality klienta najdete v tématu [použití automatického přiřazení lokality pro počítače](../../../clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment).  

Další informace o tom, jak nakonfigurovat přiřazení lokality, najdete v následujících postupech:

- [Konfigurace přiřazení lokality a výběr systémových serverů lokality](boundary-group-procedures.md#bkmk_references)
- [Konfigurace záložní lokality pro automatické přiřazení lokality](boundary-group-procedures.md#bkmk_site-fallback)

## <a name="distribution-points"></a>Distribuční body

Když klient požádá o umístění distribučního bodu, Configuration Manager odešle klientovi seznam systémů lokality. Tyto systémy lokality jsou vhodného typu přidruženého ke každé skupině hranic, která zahrnuje aktuální umístění v síti klienta:

- **Během distribuce softwaru**si klienti vyžádají umístění obsahu nasazení na platném zdroji obsahu. Toto umístění může být distribučním bodem nebo zdrojem sdílené mezipaměti.  

- **Během nasazení operačního systému**si klienti vyžádají umístění pro odeslání nebo přijetí informací o migraci stavu.  

  - Klienti získávají obsah na základě chování skupiny hranic. Další informace najdete v tématu [Podpora pořadí úkolů pro skupiny hranic](#bkmk_bgr-osd).  

Pokud klient v rámci nasazení obsahu požaduje obsah, který není dostupný ze zdroje v aktuální skupině hranic, klient bude nadále požadovat tento obsah. Klient se pokusí o různé zdroje obsahu v aktuální skupině hranic, dokud nedosáhne záložního období pro sousední nebo výchozí skupinu hranic lokality. Pokud klient ještě nenašel obsah, rozbalí jeho vyhledávání zdrojů obsahu, aby zahrnoval sousední skupiny hranic.

Pokud nakonfigurujete obsah pro distribuci na vyžádání a není k dispozici v distribučním bodě, když ho klient požaduje, lokalita zahájí přenos obsahu do tohoto distribučního bodu. Je možné, že klient najde tento server jako zdroj obsahu a pak se vrátí k použití sousední skupiny hranic.

### <a name="client-installation"></a><a name="bkmk_ccmsetup"></a>Instalace klienta

Instalační program klienta Configuration Manager, program CCMSetup, může získat obsah instalace z místního zdroje nebo přes bod správy. Jeho počáteční chování závisí na parametrech příkazového řádku, které použijete k instalaci klienta:<!-- MEMDocs#286 -->

- Pokud nepoužijete parametry **/MP** ani **/source** , program CCMSetup se pokusí získat seznam bodů správy ze služby Active Directory nebo DNS.
- Pokud zadáte jenom **/source**, vynutí instalaci ze zadané cesty. Neobjevují body správy. Pokud v zadané cestě nenalezne ccmsetup.cab, program CCMSetup se nezdařil.
- Pokud zadáte obě **/MP** i **/source**, zkontroluje zadané body správy a všechny zjistí. Pokud nemůže najít platný bod správy, přejde zpět na zadanou zdrojovou cestu.

Další informace o těchto parametrech CCMSetup najdete v tématu [parametry a vlastnosti instalace klienta](../../../clients/deploy/about-client-installation-properties.md).

<!--1358840-->
Když se CCMSetup spojí s bodem správy, aby vyhledal potřebný obsah, bod správy vrátí distribuční body na základě konfigurace hraniční skupiny. Pokud definujete vztahy na hraniční skupině, bod správy vrátí distribuční body v následujícím pořadí:

1. Aktuální skupina hranic  
2. Sousední skupiny hranic  
3. Výchozí skupina hranic lokality  

> [!Note]  
> Proces instalace klienta nepoužívá záložní čas. Pokud chcete co nejrychleji najít obsah, okamžitě se vrátí k další hraniční skupině.
>
> V předchozích verzích Configuration Manager v průběhu tohoto procesu bod správy vrátil pouze distribuční body v aktuální skupině hranic klienta. Pokud není k dispozici žádný obsah, proces instalace se vrátí ke stažení obsahu z bodu správy. Neexistovala možnost vrátit se do distribučních bodů v jiných skupinách hranic, které by mohly mít potřebný obsah.

### <a name="task-sequence-support-for-boundary-groups"></a><a name="bkmk_bgr-osd"></a>Podpora pořadí úkolů pro skupiny hranic

<!--1359025-->
Když zařízení spustí pořadí úkolů a potřebuje získat obsah, použije se chování skupiny hranic podobné jako u klienta Configuration Manager.

Toto chování nakonfigurujte na stránce **distribuční body** nasazení pořadí úloh pomocí následujících nastavení:

- **Není-li místní distribuční bod k dispozici, použijte vzdálený distribuční bod**: pro toto nasazení může pořadí úkolů přejít zpět na distribuční body v sousední hraniční skupině.  

- **Umožnit klientům používat distribuční body z výchozí skupiny hranic lokality**: pro toto nasazení může pořadí úkolů přejít zpět do distribučních bodů ve výchozí skupině hranic lokality.  

Chcete-li použít toto nové chování, nezapomeňte aktualizovat klienty na nejnovější verzi.

#### <a name="location-priority"></a>Priorita umístění  

Pořadí úkolů se pokusí získat obsah v následujícím pořadí:  

1. Zdroje sdílené mezipaměti  

2. Distribuční body v *aktuální* skupině hranic  

3. Distribuční body v *sousední* skupině hranic  

    > [!Important]  
    > Vzhledem k tomu, že se jedná o charakter zpracování pořadí úkolů v reálném čase, nečeká na dobu převzetí služeb při selhání v sousední hraniční skupině. K určení priorit sousedních skupin hranic používá dobu převzetí služeb při selhání. Například pokud pořadí úloh nezíská obsah z distribučního bodu v aktuální skupině hranic, okamžitě se pokusí distribuční bod v sousední skupině hranic s nejkratším časem převzetí služeb při selhání. Pokud se tento proces nezdařil, dojde k převzetí služeb při selhání na distribuční bod v sousední skupině hranic s větším časem převzetí služeb při selhání.  

4. Distribuční body ve výchozí skupině hranic *lokality*  

Soubor protokolu pořadí úkolů **souboru Smsts. log** zobrazuje prioritu používaných zdrojů umístění podle vlastností nasazení.

### <a name="boundary-group-options-for-peer-downloads"></a><a name="bkmk_bgoptions"></a>Možnosti skupiny hranic pro rovnocenné soubory ke stažení

<!--1356193, 1358749-->
Skupiny hranic obsahují následující dodatečná nastavení, která vám poskytnou větší kontrolu nad distribucí obsahu ve vašem prostředí:  

- [Povolí stahování ze strany partnerů v této skupině hranic.](#bkmk_bgoptions1)  

- [Během stahování po straně druhé se používají jenom partnerské uzly v rámci stejné podsítě.](#bkmk_bgoptions2)  

- [Preferovat distribuční body přes partnerské uzly se stejnou podsítí](#bkmk_bgoptions3)  

- [Preferovat cloudové distribuční body přes distribuční body](#bkmk_bgoptions4)  

Další informace o tom, jak nakonfigurovat tato nastavení, najdete v tématu [Konfigurace hraniční skupiny](boundary-group-procedures.md#bkmk_config).

Pokud je zařízení ve více než jedné skupině hranic, platí následující chování pro tato nastavení:

- **Povolí stahování ze strany partnera v této skupině hranic**: Pokud je v jedné skupině hranic zakázaná, klient nebude používat optimalizaci doručení.
- **Během stahování po straně druhé se používají jenom partnerské uzly se stejnou podsítí**: Pokud je povolená v jedné skupině hranic, toto nastavení se projeví.
- **Preferovat distribuční body přes partnerské uzly ve stejné podsíti**: Pokud je povolená v jedné skupině hranic, toto nastavení se projeví.
- **Preferovat cloudové prostředky prostřednictvím místních zdrojů**: Pokud je povolená v jedné skupině hranic, toto nastavení se projeví.

#### <a name="allow-peer-downloads-in-this-boundary-group"></a><a name="bkmk_bgoptions1"></a>Povolí stahování ze strany partnerů v této skupině hranic.

Standardně je toto nastavení povolené. Bod správy poskytuje klientům seznam umístění obsahu, která obsahují partnerské zdroje. Toto nastavení má vliv také na použití ID skupin pro [optimalizaci doručení](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization).  

Existují dva běžné scénáře, ve kterých byste měli zvážit zakázání této možnosti:  

- Máte-li skupinu hranic, která zahrnuje hranice geograficky rozptýlených umístění, jako je například síť VPN. Dva klienti můžou být ve stejné skupině hranic, protože jsou připojení prostřednictvím sítě VPN, ale v rozsáhlých různých umístěních, která jsou nevhodná pro sdílení obsahu v partnerském vztahu.  

- Použijete-li jednu velkou skupinu hranic pro přiřazení lokality, která neodkazuje na žádné distribuční body.  

> [!IMPORTANT]
> Pokud je zařízení ve více než jedné skupině hranic, ujistěte se, že toto nastavení povolíte pro všechny skupiny hranic daného zařízení. V opačném případě klient nepoužije optimalizaci doručování. Například nenastaví klíč registru DOGroupID.

#### <a name="during-peer-downloads-only-use-peers-within-the-same-subnet"></a><a name="bkmk_bgoptions2"></a>Během stahování po straně druhé se používají jenom partnerské uzly v rámci stejné podsítě.

Toto nastavení je závislé na předchozí možnosti. Pokud tuto možnost povolíte, bude bod správy obsahovat jenom v seznamu umístění obsahu partnerské zdroje, které jsou ve stejné podsíti jako klient.

Běžné scénáře pro povolení této možnosti:

- Návrh skupiny hranic pro distribuci obsahu zahrnuje jednu velkou skupinu hranic, která překrývá jiné menší skupiny hranic. Díky tomuto novému nastavení seznam zdrojů obsahu, které bod správy poskytuje klientům, zahrnuje pouze partnerské zdroje ze stejné podsítě.

- Máte jednu velkou skupinu hranic pro všechna Odloučená pracoviště. Tuto možnost povolte a klienti sdílejí obsah v rámci podsítě jenom na vzdáleném pracovišti místo rizikového sdílení obsahu mezi umístěními.

Počínaje verzí 2002 můžete v závislosti na konfiguraci sítě vyloučit určité podsítě pro porovnání. Například chcete zahrnout hranici, ale vyloučit konkrétní podsíť VPN. Ve výchozím nastavení Configuration Manager vyloučí výchozí podsíť Teredo ( `2001:0000:%` ).<!--3555777-->

> [!NOTE]
> Když při [rozšíření samostatné primární lokality](../install/prerequisites-for-installing-sites.md#bkmk_expand) do verze 2002 přidáte lokalitu centrální správy (CAS), seznam vyloučení podsítě se vrátí k výchozímu. Pokud chcete tento problém obejít, po rozšíření lokality spusťte PowerShellový skript, který přizpůsobuje seznam vyloučení podsítí na certifikačních autoritách.<!-- 6309068 -->

Importujte seznam vyloučení podsítí jako řetězec podsítě oddělený čárkami. Použijte symbol procenta ( `%` ) jako zástupný znak. Na serveru lokality nejvyšší úrovně nastavte nebo přečtěte vlastnost **SubnetExclusionList** Embedded pro součást **SMS_HIERARCHY_MANAGER** ve třídě **SMS_SCI_Component** . Další informace najdete v tématu [SMS_SCI_Component serverové třídy služby WMI](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md).

##### <a name="sample-powershell-script-to-update-the-subnet-exclusion-list"></a>Ukázkový skript PowerShellu pro aktualizaci seznamu vyloučení podsítě

Následující skript představuje vzorový způsob, jak tuto hodnotu změnit. Přidejte podsítě do proměnné **PropertyValue** po `2001:0000:%,172.16.16.0` . Je to řetězec oddělený čárkami. Spusťte tento skript na serveru lokality nejvyšší úrovně ve vaší hierarchii.

```PowerShell
$PropertyValue = "2001:0000:%,172.16.16.0"
$PropertyName = "SubnetExclusionList"

$providerMachine = Get-WmiObject -Class "SMS_ProviderLocation" -Namespace "root\sms"

if ($providerMachine -is [system.array])
{
    $providerMachine=$providerMachine[0]
}

$SiteCode = $providerMachine.SiteCode

$component = Get-WmiObject -Query 'select comp.* from sms_sci_component comp join SMS_SCI_SiteDefinition sdef on sdef.SiteCode=comp.SiteCode where sdef.ParentSiteCode="" and comp.componentname="SMS_HIERARCHY_MANAGER"' -ComputerName $providerMachine.Machine -Namespace root\sms\site_$SiteCode
$properties = $component.props

Write-host "Updating property for site " $SiteCode

foreach ($property in $properties)
{
  if ($property.propertyname -like $PropertyName)
  {
    Write-host "Current value for SubnetExclusionList is  " $property.value1
    $property.value1 = $PropertyValue
    Write-host "Updating value for SubnetExclusionList to " $property.value1
    break
  }
}

$component.props = $properties
$component.put()
```

> [!NOTE]
> Ve výchozím nastavení Configuration Manager zahrnuje podsíť Teredo v tomto seznamu. Když seznam změníte, vždy nejprve Přečtěte stávající hodnotu. Přidejte do seznamu další podsítě a pak nastavte novou hodnotu.

#### <a name="prefer-distribution-points-over-peers-with-the-same-subnet"></a><a name="bkmk_bgoptions3"></a>Preferovat distribuční body přes partnerské uzly se stejnou podsítí

Ve výchozím nastavení řídí bod správy prioritu zdrojů sdílené mezipaměti v horní části seznamu umístění obsahu. Toto nastavení obrátí prioritu u klientů, kteří jsou ve stejné podsíti jako zdroj sdílené mezipaměti.

> [!TIP]
> Toto chování platí pro klienta Configuration Manager. Neplatí, pokud pořadí úkolů stáhne obsah. Když je pořadí úloh spuštěno, dává přednost zdroji sdílené mezipaměti v distribučních bodech.<!-- SCCMDocs#1376 -->

#### <a name="prefer-cloud-distribution-points-over-distribution-points"></a><a name="bkmk_bgoptions4"></a>Preferovat cloudové distribuční body přes distribuční body

Pokud máte pobočku s rychlejším internetovým propojením, můžete nyní nastavit prioritu cloudového obsahu.  

Ve verzi 1902 je toto nastavení nyní s názvem **preferovat cloudové zdroje prostřednictvím místních zdrojů**. Mezi cloudové zdroje patří následující:<!-- SCCMDocs#1529 -->

- Distribuční body cloudu
- Microsoft Update (přidáno ve verzi 1902)

## <a name="software-update-points"></a><a name="bkmk_sup"></a>Body aktualizace softwaru 

Klienti používají skupiny hranic k vyhledání nového bodu aktualizace softwaru. Chcete-li určit, které servery může klient najít, přidejte jednotlivé body aktualizace softwaru do různých skupin hranic.

Pokud přidáte všechny existující body aktualizace softwaru do výchozí skupiny hranic lokality, klient vybere bod aktualizace softwaru z fondu dostupných serverů. Toto chování je podobné jako u předchozích verzí Configuration Manager aktuální větev. V případě řízeného výběru a nouzového chování přidejte jednotlivé body aktualizace softwaru do různých skupin hranic.

Pokud nainstalujete novou lokalitu, body aktualizace softwaru se nepřidá do výchozí skupiny hranic lokality. Přiřaďte body aktualizace softwaru do hraniční skupiny, aby je klienti mohli najít a používat.

### <a name="fallback-for-software-update-points"></a>Záloha pro body aktualizace softwaru

Záložní verze bodů aktualizace softwaru je nakonfigurována jako jiné role systému lokality, ale má následující omezení:  

#### <a name="new-clients-use-boundary-groups-to-select-software-update-points"></a>Noví klienti používají skupiny hranic k výběru bodů aktualizace softwaru

Když instalujete nové klienty, vybere bod aktualizace softwaru z těchto serverů přidružených ke skupinám hranic, které nakonfigurujete. Toto chování nahrazuje předchozí chování, kdy klienti vyberou bod aktualizace softwaru náhodně ze seznamu serverů, které sdílejí doménovou strukturu klienta.

#### <a name="clients-continue-to-use-a-last-known-good-software-update-point-until-they-fallback-to-find-a-new-one"></a>Klienti budou dál používat poslední známý dobrý bod aktualizace softwaru, dokud nebudou moct najít nový.

Klienti, kteří již mají bod aktualizace softwaru nadále jej používají, dokud nebudete mít přístup. Toto chování zahrnuje pokračující použití bodu aktualizace softwaru, který není přidružený k aktuální skupině hranic daného klienta.

Toto chování je záměrné. Klient nadále používá existující bod aktualizace softwaru, i když není v aktuální skupině hranic klienta. Když se bod aktualizace softwaru změní, klient synchronizuje data s novým serverem, což způsobí významné využití sítě. Pokud všichni klienti přejdou na nový server současně, zpoždění při přechodu pomůže vyhnout se sytosti vaší sítě.

#### <a name="a-client-always-tries-to-reach-its-last-known-good-software-update-point-for-120-minutes-before-starting-fallback"></a>Klient se vždycky pokusí spojit svůj poslední známý bod aktualizace softwaru po dobu 120 minut, než se spustí Fallback.

Pokud klient nevytvořil kontakt, po 120 minutách se spustí záložní. Když se služba Fallback spustí, klient obdrží seznam všech bodů aktualizace softwaru v aktuální skupině hranic. Další body aktualizace softwaru v sousedství a výchozí skupiny hranic na webu jsou k dispozici na základě záložních konfigurací.

### <a name="fallback-configurations-for-software-update-points"></a>Záložní konfigurace bodů aktualizace softwaru

V případě, že chcete, aby body aktualizace softwaru byly kratší než 120 minut, můžete nakonfigurovat **záložní časy (v minutách)** . Klient se ale stále snaží získat přístup k původnímu bodu aktualizace softwaru po dobu 120 minut. Pak rozbalí své hledání na další servery. Záložní doba skupiny hranic se spustí, když se klient poprvé nepřipojí k původnímu serveru. Když klient rozšíří hledání, lokalita poskytne všechny hraniční skupiny, které jsou nakonfigurovány na méně než 120 minut.

Chcete-li zablokovat použití bodu aktualizace softwaru pro sousední hraniční skupinu, nastavte nastavení na hodnotu **nikdy nespouštět**.

Po neúspěšném přístupu k původnímu serveru po dobu dvou hodin klient použije kratší cyklus k navázání připojení k novému bodu aktualizace softwaru. Díky tomuto chování může klient rychle prohledávat seznam potenciálních bodů aktualizace softwaru.

#### <a name="example"></a>Příklad

Nakonfigurujete body aktualizace softwaru v hraniční skupině *A* na přechod po **10** minutách. Nakonfigurujete stejné nastavení pro skupinu hranic *B* na **130** minut. Klient ve skupině hranic *Z* nedokáže získat přístup k poslednímu známému bodu aktualizace softwaru.

- Po dalších 120 minut se klient pokusí dosáhnout pouze původního serveru ve skupině hranic Z. Po 10 minutách Configuration Manager přidá body aktualizace softwaru z hraniční skupiny A do fondu dostupných serverů. Klient se ale nepokusí kontaktovat tyto nebo jiné servery, dokud neuplyne počáteční období 120 minut.  

- Po pokusu o kontaktování původního bodu aktualizace softwaru po dobu 120 minut klient rozšíří hledání. Přidává servery do dostupného fondu bodů aktualizace softwaru, které jsou v aktuálním a všech sousedních hraničních skupinách nakonfigurovaných na 120 minut nebo i méně. Tento fond zahrnuje servery ve skupině hranic A, které byly dříve přidány do fondu dostupných serverů.  

- Po 10 minutách klient rozšíří hledání tak, aby zahrnovalo body aktualizace softwaru ze skupiny hranic B. Toto období vychází z celkového počtu 130 minut od okamžiku, kdy se klient poprvé nedostal do svého posledního známého bodu aktualizace softwaru.  

### <a name="manually-switch-to-a-new-software-update-point"></a>Ručně přepnout na nový bod aktualizace softwaru

Spolu s Fallback můžete pomocí klientského oznámení ručně vynutit, aby se zařízení přepnulo na nový bod aktualizace softwaru.

Když přepnete na nový server, zařízení k vyhledání nového serveru použijí zálohu. Klienti v průběhu příštího cyklu prověřování aktualizací softwaru přepnou na nový bod aktualizace softwaru.<!-- SCCMDocs#1537 -->

Zkontrolujte konfigurace skupiny hranic. Než začnete s touto změnou, ujistěte se, že body aktualizace softwaru jsou ve správných skupinách hranic.

Další informace najdete v tématu [Ruční přepnutí klientů do nového bodu aktualizace softwaru](../../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs).

### <a name="intranet-clients-can-use-a-cmg-software-update-point"></a><a name="bkmk_cmg-sup"></a>Intranetové klienty můžou používat CMG bod aktualizace softwaru.
<!--7102873-->
Počínaje verzí 2006 můžou intranetové klienti získat přístup k CMG bodu aktualizace softwaru, když je přiřazený ke skupině hranic a v bodu aktualizace softwaru [je povolená možnost **Povolit Configuration Manager cloudové služby pro správu cloudu** ](../../../clients/manage/cmg/setup-cloud-management-gateway.md#bkmk_role) . Intranetovým zařízením můžete dovolit, aby kontrolovala CMG bod aktualizace softwaru v následujících scénářích:

- Když se počítač připojí k síti VPN, bude pokračovat v kontrole proti CMGmu bodu aktualizace softwaru přes Internet.
- Pokud je jediným bodem aktualizace softwaru pro skupinu hranic CMG bod aktualizace softwaru, pak se na něj budou kontrolovat všechna intranetová a Internetová zařízení.

## <a name="management-points"></a>Body správy

<!-- 1324594 -->
Konfigurace záložních vztahů pro body správy mezi hraničními skupinami. Toto chování nabízí větší kontrolu nad body správy, které klienti používají. Na kartě **relace** ve vlastnostech skupiny hranic je sloupec pro bod správy. Když přidáte novou skupinu záložních hranic, doba použití pro bod správy je aktuálně vždycky nulová (0). Toto chování je stejné jako **výchozí chování** ve výchozí skupině hranic lokality.

Dříve došlo k běžnému problému, když jste v zabezpečené síti měli chráněný bod správy. Klienti v hlavní síti obdrželi zásady, které tento chráněný bod správy zahrnovaly, i když s ním nemohli komunikovat přes bránu firewall. Chcete-li tento problém vyřešit nyní, použijte možnost **nikdy** Nezálohovat a ujistěte se, že klienti spadají pouze do bodů správy, se kterými můžou komunikovat.

> [!Note]  
> Pokud povolíte distribuční body ve výchozí skupině hranic lokality do zálohy a bod správy je společně umístěn v distribučním bodě, lokalita také přidá tento bod správy do výchozí skupiny hranic lokality.<!--VSO 2841292-->  

Pokud je klient v hraniční skupině, která nemá přiřazený bod správy, lokalita klientovi poskytne úplný seznam bodů správy. Tím se zajistí, že klient vždy obdrží seznam bodů správy.

Záložní skupina hranic bodu správy nezmění chování při instalaci klienta (ccmsetup.exe). Pokud příkazový řádek neurčí počáteční bod správy pomocí parametru/MP, nový klient obdrží úplný seznam dostupných bodů správy. Pro svůj úvodní proces zavedení používá klient první bod správy, ke kterému má přístup. Po registraci klienta s lokalitou obdrží seznam bodů správy správně seřazený s tímto novým chováním.

Další informace o chování klienta při získávání obsahu během instalace najdete v tématu [instalace klienta](#bkmk_ccmsetup).

Pokud při upgradu klienta nezadáte parametr příkazového řádku/MP, klient bude dotazovat zdroje, jako je Active Directory a WMI, pro libovolný dostupný bod správy. Upgrade klienta nedodržuje konfiguraci skupiny hranic. <!--VSO 2841292-->  

Aby mohli klienti tuto funkci používat, povolte následující nastavení: **Klienti dávají přednost používání bodů správy zadaných ve skupinách hranic** v **Nastavení hierarchie**.

> [!Note]  
> Procesy nasazení operačního systému neznají skupiny hranic pro body správy.  

### <a name="troubleshooting"></a>Poradce při potížích

Nové položky se zobrazí v **LocationServices. log**. Atribut **Local** identifikuje jeden z následujících stavů:

- **0**: neznámý  

- **1**: zadaný bod správy je pouze ve výchozí skupině hranic lokality pro záložní  

- **2**: zadaný bod správy je ve vzdálené nebo sousední skupině hranic. Když je bod správy v sousedu i ve výchozích skupinách hranic lokality, je to 2.  

- **3**: zadaný bod správy je v místní nebo aktuální skupině hranic. Když je bod správy v aktuální skupině hranic a buď sousední uzel, nebo výchozí skupina hranic lokality, bude lokalita 3. Pokud nepovolíte nastavení preferované body správy v nastavení hierarchie, je vždy 3 bez ohledu na to, ve které skupině hranic se bod správy nachází.  

Klienti používají jako první místní body správy (místní 3), vzdálenou sekundu (u 2) a pak záložní (místní 1).

Když klient obdrží pět chyb během 10 minut a nedokáže komunikovat s bodem správy v aktuální skupině hranic, pokusí se kontaktovat bod správy v sousední síti nebo výchozí skupině hranic lokality. Pokud se bod správy v aktuální skupině hranic později znovu vrátí do režimu online, klient se vrátí do místního bodu správy v dalším cyklu aktualizace. Aktualizační cyklus je 24 hodin nebo když se služba agenta Configuration Manager restartuje.

## <a name="preferred-management-points"></a><a name="bkmk_preferred"></a>Preferované body správy

> [!Note]
> Chování nastavení této hierarchie u **klientů upřednostňuje používání bodů správy zadaných ve skupinách hranic, které**se změnily ve verzi 1802. Pokud povolíte toto nastavení, Configuration Manager použije funkci skupiny hranic pro přiřazený bod správy. Další informace najdete v tématu [body správy](#management-points).

Preferované body správy umožňují klientovi identifikovat bod správy, který je přidružený k aktuálnímu umístění v síti (hranice).  

- Klient se pokusí použít upřednostňovaný bod správy z přiřazené lokality před použitím některého z jeho přiřazené lokality, který není nakonfigurován jako upřednostňovaný.  

- Chcete-li použít tuto možnost, povolte **klientům, aby používaly body správy zadané ve skupinách hranic** v **Nastavení hierarchie**. Poté nakonfigurujte skupiny hranic v jednotlivých primárních lokalitách. Zahrňte body správy, které by měly být přidruženy k hranicím přidruženým této skupině hranic. Další informace najdete v tématu [Povolení použití upřednostňovaných bodů správy](boundary-group-procedures.md#bkmk_proc-prefer).  

- Když konfigurujete upřednostňované body správy a klient uspořádá svůj seznam bodů správy, umístí klient upřednostňované body správy na začátek seznamu. Tento seznam obsahuje všechny body správy z lokality přiřazené klientovi.  

> [!NOTE]  
> Klientský Roaming znamená, že změní jeho umístění v síti. Například při přenosu přenosného počítače do vzdáleného umístění pobočky. Když se klient roaminge, může použít bod správy z místní lokality a teprve potom se pokusí použít server z jeho přiřazené lokality. Tento seznam serverů z jeho přiřazené lokality zahrnuje preferované body správy. Další informace najdete v tématu [Vysvětlení způsobu, jakým klienti hledají služby a prostředky lokality](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="overlapping-boundaries"></a>Překrývající se hranice  

Configuration Manager podporuje konfigurace překrývajících se hranic pro umístění obsahu. Pokud síťové umístění klienta patří do více než jedné skupiny hranic:

- Když klient požádá o obsah, Configuration Manager odešle klientovi seznam všech distribučních bodů, které mají obsah.  

- Když klient požádá server o odeslání nebo přijetí informací o stavu migrace, Configuration Manager odešle klientovi seznam všech bodů migrace stavu přidružených ke skupině hranic, která obsahuje aktuální síťové umístění klienta.  

Díky tomuto chování může klient zvolit nejbližší server, ze kterého se má přenášet obsah nebo informace o migraci stavu.  

## <a name="example-of-using-boundary-groups"></a>Příklad použití skupin hranic

Následující příklad používá klienta k hledání obsahu z distribučního bodu. Tento příklad lze použít na jiné role systému lokality, které používají skupiny hranic.

Vytvořte tři skupiny hranic, které nesdílejí hranice nebo servery systému lokality:  

- BG_A skupiny s distribučními body DP_A1 a DP_A2  

- BG_B skupiny s distribučními body DP_B1 a DP_B2  

- BG_C skupiny s distribučními body DP_C1 a DP_C2  

Přidejte síťová umístění klientů jako hranice jenom BG_A hraniční skupině. Pak nakonfigurujte vztahy z této skupiny hranic na jiné dvě hraniční skupiny:  

- Konfigurace distribučních bodů pro první *sousední* skupinu (BG_B), která se má používat po 10 minutách Tato skupina obsahuje distribuční body DP_B1 a DP_B2. Obě jsou dobře připojené k umístění hranic první skupiny.  

- Nakonfigurujte druhou *sousední* skupinu (BG_C), která se má použít po 20 minutách. Tato skupina obsahuje distribuční body DP_C1 a DP_C2. Obě jsou v síti WAN z dalších dvou hraničních skupin.  

- Do výchozí skupiny hranic lokality přidejte taky jiný distribuční bod, který je na serveru lokality. Tento server má vaše nejmenší preferované zdrojové umístění obsahu, ale je centrálně umístěný ve všech skupinách hranic.

    Příklad skupin hranic a záložních časů:

    ![Příklad skupin hranic a záložních časů](media/BG_Fallback.png)  

S touto konfigurací:  

- Klient začne vyhledávat obsah z distribučních bodů v *aktuální* skupině hranic (BG_A). Vyhledá v každém distribučním bodě dvě minuty a potom přepne do dalšího distribučního bodu v hraniční skupině. Fond platných umístění pro zdroj obsahu pro klienta zahrnuje DP_A1 a DP_A2.  

- Pokud se klientovi po 10 minutách nenajde obsah ze své *aktuální* skupiny hranic, přidá distribuční body ze skupiny hranic BG_B do svého hledání. Pak pokračuje v hledání obsahu z distribučního bodu ve svém kombinovaném fondu serverů. Tento fond teď zahrnuje servery ze skupin hranic BG_A i BG_B. Klient pokračuje v kontaktování každého distribučního bodu po dobu dvou minut a pak přepne na další server v jeho fondu. Fond platných umístění zdroje obsahu pro klienta zahrnuje DP_A1, DP_A2, DP_B1 a DP_B2.  

- Pokud klient ještě po dalších 10 minutách (celkem 20 minut) nenalezl distribuční bod s obsahem, rozbalí jeho fond tak, aby zahrnoval dostupné servery z druhé *sousední* skupiny, skupiny hranic BG_C. Klient teď má šest distribučních bodů pro vyhledávání: DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 a DP_C2. Pokračuje v přechodu na nový distribuční bod každé dvě minuty, dokud nenalezne obsah.  

- Pokud klient nenalezl obsah po celkem 120 minut, bude se vrátit k zahrnutí *výchozí skupiny hranic lokality* jako součást jejich pokračování v hledání. Fond nyní zahrnuje všechny distribuční body ze tří nakonfigurovaných skupin hranic a konečný distribuční bod umístěný na serveru lokality. Klient pak pokračuje v hledání obsahu a mění distribuční body každé dvě minuty, dokud nenalezne obsah.  

Konfigurací různých sousedních skupin, které budou k dispozici v různých časech, můžete určit, kdy se konkrétní distribuční body přidávají jako umístění zdroje obsahu. Klient používá pro výchozí skupinu hranic lokality jako bezpečnostní síť pro obsah, který není dostupný z jiného umístění, záložní skupinu.

## <a name="changes-from-prior-versions"></a>Změny z předchozích verzí

Níže jsou uvedené klíčové změny skupin hranic a způsob, jakým klienti hledají obsah v Configuration Manager aktuální větvi. Mnohé z těchto změn a konceptů společně fungují.

### <a name="configurations-for-fast-or-slow-are-removed"></a>Konfigurace pro rychlé nebo pomalé služby se odeberou.

Už nemusíte konfigurovat jednotlivé distribuční body, aby byly rychlé nebo pomalé. Místo toho je pro každý systém lokality, který je přidružený ke skupině hranic, zacházeno stejným způsobem. Z důvodu této změny nepodporuje karta **odkazy** v rámci vlastností hraniční skupiny, aby konfigurace byla rychlá nebo pomalá.  

### <a name="new-default-boundary-group-at-each-site"></a>Nová výchozí skupina hranic v každé lokalitě

Každá primární lokalita má novou výchozí skupinu hranic s názvem **Default-site-hranice-Group &lt; SiteCode>**. Pokud klient nástroje není v síťovém umístění, které je přiřazeno ke skupině hranic, používá systémy lokality přidružené k výchozí skupině ze své přiřazené lokality. Naplánujte použití této skupiny hranic jako náhrady za koncept záložního umístění obsahu.

#### <a name="allow-fallback-source-locations-for-content-is-removed"></a>Odebrat **záložní umístění zdrojů pro obsah** je odebráno.

Nebudete už explicitně konfigurovat distribuční bod, který se má použít pro záložní použití. Možnosti konfigurace tohoto nastavení se odeberou z konzoly.

Kromě toho je výsledkem nastavení **umožnění klientům použít náhradní umístění zdroje obsahu** v typu nasazení pro aplikace. Toto nastavení pro typ nasazení teď umožňuje klientovi použít výchozí skupinu hranic lokality jako umístění zdroje obsahu.

#### <a name="boundary-groups-relationships"></a>Vztahy skupin hranic

Každou skupinu hranic můžete propojit s jednou nebo více dalšími hraničními skupinami. Tyto odkazy tvoří vztahy, které nakonfigurujete na kartě vlastností nové skupiny hranic s názvem **relace**:  

- Každá skupina hranic, se kterou je klient přímo přidružený, se nazývá **aktuální** skupina hranic.  

- Každá skupina hranic, kterou může klient použít kvůli přidružení mezi *aktuální* skupinou hranic daného klienta a jinou skupinou se nazývá **sousední** skupina hranic.  

- Na kartě **relace** přidejte skupiny hranic, které chcete použít jako *sousední* skupinu hranic. Také nakonfigurujte čas v minutách pro záložní použití. V případě, že se klientovi nepovede najít obsah z distribučního bodu v *aktuální* skupině, bude tato doba v případě, kdy klient začne hledat umístění obsahu ze *sousedních* hraničních skupin.  

    Když přidáte nebo změníte konfiguraci skupiny hranic, můžete z aktuální skupiny, kterou konfigurujete, zablokovat přechod na konkrétní skupinu hranic.  

Chcete-li použít novou konfiguraci, definujte explicitní přidružení (propojení) z jedné skupiny hranic na jinou. Nakonfigurujte všechny distribuční body v příslušné skupině se stejnou dobu v minutách. Když se klientovi nepovede najít zdroj obsahu ze své *aktuální* skupiny hranic, určí se čas, který nakonfigurujete, kdy začne hledat zdroje obsahu ze své sousední hraniční skupiny.

Kromě skupin hranic, které výslovně nakonfigurujete, má každá skupina hranic implicitní odkaz na výchozí skupinu hranic lokality. Tento odkaz bude aktivní po 120 minutách. Výchozí skupina hranic lokality se pak stal sousední skupinou hranic. Toto chování umožňuje klientům použít jako umístění zdroje obsahu distribuční body přidružené k této skupině hranic.

Toto chování nahrazuje, co bylo dříve označováno jako nouzové pro obsah. Potlačí toto výchozí chování 120 minut tím, že explicitně přidružíte výchozí skupinu hranic lokality k *aktuální* skupině. Nastavte určitou dobu v minutách nebo zablokujte zcela zálohu, aby nedocházelo k jejímu použití.

### <a name="clients-try-to-get-content-from-each-distribution-point-for-up-to-two-minutes"></a>Klienti se pokusí získat obsah z každého distribučního bodu po dobu až dvou minut.

Když klient vyhledá zdrojové umístění obsahu, pokusí se o přístup ke každému distribučnímu bodu po dobu dvou minut, než se pokusí o další distribuční bod. Toto chování se změní z předchozích verzí, kde se klienti pokusili připojit k distribučnímu bodu po dobu až dvou hodin.

- Klienti náhodně vyberou první distribuční bod z fondu dostupných serverů v rámci *aktuální* skupiny hranic (nebo skupin) daného klienta.  

- Pokud klient nenalezne obsah, bude po dvou minutách přepnut do nového distribučního bodu a pokusí se získat obsah z tohoto serveru. Tento proces opakuje každé dvě minuty, dokud klient nenajde obsah nebo nedosáhne posledního serveru v jeho fondu.  

- Pokud klient nemůže najít platné umístění zdroje obsahu z *aktuálního* fondu předtím, než dosáhne období pro přechod do *sousední* skupiny hranic, klient přidá distribuční body z této *sousední* skupiny na konec aktuálního seznamu. Pak vyhledá rozbalenou skupinu zdrojových umístění, která zahrnují distribuční body ze skupin hranic.  

    > [!TIP]  
    > Když vytvoříte explicitní propojení z aktuální skupiny hranic na výchozí skupinu hranic lokality a nadefinujete záložní čas, který je kratší než záložní čas pro odkaz na sousední skupinu hranic, začnou klienti prohledávat umístění zdroje z výchozí skupiny hranic lokality před zahrnutím sousední skupiny.  

- Když se klientovi nepovede získat obsah z posledního serveru ve fondu, zahájí proces znovu.  

## <a name="see-also"></a>Viz také

- [Postupy pro skupiny hranic](boundary-group-procedures.md)  

- [O hranicích](boundaries.md)  

- [Základní koncepty správy obsahu](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md)  
