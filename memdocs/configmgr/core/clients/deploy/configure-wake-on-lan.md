---
title: Konfigurace funkce Wake on LAN
titleSuffix: Configuration Manager
description: V Configuration Manager vyberte Wake On LAN nastavení.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dcf6005d0364106df8717a1151dbad617e455ff9
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127031"
---
# <a name="how-to-configure-wake-on-lan-in-configuration-manager"></a>Postup konfigurace funkce Wake on LAN v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Zadejte nastavení funkce Wake on LAN pro Configuration Manager, pokud chcete počítače uvést do stavu spánku.

## <a name="wake-on-lan-starting-in-version-1810"></a><a name="bkmk_wol-1810"></a>Funkce Wake on LAN počínaje verzí 1810
<!--3607710-->
Počínaje Configuration Manager 1810 existuje nový způsob, jak vybudit počítače v režimu spánku. Klienty můžete probouzet z konzoly Configuration Manager, i když klient nástroje není ve stejné podsíti jako server lokality. Pokud potřebujete provést údržbu nebo dotazování na zařízení, nebudete omezeni vzdálenými klienty, kteří jsou v režimu spánku. Webový server používá kanál oznámení klienta k identifikaci jiných klientů, kteří se nacházejí ve stejné vzdálené podsíti, a pak tyto klienty používá k odeslání požadavku Wake on LAN (Magic Packet). Použití kanálu pro oznamování klienta pomáhá předcházet klapkám MAC, což by mohlo způsobit vypnutí portu směrovačem. Novou verzi funkce Wake on LAN lze povolit ve stejnou dobu jako [starší verze](#bkmk_wol-previous).

### <a name="limitations"></a>Omezení
<!--7323898, 7363492-->
- Aspoň jeden klient v cílové podsíti musí být v běhu.
- Tato funkce nepodporuje tyto síťové technologie:
   - IPv6
   - 802.1 x – ověření sítě
    >[!NOTE]
    > ověřování sítě 802.1 x může pracovat s další konfigurací v závislosti na hardwaru a jeho konfiguraci.
- Počítače se probudí jenom v případě, že je upozorníte pomocí oznámení klienta **Wake-up** .
    - Pro probuzení, když dojde ke konečnému termínu, se použije starší verze funkce Wake on LAN.
    -  Pokud starší verze není povolená, neproběhne probuzení klienta pro nasazení vytvořená pomocí nastavení **použít funkci Wake-on-LAN k probuzení klientů pro požadovaná nasazení** nebo **odesílání paketů buzení ze spánku**.  

### <a name="security-role-permissions"></a>Oprávnění role zabezpečení

- **Oznamovat prostředek** pod kategorií kolekce

### <a name="configure-the-clients-to-use-wake-on-lan-starting-in-version-1810"></a>Konfigurace klientů pro použití funkce Wake on LAN počínaje verzí 1810

Dříve jste museli ručně povolit klienta funkce Wake on LAN ve vlastnostech síťového adaptéru. Configuration Manager 1810 obsahuje nové nastavení klienta s názvem **Povolení probuzení ze sítě**. Místo změny vlastností síťového adaptéru nakonfigurujte a nasaďte toto nastavení.

1. V části **Správa**klikněte na **nastavení klienta**.
1. Vyberte nastavení klienta, které chcete upravit, nebo vytvořte nové vlastní nastavení klienta pro nasazení. Další informace najdete v tématu [Konfigurace nastavení klienta](configure-client-settings.md).
1. V nastavení klienta **řízení spotřeby** vyberte **Povolit** pro nastavení **Povolit probuzení ze sítě** . Další informace o tomto nastavení najdete v tématu [informace o nastavení klienta](about-client-settings.md#power-management).

4. Počínaje Configuration Manager 1902 se nová verze funkce Wake on LAN dodrží vlastní port UDP, který zadáte pro [nastavení klienta](about-client-settings.md#power-management) **Wake on LAN číslo portu (UDP)** . Toto nastavení sdílí nová i starší verze funkce Wake on LAN.
 
<!--3605925-->

### <a name="wake-up-a-client-using-client-notification-starting-in-1810"></a>Probuzení klienta pomocí klientského oznámení od 1810
 
V kolekci můžete probudit jednoho klienta nebo všechny klienty v režimu spánku. U zařízení, která už v kolekci běží, se pro ně neprovádí žádná akce. Požadavek Wake on LAN bude odeslán pouze klientům, kteří jsou v režimu spánku. Další informace o tom, jak oznámit klientovi, aby se probudil, najdete v tématu [klientské oznámení](../manage/client-notification.md).

- **Postup probuzení jednoho klienta:** Klikněte pravým tlačítkem na klienta, přejděte na **klientské oznámení**a pak vyberte **probuzení**.

   ![Oznámení o probuzení klienta v konzole nástroje](media/wol-wake-up-client-notification.png)

- **Postup probuzení všech spících klientů v kolekci:** Klikněte pravým tlačítkem na kolekci zařízení, přejděte na **klientské oznámení**a pak vyberte **probuzení**.
   - Tuto akci nejde spustit na předdefinovaných kolekcích.
   - Pokud máte kombinaci klientů v režimu spánku a i v kolekci, odesílají se žádosti funkce Wake on LAN jenom klientům, kteří jsou v režimu spánku.
   - Počínaje Configuration Manager 2002 je tato akce k dispozici z konzoly připojené k lokalitě centrální správy, samostatné lokalitě nebo podřízené primární lokalitě.
   - Ve verzích 1910 a starších se tato akce aktivuje jenom v případě, že je konzola Configuration Manager připojená k samostatné nebo podřízené primární lokalitě. V případě připojení k lokalitě centrální správy není akce k dispozici.

### <a name="what-to-expect-when-only-the-new-version-of-wake-on-lan-is-enabled"></a>Co očekávat, když je povolená jenom nová verze funkce Wake on LAN

Pokud máte zapnutou pouze novou verzi funkce Wake on LAN, je povoleno pouze oznámení klienta **Wake up** . Klientům se nepošle oznámení, když se v nasazeních, jako je pořadí úkolů, distribuce softwaru nebo instalace aktualizací softwaru, dodrží konečný termín. Jakmile je spící počítač zase online, bude se projevit v konzole nástroje při kontrole s bodem správy.

Od verze Configuration Manager 1902 můžete zadat port Wake on LAN. Toto nastavení sdílí nová i starší verze funkce Wake on LAN.

### <a name="what-to-expect-when-both-versions-of-wake-on-lan-are-enabled"></a>Co očekávat, když jsou povolené obě verze funkce Wake on LAN

Pokud máte zapnuté obě verze funkce Wake on LAN, můžete použít oznámení klienta **Wake up** a probudit v konečném termínu. Oznámení klienta funguje trochu jinak než tradiční funkce Wake on LAN. Stručné vysvětlení, jak funguje klientské oznámení, najdete v části funkce [Wake on LAN počínaje verzí 1810](#bkmk_wol-1810) . Nové nastavení klienta **povolující probuzení ze sítě** změní vlastnosti síťové karty tak, aby povolovaly funkci Wake on LAN. Už je nemusíte ručně měnit pro nové počítače, které se přidají do vašeho prostředí. Všechny ostatní funkce funkce Wake on LAN se nezměnily.

Počínaje verzí 1902 se oznámení klienta **probuzení** dodrží stávající nastavení **Wake on LAN číslo portu (UDP)** .


## <a name="wake-on-lan-for-version-1806-and-earlier"></a><a name="bkmk_wol-previous"></a>Funkce Wake on LAN pro verzi 1806 a starší

Zadejte nastavení funkce Wake on LAN pro Configuration Manager, pokud chcete počítačům přenášet stav z režimu spánku, aby bylo možné nainstalovat požadovaný software, například aktualizace softwaru, aplikace, pořadí úloh a programy.

Funkci Wake on LAN můžete doplnit pomocí nastavení klienta proxy probuzení. Chcete-li však použít proxy probuzení, je nutné nejprve povolit funkci Wake on LAN pro lokalitu a zadat možnost **použít pouze pakety buzení ze spánku** a **jednosměrové vysílání** pro metodu přenosu funkce Wake on LAN. Toto řešení pro probuzení podporuje také připojení ad hoc, například připojení ke vzdálené ploše.

Pomocí prvního postupu nakonfigurujte primární lokalitu pro funkci Wake on LAN. Pak použijte druhý postup ke konfiguraci nastavení klienta proxy probuzení. Tento druhý postup nakonfiguruje výchozí nastavení klienta pro nastavení proxy probuzení, která se použijí pro všechny počítače v hierarchii. Pokud chcete toto nastavení použít jenom pro vybrané počítače, vytvořte vlastní nastavení zařízení a přiřaďte ho ke kolekci obsahující počítače, které chcete konfigurovat pro proxy probuzení. Další informace o tom, jak vytvořit vlastní nastavení klienta, najdete v tématu [Postup konfigurace nastavení klienta](../../../core/clients/deploy/configure-client-settings.md).

Počítač, který obdrží nastavení klienta proxy probuzení, bude asi po dobu 1-3 sekund pozastavit jeho síťové připojení. K tomu dochází, když klient musí resetovat síťovou kartu, aby na něm mohl zapnout ovladač proxy probuzení.

> [!WARNING]
> Abyste se vyhnuli neočekávanému výpadku síťových služeb, vyhodnoťte proxy probuzení v izolované a reprezentativní síťové infrastruktuře. Pak použijte vlastní nastavení klienta k rozšíření testu na vybranou skupinu počítačů v několika podsítích. Další informace o tom, jak funguje proxy probuzení, najdete v tématu [plánování probuzení klientů](../../../core/clients/deploy/plan/plan-wake-up-clients.md).


### <a name="to-configure-wake-on-lan-for-a-site-for-version-1806-and-earlier"></a>Konfigurace funkce Wake on LAN pro lokalitu pro verzi 1806 a starší

 Chcete-li používat funkci Wake on LAN, je nutné ji povolit pro každou lokalitu v hierarchii.

1. V konzole Configuration Manager klikněte na **správa > Konfigurace lokality > lokality**.
2. Klikněte na primární lokalitu, kterou chcete nakonfigurovat, a potom klikněte na **vlastnosti**.
3. Klikněte na kartu **Wake on LAN** a nakonfigurujte možnosti, které pro tento web požadujete. Chcete-li zajistit podporu proxy probuzení, vyberte možnost **používat pouze pakety buzení ze spánku** a **jednosměrové vysílání**. Další informace najdete v tématu [plánování probuzení klientů](../../../core/clients/deploy/plan/plan-wake-up-clients.md).
4. Klikněte na **OK** a opakujte postup pro všechny primární lokality v hierarchii.

![Povolit Wake On LAN ve vlastnostech webu](media/wol-site-properties.png)

### <a name="to-configure-wake-up-proxy-client-settings"></a>Konfigurace nastavení klienta proxy probuzení

1. V konzole Configuration Manager otevřete **> nastavení klienta**v části Správa.
2. Klikněte na **výchozí nastavení klienta**a pak klikněte na **vlastnosti**.
3. Vyberte **řízení spotřeby** a pak pro **Povolit proxy probuzení**zvolte **Ano** .
4. Zkontrolujte a v případě potřeby nakonfigurujte další nastavení proxy probuzení. Další informace o těchto nastaveních najdete v tématu [nastavení řízení spotřeby](../../../core/clients/deploy/about-client-settings.md#power-management).
5. Kliknutím na tlačítko **OK** zavřete dialogové okno a potom kliknutím na tlačítko **OK** zavřete dialogové okno výchozí nastavení klienta.

Pomocí následujících sestav Wake On LAN můžete monitorovat instalaci a konfiguraci proxy probuzení:

- Přehled stavu nasazení proxy probuzení
- Podrobnosti stavu nasazení proxy probuzení

> [!TIP]
> Chcete-li otestovat, zda proxy probuzení funguje, otestujte připojení k počítači v režimu spánku. Například se připojte ke sdílené složce v tomto počítači nebo se pokuste připojit k počítači pomocí vzdálené plochy. Používáte-li přímý přístup, ověřte, zda předpony IPv6 fungují, a to tak, že se pokusíte použít stejné testy pro spící počítač, který je aktuálně připojen k Internetu.
