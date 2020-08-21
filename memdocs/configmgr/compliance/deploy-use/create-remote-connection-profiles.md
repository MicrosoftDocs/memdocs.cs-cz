---
title: Vytváření profilů vzdáleného připojení
titleSuffix: Configuration Manager
description: Pomocí Configuration Manager profilů vzdáleného připojení umožníte uživatelům vzdálené připojení k pracovním počítačům.
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 8c6eabc4-5dda-4682-b03e-3a450e6ef65a
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 1434d7802eb1ed68cb0a575778bdae1e5e99c9ec
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694742"
---
# <a name="remote-connection-profiles-in-configuration-manager"></a>Profily vzdáleného připojení v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pomocí Configuration Manager profilů vzdáleného připojení umožníte uživatelům vzdálené připojení k pracovním počítačům. Tyto profily umožňují nasazení Připojení ke vzdálené ploše nastavení pro uživatele ve vaší hierarchii. Uživatelé mají přístup k libovolnému primárnímu pracovnímu počítači prostřednictvím připojení k síti VPN prostřednictvím vzdálené plochy.  

> [!IMPORTANT]  
> Když určíte nastavení profilu vzdáleného připojení pomocí Configuration Manager, klient uloží nastavení v místních zásadách systému Windows. Tato nastavení můžou potlačit nastavení vzdálené plochy, které nakonfigurujete v jiné aplikaci. Kromě toho, pokud ke konfiguraci nastavení vzdálené plochy použijete Zásady skupiny Windows, nastavení zadaná v Zásady skupiny přepíší nastavení Configuration Manager.

Configuration Manager vytvoří skupinu zabezpečení na klientech, **připojí se ke VZDÁLENÉMU počítači**. Když nasadíte profil vzdáleného připojení, klient přidá do této skupiny primární uživatele počítače. Místní správce může do této skupiny ručně přidat nebo odebrat uživatele, ale při dalším vyhodnocení dodržování předpisů profilu Configuration Manager aktualizuje členství.

> [!IMPORTANT]  
> Pokud se vztah spřažení uživatelských zařízení mezi uživatelem a zařízením změní, Configuration Manager zakáže profil vzdáleného připojení a nastavení brány Windows Firewall, aby se zabránilo připojení k počítači.

## <a name="prerequisites"></a>Předpoklady  

### <a name="external-dependencies"></a>Externí závislosti  

- Pokud chcete uživatelům povolit připojení z Internetu, nainstalujte a nakonfigurujte Brána vzdálené plochy Server. Další informace o tom, jak nainstalovat a nakonfigurovat Brána vzdálené plochy Server, najdete v tématu [Vzdálená plocha – přístup odkudkoli](/windows-server/remote/remote-desktop-services/rds-plan-access-from-anywhere).

- Pokud klienti používají bránu firewall založenou na hostiteli, musí povolit mstsc.exe program. Pokud konfigurujete profil vzdáleného připojení, povolte nastavení **Povolit výjimku brány Windows Firewall pro připojení v doménách systému Windows a v privátních sítích**. Toto nastavení umožňuje Configuration Manager automatickou konfiguraci brány Windows Firewall.

    > [!TIP]
    > Konfigurace brány Windows Firewall pomocí nastavení zásad skupiny může potlačit konfiguraci nastavenou v nástroji Configuration Manager. Pokud používáte Zásady skupiny ke konfiguraci brány Windows Firewall, ujistěte se, že nastavení Zásady skupiny neblokuje mstsc.exe.

    Pokud klienti používají jinou bránu firewall hostitele, nakonfigurujte tuto závislost brány firewall ručně.  

### <a name="configuration-manager-dependencies"></a>Závislosti nástroje Configuration Manager  

- Aby se uživatel mohl připojit k pracovnímu počítači, musí být tento počítač primárním zařízením uživatele. Další informace najdete v tématu [propojení uživatelů a zařízení pomocí spřažení uživatelských zařízení](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

- Aby bylo možné spravovat profily vzdáleného připojení, váš uživatelský účet potřebuje určitá oprávnění v Configuration Manager. Integrovaná role **Správce nastavení dodržování předpisů** zahrnuje oprávnění potřebná ke správě těchto profilů. Další informace najdete v tématu [Konfigurace správy na základě rolí](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="security-and-privacy-considerations"></a>Požadavky na zabezpečení a ochranu osobních údajů

### <a name="security-considerations"></a>Důležité informace o zabezpečení  

- Místo toho, abyste uživatelům povolili identifikaci jejich primárního zařízení, ručně zadejte spřažení uživatelských zařízení. Nepovolujte konfiguraci na základě využití.

  - Než budete moct nasadit profil vzdáleného připojení, musíte povolit možnost povolit **všem primárním uživatelům pracovních počítačů vzdálené připojení**. V této konfiguraci byste měli vždycky ručně zadat spřažení uživatelských zařízení. Neberte v úvahu informace, které Configuration Manager shromažďuje od uživatelů nebo ze zařízení, které mají být autoritativní. Pokud nasadíte profil a důvěryhodný administrativní uživatel neurčí spřažení uživatelských zařízení, mohou neoprávnění uživatelé obdržet zvýšená oprávnění a můžou se vzdáleně připojit k počítačům.

  - Configuration Manager shromažďuje informace na základě využití prostřednictvím stavových zpráv, což je rychlý, ale nezabezpečený komunikační kanál. Pro zmírnění této hrozby použijte podepisování pomocí protokolu SMB (Server Message Block) nebo IPsec (Internet Protocol security) mezi klientskými počítači a bodem správy.

- Omezte oprávnění místního správce v počítači serveru lokality. Místní správce na serveru lokality může ručně přidat členy do skupiny zabezpečení **Remote PC Connect** , kterou Configuration Manager automaticky vytvoří a udržuje. Tato akce může způsobit zvýšení oprávnění, protože členové obdrží oprávnění vzdálené plochy.

### <a name="privacy-considerations"></a>Aspekty ochrany osobních údajů  

Když se uživatel vzdáleně připojí k pracovnímu počítači, stáhne soubor. wsrdp. Tento soubor obsahuje název zařízení a název serveru Brána vzdálené plochy. Tyto hodnoty jsou nutné k vytvoření relace vzdálené plochy. Soubor .wsrdp se stáhne a automaticky se místně uloží. Tento soubor se přepíše při dalším spuštění relace vzdálené plochy uživatelem.  

## <a name="create-a-profile"></a>Vytvoření profilu

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** , rozbalte položku **Nastavení dodržování předpisů**a vyberte **profily vzdáleného připojení**.  

1. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte **vytvořit profil vzdáleného připojení**.  

1. Na stránce **Obecné** v **Průvodci vytvořením profilu vzdáleného připojení**zadejte název a volitelný popis profilu. Obě hodnoty mají maximální povolený limit 256 znaků.  

1. Na stránce **nastavení profilu** určete následující nastavení:  

    - **Úplný název a port serveru Brána vzdálené plochy (volitelné)**: zadejte název Brána vzdálené plochy serveru, který se má použít pro připojení. Tato hodnota má následující požadavky:

        - Název serveru nemůže být delší než 256 znaků.
        - Může obsahovat velká písmena, malá písmena a číselné znaky.
        - Kromě teček () `.` mezi segmenty a dvojtečkou ( `:` ) před portem jsou jedinými speciálními znaky pomlčky ( `–` ) a podtržítko ( `_` ).
        - Configuration Manager nepodporuje použití mezinárodního názvu domény pro tuto hodnotu.

    - **Povolit připojení pouze z počítačů, v nichž je spuštěna Vzdálená plocha s ověřování na úrovni sítě**: Toto nastavení ve výchozím nastavení přidá další úroveň zabezpečení pro připojení. Další informace najdete v tématu [udělení přístupu ke vzdálené ploše](/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#why-allow-connections-only-with-network-level-authentication).

    - Povolit následující nastavení připojení:

        - **Povolit vzdálené připojení k pracovním počítačům**

        - **Povolit vzdálené připojení všem primárním uživatelům pracovního počítače**

        - **Povolit výjimku brány Windows Firewall pro připojení k doménám systému Windows a k soukromým sítím**

        > [!IMPORTANT]  
        > Aby bylo možné pokračovat, musí být všechna tři nastavení stejná.

        Tato nastavení zakažte jenom v případě, že nasadíte profil pro vypnutí vzdálených připojení.

1. Dokončete průvodce.

Nový profil se zobrazí v uzlu **profily vzdáleného připojení** v pracovním prostoru **prostředky a kompatibilita** .  

## <a name="deploy"></a>Nasazení

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** , rozbalte položku **Nastavení dodržování předpisů**a vyberte **profily vzdáleného připojení**.

1. V seznamu **profily vzdáleného připojení** vyberte profil, který chcete nasadit. Na kartě **Domů** na pásu karet ve skupině **nasazení** vyberte **nasadit**.  

1. V okně **Nasadit profil vzdáleného připojení** zadejte následující informace:

    - **Kolekce**: procházením vyberte kolekci zařízení, do které chcete nasadit profil.

    - **Napravit pravidla nesplňující požadavky**, je-li to podporováno: Toto nastavení povolte, pokud chcete automaticky opravit nastavení profilu, když nedodržují předpisy na zařízení. Pokud neexistuje, může být profil nekompatibilní.

    - **Povolit nápravu mimo okno údržby**: Pokud nakonfigurujete časové období údržby pro kolekci, do které nasazujete profil, tuto možnost povolte, pokud chcete Configuration Manager opravit, a to mimo časové období údržby. Další informace najdete v tématu [použití časových období údržby](../../core/clients/manage/collections/use-maintenance-windows.md).

    - **Generovat upozornění**: tuto možnost povolte, pokud chcete nakonfigurovat výstrahu o dodržování předpisů.

    - **Zadejte plán vyhodnocení shody pro tyto standardní hodnoty konfigurace**: zadejte jednoduchý nebo vlastní plán, podle kterého klient vyhodnocuje profil.

1. Výběrem **OK** zavřete okno a vytvořte nasazení.

### <a name="client-evaluation"></a>Vyhodnocení klientů

Klient vyhodnocuje profil, když se uživatel přihlásí.

Pokud zařízení opustí kolekci, do které nasadíte profil vzdáleného připojení, Configuration Manager zakáže nastavení na zařízení. Aby však tento proces správně proběhl, musíte mít již nasazenu alespoň jednu položku konfigurace nebo standardní hodnoty konfigurace obsahující položku konfigurace z lokality.

### <a name="conflict-resolution"></a>Řešení konfliktů

Nesaďte více než jeden profil vzdáleného připojení s konfliktním nastavením do stejného zařízení. Například nasadíte dva profily s různými nastaveními do stejné kolekce. Nakonfigurujete jenom jedno nasazení profilu, aby se napravila **pravidla nesplňující požadavky, pokud se podporuje**. Toto nasazení může potlačit nastavení ve druhém profilu. Configuration Manager nepodporuje tento typ nasazení profilu vzdáleného připojení.

## <a name="monitor"></a>Monitorování

V konzole Configuration Manager otevřete pracovní prostor **monitorování** a vyberte **nasazení**. V seznamu **nasazení** vyberte nasazení profilu vzdáleného připojení.

Na hlavní stránce můžete zkontrolovat souhrnné informace o kompatibilitě nasazení profilu vzdáleného připojení. Chcete-li zobrazit podrobnější informace, vyberte nasazení profilu. Pak na kartě **Domů** na pásu karet ve skupině **nasazení** vyberte **Zobrazit stav**. Tato akce otevře stránku **stav nasazení** .  

Na stránce **Stav nasazení** naleznete následující karty:  

- **Kompatibilní**: Zobrazuje kompatibilitu profilu vzdáleného připojení podle počtu ovlivněných prostředků.

    > [!IMPORTANT]  
    > Klient vyhodnocuje profil vzdáleného připojení, pokud jej nelze použít. Nicméně stále hlásí, že jsou kompatibilní.

- **Chyba**: zobrazuje seznam všech chyb pro vybrané nasazení profilu vzdáleného připojení podle počtu ovlivněných prostředků.

- **Nekompatibilní**: zobrazuje seznam všech pravidel nesplňujících požadavky v rámci profilu vzdáleného připojení podle počtu ovlivněných prostředků.

- **Neznámé**: zobrazuje seznam všech zařízení, u nichž nebyla nahlášena kompatibilita pro vybrané nasazení profilu vzdáleného připojení, spolu s aktuálním stavem klienta pro daná zařízení.

Na libovolné kartě otevřete pravidlo, které vytvoří dočasný poduzel pod uzlem **Uživatelé** v pracovním prostoru **prostředky a kompatibilita** . Tento dílčí uzel obsahuje všechna zařízení se stavem dodržování předpisů vybrané karty.

V podokně **Podrobnosti o aktivech** jsou zobrazena zařízení s vybraným stavem dodržování předpisů pro tento profil. V seznamu otevřete zařízení, ve kterém se zobrazí další informace.

## <a name="reports"></a>Sestavy

Configuration Manager obsahují předdefinované sestavy, pomocí kterých můžete monitorovat informace o profilech vzdáleného připojení. Tyto sestavy obsahují kategorii sestav **Správa nastavení a kompatibility**.  

> [!IMPORTANT]  
> Zástupný znak () použijte `%` při použití parametrů **Filtr zařízení** a **Filtr uživatelů** v sestavách pro nastavení dodržování předpisů.  

Další informace o tom, jak nakonfigurovat vytváření sestav v Configuration Manager, najdete v tématu [Úvod do vytváření sestav](../../core/servers/manage/introduction-to-reporting.md).