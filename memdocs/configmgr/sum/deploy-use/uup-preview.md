---
title: UUP ve verzi Preview
titleSuffix: Configuration Manager
description: Pokyny pro verzi Preview integrace UUP
ms.date: 11/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: f06955ac-70ed-424d-a3e7-6b80ff2e114f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3871b51c85d0474c4bea2da24fc5a2f31d02f59f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719733"
---
# <a name="uup-private-preview-instructions"></a>Pokyny pro UUP Private Preview

> [!Note]  
> Tyto informace se vztahují k funkci ve verzi Preview, která se podstatně změnila předtím, než se komerční verze uvolní. Microsoft neposkytuje žádné záruky, výslovné ani předpokládané, týkající se zde uváděných informací.  

## <a name="introduction"></a>Úvod

UUP (Unified Update Platform) je platforma pro balení a publikování, kterou příjemci a podniková zařízení používají pro příjem aktualizací z web Windows Update pro firmy. Program UUP Private Preview je určen pro zákazníky, kteří se dohodli, že pomůžou Microsoftu ověřit používání aktualizací UUP v Configuration Manager, aby mohli řešit problémy, které zákazníci hlásí s operačním systémem Windows ještě dnes. Tyto aktualizace nejsou aktuálně veřejně dostupné.

Další informace o UUP najdete v následujícím příspěvku na blogu pro Windows: [aktualizace naší UUP (Unified Update Platform)](https://blogs.windows.com/windowsexperience/2017/03/02/an-update-on-our-unified-update-platform-uup/).

## <a name="benefits"></a>Výhody

Funkce Windows 10 UUP a kumulativní aktualizace vám pomůžou vyřešit několik problémů, které zákazníci nahlásí s operačním systémem Windows ještě dnes.

### <a name="feature-updates"></a>Aktualizace funkcí

- V případě aktualizace funkcí UUP zachovává proces Windows Update na vyžádání (francouzské) a jazykové sady.

- Aktualizujte přímo na nejnovější úroveň dodržování předpisů zabezpečení. Nemusíte instalovat aktualizace zabezpečení hned po aktualizaci funkcí. Microsoft publikuje novou aktualizaci funkcí každý měsíc pomocí nejnovější kumulativní aktualizace zabezpečení. Nemusíte stahovat ani distribuovat většinu obsahu aktualizace funkcí každý měsíc. Stáhli jste jenom aktualizaci zabezpečení, která UUP sdílí s kumulativní aktualizací.

### <a name="cumulative-updates"></a>Kumulativní aktualizace

- Kumulativní aktualizace s UUP zahrnují aktualizace zásobníku cestou nadřazené (Servicing) s měsíčními kumulativními aktualizacemi zabezpečení. Toto chování řeší potíže s orchestrací těchto dvou aktualizací. Zajišťuje, aby byly k dispozici aktualizace zásobníku údržby pro instalaci kumulativních aktualizací. Tyto vztahy nemusíte spravovat ani orchestrovat.

- Kumulativní aktualizace s UUP umožňují distribuci FRANCOUZSKÝch a jazykových sad do offline režimu. Toto chování umožňuje uživatelům přidávat je na vyžádání. Uživatelé nemusí stahovat z Internetu a nemusíte si vystavovat, jak tento obsah připravit.

## <a name="set-up"></a>Nastavení

### <a name="1-send-your-wsus-id-to-microsoft"></a>1. odešlete ID služby WSUS společnosti Microsoft.

Pokud se chcete zapojit do UUP Private Preview, sdílejte své ID služby WSUS s vaším kontaktem UUP ve verzi Preview. Společnost Microsoft schválí vaše prostředí WSUS do programu UUP Preview. Bez tohoto ID nemůžete zobrazit žádné aktualizace UUP, dokud není verze Preview veřejná.

Chcete-li získat ID služby WSUS, spusťte následující skript prostředí PowerShell:

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId

# also check MUUrl
$config.MUUrl
```

Vlastnost **MUUrl** by měla být `https://sws.update.microsoft.com`. Pokud ho chcete změnit, přečtěte si článek řešení v následujícím článku podpory: [synchronizace WSUS se nezdařila s SoapException](https://support.microsoft.com/help/4482416/wsus-synchronization-fails-with-soapexception).

### <a name="2-update-configuration-manager"></a>2. aktualizace Configuration Manager

Proveďte následující změny Configuration Managerho webu pro podporu této UUP verze Preview:

#### <a name="diagnostics-and-usage-data-level"></a>Úroveň dat diagnostiky a využití

Zvažte zvýšení Configuration Manager úrovně diagnostiky a využití dat v této verzi Preview. **Celá** úroveň pomáhá Microsoftu lépe analyzovat a řešit problémy s touto novou funkcí. Další informace najdete v tématu [úrovně shromažďování diagnostických dat o využití pro verzi 1906](../../core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1906.md).

#### <a name="install-the-latest-update"></a>Nainstalovat nejnovější aktualizaci

1. Aktualizujte lokalitu pomocí jedné z následujících aktualizací:

    - Verze 1902 s [kumulativní aktualizací](https://support.microsoft.com/help/4500571)
    - [Verze 1906](../../core/servers/manage/checklist-for-installing-update-1906.md)

    Další informace najdete v tématu [instalace konzolových aktualizací](../../core/servers/manage/install-in-console-updates.md).

2. Aktualizujte klienty.  

    - Pro zjednodušení tohoto procesu zvažte použití automatického upgradu klienta. Další informace najdete v tématu [upgrade klientů](../../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).  

    - Aby nedocházelo ke *zbytečnému stahování* nevyužitého obsahu po 6 GB, aktualizujte všechny klienty, na které cílíte na aktualizace UUP.

### <a name="3-update-windows-clients-to-a-supported-version"></a>3. aktualizace klientů Windows na podporovanou verzi

Aby se aktualizace UUP úspěšně nainstalovaly, nainstalujte obě tyto aktualizace:

1. Konkrétní minimální kumulativní měsíční úroveň dodržování předpisů.

2. Konkrétní nekumulativní aktualizace bez zabezpečení z katalogu Microsoft Update. Pokud chcete importovat aktualizaci do Configuration Manager pro nasazení, přečtěte si téma [Import aktualizací z katalogu Microsoft Update](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog).

#### <a name="supported-versions-of-windows-10-and-required-updates"></a>Podporované verze Windows 10 a požadované aktualizace

| Verze Windows 10 | Minimální úroveň dodržování předpisů | Další aktualizace katalogu |
| ------------------ | ------------------------ | ------------------ |
| **Windows 10 verze 1903** | RTM | 7. listopadu 2019, [KB4529943](https://www.catalog.update.microsoft.com/search.aspx?q=4529943) |
| **Windows 10 verze 1809** | Srpen 2019, [KB4511553](https://support.microsoft.com/help/4511553/windows-10-update-kb4511553) | 7. listopadu 2019, [KB4514987](https://www.catalog.update.microsoft.com/search.aspx?q=4514987) |
| **Windows 10 verze 1803** | Duben 2019, [KB4493464](https://support.microsoft.com/help/4493464/windows-10-update-kb4493464) | 7. listopadu 2019, [KB4512745](https://www.catalog.update.microsoft.com/search.aspx?q=4512745) |
| **Windows 10 verze 1709** | Duben 2019, [KB4493441](https://support.microsoft.com/help/4493441/windows-10-update-kb4493441) | 7. listopadu 2019, [KB4512744](https://www.catalog.update.microsoft.com/search.aspx?q=4512744) |

> [!IMPORTANT]
> - Pokud k klientovi nainstalujete aktualizace z 12. listopadu 2019, než 7. listopadu 2019 další aktualizace katalogu, web Windows Update změny agenta potřebné k podpoře UUP budou přepsány. Chcete-li opravit klienty v tomto scénáři, nainstalujte po 12. listopadu 2019 aktualizace další aktualizace katalogu.
> - Pokud na klienta použijete aktualizaci funkcí, budete muset po dokončení upgradu znovu nainstalovat další aktualizaci katalogu.
> - Pro snazší testování aktualizací funkcí importujte aktualizace do Configuration Manager. Další informace najdete v tématu [Import aktualizací z katalogu Microsoft Update](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog). Po dokončení aktualizace funkcí se další aktualizace katalogu zobrazí jako **povinná**, což umožňuje automatické nasazení do verze OS na úrovni služby.

### <a name="4-allow-clients-to-download-delta-content-when-available"></a>4. umožňuje klientům stahovat v případě dostupnosti rozdílový obsah.

Aby se aktualizace UUP správně stahoval, povolte nastavení klienta, aby **klienti mohli povolit stahování rozdílových obsahu, pokud je dostupný**. Toto nastavení umožňuje Configuration Manager povolit, aby agent web Windows Update (WUA) určil potřebný obsah ke stažení do klientů. Toto chování je místo výchozí, kde klient Configuration Manager stáhne veškerý obsah přidružený k aktualizaci UUP. Pokud povolíte toto nastavení, WUA určí další obsah požadovaný z každé aktualizace UUP. Například pouze požadované francouzské a jazykové sady.

Pokud povolíte toto nastavení, nebude to mít vliv na stahování obsahu serveru z Internetu. Vztahuje se jenom na stahování klientů. Než nasadíte aktualizace UUP na klienty, použijte toto nastavení u klientů, kteří splňují podporované verze pro UUP. Aktualizace požadovaných klientů řeší problémy s kompatibilitou aktualizací UUP ve službě WSUS a Configuration Manager.

Další informace o tomto nastavení klienta najdete v tématu [informace o nastavení klienta – aktualizace softwaru](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) .

### <a name="5-review-your-software-update-infrastructure"></a>5. Prohlédněte si infrastrukturu aktualizace softwaru

Před synchronizací aktualizací UUP si Projděte pravidla automatického nasazení (ADR) a plány údržby. Pokud nechcete, aby se tyto aktualizace automaticky nasadily, upravte své pravidla automatického nasazení tak, aby se vyfiltroval. Další informace najdete v tématu [Jak najít synchronizované aktualizace UUP](#how-to-find-synced-uup-updates). Ve výchozím nastavení existující plány údržby nasazují pouze aktualizace bez UUP. Chcete-li toto chování změnit, můžete upravit plány údržby.

Zkontrolujte své zprávy o dodržování předpisů a podle potřeby je upravte. Pokud například měříte dodržování předpisů napříč všemi produkty, zobrazí se nyní kumulativní aktualizace UUP i bez UUP. Zařízení budou hlásit dodržování předpisů proti oběma typům aktualizací. Ujistěte se, že vaše zprávy o dodržování předpisů tuto změnu řeší.

## <a name="enable-uup-and-start-testing"></a>Povolit UUP a spustit testování

### <a name="select-products-and-classifications-to-sync"></a>Vyberte produkty a klasifikace, které se mají synchronizovat.

Až budete připraveni zahájit synchronizaci aktualizací UUP a společnost Microsoft schválila vaše ID služby WSUS, povolte nové produkty:

1. [Synchronizuje aktualizace softwaru](../get-started/synchronize-software-updates.md) , aby bylo možné naplnit nové produkty.  

2. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **lokality** .

3. Vyberte lokalitu nejvyšší úrovně, která je buď lokalita centrální správy (CAS) nebo samostatná primární lokalita.

4. Na pásu karet vyberte možnost **Konfigurovat součásti webu**a zvolte možnost **bod aktualizace softwaru**.

5. Přepněte na kartu **produkty** a vyberte jeden nebo více z následujících produktů: 

    - **Windows 10 UUP ve verzi Preview**
    - **Windows Server UUP ve verzi Preview**

6. Přepněte na kartu **klasifikace** a vyberte následující možnosti:  

    - **Aktualizace zabezpečení**: zobrazení kumulativních aktualizací UUP  
    - **Upgrady**: zobrazí se aktualizace funkcí UUP.  

7. Opětovně synchronizujte aktualizace softwaru, abyste viděli nové aktualizace UUP.

### <a name="how-to-find-synced-uup-updates"></a>Jak najít synchronizované aktualizace UUP

Po synchronizaci aktualizací UUP do svého prostředí je vyhledejte v konzole Configuration Manager k otestování. Existují dva způsoby, jak najít aktualizace verze Preview:

- Vzhledem k tomu, že jsou tyto aktualizace ve verzi Preview v samostatném produktu, pomocí filtru produktu tyto aktualizace Najděte. Pomocí filtru produktů v plánu údržby můžete nasadit aktualizace funkcí UUP nebo non-UUP.  

- Ve **všech aktualizacích softwaru** a **všech uzlech aktualizace Windows 10** **knihovny softwaru**je k dispozici nová volitelná **značka**sloupce. Tato vlastnost je také k dispozici jako filtr v pravidla automatického nasazení. V případě aktualizací UUP vyhledejte v tomto poli `UUP`pro. Pro aktualizace bez UUP je tato prázdná.  

### <a name="updates-available-during-preview"></a>Aktualizace dostupné během verze Preview

Další informace o všech aktualizacích Windows 10 vydaných Microsoftem najdete v tématu [informace o verzi Windows 10](https://docs.microsoft.com/windows/release-information/).

#### <a name="cumulative-updates-to-test"></a>Kumulativní aktualizace k testování

I když vidíte, že jsou k dispozici různé aktualizace s UUP, začněte s aktualizací **září 2019** (2019-09) nebo novější verzí. Příklad:

- 2019-09 kumulativní aktualizace pro Windows 10 verze 1809 pro systémy založené na platformě x64 (KB4512578)
- 2019-09 kumulativní aktualizace pro Windows 10 verze 1803 pro systémy založené na platformě x64 (KB4516058)
- 2019-09 kumulativní aktualizace pro Windows 10 verze 1709 pro systémy založené na platformě x64 (KB4516066)

#### <a name="feature-updates-to-test"></a>Aktualizace funkcí k testování

I když se může zobrazit několik dostupných aktualizací UUP, začněte s aktualizací **září 2019** (2019-09B) nebo novější verzí. Příklad:

- Aktualizace funkcí na Windows 10 verze 1809 x64 2019-09B
- Aktualizace funkcí na Windows 10 verze 1803 x64 2019-09B

## <a name="scenarios-to-test"></a>Scénáře k otestování

### <a name="test-feature-updates"></a>Testování aktualizací funkcí

- Aktualizovat přímo na zvolenou úroveň dodržování předpisů zabezpečení  

- Před aktualizací nainstalujte FODs a jazykové sady. Ujistěte se, že aktualizace zachovává tyto součásti.  

### <a name="test-cumulative-updates"></a>Test kumulativních aktualizací

Během období Preview udržují klienti kompatibilní s aktualizací typu UUP pro více po sobě jdoucích aktualizací. Tento test vám pomůže pochopit průběžné chování.

### <a name="test-content"></a>Test obsahu

První aktualizace pro každou hlavní verzi (1809, 1803, 1709), architektura a jazykové kombinace se jeví jako velká. Tato velikost je v počtu souborů i místo na disku, a to v porovnání s tím, co jste předtím viděli s aktualizacemi bez UUP. Tento dodatečný obsah je primárně určen pro všechny francouzské a jazykové sady pro kumulativní aktualizace. Pro aktualizace funkcí je pro tuto první aktualizaci k dispozici další velký obsah.

V budoucích kumulativních aktualizacích a aktualizacích funkcí je množství nového obsahu, které lokalita stahuje a distribuuje, mnohem menší. UUP inteligentně sdílí všechny francouzské a jazykové sady mezi aktualizacemi. Tento sdílený obsah není nutné znovu stahovat ani distribuovat. Ve verzi Preview se v systému Windows 10 verze 1709 a 1803 tento měsíční soubor ke stažení shoduje se stejnou velikostí kumulativních aktualizací ve scénářích, které nejsou UUP. Ve Windows 10 verze 1809 a novějších se přírůstkové stahování kumulativní aktualizace značně zmenší každý měsíc.

Když se podíváte na celkový obsah, který se stáhl a distribuuje po dobu 12 měsíců pro *neexpresní*verzi, Windows 10 verze 1803 bez UUP by měla být přibližně stejná jako verze 1809 s UUP. Celkový obsah stažený a distribuovaný v celém životnosti vydaných verzí je menší ve verzi 1809 s UUP.

### <a name="supported-content-channels"></a>Podporované kanály obsahu

Pro verzi Preview otestujte typické scénáře reálného světa. UUP podporuje všechny kanály obsahu, včetně:

- Optimalizace doručování systému Windows (DO)
  - Pokud používáte, ujistěte se, že je správně nakonfigurované. Další informace najdete v tématu [optimalizace doručování aktualizací Windows 10](optimize-windows-10-update-delivery.md).
- Configuration Manager sdílené mezipaměti
- Služba BranchCache systému Windows
- Použijte možnost **bez balíčku pro nasazení** a klienti stahují přímo z Microsoft Update. Tuto možnost použijte s optimalizací doručení.
- Alternativní poskytovatelé obsahu třetích stran

Další informace o kanálech obsahu najdete v tématu [optimalizace doručování aktualizací Windows 10](optimize-windows-10-update-delivery.md).

<!-- TODO: Addlink to WSUS Perf documentation-->
