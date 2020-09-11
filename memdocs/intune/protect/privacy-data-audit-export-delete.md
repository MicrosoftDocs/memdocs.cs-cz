---
title: Audit, export a odstranění osobních dat
titleSuffix: Microsoft Intune
description: Naučte se auditovat, exportovat a odstraňovat osobní data.
keywords: GDPR, osobní údaje, soukromí
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 9/10/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 96990be0-eb1e-43a4-a0e4-09c7dbdc2bf4
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5d792df5a4a8690751d7d140aa7fa89191aedb1b
ms.sourcegitcommit: d6cbd1a1c2926064e074e3431471534eb142c905
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/11/2020
ms.locfileid: "90012625"
---
# <a name="audit-export-or-delete-personal-data-in-intune"></a>Audit, export a odstranění osobních dat v Intune

Správci Intune mohou v protokolech auditu sledovat aktivity spojené s osobními daty. Správci také mohou osobní data exportovat a odstraňovat.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-intro-sentence.md)]

## <a name="audit-personal-data"></a>Audit osobních dat

Správci tenantů najdou v protokolech auditu zaznamenané aktivity, které v Microsoft Intune generují změnu. Protokoly auditu jsou k dispozici pro různé aktivity týkající se správy. Většinou jde o tyto akce: vytváření, aktualizace (úpravy), odstranění nebo přiřazení. Správci mohou kontrolovat také vzdálené úlohy, které generují auditované události. Protokoly auditu mohou obsahovat osobní data o uživatelích zařízení zaregistrovaných v Intune.  

Z bezpečnostních důvodů smí Intune udržovat protokoly auditu o akcích uživatelů a zařízení jenom za jeden rok. Po uplynutí ročního archivačního období budou tyto protokoly automaticky odstraněny.

Pokud chcete kontrolovat protokoly auditu, přečtěte si článek [Protokoly auditu pro aktivity v Intune](../fundamentals/monitor-audit-logs.md). 

Správci nemůžou odstranit protokoly auditu.

Auditované události se uchovávají jeden rok. Správci tenanta si mohou vyžádat protokoly auditu vyplněním [formuláře žádosti o podporu](https://privacy.microsoft.com/en-US/privacy-questions?).

## <a name="export-personal-data"></a>Export osobních dat

Správci mohou osobní data koncových uživatelů exportovat, včetně účtů, dat o službách a souvisejících protokolů, aby vyhověli požadavkům spojeným s právy subjektů, kterých se data týkají. Je to pro vás a vaši organizaci, abyste se rozhodli, jestli chcete subjektu údajů poskytnout kopii osobních údajů, nebo jestli máte oprávněný podnikový důvod k jeho odmítnutí. Pokud se rozhodnete poskytnout kopii osobních dat, můžete subjektu poskytnout kopii skutečného dokumentu, upravenou verzi nebo snímek obrazovky s částí informací, které považujete za vhodné ke sdílení.

Pokud chcete exportovat osobní údaje uživatele, můžete použít: 
- Okno správy mobilních zařízení v Intune, ze kterého můžete exportovat seznam zařízení. Data o zařízeních také můžete přímo kopírovat.
- [Skript Export-IntuneData.ps1](https://aka.ms/intunedataexport).

## <a name="delete-end-user-personal-data"></a>Odstranění osobních dat koncového uživatele

Existují tři způsoby, jak odebrat osobní data spravovaná v Intune:
- Odstranění uživatele z Azure Active Directory
- Resetování zařízení do továrního nastavení
- Samostatné odebrání uživatelem

### <a name="delete-a-user-from-intune"></a>Odstranění uživatele z Intune

Pokud chcete z Intune odstranit osobní údaje koncového uživatele, správce musí [uživatele odstranit z Azure Active Directory (Azure AD)](/azure/active-directory/fundamentals/add-users-azure-active-directory#delete-a-user). Když se uživatel z Azure AD odstraní (nevratný), obdrží Intune signál odstranit z Azure AD a pak automaticky zahájí mazání všech osobních údajů tohoto uživatele ze služby Intune. Informace o uživateli budou odstraněny ze služby Intune do 30 dnů od akce odebrání.

### <a name="reset-device-to-factory-settings"></a>Resetování zařízení do továrního nastavení
Když zařízení resetujete do továrního nastavení, obnoví se všechna firemní i osobní data a nastavení do původního továrního nastavení. To je užitečné, když chcete zařízení předat dalšímu zaměstnanci. Uživatelské soubory, aplikace nainstalované uživatelem a jiné než výchozí nastavení se odeberou a tato data se ze služby Intune odstraní do 30 dnů od akce odebrání.

### <a name="user-self-removal-from-intune-management"></a>Samostatné odebrání uživatele ze správy v Intune
Uživatelé mohou odebrat osobní zařízení se systémem [Android, Apple nebo Windows](../user-help/unenroll-your-device-from-intune-android.md) ze správy v Intune i bez pomoci správce.   

### <a name="retire"></a>Vyřazení
Když zařízení **vyřadíte**, Intune odebere poskytnutá data, jako jsou firemní aplikace, data o aplikacích spravovaných v Intune, nastavení zásad a e-mailové profily zřízené prostřednictvím Intune. Tato akce opustí osobní údaje uživatele v zařízení.

### <a name="delete-a-tenant-from-microsoft-intune"></a>Odstranění tenanta z Microsoft Intune

Pokud zákazník, který používá tenanta Intune, zruší svůj účet Intune, odstraní se všechna data tenanta do 180 dnů od zavření účtu Intune zákazníkem. Pokud je tenant služby Azure AD přidružený k jiným předplatným Microsoft Enterprise (Azure, Microsoft 365), odstraní se jenom zákaznická data Intune. Prostředek tenanta Azure AD se uchovává pro použití v jiných předplatných. Pokud je účet Intune jediným předplatným přidruženým k tenantovi Azure AD, tenant se odstraní a všechny prostředky a zákaznická data se také odstraní.

## <a name="next-steps"></a>Další kroky

Zjistěte [, jak zobrazit a opravit](privacy-data-view-correct.md) osobní údaje osobních dat v Intune.
