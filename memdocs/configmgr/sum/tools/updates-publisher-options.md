---
title: Konfigurace možností
titleSuffix: Configuration Manager
description: Konfigurace možností pro použití System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 4e620080-5400-45bb-87c2-fbdbc8aeacac
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8b6578e32d5ae5a003c485960b556f3b87e8d557
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717724"
---
# <a name="configure-options-for-updates-publisher"></a>Konfigurovat možnosti pro aplikaci Updates Publisher

*Platí pro: System Center Updates Publisher*

Zkontrolujte a nakonfigurujte možnosti a související nastavení, která mají vliv na provoz nástroje Updates Publisher.

Chcete-li získat přístup k možnostem Vydavatel aktualizací v levém horním rohu konzoly, klikněte na kartu **vlastnosti** **aplikace Updates Publisher** a pak zvolte **Možnosti**.

![Možnosti](media/properties1.png)   


Možnosti jsou rozdělené do následujících možností:

-   Update Server
-   Server nástroje ConfigMgr
-   Nastavení proxy serveru
-   Důvěryhodní vydavatelé
-   Upřesnit
-   Aktualizace
-   protokolování

## <a name="update-server"></a>Update Server
Aby bylo možné [publikovat aktualizace](manage-updates-with-updates-publisher.md#publish-updates-and-bundles-from-the-updates-workspace), je nutné, aby aplikace Publisher nakonfigurovali pro práci se serverem aktualizací, jako je Windows Server Update Services (WSUS). To zahrnuje určení serveru, metod pro připojení k tomuto serveru, když je vzdálený z konzoly nástroje, a certifikát, který se má použít k digitálnímu podepisování aktualizací, které publikujete.

- **Nakonfigurujte server aktualizací**. Když nakonfigurujete server aktualizací, vyberte server WSUS na nejvyšší úrovni (aktualizace serveru) ve vaší hierarchii Configuration Manager, aby všechny podřízené lokality měly přístup k aktualizacím, které publikujete.

  Pokud je váš server aktualizace vzdálený od serveru pro aktualizace, zadejte plně kvalifikovaný název domény (FQDN) serveru a pokud se připojíte přes SSL. Při připojení pomocí protokolu SSL se výchozí port změní z 8530 na 8531. Zajistěte, aby nastavený port odpovídal tomu, co používá váš server aktualizací.

  > [!TIP]  
  > Pokud neprovedete konfiguraci serveru aktualizací, můžete i nadále používat nástroje Updates Publisher k vytváření aktualizací softwaru.

- **Nakonfigurujte podpisový certifikát**. Předtím, než budete moci nakonfigurovat podpisový certifikát, musíte nakonfigurovat a úspěšně připojit k serveru aktualizací.

  Nástroj Updates Publisher používá podpisový certifikát k podepsání aktualizací softwaru, které jsou publikovány na serveru aktualizací. Publikování se nepovede, pokud není k dispozici digitální certifikát v úložišti certifikátů serveru aktualizací nebo v počítači, který spouští nástroje Updates Publisher.

  Další informace o přidání certifikátu do úložiště certifikátů najdete v tématu [certifikáty a zabezpečení pro Updates Publisher](updates-publisher-security.md).

  Pokud se digitální certifikát pro server aktualizací nerozpozná automaticky, vyberte jednu z následujících možností:

  -   **Procházet**: Procházet je k dispozici pouze v případě, že je server aktualizací nainstalován na serveru, na kterém spouštíte konzolu nástroje. Po výběru certifikátu musíte zvolit **vytvořit** , chcete-li tento certifikát přidat do úložiště certifikátů služby WSUS na serveru aktualizací. Pro certifikáty, které vyberete touto metodou, je nutné zadat heslo k souboru **. pfx** .

  -   **Vytvořit:** Tuto možnost použijte k vytvoření nového certifikátu. Tím se také přidá certifikát do úložiště certifikátů služby WSUS na serveru aktualizací.

  **Pokud vytvoříte vlastní podpisový certifikát**, nakonfigurujte následující:

  -   Zaškrtněte možnost **Povolit export privátního klíče** .

  -   Nastavte **použití klíče** na digitální podpis.

  -   Nastavte **minimální velikost klíče** na hodnotu větší nebo rovnou 2048 bitu.

  Pomocí možnosti **Odebrat** odeberte certifikát z úložiště certifikátů služby WSUS. Tato možnost je k dispozici v případě, že je server aktualizací místní než konzola nástroje Updates Publisher, kterou použijete, nebo pokud jste použili **protokol SSL** pro připojení ke vzdálenému serveru aktualizací.

## <a name="configmgr-server"></a>Server nástroje ConfigMgr
Tyto možnosti použijte při použití Configuration Manager s nástrojem Updates Publisher.

-   **Zadejte Configuration Manager Server:** Po povolení podpory pro Configuration Manager zadejte umístění serveru lokality nejvyšší úrovně ze své Configuration Manager hierarchie. Pokud je tento server vzdálený z instalace nástroje Updates Publisher, zadejte plně kvalifikovaný název domény serveru lokality. Vyberte možnost **Test připojení** , abyste se ujistili, že se můžete připojit k serveru lokality.

-   **Konfigurovat prahové hodnoty:** Prahové hodnoty se používají, když publikujete aktualizace s automatickým typem publikace. Mezní hodnoty určují, kdy se publikuje celý obsah pro aktualizaci místo jenom metadat. Další informace o typech publikací najdete v tématu [přiřazení aktualizací k publikaci](manage-updates-with-updates-publisher.md#assign-updates-and-bundles-to-a-publication) .

    Můžete jeden nebo oba tyto prahové hodnoty:

    -   **Požadovaná prahová hodnota počtu klientů:** Definuje, kolik klientů musí vyžadovat aktualizaci, než může vydavatel aktualizací automaticky publikovat kompletní sadu obsahu pro danou aktualizaci. Dokud zadaný počet klientů nepožaduje aktualizaci, budou publikována pouze metadata aktualizace.

    -   **Prahová hodnota velikosti zdroje balíčku (MB):** Tím zabráníte automatickému publikování aktualizací, které překračují zadanou velikost. Pokud velikost aktualizací překročí tuto hodnotu, publikují se jenom metadata. Aktualizace, které jsou menší než zadaná velikost, můžou mít svůj úplný obsah publikovaný.

## <a name="proxy-settings"></a>Nastavení proxy serveru
Nástroj Updates Publisher používá nastavení proxy serveru při importu katalogů softwaru z Internetu nebo publikování aktualizací na internetu.

-   Zadejte plně kvalifikovaný název domény nebo IP adresu proxy server. Podporují se adresy IPv4 a IPv6.

-   Pokud proxy server ověřuje uživatele pro přístup k Internetu, musíte zadat název Windows. Univerzální hlavní název (UPN) není podporován.

## <a name="trusted-publishers"></a>Důvěryhodní vydavatelé
Při importu katalogu aktualizací se jako důvěryhodný vydavatel přidá zdroj tohoto katalogu (na základě jeho certifikátu). Podobně při publikování aktualizace se zdroj certifikátu aktualizací přidá jako důvěryhodný vydavatel.

Můžete zobrazit podrobnosti o certifikátu pro každého vydavatele a odebrat vydavatele ze seznamu důvěryhodných vydavatelů.

Obsah vydavatelů, kteří nejsou důvěryhodní, může potenciálně poškodit klientské počítače, když klient hledá aktualizace. Obsah byste měli přijmout jenom od vydavatelů, kterým důvěřujete.

## <a name="advanced"></a>Upřesnit
Mezi pokročilé možnosti patří následující:

-   **Umístění úložiště:** Zobrazení a úprava umístění databázového souboru **Scupdb. sdf**. Tento soubor je úložištěm pro nástroje Updates Publisher.

-   **Časové razítko:** Když je tato možnost povolená, přidá se k aktualizacím, které podepisují při podepsání, časové razítko. Po vypršení platnosti certifikátu je možné použít aktualizaci, která byla podepsána v době, kdy byl certifikát platný. Ve výchozím nastavení se aktualizace softwaru nedají nasadit po vypršení platnosti jejich podpisového certifikátu.

-   **Vyhledat aktualizace pro odebírané katalogy:** Pokaždé, když se spustí Vydavatel aktualizací, může automaticky vyhledat aktualizace katalogů, které jste si předplatili. Po nalezení aktualizace katalogu jsou podrobnosti v okně **Přehled** **pracovního prostoru aktualizace**k dispozici jako **nedávné výstrahy** .

-   **Odvolání certifikátu:** Tuto možnost vyberte, pokud chcete povolit kontroly odvolání certifikátů.

-   **Publikování v místním zdroji:** Služba Updates Publisher může použít místní kopii aktualizace, kterou publikujete před stažením této aktualizace z Internetu. Umístění musí být složka v počítači, na kterém je spuštěna aplikace Updates Publisher. Ve výchozím nastavení je toto umístění **Documents\LocalSourcePublishing.** Tento postup použijte, pokud jste dříve stáhli jednu nebo více aktualizací, nebo jste udělali změny v aktualizaci, kterou chcete nasadit.

-   **Průvodce vyčištěním aktualizací softwaru:** Spusťte Průvodce vyčištěním aktualizací. Průvodce vyprší aktualizace, které jsou na serveru aktualizací, ale ne v úložišti Publisher Updates. Další podrobnosti najdete v tématu [vypršení neodkazování aktualizací](#expire-unreferenced-software-updates) .

## <a name="updates"></a>Aktualizace
 Updates Publisher může automaticky kontrolovat nové aktualizace pokaždé, když se otevře. Můžete se také přihlásit k odběru buildů Preview aplikace Publisher.

Chcete-li ručně vyhledat aktualizace, v konzole aplikace Updates Publisher klikněte na tlačítko ![vlastnosti.](media/properties2.png)  
Chcete-li otevřít **Vlastnosti aplikace Publisher Updates**a pak zvolte možnost **Vyhledat aktualizace**.

Když Publisher Updates najde novou aktualizaci, zobrazí se okno **aktualizace k dispozici** a pak se můžete rozhodnout nainstalovat. Pokud se rozhodnete, že aktualizaci nenainstalujete, nabídne se při příštím otevření konzoly.

## <a name="logging"></a>protokolování
Aktualizace aplikace Publisher zaznamenává základní informace o nástroji Updates Publisher do **%windir%\Temp\UpdatesPublisher.log**.

K zobrazení protokolu použijte Poznámkový blok nebo **CMTrace** . CMTrace je nástroj souboru protokolu Configuration Manager a najdete ho ve složce **\SMSSetup\Tools** zdrojového média Configuration Manager.

Můžete změnit velikost protokolu a jeho úroveň podrobností.

Pokud povolíte protokolování databáze, budou zahrnuty informace o dotazech, které jsou spuštěny proti databázi nástroje Updates Publisher. Použití protokolování databáze může vést ke snížení výkonu počítače nástroje Updates Publisher.

Chcete-li zobrazit soubor protokolu, v konzole nástroje klikněte ![na](media/properties2.png) vlastnosti. tím otevřete **vlastnosti vydavatele aktualizace**a poté zvolte možnost **Zobrazit soubor protokolu**.

## <a name="expire-unreferenced-software-updates"></a>Vypršení neodkazování aktualizací softwaru
**Průvodce vyčištěním aktualizací softwaru** můžete použít k vypršení platnosti aktualizací, které jsou na serveru aktualizací, ale ne v úložišti vydavatelů aktualizací. Tím se upozorní Configuration Manager, že se tyto aktualizace z jakéhokoli budoucího nasazení odeberou.

Platnost aktualizace, kterou vyprší, nelze vrátit zpět. Tuto úlohu proveďte jenom v případě, že jste si jisti, že vaše organizace už nevyžaduje vybrané aktualizace softwaru.

### <a name="to-remove-expired-software-updates"></a>Odebrání aktualizací softwaru s vypršenou platností
1.  V konzole nástroje Updates Publisher kliknutím ![na](media/properties2.png) vlastnosti otevřete okno **aktualizace – vlastnosti vydavatele**a pak zvolte **Možnosti**.

2.  Zvolte možnost **Upřesnit**a potom v části **Průvodce čistým nastavením aktualizace softwaru** zvolte možnost **Spustit**.

3.  Vyberte aktualizace softwaru, jejichž platnost vypršela, a klikněte na tlačítko **Další**.

4.  Po kontrole výběrů vyberte možnost **Další** a přijměte výběr a vypršení platnosti těchto aktualizací.

5.  Po dokončení průvodce klikněte na tlačítko **Zavřít** a dokončete průvodce.
