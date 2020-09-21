---
title: Shromažďování dat pro připojení tenanta
titleSuffix: Configuration Manager
description: Seznamte se s diagnostickými daty, která Configuration Manager shromažďuje pro funkce připojení tenanta.
ms.date: 09/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 4b305a71-9ad8-4332-9692-d51554158981
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 00a01e4ceadc716a42381999b2e4603bcbe55524
ms.sourcegitcommit: eaa077aa028a76a4873e4aa7437888f901a7e77f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/18/2020
ms.locfileid: "90767797"
---
# <a name="tenant-attach-data-collection"></a>Shromažďování dat pro připojení tenanta

*Platí pro: Configuration Manager (Current Branch)*

<!-- 6505626 -->
Když připojíte Configuration Manager web k tenantovi Microsoft Intune, lokalita odešle společnosti Microsoft další data. Tento článek shrnuje data, která se odesílají.

Při připojení klienta se vaše konzola v cloudu centra pro správu Microsoft Endpoint Manageru. Tato architektura umožňuje lokalitě Configuration Manager synchronizovat data o zařízení a uživatele s vaším klientem Intune. Pak můžete dotazovat a prezentovat data z místního prostředí v konzole cloudu v reálném čase bez aktivní synchronizace. Může načíst rozsáhlá Nestálá data z vaší místní lokality. Při připojení klienta se pomocí kombinace těchto metod poskytují efektivní informace v konzole cloudu.

> [!IMPORTANT]
> Zásady pro zpracování dat společnosti Microsoft jsou popsány v [Microsoft Intune prohlášení o zásadách ochrany osobních údajů](/legal/intune/microsoft-intune-privacy-statement). Zákaznická data používáme jenom k poskytování služeb, ke kterým jste se zaregistrovali.
>
> Žádná data shromážděná naší službou nebudeme prodávat z jakéhokoli důvodu žádné třetí straně.
>
> Data jsou všechna požadovaná data služby potřebná pro připojení klienta k prostředí. Požadovaná data služby obsahují následující informace:
>
> - **Obsah zákazníka**, což je obsah, který vytvoříte. Například název aplikace LOB.
> - **Funkční data**, která obsahují informace potřebné k tomu, aby bylo možné provést úlohu. Například konfigurační informace o aplikaci.
> - **Diagnostická data služby**, což jsou data potřebná k zajištění zabezpečení služby, aktuálnost a provádění podle očekávání. Vzhledem k tomu, že tato data jsou výhradně spojená s propojenými prostředími, je nezávisle na požadovaných nebo volitelných úrovních diagnostických dat.

Microsoft Endpoint Manager shromažďuje informace, které spadají do tří kategorií:

- **Identifikovaná data**: většina dat, která služba Microsoft Endpoint Manager shromažďuje, má identifikovaná data. Tato data se vážou k uživateli, zařízení nebo aplikaci a pro správu jako takovou jsou nezbytná. Identifikovaná data se používají ke správě zařízení a aplikací uživatele.

- **Pseudonymovaná data**: Tato data jsou přidružená k jedinečnému identifikátoru. Obvykle se jedná o číslo generované systémem, které sám o sobě nemůže identifikovat jednotlivé osoby. Microsoft Endpoint Manager používá tato data k poskytování podnikové služby.

- **Agregovaná data**: Tato data jsou statistiky využití, například počet zařízení nebo které ovládací prvky používáte v centru pro správu Microsoft Endpoint Manageru.

V následujících částech najdete příklady typů dat, která se klient připojuje ke cloudu. Jsou seskupeny podle funkční entity, takže se můžete podívat na konkrétní funkce, které používáte.

## <a name="applications"></a>Aplikace
<!-- 6502080 -->

Pro každý typ nasazení Instalační služba systému Windows (MSI):

- **ProductName**: název aplikace
- **Vydavatel**: entita, která publikovala software
- **Verze**: verze aplikace
- **ProductLanguage**: kód jazyka pro aplikaci
- **ProgramID**: identifikátor typu nasazení

## <a name="device-sync"></a>Synchronizace zařízení
<!-- 6505639 -->

Pro každé zařízení:

- **SMSID**: jedinečný identifikátor hierarchie Configuration Manager
- **AADTenantID**: jedinečný identifikátor tenanta Azure Active Directory (Azure AD)
- **AADDeviceID**: jedinečný identifikátor zařízení v Azure AD
- **Název**: název hostitele zařízení
- **DeviceOS**: název operačního systému zařízení. Například `Microsoft Windows NT Server 6.3`.
- **DeviceOSBuild**: verze buildu operačního systému zařízení. Například `10.0.19041`.
- **AADPrimaryUserID**: jedinečný identifikátor primárního uživatele zařízení ve službě Azure AD
- **Model**: model zařízení
- **Výrobce**: výrobce zařízení
- **Sériové: sériové**číslo zařízení
- **DomainNames**: všechny názvy domén pro zařízení
- **Skladová jednotka (SKU)**

## <a name="windows-defender-advanced-threat-protection-atp"></a>Windows Defender Advanced Threat Protection (ATP)
<!-- 6505652 -->

Pro každou kolekci, kterou jste vybrali pro nasazení zásad ATP:

- **CollectionID**: jedinečný identifikátor kolekce. Například `ABC00014`.
- **CollectionName**: název kolekce. Například `All Windows servers`.
- **CollectionType**: Určuje, zda se jedná o zařízení nebo kolekci uživatelů.
- **CountTargeted**: počet zařízení, na která tato zásada cílíte
- **CountCompliant**: počet zařízení, která jsou v souladu s touto zásadou.
- **CountNonCompliant**: počet zařízení, která nejsou kompatibilní s touto zásadou
- **CountFailed**: počet zařízení, kterým se nepovedlo zpracovat tuto zásadu
- **CountActivated**
- **CountEnforced**

## <a name="see-also"></a>Viz také

Obecnější informace o datech, která Configuration Manager shromažďuje, najdete v tématu [Diagnostika a data o využití pro Configuration Manager](../core/plan-design/diagnostics/diagnostics-and-usage-data.md).

Další informace o souvisejících aspektech ochrany osobních údajů najdete v následujících článcích:

- [Microsoft Intune – prohlášení o zásadách ochrany osobních údajů](/legal/intune/microsoft-intune-privacy-statement)
- [Dodržování předpisů pro Windows 10 a ochranu osobních údajů](/windows/privacy/windows-10-and-privacy-compliance)
- [Licenční podmínky a dokumentace](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  
- [Zabezpečení a ochrana osobních údajů v Microsoft Azure datových Centre](https://azure.microsoft.com/global-infrastructure/)  
- [Jistota v důvěryhodném cloudu](https://azure.microsoft.com/overview/trusted-cloud/)  
- [Centrum zabezpečení](https://www.microsoft.com/trustcenter)  
