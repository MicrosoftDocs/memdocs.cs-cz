---
title: Spoluspráva pro zařízení s Windows 10
titleSuffix: Configuration Manager
description: Naučte se souběžně spravovat zařízení s Windows 10 pomocí Configuration Manager i Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/24/2020
ms.topic: overview
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: e06dc0d40eb6359d11ef31045989d7ed398b3687
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711319"
---
# <a name="what-is-co-management"></a>Co je spoluspráva?

<!-- 1350871 -->
Spoluspráva je jedním z hlavních způsobů, jak připojit stávající nasazení Configuration Manager ke cloudu Microsoft 365. Pomůže vám odemknout další cloudové možnosti, jako je podmíněný přístup.

Zařízení s Windows 10 můžete pomocí Configuration Manageru a Microsoft Intune spravovat souběžně – a to formou spolusprávy. Umožňuje vám připojit stávající investice do Configuration Manager přidáním nových funkcí. Díky spolusprávě máte flexibilitu při používání technologických řešení, které nejlépe vyhovuje vaší organizaci.

Když má zařízení s Windows 10 klienta Configuration Manager a je zaregistrované v Intune, získáte výhody obou služeb. Vy budete řídit, které úlohy (pokud existují), přepnete autoritu z Configuration Manager na Intune. Configuration Manager nadále spravuje všechny ostatní úlohy, včetně úloh, které nepřepnete do Intune, a všech ostatních funkcí Configuration Manager, které spoluspráva nepodporuje.

Také je možné vytvořit pilotní úlohu s využitím samostatné kolekce zařízení. Pilotní nasazení umožňuje testovat funkčnost Intune s podmnožinou zařízení před přepnutím větší skupiny.

![Diagram s přehledem spolusprávy](media/co-management-overview.svg)

[Zobrazit diagram v plné velikosti](media/co-management-overview.svg)

> [!Note]  
> Pokud současně spravujete zařízení s Windows 10 pomocí Configuration Manager i Microsoft Intune, tato konfigurace se nazývá *spoluspráva*. Když spravujete zařízení pomocí Configuration Manager a zaregistrujete je do služby MDM třetí strany, tato konfigurace se nazývá *koexistence*. Pokud se dva řídící autority pro jedno zařízení nepatřičně orchestrují mezi těmito dvěma zařízeními, může být obtížné. Díky spolusprávě Configuration Manager a Intune vyvážit [úlohy](#workloads) a zajistěte, aby nedocházelo ke konfliktům. Tato interakce neexistuje se službami třetích stran, takže existují určitá omezení možností správy koexistence. Další informace najdete v tématu [koexistence MDM třetí strany s Configuration Manager](coexistence.md).

## <a name="paths-to-co-management"></a>Cesty ke spolusprávě

Existují dva hlavní cesty, které je možné využít ke společné správě:  

- **Existující klienti Configuration Manager**: máte zařízení s Windows 10, která už Configuration Manager klienty. Nastavili jste hybridní službu Azure AD a zaregistrovali jste ji v Intune.  

- **Nová internetová zařízení**: máte nová zařízení s Windows 10, která se připojí k Azure AD a automaticky se zaregistrují do Intune. Nainstalujete klienta Configuration Manager pro dosažení stavu spolusprávy.  

Další informace o cestách najdete v tématu věnovaném [cestám ke společné správě](quickstart-paths.md).

## <a name="benefits"></a>Výhody

Když zaregistrujete existující Configuration Manager klienty při spolusprávě, získáte následující okamžitou hodnotu:  

- Podmíněný přístup s dodržováním předpisů zařízením  

- Vzdálené akce založené na Intune, například: restart, vzdálené řízení nebo obnovení továrního nastavení

- Centralizovaná viditelnost stavu zařízení  

- Propojení uživatelů, zařízení a aplikací pomocí Azure Active Directory (Azure AD)  

- Moderní zřizování pomocí Windows autopilotu  

- Vzdálené akce

Další informace o této okamžité hodnotě ze spolusprávy najdete v tématu rychlé starty, které se [připojují ke cloudu a spolusprávě](quickstarts.md).

Spoluspráva také umožňuje orchestraci pomocí Intune pro několik úloh. Další informace najdete v části [úlohy](#workloads) .

## <a name="prerequisites"></a>Požadavky

Společná správa má tyto požadavky v následujících oblastech:

- [Licencování](#licensing)  
- [Configuration Manager](#configuration-manager)  
- [Azure Active Directory](#azure-ad) (Azure AD)  
- [Microsoft Intune](#intune)  
- [Windows 10](#windows-10)  
- [Oprávnění a role](#permissions-and-roles)  

### <a name="licensing"></a>Licencování

- Azure AD Premium

    > [!Note]  
    > Předplatné Enterprise Mobility + Security (EMS) zahrnuje Azure Active Directory Premium i Microsoft Intune.

- Aspoň jednu licenci Intune pro vás jako správce pro přístup k portálu Intune.

    > [!Tip]
    > Ujistěte se, že přiřadíte licenci pro Intune k účtu, který používáte k přihlášení do svého tenanta. V opačném případě se přihlášení nezdařilo s chybovou zprávou "uživatel nebyl rozpoznán".
    >
    > Už nemusíte kupovat a přiřazovat k vašim uživatelům jednotlivé licence Intune ani EMS. Další informace najdete v tématu [Nejčastější dotazy k produktu a licencování](../core/understand/product-and-licensing-faq.md#bkmk_mem).

### <a name="configuration-manager"></a>Configuration Manager

Spoluspráva vyžaduje Configuration Manager verze 1710 nebo novější.

Od verze 1806 Configuration Manager můžete připojit více instancí Configuration Manager k jednomu klientovi Intune. <!--1357944-->  

Povolení spolusprávy nevyžaduje, abyste svůj web připojili ke službě Azure AD. Pro [druhý scénář cesty](#paths-to-co-management)vyžadují internetové Configuration Manager klienti [bránu pro správu cloudu](../core/clients/manage/cmg/plan-cloud-management-gateway.md) (CMG). CMG vyžaduje, aby se lokalita [připojila k Azure AD pro správu cloudu](../core/servers/deploy/configure/azure-services-wizard.md).

### <a name="azure-ad"></a>Azure AD

- Zařízení s Windows 10 musí být připojená k Azure AD. Může to být jeden z následujících typů:  

  - [Hybridní služba Azure AD – připojeno](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan), kde je zařízení připojené k místní službě Active Directory a připojené k vašemu Azure Active Directory.  

  - Pouze [Služba Azure AD – připojeno](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan) . (Tento typ se někdy označuje jako "cloudová doména připojená".<!--SCCMDocs issue 605-->  

### <a name="intune"></a>Intune

- [Nastavení Intune](https://docs.microsoft.com/intune/setup-steps)  

- [Povolení automatické registrace pro Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)  

### <a name="windows-10"></a>Windows 10

Upgradujte svoje zařízení na Windows 10 verze 1709 nebo novější. Další informace najdete v tématu věnovaném [přijetí Windows jako služby](../core/understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service).

> [!IMPORTANT]
> Zařízení s Windows 10 Mobile nepodporují spolusprávu.

### <a name="permissions-and-roles"></a>Oprávnění a role

<!--SCCMDocs issue #667-->
| Akce | Nutná role |
|----|----|
| Nastavení brány pro správu cloudu v Configuration Manager | **Správce předplatného** Azure |
| Vytváření aplikací Azure AD z Configuration Manager | **Globální správce** Azure AD |
| Import aplikací Azure v Configuration Manager | **Správce s úplnými oprávněními** Configuration Manager<br>Nepotřebujete žádné další role Azure. |
| Povolit spolusprávu v Configuration Manager | Uživatel Azure AD<br>Configuration Manager **úplného správce** se **všemi** právy oboru.<!--SCCMDoc issue 626--> |

Další informace o rolích Azure najdete v tématu [pochopení různých rolí](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).

Další informace o rolích Configuration Manager najdete v tématu [základy správy na základě rolí](../core/understand/fundamentals-of-role-based-administration.md).

## <a name="workloads"></a>Úlohy

Nemusíte přepínat úlohy, nebo je můžete provést jednotlivě, až budete připraveni. Configuration Manager nadále spravuje všechny ostatní úlohy, včetně úloh, které nepřepnete do Intune, a všech ostatních funkcí Configuration Manager, které spoluspráva nepodporuje.

Spoluspráva podporuje následující úlohy:

- Compliance zásady  

- Zásady web Windows Update  

- Zásady přístupu k prostředkům  

- Funkce Endpoint Protection  

- Konfigurace zařízení  

- Aplikace pro Office Klikni a spusť  

- Klientské aplikace  

Další informace najdete v tématu [úlohy](workloads.md).

## <a name="monitor-co-management"></a>Sledování spolusprávy

Řídicí panel spolusprávy vám pomůže zkontrolovat počítače, které jsou ve vašem prostředí spoluspravované. Grafy můžou identifikovat zařízení, která by mohla vyžadovat pozornost.

![Snímek obrazovky řídicího panelu spolusprávy](media/co-management-dashboard.png)

Další informace najdete v tématu [monitorování spolusprávy](how-to-monitor.md).

## <a name="next-steps"></a>Další kroky

- [Další informace o okamžité hodnotě a Začínáme s spolusprávou](quickstarts.md)  

- [Kurz: povolení spolusprávy pro stávající klienty Configuration Manager](tutorial-co-manage-clients.md)  
