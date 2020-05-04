---
title: Probuzení klientů
titleSuffix: Configuration Manager
description: Plánování probuzení klientů v Configuration Manager pomocí Wake On LAN (WOL).
ms.date: 04/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 52ee82b2-0b91-4829-89df-80a6abc0e63a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: feea1cdea52b76b900497e84eea210444535fcd8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713258"
---
# <a name="plan-how-to-wake-up-clients-in-configuration-manager"></a>Plánování probuzení klientů v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

 Configuration Manager podporuje tradiční pakety buzení ze spánku pro probuzení počítačů v režimu spánku, když chcete nainstalovat požadovaný software, například aktualizace softwaru a aplikace.

> [!NOTE]
> Tento článek popisuje, jak starší verze funkce Wake on LAN funguje. Tato funkce stále existuje ve verzi Configuration Manager 1810, která také obsahuje novější verzi funkce Wake on LAN. Obě verze funkce Wake on LAN lze v mnoha případech povolit současně. Další informace o tom, jak nová verze funkcí Wake on LAN začíná v 1810 a povoluje jednu nebo obě verze, najdete v tématu [jak nakonfigurovat funkci Wake on LAN](../configure-wake-on-lan.md).  

## <a name="how-to-wake-up-clients-in-configuration-manager"></a>Postup probuzení klientů v Configuration Manager

 Configuration Manager podporuje tradiční pakety buzení ze spánku pro probuzení počítačů v režimu spánku, když chcete nainstalovat požadovaný software, například aktualizace softwaru a aplikace.  

Tradiční metodu probuzení paketů můžete doplnit pomocí nastavení klienta proxy probuzení. Proxy probuzení používá protokol peer-to-peer a vybrané počítače ke kontrole, zda ostatní počítače v podsíti fungují a v případě potřeby je probudí. Pokud je lokalita nakonfigurována pro Wake On LAN a klienti jsou nakonfigurováni pro proxy probuzení, proces funguje následujícím způsobem:  

1. Počítače s nainstalovaným klientem Configuration Manager a nejsou v režimu spánku v podsíti kontrolují, jestli jsou ostatní počítače v podsíti aktivní. Tuto kontrolu provedou tím, že každých pět sekund posílá příkaz k příkazu příkazového testu TCP/IP.  

2. Pokud není žádná odpověď z jiných počítačů, předpokládá se, že jsou v režimu spánku. Počítače, které se používají, se stanou *počítačem správce* pro podsíť.  

    Vzhledem k tomu, že počítač nemusí reagovat z jiného důvodu než v režimu spánku (například je vypnutý, odebraný ze sítě nebo nastavení klienta probuzení proxy serveru se už nepoužívá), pošle se počítači paket buzení ze spánku každý den ve 2 hodiny. místní čas. U počítačů, které nereagují, se již nebude předpokládat, že jsou v režimu spánku a nebudou probuzený pomocí proxy probuzení.  

    Aby bylo možné podporovat proxy probuzení, musí být pro každou podsíť v režimu spánku aspoň tři počítače. Aby bylo možné tento požadavek dosáhnout, jsou tři počítače nedeterministické, aby byly *počítači strážce* pro danou podsíť. Tento stav znamená, že zůstanou v režimu bez ohledu na to, jestli jsou všechny nakonfigurované zásady napájení po určitou dobu nečinnosti v režimu spánku nebo hibernace. Počítače strážce dodržují příkazy pro vypnutí nebo restartování, například v důsledku úloh údržby. Pokud k této akci dojde, zbývající počítače strážce probudit jiný počítač v podsíti, aby tato podsíť dál měly tři počítače strážce.  

3. Počítače správce požádají síťový přepínač o přesměrování síťového provozu v spících počítačích do sebe samé.  

    Přesměrování se dosahuje počítačem správce, který vysílá rámec sítě Ethernet, který jako zdrojovou adresu používá adresu MAC pro spící počítač. Toto chování způsobí, že se síťový přepínač chová, jako by byl spící počítač přesunut na stejný port, na kterém je počítač se správcem zapnutý. Počítač správce taky odesílá pakety ARP pro spící počítače, aby se položka aktualizovala v mezipaměti ARP. Počítač správce také reaguje na požadavky ARP jménem spícího počítače a odpoví adresou MAC počítače v režimu spánku.  

   > [!WARNING]  
   >  Během tohoto procesu zůstane mapování IP-na MAC pro počítač v režimu spánku stejné. Proxy probuzení funguje tak, že informují síťový přepínač, že port, který byl zaregistrován jiným síťovým adaptérem, používá jiný síťový adaptér. Toto chování se ale označuje jako metoda MAC a není neobvyklé pro standardní síťové operace. Některé nástroje pro monitorování sítě hledají toto chování a mohou předpokládat, že je něco špatně. V důsledku toho můžou tyto nástroje pro monitorování generovat výstrahy nebo vypnout porty, když používáte proxy probuzení.  
   >   
   >  Nepoužívejte proxy probuzení, pokud vaše nástroje pro monitorování sítě a služby neumožňují použití klapky MAC.  

4. Když se u počítače v režimu spánku zobrazí nový požadavek na připojení TCP a požadavek je na port, na který spící počítač nacházel před přechodem do režimu spánku, počítač Správce odešle paket buzení ze spánku do spícího počítače a pak zastaví přesměrování provozu pro tento počítač.  

5. Spící počítač obdrží paket buzení ze spánku a probudí. Odesílající počítač automaticky znovu pokusy o připojení a tentokrát je v počítači funkční a může reagovat.  

   Proxy probuzení má následující předpoklady a omezení:  

> [!IMPORTANT]  
>  Pokud máte samostatný tým, který je zodpovědný za síťovou infrastrukturu a síťové služby, upozorněte a zahrňte tento tým během zkušebního a zkušebního období. Například v síti, která využívá řízení přístupu k síti 802.1 X, proxy probuzení nebude fungovat a může přerušit síťovou službu. Kromě toho může proxy probuzení způsobit, že některé nástroje pro monitorování sítě generují výstrahy, když nástroje zjišťují provoz pro probuzení dalších počítačů.  

-   Všechny operační systémy Windows, které jsou uvedené jako Podporovaní klienti v [podporovaných operačních systémech pro klienty a zařízení](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) , jsou podporované pro Wake on LAN.  

-   Hostované operační systémy, které běží na virtuálním počítači, se nepodporují.  

-   Klienti musí mít povolený proxy probuzení pomocí nastavení klienta. I když operace proxy probuzení není závislá na inventáři hardwaru, klienti nehlásí instalaci služby proxy probuzení, pokud nejsou povolené pro inventář hardwaru a neodesílají aspoň jeden inventář hardwaru.  

-   Síťové adaptéry (a případně i systém BIOS) musí být povolené a nakonfigurované pro pakety buzení ze spánku. Pokud síťový adaptér není nakonfigurován pro pakety buzení ze spánku nebo je toto nastavení zakázáno, Configuration Manager bude automaticky nakonfigurován a povolen pro počítač, když obdrží nastavení klienta pro povolení proxy probuzení.  

-   Pokud má počítač více než jeden síťový adaptér, nemůžete nakonfigurovat, který adaptér použít pro proxy probuzení; volba je nedeterministické. Zvolený adaptér se ale zaznamená do souboru SleepAgent_<domény\> @SYSTEM_0.log .  

-   Síť musí umožňovat požadavky na odezvu ICMP (alespoň v rámci podsítě). Interval pěti sekund, který se používá k odesílání příkazů příkazu příkazového testu ICMP, nelze nakonfigurovat.  

-   Komunikace je nešifrovaná a neověřená a protokol IPsec není podporován.  

-   Následující konfigurace sítě se nepodporují:  

    -   802.1 x s ověřováním portů  

    -   Bezdrátové sítě  

    -   Síťové přepínače, které vážou adresy MAC na konkrétní porty  

    -   Jenom sítě s protokolem IPv6  

    -   Doba trvání zapůjčení DHCP je kratší než 24 hodin.  

Chcete-li provést probuzení počítačů pro naplánovanou instalaci softwaru, je nutné nakonfigurovat každou primární lokalitu na použití paketů buzení ze spánku.  

 Chcete-li použít proxy probuzení, je nutné kromě konfigurace primární lokality nasadit také nastavení klienta proxy probuzení nástroje řízení spotřeby.  

Rozhodněte, jestli se mají používat pakety všesměrového vysílání směrované na podsíť, nebo pakety jednosměrového vysílání, a jaké číslo portu UDP se má použít. Ve výchozím nastavení jsou tradiční pakety buzení ze spánku přenášeny pomocí portu UDP 9, ale pokud chcete zvýšit zabezpečení, můžete vybrat alternativní port pro lokalitu, pokud je tento alternativní port podporován zabranými směrovači a branami firewall.  

## <a name="choose-between-unicast-and-subnet-directed-broadcast-for-wake-on-lan"></a>Volba mezi jednosměrovým vysíláním a všesměrovým vysíláním směrovaného na podsíť pro funkci Wake-on-LAN  
 Pokud se rozhodnete probuzení počítačů při posílání tradičních paketů buzení ze spánku, musíte se rozhodnout, jestli chcete přenést pakety jednosměrového vysílání nebo pakety všesměrového vysílání s přímým přístupem k podsíti. Pokud používáte proxy probuzení, je nutné použít pakety jednosměrového vysílání. Jinak použijte následující tabulku, která vám pomůže určit, kterou metodu přenosu zvolit.  

|Způsob přenosu|Výhoda|Nevýhoda|  
|-------------------------|---------------|------------------|  
|–|Bezpečnější řešení než všesměrové vysílání směrované na podsíť, protože paket se odesílá přímo do počítače místo do všech počítačů v podsíti.<br /><br /> Nemusí vyžadovat rekonfiguraci směrovačů (možná budete muset nakonfigurovat mezipaměť protokolu ARP).<br /><br /> Spotřebovává méně šířky pásma sítě než přenos všesměrového vysílání směrovaného na podsíť.<br /><br /> Podporováno s protokoly IPv4 a IPv6.|Pakety buzení ze spánku nenaleznou cílové počítače, u kterých se po posledním plánu inventarizace hardwaru změnila adresa podsítě.<br /><br /> Může být nutné nakonfigurovat přepínače pro přeposílání paketů UDP.<br /><br /> Některé síťové adaptéry nemusí reagovat na pakety buzení ze spánku ve všech stavech režimu spánku, když používají jako metodu přenosu jednosměrové vysílání.|  
|Všesměrové vysílání směrované na podsíť|Vyšší míra úspěšnosti než u jednosměrového vysílání, pokud máte počítače, které často mění svoji IP adresu ve stejné podsíti.<br /><br /> Nepožaduje se žádná změna konfigurace přepínače.<br /><br /> Vysoká míra kompatibility s adaptéry počítače pro všechny stavy režimu spánku, protože všesměrové vysílání směrované na podsíť bylo původní metodou přenosu pro odesílání paketů buzení ze spánku.|Méně bezpečné řešení než použití jednosměrového vysílání, protože Útočník by mohl odeslat nepřetržité streamy žádostí o odezvu ICMP z padělané zdrojové adresy na adresu směrovaného vysílání. To způsobí, že všichni hostitelé odpoví na tuto zdrojovou adresu. Pokud jsou směrovače nakonfigurované tak, aby umožňovaly všesměrové vysílání směrované na podsíť, doporučuje se z bezpečnostních důvodů další konfigurace:<br /><br /> – Nakonfigurujte směrovače tak, aby povolovaly jenom všesměrové vysílání směrované přes IP adresu ze serveru Configuration Manager, pomocí zadaného čísla portu UDP.<br />-Nakonfigurujte Configuration Manager pro použití zadaného jiného než výchozího čísla portu.<br /><br /> Může vyžadovat znovu konfiguraci všech používaných směrovačů, aby bylo možné povolit všesměrové vysílání směrované na podsíť.<br /><br /> Spotřebovává větší šířku pásma sítě, než je přenos jednosměrového vysílání.<br /><br /> Podporováno pouze s protokolem IPv4; Protokol IPv6 není podporován.|  

> [!WARNING]  
>  Všesměrové vysílání směrované na podsíť obsahuje bezpečnostní rizika: Útočník by mohl odeslat nepřetržité streamy žádostí o odezvu protokolu ICMP (Internet Control Message Protocol) z padělané zdrojové adresy na adresu směrovaného všesměrového vysílání, což způsobí, že všichni hostitelé odpoví na tuto zdrojovou adresu. Tento typ útoku na útok DOS se často označuje jako útok na Smurf a obvykle se snižuje tím, že nepovoluje všesměrové vysílání směrované na podsíť.
