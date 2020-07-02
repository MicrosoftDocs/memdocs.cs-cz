---
title: Registrace zařízení v Desktop Analytics
titleSuffix: Configuration Manager
description: Naučte se registrovat zařízení v Desktop Analytics.
ms.date: 07/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 8f3a2cfd2cb18d6247c35ae46efab2ab9f89b254
ms.sourcegitcommit: 2c5fd7c8603b88b753765f3cc298d0a0bacaf521
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/01/2020
ms.locfileid: "85819997"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>Jak zaregistrovat zařízení v Desktop Analytics

Když [připojíte Configuration Manager](connect-configmgr.md) k Desktop Analytics, nakonfigurujete nastavení pro registraci zařízení na Desktop Analytics. Tato nastavení můžete kdykoli změnit. Také se ujistěte, že jsou zařízení aktuální.

## <a name="update-devices"></a>Aktualizace zařízení

Desktop Analytics používá dvě hlavní součásti systému Windows:

- **Součást kompatibility**: součást kompatibility (**posouzení**) spouští diagnostiku na zařízení s Windows k vyhodnocení stavu kompatibility s nejnovějšími verzemi Windows 10.

- **Prostředí připojené uživatele a služba telemetrie**: když jsou zapnutá diagnostická data Windows, služba připojení uživatele a prostředí telemetrie (**DiagTrack**) shromažďuje data o systému, aplikaci a ovladači. Microsoft analyzuje tato data a sdílí je s vámi přes Desktop Analytics.

Nainstalujte si nejnovější verzi těchto součástí, abyste získali nejlepší zkušenosti s funkcí Desktop Analytics.

V následující tabulce jsou uvedeny aktualizace pro jednotlivé komponenty v podporovaných verzích operačních systémů:

| Verze operačního systému | Ohodnocovatel | DiagTrack |
| --------------| ----------------------- | -------------------|
| Systém Windows 10 2004 | Zahrnutá <sup> [Poznámka 1](#bkmk_note1)</sup> | [Nejnovější kumulativní aktualizace](https://support.microsoft.com/help/4555932) |
| Systém Windows 10 1909 | Zahrnutá <sup> [Poznámka 1](#bkmk_note1)</sup> | [Nejnovější kumulativní aktualizace](https://support.microsoft.com/help/4529964) |
| Systém Windows 10 1903 | Zahrnutá <sup> [Poznámka 1](#bkmk_note1)</sup> | [Nejnovější kumulativní aktualizace](https://support.microsoft.com/help/4498140) |
| Systém Windows 10 1809 | Zahrnutá <sup> [Poznámka 1](#bkmk_note1)</sup> | [Nejnovější kumulativní aktualizace](https://support.microsoft.com/help/4464619) |
| Systém Windows 10 1803 | Zahrnutá <sup> [Poznámka 1](#bkmk_note1)</sup> | [Nejnovější kumulativní aktualizace](https://support.microsoft.com/help/4099479) |
| Systém Windows 10 1709 | Zahrnutá <sup> [Poznámka 1](#bkmk_note1)</sup> | [Nejnovější kumulativní aktualizace](https://support.microsoft.com/help/4043454) |
| Windows 8.1 | [KB 2976978](https://support.microsoft.com/help/2976978) – <sup> [Poznámka 2](#bkmk_note2)</sup> | [Poslední měsíční souhrn](https://support.microsoft.com/help/4009470) |
| Windows 7 SP1 | [KB 2952664](https://support.microsoft.com/help/2952664) – <sup> [Poznámka 3](#bkmk_note3)</sup> | [Poslední měsíční souhrn](https://support.microsoft.com/help/4009469) |

> [!TIP]
> K automatické instalaci těchto aktualizací použijte Configuration Manager. Další informace najdete v tématu [nasazení aktualizací softwaru](../sum/deploy-use/deploy-software-updates.md).
>
> Po prvním instalování aktualizací kompatibility restartujte zařízení.

### <a name="note-1-windows-10"></a><a name="bkmk_note1"></a>Poznámka 1: Windows 10

I když Windows 10 zahrnuje tyto komponenty standardně, zařízení s Windows 10 vyžadují nejnovější kumulativní aktualizaci, aby získala plnou funkčnost pro desktopovou analýzu, jako je vyhodnocení zařízení kvůli kompatibilitě s nejnovější verzí operačního systému.

### <a name="note-2-windows-81"></a><a name="bkmk_note2"></a>Poznámka 2: Windows 8.1

Společnost Microsoft pravidelně zvyšuje aktualizace této součásti, ale přidružené číslo znalostní báze se nezmění. Ujistěte se, že máte vždycky nejnovější verzi aktualizace.

Tato součást spustí diagnostiku v systémech Windows 8.1, které se podílejí na program Zlepšování softwaru a služeb na základě zkušeností uživatelů Windows. Tato diagnostika vám pomůže zjistit, jestli máte při upgradu na Windows 10 problémy s kompatibilitou.

### <a name="note-3-windows-7"></a><a name="bkmk_note3"></a>Poznámka 3: Windows 7

Pokud vaše organizace nepoužívá aktualizace "měsíčního" souhrnu kvality "na zařízeních s Windows 7, a týká se jenom jenom aktualizací jenom" jenom "zabezpečení", najdete v [seznamu aktualizací NAHRAZUJÍCÍ KB 2952664](https://www.catalog.update.microsoft.com/ScopedViewInline.aspx?updateid=ad3652cd-2689-4726-b3ef-b086ded23c7c)jenom některé aktualizace zabezpečení. Místo článku KB 2952664 můžete nainstalovat tyto novější aktualizace.

> [!NOTE]
> V případě Windows 8.1 Microsoft jako součást "měsíčního souhrnu kvality" aktualizuje jenom KB 2976978.

## <a name="device-enrollment"></a>Registrace zařízení

Služba Desktop Analytics nemá žádné agenty k instalaci. Registrace zařízení vyžaduje konfiguraci nastavení na zařízeních, která chcete monitorovat. Tato nastavení řídí, která instance aplikace Desktop Analytics má zařízení odesílat vaše data, a další možnosti konfigurace.

> [!Note]  
> Pokud jste dříve používali Windows Analytics, použijte stejný pracovní prostor pro Desktop Analytics. Je potřeba znovu zaregistrovat zařízení k Desktop Analytics, kterou jste předtím zaregistrovali ve Windows Analytics.
>
> Můžete mít jenom jeden pracovní prostor pro Desktop Analytics na tenanta Azure AD. Zařízení mohou odesílat diagnostická data pouze do jednoho pracovního prostoru.  

Configuration Manager poskytuje integrované prostředí pro správu a nasazení těchto nastavení klientů. Pro dosažení co nejlepších výsledků použijte Configuration Manager.

Když připojíte Configuration Manager k Desktop Analytics, nakonfigurujete nastavení pro registraci zařízení. Další informace najdete v tématu [Postup připojení Configuration Manager s desktopovou analýzou](connect-configmgr.md#bkmk_connect).

Chcete-li změnit tato nastavení, použijte následující postup:

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte uzel **služby Azure** . Vyberte připojení k Desktop Analytics a na pásu karet zvolte **vlastnosti** .

2. Na stránce **diagnostická data** proveďte v následujících nastaveních změny podle potřeby:  

    - **Komerční ID**: Tato hodnota by se měla automaticky naplnit ID vaší organizace. Pokud ne, ujistěte se, že je proxy server nakonfigurovaná tak, aby umožňovala všem požadovaným [koncovým bodům](enable-data-sharing.md#endpoints) znovu pokračovat. Komerční ID můžete také načíst ručně z [portálu Desktop Analytics](monitor-connection-health.md#bkmk_ViewCommercialID).

    - **Úroveň diagnostických dat Windows 10**: Další informace najdete v tématu [úrovně diagnostických dat](enable-data-sharing.md#diagnostic-data-levels).  

    - **Povolení názvu zařízení v diagnostických datech**: Další informace najdete v tématu [název zařízení](#device-name).  

    Když na této stránce provedete změny, zobrazí se na stránce **dostupné funkce** verze Preview funkce Desktop Analytics s vybraným nastavením diagnostických dat.  

3. Na stránce **připojení k Desktop Analytics** proveďte v následujících nastaveníech změny:

    - **Zobrazovaný název**: portál Analytics pro stolní počítače zobrazuje toto Configuration Manager připojení pomocí tohoto názvu.  

    - **Cílová kolekce**: Tato kolekce zahrnuje všechna zařízení, která Configuration Manager nakonfigurují pomocí nastavení komerčního ID a dat diagnostiky. Je to celá sada zařízení, která Configuration Manager se připojují ke službě Desktop Analytics.  

    - **Zařízení v cílové kolekci používají pro odchozí komunikaci uživatelem ověřený proxy server**: ve výchozím nastavení je tato hodnota **ne**. V případě potřeby v prostředí nastavte na **Ano**. Další informace najdete v tématu [ověřování proxy serveru](enable-data-sharing.md#proxy-server-authentication).

    - **Vyberte konkrétní kolekce, které se mají synchronizovat s desktopovou analýzou**: Pokud chcete zahrnout další kolekce z hierarchie **cílové kolekce** , vyberte **Přidat** . Tyto kolekce jsou k dispozici na portálu Desktop Analytics pro seskupení s plány nasazení. Nezapomeňte zahrnout pilotní a pilotní kolekce.  <!-- 4097528 -->

        > [!IMPORTANT]
        > Tyto kolekce se budou i nadále synchronizovat se změnami členství. Například plán nasazení používá kolekci s pravidlem členství v systému Windows 7. Když se tato zařízení upgradují na Windows 10 a Configuration Manager vyhodnotí členství v kolekci, odfiltrují se tato zařízení z plánu shromažďování a nasazení.

### <a name="windows-settings"></a>Nastavení Windows

Když Configuration Manager zaregistruje zařízení do Desktop Analytics, nastaví zásady Windows pro konfiguraci zařízení pro Desktop Analytics. Ve většině případů se tato nastavení konfigurují jenom pomocí Configuration Manager. Tato nastavení nepoužívejte také v objektech zásad skupiny domén.

Další informace najdete v tématu [nastavení zásad skupiny pro Desktop Analytics](group-policy-settings.md).

### <a name="device-name"></a>Název zařízení

Počínaje systémem Windows 10 verze 1803 se název zařízení už ve výchozím nastavení neshromažďuje. Shromažďování názvu zařízení s diagnostickými daty vyžaduje samostatné přihlášení. Bez názvu zařízení je obtížné určit, která zařízení vyžadují pozornost při vyhodnocování upgradu na novou verzi Windows.

Pokud název zařízení neodešlete, zobrazí se v nástroji Desktop Analytics jako neznámý:

![Seznam zařízení v Desktop Analytics se zobrazenými názvy "neznámé"](media/unknown-device-name.png)

K dispozici je možnost nastavení Configuration Manager pro Desktop Analytics pro konfiguraci této možnosti: **umožňuje v diagnostických datech použít název zařízení**. Toto nastavení Configuration Manager řídí [nastavení zásad systému Windows](group-policy-settings.md), **AllowDeviceNameInTelemetry**.

### <a name="conflict-resolution"></a>Řešení konfliktů

Obecně platí, že pomocí kolekce Configuration Manager můžete cílit na nastavení a registraci Desktop Analytics. Použijte přímé členství nebo dotazy pro zahrnutí nebo vyloučení zařízení z kolekce. Další informace najdete v tématu [vytváření kolekcí](../core/clients/manage/collections/create-collections.md).

Configuration Manager nakonfiguruje nastavení systému Windows pouze v případě, že hodnota ještě neexistuje. Pokud potřebujete nakonfigurovat různá nastavení pro jedinečnou skupinu zařízení, můžete použít [Zásady skupiny](group-policy-settings.md). Nastavení, která cílí na zásady skupiny, mají přednost před nastaveními Configuration Manager. Zařízení, na která cílí zásady skupiny, nemusí přesně odrážet stav na řídicím panelu [stavu připojení](monitor-connection-health.md) .

Při konfiguraci úrovně diagnostiky dat nastavíte horní hranici zařízení. Ve výchozím nastavení ve Windows 10 verze 1803 a novější se uživatelé můžou rozhodnout nastavit nižší úroveň. Toto chování můžete řídit pomocí nastavení zásad skupiny, **Konfigurovat nastavení výslovných přihlášení k telemetrie v uživatelském rozhraní**. Další informace najdete v tématu [nastavení zásad skupiny pro Desktop Analytics](group-policy-settings.md).

### <a name="proxy-settings"></a>Nastavení proxy serveru

Pokud vaše organizace používá proxy server ověřování pro přístup k Internetu, ujistěte se, že jste správně nakonfigurovali nebo zařízení. Další informace najdete v tématu [ověřování proxy serveru](enable-data-sharing.md#proxy-server-authentication).

## <a name="next-steps"></a>Další kroky

Přejděte k dalšímu článku a vytvořte plány nasazení v Desktop Analytics.
> [!div class="nextstepaction"]
> [Vytvoření plánů nasazení](create-deployment-plans.md)
