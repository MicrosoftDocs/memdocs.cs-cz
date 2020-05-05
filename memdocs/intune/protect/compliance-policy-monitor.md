---
title: Monitorování zásad dodržování předpisů u zařízení v Microsoft Intune – Azure | Microsoft Docs
description: Na řídicím panelu pro dodržování předpisů zařízením můžete monitorovat celkový stav dodržování předpisů zařízením, zobrazit sestavy a dodržování předpisů zařízením podle jednotlivých zásad a nastavení.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/18/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a703914b589430f3e2347c0ea08843193595dc0e
ms.sourcegitcommit: 56bb5419c41c2e150ffed0564350123135ea4592
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/02/2020
ms.locfileid: "82729330"
---
# <a name="monitor-intune-device-compliance-policies"></a>Monitorování zásad dodržování předpisů zařízením v Intune

Sestavy dodržování předpisů slouží ke kontrole dodržování předpisů zařízeními a řešení problémů souvisejících s dodržováním předpisů ve vaší organizaci. Pomocí těchto sestav můžete zobrazit následující informace:

- Celkový stav dodržování předpisů zařízeními
- Stav dodržování předpisů pro individuální nastavení
- Stav dodržování předpisů pro individuální zásadu
- Podrobnosti o jednotlivých zařízeních otevřené za účelem zobrazení konkrétních nastavení a zásad, které mají vliv na zařízení

## <a name="open-the-compliance-dashboard"></a>Otevření řídicího panelu pro dodržování předpisů

Otevřete **řídicí panel Intune pro dodržování předpisů zařízením**:

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **zařízení** > **Přehled** > karta**stav dodržování předpisů** .

> [!IMPORTANT]
> Aby mohla zařízení přijímat zásady dodržování předpisů, musejí být zaregistrovaná v Intune.

## <a name="dashboard-overview"></a>Přehled řídicího panelu

Po otevření řídicího panelu se zobrazí přehled se všemi sestavami dodržování předpisů. V těchto sestavách můžete kontrolovat:

- Celkové dodržování předpisů u zařízení
- Dodržování předpisů zařízením podle zásad
- Dodržování předpisů zařízením podle nastavení
- Stav agenta hrozeb
- Stav ochrany zařízení

![Obrázek řídicího panelu s řídicím panelem pro dodržování předpisů zařízením a různými sestavami](./media/compliance-policy-monitor/idc-1.png)

Když se do těchto sestav ponoříte, najdete také specifické zásady dodržování předpisů a nastavení pro konkrétní zařízení, včetně stavu dodržování předpisů pro každé nastavení.

### <a name="device-compliance-status"></a>Stav dodržování předpisů zařízením

Graf **stavu dodržování předpisů zařízením** zobrazuje stavy dodržování předpisů pro všechna zařízení zaregistrovaná v Intune. Stavy jsou uložené ve dvou různých databázích – Intune a Azure Active Directory.

> [!IMPORTANT]
> Intune sleduje u všech vyhodnocení dodržování předpisů na zařízení plán vrácení se změnami zařízení. [Přečtěte si další informace o plánu vrácení se změnami zařízení](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

Podrobnosti o různých stavech zásad dodržování předpisů zařízením jsou následující:

- **Vyhovující předpisům**: Zařízení úspěšně použilo jedno nebo více nastavení zásad dodržování předpisů zařízením.

- **V období odkladu**: Na zařízení je zacíleno jedno nebo více nastavení zásad dodržování předpisů zařízením. Ale uživatel zatím zásady nepoužil. To znamená, že zařízení nedodržuje předpisy, ale je v období odkladu definovaném správcem.

  - Přečtěte si další informace o [akcích pro zařízení nedodržující předpisy](actions-for-noncompliance.md).

- **Nevyhodnoceno**: Počáteční stav všech nově zaregistrovaných zařízení. Mezi další možné příčiny tohoto stavu patří:

  - Zařízení, která nemají přiřazenou zásadu dodržování předpisů a nemají Trigger ke kontrole dodržování předpisů
  - Zařízení, která nejsou zaregistrovaná od poslední aktualizace zásad dodržování předpisů
  - Zařízení, která nejsou přidružená konkrétnímu uživateli, například:
    - zařízení se systémem iOS/iPadOS zakoupená prostřednictvím programu Apple Program registrace zařízení (DEP), který nemá přidružení uživatele
    - Zařízení s Androidem pro veřejného terminálu nebo zařízení s Androidem Enterprise
  - Zařízení zaregistrovaná pomocí účtu správce registrace zařízení (DEM)

- **Nedodržující předpisy**: Zařízení se nepodařilo použít jedno nebo více nastavení zásad dodržování předpisů zařízením. Nebo uživatel nedodržuje zásady.

- **Zařízení není synchronizované**: Zařízení se nepodařilo oznámit svůj stav zásad dodržování předpisů zařízením z některého z následujících důvodů:

  - **Neznámý**: Zařízení je offline nebo se mu s Intune nebo Azure AD nepodařilo komunikovat z jiných důvodů.

  - **Chyba**: Zařízení se nepodařilo komunikovat s Intune a Azure AD a obdrželo chybovou zprávu s odůvodněním.

> [!IMPORTANT]
> Zařízení, která jsou zaregistrovaná v Intune, ale nejsou na ně zacílené žádné zásady dodržování předpisů zařízením, jsou v této sestavě uvedená jako **Vyhovující předpisům**.

#### <a name="drill-down-for-more-details"></a>Zobrazení podrobností

V grafu **Stav dodržování předpisů pro zařízení** vyberte některý stav. Můžete například vybrat **Nedodržující předpisy**:

![Výběr stavu dodržování předpisů](./media/compliance-policy-monitor/select-not-compliant-status.png)

Tato akce otevře okno **dodržování předpisů zařízením** a zobrazí zařízení v grafu **stavu zařízení** . Graf zobrazuje více podrobností o zařízeních v tomto stavu, včetně platformy operačního systému, data posledního vrácení se změnami a dalších.
![Snímek řídicího panelu s podrobnostmi o zařízeních v příslušném stavu](./media/compliance-policy-monitor/drill-down-details.png)

Pokud chcete zobrazit všechna zařízení vlastněná konkrétním uživatelem, můžete také filtrovat sestavu grafu zadáním e-mailu uživatele.

> [!TIP]
> Pokud se uživatel do zařízení přihlásí, zařízení se zásadami dodržování předpisů zařízení odešle zprávu o dodržování předpisů zpět do Intune, která zobrazuje **systémový účet** jako hlavní název uživatele. Důvodem je to, že zásady dodržování předpisů pro zařízení byly cílené na skupinu uživatelů nebo zařízení a v době vyhodnocení dodržování předpisů nebylo na zařízení přihlášen žádný uživatel.
>
> Pokud se navíc ke stejnému zařízení přihlásilo více uživatelů a toto zařízení je cílem zásad dodržování předpisů pro zařízení a zvažuje, že tito uživatelé jsou součástí stejné zásady dodržování předpisů pro zařízení, které je třeba vyhodnotit, může sestava dodržování předpisů zobrazovat stejné zařízení víckrát, protože každý uživatel přihlášený k zařízení musí vyhodnotit zásady dodržování předpisů zařízením a nahlásit ho zpátky do Intune.

#### <a name="filter-and-columns"></a>Filtrování a sloupce

![Výběr tlačítek Filtrovat a Sloupce pro změnu výsledků zobrazených v grafu](./media/compliance-policy-monitor/filter-columns.png)

Když vyberete tlačítko **Filtr** , otevře se filtr s dalšími možnostmi, včetně stavu **dodržování předpisů** , zařízení s **jailbreakem** a dalších. Kliknutím na **Použít** výsledky aktualizujete.

Pomocí vlastnosti **Sloupce** můžete ve výstupním grafu přidávat nebo odebírat sloupce. Například sloupec **Hlavní název uživatele** může zobrazovat e-mailovou adresu zaregistrovanou na zařízení. Kliknutím na **Použít** výsledky aktualizujete.

#### <a name="device-details"></a>Podrobnosti o zařízení

V grafu **podrobností o zařízení** vyberte konkrétní zařízení a pak vyberte **dodržování předpisů zařízením**:

![Výběr zařízení a možnosti Dodržování předpisů zařízením pro zobrazení použitých zásad dodržování předpisů](./media/compliance-policy-monitor/see-policies-applied-specific-device.png)

Intune zobrazí další podrobnosti o nastavení zásad dodržování předpisů zařízením použitým na tomto zařízení. Když některou ze zásad vyberete, zobrazí se všechna její nastavení.

### <a name="devices-without-compliance"></a>Zařízení bez dodržování předpisů

Na stránce *stav dodržování předpisů* můžete vedle grafu *dodržování zásad* vybrat dlaždici **zařízení bez zásad dodržování předpisů** a zobrazit informace o zařízeních, která nemají přiřazené žádné zásady dodržování předpisů:

![Zobrazení zařízení bez zásad dodržování předpisů](./media/compliance-policy-monitor/devices-without-policies.png)

Když tuto dlaždici vyberete, zobrazí se všechna zařízení bez zásad dodržování předpisů. Kromě toho jsou zde uvedeny informace o uživateli zařízení, stavu nasazení zásady a modelu zařízení.

#### <a name="what-you-need-to-know"></a>Co je potřeba vědět

- U nastavení zabezpečení **Označit zařízení, která nemají přiřazené žádné zásady dodržování předpisů, jako** je důležité určit zařízení bez zásad dodržování předpisů. Potom jim můžete přiřadit aspoň jednu zásadu dodržování předpisů.

  Nastavení zabezpečení můžete konfigurovat na portálu Intune.  > **Nastavení zásad dodržování**předpisů **zařízením** > v**zásadách dodržování předpisů**. Potom nastavte možnost **Označit zařízení, která nemají přiřazené žádné zásady dodržování předpisů, jako** na **Vyhovující předpisům**, nebo **Nevyhovující předpisům**.

  Další informace najdete v článku o [vylepšeních zabezpečení ve službě Intune](https://blogs.technet.microsoft.com/intunesupport/2018/02/09/updated-upcoming-security-enhancements-in-the-intune-service/).

- Uživatelé, kteří mají přiřazen kterýkoli typ zásady dodržování předpisů, se v sestavě nezobrazí (bez ohledu na platformu zařízení). Pokud jste například uživateli se zařízením s Androidem přiřadili zásadu dodržování předpisů pro Windows, jeho zařízení se v sestavě nezobrazí. Intune ale toto zařízení s Androidem vyhodnotí jako nevyhovující. Pokud se chcete podobným problémům vyhnout, doporučujeme vytvářet zásady pro každou platformu zařízení zvlášť a nasazovat je u všech uživatelů.

### <a name="per-policy-device-compliance"></a>Dodržování předpisů zařízením podle zásad

V grafu **dodržování zásad** se zobrazují zásady a kolik zařízení dodržuje předpisy a nedodržují předpisy.

![Snímek seznamu zásad s počtem zařízení, které je splňují a nesplňují](./media/compliance-policy-monitor/idc-8.png)

### <a name="setting-compliance"></a>Dodržování nastavení

Graf **Nastavení dodržování předpisů** zobrazuje všechna nastavení zásad dodržování předpisů zařízením ze všech zásad dodržování předpisů, platformy nastavení zásad a počet zařízení nesplňujících požadavky.

![Snímek seznamu všech nastavení v různých zásadách](./media/compliance-policy-monitor/idc-10.png)

## <a name="view-compliance-reports"></a>Zobrazení sestav dodržování předpisů

Kromě použití grafů na *stav dodržování předpisů*můžete přejít na **zprávy** > **dodržování předpisů zařízením**.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Vyberte **Devices** > **monitorování**zařízení a pak z nižšího **dodržování předpisů** vyberte sestavu, kterou chcete zobrazit. K dispozici jsou tyto sestavy dodržování předpisů:

   - Dodržování předpisů zařízení
   - Zařízení nedodržující předpisy
   - Zařízení bez zásad dodržování předpisů
   - Dodržování nastavení
   - Dodržování zásad
   - Sestava ověření stavu systému Windows
   - Stav agenta hrozeb

Další informace o sestavách najdete v tématu [sestavy Intune](../fundamentals/reports.md) .

## <a name="view-status-of-device-policies"></a>Zobrazení stavu zásad zařízení

Různé stavy zásad můžete zkontrolovat podle platformy. Máte například zásady dodržování předpisů v macOS. Chcete zobrazit zařízení, které jsou těmito zásadami ovlivněné, a zjistit, jestli se vyskytly konflikty nebo chyby.

Tato funkce je zahrnutá v sestavách stavu zařízení:

1. Vyberte > **zásady****zásady dodržování předpisů**pro **zařízení** > . Zobrazí se seznam zásad včetně platformy, pokud je příslušná zásada přiřazená, a další podrobnosti.
2. Vyberte zásadu > **Přehled**. Přiřazení zásad v tomto zobrazení zahrnuje následující stavy:

    - **Úspěch**: zásada se použije
    - **Chyba**: zásadu se nepovedlo použít. Tato zpráva se obvykle zobrazí s chybovým kódem, který odkazuje na vysvětlení.
    - **Konflikt**: pro stejné zařízení se aplikují dvě nastavení a Intune ho nedokáže rozřadit do konfliktu. Správce by měl provést kontrolu.
    - **Čeká na vyřízení**: zařízení ještě není zaregistrované v Intune, aby bylo možné tyto zásady přijmout.
    - **Nedá se použít**: zařízení nemůže tuto zásadu přijmout. Zásada například aktualizuje nastavení pro iOS 11.1, ale zařízení používá iOS 10.

3. Pokud chcete zobrazit podrobnosti o zařízeních používajících tyto zásady, vyberte některý stav. Vyberte například **Úspěšné**. V dalším okně se zobrazí podrobnosti o konkrétním zařízení včetně jeho názvu a stavu nasazení.

## <a name="how-intune-resolves-policy-conflicts"></a>Způsob řešení konfliktů zásad v Intune

Konflikty zásad můžou vzniknout, když se na zařízení použije více zásad Intune. Pokud se nastavení zásad překrývají, vyřeší Intune všechny konflikty s použitím následujících pravidel:

- Pokud konfliktní nastavení pocházejí ze zásad konfigurace a dodržování předpisů služby Intune, bude mít nastavení v zásadách dodržování předpisů přednost před nastavením v zásadách konfigurace. Platí to i v situaci, kdy je nastavení v zásadách konfigurace bezpečnější.

- Pokud jste nasadili více zásad dodržování předpisů, použije Intune ty nejbezpečnější z nich.

## <a name="next-steps"></a>Další kroky

[Přehled zásad dodržování předpisů](device-compliance-get-started.md)
