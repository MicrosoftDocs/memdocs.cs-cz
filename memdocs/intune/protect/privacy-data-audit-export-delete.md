---
title: Audit, export a odstranění osobních dat
titleSuffix: Microsoft Intune
description: Naučte se auditovat, exportovat a odstraňovat osobní data.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/18/2018
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
ms.openlocfilehash: db3146bbaae3362e97c8c076823b58dbcd57c4af
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79325319"
---
# <a name="audit-export-or-delete-personal-data-in-intune"></a>Audit, export a odstranění osobních dat v Intune

Správci Intune mohou v protokolech auditu sledovat aktivity spojené s osobními daty. Správci také mohou osobní data exportovat a odstraňovat.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-intro-sentence.md)]

## <a name="audit-personal-data"></a>Audit osobních dat

Správci tenantů najdou v protokolech auditu zaznamenané aktivity, které v Microsoft Intune generují změnu. Protokoly auditu jsou k dispozici pro různé aktivity týkající se správy. Většinou jde o tyto akce: vytváření, aktualizace (úpravy), odstranění nebo přiřazení. Správci mohou kontrolovat také vzdálené úlohy, které generují auditované události. Protokoly auditu mohou obsahovat osobní data o uživatelích zařízení zaregistrovaných v Intune.  

Z bezpečnostních důvodů smí Intune udržovat protokoly auditu o akcích uživatelů a zařízení jenom za jeden rok. Po uplynutí ročního archivačního období budou tyto protokoly automaticky odstraněny.

Pokud chcete kontrolovat protokoly auditu, přečtěte si článek [Protokoly auditu pro aktivity v Intune](../fundamentals/monitor-audit-logs.md). 

Správci nemohou protokoly auditu odstraňovat.

Auditované události se uchovávají jeden rok. Správci tenanta si mohou vyžádat protokoly auditu vyplněním [formuláře žádosti o podporu](https://privacy.microsoft.com/en-US/privacy-questions?).

## <a name="export-personal-data"></a>Export osobních dat

Správci mohou osobní data koncových uživatelů exportovat, včetně účtů, dat o službách a souvisejících protokolů, aby vyhověli požadavkům spojeným s právy subjektů, kterých se data týkají. Vy a vaše organizace rozhodnete, jestli subjektu, kterého se data týkají, poskytnete kopii osobních dat, nebo máte oprávněné obchodní důvody, proč poskytnutí dat odmítnout. Pokud se rozhodnete poskytnout kopii osobních dat, můžete subjektu poskytnout kopii skutečného dokumentu, upravenou verzi nebo snímek obrazovky s částí informací, které považujete za vhodné ke sdílení.

K exportu osobních dat uživatele můžete použít: 
- Okno správy mobilních zařízení v Intune, ze kterého můžete exportovat seznam zařízení. Data o zařízeních také můžete přímo kopírovat.
- [Skript Export-IntuneData.ps1](https://aka.ms/intunedataexport).

## <a name="delete-end-user-personal-data"></a>Odstranění osobních dat koncového uživatele

Existují tři způsoby, jak odebrat osobní data spravovaná v Intune:
- Odstranění uživatele z Azure Active Directory
- Resetování zařízení do továrního nastavení
- Samostatné odebrání uživatelem

### <a name="delete-a-user-from-intune"></a>Odstranění uživatele z Intune

Pokud chce správce z Intune odstranit osobní data koncového uživatele, musí [ho odstranit z Azure Active Directory (AAD)](https://docs.microsoft.com/azure/active-directory/fundamentals/add-users-azure-active-directory#delete-a-user). Po trvalém odstranění uživatele z AAD obdrží Intune signál o odstranění z AAD. Na jeho základě začne ze služby Intune automaticky mazat všechna osobní data uživatele. Informace o uživateli budou ze služby Intune odstraněny do 30 dnů od jeho odebrání.

### <a name="reset-device-to-factory-settings"></a>Resetování zařízení do továrního nastavení
Když zařízení resetujete do továrního nastavení, obnoví se všechna firemní i osobní data a nastavení do původního továrního nastavení. To je užitečné, když chcete zařízení předat dalšímu zaměstnanci. Do 30 dnů od odebrání uživatele budou ze služby Intune odstraněny uživatelské soubory, aplikace instalované uživatelem a veškeré nastavení, které není výchozí.

### <a name="user-self-removal-from-intune-management"></a>Samostatné odebrání uživatele ze správy v Intune
Uživatelé mohou odebrat osobní zařízení se systémem [Android, Apple nebo Windows](https://docs.microsoft.com/user-help/unenroll-your-device-from-intune-android) ze správy v Intune i bez pomoci správce.   

### <a name="retire"></a>Vyřadit
Když zařízení **vyřadíte**, Intune odebere poskytnutá data, jako jsou firemní aplikace, data o aplikacích spravovaných v Intune, nastavení zásad a e-mailové profily zřízené prostřednictvím Intune. Při této akci zůstanou v zařízení osobní data uživatele.

### <a name="delete-a-tenant-from-microsoft-intune"></a>Odstranění tenanta z Microsoft Intune

Pokud zákazník, který používá tenanta Intune, zruší svůj účet Intune, odstraní se všechna data tenanta do 180 dnů od zavření účtu Intune zákazníkem. Pokud má tenant AAD přidružené jiné podnikové předplatné Microsoftu (třeba Azure nebo Ofice 365), odstraní se jenom data zákazníka Intune. Tenant AAD se zachová, aby ho mohla využívat jiná předplatná. Pokud má tenant AAD přidružené jenom předplatné účtu Intune, bude odstraněn tenant, všechny prostředky i zákazníkova data.

## <a name="next-steps"></a>Další kroky

Přečtete si, jak [auditovat, exportovat nebo odstranit](privacy-data-audit-export-delete.md) osobní data evidovaná v Intune.
