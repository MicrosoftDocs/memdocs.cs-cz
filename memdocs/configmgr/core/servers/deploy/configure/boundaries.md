---
title: Definovat hranice
titleSuffix: Configuration Manager
description: Zjistěte, jak definovat síťová umístění v intranetu, která můžou obsahovat zařízení, která chcete spravovat.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 13312c20edbda290daaa0d51908adeb7ab4a6860
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700057"
---
# <a name="define-network-locations-as-boundaries-for-configuration-manager"></a>Definovat síťová umístění jako hranice pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Hranice Configuration Manager jsou umístění v síti obsahující zařízení, která chcete spravovat. Můžete vytvořit různé typy hranic, například lokalitu služby Active Directory nebo síťovou IP adresu. Když klient Configuration Manager identifikuje podobné síťové umístění, toto zařízení je součástí hranice.

Configuration Manager podporuje následující typy hranic:

- Podsíť protokolu IP
- Lokalita Active Directory
- Předpona IPv6
- Rozsah IP adres
- VPN (počínaje verzí 2006)

Můžete ručně vytvořit jednotlivé hranice nebo použít [zjišťování doménové struktury služby Active Directory](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest). Tato metoda zjišťování automaticky vyhledá a vytvoří hranice pro podsítě protokolu IP a lokality služby Active Directory. Když funkce zjišťování doménové struktury služby Active Directory identifikuje tuto nadsíť pro lokalitu služby Active Directory, Configuration Manager převede tuto nadsíť na hranici rozsahu IP adres.

Pokud zařízení není na hranici, kterou očekáváte, může to být způsobeno tím, že jste jeho umístění v síti nedefinovali jako hranici. Pokud je síťové umístění zařízení nejisté, potvrďte to pomocí následujících příkazů Windows na zařízení:

- IP adresa: `ipconfig`
- Lokalita služby Active Directory: `nltest /dsgetsite`
- S2S `ipconfig /all`

## <a name="boundary-types"></a>Typy hranic

### <a name="ip-subnet"></a>Podsíť protokolu IP

Typ hranice podsítě IP adres vyžaduje **ID podsítě**. Například, `169.254.0.0`. Pokud zadáte **síť** (výchozí bránu) a hodnoty **masky podsítě** , Configuration Manager automaticky vypočítá **ID podsítě**. Při uložení hranice Configuration Manager uloží pouze hodnotu ID podsítě.

> [!NOTE]
> Configuration Manager nepodporuje přímou položku tuto nadsíť jako hranici. Místo toho použijte jako typ hranice rozsah IP adres.

### <a name="active-directory-site"></a>Lokalita Active Directory

Pro typ hranice **lokalit služby Active Directory** zadáte název webu. Můžete zadat název nebo procházet místní doménovou strukturu serveru lokality.

Když pro hranici zadáte lokalitu služby Active Directory, bude tato hranice zahrnovat každou podsíť protokolu IP, která je členem dané lokality služby Active Directory. Pokud se konfigurace lokality služby Active Directory změní ve službě Active Directory, změní se také síťová umístění zahrnutá v této hranici.  

Pro zařízení s čistým Azure Active Directorym (Azure AD) nefungují hranice lokalit služby Active Directory, označované taky jako cloudová zařízení připojená k doméně. Pokud jsou místně přenášeny do místního prostředí a vytváříte pouze hranice typu lokality služby Active Directory, tato zařízení nebudou v hranici.

> [!TIP]
> Pomocí následujícího příkazu systému Windows zobrazte aktuální lokalitu služby Active Directory zařízení: `nltest /dsgetsite` .
>
> Chcete-li zjistit, zda je klient připojen k doméně, použijte následující příkaz systému Windows: `dsregcmd /status` . Další informace najdete v tématu [dsregcmd Command-Device State](/azure/active-directory/devices/troubleshoot-device-dsregcmd).

### <a name="ipv6-prefix"></a>Předpona IPv6

Pro typ hranice **předpony IPv6** zadáte **předponu**. Například, `2001:1111:2222:3333`.

### <a name="ip-address-range"></a>Rozsah IP adres

Jako typ hranice **rozsahu IP adres** zadejte **Počáteční IP adresu** a **koncovou IP adresu** rozsahu. Rozsah může zahrnovat část podsítě protokolu IP nebo více podsítí protokolu IP. K podpoře tuto nadsíť použijte typ hranice rozsahu IP adres.

Tento typ můžete také použít k definování hranice pro jednu IP adresu. Jako počáteční i koncovou IP adresu nastavte stejnou hodnotu. Tato konfigurace může být užitečná pro jedinečná zařízení nebo testovací prostředí.

### <a name="vpn"></a>Síť VPN

<!--7020519-->

Od verze 2006 můžete pro zjednodušení správy vzdálených klientů vytvořit hraniční typ pro sítě VPN. Když klient odešle požadavek na umístění, obsahuje další informace o jeho konfiguraci sítě. Na základě těchto informací server určí, jestli je klient na síti VPN. Pokud chcete Configuration Manager přidružit klienta k hranici, připojte zařízení k síti VPN.

Hranici sítě VPN můžete nakonfigurovat několika způsoby:

- **Automaticky zjišťovat síť VPN**: Configuration Manager DETEKUJE řešení VPN, které používá protokol PPTP (Point-to-Point Tunneling Protocol). Pokud síť VPN nerozpozná, použijte jednu z dalších možností. Hodnota hranice v seznamu konzoly bude `Auto:On` .

- **Název připojení**: zadejte název připojení VPN na zařízení. Jedná se o název síťového adaptéru ve Windows pro připojení VPN. Configuration Manager odpovídá prvním 250 znakům řetězce, ale nepodporuje zástupné znaky nebo částečné řetězce. Hodnota hranice v seznamu konzoly bude `Name:<name>` , kde `<name>` je název připojení, který zadáte.

  Například spustíte `ipconfig` příkaz na zařízení a jeden z oddílů začíná na: `PPP adapter ContosoVPN:` . `ContosoVPN`Jako **název připojení**použijte řetězec. V seznamu se zobrazí jako `Name:CONTOSOVPN` .

- **Popis připojení**: zadejte popis připojení VPN. Configuration Manager odpovídá prvním 243 znakům řetězce, ale nepodporuje zástupné znaky nebo částečné řetězce. Hodnota hranice v seznamu konzoly bude `Description:<description>` , kde `<description>` je popis připojení, který zadáte.

  Například spustíte `ipconfig /all` příkaz na zařízení a jedno z připojení obsahuje následující řádek: `Description . . . . . . . . . . . : ContosoMainVPN` . `ContosoMainVPN`Jako **Popis připojení**použijte řetězec. V seznamu se zobrazí jako `Description:CONTOSOMAINVPN` .

> [!IMPORTANT]
> Pokud chcete plně využít tuto funkci, po aktualizaci lokality aktualizujte také klienty na nejnovější verzi. Nové funkce se zobrazí v konzole Configuration Manager, když aktualizujete lokalitu a konzolu. Kompletní scénář není funkční, dokud nebude verze klienta zároveň nejnovější.
>
> Chcete-li použít tuto hranici sítě VPN během nasazování operačního systému, nezapomeňte také aktualizovat spouštěcí bitovou kopii tak, aby obsahovala nejnovější binární soubory klienta.

## <a name="create-a-boundary"></a>Vytvořit hranici

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace hierarchie**a vyberte uzel **hranice** .

1. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte **vytvořit hranici**.

1. Na kartě **Obecné** v okně **vytvořit hranici** zadejte následující informace:

    - **Popis**: Identifikujte hranici popisným názvem nebo odkazem.

        > [!NOTE]
        > Configuration Manager automaticky pojmenuje hranici na základě jejího typu a rozsahu. Nemůžete upravit název.

    - **Typ**: Vyberte typ hranice, která se má vytvořit. Pak zadejte další informace, které typ vyžaduje. Další informace naleznete v tématu [typy hranic](#boundary-types).

1. Přepněte na kartu **skupiny hranic** . Pokud již máte v lokalitě skupiny hranic, můžete tuto novou hranici ihned přidat do jedné nebo více skupin.

1. Výběrem **OK** uložte novou hranici.

## <a name="configure-a-boundary"></a>Konfigurace hranice

> [!TIP]
> Při vytváření hranice je Configuration Manager automaticky pojmenována na základě typu a rozsahu hranice. Tento název nemůžete změnit. Pro lepší identifikaci hranice v konzole Configuration Manager zadejte popis.

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace hierarchie**a vyberte uzel **hranice** .

1. Vyberte hranici, kterou chcete upravit. Na kartě **Domů** na pásu karet ve skupině **vlastnosti** vyberte možnost **vlastnosti**.

1. V okně **vlastnosti** pro hranici můžete na kartě **Obecné** nakonfigurovat následující nastavení:

    - Upravit **Popis**
    - Změnit **typ** hranice
    - Změňte rozsah ohraničení úpravou jeho síťových umístění. Například pro hranici lokality služby Active Directory lze zadat nový název lokality služby Active Directory.

1. Chcete-li zobrazit systémy lokalit, které jsou přidruženy k této hranici, přepněte na kartu **systémy lokality** . Tuto konfiguraci nemůžete změnit z vlastností hranice.

    > [!TIP]
    > Aby byl server uveden jako systém lokality pro hranici, přidružte jej jako server systému lokality pro alespoň jednu skupinu hranic, která zahrnuje tuto hranici. Tuto konfiguraci nastavte na kartě **odkazy** skupiny hranic. Další informace najdete v tématu [Konfigurace přiřazení lokality a výběr systémových serverů lokality](boundary-group-procedures.md#bkmk_references).

1. Pokud chcete pro tuto hranici změnit členství ve skupině hranic, vyberte kartu **skupiny hranic** :

    - Chcete-li přidat tuto hranici do jedné nebo více skupin hranic, vyberte možnost **Přidat**. Vyberte jednu nebo více skupin hranic a pak vyberte **OK**.

    - Pokud chcete tuto hranici ze skupiny hranic odebrat, vyberte skupinu hranic a pak vyberte **Odebrat**.

1. Výběrem **OK** zavřete vlastnosti hranice a uložte konfiguraci.

## <a name="next-steps"></a>Další kroky

Každá hranice je k dispozici pro každý web ve vaší hierarchii. Po vytvoření hranice přidejte hranici do jedné nebo více [skupin hranic](boundary-groups.md).