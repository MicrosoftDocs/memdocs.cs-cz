---
title: Nejčastější dotazy k Desktop Analytics
titleSuffix: Configuration Manager
description: Nejčastější dotazy k Desktop Analytics
ms.date: 02/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: b24369f2c2f21208f188cf5c0c2ef3a28db83c04
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700816"
---
# <a name="desktop-analytics-faq"></a>Časté otázky k Desktop Analytics

## <a name="prerequisites"></a>Předpoklady

### <a name="can-i-use-cloud-enabled-analytics-with-intune-managed-devices"></a><a name="bkmk_intune"></a> Můžu na zařízeních spravovaných přes Intune použít cloudové analýzy?

Ne dnes, ale podívejte se na oznámení od Microsoft Ignite 2019 na stránce [Správa zařízení řízené přehledy](https://myignite.techcommunity.microsoft.com/sessions/81690?source=sessions). Toto plánované řešení je následníkem Stav zařízení a Upgrade Readiness.

Velká většina zákazníků, kteří můžou využít pracovní postup Desktop Analytics, používá Configuration Manager k nasazení systému Windows. Víme, že zákazníci Intune rádiují další poznatky z analytických dat a pracujeme na způsobech, jak s nimi sdílet přehledy.

### <a name="its-been-over-72-hours-and-the-portal-is-still-processing-data-what-next"></a>Je víc než 72 hodin a portál stále zpracovává data, co dál?

Při nastavování Desktop Analytics se v sestavách Configuration Manager a portálu pro Desktop Analytics nemusí okamžitě zobrazovat úplná data. Zpracování dat službou může trvat 2-3 dní. Pokud je více než 72 hodin a portál stále zpracovává data, postupujte podle následujících kroků:

- Pokud chcete ověřit, že jsou aktivní zařízení správně nakonfigurovaná, použijte [řídicí panel stavu připojení](monitor-connection-health.md). Tento řídicí panel se v reálném čase neaktualizuje.
- Zajistěte, aby zařízení odesílala diagnostická data do služby Desktop Analytics. Další informace najdete v tématu [Povolení sdílení dat](enable-data-sharing.md).
- Zřizování [aplikací Azure AD](troubleshooting.md#bkmk_AzureADApps) ve službě Azure AD.
- Podívejte se na zařízení, která máte v posledních sedmi dnech přidružená k vaší organizaci. Na [portálu Desktop Analytics](https://aka.ms/desktopanalytics)otevřete podokno **připojené služby** . Vyberte možnost **Registrovat zařízení**a **Zobrazit poslední data.**

  > [!IMPORTANT]
  > Možnost Analytics pro stolní počítače, která **zobrazuje poslední data** , je zastaralá. Tato akce bude odebrána v budoucí verzi služby Desktop Analytics. Další informace najdete v tématu [zastaralé funkce](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!--7080949-->  

Pokud jsou zařízení správně nakonfigurovaná a stále nevidíte data v pracovním prostoru, obraťte se na [podporu Microsoftu](https://support.microsoft.com/hub/4343728/support-for-business).

## <a name="connect-configuration-manager"></a>Připojení správce konfigurací

### <a name="can-i-change-the-target-or-additional-collections"></a>Můžu změnit cíl nebo další kolekce?

Ano, použijte následující postup:

- V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **služby Azure** . Otevřete vlastnosti položky přidružené k vaší službě Desktop Analytics.

- Na kartě **připojení pro Desktop Analytics** změňte **cílovou kolekci** nebo spravujte další kolekce.

<!-- 7130169 -->
> [!Note]
> Do seznamu dalších kolekcí nezahrnujte více než 20 kolekcí. Buďte opatrní na celkovém počtu zařízení v každé kolekci. Vždy zahrňte [globální pilotní zahrnutí a vyloučení kolekcí](deploy-pilot.md#bkmk_GlobalPilot).  

> [!IMPORTANT]  
> Configuration Manager používá zásadu nastavení ke konfiguraci zařízení v cílové kolekci. Tato zásada zahrnuje nastavení diagnostických dat, která umožňují zařízením odesílat data společnosti Microsoft. Změna cílové kolekce nevrátí zpět zásady nastavení na zařízeních, která už nejsou v cílové kolekci. Pokud nechcete, aby zařízení pokračovala v odesílání diagnostických dat, [překonfigurujte zařízení](account-close.md#reconfigure-clients).

## <a name="windows-upgrade"></a>Upgrade Windows

### <a name="can-i-upgrade-windows-and-change-architecture"></a>Můžu upgradovat Windows a změnit architekturu?

Desktop Analytics je navržený tak, aby nejlépe podporoval místní upgrady. Místní upgrady nepodporují migrace z 32-bitů na 64 bitovou architekturu. Pokud potřebujete migrovat počítače v tomto scénáři, použijte scénář aktualizace. Přehledy Desktop Analytics jsou v tomto scénáři stále cenné, ale můžete ignorovat doprovodné materiály týkající se upgradu.

Další informace najdete v tématu [Aktualizace existujícího počítače s novou verzí Windows](../osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md).

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>Můžu při upgradu systému Windows změnit stav systému BIOS na rozhraní UEFI?

Ano. Další informace najdete v tématu [převedení ze systému BIOS na rozhraní UEFI během místního upgradu](../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>Můžu použít desktopovou analýzu s Windows 10 LTSC?

Desktop Analytics nepodporuje zařízení LTSC (Long-Term Servicing Channel) Windows 10. Další informace najdete v tématu [Přehled služby Windows as](/windows/deployment/update/waas-overview#long-term-servicing-channel).

### <a name="can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal"></a>Můžu zkrátit dobu potřebnou k aktualizaci dat na portálu Desktop Analytics?

Na portálu pro Desktop Analytics existují dva typy dat: data správců a diagnostická data. Pokud chcete aktualizovat data správce na vyžádání, otevřete informační rámeček měna dat a vyberte **použít změny**. Tato akce okamžitě aktivuje jednorázovou aktualizaci všech nedokončených změn správců ve vašich pracovních prostorech. Změny se šíří a jsou všeobecně dostupné během 15-60 minut. Časování závisí na velikosti vašeho pracovního prostoru a rozsahu nedokončených změn. Můžete požádat o aktualizaci dat na vyžádání až šestkrát během 24 hodin.

Všechna data se aktualizují automaticky jednou denně, a to i v případě, že nepožadujete aktualizaci dat na vyžádání. Neexistuje žádný způsob, jak aktivovat aktualizace diagnostických dat na vyžádání. Další informace o různých typech dat v Desktop Analytics najdete v tématu [latence dat](troubleshooting.md#data-latency).

## <a name="privacy"></a>Ochrana osobních údajů

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>Dá se analýza na ploše použít bez přímého připojení klienta ke službě Microsoft Správa dat Service?

Ne, celá služba využívá diagnostická data Windows, což vyžaduje, aby zařízení měla toto přímé připojení.

### <a name="can-i-choose-the-data-center-location"></a>Můžu zvolit umístění datového centra?

Pro Azure Log Analytics: Ano, při nastavování Desktop Analytics a vytvoření pracovního prostoru Log Analytics.

Pro Azure Storage Správa dat služby a analýzy společnosti Microsoft: Ne, tyto dvě služby jsou hostovány v USA.

### <a name="where-is-my-organizations-data-stored"></a>Kde jsou uložená data organizace?

Diagnostická data Windows z vašich počítačů se šifrují, odesílají a zpracovávají v zabezpečených datových centrech spravovaných Microsoftem, která se nacházejí v USA. Microsoft poskytuje analýzu dat souvisejících s desktopovou analýzou prostřednictvím řešení Desktop Analytics v Azure Portal. Plocha Analytics je podporovaná ve většině oblastí, kde [je Log Analytics k dispozici](https://azure.microsoft.com/global-infrastructure/services/?products=monitor&regions=all). Pokud vyberete mezinárodní oblast Azure, vaše diagnostická data se pořád posílají a zpracovávají v zabezpečených datových centrech Microsoftu v USA.

## <a name="existing-windows-analytics-customers"></a>Stávající zákazníci Windows Analytics

> [!Important]  
> Služba Windows Analytics se vyřadí od 31. ledna 2020.
>
> Další informace najdete v [článku KB 4521815: vyřazení služby Windows Analytics na 31. ledna 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

### <a name="can-i-use-update-compliance-together-with-desktop-analytics"></a>Můžu použít Update Compliance společně s desktopovou analýzou?

Ano. Pokud v Azure Portal dnes používáte [Update Compliance](/windows/deployment/update/update-compliance-get-started) , můžete to provést i po uplynutí ledna 2020.

Další informace najdete v [článku KB 4521815: vyřazení služby Windows Analytics na 31. ledna 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

### <a name="are-there-any-windows-analytics-features-that-arent-available-in-desktop-analytics"></a>Existují nějaké funkce Windows Analytics, které nejsou k dispozici v Desktop Analytics?

<!-- 3616924 -->
Ano, následující funkce Windows Analytics byly buď vyřazené, nebo ještě nejsou k dispozici v Desktop Analytics:

#### <a name="general"></a>Obecné

- Podpora scénářů, které nevyžadují Configuration Manager. Například podpora služby [Intune](#bkmk_intune).
- Požadavek na licencování jakékoli platné licence Windows vs E3, E5
- Podpora více pracovních prostorů na tenanta Azure AD
- Možnost spouštět vlastní dotazy a exportovat nezpracovaná data řešení
- Dokumentace k datovému modelu pro vlastní sestavy

#### <a name="upgrade-readiness"></a>Upgrade Readiness

- Data zjišťování webu aplikace Internet Explorer
- Přehled doplňku Microsoft 365 Apps (teď [dostupné v Configuration Manager](#bkmk_office))
- Přehledy centra Feedback

#### <a name="update-compliance"></a>Update Compliance

- Podpora web Windows Update pro firmy
- Přehledy pro optimalizaci doručení
- Podpora kanálu pro dlouhodobé obsluhy Windows 10 (LTSC)
- Sestavy Windows Insider
- Stav programu Windows Defender

> [!Note]
> Všechny existující funkce Update Compliance, včetně těch, které nejsou k dispozici v Desktop Analytics, zůstávají k dispozici v řešení [Update Compliance](/windows/deployment/update/update-compliance-get-started) v Azure Portal.

#### <a name="device-health"></a>Stav zařízení

- Stav ovladače
- Stav aplikace (mimo plán nasazení)
- Často chybná zařízení nebo chyby způsobené ovladačem
- Přihlašovací stav pro Windows
- Windows Information Protection
- Podpora pro Windows Server

## <a name="other"></a>Ostatní

### <a name="can-i-use-desktop-analytics-for-my-microsoft-365-apps-upgrades"></a><a name="bkmk_office"></a> Můžu pro upgrady Microsoft 365 aplikací použít desktopovou analýzu?

Ne, analýza stolních počítačů se zaměřuje na Windows. Vývoj desktopových analýz od Microsoftu v těsné spolupráci s mnoha zákazníky. Názory na zákazníky jsou informace o tom, jak Analytics Desktop vylepšuje schopnost spolehlivě spravovat nasazení Windows. Také nám sdělí, že chtějí [Microsoft 365 aplikace](../sum/deploy-use/office-365-dashboard.md#bkmk_o365_readiness) lépe integrovat s nástroji pro správu Microsoft 365ch aplikací v Configuration Manager a Intune. Společnost Microsoft bude v těchto oblastech nadále investovat a přitom se zaměřuje na scénáře ve Windows v oblasti Desktop Analytics.

### <a name="how-can-i-provide-feedback-about-desktop-analytics"></a>Jak můžu sdělit svůj názor na Desktop Analytics?

Pokud chcete sdílet svůj názor na Desktop Analytics, vyberte ikonu **odeslat smajlíka** v horní části portálu. Přidejte snímek obrazovky s vaším odesláním a pomozte Microsoftu lépe pochopit vaše názory. Můžete také odesílat návrhy produktů a hlasovat o dalších nápadech na [UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas?category_id=366805).

> [!Note]
> Soukromé informace nikdy nesdílejte prostřednictvím Poslat smajlíka nebo UserVoice. Tyto soukromé informace zahrnují ID tenanta nebo komerční ID. Microsoft neposkytuje podporu prostřednictvím kanálu odeslat smajlíka nebo UserVoice. Pokud chcete získat nápovědu k pracovnímu prostoru Desktop Analytics, vyberte v navigační nabídce odkaz **Nápověda a podpora a** otevřete lístek podpory.