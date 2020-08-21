---
title: Aplikace pro Microsoft Store
titleSuffix: Configuration Manager
description: Spravujte a nasaďte aplikace z Microsoft Store pro firmy a vzdělávání pomocí Configuration Manager.
ms.date: 12/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a8125f55215fd597d9611723e1d36629850bff44
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695218"
---
# <a name="manage-apps-from-the-microsoft-store-for-business-and-education-with-configuration-manager"></a>Správa aplikací z Microsoft Store pro firmy a vzdělávání pomocí Configuration Manager

[Microsoft Store pro firmy a vzdělávání](/microsoft-store/) je místo, kde můžete najít a získat aplikace pro Windows pro vaši organizaci. Když úložiště připojíte k Configuration Manager, synchronizuje se seznam aplikací, které jste získali. Tyto aplikace můžete zobrazit v konzole Configuration Manager a nasazovat je, jako byste nasadili jakoukoli jinou aplikaci.

## <a name="online-and-offline-apps"></a><a name="bkmk_apps"></a> Online a offline aplikace

Microsoft Store pro firmy a vzdělávání podporuje dva typy aplikací:

- **Online**: Tento typ licence vyžaduje, aby se uživatelé a zařízení připojili k Storu a získali aplikaci a její licenci. Zařízení s Windows 10 musí být připojená k Azure AD, Azure Active Directory (Azure AD).  

- **Offline**: Tento typ umožňuje ukládat aplikace a licence do mezipaměti, aby se nasadily přímo v místní síti. Zařízení se nepotřebují připojit k úložišti nebo mít připojení k Internetu.

Další informace najdete v tématu [přehled Microsoft Store pro firmy a vzdělávání](/microsoft-store/microsoft-store-for-business-overview).

### <a name="summary-of-capabilities"></a>Souhrn funkcí

Configuration Manager podporuje správu Microsoft Store pro obchodní a vzdělávací aplikace na zařízeních s Windows 10 pomocí klienta Configuration Manager a taky zařízení s Windows 10 zaregistrovaných v Microsoft Intune. Configuration Manager nabízí následující možnosti pro online a offline aplikace:

|Schopnost|Offline aplikace|Online aplikace|
|------------|------------|------------|
|Synchronizovat data aplikace s Configuration Manager<br>(synchronizace probíhá každých 24 hodin)|Ano|Ano|
|Vytváření aplikací Configuration Manager z aplikací ze Storu|Ano|Ano|
|Podpora pro bezplatné aplikace ze Storu|Ano|Ano|
|Podpora placených aplikací ze Storu|Ne|Ano,<sup>[Poznámka: 1](#bkmk_note1)</sup>|
|Podpora požadovaných nasazení pro kolekce uživatelů nebo zařízení|Ano|Ano|
|Podpora dostupných nasazení pro kolekce uživatelů nebo zařízení|Ano|Ano|
|Podpora obchodních aplikací ze Storu|Ano|Ano|
|Zřízení aplikace pro Store pro všechny uživatele na zařízení –<sup>[Poznámka 2](#bkmk_note2)</sup><!--1358310-->|Ano|Ano|

#### <a name="note-1-online-licensed-apps-version-requirement"></a><a name="bkmk_note1"></a> Poznámka 1: požadavek na verzi licencovaných aplikací online

Pokud chcete nasadit online licencované aplikace do zařízení s Windows 10 pomocí klienta Configuration Manager, musí používat Windows 10 verze 1703 nebo novější.  

#### <a name="note-2-configuration-manager-minimum-version"></a><a name="bkmk_note2"></a> Poznámka 2: Configuration Manager minimální verze

Počínaje verzí 1806. Další informace najdete v tématu [vytváření aplikací pro Windows](../get-started/creating-windows-applications.md#bkmk_provision).  

### <a name="deploying-online-apps-using-the-microsoft-store-for-business-and-education-to-devices-that-run-the-configuration-manager-client"></a>Nasazení online aplikací pomocí Microsoft Store pro firmy a vzdělávání u zařízení, na kterých běží klient Configuration Manager

Než nasadíte Microsoft Store pro obchodní a vzdělávací aplikace do zařízení, na kterých běží plný Configuration Manager klient, vezměte v úvahu následující body:

- Pro plnou funkčnost musí na zařízeních běžet Windows 10 verze 1703 nebo novější.  

- Zaregistrujte nebo připojte zařízení ke stejnému tenantovi Azure AD, kde jste zaregistrovali Microsoft Store pro firmy a vzdělávání jako nástroj pro správu.  

- Když se účet místního správce přihlásí na zařízení, nemůže získat přístup k Microsoft Store pro obchodní a vzdělávací aplikace.  

- Zařízení musí mít živé připojení k Internetu Microsoft Store pro firmy a vzdělávání. Další informace, včetně konfigurace proxy serveru, najdete v části [požadavky](/microsoft-store/prerequisites-microsoft-store-for-business).  

### <a name="notes-for-devices-running-earlier-versions-of-windows-10"></a>Poznámky pro zařízení s dřívějšími verzemi Windows 10

Na zařízeních s klientem Configuration Manager a systémem Windows 10 verze 1607 nebo starší platí následující funkce:  

Když vynutili instalaci aplikace na zařízení jedním z následujících způsobů:  

- Uživatel aplikaci nainstaluje.  

- Nasazení dosáhne konečného termínu instalace

- Opakované vyhodnocení po instalaci pro požadovaná nasazení  

Pak dojde k následujícímu chování:  

- Klient Configuration Manager vynutil aplikaci spuštěním Microsoft Store aplikace.  

- Uživatel musí dokončit instalaci ze Storu.  

- V konzole Configuration Manager nahlásí stav nasazení aplikace chybu s následující chybou: "Microsoft Store aplikace byla otevřena v klientském počítači a čeká, až uživatel dokončí instalaci."  

Při dalším cyklu hodnocení aplikace:  

- Pokud uživatel aplikaci nainstaloval ze Storu, aplikace ohlásí **úspěch** stavu.  

- Pokud se uživatel nepokusil nainstalovat aplikaci ze Storu:  

  - Pro požadovaná nasazení se klient Configuration Manager pokusí znovu spustit aplikaci Store.  

  - Configuration Manager nebude znovu vymáhat dostupná nasazení

#### <a name="devices-running-earlier-versions-of-windows-10"></a>Zařízení s dřívějšími verzemi Windows 10

- Obchodní aplikace nemůžete nasadit z Microsoft Store pro firmy a vzdělávání.

- Když nasadíte placené aplikace z obchodu, uživatelé se musí přihlásit do Storu a získat aplikaci sami.  

- Pokud nasadíte zásady skupiny, abyste zakázali přístup k verzi Microsoft Store spotřebitelů, nasazení z Microsoft Store pro firmy a vzdělávání nebudou fungovat. K tomuto chování dochází, i když povolíte Microsoft Store pro firmy a vzdělávání.  

## <a name="set-up-synchronization"></a><a name="bkmk_setup"></a> Nastavení synchronizace

Když synchronizujete seznam Microsoft Store pro obchodní a vzdělávací aplikace, které vaše organizace získala, zobrazí se tyto aplikace v konzole Configuration Manager.

Připojte svůj Configuration Manager web k Azure AD a Microsoft Store pro firmy a vzdělávání. Další informace a podrobnosti o tomto procesu najdete v tématu [Konfigurace služeb Azure](../../core/servers/deploy/configure/azure-services-wizard.md). Umožňuje vytvořit připojení ke službě **Microsoft Store pro firmy** .

Ujistěte se, že spojovací bod služby a cílová zařízení mají přístup ke cloudové službě. Další informace najdete v tématu [předpoklady pro Microsoft Store pro firmy a vzdělávání – konfigurace proxy serveru](/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration).

### <a name="supplemental-information-and-configuration"></a><a name="bkmk_config"></a> Doplňující informace a konfigurace

Na stránce **aplikace** v Průvodci službami Azure nejdřív nakonfigurujte **prostředí Azure** a **webovou aplikaci**. Pak si přečtěte část **Další informace** v dolní části stránky. Tyto informace zahrnují následující další akce na portálu Microsoft Store for Business a vzdělávání:  

- Nakonfigurujte Configuration Manager jako nástroj pro správu úložiště. Další informace najdete v tématu [Konfigurace poskytovatele správy](/microsoft-store/configure-mdm-provider-microsoft-store-for-business).  

- Povolí podporu pro offline licencované aplikace. Další informace najdete v tématu [distribuce offline aplikací](/microsoft-store/distribute-offline-apps).  

- Získejte alespoň jednu aplikaci. Další informace najdete v tématu [vyhledání a získání aplikací](/microsoft-store/find-and-acquire-apps-overview).  

Na stránce **Konfigurace** v Průvodci službami Azure zadejte následující informace:  

- **Cesta k úložišti obsahu aplikace Microsoft Store pro firmy**: Zadejte sdílenou cestu k síti, včetně složky. Například, `\\server\share\folder`. Když se server lokality synchronizuje s úložištěm, uloží obsah do mezipaměti v tomto umístění. Když vytvoříte aplikaci v Configuration Manager, server lokality zkopíruje obsah aplikace z této místní mezipaměti do knihovny obsahu webu.  

- **Vybrané jazyky**: Vyberte jazyky, které se mají synchronizovat ze Storu, a zobrazí se uživatelům v centru softwaru. Pokud uživatel například nakonfiguruje systém Windows pro němčinu, Centrum softwaru zobrazí německé řetězce pro aplikaci ze Storu. Toto chování vyžaduje, aby byl tento jazyk synchronizovaný a aby existoval pro konkrétní aplikaci.

- **Výchozí jazyk**: Pokud je jazyk uživatele nedostupný, vyberte výchozí jazyk, který chcete použít.  

> [!NOTE]
> Configuration Manager nesynchronizuje ikonu aplikace ze Storu. Pokud potřebujete ikonu pro zobrazení této aplikace v centru softwaru, přidejte ji ručně do vlastností aplikace. Další informace najdete v tématu [Ruční zadání informací o aplikaci](create-applications.md#bkmk_manual-app).<!-- 2837053 -->

## <a name="create-and-deploy-the-app"></a><a name="bkmk_deploy"></a> Vytvoření a nasazení aplikace

Po synchronizaci vytvořte a nasaďte Microsoft Store pro obchodní a vzdělávací aplikace podobně jako jakékoli jiné aplikace Configuration Manager.

1. V pracovním prostoru **softwarová knihovna** konzoly Configuration Manager rozbalte položku **Správa aplikací**a pak vyberte možnost **informace o licenci pro uzel aplikace pro Store** .  

2. Zvolte aplikaci, kterou chcete nasadit, a pak na pásu karet vyberte **vytvořit aplikaci** .  

Lokalita vytvoří Configuration Manager aplikaci obsahující Microsoft Store pro firmy a vzdělávání.

Pak tuto aplikaci nasaďte a sledujte stejně jako jakoukoli jinou aplikaci Configuration Manager. Další informace najdete v následujících článcích:  

- [Nasazení aplikací](deploy-applications.md)
- [Monitorování aplikací z konzoly](monitor-applications-from-the-console.md)

## <a name="next-steps"></a>Další kroky

V pracovním prostoru **softwarová knihovna** rozbalte položku **Správa aplikací**a potom vyberte možnost **informace o licenci pro uzel aplikace pro Store** .

Pro každou aplikaci ze Storu, kterou spravujete, si prohlédněte následující informace o aplikaci:

- Název aplikace
- Aplikační platforma
- Počet licencí pro aplikaci, kterou vlastníte
- Počet dostupných licencí

Po nasazení online aplikací přijde všechny aktualizace této aplikace přímo z Microsoft Store. Configuration Manager nekontrolují dodržování předpisů pro online aplikace, a to pouze v případě, že systém Windows hlásí aplikaci jako nainstalovanou.  

Když do zařízení s Windows 10 nasazujete offline aplikace pomocí klienta Configuration Manager, neumožníte uživatelům aktualizovat aplikace z externích nasazení Configuration Manager. Řízení aktualizací pro offline aplikace je zvlášť důležité v prostředích s více uživateli, jako jsou například učebny. Jedním z možností, jak Microsoft Store zakázat, je použití [zásad skupiny](/windows/configuration/stop-employees-from-using-microsoft-store#block-microsoft-store-using-group-policy).

Jakmile Microsoft Store pro firmy a vzdělávací správce získá offline aplikaci, nepublikujte aplikaci uživatelům přes Store. Tato konfigurace zajistí, že uživatelé nebudou moct instalovat nebo aktualizovat online. Uživatelé dostanou pouze offline aktualizace aplikací prostřednictvím Configuration Manager.

## <a name="see-also"></a>Viz také:

[Řešení potíží s Microsoft Store pro podnikání a vzdělávání pomocí Configuration Manager](troubleshoot-microsoft-store-for-business-integration.md)